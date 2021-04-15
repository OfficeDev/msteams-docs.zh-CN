---
title: 测试和调试自动程序
description: 介绍如何在 Microsoft Teams 中测试机器人
keywords: teams 机器人测试
ms.topic: how-to
ms.date: 03/20/2019
ms.openlocfilehash: 6403d9ba16510860492735944899285058d9c0f3
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696603"
---
# <a name="test-and-debug-your-microsoft-teams-bot"></a><span data-ttu-id="c12ac-104">测试和调试 Microsoft Teams 自动程序</span><span class="sxs-lookup"><span data-stu-id="c12ac-104">Test and debug your Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="c12ac-105">测试自动程序时，需要考虑希望自动程序运行的上下文 () 以及你可能已添加到需要特定于 Microsoft Teams 的数据的自动程序的任何功能。</span><span class="sxs-lookup"><span data-stu-id="c12ac-105">When testing your bot you need to take into consideration both the context(s) you want your bot to run in, as well as any functionality you may have added to your bot that requires data specific to Microsoft Teams.</span></span> <span data-ttu-id="c12ac-106">确保你选择用于测试机器人的方法与它的功能一致。</span><span class="sxs-lookup"><span data-stu-id="c12ac-106">Make sure that the method you chose to test your bot aligns with its functionality.</span></span>

## <a name="test-by-uploading-to-teams"></a><span data-ttu-id="c12ac-107">通过上传到 Teams 进行测试</span><span class="sxs-lookup"><span data-stu-id="c12ac-107">Test by uploading to Teams</span></span>

<span data-ttu-id="c12ac-108">测试自动程序的最全面方法就是创建应用包并将其上传到 Teams。</span><span class="sxs-lookup"><span data-stu-id="c12ac-108">The most comprehensive way to test your bot is by creating an app package and uploading it to Teams.</span></span> <span data-ttu-id="c12ac-109">这是在所有范围内测试自动程序可用的完整功能的唯一方法。</span><span class="sxs-lookup"><span data-stu-id="c12ac-109">This is the only method to test the full functionality available to your bot, across all scopes.</span></span>

