---
title: 将Power Virtual Agents聊天机器人添加到Teams
author: laujan
description: 在Power Virtual Agents平台中集成Teams聊天机器人
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: a38b2447bba42e70d8a1c3c9dca5d92e41cfb77c
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630591"
---
# <a name="add-power-virtual-agents-chatbot"></a><span data-ttu-id="42a50-103">添加 Power Virtual Agent 聊天机器人</span><span class="sxs-lookup"><span data-stu-id="42a50-103">Add Power Virtual Agents chatbot</span></span> 

<span data-ttu-id="42a50-104">Power Virtual Agents无代码的引导式图形界面解决方案，它使团队的每位成员能够创建丰富的对话聊天机器人，这些聊天机器人可轻松与 Teams 集成。</span><span class="sxs-lookup"><span data-stu-id="42a50-104">Power Virtual Agents is a no-code, guided graphical interface solution that empowers every member of your team to create rich, conversational chatbots that easily integrate with the Teams platform.</span></span> <span data-ttu-id="42a50-105">在网站中创作Power Virtual Agents内容自然地呈现在Teams。</span><span class="sxs-lookup"><span data-stu-id="42a50-105">All content authored in Power Virtual Agents renders naturally in Teams.</span></span> <span data-ttu-id="42a50-106">Power Virtual Agents聊天机器人与本机聊天画布Teams用户互动。</span><span class="sxs-lookup"><span data-stu-id="42a50-106">Power Virtual Agents bots engage with users in the Teams native chat canvas.</span></span> <span data-ttu-id="42a50-107">IT 管理员、业务分析师、域专家和熟练应用开发人员可以针对 Teams 设计、开发和发布智能虚拟代理，而无需设置开发环境。</span><span class="sxs-lookup"><span data-stu-id="42a50-107">The IT administrators, business analysts, domain specialists, and skilled app developers can design, develop, and publish intelligent virtual agents for Teams without having to setup a development environment.</span></span> <span data-ttu-id="42a50-108">他们可以创建 Web 服务，或直接在 Bot Framework 中注册。</span><span class="sxs-lookup"><span data-stu-id="42a50-108">They can create a web service, or directly register with the Bot Framework.</span></span> 

<span data-ttu-id="42a50-109">本文档指导您如何通过 Teams 门户Teams Power Virtual Agents聊天机器人，以及如何使用 App Studio Teams聊天机器人。</span><span class="sxs-lookup"><span data-stu-id="42a50-109">This document guides you on how to make your chatbot available in Teams through the Power Virtual Agents portal, and add your bot to Teams using App Studio.</span></span> 

<span data-ttu-id="42a50-110">Power Virtual Agents可以创建功能强大的聊天机器人，这些聊天机器人可以回答客户、其他员工或您的网站或服务的访问者提出的问题。</span><span class="sxs-lookup"><span data-stu-id="42a50-110">Power Virtual Agents lets you create powerful chatbots that can answer questions posed by your customers, other employees, or visitors to your website or service.</span></span>

<span data-ttu-id="42a50-111">无需数据工作者或开发人员，即可轻松创建这些机器人。</span><span class="sxs-lookup"><span data-stu-id="42a50-111">These bots can be created easily without the need for data scientists or developers.</span></span>

> [!NOTE]
> <span data-ttu-id="42a50-112">通过将聊天机器人Microsoft Teams聊天机器人，一些数据（如聊天机器人内容和用户聊天内容）会与用户Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="42a50-112">By adding your chatbot to Microsoft Teams, some of the data, such as bot content and user chat content, is shared with Microsoft Teams.</span></span> <span data-ttu-id="42a50-113">这意味着你的数据流在组织的合规性以及地理或 [区域边界之外](/power-virtual-agents/data-location)。</span><span class="sxs-lookup"><span data-stu-id="42a50-113">It means that your data flows outside of your [organization’s compliance and geographic or regional boundaries](/power-virtual-agents/data-location).</span></span> <br/>

## <a name="make-your-chatbot-available-in-teams-through-the-power-virtual-agents-portal"></a><span data-ttu-id="42a50-114">通过 Teams 门户Power Virtual Agents聊天机器人</span><span class="sxs-lookup"><span data-stu-id="42a50-114">Make your chatbot available in Teams through the Power Virtual Agents portal</span></span>

