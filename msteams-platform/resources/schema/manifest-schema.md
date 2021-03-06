---
title: 清单架构参考
description: 介绍 Microsoft Teams 的清单架构
ms.topic: reference
ms.author: lajanuar
keywords: 团队清单架构
ms.openlocfilehash: 291d748d546dec16fa4bf748318b8749b7d0275d
ms.sourcegitcommit: 9cfbc44912980a33d2d7c7c85739aeea6ccb41de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "50479851"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>参考：Microsoft Teams 的清单架构

Teams 清单介绍了应用如何集成到 Microsoft Teams 产品。 清单必须符合托管在 的架构 [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json) 。 早期版本 1.0-1.4 也受 URL ("v1.x"支持) 。

以下架构示例显示了所有扩展性选项。

## <a name="sample-full-manifest"></a>示例完整清单

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.8",
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
          "description": "Command Description; e.g., Search for a customer",
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
        }
      ],
      "taskInfo": {
        "title": "Initial dialog title",
        "width": "Dialog width",
        "height": "Dialog height",
        "url": "Initial webview URL"
      },
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
    ],
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
  "defaultInstallScope": {
     "type": "string",
     "enum": [
        "personal",
        "team",
        "groupchat",
        "meetings"
      ],
      "description": "The install scope is defined for this app by default. It is the option displayed on the button when a user tries to add the app."
    },
  "defaultGroupCapability": {
      "type": "object",
      "properties": {
        "team": {
          "type": "string",
          "enum": [
            "tab",
            "bot",
            "connector"
          ],
          "description": "When the selected install scope is Team, this field specifies the default capability available."
    },
    "groupchat": {
      "type": "string",
      "enum": [
            "tab",
            "bot",
            "connector"
      ],
      "description": "When the selected install scope is Group Chat, this field specifies the default capability available."
    },
    "meetings": {
      "type": "string",
      "enum": [
            "tab",
            "bot",
            "connector"
      ],
      "description": "When the selected install scope is Meetings, this field specifies the default capability available."
      }
    },
    "description": "When a group install scope is selected, this defines the default capability when the user installs the app.",
    "additionalProperties": false

}
```

架构定义以下属性：

## <a name="schema"></a>$schema

可选，但建议使用字符串

引用https:// JSON 架构的 URL。

## <a name="manifestversion"></a>manifestVersion

**必需** — 字符串

此清单使用的清单架构版本。 它必须是 1.7。

## <a name="version"></a>version

**必需** — 字符串

特定应用的版本。 如果更新清单中的某些内容，则版本也必须递增。 这样，在安装新清单时，它将覆盖现有清单，并且用户会收到新功能。 如果此应用已提交到应用商店，则必须重新提交和重新验证新清单。 应用用户会在清单获得批准后的几小时内自动收到新的更新清单。

如果应用对权限的请求更改，系统将提示用户升级并重新同意应用。

此版本字符串必须遵循 [Semver](http://semver.org/) 标准 (MAJOR。MINOR。PATCH) 。

## <a name="id"></a>id

**必需** — Microsoft 应用 ID

ID 是 Microsoft 为应用生成的唯一标识符。 如果你的机器人通过 Microsoft Bot Framework 注册，或者你的选项卡的 Web 应用已登录 Microsoft，则你有一个 ID。 必须在此处输入 ID。 否则，必须在"我的应用程序" ([Microsoft](https://apps.dev.microsoft.com) 应用程序注册门户) 。 如果添加自动程序，请使用同一 ID。

> [!NOTE]
> 如果你要向 AppSource 中的现有应用提交更新，则不得修改清单中的 ID。

## <a name="developer"></a>developer

**必需** — 对象

提供有关你的公司的信息。 对于提交到 AppSource (以前为 Office 应用商店) ，这些值必须与 AppSource 条目中的信息匹配。 有关 [其他信息，](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) 请参阅发布指南。

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`name`|32 个字符|✔|开发人员显示名称的指南。|
|`websiteUrl`|2048 个字符|✔|https://网站的 URL。 此链接必须将用户带至你的公司或特定于产品的登陆页面。|
|`privacyUrl`|2048 个字符|✔|该https://指向开发人员隐私策略的 URL。|
|`termsOfUseUrl`|2048 个字符|✔|https://开发人员使用条款的 URL。|
|`mpnId`|10 个字符| |**可选** 标识生成应用的合作伙伴组织的 Microsoft 合作伙伴网络 ID。|

## <a name="name"></a>name

**必需** — 对象

在 Teams 体验中向用户显示的应用体验名称。 对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。 值 `short` 和 `full` 的值必须不同。

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`short`|30 个字符|✔|应用的显示名称的简短设置。|
|`full`|100 个字符||应用的完整名称，在完整应用名称超过 30 个字符时使用。|

## <a name="description"></a>说明

**必需** — 对象

向用户描述你的应用。 对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。

确保你的说明准确地描述你的体验，并提供可帮助潜在客户了解你的体验所完成操作的信息。 如果需要使用外部帐户，则必须在完整说明中记下。 值和 `short` `full` 的值必须不同。 简短说明不得在长描述中重复，且不得包含任何其他应用名称。

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`short`|80 个字符|✔|应用体验的简短说明，在空间有限时使用。|
|`full`|4000 个字符|✔|应用的完整说明。|

## <a name="packagename"></a>packageName

**可选** — 字符串

反向域表示法中应用的唯一标识符;例如，com.example.myapp。 最大长度：64 个字符。

## <a name="localizationinfo"></a>localizationInfo

**可选** — 对象

允许指定默认语言，以及指向其他语言文件的指针。 请参阅 [本地化](~/concepts/build-and-test/apps-localization.md)。

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`defaultLanguageTag`||✔|此顶级清单文件中字符串的语言标记。|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

指定其他语言翻译的对象数组。

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`languageTag`||✔|提供的文件中字符串的语言标记。|
|`file`||✔|指向包含已翻译字符串的 .json 文件的相对文件路径。|

## <a name="icons"></a>图标

**必需** — 对象

Teams 应用中使用的图标。 图标文件必须作为上传包的一部分包含在内。 有关详细信息 [，](../../concepts/build-and-test/apps-package.md#app-icons) 请参阅"图标"。

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`outline`|32 x 32 像素|✔|指向透明 32x32 PNG 大纲图标的相对文件路径。|
|`color`|192 x 192 像素|✔|完整颜色 192x192 PNG 图标的相对文件路径。|

## <a name="accentcolor"></a>accentColor

**可选** — HTML 十六进制颜色代码

要与大纲图标结合使用并用作背景的颜色。

值必须是以"#"开头的有效 HTML 颜色代码，例如 `#4464ee` 。

