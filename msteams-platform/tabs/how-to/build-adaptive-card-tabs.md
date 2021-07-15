---
title: 生成自适应卡片选项卡
author: KirtiPereira
description: 使用自适应卡片生成选项卡
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: aaa6ae00e4a70ea27c27638ed9475bc7edec25da
ms.sourcegitcommit: e327c9766dfa05abb468cdc71319e3cba7c6c79f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/14/2021
ms.locfileid: "53428714"
---
# <a name="build-tabs-with-adaptive-cards"></a><span data-ttu-id="ee7a2-103">具有自适应卡片的生成选项卡</span><span class="sxs-lookup"><span data-stu-id="ee7a2-103">Build tabs with Adaptive Cards</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="ee7a2-104">此功能 [在公用开发者预览版](~/resources/dev-preview/developer-preview-intro.md) 桌面和移动版中受支持。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-104">This feature is in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) and is supported in desktop and mobile.</span></span> <span data-ttu-id="ee7a2-105">即将推出 Web 浏览器中的支持。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-105">Support in the web browser is coming soon.</span></span>
> * <span data-ttu-id="ee7a2-106">带自适应卡片的选项卡当前仅作为个人应用受支持。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-106">Tabs with Adaptive Cards are currently only supported as personal apps.</span></span>

<span data-ttu-id="ee7a2-107">使用传统方法开发选项卡时，您可能会遇到这些问题，如 HTML 和 CSS 注意事项、加载时间较慢、iFrame 约束以及服务器维护和成本。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-107">When developing a tab using the traditional method, you might run into these issues, such as HTML and CSS considerations, slow load times, iFrame constraints, and server maintenance and costs.</span></span> <span data-ttu-id="ee7a2-108">自适应卡片选项卡是一种在卡片中生成选项卡的Teams。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-108">Adaptive Card tabs is a new way to build tabs in Teams.</span></span> <span data-ttu-id="ee7a2-109">你可以将自适应卡片呈现到选项卡，而不是在 IFrame 中嵌入 Web 内容。前端使用自适应卡片呈现，而后端由机器人提供电源。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-109">Instead of embedding web content in an IFrame, you can render Adaptive Cards to a tab. While the front-end is rendered with Adaptive Cards, the backend is powered by a bot.</span></span> <span data-ttu-id="ee7a2-110">机器人负责接受请求，以及使用呈现的自适应卡片进行相应响应。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-110">The bot is responsible for accepting requests and responding appropriately with the Adaptive Card that is rendered.</span></span>

<span data-ttu-id="ee7a2-111">可以使用现成的用户界面 (和 UI) 构建基块（在桌面、Web 和移动设备上外观) 构建基块）生成选项卡。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-111">You can build your tabs with ready-made user interface (UI) building blocks that look and feel native on desktop, web, and mobile.</span></span> <span data-ttu-id="ee7a2-112">本文可帮助你了解对应用清单所需的更改、调用活动如何请求和发送带自适应卡片的选项卡信息，以及对任务模块工作流的影响。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-112">This article helps you understand the changes required to be made to the app manifest, how the invoke activity requests and sends information in tab with Adaptive Cards, and the impact on the task module workflow.</span></span>

<span data-ttu-id="ee7a2-113">下图描述了使用桌面和移动版自适应卡片生成选项卡：</span><span class="sxs-lookup"><span data-stu-id="ee7a2-113">The following image depicts build tabs with Adaptive Cards in desktop and mobile:</span></span>

:::image type="content" source="../../assets/images/tabs/adaptive-cards-rendered-in-tabs.jpg" alt-text="选项卡中呈现的自适应卡片示例。" border="false":::

## <a name="prerequisites"></a><span data-ttu-id="ee7a2-115">必备条件</span><span class="sxs-lookup"><span data-stu-id="ee7a2-115">Prerequisites</span></span>

