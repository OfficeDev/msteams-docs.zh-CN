---
title: 向自动程序Teams身份验证
author: surbhigupta
description: 如何将 OAuth 身份验证添加到自动程序Microsoft Teams。
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 3e36d6166dcf3f835252fb2310b6672cb115d7d4
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069015"
---
# <a name="add-authentication-to-your-teams-bot"></a><span data-ttu-id="61974-103">向自动程序Teams身份验证</span><span class="sxs-lookup"><span data-stu-id="61974-103">Add authentication to your Teams bot</span></span>

<span data-ttu-id="61974-104">有时可能需要在可代表用户Microsoft Teams访问资源（如邮件服务）的聊天机器人。</span><span class="sxs-lookup"><span data-stu-id="61974-104">There are times when you may need to create bots in Microsoft Teams that can access resources on behalf of the user, such as a mail service.</span></span>

<span data-ttu-id="61974-105">本文演示如何使用基于 OAuth 2.0 的 Azure Bot Service v4 SDK 身份验证。</span><span class="sxs-lookup"><span data-stu-id="61974-105">This article demonstrates how to use Azure Bot Service v4 SDK authentication, based on OAuth 2.0.</span></span> <span data-ttu-id="61974-106">这使得开发能够基于用户凭据使用身份验证令牌的自动程序变得更简单。</span><span class="sxs-lookup"><span data-stu-id="61974-106">This makes it easier to develop a bot that can use authentication tokens based on the user's credentials.</span></span> <span data-ttu-id="61974-107">所有这一切的关键是使用标识 **提供程序**，我们将在稍后看到。</span><span class="sxs-lookup"><span data-stu-id="61974-107">Key in all this is the use of **identity providers**, as we will see later.</span></span>

<span data-ttu-id="61974-108">OAuth 2.0 是 Azure Active Directory (Azure AD) 和许多其他身份标识提供程序用于身份验证和授权的开放标准。</span><span class="sxs-lookup"><span data-stu-id="61974-108">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="61974-109">对 OAuth 2.0 有基本的了解是在 Teams 中进行身份验证的先决条件。</span><span class="sxs-lookup"><span data-stu-id="61974-109">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

