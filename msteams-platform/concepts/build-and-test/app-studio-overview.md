---
title: App Studio for Microsoft Teams 入门
description: 开始使用 App Studio 在 Microsoft Teams 中构建出色的应用
keywords: 应用室团队入门
localization_priority: Normal
ms.topic: overview
ms.openlocfilehash: 391086b85f0e68e1a864c3d4254bdbe62b5eaa1a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565198"
---
# <a name="quickly-develop-apps-with-app-studio-for-microsoft-teams"></a><span data-ttu-id="62610-104">使用 App Studio for Microsoft Teams 快速开发应用</span><span class="sxs-lookup"><span data-stu-id="62610-104">Quickly develop apps with App Studio for Microsoft Teams</span></span>

<span data-ttu-id="62610-105">无论你为企业开发自定义应用还是为世界各地的团队开发 SaaS 应用程序，App Studio 都可以轻松创建或集成你自己的 Microsoft Teams 应用，其方式包括简化应用程序的清单和包的创建，并提供卡片编辑器和响应控制库等有用工具。</span><span class="sxs-lookup"><span data-stu-id="62610-105">App Studio makes it easy to start creating or integrating your own Microsoft Teams apps, whether you develop custom apps for your enterprise or SaaS applications for teams around the world by streamlining the creation of the manifest and package for your app and providing useful tools like the Card Editor and a React control library.</span></span>

## <a name="installing-app-studio"></a><span data-ttu-id="62610-106">安装 App Studio</span><span class="sxs-lookup"><span data-stu-id="62610-106">Installing App Studio</span></span>

<span data-ttu-id="62610-107">App Studio 是一款可在 Teams 商店找到的 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="62610-107">App Studio is a Teams app which can be found in the Teams store.</span></span> <span data-ttu-id="62610-108">按照此链接直接下载[App Studio。](https://aka.ms/InstallTeamsAppStudio)</span><span class="sxs-lookup"><span data-stu-id="62610-108">Follow this link for direct download [App Studio](https://aka.ms/InstallTeamsAppStudio).</span></span> <span data-ttu-id="62610-109">还可以在应用商店中查找该应用。</span><span class="sxs-lookup"><span data-stu-id="62610-109">You can also find the app in the app store.</span></span>

<span data-ttu-id="62610-110">在应用商店中，搜索 App Studio。</span><span class="sxs-lookup"><span data-stu-id="62610-110">In the store, search for App Studio.</span></span>

![App studio 的应用商店条目](~/assets/images/get-started/storeteamsappstudio.png)

<span data-ttu-id="62610-112">选择 App Studio 磁贴以打开应用安装页面：</span><span class="sxs-lookup"><span data-stu-id="62610-112">Select the App Studio tile to open the app install page:</span></span>

![配置 app studio](~/assets/images/get-started/teamsappstudioconfiguration.png)

<span data-ttu-id="62610-114">选择“**安装**”。</span><span class="sxs-lookup"><span data-stu-id="62610-114">Select **install**.</span></span>

![app studio](~/assets/images/get-started/teamsappstudio.png)

<span data-ttu-id="62610-116">在 App Studio 中后，单击 **清单编辑器** 选项卡，可在其中导入现有应用或创建新应用。</span><span class="sxs-lookup"><span data-stu-id="62610-116">Once you are in App Studio, click on the **Manifest editor** tab where you can either import an existing app or create a new app.</span></span>

## <a name="app-studio-features"></a><span data-ttu-id="62610-117">App Studio 功能</span><span class="sxs-lookup"><span data-stu-id="62610-117">App Studio Features</span></span>

<span data-ttu-id="62610-118">本节介绍对话、清单编辑器、详细信息和功能等功能。</span><span class="sxs-lookup"><span data-stu-id="62610-118">This section covers features, such as conversation, manifest editor, details, and capabilities.</span></span> <span data-ttu-id="62610-119">可以使用应用自定义自定义自定义功能。</span><span class="sxs-lookup"><span data-stu-id="62610-119">You can customize your capabilities using app customization.</span></span>

### <a name="conversation"></a><span data-ttu-id="62610-120">对话</span><span class="sxs-lookup"><span data-stu-id="62610-120">Conversation</span></span>

<span data-ttu-id="62610-121">你可以在这里查看在 App Studio [在 App Studio](#card-editor) 将卡片发送到你自己来测试这些卡片在 Teams 中的外观。</span><span class="sxs-lookup"><span data-stu-id="62610-121">This is where you can see what [cards you create in App Studio](#card-editor) look like in Teams when you test them by sending them to yourself.</span></span>

### <a name="manifest-editor"></a><span data-ttu-id="62610-122">清单编辑器</span><span class="sxs-lookup"><span data-stu-id="62610-122">Manifest Editor</span></span>

<span data-ttu-id="62610-123">如前文所述，Microsoft Teams 应用包最重要的部分就是其 manifest.json 文件。</span><span class="sxs-lookup"><span data-stu-id="62610-123">As mentioned earlier, the most significant part of a Microsoft Teams app package is its manifest.json file.</span></span> <span data-ttu-id="62610-124">此文件必须遵循 [Teams 应用架构](~/resources/schema/manifest-schema.md)，包含可使 Teams 向用户正确呈现应用的元数据。</span><span class="sxs-lookup"><span data-stu-id="62610-124">This file, which must conform to the [Teams App schema](~/resources/schema/manifest-schema.md), contains metadata which allows Teams to correctly present your app to users.</span></span>

<span data-ttu-id="62610-125">App Studio 中的"清单编辑器"选项卡简化了清单的创建，可用于描述应用、上传图标、添加应用功能并生成 .zip 文件，可轻松上传到 Teams，以便进行测试或分发供其他人使用。</span><span class="sxs-lookup"><span data-stu-id="62610-125">The Manifest Editor tab in App Studio simplifies creating the manifest, allowing you to describe the app, upload your icons, add app capabilities, and produce a .zip file which can easily be uploaded into Teams for testing or distributed for others to use.</span></span> <span data-ttu-id="62610-126">请注意，App Studio 不会为应用生成功能代码，也不托管应用。</span><span class="sxs-lookup"><span data-stu-id="62610-126">Note that App Studio does not produce functional code for your app, or host your app.</span></span> <span data-ttu-id="62610-127">应用必须已在应用上传流程的清单中列出的 URL 上托管并运行，以产生工作应用。</span><span class="sxs-lookup"><span data-stu-id="62610-127">Your app must already be hosted and running at the URL listed in the manifest for the app upload process to result in a working app.</span></span>

#### <a name="details"></a><span data-ttu-id="62610-128">详细信息</span><span class="sxs-lookup"><span data-stu-id="62610-128">Details</span></span>

<span data-ttu-id="62610-129">清单编辑器的详细信息部分定义所创建应用的详细信息。</span><span class="sxs-lookup"><span data-stu-id="62610-129">The details section of the Manifest Editor defines the high-level description of the app you are making.</span></span> <span data-ttu-id="62610-130">这包括应用的名称、说明和视觉品牌等内容。</span><span class="sxs-lookup"><span data-stu-id="62610-130">This includes things such as the app’s name, description, and visual branding.</span></span> <span data-ttu-id="62610-131">可以自动生成应用程序的 GUID，并提供隐私声明和使用条款的 URL。</span><span class="sxs-lookup"><span data-stu-id="62610-131">You can automatically generate a GUID for your app and provide URLs for your privacy statement and terms of use.</span></span>

#### <a name="capabilities"></a><span data-ttu-id="62610-132">功能</span><span class="sxs-lookup"><span data-stu-id="62610-132">Capabilities</span></span>

<span data-ttu-id="62610-133">清单编辑器的功能部分介绍定义应用的功能并列出其中每个功能的详细信息。</span><span class="sxs-lookup"><span data-stu-id="62610-133">The capabilities section of the Manifest Editor is where the app's capabilities are defined and where details of each of those capabilities are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="62610-134">最佳做法是，你必须提供自定义指南，以便应用用户和客户在自定义应用时遵循这些准则。</span><span class="sxs-lookup"><span data-stu-id="62610-134">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> <span data-ttu-id="62610-135">有关详细信息，请参阅自定义[应用程序中Microsoft Teams。](/MicrosoftTeams/customize-apps)</span><span class="sxs-lookup"><span data-stu-id="62610-135">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>


##### <a name="tabs"></a><span data-ttu-id="62610-136">选项卡</span><span class="sxs-lookup"><span data-stu-id="62610-136">Tabs</span></span>

* <span data-ttu-id="62610-137">**团队选项卡。**</span><span class="sxs-lookup"><span data-stu-id="62610-137">**Team Tabs.**</span></span> <span data-ttu-id="62610-138">团队选项卡将成为频道的一部分，可提供对团队信息和资源的快速访问。</span><span class="sxs-lookup"><span data-stu-id="62610-138">A team tab becomes part of a channel and provides quick access to team information and resources.</span></span> <span data-ttu-id="62610-139">例如，频道的"Planner"选项卡包含单个计划;Power BI 选项卡映射到特定报表。</span><span class="sxs-lookup"><span data-stu-id="62610-139">For example, the Planner tab for a channel contains a single plan; the Power BI tab maps to a specific report.</span></span> <span data-ttu-id="62610-140">用户可以向下钻取相关上下文，但无法导航到选项卡外部。例如，Power BI 选项卡不会启用到其他 Power BI 报表的导航，但它允许" *转到网站* "按钮，该按钮在 Power BI 主网站中启动报表。</span><span class="sxs-lookup"><span data-stu-id="62610-140">Users can drill down to the relevant context, but they should not be able to navigate outside the tab. The Power BI tab, for instance, doesn't enable navigation to other Power BI reports, but it does enable the *Go to website* button that launches the report in the main Power BI website.</span></span>

  <span data-ttu-id="62610-141">对于团队选项卡，必须使用 *配置 URL* 显示选项并收集信息，以便用户可以自定义选项卡的内容和体验。当用户首次将选项卡添加到频道时，将显示此 HTML 表格。</span><span class="sxs-lookup"><span data-stu-id="62610-141">For team tabs, you must provide a *Configuration URL* to present options and gather information so users can customize the content and experience of your tab. This iframed HTML page is displayed when a user first adds the tab to a channel.</span></span>

  <span data-ttu-id="62610-142">你还必须提供选项卡期望从其加载或链接到的任何其他域。</span><span class="sxs-lookup"><span data-stu-id="62610-142">You must also provide any additional domains that the tab expects to load from or link to.</span></span>

* <span data-ttu-id="62610-143">**个人选项卡。**</span><span class="sxs-lookup"><span data-stu-id="62610-143">**Personal Tabs.**</span></span> <span data-ttu-id="62610-144">本部分允许你定义一组选项卡，这些选项卡默认在个人应用体验中显示 (用户在团队或频道应用的上下文之外使用你的应用时) 。</span><span class="sxs-lookup"><span data-stu-id="62610-144">This section lets you define a set of tabs that are presented by default in the personal app experience (experience a user has with your app outside the context of a team or channel).</span></span> <span data-ttu-id="62610-145">在这部分内容中，提供选项卡名称、唯一标识符、指向将在 Teams 中显示的 UI 的 URL，以及用户选择在浏览器中查看选项卡时使用的 URL（可选）。</span><span class="sxs-lookup"><span data-stu-id="62610-145">In this section, provide the tab name, a unique identifier, the URL that points to the UI to be displayed in Teams, and optionally, the URL to use if a user opts to view the tab in a browser.</span></span> <span data-ttu-id="62610-146">使用Teams选项卡，提供选项卡预期从其中加载或链接到的其他任何域。</span><span class="sxs-lookup"><span data-stu-id="62610-146">With Teams tabs, provide any additional domains from which the tab expects to load from or link to.</span></span>

##### <a name="bots"></a><span data-ttu-id="62610-147">机器人</span><span class="sxs-lookup"><span data-stu-id="62610-147">Bots</span></span>

<span data-ttu-id="62610-148">通过此部分，可以将一 [对话自动](~/bots/what-are-bots.md) 添加到应用中。</span><span class="sxs-lookup"><span data-stu-id="62610-148">This section allows you to add a [conversational bot](~/bots/what-are-bots.md) to your app.</span></span> <span data-ttu-id="62610-149">如果你已有注册了 Bot Framework 的自动程序，您可以通过单击 *"设置* 并单击自动程序的名称"自动框架 ID"并定义自动程序工作的范围来添加自动程序。</span><span class="sxs-lookup"><span data-stu-id="62610-149">If you already have a bot registered with Bot Framework, you can add that bot by clicking *Set Up* and supplying the bot's name, Bot Framework ID, and defining the scopes in which the bot will work.</span></span>

<span data-ttu-id="62610-150">如果你尚未在 Bot Framework 中注册自动 **，请单击"注册** 自动程序"以创建新的自动程序。</span><span class="sxs-lookup"><span data-stu-id="62610-150">If you have not yet registered a bot with the Bot Framework, click **Register** to create a new one.</span></span> <span data-ttu-id="62610-151">完成注册自动程序后，请返回清单编辑器的此部分，输入其名称和 Bot Framework ID。</span><span class="sxs-lookup"><span data-stu-id="62610-151">Once you’re done registering your bot, come back to this section of the Manifest Editor to enter its name and Bot Framework ID.</span></span>

<span data-ttu-id="62610-152">提供自动程序信息后，你现在可以选择定义自动程序可以建议给用户的命令列表。</span><span class="sxs-lookup"><span data-stu-id="62610-152">After you have supplied your bot's information, you can now optionally define a list of commands that your bot can suggest to users.</span></span> <span data-ttu-id="62610-153">添加命令的名称、指示其语法和参数的命令说明以及此命令应应用于的范围。</span><span class="sxs-lookup"><span data-stu-id="62610-153">Add the name of the command, a description of the command which indicates its syntax and arguments, and the scope(s) to which this command should apply.</span></span>

> [!NOTE]
> <span data-ttu-id="62610-154">如果已定义自动程序仅支持一个作用域，则忽略为不受支持的范围指定的命令。</span><span class="sxs-lookup"><span data-stu-id="62610-154">If you have defined your bot to only support one scope, the commands specified for the unsupported scope is ignored.</span></span> <span data-ttu-id="62610-155">你随时都可以编辑你的自动程序支持的范围。</span><span class="sxs-lookup"><span data-stu-id="62610-155">You can edit the scopes your bot supports at any time.</span></span>

##### <a name="connectors"></a><span data-ttu-id="62610-156">连接器</span><span class="sxs-lookup"><span data-stu-id="62610-156">Connectors</span></span>

<span data-ttu-id="62610-157">此部分允许向应用添加连接器。</span><span class="sxs-lookup"><span data-stu-id="62610-157">This section allows you to add a connector to your app.</span></span> <span data-ttu-id="62610-158">如果已注册 Office 365 连接器，请选择" **设置** 并输入连接器的名称和 ID。</span><span class="sxs-lookup"><span data-stu-id="62610-158">If you already have registered an Office 365 connector, choose **Set up** and enter the name and ID of the connector.</span></span> <span data-ttu-id="62610-159">如果需要新的连接器，请单击 **注册** 以在浏览器中访问连接器开发人员仪表板。</span><span class="sxs-lookup"><span data-stu-id="62610-159">If you want a new connector click **Register** to be taken to the Connector Developer Dashboard in your browser.</span></span>

> [!NOTE]
> <span data-ttu-id="62610-160">通过应用自定义，管理员可以更改通过机器人、消息传递扩展、选项卡和连接器加载的应用的外观。</span><span class="sxs-lookup"><span data-stu-id="62610-160">App customization enables admins to change the look-and-feel of the apps loaded through bots, messaging extensions, tabs, and connectors.</span></span> <span data-ttu-id="62610-161">例如，如果Teams将 **Contoso** 中的应用程序的名称自定义为 **Contoso 代理**，则应用将显示为用户的新名称 **Contoso Agent。**</span><span class="sxs-lookup"><span data-stu-id="62610-161">For example, if the Teams admin customizes the name of an app from **Contoso** to **Contoso Agent**, then the app will appear with the new name **Contoso Agent** to users.</span></span> <span data-ttu-id="62610-162">但是，向聊天添加连接器时，连接器仍将在列表中显示应用的名称为 **Contoso**。</span><span class="sxs-lookup"><span data-stu-id="62610-162">However, while adding a connector to a chat, in the list the connectors will still show the name of the app as **Contoso**.</span></span>


##### <a name="messaging-extensions"></a><span data-ttu-id="62610-163">消息扩展</span><span class="sxs-lookup"><span data-stu-id="62610-163">Messaging Extensions</span></span>

<span data-ttu-id="62610-164">[消息传递扩展](~/messaging-extensions/what-are-messaging-extensions.md) 是一种强大的方法，让用户在 Microsoft Teams 中参与你的应用。</span><span class="sxs-lookup"><span data-stu-id="62610-164">[Messaging extensions](~/messaging-extensions/what-are-messaging-extensions.md) are a powerful way for users to engage with your app within Microsoft Teams.</span></span> <span data-ttu-id="62610-165">用户可以查询服务的信息，将该信息以卡片形式发布到频道或聊天对话中。</span><span class="sxs-lookup"><span data-stu-id="62610-165">Users can query for information from your service and post that information in the form of cards, right into the channel or chat conversation.</span></span>

<span data-ttu-id="62610-166">消息扩展由 Bot Framework 自动程序支持，因此它们要求配置自动程序运行。</span><span class="sxs-lookup"><span data-stu-id="62610-166">Messaging extensions are powered by Bot Framework bots, so they require a configured bot to operate.</span></span> <span data-ttu-id="62610-167">如果拥有要为消息扩展提供 Power 的自动程序的名称和 Bot Framework ID，请输入该 ID。</span><span class="sxs-lookup"><span data-stu-id="62610-167">If you have the name and Bot Framework ID of the bot you would like to power the messaging extension, enter it.</span></span> <span data-ttu-id="62610-168">否则，请单击 **注册** 创建一个，然后输入信息。</span><span class="sxs-lookup"><span data-stu-id="62610-168">Otherwise, click **Register** to create one and enter the information afterward.</span></span> <span data-ttu-id="62610-169">选择用户是否可以更新消息扩展的配置。</span><span class="sxs-lookup"><span data-stu-id="62610-169">Select whether the configuration of a messaging extension can be updated by the user.</span></span>

<span data-ttu-id="62610-170">配置基础自动程序后，定义邮件扩展可以接受的命令和参数。</span><span class="sxs-lookup"><span data-stu-id="62610-170">Once you have the underlying bot configured, define the commands and parameters which the messaging extension can accept.</span></span>

<span data-ttu-id="62610-171">每个命令都需要标题和 ID。</span><span class="sxs-lookup"><span data-stu-id="62610-171">Each command requires a title and an ID.</span></span> <span data-ttu-id="62610-172">命令可以选择性地包含用户说明。</span><span class="sxs-lookup"><span data-stu-id="62610-172">The command can optionally contain a description for the user.</span></span> <span data-ttu-id="62610-173">每个命令可支持最多五个参数，每个参数要求：</span><span class="sxs-lookup"><span data-stu-id="62610-173">Each command can support up to five parameters, each of which requires:</span></span>

* <span data-ttu-id="62610-174">显示在客户端和用户请求Teams参数的名称。</span><span class="sxs-lookup"><span data-stu-id="62610-174">The name of the parameter as it appears in the Teams client and is included in the user request.</span></span>
* <span data-ttu-id="62610-175">用户友好标题。</span><span class="sxs-lookup"><span data-stu-id="62610-175">A user-friendly title.</span></span>
* <span data-ttu-id="62610-176">可选说明。</span><span class="sxs-lookup"><span data-stu-id="62610-176">An optional description.</span></span>

> [!NOTE]
> <span data-ttu-id="62610-177">若要使用 app studio 创建消息传递扩展，请参阅 [使用 app studio 创建消息传递扩展](~/resources/create-messaging-extension-using-appstudio.md)。</span><span class="sxs-lookup"><span data-stu-id="62610-177">To create messaging extension using app studio, see [create messaging extension using app studio](~/resources/create-messaging-extension-using-appstudio.md).</span></span>

#### <a name="test-and-distribute"></a><span data-ttu-id="62610-178">测试和分发</span><span class="sxs-lookup"><span data-stu-id="62610-178">Test and Distribute</span></span>

<span data-ttu-id="62610-179">定义完应用程序后，"测试并分发"部分可导出应用定义为压缩文件，然后可将其共享并上传到 Teams 客户端进行测试。</span><span class="sxs-lookup"><span data-stu-id="62610-179">Once you have finished defining your application, the Test and Distribute section allows you export your app’s definition as a zip file which then can be shared and uploaded into the Teams client for testing.</span></span> <span data-ttu-id="62610-180">单击"导出"以 *appname.zip* 下载默认下载目录中的 zip 文件。</span><span class="sxs-lookup"><span data-stu-id="62610-180">Clicking export downloads the zip file as *appname.zip* in your default download directory.</span></span>

##### <a name="publish-your-app-to-teams"></a><span data-ttu-id="62610-181">将应用发布到 Teams</span><span class="sxs-lookup"><span data-stu-id="62610-181">Publish your app to Teams</span></span>
<span data-ttu-id="62610-182">在项目主页上，你可以将应用上载到团队、将应用提交到公司自定义应用商店供你组织的用户使用，或将应用提交到所有 Teams 用户的应用源。</span><span class="sxs-lookup"><span data-stu-id="62610-182">On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span> <span data-ttu-id="62610-183">IT 管理员将审阅这些提交。</span><span class="sxs-lookup"><span data-stu-id="62610-183">Your IT admin will review these submissions.</span></span> <span data-ttu-id="62610-184">可返回" *发布* 页面，检查提交状态，并了解应用是否已获 IT 管理员批准或拒绝。这也是提交应用更新或取消当前任何活动提交的地方。</span><span class="sxs-lookup"><span data-stu-id="62610-184">You can return to the *Publish* page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

### <a name="card-editor"></a><span data-ttu-id="62610-185">卡片编辑器</span><span class="sxs-lookup"><span data-stu-id="62610-185">Card Editor</span></span>

<span data-ttu-id="62610-186">卡片是包含短信息或相关信息的容器。</span><span class="sxs-lookup"><span data-stu-id="62610-186">A card is a container for short or related pieces of information.</span></span> <span data-ttu-id="62610-187">Microsoft Teams 支持卡片，卡片可以有多个属性和附件。</span><span class="sxs-lookup"><span data-stu-id="62610-187">Microsoft Teams supports cards, which can have multiple properties and attachments.</span></span> <span data-ttu-id="62610-188">卡片是自动程序和连接器将可操作的信息中继给用户的一种重要方式。</span><span class="sxs-lookup"><span data-stu-id="62610-188">Cards are a key way that bots and connectors relay actionable information to users.</span></span> 

<span data-ttu-id="62610-189">为了简化此过程且减少出错，可以使用"卡片编辑器"选项卡使用窗体生成主卡或缩略图卡，并验证和测试生成的卡片 (就像用户通过自动程序) 看到它一样。</span><span class="sxs-lookup"><span data-stu-id="62610-189">To make this process easier and less error-prone, the Card Editor tab lets you build Hero Cards or Thumbnail Cards using a form and verify and test the resulting card (exactly as a user would see it) through a bot.</span></span> <span data-ttu-id="62610-190">它还为卡片提供相应的 JSON 或 Node.js 代码，可将其复制/粘贴到 C# 应用的源代码中。</span><span class="sxs-lookup"><span data-stu-id="62610-190">It also provides the corresponding JSON, C#, or Node.js code for the card that you can copy/paste into your app's source code.</span></span>

<span data-ttu-id="62610-191">如果已有要验证的卡片，可在 Teams 中将该卡的 JSON 粘贴到 *"添加卡信息"下的 JSON 选项卡中* 然后将其发送给自己以查看聊天中的外观。</span><span class="sxs-lookup"><span data-stu-id="62610-191">If you already have a card that you would like to verify inside Teams, you can paste the JSON for that card into the JSON tab under *Add card info* and send it to yourself to see what it looks like in a chat.</span></span>

### <a name="react-control-library"></a><span data-ttu-id="62610-192">反应控件库</span><span class="sxs-lookup"><span data-stu-id="62610-192">React Control Library</span></span>

>[!Note]
> <span data-ttu-id="62610-193">以后React弃用此控件库。</span><span class="sxs-lookup"><span data-stu-id="62610-193">This React control library is deprecated in the future.</span></span> <span data-ttu-id="62610-194">请考虑将 [Fluent-UI react 控件用作](https://microsoft.github.io/fluent-ui-react/) 以前作为 Stardust UI 的替代项。</span><span class="sxs-lookup"><span data-stu-id="62610-194">Consider using the [Fluent-UI react controls as an alternative](https://microsoft.github.io/fluent-ui-react/) previously Stardust UI.</span></span>

<span data-ttu-id="62610-195">创建遵循 Teams 最佳做法的应用是使应用的外观与 Teams 客户端体验完美契合的一种好方法。</span><span class="sxs-lookup"><span data-stu-id="62610-195">Creating an app that follows the Teams best practices is a great way to give your app a look and feel that fits seamlessly with the Teams client experience.</span></span> <span data-ttu-id="62610-196">你使用的 UI 控件对于实现这一目标至关重要。</span><span class="sxs-lookup"><span data-stu-id="62610-196">The UI controls that you use are critical to achieving that end.</span></span> <span data-ttu-id="62610-197">为更轻松地创建一致的 UI，App Studio 提供了几种符合 Teams 设计原则的 UI 控件类别。</span><span class="sxs-lookup"><span data-stu-id="62610-197">To make it easier to create a consistent UI, App Studio provides several categories of UI controls which follow Teams design principles.</span></span>

<span data-ttu-id="62610-198">提供了控件和相应的"响应"组件的示例，可准备在构建应用时使用。</span><span class="sxs-lookup"><span data-stu-id="62610-198">Examples of the controls and corresponding React components are provided and ready to use in building your app.</span></span>

#### <a name="controls"></a><span data-ttu-id="62610-199">控件</span><span class="sxs-lookup"><span data-stu-id="62610-199">Controls</span></span>

<span data-ttu-id="62610-200">控件包括：</span><span class="sxs-lookup"><span data-stu-id="62610-200">Controls include:</span></span>

* <span data-ttu-id="62610-201">按钮</span><span class="sxs-lookup"><span data-stu-id="62610-201">Buttons</span></span>
* <span data-ttu-id="62610-202">下拉列表</span><span class="sxs-lookup"><span data-stu-id="62610-202">Dropdowns</span></span>
* <span data-ttu-id="62610-203">复选框</span><span class="sxs-lookup"><span data-stu-id="62610-203">Checkboxes</span></span>
* <span data-ttu-id="62610-204">单选按钮</span><span class="sxs-lookup"><span data-stu-id="62610-204">Radio Buttons</span></span>
* <span data-ttu-id="62610-205">切换</span><span class="sxs-lookup"><span data-stu-id="62610-205">Toggles</span></span>
* <span data-ttu-id="62610-206">文本区域</span><span class="sxs-lookup"><span data-stu-id="62610-206">Text Areas</span></span>
* <span data-ttu-id="62610-207">链接</span><span class="sxs-lookup"><span data-stu-id="62610-207">Links</span></span>
* <span data-ttu-id="62610-208">选项卡</span><span class="sxs-lookup"><span data-stu-id="62610-208">Tabs</span></span>
* <span data-ttu-id="62610-209">表格</span><span class="sxs-lookup"><span data-stu-id="62610-209">Tables</span></span>
* <span data-ttu-id="62610-210">图标</span><span class="sxs-lookup"><span data-stu-id="62610-210">Icons</span></span>
