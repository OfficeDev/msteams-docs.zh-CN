---
title: 在本地测试和调试机器人
author: surbhigupta
description: 了解如何通过旁加载、使用机器人模拟器Teams外部以及直接与机器人交谈，在Teams环境中使用 IDE 在本地测试和调试机器人。
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: a673f1cd260c9b53de477cdd5084bd521c79bd41
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103984"
---
# <a name="test-and-debug-your-bot-locally"></a>在本地测试和调试机器人

测试机器人时，需要同时考虑希望机器人运行的上下文，以及可能已添加到需要特定于Microsoft Teams数据的机器人的任何功能。 确保选择测试机器人的方法与其功能一致。

## <a name="test-by-uploading-to-teams"></a>通过上传到Teams进行测试

测试机器人的最全面方法是创建应用包并将其上传到Teams。 这是测试机器人在所有范围内可用的完整功能的唯一方法。

上传应用有两种方法：

* 使用 [App Studio](~/concepts/build-and-test/app-studio-overview.md)。
* 手动[创建应用包](~/concepts/build-and-test/apps-package.md)，然后[上传应用](~/concepts/deploy-and-publish/apps-upload.md)。

> [!NOTE]
> 若要更改清单并重新上传应用，请在上传已更改的应用包之前 [删除机器人](#delete-a-bot-from-teams) 。
> 若要测试机器人，请在Teams中启用旁加载。 请参阅 [启用旁加载](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。

## <a name="debug-your-bot-locally"></a>在本地调试机器人

如果在开发期间在本地托管机器人，则需要使用 [ngrok](https://ngrok.com/) 等隧道服务来测试机器人。 下载并安装 ngrok 后，添加 `ngrok` 到路径，并运行以下命令以启动隧道服务：

```bash
ngrok http <port> -host-header=localhost:<port>
```

使用应用清单中 ngrok 提供的 https 终结点。

> [!NOTE]
> 如果关闭命令窗口并重新启动，则会生成新的 URL，并且需要更新机器人终结点地址才能使用它。

## <a name="test-your-bot-without-uploading-to-teams"></a>在不上传到Teams的情况下测试机器人

有时，可能需要测试机器人，而无需将其安装为Teams中的应用。 我们提供了两种测试机器人的方法。 在不将其安装为应用的情况下测试机器人对于确保机器人可用并做出响应非常有用，但不允许你测试可能已添加到机器人的Microsoft Teams功能的完整广度。 如果需要完全测试机器人，请 [通过上传查看测试](#test-by-uploading-to-teams)。

### <a name="use-the-bot-emulator"></a>使用机器人Emulator

Bot Framework Emulator是一个桌面应用程序，允许机器人开发人员在本地或远程测试和调试机器人。 模拟器可帮助你与机器人聊天，并检查机器人发送和接收的消息。 这对于验证机器人是否可用并做出响应非常有用。 但是，模拟器不允许你测试添加到机器人的任何特定于Teams功能，机器人的响应也无法准确直观地表示它们在Teams中的呈现方式。 如果需要测试其中任一项内容，最好 [上传机器人](#test-by-uploading-to-teams)。

有关详细信息，请参阅[有关Bot Framework Emulator的完整说明](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)。

### <a name="talk-to-your-bot-directly-by-id"></a>直接通过 ID 与机器人通信

> [!Important]
> 按 ID 与机器人交谈仅用于基本测试目的。 添加到机器人的任何特定Teams功能都无法正常工作。

还可以使用机器人的 ID 启动与机器人的对话。 通过这些方法之一添加机器人时，无法在频道对话中寻址，并且无法利用其他Microsoft Teams应用功能（如选项卡或消息扩展）。 可以通过以下方式之一启动对话：

* 在 [机器人的“机器人仪表板](https://dev.botframework.com/bots)”页上的 **“通道**”下，选择 **“添加到Microsoft Teams**”。 Microsoft Teams启动与机器人的个人聊天。

* 直接从Microsoft Teams中引用机器人的应用 ID：
   1. 在 [机器人的“机器人仪表板](https://dev.botframework.com/bots) ”页上的 **“详细信息**”下，复制机器人的 **Microsoft 应用 ID** 。
  
      ![获取机器人的 AppID](~/assets/images/bots_appid_botframework.png)
  
   2. 打开Microsoft Teams，在 **“聊天**”窗格上，选择 **“添加聊天**”图标。 在 **To：** 中，粘贴机器人的 Microsoft 应用 ID。
  
      ![上传机器人](~/assets/images/bots_uploading.png)

      应用 ID 必须解析为机器人名称。

   3. 选择机器人并发送消息以启动对话。
      或者，可以将机器人的应用 ID 粘贴到Microsoft Teams左上角的搜索框中。 在搜索结果页中，导航到 **“人员”** 选项卡以查看机器人并开始与机器人聊天。

> [!Note]
> 若要Microsoft Teams引用机器人的应用 ID，请启用[应用旁加载](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。

机器人在将机器人添加到团队时接收 `conversationUpdate` 事件，但对象中 `channelData` 没有团队信息。

## <a name="block-a-bot-in-personal-chat"></a>在个人聊天中阻止机器人

用户可以选择阻止机器人发送个人聊天消息。 他们可以通过在聊天通道中右键单击机器人并选择 **“阻止机器人对话**”来切换此问题。 这意味着机器人继续发送消息，但是用户不会收到消息。

![阻止机器人](~/assets/images/bots/botdisable.png)

## <a name="remove-a-bot-from-a-team"></a>从团队中删除机器人

用户可以通过在团队视图中的机器人列表中选择垃圾桶图标来删除机器人。 这只会从该团队的使用中删除机器人，单个用户仍然可以在个人上下文中进行交互。 用户不能禁用或删除个人上下文中的机器人。

## <a name="disable-a-bot-in-teams"></a>在 Teams 中禁用机器人

若要阻止机器人接收消息，请转到 **机器人仪表板** 并编辑Microsoft Teams通道。 清除 **“启用Microsoft Teams**”选项。 这会阻止用户与机器人交互，但是，它仍可发现，并且用户仍能够将其添加到Teams。

## <a name="delete-a-bot-from-teams"></a>从Teams中删除机器人

若要从Teams中完全删除机器人，请转到 **机器人仪表板** 并编辑Microsoft Teams通道。 选择底部的 **“删除”** 按钮。 这会阻止用户发现、添加机器人并与机器人交互。 这不会从其他用户的Teams实例中删除机器人，但是，它也会停止为它们运行。

## <a name="see-also"></a>另请参阅

* [使用检查中间件调试机器人](/azure/bot-service/bot-service-debug-inspection-middleware)
* [在本地调试呼叫和会议机器人](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
