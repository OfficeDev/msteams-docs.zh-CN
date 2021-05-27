---
title: 开发者预览版清单架构参考
description: 介绍清单支持的架构Microsoft Teams
ms.topic: reference
keywords: teams 清单架构开发者预览版
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: a5c75046b950484a897fa2720444899c4817989c
ms.sourcegitcommit: 25c02757fe207cdff916ba63aa215f88e24e1d6f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2021
ms.locfileid: "52667416"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a>开发人员预览清单架构Microsoft Teams

> [!NOTE]
> 有关此计划以及如何加入计划的信息 [，请参阅](~/resources/dev-preview/developer-preview-intro.md)开发者预览版。
> 如果未使用开发人员预览版，则不应使用此版本的清单。 请参阅[Reference： Manifest schema for Microsoft Teams](~/resources/schema/manifest-schema.md) for the public version of the manifest。

Microsoft Teams清单介绍了应用如何集成到 Microsoft Teams 产品。 清单必须符合 托管在 的架构 [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) 。

有关可用功能详细信息，请参阅公共更新开发者预览版[中的Microsoft Teams。](~/resources/dev-preview/developer-preview-features.md)

## <a name="sample-full-manifest"></a>示例完整清单

```json
{
  "$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
  "manifestVersion": "devPreview",
  "version": "1.0.0",
  "id": "%MICROSOFT-APP-ID%",
  "packageName": "com.example.myapp",
  "devicePermissions" : [ "geolocation", "media" ],
  "developer": {
    "name": "Publisher Name",
    "websiteUrl": "https://website.com/",
    "privacyUrl": "https://website.com/privacy",
    "termsOfUseUrl": "https://website.com/app-tos",
    "mpnId": "1234567890"
  },
  "localizationInfo": {
    "defaultLanguageTag": "es-es",
    "additionalLanguages": [
      {
        "languageTag": "en-us",
        "file": "en-us.json"
      }
    ]
  },
  "name": {
    "short": "Name of your app (<=30 chars)",
    "full": "Full name of app, if longer than 30 characters"
  },
  "description": {
    "short": "Short description of your app",
    "full": "Full description of your app"
  },
  "icons": {
    "outline": "%FILENAME-32x32px%",
    "color": "%FILENAME-192x192px"
  },
  "accentColor": "%HEX-COLOR%",
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [ "team", "groupchat" ]
    }
  ],
  "staticTabs": [
    {
      "entityId": "idForPage",
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content?host=msteams",
      "contentBotId": "Specifies to the app that tab is an Adaptive Card Tab. You can either provide the contentBotId or contentUrl.",
      "websiteUrl": "https://contoso.com/content",
      "scopes": [ "personal" ]
    }
  ],
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "scopes": [ "team", "personal", "groupchat" ],
      "supportsFiles": true,
      "commandLists": [
        {
          "scopes": [ "team", "groupchat" ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command N",
              "description": "Description of Command N"
            }
          ]
        },
        {
          "scopes": [ "personal", "groupchat" ],
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
      "configurationUrl": "https://contoso.com/teamsconnector/configure",
      "scopes": [ "team"]
    }
  ],
  "composeExtensions": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "exampleCmd1",
          "title": "Example Command",
          "description": "Command Description; e.g., Search on the web",
          "initialRun": true,
          "type" : "search",
          "context" : ["compose", "commandBox"],
          "parameters": [
            {
              "name": "keyword",
              "title": "Search keywords",
              "description": "Enter the keywords to search for"
            }
          ]
        },
        {
          "id": "exampleCmd2",
          "title": "Example Command 2",
          "description": "Command Description; e.g., Search for a customer",
          "initialRun": true,
          "type" : "action",
          "fetchTask" : true,
          "context" : ["message"],
          "parameters": [
            {
              "name": "custinfo",
              "title": "Customer name",
              "description": "Enter a customer name",
              "inputType" : "text"
            }
          ]
        },
        {
          "id": "exampleMessageHandler",
          "title": "Message Handler",
          "description": "Domains that will create a preview when pasted into the compose box",
          "messageHandlers": [
            {
              "type" : "link",
              "value" : {
                "domains" : [
                  "mysite.someplace.com",
                  "othersite.someplace.com"
                ]
              }
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers",
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
   "configurableProperties": [
     "name",
     "shortDescription",
     "longDescription",
     "smallImageUrl", 
     "largeImageUrl", 
     "accentColor",
     "websiteUrl",
     "privacyUrl",
     "termsOfUseUrl"        
  ],
  "defaultInstallScope": "meetings",
  "defaultGroupCapability": {
    "meetings": "tab", 
    "team": "bot", 
    "groupchat": "bot"
  }
}
```