## <a name="configurabletabs"></a>configurableTabs

**可选** — 数组

当你的应用体验具有团队频道选项卡体验时，需要在添加前进行额外配置时使用。 可配置的选项卡仅在团队作用域 (不支持个人) ，并且当前每个应用仅支持一个选项卡。 

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`configurationUrl`|string|2048 个字符|✔|配置https://时将使用的 URL。|
|`scopes`|枚举数组|1 |✔|目前，可配置的选项卡仅支持 `team` 和 `groupchat` 范围。 |
|`canUpdateConfiguration`|boolean|||一个值，指示用户创建后是否可以更新选项卡配置的实例。 默认值 **：true**。|
|`context` |枚举数组|6 ||支持选项卡的范围 `contextItem` 集。 默认值 **：[channelTab、privateChatTab、meetingChatTab、meetingDetailsTab]**。|
|`sharePointPreviewImage`|string|2048||选项卡预览图像的相对文件路径，用于 SharePoint。 大小 1024x768。 |
|`supportedSharePointHosts`|枚举数组|1 ||定义如何在 SharePoint 中提供选项卡。 选项 `sharePointFullPage` 包括和 `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**可选** — 数组

定义一组默认情况下可以"固定"的选项卡，而无需用户手动添加它们。 在范围中声明 `personal` 的静态选项卡始终固定到应用的个人体验。 当前不支持在范围 `team` 中声明的静态选项卡。

此项是一个数组 (类型的所有元素) 最多包含 16 个元素 `object` 。 只有提供静态选项卡解决方案的解决方案才需要此块。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`entityId`|string|64 个字符|✔|选项卡显示的实体的唯一标识符。|
|`name`|string|128 个字符|✔|显示名称界面中选项卡的显示内容。|
|`contentUrl`|string||✔|指向要显示在 Teams 画布中的实体 UI 的 https:// URL。|
|`websiteUrl`|string|||用户https://浏览器中查看时要指向的 URL。|
|`searchUrl`|string|||要https://搜索查询的 URL。|
|`scopes`|枚举数组|1 |✔|目前，静态选项卡仅支持范围，这意味着只能将范围预配为个人 `personal` 体验的一部分。|
|`context` | 枚举数组| 2 || 支持选项卡的范围 `contextItem` 集。|

> [!NOTE]
> 如果你的选项卡需要依赖上下文的信息来显示相关内容或启动身份验证流，请参阅"获取[Microsoft Teams"选项卡的上下文](../../tabs/how-to/access-teams-context.md)。

## <a name="bots"></a>自动程序

**可选** — 数组

定义自动程序解决方案以及可选信息（如默认命令属性）。

该项目是一个数组 (，当前每个应用仅允许一个自动程序) 类型的所有元素 &mdash; `object` 。 只有提供自动程序体验的解决方案才需要此块。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`botId`|string|64 个字符|✔|使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。 这可能与整体应用 [ID 相同](#id)。|
|`scopes`|枚举数组|3 |✔|指定自动程序是在 `team` 内的频道上下文中提供体验、在群组聊天 (`groupchat`) 中提供体验，还是仅在单个用户 (`personal`) 范围内提供体验。 这些选项不具排他性。|
|`needsChannelSelector`|boolean|||描述自动程序是否利用用户提示将自动程序添加到特定频道。 默认值： **`false`**|
|`isNotificationOnly`|boolean|||指示自动程序是否为单向、仅通知的自动程序，而不是对话自动程序。 默认值： **`false`**|
|`supportsFiles`|boolean|||指示自动程序是否支持在个人聊天中上传/下载文件。 默认值： **`false`**|
|`supportsCalling`|boolean|||指示自动程序支持音频呼叫位置的值。 **重要** 提示：此属性当前是实验性的。 实验属性可能不完整，并且可能在完全可用之前发生更改。  它仅用于测试和探索目的，不得在生产应用程序中使用。 默认值： **`false`**|
|`supportsVideo`|boolean|||指示机器人支持视频呼叫位置的值。 **重要** 提示：此属性当前是实验性的。 实验属性可能不完整，并且可能在完全可用之前发生更改。  它仅用于测试和探索目的，不得在生产应用程序中使用。 默认值： **`false`**|

### <a name="botscommandlists"></a>bots.commandLists

自动程序可以推荐给用户的命令的可选列表。 该对象是一个数组 (包含最多 2 个元素) 所有类型元素;您必须为自动程序支持的每个范围定义单独的 `object` 命令列表。 有关详细信息 [，请参阅自动](~/bots/how-to/create-a-bot-commands-menu.md) 程序菜单。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`items.scopes`|枚举数组|3 |✔|指定命令列表有效的作用域。 选项包括 `team`、`personal` 和 `groupchat`。|
|`items.commands`|对象数组|10  |✔|自动程序支持的命令数组：<br>`title`：自动程序命令名称（字符串，32）<br>`description`：命令语法及其参数的简单描述或示例（字符串，128）|

### <a name="botscommandlistscommands"></a>bots.commandLists.commands

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|title|string|12 |✔|自动程序命令名称|
|说明|string|128 个字符|✔|简单文本说明或命令语法及其参数的示例。|

## <a name="connectors"></a>连接器

**可选** — 数组

此 `connectors` 块为应用定义 Office 365 连接器。

对象是一个数组， (类型元素) 1 个元素 `object` 。 只有提供连接器的解决方案才需要此块。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`configurationUrl`|string|2048 个字符|✔|配置https://时将使用的 URL。|
|`scopes`|枚举数组|1 |✔|指定连接器是提供在 a 中频道上下文中的体验，还是仅针对单个用户 `team` `personal` () 。 目前，仅 `team` 支持范围。|
|`connectorId`|string|64 个字符|✔|连接器的唯一标识符，与连接器开发人员仪表板中的 ID [相匹配](https://aka.ms/connectorsdashboard)。|

## <a name="composeextensions"></a>composeExtensions

**可选** — 数组

定义应用的消息扩展。

> [!NOTE]
> 功能的名称在 2017 年 11 月从"撰写扩展"更改为"邮件扩展"，但清单名称保持不变，以便现有扩展继续工作。

该项目是一个数组， (类型的所有元素) 最多包含 1 个元素 `object` 。 只有提供邮件扩展的解决方案才需要此块。

|名称| 类型 | 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`botId`|string|64|✔|自动程序支持消息传递扩展的唯一 Microsoft 应用 ID，如在 Bot Framework 中注册的。 这可能与整体应用 ID 相同。|
|`commands`|对象数组|10  |✔|邮件扩展支持的命令数组|
|`canUpdateConfiguration`|boolean|||一个值，指示用户是否可以更新邮件扩展的配置。 默认值：**False**。|
|`messageHandlers`|对象数组|5 ||允许当满足特定条件时调用应用的处理程序列表。|
|`messageHandlers.type`|string|||邮件处理程序的类型。 必须是 `"link"`。|
|`messageHandlers.value.domains`|字符串数组|||链接消息处理程序可以注册的域数组。|

### <a name="composeextensionscommands"></a>composeExtensions.commands

邮件扩展必须声明一个或多个命令。 每个命令在 Microsoft Teams 中显示为基于 UI 的入口点的潜在交互。 最多有 10 个命令。

每个命令项都是具有以下结构的对象：

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`id`|string|64 个字符|✔|命令的 ID。|
|`title`|string|32 个字符|✔|用户友好命令名称。|
|`type`|string|64 个字符||命令的类型。 或 `query` `action` 。 默认值： **查询**。|
|`description`|string|128 个字符||向用户显示的说明，用于指示此命令的用途。|
|`initialRun`|boolean|||布尔值指示命令最初是否运行，没有参数。 默认为 **false**。|
|`context`|字符串数组|3 ||定义可以从何处调用邮件扩展。 `compose`， 的任意 `commandBox` 组合 `message` 。 默认值为“`["compose","commandBox"]`”。|
|`fetchTask`|boolean|||一个布尔值，指示它是否必须动态获取任务模块。 默认为 **false**。|
|`taskInfo`|object|||指定在使用邮件扩展命令时要预加载的任务模块。|
|`taskInfo.title`|string|64 个字符||初始对话框标题。|
|`taskInfo.width`|string|||对话框宽度 - 以像素为单位的一个数字或默认布局，如"large"、"medium"或"small"。|
|`taskInfo.height`|string|||对话框高度 - 以像素为单位的一个数字或默认布局，如"large"、"medium"或"small"。|
|`taskInfo.url`|string|||初始 Web 视图 URL。|
|`parameters`|对象的数组|5 个项目|✔|命令采用的参数列表。 最小值：1;最大值：5。|
|`parameters.name`|string|64 个字符|✔|在客户端中显示的参数的名称。 这包含在用户请求中。|
|`parameters.title`|string|32 个字符|✔|参数的用户友好标题。|
|`parameters.description`|string|128 个字符||描述此参数用途的用户友好字符串。|
|`parameters.value`|string|512 个字符||参数的初始值。|
|`parameters.inputType`|string|128 个字符||定义在任务模块上显示的控件的类型 `fetchTask: true` 。 之一 `text, textarea, number, date, time, toggle, choiceset` 。|
|`parameters.choices`|对象数组|10 个项目||`choiceset`的选项。 仅在为 `parameter.inputType` `choiceset` 时使用。|
|`parameters.choices.title`|string|128 个字符|✔|选项的标题。|
|`parameters.choices.value`|string|512 个字符|✔|选项的值。|

## <a name="permissions"></a>权限

**可选** — 字符串数组

一个数组，用于指定应用程序请求的权限，使 `string` 最终用户知道扩展执行方式。 以下选项是非独占的：

* `identity`&emsp;需要用户标识信息
* `messageTeamMembers`&emsp;需要向团队成员发送直接消息的权限

在应用更新期间更改这些权限会导致用户在运行更新的应用后重复同意过程。 有关详细信息 [，请参阅更新](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) 应用。

## <a name="devicepermissions"></a>devicePermissions

**可选** — 字符串数组

在应用请求访问的用户设备上提供本机功能。 选项包括：

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**可选**，除非 **有说明** ，但必需

应用预期在 Teams 客户端内加载的网站的有效域列表。 域列表可以包含通配符，例如 `*.example.com` 。 这完全匹配域的一个段;如果需要匹配，请使用 `a.b.example.com` `*.*.example.com` 。 如果你的选项卡配置或内容 UI 需要导航到除用于选项卡配置的域之外的其他任何域，则必须在此处指定该域。

不需要 **在** 应用中包含要支持的标识提供程序的域。 例如，若要使用 Google ID 进行身份验证，必须重定向到 accounts.google.com，但不得在 `validDomains[]` accounts.google.com。

需要自己的 sharepoint URL 正常运行的 Teams 应用在有效域列表中包括"{teamsitedomain}"。

> [!IMPORTANT]
> 不要直接添加或通过通配符添加控件之外的域。 例如， `yourapp.onmicrosoft.com` 有效，但是 `*.onmicrosoft.com` ，无效。

对象是包含类型的所有元素的数组 `string` 。

## <a name="webapplicationinfo"></a>webApplicationInfo

**可选** — 对象

提供 Azure Active Directory (AAD) 应用 ID 和 Microsoft Graph 信息，以帮助用户无缝登录你的应用。 如果你的应用在 AAD 中注册，则必须提供应用 ID，以便管理员可以轻松地在 Teams 管理中心查看权限并授予许可。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`id`|string|36 个字符|✔|应用的 AAD 应用程序 ID。 此 ID 必须是 GUID。|
|`resource`|string|2048 个字符|✔|用于获取 SSO 身份验证令牌的应用的资源 URL。 </br> **注意：** 如果不使用 SSO，请确保在此字段中向应用清单输入虚拟字符串值，例如， https://notapplicable 以避免错误响应。 |
|`applicationPermissions`|array of strings|128 个字符||指定 [具体资源特定许可](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)。|

## <a name="showloadingindicator"></a>showLoadingIndicator

**可选** — 布尔值

指示在加载应用或选项卡时是否显示加载指示器。 默认为 **false**。
>[!NOTE]
>如果在应用清单中选择 true，若要正确加载页面，请修改选项卡和任务模块的内容页，如"显示本机加载指示器文档 `showLoadingIndicator` ["](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) 中所述。


## <a name="isfullscreen"></a>isFullScreen

 **可选** — 布尔值

指示使用选项卡标题栏或不带选项卡标题栏呈现个人应用的地方。 默认为 **false**。

## <a name="activities"></a>activities

**可选** — 对象

定义应用用于发布用户活动源的属性。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`activityTypes`|对象数组|128 个项目| | 提供你的应用可以发布给用户活动源的活动类型。|

### <a name="activitiesactivitytypes"></a>activities.activityTypes

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`type`|string|32 个字符|✔|通知类型。 *请参阅下文*。|
|`description`|string|128 个字符|✔|通知的简要说明。 *请参阅下文*。|
|`templateText`|string|128 个字符|✔|例如："{actor} 已创建任务 {taskId} for you"|

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
>
>
