---
title: 测试和调试自动程序
description: 介绍如何在 Microsoft Teams
keywords: teams 机器人测试
ms.topic: how-to
localization_priority: Normal
ms.date: 03/20/2019
ms.openlocfilehash: 269b0680e45d764cf4cb0269c40d3d202145edb8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566458"
---
# <a name="test-and-debug-your-microsoft-teams-bot"></a><span data-ttu-id="b890c-104">测试和调试自动Microsoft Teams程序</span><span class="sxs-lookup"><span data-stu-id="b890c-104">Test and debug your Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="b890c-105">测试自动程序时，需要考虑希望自动程序运行的上下文 () 以及你可能已添加到需要特定于 Microsoft Teams 的数据的自动程序的任何功能。</span><span class="sxs-lookup"><span data-stu-id="b890c-105">When testing your bot you need to take into consideration both the context(s) you want your bot to run in, as well as any functionality you may have added to your bot that requires data specific to Microsoft Teams.</span></span> <span data-ttu-id="b890c-106">确保你选择用于测试机器人的方法与它的功能一致。</span><span class="sxs-lookup"><span data-stu-id="b890c-106">Make sure that the method you chose to test your bot aligns with its functionality.</span></span>

## <a name="test-by-uploading-to-teams"></a><span data-ttu-id="b890c-107">通过上载到网站进行测试Teams</span><span class="sxs-lookup"><span data-stu-id="b890c-107">Test by uploading to Teams</span></span>

<span data-ttu-id="b890c-108">测试自动程序最全面的方式是创建应用包并将其上传到Teams。</span><span class="sxs-lookup"><span data-stu-id="b890c-108">The most comprehensive way to test your bot is by creating an app package and uploading it to Teams.</span></span> <span data-ttu-id="b890c-109">这是在所有范围内测试自动程序可用的完整功能的唯一方法。</span><span class="sxs-lookup"><span data-stu-id="b890c-109">This is the only method to test the full functionality available to your bot, across all scopes.</span></span>

