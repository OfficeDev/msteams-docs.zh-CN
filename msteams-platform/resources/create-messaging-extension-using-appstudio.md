---
title: 使用 App Studio 创建消息传递
author: clearab
description: 了解如何使用 App Studio 创建 Microsoft Teams 消息传递扩展。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 25086d959004046e8227de46b31d840c0b3fd228
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51697224"
---
# <a name="create-a-messaging-extension-using-app-studio"></a><span data-ttu-id="d02f0-103">使用 App Studio 创建消息传递</span><span class="sxs-lookup"><span data-stu-id="d02f0-103">Create a messaging extension using App Studio</span></span>

> [!TIP]
> <span data-ttu-id="d02f0-104">寻找更快速入门的方法？</span><span class="sxs-lookup"><span data-stu-id="d02f0-104">Looking for a faster way to get started?</span></span> <span data-ttu-id="d02f0-105">使用 Microsoft Teams [策略](../build-your-first-app/build-messaging-extension.md) 创建消息传递Toolkit。</span><span class="sxs-lookup"><span data-stu-id="d02f0-105">Create a [messaging extension](../build-your-first-app/build-messaging-extension.md) using the Microsoft Teams Toolkit.</span></span>

<span data-ttu-id="d02f0-106">在高级别上，您需要完成以下步骤以创建邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="d02f0-106">At a high level, you'll need to complete the following steps to create a messaging extension.</span></span>

1. <span data-ttu-id="d02f0-107">准备开发环境</span><span class="sxs-lookup"><span data-stu-id="d02f0-107">Prepare your development environment</span></span>
2. <span data-ttu-id="d02f0-108">在开发时创建和部署 (服务使用隧道服务（如 ngrok）在本地运行) </span><span class="sxs-lookup"><span data-stu-id="d02f0-108">Create and deploy your web service (while developing use a tunneling service like ngrok to run it locally)</span></span>
3. <span data-ttu-id="d02f0-109">使用 Bot Framework 注册你的 Web 服务</span><span class="sxs-lookup"><span data-stu-id="d02f0-109">Register your web service with the Bot Framework</span></span>
4. <span data-ttu-id="d02f0-110">创建应用包</span><span class="sxs-lookup"><span data-stu-id="d02f0-110">Create your app package</span></span>
5. <span data-ttu-id="d02f0-111">将你的程序包上传到 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d02f0-111">Upload your package to Microsoft Teams</span></span>

<span data-ttu-id="d02f0-112">创建 Web 服务、创建应用包以及使用 Bot Framework 注册 Web 服务可以按任意顺序完成。</span><span class="sxs-lookup"><span data-stu-id="d02f0-112">Creating your web service, creating your app package, and registering your web service with the Bot Framework can be done in any order.</span></span> <span data-ttu-id="d02f0-113">由于这三个部分相互关联，因此无论按哪种顺序执行它们，都需要返回以更新其他部分。</span><span class="sxs-lookup"><span data-stu-id="d02f0-113">Because those three pieces are so intertwined, no matter which order you do them in you'll need return to update the others.</span></span> <span data-ttu-id="d02f0-114">注册需要来自部署的 Web 服务的消息终结点，并且 Web 服务需要通过注册创建的 ID 和密码。</span><span class="sxs-lookup"><span data-stu-id="d02f0-114">Your registration needs the messaging endpoint from your deployed web service, and your web service needs the Id and password created from your registration.</span></span> <span data-ttu-id="d02f0-115">你的应用清单还需要该 ID 以将 Teams 连接到 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="d02f0-115">Your app manifest also needs that Id to connect Teams to your web service.</span></span>

