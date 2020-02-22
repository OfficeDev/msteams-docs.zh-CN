---
title: 使用邮件扩展进行搜索
description: 介绍如何开发基于搜索的邮件扩展插件
keywords: 工作组邮件传递扩展邮件扩展搜索
ms.date: 07/20/2019
ms.openlocfilehash: c220d976fa3e9920c8d4bb332a793b23d9b294c4
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228043"
---
# <a name="search-with-messaging-extensions"></a>使用邮件扩展进行搜索

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

基于搜索的邮件扩展允许您查询服务并以卡片形式发送该信息，并将其发布到您的邮件中

![邮件扩展卡的示例](~/assets/images/compose-extensions/ceexample.png)

以下各节介绍如何执行此操作。

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="search-type-message-extensions"></a>搜索类型邮件扩展名

对于基于搜索的邮件扩展， `type`请将`query`参数设置为。 下面是包含单个搜索命令的清单示例。 单个消息传递扩展最长可以有10个不同的命令与之关联。 这可以包括多个搜索和多个基于操作的命令。

#### <a name="complete-app-manifest-example"></a>完整的应用程序清单示例

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.bing",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://bingbotservice.azurewebsites.net/",
    "privacyUrl": "http://bingbotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://bingbotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "Bing",
    "full": "Bing"
  },
  "description": {
    "short": "Find Bing search results",
    "full": "Find Bing search results and share them with your team members."
  },
  "icons": {
    "outline": "bing-outline.jpg",
    "color": "bing-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [{
          "id": "searchCmd",
          "description": "Search Bing for information on the web",
          "title": "Search",
          "initialRun": true,
          "parameters": [{
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "bingbotservice.azurewebsites.net",
    "*.bingbotservice.azurewebsites.net"
  ]
}
```

### <a name="test-via-uploading"></a>通过上传进行测试

您可以通过上载您的应用程序来测试您的邮件扩展。

若要打开邮件扩展插件，请导航到任何聊天或频道。 选择 "撰写" 框中的 "**更多选项**（**&#8943;**）" 按钮，然后选择您的邮件扩展。

## <a name="add-event-handlers"></a>添加事件处理程序

大部分工作都涉及`onQuery`事件，后者处理邮件扩展窗口中的所有交互。

如果在清单`canUpdateConfiguration`中`true`设置为，则会为邮件扩展启用 "**设置**" 菜单项，还必须处理`onQuerySettingsUrl`和`onSettingsUpdate`。

### <a name="handle-onquery-events"></a>处理 onQuery 事件

邮件扩展在邮件扩展`onQuery`窗口中发生任何事情或发送到窗口时，都会收到事件。

如果您的消息扩展使用配置页，则您的`onQuery`处理程序应首先检查是否有任何存储的配置信息;如果未配置邮件扩展，则返回一个`config`包含指向配置页面的链接的响应。 请注意，来自配置页面的响应也由`onQuery`处理。 （唯一例外是处理程序调用配置页面时`onQuerySettingsUrl`; 请参阅下一节。）

如果您的邮件扩展需要身份验证，请检查用户状态信息;如果用户未登录，请按照本主题后面的 "[身份验证](#authentication)" 一节中的说明操作。

接下来，检查`initialRun`是否已设置;如果是这样，请采取相应的操作，如提供说明或响应列表。

用于`onQuery`提示用户输入信息的处理程序的其余部分，显示预览卡的列表，并返回用户选择的卡片。

### <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a>处理 onQuerySettingsUrl 和 onSettingsUpdate 事件

和事件一起使用，以启用 "设置" 菜单项。 **** `onQuerySettingsUrl` `onSettingsUpdate`

!["设置" 菜单项的位置的屏幕截图](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

您的处理`onQuerySettingsUrl`程序用于返回配置页面的 URL;配置页面关闭后，您的处理程序`onSettingsUpdate`用于接受并保存返回的状态。 （这是`onQuery` *不*会从配置页接收响应的一种情况。）

## <a name="receive-and-respond-to-queries"></a>接收和响应查询

对邮件扩展的每个请求都是通过`Activity`发布到您的回调 URL 的对象来完成的。 请求包含有关用户命令的信息，如 ID 和参数值。 该请求还提供有关在其中调用扩展的上下文的元数据，包括用户和租户 ID，以及聊天 ID 或频道和团队 Id。

### <a name="receive-user-requests"></a>接收用户请求

当用户执行查询时，Microsoft 团队会将您的服务发送到一个`Activity`标准的 Bot 框架对象。 `Activity`对于已`type`设置为`invoke`并`name`设置为受支持`composeExtension`的类型的，您的服务应执行其逻辑，如下表所示。

除了标准 bot 活动属性之外，有效负载还包含以下请求元数据：

|属性名称|用途|
|---|---|
|`type`| 请求类型;必须为`invoke`。 |
|`name`| 向您的服务发出的命令的类型。 目前支持以下类型： <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| 发送请求的用户的 ID。 |
|`from.name`| 发送请求的用户的名称。 |
|`from.aadObjectId`| 发送请求的用户的 Azure Active Directory 对象 id。 |
|`channelData.tenant.id`| Azure Active Directory 租户 ID。 |
|`channelData.channel.id`| 通道 ID （如果请求是在通道中发出的）。 |
|`channelData.team.id`| "工作组 ID" （如果请求是在通道中进行的）。 |
|`clientInfo`|有关用于发送用户消息的客户端软件的可选元数据。 实体可以包含两个属性：<br>`country`字段包含用户检测到的位置。<br>`platform`字段描述邮件客户端平台。 <br>有关其他信息，请*参阅*[非 IRI 实体类型-clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)。|

请求参数本身位于 value 对象中，其中包括以下属性：

| 属性名称 | 用途 |
|---|---|
| `commandId` | 用户调用的命令的名称，与应用程序清单中声明的命令之一相匹配。 |
| `parameters` | 参数数组。 每个 parameter 对象包含参数名称，以及用户提供的参数值。 |
| `queryOptions` | 分页参数： <br>`skip`：跳过此查询的计数 <br>`count`：要返回的元素数 |

#### <a name="request-example"></a>请求示例

```json
{
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "searchKeywords",
        "value": "Toronto"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  "type": "invoke",
  "timestamp": "2017-05-01T15:45:51.876Z",
  "localTimestamp": "2017-05-01T08:45:51.876-07:00",
  "id": "f:622749630322482883",
  "channelId": "msteams",
  "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
  "from": {
    "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
    "name": "Larry Jin",
    "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
  },
  "conversation": {
    "id": "19:skypespaces_8198cfe0dd2647ae91930f0974768a40@thread.skype"
  },
  "recipient": {
    "id": "28:b4922ea1-5315-4fd0-9b21-d941ab06e39f",
    "name": "TheComposeExtensionDev"
  },
  "entities": [
    {
    "type": "clientInfo",
      "country": "US",
      "platform": "Windows"
    }
  ]
}
```

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a>接收来自插入到撰写消息框中的链接的请求

作为用于搜索外部服务的替代（或补充），您可以使用插入到 "撰写" 消息框中的 URL 来查询服务并返回一个卡片。 在下面的屏幕截图中，用户已在 Azure DevOps 中的工作项的 URL 中粘贴了邮件扩展已将其解析为卡片。

![Link unfurling 的示例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

若要使您的邮件扩展能够与链接进行交互，这种方法首先需要`messageHandlers`将该数组添加到应用程序清单中，如下例所示：

```json
"composeExtensions": [
  {
    "botId": "abc123456-ab12-ab12-ab12-abcdef123456",
    "messageHandlers": [
      {
        "type": "link",
        "value": {
          "domains": [
            "*.trackeddomain.com"
          ]
        }
      }
    ]
  }
]
```

在添加了要侦听应用程序清单的域之后，您需要更改您的 bot 代码以[响应](#respond-to-user-requests)以下调用请求。

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

如果您的应用程序返回多个项目，则仅使用第一个项目。

### <a name="respond-to-user-requests"></a>响应用户请求

当用户执行查询时，Microsoft 团队会向您的服务发出同步 HTTP 请求。 在这种情况下，您的代码有5秒的时间来提供对请求的 HTTP 响应。 在这段时间内，您的服务可以执行其他查找，或提供服务请求所需的任何其他业务逻辑。

您的服务应使用与用户查询匹配的结果进行响应。 响应必须指示 HTTP 状态代码`200 OK` ，以及具有以下正文的有效 application/json 对象：

|属性名称|用途|
|---|---|
|`composeExtension`|顶级响应信封。|
|`composeExtension.type`|响应的类型。 支持以下类型： <br>`result`：显示搜索结果列表 <br>`auth`：要求用户进行身份验证 <br>`config`：要求用户设置邮件扩展 <br>`message`：显示纯文本消息 |
|`composeExtension.attachmentLayout`|指定附件的布局。 用于类型`result`的响应。 <br>目前支持以下类型： <br>`list`：包含缩略图、标题和文本字段的卡片对象的列表 <br>`grid`：缩略图图像的网格 |
|`composeExtension.attachments`|有效的附件对象的数组。 用于类型`result`的响应。 <br>目前支持以下类型： <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|建议的操作。 用于类型`auth`或`config`的响应。 |
|`composeExtension.text`|要显示的消息。 用于类型`message`的响应。 |

#### <a name="response-card-types-and-previews"></a>响应卡片类型和预览

我们支持以下附件类型：

* [缩略图卡片](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [英雄卡片](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365 连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [自适应卡片](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

请参阅[卡片](~/task-modules-and-cards/what-are-cards.md)获取概述。

若要了解如何使用缩略图和英雄卡片类型，请参阅[添加卡片和卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。

有关 Office 365 连接器卡的其他文档，请参阅[使用 office 365 连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)。

结果列表显示在 Microsoft 团队 UI 中，每个项目都有一个预览。 将通过以下两种方式之一生成预览：

* 在`attachment`对象`preview`中使用属性。 该`preview`附件只能是一个英雄或缩略图卡片。
* 从附件的基本`title`、 `text`和`image`属性中提取。 仅当未设置该`preview`属性且这些属性可用时，才使用这些属性。

您可以仅通过设置其预览属性，在结果列表中显示自适应或 Office 365 连接器卡的预览。如果结果已经是英雄或缩略图卡片，则无需执行此步骤。 如果使用预览附件，则它必须是英雄或缩略图卡片。 如果未指定 preview 属性，卡片的预览将会失败，并且不会显示任何内容。

#### <a name="response-example"></a>响应示例

本示例显示一个响应，其中包含两个结果，混合不同的卡片格式： Office 365 连接器和自适应。 虽然您可能想要在响应中使用一种卡片格式，但它会显示`preview` `attachments`集合中每个元素的属性如何以所述的英雄或缩略图格式显式定义预览。

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "attachments": [
      {
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage": "https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value": "[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        }
      },
      {
        "contentType": "application/vnd.microsoft.card.adaptive",
        "content": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Container",
              "items": [
                {
                  "type": "TextBlock",
                  "text": "Microsoft Corp (NASDAQ: MSFT)",
                  "size": "medium",
                  "isSubtle": true
                },
                {
                  "type": "TextBlock",
                  "text": "September 19, 4:00 PM EST",
                  "isSubtle": true
                }
              ]
            },
            {
              "type": "Container",
              "spacing": "none",
              "items": [
                {
                  "type": "ColumnSet",
                  "columns": [
                    {
                      "type": "Column",
                      "width": "stretch",
                      "items": [
                        {
                          "type": "TextBlock",
                          "text": "75.30",
                          "size": "extraLarge"
                        },
                        {
                          "type": "TextBlock",
                          "text": "▼ 0.20 (0.32%)",
                          "size": "small",
                          "color": "attention",
                          "spacing": "none"
                        }
                      ]
                    },
                    {
                      "type": "Column",
                      "width": "auto",
                      "items": [
                        {
                          "type": "FactSet",
                          "facts": [
                            {
                              "title": "Open",
                              "value": "62.24"
                            },
                            {
                              "title": "High",
                              "value": "62.98"
                            },
                            {
                              "title": "Low",
                              "value": "62.20"
                            }
                          ]
                        }
                      ]
                    }
                  ]
                }
              ]
            }
          ],
          "version": "1.0"
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "Microsoft Corp (NASDAQ: MSFT)",
            "text": "75.30 ▼ 0.20 (0.32%)"
          }
        }
      }
    ]
  }
}
```

### <a name="default-query"></a>默认查询

如果在清单`initialRun`中`true`设置为，Microsoft 团队会在用户第一次打开邮件扩展时发出 "默认" 查询。 您的服务可以使用一组预填充的结果对此查询做出响应。 这对于显示（例如，最近查看的项目、收藏夹或其他不依赖于用户输入的信息）可能很有用。

默认查询的结构与任何常规用户查询相同，但其字符串值为`initialRun` `true`的参数除外。

#### <a name="request-example-for-a-default-query"></a>默认查询的请求示例

```json
{
  "type": "invoke",
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "initialRun",
        "value": "true"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  ⋮
}
```

## <a name="identify-the-user"></a>标识用户

对服务的每个请求都包括执行请求的用户的已模糊处理 ID，以及用户的显示名称和 Azure Active Directory 对象 ID。

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

`id`和`aadObjectId`值保证已通过身份验证的团队用户的。 它们可用作在您的服务中查找凭据或任何缓存状态时使用的键。 此外，每个请求都包含用户的 Azure Active Directory 租户 ID，可用于标识用户的组织。 如果适用，该请求还包含发出请求的团队和频道 Id。

## <a name="authentication"></a>身份验证

如果您的服务需要进行用户身份验证，则需要在用户登录后才能使用邮件扩展。 如果您已编写用于用户签名的 bot 或选项卡，则应熟悉此部分。

序列如下所示：

1. 用户发出查询，或将默认查询自动发送到您的服务。
2. 您的服务通过检查团队用户 ID 检查用户是否先进行身份验证。
3. 如果用户未通过身份验证，则发送回复`auth` ，并提供`openUrl`建议的操作，包括身份验证 URL。
4. Microsoft 团队客户端使用给定的身份验证 URL 启动承载你的网页的弹出窗口。
5. 用户登录后，应关闭窗口并向团队客户端发送 "身份验证代码"。
6. 然后，团队客户端将查询重新发出到您的服务，其中包括在步骤5中传递的身份验证代码。

您的服务应验证步骤6中收到的身份验证代码是否与步骤5中的验证代码相匹配。 这可确保恶意用户不会尝试欺骗或危害登录流。 这将有效地 "关闭循环" 以完成安全身份验证序列。

### <a name="respond-with-a-sign-in-action"></a>使用登录操作进行响应

若要提示未经过身份验证的用户登录，请使用包含身份验证`openUrl` URL 的 "类型" 建议操作进行响应。

#### <a name="response-example-for-a-sign-in-action"></a>登录操作的响应示例

```json
{
  "composeExtension":{
    "type":"auth",
    "suggestedActions":{
      "actions":[
        {
          "type": "openUrl",
          "value": "https://example.com/auth",
          "title": "Sign in to this app"
        }
      ]
    }
  }
}
```

> [!NOTE]
> 若要在团队弹出窗口中承载登录体验，URL 的域部分必须位于您的应用程序的有效域的列表中。 （请参阅清单架构中的[validDomains](~/resources/schema/manifest-schema.md#validdomains) 。）

### <a name="start-the-sign-in-flow"></a>启动登录流

您的登录体验应响应且适合弹出窗口。 它应与使用邮件传递的[Microsoft 团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client)集成。

与在 Microsoft 团队中运行的其他嵌入式体验一样，窗口中的代码需要先调用`microsoftTeams.initialize()`。 如果你的代码执行 OAuth 流，则可以将团队用户 ID 传递到你的窗口，然后可以将其传递到 OAuth 登录 URL。

### <a name="complete-the-sign-in-flow"></a>完成登录流

当登录请求完成并重定向回您的页面时，应执行以下步骤：

1. 生成安全代码。 （可以是一个随机数字。）您需要将此代码与您的服务进行缓存，以及通过登录流（例如 OAuth 2.0 令牌）获取的凭据。
2. 调用`microsoftTeams.authentication.notifySuccess`并传递安全代码。

此时，窗口将关闭，并将控制传递给团队客户端。 客户端现在可以重新发出原始用户查询，以及`state`属性中的安全代码。 您的代码可以使用安全代码查找之前存储的凭据以完成身份验证序列，然后完成用户请求。

#### <a name="reissued-request-example"></a>重新颁发的请求示例

```json
{
    "name": "composeExtension/query",
    "value": {
        "commandId": "insertWiki",
        "parameters": [{
            "name": "searchKeyword",
            "value": "lakers"
        }],
        "state": "12345",
        "queryOptions": {
            "skip": 0,
            "count": 25
        }
    },
    "type": "invoke",
    "timestamp": "2017-04-26T05:18:25.629Z",
    "localTimestamp": "2017-04-25T22:18:25.629-07:00",
    "entities": [{
        "type": "clientInfo",
        "country": "US",
        "platform": "Web",
        
    }],
    "text": "",
    "attachments": [],
    "address": {
        "id": "f:7638210432489287768",
        "channelId": "msteams",
        "user": {
            "id": "29:1A5TJWHkbOwSyu_L9Ktk9QFI1d_kBOEPeNEeO1INscpKHzHTvWfiau5AX_6y3SuiOby-r73dzHJ17HipUWqGPgw",
            "aadObjectId": "fc8ca1c0-d043-4af6-b09f-141536207403"
        },
        "conversation": {
            "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
        },
        "bot": {
            "id": "28:c073afa8-7e77-4f92-b3e7-aa589e952a3e",
            "name": "maotestbot2"
        },
        "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
        "useAuth": true
    },
    "source": "msteams"
}
```

## <a name="sdk-support"></a>SDK 支持

### <a name="net"></a>.NET

若要使用机器人生成器 SDK 为 .NET 接收和处理查询，您可以在 "传入`invoke` " 活动中检查操作类型，然后使用[NuGet 包 "."](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)中的帮助程序方法来确定它是否为邮件扩展活动。

#### <a name="example-code-in-net"></a>.NET 中的示例代码

```csharp
public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
{
    if (activity.Type == ActivityTypes.Invoke) // Received an invoke
    {
        if (activity.IsComposeExtensionQuery())
        {
            // This is the response object that will get sent back to the messaging extension request.
            ComposeExtensionResponse invokeResponse = null;

            // This helper method gets the query as an object.
            var query = activity.GetComposeExtensionQueryData();

            if (query.CommandId != null && query.Parameters != null && query.Parameters.Count > 0)
            {
                // query.Parameters has the parameters sent by client
                var results = new ComposeExtensionResult()
                {
                    AttachmentLayout = "list",
                    Type = "result",
                    Attachments = new List<ComposeExtensionAttachment>(),
                };
                invokeResponse.ComposeExtension = results;
            }

            // Return the response
            return Request.CreateResponse<ComposeExtensionResponse>(HttpStatusCode.OK, invokeResponse);
        } else
        {
            // Handle other types of Invoke activities here.
        }
    } else {
      // Failure case catch-all.
      var response = Request.CreateResponse(HttpStatusCode.BadRequest);
      response.Content = new StringContent("Invalid request! This API supports only messaging extension requests. Check your query and try again");
      return response;
    }
}
```

### <a name="nodejs"></a>Node.js

#### <a name="example-code-in-nodejs"></a>Node.js 中的示例代码

```javascript
require('dotenv').config();

import * as restify from 'restify';
import * as builder from 'botbuilder';
import * as teamBuilder from 'botbuilder-teams';

class App {
    run() {
        const server = restify.createServer();
        let teamChatConnector = new teamBuilder.TeamsChatConnector({
            appId: process.env.MICROSOFT_APP_ID,
            appPassword: process.env.MICROSOFT_APP_PASSWORD
        });

        // Command ID must match what's defined in manifest
        teamChatConnector.onQuery('<%= commandId %>',
            (event: builder.IEvent,
            query: teamBuilder.ComposeExtensionQuery,
            callback: (err: Error, result: teamBuilder.IComposeExtensionResponse, statusCode: number) => void) => {
                // Check for initialRun; i.e., when you should return default results
                // if (query.parameters[0].name === 'initialRun') {}

                // Check query.queryOptions.count and query.queryOptions.skip for paging

                // Return auth response
                // let response = teamBuilder.ComposeExtensionResponse.auth().actions([
                //     builder.CardAction.openUrl(null, 'https://authUrl', 'Please sign in')
                // ]).toResponse();

                // Return config response
                // let response = teamBuilder.ComposeExtensionResponse.config().actions([
                //     builder.CardAction.openUrl(null, 'https://configUrl', 'Please sign in')
                // ]).toResponse();

                // Return result response
                let response = teamBuilder.ComposeExtensionResponse.result('list').attachments([
                    new builder.ThumbnailCard()
                        .title('Test thumbnail card')
                        .text('This is a test thumbnail card')
                        .images([new builder.CardImage().url('https://bot-framework.azureedge.net/bot-icons-v1/bot-framework-default-9.png')])
                        .toAttachment()
                ]).toResponse();
                callback(null, response, 200);
            });
        server.post('/api/composeExtension', teamChatConnector.listen());
        server.listen(process.env.PORT, () => console.log(`listening to port:` + process.env.PORT));
    }
}

const app = new App();
app.run();
```
*另请参阅* [Bot 框架示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。
