---
title: 生成自适应卡片选项卡
author: KirtiPereira
description: 使用自适应卡片生成选项卡
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: d65fc537b5282c050d891a6a73ff114c630e2c1c
ms.sourcegitcommit: c59d90ae03eae32996db49f162855965b55c52fe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2021
ms.locfileid: "52668846"
---
# <a name="build-tabs-with-adaptive-cards"></a><span data-ttu-id="8bee4-103">具有自适应卡片的生成选项卡</span><span class="sxs-lookup"><span data-stu-id="8bee4-103">Build tabs with Adaptive Cards</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="8bee4-104">此功能 [在公用开发者预览版](~/resources/dev-preview/developer-preview-intro.md) 桌面和移动版中受支持。</span><span class="sxs-lookup"><span data-stu-id="8bee4-104">This feature is in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) and is supported in desktop and mobile.</span></span> <span data-ttu-id="8bee4-105">即将推出 Web 浏览器中的支持。</span><span class="sxs-lookup"><span data-stu-id="8bee4-105">Support in the web browser is coming soon.</span></span>
> * <span data-ttu-id="8bee4-106">带自适应卡片的选项卡当前仅作为个人应用受支持。</span><span class="sxs-lookup"><span data-stu-id="8bee4-106">Tabs with Adaptive Cards are currently only supported as personal apps.</span></span>

<span data-ttu-id="8bee4-107">使用自适应卡片轻松生成选项卡。</span><span class="sxs-lookup"><span data-stu-id="8bee4-107">Use Adaptive Cards to build tabs with ease.</span></span> <span data-ttu-id="8bee4-108">可以使用现成的 UI Lego 块生成选项卡，这些块在桌面、Web 和移动设备上具有本机外观。</span><span class="sxs-lookup"><span data-stu-id="8bee4-108">You can build your tabs with ready-made UI Lego-blocks that look and feel native on desktop, web, and mobile.</span></span> <span data-ttu-id="8bee4-109">使用自适应卡片生成选项卡可集中Teams自动程序后端和自适应卡片前端的所有应用功能，因此无需为机器人和选项卡提供不同的后端。</span><span class="sxs-lookup"><span data-stu-id="8bee4-109">Building tabs with Adaptive Cards centralizes all Teams app capabilities around a bot backend and Adaptive Card frontend, thus, eliminating the need for a different backend for your bot and tabs.</span></span> <span data-ttu-id="8bee4-110">这大大减少了应用程序服务器和Teams成本。</span><span class="sxs-lookup"><span data-stu-id="8bee4-110">This greatly reduces server and maintenance costs of your Teams app.</span></span> <span data-ttu-id="8bee4-111">本文可帮助你了解对应用清单所需的更改、调用活动如何请求和发送带自适应卡片的选项卡信息，以及对任务模块工作流的影响。</span><span class="sxs-lookup"><span data-stu-id="8bee4-111">This article helps you understand the changes required to be made to the app manifest, how the invoke activity requests and sends information in tab with Adaptive Cards, and the impact on the task module workflow.</span></span> 

下图描述了在桌面和移动设备上使用自适应卡片生成选项卡： :::image type="content" source="../../assets/images/tabs/adaptive-cards-rendered-in-tabs.jpg" alt-text="选项卡中呈现的自适应卡片示例。" border="false":::

## <a name="prerequisites"></a><span data-ttu-id="8bee4-113">先决条件</span><span class="sxs-lookup"><span data-stu-id="8bee4-113">Prerequisites</span></span>

<span data-ttu-id="8bee4-114">在开始使用自适应卡片生成选项卡之前，你必须：</span><span class="sxs-lookup"><span data-stu-id="8bee4-114">Before you start using Adaptive Cards to build tabs, you must:</span></span>