<span data-ttu-id="ee7a2-116">在开始使用自适应卡片生成选项卡之前，你必须：</span><span class="sxs-lookup"><span data-stu-id="ee7a2-116">Before you start using Adaptive Cards to build tabs, you must:</span></span>

* <span data-ttu-id="ee7a2-117">熟悉自动程序[开发、](../../bots/what-are-bots.md)[自适应卡片](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)和 Teams[](../../task-modules-and-cards/task-modules/task-modules-bots.md)中的任务模块。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-117">Be familiar with, [bot development](../../bots/what-are-bots.md), [Adaptive Cards](../../task-modules-and-cards/what-are-cards.md#adaptive-cards), and [task modules](../../task-modules-and-cards/task-modules/task-modules-bots.md) in Teams.</span></span>
* <span data-ttu-id="ee7a2-118">使机器人在 Teams中运行，以用于你的开发。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-118">Have a bot running in Teams for your development.</span></span>
* <span data-ttu-id="ee7a2-119">在公共[开发者预览版。](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="ee7a2-119">Be in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

## <a name="changes-to-app-manifest"></a><span data-ttu-id="ee7a2-120">对应用清单的更改</span><span class="sxs-lookup"><span data-stu-id="ee7a2-120">Changes to app manifest</span></span>

<span data-ttu-id="ee7a2-121">呈现选项卡的个人应用必须在其应用 `staticTabs` 清单中包括数组。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-121">Personal apps that render tabs must include a `staticTabs` array in their app manifest.</span></span> <span data-ttu-id="ee7a2-122">在定义中提供 属性时 `contentBotId` ，将呈现自适应卡片 `staticTab` 选项卡。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-122">Adaptive Card tabs are rendered when the `contentBotId` property is provided in the `staticTab` definition.</span></span> <span data-ttu-id="ee7a2-123">静态选项卡定义必须包含 ，指定自适应 `contentBotId` 卡片选项卡或 `contentUrl` ，指定典型的托管 Web 内容选项卡体验。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-123">Static tab definitions must contain either a `contentBotId`, specifying an Adaptive Card tab or a `contentUrl`, specifying a typical hosted web content tab experience.</span></span>

> [!NOTE]
> <span data-ttu-id="ee7a2-124">`contentBotId`属性当前在清单版本 1.9 或更高版本中可用。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-124">The `contentBotId` property is currently available in manifest version 1.9 or later.</span></span>

<span data-ttu-id="ee7a2-125">为 `contentBotId` 属性提供 `botId` "自适应卡片"选项卡必须通信的 。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-125">Provide the `contentBotId` property with the `botId` that the Adaptive Card tab must communicate with.</span></span> <span data-ttu-id="ee7a2-126">为"自适应卡片"选项卡配置的在每个调用请求的参数中发送，并可用于区分由同一自动程序提供电源的自适应卡片 `entityId` `tabContext` 选项卡。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-126">The `entityId` configured for the Adaptive Card tab is sent in the `tabContext` parameter of each invoke request, and can be used to differentiate Adaptive Card Tabs that are powered by the same bot.</span></span> <span data-ttu-id="ee7a2-127">有关其他静态选项卡定义字段的信息，请参阅 [清单架构](../../resources/schema/manifest-schema.md#statictabs)。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-127">For more information about other static tab definition fields, see [manifest schema](../../resources/schema/manifest-schema.md#statictabs).</span></span>

<span data-ttu-id="ee7a2-128">下面是自适应卡片选项卡清单示例：</span><span class="sxs-lookup"><span data-stu-id="ee7a2-128">Following is a sample Adaptive Card tab manifest:</span></span>

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

## <a name="invoke-activities"></a><span data-ttu-id="ee7a2-129">调用活动</span><span class="sxs-lookup"><span data-stu-id="ee7a2-129">Invoke activities</span></span>

<span data-ttu-id="ee7a2-130">自适应卡片选项卡和自动程序之间的通信通过活动 `invoke` 完成。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-130">Communication between your Adaptive Card tab and your bot is done through `invoke` activities.</span></span> <span data-ttu-id="ee7a2-131">每个 `invoke` 活动都有一个对应的 **名称**。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-131">Each `invoke` activity has a corresponding **name**.</span></span> <span data-ttu-id="ee7a2-132">使用每个活动的名称来区分每个请求。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-132">Use the name of each activity to differentiate each request.</span></span> <span data-ttu-id="ee7a2-133">`tab/fetch``tab/submit`和 是本节中介绍的活动。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-133">`tab/fetch` and `tab/submit` are the activities covered in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="ee7a2-134">机器人需要向服务 URL 发送 [所有响应](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#base-uri&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-134">Bots need to send all the responses to [service URL](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#base-uri&preserve-view=true).</span></span> <span data-ttu-id="ee7a2-135">服务 URL 作为传入有效负载的一 `activity` 部分接收。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-135">Service URL is received as part of incoming `activity` payload.</span></span>

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a><span data-ttu-id="ee7a2-136">提取自适应卡片以呈现到选项卡</span><span class="sxs-lookup"><span data-stu-id="ee7a2-136">Fetch Adaptive Card to render to a tab</span></span>

<span data-ttu-id="ee7a2-137">`tab/fetch` 是机器人在用户打开自适应卡片选项卡时收到的第一个调用请求。当机器人收到请求时，它会发送一 **个选项卡继续** 响应或一个选项卡 **身份验证** 响应。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-137">`tab/fetch` is the first invoke request that your bot receives when a user opens an Adaptive Card tab. When your bot receives the request, it either sends a tab **continue** response or a tab **auth** response.</span></span>
<span data-ttu-id="ee7a2-138">继续 **响应** 包括卡片的 **数组**，该数组按数组顺序垂直呈现到选项卡。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-138">The **continue** response includes an array for **cards**, which is rendered vertically to the tab in the order of the array.</span></span>

> [!NOTE]
> <span data-ttu-id="ee7a2-139">有关身份验证响应 **详细信息，** 请参阅 [身份验证](#authentication)。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-139">For more information on **auth** response, see [authentication](#authentication).</span></span>

<span data-ttu-id="ee7a2-140">以下代码提供请求 `tab/fetch` 和响应的示例：</span><span class="sxs-lookup"><span data-stu-id="ee7a2-140">The following code provides examples of `tab/fetch` request and response:</span></span>

<span data-ttu-id="ee7a2-141">**`tab/fetch` request**</span><span class="sxs-lookup"><span data-stu-id="ee7a2-141">**`tab/fetch` request**</span></span>

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

<span data-ttu-id="ee7a2-142">**`tab/fetch` 响应**</span><span class="sxs-lookup"><span data-stu-id="ee7a2-142">**`tab/fetch` response**</span></span>

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

### <a name="handle-submits-from-adaptive-card"></a><span data-ttu-id="ee7a2-143">处理自适应卡片中的提交</span><span class="sxs-lookup"><span data-stu-id="ee7a2-143">Handle submits from Adaptive Card</span></span>

<span data-ttu-id="ee7a2-144">在选项卡中呈现自适应卡片后，它必须能够响应用户交互。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-144">After an Adaptive Card is rendered in the tab, it must be able to respond to user interactions.</span></span> <span data-ttu-id="ee7a2-145">此响应由调用 `tab/submit` 请求处理。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-145">This response is handled by the `tab/submit` invoke request.</span></span>

<span data-ttu-id="ee7a2-146">当用户在"自适应卡片"选项卡上选择按钮时，会通过自适应卡片的功能将请求触发到具有相应数据的 `tab/submit` `Action.Submit` 机器人。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-146">When a user selects a button on the Adaptive Card tab, the `tab/submit` request is triggered to your bot with the corresponding data through the `Action.Submit` function of Adaptive Card.</span></span> <span data-ttu-id="ee7a2-147">自适应卡片数据通过请求的 data 属性 `tab/submit` 提供。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-147">The Adaptive Card data is available through the data property of the `tab/submit` request.</span></span> <span data-ttu-id="ee7a2-148">您收到以下请求响应之一：</span><span class="sxs-lookup"><span data-stu-id="ee7a2-148">You receive either of the following responses to your request:</span></span>

* <span data-ttu-id="ee7a2-149">无正文的 HTTP `200` 状态代码响应。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-149">An HTTP status code `200` response with no body.</span></span> <span data-ttu-id="ee7a2-150">空 200 响应会导致客户端不执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-150">An empty 200 response results in no action taken by the client.</span></span>
* <span data-ttu-id="ee7a2-151">标准选项卡 `200` **继续响应** ，如提取自适应 [卡片 中介绍](#fetch-adaptive-card-to-render-to-a-tab)。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-151">The standard `200` tab **continue** response, as explained in [fetch Adaptive Card](#fetch-adaptive-card-to-render-to-a-tab).</span></span> <span data-ttu-id="ee7a2-152">选项卡 **继续** 响应会触发客户端使用继续响应的卡片数组中提供的自适应卡片更新呈现的自适应 **卡片** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-152">A tab **continue** response triggers the client to update the rendered Adaptive Card tab with the Adaptive Cards provided in the cards array of the **continue** response.</span></span>

<span data-ttu-id="ee7a2-153">以下代码提供请求 `tab/submit` 和响应的示例：</span><span class="sxs-lookup"><span data-stu-id="ee7a2-153">The following code provides examples of `tab/submit` request and response:</span></span>

<span data-ttu-id="ee7a2-154">**`tab/submit` request**</span><span class="sxs-lookup"><span data-stu-id="ee7a2-154">**`tab/submit` request**</span></span>

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

<span data-ttu-id="ee7a2-155">**`tab/submit` 响应**</span><span class="sxs-lookup"><span data-stu-id="ee7a2-155">**`tab/submit` response**</span></span>

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

## <a name="understand-task-module-workflow"></a><span data-ttu-id="ee7a2-156">了解任务模块工作流</span><span class="sxs-lookup"><span data-stu-id="ee7a2-156">Understand task module workflow</span></span>

<span data-ttu-id="ee7a2-157">任务模块还使用自适应卡片 `task/fetch` 调用和 `task/submit` 请求和响应。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-157">The task module also uses Adaptive Card to invoke `task/fetch` and `task/submit` requests and responses.</span></span> <span data-ttu-id="ee7a2-158">有关详细信息，请参阅使用[自动程序中Microsoft Teams模块](../../task-modules-and-cards/task-modules/task-modules-bots.md)。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-158">For more information, see [using Task Modules in Microsoft Teams bots](../../task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="ee7a2-159">随着自适应卡片选项卡的引入，机器人响应请求方式会 `task/submit` 发生变化。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-159">With the introduction of Adaptive Card tab, there is a change in how the bot responds to a `task/submit` request.</span></span> <span data-ttu-id="ee7a2-160">如果你使用的是自适应卡片选项卡，机器人会使用标准选项卡继续响应来响应调用请求，并 `task/submit` 关闭任务模块。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-160">If you are using an Adaptive Card tab, the bot responds to the `task/submit` invoke request with the standard tab **continue** response, and closes the task module.</span></span> <span data-ttu-id="ee7a2-161">通过呈现选项卡继续响应正文中提供的新卡片列表，可 **更新** "自适应卡片"选项卡。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-161">The Adaptive Card tab is updated by rendering the new list of cards provided in the tab **continue** response body.</span></span>

### <a name="invoke-taskfetch"></a><span data-ttu-id="ee7a2-162">Invoke `task/fetch`</span><span class="sxs-lookup"><span data-stu-id="ee7a2-162">Invoke `task/fetch`</span></span>

<span data-ttu-id="ee7a2-163">以下代码提供请求 `task/fetch` 和响应的示例：</span><span class="sxs-lookup"><span data-stu-id="ee7a2-163">The following code provides examples of `task/fetch` request and response:</span></span>

<span data-ttu-id="ee7a2-164">**`task/fetch` request**</span><span class="sxs-lookup"><span data-stu-id="ee7a2-164">**`task/fetch` request**</span></span>
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

<span data-ttu-id="ee7a2-165">**`task/fetch` 响应**</span><span class="sxs-lookup"><span data-stu-id="ee7a2-165">**`task/fetch` response**</span></span>

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

### <a name="invoke-tasksubmit"></a><span data-ttu-id="ee7a2-166">Invoke `task/submit`</span><span class="sxs-lookup"><span data-stu-id="ee7a2-166">Invoke `task/submit`</span></span>

<span data-ttu-id="ee7a2-167">以下代码提供请求 `task/submit` 和响应的示例：</span><span class="sxs-lookup"><span data-stu-id="ee7a2-167">The following code provides examples of `task/submit` request and response:</span></span>

<span data-ttu-id="ee7a2-168">**`task/submit` request**</span><span class="sxs-lookup"><span data-stu-id="ee7a2-168">**`task/submit` request**</span></span>

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

<span data-ttu-id="ee7a2-169">**`task/submit` 选项卡响应类型**</span><span class="sxs-lookup"><span data-stu-id="ee7a2-169">**`task/submit` tab response type**</span></span>

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

## <a name="authentication"></a><span data-ttu-id="ee7a2-170">身份验证</span><span class="sxs-lookup"><span data-stu-id="ee7a2-170">Authentication</span></span>

<span data-ttu-id="ee7a2-171">在本文的前面几节中，你已看到大部分开发范例都可以从任务模块请求和响应扩展到选项卡请求和响应中。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-171">In the previous sections of this article, you have seen that most of the development paradigms can be extended from the task module requests and responses into tab requests and responses.</span></span> <span data-ttu-id="ee7a2-172">处理身份验证时，自适应卡片选项卡的工作流遵循邮件扩展的身份验证模式。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-172">When it comes to handling authentication, the workflow for Adaptive Card tab follows the authentication pattern for messaging extensions.</span></span> <span data-ttu-id="ee7a2-173">有关详细信息，请参阅 [添加身份验证](../../messaging-extensions/how-to/add-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-173">For more information, see [add authentication](../../messaging-extensions/how-to/add-authentication.md).</span></span>

<span data-ttu-id="ee7a2-174">`tab/fetch` 请求可以有继续 **响应** 或 **身份验证** 响应。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-174">`tab/fetch` requests can have either a **continue** or an **auth** response.</span></span> <span data-ttu-id="ee7a2-175">当 `tab/fetch` 触发请求并收到选项卡 **身份验证** 响应时，登录页会向用户显示。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-175">When a `tab/fetch` request is triggered and receives a tab **auth** response, the sign-in page is shown to the user.</span></span>

<span data-ttu-id="ee7a2-176">**通过调用获取身份验证 `tab/fetch` 代码**</span><span class="sxs-lookup"><span data-stu-id="ee7a2-176">**To get an authentication code through `tab/fetch` invoke**</span></span>

1. <span data-ttu-id="ee7a2-177">打开你的应用。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-177">Open your app.</span></span> <span data-ttu-id="ee7a2-178">将显示登录页。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-178">The sign in page appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ee7a2-179">应用徽标通过应用 `icon` 清单中定义的 属性提供。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-179">The app logo is provided through the `icon` property defined in the app manifest.</span></span> <span data-ttu-id="ee7a2-180">在选项卡身份验证响应正文中返回的属性中定义徽标后显示 `title` 的标题。 </span><span class="sxs-lookup"><span data-stu-id="ee7a2-180">The title appearing after the logo is defined in the `title` property returned in the tab **auth** response body.</span></span>

1. <span data-ttu-id="ee7a2-181">选择“**登录**”。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-181">Select **Sign in**.</span></span> <span data-ttu-id="ee7a2-182">您将重定向到身份验证响应正文的 属性中提供的 `value` 身份验证 URL。 </span><span class="sxs-lookup"><span data-stu-id="ee7a2-182">You are redirected to the authentication URL provided in the `value` property of the **auth** response body.</span></span>
1. <span data-ttu-id="ee7a2-183">将出现一个弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-183">A pop-up window appears.</span></span> <span data-ttu-id="ee7a2-184">此弹出窗口使用身份验证 URL 托管网页。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-184">This pop-up window hosts your web page using the authentication URL.</span></span>
1. <span data-ttu-id="ee7a2-185">登录后，关闭窗口。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-185">After you sign in, close the window.</span></span> <span data-ttu-id="ee7a2-186">身份验证 **代码** 将发送到 Teams 客户端。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-186">An **authentication code** is sent to the Teams client.</span></span>
1. <span data-ttu-id="ee7a2-187">然后Teams客户端重新向服务提出请求，其中包括托管网页提供的 `tab/fetch` 身份验证代码。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-187">The Teams client then reissues the `tab/fetch` request to your service, which includes the authentication code provided by your hosted web page.</span></span>

### <a name="tabfetch-authentication-data-flow"></a><span data-ttu-id="ee7a2-188">`tab/fetch` 身份验证数据流</span><span class="sxs-lookup"><span data-stu-id="ee7a2-188">`tab/fetch` authentication data flow</span></span>

<span data-ttu-id="ee7a2-189">下图概述了身份验证数据流如何用于 `tab/fetch` 调用。</span><span class="sxs-lookup"><span data-stu-id="ee7a2-189">The following image provides an overview of how the authentication data flow works for a `tab/fetch` invoke.</span></span>

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="自适应卡片选项卡身份验证流的示例。" border="false":::

<span data-ttu-id="ee7a2-191">**`tab/fetch` 身份验证响应**</span><span class="sxs-lookup"><span data-stu-id="ee7a2-191">**`tab/fetch` auth response**</span></span>

<span data-ttu-id="ee7a2-192">以下代码提供了身份验证 `tab/fetch` 响应的示例：</span><span class="sxs-lookup"><span data-stu-id="ee7a2-192">The following code provides an example of `tab/fetch` auth response:</span></span>

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

### <a name="example"></a><span data-ttu-id="ee7a2-193">示例</span><span class="sxs-lookup"><span data-stu-id="ee7a2-193">Example</span></span>

<span data-ttu-id="ee7a2-194">以下代码显示了重新发送的请求示例：</span><span class="sxs-lookup"><span data-stu-id="ee7a2-194">The following code shows a reissued request example:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="ee7a2-195">另请参阅</span><span class="sxs-lookup"><span data-stu-id="ee7a2-195">See also</span></span>

* [<span data-ttu-id="ee7a2-196">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="ee7a2-196">Adaptive Card</span></span>](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [<span data-ttu-id="ee7a2-197">Teams选项卡</span><span class="sxs-lookup"><span data-stu-id="ee7a2-197">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="ee7a2-198">创建个人选项卡</span><span class="sxs-lookup"><span data-stu-id="ee7a2-198">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="ee7a2-199">创建频道或组选项卡</span><span class="sxs-lookup"><span data-stu-id="ee7a2-199">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="ee7a2-200">移动设备上的选项卡</span><span class="sxs-lookup"><span data-stu-id="ee7a2-200">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)

## <a name="next-step"></a><span data-ttu-id="ee7a2-201">后续步骤</span><span class="sxs-lookup"><span data-stu-id="ee7a2-201">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ee7a2-202">选项卡链接展开和阶段视图</span><span class="sxs-lookup"><span data-stu-id="ee7a2-202">Tabs link unfurling and Stage View</span></span>](~/tabs/tabs-link-unfurling.md)
