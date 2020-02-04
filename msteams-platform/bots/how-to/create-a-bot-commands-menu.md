---
title: 为你的 bot 创建命令菜单
author: clearab
description: 如何为 Microsoft 团队 bot 创建命令菜单
ms.topic: overview, command menu
ms.author: anclear
ms.openlocfilehash: 81efb94fc882aa4653ab162863d5d973aeae87b9
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673135"
---
# <a name="bot-command-menus"></a><span data-ttu-id="65757-103">Bot 命令菜单</span><span class="sxs-lookup"><span data-stu-id="65757-103">Bot command menus</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

> [!Note]
> <span data-ttu-id="65757-104">移动客户端上不会显示 Bot 菜单。</span><span class="sxs-lookup"><span data-stu-id="65757-104">Bot menus won't appear on mobile clients.</span></span>

<span data-ttu-id="65757-105">通过为你的 bot 添加命令菜单，你可以定义你的 bot 可以始终响应的一组核心命令。</span><span class="sxs-lookup"><span data-stu-id="65757-105">Add command menu for your bot allows you to define a set of core commands your bot can always respond to.</span></span> <span data-ttu-id="65757-106">当用户正在使用你的 bot 时，会向用户显示撰写邮件区域上方的命令列表。</span><span class="sxs-lookup"><span data-stu-id="65757-106">The list of commands is presented to the user above the compose message area when they are conversing with your bot.</span></span> <span data-ttu-id="65757-107">从列表中选择一个命令会将命令字符串插入到撰写消息框中，所有用户都需要选择 "**发送**"。</span><span class="sxs-lookup"><span data-stu-id="65757-107">Selecting a command from the list will insert the command string into the compose message box, then all users need to do is select **Send**.</span></span>

![Bot 命令菜单](./conversations/media/bot-menu-sample.png)

## <a name="create-a-command-menu-for-your-bot"></a><span data-ttu-id="65757-109">为你的 bot 创建命令菜单</span><span class="sxs-lookup"><span data-stu-id="65757-109">Create a command menu for your bot</span></span>

<span data-ttu-id="65757-110">命令菜单在应用部件清单（manifest）中定义。</span><span class="sxs-lookup"><span data-stu-id="65757-110">Command menus are defined in your app manifest.</span></span> <span data-ttu-id="65757-111">您可以使用应用程序 Studio 来帮助您创建它们，也可以手动添加它们。</span><span class="sxs-lookup"><span data-stu-id="65757-111">You can either use App Studio to help you create them, or add them manually.</span></span>

### <a name="creating-a-command-menu-for-your-bot-using-app-studio"></a><span data-ttu-id="65757-112">使用应用程序 Studio 为你的机器人创建命令菜单</span><span class="sxs-lookup"><span data-stu-id="65757-112">Creating a command menu for your bot using App Studio</span></span>

<span data-ttu-id="65757-113">此处的说明假定您将编辑现有的应用程序清单。</span><span class="sxs-lookup"><span data-stu-id="65757-113">The instructions here assume that you'll be editing an existing app manifest.</span></span> <span data-ttu-id="65757-114">无论是创建新的清单还是编辑现有的清单，添加命令菜单的步骤都是相同的。</span><span class="sxs-lookup"><span data-stu-id="65757-114">The steps for adding a command menu are the same, whether you're creating a new manifest or editing an existing one.</span></span>

1. <span data-ttu-id="65757-115">打开应用程序 Studio .。。左侧导航轨上的 "溢出" 菜单。</span><span class="sxs-lookup"><span data-stu-id="65757-115">Open App Studio from the ... overflow menu on the left navigation rail.</span></span> <span data-ttu-id="65757-116">如果你没有可用的应用程序，可以下载。</span><span class="sxs-lookup"><span data-stu-id="65757-116">If you don't have App Studio available you can download it.</span></span> <span data-ttu-id="65757-117">有关使用应用程序 Studio 的详细信息，请参阅[安装应用程序 studio](https://aka.ms/teams-app-studio#installing-app-studio) 。</span><span class="sxs-lookup"><span data-stu-id="65757-117">See [Installing App Studio](https://aka.ms/teams-app-studio#installing-app-studio) for more information on using App Studio.</span></span>

    ![应用程序工作室](./conversations/media/AppStudio.png)

