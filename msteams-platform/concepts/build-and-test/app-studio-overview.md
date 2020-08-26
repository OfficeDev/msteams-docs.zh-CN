---
title: Microsoft 团队的应用程序 Studio 入门
description: 使用应用程序 Studio 开始在 Microsoft 团队中构建出色的应用程序
keywords: 入门应用程序 studio 团队
ms.date: 03/20/2019
ms.openlocfilehash: b8bae38ae2a3044d87389b4bd5ee3d5a7d1e029d
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874875"
---
# <a name="quickly-develop-apps-with-app-studio-for-microsoft-teams"></a><span data-ttu-id="a89f5-104">使用 Microsoft 团队的应用程序工作室快速开发应用程序</span><span class="sxs-lookup"><span data-stu-id="a89f5-104">Quickly develop apps with App Studio for Microsoft Teams</span></span>

<span data-ttu-id="a89f5-105">无论是为企业中的团队开发自定义应用程序，还是通过简化应用程序的清单和包，并提供卡片编辑器和响应控件库等有用的工具，应用程序 Studio 都可以轻松地开始创建或集成您自己的 Microsoft 团队应用程序。</span><span class="sxs-lookup"><span data-stu-id="a89f5-105">App Studio makes it easy to start creating or integrating your own Microsoft Teams apps, whether you develop custom apps for your enterprise or SaaS applications for teams around the world by streamlining the creation of the manifest and package for your app and providing useful tools like the Card Editor and a React control library.</span></span>

## <a name="installing-app-studio"></a><span data-ttu-id="a89f5-106">安装应用程序 Studio</span><span class="sxs-lookup"><span data-stu-id="a89f5-106">Installing App Studio</span></span>

