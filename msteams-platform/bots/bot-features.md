---
title: 智能机器人和 SDK
author: surbhigupta
description: 用于构建自动程序的工具和 SDK Microsoft Teams概述。
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 1818ebfa102ce55d8243c16f460fa688fc67fdc3
ms.sourcegitcommit: 4abb9ca0b0e9661c7e2e329d9f10bad580e7d8f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2022
ms.locfileid: "64464766"
---
# <a name="bots-and-sdks"></a>智能机器人和 SDK

可以使用以下工具或功能之Microsoft Teams创建适用于以下工具或功能的聊天机器人：

* [Microsoft Bot Framework SDK](#bots-with-the-microsoft-bot-framework)
* [Power Virtual Agents](#bots-with-power-virtual-agents)
* [虚拟助理](~/samples/virtual-assistant.md)
* [Webhook 和连接器](#bots-with-webhooks-and-connectors)

## <a name="bots-with-the-microsoft-bot-framework"></a>具有自动程序Microsoft Bot Framework

你的Teams自动程序由以下内容组成：

* 由你托管的可公开访问的 Web 服务。
* Web 服务的自动程序框架注册。
* 你的Teams应用程序包，可将Teams客户端连接到 Web 服务。

> [!TIP]
> 使用开发人员门户向 Bot Framework 注册 Web 服务并指定应用配置。 有关详细信息，请参阅使用开发人员门户[管理应用Teams](~/concepts/build-and-test/teams-developer-portal.md)。

Bot [Framework](https://dev.botframework.com/) 是一个丰富的 SDK，用于创建使用 C#、Java、Python 和 JavaScript 的聊天机器人。 如果你已有基于 Bot Framework 的自动程序，你可以轻松修改它以在 Teams。 使用 C# 或 Node.js 来利用 [我们的 SDK](/microsoftteams/platform/#pivot=sdk-tools)。 这些包扩展基本 Bot Builder SDK 类和方法，如下所示：

* 使用专用卡类型，如Office 365卡。
* 在Teams设置特定于频道的数据。
* 处理邮件扩展请求。

> [!IMPORTANT]
> 你可以以任何Teams技术开发应用，并直接调用 [Bot Framework REST API](/bot-framework/rest-api/bot-framework-rest-overview)。 但是，你必须在所有情况下执行令牌处理。

## <a name="bots-with-power-virtual-agents"></a>具有自动程序Power Virtual Agents

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)是在 Microsoft Power 平台和 Bot Framework 上构建的聊天机器人服务。 Power Virtual Agent 开发过程使用引导式无代码和图形界面方法，使团队成员能够轻松创建和维护智能虚拟代理。 在 Power Virtual Agents 门户[创建聊天](https://powervirtualagents.microsoft.com)机器人后，可以轻松地[将其与](how-to/add-power-virtual-agents-bot-to-teams.md)Teams。 有关入门信息，请参阅Power Virtual Agents[文档](/power-virtual-agents)。

>[!NOTE]
>不得使用 Microsoft Power Platform 创建要发布到应用商店Teams应用。 Microsoft Power Platform 应用只能发布到组织的应用商店。

## <a name="bots-with-webhooks-and-connectors"></a>具有 Webhook 和连接器的机器人

Webhook 和连接器将机器人连接到 Web 服务。 使用 webhook 和连接器，可以创建用于基本交互的自动程序，例如创建工作流或其他简单命令。 它们仅在创建它们的团队中可用，并且适用于特定于公司工作流的简单流程。 有关详细信息，请参阅 [什么是 Webhook 和连接器](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)。

## <a name="advantages-of-bots"></a>自动程序的优点

Microsoft Teams 中的机器人可以进行一对一对话、群聊或参与团队的频道。 每个范围都为对话机器人提供了独特的机遇与挑战。

| 在频道中 | 在群聊中 | 在一对一聊天中 |
| :-- | :-- | :-- |
| 大规模覆盖 | 成员更少 | 传统方式 |
| 简洁的单个交互 | @mention自动程序  | Q&A bots |
| @mention自动程序 | 类似于频道 | 告知小人并做笔记的机器人 |

### <a name="in-a-channel"></a>在频道中

频道包含多个人员之间的线程对话，甚至最多包含两千个。 这可能会导致自动程序大规模访问，但个人交互必须简洁。 传统的多向交互不起作用。 相反，必须查找使用交互式卡片或任务模块，或将对话移动到一对一对话以收集大量信息。 自动程序仅有权访问其为 的邮件 `@mentioned`。 您可以使用 Microsoft 权限和组织级别权限从Graph检索其他邮件。

在下列情况下，自动程序在频道中效果更好：

* 通知，你提供交互式卡片供用户获取其他信息。
* 反馈方案，如投票和调查。
* 单个请求或响应周期可解析交互，并且结果对对话中的多个成员很有用。
* 社交或有趣的机器人，你可获取出色的 cat 图像，随机选择获胜方等。

### <a name="in-a-group-chat"></a>在群聊中

群聊是在三个及以上人员之间进行的非按线索组织的对话。 其中的成员一般比频道中的少且更短暂。 与频道类似，自动程序仅有权访问直接位于其中的消息 `@mentioned` 。

在机器人在频道中更好地工作的情况下，也更好地在群聊中工作。

### <a name="in-a-one-to-one-chat"></a>在一对一聊天中

一对一聊天是对话机器人与用户交互的传统方式。 一对一对话机器人的一些示例如下：

* Q&A bots
* 启动其他系统中工作流的机器人
* 告知机器人
* 在创建一对一聊天机器人之前，请考虑基于对话的界面是否是显示功能的最佳方法。

## <a name="disadvantages-of-bots"></a>机器人的缺点

自动程序与用户之间的广泛对话是完成任务的一种缓慢而复杂的方法。 支持过多命令（尤其是大量命令）的自动程序未成功，或者用户无法积极查看。

### <a name="have-multi-turn-experiences-in-chat"></a>在聊天中拥有多轮体验

一个广泛的对话框要求开发人员保持状态。 若要退出此状态，用户必须退出或选择"取消 **"**。 此外，该过程很繁琐。 例如，请参阅以下对话方案：

用户：安排与 Megan 的会议。

BOT：我找到了 200 个结果，请包含名字和姓氏。

用户：与 Megan Bowen 安排会议。

BOT：好的，你要在什么时间与 Megan Bowen 会面？

用户：下午 1：00。

BOT：哪一天？

### <a name="support-too-many-commands"></a>支持过多命令

由于当前自动程序菜单中只有六个可见命令，因此不可能以任何频率使用其他任何命令。 深入到特定领域的机器人，而不是尝试成为广泛的助手，可以更好地工作并提供更好的帮助。

### <a name="maintain-a-large-knowledge-base"></a>维护大型知识库

自动程序的缺点之一是很难维护具有未应答响应的大型检索知识库。 自动程序最适合于短而快速交互，而不是通过长列表来寻找答案。

## <a name="code-snippets"></a>代码段

以下代码提供了频道团队范围的自动程序活动示例：

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var mention = new Mention
    {
        Mentioned = turnContext.Activity.From,
        Text = $"<at>{XmlConvert.EncodeName(turnContext.Activity.From.Name)}</at>",
    };

    var replyActivity = MessageFactory.Text($"Hello {mention.Text}.");
    replyActivity.Entities = new List<Entity> { mention };

    await turnContext.SendActivityAsync(replyActivity, cancellationToken);
}

```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

this.onMessage(async (turnContext, next) => {
    const mention = {
        mentioned: turnContext.activity.from,
        text: `<at>${ new TextEncoder().encode(turnContext.activity.from.name) }</at>`,
    } as Mention;

    const replyActivity = MessageFactory.text(`Hello ${mention.text}`);
    replyActivity.entities = [mention];

    await turnContext.sendActivity(replyActivity);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});

```

---

以下代码提供了一对一聊天的自动程序活动示例：

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

// Handle message activity
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    turnContext.Activity.RemoveRecipientMention();
    var text = turnContext.Activity.Text.Trim().ToLower();
  await turnContext.SendActivityAsync(MessageFactory.Text($"Your message is {text}."), cancellationToken);
}
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript
this.onMessage(async (context, next) => {
    await context.sendActivity(MessageFactory.text("Your message is:" + context.activity.text));
    await next();
});
```

---

## <a name="code-sample"></a>代码示例

|示例名称 | Description | .NETCore | Node.js |
|----------------|-----------------|--------------|----------------|
| Teams 对话自动程序 | 消息和对话事件处理。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)|
| 机器人示例 | 自动程序示例集 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore) | |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [智能机器人活动处理程序](~/bots/bot-basics.md)

## <a name="see-also"></a>另请参阅

* [通话和会议机器人](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)
* [智能机器人对话](~/bots/how-to/conversations/conversation-basics.md)
* [自动程序命令菜单](~/bots/how-to/create-a-bot-commands-menu.md)
* [聊天机器人的身份验证Microsoft Teams](~/bots/how-to/authentication/auth-flow-bot.md)
* [使用机器人的任务模块](~/task-modules-and-cards/task-modules/task-modules-bots.md)
