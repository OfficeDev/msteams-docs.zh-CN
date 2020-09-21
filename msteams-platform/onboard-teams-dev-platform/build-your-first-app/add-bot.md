---
title: 创建适合 Teams 的机器人
author: heath-hamilton
description: 了解如何在您的首个 Microsoft 团队应用程序中构建机器人。
ms.author: lajanuar
ms.date: 08/31/2020
ms.topic: tutorial
ms.openlocfilehash: f1307bcc7bb864ddfa97b9297f34fa4f7d5fcb0d
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964672"
---
# <a name="create-a-bot-for-teams"></a><span data-ttu-id="7ab9d-103">创建适合 Teams 的机器人</span><span class="sxs-lookup"><span data-stu-id="7ab9d-103">Create a bot for Teams</span></span>

<span data-ttu-id="7ab9d-104">您将在本教程中构建基本 *机器人* 应用程序。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-104">You'll build a basic *bot* app in this tutorial.</span></span> <span data-ttu-id="7ab9d-105">Bot 充当团队用户与 web 服务之间的媒介。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-105">A bot acts as an intermediary between Teams users and your web service.</span></span> <span data-ttu-id="7ab9d-106">用户可以与机器人聊天以快速获取信息或启动服务执行的工作流和任务。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="7ab9d-107">您的分配</span><span class="sxs-lookup"><span data-stu-id="7ab9d-107">Your assignment</span></span>

<span data-ttu-id="7ab9d-108">你的工作区已使用 [选项卡](../build-your-first-app/add-personal-tab.md) 在团队中呈现重要的联系人信息。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-108">Your workplace has been using [tabs](../build-your-first-app/add-personal-tab.md) to surface important contact information in Teams.</span></span> <span data-ttu-id="7ab9d-109">例如，同事可以快速访问技术支持电话号码。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-109">For example, colleagues have quick access to the help desk phone number.</span></span> <span data-ttu-id="7ab9d-110">而不是打电话，如果用户可以使用 chatbot 联系技术支持，该怎么办？</span><span class="sxs-lookup"><span data-stu-id="7ab9d-110">But instead of calling, what if people could contact the help desk using a chatbot?</span></span> <span data-ttu-id="7ab9d-111">你的老板要求你查看如何快速启动并在团队中运行基本的会话机器人。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-111">Your boss asks you to look at how quickly you can get a basic conversational bot up and running in Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="7ab9d-112">你将了解的内容</span><span class="sxs-lookup"><span data-stu-id="7ab9d-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="7ab9d-113">使用 Microsoft 团队工具包为 Visual Studio Code 创建一个应用程序项目和机器人</span><span class="sxs-lookup"><span data-stu-id="7ab9d-113">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="7ab9d-114">确定应用程序清单属性和与 bot 相关的一些基架</span><span class="sxs-lookup"><span data-stu-id="7ab9d-114">Identify the app manifest properties and some of the scaffolding relevant to bots</span></span>
> * <span data-ttu-id="7ab9d-115">在本地托管 bot</span><span class="sxs-lookup"><span data-stu-id="7ab9d-115">Host a bot locally</span></span>
> * <span data-ttu-id="7ab9d-116">为团队配置机器人</span><span class="sxs-lookup"><span data-stu-id="7ab9d-116">Configure a bot for Teams</span></span>
> * <span data-ttu-id="7ab9d-117">旁加载和测试团队中的 bot</span><span class="sxs-lookup"><span data-stu-id="7ab9d-117">Sideload and test a bot in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7ab9d-118">准备工作</span><span class="sxs-lookup"><span data-stu-id="7ab9d-118">Before you begin</span></span>

