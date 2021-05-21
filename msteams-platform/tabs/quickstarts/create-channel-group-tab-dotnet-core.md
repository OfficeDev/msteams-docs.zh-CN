---
title: 创建包含"频道和组"选项卡 ASP.NET Core
author: laujan
description: 使用自定义频道和组选项卡创建自定义频道和组选项卡的快速 ASP.NET Core。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: f748335b621e9bc93272aaeb8d7e12ecc3ebbee0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52580447"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnetcore"></a>使用 ASP.NETCore 创建自定义频道和组选项卡

在此快速入门中，我们将演练创建自定义频道/组选项卡，该选项卡包含C#和 ASP.Net Core 用户页面。 我们还将使用 App [Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md)完成应用清单，并部署选项卡以Teams。

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>获取源代码

打开命令提示符，为选项卡项目创建新目录。 我们提供了一个简单的项目，让你开始操作。 若要检索源代码，可以下载 zip 文件夹并提取文件或将示例存储库克隆到新目录中：

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

获得源代码后，打开"Visual Studio并选择"**打开项目或解决方案"。** 导航到选项卡应用程序目录，然后打开 **ChannelGroupTab.sln**。

若要生成并运行应用程序，请按 **F5** 或从"调试 **"** 菜单中选择"开始 **调试** "。 在浏览器中，导航到下面的 URL 并验证应用程序是否加载正确：

- `http://localhost:44355`
- `http://localhost:44355/privacy`
- `http://localhost:44355/tou`

## <a name="review-the-source-code"></a>查看源代码

### <a name="startupcs"></a>Startup.cs

此项目从 2.2 web 应用程序 ASP.NET Core模板创建，在设置时选中了"高级 *- 为 HTTPS* 配置"复选框。 MVC 服务由依赖关系注入框架的方法 `ConfigureServices()` 注册。 此外，默认情况下，空模板不支持为静态内容提供服务，因此静态文件中间件将添加到 `Configure()` 方法：

```csharp
public void ConfigureServices(IServiceCollection services)
  {
    services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
  }
public void Configure(IApplicationBuilder app)
  {
    app.UseStaticFiles();
    app.UseMvc();
  }
```

### <a name="wwwroot-folder"></a>wwwroot 文件夹

在 ASP.NET Core中，Web 根文件夹是应用程序查找静态文件的位置。

### <a name="indexcshtml"></a>Index.cshtml

ASP.NET Core将名为 *Index* 的文件视为网站的默认/主页。 当浏览器 URL 指向网站的根目录时 **，Index.cshtml** 将显示为应用程序的主页。

### <a name="tabcs"></a>Tab.cs

此C#文件包含将在配置期间从 **Tab.cshtml** 调用的方法。

### <a name="appmanifest-folder"></a>AppManifest 文件夹

此文件夹包含以下所需的应用包文件：

- 全 **色图标** ，大小为 192 x 192 像素。
- 一 **个 32** x 32 像素的透明边框图标。
- 指定 **manifest.js** 属性的 on 文件。

这些文件需要在应用包中压缩，以用于将选项卡上载到Teams。 当用户选择添加或更新选项卡时，Microsoft Teams将加载清单中指定的，将其嵌入 IFrame 中，并将其 `configurationUrl` 呈现在选项卡中。

### <a name="csproj"></a>.csproj

在"Visual Studio资源管理器"窗口中，右键单击项目并选择"编辑Project **文件"。** 在文件底部，你将看到在应用程序生成时创建和更新 zip 文件夹的代码：

```xml
<PropertyGroup>
    <PostBuildEvent>powershell.exe Compress-Archive -Path \"$(ProjectDir)AppManifest\*\" -DestinationPath \"$(TargetDir)tab.zip\" -Force</PostBuildEvent>
  </PropertyGroup>

  <ItemGroup>
    <EmbeddedResource Include="AppManifest\icon-outline.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\icon-color.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\manifest.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
  </ItemGroup>
```

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- 打开项目目录根目录中的命令提示符并运行以下命令：

    ```bash
    ngrok http https://localhost:44355 -host-header="localhost:44355"
    ```

- Ngrok 将侦听来自 Internet 的请求，并且将在应用程序在端口 44355 上运行时将它们路由到您的应用程序。 它应 `https://y8rCgT2b.ngrok.io/` 类似于 *y8rCgT2b* 替换为 ngrok 字母数字 HTTPS URL。

- 请确保使命令提示符保持运行 ngrok 并记下 URL，稍后将需要它。

## <a name="update-your-application"></a>更新应用程序

在 *Tab.cshtml* 中，应用程序向用户显示两个选项按钮，用于显示带红色或灰色图标的选项卡。 选择" **选择灰色"** 或 **"选择红色** "按钮将分别触发或 ，设置 并启用配置页上的 `saveGray()` `saveRed()` `settings.setValidityState(true)` **"** 保存"按钮。 此代码Teams您满足配置要求，并且安装可以继续。 保存时，将设置 `settings.setSettings` 的参数。 最后 `saveEvent.notifySuccess()` ，调用 以指示已成功解析内容 URL。

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 ASP.NETCore MVC 创建自定义频道和组选项卡](~/tabs/quickstarts/create-channel-group-tab-dotnet-core-mvc.md)