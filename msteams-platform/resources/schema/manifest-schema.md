---
title: 清单架构参考
description: 介绍 Microsoft 团队清单支持的架构
keywords: 团队清单架构
ms.openlocfilehash: d4a2864c18a5066673bafab42a46733a0ab5f116
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673271"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>参考： Microsoft 团队的清单架构

Microsoft 团队清单介绍了应用程序如何集成到 Microsoft 团队产品中。 您的清单必须符合托管的架构[`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json)。 此外，还支持早期版本 1.0-1.4 （使用 URL 中的 "v1"）。

以下架构示例显示了所有扩展性选项。

## <a name="sample-full-manifest"></a>完整清单示例

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
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
    "defaultLanguageTag": "en-us",
    "additionalLanguages": [
      {
        "languageTag": "es-es",
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
        }
      ],
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
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
     "contoso.com",
     "mysite.someplace.com",
     "othersite.someplace.com"
  ]
}
```

架构定义了以下属性：

## <a name="schema"></a>$schema

*可选，但建议* &ndash;的字符串

引用清单的 JSON 架构的 https://URL。

## <a name="manifestversion"></a>manifestVersion

**必需** &ndash;的字符串

此清单使用的清单架构的版本。 它应为 "1.5"。

## <a name="version"></a>version

**必需** &ndash;的字符串

特定应用程序的版本。 如果您更新清单中的某些内容，该版本还必须递增。 这样一来，在安装新的清单时，它将覆盖现有的版本，用户将获得新的功能。 如果此应用程序已提交到应用商店，则必须重新提交新清单，然后再对其进行重新验证。 然后，此应用程序的用户将在几小时内自动获取新更新的清单（在批准后）。

如果应用程序要求更改权限，则系统将提示用户升级并重新同意该应用。

此版本字符串必须遵循[semver](http://semver.org/) STANDARD （主要。网格.修补程序）。

## <a name="id"></a>id

**必需** &ndash;的 Microsoft 应用程序 ID

Microsoft 为此应用程序生成的唯一标识符。 如果你已通过 Microsoft Bot 框架注册了 bot，或者你的选项卡的 web 应用已使用 Microsoft 登录，则你应该已经有 ID，应在此处输入它。 否则，应在 Microsoft 应用注册门户（[我的应用程序](https://apps.dev.microsoft.com)）上生成一个新的 ID，在此处输入它，然后在添加机器人时重用它。注意：如果您在 AppSource 中提交对现有应用程序的更新，您的清单中的 ID 不得修改。

## <a name="packagename"></a>packageName

**必需** &ndash;的字符串

此应用的以反向域表示法表示的唯一标识符;例如，.com. myapp。

## <a name="developer"></a>developer

**Required**

指定有关贵公司的信息。 对于提交到 AppSource （以前称为 "Office 应用商店"）的应用程序，这些值必须与您的 AppSource 条目中的信息相匹配。 有关详细信息，请参阅我们的[发布指南](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)。

|姓名| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`name`|32个字符|✔|开发人员的显示名称。|
|`websiteUrl`|2048 个字符|✔|开发人员网站的 https://URL。 此链接应将用户带到您的公司或特定于产品的登陆页面。|
|`privacyUrl`|2048 个字符|✔|开发人员的隐私策略的 https://URL。|
|`termsOfUseUrl`|2048 个字符|✔|开发人员使用条款的 https://URL。|
|`mpnId`|10个字符| |**可选**用于标识合作伙伴组织构建应用程序的 Microsoft 合作伙伴网络 ID。|

## <a name="localizationinfo"></a>localizationInfo

**可选**

允许指定默认语言，以及指向其他语言文件的指针。 请参阅[本地化](~/concepts/build-and-test/apps-localization.md)。

|姓名| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`defaultLanguageTag`||✔|此顶级清单文件中的字符串的语言标记。|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

指定其他语言翻译的对象的数组。

|姓名| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`languageTag`||✔|所提供文件中的字符串的语言标记。|
|`file`||✔|包含翻译字符串的 json 文件的相对文件路径。|

## <a name="name"></a>name

**Required**

在团队体验中向用户显示的应用程序体验的名称。 对于提交到 AppSource 的应用程序，这些值必须与您的 AppSource 条目中的信息相匹配。 `short`和`full`的值不应相同。

|姓名| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`short`|30 个字符|✔|应用程序的短显示名称。|
|`full`|100 个字符||应用程序的全名，如果完整的应用程序名称超过30个字符，则使用该名称。|

## <a name="description"></a>说明

**Required**

向用户介绍你的应用程序。 对于提交到 AppSource 的应用程序，这些值必须与您的 AppSource 条目中的信息相匹配。

确保你的说明准确描述你的体验，并提供信息，以帮助潜在客户了解你的体验。 如果需要使用外部帐户，还应在完整说明中说明。 `short`和`full`的值不应相同。  您的简短说明不得在详细说明中重复，并且不得包含任何其他应用程序名称。

|姓名| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`short`|80个字符|✔|在空间有限时使用的应用程序体验的简短说明。|
|`full`|4000个字符|✔|您的应用程序的完整说明。|

## <a name="icons"></a>图标

**Required**

在团队应用程序中使用的图标。 图标文件必须作为上载包的一部分包括在内。 有关详细信息，请参阅[图标](~/concepts/build-and-test/apps-package.md#icons)。

|姓名| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`outline`|2048 个字符|✔|指向透明 32x32 PNG 边框图标的相对文件路径。|
|`color`|2048 个字符|✔|完整颜色 192x192 PNG 图标的相对文件路径。|

## <a name="accentcolor"></a>accentColor

**必需** &ndash;的字符串

与大纲图标的背景一起使用的颜色。

值必须是以 "#" 开头的有效 HTML 颜色代码，例如`#4464ee`。

## <a name="configurabletabs"></a>configurableTabs

**可选**

当您的应用程序体验具有在添加之前需要额外配置的团队频道选项卡体验时使用。 仅在团队作用域中支持可配置的选项卡，并且每个应用程序目前仅支持一个选项卡。

对象是一个包含所有类型`object`的元素的数组。 仅在提供可配置的通道选项卡解决方案的解决方案中，此块才是必需的。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`configurationUrl`|String|2048 个字符|✔|配置选项卡时要使用的 https://URL。|
|`canUpdateConfiguration`|Boolean|||一个值，指示是否可在用户创建之后更新该选项卡的配置实例。 设置`true`|
|`scopes`|枚举数组|1 |✔|目前，可配置的`team`选项卡仅`groupchat`支持和范围。 |
|`sharePointPreviewImage`|String|2048||要在 SharePoint 中使用的选项卡预览图像的相对文件路径。 字号（1024x768）。 |
|`supportedSharePointHosts`|枚举数组|1 ||定义您的选项卡在 SharePoint 中的可用方式。 选项包括`sharePointFullPage`和`sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**可选**

定义一组可在默认情况下 "固定" 的选项卡，而无需用户手动添加它们。 在范围内声明`personal`的静态制表符始终固定到应用的个人体验中。 当前不支持在`team`范围中声明的静态选项卡。

对象是包含类型`object`的所有元素的数组（最多16个元素）。 仅在提供静态选项卡解决方案的解决方案中，此块是必需的。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`entityId`|String|64个字符|✔|选项卡显示的实体的唯一标识符。|
|`name`|String|128个字符|✔|该选项卡在通道接口中的显示名称。|
|`contentUrl`|String|2048 个字符|✔|指向要在团队画布中显示的实体 UI 的 https://URL。|
|`websiteUrl`|String|2048 个字符||要指向的 https://URL，如果用户要在浏览器中查看。|
|`scopes`|枚举数组|1 |✔|目前，静态选项卡仅支持`personal`作用域，这意味着它只能作为个人体验的一部分进行预配。|

## <a name="bots"></a>bot

**可选**

定义机器人解决方案以及可选信息，如默认的命令属性。

该对象是数组（每个应用程序最多&mdash;只能有一个一个 bot 仅允许一个 bot）和所有类型`object`的元素。 仅在提供机器人体验的解决方案中，此块才是必需的。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`botId`|String|64个字符|✔|与 Bot 框架一起注册的 bot 的唯一 Microsoft 应用 ID。 这可能与整体[应用程序 ID](#id)很好。|
|`needsChannelSelector`|Boolean|||描述 bot 是否利用用户提示将机器人添加到特定频道。 设置`false`|
|`isNotificationOnly`|Boolean|||指示 bot 是否为单向仅通知 bot，而不是对话机器人。 设置`false`|
|`supportsFiles`|Boolean|||指示 bot 是否支持在个人聊天中上载/下载文件的功能。 设置`false`|
|`scopes`|枚举数组|3 |✔|指定机器人是在中的频道上下文中`team`、在组中的聊天（`groupchat`）中，还是在仅限于单个用户（`personal`）的体验中提供体验。 这些选项是非独占的。|

### <a name="botscommandlists"></a>commandLists

你的 bot 可以向用户推荐的命令的可选列表。 对象是包含所有类型`object`元素的数组（最多2个元素）;您必须为你的 bot 支持的每个作用域定义单独的命令列表。 有关详细信息，请参阅[Bot 菜单](~/bots/how-to/create-a-bot-commands-menu.md)。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`items.scopes`|枚举数组|3 |✔|指定命令列表有效的范围。 选项包括`team`、 `personal`和`groupchat`。|
|`items.commands`|对象数组|10 |✔|机器人支持的命令数组：<br>`title`： bot 命令名称（string，32）<br>`description`：命令语法及其参数的简单说明或示例（string，128）|

## <a name="connectors"></a>插槽

**可选**

`connectors` Block 定义了应用程序的 Office 365 连接器。

对象是包含所有类型`object`元素的数组（最多1个元素）。 仅对提供连接器的解决方案而言，此块是必需的。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`configurationUrl`|String|2048 个字符|✔|配置连接器时要使用的 https://URL。|
|`connectorId`|String|64个字符|✔|与[连接器开发人员仪表板](https://aka.ms/connectorsdashboard)中的 ID 相匹配的连接器的唯一标识符。|
|`scopes`|枚举数组|1 |✔|指定连接器是在中的频道上下文中`team`，还是在仅限于单个用户的体验（`personal`）中提供体验。 目前，仅支持`team`作用域。|

## <a name="composeextensions"></a>composeExtensions

**可选**

定义应用程序的消息扩展。

> [!NOTE]
> 功能的名称已从11月2017的 "撰写分机" 更改为 "消息扩展"，但清单名称保持不变，以便现有扩展能够继续正常工作。

对象是包含所有类型`object`元素的数组（最多1个元素）。 仅对提供邮件扩展的解决方案而言，此块是必需的。

|名称| 类型 | 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`botId`|String|64|✔|与 Bot 框架一起注册的支持邮件扩展的 bot 的唯一 Microsoft 应用 ID。 这可能与整体应用程序 ID 很好。|
|`canUpdateConfiguration`|Boolean|||一个值，指示用户是否可以更新邮件扩展的配置。 默认值为`false`。|
|`commands`|对象数组|10 |✔|邮件扩展支持的命令数组|
|`messageHandlers`|对象数组|5 ||允许在满足特定条件时调用应用程序的处理程序列表。 域也必须列在`validDomains`|
|`messageHandlers.type`|String|||消息处理程序的类型。 必须是 `"link"`。|
|`messageHandlers.value.domains`|Array of Strings|||链接消息处理程序可以为其注册的域的数组。|

### <a name="composeextensionscommands"></a>composeExtensions

您的邮件扩展应声明一个或多个命令。 在 Microsoft 团队中，每个命令都显示为从基于 UI 的入口点的潜在交互。 最多可以有10个命令。

每个命令项都是一个具有以下结构的对象：

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`id`|String|64个字符|✔|命令的 ID|
|`type`|String|64个字符||命令的类型。 一个`query`或`action`。 设置`query`|
|`title`|String|32个字符|✔|用户友好的命令名称|
|`description`|String|128个字符||对用户显示的说明，以指示此命令的用途|
|`initialRun`|Boolean|||一个布尔值，指示是否在最初不使用任何参数的情况之下运行该命令。 设置`false`|
|`context`|Array of Strings|3 ||定义可以从中调用邮件扩展的位置。 、 `commandBox`、 `message`的`compose`的任意组合。 默认值为`["compose", "commandBox"]`|
|`fetchTask`|Boolean|||一个布尔值，指示是否应动态获取任务模块|
|`taskInfo`|对象|||指定在使用消息扩展命令时要预加载的任务模块|
|`taskInfo.title`|String|64||初始对话框标题|
|`taskInfo.width`|String|||对话框宽度-以像素为单位的数字或默认布局，如 "大"、"中" 或 "small"|
|`taskInfo.height`|String|||对话框高度-以像素为单位的数字或默认布局，如 "大"、"中" 或 "small"|
|`taskInfo.url`|String|||初始 web 视图 URL|
|`parameters`|对象数组|5 |✔|命令所采用的参数的列表。 最小值： 1;最大值：5|
|`parameter.name`|String|64个字符|✔|在客户端中显示的参数的名称。 此项包含在用户请求中。|
|`parameter.title`|String|32个字符|✔|参数的用户友好标题。|
|`parameter.description`|String|128个字符||描述此参数用途的用户友好字符串。|
|`parameter.inputType`|String|128个字符||定义在的任务模块上显示的控件的类型`fetchTask: true`。 一个`text` `textarea`、 `number` `date`、、、、 `time` `toggle``choiceset`|
|`parameter.choices`|对象数组|10 ||的选项选项`choiceset`。 仅在何时`parameter.inputType`使用`choiceset`|
|`parameter.choices.title`|String|128||选项的标题|
|`parameter.choices.value`|String|512||选项的值|

## <a name="permissions"></a>permissions

**可选**

一个数组， `string`它指定应用程序请求的权限，这样最终用户就可以知道扩展将如何执行。 以下选项是非独占的：

* `identity`&emsp;需要用户标识信息
* `messageTeamMembers`&emsp;需要向团队成员发送直接消息的权限

在更新应用程序时更改这些权限将导致用户在首次运行更新的应用程序时重复同意过程。 有关详细信息，请参阅[更新应用](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)。

## <a name="devicepermissions"></a>devicePermissions

**可选**字符串数组

在用户的设备上指定您的应用程序可能会请求访问的本机功能。 选项包括：

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**可选**，但**所需**的除外

应用程序希望在团队客户端中加载的网站的有效域列表。 例如`*.example.com`，域列表可以包含通配符。 这与域的一段完全匹配;如果需要匹配`a.b.example.com` ，请使用`*.*.example.com`。 如果您的选项卡配置或内容 UI 需要导航到其他任何域，除了用于选项卡配置之外，则必须在此处指定该域。

但是，**不**需要在您的应用程序中包含要支持的标识提供程序的域。 例如，若要使用 Google ID 进行身份验证，需要重定向到 accounts.google.com，但不应在中`validDomains[]`包含 accounts.google.com。

需要其自己的 sharepoint Url 的团队应用程序能够正常工作，可能会在其有效的域列表中包含 "{teamsitedomain}"。

> [!IMPORTANT]
> 不要直接或通过通配符添加位于控件外部的域。 例如， `yourapp.onmicrosoft.com`是有效的，但`*.onmicrosoft.com`无效。

对象是一个包含所有类型`string`的元素的数组。

## <a name="webapplicationinfo"></a>webApplicationInfo

**可选**

指定 AAD 应用 ID 和 Graph 信息，以帮助用户无缝登录 AAD 应用。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`id`|String|36个字符|✔|应用程序的 AAD 应用程序 id。 此 id 必须为 GUID。|
|`resource`|String|2048 个字符|✔|用于获取 SSO 的身份验证令牌的应用程序的资源 url。|
