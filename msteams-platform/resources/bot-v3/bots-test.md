---
title: 测试和调试机器人
description: 介绍如何在Microsoft Teams中测试机器人
keywords: teams 机器人测试
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 03/20/2019
ms.openlocfilehash: df403343aab60ebd802b4da0e871649ded8b8a7e
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103430"
---
# <a name="test-and-debug-your-microsoft-teams-bot"></a>测试和调试Microsoft Teams机器人

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

测试机器人时，需要考虑上下文 () 你希望机器人运行，以及可能已添加到机器人的任何功能，这些功能需要特定于Microsoft Teams的数据。 确保你选择测试机器人的方法与其功能一致。

## <a name="test-by-uploading-to-teams"></a>通过上传到Teams进行测试

测试机器人的最全面方法是创建应用包并将其上传到Teams。 这是测试机器人在所有范围内可用的完整功能的唯一方法。

有两种方法用于上传应用。 可以使用 [App Studio](~/concepts/build-and-test/app-studio-overview.md) ，也可以手动 [创建应用包](~/concepts/build-and-test/apps-package.md) 并 [上传应用](~/concepts/deploy-and-publish/apps-upload.md)。 如果需要更改清单并重新加载应用，应先 [删除机器人](#deleting-a-bot-from-teams) ，然后再上传已更改的应用包。

## <a name="debug-your-bot-locally"></a>在本地调试机器人

如果在开发期间在本地托管机器人，则需要使用 [ngrok](https://ngrok.com/) 等隧道服务来测试机器人。 下载并安装 ngrok 后，运行以下命令以启动隧道服务。 可能需要将 ngrok 添加到路径。

```bash
ngrok http <port> -host-header=localhost:<port>
```

使用应用清单中 ngrok 提供的 https 终结点。 如果关闭命令窗口并重新启动，你将获得一个新的 URL，并且还需要更新机器人终结点地址才能使用该 URL。

## <a name="testing-your-bot-without-uploading-to-teams"></a>测试机器人而不上传到Teams

有时需要测试机器人，而无需将其安装为Teams中的应用。 我们提供了两种测试方法。 在不将其安装为应用的情况下测试机器人对于确保机器人可用并做出响应非常有用，但不允许你测试可能已添加到机器人的Microsoft Teams功能的完整广度。 如果需要完全测试机器人，请按照说明 [上传进行测试](#test-by-uploading-to-teams)。

### <a name="use-the-bot-emulator"></a>使用机器人Emulator

Bot Framework Emulator是一个桌面应用程序，允许机器人开发人员在本地或远程测试和调试其机器人。 使用模拟器，可以与机器人聊天，并检查机器人发送和接收的消息。 这对于验证机器人是否可用并做出响应非常有用，但模拟器不允许你测试已添加到机器人的任何特定于Teams的功能，机器人的响应也不会成为在Teams中呈现这些功能的准确视觉表示形式。 如果需要测试其中任一项，则不最好 [上传机器人](#test-by-uploading-to-teams)。

可[在此](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)处找到有关Bot Framework Emulator的完整说明。

### <a name="talk-to-your-bot-directly-by-id"></a>直接通过 ID 与机器人通信

>[!Important]
>按 ID 与机器人交谈仅用于测试目的。

还可以使用机器人的 ID 启动与机器人的对话。 下面提供了两种执行此操作的方法。 通过这些方法之一添加机器人后，它将无法在频道对话中寻址，也无法利用其他Microsoft Teams应用功能，例如选项卡或消息扩展。

1. 在 [机器人的“机器人仪表板](https://dev.botframework.com/bots)”页上的 **“通道**”下，选择 **“添加到Microsoft Teams**”。 Microsoft Teams将启动与机器人进行个人聊天。
2. 直接从Microsoft Teams中引用机器人的应用 ID：
   * 在 [机器人的“机器人仪表板](https://dev.botframework.com/bots) ”页上的 **“详细信息**”下，复制机器人的 **Microsoft 应用 ID** 。
  
     ![获取机器人的 AppID](~/assets/images/bots_appid_botframework.png)
  
   * 在Microsoft Teams内的 **“聊天**”窗格中，选择 **“添加聊天**”图标。 对于 **To：**，粘贴机器人的 Microsoft 应用 ID。
  
     ![上传机器人的 AppID](~/assets/images/bots_uploading.png)

     应用 ID 应解析为机器人名称。

   * 选择机器人并发送消息以启动对话。
   * 或者，可以将机器人的应用 ID 粘贴到Microsoft Teams左上角的搜索框中。 在搜索结果页中，导航到“人员”选项卡以查看机器人并开始与机器人聊天。

机器人将收到事件， `conversationUpdate` 就像添加到团队中的机器人一样，但对象中 `channelData` 没有团队信息。

## <a name="blocking-a-bot-in-personal-chat"></a>在个人聊天中阻止机器人

请注意，用户可以选择阻止机器人发送个人聊天消息。 他们可以通过在聊天通道中右键单击机器人并选择 **“阻止机器人对话**”来切换此问题。 这意味着机器人将继续发送消息，但用户不会收到这些消息。

![阻止机器人](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a>从团队中删除机器人

用户可以通过在其团队视图中的机器人列表中选择垃圾桶图标来删除机器人。 请注意，这只会从该团队的使用中删除机器人，单个用户可以在个人上下文中进行交互。

用户无法禁用或删除个人上下文中的机器人，无法从Teams中完全删除机器人。

## <a name="disabling-a-bot-in-teams"></a>在 Teams 中禁用机器人

若要停止机器人接收消息，请转到机器人仪表板并编辑Microsoft Teams通道。 清除 **“启用Microsoft Teams**”选项。 这会阻止用户与机器人交互，但它仍可发现，并且用户可以将其添加到团队。

## <a name="deleting-a-bot-from-teams"></a>从Teams中删除机器人

若要从Teams中完全删除机器人，请转到机器人仪表板并编辑Microsoft Teams通道。 选择底部的 **“删除”** 按钮。 这会阻止用户发现、添加机器人或与机器人交互。 请注意，这不会从其他用户的Teams实例中删除机器人，尽管也会停止为其运行。

## <a name="removing-your-bot-from-appsource"></a>从 AppSource 中删除机器人

如果要从以前Office应用商店) 的 AppSource (中的Teams应用中删除机器人，则必须从应用清单中删除机器人并重新提交应用以进行验证。 有关详细信息，请参阅[将Microsoft Teams应用发布到 AppSource](~/concepts/deploy-and-publish/apps-publish.md)。
