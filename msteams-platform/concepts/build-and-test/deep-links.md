---
title: 创建深层链接
description: 了解如何创建深层链接，以及如何在 Microsoft Teams 应用中使用和导航它们（带有选项卡）。
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: e5e9596c6049e899e6cc807b7ce2128b322a971e
ms.sourcegitcommit: 9d318eda5589ea8f5519d05cb83e0acf3e13e2f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66150678"
---
# <a name="create-deep-links"></a>创建深层链接

深层链接是一种导航机制，可用于将用户与 Teams 和 Teams 应用中的信息和功能联系起来。 创建深度链接可能有用的一些方案如下:

* 将用户导航到应用的某个选项卡中的内容。 例如，应用可以有一个自动程序，用于发送通知用户重要活动的消息。 当用户点击通知时，深层链接将导航到选项卡，以便用户可以查看有关活动的更多详细信息。
* 应用通过预先填充包含所需参数的深层链接，自动执行或简化某些用户任务，例如创建聊天或安排会议。 这样可以避免用户手动输入信息。

Microsoft Teams JavaScript 客户端 SDK (TeamsJS) 简化了导航过程。 对于许多方案（例如导航到选项卡中的内容和信息，或者甚至启动聊天对话框），SDK 提供强类型的 API，从而改进体验，并可替换深层链接的使用。 建议将这些 API 用于可能在其他主机 (Outlook，Office) 中运行的 Teams 应用，因为它们还提供了一种方法来检查该主机是否支持正在使用的功能。 以下部分显示有关深层链接的信息，但也强调了过去需要深层链接的方案如何随着 TeamsJS 的 v2 版本而发生更改。

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

> [!NOTE]
>
> 深层链接的行为取决于多种因素。 以下列表概述了 Teams 实体上的深层链接的行为。
>
> **选项卡**：  
> ✔直接导航到深层链接 URL。
>
> **自动程序**：  
> ✔卡片正文中的深层链接：首先在浏览器中打开。  
> ✔在自适应卡片中添加到 OpenURL 操作的深层链接：直接导航到深层链接 URL。  
> ✔卡片中的超链接 markdown 文本：首先在浏览器中打开。  
>
> **聊天**：  
> ✔文本消息超链接标记：直接导航到深层链接 URL。  
> ✔粘贴在常规聊天对话中的链接：直接导航到深层链接 URL。
>
>
>跨 Microsoft 365 (Outlook/Office) 扩展的 Teams 应用的导航行为取决于两个因素：
>
> * 深层链接指向的目标
> * 运行 Teams 应用的主机
>
> 如果 Teams 应用在目标深层链接的主机内运行，则应用将直接在主机内打开。 但是，如果 Teams 应用在目标深层链接所在的不同主机中运行，则应用将首先在浏览器中打开。

## <a name="deep-link-to-your-tab"></a>深层链接你的选项卡

可在 Teams 应用中创建实体的深层链接。 此方法用于创建导航到选项卡中的内容和信息的链接。例如，如果选项卡包含任务列表，团队成员可以创建和共享各个任务的链接。 选择链接时，它会导航到焦点位于特定项的选项卡。

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

