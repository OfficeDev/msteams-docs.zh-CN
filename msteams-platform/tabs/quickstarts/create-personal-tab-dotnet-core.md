---
title: 使用"个人"选项卡创建 ASP.NET Core
author: laujan
description: 使用自定义选项卡创建自定义个人选项卡的快速 ASP.NET Core。
ms.topic: quickstart
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 41aa916f4c69d50e48254d0f4934109429dab83c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566892"
---
# <a name="create-a-personal-tab-using-aspnetcore"></a><span data-ttu-id="3fdbb-103">使用 ASP.NETCore 创建个人选项卡</span><span class="sxs-lookup"><span data-stu-id="3fdbb-103">Create a personal tab using ASP.NETCore</span></span>

<span data-ttu-id="3fdbb-104">在此快速入门中，我们将演练创建自定义个人选项卡，该选项卡包含C#和 ASP.Net Core 用户页面。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-104">In this quickstart, we'll walk-through creating a custom personal tab with C# and ASP.Net Core Razor pages.</span></span> <span data-ttu-id="3fdbb-105">我们还将使用 App [Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md)完成应用清单，并部署选项卡以Teams。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="3fdbb-106">获取源代码</span><span class="sxs-lookup"><span data-stu-id="3fdbb-106">Get the source code</span></span>

<span data-ttu-id="3fdbb-107">打开命令提示符，为选项卡项目创建新目录。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="3fdbb-108">我们提供了一个简单的项目，让你开始操作。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-108">We have provided a simple project to get you started.</span></span> <span data-ttu-id="3fdbb-109">若要检索源代码，可以下载 zip 文件夹并提取文件或将示例存储库克隆到新目录中：</span><span class="sxs-lookup"><span data-stu-id="3fdbb-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="3fdbb-110">获得源代码后，打开"Visual Studio并选择"**打开项目或解决方案"。**</span><span class="sxs-lookup"><span data-stu-id="3fdbb-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="3fdbb-111">导航到选项卡应用程序目录，然后打开 **PersonalTab.sln**。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-111">Navigate to the tab application directory and open **PersonalTab.sln**.</span></span>

<span data-ttu-id="3fdbb-112">若要生成并运行应用程序，请按 **F5** 或从"调试 **"** 菜单中选择"开始 **调试** "。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="3fdbb-113">在浏览器中，导航到下面的 URL 以验证应用程序是否加载正确：</span><span class="sxs-lookup"><span data-stu-id="3fdbb-113">In a browser navigate to the URLs below to verify the application loaded properly:</span></span>

