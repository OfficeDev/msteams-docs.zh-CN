---
title: 在本地测试和调试你的 bot
author: clearab
description: 通过 IDE 在本地测试和调试你的 bot
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 8494302b41e33910cb33f8c6889d82505b703577
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673129"
---
# <a name="test-and-debug-your-bot-locally"></a><span data-ttu-id="20eba-103">在本地测试和调试你的 bot</span><span class="sxs-lookup"><span data-stu-id="20eba-103">Test and debug your bot locally</span></span>

<span data-ttu-id="20eba-104">测试你的 bot 时，需要考虑要在其上运行你的 bot 的上下文，以及你可能已添加到你的 bot 中的、需要 Microsoft 团队专用数据的任何功能。</span><span class="sxs-lookup"><span data-stu-id="20eba-104">When testing your bot you need to take into consideration both the context(s) you want your bot to run in, as well as any functionality you may have added to your bot that requires data specific to Microsoft Teams.</span></span> <span data-ttu-id="20eba-105">请确保你选择的用于测试你的 bot 的方法与其功能保持一致。</span><span class="sxs-lookup"><span data-stu-id="20eba-105">Make sure that the method you chose to test your bot aligns with its functionality.</span></span>

## <a name="test-by-uploading-to-teams"></a><span data-ttu-id="20eba-106">通过上传到团队进行测试</span><span class="sxs-lookup"><span data-stu-id="20eba-106">Test by uploading to Teams</span></span>

<span data-ttu-id="20eba-107">若要测试你的 bot，最全面的方法是创建一个应用包并将其上传到团队。</span><span class="sxs-lookup"><span data-stu-id="20eba-107">The most comprehensive way to test your bot is by creating an app package and uploading it to Teams.</span></span> <span data-ttu-id="20eba-108">这是在所有作用域中测试自动程序可用的完整功能的唯一方法。</span><span class="sxs-lookup"><span data-stu-id="20eba-108">This is the only method to test the full functionality available to your bot, across all scopes.</span></span>

