---
title: 清单架构参考
description: 介绍 Microsoft 团队的清单架构
keywords: 团队清单架构
author: laujan
ms.author: lajanuar
ms.openlocfilehash: e25f50fc8da357553c1f0a8b01dc51af079ed2bb
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604611"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>参考： Microsoft 团队的清单架构

Microsoft 团队清单介绍了应用程序如何集成到 Microsoft 团队产品中。 您的清单必须符合托管的架构 [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json) 。 在 URL) 中使用 "v1" 时，也 (支持早期版本 1.0-1.4。

以下架构示例显示了所有扩展性选项。

## <a name="sample-full-manifest"></a>完整清单示例

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
  }
}
```

架构定义了以下属性：

## <a name="schema"></a>$schema

*可选，但建议* —字符串

引用清单的 JSON 架构的 https://URL。

## <a name="manifestversion"></a>manifestVersion

**必需** -字符串

此清单使用的清单架构的版本。 它应为 "1.7"。

## <a name="version"></a>version

**必需** -字符串

特定应用程序的版本。 如果您更新清单中的某些内容，该版本还必须递增。 这样一来，在安装新的清单时，它将覆盖现有的版本，用户将获得新的功能。 如果此应用程序已提交到应用商店，则必须重新提交新清单，然后再对其进行重新验证。 然后，此应用程序的用户将在几小时内自动获取新更新的清单（在批准后）。

如果应用程序要求更改权限，则系统将提示用户升级并重新同意该应用。

此版本字符串必须遵循 [semver](http://semver.org/) STANDARD (主要版本。网格.PATCH) 。

## <a name="id"></a>id

**必需** — MICROSOFT app ID

Microsoft 为此应用程序生成的唯一标识符。 如果你已通过 Microsoft Bot 框架注册了 bot，或者你的选项卡的 web 应用已使用 Microsoft 登录，则你应该已经有 ID，应在此处输入它。 否则，应在 Microsoft 应用程序注册门户 ([我的应用程序](https://apps.dev.microsoft.com) ") 上生成一个新的 ID，在此处输入它，然后在添加机器人时重用它。注意：如果您在 AppSource 中提交对现有应用程序的更新，您的清单中的 ID 不得修改。

## <a name="developer"></a>developer

**必需** -对象

指定有关贵公司的信息。 对于提交到 AppSource 的应用程序 (以前的 Office 应用商店) ，这些值必须与您的 AppSource 条目中的信息相匹配。 有关详细信息，请参阅我们的 [发布指南](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) 。

|名称| 最大大小 | 必需 | Description|
|---|---|---|---|
|`name`|32个字符|✔|开发人员的显示名称。|
|`websiteUrl`|2048 个字符|✔|开发人员网站的 https://URL。 此链接应将用户带到您的公司或特定于产品的登陆页面。|
|`privacyUrl`|2048 个字符|✔|开发人员的隐私策略的 https://URL。|
|`termsOfUseUrl`|2048 个字符|✔|开发人员使用条款的 https://URL。|
|`mpnId`|10个字符| |**可选** 用于标识合作伙伴组织构建应用程序的 Microsoft 合作伙伴网络 ID。|

## <a name="name"></a>name

**必需** -对象

在团队体验中向用户显示的应用程序体验的名称。 对于提交到 AppSource 的应用程序，这些值必须与您的 AppSource 条目中的信息相匹配。 和的值 `short` `full` 不应相同。

|名称| 最大大小 | 必需 | Description|
|---|---|---|---|
|`short`|30 个字符|✔|应用程序的短显示名称。|
|`full`|100 个字符||应用程序的全名，如果完整的应用程序名称超过30个字符，则使用该名称。|

## <a name="description"></a>说明

**必需** -对象

向用户介绍你的应用程序。 对于提交到 AppSource 的应用程序，这些值必须与您的 AppSource 条目中的信息相匹配。

确保你的说明准确描述你的体验，并提供信息，以帮助潜在客户了解你的体验。 如果需要使用外部帐户，还应在完整说明中说明。 和的值 `short` `full` 不应相同。  您的简短说明不得在详细说明中重复，并且不得包含任何其他应用程序名称。

|名称| 最大大小 | 必需 | Description|
|---|---|---|---|
|`short`|80个字符|✔|在空间有限时使用的应用程序体验的简短说明。|
|`full`|4000个字符|✔|您的应用程序的完整说明。|

## <a name="packagename"></a>packageName

**Optional** -string

此应用的以反向域表示法表示的唯一标识符;例如，.com. myapp。 最大长度：64 个字符。

## <a name="localizationinfo"></a>localizationInfo

**Optional** —对象

允许指定默认语言，以及指向其他语言文件的指针。 请参阅 [本地化](~/concepts/build-and-test/apps-localization.md)。

|名称| 最大大小 | 必需 | Description|
|---|---|---|---|
|`defaultLanguageTag`||✔|此顶级清单文件中的字符串的语言标记。|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

指定其他语言翻译的对象的数组。

|名称| 最大大小 | 必需 | Description|
|---|---|---|---|
|`languageTag`||✔|所提供文件中的字符串的语言标记。|
|`file`||✔|包含翻译字符串的 json 文件的相对文件路径。|

## <a name="icons"></a>图标

**必需** -对象

在团队应用程序中使用的图标。 图标文件必须作为上载包的一部分包括在内。 有关详细信息，请参阅 [图标](../../concepts/build-and-test/apps-package.md#app-icons) 。

|名称| 最大大小 | 必需 | Description|
|---|---|---|---|
|`outline`|32 x 32 像素|✔|指向透明 32x32 PNG 边框图标的相对文件路径。|
|`color`|192 x 192 像素|✔|完整颜色 192x192 PNG 图标的相对文件路径。|

## <a name="accentcolor"></a>accentColor

**可选** — HTML 十六进制颜色代码

与大纲图标的背景一起使用的颜色。

值必须是以 "#" 开头的有效 HTML 颜色代码，例如 `#4464ee` 。

