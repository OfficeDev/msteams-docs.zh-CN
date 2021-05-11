---
title: 使用 ASP 创建个人选项卡。 NET Core MVC
author: laujan
description: 使用 ASP 创建自定义个人选项卡的快速入门指南。 NET Core MVC。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 3ec6b5c054384653e30e46cbffed4a2af6662c33
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019564"
---
# <a name="create-a-custom-personal-tab-with-asp-net-core-mvc"></a><span data-ttu-id="ff097-105">使用 ASP 创建自定义个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="ff097-105">Create a Custom Personal Tab with ASP.</span></span> <span data-ttu-id="ff097-106">NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="ff097-106">NET Core MVC</span></span>

<span data-ttu-id="ff097-107">在此快速入门中，我们将演练使用 C# 和 ASP 创建自定义个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="ff097-107">In this quickstart we'll walk-through creating a custom personal tab with C# and ASP.</span></span> <span data-ttu-id="ff097-108">Net Core MVC。</span><span class="sxs-lookup"><span data-stu-id="ff097-108">Net Core MVC.</span></span> <span data-ttu-id="ff097-109">我们还将使用 App [Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md)完成应用清单，并部署选项卡以Teams。</span><span class="sxs-lookup"><span data-stu-id="ff097-109">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="ff097-110">获取源代码</span><span class="sxs-lookup"><span data-stu-id="ff097-110">Get the source code</span></span>

<span data-ttu-id="ff097-111">打开命令提示符，为选项卡项目创建新目录。</span><span class="sxs-lookup"><span data-stu-id="ff097-111">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="ff097-112">我们提供了一个简单的项目，让你开始操作。</span><span class="sxs-lookup"><span data-stu-id="ff097-112">We have provided a simple project to get you started.</span></span> <span data-ttu-id="ff097-113">若要检索源代码，可以下载 zip 文件夹并提取文件或将示例存储库克隆到新目录中：</span><span class="sxs-lookup"><span data-stu-id="ff097-113">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="ff097-114">获得源代码后，打开"Visual Studio并选择"**打开项目或解决方案"。**</span><span class="sxs-lookup"><span data-stu-id="ff097-114">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="ff097-115">导航到选项卡应用程序目录，然后打开 **PersonalTabMVC.sln**。</span><span class="sxs-lookup"><span data-stu-id="ff097-115">Navigate to the tab application directory and open **PersonalTabMVC.sln**.</span></span>

<span data-ttu-id="ff097-116">若要生成并运行应用程序，请按 **F5** 或从"调试 **"** 菜单中选择"开始 **调试** "。</span><span class="sxs-lookup"><span data-stu-id="ff097-116">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="ff097-117">在浏览器中，导航到下面的 URL 以验证应用程序是否加载正确：</span><span class="sxs-lookup"><span data-stu-id="ff097-117">In a browser navigate to the URLs below to verify that the application loaded properly:</span></span>