* <span data-ttu-id="8bee4-115">熟悉自动程序[开发、](../../bots/what-are-bots.md)[自适应卡片](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)和任务[模块](../../task-modules-and-cards/task-modules/task-modules-bots.md)Teams。</span><span class="sxs-lookup"><span data-stu-id="8bee4-115">Be familiar with, [bot development](../../bots/what-are-bots.md), [Adaptive Cards](../../task-modules-and-cards/what-are-cards.md#adaptive-cards), and [Task Modules](../../task-modules-and-cards/task-modules/task-modules-bots.md) in Teams.</span></span>
* <span data-ttu-id="8bee4-116">使机器人在 Teams中运行，以用于你的开发。</span><span class="sxs-lookup"><span data-stu-id="8bee4-116">Have a bot running in Teams for your development.</span></span>
* <span data-ttu-id="8bee4-117">在公共[开发者预览版。](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="8bee4-117">Be in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

## <a name="changes-to-app-manifest"></a><span data-ttu-id="8bee4-118">对应用清单的更改</span><span class="sxs-lookup"><span data-stu-id="8bee4-118">Changes to app manifest</span></span>

<span data-ttu-id="8bee4-119">呈现选项卡的个人应用必须在其应用 `staticTabs` 清单中包括数组。</span><span class="sxs-lookup"><span data-stu-id="8bee4-119">Personal apps that render tabs must include a `staticTabs` array in their app manifest.</span></span> <span data-ttu-id="8bee4-120">在定义中提供属性时 `contentBotId` ，将呈现自适应卡片 `staticTab` 选项卡。</span><span class="sxs-lookup"><span data-stu-id="8bee4-120">Adaptive Card Tab are rendered when the `contentBotId` property is provided in the `staticTab` definition.</span></span> <span data-ttu-id="8bee4-121">静态选项卡定义必须包含 ，指定自适应卡片 `contentBotId` 选项卡或 `contentUrl` ，指定典型的托管 Web 内容选项卡体验。</span><span class="sxs-lookup"><span data-stu-id="8bee4-121">Static tab definitions must contain either a `contentBotId`, specifying an Adaptive Card Tab or a `contentUrl`, specifying a typical hosted web content tab experience.</span></span>

> [!NOTE]
> <span data-ttu-id="8bee4-122">属性 `contentBotId` 当前提供清单版本 1.9 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="8bee4-122">The `contentBotId` property is currently available manifest version 1.9 or later.</span></span> 

<span data-ttu-id="8bee4-123">为 `contentBotId` 属性提供 `botId` 自适应卡片选项卡必须通信的 。</span><span class="sxs-lookup"><span data-stu-id="8bee4-123">Provide the `contentBotId` property with the `botId` that the Adaptive Card Tab must communicate with.</span></span> <span data-ttu-id="8bee4-124">为自适应卡片选项卡配置的在每个调用请求的参数中发送，可用于区分由同一自动程序支持的不同自适应卡片 `entityId` `tabContext` 选项卡。</span><span class="sxs-lookup"><span data-stu-id="8bee4-124">The `entityId` configured for the Adaptive Card Tab is sent in the `tabContext` parameter of each invoke request, and can be used to differentiate different Adaptive Card Tabs that are powered by the same bot.</span></span> <span data-ttu-id="8bee4-125">有关其他静态选项卡定义字段的信息，请参阅 [清单架构](../../resources/schema/manifest-schema.md#statictabs)。</span><span class="sxs-lookup"><span data-stu-id="8bee4-125">For more information about other static tab definition fields, see [manifest schema](../../resources/schema/manifest-schema.md#statictabs).</span></span>

<span data-ttu-id="8bee4-126">下面是自适应卡片选项卡清单示例：</span><span class="sxs-lookup"><span data-stu-id="8bee4-126">Following is a sample Adaptive Card Tab manifest:</span></span>

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

## <a name="invoke-activities"></a><span data-ttu-id="8bee4-127">调用活动</span><span class="sxs-lookup"><span data-stu-id="8bee4-127">Invoke activities</span></span>

<span data-ttu-id="8bee4-128">自适应卡片选项卡和自动程序之间的通信通过活动 `invoke` 完成。</span><span class="sxs-lookup"><span data-stu-id="8bee4-128">Communication between your Adaptive Card Tab and your bot is done through `invoke` activities.</span></span> <span data-ttu-id="8bee4-129">每个 `invoke` 活动都有一个对应的 *名称*。</span><span class="sxs-lookup"><span data-stu-id="8bee4-129">Each `invoke` activity has a corresponding *name*.</span></span> <span data-ttu-id="8bee4-130">使用每个活动的名称来区分每个请求。</span><span class="sxs-lookup"><span data-stu-id="8bee4-130">Use the name of each activity to differentiate each request.</span></span> <span data-ttu-id="8bee4-131">`tab/fetch``tab/submit`和 是本节中介绍的活动。</span><span class="sxs-lookup"><span data-stu-id="8bee4-131">`tab/fetch` and `tab/submit` are the activities covered in this section.</span></span>

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a><span data-ttu-id="8bee4-132">提取自适应卡片以呈现到选项卡</span><span class="sxs-lookup"><span data-stu-id="8bee4-132">Fetch Adaptive Card to render to a tab</span></span>

<span data-ttu-id="8bee4-133">`tab/fetch` 是机器人在用户打开自适应卡片选项卡时收到的第一个调用请求。</span><span class="sxs-lookup"><span data-stu-id="8bee4-133">`tab/fetch` is the first invoke request that your bot receives when a user opens an Adaptive Card Tabs.</span></span> <span data-ttu-id="8bee4-134">When your bot receives the request， it will send a tab **continue** response or a tab **auth** response.</span><span class="sxs-lookup"><span data-stu-id="8bee4-134">When your bot receives the request, it will either send a tab **continue** response or a tab **auth** response.</span></span>
<span data-ttu-id="8bee4-135">继续 **响应** 包括卡片的 **数组**，该数组按数组顺序垂直呈现到选项卡。</span><span class="sxs-lookup"><span data-stu-id="8bee4-135">The **continue** response includes an array for **cards**, which is rendered vertically to the tab in the order of the array.</span></span>

> [!NOTE]
> <span data-ttu-id="8bee4-136">身份验证 **部分** 详细介绍了 [身份验证响应。](#authentication)</span><span class="sxs-lookup"><span data-stu-id="8bee4-136">The **auth** response is explained in detail in the [authentication](#authentication) section.</span></span>

<span data-ttu-id="8bee4-137">以下代码段是请求 `tab/fetch` 和响应的示例：</span><span class="sxs-lookup"><span data-stu-id="8bee4-137">The following code snippets are examples of `tab/fetch` request and response:</span></span>

<span data-ttu-id="8bee4-138">**`tab/fetch` request**</span><span class="sxs-lookup"><span data-stu-id="8bee4-138">**`tab/fetch` request**</span></span>

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

<span data-ttu-id="8bee4-139">**`tab/fetch` 响应**</span><span class="sxs-lookup"><span data-stu-id="8bee4-139">**`tab/fetch` response**</span></span>

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

### <a name="handle-submits-from-adaptive-card"></a><span data-ttu-id="8bee4-140">处理自适应卡片中的提交</span><span class="sxs-lookup"><span data-stu-id="8bee4-140">Handle submits from Adaptive Card</span></span>

<span data-ttu-id="8bee4-141">在选项卡中呈现自适应卡片后，它必须能够响应用户交互。</span><span class="sxs-lookup"><span data-stu-id="8bee4-141">After an Adaptive Card is rendered in the tab, it must be able to respond to user interactions.</span></span> <span data-ttu-id="8bee4-142">此响应由调用 `tab/submit` 请求处理。</span><span class="sxs-lookup"><span data-stu-id="8bee4-142">This response is handled by the `tab/submit` invoke request.</span></span>

<span data-ttu-id="8bee4-143">当用户在自适应卡片选项卡上选择按钮时，请求通过自适应卡片的 `tab/submit` *Action.Submit* 函数触发到具有相应数据的机器人。</span><span class="sxs-lookup"><span data-stu-id="8bee4-143">When a user selects a button on the Adaptive Card Tab, the `tab/submit` request is triggered to your bot with the corresponding data through the *Action.Submit* function of Adaptive Card.</span></span> <span data-ttu-id="8bee4-144">自适应卡片数据通过请求的 data 属性 `tab/submit` 提供。</span><span class="sxs-lookup"><span data-stu-id="8bee4-144">The Adaptive Card data is available through the data property of the `tab/submit` request.</span></span> <span data-ttu-id="8bee4-145">您将收到以下请求响应之一：</span><span class="sxs-lookup"><span data-stu-id="8bee4-145">You will receive either of the following responses to your request:</span></span>

* <span data-ttu-id="8bee4-146">无正文的 http `200` 状态代码响应。</span><span class="sxs-lookup"><span data-stu-id="8bee4-146">A http status code `200` response with no body.</span></span> <span data-ttu-id="8bee4-147">空 200 响应将导致客户端不执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="8bee4-147">An empty 200 response will result in no action taken by the client.</span></span>
* <span data-ttu-id="8bee4-148">标准选项卡 `200` **继续响应** ，如提取自适应 [卡片部分](#fetch-adaptive-card-to-render-to-a-tab) 所述。</span><span class="sxs-lookup"><span data-stu-id="8bee4-148">The standard `200` tab **continue** response, as explained in [Fetch Adaptive Card](#fetch-adaptive-card-to-render-to-a-tab) section.</span></span> <span data-ttu-id="8bee4-149">选项卡 **继续** 响应会触发客户端使用继续响应的卡片数组中提供的自适应卡片更新呈现的自适应 **卡片选项卡。**</span><span class="sxs-lookup"><span data-stu-id="8bee4-149">A tab **continue** response triggers the client to update the rendered Adaptive Card Tab with the Adaptive Cards provided in the cards array of the **continue** response.</span></span>

<span data-ttu-id="8bee4-150">以下代码段是请求 `tab/submit` 和响应的示例：</span><span class="sxs-lookup"><span data-stu-id="8bee4-150">The following code snippets are examples of `tab/submit` request and response:</span></span>

<span data-ttu-id="8bee4-151">**`tab/submit` request**</span><span class="sxs-lookup"><span data-stu-id="8bee4-151">**`tab/submit` request**</span></span>

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

<span data-ttu-id="8bee4-152">**`tab/submit` 响应**</span><span class="sxs-lookup"><span data-stu-id="8bee4-152">**`tab/submit` response**</span></span>

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

## <a name="understand-task-module-workflow"></a><span data-ttu-id="8bee4-153">了解任务模块工作流</span><span class="sxs-lookup"><span data-stu-id="8bee4-153">Understand task module workflow</span></span>

<span data-ttu-id="8bee4-154">任务模块还使用自适应卡片 `task/fetch` 调用和 `task/submit` 请求和响应。</span><span class="sxs-lookup"><span data-stu-id="8bee4-154">The task module also uses Adaptive Card to invoke `task/fetch` and `task/submit` requests and responses.</span></span> <span data-ttu-id="8bee4-155">有关详细信息，请参阅使用自动程序[中Microsoft Teams模块](../../task-modules-and-cards/task-modules/task-modules-bots.md)。</span><span class="sxs-lookup"><span data-stu-id="8bee4-155">For more information, see [Using Task Modules in Microsoft Teams bots](../../task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="8bee4-156">但是，随着自适应卡片选项卡的引入，机器人响应请求方式会 `task/submit` 发生变化。</span><span class="sxs-lookup"><span data-stu-id="8bee4-156">However, with the introduction of Adaptive Card Tab there is a change in how the bot responds to a `task/submit` request.</span></span> <span data-ttu-id="8bee4-157">如果你使用的是自适应卡片选项卡，机器人会使用标准选项卡继续响应来响应调用请求，并 `task/submit` 关闭任务模块。</span><span class="sxs-lookup"><span data-stu-id="8bee4-157">If you are using an Adaptive Card Tab, the bot responds to the `task/submit` invoke request with the standard tab **continue** response, and closes the task module.</span></span> <span data-ttu-id="8bee4-158">自适应卡片选项卡通过呈现选项卡继续响应正文中提供的新卡片 **列表** 进行更新。</span><span class="sxs-lookup"><span data-stu-id="8bee4-158">The Adaptive Card Tab is updated by rendering the new list of cards provided in the tab **continue** response body.</span></span>

### <a name="invoke-taskfetch"></a><span data-ttu-id="8bee4-159">Invoke `task/fetch`</span><span class="sxs-lookup"><span data-stu-id="8bee4-159">Invoke `task/fetch`</span></span>

<span data-ttu-id="8bee4-160">以下代码段是请求 `task/fetch` 和响应的示例：</span><span class="sxs-lookup"><span data-stu-id="8bee4-160">The following code snippets are examples of `task/fetch` request and response:</span></span>

<span data-ttu-id="8bee4-161">**`task/fetch` request**</span><span class="sxs-lookup"><span data-stu-id="8bee4-161">**`task/fetch` request**</span></span>
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

<span data-ttu-id="8bee4-162">**`task/fetch` 响应**</span><span class="sxs-lookup"><span data-stu-id="8bee4-162">**`task/fetch` response**</span></span>

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

### <a name="invoke-tasksubmit"></a><span data-ttu-id="8bee4-163">Invoke `task/submit`</span><span class="sxs-lookup"><span data-stu-id="8bee4-163">Invoke `task/submit`</span></span>

<span data-ttu-id="8bee4-164">以下代码段是请求 `task/submit` 和响应的示例：</span><span class="sxs-lookup"><span data-stu-id="8bee4-164">The following code snippets are examples of `task/submit` request and response:</span></span>

<span data-ttu-id="8bee4-165">**`task/submit` request**</span><span class="sxs-lookup"><span data-stu-id="8bee4-165">**`task/submit` request**</span></span>

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

<span data-ttu-id="8bee4-166">**`task/submit` 选项卡响应类型**</span><span class="sxs-lookup"><span data-stu-id="8bee4-166">**`task/submit` tab response type**</span></span>

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

## <a name="authentication"></a><span data-ttu-id="8bee4-167">身份验证</span><span class="sxs-lookup"><span data-stu-id="8bee4-167">Authentication</span></span>

<span data-ttu-id="8bee4-168">在本文的前面几节中，你已看到大部分开发范例可以外推自任务模块请求和响应到选项卡请求和响应中。</span><span class="sxs-lookup"><span data-stu-id="8bee4-168">In the previous sections of this article, you have seen that most of the development paradigms could be extrapolated from the task module requests and responses into tab requests and responses.</span></span> <span data-ttu-id="8bee4-169">但是，当涉及到处理身份验证时，自适应卡片选项卡的工作流遵循邮件扩展的身份验证模式。</span><span class="sxs-lookup"><span data-stu-id="8bee4-169">However, when it comes to handling authentication, the workflow for Adaptive Card Tab follows the authentication pattern for messaging extensions.</span></span> <span data-ttu-id="8bee4-170">有关详细信息，请参阅 [添加身份验证](../../messaging-extensions/how-to/add-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="8bee4-170">For more information, see [add authentication](../../messaging-extensions/how-to/add-authentication.md).</span></span> 

<span data-ttu-id="8bee4-171">在 ["调用活动](#invoke-activities)"部分，将通知你请求可以具有继续响应 `tab/fetch` 或 **身份验证** 响应。</span><span class="sxs-lookup"><span data-stu-id="8bee4-171">In the [invoke activities](#invoke-activities) section, you were informed that `tab/fetch` requests can have either a **continue** or an **auth** response.</span></span> <span data-ttu-id="8bee4-172">当 `tab/fetch` 触发请求并收到选项卡 **身份验证** 响应时，登录页会向用户显示。</span><span class="sxs-lookup"><span data-stu-id="8bee4-172">When a `tab/fetch` request is triggered and receives a tab **auth** response, the sign-in page is shown to the user.</span></span> 

<span data-ttu-id="8bee4-173">**通过调用获取身份验证 `tab/fetch` 代码**</span><span class="sxs-lookup"><span data-stu-id="8bee4-173">**To get an authentication code through `tab/fetch` invoke**</span></span>

1. <span data-ttu-id="8bee4-174">打开你的应用。</span><span class="sxs-lookup"><span data-stu-id="8bee4-174">Open your app.</span></span> <span data-ttu-id="8bee4-175">将显示登录页。</span><span class="sxs-lookup"><span data-stu-id="8bee4-175">The sign in page appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8bee4-176">应用徽标通过应用清单中定义的 属性提供，徽标在选项卡身份验证响应正文中返回的属性中定义后显示 `icon` `title` 的标题。 </span><span class="sxs-lookup"><span data-stu-id="8bee4-176">The app logo is provided through the `icon` property defined in the app manifest, and the title appearing after the logo is defined in the `title` property returned in the tab **auth** response body.</span></span>

1. <span data-ttu-id="8bee4-177">选择“**登录**”。</span><span class="sxs-lookup"><span data-stu-id="8bee4-177">Select **Sign in**.</span></span> <span data-ttu-id="8bee4-178">您将重定向到身份验证响应正文的 属性中提供的 `value` 身份验证 URL。 </span><span class="sxs-lookup"><span data-stu-id="8bee4-178">You are redirected to the authentication URL provided in the `value` property of the **auth** response body.</span></span> 
1. <span data-ttu-id="8bee4-179">将出现一个弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="8bee4-179">A pop-up window appears.</span></span> <span data-ttu-id="8bee4-180">此弹出窗口使用身份验证 URL 托管网页。</span><span class="sxs-lookup"><span data-stu-id="8bee4-180">This pop-up window hosts your web page using the authentication URL.</span></span>
1. <span data-ttu-id="8bee4-181">登录后，关闭窗口。</span><span class="sxs-lookup"><span data-stu-id="8bee4-181">After you sign in, close the window.</span></span> <span data-ttu-id="8bee4-182">身份验证 *代码* 将发送到 Teams 客户端。</span><span class="sxs-lookup"><span data-stu-id="8bee4-182">An *authentication code* is sent to the Teams client.</span></span>
1. <span data-ttu-id="8bee4-183">然后Teams客户端重新向服务提出请求，其中包括托管网页提供的 `tab/fetch` 身份验证代码。</span><span class="sxs-lookup"><span data-stu-id="8bee4-183">The Teams client then reissues the `tab/fetch` request to your service, which includes the authentication code provided by your hosted web page.</span></span> 

### <a name="tabfetch-authentication-data-flow"></a><span data-ttu-id="8bee4-184">`tab/fetch` 身份验证数据流</span><span class="sxs-lookup"><span data-stu-id="8bee4-184">`tab/fetch` authentication data flow</span></span>

<span data-ttu-id="8bee4-185">下图概述了身份验证数据流如何用于 `tab/fetch` 调用。</span><span class="sxs-lookup"><span data-stu-id="8bee4-185">The following image provides an overview of how the authentication data flow works for a `tab/fetch` invoke.</span></span>

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="自适应卡片选项卡身份验证流的示例。" border="false":::

<span data-ttu-id="8bee4-187">**`tab/fetch` 身份验证响应**</span><span class="sxs-lookup"><span data-stu-id="8bee4-187">**`tab/fetch` auth response**</span></span>

<span data-ttu-id="8bee4-188">以下代码段是身份验证 `tab/fetch` 响应的一个示例：</span><span class="sxs-lookup"><span data-stu-id="8bee4-188">The following code snippet is an example of `tab/fetch` auth response:</span></span>

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

### <a name="example"></a><span data-ttu-id="8bee4-189">示例</span><span class="sxs-lookup"><span data-stu-id="8bee4-189">Example</span></span>

<span data-ttu-id="8bee4-190">下面显示了重新发送的请求示例：</span><span class="sxs-lookup"><span data-stu-id="8bee4-190">The following shows a reissued request example:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="8bee4-191">另请参阅</span><span class="sxs-lookup"><span data-stu-id="8bee4-191">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8bee4-192">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="8bee4-192">Adaptive Card</span></span>](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)

