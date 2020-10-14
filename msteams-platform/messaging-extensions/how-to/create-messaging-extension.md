---
title: 为工作组创建邮件扩展
author: clearab
description: 了解如何创建团队消息扩展
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 03fe4463f7e7af0874af4ce4f487f1a01fdd5fe6
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452594"
---
# <a name="create-a-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="bcb41-103">为 Microsoft 团队创建消息扩展</span><span class="sxs-lookup"><span data-stu-id="bcb41-103">Create a messaging extension for Microsoft Teams</span></span>

> [!TIP]
> <span data-ttu-id="bcb41-104">寻求更快的入门方式？</span><span class="sxs-lookup"><span data-stu-id="bcb41-104">Looking for a faster way to get started?</span></span> <span data-ttu-id="bcb41-105">使用 Microsoft 团队工具包创建 [邮件扩展插件](../../build-your-first-app/build-messaging-extension.md) 。</span><span class="sxs-lookup"><span data-stu-id="bcb41-105">Create a [messaging extension](../../build-your-first-app/build-messaging-extension.md) using the Microsoft Teams Toolkit.</span></span>

<span data-ttu-id="bcb41-106">在较高级别，需要完成以下步骤以创建邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="bcb41-106">At a high level, you'll need to complete the following steps to create a messaging extension.</span></span>

1. <span data-ttu-id="bcb41-107">准备开发环境</span><span class="sxs-lookup"><span data-stu-id="bcb41-107">Prepare your development environment</span></span>
2. <span data-ttu-id="bcb41-108">在开发时，创建和部署 web 服务 (使用隧道服务（如 ngrok）在本地运行它) </span><span class="sxs-lookup"><span data-stu-id="bcb41-108">Create and deploy your web service (while developing use a tunneling service like ngrok to run it locally)</span></span>
3. <span data-ttu-id="bcb41-109">使用 Bot Framework 注册你的 Web 服务</span><span class="sxs-lookup"><span data-stu-id="bcb41-109">Register your web service with the Bot Framework</span></span>
4. <span data-ttu-id="bcb41-110">创建应用包</span><span class="sxs-lookup"><span data-stu-id="bcb41-110">Create your app package</span></span>
5. <span data-ttu-id="bcb41-111">将你的程序包上传到 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="bcb41-111">Upload your package to Microsoft Teams</span></span>

<span data-ttu-id="bcb41-112">可以按照任何顺序，创建 web 服务，创建应用程序包，并将您的 web 服务注册到 Bot 框架。</span><span class="sxs-lookup"><span data-stu-id="bcb41-112">Creating your web service, creating your app package, and registering your web service with the Bot Framework can be done in any order.</span></span> <span data-ttu-id="bcb41-113">由于这三个部分如此 intertwined，无论你在哪种顺序中执行此操作，都需要返回以更新其他内容。</span><span class="sxs-lookup"><span data-stu-id="bcb41-113">Because those three pieces are so intertwined, no matter which order you do them in you'll need return to update the others.</span></span> <span data-ttu-id="bcb41-114">您的注册需要来自已部署的 web 服务的消息终结点，并且您的 web 服务需要从您的注册创建的 Id 和密码。</span><span class="sxs-lookup"><span data-stu-id="bcb41-114">Your registration needs the messaging endpoint from your deployed web service, and your web service needs the Id and password created from your registration.</span></span> <span data-ttu-id="bcb41-115">您的应用程序清单还需要该 Id 才能将团队连接到您的 web 服务。</span><span class="sxs-lookup"><span data-stu-id="bcb41-115">Your app manifest also needs that Id to connect Teams to your web service.</span></span>