* `http://localhost:44335`
* `http://localhost:44335/privacy`
* `http://localhost:44335/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="ff097-118">查看源代码</span><span class="sxs-lookup"><span data-stu-id="ff097-118">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="ff097-119">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="ff097-119">Startup.cs</span></span>

<span data-ttu-id="ff097-120">此项目是使用 ASP 创建的。</span><span class="sxs-lookup"><span data-stu-id="ff097-120">This project was created from an ASP.</span></span> <span data-ttu-id="ff097-121">NET Core 2.2 Web 应用程序空模板，在设置时选中了"高级 *- 配置 HTTPS"* 复选框。</span><span class="sxs-lookup"><span data-stu-id="ff097-121">NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="ff097-122">MVC 服务由依赖关系注入框架的方法 `ConfigureServices()` 注册。</span><span class="sxs-lookup"><span data-stu-id="ff097-122">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="ff097-123">此外，默认情况下，空模板不支持为静态内容提供服务，因此静态文件中间件将添加到 `Configure()` 方法：</span><span class="sxs-lookup"><span data-stu-id="ff097-123">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="ff097-124">wwwroot 文件夹</span><span class="sxs-lookup"><span data-stu-id="ff097-124">wwwroot folder</span></span>

<span data-ttu-id="ff097-125">在 ASP 中。</span><span class="sxs-lookup"><span data-stu-id="ff097-125">In ASP.</span></span> <span data-ttu-id="ff097-126">NET Core，Web 根文件夹是应用程序查找静态文件的位置。</span><span class="sxs-lookup"><span data-stu-id="ff097-126">NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="ff097-127">AppManifest 文件夹</span><span class="sxs-lookup"><span data-stu-id="ff097-127">AppManifest folder</span></span>

<span data-ttu-id="ff097-128">此文件夹包含以下所需的应用包文件：</span><span class="sxs-lookup"><span data-stu-id="ff097-128">This folder contains the following required app package files:</span></span>

* <span data-ttu-id="ff097-129">全 **色图标** ，大小为 192 x 192 像素。</span><span class="sxs-lookup"><span data-stu-id="ff097-129">A **full color icon** measuring 192 x 192 pixels.</span></span>
* <span data-ttu-id="ff097-130">一 **个 32** x 32 像素的透明边框图标。</span><span class="sxs-lookup"><span data-stu-id="ff097-130">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
* <span data-ttu-id="ff097-131">指定 **manifest.js** 属性的 on 文件。</span><span class="sxs-lookup"><span data-stu-id="ff097-131">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="ff097-132">这些文件需要在应用包中压缩，以用于将选项卡上载到Teams。</span><span class="sxs-lookup"><span data-stu-id="ff097-132">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="ff097-133">Microsoft Teams将加载清单中指定的 ，将其嵌入 `contentUrl` IFrame，并将其呈现在选项卡中。</span><span class="sxs-lookup"><span data-stu-id="ff097-133">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="ff097-134">.csproj</span><span class="sxs-lookup"><span data-stu-id="ff097-134">.csproj</span></span>

<span data-ttu-id="ff097-135">在"Visual Studio资源管理器"窗口中，右键单击项目并选择"编辑Project **文件"。**</span><span class="sxs-lookup"><span data-stu-id="ff097-135">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="ff097-136">在文件底部，你将看到在应用程序生成时创建和更新 zip 文件夹的代码：</span><span class="sxs-lookup"><span data-stu-id="ff097-136">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="models"></a><span data-ttu-id="ff097-137">模型</span><span class="sxs-lookup"><span data-stu-id="ff097-137">Models</span></span>

<span data-ttu-id="ff097-138">*PersonalTab.cs* 提供 Message 对象和方法，当用户在 PersonalTab 视图中选择按钮时，该对象和方法将从 *PersonalTabController* 调用。 </span><span class="sxs-lookup"><span data-stu-id="ff097-138">*PersonalTab.cs* presents a Message object and methods that will be called from *PersonalTabController* when a user selects a button in the *PersonalTab* View.</span></span>

### <a name="views"></a><span data-ttu-id="ff097-139">视图</span><span class="sxs-lookup"><span data-stu-id="ff097-139">Views</span></span>

#### <a name="home"></a><span data-ttu-id="ff097-140">主页</span><span class="sxs-lookup"><span data-stu-id="ff097-140">Home</span></span>

<span data-ttu-id="ff097-141">ASP。</span><span class="sxs-lookup"><span data-stu-id="ff097-141">ASP.</span></span> <span data-ttu-id="ff097-142">NET Core 将名为 *Index* 的文件视为网站的默认/主页。</span><span class="sxs-lookup"><span data-stu-id="ff097-142">NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="ff097-143">当浏览器 URL 指向网站的根目录时 *，Index.cshtml* 将显示为应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="ff097-143">When your browser URL points to the root of the site, *Index.cshtml* will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="ff097-144">共享的内容</span><span class="sxs-lookup"><span data-stu-id="ff097-144">Shared</span></span>

<span data-ttu-id="ff097-145">部分视图标记 *_Layout.cshtml* 包含应用程序的整体页面结构和共享的可视元素。</span><span class="sxs-lookup"><span data-stu-id="ff097-145">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="ff097-146">它还将引用Teams库。</span><span class="sxs-lookup"><span data-stu-id="ff097-146">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="ff097-147">控制器</span><span class="sxs-lookup"><span data-stu-id="ff097-147">Controllers</span></span>

<span data-ttu-id="ff097-148">控制器使用 ViewBag 属性将值动态传输给视图。</span><span class="sxs-lookup"><span data-stu-id="ff097-148">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* <span data-ttu-id="ff097-149">打开项目目录根目录中的命令提示符并运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="ff097-149">Open a command prompt in the root of your project directory and run the following command:</span></span>

``` bash
ngrok http https://localhost:44345 -host-header="localhost:44345"
```

* <span data-ttu-id="ff097-150">Ngrok 将侦听来自 Internet 的请求，并且将在应用程序在端口 44325 上运行时将它们路由到您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="ff097-150">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="ff097-151">它应 `https://y8rPrT2b.ngrok.io/` 类似于 *y8rPrT2b* 替换为 ngrok 字母数字 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="ff097-151">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

* <span data-ttu-id="ff097-152">请确保使命令提示符保持运行 ngrok，并记下 URL，稍后将需要它。</span><span class="sxs-lookup"><span data-stu-id="ff097-152">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

* <span data-ttu-id="ff097-153">通过打开浏览器，然后通过命令提示符窗口中提供的 ngrok HTTPS URL 进入内容页面，验证 *ngrok* 是否正常运行。</span><span class="sxs-lookup"><span data-stu-id="ff097-153">Verify that *ngrok* is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> <span data-ttu-id="ff097-154">[!</span><span class="sxs-lookup"><span data-stu-id="ff097-154">[!</span></span> <span data-ttu-id="ff097-155">提示] 你需要让应用程序在 Visual Studio 和 ngrok 中运行才能完成此快速入门。</span><span class="sxs-lookup"><span data-stu-id="ff097-155">TIP] You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="ff097-156">如果需要停止运行应用程序，Visual Studio运行应用程序，请 **保持 ngrok 运行**。</span><span class="sxs-lookup"><span data-stu-id="ff097-156">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="ff097-157">当应用程序在服务器中重新启动时，它将继续侦听并Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="ff097-157">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="ff097-158">如果必须重新启动 ngrok 服务，它将返回一个新 URL，并且必须更新使用该 URL 的每一处。</span><span class="sxs-lookup"><span data-stu-id="ff097-158">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="ff097-159">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="ff097-159">Run your application</span></span>

* <span data-ttu-id="ff097-160">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span><span class="sxs-lookup"><span data-stu-id="ff097-160">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]
