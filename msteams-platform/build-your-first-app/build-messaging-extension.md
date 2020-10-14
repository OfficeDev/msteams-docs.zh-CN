---
title: 入门-构建消息扩展
author: heath-hamilton
description: 使用 Microsoft 团队工具包快速创建 Microsoft 团队消息扩展。
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
ms.openlocfilehash: b19856eacee866ebbc89f21ac12575f1392918b3
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452832"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="68f6d-103">为 Microsoft 团队构建消息扩展</span><span class="sxs-lookup"><span data-stu-id="68f6d-103">Build a messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="68f6d-104">有两种类型的团队 *邮件扩展*： [搜索命令](../messaging-extensions/how-to/search-commands/define-search-command.md) 和 [动作命令](../messaging-extensions/how-to/action-commands/define-action-command.md)。</span><span class="sxs-lookup"><span data-stu-id="68f6d-104">There are two types of Teams *messaging extensions*: [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="68f6d-105">在本课中，您将创建一个 *搜索命令* (也称为 " *基于搜索的邮件扩展* ") ，这是查找外部内容并在团队中共享它的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="68f6d-105">In this lesson, you'll create a *search command* (also known as a *search-based messaging extension*), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="68f6d-106">用户可以从 " [团队撰写" 或 "命令" 框](../messaging-extensions/what-are-messaging-extensions.md)中访问搜索命令。</span><span class="sxs-lookup"><span data-stu-id="68f6d-106">Users can access search commands from the [Teams compose or command box](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="68f6d-107">您的分配</span><span class="sxs-lookup"><span data-stu-id="68f6d-107">Your assignment</span></span>

<span data-ttu-id="68f6d-108">您的组织的技术支持人员通过团队与用户通信，但票证驻留在单独的系统中。</span><span class="sxs-lookup"><span data-stu-id="68f6d-108">Your organization's help desk communicates with users through Teams, but the tickets reside in a separate system.</span></span> <span data-ttu-id="68f6d-109">这意味着支持人员必须在应用程序之间持续来回切换。</span><span class="sxs-lookup"><span data-stu-id="68f6d-109">This means support staff must constantly go back and forth between apps.</span></span> <span data-ttu-id="68f6d-110">您将通过为工作组创建简单的基于搜索的邮件扩展功能，来研究如何减少这种更多的上下文切换。</span><span class="sxs-lookup"><span data-stu-id="68f6d-110">You'll investigate how you might reduce this much context switching by creating a simple search-based messaging extension for Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="68f6d-111">你将了解的内容</span><span class="sxs-lookup"><span data-stu-id="68f6d-111">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="68f6d-112">使用 Microsoft 团队工具包为 Visual Studio Code 创建应用程序项目和邮件扩展 bot</span><span class="sxs-lookup"><span data-stu-id="68f6d-112">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="68f6d-113">标识应用程序清单属性和一些与邮件扩展相关的基架</span><span class="sxs-lookup"><span data-stu-id="68f6d-113">Identify the app manifest properties and some of the scaffolding relevant to messaging extensions</span></span>
> * <span data-ttu-id="68f6d-114">在本地托管应用程序</span><span class="sxs-lookup"><span data-stu-id="68f6d-114">Host an app locally</span></span>
> * <span data-ttu-id="68f6d-115">为邮件扩展配置 bot</span><span class="sxs-lookup"><span data-stu-id="68f6d-115">Configure the bot for your messaging extension</span></span>
> * <span data-ttu-id="68f6d-116">旁加载和测试团队中的邮件扩展</span><span class="sxs-lookup"><span data-stu-id="68f6d-116">Sideload and test a messaging extension in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="68f6d-117">准备工作</span><span class="sxs-lookup"><span data-stu-id="68f6d-117">Before you begin</span></span>

<span data-ttu-id="68f6d-118">如果还没有，请确保 [了解并安装团队开发先决条件](build-first-app-overview.md#get-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="68f6d-118">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="68f6d-119">1. 创建您的应用程序项目</span><span class="sxs-lookup"><span data-stu-id="68f6d-119">1. Create your app project</span></span>

<span data-ttu-id="68f6d-120">Microsoft 团队工具包可帮助您为邮件扩展设置以下组件：</span><span class="sxs-lookup"><span data-stu-id="68f6d-120">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="68f6d-121">与邮件扩展相关的**应用程序清单和基架**</span><span class="sxs-lookup"><span data-stu-id="68f6d-121">**App manifest and scaffolding** relevant to messaging extensions</span></span>
* <span data-ttu-id="68f6d-122">自动注册到 Microsoft Azure Bot 服务的邮件扩展的**Bot**</span><span class="sxs-lookup"><span data-stu-id="68f6d-122">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="68f6d-123">如果之前尚未创建团队应用程序项目，您可能会发现，请按照 [以下说明](../build-your-first-app/build-and-run.md) 更详细地说明项目。</span><span class="sxs-lookup"><span data-stu-id="68f6d-123">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队**"， :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 " **创建新的团队应用**"。
1. <span data-ttu-id="68f6d-125">为你的团队应用输入名称。</span><span class="sxs-lookup"><span data-stu-id="68f6d-125">Enter a name for your Teams app.</span></span> <span data-ttu-id="68f6d-126"> (这是您的应用程序的默认名称，也是本地计算机上的应用程序项目目录的名称。 ) </span><span class="sxs-lookup"><span data-stu-id="68f6d-126">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="68f6d-127">在 " **添加功能** " 屏幕上，依次选择 " **消息扩展** " 和 " **下一步**"</span><span class="sxs-lookup"><span data-stu-id="68f6d-127">On the **Add capabilities** screen, select **Messaging Extension** then **Next**.</span></span>
1. <span data-ttu-id="68f6d-128">在 " **配置消息扩展** " 屏幕上，执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="68f6d-128">On the **Configure messaging extension** screen, do the following:</span></span>
    1. <span data-ttu-id="68f6d-129">为邮件扩展类型选择 " **基于搜索** 的选项"。</span><span class="sxs-lookup"><span data-stu-id="68f6d-129">Choose only the **Search-based** option for the type of messaging extension.</span></span>
    1. <span data-ttu-id="68f6d-130">选择 " **创建新的 Bot** 并 **登录** " 以使用 Microsoft 365 开发帐户登录。</span><span class="sxs-lookup"><span data-stu-id="68f6d-130">Select **Create a new Bot** and **Login** to sign in with your Microsoft 365 development account.</span></span>
    1. <span data-ttu-id="68f6d-131">将你的 bot ID 和密码存储 (稍后需要一些) 。</span><span class="sxs-lookup"><span data-stu-id="68f6d-131">Store your bot ID and password (you need this a little later).</span></span>
    1. <span data-ttu-id="68f6d-132"> (可选) 输入你的 bot 的自定义名称，然后选择 " **创建**"。</span><span class="sxs-lookup"><span data-stu-id="68f6d-132">(Optional) Enter a custom name for your bot and select **Create**.</span></span> <span data-ttu-id="68f6d-133"> (这不是已指定的团队应用程序的名称。 ) </span><span class="sxs-lookup"><span data-stu-id="68f6d-133">(This is not the name of the Teams app you already specified.)</span></span>
    1. <span data-ttu-id="68f6d-134">现在，为 "链接 unfurling" 选择 " **否** " 选项。</span><span class="sxs-lookup"><span data-stu-id="68f6d-134">For now, select **No** for the link unfurling option.</span></span></br>
:::image type="content" source="../assets/images/build-your-first-app/choose-me-search.png" alt-text="演示如何在团队工具包中登录到 Microsoft 365 帐户，以创建用于邮件扩展的新 bot。":::
1. <span data-ttu-id="68f6d-136">选择屏幕底部的 " **完成** " 以配置项目。</span><span class="sxs-lookup"><span data-stu-id="68f6d-136">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="68f6d-137">2. 确定相关的应用程序项目组件</span><span class="sxs-lookup"><span data-stu-id="68f6d-137">2. Identify relevant app project components</span></span>

<span data-ttu-id="68f6d-138">大多数应用程序清单和基架是在使用团队工具包创建项目时自动设置的。</span><span class="sxs-lookup"><span data-stu-id="68f6d-138">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="68f6d-139">应用程序清单</span><span class="sxs-lookup"><span data-stu-id="68f6d-139">App manifest</span></span>

<span data-ttu-id="68f6d-140">应用程序清单中的以下代码片段 (`manifest.json` 项目目录中的文件 `.publish`) 显示与邮件扩展相关的属性和默认值。</span><span class="sxs-lookup"><span data-stu-id="68f6d-140">The following snippet from the app manifest (the `manifest.json` file in your project's `.publish` directory) shows the properties and default values relevant to messaging extensions.</span></span>

```JSON
"composeExtensions": [
    {
        "botId": "{botId0}",
        "canUpdateConfiguration": true,
        "commands": [
            {
                "id": "searchQuery",
                "context": [
                    "compose",
                    "commandBox"
                ],
                "description": "Test command to run query",
                "title": "Search",
                "type": "query",
                "parameters": [
                    {
                        "name": "searchQuery",
                        "title": "Search Query",
                        "description": "Your search query",
                        "inputType": "text"
                    }
                ]
            }
        ]
    }
],
```

<span data-ttu-id="68f6d-141">让我们了解工具包为你创建的一些属性。</span><span class="sxs-lookup"><span data-stu-id="68f6d-141">Let's understand some of the properties the toolkit created for you.</span></span> <span data-ttu-id="68f6d-142"> (查看受支持属性的完整列表 [`composeExtensions`](../resources/schema/manifest-schema.md#composeextensions) 。 ) </span><span class="sxs-lookup"><span data-stu-id="68f6d-142">(See the full list of supported [`composeExtensions`](../resources/schema/manifest-schema.md#composeextensions) properties.)</span></span>

* <span data-ttu-id="68f6d-143">`botId`：你创建的你的项目设置的 bot 的 ID。</span><span class="sxs-lookup"><span data-stu-id="68f6d-143">`botId`: The ID of the bot you created setting up your project.</span></span> <span data-ttu-id="68f6d-144"> (存储在中 `{botId0}` ，则可以在中查找实际的 ID `Development.env` 。 ) </span><span class="sxs-lookup"><span data-stu-id="68f6d-144">(Stored in `{botId0}`, you can find the actual ID in `Development.env`.)</span></span>
* <span data-ttu-id="68f6d-145">`commands`：邮件扩展的可用命令。</span><span class="sxs-lookup"><span data-stu-id="68f6d-145">`commands`: Available commands for the messaging extension.</span></span> <span data-ttu-id="68f6d-146">该工具包为您提供了搜索命令的基架。</span><span class="sxs-lookup"><span data-stu-id="68f6d-146">The toolkit provided you scaffolding for a search command.</span></span>
* <span data-ttu-id="68f6d-147">`context`：用户可以在其中调用邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="68f6d-147">`context`: Where users can invoke the messaging extension.</span></span> <span data-ttu-id="68f6d-148">在这种情况下，可以从 "团队撰写" 或 "命令" 框启动邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="68f6d-148">In this case, you can launch the messaging extension from the Teams compose or command box.</span></span>
* <span data-ttu-id="68f6d-149">`description`： UI 帮助文本，用于指示命令的用途或用法。</span><span class="sxs-lookup"><span data-stu-id="68f6d-149">`description`: UI help text indicating what the command does or how to use it.</span></span>
* <span data-ttu-id="68f6d-150">`parameters`：包含所有参数一个命令接受 (必须至少有一个，并且最多可以有五个) 。</span><span class="sxs-lookup"><span data-stu-id="68f6d-150">`parameters`: Includes all parameters a command accepts (you must have at least one and can have up to five).</span></span>
* <span data-ttu-id="68f6d-151">`parameters.description`： UI 帮助文本，用于描述参数的用途或示例输入。</span><span class="sxs-lookup"><span data-stu-id="68f6d-151">`parameters.description`: UI help text describing the parameter's purpose or example input.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="68f6d-152">应用程序基架</span><span class="sxs-lookup"><span data-stu-id="68f6d-152">App scaffolding</span></span>

<span data-ttu-id="68f6d-153">应用程序基架包含一个 `.env` 文件，该文件位于项目的根目录中，用于存储邮件扩展机器人的 ID 和密码。</span><span class="sxs-lookup"><span data-stu-id="68f6d-153">The app scaffolding includes a `.env` file, located in the root directory of your project, which stores the ID and password of your messaging extension's bot.</span></span>

<span data-ttu-id="68f6d-154">此外，在根目录中，还有一个 `botActivityHandler.js` 用于处理邮件扩展 (或技术方面的文件， [邮件扩展程序的 Bot](#4-configure-the-bot-for-your-messaging-extension)) 响应团队中的搜索查询。</span><span class="sxs-lookup"><span data-stu-id="68f6d-154">Also in the root directory, there's a `botActivityHandler.js` file for handling how your messaging extension (or technically, the [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="68f6d-155">3. 设置应用程序的安全隧道</span><span class="sxs-lookup"><span data-stu-id="68f6d-155">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="68f6d-156">出于测试目的，让我们在本地 web 服务器上托管您的邮件扩展 (端口 3978) 。</span><span class="sxs-lookup"><span data-stu-id="68f6d-156">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span>

1. <span data-ttu-id="68f6d-157">在终端中，运行 `ngrok http -host-header=rewrite 3978` 。</span><span class="sxs-lookup"><span data-stu-id="68f6d-157">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="68f6d-158">在输出中复制 HTTPS URL，因为团队需要 HTTPS 连接。</span><span class="sxs-lookup"><span data-stu-id="68f6d-158">Copy the HTTPS URL in the output since Teams requires HTTPS connections.</span></span>
1. <span data-ttu-id="68f6d-159">在 `.publish` 目录中，打开 `Development.env` 。</span><span class="sxs-lookup"><span data-stu-id="68f6d-159">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="68f6d-160">将 `baseUrl0` 值替换为复制的 URL。</span><span class="sxs-lookup"><span data-stu-id="68f6d-160">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="68f6d-161"> (例如，改 `baseUrl0=http://localhost:3000` 为 `baseUrl0=https://85528b2b3ca5.ngrok.io` 。 ) </span><span class="sxs-lookup"><span data-stu-id="68f6d-161">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ca5.ngrok.io`.)</span></span>

<span data-ttu-id="68f6d-162">您的应用程序清单指向你承载邮件扩展使用的 bot 的位置。</span><span class="sxs-lookup"><span data-stu-id="68f6d-162">Your app manifest is pointing to where you're hosting the bot used by the messaging extension.</span></span>

## <a name="4-configure-the-bot-for-your-messaging-extension"></a><span data-ttu-id="68f6d-163">4. 配置邮件扩展的 bot</span><span class="sxs-lookup"><span data-stu-id="68f6d-163">4. Configure the bot for your messaging extension</span></span>

<span data-ttu-id="68f6d-164">邮件扩展依靠 bot 来发送和处理从团队到托管服务的用户请求。</span><span class="sxs-lookup"><span data-stu-id="68f6d-164">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span>

<span data-ttu-id="68f6d-165">自动程序必须在 Azure Bot 服务中注册，这是在使用团队工具包设置应用程序时完成的。</span><span class="sxs-lookup"><span data-stu-id="68f6d-165">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

### <a name="specify-your-bot-id-and-password"></a><span data-ttu-id="68f6d-166">指定你的 bot ID 和密码</span><span class="sxs-lookup"><span data-stu-id="68f6d-166">Specify your bot ID and password</span></span>

<span data-ttu-id="68f6d-167">在使用 Azure Bot 服务注册你的 bot 时，系统会为你的团队应用必须知道的 ID 和密码分配你的 bot。</span><span class="sxs-lookup"><span data-stu-id="68f6d-167">When your bot is registered with the Azure Bot Service, it's assigned an ID and password that your Teams app must know about.</span></span>

1. <span data-ttu-id="68f6d-168">查找在工具包设置过程中存储的 bot ID 和密码。</span><span class="sxs-lookup"><span data-stu-id="68f6d-168">Locate the bot ID and password you stored during toolkit setup.</span></span>
1. <span data-ttu-id="68f6d-169">在您的根目录中，打开该 `.env` 文件。</span><span class="sxs-lookup"><span data-stu-id="68f6d-169">In your root directory, open the `.env` file.</span></span>
1. <span data-ttu-id="68f6d-170">分别将机器人 ID 和密码分别设置为 `BotId` 和 `BotPassword` 属性。</span><span class="sxs-lookup"><span data-stu-id="68f6d-170">Set your bot ID and password to the `BotId` and `BotPassword` properties, respectively.</span></span>

### <a name="add-the-bot-endpoint-address"></a><span data-ttu-id="68f6d-171">添加 bot 终结点地址</span><span class="sxs-lookup"><span data-stu-id="68f6d-171">Add the bot endpoint address</span></span>

<span data-ttu-id="68f6d-172">您必须指定用于接收和处理邮件扩展中的搜索查询的 bot 终结点 URL。</span><span class="sxs-lookup"><span data-stu-id="68f6d-172">You must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="68f6d-173">通常，URL 如下所示 `https://HOST_URL/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="68f6d-173">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="68f6d-174">您可以在团队工具包中快速配置此设置。</span><span class="sxs-lookup"><span data-stu-id="68f6d-174">You can configure this quickly in the Teams Toolkit.</span></span>

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队**"， :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 " **打开 Microsoft 团队工具包**"。
1. <span data-ttu-id="68f6d-176">转到 **Bot 管理 > 现有的 bot 注册** ，并选择在安装过程中创建的 bot。</span><span class="sxs-lookup"><span data-stu-id="68f6d-176">Go to **Bot management > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="68f6d-177">在 " **机器人终结点地址** " 字段中，输入您在其中承载机器人的本地 web 服务器 (`baseUrl10` 值) 并追加 `/api/messages` 到它。</span><span class="sxs-lookup"><span data-stu-id="68f6d-177">In the **Bot endpoint address** field, enter the local web server where you're hosting the bot (`baseUrl10` value) and append `/api/messages` to it.</span></span>

<span data-ttu-id="68f6d-178">你的 bot 将能够处理你的邮件扩展中的查询。</span><span class="sxs-lookup"><span data-stu-id="68f6d-178">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="5-run-your-app"></a><span data-ttu-id="68f6d-179">5. 运行您的应用程序</span><span class="sxs-lookup"><span data-stu-id="68f6d-179">5. Run your app</span></span>

<span data-ttu-id="68f6d-180">您已经设置了一个 URL 来托管您的邮件扩展并将其配置为处理搜索。</span><span class="sxs-lookup"><span data-stu-id="68f6d-180">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="68f6d-181">现在就可以启动并运行您的应用程序了。</span><span class="sxs-lookup"><span data-stu-id="68f6d-181">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="68f6d-182">在终端中，转到您的应用程序项目的根目录并运行该目录 `npm install` 。</span><span class="sxs-lookup"><span data-stu-id="68f6d-182">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="68f6d-183">运行 `npm start` 。</span><span class="sxs-lookup"><span data-stu-id="68f6d-183">Run `npm start`.</span></span>

<span data-ttu-id="68f6d-184">如果成功，你会看到类似于以下的消息，指示你的邮件扩展服务正在侦听以下内容中的活动 `localhost` ：</span><span class="sxs-lookup"><span data-stu-id="68f6d-184">If successful, you see something like the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="68f6d-185">6. 旁加载您的邮件扩展在团队中</span><span class="sxs-lookup"><span data-stu-id="68f6d-185">6. Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="68f6d-186">在邮件扩展运行的情况下，可以将其安装在团队中。</span><span class="sxs-lookup"><span data-stu-id="68f6d-186">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="68f6d-187">如果您在之前未旁加载团队应用程序并遇到问题，请按照这些 [说明](../build-your-first-app/build-and-run.md#5-sideload-your-app-in-teams)进行操作。</span><span class="sxs-lookup"><span data-stu-id="68f6d-187">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#5-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="68f6d-188">使用允许应用旁加载的帐户登录到团队客户端。</span><span class="sxs-lookup"><span data-stu-id="68f6d-188">Log in to the Teams client with your account that allows app sideloading.</span></span>
1. <span data-ttu-id="68f6d-189">选择 " **应用**"，然后选择 " **上载自定义应用**"。</span><span class="sxs-lookup"><span data-stu-id="68f6d-189">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="68f6d-190">转到您的应用程序项目 `.publish` 文件夹，然后选择 `Development.zip` 。</span><span class="sxs-lookup"><span data-stu-id="68f6d-190">Go to your app project `.publish` folder and select `Development.zip`.</span></span>
1. <span data-ttu-id="68f6d-191">在 "安装模式" 中，选择 " **添加** " 以安装您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="68f6d-191">In the install modal, select **Add** to install your app.</span></span>

## <a name="7-test-your-messaging-extension"></a><span data-ttu-id="68f6d-192">7. 测试邮件扩展</span><span class="sxs-lookup"><span data-stu-id="68f6d-192">7. Test your messaging extension</span></span>

<span data-ttu-id="68f6d-193">了解邮件扩展在团队聊天中的工作方式。</span><span class="sxs-lookup"><span data-stu-id="68f6d-193">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="68f6d-194">启动新聊天。</span><span class="sxs-lookup"><span data-stu-id="68f6d-194">Start a new chat.</span></span> 在 "撰写" 框中，选择 " **更多** :::image type="icon" source="../assets/icons/teams-client-more.png"::: "，然后选择您刚刚旁加载的邮件扩展应用程序。<br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-access.png" alt-text="演示如何在团队工具包中登录到 Microsoft 365 帐户，以创建用于邮件扩展的新 bot。":::
1. <span data-ttu-id="68f6d-197">请尝试搜索某个内容 (例如，"入场券" ) 。</span><span class="sxs-lookup"><span data-stu-id="68f6d-197">Try searching for something (for example, "Tickets").</span></span> <span data-ttu-id="68f6d-198">如果你的应用程序正常运行，你将看到示例搜索结果 (你可以在以后添加自己的) 。</span><span class="sxs-lookup"><span data-stu-id="68f6d-198">If your app is working, you'll see sample search results (you can add your own later).</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="演示如何在团队工具包中登录到 Microsoft 365 帐户，以创建用于邮件扩展的新 bot。":::

## <a name="well-done"></a><span data-ttu-id="68f6d-200">干的好</span><span class="sxs-lookup"><span data-stu-id="68f6d-200">Well done</span></span>

<span data-ttu-id="68f6d-201">恭喜你！</span><span class="sxs-lookup"><span data-stu-id="68f6d-201">Congratulations!</span></span> <span data-ttu-id="68f6d-202">您有一个基本的工作组邮件扩展，它设置为在撰写或命令框中搜索外部内容。</span><span class="sxs-lookup"><span data-stu-id="68f6d-202">You have a basic Teams messaging extension that's set up to search for external content in the compose or command box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68f6d-203">后续步骤</span><span class="sxs-lookup"><span data-stu-id="68f6d-203">Next steps</span></span>

<span data-ttu-id="68f6d-204">请参阅以下页面以继续操作并生成功能齐全的邮件扩展：</span><span class="sxs-lookup"><span data-stu-id="68f6d-204">See the following pages to continue and build a fully featured messaging extension:</span></span>

1. <span data-ttu-id="68f6d-205">定义与您的服务相关的[搜索命令](../messaging-extensions/how-to/search-commands/define-search-command.md)。</span><span class="sxs-lookup"><span data-stu-id="68f6d-205">[Define search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) that are relevant to your service.</span></span>
1. <span data-ttu-id="68f6d-206">将您的服务配置为 [响应用户的搜索](../messaging-extensions/how-to/search-commands/respond-to-search.md)。</span><span class="sxs-lookup"><span data-stu-id="68f6d-206">Configure your service to [respond to users' searches](../messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="68f6d-207">疑难解答</span><span class="sxs-lookup"><span data-stu-id="68f6d-207">Troubleshooting</span></span>

<span data-ttu-id="68f6d-208">如果你在完成本教程时遇到问题，以下信息可能会有所帮助。</span><span class="sxs-lookup"><span data-stu-id="68f6d-208">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="toolkit-setup-fails"></a><span data-ttu-id="68f6d-209">工具包安装程序失败</span><span class="sxs-lookup"><span data-stu-id="68f6d-209">Toolkit setup fails</span></span>

<span data-ttu-id="68f6d-210">使用 "团队" 工具包设置应用程序项目时，在选择 " **创建新的 Bot** " 选项并使用 Microsoft 365 开发帐户登录后，将会收到错误消息。</span><span class="sxs-lookup"><span data-stu-id="68f6d-210">While setting up your app project with the Teams Toolkit, you get an error after selecting the **Create a new Bot** option and logging in with your Microsoft 365 development account.</span></span>

<span data-ttu-id="68f6d-211">这可能是身份验证问题。</span><span class="sxs-lookup"><span data-stu-id="68f6d-211">This could be an authentication issue.</span></span> <span data-ttu-id="68f6d-212">按照以下步骤完成对项目的设置。</span><span class="sxs-lookup"><span data-stu-id="68f6d-212">Follow these steps to finish setting up your project.</span></span>

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队**"， :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 " **注销**"。
1. <span data-ttu-id="68f6d-214">通过使用相同帐户登录并创建新的 bot，再次执行安装过程。</span><span class="sxs-lookup"><span data-stu-id="68f6d-214">Go through the setup process again by logging in with the same account and creating a new bot.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="68f6d-215">机器人未连接到团队</span><span class="sxs-lookup"><span data-stu-id="68f6d-215">Bot isn't connected to Teams</span></span>

<span data-ttu-id="68f6d-216">如果您安装了应用程序但不能正常运行，请确保消息扩展的 bot 已 [连接到 Azure Bot 服务的团队 *频道*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="68f6d-216">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="68f6d-217">请务必了解，这与团队中的频道不相同。</span><span class="sxs-lookup"><span data-stu-id="68f6d-217">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="68f6d-218">在这种情况下，通道是 Azure Bot 服务将你的 Bot 连接到团队或其他 [受支持的 Microsoft 或第三方通信应用程序](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)的方式。</span><span class="sxs-lookup"><span data-stu-id="68f6d-218">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="68f6d-219">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="68f6d-219">Learn more</span></span>

* [<span data-ttu-id="68f6d-220">包含链接 unfurling 功能</span><span class="sxs-lookup"><span data-stu-id="68f6d-220">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="68f6d-221">添加身份验证</span><span class="sxs-lookup"><span data-stu-id="68f6d-221">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="68f6d-222">创建基于操作的消息扩展</span><span class="sxs-lookup"><span data-stu-id="68f6d-222">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="68f6d-223">Microsoft Bot 框架</span><span class="sxs-lookup"><span data-stu-id="68f6d-223">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