<span data-ttu-id="c12ac-110">有两种上传应用的方法。</span><span class="sxs-lookup"><span data-stu-id="c12ac-110">There are two methods for uploading your app.</span></span> <span data-ttu-id="c12ac-111">可以使用 App [Studio](~/concepts/build-and-test/app-studio-overview.md)来帮助你，也可以手动创建应用[包并](~/concepts/build-and-test/apps-package.md)[上传应用](~/concepts/deploy-and-publish/apps-upload.md)。</span><span class="sxs-lookup"><span data-stu-id="c12ac-111">You can either use [App Studio](~/concepts/build-and-test/app-studio-overview.md) to help you, or you can manually [create an app package](~/concepts/build-and-test/apps-package.md) and [upload your app](~/concepts/deploy-and-publish/apps-upload.md).</span></span> <span data-ttu-id="c12ac-112">如果你需要更改清单并重新上传应用，应在上传更改的应用包之前删除自动[](#deleting-a-bot-from-teams)程序。</span><span class="sxs-lookup"><span data-stu-id="c12ac-112">If you need to alter your manifest and re-upload your app, you should [delete your bot](#deleting-a-bot-from-teams) before uploading your altered app package.</span></span>

## <a name="debug-your-bot-locally"></a><span data-ttu-id="c12ac-113">在本地调试机器人</span><span class="sxs-lookup"><span data-stu-id="c12ac-113">Debug your bot locally</span></span>

<span data-ttu-id="c12ac-114">如果你在开发期间在本地托管机器人，则需要使用 [类似 ngrok](https://ngrok.com/) 的隧道服务来测试机器人。</span><span class="sxs-lookup"><span data-stu-id="c12ac-114">If you are hosting your bot locally during development you'll need to use a tunneling service like [ngrok](https://ngrok.com/) in order to test your bot.</span></span> <span data-ttu-id="c12ac-115">下载并安装 ngrok 后，运行以下命令以启动隧道服务 (你可能需要将 ngrok 添加到路径) 。</span><span class="sxs-lookup"><span data-stu-id="c12ac-115">Once you've downloaded and installed ngrok, run the below command to start the tunneling service (you may need to add ngrok to your path).</span></span>

```bash
ngrok http <port> -host-header=localhost:<port>
```

<span data-ttu-id="c12ac-116">在应用清单中，使用 ngrok 提供的 https 终结点。</span><span class="sxs-lookup"><span data-stu-id="c12ac-116">Use the https endpoint provided by ngrok in your app manifest.</span></span> <span data-ttu-id="c12ac-117">如果关闭命令窗口并重启，你将获得一个新 URL，并且你将需要更新你的自动程序终结点地址以使用该地址。</span><span class="sxs-lookup"><span data-stu-id="c12ac-117">If you close your command window and restart you'll get a new URL, and you'll need to update your bot endpoint address to use that one as well.</span></span>

## <a name="testing-your-bot-without-uploading-to-teams"></a><span data-ttu-id="c12ac-118">在未上传到 Teams 的情况下测试自动程序</span><span class="sxs-lookup"><span data-stu-id="c12ac-118">Testing your bot without uploading to Teams</span></span>

<span data-ttu-id="c12ac-119">有时，可能需要测试自动程序，无需将其安装为 Teams 中的应用。</span><span class="sxs-lookup"><span data-stu-id="c12ac-119">Occasionally it may be necessary to test your bot without installing it as an app in Teams.</span></span> <span data-ttu-id="c12ac-120">我们在下面提供了两种执行此操作的方法。</span><span class="sxs-lookup"><span data-stu-id="c12ac-120">We provide two methods for doing so below.</span></span> <span data-ttu-id="c12ac-121">在未将其安装为应用的情况下测试自动程序对于确保自动程序可用并做出响应非常有用，但是，它不允许测试你已添加到自动程序的全部 Microsoft Teams 功能。</span><span class="sxs-lookup"><span data-stu-id="c12ac-121">Testing your bot without installing it as an app can be useful to ensure your bot is available and responding, however it will not allow you to test the full breadth of Microsoft Teams functionality you may have added to your bot.</span></span> <span data-ttu-id="c12ac-122">如果你需要完全测试自动程序，请按照上传 [的说明进行测试](#test-by-uploading-to-teams)。</span><span class="sxs-lookup"><span data-stu-id="c12ac-122">If you need to fully test your bot, please follow the instructions for [testing by uploading](#test-by-uploading-to-teams).</span></span>

### <a name="use-the-bot-emulator"></a><span data-ttu-id="c12ac-123">使用自动程序仿真器</span><span class="sxs-lookup"><span data-stu-id="c12ac-123">Use the Bot Emulator</span></span>

<span data-ttu-id="c12ac-124">Bot Framework Emulator 是一个桌面应用程序，允许机器人开发人员在本地或远程测试和调试其机器人。</span><span class="sxs-lookup"><span data-stu-id="c12ac-124">The Bot Framework Emulator is a desktop application that allows bot developers to test and debug their bots, either locally or remotely.</span></span> <span data-ttu-id="c12ac-125">使用仿真器，你可以与机器人聊天并检查机器人发送和接收的消息。</span><span class="sxs-lookup"><span data-stu-id="c12ac-125">Using the emulator, you can chat with your bot and inspect the messages that your bot sends and receives.</span></span> <span data-ttu-id="c12ac-126">这可用于验证自动程序是否可用并做出响应，但仿真器不允许测试已添加到自动程序的任何特定于 Teams 的功能，并且自动程序的响应也不会准确地直观地表示它们在 Teams 中的呈现方式。</span><span class="sxs-lookup"><span data-stu-id="c12ac-126">This can be useful for verifying that your bot is available and responding, however the emulator will not allow you to test any Teams-specific functionality you've added to your bot, nor will responses from your bot be an accurate visual representation of how they will be rendered in Teams.</span></span> <span data-ttu-id="c12ac-127">如果你需要测试其中任一内容，最好上传 [自动程序](#test-by-uploading-to-teams)。</span><span class="sxs-lookup"><span data-stu-id="c12ac-127">If you need to test either of those things it is best to [upload your bot](#test-by-uploading-to-teams).</span></span>

<span data-ttu-id="c12ac-128">有关 Bot Framework Emulator 的完整说明，请参阅 [此处](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="c12ac-128">Complete instructions on the Bot Framework Emulator can be found [here](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true).</span></span>

### <a name="talk-to-your-bot-directly-by-id"></a><span data-ttu-id="c12ac-129">直接通过 ID 与机器人交谈</span><span class="sxs-lookup"><span data-stu-id="c12ac-129">Talk to your bot directly by Id</span></span>

>[!Important]
><span data-ttu-id="c12ac-130">按 ID 与机器人交谈仅用于测试目的。</span><span class="sxs-lookup"><span data-stu-id="c12ac-130">Talking to your bot by Id is intended for testing purposes only.</span></span>

<span data-ttu-id="c12ac-131">您还可以使用自动程序 ID 启动对话。下面提供两种执行此操作的方法。</span><span class="sxs-lookup"><span data-stu-id="c12ac-131">You can also initiate a conversation with your bot by using its Id. Two methods for doing so are given below.</span></span> <span data-ttu-id="c12ac-132">通过这些方法之一添加自动程序后，将无法在频道对话中处理它，并且你无法利用其他 Microsoft Teams 应用功能，如选项卡或消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="c12ac-132">When a bot has been added through one of these methods it will not be addressable in channel conversations, and you cannot take advantage of other Microsoft Teams app capabilities like tabs or messaging extensions.</span></span>

1. <span data-ttu-id="c12ac-133">在机器人 [的"](https://dev.botframework.com/bots)自动程序仪表板"页上的"**频道"下**，选择"**添加到 Microsoft Teams"。**</span><span class="sxs-lookup"><span data-stu-id="c12ac-133">On the [Bot Dashboard](https://dev.botframework.com/bots) page for your bot, under **Channels**, select **Add to Microsoft Teams**.</span></span> <span data-ttu-id="c12ac-134">Microsoft Teams 将启动与机器人进行个人聊天。</span><span class="sxs-lookup"><span data-stu-id="c12ac-134">Microsoft Teams will launch with a personal chat with your bot.</span></span>
2. <span data-ttu-id="c12ac-135">直接从 Microsoft Teams 中引用机器人的应用 ID：</span><span class="sxs-lookup"><span data-stu-id="c12ac-135">Directly reference your bot's app ID from within Microsoft Teams:</span></span>
   * <span data-ttu-id="c12ac-136">在 [自动程序"](https://dev.botframework.com/bots)自动程序仪表板"页上的"详细信息 **"** 下，复制自动程序 Microsoft **应用 ID。**</span><span class="sxs-lookup"><span data-stu-id="c12ac-136">On the [Bot Dashboard](https://dev.botframework.com/bots) page for your bot, under **Details**, copy the **Microsoft App ID** for your bot.</span></span>
  
     ![获取机器人的 AppID](~/assets/images/bots_appid_botframework.png)
  
   * <span data-ttu-id="c12ac-138">在 Microsoft Teams 内的"聊天 **"** 窗格中，选择" **添加聊天"** 图标。</span><span class="sxs-lookup"><span data-stu-id="c12ac-138">From within Microsoft Teams, on the **Chat** pane, select the **Add chat** icon.</span></span> <span data-ttu-id="c12ac-139">For **To:**, paste your bot's Microsoft App ID.</span><span class="sxs-lookup"><span data-stu-id="c12ac-139">For **To:**, paste your bot's Microsoft App ID.</span></span>
  
     ![上传机器人的 AppID](~/assets/images/bots_uploading.png)

     <span data-ttu-id="c12ac-141">应用 ID 应解析为自动程序名称。</span><span class="sxs-lookup"><span data-stu-id="c12ac-141">The app ID should resolve to your bot name.</span></span>

   * <span data-ttu-id="c12ac-142">选择自动程序并发送消息以启动对话。</span><span class="sxs-lookup"><span data-stu-id="c12ac-142">Select your bot and send a message to initiate a conversation.</span></span>
   * <span data-ttu-id="c12ac-143">或者，你可以将机器人的应用 ID 粘贴到 Microsoft Teams 左上方的搜索框中。</span><span class="sxs-lookup"><span data-stu-id="c12ac-143">Alternatively, you can paste your bot's app ID in the search box in the top left in Microsoft Teams.</span></span> <span data-ttu-id="c12ac-144">在搜索结果页面中，导航到"人员"选项卡以查看自动程序并开始与它聊天。</span><span class="sxs-lookup"><span data-stu-id="c12ac-144">In the search results page, navigate to the People tab to see your bot and to start chatting with it.</span></span>

<span data-ttu-id="c12ac-145">机器人将像添加到团队的机器人一样接收事件，但 `conversationUpdate` 对象中不会包含团队 `channelData` 信息。</span><span class="sxs-lookup"><span data-stu-id="c12ac-145">Your bot will receive the `conversationUpdate` event just like bots added to a team, but without the team information in the `channelData` object.</span></span>

## <a name="blocking-a-bot-in-personal-chat"></a><span data-ttu-id="c12ac-146">阻止个人聊天中的机器人</span><span class="sxs-lookup"><span data-stu-id="c12ac-146">Blocking a bot in personal chat</span></span>

<span data-ttu-id="c12ac-147">请注意，用户可以选择阻止机器人发送个人聊天消息。</span><span class="sxs-lookup"><span data-stu-id="c12ac-147">Note that users can choose to block your bot from sending personal chat messages.</span></span> <span data-ttu-id="c12ac-148">他们可通过右键单击聊天频道中的机器人并选择"阻止机器人对话" **来切换此模式**。</span><span class="sxs-lookup"><span data-stu-id="c12ac-148">They may toggle this by right-clicking your bot in the chat channel and choosing **Block bot conversation**.</span></span> <span data-ttu-id="c12ac-149">这意味着自动程序将继续发送消息，但用户不会收到这些消息。</span><span class="sxs-lookup"><span data-stu-id="c12ac-149">This means your bots will continue to send messages but the user will not receive those messages.</span></span>

![阻止机器人](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a><span data-ttu-id="c12ac-151">从团队中删除机器人</span><span class="sxs-lookup"><span data-stu-id="c12ac-151">Removing a bot from a team</span></span>

<span data-ttu-id="c12ac-152">用户可以通过在团队视图中选择机器人列表上的"回收站"图标来删除机器人。</span><span class="sxs-lookup"><span data-stu-id="c12ac-152">Users can delete the bot by choosing the trash-can icon on the bots list in their teams view.</span></span> <span data-ttu-id="c12ac-153">请注意，这只会从该团队的使用中删除自动程序;单个用户仍可在个人上下文中交互。</span><span class="sxs-lookup"><span data-stu-id="c12ac-153">Note that this only removes the bot from that team's use; individual users will still be able to interact in personal context.</span></span>

<span data-ttu-id="c12ac-154">用户无法禁用或删除个人上下文中的聊天机器人，但无法从 Teams 中完全删除聊天机器人。</span><span class="sxs-lookup"><span data-stu-id="c12ac-154">Bots in personal context cannot be disabled or removed by a user, short of completely removing the bot from Teams.</span></span>

## <a name="disabling-a-bot-in-teams"></a><span data-ttu-id="c12ac-155">在 Teams 中禁用机器人</span><span class="sxs-lookup"><span data-stu-id="c12ac-155">Disabling a bot in Teams</span></span>

<span data-ttu-id="c12ac-156">若要停止机器人接收消息，请转到自动程序仪表板并编辑 Microsoft Teams 频道。</span><span class="sxs-lookup"><span data-stu-id="c12ac-156">To stop your bot receiving messages, go to your Bot Dashboard and edit the Microsoft Teams channel.</span></span> <span data-ttu-id="c12ac-157">清除" **在 Microsoft Teams 上启用"** 选项。</span><span class="sxs-lookup"><span data-stu-id="c12ac-157">Clear the **Enable on Microsoft Teams** option.</span></span> <span data-ttu-id="c12ac-158">这将阻止用户与机器人交互，但仍可以发现它，并且用户仍能够将其添加到团队。</span><span class="sxs-lookup"><span data-stu-id="c12ac-158">This prevents users from interacting with the bot, but it will still be discoverable and users will still be able to add it to teams.</span></span>

## <a name="deleting-a-bot-from-teams"></a><span data-ttu-id="c12ac-159">从 Teams 中删除机器人</span><span class="sxs-lookup"><span data-stu-id="c12ac-159">Deleting a bot from Teams</span></span>

<span data-ttu-id="c12ac-160">若要从 Teams 中完全删除自动程序，请转到自动程序仪表板并编辑 Microsoft Teams 频道。</span><span class="sxs-lookup"><span data-stu-id="c12ac-160">To remove your bot completely from Teams, go to your Bot Dashboard and edit the Microsoft Teams channel.</span></span> <span data-ttu-id="c12ac-161">选择底部的 **"删除** "按钮。</span><span class="sxs-lookup"><span data-stu-id="c12ac-161">Choose the **Delete** button at the bottom.</span></span> <span data-ttu-id="c12ac-162">这将阻止用户发现、添加或与机器人交互。</span><span class="sxs-lookup"><span data-stu-id="c12ac-162">This prevents users from discovering, adding, or interacting with your bot.</span></span> <span data-ttu-id="c12ac-163">请注意，这不会从其他用户的 Teams 实例中删除自动程序，尽管它也将停止为它们运行。</span><span class="sxs-lookup"><span data-stu-id="c12ac-163">Note that this does not remove the bot from other users' Teams instances, although it will cease functioning for them as well.</span></span>

## <a name="removing-your-bot-from-appsource"></a><span data-ttu-id="c12ac-164">从 AppSource 中删除机器人</span><span class="sxs-lookup"><span data-stu-id="c12ac-164">Removing your bot from AppSource</span></span>

<span data-ttu-id="c12ac-165">如果你想要从 AppSource 中的 Teams 应用中删除自动程序 (以前是 Office 应用商店) ，则必须从应用清单中删除自动程序并重新提交应用进行验证。</span><span class="sxs-lookup"><span data-stu-id="c12ac-165">If you want to remove your bot from your Teams app in AppSource (formerly Office Store), you must remove the bot from your app manifest and resubmit your app for validation.</span></span> <span data-ttu-id="c12ac-166">有关详细信息[，请参阅将 Microsoft Teams 应用发布到 AppSource。](~/concepts/deploy-and-publish/apps-publish.md)</span><span class="sxs-lookup"><span data-stu-id="c12ac-166">See [Publish your Microsoft Teams app to AppSource](~/concepts/deploy-and-publish/apps-publish.md) for more information.</span></span>
