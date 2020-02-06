---
title: 为 Microsoft Teams 创建自动程序
author: clearab
description: 如何为 Microsoft Teams 创建自动程序。
ms.topic: conceptual
localization_priority: Priority
ms.author: anclear
ms.openlocfilehash: 9e0bd603772cf4da8465a638c4a7f5b426a1fbfb
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673392"
---
# <a name="create-a-bot-for-microsoft-teams"></a><span data-ttu-id="a6d98-103">为 Microsoft Teams 创建自动程序</span><span class="sxs-lookup"><span data-stu-id="a6d98-103">Create a bot for Microsoft Teams</span></span>

<span data-ttu-id="a6d98-104">需要完成以下步骤才能创建对话自动程序：</span><span class="sxs-lookup"><span data-stu-id="a6d98-104">You'll need to complete the following steps to create a conversational bot:</span></span>

1. <span data-ttu-id="a6d98-105">准备开发环境。</span><span class="sxs-lookup"><span data-stu-id="a6d98-105">Prepare your development environment.</span></span>
1. <span data-ttu-id="a6d98-106">创建 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="a6d98-106">Create your web service.</span></span>
1. <span data-ttu-id="a6d98-107">使用 Microsoft Bot Framework 将你的 Web 服务注册为自动程序。</span><span class="sxs-lookup"><span data-stu-id="a6d98-107">Register your web service as a bot with Microsoft Bot Framework.</span></span>
1. <span data-ttu-id="a6d98-108">创建应用程序清单和应用程序包。</span><span class="sxs-lookup"><span data-stu-id="a6d98-108">Create your app manifest and your app package.</span></span>
1. <span data-ttu-id="a6d98-109">将程序包上传到 Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="a6d98-109">Upload your package to Microsoft Teams.</span></span>

<span data-ttu-id="a6d98-110">可使用 Bot Framework 按照任何顺序创建 Web 服务、注册 Web 服务和创建应用程序包：但是，由于这三个部分交织在一起，因此无论按什么顺序执行操作，都需要返回以更新其他部分。</span><span class="sxs-lookup"><span data-stu-id="a6d98-110">Creating your web service, registering your web service, and creating your app package, with the Bot Framework can be done in any order; however, because the three pieces are so intertwined, no matter in which order you do them, you'll need to return to update the others.</span></span> <span data-ttu-id="a6d98-111">注册需要来自部署的 Web 服务的消息传递终结点，并且 Web 服务需要从注册中创建的 ID 和密码。</span><span class="sxs-lookup"><span data-stu-id="a6d98-111">Your registration needs the messaging endpoint from your deployed web service and your web service needs the ID and password created from your registration.</span></span> <span data-ttu-id="a6d98-112">应用程序清单还需要注册 ID 才能将 Teams 连接到 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="a6d98-112">Your app manifest also needs the registration ID to connect Teams to your web service.</span></span>

<span data-ttu-id="a6d98-113">构建自动程序时，你将定期在更改应用程序清单与将代码部署到 Web 服务之间切换。</span><span class="sxs-lookup"><span data-stu-id="a6d98-113">As you're building your bot, you'll regularly move between changing your app manifest and deploying code to your web service.</span></span> <span data-ttu-id="a6d98-114">使用应用程序清单时，请记住，你可以手动操作 JSON 文件，也可以通过 App Studio 进行更改。</span><span class="sxs-lookup"><span data-stu-id="a6d98-114">When working with the app manifest, keep in mind you can either manually manipulate the JSON file, or make changes through App Studio.</span></span> <span data-ttu-id="a6d98-115">无论采用哪种方法，当你对清单进行更改时，都需要在 Teams 中重新部署（上传）你的应用；但是，在将更改部署到 Web 服务时无需这样做。</span><span class="sxs-lookup"><span data-stu-id="a6d98-115">Either way, you'll need to re-deploy (upload) your app in Teams when you make a change to the manifest; however, there's no need to do so when you deploy changes to your web service.</span></span>

<span data-ttu-id="a6d98-116">有关 Bot Framework 的其他信息，请参阅 [Bot Framework 文档](/azure/bot-service/)。</span><span class="sxs-lookup"><span data-stu-id="a6d98-116">See the [Bot Framework Documentation](/azure/bot-service/) for additional information on the Bot Framework.</span></span>

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a><span data-ttu-id="a6d98-117">创建 Web 服务</span><span class="sxs-lookup"><span data-stu-id="a6d98-117">Create your web service</span></span>