该架构定义以下属性：

## <a name="schema"></a>$schema

*可选，但建议* &ndash; 字符串

引用 https:// JSON 架构的 URL。

## <a name="manifestversion"></a>manifestVersion

**必需** &ndash; 字符串

此清单使用的清单架构版本。 它应为"devPreview"。

## <a name="version"></a>version

**必需** &ndash; 字符串

特定应用的版本。 如果更新清单中的某些内容，则版本也必须递增。 这样一来，在安装新的清单时，它将覆盖现有的版本，用户将获得新的功能。 如果此应用已提交到应用商店，则新清单必须重新提交和重新验证。 然后，此应用的用户将在经过批准后数小时内自动获取新的更新清单。

如果应用请求的权限更改，将提示用户升级并重新同意应用。

此版本字符串必须遵循 [Semver](http://semver.org/) 标准 (MAJOR。MINOR。PATCH) 。

## <a name="id"></a>id

**必需** &ndash; Microsoft 应用 ID

此应用的唯一 Microsoft 生成的标识符。 如果你已经通过 Microsoft Bot Framework 注册了自动程序，或者你的选项卡的 Web 应用已经使用 Microsoft 登录，你应该已经拥有 ID，并且应在此处输入它。 否则，应在"我的应用程序" (Microsoft 应用程序注册门户 [) 生成](https://apps.dev.microsoft.com) 一个新 ID，在此处输入，然后在添加自动程序时重复使用 [它](~/bots/how-to/create-a-bot-for-teams.md)。

## <a name="packagename"></a>packageName

**必需** &ndash; 字符串

反向域表示法中此应用程序的唯一标识符;例如，com.example.myapp。

## <a name="developer"></a>developer

**Required**

指定有关你的公司的信息。 对于提交到 AppSource (之前Office应用商店) ，这些值必须与 AppSource 条目中的信息匹配。

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`name`|32 个字符|✔|开发人员显示名称的指南。|
|`websiteUrl`|2048 个字符|✔|the https:// URL to the developer's website. 此链接应让用户访问你的公司或特定于产品的登陆页面。|
|`privacyUrl`|2048 个字符|✔|the https:// URL to the developer's privacy policy.|
|`termsOfUseUrl`|2048 个字符|✔|the https:// URL to the developer's use terms.|
|`mpnId`|10 个字符|✔|**可选** 标识生成应用的合作伙伴组织的 Microsoft 合作伙伴网络 ID。|

## <a name="localizationinfo"></a>localizationInfo

**可选**

允许指定默认语言，以及指向其他语言文件的指针。 请参阅 [本地化](~/concepts/build-and-test/apps-localization.md)。

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`defaultLanguageTag`|4 个字符|✔|此顶级清单文件中字符串的语言标记。|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

指定其他语言翻译的对象数组。

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`languageTag`|4 个字符|✔|提供的文件中字符串的语言标记。|
|`file`|4 个字符|✔|包含已翻译字符串的 .json 文件的相对文件路径。|

## <a name="name"></a>name

**Required**

应用体验的名称，在应用体验中向Teams显示。 对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。 和 `short` `full` 的值不应相同。

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`short`|30 个字符|✔|应用的显示名称。|
|`full`|100 个字符||应用的完整名称，在完整应用名称超过 30 个字符时使用。|

## <a name="description"></a>说明

**Required**

向用户描述你的应用。 对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。

确保你的描述准确地描述了你的体验，并提供相关信息来帮助潜在客户了解你的体验。 还应在完整说明中注意，如果需要使用外部帐户。 和 `short` `full` 的值不应相同。  简短说明不得在详细说明中重复，且不得包含任何其他应用名称。

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`short`|80 个字符|✔|应用体验的简短说明，在空间有限时使用。|
|`full`|4000 个字符|✔|应用的完整说明。|

## <a name="icons"></a>图标

**Required**

在应用内使用的Teams图标。 图标文件必须作为上传程序包的一部分包含在内。

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`outline`|2048 个字符|✔|指向透明 32x32 PNG 大纲图标的相对文件路径。|
|`color`|2048 个字符|✔|完整颜色 192x192 PNG 图标的相对文件路径。|

## <a name="accentcolor"></a>accentColor

**必需** &ndash; 字符串

要与 和 结合使用用作大纲图标背景的颜色。

该值必须是以"#"开头的有效 HTML 颜色代码，例如 `#4464ee` 。

## <a name="configurabletabs"></a>configurableTabs

**可选**

当你的应用体验具有团队频道选项卡体验时，需要在添加前进行额外配置。 可配置的选项卡仅在团队范围内受支持，并且当前每个应用仅支持一个选项卡。

对象是包含类型 的所有元素的数组 `object` 。 只有提供可配置通道选项卡解决方案的解决方案才需要此块。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`configurationUrl`|String|2048 个字符|✔|配置 https:// 时将使用的 URL。|
|`canUpdateConfiguration`|Boolean|||一个值，指示用户创建后是否可以更新选项卡配置的实例。 默认值： `true`|
|`scopes`|枚举数组|1|✔|目前，可配置的选项卡仅支持 `team` 和 `groupchat` 作用域。 |
|`sharePointPreviewImage`|String|2048||选项卡预览图像的相对文件路径，用于SharePoint。 大小 1024x768。 |
|`supportedSharePointHosts`|枚举数组|1||定义选项卡在页面SharePoint。 选项为 `sharePointFullPage` 和 `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**可选**

定义一组默认情况下可以"固定"的选项卡，而无需用户手动添加它们。 范围中声明 `personal` 的静态选项卡始终固定到应用的个人体验。 作用域中声明的 `team` 静态选项卡当前不受支持。

通过指定 而不是 在 staticTabs 块中呈现带自适应 `contentBotId` `contentUrl` **卡片的** 选项卡。

对象是一个数组 (类型的所有元素) 最多包含 16 个元素 `object` 。 只有提供静态选项卡解决方案的解决方案才需要此块。


|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`entityId`|字符串|64 个字符|✔|选项卡显示的实体的唯一标识符。|
|`name`|String|128 个字符|✔|选项卡显示名称界面中的列数。|
|`contentUrl`|String|2048 个字符|✔|指向要 https:// 画布中的实体 UI 的 Teams URL。|
|`contentBotId`|   | | | 自动Microsoft Teams门户中为自动程序指定的应用 ID。 |
|`websiteUrl`|String|2048 个字符||用户 https:// 在浏览器中查看时指向的 URL。|
|`scopes`|枚举数组|1|✔|目前，静态选项卡仅支持范围，这意味着只能将作用域预配 `personal` 为个人体验的一部分。|

## <a name="bots"></a>bots

**可选**

定义自动程序解决方案以及默认命令属性等可选信息。

对象是一个 (，当前每个应用仅允许一个自动程序) 类型的所有元素 &mdash; `object` 。 只有提供自动程序体验的解决方案才需要此块。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`botId`|字符串|64 个字符|✔|使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。 这可能与整个应用 [ID 相同](#id)。|
|`needsChannelSelector`|布尔值|||描述自动程序是否利用用户提示将自动程序添加到特定频道。 默认值： `false`|
|`isNotificationOnly`|布尔值|||指示自动程序是否为单向、仅通知的自动程序，而不是对话自动程序。 默认值： `false`|
|`supportsFiles`|布尔值|||指示自动程序是否支持在个人聊天中上传/下载文件。 默认值： `false`|
|`scopes`|枚举数组|3|✔|指定自动程序是在 `team` 内的频道上下文中提供体验、在群组聊天 (`groupchat`) 中提供体验，还是仅在单个用户 (`personal`) 范围内提供体验。 这些选项不具排他性。|

### <a name="botscommandlists"></a>bots.commandLists

自动程序可以推荐给用户的命令的可选列表。 对象是一个 (，最多包含 2 个元素) 所有类型元素;您必须为自动程序支持的每个范围定义单独的 `object` 命令列表。 有关详细信息，请参阅自动 [程序菜单](~/bots/how-to/create-a-bot-commands-menu.md)。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`items.scopes`|枚举数组|3|✔|指定命令列表有效的作用域。 选项包括 `team`、`personal` 和 `groupchat`。|
|`items.commands`|对象数组|10  |✔|自动程序支持的命令数组：<br>`title`：自动程序命令名称 (字符串，32) 。<br>`description`：命令语法及其参数的简单说明或示例， (字符串，128) 。|

## <a name="connectors"></a>连接器

**可选**

`connectors`块为应用Office 365连接器。

对象是一个数组， (类型的所有元素) 1 个元素 `object` 。 只有提供连接器的解决方案才需要此块。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`configurationUrl`|String|2048 个字符|✔|配置 https:// 时将使用的 URL。|
|`connectorId`|字符串|64 个字符|✔|连接器的唯一标识符，与连接器开发人员仪表板中的 ID [相匹配](https://aka.ms/connectorsdashboard)。|
|`scopes`|枚举数组|1|✔|指定连接器是提供在 中频道上下文中的体验，还是仅针对单个用户 `team` `personal` () 。 目前，仅 `team` 支持范围。|

## <a name="composeextensions"></a>composeExtensions

**可选**

为应用定义消息传递扩展。

> [!NOTE]
> 2017 年 11 月，功能名称从"撰写扩展"更改为"邮件扩展"，但清单名称保持不变，以便现有扩展继续工作。

对象是一个数组， (类型的所有元素) 1 个元素 `object` 。 只有提供邮件扩展的解决方案才需要此块。

|名称| 类型 | 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`botId`|String|64|✔|自动程序支持消息传递扩展的唯一 Microsoft 应用 ID，在 Bot Framework 中注册。 这可能与整个应用 [ID 相同](#id)。|
|`canUpdateConfiguration`|Boolean|||一个值，指示用户是否可以更新邮件扩展的配置。 默认值为 `false`。|
|`commands`|对象数组|10  |✔|邮件扩展支持的命令数组|

### <a name="composeextensionscommands"></a>composeExtensions.commands

邮件扩展应声明一个或多个命令。 每个命令都Microsoft Teams UI 入口点的潜在交互。 最多有 10 个命令。

每个命令项都是具有以下结构的对象：

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`id`|字符串|64 个字符|✔|命令的 ID。|
|`type`|字符串|64 个字符||命令的类型。 或 `query` `action` 之一。 默认值： `query`|
|`title`|String|32 个字符|✔|用户友好命令名称。|
|`description`|String|128 个字符||向用户显示以指示此命令用途的说明。|
|`initialRun`|Boolean|||一个布尔值，指示命令最初是否应该没有参数运行。 默认值： `false`|
|`context`|Array of Strings|3||定义可以从何处调用邮件扩展。 、 `compose` 、 的任意 `commandBox` 组合 `message` 。 默认值为 `["compose", "commandBox"]`|
|`fetchTask`|Boolean|||一个布尔值，指示它应动态提取任务模块。|
|`taskInfo`|对象|||指定在使用消息传递扩展命令时要预加载的任务模块。|
|`taskInfo.title`|String|64||初始对话框标题。|
|`taskInfo.width`|String|||对话框宽度 - 以像素为单位的一个数字或默认布局，例如"large"、"medium"或"small"。|
|`taskInfo.height`|String|||对话框高度 - 以像素为单位的一个数字或默认布局，例如"large"、"medium"或"small"。|
|`taskInfo.url`|String|||初始 Web 视图 URL。|
|`messageHandlers`|对象数组|5 ||允许满足某些条件时调用应用的处理程序列表。 还必须在 中列出域 `validDomains` 。|
|`messageHandlers.type`|String|||消息处理程序的类型。 必须是 `"link"`。|
|`messageHandlers.value.domains`|Array of Strings|||链接邮件处理程序可以注册的域数组。|
|`parameters`|对象数组|5 |✔|命令采用的参数列表。 最小值：1;最大值：5|
|`parameter.name`|字符串|64 个字符|✔|显示在客户端中的参数的名称。 这包括在用户请求中。|
|`parameter.title`|String|32 个字符|✔|参数的用户友好标题。|
|`parameter.description`|String|128 个字符||描述此参数用途的用户友好字符串。|
|`parameter.inputType`|String|128 个字符||定义在任务模块上显示的控件的类型 `fetchTask: true` 。 `text` `textarea` `number` `date` `time` 、、、、、、、 `toggle` 之一 `choiceset` 。|
|`parameter.choices`|对象数组|10  ||的选项 `choiceset` 。 仅在 为 `parameter.inputType` `choiceset` 时使用 。|
|`parameter.choices.title`|String|128||选项的标题。|
|`parameter.choices.value`|String|512||选项的值。|

## <a name="permissions"></a>权限

**可选**

一个数组，指定应用请求哪些权限，让最终用户 `string` 知道扩展将执行什么操作。 以下选项非独占：

* `identity`&emsp;需要用户标识信息。
* `messageTeamMembers`&emsp;需要向团队成员发送直接消息的权限。

在更新应用时更改这些权限将导致用户在首次运行更新后的应用时重复同意过程。

## <a name="devicepermissions"></a>devicePermissions

**可选** 字符串数组

指定应用可能请求访问的用户设备上本机功能。 选项有：

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**可选**，但 **已指出的必需** 项除外

应用预期从其中加载任何内容的有效域的列表。 域列表可以包含通配符，例如 `*.example.com` 。 这完全匹配域的一个段;如果需要匹配，请使用 `a.b.example.com` `*.*.example.com` 。 如果你的选项卡配置或内容 UI 需要导航到除用于选项卡配置的其他任何其他域，则必须在此处指定该域。

但是 **，** 不需要在应用中包含要支持的标识提供程序的域。 例如，若要使用 Google ID 进行身份验证，必须重定向到 accounts.google.com，但不应将 accounts.google.com 包括在 `validDomains[]` 中。

> [!IMPORTANT]
> 不要直接或通过通配符添加超出你控制的域。 例如， `yourapp.onmicrosoft.com` 有效，但 `*.onmicrosoft.com` 无效。

对象是包含类型 的所有元素的数组 `string` 。

## <a name="webapplicationinfo"></a>webApplicationInfo

**可选**

指定 AAD 应用 ID 和Graph信息以帮助用户无缝登录到 AAD 应用。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`id`|String|36 个字符|✔|应用的 AAD 应用程序 ID。 此 ID 必须是 GUID。|
|`resource`|String|2048 个字符|✔|用于获取 SSO 身份验证令牌的应用的资源 URL。|
|`applicationPermissions`|数组|最多 100 个项目|✔|应用程序的资源权限。|

## <a name="configurableproperties"></a>configurableProperties

**可选** - 数组

`configurableProperties`此块定义管理员可Teams应用属性。 有关详细信息，请参阅自定义[应用程序中Microsoft Teams。](/MicrosoftTeams/customize-apps)

> [!NOTE]
> 必须定义至少一个属性。 最多可以在此块中定义九个属性。
> 最佳做法是，你必须提供自定义指南，以便应用用户和客户在自定义应用时遵循这些准则。 

可以定义以下任一属性：
* `name`：允许管理员更改应用显示名称。
* `shortDescription`：允许管理员更改应用的简短说明。
* `longDescription`：允许管理员更改应用的详细说明。
* `smallImageUrl`：它是 `outline` 清单块 `icons` 中的 属性。
* `largeImageUrl`：它是 `color` 清单块 `icons` 中的 属性。
* `accentColor`：它是要与 和 一起使用的颜色，作为大纲图标的背景。
* `websiteUrl`：它是 https:// 网站的 URL。
* `privacyUrl`：它是 https:// 隐私策略的 URL。
* `termsOfUseUrl`：它是 https:// 使用条款的 URL。

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

