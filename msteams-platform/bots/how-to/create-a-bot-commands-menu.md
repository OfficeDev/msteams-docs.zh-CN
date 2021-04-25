---
title: 为自动程序创建命令菜单
author: clearab
description: 如何为 Microsoft Teams 自动程序创建命令菜单
ms.topic: how-to
ms.author: anclear
ms.openlocfilehash: a4d53d8287d425120d24f559b8ffffabebdbcfb4
ms.sourcegitcommit: dd2220f691029d043aaddfc7c229e332735acb1d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2021
ms.locfileid: "51995895"
---
# <a name="bot-command-menus"></a><span data-ttu-id="5d40d-103">自动程序命令菜单</span><span class="sxs-lookup"><span data-stu-id="5d40d-103">Bot command menus</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

> [!Note]
> <span data-ttu-id="5d40d-104">自动程序菜单不显示在移动客户端上。</span><span class="sxs-lookup"><span data-stu-id="5d40d-104">Bot menus do not appear on mobile clients.</span></span>

<span data-ttu-id="5d40d-105">若要定义自动程序可以响应的核心命令集，你可以添加一个命令菜单以及自动程序命令的下拉列表。</span><span class="sxs-lookup"><span data-stu-id="5d40d-105">To define a set of core commands that your bot can respond to, you can add a command menu with a drop-down list of commands for your bot.</span></span> <span data-ttu-id="5d40d-106">当用户与自动程序对话时，将在撰写邮件区域中显示命令列表。</span><span class="sxs-lookup"><span data-stu-id="5d40d-106">The list of commands is presented to the users in the compose message area when they are in conversation with your bot.</span></span> <span data-ttu-id="5d40d-107">Select a command from the list to insert the command string into the compose message box and select **Send**.</span><span class="sxs-lookup"><span data-stu-id="5d40d-107">Select a command from the list to insert the command string into the compose message box and select **Send**.</span></span>

![自动程序命令菜单](./conversations/media/bot-menu-sample.png)

## <a name="create-a-command-menu-for-your-bot"></a><span data-ttu-id="5d40d-109">为自动程序创建命令菜单</span><span class="sxs-lookup"><span data-stu-id="5d40d-109">Create a command menu for your bot</span></span>

<span data-ttu-id="5d40d-110">命令菜单在应用清单中定义。</span><span class="sxs-lookup"><span data-stu-id="5d40d-110">Command menus are defined in your app manifest.</span></span> <span data-ttu-id="5d40d-111">可以使用 App **Studio 创建** 它们，或在应用清单中手动添加它们。</span><span class="sxs-lookup"><span data-stu-id="5d40d-111">You can either use **App Studio** to create them or add them manually in the app manifest.</span></span>

### <a name="create-a-command-menu-for-your-bot-using-app-studio"></a><span data-ttu-id="5d40d-112">使用 App Studio 为机器人创建命令菜单</span><span class="sxs-lookup"><span data-stu-id="5d40d-112">Create a command menu for your bot using App Studio</span></span>

<span data-ttu-id="5d40d-113">为自动程序创建命令菜单的先决条件是必须编辑现有应用清单。</span><span class="sxs-lookup"><span data-stu-id="5d40d-113">A prerequisite to create a command menu for your bot is that you must edit an existing app manifest.</span></span> <span data-ttu-id="5d40d-114">无论是创建新清单还是编辑现有清单，添加命令菜单的步骤都是相同的。</span><span class="sxs-lookup"><span data-stu-id="5d40d-114">The steps to add a command menu are the same, whether you create a new manifest or edit an existing one.</span></span>

<span data-ttu-id="5d40d-115">**使用 App Studio 为机器人创建命令菜单**</span><span class="sxs-lookup"><span data-stu-id="5d40d-115">**To create a command menu for your bot using App Studio**</span></span>

