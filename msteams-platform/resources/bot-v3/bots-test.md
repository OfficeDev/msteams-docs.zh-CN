---
title: 测试和调试自动程序
description: 介绍如何在 Microsoft Teams
keywords: teams 机器人测试
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 03/20/2019
ms.openlocfilehash: 71d70aef3adeb3d351223e918aec21d0d2dea440
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2021
ms.locfileid: "60720118"
---
# <a name="test-and-debug-your-microsoft-teams-bot"></a>测试和调试Microsoft Teams程序

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

测试自动程序时，需要考虑希望自动程序运行的上下文 () 以及你可能已添加到需要特定于 Microsoft Teams 的数据的自动程序的任何功能。 确保你选择用于测试机器人的方法与它的功能一致。

## <a name="test-by-uploading-to-teams"></a>通过上传到网站进行测试Teams

测试自动程序最全面的方式是创建应用包并将其上传到Teams。 这是在所有范围内测试自动程序可用的完整功能的唯一方法。

有两种上传应用的方法。 可以使用 App [Studio，](~/concepts/build-and-test/app-studio-overview.md) 也可以手动创建 [应用](~/concepts/build-and-test/apps-package.md) 包并 [上传应用](~/concepts/deploy-and-publish/apps-upload.md)。 如果你需要更改清单并重新加载应用，应在上传更改的应用包之前删除自动[](#deleting-a-bot-from-teams)程序。

## <a name="debug-your-bot-locally"></a>在本地调试机器人

如果你在开发期间在本地托管机器人，则需要使用 [类似 ngrok](https://ngrok.com/) 的隧道服务来测试机器人。 下载并安装 ngrok 后，运行以下命令以启动隧道服务。 你可能需要将 ngrok 添加到你的路径。

```bash
ngrok http <port> -host-header=localhost:<port>
```

在应用清单中，使用 ngrok 提供的 https 终结点。 如果关闭命令窗口并重新启动，你将会获得一个新 URL，并且需要更新你的自动程序终结点地址以使用该地址。

## <a name="testing-your-bot-without-uploading-to-teams"></a>测试自动程序而不上载到Teams

有时，在不将其安装为应用的情况下测试自动程序Teams。 我们提供两种测试方法。 在未将其安装为应用的情况下测试自动程序对于确保自动程序可用并做出响应非常有用，但是它不允许你测试可能已添加到自动程序的全部 Microsoft Teams 功能。 如果你需要完全测试自动程序，请按照上传 [的说明进行测试](#test-by-uploading-to-teams)。

### <a name="use-the-bot-emulator"></a>使用自动程序Emulator

the Bot Framework Emulator is a desktop application that allows bot developers to test and debug their bots， either locally or remotely. 使用仿真器，你可以与机器人聊天并检查机器人发送和接收的消息。 这可用于验证机器人是否可用并做出响应，但仿真器不允许测试已添加到自动程序的任何 Teams 特定功能，来自自动程序的响应也不会成为它们在 Teams 中的呈现方式的准确直观表示形式。 如果你需要测试其中任一内容，那么上传自动程序并非最佳 [方法](#test-by-uploading-to-teams)。

有关此Bot Framework Emulator的完整说明，请参阅[此处](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)。

### <a name="talk-to-your-bot-directly-by-id"></a>直接通过 ID 与机器人交谈

>[!Important]
>通过 ID 与机器人交谈仅用于测试目的。

您还可以使用自动程序 ID 启动对话。 下面提供两种执行此操作的方法。 当通过这些方法之一添加自动程序时，它无法通过频道对话进行解决，并且你无法利用其他 Microsoft Teams 应用功能，如选项卡或消息传递扩展。

1. 在机器人 [的"自动](https://dev.botframework.com/bots)程序仪表板"页上的"频道 **"** 下，选择"**添加到Microsoft Teams"。** Microsoft Teams聊天机器人通过个人聊天启动。
2. 直接在应用中引用自动程序Microsoft Teams：
   * 在 [自动程序"](https://dev.botframework.com/bots)自动程序仪表板"页上的"详细信息 **"** 下，复制自动程序 Microsoft **应用 ID。**
  
     ![获取机器人的 AppID](~/assets/images/bots_appid_botframework.png)
  
   * 在"Microsoft Teams"**窗格中，选择**"添加 **聊天"** 图标。 For **To:**, paste your bot's Microsoft App ID.
  
     ![上传机器人的 AppID](~/assets/images/bots_uploading.png)

     应用 ID 应解析为自动程序名称。

   * 选择自动程序并发送消息以启动对话。
   * 或者，你可以将机器人的应用 ID 粘贴到搜索框左上方的搜索框中Microsoft Teams。 在搜索结果页面中，导航到"人员"选项卡以查看自动程序并开始与它聊天。

机器人将像添加到团队的机器人一样接收事件，但 `conversationUpdate` 对象中不会包含团队 `channelData` 信息。

## <a name="blocking-a-bot-in-personal-chat"></a>阻止个人聊天中的机器人

请注意，用户可以选择阻止机器人发送个人聊天消息。 他们可通过右键单击聊天频道中的机器人并选择"阻止机器人对话" **来切换此模式**。 这意味着自动程序将继续发送消息，但用户不会收到这些消息。

![阻止机器人](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a>从团队中删除机器人

用户可以通过在团队视图中选择机器人列表上的"回收站"图标来删除机器人。 请注意，这只会从该团队的使用中删除自动程序，单个用户可以在个人上下文中交互。

用户无法禁用或删除个人上下文中的自动程序，但无法从用户Teams。

## <a name="disabling-a-bot-in-teams"></a>禁用聊天机器人Teams

若要停止机器人接收消息，请转到自动程序仪表板并编辑Microsoft Teams通道。 清除"**启用Microsoft Teams** 选项。 这将阻止用户与机器人交互，但仍可以发现它，并且用户可以将其添加到团队。

## <a name="deleting-a-bot-from-teams"></a>从聊天机器人中删除Teams

若要从自动程序完全Teams，请转到自动程序仪表板并编辑Microsoft Teams通道。 选择底部的 **"删除** "按钮。 这将阻止用户发现、添加或与机器人交互。 请注意，这不会将机器人从其他用户Teams中删除，尽管它也将停止运行。

## <a name="removing-your-bot-from-appsource"></a>从 AppSource 中删除机器人

如果你希望从 AppSource (Office Store) 中的 Teams 应用中删除自动程序，必须从应用清单中删除自动程序并重新提交应用进行验证。 有关详细信息，请参阅将[应用Microsoft Teams AppSource。](~/concepts/deploy-and-publish/apps-publish.md)
