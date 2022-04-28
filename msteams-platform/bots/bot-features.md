---
title: 智能机器人和 SDK
author: surbhigupta
description: 用于生成Microsoft Teams机器人的工具和 SDK 概述。
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 52f933aaddd5a02319ae1c0a35e9a4a26b617b57
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104320"
---
# <a name="bots-and-sdks"></a>智能机器人和 SDK

可以使用以下工具或功能之一创建在Microsoft Teams中工作的机器人：

* [Microsoft Bot Framework SDK](#bots-with-the-microsoft-bot-framework)
* [Power Virtual Agents](#bots-with-power-virtual-agents)
* [虚拟助理](~/samples/virtual-assistant.md)
* [Webhook 和连接器](#bots-with-webhooks-and-connectors)

## <a name="bots-with-the-microsoft-bot-framework"></a>具有Microsoft Bot Framework的机器人

Teams机器人包括以下内容：

* 由你托管的可公开访问的 Web 服务。
* Web 服务的 Bot Framework 注册。
* Teams应用包，用于将Teams客户端连接到 Web 服务。

> [!TIP]
> 使用开发人员门户将 Web 服务注册到 Bot Framework 并指定应用配置。 有关详细信息，请参阅[开发人员门户管理应用以进行Teams](~/concepts/build-and-test/teams-developer-portal.md)。

[Bot Framework](https://dev.botframework.com/) 是一种丰富的 SDK，用于使用 C#、Java、Python 和 JavaScript 创建机器人。 如果已有基于 Bot Framework 的机器人，则可以轻松修改它以在Teams中工作。 使用 C# 或Node.js利用 [SDK](/microsoftteams/platform/#pivot=sdk-tools)。 这些包扩展了基本的 Bot Builder SDK 类和方法，如下所示：

* 使用专用卡片类型，例如Office 365连接器卡。
* 设置活动Teams特定的通道数据。
* 处理消息扩展请求。

> [!IMPORTANT]
> 可以在任何 Web 编程技术中开发Teams应用，并直接调用 [Bot Framework REST API](/bot-framework/rest-api/bot-framework-rest-overview)。 但是，必须在所有情况下执行令牌处理。

## <a name="bots-with-power-virtual-agents"></a>具有Power Virtual Agents的机器人

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)是在 Microsoft Power 平台和 Bot Framework 上构建的聊天机器人服务。 Power Virtual Agent 开发过程使用引导式、无代码和图形接口方法，使团队成员能够轻松创建和维护智能虚拟代理。 在[Power Virtual Agents门户](https://powervirtualagents.microsoft.com)中创建聊天机器人后，可以轻松[地将其与Teams集成](how-to/add-power-virtual-agents-bot-to-teams.md)。 有关入门的详细信息，请[参阅Power Virtual Agents文档](/power-virtual-agents)。

>[!NOTE]
>不得使用 Microsoft Power Platform 创建要发布到Teams应用商店的应用。 Microsoft Power Platform 应用只能发布到组织的应用商店。

## <a name="bots-with-webhooks-and-connectors"></a>具有 Webhook 和连接器的机器人

Webhook 和连接器将机器人连接到 Web 服务。 使用 Webhook 和连接器，可以创建用于基本交互的机器人，例如创建工作流或其他简单命令。 它们仅在创建它们的团队中可用，适用于特定于公司工作流的简单流程。 有关详细信息，请参阅 [什么是 Webhook 和连接器](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)。

## <a name="advantages-of-bots"></a>机器人的优点

Microsoft Teams 中的机器人可以进行一对一对话、群聊或参与团队的频道。 每个范围为聊天机器人提供独特的机会和挑战。

| 在通道中 | 在群组聊天中 | 在一对一聊天中 |
| :-- | :-- | :-- |
| 大规模访问 | 成员数减少 | 传统方式 |
| 简洁的单个交互 | @mention机器人  | Q&A 机器人 |
| @mention机器人 | 类似于通道 | 讲笑话和做笔记的机器人 |

### <a name="in-a-channel"></a>在通道中

频道包含多个人员之间的线程对话，甚至最多两千个。 这可能会为机器人提供巨大的影响力，但单个交互必须简洁。 传统的多轮次交互不起作用。 相反，必须使用交互式卡片或任务模块，或将对话移动到一对一对话以收集大量信息。 机器人仅有权访问其 `@mentioned`所在的消息。 可以使用 Microsoft Graph 和组织级别权限从对话中检索其他消息。

在以下情况下，机器人在频道中效果更好：

* 通知，其中提供交互式卡片，供用户获取其他信息。
* 反馈方案，如轮询和调查。
* 单个请求或响应周期可解析交互，结果对会话的多个成员非常有用。
* 社交或有趣的机器人，在那里你得到一个真棒猫的形象，随机挑选一个赢家，等等。

### <a name="in-a-group-chat"></a>在群组聊天中

群聊是在三个及以上人员之间进行的非按线索组织的对话。 其中的成员一般比频道中的少且更短暂。 与通道类似，机器人仅有权访问直接访问的消息 `@mentioned` 。

如果机器人在频道中工作得更好，在群聊中工作也更好。

### <a name="in-a-one-to-one-chat"></a>在一对一聊天中

一对一聊天是聊天机器人与用户交互的传统方式。 一对一会话机器人的一些示例包括：

* Q&A 机器人
* 在其他系统中启动工作流的机器人
* 讲笑话的机器人
* 在创建一对一聊天机器人之前做笔记的机器人，请考虑基于聊天的接口是否是呈现功能的最佳方式。

## <a name="disadvantages-of-bots"></a>机器人的缺点

机器人与用户之间广泛对话是完成任务的一种缓慢而复杂的方法。 支持过多命令（尤其是各种命令）的机器人不会成功或被用户积极查看。

### <a name="have-multi-turn-experiences-in-chat"></a>在聊天中具有多轮次体验

广泛的对话需要开发人员保持状态。 若要退出此状态，用户必须超时或选择 **“取消**”。 此外，这个过程也是繁琐的。 例如，请参阅以下对话方案：

用户：安排与 Megan 的会议。

机器人：我发现了200个结果，请包括名字和姓氏。

用户：安排与梅根·鲍文的会议。

机器人：好吧，你想在什么时间与梅根·鲍文见面？

用户：下午 1：00。

机器人：哪一天？

### <a name="support-too-many-commands"></a>支持过多的命令

由于当前机器人菜单中只有 6 个可见命令，因此不太可能以任何频率使用其他命令。 深入到特定区域的机器人，而不是试图成为一个广泛的助理工作和票价更好。

### <a name="maintain-a-large-knowledge-base"></a>维护大型知识库

机器人的缺点之一是很难使用未分段的响应来维护大型检索知识库。 机器人最适合进行简短、快速的交互，而不筛选寻找答案的长列表。

## <a name="code-snippets"></a>代码段

以下代码提供了频道团队范围的机器人活动的示例：

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

以下代码提供了一对一聊天的机器人活动示例：

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

|示例名称 | Description | .NETCore | Node.js | Python|
|----------------|-----------------|--------------|----------------|-------|
| Teams 对话自动程序 | 消息传送和会话事件处理。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot)|
| 机器人示例 | 机器人示例集 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore) |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python)|

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [智能机器人活动处理程序](~/bots/bot-basics.md)

## <a name="see-also"></a>另请参阅

* [通话和会议机器人](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)
* [智能机器人对话](~/bots/how-to/conversations/conversation-basics.md)
* [机器人命令菜单](~/bots/how-to/create-a-bot-commands-menu.md)
* [Microsoft Teams中机器人的身份验证流](~/bots/how-to/authentication/auth-flow-bot.md)
* [使用机器人的任务模块](~/task-modules-and-cards/task-modules/task-modules-bots.md)