<span data-ttu-id="20eba-109">有两种方法可用于上载应用程序。</span><span class="sxs-lookup"><span data-stu-id="20eba-109">There are two methods for uploading your app.</span></span> <span data-ttu-id="20eba-110">您可以使用[应用程序 Studio](~/concepts/build-and-test/app-studio-overview.md)来帮助您，也可以手动[创建应用程序包](~/concepts/build-and-test/apps-package.md)并[上传应用程序](~/concepts/deploy-and-publish/apps-upload.md)。</span><span class="sxs-lookup"><span data-stu-id="20eba-110">You can either use [App Studio](~/concepts/build-and-test/app-studio-overview.md) to help you, or you can manually [create an app package](~/concepts/build-and-test/apps-package.md) and [upload your app](~/concepts/deploy-and-publish/apps-upload.md).</span></span> <span data-ttu-id="20eba-111">如果需要更改清单并重新上载您的应用程序，则应在上载更改的应用程序包之前[删除你的 bot](#deleting-a-bot-from-teams) 。</span><span class="sxs-lookup"><span data-stu-id="20eba-111">If you need to alter your manifest and re-upload your app, you should [delete your bot](#deleting-a-bot-from-teams) before uploading your altered app package.</span></span>

## <a name="debug-your-bot-locally"></a><span data-ttu-id="20eba-112">在本地调试你的 bot</span><span class="sxs-lookup"><span data-stu-id="20eba-112">Debug your bot locally</span></span>

<span data-ttu-id="20eba-113">如果你在开发过程中将你的 bot 托管在本地，则需要使用隧道服务（如[ngrok](https://ngrok.com/) ）来测试你的 bot。</span><span class="sxs-lookup"><span data-stu-id="20eba-113">If you are hosting your bot locally during development you'll need to use a tunneling service like [ngrok](https://ngrok.com/) in order to test your bot.</span></span> <span data-ttu-id="20eba-114">下载并安装 ngrok 后，运行以下命令以启动隧道服务（您可能需要向路径中添加 ngrok）。</span><span class="sxs-lookup"><span data-stu-id="20eba-114">Once you've downloaded and installed ngrok, run the below command to start the tunneling service (you may need to add ngrok to your path).</span></span>

```bash
ngrok http <port> -host-header=localhost:<port>
```

<span data-ttu-id="20eba-115">在应用程序清单中使用 ngrok 提供的 https 终结点。</span><span class="sxs-lookup"><span data-stu-id="20eba-115">Use the https endpoint provided by ngrok in your app manifest.</span></span> <span data-ttu-id="20eba-116">如果关闭命令窗口并重新启动，则会收到一个新的 URL，您需要将你的 bot 终结点地址更新为同时使用该地址。</span><span class="sxs-lookup"><span data-stu-id="20eba-116">If you close your command window and restart you'll get a new URL, and you'll need to update your bot endpoint address to use that one as well.</span></span>

## <a name="testing-your-bot-without-uploading-to-teams"></a><span data-ttu-id="20eba-117">在不上载到团队的情况下测试你的机器人</span><span class="sxs-lookup"><span data-stu-id="20eba-117">Testing your bot without uploading to Teams</span></span>

<span data-ttu-id="20eba-118">有时，您可能需要测试您的 bot，而无需将其作为团队中的应用程序进行安装。</span><span class="sxs-lookup"><span data-stu-id="20eba-118">Occasionally it may be necessary to test your bot without installing it as an app in Teams.</span></span> <span data-ttu-id="20eba-119">我们提供了两种方法来实现此目的。</span><span class="sxs-lookup"><span data-stu-id="20eba-119">We provide two methods for doing so below.</span></span> <span data-ttu-id="20eba-120">测试您的 bot 而不将其安装为应用程序可确保你的 bot 可用并做出响应，但不允许你测试你可能已添加到你的 bot 的 Microsoft 团队功能的全部广度。</span><span class="sxs-lookup"><span data-stu-id="20eba-120">Testing your bot without installing it as an app can be useful to ensure your bot is available and responding, however it will not allow you to test the full breadth of Microsoft Teams functionality you may have added to your bot.</span></span> <span data-ttu-id="20eba-121">如果需要完全测试你的 bot，请按照[上传](#test-by-uploading-to-teams)说明进行测试。</span><span class="sxs-lookup"><span data-stu-id="20eba-121">If you need to fully test your bot, please follow the instructions for [testing by uploading](#test-by-uploading-to-teams).</span></span>

### <a name="use-the-bot-emulator"></a><span data-ttu-id="20eba-122">使用机器人仿真程序</span><span class="sxs-lookup"><span data-stu-id="20eba-122">Use the Bot Emulator</span></span>

<span data-ttu-id="20eba-123">Bot 框架仿真程序是一种桌面应用程序，它允许 Bot 开发人员在本地或远程测试和调试自己的 bot。</span><span class="sxs-lookup"><span data-stu-id="20eba-123">The Bot Framework Emulator is a desktop application that allows bot developers to test and debug their bots, either locally or remotely.</span></span> <span data-ttu-id="20eba-124">使用模拟器，可以与你的 bot 聊天并检查你的 bot 发送和接收的邮件。</span><span class="sxs-lookup"><span data-stu-id="20eba-124">Using the emulator, you can chat with your bot and inspect the messages that your bot sends and receives.</span></span> <span data-ttu-id="20eba-125">这在验证你的 bot 是否可用并做出响应时非常有用，但是仿真程序不允许你测试你已添加到机器人的任何团队特定的功能，也不会从你的 bot 中的响应准确直观地表示它们将如何在团队中呈现。</span><span class="sxs-lookup"><span data-stu-id="20eba-125">This can be useful for verifying that your bot is available and responding, however the emulator will not allow you to test any Teams-specific functionality you've added to your bot, nor will responses from your bot be an accurate visual representation of how they will be rendered in Teams.</span></span> <span data-ttu-id="20eba-126">如果你需要测试这些内容中的任何一个，最好[上载你的机器人](#test-by-uploading-to-teams)。</span><span class="sxs-lookup"><span data-stu-id="20eba-126">If you need to test either of those things it is best to [upload your bot](#test-by-uploading-to-teams).</span></span>

<span data-ttu-id="20eba-127">可以在[此处](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0)找到机器人框架仿真程序的完整说明。</span><span class="sxs-lookup"><span data-stu-id="20eba-127">Complete instructions on the Bot Framework Emulator can be found [here](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0).</span></span>

### <a name="talk-to-your-bot-directly-by-id"></a><span data-ttu-id="20eba-128">按 Id 直接联系你的 bot</span><span class="sxs-lookup"><span data-stu-id="20eba-128">Talk to your bot directly by Id</span></span>

>[!Important]
><span data-ttu-id="20eba-129">按 Id 与你的 bot 对话仅适用于基本测试目的。</span><span class="sxs-lookup"><span data-stu-id="20eba-129">Talking to your bot by Id is intended for basic testing purposes only.</span></span> <span data-ttu-id="20eba-130">你添加到你的 bot 的任何团队特定的功能将无法工作。</span><span class="sxs-lookup"><span data-stu-id="20eba-130">Any Teams-specific functionality you've added to your bot will not work.</span></span>

<span data-ttu-id="20eba-131">此外，还可以使用你的 bot 启动与你的 bot 的对话，方法是使用其 Id。下面给出了两种执行此操作的方法。</span><span class="sxs-lookup"><span data-stu-id="20eba-131">You can also initiate a conversation with your bot by using its Id. Two methods for doing so are given below.</span></span> <span data-ttu-id="20eba-132">通过其中一种方法添加机器人时，它不会在通道对话中可寻址，也不能利用其他 Microsoft 团队应用功能（如选项卡或邮件扩展）。</span><span class="sxs-lookup"><span data-stu-id="20eba-132">When a bot has been added through one of these methods it will not be addressable in channel conversations, and you cannot take advantage of other Microsoft Teams app capabilities like tabs or messaging extensions.</span></span>

1. <span data-ttu-id="20eba-133">在你的 bot 的 "[机器人仪表板](https://dev.botframework.com/bots)" 页面上的 "**频道**" 下，选择 "**添加到 Microsoft 团队**"。</span><span class="sxs-lookup"><span data-stu-id="20eba-133">On the [Bot Dashboard](https://dev.botframework.com/bots) page for your bot, under **Channels**, select **Add to Microsoft Teams**.</span></span> <span data-ttu-id="20eba-134">Microsoft 团队将启动与你的 bot 的个人聊天。</span><span class="sxs-lookup"><span data-stu-id="20eba-134">Microsoft Teams will launch with a personal chat with your bot.</span></span>
2. <span data-ttu-id="20eba-135">直接从 Microsoft 团队中引用你的 bot 的应用 ID：</span><span class="sxs-lookup"><span data-stu-id="20eba-135">Directly reference your bot's app ID from within Microsoft Teams:</span></span>
   * <span data-ttu-id="20eba-136">在你的 bot 的 " [Bot 仪表板](https://dev.botframework.com/bots)" 页面上，在 "**详细信息**" 下，复制你的 BOT 的**Microsoft 应用 ID** 。</span><span class="sxs-lookup"><span data-stu-id="20eba-136">On the [Bot Dashboard](https://dev.botframework.com/bots) page for your bot, under **Details**, copy the **Microsoft App ID** for your bot.</span></span>
  
     ![获取 bot 的 AppID](~/assets/images/bots_appid_botframework.png)
  
   * <span data-ttu-id="20eba-138">在 Microsoft 团队中，在**聊天**窗格中，选择 "**添加聊天**" 图标。</span><span class="sxs-lookup"><span data-stu-id="20eba-138">From within Microsoft Teams, on the **Chat** pane, select the **Add chat** icon.</span></span> <span data-ttu-id="20eba-139">对于 **：**，请粘贴你的 Bot 的 MICROSOFT 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="20eba-139">For **To:**, paste your bot's Microsoft App ID.</span></span>
  
     ![获取 bot 的 AppID](~/assets/images/bots_uploading.png)

     <span data-ttu-id="20eba-141">应用 ID 应解析为你的 bot 名称。</span><span class="sxs-lookup"><span data-stu-id="20eba-141">The app ID should resolve to your bot name.</span></span>

   * <span data-ttu-id="20eba-142">选择你的 bot 并发送一封邮件以启动对话。</span><span class="sxs-lookup"><span data-stu-id="20eba-142">Select your bot and send a message to initiate a conversation.</span></span>
   * <span data-ttu-id="20eba-143">或者，可以将你的 bot 的应用 ID 粘贴到 Microsoft 团队中左上角的搜索框中。</span><span class="sxs-lookup"><span data-stu-id="20eba-143">Alternatively, you can paste your bot's app ID in the search box in the top left in Microsoft Teams.</span></span> <span data-ttu-id="20eba-144">在 "搜索结果" 页上，导航到 "人员" 选项卡以查看你的 bot 并开始与之聊天。</span><span class="sxs-lookup"><span data-stu-id="20eba-144">In the search results page, navigate to the People tab to see your bot and to start chatting with it.</span></span>

<span data-ttu-id="20eba-145">你的 bot 将接收`conversationUpdate`事件，就像添加到团队中的 bot 一样，但没有`channelData`对象中的团队信息。</span><span class="sxs-lookup"><span data-stu-id="20eba-145">Your bot will receive the `conversationUpdate` event just like bots added to a team, but without the team information in the `channelData` object.</span></span>

## <a name="blocking-a-bot-in-personal-chat"></a><span data-ttu-id="20eba-146">阻止个人聊天中的 bot</span><span class="sxs-lookup"><span data-stu-id="20eba-146">Blocking a bot in personal chat</span></span>

<span data-ttu-id="20eba-147">请注意，用户可以选择阻止你的 bot 发送个人聊天消息。</span><span class="sxs-lookup"><span data-stu-id="20eba-147">Note that users can choose to block your bot from sending personal chat messages.</span></span> <span data-ttu-id="20eba-148">他们可以通过右键单击聊天频道中的 bot 并选择 "**阻止机器人对话**" 来切换此功能。</span><span class="sxs-lookup"><span data-stu-id="20eba-148">They may toggle this by right-clicking your bot in the chat channel and choosing **Block bot conversation**.</span></span> <span data-ttu-id="20eba-149">这意味着你的 bot 将继续发送邮件，但用户将不会收到这些邮件。</span><span class="sxs-lookup"><span data-stu-id="20eba-149">This means your bots will continue to send messages but the user will not receive those messages.</span></span>

![阻止 bot](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a><span data-ttu-id="20eba-151">从团队中删除机器人</span><span class="sxs-lookup"><span data-stu-id="20eba-151">Removing a bot from a team</span></span>

<span data-ttu-id="20eba-152">用户可以通过在其 "团队" 视图中的 "bot" 列表中选择垃圾桶图标来删除机器人。</span><span class="sxs-lookup"><span data-stu-id="20eba-152">Users can delete the bot by choosing the trash-can icon on the bots list in their teams view.</span></span> <span data-ttu-id="20eba-153">请注意，这只会从该团队使用中删除机器人;单个用户将仍能够在个人上下文中进行交互。</span><span class="sxs-lookup"><span data-stu-id="20eba-153">Note that this only removes the bot from that team's use; individual users will still be able to interact in personal context.</span></span>

<span data-ttu-id="20eba-154">个人上下文中的 bot 不能被用户禁用或删除，而是从团队完全删除机器人的短时间。</span><span class="sxs-lookup"><span data-stu-id="20eba-154">Bots in personal context cannot be disabled or removed by a user, short of completely removing the bot from Teams.</span></span>

## <a name="disabling-a-bot-in-teams"></a><span data-ttu-id="20eba-155">在团队中禁用机器人</span><span class="sxs-lookup"><span data-stu-id="20eba-155">Disabling a bot in Teams</span></span>

<span data-ttu-id="20eba-156">若要停止你的 bot 接收邮件，请转到你的机器人仪表板并编辑 Microsoft 团队频道。</span><span class="sxs-lookup"><span data-stu-id="20eba-156">To stop your bot receiving messages, go to your Bot Dashboard and edit the Microsoft Teams channel.</span></span> <span data-ttu-id="20eba-157">清除 "**在 Microsoft 团队中启用**" 选项。</span><span class="sxs-lookup"><span data-stu-id="20eba-157">Clear the **Enable on Microsoft Teams** option.</span></span> <span data-ttu-id="20eba-158">这样可以防止用户与 bot 交互，但仍然可以发现，用户仍可以将其添加到团队。</span><span class="sxs-lookup"><span data-stu-id="20eba-158">This prevents users from interacting with the bot, but it will still be discoverable and users will still be able to add it to teams.</span></span>

## <a name="deleting-a-bot-from-teams"></a><span data-ttu-id="20eba-159">从团队中删除机器人</span><span class="sxs-lookup"><span data-stu-id="20eba-159">Deleting a bot from Teams</span></span>

<span data-ttu-id="20eba-160">若要从团队中完全删除你的 bot，请转到你的机器人仪表板并编辑 Microsoft 团队频道。</span><span class="sxs-lookup"><span data-stu-id="20eba-160">To remove your bot completely from Teams, go to your Bot Dashboard and edit the Microsoft Teams channel.</span></span> <span data-ttu-id="20eba-161">选择底部的 "**删除**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="20eba-161">Choose the **Delete** button at the bottom.</span></span> <span data-ttu-id="20eba-162">这样可以防止用户发现、添加或与你的 bot 进行交互。</span><span class="sxs-lookup"><span data-stu-id="20eba-162">This prevents users from discovering, adding, or interacting with your bot.</span></span> <span data-ttu-id="20eba-163">请注意，这不会从其他用户的团队实例中删除机器人，尽管它也会停止运行。</span><span class="sxs-lookup"><span data-stu-id="20eba-163">Note that this does not remove the bot from other users' Teams instances, although it will cease functioning for them as well.</span></span>