<span data-ttu-id="bcb41-116">在构建邮件扩展时，您将在更改应用程序清单和向 web 服务部署代码之间进行定期移动。</span><span class="sxs-lookup"><span data-stu-id="bcb41-116">As you're building your messaging extension, you'll regularly be moving between changing your app manifest, and deploying code to your web service.</span></span> <span data-ttu-id="bcb41-117">在使用应用程序清单时，请记住，可以手动操作 JSON 文件，也可以通过应用程序 Studio 进行更改。</span><span class="sxs-lookup"><span data-stu-id="bcb41-117">When working with the app manifest, keep in mind that you can either manually manipulate the JSON file, or make changes through App Studio.</span></span> <span data-ttu-id="bcb41-118">无论哪种方式，在对清单进行更改时，都需要重新部署 (上传) 您的团队中的应用程序，但在将更改部署到 web 服务时，无需执行此操作。</span><span class="sxs-lookup"><span data-stu-id="bcb41-118">Either way, you'll need to re-deploy (upload) your app in Teams when you make a change to the manifest, but there's no need to do so when you deploy changes to your web service.</span></span>

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a><span data-ttu-id="bcb41-119">创建 Web 服务</span><span class="sxs-lookup"><span data-stu-id="bcb41-119">Create your web service</span></span>

<span data-ttu-id="bcb41-120">您的邮件扩展的核心是您的 web 服务。</span><span class="sxs-lookup"><span data-stu-id="bcb41-120">The heart of your messaging extension is your web service.</span></span> <span data-ttu-id="bcb41-121">它将定义单个路由，通常是 `/api/messages` 接收上的所有请求。</span><span class="sxs-lookup"><span data-stu-id="bcb41-121">It will define a single route, typically `/api/messages`, to receive all requests on.</span></span> <span data-ttu-id="bcb41-122">如果你从头开始，你有几个选项可供选择。</span><span class="sxs-lookup"><span data-stu-id="bcb41-122">If you're getting started from scratch, you have a few options to choose from.</span></span>

