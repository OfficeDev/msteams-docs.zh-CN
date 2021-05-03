---
title: 定义消息传递扩展搜索命令
author: clearab
description: 为应用程序定义消息传递扩展Microsoft Teams命令。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 19f1fdf7bd4efdbb0de11d1abad341ec24bc27bd
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696787"
---
# <a name="define-messaging-extension-search-commands"></a><span data-ttu-id="5df49-103">定义消息传递扩展搜索命令</span><span class="sxs-lookup"><span data-stu-id="5df49-103">Define messaging extension search commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="5df49-104">邮件扩展搜索命令允许用户搜索外部系统，并将该搜索的结果插入卡片形式的邮件中。</span><span class="sxs-lookup"><span data-stu-id="5df49-104">Messaging extension search commands allow users to search external systems and insert the results of that search into a message in the form of a card.</span></span> <span data-ttu-id="5df49-105">本文档指导您如何选择搜索命令调用位置，以及将搜索命令添加到应用清单。</span><span class="sxs-lookup"><span data-stu-id="5df49-105">This document guides you on how to select  search command invoke locations, and add the search command to your app manifest.</span></span>

> [!NOTE]
> <span data-ttu-id="5df49-106">结果卡大小限制为 28 KB。</span><span class="sxs-lookup"><span data-stu-id="5df49-106">The result card size limit is 28 KB.</span></span> <span data-ttu-id="5df49-107">如果卡的大小超过 28 KB，则不发送该卡。</span><span class="sxs-lookup"><span data-stu-id="5df49-107">The card is not sent if its size exceeds 28 KB.</span></span>

## <a name="select-search-command-invoke-locations"></a><span data-ttu-id="5df49-108">选择搜索命令调用位置</span><span class="sxs-lookup"><span data-stu-id="5df49-108">Select search command invoke locations</span></span>

<span data-ttu-id="5df49-109">从以下任一位置或两个位置调用搜索命令：</span><span class="sxs-lookup"><span data-stu-id="5df49-109">The search command is invoked from any one or both of the following locations:</span></span>

* <span data-ttu-id="5df49-110">撰写邮件区域：撰写邮件区域底部的按钮。</span><span class="sxs-lookup"><span data-stu-id="5df49-110">Compose message area: The buttons at the bottom of the compose message area.</span></span>
* <span data-ttu-id="5df49-111">命令框：@mentioning命令框中显示。</span><span class="sxs-lookup"><span data-stu-id="5df49-111">Command box: By @mentioning in the command box.</span></span>

<span data-ttu-id="5df49-112">从撰写邮件区域调用搜索命令时，用户将结果发送到对话。</span><span class="sxs-lookup"><span data-stu-id="5df49-112">When search command is invoked from the compose message area, the user sends the results to the conversation.</span></span> <span data-ttu-id="5df49-113">从命令框调用它时，用户与生成的卡片交互，或复制该卡片以在其他地方使用。</span><span class="sxs-lookup"><span data-stu-id="5df49-113">When it is invoked from the command box, the user interacts with the resulting card, or copies it for use elsewhere.</span></span>

<span data-ttu-id="5df49-114">下图显示了搜索命令的调用位置：</span><span class="sxs-lookup"><span data-stu-id="5df49-114">The following image displays the invoke locations of the search command:</span></span>

![搜索命令调用位置](~/assets/images/messaging-extension/search-command-invoke-locations.png)

## <a name="add-the-search-command-to-your-app-manifest"></a><span data-ttu-id="5df49-116">将搜索命令添加到应用清单</span><span class="sxs-lookup"><span data-stu-id="5df49-116">Add the search command to your app manifest</span></span>

<span data-ttu-id="5df49-117">若要将搜索命令添加到应用清单，必须将新对象添加到应用清单 `composeExtension` JSON 的顶层。</span><span class="sxs-lookup"><span data-stu-id="5df49-117">To add the search command to your app manifest, you must add a new `composeExtension` object to the top level of your app manifest JSON.</span></span> <span data-ttu-id="5df49-118">可以在 App Studio 的帮助下或手动添加搜索命令。</span><span class="sxs-lookup"><span data-stu-id="5df49-118">You can add the search command either with the help of App Studio, or manually.</span></span>

### <a name="create-a-search-command-using-app-studio"></a><span data-ttu-id="5df49-119">使用 App Studio 创建搜索命令</span><span class="sxs-lookup"><span data-stu-id="5df49-119">Create a search command using App Studio</span></span>

