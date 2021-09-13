---
title: 在本地测试和调试机器人
author: surbhigupta
description: 使用 IDE 在本地测试和调试机器人
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: a143830ad32b42e9613011b3f08cfb9afd838f26
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155684"
---
# <a name="test-and-debug-your-bot-locally"></a>在本地测试和调试机器人

测试自动程序时，需要考虑希望自动程序运行的环境，以及你已添加到自动程序（需要特定于自动程序的数据）Microsoft Teams。 确保你选择用于测试机器人的方法与它的功能一致。

## <a name="test-by-uploading-to-teams"></a>通过上传到网站进行测试Teams

测试自动程序最全面的方式是创建应用包并将其上传到Teams。 这是在所有范围内测试自动程序可用的完整功能的唯一方法。

有两种上传应用的方法：
* 使用 [App Studio](~/concepts/build-and-test/app-studio-overview.md)。
* [手动创建应用](~/concepts/build-and-test/apps-package.md) 包，然后 [上传应用](~/concepts/deploy-and-publish/apps-upload.md)。

> [!NOTE]
> 如果你需要更改清单并重新上传应用，则必须在上传已更改的应用包之前删除[](#delete-a-bot-from-teams)自动程序。

## <a name="debug-your-bot-locally"></a>在本地调试机器人

如果你在开发期间在本地托管机器人，则需要使用 [类似 ngrok](https://ngrok.com/) 的隧道服务来测试机器人。 下载并安装 ngrok 后，添加到您的路径，然后运行 `ngrok` 以下命令以启动隧道服务：

```bash
ngrok http <port> -host-header=localhost:<port>
```

在应用清单中，使用 ngrok 提供的 https 终结点。 

> [!NOTE]
> 如果关闭命令窗口并重新启动，将生成一个新 URL，并且你需要更新自动程序终结点地址才能使用它。

## <a name="test-your-bot-without-uploading-to-teams"></a>在不上载到自动程序的情况下测试Teams

有时，可能需要测试自动程序，而无需将其安装为 Teams。 我们提供两种测试自动程序的方法。 在不将机器人安装为应用的情况下测试它对于确保自动程序可用并做出响应非常有用，但是它不允许你测试可能已添加到自动程序的全部 Microsoft Teams 功能。 如果你需要完全测试自动程序，请参阅 [通过上传 进行测试](#test-by-uploading-to-teams)。

### <a name="use-the-bot-emulator"></a>使用自动程序Emulator

此Bot Framework Emulator是一个桌面应用程序，允许机器人开发人员在本地或远程测试和调试其机器人。 仿真器可帮助你与机器人聊天并检查机器人发送和接收的消息。 这可用于验证自动程序是否可用并做出响应。 但是，仿真器不允许测试已添加到自动Teams的任何特定于 Teams 的功能，来自自动程序的响应也不能准确地直观地表示它们在 Teams 中的呈现方式。 如果你需要测试其中任一内容，最好上传 [自动程序](#test-by-uploading-to-teams)。

有关详细信息，请参阅上[的完整说明Bot Framework Emulator。](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)

### <a name="talk-to-your-bot-directly-by-id"></a>直接通过 ID 与机器人交谈

> [!Important]
> 通过 ID 与机器人交谈仅用于基本测试目的。 添加到Teams的任何特定于自动程序的功能都无法正常工作。

您还可以使用自动程序 ID 启动对话。 通过这些方法之一添加自动程序后，将无法在频道对话中解决它，并且你无法利用其他 Microsoft Teams 应用功能，如选项卡或消息传递扩展。 可以通过以下方法之一启动对话：

* 在机器人 [的"](https://dev.botframework.com/bots)自动程序仪表板"页上的"频道 **"** 下，选择"添加到 **Microsoft Teams"。** Microsoft Teams聊天机器人启动个人聊天。

* 直接在应用中引用自动程序Microsoft Teams：
   1. 在 [自动程序"](https://dev.botframework.com/bots)自动程序仪表板"页上的"详细信息 **"** 下，复制自动程序 Microsoft **应用 ID。**
  
      ![获取机器人的 AppID](~/assets/images/bots_appid_botframework.png)
  
   2. 打开Microsoft Teams，**在"聊天**"窗格中，选择"**添加聊天"** 图标。 在 **"To："** 中，粘贴机器人的 Microsoft 应用 ID。
  
      ![上传机器人](~/assets/images/bots_uploading.png)

      应用 ID 必须解析为自动程序名称。

   3. 选择自动程序并发送消息以启动对话。
      或者，你可以将机器人的应用 ID 粘贴到搜索框左上方的搜索框中Microsoft Teams。 在搜索结果页面中，导航到"人员" **选项卡以查看** 自动程序并开始与它聊天。

在将机器人添加到团队时，自动程序将接收事件，而对象 `conversationUpdate` 中未包含团队 `channelData` 信息。

## <a name="block-a-bot-in-personal-chat"></a>在个人聊天中阻止聊天机器人

用户可以选择阻止机器人发送个人聊天消息。 他们可通过右键单击聊天频道中的机器人并选择"阻止机器人对话" **来切换此模式**。 这意味着，自动程序将继续发送消息，但是用户不会收到这些消息。

![阻止机器人](~/assets/images/bots/botdisable.png)

## <a name="remove-a-bot-from-a-team"></a>从团队中删除机器人

用户可以通过在团队视图中选择机器人列表上的"回收站"图标来删除机器人。 这仅从该团队的使用中删除自动程序，单个用户仍可在个人上下文中交互。 用户无法禁用或删除个人上下文中的聊天机器人。

## <a name="disable-a-bot-in-teams"></a>禁用自动程序Teams

若要阻止机器人接收消息，**请转到自动程序** 仪表板并编辑Microsoft Teams通道。 清除"**启用Microsoft Teams** 选项。 这将阻止用户与机器人交互，但是，它仍然可发现，并且用户仍将能够将其添加到Teams。

## <a name="delete-a-bot-from-teams"></a>从用户中删除Teams

若要从自动程序完全Teams，**请转到自动程序** 仪表板并编辑Microsoft Teams通道。 选择底部的 **"删除** "按钮。 这将阻止用户发现、添加机器人并与其交互。 这不会将机器人从其他用户的 Teams实例中删除，但会停止为它们运行。

## <a name="see-also"></a>另请参阅

* [使用检查中间件调试机器人](/azure/bot-service/bot-service-debug-inspection-middleware)
* [在本地调试呼叫和会议机器人](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