<span data-ttu-id="a6d98-118">自动程序的核心是 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="a6d98-118">The heart of your bot is your web service.</span></span> <span data-ttu-id="a6d98-119">它将定义用于接收所有请求的路由，通常为 `/api/messages`。</span><span class="sxs-lookup"><span data-stu-id="a6d98-119">It will define a single route, typically `/api/messages`, on which to receive all requests.</span></span> <span data-ttu-id="a6d98-120">若要开始，可选择以下选项之一：</span><span class="sxs-lookup"><span data-stu-id="a6d98-120">To get started, you have a few options to choose from:</span></span>

* <span data-ttu-id="a6d98-121">从采用 [C#/dotnet](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot) 或 [JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) 编写的 Teams 对话自动程序示例开始。</span><span class="sxs-lookup"><span data-stu-id="a6d98-121">Start with the Teams conversation bot sample in either [C#/dotnet](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot) or [JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot).</span></span>
* <span data-ttu-id="a6d98-122">如果你使用的是 JavaScript，请使用[适用于 Microsoft Teams 的 Yeoman 生成器](https://github.com/OfficeDev/generator-teams)来搭建 Teams 应用，包括你的 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="a6d98-122">If you're using JavaScript, use the [Yeoman Generator for Microsoft Teams](https://github.com/OfficeDev/generator-teams) to scaffold your Teams app, including your web service.</span></span> <span data-ttu-id="a6d98-123">当构建包含多个对话自动程序的 Teams 应用时，它尤其有用。</span><span class="sxs-lookup"><span data-stu-id="a6d98-123">This is particularly helpful when building a Teams app that contains more than just a conversational bot.</span></span>
* <span data-ttu-id="a6d98-124">从头开始创建 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="a6d98-124">Create your web service from scratch.</span></span> <span data-ttu-id="a6d98-125">可选择添加面向你的语言的 Bot Framework SDK，也可以直接使用 JSON 有效负载。</span><span class="sxs-lookup"><span data-stu-id="a6d98-125">You can choose to add the Bot Framework SDK for your language, or you can work directly with the JSON payloads.</span></span>

## <a name="register-your-web-service-with-the-bot-framework"></a><span data-ttu-id="a6d98-126">使用 Bot Framework 注册你的 Web 服务</span><span class="sxs-lookup"><span data-stu-id="a6d98-126">Register your web service with the Bot Framework</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a6d98-127">注册 Web 服务时，请确保将**显示名称**设置为与应用程序清单中的**简短名称**相同的名称。</span><span class="sxs-lookup"><span data-stu-id="a6d98-127">When registering your web service, be sure to set the **Display name** to the same name you used for your **Short name** in your app manifest.</span></span> <span data-ttu-id="a6d98-128">通过直接上传或利用组织的应用程序目录分发应用程序时，由自动程序发送到对话的消息将使用注册的**显示名称**，而不是应用程序的**简短名称**。</span><span class="sxs-lookup"><span data-stu-id="a6d98-128">When your app is distributed by either direct uploading or through an organization's app catalog, messages sent to a conversation by your bot will use the registration's **Display name** rather than the app's **Short name**.</span></span>

<span data-ttu-id="a6d98-129">通过使用 Bot Framework 来注册 Web 服务，可在 Teams 客户端与 Web 服务之间建立安全的通信通道。</span><span class="sxs-lookup"><span data-stu-id="a6d98-129">Registering your web service with the Bot Framework provides a secure communication channel between the Teams client and your web service.</span></span> <span data-ttu-id="a6d98-130">Teams 客户端与 Web 服务永远不会直接通信。</span><span class="sxs-lookup"><span data-stu-id="a6d98-130">The Teams client and your web service never communicate directly.</span></span> <span data-ttu-id="a6d98-131">相反，消息通过 Bot Framework Service 进行路由（Microsoft Teams 使用此服务的单独实例，它符合 Office 365 标准）。</span><span class="sxs-lookup"><span data-stu-id="a6d98-131">Instead, messages are routed through the Bot Framework Service (Microsoft Teams uses a separate instance of this service that is compliant with Office 365 standards).</span></span>

<span data-ttu-id="a6d98-132">使用 Bot Framework 注册 Web 服务时，有两个选项可供选择。</span><span class="sxs-lookup"><span data-stu-id="a6d98-132">You have two options when registering your web service with the Bot Framework.</span></span> <span data-ttu-id="a6d98-133">可以使用 [App Studio](#using-app-studio) 或[旧门户](#in-the-legacy-portal)来注册你的自动程序，而无需使用 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="a6d98-133">You can use either [App Studio](#using-app-studio) or the [legacy portal](#in-the-legacy-portal) to register your bot without using an Azure subscription.</span></span> <span data-ttu-id="a6d98-134">或者，如果你已拥有 Azure 订阅（或者不介意创建一个），则可以使用 [Azure 门户](#with-an-azure-subscription)来注册 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="a6d98-134">Or, if you already have an Azure subscription (or don't mind creating one), you can use [the Azure portal](#with-an-azure-subscription) to register your web service.</span></span>

### <a name="without-an-azure-subscription"></a><span data-ttu-id="a6d98-135">无 Azure 订阅</span><span class="sxs-lookup"><span data-stu-id="a6d98-135">Without an Azure subscription</span></span>

<span data-ttu-id="a6d98-136">如果你不想在 Azure 中创建自动程序注册，则**必须**使用此链接 - https://dev.botframework.com/bots/new 或 App Studio。</span><span class="sxs-lookup"><span data-stu-id="a6d98-136">If you do not wish to create your bot registration in Azure, you **must** use either this link - https://dev.botframework.com/bots/new, or App Studio.</span></span> <span data-ttu-id="a6d98-137">如果单击 Bot Framework 门户中的“*创建自动程序*”按钮，将在 Microsoft Azure 中创建自动程序注册，并且需要提供 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="a6d98-137">If you click on the *Create a bot* button in the Bot Framework portal, you will create your bot registration in Microsoft Azure, and will need to provide an Azure subscription.</span></span> <span data-ttu-id="a6d98-138">若要在创建后管理注册或将其迁移到 Azure 订阅，请转到：https://dev.botframework.com/bots。</span><span class="sxs-lookup"><span data-stu-id="a6d98-138">To manage your registration or migrate it to an Azure subscription after creation go to: https://dev.botframework.com/bots.</span></span>

<span data-ttu-id="a6d98-139">当你编辑未在 Azure 中注册的现有 Bot Framework 注册的属性时，你将看到“迁移状态”列和蓝色“迁移”按钮，该按钮会将你带到 Microsoft Azure 门户。</span><span class="sxs-lookup"><span data-stu-id="a6d98-139">When you edit the properties of an existing Bot Framework registration not registered in Azure, you'll see A "Migration status" column and a blue "Migrate" button that will take you to the Microsoft Azure portal.</span></span> <span data-ttu-id="a6d98-140">除非你希望这样做，否则不要选择“迁移”按钮。</span><span class="sxs-lookup"><span data-stu-id="a6d98-140">Don't select the "Migrate" button unless that's what you want to do.</span></span> <span data-ttu-id="a6d98-141">相反，请选择自动程序的**名称**，然后可以编辑其属性：</span><span class="sxs-lookup"><span data-stu-id="a6d98-141">Instead, select the **name** of the bot and you can edit its properties:</span></span>

   ![编辑自动程序属性](~/assets/images/bots/bf-migrate-bot-to-azure.png)

<span data-ttu-id="a6d98-143">**必须**在 Azure 中注册自动程序（通过在 Azure 门户中创建或通过迁移）的应用场景：</span><span class="sxs-lookup"><span data-stu-id="a6d98-143">Scenarios when you **must** have your bot registration in Azure (either by creating it in the Azure portal or via migration):</span></span>

* <span data-ttu-id="a6d98-144">你希望使用 Bot Framework 的 [OAuthPrompt](./authentication/auth-flow-bot.md) 进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="a6d98-144">You want to use the Bot Framework's [OAuthPrompt](./authentication/auth-flow-bot.md) for authentication.</span></span>
* <span data-ttu-id="a6d98-145">你希望启用其他频道，例如网上聊天、Direct Line 或 Skype。</span><span class="sxs-lookup"><span data-stu-id="a6d98-145">You want to enable additional channels like Web Chat, Direct Line, or Skype.</span></span>

#### <a name="using-app-studio"></a><span data-ttu-id="a6d98-146">使用 App Studio</span><span class="sxs-lookup"><span data-stu-id="a6d98-146">Using App Studio</span></span>

<span data-ttu-id="a6d98-147">*App Studio* 是一种 Teams 应用，可帮助你构建 Teams 应用，包括将 Web 服务注册为自动程序、创建应用程序清单和应用程序包。</span><span class="sxs-lookup"><span data-stu-id="a6d98-147">*App Studio* is a Teams app that helps you build Teams apps, including registering your web service as a bot, creating an app manifest, and your app package.</span></span> <span data-ttu-id="a6d98-148">它还包含 React 控件库和卡的可配置示例。</span><span class="sxs-lookup"><span data-stu-id="a6d98-148">It also contains a React control library and configurable samples for cards.</span></span> <span data-ttu-id="a6d98-149">请参阅[开始使用 Teams App Studio](../../concepts/build-and-test/app-studio-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a6d98-149">See [Getting started with Teams App Studio](../../concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="a6d98-150">请记住，如果使用 App Studio 注册你的 Web 服务，则需要转到 https://dev.botframework.com/bots 以管理你的注册。</span><span class="sxs-lookup"><span data-stu-id="a6d98-150">Remember, if you use App Studio to register your web service you'll need to go to https://dev.botframework.com/bots to manage your registration.</span></span> <span data-ttu-id="a6d98-151">某些设置（例如你的消息传递终结点）也可以在 App Studio 中进行更新。</span><span class="sxs-lookup"><span data-stu-id="a6d98-151">Some settings (like your messaging endpoint) can be updated in App Studio as well.</span></span>

#### <a name="in-the-legacy-portal"></a><span data-ttu-id="a6d98-152">在旧门户中</span><span class="sxs-lookup"><span data-stu-id="a6d98-152">In the legacy portal</span></span>

<span data-ttu-id="a6d98-153">使用此链接创建自动程序注册：https://dev.botframework.com/bots/new。</span><span class="sxs-lookup"><span data-stu-id="a6d98-153">Create your bot registration using this link: https://dev.botframework.com/bots/new.</span></span> <span data-ttu-id="a6d98-154">**创建自动程序后，请确保从特色频道列表中将 Microsoft Teams 添加为频道。**</span><span class="sxs-lookup"><span data-stu-id="a6d98-154">**Be sure to add Microsoft Teams as a channel from the featured channels list after creating your bot.**</span></span> <span data-ttu-id="a6d98-155">如果你已经创建应用程序包/清单，请随意重复使用你生成的任何 Microsoft 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="a6d98-155">Feel free to re-use any Microsoft App ID you generated if you've already created your app package/manifest.</span></span>

   ![Bot Framework 注册页面](~/assets/images/bots/bfregister.png)

### <a name="with-an-azure-subscription"></a><span data-ttu-id="a6d98-157">拥有 Azure 订阅</span><span class="sxs-lookup"><span data-stu-id="a6d98-157">With an Azure subscription</span></span>

<span data-ttu-id="a6d98-158">你还可以通过在 Azure 门户中创建“自动程序频道注册”资源来注册 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="a6d98-158">You can also register your web service by creating a Bot Channels Registration resource in the Azure portal.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

<span data-ttu-id="a6d98-159">[Bot Framework 门户](https://dev.botframework.com)已针对在 Microsoft Azure 中注册自动程序进行了优化。</span><span class="sxs-lookup"><span data-stu-id="a6d98-159">The [Bot Framework portal](https://dev.botframework.com) is optimized for registering bots in Microsoft Azure.</span></span> <span data-ttu-id="a6d98-160">以下是几个注意事项：</span><span class="sxs-lookup"><span data-stu-id="a6d98-160">Here are some things to know:</span></span>

* <span data-ttu-id="a6d98-161">在 Azure 中注册的自动程序的 Microsoft Teams 频道是**免费**的。</span><span class="sxs-lookup"><span data-stu-id="a6d98-161">The Microsoft Teams channel for bots registered on Azure is **free**.</span></span> <span data-ttu-id="a6d98-162">通过 Teams 渠道发送的消息将不会计入自动程序使用的消息中。</span><span class="sxs-lookup"><span data-stu-id="a6d98-162">Messages sent over the Teams channel will NOT count towards the consumed messages for the bot.</span></span>
* <span data-ttu-id="a6d98-163">如果你使用 Microsoft Azure 注册自动程序，则无需在 Microsoft Azure 上*托管*自动程序代码。</span><span class="sxs-lookup"><span data-stu-id="a6d98-163">If you register your bot using Microsoft Azure, your bot code doesn't need to be *hosted* on Microsoft Azure.</span></span>
* <span data-ttu-id="a6d98-164">如果你使用 Microsoft Azure 门户注册自动程序，则必须拥有 Microsoft Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="a6d98-164">If you do register a bot using Microsoft Azure portal, you must have a Microsoft Azure account.</span></span> <span data-ttu-id="a6d98-165">你可以[免费创建一个](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="a6d98-165">You can [create one for free](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="a6d98-166">若要在创建 Azure 帐户时验证你的身份，必须提供信用卡，但不会收费；在 Microsoft Teams 中创建和使用自动程序始终是免费的。</span><span class="sxs-lookup"><span data-stu-id="a6d98-166">To verify your identity when you create an Azure account, you must provide a credit card, but it won't be charged; it's always free to create and use bots with Microsoft Teams.</span></span>

## <a name="create-your-app-manifest-and-package"></a><span data-ttu-id="a6d98-167">创建应用程序清单和程序包</span><span class="sxs-lookup"><span data-stu-id="a6d98-167">Create your app manifest and package</span></span>

<span data-ttu-id="a6d98-168">[应用程序清单](~/resources/schema/manifest-schema.md)定义了应用程序的元数据、应用程序正在使用的扩展点以及指向这些扩展点连接到的 Web 服务的指针。</span><span class="sxs-lookup"><span data-stu-id="a6d98-168">Your [app manifest](~/resources/schema/manifest-schema.md) defines the metadata for your app, the extension points your app is using, and pointers to the web services those extension points connect to.</span></span> <span data-ttu-id="a6d98-169">你可以使用 App Studio 帮助创建应用程序清单，也可以手动创建。</span><span class="sxs-lookup"><span data-stu-id="a6d98-169">You can either use App Studio to help you create your app manifest, or create it manually.</span></span>

### <a name="add-using-app-studio"></a><span data-ttu-id="a6d98-170">使用 App Studio 添加</span><span class="sxs-lookup"><span data-stu-id="a6d98-170">Add using App Studio</span></span>

1. <span data-ttu-id="a6d98-171">在 Teams 客户端中，从左侧导航栏上的“**…**”溢出菜单中打开 App Studio。</span><span class="sxs-lookup"><span data-stu-id="a6d98-171">In the Teams client, open App Studio from the **...** overflow menu on the left navigation rail.</span></span> <span data-ttu-id="a6d98-172">如果尚未安装 App Studio，则可以通过搜索它来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="a6d98-172">If App Studio isn't already installed, you can do so by searching for it.</span></span>
2. <span data-ttu-id="a6d98-173">在“**清单编辑器**”选项卡上，选择“**创建新应用**”（或者，如果要将自动程序添加到现有应用中，则可以导入应用程序包）</span><span class="sxs-lookup"><span data-stu-id="a6d98-173">On the **Manifest editor** tab select **Create a new app** (or if you're adding a bot to an existing app, you can import your app package)</span></span>
3. <span data-ttu-id="a6d98-174">添加应用详细信息（有关每个字段的完整说明，请参阅[清单架构定义](~/resources/schema/manifest-schema.md)）。</span><span class="sxs-lookup"><span data-stu-id="a6d98-174">Add your app details (see [manifest schema definition](~/resources/schema/manifest-schema.md) for full descriptions of each field).</span></span>
4. <span data-ttu-id="a6d98-175">在“**自动程序**”选项卡上，选择“**设置**”按钮。</span><span class="sxs-lookup"><span data-stu-id="a6d98-175">On the **Bots** tab select the **Setup** button.</span></span>
5. <span data-ttu-id="a6d98-176">你可以创建新的 Web 服务注册（**新自动程序**），或者如果已经注册了一个，请选择**现有自动程序**。</span><span class="sxs-lookup"><span data-stu-id="a6d98-176">You can either create a new web service registration (**New bot**), or if you've already registered one, select **Existing bot**.</span></span>
6. <span data-ttu-id="a6d98-177">选择自动程序所需的功能和作用域。</span><span class="sxs-lookup"><span data-stu-id="a6d98-177">Select the capabilities and scopes your bot will need.</span></span>
7. <span data-ttu-id="a6d98-178">如有必要，请更新自动程序终结点地址以指向你的自动程序。</span><span class="sxs-lookup"><span data-stu-id="a6d98-178">If necessary, update your bot endpoint address to point to your bot.</span></span> <span data-ttu-id="a6d98-179">它应该类似于 `https://someplace.com/api/messages`。</span><span class="sxs-lookup"><span data-stu-id="a6d98-179">It should look something like `https://someplace.com/api/messages`.</span></span>
8. <span data-ttu-id="a6d98-180">（可选）添加[自动程序命令](~/bots/how-to/create-a-bot-commands-menu.md)。</span><span class="sxs-lookup"><span data-stu-id="a6d98-180">Optionally, add [bot commands](~/bots/how-to/create-a-bot-commands-menu.md).</span></span>
9. <span data-ttu-id="a6d98-181">（可选）你可以从“**测试和分发**”选项卡下载完整的应用程序包。</span><span class="sxs-lookup"><span data-stu-id="a6d98-181">Optionally, you can download your completed app package from the **Test and distribute** tab.</span></span>

### <a name="create-it-manually"></a><span data-ttu-id="a6d98-182">手动创建</span><span class="sxs-lookup"><span data-stu-id="a6d98-182">Create it manually</span></span>

<span data-ttu-id="a6d98-183">与消息传递扩展和选项卡一样，你可以更新[应用程序清单](~/resources/schema/manifest-schema.md)以定义你的自动程序。</span><span class="sxs-lookup"><span data-stu-id="a6d98-183">As with messaging extensions and tabs, you update the [app-manifest](~/resources/schema/manifest-schema.md) to define your bot.</span></span> <span data-ttu-id="a6d98-184">使用 `bots` 属性在你的应用程序清单中添加新的顶级 JSON 结构。</span><span class="sxs-lookup"><span data-stu-id="a6d98-184">Add new top-level JSON structure in your app manifest with the `bots` property.</span></span>

|<span data-ttu-id="a6d98-185">姓名</span><span class="sxs-lookup"><span data-stu-id="a6d98-185">Name</span></span>| <span data-ttu-id="a6d98-186">类型</span><span class="sxs-lookup"><span data-stu-id="a6d98-186">Type</span></span>| <span data-ttu-id="a6d98-187">最大大小</span><span class="sxs-lookup"><span data-stu-id="a6d98-187">Maximum size</span></span> | <span data-ttu-id="a6d98-188">必需</span><span class="sxs-lookup"><span data-stu-id="a6d98-188">Required</span></span> | <span data-ttu-id="a6d98-189">说明</span><span class="sxs-lookup"><span data-stu-id="a6d98-189">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="a6d98-190">字符串</span><span class="sxs-lookup"><span data-stu-id="a6d98-190">String</span></span>|<span data-ttu-id="a6d98-191">64 个字符</span><span class="sxs-lookup"><span data-stu-id="a6d98-191">64 characters</span></span>|<span data-ttu-id="a6d98-192">✔</span><span class="sxs-lookup"><span data-stu-id="a6d98-192">✔</span></span>|<span data-ttu-id="a6d98-193">使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="a6d98-193">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="a6d98-194">它可能与整个应用 ID 相同。</span><span class="sxs-lookup"><span data-stu-id="a6d98-194">This may well be the same as the overall app ID.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="a6d98-195">布尔值</span><span class="sxs-lookup"><span data-stu-id="a6d98-195">Boolean</span></span>|||<span data-ttu-id="a6d98-196">描述自动程序是否利用用户提示将自动程序添加到特定频道。</span><span class="sxs-lookup"><span data-stu-id="a6d98-196">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="a6d98-197">默认值：`false`。</span><span class="sxs-lookup"><span data-stu-id="a6d98-197">Default: `false`.</span></span>|
|`isNotificationOnly`|<span data-ttu-id="a6d98-198">布尔值</span><span class="sxs-lookup"><span data-stu-id="a6d98-198">Boolean</span></span>|||<span data-ttu-id="a6d98-199">指示自动程序是否为单向、仅通知的自动程序，而不是对话自动程序。</span><span class="sxs-lookup"><span data-stu-id="a6d98-199">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="a6d98-200">默认值：`false`。</span><span class="sxs-lookup"><span data-stu-id="a6d98-200">Default: `false`.</span></span>|
|`supportsFiles`|<span data-ttu-id="a6d98-201">布尔值</span><span class="sxs-lookup"><span data-stu-id="a6d98-201">Boolean</span></span>|||<span data-ttu-id="a6d98-202">指示自动程序是否支持在个人聊天中上传/下载文件。</span><span class="sxs-lookup"><span data-stu-id="a6d98-202">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="a6d98-203">默认值：`false`。</span><span class="sxs-lookup"><span data-stu-id="a6d98-203">Default: `false`.</span></span>|
|`scopes`|<span data-ttu-id="a6d98-204">枚举数组</span><span class="sxs-lookup"><span data-stu-id="a6d98-204">Array of enum</span></span>|<span data-ttu-id="a6d98-205">3</span><span class="sxs-lookup"><span data-stu-id="a6d98-205">3</span></span>|<span data-ttu-id="a6d98-206">✔</span><span class="sxs-lookup"><span data-stu-id="a6d98-206">✔</span></span>|<span data-ttu-id="a6d98-207">指定自动程序是在 `team` 内的频道上下文中提供体验、在群组聊天 (`groupchat`) 中提供体验，还是仅在单个用户 (`personal`) 范围内提供体验。</span><span class="sxs-lookup"><span data-stu-id="a6d98-207">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="a6d98-208">这些选项不具排他性。</span><span class="sxs-lookup"><span data-stu-id="a6d98-208">These options are non-exclusive.</span></span>|

<span data-ttu-id="a6d98-209">（可选）你可以定义由自动程序向用户推荐的一个或多个命令列表。</span><span class="sxs-lookup"><span data-stu-id="a6d98-209">Optionally, you can define one or more lists of commands that your bot can recommend to users.</span></span> <span data-ttu-id="a6d98-210">对象是一个数组（最多 2 个元素），所有元素的类型均为 `object`。</span><span class="sxs-lookup"><span data-stu-id="a6d98-210">The object is an array (maximum of 2 elements) with all elements of type `object`.</span></span> <span data-ttu-id="a6d98-211">你必须为自动程序支持的每个作用域定义一个单独的命令列表。</span><span class="sxs-lookup"><span data-stu-id="a6d98-211">You must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="a6d98-212">有关详细信息，*请参阅*[自动程序菜单](./create-a-bot-commands-menu.md)。</span><span class="sxs-lookup"><span data-stu-id="a6d98-212">*See* [Bot menus](./create-a-bot-commands-menu.md), for more information.</span></span>

|<span data-ttu-id="a6d98-213">姓名</span><span class="sxs-lookup"><span data-stu-id="a6d98-213">Name</span></span>| <span data-ttu-id="a6d98-214">类型</span><span class="sxs-lookup"><span data-stu-id="a6d98-214">Type</span></span>| <span data-ttu-id="a6d98-215">最大大小</span><span class="sxs-lookup"><span data-stu-id="a6d98-215">Maximum size</span></span> | <span data-ttu-id="a6d98-216">必需</span><span class="sxs-lookup"><span data-stu-id="a6d98-216">Required</span></span> | <span data-ttu-id="a6d98-217">说明</span><span class="sxs-lookup"><span data-stu-id="a6d98-217">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="a6d98-218">枚举数组</span><span class="sxs-lookup"><span data-stu-id="a6d98-218">array of enum</span></span>|<span data-ttu-id="a6d98-219">3</span><span class="sxs-lookup"><span data-stu-id="a6d98-219">3</span></span>|<span data-ttu-id="a6d98-220">✔</span><span class="sxs-lookup"><span data-stu-id="a6d98-220">✔</span></span>|<span data-ttu-id="a6d98-221">指定命令列表有效的作用域。</span><span class="sxs-lookup"><span data-stu-id="a6d98-221">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="a6d98-222">选项包括 `team`、`personal` 和 `groupchat`。</span><span class="sxs-lookup"><span data-stu-id="a6d98-222">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="a6d98-223">对象数组</span><span class="sxs-lookup"><span data-stu-id="a6d98-223">array of objects</span></span>|<span data-ttu-id="a6d98-224">10</span><span class="sxs-lookup"><span data-stu-id="a6d98-224">10</span></span>|<span data-ttu-id="a6d98-225">✔</span><span class="sxs-lookup"><span data-stu-id="a6d98-225">✔</span></span>|<span data-ttu-id="a6d98-226">自动程序支持的命令数组：</span><span class="sxs-lookup"><span data-stu-id="a6d98-226">An array of commands the bot supports:</span></span><br><span data-ttu-id="a6d98-227">`title`：自动程序命令名称（字符串，32）</span><span class="sxs-lookup"><span data-stu-id="a6d98-227">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="a6d98-228">`description`：命令语法及其参数的简单描述或示例（字符串，128）</span><span class="sxs-lookup"><span data-stu-id="a6d98-228">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

#### <a name="simple-manifest-example"></a><span data-ttu-id="a6d98-229">简单清单示例</span><span class="sxs-lookup"><span data-stu-id="a6d98-229">Simple manifest example</span></span>

<span data-ttu-id="a6d98-230">下面的示例是一个简单的自动程序对象，其中定义了两个命令列表。</span><span class="sxs-lookup"><span data-stu-id="a6d98-230">The example below is a simple bot object, with two command lists defined.</span></span> <span data-ttu-id="a6d98-231">这不是整个应用程序清单文件，只是特定于消息传递扩展的部分。</span><span class="sxs-lookup"><span data-stu-id="a6d98-231">This is not the entire app manifest file, just the part specific to messaging extensions.</span></span>

```json
...
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "scopes": [ "team", "personal", "groupchat" ],
      "supportsFiles": true,
      "commandLists": [
        {
          "scopes": [ "team", "groupchat" ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command N",
              "description": "Description of Command N"
            }
          ]
        },
        {
          "scopes": [ "personal", "groupchat" ],
          "commands": [
            {
              "title": "Personal command 1",
              "description": "Description of Personal command 1"
            },
            {
              "title": "Personal command N",
              "description": "Description of Personal command N"
            }
          ]
        }
      ]
    }
  ],
...
```

#### <a name="create-your-app-package-manually"></a><span data-ttu-id="a6d98-232">手动创建应用程序包</span><span class="sxs-lookup"><span data-stu-id="a6d98-232">Create your app package manually</span></span>

<span data-ttu-id="a6d98-233">若要创建应用程序包，你需要将应用程序清单和（可选）应用程序图标添加到 .zip 存档文件中。</span><span class="sxs-lookup"><span data-stu-id="a6d98-233">To create an app package, you need to add your app manifest and (optionally) your app icons to a .zip archive file.</span></span> <span data-ttu-id="a6d98-234">有关完整详细信息，请参阅[创建应用程序包](~/concepts/build-and-test/apps-package.md)。</span><span class="sxs-lookup"><span data-stu-id="a6d98-234">See [Create your app package](~/concepts/build-and-test/apps-package.md) for complete details.</span></span> <span data-ttu-id="a6d98-235">请确保 .zip 存档文件仅包含必需的文件，并且内部没有其他文件夹结构。</span><span class="sxs-lookup"><span data-stu-id="a6d98-235">Make sure your .zip archive contains only the necessary files, and has no additional folder structure inside of it.</span></span>

## <a name="upload-your-package-to-microsoft-teams"></a><span data-ttu-id="a6d98-236">将你的程序包上传到 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a6d98-236">Upload your package to Microsoft Teams</span></span>

<span data-ttu-id="a6d98-237">如果你一直在使用 App Studio，则可以从**清单编辑器**的“**测试和分发**”选项卡中安装应用。</span><span class="sxs-lookup"><span data-stu-id="a6d98-237">If you've been using App Studio, you can install your app from the **Test and distribute** tab of the **Manifest editor**.</span></span> <span data-ttu-id="a6d98-238">或者，你也可以通过以下方法安装应用程序包，即单击左侧导航栏中的 `...` 溢出菜单，单击“**更多应用**”，然后单击“**上载自定义应用**”链接。</span><span class="sxs-lookup"><span data-stu-id="a6d98-238">Alternatively, you can install your app package by clicking the `...` overflow menu from the left navigation rail, clicking **More apps**, then the **Upload a custom app** link.</span></span> <span data-ttu-id="a6d98-239">你还可以将应用程序清单或应用程序包导入到 App Studio 中，以在上传之前进行其他更新。</span><span class="sxs-lookup"><span data-stu-id="a6d98-239">You can also import an app manifest or app package into App Studio to make additional updates before uploading.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6d98-240">后续步骤</span><span class="sxs-lookup"><span data-stu-id="a6d98-240">Next steps</span></span>

* [<span data-ttu-id="a6d98-241">自动程序对话基础知识</span><span class="sxs-lookup"><span data-stu-id="a6d98-241">Bot conversation basics</span></span>](./conversations/conversation-basics.md)
* [<span data-ttu-id="a6d98-242">订阅对话事件</span><span class="sxs-lookup"><span data-stu-id="a6d98-242">Subscribe to conversation events</span></span>](./conversations/subscribe-to-conversation-events.md)
