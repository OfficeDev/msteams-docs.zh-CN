---
title: 智能机器人和 SDK
author: surbhigupta
description: 用于构建 Microsoft Teams 机器人的工具和 SDK 概述。
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 05cb93fef74d22931591b3bb077afbb785d168ad
ms.sourcegitcommit: aa95313cdab4fbf0a9f62a047ebbe6a5f1fbbf5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2022
ms.locfileid: "65602235"
---
# <a name="bots-and-sdks"></a>智能机器人和 SDK

可以使用以下工具或功能之一创建在 Microsoft Teams 中工作的机器人：

* [Microsoft Bot Framework SDK](#bots-with-the-microsoft-bot-framework)
* [Power Virtual Agents](#bots-with-power-virtual-agents)
* [虚拟助理](~/samples/virtual-assistant.md)
* [Webhook 和连接器](#bots-with-webhooks-and-connectors)
* [Azure 机器人服务](#azure-bot-service)

## <a name="bots-with-the-microsoft-bot-framework"></a>具有 Microsoft Bot Framework 的机器人

Teams 机器人包括以下内容：

* 由你主持的公共访问的 Web 服务。
* Web 服务的 Bot Framework 注册。
* Teams 应用服务包用于将 Teams 客户端连接到 Web 服务。

> [!TIP]
> 使用开发人员门户将 Web 服务注册到 Bot Framework 并指定应用配置。 有关详细信息，请参阅[通过 Teams 开发人员门户管理应用](~/concepts/build-and-test/teams-developer-portal.md)。

[Bot Framework](https://dev.botframework.com/) 是一个丰富的 SDK，用于使用 C#、Java、Python 和 JavaScript 创建机器人。 如果具有基于 Bot Framework 的机器人，则可以对其进行修改以在 Teams 中工作。 使用 C# 或 Node.js 来利用我们的 [SDK](/microsoftteams/platform/#pivot=sdk-tools)。 这些工具包拓展了基本机器人生成器 SDK 的类和方法，见如下所示：

* 使用专用卡类型，例如 Office 365 连接器卡。
* 设置与活动相关的 Teams 特定频道数据。
* 处理消息扩展请求。

> [!IMPORTANT]
> 可以在任何 Web 编程技术中开发 Teams 应用，并直接调用 [Bot Framework REST API](/bot-framework/rest-api/bot-framework-rest-overview)。 但是，在任何情况下都必须执行令牌处理。

## <a name="bots-with-power-virtual-agents"></a>具有 Power Virtual Agents 的机器人

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) 是在 Microsoft Power 平台和 Bot Framework 上构建的聊天机器人服务。 Power Virtual Agent 开发过程使用引导式、无代码和图形界面方法，使团队成员能够轻松创建和维护智能虚拟代理。 在 [Power Virtual Agents门户](https://powervirtualagents.microsoft.com)中创建聊天机器人后，可以轻松地[将其与 Teams 集成](how-to/add-power-virtual-agents-bot-to-teams.md)。 有关入门的详细信息，请参阅 [Power Virtual Agents 文档](/power-virtual-agents)。

>[!NOTE]
>不得使用 Microsoft Power Platform 创建要发布到Teams 应用商店的应用。 Microsoft Power Platform 应用只能发布到组织的应用商店。

## <a name="bots-with-webhooks-and-connectors"></a>具有 Webhook 和连接器的机器人

Webhook 和连接器将机器人连接到 Web 服务。 使用 Webhook 和连接器，可以创建用于基本交互的机器人，例如创建工作流或其他简单命令。 它们仅在创建它们的团队中可用，适用于特定于公司工作流的简单流程。 有关详细信息，请参阅[什么是 Webhook 和连接器](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)。

## <a name="azure-bot-service"></a>Azure 机器人服务

Azure 机器人服务和 Bot Framework 提供用于生成、测试、部署和管理智能机器人的工具，所有这些工具都位于一个位置。 还可以在 Azure 机器人服务中创建机器人。

> [!IMPORTANT]
> Microsoft Teams中的机器人应用程序可通过 [Azure 机器人服务](/azure/bot-service/channel-connect-teams)在GCC-High中使用。

> [!NOTE]
> * GCCH 中的机器人仅支持清单版本 v1.10。
> * 自适应卡片中的图像 URL 在 GCCH 环境中不受支持。 可以将图像 URL 替换为 Base64 编码的 DataUri。
> * Azure 政府中的机器人通道注册将预配 Web 应用机器人、应用服务 (应用服务计划) 和应用程序见解，但不支持仅在不提供应用服务)  (预配 azure 机器人服务。
>   <details>
>   <summary><b>如果只想进行机器人注册</b></summary>
>
>   * 转到资源组并手动删除未使用的资源。 例如，如果在机器人注册) 期间创建了应用服务、应用服务计划 (，如果选择在机器人注册) 期间启用应用服务，则应用程序见解 (。
>   * 还可以使用 az-cli 进行机器人注册：
>
>     1. 登录到 azure 并设置订阅 <br> 
>           &nbsp; az cloud set –name “AzureUSGovernment” <br> 
>           &nbsp; az account set –name “`subscriptionname/id`”.<br>
>     1. 创建应用注册  
>           &nbsp; az ad app create --display-name “`name`” <br> 
>           &nbsp; --password“`password`” --available-to-other-tenants.<br> 
>           应用 ID 将在此处创建。<br>
>     1. 创建机器人资源 <br>
>           &nbsp; az bot create –resource-group “`resource-group`”<br>
>           &nbsp; --appid“`appid`”<br>
>           &nbsp; --name “`botid`”<br>
>           &nbsp; --kind “registration”。<br>
>
> </details>

对于 GCCH 环境，需要使用[Azure 政府门户](https://portal.azure.us)注册机器人。

:::image type="content" source="../assets/videos/abs-bot.gif" alt-text="Azure 政府门户":::
<br>
<br>
机器人中需要对GCC-High环境进行以下更改：
<br>
<br>
<details>
<summary><b>配置更改</b></summary>

在Azure 政府门户中进行机器人注册时，请确保更新机器人配置以连接到 Azure govermnet 实例。 下面是配置详细信息：

| 配置名称 | 值 |
|----|----|
| ChannelService | `https://botframework.azure.us` |
| OAuthUrl | `https://tokengcch.botframework.azure.us` |
| ToChannelFromBotLoginUrl | `https://login.microsoftonline.us/MicrosoftServices.onmicrosoft.us` |
| ToChannelFromBotOAuthScope | `https://api.botframework.us` |
| ToBotFromChannelTokenIssuer | `https://api.botframework.us`  |
| BotOpenIdMetadata | `https://login.botframework.azure.us/v1/.well-known/openidconfiguration` |

</details>
<br>
<details>
<summary><b>更新到 appsettings.json & startup.cs</b></summary>

1. **更新 appsettings.json：**

    * 设置 `ConnectionName` 为添加到机器人的 OAuth 连接设置的名称。

    * 设置 `MicrosoftAppId` 为机器人的应用 ID，以及 `MicrosoftAppPassword` 为应用机密。
    
    根据机器人机密中的字符，可能需要 XML 转义密码。 例如，任何 ampersands (&) 都需要编码为 `&amp;`。

    ```json
    {
      "MicrosoftAppType": "",
      "MicrosoftAppId": "",
      "MicrosoftAppPassword": "",
      "MicrosoftAppTenantId": "",
      "ConnectionName": ""
    }
    ```
2. **更新 Startup.cs：**

    若要在 *非公共 Azure 云*（如政府云）或具有数据驻留的机器人中使用 OAuth，必须在 **Startup.cs** 文件中添加以下代码。
    
    ```csharp
    string uri = "<uri-to-use>";
    MicrosoftAppCredentials.TrustServiceUrl(uri);
    OAuthClientConfig.OAuthEndpoint = uri;
    ```
    
    以下 URI 之一在哪里 \<uri-to-use\> ：

    |**URI**|**说明**|
    |---|---|
    |`https://europe.api.botframework.com`|对于在欧洲具有数据驻留的公有云机器人。|
    |`https://unitedstates.api.botframework.com`|对于在美国中具有数据驻留的公有云机器人。|
    |`https://apiGCCH.botframework.azure.us`|对于美国没有数据驻留的政府云机器人。|
    |`https://api.botframework.com`|对于没有数据驻留的公有云机器人。 这是默认 URI，不需要更改 **Startup.cs**。|

3. 应将应用注册的重定向 URL 从 Azure 更新到 `https://tokengcch.botframework.azure.us/.auth/web/redirect`。

</details>

## <a name="advantages-of-bots"></a>机器人的优点

Microsoft Teams 中的机器人可以进行一对一对话、群聊或参与团队的频道。 每个范围都为聊天机器人提供了独特的机会和挑战。

| 在频道中 | 在群组聊天中 | 在一对一聊天中 |
| :-- | :-- | :-- |
| 广阔的范围 | 成员数减少 | 传统方式 |
| 简洁的个人交互 | @提及机器人  | 问答机器人 |
| @提及机器人 | 类似于频道 | 讲笑话和做笔记的机器人 |

### <a name="in-a-channel"></a>在频道中

频道包含多个人员之间的线程对话，甚至最多可达到两千人。 这可能会让机器人拥有广阔的范围，但是个人交互需要简洁。 传统的多轮交互不起作用。 可以尝试使用交互卡片或任务模块，或者如果要收集很多信息的话，也可以将对话转移到一对一模式。 机器人仅有权访问被 `@mentioned` 的消息。 可以使用 Microsoft Graph 和组织级别权限从对话中检索额外的消息。

在以下情况下，机器人在频道中效果更好：

* 通知，特别是在为用户提供交互卡以便获取额外信息时。
* 像投票和调查这样的反馈场景。
* 单个请求或响应周期可解决交互，结果对多个成员对话非常有用。
* 可以通过社交或娱乐机器人得到很棒的猫图像，随机挑选赢家等。

### <a name="in-a-group-chat"></a>在群组聊天中

群聊是在三个及以上人员之间进行的非按线索组织的对话。 其中的成员一般比频道中的少且更短暂。 与频道类似的是，机器人仅有权访问被 `@mentioned` 的消息。

如果机器人在频道中工作良好，那么在群聊中也会更好。

### <a name="in-a-one-to-one-chat"></a>在一对一聊天中

一对一聊天是对话机器人与用户进行交互的传统方式。 一对一对话机器人的一些示例包括：

* 问答机器人
* 在其他系统中启动工作流的机器人
* 讲笑话的机器人
* 在创建一对一聊天机器人之前做笔记的机器人，请考虑基于对话的界面是否能够最佳呈现功能。

## <a name="disadvantages-of-bots"></a>机器人的缺点

机器人与用户之间的广泛对话是一种完成任务的缓慢而复杂的方法。 支持过多命令（尤其是范围广泛的命令）的机器人不会成功或被用户积极查看。

### <a name="have-multi-turn-experiences-in-chat"></a>在聊天中具有多轮体验

广泛的对话需要开发人员保持状态。 要退出此状态，用户必须超时或选择 **取消**。 此外，这个过程也很繁琐。 例如，请查看以下对话方案：

用户：安排与 Megan 的会议。

机器人：我发现了 200 个结果，请包括名字和姓氏。

用户：安排与 Megan Bowen 的会面。

机器人：好吧，要在什么时间与 Megan Bowen 见面？

用户：下午 1：00。

机器人：哪一天？

### <a name="support-too-many-commands"></a>支持过多的命令

由于当前机器人菜单中只有 6 个命令，因此不太可能以任何频率使用其他命令。 深入到特定区域的机器人，而不是试图成为用途广泛的助理，工作状况和费用会更合理。

### <a name="maintain-a-large-knowledge-base"></a>维护大型知识库

机器人的缺点之一是很难使用未分级的响应来维护大型检索知识库。 机器人最适合进行简短、快速的交互，而不适合在寻找答案的长列表之间切换。

## <a name="code-snippets"></a>代码段

以下代码提供了频道团队活动范围的机器人示例：

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
| Teams 对话自动程序 | 消息传递和对话事件处理。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot)|
| 机器人示例 | 机器人示例集 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore) |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python)|

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [智能机器人活动处理程序](~/bots/bot-basics.md)

## <a name="see-also"></a>另请参阅

* [通话和会议机器人](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)
* [智能机器人对话](~/bots/how-to/conversations/conversation-basics.md)
* [机器人命令菜单](~/bots/how-to/create-a-bot-commands-menu.md)
* [Microsoft Teams 中机器人的身份验证流程](~/bots/how-to/authentication/auth-flow-bot.md)
* [使用机器人的任务模块](~/task-modules-and-cards/task-modules/task-modules-bots.md)
