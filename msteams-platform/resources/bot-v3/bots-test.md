---
title: 测试和调试机器人
description: 在本文中，你将了解如何在Microsoft Teams中测试和调试机器人，并在不上传到Teams
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 03/20/2019
ms.openlocfilehash: 71045071666ecc21cdc376590deef90223694d15
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189752"
---
# <a name="test-and-debug-your-microsoft-teams-bot"></a>测试和调试 Microsoft Teams 机器人

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

测试机器人时，必须同时考虑上下文 () 希望机器人运行，以及可能已添加到机器人的任何功能，这些功能需要特定于Microsoft Teams的数据。 确保你选择测试机器人的方法与其功能一致。

## <a name="test-by-uploading-to-teams"></a>通过上传到 Teams 进行测试

测试机器人的最全面方法是创建应用包并将其上传到 Teams。 这是测试机器人在所有范围内可用的完整功能的唯一方法。

有两种方法用于上传应用。 可以使用 [App Studio](~/concepts/build-and-test/app-studio-overview.md)，也可以手动[创建应用包](~/concepts/build-and-test/apps-package.md)并[上传应用](~/concepts/deploy-and-publish/apps-upload.md)。 如果需要更改清单并重新加载应用，应先 [删除机器人](#deleting-a-bot-from-teams) ，然后再上传已更改的应用包。

## <a name="debug-your-bot-locally"></a>在本地调试机器人

如果在开发期间在本地托管机器人，则需要使用 [ngrok](https://ngrok.com/) 等隧道服务来测试机器人。 下载并安装 ngrok 后，运行以下命令以启动隧道服务。 可能需要将 ngrok 添加到路径。

```bash
ngrok http <port> -host-header=localhost:<port>
```

使用应用清单中 ngrok 提供的 https 端点。 如果关闭命令窗口并重新启动，你将获得一个新的 URL，并且还需要更新机器人终结点地址才能使用该 URL。

## <a name="testing-your-bot-without-uploading-to-teams"></a>测试机器人而不上传到 Teams

有时需要测试机器人，而无需将其作为应用安装到 Teams 中。 我们提供了两种测试方法。 在不将其安装为应用的情况下测试机器人对于确保机器人可用和响应非常有用，但不允许你测试可能已添加到机器人的Teams功能的完整广度。 如果需要完全测试机器人，请按照[通过上传进行测试](#test-by-uploading-to-teams)说明操作。

### <a name="use-the-bot-emulator"></a>使用机器人仿真器

Bot Framework Emulator 是一个桌面应用程序，允许机器人开发人员在本地或远程测试和调试其机器人。 使用该仿真器，可以与机器人聊天并检查机器人发送和接收的消息。 这对于验证机器人是否可用并做出响应非常有用，但是模拟器不允许你测试已添加到机器人的任何特定于Teams的功能，机器人的响应也不会准确直观地表示它们在Teams中的呈现方式。 如果需要测试其中任一项，则最好不要[上传机器人](#test-by-uploading-to-teams)。

可在[此处](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)找到有关 Bot Framework Emulator 的完整说明。

### <a name="talk-to-your-bot-directly-by-id"></a>直接按 ID 与机器人交谈

>[!Important]
>按 ID 与机器人交谈仅用于测试目的。

还可以使用机器人的 ID 启动与机器人的对话。 下面提供了两种执行此操作的方法。 通过其中一种方法添加机器人时，它将无法在频道对话中寻址，并且无法利用其他Microsoft Teams应用功能，例如选项卡或消息扩展。

1. 在机器人的“[机器人仪表板](https://dev.botframework.com/bots)”页面上，在“**频道**”下，选择“**添加到 Microsoft Teams**”。 Teams将启动与机器人的个人聊天。
2. 直接从Teams中引用机器人的应用 ID：
   * 在机器人的“[机器人仪表板](https://dev.botframework.com/bots)”页面上，在“**详细信息**”下，复制机器人的“**Microsoft 应用 ID**”。
  
      :::image type="content" source="../../assets/images/bots_appid_botframework.png" alt-text="机器人仪表板":::
  
   * 在Teams内的 **“聊天**”窗格中，选择 **“添加聊天**”图标。 对于 **To:**，粘贴机器人的 Microsoft 应用 ID。
  
      :::image type="content" source="../../assets/images/bots_uploading.png" alt-text="上传机器人的 AppID"border="true":::

     应用 ID 应解析为机器人名称。

   * 选择机器人并发送消息以启动对话。

   * 或者，可以将机器人的应用 ID 粘贴到 Microsoft Teams 左上角的搜索框中。 在搜索结果页中，转到“人员”选项卡以查看机器人并开始与机器人聊天。

机器人将收到 `conversationUpdate` 事件，就像添加到团队中的机器人一样，但没有 `channelData` 对象中的团队信息。

## <a name="blocking-a-bot-in-personal-chat"></a>在个人聊天中阻止机器人

用户可以选择阻止机器人发送个人聊天消息。 他们可以通过在聊天频道中右键单击机器人并选择“**阻止机器人对话**”来进行切换。 这意味着机器人将继续发送消息，但用户不会收到这些消息。

  :::image type="content" source="../../assets/images/bots/botdisable.png" alt-text="阻止机器人"border="true":::

## <a name="removing-a-bot-from-a-team"></a>从团队中删除机器人

用户可以通过在其团队视图中的机器人列表中选择垃圾桶图标来删除机器人。 请注意，这只会从该团队的使用中删除机器人，单个用户可以在个人上下文中进行交互。

用户无法禁用或删除个人上下文中的机器人，无法从Teams中完全删除机器人。

## <a name="disabling-a-bot-in-teams"></a>在 Teams 中禁用机器人

若要停止机器人接收消息，请转到“机器人仪表板”并编辑 Microsoft Teams 通道。 清除”**在 Microsoft Teams 上启用**”选项。 这会阻止用户与机器人交互，但它仍是可发现的，并且用户可以将其添加到团队。

## <a name="deleting-a-bot-from-teams"></a>从 Teams 中删除机器人

若要从 Teams 中完全删除机器人，请转到“机器人仪表板”并编辑 Microsoft Teams 通道。 选择底部的”**删除**”按钮。 这会阻止用户发现、添加机器人或与机器人交互。 这不会从其他用户的Teams实例中删除机器人，尽管它也会停止为其运行。

## <a name="removing-your-bot-from-appsource"></a>从 AppSource 中删除机器人

如果要在 AppSource（以前称为 Office 应用商店）中从 Teams 应用删除机器人，则必须从应用清单中删除机器人并重新提交应用以进行验证。 有关详细信息，请参阅[将 Microsoft Teams 应用发布到 AppSource](~/concepts/deploy-and-publish/apps-publish.md)。
