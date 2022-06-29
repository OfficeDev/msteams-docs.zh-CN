---
title: 生成自适应卡片选项卡
author: KirtiPereira
description: 在本模块中，了解如何通过代码示例使用自适应卡片生成选项卡，包括调用活动、了解任务模块工作流和身份验证。
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: c42ea356e3654453d20f59a8be33412b1e608939
ms.sourcegitcommit: c7fbb789b9654e9b8238700460b7ae5b2a58f216
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2022
ms.locfileid: "66485238"
---
# <a name="build-tabs-with-adaptive-cards"></a>具有自适应卡片的生成选项卡

> [!IMPORTANT]
>
> * 自适应卡片选项卡目前仅作为个人应用受支持。

使用传统方法开发选项卡时，可能会遇到以下问题:

* HTML 和 CSS 注意事项
* 加载时间缓慢
* iFrame 约束
* 服务器维护和成本

自适应卡片选项卡是在 Teams 中生成选项卡的新方法。 可以将自适应卡片呈现到选项卡，而不是在 IFrame 中嵌入 Web 内容。前端通过自适应卡片呈现，后端由机器人提供支持。 机器人负责接受请求，并使用呈现的自适应卡片进行适当的响应。

可以在桌面、Web 和移动设备上使用现成的用户界面(UI)构建基块来生成选项卡。 本文可帮助你了解需对应用清单执行的更改。 本文还确定了调用活动如何使用自适应卡片在选项卡中请求并发送信息，以及它对任务模块工作流的影响。

下图显示了如何在桌面和移动设备中使用自适应卡片生成选项卡:

:::image type="content" source="../../assets/images/adaptive-cards-rendered-in-tabs.png" alt-text="选项卡中呈现的自适应卡片示例。" border="false":::

## <a name="prerequisites"></a>先决条件

在开始使用自适应卡片生成选项卡之前，必须:

