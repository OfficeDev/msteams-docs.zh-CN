---
title: 定义邮件扩展搜索命令
author: clearab
description: 为 Microsoft Teams 应用定义邮件扩展搜索命令。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 18bac3049fec8fead168c12f2832bfbbb72cf609
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449267"
---
# <a name="define-messaging-extension-search-commands"></a><span data-ttu-id="da272-103">定义邮件扩展搜索命令</span><span class="sxs-lookup"><span data-stu-id="da272-103">Define messaging extension search commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="da272-104">邮件扩展搜索命令允许用户搜索外部系统，并将该搜索的结果插入卡片形式的邮件中。</span><span class="sxs-lookup"><span data-stu-id="da272-104">Messaging extension search commands allow your users to search external systems and insert the results of that search into a message in the form of a card.</span></span>

> [!NOTE]
> <span data-ttu-id="da272-105">结果卡片大小限制为 28 KB。</span><span class="sxs-lookup"><span data-stu-id="da272-105">The result card size limit is 28 KB.</span></span> <span data-ttu-id="da272-106">如果卡的大小超过 28 KB，则不发送该卡。</span><span class="sxs-lookup"><span data-stu-id="da272-106">The card is not sent if its size exceeds 28 KB.</span></span> 

## <a name="choose-messaging-extension-invoke-locations"></a><span data-ttu-id="da272-107">选择消息扩展调用位置</span><span class="sxs-lookup"><span data-stu-id="da272-107">Choose messaging extension invoke locations</span></span>

<span data-ttu-id="da272-108">需要确定的第一件事是，在何处触发搜索命令 (具体调用搜索) 位置。 </span><span class="sxs-lookup"><span data-stu-id="da272-108">The first thing you need to decide is where your search command can be triggered (or specifically, *invoked*) from.</span></span> <span data-ttu-id="da272-109">可以从以下一个或两个位置调用搜索命令：</span><span class="sxs-lookup"><span data-stu-id="da272-109">Your search command can be invoked from one or both of the following locations:</span></span>

* <span data-ttu-id="da272-110">撰写邮件区域底部的按钮</span><span class="sxs-lookup"><span data-stu-id="da272-110">The buttons at the bottom of the compose message area</span></span>
* <span data-ttu-id="da272-111">在@mentioning框中显示</span><span class="sxs-lookup"><span data-stu-id="da272-111">By @mentioning in the command box</span></span>

<span data-ttu-id="da272-112">从撰写邮件区域调用时，用户可选择将结果发送到对话。</span><span class="sxs-lookup"><span data-stu-id="da272-112">When invoked from the compose message area, your user will have the option of sending the results to the conversation.</span></span> <span data-ttu-id="da272-113">从命令框调用时，用户可以与生成的卡片进行交互，或复制它以在其他地方使用。</span><span class="sxs-lookup"><span data-stu-id="da272-113">When invoked from the command box, the user can interact with the resulting card, or copy it for use elsewhere.</span></span>

## <a name="add-the-command-to-your-app-manifest"></a><span data-ttu-id="da272-114">将命令添加到应用清单</span><span class="sxs-lookup"><span data-stu-id="da272-114">Add the command to your app manifest</span></span>

<span data-ttu-id="da272-115">现在，你已决定用户如何与搜索命令交互，是时候将其添加到应用清单了。</span><span class="sxs-lookup"><span data-stu-id="da272-115">Now that you've decided how users will interact with your search command, it is time to add it to your app manifest.</span></span> <span data-ttu-id="da272-116">为此，你将向应用清单 JSON 的顶层添加新 `composeExtension` 对象。</span><span class="sxs-lookup"><span data-stu-id="da272-116">To do this you'll add a new `composeExtension` object to the top level of your app manifest JSON.</span></span> <span data-ttu-id="da272-117">可以在 App Studio 的帮助下或手动执行。</span><span class="sxs-lookup"><span data-stu-id="da272-117">You can either do so with the help of App Studio, or manually.</span></span>

### <a name="create-a-command-using-app-studio"></a><span data-ttu-id="da272-118">使用 App Studio 创建命令</span><span class="sxs-lookup"><span data-stu-id="da272-118">Create a command using App Studio</span></span>

