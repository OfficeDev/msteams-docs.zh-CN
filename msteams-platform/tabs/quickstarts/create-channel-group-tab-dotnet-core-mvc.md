---
title: 使用 MVC 创建频道和 ASP.NET Core选项卡
author: laujan
description: 使用 MVC 创建自定义频道和组选项卡 ASP.NET Core指南
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 9d89fd98bae9732a8f9e2d34b82d7fc0e6985e01
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020308"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core-mvc"></a>使用 MVC 创建自定义频道和组 ASP.NET Core选项卡

在此快速入门中，我们将演练使用核心 MVC 创建自定义频道/C#ASP.Net 选项卡。 我们还将使用 App [Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md)完成应用清单，并部署选项卡以Teams。

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>获取源代码

打开命令提示符，为选项卡项目创建新目录。 我们提供了一个简单的 ["频道组选项卡](https://github.com/OfficeDev/microsoft-teams-sample-tabs/ChannelGroupTabMVC) "项目，让你开始操作。 若要检索源代码，可以下载 zip 文件夹并提取文件或将示例存储库克隆到新目录中：

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

获得源代码后，打开"Visual Studio并选择"**打开项目或解决方案"。** 导航到选项卡应用程序目录，然后打开 **ChannelGroupTabMVC.sln**。

若要生成并运行应用程序，请按 **F5** 或从"调试 **"** 菜单中选择"开始 **调试** "。 在浏览器中，导航到下面的 URL 并验证应用程序是否加载正确：

- `http://localhost:44360`
- `http://localhost:44360/privacy`
- `http://localhost:44360/tou`

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

### <a name="appmanifest-folder"></a>AppManifest 文件夹

此文件夹包含以下所需的应用包文件：

- 全 **色图标** ，大小为 192 x 192 像素。
- 一 **个 32** x 32 像素的透明边框图标。
- 指定 **manifest.js** 属性的 on 文件。

这些文件需要在应用包中压缩，以用于将选项卡上载到Teams。

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

### <a name="models"></a>模型

*ChannelGroup.cs* 提供 Message 对象和方法，将在配置期间从控制器调用该对象和方法。

### <a name="views"></a>视图

#### <a name="home"></a>主页

ASP.NET Core将名为 *Index* 的文件视为网站的默认/主页。 当浏览器 URL 指向网站的根目录时 **，Index.cshtml** 将显示为应用程序的主页。

#### <a name="shared"></a>共享的内容

部分视图标记 *_Layout.cshtml* 包含应用程序的整体页面结构和共享的可视元素。 它还将引用Teams库。

### <a name="controllers"></a>控制器

控制器使用 ViewBag 属性将值动态传输给视图。

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- 打开项目目录根目录中的命令提示符并运行以下命令：

```bash
ngrok http https://localhost:443560 -host-header="localhost:44360"
```

- Ngrok 将侦听来自 Internet 的请求，并且将在应用程序在端口 44355 上运行时将它们路由到您的应用程序。  它应 `https://y8rCgT2b.ngrok.io/` 类似于 *y8rCgT2b* 替换为 ngrok 字母数字 HTTPS URL。

- 请确保使命令提示符保持运行 ngrok 并记下 URL，稍后将需要它。

## <a name="update-your-application"></a>更新应用程序

在 **Tab.cshtml** 中，应用程序向用户显示两个选项按钮，用于显示带红色或灰色图标的选项卡。 选择" **选择灰色"** 或 **"选择红色** "按钮将分别触发或 ，设置 并启用配置页上的 `saveGray()` `saveRed()` `settings.setValidityState(true)` **"** 保存"按钮。 此代码Teams您满足配置要求，并且安装可以继续。 保存时，将设置 `settings.setSettings` 的参数。 最后 `saveEvent.notifySuccess()` ，调用 以指示已成功解析内容 URL。

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

[!INCLUDE [dotnet-upload-to-teams](~/includes/tabs/dotnet-upload-to-teams.md)]
