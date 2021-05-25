---
title: 创建包含"频道和组"选项卡 ASP.NET Core
author: laujan
description: 使用自定义频道和组选项卡创建自定义频道和组选项卡的快速 ASP.NET Core。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 1004e40e28875524ea1f38a3f6b3c2c53330fec1
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630367"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnetcore"></a><span data-ttu-id="adeac-103">使用 ASP.NETCore 创建自定义频道和组选项卡</span><span class="sxs-lookup"><span data-stu-id="adeac-103">Create a Custom Channel and Group Tab with ASP.NETCore</span></span>

<span data-ttu-id="adeac-104">在此快速入门中，我们将演练创建自定义频道/组选项卡，该选项卡包含C#和 ASP.Net Core 用户页面。</span><span class="sxs-lookup"><span data-stu-id="adeac-104">In this quickstart we'll walk-through creating a custom channel/group tab with C# and ASP.Net Core Razor page.</span></span> <span data-ttu-id="adeac-105">我们还将使用 App [Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md)完成应用清单，并部署选项卡以Teams。</span><span class="sxs-lookup"><span data-stu-id="adeac-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="adeac-106">获取源代码</span><span class="sxs-lookup"><span data-stu-id="adeac-106">Get the source code</span></span>

<span data-ttu-id="adeac-107">打开命令提示符，为选项卡项目创建新目录。</span><span class="sxs-lookup"><span data-stu-id="adeac-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="adeac-108">我们提供了一个简单的项目，让你开始操作。</span><span class="sxs-lookup"><span data-stu-id="adeac-108">We have provided a simple project to get you started.</span></span> <span data-ttu-id="adeac-109">若要检索源代码，可以下载 zip 文件夹并提取文件或将示例存储库克隆到新目录中：</span><span class="sxs-lookup"><span data-stu-id="adeac-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="adeac-110">获得源代码后，打开"Visual Studio并选择"**打开项目或解决方案"。**</span><span class="sxs-lookup"><span data-stu-id="adeac-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="adeac-111">导航到选项卡应用程序目录，然后打开 **ChannelGroupTab.sln**。</span><span class="sxs-lookup"><span data-stu-id="adeac-111">Navigate to the tab application directory and open **ChannelGroupTab.sln**.</span></span>

<span data-ttu-id="adeac-112">若要生成并运行应用程序，请按 **F5** 或从"调试 **"** 菜单中选择"开始 **调试** "。</span><span class="sxs-lookup"><span data-stu-id="adeac-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="adeac-113">在浏览器中，导航到下面的 URL 并验证应用程序是否加载正确：</span><span class="sxs-lookup"><span data-stu-id="adeac-113">In a browser navigate to the URLs below and verify the application loaded properly:</span></span>

- `http://localhost:44355`
- `http://localhost:44355/privacy`
- `http://localhost:44355/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="adeac-114">查看源代码</span><span class="sxs-lookup"><span data-stu-id="adeac-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="adeac-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="adeac-115">Startup.cs</span></span>

<span data-ttu-id="adeac-116">此项目从 2.2 web 应用程序 ASP.NET Core模板创建，在设置时选中了"高级 *- 为 HTTPS* 配置"复选框。</span><span class="sxs-lookup"><span data-stu-id="adeac-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="adeac-117">MVC 服务由依赖关系注入框架的方法 `ConfigureServices()` 注册。</span><span class="sxs-lookup"><span data-stu-id="adeac-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="adeac-118">此外，默认情况下，空模板不支持为静态内容提供服务，因此静态文件中间件将添加到 `Configure()` 方法：</span><span class="sxs-lookup"><span data-stu-id="adeac-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="adeac-119">wwwroot 文件夹</span><span class="sxs-lookup"><span data-stu-id="adeac-119">wwwroot folder</span></span>

<span data-ttu-id="adeac-120">在 ASP.NET Core中，Web 根文件夹是应用程序查找静态文件的位置。</span><span class="sxs-lookup"><span data-stu-id="adeac-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="indexcshtml"></a><span data-ttu-id="adeac-121">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="adeac-121">Index.cshtml</span></span>

<span data-ttu-id="adeac-122">ASP.NET Core将名为 *Index* 的文件视为网站的默认/主页。</span><span class="sxs-lookup"><span data-stu-id="adeac-122">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="adeac-123">当浏览器 URL 指向网站的根目录时 **，Index.cshtml** 将显示为应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="adeac-123">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

### <a name="tabcs"></a><span data-ttu-id="adeac-124">Tab.cs</span><span class="sxs-lookup"><span data-stu-id="adeac-124">Tab.cs</span></span>

<span data-ttu-id="adeac-125">此C#文件包含将在配置期间从 **Tab.cshtml** 调用的方法。</span><span class="sxs-lookup"><span data-stu-id="adeac-125">This C# file contains a method that will be called from **Tab.cshtml** during configuration.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="adeac-126">AppManifest 文件夹</span><span class="sxs-lookup"><span data-stu-id="adeac-126">AppManifest folder</span></span>

<span data-ttu-id="adeac-127">此文件夹包含以下所需的应用包文件：</span><span class="sxs-lookup"><span data-stu-id="adeac-127">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="adeac-128">全 **色图标** ，大小为 192 x 192 像素。</span><span class="sxs-lookup"><span data-stu-id="adeac-128">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="adeac-129">一 **个 32** x 32 像素的透明边框图标。</span><span class="sxs-lookup"><span data-stu-id="adeac-129">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="adeac-130">指定 **manifest.js** 属性的 on 文件。</span><span class="sxs-lookup"><span data-stu-id="adeac-130">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="adeac-131">这些文件需要在应用包中压缩，以用于将选项卡上载到Teams。</span><span class="sxs-lookup"><span data-stu-id="adeac-131">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="adeac-132">当用户选择添加或更新选项卡时，Microsoft Teams将加载清单中指定的，将其嵌入 IFrame 中，并将其 `configurationUrl` 呈现在选项卡中。</span><span class="sxs-lookup"><span data-stu-id="adeac-132">When a user chooses to add or update your tab, Microsoft Teams will load the `configurationUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="adeac-133">.csproj</span><span class="sxs-lookup"><span data-stu-id="adeac-133">.csproj</span></span>

