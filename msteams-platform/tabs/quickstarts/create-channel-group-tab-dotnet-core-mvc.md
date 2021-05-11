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
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core-mvc"></a><span data-ttu-id="93940-103">使用 MVC 创建自定义频道和组 ASP.NET Core选项卡</span><span class="sxs-lookup"><span data-stu-id="93940-103">Create a Custom Channel and Group Tab with ASP.NET Core MVC</span></span>

<span data-ttu-id="93940-104">在此快速入门中，我们将演练使用核心 MVC 创建自定义频道/C#ASP.Net 选项卡。</span><span class="sxs-lookup"><span data-stu-id="93940-104">In this quickstart we'll walk-through creating a custom channel/group tab with C# and ASP.Net Core MVC.</span></span> <span data-ttu-id="93940-105">我们还将使用 App [Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md)完成应用清单，并部署选项卡以Teams。</span><span class="sxs-lookup"><span data-stu-id="93940-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="93940-106">获取源代码</span><span class="sxs-lookup"><span data-stu-id="93940-106">Get the source code</span></span>

<span data-ttu-id="93940-107">打开命令提示符，为选项卡项目创建新目录。</span><span class="sxs-lookup"><span data-stu-id="93940-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="93940-108">我们提供了一个简单的 ["频道组选项卡](https://github.com/OfficeDev/microsoft-teams-sample-tabs/ChannelGroupTabMVC) "项目，让你开始操作。</span><span class="sxs-lookup"><span data-stu-id="93940-108">We have provided a simple [Channel Group Tab](https://github.com/OfficeDev/microsoft-teams-sample-tabs/ChannelGroupTabMVC) project to get you started.</span></span> <span data-ttu-id="93940-109">若要检索源代码，可以下载 zip 文件夹并提取文件或将示例存储库克隆到新目录中：</span><span class="sxs-lookup"><span data-stu-id="93940-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="93940-110">获得源代码后，打开"Visual Studio并选择"**打开项目或解决方案"。**</span><span class="sxs-lookup"><span data-stu-id="93940-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="93940-111">导航到选项卡应用程序目录，然后打开 **ChannelGroupTabMVC.sln**。</span><span class="sxs-lookup"><span data-stu-id="93940-111">Navigate to the tab application directory and open **ChannelGroupTabMVC.sln**.</span></span>

<span data-ttu-id="93940-112">若要生成并运行应用程序，请按 **F5** 或从"调试 **"** 菜单中选择"开始 **调试** "。</span><span class="sxs-lookup"><span data-stu-id="93940-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="93940-113">在浏览器中，导航到下面的 URL 并验证应用程序是否加载正确：</span><span class="sxs-lookup"><span data-stu-id="93940-113">In a browser, navigate to the URLs below and verify that the application loaded properly:</span></span>

- `http://localhost:44360`
- `http://localhost:44360/privacy`
- `http://localhost:44360/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="93940-114">查看源代码</span><span class="sxs-lookup"><span data-stu-id="93940-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="93940-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="93940-115">Startup.cs</span></span>

<span data-ttu-id="93940-116">此项目从 2.2 web 应用程序 ASP.NET Core模板创建，在设置时选中了"高级 *- 为 HTTPS* 配置"复选框。</span><span class="sxs-lookup"><span data-stu-id="93940-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="93940-117">MVC 服务由依赖关系注入框架的方法 `ConfigureServices()` 注册。</span><span class="sxs-lookup"><span data-stu-id="93940-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="93940-118">此外，默认情况下，空模板不支持为静态内容提供服务，因此静态文件中间件将添加到 `Configure()` 方法：</span><span class="sxs-lookup"><span data-stu-id="93940-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="93940-119">wwwroot 文件夹</span><span class="sxs-lookup"><span data-stu-id="93940-119">wwwroot folder</span></span>

<span data-ttu-id="93940-120">在 ASP.NET Core中，Web 根文件夹是应用程序查找静态文件的位置。</span><span class="sxs-lookup"><span data-stu-id="93940-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="93940-121">AppManifest 文件夹</span><span class="sxs-lookup"><span data-stu-id="93940-121">AppManifest folder</span></span>

<span data-ttu-id="93940-122">此文件夹包含以下所需的应用包文件：</span><span class="sxs-lookup"><span data-stu-id="93940-122">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="93940-123">全 **色图标** ，大小为 192 x 192 像素。</span><span class="sxs-lookup"><span data-stu-id="93940-123">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="93940-124">一 **个 32** x 32 像素的透明边框图标。</span><span class="sxs-lookup"><span data-stu-id="93940-124">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="93940-125">指定 **manifest.js** 属性的 on 文件。</span><span class="sxs-lookup"><span data-stu-id="93940-125">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="93940-126">这些文件需要在应用包中压缩，以用于将选项卡上载到Teams。</span><span class="sxs-lookup"><span data-stu-id="93940-126">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span>

### <a name="csproj"></a><span data-ttu-id="93940-127">.csproj</span><span class="sxs-lookup"><span data-stu-id="93940-127">.csproj</span></span>

<span data-ttu-id="93940-128">在"Visual Studio资源管理器"窗口中，右键单击项目并选择"编辑Project **文件"。**</span><span class="sxs-lookup"><span data-stu-id="93940-128">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="93940-129">在文件底部，你将看到在应用程序生成时创建和更新 zip 文件夹的代码：</span><span class="sxs-lookup"><span data-stu-id="93940-129">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="models"></a><span data-ttu-id="93940-130">模型</span><span class="sxs-lookup"><span data-stu-id="93940-130">Models</span></span>

<span data-ttu-id="93940-131">*ChannelGroup.cs* 提供 Message 对象和方法，将在配置期间从控制器调用该对象和方法。</span><span class="sxs-lookup"><span data-stu-id="93940-131">*ChannelGroup.cs* presents a Message object and methods that will be called from the Controllers during configuration.</span></span>

### <a name="views"></a><span data-ttu-id="93940-132">视图</span><span class="sxs-lookup"><span data-stu-id="93940-132">Views</span></span>

#### <a name="home"></a><span data-ttu-id="93940-133">主页</span><span class="sxs-lookup"><span data-stu-id="93940-133">Home</span></span>

<span data-ttu-id="93940-134">ASP.NET Core将名为 *Index* 的文件视为网站的默认/主页。</span><span class="sxs-lookup"><span data-stu-id="93940-134">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="93940-135">当浏览器 URL 指向网站的根目录时 **，Index.cshtml** 将显示为应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="93940-135">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="93940-136">共享的内容</span><span class="sxs-lookup"><span data-stu-id="93940-136">Shared</span></span>

<span data-ttu-id="93940-137">部分视图标记 *_Layout.cshtml* 包含应用程序的整体页面结构和共享的可视元素。</span><span class="sxs-lookup"><span data-stu-id="93940-137">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="93940-138">它还将引用Teams库。</span><span class="sxs-lookup"><span data-stu-id="93940-138">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="93940-139">控制器</span><span class="sxs-lookup"><span data-stu-id="93940-139">Controllers</span></span>

<span data-ttu-id="93940-140">控制器使用 ViewBag 属性将值动态传输给视图。</span><span class="sxs-lookup"><span data-stu-id="93940-140">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- <span data-ttu-id="93940-141">打开项目目录根目录中的命令提示符并运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="93940-141">Open a command prompt in the root of your project directory and run the following command:</span></span>

```bash
ngrok http https://localhost:443560 -host-header="localhost:44360"
```

- <span data-ttu-id="93940-142">Ngrok 将侦听来自 Internet 的请求，并且将在应用程序在端口 44355 上运行时将它们路由到您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="93940-142">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44355.</span></span>  <span data-ttu-id="93940-143">它应 `https://y8rCgT2b.ngrok.io/` 类似于 *y8rCgT2b* 替换为 ngrok 字母数字 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="93940-143">It should resemble `https://y8rCgT2b.ngrok.io/` where *y8rCgT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="93940-144">请确保使命令提示符保持运行 ngrok 并记下 URL，稍后将需要它。</span><span class="sxs-lookup"><span data-stu-id="93940-144">Be sure to keep the command prompt with ngrok running and to make note of the URL — you'll need it later.</span></span>

## <a name="update-your-application"></a><span data-ttu-id="93940-145">更新应用程序</span><span class="sxs-lookup"><span data-stu-id="93940-145">Update your application</span></span>

<span data-ttu-id="93940-146">在 **Tab.cshtml** 中，应用程序向用户显示两个选项按钮，用于显示带红色或灰色图标的选项卡。</span><span class="sxs-lookup"><span data-stu-id="93940-146">Within **Tab.cshtml** the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="93940-147">选择" **选择灰色"** 或 **"选择红色** "按钮将分别触发或 ，设置 并启用配置页上的 `saveGray()` `saveRed()` `settings.setValidityState(true)` **"** 保存"按钮。</span><span class="sxs-lookup"><span data-stu-id="93940-147">Choosing the **Select Gray** or **Select Red** button fires `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="93940-148">此代码Teams您满足配置要求，并且安装可以继续。</span><span class="sxs-lookup"><span data-stu-id="93940-148">This code lets Teams know that you have satisfied the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="93940-149">保存时，将设置 `settings.setSettings` 的参数。</span><span class="sxs-lookup"><span data-stu-id="93940-149">On save, the parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="93940-150">最后 `saveEvent.notifySuccess()` ，调用 以指示已成功解析内容 URL。</span><span class="sxs-lookup"><span data-stu-id="93940-150">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

[!INCLUDE [dotnet-upload-to-teams](~/includes/tabs/dotnet-upload-to-teams.md)]