<span data-ttu-id="42a50-115">若要通过 Teams 门户Power Virtual Agents聊天机器人，必须执行以下过程步骤：</span><span class="sxs-lookup"><span data-stu-id="42a50-115">To make your chatbot available in Teams through the Power Virtual Agents portal, you must perform the following process steps:</span></span>

<span data-ttu-id="42a50-116">**使聊天机器人在聊天室Teams**</span><span class="sxs-lookup"><span data-stu-id="42a50-116">**To make the chatbot available in Teams**</span></span>

1. <span data-ttu-id="42a50-117">**发布最新的自动程序内容**</span><span class="sxs-lookup"><span data-stu-id="42a50-117">**Publish the latest bot content**</span></span>  
<span data-ttu-id="42a50-118">在聊天机器人门户Power Virtual Agents后，必须发布聊天机器人Teams用户才能与其交互。</span><span class="sxs-lookup"><span data-stu-id="42a50-118">After creating a chatbot in the Power Virtual Agents portal, you must publish your bot before Teams users can interact with it.</span></span> <span data-ttu-id="42a50-119">有关详细信息，请参阅发布 [最新的自动程序内容](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content)。</span><span class="sxs-lookup"><span data-stu-id="42a50-119">For more information, see [Publish the latest bot content](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content).</span></span>

   ![在电源虚拟代理门户中发布](../../assets/images/pva-publish.png)

1. <span data-ttu-id="42a50-121">**配置Teams通道**</span><span class="sxs-lookup"><span data-stu-id="42a50-121">**Configure the Teams channel**</span></span>  
<span data-ttu-id="42a50-122">发布自动程序后，添加Teams频道，以便自动程序可供Teams用户使用。</span><span class="sxs-lookup"><span data-stu-id="42a50-122">After publishing your bot, add the Teams channel to make the bot available to Teams users.</span></span>

   ![电源虚拟代理门户中的通道](../../assets/images/pva-channels.png)

1. <span data-ttu-id="42a50-124">**为聊天机器人生成应用 ID**</span><span class="sxs-lookup"><span data-stu-id="42a50-124">**Generate an App ID for your chatbot**</span></span>  
<span data-ttu-id="42a50-125">将Teams添加到聊天机器人后 **，在对话框中** 生成应用 ID。</span><span class="sxs-lookup"><span data-stu-id="42a50-125">After adding the Teams channel to your chatbot, an **App ID** is generated in the dialog box.</span></span> <span data-ttu-id="42a50-126">应用 ID 是 Microsoft 为自动程序生成的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="42a50-126">The App ID is a unique Microsoft generated identifier for your bot.</span></span> <span data-ttu-id="42a50-127">保存应用 ID，为应用创建应用Teams。</span><span class="sxs-lookup"><span data-stu-id="42a50-127">Save the App ID to create an app package for Teams.</span></span>

## <a name="add-your-bot-to-teams-using-app-studio"></a><span data-ttu-id="42a50-128">使用 App Studio Teams聊天机器人</span><span class="sxs-lookup"><span data-stu-id="42a50-128">Add your bot to Teams using App Studio</span></span>

<span data-ttu-id="42a50-129">如果在[Teams](/microsoftteams/admin-settings)实例中启用了上载自定义应用，Teams App Studio 直接上载聊天机器人并立即开始使用它。</span><span class="sxs-lookup"><span data-stu-id="42a50-129">If [uploading custom apps is enabled](/microsoftteams/admin-settings) in your Teams instance, you can use Teams App Studio to directly upload your chatbot and start using it immediately.</span></span> <span data-ttu-id="42a50-130">若要共享聊天机器人，你可以请求管理员在租户应用目录中提供机器人，也可以将应用包发送给其他人，让他们单独上传它。</span><span class="sxs-lookup"><span data-stu-id="42a50-130">To share your chatbot, you can request your admin to make your bot available in the tenant app catalog or you can send your app package to others and ask them to upload it independently.</span></span>

