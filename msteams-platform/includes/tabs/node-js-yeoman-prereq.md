## <a name="prerequisites"></a><span data-ttu-id="e6b95-101">先决条件</span><span class="sxs-lookup"><span data-stu-id="e6b95-101">Prerequisites</span></span>

- <span data-ttu-id="e6b95-102">若要完成此快速入门，你需要一个 Office 365 租户和一个配置了启用"允许上载自定义应用 *"的团队* 。</span><span class="sxs-lookup"><span data-stu-id="e6b95-102">To complete this quickstart you will need an Office 365 tenant and a team configured with *Allow uploading custom apps* enabled.</span></span> <span data-ttu-id="e6b95-103">若要了解更多信息，请参阅 [准备 Office 365 租户](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="e6b95-103">To learn more, see [Prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

  - <span data-ttu-id="e6b95-104">如果当前没有 Office 365 帐户，可以通过 Office 365 开发人员计划注册免费订阅。</span><span class="sxs-lookup"><span data-stu-id="e6b95-104">If you don't currently have an Office 365 account, you can sign up for a free subscription through the Office 365 Developer Program.</span></span> <span data-ttu-id="e6b95-105">只要将订阅用于正在进行的开发，订阅就会保持活动状态。</span><span class="sxs-lookup"><span data-stu-id="e6b95-105">The subscription will remain active as long as you're using it for ongoing development.</span></span> <span data-ttu-id="e6b95-106">请参阅 [欢迎使用 Office 365 开发人员计划](https://docs.microsoft.com/office/developer-program/microsoft-365-developer-program)。</span><span class="sxs-lookup"><span data-stu-id="e6b95-106">See [Welcome to the Office 365 Developer Program](https://docs.microsoft.com/office/developer-program/microsoft-365-developer-program).</span></span>

<span data-ttu-id="e6b95-107">此外，此项目要求在开发环境中安装以下内容：</span><span class="sxs-lookup"><span data-stu-id="e6b95-107">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="e6b95-108">任何文本编辑器或 IDE。</span><span class="sxs-lookup"><span data-stu-id="e6b95-108">Any text editor or IDE.</span></span> <span data-ttu-id="e6b95-109">你可以免费安装和 [Visual Studio代码](https://code.visualstudio.com/download) 。</span><span class="sxs-lookup"><span data-stu-id="e6b95-109">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

- <span data-ttu-id="e6b95-110">[Node.js/npm](https://nodejs.org/en/)。</span><span class="sxs-lookup"><span data-stu-id="e6b95-110">[Node.js/npm](https://nodejs.org/en/).</span></span> <span data-ttu-id="e6b95-111">你应该使用最新的 LTS 版本。</span><span class="sxs-lookup"><span data-stu-id="e6b95-111">You should use the latest LTS version.</span></span> <span data-ttu-id="e6b95-112">Node 程序包管理器 (npm) 将在安装 Node.js 时安装到系统中。</span><span class="sxs-lookup"><span data-stu-id="e6b95-112">The Node Package Manager (npm) will install into your system with the installation of Node.js.</span></span>

- <span data-ttu-id="e6b95-113">在成功安装 Node.js，在命令提示符中键入以下内容来安装 [Yeoman](https://yeoman.io/) 和 [gulp-cli](https://www.npmjs.com/package/gulp-cli) 程序包：</span><span class="sxs-lookup"><span data-stu-id="e6b95-113">After you've successfully installed Node.js, install the [Yeoman](https://yeoman.io/) and [gulp-cli](https://www.npmjs.com/package/gulp-cli) packages by typing the following in your command prompt:</span></span>

```bash
npm install yo gulp-cli --global
```

- <span data-ttu-id="e6b95-114">在命令提示符中键入以下内容，安装 Microsoft Teams 应用生成器：</span><span class="sxs-lookup"><span data-stu-id="e6b95-114">Install the Microsoft Teams Apps generator by typing the following in your command prompt:</span></span>

```bash
npm install generator-teams --global
```

## <a name="generate-your-project"></a><span data-ttu-id="e6b95-115">生成项目</span><span class="sxs-lookup"><span data-stu-id="e6b95-115">Generate your project</span></span>

- <span data-ttu-id="e6b95-116">打开命令提示符，为选项卡项目创建新目录。</span><span class="sxs-lookup"><span data-stu-id="e6b95-116">Open a command prompt and create a new directory for your tab project.</span></span>

- <span data-ttu-id="e6b95-117">若要启动生成器，请导航到新目录并键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="e6b95-117">To start the generator, navigate to your new directory and type the following command:</span></span>

```bash
yo teams
```

- <span data-ttu-id="e6b95-118">接下来，您将提供一系列值，这些值将用于应用程序的 on **manifest.js文件中** ：</span><span class="sxs-lookup"><span data-stu-id="e6b95-118">Next, you'll provide a series of values that will be used in your application's **manifest.json** file:</span></span>

![生成器打开屏幕截图](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

<span data-ttu-id="e6b95-120">**你的解决方案名称是什么？**</span><span class="sxs-lookup"><span data-stu-id="e6b95-120">**What is your solution name?**</span></span>

<span data-ttu-id="e6b95-121">这是项目名称。</span><span class="sxs-lookup"><span data-stu-id="e6b95-121">This is your project name.</span></span> <span data-ttu-id="e6b95-122">可以通过按 Enter 接受建议的名称。</span><span class="sxs-lookup"><span data-stu-id="e6b95-122">You can accept the suggested name by pressing enter.</span></span>

<span data-ttu-id="e6b95-123">**要将文件存放在哪里?**</span><span class="sxs-lookup"><span data-stu-id="e6b95-123">**Where do you want to place the files?**</span></span>

<span data-ttu-id="e6b95-124">您当前在项目目录中。</span><span class="sxs-lookup"><span data-stu-id="e6b95-124">You're currently in your project directory.</span></span> <span data-ttu-id="e6b95-125">按 Enter。</span><span class="sxs-lookup"><span data-stu-id="e6b95-125">Press enter.</span></span>

<span data-ttu-id="e6b95-126">**Microsoft Teams 应用项目的标题**</span><span class="sxs-lookup"><span data-stu-id="e6b95-126">**Title of your Microsoft Teams app project?**</span></span>

<span data-ttu-id="e6b95-127">这是你的应用包名称，将在应用清单和说明中使用。</span><span class="sxs-lookup"><span data-stu-id="e6b95-127">This is your app package name and will be used in the app manifest and description.</span></span>

<span data-ttu-id="e6b95-128">**你的 (公司) 名称？ (最多 32 个字符)**</span><span class="sxs-lookup"><span data-stu-id="e6b95-128">**Your (company) name? (max 32 characters)**</span></span>

<span data-ttu-id="e6b95-129">你的公司名称将在应用清单中使用。</span><span class="sxs-lookup"><span data-stu-id="e6b95-129">Your company name will be used in the app manifest.</span></span>

<br><span data-ttu-id="e6b95-130">**要使用哪个清单版本？**</span><span class="sxs-lookup"><span data-stu-id="e6b95-130">**Which manifest version would you like to use?**</span></span>

<span data-ttu-id="e6b95-131">选择默认架构。</span><span class="sxs-lookup"><span data-stu-id="e6b95-131">Select the default schema.</span></span>

<span data-ttu-id="e6b95-132">**快速基架？ (Y/n)**</span><span class="sxs-lookup"><span data-stu-id="e6b95-132">**Quick scaffolding? (Y/n)**</span></span>

<span data-ttu-id="e6b95-133">默认值为 yes;输入 **n** 以输入你的 Microsoft 合作伙伴 ID。</span><span class="sxs-lookup"><span data-stu-id="e6b95-133">The default is yes; enter **n** to enter your Microsoft Partner Id.</span></span>

<span data-ttu-id="e6b95-134">**输入你的 Microsoft 合作伙伴 ID（如果有） (留空可跳过)**</span><span class="sxs-lookup"><span data-stu-id="e6b95-134">**Enter your Microsoft Partner Id, if you have one? (Leave blank to skip)**</span></span>

<span data-ttu-id="e6b95-135">此字段不是必需的，并且只应在你已是 Microsoft 合作伙伴网络的一 [部分时使用](https://partner.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="e6b95-135">This field isn't required and should only be used if you're already part of the [Microsoft Partner Network](https://partner.microsoft.com).</span></span>

<span data-ttu-id="e6b95-136">**要向项目添加哪些内容？**</span><span class="sxs-lookup"><span data-stu-id="e6b95-136">**What do you want to add to your project?**</span></span>

<span data-ttu-id="e6b95-137">选择 &ast; () 选项卡"。</span><span class="sxs-lookup"><span data-stu-id="e6b95-137">Select ( &ast; ) A Tab.</span></span>

<span data-ttu-id="e6b95-138">**将在其中托管此解决方案的 URL？**</span><span class="sxs-lookup"><span data-stu-id="e6b95-138">**The URL where you will host this solution?**</span></span>

<span data-ttu-id="e6b95-139">默认情况下，生成器建议 Azure 网站 URL。</span><span class="sxs-lookup"><span data-stu-id="e6b95-139">By default the generator suggests an Azure Web Sites URL.</span></span> <span data-ttu-id="e6b95-140">你将仅在本地测试你的应用，因此，完成此快速入门不需要有效的 URL。</span><span class="sxs-lookup"><span data-stu-id="e6b95-140">You'll only be testing your app locally, therefore, a valid URL is not necessary to complete this quickstart.</span></span>

<span data-ttu-id="e6b95-141">**是否包含测试框架和初始测试？ (y/N)**</span><span class="sxs-lookup"><span data-stu-id="e6b95-141">**Would you like to include Test framework and initial tests? (y/N)**</span></span>

<span data-ttu-id="e6b95-142">选择 **不包括** 此项目的测试框架。</span><span class="sxs-lookup"><span data-stu-id="e6b95-142">Choose **not** to include a test framework for this project.</span></span> <span data-ttu-id="e6b95-143">默认值为 yes;输入 **n**。</span><span class="sxs-lookup"><span data-stu-id="e6b95-143">The default is yes; enter **n**.</span></span>

<span data-ttu-id="e6b95-144">**是否对遥测使用 Azure 应用程序见解？ (y/N)**</span><span class="sxs-lookup"><span data-stu-id="e6b95-144">**Would you like to use Azure Applications Insights for telemetry? (y/N)**</span></span>

<span data-ttu-id="e6b95-145">选择 **不包括** [Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e6b95-145">Choose **not** to include [Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md).</span></span> <span data-ttu-id="e6b95-146">默认值为"否";输入 **n**。</span><span class="sxs-lookup"><span data-stu-id="e6b95-146">The default is no; enter **n**.</span></span>

<span data-ttu-id="e6b95-147">**默认选项卡名称 (最多为 16 个字符) ？**</span><span class="sxs-lookup"><span data-stu-id="e6b95-147">**Default Tab Name (max 16 characters)?**</span></span>

<span data-ttu-id="e6b95-148">命名选项卡。此选项卡名称将在整个项目中用作文件/URL 路径组件。</span><span class="sxs-lookup"><span data-stu-id="e6b95-148">Name your tab. This tab name will be used throughout your project as a file/URL path component.</span></span>