<span data-ttu-id="b890c-110">有两种上传应用的方法。</span><span class="sxs-lookup"><span data-stu-id="b890c-110">There are two methods for uploading your app.</span></span> <span data-ttu-id="b890c-111">可以使用 App [Studio](~/concepts/build-and-test/app-studio-overview.md)来帮助你，也可以手动创建应用[包并](~/concepts/build-and-test/apps-package.md)[上传应用](~/concepts/deploy-and-publish/apps-upload.md)。</span><span class="sxs-lookup"><span data-stu-id="b890c-111">You can either use [App Studio](~/concepts/build-and-test/app-studio-overview.md) to help you, or you can manually [create an app package](~/concepts/build-and-test/apps-package.md) and [upload your app](~/concepts/deploy-and-publish/apps-upload.md).</span></span> <span data-ttu-id="b890c-112">如果你需要更改清单并重新上传应用，应在上传更改的应用包之前删除自动[](#deleting-a-bot-from-teams)程序。</span><span class="sxs-lookup"><span data-stu-id="b890c-112">If you need to alter your manifest and re-upload your app, you should [delete your bot](#deleting-a-bot-from-teams) before uploading your altered app package.</span></span>

## <a name="debug-your-bot-locally"></a><span data-ttu-id="b890c-113">在本地调试机器人</span><span class="sxs-lookup"><span data-stu-id="b890c-113">Debug your bot locally</span></span>

<span data-ttu-id="b890c-114">如果你在开发期间在本地托管机器人，则需要使用 [类似 ngrok](https://ngrok.com/) 的隧道服务来测试机器人。</span><span class="sxs-lookup"><span data-stu-id="b890c-114">If you are hosting your bot locally during development you'll need to use a tunneling service like [ngrok](https://ngrok.com/) in order to test your bot.</span></span> <span data-ttu-id="b890c-115">下载并安装 ngrok 后，运行以下命令以启动隧道服务。</span><span class="sxs-lookup"><span data-stu-id="b890c-115">Once you've downloaded and installed ngrok, run the below command to start the tunneling service.</span></span> <span data-ttu-id="b890c-116">你可能需要将 ngrok 添加到你的路径。</span><span class="sxs-lookup"><span data-stu-id="b890c-116">You may need to add ngrok to your path.</span></span>

```bash
ngrok http <port> -host-header=localhost:<port>
```

<span data-ttu-id="b890c-117">在应用清单中，使用 ngrok 提供的 https 终结点。</span><span class="sxs-lookup"><span data-stu-id="b890c-117">Use the https endpoint provided by ngrok in your app manifest.</span></span> <span data-ttu-id="b890c-118">如果关闭命令窗口并重启，你将获得一个新 URL，并且你将需要更新你的自动程序终结点地址以使用该地址。</span><span class="sxs-lookup"><span data-stu-id="b890c-118">If you close your command window and restart you'll get a new URL, and you'll need to update your bot endpoint address to use that one as well.</span></span>

## <a name="testing-your-bot-without-uploading-to-teams"></a><span data-ttu-id="b890c-119">测试自动程序而不上载到Teams</span><span class="sxs-lookup"><span data-stu-id="b890c-119">Testing your bot without uploading to Teams</span></span>

<span data-ttu-id="b890c-120">有时，可能需要测试自动程序，而无需将其安装为 Teams。</span><span class="sxs-lookup"><span data-stu-id="b890c-120">Occasionally it may be necessary to test your bot without installing it as an app in Teams.</span></span> <span data-ttu-id="b890c-121">我们在下面提供了两种执行此操作的方法。</span><span class="sxs-lookup"><span data-stu-id="b890c-121">We provide two methods for doing so below.</span></span> <span data-ttu-id="b890c-122">在不将机器人安装为应用的情况下测试它对于确保自动程序可用并做出响应非常有用，但是，它不允许测试可能添加到自动程序的全部 Microsoft Teams 功能。</span><span class="sxs-lookup"><span data-stu-id="b890c-122">Testing your bot without installing it as an app can be useful to ensure your bot is available and responding, however it will not allow you to test the full breadth of Microsoft Teams functionality you may have added to your bot.</span></span> <span data-ttu-id="b890c-123">如果你需要完全测试自动程序，请按照上传 [的说明进行测试](#test-by-uploading-to-teams)。</span><span class="sxs-lookup"><span data-stu-id="b890c-123">If you need to fully test your bot, please follow the instructions for [testing by uploading](#test-by-uploading-to-teams).</span></span>

### <a name="use-the-bot-emulator"></a><span data-ttu-id="b890c-124">使用自动程序仿真器</span><span class="sxs-lookup"><span data-stu-id="b890c-124">Use the Bot Emulator</span></span>

<span data-ttu-id="b890c-125">此Bot Framework Emulator是一个桌面应用程序，允许机器人开发人员在本地或远程测试和调试其自动程序。</span><span class="sxs-lookup"><span data-stu-id="b890c-125">The Bot Framework Emulator is a desktop application that allows bot developers to test and debug their bots, either locally or remotely.</span></span> <span data-ttu-id="b890c-126">使用仿真器，你可以与机器人聊天并检查机器人发送和接收的消息。</span><span class="sxs-lookup"><span data-stu-id="b890c-126">Using the emulator, you can chat with your bot and inspect the messages that your bot sends and receives.</span></span> <span data-ttu-id="b890c-127">这可用于验证自动程序是否可用并做出响应，但仿真器不允许测试已添加到自动程序的任何 Teams 特定功能，来自自动程序的响应也不会成为它们在 Teams 中的呈现方式的准确直观表示形式。</span><span class="sxs-lookup"><span data-stu-id="b890c-127">This can be useful for verifying that your bot is available and responding, however the emulator will not allow you to test any Teams-specific functionality you've added to your bot, nor will responses from your bot be an accurate visual representation of how they will be rendered in Teams.</span></span> <span data-ttu-id="b890c-128">如果你需要测试其中任一内容，最好上传 [自动程序](#test-by-uploading-to-teams)。</span><span class="sxs-lookup"><span data-stu-id="b890c-128">If you need to test either of those things it is best to [upload your bot](#test-by-uploading-to-teams).</span></span>

<span data-ttu-id="b890c-129">有关完整说明Bot Framework Emulator可以在此处[找到](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="b890c-129">Complete instructions on the Bot Framework Emulator can be found [here](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true).</span></span>

### <a name="talk-to-your-bot-directly-by-id"></a><span data-ttu-id="b890c-130">直接通过 ID 与机器人交谈</span><span class="sxs-lookup"><span data-stu-id="b890c-130">Talk to your bot directly by Id</span></span>

>[!Important]
><span data-ttu-id="b890c-131">按 ID 与机器人交谈仅用于测试目的。</span><span class="sxs-lookup"><span data-stu-id="b890c-131">Talking to your bot by Id is intended for testing purposes only.</span></span>

<span data-ttu-id="b890c-132">您还可以使用自动程序 ID 启动对话。下面提供两种执行此操作的方法。</span><span class="sxs-lookup"><span data-stu-id="b890c-132">You can also initiate a conversation with your bot by using its Id. Two methods for doing so are given below.</span></span> <span data-ttu-id="b890c-133">通过这些方法之一添加自动程序后，将无法在频道对话中处理它，并且你无法利用其他 Microsoft Teams 应用功能，如选项卡或消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="b890c-133">When a bot has been added through one of these methods it will not be addressable in channel conversations, and you cannot take advantage of other Microsoft Teams app capabilities like tabs or messaging extensions.</span></span>

1. <span data-ttu-id="b890c-134">在 [机器人的"](https://dev.botframework.com/bots)自动程序仪表板"页上的"频道 **"** 下，选择"**添加到Microsoft Teams"。**</span><span class="sxs-lookup"><span data-stu-id="b890c-134">On the [Bot Dashboard](https://dev.botframework.com/bots) page for your bot, under **Channels**, select **Add to Microsoft Teams**.</span></span> <span data-ttu-id="b890c-135">Microsoft Teams自动程序通过个人聊天启动。</span><span class="sxs-lookup"><span data-stu-id="b890c-135">Microsoft Teams will launch with a personal chat with your bot.</span></span>
2. <span data-ttu-id="b890c-136">直接在应用中引用自动程序Microsoft Teams：</span><span class="sxs-lookup"><span data-stu-id="b890c-136">Directly reference your bot's app ID from within Microsoft Teams:</span></span>
   * <span data-ttu-id="b890c-137">在 [自动程序"](https://dev.botframework.com/bots)自动程序仪表板"页上的"详细信息 **"** 下，复制自动程序 Microsoft **应用 ID。**</span><span class="sxs-lookup"><span data-stu-id="b890c-137">On the [Bot Dashboard](https://dev.botframework.com/bots) page for your bot, under **Details**, copy the **Microsoft App ID** for your bot.</span></span>
  
     ![获取机器人的 AppID](~/assets/images/bots_appid_botframework.png)
  
   * <span data-ttu-id="b890c-139">在"Microsoft Teams"**窗格中，选择**"添加 **聊天"** 图标。</span><span class="sxs-lookup"><span data-stu-id="b890c-139">From within Microsoft Teams, on the **Chat** pane, select the **Add chat** icon.</span></span> <span data-ttu-id="b890c-140">For **To:**, paste your bot's Microsoft App ID.</span><span class="sxs-lookup"><span data-stu-id="b890c-140">For **To:**, paste your bot's Microsoft App ID.</span></span>
  
     ![上传机器人的 AppID](~/assets/images/bots_uploading.png)

     <span data-ttu-id="b890c-142">应用 ID 应解析为自动程序名称。</span><span class="sxs-lookup"><span data-stu-id="b890c-142">The app ID should resolve to your bot name.</span></span>

   * <span data-ttu-id="b890c-143">选择自动程序并发送消息以启动对话。</span><span class="sxs-lookup"><span data-stu-id="b890c-143">Select your bot and send a message to initiate a conversation.</span></span>
   * <span data-ttu-id="b890c-144">或者，你可以将机器人的应用 ID 粘贴到搜索框左上方的搜索框中Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="b890c-144">Alternatively, you can paste your bot's app ID in the search box in the top left in Microsoft Teams.</span></span> <span data-ttu-id="b890c-145">在搜索结果页面中，导航到"人员"选项卡以查看自动程序并开始与它聊天。</span><span class="sxs-lookup"><span data-stu-id="b890c-145">In the search results page, navigate to the People tab to see your bot and to start chatting with it.</span></span>

<span data-ttu-id="b890c-146">机器人将像添加到团队的机器人一样接收事件，但 `conversationUpdate` 对象中不会包含团队 `channelData` 信息。</span><span class="sxs-lookup"><span data-stu-id="b890c-146">Your bot will receive the `conversationUpdate` event just like bots added to a team, but without the team information in the `channelData` object.</span></span>

## <a name="blocking-a-bot-in-personal-chat"></a><span data-ttu-id="b890c-147">阻止个人聊天中的机器人</span><span class="sxs-lookup"><span data-stu-id="b890c-147">Blocking a bot in personal chat</span></span>

<span data-ttu-id="b890c-148">请注意，用户可以选择阻止机器人发送个人聊天消息。</span><span class="sxs-lookup"><span data-stu-id="b890c-148">Note that users can choose to block your bot from sending personal chat messages.</span></span> <span data-ttu-id="b890c-149">他们可通过右键单击聊天频道中的机器人并选择"阻止机器人对话" **来切换此模式**。</span><span class="sxs-lookup"><span data-stu-id="b890c-149">They may toggle this by right-clicking your bot in the chat channel and choosing **Block bot conversation**.</span></span> <span data-ttu-id="b890c-150">这意味着自动程序将继续发送消息，但用户不会收到这些消息。</span><span class="sxs-lookup"><span data-stu-id="b890c-150">This means your bots will continue to send messages but the user will not receive those messages.</span></span>

![阻止机器人](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a><span data-ttu-id="b890c-152">从团队中删除机器人</span><span class="sxs-lookup"><span data-stu-id="b890c-152">Removing a bot from a team</span></span>

<span data-ttu-id="b890c-153">用户可以通过在团队视图中选择机器人列表上的"回收站"图标来删除机器人。</span><span class="sxs-lookup"><span data-stu-id="b890c-153">Users can delete the bot by choosing the trash-can icon on the bots list in their teams view.</span></span> <span data-ttu-id="b890c-154">请注意，这只会从该团队的使用中删除自动程序;单个用户仍可在个人上下文中交互。</span><span class="sxs-lookup"><span data-stu-id="b890c-154">Note that this only removes the bot from that team's use; individual users will still be able to interact in personal context.</span></span>

<span data-ttu-id="b890c-155">用户无法禁用或删除个人上下文中的自动程序，但无法从用户Teams。</span><span class="sxs-lookup"><span data-stu-id="b890c-155">Bots in personal context cannot be disabled or removed by a user, short of completely removing the bot from Teams.</span></span>

## <a name="disabling-a-bot-in-teams"></a><span data-ttu-id="b890c-156">禁用聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="b890c-156">Disabling a bot in Teams</span></span>

<span data-ttu-id="b890c-157">若要停止机器人接收消息，请转到自动程序仪表板并编辑Microsoft Teams通道。</span><span class="sxs-lookup"><span data-stu-id="b890c-157">To stop your bot receiving messages, go to your Bot Dashboard and edit the Microsoft Teams channel.</span></span> <span data-ttu-id="b890c-158">清除"**启用Microsoft Teams** 选项。</span><span class="sxs-lookup"><span data-stu-id="b890c-158">Clear the **Enable on Microsoft Teams** option.</span></span> <span data-ttu-id="b890c-159">这将阻止用户与机器人交互，但仍可以发现它，并且用户仍能够将其添加到团队。</span><span class="sxs-lookup"><span data-stu-id="b890c-159">This prevents users from interacting with the bot, but it will still be discoverable and users will still be able to add it to teams.</span></span>

## <a name="deleting-a-bot-from-teams"></a><span data-ttu-id="b890c-160">从用户中删除Teams</span><span class="sxs-lookup"><span data-stu-id="b890c-160">Deleting a bot from Teams</span></span>

<span data-ttu-id="b890c-161">若要从自动程序完全Teams，请转到自动程序仪表板并编辑Microsoft Teams通道。</span><span class="sxs-lookup"><span data-stu-id="b890c-161">To remove your bot completely from Teams, go to your Bot Dashboard and edit the Microsoft Teams channel.</span></span> <span data-ttu-id="b890c-162">选择底部的 **"删除** "按钮。</span><span class="sxs-lookup"><span data-stu-id="b890c-162">Choose the **Delete** button at the bottom.</span></span> <span data-ttu-id="b890c-163">这将阻止用户发现、添加或与机器人交互。</span><span class="sxs-lookup"><span data-stu-id="b890c-163">This prevents users from discovering, adding, or interacting with your bot.</span></span> <span data-ttu-id="b890c-164">请注意，这不会将机器人从其他用户Teams中删除，尽管它也将停止运行。</span><span class="sxs-lookup"><span data-stu-id="b890c-164">Note that this does not remove the bot from other users' Teams instances, although it will cease functioning for them as well.</span></span>

## <a name="removing-your-bot-from-appsource"></a><span data-ttu-id="b890c-165">从 AppSource 中删除机器人</span><span class="sxs-lookup"><span data-stu-id="b890c-165">Removing your bot from AppSource</span></span>

<span data-ttu-id="b890c-166">如果你希望从 AppSource (Office Store) 中的 Teams 应用中删除自动程序，必须从应用清单中删除自动程序并重新提交应用进行验证。</span><span class="sxs-lookup"><span data-stu-id="b890c-166">If you want to remove your bot from your Teams app in AppSource (previously Office Store), you must remove the bot from your app manifest and resubmit your app for validation.</span></span> <span data-ttu-id="b890c-167">有关详细信息，请参阅将[应用Microsoft Teams AppSource。](~/concepts/deploy-and-publish/apps-publish.md)</span><span class="sxs-lookup"><span data-stu-id="b890c-167">For more information, see [Publish your Microsoft Teams app to AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span></span>
