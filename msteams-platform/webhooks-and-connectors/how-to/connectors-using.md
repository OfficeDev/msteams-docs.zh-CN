---
title: 创建和发送邮件
author: laujan
description: 介绍如何使用 Microsoft Teams 中的 Office 365 连接器
ms.topic: how-to
localization_priority: Normal
keywords: Teams o365 连接器
ms.openlocfilehash: e396d0048831634f683b6df925853464698fb96a
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140526"
---
# <a name="create-and-send-messages"></a><span data-ttu-id="128dc-104">创建和发送邮件</span><span class="sxs-lookup"><span data-stu-id="128dc-104">Create and send messages</span></span>

<span data-ttu-id="128dc-105">您可以创建可操作邮件，并通过传入 Webhook 或 Office 365 连接器发送。</span><span class="sxs-lookup"><span data-stu-id="128dc-105">You can create actionable messages and send it through Incoming Webhook or Office 365 Connector.</span></span>

## <a name="create-actionable-messages"></a><span data-ttu-id="128dc-106">创建可操作邮件</span><span class="sxs-lookup"><span data-stu-id="128dc-106">Create actionable messages</span></span>

<span data-ttu-id="128dc-107">可操作邮件包含卡片上的三个可见按钮。</span><span class="sxs-lookup"><span data-stu-id="128dc-107">The actionable messages include three visible buttons on the card.</span></span> <span data-ttu-id="128dc-108">每个按钮通过使用操作在邮件的 属性中定义，每个按钮都有一个输入类型、一个 `potentialAction` `ActionCard` 文本字段、一个日期选取器或一个多选项列表。</span><span class="sxs-lookup"><span data-stu-id="128dc-108">Each button is defined in the `potentialAction` property of the message by using `ActionCard` actions, each with an input type, a text field, a date picker, or a multi-choice list.</span></span> <span data-ttu-id="128dc-109">每个 `ActionCard` 都有一个关联的操作，例如 `HttpPOST` 。</span><span class="sxs-lookup"><span data-stu-id="128dc-109">Each `ActionCard` has an associated action, for example `HttpPOST`.</span></span>

<span data-ttu-id="128dc-110">连接器卡支持以下操作：</span><span class="sxs-lookup"><span data-stu-id="128dc-110">The connector cards support the following actions:</span></span>

- <span data-ttu-id="128dc-111">`ActionCard`：显示一个或多个输入类型和关联的操作。</span><span class="sxs-lookup"><span data-stu-id="128dc-111">`ActionCard`: Presents one or more input types and associated actions.</span></span>
- <span data-ttu-id="128dc-112">`HttpPOST`：向 URL 发送 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="128dc-112">`HttpPOST`: Sends POST request to a URL.</span></span>
- <span data-ttu-id="128dc-113">`OpenUri`：在单独的浏览器或应用中打开 URI，并基于操作系统选择面向不同的 URI。</span><span class="sxs-lookup"><span data-stu-id="128dc-113">`OpenUri`: Opens URI in a separate browser or app, optionally targets different URIs based on operating systems.</span></span>

<span data-ttu-id="128dc-114">`ActionCard` 操作支持三种输入类型：</span><span class="sxs-lookup"><span data-stu-id="128dc-114">The `ActionCard` action supports three input types:</span></span>

- <span data-ttu-id="128dc-115">`TextInput`：具有可选长度限制的单行或多行文本字段。</span><span class="sxs-lookup"><span data-stu-id="128dc-115">`TextInput`: A single line or multiline text field with an optional length limit.</span></span>
- <span data-ttu-id="128dc-116">`DateInput`：具有可选时间选择器的日期选择器。</span><span class="sxs-lookup"><span data-stu-id="128dc-116">`DateInput`: A date selector with an optional time selector.</span></span>
- <span data-ttu-id="128dc-117">`MultichoiceInput`：提供单选或多选选项的枚举列表。</span><span class="sxs-lookup"><span data-stu-id="128dc-117">`MultichoiceInput`: An enumerated list of choices offering either a single selection or multiple selections.</span></span>

<span data-ttu-id="128dc-118">`MultichoiceInput` 支持控制列表最初是否完全展开的 `style` 属性。</span><span class="sxs-lookup"><span data-stu-id="128dc-118">`MultichoiceInput` supports a `style` property that controls whether the list initially appears fully expanded.</span></span> <span data-ttu-id="128dc-119">的默认值取决于 `style` 的值 `isMultiSelect` ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="128dc-119">The default value of `style` depends on the value of `isMultiSelect` as follows:</span></span>