- `http://localhost:44325/`
- `http://localhost:44325/personal`
- `http://localhost:44325/privacy`
- `http://localhost:44325/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="3fdbb-114">查看源代码</span><span class="sxs-lookup"><span data-stu-id="3fdbb-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="3fdbb-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="3fdbb-115">Startup.cs</span></span>

<span data-ttu-id="3fdbb-116">此项目从 2.2 web 应用程序 ASP.NET Core模板创建，在设置时选中了"高级 **- 为 HTTPS** 配置"复选框。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the **Advanced - Configure for HTTPS** check box selected at setup.</span></span> <span data-ttu-id="3fdbb-117">MVC 服务由依赖关系注入框架的方法 `ConfigureServices()` 注册。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="3fdbb-118">此外，默认情况下，空模板不支持为静态内容提供服务，因此静态文件中间件将添加到 `Configure()` 方法：</span><span class="sxs-lookup"><span data-stu-id="3fdbb-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="3fdbb-119">wwwroot 文件夹</span><span class="sxs-lookup"><span data-stu-id="3fdbb-119">wwwroot folder</span></span>

<span data-ttu-id="3fdbb-120">在 ASP.NET Core中，Web 根文件夹是应用程序查找静态文件的位置。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="indexcshtml"></a><span data-ttu-id="3fdbb-121">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="3fdbb-121">Index.cshtml</span></span>

<span data-ttu-id="3fdbb-122">ASP.NET Core将名为 *Index* 的文件视为网站的默认/主页。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-122">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="3fdbb-123">当浏览器 URL 指向网站的根目录时 **，Index.cshtml** 将显示为应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-123">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="3fdbb-124">AppManifest 文件夹</span><span class="sxs-lookup"><span data-stu-id="3fdbb-124">AppManifest folder</span></span>

<span data-ttu-id="3fdbb-125">此文件夹包含以下所需的应用包文件：</span><span class="sxs-lookup"><span data-stu-id="3fdbb-125">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="3fdbb-126">全 **色图标** ，大小为 192 x 192 像素。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-126">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="3fdbb-127">一 **个 32** x 32 像素的透明边框图标。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-127">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="3fdbb-128">指定 **manifest.js** 属性的 on 文件。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-128">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="3fdbb-129">这些文件需要在应用包中压缩，以用于将选项卡上载到Teams。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-129">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="3fdbb-130">Microsoft Teams清单中加载指定的 ，将其嵌入 <`contentUrl` iframe 中，并将其 \> 呈现在选项卡中。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-130">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an <iframe\>, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="3fdbb-131">.csproj</span><span class="sxs-lookup"><span data-stu-id="3fdbb-131">.csproj</span></span>

<span data-ttu-id="3fdbb-132">在"Visual Studio资源管理器"窗口中，右键单击项目并选择"编辑Project **文件"。**</span><span class="sxs-lookup"><span data-stu-id="3fdbb-132">In the Visual Studio Solution Explorer window, right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="3fdbb-133">在文件底部，你将看到在应用程序生成时创建和更新 zip 文件夹的代码：</span><span class="sxs-lookup"><span data-stu-id="3fdbb-133">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

- <span data-ttu-id="3fdbb-134">打开项目目录根目录中的命令提示符并运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="3fdbb-134">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ```bash
    ngrok http https://localhost:44325 -host-header="localhost:44325"
    ```

- <span data-ttu-id="3fdbb-135">Ngrok 将侦听来自 Internet 的请求，并且将在应用程序在端口 44325 上运行时将它们路由到您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-135">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="3fdbb-136">它应 `https://y8rPrT2b.ngrok.io/` 类似于 *y8rPrT2b* 替换为 ngrok 字母数字 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-136">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="3fdbb-137">请确保使命令提示符保持运行 ngrok，并记下 URL，稍后将需要它。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-137">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

- <span data-ttu-id="3fdbb-138">通过打开浏览器，然后通过命令提示符窗口中提供的 ngrok HTTPS URL 进入内容页面，验证 **ngrok** 是否正常运行。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-138">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

>[!TIP]
><span data-ttu-id="3fdbb-139">你需要让应用程序在 Visual Studio 和 ngrok 中运行才能完成此快速入门。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-139">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="3fdbb-140">如果需要停止运行应用程序，Visual Studio运行应用程序，请 **保持 ngrok 运行**。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-140">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="3fdbb-141">当应用程序在服务器中重新启动时，它将继续侦听并Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-141">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="3fdbb-142">如果必须重新启动 ngrok 服务，它将返回一个新 URL，并且必须更新使用该 URL 的每一处。</span><span class="sxs-lookup"><span data-stu-id="3fdbb-142">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="3fdbb-143">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="3fdbb-143">Run your application</span></span>

- <span data-ttu-id="3fdbb-144">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span><span class="sxs-lookup"><span data-stu-id="3fdbb-144">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

## <a name="next-step"></a><span data-ttu-id="3fdbb-145">后续步骤</span><span class="sxs-lookup"><span data-stu-id="3fdbb-145">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3fdbb-146">使用 ASP.NETCore MVC 创建自定义个人选项卡</span><span class="sxs-lookup"><span data-stu-id="3fdbb-146">Create a Custom Personal Tab with ASP.NETCore MVC</span></span>](~/tabs/quickstarts/create-personal-tab-dotnet-core-mvc.md)