1. <span data-ttu-id="42a50-131">**在 Teams 安装 App Studio**</span><span class="sxs-lookup"><span data-stu-id="42a50-131">**Install App Studio in Teams**</span></span>  
<span data-ttu-id="42a50-132">App Studio 是一款Teams应用。</span><span class="sxs-lookup"><span data-stu-id="42a50-132">App Studio is a Teams app.</span></span> <span data-ttu-id="42a50-133">从 Teams 应用商店安装 App Studio，从而简化在应用商店中创建和注册Teams：</span><span class="sxs-lookup"><span data-stu-id="42a50-133">Install App Studio from the Teams store that simplifies the process of bot creation and registration in Teams:</span></span> 

   1. <span data-ttu-id="42a50-134">从应用程序实例中选择Teams图标，然后搜索 **App Studio**。</span><span class="sxs-lookup"><span data-stu-id="42a50-134">Select the app store icon from Teams instance, and search for **App Studio**.</span></span>

      &emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="../../assets/images/get-started/app-studio-store.png"/>   

   1. <span data-ttu-id="42a50-135">选择 **App Studio** 磁贴 **，然后选择弹出** 对话框中的"安装"。</span><span class="sxs-lookup"><span data-stu-id="42a50-135">Select the **App Studio** tile and select **Install** in the pop-up dialog box.</span></span>

      &emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

1. <span data-ttu-id="42a50-136">**在 App Studio Teams应用清单**</span><span class="sxs-lookup"><span data-stu-id="42a50-136">**Create the Teams app manifest in App Studio**</span></span>  
<span data-ttu-id="42a50-137">聊天机器人Teams应用清单 JSON 文件定义，该文件提供有关自动程序及其功能的基本信息。</span><span class="sxs-lookup"><span data-stu-id="42a50-137">Bots in Teams are defined by an app manifest JSON file that provides the basic information about your bot and its capabilities.</span></span> <span data-ttu-id="42a50-138">在 **App Studio** 中， **选择清单编辑器**，然后选择 **创建新应用**。</span><span class="sxs-lookup"><span data-stu-id="42a50-138">In **App Studio**, select **Manifest editor**, and select **Create a new app**.</span></span>

    ![创建新应用](../../assets/images/get-started/create-new-app.png)