* 熟悉 Teams 中的 [机器人开发](../../bots/what-are-bots.md)、[自适应卡片](https://adaptivecards.io/) 和 [任务模块](../../task-modules-and-cards/task-modules/task-modules-bots.md)。
* 让机器人在 Teams 中运行以进行开发。

## <a name="changes-to-app-manifest"></a>对应用清单的更改

呈现选项卡的个人应用必须在其应用清单中包含 `staticTabs` 数组。 在 `staticTab` 定义中提供 `contentBotId` 属性时，会呈现自适应卡片选项卡。 静态选项卡定义必须包含 `contentBotId` 以指定自适应卡片选项卡，或包含 `contentUrl` 以指定典型的托管 Web 内容选项卡体验。

> [!NOTE]
> `contentBotId` 属性当前在清单版本 1.9 或更高版本中提供。

为 `contentBotId` 属性提供自适应卡片选项卡必须与之通信的 `botId`。 为自适应卡片选项卡配置的 `entityId` 在每个调用请求的 `tabContext` 参数z 发送，可用于区分由同一机器人提供支持的自适应卡片选项卡。 有关其他静态选项卡定义字段的详细信息，请参阅 [清单架构](../../resources/schema/manifest-schema.md#statictabs)。

以下是自适应卡片选项卡清单示例:

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

自适应卡片选项卡和机器人之间的通信通过 `invoke` 活动完成。 每个 `invoke` 活动都有相应的 **名称**。 使用每个活动的名称以区分每个请求。 `tab/fetch` 和 `tab/submit` 为本节涉及的活动。

> [!NOTE]
>
> * 机器人需要将所有响应发送到 [服务 URL](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#base-uri&preserve-view=true)。 服务 URL 作为传入 `activity` 有效负载的一部分接收。
> * 调用有效负载大小已增加到 80kb。

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a>提取自适应卡片以呈现到选项卡

`tab/fetch` 是用户打开自适应卡片选项卡时机器人收到的第一个调用请求。当机器人收到请求时，它会发送选项卡 **继续** 响应或选项卡 **身份验证** 响应。
**继续** 响应包含 **卡片** 数组，它按照数组的顺序垂直呈现到选项卡。

> [!NOTE]
> 有关 **身份验证** 响应的详细信息，请参阅 [身份验证](#authentication)。

以下代码提供了 `tab/fetch` 请求和响应示例:

**`tab/fetch` 请求**

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
                },
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

在选项卡中呈现自适应卡片后，卡片可以响应用户交互。 此响应由 `tab/submit` 调用请求处理。

当用户选择自适应卡片选项卡上的按钮时，会通过自适应卡片的 `Action.Submit` 函数将 `tab/submit` 请求触发到机器人，并随附相应数据。 自适应卡片数据通过 `tab/submit` 请求的数据属性提供。 你收到以下其中一个对请求的响应:

* 无正文的 HTTP 状态代码 `200` 响应。 空的 200 响应导致客户端不执行任何操作。
* 标准 `200` 选项卡 **继续** 响应，如 [提取自适应卡片](#fetch-adaptive-card-to-render-to-a-tab) 中所述。 选项卡 **继续** 响应会触发客户端使用 **继续** 响应卡片数组中提供的自适应卡片来更新呈现的自适应卡片选项卡。

以下代码提供了 `tab/submit` 请求和响应示例:

**`tab/submit` 请求**

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

任务模块还使用自适应卡片来调用 `task/fetch` 和 `task/submit` 请求及响应。 有关详细信息，请参阅 [在 Microsoft Teams 机器人中使用任务模块](../../task-modules-and-cards/task-modules/task-modules-bots.md)。

随着自适应卡片选项卡的引入，机器人响应 `task/submit` 请求的方式发生了改变。 如果使用的是自适应卡片选项卡，则机器人会使用标准选项卡 **继续** 响应来响应 `task/submit` 调用请求，并关闭任务模块。 呈现选项卡 **继续** 响应正文中提供的新卡片列表，从而更新自适应卡片选项卡。

### <a name="invoke-taskfetch"></a>调用 `task/fetch`

以下代码提供了 `task/fetch` 请求和响应示例:

**`task/fetch` 请求**

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

### <a name="invoke-tasksubmit"></a>调用 `task/submit`

以下代码提供了 `task/submit` 请求和响应示例:

**`task/submit` 请求**

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

在前面的节中，你已了解大多数开发范例可以从任务模块请求和响应扩展到选项卡请求和响应。 在处理身份验证时，自适应卡片选项卡的工作流遵循消息扩展的身份验证模式。 有关详细信息，请参阅 [添加身份验证](../../messaging-extensions/how-to/add-authentication.md)。

`tab/fetch` 请求可以具有 **继续** 或 **身份验证** 响应。 触发 `tab/fetch` 请求并接收选项卡 **身份验证** 响应时，会向用户显示登录页面。

**要通过 `tab/fetch` 调用** 获取身份验证代码

1. 打开应用。 会显示登录页面。

    > [!NOTE]
    > 应用徽标通过应用清单中定义的 `icon` 属性提供。 在选项卡 **身份验证** 响应正文中返回的 `title` 属性中定义徽标之后显示的标题。

1. 选择“**登录**”。 你已重定向到 **身份验证** 响应正文的 `value` 属性中提供的身份验证 URL。
1. 将出现一个弹出窗口。 此弹出窗口使用身份验证 URL 托管网页。
1. 登录后，关闭窗口。 **身份验证代码** 会发送到 Teams 客户端。
1. 然后，Teams 客户端会向服务重新发出 `tab/fetch` 请求，其中包括托管网页提供的身份验证代码。

### <a name="tabfetch-authentication-data-flow"></a>`tab/fetch` 身份验证数据流

下图概述了身份验证数据流如何适用于 `tab/fetch` 调用。

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow1.png" alt-text="自适应卡片选项卡身份验证流示例。" border="false" lightbox="../../assets/images/tabs/adaptive-cards-tab-auth-flow2.png":::

**`tab/fetch` 身份验证响应**

以下代码提供了 `tab/fetch` 身份验证响应示例:

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

以下代码显示了重新发出的请求示例:

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

## <a name="code-sample"></a>代码示例

|**示例名称** | **说明** |**.NET** | **Node.js** |
|----------------|-----------------|--------------|--------------|
| 在 Teams 选项卡中显示自适应卡片 | Microsoft Teams 选项卡示例代码，演示如何在 Teams 中显示自适应卡片。 |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/csharp)| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/nodejs) |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [选项卡链接展开和演示区域视图](~/tabs/tabs-link-unfurling.md)

## <a name="see-also"></a>另请参阅

* [自适应卡](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [Teams 选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建频道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)
* [移动设备上的选项卡](~/tabs/design/tabs-mobile.md)
* [表单完成反馈](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
