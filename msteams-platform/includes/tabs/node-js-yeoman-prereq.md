## <a name="prerequisites"></a><span data-ttu-id="6f429-101">先决条件</span><span class="sxs-lookup"><span data-stu-id="6f429-101">Prerequisites</span></span>

- <span data-ttu-id="6f429-102">若要完成此快速入门，你将需要 Office 365 租户和配置了 "*允许上载自定义应用程序*" 的团队。</span><span class="sxs-lookup"><span data-stu-id="6f429-102">To complete this quickstart you will need an Office 365 tenant and a team configured with *Allow uploading custom apps* enabled.</span></span> <span data-ttu-id="6f429-103">若要了解详细信息，请参阅[准备 Office 365 租户](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="6f429-103">To learn more, see [Prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

  - <span data-ttu-id="6f429-104">如果当前没有 Office 365 帐户，可以通过 Office 365 开发人员计划注册免费订阅。</span><span class="sxs-lookup"><span data-stu-id="6f429-104">If you don't currently have an Office 365 account, you can sign up for a free subscription through the Office 365 Developer Program.</span></span> <span data-ttu-id="6f429-105">只要您使用它进行持续开发，订阅将保持活动状态。</span><span class="sxs-lookup"><span data-stu-id="6f429-105">The subscription will remain active as long as you're using it for ongoing development.</span></span> <span data-ttu-id="6f429-106">请参阅[欢迎使用 Office 365 开发人员计划](/OfficeDev/office-dev-program-docs/docs/office-365-developer-program.md)。</span><span class="sxs-lookup"><span data-stu-id="6f429-106">See [Welcome to the Office 365 Developer Program](/OfficeDev/office-dev-program-docs/docs/office-365-developer-program.md).</span></span>

<span data-ttu-id="6f429-107">此外，此项目要求在开发环境中安装以下各项：</span><span class="sxs-lookup"><span data-stu-id="6f429-107">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="6f429-108">任何文本编辑器或 IDE。</span><span class="sxs-lookup"><span data-stu-id="6f429-108">Any text editor or IDE.</span></span> <span data-ttu-id="6f429-109">您可以免费安装和使用[Visual Studio Code](https://code.visualstudio.com/download) 。</span><span class="sxs-lookup"><span data-stu-id="6f429-109">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

- <span data-ttu-id="6f429-110">[Node.js/npm](https://nodejs.org/en/)。</span><span class="sxs-lookup"><span data-stu-id="6f429-110">[Node.js/npm](https://nodejs.org/en/).</span></span> <span data-ttu-id="6f429-111">应使用最新的 LTS 版本。</span><span class="sxs-lookup"><span data-stu-id="6f429-111">You should use the latest LTS version.</span></span> <span data-ttu-id="6f429-112">节点包管理器（npm）将在安装 node.js 的情况中安装到系统中。</span><span class="sxs-lookup"><span data-stu-id="6f429-112">The Node Package Manager (npm) will install into your system with the installation of Node.js.</span></span>

- <span data-ttu-id="6f429-113">成功安装 node.js 后，在命令提示符处键入以下命令，以安装[Yeoman](https://yeoman.io/)和[gulp](https://www.npmjs.com/package/gulp-cli)程序包：</span><span class="sxs-lookup"><span data-stu-id="6f429-113">After you've successfully installed Node.js, install the [Yeoman](https://yeoman.io/) and [gulp-cli](https://www.npmjs.com/package/gulp-cli) packages by typing the following in your command prompt:</span></span>

```bash
npm install yo gulp-cli --global
```

- <span data-ttu-id="6f429-114">通过在命令提示符处键入以下内容来安装 Microsoft 团队应用生成器：</span><span class="sxs-lookup"><span data-stu-id="6f429-114">Install the Microsoft Teams Apps generator by typing the following in your command prompt:</span></span>

```bash
npm install generator-teams --global
```

## <a name="generate-your-project"></a><span data-ttu-id="6f429-115">生成项目</span><span class="sxs-lookup"><span data-stu-id="6f429-115">Generate your project</span></span>

- <span data-ttu-id="6f429-116">打开命令提示符并为您的选项卡项目创建一个新目录。</span><span class="sxs-lookup"><span data-stu-id="6f429-116">Open a command prompt and create a new directory for your tab project.</span></span>

- <span data-ttu-id="6f429-117">若要启动生成器，请导航到新目录并键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="6f429-117">To start the generator, navigate to your new directory and type the following command:</span></span>

```bash
yo teams
```

- <span data-ttu-id="6f429-118">接下来，你将提供将在应用程序的**清单 json**文件中使用的一系列值：</span><span class="sxs-lookup"><span data-stu-id="6f429-118">Next, you'll provide a series of values that will be used in your application's **manifest.json** file:</span></span>

![生成器打开屏幕截图](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

<span data-ttu-id="6f429-120">**您的解决方案名称是什么？**</span><span class="sxs-lookup"><span data-stu-id="6f429-120">**What is your solution name?**</span></span>

<span data-ttu-id="6f429-121">这是您的项目名称。</span><span class="sxs-lookup"><span data-stu-id="6f429-121">This is your project name.</span></span> <span data-ttu-id="6f429-122">您可以按 enter 接受建议的名称。</span><span class="sxs-lookup"><span data-stu-id="6f429-122">You can accept the suggested name by pressing enter.</span></span>

<span data-ttu-id="6f429-123">**要将文件存放在哪里?**</span><span class="sxs-lookup"><span data-stu-id="6f429-123">**Where do you want to place the files?**</span></span>

<span data-ttu-id="6f429-124">您当前位于项目目录中。</span><span class="sxs-lookup"><span data-stu-id="6f429-124">You're currently in your project directory.</span></span> <span data-ttu-id="6f429-125">按 enter。</span><span class="sxs-lookup"><span data-stu-id="6f429-125">Press enter.</span></span>

<span data-ttu-id="6f429-126">**Microsoft 团队应用程序项目的标题？**</span><span class="sxs-lookup"><span data-stu-id="6f429-126">**Title of your Microsoft Teams app project?**</span></span>

<span data-ttu-id="6f429-127">这是您的应用程序包名称，将在应用程序清单和说明中使用。</span><span class="sxs-lookup"><span data-stu-id="6f429-127">This is your app package name and will be used in the app manifest and description.</span></span>

<span data-ttu-id="6f429-128">**您的（公司）名称？（最多32个字符）**</span><span class="sxs-lookup"><span data-stu-id="6f429-128">**Your (company) name? (max 32 characters)**</span></span>

<span data-ttu-id="6f429-129">你的公司名称将在应用部件清单（manifest）中使用。</span><span class="sxs-lookup"><span data-stu-id="6f429-129">Your company name will be used in the app manifest.</span></span>

<br><span data-ttu-id="6f429-130">**您要使用哪个清单版本？**</span><span class="sxs-lookup"><span data-stu-id="6f429-130">**Which manifest version would you like to use?**</span></span>

<span data-ttu-id="6f429-131">选择默认架构。</span><span class="sxs-lookup"><span data-stu-id="6f429-131">Select the default schema.</span></span>

<span data-ttu-id="6f429-132">**如果你有一个，请输入你的 Microsoft 合作伙伴 Id？（保留为空将跳过）**</span><span class="sxs-lookup"><span data-stu-id="6f429-132">**Enter your Microsoft Partner Id, if you have one? (Leave blank to skip)**</span></span>

<span data-ttu-id="6f429-133">此字段不是必需的，仅当您已经是[Microsoft 合作伙伴网络](https://partner.microsoft.com)的一部分时才应使用此字段。</span><span class="sxs-lookup"><span data-stu-id="6f429-133">This field isn't required and should only be used if you're already part of the [Microsoft Partner Network](https://partner.microsoft.com).</span></span>

<span data-ttu-id="6f429-134">**您想要将什么添加到你的项目？**</span><span class="sxs-lookup"><span data-stu-id="6f429-134">**What do you want to add to your project?**</span></span>

<span data-ttu-id="6f429-135">选择 " &ast; （）" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="6f429-135">Select ( &ast; ) A Tab.</span></span>

<span data-ttu-id="6f429-136">**你将在其中承载此解决方案的 URL？**</span><span class="sxs-lookup"><span data-stu-id="6f429-136">**The URL where you will host this solution?**</span></span>

<span data-ttu-id="6f429-137">默认情况下，生成器会建议使用 Azure 网站 URL。</span><span class="sxs-lookup"><span data-stu-id="6f429-137">By default the generator suggests an Azure Web Sites URL.</span></span> <span data-ttu-id="6f429-138">您只会在本地测试您的应用程序，因此，不需要使用有效的 URL 即可完成此快速入门。</span><span class="sxs-lookup"><span data-stu-id="6f429-138">You'll only be testing your app locally, therefore, a valid URL is not necessary to complete this quickstart.</span></span>

<span data-ttu-id="6f429-139">**是否要包括测试框架和初始测试？（y/N）**</span><span class="sxs-lookup"><span data-stu-id="6f429-139">**Would you like to include Test framework and initial tests? (y/N)**</span></span>

<span data-ttu-id="6f429-140">选择**不**包含此项目的测试框架。</span><span class="sxs-lookup"><span data-stu-id="6f429-140">Choose **not** to include a test framework for this project.</span></span> <span data-ttu-id="6f429-141">默认值为 "是";输入**n**。</span><span class="sxs-lookup"><span data-stu-id="6f429-141">The default is yes; enter **n**.</span></span>

<span data-ttu-id="6f429-142">**您是否要使用适用于遥测的 Azure 应用程序见解？（y/N）**</span><span class="sxs-lookup"><span data-stu-id="6f429-142">**Would you like to use Azure Applications Insights for telemetry? (y/N)**</span></span>

<span data-ttu-id="6f429-143">选择**不**包含[Azure application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6f429-143">Choose **not** to include [Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md).</span></span> <span data-ttu-id="6f429-144">默认值为 no;输入**n**。</span><span class="sxs-lookup"><span data-stu-id="6f429-144">The default is no; enter **n**.</span></span>

<span data-ttu-id="6f429-145">**默认选项卡名称（最多16个字符）？**</span><span class="sxs-lookup"><span data-stu-id="6f429-145">**Default Tab Name (max 16 characters)?**</span></span>

<span data-ttu-id="6f429-146">命名您的选项卡。此选项卡名称将在整个项目中用作文件/URL 路径组件。</span><span class="sxs-lookup"><span data-stu-id="6f429-146">Name your tab. This tab name will be used throughout your project as a file/URL path component.</span></span>
