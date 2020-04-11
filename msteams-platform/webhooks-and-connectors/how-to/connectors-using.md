---
title: 向连接器和 Webhook 发送邮件
description: 介绍如何使用 Microsoft Teams 中的 Office 365 连接器
localization_priority: Priority
keywords: Teams o365 连接器
ms.openlocfilehash: df91dfc68dbafb5e32d8c0e5732eb820c21a51b0
ms.sourcegitcommit: a08f1c7eb9fca11f44842773ab669c69d4af40db
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/10/2020
ms.locfileid: "43225775"
---
# <a name="sending-messages-to-connectors-and-webhooks"></a><span data-ttu-id="645bd-104">向连接器和 Webhook 发送邮件</span><span class="sxs-lookup"><span data-stu-id="645bd-104">Sending messages to connectors and webhooks</span></span>

<span data-ttu-id="645bd-105">若要通过 Office 365 连接器或传入 Webhook 发送邮件，请将 JSON 有效负载发布到 Webhook URL。</span><span class="sxs-lookup"><span data-stu-id="645bd-105">To send a message through your Office 365 Connector or incoming webhook, you post a JSON payload to the webhook URL.</span></span> <span data-ttu-id="645bd-106">通常，此有效负载将采用 [Office 365 连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)的形式。</span><span class="sxs-lookup"><span data-stu-id="645bd-106">Typically this payload will be in the form of an [Office 365 Connector Card](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="645bd-107">还可使用此 JSON 创建包含丰富输入内容（如文本输入、多重选择或选择日期和时间）的卡。</span><span class="sxs-lookup"><span data-stu-id="645bd-107">You can also use this JSON to create cards containing rich inputs, such as text entry, multi-select, or picking a date and time.</span></span> <span data-ttu-id="645bd-108">生成卡并将其发布到 Webhook URL 的代码可以在任何托管服务上运行。</span><span class="sxs-lookup"><span data-stu-id="645bd-108">The code that generates the card and posts to the webhook URL can be running on any hosted service.</span></span> <span data-ttu-id="645bd-109">这些卡片被定义为可操作邮件的一部分，在 Teams 机器人和邮件扩展中使用的[卡片](~/task-modules-and-cards/what-are-cards.md)受支持。</span><span class="sxs-lookup"><span data-stu-id="645bd-109">These cards are defined as part of actionable messages, and are also supported in [cards](~/task-modules-and-cards/what-are-cards.md) used in Teams bots and Messaging extensions.</span></span>

### <a name="example-connector-message"></a><span data-ttu-id="645bd-110">示例连接器邮件</span><span class="sxs-lookup"><span data-stu-id="645bd-110">Example connector message</span></span>

```json
{
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "themeColor": "0076D7",
    "summary": "Larry Bryant created a new task",
    "sections": [{
        "activityTitle": "![TestImage](https://47a92947.ngrok.io/Content/Images/default.png)Larry Bryant created a new task",
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
            "target": "http://..."
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
            "target": "http://..."
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
            "target": "http://..."
        }]
    }]
}
```

<span data-ttu-id="645bd-111">此邮件在频道中生成以下卡片。</span><span class="sxs-lookup"><span data-stu-id="645bd-111">This message produces the following card in the channel.</span></span>

![连接器卡的屏幕截图](~/assets/images/connectors/connector_message.png)

## <a name="creating-actionable-messages"></a><span data-ttu-id="645bd-113">创建可操作邮件</span><span class="sxs-lookup"><span data-stu-id="645bd-113">Creating actionable messages</span></span>

<span data-ttu-id="645bd-114">上一节中的示例包括卡上的三个可见按钮。</span><span class="sxs-lookup"><span data-stu-id="645bd-114">The example in the preceding section includes three visible buttons on the card.</span></span> <span data-ttu-id="645bd-115">通过使用 `ActionCard` 操作在邮件的 `potentialAction` 属性中定义每个按钮，每个操作包含一个输入类型：文本字段、日期选取器或多选列表。</span><span class="sxs-lookup"><span data-stu-id="645bd-115">Each button is defined in the `potentialAction` property of the message by using `ActionCard` actions, each containing an input type: a text field, a date picker, or a multi-choice list.</span></span> <span data-ttu-id="645bd-116">每个 `ActionCard` 操作都具有关联的操作，例如 `HttpPOST`。</span><span class="sxs-lookup"><span data-stu-id="645bd-116">Each `ActionCard` action has an associated action, for example `HttpPOST`.</span></span>

<span data-ttu-id="645bd-117">连接器卡支持三种类型的操作：</span><span class="sxs-lookup"><span data-stu-id="645bd-117">Connector cards support three types of actions:</span></span>

- <span data-ttu-id="645bd-118">`ActionCard` 显示一个或多个输入类型和关联的操作</span><span class="sxs-lookup"><span data-stu-id="645bd-118">`ActionCard` Presents one or more input types and associated actions</span></span>
- <span data-ttu-id="645bd-119">`HttpPOST` 向 URL 发送 POST 请求</span><span class="sxs-lookup"><span data-stu-id="645bd-119">`HttpPOST` Sends a POST request to a URL</span></span>
- <span data-ttu-id="645bd-120">`OpenUri` 在单独的浏览器或应用程序中打开 URI；根据操作系统，可选择性地针对不同的 URI</span><span class="sxs-lookup"><span data-stu-id="645bd-120">`OpenUri` Opens a URI in a separate browser or app; optionally targets different URIs based on operating systems</span></span>

<span data-ttu-id="645bd-121">（第四个操作 `ViewAction` 仍受支持，但不再需要；改用 `OpenUri`。）</span><span class="sxs-lookup"><span data-stu-id="645bd-121">(A fourth action, `ViewAction`, is still supported but no longer needed; use `OpenUri` instead.)</span></span>

<span data-ttu-id="645bd-122">`ActionCard` 操作支持三种输入类型：</span><span class="sxs-lookup"><span data-stu-id="645bd-122">The `ActionCard` action supports three input types:</span></span>

- <span data-ttu-id="645bd-123">`TextInput` 具有可选长度限制的单行或多行文本字段</span><span class="sxs-lookup"><span data-stu-id="645bd-123">`TextInput` A single-line or multiline text field with an optional length limit</span></span>
- <span data-ttu-id="645bd-124">`DateInput` 具有可选时间选择器的日期选择器</span><span class="sxs-lookup"><span data-stu-id="645bd-124">`DateInput` A date selector with an optional time selector</span></span>
- <span data-ttu-id="645bd-125">`MultichoiceInput` 提供单项选择或多重选择的选项枚举列表</span><span class="sxs-lookup"><span data-stu-id="645bd-125">`MultichoiceInput` A enumerated list of choices offering either a single selection or multiple selections</span></span>

<span data-ttu-id="645bd-126">`MultichoiceInput` 支持控制列表最初是否完全展开的 `style` 属性。</span><span class="sxs-lookup"><span data-stu-id="645bd-126">`MultichoiceInput` supports a `style` property that controls whether the list initially appears fully expanded.</span></span> <span data-ttu-id="645bd-127">`style` 的默认值取决于 `isMultiSelect` 的值。</span><span class="sxs-lookup"><span data-stu-id="645bd-127">The default value of `style` depends on the value of `isMultiSelect`.</span></span>

| `isMultiSelect` | <span data-ttu-id="645bd-128">`style` 默认值</span><span class="sxs-lookup"><span data-stu-id="645bd-128">`style` default</span></span> |
| --- | --- |
| <span data-ttu-id="645bd-129">`false` 或未指定</span><span class="sxs-lookup"><span data-stu-id="645bd-129">`false` or not specified</span></span> | `compact` |
| `true` | `expanded` |

<span data-ttu-id="645bd-130">如果想要以精简样式初始显示多选列表，则必须同时指定 `"isMultiSelect": true` 和 `"style": true`。</span><span class="sxs-lookup"><span data-stu-id="645bd-130">If you want a multiselect list initially displayed in the compact style, you must specify both `"isMultiSelect": true` and `"style": true`.</span></span>

> [!NOTE]
> <span data-ttu-id="645bd-131">在 Microsoft Teams 中的指定 `style` 属性的 `compact` 与在 Microsoft Outlook 中指定 `style` 属性的 `normal` 相同。</span><span class="sxs-lookup"><span data-stu-id="645bd-131">Specifying `compact` for the `style` property in Microsoft Teams is the same as specifying `normal` for the `style` property in Microsoft Outlook.</span></span>

<span data-ttu-id="645bd-132">有关连接器卡操作的所有其他详细信息，请参阅可操作的邮件卡参考中的**[“操作”](/outlook/actionable-messages/card-reference#actions)**。</span><span class="sxs-lookup"><span data-stu-id="645bd-132">For all other details about Connector card actions, see **[Actions](/outlook/actionable-messages/card-reference#actions)** in the actionable message card reference.</span></span>

## <a name="setting-up-a-custom-incoming-webhook"></a><span data-ttu-id="645bd-133">设置自定义传入 Webhook</span><span class="sxs-lookup"><span data-stu-id="645bd-133">Setting up a custom incoming webhook</span></span>

<span data-ttu-id="645bd-134">请按照以下步骤，了解如何向连接器发送简单卡。</span><span class="sxs-lookup"><span data-stu-id="645bd-134">Follow these steps to see how to send a simple card to a Connector.</span></span>

1. <span data-ttu-id="645bd-135">在 Microsoft Teams 中，选择频道名称旁边的 **“更多选项”**(**&#8943;**) ，然后选择 **“连接器”**。</span><span class="sxs-lookup"><span data-stu-id="645bd-135">In Microsoft Teams, choose **More options** (**&#8943;**) next to the channel name and then choose **Connectors**.</span></span>
2. <span data-ttu-id="645bd-136">滚动浏览 **“传入 Webhook”** 的连接器列表，然后选择 **“添加”**。</span><span class="sxs-lookup"><span data-stu-id="645bd-136">Scroll through the list of Connectors to **Incoming Webhook**, and choose **Add**.</span></span>
3. <span data-ttu-id="645bd-137">输入 Webhook 的名称，上传图像以与 Webhook 中的数据相关联，然后选择 **“创建”**。</span><span class="sxs-lookup"><span data-stu-id="645bd-137">Enter a name for the webhook, upload an image to associate with data from the webhook, and choose **Create**.</span></span>
4. <span data-ttu-id="645bd-138">将 Webhook 复制到剪贴板并保存。</span><span class="sxs-lookup"><span data-stu-id="645bd-138">Copy the webhook to the clipboard and save it.</span></span> <span data-ttu-id="645bd-139">需要 Webhook URL 才能将信息发送到 Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="645bd-139">You'll need the webhook URL for sending information to Microsoft Teams.</span></span>
5. <span data-ttu-id="645bd-140">选择 **“完成”**。</span><span class="sxs-lookup"><span data-stu-id="645bd-140">Choose **Done**.</span></span>

### <a name="post-a-message-to-the-webhook-using-curl"></a><span data-ttu-id="645bd-141">使用 cURL 将邮件发布到 Webhook</span><span class="sxs-lookup"><span data-stu-id="645bd-141">Post a message to the webhook using cURL</span></span>

<span data-ttu-id="645bd-142">以下步骤使用 [cURL](https://curl.haxx.se/)。</span><span class="sxs-lookup"><span data-stu-id="645bd-142">The following steps use [cURL](https://curl.haxx.se/).</span></span> <span data-ttu-id="645bd-143">假设你已安装，并熟悉其基本用法。</span><span class="sxs-lookup"><span data-stu-id="645bd-143">We assume that you have this installed and are familiar with its basic usage.</span></span>

1. <span data-ttu-id="645bd-144">在命令行中输入以下 cURL 命令：</span><span class="sxs-lookup"><span data-stu-id="645bd-144">From the command line, enter the following cURL command:</span></span>

   ```bash
   // on macOS or Linux
   curl -H 'Content-Type: application/json' -d '{\"text\": \"Hello World\"}' <YOUR WEBHOOK URL>
   ```

   ```bash
   // on Windows
   curl.exe -H 'Content-Type: application/json' -d '{\"text\": \"Hello World\"}' <YOUR WEBHOOK URL>
   ```

2. <span data-ttu-id="645bd-145">如果 POST 成功，则可以看到 `curl` 简单输出 **1**。</span><span class="sxs-lookup"><span data-stu-id="645bd-145">If the POST succeeds, you should see a simple **1** output by `curl`.</span></span>
3. <span data-ttu-id="645bd-146">检查 Microsoft Team 客户端。</span><span class="sxs-lookup"><span data-stu-id="645bd-146">Check the Microsoft Team client.</span></span> <span data-ttu-id="645bd-147">你应查看发布到团队的新卡片。</span><span class="sxs-lookup"><span data-stu-id="645bd-147">You should see the new card posted to the team.</span></span>

### <a name="post-a-message-to-the-webhook-using-powershell"></a><span data-ttu-id="645bd-148">使用 PowerShell 将邮件发布到 Webhook</span><span class="sxs-lookup"><span data-stu-id="645bd-148">Post a message to the webhook using PowerShell</span></span>

<span data-ttu-id="645bd-149">以下步骤使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="645bd-149">The following steps use PowerShell.</span></span> <span data-ttu-id="645bd-150">假设你已安装，并熟悉其基本用法。</span><span class="sxs-lookup"><span data-stu-id="645bd-150">We assume that you have this installed and are familiar with its basic usage.</span></span>

1. <span data-ttu-id="645bd-151">在 PowerShell 提示符中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="645bd-151">From the PowerShell prompt, enter the following command:</span></span>

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

2. <span data-ttu-id="645bd-152">如果 POST 成功，则可以看到 `Invoke-RestMethod` 简单输出 **1**。</span><span class="sxs-lookup"><span data-stu-id="645bd-152">If the POST succeeds, you should see a simple **1** output by `Invoke-RestMethod`.</span></span>
3. <span data-ttu-id="645bd-153">检查与 Webhook URL 相关联的 Microsoft Teams 频道。</span><span class="sxs-lookup"><span data-stu-id="645bd-153">Check the Microsoft Teams channel associated with the webhook URL.</span></span> <span data-ttu-id="645bd-154">你应查看发布到频道的新卡片。</span><span class="sxs-lookup"><span data-stu-id="645bd-154">You should see the new card posted to the channel.</span></span>

- <span data-ttu-id="645bd-155">包含两个图标，按照[“图标”](~/concepts/build-and-test/apps-package.md#icons)中的说明。</span><span class="sxs-lookup"><span data-stu-id="645bd-155">Include two icons, following the instructions in [Icons](~/concepts/build-and-test/apps-package.md#icons).</span></span>
- <span data-ttu-id="645bd-156">修改清单的 `icons` 部分，以便引用图标的文件名，而不是 URL。</span><span class="sxs-lookup"><span data-stu-id="645bd-156">Modify the `icons` portion of the manifest to refer to the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="645bd-157">以下 manifest.json 文件包含测试和提交应用程序所需的基本元素。</span><span class="sxs-lookup"><span data-stu-id="645bd-157">The following manifest.json file contains the basic elements needed to test and submit your app.</span></span>

> [!NOTE]
> <span data-ttu-id="645bd-158">将以下示例中的 `id` 和 `connectorId` 替换为连接器的 GUID。</span><span class="sxs-lookup"><span data-stu-id="645bd-158">Replace `id` and `connectorId` in the following example with the GUID of your Connector.</span></span>

#### <a name="example-manifestjson-with-connector"></a><span data-ttu-id="645bd-159">带连接器的示例 manifest.json</span><span class="sxs-lookup"><span data-stu-id="645bd-159">Example manifest.json with connector</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "id": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
  "version": "1.0",
  "packageName": "com.sampleapp",
  "developer": {
    "name": "Publisher",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.microsoft.com",
    "termsOfUseUrl": "https://www.microsoft.com"
  },
  "description": {
    "full": "This is a small sample app we made for you! This app has samples of all capabilities Microsoft Teams supports.",
    "short": "This is a small sample app we made for you!"
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App"
  },
  "accentColor": "#FFFFFF",
  "needsIdentity": "true"
}
```

## <a name="testing-your-connector"></a><span data-ttu-id="645bd-160">测试连接器</span><span class="sxs-lookup"><span data-stu-id="645bd-160">Testing your connector</span></span>

<span data-ttu-id="645bd-161">若要测试连接器，请将其上传到团队中，就像使用任何其他应用程序一样。</span><span class="sxs-lookup"><span data-stu-id="645bd-161">To test your Connector, upload it to a team as you would with any other app.</span></span> <span data-ttu-id="645bd-162">可使用连接器开发人员仪表板中的清单文件（按照上一部分的说明进行修改）和两个图标文件来创建 .zip 包。</span><span class="sxs-lookup"><span data-stu-id="645bd-162">You can create a .zip package using the manifest file from the Connectors Developer Dashboard (modified as directed in the preceding section) and the two icon files.</span></span>

<span data-ttu-id="645bd-163">上传应用程序后，从任意频道打开连接器列表。</span><span class="sxs-lookup"><span data-stu-id="645bd-163">After you upload the app, open the Connectors list from any channel.</span></span> <span data-ttu-id="645bd-164">向下滚动到底部，查看 **“上传”** 部分中的应用程序。</span><span class="sxs-lookup"><span data-stu-id="645bd-164">Scroll to the bottom to see your app in the **Uploaded** section.</span></span>

![“连接器”对话框中上传部分的屏幕截图](~/assets/images/connectors/connector_dialog_uploaded.png)

<span data-ttu-id="645bd-166">现在可启动配置体验。</span><span class="sxs-lookup"><span data-stu-id="645bd-166">You can now launch the configuration experience.</span></span> <span data-ttu-id="645bd-167">请注意，此流程是通过弹出窗口完全在 Microsoft Teams 中发生。</span><span class="sxs-lookup"><span data-stu-id="645bd-167">Be aware that this flow occurs entirely within Microsoft Teams through a pop-up window.</span></span> <span data-ttu-id="645bd-168">目前，这种行为与我们创建的连接器中的配置体验不同；我们正在努力统一体验。</span><span class="sxs-lookup"><span data-stu-id="645bd-168">Currently, this behavior differs from the configuration experience in Connectors that we created; we are working on unifying the experiences.</span></span>

<span data-ttu-id="645bd-169">若要验证 `HttpPOST` 操作是否正常工作，请使用[自定义传入 Webhook](#setting-up-a-custom-incoming-webhook)。</span><span class="sxs-lookup"><span data-stu-id="645bd-169">To verify that an `HttpPOST` action is working correctly, use your [custom incoming webhook](#setting-up-a-custom-incoming-webhook).</span></span>

## <a name="rate-limiting-for-connectors"></a><span data-ttu-id="645bd-170">连接器的速率限制</span><span class="sxs-lookup"><span data-stu-id="645bd-170">Rate limiting for connectors</span></span>

<span data-ttu-id="645bd-171">应用程序速率限制可以控制允许连接器或传入 Webhook 在频道上生成的流量。</span><span class="sxs-lookup"><span data-stu-id="645bd-171">Application rate limits control the traffic that a connector or an incoming webhook is allowed to generate on a channel.</span></span> <span data-ttu-id="645bd-172">Teams 通过固定速率窗口以及以秒为单位的增量计数器跟踪请求。</span><span class="sxs-lookup"><span data-stu-id="645bd-172">Teams tracks requests via a fixed-rate window and incremental counter measured in seconds.</span></span>  <span data-ttu-id="645bd-173">如果发出的请求过多，则会限制客户端连接，直至该窗口刷新（即在固定速率的持续时间内）。</span><span class="sxs-lookup"><span data-stu-id="645bd-173">If too many requests are made, the client connection will be throttled until the window refreshes, i.e., for the duration of the fixed rate.</span></span>

### <a name="transactions-per-second-thresholds"></a><span data-ttu-id="645bd-174">**每秒事务数阈值**</span><span class="sxs-lookup"><span data-stu-id="645bd-174">**Transactions per second thresholds**</span></span>

| <span data-ttu-id="645bd-175">时间（秒）</span><span class="sxs-lookup"><span data-stu-id="645bd-175">Time (seconds)</span></span>  | <span data-ttu-id="645bd-176">允许的最大请求数</span><span class="sxs-lookup"><span data-stu-id="645bd-176">Maximum allowed requests</span></span>  |
|---|---|
| <span data-ttu-id="645bd-177">1</span><span class="sxs-lookup"><span data-stu-id="645bd-177">1</span></span>   | <span data-ttu-id="645bd-178">4</span><span class="sxs-lookup"><span data-stu-id="645bd-178">4</span></span>  |  
| <span data-ttu-id="645bd-179">30</span><span class="sxs-lookup"><span data-stu-id="645bd-179">30</span></span>   | <span data-ttu-id="645bd-180">60</span><span class="sxs-lookup"><span data-stu-id="645bd-180">60</span></span>  |  
| <span data-ttu-id="645bd-181">3600</span><span class="sxs-lookup"><span data-stu-id="645bd-181">3600</span></span>   | <span data-ttu-id="645bd-182">100</span><span class="sxs-lookup"><span data-stu-id="645bd-182">100</span></span>  |
| <span data-ttu-id="645bd-183">7200</span><span class="sxs-lookup"><span data-stu-id="645bd-183">7200</span></span> | <span data-ttu-id="645bd-184">150</span><span class="sxs-lookup"><span data-stu-id="645bd-184">150</span></span>  |
| <span data-ttu-id="645bd-185">86400</span><span class="sxs-lookup"><span data-stu-id="645bd-185">86400</span></span>  | <span data-ttu-id="645bd-186">1800</span><span class="sxs-lookup"><span data-stu-id="645bd-186">1800</span></span>  |

<span data-ttu-id="645bd-187">*另请参阅* [Office 365 连接器 - Microsoft Teams](https://docs.microsoft.com/connectors/teams/)</span><span class="sxs-lookup"><span data-stu-id="645bd-187">*See also* [Office 365 Connectors — Microsoft Teams](https://docs.microsoft.com/connectors/teams/)</span></span>

<span data-ttu-id="645bd-188">如下所示，[具有指数补偿的重试逻辑](/azure/architecture/patterns/retry)将减轻速率限制，以应对请求在一秒内超出限制的情况。</span><span class="sxs-lookup"><span data-stu-id="645bd-188">A [retry logic with exponential back-off](/azure/architecture/patterns/retry) like below would mitigate rate limiting for cases where requests are exceeding the limits within a second.</span></span> <span data-ttu-id="645bd-189">请按照[最佳做法](../../bots/how-to/rate-limit.md#best-practices)避免达到速率限制。</span><span class="sxs-lookup"><span data-stu-id="645bd-189">Please follow [best practices](../../bots/how-to/rate-limit.md#best-practices) to avoid hitting the rate limits.</span></span>

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
 
<span data-ttu-id="645bd-190">这些限制已就位，通过连接器减少频道垃圾邮件，并确保最终用户获得最佳体验。</span><span class="sxs-lookup"><span data-stu-id="645bd-190">These limits are in place to reduce spamming a channel by a connector and ensures an optimal experience to your end users.</span></span>