2. <span data-ttu-id="65757-119">在应用程序 Studio 中，选择 "**清单编辑器**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="65757-119">Once in App Studio, select the **Manifest editor** tab.</span></span>

3. <span data-ttu-id="65757-120">在 "**功能**" 部分的 "清单编辑器" 视图的左列中，选择 " **bot**"。</span><span class="sxs-lookup"><span data-stu-id="65757-120">In the left column of the manifest editor view in the **Capabilities** section, select **Bots**.</span></span>

4. <span data-ttu-id="65757-121">在清单编辑器视图的右列中的 "**命令**" 部分，选择 "**添加**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="65757-121">In the right column of the manifest editor view in the **Commands** section, select the **Add** button.</span></span>

    ![应用程序 Studio 命令菜单添加按钮](./conversations/media/AppStudio-CommandMenu-Add.png)

5. <span data-ttu-id="65757-123">将显示**新的命令**屏幕。</span><span class="sxs-lookup"><span data-stu-id="65757-123">The **New Command** screen appears.</span></span> <span data-ttu-id="65757-124">输入要显示为菜单命令的**命令文本**，以及要在菜单中的命令文本正下方显示的 "**帮助" 文本**。</span><span class="sxs-lookup"><span data-stu-id="65757-124">Enter the **Command text** that you want to have appear as the menu command, and the **Help text** that you want to have appear directly under the command text in the menu.</span></span> <span data-ttu-id="65757-125">这应该是命令用途的简短说明。</span><span class="sxs-lookup"><span data-stu-id="65757-125">This should be a brief explanation of the purpose of the command.</span></span>

6. <span data-ttu-id="65757-126">接下来，选择要在其中显示此命令菜单的范围，然后选择 "**保存**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="65757-126">Next, select the scope(s) where you want this command menu to appear, then select the **Save** button.</span></span>

    ![应用程序 Studio 命令菜单添加按钮](./conversations/media/AppStudio-NewCommandMenu.png)

### <a name="creating-a-command-menu-for-your-bot-by-editing-manifestjson"></a><span data-ttu-id="65757-128">通过编辑 Manifest 创建用于你的 bot 的命令菜单**json**</span><span class="sxs-lookup"><span data-stu-id="65757-128">Creating a command menu for your bot by editing **Manifest.json**</span></span>

<span data-ttu-id="65757-129">创建命令菜单的另一种有效方法是在开发 bot 源代码时直接在清单文件中创建它。</span><span class="sxs-lookup"><span data-stu-id="65757-129">Another valid approach for creating a command menu is to create it directly in the manifest file while developing your bot source code.</span></span> <span data-ttu-id="65757-130">使用此方法时，请记住以下几点：</span><span class="sxs-lookup"><span data-stu-id="65757-130">Here are a few things to keep in mind when using this approach:</span></span>

1. <span data-ttu-id="65757-131">每个菜单最长可支持10个命令。</span><span class="sxs-lookup"><span data-stu-id="65757-131">Each menu supports up to 10 commands.</span></span>

2. <span data-ttu-id="65757-132">可以创建将在所有范围中运行的单个命令菜单。</span><span class="sxs-lookup"><span data-stu-id="65757-132">You can create a single command menu that will work in all scopes.</span></span>

3. <span data-ttu-id="65757-133">您可以为每个作用域创建不同的命令菜单</span><span class="sxs-lookup"><span data-stu-id="65757-133">You can create a different command menu for each scope</span></span>

#### <a name="manifest-example---single-menu-for-both-scopes"></a><span data-ttu-id="65757-134">清单示例-两个范围的单个菜单</span><span class="sxs-lookup"><span data-stu-id="65757-134">Manifest example - single menu for both scopes</span></span>

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

