---
title: 将 Power Virtual Agents 聊天机器人添加到 Teams
author: laujan
description: 在 Teams 平台中集成 Power Virtual Agents 聊天机器人
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 6103e3b58d7283eab6e9a9932f6dc7778d6fc697
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51697093"
---
# <a name="integrate-a-power-virtual-agents-chatbot-with-microsoft-teams"></a><span data-ttu-id="f787b-103">将 Power Virtual Agents 聊天机器人与 Microsoft Teams 集成</span><span class="sxs-lookup"><span data-stu-id="f787b-103">Integrate a Power Virtual Agents chatbot with Microsoft Teams</span></span>

<span data-ttu-id="f787b-104">[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) 是无代码的引导式图形界面解决方案，它使团队的每位成员能够创建丰富的对话聊天机器人，这些聊天机器人可轻松与 Teams 平台集成。</span><span class="sxs-lookup"><span data-stu-id="f787b-104">[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) is a no-code, guided graphical interface solution that empowers every member of your team to create rich, conversational chatbots that easily integrate with the Teams platform.</span></span> <span data-ttu-id="f787b-105">在 Power Virtual Agents 中创作的所有内容自然呈现在 Teams 中，Power Virtual Agents 机器人与 Teams 本机聊天画布中的用户互动。</span><span class="sxs-lookup"><span data-stu-id="f787b-105">All content authored in Power Virtual Agents renders naturally in Teams and Power Virtual Agents bots engage with users in the Teams native chat canvas.</span></span> <span data-ttu-id="f787b-106">你的 IT 管理员、业务分析师、域专家和经验丰富的应用开发人员可以设计、开发和发布 Teams 的智能虚拟代理，而无需设置开发环境、创建 Web 服务或直接在 Bot Framework 中注册。</span><span class="sxs-lookup"><span data-stu-id="f787b-106">Your IT administrators, business analysts, domain specialists, and skilled app developers can design, develop and publish intelligent virtual agents for Teams without having to setup a development environment, create a web service, or directly register with the Bot Framework.</span></span>  <span data-ttu-id="f787b-107">*请参阅*[使用 Microsoft Power Virtual Agents 为 Teams 创建聊天机器人](../bot-features.md#bots-and-the-microsoft-power-virtual-agents)。</span><span class="sxs-lookup"><span data-stu-id="f787b-107">*See* [Create a chatbot for Teams with Microsoft Power Virtual Agents](../bot-features.md#bots-and-the-microsoft-power-virtual-agents).</span></span>

> [!NOTE]
> <span data-ttu-id="f787b-108">通过将聊天机器人添加到 Microsoft Teams，一些数据（如聊天机器人内容和最终用户聊天内容）将与 Microsoft Teams (这意味着你的数据将流出组织的合规性以及地理或区域边界[) 。](/power-virtual-agents/data-location)</span><span class="sxs-lookup"><span data-stu-id="f787b-108">By adding your chatbot to Microsoft Teams, some of data, such as bot content and end-user chat content, will be shared with Microsoft Teams (meaning that your data will flow outside of your [organization’s compliance and geographic or regional boundaries](/power-virtual-agents/data-location)).</span></span> <br/>
> <span data-ttu-id="f787b-109">有关详细信息，请参阅 Microsoft [Teams 中的安全性和合规性](/MicrosoftTeams/security-compliance-overview)。</span><span class="sxs-lookup"><span data-stu-id="f787b-109">For more information, see the [Security and compliance in Microsoft Teams](/MicrosoftTeams/security-compliance-overview).</span></span>

## <a name="make-your-chatbot-available-in-teams-via-the-power-virtual-agents-portal"></a><span data-ttu-id="f787b-110">通过 Power Virtual Agents 门户在 Teams 中提供聊天机器人</span><span class="sxs-lookup"><span data-stu-id="f787b-110">Make your chatbot available in Teams via the Power Virtual Agents portal</span></span>

1. <span data-ttu-id="f787b-111">**发布最新的自动程序内容**。</span><span class="sxs-lookup"><span data-stu-id="f787b-111">**Publish the latest bot content**.</span></span>  <span data-ttu-id="f787b-112">在 Power [Virtual Agents](https://powervirtualagents.microsoft.com)门户中创建聊天机器人后，你至少需要发布一次聊天机器人，Teams 用户才能与之交互。</span><span class="sxs-lookup"><span data-stu-id="f787b-112">After you have created a chatbot in the [Power Virtual Agents portal](https://powervirtualagents.microsoft.com), you need to publish your bot at least once before Teams users can interact with it.</span></span> <span data-ttu-id="f787b-113">请参阅 [发布最新的自动程序内容](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content)。</span><span class="sxs-lookup"><span data-stu-id="f787b-113">See [Publish the latest bot content](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content).</span></span>

![在电源虚拟代理门户中发布](../../assets/images/pva-publish.png)

2. <span data-ttu-id="f787b-115">**配置 Teams 频道**。</span><span class="sxs-lookup"><span data-stu-id="f787b-115">**Configure the Teams channel**.</span></span> <span data-ttu-id="f787b-116">发布自动程序后，可以添加 Teams 频道，使机器人可供 Teams 用户使用。</span><span class="sxs-lookup"><span data-stu-id="f787b-116">After publishing your bot, you can add the Teams channel to make the bot available to Teams users.</span></span>

![电源虚拟代理门户中的通道](../../assets/images/pva-channels.png)

3. <span data-ttu-id="f787b-118">**为 chatbot 生成应用 ID。**</span><span class="sxs-lookup"><span data-stu-id="f787b-118">**Generate an App Id for your chatbot**.</span></span>  <span data-ttu-id="f787b-119">成功将 Teams 频道添加到聊天机器人后，将在对话框中生成应用 ID。</span><span class="sxs-lookup"><span data-stu-id="f787b-119">When the Teams channel has been successfully added to your chatbot, an **App Id** will be generated in the dialog box.</span></span> <span data-ttu-id="f787b-120">应用 ID 是 Microsoft 为自动程序生成的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="f787b-120">The App Id is a unique Microsoft generated identifier for your bot.</span></span>  <span data-ttu-id="f787b-121">复制并保存应用 ID，稍后将需要它来创建 Teams 应用包。</span><span class="sxs-lookup"><span data-stu-id="f787b-121">Copy and save the App Id — you will need it later to create an app package for Teams.</span></span>

## <a name="add-your-bot-to-teams-using-app-studio"></a><span data-ttu-id="f787b-122">使用 App Studio 将机器人添加到 Teams</span><span class="sxs-lookup"><span data-stu-id="f787b-122">Add your bot to Teams using App Studio</span></span>

<span data-ttu-id="f787b-123">如果在 [Teams 实例中启用了](/microsoftteams/admin-settings) 上传自定义应用，可以使用 Teams App Studio 直接上传聊天机器人并开始使用它。</span><span class="sxs-lookup"><span data-stu-id="f787b-123">If [uploading custom apps is enabled](/microsoftteams/admin-settings) in your Teams instance, you can use Teams App Studio to directly upload your chatbot and start using it right away.</span></span> <span data-ttu-id="f787b-124">如果你想要共享聊天机器人，你可以请求管理员在租户应用目录中提供机器人，也可以向其他人发送你的应用包，并让他们单独上传它。</span><span class="sxs-lookup"><span data-stu-id="f787b-124">If you want to share your chatbot, you can request that your admin make your bot available in the tenant app catalog or you can send others your app package and ask them to upload it independently.</span></span>

1. <span data-ttu-id="f787b-125">**在 Teams 中安装 App Studio。**</span><span class="sxs-lookup"><span data-stu-id="f787b-125">**Install App Studio in Teams**.</span></span> <span data-ttu-id="f787b-126">App Studio 是一款可以从 Teams 应用商店安装的 Teams 应用，可简化 Teams 中机器人的创建和注册过程：</span><span class="sxs-lookup"><span data-stu-id="f787b-126">App Studio is a Teams app you can install from the Teams store that simplifies the creation and registration of your bot in Teams:</span></span> 

  * <span data-ttu-id="f787b-127">从 Teams 实例的左侧导航栏底部选择应用商店图标，然后搜索 **App Studio**。</span><span class="sxs-lookup"><span data-stu-id="f787b-127">Select the app store icon from the bottom of the left nav bar in your Teams instance, and search for **App Studio**.</span></span>
>

&emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="/msteams-docs/msteams-platform/assets/images/get-started/app-studio-store.png"/>   

  * <span data-ttu-id="f787b-128">选择 **App Studio** 磁贴 **，然后选择** 弹出对话框中的"安装"。</span><span class="sxs-lookup"><span data-stu-id="f787b-128">Select the **App Studio** tile and choose **Install** in the pop-up dialog box.</span></span>
>
&emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

2. <span data-ttu-id="f787b-129">**在 App Studio 中创建 Teams 应用清单**。</span><span class="sxs-lookup"><span data-stu-id="f787b-129">**Create the Teams app manifest in App Studio**.</span></span>  <span data-ttu-id="f787b-130">Teams 中的自动程序由应用清单 (JSON) 文件定义，该文件提供有关机器人及其功能的基本信息。</span><span class="sxs-lookup"><span data-stu-id="f787b-130">Bots in Teams are defined by an app manifest (JSON) file that provides basic information about your bot and its capabilities.</span></span> <span data-ttu-id="f787b-131">在 **App Studio 中\*\*\*\*，选择"清单编辑器**   =>  **""新建应用"。**</span><span class="sxs-lookup"><span data-stu-id="f787b-131">In **App Studio** select **Manifest editor**  => **Create a new app**.</span></span>
3. <span data-ttu-id="f787b-132">**添加自动程序详细信息**。</span><span class="sxs-lookup"><span data-stu-id="f787b-132">**Add your bot details**.</span></span> <span data-ttu-id="f787b-133">有关每个字段的完整说明，请参阅 [清单架构定义](../../resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="f787b-133">For a full descriptions of each field see [manifest schema definition](../../resources/schema/manifest-schema.md).</span></span> <span data-ttu-id="f787b-134">请务必填写所有必填字段。</span><span class="sxs-lookup"><span data-stu-id="f787b-134">Be sure to complete all required fields.</span></span>
4. <span data-ttu-id="f787b-135">**设置自动程序**。</span><span class="sxs-lookup"><span data-stu-id="f787b-135">**Set up your bot**.</span></span> <span data-ttu-id="f787b-136">导航到 **"自动程序** "选项卡，选择" **设置"** 按钮，选择" **现有** 自动程序"，然后输入自动程序名称。</span><span class="sxs-lookup"><span data-stu-id="f787b-136">Navigate to the **Bots** tab, select the **Setup** button, choose **Existing bot**, and enter your bot name.</span></span>
5. <span data-ttu-id="f787b-137">**添加应用 ID**。导航到 **"连接到其他自动程序 ID"，** 并粘贴之前复制的应用 ID。</span><span class="sxs-lookup"><span data-stu-id="f787b-137">**Add your App Id**. Navigate to **Connect to a different bot id** and paste in the **App Id** you copied earlier.</span></span> <span data-ttu-id="f787b-138">在"作用域"下 **，选择"个人**"，然后选择"保存 **"。**</span><span class="sxs-lookup"><span data-stu-id="f787b-138">Under scope, select **Personal** and then select **Save**.</span></span>
6. <span data-ttu-id="f787b-139">**为自动程序添加有效的域**。</span><span class="sxs-lookup"><span data-stu-id="f787b-139">**Add valid domains for your bot**.</span></span>  <span data-ttu-id="f787b-140">只有当机器人要求用户登录时，才需要执行此步骤。</span><span class="sxs-lookup"><span data-stu-id="f787b-140">This step is only required if your bot requires the user to sign in.</span></span> <span data-ttu-id="f787b-141">导航到 **"域和权限"，** 并在" **有效域** "字段中输入以下内容：</span><span class="sxs-lookup"><span data-stu-id="f787b-141">Navigate to **Domains and permissions** and  in the **Valid Domains** field input the following:</span></span>

```bash
token.botframework.com
```

7.  <span data-ttu-id="f787b-142">**测试和分发机器人**。</span><span class="sxs-lookup"><span data-stu-id="f787b-142">**Test and distribute your bot**.</span></span> <span data-ttu-id="f787b-143">选择" **测试和分发"** 选项卡，然后选择" **安装** "以将机器人直接添加到 Teams 实例。</span><span class="sxs-lookup"><span data-stu-id="f787b-143">Choose the **Test and distribute** tab and choose **Install** to add your bot directly to your Teams instance.</span></span> <span data-ttu-id="f787b-144">（可选）你可以下载已完成的应用包以与 Teams 用户共享，或提供给管理员，以便自动程序在租户应用目录中可用。</span><span class="sxs-lookup"><span data-stu-id="f787b-144">Optionally, you can download your completed app package to share with Teams users or provide it to your admin to make your bot available in the tenant app catalog.</span></span>
8. <span data-ttu-id="f787b-145">**启动聊天**。</span><span class="sxs-lookup"><span data-stu-id="f787b-145">**Start a chat**.</span></span> <span data-ttu-id="f787b-146">将 Power Virtual Agents 聊天机器人添加到 Teams 的安装过程已完成。</span><span class="sxs-lookup"><span data-stu-id="f787b-146">The setup process for adding your Power Virtual Agents chat bot to Teams is complete.</span></span> <span data-ttu-id="f787b-147">现在可以在个人聊天中与机器人开始对话。</span><span class="sxs-lookup"><span data-stu-id="f787b-147">You can now start a conversation with your bot in a personal chat.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f787b-148">了解更多信息：发布 Power Virtual Agents 机器人</span><span class="sxs-lookup"><span data-stu-id="f787b-148">Learn more: Publish your Power Virtual Agents bot</span></span>](/power-virtual-agents/publication-fundamentals-publish-channels)
