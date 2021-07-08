---
title: 生成自适应卡片选项卡
author: KirtiPereira
description: 使用自适应卡片生成选项卡
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 5a66f49db3710885b926a7abce45ef858bf0b092
ms.sourcegitcommit: b1f9162a0bbcd276064ae9e4f1e8bccc06cb7035
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2021
ms.locfileid: "53328056"
---
# <a name="build-tabs-with-adaptive-cards"></a>具有自适应卡片的生成选项卡

> [!IMPORTANT]
> * 此功能 [在公用开发者预览版](~/resources/dev-preview/developer-preview-intro.md) 桌面和移动版中受支持。 即将推出 Web 浏览器中的支持。
> * 带自适应卡片的选项卡当前仅作为个人应用受支持。

使用传统方法开发选项卡时，您可能会遇到这些问题，如 HTML 和 CSS 注意事项、加载时间较慢、iFrame 约束以及服务器维护和成本。 自适应卡片选项卡是一种在卡片中生成选项卡的Teams。 你可以将自适应卡片呈现到选项卡，而不是在 IFrame 中嵌入 Web 内容。前端使用自适应卡片呈现，而后端由机器人提供电源。 机器人负责接受请求，以及使用呈现的自适应卡片进行相应响应。

可以使用现成的用户界面和 UI 构建选项卡 (UI) 在桌面、Web 和移动设备上具有本机外观的 Lego 块。 本文可帮助你了解对应用清单所需的更改、调用活动如何请求和发送带自适应卡片的选项卡信息，以及对任务模块工作流的影响。

下图描述了使用桌面和移动版自适应卡片生成选项卡：

:::image type="content" source="../../assets/images/tabs/adaptive-cards-rendered-in-tabs.jpg" alt-text="选项卡中呈现的自适应卡片示例。" border="false":::

## <a name="prerequisites"></a>先决条件

在开始使用自适应卡片生成选项卡之前，你必须：

* 熟悉自动程序[开发、](../../bots/what-are-bots.md)[自适应卡片](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)和 Teams[](../../task-modules-and-cards/task-modules/task-modules-bots.md)中的任务模块。
* 使机器人在 Teams中运行，以用于你的开发。
* 在公共[开发者预览版。](~/resources/dev-preview/developer-preview-intro.md)

## <a name="changes-to-app-manifest"></a>对应用清单的更改

呈现选项卡的个人应用必须在其应用 `staticTabs` 清单中包括数组。 在定义中提供 属性时 `contentBotId` ，将呈现自适应卡片 `staticTab` 选项卡。 静态选项卡定义必须包含 ，指定自适应 `contentBotId` 卡片选项卡或 `contentUrl` ，指定典型的托管 Web 内容选项卡体验。

> [!NOTE]
> `contentBotId`属性当前在清单版本 1.9 或更高版本中可用。

