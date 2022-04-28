---
title: 使用消息扩展进行搜索
description: 介绍如何开发基于搜索的消息扩展插件
keywords: teams 消息扩展消息扩展搜索
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 07/20/2019
ms.openlocfilehash: 13915bc3e67f6d5789fe9e977f6579a05a010542
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104397"
---
# <a name="search-with-message-extensions"></a>使用消息扩展进行搜索

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

使用基于搜索的消息扩展插件，可以查询服务，然后以卡片的形式将该信息直接发布到邮件中。

![消息扩展卡的示例](~/assets/images/compose-extensions/ceexample.png)

以下部分介绍如何执行此操作：

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

## <a name="search-type-message-extensions"></a>搜索类型消息扩展插件

对于基于搜索的消息扩展，请将 `type` 参数设置为 `query`。 下面是包含单个搜索命令的清单示例。 单个消息扩展最多可以有 10 个不同的命令与之关联。 这可以包括多个搜索和多个基于操作的命令。

### <a name="complete-app-manifest-example"></a>完整的应用清单示例

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

## <a name="test-via-uploading"></a>通过上传进行测试

可以通过上传应用来测试消息扩展。

若要打开邮件扩展插件，请导航到任何聊天或频道。 在撰写框中选择“ **更多”选项** **(&#8943;**) 按钮，然后选择邮件扩展。

## <a name="add-event-handlers"></a>添加事件处理程序

大部分工作都涉及该 `onQuery` 事件，该事件处理消息扩展窗口中的所有交互。

如果设置为`canUpdateConfiguration``true`清单中，则为消息扩展启用 **设置** 菜单项，并且还必须处理和`onSettingsUpdate`处理`onQuerySettingsUrl`。

## <a name="handle-onquery-events"></a>处理 onQuery 事件

消息扩展在消息扩展窗口中发生任何事件或发送到窗口时接收 `onQuery` 事件。

如果消息扩展使用配置页，则处理程序 `onQuery` 应首先检查是否存在任何存储的配置信息;如果未配置消息扩展名，则返回带有 `config` 配置页链接的响应。 请注意，配置页的响应也由 `onQuery`处理。 唯一的例外是处理程序 `onQuerySettingsUrl`调用配置页时;请参阅以下部分：

如果消息扩展需要身份验证，请检查用户状态信息;如果用户未登录，请按照本主题后面的 [“身份验证”](#authentication) 部分中的说明操作。

接下来，检查是否 `initialRun` 已设置;如果是，请采取适当的操作，例如提供说明或响应列表。

处理程序的其余部分提示 `onQuery` 用户获取信息，显示预览卡列表，并返回用户选择的卡片。

## <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a>处理 onQuerySettingsUrl 和 onSettingsUpdate 事件

和`onQuerySettingsUrl``onSettingsUpdate`事件协同工作，以启用 **设置** 菜单项。

![设置菜单项位置的屏幕截图](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

用于返回配置页的 URL 的处理程序 `onQuerySettingsUrl` ;在配置页关闭后，你的处理程序接受 `onSettingsUpdate` 并保存返回的状态。 在这种情况下，`onQuery`*不会* 从配置页接收响应。

## <a name="receive-and-respond-to-queries"></a>接收和响应查询

对消息扩展的每个请求都是通过 `Activity` 发布到回调 URL 的对象完成的。 请求包含有关用户命令的信息，例如 ID 和参数值。 该请求还提供有关调用扩展的上下文的元数据，包括用户和租户 ID，以及聊天 ID、频道和团队 ID。

### <a name="receive-user-requests"></a>接收用户请求

当用户执行查询时，Microsoft Teams向服务发送标准 Bot Framework `Activity` 对象。 服务应为已`type`设置`invoke`为`Activity`受`name`支持的`composeExtension`类型的服务执行其逻辑，如下表所示。

除了标准机器人活动属性外，有效负载还包含以下请求元数据：

|属性名称|用途|
|---|---|
|`type`| 请求类型;必须是 `invoke`. |
|`name`| 颁发给服务的命令类型。 目前支持以下类型： <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| 发送请求的用户的 ID。 |
|`from.name`| 发送请求的用户的名称。 |
|`from.aadObjectId`| Microsoft Azure Active Directory (Azure AD) 发送请求的用户的对象 ID。 |
|`channelData.tenant.id`| Microsoft Azure Active Directory (Azure AD) 租户 ID。 |
|`channelData.channel.id`| 如果请求是在通道) 中发出，则通道 ID (。 |
|`channelData.team.id`| 如果请求是在频道) 中发出，团队 ID (。 |
|`clientInfo`|有关用于发送用户消息的客户端软件的可选元数据。 实体可以包含两个属性：<br>该 `country` 字段包含用户检测到的位置。<br>该 `platform` 字段介绍消息传送客户端平台。 <br>有关其他信息，请 *参阅*[非 IRI 实体类型 - clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)。|

请求参数本身位于值对象中，其中包括以下属性：

| 属性名称 | 用途 |
|---|---|
| `commandId` | 用户调用的命令的名称，与应用清单中声明的命令之一匹配。 |
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

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a>从插入撰写消息框中的链接接收请求

作为搜索外部服务的替代 (或) ，可以使用插入撰写消息框中的 URL 来查询服务并返回卡片。 在下面的屏幕截图中，用户已粘贴到Azure DevOps中已将消息扩展解析为卡片的工作项的 URL 中。

![链接展开示例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

若要使消息扩展能够以这种方式与链接交互，首先需要将数组添加 `messageHandlers` 到应用清单，如以下示例所示：

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

添加域以侦听应用清单后，需要更改机器人代码以 [响应](#respond-to-user-requests) 以下调用请求。

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

如果应用返回多个项，则仅使用第一个项目。

### <a name="respond-to-user-requests"></a>响应用户请求

当用户执行查询时，Microsoft Teams向服务发出同步 HTTP 请求。 此时，代码有 5 秒的时间提供对请求的 HTTP 响应。 在此期间，服务可以执行其他查找或为请求提供服务所需的任何其他业务逻辑。

服务应响应与用户查询匹配的结果。 响应必须指示具有以下正文的 `200 OK` HTTP 状态代码和有效的 application/json 对象：

|属性名称|用途|
|---|---|
|`composeExtension`|顶级响应信封。|
|`composeExtension.type`|响应类型。 支持以下类型： <br>`result`：显示搜索结果的列表 <br>`auth`：要求用户进行身份验证 <br>`config`：要求用户设置消息扩展插件 <br>`message`: 显示纯文本邮件 |
|`composeExtension.attachmentLayout`|指定附件的布局。 用于类型 `result`响应。 <br>目前支持以下类型： <br>`list`：包含缩略图、标题和文本字段的卡片对象列表 <br>`grid`：缩略图图像的网格 |
|`composeExtension.attachments`|有效附件对象的数组。 用于类型 `result`响应。 <br>目前支持以下类型： <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|建议的操作。 用于类型或 `config`. `auth` 的响应。 |
|`composeExtension.text`|要显示的消息。 用于类型 `message`响应。 |

#### <a name="response-card-types-and-previews"></a>响应卡类型和预览

我们支持以下附件类型：

* [缩略图卡](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [主图卡](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365 连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [自适应卡片](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

有关详细信息，请参阅 [卡](~/task-modules-and-cards/what-are-cards.md) 片以获取概述。

若要了解如何使用缩略图和主图卡类型，请 [参阅“添加卡片和卡片”操作](~/task-modules-and-cards/cards/cards-actions.md)。

有关Office 365连接器卡的其他文档，请参阅[“使用Office 365连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)”。

结果列表显示在每个项的预览Microsoft Teams UI 中。 预览版是通过以下两种方式之一生成的：

* `preview`使用对象中的`attachment`属性。 附 `preview` 件只能是 Hero 或缩略图卡。
* 从附件的基本`title``text`属性和`image`属性中提取。 仅当未设置属性且这些属性可用时 `preview` ，才使用这些属性。

只需设置结果列表的预览属性，即可在结果列表中显示自适应或Office 365连接器卡片的预览;如果结果已经是主图或缩略图卡，则不需要此功能。 如果使用预览附件，则它必须是 Hero 卡或缩略图卡。 如果未指定预览属性，则卡片预览将失败，不会显示任何内容。

#### <a name="response-example"></a>响应示例

此示例显示包含两个结果的响应，其中混合了不同的卡片格式：Office 365连接器和自适应。 虽然你可能希望在响应中保留一种卡片格式，但它显示了集合中每个元素的`attachments`属性必须如何`preview`显式定义预览版或缩略图格式，如上所述。

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

如果设置`initialRun`为`true`在清单中，Microsoft Teams用户首次打开消息扩展时发出“默认”查询。 服务可以使用一组预填充的结果来响应此查询。 这对于显示最近查看的项目、收藏夹或不依赖于用户输入的任何其他信息非常有用。

默认查询的结构与任何常规用户查询相同，但字符串值为`true`其参数`initialRun`除外。

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

对服务的每个请求包括执行请求的用户的模糊 ID，以及用户的显示名称和Microsoft Azure Active Directory (Azure AD) 对象 ID。

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

保证`id`和`aadObjectId`值是经过身份验证的Teams用户的值。 它们可以用作密钥来查找凭据或服务中的任何缓存状态。 此外，每个请求都包含用户的Microsoft Azure Active Directory (Azure AD) 租户 ID，可用于标识用户的组织。 如果适用，请求还包含从中发起请求的团队和通道 ID。

## <a name="authentication"></a>身份验证

如果服务需要用户身份验证，则需要先登录用户，然后才能使用消息扩展名。 如果已编写机器人或登录用户的选项卡，则应熟悉此部分。

序列如下所示：

1. 用户发出查询，或者默认查询会自动发送到服务。
2. 服务通过检查Teams用户 ID 来检查用户是否已首次进行身份验证。
3. 如果用户尚未进行身份验证，请使用建议的`openUrl`操作（包括身份验证 URL）发回`auth`响应。
4. Microsoft Teams客户端使用给定的身份验证 URL 启动托管网页的弹出窗口。
5. 用户登录后，应关闭窗口并将“身份验证代码”发送到Teams客户端。
6. 然后，Teams客户端将查询重新颁发到服务，其中包括在步骤 5 中传递的身份验证代码。

服务应验证步骤 6 中收到的身份验证代码是否与步骤 5 中的身份验证代码匹配。 这可确保恶意用户不会尝试欺骗或破坏登录流。 这可以有效地“关闭循环”以完成安全身份验证序列。

### <a name="respond-with-a-sign-in-action"></a>使用登录操作进行响应

若要提示未经身份验证的用户登录，请使用包含身份验证 URL 的类型 `openUrl` 建议操作进行响应。

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
> 若要在Teams弹出窗口中托管登录体验，URL 的域部分必须位于应用的有效域列表中。 有关详细信息，请参阅清单架构中的 [validDomains](~/resources/schema/manifest-schema.md#validdomains) 。

### <a name="start-the-sign-in-flow"></a>启动登录流

登录体验应具有响应能力，并适合在弹出窗口中。 它应与使用消息传递[的 Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 集成。

与Microsoft Teams内运行的其他嵌入式体验一样，窗口内的代码需要先调用`microsoftTeams.initialize()`。 如果代码执行 OAuth 流，则可以将Teams用户 ID 传递到窗口，然后将其传递到 OAuth 登录 URL。

### <a name="complete-the-sign-in-flow"></a>完成登录流

登录请求完成并重定向回页面后，应执行以下步骤：

1. 生成安全代码。  (这可能是一个随机数字。) 需要在服务上缓存此代码，以及通过登录流（例如 OAuth 2.0 令牌）获取的凭据。
2. 调用 `microsoftTeams.authentication.notifySuccess` 并传递安全代码。

此时，窗口关闭，控件传递给Teams客户端。 客户端现在可以重新发布原始用户查询，以及属性中 `state` 的安全代码。 代码可以使用安全代码查找之前存储的凭据以完成身份验证序列，然后完成用户请求。

#### <a name="reissued-request-example"></a>重新发出的请求示例

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

若要使用 Bot Builder SDK for .NET 接收和处理查询，可以检查`invoke`传入活动的操作类型，然后使用 NuGet 包 [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) 中的帮助程序方法来确定它是否是消息扩展活动。

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

#### <a name="example-code-in-nodejs"></a>Node.js中的示例代码

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
