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
# <a name="test-and-debug-your-bot-locally"></a>在本地测试和调试你的 bot

测试你的 bot 时，需要考虑要在其上运行你的 bot 的上下文，以及你可能已添加到你的 bot 中的、需要 Microsoft 团队专用数据的任何功能。 请确保你选择的用于测试你的 bot 的方法与其功能保持一致。

## <a name="test-by-uploading-to-teams"></a>通过上传到团队进行测试

若要测试你的 bot，最全面的方法是创建一个应用包并将其上传到团队。 这是在所有作用域中测试自动程序可用的完整功能的唯一方法。

有两种方法可用于上载应用程序。 您可以使用[应用程序 Studio](~/concepts/build-and-test/app-studio-overview.md)来帮助您，也可以手动[创建应用程序包](~/concepts/build-and-test/apps-package.md)并[上传应用程序](~/concepts/deploy-and-publish/apps-upload.md)。 如果需要更改清单并重新上载您的应用程序，则应在上载更改的应用程序包之前[删除你的 bot](#deleting-a-bot-from-teams) 。

## <a name="debug-your-bot-locally"></a>在本地调试你的 bot

如果你在开发过程中将你的 bot 托管在本地，则需要使用隧道服务（如[ngrok](https://ngrok.com/) ）来测试你的 bot。 下载并安装 ngrok 后，运行以下命令以启动隧道服务（您可能需要向路径中添加 ngrok）。

```bash
ngrok http <port> -host-header=localhost:<port>
```

在应用程序清单中使用 ngrok 提供的 https 终结点。 如果关闭命令窗口并重新启动，则会收到一个新的 URL，您需要将你的 bot 终结点地址更新为同时使用该地址。

## <a name="testing-your-bot-without-uploading-to-teams"></a>在不上载到团队的情况下测试你的机器人

有时，您可能需要测试您的 bot，而无需将其作为团队中的应用程序进行安装。 我们提供了两种方法来实现此目的。 测试您的 bot 而不将其安装为应用程序可确保你的 bot 可用并做出响应，但不允许你测试你可能已添加到你的 bot 的 Microsoft 团队功能的全部广度。 如果需要完全测试你的 bot，请按照[上传](#test-by-uploading-to-teams)说明进行测试。

### <a name="use-the-bot-emulator"></a>使用机器人仿真程序

Bot 框架仿真程序是一种桌面应用程序，它允许 Bot 开发人员在本地或远程测试和调试自己的 bot。 使用模拟器，可以与你的 bot 聊天并检查你的 bot 发送和接收的邮件。 这在验证你的 bot 是否可用并做出响应时非常有用，但是仿真程序不允许你测试你已添加到机器人的任何团队特定的功能，也不会从你的 bot 中的响应准确直观地表示它们将如何在团队中呈现。 如果你需要测试这些内容中的任何一个，最好[上载你的机器人](#test-by-uploading-to-teams)。

可以在[此处](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0)找到机器人框架仿真程序的完整说明。

### <a name="talk-to-your-bot-directly-by-id"></a>按 Id 直接联系你的 bot

>[!Important]
>按 Id 与你的 bot 对话仅适用于基本测试目的。 你添加到你的 bot 的任何团队特定的功能将无法工作。

此外，还可以使用你的 bot 启动与你的 bot 的对话，方法是使用其 Id。下面给出了两种执行此操作的方法。 通过其中一种方法添加机器人时，它不会在通道对话中可寻址，也不能利用其他 Microsoft 团队应用功能（如选项卡或邮件扩展）。

1. 在你的 bot 的 "[机器人仪表板](https://dev.botframework.com/bots)" 页面上的 "**频道**" 下，选择 "**添加到 Microsoft 团队**"。 Microsoft 团队将启动与你的 bot 的个人聊天。
2. 直接从 Microsoft 团队中引用你的 bot 的应用 ID：
   * 在你的 bot 的 " [Bot 仪表板](https://dev.botframework.com/bots)" 页面上，在 "**详细信息**" 下，复制你的 BOT 的**Microsoft 应用 ID** 。
  
     ![获取 bot 的 AppID](~/assets/images/bots_appid_botframework.png)
  
   * 在 Microsoft 团队中，在**聊天**窗格中，选择 "**添加聊天**" 图标。 对于 **：**，请粘贴你的 Bot 的 MICROSOFT 应用 ID。
  
     ![获取 bot 的 AppID](~/assets/images/bots_uploading.png)

     应用 ID 应解析为你的 bot 名称。

   * 选择你的 bot 并发送一封邮件以启动对话。
   * 或者，可以将你的 bot 的应用 ID 粘贴到 Microsoft 团队中左上角的搜索框中。 在 "搜索结果" 页上，导航到 "人员" 选项卡以查看你的 bot 并开始与之聊天。

你的 bot 将接收`conversationUpdate`事件，就像添加到团队中的 bot 一样，但没有`channelData`对象中的团队信息。

## <a name="blocking-a-bot-in-personal-chat"></a>阻止个人聊天中的 bot

请注意，用户可以选择阻止你的 bot 发送个人聊天消息。 他们可以通过右键单击聊天频道中的 bot 并选择 "**阻止机器人对话**" 来切换此功能。 这意味着你的 bot 将继续发送邮件，但用户将不会收到这些邮件。

![阻止 bot](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a>从团队中删除机器人

用户可以通过在其 "团队" 视图中的 "bot" 列表中选择垃圾桶图标来删除机器人。 请注意，这只会从该团队使用中删除机器人;单个用户将仍能够在个人上下文中进行交互。

个人上下文中的 bot 不能被用户禁用或删除，而是从团队完全删除机器人的短时间。

## <a name="disabling-a-bot-in-teams"></a>在团队中禁用机器人

若要停止你的 bot 接收邮件，请转到你的机器人仪表板并编辑 Microsoft 团队频道。 清除 "**在 Microsoft 团队中启用**" 选项。 这样可以防止用户与 bot 交互，但仍然可以发现，用户仍可以将其添加到团队。

## <a name="deleting-a-bot-from-teams"></a>从团队中删除机器人

若要从团队中完全删除你的 bot，请转到你的机器人仪表板并编辑 Microsoft 团队频道。 选择底部的 "**删除**" 按钮。 这样可以防止用户发现、添加或与你的 bot 进行交互。 请注意，这不会从其他用户的团队实例中删除机器人，尽管它也会停止运行。