<span data-ttu-id="adeac-134">在"Visual Studio资源管理器"窗口中，右键单击项目并选择"编辑Project **文件"。**</span><span class="sxs-lookup"><span data-stu-id="adeac-134">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="adeac-135">在文件底部，你将看到在应用程序生成时创建和更新 zip 文件夹的代码：</span><span class="sxs-lookup"><span data-stu-id="adeac-135">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

- <span data-ttu-id="adeac-136">打开项目目录根目录中的命令提示符并运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="adeac-136">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ```bash
    ngrok http https://localhost:44355 -host-header="localhost:44355"
    ```

- <span data-ttu-id="adeac-137">Ngrok 将侦听来自 Internet 的请求，并且将在应用程序在端口 44355 上运行时将它们路由到您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="adeac-137">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44355.</span></span> <span data-ttu-id="adeac-138">它应 `https://y8rCgT2b.ngrok.io/` 类似于 *y8rCgT2b* 替换为 ngrok 字母数字 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="adeac-138">It should resemble `https://y8rCgT2b.ngrok.io/` where *y8rCgT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="adeac-139">请确保使命令提示符保持运行 ngrok 并记下 URL，稍后将需要它。</span><span class="sxs-lookup"><span data-stu-id="adeac-139">Be sure to keep the command prompt with ngrok running and to make note of the URL — you'll need it later.</span></span>

## <a name="update-your-application"></a><span data-ttu-id="adeac-140">更新应用程序</span><span class="sxs-lookup"><span data-stu-id="adeac-140">Update your application</span></span>

<span data-ttu-id="adeac-141">在 *Tab.cshtml* 中，应用程序向用户显示两个选项按钮，用于显示带红色或灰色图标的选项卡。</span><span class="sxs-lookup"><span data-stu-id="adeac-141">Within *Tab.cshtml* the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="adeac-142">选择" **选择灰色"** 或 **"选择红色** "按钮将分别触发或 ，设置 并启用配置页上的 `saveGray()` `saveRed()` `settings.setValidityState(true)` **"** 保存"按钮。</span><span class="sxs-lookup"><span data-stu-id="adeac-142">Choosing the **Select Gray** or **Select Red** button fires `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="adeac-143">此代码Teams您满足配置要求，并且安装可以继续。</span><span class="sxs-lookup"><span data-stu-id="adeac-143">This code lets Teams know that you have satisfied the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="adeac-144">保存时，将设置 `settings.setSettings` 的参数。</span><span class="sxs-lookup"><span data-stu-id="adeac-144">On save, the parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="adeac-145">最后 `saveEvent.notifySuccess()` ，调用 以指示已成功解析内容 URL。</span><span class="sxs-lookup"><span data-stu-id="adeac-145">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

## <a name="next-step"></a><span data-ttu-id="adeac-146">后续步骤</span><span class="sxs-lookup"><span data-stu-id="adeac-146">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="adeac-147">使用 ASP.NETCore MVC 创建自定义频道和组选项卡</span><span class="sxs-lookup"><span data-stu-id="adeac-147">Create a Custom Channel and Group Tab with ASP.NETCore MVC</span></span>](~/tabs/quickstarts/create-channel-group-tab-dotnet-core-mvc.md)
