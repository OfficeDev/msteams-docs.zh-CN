---
title: 在本地测试和调试机器人
author: surbhigupta
description: 了解如何使用 Teams 环境中的 IDE 通过旁加载、在 Teams 外部使用机器人仿真器以及直接与机器人交谈来在本地测试和调试机器人。
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 1c0c2124c12e9ab13bf72008e8dda0846f35d768
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757596"
---
# <a name="test-and-debug-your-bot-locally"></a>在本地测试和调试机器人

测试机器人时，需要考虑希望机器人运行的上下文，以及可能已添加到机器人的任何功能，这些功能需要特定于Microsoft Teams的数据。 确保选择测试机器人的方法与其功能一致。

## <a name="test-by-uploading-to-teams"></a>通过上传到 Teams 进行测试

测试机器人的最全面方法是创建应用包并将其上传到 Teams。 这是测试机器人在所有范围内可用的完整功能的唯一方法。

有两种方法用于上传应用：

* 使用 [App Studio](~/concepts/build-and-test/app-studio-overview.md)。
* 手动[创建应用包](~/concepts/build-and-test/apps-package.md)，然后[上传应用](~/concepts/deploy-and-publish/apps-upload.md)。

> [!NOTE]
> 若要更改清单并重新上传应用，请在上传已更改的应用包之前[删除机器人](#delete-a-bot-from-teams)。
> 若要测试机器人，请在 Teams 中启用旁加载。 请参阅[启用旁加载](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。

## <a name="debug-your-bot-locally"></a>在本地调试机器人

如果在开发期间在本地托管机器人，则需要使用 [ngrok](https://ngrok.com/) 等隧道服务来测试机器人。 下载并安装 ngrok 后，将 `ngrok` 添加到路径，然后运行以下命令以启动隧道服务：

```bash
ngrok http <port> --host-header=localhost:<port>
```

在应用清单中使用由 ngrok 提供的 https 终结点。

> [!NOTE]
> 如果关闭命令窗口并重新启动，将生成一个新的 URL，你需要更新机器人终结点地址才能使用该 URL。

## <a name="test-your-bot-without-uploading-to-teams"></a>在不上传到 Teams 的情况下测试机器人

有时需要测试机器人，而无需将其作为应用安装到 Teams 中。 我们提供了两种测试机器人的方法。 测试机器人而不将其安装为应用可能非常有用，可确保机器人可用并响应。 但是，它不允许你测试已添加到机器人的Microsoft Teams功能的完整广度。 若要全面测试机器人，请参阅[通过上传进行测试](#test-by-uploading-to-teams)。

### <a name="use-the-bot-emulator"></a>使用机器人仿真器

Bot Framework Emulator 是一个桌面应用程序，允许机器人开发人员在本地或远程测试和调试其机器人。 该仿真器可帮助你与机器人聊天并检查机器人发送和接收的消息。 这对于验证机器人是否可用并做出响应非常有用。 但是，该仿真器不允许你测试已添加到机器人的任何特定于 Teams 的功能，机器人的响应也无法准确直观地表现它们在 Teams 中的呈现方式。 如果需要测试其中任一项，则最好[上传机器人](#test-by-uploading-to-teams)。

有关详细信息，请参阅[有关 Bot Framework Emulator 的完整说明](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)。

### <a name="talk-to-your-bot-directly-by-id"></a>直接通过 ID 与机器人交谈

> [!Important]
> 通过 ID 与机器人交谈仅用于基本测试目的。 添加到机器人的任何特定于 Teams 的功能都无法正常工作。

使用机器人的 ID 启动与机器人的对话。 通过其中一种方法添加机器人后，它将无法在频道对话中寻址，你也无法利用其他 Microsoft Teams 应用功能，例如选项卡或消息扩展。 通过以下方式之一启动对话：

* 在机器人的“[机器人仪表板](https://dev.botframework.com/bots)”页面上，在“**频道**”下，选择“**添加到 Microsoft Teams**”。 Microsoft Teams 将启动与机器人的个人聊天。

* 直接从 Microsoft Teams 中引用机器人的应用 ID：
   1. 在机器人的“[机器人仪表板](https://dev.botframework.com/bots)”页面上，在“**详细信息**”下，复制机器人的“**Microsoft 应用 ID**”。
  
      ![获取机器人的应用 ID](~/assets/images/bots_appid_botframework.png)
  
   2. 打开 Microsoft Teams，在“**聊天**”窗格上，选择“**添加聊天**”图标。 在“**聊天对象:**”中，粘贴机器人的 Microsoft 应用 ID。
  
      ![上传机器人](~/assets/images/bots_uploading.png)

      应用 ID 必须解析为机器人名称。

   3. 选择机器人并发送消息以发起对话。
      或者，可以将机器人的应用 ID 粘贴到 Microsoft Teams 左上角的搜索框中。 在搜索结果页中，转到“**人员**”选项卡以查看机器人并开始与机器人聊天。

> [!Note]
> 若要让 Microsoft Teams 引用机器人的应用 ID，请启用“[应用旁加载](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)”。

将机器人添加到团队时，机器人会收到 `conversationUpdate` 事件，而 `channelData` 对象中没有团队信息。

## <a name="block-a-bot-in-personal-chat"></a>在个人聊天中阻止机器人

用户可以选择阻止机器人发送个人聊天消息。 他们可以通过在聊天频道中右键单击机器人并选择“**阻止机器人对话**”来进行切换。 这意味着机器人继续发送消息，但是用户不会收到消息。

![阻止机器人](~/assets/images/bots/botdisable.png)

## <a name="remove-a-bot-from-a-team"></a>从团队中删除机器人

用户可以通过在其团队视图中的机器人列表中选择垃圾桶图标来删除机器人。 这只会从该团队的使用中删除机器人。 单个用户仍然可以在个人上下文中进行交互。 用户无法禁用或删除个人上下文中的机器人。

## <a name="disable-a-bot-in-teams"></a>在 Teams 中禁用机器人

若要阻止机器人接收消息，请转到“**机器人仪表板**”并编辑 Teams 频道。 清除”**在 Microsoft Teams 上启用**”选项。 这会阻止用户与机器人交互，但它仍是可发现的，并且用户仍可以将其添加到 Teams。

## <a name="delete-a-bot-from-teams"></a>从 Teams 中删除机器人

若要从 Teams 中完全删除机器人，请转到“**机器人仪表板**”并编辑 Teams 频道。 选择底部的“**删除**”按钮。 这会阻止用户发现、添加机器人和与机器人交互。 这不会从其他用户的 Teams 实例中删除机器人，但是，它会停止为用户运行。

## <a name="see-also"></a>另请参阅

* [使用检查中间件调试机器人](/azure/bot-service/bot-service-debug-inspection-middleware)
* [在本地调试呼叫和会议机器人](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