<span data-ttu-id="da272-119">创建搜索命令的先决条件是您必须已创建邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="da272-119">The prerequisite to create a search command is that you must already create a messaging extension.</span></span> <span data-ttu-id="da272-120">若要了解如何创建邮件扩展，请参阅 [创建邮件扩展](~/messaging-extensions/how-to/create-messaging-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="da272-120">For information on how to create a messaging extension, see [create a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

<span data-ttu-id="da272-121">**创建搜索命令**</span><span class="sxs-lookup"><span data-stu-id="da272-121">**To create a search command**</span></span>

1. <span data-ttu-id="da272-122">在 Microsoft Teams 客户端中，打开 **App Studio，** 然后选择清单 **编辑器** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="da272-122">From the Microsoft Teams client, open **App Studio**, and select the **Manifest editor** tab.</span></span>
1. <span data-ttu-id="da272-123">如果你已在 **App Studio** 中创建应用包，请从列表中选择它。</span><span class="sxs-lookup"><span data-stu-id="da272-123">If you already created an app package in the **App Studio**, choose it from the list.</span></span> <span data-ttu-id="da272-124">如果尚未创建应用包，请导入现有应用包。</span><span class="sxs-lookup"><span data-stu-id="da272-124">If you have not created an app package, import an existing one.</span></span>
1. <span data-ttu-id="da272-125">导入应用包后，在 **"功能"下选择**"消息扩展 **"。**</span><span class="sxs-lookup"><span data-stu-id="da272-125">After importing an app package, select **Messaging extensions** under **Capabilities**.</span></span>
1. <span data-ttu-id="da272-126">选择 **"** 消息扩展 **"页** 中的"在命令"部分添加。</span><span class="sxs-lookup"><span data-stu-id="da272-126">Select **Add** in the **Command** section in the messaging extensions page.</span></span>
1. <span data-ttu-id="da272-127">Choose **Allow users to query your service for information and insert that into a message.**</span><span class="sxs-lookup"><span data-stu-id="da272-127">Choose **Allow users to query your service for information and insert that into a message**.</span></span>
1. <span data-ttu-id="da272-128">添加命令 **ID** 和 **标题**。</span><span class="sxs-lookup"><span data-stu-id="da272-128">Add a **Command Id** and a **Title**.</span></span>
1. <span data-ttu-id="da272-129">选择必须触发搜索命令的位置。</span><span class="sxs-lookup"><span data-stu-id="da272-129">Select the location from where your search command must be triggered.</span></span> <span data-ttu-id="da272-130">选择 **邮件** 当前不会更改搜索命令的行为。</span><span class="sxs-lookup"><span data-stu-id="da272-130">Selecting **message** does not currently alter the behavior of your search command.</span></span>
1. <span data-ttu-id="da272-131">添加搜索参数，然后选择"**保存"。**</span><span class="sxs-lookup"><span data-stu-id="da272-131">Add your search parameter and select **Save**.</span></span>
 
### <a name="manually-create-a-command"></a><span data-ttu-id="da272-132">手动创建命令</span><span class="sxs-lookup"><span data-stu-id="da272-132">Manually create a command</span></span>

<span data-ttu-id="da272-133">若要将邮件扩展搜索命令手动添加到应用清单，需要将以下参数添加到 `composeExtension.commands` 对象数组。</span><span class="sxs-lookup"><span data-stu-id="da272-133">To manually add your messaging extension search command to your app manifest, you'll need to add the following parameters to your `composeExtension.commands` array of objects.</span></span>

| <span data-ttu-id="da272-134">属性名称</span><span class="sxs-lookup"><span data-stu-id="da272-134">Property name</span></span> | <span data-ttu-id="da272-135">用途</span><span class="sxs-lookup"><span data-stu-id="da272-135">Purpose</span></span> | <span data-ttu-id="da272-136">是否必需？</span><span class="sxs-lookup"><span data-stu-id="da272-136">Required?</span></span> | <span data-ttu-id="da272-137">最低清单版本</span><span class="sxs-lookup"><span data-stu-id="da272-137">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="da272-138">分配给此命令的唯一 ID。</span><span class="sxs-lookup"><span data-stu-id="da272-138">Unique ID that you assign to this command.</span></span> <span data-ttu-id="da272-139">用户请求将包含此 ID。</span><span class="sxs-lookup"><span data-stu-id="da272-139">The user request will include this ID.</span></span> | <span data-ttu-id="da272-140">是</span><span class="sxs-lookup"><span data-stu-id="da272-140">Yes</span></span> | <span data-ttu-id="da272-141">1.0</span><span class="sxs-lookup"><span data-stu-id="da272-141">1.0</span></span> |
| `title` | <span data-ttu-id="da272-142">命令名称。</span><span class="sxs-lookup"><span data-stu-id="da272-142">Command name.</span></span> <span data-ttu-id="da272-143">此值显示在 UI 中。</span><span class="sxs-lookup"><span data-stu-id="da272-143">This value appears in the UI.</span></span> | <span data-ttu-id="da272-144">是</span><span class="sxs-lookup"><span data-stu-id="da272-144">Yes</span></span> | <span data-ttu-id="da272-145">1.0</span><span class="sxs-lookup"><span data-stu-id="da272-145">1.0</span></span> |
| `description` | <span data-ttu-id="da272-146">指示此命令执行哪些操作的帮助文本。</span><span class="sxs-lookup"><span data-stu-id="da272-146">Help text indicating what this command does.</span></span> <span data-ttu-id="da272-147">此值显示在 UI 中。</span><span class="sxs-lookup"><span data-stu-id="da272-147">This value appears in the UI.</span></span> | <span data-ttu-id="da272-148">是</span><span class="sxs-lookup"><span data-stu-id="da272-148">Yes</span></span> | <span data-ttu-id="da272-149">1.0</span><span class="sxs-lookup"><span data-stu-id="da272-149">1.0</span></span> |
| `type` | <span data-ttu-id="da272-150">必须是 `query`</span><span class="sxs-lookup"><span data-stu-id="da272-150">Must be `query`</span></span> | <span data-ttu-id="da272-151">否</span><span class="sxs-lookup"><span data-stu-id="da272-151">No</span></span> | <span data-ttu-id="da272-152">1.4</span><span class="sxs-lookup"><span data-stu-id="da272-152">1.4</span></span> |
|`initialRun` | <span data-ttu-id="da272-153">如果设置为 **true，** 则指示在用户选择 UI 中的此命令后，应尽快执行此命令。</span><span class="sxs-lookup"><span data-stu-id="da272-153">If set to **true**, indicates this command should be executed as soon as the user chooses this command in the UI.</span></span> | <span data-ttu-id="da272-154">否</span><span class="sxs-lookup"><span data-stu-id="da272-154">No</span></span> | <span data-ttu-id="da272-155">1.0</span><span class="sxs-lookup"><span data-stu-id="da272-155">1.0</span></span> |
| `context` | <span data-ttu-id="da272-156">用于定义搜索操作可用的上下文的可选值数组。</span><span class="sxs-lookup"><span data-stu-id="da272-156">Optional array of values that defines the context the search action is available in.</span></span> <span data-ttu-id="da272-157">可能的值是 `message` ， `compose` 或 `commandBox` 。</span><span class="sxs-lookup"><span data-stu-id="da272-157">Possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="da272-158">默认值为“`["compose", "commandBox"]`”。</span><span class="sxs-lookup"><span data-stu-id="da272-158">Default is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="da272-159">否</span><span class="sxs-lookup"><span data-stu-id="da272-159">No</span></span> | <span data-ttu-id="da272-160">1.5</span><span class="sxs-lookup"><span data-stu-id="da272-160">1.5</span></span> |

<span data-ttu-id="da272-161">你还需要添加搜索参数的详细信息，这将定义在 Teams 客户端中对用户可见的文本。</span><span class="sxs-lookup"><span data-stu-id="da272-161">You'll also need to add the details of the search parameter, which will define the text visible to your user in the Teams client.</span></span>

| <span data-ttu-id="da272-162">属性名称</span><span class="sxs-lookup"><span data-stu-id="da272-162">Property name</span></span> | <span data-ttu-id="da272-163">用途</span><span class="sxs-lookup"><span data-stu-id="da272-163">Purpose</span></span> | <span data-ttu-id="da272-164">是否必需？</span><span class="sxs-lookup"><span data-stu-id="da272-164">Required?</span></span> | <span data-ttu-id="da272-165">最低清单版本</span><span class="sxs-lookup"><span data-stu-id="da272-165">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="da272-166">命令的参数静态列表。</span><span class="sxs-lookup"><span data-stu-id="da272-166">Static list of parameters for the command.</span></span> | <span data-ttu-id="da272-167">否</span><span class="sxs-lookup"><span data-stu-id="da272-167">No</span></span> | <span data-ttu-id="da272-168">1.0</span><span class="sxs-lookup"><span data-stu-id="da272-168">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="da272-169">参数的名称。</span><span class="sxs-lookup"><span data-stu-id="da272-169">The name of the parameter.</span></span> <span data-ttu-id="da272-170">这将在用户请求中发送到你的服务。</span><span class="sxs-lookup"><span data-stu-id="da272-170">This is sent to your service in the user request.</span></span> | <span data-ttu-id="da272-171">是</span><span class="sxs-lookup"><span data-stu-id="da272-171">Yes</span></span> | <span data-ttu-id="da272-172">1.0</span><span class="sxs-lookup"><span data-stu-id="da272-172">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="da272-173">描述此参数的用途或应提供的值示例。</span><span class="sxs-lookup"><span data-stu-id="da272-173">Describes this parameter’s purposes or example of the value that should be provided.</span></span> <span data-ttu-id="da272-174">此值显示在 UI 中。</span><span class="sxs-lookup"><span data-stu-id="da272-174">This value appears in the UI.</span></span> | <span data-ttu-id="da272-175">是</span><span class="sxs-lookup"><span data-stu-id="da272-175">Yes</span></span> | <span data-ttu-id="da272-176">1.0</span><span class="sxs-lookup"><span data-stu-id="da272-176">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="da272-177">简短的用户友好参数标题或标签。</span><span class="sxs-lookup"><span data-stu-id="da272-177">Short user-friendly parameter title or label.</span></span> | <span data-ttu-id="da272-178">是</span><span class="sxs-lookup"><span data-stu-id="da272-178">Yes</span></span> | <span data-ttu-id="da272-179">1.0</span><span class="sxs-lookup"><span data-stu-id="da272-179">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="da272-180">设置为所需的输入类型。</span><span class="sxs-lookup"><span data-stu-id="da272-180">Set to the type of input required.</span></span> <span data-ttu-id="da272-181">可能的值包括 `text` ， ， ， ， `textarea` `number` `date` `time` `toggle` 。</span><span class="sxs-lookup"><span data-stu-id="da272-181">Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="da272-182">默认值设置为 `text`</span><span class="sxs-lookup"><span data-stu-id="da272-182">Default is set to `text`</span></span> | <span data-ttu-id="da272-183">否</span><span class="sxs-lookup"><span data-stu-id="da272-183">No</span></span> | <span data-ttu-id="da272-184">1.4</span><span class="sxs-lookup"><span data-stu-id="da272-184">1.4</span></span> |

#### <a name="app-manifest-example"></a><span data-ttu-id="da272-185">应用清单示例</span><span class="sxs-lookup"><span data-stu-id="da272-185">App manifest example</span></span>

<span data-ttu-id="da272-186">下面是定义搜索 `composeExtensions` 命令的对象的示例。</span><span class="sxs-lookup"><span data-stu-id="da272-186">Below is an example of a `composeExtensions` object defining a search command.</span></span> <span data-ttu-id="da272-187">这不是完整清单的示例，有关完整应用清单架构，请参阅： [应用清单架构](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="da272-187">It is not an example of the complete manifest, for the full app manifest schema see: [App manifest schema](~/resources/schema/manifest-schema.md).</span></span>

```json
{
...
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
...
}
```

## <a name="next-steps"></a><span data-ttu-id="da272-188">后续步骤</span><span class="sxs-lookup"><span data-stu-id="da272-188">Next steps</span></span>

<span data-ttu-id="da272-189">现在，你已添加搜索命令，你将需要 [处理搜索请求](~/messaging-extensions/how-to/search-commands/respond-to-search.md)。</span><span class="sxs-lookup"><span data-stu-id="da272-189">Now that you've added your search command, you'll need to [handle the search request](~/messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