| `isMultiSelect` | <span data-ttu-id="128dc-120">`style` 默认值</span><span class="sxs-lookup"><span data-stu-id="128dc-120">`style` default</span></span> |
| --- | --- |
| <span data-ttu-id="128dc-121">`false` 或未指定</span><span class="sxs-lookup"><span data-stu-id="128dc-121">`false` or not specified</span></span> | `compact` |
| `true` | `expanded` |

<span data-ttu-id="128dc-122">若要以紧凑样式显示多选项列表，必须同时指定 `"isMultiSelect": true` 和 `"style": true` 。</span><span class="sxs-lookup"><span data-stu-id="128dc-122">To display the multiselect list in the compact style, you must specify both `"isMultiSelect": true` and `"style": true`.</span></span>

<span data-ttu-id="128dc-123">有关连接器卡操作详细信息，请参阅 [操作](/outlook/actionable-messages/card-reference#actions)。</span><span class="sxs-lookup"><span data-stu-id="128dc-123">For more information on connector card actions, see [Actions](/outlook/actionable-messages/card-reference#actions).</span></span>

> [!NOTE]
> * <span data-ttu-id="128dc-124">在 Microsoft Teams 中指定 `style` 属性的 `compact` 与在 Microsoft Outlook 中指定 `style` 属性的 `normal` 相同。</span><span class="sxs-lookup"><span data-stu-id="128dc-124">Specifying `compact` for the `style` property in Microsoft Teams is the same as specifying `normal` for the `style` property in Microsoft Outlook.</span></span>
> * <span data-ttu-id="128dc-125">对于 HttpPOST 操作，请求中包括承载令牌。</span><span class="sxs-lookup"><span data-stu-id="128dc-125">For the HttpPOST action, the bearer token is included with the requests.</span></span> <span data-ttu-id="128dc-126">此令牌包括已执行该操作的 Office 365 用户的 Azure AD 标识。</span><span class="sxs-lookup"><span data-stu-id="128dc-126">This token includes the Azure AD identity of the Office 365 user who took the action.</span></span>

## <a name="send-a-message-through-incoming-webhook-or-office-365-connector"></a><span data-ttu-id="128dc-127">通过传入 Webhook 或 Office 365 连接器发送邮件</span><span class="sxs-lookup"><span data-stu-id="128dc-127">Send a message through Incoming Webhook or Office 365 Connector</span></span>

<span data-ttu-id="128dc-128">若要通过传入 Webhook 或 Office 365 连接器发送邮件，请将 JSON 有效负载张贴到 webhook URL。</span><span class="sxs-lookup"><span data-stu-id="128dc-128">To send a message through your Incoming Webhook or Office 365 Connector, post a JSON payload to the webhook URL.</span></span> <span data-ttu-id="128dc-129">此有效负载必须以连接器Office 365[的形式。](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)</span><span class="sxs-lookup"><span data-stu-id="128dc-129">This payload must be in the form of an [Office 365 connector card](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="128dc-130">您还可以使用此 JSON 创建包含丰富输入（如文本输入、多选或选择日期和时间）的卡片。</span><span class="sxs-lookup"><span data-stu-id="128dc-130">You can also use this JSON to create cards containing rich inputs, such as text entry, multiselect, or selecting date and time.</span></span> <span data-ttu-id="128dc-131">生成卡片并张贴到 webhook URL 的代码可以在任何托管服务中运行。</span><span class="sxs-lookup"><span data-stu-id="128dc-131">The code that generates the card and posts it to the webhook URL can run on any hosted service.</span></span> <span data-ttu-id="128dc-132">这些卡片定义为可操作邮件的一部分，在卡片中也受[](~/task-modules-and-cards/what-are-cards.md)支持，用于Teams聊天机器人和消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="128dc-132">These cards are defined as part of actionable messages and are also supported in [cards](~/task-modules-and-cards/what-are-cards.md), used in Teams bots and messaging extensions.</span></span>

### <a name="example-of-connector-message"></a><span data-ttu-id="128dc-133">连接器邮件示例</span><span class="sxs-lookup"><span data-stu-id="128dc-133">Example of connector message</span></span>

<span data-ttu-id="128dc-134">连接器邮件的示例如下所示：</span><span class="sxs-lookup"><span data-stu-id="128dc-134">An example of connector message is as follows:</span></span>

```json
{
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "themeColor": "0076D7",
    "summary": "Larry Bryant created a new task",
    "sections": [{
        "activityTitle": "Larry Bryant created a new task",
        "activitySubtitle": "On Project Tango",
        "activityImage": "https://teamsnodesample.azurewebsites.net/static/img/image5.png",
        "facts": [{
            "name": "Assigned to",
            "value": "Unassigned"
        }, {
            "name": "Due date",
            "value": "Mon May 01 2017 17:07:18 GMT-0700 (Pacific Daylight Time)"
        }, {
            "name": "Status",
            "value": "Not started"
        }],
        "markdown": true
    }],
    "potentialAction": [{
        "@type": "ActionCard",
        "name": "Add a comment",
        "inputs": [{
            "@type": "TextInput",
            "id": "comment",
            "isMultiline": false,
            "title": "Add a comment here for this task"
        }],
        "actions": [{
            "@type": "HttpPOST",
            "name": "Add comment",
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "ActionCard",
        "name": "Set due date",
        "inputs": [{
            "@type": "DateInput",
            "id": "dueDate",
            "title": "Enter a due date for this task"
        }],
        "actions": [{
            "@type": "HttpPOST",
            "name": "Save",
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "OpenUri",
        "name": "Learn More",
        "targets": [{
            "os": "default",
            "uri": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "ActionCard",
        "name": "Change status",
        "inputs": [{
            "@type": "MultichoiceInput",
            "id": "list",
            "title": "Select a status",
            "isMultiSelect": "false",
            "choices": [{
                "display": "In Progress",
                "value": "1"
            }, {
                "display": "Active",
                "value": "2"
            }, {
                "display": "Closed",
                "value": "3"
            }]
        }],
        "actions": [{
            "@type": "HttpPOST",
            "name": "Save",
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }]
}
```

<span data-ttu-id="128dc-135">此消息在频道中提供以下卡片：</span><span class="sxs-lookup"><span data-stu-id="128dc-135">This message provides the following card in the channel:</span></span>

![连接器卡的屏幕截图](~/assets/images/connectorcard.png)

## <a name="send-messages-using-curl-and-powershell"></a><span data-ttu-id="128dc-137">使用 cURL 和 PowerShell 发送邮件</span><span class="sxs-lookup"><span data-stu-id="128dc-137">Send messages using cURL and PowerShell</span></span>

# <a name="curl"></a>[<span data-ttu-id="128dc-138">cURL</span><span class="sxs-lookup"><span data-stu-id="128dc-138">cURL</span></span>](#tab/cURL)

<span data-ttu-id="128dc-139">**使用 cURL 在 Webhook 中发布消息**</span><span class="sxs-lookup"><span data-stu-id="128dc-139">**To post a message in the webhook with cURL**</span></span>

1. <span data-ttu-id="128dc-140">使用 安装 https://curl.haxx.se/ cURL：。</span><span class="sxs-lookup"><span data-stu-id="128dc-140">Install cURL using: https://curl.haxx.se/.</span></span>

1. <span data-ttu-id="128dc-141">在命令行中输入以下 cURL 命令：</span><span class="sxs-lookup"><span data-stu-id="128dc-141">From the command line, enter the following cURL command:</span></span>

   ```bash
   // on macOS or Linux
   curl -H 'Content-Type: application/json' -d '{"text": "Hello World"}' <YOUR WEBHOOK URL>
   ```

   ```bash
   // on Windows
   curl.exe -H "Content-Type:application/json" -d "{'text':'Hello World'}" <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > <span data-ttu-id="128dc-142">如果 POST 成功，则必须看到 一个简单的 **1** 输出 `curl` 。</span><span class="sxs-lookup"><span data-stu-id="128dc-142">If the POST succeeds, you must see a simple **1** output by `curl`.</span></span>

1. <span data-ttu-id="128dc-143">检查Microsoft Teams新卡片的客户端。</span><span class="sxs-lookup"><span data-stu-id="128dc-143">Check the Microsoft Teams client for the new card posted.</span></span>

# <a name="powershell"></a>[<span data-ttu-id="128dc-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="128dc-144">PowerShell</span></span>](#tab/PowerShell)

 <span data-ttu-id="128dc-145">先决条件：安装 PowerShell 并熟悉其基本用法。</span><span class="sxs-lookup"><span data-stu-id="128dc-145">Prerequisite: Installation of PowerShell and familiarization with its basic usage.</span></span>

<span data-ttu-id="128dc-146">**使用 PowerShell 向 Webhook 发布消息**</span><span class="sxs-lookup"><span data-stu-id="128dc-146">**To post a message to the webhook with PowerShell**</span></span>

1. <span data-ttu-id="128dc-147">在 PowerShell 提示符中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="128dc-147">From the PowerShell prompt, enter the following command:</span></span>

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > <span data-ttu-id="128dc-148">如果 POST 成功，则必须看到 一个简单的 **1** 输出 `Invoke-RestMethod` 。</span><span class="sxs-lookup"><span data-stu-id="128dc-148">If the POST succeeds, you must see a simple **1** output by `Invoke-RestMethod`.</span></span>

1. <span data-ttu-id="128dc-149">检查与 Webhook URL 相关联的 Microsoft Teams 频道。</span><span class="sxs-lookup"><span data-stu-id="128dc-149">Check the Microsoft Teams channel associated with the webhook URL.</span></span> <span data-ttu-id="128dc-150">你可以看到已张贴到频道的新卡片。</span><span class="sxs-lookup"><span data-stu-id="128dc-150">You can see the new card posted to the channel.</span></span> <span data-ttu-id="128dc-151">使用连接器测试或发布应用之前，必须执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="128dc-151">Before you use the connector to test or publish your app, you must do the following:</span></span>

    - <span data-ttu-id="128dc-152">[包括两个图标](../../concepts/build-and-test/apps-package.md#app-icons)。</span><span class="sxs-lookup"><span data-stu-id="128dc-152">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
    - <span data-ttu-id="128dc-153">将 `icons` 清单部分修改为图标（而不是 URL）的文件名。</span><span class="sxs-lookup"><span data-stu-id="128dc-153">Modify the `icons` portion of the manifest to the file names of the icons instead of URLs.</span></span>

---

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a><span data-ttu-id="128dc-154">使用传入 Webhook 发送自适应卡片</span><span class="sxs-lookup"><span data-stu-id="128dc-154">Send Adaptive Cards using an Incoming Webhook</span></span>

> [!NOTE]
> * <span data-ttu-id="128dc-155">完全支持所有本机自适应卡片架构元素（除外 `Action.Submit` ）。</span><span class="sxs-lookup"><span data-stu-id="128dc-155">All native Adaptive Card schema elements, except `Action.Submit`, are fully supported.</span></span>
> * <span data-ttu-id="128dc-156">支持的操作包括 [**Action.OpenURL、Action.ShowCard**](https://adaptivecards.io/explorer/Action.OpenUrl.html)和 [**Action.ToggleVisibility。**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html) [](https://adaptivecards.io/explorer/Action.ShowCard.html)</span><span class="sxs-lookup"><span data-stu-id="128dc-156">The supported actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), and [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span></span>

<span data-ttu-id="128dc-157">**通过传入 Webhook 发送自适应卡片**</span><span class="sxs-lookup"><span data-stu-id="128dc-157">**To send Adaptive Cards through an Incoming Webhook**</span></span>

1. <span data-ttu-id="128dc-158">在 Teams 中设置自定义[webhook。](/add-incoming-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="128dc-158">[Setup a custom webhook](/add-incoming-webhook.md) in Teams.</span></span>
1. <span data-ttu-id="128dc-159">使用下面的代码创建自适应卡片 JSON 文件：</span><span class="sxs-lookup"><span data-stu-id="128dc-159">Create Adaptive Card JSON file using the following code:</span></span>

    ```json
    {
       "type":"message",
       "attachments":[
          {
             "contentType":"application/vnd.microsoft.card.adaptive",
             "contentUrl":null,
             "content":{
                "$schema":"http://adaptivecards.io/schemas/adaptive-card.json",
                "type":"AdaptiveCard",
                "version":"1.2",
                "body":[
                    {
                    "type": "TextBlock",
                    "text": "For Samples and Templates, see [https://adaptivecards.io/samples](https://adaptivecards.io/samples)"
                    }
                ]
             }
          }
       ]
    }
    ```

    <span data-ttu-id="128dc-160">自适应卡片 JSON 文件的属性如下所示：</span><span class="sxs-lookup"><span data-stu-id="128dc-160">The properties for Adaptive Card JSON file are as follows:</span></span>

    * <span data-ttu-id="128dc-161">`"type"` 字段必须为 `"message"`。</span><span class="sxs-lookup"><span data-stu-id="128dc-161">The `"type"` field must be `"message"`.</span></span>
    * <span data-ttu-id="128dc-162">`"attachments"` 阵列包含一组卡对象。</span><span class="sxs-lookup"><span data-stu-id="128dc-162">The `"attachments"` array contains a set of card objects.</span></span>
    * <span data-ttu-id="128dc-163">该字段 `"contentType"` 必须设置为自适应卡片类型。</span><span class="sxs-lookup"><span data-stu-id="128dc-163">The `"contentType"` field must be set to Adaptive Card type.</span></span>
    * <span data-ttu-id="128dc-164">`"content"` 对象为采用 JSON 格式的卡。</span><span class="sxs-lookup"><span data-stu-id="128dc-164">The `"content"` object is the card formatted in JSON.</span></span>

1. <span data-ttu-id="128dc-165">使用 Postman 测试自适应卡片：</span><span class="sxs-lookup"><span data-stu-id="128dc-165">Test your Adaptive Card with Postman:</span></span>

    * <span data-ttu-id="128dc-166">使用 [Postman](https://www.postman.com) 测试自适应卡片以向 URL 发送 POST 请求，该请求创建用于设置传入 Webhook。</span><span class="sxs-lookup"><span data-stu-id="128dc-166">Test the Adaptive Card using [Postman](https://www.postman.com) to send a POST request to the URL, created to set up Incoming Webhook.</span></span>
    * <span data-ttu-id="128dc-167">将 JSON 文件粘贴到请求正文中，并查看"自适应卡片"Teams。</span><span class="sxs-lookup"><span data-stu-id="128dc-167">Paste the JSON file in the body of the request and view the Adaptive Card message in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="128dc-168">使用自适应卡片 [代码示例和模板](https://adaptivecards.io/samples) 测试 POST 请求的正文。</span><span class="sxs-lookup"><span data-stu-id="128dc-168">Use Adaptive Card [code samples and templates](https://adaptivecards.io/samples) to test the body of POST request.</span></span>

## <a name="rate-limiting-for-connectors"></a><span data-ttu-id="128dc-169">连接器的速率限制</span><span class="sxs-lookup"><span data-stu-id="128dc-169">Rate limiting for connectors</span></span>

<span data-ttu-id="128dc-170">应用程序速率限制控制允许连接器或传入 Webhook 在通道上生成的流量。</span><span class="sxs-lookup"><span data-stu-id="128dc-170">Application rate limits control the traffic that a connector or an Incoming Webhook is permitted to generate on a channel.</span></span> <span data-ttu-id="128dc-171">Teams固定速率窗口和增量计数器（以秒为单位）跟踪请求。</span><span class="sxs-lookup"><span data-stu-id="128dc-171">Teams track requests using a fixed rate window and incremental counter measured in seconds.</span></span> <span data-ttu-id="128dc-172">如果一秒钟提出四次以上请求，则客户端连接将受到限制，直到窗口在固定速率期间刷新。</span><span class="sxs-lookup"><span data-stu-id="128dc-172">If more than four requests are made in a second, the client connection is throttled until the window refreshes for the duration of the fixed rate.</span></span>

### <a name="transactions-per-second-thresholds"></a><span data-ttu-id="128dc-173">每秒事务数阈值</span><span class="sxs-lookup"><span data-stu-id="128dc-173">Transactions per second thresholds</span></span>

<span data-ttu-id="128dc-174">下表提供了基于时间的交易详细信息：</span><span class="sxs-lookup"><span data-stu-id="128dc-174">The following table provides the time based transaction details:</span></span>

| <span data-ttu-id="128dc-175">时间（以秒表示）</span><span class="sxs-lookup"><span data-stu-id="128dc-175">Time in seconds</span></span>  | <span data-ttu-id="128dc-176">允许的最大请求数</span><span class="sxs-lookup"><span data-stu-id="128dc-176">Maximum allowed requests</span></span>  |
|---|---|
| <span data-ttu-id="128dc-177">1 </span><span class="sxs-lookup"><span data-stu-id="128dc-177">1</span></span>   | <span data-ttu-id="128dc-178">4 </span><span class="sxs-lookup"><span data-stu-id="128dc-178">4</span></span>  |  
| <span data-ttu-id="128dc-179">30</span><span class="sxs-lookup"><span data-stu-id="128dc-179">30</span></span>   | <span data-ttu-id="128dc-180">60</span><span class="sxs-lookup"><span data-stu-id="128dc-180">60</span></span>  |  
| <span data-ttu-id="128dc-181">3600</span><span class="sxs-lookup"><span data-stu-id="128dc-181">3600</span></span>   | <span data-ttu-id="128dc-182">100</span><span class="sxs-lookup"><span data-stu-id="128dc-182">100</span></span>  |
| <span data-ttu-id="128dc-183">7200</span><span class="sxs-lookup"><span data-stu-id="128dc-183">7200</span></span> | <span data-ttu-id="128dc-184">150</span><span class="sxs-lookup"><span data-stu-id="128dc-184">150</span></span>  |
| <span data-ttu-id="128dc-185">86400</span><span class="sxs-lookup"><span data-stu-id="128dc-185">86400</span></span>  | <span data-ttu-id="128dc-186">1800</span><span class="sxs-lookup"><span data-stu-id="128dc-186">1800</span></span>  |

<span data-ttu-id="128dc-187">对于 [请求在](/azure/architecture/patterns/retry) 一秒钟内超出限制的情况，具有指数退信的重试逻辑可以缓解速率限制。</span><span class="sxs-lookup"><span data-stu-id="128dc-187">A [retry logic with exponential back-off](/azure/architecture/patterns/retry) can mitigate rate limiting for cases where requests are exceeding the limits within a second.</span></span> <span data-ttu-id="128dc-188">请 [遵循最佳做法](../../bots/how-to/rate-limit.md) 以避免达到速率限制。</span><span class="sxs-lookup"><span data-stu-id="128dc-188">Follow [best practices](../../bots/how-to/rate-limit.md) to avoid hitting the rate limits.</span></span>

> [!NOTE]
> <span data-ttu-id="128dc-189">对于 [请求在](/azure/architecture/patterns/retry) 一秒钟内超出限制的情况，具有指数退信的重试逻辑可以缓解速率限制。</span><span class="sxs-lookup"><span data-stu-id="128dc-189">A [retry logic with exponential back-off](/azure/architecture/patterns/retry) can mitigate rate limiting for cases where requests are exceeding the limits within a second.</span></span> <span data-ttu-id="128dc-190">请参阅 [HTTP 429 响应](../../bots/how-to/rate-limit.md#handle-http-429-responses)以避免达到速率限制。</span><span class="sxs-lookup"><span data-stu-id="128dc-190">Refer [HTTP 429 responses](../../bots/how-to/rate-limit.md#handle-http-429-responses) to avoid hitting the rate limits.</span></span>

```csharp
// Please note that response body needs to be extracted and read 
// as Connectors do not throw 429s
try
{
    // Perform Connector POST operation     
    var httpResponseMessage = await _client.PostAsync(IncomingWebhookUrl, new StringContent(content));
    // Read response content
    var responseContent = await httpResponseMessage.Content.ReadAsStringAsync();
    if (responseContent.Contains("Microsoft Teams endpoint returned HTTP error 429")) 
    {
        // initiate retry logic
    }
}
```

<span data-ttu-id="128dc-191">这些限制用于减少连接器发送的频道垃圾邮件，并确保为用户提供最佳体验。</span><span class="sxs-lookup"><span data-stu-id="128dc-191">These limits are in place to reduce spamming a channel by a connector and ensures an optimal experience to users.</span></span>

## <a name="see-also"></a><span data-ttu-id="128dc-192">另请参阅</span><span class="sxs-lookup"><span data-stu-id="128dc-192">See also</span></span>

* [<span data-ttu-id="128dc-193">Office 365连接器Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="128dc-193">Office 365 Connectors for Microsoft Teams</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [<span data-ttu-id="128dc-194">创建传入 Webhook</span><span class="sxs-lookup"><span data-stu-id="128dc-194">Create an Incoming Webhook</span></span>](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [<span data-ttu-id="128dc-195">创建传出 Webhook</span><span class="sxs-lookup"><span data-stu-id="128dc-195">Create an Outgoing Webhook</span></span>](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