<span data-ttu-id="7ab9d-119">如果尚未安装，请设置你的 Microsoft 365 开发 [帐户](building-real-world-app.md#set-up-your-development-account) 和 [团队应用工具](building-real-world-app.md#install-your-development-tools)。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-119">If you haven't yet, set up your Microsoft 365 development [account](building-real-world-app.md#set-up-your-development-account) and [Teams app tools](building-real-world-app.md#install-your-development-tools).</span></span>

## <a name="create-your-app-project-and-bot"></a><span data-ttu-id="7ab9d-120">创建您的应用程序项目和机器人</span><span class="sxs-lookup"><span data-stu-id="7ab9d-120">Create your app project and bot</span></span>

<span data-ttu-id="7ab9d-121">Microsoft 团队工具包可帮助您为您的应用程序设置以下组件：</span><span class="sxs-lookup"><span data-stu-id="7ab9d-121">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span>

* <span data-ttu-id="7ab9d-122">**App 项目**：包括与 bot 相关的应用程序清单和基架</span><span class="sxs-lookup"><span data-stu-id="7ab9d-122">**App project**: Includes the app manifest and scaffolding relevant to bots</span></span>
* <span data-ttu-id="7ab9d-123">**Bot**：配置新的 Bot 并使用 Microsoft Azure Bot 服务注册它</span><span class="sxs-lookup"><span data-stu-id="7ab9d-123">**Bot**: Configures a new bot and registers it with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="7ab9d-124">如果之前尚未创建团队应用程序项目，您可能会发现，请按照 [以下说明](../build-your-first-app/build-and-run.md) 更详细地说明项目。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-124">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队**"， :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: 然后选择 " **创建新的团队应用**"。
1. <span data-ttu-id="7ab9d-126">为你的团队应用输入名称。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-126">Enter a name for your Teams app.</span></span> <span data-ttu-id="7ab9d-127"> (这是您的应用程序的默认名称，也是本地计算机上的应用程序项目目录的名称。 ) </span><span class="sxs-lookup"><span data-stu-id="7ab9d-127">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="7ab9d-128">在 " **添加功能** " 屏幕上，依次选择 **Bot** 和 " **下一步**"。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-128">On the **Add capabilities** screen, select **Bot** then **Next**.</span></span>
1. <span data-ttu-id="7ab9d-129">选择 " **创建新的 Bot** 并 **登录** " 以使用 Microsoft 365 开发帐户登录。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-129">Select **Create a new Bot** and **Login** to sign in with your Microsoft 365 development account.</span></span><br/>
:::image type="content" source="../doc-links/images/vsc-create-bot.png" alt-text="该图显示了如何在团队工具包中登录到 Microsoft 365 帐户以创建新的 bot。":::
1. <span data-ttu-id="7ab9d-131"> (可选) 输入你的 bot 的自定义名称，然后选择 " **创建**"。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-131">(Optional) Enter a custom name for your bot and select **Create**.</span></span> <span data-ttu-id="7ab9d-132"> (记住，这是你的 bot 的名称，而不是你已指定的团队应用程序的名称。 ) </span><span class="sxs-lookup"><span data-stu-id="7ab9d-132">(Remember, this is the name for your bot and not the name of the Teams app you already specified.)</span></span>
1. <span data-ttu-id="7ab9d-133">选择屏幕底部的 " **完成** " 以配置项目。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-133">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="identify-relevant-app-project-components"></a><span data-ttu-id="7ab9d-134">确定相关的应用程序项目组件</span><span class="sxs-lookup"><span data-stu-id="7ab9d-134">Identify relevant app project components</span></span>

<span data-ttu-id="7ab9d-135">大多数应用程序清单和基架是在使用团队工具包创建项目时自动设置的。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-135">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="7ab9d-136">我们来看看构建机器人的主要组件。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-136">Let's look at the main components for building a bot.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="7ab9d-137">应用程序清单</span><span class="sxs-lookup"><span data-stu-id="7ab9d-137">App manifest</span></span>

<span data-ttu-id="7ab9d-138">应用程序清单中的以下代码片段 (`manifest.json` 项目目录中的文件 `.publish`) 显示与 bot 相关的属性和默认值。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-138">The following snippet from the app manifest (the `manifest.json` file in your project's `.publish` directory) shows the properties and default values relevant to bots.</span></span>

```JSON
    "bots": [
        {
            "botId": "{botId0}",
            "scopes": [
                "personal",
                "groupchat",
                "team"
            ],
            "supportsFiles": false,
            "isNotificationOnly": false,
            "commandLists": [
                {
                    "scopes": [
                        "personal",
                        "groupchat",
                        "team"
                    ],
                    "commands": [
                        {
                            "title": "Hello",
                            "description": "Sends a hello message and @mention the sender"
                        }
                    ]
                }
            ]
        }
    ],
```

<span data-ttu-id="7ab9d-139">现在，让我们将重点放在以下必需属性上。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-139">For now, let's just focus on the following required properties.</span></span> <span data-ttu-id="7ab9d-140"> (查看受支持属性的完整列表 [`bots`](../../resources/schema/manifest-schema.md#bots) 。 ) </span><span class="sxs-lookup"><span data-stu-id="7ab9d-140">(See the full list of supported [`bots`](../../resources/schema/manifest-schema.md#bots) properties.)</span></span>

* <span data-ttu-id="7ab9d-141">`botId`：你创建的你的项目设置的 bot 的 ID。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-141">`botId`: The ID of the bot you created setting up your project.</span></span> <span data-ttu-id="7ab9d-142"> (存储在中 `{botId0}` ，则可以在中查找实际的 ID `Development.env` 。 ) </span><span class="sxs-lookup"><span data-stu-id="7ab9d-142">(Stored in `{botId0}`, you can find the actual ID in `Development.env`.)</span></span>
* <span data-ttu-id="7ab9d-143">`scopes`：指定你的 bot 在 `personal` 、 `groupchat` 或 `team` (（即通道) 上下文中是否可用。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-143">`scopes`: Specifies if your bot is available in `personal`, `groupchat`, or `team` (i.e., channel) contexts.</span></span>
* <span data-ttu-id="7ab9d-144">`commands`：用户可以发送到你的 bot 的可用命令。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-144">`commands`: Available commands users can send to your bot.</span></span>
* <span data-ttu-id="7ab9d-145">`title`：用户在团队客户端中看到的 bot 命令名称。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-145">`title`: A bot command name users see in the Teams client.</span></span>
* <span data-ttu-id="7ab9d-146">`description`：用于帮助用户了解 bot 命令执行的操作的语法和参数的简短说明或示例。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-146">`description`: A short description or example of the syntax and arguments to help users understand what a bot command does.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="7ab9d-147">应用程序基架</span><span class="sxs-lookup"><span data-stu-id="7ab9d-147">App scaffolding</span></span>

<span data-ttu-id="7ab9d-148">应用程序基架提供一个 `botActivityHandler.js` 文件，该文件位于项目的根目录中，用于处理你的 bot 如何处理团队中的活动 (例如，bot 如何对特定邮件（如 "Hello" ) ）进行响应。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-148">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your bot processes activities in Teams (for example, how the bot responds to specific messages such as "Hello").</span></span>

## <a name="set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="7ab9d-149">设置到您的应用程序的安全隧道</span><span class="sxs-lookup"><span data-stu-id="7ab9d-149">Set up a secure tunnel to your app</span></span>

<span data-ttu-id="7ab9d-150">出于测试目的，让你将你的 bot 托管在本地 web 服务器上 (端口 3978) 。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-150">For testing purposes, let's host your bot on a local web server (port 3978).</span></span>

1. <span data-ttu-id="7ab9d-151">在终端中，运行 `ngrok http -host-header=rewrite 3978` 。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-151">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="7ab9d-152">在输出中复制 HTTPS URL，因为团队需要 HTTPS 连接。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-152">Copy the HTTPS URL in the output since Teams requires HTTPS connections.</span></span>
1. <span data-ttu-id="7ab9d-153">在 `.publish` 目录中，打开 `Development.env` 。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-153">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="7ab9d-154">将 `baseUrl0` 值替换为复制的 URL。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-154">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="7ab9d-155"> (例如，改 `baseUrl0=http://localhost:3000` 为 `baseUrl0=https://85528b2b3ca5.ngrok.io` 。 ) </span><span class="sxs-lookup"><span data-stu-id="7ab9d-155">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ca5.ngrok.io`.)</span></span>

<span data-ttu-id="7ab9d-156">你的应用程序清单指向你承载机器人的位置。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-156">Your app manifest is pointing to where you're hosting the bot.</span></span>

## <a name="configuring-your-bot"></a><span data-ttu-id="7ab9d-157">配置你的 bot</span><span class="sxs-lookup"><span data-stu-id="7ab9d-157">Configuring your bot</span></span>

<span data-ttu-id="7ab9d-158">若要在团队中使用 bot，必须将其注册到 Azure Bot 服务。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-158">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="7ab9d-159">幸运的是，当您使用团队工具包设置应用程序时，将自动完成此操作。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-159">Lucky for you, this is done automatically when you set up your app using the Teams Toolkit.</span></span>

### <a name="add-the-bot-endpoint-address"></a><span data-ttu-id="7ab9d-160">添加 bot 终结点地址</span><span class="sxs-lookup"><span data-stu-id="7ab9d-160">Add the bot endpoint address</span></span>

<span data-ttu-id="7ab9d-161">您必须指定接收和处理用户邮件的终结点 URL (例如，发送到 bot 的请求) 。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-161">You must specify an endpoint URL to receive and process user messages (i.e., requests) sent to the bot.</span></span> <span data-ttu-id="7ab9d-162">通常，URL 如下所示 `https://HOST_URL/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-162">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="7ab9d-163">您可以在团队工具包中快速配置此设置。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-163">You can configure this quickly in the Teams Toolkit.</span></span>

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队**"， :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: 然后选择 " **打开 Microsoft 团队工具包**"。
1. <span data-ttu-id="7ab9d-165">转到 **Bot 管理 > 现有的 bot 注册** ，并选择在安装过程中创建的 bot。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-165">Go to **Bot management > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="7ab9d-166">在 " **机器人终结点地址** " 字段中，输入承载机器人的本地 web 服务器，并 `/api/messages` 向其追加。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-166">In the **Bot endpoint address** field, enter the local web server where you're hosting the bot and append `/api/messages` to it.</span></span>

    :::image type="content" source="../doc-links/images/bot-config-endpoint-url.png" alt-text="图中显示可在团队工具包中配置 bot 终结点 URL 的位置。":::

<span data-ttu-id="7ab9d-168">你的 bot 将能够响应团队中的邮件。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-168">Your bot will be able to respond to messages in Teams.</span></span>

## <a name="run-your-app"></a><span data-ttu-id="7ab9d-169">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="7ab9d-169">Run your app</span></span>

<span data-ttu-id="7ab9d-170">您已经设置了承载你的 bot 并将其配置为处理邮件的 URL。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-170">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="7ab9d-171">现在是将你的 bot 准备好并运行了。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-171">It's time to get your bot up and running.</span></span>

1. <span data-ttu-id="7ab9d-172">在终端中，转到您的应用程序项目的根目录并运行该目录 `npm install` 。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-172">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="7ab9d-173">运行 `npm start` 。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-173">Run `npm start`.</span></span>

<span data-ttu-id="7ab9d-174">如果成功，你会看到类似如下的消息，指示你的 bot 正在侦听你的活动 `localhost` ：</span><span class="sxs-lookup"><span data-stu-id="7ab9d-174">If successful, you see something like the following message indicating your bot is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="sideload-your-bot-in-teams"></a><span data-ttu-id="7ab9d-175">在团队中旁加载你的机器人</span><span class="sxs-lookup"><span data-stu-id="7ab9d-175">Sideload your bot in Teams</span></span>

<span data-ttu-id="7ab9d-176">在运行机器人的情况下，可以将其安装在团队中。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-176">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="7ab9d-177">如果您在之前未旁加载团队应用程序并遇到问题，请按照这些 [说明](../build-your-first-app/build-and-run.md#sideload-your-app-in-teams)进行操作。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-177">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="7ab9d-178">使用允许应用旁加载的帐户登录到团队客户端。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-178">Log in to the Teams client with your account that allows app sideloading.</span></span>
1. <span data-ttu-id="7ab9d-179">选择 " **应用**"，然后选择 " **上载自定义应用**"。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-179">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="7ab9d-180">转到您的应用程序项目 `.publish` 文件夹，然后选择 `Development.zip` 。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-180">Go to your app project `.publish` folder and select `Development.zip`.</span></span>
1. <span data-ttu-id="7ab9d-181">在 "安装模式" 中，选择 " **添加** " 以安装您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-181">In the install modal, select **Add** to install your app.</span></span>

## <a name="test-your-bot"></a><span data-ttu-id="7ab9d-182">测试你的 bot</span><span class="sxs-lookup"><span data-stu-id="7ab9d-182">Test your bot</span></span>

<span data-ttu-id="7ab9d-183">现在，为有趣部分：让我们在一对一聊天中说出 "Hello" 到你的机器人。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-183">Now for the fun part: Let's say "Hello" to your bot in a one-on-one chat.</span></span>

1. 在团队中，选择左侧的 " **更多**" :::image type="icon" source="../doc-links/images/teams-client-more.png"::: 。
1. <span data-ttu-id="7ab9d-185">找到并选择您刚刚旁加载的 bot。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-185">Locate and select the bot you just sideloaded.</span></span><br/>
   :::image type="content" source="../doc-links/images/bot-teams-access.png" alt-text="图示显示在团队中访问机器人的位置。":::
1. <span data-ttu-id="7ab9d-187">在 "撰写" 框中，发送一 `Hello` 封邮件。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-187">In the compose box, send a `Hello` message.</span></span>

<span data-ttu-id="7ab9d-188">你的 bot 将回复如下邮件等内容。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-188">Your bot replies with something like the following message.</span></span>

:::image type="content" source="../doc-links/images/contoso-chatbot.png" alt-text="显示用户将 "Hello" 发送到团队 bot 并获取响应的屏幕截图。":::

> [!NOTE]
> <span data-ttu-id="7ab9d-190">如果在测试你的 bot 后进行代码更改（例如，更新），则 `botActivityHandler.js` 必须再次运行应用以查看团队中反映的更改。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-190">If you make code changes after testing your bot—for example, you update `botActivityHandler.js`—you must run your app again to see those changes reflected in Teams.</span></span>

## <a name="well-done"></a><span data-ttu-id="7ab9d-191">干的好</span><span class="sxs-lookup"><span data-stu-id="7ab9d-191">Well done</span></span>

<span data-ttu-id="7ab9d-192">恭喜你！</span><span class="sxs-lookup"><span data-stu-id="7ab9d-192">Congratulations!</span></span> <span data-ttu-id="7ab9d-193">您有一个基本的团队 bot，可以与用户一次或在组设置 (频道和聊天) 通信。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-193">You have a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7ab9d-194">故障排除</span><span class="sxs-lookup"><span data-stu-id="7ab9d-194">Troubleshooting</span></span>

<span data-ttu-id="7ab9d-195">如果你在完成本教程时遇到问题，以下信息可能会有所帮助。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-195">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="toolkit-setup-fails"></a><span data-ttu-id="7ab9d-196">工具包安装程序失败</span><span class="sxs-lookup"><span data-stu-id="7ab9d-196">Toolkit setup fails</span></span>

<span data-ttu-id="7ab9d-197">使用 "团队" 工具包设置应用程序项目时，在选择 " **创建新的 Bot** " 选项并使用 Microsoft 365 开发帐户登录后，将会收到错误消息。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-197">While setting up your app project with the Teams Toolkit, you get an error after selecting the **Create a new Bot** option and logging in with your Microsoft 365 development account.</span></span>

<span data-ttu-id="7ab9d-198">这可能是身份验证问题。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-198">This could be an authentication issue.</span></span> <span data-ttu-id="7ab9d-199">按照以下步骤完成对项目的设置。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-199">Follow these steps to finish setting up your project.</span></span>

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队**"， :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: 然后选择 " **注销**"。
1. <span data-ttu-id="7ab9d-201">通过使用相同帐户登录并创建新的 bot，再次执行安装过程。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-201">Go through the setup process again by logging in with the same account and creating a new bot.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="7ab9d-202">机器人未连接到团队</span><span class="sxs-lookup"><span data-stu-id="7ab9d-202">Bot isn't connected to Teams</span></span>

<span data-ttu-id="7ab9d-203">如果您安装了应用程序，但机器人无法正常运行，请确保将 bot [连接到 Azure Bot 服务的团队 *频道*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-203">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="7ab9d-204">请务必了解，这与团队中的频道不相同。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-204">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="7ab9d-205">在这种情况下，通道是 Azure Bot 服务将你的 Bot 连接到团队或其他 [受支持的 Microsoft 或第三方通信应用程序](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)的方式。</span><span class="sxs-lookup"><span data-stu-id="7ab9d-205">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="7ab9d-206">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="7ab9d-206">Learn more</span></span>

* [<span data-ttu-id="7ab9d-207">请参阅其他团队 bot 可以使用 (GitHub 中的一个示例) </span><span class="sxs-lookup"><span data-stu-id="7ab9d-207">See what else Teams bots can do with one of our samples (GitHub)</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="7ab9d-208">自动程序对话基础知识</span><span class="sxs-lookup"><span data-stu-id="7ab9d-208">Bot conversation basics</span></span>](../../bots/how-to/conversations/conversation-basics.md)
* [<span data-ttu-id="7ab9d-209">团队中的 Bot 身份验证</span><span class="sxs-lookup"><span data-stu-id="7ab9d-209">Bot authentication in Teams</span></span>](../../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="7ab9d-210">Microsoft Bot 框架</span><span class="sxs-lookup"><span data-stu-id="7ab9d-210">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
