---
title: 使用 ASP.NET Core 创建个人选项卡
author: laujan
description: 用于创建带有 ASP.NET Core 的自定义个人选项卡的快速入门指南。
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 39f45dd79606d1416f3924d01f75c5bedc11bfba
ms.sourcegitcommit: 43e1be9d9e3651ce73a8d2139e44d75550a0ca60
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2020
ms.locfileid: "49476936"
---
# <a name="create-a-personal-tab-with-aspnet-core"></a><span data-ttu-id="673f7-103">使用 ASP.NET Core 创建个人选项卡</span><span class="sxs-lookup"><span data-stu-id="673f7-103">Create a personal tab with ASP.NET Core</span></span>

<span data-ttu-id="673f7-104">在此快速入门中，我们将介绍如何创建包含 c # 和 ASP.Net Core Razor 页面的自定义个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="673f7-104">In this quickstart, we'll walk-through creating a custom personal tab with C# and ASP.Net Core Razor pages.</span></span> <span data-ttu-id="673f7-105">我们还将使用 [Microsoft 团队的应用 Studio](~/concepts/build-and-test/app-studio-overview.md) 来完成你的应用程序清单，并将你的选项卡部署到团队。</span><span class="sxs-lookup"><span data-stu-id="673f7-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="673f7-106">获取源代码</span><span class="sxs-lookup"><span data-stu-id="673f7-106">Get the source code</span></span>

<span data-ttu-id="673f7-107">打开命令提示符并为您的选项卡项目创建一个新目录。</span><span class="sxs-lookup"><span data-stu-id="673f7-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="673f7-108">我们提供了一个简单的项目，可帮助你入门。</span><span class="sxs-lookup"><span data-stu-id="673f7-108">We have provided a simple project to get you started.</span></span> <span data-ttu-id="673f7-109">若要检索源代码，可以下载 zip 文件夹并解压缩文件，或将示例存储库克隆到新目录：</span><span class="sxs-lookup"><span data-stu-id="673f7-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="673f7-110">拥有源代码后，打开 Visual Studio 并选择 " **打开项目或解决方案**"。</span><span class="sxs-lookup"><span data-stu-id="673f7-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="673f7-111">导航到 "选项卡应用程序目录"，然后打开 " **PersonalTab**"。</span><span class="sxs-lookup"><span data-stu-id="673f7-111">Navigate to the tab application directory and open **PersonalTab.sln**.</span></span>

<span data-ttu-id="673f7-112">若要生成并运行应用程序，请按 **F5** 或从 "**调试**" 菜单中选择 "**启动调试**"。</span><span class="sxs-lookup"><span data-stu-id="673f7-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="673f7-113">在浏览器中导航到以下 Url，以验证是否正确加载了应用程序：</span><span class="sxs-lookup"><span data-stu-id="673f7-113">In a browser navigate to the URLs below to verify the application loaded properly:</span></span>

