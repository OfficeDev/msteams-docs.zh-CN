---
title: 使用 ASP 创建个人选项卡。 NET Core MVC
author: laujan
description: 使用 ASP 创建自定义个人选项卡的快速入门指南。 NET Core MVC。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 01418adb32335660bb20f74ecfaa0e7e27230c93
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566622"
---
# <a name="create-a-custom-personal-tab-with-aspnet-core-mvc"></a>使用 MVC 创建自定义个人 ASP.NET Core选项卡

在此快速入门中，我们将演练使用 C# 和 core MVC ASP.Net 自定义个人选项卡。 我们还将使用 App [Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md)完成应用清单，并部署选项卡以Teams。

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>获取源代码

打开命令提示符，为选项卡项目创建新目录。 我们提供了一个简单的项目，让你开始操作。 若要检索源代码，可以下载 zip 文件夹并提取文件或将示例存储库克隆到新目录中：

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

获得源代码后，打开"Visual Studio并选择"**打开项目或解决方案"。** 导航到选项卡应用程序目录，然后打开 **PersonalTabMVC.sln**。

若要生成并运行应用程序，请按 **F5** 或从"调试 **"** 菜单中选择"开始 **调试** "。 在浏览器中，导航到下面的 URL 以验证应用程序是否加载正确：

* `http://localhost:44335`
* `http://localhost:44335/privacy`
* `http://localhost:44335/tou`

## <a name="review-the-source-code"></a>查看源代码

### <a name="startupcs"></a>Startup.cs

此项目是使用 ASP 创建的。 NET Core 2.2 Web 应用程序空模板，在设置时选中了"高级 *- 配置 HTTPS"* 复选框。 MVC 服务由依赖关系注入框架的方法 `ConfigureServices()` 注册。 此外，默认情况下，空模板不支持为静态内容提供服务，因此静态文件中间件将添加到 `Configure()` 方法：

``` csharp
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

在 ASP 中。 NET Core，Web 根文件夹是应用程序查找静态文件的位置。

### <a name="appmanifest-folder"></a>AppManifest 文件夹

此文件夹包含以下所需的应用包文件：

* 全 **色图标** ，大小为 192 x 192 像素。
* 一 **个 32** x 32 像素的透明边框图标。
* 指定 **manifest.js** 属性的 on 文件。

这些文件需要在应用包中压缩，以用于将选项卡上载到Teams。 Microsoft Teams将加载清单中指定的 ，将其嵌入 `contentUrl` IFrame，并将其呈现在选项卡中。

### <a name="csproj"></a>.csproj

在"Visual Studio资源管理器"窗口中，右键单击项目并选择"编辑Project **文件"。** 在文件底部，你将看到在应用程序生成时创建和更新 zip 文件夹的代码：

``` xml
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

**PersonalTab.cs** 提供 Message 对象和方法，当用户在 PersonalTab 视图中选择按钮时，该对象和方法将从 *PersonalTabController* 调用。 

### <a name="views"></a>视图

#### <a name="home"></a>主页

ASP。 NET Core 将名为 **Index** 的文件视为网站的默认页面或主页。 当浏览器 URL 指向网站的根目录时 **，Index.cshtml** 将显示为应用程序的主页。

#### <a name="shared"></a>共享的内容

部分视图标记 *_Layout.cshtml* 包含应用程序的整体页面结构和共享的可视元素。 它还将引用Teams库。

### <a name="controllers"></a>控制器

控制器使用 ViewBag 属性将值动态传输给视图。

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* 打开项目目录根目录中的命令提示符并运行以下命令：

    ``` bash
    ngrok http https://localhost:44345 -host-header="localhost:44345"
    ```

* Ngrok 将侦听来自 Internet 的请求，并且将在应用程序在端口 44325 上运行时将它们路由到您的应用程序。  它应 `https://y8rPrT2b.ngrok.io/` 类似于 *y8rPrT2b* 替换为 ngrok 字母数字 HTTPS URL。

* 请确保使命令提示符保持运行 ngrok，并记下 URL，稍后将需要它。

* 通过打开浏览器，然后通过命令提示符窗口中提供的 ngrok HTTPS URL 进入内容页面，验证 **ngrok** 是否正常运行。

> [!TIP]
> 你需要让应用程序在 Visual Studio 和 ngrok 中运行才能完成此快速入门。 如果需要停止运行应用程序，Visual Studio运行应用程序，请 **保持 ngrok 运行**。 当应用程序在服务器中重新启动时，它将继续侦听并Visual Studio。 如果必须重新启动 ngrok 服务，它将返回一个新 URL，并且必须更新使用该 URL 的每一处。

### <a name="run-your-application"></a>运行应用程序

* In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [使用自定义频道和组选项卡，Node.js Yeoman 生成器进行Microsoft Teams](~/tabs/quickstarts/create-channel-group-tab-node-yeoman.md)
