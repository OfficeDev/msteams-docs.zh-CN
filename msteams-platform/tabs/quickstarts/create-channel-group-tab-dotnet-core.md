---
title: 使用 ASP.NET Core 创建通道和组选项卡
author: laujan
description: 用于创建带有 ASP.NET Core 的自定义频道和分组选项卡的快速入门指南。
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: 7fdc4b042aac0664ae9d62c73c90689c75823592
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673474"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core"></a>使用 ASP.NET Core 创建自定义通道和组选项卡

在此快速入门中，我们将介绍如何使用 c # 和 ASP.Net Core Razor 页创建自定义频道/组选项卡。 我们还将使用[Microsoft 团队的应用 Studio](~/concepts/build-and-test/app-studio-overview.md)来完成你的应用程序清单，并将你的选项卡部署到团队。

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>获取源代码

打开命令提示符并为您的选项卡项目创建一个新目录。 我们提供了一个简单的项目，可帮助你入门。 若要检索源代码，可以下载 zip 文件夹并解压缩文件，或将示例存储库克隆到新目录：

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

拥有源代码后，打开 Visual Studio 并选择 "**打开项目或解决方案**"。 导航到 "选项卡应用程序目录"，然后打开 " **ChannelGroupTab**"。

若要生成并运行应用程序，请按**F5**或从 "**调试**" 菜单中选择 "**启动调试**"。 在浏览器中导航到以下 Url 并验证是否正确加载了应用程序：

- `http://localhost:44355`
- `http://localhost:44355/privacy`
- `http://localhost:44355/tou`

## <a name="review-the-source-code"></a>查看源代码

### <a name="startupcs"></a>Startup.cs

此项目是从 ASP.NET Core 2.2 Web 应用程序空模板创建的，并且在安装程序中选中了 "*高级-配置为 HTTPS* " 复选框。 MVC 服务由依赖关系注入框架的`ConfigureServices()`方法注册。 此外，默认情况下，空模板不启用静态内容的服务，因此将静态文件中间件添加`Configure()`到方法中：

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

在 ASP.NET Core 中，web 根文件夹是应用程序查找静态文件的位置。

### <a name="indexcshtml"></a>索引 cshtml

ASP.NET Core 将称为*Index*的文件视为网站的默认/主页。 当浏览器 URL 指向网站的根目录时，将显示**索引. cshtml**将显示为应用程序的主页。

### <a name="tabcs"></a>Tab.cs

此 c # 文件包含在配置过程中将从**选项卡**调用的方法。

### <a name="appmanifest-folder"></a>Appmanifest.xml 文件夹

此文件夹包含以下所需的应用程序包文件：

- 以 192 x 192 像素为单位的**完整彩色图标**。
- 一个**透明的大纲图标**，用于度量 32 x 32 像素。
- 一个指定应用程序的属性的**清单 json**文件。

需要将这些文件压缩到应用程序包中，以便在将选项卡上载到团队时使用。 当用户选择添加或更新选项卡时，Microsoft 团队将加载清单中`configurationUrl`指定的项，将其嵌入 IFrame 中，并在您的选项卡中进行呈现。

### <a name="csproj"></a>.csproj

在 Visual Studio "解决方案资源管理器" 窗口中，右键单击该项目，然后选择 "**编辑项目文件**"。 在该文件的底部，您将看到在应用程序生成时创建和更新您的 zip 文件夹的代码：

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

- 在项目目录的根目录中打开命令提示符，并运行以下命令：

```bash
ngrok http https://localhost:44355 -host-header="localhost:44355"
```

- Ngrok 将侦听来自 internet 的请求，并在其运行在端口44355上时将它们路由到您的应用程序。 它应类似`https://y8rCgT2b.ngrok.io/`于在*y8rCgT2b*替换为 NGROK 字母数字 HTTPS URL 的位置。

- 请务必在 ngrok 运行的同时保留命令提示符，并记下该 URL，稍后将需要它。

## <a name="update-your-application"></a>更新应用程序

在*选项卡中。 cshtml*应用程序为用户提供了两个选项按钮，用于显示带有红色或灰色图标的选项卡。 选择 "**选择灰色**" 或 "**选择红色**" `saveGray()`按钮将触发或`settings.setValidityState(true)` `saveRed()`分别设置和启用 "配置" 页上的 "**保存**" 按钮。 此代码使团队知道您已经满足配置要求，可以继续安装。 在保存`settings.setSettings`时设置的参数。 最后， `saveEvent.notifySuccess()`将调用，以指示内容 URL 已成功解析。

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

[!INCLUDE [dotnet-upload-to-teams](~/includes/tabs/dotnet-upload-to-teams.md)]