<span data-ttu-id="5df49-120">创建搜索命令的先决条件是，必须已创建邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="5df49-120">The prerequisite to create a search command is that you must already have created a messaging extension.</span></span> <span data-ttu-id="5df49-121">若要了解如何创建邮件扩展，请参阅创建 [邮件扩展](~/messaging-extensions/how-to/create-messaging-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="5df49-121">For information on how to create a messaging extension, see [create a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

<span data-ttu-id="5df49-122">**创建搜索命令**</span><span class="sxs-lookup"><span data-stu-id="5df49-122">**To create a search command**</span></span>

1. <span data-ttu-id="5df49-123">从 **客户端** 打开 App Studio Microsoft Teams，然后选择"**清单编辑器"** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="5df49-123">Open **App Studio** from the Microsoft Teams client, and select the **Manifest Editor** tab.</span></span>
1.  <span data-ttu-id="5df49-124">如果你已在 **App Studio** 中创建应用包，请从列表中选择。</span><span class="sxs-lookup"><span data-stu-id="5df49-124">If you already created your app package in **App Studio**, select from the list.</span></span> <span data-ttu-id="5df49-125">如果尚未创建应用包，请导入现有应用包。</span><span class="sxs-lookup"><span data-stu-id="5df49-125">If you have not created an app package, import an existing one.</span></span>
1. <span data-ttu-id="5df49-126">导入应用包后，选择 **功能下的** 消息传递 **扩展**。</span><span class="sxs-lookup"><span data-stu-id="5df49-126">After importing app package, select **Messaging extensions** under **Capabilities**.</span></span> <span data-ttu-id="5df49-127">你获得一个弹出窗口来设置邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="5df49-127">You get a pop-up window to set up the messaging extension.</span></span>
1. <span data-ttu-id="5df49-128">选择 **窗口中** 的"设置"，将消息传递扩展包括在你的应用体验中。</span><span class="sxs-lookup"><span data-stu-id="5df49-128">Select **Set up** in the window to include the messaging extension in your app experience.</span></span> <span data-ttu-id="5df49-129">下图显示了邮件扩展设置页面：</span><span class="sxs-lookup"><span data-stu-id="5df49-129">The following image displays the messaging extension set up page:</span></span> 

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>

1. <span data-ttu-id="5df49-130">若要创建消息扩展，你需要一个 Microsoft 注册的自动程序。</span><span class="sxs-lookup"><span data-stu-id="5df49-130">To create the messaging extension, you need a Microsoft registered bot.</span></span> <span data-ttu-id="5df49-131">可以使用现有自动程序或创建新的自动程序。</span><span class="sxs-lookup"><span data-stu-id="5df49-131">You can either use an existing bot or create a new bot.</span></span> <span data-ttu-id="5df49-132">选择 **"创建新自动程序**"选项，为新的自动程序命名，然后选择"创建 **"。**</span><span class="sxs-lookup"><span data-stu-id="5df49-132">Select **Create new bot** option, give a name for the new bot, and select **Create**.</span></span> <span data-ttu-id="5df49-133">下图显示了邮件扩展的自动程序创建：</span><span class="sxs-lookup"><span data-stu-id="5df49-133">The following image displays bot creation for messaging extension:</span></span>

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. <span data-ttu-id="5df49-134">选择 **"** 邮件扩展 **"** 页的"命令"部分中的"添加"，以包含决定邮件扩展行为的命令。</span><span class="sxs-lookup"><span data-stu-id="5df49-134">Select **Add** in the **Command section** of the messaging extensions page to include the commands which decides the behaviour of messaging extension.</span></span>   
<span data-ttu-id="5df49-135">下图显示了邮件扩展的命令添加：</span><span class="sxs-lookup"><span data-stu-id="5df49-135">The following image displays command addition for messaging extension:</span></span>

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>
1. <span data-ttu-id="5df49-136">选择 **"允许用户查询服务信息"，并将其插入到消息中**。</span><span class="sxs-lookup"><span data-stu-id="5df49-136">Select **Allow users to query your service for information and insert that into a message**.</span></span> <span data-ttu-id="5df49-137">下图显示了搜索命令参数选择：</span><span class="sxs-lookup"><span data-stu-id="5df49-137">The following image displays the search command parameter selection:</span></span>

    <img src="~/assets/images/messaging-extension/search-command-parameter-selection.png" alt="search command parameter selection" width="500"/>

1. <span data-ttu-id="5df49-138">添加命令 **ID** 和 **标题**。</span><span class="sxs-lookup"><span data-stu-id="5df49-138">Add a **Command Id** and a **Title**.</span></span>
1. <span data-ttu-id="5df49-139">选择必须调用搜索命令的位置。</span><span class="sxs-lookup"><span data-stu-id="5df49-139">Select the location from where your search command must be invoked.</span></span> <span data-ttu-id="5df49-140">选择 **邮件** 当前不会更改搜索命令的行为。</span><span class="sxs-lookup"><span data-stu-id="5df49-140">Selecting **message** does not currently alter the behavior of your search command.</span></span> <span data-ttu-id="5df49-141">下图显示了搜索命令调用位置：</span><span class="sxs-lookup"><span data-stu-id="5df49-141">The following image displays the search command invoke location:</span></span>

    <img src="~/assets/images/messaging-extension/search-command-invoke-location-selection.png" alt="search command invoke location selection]" width="500"/>

1. <span data-ttu-id="5df49-142">添加搜索参数，然后选择"保存 **"。**</span><span class="sxs-lookup"><span data-stu-id="5df49-142">Add your search parameter and select **Save**.</span></span>

### <a name="create-a-search-command-manually"></a><span data-ttu-id="5df49-143">手动创建搜索命令</span><span class="sxs-lookup"><span data-stu-id="5df49-143">Create a search command manually</span></span> 

<span data-ttu-id="5df49-144">若要将邮件扩展搜索命令手动添加到应用清单，必须将以下参数添加到 `composeExtension.commands` 对象数组：</span><span class="sxs-lookup"><span data-stu-id="5df49-144">To manually add your messaging extension search command to your app manifest, you must add the following parameters to your `composeExtension.commands` array of objects:</span></span>

| <span data-ttu-id="5df49-145">属性名称</span><span class="sxs-lookup"><span data-stu-id="5df49-145">Property name</span></span> | <span data-ttu-id="5df49-146">用途</span><span class="sxs-lookup"><span data-stu-id="5df49-146">Purpose</span></span> | <span data-ttu-id="5df49-147">是否必需？</span><span class="sxs-lookup"><span data-stu-id="5df49-147">Required?</span></span> | <span data-ttu-id="5df49-148">最低清单版本</span><span class="sxs-lookup"><span data-stu-id="5df49-148">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="5df49-149">此属性是分配给搜索命令的唯一 ID。</span><span class="sxs-lookup"><span data-stu-id="5df49-149">This property is an unique ID that you assign to search command.</span></span> <span data-ttu-id="5df49-150">用户请求包括此 ID。</span><span class="sxs-lookup"><span data-stu-id="5df49-150">The user request includes this ID.</span></span> | <span data-ttu-id="5df49-151">是</span><span class="sxs-lookup"><span data-stu-id="5df49-151">Yes</span></span> | <span data-ttu-id="5df49-152">1.0</span><span class="sxs-lookup"><span data-stu-id="5df49-152">1.0</span></span> |
| `title` | <span data-ttu-id="5df49-153">此属性是命令名称。</span><span class="sxs-lookup"><span data-stu-id="5df49-153">This property is a command name.</span></span> <span data-ttu-id="5df49-154">此值显示在用户界面用户界面 (UI) 。</span><span class="sxs-lookup"><span data-stu-id="5df49-154">This value appears in the user interface (UI).</span></span> | <span data-ttu-id="5df49-155">是</span><span class="sxs-lookup"><span data-stu-id="5df49-155">Yes</span></span> | <span data-ttu-id="5df49-156">1.0</span><span class="sxs-lookup"><span data-stu-id="5df49-156">1.0</span></span> |
| `description` | <span data-ttu-id="5df49-157">此属性是一个帮助文本，用于指示此命令执行哪些操作。</span><span class="sxs-lookup"><span data-stu-id="5df49-157">This property is a help text indicating what this command does.</span></span> <span data-ttu-id="5df49-158">此值显示在 UI 中。</span><span class="sxs-lookup"><span data-stu-id="5df49-158">This value appears in the UI.</span></span> | <span data-ttu-id="5df49-159">是</span><span class="sxs-lookup"><span data-stu-id="5df49-159">Yes</span></span> | <span data-ttu-id="5df49-160">1.0</span><span class="sxs-lookup"><span data-stu-id="5df49-160">1.0</span></span> |
| `type` | <span data-ttu-id="5df49-161">此属性必须为 `query` 。</span><span class="sxs-lookup"><span data-stu-id="5df49-161">This property must be a `query`.</span></span> | <span data-ttu-id="5df49-162">否</span><span class="sxs-lookup"><span data-stu-id="5df49-162">No</span></span> | <span data-ttu-id="5df49-163">1.4</span><span class="sxs-lookup"><span data-stu-id="5df49-163">1.4</span></span> |
|`initialRun` | <span data-ttu-id="5df49-164">如果此属性设置为 **true**，则指示用户一旦在 UI 中选择此命令，就应执行此命令。</span><span class="sxs-lookup"><span data-stu-id="5df49-164">If this property is set to **true**, it indicates this command should be executed as soon as the user selects this command in the UI.</span></span> | <span data-ttu-id="5df49-165">否</span><span class="sxs-lookup"><span data-stu-id="5df49-165">No</span></span> | <span data-ttu-id="5df49-166">1.0</span><span class="sxs-lookup"><span data-stu-id="5df49-166">1.0</span></span> |
| `context` | <span data-ttu-id="5df49-167">此属性是一个可选的值数组，用于定义搜索操作可用的上下文。</span><span class="sxs-lookup"><span data-stu-id="5df49-167">This property is an optional array of values that defines the context the search action is available in.</span></span> <span data-ttu-id="5df49-168">可取值包括 `message`、`compose` 或 `commandBox`。</span><span class="sxs-lookup"><span data-stu-id="5df49-168">The possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="5df49-169">默认值为 `["compose", "commandBox"]`。</span><span class="sxs-lookup"><span data-stu-id="5df49-169">The default is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="5df49-170">否</span><span class="sxs-lookup"><span data-stu-id="5df49-170">No</span></span> | <span data-ttu-id="5df49-171">1.5</span><span class="sxs-lookup"><span data-stu-id="5df49-171">1.5</span></span> |

<span data-ttu-id="5df49-172">您必须添加搜索参数的详细信息，该参数定义您的用户在 Teams 客户端中可见的文本。</span><span class="sxs-lookup"><span data-stu-id="5df49-172">You must add the details of the search parameter, that defines the text visible to your user in the Teams client.</span></span>

| <span data-ttu-id="5df49-173">属性名称</span><span class="sxs-lookup"><span data-stu-id="5df49-173">Property name</span></span> | <span data-ttu-id="5df49-174">用途</span><span class="sxs-lookup"><span data-stu-id="5df49-174">Purpose</span></span> | <span data-ttu-id="5df49-175">是否必需？</span><span class="sxs-lookup"><span data-stu-id="5df49-175">Is required?</span></span> | <span data-ttu-id="5df49-176">最低清单版本</span><span class="sxs-lookup"><span data-stu-id="5df49-176">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="5df49-177">此属性定义命令的参数静态列表。</span><span class="sxs-lookup"><span data-stu-id="5df49-177">This property defines a static list of parameters for the command.</span></span> | <span data-ttu-id="5df49-178">否</span><span class="sxs-lookup"><span data-stu-id="5df49-178">No</span></span> | <span data-ttu-id="5df49-179">1.0</span><span class="sxs-lookup"><span data-stu-id="5df49-179">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="5df49-180">此属性描述参数的名称。</span><span class="sxs-lookup"><span data-stu-id="5df49-180">This property describes the name of the parameter.</span></span> <span data-ttu-id="5df49-181">这将在用户请求中发送到你的服务。</span><span class="sxs-lookup"><span data-stu-id="5df49-181">This is sent to your service in the user request.</span></span> | <span data-ttu-id="5df49-182">是</span><span class="sxs-lookup"><span data-stu-id="5df49-182">Yes</span></span> | <span data-ttu-id="5df49-183">1.0</span><span class="sxs-lookup"><span data-stu-id="5df49-183">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="5df49-184">此属性描述参数的用途或必须提供的值示例。</span><span class="sxs-lookup"><span data-stu-id="5df49-184">This property describes the parameter’s purposes or example of the value that must be provided.</span></span> <span data-ttu-id="5df49-185">此值显示在 UI 中。</span><span class="sxs-lookup"><span data-stu-id="5df49-185">This value appears in the UI.</span></span> | <span data-ttu-id="5df49-186">是</span><span class="sxs-lookup"><span data-stu-id="5df49-186">Yes</span></span> | <span data-ttu-id="5df49-187">1.0</span><span class="sxs-lookup"><span data-stu-id="5df49-187">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="5df49-188">此属性是一个简短的用户友好参数标题或标签。</span><span class="sxs-lookup"><span data-stu-id="5df49-188">This property is a short user-friendly parameter title or label.</span></span> | <span data-ttu-id="5df49-189">是</span><span class="sxs-lookup"><span data-stu-id="5df49-189">Yes</span></span> | <span data-ttu-id="5df49-190">1.0</span><span class="sxs-lookup"><span data-stu-id="5df49-190">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="5df49-191">此属性设置为所需输入的类型。</span><span class="sxs-lookup"><span data-stu-id="5df49-191">This property is set to the type of the input required.</span></span> <span data-ttu-id="5df49-192">可能的值包括 `text` `textarea` `number` 、、、、、。 `date` `time` `toggle`</span><span class="sxs-lookup"><span data-stu-id="5df49-192">Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="5df49-193">默认值设置为 `text` 。</span><span class="sxs-lookup"><span data-stu-id="5df49-193">Default is set to `text`.</span></span> | <span data-ttu-id="5df49-194">否</span><span class="sxs-lookup"><span data-stu-id="5df49-194">No</span></span> | <span data-ttu-id="5df49-195">1.4</span><span class="sxs-lookup"><span data-stu-id="5df49-195">1.4</span></span> |

#### <a name="example"></a><span data-ttu-id="5df49-196">示例</span><span class="sxs-lookup"><span data-stu-id="5df49-196">Example</span></span>

<span data-ttu-id="5df49-197">以下部分是定义搜索命令的对象的简单应用 `composeExtensions` 清单的示例：</span><span class="sxs-lookup"><span data-stu-id="5df49-197">Following section is an example of the simple app manifest of the `composeExtensions` object defining a search command:</span></span> 

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
<span data-ttu-id="5df49-198">有关完整的应用清单，请参阅 [应用清单架构](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="5df49-198">For the complete app manifest, see [App manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="code-sample"></a><span data-ttu-id="5df49-199">代码示例</span><span class="sxs-lookup"><span data-stu-id="5df49-199">Code sample</span></span>

| <span data-ttu-id="5df49-200">示例名称</span><span class="sxs-lookup"><span data-stu-id="5df49-200">Sample Name</span></span>           | <span data-ttu-id="5df49-201">说明</span><span class="sxs-lookup"><span data-stu-id="5df49-201">Description</span></span> | <span data-ttu-id="5df49-202">.NET</span><span class="sxs-lookup"><span data-stu-id="5df49-202">.NET</span></span>    | <span data-ttu-id="5df49-203">Node.js</span><span class="sxs-lookup"><span data-stu-id="5df49-203">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="5df49-204">Teams邮件扩展操作</span><span class="sxs-lookup"><span data-stu-id="5df49-204">Teams messaging extension action</span></span>| <span data-ttu-id="5df49-205">介绍如何定义操作命令、创建任务模块和响应任务模块提交操作。</span><span class="sxs-lookup"><span data-stu-id="5df49-205">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="5df49-206">View</span><span class="sxs-lookup"><span data-stu-id="5df49-206">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="5df49-207">View</span><span class="sxs-lookup"><span data-stu-id="5df49-207">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="5df49-208">Teams邮件扩展搜索</span><span class="sxs-lookup"><span data-stu-id="5df49-208">Teams messaging extension search</span></span>   |  <span data-ttu-id="5df49-209">介绍如何定义搜索命令并响应搜索。</span><span class="sxs-lookup"><span data-stu-id="5df49-209">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="5df49-210">View</span><span class="sxs-lookup"><span data-stu-id="5df49-210">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="5df49-211">View</span><span class="sxs-lookup"><span data-stu-id="5df49-211">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a><span data-ttu-id="5df49-212">后续步骤</span><span class="sxs-lookup"><span data-stu-id="5df49-212">Next step</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="5df49-213">[响应搜索命令](~/messaging-extensions/how-to/search-commands/respond-to-search.md)。</span><span class="sxs-lookup"><span data-stu-id="5df49-213">[Respond to the search commands](~/messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

