---
title: 向你的团队 bot 添加身份验证
author: clearab
description: 如何：将 OAuth 身份验证添加到 Microsoft 团队中的 bot。
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 403072efeccdd09e46ac93e2e811ee2d10131668
ms.sourcegitcommit: aabfd65a67e1889ec16f09476bc757dd4a46ec5b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2020
ms.locfileid: "48097884"
---
# <a name="add-authentication-to-your-teams-bot"></a><span data-ttu-id="6003a-103">向你的团队 bot 添加身份验证</span><span class="sxs-lookup"><span data-stu-id="6003a-103">Add authentication to your Teams bot</span></span>

<span data-ttu-id="6003a-104">有时，您可能需要在 Microsoft 团队中创建可代表用户访问资源的 bot，如邮件服务。</span><span class="sxs-lookup"><span data-stu-id="6003a-104">There are times when you may need to create bots in Microsoft Teams that can access resources on behalf of the user, such as a mail service.</span></span>

<span data-ttu-id="6003a-105">本文演示如何使用基于 OAuth 2.0 的 Azure Bot 服务 v4 SDK 身份验证。</span><span class="sxs-lookup"><span data-stu-id="6003a-105">This article demonstrates how to use Azure Bot Service v4 SDK authentication, based on OAuth 2.0.</span></span> <span data-ttu-id="6003a-106">这样，就可以更轻松地开发可使用基于用户凭据的身份验证令牌的 bot。</span><span class="sxs-lookup"><span data-stu-id="6003a-106">This makes it easier to develop a bot that can use authentication tokens based on the user's credentials.</span></span> <span data-ttu-id="6003a-107">关键是使用 **标识提供程序**，因为我们将在后面看到。</span><span class="sxs-lookup"><span data-stu-id="6003a-107">Key in all this is the use of **identity providers**, as we will see later.</span></span>

<span data-ttu-id="6003a-108">OAuth 2.0 是一种开放标准，用于 Azure Active Directory (Azure AD) 和许多其他标识提供程序使用的身份验证和授权。</span><span class="sxs-lookup"><span data-stu-id="6003a-108">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="6003a-109">对 OAuth 2.0 的基本了解是在团队中使用身份验证的先决条件。</span><span class="sxs-lookup"><span data-stu-id="6003a-109">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

