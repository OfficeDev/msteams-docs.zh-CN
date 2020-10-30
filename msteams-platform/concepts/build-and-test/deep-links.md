---
title: 创建深层链接
description: 介绍深层链接以及如何在应用程序中使用它们
keywords: 团队深层链接 deeplink
ms.openlocfilehash: 03580c4d15c82da70402d68d85b0d28f8afa670e
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796328"
---
# <a name="create-deep-links-to-content-and-features-in-microsoft-teams"></a>创建指向 Microsoft 团队中的内容和功能的深层链接

您可以创建指向团队客户端中的信息和功能的链接。 这可能有用的示例：

* 将用户导航到某个应用程序的选项卡中的内容。 例如，您的应用程序可能有一个用于发送通知用户重要活动的邮件的 bot。 当用户点击通知时，深层链接将导航到 "" 选项卡，以便用户可以查看有关活动的更多详细信息。
* 您的应用程序通过使用所需参数预填充深层链接来自动执行或简化某些用户任务，如创建聊天或安排会议。 这样，用户就无需手动输入信息。

## <a name="deep-linking-to-your-tab"></a>深度链接到你的选项卡

您可以创建指向团队中的实体的深层链接。 通常，这用于创建导航到您的选项卡中的内容和信息的链接。例如，如果您的选项卡中包含任务列表工作组成员可以创建和共享单个任务的链接。 单击时，链接将导航到重点关注特定项目的选项卡。 若要实现此目的，请为每个项目添加 "复制链接" 操作，采用最适合您的 UI 的任何方式。 当用户执行此操作时，将调用 `shareDeepLink()` 以显示一个对话框，其中包含用户可以复制到剪贴板的链接。 在进行此调用时，还会为您的项目传递一个 ID，在后续 [链接时，](~/tabs/how-to/access-teams-context.md) 将返回该 ID，并且重新加载您的选项卡。

或者，也可以使用本主题后面所指定的格式以编程方式生成深层链接。 您可能需要在 [机器人](~/bots/what-are-bots.md) 和 [连接器](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) 消息中使用这些选项，以告知用户对您的选项卡或其中的项目所做的更改。

> [!NOTE]
> 这不同于 **复制指向选项卡** 菜单项的链接提供的链接，它只生成指向此选项卡的深层链接。

### <a name="showing-a-deep-link-to-an-item-within-your-tab"></a>在选项卡中显示指向某个项目的深层链接

若要显示一个对话框，其中包含指向您的选项卡中的项的深层链接，请调用 `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })`

提供以下字段：

* `subEntityId`&emsp;选项卡中您要深度链接的项的唯一标识符
* `subEntityLabel`&emsp;用于显示深层链接的项的标签
* `subEntityWebUrl`&emsp;一个可选字段，如果客户端不支持呈现该选项卡，则为要使用的回退 URL

### <a name="generating-a-deep-link-to-your-tab"></a>生成指向您的选项卡的深层链接

> [!NOTE]
> 静态选项卡的作用域为 "个人"，且可配置的选项卡的作用域为 "team"。 由于只有可配置的选项卡具有 `channel` 与其上下文对象相关联的属性，这两个选项卡类型的语法略有不同。 有关个人和团队作用域的详细信息，请参阅 [清单](~/resources/schema/manifest-schema.md) 参考。
> [!NOTE]
> 仅当选项卡是使用 v 0.4 或更高版本库配置的，并且由于具有实体 ID 时，Deep 链接才会正常工作。 指向不含实体 Id 的选项卡的深层链接仍会导航到选项卡，但不能向该选项卡提供子实体 ID。

此格式适用于您可以在机器人、连接器或邮件扩充卡中使用的深层链接：

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

查询参数为：

