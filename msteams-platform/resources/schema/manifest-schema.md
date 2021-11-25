---
title: 清单架构参考
description: 介绍列表的清单Microsoft Teams
ms.topic: reference
ms.author: lajanuar
ms.localizationpriority: medium
keywords: teams 清单架构
ms.openlocfilehash: 57936f553d07d984f819c8af84c6a9bfd0a1f26f
ms.sourcegitcommit: ba911ce3de7d096514f876faf00e4174444e2285
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2021
ms.locfileid: "61178242"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>参考：Microsoft Teams

Teams清单介绍了应用如何集成到 Microsoft Teams 产品。 清单必须符合 托管在 的架构 [`https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json) 。 早期版本 1.0、1.1,..., 和 1.11 也受 URL ("v1.x") 。
有关在每个版本中所做的更改详细信息，请参阅 [清单更改日志](https://github.com/OfficeDev/microsoft-teams-app-schema/releases)。

以下架构示例显示了所有扩展性选项：

## <a name="sample-full-manifest"></a>示例完整清单

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
  "manifestVersion": "1.11",
  "version": "1.0.0",
  "id": "%MICROSOFT-APP-ID%",
  "packageName": "com.example.myapp",
  "localizationInfo": {
    "defaultLanguageTag": "en-us",
    "additionalLanguages": [
      {
        "languageTag": "es-es",
        "file": "en-us.json"
      }
    ]
  },
  "developer": {
    "name": "Publisher Name",
    "websiteUrl": "https://website.com/",
    "privacyUrl": "https://website.com/privacy",
    "termsOfUseUrl": "https://website.com/app-tos",
    "mpnId": "1234567890"
  },
  "name": {
    "short": "Name of your app (<=30 chars)",
    "full": "Full name of app, if longer than 30 characters (<=100 chars)"
  },
  "description": {
    "short": "Short description of your app (<= 80 chars)",
    "full": "Full description of your app (<= 4000 chars)"
  },
  "icons": {
    "outline": "A relative path to a transparent .png icon — 32px X 32px",
    "color": "A relative path to a full color .png icon — 192px X 192px"
  },
  "accentColor": "A valid HTML color code.",
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "scopes": [
        "team",
        "groupchat"
      ],
      "canUpdateConfiguration": true,
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel",
        "meetingStage"
      ],
      "sharePointPreviewImage": "Relative path to a tab preview image for use in SharePoint — 1024px X 768",
      "supportedSharePointHosts": [
         "sharePointFullPage",
         "sharePointWebPart"
      ]
    }
  ],
  "staticTabs": [
    {
      "entityId": "unique Id for the page entity",
      "scopes": [
        "personal"
      ],
      "context":[
        "personalTab",
        "channelTab"
        ],
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content (displayed in Teams canvas)",
      "websiteUrl": "https://contoso.com/content (displayed in web browser)",
       "searchUrl":  "https://contoso.com/content (displayed in web browser)"
    }
  ],
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "scopes": [
        "team",
        "personal",
        "groupchat"
      ],
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "supportsFiles": true,
      "supportsCalling": false,
      "supportsVideo": true,
      "commandLists": [
        {
          "scopes": [
            "team",
            "groupchat"
          ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command 2",
              "description": "Description of Command 2"
            }
          ]
        },
        {
          "scopes": [
            "personal",
            "groupchat"
          ],
          "commands": [
            {
              "title": "Personal command 1",
              "description": "Description of Personal command 1"
            },
            {
              "title": "Personal command N",
              "description": "Description of Personal command N"
            }
          ]
        }
      ]
    }
  ],
  "connectors": [
    {
      "connectorId": "GUID-FROM-CONNECTOR-DEV-PORTAL%",
      "scopes": [
        "team"
      ],
      "configurationUrl": "https://contoso.com/teamsconnector/configure"
    }
  ],
  "composeExtensions": [
    {
      "canUpdateConfiguration": true,
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "commands": [
        {
          "id": "exampleCmd1",
          "title": "Example Command",
          "type": "query",
          "context": [
            "compose",
            "commandBox"
          ],
          "description": "Command Description; e.g., Search on the web",
          "initialRun": true,
          "fetchTask": false,
          "parameters": [
            {
              "name": "keyword",
              "title": "Search keywords",
              "inputType": "text",
              "description": "Enter the keywords to search for",
              "value": "Initial value for the parameter",
              "choices": [
                {
                  "title": "Title of the choice",
                  "value": "Value of the choice"
                }
              ]
            }
          ]
        },
        {
          "id": "exampleCmd2",
          "title": "Example Command 2",
          "type": "action",
          "context": [
            "message"
          ],
          "description": "Command Description; e.g., Add a customer",
          "initialRun": true,
          "fetchTask": true,
          "parameters": [
            {
              "name": "custinfo",
              "title": "Customer name",
              "description": "Enter a customer name",
              "inputType": "text"
            }
          ]
        },
         {
          "id": "exampleCmd3",
          "title": "Example Command 3",
          "type": "action",
          "context": [
            "compose",
            "commandBox",
            "message"
          ],
          "description": "Command Description; e.g., Add a customer",
          "fetchTask": false,
          "taskInfo": {
            "title": "Initial dialog title",
            "width": "Dialog width",
            "height": "Dialog height",
            "url": "Initial webview URL"
          }
        }
      ],
      "messageHandlers": [
        {
          "type": "link",
          "value": {
            "domains": [
              "mysite.someplace.com",
              "othersite.someplace.com"
            ]
          }
        }
      ]
    }
  ],
"permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "devicePermissions": [
    "geolocation",
    "media",
    "notifications",
    "midi",
    "openExternal"
  ],
  "validDomains": [
    "contoso.com",
    "mysite.someplace.com",
    "othersite.someplace.com"
  ],
  "webApplicationInfo": {
    "id": "AAD App ID",
    "resource": "Resource URL for acquiring auth token for SSO",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelSettings.Read.Group",
      "ChannelSettings.Edit.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "ChannelMessage.Read.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.Edit.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group",
      "Member.ReadWrite.Group",
      "Owner.ReadWrite.Group"
    ]
  },
  "showLoadingIndicator": false,
  "isFullScreen": false,
  "activities": {
    "activityTypes": [
      {
        "type": "taskCreated",
        "description": "Task created activity",
        "templateText": "<team member> created task <taskId> for you"
      },
      {
        "type": "userMention",
        "description": "Personal mention activity",
        "templateText": "<team member> mentioned you"
      }
    ]
  },
  "defaultBlockUntilAdminAction": true,
  "publisherDocsUrl": "https://website.com/app-info",
  "defaultInstallScope": "meetings",
  "defaultGroupCapability": {
    "meetings": "tab", 
    "team": "bot", 
    "groupchat": "bot"
  },
 "configurableProperties": [
     "name",
     "shortDescription",
     "longDescription",
     "smallImageUrl", 
     "largeImageUrl", 
     "accentColor",
     "developerUrl",
     "privacyUrl",
     "termsOfUseUrl"        
 ],
  "subscriptionOffer": {
    "offerId": "publisherId.offerId"
  }
}
```

该架构定义以下属性：

## <a name="schema"></a>$schema

可选，但建议使用 string

引用 https:// JSON 架构的 URL。

## <a name="manifestversion"></a>manifestVersion

**必需**-string

此清单使用的清单架构版本。 必须为 1.10。

## <a name="version"></a>version

**必需**-string

特定应用的版本。 在清单中更新某些内容时，版本也必须递增。 这样，在安装新清单时，它会覆盖现有清单，并且用户会收到新功能。 当此应用提交到应用商店时，必须重新提交并重新验证新的清单。 应用用户会在清单获得批准后的数小时内自动收到新的更新清单。

如果应用程序对权限的请求更改，将提示用户升级并重新与应用进行升级。

此版本字符串必须遵循 [Semver](http://semver.org/) 标准 (MAJOR。MINOR。PATCH) 。

## <a name="id"></a>id

**必需**- Microsoft 应用 ID

ID 是 Microsoft 为应用生成的唯一标识符。 如果你的自动程序通过 Microsoft Bot Framework 注册，则你有一个 ID。 如果你的选项卡的 Web 应用已经使用 Microsoft 登录，你有一个 ID。 必须在此处输入 ID。 否则，必须在 Microsoft 应用程序注册门户[中生成一个新 ID。](https://aka.ms/appregistrations) 如果添加自动程序，请使用同一 ID。

> [!NOTE]
> 如果你要向 AppSource 中的现有应用提交更新，则清单中的 ID 不得修改。

## <a name="developer"></a>developer

**必需**—object

指定有关贵公司的信息。 对于提交到应用商店Teams，这些值必须与应用商店一览中的信息匹配。 有关详细信息，请参阅应用商店Teams[指南](~/concepts/deploy-and-publish/appsource/publish.md)。

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`name`|32 个字符|✔|开发人员显示名称的指南。|
|`websiteUrl`|2048 个字符|✔|the https:// URL to the developer's website. 此链接必须将用户指向你的公司或特定于产品的登陆页面。|
|`privacyUrl`|2048 个字符|✔|the https:// URL to the developer's privacy policy.|
|`termsOfUseUrl`|2048 个字符|✔|the https:// URL to the developer's use terms.|
|`mpnId`|10 个字符| |**可选** 标识生成应用的合作伙伴组织的 Microsoft 合作伙伴网络 ID。|

## <a name="name"></a>name

**必需**—object

应用体验的名称，在应用体验中向Teams显示。 对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。 和 `short` `full` 的值必须不同。

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`short`|30 个字符|✔|应用的显示名称。|
|`full`|100 个字符||应用的完整名称，在完整应用名称超过 30 个字符时使用。|

## <a name="description"></a>说明

**必需**—object

向用户描述你的应用。 对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。

确保你的描述描述你的体验，并帮助潜在客户了解你的体验。 如果需要使用外部帐户，则必须在完整说明中记下。 和 `short` `full` 的值必须不同。 简短说明不能在详细说明中重复，并且不得包含任何其他应用名称。

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`short`|80 个字符|✔|应用体验的简短说明，在空间有限时使用。|
|`full`|4000 个字符|✔|应用的完整说明。|

## <a name="packagename"></a>packageName

**可选**—string

反向域表示法的应用的唯一标识符;例如，com.example.myapp。 最大长度：64 个字符。

## <a name="localizationinfo"></a>localizationInfo

**可选**—object

允许指定默认语言并提供指向更多语言文件的指针。 有关详细信息，请参阅 [本地化](~/concepts/build-and-test/apps-localization.md)。

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`defaultLanguageTag`||✔|此顶级清单文件中字符串的语言标记。|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

指定更多语言翻译的对象数组。

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`languageTag`||✔|提供的文件中字符串的语言标记。|
|`file`||✔|包含已翻译字符串的 .json 文件的相对文件路径。|

## <a name="icons"></a>图标

**必需**—object

应用中使用的Teams图标。 图标文件必须作为上传程序包的一部分包含在内。 有关详细信息， [请参阅图标](../../concepts/build-and-test/apps-package.md#app-icons)。

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`outline`|32 x 32 像素|✔|指向透明 32x32 PNG 大纲图标的相对文件路径。|
|`color`|192 x 192 像素|✔|完整颜色 192x192 PNG 图标的相对文件路径。|

## <a name="accentcolor"></a>accentColor

**必需**— HTML 十六进制颜色代码

要用作边框图标背景的颜色。

该值必须是以"#"开头的有效 HTML 颜色代码，例如 `#4464ee` 。

## <a name="configurabletabs"></a>configurableTabs

**可选**—array

当你的应用体验具有团队频道选项卡体验时，需要在添加前进行额外配置。 可配置的选项卡仅在 和 作用域 `team` 中 `groupchat` 受支持，你可以多次配置相同的选项卡。 但是，只能在清单中定义它一次。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`configurationUrl`|string|2048 个字符|✔|配置 https:// 时将使用的 URL。|
|`scopes`|枚举数组|1|✔|目前，可配置的选项卡仅支持 `team` 和 `groupchat` 作用域。 |
|`canUpdateConfiguration`|boolean|||一个值，指示用户创建后是否可以更新选项卡配置的实例。 默认值 **：true**。|
|`context` |枚举数组|6 ||支持选项卡的范围 `contextItem` [集](../../tabs/how-to/access-teams-context.md)。 默认值 **：[channelTab、privateChatTab、meetingChatTab、meetingDetailsTab]**。|
|`sharePointPreviewImage`|string|2048||选项卡预览图像的相对文件路径，用于SharePoint。 大小 1024x768。 |
|`supportedSharePointHosts`|枚举数组|1||定义选项卡如何可用于SharePoint。 选项为 `sharePointFullPage` 和 `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**可选**—array

定义一组默认情况下可以"固定"的选项卡，而无需用户手动添加它们。 范围中声明 `personal` 的静态选项卡始终固定到应用的个人体验。 作用域中声明的 `team` 静态选项卡当前不受支持。

此项是一个数组 (类型的所有元素) 最多包含 16 个元素 `object` 。 只有提供静态选项卡解决方案的解决方案才需要此块。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`entityId`|string|64 个字符|✔|选项卡显示的实体的唯一标识符。|
|`name`|string|128 个字符|✔|the 显示名称 of the tab in the channel interface.|
|`contentUrl`|string||✔|指向要 https:// 画布中的实体 UI 的Teams URL。|
|`websiteUrl`|string|||The https:// URL to point to if a user opts to view in a browser.|
|`searchUrl`|string|||The https:// URL to point to for a user's search queries.|
|`scopes`|枚举数组|1|✔|目前，静态选项卡仅支持范围，这意味着只能将作用域预配 `personal` 为个人体验的一部分。|
|`context` | 枚举数组| 2|| 支持选项卡的范围 `contextItem` 集。|

> [!NOTE]
>  第三方开发人员无法使用 searchUrl 功能。
> 如果你的选项卡需要上下文相关信息来显示相关内容或启动身份验证流，有关详细信息，请参阅获取你的Microsoft Teams[上下文。](../../tabs/how-to/access-teams-context.md)

## <a name="bots"></a>bots

**可选**—array

定义自动程序解决方案以及默认命令属性等可选信息。

该项目是一个数组 (，当前每个应用最多只能有一个自动程序) 类型的所有元素 &mdash; `object` 。 只有提供自动程序体验的解决方案才需要此块。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`botId`|string|64 个字符|✔|使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。 ID 可以与整个应用 ID [相同](#id)。|
|`scopes`|枚举数组|3|✔|指定自动程序是在 `team` 内的频道上下文中提供体验、在群组聊天 (`groupchat`) 中提供体验，还是仅在单个用户 (`personal`) 范围内提供体验。 这些选项不具排他性。|
|`needsChannelSelector`|boolean|||描述机器人是否使用用户提示将机器人添加到特定频道。 默认值： **`false`**|
|`isNotificationOnly`|boolean|||指示自动程序是否为单向、仅通知的自动程序，而不是对话自动程序。 默认值： **`false`**|
|`supportsFiles`|boolean|||指示自动程序是否支持在个人聊天中上传/下载文件。 默认值： **`false`**|
|`supportsCalling`|boolean|||指示自动程序支持音频呼叫位置的值。 **重要** 提示：此属性当前为实验属性。 实验属性可能不完整，并且可能在完全可用之前发生更改。  该属性仅供测试和探索使用，不得在生产应用程序中使用。 默认值： **`false`**|
|`supportsVideo`|boolean|||指示机器人支持视频呼叫位置的值。 **重要** 提示：此属性当前为实验属性。 实验属性可能不完整，并且可能在完全可用之前发生更改。  该属性仅供测试和探索使用，不得在生产应用程序中使用。 默认值： **`false`**|

### <a name="botscommandlists"></a>bots.commandLists

自动程序可以推荐给用户的命令的可选列表。 对象是一个 (，最多包含两个元素) 所有类型元素;您必须为自动程序支持的每个范围定义单独的 `object` 命令列表。 有关详细信息，请参阅自动 [程序菜单](~/bots/how-to/create-a-bot-commands-menu.md)。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`items.scopes`|枚举数组|3|✔|指定命令列表有效的作用域。 选项包括 `team`、`personal` 和 `groupchat`。|
|`items.commands`|对象数组|10 |✔|自动程序支持的命令数组：<br>`title`：自动程序命令名称（字符串，32）<br>`description`：命令语法及其参数的简单说明或示例， (字符串，128) 。|

### <a name="botscommandlistscommands"></a>bots.commandLists.commands

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|title|string|12 |✔|自动程序命令名称。|
|说明|string|128 个字符|✔|简单文本说明或命令语法及其参数的示例。|

## <a name="connectors"></a>连接器

**可选**—array

`connectors`块为应用Office 365连接器。

对象是一个数组， (类型的所有元素) 一个元素 `object` 。 只有提供连接器的解决方案才需要此块。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`configurationUrl`|string|2048 个字符|✔|配置 https:// 时将使用的 URL。|
|`scopes`|枚举数组|1|✔|指定连接器是提供在 中频道上下文中的体验，还是仅针对单个用户或单个用户 `team` `personal` () 。 目前，仅 `team` 支持范围。|
|`connectorId`|string|64 个字符|✔|连接器的唯一标识符，该标识符与连接器开发人员仪表板中的 ID [相匹配](https://aka.ms/connectorsdashboard)。|

## <a name="composeextensions"></a>composeExtensions

**可选**—array

为应用定义消息传递扩展。

> [!NOTE]
> 2017 年 11 月，功能名称从"撰写扩展"更改为"邮件扩展"，但清单名称保持不变，以便现有扩展继续工作。

该项目是一个数组， (类型的所有元素) 一个元素 `object` 。 只有提供邮件扩展的解决方案才需要此块。

|名称| 类型 | 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`botId`|string|64|✔|自动程序支持消息传递扩展的唯一 Microsoft 应用 ID，在 Bot Framework 中注册。 ID 可以与整个应用 ID 相同。|
|`commands`|对象数组|10 |✔|邮件扩展支持的命令数组。|
|`canUpdateConfiguration`|boolean|||一个值，指示用户是否可以更新邮件扩展的配置。 默认值：**False**。|
|`messageHandlers`|对象数组|5||允许满足某些条件时调用应用的处理程序列表。|
|`messageHandlers.type`|string|||消息处理程序的类型。 必须是 `"link"`。|
|`messageHandlers.value.domains`|字符串数组|||链接邮件处理程序可以注册的域数组。|

### <a name="composeextensionscommands"></a>composeExtensions.commands

邮件扩展必须声明一个或多个最多包含 10 个命令的命令。 每个命令Microsoft Teams作为从基于 UI 的入口点进行的潜在交互。

每个命令项都是具有以下结构的对象：

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`id`|string|64 个字符|✔|命令的 ID。|
|`title`|string|32 个字符|✔|用户友好命令名称。|
|`type`|string|64 个字符||命令的类型。 或 `query` `action` 之一。 默认值 **：query**。|
|`description`|string|128 个字符||向用户显示以指示此命令用途的说明。|
|`initialRun`|boolean|||布尔值指示命令最初是否运行，没有参数。 默认为 **false**。|
|`context`|字符串数组|3||定义可以从何处调用邮件扩展。 、 `compose` 、 的任意 `commandBox` 组合 `message` 。 默认值为 `["compose","commandBox"]`。|
|`fetchTask`|boolean|||一个布尔值，指示它是否必须动态提取任务模块。 默认为 **false**。|
|`taskInfo`|object|||指定在使用消息传递扩展命令时要预加载的任务模块。|
|`taskInfo.title`|string|64 个字符||初始对话框标题。|
|`taskInfo.width`|string|||对话框宽度 - 以像素为单位的一个数字或默认布局，例如"large"、"medium"或"small"。|
|`taskInfo.height`|string|||对话框高度 - 以像素为单位的一个数字或默认布局，例如"large"、"medium"或"small"。|
|`taskInfo.url`|string|||初始 Web 视图 URL。|
|`parameters`|对象数组|5 个项目|✔|命令采用的参数列表。 最小值：1;最大值：5。|
|`parameters.name`|string|64 个字符|✔|显示在客户端中的参数的名称。 参数名称包含在用户请求中。|
|`parameters.title`|string|32 个字符|✔|参数的用户友好标题。|
|`parameters.description`|string|128 个字符||描述此参数用途的用户友好字符串。|
|`parameters.value`|string|512 个字符||参数的初始值。 当前不支持值|
|`parameters.inputType`|string|128 个字符||定义在任务模块上显示的控件的类型 `fetchTask: true` 。 之一 `text, textarea, number, date, time, toggle, choiceset` 。|
|`parameters.choices`|对象数组|10 个项目||的选项 `choiceset` 。 仅在 为 `parameter.inputType` `choiceset` 时使用 。|
|`parameters.choices.title`|string|128 个字符|✔|选项的标题。|
|`parameters.choices.value`|string|512 个字符|✔|选项的值。|

## <a name="permissions"></a>permissions

**可选**— 字符串数组

的数组，指定应用请求哪些权限，让最终用户 `string` 知道扩展执行什么操作。 以下选项非独占：

* `identity`&emsp;需要用户标识信息。
* `messageTeamMembers`&emsp;需要向团队成员发送直接消息的权限。

在应用更新期间更改这些权限，会导致用户在运行更新后的应用后重复同意过程。 有关详细信息，请参阅 [更新应用](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)。

## <a name="devicepermissions"></a>devicePermissions

**可选**— 字符串数组

在应用请求访问的用户设备上提供本机功能。 选项有：

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**可选**，除非 **有说明** ，否则必选。

应用预期在客户端内加载的网站的有效Teams列表。 域列表可以包含通配符，例如 `*.example.com` ， 。 有效域与域的一个段完全匹配;如果需要匹配，请使用 `a.b.example.com` `*.*.example.com` 。 如果你的选项卡配置或内容 UI 导航到除选项卡配置外任何其他域，则必须在此处指定该域。

**请勿** 在应用中包含要支持的标识提供程序的域。 例如，若要使用 Google ID 进行身份验证，必须重定向到 accounts.google.com，但不得在 `validDomains[]` accounts.google.com。

Teams需要其自己的SharePoint URL 正常运行的应用，其有效域列表中包括"{teamsitedomain}"。

> [!IMPORTANT]
> 不要直接添加或通过通配符添加超出您控制的域。 例如， `yourapp.onmicrosoft.com` 是有效的，但 `*.onmicrosoft.com` 是 无效。

对象是包含类型 的所有元素的数组 `string` 。

## <a name="webapplicationinfo"></a>webApplicationInfo

**可选**—object

提供Azure Active Directory (AAD) 应用 ID 和 Microsoft Graph信息，以帮助用户无缝登录你的应用。 如果你的应用已注册AAD，则必须提供应用 ID。 管理员可以在管理中心内轻松查看权限Teams同意。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`id`|string|36 个字符|✔|AAD应用程序 ID。 此 ID 必须是 GUID。|
|`resource`|string|2048 个字符|✔|用于获取 SSO 身份验证令牌的应用的资源 URL。 </br> **注意：** 如果不使用 SSO，请确保在此字段中向应用清单输入虚拟字符串值，以避免 https://notapplicable 错误响应。 |
|`applicationPermissions`|array of strings|128 个字符||指定具体 [资源特定许可](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)。|

## <a name="showloadingindicator"></a>showLoadingIndicator

**可选**—boolean

指示在加载应用或选项卡时是否显示加载指示器。 默认为 **false**。
>[!NOTE]
>如果在应用清单中选择 true，若要正确加载页面，请修改选项卡和任务模块的内容页，如显示本机加载指示器文档 `showLoadingIndicator` 中所述。 [](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)


## <a name="isfullscreen"></a>isFullScreen

 **可选**—boolean

指示在具有或没有选项卡标题栏的情况下呈现个人应用。 默认为 **false**。

> [!NOTE]
> `isFullScreen`仅适用于选项卡SharePoint存储应用。

## <a name="activities"></a>activities

**可选**—object

定义应用用于发布用户活动源的属性。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`activityTypes`|对象数组|128 项| | 提供你的应用可以发布给用户活动源的活动类型。|

### <a name="activitiesactivitytypes"></a>activities.activityTypes

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`type`|string|32 个字符|✔|通知类型。 *请参阅下文*。|
|`description`|string|128 个字符|✔|通知的简要说明。 *请参阅下文*。|
|`templateText`|string|128 个字符|✔|例如："{actor} 已创建任务 {taskId}"|

```json
{
   "activities":{
      "activityTypes":[
         {
            "type":"taskCreated",
            "description":"Task Created Activity",
            "templateText":"{actor} created task {taskId} for you"
         },
         {
            "type":"teamMention",
            "description":"Team Mention Activity",
            "templateText":"{actor} mentioned team"
         },
         {
            "type":"channelMention",
            "description":"Channel Mention Activity",
            "templateText":"{actor} mentioned channel"
         },
         {
            "type":"userMention",
            "description":"Personal Mention Activity",
            "templateText":"{actor} mentioned user"
         },
         {
            "type":"calendarForward",
            "description":"Forwarding a Calendar Event",
            "templateText":"{actor} sent user an invite on behalf of {eventOwner}"
         },
         {
            "type":"calendarForward",
            "description":"Forwarding a Calendar Event",
            "templateText":"{actor} sent user an invite on behalf of {eventOwner}"
         },
         {
            "type":"creatorTaskCreated",
            "description":"Created Task Created",
            "templateText":"The Creator created task {taskId} for you"
         }
      ]
   }
}
```

***

## <a name="defaultinstallscope"></a>defaultInstallScope

**可选** - string

指定默认情况下为此应用定义的安装范围。 定义的范围将是当用户尝试添加应用时按钮上显示的选项。 选项有：
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a>defaultGroupCapability

**可选** - object

选择组安装范围后，它将在用户安装应用时定义默认功能。 选项有：
* `team`
* `groupchat`
* `meetings`
 
|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`team`|string|||当选择的安装范围为 `team` 时，此字段指定可用的默认功能。 选项 `tab` ：、 `bot` 或 `connector` 。|
|`groupchat`|string|||当选择的安装范围为 `groupchat` 时，此字段指定可用的默认功能。 选项 `tab` ：、 `bot` 或 `connector` 。|
|`meetings`|string|||当选择的安装范围为 `meetings` 时，此字段指定可用的默认功能。 选项 `tab` ：、 `bot` 或 `connector` 。|

## <a name="configurableproperties"></a>configurableProperties

**可选** - 数组

`configurableProperties`此块定义管理员可Teams的应用程序属性。 有关详细信息，请参阅启用 [应用自定义](~/concepts/design/enable-app-customization.md)。 自定义或 LOB 应用中不支持应用自定义功能。

> [!NOTE]
> 必须定义至少一个属性。 最多可以在此块中定义九个属性。

可以定义以下任一属性：

* `name`：应用显示名称。
* `shortDescription`：应用的简短说明。
* `longDescription`：应用的详细说明。
* `smallImageUrl`：应用的大纲图标。
* `largeImageUrl`：应用的颜色图标。
* `accentColor`：用于边框图标的颜色和背景。
* `developerUrl`：开发人员网站的 HTTPS URL。
* `privacyUrl`：开发人员隐私策略的 HTTPS URL。
* `termsOfUseUrl`：开发人员使用条款的 HTTPS URL。

## <a name="defaultblockuntiladminaction"></a>defaultBlockUntilAdminAction

**可选**—boolean
 
当 `defaultBlockUntilAdminAction` 属性设置为 **true** 时，应用默认向用户隐藏，直到管理员允许它。 如果设置为 **true，** 则应用将隐藏所有租户和最终用户。 租户管理员可以在管理中心内查看Teams，并采取措施以允许或阻止该应用。 默认值为 **false**。 有关默认应用块详细信息，请参阅隐藏[Teams应用，直到管理员批准](~/concepts/design/enable-app-customization.md#hide-teams-app-until-admin-approves)。

## <a name="publisherdocsurl"></a>publisherDocsUrl

**可选** - string

**最大大小** - 128 个字符

属性依赖于 `defaultBlockUntilAdminAction` 。 当 属性设置为 true 时，提供指向信息页的 HTTPS URL，以便管理员在允许应用（默认情况下被阻止）之前 `defaultBlockUntilAdminAction`  `publisherDocsUrl` 获取指南。

## <a name="subscriptionoffer"></a>subscriptionOffer

**可选** - object

指定与你的应用关联的 SaaS 产品/服务。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`offerId`| string | 2，048 个字符 | ✔ | 包含你的产品/服务 ID Publisher产品/服务 ID 的唯一标识符，可在合作伙伴[中心找到](https://partner.microsoft.com/dashboard)。 必须将字符串格式为 `publisherId.offerId` 。|

## <a name="see-also"></a>另请参阅

* [了解Microsoft Teams应用程序结构](~/concepts/design/app-structure.md)
* [启用应用自定义](~/concepts/design/enable-app-customization.md)
* [本地化应用](~/concepts/build-and-test/apps-localization.md)
* [集成媒体功能](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [开发者预览版清单架构参考 - Teams](~/resources/schema/manifest-schema-dev-preview.md)