为 `contentBotId` 属性提供 `botId` "自适应卡片"选项卡必须通信的 。 为"自适应卡片"选项卡配置的在每个调用请求的参数中发送，并可用于区分由同一自动程序提供电源的自适应卡片 `entityId` `tabContext` 选项卡。 有关其他静态选项卡定义字段的信息，请参阅 [清单架构](../../resources/schema/manifest-schema.md#statictabs)。

下面是自适应卡片选项卡清单示例：

```json
{
  "$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
  "manifestVersion": "1.9",
  "id": "00000000-0000-0000-0000-000000000000",
  "version": "0.0.1",
  "packageName": "acprototype",
  "developer": {
    "name": "Contoso",
    "websiteUrl": "https://contoso.yourwebsite.com",
    "privacyUrl": "https://contoso.yourwebsite.com/privacy.html",
    "termsOfUseUrl": "https://contoso.yourwebsite.com/terms.html"
  },
  "name": {
    "short": "Contoso",
    "full": "Contoso Home"
  },
  "description": {
    "short": "Add short description here",
    "full": "Add full description here"
  },
  "icons": {
    "outline": "icon-outline.png",
    "color": "icon-color.png"
  },
  "accentColor": "#D85028",
  "configurableTabs": [],
  "staticTabs": [
    {
      "entityId": "homeTab",
      "name": "Home",
      "contentBotId": "00000000-0000-0000-0000-000000000000",
      "scopes": ["personal"]
    },
    {
      "entityId": "moreTab",
      "name": "More",
      "contentBotId": "00000000-0000-0000-0000-000000000000",
      "scopes": ["personal"]
    }
  ],
  "connectors": [],
  "composeExtensions": [],
  "permissions": ["identity", "messageTeamMembers"],
  "validDomains": [
    "contoso.yourwebsite.com",
    "token.botframework.com"
  ]
}
```

## <a name="invoke-activities"></a>调用活动

自适应卡片选项卡和自动程序之间的通信通过活动 `invoke` 完成。 每个 `invoke` 活动都有一个对应的 **名称**。 使用每个活动的名称来区分每个请求。 `tab/fetch``tab/submit`和 是本节中介绍的活动。

> [!NOTE]
> 机器人需要向服务 URL 发送 [所有响应](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#base-uri&preserve-view=true)。 服务 URL 作为传入有效负载的一 `activity` 部分接收。

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a>提取自适应卡片以呈现到选项卡

`tab/fetch` 是机器人在用户打开自适应卡片选项卡时收到的第一个调用请求。当机器人收到请求时，它会发送一 **个选项卡继续** 响应或一个选项卡 **身份验证** 响应。
继续 **响应** 包括卡片的 **数组**，该数组按数组顺序垂直呈现到选项卡。

> [!NOTE]
> 有关身份验证响应 **详细信息，** 请参阅 [身份验证](#authentication)。

以下代码提供请求 `tab/fetch` 和响应的示例：

**`tab/fetch` request**

```json
// tab/fetch POST request: agents/{botId}/invoke
{
    "name": "tab/fetch",
    "value: {
        "tabContext": {
            "tabEntityId": "{tab_entity_id}"
        },
        "context": {
            "theme": "default"
            }
    },
    "conversation": {
        "id": "{generated_conversation_id}"
    },
    "imdisplayname": "{user_display_name}"
}
```

**`tab/fetch` 响应**

```json
// tab/fetch **continue** POST response:
{
    "tab": {
        "type": "continue",
        "value": {
            "cards": [
                {
                    "card": adaptiveCard1,
                },
                {
                    "card": adaptiveCard2,
                }
                {
                    "card": adaptiveCard3
                }  
            ]
        },
    },
    "responseType": "tab"
}
```

### <a name="handle-submits-from-adaptive-card"></a>处理自适应卡片中的提交

在选项卡中呈现自适应卡片后，它必须能够响应用户交互。 此响应由调用 `tab/submit` 请求处理。

当用户在"自适应卡片"选项卡上选择按钮时，会通过自适应卡片的功能将请求触发到具有相应数据的 `tab/submit` `Action.Submit` 机器人。 自适应卡片数据通过请求的 data 属性 `tab/submit` 提供。 您收到以下请求响应之一：

* 无正文的 HTTP `200` 状态代码响应。 空 200 响应会导致客户端不执行任何操作。
* 标准选项卡 `200` **继续响应** ，如提取自适应 [卡片 中介绍](#fetch-adaptive-card-to-render-to-a-tab)。 选项卡 **继续** 响应会触发客户端使用继续响应的卡片数组中提供的自适应卡片更新呈现的自适应 **卡片** 选项卡。

以下代码提供请求 `tab/submit` 和响应的示例：

**`tab/submit` request**

```json
// tab/submit POST request: agents/{botId}/invoke:
{
    "name": "tab/submit",
    "value": {
        "data": {
            "type": "tab/submit",
            //...<data properties>
            },
        "context": {
            "theme": "default"
            },
        "tabContext": {
            "tabEntityId": "{tab_entity_id}"
            },
        },
    "conversation": {
           "id": "{generated_conversation_id}" 
        },
    "imdisplayname": "{user_display_name}"
}
```

**`tab/submit` 响应**

```json
//tab/fetch **continue** POST response:
{
    "tab": {
        "type": "continue",
        "value": {
            "cards": [
              {
                "card": adaptiveCard1,
                },
              {
                "card": adaptiveCard2,
                } 
            ]
        },
    },
    "responseType": "tab"
}
```

## <a name="understand-task-module-workflow"></a>了解任务模块工作流

任务模块还使用自适应卡片 `task/fetch` 调用和 `task/submit` 请求和响应。 有关详细信息，请参阅使用[自动程序中Microsoft Teams模块](../../task-modules-and-cards/task-modules/task-modules-bots.md)。

随着自适应卡片选项卡的引入，机器人响应请求方式会 `task/submit` 发生变化。 如果你使用的是自适应卡片选项卡，机器人会使用标准选项卡继续响应来响应调用请求，并 `task/submit` 关闭任务模块。 通过呈现选项卡继续响应正文中提供的新卡片列表，可 **更新** "自适应卡片"选项卡。

### <a name="invoke-taskfetch"></a>Invoke `task/fetch`

以下代码提供请求 `task/fetch` 和响应的示例：

**`task/fetch` request**
```json
// task/fetch POST request: agents/{botId}/invoke
{
    "name": "task/fetch",
    "value": {
        "data": {
            "type": "task/fetch"
        },
        "context": {
            "theme": "default",
        },
        "tabContext": {
            "tabEntityId": "{tab_entity_id}"
        }
    },
    "imdisplayname": "{user_display_name}",
    "conversation": {
        "id": "{generated_conversation_id}"
    } 
}
```

**`task/fetch` 响应**

```json
// task/fetch POST response: agents/{botId}/invoke
{
    "task": {
        "value": {
            "title": "Ninja Cat",
            "height": "small",
            "width": "small",
            "card": {
                "contentType": "application/vnd.microsoft.card.adaptive",
                "content": adaptiveCard,
            }
        },
    "type": "continue"
    },
    "responseType": "task"
}
```

### <a name="invoke-tasksubmit"></a>Invoke `task/submit`

以下代码提供请求 `task/submit` 和响应的示例：

**`task/submit` request**

```json
// task/submit POST request: agent/{botId}/invoke:
{
    "name": "task/submit",
    "value": {
        "data": {serialized_data_object},
        "context": {
            "theme": "default"
        },
    "tabContext": {
        "tabEntityId": "{tab_entity_id}"
        },
    },
    "conversation": {
        "id": "{generated_conversation_id}"
    },
    "imdisplayname": "{user_display_name}",
}
```

**`task/submit` 选项卡响应类型**

```json
// tab/fetch **continue** POST response: 
{
    "task":{
        "value": {
            "tab": {
                "type": "continue",
                "value": {
                    "cards": [
                        {
                            "card": adaptiveCard1
                        },
                        {
                            "card": adaptiveCard2
                        }
                    ]
                }
            }
        },
        "type": "continue"
    },
    "responseType": "task"
}
```

## <a name="authentication"></a>身份验证

在本文的前面几节中，你已看到大部分开发范例都可以从任务模块请求和响应扩展到选项卡请求和响应中。 处理身份验证时，自适应卡片选项卡的工作流遵循邮件扩展的身份验证模式。 有关详细信息，请参阅 [添加身份验证](../../messaging-extensions/how-to/add-authentication.md)。

`tab/fetch` 请求可以有继续 **响应** 或 **身份验证** 响应。 当 `tab/fetch` 触发请求并收到选项卡 **身份验证** 响应时，登录页会向用户显示。

**通过调用获取身份验证 `tab/fetch` 代码**

1. 打开你的应用。 将显示登录页。

    > [!NOTE]
    > 应用徽标通过应用 `icon` 清单中定义的 属性提供。 在选项卡身份验证响应正文中返回的属性中定义徽标后显示 `title` 的标题。 

1. 选择“**登录**”。 您将重定向到身份验证响应正文的 属性中提供的 `value` 身份验证 URL。 
1. 将出现一个弹出窗口。 此弹出窗口使用身份验证 URL 托管网页。
1. 登录后，关闭窗口。 身份验证 **代码** 将发送到 Teams 客户端。
1. 然后Teams客户端重新向服务提出请求，其中包括托管网页提供的 `tab/fetch` 身份验证代码。

### <a name="tabfetch-authentication-data-flow"></a>`tab/fetch` 身份验证数据流

下图概述了身份验证数据流如何用于 `tab/fetch` 调用。

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="自适应卡片选项卡身份验证流的示例。" border="false":::

**`tab/fetch` 身份验证响应**

以下代码提供了身份验证 `tab/fetch` 响应的示例：

```json
// tab/auth POST response (openURL)
{
    "tab": {
        "type": "auth",
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

### <a name="example"></a>示例

以下代码显示了重新发送的请求示例：

```json
{
    "name": "tab/fetch",
    "type": "invoke",
    "timestamp": "2021-01-15T00:10:12.253Z",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "from": {
        "id": "{id}",
        "name": "John Smith",
        "aadObjectId": "00000000-0000-0000-0000-000000000000"
    },
    "conversation": {
        "tenantId": "{tenantId}",
        "id": "tab:{guid}"
    },
    "recipients": {
        "id": "28:00000000-0000-0000-0000-000000000000",
        "name": "ContosoApp"
    },
    "entities": [
        {
            "locale": "en-us",
            "country": "US",
            "platform": "Windows",
            "timezone": "America/Los_Angeles",
            "type": "clientInfo"
        }
    ],
    "channelData": {
        "tenant": { "id": "00000000-0000-0000-0000-000000000000" },
        "source": { "name": "message" }
    },
    "value": {
        "tabContext": { "tabEntityId": "homeTab" },
        "state": "0.43195668034524815"
    },
    "locale": "en-US",
    "localTimeZone": "America/Los_Angeles"
}
```

## <a name="see-also"></a>另请参阅

* [自适应卡片](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [Teams选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建频道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)
* [移动设备上的选项卡](~/tabs/design/tabs-mobile.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [选项卡链接展开和阶段视图](~/tabs/tabs-link-unfurling.md)