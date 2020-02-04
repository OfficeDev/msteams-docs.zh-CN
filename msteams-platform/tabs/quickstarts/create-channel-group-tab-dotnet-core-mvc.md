---
title: 使用 ASP.NET Core MVC 创建通道和组选项卡
author: laujan
description: 用于创建带有 ASP.NET Core MVC 的自定义频道和分组选项卡的快速入门指南。
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: 57c22d10414eb8ec93249584219488397f0b6b33
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673211"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core-mvc"></a><span data-ttu-id="fc04f-103">使用 ASP.NET Core MVC 创建自定义通道和组选项卡</span><span class="sxs-lookup"><span data-stu-id="fc04f-103">Create a Custom Channel and Group Tab with ASP.NET Core MVC</span></span>

<span data-ttu-id="fc04f-104">在此快速入门中，我们将介绍如何使用 c # 和 ASP.Net Core MVC 创建自定义频道/组选项卡。</span><span class="sxs-lookup"><span data-stu-id="fc04f-104">In this quickstart we'll walk-through creating a custom channel/group tab with C# and ASP.Net Core MVC.</span></span> <span data-ttu-id="fc04f-105">我们还将使用[Microsoft 团队的应用 Studio](~/concepts/build-and-test/app-studio-overview.md)来完成你的应用程序清单，并将你的选项卡部署到团队。</span><span class="sxs-lookup"><span data-stu-id="fc04f-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="fc04f-106">获取源代码</span><span class="sxs-lookup"><span data-stu-id="fc04f-106">Get the source code</span></span>

<span data-ttu-id="fc04f-107">打开命令提示符并为您的选项卡项目创建一个新目录。</span><span class="sxs-lookup"><span data-stu-id="fc04f-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="fc04f-108">我们提供了一个简单的[通道组选项卡](https://github.com/OfficeDev/microsoft-teams-sample-tabs/ChannelGroupTabMVC)项目，可帮助你入门。</span><span class="sxs-lookup"><span data-stu-id="fc04f-108">We have provided a simple [Channel Group Tab](https://github.com/OfficeDev/microsoft-teams-sample-tabs/ChannelGroupTabMVC) project to get you started.</span></span> <span data-ttu-id="fc04f-109">若要检索源代码，可以下载 zip 文件夹并解压缩文件，或将示例存储库克隆到新目录：</span><span class="sxs-lookup"><span data-stu-id="fc04f-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="fc04f-110">拥有源代码后，打开 Visual Studio 并选择 "**打开项目或解决方案**"。</span><span class="sxs-lookup"><span data-stu-id="fc04f-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="fc04f-111">导航到 "选项卡应用程序目录"，然后打开 " **ChannelGroupTabMVC**"。</span><span class="sxs-lookup"><span data-stu-id="fc04f-111">Navigate to the tab application directory and open **ChannelGroupTabMVC.sln**.</span></span>

<span data-ttu-id="fc04f-112">若要生成并运行应用程序，请按**F5**或从 "**调试**" 菜单中选择 "**启动调试**"。</span><span class="sxs-lookup"><span data-stu-id="fc04f-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="fc04f-113">在浏览器中，导航到以下 Url 并验证应用程序是否已正确加载：</span><span class="sxs-lookup"><span data-stu-id="fc04f-113">In a browser, navigate to the URLs below and verify that the application loaded properly:</span></span>

