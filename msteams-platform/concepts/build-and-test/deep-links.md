---
title: 创建指向内容的深层链接
description: 介绍深层链接以及如何在应用中使用它们
ms.topic: how-to
keywords: 团队深层链接深层链接
ms.openlocfilehash: d6efe7332035320d2114e0e834d1c971ccc7108c
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231559"
---
# <a name="create-deep-links-to-content-and-features-in-microsoft-teams"></a>创建指向 Microsoft Teams 中内容和功能的深层链接

可以在 Teams 内创建指向信息和功能的链接。 创建深层链接很有用的示例如下所示：

* 将用户导航到应用选项卡之一中的内容。 例如，你的应用可以有一个自动程序来发送消息，通知用户重要活动。 当用户点击通知时，深层链接将导航到选项卡，以便用户可以查看有关活动的更多详细信息。
* 你的应用通过预填充包含所需参数的深层链接，自动执行或简化某些用户任务，如创建聊天或安排会议。 这无需用户手动输入信息。

> [!NOTE]
>
> 深层链接先启动浏览器，然后再导航到内容和信息，如下所示：
>
> **Tab**：  
> ✔直接导航到深层链接 URL。
>
> **自动程序**：  
> ✔正文中的深度链接 - 首先在浏览器中打开。  
> ✔添加到自适应卡片中的 OpenURL 操作中的 Deeplink - 直接导航到深度链接 url。  
> ✔中的超链接标记文本 - 首先在浏览器中打开。  
>
> **聊天**：  
> ✔文本消息超链接标记：直接导航到深层链接 URL。  
> ✔常规聊天对话中粘贴的链接 - 直接导航到深层链接 URL。

## <a name="deep-linking-to-your-tab"></a>到选项卡的深层链接

你可以创建指向 Teams 中实体的深层链接。 通常，这用于创建导航到选项卡中内容和信息的链接。例如，如果选项卡包含任务列表，工作组成员可以创建并共享指向单个任务的链接。 选择链接时，它会导航到以特定项目为焦点的选项卡。 若要实现此目标，请以最适合你的 UI 的任何方式向每个项目添加"复制链接"操作。 当用户采取此操作时，您调用以显示一个对话框，其中包含用户可复制到 `shareDeepLink()` 剪贴板的链接。 进行此调用时，还会传递项的 ID，在单击链接并重新加载选项卡时，会[](~/tabs/how-to/access-teams-context.md)返回该 ID。

或者，您也可以使用本主题稍后指定的格式以编程方式生成深层链接。 可以在 [自动程序消息](~/bots/what-are-bots.md) 和连接器消息 [中](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) 使用这些消息，以通知用户选项卡或其中项目的更改。

> [!NOTE]
> 此深层链接不同于指向选项卡菜单项的 **"** 复制"链接提供的链接，而该链接仅生成指向此选项卡的深层链接。

>[!NOTE]
> 目前，shareDeepLink 在移动平台上不起作用。

### <a name="showing-a-deep-link-to-an-item-within-your-tab"></a>显示指向选项卡内项目的深层链接

若要显示包含指向选项卡中项目的深层链接的对话框，请调用 `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })`

提供以下字段：

* `subEntityId`&emsp;要深入链接到的选项卡内项目的唯一标识符
* `subEntityLabel`&emsp;用于显示深层链接的项目的标签
* `subEntityWebUrl`&emsp;具有回退 URL 的可选字段，如果客户端不支持呈现选项卡

### <a name="generating-a-deep-link-to-your-tab"></a>生成到选项卡的深层链接

> [!NOTE]
> 个人选项卡具有 `personal` 范围，而频道和组选项卡使用 `team` 或 `group` 作用域。 这两个选项卡类型的语法略有不同，因为只有可配置的选项卡具有与其上下文 `channel` 对象关联的属性。 有关 [选项卡](~/resources/schema/manifest-schema.md) 范围详细信息，请参阅清单参考。

> [!NOTE]
> 只有在使用 v0.4 或更高版本库配置了选项卡并且由于该选项卡具有实体 ID 时，深度链接才能正常工作。 指向没有实体 ID 的选项卡的深层链接仍导航到选项卡，但无法向选项卡提供子实体 ID。

对可以在自动程序、连接器或邮件扩展卡中使用的深层链接使用以下格式：

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> 如果自动程序发送包含深层链接的消息，则当用户选择链接时将打开一 `TextBlock` 个新的浏览器选项卡。 这发生在 Chrome 和 Microsoft Teams 桌面应用中，两者均在 Linux 上运行。
> 如果机器人将相同的深层链接 URL 发送到一个，则当用户选择链接时，将在当前浏览器选项卡中打开 `Action.OpenUrl` Teams 选项卡。 未打开新浏览器选项卡。

查询参数包括：

* `appId`&emsp;清单中的 ID;例如，"fe4a8eba-2a31-4737-8e33-e5fae6fee194"
* `entityId`&emsp;选项卡中项的 ID，在配置选项卡 [时提供](~/tabs/how-to/create-tab-pages/configuration-page.md);例如，"tasklist123"
* `entityWebUrl`或具有回退 URL 的可选字段（如果客户端不支持呈现选项卡）;例如 `subEntityWebUrl` &emsp; ，" https://tasklist.example.com/123 " 或 https://tasklist.example.com/list123/task456 "
* `entityLabel`或选项卡中项的标签，用于显示深层链接;例如，" `subEntityLabel` &emsp; 任务列表 123"或"任务 456"
* `context`&emsp;包含以下字段的 JSON 对象：
  * `subEntityId`&emsp;选项卡内项 _的_ ID;例如，"task456"
  * `channelId`&emsp;选项卡上下文中提供的 Microsoft Teams 频道 [ID;](~/tabs/how-to/access-teams-context.md)例如，"19：cbe3683f25094106b826c9cada3afbe0@thread.skype"。 此属性仅在作用域为"team"的可配置选项卡中可用。 它在静态选项卡中不可用，这些选项卡的范围为"个人"。

示例：

* 指向可配置选项卡本身的链接： `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* 指向可配置选项卡中的任务项的链接： `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* 指向静态选项卡本身的链接： `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`
* 指向静态选项卡中的任务项的链接： `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`

> [!IMPORTANT]
> 确保所有查询参数都正确编码了 URI。 您必须使用上一个示例遵循之前的示例：
> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consuming-a-deep-link-from-a-tab"></a>从选项卡使用深层链接

导航到深层链接时，Microsoft Teams 只需导航到选项卡，并通过 Microsoft Teams JavaScript 库提供一种机制，以检索子实体 ID（如果存在）。

如果 [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) 选项卡通过深层链接导航，调用将返回包含 `subEntityId` 字段的上下文。

## <a name="deep-linking-from-your-tab"></a>从选项卡进行深层链接

你可以从选项卡深入链接到 Teams 中的内容。如果你的选项卡需要链接到 Teams 中的其他内容（如频道、消息、其他选项卡，或者甚至打开计划对话框，这非常有用。 若要从选项卡触发深层链接，应调用：

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

此调用将你导航到正确的 URL，或触发客户端操作，例如打开计划或应用安装对话框。 请参阅以下示例：

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a>到聊天的深层链接

通过指定参与者集，可以创建指向用户之间的私人聊天的深层链接。 如果指定参与者不存在聊天，则链接将用户导航到空的新聊天。 在用户发送第一条消息之前，会以草稿状态新建聊天。 否则，您可以指定聊天的名称（如果它不存在）以及应插入到用户的撰写框中的文本。 你可以将此功能视为用户执行手动操作以导航到或创建聊天，然后键入消息的快捷方式。

例如，如果你将 Office 365 用户配置文件作为卡片从自动程序返回，此深层链接可让用户轻松与该用户聊天。

### <a name="generating-a-deep-link-to-a-chat"></a>生成到聊天的深层链接

对于可以在自动程序、连接器或邮件扩展卡中使用的深层链接，请使用此格式：

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

示例：`https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

查询参数包括：

* `users`：表示聊天参与者的用户 ID 的逗号分隔列表。 执行该操作的用户始终作为参与者包含在内。 目前，用户 ID 字段支持 Azure AD UserPrincipalName，通常仅支持电子邮件地址。
* `topicName`：一个可选字段，用于显示名称（如果与 3 个或多个用户进行聊天）。 如果未指定此字段，则聊天显示名称基于参与者的名称。
* `message`：在聊天状态为草稿时要插入到当前用户的撰写框中的消息文本的可选字段。

若要将此深层链接与自动程序一同使用，可以在卡片按钮中指定此链接作为 URL 目标，或点击操作类型的 `openUrl` 操作。

### <a name="generating-a-deep-link-to-a-call"></a>生成与呼叫的深层链接

对于可以在自动程序、连接器或邮件扩展卡中使用的深层链接，请使用此格式：

`https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>`

示例：`https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

查询参数包括：

* `users`：表示呼叫参与者的用户 ID 的逗号分隔列表。 执行该操作的用户始终作为参与者包含在内。 目前，用户 ID 字段支持 Azure AD UserPrincipalName，通常仅支持电子邮件地址。

## <a name="linking-to-the-scheduling-dialog"></a>链接到计划对话框

> [!Note]
> 此功能目前处于开发人员预览阶段。

可以创建指向 Teams 内置计划对话框的深层链接。 如果你的应用可帮助用户完成日历或计划相关任务，这尤其有用。

### <a name="generating-a-deep-link-to-the-scheduling-dialog"></a>生成到计划对话框的深层链接

对可以在自动程序、连接器或邮件扩展卡中使用的深层链接使用以下格式： `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

示例：`https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

查询参数包括：

* `attendees`：表示会议与会者的用户 ID 的可选逗号分隔列表。 执行该操作的用户是会议组织者。 用户 ID 字段当前仅支持 Azure AD UserPrincipalName，通常为电子邮件地址。
* `startTime`：事件的可选开始时间。 这应该采用长 [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)格式，例如"2018-03-12T23：55：25+02：00"。
* `endTime`：事件的可选结束时间，也采用 ISO 8601 格式。
* `subject`：会议主题的可选字段。
* `content`：会议详细信息字段的可选字段。

目前不支持指定位置。 你必须指定 UTC 偏移量，这意味着生成开始时间和结束时间时时区。

若要将此深层链接与自动程序一同使用，可以在卡片按钮中指定此链接作为 URL 目标，或点击操作类型的 `openUrl` 操作。