若要实现此操作，请以任何最适合 UI 的方式向每个项目添加“**复制链接**”操作。 当用户执行此操作时，将调用 [pages.shareDeepLink()](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest#@microsoft-teams-js-pages-sharedeeplink&preserve-view=true) 以显示包含用户可复制到剪贴板的链接的对话框。 进行此调用时，请为项目传递一个 ID，点击链接并重新加载选项卡时，将在[上下文](~/tabs/how-to/access-teams-context.md)中返回该 ID。

```javascript
pages.shareDeepLink({ subPageId: <subPageId>, subPageLabel: <subPageLabel>, subPageWebUrl: <subPageWebUrl> })
```

需要将字段替换为适当的信息：

* `subPageId`：要向其进行深层链接的页面内项的唯一标识符。
* `subPageLabel`：用于显示深层链接的项的标签。
* `subPageWebUrl`：客户端无法呈现页面时使用的回退 URL。

有关详细信息，请参阅 [pages.shareDeepLink()](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest#@microsoft-teams-js-pages-sharedeeplink&preserve-view=true)。

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

若要实现此操作，请向每个项目添加 **复制链接** 操作，以任何最适合 UI 的方式。 当用户执行此操作时，将调用 `shareDeepLink()` 以显示包含用户可复制到剪贴板的链接的对话框。 进行此调用时，你还会传递项目的 ID，当链接被跟踪并重新加载选项卡时，你将返回[上下文](~/tabs/how-to/access-teams-context.md)。

```javascript
microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })
```

需要将字段替换为适当的信息：

* `subEntityId`：要向其进行深层链接的选项卡内项的唯一标识符。
* `subEntityLabel`：用于显示深层链接的项的标签。
* `subEntityWebUrl`：如果客户端不支持呈现选项卡，要使用的具有回退 URL 的可选字段。

---

或者，还可以使用本文中稍后指定的格式以编程方式生成深层链接。 可以在[自动程序](~/bots/what-are-bots.md)和[连接器](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)消息中使用深层链接，告知用户有关选项卡或其中项目更改的信息。

> [!NOTE]
> 此深层链接与 **复制链接到选项卡** 菜单项提供的链接不同，后者仅生成此选项卡的深层链接。

>[!IMPORTANT]
> 目前，shareDeepLink 在移动平台上不起作用。

### <a name="consume-a-deep-link-from-a-tab"></a>使用选项卡中的深层链接

导航到深层链接时，Microsoft Teams 只需导航到选项卡，并通过 Teams JavaScript 库提供一种机制来检索子页面 ID（如果存在）。

如果选项卡通过深层链接导航，则 TeamsJS v1 中的 [`app.getContext()`](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-getcontext&preserve-view=true) 调用 (`microsoftTeams.getContext()`) 将返回一个承诺，该承诺将使用包含 `subPageId` 属性 (TeamsJS v1 的 subEntityId) 的上下文进行解析。 有关详细信息，请参阅 [PageInfo 接口](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-pageinfo&preserve-view=true)。

### <a name="generate-a-deep-link-to-your-tab"></a>生成选项卡的深层链接

虽然建议使用 `shareDeepLink()` 来生成指向选项卡的深层链接，但也可以手动创建一个。

> [!NOTE]
>
> * 个人选项卡具有 `personal` 作用域，而通道和组选项卡使用 `team` 或 `group` 作用域。 这两种选项卡类型的语法略有不同，因为只有可配置的选项卡具有与其上下文对象关联的 `channel` 属性。 有关选项卡范围的详细信息，请参阅[应用程序清单](~/resources/schema/manifest-schema.md)参考。
> * 仅当使用 v0.4 或更高版本库配置了选项卡并且具有实体 ID 时，深层链接才能正常工作。 没有实体 ID 的选项卡的深层链接仍会导航到选项卡，但无法向选项卡提供子实体 ID。

对可在自动程序、连接器或消息扩展卡中使用的深层链接使用以下格式：

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> 如果机器人发送包含 `TextBlock` 和深层链接的消息，则当用户选择链接时，将打开新的浏览器选项卡。 这发生在 Chrome 和 Teams 桌面应用中，两者都在 Linux 上运行。
> 如果机器人将相同的深层链接 URL 发送到 `Action.OpenUrl`，则当用户选择链接时，Teams 选项卡将在当前浏览器选项卡中打开。 未打开新的浏览器选项卡。

<!--- TBD: Edit this article.
* Admonitions/alerts seem to be overused. 
* An important alert at the end of this table does not make sense. Also, it has a code snippet inside it.
* List items in the table are not formatted well in output.
* Some headings use -ing verbs.
* Example values and some URLs should be in backticks and not emphasized.
* Codeblock are missing language.
* Check for markdownlint errors.
* Table with just a row isn't really needed. Provide the content without tabulating it.
--->

查询参数为：

| 参数名称 | 说明 | 示例 |
|:------------|:--------------|:---------------------|
| `appId`&emsp; | Teams 管理中心的 ID。 |fe4a8eba-2a31-4737-8e33-e5fae6fee194|
| `entityId`&emsp; | 选项卡中项的 ID，在[配置选项卡](~/tabs/how-to/create-tab-pages/configuration-page.md)时提供。|Tasklist123|
| `entityWebUrl` 或 `subEntityWebUrl`&emsp; | 在客户端不支持呈现选项卡时要是用的具有回退 URL 的可选字段。 | `https://tasklist.example.com/123` 或 `https://tasklist.example.com/list123/task456` |
| `entityLabel` 或 `subEntityLabel`&emsp; | 选项卡中项的标签，显示深层链接时要使用。 | 任务列表 123 或 任务 456 |
| `context.subEntityId`&emsp; | 选项卡内项的 ID。 |Task456 |
| `context.channelId`&emsp; | 选项卡 [上下文](~/tabs/how-to/access-teams-context.md) 中提供的 Microsoft Teams 频道 ID。 此属性仅在 **团队** 范围内的可配置选项卡中可用。 它在具有 **个人** 范围的静态选项卡中不可用。| 19:cbe3683f25094106b826c9cada3afbe0@thread.skype |
| `chatId`&emsp; | 可从选项卡 [上下文](~/tabs/how-to/access-teams-context.md) 中获得的用于群组和会议聊天的 ChatId。 | 17:b42de192376346a7906a7dd5cb84b673@thread.v2 |
| `contextType`&emsp; |  聊天是唯一受支持的会议上下文类型 | 聊天 |

**示例**：

* 链接到静态 (个人) 选项卡本身:

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`

* 链接到静态 (个人) 选项卡内的任务项目:

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`

* 链接到可配置选项卡本身：

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`

* 链接到可配置选项卡中的任务项：

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`

* 链接到添加到会议或群组聊天的选项卡应用:

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456?context={"chatId": "17:b42de192376346a7906a7dd5cb84b673@thread.v2","contextType":"chat"}`

> [!IMPORTANT]
> 确保所有查询参数都正确编码了 URI。 必须使用最后一个示例来遵循前面的示例：
>
> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

## <a name="navigation-from-your-tab"></a>从选项卡导航

可以使用 TeamsJS 或深层链接从选项卡导航到 Teams 中的内容。 如果选项卡需要将用户与 Teams 中的其他内容（例如频道、消息、另一个选项卡，甚至打开计划对话框）连接起来，这将非常有用。 以前，导航可能需要一个深层链接，但现在可以在许多实例中使用 SDK 来完成。 以下部分显示了这两种方法，但建议在可能的情况下使用 SDK 的强类型功能。

使用 TeamsJS 的好处之一，尤其是对于可能在其他主机 (Outlook 和 Office) 中运行的 Teams 应用，可以检查主机是否支持你尝试使用的功能。 若要检查主机对功能的支持，可以使用与 API 命名空间关联的 `isSupported()` 函数。 TeamsJS SDK 通过命名空间将 API 组织为功能。 例如，在命名空间 `pages` 中使用 API 之前，可以检查从 `pages.isSupported()` 返回的布尔值，并在应用和应用 UI 的上下文中执行相应操作。  

有关 TeamsJS 中的功能和 API 的更多信息，请参阅 [使用 Microsoft Teams JavaScript 客户端 SDK 生成选项卡和其他托管体验](~/tabs/how-to/using-teams-client-sdk.md#apis-organized-into-capabilities)。

### <a name="navigate-within-your-app"></a>在应用内导航

可以使用 TeamsJS 在应用中导航。 以下代码演示如何导航到 Teams 应用中的特定实体。

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

可以使用 [pages.navigateToApp()](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest#@microsoft-teams-js-pages-navigatetoapp&preserve-view=true) 函数从选项卡触发导航，如以下代码所示：

```javascript
if (pages.isSupported()) {
  const navPromise = pages.navigateToApp({ appId: <appId>, pageId: <pageId>, webUrl: <webUrl>, subPageId: <subPageId>, channelId:<channelId>});
  navPromise.
     then((result) => {/*Successful navigation*/}).
     catch((error) => {/*Failed navigation*/});
}
else { /* handle case where capability isn't supported */ }
```

有关使用页面功能的详细信息，请参阅 [pages.navigateToApp()](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest#@microsoft-teams-js-pages-navigatetoapp&preserve-view=true) 和其他导航选项的“[页面](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest&preserve-view=true)”命名空间。 如果需要，还可以使用 [app.openLink()](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-openlink&preserve-view=true) 函数直接打开深层链接。

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

若要从选项卡触发深层链接，请调用：

```javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

---

### <a name="open-a-scheduling-dialog"></a>打开计划对话框

可以从 Teams 应用打开计划对话框，如以下代码所示。 如果你的应用帮助用户完成日历或计划相关任务，这尤其有用。

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```javascript
// Open a scheduling dialog from your tab
if(calendar.isSupported()) {
   const calendarPromise = calendar.composeMeeting({
      attendees: ["joe@contoso.com", "bob@contoso.com"],
      content: "test content",
      endTime: "2018-10-24T10:30:00-07:00"
      startTime: "2018-10-24T10:00:00-07:00"
      subject: "test subject"});
   calendarPromise.
      then((result) => {/*Successful operation*/}).
      catch((error) => {/*Unsuccessful operation*/});
}
else { /* handle case where capability isn't supported */ }
```

有关使用日历的详细信息，请参阅 API 参考文档中的“[日历](/javascript/api/@microsoft/teams-js/calendar?view=msteams-client-js-latest&preserve-view=true)”命名空间。

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");
```

---

#### <a name="generate-a-deep-link-to-the-scheduling-dialog"></a>生成计划对话框的深层链接

虽然建议使用 TeamsJS 的强类型 API，但可以手动创建指向 Teams 内置计划对话框的深层链接。 将以下格式用于可以在机器人、连接器或消息扩展卡片中使用的深层链接：`https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

例如：`https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

> [!NOTE]
> 搜索参数不支持用 `+` 信号代替空格 (``)。 请确保 URI 编码代码对空格返回 `%20`，例如 `?subject=test%20subject` 是好的，但 `?subject=test+subject` 是不好的。

查询参数为：

* `attendees`：表示会议与会者的用户 ID 的可选逗号分隔列表。 执行操作的用户是会议组织者。 用户 ID 字段当前仅支持 Azure AD UserPrincipalName，通常是电子邮件地址。
* `startTime`：事件的可选开始时间。 这应采用 [long ISO 8601 格式](https://en.wikipedia.org/wiki/ISO_8601)，例如 *2018-03-12T23:55:25+02:00*。
* `endTime`：事件的可选结束时间，也采用 ISO 8601 格式。
* `subject`：会议主题的可选字段。
* `content`：会议详细信息字段的可选字段。

> [!NOTE]
> 目前不支持指定位置。必须指定 UTC 偏移量，它表示生成开始和结束时间时的时区。

若要将此深层链接与机器人配合使用，可以在卡片的按钮中将此链接指定为 URL 目标，或通过 `openUrl` 操作类型点击操作。

### <a name="open-an-app-install-dialog"></a>打开应用安装对话框

可以从 Teams 应用打开应用安装对话框，如以下代码所示。

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```javascript
// Open an app install dialog from your tab
if(appInstallDialog.isSupported()) {
    const dialogPromise = appInstallDialog.openAppInstallDialog({ appID: <appId>});
    dialogPromise.
      then((result) => {/*Successful operation*/}).
      catch((error) => {/*Unsuccessful operation*/});
}
else { /* handle case where capability isn't supported */ }
```

有关安装对话框的详细信息，请参阅 API 参考文档中的 [appInstallDialog.openAppInstallDialog()](/javascript/api/@microsoft/teams-js/appinstalldialog?view=msteams-client-js-latest#@microsoft-teams-js-appinstalldialog-openappinstalldialog&preserve-view=true) 函数。

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```javascript
// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

---

### <a name="navigate-to-a-chat"></a>导航到聊天

通过指定参与者集，可以使用 TeamsJS 在用户之间导航或创建私人聊天。 如果不存在与指定参与者的聊天，则会将用户导航到空的新聊天。 在用户发送第一条消息之前，将在草稿状态下创建新聊天。 否则，可以指定聊天的名称（如果尚不存在）以及应插入到用户撰写框中的文本。 可以将此功能视为用户执行手动操作以导航到或创建聊天，然后键入消息的快捷方式。

例如，如果从机器人以卡片形式返回 Office 365 用户配置文件，则用户可通过此深层链接轻松与该用户聊天。 以下示例演示如何使用初始消息向一组参与者打开聊天消息。

```javascript
if(chat.isSupported()) {
    const chatPromise = chat.openGroupChat({ users: ["joe@contoso.com","bob@contoso.com"], topic: "Prep For Meeting Tomorrow", message: "Hi folks kicking off chat about our meeting tomorrow"});
    chatPromise.
      then((result) => {/*Successful operation*/}).
      catch((error) => {/*Unsuccessful operation*/});
}
else { /* handle case where capability isn't supported */ }
```

虽然建议使用强类型 API，但也可以将以下格式用于手动创建的深层链接，该链接可以在机器人、连接器或消息扩展卡片中使用：

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

例如：`https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

查询参数为：

* `users`：表示聊天参与者的用户 ID 的逗号分隔列表。 执行操作的用户始终作为参与者被包括在内。 目前，“用户 ID”字段支持 Microsoft Azure Active Directory (Azure AD) UserPrincipalName，例如仅支持电子邮件地址。
* `topicName`：与三个或更多用户聊天时，聊天显示名称的可选字段。 如果未指定此字段，则聊天的显示名称基于参与者的姓名。
* `message`：要在聊天处于草稿状态时插入当前用户撰写框的消息文本的可选字段。

若要将此深层链接与机器人配合使用，请在卡的按钮中将此项指定为 URL 目标，或通过 `openUrl` 操作类型点击操作。

### <a name="generate-deep-links-to-channel-conversation"></a>生成指向频道对话的深层链接

使用此深层链接格式导航到频道线程中的特定对话：

`https://teams.microsoft.com/l/message/<channelId>/<parentMessageId>?tenantId=<tenantId>&groupId=<groupId>&parentMessageId=<parentMessageId>&teamName=<teamName>&channelName=<channelName>&createdTime=<createdTime>`

例如：`https://teams.microsoft.com/l/message/<channelId>/1648741500652?tenantId=<tenantId>&groupId=<groupId>&parentMessageId=1648741500652&teamName=<teamName>&channelName=<channelName>&createdTime=1648741500652`

查询参数为：

* `channelId`：会话的频道 ID。 例如，`19:3997a8734ee5432bb9cdedb7c432ae7d@thread.tacv2`。
* `tenantId`：租户 ID，如 `0d9b645f-597b-41f0-a2a3-ef103fbd91bb`。
* `groupId`：文件的组 ID。 例如，`3606f714-ec2e-41b3-9ad1-6afb331bd35d`。
* `parentMessageId`：会话的父消息 ID。
* `teamName`：团队名称。
* `channelName`：团队频道的名称。

> [!NOTE]
> 可以在通道的 URL 中看到 `channelId` 和 `groupId`。

### <a name="generate-deep-links-to-file-in-channel"></a>在通道中生成文件的深层链接

机器人、连接器或消息扩展卡片中使用以下深层链接格式：

`https://teams.microsoft.com/l/file/<fileId>?tenantId=<tenantId>&fileType=<fileType>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadId>&groupId=<groupId>`

查询参数为：

* `fileId`：Sharepoint Online 中的唯一文件 ID，也称为 `sourcedoc`。例如，`1FA202A5-3762-4F10-B550-C04F81F6ACBD`。
* `tenantId`：租户 ID，如 `0d9b645f-597b-41f0-a2a3-ef103fbd91bb`。
* `fileType`：支持的文件类型，如 .docx、.pptx、.xlsx 和 .pdf
* `objectUrl`：文件的对象 URL。 格式为 `https://{tenantName}.sharepoint.com/sites/{TeamName}/SharedDocuments/{ChannelName}/FileName.ext`。 例如，`https://microsoft.sharepoint.com/teams/(filepath)`。
* `baseUrl`：文件的基本 URL。 格式为 `https://{tenantName}.sharepoint.com/sites/{TeamName}`。 例如，`https://microsoft.sharepoint.com/teams`。
* `serviceName`：服务名称、应用 ID。 例如，`teams`。
* `threadId`：threadId 是存储文件的团队的团队 ID。 它是可选的，不能为存储在用户 OneDrive 文件夹中的文件设置。 threadId - 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype。
* `groupId`：文件的组 ID。 例如，`ae063b79-5315-4ddb-ba70-27328ba6c31e`。

> [!NOTE]
> 可以在通道的 URL 中看到 `threadId` 和 `groupId`。  

机器人、连接器或消息扩展卡片中使用以下深层链接格式：

`https://teams.microsoft.com/l/file/<fileId>?tenantId=<tenantId>&fileType=<fileType>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadId>&groupId=<groupId>`

以下示例格式说明了指向文件的深层链接：

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80?tenantId=0d9b645f-597b-41f0-a2a3-ef103fbd91bb&fileType=pptx&objectUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform%2FShared%20Documents%2FFC7-%20Bot%20and%20Action%20Infra%2FKaizala%20Actions%20in%20Adaptive%20Cards%20-%20Deck.pptx&baseUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform&serviceName=teams&threadId=19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype&groupId=ae063b79-5315-4ddb-ba70-27328ba6c31e`

#### <a name="serialization-of-this-object"></a>此对象的序列化

```javascript
{
fileId: "5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80",
tenantId: "0d9b645f-597b-41f0-a2a3-ef103fbd91bb",
filetype: = "pptx",
objectUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform/Shared Documents/FC7- Bot and Action Infra/Kaizala Actions in Adaptive Cards - Deck.pptx",
baseUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform",
serviceName: "teams",
threadId: = "19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype",
groupId: "ae063b79-5315-4ddb-ba70-27328ba6c31e"
}
```

### <a name="deep-linking-to-an-app"></a>深层链接到聊天

在 Teams 应用商店中列出应用后，为应用创建深层链接。 若要创建启动 Teams 的链接，请将应用 ID 追加到以下 URL：`https://teams.microsoft.com/l/app/<your-app-id>`。 将显示一个对话框来安装应用。
  
### <a name="deep-linking-for-sharepoint-framework-tabs"></a>SharePoint 框架选项卡的深层链接

可以在机器人、连接器或消息扩展卡片中使用以下深层链接格式：`https://teams.microsoft.com/l/entity/<AppId>/<EntityId>?webUrl=<entityWebUrl>/<EntityName>`

> [!NOTE]
> 当机器人发送包含深层链接的 TextBlock 消息时，当用户选择链接时，将打开新的浏览器选项卡。 这发生在 Linux 上运行的 Chrome 和 Microsoft Teams 桌面应用中。
> 如果机器人将相同的深层链接 URL 发送到 `Action.OpenUrl`，则当用户选择链接时，Teams 选项卡将在当前浏览器中打开。 未打开新的浏览器选项卡。

查询参数为：

* `appID`：清单 ID，例如 `fe4a8eba-2a31-4737-8e33-e5fae6fee194`。

* `entityID`：在[配置选项卡](~/tabs/how-to/create-tab-pages/configuration-page.md)时提供的项 ID。例如 `tasklist123`。
* `entityWebUrl`：客户端不支持选项卡呈现情况下具有回退 URL 的可选字段 - `https://tasklist.example.com/123` 或 `https://tasklist.example.com/list123/task456`。
* `entityName`：选项卡中项的标签，在显示深层链接时使用，任务列表 123 或任务 456。

例如：`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&TaskList`

### <a name="navigate-to-an-audio-or-audio-video-call"></a>导航到音频或音频视频聊天

通过指定通话类型和参与者，可以向单个用户或一组用户调用仅音频或音频视频聊天。 在进行呼叫之前，Teams 客户端会提示确认以进行呼叫。 对于群组调用，可以在同一深层链接调用中调用一组 VoIP 用户和一组 PSTN 用户。

在视频通话时，客户端将请求确认并打开呼叫方的通话视频。 呼叫接收方可以选择通过 Teams 呼叫通知窗口通过仅音频或音频和视频进行响应。

> [!NOTE]
> 此方法不能用于调用会议。

以下代码演示如何使用 TeamsJS SDK 启动调用：

```javascript
if(call.isSupported()) {
    const callPromise = call.startCall({ targets: ["joe@contoso.com","bob@contoso.com","4:9876543210"], requestedModalities: [call.CallModalities.Audio], source: "demoApp"});
    callPromise.
      then((result) => {/*Successful operation*/}).
      catch((error) => {/*Unsuccessful operation*/});
}
else { /* handle case where capability isn't supported */ }

```

#### <a name="generate-a-deep-link-to-a-call"></a>生成呼叫的深层链接

虽然建议使用 TeamsJS 的强类型 API，但也可以使用手动创建的深层链接来启动调用。

| 深度链接 | 格式 | 示例 |
|-----------|--------|---------|
| 进行音频通话 | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com` |
| 进行音频和视频通话 | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>&withVideo=true` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withVideo=true` |
|使用可选参数源进行音频和视频通话 | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>&withVideo=true&source=demoApp` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withVideo=true&source=demoApp` |  
| 对 VoIP 和 PSTN 用户进行音频和视频通话 | `https://teams.microsoft.com/l/call/0/0?users=<user1>,4:<phonenumber>` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,4:9876543210` |
  
下面是查询参数：

* `users`：表示呼叫参与者的用户 ID 的逗号分隔列表。 目前，用户 ID 字段支持 Azure AD UserPrincipalName（通常为电子邮件地址），或者在 PSTN 通话时，它支持 pstn mri 4:&lt;phonenumber&gt;。
* `withVideo`：这是一个可选参数，可用于进行视频通话。 设置此参数将仅打开调用方的相机。 呼叫接收方可以选择通过 Teams 呼叫通知窗口通过音频或音频和视频呼叫进行应答。
* `Source`：这是一个可选参数，用于通知深层链接的源。

## <a name="code-sample"></a>代码示例

| 示例名称 | Description | C# |Node.js|
|-------------|-------------|------|----|
|使用子实体 ID 的深层链接  | Teams 示例应用，用于演示从机器人聊天到使用子实体 ID 的选项卡的深层链接。|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/nodejs)|

## <a name="see-also"></a>另请参阅

* [集成 web 应用](~/samples/integrate-web-apps-overview.md)
* [Moodle LMS](~/resources/moodleinstructions.md)