- `http://localhost:44360`
- `http://localhost:44360/privacy`
- `http://localhost:44360/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="fc04f-114">查看源代码</span><span class="sxs-lookup"><span data-stu-id="fc04f-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="fc04f-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="fc04f-115">Startup.cs</span></span>

<span data-ttu-id="fc04f-116">此项目是从 ASP.NET Core 2.2 Web 应用程序空模板创建的，并且在安装程序中选中了 "*高级-配置为 HTTPS* " 复选框。</span><span class="sxs-lookup"><span data-stu-id="fc04f-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="fc04f-117">MVC 服务由依赖关系注入框架的`ConfigureServices()`方法注册。</span><span class="sxs-lookup"><span data-stu-id="fc04f-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="fc04f-118">此外，默认情况下，空模板不启用静态内容的服务，因此将静态文件中间件添加`Configure()`到方法中：</span><span class="sxs-lookup"><span data-stu-id="fc04f-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="fc04f-119">wwwroot 文件夹</span><span class="sxs-lookup"><span data-stu-id="fc04f-119">wwwroot folder</span></span>

<span data-ttu-id="fc04f-120">在 ASP.NET Core 中，web 根文件夹是应用程序查找静态文件的位置。</span><span class="sxs-lookup"><span data-stu-id="fc04f-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="fc04f-121">Appmanifest.xml 文件夹</span><span class="sxs-lookup"><span data-stu-id="fc04f-121">AppManifest folder</span></span>

<span data-ttu-id="fc04f-122">此文件夹包含以下所需的应用程序包文件：</span><span class="sxs-lookup"><span data-stu-id="fc04f-122">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="fc04f-123">以 192 x 192 像素为单位的**完整彩色图标**。</span><span class="sxs-lookup"><span data-stu-id="fc04f-123">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="fc04f-124">一个**透明的大纲图标**，用于度量 32 x 32 像素。</span><span class="sxs-lookup"><span data-stu-id="fc04f-124">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="fc04f-125">一个指定应用程序的属性的**清单 json**文件。</span><span class="sxs-lookup"><span data-stu-id="fc04f-125">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="fc04f-126">需要将这些文件压缩到应用程序包中，以便在将选项卡上载到团队时使用。</span><span class="sxs-lookup"><span data-stu-id="fc04f-126">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span>

### <a name="csproj"></a><span data-ttu-id="fc04f-127">.csproj</span><span class="sxs-lookup"><span data-stu-id="fc04f-127">.csproj</span></span>

<span data-ttu-id="fc04f-128">在 Visual Studio "解决方案资源管理器" 窗口中，右键单击该项目，然后选择 "**编辑项目文件**"。</span><span class="sxs-lookup"><span data-stu-id="fc04f-128">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="fc04f-129">在该文件的底部，您将看到在应用程序生成时创建和更新您的 zip 文件夹的代码：</span><span class="sxs-lookup"><span data-stu-id="fc04f-129">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="models"></a><span data-ttu-id="fc04f-130">模型</span><span class="sxs-lookup"><span data-stu-id="fc04f-130">Models</span></span>

<span data-ttu-id="fc04f-131">*ChannelGroup.cs*显示在配置过程中将从控制器调用的 Message 对象和方法。</span><span class="sxs-lookup"><span data-stu-id="fc04f-131">*ChannelGroup.cs* presents a Message object and methods that will be called from the Controllers during configuration.</span></span>

### <a name="views"></a><span data-ttu-id="fc04f-132">视图</span><span class="sxs-lookup"><span data-stu-id="fc04f-132">Views</span></span>

#### <a name="home"></a><span data-ttu-id="fc04f-133">开始</span><span class="sxs-lookup"><span data-stu-id="fc04f-133">Home</span></span>

<span data-ttu-id="fc04f-134">ASP.NET Core 将称为*Index*的文件视为网站的默认/主页。</span><span class="sxs-lookup"><span data-stu-id="fc04f-134">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="fc04f-135">当浏览器 URL 指向网站的根目录时，将显示**索引. cshtml**将显示为应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="fc04f-135">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="fc04f-136">共享的内容</span><span class="sxs-lookup"><span data-stu-id="fc04f-136">Shared</span></span>

<span data-ttu-id="fc04f-137">分部视图标记 *_Layout. cshtml*包含应用程序的整体页面结构和共享的可视化元素。</span><span class="sxs-lookup"><span data-stu-id="fc04f-137">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="fc04f-138">它还将引用团队库。</span><span class="sxs-lookup"><span data-stu-id="fc04f-138">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="fc04f-139">控制器</span><span class="sxs-lookup"><span data-stu-id="fc04f-139">Controllers</span></span>

<span data-ttu-id="fc04f-140">这些控制器使用 ViewBag 属性将值动态转移到视图。</span><span class="sxs-lookup"><span data-stu-id="fc04f-140">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- <span data-ttu-id="fc04f-141">在项目目录的根目录中打开命令提示符，并运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="fc04f-141">Open a command prompt in the root of your project directory and run the following command:</span></span>

```bash
ngrok http https://localhost:443560 -host-header="localhost:44360"
```

- <span data-ttu-id="fc04f-142">Ngrok 将侦听来自 internet 的请求，并在其运行在端口44355上时将它们路由到您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="fc04f-142">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44355.</span></span>  <span data-ttu-id="fc04f-143">它应类似`https://y8rCgT2b.ngrok.io/`于在*y8rCgT2b*替换为 NGROK 字母数字 HTTPS URL 的位置。</span><span class="sxs-lookup"><span data-stu-id="fc04f-143">It should resemble `https://y8rCgT2b.ngrok.io/` where *y8rCgT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="fc04f-144">请务必在 ngrok 运行的同时保留命令提示符，并记下该 URL，稍后将需要它。</span><span class="sxs-lookup"><span data-stu-id="fc04f-144">Be sure to keep the command prompt with ngrok running and to make note of the URL — you'll need it later.</span></span>

## <a name="update-your-application"></a><span data-ttu-id="fc04f-145">更新应用程序</span><span class="sxs-lookup"><span data-stu-id="fc04f-145">Update your application</span></span>

<span data-ttu-id="fc04f-146">在**选项卡中。 cshtml**应用程序为用户提供了两个选项按钮，用于显示带有红色或灰色图标的选项卡。</span><span class="sxs-lookup"><span data-stu-id="fc04f-146">Within **Tab.cshtml** the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="fc04f-147">选择 "**选择灰色**" 或 "**选择红色**" `saveGray()`按钮将触发或`settings.setValidityState(true)` `saveRed()`分别设置和启用 "配置" 页上的 "**保存**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="fc04f-147">Choosing the **Select Gray** or **Select Red** button fires `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="fc04f-148">此代码使团队知道您已经满足配置要求，可以继续安装。</span><span class="sxs-lookup"><span data-stu-id="fc04f-148">This code lets Teams know that you have satisfied the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="fc04f-149">在保存`settings.setSettings`时设置的参数。</span><span class="sxs-lookup"><span data-stu-id="fc04f-149">On save, the parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="fc04f-150">最后， `saveEvent.notifySuccess()`将调用，以指示内容 URL 已成功解析。</span><span class="sxs-lookup"><span data-stu-id="fc04f-150">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

[!INCLUDE [dotnet-upload-to-teams](~/includes/tabs/dotnet-upload-to-teams.md)]