1. <span data-ttu-id="42a50-140">**添加机器人详细信息**</span><span class="sxs-lookup"><span data-stu-id="42a50-140">**Add your bot details**</span></span>  
<span data-ttu-id="42a50-141">完成所有必填字段。</span><span class="sxs-lookup"><span data-stu-id="42a50-141">Complete all the required fields.</span></span> <span data-ttu-id="42a50-142">有关每个字段的完整说明，请参阅 [清单架构定义](../../resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="42a50-142">For a full description of each field see [manifest schema definition](../../resources/schema/manifest-schema.md).</span></span>

    ![添加应用详细信息](../../assets/images/get-started/add-app-details.png)

1. <span data-ttu-id="42a50-144">**设置自动程序** 若要设置自动程序，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="42a50-144">**Set up your bot** To set-up the bot, perform the following steps:</span></span> 
     1. <span data-ttu-id="42a50-145">打开 **"机器人"** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="42a50-145">Open the **Bots** tab.</span></span> 
     1. <span data-ttu-id="42a50-146">选择 **"**  >  **设置现有自动** 程序"，然后输入机器人的名称。</span><span class="sxs-lookup"><span data-stu-id="42a50-146">Select **Setup** > **Existing bot** and enter the name of your bot.</span></span>

   ![自动程序设置](../../assets/images/get-started/bot-set-up.png) 

   <span data-ttu-id="42a50-148">下图描述了如何设置现有自动程序：</span><span class="sxs-lookup"><span data-stu-id="42a50-148">The following image depicts how to set-up an existing bot:</span></span>      

   ![现有自动程序设置](../../assets/images/get-started/existing-bot-set-up.png)
       
1. <span data-ttu-id="42a50-150">**添加应用 ID**</span><span class="sxs-lookup"><span data-stu-id="42a50-150">**Add your App ID**</span></span>  
<span data-ttu-id="42a50-151">若要添加应用 ID，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="42a50-151">To add your App ID, perform the following steps:</span></span>  
    1. <span data-ttu-id="42a50-152">选择 **连接自动程序 ID，** 并粘贴 **之前** 复制的应用 ID。</span><span class="sxs-lookup"><span data-stu-id="42a50-152">Select **Connect to a different bot id** and paste the **App Id** you copied earlier.</span></span> 
    1. <span data-ttu-id="42a50-153">选择 **"作用域**  >  **个人**  >  **保存"。**</span><span class="sxs-lookup"><span data-stu-id="42a50-153">Select **Scope** > **Personal** > **Save**.</span></span>

    ![添加应用 ID](../../assets/images/get-started/add-app-id.png)

1. <span data-ttu-id="42a50-155">**为自动程序添加有效域**</span><span class="sxs-lookup"><span data-stu-id="42a50-155">**Add valid domains for your bot**</span></span>  
<span data-ttu-id="42a50-156">只有当机器人要求用户登录时，才需要执行此步骤。</span><span class="sxs-lookup"><span data-stu-id="42a50-156">This step is only required if your bot requires the user to sign in.</span></span> <span data-ttu-id="42a50-157">选择 **"域和权限"，** 在" **有效域** "字段中提供以下输入：</span><span class="sxs-lookup"><span data-stu-id="42a50-157">Select **Domains and permissions** and in the **Valid Domains** field, provide the following input:</span></span>

    ```bash
       token.botframework.com
    ```

1. <span data-ttu-id="42a50-158">**测试和分发机器人**</span><span class="sxs-lookup"><span data-stu-id="42a50-158">**Test and distribute your bot**</span></span>  
<span data-ttu-id="42a50-159">打开 **测试和分发选项卡\*\*\*\*，然后选择安装** 以将机器人直接添加到你的Teams实例。</span><span class="sxs-lookup"><span data-stu-id="42a50-159">Open **Test and distribute** tab and select **Install** to add your bot directly to your Teams instance.</span></span> <span data-ttu-id="42a50-160">或者，你可以下载已完成的应用包，以便与Teams共享，或提供给管理员以在租户应用目录中提供自动程序。</span><span class="sxs-lookup"><span data-stu-id="42a50-160">Alternately, you can download the completed app package to share with Teams users or provide it to your admin to make your bot available in the tenant app catalog.</span></span>

1. <span data-ttu-id="42a50-161">**启动聊天** </span><span class="sxs-lookup"><span data-stu-id="42a50-161">**Start a chat** </span></span>  
<span data-ttu-id="42a50-162">将聊天聊天机器人添加到聊天Power Virtual Agents的Teams过程已完成。</span><span class="sxs-lookup"><span data-stu-id="42a50-162">The set-up process for adding your Power Virtual Agents chat bot to Teams is complete.</span></span> <span data-ttu-id="42a50-163">现在可以在个人聊天中与机器人开始对话。</span><span class="sxs-lookup"><span data-stu-id="42a50-163">You can now start a conversation with your bot in a personal chat.</span></span>

## <a name="see-also"></a><span data-ttu-id="42a50-164">另请参阅</span><span class="sxs-lookup"><span data-stu-id="42a50-164">See also</span></span>

* [<span data-ttu-id="42a50-165">Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="42a50-165">Power Virtual Agents</span></span>](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)  
* <span data-ttu-id="42a50-166">[使用 Microsoft Teams 创建聊天Power Virtual Agents。](../bot-features.md#bots-and-the-microsoft-power-virtual-agents)</span><span class="sxs-lookup"><span data-stu-id="42a50-166">[Create a chatbot for Teams with Microsoft Power Virtual Agents](../bot-features.md#bots-and-the-microsoft-power-virtual-agents).</span></span>  
* [<span data-ttu-id="42a50-167">Power Virtual Agents门户</span><span class="sxs-lookup"><span data-stu-id="42a50-167">Power Virtual Agents portal</span></span>](https://powervirtualagents.microsoft.com)
* [<span data-ttu-id="42a50-168">发布自动Power Virtual Agents程序</span><span class="sxs-lookup"><span data-stu-id="42a50-168">Publish your Power Virtual Agents bot</span></span>](/power-virtual-agents/publication-fundamentals-publish-channels)
* <span data-ttu-id="42a50-169">[安全与合规Microsoft Teams。](/MicrosoftTeams/security-compliance-overview)</span><span class="sxs-lookup"><span data-stu-id="42a50-169">[Security and compliance in Microsoft Teams](/MicrosoftTeams/security-compliance-overview).</span></span>

## <a name="next-step"></a><span data-ttu-id="42a50-170">后续步骤</span><span class="sxs-lookup"><span data-stu-id="42a50-170">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="42a50-171">创建虚拟助理</span><span class="sxs-lookup"><span data-stu-id="42a50-171">Create virtual assistant</span></span>](~/samples/virtual-assistant.md)