* <span data-ttu-id="bcb41-123">使用我们的 [快速入门](#learn-more) 教程之一，它将指导您完成 web 服务的创建。</span><span class="sxs-lookup"><span data-stu-id="bcb41-123">Use one of our [quickstarts](#learn-more) tutorials that will guide you through the creation of your web service.</span></span>
* <span data-ttu-id="bcb41-124">选择要从其开始的 [Bot 框架示例存储库](https://github.com/Microsoft/BotBuilder-Samples) 中提供的邮件扩展示例之一。</span><span class="sxs-lookup"><span data-stu-id="bcb41-124">Choose one of the messaging extension samples available in the [Bot Framework sample repository](https://github.com/Microsoft/BotBuilder-Samples) to start from.</span></span>
* <span data-ttu-id="bcb41-125">如果您使用的是 JavaScript，请使用 [Microsoft 团队的 Yeoman 生成器](https://github.com/OfficeDev/generator-teams) 搭建团队应用程序（包括 web 服务）。</span><span class="sxs-lookup"><span data-stu-id="bcb41-125">If you're using JavaScript, use the [Yeoman generator for Microsoft Teams](https://github.com/OfficeDev/generator-teams) to scaffold your Teams app, including your web service.</span></span>
* <span data-ttu-id="bcb41-126">从头开始创建 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="bcb41-126">Create your web service from scratch.</span></span> <span data-ttu-id="bcb41-127">可选择添加面向你的语言的 Bot Framework SDK，也可以直接使用 JSON 有效负载。</span><span class="sxs-lookup"><span data-stu-id="bcb41-127">You can choose to add the Bot Framework SDK for your language, or you can work directly with the JSON payloads.</span></span>

## <a name="register-your-web-service-with-the-bot-framework"></a><span data-ttu-id="bcb41-128">使用 Bot Framework 注册你的 Web 服务</span><span class="sxs-lookup"><span data-stu-id="bcb41-128">Register your web service with the Bot Framework</span></span>

<span data-ttu-id="bcb41-129">邮件扩展利用 Bot 框架的邮件架构和安全通信协议;如果尚未安装，则需要在 Bot 框架上注册 web 服务。</span><span class="sxs-lookup"><span data-stu-id="bcb41-129">Messaging extensions take advantage of the Bot Framework's messaging schema and secure communication protocol; if you don't already have one you'll need to register your web service on the Bot Framework.</span></span> <span data-ttu-id="bcb41-130">Microsoft 应用 Id (我们会将其作为你的 Bot Id 从团队内部进行引用，以便从其他应用程序 Id 中进行标识。你可能会使用) ，邮件扩展中将使用使用 Bot 框架注册的邮件终结点来接收和响应请求。</span><span class="sxs-lookup"><span data-stu-id="bcb41-130">The Microsoft App Id (we'll refer to this as your Bot Id from inside of Teams, to identify it from other App Id's you might be working with) and the messaging endpoint your register with the Bot Framework will be used in your messaging extension to receive and respond to requests.</span></span> <span data-ttu-id="bcb41-131">如果使用的是现有注册，请确保 [启用 Microsoft 团队频道](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="bcb41-131">If you're using an existing registration, make sure you [enable the Microsoft Teams channel](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="bcb41-132">如果您关注其中一个快速入门或从一个可用示例开始，则将通过注册 web 服务来指导您。</span><span class="sxs-lookup"><span data-stu-id="bcb41-132">If you follow one of the quickstarts or start from one of the available samples you'll be guided through registering your web service.</span></span> <span data-ttu-id="bcb41-133">如果要手动注册服务，有三个选项可执行此操作。</span><span class="sxs-lookup"><span data-stu-id="bcb41-133">If you want to manually register your service you have three options to do so.</span></span> <span data-ttu-id="bcb41-134">如果你选择不使用 Azure 订阅进行注册，将无法利用 Bot 框架提供的简化 OAuth 身份验证流。</span><span class="sxs-lookup"><span data-stu-id="bcb41-134">If you choose to register without using an Azure subscription you will not be able to take advantage of the simplified OAuth authentication flow provided by the Bot Framework.</span></span> <span data-ttu-id="bcb41-135">创建后，你将能够将注册迁移到 Azure。</span><span class="sxs-lookup"><span data-stu-id="bcb41-135">You will be able to migrate your registration to Azure after creation.</span></span>

* <span data-ttu-id="bcb41-136">如果你有 Azure 订阅 (或想要创建一个新的) ，则可以使用 Azure 门户手动注册 web 服务。</span><span class="sxs-lookup"><span data-stu-id="bcb41-136">If you have an Azure subscription (or want to create a new one), you can register your web service manually using the Azure Portal.</span></span> <span data-ttu-id="bcb41-137">创建 "Bot 通道注册" 资源。</span><span class="sxs-lookup"><span data-stu-id="bcb41-137">Create a "Bot Channels Registration" resource.</span></span> <span data-ttu-id="bcb41-138">您可以选择免费定价层，因为来自 Microsoft 团队的邮件不会将每个月的允许总邮件数计到每个月。</span><span class="sxs-lookup"><span data-stu-id="bcb41-138">You can choose the free pricing tier, as messages from Microsoft Teams do not count towards your total allowable messages per month.</span></span>
* <span data-ttu-id="bcb41-139">如果您不想使用 Azure 订阅，则可以使用 [旧版注册门户](https://dev.botframework.com/bots/new)。</span><span class="sxs-lookup"><span data-stu-id="bcb41-139">If you do not wish to use an Azure subscription, you can use the [legacy registration portal](https://dev.botframework.com/bots/new).</span></span>
* <span data-ttu-id="bcb41-140">应用程序 Studio 还可帮助您在) 中注册 web 服务 (bot。</span><span class="sxs-lookup"><span data-stu-id="bcb41-140">App Studio can also help you register your web service (bot).</span></span> <span data-ttu-id="bcb41-141">通过应用程序 Studio 注册的 Web 服务未在 Azure 中注册。</span><span class="sxs-lookup"><span data-stu-id="bcb41-141">Web services registered through App Studio are not registered in Azure.</span></span> <span data-ttu-id="bcb41-142">您可以使用 [旧版门户](https://dev.botframework.com/bots) 查看、管理和迁移您的注册。</span><span class="sxs-lookup"><span data-stu-id="bcb41-142">You can use the [legacy portal](https://dev.botframework.com/bots) to view, manage, and migrate your registrations.</span></span>

## <a name="create-your-app-manifest"></a><span data-ttu-id="bcb41-143">创建您的应用程序清单</span><span class="sxs-lookup"><span data-stu-id="bcb41-143">Create your app manifest</span></span>

<span data-ttu-id="bcb41-144">你可以使用 App Studio 帮助创建应用程序清单，也可以手动创建。</span><span class="sxs-lookup"><span data-stu-id="bcb41-144">You can either use App Studio to help you create your app manifest, or create it manually.</span></span>

### <a name="create-your-app-manifest-using-app-studio"></a><span data-ttu-id="bcb41-145">使用应用程序 Studio 创建应用程序清单</span><span class="sxs-lookup"><span data-stu-id="bcb41-145">Create your app manifest using App Studio</span></span>

<span data-ttu-id="bcb41-146">您可以使用 Microsoft 团队客户端中的应用程序 Studio 应用来帮助创建应用程序清单。</span><span class="sxs-lookup"><span data-stu-id="bcb41-146">You can use the App Studio app from within the Microsoft Teams client to help create your app manifest.</span></span>

1. <span data-ttu-id="bcb41-147">在 Teams 客户端中，从左侧导航栏上的“**…**”溢出菜单中打开 App Studio。</span><span class="sxs-lookup"><span data-stu-id="bcb41-147">In the Teams client, open App Studio from the **...** overflow menu on the left navigation rail.</span></span> <span data-ttu-id="bcb41-148">如果尚未安装，可以通过搜索来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="bcb41-148">If it isn't already installed, you can do so by searching for it.</span></span>
2. <span data-ttu-id="bcb41-149">在 " **清单编辑器** " 选项卡上，选择 " **新建应用程序** " (如果要将邮件扩展添加到现有应用程序，可以导入应用程序包) </span><span class="sxs-lookup"><span data-stu-id="bcb41-149">On the **Manifest editor** tab select **Create a new app** (or if you're adding a messaging extension to an existing app, you can import your app package)</span></span>
3. <span data-ttu-id="bcb41-150">添加应用详细信息（有关每个字段的完整说明，请参阅[清单架构定义](~/resources/schema/manifest-schema.md)）。</span><span class="sxs-lookup"><span data-stu-id="bcb41-150">Add your app details (see [manifest schema definition](~/resources/schema/manifest-schema.md) for full descriptions of each field).</span></span>
4. <span data-ttu-id="bcb41-151">在 " **邮件扩展** " 选项卡上，单击 " **设置** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="bcb41-151">On the **Messaging extensions** tab click the **Setup** button.</span></span>
5. <span data-ttu-id="bcb41-152">您可以创建新的 web 服务 (bot) 以供您的邮件扩展使用，或者，如果您已注册，请在此处选择/添加一个。</span><span class="sxs-lookup"><span data-stu-id="bcb41-152">You can either create a new web service (bot) for your messaging extension to use, or if you've already registered one select/add it here.</span></span>
6. <span data-ttu-id="bcb41-153">如有必要，请更新自动程序终结点地址以指向你的自动程序。</span><span class="sxs-lookup"><span data-stu-id="bcb41-153">If necessary, update your bot endpoint address to point to your bot.</span></span> <span data-ttu-id="bcb41-154">它应该类似于 `https://someplace.com/api/messages`。</span><span class="sxs-lookup"><span data-stu-id="bcb41-154">It should look something like `https://someplace.com/api/messages`.</span></span>
7. <span data-ttu-id="bcb41-155">"**命令**" 部分的 "**添加**" 按钮将指导您将命令添加到邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="bcb41-155">The **Add** button in the **Command** section will guide you through adding commands to your messaging extension.</span></span> <span data-ttu-id="bcb41-156">有关添加命令的详细信息，请参阅 " [了解更多](#learn-more) " 部分。</span><span class="sxs-lookup"><span data-stu-id="bcb41-156">See the [Learn more](#learn-more) section for links to more information on adding commands.</span></span> <span data-ttu-id="bcb41-157">请记住，您最长可为邮件扩展定义10个命令。</span><span class="sxs-lookup"><span data-stu-id="bcb41-157">Remember you can define up to 10 commands for your messaging extension.</span></span>
8. <span data-ttu-id="bcb41-158">通过 " **邮件处理程序** " 部分，您可以添加将在其中触发消息的域。</span><span class="sxs-lookup"><span data-stu-id="bcb41-158">The **Message Handlers** section allows you to add a domain that your messaging will trigger on.</span></span> <span data-ttu-id="bcb41-159">有关详细信息，请参阅 [link unfurling](~/messaging-extensions/how-to/link-unfurling.md) 。</span><span class="sxs-lookup"><span data-stu-id="bcb41-159">See [link unfurling](~/messaging-extensions/how-to/link-unfurling.md) for more information.</span></span>

<span data-ttu-id="bcb41-160">从 " **完成 => 测试和分布** " 选项卡上，您可以 **下载** 应用程序包 (其中包括您的应用程序清单和应用程序图标) 或 **安装** 程序包。</span><span class="sxs-lookup"><span data-stu-id="bcb41-160">From the **Finish => Test and distribute** tab you can **Download** your app package (which includes your app manifest as well as your app icons), or **Install** the package.</span></span>

### <a name="create-your-app-manifest-manually"></a><span data-ttu-id="bcb41-161">手动创建应用程序清单</span><span class="sxs-lookup"><span data-stu-id="bcb41-161">Create your app manifest manually</span></span>

<span data-ttu-id="bcb41-162">与 bot 和选项卡一样，您可以更新应用程序 [清单](~/resources/schema/manifest-schema.md#composeextensions) 以包含邮件扩展属性。</span><span class="sxs-lookup"><span data-stu-id="bcb41-162">As with bots and tabs, you update the [app manifest](~/resources/schema/manifest-schema.md#composeextensions) of your app to include the messaging extension properties.</span></span> <span data-ttu-id="bcb41-163">这些属性控制您的邮件扩展在 Microsoft 团队客户端中的显示和行为。</span><span class="sxs-lookup"><span data-stu-id="bcb41-163">These properties govern how your messaging extension appears and behaves in the Microsoft Teams client.</span></span> <span data-ttu-id="bcb41-164">从清单的1.0 版开始，支持邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="bcb41-164">Messaging extensions are supported beginning with v1.0 of the manifest.</span></span>

#### <a name="declare-your-messaging-extension"></a><span data-ttu-id="bcb41-165">声明消息扩展</span><span class="sxs-lookup"><span data-stu-id="bcb41-165">Declare your messaging extension</span></span>

<span data-ttu-id="bcb41-166">若要添加消息扩展，请在应用程序清单中将新的顶级 JSON 结构包含在 `composeExtensions` 属性中。</span><span class="sxs-lookup"><span data-stu-id="bcb41-166">To add a messaging extension, include a new top-level JSON structure in your app manifest with the `composeExtensions` property.</span></span> <span data-ttu-id="bcb41-167">您可以为您的应用程序创建一个单一的邮件扩展，最长可包含10个命令。</span><span class="sxs-lookup"><span data-stu-id="bcb41-167">You create a single messaging extension for your app, with up to 10 commands.</span></span>

> [!NOTE]
> <span data-ttu-id="bcb41-168">清单将邮件传递扩展作为引用 `composeExtensions` 。</span><span class="sxs-lookup"><span data-stu-id="bcb41-168">The manifest refers to messaging extensions as `composeExtensions`.</span></span> <span data-ttu-id="bcb41-169">这是为了保持向后兼容性。</span><span class="sxs-lookup"><span data-stu-id="bcb41-169">This is to maintain backward compatibility.</span></span>

<span data-ttu-id="bcb41-170">扩展定义是一个具有以下结构的对象：</span><span class="sxs-lookup"><span data-stu-id="bcb41-170">The extension definition is an object that has the following structure:</span></span>

| <span data-ttu-id="bcb41-171">属性名称</span><span class="sxs-lookup"><span data-stu-id="bcb41-171">Property name</span></span> | <span data-ttu-id="bcb41-172">用途</span><span class="sxs-lookup"><span data-stu-id="bcb41-172">Purpose</span></span> | <span data-ttu-id="bcb41-173">是否必需？</span><span class="sxs-lookup"><span data-stu-id="bcb41-173">Required?</span></span> |
|---|---|---|
| `botId` | <span data-ttu-id="bcb41-174">使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="bcb41-174">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="bcb41-175">通常应与整个团队应用程序的 ID 相同。</span><span class="sxs-lookup"><span data-stu-id="bcb41-175">This should typically be the same as the ID for your overall Teams app.</span></span> | <span data-ttu-id="bcb41-176">是</span><span class="sxs-lookup"><span data-stu-id="bcb41-176">Yes</span></span> |
| `canUpdateConfiguration` | <span data-ttu-id="bcb41-177">启用 " **设置** " 菜单项。</span><span class="sxs-lookup"><span data-stu-id="bcb41-177">Enables **Settings** menu item.</span></span> | <span data-ttu-id="bcb41-178">否</span><span class="sxs-lookup"><span data-stu-id="bcb41-178">No</span></span> |
| `commands` | <span data-ttu-id="bcb41-179">此消息扩展支持的命令数组。</span><span class="sxs-lookup"><span data-stu-id="bcb41-179">Array of commands that this messaging extension supports.</span></span> <span data-ttu-id="bcb41-180">限制为10个命令。</span><span class="sxs-lookup"><span data-stu-id="bcb41-180">You are limited to 10 commands.</span></span> | <span data-ttu-id="bcb41-181">是</span><span class="sxs-lookup"><span data-stu-id="bcb41-181">Yes</span></span> |

#### <a name="define-your-commands"></a><span data-ttu-id="bcb41-182">定义命令</span><span class="sxs-lookup"><span data-stu-id="bcb41-182">Define your commands</span></span>

<span data-ttu-id="bcb41-183">您的邮件扩展应声明一个或多个命令，这些命令定义用户可以触发邮件扩展的位置和交互的类型。</span><span class="sxs-lookup"><span data-stu-id="bcb41-183">Your messaging extension should declare one or more commands, which define where your users can trigger your messaging extension, and the type of interaction.</span></span> <span data-ttu-id="bcb41-184">有关消息扩展命令的详细信息，请参阅 [了解详细](#learn-more) 信息。</span><span class="sxs-lookup"><span data-stu-id="bcb41-184">See [learn more](#learn-more) for more information on messaging extension commands.</span></span>

#### <a name="simple-manifest-example"></a><span data-ttu-id="bcb41-185">简单清单示例</span><span class="sxs-lookup"><span data-stu-id="bcb41-185">Simple manifest example</span></span>

<span data-ttu-id="bcb41-186">下面的示例是包含搜索命令的应用程序清单中的一个简单的消息扩展对象。</span><span class="sxs-lookup"><span data-stu-id="bcb41-186">The example below is a simple messaging extension object in the app manifest with a search command.</span></span> <span data-ttu-id="bcb41-187">这不是整个应用程序清单文件，只是特定于消息传递扩展的部分。</span><span class="sxs-lookup"><span data-stu-id="bcb41-187">This is not the entire app manifest file, just the part specific to messaging extensions.</span></span> <span data-ttu-id="bcb41-188">有关完整示例，请参阅 [应用部件清单](~/resources/schema/manifest-schema.md) （manifest）架构。</span><span class="sxs-lookup"><span data-stu-id="bcb41-188">See [app manifest schema](~/resources/schema/manifest-schema.md) for a complete example.</span></span>

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

## <a name="add-your-invoke-message-handlers"></a><span data-ttu-id="bcb41-189">添加调用消息处理程序</span><span class="sxs-lookup"><span data-stu-id="bcb41-189">Add your invoke message handlers</span></span>

<span data-ttu-id="bcb41-190">当用户触发邮件扩展时，您需要处理初始调用邮件，收集用户的某些信息，然后处理该信息并做出相应的响应。</span><span class="sxs-lookup"><span data-stu-id="bcb41-190">When your users trigger your messaging extension you'll need to handle the initial invoke message, collect some information from the user, then process that information and respond appropriately.</span></span> <span data-ttu-id="bcb41-191">若要执行此操作，首先需要决定要向邮件扩展中添加的命令类型，并 [添加操作命令](~/messaging-extensions/how-to/action-commands/define-action-command.md) 或 [添加搜索命令](~/messaging-extensions/how-to/search-commands/define-search-command.md)。</span><span class="sxs-lookup"><span data-stu-id="bcb41-191">To do that, you'll first need to decide what kind of commands you want to add to your messaging extension and either [add an action commands](~/messaging-extensions/how-to/action-commands/define-action-command.md) or [add a search commands](~/messaging-extensions/how-to/search-commands/define-search-command.md).</span></span>

## <a name="messaging-extensions-in-teams-meetings"></a><span data-ttu-id="bcb41-192">团队会议中的邮件扩展</span><span class="sxs-lookup"><span data-stu-id="bcb41-192">Messaging extensions in Teams meetings</span></span>

<span data-ttu-id="bcb41-193">会议开始后，团队参与者可以在实时呼叫过程中与您的邮件扩展直接交互。</span><span class="sxs-lookup"><span data-stu-id="bcb41-193">Once a meeting begins, Teams participants can interact directly with your messaging extension during a live call.</span></span> <span data-ttu-id="bcb41-194">在构建会议内邮件扩展时，请考虑以下几点：</span><span class="sxs-lookup"><span data-stu-id="bcb41-194">Consider the following when building your in-meeting messaging extension:</span></span>

1. <span data-ttu-id="bcb41-195">**Location**。</span><span class="sxs-lookup"><span data-stu-id="bcb41-195">**Location**.</span></span> <span data-ttu-id="bcb41-196">您的邮件扩展可以从撰写邮件区域、命令框或会议聊天 @mentioned 中进行调用。</span><span class="sxs-lookup"><span data-stu-id="bcb41-196">Your messaging extension can be invoked from the compose message area, the command box, or @mentioned in the meeting chat.</span></span>

1. <span data-ttu-id="bcb41-197">**元数据**。</span><span class="sxs-lookup"><span data-stu-id="bcb41-197">**Metadata**.</span></span> <span data-ttu-id="bcb41-198">调用邮件扩展时，可以通过和来识别用户和租户 `userId` `tenantId` 。</span><span class="sxs-lookup"><span data-stu-id="bcb41-198">When your messaging extension is invoked it can identify the user and tenant from `userId` and `tenantId`.</span></span> <span data-ttu-id="bcb41-199">可在 `channelData` 对象中找到 `meetingId`。</span><span class="sxs-lookup"><span data-stu-id="bcb41-199">The `meetingId` can be found as part of the `channelData` object.</span></span> <span data-ttu-id="bcb41-200">您的应用程序可以使用 `userId` 和， `meetingId`  以获取用于 `GetParticipant` 检索用户角色的 API 请求。</span><span class="sxs-lookup"><span data-stu-id="bcb41-200">Your app can use the `userId` and `meetingId`  for the `GetParticipant` API request to retrieve user roles.</span></span>

1. <span data-ttu-id="bcb41-201">**命令类型**。</span><span class="sxs-lookup"><span data-stu-id="bcb41-201">**Command type**.</span></span> <span data-ttu-id="bcb41-202">如果您的邮件扩展使用 [基于操作的命令](../../messaging-extensions/what-are-messaging-extensions.md#action-commands)，它应遵循选项卡式 [单一登录](../../tabs/how-to/authentication/auth-aad-sso.md) 身份验证。</span><span class="sxs-lookup"><span data-stu-id="bcb41-202">If your message extension uses [action-based commands](../../messaging-extensions/what-are-messaging-extensions.md#action-commands), it should follow tabs [single sign-on](../../tabs/how-to/authentication/auth-aad-sso.md) authentication.</span></span>

1. <span data-ttu-id="bcb41-203">**用户体验**。</span><span class="sxs-lookup"><span data-stu-id="bcb41-203">**User experience**.</span></span> <span data-ttu-id="bcb41-204">您应确定会议聊天过程中调用的最终用户体验邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="bcb41-204">You should determine the intended the end-user experience for messaging extensions invoked during a meeting chat.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcb41-205">后续步骤</span><span class="sxs-lookup"><span data-stu-id="bcb41-205">Next steps</span></span>

* [<span data-ttu-id="bcb41-206">创建操作命令</span><span class="sxs-lookup"><span data-stu-id="bcb41-206">Create action commands</span></span>](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="bcb41-207">创建搜索命令</span><span class="sxs-lookup"><span data-stu-id="bcb41-207">Create search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [<span data-ttu-id="bcb41-208">链接展开</span><span class="sxs-lookup"><span data-stu-id="bcb41-208">Link unfurling</span></span>](~/messaging-extensions/how-to/link-unfurling.md)

## <a name="learn-more"></a><span data-ttu-id="bcb41-209">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="bcb41-209">Learn more</span></span>

<span data-ttu-id="bcb41-210">在快速入门中试用：</span><span class="sxs-lookup"><span data-stu-id="bcb41-210">Try it out in a quickstart:</span></span>

* <span data-ttu-id="bcb41-211">适用于 C 的快速入门#</span><span class="sxs-lookup"><span data-stu-id="bcb41-211">Quickstarts for C#</span></span>
  * [<span data-ttu-id="bcb41-212">带有基于操作的命令的消息扩展</span><span class="sxs-lookup"><span data-stu-id="bcb41-212">Messaging extension with action-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [<span data-ttu-id="bcb41-213">包含基于搜索的命令的邮件扩展</span><span class="sxs-lookup"><span data-stu-id="bcb41-213">Messaging extension with search-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* <span data-ttu-id="bcb41-214">适用于 JavaScript 的快速入门</span><span class="sxs-lookup"><span data-stu-id="bcb41-214">Quickstarts for JavaScript</span></span>
  * [<span data-ttu-id="bcb41-215">带有基于操作的命令的消息扩展</span><span class="sxs-lookup"><span data-stu-id="bcb41-215">Messaging extension with action-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [<span data-ttu-id="bcb41-216">包含基于搜索的命令的邮件扩展</span><span class="sxs-lookup"><span data-stu-id="bcb41-216">Messaging extension with search-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

<span data-ttu-id="bcb41-217">了解有关邮件扩展的详细信息概念：</span><span class="sxs-lookup"><span data-stu-id="bcb41-217">Learn more about messaging extensions concepts:</span></span>

* [<span data-ttu-id="bcb41-218">了解团队应用程序功能？</span><span class="sxs-lookup"><span data-stu-id="bcb41-218">Understand Teams app capabilities ?</span></span>](~/concepts/extensibility-points.md)
* [<span data-ttu-id="bcb41-219">什么是邮件扩展？</span><span class="sxs-lookup"><span data-stu-id="bcb41-219">What are messaging extensions?</span></span>](~/messaging-extensions/what-are-messaging-extensions.md)