<span data-ttu-id="a89f5-107">应用程序 Studio 是团队存储中可找到的团队应用程序。</span><span class="sxs-lookup"><span data-stu-id="a89f5-107">App Studio is a Teams app which can be found in the Teams store.</span></span> <span data-ttu-id="a89f5-108">按照以下直接下载链接： [App Studio](https://aka.ms/InstallTeamsAppStudio) (您还可以在应用商店) 中找到该应用程序。</span><span class="sxs-lookup"><span data-stu-id="a89f5-108">Follow this link for direct download: [App Studio](https://aka.ms/InstallTeamsAppStudio) (you can also find the app in the app store).</span></span>

<span data-ttu-id="a89f5-109">在应用商店中，搜索应用程序 Studio。</span><span class="sxs-lookup"><span data-stu-id="a89f5-109">In the store, search for App Studio.</span></span>

![应用程序 studio 的存储项](~/assets/images/get-started/storeteamsappstudio.png)

<span data-ttu-id="a89f5-111">选择应用程序制作室磁贴以打开 "应用安装" 页：</span><span class="sxs-lookup"><span data-stu-id="a89f5-111">Select the App Studio tile to open the app install page:</span></span>

![配置应用程序 studio](~/assets/images/get-started/teamsappstudioconfiguration.png)

<span data-ttu-id="a89f5-113">选择 " *安装*"。</span><span class="sxs-lookup"><span data-stu-id="a89f5-113">Select *install*.</span></span>

![应用程序工作室](~/assets/images/get-started/teamsappstudio.png)

<span data-ttu-id="a89f5-115">在应用程序 Studio 中，单击 " *清单编辑器* " 选项卡，可在其中导入现有应用程序或创建新的应用程序。</span><span class="sxs-lookup"><span data-stu-id="a89f5-115">Once you are in App Studio, click on the *Manifest editor* tab where you can either import an existing app or create a new app.</span></span>

## <a name="app-studio-features"></a><span data-ttu-id="a89f5-116">应用程序工作室功能</span><span class="sxs-lookup"><span data-stu-id="a89f5-116">App Studio Features</span></span>

### <a name="conversation"></a><span data-ttu-id="a89f5-117">对话</span><span class="sxs-lookup"><span data-stu-id="a89f5-117">Conversation</span></span>

<span data-ttu-id="a89f5-118">在您通过将其发送给自己时，您可以在应用程序中看到在 [应用程序 Studio 中创建的卡片](#card-editor) 在团队中的外观。</span><span class="sxs-lookup"><span data-stu-id="a89f5-118">This is where you can see what [cards you create in App Studio](#card-editor) look like in Teams when you test them by sending them to yourself.</span></span>

### <a name="manifest-editor"></a><span data-ttu-id="a89f5-119">清单编辑器</span><span class="sxs-lookup"><span data-stu-id="a89f5-119">Manifest Editor</span></span>

<span data-ttu-id="a89f5-120">如前所述，Microsoft 团队应用程序包最重要的部分是它在文件上的 manifest.js。</span><span class="sxs-lookup"><span data-stu-id="a89f5-120">As mentioned earlier, the most significant part of a Microsoft Teams app package is its manifest.json file.</span></span> <span data-ttu-id="a89f5-121">此文件必须符合 [团队应用程序架构](~/resources/schema/manifest-schema.md)，其中包含允许团队正确向用户提供你的应用程序的元数据。</span><span class="sxs-lookup"><span data-stu-id="a89f5-121">This file, which must conform to the [Teams App schema](~/resources/schema/manifest-schema.md), contains metadata which allows Teams to correctly present your app to users.</span></span>

<span data-ttu-id="a89f5-122">应用程序 Studio 中的 "清单编辑器" 选项卡简化了清单的创建，使您能够描述应用程序、上载图标、添加应用程序功能，并生成可轻松地将其上载到团队以供测试或分发以供其他人使用的 .zip 文件。</span><span class="sxs-lookup"><span data-stu-id="a89f5-122">The Manifest Editor tab in App Studio simplifies creating the manifest, allowing you to describe the app, upload your icons, add app capabilities, and produce a .zip file which can easily be uploaded into Teams for testing or distributed for others to use.</span></span> <span data-ttu-id="a89f5-123">请注意，应用程序 Studio 不会为您的应用程序生成功能代码，也不会承载您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="a89f5-123">Note that App Studio does not produce functional code for your app, or host your app.</span></span> <span data-ttu-id="a89f5-124">您的应用程序必须已在应用程序上传过程的清单中列出的 URL 处进行托管和运行，才能生成有效的应用程序。</span><span class="sxs-lookup"><span data-stu-id="a89f5-124">Your app must already be hosted and running at the URL listed in the manifest for the app upload process to result in a working app.</span></span>

#### <a name="details"></a><span data-ttu-id="a89f5-125">详细信息</span><span class="sxs-lookup"><span data-stu-id="a89f5-125">Details</span></span>

<span data-ttu-id="a89f5-126">清单编辑器的 "详细信息" 部分定义了正在进行的应用程序的简要说明。</span><span class="sxs-lookup"><span data-stu-id="a89f5-126">The details section of the Manifest Editor defines the high-level description of the app you are making.</span></span> <span data-ttu-id="a89f5-127">其中包括应用程序的名称、说明和视觉品牌等内容。</span><span class="sxs-lookup"><span data-stu-id="a89f5-127">This includes things such as the app’s name, description, and visual branding.</span></span> <span data-ttu-id="a89f5-128">您可以为您的应用程序自动生成 GUID，并提供隐私声明和使用条款的 Url。</span><span class="sxs-lookup"><span data-stu-id="a89f5-128">You can automatically generate a GUID for your app and provide URLs for your privacy statement and terms of use.</span></span>

#### <a name="capabilities"></a><span data-ttu-id="a89f5-129">功能</span><span class="sxs-lookup"><span data-stu-id="a89f5-129">Capabilities</span></span>

<span data-ttu-id="a89f5-130">清单编辑器的 "功能" 部分是指定义应用程序功能的位置，其中列出了每个功能的详细信息。</span><span class="sxs-lookup"><span data-stu-id="a89f5-130">The capabilities section of the Manifest Editor is where the app's capabilities are defined and where details of each of those capabilities are listed.</span></span>

##### <a name="tabs"></a><span data-ttu-id="a89f5-131">选项卡</span><span class="sxs-lookup"><span data-stu-id="a89f5-131">Tabs</span></span>

* <span data-ttu-id="a89f5-132">**团队选项卡。**</span><span class="sxs-lookup"><span data-stu-id="a89f5-132">**Team Tabs.**</span></span> <span data-ttu-id="a89f5-133">"团队" 选项卡成为通道的一部分，可提供对团队信息和资源的快速访问。</span><span class="sxs-lookup"><span data-stu-id="a89f5-133">A team tab becomes part of a channel and provides quick access to team information and resources.</span></span> <span data-ttu-id="a89f5-134">例如，频道的 "Planner" 选项卡包含一个计划;Power BI 选项卡映射到特定报告。</span><span class="sxs-lookup"><span data-stu-id="a89f5-134">For example, the Planner tab for a channel contains a single plan; the Power BI tab maps to a specific report.</span></span> <span data-ttu-id="a89f5-135">用户可以向下钻取到相关上下文，但不能在选项卡外导航。例如，Power BI 选项卡不启用到其他 Power BI 报告的导航，但确实启用了 " *转到网站* " 按钮，该按钮可在主 Power bi 网站中启动报告。</span><span class="sxs-lookup"><span data-stu-id="a89f5-135">Users can drill down to the relevant context, but they should not be able to navigate outside the tab. The Power BI tab, for instance, doesn't enable navigation to other Power BI reports, but it does enable the *Go to website* button that launches the report in the main Power BI website.</span></span>

  <span data-ttu-id="a89f5-136">对于 "团队" 选项卡，您必须提供一个用于呈现选项和收集信息的 *配置 URL* ，以便用户可以自定义选项卡的内容和体验。当用户第一次将选项卡添加到频道中时，将显示此 iframed HTML 页面。</span><span class="sxs-lookup"><span data-stu-id="a89f5-136">For team tabs, you must provide a *Configuration URL* to present options and gather information so users can customize the content and experience of your tab. This iframed HTML page is displayed when a user first adds the tab to a channel.</span></span>

  <span data-ttu-id="a89f5-137">此外，还必须提供 tab 要从中加载或链接到的任何其他域。</span><span class="sxs-lookup"><span data-stu-id="a89f5-137">You must also provide any additional domains that the tab expects to load from or link to.</span></span>

* <span data-ttu-id="a89f5-138">**个人选项卡。**</span><span class="sxs-lookup"><span data-stu-id="a89f5-138">**Personal Tabs.**</span></span> <span data-ttu-id="a89f5-139">此部分允许您定义一组默认情况下在个人应用程序体验 (中显示的选项卡，即用户在团队或频道) 上下文之外的应用体验。</span><span class="sxs-lookup"><span data-stu-id="a89f5-139">This section lets you define a set of tabs that are presented by default in the personal app experience (i.e. the experience a user has with your app outside the context of a team or channel).</span></span> <span data-ttu-id="a89f5-140">在此部分中，提供选项卡名称、唯一标识符、指向要在团队中显示的 UI 的 URL，以及如果用户选择在浏览器中查看选项卡时要使用的 URL （可选）。</span><span class="sxs-lookup"><span data-stu-id="a89f5-140">In this section, provide the tab name, a unique identifier, the URL that points to the UI to be displayed in Teams, and optionally, the URL to use if a user opts to view the tab in a browser.</span></span> <span data-ttu-id="a89f5-141">与团队选项卡一样，提供要从中从其加载或链接的选项卡的任何其他域。</span><span class="sxs-lookup"><span data-stu-id="a89f5-141">As with Teams tabs, provide any additional domains from which the tab expects to load from or link to.</span></span>

##### <a name="bots"></a><span data-ttu-id="a89f5-142">机器人</span><span class="sxs-lookup"><span data-stu-id="a89f5-142">Bots</span></span>

<span data-ttu-id="a89f5-143">此部分允许您向应用中添加 [对话机器人](~/bots/what-are-bots.md) 。</span><span class="sxs-lookup"><span data-stu-id="a89f5-143">This section allows you to add a [conversational bot](~/bots/what-are-bots.md) to your app.</span></span> <span data-ttu-id="a89f5-144">如果已有使用 Bot 框架注册的 bot，可以通过单击 "设置" " *设置* " 并提供 bot 的名称、BOT 框架 ID，并定义 bot 将使用的范围来添加该 bot。</span><span class="sxs-lookup"><span data-stu-id="a89f5-144">If you already have a bot registered with Bot Framework, you can add that bot by clicking *Set Up* and supplying the bot's name, Bot Framework ID, and defining the scopes in which the bot will work.</span></span>

<span data-ttu-id="a89f5-145">如果您尚未向 Bot 框架注册 bot，请单击 " *注册* " 以创建一个新的 bot。</span><span class="sxs-lookup"><span data-stu-id="a89f5-145">If you have not yet registered a bot with the Bot Framework, click *Register* to create a new one.</span></span> <span data-ttu-id="a89f5-146">完成对你的 bot 的注册后，请返回清单编辑器的此部分，以输入其名称和 Bot 框架 ID。</span><span class="sxs-lookup"><span data-stu-id="a89f5-146">Once you’re done registering your bot, come back to this section of the Manifest Editor to enter its name and Bot Framework ID.</span></span>

<span data-ttu-id="a89f5-147">提供你的 bot 的信息后，你现在可以选择定义你的 bot 可以向用户建议的命令列表。</span><span class="sxs-lookup"><span data-stu-id="a89f5-147">Once you have supplied your bot's information, you can now optionally define a list of commands that your bot can suggest to users.</span></span> <span data-ttu-id="a89f5-148">添加命令的名称、指示其语法和参数的命令的说明以及此命令应应用于的作用域 (s) 。</span><span class="sxs-lookup"><span data-stu-id="a89f5-148">Add the name of the command, a description of the command which indicates its syntax and arguments, and the scope(s) to which this command should apply.</span></span>

<span data-ttu-id="a89f5-149">请注意，如果您已将你的 bot 定义为仅支持一个作用域，则将忽略为不受支持的作用域指定的命令。</span><span class="sxs-lookup"><span data-stu-id="a89f5-149">Note that if you have defined your bot to only support one scope, commands specified for the unsupported scope will be ignored.</span></span> <span data-ttu-id="a89f5-150">你可以随时编辑你的 bot 支持的范围。</span><span class="sxs-lookup"><span data-stu-id="a89f5-150">You can edit the scopes your bot supports at any time.</span></span>

##### <a name="connectors"></a><span data-ttu-id="a89f5-151">连接器</span><span class="sxs-lookup"><span data-stu-id="a89f5-151">Connectors</span></span>

<span data-ttu-id="a89f5-152">此部分允许您将连接器添加到您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="a89f5-152">This section allows you to add a connector to your app.</span></span> <span data-ttu-id="a89f5-153">如果您已经注册了 Office 365 连接器，请选择 " *设置* "，并输入连接器的名称和 ID。</span><span class="sxs-lookup"><span data-stu-id="a89f5-153">If you already have registered an Office 365 connector, choose *Set up* and enter the name and ID of the connector.</span></span> <span data-ttu-id="a89f5-154">如果您想要新的连接器，请单击 " *注册* " 以转到浏览器中的连接器开发人员仪表板。</span><span class="sxs-lookup"><span data-stu-id="a89f5-154">If you want a new connector click *Register* to be taken to the Connector Developer Dashboard in your browser.</span></span>

##### <a name="messaging-extensions"></a><span data-ttu-id="a89f5-155">消息扩展</span><span class="sxs-lookup"><span data-stu-id="a89f5-155">Messaging Extensions</span></span>

<span data-ttu-id="a89f5-156">[邮件扩展](~/messaging-extensions/what-are-messaging-extensions.md) 是用户在 Microsoft 团队中与您的应用程序进行接洽的一种强大方式。</span><span class="sxs-lookup"><span data-stu-id="a89f5-156">[Messaging extensions](~/messaging-extensions/what-are-messaging-extensions.md) are a powerful way for users to engage with your app within Microsoft Teams.</span></span> <span data-ttu-id="a89f5-157">用户可以查询服务中的信息，并以卡片形式发布该信息，直接进入频道或聊天对话。</span><span class="sxs-lookup"><span data-stu-id="a89f5-157">Users can query for information from your service and post that information in the form of cards, right into the channel or chat conversation.</span></span>

<span data-ttu-id="a89f5-158">邮件扩展由 Bot 框架 bot 提供支持，因此需要配置的 Bot 才能运行。</span><span class="sxs-lookup"><span data-stu-id="a89f5-158">Messaging extensions are powered by Bot Framework bots, so they require a configured bot to operate.</span></span> <span data-ttu-id="a89f5-159">如果您具有要为邮件扩展提供电源的 bot 的名称和 Bot 框架 ID，请输入该 ID。</span><span class="sxs-lookup"><span data-stu-id="a89f5-159">If you have the name and Bot Framework ID of the bot you would like to power the messaging extension, enter it.</span></span> <span data-ttu-id="a89f5-160">否则，请单击 " *注册* " 创建一个并在随后输入信息。</span><span class="sxs-lookup"><span data-stu-id="a89f5-160">Otherwise, click *Register* to create one and enter the information afterward.</span></span> <span data-ttu-id="a89f5-161">选择用户是否可以更新邮件扩展的配置。</span><span class="sxs-lookup"><span data-stu-id="a89f5-161">Select whether the configuration of a messaging extension can be updated by the user.</span></span>

<span data-ttu-id="a89f5-162">配置了基础 bot 后，定义邮件扩展可接受的命令和参数。</span><span class="sxs-lookup"><span data-stu-id="a89f5-162">Once you have the underlying bot configured, define the commands and parameters which the messaging extension can accept.</span></span>

<span data-ttu-id="a89f5-163">每个命令都需要一个标题和一个 ID。</span><span class="sxs-lookup"><span data-stu-id="a89f5-163">Each command requires a title and an ID.</span></span> <span data-ttu-id="a89f5-164">该命令可以选择包含用户的说明。</span><span class="sxs-lookup"><span data-stu-id="a89f5-164">The command can optionally contain a description for the user.</span></span> <span data-ttu-id="a89f5-165">每个命令最长可支持五个参数，其中每个都需要：</span><span class="sxs-lookup"><span data-stu-id="a89f5-165">Each command can support up to five parameters, each of which requires:</span></span>

* <span data-ttu-id="a89f5-166">在团队客户端中显示并包含在用户请求中的参数的名称</span><span class="sxs-lookup"><span data-stu-id="a89f5-166">The name of the parameter as it appears in the Teams client and is included in the user request</span></span>
* <span data-ttu-id="a89f5-167">用户友好的标题</span><span class="sxs-lookup"><span data-stu-id="a89f5-167">A user-friendly title</span></span>
* <span data-ttu-id="a89f5-168">可选说明</span><span class="sxs-lookup"><span data-stu-id="a89f5-168">An optional description</span></span>

#### <a name="test-and-distribute"></a><span data-ttu-id="a89f5-169">测试和分发</span><span class="sxs-lookup"><span data-stu-id="a89f5-169">Test and Distribute</span></span>

<span data-ttu-id="a89f5-170">定义完应用程序后，"测试和分发" 部分将允许您将应用程序的定义导出为 zip 文件，然后可以共享该文件并将其上载到团队客户端进行测试。</span><span class="sxs-lookup"><span data-stu-id="a89f5-170">Once you have finished defining your application, the Test and Distribute section allows you export your app’s definition as a zip file which then can be shared and uploaded into the Teams client for testing.</span></span> <span data-ttu-id="a89f5-171">单击 "导出" 会将 zip 文件下载为默认下载目录中 *appname.zip* 。</span><span class="sxs-lookup"><span data-stu-id="a89f5-171">Clicking export downloads the zip file as *appname.zip* in your default download directory.</span></span>

##### <a name="publish-your-app-to-teams"></a><span data-ttu-id="a89f5-172">将您的应用程序发布到团队</span><span class="sxs-lookup"><span data-stu-id="a89f5-172">Publish your app to Teams</span></span>
<span data-ttu-id="a89f5-173">在您的项目主页上，您可以将应用程序上载到团队，将您的应用程序提交到贵组织中用户的公司自定义应用商店，或将您的应用程序提交到所有团队用户的应用程序源。</span><span class="sxs-lookup"><span data-stu-id="a89f5-173">On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span> <span data-ttu-id="a89f5-174">你的 IT 管理员将查看这些提交。</span><span class="sxs-lookup"><span data-stu-id="a89f5-174">Your IT admin will review these submissions.</span></span> <span data-ttu-id="a89f5-175">您可以返回到 " *发布* " 页面以查看您的提交状态，并了解您的应用程序是否已由 IT 管理员批准或拒绝。此外，您还可以将更新提交到您的应用程序或取消任何当前活动的提交。</span><span class="sxs-lookup"><span data-stu-id="a89f5-175">You can return to the *Publish* page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

### <a name="card-editor"></a><span data-ttu-id="a89f5-176">卡片编辑器</span><span class="sxs-lookup"><span data-stu-id="a89f5-176">Card Editor</span></span>

<span data-ttu-id="a89f5-177">卡片是简短或相关信息片段的容器。</span><span class="sxs-lookup"><span data-stu-id="a89f5-177">A card is a container for short or related pieces of information.</span></span> <span data-ttu-id="a89f5-178">Microsoft 团队支持可具有多个属性和附件的卡片。</span><span class="sxs-lookup"><span data-stu-id="a89f5-178">Microsoft Teams supports cards, which can have multiple properties and attachments.</span></span> <span data-ttu-id="a89f5-179">卡片是 bot 和连接器向用户中继可操作信息的关键方式。</span><span class="sxs-lookup"><span data-stu-id="a89f5-179">Cards are a key way that bots and connectors relay actionable information to users.</span></span> 

<span data-ttu-id="a89f5-180">为了使此过程更简单且更易于出错，"卡片编辑器" 选项卡可让您使用窗体构建英雄卡片或缩略图卡，并验证和测试生成的卡片 (完全按照用户将通过 bot 查看) 的情况。</span><span class="sxs-lookup"><span data-stu-id="a89f5-180">To make this process easier and less error-prone, the Card Editor tab lets you build Hero Cards or Thumbnail Cards using a form and verify and test the resulting card (exactly as a user would see it) via a bot.</span></span> <span data-ttu-id="a89f5-181">它还为您可以复制/粘贴到您的应用程序源代码中的卡片提供相应的 JSON、c # 或 Node.js 代码。</span><span class="sxs-lookup"><span data-stu-id="a89f5-181">It also provides the corresponding JSON, C#, or Node.js code for the card that you can copy/paste into your app's source code.</span></span>

<span data-ttu-id="a89f5-182">如果您已经有要在团队中验证的卡片，则可以将该卡片的 JSON 粘贴到 " *添加卡片信息* " 下的 json 选项卡中，并将其发送给自己，以查看其在聊天中的外观。</span><span class="sxs-lookup"><span data-stu-id="a89f5-182">If you already have a card that you would like to verify inside Teams, you can paste the JSON for that card into the JSON tab under *Add card info* and send it to yourself to see what it looks like in a chat.</span></span>

### <a name="react-control-library"></a><span data-ttu-id="a89f5-183">响应控件库</span><span class="sxs-lookup"><span data-stu-id="a89f5-183">React Control Library</span></span>

>[!Note]
> <span data-ttu-id="a89f5-184">这将在将来弃用此响应控制库。</span><span class="sxs-lookup"><span data-stu-id="a89f5-184">This React control library will be deprecated in the future.</span></span> <span data-ttu-id="a89f5-185">考虑使用 [熟知的 ui 响应控件作为替代](https://microsoft.github.io/fluent-ui-react/) (以前的 Stardust UI) 。</span><span class="sxs-lookup"><span data-stu-id="a89f5-185">Consider using the [Fluent-UI react controls as an alternative](https://microsoft.github.io/fluent-ui-react/) (formerly Stardust UI).</span></span>

<span data-ttu-id="a89f5-186">创建遵循 "团队最佳实践" 的应用程序是为您的应用程序提供与团队客户端体验无缝匹配的外观的绝佳方式。</span><span class="sxs-lookup"><span data-stu-id="a89f5-186">Creating an app that follows the Teams best practices is a great way to give your app a look and feel that fits seamlessly with the Teams client experience.</span></span> <span data-ttu-id="a89f5-187">您使用的 UI 控件对实现该结尾至关重要。</span><span class="sxs-lookup"><span data-stu-id="a89f5-187">The UI controls that you use are critical to achieving that end.</span></span> <span data-ttu-id="a89f5-188">为了便于创建一致的 UI，应用程序 Studio 提供了多种类别的 UI 控件，这些控件遵循团队设计原则。</span><span class="sxs-lookup"><span data-stu-id="a89f5-188">To make it easier to create a consistent UI, App Studio provides several categories of UI controls which follow Teams design principles.</span></span>

<span data-ttu-id="a89f5-189">提供了控件和相应的响应组件的示例，并准备好在生成应用程序时使用它们。</span><span class="sxs-lookup"><span data-stu-id="a89f5-189">Examples of the controls and corresponding React components are provided and ready to use in building your app.</span></span>

#### <a name="controls"></a><span data-ttu-id="a89f5-190">控件</span><span class="sxs-lookup"><span data-stu-id="a89f5-190">Controls</span></span>

<span data-ttu-id="a89f5-191">控件包括：</span><span class="sxs-lookup"><span data-stu-id="a89f5-191">Controls include:</span></span>

* <span data-ttu-id="a89f5-192">按钮</span><span class="sxs-lookup"><span data-stu-id="a89f5-192">Buttons</span></span>
* <span data-ttu-id="a89f5-193">下拉</span><span class="sxs-lookup"><span data-stu-id="a89f5-193">Dropdowns</span></span>
* <span data-ttu-id="a89f5-194">复选框</span><span class="sxs-lookup"><span data-stu-id="a89f5-194">Checkboxes</span></span>
* <span data-ttu-id="a89f5-195">单选按钮</span><span class="sxs-lookup"><span data-stu-id="a89f5-195">Radio Buttons</span></span>
* <span data-ttu-id="a89f5-196">关</span><span class="sxs-lookup"><span data-stu-id="a89f5-196">Toggles</span></span>
* <span data-ttu-id="a89f5-197">文本区域</span><span class="sxs-lookup"><span data-stu-id="a89f5-197">Text Areas</span></span>
* <span data-ttu-id="a89f5-198">链接</span><span class="sxs-lookup"><span data-stu-id="a89f5-198">Links</span></span>
* <span data-ttu-id="a89f5-199">选项卡</span><span class="sxs-lookup"><span data-stu-id="a89f5-199">Tabs</span></span>
* <span data-ttu-id="a89f5-200">表格</span><span class="sxs-lookup"><span data-stu-id="a89f5-200">Tables</span></span>
* <span data-ttu-id="a89f5-201">图标</span><span class="sxs-lookup"><span data-stu-id="a89f5-201">Icons</span></span>