<span data-ttu-id="d02f0-116">生成邮件扩展时，你将定期在更改应用清单和将代码部署到 Web 服务之间移动。</span><span class="sxs-lookup"><span data-stu-id="d02f0-116">As you're building your messaging extension, you'll regularly be moving between changing your app manifest, and deploying code to your web service.</span></span> <span data-ttu-id="d02f0-117">使用应用清单时，请记住，你可以手动操作 JSON 文件，或者通过 App Studio 进行更改。</span><span class="sxs-lookup"><span data-stu-id="d02f0-117">When working with the app manifest, keep in mind that you can either manually manipulate the JSON file, or make changes through App Studio.</span></span> <span data-ttu-id="d02f0-118">无论采用哪种方式，在更改清单时) 在 Teams 中重新部署 (上传应用，但在将更改部署到 Web 服务时无需这样做。</span><span class="sxs-lookup"><span data-stu-id="d02f0-118">Either way, you'll need to re-deploy (upload) your app in Teams when you make a change to the manifest, but there's no need to do so when you deploy changes to your web service.</span></span>

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a><span data-ttu-id="d02f0-119">创建 Web 服务</span><span class="sxs-lookup"><span data-stu-id="d02f0-119">Create your web service</span></span>

<span data-ttu-id="d02f0-120">邮件扩展的核心是 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="d02f0-120">The heart of your messaging extension is your web service.</span></span> <span data-ttu-id="d02f0-121">它将定义一个路由（通常为 `/api/messages` ）以接收所有请求。</span><span class="sxs-lookup"><span data-stu-id="d02f0-121">It will define a single route, typically `/api/messages`, to receive all requests on.</span></span> <span data-ttu-id="d02f0-122">如果你从头开始，你可以从几个选项中进行选择。</span><span class="sxs-lookup"><span data-stu-id="d02f0-122">If you're getting started from scratch, you have a few options to choose from.</span></span>

* <span data-ttu-id="d02f0-123">使用我们的快速 [入门](#learn-more) 教程之一指导你创建 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="d02f0-123">Use one of our [quickstarts](#learn-more) tutorials that will guide you through the creation of your web service.</span></span>
* <span data-ttu-id="d02f0-124">从 Bot [Framework](https://github.com/Microsoft/BotBuilder-Samples) 示例存储库中选择一个消息扩展示例。</span><span class="sxs-lookup"><span data-stu-id="d02f0-124">Choose one of the messaging extension samples available in the [Bot Framework sample repository](https://github.com/Microsoft/BotBuilder-Samples) to start from.</span></span>
* <span data-ttu-id="d02f0-125">如果你使用的是 JavaScript，请使用 Microsoft Teams 的 [Yeoman](https://github.com/OfficeDev/generator-teams) 生成器为 Teams 应用（包括 Web 服务）搭建基架。</span><span class="sxs-lookup"><span data-stu-id="d02f0-125">If you're using JavaScript, use the [Yeoman generator for Microsoft Teams](https://github.com/OfficeDev/generator-teams) to scaffold your Teams app, including your web service.</span></span>
* <span data-ttu-id="d02f0-126">从头开始创建 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="d02f0-126">Create your web service from scratch.</span></span> <span data-ttu-id="d02f0-127">可选择添加面向你的语言的 Bot Framework SDK，也可以直接使用 JSON 有效负载。</span><span class="sxs-lookup"><span data-stu-id="d02f0-127">You can choose to add the Bot Framework SDK for your language, or you can work directly with the JSON payloads.</span></span>

## <a name="register-your-web-service-with-the-bot-framework"></a><span data-ttu-id="d02f0-128">使用 Bot Framework 注册你的 Web 服务</span><span class="sxs-lookup"><span data-stu-id="d02f0-128">Register your web service with the Bot Framework</span></span>

<span data-ttu-id="d02f0-129">邮件扩展利用 Bot Framework 的消息架构和安全通信协议;如果还没有，则需要在 Bot Framework 上注册 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="d02f0-129">Messaging extensions take advantage of the Bot Framework's messaging schema and secure communication protocol; if you don't already have one you'll need to register your web service on the Bot Framework.</span></span> <span data-ttu-id="d02f0-130">Microsoft 应用 ID (我们将它作为来自 Teams 内部的自动程序 ID 进行引用，以便从你可能正在处理) 的其他应用 ID 中标识它，在 Bot Framework 中注册的消息终结点将在你的消息传递扩展中用于接收和响应请求。</span><span class="sxs-lookup"><span data-stu-id="d02f0-130">The Microsoft App Id (we'll refer to this as your Bot Id from inside of Teams, to identify it from other App Id's you might be working with) and the messaging endpoint your register with the Bot Framework will be used in your messaging extension to receive and respond to requests.</span></span> <span data-ttu-id="d02f0-131">如果你使用的是现有注册，请确保启用 Microsoft Teams [频道](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="d02f0-131">If you're using an existing registration, make sure you [enable the Microsoft Teams channel](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="d02f0-132">如果你遵循其中一个快速入门或从其中一个可用示例开始，将指导你完成注册 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="d02f0-132">If you follow one of the quickstarts or start from one of the available samples you'll be guided through registering your web service.</span></span> <span data-ttu-id="d02f0-133">如果要手动注册服务，有三个选项可进行注册。</span><span class="sxs-lookup"><span data-stu-id="d02f0-133">If you want to manually register your service you have three options to do so.</span></span> <span data-ttu-id="d02f0-134">如果选择注册而不使用 Azure 订阅，将无法利用 Bot Framework 提供的简化 OAuth 身份验证流。</span><span class="sxs-lookup"><span data-stu-id="d02f0-134">If you choose to register without using an Azure subscription you will not be able to take advantage of the simplified OAuth authentication flow provided by the Bot Framework.</span></span> <span data-ttu-id="d02f0-135">创建后，你将能够将注册迁移到 Azure。</span><span class="sxs-lookup"><span data-stu-id="d02f0-135">You will be able to migrate your registration to Azure after creation.</span></span>

* <span data-ttu-id="d02f0-136">如果你有 Azure 订阅 (或想要创建新的 Azure) ，可以使用 Azure 门户手动注册 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="d02f0-136">If you have an Azure subscription (or want to create a new one), you can register your web service manually using the Azure Portal.</span></span> <span data-ttu-id="d02f0-137">创建"Bot Channels Registration"资源。</span><span class="sxs-lookup"><span data-stu-id="d02f0-137">Create a "Bot Channels Registration" resource.</span></span> <span data-ttu-id="d02f0-138">你可以选择免费定价层，因为来自 Microsoft Teams 的消息不计入每月允许的消息总数。</span><span class="sxs-lookup"><span data-stu-id="d02f0-138">You can choose the free pricing tier, as messages from Microsoft Teams do not count towards your total allowable messages per month.</span></span>
* <span data-ttu-id="d02f0-139">如果你不希望使用 Azure 订阅，可以使用旧版 [注册门户](https://dev.botframework.com/bots/new)。</span><span class="sxs-lookup"><span data-stu-id="d02f0-139">If you do not wish to use an Azure subscription, you can use the [legacy registration portal](https://dev.botframework.com/bots/new).</span></span>
* <span data-ttu-id="d02f0-140">App Studio 还可以帮助你注册 Web 服务 (自动) 。</span><span class="sxs-lookup"><span data-stu-id="d02f0-140">App Studio can also help you register your web service (bot).</span></span> <span data-ttu-id="d02f0-141">通过 App Studio 注册的 Web 服务未在 Azure 中注册。</span><span class="sxs-lookup"><span data-stu-id="d02f0-141">Web services registered through App Studio are not registered in Azure.</span></span> <span data-ttu-id="d02f0-142">可以使用旧 [门户查看](https://dev.botframework.com/bots) 、管理和迁移注册。</span><span class="sxs-lookup"><span data-stu-id="d02f0-142">You can use the [legacy portal](https://dev.botframework.com/bots) to view, manage, and migrate your registrations.</span></span>

## <a name="create-your-app-manifest"></a><span data-ttu-id="d02f0-143">创建应用清单</span><span class="sxs-lookup"><span data-stu-id="d02f0-143">Create your app manifest</span></span>

<span data-ttu-id="d02f0-144">你可以使用 App Studio 帮助创建应用程序清单，也可以手动创建。</span><span class="sxs-lookup"><span data-stu-id="d02f0-144">You can either use App Studio to help you create your app manifest, or create it manually.</span></span>

### <a name="create-your-app-manifest-using-app-studio"></a><span data-ttu-id="d02f0-145">使用 App Studio 创建应用清单</span><span class="sxs-lookup"><span data-stu-id="d02f0-145">Create your app manifest using App Studio</span></span>

<span data-ttu-id="d02f0-146">可以在 Microsoft Teams 客户端内使用 App Studio 应用来帮助创建应用清单。</span><span class="sxs-lookup"><span data-stu-id="d02f0-146">You can use the App Studio app from within the Microsoft Teams client to help create your app manifest.</span></span>

1. <span data-ttu-id="d02f0-147">在 Teams 客户端中，从左侧导航栏上的“**…**”溢出菜单中打开 App Studio。</span><span class="sxs-lookup"><span data-stu-id="d02f0-147">In the Teams client, open App Studio from the **...** overflow menu on the left navigation rail.</span></span> <span data-ttu-id="d02f0-148">如果尚未安装，则可以通过搜索来这样做。</span><span class="sxs-lookup"><span data-stu-id="d02f0-148">If it isn't already installed, you can do so by searching for it.</span></span>
2. <span data-ttu-id="d02f0-149">在清单 **编辑器** 选项卡上 **，选择** 创建新应用 (或者如果你要向现有应用添加消息传递扩展，你可以将应用包) </span><span class="sxs-lookup"><span data-stu-id="d02f0-149">On the **Manifest editor** tab select **Create a new app** (or if you're adding a messaging extension to an existing app, you can import your app package)</span></span>
3. <span data-ttu-id="d02f0-150">添加应用详细信息（有关每个字段的完整说明，请参阅[清单架构定义](~/resources/schema/manifest-schema.md)）。</span><span class="sxs-lookup"><span data-stu-id="d02f0-150">Add your app details (see [manifest schema definition](~/resources/schema/manifest-schema.md) for full descriptions of each field).</span></span>
4. <span data-ttu-id="d02f0-151">在" **消息扩展"** 选项卡上，单击" **设置"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="d02f0-151">On the **Messaging extensions** tab click the **Setup** button.</span></span>
5. <span data-ttu-id="d02f0-152">你可以创建新的 Web 服务 (自动) 供邮件扩展使用，或者如果你已注册一个，请在此处选择/添加它。</span><span class="sxs-lookup"><span data-stu-id="d02f0-152">You can either create a new web service (bot) for your messaging extension to use, or if you've already registered one select/add it here.</span></span>
6. <span data-ttu-id="d02f0-153">如有必要，请更新自动程序终结点地址以指向你的自动程序。</span><span class="sxs-lookup"><span data-stu-id="d02f0-153">If necessary, update your bot endpoint address to point to your bot.</span></span> <span data-ttu-id="d02f0-154">它应该类似于 `https://someplace.com/api/messages`。</span><span class="sxs-lookup"><span data-stu-id="d02f0-154">It should look something like `https://someplace.com/api/messages`.</span></span>
7. <span data-ttu-id="d02f0-155">"**命令\*\*\*\*"部分中的**"添加"按钮将指导你向邮件扩展添加命令。</span><span class="sxs-lookup"><span data-stu-id="d02f0-155">The **Add** button in the **Command** section will guide you through adding commands to your messaging extension.</span></span> <span data-ttu-id="d02f0-156">有关添加 [命令详细信息](#learn-more) 的链接，请参阅了解详细信息部分。</span><span class="sxs-lookup"><span data-stu-id="d02f0-156">See the [Learn more](#learn-more) section for links to more information on adding commands.</span></span> <span data-ttu-id="d02f0-157">请记住，您可以为邮件扩展定义最多 10 个命令。</span><span class="sxs-lookup"><span data-stu-id="d02f0-157">Remember you can define up to 10 commands for your messaging extension.</span></span>
8. <span data-ttu-id="d02f0-158">" **消息处理程序"** 部分允许您添加邮件将触发的域。</span><span class="sxs-lookup"><span data-stu-id="d02f0-158">The **Message Handlers** section allows you to add a domain that your messaging will trigger on.</span></span> <span data-ttu-id="d02f0-159">有关详细信息 [，请参阅链接](~/messaging-extensions/how-to/link-unfurling.md) 取消链接。</span><span class="sxs-lookup"><span data-stu-id="d02f0-159">See [link unfurling](~/messaging-extensions/how-to/link-unfurling.md) for more information.</span></span>

<span data-ttu-id="d02f0-160">从"**完成 =**> 测试并分发"选项卡中，你可以下载应用包 (其中包含应用清单以及应用图标) 或安装程序包。 </span><span class="sxs-lookup"><span data-stu-id="d02f0-160">From the **Finish => Test and distribute** tab you can **Download** your app package (which includes your app manifest as well as your app icons), or **Install** the package.</span></span>

### <a name="create-your-app-manifest-manually"></a><span data-ttu-id="d02f0-161">手动创建应用清单</span><span class="sxs-lookup"><span data-stu-id="d02f0-161">Create your app manifest manually</span></span>

<span data-ttu-id="d02f0-162">与机器人和选项卡一样，更新 [应用](~/resources/schema/manifest-schema.md#composeextensions) 的应用清单以包含消息传递扩展属性。</span><span class="sxs-lookup"><span data-stu-id="d02f0-162">As with bots and tabs, you update the [app manifest](~/resources/schema/manifest-schema.md#composeextensions) of your app to include the messaging extension properties.</span></span> <span data-ttu-id="d02f0-163">这些属性控制邮件扩展在 Microsoft Teams 客户端中的显示和行为方式。</span><span class="sxs-lookup"><span data-stu-id="d02f0-163">These properties govern how your messaging extension appears and behaves in the Microsoft Teams client.</span></span> <span data-ttu-id="d02f0-164">从清单的 v1.0 开始，支持消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="d02f0-164">Messaging extensions are supported beginning with v1.0 of the manifest.</span></span>

#### <a name="declare-your-messaging-extension"></a><span data-ttu-id="d02f0-165">声明邮件扩展</span><span class="sxs-lookup"><span data-stu-id="d02f0-165">Declare your messaging extension</span></span>

<span data-ttu-id="d02f0-166">若要添加消息传递扩展，请通过 属性在应用清单中添加一个新的顶级 JSON `composeExtensions` 结构。</span><span class="sxs-lookup"><span data-stu-id="d02f0-166">To add a messaging extension, include a new top-level JSON structure in your app manifest with the `composeExtensions` property.</span></span> <span data-ttu-id="d02f0-167">使用最多 10 个命令为应用创建单个消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="d02f0-167">You create a single messaging extension for your app, with up to 10 commands.</span></span>

> [!NOTE]
> <span data-ttu-id="d02f0-168">清单将消息传递扩展引用为 `composeExtensions` 。</span><span class="sxs-lookup"><span data-stu-id="d02f0-168">The manifest refers to messaging extensions as `composeExtensions`.</span></span> <span data-ttu-id="d02f0-169">这是为了维护向后兼容性。</span><span class="sxs-lookup"><span data-stu-id="d02f0-169">This is to maintain backward compatibility.</span></span>

<span data-ttu-id="d02f0-170">扩展定义是具有以下结构的对象：</span><span class="sxs-lookup"><span data-stu-id="d02f0-170">The extension definition is an object that has the following structure:</span></span>

| <span data-ttu-id="d02f0-171">属性名称</span><span class="sxs-lookup"><span data-stu-id="d02f0-171">Property name</span></span> | <span data-ttu-id="d02f0-172">用途</span><span class="sxs-lookup"><span data-stu-id="d02f0-172">Purpose</span></span> | <span data-ttu-id="d02f0-173">是否必需？</span><span class="sxs-lookup"><span data-stu-id="d02f0-173">Required?</span></span> |
|---|---|---|
| `botId` | <span data-ttu-id="d02f0-174">使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="d02f0-174">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="d02f0-175">这通常应该与整个 Teams 应用的 ID 相同。</span><span class="sxs-lookup"><span data-stu-id="d02f0-175">This should typically be the same as the ID for your overall Teams app.</span></span> | <span data-ttu-id="d02f0-176">是</span><span class="sxs-lookup"><span data-stu-id="d02f0-176">Yes</span></span> |
| `canUpdateConfiguration` | <span data-ttu-id="d02f0-177">启用 **"设置"** 菜单项。</span><span class="sxs-lookup"><span data-stu-id="d02f0-177">Enables **Settings** menu item.</span></span> | <span data-ttu-id="d02f0-178">否</span><span class="sxs-lookup"><span data-stu-id="d02f0-178">No</span></span> |
| `commands` | <span data-ttu-id="d02f0-179">此邮件扩展支持的命令数组。</span><span class="sxs-lookup"><span data-stu-id="d02f0-179">Array of commands that this messaging extension supports.</span></span> <span data-ttu-id="d02f0-180">只能使用 10 个命令。</span><span class="sxs-lookup"><span data-stu-id="d02f0-180">You are limited to 10 commands.</span></span> | <span data-ttu-id="d02f0-181">是</span><span class="sxs-lookup"><span data-stu-id="d02f0-181">Yes</span></span> |

#### <a name="define-your-commands"></a><span data-ttu-id="d02f0-182">定义命令</span><span class="sxs-lookup"><span data-stu-id="d02f0-182">Define your commands</span></span>

<span data-ttu-id="d02f0-183">邮件扩展应声明一个或多个命令，这些命令定义用户可以在何处触发邮件扩展以及交互类型。</span><span class="sxs-lookup"><span data-stu-id="d02f0-183">Your messaging extension should declare one or more commands, which define where your users can trigger your messaging extension, and the type of interaction.</span></span> <span data-ttu-id="d02f0-184">有关 [邮件](#learn-more) 扩展命令详细信息，请参阅了解详细信息。</span><span class="sxs-lookup"><span data-stu-id="d02f0-184">See [learn more](#learn-more) for more information on messaging extension commands.</span></span>

#### <a name="simple-manifest-example"></a><span data-ttu-id="d02f0-185">简单清单示例</span><span class="sxs-lookup"><span data-stu-id="d02f0-185">Simple manifest example</span></span>

<span data-ttu-id="d02f0-186">以下示例是应用清单中具有搜索命令的简单消息传递扩展对象。</span><span class="sxs-lookup"><span data-stu-id="d02f0-186">The following example is a simple messaging extension object in the app manifest with a search command.</span></span> <span data-ttu-id="d02f0-187">这不是整个应用程序清单文件，只是特定于消息传递扩展的部分。</span><span class="sxs-lookup"><span data-stu-id="d02f0-187">This is not the entire app manifest file, just the part specific to messaging extensions.</span></span> <span data-ttu-id="d02f0-188">有关 [完整示例，](~/resources/schema/manifest-schema.md) 请参阅应用清单架构。</span><span class="sxs-lookup"><span data-stu-id="d02f0-188">See [app manifest schema](~/resources/schema/manifest-schema.md) for a complete example.</span></span>

```json
...
"composeExtensions": [
  {
    "botId": "abcd1234-1fc5-4d97-a142-35bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "searchCmd",
        "description": "Search you ToDo's",
        "title": "Search",
        "initialRun": true,
        "parameters": [
          {
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }
        ]
      }
    ]
  }
]
...
```

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="d02f0-189">完整的应用清单示例</span><span class="sxs-lookup"><span data-stu-id="d02f0-189">Complete app manifest example</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.Todo",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://todobotservice.azurewebsites.net/",
    "privacyUrl": "http://todobotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://todobotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "To Do",
    "full": "To Do"
  },
  "description": {
    "short": "Find or create a new task in To Do",
    "full": "Find or create a new task in To Do"
  },
  "icons": {
    "outline": "todo-outline.jpg",
    "color": "todo-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "searchCmd",
          "description": "Search you Todo's",
          "title": "Search",
          "initialRun": true,
          "context": ["commandBox", "compose"],
          "parameters": [
            {
              "name": "searchKeyword",
              "description": "Enter your search keywords",
              "title": "Keywords"
            }
          ]
        },
        {
          "id": "addTodo",
          "description": "Create a To Do item",
          "title": "Create To Do",
          "type": "action",
          "context": ["commandBox", "message", "compose"],
          "parameters": [
            {
              "name": "Name",
              "description": "To Do Title",
              "title": "Title",
              "inputType": "text"
            },
            {
              "name": "Description",
              "description": "Description of the task",
              "title": "Description",
              "inputType": "textarea"
            },
            {
              "name": "Date",
              "description": "Due date for the task",
              "title": "Date",
              "inputType": "date"
            }
          ]
        },
        {
          "id": "reassignTodo",
          "description": "Reassign a todo item",
          "title": "Reassign a todo item",
          "type": "action",
          "fetchTask": true,
          "parameters": [
            {
              "name": "Name",
              "title": "Title"
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "todobotservice.azurewebsites.net",
    "*.todobotservice.azurewebsites.net"
  ]
}
```

## <a name="add-your-invoke-message-handlers"></a><span data-ttu-id="d02f0-190">添加调用消息处理程序</span><span class="sxs-lookup"><span data-stu-id="d02f0-190">Add your invoke message handlers</span></span>

<span data-ttu-id="d02f0-191">当用户触发消息扩展时，你需要处理初始调用消息，从用户收集一些信息，然后处理该信息并做出相应的响应。</span><span class="sxs-lookup"><span data-stu-id="d02f0-191">When your users trigger your messaging extension you'll need to handle the initial invoke message, collect some information from the user, then process that information and respond appropriately.</span></span> <span data-ttu-id="d02f0-192">为此，首先需要确定要添加到邮件扩展中的命令类型，并添加操作[命令或](~/messaging-extensions/how-to/action-commands/define-action-command.md)[添加搜索命令](~/messaging-extensions/how-to/search-commands/define-search-command.md)。</span><span class="sxs-lookup"><span data-stu-id="d02f0-192">To do that, you'll first need to decide what kind of commands you want to add to your messaging extension and either [add an action commands](~/messaging-extensions/how-to/action-commands/define-action-command.md) or [add a search commands](~/messaging-extensions/how-to/search-commands/define-search-command.md).</span></span>

## <a name="messaging-extensions-in-teams-meetings"></a><span data-ttu-id="d02f0-193">Teams 会议中的消息扩展</span><span class="sxs-lookup"><span data-stu-id="d02f0-193">Messaging extensions in Teams meetings</span></span>

> [!NOTE]
> <span data-ttu-id="d02f0-194">如果会议或群聊在名单中有联盟用户，则 Teams 将禁止所有用户（包括组织者）访问消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="d02f0-194">If a meeting or group chat has federated users in the roster, Teams suppresses access to messaging extensions for all users, including the organizer.</span></span>

<span data-ttu-id="d02f0-195">会议开始后，Teams 参与者可以在实时呼叫期间直接与消息扩展进行交互。</span><span class="sxs-lookup"><span data-stu-id="d02f0-195">Once a meeting begins, Teams participants can interact directly with your messaging extension during a live call.</span></span> <span data-ttu-id="d02f0-196">生成会议内消息传递扩展时，请考虑以下事项：</span><span class="sxs-lookup"><span data-stu-id="d02f0-196">Consider the following when building your in-meeting messaging extension:</span></span>

1. <span data-ttu-id="d02f0-197">**Location**。</span><span class="sxs-lookup"><span data-stu-id="d02f0-197">**Location**.</span></span> <span data-ttu-id="d02f0-198">可以从会议聊天中的撰写消息区域、命令框或消息@mentioned消息扩展。</span><span class="sxs-lookup"><span data-stu-id="d02f0-198">Your messaging extension can be invoked from the compose message area, the command box, or @mentioned in the meeting chat.</span></span>

1. <span data-ttu-id="d02f0-199">**元数据**。</span><span class="sxs-lookup"><span data-stu-id="d02f0-199">**Metadata**.</span></span> <span data-ttu-id="d02f0-200">调用消息扩展时，它可以从 和 标识用户和 `userId` 租户 `tenantId` 。</span><span class="sxs-lookup"><span data-stu-id="d02f0-200">When your messaging extension is invoked it can identify the user and tenant from `userId` and `tenantId`.</span></span> <span data-ttu-id="d02f0-201">可在 `channelData` 对象中找到 `meetingId`。</span><span class="sxs-lookup"><span data-stu-id="d02f0-201">The `meetingId` can be found as part of the `channelData` object.</span></span> <span data-ttu-id="d02f0-202">你的应用可以使用 和 `userId` `meetingId`  的 API `GetParticipant` 请求检索用户角色。</span><span class="sxs-lookup"><span data-stu-id="d02f0-202">Your app can use the `userId` and `meetingId`  for the `GetParticipant` API request to retrieve user roles.</span></span>

1. <span data-ttu-id="d02f0-203">**命令类型**。</span><span class="sxs-lookup"><span data-stu-id="d02f0-203">**Command type**.</span></span> <span data-ttu-id="d02f0-204">如果邮件扩展使用 [基于操作的命令](../messaging-extensions/what-are-messaging-extensions.md#action-commands)，它应遵循选项卡 [单一登录](../tabs/how-to/authentication/auth-aad-sso.md) 身份验证。</span><span class="sxs-lookup"><span data-stu-id="d02f0-204">If your message extension uses [action-based commands](../messaging-extensions/what-are-messaging-extensions.md#action-commands), it should follow tabs [single sign-on](../tabs/how-to/authentication/auth-aad-sso.md) authentication.</span></span>

1. <span data-ttu-id="d02f0-205">**用户体验**。</span><span class="sxs-lookup"><span data-stu-id="d02f0-205">**User experience**.</span></span> <span data-ttu-id="d02f0-206">消息扩展的外观和行为应该与在会议外相同。</span><span class="sxs-lookup"><span data-stu-id="d02f0-206">You messaging extension should look and behave the same as it would outside a meeting.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d02f0-207">后续步骤</span><span class="sxs-lookup"><span data-stu-id="d02f0-207">Next steps</span></span>

* [<span data-ttu-id="d02f0-208">创建操作命令</span><span class="sxs-lookup"><span data-stu-id="d02f0-208">Create action commands</span></span>](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="d02f0-209">创建搜索命令</span><span class="sxs-lookup"><span data-stu-id="d02f0-209">Create search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [<span data-ttu-id="d02f0-210">链接展开</span><span class="sxs-lookup"><span data-stu-id="d02f0-210">Link unfurling</span></span>](~/messaging-extensions/how-to/link-unfurling.md)

## <a name="learn-more"></a><span data-ttu-id="d02f0-211">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="d02f0-211">Learn more</span></span>

<span data-ttu-id="d02f0-212">在快速入门中试用：</span><span class="sxs-lookup"><span data-stu-id="d02f0-212">Try it out in a quickstart:</span></span>

* <span data-ttu-id="d02f0-213">C 快速入门#</span><span class="sxs-lookup"><span data-stu-id="d02f0-213">Quickstarts for C#</span></span>
  * [<span data-ttu-id="d02f0-214">使用基于操作的命令的邮件扩展</span><span class="sxs-lookup"><span data-stu-id="d02f0-214">Messaging extension with action-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [<span data-ttu-id="d02f0-215">使用基于搜索的命令的邮件扩展</span><span class="sxs-lookup"><span data-stu-id="d02f0-215">Messaging extension with search-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* <span data-ttu-id="d02f0-216">JavaScript 快速入门</span><span class="sxs-lookup"><span data-stu-id="d02f0-216">Quickstarts for JavaScript</span></span>
  * [<span data-ttu-id="d02f0-217">使用基于操作的命令的邮件扩展</span><span class="sxs-lookup"><span data-stu-id="d02f0-217">Messaging extension with action-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [<span data-ttu-id="d02f0-218">使用基于搜索的命令的邮件扩展</span><span class="sxs-lookup"><span data-stu-id="d02f0-218">Messaging extension with search-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

<span data-ttu-id="d02f0-219">详细了解 Teams 开发概念：</span><span class="sxs-lookup"><span data-stu-id="d02f0-219">Learn more about Teams development concepts:</span></span>

* [<span data-ttu-id="d02f0-220">了解 Teams 应用功能</span><span class="sxs-lookup"><span data-stu-id="d02f0-220">Understand Teams app capabilities</span></span>](../concepts/capabilities-overview.md)
* [<span data-ttu-id="d02f0-221">什么是消息扩展？</span><span class="sxs-lookup"><span data-stu-id="d02f0-221">What are messaging extensions?</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
