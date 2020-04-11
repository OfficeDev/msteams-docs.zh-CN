---
title: 向你的团队 bot 添加身份验证
author: clearab
description: 如何：将 OAuth 身份验证添加到 Microsoft 团队中的 bot。
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 4a573037e970be3f6c010a0a3c4b2e18be811d2f
ms.sourcegitcommit: a08f1c7eb9fca11f44842773ab669c69d4af40db
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/10/2020
ms.locfileid: "43225796"
---
# <a name="add-authentication-to-your-teams-bot"></a><span data-ttu-id="913fe-103">向你的团队 bot 添加身份验证</span><span class="sxs-lookup"><span data-stu-id="913fe-103">Add authentication to your Teams bot</span></span>

<span data-ttu-id="913fe-104">有时，您可能需要在 Microsoft 团队中创建可代表用户访问资源的 bot，如邮件服务。</span><span class="sxs-lookup"><span data-stu-id="913fe-104">There are times when you may need to create bots in Microsoft Teams that can access resources on behalf of the user, such as a mail service.</span></span>

<span data-ttu-id="913fe-105">本文演示如何使用基于 OAuth 2.0 的 Azure Bot 服务 v4 SDK 身份验证。</span><span class="sxs-lookup"><span data-stu-id="913fe-105">This article demonstrates how to use Azure Bot Service v4 SDK authentication, based on OAuth 2.0.</span></span> <span data-ttu-id="913fe-106">这样，就可以更轻松地开发可使用基于用户凭据的身份验证令牌的 bot。</span><span class="sxs-lookup"><span data-stu-id="913fe-106">This makes it easier to develop a bot that can use authentication tokens based on the user's credentials.</span></span> <span data-ttu-id="913fe-107">关键是使用**标识提供程序**，因为我们将在后面看到。</span><span class="sxs-lookup"><span data-stu-id="913fe-107">Key in all this is the use of **identity providers**, as we will see later.</span></span>

<span data-ttu-id="913fe-108">OAuth 2.0 是一种开放的标准，用于 Azure Active Directory （Azure AD）和许多其他标识提供程序使用的身份验证和授权。</span><span class="sxs-lookup"><span data-stu-id="913fe-108">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="913fe-109">对 OAuth 2.0 的基本了解是在团队中使用身份验证的先决条件。</span><span class="sxs-lookup"><span data-stu-id="913fe-109">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