1. <span data-ttu-id="5d40d-116">打开 **Teams，然后** 从左窗格中选择"应用"。</span><span class="sxs-lookup"><span data-stu-id="5d40d-116">Open Teams and select **Apps** from the left pane.</span></span> <span data-ttu-id="5d40d-117">在"**应用"** 页中，搜索 **App Studio，** 然后选择"打开 **"。**</span><span class="sxs-lookup"><span data-stu-id="5d40d-117">In the **Apps** page, search for **App Studio**, and select **Open**.</span></span> 
   > [!NOTE]
   > <span data-ttu-id="5d40d-118">如果你没有 **App Studio，** 可以下载它。</span><span class="sxs-lookup"><span data-stu-id="5d40d-118">If you do not have **App Studio**, you can download it.</span></span> <span data-ttu-id="5d40d-119">有关详细信息，请参阅安装[App Studio。](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio)</span><span class="sxs-lookup"><span data-stu-id="5d40d-119">For more information, see [installing App Studio](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio).</span></span>

    ![应用程序 Studio](./conversations/media/AppStudio.png)

2. <span data-ttu-id="5d40d-121">在 **App Studio** 中，选择 **"清单编辑器"** 选项卡。如果你没有现有应用包，可以创建或导入现有应用。</span><span class="sxs-lookup"><span data-stu-id="5d40d-121">In **App Studio**, select the **Manifest editor** tab. If you do not have an existing app package, you can create or import an existing app.</span></span> <span data-ttu-id="5d40d-122">有关详细信息，请参阅 [更新应用包](~/tutorials/get-started-dotnet-app-studio.md#use-app-studio-to-update-the-app-package)。</span><span class="sxs-lookup"><span data-stu-id="5d40d-122">For more information, see [update an app package](~/tutorials/get-started-dotnet-app-studio.md#use-app-studio-to-update-the-app-package).</span></span>

3. <span data-ttu-id="5d40d-123">在清单编辑器的左侧 **窗格中的**"功能"部分，选择"**自动程序"。**</span><span class="sxs-lookup"><span data-stu-id="5d40d-123">In the left pane of the **Manifest editor** and in the **Capabilities** section, select **Bots**.</span></span>

4. <span data-ttu-id="5d40d-124">在清单编辑器的右侧 **窗格中的**"命令"部分 **，选择**"添加 **"。**</span><span class="sxs-lookup"><span data-stu-id="5d40d-124">In the right pane of the **Manifest editor** and in the **Commands** section, select **Add**.</span></span> <span data-ttu-id="5d40d-125">将显示 **"新建命令** "屏幕。</span><span class="sxs-lookup"><span data-stu-id="5d40d-125">The **New Command** screen appears.</span></span>

    ![App Studio 命令菜单添加按钮](./conversations/media/AppStudio-CommandMenu-Add.png)

5. <span data-ttu-id="5d40d-127">输入 **命令文本** ，该文本必须显示为自动程序的命令菜单。</span><span class="sxs-lookup"><span data-stu-id="5d40d-127">Enter the **Command text** that must appear as the command menu for your bot.</span></span>

6. <span data-ttu-id="5d40d-128">输入 **必须在菜单中** 的命令文本下显示的帮助文本。</span><span class="sxs-lookup"><span data-stu-id="5d40d-128">Enter the **Help text** that must appear under the command text in the menu.</span></span> <span data-ttu-id="5d40d-129">**帮助文本** 必须是命令用途的简要说明。</span><span class="sxs-lookup"><span data-stu-id="5d40d-129">**Help text** must be a brief explanation of the purpose of the command.</span></span>

7. <span data-ttu-id="5d40d-130">选中"**范围**"复选框以选择此命令菜单必须显示在何处，然后选择"保存 **"。**</span><span class="sxs-lookup"><span data-stu-id="5d40d-130">Select the **Scope** check boxes to select where this command menu must appear, and select **Save**.</span></span>

    ![App Studio 新命令菜单按钮](./conversations/media/AppStudio-NewCommandMenu.png)

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a><span data-ttu-id="5d40d-132">通过编辑"打开"菜单为自动程序Manifest.js菜单</span><span class="sxs-lookup"><span data-stu-id="5d40d-132">Create a command menu for your bot by editing Manifest.json</span></span>

<span data-ttu-id="5d40d-133">创建命令菜单的另一种方式是在开发自动程序源代码时直接在清单文件中创建它。</span><span class="sxs-lookup"><span data-stu-id="5d40d-133">Another way to create a command menu is to create it directly in the manifest file while developing your bot source code.</span></span> <span data-ttu-id="5d40d-134">若要使用此方法，请遵循以下几点：</span><span class="sxs-lookup"><span data-stu-id="5d40d-134">To use this method, follow these points:</span></span>

* <span data-ttu-id="5d40d-135">每个菜单最多支持 10 个命令。</span><span class="sxs-lookup"><span data-stu-id="5d40d-135">Each menu supports up to ten commands.</span></span>
* <span data-ttu-id="5d40d-136">创建在所有范围内工作的单个命令菜单。</span><span class="sxs-lookup"><span data-stu-id="5d40d-136">Create a single command menu that works in all scopes.</span></span>
* <span data-ttu-id="5d40d-137">为每个范围创建不同的命令菜单。</span><span class="sxs-lookup"><span data-stu-id="5d40d-137">Create a different command menu for each scope.</span></span>

#### <a name="manifest-example-for-single-menu-for-both-scopes"></a><span data-ttu-id="5d40d-138">两个作用域的单个菜单的清单示例</span><span class="sxs-lookup"><span data-stu-id="5d40d-138">Manifest example for single menu for both scopes</span></span>

<span data-ttu-id="5d40d-139">两个作用域的单个菜单的清单示例代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="5d40d-139">The manifest example code for single menu for both scopes is as follows:</span></span>

```json
{
  ⋮
  "bots":[
    {
      "botId":"[Microsoft App ID for your bot]",
      "scopes": [
        "personal",
        "team"
      ],
      "commandLists":[
        {
          "scopes":[
            "team",
            "personal"
          ],
          "commands":[
            {
              "title":"Help",
              "description":"Displays this help message"
            },
            {
              "title":"Search Flights",
              "description":"Search flights from Seattle to Phoenix May 2-5 departing after 3pm"
            },
            {
              "title":"Search Hotels",
              "description":"Search hotels in Portland tonight"
            },
            {
              "title":"Best Time to Fly",
              "description":"Best time to fly to London for a 5 day trip this summer"
            }
          ]
        }
      ]
    }
  ],
  ...
}
```

#### <a name="manifest-example-for-the-menu-for-each-scope"></a><span data-ttu-id="5d40d-140">每个范围的菜单的清单示例</span><span class="sxs-lookup"><span data-stu-id="5d40d-140">Manifest example for the menu for each scope</span></span>

<span data-ttu-id="5d40d-141">每个范围的菜单的清单示例代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="5d40d-141">The manifest example code for the menu for each scope is as follows:</span></span>

```json
{
  ...
  "bots":[
    {
      "botId":"<Microsoft app ID for your bot>",
      "scopes": [
        "groupChat",
        "team"
      ],
      "commandLists":[
        {
          "scopes":[
            "team"
          ],
          "commands":[
            {
            "title":"help",
            "description":"Displays this help message for channels"
            }
          ]
        },
        {
          "scopes":[
            "groupChat"
          ],
          "commands":[
            {
            "title":"help",
            "description":"Displays this help message for group chat"
            }
          ]
        }
      ]
    }
  ],
  ...
}
```

<span data-ttu-id="5d40d-142">处理来自用户的任何消息时，必须在自动程序代码中处理菜单命令。</span><span class="sxs-lookup"><span data-stu-id="5d40d-142">You must handle menu commands in your bot code as you handle any message from users.</span></span> <span data-ttu-id="5d40d-143">可以通过解析邮件文本的"提及"部分来处理自动程序 **\@ 代码中** 的菜单命令。</span><span class="sxs-lookup"><span data-stu-id="5d40d-143">You can handle menu commands in your bot code by parsing out the **\@Mention** portion of the message text.</span></span>

## <a name="handle-menu-commands-in-your-bot-code"></a><span data-ttu-id="5d40d-144">处理自动程序代码中的菜单命令</span><span class="sxs-lookup"><span data-stu-id="5d40d-144">Handle menu commands in your bot code</span></span>

<span data-ttu-id="5d40d-145">组或频道中的机器人仅在消息中提到时 `@botname` 进行响应。</span><span class="sxs-lookup"><span data-stu-id="5d40d-145">Bots in a group or channel respond only when they are mentioned `@botname` in a message.</span></span> <span data-ttu-id="5d40d-146">自动程序在组或频道范围中收到的每封邮件在返回的消息文本中包含其名称。</span><span class="sxs-lookup"><span data-stu-id="5d40d-146">Every message received by a bot when in a group or channel scope contains its name in the message text returned.</span></span> <span data-ttu-id="5d40d-147">在处理返回的命令之前，邮件分析必须处理自动程序使用其名称接收的消息。</span><span class="sxs-lookup"><span data-stu-id="5d40d-147">Before handling the command being returned, your message parsing must handle the message received by a bot with its name.</span></span>

> [!NOTE]
> <span data-ttu-id="5d40d-148">若要在代码中处理命令，它们作为常规消息发送到自动程序。</span><span class="sxs-lookup"><span data-stu-id="5d40d-148">To handle the commands in code, they are sent to your bot as a regular message.</span></span> <span data-ttu-id="5d40d-149">必须像处理用户发送的其他任何邮件一样处理邮件。</span><span class="sxs-lookup"><span data-stu-id="5d40d-149">You must handle them as you would handle any other message from your users.</span></span> <span data-ttu-id="5d40d-150">代码中的命令在文本框中插入预配置的文本。</span><span class="sxs-lookup"><span data-stu-id="5d40d-150">The commands in code insert pre-configured text into the text box.</span></span> <span data-ttu-id="5d40d-151">然后，用户必须像发送任何其他邮件一样发送该文本。</span><span class="sxs-lookup"><span data-stu-id="5d40d-151">The user must then send that text as they do for any other message.</span></span>

# <a name="c"></a>[<span data-ttu-id="5d40d-152">C#</span><span class="sxs-lookup"><span data-stu-id="5d40d-152">C#</span></span>](#tab/dotnet)

<span data-ttu-id="5d40d-153">可以使用 Microsoft Bot Framework 提供的静态方法分析邮件文本的 **\@ "** 提及"部分。</span><span class="sxs-lookup"><span data-stu-id="5d40d-153">You can parse out the **\@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework.</span></span> <span data-ttu-id="5d40d-154">它是名为 的 `Activity` 类的一个方法 `RemoveRecipientMention` 。</span><span class="sxs-lookup"><span data-stu-id="5d40d-154">It is a method of the `Activity` class named `RemoveRecipientMention`.</span></span>

<span data-ttu-id="5d40d-155">用于C#"提及"部分的代码如下所示： **\@**</span><span class="sxs-lookup"><span data-stu-id="5d40d-155">The C# code to parse out the **\@Mention** portion of the message text is as follows:</span></span>

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascript"></a>[<span data-ttu-id="5d40d-156">JavaScript</span><span class="sxs-lookup"><span data-stu-id="5d40d-156">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="5d40d-157">可以使用自动程序框架提供的静态 **\@** 方法分析邮件文本的"提及"部分。</span><span class="sxs-lookup"><span data-stu-id="5d40d-157">You can parse out the **\@Mention** portion of the message text using a static method provided with the Bot Framework.</span></span> <span data-ttu-id="5d40d-158">它是名为 的 `TurnContext` 类的一个方法 `removeMentionText` 。</span><span class="sxs-lookup"><span data-stu-id="5d40d-158">It is a method of the `TurnContext` class named `removeMentionText`.</span></span>

<span data-ttu-id="5d40d-159">用于解析邮件文本的 **\@ "** 提及"部分的 JavaScript 代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="5d40d-159">The JavaScript code to parse out the **\@Mention** portion of the message text is as follows:</span></span>

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[<span data-ttu-id="5d40d-160">Python</span><span class="sxs-lookup"><span data-stu-id="5d40d-160">Python</span></span>](#tab/python)

<span data-ttu-id="5d40d-161">可以使用 Bot Framework **@Mention** 静态方法解析邮件文本的 @Mention 部分。</span><span class="sxs-lookup"><span data-stu-id="5d40d-161">You can parse out the **@Mention** portion of the message text using a static method provided with the Bot Framework.</span></span> <span data-ttu-id="5d40d-162">它是名为 的 `TurnContext` 类的一个方法 `remove_recipient_mention` 。</span><span class="sxs-lookup"><span data-stu-id="5d40d-162">It is a method of the `TurnContext` class named `remove_recipient_mention`.</span></span>

<span data-ttu-id="5d40d-163">用于分析邮件文本的 **\@ "提及**"部分的 Python 代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="5d40d-163">The Python code to parse out the **\@Mention** portion of the message text is as follows:</span></span>

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

<span data-ttu-id="5d40d-164">若要使自动程序代码顺利运行，必须遵循一些最佳做法。</span><span class="sxs-lookup"><span data-stu-id="5d40d-164">To enable smooth functioning of your bot code, there are few best practices that you must follow.</span></span>

## <a name="command-menu-best-practices"></a><span data-ttu-id="5d40d-165">命令菜单最佳实践</span><span class="sxs-lookup"><span data-stu-id="5d40d-165">Command menu best practices</span></span>

<span data-ttu-id="5d40d-166">以下是命令菜单最佳实践：</span><span class="sxs-lookup"><span data-stu-id="5d40d-166">Following are the command menu best practices:</span></span>

* <span data-ttu-id="5d40d-167">保持简单：自动程序菜单旨在显示自动程序的关键功能。</span><span class="sxs-lookup"><span data-stu-id="5d40d-167">Keep it simple: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="5d40d-168">保持简短：菜单选项不能长，不能是复杂的自然语言语句。</span><span class="sxs-lookup"><span data-stu-id="5d40d-168">Keep it short: Menu options must not be long and must not be complex natural language statements.</span></span> <span data-ttu-id="5d40d-169">它们必须是简单的命令。</span><span class="sxs-lookup"><span data-stu-id="5d40d-169">They must be simple commands.</span></span>
* <span data-ttu-id="5d40d-170">保持它可以进行通话：自动程序菜单操作或命令必须始终可用，无论对话的状态或聊天机器人位于哪个对话中。</span><span class="sxs-lookup"><span data-stu-id="5d40d-170">Keep it invokable: Bot menu actions or commands must always be available, regardless of the state of the conversation or the dialog the bot is in.</span></span>

> [!NOTE]
> <span data-ttu-id="5d40d-171">如果从清单中删除任何命令，则必须重新部署应用来实现更改。</span><span class="sxs-lookup"><span data-stu-id="5d40d-171">If you remove any commands from your manifest, you must redeploy your app to implement the changes.</span></span> <span data-ttu-id="5d40d-172">通常，对清单的任何更改都需要重新部署应用。</span><span class="sxs-lookup"><span data-stu-id="5d40d-172">In general, any changes to the manifest require you to redeploy your app.</span></span>

## <a name="next-step"></a><span data-ttu-id="5d40d-173">后续步骤</span><span class="sxs-lookup"><span data-stu-id="5d40d-173">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5d40d-174">频道和群组对话</span><span class="sxs-lookup"><span data-stu-id="5d40d-174">Channel and group conversations</span></span>](~/bots/how-to/conversations/channel-and-group-conversations.md)
