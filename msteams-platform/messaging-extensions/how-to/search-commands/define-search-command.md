---
title: 定义邮件扩展搜索命令
author: clearab
description: 为 Microsoft 团队应用程序定义邮件扩展搜索命令。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: b6837fb8a131d8ce3e2bbd0c51c2861dbffda2bc
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673305"
---
# <a name="define-messaging-extension-search-commands"></a><span data-ttu-id="93103-103">定义邮件扩展搜索命令</span><span class="sxs-lookup"><span data-stu-id="93103-103">Define messaging extension search commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="93103-104">邮件扩展搜索命令允许您的用户搜索外部系统，并将该搜索的结果插入卡片形式的邮件中。</span><span class="sxs-lookup"><span data-stu-id="93103-104">Messaging extension search commands allow your users to search external systems and insert the results of that search into a message in the form of a card.</span></span>

## <a name="choose-messaging-extension-invoke-locations"></a><span data-ttu-id="93103-105">选择消息扩展调用位置</span><span class="sxs-lookup"><span data-stu-id="93103-105">Choose messaging extension invoke locations</span></span>

<span data-ttu-id="93103-106">您需要确定的第一件事是可以从其触发搜索命令（或更具体地说，*调用*）。</span><span class="sxs-lookup"><span data-stu-id="93103-106">The first thing you need to decide is where your search command can be triggered (or more specifically, *invoked*) from.</span></span> <span data-ttu-id="93103-107">您可以从以下一个或两个位置调用您的搜索命令：</span><span class="sxs-lookup"><span data-stu-id="93103-107">Your search command can be invoked from one or both of the following locations:</span></span>

* <span data-ttu-id="93103-108">撰写邮件区域底部的按钮</span><span class="sxs-lookup"><span data-stu-id="93103-108">The buttons at the bottom of the compose message area</span></span>
* <span data-ttu-id="93103-109">通过在命令框中 @mentioning</span><span class="sxs-lookup"><span data-stu-id="93103-109">By @mentioning in the command box</span></span>

<span data-ttu-id="93103-110">从撰写邮件区域调用时，您的用户将可以选择将结果发送到对话。</span><span class="sxs-lookup"><span data-stu-id="93103-110">When invoked from the compose message area, your user will have the option of sending the results to the conversation.</span></span> <span data-ttu-id="93103-111">在命令框中调用用户时，用户可以与生成的卡片进行交互，或将其复制以供其他地方使用。</span><span class="sxs-lookup"><span data-stu-id="93103-111">When invoked from the command box, the user can interact with the resulting card, or copy it for use elsewhere.</span></span>

## <a name="add-the-command-to-your-app-manifest"></a><span data-ttu-id="93103-112">将命令添加到应用程序清单</span><span class="sxs-lookup"><span data-stu-id="93103-112">Add the command to your app manifest</span></span>

<span data-ttu-id="93103-113">现在，您已经决定了用户将如何与您的搜索命令进行交互，现在可以将其添加到您的应用程序清单中了。</span><span class="sxs-lookup"><span data-stu-id="93103-113">Now that you've decided how users will interact with your search command, it is time to add it to your app manifest.</span></span> <span data-ttu-id="93103-114">若要执行此操作，请将`composeExtension`新对象添加到应用程序清单 JSON 的最高级别。</span><span class="sxs-lookup"><span data-stu-id="93103-114">To do this you'll add a new `composeExtension` object to the top level of your app manifest JSON.</span></span> <span data-ttu-id="93103-115">您可以使用应用程序 Studio 的帮助或手动执行此操作。</span><span class="sxs-lookup"><span data-stu-id="93103-115">You can either do so with the help of App Studio, or manually.</span></span>

### <a name="create-a-command-using-app-studio"></a><span data-ttu-id="93103-116">使用应用程序 Studio 创建命令</span><span class="sxs-lookup"><span data-stu-id="93103-116">Create a command using App Studio</span></span>

