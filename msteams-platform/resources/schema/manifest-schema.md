---
title: 清单架构参考
description: 介绍 Microsoft Teams 的清单架构
ms.topic: reference
ms.author: lajanuar
ms.localizationpriority: high
keywords: 团队清单架构
ms.openlocfilehash: 14f1bdaa546fd18612e9869efc2f1216c1aef8db
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453766"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>参考：Microsoft Teams 的清单架构

Teams 清单介绍应用如何集成到 Microsoft Teams 产品中。 清单必须符合托管在 [`https://developer.microsoft.com/json-schemas/teams/v1.12/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.12/MicrosoftTeams.schema.json)的架构。 还支持以前的版本 1.0、1.1,..., 和 1.12 (在 URL 中使用"v1.x")。
有关每个版本中所做的更改的详细信息，请参阅[管理更改日志](https://github.com/OfficeDev/microsoft-teams-app-schema/releases)。

以下架构示例显示所有扩展性选项：

## <a name="sample-full-manifest"></a>示例完整清单

```json
{
    "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.12/MicrosoftTeams.schema.json",
    "manifestVersion": "1.12",
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
            "context": [
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
            "context": [
                "personalTab",
                "channelTab"
            ],
            "name": "Display name of tab",
            "contentUrl": "https://contoso.com/content (displayed in Teams canvas)",
            "websiteUrl": "https://contoso.com/content (displayed in web browser)",
            "searchUrl": "https://contoso.com/content (displayed in web browser)"
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
        "resource": "Resource URL for acquiring auth token for SSO"
    },
    "authorization": {
        "permissions": {
            "resourceSpecific": [
                {
                    "type": "Application",
                    "name": "ChannelSettings.Read.Group"
                },
                {
                    "type": "Delegated",
                    "name": "ChannelMeetingParticipant.Read.Group"
                }
            ]
        }
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
    },
    "meetingExtensionDefinition": {
        "scenes": [
            {
                "id": "9082c811-7e6a-4174-8173-6ccd57d377e6",
                "name": "Getting started sample",
                "file": "scenes/sceneMetadata.json",
                "preview": "scenes/scenePreview.png",
                "maxAudience": 15,
                "seatsReservedForOrganizersOrPresenters": 0
            },
            {
                "id": "afeaed22-f89b-48e1-98b4-46a514344e4a",
                "name": "Sample-1",
                "file": "scenes/sceneMetadata.json",
                "preview": "scenes/scenePreview.png",
                "maxAudience": 15,
                "seatsReservedForOrganizersOrPresenters": 3
            }
        ]
    }
}
```

架构定义以下属性：

## <a name="schema"></a>$schema

可选，但建议 — 的字符串

引用清单的 JSON 架构的 https:// URL。

## <a name="manifestversion"></a>manifestVersion

**必需**— 字符串

此清单使用的清单架构的版本。

## <a name="version"></a>version

**必需**— 字符串

特定应用的版本。 更新清单中的内容时，版本也必须递增。 这样，当安装新清单时，它将覆盖现有清单，并且用户会收到新功能。 将此应用提交到应用商店时，必须重新提交并重新验证新清单。 应用用户会在清单获得批准后几小时内自动收到新的更新清单。

如果应用请求权限更改，系统会提示用户升级并重新进入应用。

此版本字符串必须遵循[semver](http://semver.org/)标准 (MAJOR.MINOR.PATCH)。

## <a name="id"></a>id

**必需**—Microsoft 应用 ID

ID 是 Microsoft 为应用生成的唯一标识符。 如果机器人是通过Microsoft Bot Framework注册的，则有一个 ID。 如果你的选项卡的 Web 应用已使用 Microsoft 登录，则你有一个 ID。 必须在此处输入 ID。 否则，必须在 [Microsoft 应用程序注册门户](https://aka.ms/appregistrations)生成新 ID。 如果添加机器人，请使用相同的 ID。

> [!NOTE]
> 如果要将更新提交到 AppSource 中的现有应用，则不得修改清单中的 ID。

## <a name="developer"></a>developer

**必需**— 对象

指定有关公司的信息。 对于提交到 Teams 应用商店的应用，这些值必须与应用商店一览中的信息匹配。 有关详细信息，请参阅 [Teams Store 发布指南](~/concepts/deploy-and-publish/appsource/publish.md)。

|名称| 最大大小 | 必需 | Description|
|---|---|---|---|
|`name`|32 个字符|✔|开发人员的显示名称。|
|`websiteUrl`|2048 个字符|✔|开发人员网站的 https:// URL。 此链接必须将用户转到公司或产品特定的登陆页面。|
|`privacyUrl`|2048 个字符|✔|开发人员隐私策略的 https:// URL。|
|`termsOfUseUrl`|2048 个字符|✔|开发人员使用条款的 https:// URL。|
|`mpnId`|10 个字符| |**可选** 标识生成应用的合作伙伴组织的Microsoft 合作伙伴网络 ID。|

## <a name="name"></a>name

**必需**— 对象

应用体验的名称，在 Teams 体验中向用户显示。 对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。 `short`和`full`的值必须不同。

|名称| 最大大小 | 必需 | Description|
|---|---|---|---|
|`short`|30 个字符|✔|应用的短显示名称。|
|`full`|100 个字符||如果完整应用名称超过 30 个字符，则使用应用的全名。|

## <a name="description"></a>说明

**必需**— 对象

向用户描述应用。对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。

确保说明描述你的体验，并帮助潜在客户了解你的体验。 如果需要使用外部帐户，则必须在完整说明中进行说明。 `short`和`full`的值必须不同。 简短说明不能在长说明中重复，也不能包含任何其他应用名称。

|名称| 最大大小 | 必需 | Description|
|---|---|---|---|
|`short`|80 个字符|✔|应用体验的简短说明，在空间受限时使用。|
|`full`|4000 个字符|✔|应用的完整说明。|

## <a name="packagename"></a>packageName

**可选**— 字符串

反向域表示法中应用的唯一标识符；例如，com.example.myapp。最大长度：64 个字符。

## <a name="localizationinfo"></a>localizationInfo

**可选**— 对象

允许默认语言的规范，并提供指向更多语言文件的指针。有关详细信息，请参阅 [本地化](~/concepts/build-and-test/apps-localization.md)。

|名称| 最大大小 | 必需 | Description|
|---|---|---|---|
|`defaultLanguageTag`||✔|此顶级清单文件中字符串的语言标记。|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

指定更多语言翻译的对象数组。

|名称| 最大大小 | 必需 | Description|
|---|---|---|---|
|`languageTag`||✔|所提供文件中字符串的语言标记。|
|`file`||✔|包含已翻译字符串的 .json 文件的相对文件路径。|

## <a name="icons"></a>图标

**必需**— 对象

Teams 应用中使用的图标。 图标文件必须作为上传包的一部分包含在内。 有关详细信息，请参阅 [图标](../../concepts/build-and-test/apps-package.md#app-icons)。

|名称| 最大大小 | 必需 | Description|
|---|---|---|---|
|`outline`|32 x 32 像素|✔|透明 32x32 PNG 大纲图标的相对文件路径。|
|`color`|192 x 192 像素|✔|完整颜色 192x192 PNG 图标的相对文件路径。|

## <a name="accentcolor"></a>accentColor

**必需**— HTML 十六进制颜色代码

要使用的颜色和大纲图标的背景。

该值必须是以"#"开头的有效 HTML 颜色代码，例如 `#4464ee`。

## <a name="configurabletabs"></a>configurableTabs

**可选**— 数组

当应用体验具有团队频道选项卡体验时使用，该体验需要在添加之前进行额外配置。 只能在 `team` 和 `groupchat` 作用域中使用可配置的选项卡，并且可以多次配置相同的选项卡。 但是，只能在清单中定义一次。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`configurationUrl`|string|2048 个字符|✔|配置选项卡时要使用的 https:// URL。|
|`scopes`|枚举数组|1|✔|目前，可配置选项卡仅支持 `team` 和 `groupchat` 范围。 |
|`canUpdateConfiguration`|Boolean|||一个值，该值指示创建后用户是否可以更新选项卡配置的实例。默认值：**true**。|
|`context` |枚举数组|6 ||[支持选项卡](../../tabs/how-to/access-teams-context.md)的 `contextItem` 范围的集合。 默认值：**[channelTab， privateChatTab， meetingChatTab， meetingDetailsTab]**。|
|`sharePointPreviewImage`|string|2048||用于 SharePoint 的选项卡预览图像的相对文件路径。大小 1024x768。 |
|`supportedSharePointHosts`|枚举数组|1||定义如何在 SharePoint 中提供选项卡。选项 `sharePointFullPage` 和 `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**可选**— 数组

定义默认情况下可以"固定"的一组选项卡，而无需用户手动添加它们。 在 `personal` 范围内声明的静态选项卡始终固定到应用的个人体验。 当前不支持在 `team` 作用域中声明的静态选项卡。

此项是一个数组（最多 16 个元素），其类型的所有元素 `object`。 只有提供静态选项卡解决方案的解决方案才需要此块。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`entityId`|string|64 个字符|✔|选项卡显示的实体的唯一标识符。|
|`name`|string|128 个字符|✔|通道接口中选项卡的显示名称。|
|`contentUrl`|string||✔|指向要在 Teams 画布中显示的实体 UI 的 https:// URL。|
|`websiteUrl`|string|||要指向用户是否选择在浏览器中查看的 https:// URL。|
|`searchUrl`|string|||要指向用户搜索查询的 https:// URL。|
|`scopes`|枚举数组|1|✔|目前，静态选项卡仅支持 `personal` 范围，这意味着只能将其预配为个人体验的一部分。|
|`context` | 枚举数组| 2|| 支持选项卡的 `contextItem` 范围集。|

> [!NOTE]
> searchUrl 功能不适用于第三方开发人员。如果选项卡需要上下文相关信息来显示相关内容或启动身份验证流，请参阅 [获取 Microsoft Teams 选项卡的上下文](../../tabs/how-to/access-teams-context.md)。

## <a name="bots"></a>机器人

**可选**— 数组

定义机器人解决方案以及可选信息（如默认命令属性）。

该项是一个数组（目前每个应用仅允许一个机器人&mdash;最多一个元素），类型为 `object`的所有元素。 只有提供机器人体验的解决方案才需要此块。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`botId`|string|64 个字符|✔|使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。 ID 可以与整体[应用 ID](#id)相同。|
|`scopes`|枚举数组|3|✔|指定机器人是在 `team`、群组聊天（`groupchat`）的频道上下文中提供体验还是单独限于单个用户的体验（`personal`）。这些选项不是独占的。|
|`needsChannelSelector`|Boolean|||描述机器人是否使用用户提示将机器人添加到特定通道。默认值：**`false`**|
|`isNotificationOnly`|Boolean|||指示机器人是否为单向、仅通知机器人，而不是聊天机器人。默认值：**`false`**|
|`supportsFiles`|Boolean|||指示机器人是否支持在个人聊天中上传/下载文件的功能。默认值：**`false`**|
|`supportsCalling`|Boolean|||一个值，该值指示机器人支持音频调用的位置。 **IMPORTANT**： 此属性当前为实验性属性。 实验性属性可能无法完成，并且在完全可用之前可能会进行更改。  该属性仅用于测试和探索目的，不得在生产应用程序中使用。 默认值：**`false`**|
|`supportsVideo`|Boolean|||一个值，该值指示机器人支持视频通话的位置。 **IMPORTANT**： 此属性当前为实验性属性。 实验性属性可能无法完成，并且在完全可用之前可能会进行更改。  该属性仅用于测试和探索目的，不得在生产应用程序中使用。 默认值：**`false`**|

### <a name="botscommandlists"></a>bots.commandLists

机器人可以向用户推荐的命令的可选列表。 对象是一个数组（最多两个元素），其类型为 `object`;必须为机器人支持的每个范围定义一个单独的命令列表。 有关详细信息，请参阅[机器人菜单](~/bots/how-to/create-a-bot-commands-menu.md)。

|名称| 类型| 最大大小 | 必需 | Description|
|---|---|---|---|---|
|`items.scopes`|枚举数组|3|✔|指定命令列表有效的范围。选项为 `team`、 `personal`和 `groupchat`。|
|`items.commands`|对象数组|10 |✔|自动程序支持的命令数组：<br>`title`：自动程序命令名称（字符串，32）<br>`description`：命令语法及其参数的简单说明或示例（字符串，128）。|

### <a name="botscommandlistscommands"></a>bots.commandLists.commands

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|title|string|12 |✔|机器人命令名称。|
|description|string|128 个字符|✔|简单的文本说明或命令语法及其参数的示例。|

## <a name="connectors"></a>连接器

**可选**— 数组

`connectors`块定义应用的 Office 365 连接器。

对象是一个数组（最多一个元素），其中所有元素的类型为 `object`。 只有提供连接器的解决方案才需要此块。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`configurationUrl`|string|2048 个字符|✔|配置连接器时要使用的 https:// URL。|
|`scopes`|枚举数组|1|✔|指定连接器是在 `team` 中频道的上下文中提供体验，还是单独限于单个用户的体验（`personal`）。目前，仅支持 `team` 范围。|
|`connectorId`|string|64 个字符|✔|连接器的唯一标识符，与[Connectors 开发人员仪表板](https://aka.ms/connectorsdashboard)中的 ID 匹配。|

## <a name="composeextensions"></a>composeExtensions

**可选**— 数组

定义应用的消息传递扩展。

> [!NOTE]
> 已从"撰写扩展"更改了该功能的名称到"消息传递扩展>在 2017 年 11 月，但清单名称保持不变，以便现有扩展继续运行。

该项是一个数组（最大值为一个元素），其中所有元素的类型。 `object` 只有提供消息传递扩展的解决方案才需要此块。

|名称| 类型 | 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`botId`|string|64|✔|支持消息传递扩展的机器人的唯一 Microsoft 应用 ID，已向Bot Framework注册。 ID 可以与整体应用 ID 相同。|
|`commands`|对象数组|10 |✔|消息传递扩展支持的命令数组。|
|`canUpdateConfiguration`|Boolean|||一个值，该值指示用户是否可以更新消息传递扩展插件的配置。默认值：**false**。|
|`messageHandlers`|对象数组|5||允许在满足特定条件时调用应用的处理程序列表。|
|`messageHandlers.type`|string|||消息处理程序的类型。必须 `"link"`。|
|`messageHandlers.value.domains`|字符串数组|||链接消息处理程序可以注册的域数组。|

### <a name="composeextensionscommands"></a>composeExtensions.commands

消息传递扩展插件必须声明一个或多个最多包含 10 个命令的命令。 每个命令都显示在 Microsoft Teams 中，作为来自基于 UI 的入口点的潜在交互。

每个命令项都是具有以下结构的对象：

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`id`|string|64 个字符|✔|命令的 ID。|
|`title`|string|32 个字符|✔|用户友好的命令名称。|
|`type`|string|64 个字符||命令的类型。 `query`或`action`之一。 默认值： **查询**。|
|`description`|string|128 个字符||向用户显示以指示此命令用途的说明。|
|`initialRun`|Boolean|||布尔值指示命令最初是否在没有参数时运行。默认值为 **false**。|
|`context`|字符串数组|3||定义可以从何处调用消息扩展插件。 `compose`、`commandBox`、`message`的任何组合。 默认值为“`["compose","commandBox"]`”。|
|`fetchTask`|Boolean|||一个布尔值，指示它是否必须动态提取任务模块。默认值为 **false**。|
|`taskInfo`|object|||指定使用消息传递扩展命令时要预加载的任务模块。|
|`taskInfo.title`|string|64 个字符||初始对话框标题。|
|`taskInfo.width`|string|||对话框宽度 - 数字（以像素为单位）或默认布局，如"large"、"medium"或"small"。|
|`taskInfo.height`|string|||对话框高度 - 数字（以像素为单位）或默认布局，如"large"、"medium"或"small"。|
|`taskInfo.url`|string|||初始 Web 视图 URL。|
|`parameters`|对象数组|5 个项目|✔|命令采用的参数列表。 最小值：1;最大值： 5。|
|`parameters.name`|string|64 个字符|✔|在客户端中显示的参数的名称。参数名称包含在用户请求中。|
|`parameters.title`|string|32 个字符|✔|参数的用户友好标题。|
|`parameters.description`|string|128 个字符||描述此参数用途的用户友好字符串。|
|`parameters.value`|string|512 个字符||参数的初始值。 当前不支持该值|
|`parameters.inputType`|string|128 个字符||定义任务模块上为`fetchTask: true` 显示的控件类型。 `text, textarea, number, date, time, toggle, choiceset` 之一。|
|`parameters.choices`|对象数组|10 项||`choiceset`的选择选项。 仅当`parameter.inputType``choiceset`时使用。|
|`parameters.choices.title`|string|128 个字符|✔|选择的标题。|
|`parameters.choices.value`|string|512 个字符|✔|选项的值。|

## <a name="permissions"></a>permissions

**Optional**—字符串数组

`string`数组，指定应用请求的权限，让最终用户了解扩展的执行方式。以下选项是非独占的：

* `identity`&emsp;需要用户标识信息。
* `messageTeamMembers`&emsp;请求向团队成员发送直接消息的权限。

在应用更新期间更改这些权限会导致用户在运行更新的应用后重复同意过程。有关详细信息，请参阅 [更新应用](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)。

## <a name="devicepermissions"></a>devicePermissions

**Optional**—字符串数组

在应用请求访问的用户设备上提供本机功能。选项包括：

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**可选**，除非 **所述的必需**。

应用应在 Teams 客户端中加载的网站的有效域列表。 域列表可以包含通配符，例如，`*.example.com`。 有效域与域的一个段完全匹配;如果需要匹配 `a.b.example.com`则使用 `*.*.example.com`。 如果选项卡配置或内容 UI 导航到选项卡配置以外的任何其他域，则必须在此处指定该域。

请 **不要** 包含要在应用中支持的标识提供程序的域。 例如，若要使用 Google ID 进行身份验证，需要重定向到 accounts.google.com，但是，不得在 `validDomains[]`中包含 accounts.google.com。

需要自己的 SharePoint URL 才能正常运行的 Teams 应用包括 "{teamsitedomain}>在其有效域列表中。

> [!IMPORTANT]
> 不要直接或通过通配符添加超出控制范围的域。 例如， `yourapp.onmicrosoft.com` 有效，但是， `*.onmicrosoft.com` 无效。

对象是一个数组，其中包含类型的所有元素 `string`。

## <a name="webapplicationinfo"></a>webApplicationInfo

**可选**— 对象

提供 Azure Active Directory 应用 ID 和 Microsoft Graph 信息，以帮助用户无缝登录到应用。 如果应用已在 Microsoft Azure Active Directory (Azure AD) 中注册，则必须提供应用 ID。 管理员可以在 Teams 管理中心轻松查看权限并授予同意。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`id`|string|36 个字符|✔|应用的 Azure AD 应用程序 ID。 此 ID 必须是 GUID。|
|`resource`|string|2048 个字符|✔|用于获取 SSO 的身份验证令牌的应用的资源 URL。 </br> **注意：** 如果未使用 SSO，请确保在此字段中向应用清单输入虚拟字符串值，例如， https://notapplicable 以避免错误响应。 |

## <a name="showloadingindicator"></a>showLoadingIndicator

**可选**— 布尔值

指示是否在加载应用或选项卡时显示加载指示器。默认值为 **false**。
>[!NOTE]
>如果在应用清单中选择`showLoadingIndicator` 为 true，若要正确加载页面，请修改选项卡和任务模块的内容页，如 [显示本机加载指示器](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) 文档中所述。

## <a name="isfullscreen"></a>isFullScreen

 **可选**— 布尔值

指示使用或不使用选项卡标题栏呈现个人应用的位置。默认值为 **false**。

> [!NOTE]
> `isFullScreen` 仅适用于发布到组织的应用。

## <a name="activities"></a>activities

**可选**— 对象

定义应用用于发布用户活动源的属性。

|名称| 类型| 最大大小 | 必需 | Description|
|---|---|---|---|---|
|`activityTypes`|对象数组|128 个项目| | 提供应用可以发布到用户活动源的活动类型。|

### <a name="activitiesactivitytypes"></a>activities.activityTypes

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`type`|string|32 个字符|✔|通知类型。 *请参阅下文*。|
|`description`|string|128 个字符|✔|通知的简要说明。 *请参阅下面的*。|
|`templateText`|string|128 个字符|✔|例如："{actor} 为你创建了任务 {taskId}"|

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

**可选** - 字符串

指定默认情况下为此应用定义的安装范围。 定义的范围将是当用户尝试添加应用时按钮上显示的选项。 选项有：

* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a>defaultGroupCapability

**可选** - object

选择组安装范围后，它将在用户安装应用时定义默认功能。选项包括：

* `team`
* `groupchat`
* `meetings`

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`team`|string|||当所选安装范围 `team` 时，此字段指定可用的默认功能。选项：`tab`、 `bot`或 `connector`。|
|`groupchat`|string|||当所选安装范围 `groupchat` 时，此字段指定可用的默认功能。选项：`tab`、 `bot`或 `connector`。|
|`meetings`|string|||当所选安装范围 `meetings` 时，此字段指定可用的默认功能。选项：`tab`、 `bot`或 `connector`。|

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

**可选**— 布尔值

当 `defaultBlockUntilAdminAction` 属性设置为 **true** 时，应用默认向用户隐藏，直到管理员允许它。 如果设置为 **true，** 则应用将隐藏所有租户和最终用户。 租户管理员可以在管理中心内Teams应用，并采取措施以允许或阻止该应用。 默认值为 **false**。 有关默认应用块详细信息，请参阅隐藏[Teams应用，直到管理员批准](~/concepts/design/enable-app-customization.md#hide-teams-app-until-admin-approves)。

## <a name="publisherdocsurl"></a>publisherDocsUrl

**可选** - 字符串

**最大大小** - 128 个字符

是一个指向信息页的 HTTPS URL，供管理员在允许应用之前获取指南， `publisherDocsUrl` 此应用默认被阻止。 它还可用于提供有关对租户管理员有用的应用的任何说明或信息。

## <a name="subscriptionoffer"></a>subscriptionOffer

**可选** - object

指定与你的应用关联的 SaaS 产品/服务。

|名称| 类型|最大大小|必需|说明|
|---|---|---|---|---|
|`offerId`| string | 2048 个字符 | ✔ | 包含发布者 ID 和产品/服务 ID 的唯一标识符，可在 [合作伙伴中心](https://partner.microsoft.com/dashboard)中找到。必须将字符串格式设置为 `publisherId.offerId`。|

## <a name="meetingextensiondefinition"></a>meetingExtensionDefinition

**可选** - object

指定会议扩展定义。有关详细信息，请参阅 [Teams 中的自定义“同框场景模式”场景](../../apps-in-teams-meetings/teams-together-mode.md)。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`scenes`|对象数组| 5 个项目||会议支持的场景。|

### <a name="meetingextensiondefinitionscenes"></a>meetingExtensionDefinition.scenes

|名称| 类型|最大大小|必需 |Description|
|---|---|---|---|---|
|`id`|||✔| 场景的唯一标识符。 此 ID 必须是 GUID。 |
|`name`| string | 128 个字符 |✔| 场景的名称。 |
|`file`|||✔| 场景的元数据 json 文件的相对文件路径。 |
|`preview`|||✔| 场景的 PNG 预览图标的相对文件路径。 |
|`maxAudience`| integer | 50  |✔| 场景中支持的最大受众数。 |
|`seatsReservedForOrganizersOrPresenters`| integer | 50 |✔| 为组织者或演示者保留的席位数。|

## <a name="authorization"></a>授权

**可选** - 对象

指定并合并应用的授权相关信息。

|名称| 类型|最大大小|必需 |说明|
|---|---|---|---|---|
|`permissions`||||应用运行所需的权限列表。|

### <a name="authorizationpermissions"></a>authorization.permissions

|名称| 类型|最大大小|必需 |说明|
|---|---|---|---|---|
|`resourceSpecific`| 对象数组|16 个项目||在资源实例级别保护数据访问的权限。|

### <a name="authorizationpermissionsresourcespecific"></a>authorization.permissions.resourceSpecific

|名称| 类型|最大大小|必需 |说明|
|---|---|---|---|---|
|`type`|string||✔| 特定于资源的权限类型。选项：`Application` 和 `Delegated`。|
|`name`|string|128 个字符|✔|特定于资源的权限名称。 有关详细信息，请参阅[资源对应的应用程序权限](#resource-specific-application-permissions)和[资源对应的委派权限](#resource-specific-delegated-permissions)|

#### <a name="resource-specific-application-permissions"></a>资源对应的应用程序权限

应用程序权限允许应用在用户未登录的情况下访问数据。 有关应用程序权限的信息，请参阅 [MS Graph 和 MS BotSDK 的资源相应的许可](../../graph-api/rsc/resource-specific-consent.md)。

#### <a name="resource-specific-delegated-permissions"></a>资源对应的委派权限

委派的权限允许应用代表已登录用户访问数据。

* **团队的资源对应的委派权限**

    |**名称**|**说明**|
    |---|---|
    |`ChannelMeetingParticipant.Read.Group`| 允许应用代表已登录用户读取与此团队关联的频道会议的参与者信息，包括姓名、角色、ID、加入和离开时间。|
    |`InAppPurchase.Allow.Group`| 允许应用代表已登录用户向此团队中的用户显示市场产品/服务并在应用中完成购买。|
    |`ChannelMeetingStage.Write.Group`| 允许应用代表已登录用户在与此团队关联的频道会议中显示会议阶段的内容。|

* **聊天或会议的资源对应的委派权限**

    |**名称**|**说明**|
    |---|---|
    |`InAppPurchase.Allow.Chat`|允许应用代表已登录用户向此聊天和任何关联会议中的用户显示市场产品/服务，并在应用中完成其购买。|
    |`MeetingStage.Write.Chat`|允许应用代表已登录用户在与此聊天关联的会议中显示会议阶段的内容。|
    |`OnlineMeetingParticipant.Read.Chat`|允许应用代表已登录用户读取与此聊天关联的会议的参与者信息，包括姓名、角色、ID、加入和离开时间。|
    |`OnlineMeetingParticipant.ToggleIncomingAudio.Chat`|允许应用代表登录用户为与此聊天关联的会议中的参与者切换传入音频。|

* **用户的资源对应的委派权限**

    |**名称**|**说明**|
    |---|---|
    |`InAppPurchase.Allow.User`|允许应用代表已登录用户显示用户市场产品/服务并完成用户在应用内的购买。|

## <a name="see-also"></a>另请参阅

* [了解Microsoft Teams结构](~/concepts/design/app-structure.md)
* [启用应用自定义](~/concepts/design/enable-app-customization.md)
* [本地化应用](~/concepts/build-and-test/apps-localization.md)
* [集成媒体功能](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Microsoft Teams 的公共开发人员预览清单架构](manifest-schema-dev-preview.md)
