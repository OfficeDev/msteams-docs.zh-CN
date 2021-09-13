---
title: 使用邮件扩展进行搜索
description: 介绍如何开发基于搜索的邮件扩展
keywords: teams 邮件扩展邮件扩展搜索
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 07/20/2019
ms.openlocfilehash: a8e4a80835dade53c129e9efe1b21cd6715104ce
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156013"
---
# <a name="search-with-messaging-extensions"></a>使用邮件扩展进行搜索

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

基于搜索的邮件扩展允许你查询服务，以卡片的形式将该信息张贴到邮件中。

![邮件扩展卡示例](~/assets/images/compose-extensions/ceexample.png)

以下各节介绍如何执行下列操作：

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="search-type-message-extensions"></a>搜索类型邮件扩展

对于基于搜索的邮件扩展，将 `type` 参数设置为 `query` 。 下面是一个使用单个搜索命令的清单示例。 单个邮件扩展最多可以有 10 个不同的命令与之关联。 这可包括多个搜索和多个基于操作的命令。

#### <a name="complete-app-manifest-example"></a>完整的应用清单示例

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
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

可以通过上传应用来测试邮件扩展。

若要打开消息扩展，请导航到任何聊天或频道。 在撰写 **框中** 选择" (&#8943;) "按钮，然后选择邮件扩展。 

## <a name="add-event-handlers"></a>添加事件处理程序

大多数工作都涉及 事件，该事件处理邮件扩展 `onQuery` 窗口中的所有交互。

如果在清单中设置为 ，则为邮件设置启用"联系人"菜单项，并且 `canUpdateConfiguration` `true` 还必须处理 和 `onQuerySettingsUrl` `onSettingsUpdate` 。

### <a name="handle-onquery-events"></a>处理 onQuery 事件

邮件扩展在邮件扩展窗口中发生任何事件或发送到该窗口时 `onQuery` 接收事件。

如果邮件扩展使用配置页，则 处理程序应首先检查任何存储的配置信息;如果未配置邮件扩展，则返回响应，并返回指向配置页面 `onQuery` `config` 的链接。 请注意，来自配置页面的响应也由 处理 `onQuery` 。 唯一的例外是由 的处理程序调用配置页时; `onQuerySettingsUrl` 请参阅以下部分：