#### <a name="manifest-example---menu-for-each-scope"></a><span data-ttu-id="65757-135">清单示例-每个范围的菜单</span><span class="sxs-lookup"><span data-stu-id="65757-135">Manifest example - menu for each scope</span></span>

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

## <a name="handling-menu-commands-in-your-bot-code"></a><span data-ttu-id="65757-136">处理机器人代码中的菜单命令</span><span class="sxs-lookup"><span data-stu-id="65757-136">Handling menu commands in your bot code</span></span>

<span data-ttu-id="65757-137">组或通道中的 bot 仅在邮件中提及（"@botname"）时响应。</span><span class="sxs-lookup"><span data-stu-id="65757-137">Bots in a group or channel respond only when they are mentioned ("@botname") in a message.</span></span> <span data-ttu-id="65757-138">因此，在组或频道作用域中，由 bot 接收的每封邮件将在返回的邮件文本中包含其自己的名称。</span><span class="sxs-lookup"><span data-stu-id="65757-138">As a result, every message received by a bot when in a group or channel scope will contain its own name in the message text returned.</span></span> <span data-ttu-id="65757-139">您需要确保在处理返回的命令之前，您的邮件分析处理程序。</span><span class="sxs-lookup"><span data-stu-id="65757-139">You need to ensure your message parsing handles that before handling the command being returned.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="65757-140">C #/.NET</span><span class="sxs-lookup"><span data-stu-id="65757-140">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="65757-141">您可以使用 Microsoft Bot 框架（名为`Activity` `RemoveRecipientMention`的类的方法）提供的静态方法分析邮件文本的\*\* \@提及\*\*部分。</span><span class="sxs-lookup"><span data-stu-id="65757-141">You can parse out the **\@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework — a method of the `Activity` class named `RemoveRecipientMention`.</span></span>

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="65757-142">JavaScript/node.js</span><span class="sxs-lookup"><span data-stu-id="65757-142">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="65757-143">您可以使用 Microsoft Bot 框架（名为`TurnContext` `removeMentionText`的类的方法）提供的静态方法分析邮件文本的\*\* \@提及\*\*部分。</span><span class="sxs-lookup"><span data-stu-id="65757-143">You can parse out the **\@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework — a method of the `TurnContext` class named `removeMentionText`.</span></span>

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="pythontabpython"></a>[<span data-ttu-id="65757-144">Python</span><span class="sxs-lookup"><span data-stu-id="65757-144">Python</span></span>](#tab/python)


<span data-ttu-id="65757-145">您可以使用 Microsoft Bot \*\*\*\* 框架（名为`TurnContext` `remove_recipient_mention`的类的方法）提供的静态方法分析邮件文本的 @Mention 部分。</span><span class="sxs-lookup"><span data-stu-id="65757-145">You can parse out the **@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework — a method of the `TurnContext` class named `remove_recipient_mention`.</span></span>

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

## <a name="command-menu-best-practices"></a><span data-ttu-id="65757-146">命令菜单最佳做法</span><span class="sxs-lookup"><span data-stu-id="65757-146">Command menu best practices</span></span>

* <span data-ttu-id="65757-147">**保持简单**： bot 菜单旨在提供你的 bot 的主要功能。</span><span class="sxs-lookup"><span data-stu-id="65757-147">**Keep it simple**: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="65757-148">**保持简短**：菜单选项不应是超长且复杂的自然语言语句—它们应为简单命令。</span><span class="sxs-lookup"><span data-stu-id="65757-148">**Keep it short**: Menu options shouldn’t be extremely long and complex natural language statements — they should be simple commands.</span></span>
* <span data-ttu-id="65757-149">**将其 invokable**：自动程序菜单操作/命令应始终可用，而不考虑会话的状态或机器人所在的对话框。</span><span class="sxs-lookup"><span data-stu-id="65757-149">**Keep it invokable**: Bot menu actions/commands should always be available, regardless of the state of the conversation or the dialog the bot is in.</span></span>
