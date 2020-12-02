---
title: 为你的 bot 创建命令菜单
author: clearab
description: 如何为 Microsoft 团队 bot 创建命令菜单
ms.topic: overview, command menu
ms.author: anclear
ms.openlocfilehash: ccbacc6ec6f18a38512d81dc898d0b14357d6ef7
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552484"
---
# <a name="bot-command-menus"></a><span data-ttu-id="0d3fc-103">Bot 命令菜单</span><span class="sxs-lookup"><span data-stu-id="0d3fc-103">Bot command menus</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

> [!Note]
> <span data-ttu-id="0d3fc-104">移动客户端上不会显示 Bot 菜单。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-104">Bot menus won't appear on mobile clients.</span></span>

<span data-ttu-id="0d3fc-105">通过为你的 bot 添加命令菜单，你可以定义你的 bot 可以始终响应的一组核心命令。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-105">Add command menu for your bot allows you to define a set of core commands your bot can always respond to.</span></span> <span data-ttu-id="0d3fc-106">当用户正在使用你的 bot 时，会向用户显示撰写邮件区域上方的命令列表。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-106">The list of commands is presented to the user above the compose message area when they are conversing with your bot.</span></span> <span data-ttu-id="0d3fc-107">从列表中选择一个命令会将命令字符串插入到撰写消息框中，所有用户都需要选择 " **发送**"。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-107">Selecting a command from the list will insert the command string into the compose message box, then all users need to do is select **Send**.</span></span>

![Bot 命令菜单](./conversations/media/bot-menu-sample.png)

## <a name="create-a-command-menu-for-your-bot"></a><span data-ttu-id="0d3fc-109">为你的 bot 创建命令菜单</span><span class="sxs-lookup"><span data-stu-id="0d3fc-109">Create a command menu for your bot</span></span>

<span data-ttu-id="0d3fc-110">命令菜单在应用部件清单（manifest）中定义。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-110">Command menus are defined in your app manifest.</span></span> <span data-ttu-id="0d3fc-111">您可以使用应用程序 Studio 来帮助您创建它们，也可以手动添加它们。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-111">You can either use App Studio to help you create them, or add them manually.</span></span>

### <a name="creating-a-command-menu-for-your-bot-using-app-studio"></a><span data-ttu-id="0d3fc-112">使用应用程序 Studio 为你的机器人创建命令菜单</span><span class="sxs-lookup"><span data-stu-id="0d3fc-112">Creating a command menu for your bot using App Studio</span></span>

<span data-ttu-id="0d3fc-113">此处的说明假定您将编辑现有的应用程序清单。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-113">The instructions here assume that you'll be editing an existing app manifest.</span></span> <span data-ttu-id="0d3fc-114">无论是创建新的清单还是编辑现有的清单，添加命令菜单的步骤都是相同的。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-114">The steps for adding a command menu are the same, whether you're creating a new manifest or editing an existing one.</span></span>

1. <span data-ttu-id="0d3fc-115">打开应用程序 Studio .。。左侧导航轨上的 "溢出" 菜单。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-115">Open App Studio from the ... overflow menu on the left navigation rail.</span></span> <span data-ttu-id="0d3fc-116">如果你没有可用的应用程序，可以下载。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-116">If you don't have App Studio available you can download it.</span></span> <span data-ttu-id="0d3fc-117">有关使用应用程序 Studio 的详细信息，请参阅 [安装应用程序 studio](https://aka.ms/teams-app-studio#installing-app-studio) 。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-117">See [Installing App Studio](https://aka.ms/teams-app-studio#installing-app-studio) for more information on using App Studio.</span></span>

    ![应用程序工作室](./conversations/media/AppStudio.png)

2. <span data-ttu-id="0d3fc-119">在应用程序 Studio 中，选择 " **清单编辑器** " 选项卡。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-119">Once in App Studio, select the **Manifest editor** tab.</span></span>

