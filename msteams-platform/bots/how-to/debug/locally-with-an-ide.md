---
title: 在本地测试和调试机器人
author: clearab
description: 使用 IDE 在本地测试和调试机器人
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 495e4dd2a3f29dbe0be61e8b42827bfc8c8a6f94
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020019"
---
# <a name="test-and-debug-your-bot-locally"></a><span data-ttu-id="693d5-103">在本地测试和调试机器人</span><span class="sxs-lookup"><span data-stu-id="693d5-103">Test and debug your bot locally</span></span>

<span data-ttu-id="693d5-104">测试自动程序时，需要考虑希望自动程序运行的环境，以及可能添加到自动程序（需要特定于 Microsoft Teams 的数据）的任何功能。</span><span class="sxs-lookup"><span data-stu-id="693d5-104">When testing your bot you need to take into consideration both the contexts you want your bot to run in, and any functionality you may have added to your bot that requires data specific to Microsoft Teams.</span></span> <span data-ttu-id="693d5-105">确保你选择用于测试机器人的方法与它的功能一致。</span><span class="sxs-lookup"><span data-stu-id="693d5-105">Make sure that the method you choose to test your bot aligns with its functionality.</span></span>

## <a name="test-by-uploading-to-teams"></a><span data-ttu-id="693d5-106">通过上传到 Teams 进行测试</span><span class="sxs-lookup"><span data-stu-id="693d5-106">Test by uploading to Teams</span></span>

<span data-ttu-id="693d5-107">测试自动程序的最全面方法就是创建应用包并将其上传到 Teams。</span><span class="sxs-lookup"><span data-stu-id="693d5-107">The most comprehensive way to test your bot is by creating an app package and uploading it to Teams.</span></span> <span data-ttu-id="693d5-108">这是在所有范围内测试自动程序可用的完整功能的唯一方法。</span><span class="sxs-lookup"><span data-stu-id="693d5-108">This is the only method to test the full functionality available to your bot, across all scopes.</span></span>