<span data-ttu-id="6003a-110">有关基本了解，请参阅 [oauth 2 已简化](https://aka.ms/oauth2-simplified) ，有关完整规范，则为 [oauth 2.0](https://oauth.net/2/) 。</span><span class="sxs-lookup"><span data-stu-id="6003a-110">See [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) for a basic understanding, and [OAuth 2.0](https://oauth.net/2/) for the complete specification.</span></span>

<span data-ttu-id="6003a-111">有关 Azure Bot 服务如何处理身份验证的详细信息，请参阅 [对话中的用户身份验证](https://aka.ms/azure-bot-authentication)。</span><span class="sxs-lookup"><span data-stu-id="6003a-111">For more information about how the Azure Bot Service handles authentication, see [User authentication within a conversation](https://aka.ms/azure-bot-authentication).</span></span>

<span data-ttu-id="6003a-112">在本文中，您将了解：</span><span class="sxs-lookup"><span data-stu-id="6003a-112">In this article you'll learn:</span></span>

- <span data-ttu-id="6003a-113">**如何创建启用身份验证的 bot**。</span><span class="sxs-lookup"><span data-stu-id="6003a-113">**How to create an authentication-enabled bot**.</span></span> <span data-ttu-id="6003a-114">你将使用 [cs-auth 示例][teams-auth-bot-cs] 来处理用户登录凭据和生成身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="6003a-114">You'll use [cs-auth-sample][teams-auth-bot-cs] to handle user sign-in credentials and the generating the authentication token.</span></span>
- <span data-ttu-id="6003a-115">**如何将机器人部署到 Azure 并将其与标识提供程序关联**。</span><span class="sxs-lookup"><span data-stu-id="6003a-115">**How to deploy the bot to Azure and associate it with an identity provider**.</span></span> <span data-ttu-id="6003a-116">提供程序根据用户登录凭据发出令牌。</span><span class="sxs-lookup"><span data-stu-id="6003a-116">The provider issues a token based on user sign-in credentials.</span></span> <span data-ttu-id="6003a-117">Bot 可以使用令牌访问需要身份验证的资源，如邮件服务。</span><span class="sxs-lookup"><span data-stu-id="6003a-117">The bot can use the token to access resources, such as a mail service, which require authentication.</span></span> <span data-ttu-id="6003a-118">有关详细信息，请参阅  [适用于 bot 的 Microsoft 团队身份验证流](auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="6003a-118">For more information see  [Microsoft Teams authentication flow for bots](auth-flow-bot.md).</span></span>
- <span data-ttu-id="6003a-119">**如何在 Microsoft 团队中集成机器人**。</span><span class="sxs-lookup"><span data-stu-id="6003a-119">**How to integrate the bot within Microsoft Teams**.</span></span> <span data-ttu-id="6003a-120">将 bot 集成后，可以在聊天中登录并与之交换邮件。</span><span class="sxs-lookup"><span data-stu-id="6003a-120">Once the bot has been integrated, you can sign in and exchange messages with it in a chat.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6003a-121">先决条件</span><span class="sxs-lookup"><span data-stu-id="6003a-121">Prerequisites</span></span>

- <span data-ttu-id="6003a-122">有关 [机器人基础][concept-basics]知识、 [管理状态][concept-state]、 [对话框库][concept-dialogs]以及如何 [实施顺序对话流][simple-dialog]的知识。</span><span class="sxs-lookup"><span data-stu-id="6003a-122">Knowledge of [bot basics][concept-basics], [managing state][concept-state], the [dialogs library][concept-dialogs], and how to [implement sequential conversation flow][simple-dialog].</span></span>
- <span data-ttu-id="6003a-123">Azure 和 OAuth 2.0 开发方面的知识。</span><span class="sxs-lookup"><span data-stu-id="6003a-123">Knowledge of Azure and OAuth 2.0 development.</span></span>
- <span data-ttu-id="6003a-124">当前版本的 Visual Studio 和 Git。</span><span class="sxs-lookup"><span data-stu-id="6003a-124">The current versions of Visual Studio and Git.</span></span>
- <span data-ttu-id="6003a-125">Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="6003a-125">Azure account.</span></span> <span data-ttu-id="6003a-126">如果需要，可以创建 [Azure 免费帐户](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="6003a-126">If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="6003a-127">下面的示例。</span><span class="sxs-lookup"><span data-stu-id="6003a-127">The following sample.</span></span>

    | <span data-ttu-id="6003a-128">示例</span><span class="sxs-lookup"><span data-stu-id="6003a-128">Sample</span></span> | <span data-ttu-id="6003a-129">BotBuilder 版本</span><span class="sxs-lookup"><span data-stu-id="6003a-129">BotBuilder version</span></span> | <span data-ttu-id="6003a-130">示</span><span class="sxs-lookup"><span data-stu-id="6003a-130">Demonstrates</span></span> |
    |:---|:---:|:---|
    | <span data-ttu-id="6003a-131">Cs 中的**Bot 身份验证**- [auth-示例][teams-auth-bot-cs]</span><span class="sxs-lookup"><span data-stu-id="6003a-131">**Bot authentication** in [cs-auth-sample][teams-auth-bot-cs]</span></span> | <span data-ttu-id="6003a-132">v4</span><span class="sxs-lookup"><span data-stu-id="6003a-132">v4</span></span> | <span data-ttu-id="6003a-133">OAuthCard 支持</span><span class="sxs-lookup"><span data-stu-id="6003a-133">OAuthCard support</span></span> |
    | <span data-ttu-id="6003a-134">[Js-auth][teams-auth-bot-js]中的**Bot 身份验证**-示例</span><span class="sxs-lookup"><span data-stu-id="6003a-134">**Bot authentication** in [js-auth-sample][teams-auth-bot-js]</span></span> | <span data-ttu-id="6003a-135">v4</span><span class="sxs-lookup"><span data-stu-id="6003a-135">v4</span></span>| <span data-ttu-id="6003a-136">OAuthCard 支持</span><span class="sxs-lookup"><span data-stu-id="6003a-136">OAuthCard support</span></span>  |
    | <span data-ttu-id="6003a-137">[Py-auth][teams-auth-bot-py]中的**Bot 身份验证**-示例</span><span class="sxs-lookup"><span data-stu-id="6003a-137">**Bot authentication** in [py-auth-sample][teams-auth-bot-py]</span></span> | <span data-ttu-id="6003a-138">v4</span><span class="sxs-lookup"><span data-stu-id="6003a-138">v4</span></span> | <span data-ttu-id="6003a-139">OAuthCard 支持</span><span class="sxs-lookup"><span data-stu-id="6003a-139">OAuthCard support</span></span> |

## <a name="create-the-resource-group"></a><span data-ttu-id="6003a-140">创建资源组</span><span class="sxs-lookup"><span data-stu-id="6003a-140">Create the resource group</span></span>

<span data-ttu-id="6003a-141">资源组和服务计划不是必需的，但它们使您可以方便地释放所创建的资源。</span><span class="sxs-lookup"><span data-stu-id="6003a-141">The resource group and the service plan aren't strictly necessary, but they allow you to conveniently release the resources you create.</span></span> <span data-ttu-id="6003a-142">这对于保持资源的组织和可管理性来说是很好的做法。</span><span class="sxs-lookup"><span data-stu-id="6003a-142">This is good practice for keeping your resources organized and manageable.</span></span>

<span data-ttu-id="6003a-143">您可以使用资源组为 Bot 框架创建单独的资源。</span><span class="sxs-lookup"><span data-stu-id="6003a-143">You use a resource group to create individual resources for the Bot Framework.</span></span> <span data-ttu-id="6003a-144">为了提高性能，请确保这些资源位于同一个 Azure 区域中。</span><span class="sxs-lookup"><span data-stu-id="6003a-144">For performance, ensure that these resources are located in the same Azure region.</span></span>

1. <span data-ttu-id="6003a-145">在您的浏览器中，登录到 [**Azure 门户**][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="6003a-145">In your browser, sign into the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="6003a-146">在左侧导航窗格中，选择 " **资源组**"。</span><span class="sxs-lookup"><span data-stu-id="6003a-146">In the left navigation panel, select **Resource groups**.</span></span>
1. <span data-ttu-id="6003a-147">在显示的窗口的左上角，选择 " **添加** " 选项卡以创建新的资源组。</span><span class="sxs-lookup"><span data-stu-id="6003a-147">In the upper left of the displayed window, select **Add** tab to create a new resource group.</span></span> <span data-ttu-id="6003a-148">系统将提示你提供以下内容：</span><span class="sxs-lookup"><span data-stu-id="6003a-148">You'll be prompted to provide the following:</span></span>
    1. <span data-ttu-id="6003a-149">**订阅**。</span><span class="sxs-lookup"><span data-stu-id="6003a-149">**Subscription**.</span></span> <span data-ttu-id="6003a-150">使用现有订阅。</span><span class="sxs-lookup"><span data-stu-id="6003a-150">Use your existing subscription.</span></span>
    1. <span data-ttu-id="6003a-151">**资源组**。</span><span class="sxs-lookup"><span data-stu-id="6003a-151">**Resource group**.</span></span> <span data-ttu-id="6003a-152">输入资源组的名称。</span><span class="sxs-lookup"><span data-stu-id="6003a-152">Enter the name for the resource group.</span></span> <span data-ttu-id="6003a-153">例如，  *TeamsResourceGroup*。</span><span class="sxs-lookup"><span data-stu-id="6003a-153">An example could be  *TeamsResourceGroup*.</span></span> <span data-ttu-id="6003a-154">请记住，该名称必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="6003a-154">Remember that the name must be unique.</span></span>
    1. <span data-ttu-id="6003a-155">从 " **区域** " 下拉菜单中，选择 " *美国西部*" 或 "接近您的应用程序的区域"。</span><span class="sxs-lookup"><span data-stu-id="6003a-155">From the **Region** drop-down menu, select *West US*, or a region close to your applications.</span></span>
    1. <span data-ttu-id="6003a-156">选择 " **查看" 和 "创建** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="6003a-156">Select the **Review and create** button.</span></span> <span data-ttu-id="6003a-157">您应该会看到标题为 "已 *通过验证*"。</span><span class="sxs-lookup"><span data-stu-id="6003a-157">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="6003a-158">选择 " **创建** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="6003a-158">Select the **Create** button.</span></span> <span data-ttu-id="6003a-159">创建资源组可能需要几分钟的时间。</span><span class="sxs-lookup"><span data-stu-id="6003a-159">It may take a few minutes to create the resource group.</span></span>

> [!TIP]
> <span data-ttu-id="6003a-160">与本教程后面创建的资源一样，最好将此资源组固定到您的仪表板以便轻松访问。</span><span class="sxs-lookup"><span data-stu-id="6003a-160">As with the resources you'll create later in this tutorial, it's a good idea to pin this resource group to your dashboard for easy access.</span></span> <span data-ttu-id="6003a-161">如果您想要这样做，请选择 pin 图标 & # 128204;在仪表板的右上方。</span><span class="sxs-lookup"><span data-stu-id="6003a-161">If you'd like to do so, select the pin icon &#128204; in the upper right of the dashboard.</span></span>

## <a name="create-the-service-plan"></a><span data-ttu-id="6003a-162">创建服务计划</span><span class="sxs-lookup"><span data-stu-id="6003a-162">Create the service plan</span></span>

1. <span data-ttu-id="6003a-163">在 [**Azure 门户**][azure-portal]的左侧导航窗格中，选择 " **创建资源**"。</span><span class="sxs-lookup"><span data-stu-id="6003a-163">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="6003a-164">在 "搜索" 框中，键入 *App Service Plan*。</span><span class="sxs-lookup"><span data-stu-id="6003a-164">In the search box, type *App Service Plan*.</span></span> <span data-ttu-id="6003a-165">从搜索结果中选择 **应用服务计划** 卡片。</span><span class="sxs-lookup"><span data-stu-id="6003a-165">Select the **App Service Plan** card from the search results.</span></span>
1. <span data-ttu-id="6003a-166">选择“创建”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="6003a-166">Select **Create**.</span></span>
1. <span data-ttu-id="6003a-167">系统将要求你提供以下信息：</span><span class="sxs-lookup"><span data-stu-id="6003a-167">You'll be asked to provide the following information:</span></span>
    1. <span data-ttu-id="6003a-168">**订阅**。</span><span class="sxs-lookup"><span data-stu-id="6003a-168">**Subscription**.</span></span> <span data-ttu-id="6003a-169">您可以使用现有订阅。</span><span class="sxs-lookup"><span data-stu-id="6003a-169">You can use an existing subscription.</span></span>
    1. <span data-ttu-id="6003a-170">**资源组**。</span><span class="sxs-lookup"><span data-stu-id="6003a-170">**Resource Group**.</span></span> <span data-ttu-id="6003a-171">选择之前创建的组。</span><span class="sxs-lookup"><span data-stu-id="6003a-171">Select the group you created earlier.</span></span>
    1. <span data-ttu-id="6003a-172">**名称**。</span><span class="sxs-lookup"><span data-stu-id="6003a-172">**Name**.</span></span> <span data-ttu-id="6003a-173">输入服务计划的名称。</span><span class="sxs-lookup"><span data-stu-id="6003a-173">Enter the name for the service plan.</span></span> <span data-ttu-id="6003a-174">例如，  *TeamsServicePlan*。</span><span class="sxs-lookup"><span data-stu-id="6003a-174">An example could be  *TeamsServicePlan*.</span></span> <span data-ttu-id="6003a-175">请记住，此名称在组中必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="6003a-175">Remember that the name must be unique, within the group.</span></span>
    1. <span data-ttu-id="6003a-176">**操作系统**。</span><span class="sxs-lookup"><span data-stu-id="6003a-176">**Operating System**.</span></span> <span data-ttu-id="6003a-177">选择 " *Windows* " 或 "适用的操作系统"。</span><span class="sxs-lookup"><span data-stu-id="6003a-177">Select *Windows* or your applicable OS.</span></span>
    1. <span data-ttu-id="6003a-178">**区域**。</span><span class="sxs-lookup"><span data-stu-id="6003a-178">**Region**.</span></span> <span data-ttu-id="6003a-179">选择 " *西部* " 或 "区域接近您的应用程序"。</span><span class="sxs-lookup"><span data-stu-id="6003a-179">Select *West US* or a region close to your applications.</span></span>
    1. <span data-ttu-id="6003a-180">**定价层**。</span><span class="sxs-lookup"><span data-stu-id="6003a-180">**Pricing Tier**.</span></span> <span data-ttu-id="6003a-181">确保选择了 " *标准 S1* "。</span><span class="sxs-lookup"><span data-stu-id="6003a-181">Make sure that *Standard S1* is selected.</span></span> <span data-ttu-id="6003a-182">此值应为默认值。</span><span class="sxs-lookup"><span data-stu-id="6003a-182">This should be the default value.</span></span>
    1. <span data-ttu-id="6003a-183">选择 " **查看" 和 "创建** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="6003a-183">Select the **Review and create** button.</span></span> <span data-ttu-id="6003a-184">您应该会看到标题为 "已 *通过验证*"。</span><span class="sxs-lookup"><span data-stu-id="6003a-184">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="6003a-185">选择“创建”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="6003a-185">Select **Create**.</span></span> <span data-ttu-id="6003a-186">可能需要几分钟的时间来创建应用服务计划。</span><span class="sxs-lookup"><span data-stu-id="6003a-186">It may take a few minutes to create the app service plan.</span></span> <span data-ttu-id="6003a-187">该计划将列在资源组中。</span><span class="sxs-lookup"><span data-stu-id="6003a-187">The plan will be listed in the resource group.</span></span>

## <a name="create-the-bot-channels-registration"></a><span data-ttu-id="6003a-188">创建 bot 通道注册</span><span class="sxs-lookup"><span data-stu-id="6003a-188">Create the bot channels registration</span></span>

<span data-ttu-id="6003a-189">如果你有 Microsoft 应用 Id 和应用密码 (客户端机密) ，bot 通道注册会将您的 web 服务注册为 bot 框架的 bot。</span><span class="sxs-lookup"><span data-stu-id="6003a-189">The bot channels registration registers your web service as a bot with the Bot Framework, provided you have a Microsoft App Id and App password (client secret).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6003a-190">仅当你的 bot 未托管在 Azure 中时，才需要注册你的 bot。</span><span class="sxs-lookup"><span data-stu-id="6003a-190">You only need to register your bot if it is not hosted in Azure.</span></span> <span data-ttu-id="6003a-191">如果你通过 Azure 门户 [创建了一个 bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) ，则它已向该服务注册。</span><span class="sxs-lookup"><span data-stu-id="6003a-191">If you [created a bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) through the Azure portal then it is already registered with the service.</span></span> <span data-ttu-id="6003a-192">如果你通过 [Bot 框架](https://dev.botframework.com/bots/new) 或 [AppStudio](~/concepts/build-and-test/app-studio-overview.md) 创建了你的 bot，你的 Bot 不会在 Azure 中注册。</span><span class="sxs-lookup"><span data-stu-id="6003a-192">If you created your bot through the [Bot Framework](https://dev.botframework.com/bots/new) or [AppStudio](~/concepts/build-and-test/app-studio-overview.md) your bot isn't registered in Azure.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

> [!NOTE]
> <span data-ttu-id="6003a-193">自动程序通道注册资源将显示 **全局** 区域，即使您选择了 "西部我们"。</span><span class="sxs-lookup"><span data-stu-id="6003a-193">The Bot Channels Registration resource will show the **Global** region even if you selected West US.</span></span> <span data-ttu-id="6003a-194">这是预期的。</span><span class="sxs-lookup"><span data-stu-id="6003a-194">This is expected.</span></span>

<span data-ttu-id="6003a-195">有关详细信息，请参阅为 [团队创建机器人](../create-a-bot-for-teams.md)。</span><span class="sxs-lookup"><span data-stu-id="6003a-195">For more information, see [Create a bot for Teams](../create-a-bot-for-teams.md).</span></span>

## <a name="create-the-identity-provider"></a><span data-ttu-id="6003a-196">创建标识提供程序</span><span class="sxs-lookup"><span data-stu-id="6003a-196">Create the identity provider</span></span>

<span data-ttu-id="6003a-197">您需要可用于身份验证的标识提供程序。</span><span class="sxs-lookup"><span data-stu-id="6003a-197">You need an identity provider that can be used for authentication.</span></span>
<span data-ttu-id="6003a-198">在此过程中，你将使用 Azure AD 提供程序;此外，还可以使用其他受支持的 Azure AD 标识提供程序。</span><span class="sxs-lookup"><span data-stu-id="6003a-198">In this procedure you'll use an Azure AD provider; other Azure AD supported identity providers can also be used.</span></span>

1. <span data-ttu-id="6003a-199">在 [**Azure 门户**][azure-portal]的左侧导航窗格中，选择 " **Azure Active Directory**"。</span><span class="sxs-lookup"><span data-stu-id="6003a-199">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Azure Active Directory**.</span></span>
    > [!TIP]
    > <span data-ttu-id="6003a-200">你将需要在可同意委派应用程序请求的租户中创建并注册此 Azure AD 资源。</span><span class="sxs-lookup"><span data-stu-id="6003a-200">You'll need to create and register this Azure AD resource in a tenant in which you can consent to delegate permissions requested by an application.</span></span>
    > <span data-ttu-id="6003a-201">有关创建租户的说明，请参阅 [访问门户和创建租户](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)。</span><span class="sxs-lookup"><span data-stu-id="6003a-201">For instruction on creating a tenant, see [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span></span>
1. <span data-ttu-id="6003a-202">在左面板中，选择 " **应用注册**"。</span><span class="sxs-lookup"><span data-stu-id="6003a-202">In the left panel, select **App registrations**.</span></span>
1. <span data-ttu-id="6003a-203">在右侧面板中，选择左上角的 " **新建注册** " 选项卡。</span><span class="sxs-lookup"><span data-stu-id="6003a-203">In the right panel, select the **New registration** tab, in the upper left.</span></span>
1. <span data-ttu-id="6003a-204">系统将要求你提供以下信息：</span><span class="sxs-lookup"><span data-stu-id="6003a-204">You'll be asked to provide the following information:</span></span>
   1. <span data-ttu-id="6003a-205">**名称**。</span><span class="sxs-lookup"><span data-stu-id="6003a-205">**Name**.</span></span> <span data-ttu-id="6003a-206">输入应用程序的名称。</span><span class="sxs-lookup"><span data-stu-id="6003a-206">Enter the name for the application.</span></span> <span data-ttu-id="6003a-207">例如，  *BotTeamsIdentity*。</span><span class="sxs-lookup"><span data-stu-id="6003a-207">An example could be  *BotTeamsIdentity*.</span></span> <span data-ttu-id="6003a-208">请记住，该名称必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="6003a-208">Remember that the name must be unique.</span></span>
   1. <span data-ttu-id="6003a-209">为您的应用程序选择 **支持的帐户类型** 。</span><span class="sxs-lookup"><span data-stu-id="6003a-209">Select the **Supported account types** for your application.</span></span> <span data-ttu-id="6003a-210">选择任何 \* (任何 AZURE AD 目录-多租户) 和个人 Microsoft 帐户 (例如 Skype、Xbox) 的组织目录中的 "帐户" \*。</span><span class="sxs-lookup"><span data-stu-id="6003a-210">Select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
   1. <span data-ttu-id="6003a-211">对于 **重定向 URI**：</span><span class="sxs-lookup"><span data-stu-id="6003a-211">For the **Redirect URI**:</span></span><br/>
       <span data-ttu-id="6003a-212">&#x2713;选择 " **Web**"。</span><span class="sxs-lookup"><span data-stu-id="6003a-212">&#x2713;Select **Web**.</span></span> <br/>
       <span data-ttu-id="6003a-213">&#x2713; 将 URL 设置为 `https://token.botframework.com/.auth/web/redirect` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-213">&#x2713; Set the URL to `https://token.botframework.com/.auth/web/redirect`.</span></span>
   1. <span data-ttu-id="6003a-214">选择“**注册**”。</span><span class="sxs-lookup"><span data-stu-id="6003a-214">Select **Register**.</span></span>

1. <span data-ttu-id="6003a-215">创建后，Azure 将显示该应用程序的 " **概述** " 页。</span><span class="sxs-lookup"><span data-stu-id="6003a-215">Once it is created, Azure displays the **Overview** page for the app.</span></span> <span data-ttu-id="6003a-216">将下面的信息复制并保存到一个文件中：</span><span class="sxs-lookup"><span data-stu-id="6003a-216">Copy and save the following information to a file:</span></span>

    1. <span data-ttu-id="6003a-217">**应用程序 (客户端) ID**值。</span><span class="sxs-lookup"><span data-stu-id="6003a-217">The **Application (client) ID** value.</span></span> <span data-ttu-id="6003a-218">将此 Azure 标识应用程序注册到你的 bot 时，你将在稍后将此值用作 *客户端 ID* 。</span><span class="sxs-lookup"><span data-stu-id="6003a-218">You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.</span></span>
    1. <span data-ttu-id="6003a-219">**目录 (租户) ID**值。</span><span class="sxs-lookup"><span data-stu-id="6003a-219">The **Directory (tenant) ID** value.</span></span> <span data-ttu-id="6003a-220">您还将此值用作 *租户 ID* ，以向你的 bot 注册此 Azure 标识应用程序。</span><span class="sxs-lookup"><span data-stu-id="6003a-220">You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.</span></span>

1. <span data-ttu-id="6003a-221">在左面板中，选择 " **证书 & 密码** " 以创建应用程序的客户端密码。</span><span class="sxs-lookup"><span data-stu-id="6003a-221">In the left panel, select **Certificates & secrets** to create a client secret for your application.</span></span>

   1. <span data-ttu-id="6003a-222">在 " **客户端密码**" 下，选择 &#x2795; **新的客户端密码**。</span><span class="sxs-lookup"><span data-stu-id="6003a-222">Under **Client secrets**, select &#x2795; **New client secret**.</span></span>
   1. <span data-ttu-id="6003a-223">添加描述以标识来自其他用户可能需要为此应用程序创建的此机密，如 *团队中的 Bot 标识应用程序*。</span><span class="sxs-lookup"><span data-stu-id="6003a-223">Add a description to identify this secret from others you might need to create for this app, such as *Bot identity app in Teams*.</span></span>
   1. <span data-ttu-id="6003a-224">将 **过期** 时间设置为您所做的选择。</span><span class="sxs-lookup"><span data-stu-id="6003a-224">Set **Expires** to your selection.</span></span>
   1. <span data-ttu-id="6003a-225">选择“**添加**”。</span><span class="sxs-lookup"><span data-stu-id="6003a-225">Select **Add**.</span></span>
   1. <span data-ttu-id="6003a-226">在离开此页面之前，请 **记录此密码**。</span><span class="sxs-lookup"><span data-stu-id="6003a-226">Before leaving this page, **record the secret**.</span></span> <span data-ttu-id="6003a-227">在你将 Azure AD 应用程序注册到你的 bot 时，你将在稍后将此值用作 _客户端密码_ 。</span><span class="sxs-lookup"><span data-stu-id="6003a-227">You'll use this value later as the _Client secret_ when you register your Azure AD application with your bot.</span></span>

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a><span data-ttu-id="6003a-228">配置标识提供程序连接，并将其注册到机器人</span><span class="sxs-lookup"><span data-stu-id="6003a-228">Configure the identity provider connection and register it with the bot</span></span>

<span data-ttu-id="6003a-229">注意-服务提供商有两个选项-Azure AD V1 和 Azure AD V2。</span><span class="sxs-lookup"><span data-stu-id="6003a-229">Note-there are two options for Service Providers here-Azure AD V1 and Azure AD V2.</span></span>  <span data-ttu-id="6003a-230">[这里](https://docs.microsoft.com/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison)汇总了两个提供程序之间的差异，但一般来说，V2 提供了有关更改 bot 权限的更多灵活性。</span><span class="sxs-lookup"><span data-stu-id="6003a-230">The differences between the two providers are summarized [here](https://docs.microsoft.com/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison), but in general, V2 provides more flexibility with respect to changing bot permissions.</span></span>  <span data-ttu-id="6003a-231">Graph API 权限在 "范围" 字段中列出，并在添加新权限时，bot 将允许用户在下一个登录时同意新权限。</span><span class="sxs-lookup"><span data-stu-id="6003a-231">Graph API permissions are listed in the scopes field, and as new ones are added, bots will allow users to consent to the new permissions on the next sign in.</span></span>  <span data-ttu-id="6003a-232">对于 V1，用户必须删除机器人许可，以获取在 OAuth 对话框中提示的新权限。</span><span class="sxs-lookup"><span data-stu-id="6003a-232">For V1, the bot consent must be deleted by the user for new permissions to be prompted in the OAuth dialog.</span></span> 

#### <a name="azure-ad-v1"></a><span data-ttu-id="6003a-233">Azure AD V1</span><span class="sxs-lookup"><span data-stu-id="6003a-233">Azure AD V1</span></span>

1. <span data-ttu-id="6003a-234">在 [**Azure 门户**][azure-portal]中，从仪表板中选择资源组。</span><span class="sxs-lookup"><span data-stu-id="6003a-234">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="6003a-235">选择你的 bot 频道注册链接。</span><span class="sxs-lookup"><span data-stu-id="6003a-235">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="6003a-236">在 "资源" 页上，选择 " **设置**"。</span><span class="sxs-lookup"><span data-stu-id="6003a-236">On the resource page, select **Settings**.</span></span>
1. <span data-ttu-id="6003a-237">在页面底部附近的 " **OAuth 连接设置** " 下，选择 " **添加设置**"。</span><span class="sxs-lookup"><span data-stu-id="6003a-237">Under **OAuth Connection Settings** near the bottom of the page, select **Add Setting**.</span></span>
1. <span data-ttu-id="6003a-238">如下所示完成表单：</span><span class="sxs-lookup"><span data-stu-id="6003a-238">Complete the form as follows:</span></span>

    1. <span data-ttu-id="6003a-239">**名称**。</span><span class="sxs-lookup"><span data-stu-id="6003a-239">**Name**.</span></span> <span data-ttu-id="6003a-240">输入连接的名称。</span><span class="sxs-lookup"><span data-stu-id="6003a-240">Enter a name for the connection.</span></span> <span data-ttu-id="6003a-241">您将在文件的 bot 中使用此名称 `appsettings.json` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-241">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="6003a-242">例如 *BotTeamsAuthADv1*。</span><span class="sxs-lookup"><span data-stu-id="6003a-242">For example *BotTeamsAuthADv1*.</span></span>
    1. <span data-ttu-id="6003a-243">**服务提供商**。</span><span class="sxs-lookup"><span data-stu-id="6003a-243">**Service Provider**.</span></span> <span data-ttu-id="6003a-244">选择“**Azure Active Directory**”。</span><span class="sxs-lookup"><span data-stu-id="6003a-244">Select **Azure Active Directory**.</span></span> <span data-ttu-id="6003a-245">选择此项后，将显示 Azure AD 特有的字段。</span><span class="sxs-lookup"><span data-stu-id="6003a-245">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="6003a-246">**客户端 id**。在上面的步骤中，输入您为 Azure 标识提供程序应用程序记录的应用程序 (客户端) ID。</span><span class="sxs-lookup"><span data-stu-id="6003a-246">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="6003a-247">**客户端密码**。</span><span class="sxs-lookup"><span data-stu-id="6003a-247">**Client secret**.</span></span> <span data-ttu-id="6003a-248">在上面的步骤中，输入您为 Azure 标识提供程序应用程序记录的密码。</span><span class="sxs-lookup"><span data-stu-id="6003a-248">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="6003a-249">**授予类型**。</span><span class="sxs-lookup"><span data-stu-id="6003a-249">**Grant Type**.</span></span> <span data-ttu-id="6003a-250">Enter `authorization_code` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-250">Enter `authorization_code`.</span></span>
    1. <span data-ttu-id="6003a-251">**登录 URL**。</span><span class="sxs-lookup"><span data-stu-id="6003a-251">**Login URL**.</span></span> <span data-ttu-id="6003a-252">Enter `https://login.microsoftonline.com` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-252">Enter `https://login.microsoftonline.com`.</span></span>
    1. <span data-ttu-id="6003a-253">**租户 ID**，输入您之前为您的 Azure 标识应用程序记录的 **目录 (租户) ID** ，或根据您创建标识提供程序应用程序时选择的受支持的帐户类型（ **常见** ）。</span><span class="sxs-lookup"><span data-stu-id="6003a-253">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="6003a-254">若要确定要分配的值，请执行以下条件：</span><span class="sxs-lookup"><span data-stu-id="6003a-254">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="6003a-255">如果选择了 "仅 \*在此组织目录中的帐户 \* " （仅限 microsoft \*AAD 目录-"多租户" 中 \* 的 "仅 microsoft 单一租户) " 或 "帐户" (中的 "帐户" () 请输入您之前为 AAD 应用程序记录的 **租户 ID** 。</span><span class="sxs-lookup"><span data-stu-id="6003a-255">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="6003a-256">这将是与可以进行身份验证的用户关联的租户。</span><span class="sxs-lookup"><span data-stu-id="6003a-256">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="6003a-257">如果您在 \*任何 AAD 目录中选择了任何组织目录 (的帐户-多租户和个人 Microsoft 帐户（例如 Skype、Xbox、Outlook) \* 输入 " **通用** 词" 而不是 "租户 ID"）。</span><span class="sxs-lookup"><span data-stu-id="6003a-257">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="6003a-258">否则，AAD 应用将通过已选择 ID 的租户进行验证，并排除个人 Microsoft 帐户。</span><span class="sxs-lookup"><span data-stu-id="6003a-258">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    <span data-ttu-id="6003a-259">水平.</span><span class="sxs-lookup"><span data-stu-id="6003a-259">h.</span></span> <span data-ttu-id="6003a-260">对于 " **资源 URL**"，请输入 `https://graph.microsoft.com/` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-260">For **Resource URL**, enter `https://graph.microsoft.com/`.</span></span> <span data-ttu-id="6003a-261">当前代码示例中不使用此代码。</span><span class="sxs-lookup"><span data-stu-id="6003a-261">This is not used in the current code sample.</span></span>  
    <span data-ttu-id="6003a-262">i.</span><span class="sxs-lookup"><span data-stu-id="6003a-262">i.</span></span> <span data-ttu-id="6003a-263">将 **范围** 保留为空。</span><span class="sxs-lookup"><span data-stu-id="6003a-263">Leave **Scopes** blank.</span></span> <span data-ttu-id="6003a-264">下面的图像是一个示例：</span><span class="sxs-lookup"><span data-stu-id="6003a-264">The following image is an example:</span></span>

    ![团队 bot 应用程序身份验证连接字符串 adv1 视图](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. <span data-ttu-id="6003a-266">选择“**保存**”。</span><span class="sxs-lookup"><span data-stu-id="6003a-266">Select **Save**.</span></span>

#### <a name="azure-ad-v2"></a><span data-ttu-id="6003a-267">Azure AD V2</span><span class="sxs-lookup"><span data-stu-id="6003a-267">Azure AD V2</span></span>

1. <span data-ttu-id="6003a-268">在 [**Azure 门户**][azure-portal]中，从仪表板中选择资源组。</span><span class="sxs-lookup"><span data-stu-id="6003a-268">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="6003a-269">选择你的 bot 频道注册链接。</span><span class="sxs-lookup"><span data-stu-id="6003a-269">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="6003a-270">在 "资源" 页上，选择 " **设置**"。</span><span class="sxs-lookup"><span data-stu-id="6003a-270">On the resource page, select **Settings**.</span></span>
1. <span data-ttu-id="6003a-271">在页面底部附近的 " **OAuth 连接设置** " 下，选择 " **添加设置**"。</span><span class="sxs-lookup"><span data-stu-id="6003a-271">Under **OAuth Connection Settings** near the bottom of the page, select **Add Setting**.</span></span>
1. <span data-ttu-id="6003a-272">如下所示完成表单：</span><span class="sxs-lookup"><span data-stu-id="6003a-272">Complete the form as follows:</span></span>

    1. <span data-ttu-id="6003a-273">**名称**。</span><span class="sxs-lookup"><span data-stu-id="6003a-273">**Name**.</span></span> <span data-ttu-id="6003a-274">输入连接的名称。</span><span class="sxs-lookup"><span data-stu-id="6003a-274">Enter a name for the connection.</span></span> <span data-ttu-id="6003a-275">您将在文件的 bot 中使用此名称 `appsettings.json` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-275">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="6003a-276">例如 *BotTeamsAuthADv2*。</span><span class="sxs-lookup"><span data-stu-id="6003a-276">For example *BotTeamsAuthADv2*.</span></span>
    1. <span data-ttu-id="6003a-277">**服务提供商**。</span><span class="sxs-lookup"><span data-stu-id="6003a-277">**Service Provider**.</span></span> <span data-ttu-id="6003a-278">选择 " **Azure Active Directory v2**"。</span><span class="sxs-lookup"><span data-stu-id="6003a-278">Select **Azure Active Directory v2**.</span></span> <span data-ttu-id="6003a-279">选择此项后，将显示 Azure AD 特有的字段。</span><span class="sxs-lookup"><span data-stu-id="6003a-279">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="6003a-280">**客户端 id**。在上面的步骤中，输入您为 Azure 标识提供程序应用程序记录的应用程序 (客户端) ID。</span><span class="sxs-lookup"><span data-stu-id="6003a-280">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="6003a-281">**客户端密码**。</span><span class="sxs-lookup"><span data-stu-id="6003a-281">**Client secret**.</span></span> <span data-ttu-id="6003a-282">在上面的步骤中，输入您为 Azure 标识提供程序应用程序记录的密码。</span><span class="sxs-lookup"><span data-stu-id="6003a-282">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="6003a-283">**令牌交换 URL**。</span><span class="sxs-lookup"><span data-stu-id="6003a-283">**Token Exchange URL**.</span></span> <span data-ttu-id="6003a-284">将此留空。</span><span class="sxs-lookup"><span data-stu-id="6003a-284">Leave this blank.</span></span>
    1. <span data-ttu-id="6003a-285">**租户 ID**，输入您之前为您的 Azure 标识应用程序记录的 **目录 (租户) ID** ，或根据您创建标识提供程序应用程序时选择的受支持的帐户类型（ **常见** ）。</span><span class="sxs-lookup"><span data-stu-id="6003a-285">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="6003a-286">若要确定要分配的值，请执行以下条件：</span><span class="sxs-lookup"><span data-stu-id="6003a-286">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="6003a-287">如果选择了 "仅 \*在此组织目录中的帐户 \* " （仅限 microsoft \*AAD 目录-"多租户" 中 \* 的 "仅 microsoft 单一租户) " 或 "帐户" (中的 "帐户" () 请输入您之前为 AAD 应用程序记录的 **租户 ID** 。</span><span class="sxs-lookup"><span data-stu-id="6003a-287">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="6003a-288">这将是与可以进行身份验证的用户关联的租户。</span><span class="sxs-lookup"><span data-stu-id="6003a-288">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="6003a-289">如果您在 \*任何 AAD 目录中选择了任何组织目录 (的帐户-多租户和个人 Microsoft 帐户（例如 Skype、Xbox、Outlook) \* 输入 " **通用** 词" 而不是 "租户 ID"）。</span><span class="sxs-lookup"><span data-stu-id="6003a-289">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="6003a-290">否则，AAD 应用将通过已选择 ID 的租户进行验证，并排除个人 Microsoft 帐户。</span><span class="sxs-lookup"><span data-stu-id="6003a-290">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    1. <span data-ttu-id="6003a-291">对于 " **范围**"，请输入此应用程序需要的以空格分隔的图形权限列表，例如： User. User.readbasic.all。 read</span><span class="sxs-lookup"><span data-stu-id="6003a-291">For **Scopes**, enter a space-delimited list of graph permissions this application requires e.g.: User.Read User.ReadBasic.All Mail.Read</span></span> 

1. <span data-ttu-id="6003a-292">选择“**保存**”。</span><span class="sxs-lookup"><span data-stu-id="6003a-292">Select **Save**.</span></span>

### <a name="test-the-connection"></a><span data-ttu-id="6003a-293">测试连接</span><span class="sxs-lookup"><span data-stu-id="6003a-293">Test the connection</span></span>

1. <span data-ttu-id="6003a-294">选择该连接条目以打开您刚创建的连接。</span><span class="sxs-lookup"><span data-stu-id="6003a-294">Select the connection entry to open the connection you just created.</span></span>
1. <span data-ttu-id="6003a-295">在 "**服务提供程序连接" 设置**面板的顶部选择 "**测试连接**"。</span><span class="sxs-lookup"><span data-stu-id="6003a-295">Select **Test Connection** at the top of the **Service Provider Connection Setting** panel.</span></span>
1. <span data-ttu-id="6003a-296">第一次执行此操作时，将打开一个新的浏览器窗口，要求您选择帐户。</span><span class="sxs-lookup"><span data-stu-id="6003a-296">The first time you do this will open a new browser window asking you to select an account.</span></span> <span data-ttu-id="6003a-297">选择要使用的一个。</span><span class="sxs-lookup"><span data-stu-id="6003a-297">Select the one you want to use.</span></span>
1. <span data-ttu-id="6003a-298">接下来，系统将要求您允许标识提供程序使用您的数据 (凭据) 。</span><span class="sxs-lookup"><span data-stu-id="6003a-298">Next, you'll be asked to allow to the identity provider to use your data (credentials).</span></span> <span data-ttu-id="6003a-299">下面的图像是一个示例：</span><span class="sxs-lookup"><span data-stu-id="6003a-299">The following image is an example:</span></span>

    ![团队 bot 身份验证连接字符串 adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. <span data-ttu-id="6003a-301">选择 " **接受**"。</span><span class="sxs-lookup"><span data-stu-id="6003a-301">Select **Accept**.</span></span>
1. <span data-ttu-id="6003a-302">然后，这会将您重定向到 "成功" 页的 " \*\*测试连接 \<your-connection-name> \*\* "。</span><span class="sxs-lookup"><span data-stu-id="6003a-302">This should then redirect you to a **Test Connection to \<your-connection-name> Succeeded** page.</span></span> <span data-ttu-id="6003a-303">如果遇到错误，请刷新页面。</span><span class="sxs-lookup"><span data-stu-id="6003a-303">Refresh the page if you get an error.</span></span> <span data-ttu-id="6003a-304">下面的图像是一个示例：</span><span class="sxs-lookup"><span data-stu-id="6003a-304">The following image is an example:</span></span>

  ![团队 bot 应用程序身份验证连接 str adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

<span data-ttu-id="6003a-306">Bot 代码使用连接名称来检索用户身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="6003a-306">The connection name is used by the bot code to retrieve user authentication tokens.</span></span>

## <a name="prepare-the-bot-sample-code"></a><span data-ttu-id="6003a-307">准备机器人示例代码</span><span class="sxs-lookup"><span data-stu-id="6003a-307">Prepare the bot sample code</span></span>

<span data-ttu-id="6003a-308">完成初步设置后，我们将重点介绍如何创建要在本文中使用的 bot。</span><span class="sxs-lookup"><span data-stu-id="6003a-308">With the preliminary settings done, let's focus on the creation of the bot to use in this article.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6003a-309">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6003a-309">C#/.NET</span></span>](#tab/dotnet)

1. <span data-ttu-id="6003a-310">克隆： [cs-auth-示例][teams-auth-bot-cs]。</span><span class="sxs-lookup"><span data-stu-id="6003a-310">Clone [cs-auth-sample][teams-auth-bot-cs].</span></span>
1. <span data-ttu-id="6003a-311">启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="6003a-311">Launch Visual Studio.</span></span>
1. <span data-ttu-id="6003a-312">在工具栏中，选择 " **文件-> 打开-> 项目/解决方案** "，然后打开 "bot" 项目。</span><span class="sxs-lookup"><span data-stu-id="6003a-312">From the toolbar select **File -> Open -> Project/Solution** and open the bot project.</span></span>
1. <span data-ttu-id="6003a-313">在 c # 中更新 **appsettings.js** ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6003a-313">In C# Update **appsettings.json** as follows:</span></span>

    - <span data-ttu-id="6003a-314">设置 `ConnectionName` 为你添加到 bot 通道注册的标识提供程序连接的名称。</span><span class="sxs-lookup"><span data-stu-id="6003a-314">Set `ConnectionName` to the name of the identity provider connection you added to the bot channel registration.</span></span> <span data-ttu-id="6003a-315">本示例中使用的名称是 *BotTeamsAuthADv1*。</span><span class="sxs-lookup"><span data-stu-id="6003a-315">The name we used in this example is *BotTeamsAuthADv1*.</span></span>
    - <span data-ttu-id="6003a-316">设置 `MicrosoftAppId` 为在 bot 频道注册时保存的 **BOT 应用 ID** 。</span><span class="sxs-lookup"><span data-stu-id="6003a-316">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="6003a-317">设置 `MicrosoftAppPassword` 为在 bot 频道注册时保存的 **客户机密** 。</span><span class="sxs-lookup"><span data-stu-id="6003a-317">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="6003a-318">将设置 `ConnectionName` 为标识提供程序连接的名称。</span><span class="sxs-lookup"><span data-stu-id="6003a-318">Set the `ConnectionName` to the name of the identity provider connection.</span></span>

    <span data-ttu-id="6003a-319">根据你的 bot 密码中的字符，你可能需要 XML 对密码进行转义。</span><span class="sxs-lookup"><span data-stu-id="6003a-319">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="6003a-320">例如，任何与 ( # A0) 的符号都需要编码为 `&amp;` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-320">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. <span data-ttu-id="6003a-321">在 "解决方案资源管理器" 中，导航到 " `TeamsAppManifest` 打开 `manifest.json` " 和 "设置" 文件夹， `id` 并转 `botId` 到在 bot 频道注册时保存的 **bot 应用 ID** 。</span><span class="sxs-lookup"><span data-stu-id="6003a-321">In the Solution Explorer, navigate to the `TeamsAppManifest` folder, open `manifest.json` and set `id` and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="javascript"></a>[<span data-ttu-id="6003a-322">JavaScript</span><span class="sxs-lookup"><span data-stu-id="6003a-322">JavaScript</span></span>](#tab/node-js)

1. <span data-ttu-id="6003a-323">Clone [节点-auth-示例][teams-auth-bot-js]。</span><span class="sxs-lookup"><span data-stu-id="6003a-323">Clone [node-auth-sample][teams-auth-bot-js].</span></span>
1. <span data-ttu-id="6003a-324">在控制台中，导航到项目：</span><span class="sxs-lookup"><span data-stu-id="6003a-324">In a console, navigate to the project:</span></span> </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. <span data-ttu-id="6003a-325">安装模块</span><span class="sxs-lookup"><span data-stu-id="6003a-325">Install modules</span></span></br></br>
`npm install`
1. <span data-ttu-id="6003a-326">更新 **env** 配置，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6003a-326">Update the **.env** configuration as follows:</span></span>

    - <span data-ttu-id="6003a-327">设置 `MicrosoftAppId` 为在 bot 频道注册时保存的 **BOT 应用 ID** 。</span><span class="sxs-lookup"><span data-stu-id="6003a-327">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="6003a-328">设置 `MicrosoftAppPassword` 为在 bot 频道注册时保存的 **客户机密** 。</span><span class="sxs-lookup"><span data-stu-id="6003a-328">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="6003a-329">将设置 `connectionName` 为标识提供程序连接的名称。</span><span class="sxs-lookup"><span data-stu-id="6003a-329">Set the `connectionName` to the name of the identity provider connection.</span></span>

    <span data-ttu-id="6003a-330">根据你的 bot 密码中的字符，你可能需要 XML 对密码进行转义。</span><span class="sxs-lookup"><span data-stu-id="6003a-330">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="6003a-331">例如，任何与 ( # A0) 的符号都需要编码为 `&amp;` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-331">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. <span data-ttu-id="6003a-332">在 `teamsAppManifest` 文件夹中，打开 `manifest.json` 并将 `id`  其设置为您的 **Microsoft 应用 id** ，并将 `botId` 其设置为在 bot 频道注册时保存的 **bot 应用 id** 。</span><span class="sxs-lookup"><span data-stu-id="6003a-332">In the `teamsAppManifest` folder, open `manifest.json` and set `id`  to your **Microsoft App ID** and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="python"></a>[<span data-ttu-id="6003a-333">Python</span><span class="sxs-lookup"><span data-stu-id="6003a-333">Python</span></span>](#tab/python)

1. <span data-ttu-id="6003a-334">Clone 存储库中的 [py-auth-示例][teams-auth-bot-py] 。</span><span class="sxs-lookup"><span data-stu-id="6003a-334">Clone [py-auth-sample][teams-auth-bot-py] from the github repository.</span></span>
1. <span data-ttu-id="6003a-335">更新 **config.py**：</span><span class="sxs-lookup"><span data-stu-id="6003a-335">Update **config.py**:</span></span>

    - <span data-ttu-id="6003a-336">设置 `ConnectionName` 为你添加到你的 bot 的 OAuth 连接设置的名称。</span><span class="sxs-lookup"><span data-stu-id="6003a-336">Set `ConnectionName` to the name of the OAuth connection setting you added to your bot.</span></span>
    - <span data-ttu-id="6003a-337">将 `MicrosoftAppId` 和设置 `MicrosoftAppPassword` 为你的 bot 的应用 ID 和应用密码。</span><span class="sxs-lookup"><span data-stu-id="6003a-337">Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.</span></span>

      <span data-ttu-id="6003a-338">根据你的 bot 密码中的字符，你可能需要 XML 对密码进行转义。</span><span class="sxs-lookup"><span data-stu-id="6003a-338">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="6003a-339">例如，任何与 ( # A0) 的符号都需要编码为 `&amp;` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-339">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="6003a-340">将机器人部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="6003a-340">Deploy the bot to Azure</span></span>

<span data-ttu-id="6003a-341">若要部署 bot，请按照 how to 将 [机器人部署到 Azure](https://aka.ms/azure-bot-deployment-cli)中的步骤操作。</span><span class="sxs-lookup"><span data-stu-id="6003a-341">To deploy the bot, follow the steps in the how to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span></span>

<span data-ttu-id="6003a-342">或者，在 Visual Studio 中，可以按照以下步骤操作：</span><span class="sxs-lookup"><span data-stu-id="6003a-342">Alternatively, while in Visual Studio, you can follow these steps:</span></span>

1. <span data-ttu-id="6003a-343">在 Visual Studio " *解决方案资源管理器* " 中，选择并按住 (或右键单击) 项目名称。</span><span class="sxs-lookup"><span data-stu-id="6003a-343">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span></span>
1. <span data-ttu-id="6003a-344">在下拉菜单中，选择 " **发布**"。</span><span class="sxs-lookup"><span data-stu-id="6003a-344">In the drop-down menu, select **Publish**.</span></span>
1. <span data-ttu-id="6003a-345">在显示的窗口中，选择 " **新建** " 链接。</span><span class="sxs-lookup"><span data-stu-id="6003a-345">In the displayed window, select the **New** link.</span></span>
1. <span data-ttu-id="6003a-346">在对话框窗口中，选择左侧的 " **App Service** "，在右侧 **创建 "新建** "。</span><span class="sxs-lookup"><span data-stu-id="6003a-346">In the dialog window, select **App Service** on the left and **Create New** on the right.</span></span>
1. <span data-ttu-id="6003a-347">选择 " **发布** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="6003a-347">Select the **Publish** button.</span></span>
1. <span data-ttu-id="6003a-348">在下一个对话框窗口中，输入所需的信息。</span><span class="sxs-lookup"><span data-stu-id="6003a-348">In the next dialog window, enter the required information.</span></span> <span data-ttu-id="6003a-349">示例如下：</span><span class="sxs-lookup"><span data-stu-id="6003a-349">The following is an example:</span></span>

   ![auth-应用程序-服务](../../../assets/images/authentication/auth-bot-app-service.png)

1. <span data-ttu-id="6003a-351">选择“创建”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="6003a-351">Select **Create**.</span></span>
1. <span data-ttu-id="6003a-352">如果部署成功完成，您应该会看到它在 Visual Studio 中反映出来。</span><span class="sxs-lookup"><span data-stu-id="6003a-352">If the deployment completes successfully, you should see it reflected in Visual Studio.</span></span> <span data-ttu-id="6003a-353">此外，默认浏览器中会显示一个页面，指示 *你的 bot 已准备就绪！*。</span><span class="sxs-lookup"><span data-stu-id="6003a-353">Moreover, a page is displayed in your default browser saying *Your bot is ready!*.</span></span> <span data-ttu-id="6003a-354">该 URL 将类似于： `https://botteamsauth.azurewebsites.net/` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-354">The URL will be similar to this: `https://botteamsauth.azurewebsites.net/`.</span></span> <span data-ttu-id="6003a-355">将其保存到文件中。</span><span class="sxs-lookup"><span data-stu-id="6003a-355">Save it to a file.</span></span>
1. <span data-ttu-id="6003a-356">在浏览器中，导航到 [**Azure 门户**][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="6003a-356">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="6003a-357">检查您的资源组，应将 bot 与其他资源一起列出。</span><span class="sxs-lookup"><span data-stu-id="6003a-357">Check your resource group, the bot should be listed along with the other resources.</span></span> <span data-ttu-id="6003a-358">下面的图像是一个示例：</span><span class="sxs-lookup"><span data-stu-id="6003a-358">The following image is an example:</span></span>

    ![团队-机器人-auth-应用程序-服务-组](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. <span data-ttu-id="6003a-360">在 "资源" 组中，选择 "bot 频道注册名称" (链接) 。</span><span class="sxs-lookup"><span data-stu-id="6003a-360">In the resource group, select the bot channel registration name (link).</span></span>
1. <span data-ttu-id="6003a-361">在左面板中，选择 " **设置**"。</span><span class="sxs-lookup"><span data-stu-id="6003a-361">In the left panel, select **Settings**.</span></span>
1. <span data-ttu-id="6003a-362">在 " **邮件终结点** " 框中，输入上面接下来的 URL `api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-362">In the **Messaging endpoint** box, enter the URL obtained above followed by `api/messages`.</span></span> <span data-ttu-id="6003a-363">下面是一个示例： `https://botteamsauth.azurewebsites.net/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-363">This is an example: `https://botteamsauth.azurewebsites.net/api/messages`.</span></span>
1. <span data-ttu-id="6003a-364">选择左上角的 " **保存** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="6003a-364">Select the **Save** button in the upper left.</span></span>

## <a name="test-the-bot-using-the-emulator"></a><span data-ttu-id="6003a-365">使用模拟器测试机器人</span><span class="sxs-lookup"><span data-stu-id="6003a-365">Test the bot using the Emulator</span></span>

<span data-ttu-id="6003a-366">如果尚未执行此操作，请安装 [Microsoft Bot 框架模拟器](https://aka.ms/bot-framework-emulator-readme)。</span><span class="sxs-lookup"><span data-stu-id="6003a-366">If you haven't done it already, install the [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span></span> <span data-ttu-id="6003a-367">另请参阅 [Debug with The 模拟器](https://aka.ms/bot-framework-emulator-debug-with-emulator)。</span><span class="sxs-lookup"><span data-stu-id="6003a-367">See also [Debug with the Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span></span>

<span data-ttu-id="6003a-368">为了使 bot 示例登录正常工作，您必须配置仿真程序，如下所示。</span><span class="sxs-lookup"><span data-stu-id="6003a-368">In order for the bot sample login to work you must configure the Emulator as shown below.</span></span>

### <a name="configure-the-emulator-for-authentication"></a><span data-ttu-id="6003a-369">配置仿真程序以进行身份验证</span><span class="sxs-lookup"><span data-stu-id="6003a-369">Configure the Emulator for authentication</span></span>

<span data-ttu-id="6003a-370">如果 bot 需要身份验证，则必须配置仿真程序，如下所示。</span><span class="sxs-lookup"><span data-stu-id="6003a-370">If a bot requires authentication, you must configure the Emulator as shown below.</span></span>

1. <span data-ttu-id="6003a-371">启动仿真程序。</span><span class="sxs-lookup"><span data-stu-id="6003a-371">Start the Emulator.</span></span>
1. <span data-ttu-id="6003a-372">在仿真程序中，选择左下角 &#9881; 的齿轮图标，或右上角的 " **仿真程序设置** " 选项卡。</span><span class="sxs-lookup"><span data-stu-id="6003a-372">In the Emulator, select the gear icon &#9881; in the bottom left, or the **Emulator Settings** tab in the upper right.</span></span>
1. <span data-ttu-id="6003a-373">通过 **使用版本1.0 身份验证令牌**选中此框。</span><span class="sxs-lookup"><span data-stu-id="6003a-373">Check the box by **Use version 1.0 authentication tokens**.</span></span>
1. <span data-ttu-id="6003a-374">输入 **ngrok** 工具的本地路径。</span><span class="sxs-lookup"><span data-stu-id="6003a-374">Enter the local path to the **ngrok** tool.</span></span> <span data-ttu-id="6003a-375">*请参阅* Bot 框架仿真程序/ngrok 隧道集成 [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok))。</span><span class="sxs-lookup"><span data-stu-id="6003a-375">*See* the Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span></span> <span data-ttu-id="6003a-376">有关更多工具信息，请参阅 [ngrok](https://ngrok.com/)。</span><span class="sxs-lookup"><span data-stu-id="6003a-376">For more tool information, see [ngrok](https://ngrok.com/).</span></span>
1. <span data-ttu-id="6003a-377">**在仿真程序启动时，通过运行 ngrok**选中该框。</span><span class="sxs-lookup"><span data-stu-id="6003a-377">Check the box by **Run ngrok when the Emulator starts up**.</span></span>
1. <span data-ttu-id="6003a-378">选择 " **保存** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="6003a-378">Select the **Save** button.</span></span>

<span data-ttu-id="6003a-379">当 bot 显示登录卡且用户选择登录按钮时，仿真程序将打开一个页面，用户可使用该页面使用身份验证提供程序进行登录。</span><span class="sxs-lookup"><span data-stu-id="6003a-379">When the bot displays a sign-in card and the user selects the sign-in button, the Emulator opens a page that the user can use to sign in with the authentication provider.</span></span>
<span data-ttu-id="6003a-380">一旦用户执行此操作，提供程序将生成用户令牌，并将其发送到 bot。</span><span class="sxs-lookup"><span data-stu-id="6003a-380">Once the user does so, the provider generates a user token and sends it to the bot.</span></span> <span data-ttu-id="6003a-381">之后，bot 可以代表用户执行操作。</span><span class="sxs-lookup"><span data-stu-id="6003a-381">After that, the bot can act on behalf of the user.</span></span>

### <a name="test-the-bot-locally"></a><span data-ttu-id="6003a-382">本地测试机器人</span><span class="sxs-lookup"><span data-stu-id="6003a-382">Test the bot locally</span></span>

<span data-ttu-id="6003a-383">配置身份验证机制之后，可以执行实际的机器人测试。</span><span class="sxs-lookup"><span data-stu-id="6003a-383">After you have configured the authentication mechanism, you can perform the actual bot testing.</span></span>  

1. <span data-ttu-id="6003a-384">通过 Visual Studio 在你的计算机上本地运行机器人示例（例如）。</span><span class="sxs-lookup"><span data-stu-id="6003a-384">Run the bot sample locally on your machine, via Visual Studio for example.</span></span>
1. <span data-ttu-id="6003a-385">启动仿真程序。</span><span class="sxs-lookup"><span data-stu-id="6003a-385">Start the Emulator.</span></span>
1. <span data-ttu-id="6003a-386">选择 " **打开 bot** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="6003a-386">Select the **Open bot** button.</span></span>
1. <span data-ttu-id="6003a-387">在 **机器人 url**中，输入 bot 的本地 URL。</span><span class="sxs-lookup"><span data-stu-id="6003a-387">In the **Bot URL**, enter the bot's local URL.</span></span> <span data-ttu-id="6003a-388">通常为 `http://localhost:3978/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-388">Usually, `http://localhost:3978/api/messages`.</span></span>
1. <span data-ttu-id="6003a-389">在 **Microsoft 应用 id** 中，输入 bot 的应用 id `appsettings.json` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-389">In the **Microsoft App ID** enter the bot's app ID from `appsettings.json`.</span></span>
1. <span data-ttu-id="6003a-390">在 **Microsoft App 密码** 中，输入 bot 的应用密码 `appsettings.json` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-390">In the **Microsoft App password** enter the bot's app password from the `appsettings.json`.</span></span>
1. <span data-ttu-id="6003a-391">选择 " **连接**"。</span><span class="sxs-lookup"><span data-stu-id="6003a-391">Select **Connect**.</span></span>
1. <span data-ttu-id="6003a-392">在安装程序启动并运行后，输入任何文本以显示登录卡。</span><span class="sxs-lookup"><span data-stu-id="6003a-392">After the bot is up and running, enter any text to display the sign-in card.</span></span>
1. <span data-ttu-id="6003a-393">选择 " **登录** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="6003a-393">Select the **Sign in** button.</span></span>
1. <span data-ttu-id="6003a-394">将显示一个弹出对话框，以 **确认打开的 URL**。</span><span class="sxs-lookup"><span data-stu-id="6003a-394">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="6003a-395">这是为了让 bot 的用户 () 进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="6003a-395">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="6003a-396">选择 " **确认**"。</span><span class="sxs-lookup"><span data-stu-id="6003a-396">Select **Confirm**.</span></span>
1. <span data-ttu-id="6003a-397">如果需要，请选择适用用户的帐户。</span><span class="sxs-lookup"><span data-stu-id="6003a-397">If asked, select the applicable user's account.</span></span>
1. <span data-ttu-id="6003a-398">根据您对仿真程序使用的配置，可以获取以下内容之一：</span><span class="sxs-lookup"><span data-stu-id="6003a-398">Depending which configuration you used for the Emulator, you get one of the following:</span></span>
    1. <span data-ttu-id="6003a-399">**使用登录验证代码**</span><span class="sxs-lookup"><span data-stu-id="6003a-399">**Using sign-in verification code**</span></span>  
      <span data-ttu-id="6003a-400">&#x2713; 打开显示验证代码的窗口。</span><span class="sxs-lookup"><span data-stu-id="6003a-400">&#x2713; A window is opened displaying the validation code.</span></span>  
      <span data-ttu-id="6003a-401">&#x2713; 将验证代码复制并输入到聊天框中，以完成登录。</span><span class="sxs-lookup"><span data-stu-id="6003a-401">&#x2713; Copy and enter the validation code into the chat box to complete the sign-in.</span></span>
    1. <span data-ttu-id="6003a-402">**使用身份验证令牌**。</span><span class="sxs-lookup"><span data-stu-id="6003a-402">**Using authentication tokens**.</span></span>  
      <span data-ttu-id="6003a-403">&#x2713; 您根据您的凭据登录。</span><span class="sxs-lookup"><span data-stu-id="6003a-403">&#x2713; You're logged in based on your credentials.</span></span>

    <span data-ttu-id="6003a-404">以下图像是登录后的 bot UI 的示例：</span><span class="sxs-lookup"><span data-stu-id="6003a-404">The following image is an example of the bot UI after you've logged in:</span></span>

    ![auth bot 登录仿真程序](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. <span data-ttu-id="6003a-406">如果你在 bot 询问*你是否要查看令牌*时选择 **"是"** ，则会收到类似于以下内容的响应：</span><span class="sxs-lookup"><span data-stu-id="6003a-406">If you select **Yes** when the bot asks *Would you like to view your token?*, you'll get a response similar to the following:</span></span>

    ![身份验证 bot 登录仿真程序令牌](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. <span data-ttu-id="6003a-408">在 "输入聊天" 框中输入 **注销** 以注销。这将释放用户令牌，并且机器人将无法代表你进行操作，除非你再次登录。</span><span class="sxs-lookup"><span data-stu-id="6003a-408">Enter **logout** in the input chat box to sign out. This releases the user token, and the bot won't be able to act on your behalf until you sign in again.</span></span>

> [!NOTE]
> <span data-ttu-id="6003a-409">Bot 身份验证需要使用 **Bot 连接器服务**。</span><span class="sxs-lookup"><span data-stu-id="6003a-409">Bot authentication requires use of the **Bot Connector Service**.</span></span> <span data-ttu-id="6003a-410">服务访问你的 bot 的 bot 通道注册信息。</span><span class="sxs-lookup"><span data-stu-id="6003a-410">The service accesses the bot channels registration information for your bot.</span></span>

## <a name="test-the-deployed-bot"></a><span data-ttu-id="6003a-411">测试部署的 bot</span><span class="sxs-lookup"><span data-stu-id="6003a-411">Test the deployed bot</span></span>

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. <span data-ttu-id="6003a-412">在浏览器中，导航到 [**Azure 门户**][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="6003a-412">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="6003a-413">查找您的资源组。</span><span class="sxs-lookup"><span data-stu-id="6003a-413">Find your resource group.</span></span>
1. <span data-ttu-id="6003a-414">选择 "资源" 链接。</span><span class="sxs-lookup"><span data-stu-id="6003a-414">Select the resource link.</span></span> <span data-ttu-id="6003a-415">将显示 "资源" 页。</span><span class="sxs-lookup"><span data-stu-id="6003a-415">The resource page is displayed.</span></span>
1. <span data-ttu-id="6003a-416">在 "资源" 页中，选择 " **在 Web 聊天中测试**"。</span><span class="sxs-lookup"><span data-stu-id="6003a-416">In the resource page, select **Test in Web Chat**.</span></span> <span data-ttu-id="6003a-417">机器人将启动并显示预定义的问候语。</span><span class="sxs-lookup"><span data-stu-id="6003a-417">The bot starts and displays the predefined greetings.</span></span>
1. <span data-ttu-id="6003a-418">在 "聊天" 框中键入任何内容。</span><span class="sxs-lookup"><span data-stu-id="6003a-418">Type anything in the chat box.</span></span>
1. <span data-ttu-id="6003a-419">选择 " **登录** " 框。</span><span class="sxs-lookup"><span data-stu-id="6003a-419">Select the **Sign in** box.</span></span>
1. <span data-ttu-id="6003a-420">将显示一个弹出对话框，以 **确认打开的 URL**。</span><span class="sxs-lookup"><span data-stu-id="6003a-420">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="6003a-421">这是为了让 bot 的用户 () 进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="6003a-421">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="6003a-422">选择 " **确认**"。</span><span class="sxs-lookup"><span data-stu-id="6003a-422">Select **Confirm**.</span></span>
1. <span data-ttu-id="6003a-423">如果需要，请选择适用用户的帐户。</span><span class="sxs-lookup"><span data-stu-id="6003a-423">If asked, select the applicable user's account.</span></span>
    <span data-ttu-id="6003a-424">以下图像是登录后的 bot UI 的示例：</span><span class="sxs-lookup"><span data-stu-id="6003a-424">The following image is an example of the bot UI after you have logged in:</span></span>

    ![已部署身份验证 bot 登录](../../../assets/images/authentication/auth-bot-login-deployed.PNG)<span data-ttu-id="6003a-426">.</span><span class="sxs-lookup"><span data-stu-id="6003a-426">.</span></span>

1. <span data-ttu-id="6003a-427">选择 **"是"** 按钮以显示您的身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="6003a-427">Select the **Yes** button to display your authentication token.</span></span> <span data-ttu-id="6003a-428">下面的图像是一个示例：</span><span class="sxs-lookup"><span data-stu-id="6003a-428">The following image is an example:</span></span>

    ![授权 bot 登录部署令牌](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG)<span data-ttu-id="6003a-430">.</span><span class="sxs-lookup"><span data-stu-id="6003a-430">.</span></span>

1. <span data-ttu-id="6003a-431">输入注销以注销。</span><span class="sxs-lookup"><span data-stu-id="6003a-431">Enter logout to sign out.</span></span>

    ![已部署注销的身份验证机器人](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> <span data-ttu-id="6003a-433">如果你在登录时遇到问题，请尝试再次测试连接，如前面步骤中所述。</span><span class="sxs-lookup"><span data-stu-id="6003a-433">If you're having problems signing in, try to test the connection again as described in the previous steps.</span></span> <span data-ttu-id="6003a-434">这可能会重新创建身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="6003a-434">This could recreate the authentication token.</span></span>
> <span data-ttu-id="6003a-435">在 Azure 中使用 Bot 框架 Web 聊天客户端时，您可能需要在身份验证正确建立前多次进行登录。</span><span class="sxs-lookup"><span data-stu-id="6003a-435">With the Bot Framework Web Chat client in Azure, you may need to sign in several times before the authentication is established correctly.</span></span>

## <a name="install-and-test-the-bot-in-teams"></a><span data-ttu-id="6003a-436">在团队中安装和测试机器人</span><span class="sxs-lookup"><span data-stu-id="6003a-436">Install and test the bot in Teams</span></span>

1. <span data-ttu-id="6003a-437">在机器人项目中，确保 `TeamsAppManifest` 文件夹包含 `manifest.json` `outline.png` 和文件一起包含 `color.png` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-437">In your bot project, ensure that the `TeamsAppManifest` folder contains the `manifest.json` along with an `outline.png` and `color.png` files.</span></span>
1. <span data-ttu-id="6003a-438">在 "解决方案资源管理器" 中，导航到该 `TeamsAppManifest` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="6003a-438">In Solution Explorer, navigate to the `TeamsAppManifest` folder.</span></span> <span data-ttu-id="6003a-439">`manifest.json`通过分配以下值进行编辑：</span><span class="sxs-lookup"><span data-stu-id="6003a-439">Edit `manifest.json` by assigning the following values:</span></span>
    1. <span data-ttu-id="6003a-440">确保在将 bot 频道注册时收到的 **Bot 应用 ID** 分配给 `id` 和 `botId` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-440">Ensure that the **bot App ID** you received at the time of the bot channel registration is assigned to `id` and `botId`.</span></span>
    1. <span data-ttu-id="6003a-441">将此值分配给： `validDomains: [ "token.botframework.com" ]` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-441">Assign this value: `validDomains: [ "token.botframework.com" ]`.</span></span>
1. <span data-ttu-id="6003a-442">选择和 **压缩** `manifest.json` 、 `outline.png` 和 `color.png` 文件。</span><span class="sxs-lookup"><span data-stu-id="6003a-442">Select and **zip** the `manifest.json`, `outline.png`, and `color.png` files.</span></span>
1. <span data-ttu-id="6003a-443">打开 **Microsoft 团队**。</span><span class="sxs-lookup"><span data-stu-id="6003a-443">Open **Microsoft Teams**.</span></span>
1. <span data-ttu-id="6003a-444">在左侧面板中的底部，选择 "应用" **图标**。</span><span class="sxs-lookup"><span data-stu-id="6003a-444">In the left panel, at the bottom, select the **Apps icon**.</span></span>
1. <span data-ttu-id="6003a-445">在右侧面板的底部，选择 " **上传自定义应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="6003a-445">In the right panel, at the bottom, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="6003a-446">导航到该 `TeamsAppManifest` 文件夹并上传压缩清单。</span><span class="sxs-lookup"><span data-stu-id="6003a-446">Navigate to the `TeamsAppManifest` folder and upload the zipped manifest.</span></span>
<span data-ttu-id="6003a-447">将显示以下向导：</span><span class="sxs-lookup"><span data-stu-id="6003a-447">The following wizard is displayed:</span></span>

    ![授权 bot 团队上传](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. <span data-ttu-id="6003a-449">选择 " **添加到团队** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="6003a-449">Select the **Add to a team** button.</span></span>
1. <span data-ttu-id="6003a-450">在下一个窗口中，选择要在其中使用 bot 的团队。</span><span class="sxs-lookup"><span data-stu-id="6003a-450">In the next window, select the team where you want to use the bot.</span></span>
1. <span data-ttu-id="6003a-451">选择 " **设置机器人** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="6003a-451">Select the **Set up a bot** button.</span></span>
1. <span data-ttu-id="6003a-452">在左面板中选择 ( # A3) 的三个点。</span><span class="sxs-lookup"><span data-stu-id="6003a-452">Select the three dots (&#x25cf;&#x25cf;&#x25cf;) in the left panel.</span></span> <span data-ttu-id="6003a-453">然后，选择 " **App Studio** " 图标。</span><span class="sxs-lookup"><span data-stu-id="6003a-453">Then select the **App Studio** icon.</span></span>
1. <span data-ttu-id="6003a-454">选择 " **清单编辑器** " 选项卡。您应该会看到您上载的 bot 的图标。</span><span class="sxs-lookup"><span data-stu-id="6003a-454">Select the **Manifest editor** tab. You should see the icon for the bot you uploaded.</span></span>
1. <span data-ttu-id="6003a-455">此外，您还应该能够在聊天列表中看到作为联系人列出的 bot，您可以使用它来与 bot 交换邮件。</span><span class="sxs-lookup"><span data-stu-id="6003a-455">Also, you should be able to see the bot listed as a contact in the chat list that you can use to exchange messages with the bot.</span></span>

### <a name="testing-the-bot-locally-in-teams"></a><span data-ttu-id="6003a-456">在团队中本地测试机器人</span><span class="sxs-lookup"><span data-stu-id="6003a-456">Testing the bot locally in Teams</span></span>

<span data-ttu-id="6003a-457">Microsoft 团队是完全基于云的产品，它需要使用 HTTPS 终结点从云中获取所有 it 访问的服务。</span><span class="sxs-lookup"><span data-stu-id="6003a-457">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="6003a-458">因此，若要启用机器人 (我们的示例) 在团队中工作，您需要将代码发布到您选择的云，或使本地运行的实例可通过 **隧道** 工具进行外部访问。</span><span class="sxs-lookup"><span data-stu-id="6003a-458">Therefore, to enable the bot (our sample) to work in Teams, you need to either publish the code to the cloud of your choice, or make a locally running instance externally accessible via a **tunneling** tool.</span></span> <span data-ttu-id="6003a-459">我们建议  [ngrok](https://ngrok.com/download)，这将为您在您的计算机上本地打开的端口创建外部可寻址的 URL。</span><span class="sxs-lookup"><span data-stu-id="6003a-459">We recommend  [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span>
<span data-ttu-id="6003a-460">若要设置 ngrok 以准备在本地运行 Microsoft 团队应用程序，请按照以下步骤操作：</span><span class="sxs-lookup"><span data-stu-id="6003a-460">To set up ngrok in preparation for running your Microsoft Teams app locally, follow these steps:</span></span>

1. <span data-ttu-id="6003a-461">在终端窗口中，转到已安装的目录 `ngrok.exe` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-461">In a terminal window, go the directory where you have `ngrok.exe` installed.</span></span> <span data-ttu-id="6003a-462">建议设置要指向的 *环境变量* 路径。</span><span class="sxs-lookup"><span data-stu-id="6003a-462">We suggest setting the *environment variable* path to point to it.</span></span>
1. <span data-ttu-id="6003a-463">例如，运行 `ngrok http 3978 --host-header=localhost:3978` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-463">Run, for example, `ngrok http 3978 --host-header=localhost:3978`.</span></span> <span data-ttu-id="6003a-464">根据需要更换端口号。</span><span class="sxs-lookup"><span data-stu-id="6003a-464">Replace the port number as needed.</span></span>
<span data-ttu-id="6003a-465">这将启动 ngrok 以侦听您指定的端口。</span><span class="sxs-lookup"><span data-stu-id="6003a-465">This launches ngrok to listen on the port you specify.</span></span> <span data-ttu-id="6003a-466">在 return 中，它为您提供一个外部可寻址的 URL，只要 ngrok 正在运行，它就会有效。</span><span class="sxs-lookup"><span data-stu-id="6003a-466">In return, it gives you an externally addressable URL, valid for as long as ngrok is running.</span></span> <span data-ttu-id="6003a-467">下面的图像是一个示例：</span><span class="sxs-lookup"><span data-stu-id="6003a-467">The following image is an example:</span></span>

    ![团队机器人应用程序身份验证连接字符串 adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG)<span data-ttu-id="6003a-469">.</span><span class="sxs-lookup"><span data-stu-id="6003a-469">.</span></span>

1. <span data-ttu-id="6003a-470">复制转发 HTTPS 地址。</span><span class="sxs-lookup"><span data-stu-id="6003a-470">Copy the forwarding HTTPS address.</span></span> <span data-ttu-id="6003a-471">它应类似于以下内容： `https://dea822bf.ngrok.io/` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-471">It should be similar to the following: `https://dea822bf.ngrok.io/`.</span></span>
1. <span data-ttu-id="6003a-472">Append `/api/messages` 获取 `https://dea822bf.ngrok.io/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-472">Append `/api/messages` to obtain `https://dea822bf.ngrok.io/api/messages`.</span></span> <span data-ttu-id="6003a-473">这是在 Microsoft 团队的聊天中，在计算机上本地运行的 bot 的 **消息终结点** ，并可通过 web 访问。</span><span class="sxs-lookup"><span data-stu-id="6003a-473">This is the **messages endpoint** for the bot running locally on your machine and reachable over the web in a chat in Microsoft Teams.</span></span>
1. <span data-ttu-id="6003a-474">要执行的最后一个步骤是更新已部署的 bot 的消息终结点。</span><span class="sxs-lookup"><span data-stu-id="6003a-474">One final step to perform is to update the messages endpoint of the deployed bot.</span></span> <span data-ttu-id="6003a-475">在此示例中，我们在 Azure 中部署了机器人。</span><span class="sxs-lookup"><span data-stu-id="6003a-475">In the example, we deployed the bot in Azure.</span></span> <span data-ttu-id="6003a-476">因此，\* \* 我们将执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="6003a-476">So \*\*let's perform these steps:</span></span>
    1. <span data-ttu-id="6003a-477">在浏览器中导航到 [**Azure 门户**][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="6003a-477">In your browser navigate to the [**Azure portal**][azure-portal].</span></span>
    1. <span data-ttu-id="6003a-478">选择你的 **Bot 频道注册**。</span><span class="sxs-lookup"><span data-stu-id="6003a-478">Select your **Bot Channel Registration**.</span></span>
    1. <span data-ttu-id="6003a-479">在左面板中，选择 " **设置**"。</span><span class="sxs-lookup"><span data-stu-id="6003a-479">In the left panel, select **Settings**.</span></span>
    1. <span data-ttu-id="6003a-480">在右侧面板中的 " **邮件终结点** " 框中，输入 ngrok URL （在我们的示例中） `https://dea822bf.ngrok.io/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="6003a-480">In the right panel, in the **Messaging endpoint** box, enter the ngrok URL, in our example, `https://dea822bf.ngrok.io/api/messages`.</span></span>
1. <span data-ttu-id="6003a-481">在本地启动你的 bot，例如在 Visual Studio 调试模式下。</span><span class="sxs-lookup"><span data-stu-id="6003a-481">Start your bot locally, for example in Visual Studio debug mode.</span></span>
1. <span data-ttu-id="6003a-482">使用 Bot 框架门户的 **测试 Web 聊天**在本地运行时测试机器人。</span><span class="sxs-lookup"><span data-stu-id="6003a-482">Test the bot while running locally using the Bot Framework portal's **Test Web chat**.</span></span> <span data-ttu-id="6003a-483">与模拟器一样，此测试不允许您访问特定于团队的功能。</span><span class="sxs-lookup"><span data-stu-id="6003a-483">Like the Emulator, this test doesn't allow you to access Teams-specific functionality.</span></span>
1. <span data-ttu-id="6003a-484">在运行的终端窗口中 `ngrok` ，可以查看 bot 和 web 聊天客户端之间的 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="6003a-484">In the terminal window where `ngrok` is running you can see HTTP traffic between the bot and the web chat client.</span></span> <span data-ttu-id="6003a-485">如果需要更详细的视图，请在浏览器窗口中输入 `http://127.0.0.1:4040` 从以前的终端窗口中获取的。</span><span class="sxs-lookup"><span data-stu-id="6003a-485">If you want a more detailed view, in a browser window enter `http://127.0.0.1:4040` you obtained from the previous terminal window.</span></span> <span data-ttu-id="6003a-486">下面的图像是一个示例：</span><span class="sxs-lookup"><span data-stu-id="6003a-486">The following image is an example:</span></span>

    ![auth bot 团队 ngrok 测试](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png)<span data-ttu-id="6003a-488">.</span><span class="sxs-lookup"><span data-stu-id="6003a-488">.</span></span>

> [!NOTE]
> <span data-ttu-id="6003a-489">如果您停止并重新启动 ngrok，则 URL 会发生更改。</span><span class="sxs-lookup"><span data-stu-id="6003a-489">If you stop and restart ngrok, the URL changes.</span></span> <span data-ttu-id="6003a-490">若要在项目中使用 ngrok，并根据所使用的功能，必须更新所有 URL 引用。</span><span class="sxs-lookup"><span data-stu-id="6003a-490">To use ngrok in your project, and depending on the capabilities you're using, you must update all URL references.</span></span>
 

## <a name="additional-information"></a><span data-ttu-id="6003a-491">其他信息</span><span class="sxs-lookup"><span data-stu-id="6003a-491">Additional information</span></span>

### <a name="teamsappmanifestmanifestjson"></a><span data-ttu-id="6003a-492">上的 TeamsAppManifest/manifest.js</span><span class="sxs-lookup"><span data-stu-id="6003a-492">TeamsAppManifest/manifest.json</span></span>

<span data-ttu-id="6003a-493">此清单包含 Microsoft 团队与 bot 连接所需的信息。</span><span class="sxs-lookup"><span data-stu-id="6003a-493">This manifest contains information needed by Microsoft Teams to connect with the bot.</span></span>  

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0.0",
  "id": "",
  "packageName": "com.teams.auth.bot",
  "developer": {
    "name": "TeamsBotAuth",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.teams.com/privacy",
    "termsOfUseUrl": "https://www.teams.com/termsofuse"
  },
  "icons": {
    "color": "color.png",
    "outline": "outline.png"
  },
  "name": {
    "short": "TeamsBotAuth",
    "full": "Teams Bot Authentication"
  },
  "description": {
    "short": "TeamsBotAuth",
    "full": "Teams Bot Authentication"
  },
  "accentColor": "#FFFFFF",
  "bots": [
    {
      "botId": "",
      "scopes": [
        "groupchat",
        "team"
      ],
      "supportsFiles": false,
      "isNotificationOnly": false
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [ "token.botframework.com" ]
}
```

<span data-ttu-id="6003a-494">通过身份验证，团队的行为与其他频道略有不同，如下所述。</span><span class="sxs-lookup"><span data-stu-id="6003a-494">With authentication, Teams behaves slightly differently than other channels, as explained below.</span></span>

### <a name="handling-invoke-activity"></a><span data-ttu-id="6003a-495">处理调用活动</span><span class="sxs-lookup"><span data-stu-id="6003a-495">Handling Invoke Activity</span></span>

<span data-ttu-id="6003a-496">**调用活动**将发送到 bot，而不是其他通道使用的事件活动。</span><span class="sxs-lookup"><span data-stu-id="6003a-496">An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.</span></span>
<span data-ttu-id="6003a-497">这是通过 **ActivityHandler**的 classing 完成的。</span><span class="sxs-lookup"><span data-stu-id="6003a-497">This is done by sub-classing the **ActivityHandler**.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6003a-498">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6003a-498">C#/.NET</span></span>](#tab/dotnet-sample)

<span data-ttu-id="6003a-499">**Bot/DialogBot**</span><span class="sxs-lookup"><span data-stu-id="6003a-499">**Bots/DialogBot.cs**</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

<span data-ttu-id="6003a-500">**Bot/TeamsBot**</span><span class="sxs-lookup"><span data-stu-id="6003a-500">**Bots/TeamsBot.cs**</span></span>

<span data-ttu-id="6003a-501">如果使用了**OAuthPrompt** ，则必须将*调用活动*转发到对话框。</span><span class="sxs-lookup"><span data-stu-id="6003a-501">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a><span data-ttu-id="6003a-502">TeamsActivityHandler.cs</span><span class="sxs-lookup"><span data-stu-id="6003a-502">TeamsActivityHandler.cs</span></span>

```csharp

protected virtual Task OnInvokeActivityAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    switch (turnContext.Activity.Name)
    {
        case "signin/verifyState":
            return OnSigninVerifyStateAsync(turnContext, cancellationToken);

        default:
            return Task.CompletedTask;
    }
}

protected virtual Task OnSigninVerifyStateAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    return Task.CompletedTask;
}
```

# <a name="javascript"></a>[<span data-ttu-id="6003a-503">JavaScript</span><span class="sxs-lookup"><span data-stu-id="6003a-503">JavaScript</span></span>](#tab/node-js-dialog-sample)

<span data-ttu-id="6003a-504">**bot/dialogBot.js**</span><span class="sxs-lookup"><span data-stu-id="6003a-504">**bots/dialogBot.js**</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

<span data-ttu-id="6003a-505">**bot/teamsBot.js**</span><span class="sxs-lookup"><span data-stu-id="6003a-505">**bots/teamsBot.js**</span></span>

<span data-ttu-id="6003a-506">如果使用了**OAuthPrompt** ，则必须将*调用活动*转发到对话框。</span><span class="sxs-lookup"><span data-stu-id="6003a-506">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

<span data-ttu-id="6003a-507">**对话框/mainDialog.js**</span><span class="sxs-lookup"><span data-stu-id="6003a-507">**dialogs/mainDialog.js**</span></span>

<span data-ttu-id="6003a-508">在对话步骤中，使用 `beginDialog` "" 启动 OAuth 提示，这将要求用户登录。</span><span class="sxs-lookup"><span data-stu-id="6003a-508">Within a dialog step, use `beginDialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="6003a-509">如果用户已登录，则会生成令牌响应事件，而不会提示用户。</span><span class="sxs-lookup"><span data-stu-id="6003a-509">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="6003a-510">否则，这将提示用户登录。</span><span class="sxs-lookup"><span data-stu-id="6003a-510">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="6003a-511">Azure Bot 服务在用户尝试登录后发送令牌响应事件。</span><span class="sxs-lookup"><span data-stu-id="6003a-511">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

<span data-ttu-id="6003a-512">在下面的对话框步骤中，检查上一步的结果中是否存在令牌。</span><span class="sxs-lookup"><span data-stu-id="6003a-512">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="6003a-513">如果不为 null，则用户已成功登录。</span><span class="sxs-lookup"><span data-stu-id="6003a-513">If it is not null, the user successfully signed in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

<span data-ttu-id="6003a-514">**bot/logoutDialog.js**</span><span class="sxs-lookup"><span data-stu-id="6003a-514">**bots/logoutDialog.js**</span></span>

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[<span data-ttu-id="6003a-515">Python</span><span class="sxs-lookup"><span data-stu-id="6003a-515">Python</span></span>](#tab/python-sample)

<span data-ttu-id="6003a-516">**bot/dialog_bot py**</span><span class="sxs-lookup"><span data-stu-id="6003a-516">**bots/dialog_bot.py**</span></span>

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

<span data-ttu-id="6003a-517">**bot/teams_bot py**</span><span class="sxs-lookup"><span data-stu-id="6003a-517">**bots/teams_bot.py**</span></span>

<span data-ttu-id="6003a-518">如果使用了**OAuthPrompt** ，则必须将*调用活动*转发到对话框。</span><span class="sxs-lookup"><span data-stu-id="6003a-518">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

<span data-ttu-id="6003a-519">**对话框/main_dialog py**</span><span class="sxs-lookup"><span data-stu-id="6003a-519">**dialogs/main_dialog.py**</span></span>

<span data-ttu-id="6003a-520">在对话步骤中，使用 `begin_dialog` "" 启动 OAuth 提示，这将要求用户登录。</span><span class="sxs-lookup"><span data-stu-id="6003a-520">Within a dialog step, use `begin_dialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="6003a-521">如果用户已登录，则会生成令牌响应事件，而不会提示用户。</span><span class="sxs-lookup"><span data-stu-id="6003a-521">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="6003a-522">否则，这将提示用户登录。</span><span class="sxs-lookup"><span data-stu-id="6003a-522">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="6003a-523">Azure Bot 服务在用户尝试登录后发送令牌响应事件。</span><span class="sxs-lookup"><span data-stu-id="6003a-523">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

<span data-ttu-id="6003a-524">在下面的对话框步骤中，检查上一步的结果中是否存在令牌。</span><span class="sxs-lookup"><span data-stu-id="6003a-524">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="6003a-525">如果不为 null，则用户已成功登录。</span><span class="sxs-lookup"><span data-stu-id="6003a-525">If it is not null, the user successfully signed in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

<span data-ttu-id="6003a-526">**对话框/logout_dialog py**</span><span class="sxs-lookup"><span data-stu-id="6003a-526">**dialogs/logout_dialog.py**</span></span>

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

> [!div class="nextstepaction"]
> [<span data-ttu-id="6003a-527">了解如何通过 Azure Bot 服务添加身份验证</span><span class="sxs-lookup"><span data-stu-id="6003a-527">Learn about adding adding authentication via Azure Bot Service</span></span>](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: https://docs.microsoft.com/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0
[concept-state]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0
[concept-dialogs]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0
[simple-dialog]: https://docs.microsoft.com/azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0

[teams-auth-bot-cs]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[teams-auth-bot-js]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth

[azure-aad-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview
[aad-registration-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview
