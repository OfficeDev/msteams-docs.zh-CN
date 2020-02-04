---
title: 使用 ASP.NET Core 创建个人选项卡
author: laujan
description: 用于创建带有 ASP.NET Core 的自定义个人选项卡的快速入门指南。
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: b279c96f47265fe1928ae90d661e7dc042085b39
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673459"
---
# <a name="create-a-custom-personal-tab-with-aspnet-core"></a>使用 ASP.NET Core 创建自定义个人选项卡

在此快速入门中，我们将介绍如何创建包含 c # 和 ASP.Net Core Razor 页面的自定义个人选项卡。 我们还将使用[Microsoft 团队的应用 Studio](~/concepts/build-and-test/app-studio-overview.md)来完成你的应用程序清单，并将你的选项卡部署到团队。

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>获取源代码

打开命令提示符并为您的选项卡项目创建一个新目录。 我们提供了一个简单的项目，可帮助你入门。 若要检索源代码，可以下载 zip 文件夹并解压缩文件，或将示例存储库克隆到新目录：

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

拥有源代码后，打开 Visual Studio 并选择 "**打开项目或解决方案**"。 导航到 "选项卡应用程序目录"，然后打开 " **PersonalTab**"。

若要生成并运行应用程序，请按**F5**或从 "**调试**" 菜单中选择 "**启动调试**"。 在浏览器中导航到以下 Url，以验证是否正确加载了应用程序：

- `http://localhost:44325/`
- `http://localhost:44325/personal`
- `http://localhost:44325/privacy`
- `http://localhost:44325/tou`

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

### <a name="appmanifest-folder"></a>Appmanifest.xml 文件夹

此文件夹包含以下所需的应用程序包文件：

- 以 192 x 192 像素为单位的**完整彩色图标**。
- 一个**透明的大纲图标**，用于度量 32 x 32 像素。
- 一个指定应用程序的属性的**清单 json**文件。

需要将这些文件压缩到应用程序包中，以便在将选项卡上载到团队时使用。 Microsoft 团队将加载清单`contentUrl`中指定的项，将其嵌入 IFrame 中，并在您的选项卡中呈现。

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

[!INCLUDE  [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- 在项目目录的根目录中打开命令提示符，并运行以下命令：

```bash
ngrok http https://localhost:44325 -host-header="localhost:44325"
```

- Ngrok 将侦听来自 internet 的请求，并在其运行在端口44325上时将它们路由到您的应用程序。  它应类似`https://y8rPrT2b.ngrok.io/`于在*y8rPrT2b*替换为 NGROK 字母数字 HTTPS URL 的位置。

- 请务必在运行命令提示符时保留 ngrok，并记下该 URL，稍后将需要它。

- 通过在命令提示符窗口中提供的 ngrok HTTPS URL 打开浏览器并转到内容页，验证*ngrok*是否正在运行并正常运行。

>[!TIP]
>您需要在 Visual Studio 和 ngrok 中同时运行应用程序，才能完成此快速入门。 如果需要在 Visual Studio 中停止运行应用程序以进行处理，请**保持 ngrok 运行状态**。 它将继续侦听，并将在 Visual Studio 中重新启动时继续路由应用程序的请求。 如果您必须重新启动 ngrok 服务，它将返回一个新的 URL，您必须更新使用该 URL 的每个位置。

### <a name="run-your-application"></a>运行应用程序

- 在 Visual Studio 中，按**F5**或从应用程序的 "**调试**" 菜单中选择 "**启动调试**"。

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]