- `http://localhost:44325/`
- `http://localhost:44325/personal`
- `http://localhost:44325/privacy`
- `http://localhost:44325/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="673f7-114">查看源代码</span><span class="sxs-lookup"><span data-stu-id="673f7-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="673f7-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="673f7-115">Startup.cs</span></span>

<span data-ttu-id="673f7-116">此项目是从 ASP.NET Core 2.2 Web 应用程序空模板创建的，并且在安装程序中选中了 " *高级-配置为 HTTPS* " 复选框。</span><span class="sxs-lookup"><span data-stu-id="673f7-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="673f7-117">MVC 服务由依赖关系注入框架的 `ConfigureServices()` 方法注册。</span><span class="sxs-lookup"><span data-stu-id="673f7-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="673f7-118">此外，默认情况下，空模板不启用静态内容的服务，因此将静态文件中间件添加到 `Configure()` 方法中：</span><span class="sxs-lookup"><span data-stu-id="673f7-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="673f7-119">wwwroot 文件夹</span><span class="sxs-lookup"><span data-stu-id="673f7-119">wwwroot folder</span></span>

<span data-ttu-id="673f7-120">在 ASP.NET Core 中，web 根文件夹是应用程序查找静态文件的位置。</span><span class="sxs-lookup"><span data-stu-id="673f7-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="indexcshtml"></a><span data-ttu-id="673f7-121">索引 cshtml</span><span class="sxs-lookup"><span data-stu-id="673f7-121">Index.cshtml</span></span>

<span data-ttu-id="673f7-122">ASP.NET Core 将称为 *Index* 的文件视为网站的默认/主页。</span><span class="sxs-lookup"><span data-stu-id="673f7-122">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="673f7-123">当浏览器 URL 指向网站的根目录时，将显示 **索引. cshtml** 将显示为应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="673f7-123">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="673f7-124">Appmanifest.xml 文件夹</span><span class="sxs-lookup"><span data-stu-id="673f7-124">AppManifest folder</span></span>

<span data-ttu-id="673f7-125">此文件夹包含以下所需的应用程序包文件：</span><span class="sxs-lookup"><span data-stu-id="673f7-125">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="673f7-126">以 192 x 192 像素为单位的 **完整彩色图标** 。</span><span class="sxs-lookup"><span data-stu-id="673f7-126">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="673f7-127">一个 **透明的大纲图标** ，用于度量 32 x 32 像素。</span><span class="sxs-lookup"><span data-stu-id="673f7-127">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="673f7-128">指定应用程序属性的文件 **上的manifest.js** 。</span><span class="sxs-lookup"><span data-stu-id="673f7-128">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="673f7-129">需要将这些文件压缩到应用程序包中，以便在将选项卡上载到团队时使用。</span><span class="sxs-lookup"><span data-stu-id="673f7-129">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="673f7-130">Microsoft 团队将 `contentUrl` 在清单中加载指定的，将其嵌入到 <iframe 中， \> 并在您的选项卡中进行呈现。</span><span class="sxs-lookup"><span data-stu-id="673f7-130">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an <iframe\>, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="673f7-131">.csproj</span><span class="sxs-lookup"><span data-stu-id="673f7-131">.csproj</span></span>

<span data-ttu-id="673f7-132">在 Visual Studio "解决方案资源管理器" 窗口中，右键单击该项目，然后选择 " **编辑项目文件**"。</span><span class="sxs-lookup"><span data-stu-id="673f7-132">In the Visual Studio Solution Explorer window, right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="673f7-133">在该文件的底部，您将看到在应用程序生成时创建和更新您的 zip 文件夹的代码：</span><span class="sxs-lookup"><span data-stu-id="673f7-133">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

- <span data-ttu-id="673f7-134">在项目目录的根目录中打开命令提示符，并运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="673f7-134">Open a command prompt in the root of your project directory and run the following command:</span></span>

```bash
ngrok http https://localhost:44325 -host-header="localhost:44325"
```

- <span data-ttu-id="673f7-135">Ngrok 将侦听来自 internet 的请求，并在其运行在端口44325上时将它们路由到您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="673f7-135">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="673f7-136">它应类似于 `https://y8rPrT2b.ngrok.io/` 在 *y8rPrT2b* 替换为 NGROK 字母数字 HTTPS URL 的位置。</span><span class="sxs-lookup"><span data-stu-id="673f7-136">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="673f7-137">请务必在运行命令提示符时保留 ngrok，并记下该 URL，稍后将需要它。</span><span class="sxs-lookup"><span data-stu-id="673f7-137">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

- <span data-ttu-id="673f7-138">通过在命令提示符窗口中提供的 ngrok HTTPS URL 打开浏览器并转到内容页，验证 *ngrok* 是否正在运行并正常运行。</span><span class="sxs-lookup"><span data-stu-id="673f7-138">Verify that *ngrok* is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

>[!TIP]
><span data-ttu-id="673f7-139">您需要在 Visual Studio 和 ngrok 中同时运行应用程序，才能完成此快速入门。</span><span class="sxs-lookup"><span data-stu-id="673f7-139">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="673f7-140">如果需要在 Visual Studio 中停止运行应用程序以进行处理，请 **保持 ngrok 运行状态**。</span><span class="sxs-lookup"><span data-stu-id="673f7-140">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="673f7-141">它将继续侦听，并将在 Visual Studio 中重新启动时继续路由应用程序的请求。</span><span class="sxs-lookup"><span data-stu-id="673f7-141">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="673f7-142">如果您必须重新启动 ngrok 服务，它将返回一个新的 URL，您必须更新使用该 URL 的每个位置。</span><span class="sxs-lookup"><span data-stu-id="673f7-142">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="673f7-143">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="673f7-143">Run your application</span></span>

- <span data-ttu-id="673f7-144">在 Visual Studio 中，按 **F5** 或从应用程序的 "**调试**" 菜单中选择 "**启动调试**"。</span><span class="sxs-lookup"><span data-stu-id="673f7-144">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]
