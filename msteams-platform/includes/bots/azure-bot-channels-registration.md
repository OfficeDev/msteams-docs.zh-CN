---
title: Azure 自动程序通道注册
description: 介绍了用于注册的 Azure 自动程序通道
localization_priority: Normal
ms.topic: overview
ms.author: surbhigupta12
ms.openlocfilehash: 3cbbd204daf98f1c3528dcb6efcfde299a402912
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020946"
---
1. <span data-ttu-id="15178-103">在 [Azure 门户的](https://ms.portal.azure.com/#home)"Azure 服务"下，选择 **"创建资源"。**</span><span class="sxs-lookup"><span data-stu-id="15178-103">In the [Azure portal](https://ms.portal.azure.com/#home), under Azure services, select **Create a resource**.</span></span>
1. <span data-ttu-id="15178-104">在搜索框中输入"bot"。</span><span class="sxs-lookup"><span data-stu-id="15178-104">In the search box enter "bot".</span></span> <span data-ttu-id="15178-105">在下拉列表中，选择自动 **程序频道注册**。</span><span class="sxs-lookup"><span data-stu-id="15178-105">And in the drop-down list, select **Bot Channels Registration**.</span></span>
1. <span data-ttu-id="15178-106">选择" **创建"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="15178-106">Select the **Create** button.</span></span>
1. <span data-ttu-id="15178-107">在" **自动程序通道注册"** 边栏选项卡中，提供有关自动程序的请求信息。</span><span class="sxs-lookup"><span data-stu-id="15178-107">In the **Bot Channel Registration** blade, provide the requested information about your bot.</span></span>
1. <span data-ttu-id="15178-108">现在 **，将"消息** 终结点"框留空，将在部署自动程序后输入所需的 URL。</span><span class="sxs-lookup"><span data-stu-id="15178-108">Leave the **Messaging endpoint** box empty for now, you will enter the required URL after deploying the bot.</span></span> <span data-ttu-id="15178-109">下图显示了注册设置的示例：</span><span class="sxs-lookup"><span data-stu-id="15178-109">The following picture shows an example of the registration settings:</span></span>

    ![自动程序应用通道注册](../../assets/images/authentication/auth-bot-channels-registration.png)

1. <span data-ttu-id="15178-111">单击 **"Microsoft 应用 ID 和密码"，** 然后单击"**新建"。**</span><span class="sxs-lookup"><span data-stu-id="15178-111">Click **Microsoft App ID and password** and then **Create New**.</span></span>

    <span data-ttu-id="15178-112">![创建 Microsoft 应用 ID ](../../assets/images/authentication/CreateMicrosoftAppID.png) ![ 创建新的 Microsoft 应用 ID](../../assets/images/authentication/CreateNewMicrosoftAppID.png)</span><span class="sxs-lookup"><span data-stu-id="15178-112">![Create Microsoft App ID](../../assets/images/authentication/CreateMicrosoftAppID.png) ![Create New Microsoft App ID](../../assets/images/authentication/CreateNewMicrosoftAppID.png)</span></span>    

1. <span data-ttu-id="15178-113">单击 **"应用注册门户"链接中的"创建应用 ID"。**</span><span class="sxs-lookup"><span data-stu-id="15178-113">Click **Create App ID in the App Registration Portal** link.</span></span>

   ![应用注册](../../assets/images/authentication/AppRegistration.png)
   
1. <span data-ttu-id="15178-115">在显示的 **"应用注册"** 窗口中，单击左上角 **的** "新建注册"选项卡。</span><span class="sxs-lookup"><span data-stu-id="15178-115">In the displayed **App registration** window, click the **New registration** tab in the upper left.</span></span>
1. <span data-ttu-id="15178-116">输入要注册的自动程序应用程序的名称，我们使用了 *BotTeamsAuth* (你需要选择自己的唯一名称) 。</span><span class="sxs-lookup"><span data-stu-id="15178-116">Enter the name of the bot application you are registering, we used *BotTeamsAuth* (you need to select your own unique name).</span></span>
1. <span data-ttu-id="15178-117">对于"支持的帐户类型"，选择任何组织目录中的帐户 (任何 Azure AD 目录 - 多租户) 和个人 Microsoft 帐户 (例如 *Skype、Xbox) 。*</span><span class="sxs-lookup"><span data-stu-id="15178-117">For the **Supported account types** select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
1. <span data-ttu-id="15178-118">单击" **注册"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="15178-118">Click the **Register** button.</span></span> <span data-ttu-id="15178-119">完成后，Azure 将显示 *应用程序的* "概述"页。</span><span class="sxs-lookup"><span data-stu-id="15178-119">Once completed, Azure displays the *Overview* page for the application.</span></span>
1. <span data-ttu-id="15178-120">复制并保存到应用程序客户端 (**ID**) 文件。</span><span class="sxs-lookup"><span data-stu-id="15178-120">Copy and save to a file the **Application (client) ID** value.</span></span>
1. <span data-ttu-id="15178-121">在左侧面板中，单击"**证书和密码"。**</span><span class="sxs-lookup"><span data-stu-id="15178-121">In the left panel, click **Certificate and secrets**.</span></span>
    1. <span data-ttu-id="15178-122">在 *"客户端密码"* 下，单击 **"新建客户端密码"。**</span><span class="sxs-lookup"><span data-stu-id="15178-122">Under *Client secrets*, click **New client secret**.</span></span>
    1. <span data-ttu-id="15178-123">添加描述，以便从可能需要为此应用创建的其他人识别此密码。</span><span class="sxs-lookup"><span data-stu-id="15178-123">Add a description to identify this secret from others you might need to create for this app.</span></span>
    1. <span data-ttu-id="15178-124">设置 *到期* 到你的选择。</span><span class="sxs-lookup"><span data-stu-id="15178-124">Set *Expires* to your selection.</span></span>
    1. <span data-ttu-id="15178-125">单击“**添加**”。</span><span class="sxs-lookup"><span data-stu-id="15178-125">Click **Add**.</span></span>
    1. <span data-ttu-id="15178-126">复制客户端密码并将其保存到文件中。</span><span class="sxs-lookup"><span data-stu-id="15178-126">Copy the client secret and save it to a file.</span></span>
1. <span data-ttu-id="15178-127">返回到自动 **程序通道注册** 窗口，并分别复制 **Microsoft 应用 ID** 和密码框中的应用 *ID* 和 **客户端** 密码。</span><span class="sxs-lookup"><span data-stu-id="15178-127">Go back to the **Bot Channel Registration** window and copy the *App ID* and the *Client secret* in the **Microsoft App ID** and **Password** boxes, respectively.</span></span>
1. <span data-ttu-id="15178-128">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="15178-128">Click **OK**.</span></span>
1. <span data-ttu-id="15178-129">最后，单击"**创建"。**</span><span class="sxs-lookup"><span data-stu-id="15178-129">Finally, click **Create**.</span></span>

<span data-ttu-id="15178-130">Azure 创建注册资源后，它将包含在资源组列表中。</span><span class="sxs-lookup"><span data-stu-id="15178-130">After Azure has created the registration resource it will be included in the resource group list.</span></span>  

![自动程序应用通道注册组](~/assets/images/authentication/auth-bot-channels-registration-group.PNG)

<span data-ttu-id="15178-132">创建自动程序频道注册后，你需要启用 Teams 频道。</span><span class="sxs-lookup"><span data-stu-id="15178-132">Once your bot channels registration is created, you'll need to enable the Teams channel.</span></span>

1. <span data-ttu-id="15178-133">在 [Azure 门户的](https://ms.portal.azure.com/#home)"Azure 服务"下，选择刚 **创建的** 自动程序通道注册。</span><span class="sxs-lookup"><span data-stu-id="15178-133">In the [Azure portal](https://ms.portal.azure.com/#home), under Azure services, select the **Bot Channel Registration** you just created.</span></span>
1. <span data-ttu-id="15178-134">在左侧面板中，单击"**频道"。**</span><span class="sxs-lookup"><span data-stu-id="15178-134">In the left panel, click **Channels**.</span></span>
1. <span data-ttu-id="15178-135">单击"Microsoft Teams"图标，然后选择"保存 **"。**</span><span class="sxs-lookup"><span data-stu-id="15178-135">Click the Microsoft Teams icon, then choose **Save**.</span></span>