如果邮件扩展需要身份验证，请检查用户状态信息;如果用户未登录，请按照本主题稍后的身份验证 [部分中](#authentication) 的说明进行操作。

接下来，检查是否已设置;如果是，则采取相应的操作，例如提供说明 `initialRun` 或响应列表。

其余处理程序将提示用户输入信息，显示预览卡片列表，并返回 `onQuery` 用户选择的卡片。

### <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a>处理 onQuerySettingsUrl 和 onSettingsUpdate 事件

和 `onQuerySettingsUrl` `onSettingsUpdate` 事件协同工作以启用设置菜单项。 

![菜单项的位置设置屏幕截图](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

的处理程序返回配置页的 URL;配置页关闭后，您的 `onQuerySettingsUrl` 处理程序接受 `onSettingsUpdate` 并保存返回的状态。 这是一个无法 `onQuery` *从* 配置页面接收响应的情况。

## <a name="receive-and-respond-to-queries"></a>接收和响应查询

对消息扩展的每次请求都通过发布至回调 `Activity` URL 的对象完成。 请求包含有关用户命令的信息，如 ID 和参数值。 请求还会提供有关调用扩展的上下文的元数据，包括用户和租户 ID，以及聊天 ID 或频道和团队 ID。

### <a name="receive-user-requests"></a>接收用户请求

当用户执行查询时，Microsoft Teams向服务发送标准 Bot Framework `Activity` 对象。 服务应执行其逻辑，该逻辑已设置为 并设置为支持 `Activity` `type` `invoke` `name` `composeExtension` 的类型，如下表所示。

除了标准自动程序活动属性之外，有效负载还包含以下请求元数据：

|属性名称|用途|
|---|---|
|`type`| 请求类型;必须为 `invoke` 。 |
|`name`| 向服务发出的命令类型。 目前支持以下类型： <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| 发送请求的用户的 ID。 |
|`from.name`| 发送请求的用户的名称。 |
|`from.aadObjectId`| Azure Active Directory发送请求的用户的对象 ID。 |
|`channelData.tenant.id`| Azure Active Directory 租户 ID。 |
|`channelData.channel.id`| 如果在 (通道中提出请求，频道 ID 将) 。 |
|`channelData.team.id`| 如果 (频道中提出请求，团队 ID 将) 。 |
|`clientInfo`|有关用于发送用户消息的客户端软件的可选元数据。 实体可以包含两个属性：<br>`country`该字段包含用户的检测位置。<br>`platform`字段描述消息客户端平台。 <br>有关其他信息，请参阅 *非* [IRI 实体类型 — clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)。|

请求参数本身位于 value 对象中，其中包括以下属性：

| 属性名称 | 用途 |
|---|---|
| `commandId` | 用户调用的命令的名称，与在应用清单中声明的命令之一匹配。 |
| `parameters` | 参数数组：每个参数对象都包含参数名称以及用户提供的参数值。 |
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

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a>从插入撰写消息框的链接接收请求

作为一 (或除了) 外部服务外，您还可以使用插入到撰写消息框中的 URL 查询您的服务并返回一张卡片。 在下面的屏幕截图中，用户已粘贴到邮件扩展已解析为Azure DevOps中工作项的 URL。

![链接取消链接示例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

若要使邮件扩展能够与链接进行交互，你首先需要将数组添加到应用清单， `messageHandlers` 如以下示例所示：

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

添加域以侦听应用清单后，你需要更改自动程序代码以 [响应](#respond-to-user-requests) 以下调用请求。

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

如果你的应用返回多个项目，则只会使用第一个项目。

### <a name="respond-to-user-requests"></a>响应用户请求

当用户执行查询时，Microsoft Teams向服务发送同步 HTTP 请求。 此时，您的代码有 5 秒时间提供对请求的 HTTP 响应。 在此期间，你的服务可以执行其他查找，或执行为请求提供服务所需的任何其他业务逻辑。

服务应响应与用户查询匹配的结果。 响应必须指示 的 HTTP 状态代码和具有以下正文的有效 `200 OK` application/json 对象：

|属性名称|用途|
|---|---|
|`composeExtension`|顶级响应信封。|
|`composeExtension.type`|响应类型。 支持以下类型： <br>`result`：显示搜索结果列表 <br>`auth`：要求用户进行身份验证 <br>`config`：要求用户设置邮件扩展 <br>`message`: 显示纯文本邮件 |
|`composeExtension.attachmentLayout`|指定附件的布局。 用于 类型 `result` 的响应。 <br>目前支持以下类型： <br>`list`：包含缩略图、标题和文本字段的卡片对象列表 <br>`grid`：缩略图图像的网格 |
|`composeExtension.attachments`|有效 attachment 对象的数组。 用于 类型 `result` 的响应。 <br>目前支持以下类型： <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|建议的操作。 用于 或 类型的 `auth` 响应 `config` 。 |
|`composeExtension.text`|要显示的消息。 用于 类型 `message` 的响应。 |

#### <a name="response-card-types-and-previews"></a>响应卡类型和预览

我们支持以下附件类型：

* [缩略图卡片](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Hero card](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [自适应卡片](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

有关详细信息，请参阅有关概述 [的](~/task-modules-and-cards/what-are-cards.md) 卡片。

若要了解如何使用缩略图和 Hero 卡片类型，请参阅 [添加卡片和卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。

有关连接器卡的其他Office 365，请参阅使用[Office 365 连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)。

结果列表显示在项目 UI 中Microsoft Teams每个项目的预览。 预览以以下两种方式之一生成：

* 在 `preview` 对象内使用 `attachment` 属性。 附件 `preview` 只能是 Hero 或 Thumbnail 卡片。
* 从附件的基本 `title` 、 `text` 和 `image` 属性中提取。 只有在属性未设置且这些属性可用 `preview` 时，才使用这些属性。

只需设置自适应或Office 365预览属性，就可以在结果列表中显示自适应或连接器卡片的预览;如果结果已是 hero 或 thumbnail 卡片，则不需要这样做。 如果使用预览附件，它必须是 Hero 或 Thumbnail 卡片。 如果未指定任何预览属性，则卡片预览将失败，并且不会显示任何内容。

#### <a name="response-example"></a>响应示例

此示例显示包含两个结果的响应，混合了不同的卡片格式：Office 365 Connector 和 Adaptive。 虽然你可能想要在响应中坚持使用一个卡片格式，但它显示了集合中每个元素的 属性如何显式定义以 hero 或 thumbnail 格式的预览 `preview` `attachments` ，如上所述。

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
              "activityImage&quot;: &quot;https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value&quot;: &quot;[Larry Brown](mailto:larryb@example.com)"
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

如果在清单中设置为 ，则Microsoft Teams用户首次打开邮件扩展时，将发送"默认 `initialRun` `true` "查询。 你的服务可以使用一组预填充的结果来响应此查询。 这可用于显示最近查看的项目、收藏夹或其他不依赖于用户输入的信息。

默认查询的结构与任何常规用户查询相同，字符串值为 的参数除外 `initialRun` `true` 。

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

每个对服务的请求都包括执行请求的用户的模糊 ID，以及用户的 显示名称 和 Azure Active Directory 对象 ID。

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

`id`和 `aadObjectId` 值保证为经过身份验证的用户Teams的值。 它们可用作在服务中查找凭据或任何缓存状态的密钥。 此外，每个请求都包含Azure Active Directory租户 ID，可用于标识用户的组织。 如果适用，请求还包含源自请求的团队和频道的 ID。

## <a name="authentication"></a>身份验证

如果服务需要用户身份验证，则需要先登录用户，然后才能使用消息传递扩展。 如果你已编写登录用户的自动程序或选项卡，应熟悉此部分。

顺序如下所示：

1. 用户发出查询，或者默认查询将自动发送到您的服务。
2. 服务通过检查用户 ID 来检查用户是否首先Teams身份验证。
3. 如果用户尚未进行身份验证，请发送回包含建议操作（包括身份验证 `auth` `openUrl` URL）的响应。
4. 客户端Microsoft Teams给定身份验证 URL 启动承载网页的弹出窗口。
5. 用户登录后，应关闭窗口，并将"身份验证代码"Teams客户端。
6. 然后Teams客户端向服务重新提供查询，其中包括步骤 5 中传递的身份验证代码。

服务应验证步骤 6 中收到的身份验证代码是否与步骤 5 中的身份验证代码匹配。 这可确保恶意用户不会尝试欺骗或破坏登录流。 这实际上"关闭循环"以完成安全身份验证序列。

### <a name="respond-with-a-sign-in-action"></a>使用登录操作响应

若要提示未经身份验证的用户登录，请通过包含身份验证 URL 的类型的建议操作 `openUrl` 进行响应。

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
> 若要在弹出窗口中托管登录Teams，URL 的域部分必须位于应用的有效域列表中。 有关详细信息，请参阅[清单架构中的 validDomains。](~/resources/schema/manifest-schema.md#validdomains)

### <a name="start-the-sign-in-flow"></a>启动登录流程

你的登录体验应响应迅速且适合弹出窗口。 它应与使用消息Microsoft Teams [JavaScript 客户端 SDK](/javascript/api/overview/msteams-client)集成。

与其他嵌入体验一样，Microsoft Teams内的代码需要先调用 `microsoftTeams.initialize()` 。 如果你的代码执行 OAuth 流，你可以将Teams用户 ID 传递到你的窗口，然后可以将它传递到 OAuth 登录 URL。

### <a name="complete-the-sign-in-flow"></a>完成登录流程

当登录请求完成并重定向回你的页面时，它应执行以下步骤：

1. 生成安全代码。  (这是一个随机数字。) 您需要在服务上缓存此代码，以及通过登录流（如 OAuth 2.0 令牌）获取的凭据。
2. 调用 `microsoftTeams.authentication.notifySuccess` 并传递安全代码。

此时，窗口关闭，控件将传递给Teams客户端。 客户端现在可以重新发送原始用户查询以及 属性中的安全 `state` 代码。 代码可以使用安全代码查找之前存储的凭据以完成身份验证序列，然后完成用户请求。

#### <a name="reissued-request-example"></a>重新请求示例

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

若要使用适用于 .NET 的 Bot Builder SDK 接收和处理查询，可以检查传入活动上的操作类型，然后使用 NuGet 程序包 `invoke` [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)中的帮助程序方法确定它是否是消息传递扩展活动。

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

#### <a name="example-code-in-nodejs"></a>示例代码Node.js

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

## <a name="see-also"></a>另请参阅

[Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。