3. <span data-ttu-id="0d3fc-120">在 " **功能** " 部分的 "清单编辑器" 视图的左列中，选择 " **bot**"。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-120">In the left column of the manifest editor view in the **Capabilities** section, select **Bots**.</span></span>

4. <span data-ttu-id="0d3fc-121">在清单编辑器视图的右列中的 " **命令** " 部分，选择 " **添加** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-121">In the right column of the manifest editor view in the **Commands** section, select the **Add** button.</span></span>

    ![应用程序 Studio 命令菜单添加按钮](./conversations/media/AppStudio-CommandMenu-Add.png)

5. <span data-ttu-id="0d3fc-123">将显示 **新的命令** 屏幕。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-123">The **New Command** screen appears.</span></span> <span data-ttu-id="0d3fc-124">输入要显示为菜单命令的 **命令文本** ，以及要在菜单中的命令文本正下方显示的 " **帮助" 文本** 。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-124">Enter the **Command text** that you want to have appear as the menu command, and the **Help text** that you want to have appear directly under the command text in the menu.</span></span> <span data-ttu-id="0d3fc-125">这应该是命令用途的简短说明。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-125">This should be a brief explanation of the purpose of the command.</span></span>

6. <span data-ttu-id="0d3fc-126">接下来，选择要在其上显示此命令菜单的范围 (s) ，然后选择 " **保存** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-126">Next, select the scope(s) where you want this command menu to appear, then select the **Save** button.</span></span>

    ![应用程序 Studio 命令菜单添加按钮](./conversations/media/AppStudio-NewCommandMenu.png)

### <a name="creating-a-command-menu-for-your-bot-by-editing-manifestjson"></a><span data-ttu-id="0d3fc-128">通过 **在上编辑Manifest.js** 来创建你的 bot 的命令菜单</span><span class="sxs-lookup"><span data-stu-id="0d3fc-128">Creating a command menu for your bot by editing **Manifest.json**</span></span>

<span data-ttu-id="0d3fc-129">创建命令菜单的另一种有效方法是在开发 bot 源代码时直接在清单文件中创建它。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-129">Another valid approach for creating a command menu is to create it directly in the manifest file while developing your bot source code.</span></span> <span data-ttu-id="0d3fc-130">使用此方法时，请记住以下几点：</span><span class="sxs-lookup"><span data-stu-id="0d3fc-130">Here are a few things to keep in mind when using this approach:</span></span>

1. <span data-ttu-id="0d3fc-131">每个菜单最长可支持10个命令。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-131">Each menu supports up to 10 commands.</span></span>

2. <span data-ttu-id="0d3fc-132">可以创建将在所有范围中运行的单个命令菜单。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-132">You can create a single command menu that will work in all scopes.</span></span>

3. <span data-ttu-id="0d3fc-133">您可以为每个作用域创建不同的命令菜单</span><span class="sxs-lookup"><span data-stu-id="0d3fc-133">You can create a different command menu for each scope</span></span>

#### <a name="manifest-example---single-menu-for-both-scopes"></a><span data-ttu-id="0d3fc-134">清单示例-两个范围的单个菜单</span><span class="sxs-lookup"><span data-stu-id="0d3fc-134">Manifest example - single menu for both scopes</span></span>

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

#### <a name="manifest-example---menu-for-each-scope"></a><span data-ttu-id="0d3fc-135">清单示例-每个范围的菜单</span><span class="sxs-lookup"><span data-stu-id="0d3fc-135">Manifest example - menu for each scope</span></span>

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

## <a name="handling-menu-commands-in-your-bot-code"></a><span data-ttu-id="0d3fc-136">处理机器人代码中的菜单命令</span><span class="sxs-lookup"><span data-stu-id="0d3fc-136">Handling menu commands in your bot code</span></span>