<span data-ttu-id="61974-110">有关[完整规范，请参阅 OAuth 2 Simplified](https://aka.ms/oauth2-simplified)了解基本信息，请参阅[OAuth 2.0。](https://oauth.net/2/)</span><span class="sxs-lookup"><span data-stu-id="61974-110">See [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) for a basic understanding, and [OAuth 2.0](https://oauth.net/2/) for the complete specification.</span></span>

<span data-ttu-id="61974-111">有关 Azure Bot 服务如何处理身份验证的信息，请参阅对话 [中的用户身份验证](https://aka.ms/azure-bot-authentication)。</span><span class="sxs-lookup"><span data-stu-id="61974-111">For more information about how the Azure Bot Service handles authentication, see [User authentication within a conversation](https://aka.ms/azure-bot-authentication).</span></span>

<span data-ttu-id="61974-112">在本文中，您将了解：</span><span class="sxs-lookup"><span data-stu-id="61974-112">In this article you'll learn:</span></span>

- <span data-ttu-id="61974-113">**如何创建启用身份验证的机器人**。</span><span class="sxs-lookup"><span data-stu-id="61974-113">**How to create an authentication-enabled bot**.</span></span> <span data-ttu-id="61974-114">你将使用 [cs-auth-sample][teams-auth-bot-cs] 来处理用户登录凭据和生成身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="61974-114">You'll use [cs-auth-sample][teams-auth-bot-cs] to handle user sign-in credentials and the generating the authentication token.</span></span>
- <span data-ttu-id="61974-115">**如何将机器人部署到 Azure 并将其与标识提供程序关联**。</span><span class="sxs-lookup"><span data-stu-id="61974-115">**How to deploy the bot to Azure and associate it with an identity provider**.</span></span> <span data-ttu-id="61974-116">提供程序根据用户登录凭据颁发令牌。</span><span class="sxs-lookup"><span data-stu-id="61974-116">The provider issues a token based on user sign-in credentials.</span></span> <span data-ttu-id="61974-117">机器人可以使用令牌访问需要身份验证的资源，如邮件服务。</span><span class="sxs-lookup"><span data-stu-id="61974-117">The bot can use the token to access resources, such as a mail service, which require authentication.</span></span> <span data-ttu-id="61974-118">有关详细信息，请参阅[Microsoft Teams的身份验证流](auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="61974-118">For more information see  [Microsoft Teams authentication flow for bots](auth-flow-bot.md).</span></span>
- <span data-ttu-id="61974-119">**如何将自动程序集成到 Microsoft Teams。**</span><span class="sxs-lookup"><span data-stu-id="61974-119">**How to integrate the bot within Microsoft Teams**.</span></span> <span data-ttu-id="61974-120">集成自动程序后，可以在聊天中登录并交换消息。</span><span class="sxs-lookup"><span data-stu-id="61974-120">Once the bot has been integrated, you can sign in and exchange messages with it in a chat.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61974-121">先决条件</span><span class="sxs-lookup"><span data-stu-id="61974-121">Prerequisites</span></span>

- <span data-ttu-id="61974-122">了解[自动程序基础知识][concept-basics][、管理状态][concept-state][、对话框库][concept-dialogs]以及如何[实现顺序对话流][simple-dialog]。</span><span class="sxs-lookup"><span data-stu-id="61974-122">Knowledge of [bot basics][concept-basics], [managing state][concept-state], the [dialogs library][concept-dialogs], and how to [implement sequential conversation flow][simple-dialog].</span></span>
- <span data-ttu-id="61974-123">了解 Azure 和 OAuth 2.0 开发。</span><span class="sxs-lookup"><span data-stu-id="61974-123">Knowledge of Azure and OAuth 2.0 development.</span></span>
- <span data-ttu-id="61974-124">当前版本的 Visual Studio 和 Git。</span><span class="sxs-lookup"><span data-stu-id="61974-124">The current versions of Visual Studio and Git.</span></span>
- <span data-ttu-id="61974-125">Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="61974-125">Azure account.</span></span> <span data-ttu-id="61974-126">如果需要，你可以创建 Azure [免费帐户](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="61974-126">If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="61974-127">以下示例：</span><span class="sxs-lookup"><span data-stu-id="61974-127">The following sample:</span></span>

    | <span data-ttu-id="61974-128">示例</span><span class="sxs-lookup"><span data-stu-id="61974-128">Sample</span></span> | <span data-ttu-id="61974-129">BotBuilder 版本</span><span class="sxs-lookup"><span data-stu-id="61974-129">BotBuilder version</span></span> | <span data-ttu-id="61974-130">演示</span><span class="sxs-lookup"><span data-stu-id="61974-130">Demonstrates</span></span> |
    |:---|:---:|:---|
    | <span data-ttu-id="61974-131"> [cs-auth-sample 中的自动程序身份验证][teams-auth-bot-cs]</span><span class="sxs-lookup"><span data-stu-id="61974-131">**Bot authentication** in [cs-auth-sample][teams-auth-bot-cs]</span></span> | <span data-ttu-id="61974-132">v4</span><span class="sxs-lookup"><span data-stu-id="61974-132">v4</span></span> | <span data-ttu-id="61974-133">OAuthCard 支持</span><span class="sxs-lookup"><span data-stu-id="61974-133">OAuthCard support</span></span> |
    | <span data-ttu-id="61974-134"> [js-auth-sample 中的自动程序身份验证][teams-auth-bot-js]</span><span class="sxs-lookup"><span data-stu-id="61974-134">**Bot authentication** in [js-auth-sample][teams-auth-bot-js]</span></span> | <span data-ttu-id="61974-135">v4</span><span class="sxs-lookup"><span data-stu-id="61974-135">v4</span></span>| <span data-ttu-id="61974-136">OAuthCard 支持</span><span class="sxs-lookup"><span data-stu-id="61974-136">OAuthCard support</span></span>  |
    | <span data-ttu-id="61974-137"> [py-auth-sample 中的自动程序身份验证][teams-auth-bot-py]</span><span class="sxs-lookup"><span data-stu-id="61974-137">**Bot authentication** in [py-auth-sample][teams-auth-bot-py]</span></span> | <span data-ttu-id="61974-138">v4</span><span class="sxs-lookup"><span data-stu-id="61974-138">v4</span></span> | <span data-ttu-id="61974-139">OAuthCard 支持</span><span class="sxs-lookup"><span data-stu-id="61974-139">OAuthCard support</span></span> |

## <a name="create-the-resource-group"></a><span data-ttu-id="61974-140">创建资源组</span><span class="sxs-lookup"><span data-stu-id="61974-140">Create the resource group</span></span>

<span data-ttu-id="61974-141">资源组和服务计划并非严格必需的，但它们允许您便捷地释放您创建的资源。</span><span class="sxs-lookup"><span data-stu-id="61974-141">The resource group and the service plan aren't strictly necessary, but they allow you to conveniently release the resources you create.</span></span> <span data-ttu-id="61974-142">这是保持资源有序且易于管理的良好做法。</span><span class="sxs-lookup"><span data-stu-id="61974-142">This is good practice for keeping your resources organized and manageable.</span></span>

<span data-ttu-id="61974-143">使用资源组为 Bot Framework 创建单个资源。</span><span class="sxs-lookup"><span data-stu-id="61974-143">You use a resource group to create individual resources for the Bot Framework.</span></span> <span data-ttu-id="61974-144">为了提高性能，请确保这些资源位于同一 Azure 区域。</span><span class="sxs-lookup"><span data-stu-id="61974-144">For performance, ensure that these resources are located in the same Azure region.</span></span>

1. <span data-ttu-id="61974-145">在浏览器中，登录到 Azure [**门户**][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="61974-145">In your browser, sign into the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="61974-146">在左侧导航面板中，选择"**资源组"。**</span><span class="sxs-lookup"><span data-stu-id="61974-146">In the left navigation panel, select **Resource groups**.</span></span>
1. <span data-ttu-id="61974-147">在显示窗口的左上角，选择" **添加** "选项卡以创建新的资源组。</span><span class="sxs-lookup"><span data-stu-id="61974-147">In the upper left of the displayed window, select **Add** tab to create a new resource group.</span></span> <span data-ttu-id="61974-148">系统将提示你提供以下内容：</span><span class="sxs-lookup"><span data-stu-id="61974-148">You'll be prompted to provide the following:</span></span>
    1. <span data-ttu-id="61974-149">**订阅**。</span><span class="sxs-lookup"><span data-stu-id="61974-149">**Subscription**.</span></span> <span data-ttu-id="61974-150">使用现有订阅。</span><span class="sxs-lookup"><span data-stu-id="61974-150">Use your existing subscription.</span></span>
    1. <span data-ttu-id="61974-151">**资源组**。</span><span class="sxs-lookup"><span data-stu-id="61974-151">**Resource group**.</span></span> <span data-ttu-id="61974-152">输入资源组的名称。</span><span class="sxs-lookup"><span data-stu-id="61974-152">Enter the name for the resource group.</span></span> <span data-ttu-id="61974-153">例如  *，TeamsResourceGroup*。</span><span class="sxs-lookup"><span data-stu-id="61974-153">An example could be  *TeamsResourceGroup*.</span></span> <span data-ttu-id="61974-154">请记住，该名称必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="61974-154">Remember that the name must be unique.</span></span>
    1. <span data-ttu-id="61974-155">从" **区域** "下拉菜单中，选择" *美国* 西部"或靠近应用程序的区域。</span><span class="sxs-lookup"><span data-stu-id="61974-155">From the **Region** drop-down menu, select *West US*, or a region close to your applications.</span></span>
    1. <span data-ttu-id="61974-156">选择" **审阅并创建"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="61974-156">Select the **Review and create** button.</span></span> <span data-ttu-id="61974-157">你应该会看到一个横幅，显示 *"验证通过"。*</span><span class="sxs-lookup"><span data-stu-id="61974-157">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="61974-158">选择" **创建"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="61974-158">Select the **Create** button.</span></span> <span data-ttu-id="61974-159">可能需要几分钟时间才能创建资源组。</span><span class="sxs-lookup"><span data-stu-id="61974-159">It may take a few minutes to create the resource group.</span></span>

> [!TIP]
> <span data-ttu-id="61974-160">与本教程稍后将创建的资源一样，建议将此资源组固定到仪表板以轻松访问。</span><span class="sxs-lookup"><span data-stu-id="61974-160">As with the resources you'll create later in this tutorial, it's a good idea to pin this resource group to your dashboard for easy access.</span></span> <span data-ttu-id="61974-161">如果你希望这样做，请选择固定图标&#128204;位于仪表板的右上角。</span><span class="sxs-lookup"><span data-stu-id="61974-161">If you'd like to do so, select the pin icon &#128204; in the upper right of the dashboard.</span></span>

## <a name="create-the-service-plan"></a><span data-ttu-id="61974-162">创建服务计划</span><span class="sxs-lookup"><span data-stu-id="61974-162">Create the service plan</span></span>

1. <span data-ttu-id="61974-163">在 [**Azure 门户的**][azure-portal]左侧导航面板上，选择"**创建资源"。**</span><span class="sxs-lookup"><span data-stu-id="61974-163">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="61974-164">在搜索框中，键入 *应用服务计划*。</span><span class="sxs-lookup"><span data-stu-id="61974-164">In the search box, type *App Service Plan*.</span></span> <span data-ttu-id="61974-165">从 **搜索结果中选择"应用** 服务计划"卡。</span><span class="sxs-lookup"><span data-stu-id="61974-165">Select the **App Service Plan** card from the search results.</span></span>
1. <span data-ttu-id="61974-166">选择 **创建**。</span><span class="sxs-lookup"><span data-stu-id="61974-166">Select **Create**.</span></span>
1. <span data-ttu-id="61974-167">将要求您提供以下信息：</span><span class="sxs-lookup"><span data-stu-id="61974-167">You'll be asked to provide the following information:</span></span>
    1. <span data-ttu-id="61974-168">**订阅**。</span><span class="sxs-lookup"><span data-stu-id="61974-168">**Subscription**.</span></span> <span data-ttu-id="61974-169">可以使用现有订阅。</span><span class="sxs-lookup"><span data-stu-id="61974-169">You can use an existing subscription.</span></span>
    1. <span data-ttu-id="61974-170">**资源组**。</span><span class="sxs-lookup"><span data-stu-id="61974-170">**Resource Group**.</span></span> <span data-ttu-id="61974-171">选择之前创建的组。</span><span class="sxs-lookup"><span data-stu-id="61974-171">Select the group you created earlier.</span></span>
    1. <span data-ttu-id="61974-172">**名称**。</span><span class="sxs-lookup"><span data-stu-id="61974-172">**Name**.</span></span> <span data-ttu-id="61974-173">输入服务计划的名称。</span><span class="sxs-lookup"><span data-stu-id="61974-173">Enter the name for the service plan.</span></span> <span data-ttu-id="61974-174">例如  *，TeamsServicePlan*。</span><span class="sxs-lookup"><span data-stu-id="61974-174">An example could be  *TeamsServicePlan*.</span></span> <span data-ttu-id="61974-175">请记住，该名称在组内必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="61974-175">Remember that the name must be unique, within the group.</span></span>
    1. <span data-ttu-id="61974-176">**操作系统**。</span><span class="sxs-lookup"><span data-stu-id="61974-176">**Operating System**.</span></span> <span data-ttu-id="61974-177">选择 *Windows* 或适用的操作系统。</span><span class="sxs-lookup"><span data-stu-id="61974-177">Select *Windows* or your applicable OS.</span></span>
    1. <span data-ttu-id="61974-178">**区域**。</span><span class="sxs-lookup"><span data-stu-id="61974-178">**Region**.</span></span> <span data-ttu-id="61974-179">选择 *"美国* 西部"或"靠近你的应用程序的区域"。</span><span class="sxs-lookup"><span data-stu-id="61974-179">Select *West US* or a region close to your applications.</span></span>
    1. <span data-ttu-id="61974-180">**定价层**。</span><span class="sxs-lookup"><span data-stu-id="61974-180">**Pricing Tier**.</span></span> <span data-ttu-id="61974-181">确保选中 *"标准 S1"。*</span><span class="sxs-lookup"><span data-stu-id="61974-181">Make sure that *Standard S1* is selected.</span></span> <span data-ttu-id="61974-182">此值应为默认值。</span><span class="sxs-lookup"><span data-stu-id="61974-182">This should be the default value.</span></span>
    1. <span data-ttu-id="61974-183">选择" **审阅并创建"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="61974-183">Select the **Review and create** button.</span></span> <span data-ttu-id="61974-184">你应该会看到一个横幅，显示 *"验证通过"。*</span><span class="sxs-lookup"><span data-stu-id="61974-184">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="61974-185">选择 **创建**。</span><span class="sxs-lookup"><span data-stu-id="61974-185">Select **Create**.</span></span> <span data-ttu-id="61974-186">创建应用服务计划可能需要几分钟时间。</span><span class="sxs-lookup"><span data-stu-id="61974-186">It may take a few minutes to create the app service plan.</span></span> <span data-ttu-id="61974-187">计划将在资源组中列出。</span><span class="sxs-lookup"><span data-stu-id="61974-187">The plan will be listed in the resource group.</span></span>

## <a name="create-the-bot-channels-registration"></a><span data-ttu-id="61974-188">创建自动程序通道注册</span><span class="sxs-lookup"><span data-stu-id="61974-188">Create the bot channels registration</span></span>

<span data-ttu-id="61974-189">自动程序通道注册将你的 Web 服务注册为 Bot Framework 的自动程序，只要你拥有 Microsoft 应用 ID 和应用密码 (客户端密码) 。</span><span class="sxs-lookup"><span data-stu-id="61974-189">The bot channels registration registers your web service as a bot with the Bot Framework, provided you have a Microsoft App Id and App password (client secret).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61974-190">如果你的机器人未托管在 Azure 中，则只需注册它。</span><span class="sxs-lookup"><span data-stu-id="61974-190">You only need to register your bot if it is not hosted in Azure.</span></span> <span data-ttu-id="61974-191">如果你通过 Azure [门户](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) 创建了自动程序，则它已在服务中注册。</span><span class="sxs-lookup"><span data-stu-id="61974-191">If you [created a bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) through the Azure portal then it is already registered with the service.</span></span> <span data-ttu-id="61974-192">如果你通过 Bot [Framework](https://dev.botframework.com/bots/new) 或 [AppStudio](~/concepts/build-and-test/app-studio-overview.md) 创建了自动程序，你的机器人不会在 Azure 中注册。</span><span class="sxs-lookup"><span data-stu-id="61974-192">If you created your bot through the [Bot Framework](https://dev.botframework.com/bots/new) or [AppStudio](~/concepts/build-and-test/app-studio-overview.md) your bot isn't registered in Azure.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

> [!NOTE]
> <span data-ttu-id="61974-193">Bot Channels Registration 资源将显示 **全局区域** ，即使你选择了美国西部。</span><span class="sxs-lookup"><span data-stu-id="61974-193">The Bot Channels Registration resource will show the **Global** region even if you selected West US.</span></span> <span data-ttu-id="61974-194">这是预期结果。</span><span class="sxs-lookup"><span data-stu-id="61974-194">This is expected.</span></span>

<span data-ttu-id="61974-195">有关详细信息，请参阅为用户[创建自动程序Teams。](../create-a-bot-for-teams.md)</span><span class="sxs-lookup"><span data-stu-id="61974-195">For more information, see [Create a bot for Teams](../create-a-bot-for-teams.md).</span></span>

## <a name="create-the-identity-provider"></a><span data-ttu-id="61974-196">创建标识提供程序</span><span class="sxs-lookup"><span data-stu-id="61974-196">Create the identity provider</span></span>

<span data-ttu-id="61974-197">您需要一个可用于身份验证的标识提供程序。</span><span class="sxs-lookup"><span data-stu-id="61974-197">You need an identity provider that can be used for authentication.</span></span>
<span data-ttu-id="61974-198">在此过程中，你将使用 Azure AD 提供程序;其他 Azure AD 支持的标识提供程序也可使用。</span><span class="sxs-lookup"><span data-stu-id="61974-198">In this procedure you'll use an Azure AD provider; other Azure AD supported identity providers can also be used.</span></span>

1. <span data-ttu-id="61974-199">在 [**Azure 门户的**][azure-portal]左侧导航面板上，选择 **"Azure Active Directory"。**</span><span class="sxs-lookup"><span data-stu-id="61974-199">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Azure Active Directory**.</span></span>
    > [!TIP]
    > <span data-ttu-id="61974-200">你需要在租户中创建和注册此 Azure AD 资源，你可以同意委派应用程序请求的权限。</span><span class="sxs-lookup"><span data-stu-id="61974-200">You'll need to create and register this Azure AD resource in a tenant in which you can consent to delegate permissions requested by an application.</span></span>
    > <span data-ttu-id="61974-201">有关创建租户的说明，请参阅 [访问门户并创建租户](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)。</span><span class="sxs-lookup"><span data-stu-id="61974-201">For instruction on creating a tenant, see [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span></span>
1. <span data-ttu-id="61974-202">在左侧面板中，选择 **"应用注册"。**</span><span class="sxs-lookup"><span data-stu-id="61974-202">In the left panel, select **App registrations**.</span></span>
1. <span data-ttu-id="61974-203">在右侧面板中，选择左上角 **的** "新建注册"选项卡。</span><span class="sxs-lookup"><span data-stu-id="61974-203">In the right panel, select the **New registration** tab, in the upper left.</span></span>
1. <span data-ttu-id="61974-204">将要求您提供以下信息：</span><span class="sxs-lookup"><span data-stu-id="61974-204">You'll be asked to provide the following information:</span></span>
   1. <span data-ttu-id="61974-205">**名称**。</span><span class="sxs-lookup"><span data-stu-id="61974-205">**Name**.</span></span> <span data-ttu-id="61974-206">输入应用程序的名称。</span><span class="sxs-lookup"><span data-stu-id="61974-206">Enter the name for the application.</span></span> <span data-ttu-id="61974-207">例如  *，BotTeamsIdentity*。</span><span class="sxs-lookup"><span data-stu-id="61974-207">An example could be  *BotTeamsIdentity*.</span></span> <span data-ttu-id="61974-208">请记住，该名称必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="61974-208">Remember that the name must be unique.</span></span>
   1. <span data-ttu-id="61974-209">选择 **应用程序支持** 的帐户类型。</span><span class="sxs-lookup"><span data-stu-id="61974-209">Select the **Supported account types** for your application.</span></span> <span data-ttu-id="61974-210">选择任何组织目录中的帐户 (任何 Azure AD 目录 - 多租户) 和个人 Microsoft 帐户 *(例如 Skype、Xbox) 。*</span><span class="sxs-lookup"><span data-stu-id="61974-210">Select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
   1. <span data-ttu-id="61974-211">对于 **重定向 URI：**</span><span class="sxs-lookup"><span data-stu-id="61974-211">For the **Redirect URI**:</span></span><br/>
       <span data-ttu-id="61974-212">&#x2713;选择 **Web。**</span><span class="sxs-lookup"><span data-stu-id="61974-212">&#x2713;Select **Web**.</span></span> <br/>
       <span data-ttu-id="61974-213">&#x2713;将 URL 设置为 `https://token.botframework.com/.auth/web/redirect` 。</span><span class="sxs-lookup"><span data-stu-id="61974-213">&#x2713; Set the URL to `https://token.botframework.com/.auth/web/redirect`.</span></span>
   1. <span data-ttu-id="61974-214">选择“**注册**”。</span><span class="sxs-lookup"><span data-stu-id="61974-214">Select **Register**.</span></span>

1. <span data-ttu-id="61974-215">创建后，Azure 将显示 **应用的"** 概述"页。</span><span class="sxs-lookup"><span data-stu-id="61974-215">Once it is created, Azure displays the **Overview** page for the app.</span></span> <span data-ttu-id="61974-216">将以下信息复制并保存到文件中：</span><span class="sxs-lookup"><span data-stu-id="61974-216">Copy and save the following information to a file:</span></span>

    1. <span data-ttu-id="61974-217">Application **(客户端) ID** 值。</span><span class="sxs-lookup"><span data-stu-id="61974-217">The **Application (client) ID** value.</span></span> <span data-ttu-id="61974-218">稍后在自动程序中注册此 Azure标识应用程序时，将此值用作客户端 ID。</span><span class="sxs-lookup"><span data-stu-id="61974-218">You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.</span></span>
    1. <span data-ttu-id="61974-219">租户 **的 (ID) ID** 值。</span><span class="sxs-lookup"><span data-stu-id="61974-219">The **Directory (tenant) ID** value.</span></span> <span data-ttu-id="61974-220">稍后，你还将使用此值作为 *租户 ID，* 向自动程序注册此 Azure 标识应用程序。</span><span class="sxs-lookup"><span data-stu-id="61974-220">You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.</span></span>

1. <span data-ttu-id="61974-221">在左侧面板中， **选择** "&密码"，为应用程序创建客户端密码。</span><span class="sxs-lookup"><span data-stu-id="61974-221">In the left panel, select **Certificates & secrets** to create a client secret for your application.</span></span>

   1. <span data-ttu-id="61974-222">在 **"客户端密码**"下 **，&#x2795;"新建客户端密码"。**</span><span class="sxs-lookup"><span data-stu-id="61974-222">Under **Client secrets**, select &#x2795; **New client secret**.</span></span>
   1. <span data-ttu-id="61974-223">添加描述以从可能需要为此应用创建的其他人（例如，Teams 中的自动程序 *标识应用）标识此Teams。*</span><span class="sxs-lookup"><span data-stu-id="61974-223">Add a description to identify this secret from others you might need to create for this app, such as *Bot identity app in Teams*.</span></span>
   1. <span data-ttu-id="61974-224">设置 **到期** 到你的选择。</span><span class="sxs-lookup"><span data-stu-id="61974-224">Set **Expires** to your selection.</span></span>
   1. <span data-ttu-id="61974-225">选择“**添加**”。</span><span class="sxs-lookup"><span data-stu-id="61974-225">Select **Add**.</span></span>
   1. <span data-ttu-id="61974-226">在离开此页面之前， **请记录密码**。</span><span class="sxs-lookup"><span data-stu-id="61974-226">Before leaving this page, **record the secret**.</span></span> <span data-ttu-id="61974-227">稍后，当你向自动程序注册 Azure  AD 应用程序时，你将使用此值作为客户端密码。</span><span class="sxs-lookup"><span data-stu-id="61974-227">You'll use this value later as the _Client secret_ when you register your Azure AD application with your bot.</span></span>

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a><span data-ttu-id="61974-228">配置标识提供程序连接，然后向自动程序注册该连接</span><span class="sxs-lookup"><span data-stu-id="61974-228">Configure the identity provider connection and register it with the bot</span></span>

<span data-ttu-id="61974-229">注意-此处有两个适用于服务提供商的选项-Azure AD V1 和 Azure AD V2。</span><span class="sxs-lookup"><span data-stu-id="61974-229">Note-there are two options for Service Providers here-Azure AD V1 and Azure AD V2.</span></span>  <span data-ttu-id="61974-230">此处总结了两个提供程序之间的差异，但通常[](/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison)V2 在更改自动程序权限方面提供了更大的灵活性。</span><span class="sxs-lookup"><span data-stu-id="61974-230">The differences between the two providers are summarized [here](/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison), but in general, V2 provides more flexibility with respect to changing bot permissions.</span></span>  <span data-ttu-id="61974-231">GraphAPI 权限在范围字段中列出，当添加新权限时，自动程序将允许用户在下次登录时同意新权限。</span><span class="sxs-lookup"><span data-stu-id="61974-231">Graph API permissions are listed in the scopes field, and as new ones are added, bots will allow users to consent to the new permissions on the next sign in.</span></span>  <span data-ttu-id="61974-232">对于 V1，用户必须删除自动程序同意，才能在 OAuth 对话框中提示新权限。</span><span class="sxs-lookup"><span data-stu-id="61974-232">For V1, the bot consent must be deleted by the user for new permissions to be prompted in the OAuth dialog.</span></span> 

#### <a name="azure-ad-v1"></a><span data-ttu-id="61974-233">Azure AD V1</span><span class="sxs-lookup"><span data-stu-id="61974-233">Azure AD V1</span></span>

1. <span data-ttu-id="61974-234">在 [**Azure 门户中**][azure-portal]，从仪表板中选择资源组。</span><span class="sxs-lookup"><span data-stu-id="61974-234">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="61974-235">选择自动程序通道注册链接。</span><span class="sxs-lookup"><span data-stu-id="61974-235">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="61974-236">打开资源页，**然后选择"配置\*\*\*\*"设置。**</span><span class="sxs-lookup"><span data-stu-id="61974-236">Open the resource page and select **Configuration** under **Settings**.</span></span> 
1. <span data-ttu-id="61974-237">选择 **"添加 OAuth 连接设置"。**</span><span class="sxs-lookup"><span data-stu-id="61974-237">Select **Add OAuth Connection Settings**.</span></span>    
<span data-ttu-id="61974-238">下图显示了资源页中的相应选择：</span><span class="sxs-lookup"><span data-stu-id="61974-238">The following image displays the corresponding selection in the resource page:</span></span>  
<span data-ttu-id="61974-239">![SampleAppDemoBot 配置](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span><span class="sxs-lookup"><span data-stu-id="61974-239">![SampleAppDemoBot configuration](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span></span>
1. <span data-ttu-id="61974-240">如下所示完成表单：</span><span class="sxs-lookup"><span data-stu-id="61974-240">Complete the form as follows:</span></span>

    1. <span data-ttu-id="61974-241">**名称**。</span><span class="sxs-lookup"><span data-stu-id="61974-241">**Name**.</span></span> <span data-ttu-id="61974-242">输入连接的名称。</span><span class="sxs-lookup"><span data-stu-id="61974-242">Enter a name for the connection.</span></span> <span data-ttu-id="61974-243">你将在文件的自动程序中使用此 `appsettings.json` 名称。</span><span class="sxs-lookup"><span data-stu-id="61974-243">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="61974-244">例如 *BotTeamsAuthADv1*。</span><span class="sxs-lookup"><span data-stu-id="61974-244">For example *BotTeamsAuthADv1*.</span></span>
    1. <span data-ttu-id="61974-245">**服务提供程序**。</span><span class="sxs-lookup"><span data-stu-id="61974-245">**Service Provider**.</span></span> <span data-ttu-id="61974-246">选择 **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="61974-246">Select **Azure Active Directory**.</span></span> <span data-ttu-id="61974-247">选择此选项后，将显示特定于 Azure AD 的字段。</span><span class="sxs-lookup"><span data-stu-id="61974-247">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="61974-248">**客户端 ID**。在以上 (中) 为 Azure 标识提供程序应用记录的应用程序客户端标识 ID。</span><span class="sxs-lookup"><span data-stu-id="61974-248">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="61974-249">**客户端密码**。</span><span class="sxs-lookup"><span data-stu-id="61974-249">**Client secret**.</span></span> <span data-ttu-id="61974-250">在以上步骤中输入为 Azure 标识提供程序应用记录机密。</span><span class="sxs-lookup"><span data-stu-id="61974-250">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="61974-251">**授予类型**。</span><span class="sxs-lookup"><span data-stu-id="61974-251">**Grant Type**.</span></span> <span data-ttu-id="61974-252">输入 `authorization_code` 。</span><span class="sxs-lookup"><span data-stu-id="61974-252">Enter `authorization_code`.</span></span>
    1. <span data-ttu-id="61974-253">**登录 URL**。</span><span class="sxs-lookup"><span data-stu-id="61974-253">**Login URL**.</span></span> <span data-ttu-id="61974-254">输入 `https://login.microsoftonline.com` 。</span><span class="sxs-lookup"><span data-stu-id="61974-254">Enter `https://login.microsoftonline.com`.</span></span>
    1. <span data-ttu-id="61974-255">**"租户 ID"， (** 之前为 Azure 标识应用录制的目录或租户) ID，具体取决于创建标识提供程序应用时选择的支持的帐户类型。 </span><span class="sxs-lookup"><span data-stu-id="61974-255">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="61974-256">要决定要分配的值，请遵循以下条件：</span><span class="sxs-lookup"><span data-stu-id="61974-256">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="61974-257">如果你选择了仅 *(Microsoft* 组织目录中的帐户 - 单租户) 或任何组织目录 (*Microsoft AAD* 目录 - 多租户) 请输入之前为 AAD 应用记录的租户 **ID。**</span><span class="sxs-lookup"><span data-stu-id="61974-257">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="61974-258">这将是与可以进行身份验证的用户关联的租户。</span><span class="sxs-lookup"><span data-stu-id="61974-258">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="61974-259">如果在任意组织目录中选择了"帐户 (任何 AAD 目录 - 多租户和个人 Microsoft 帐户（例如 *Skype、Xbox）Outlook)* 输入 common 一词，而不是租户ID。</span><span class="sxs-lookup"><span data-stu-id="61974-259">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="61974-260">否则，AAD 应用会通过已选择 ID 的租户进行验证，并排除个人 Microsoft 帐户。</span><span class="sxs-lookup"><span data-stu-id="61974-260">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    <span data-ttu-id="61974-261">h.</span><span class="sxs-lookup"><span data-stu-id="61974-261">h.</span></span> <span data-ttu-id="61974-262">对于 **"资源 URL"，** 输入 `https://graph.microsoft.com/` 。</span><span class="sxs-lookup"><span data-stu-id="61974-262">For **Resource URL**, enter `https://graph.microsoft.com/`.</span></span> <span data-ttu-id="61974-263">当前代码示例中没有使用此功能。</span><span class="sxs-lookup"><span data-stu-id="61974-263">This is not used in the current code sample.</span></span>  
    <span data-ttu-id="61974-264">i.</span><span class="sxs-lookup"><span data-stu-id="61974-264">i.</span></span> <span data-ttu-id="61974-265">将 **"范围"** 留空。</span><span class="sxs-lookup"><span data-stu-id="61974-265">Leave **Scopes** blank.</span></span> <span data-ttu-id="61974-266">下图是一个示例：</span><span class="sxs-lookup"><span data-stu-id="61974-266">The following image is an example:</span></span>

    ![teams 自动程序应用程序身份验证连接字符串 adv1 视图](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. <span data-ttu-id="61974-268">选择“**保存**”。</span><span class="sxs-lookup"><span data-stu-id="61974-268">Select **Save**.</span></span>

#### <a name="azure-ad-v2"></a><span data-ttu-id="61974-269">Azure AD V2</span><span class="sxs-lookup"><span data-stu-id="61974-269">Azure AD V2</span></span>

1. <span data-ttu-id="61974-270">在 [**Azure 门户中**][azure-portal]，从仪表板中选择资源组。</span><span class="sxs-lookup"><span data-stu-id="61974-270">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="61974-271">选择自动程序通道注册链接。</span><span class="sxs-lookup"><span data-stu-id="61974-271">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="61974-272">打开资源页，**然后选择"配置\*\*\*\*"设置。**</span><span class="sxs-lookup"><span data-stu-id="61974-272">Open the resource page and select **Configuration** under **Settings**.</span></span> 
1. <span data-ttu-id="61974-273">选择 **"添加 OAuth 连接设置"。**</span><span class="sxs-lookup"><span data-stu-id="61974-273">Select **Add OAuth Connection Settings**.</span></span>  
<span data-ttu-id="61974-274">下图显示了资源页中的相应选择：</span><span class="sxs-lookup"><span data-stu-id="61974-274">The following image displays the corresponding selection in the resource page:</span></span>        
<span data-ttu-id="61974-275">![SampleAppDemoBot 配置](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span><span class="sxs-lookup"><span data-stu-id="61974-275">![SampleAppDemoBot Configuration](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span></span> 

1. <span data-ttu-id="61974-276">如下所示完成表单：</span><span class="sxs-lookup"><span data-stu-id="61974-276">Complete the form as follows:</span></span>

    1. <span data-ttu-id="61974-277">**名称**。</span><span class="sxs-lookup"><span data-stu-id="61974-277">**Name**.</span></span> <span data-ttu-id="61974-278">输入连接的名称。</span><span class="sxs-lookup"><span data-stu-id="61974-278">Enter a name for the connection.</span></span> <span data-ttu-id="61974-279">你将在文件的自动程序中使用此 `appsettings.json` 名称。</span><span class="sxs-lookup"><span data-stu-id="61974-279">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="61974-280">例如 *BotTeamsAuthADv2*。</span><span class="sxs-lookup"><span data-stu-id="61974-280">For example *BotTeamsAuthADv2*.</span></span>
    1. <span data-ttu-id="61974-281">**服务提供程序**。</span><span class="sxs-lookup"><span data-stu-id="61974-281">**Service Provider**.</span></span> <span data-ttu-id="61974-282">选择 **"Azure Active Directory v2"。**</span><span class="sxs-lookup"><span data-stu-id="61974-282">Select **Azure Active Directory v2**.</span></span> <span data-ttu-id="61974-283">选择此选项后，将显示特定于 Azure AD 的字段。</span><span class="sxs-lookup"><span data-stu-id="61974-283">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="61974-284">**客户端 ID**。在以上 (中) 为 Azure 标识提供程序应用记录的应用程序客户端标识 ID。</span><span class="sxs-lookup"><span data-stu-id="61974-284">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="61974-285">**客户端密码**。</span><span class="sxs-lookup"><span data-stu-id="61974-285">**Client secret**.</span></span> <span data-ttu-id="61974-286">在以上步骤中输入为 Azure 标识提供程序应用记录机密。</span><span class="sxs-lookup"><span data-stu-id="61974-286">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="61974-287">**令牌Exchange URL**。</span><span class="sxs-lookup"><span data-stu-id="61974-287">**Token Exchange URL**.</span></span> <span data-ttu-id="61974-288">保留此为空白。</span><span class="sxs-lookup"><span data-stu-id="61974-288">Leave this blank.</span></span>
    1. <span data-ttu-id="61974-289">**"租户 ID"， (** 之前为 Azure 标识应用录制的目录或租户) ID，具体取决于创建标识提供程序应用时选择的支持的帐户类型。 </span><span class="sxs-lookup"><span data-stu-id="61974-289">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="61974-290">要决定要分配的值，请遵循以下条件：</span><span class="sxs-lookup"><span data-stu-id="61974-290">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="61974-291">如果你选择了仅 *(Microsoft* 组织目录中的帐户 - 单租户) 或任何组织目录 (*Microsoft AAD* 目录 - 多租户) 请输入之前为 AAD 应用记录的租户 **ID。**</span><span class="sxs-lookup"><span data-stu-id="61974-291">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="61974-292">这将是与可以进行身份验证的用户关联的租户。</span><span class="sxs-lookup"><span data-stu-id="61974-292">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="61974-293">如果在任意组织目录中选择了"帐户 (任何 AAD 目录 - 多租户和个人 Microsoft 帐户（例如 *Skype、Xbox）Outlook)* 输入 common 一词，而不是租户ID。</span><span class="sxs-lookup"><span data-stu-id="61974-293">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="61974-294">否则，AAD 应用会通过已选择 ID 的租户进行验证，并排除个人 Microsoft 帐户。</span><span class="sxs-lookup"><span data-stu-id="61974-294">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    1. <span data-ttu-id="61974-295">对于 **Scopes，** 输入此应用程序所需的图形权限的空格分隔列表，例如：User.Read User.ReadBasic.All Mail.Read</span><span class="sxs-lookup"><span data-stu-id="61974-295">For **Scopes**, enter a space-delimited list of graph permissions this application requires e.g.: User.Read User.ReadBasic.All Mail.Read</span></span> 

1. <span data-ttu-id="61974-296">选择“**保存**”。</span><span class="sxs-lookup"><span data-stu-id="61974-296">Select **Save**.</span></span>

### <a name="test-the-connection"></a><span data-ttu-id="61974-297">测试连接</span><span class="sxs-lookup"><span data-stu-id="61974-297">Test the connection</span></span>

1. <span data-ttu-id="61974-298">选择连接条目以打开刚创建的连接。</span><span class="sxs-lookup"><span data-stu-id="61974-298">Select the connection entry to open the connection you just created.</span></span>
1. <span data-ttu-id="61974-299">选择 **"服务提供商** 连接设置"面板顶部的 **"测试连接** "。</span><span class="sxs-lookup"><span data-stu-id="61974-299">Select **Test Connection** at the top of the **Service Provider Connection Setting** panel.</span></span>
1. <span data-ttu-id="61974-300">第一次这样做时，将打开一个新的浏览器窗口，要求你选择帐户。</span><span class="sxs-lookup"><span data-stu-id="61974-300">The first time you do this will open a new browser window asking you to select an account.</span></span> <span data-ttu-id="61974-301">选择您想要使用的人。</span><span class="sxs-lookup"><span data-stu-id="61974-301">Select the one you want to use.</span></span>
1. <span data-ttu-id="61974-302">接下来，将要求你允许标识提供程序使用你的数据 (凭据) 。</span><span class="sxs-lookup"><span data-stu-id="61974-302">Next, you'll be asked to allow to the identity provider to use your data (credentials).</span></span> <span data-ttu-id="61974-303">下图是一个示例：</span><span class="sxs-lookup"><span data-stu-id="61974-303">The following image is an example:</span></span>

    ![teams 自动程序身份验证连接字符串 adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. <span data-ttu-id="61974-305">选择 **接受**。</span><span class="sxs-lookup"><span data-stu-id="61974-305">Select **Accept**.</span></span>
1. <span data-ttu-id="61974-306">然后，这会将您重定向到" **测试连接成功 \<your-connection-name> "** 页。</span><span class="sxs-lookup"><span data-stu-id="61974-306">This should then redirect you to a **Test Connection to \<your-connection-name> Succeeded** page.</span></span> <span data-ttu-id="61974-307">如果收到错误，请刷新页面。</span><span class="sxs-lookup"><span data-stu-id="61974-307">Refresh the page if you get an error.</span></span> <span data-ttu-id="61974-308">下图是一个示例：</span><span class="sxs-lookup"><span data-stu-id="61974-308">The following image is an example:</span></span>

    ![teams 自动程序应用程序身份验证连接 str adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

<span data-ttu-id="61974-310">自动程序代码使用连接名称检索用户身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="61974-310">The connection name is used by the bot code to retrieve user authentication tokens.</span></span>

## <a name="prepare-the-bot-sample-code"></a><span data-ttu-id="61974-311">准备自动程序示例代码</span><span class="sxs-lookup"><span data-stu-id="61974-311">Prepare the bot sample code</span></span>

<span data-ttu-id="61974-312">完成初步设置后，让我们着重介绍本文中要使用的机器人的创建。</span><span class="sxs-lookup"><span data-stu-id="61974-312">With the preliminary settings done, let's focus on the creation of the bot to use in this article.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="61974-313">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="61974-313">C#/.NET</span></span>](#tab/dotnet)

1. <span data-ttu-id="61974-314">克隆 [cs-auth-sample][teams-auth-bot-cs]。</span><span class="sxs-lookup"><span data-stu-id="61974-314">Clone [cs-auth-sample][teams-auth-bot-cs].</span></span>
1. <span data-ttu-id="61974-315">启动Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="61974-315">Launch Visual Studio.</span></span>
1. <span data-ttu-id="61974-316">从工具栏中选择文件 **-> 打开 -> Project/解决方案** 并打开自动程序项目。</span><span class="sxs-lookup"><span data-stu-id="61974-316">From the toolbar select **File -> Open -> Project/Solution** and open the bot project.</span></span>
1. <span data-ttu-id="61974-317">在C#更新 **appsettings.js如下所示** 打开：</span><span class="sxs-lookup"><span data-stu-id="61974-317">In C# Update **appsettings.json** as follows:</span></span>

    - <span data-ttu-id="61974-318">设置为 `ConnectionName` 添加到自动程序通道注册的标识提供程序连接的名称。</span><span class="sxs-lookup"><span data-stu-id="61974-318">Set `ConnectionName` to the name of the identity provider connection you added to the bot channel registration.</span></span> <span data-ttu-id="61974-319">此示例中使用的名称是 *BotTeamsAuthADv1*。</span><span class="sxs-lookup"><span data-stu-id="61974-319">The name we used in this example is *BotTeamsAuthADv1*.</span></span>
    - <span data-ttu-id="61974-320">设置为 `MicrosoftAppId` 在 **自动程序** 通道注册时保存的自动程序应用 ID。</span><span class="sxs-lookup"><span data-stu-id="61974-320">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="61974-321">设置为 `MicrosoftAppPassword` 在 **自动程序** 频道注册时保存的客户密码。</span><span class="sxs-lookup"><span data-stu-id="61974-321">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>

    <span data-ttu-id="61974-322">根据自动程序密码中的字符，可能需要对密码进行 XML 转义。</span><span class="sxs-lookup"><span data-stu-id="61974-322">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="61974-323">例如，任何与 (&) 需要编码为 `&amp;` 。</span><span class="sxs-lookup"><span data-stu-id="61974-323">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. <span data-ttu-id="61974-324">在"解决方案资源管理器"中，导航到文件夹，打开并设置 ，然后转到在自动程序通道注册时保存的 `TeamsAppManifest` `manifest.json` `id` `botId` 自动程序应用 ID。 </span><span class="sxs-lookup"><span data-stu-id="61974-324">In the Solution Explorer, navigate to the `TeamsAppManifest` folder, open `manifest.json` and set `id` and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="javascript"></a>[<span data-ttu-id="61974-325">JavaScript</span><span class="sxs-lookup"><span data-stu-id="61974-325">JavaScript</span></span>](#tab/node-js)

1. <span data-ttu-id="61974-326">克隆 [node-auth-sample][teams-auth-bot-js]。</span><span class="sxs-lookup"><span data-stu-id="61974-326">Clone [node-auth-sample][teams-auth-bot-js].</span></span>
1. <span data-ttu-id="61974-327">在控制台中，导航到项目：</span><span class="sxs-lookup"><span data-stu-id="61974-327">In a console, navigate to the project:</span></span> </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. <span data-ttu-id="61974-328">安装模块</span><span class="sxs-lookup"><span data-stu-id="61974-328">Install modules</span></span></br></br>
`npm install`
1. <span data-ttu-id="61974-329">更新 **.env** 配置，如下所示：</span><span class="sxs-lookup"><span data-stu-id="61974-329">Update the **.env** configuration as follows:</span></span>

    - <span data-ttu-id="61974-330">设置为 `MicrosoftAppId` 在 **自动程序** 通道注册时保存的自动程序应用 ID。</span><span class="sxs-lookup"><span data-stu-id="61974-330">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="61974-331">设置为 `MicrosoftAppPassword` 在 **自动程序** 频道注册时保存的客户密码。</span><span class="sxs-lookup"><span data-stu-id="61974-331">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="61974-332">将 `connectionName` 设置为标识提供程序连接的名称。</span><span class="sxs-lookup"><span data-stu-id="61974-332">Set the `connectionName` to the name of the identity provider connection.</span></span>
    <span data-ttu-id="61974-333">根据自动程序密码中的字符，可能需要对密码进行 XML 转义。</span><span class="sxs-lookup"><span data-stu-id="61974-333">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="61974-334">例如，任何与 (&) 需要编码为 `&amp;` 。</span><span class="sxs-lookup"><span data-stu-id="61974-334">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. <span data-ttu-id="61974-335">在文件夹中，打开并设置为 Microsoft 应用 ID 以及你在自动程序通道注册时保存的 `teamsAppManifest` `manifest.json` `id`  `botId` 自动程序应用ID。</span><span class="sxs-lookup"><span data-stu-id="61974-335">In the `teamsAppManifest` folder, open `manifest.json` and set `id`  to your **Microsoft App ID** and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="python"></a>[<span data-ttu-id="61974-336">Python</span><span class="sxs-lookup"><span data-stu-id="61974-336">Python</span></span>](#tab/python)

1. <span data-ttu-id="61974-337">从[github 存储库中克隆 py-auth-sample。][teams-auth-bot-py]</span><span class="sxs-lookup"><span data-stu-id="61974-337">Clone [py-auth-sample][teams-auth-bot-py] from the github repository.</span></span>
1. <span data-ttu-id="61974-338">更新 **config.py：**</span><span class="sxs-lookup"><span data-stu-id="61974-338">Update **config.py**:</span></span>

    - <span data-ttu-id="61974-339">设置为 `ConnectionName` 添加到自动程序中的 OAuth 连接设置的名称。</span><span class="sxs-lookup"><span data-stu-id="61974-339">Set `ConnectionName` to the name of the OAuth connection setting you added to your bot.</span></span>
    - <span data-ttu-id="61974-340">将 `MicrosoftAppId` 和 `MicrosoftAppPassword` 设置为自动程序的应用 ID 和应用密码。</span><span class="sxs-lookup"><span data-stu-id="61974-340">Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.</span></span>

      <span data-ttu-id="61974-341">根据自动程序密码中的字符，可能需要对密码进行 XML 转义。</span><span class="sxs-lookup"><span data-stu-id="61974-341">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="61974-342">例如，任何与 (&) 需要编码为 `&amp;` 。</span><span class="sxs-lookup"><span data-stu-id="61974-342">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="61974-343">将机器人部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="61974-343">Deploy the bot to Azure</span></span>

<span data-ttu-id="61974-344">若要部署机器人，请按照如何将机器人部署到 [Azure 中的步骤操作](https://aka.ms/azure-bot-deployment-cli)。</span><span class="sxs-lookup"><span data-stu-id="61974-344">To deploy the bot, follow the steps in the how to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span></span>

<span data-ttu-id="61974-345">或者，在Visual Studio时，可以执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="61974-345">Alternatively, while in Visual Studio, you can follow these steps:</span></span>

1. <span data-ttu-id="61974-346">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span><span class="sxs-lookup"><span data-stu-id="61974-346">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span></span>
1. <span data-ttu-id="61974-347">在下拉菜单中，选择"发布 **"。**</span><span class="sxs-lookup"><span data-stu-id="61974-347">In the drop-down menu, select **Publish**.</span></span>
1. <span data-ttu-id="61974-348">在显示的窗口中，选择"新建 **"** 链接。</span><span class="sxs-lookup"><span data-stu-id="61974-348">In the displayed window, select the **New** link.</span></span>
1. <span data-ttu-id="61974-349">在对话框窗口中，选择左侧 **的应用服务** ，在右侧 **选择新建** 。</span><span class="sxs-lookup"><span data-stu-id="61974-349">In the dialog window, select **App Service** on the left and **Create New** on the right.</span></span>
1. <span data-ttu-id="61974-350">选择" **发布"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="61974-350">Select the **Publish** button.</span></span>
1. <span data-ttu-id="61974-351">在下一个对话框窗口中，输入所需信息。</span><span class="sxs-lookup"><span data-stu-id="61974-351">In the next dialog window, enter the required information.</span></span> <span data-ttu-id="61974-352">示例如下：</span><span class="sxs-lookup"><span data-stu-id="61974-352">The following is an example:</span></span>

    ![auth-app-service](../../../assets/images/authentication/auth-bot-app-service.png)

1. <span data-ttu-id="61974-354">选择 **创建**。</span><span class="sxs-lookup"><span data-stu-id="61974-354">Select **Create**.</span></span>
1. <span data-ttu-id="61974-355">如果部署成功完成，则应该会看到部署Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="61974-355">If the deployment completes successfully, you should see it reflected in Visual Studio.</span></span> <span data-ttu-id="61974-356">此外，默认浏览器中会显示一个页面，*指出自动程序已准备就绪！。*</span><span class="sxs-lookup"><span data-stu-id="61974-356">Moreover, a page is displayed in your default browser saying *Your bot is ready!*.</span></span> <span data-ttu-id="61974-357">URL 将类似于 `https://botteamsauth.azurewebsites.net/` ：。</span><span class="sxs-lookup"><span data-stu-id="61974-357">The URL will be similar to this: `https://botteamsauth.azurewebsites.net/`.</span></span> <span data-ttu-id="61974-358">将其保存到文件中。</span><span class="sxs-lookup"><span data-stu-id="61974-358">Save it to a file.</span></span>
1. <span data-ttu-id="61974-359">在浏览器中，导航到 [**Azure 门户**][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="61974-359">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="61974-360">检查你的资源组，应列出自动程序以及其他资源。</span><span class="sxs-lookup"><span data-stu-id="61974-360">Check your resource group, the bot should be listed along with the other resources.</span></span> <span data-ttu-id="61974-361">下图是一个示例：</span><span class="sxs-lookup"><span data-stu-id="61974-361">The following image is an example:</span></span>

    ![teams-bot-auth-app-service-group](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. <span data-ttu-id="61974-363">在资源组中，选择自动程序通道注册 (链接) 。</span><span class="sxs-lookup"><span data-stu-id="61974-363">In the resource group, select the bot channel registration name (link).</span></span>
1. <span data-ttu-id="61974-364">在左侧面板中，选择 **"设置"。**</span><span class="sxs-lookup"><span data-stu-id="61974-364">In the left panel, select **Settings**.</span></span>
1. <span data-ttu-id="61974-365">在" **消息终结点** "框中，输入上面获得的 URL，后跟 `api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="61974-365">In the **Messaging endpoint** box, enter the URL obtained above followed by `api/messages`.</span></span> <span data-ttu-id="61974-366">这是一个示例 `https://botteamsauth.azurewebsites.net/api/messages` ：。</span><span class="sxs-lookup"><span data-stu-id="61974-366">This is an example: `https://botteamsauth.azurewebsites.net/api/messages`.</span></span>
1. <span data-ttu-id="61974-367">选择左上角 **的"** 保存"按钮。</span><span class="sxs-lookup"><span data-stu-id="61974-367">Select the **Save** button in the upper left.</span></span>

## <a name="test-the-bot-using-the-emulator"></a><span data-ttu-id="61974-368">使用自动程序测试Emulator</span><span class="sxs-lookup"><span data-stu-id="61974-368">Test the bot using the Emulator</span></span>

<span data-ttu-id="61974-369">如果尚未执行，请安装[Microsoft Bot Framework Emulator。](https://aka.ms/bot-framework-emulator-readme)</span><span class="sxs-lookup"><span data-stu-id="61974-369">If you haven't done it already, install the [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span></span> <span data-ttu-id="61974-370">另请参阅[使用 Emulator 调试](https://aka.ms/bot-framework-emulator-debug-with-emulator)。</span><span class="sxs-lookup"><span data-stu-id="61974-370">See also [Debug with the Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span></span>

<span data-ttu-id="61974-371">为了让机器人示例登录正常工作，你必须配置Emulator。</span><span class="sxs-lookup"><span data-stu-id="61974-371">In order for the bot sample login to work you must configure the Emulator.</span></span>

### <a name="configure-the-emulator-for-authentication"></a><span data-ttu-id="61974-372">配置Emulator身份验证策略</span><span class="sxs-lookup"><span data-stu-id="61974-372">Configure the Emulator for authentication</span></span>

<span data-ttu-id="61974-373">如果机器人需要身份验证，则必须配置Emulator。</span><span class="sxs-lookup"><span data-stu-id="61974-373">If a bot requires authentication, you must configure the Emulator.</span></span> <span data-ttu-id="61974-374">配置：</span><span class="sxs-lookup"><span data-stu-id="61974-374">To configure:</span></span>

1. <span data-ttu-id="61974-375">启动Emulator。</span><span class="sxs-lookup"><span data-stu-id="61974-375">Start the Emulator.</span></span>
1. <span data-ttu-id="61974-376">在Emulator中，选择&#9881;左下角的齿轮图标，或Emulator 设置右上角的"齿轮"选项卡。 </span><span class="sxs-lookup"><span data-stu-id="61974-376">In the Emulator, select the gear icon &#9881; in the bottom left, or the **Emulator Settings** tab in the upper right.</span></span>
1. <span data-ttu-id="61974-377">选中"使用 **版本 1.0 身份验证令牌"复选框**。</span><span class="sxs-lookup"><span data-stu-id="61974-377">Check the box by **Use version 1.0 authentication tokens**.</span></span>
1. <span data-ttu-id="61974-378">输入 **ngrok** 工具的本地路径。</span><span class="sxs-lookup"><span data-stu-id="61974-378">Enter the local path to the **ngrok** tool.</span></span> <span data-ttu-id="61974-379">*请参阅* Bot Framework Emulator /ngrok 隧道集成 [Wiki。](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok))</span><span class="sxs-lookup"><span data-stu-id="61974-379">*See* the Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span></span> <span data-ttu-id="61974-380">有关详细信息，请参阅 [ngrok](https://ngrok.com/)。</span><span class="sxs-lookup"><span data-stu-id="61974-380">For more tool information, see [ngrok](https://ngrok.com/).</span></span>
1. <span data-ttu-id="61974-381">选中在启动应用程序 **时运行 ngrok Emulator复选框**。</span><span class="sxs-lookup"><span data-stu-id="61974-381">Check the box by **Run ngrok when the Emulator starts up**.</span></span>
1. <span data-ttu-id="61974-382">选择" **保存"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="61974-382">Select the **Save** button.</span></span>

<span data-ttu-id="61974-383">当机器人显示登录卡并且用户选择登录按钮时，Emulator会打开一个页面，用户可使用该页面登录身份验证提供程序。</span><span class="sxs-lookup"><span data-stu-id="61974-383">When the bot displays a sign-in card and the user selects the sign-in button, the Emulator opens a page that the user can use to sign in with the authentication provider.</span></span>
<span data-ttu-id="61974-384">一旦用户这样做，提供程序将生成用户令牌并将其发送给机器人。</span><span class="sxs-lookup"><span data-stu-id="61974-384">Once the user does so, the provider generates a user token and sends it to the bot.</span></span> <span data-ttu-id="61974-385">之后，机器人可以代表用户操作。</span><span class="sxs-lookup"><span data-stu-id="61974-385">After that, the bot can act on behalf of the user.</span></span>

### <a name="test-the-bot-locally"></a><span data-ttu-id="61974-386">在本地测试机器人</span><span class="sxs-lookup"><span data-stu-id="61974-386">Test the bot locally</span></span>

<span data-ttu-id="61974-387">配置身份验证机制后，可以执行实际的自动程序测试。</span><span class="sxs-lookup"><span data-stu-id="61974-387">After you have configured the authentication mechanism, you can perform the actual bot testing.</span></span>  

1. <span data-ttu-id="61974-388">例如，通过 Visual Studio计算机上本地运行自动程序示例。</span><span class="sxs-lookup"><span data-stu-id="61974-388">Run the bot sample locally on your machine, via Visual Studio for example.</span></span>
1. <span data-ttu-id="61974-389">启动Emulator。</span><span class="sxs-lookup"><span data-stu-id="61974-389">Start the Emulator.</span></span>
1. <span data-ttu-id="61974-390">选择" **打开自动程序"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="61974-390">Select the **Open bot** button.</span></span>
1. <span data-ttu-id="61974-391">在自动 **程序 URL** 中，输入机器人的本地 URL。</span><span class="sxs-lookup"><span data-stu-id="61974-391">In the **Bot URL**, enter the bot's local URL.</span></span> <span data-ttu-id="61974-392">通常为 `http://localhost:3978/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="61974-392">Usually, `http://localhost:3978/api/messages`.</span></span>
1. <span data-ttu-id="61974-393">在 **Microsoft 应用 ID 中** ，从 输入机器人的应用 `appsettings.json` ID。</span><span class="sxs-lookup"><span data-stu-id="61974-393">In the **Microsoft App ID** enter the bot's app ID from `appsettings.json`.</span></span>
1. <span data-ttu-id="61974-394">在 **Microsoft 应用密码中** ，从 输入自动程序的应用密码 `appsettings.json` 。</span><span class="sxs-lookup"><span data-stu-id="61974-394">In the **Microsoft App password** enter the bot's app password from the `appsettings.json`.</span></span>
1. <span data-ttu-id="61974-395">选择 **"连接"。**</span><span class="sxs-lookup"><span data-stu-id="61974-395">Select **Connect**.</span></span>
1. <span data-ttu-id="61974-396">启动并运行自动程序后，输入任何文本以显示登录卡。</span><span class="sxs-lookup"><span data-stu-id="61974-396">After the bot is up and running, enter any text to display the sign-in card.</span></span>
1. <span data-ttu-id="61974-397">选择" **登录"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="61974-397">Select the **Sign in** button.</span></span>
1. <span data-ttu-id="61974-398">将显示一个弹出对话框以确认打开 **URL。**</span><span class="sxs-lookup"><span data-stu-id="61974-398">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="61974-399">这是为了允许自动程序的用户 () 进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="61974-399">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="61974-400">选择“**确认**”。</span><span class="sxs-lookup"><span data-stu-id="61974-400">Select **Confirm**.</span></span>
1. <span data-ttu-id="61974-401">如果系统询问，请选择适用的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="61974-401">If asked, select the applicable user's account.</span></span>
1. <span data-ttu-id="61974-402">根据用于测试Emulator，您将获得以下选项之一：</span><span class="sxs-lookup"><span data-stu-id="61974-402">Depending which configuration you used for the Emulator, you get one of the following:</span></span>
    1. <span data-ttu-id="61974-403">**使用登录验证码**</span><span class="sxs-lookup"><span data-stu-id="61974-403">**Using sign-in verification code**</span></span>  
      <span data-ttu-id="61974-404">&#x2713;打开一个显示验证代码的窗口。</span><span class="sxs-lookup"><span data-stu-id="61974-404">&#x2713; A window is opened displaying the validation code.</span></span>  
      <span data-ttu-id="61974-405">&#x2713;将验证代码复制并输入到聊天框中以完成登录。</span><span class="sxs-lookup"><span data-stu-id="61974-405">&#x2713; Copy and enter the validation code into the chat box to complete the sign-in.</span></span>
    1. <span data-ttu-id="61974-406">**使用身份验证令牌**。</span><span class="sxs-lookup"><span data-stu-id="61974-406">**Using authentication tokens**.</span></span>  
      <span data-ttu-id="61974-407">&#x2713;基于凭据登录。</span><span class="sxs-lookup"><span data-stu-id="61974-407">&#x2713; You're logged in based on your credentials.</span></span>

    <span data-ttu-id="61974-408">下图是登录后自动程序 UI 的一个示例：</span><span class="sxs-lookup"><span data-stu-id="61974-408">The following image is an example of the bot UI after you've logged in:</span></span>

    ![身份验证机器人登录仿真器](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. <span data-ttu-id="61974-410">如果在机器人 **询问"** 是否要查看令牌？"时选择"是 *"，* 你得到的响应如下所示：</span><span class="sxs-lookup"><span data-stu-id="61974-410">If you select **Yes** when the bot asks *Would you like to view your token?*, you'll get a response similar to the following:</span></span>

    ![身份验证机器人登录仿真器令牌](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. <span data-ttu-id="61974-412">在 **输入聊天** 框中输入注销以注销。这将释放用户令牌，在重新登录之前，自动程序将无法代表你操作。</span><span class="sxs-lookup"><span data-stu-id="61974-412">Enter **logout** in the input chat box to sign out. This releases the user token, and the bot won't be able to act on your behalf until you sign in again.</span></span>

> [!NOTE]
> <span data-ttu-id="61974-413">自动程序身份验证需要使用 **Bot 连接器服务**。</span><span class="sxs-lookup"><span data-stu-id="61974-413">Bot authentication requires use of the **Bot Connector Service**.</span></span> <span data-ttu-id="61974-414">该服务访问自动程序的自动程序通道注册信息。</span><span class="sxs-lookup"><span data-stu-id="61974-414">The service accesses the bot channels registration information for your bot.</span></span>

## <a name="test-the-deployed-bot"></a><span data-ttu-id="61974-415">测试已部署的自动程序</span><span class="sxs-lookup"><span data-stu-id="61974-415">Test the deployed bot</span></span>

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. <span data-ttu-id="61974-416">在浏览器中，导航到 [**Azure 门户**][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="61974-416">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="61974-417">查找资源组。</span><span class="sxs-lookup"><span data-stu-id="61974-417">Find your resource group.</span></span>
1. <span data-ttu-id="61974-418">选择资源链接。</span><span class="sxs-lookup"><span data-stu-id="61974-418">Select the resource link.</span></span> <span data-ttu-id="61974-419">将显示资源页。</span><span class="sxs-lookup"><span data-stu-id="61974-419">The resource page is displayed.</span></span>
1. <span data-ttu-id="61974-420">在资源页中，选择"**在 Web 聊天中测试"。**</span><span class="sxs-lookup"><span data-stu-id="61974-420">In the resource page, select **Test in Web Chat**.</span></span> <span data-ttu-id="61974-421">自动程序启动并显示预定义的问候语。</span><span class="sxs-lookup"><span data-stu-id="61974-421">The bot starts and displays the predefined greetings.</span></span>
1. <span data-ttu-id="61974-422">在聊天框中键入任何内容。</span><span class="sxs-lookup"><span data-stu-id="61974-422">Type anything in the chat box.</span></span>
1. <span data-ttu-id="61974-423">选中 **"登录"** 框。</span><span class="sxs-lookup"><span data-stu-id="61974-423">Select the **Sign in** box.</span></span>
1. <span data-ttu-id="61974-424">将显示一个弹出对话框以确认打开 **URL。**</span><span class="sxs-lookup"><span data-stu-id="61974-424">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="61974-425">这是为了允许自动程序的用户 () 进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="61974-425">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="61974-426">选择“**确认**”。</span><span class="sxs-lookup"><span data-stu-id="61974-426">Select **Confirm**.</span></span>
1. <span data-ttu-id="61974-427">如果系统询问，请选择适用的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="61974-427">If asked, select the applicable user's account.</span></span>
    <span data-ttu-id="61974-428">下图是登录后自动程序 UI 的示例：</span><span class="sxs-lookup"><span data-stu-id="61974-428">The following image is an example of the bot UI after you have logged in:</span></span>

    ![已部署身份验证机器人登录](../../../assets/images/authentication/auth-bot-login-deployed.PNG)<span data-ttu-id="61974-430">.</span><span class="sxs-lookup"><span data-stu-id="61974-430">.</span></span>

1. <span data-ttu-id="61974-431">选择" **是"** 按钮以显示身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="61974-431">Select the **Yes** button to display your authentication token.</span></span> <span data-ttu-id="61974-432">下图是一个示例：</span><span class="sxs-lookup"><span data-stu-id="61974-432">The following image is an example:</span></span>

    ![身份验证机器人登录部署的令牌](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG)<span data-ttu-id="61974-434">.</span><span class="sxs-lookup"><span data-stu-id="61974-434">.</span></span>

1. <span data-ttu-id="61974-435">输入注销以注销。</span><span class="sxs-lookup"><span data-stu-id="61974-435">Enter logout to sign out.</span></span>

    ![身份验证机器人部署的注销](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> <span data-ttu-id="61974-437">如果登录时遇到问题，请尝试再次测试连接，如前面的步骤中所述。</span><span class="sxs-lookup"><span data-stu-id="61974-437">If you're having problems signing in, try to test the connection again as described in the previous steps.</span></span> <span data-ttu-id="61974-438">这可重新创建身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="61974-438">This could recreate the authentication token.</span></span>
> <span data-ttu-id="61974-439">使用 Azure 中的 Bot Framework Web Chat 客户端，可能需要多次登录，然后才能正确建立身份验证。</span><span class="sxs-lookup"><span data-stu-id="61974-439">With the Bot Framework Web Chat client in Azure, you may need to sign in several times before the authentication is established correctly.</span></span>

## <a name="install-and-test-the-bot-in-teams"></a><span data-ttu-id="61974-440">安装并测试自动程序Teams</span><span class="sxs-lookup"><span data-stu-id="61974-440">Install and test the bot in Teams</span></span>

1. <span data-ttu-id="61974-441">在自动程序项目中，确保 `TeamsAppManifest` 文件夹包含 以及 `manifest.json` 和 `outline.png` `color.png` 文件。</span><span class="sxs-lookup"><span data-stu-id="61974-441">In your bot project, ensure that the `TeamsAppManifest` folder contains the `manifest.json` along with an `outline.png` and `color.png` files.</span></span>
1. <span data-ttu-id="61974-442">在"解决方案资源管理器"中，导航到 `TeamsAppManifest` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="61974-442">In Solution Explorer, navigate to the `TeamsAppManifest` folder.</span></span> <span data-ttu-id="61974-443">通过 `manifest.json` 分配以下值进行编辑：</span><span class="sxs-lookup"><span data-stu-id="61974-443">Edit `manifest.json` by assigning the following values:</span></span>
    1. <span data-ttu-id="61974-444">确保将 **你在自动** 程序通道注册时收到的自动程序应用 ID 分配给 `id` 和 `botId` 。</span><span class="sxs-lookup"><span data-stu-id="61974-444">Ensure that the **bot App ID** you received at the time of the bot channel registration is assigned to `id` and `botId`.</span></span>
    1. <span data-ttu-id="61974-445">分配此值 `validDomains: [ "token.botframework.com" ]` ：。</span><span class="sxs-lookup"><span data-stu-id="61974-445">Assign this value: `validDomains: [ "token.botframework.com" ]`.</span></span>
1. <span data-ttu-id="61974-446">选择 并 **压缩** `manifest.json` 、 和 `outline.png` `color.png` 文件。</span><span class="sxs-lookup"><span data-stu-id="61974-446">Select and **zip** the `manifest.json`, `outline.png`, and `color.png` files.</span></span>
1. <span data-ttu-id="61974-447">打开 **Microsoft Teams**。</span><span class="sxs-lookup"><span data-stu-id="61974-447">Open **Microsoft Teams**.</span></span>
1. <span data-ttu-id="61974-448">在左侧面板的底部，选择应用 **图标**。</span><span class="sxs-lookup"><span data-stu-id="61974-448">In the left panel, at the bottom, select the **Apps icon**.</span></span>
1. <span data-ttu-id="61974-449">在右侧面板的底部，选择 **"Upload应用"。**</span><span class="sxs-lookup"><span data-stu-id="61974-449">In the right panel, at the bottom, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="61974-450">导航到 `TeamsAppManifest` 文件夹并上载压缩的清单。</span><span class="sxs-lookup"><span data-stu-id="61974-450">Navigate to the `TeamsAppManifest` folder and upload the zipped manifest.</span></span>
<span data-ttu-id="61974-451">将显示以下向导：</span><span class="sxs-lookup"><span data-stu-id="61974-451">The following wizard is displayed:</span></span>

    ![身份验证机器人团队上传](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. <span data-ttu-id="61974-453">选择“**添加到团队**”按钮。</span><span class="sxs-lookup"><span data-stu-id="61974-453">Select the **Add to a team** button.</span></span>
1. <span data-ttu-id="61974-454">In the next window， select the team where you want to use the bot.</span><span class="sxs-lookup"><span data-stu-id="61974-454">In the next window, select the team where you want to use the bot.</span></span>
1. <span data-ttu-id="61974-455">选择" **设置自动程序"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="61974-455">Select the **Set up a bot** button.</span></span>
1. <span data-ttu-id="61974-456">选择左面板 (&#x25cf;&#x25cf;&#x25cf;) 三个点。</span><span class="sxs-lookup"><span data-stu-id="61974-456">Select the three dots (&#x25cf;&#x25cf;&#x25cf;) in the left panel.</span></span> <span data-ttu-id="61974-457">然后选择 **App Studio** 图标。</span><span class="sxs-lookup"><span data-stu-id="61974-457">Then select the **App Studio** icon.</span></span>
1. <span data-ttu-id="61974-458">选择清单 **编辑器** 选项卡。你应该会看到上传的自动程序图标。</span><span class="sxs-lookup"><span data-stu-id="61974-458">Select the **Manifest editor** tab. You should see the icon for the bot you uploaded.</span></span>
1. <span data-ttu-id="61974-459">此外，你应该能够看到聊天列表中列为联系人的聊天机器人，可用于与聊天机器人交换消息。</span><span class="sxs-lookup"><span data-stu-id="61974-459">Also, you should be able to see the bot listed as a contact in the chat list that you can use to exchange messages with the bot.</span></span>

### <a name="testing-the-bot-locally-in-teams"></a><span data-ttu-id="61974-460">在本地测试聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="61974-460">Testing the bot locally in Teams</span></span>

<span data-ttu-id="61974-461">Microsoft Teams完全基于云的产品，它要求它访问的所有服务都使用 HTTPS 终结点从云中提供。</span><span class="sxs-lookup"><span data-stu-id="61974-461">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="61974-462">因此，若要使自动程序 (我们的示例) 在 Teams 中工作，你需要将代码发布到你选择的云，或通过隧道工具使本地运行的实例可从外部访问。 </span><span class="sxs-lookup"><span data-stu-id="61974-462">Therefore, to enable the bot (our sample) to work in Teams, you need to either publish the code to the cloud of your choice, or make a locally running instance externally accessible via a **tunneling** tool.</span></span> <span data-ttu-id="61974-463">我们建议  [使用 ngrok，](https://ngrok.com/download)这将为计算机上本地打开的端口创建一个外部可地址 URL。</span><span class="sxs-lookup"><span data-stu-id="61974-463">We recommend  [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span>
<span data-ttu-id="61974-464">若要设置 ngrok 以准备在本地运行 Microsoft Teams 应用，请按照以下步骤操作：</span><span class="sxs-lookup"><span data-stu-id="61974-464">To set up ngrok in preparation for running your Microsoft Teams app locally, follow these steps:</span></span>

1. <span data-ttu-id="61974-465">在终端窗口中，转到已安装的 `ngrok.exe` 目录。</span><span class="sxs-lookup"><span data-stu-id="61974-465">In a terminal window, go the directory where you have `ngrok.exe` installed.</span></span> <span data-ttu-id="61974-466">我们建议将 *环境变量* 路径设置为指向该路径。</span><span class="sxs-lookup"><span data-stu-id="61974-466">We suggest setting the *environment variable* path to point to it.</span></span>
1. <span data-ttu-id="61974-467">运行，例如 `ngrok http 3978 --host-header=localhost:3978` ， 。</span><span class="sxs-lookup"><span data-stu-id="61974-467">Run, for example, `ngrok http 3978 --host-header=localhost:3978`.</span></span> <span data-ttu-id="61974-468">根据需要替换端口号。</span><span class="sxs-lookup"><span data-stu-id="61974-468">Replace the port number as needed.</span></span>
<span data-ttu-id="61974-469">这将启动 ngrok 以侦听你指定的端口。</span><span class="sxs-lookup"><span data-stu-id="61974-469">This launches ngrok to listen on the port you specify.</span></span> <span data-ttu-id="61974-470">作为返回，它会为你提供一个外部可地址 URL，只要 ngrok 正在运行，该 URL 就有效。</span><span class="sxs-lookup"><span data-stu-id="61974-470">In return, it gives you an externally addressable URL, valid for as long as ngrok is running.</span></span> <span data-ttu-id="61974-471">下图是一个示例：</span><span class="sxs-lookup"><span data-stu-id="61974-471">The following image is an example:</span></span>

    ![teams 自动程序应用程序身份验证连接字符串 adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG)<span data-ttu-id="61974-473">.</span><span class="sxs-lookup"><span data-stu-id="61974-473">.</span></span>

1. <span data-ttu-id="61974-474">复制转发 HTTPS 地址。</span><span class="sxs-lookup"><span data-stu-id="61974-474">Copy the forwarding HTTPS address.</span></span> <span data-ttu-id="61974-475">它应类似于以下内容 `https://dea822bf.ngrok.io/` ：。</span><span class="sxs-lookup"><span data-stu-id="61974-475">It should be similar to the following: `https://dea822bf.ngrok.io/`.</span></span>
1. <span data-ttu-id="61974-476">Append `/api/messages` 以获取 `https://dea822bf.ngrok.io/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="61974-476">Append `/api/messages` to obtain `https://dea822bf.ngrok.io/api/messages`.</span></span> <span data-ttu-id="61974-477">这是自动 **程序** 在计算机本地运行的消息终结点，在 Microsoft Teams 聊天中可Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="61974-477">This is the **messages endpoint** for the bot running locally on your machine and reachable over the web in a chat in Microsoft Teams.</span></span>
1. <span data-ttu-id="61974-478">要执行的最后一步是更新已部署机器人的消息终结点。</span><span class="sxs-lookup"><span data-stu-id="61974-478">One final step to perform is to update the messages endpoint of the deployed bot.</span></span> <span data-ttu-id="61974-479">在示例中，我们在 Azure 中部署了机器人。</span><span class="sxs-lookup"><span data-stu-id="61974-479">In the example, we deployed the bot in Azure.</span></span> <span data-ttu-id="61974-480">因此，让我们执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="61974-480">So \*\*let's perform these steps:</span></span>
    1. <span data-ttu-id="61974-481">在浏览器中导航到 [**Azure 门户**][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="61974-481">In your browser navigate to the [**Azure portal**][azure-portal].</span></span>
    1. <span data-ttu-id="61974-482">选择自动 **程序频道注册**。</span><span class="sxs-lookup"><span data-stu-id="61974-482">Select your **Bot Channel Registration**.</span></span>
    1. <span data-ttu-id="61974-483">在左侧面板中，选择 **"设置"。**</span><span class="sxs-lookup"><span data-stu-id="61974-483">In the left panel, select **Settings**.</span></span>
    1. <span data-ttu-id="61974-484">在右侧面板的"消息 **终结点** "框中，输入 ngrok URL，在我们的示例中为 `https://dea822bf.ngrok.io/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="61974-484">In the right panel, in the **Messaging endpoint** box, enter the ngrok URL, in our example, `https://dea822bf.ngrok.io/api/messages`.</span></span>
1. <span data-ttu-id="61974-485">在本地启动自动程序，例如，在Visual Studio模式下。</span><span class="sxs-lookup"><span data-stu-id="61974-485">Start your bot locally, for example in Visual Studio debug mode.</span></span>
1. <span data-ttu-id="61974-486">使用 Bot Framework 门户的测试 Web 聊天在本地运行时 **测试机器人**。</span><span class="sxs-lookup"><span data-stu-id="61974-486">Test the bot while running locally using the Bot Framework portal's **Test Web chat**.</span></span> <span data-ttu-id="61974-487">与Emulator一样，此测试不允许你Teams特定功能。</span><span class="sxs-lookup"><span data-stu-id="61974-487">Like the Emulator, this test doesn't allow you to access Teams-specific functionality.</span></span>
1. <span data-ttu-id="61974-488">在运行的终端窗口中，你可以看到自动程序与 Web 聊天客户端之间的 `ngrok` HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="61974-488">In the terminal window where `ngrok` is running you can see HTTP traffic between the bot and the web chat client.</span></span> <span data-ttu-id="61974-489">如果需要更详细的视图，请在浏览器窗口中输入从上一个终端 `http://127.0.0.1:4040` 窗口获取的视图。</span><span class="sxs-lookup"><span data-stu-id="61974-489">If you want a more detailed view, in a browser window enter `http://127.0.0.1:4040` you obtained from the previous terminal window.</span></span> <span data-ttu-id="61974-490">下图是一个示例：</span><span class="sxs-lookup"><span data-stu-id="61974-490">The following image is an example:</span></span>

    ![身份验证机器人团队 ngrok 测试](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png)<span data-ttu-id="61974-492">.</span><span class="sxs-lookup"><span data-stu-id="61974-492">.</span></span>

> [!NOTE]
> <span data-ttu-id="61974-493">如果停止并重新启动 ngrok，URL 将发生更改。</span><span class="sxs-lookup"><span data-stu-id="61974-493">If you stop and restart ngrok, the URL changes.</span></span> <span data-ttu-id="61974-494">若要在项目中使用 ngrok，并且根据您使用的功能，您必须更新所有 URL 引用。</span><span class="sxs-lookup"><span data-stu-id="61974-494">To use ngrok in your project, and depending on the capabilities you're using, you must update all URL references.</span></span>
 

## <a name="additional-information"></a><span data-ttu-id="61974-495">其他信息</span><span class="sxs-lookup"><span data-stu-id="61974-495">Additional information</span></span>

### <a name="teamsappmanifestmanifestjson"></a><span data-ttu-id="61974-496">TeamsAppManifest/manifest.js打开</span><span class="sxs-lookup"><span data-stu-id="61974-496">TeamsAppManifest/manifest.json</span></span>

<span data-ttu-id="61974-497">此清单包含用户Microsoft Teams自动程序连接时需要的信息：</span><span class="sxs-lookup"><span data-stu-id="61974-497">This manifest contains information needed by Microsoft Teams to connect with the bot:</span></span>  

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
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

<span data-ttu-id="61974-498">使用身份验证Teams与其他通道的行为稍有不同，如下所述。</span><span class="sxs-lookup"><span data-stu-id="61974-498">With authentication, Teams behaves slightly differently than other channels, as explained below.</span></span>

### <a name="handling-invoke-activity"></a><span data-ttu-id="61974-499">处理调用活动</span><span class="sxs-lookup"><span data-stu-id="61974-499">Handling Invoke Activity</span></span>

<span data-ttu-id="61974-500">将 **Invoke 活动** 发送到机器人，而不是其他频道使用的事件活动。</span><span class="sxs-lookup"><span data-stu-id="61974-500">An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.</span></span>
<span data-ttu-id="61974-501">这是通过对 **ActivityHandler 进行子类化完成**。</span><span class="sxs-lookup"><span data-stu-id="61974-501">This is done by sub-classing the **ActivityHandler**.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="61974-502">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="61974-502">C#/.NET</span></span>](#tab/dotnet-sample)

<span data-ttu-id="61974-503">**Bots/DialogBot.cs**</span><span class="sxs-lookup"><span data-stu-id="61974-503">**Bots/DialogBot.cs**</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

<span data-ttu-id="61974-504">**Bots/TeamsBot.cs**</span><span class="sxs-lookup"><span data-stu-id="61974-504">**Bots/TeamsBot.cs**</span></span>

<span data-ttu-id="61974-505">如果使用 **OAuthPrompt，** 则必须将 Invoke 活动转发到对话框。 </span><span class="sxs-lookup"><span data-stu-id="61974-505">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a><span data-ttu-id="61974-506">TeamsActivityHandler.cs</span><span class="sxs-lookup"><span data-stu-id="61974-506">TeamsActivityHandler.cs</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="61974-507">JavaScript</span><span class="sxs-lookup"><span data-stu-id="61974-507">JavaScript</span></span>](#tab/node-js-dialog-sample)

<span data-ttu-id="61974-508">**bots/dialogBot.js**</span><span class="sxs-lookup"><span data-stu-id="61974-508">**bots/dialogBot.js**</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

<span data-ttu-id="61974-509">**bots/teamsBot.js**</span><span class="sxs-lookup"><span data-stu-id="61974-509">**bots/teamsBot.js**</span></span>

<span data-ttu-id="61974-510">如果使用 **OAuthPrompt，** 则必须将 Invoke 活动转发到对话框。 </span><span class="sxs-lookup"><span data-stu-id="61974-510">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

<span data-ttu-id="61974-511">**dialogs/mainDialog.js**</span><span class="sxs-lookup"><span data-stu-id="61974-511">**dialogs/mainDialog.js**</span></span>

<span data-ttu-id="61974-512">在对话框步骤中， `beginDialog` 使用 启动 OAuth 提示，该提示要求用户登录。</span><span class="sxs-lookup"><span data-stu-id="61974-512">Within a dialog step, use `beginDialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="61974-513">如果用户已登录，这将生成令牌响应事件，而不会提示用户。</span><span class="sxs-lookup"><span data-stu-id="61974-513">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="61974-514">否则，将提示用户登录。</span><span class="sxs-lookup"><span data-stu-id="61974-514">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="61974-515">Azure Bot 服务在用户尝试登录后发送令牌响应事件。</span><span class="sxs-lookup"><span data-stu-id="61974-515">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

<span data-ttu-id="61974-516">在下面的对话框步骤中，检查上一步的结果中是否存在令牌。</span><span class="sxs-lookup"><span data-stu-id="61974-516">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="61974-517">如果不是 null，则用户已成功登录。</span><span class="sxs-lookup"><span data-stu-id="61974-517">If it is not null, the user successfully signed in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

<span data-ttu-id="61974-518">**bots/logoutDialog.js**</span><span class="sxs-lookup"><span data-stu-id="61974-518">**bots/logoutDialog.js**</span></span>

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[<span data-ttu-id="61974-519">Python</span><span class="sxs-lookup"><span data-stu-id="61974-519">Python</span></span>](#tab/python-sample)

<span data-ttu-id="61974-520">**bots/dialog_bot.py**</span><span class="sxs-lookup"><span data-stu-id="61974-520">**bots/dialog_bot.py**</span></span>

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

<span data-ttu-id="61974-521">**bots/teams_bot.py**</span><span class="sxs-lookup"><span data-stu-id="61974-521">**bots/teams_bot.py**</span></span>

<span data-ttu-id="61974-522">如果使用 **OAuthPrompt，** 则必须将 Invoke 活动转发到对话框。 </span><span class="sxs-lookup"><span data-stu-id="61974-522">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

<span data-ttu-id="61974-523">**dialogs/main_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="61974-523">**dialogs/main_dialog.py**</span></span>

<span data-ttu-id="61974-524">在对话框步骤中， `begin_dialog` 使用 启动 OAuth 提示，该提示要求用户登录。</span><span class="sxs-lookup"><span data-stu-id="61974-524">Within a dialog step, use `begin_dialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="61974-525">如果用户已登录，这将生成令牌响应事件，而不会提示用户。</span><span class="sxs-lookup"><span data-stu-id="61974-525">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="61974-526">否则，将提示用户登录。</span><span class="sxs-lookup"><span data-stu-id="61974-526">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="61974-527">Azure Bot 服务在用户尝试登录后发送令牌响应事件。</span><span class="sxs-lookup"><span data-stu-id="61974-527">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

<span data-ttu-id="61974-528">在下面的对话框步骤中，检查上一步的结果中是否存在令牌。</span><span class="sxs-lookup"><span data-stu-id="61974-528">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="61974-529">如果不是 null，则用户已成功登录。</span><span class="sxs-lookup"><span data-stu-id="61974-529">If it is not null, the user successfully signed in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

<span data-ttu-id="61974-530">**dialogs/logout_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="61974-530">**dialogs/logout_dialog.py**</span></span>

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

## <a name="see-also"></a><span data-ttu-id="61974-531">另请参阅</span><span class="sxs-lookup"><span data-stu-id="61974-531">See also</span></span>

[<span data-ttu-id="61974-532">通过 Azure Bot 服务添加身份验证</span><span class="sxs-lookup"><span data-stu-id="61974-532">Add authentication through Azure Bot Service</span></span>](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: /azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true
[concept-state]: /azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0&preserve-view=true
[concept-dialogs]: /azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0&preserve-view=true
[simple-dialog]: /azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0&preserve-view=true

[teams-auth-bot-cs]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[teams-auth-bot-js]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth

[azure-aad-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview
[aad-registration-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview
