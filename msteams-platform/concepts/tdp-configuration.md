---
title: 开发人员门户中的应用配置
description: 了解如何使用开发人员门户为用户配置和管理Microsoft Teams
keywords: 开发人员门户团队入门
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: ce290bd7daa46467be279aae7c608321e75e2d57
ms.sourcegitcommit: d972953994e405c6afc42e4d4a76b48c6d4cfb5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52635085"
---
# <a name="app-configuration"></a><span data-ttu-id="0acf5-104">应用配置</span><span class="sxs-lookup"><span data-stu-id="0acf5-104">App configuration</span></span>

<span data-ttu-id="0acf5-105">应用包最重要的部分Microsoft Teams文件上的manifest.js部分。</span><span class="sxs-lookup"><span data-stu-id="0acf5-105">The most significant part of a Microsoft Teams app package is its manifest.json file.</span></span> <span data-ttu-id="0acf5-106">此文件必须符合应用Teams[架构](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="0acf5-106">This file must conform to the [Teams App schema](~/resources/schema/manifest-schema.md).</span></span> <span data-ttu-id="0acf5-107">on manifest.js文件包含元数据，Teams向用户正确呈现你的应用。</span><span class="sxs-lookup"><span data-stu-id="0acf5-107">The manifest.json file contains metadata, which allows Teams to correctly present your app to users.</span></span>

<span data-ttu-id="0acf5-108">您可以在开发人员门户的"配置 **"** 部分执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="0acf5-108">You can perform the following actions in the **Configure** section of the Developer Portal:</span></span>

* <span data-ttu-id="0acf5-109">轻松创建应用包。</span><span class="sxs-lookup"><span data-stu-id="0acf5-109">Create an app package easily.</span></span>
* <span data-ttu-id="0acf5-110">描述应用。</span><span class="sxs-lookup"><span data-stu-id="0acf5-110">Describe the app.</span></span>
* <span data-ttu-id="0acf5-111">Upload图标。</span><span class="sxs-lookup"><span data-stu-id="0acf5-111">Upload your icons.</span></span>
* <span data-ttu-id="0acf5-112">生成.zip文件以轻松分发。</span><span class="sxs-lookup"><span data-stu-id="0acf5-112">Produce a .zip file for easy distribution.</span></span>

> [!NOTE]
> <span data-ttu-id="0acf5-113">开发人员门户不会为你的应用生成功能代码，也不托管你的应用。</span><span class="sxs-lookup"><span data-stu-id="0acf5-113">Developer Portal does not produce functional code for your app, or host your app.</span></span> <span data-ttu-id="0acf5-114">应用必须已在应用上传流程的清单中列出的 URL 上托管并运行，以产生工作应用。</span><span class="sxs-lookup"><span data-stu-id="0acf5-114">Your app must already be hosted and running at the URL listed in the manifest for the app upload process to result in a working app.</span></span>

:::image type="content" source="~/assets/images/tdp/tdp_configure_1.png" alt-text="Screenshot showing the Configure page of Teams Developer Portal.":::

## <a name="basic-information-and-branding"></a><span data-ttu-id="0acf5-116">基本信息和品牌</span><span class="sxs-lookup"><span data-stu-id="0acf5-116">Basic information and Branding</span></span>

<span data-ttu-id="0acf5-117">基本 **信息和\*\*\*\*品牌** 打造部分定义了你正在制作的应用的简要说明。</span><span class="sxs-lookup"><span data-stu-id="0acf5-117">The **Basic information** and **Branding** sections define the high-level description of the app you are making.</span></span> <span data-ttu-id="0acf5-118">这包括应用的名称、说明和视觉品牌。</span><span class="sxs-lookup"><span data-stu-id="0acf5-118">This includes the app’s name, description, and visual branding.</span></span> <span data-ttu-id="0acf5-119">此部分中的信息将用于应用的应用商店Teams应用安装对话中。</span><span class="sxs-lookup"><span data-stu-id="0acf5-119">The information in this section will be used in your app's Teams store listing and app installation dialogue.</span></span>

## <a name="capabilities"></a><span data-ttu-id="0acf5-120">功能</span><span class="sxs-lookup"><span data-stu-id="0acf5-120">Capabilities</span></span>

<span data-ttu-id="0acf5-121">配置的 **"** 功能"部分列出了应用的功能详细信息。</span><span class="sxs-lookup"><span data-stu-id="0acf5-121">The **Capabilities** section of Configuration has the app's capabilities details listed.</span></span>

> [!NOTE]
> <span data-ttu-id="0acf5-122">应用自定义功能目前仅在开发人员预览版中可用。</span><span class="sxs-lookup"><span data-stu-id="0acf5-122">The app customization feature is currently available in the developer preview only.</span></span>
> 
> <span data-ttu-id="0acf5-123">最佳做法是，你必须提供自定义指南，以便应用用户和客户在自定义应用时遵循这些准则。</span><span class="sxs-lookup"><span data-stu-id="0acf5-123">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> <span data-ttu-id="0acf5-124">有关详细信息，请参阅自定义[应用程序中Microsoft Teams。](/MicrosoftTeams/customize-apps)</span><span class="sxs-lookup"><span data-stu-id="0acf5-124">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

<span data-ttu-id="0acf5-125">以下是功能：</span><span class="sxs-lookup"><span data-stu-id="0acf5-125">Following are the capabilities:</span></span>

:::image type="content" source="~/assets/images/tdp/tdp_capabilities.png" alt-text="Screenshot showing the Configure page of Teams Developer Portal.":::

* <span data-ttu-id="0acf5-127">**个人应用**</span><span class="sxs-lookup"><span data-stu-id="0acf5-127">**Personal app**</span></span> 

  <span data-ttu-id="0acf5-128">本部分允许你定义在个人应用体验中默认呈现的一组选项卡，即用户在团队或频道上下文之外使用你的应用的体验。</span><span class="sxs-lookup"><span data-stu-id="0acf5-128">This section lets you define a set of tabs that are presented by default in the personal app experience, that is, the experience a user has with your app outside the context of a team or channel.</span></span> <span data-ttu-id="0acf5-129">在此部分中，提供以下详细信息：</span><span class="sxs-lookup"><span data-stu-id="0acf5-129">In this section, provide the following details:</span></span>

  * <span data-ttu-id="0acf5-130">选项卡名称。</span><span class="sxs-lookup"><span data-stu-id="0acf5-130">The tab name.</span></span>
  * <span data-ttu-id="0acf5-131">唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="0acf5-131">A unique identifier.</span></span>
  * <span data-ttu-id="0acf5-132">指向要显示在 Teams 中的 UI 的 URL。</span><span class="sxs-lookup"><span data-stu-id="0acf5-132">The URL that points to the UI to be displayed in Teams.</span></span>
  * <span data-ttu-id="0acf5-133">用户选择在浏览器中查看选项卡时使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="0acf5-133">The URL to use if a user opts to view the tab in a browser.</span></span> <span data-ttu-id="0acf5-134">这是可选信息。</span><span class="sxs-lookup"><span data-stu-id="0acf5-134">This is an optional information.</span></span>
  * <span data-ttu-id="0acf5-135">选项卡预期从其中加载或链接到的其他任何域。</span><span class="sxs-lookup"><span data-stu-id="0acf5-135">Any additional domains from which the tab expects to load from or link to.</span></span>

* <span data-ttu-id="0acf5-136">**组和频道应用**</span><span class="sxs-lookup"><span data-stu-id="0acf5-136">**Group and channel app**</span></span>

  <span data-ttu-id="0acf5-137">"Teams选项卡将成为频道的一部分，并快速访问团队信息和资源。</span><span class="sxs-lookup"><span data-stu-id="0acf5-137">A Teams tab becomes part of a channel and provides quick access to team information and resources.</span></span> <span data-ttu-id="0acf5-138">例如，频道的"规划器"选项卡包含单个计划，Power BI选项卡映射到特定报表。</span><span class="sxs-lookup"><span data-stu-id="0acf5-138">For example, the Planner tab for a channel contains a single plan, the Power BI tab maps to a specific report.</span></span> <span data-ttu-id="0acf5-139">用户可以向下钻取相关上下文，但无法导航到选项卡外部。例如，Power BI 选项卡不会启用到其他 Power BI 报表的导航，但它允许" **转到网站** "按钮，该按钮在 Power BI 主网站中启动报表。</span><span class="sxs-lookup"><span data-stu-id="0acf5-139">Users can drill down to the relevant context, but they should not be able to navigate outside the tab. The Power BI tab, for instance, doesn't enable navigation to other Power BI reports, but it does enable the **Go to website** button that launches the report in the main Power BI website.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0acf5-140">对于团队选项卡，必须提供配置 URL 来显示选项和收集信息，这将帮助您自定义选项卡的内容和体验。当用户首次将选项卡添加到频道时，将显示此 iframed HTML 页面。</span><span class="sxs-lookup"><span data-stu-id="0acf5-140">For team tabs, you must provide a Configuration URL to present options and gather information, that would help you to customize the content and experience of your tab. This iframed HTML page is displayed when a user first adds the tab to a channel.</span></span>
    > <span data-ttu-id="0acf5-141">你还必须提供选项卡期望从其加载或链接到的任何其他域。</span><span class="sxs-lookup"><span data-stu-id="0acf5-141">You must also provide any additional domains that the tab expects to load from or link to.</span></span>

* <span data-ttu-id="0acf5-142">**机器人**</span><span class="sxs-lookup"><span data-stu-id="0acf5-142">**Bot**</span></span>

  <span data-ttu-id="0acf5-143">通过此部分，可以将一 [对话自动](~/bots/what-are-bots.md) 添加到应用中。</span><span class="sxs-lookup"><span data-stu-id="0acf5-143">This section allows you to add a [conversational bot](~/bots/what-are-bots.md) to your app.</span></span> <span data-ttu-id="0acf5-144">如果你已有注册了 Bot Framework 的自动程序，您可以通过单击 **"设置** 并单击自动程序的名称"自动框架 ID"并定义自动程序工作的范围来添加自动程序。</span><span class="sxs-lookup"><span data-stu-id="0acf5-144">If you already have a bot registered with Bot Framework, you can add that bot by clicking **Set Up** and supplying the bot's name, Bot Framework ID, and defining the scopes in which the bot will work.</span></span>

  <span data-ttu-id="0acf5-145">如果尚未向 Bot Framework 注册自动程序，请单击" **注册"** 以创建新的聊天机器人。</span><span class="sxs-lookup"><span data-stu-id="0acf5-145">If you have not registered the bot with the Bot Framework yet, click **Register** to create a new one.</span></span> <span data-ttu-id="0acf5-146">注册自动程序后，返回到清单编辑器的此部分以输入其名称和自动程序框架 ID。</span><span class="sxs-lookup"><span data-stu-id="0acf5-146">After you have registered your bot, come back to this section of the Manifest Editor to enter its name and Bot Framework ID.</span></span>

  <span data-ttu-id="0acf5-147">提供自动程序信息后，你现在可以选择定义自动程序可以建议给用户的命令列表。</span><span class="sxs-lookup"><span data-stu-id="0acf5-147">After you have supplied your bot's information, you can now optionally define a list of commands that your bot can suggest to users.</span></span> <span data-ttu-id="0acf5-148">添加命令的名称、指示其语法和参数的命令说明以及此命令应应用于的范围。</span><span class="sxs-lookup"><span data-stu-id="0acf5-148">Add the name of the command, a description of the command which indicates its syntax and arguments, and the scope(s) to which this command should apply.</span></span>

  <span data-ttu-id="0acf5-149">请注意，如果将自动程序定义为仅支持一个作用域，则为不受支持的范围指定的命令将被忽略。</span><span class="sxs-lookup"><span data-stu-id="0acf5-149">Note that if you have defined your bot to only support one scope, commands specified for the unsupported scope will be ignored.</span></span> <span data-ttu-id="0acf5-150">你随时都可以编辑你的自动程序支持的范围。</span><span class="sxs-lookup"><span data-stu-id="0acf5-150">You can edit the scopes your bot supports at any time.</span></span>

* <span data-ttu-id="0acf5-151">**Connector**</span><span class="sxs-lookup"><span data-stu-id="0acf5-151">**Connector**</span></span>

  <span data-ttu-id="0acf5-152">此部分允许向应用添加连接器。</span><span class="sxs-lookup"><span data-stu-id="0acf5-152">This section allows you to add a connector to your app.</span></span> <span data-ttu-id="0acf5-153">如果已注册连接器Office 365，**请选择"设置**"，然后输入连接器的名称和 ID。</span><span class="sxs-lookup"><span data-stu-id="0acf5-153">If you already have registered an Office 365 connector, select **Set up** and enter the name and ID of the connector.</span></span> <span data-ttu-id="0acf5-154">如果需要新的连接器，请单击 **注册** 以在浏览器中访问连接器开发人员仪表板。</span><span class="sxs-lookup"><span data-stu-id="0acf5-154">If you want a new connector click **Register** to be taken to the Connector Developer Dashboard in your browser.</span></span>

  > [!NOTE]
  > <span data-ttu-id="0acf5-155">通过应用自定义，管理员可以更改通过机器人、消息传递扩展、选项卡和连接器加载的应用的外观。</span><span class="sxs-lookup"><span data-stu-id="0acf5-155">App customization enables admins to change the look-and-feel of the apps loaded through bots, messaging extensions, tabs, and connectors.</span></span> <span data-ttu-id="0acf5-156">例如，如果Teams将应用的名称自定义为 ，则应用将显示为用户的新 `Contoso` `Contoso Agent` `Contoso Agent` 名称。</span><span class="sxs-lookup"><span data-stu-id="0acf5-156">For example, if the Teams admin customizes the name of an app from `Contoso` to `Contoso Agent`, then the app will appear with the new name `Contoso Agent` to the users.</span></span> <span data-ttu-id="0acf5-157">但是，在列表中向聊天添加连接器时，连接器仍将应用名称显示为 `Contoso` 。</span><span class="sxs-lookup"><span data-stu-id="0acf5-157">However, while adding a connector to a chat, in the list, the connectors will still show the name of the app as `Contoso`.</span></span>

* <span data-ttu-id="0acf5-158">**消息扩展**</span><span class="sxs-lookup"><span data-stu-id="0acf5-158">**Messaging Extensions**</span></span>

  <span data-ttu-id="0acf5-159">[消息传递扩展](~/messaging-extensions/what-are-messaging-extensions.md) 是一种强大的方法，让用户在 Microsoft Teams 中参与你的应用。</span><span class="sxs-lookup"><span data-stu-id="0acf5-159">[Messaging extensions](~/messaging-extensions/what-are-messaging-extensions.md) are a powerful way for users to engage with your app within Microsoft Teams.</span></span> <span data-ttu-id="0acf5-160">用户可以查询服务的信息，将该信息以卡片形式发布到频道或聊天对话中。</span><span class="sxs-lookup"><span data-stu-id="0acf5-160">Users can query for information from your service and post that information in the form of cards, right into the channel or chat conversation.</span></span>

  <span data-ttu-id="0acf5-161">消息扩展由 Bot Framework 自动程序支持，因此它们要求配置自动程序运行。</span><span class="sxs-lookup"><span data-stu-id="0acf5-161">Messaging extensions are powered by Bot Framework bots, so they require a configured bot to operate.</span></span> <span data-ttu-id="0acf5-162">如果拥有要为消息扩展提供 Power 的自动程序的名称和 Bot Framework ID，请输入该 ID。</span><span class="sxs-lookup"><span data-stu-id="0acf5-162">If you have the name and Bot Framework ID of the bot you would like to power the messaging extension, enter it.</span></span> <span data-ttu-id="0acf5-163">否则，请单击 *注册* 创建一个，然后输入信息。</span><span class="sxs-lookup"><span data-stu-id="0acf5-163">Otherwise, click *Register* to create one and enter the information afterward.</span></span> <span data-ttu-id="0acf5-164">选择用户是否可以更新消息扩展的配置。</span><span class="sxs-lookup"><span data-stu-id="0acf5-164">Select whether the configuration of a messaging extension can be updated by the user.</span></span>

  <span data-ttu-id="0acf5-165">配置基础自动程序后，定义邮件扩展可以接受的命令和参数。</span><span class="sxs-lookup"><span data-stu-id="0acf5-165">After you have the underlying bot configured, define the commands and parameters which the messaging extension can accept.</span></span>

  <span data-ttu-id="0acf5-166">每个命令都需要标题和 ID。</span><span class="sxs-lookup"><span data-stu-id="0acf5-166">Each command requires a title and an ID.</span></span> <span data-ttu-id="0acf5-167">命令可以选择性地包含用户说明。</span><span class="sxs-lookup"><span data-stu-id="0acf5-167">The command can optionally contain a description for the user.</span></span> <span data-ttu-id="0acf5-168">每个命令最多支持五个参数，每个参数都需要：</span><span class="sxs-lookup"><span data-stu-id="0acf5-168">Each command can support up to five parameters, each of which requires the following:</span></span>

  * <span data-ttu-id="0acf5-169">显示在客户端和用户请求Teams参数的名称。</span><span class="sxs-lookup"><span data-stu-id="0acf5-169">The name of the parameter as it appears in the Teams client and is included in the user request.</span></span>
  * <span data-ttu-id="0acf5-170">用户友好标题。</span><span class="sxs-lookup"><span data-stu-id="0acf5-170">A user-friendly title.</span></span>
  * <span data-ttu-id="0acf5-171">可选说明。</span><span class="sxs-lookup"><span data-stu-id="0acf5-171">An optional description.</span></span>

  > [!NOTE]
  > <span data-ttu-id="0acf5-172">若要使用 app studio 创建消息传递扩展，请参阅 [使用 app studio 创建消息传递扩展](~/resources/create-messaging-extension-using-appstudio.md)。</span><span class="sxs-lookup"><span data-stu-id="0acf5-172">To create messaging extension using app studio, see [create messaging extension using app studio](~/resources/create-messaging-extension-using-appstudio.md).</span></span>

* <span data-ttu-id="0acf5-173">**会议扩展名**</span><span class="sxs-lookup"><span data-stu-id="0acf5-173">**Meeting extension**</span></span>

  <span data-ttu-id="0acf5-174">TODO：Rajesh R.</span><span class="sxs-lookup"><span data-stu-id="0acf5-174">//TODO: Rajesh R.</span></span>

* <span data-ttu-id="0acf5-175">**场景**</span><span class="sxs-lookup"><span data-stu-id="0acf5-175">**Scene**</span></span>

  <span data-ttu-id="0acf5-176">在一起模式下的场景是场景开发人员使用 Microsoft Scene Studio 创建的一个项目，它以场景创建者所构想的创意设置将人们与视频流一起汇集在一起。</span><span class="sxs-lookup"><span data-stu-id="0acf5-176">Scenes in Together Mode is an artifact created by the scene developer using the Microsoft Scene studio that brings people together along with their video stream in a creative setting as conceived by the scene creator.</span></span> <span data-ttu-id="0acf5-177">在构想的场景设置中，参与者具有指定席位，视频流呈现在这些座位中。</span><span class="sxs-lookup"><span data-stu-id="0acf5-177">In a conceived scene setting, participants have designated seats with video streams rendered in those seats.</span></span> <span data-ttu-id="0acf5-178">有关详细信息，请参阅Teams[模式](~/apps-in-teams-meetings/teams-together-mode.md)。</span><span class="sxs-lookup"><span data-stu-id="0acf5-178">For more information, see [Teams Together Mode](~/apps-in-teams-meetings/teams-together-mode.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="0acf5-179">Permissions</span><span class="sxs-lookup"><span data-stu-id="0acf5-179">Permissions</span></span>

<span data-ttu-id="0acf5-180">可以使用本机设备Teams（如相机、麦克风和位置）丰富你的应用。</span><span class="sxs-lookup"><span data-stu-id="0acf5-180">You can enrich your Teams app with native device capabilities, such as camera, microphone, and location.</span></span>

## <a name="languages"></a><span data-ttu-id="0acf5-181">语言</span><span class="sxs-lookup"><span data-stu-id="0acf5-181">Languages</span></span>

<span data-ttu-id="0acf5-182">设置或更改应用支持的语言。</span><span class="sxs-lookup"><span data-stu-id="0acf5-182">Set up or change the languages that your app supports.</span></span>

## <a name="single-sign-on"></a><span data-ttu-id="0acf5-183">单一登录</span><span class="sxs-lookup"><span data-stu-id="0acf5-183">Single Sign-On</span></span>

<span data-ttu-id="0acf5-184">将应用配置为使用 SSO (单一登录) 。</span><span class="sxs-lookup"><span data-stu-id="0acf5-184">Configure your app to authenticate users with single sign-on (SSO).</span></span>

## <a name="domains"></a><span data-ttu-id="0acf5-185">域</span><span class="sxs-lookup"><span data-stu-id="0acf5-185">Domains</span></span>

<span data-ttu-id="0acf5-186">应用预期在客户端内加载的网站的有效Teams列表。</span><span class="sxs-lookup"><span data-stu-id="0acf5-186">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="0acf5-187">域列表可以包含通配符，例如 `*.example.com` ， 。</span><span class="sxs-lookup"><span data-stu-id="0acf5-187">Domain listings can include wildcards, for example, `*.example.com`.</span></span> <span data-ttu-id="0acf5-188">这完全匹配域的一个段;如果需要匹配，请使用 `a.b.example.com` `*.*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="0acf5-188">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="0acf5-189">如果你的选项卡配置或内容 UI 需要导航到除用于选项卡配置的其他任何其他域，则必须在此处指定该域。</span><span class="sxs-lookup"><span data-stu-id="0acf5-189">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="0acf5-190">不需要在应用中包含要支持的标识提供程序的域。</span><span class="sxs-lookup"><span data-stu-id="0acf5-190">It is not necessary to include the domains of the identity providers you want to support in your app.</span></span> <span data-ttu-id="0acf5-191">例如，若要使用 Google ID 进行身份验证，必须重定向到 accounts.google.com，但不得在 `validDomains[]` accounts.google.com。</span><span class="sxs-lookup"><span data-stu-id="0acf5-191">For example, to authenticate using a Google ID, it is required to redirect to accounts.google.com, however, you must not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="0acf5-192">Teams需要自己的 sharepoint URL 正常运行的应用程序，请包括其有效域列表中的"{teamsitedomain}"。</span><span class="sxs-lookup"><span data-stu-id="0acf5-192">Teams apps that require their own sharepoint URLs to function well, includes "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0acf5-193">不要直接添加或通过通配符添加超出您控制的域。</span><span class="sxs-lookup"><span data-stu-id="0acf5-193">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="0acf5-194">例如， `yourapp.onmicrosoft.com` 是有效的，但 `*.onmicrosoft.com` 是 无效。</span><span class="sxs-lookup"><span data-stu-id="0acf5-194">For example, `yourapp.onmicrosoft.com` is valid, however, `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="0acf5-195">对象是包含类型 的所有元素的数组 `string` 。</span><span class="sxs-lookup"><span data-stu-id="0acf5-195">The object is an array with all elements of the type `string`.</span></span>

## <a name="advanced"></a><span data-ttu-id="0acf5-196">高级</span><span class="sxs-lookup"><span data-stu-id="0acf5-196">Advanced</span></span>
<span data-ttu-id="0acf5-197">Todo by Karthig</span><span class="sxs-lookup"><span data-stu-id="0acf5-197">//Todo by Karthig</span></span>

### <a name="app-content"></a><span data-ttu-id="0acf5-198">应用内容</span><span class="sxs-lookup"><span data-stu-id="0acf5-198">App content</span></span>
<span data-ttu-id="0acf5-199">Todo by Karthig</span><span class="sxs-lookup"><span data-stu-id="0acf5-199">//Todo by Karthig</span></span>

### <a name="first-party-settings"></a><span data-ttu-id="0acf5-200">第一方设置</span><span class="sxs-lookup"><span data-stu-id="0acf5-200">First party settings</span></span>
<span data-ttu-id="0acf5-201">Todo by Karthig</span><span class="sxs-lookup"><span data-stu-id="0acf5-201">//Todo by Karthig</span></span>

## <a name="see-also"></a><span data-ttu-id="0acf5-202">另请参阅</span><span class="sxs-lookup"><span data-stu-id="0acf5-202">See also</span></span>

* [<span data-ttu-id="0acf5-203">开发人员Teams概述</span><span class="sxs-lookup"><span data-stu-id="0acf5-203">Overview of Teams Developer Portal</span></span>](~/concepts/build-and-test/teams-developer-portal.md)
* [<span data-ttu-id="0acf5-204">分发Teams开发人员门户</span><span class="sxs-lookup"><span data-stu-id="0acf5-204">Distribute Teams Developer Portal</span></span>](~/concepts/tdp-distribute.md)
* [<span data-ttu-id="0acf5-205">开发人员门户Teams中的工具</span><span class="sxs-lookup"><span data-stu-id="0acf5-205">Tools in Teams Developer Portal</span></span>](~/concepts/tdp-tools.md)