<span data-ttu-id="0d3fc-137">组或通道中的 bot 仅在邮件中 ( "@botname" ) 提到它们时才做出响应。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-137">Bots in a group or channel respond only when they are mentioned ("@botname") in a message.</span></span> <span data-ttu-id="0d3fc-138">因此，在组或频道作用域中，由 bot 接收的每封邮件将在返回的邮件文本中包含其自己的名称。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-138">As a result, every message received by a bot when in a group or channel scope will contain its own name in the message text returned.</span></span> <span data-ttu-id="0d3fc-139">您需要确保在处理返回的命令之前，您的邮件分析处理程序。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-139">You need to ensure your message parsing handles that before handling the command being returned.</span></span>

> <span data-ttu-id="0d3fc-140">**注释** 在代码中处理命令时，它们将以常规邮件的形式发送到你的 bot。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-140">**Note** For handling the commands in code, they are sent to your bot as a regular message.</span></span> <span data-ttu-id="0d3fc-141">因此，您需要像处理来自用户的任何其他邮件那样处理这些文件。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-141">So you need to handle them as you would do for any other message from your users.</span></span> <span data-ttu-id="0d3fc-142">它们只是在文本框中插入预先配置的文本的 UI 处理。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-142">They are purely a UI treatment that inserts pre-configured text into the text box.</span></span> <span data-ttu-id="0d3fc-143">然后，用户必须像发送其他任何消息一样发送该文本。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-143">The user must then send that text as they would do for any other message.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="0d3fc-144">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="0d3fc-144">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="0d3fc-145">您可以使用 Microsoft Bot 框架（名为的类的方法）提供的静态方法分析邮件文本的 **\@ 提及** 部分 `Activity` `RemoveRecipientMention` 。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-145">You can parse out the **\@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework — a method of the `Activity` class named `RemoveRecipientMention`.</span></span>

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="0d3fc-146">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="0d3fc-146">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="0d3fc-147">您可以使用 Microsoft Bot 框架（名为的类的方法）提供的静态方法分析邮件文本的 **\@ 提及** 部分 `TurnContext` `removeMentionText` 。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-147">You can parse out the **\@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework — a method of the `TurnContext` class named `removeMentionText`.</span></span>

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[<span data-ttu-id="0d3fc-148">Python</span><span class="sxs-lookup"><span data-stu-id="0d3fc-148">Python</span></span>](#tab/python)


<span data-ttu-id="0d3fc-149">您可以使用 Microsoft Bot 框架（名为的类的方法）提供的静态方法分析邮件文本的 **@Mention** 部分 `TurnContext` `remove_recipient_mention` 。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-149">You can parse out the **@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework — a method of the `TurnContext` class named `remove_recipient_mention`.</span></span>

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

## <a name="command-menu-best-practices"></a><span data-ttu-id="0d3fc-150">命令菜单最佳做法</span><span class="sxs-lookup"><span data-stu-id="0d3fc-150">Command menu best practices</span></span>

* <span data-ttu-id="0d3fc-151">**保持简单**： bot 菜单旨在提供你的 bot 的主要功能。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-151">**Keep it simple**: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="0d3fc-152">**保持简短**：菜单选项不应是超长且复杂的自然语言语句—它们应为简单命令。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-152">**Keep it short**: Menu options shouldn’t be extremely long and complex natural language statements — they should be simple commands.</span></span>
* <span data-ttu-id="0d3fc-153">**将其 invokable**：自动程序菜单操作/命令应始终可用，而不考虑会话的状态或机器人所在的对话框。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-153">**Keep it invokable**: Bot menu actions/commands should always be available, regardless of the state of the conversation or the dialog the bot is in.</span></span>

> <span data-ttu-id="0d3fc-154">**注释** 如果从清单中删除任何命令，则需要重新部署应用，以使更改生效。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-154">**Note** If you remove any commands from your manifest, you will need to redeploy your app for the changes to take effect.</span></span> <span data-ttu-id="0d3fc-155">通常情况下，对清单所做的任何更改都需要进行此更改。</span><span class="sxs-lookup"><span data-stu-id="0d3fc-155">In general, any changes to the manifest require this.</span></span>