<span data-ttu-id="693d5-109">有两种上传应用的方法：</span><span class="sxs-lookup"><span data-stu-id="693d5-109">There are two methods for uploading your app:</span></span>
* <span data-ttu-id="693d5-110">使用 [App Studio](~/concepts/build-and-test/app-studio-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="693d5-110">Use [App Studio](~/concepts/build-and-test/app-studio-overview.md).</span></span>
* <span data-ttu-id="693d5-111">[手动创建应用](~/concepts/build-and-test/apps-package.md) 包，然后 [上传应用](~/concepts/deploy-and-publish/apps-upload.md)。</span><span class="sxs-lookup"><span data-stu-id="693d5-111">[Create an app package](~/concepts/build-and-test/apps-package.md) manually, and then [upload your app](~/concepts/deploy-and-publish/apps-upload.md).</span></span>

> [!NOTE]
> <span data-ttu-id="693d5-112">如果你需要更改清单并重新上传应用，则必须在上传已更改的应用包之前删除[](#delete-a-bot-from-teams)自动程序。</span><span class="sxs-lookup"><span data-stu-id="693d5-112">If you need to alter your manifest and re-upload your app, you must [delete your bot](#delete-a-bot-from-teams) before uploading your altered app package.</span></span>

## <a name="debug-your-bot-locally"></a><span data-ttu-id="693d5-113">在本地调试机器人</span><span class="sxs-lookup"><span data-stu-id="693d5-113">Debug your bot locally</span></span>

<span data-ttu-id="693d5-114">如果你在开发期间在本地托管机器人，则需要使用 [类似 ngrok](https://ngrok.com/) 的隧道服务来测试机器人。</span><span class="sxs-lookup"><span data-stu-id="693d5-114">If you are hosting your bot locally during development, you need to use a tunneling service like [ngrok](https://ngrok.com/) in order to test your bot.</span></span> <span data-ttu-id="693d5-115">下载并安装 ngrok 后，添加到您的路径，然后运行 `ngrok` 以下命令以启动隧道服务：</span><span class="sxs-lookup"><span data-stu-id="693d5-115">After you download and install ngrok, add `ngrok` to your path, and run the following command to start the tunneling service:</span></span>

```bash
ngrok http <port> -host-header=localhost:<port>
```

<span data-ttu-id="693d5-116">在应用清单中，使用 ngrok 提供的 https 终结点。</span><span class="sxs-lookup"><span data-stu-id="693d5-116">Use the https endpoint provided by ngrok in your app manifest.</span></span> 

> [!NOTE]
> <span data-ttu-id="693d5-117">如果关闭命令窗口并重新启动，将生成一个新 URL，并且你需要更新自动程序终结点地址才能使用它。</span><span class="sxs-lookup"><span data-stu-id="693d5-117">If you close your command window and restart, a new URL is generated and you need to update your bot endpoint address to use it.</span></span>

## <a name="test-your-bot-without-uploading-to-teams"></a><span data-ttu-id="693d5-118">在不上载到 Teams 的情况下测试自动程序</span><span class="sxs-lookup"><span data-stu-id="693d5-118">Test your bot without uploading to Teams</span></span>

<span data-ttu-id="693d5-119">有时，可能需要测试自动程序，而无需将其安装为 Teams 中的应用。</span><span class="sxs-lookup"><span data-stu-id="693d5-119">Occasionally, it may be necessary to test your bot without installing it as an app in Teams.</span></span> <span data-ttu-id="693d5-120">我们提供两种测试自动程序的方法。</span><span class="sxs-lookup"><span data-stu-id="693d5-120">We provide two methods for testing the bot.</span></span> <span data-ttu-id="693d5-121">在未将其安装为应用的情况下测试自动程序对于确保自动程序可用并做出响应非常有用，但是，它不允许测试你可能已添加到自动程序的全部 Microsoft Teams 功能。</span><span class="sxs-lookup"><span data-stu-id="693d5-121">Testing your bot without installing it as an app can be useful to ensure your bot is available and responding, however it won't allow you to test the full breadth of Microsoft Teams functionality you may have added to your bot.</span></span> <span data-ttu-id="693d5-122">如果你需要完全测试自动程序，请参阅 [通过上传 进行测试](#test-by-uploading-to-teams)。</span><span class="sxs-lookup"><span data-stu-id="693d5-122">If you need to fully test your bot, see [testing by uploading](#test-by-uploading-to-teams).</span></span>

### <a name="use-the-bot-emulator"></a><span data-ttu-id="693d5-123">使用自动程序仿真器</span><span class="sxs-lookup"><span data-stu-id="693d5-123">Use the Bot Emulator</span></span>

<span data-ttu-id="693d5-124">Bot Framework Emulator 是一个桌面应用程序，允许机器人开发人员在本地或远程测试和调试其机器人。</span><span class="sxs-lookup"><span data-stu-id="693d5-124">The Bot Framework Emulator is a desktop application that permits bot developers to test and debug their bots locally or remotely.</span></span> <span data-ttu-id="693d5-125">仿真器可帮助你与机器人聊天并检查机器人发送和接收的消息。</span><span class="sxs-lookup"><span data-stu-id="693d5-125">The emulator helps you to chat with your bot and inspect the messages that your bot sends and receives.</span></span> <span data-ttu-id="693d5-126">这可用于验证机器人是否可用并做出响应。</span><span class="sxs-lookup"><span data-stu-id="693d5-126">This can be useful for verifying that your bot is available and responding.</span></span> <span data-ttu-id="693d5-127">但是，仿真器不允许你测试已添加到自动程序的任何特定于 Teams 的功能，来自自动程序的响应也不能准确地直观地表示它们在 Teams 中的呈现方式。</span><span class="sxs-lookup"><span data-stu-id="693d5-127">However, the emulator does not permit you to test any Teams-specific functionality you have added to the bot, nor the responses from your bot are an accurate visual representation of how they are rendered in Teams.</span></span> <span data-ttu-id="693d5-128">如果你需要测试其中任一内容，最好上传 [自动程序](#test-by-uploading-to-teams)。</span><span class="sxs-lookup"><span data-stu-id="693d5-128">If you need to test either of those things it is best to [upload your bot](#test-by-uploading-to-teams).</span></span>

<span data-ttu-id="693d5-129">有关详细信息，请参阅 [Bot Framework Emulator 上的完整说明](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="693d5-129">For more information, see [complete instructions on the Bot Framework Emulator](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true).</span></span>

### <a name="talk-to-your-bot-directly-by-id"></a><span data-ttu-id="693d5-130">直接通过 ID 与机器人交谈</span><span class="sxs-lookup"><span data-stu-id="693d5-130">Talk to your bot directly by ID</span></span>

> [!Important]
> <span data-ttu-id="693d5-131">通过 ID 与机器人交谈仅用于基本测试目的。</span><span class="sxs-lookup"><span data-stu-id="693d5-131">Talking to your bot by ID is intended for basic testing purposes only.</span></span> <span data-ttu-id="693d5-132">添加到自动程序的任何特定于 Teams 的功能都无法正常工作。</span><span class="sxs-lookup"><span data-stu-id="693d5-132">Any Teams-specific functionality you have added to your bot fails to work.</span></span>

<span data-ttu-id="693d5-133">您还可以使用自动程序 ID 启动对话。</span><span class="sxs-lookup"><span data-stu-id="693d5-133">You can also initiate a conversation with your bot by using its ID.</span></span> <span data-ttu-id="693d5-134">通过这些方法之一添加自动程序后，将无法在频道对话中解决它，并且你无法利用其他 Microsoft Teams 应用功能，如选项卡或消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="693d5-134">When a bot has been added through one of these methods it is not addressable in channel conversations and you cannot take advantage of other Microsoft Teams app capabilities like tabs or messaging extensions.</span></span> <span data-ttu-id="693d5-135">可以通过以下方法之一启动对话：</span><span class="sxs-lookup"><span data-stu-id="693d5-135">You can initiate a conversation in one of the following ways:</span></span>

* <span data-ttu-id="693d5-136">在机器人 [的"](https://dev.botframework.com/bots)自动程序仪表板"页上的"**频道"下**，选择"**添加到 Microsoft Teams"。**</span><span class="sxs-lookup"><span data-stu-id="693d5-136">On the [Bot Dashboard](https://dev.botframework.com/bots) page for your bot, under **Channels**, select **Add to Microsoft Teams**.</span></span> <span data-ttu-id="693d5-137">Microsoft Teams 启动与机器人的个人聊天。</span><span class="sxs-lookup"><span data-stu-id="693d5-137">Microsoft Teams launches a personal chat with your bot.</span></span>

* <span data-ttu-id="693d5-138">直接从 Microsoft Teams 中引用机器人的应用 ID：</span><span class="sxs-lookup"><span data-stu-id="693d5-138">Directly reference your bot's app ID from within Microsoft Teams:</span></span>
   1. <span data-ttu-id="693d5-139">在 [自动程序"](https://dev.botframework.com/bots)自动程序仪表板"页上的"详细信息 **"** 下，复制自动程序 Microsoft **应用 ID。**</span><span class="sxs-lookup"><span data-stu-id="693d5-139">On the [Bot Dashboard](https://dev.botframework.com/bots) page for your bot, under **Details**, copy the **Microsoft App ID** for your bot.</span></span>
  
      ![获取机器人的 AppID](~/assets/images/bots_appid_botframework.png)
  
   2. <span data-ttu-id="693d5-141">打开 Microsoft Teams，在" **聊天"** 窗格中，选择" **添加聊天"** 图标。</span><span class="sxs-lookup"><span data-stu-id="693d5-141">Open Microsoft Teams, on the **Chat** pane, select the **Add chat** icon.</span></span> <span data-ttu-id="693d5-142">在 **"To："** 中，粘贴机器人的 Microsoft 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="693d5-142">In **To:**, paste your bot's Microsoft App ID.</span></span>
  
      ![上传机器人](~/assets/images/bots_uploading.png)

      <span data-ttu-id="693d5-144">应用 ID 必须解析为自动程序名称。</span><span class="sxs-lookup"><span data-stu-id="693d5-144">The app ID must resolve to your bot name.</span></span>

   3. <span data-ttu-id="693d5-145">选择自动程序并发送消息以启动对话。</span><span class="sxs-lookup"><span data-stu-id="693d5-145">Select your bot and send a message to initiate a conversation.</span></span>
      <span data-ttu-id="693d5-146">或者，你可以将机器人的应用 ID 粘贴到 Microsoft Teams 左上方的搜索框中。</span><span class="sxs-lookup"><span data-stu-id="693d5-146">Alternatively, you can paste your bot's app ID in the search box in the top left in Microsoft Teams.</span></span> <span data-ttu-id="693d5-147">在搜索结果页面中，导航到"人员" **选项卡以查看** 自动程序并开始与它聊天。</span><span class="sxs-lookup"><span data-stu-id="693d5-147">In the search results page, navigate to the **People** tab to see your bot and to start chatting with it.</span></span>

<span data-ttu-id="693d5-148">在将机器人添加到团队时，自动程序将接收事件，而对象 `conversationUpdate` 中未包含团队 `channelData` 信息。</span><span class="sxs-lookup"><span data-stu-id="693d5-148">Your bot receives the `conversationUpdate` event as you add the bots to a team, without the team information in the `channelData` object.</span></span>

## <a name="block-a-bot-in-personal-chat"></a><span data-ttu-id="693d5-149">在个人聊天中阻止聊天机器人</span><span class="sxs-lookup"><span data-stu-id="693d5-149">Block a bot in personal chat</span></span>

<span data-ttu-id="693d5-150">用户可以选择阻止机器人发送个人聊天消息。</span><span class="sxs-lookup"><span data-stu-id="693d5-150">Users can choose to block your bot from sending personal chat messages.</span></span> <span data-ttu-id="693d5-151">他们可通过右键单击聊天频道中的机器人并选择"阻止机器人对话" **来切换此模式**。</span><span class="sxs-lookup"><span data-stu-id="693d5-151">They may toggle this by right-clicking your bot in the chat channel and choosing **Block bot conversation**.</span></span> <span data-ttu-id="693d5-152">这意味着，自动程序将继续发送消息，但是，用户不会收到这些消息。</span><span class="sxs-lookup"><span data-stu-id="693d5-152">This means, your bots continues to send messages, however, the user does not receive the messages.</span></span>

![阻止机器人](~/assets/images/bots/botdisable.png)

## <a name="remove-a-bot-from-a-team"></a><span data-ttu-id="693d5-154">从团队中删除机器人</span><span class="sxs-lookup"><span data-stu-id="693d5-154">Remove a bot from a team</span></span>

<span data-ttu-id="693d5-155">用户可以通过在团队视图中选择机器人列表上的"回收站"图标来删除机器人。</span><span class="sxs-lookup"><span data-stu-id="693d5-155">Users can delete the bot by choosing the trash-can icon on the bots list in their team's view.</span></span> <span data-ttu-id="693d5-156">这仅从该团队的使用中删除自动程序，单个用户仍可在个人上下文中交互。</span><span class="sxs-lookup"><span data-stu-id="693d5-156">This only removes the bot from that team's use, individual users can still interact in personal context.</span></span> <span data-ttu-id="693d5-157">用户无法禁用或删除个人上下文中的聊天机器人。</span><span class="sxs-lookup"><span data-stu-id="693d5-157">Bots in personal context cannot be disabled or removed by users.</span></span>

## <a name="disable-a-bot-in-teams"></a><span data-ttu-id="693d5-158">在 Teams 中禁用自动程序</span><span class="sxs-lookup"><span data-stu-id="693d5-158">Disable a bot in Teams</span></span>

<span data-ttu-id="693d5-159">若要阻止机器人接收消息，请转到自动 **程序仪表板** 并编辑 Microsoft Teams 频道。</span><span class="sxs-lookup"><span data-stu-id="693d5-159">To stop your bot from receiving messages, go to your **Bot Dashboard** and edit the Microsoft Teams channel.</span></span> <span data-ttu-id="693d5-160">清除" **在 Microsoft Teams 上启用"** 选项。</span><span class="sxs-lookup"><span data-stu-id="693d5-160">Clear the **Enable on Microsoft Teams** option.</span></span> <span data-ttu-id="693d5-161">这将阻止用户与机器人交互，但是，它仍然可发现，并且用户仍能够将其添加到 Teams。</span><span class="sxs-lookup"><span data-stu-id="693d5-161">This prevents users from interacting with the bot, however, it will still be discoverable and users will still be able to add it to Teams.</span></span>

## <a name="delete-a-bot-from-teams"></a><span data-ttu-id="693d5-162">从 Teams 中删除自动程序</span><span class="sxs-lookup"><span data-stu-id="693d5-162">Delete a bot from Teams</span></span>

<span data-ttu-id="693d5-163">若要从 Teams 中完全删除自动程序，请转到自动 **程序仪表板** 并编辑 Microsoft Teams 频道。</span><span class="sxs-lookup"><span data-stu-id="693d5-163">To remove your bot completely from Teams, go to your **Bot Dashboard** and edit the Microsoft Teams channel.</span></span> <span data-ttu-id="693d5-164">选择底部的 **"删除** "按钮。</span><span class="sxs-lookup"><span data-stu-id="693d5-164">Choose the **Delete** button at the bottom.</span></span> <span data-ttu-id="693d5-165">这将阻止用户发现、添加机器人并与其交互。</span><span class="sxs-lookup"><span data-stu-id="693d5-165">This prevents users from discovering, adding, and interacting with your bot.</span></span> <span data-ttu-id="693d5-166">这不会将机器人从其他用户的 Teams 实例中删除，但会停止为它们运行。</span><span class="sxs-lookup"><span data-stu-id="693d5-166">This does not remove the bot from other user's Teams instances, however, it stops functioning for them as well.</span></span>

## <a name="see-also"></a><span data-ttu-id="693d5-167">另请参阅</span><span class="sxs-lookup"><span data-stu-id="693d5-167">See also</span></span>

> [!div class=nextstep]
> [<span data-ttu-id="693d5-168">使用检查中间件调试机器人</span><span class="sxs-lookup"><span data-stu-id="693d5-168">Debug your bot with inspection middleware</span></span>](/azure/bot-service/bot-service-debug-inspection-middleware)

> [!div class=nextstep]
> [<span data-ttu-id="693d5-169">在本地调试呼叫和会议机器人</span><span class="sxs-lookup"><span data-stu-id="693d5-169">Debug your calling and meeting bot locally</span></span>](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