<span data-ttu-id="913fe-110">有关基本了解，请参阅[oauth 2 已简化](https://aka.ms/oauth2-simplified)，有关完整规范，则为[oauth 2.0](https://oauth.net/2/) 。</span><span class="sxs-lookup"><span data-stu-id="913fe-110">See [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) for a basic understanding, and [OAuth 2.0](https://oauth.net/2/) for the complete specification.</span></span>

<span data-ttu-id="913fe-111">有关 Azure Bot 服务如何处理身份验证的详细信息，请参阅[对话中的用户身份验证](https://aka.ms/azure-bot-authentication)。</span><span class="sxs-lookup"><span data-stu-id="913fe-111">For more information about how the Azure Bot Service handles authentication, see [User authentication within a conversation](https://aka.ms/azure-bot-authentication).</span></span>

<span data-ttu-id="913fe-112">在本文中，您将了解：</span><span class="sxs-lookup"><span data-stu-id="913fe-112">In this article you'll learn:</span></span>

- <span data-ttu-id="913fe-113">**如何创建启用身份验证的 bot**。</span><span class="sxs-lookup"><span data-stu-id="913fe-113">**How to create an authentication-enabled bot**.</span></span> <span data-ttu-id="913fe-114">你将使用[cs-auth 示例][teams-auth-bot-cs]来处理用户登录凭据和生成身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="913fe-114">You'll use [cs-auth-sample][teams-auth-bot-cs] to handle user sign-in credentials and the generating the authentication token.</span></span>
- <span data-ttu-id="913fe-115">**如何将机器人部署到 Azure 并将其与标识提供程序关联**。</span><span class="sxs-lookup"><span data-stu-id="913fe-115">**How to deploy the bot to Azure and associate it with an identity provider**.</span></span> <span data-ttu-id="913fe-116">提供程序根据用户登录凭据发出令牌。</span><span class="sxs-lookup"><span data-stu-id="913fe-116">The provider issues a token based on user sign-in credentials.</span></span> <span data-ttu-id="913fe-117">Bot 可以使用令牌访问需要身份验证的资源，如邮件服务。</span><span class="sxs-lookup"><span data-stu-id="913fe-117">The bot can use the token to access resources, such as a mail service, which require authentication.</span></span> <span data-ttu-id="913fe-118">有关详细信息，请参阅[适用于 bot 的 Microsoft 团队身份验证流](auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="913fe-118">For more information see  [Microsoft Teams authentication flow for bots](auth-flow-bot.md).</span></span>
- <span data-ttu-id="913fe-119">**如何在 Microsoft 团队中集成机器人**。</span><span class="sxs-lookup"><span data-stu-id="913fe-119">**How to integrate the bot within Microsoft Teams**.</span></span> <span data-ttu-id="913fe-120">将 bot 集成后，可以在聊天中登录并与之交换邮件。</span><span class="sxs-lookup"><span data-stu-id="913fe-120">Once the bot has been integrated, you can sign in and exchange messages with it in a chat.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="913fe-121">先决条件</span><span class="sxs-lookup"><span data-stu-id="913fe-121">Prerequisites</span></span>

- <span data-ttu-id="913fe-122">有关[机器人基础][concept-basics]知识、[管理状态][concept-state]、[对话框库][concept-dialogs]以及如何[实施顺序对话流][simple-dialog]的知识。</span><span class="sxs-lookup"><span data-stu-id="913fe-122">Knowledge of [bot basics][concept-basics], [managing state][concept-state], the [dialogs library][concept-dialogs], and how to [implement sequential conversation flow][simple-dialog].</span></span>
- <span data-ttu-id="913fe-123">Azure 和 OAuth 2.0 开发方面的知识。</span><span class="sxs-lookup"><span data-stu-id="913fe-123">Knowledge of Azure and OAuth 2.0 development.</span></span>
- <span data-ttu-id="913fe-124">Visual Studio 2017 或更高版本和 Git。</span><span class="sxs-lookup"><span data-stu-id="913fe-124">Visual Studio 2017 or later and Git.</span></span>
- <span data-ttu-id="913fe-125">Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="913fe-125">Azure account.</span></span> <span data-ttu-id="913fe-126">如果需要，可以创建[Azure 免费帐户](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="913fe-126">If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="913fe-127">下面的示例。</span><span class="sxs-lookup"><span data-stu-id="913fe-127">The following sample.</span></span>

    | <span data-ttu-id="913fe-128">示例</span><span class="sxs-lookup"><span data-stu-id="913fe-128">Sample</span></span> | <span data-ttu-id="913fe-129">BotBuilder 版本</span><span class="sxs-lookup"><span data-stu-id="913fe-129">BotBuilder version</span></span> | <span data-ttu-id="913fe-130">示</span><span class="sxs-lookup"><span data-stu-id="913fe-130">Demonstrates</span></span> |
    |:---|:---:|:---|
    | <span data-ttu-id="913fe-131">Cs 中的**Bot 身份验证**- [auth-示例][teams-auth-bot-cs]</span><span class="sxs-lookup"><span data-stu-id="913fe-131">**Bot authentication** in [cs-auth-sample][teams-auth-bot-cs]</span></span> | <span data-ttu-id="913fe-132">v4</span><span class="sxs-lookup"><span data-stu-id="913fe-132">v4</span></span> | <span data-ttu-id="913fe-133">OAuthCard 支持</span><span class="sxs-lookup"><span data-stu-id="913fe-133">OAuthCard support</span></span> |
    | <span data-ttu-id="913fe-134">[Js-auth][teams-auth-bot-js]中的**Bot 身份验证**-示例</span><span class="sxs-lookup"><span data-stu-id="913fe-134">**Bot authentication** in [js-auth-sample][teams-auth-bot-js]</span></span> | <span data-ttu-id="913fe-135">v4</span><span class="sxs-lookup"><span data-stu-id="913fe-135">v4</span></span>| <span data-ttu-id="913fe-136">OAuthCard 支持</span><span class="sxs-lookup"><span data-stu-id="913fe-136">OAuthCard support</span></span>  |
    | <span data-ttu-id="913fe-137">[Py-auth][teams-auth-bot-py]中的**Bot 身份验证**-示例</span><span class="sxs-lookup"><span data-stu-id="913fe-137">**Bot authentication** in [py-auth-sample][teams-auth-bot-py]</span></span> | <span data-ttu-id="913fe-138">v4</span><span class="sxs-lookup"><span data-stu-id="913fe-138">v4</span></span> | <span data-ttu-id="913fe-139">OAuthCard 支持</span><span class="sxs-lookup"><span data-stu-id="913fe-139">OAuthCard support</span></span> |

## <a name="create-the-resource-group"></a><span data-ttu-id="913fe-140">创建资源组</span><span class="sxs-lookup"><span data-stu-id="913fe-140">Create the resource group</span></span>

<span data-ttu-id="913fe-141">资源组和服务计划不是必需的，但它们使您可以方便地释放所创建的资源。</span><span class="sxs-lookup"><span data-stu-id="913fe-141">The resource group and the service plan aren't strictly necessary, but they allow you to conveniently release the resources you create.</span></span> <span data-ttu-id="913fe-142">这对于保持资源的组织和可管理性来说是很好的做法。</span><span class="sxs-lookup"><span data-stu-id="913fe-142">This is good practice for keeping your resources organized and manageable.</span></span>

<span data-ttu-id="913fe-143">您可以使用资源组为 Bot 框架创建单独的资源。</span><span class="sxs-lookup"><span data-stu-id="913fe-143">You use a resource group to create individual resources for the Bot Framework.</span></span> <span data-ttu-id="913fe-144">为了提高性能，请确保这些资源位于同一个 Azure 区域中。</span><span class="sxs-lookup"><span data-stu-id="913fe-144">For performance, ensure that these resources are located in the same Azure region.</span></span>

1. <span data-ttu-id="913fe-145">在您的浏览器中，登录到[**Azure 门户**][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="913fe-145">In your browser, sign into the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="913fe-146">在左侧导航窗格中，选择 "**资源组**"。</span><span class="sxs-lookup"><span data-stu-id="913fe-146">In the left navigation panel, select **Resource groups**.</span></span>
1. <span data-ttu-id="913fe-147">在显示的窗口的左上角，选择 "**添加**" 选项卡以创建新的资源组。</span><span class="sxs-lookup"><span data-stu-id="913fe-147">In the upper left of the displayed window, select **Add** tab to create a new resource group.</span></span> <span data-ttu-id="913fe-148">系统将提示你提供以下内容：</span><span class="sxs-lookup"><span data-stu-id="913fe-148">You'll be prompted to provide the following:</span></span>
    1. <span data-ttu-id="913fe-149">**订阅**。</span><span class="sxs-lookup"><span data-stu-id="913fe-149">**Subscription**.</span></span> <span data-ttu-id="913fe-150">使用现有订阅。</span><span class="sxs-lookup"><span data-stu-id="913fe-150">Use your existing subscription.</span></span>
    1. <span data-ttu-id="913fe-151">**资源组**。</span><span class="sxs-lookup"><span data-stu-id="913fe-151">**Resource group**.</span></span> <span data-ttu-id="913fe-152">输入资源组的名称。</span><span class="sxs-lookup"><span data-stu-id="913fe-152">Enter the name for the resource group.</span></span> <span data-ttu-id="913fe-153">例如， *TeamsResourceGroup*。</span><span class="sxs-lookup"><span data-stu-id="913fe-153">An example could be  *TeamsResourceGroup*.</span></span> <span data-ttu-id="913fe-154">请记住，该名称必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="913fe-154">Remember that the name must be unique.</span></span>
    1. <span data-ttu-id="913fe-155">从 "**区域**" 下拉菜单中，选择 "*美国西部*" 或 "接近您的应用程序的区域"。</span><span class="sxs-lookup"><span data-stu-id="913fe-155">From the **Region** drop-down menu, select *West US*, or a region close to your applications.</span></span>
    1. <span data-ttu-id="913fe-156">选择 "**查看" 和 "创建**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="913fe-156">Select the **Review and create** button.</span></span> <span data-ttu-id="913fe-157">您应该会看到标题为 "已*通过验证*"。</span><span class="sxs-lookup"><span data-stu-id="913fe-157">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="913fe-158">选择 "**创建**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="913fe-158">Select the **Create** button.</span></span> <span data-ttu-id="913fe-159">创建资源组可能需要几分钟的时间。</span><span class="sxs-lookup"><span data-stu-id="913fe-159">It may take a few minutes to create the resource group.</span></span>

> [!TIP]
> <span data-ttu-id="913fe-160">与本教程后面创建的资源一样，最好将此资源组固定到您的仪表板以便轻松访问。</span><span class="sxs-lookup"><span data-stu-id="913fe-160">As with the resources you'll create later in this tutorial, it's a good idea to pin this resource group to your dashboard for easy access.</span></span> <span data-ttu-id="913fe-161">如果您想要这样做，请选择 pin 图标 & # 128204;在仪表板的右上方。</span><span class="sxs-lookup"><span data-stu-id="913fe-161">If you'd like to do so, select the pin icon &#128204; in the upper right of the dashboard.</span></span>

## <a name="create-the-service-plan"></a><span data-ttu-id="913fe-162">创建服务计划</span><span class="sxs-lookup"><span data-stu-id="913fe-162">Create the service plan</span></span>

1. <span data-ttu-id="913fe-163">在[**Azure 门户**][azure-portal]的左侧导航窗格中，选择 "**创建资源**"。</span><span class="sxs-lookup"><span data-stu-id="913fe-163">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="913fe-164">在 "搜索" 框中，键入*App Service Plan*。</span><span class="sxs-lookup"><span data-stu-id="913fe-164">In the search box, type *App Service Plan*.</span></span> <span data-ttu-id="913fe-165">从搜索结果中选择**应用服务计划**卡片。</span><span class="sxs-lookup"><span data-stu-id="913fe-165">Select the **App Service Plan** card from the search results.</span></span>
1. <span data-ttu-id="913fe-166">选择“创建”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="913fe-166">Select **Create**.</span></span>
1. <span data-ttu-id="913fe-167">系统将要求你提供以下信息：</span><span class="sxs-lookup"><span data-stu-id="913fe-167">You'll be asked to provide the following information:</span></span>
    1. <span data-ttu-id="913fe-168">**订阅**。</span><span class="sxs-lookup"><span data-stu-id="913fe-168">**Subscription**.</span></span> <span data-ttu-id="913fe-169">您可以使用现有订阅。</span><span class="sxs-lookup"><span data-stu-id="913fe-169">You can use an existing subscription.</span></span>
    1. <span data-ttu-id="913fe-170">**资源组**。</span><span class="sxs-lookup"><span data-stu-id="913fe-170">**Resource Group**.</span></span> <span data-ttu-id="913fe-171">选择之前创建的组。</span><span class="sxs-lookup"><span data-stu-id="913fe-171">Select the group you created earlier.</span></span>
    1. <span data-ttu-id="913fe-172">**名称**。</span><span class="sxs-lookup"><span data-stu-id="913fe-172">**Name**.</span></span> <span data-ttu-id="913fe-173">输入服务计划的名称。</span><span class="sxs-lookup"><span data-stu-id="913fe-173">Enter the name for the service plan.</span></span> <span data-ttu-id="913fe-174">例如， *TeamsServicePlan*。</span><span class="sxs-lookup"><span data-stu-id="913fe-174">An example could be  *TeamsServicePlan*.</span></span> <span data-ttu-id="913fe-175">请记住，此名称在组中必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="913fe-175">Remember that the name must be unique, within the group.</span></span>
    1. <span data-ttu-id="913fe-176">**操作系统**。</span><span class="sxs-lookup"><span data-stu-id="913fe-176">**Operating System**.</span></span> <span data-ttu-id="913fe-177">选择 " *Windows* " 或 "适用的操作系统"。</span><span class="sxs-lookup"><span data-stu-id="913fe-177">Select *Windows* or your applicable OS.</span></span>
    1. <span data-ttu-id="913fe-178">**区域**。</span><span class="sxs-lookup"><span data-stu-id="913fe-178">**Region**.</span></span> <span data-ttu-id="913fe-179">选择 "*西部*" 或 "区域接近您的应用程序"。</span><span class="sxs-lookup"><span data-stu-id="913fe-179">Select *West US* or a region close to your applications.</span></span>
    1. <span data-ttu-id="913fe-180">**定价层**。</span><span class="sxs-lookup"><span data-stu-id="913fe-180">**Pricing Tier**.</span></span> <span data-ttu-id="913fe-181">确保选择了 "*标准 S1* "。</span><span class="sxs-lookup"><span data-stu-id="913fe-181">Make sure that *Standard S1* is selected.</span></span> <span data-ttu-id="913fe-182">此值应为默认值。</span><span class="sxs-lookup"><span data-stu-id="913fe-182">This should be the default value.</span></span>
    1. <span data-ttu-id="913fe-183">选择 "**查看" 和 "创建**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="913fe-183">Select the **Review and create** button.</span></span> <span data-ttu-id="913fe-184">您应该会看到标题为 "已*通过验证*"。</span><span class="sxs-lookup"><span data-stu-id="913fe-184">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="913fe-185">选择“创建”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="913fe-185">Select **Create**.</span></span> <span data-ttu-id="913fe-186">可能需要几分钟的时间来创建应用服务计划。</span><span class="sxs-lookup"><span data-stu-id="913fe-186">It may take a few minutes to create the app service plan.</span></span> <span data-ttu-id="913fe-187">该计划将列在资源组中。</span><span class="sxs-lookup"><span data-stu-id="913fe-187">The plan will be listed in the resource group.</span></span>

## <a name="create-the-bot-channels-registration"></a><span data-ttu-id="913fe-188">创建 bot 通道注册</span><span class="sxs-lookup"><span data-stu-id="913fe-188">Create the bot channels registration</span></span>

<span data-ttu-id="913fe-189">如果你有 Microsoft 应用 Id 和应用密码（客户端密码），bot 通道注册会将您的 web 服务注册为带有 Bot 框架的 bot。</span><span class="sxs-lookup"><span data-stu-id="913fe-189">The bot channels registration registers your web service as a bot with the Bot Framework, provided you have a Microsoft App Id and App password (client secret).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="913fe-190">仅当你的 bot 未托管在 Azure 中时，才需要注册你的 bot。</span><span class="sxs-lookup"><span data-stu-id="913fe-190">You only need to register your bot if it is not hosted in Azure.</span></span> <span data-ttu-id="913fe-191">如果你通过 Azure 门户[创建了一个 bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0) ，则它已向该服务注册。</span><span class="sxs-lookup"><span data-stu-id="913fe-191">If you [created a bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0) through the Azure portal then it is already registered with the service.</span></span> <span data-ttu-id="913fe-192">如果你通过[Bot 框架](https://dev.botframework.com/bots/new)或[AppStudio](~/concepts/build-and-test/app-studio-overview.md)创建了你的 bot，你的 Bot 不会在 Azure 中注册。</span><span class="sxs-lookup"><span data-stu-id="913fe-192">If you created your bot through the [Bot Framework](https://dev.botframework.com/bots/new) or [AppStudio](~/concepts/build-and-test/app-studio-overview.md) your bot isn't registered in Azure.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

<span data-ttu-id="913fe-193">在 Azure 创建注册资源之后，它将包含在资源组列表中。</span><span class="sxs-lookup"><span data-stu-id="913fe-193">After Azure has created the registration resource it will be included in the resource group list.</span></span>  

![机器人应用程序通道注册组](../../../assets/images/authentication/auth-bot-channels-registration-group.PNG)

> [!NOTE]
> <span data-ttu-id="913fe-195">自动程序通道注册资源将显示**全局**区域，即使您选择了 "西部我们"。</span><span class="sxs-lookup"><span data-stu-id="913fe-195">The Bot Channels Registration resource will show the **Global** region even if you selected West US.</span></span> <span data-ttu-id="913fe-196">这是预期的。</span><span class="sxs-lookup"><span data-stu-id="913fe-196">This is expected.</span></span>

<span data-ttu-id="913fe-197">有关详细信息，请参阅为[团队创建机器人](../create-a-bot-for-teams.md)。</span><span class="sxs-lookup"><span data-stu-id="913fe-197">For more information, see [Create a bot for Teams](../create-a-bot-for-teams.md).</span></span>

## <a name="create-the-identity-provider"></a><span data-ttu-id="913fe-198">创建标识提供程序</span><span class="sxs-lookup"><span data-stu-id="913fe-198">Create the identity provider</span></span>

<span data-ttu-id="913fe-199">您需要可用于身份验证的标识提供程序。</span><span class="sxs-lookup"><span data-stu-id="913fe-199">You need an identity provider that can be used for authentication.</span></span>
<span data-ttu-id="913fe-200">在此过程中，你将使用 Azure AD 提供程序;此外，还可以使用其他受支持的 Azure AD 标识提供程序。</span><span class="sxs-lookup"><span data-stu-id="913fe-200">In this procedure you'll use an Azure AD provider; other Azure AD supported identity providers can also be used.</span></span>

1. <span data-ttu-id="913fe-201">在[**Azure 门户**][azure-portal]的左侧导航窗格中，选择 " **Azure Active Directory**"。</span><span class="sxs-lookup"><span data-stu-id="913fe-201">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Azure Active Directory**.</span></span>
    > [!TIP]
    > <span data-ttu-id="913fe-202">你将需要在可同意委派应用程序请求的租户中创建并注册此 Azure AD 资源。</span><span class="sxs-lookup"><span data-stu-id="913fe-202">You'll need to create and register this Azure AD resource in a tenant in which you can consent to delegate permissions requested by an application.</span></span>
    > <span data-ttu-id="913fe-203">有关创建租户的说明，请参阅[访问门户和创建租户](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)。</span><span class="sxs-lookup"><span data-stu-id="913fe-203">For instruction on creating a tenant, see [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span></span>
1. <span data-ttu-id="913fe-204">在左面板中，选择 "**应用注册**"。</span><span class="sxs-lookup"><span data-stu-id="913fe-204">In the left panel, select **App registrations**.</span></span>
1. <span data-ttu-id="913fe-205">在右侧面板中，选择左上角的 "**新建注册**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="913fe-205">In the right panel, select the **New registration** tab, in the upper left.</span></span>
1. <span data-ttu-id="913fe-206">系统将要求你提供以下信息：</span><span class="sxs-lookup"><span data-stu-id="913fe-206">You'll be asked to provide the following information:</span></span>
   1. <span data-ttu-id="913fe-207">**名称**。</span><span class="sxs-lookup"><span data-stu-id="913fe-207">**Name**.</span></span> <span data-ttu-id="913fe-208">输入应用程序的名称。</span><span class="sxs-lookup"><span data-stu-id="913fe-208">Enter the name for the application.</span></span> <span data-ttu-id="913fe-209">例如， *BotTeamsIdentity*。</span><span class="sxs-lookup"><span data-stu-id="913fe-209">An example could be  *BotTeamsIdentity*.</span></span> <span data-ttu-id="913fe-210">请记住，该名称必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="913fe-210">Remember that the name must be unique.</span></span>
   1. <span data-ttu-id="913fe-211">为您的应用程序选择**支持的帐户类型**。</span><span class="sxs-lookup"><span data-stu-id="913fe-211">Select the **Supported account types** for your application.</span></span> <span data-ttu-id="913fe-212">选择*任何组织目录（任何 AZURE AD 目录-多租户）和个人 Microsoft 帐户（例如 Skype、Xbox）中的 "帐户"*。</span><span class="sxs-lookup"><span data-stu-id="913fe-212">Select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
   1. <span data-ttu-id="913fe-213">对于**重定向 URI**：</span><span class="sxs-lookup"><span data-stu-id="913fe-213">For the **Redirect URI**:</span></span><br/>
       <span data-ttu-id="913fe-214">&#x2713;选择 " **Web**"。</span><span class="sxs-lookup"><span data-stu-id="913fe-214">&#x2713;Select **Web**.</span></span> <br/>
       <span data-ttu-id="913fe-215">&#x2713; 将 URL 设置为`https://token.botframework.com/.auth/web/redirect`。</span><span class="sxs-lookup"><span data-stu-id="913fe-215">&#x2713; Set the URL to `https://token.botframework.com/.auth/web/redirect`.</span></span>
   1. <span data-ttu-id="913fe-216">选择 "**注册**"。</span><span class="sxs-lookup"><span data-stu-id="913fe-216">Select **Register**.</span></span>

1. <span data-ttu-id="913fe-217">创建后，Azure 将显示该应用程序的 "**概述**" 页。</span><span class="sxs-lookup"><span data-stu-id="913fe-217">Once it is created, Azure displays the **Overview** page for the app.</span></span> <span data-ttu-id="913fe-218">将下面的信息复制并保存到一个文件中：</span><span class="sxs-lookup"><span data-stu-id="913fe-218">Copy and save the following information to a file:</span></span>

    1. <span data-ttu-id="913fe-219">**应用程序（客户端） ID**值。</span><span class="sxs-lookup"><span data-stu-id="913fe-219">The **Application (client) ID** value.</span></span> <span data-ttu-id="913fe-220">将此 Azure 标识应用程序注册到你的 bot 时，你将在稍后将此值用作*客户端 ID* 。</span><span class="sxs-lookup"><span data-stu-id="913fe-220">You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.</span></span>
    1. <span data-ttu-id="913fe-221">**目录（租户） ID**值。</span><span class="sxs-lookup"><span data-stu-id="913fe-221">The **Directory (tenant) ID** value.</span></span> <span data-ttu-id="913fe-222">您还将此值用作*租户 ID* ，以向你的 bot 注册此 Azure 标识应用程序。</span><span class="sxs-lookup"><span data-stu-id="913fe-222">You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.</span></span>

1. <span data-ttu-id="913fe-223">在左面板中，选择 "**证书 & 密码**" 以创建应用程序的客户端密码。</span><span class="sxs-lookup"><span data-stu-id="913fe-223">In the left panel, select **Certificates & secrets** to create a client secret for your application.</span></span>

   1. <span data-ttu-id="913fe-224">在 "**客户端密码**" 下，选择 &#x2795;**新的客户端密码**。</span><span class="sxs-lookup"><span data-stu-id="913fe-224">Under **Client secrets**, select &#x2795; **New client secret**.</span></span>
   1. <span data-ttu-id="913fe-225">添加描述以标识来自其他用户可能需要为此应用程序创建的此机密，如*团队中的 Bot 标识应用程序*。</span><span class="sxs-lookup"><span data-stu-id="913fe-225">Add a description to identify this secret from others you might need to create for this app, such as *Bot identity app in Teams*.</span></span>
   1. <span data-ttu-id="913fe-226">将**过期**时间设置为您所做的选择。</span><span class="sxs-lookup"><span data-stu-id="913fe-226">Set **Expires** to your selection.</span></span>
   1. <span data-ttu-id="913fe-227">选择“**添加**”。</span><span class="sxs-lookup"><span data-stu-id="913fe-227">Select **Add**.</span></span>
   1. <span data-ttu-id="913fe-228">在离开此页面之前，请**记录此密码**。</span><span class="sxs-lookup"><span data-stu-id="913fe-228">Before leaving this page, **record the secret**.</span></span> <span data-ttu-id="913fe-229">在你将 Azure AD 应用程序注册到你的 bot 时，你将在稍后将此值用作_客户端密码_。</span><span class="sxs-lookup"><span data-stu-id="913fe-229">You'll use this value later as the _Client secret_ when you register your Azure AD application with your bot.</span></span>

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a><span data-ttu-id="913fe-230">配置标识提供程序连接，并将其注册到机器人</span><span class="sxs-lookup"><span data-stu-id="913fe-230">Configure the identity provider connection and register it with the bot</span></span>

1. <span data-ttu-id="913fe-231">在[**Azure 门户**][azure-portal]中，从仪表板中选择资源组。</span><span class="sxs-lookup"><span data-stu-id="913fe-231">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="913fe-232">选择你的 bot 频道注册链接。</span><span class="sxs-lookup"><span data-stu-id="913fe-232">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="913fe-233">在 "资源" 页上，选择 "**设置**"。</span><span class="sxs-lookup"><span data-stu-id="913fe-233">On the resource page, select **Settings**.</span></span>
1. <span data-ttu-id="913fe-234">在页面底部附近的 " **OAuth 连接设置**" 下，选择 "**添加设置**"。</span><span class="sxs-lookup"><span data-stu-id="913fe-234">Under **OAuth Connection Settings** near the bottom of the page, select **Add Setting**.</span></span>
1. <span data-ttu-id="913fe-235">如下所示完成表单：</span><span class="sxs-lookup"><span data-stu-id="913fe-235">Complete the form as follows:</span></span>

    1. <span data-ttu-id="913fe-236">**名称**。</span><span class="sxs-lookup"><span data-stu-id="913fe-236">**Name**.</span></span> <span data-ttu-id="913fe-237">输入连接的名称。</span><span class="sxs-lookup"><span data-stu-id="913fe-237">Enter a name for the connection.</span></span> <span data-ttu-id="913fe-238">您将在`appsettings.json`文件的 bot 中使用此名称。</span><span class="sxs-lookup"><span data-stu-id="913fe-238">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="913fe-239">例如*BotTeamsAuthADv1*。</span><span class="sxs-lookup"><span data-stu-id="913fe-239">For example *BotTeamsAuthADv1*.</span></span>
    1. <span data-ttu-id="913fe-240">**服务提供商**。</span><span class="sxs-lookup"><span data-stu-id="913fe-240">**Service Provider**.</span></span> <span data-ttu-id="913fe-241">选择“**Azure Active Directory**”。</span><span class="sxs-lookup"><span data-stu-id="913fe-241">Select **Azure Active Directory**.</span></span> <span data-ttu-id="913fe-242">选择此项后，将显示 Azure AD 特有的字段。</span><span class="sxs-lookup"><span data-stu-id="913fe-242">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="913fe-243">**客户端 id**。在上面的步骤中，输入您为 Azure 标识提供程序应用记录的应用程序（客户端） ID。</span><span class="sxs-lookup"><span data-stu-id="913fe-243">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="913fe-244">**客户端密码**。</span><span class="sxs-lookup"><span data-stu-id="913fe-244">**Client secret**.</span></span> <span data-ttu-id="913fe-245">在上面的步骤中，输入您为 Azure 标识提供程序应用程序记录的密码。</span><span class="sxs-lookup"><span data-stu-id="913fe-245">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="913fe-246">**授予类型**。</span><span class="sxs-lookup"><span data-stu-id="913fe-246">**Grant Type**.</span></span> <span data-ttu-id="913fe-247">Enter `authorization_code`。</span><span class="sxs-lookup"><span data-stu-id="913fe-247">Enter `authorization_code`.</span></span>
    1. <span data-ttu-id="913fe-248">**登录 URL**。</span><span class="sxs-lookup"><span data-stu-id="913fe-248">**Login URL**.</span></span> <span data-ttu-id="913fe-249">Enter `https://login.microsoftonline.com`。</span><span class="sxs-lookup"><span data-stu-id="913fe-249">Enter `https://login.microsoftonline.com`.</span></span>
    1. <span data-ttu-id="913fe-250">**租户 id**，请输入您之前为 Azure 标识应用记录的**目录（租户） ID**或根据您创建标识提供程序应用程序时所选的受支持帐户类型的不同，而不是**常见**的。</span><span class="sxs-lookup"><span data-stu-id="913fe-250">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="913fe-251">若要确定要分配的值，请执行以下条件：</span><span class="sxs-lookup"><span data-stu-id="913fe-251">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="913fe-252">如果您选择了 "*仅在此组织目录中的帐户（仅限 microsoft-单个租户）* " 或 "*任何组织目录中的帐户（microsoft AAD directory-多租户）* "，请输入您之前为 AAD 应用程序记录的**租户 ID** 。</span><span class="sxs-lookup"><span data-stu-id="913fe-252">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="913fe-253">这将是与可以进行身份验证的用户关联的租户。</span><span class="sxs-lookup"><span data-stu-id="913fe-253">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="913fe-254">如果您*在任何组织目录（任何 AAD 目录-多租户和个人 Microsoft 帐户，例如 Skype、Xbox、Outlook）中*选择了 "帐户"，请输入**通用**词，而不是租户 ID。</span><span class="sxs-lookup"><span data-stu-id="913fe-254">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="913fe-255">否则，AAD 应用将通过已选择 ID 的租户进行验证，并排除个人 Microsoft 帐户。</span><span class="sxs-lookup"><span data-stu-id="913fe-255">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    <span data-ttu-id="913fe-256">水平.</span><span class="sxs-lookup"><span data-stu-id="913fe-256">h.</span></span> <span data-ttu-id="913fe-257">对于 "**资源 URL**" `https://graph.microsoft.com/`，请输入。</span><span class="sxs-lookup"><span data-stu-id="913fe-257">For **Resource URL**, enter `https://graph.microsoft.com/`.</span></span> <span data-ttu-id="913fe-258">当前代码示例中不使用此代码。</span><span class="sxs-lookup"><span data-stu-id="913fe-258">This is not used in the current code sample.</span></span>  
    <span data-ttu-id="913fe-259">得到.</span><span class="sxs-lookup"><span data-stu-id="913fe-259">i.</span></span> <span data-ttu-id="913fe-260">将**范围**保留为空。</span><span class="sxs-lookup"><span data-stu-id="913fe-260">Leave **Scopes** blank.</span></span> <span data-ttu-id="913fe-261">下面的图像是一个示例：</span><span class="sxs-lookup"><span data-stu-id="913fe-261">The following image is an example:</span></span>

    ![团队 bot 应用程序身份验证连接字符串 adv1](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. <span data-ttu-id="913fe-263">选择“**保存**”。</span><span class="sxs-lookup"><span data-stu-id="913fe-263">Select **Save**.</span></span>

### <a name="test-the-connection"></a><span data-ttu-id="913fe-264">测试连接</span><span class="sxs-lookup"><span data-stu-id="913fe-264">Test the connection</span></span>

1. <span data-ttu-id="913fe-265">选择该连接条目以打开您刚创建的连接。</span><span class="sxs-lookup"><span data-stu-id="913fe-265">Select the connection entry to open the connection you just created.</span></span>
1. <span data-ttu-id="913fe-266">在 "**服务提供程序连接" 设置**面板的顶部选择 "**测试连接**"。</span><span class="sxs-lookup"><span data-stu-id="913fe-266">Select **Test Connection** at the top of the **Service Provider Connection Setting** panel.</span></span>
1. <span data-ttu-id="913fe-267">第一次执行此操作时，将打开一个新的浏览器窗口，要求您选择帐户。</span><span class="sxs-lookup"><span data-stu-id="913fe-267">The first time you do this will open a new browser window asking you to select an account.</span></span> <span data-ttu-id="913fe-268">选择要使用的一个。</span><span class="sxs-lookup"><span data-stu-id="913fe-268">Select the one you want to use.</span></span>
1. <span data-ttu-id="913fe-269">接下来，系统将要求你允许标识提供程序使用你的数据（凭据）。</span><span class="sxs-lookup"><span data-stu-id="913fe-269">Next, you'll be asked to allow to the identity provider to use your data (credentials).</span></span> <span data-ttu-id="913fe-270">下面的图像是一个示例：</span><span class="sxs-lookup"><span data-stu-id="913fe-270">The following image is an example:</span></span>

    ![团队 bot 应用程序身份验证连接字符串 adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. <span data-ttu-id="913fe-272">选择 "**接受**"。</span><span class="sxs-lookup"><span data-stu-id="913fe-272">Select **Accept**.</span></span>
1. <span data-ttu-id="913fe-273">然后，这会将您重定向到 " **-连接-名称> 成功\<** " 页的测试连接。</span><span class="sxs-lookup"><span data-stu-id="913fe-273">This should then redirect you to a **Test Connection to \<your-connection-name> Succeeded** page.</span></span> <span data-ttu-id="913fe-274">如果遇到错误，请刷新页面。</span><span class="sxs-lookup"><span data-stu-id="913fe-274">Refresh the page if you get an error.</span></span> <span data-ttu-id="913fe-275">下面的图像是一个示例：</span><span class="sxs-lookup"><span data-stu-id="913fe-275">The following image is an example:</span></span>

  ![团队 bot 应用程序身份验证连接字符串 adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

<span data-ttu-id="913fe-277">Bot 代码使用连接名称来检索用户身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="913fe-277">The connection name is used by the bot code to retrieve user authentication tokens.</span></span>

## <a name="prepare-the-bot-sample-code"></a><span data-ttu-id="913fe-278">准备机器人示例代码</span><span class="sxs-lookup"><span data-stu-id="913fe-278">Prepare the bot sample code</span></span>

<span data-ttu-id="913fe-279">完成初步设置后，我们将重点介绍如何创建要在本文中使用的 bot。</span><span class="sxs-lookup"><span data-stu-id="913fe-279">With the preliminary settings done, let's focus on the creation of the bot to use in this article.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="913fe-280">C #/.NET</span><span class="sxs-lookup"><span data-stu-id="913fe-280">C#/.NET</span></span>](#tab/dotnet)

1. <span data-ttu-id="913fe-281">克隆： [cs-auth-示例][teams-auth-bot-cs]。</span><span class="sxs-lookup"><span data-stu-id="913fe-281">Clone [cs-auth-sample][teams-auth-bot-cs].</span></span>
1. <span data-ttu-id="913fe-282">启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="913fe-282">Launch Visual Studio.</span></span>
1. <span data-ttu-id="913fe-283">在工具栏中，选择 "**文件-> 打开-> 项目/解决方案**"，然后打开 "bot" 项目。</span><span class="sxs-lookup"><span data-stu-id="913fe-283">From the toolbar select **File -> Open -> Project/Solution** and open the bot project.</span></span>
1. <span data-ttu-id="913fe-284">在 c # 中，如下所示更新**appsettings** ：</span><span class="sxs-lookup"><span data-stu-id="913fe-284">In C# Update **appsettings.json** as follows:</span></span>

    - <span data-ttu-id="913fe-285">设置`ConnectionName`为你添加到 bot 通道注册的标识提供程序连接的名称。</span><span class="sxs-lookup"><span data-stu-id="913fe-285">Set `ConnectionName` to the name of the identity provider connection you added to the bot channel registration.</span></span> <span data-ttu-id="913fe-286">本示例中使用的名称是*BotTeamsAuthADv1*。</span><span class="sxs-lookup"><span data-stu-id="913fe-286">The name we used in this example is *BotTeamsAuthADv1*.</span></span>
    - <span data-ttu-id="913fe-287">设置`MicrosoftAppId`为在 bot 频道注册时保存的**bot 应用 ID** 。</span><span class="sxs-lookup"><span data-stu-id="913fe-287">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="913fe-288">设置`MicrosoftAppPassword`为在 bot 频道注册时保存的**客户机密**。</span><span class="sxs-lookup"><span data-stu-id="913fe-288">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="913fe-289">将设置`ConnectionName`为标识提供程序连接的名称。</span><span class="sxs-lookup"><span data-stu-id="913fe-289">Set the `ConnectionName` to the name of the identity provider connection.</span></span>

    <span data-ttu-id="913fe-290">根据你的 bot 密码中的字符，你可能需要 XML 对密码进行转义。</span><span class="sxs-lookup"><span data-stu-id="913fe-290">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="913fe-291">例如，需要将任何 & 符号（&）编码为`&amp;`。</span><span class="sxs-lookup"><span data-stu-id="913fe-291">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. <span data-ttu-id="913fe-292">在 "解决方案资源管理器" 中`TeamsAppManifest` ，导航到`manifest.json` "打开`id` " `botId`和 "设置" 文件夹，并转到在 BOT 频道注册时保存的**bot 应用 ID** 。</span><span class="sxs-lookup"><span data-stu-id="913fe-292">In the Solution Explorer, navigate to the `TeamsAppManifest` folder, open `manifest.json` and set `id` and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="javascript"></a>[<span data-ttu-id="913fe-293">JavaScript</span><span class="sxs-lookup"><span data-stu-id="913fe-293">JavaScript</span></span>](#tab/node-js)

1. <span data-ttu-id="913fe-294">Clone[节点-auth-示例][teams-auth-bot-js]。</span><span class="sxs-lookup"><span data-stu-id="913fe-294">Clone [node-auth-sample][teams-auth-bot-js].</span></span>
1. <span data-ttu-id="913fe-295">在控制台中，导航到项目：</span><span class="sxs-lookup"><span data-stu-id="913fe-295">In a console, navigate to the project:</span></span> </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. <span data-ttu-id="913fe-296">安装模块</span><span class="sxs-lookup"><span data-stu-id="913fe-296">Install modules</span></span></br></br>
`npm install`
1. <span data-ttu-id="913fe-297">更新**env**配置，如下所示：</span><span class="sxs-lookup"><span data-stu-id="913fe-297">Update the **.env** configuration as follows:</span></span>

    - <span data-ttu-id="913fe-298">设置`MicrosoftAppId`为在 bot 频道注册时保存的**bot 应用 ID** 。</span><span class="sxs-lookup"><span data-stu-id="913fe-298">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="913fe-299">设置`MicrosoftAppPassword`为在 bot 频道注册时保存的**客户机密**。</span><span class="sxs-lookup"><span data-stu-id="913fe-299">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="913fe-300">将设置`connectionName`为标识提供程序连接的名称。</span><span class="sxs-lookup"><span data-stu-id="913fe-300">Set the `connectionName` to the name of the identity provider connection.</span></span>

    <span data-ttu-id="913fe-301">根据你的 bot 密码中的字符，你可能需要 XML 对密码进行转义。</span><span class="sxs-lookup"><span data-stu-id="913fe-301">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="913fe-302">例如，需要将任何 & 符号（&）编码为`&amp;`。</span><span class="sxs-lookup"><span data-stu-id="913fe-302">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. <span data-ttu-id="913fe-303">`teamsAppManifest`在文件夹中，打开`manifest.json`并将`id`其设置为您的**Microsoft 应用 id** ，并`botId`将其设置为在 bot 频道注册时保存的**bot 应用 id** 。</span><span class="sxs-lookup"><span data-stu-id="913fe-303">In the `teamsAppManifest` folder, open `manifest.json` and set `id`  to your **Microsoft App ID** and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="python"></a>[<span data-ttu-id="913fe-304">Python</span><span class="sxs-lookup"><span data-stu-id="913fe-304">Python</span></span>](#tab/python)

1. <span data-ttu-id="913fe-305">Clone 存储库中的[py-auth-示例][teams-auth-bot-py]。</span><span class="sxs-lookup"><span data-stu-id="913fe-305">Clone [py-auth-sample][teams-auth-bot-py] from the github repository.</span></span>
1. <span data-ttu-id="913fe-306">更新**config.py**：</span><span class="sxs-lookup"><span data-stu-id="913fe-306">Update **config.py**:</span></span>

    - <span data-ttu-id="913fe-307">设置`ConnectionName`为你添加到你的 Bot 的 OAuth 连接设置的名称。</span><span class="sxs-lookup"><span data-stu-id="913fe-307">Set `ConnectionName` to the name of the OAuth connection setting you added to your bot.</span></span>
    - <span data-ttu-id="913fe-308">将`MicrosoftAppId`和`MicrosoftAppPassword`设置为你的 bot 的应用 ID 和应用密码。</span><span class="sxs-lookup"><span data-stu-id="913fe-308">Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.</span></span>

      <span data-ttu-id="913fe-309">根据你的 bot 密码中的字符，你可能需要 XML 对密码进行转义。</span><span class="sxs-lookup"><span data-stu-id="913fe-309">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="913fe-310">例如，需要将任何 & 符号（&）编码为`&amp;`。</span><span class="sxs-lookup"><span data-stu-id="913fe-310">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="913fe-311">将机器人部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="913fe-311">Deploy the bot to Azure</span></span>

<span data-ttu-id="913fe-312">若要部署 bot，请按照 how to 将[机器人部署到 Azure](https://aka.ms/azure-bot-deployment-cli)中的步骤操作。</span><span class="sxs-lookup"><span data-stu-id="913fe-312">To deploy the bot, follow the steps in the how to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span></span>

<span data-ttu-id="913fe-313">或者，在 Visual Studio 中，可以按照以下步骤操作：</span><span class="sxs-lookup"><span data-stu-id="913fe-313">Alternatively, while in Visual Studio, you can follow these steps:</span></span>

1. <span data-ttu-id="913fe-314">在 Visual Studio "*解决方案资源管理器*" 中，选择并按住（或右键单击）项目名称。</span><span class="sxs-lookup"><span data-stu-id="913fe-314">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span></span>
1. <span data-ttu-id="913fe-315">在下拉菜单中，选择 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="913fe-315">In the drop-down menu, select **Publish**.</span></span>
1. <span data-ttu-id="913fe-316">在显示的窗口中，选择 "**新建**" 链接。</span><span class="sxs-lookup"><span data-stu-id="913fe-316">In the displayed window, select the **New** link.</span></span>
1. <span data-ttu-id="913fe-317">在对话框窗口中，选择左侧的 " **App Service** "，在右侧**创建 "新建**"。</span><span class="sxs-lookup"><span data-stu-id="913fe-317">In the dialog window, select **App Service** on the left and **Create New** on the right.</span></span>
1. <span data-ttu-id="913fe-318">选择 "**发布**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="913fe-318">Select the **Publish** button.</span></span>
1. <span data-ttu-id="913fe-319">在下一个对话框窗口中，输入所需的信息。</span><span class="sxs-lookup"><span data-stu-id="913fe-319">In the next dialog window, enter the required information.</span></span> <span data-ttu-id="913fe-320">示例如下：</span><span class="sxs-lookup"><span data-stu-id="913fe-320">The following is an example:</span></span>

   ![auth-应用程序-服务](../../../assets/images/authentication/auth-bot-app-service.png)

1. <span data-ttu-id="913fe-322">选择“创建”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="913fe-322">Select **Create**.</span></span>
1. <span data-ttu-id="913fe-323">如果部署成功完成，您应该会看到它在 Visual Studio 中反映出来。</span><span class="sxs-lookup"><span data-stu-id="913fe-323">If the deployment completes successfully, you should see it reflected in Visual Studio.</span></span> <span data-ttu-id="913fe-324">此外，默认浏览器中会显示一个页面，指示*你的 bot 已准备就绪！*。</span><span class="sxs-lookup"><span data-stu-id="913fe-324">Moreover, a page is displayed in your default browser saying *Your bot is ready!*.</span></span> <span data-ttu-id="913fe-325">该 URL 将类似于： `https://botteamsauth.azurewebsites.net/`。</span><span class="sxs-lookup"><span data-stu-id="913fe-325">The URL will be similar to this: `https://botteamsauth.azurewebsites.net/`.</span></span> <span data-ttu-id="913fe-326">将其保存到文件中。</span><span class="sxs-lookup"><span data-stu-id="913fe-326">Save it to a file.</span></span>
1. <span data-ttu-id="913fe-327">在浏览器中，导航到[**Azure 门户**][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="913fe-327">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="913fe-328">检查您的资源组，应将 bot 与其他资源一起列出。</span><span class="sxs-lookup"><span data-stu-id="913fe-328">Check your resource group, the bot should be listed along with the other resources.</span></span> <span data-ttu-id="913fe-329">下面的图像是一个示例：</span><span class="sxs-lookup"><span data-stu-id="913fe-329">The following image is an example:</span></span>

    ![团队-机器人-auth-应用程序-服务-组](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. <span data-ttu-id="913fe-331">在 "资源" 组中，选择 "bot 频道注册名称" （链接）。</span><span class="sxs-lookup"><span data-stu-id="913fe-331">In the resource group, select the bot channel registration name (link).</span></span>
1. <span data-ttu-id="913fe-332">在左面板中，选择 "**设置**"。</span><span class="sxs-lookup"><span data-stu-id="913fe-332">In the left panel, select **Settings**.</span></span>
1. <span data-ttu-id="913fe-333">在 "**邮件终结点**" 框中，输入上面接下来`api/messages`的 URL。</span><span class="sxs-lookup"><span data-stu-id="913fe-333">In the **Messaging endpoint** box, enter the URL obtained above followed by `api/messages`.</span></span> <span data-ttu-id="913fe-334">下面是一个示例： `https://botteamsauth.azurewebsites.net/api/messages`。</span><span class="sxs-lookup"><span data-stu-id="913fe-334">This is an example: `https://botteamsauth.azurewebsites.net/api/messages`.</span></span>
1. <span data-ttu-id="913fe-335">选择左上角的 "**保存**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="913fe-335">Select the **Save** button in the upper left.</span></span>

## <a name="test-the-bot-using-the-emulator"></a><span data-ttu-id="913fe-336">使用模拟器测试机器人</span><span class="sxs-lookup"><span data-stu-id="913fe-336">Test the bot using the Emulator</span></span>

<span data-ttu-id="913fe-337">如果尚未执行此操作，请安装[Microsoft Bot 框架模拟器](https://aka.ms/bot-framework-emulator-readme)。</span><span class="sxs-lookup"><span data-stu-id="913fe-337">If you haven't done it already, install the [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span></span> <span data-ttu-id="913fe-338">另请参阅[Debug with The 模拟器](https://aka.ms/bot-framework-emulator-debug-with-emulator)。</span><span class="sxs-lookup"><span data-stu-id="913fe-338">See also [Debug with the Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span></span>

<span data-ttu-id="913fe-339">为了使 bot 示例登录正常工作，您必须配置仿真程序，如下所示。</span><span class="sxs-lookup"><span data-stu-id="913fe-339">In order for the bot sample login to work you must configure the Emulator as shown below.</span></span>

### <a name="configure-the-emulator-for-authentication"></a><span data-ttu-id="913fe-340">配置仿真程序以进行身份验证</span><span class="sxs-lookup"><span data-stu-id="913fe-340">Configure the Emulator for authentication</span></span>

<span data-ttu-id="913fe-341">如果 bot 需要身份验证，则必须配置仿真程序，如下所示。</span><span class="sxs-lookup"><span data-stu-id="913fe-341">If a bot requires authentication, you must configure the Emulator as shown below.</span></span>

1. <span data-ttu-id="913fe-342">启动仿真程序。</span><span class="sxs-lookup"><span data-stu-id="913fe-342">Start the Emulator.</span></span>
1. <span data-ttu-id="913fe-343">在仿真程序中，选择左下角 &#9881; 的齿轮图标，或右上角的 "**仿真程序设置**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="913fe-343">In the Emulator, select the gear icon &#9881; in the bottom left, or the **Emulator Settings** tab in the upper right.</span></span>
1. <span data-ttu-id="913fe-344">通过**使用版本1.0 身份验证令牌**选中此框。</span><span class="sxs-lookup"><span data-stu-id="913fe-344">Check the box by **Use version 1.0 authentication tokens**.</span></span>
1. <span data-ttu-id="913fe-345">输入**ngrok**工具的本地路径。</span><span class="sxs-lookup"><span data-stu-id="913fe-345">Enter the local path to the **ngrok** tool.</span></span> <span data-ttu-id="913fe-346">*请参阅*Bot 框架仿真程序/ngrok 隧道集成[Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok))。</span><span class="sxs-lookup"><span data-stu-id="913fe-346">*See* the Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span></span> <span data-ttu-id="913fe-347">有关更多工具信息，请参阅[ngrok](https://ngrok.com/)。</span><span class="sxs-lookup"><span data-stu-id="913fe-347">For more tool information, see [ngrok](https://ngrok.com/).</span></span>
1. <span data-ttu-id="913fe-348">**在仿真程序启动时，通过运行 ngrok**选中该框。</span><span class="sxs-lookup"><span data-stu-id="913fe-348">Check the box by **Run ngrok when the Emulator starts up**.</span></span>
1. <span data-ttu-id="913fe-349">选择 "**保存**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="913fe-349">Select the **Save** button.</span></span>

<span data-ttu-id="913fe-350">当 bot 显示登录卡且用户选择登录按钮时，仿真程序将打开一个页面，用户可使用该页面使用身份验证提供程序进行登录。</span><span class="sxs-lookup"><span data-stu-id="913fe-350">When the bot displays a sign-in card and the user selects the sign-in button, the Emulator opens a page that the user can use to sign in with the authentication provider.</span></span>
<span data-ttu-id="913fe-351">一旦用户执行此操作，提供程序将生成用户令牌，并将其发送到 bot。</span><span class="sxs-lookup"><span data-stu-id="913fe-351">Once the user does so, the provider generates a user token and sends it to the bot.</span></span> <span data-ttu-id="913fe-352">之后，bot 可以代表用户执行操作。</span><span class="sxs-lookup"><span data-stu-id="913fe-352">After that, the bot can act on behalf of the user.</span></span>

### <a name="test-the-bot-locally"></a><span data-ttu-id="913fe-353">本地测试机器人</span><span class="sxs-lookup"><span data-stu-id="913fe-353">Test the bot locally</span></span>

<span data-ttu-id="913fe-354">配置身份验证机制之后，可以执行实际的机器人测试。</span><span class="sxs-lookup"><span data-stu-id="913fe-354">After you have configured the authentication mechanism, you can perform the actual bot testing.</span></span>  

1. <span data-ttu-id="913fe-355">通过 Visual Studio 在你的计算机上本地运行机器人示例（例如）。</span><span class="sxs-lookup"><span data-stu-id="913fe-355">Run the bot sample locally on your machine, via Visual Studio for example.</span></span>
1. <span data-ttu-id="913fe-356">启动仿真程序。</span><span class="sxs-lookup"><span data-stu-id="913fe-356">Start the Emulator.</span></span>
1. <span data-ttu-id="913fe-357">选择 "**打开 bot** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="913fe-357">Select the **Open bot** button.</span></span>
1. <span data-ttu-id="913fe-358">在**机器人 url**中，输入 bot 的本地 URL。</span><span class="sxs-lookup"><span data-stu-id="913fe-358">In the **Bot URL**, enter the bot's local URL.</span></span> <span data-ttu-id="913fe-359">通常为`http://localhost:3978/api/messages`。</span><span class="sxs-lookup"><span data-stu-id="913fe-359">Usually, `http://localhost:3978/api/messages`.</span></span>
1. <span data-ttu-id="913fe-360">在**Microsoft 应用 id**中，输入 bot 的应用 id `appsettings.json`。</span><span class="sxs-lookup"><span data-stu-id="913fe-360">In the **Microsoft App ID** enter the bot's app ID from `appsettings.json`.</span></span>
1. <span data-ttu-id="913fe-361">在**Microsoft App 密码**中，输入 bot 的应用密码`appsettings.json`。</span><span class="sxs-lookup"><span data-stu-id="913fe-361">In the **Microsoft App password** enter the bot's app password from the `appsettings.json`.</span></span>
1. <span data-ttu-id="913fe-362">选择 "**连接**"。</span><span class="sxs-lookup"><span data-stu-id="913fe-362">Select **Connect**.</span></span>
1. <span data-ttu-id="913fe-363">在安装程序启动并运行后，输入任何文本以显示登录卡。</span><span class="sxs-lookup"><span data-stu-id="913fe-363">After the bot is up and running, enter any text to display the sign-in card.</span></span>
1. <span data-ttu-id="913fe-364">选择 "**登录**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="913fe-364">Select the **Sign in** button.</span></span>
1. <span data-ttu-id="913fe-365">将显示一个弹出对话框，以**确认打开的 URL**。</span><span class="sxs-lookup"><span data-stu-id="913fe-365">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="913fe-366">这是为了让 bot 的用户（你）可以进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="913fe-366">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="913fe-367">选择 "**确认**"。</span><span class="sxs-lookup"><span data-stu-id="913fe-367">Select **Confirm**.</span></span>
1. <span data-ttu-id="913fe-368">如果需要，请选择适用用户的帐户。</span><span class="sxs-lookup"><span data-stu-id="913fe-368">If asked, select the applicable user's account.</span></span>
1. <span data-ttu-id="913fe-369">根据您对仿真程序使用的配置，可以获取以下内容之一：</span><span class="sxs-lookup"><span data-stu-id="913fe-369">Depending which configuration you used for the Emulator, you get one of the following:</span></span>
    1. <span data-ttu-id="913fe-370">**使用登录验证代码**</span><span class="sxs-lookup"><span data-stu-id="913fe-370">**Using sign-in verification code**</span></span>  
      <span data-ttu-id="913fe-371">&#x2713; 打开显示验证代码的窗口。</span><span class="sxs-lookup"><span data-stu-id="913fe-371">&#x2713; A window is opened displaying the validation code.</span></span>  
      <span data-ttu-id="913fe-372">&#x2713; 将验证代码复制并输入到聊天框中，以完成登录。</span><span class="sxs-lookup"><span data-stu-id="913fe-372">&#x2713; Copy and enter the validation code into the chat box to complete the sign-in.</span></span>
    1. <span data-ttu-id="913fe-373">**使用身份验证令牌**。</span><span class="sxs-lookup"><span data-stu-id="913fe-373">**Using authentication tokens**.</span></span>  
      <span data-ttu-id="913fe-374">&#x2713; 您根据您的凭据登录。</span><span class="sxs-lookup"><span data-stu-id="913fe-374">&#x2713; You're logged in based on your credentials.</span></span>

    <span data-ttu-id="913fe-375">以下图像是登录后的 bot UI 的示例：</span><span class="sxs-lookup"><span data-stu-id="913fe-375">The following image is an example of the bot UI after you've logged in:</span></span>

    ![auth bot 登录仿真程序](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. <span data-ttu-id="913fe-377">如果你在 bot 询问*你是否要查看令牌*时选择 **"是"** ，则会收到类似于以下内容的响应：</span><span class="sxs-lookup"><span data-stu-id="913fe-377">If you select **Yes** when the bot asks *Would you like to view your token?*, you'll get a response similar to the following:</span></span>

    ![身份验证 bot 登录仿真程序令牌](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. <span data-ttu-id="913fe-379">在 "输入聊天" 框中输入**注销**以注销。这将释放用户令牌，并且机器人将无法代表你进行操作，除非你再次登录。</span><span class="sxs-lookup"><span data-stu-id="913fe-379">Enter **logout** in the input chat box to sign out. This releases the user token, and the bot won't be able to act on your behalf until you sign in again.</span></span>

> [!NOTE]
> <span data-ttu-id="913fe-380">Bot 身份验证需要使用**Bot 连接器服务**。</span><span class="sxs-lookup"><span data-stu-id="913fe-380">Bot authentication requires use of the **Bot Connector Service**.</span></span> <span data-ttu-id="913fe-381">服务访问你的 bot 的 bot 通道注册信息。</span><span class="sxs-lookup"><span data-stu-id="913fe-381">The service accesses the bot channels registration information for your bot.</span></span>

## <a name="test-the-deployed-bot"></a><span data-ttu-id="913fe-382">测试部署的 bot</span><span class="sxs-lookup"><span data-stu-id="913fe-382">Test the deployed bot</span></span>

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. <span data-ttu-id="913fe-383">在浏览器中，导航到[**Azure 门户**][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="913fe-383">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="913fe-384">查找您的资源组。</span><span class="sxs-lookup"><span data-stu-id="913fe-384">Find your resource group.</span></span>
1. <span data-ttu-id="913fe-385">选择 "资源" 链接。</span><span class="sxs-lookup"><span data-stu-id="913fe-385">Select the resource link.</span></span> <span data-ttu-id="913fe-386">将显示 "资源" 页。</span><span class="sxs-lookup"><span data-stu-id="913fe-386">The resource page is displayed.</span></span>
1. <span data-ttu-id="913fe-387">在 "资源" 页中，选择 "**在 Web 聊天中测试**"。</span><span class="sxs-lookup"><span data-stu-id="913fe-387">In the resource page, select **Test in Web Chat**.</span></span> <span data-ttu-id="913fe-388">机器人将启动并显示预定义的问候语。</span><span class="sxs-lookup"><span data-stu-id="913fe-388">The bot starts and displays the predefined greetings.</span></span>
1. <span data-ttu-id="913fe-389">在 "聊天" 框中键入任何内容。</span><span class="sxs-lookup"><span data-stu-id="913fe-389">Type anything in the chat box.</span></span>
1. <span data-ttu-id="913fe-390">选择 "**登录**" 框。</span><span class="sxs-lookup"><span data-stu-id="913fe-390">Select the **Sign in** box.</span></span>
1. <span data-ttu-id="913fe-391">将显示一个弹出对话框，以**确认打开的 URL**。</span><span class="sxs-lookup"><span data-stu-id="913fe-391">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="913fe-392">这是为了让 bot 的用户（你）可以进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="913fe-392">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="913fe-393">选择 "**确认**"。</span><span class="sxs-lookup"><span data-stu-id="913fe-393">Select **Confirm**.</span></span>
1. <span data-ttu-id="913fe-394">如果需要，请选择适用用户的帐户。</span><span class="sxs-lookup"><span data-stu-id="913fe-394">If asked, select the applicable user's account.</span></span>
    <span data-ttu-id="913fe-395">以下图像是登录后的 bot UI 的示例：</span><span class="sxs-lookup"><span data-stu-id="913fe-395">The following image is an example of the bot UI after you have logged in:</span></span>

    ![已部署身份验证 bot 登录](../../../assets/images/authentication/auth-bot-login-deployed.PNG)<span data-ttu-id="913fe-397">.</span><span class="sxs-lookup"><span data-stu-id="913fe-397">.</span></span>

1. <span data-ttu-id="913fe-398">选择 **"是"** 按钮以显示您的身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="913fe-398">Select the **Yes** button to display your authentication token.</span></span> <span data-ttu-id="913fe-399">下面的图像是一个示例：</span><span class="sxs-lookup"><span data-stu-id="913fe-399">The following image is an example:</span></span>

    ![授权 bot 登录部署令牌](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG)<span data-ttu-id="913fe-401">.</span><span class="sxs-lookup"><span data-stu-id="913fe-401">.</span></span>

1. <span data-ttu-id="913fe-402">输入注销以注销。</span><span class="sxs-lookup"><span data-stu-id="913fe-402">Enter logout to sign out.</span></span>

    ![已部署注销的身份验证机器人](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> <span data-ttu-id="913fe-404">如果你在登录时遇到问题，请尝试再次测试连接，如前面步骤中所述。</span><span class="sxs-lookup"><span data-stu-id="913fe-404">If you're having problems signing in, try to test the connection again as described in the previous steps.</span></span> <span data-ttu-id="913fe-405">这可能会重新创建身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="913fe-405">This could recreate the authentication token.</span></span>
> <span data-ttu-id="913fe-406">在 Azure 中使用 Bot 框架 Web 聊天客户端时，您可能需要在身份验证正确建立前多次进行登录。</span><span class="sxs-lookup"><span data-stu-id="913fe-406">With the Bot Framework Web Chat client in Azure, you may need to sign in several times before the authentication is established correctly.</span></span>

## <a name="install-and-test-the-bot-in-teams"></a><span data-ttu-id="913fe-407">在团队中安装和测试机器人</span><span class="sxs-lookup"><span data-stu-id="913fe-407">Install and test the bot in Teams</span></span>

1. <span data-ttu-id="913fe-408">在机器人`TeamsAppManifest`项目中，确保文件夹包含`manifest.json` `outline.png`和`color.png`文件一起包含。</span><span class="sxs-lookup"><span data-stu-id="913fe-408">In your bot project, ensure that the `TeamsAppManifest` folder contains the `manifest.json` along with an `outline.png` and `color.png` files.</span></span>
1. <span data-ttu-id="913fe-409">在 "解决方案资源管理器" `TeamsAppManifest`中，导航到该文件夹。</span><span class="sxs-lookup"><span data-stu-id="913fe-409">In Solution Explorer, navigate to the `TeamsAppManifest` folder.</span></span> <span data-ttu-id="913fe-410">通过`manifest.json`分配以下值进行编辑：</span><span class="sxs-lookup"><span data-stu-id="913fe-410">Edit `manifest.json` by assigning the following values:</span></span>
    1. <span data-ttu-id="913fe-411">确保在将 bot 频道注册时收到的**Bot 应用 ID**分配给`id`和`botId`。</span><span class="sxs-lookup"><span data-stu-id="913fe-411">Ensure that the **bot App ID** you received at the time of the bot channel registration is assigned to `id` and `botId`.</span></span>
    1. <span data-ttu-id="913fe-412">将此值分配`validDomains: [ "token.botframework.com" ]`给：。</span><span class="sxs-lookup"><span data-stu-id="913fe-412">Assign this value: `validDomains: [ "token.botframework.com" ]`.</span></span>
1. <span data-ttu-id="913fe-413">选择和**压缩** `manifest.json`、 `outline.png`和`color.png`文件。</span><span class="sxs-lookup"><span data-stu-id="913fe-413">Select and **zip** the `manifest.json`, `outline.png`, and `color.png` files.</span></span>
1. <span data-ttu-id="913fe-414">打开**Microsoft 团队**。</span><span class="sxs-lookup"><span data-stu-id="913fe-414">Open **Microsoft Teams**.</span></span>
1. <span data-ttu-id="913fe-415">在左侧面板中的底部，选择 "应用"**图标**。</span><span class="sxs-lookup"><span data-stu-id="913fe-415">In the left panel, at the bottom, select the **Apps icon**.</span></span>
1. <span data-ttu-id="913fe-416">在右侧面板的底部，选择 "**上传自定义应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="913fe-416">In the right panel, at the bottom, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="913fe-417">导航到该`TeamsAppManifest`文件夹并上传压缩清单。</span><span class="sxs-lookup"><span data-stu-id="913fe-417">Navigate to the `TeamsAppManifest` folder and upload the zipped manifest.</span></span>
<span data-ttu-id="913fe-418">将显示以下向导：</span><span class="sxs-lookup"><span data-stu-id="913fe-418">The following wizard is displayed:</span></span>

    ![授权 bot 团队上传](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. <span data-ttu-id="913fe-420">选择 "**添加到团队**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="913fe-420">Select the **Add to a team** button.</span></span>
1. <span data-ttu-id="913fe-421">在下一个窗口中，选择要在其中使用 bot 的团队。</span><span class="sxs-lookup"><span data-stu-id="913fe-421">In the next window, select the team where you want to use the bot.</span></span>
1. <span data-ttu-id="913fe-422">选择 "**设置机器人**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="913fe-422">Select the **Set up a bot** button.</span></span>
1. <span data-ttu-id="913fe-423">在左面板中选择三个点（&#x25cf;&#x25cf;&#x25cf;）。</span><span class="sxs-lookup"><span data-stu-id="913fe-423">Select the three dots (&#x25cf;&#x25cf;&#x25cf;) in the left panel.</span></span> <span data-ttu-id="913fe-424">然后，选择 " **App Studio** " 图标。</span><span class="sxs-lookup"><span data-stu-id="913fe-424">Then select the **App Studio** icon.</span></span>
1. <span data-ttu-id="913fe-425">选择 "**清单编辑器**" 选项卡。您应该会看到您上载的 bot 的图标。</span><span class="sxs-lookup"><span data-stu-id="913fe-425">Select the **Manifest editor** tab. You should see the icon for the bot you uploaded.</span></span>
1. <span data-ttu-id="913fe-426">此外，您还应该能够在聊天列表中看到作为联系人列出的 bot，您可以使用它来与 bot 交换邮件。</span><span class="sxs-lookup"><span data-stu-id="913fe-426">Also, you should be able to see the bot listed as a contact in the chat list that you can use to exchange messages with the bot.</span></span>

### <a name="testing-the-bot-locally-in-teams"></a><span data-ttu-id="913fe-427">在团队中本地测试机器人</span><span class="sxs-lookup"><span data-stu-id="913fe-427">Testing the bot locally in Teams</span></span>

<span data-ttu-id="913fe-428">Microsoft 团队是完全基于云的产品，它需要使用 HTTPS 终结点从云中获取所有 it 访问的服务。</span><span class="sxs-lookup"><span data-stu-id="913fe-428">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="913fe-429">因此，若要使 bot （我们的示例）能够在团队中工作，您需要将代码发布到您选择的云，或使本地运行的实例可通过**隧道**工具进行外部访问。</span><span class="sxs-lookup"><span data-stu-id="913fe-429">Therefore, to enable the bot (our sample) to work in Teams, you need to either publish the code to the cloud of your choice, or make a locally running instance externally accessible via a **tunneling** tool.</span></span> <span data-ttu-id="913fe-430">我们建议[ngrok](https://ngrok.com/download)，这将为您在您的计算机上本地打开的端口创建外部可寻址的 URL。</span><span class="sxs-lookup"><span data-stu-id="913fe-430">We recommend  [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span>
<span data-ttu-id="913fe-431">若要设置 ngrok 以准备在本地运行 Microsoft 团队应用程序，请按照以下步骤操作：</span><span class="sxs-lookup"><span data-stu-id="913fe-431">To set up ngrok in preparation for running your Microsoft Teams app locally, follow these steps:</span></span>

1. <span data-ttu-id="913fe-432">在终端窗口中，转到已`ngrok.exe`安装的目录。</span><span class="sxs-lookup"><span data-stu-id="913fe-432">In a terminal window, go the directory where you have `ngrok.exe` installed.</span></span> <span data-ttu-id="913fe-433">建议设置要指向的*环境变量*路径。</span><span class="sxs-lookup"><span data-stu-id="913fe-433">We suggest setting the *environment variable* path to point to it.</span></span>
1. <span data-ttu-id="913fe-434">例如， `ngrok http 3978 --host-header=localhost:3978`运行。</span><span class="sxs-lookup"><span data-stu-id="913fe-434">Run, for example, `ngrok http 3978 --host-header=localhost:3978`.</span></span> <span data-ttu-id="913fe-435">根据需要更换端口号。</span><span class="sxs-lookup"><span data-stu-id="913fe-435">Replace the port number as needed.</span></span>
<span data-ttu-id="913fe-436">这将启动 ngrok 以侦听您指定的端口。</span><span class="sxs-lookup"><span data-stu-id="913fe-436">This launches ngrok to listen on the port you specify.</span></span> <span data-ttu-id="913fe-437">在 return 中，它为您提供一个外部可寻址的 URL，只要 ngrok 正在运行，它就会有效。</span><span class="sxs-lookup"><span data-stu-id="913fe-437">In return, it gives you an externally addressable URL, valid for as long as ngrok is running.</span></span> <span data-ttu-id="913fe-438">下面的图像是一个示例：</span><span class="sxs-lookup"><span data-stu-id="913fe-438">The following image is an example:</span></span>

    ![团队 bot 应用程序身份验证连接字符串 adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG)<span data-ttu-id="913fe-440">.</span><span class="sxs-lookup"><span data-stu-id="913fe-440">.</span></span>

1. <span data-ttu-id="913fe-441">复制转发 HTTPS 地址。</span><span class="sxs-lookup"><span data-stu-id="913fe-441">Copy the forwarding HTTPS address.</span></span> <span data-ttu-id="913fe-442">它应类似于以下内容： `https://dea822bf.ngrok.io/`。</span><span class="sxs-lookup"><span data-stu-id="913fe-442">It should be similar to the following: `https://dea822bf.ngrok.io/`.</span></span>
1. <span data-ttu-id="913fe-443">Append `/api/messages`获取`https://dea822bf.ngrok.io/api/messages`。</span><span class="sxs-lookup"><span data-stu-id="913fe-443">Append `/api/messages` to obtain `https://dea822bf.ngrok.io/api/messages`.</span></span> <span data-ttu-id="913fe-444">这是在 Microsoft 团队的聊天中，在计算机上本地运行的 bot 的**消息终结点**，并可通过 web 访问。</span><span class="sxs-lookup"><span data-stu-id="913fe-444">This is the **messages endpoint** for the bot running locally on your machine and reachable over the web in a chat in Microsoft Teams.</span></span>
1. <span data-ttu-id="913fe-445">要执行的最后一个步骤是更新已部署的 bot 的消息终结点。</span><span class="sxs-lookup"><span data-stu-id="913fe-445">One final step to perform is to update the messages endpoint of the deployed bot.</span></span> <span data-ttu-id="913fe-446">在此示例中，我们在 Azure 中部署了机器人。</span><span class="sxs-lookup"><span data-stu-id="913fe-446">In the example, we deployed the bot in Azure.</span></span> <span data-ttu-id="913fe-447">因此，\* \* 我们将执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="913fe-447">So \*\*let's perform these steps:</span></span>
    1. <span data-ttu-id="913fe-448">在浏览器中导航到[**Azure 门户**][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="913fe-448">In your browser navigate to the [**Azure portal**][azure-portal].</span></span>
    1. <span data-ttu-id="913fe-449">选择你的**Bot 频道注册**。</span><span class="sxs-lookup"><span data-stu-id="913fe-449">Select your **Bot Channel Registration**.</span></span>
    1. <span data-ttu-id="913fe-450">在左面板中，选择 "**设置**"。</span><span class="sxs-lookup"><span data-stu-id="913fe-450">In the left panel, select **Settings**.</span></span>
    1. <span data-ttu-id="913fe-451">在右侧面板中的 "**邮件终结点**" 框中，输入 ngrok URL （在我们的`https://dea822bf.ngrok.io/api/messages`示例中）。</span><span class="sxs-lookup"><span data-stu-id="913fe-451">In the right panel, in the **Messaging endpoint** box, enter the ngrok URL, in our example, `https://dea822bf.ngrok.io/api/messages`.</span></span>
1. <span data-ttu-id="913fe-452">在本地启动你的 bot，例如在 Visual Studio 调试模式下。</span><span class="sxs-lookup"><span data-stu-id="913fe-452">Start your bot locally, for example in Visual Studio debug mode.</span></span>
1. <span data-ttu-id="913fe-453">使用 Bot 框架门户的**测试 Web 聊天**在本地运行时测试机器人。</span><span class="sxs-lookup"><span data-stu-id="913fe-453">Test the bot while running locally using the Bot Framework portal's **Test Web chat**.</span></span> <span data-ttu-id="913fe-454">与模拟器一样，此测试不允许您访问特定于团队的功能。</span><span class="sxs-lookup"><span data-stu-id="913fe-454">Like the Emulator, this test doesn't allow you to access Teams-specific functionality.</span></span>
1. <span data-ttu-id="913fe-455">在运行的终端窗口`ngrok`中，可以查看 bot 和 web 聊天客户端之间的 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="913fe-455">In the terminal window where `ngrok` is running you can see HTTP traffic between the bot and the web chat client.</span></span> <span data-ttu-id="913fe-456">如果需要更详细的视图，请在浏览器窗口中`http://127.0.0.1:4040`输入从以前的终端窗口中获取的。</span><span class="sxs-lookup"><span data-stu-id="913fe-456">If you want a more detailed view, in a browser window enter `http://127.0.0.1:4040` you obtained from the previous terminal window.</span></span> <span data-ttu-id="913fe-457">下面的图像是一个示例：</span><span class="sxs-lookup"><span data-stu-id="913fe-457">The following image is an example:</span></span>

    ![auth bot 团队 ngrok 测试](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png)<span data-ttu-id="913fe-459">.</span><span class="sxs-lookup"><span data-stu-id="913fe-459">.</span></span>

> [!NOTE]
> <span data-ttu-id="913fe-460">如果您停止并重新启动 ngrok，则 URL 会发生更改。</span><span class="sxs-lookup"><span data-stu-id="913fe-460">If you stop and restart ngrok, the URL changes.</span></span> <span data-ttu-id="913fe-461">若要在项目中使用 ngrok，并根据所使用的功能，必须更新所有 URL 引用。</span><span class="sxs-lookup"><span data-stu-id="913fe-461">To use ngrok in your project, and depending on the capabilities you're using, you must update all URL references.</span></span>

## <a name="additional-information"></a><span data-ttu-id="913fe-462">其他信息</span><span class="sxs-lookup"><span data-stu-id="913fe-462">Additional information</span></span>

### <a name="teamsappmanifestmanifestjson"></a><span data-ttu-id="913fe-463">TeamsAppManifest/manifest json</span><span class="sxs-lookup"><span data-stu-id="913fe-463">TeamsAppManifest/manifest.json</span></span>

<span data-ttu-id="913fe-464">此清单包含 Microsoft 团队与 bot 连接所需的信息。</span><span class="sxs-lookup"><span data-stu-id="913fe-464">This manifest contains information needed by Microsoft Teams to connect with the bot.</span></span>  

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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

<span data-ttu-id="913fe-465">通过身份验证，团队的行为与其他频道略有不同，如下所述。</span><span class="sxs-lookup"><span data-stu-id="913fe-465">With authentication, Teams behaves slightly differently than other channels, as explained below.</span></span>

### <a name="handling-invoke-activity"></a><span data-ttu-id="913fe-466">处理调用活动</span><span class="sxs-lookup"><span data-stu-id="913fe-466">Handling Invoke Activity</span></span>

<span data-ttu-id="913fe-467">**调用活动**将发送到 bot，而不是其他通道使用的事件活动。</span><span class="sxs-lookup"><span data-stu-id="913fe-467">An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.</span></span>
<span data-ttu-id="913fe-468">这是通过**ActivityHandler**的 classing 完成的。</span><span class="sxs-lookup"><span data-stu-id="913fe-468">This is done by sub-classing the **ActivityHandler**.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="913fe-469">C #/.NET</span><span class="sxs-lookup"><span data-stu-id="913fe-469">C#/.NET</span></span>](#tab/dotnet-sample)

<span data-ttu-id="913fe-470">**Bot/DialogBot**</span><span class="sxs-lookup"><span data-stu-id="913fe-470">**Bots/DialogBot.cs**</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

<span data-ttu-id="913fe-471">**Bot/TeamsBot**</span><span class="sxs-lookup"><span data-stu-id="913fe-471">**Bots/TeamsBot.cs**</span></span>

<span data-ttu-id="913fe-472">如果使用了**OAuthPrompt** ，则必须将*调用活动*转发到对话框。</span><span class="sxs-lookup"><span data-stu-id="913fe-472">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a><span data-ttu-id="913fe-473">TeamsActivityHandler.cs</span><span class="sxs-lookup"><span data-stu-id="913fe-473">TeamsActivityHandler.cs</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="913fe-474">JavaScript</span><span class="sxs-lookup"><span data-stu-id="913fe-474">JavaScript</span></span>](#tab/node-js-dialog-sample)

<span data-ttu-id="913fe-475">**bot/dialogBot**</span><span class="sxs-lookup"><span data-stu-id="913fe-475">**bots/dialogBot.js**</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

<span data-ttu-id="913fe-476">**bot/teamsBot**</span><span class="sxs-lookup"><span data-stu-id="913fe-476">**bots/teamsBot.js**</span></span>

<span data-ttu-id="913fe-477">如果使用了**OAuthPrompt** ，则必须将*调用活动*转发到对话框。</span><span class="sxs-lookup"><span data-stu-id="913fe-477">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

<span data-ttu-id="913fe-478">**对话框/mainDialog**</span><span class="sxs-lookup"><span data-stu-id="913fe-478">**dialogs/mainDialog.js**</span></span>

<span data-ttu-id="913fe-479">在对话步骤中，使用`beginDialog` "" 启动 OAuth 提示，这将要求用户登录。</span><span class="sxs-lookup"><span data-stu-id="913fe-479">Within a dialog step, use `beginDialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="913fe-480">如果用户已登录，则会生成令牌响应事件，而不会提示用户。</span><span class="sxs-lookup"><span data-stu-id="913fe-480">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="913fe-481">否则，这将提示用户登录。</span><span class="sxs-lookup"><span data-stu-id="913fe-481">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="913fe-482">Azure Bot 服务在用户尝试登录后发送令牌响应事件。</span><span class="sxs-lookup"><span data-stu-id="913fe-482">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

<span data-ttu-id="913fe-483">在下面的对话框步骤中，检查上一步的结果中是否存在令牌。</span><span class="sxs-lookup"><span data-stu-id="913fe-483">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="913fe-484">如果不为 null，则用户已成功登录。</span><span class="sxs-lookup"><span data-stu-id="913fe-484">If it is not null, the user successfully signed in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

<span data-ttu-id="913fe-485">**bot/logoutDialog**</span><span class="sxs-lookup"><span data-stu-id="913fe-485">**bots/logoutDialog.js**</span></span>

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[<span data-ttu-id="913fe-486">Python</span><span class="sxs-lookup"><span data-stu-id="913fe-486">Python</span></span>](#tab/python-sample)

<span data-ttu-id="913fe-487">**bot/dialog_bot py**</span><span class="sxs-lookup"><span data-stu-id="913fe-487">**bots/dialog_bot.py**</span></span>

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

<span data-ttu-id="913fe-488">**bot/teams_bot py**</span><span class="sxs-lookup"><span data-stu-id="913fe-488">**bots/teams_bot.py**</span></span>

<span data-ttu-id="913fe-489">如果使用了**OAuthPrompt** ，则必须将*调用活动*转发到对话框。</span><span class="sxs-lookup"><span data-stu-id="913fe-489">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

<span data-ttu-id="913fe-490">**对话框/main_dialog py**</span><span class="sxs-lookup"><span data-stu-id="913fe-490">**dialogs/main_dialog.py**</span></span>

<span data-ttu-id="913fe-491">在对话步骤中，使用`begin_dialog` "" 启动 OAuth 提示，这将要求用户登录。</span><span class="sxs-lookup"><span data-stu-id="913fe-491">Within a dialog step, use `begin_dialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="913fe-492">如果用户已登录，则会生成令牌响应事件，而不会提示用户。</span><span class="sxs-lookup"><span data-stu-id="913fe-492">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="913fe-493">否则，这将提示用户登录。</span><span class="sxs-lookup"><span data-stu-id="913fe-493">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="913fe-494">Azure Bot 服务在用户尝试登录后发送令牌响应事件。</span><span class="sxs-lookup"><span data-stu-id="913fe-494">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

<span data-ttu-id="913fe-495">在下面的对话框步骤中，检查上一步的结果中是否存在令牌。</span><span class="sxs-lookup"><span data-stu-id="913fe-495">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="913fe-496">如果不为 null，则用户已成功登录。</span><span class="sxs-lookup"><span data-stu-id="913fe-496">If it is not null, the user successfully signed in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

<span data-ttu-id="913fe-497">**对话框/logout_dialog py**</span><span class="sxs-lookup"><span data-stu-id="913fe-497">**dialogs/logout_dialog.py**</span></span>

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

> [!div class="nextstepaction"]
> [<span data-ttu-id="913fe-498">了解如何通过 Azure Bot 服务添加身份验证</span><span class="sxs-lookup"><span data-stu-id="913fe-498">Learn about adding adding authentication via Azure Bot Service</span></span>](https://aka.ms/azure-bot-add-authentication)

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