* `appId`&emsp;清单中的 ID;例如，"fe4a8eba-2a31-4737-8e33-e5fae6fee194"
* `entityId`&emsp;选项卡中的项的 ID，在 [配置选项卡](~/tabs/how-to/create-tab-pages/configuration-page.md)时提供;例如，"tasklist123"
* `entityWebUrl`或者 `subEntityWebUrl` &emsp; 一个可选字段，如果客户端不支持呈现该选项卡，则为要使用的回退 URL; 例如，" https://tasklist.example.com/123 " 或 " https://tasklist.example.com/list123/task456 "
* `entityLabel`或 `subEntityLabel` &emsp; 选项卡中项的标签，以在显示深层链接时使用; 例如，"任务列表 123" 或 "任务 456"
* `context`&emsp;一个包含以下字段的 JSON 对象：
  * `subEntityId`&emsp;选项卡 _中_ 项的 ID;例如，"task456"
  * `channelId`&emsp;Microsoft 团队频道 ID (可从选项卡 [上下文](~/tabs/how-to/access-teams-context.md)中获取;例如，"19： cbe3683f25094106b826c9cada3afbe0@thread skype"。 此属性仅在作用域为 "team" 的可配置选项卡中可用。 它在具有 "个人" 范围的静态选项卡中不可用。

示例：

* 链接到可配置的选项卡本身： `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* 链接到 "可配置" 选项卡中的任务项： `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* 指向静态选项卡本身的链接： `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`
* 链接到静态选项卡中的任务项： `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`

> [!IMPORTANT]
> 确保所有查询参数都经过了正确的 URI 编码。 为了提高可读性，以上示例不是，但您应该这样做。 使用最后一个示例：
> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consuming-a-deep-link-from-a-tab"></a>从选项卡中使用深层链接

导航到深层链接时，Microsoft 团队只是导航到该选项卡，并通过 Microsoft 团队 JavaScript 库提供一种机制，用于检索子实体 ID (如果它存在) 。

[`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) `subEntityId` 如果通过深层链接将选项卡导航到该字段，则调用将返回一个包含该字段的上下文。

## <a name="deep-linking-from-your-tab"></a>从你的选项卡深层链接

您可以从选项卡中 deeplink 到工作组中的内容。如果您的选项卡需要链接到团队中的其他内容（如频道、邮件、另一个选项卡或甚至打开日程安排对话框），这将非常有用。 若要从您的选项卡触发 deeplink，应调用：

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

此操作将导航到正确的 URL，或触发客户端操作，如打开计划或应用程序安装对话框。 示例：

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a>深层链接到聊天

您可以通过指定一组参与者来创建到用户之间的私人聊天的深层链接。 如果不存在与指定参与者的聊天，该链接将导航用户到空的新聊天。 新聊天将在草稿状态中创建，直到用户发送第一封邮件。 （可选）您可以指定聊天 (的名称（如果尚不存在）) ，以及应插入到用户的 "撰写" 框中的文本。 您可以将此功能视为用户执行导航或创建聊天的手动操作，然后键入邮件的快捷方式。

例如，如果您以卡片形式返回来自 bot 的 Office 365 用户配置文件，此深层链接可以让用户轻松地与此人聊天。

### <a name="generating-a-deep-link-to-a-chat"></a>生成指向聊天的深层链接

此格式适用于您可以在机器人、连接器或邮件扩充卡中使用的深层链接：

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

示例：`https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

查询参数为：

* `users`&emsp;代表聊天参与者的用户 Id 的逗号分隔列表。 执行操作的用户始终作为参与者加入。 "User ID" 字段目前仅支持 Azure AD UserPrincipalName (通常) 电子邮件地址。
* `topicName`&emsp;用于聊天的显示名称的可选字段，在与3个或更多用户聊天的情况下。 如果未指定此字段，则聊天的显示名称将基于参与者的名称。
* `message`&emsp;在聊天处于草稿状态时要插入到当前用户的撰写框中的邮件文本的可选字段。

若要使用与你的 bot 的深层链接，你可以将其指定为你的卡片按钮中的 URL 目标，或通过 `openUrl` 操作类型点击操作。

## <a name="linking-to-the-scheduling-dialog"></a>链接到计划对话框

> [!Note]
> 此功能当前处于开发人员预览版中。

您可以创建指向团队客户端的内置日程安排对话框的深层链接。 如果您的应用程序可帮助用户完成日历或与日程排定相关的任务，这将非常有用。

### <a name="generating-a-deep-link-to-the-scheduling-dialog"></a>生成指向日程安排对话框的深层链接

此格式适用于您可以在机器人、连接器或邮件扩充卡中使用的深层链接： `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

示例：`https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

查询参数为：

* `attendees`&emsp;可选的以逗号分隔的用户 Id 列表，表示会议的与会者。 执行操作的用户是会议组织者。 "User ID" 字段目前仅支持 Azure AD UserPrincipalName (通常) 电子邮件地址。
* `startTime`&emsp;事件的可选开始时间。 这应采用 [ISO 8601 的长格式](https://en.wikipedia.org/wiki/ISO_8601)，例如 "2018-03-12T23：55： 25 + 02： 00"。
* `endTime`&emsp;事件的可选结束时间，也是 ISO 8601 格式。
* `subject`&emsp;会议主题的可选字段。
* `content`&emsp;"会议详细信息" 域的可选字段。

目前，不支持指定位置。 在生成开始和结束时间时，请务必指定 UTC 偏移量 (时区) 。

若要使用与你的 bot 的深层链接，你可以将其指定为你的卡片按钮中的 URL 目标，或通过 `openUrl` 操作类型点击操作。