## <a name="configurabletabs"></a>configurableTabs

**Optional** — array

当您的应用程序体验具有在添加之前需要额外配置的团队频道选项卡体验时使用。 只有在不是个人) 的团队 (范围中支持可配置的选项卡，并且每个应用程序目前仅支持 **一个** 选项卡。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`configurationUrl`|string|2048 个字符|✔|配置选项卡时要使用的 https://URL。|
|`scopes`|枚举数组|1 |✔|目前，可配置的选项卡仅支持 `team` 和 `groupchat` 范围。 |
|`canUpdateConfiguration`|boolean|||一个值，指示是否可在用户创建之后更新该选项卡的配置实例。 默认值： **true**。|
|`context` |枚举数组|6 ||`contextItem`支持选项卡的作用域集。 默认值： **[channelTab、privateChatTab、meetingChatTab、meetingDetailsTab]**。|
|`sharePointPreviewImage`|string|2048||要在 SharePoint 中使用的选项卡预览图像的相对文件路径。 字号（1024x768）。 |
|`supportedSharePointHosts`|枚举数组|1 ||定义您的选项卡在 SharePoint 中的可用方式。 选项包括 `sharePointFullPage` 和 `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**Optional** — array

定义一组可在默认情况下 "固定" 的选项卡，而无需用户手动添加它们。 在范围内声明的静态制表符 `personal` 始终固定到应用的个人体验中。 当前不支持在范围中声明的静态选项卡 `team` 。

此项是一个数组， (最多16个元素，) 与所有类型的元素一起使用 `object` 。 仅在提供静态选项卡解决方案的解决方案中，此块是必需的。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`entityId`|string|64 个字符|✔|选项卡显示的实体的唯一标识符。|
|`name`|string|128个字符|✔|该选项卡在通道接口中的显示名称。|
|`contentUrl`|string||✔|指向要在团队画布中显示的实体 UI 的 https://URL。|
|`websiteUrl`|string|||如果用户要在浏览器中查看，则为指向的 https://URL。|
|`searchUrl`|string|||指向用户搜索查询的 https://URL。|
|`scopes`|枚举数组|1 |✔|目前，静态选项卡仅支持 `personal` 作用域，这意味着它只能作为个人体验的一部分进行预配。|
|`context` | 枚举数组| 2 || `contextItem`支持选项卡的作用域集。|

> [!NOTE]
> 如果您的选项卡需要上下文相关信息来显示相关内容或启动身份验证流，*请参阅*[获取 Microsoft 团队的上下文选项卡](../../tabs/how-to/access-teams-context.md)。

## <a name="bots"></a>bot

**Optional** — array

定义机器人解决方案以及可选信息，如默认的命令属性。

Item 是数组 (每个元素最多只能包含1个元素， &mdash; 每个应用程序) 只允许一个 bot 与所有类型的元素一起使用 `object` 。 仅在提供机器人体验的解决方案中，此块才是必需的。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`botId`|string|64 个字符|✔|使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。 这可能与整体 [应用程序 ID](#id)很好。|
|`scopes`|枚举数组|3 |✔|指定自动程序是在 `team` 内的频道上下文中提供体验、在群组聊天 (`groupchat`) 中提供体验，还是仅在单个用户 (`personal`) 范围内提供体验。 这些选项不具排他性。|
|`needsChannelSelector`|boolean|||描述自动程序是否利用用户提示将自动程序添加到特定频道。 设置 **`false`**|
|`isNotificationOnly`|boolean|||指示自动程序是否为单向、仅通知的自动程序，而不是对话自动程序。 设置 `**false**`|
|`supportsFiles`|boolean|||指示自动程序是否支持在个人聊天中上传/下载文件。 设置 **`false`**|
|`supportsCalling`|boolean|||一个值，指示机器人支持音频呼叫的位置。 **重要说明**：此属性当前为实验性。 实验性属性可能不完整，并且可能会在完全可用之前进行更改。  它仅用于测试和研究目的，不应在生产应用程序中使用。 设置 **`false`**|
|`supportsVideo`|boolean|||一个值，指示机器人支持视频通话的位置。 **重要说明**：此属性当前为实验性。 实验性属性可能不完整，并且可能会在完全可用之前进行更改。  它仅用于测试和研究目的，不应在生产应用程序中使用。 设置 **`false`**|

### <a name="botscommandlists"></a>commandLists

你的 bot 可以向用户推荐的命令的可选列表。 对象是数组 (最多为2个元素) 的所有类型的元素 `object` ; 您必须为你的 bot 支持的每个作用域定义单独的命令列表。 有关详细信息，请参阅 [Bot 菜单](~/bots/how-to/create-a-bot-commands-menu.md) 。

|名称| 类型| 最大大小 | 必需 | Description|
|---|---|---|---|---|
|`items.scopes`|枚举数组|3 |✔|指定命令列表有效的作用域。 选项包括 `team`、`personal` 和 `groupchat`。|
|`items.commands`|对象数组|10 |✔|自动程序支持的命令数组：<br>`title`：自动程序命令名称（字符串，32）<br>`description`：命令语法及其参数的简单描述或示例（字符串，128）|

### <a name="botscommandlistscommands"></a>commandLists

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|title|string|12 |✔|Bot 命令名称|
|说明|string|128个字符|✔|一个简单的文本说明或一个命令语法及其参数的示例。|

## <a name="connectors"></a>插槽

**Optional** — array

`connectors`Block 定义了应用程序的 Office 365 连接器。

对象是数组 (最大值为1的元素) 与所有类型的元素一起使用 `object` 。 仅对提供连接器的解决方案而言，此块是必需的。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`configurationUrl`|string|2048 个字符|✔|配置连接器时要使用的 https://URL。|
|`scopes`|枚举数组|1 |✔|指定连接器是在中频道的上下文中 `team` ，还是在仅限于单个用户 () 的体验中提供体验 `personal` 。 目前，仅 `team` 支持作用域。|
|`connectorId`|string|64 个字符|✔|与 [连接器开发人员仪表板](https://aka.ms/connectorsdashboard)中的 ID 相匹配的连接器的唯一标识符。|

## <a name="composeextensions"></a>composeExtensions

**Optional** — array

定义应用程序的消息扩展。

> [!NOTE]
> 功能的名称已从11月2017的 "撰写分机" 更改为 "消息扩展"，但清单名称保持不变，以便现有扩展能够继续正常工作。

Item 是一个数组， (最多1个元素) 与所有类型的元素一起使用 `object` 。 仅对提供邮件扩展的解决方案而言，此块是必需的。

|名称| 类型 | 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`botId`|string|64|✔|与 Bot 框架一起注册的支持邮件扩展的 bot 的唯一 Microsoft 应用 ID。 这可能与整体应用程序 ID 很好。|
|`commands`|对象数组|10 |✔|邮件扩展支持的命令数组|
|`canUpdateConfiguration`|boolean|||一个值，指示用户是否可以更新邮件扩展的配置。 默认值：**False**。|
|`messageHandlers`|对象数组|5 ||允许在满足特定条件时调用应用程序的处理程序列表。 域也必须列在 `validDomains`|
|`messageHandlers.type`|string|||消息处理程序的类型。 必须是 `"link"`。|
|`messageHandlers.value.domains`|字符串数组|||链接消息处理程序可以为其注册的域的数组。|

### <a name="composeextensionscommands"></a>composeExtensions

您的邮件扩展应声明一个或多个命令。 在 Microsoft 团队中，每个命令都显示为从基于 UI 的入口点的潜在交互。 最多可以有10个命令。

每个命令项都是一个具有以下结构的对象：

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`id`|string|64 个字符|✔|命令的 ID。|
|`title`|string|32个字符|✔|用户友好的命令名称。|
|`type`|string|64 个字符||命令的类型。 一个 `query` 或 `action` 。 默认值： **query**。|
|`description`|string|128个字符||对用户显示的说明，用于指示此命令的用途。|
|`initialRun`|boolean|||一个布尔值，指示是否在最初不使用任何参数的情况之下运行该命令。 默认值：**False**。|
|`context`|字符串数组|3 ||定义可以从中调用邮件扩展的位置。 、、的的任意组合 `compose` `commandBox` `message` 。 默认值为 `["compose","commandBox"]`。|
|`fetchTask`|boolean|||一个布尔值，指示是否应动态获取任务模块。 默认值：**False**。|
|`taskInfo`|object|||使用消息扩展命令指定要预加载的任务模块。|
|`taskInfo.title`|string|64 个字符||初始对话框标题。|
|`taskInfo.width`|string|||对话框宽度-以像素为单位的数字或默认布局，如 "大"、"中" 或 "small"。|
|`taskInfo.height`|string|||对话框高度-以像素为单位的数字或默认布局，如 "大"、"中" 或 "small"。|
|`taskInfo.url`|string|||初始的 web 视图 URL。|
|`parameters`|对象数组|5项|✔|命令所采用的参数的列表。 最小值： 1;最大值：5。|
|`parameters.name`|string|64 个字符|✔|在客户端中显示的参数的名称。 此项包含在用户请求中。|
|`parameters.title`|string|32个字符|✔|参数的用户友好标题。|
|`parameters.description`|string|128个字符||描述此参数用途的用户友好字符串。|
|`parameters.value`|string|512个字符||参数的初始值。|
|`parameters.inputType`|string|128个字符||定义在的任务模块上显示的控件的类型 `fetchTask: true` 。 其中一个 `text, textarea, number, date, time, toggle, choiceset` 。|
|`parameters.choices`|对象数组|10项||的选项选项 `choiceset` 。 仅在时 `parameter.inputType` 使用 `choiceset` 。|
|`parameters.choices.title`|string|128个字符|✔|选项的标题。|
|`parameters.choices.value`|string|512个字符|✔|选项的值。|

## <a name="permissions"></a>permissions

**Optional** -字符串数组

一个数组 `string` ，它指定应用程序请求的权限，这样最终用户就可以知道扩展将如何执行。 以下选项是非独占的：

* `identity`&emsp;需要用户标识信息
* `messageTeamMembers`&emsp;需要向团队成员发送直接消息的权限

在更新应用程序时更改这些权限将导致用户在首次运行更新的应用程序时重复同意过程。 有关详细信息，请参阅 [更新应用](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) 。

## <a name="devicepermissions"></a>devicePermissions

**Optional** -字符串数组

在用户的设备上指定您的应用程序可能会请求访问的本机功能。 选项包括：

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**可选**，但 **所需** 的除外

应用程序希望在团队客户端中加载的网站的有效域列表。 例如，域列表可以包含通配符 `*.example.com` 。 这与域的一段完全匹配;如果需要匹配， `a.b.example.com` 请使用 `*.*.example.com` 。 如果您的选项卡配置或内容 UI 需要导航到其他任何域，除了用于选项卡配置之外，则必须在此处指定该域。

但是， **不** 需要在您的应用程序中包含要支持的标识提供程序的域。 例如，若要使用 Google ID 进行身份验证，需要重定向到 accounts.google.com，但不应在中包含 accounts.google.com `validDomains[]` 。

需要其自己的 sharepoint Url 的团队应用程序能够正常工作，可能会在其有效的域列表中包含 "{teamsitedomain}"。

> [!IMPORTANT]
> 不要直接或通过通配符添加位于控件外部的域。 例如， `yourapp.onmicrosoft.com` 是有效的，但 `*.onmicrosoft.com` 无效。

对象是一个包含所有类型的元素的数组 `string` 。

## <a name="webapplicationinfo"></a>webApplicationInfo

**Optional** —对象

 (Azure AD) 应用 ID 和 Microsoft Graph 信息指定 Azure Active Directory，以帮助用户无缝登录你的应用。 如果您的应用程序是在 Azure AD 中注册的，则必须提供应用 ID，以便管理员可以轻松查看权限并在团队管理中心中授予许可。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`id`|string|36个字符|✔|应用程序的 AAD 应用程序 id。 此 id 必须为 GUID。|
|`resource`|string|2048 个字符|✔|用于获取 SSO 的身份验证令牌的应用程序的资源 url。|
|`applicationPermissions`|array of strings|128个字符||指定精确的 [资源特定许可](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)|

## <a name="showloadingindicator"></a>showLoadingIndicator

**可选** -boolean

指示在加载应用程序/选项卡时是否显示加载指示器。 默认值：**False**。
>[!NOTE]
>如果您在应用程序清单中设置 "showLoadingIndicator： true"，然后要正确加载页面，则必须按照 [显示本机加载指示器](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) 文档中所述的协议修改选项卡和任务模块的内容页面。


## <a name="isfullscreen"></a>isFullScreen

 **可选** -boolean

使用或不使用 tab 头条指示个人应用程序的呈现位置。 默认值：**False**。

## <a name="activities"></a>activities

**Optional** —对象

定义您的应用程序将用于发布到用户活动源的属性。

|名称| 类型| 最大大小 | 必需 | Description|
|---|---|---|---|---|
|`activityTypes`|对象数组|128项| | 指定您的应用程序可以发布到用户活动源的活动类型。|

### <a name="activitiesactivitytypes"></a>activityTypes

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`type`|string|32个字符|✔|通知类型。 *请参阅下文*。|
|`description`|string|128个字符|✔|通知的简短说明。 *请参阅下文*。|
|`templateText`|string|128个字符|✔|Ex： "{主角} 为您创建任务 {taskId}"|

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