<span data-ttu-id="93103-117">以下步骤假定您已经[创建了邮件扩展](~/messaging-extensions/how-to/create-messaging-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="93103-117">The following steps assume you've already [created a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

1. <span data-ttu-id="93103-118">在 Microsoft 团队客户端中，打开**应用程序 Studio**并选择 "**清单编辑器**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="93103-118">From the Microsoft Teams client, open **App Studio** and select the **Manifest Editor** tab.</span></span>
2. <span data-ttu-id="93103-119">如果您已经在应用程序 Studio 中创建了应用程序包，请从列表中选择它。</span><span class="sxs-lookup"><span data-stu-id="93103-119">If you've already created your app package in App Studio, chose it from the list.</span></span> <span data-ttu-id="93103-120">如果不是，则可以导入现有的应用程序包。</span><span class="sxs-lookup"><span data-stu-id="93103-120">If not, you can import an existing app package.</span></span>
3. <span data-ttu-id="93103-121">单击 "命令" 部分的 "**添加**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="93103-121">Click the **Add** button in the Command section.</span></span>
4. <span data-ttu-id="93103-122">选择 "**允许用户查询服务以获取信息" 并将其插入到邮件中**。</span><span class="sxs-lookup"><span data-stu-id="93103-122">Choose **Allow users to query your service for information and insert that into a message**.</span></span>
5. <span data-ttu-id="93103-123">添加**命令 Id**和**标题**。</span><span class="sxs-lookup"><span data-stu-id="93103-123">Add a **Command Id** and a **Title**.</span></span>
6. <span data-ttu-id="93103-124">选择要从中触发搜索命令的位置。</span><span class="sxs-lookup"><span data-stu-id="93103-124">Select where you want your search command to be triggered from.</span></span> <span data-ttu-id="93103-125">选择**邮件**当前不会改变搜索命令的行为。</span><span class="sxs-lookup"><span data-stu-id="93103-125">Selecting **message** does not currently alter the behavior of your search command.</span></span>
7. <span data-ttu-id="93103-126">添加搜索参数。</span><span class="sxs-lookup"><span data-stu-id="93103-126">Add your search parameter.</span></span>
8. <span data-ttu-id="93103-127">单击"保存"。</span><span class="sxs-lookup"><span data-stu-id="93103-127">Click Save.</span></span>

### <a name="manually-create-a-command"></a><span data-ttu-id="93103-128">手动创建命令</span><span class="sxs-lookup"><span data-stu-id="93103-128">Manually create a command</span></span>

<span data-ttu-id="93103-129">若要将邮件扩展搜索命令手动添加到应用程序清单中，需要将以下参数添加到您`composeExtension.commands`的对象数组中。</span><span class="sxs-lookup"><span data-stu-id="93103-129">To manually add your messaging extension search command to your app manifest, you'll need to add the follow parameters to your `composeExtension.commands` array of objects.</span></span>

| <span data-ttu-id="93103-130">属性名称</span><span class="sxs-lookup"><span data-stu-id="93103-130">Property name</span></span> | <span data-ttu-id="93103-131">用途</span><span class="sxs-lookup"><span data-stu-id="93103-131">Purpose</span></span> | <span data-ttu-id="93103-132">是否必需？</span><span class="sxs-lookup"><span data-stu-id="93103-132">Required?</span></span> | <span data-ttu-id="93103-133">最低清单版本</span><span class="sxs-lookup"><span data-stu-id="93103-133">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="93103-134">您分配给此命令的唯一 ID。</span><span class="sxs-lookup"><span data-stu-id="93103-134">Unique ID that you assign to this command.</span></span> <span data-ttu-id="93103-135">用户请求将包括此 ID。</span><span class="sxs-lookup"><span data-stu-id="93103-135">The user request will include this ID.</span></span> | <span data-ttu-id="93103-136">是</span><span class="sxs-lookup"><span data-stu-id="93103-136">Yes</span></span> | <span data-ttu-id="93103-137">1.0</span><span class="sxs-lookup"><span data-stu-id="93103-137">1.0</span></span> |
| `title` | <span data-ttu-id="93103-138">命令名称。</span><span class="sxs-lookup"><span data-stu-id="93103-138">Command name.</span></span> <span data-ttu-id="93103-139">此值显示在 UI 中。</span><span class="sxs-lookup"><span data-stu-id="93103-139">This value appears in the UI.</span></span> | <span data-ttu-id="93103-140">是</span><span class="sxs-lookup"><span data-stu-id="93103-140">Yes</span></span> | <span data-ttu-id="93103-141">1.0</span><span class="sxs-lookup"><span data-stu-id="93103-141">1.0</span></span> |
| `description` | <span data-ttu-id="93103-142">指示此命令执行的操作的帮助文本。</span><span class="sxs-lookup"><span data-stu-id="93103-142">Help text indicating what this command does.</span></span> <span data-ttu-id="93103-143">此值显示在 UI 中。</span><span class="sxs-lookup"><span data-stu-id="93103-143">This value appears in the UI.</span></span> | <span data-ttu-id="93103-144">是</span><span class="sxs-lookup"><span data-stu-id="93103-144">Yes</span></span> | <span data-ttu-id="93103-145">1.0</span><span class="sxs-lookup"><span data-stu-id="93103-145">1.0</span></span> |
| `type` | <span data-ttu-id="93103-146">必须是 `query`</span><span class="sxs-lookup"><span data-stu-id="93103-146">Must be `query`</span></span> | <span data-ttu-id="93103-147">否</span><span class="sxs-lookup"><span data-stu-id="93103-147">No</span></span> | <span data-ttu-id="93103-148">1.4</span><span class="sxs-lookup"><span data-stu-id="93103-148">1.4</span></span> |
|`initialRun` | <span data-ttu-id="93103-149">如果设置为**true**，则指示应在用户在 UI 中选择此命令后立即执行此命令。</span><span class="sxs-lookup"><span data-stu-id="93103-149">If set to **true**, indicates this command should be executed as soon as the user chooses this command in the UI.</span></span> | <span data-ttu-id="93103-150">否</span><span class="sxs-lookup"><span data-stu-id="93103-150">No</span></span> | <span data-ttu-id="93103-151">1.0</span><span class="sxs-lookup"><span data-stu-id="93103-151">1.0</span></span> |
| `context` | <span data-ttu-id="93103-152">用于定义搜索操作在中可用的上下文的值的可选数组。</span><span class="sxs-lookup"><span data-stu-id="93103-152">Optional array of values that defines the context the search action is available in.</span></span> <span data-ttu-id="93103-153">可能的值`message`为`compose`、或`commandBox`。</span><span class="sxs-lookup"><span data-stu-id="93103-153">Possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="93103-154">默认值为 `["compose", "commandBox"]`。</span><span class="sxs-lookup"><span data-stu-id="93103-154">Default is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="93103-155">否</span><span class="sxs-lookup"><span data-stu-id="93103-155">No</span></span> | <span data-ttu-id="93103-156">1.5</span><span class="sxs-lookup"><span data-stu-id="93103-156">1.5</span></span> |

<span data-ttu-id="93103-157">您还需要添加搜索参数的详细信息，该详细信息将定义在团队客户端中用户可见的文本。</span><span class="sxs-lookup"><span data-stu-id="93103-157">You'll also need to add the details of the search parameter, which will define the text visible to your user in the Teams client.</span></span>

| <span data-ttu-id="93103-158">属性名称</span><span class="sxs-lookup"><span data-stu-id="93103-158">Property name</span></span> | <span data-ttu-id="93103-159">用途</span><span class="sxs-lookup"><span data-stu-id="93103-159">Purpose</span></span> | <span data-ttu-id="93103-160">是否必需？</span><span class="sxs-lookup"><span data-stu-id="93103-160">Required?</span></span> | <span data-ttu-id="93103-161">最低清单版本</span><span class="sxs-lookup"><span data-stu-id="93103-161">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="93103-162">命令的参数的静态列表。</span><span class="sxs-lookup"><span data-stu-id="93103-162">Static list of parameters for the command.</span></span> | <span data-ttu-id="93103-163">否</span><span class="sxs-lookup"><span data-stu-id="93103-163">No</span></span> | <span data-ttu-id="93103-164">1.0</span><span class="sxs-lookup"><span data-stu-id="93103-164">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="93103-165">参数的名称。</span><span class="sxs-lookup"><span data-stu-id="93103-165">The name of the parameter.</span></span> <span data-ttu-id="93103-166">此项将发送到用户请求中的服务。</span><span class="sxs-lookup"><span data-stu-id="93103-166">This is sent to your service in the user request.</span></span> | <span data-ttu-id="93103-167">是</span><span class="sxs-lookup"><span data-stu-id="93103-167">Yes</span></span> | <span data-ttu-id="93103-168">1.0</span><span class="sxs-lookup"><span data-stu-id="93103-168">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="93103-169">描述了此参数的用途或应提供的值的示例。</span><span class="sxs-lookup"><span data-stu-id="93103-169">Describes this parameter’s purposes or example of the value that should be provided.</span></span> <span data-ttu-id="93103-170">此值显示在 UI 中。</span><span class="sxs-lookup"><span data-stu-id="93103-170">This value appears in the UI.</span></span> | <span data-ttu-id="93103-171">是</span><span class="sxs-lookup"><span data-stu-id="93103-171">Yes</span></span> | <span data-ttu-id="93103-172">1.0</span><span class="sxs-lookup"><span data-stu-id="93103-172">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="93103-173">短用户友好参数标题或标签。</span><span class="sxs-lookup"><span data-stu-id="93103-173">Short user-friendly parameter title or label.</span></span> | <span data-ttu-id="93103-174">是</span><span class="sxs-lookup"><span data-stu-id="93103-174">Yes</span></span> | <span data-ttu-id="93103-175">1.0</span><span class="sxs-lookup"><span data-stu-id="93103-175">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="93103-176">设置为所需的输入类型。</span><span class="sxs-lookup"><span data-stu-id="93103-176">Set to the type of input required.</span></span> <span data-ttu-id="93103-177">可能的值`text`包括`textarea`、 `number`、 `date`、 `time`、 `toggle`、。</span><span class="sxs-lookup"><span data-stu-id="93103-177">Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="93103-178">默认值设置为`text`</span><span class="sxs-lookup"><span data-stu-id="93103-178">Default is set to `text`</span></span> | <span data-ttu-id="93103-179">否</span><span class="sxs-lookup"><span data-stu-id="93103-179">No</span></span> | <span data-ttu-id="93103-180">1.4</span><span class="sxs-lookup"><span data-stu-id="93103-180">1.4</span></span> |

#### <a name="app-manifest-example"></a><span data-ttu-id="93103-181">应用部件清单示例</span><span class="sxs-lookup"><span data-stu-id="93103-181">App manifest example</span></span>

<span data-ttu-id="93103-182">下面是定义搜索命令的`composeExtensions`对象的一个示例。</span><span class="sxs-lookup"><span data-stu-id="93103-182">The below is an example of a `composeExtensions` object defining a search command.</span></span> <span data-ttu-id="93103-183">这不是完整清单的完整清单示例，请参阅：[应用程序清单架构](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="93103-183">It is not an example of the complete manifest, for the full app manifest schema see: [App manifest schema](~/resources/schema/manifest-schema.md).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="93103-184">后续步骤</span><span class="sxs-lookup"><span data-stu-id="93103-184">Next steps</span></span>

<span data-ttu-id="93103-185">现在您已经添加了搜索命令，您需要[处理搜索请求](~/messaging-extensions/how-to/search-commands/respond-to-search.md)。</span><span class="sxs-lookup"><span data-stu-id="93103-185">Now that you've added your search command, you'll need to [handle the search request](~/messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]