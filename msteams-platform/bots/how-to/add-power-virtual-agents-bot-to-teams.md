---
title: 向团队添加 Power Virtual 代理 chatbot
author: laujan
description: 在团队平台中集成电源虚拟代理 chatbot
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 125a114cb4775dfe2c9265afefae0257f57282df
ms.sourcegitcommit: 560bf433129c16888135879e2703dbdeb38ec99f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "48397685"
---
# <a name="integrate-a-power-virtual-agents-chatbot-with-microsoft-teams"></a><span data-ttu-id="5c9f2-103">将电源虚拟代理与 Microsoft 团队集成 chatbot</span><span class="sxs-lookup"><span data-stu-id="5c9f2-103">Integrate a Power Virtual Agents chatbot with Microsoft Teams</span></span>

<span data-ttu-id="5c9f2-104">[Power Virtual agent](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) 是一个无代码的、导向的图形界面解决方案，它使团队中的每个成员都能创建丰富的会话 chatbots，以便轻松地与团队平台集成。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-104">[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) is a no-code, guided graphical interface solution that empowers every member of your team to create rich, conversational chatbots that easily integrate with the Teams platform.</span></span> <span data-ttu-id="5c9f2-105">在 Power Virtual Agent 中创作的所有内容都在团队中呈现为自然，电源虚拟代理程序 bot 与团队本机聊天画布中的用户接洽。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-105">All content authored in Power Virtual Agents renders naturally in Teams and Power Virtual Agents bots engage with users in the Teams native chat canvas.</span></span> <span data-ttu-id="5c9f2-106">您的 IT 管理员、业务分析师、域专家和训练有素的应用程序开发人员可以设计、开发和发布用于团队的智能虚拟代理，而无需设置开发环境、创建 web 服务或直接在 Bot 框架中注册。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-106">Your IT administrators, business analysts, domain specialists, and skilled app developers can design, develop and publish intelligent virtual agents for Teams without having to setup a development environment, create a web service, or directly register with the Bot Framework.</span></span>  <span data-ttu-id="5c9f2-107">*请参阅*[为使用 Microsoft Power Virtual 代理的团队创建 chatbot](../what-are-bots.md#create-a-chatbot-for-teams-with-microsoft-power-virtual-agents)。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-107">*See* [Create a chatbot for Teams with Microsoft Power Virtual Agents](../what-are-bots.md#create-a-chatbot-for-teams-with-microsoft-power-virtual-agents).</span></span>

> [!NOTE]
> <span data-ttu-id="5c9f2-108">通过将您的 chatbot 添加到 Microsoft 团队，将会与 Microsoft (团队共享一些数据（例如，bot 内容和最终用户聊天内容），这意味着您的数据将在您的 [组织的合规性和地理或区域边界](/power-virtual-agents/data-location)) 之外流动。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-108">By adding your chatbot to Microsoft Teams, some of data, such as bot content and end-user chat content, will be shared with Microsoft Teams (meaning that your data will flow outside of your [organization’s compliance and geographic or regional boundaries](/power-virtual-agents/data-location)).</span></span> <br/>
> <span data-ttu-id="5c9f2-109">有关详细信息，请参阅 [Microsoft 团队中的安全性和合规性](/MicrosoftTeams/security-compliance-overview)。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-109">For more information, see the [Security and compliance in Microsoft Teams](/MicrosoftTeams/security-compliance-overview).</span></span>

## <a name="make-your-chatbot-reachable-in-teams-in-the-power-virtual-agents-portal"></a><span data-ttu-id="5c9f2-110">使你的 chatbot 可在 Power Virtual Agent 门户中的团队中访问</span><span class="sxs-lookup"><span data-stu-id="5c9f2-110">Make your chatbot reachable in Teams in the Power Virtual Agents portal</span></span>

1. <span data-ttu-id="5c9f2-111">**发布最新的 bot 内容**。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-111">**Publish the latest bot content**.</span></span>  <span data-ttu-id="5c9f2-112">在 [Power Virtual agent 门户](https://powervirtualagents.microsoft.com)中创建 chatbot 后，您至少需要在工作组用户可以与其进行交互之前发布你的机器人。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-112">After you have created a chatbot in the [Power Virtual Agents portal](https://powervirtualagents.microsoft.com), you need to publish your bot at least once before Teams users can interact with it.</span></span> <span data-ttu-id="5c9f2-113">请参阅 [发布最新的 bot 内容](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content)。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-113">See [Publish the latest bot content](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content).</span></span>

![在 power virtual agent 门户中发布](../../assets/images/pva-publish.png)

2. <span data-ttu-id="5c9f2-115">**配置团队频道**。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-115">**Configure the Teams channel**.</span></span> <span data-ttu-id="5c9f2-116">在发布你的 bot 后，你可以添加团队频道以使机器人可与团队用户访问。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-116">After publishing your bot, you can add the Teams channel to make the bot reachable to Teams users.</span></span>

![power virtual agent portal 中的频道](../../assets/images/pva-channels.png)

3. <span data-ttu-id="5c9f2-118">**为您的 Chatbot 生成应用程序 Id**  成功将团队频道添加到 chatbot 后，会在对话框中生成 **应用 Id** 。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-118">**Generate an App Id for your chatbot**  When the Teams channel has been successfully added to your chatbot, an **App Id** will be generated in the dialog box.</span></span> <span data-ttu-id="5c9f2-119">应用程序 Id 是你的 bot 的唯一 Microsoft 生成标识符。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-119">The App Id is a unique Microsoft generated identifier for your bot.</span></span>  <span data-ttu-id="5c9f2-120">复制并保存应用程序 Id —稍后将需要它来为团队创建应用程序包。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-120">Copy and save the App Id — you will need it later to create an app package for Teams.</span></span>

## <a name="add-your-bot-to-teams-using-app-studio"></a><span data-ttu-id="5c9f2-121">使用应用程序 Studio 向团队添加你的机器人</span><span class="sxs-lookup"><span data-stu-id="5c9f2-121">Add your bot to Teams using App Studio</span></span>

<span data-ttu-id="5c9f2-122">如果在团队实例中启用了 " [上载自定义应用程序](/microsoftteams/admin-settings) "，则可以使用团队应用程序 Studio 直接上传您的 chatbot，并立即开始使用它。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-122">If [uploading custom apps is enabled](/microsoftteams/admin-settings) in your Teams instance, you can use Teams App Studio to directly upload your chatbot and start using it right away.</span></span> <span data-ttu-id="5c9f2-123">如果要共享你的 chatbot，可以请求管理员让你的你的 bot 在租户应用程序目录中可用，或者可以向其他人发送应用程序包，并请求其独立上载。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-123">If you want to share your chatbot, you can request that your admin make your bot available in the tenant app catalog or you can send others your app package and ask them to upload it independently.</span></span>

1. <span data-ttu-id="5c9f2-124">**在团队中安装应用程序 Studio**。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-124">**Install App Studio in Teams**.</span></span> <span data-ttu-id="5c9f2-125">应用程序 Studio 是一个团队应用程序，您可以从团队存储中进行安装，从而简化团队中机器人的创建和注册：</span><span class="sxs-lookup"><span data-stu-id="5c9f2-125">App Studio is a Teams app you can install from the Teams store that simplifies the creation and registration of your bot in Teams:</span></span> 

  * <span data-ttu-id="5c9f2-126">从 "团队" 实例的左侧导航栏底部选择 "应用商店" 图标，然后搜索 **应用程序 Studio**。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-126">Select the app store icon from the bottom of the left nav bar in your Teams instance, and search for **App Studio**.</span></span>
>

&emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="/msteams-docs/msteams-platform/assets/images/get-started/app-studio-store.png"/>   

  * <span data-ttu-id="5c9f2-127">选择 " **应用程序制作室** " 磁贴，然后在弹出对话框中选择 " **安装** "。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-127">Select the **App Studio** tile and choose **Install** in the pop-up dialog box.</span></span>
>
&emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

2. <span data-ttu-id="5c9f2-128">**在应用程序 Studio 中创建团队应用程序清单**。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-128">**Create the Teams app manifest in App Studio**.</span></span>  <span data-ttu-id="5c9f2-129">团队中的 bot 由应用部件清单（ (JSON) 文件）定义，该文件提供有关你的 bot 及其功能的基本信息。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-129">Bots in Teams are defined by an app manifest (JSON) file that provides basic information about your bot and its capabilities.</span></span> <span data-ttu-id="5c9f2-130">在**应用程序 Studio**中选择**清单编辑器**   =>  **创建新的应用程序**。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-130">In **App Studio** select **Manifest editor**  => **Create a new app**.</span></span>
3. <span data-ttu-id="5c9f2-131">**添加你的 bot 详细信息**。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-131">**Add your bot details**.</span></span> <span data-ttu-id="5c9f2-132">有关每个字段的完整说明，请参阅 [清单架构定义](../../resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-132">For a full descriptions of each field see [manifest schema definition](../../resources/schema/manifest-schema.md).</span></span> <span data-ttu-id="5c9f2-133">请务必填写所有必填字段。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-133">Be sure to complete all required fields.</span></span>
4. <span data-ttu-id="5c9f2-134">**设置你的 bot**。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-134">**Set up your bot**.</span></span> <span data-ttu-id="5c9f2-135">导航到 " **bot** " 选项卡，选择 " **设置** " 按钮，选择 " **现有机器人**"，然后输入你的 bot 名称。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-135">Navigate to the **Bots** tab, select the **Setup** button, choose **Existing bot**, and enter your bot name.</span></span>
5. <span data-ttu-id="5c9f2-136">**添加您的应用程序 Id**。导航到 " **连接到不同的 bot id** "，并粘贴到之前复制的 **应用 id** 中。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-136">**Add your App Id**. Navigate to **Connect to a different bot id** and paste in the **App Id** you copied earlier.</span></span> <span data-ttu-id="5c9f2-137">在 "范围" 下，选择 " **个人** "，然后选择 " **保存**"。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-137">Under scope, select **Personal** and then select **Save**.</span></span>
6. <span data-ttu-id="5c9f2-138">**为你的 Bot 添加有效的域**。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-138">**Add valid domains for your bot**.</span></span>  <span data-ttu-id="5c9f2-139">仅当你的 bot 要求用户登录时，才需要执行此步骤。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-139">This step is only required if your bot requires the user to sign in.</span></span> <span data-ttu-id="5c9f2-140">导航到 " **域和权限** "，并在 " **有效域** " 字段中输入以下内容：</span><span class="sxs-lookup"><span data-stu-id="5c9f2-140">Navigate to **Domains and permissions** and  in the **Valid Domains** field input the following:</span></span>

```bash
token.botframework.com
```

7.  <span data-ttu-id="5c9f2-141">**测试和分发你的 bot**。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-141">**Test and distribute your bot**.</span></span> <span data-ttu-id="5c9f2-142">选择 " **测试和分布** " 选项卡，然后选择 " **安装** " 将你的 Bot 直接添加到团队实例中。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-142">Choose the **Test and distribute** tab and choose **Install** to add your bot directly to your Teams instance.</span></span> <span data-ttu-id="5c9f2-143">（可选）可以下载已完成的应用程序包以与团队用户共享，也可以将其提供给管理员，使你的 bot 在租户应用程序目录中可用。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-143">Optionally, you can download your completed app package to share with Teams users or provide it to your admin to make your bot available in the tenant app catalog.</span></span>
8. <span data-ttu-id="5c9f2-144">**启动聊天**。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-144">**Start a chat**.</span></span> <span data-ttu-id="5c9f2-145">将电源虚拟代理聊天机器人添加到团队的安装过程已完成。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-145">The setup process for adding your Power Virtual Agents chat bot to Teams is complete.</span></span> <span data-ttu-id="5c9f2-146">现在，你可以在个人聊天中开始与你的 bot 进行对话。</span><span class="sxs-lookup"><span data-stu-id="5c9f2-146">You can now start a conversation with your bot in a personal chat.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5c9f2-147">了解有关发布 Power Virtual 代理 bot 的详细信息</span><span class="sxs-lookup"><span data-stu-id="5c9f2-147">Learn more about publishing your Power Virtual Agents bot</span></span>](/power-virtual-agents/publication-fundamentals-publish-channels)
