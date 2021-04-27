---
title: 使用消息传递扩展启动操作
description: 创建基于操作的消息扩展以允许用户触发外部服务
localization_priority: Normal
ms.topic: how-to
keywords: teams 邮件扩展邮件扩展搜索
ms.openlocfilehash: a3122dbaf79f57054cfec2e8aef2ed4f687338be
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019732"
---
# <a name="initiate-actions-with-messaging-extensions"></a><span data-ttu-id="51f00-104">使用消息传递扩展启动操作</span><span class="sxs-lookup"><span data-stu-id="51f00-104">Initiate actions with messaging extensions</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="51f00-105">基于操作的消息扩展允许你的用户在 Teams 内触发外部服务中的操作。</span><span class="sxs-lookup"><span data-stu-id="51f00-105">Action-based messaging extensions allow your users to trigger actions in external services while inside of Teams.</span></span>

![邮件扩展卡示例](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="51f00-107">以下各节介绍如何执行这一操作。</span><span class="sxs-lookup"><span data-stu-id="51f00-107">The following sections describe how to do this.</span></span>

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a><span data-ttu-id="51f00-108">操作类型邮件扩展</span><span class="sxs-lookup"><span data-stu-id="51f00-108">Action type message extensions</span></span>

<span data-ttu-id="51f00-109">若要从邮件扩展启动操作，将 `type` 参数设置为 `action` 。</span><span class="sxs-lookup"><span data-stu-id="51f00-109">To initiate actions from a  messaging extension set the `type` parameter to `action`.</span></span> <span data-ttu-id="51f00-110">下面是一个使用搜索和创建命令的清单示例。</span><span class="sxs-lookup"><span data-stu-id="51f00-110">Below is an example of a manifest with a search and a create command.</span></span> <span data-ttu-id="51f00-111">单个邮件扩展最多可以有 10 个不同的命令。</span><span class="sxs-lookup"><span data-stu-id="51f00-111">A single messaging extension can have up to 10 different commands.</span></span> <span data-ttu-id="51f00-112">这可包括多个搜索和多个基于操作的命令。</span><span class="sxs-lookup"><span data-stu-id="51f00-112">This can include both multiple search and multiple action-based commands.</span></span>

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="51f00-113">完整的应用清单示例</span><span class="sxs-lookup"><span data-stu-id="51f00-113">Complete app manifest example</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.Todo",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://todobotservice.azurewebsites.net/",
    "privacyUrl": "http://todobotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://todobotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "To Do",
    "full": "To Do"
  },
  "description": {
    "short": "Find or create a new task in To Do",
    "full": "Find or create a new task in To Do"
  },
  "icons": {
    "outline": "todo-outline.jpg",
    "color": "todo-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "searchCmd",
          "description": "Search you Todo's",
          "title": "Search",
          "initialRun": true,
          "context": ["commandBox", "compose"],
          "parameters": [
            {
              "name": "searchKeyword",
              "description": "Enter your search keywords",
              "title": "Keywords"
            }
          ]
        },
        {
          "id": "addTodo",
          "description": "Create a To Do item",
          "title": "Create To Do",
          "type": "action",
          "context": ["commandBox", "message", "compose"],
          "parameters": [
            {
              "name": "Name",
              "description": "To Do Title",
              "title": "Title",
              "inputType": "text"
            },
            {
              "name": "Description",
              "description": "Description of the task",
              "title": "Description",
              "inputType": "textarea"
            },
            {
              "name": "Date",
              "description": "Due date for the task",
              "title": "Date",
              "inputType": "date"
            }
          ]
        },
        {
          "id": "reassignTodo",
          "description": "Reassign a todo item",
          "title": "Reassign a todo item",
          "type": "action",
          "fetchTask": true,
          "parameters": [
            {
              "name": "Name",
              "title": "Title"
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "todobotservice.azurewebsites.net",
    "*.todobotservice.azurewebsites.net"
  ]
}
```

### <a name="initiate-actions-from-messages"></a><span data-ttu-id="51f00-114">从邮件启动操作</span><span class="sxs-lookup"><span data-stu-id="51f00-114">Initiate actions from messages</span></span>

<span data-ttu-id="51f00-115">除了从撰写邮件区域启动操作之外，您还可以使用邮件扩展从邮件启动操作。</span><span class="sxs-lookup"><span data-stu-id="51f00-115">In addition to initiating actions from the compose message area, you can also use your messaging extension to initiate an action from a message.</span></span> <span data-ttu-id="51f00-116">这将允许你将邮件内容发送到自动程序进行处理，并可以选择使用"响应以提交"中所述的方法，通过响应回复 [邮件](#responding-to-submit)。</span><span class="sxs-lookup"><span data-stu-id="51f00-116">This will allow you to send the contents of the message to your bot for processing, and optionally reply to that message with a response using the method described in [Responding to submit](#responding-to-submit).</span></span> <span data-ttu-id="51f00-117">该响应将作为回复插入，您的用户可以在提交之前编辑该邮件。</span><span class="sxs-lookup"><span data-stu-id="51f00-117">The response will be inserted as a reply to the message that your users can edit before submitting.</span></span> <span data-ttu-id="51f00-118">你的用户可以从溢出菜单访问你的消息传递扩展 `...` ，然后选择 `Take action` 如下图所示。</span><span class="sxs-lookup"><span data-stu-id="51f00-118">Your users can access your messaging extension from the overflow `...` menu and then selecting `Take action` as in the image below.</span></span>

![从邮件启动操作的示例](~/assets/images/compose-extensions/messageextensions_messageaction.png)

<span data-ttu-id="51f00-120">若要使邮件扩展从邮件中工作，你需要将 参数添加到应用清单中邮件扩展的对象， `context` `commands` 如以下示例所示。</span><span class="sxs-lookup"><span data-stu-id="51f00-120">To enable your messaging extension to work from a message you'll need to add the `context` parameter to your messaging extension's `commands` object in your app manifest as in the example below.</span></span> <span data-ttu-id="51f00-121">数组的有效 `context` 字符串是 `"message"` 、 `"commandBox"` 和 `"compose"` 。</span><span class="sxs-lookup"><span data-stu-id="51f00-121">Valid strings for the `context` array are `"message"`, `"commandBox"`, and `"compose"`.</span></span> <span data-ttu-id="51f00-122">默认值为 `["compose", "commandBox"]`。</span><span class="sxs-lookup"><span data-stu-id="51f00-122">The default value is `["compose", "commandBox"]`.</span></span> <span data-ttu-id="51f00-123">有关参数 [的完整详细信息](#define-commands) ，请参阅定义命令 `context` 部分。</span><span class="sxs-lookup"><span data-stu-id="51f00-123">See the [define commands](#define-commands) section for complete details on the `context` parameter.</span></span>

```json
"composeExtensions": [
  {
    "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "reassignTodo",
        "description": "Reassign a todo item",
        "title": "Create To Do",
        "type": "Action",
        "context": ["message"],
        "fetchTask": true
    }]
    ...

```

<span data-ttu-id="51f00-124">下面是包含将在请求中发送的消息详细信息的对象示例，这些详细信息将 `value` `composeExtension` 发送给自动程序。</span><span class="sxs-lookup"><span data-stu-id="51f00-124">Below is an example of the `value` object containing the message details that will be sent as part of the `composeExtension` request be sent to your bot.</span></span>

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
...
  "value": {
    "commandId": "setReminder",
    "commandContext": "message",
    "messagePayload": {
      "id": "1111111111",
      "replyToId": null,
      "createdDateTime": "2019-02-25T21:29:36.065Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "subject": "Message subject",
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "this is the message"
    },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "wxyz12ab8-ab12-cd34-ef56-098abc123876",
          "displayName": "Jamie Smythe"
        },
        "application": null
      },
      "reactions": [
        {
          "reactionType": "like",
          "createdDateTime": "2019-02-25T22:40:40.806Z",
          "user": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "qrst12346-ab12-cd34-ef56-098abc123876",
              "displayName": "Jim Brown"
            },
            "application": null
          }
        }
      ],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Sarah",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "ab12345678-ab12-cd34-ef56-098abc123876",
              "displayName": "Sarah"
            },
            "application": null
          }
        }
      ]
    }
  ...
```

### <a name="test-via-uploading"></a><span data-ttu-id="51f00-125">通过上传进行测试</span><span class="sxs-lookup"><span data-stu-id="51f00-125">Test via uploading</span></span>

<span data-ttu-id="51f00-126">可以通过上传应用来测试邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="51f00-126">You can test your messaging extension by uploading your app.</span></span> <span data-ttu-id="51f00-127">有关详细信息 [，请参阅在团队中上传](~/concepts/deploy-and-publish/apps-upload.md) 应用。</span><span class="sxs-lookup"><span data-stu-id="51f00-127">See [Uploading your app in a team](~/concepts/deploy-and-publish/apps-upload.md) for details.</span></span>

<span data-ttu-id="51f00-128">若要打开消息扩展，请导航到任何聊天或频道。</span><span class="sxs-lookup"><span data-stu-id="51f00-128">To open your messaging extension, navigate to any of your chats or channels.</span></span> <span data-ttu-id="51f00-129">在撰写 **框中** 选择" (&#8943;) "按钮，然后选择邮件扩展。 </span><span class="sxs-lookup"><span data-stu-id="51f00-129">Choose the **More options** (**&#8943;**) button in the compose box, and choose your messaging extension.</span></span>

## <a name="collecting-input-from-users"></a><span data-ttu-id="51f00-130">收集用户输入</span><span class="sxs-lookup"><span data-stu-id="51f00-130">Collecting input from users</span></span>

<span data-ttu-id="51f00-131">在 Teams 中，有三种方法可以收集最终用户的信息。</span><span class="sxs-lookup"><span data-stu-id="51f00-131">There are three ways to collect information from an end user in Teams.</span></span>

### <a name="static-parameter-list"></a><span data-ttu-id="51f00-132">静态参数列表</span><span class="sxs-lookup"><span data-stu-id="51f00-132">Static parameter list</span></span>

<span data-ttu-id="51f00-133">在此方法中，只需在清单中定义一个静态参数列表，如"创建要执行"命令所示。</span><span class="sxs-lookup"><span data-stu-id="51f00-133">In this method, all you need to do is define a static list of parameters in the manifest as shown above in the "Create To Do" command.</span></span> <span data-ttu-id="51f00-134">若要使用此方法， `fetchTask` 请确保设置为 `false` ，并确保在清单中定义参数。</span><span class="sxs-lookup"><span data-stu-id="51f00-134">To use this method ensure `fetchTask` is set to `false` and that you define your parameters in the manifest.</span></span>

<span data-ttu-id="51f00-135">当用户选择具有静态参数的命令时，Teams 将在任务模块中生成一个包含清单中定义的参数的表单。</span><span class="sxs-lookup"><span data-stu-id="51f00-135">When a user chooses a command with static parameters, Teams will generate a form in a Task Module with the parameters defined in the manifest.</span></span> <span data-ttu-id="51f00-136">点击提交 `composeExtension/submitAction` 时，会向自动程序发送 。</span><span class="sxs-lookup"><span data-stu-id="51f00-136">On hitting Submit a `composeExtension/submitAction` is sent to the bot.</span></span> <span data-ttu-id="51f00-137">有关预期 [响应集的详细信息](#responding-to-submit) ，请参阅主题响应提交。</span><span class="sxs-lookup"><span data-stu-id="51f00-137">See the topic [Responding to submit](#responding-to-submit) for more information on the expected set of responses.</span></span>

### <a name="dynamic-input-using-an-adaptive-card"></a><span data-ttu-id="51f00-138">使用自适应卡片的动态输入</span><span class="sxs-lookup"><span data-stu-id="51f00-138">Dynamic input using an adaptive card</span></span>

<span data-ttu-id="51f00-139">在此方法中，你的服务可以定义一个自定义自适应卡片来收集最终用户的输入。</span><span class="sxs-lookup"><span data-stu-id="51f00-139">In this method, your service can define a custom adaptive card to collect the end user input.</span></span> <span data-ttu-id="51f00-140">对于此方法，在 `fetchTask` 清单中将 `true` 参数设置为 。</span><span class="sxs-lookup"><span data-stu-id="51f00-140">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span> <span data-ttu-id="51f00-141">请注意，如果设置为 `fetchTask` `true` 为命令定义的任何静态参数，将被忽略。</span><span class="sxs-lookup"><span data-stu-id="51f00-141">Note that if you set `fetchTask` to `true` any static parameters defined for the command will be ignored.</span></span>

<span data-ttu-id="51f00-142">在此方法中，你的服务将收到 `composeExtension/fetchTask` 事件，并且需要响应基于自适应卡片 [的任务模块响应](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)。</span><span class="sxs-lookup"><span data-stu-id="51f00-142">In this method your service will receive a `composeExtension/fetchTask` event and needs to respond with an adaptive card based [task module response](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="51f00-143">下面是一个包含自适应卡片的示例响应：</span><span class="sxs-lookup"><span data-stu-id="51f00-143">Below is an sample response with an adaptive card:</span></span>

```json
{
    "task": {
        "type": "continue",
        "value": {
            "card": {
                "contentType": "application/vnd.microsoft.card.adaptive",
                "content": {
                    "body": [
                        {
                            "type": "TextBlock",
                            "text": "Please enter the following information:"
                        },
                        {
                            "type": "TextBlock",
                            "text": "Name"
                        },
                        {
                            "type": "Input.Text",
                            "spacing": "None",
                            "title": "New Input.Toggle",
                            "placeholder": "Placeholder text"
                        },
                        {
                            "type": "TextBlock",
                            "text": "Date of birth"
                        },
                        {
                            "type": "Input.Date",
                            "spacing": "None",
                            "title": "New Input.Toggle"
                        }
                    ],
                    "type": "AdaptiveCard",
                    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
                    "version": "1.0"
                }
            }
        }
    }
}
```

<span data-ttu-id="51f00-144">如果用户在获取用户输入之前需要验证或配置扩展，机器人也可以响应身份验证/配置响应。</span><span class="sxs-lookup"><span data-stu-id="51f00-144">The bot can also respond with an auth/config response if the user needs to authenticate or configure the extension before getting the user input.</span></span>

### <a name="dynamic-input-using-a-web-view"></a><span data-ttu-id="51f00-145">使用 Web 视图的动态输入</span><span class="sxs-lookup"><span data-stu-id="51f00-145">Dynamic input using a web view</span></span>

<span data-ttu-id="51f00-146">在此方法中，你的服务可以显示 `<iframe>` 一个基于小部件来显示任何自定义 UI 并收集用户输入。</span><span class="sxs-lookup"><span data-stu-id="51f00-146">In this method your service can show an `<iframe>` based widget to show any custom UI and collect user input.</span></span> <span data-ttu-id="51f00-147">对于此方法，在 `fetchTask` 清单中将 `true` 参数设置为 。</span><span class="sxs-lookup"><span data-stu-id="51f00-147">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span>

<span data-ttu-id="51f00-148">就像在自适应卡片流中一样，你的服务将发送事件，并且需要 `fetchTask` 响应基于 URL [的任务模块响应](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)。</span><span class="sxs-lookup"><span data-stu-id="51f00-148">Just like in the adaptive card flow your service will be send a `fetchTask` event and needs to respond with a URL based [task module response](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="51f00-149">下面是一个包含自适应卡片的示例响应：</span><span class="sxs-lookup"><span data-stu-id="51f00-149">Below is an sample response with an Adaptive card:</span></span>

```json
{
    "task": {
        "value": {
            "url": "http://mywebapp.com/input"
        },
        "type": "continue"
    }
}
```

### <a name="request-to-install-your-conversational-bot"></a><span data-ttu-id="51f00-150">请求安装对话机器人</span><span class="sxs-lookup"><span data-stu-id="51f00-150">Request to install your conversational bot</span></span>

<span data-ttu-id="51f00-151">如果你的应用还包含对话机器人，可能需要在加载任务模块之前确保对话中已安装机器人。</span><span class="sxs-lookup"><span data-stu-id="51f00-151">If your app also contains a conversational bot, it may be necessary to ensure that your bot is installed in the conversation before loading your task module.</span></span> <span data-ttu-id="51f00-152">当你需要获取任务模块的其他上下文时，这非常有用。</span><span class="sxs-lookup"><span data-stu-id="51f00-152">This can be useful in situations where you need to get additional context for you task module.</span></span> <span data-ttu-id="51f00-153">例如，您可能需要获取名单以填充人员选取器控件或团队中的频道列表。</span><span class="sxs-lookup"><span data-stu-id="51f00-153">For example, you may need to fetch the roster to populate a people picker control, or the list of channels in a team.</span></span>

<span data-ttu-id="51f00-154">为了方便此流，当消息扩展首先收到调用检查以查看你的机器人是否安装在当前上下文中时 (可以通过尝试获取名单调用（例如) ）来实现此目的。 `composeExtension/fetchTask`</span><span class="sxs-lookup"><span data-stu-id="51f00-154">To facilitate this flow, when your messaging extension first receives the `composeExtension/fetchTask` invoke check to see if your bot is installed in the current context (you could accomplish this by attempting the get roster call, for example).</span></span> <span data-ttu-id="51f00-155">如果未安装自动程序，则返回自适应卡片以及请求用户安装自动程序的操作，请参阅下面的示例。</span><span class="sxs-lookup"><span data-stu-id="51f00-155">If your bot is not installed, you return an Adaptive Card with an action that requests the user to install your bot See the example below.</span></span> <span data-ttu-id="51f00-156">请注意，这要求用户有权在此位置安装应用;如果无法显示一条消息，要求他们联系其管理员。</span><span class="sxs-lookup"><span data-stu-id="51f00-156">Note that this requires the user to have permission to install apps in that location; if they cannot they will be presented with a message asking them to contact their administrator.</span></span>

<span data-ttu-id="51f00-157">下面是一个响应示例：</span><span class="sxs-lookup"><span data-stu-id="51f00-157">Here's an example of the response:</span></span>

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Looks like you haven't used Disco in this team/chat"
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Continue",
      "data": {
        "msteams": {
          "justInTimeInstall": true
        }
      }
    }
  ],
  "version": "1.0"
}
```

<span data-ttu-id="51f00-158">用户完成安装后，机器人将收到另一条使用 和 的调用 `name = composeExtension/submitAction` 消息 `value.data.msteams.justInTimeInstall = true` 。</span><span class="sxs-lookup"><span data-stu-id="51f00-158">Once the user completes the installation, your bot will receive another invoke message with `name = composeExtension/submitAction`, and `value.data.msteams.justInTimeInstall = true`.</span></span>

<span data-ttu-id="51f00-159">下面是一个调用示例：</span><span class="sxs-lookup"><span data-stu-id="51f00-159">Here's an example of the invoke:</span></span>

```json
{
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "msteams": {
        "justInTimeInstall": true
      }
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  },
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith"
}
```

<span data-ttu-id="51f00-160">如果已安装自动程序，你应该使用与响应相同的任务响应来响应此调用。</span><span class="sxs-lookup"><span data-stu-id="51f00-160">You should respond to this invoke with the same task response you would have responded with if the bot was already installed.</span></span>

## <a name="responding-to-submit"></a><span data-ttu-id="51f00-161">响应提交</span><span class="sxs-lookup"><span data-stu-id="51f00-161">Responding to submit</span></span>

<span data-ttu-id="51f00-162">用户输入完输入后，机器人将收到一个设置了命令 `composeExtension/submitAction` ID 和参数值的事件。</span><span class="sxs-lookup"><span data-stu-id="51f00-162">Once a user completes entering their input your bot will receive a `composeExtension/submitAction` event with the command id and parameter values set.</span></span>

<span data-ttu-id="51f00-163">这些是对 的不同预期响应 `submitAction` 。</span><span class="sxs-lookup"><span data-stu-id="51f00-163">These are the different expected responses to a `submitAction`.</span></span>

### <a name="task-module-response"></a><span data-ttu-id="51f00-164">任务模块响应</span><span class="sxs-lookup"><span data-stu-id="51f00-164">Task Module response</span></span>

<span data-ttu-id="51f00-165">当扩展需要将对话框链接在一起以了解更多信息时，会使用此功能。</span><span class="sxs-lookup"><span data-stu-id="51f00-165">This is used when your extension needs to chain dialogs together to get more information.</span></span> <span data-ttu-id="51f00-166">该响应与前面提到的 `fetchTask` 完全相同。</span><span class="sxs-lookup"><span data-stu-id="51f00-166">The response is exactly the same as `fetchTask` mentioned earlier.</span></span>

### <a name="compose-extension-authconfig-response"></a><span data-ttu-id="51f00-167">撰写扩展身份验证/配置响应</span><span class="sxs-lookup"><span data-stu-id="51f00-167">Compose extension auth/config response</span></span>

<span data-ttu-id="51f00-168">当扩展需要进行身份验证或配置才能继续时，会使用此功能。</span><span class="sxs-lookup"><span data-stu-id="51f00-168">This is used when your extension needs to either authenticate or configure in order to continue.</span></span> <span data-ttu-id="51f00-169">有关详细信息 [，请参阅](~/resources/messaging-extension-v3/search-extensions.md#authentication) 搜索部分中的身份验证部分。</span><span class="sxs-lookup"><span data-stu-id="51f00-169">See [authentication section](~/resources/messaging-extension-v3/search-extensions.md#authentication) in the search section for more details.</span></span>

### <a name="compose-extension-result-response"></a><span data-ttu-id="51f00-170">撰写扩展结果响应</span><span class="sxs-lookup"><span data-stu-id="51f00-170">Compose extension result response</span></span>

<span data-ttu-id="51f00-171">这用于将卡片作为命令的结果插入到撰写框中。</span><span class="sxs-lookup"><span data-stu-id="51f00-171">This used to insert a card into the compose box as a result of a the command.</span></span> <span data-ttu-id="51f00-172">该响应与搜索命令中使用的响应相同，但仅限于数组中的一个卡片或一个结果。</span><span class="sxs-lookup"><span data-stu-id="51f00-172">It's the same response that's used in the search command, but it's limited to one card or one result in the array.</span></span>

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        },
    "attachments": [
      {  
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage&quot;: &quot;https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value&quot;: &quot;[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        }
      }
    ]
  }
}
```

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a><span data-ttu-id="51f00-173">使用从自动程序发送的自适应卡片消息进行响应</span><span class="sxs-lookup"><span data-stu-id="51f00-173">Respond with an adaptive card message sent from a bot</span></span>

<span data-ttu-id="51f00-174">还可以响应提交操作，方法为使用自动程序将带自适应卡片的消息插入频道。</span><span class="sxs-lookup"><span data-stu-id="51f00-174">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="51f00-175">你的用户将能够在提交邮件之前预览邮件，并可能还对其进行编辑/交互。</span><span class="sxs-lookup"><span data-stu-id="51f00-175">Your user will be able to preview the message before submitting it, and potentially edit/interact with it as well.</span></span> <span data-ttu-id="51f00-176">在需要先从用户收集信息，然后再创建自适应卡片响应的情况下，这会非常有用。</span><span class="sxs-lookup"><span data-stu-id="51f00-176">This can be very useful in scenarios where you need to gather information from your users before creating an adaptive card response.</span></span> <span data-ttu-id="51f00-177">以下方案演示如何使用此流配置轮询，而无需在频道消息中包括配置步骤。</span><span class="sxs-lookup"><span data-stu-id="51f00-177">The following scenario shows how you can use this flow to configure a poll without including the configuration steps in the channel message.</span></span>

1. <span data-ttu-id="51f00-178">用户单击消息传递扩展以触发任务模块。</span><span class="sxs-lookup"><span data-stu-id="51f00-178">The user clicks the messaging extension to trigger the task module.</span></span>
1. <span data-ttu-id="51f00-179">用户使用任务模块配置轮询。</span><span class="sxs-lookup"><span data-stu-id="51f00-179">The user uses the task module to configure the poll.</span></span>
1. <span data-ttu-id="51f00-180">提交配置任务模块后，应用使用任务模块中提供的信息制作自适应卡片并将其作为 `botMessagePreview` 响应发送给客户端。</span><span class="sxs-lookup"><span data-stu-id="51f00-180">After submitting the configuration task module the app uses the information provided in the task module to craft an adaptive card and sends it as a `botMessagePreview` response to the client.</span></span>
1. <span data-ttu-id="51f00-181">然后，用户可以预览自适应卡片消息，然后机器人才能将其插入到频道中。</span><span class="sxs-lookup"><span data-stu-id="51f00-181">The user can then preview the adaptive card message before the bot will inserts it into the channel.</span></span> <span data-ttu-id="51f00-182">如果机器人不是频道成员，单击 `Send` 将添加机器人。</span><span class="sxs-lookup"><span data-stu-id="51f00-182">If the bot is not already a member of the channel, clicking `Send` will add the bot.</span></span>
1. <span data-ttu-id="51f00-183">与自适应卡片交互将更改消息，然后再发送它。</span><span class="sxs-lookup"><span data-stu-id="51f00-183">Interacting with the adaptive card will change the message before sending it.</span></span>
1. <span data-ttu-id="51f00-184">用户单击自动 `Send` 程序后，就会将消息张贴到频道。</span><span class="sxs-lookup"><span data-stu-id="51f00-184">Once the user clicks `Send` the bot will post the message to the channel.</span></span>

<span data-ttu-id="51f00-185">若要启用此流，任务模块应做出响应，如以下示例所示，这将向用户显示预览消息。</span><span class="sxs-lookup"><span data-stu-id="51f00-185">To enable this flow your task module should respond as in the example below, which will present the preview message to the user.</span></span>

>[!Note]
><span data-ttu-id="51f00-186">必须 `activityPreview` 包含正好包含 `message` 1 个自适应卡片附件的活动。</span><span class="sxs-lookup"><span data-stu-id="51f00-186">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span>

```json
{
  "composeExtension": {
    "type": "botMessagePreview",
    "activityPreview": {
      "type": "message",
      "attachments":  [
        {
          "contentType": "application/vnd.microsoft.card.adaptive",
          "content": << Card Payload >>
        }
      ]
    }
  }
}
```

<span data-ttu-id="51f00-187">现在，邮件扩展需要响应两种新类型的交互和 `value.botMessagePreviewAction = "send"` `value.botMessagePreviewAction = "edit"` 。</span><span class="sxs-lookup"><span data-stu-id="51f00-187">Your message extension will now need to respond to two new types of interactions, `value.botMessagePreviewAction = "send"` and `value.botMessagePreviewAction = "edit"`.</span></span> <span data-ttu-id="51f00-188">下面是需要 `value` 处理的对象示例：</span><span class="sxs-lookup"><span data-stu-id="51f00-188">Below is an example of the `value` object you will need to process:</span></span>

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "send" | "edit",
    "botActivityPreview": [
      {
        "type": "message/card",
        "attachments": [
          {
            "content":
              {
                "type": "AdaptiveCard",
                "body": [{<<card payload>>}]
              },
            "contentType" : "application/vnd.microsoft.card.adaptive"
          }
        ],
        "context": { "theme": "default" }
      }
    ],
  }
}
```

<span data-ttu-id="51f00-189">响应请求时，应响应 响应，并填充了用户 `edit` `task` 已提交的信息值。</span><span class="sxs-lookup"><span data-stu-id="51f00-189">When responding to the `edit` request you should respond with a `task` response with the values populated with the information the user has already submitted.</span></span> <span data-ttu-id="51f00-190">响应请求时，应该向包含最终自适应卡片 `send` 的频道发送消息。</span><span class="sxs-lookup"><span data-stu-id="51f00-190">When responding to the `send` request you should send a message to the channel containing the finalized adaptive card.</span></span>

# <a name="typescriptnodejs"></a>[<span data-ttu-id="51f00-191">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="51f00-191">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
teamChatConnector.onComposeExtensionSubmitAction((
    event: builder.IEvent,
    request: teamBuilder.IComposeExtensionActionCommandRequest,
    callback: (err: Error, result: any, statusCode: number) => void) => {
        let invokeValue = (<any> event).value;

        if (invokeValue.botMessagePreviewAction ) {
            let attachment = invokeValue.botActivityPreview[0].attachments[0];

            if (invokeValue.botMessagePreviewAction === 'send') {
                let msg = new builder.Message()
                    .address(event.address)
                    .addAttachment(attachment);
                teamChatConnector.send([msg.toMessage()],
                    (error) => {
                        if(error){
                            //TODO: Handle error and callback
                        }
                        else {
                            callback(null, null, 200);
                        }
                    }
                );
            }

            else if (invokeValue.botMessagePreviewAction === 'edit') {
              // Create the card and populate with user-inputted information
              let card = { ... }

              let taskResponse = {
                task: {
                  type: "continue",
                  value: {
                    title: "Card Preview",
                    card: {
                      contentType: 'application/vnd.microsoft.card.adaptive',
                      content: card
                    }
                  }
                }
              }
              callback(null, taskResponse, 200);
            }

        else {
            let attachment = {
                  //create adaptive card
                };
            let activity = new builder.Message().addAttachment(attachment).toMessage();
            let response = teamBuilder.ComposeExtensionResponse.messagePreview()
                .preview(activity)
                .toResponse();
            callback(null, response, 200);
        }
    });
```

<span data-ttu-id="51f00-192">*另请参阅* [Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="51f00-192">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="51f00-193">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="51f00-193">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="51f00-194">此示例使用[Microsoft.Bot.Connector.Teams SDK (v3) 。 ](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)</span><span class="sxs-lookup"><span data-stu-id="51f00-194">This sample shows this flow using the [Microsoft.Bot.Connector.Teams SDK (v3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).</span></span>

```csharp
public class MessagesController : ApiController
{

    [BotAuthentication]
    public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
    {
        MicrosoftAppCredentials.TrustServiceUrl(activity.ServiceUrl, DateTime.MaxValue);
        ConnectorClient connectorClient = new ConnectorClient(
            new Uri(activity.ServiceUrl),
            ConfigurationManager.AppSettings[MicrosoftAppCredentials.MicrosoftAppIdKey],
            ConfigurationManager.AppSettings[MicrosoftAppCredentials.MicrosoftAppPasswordKey]);

        if (activity.Type == ActivityTypes.Invoke)
        {
            // Initial task module presented to the user
            if (activity.Name == "composeExtension/fetchTask")
            {
                string task = GetTaskModule();

                return Request.CreateResponse(HttpStatusCode.OK, JObject.Parse(task));
            }
            else if (activity.Name == "composeExtension/submitAction")
            {
                dynamic activityValue = JObject.FromObject(activity.Value);
                string botMessagePreviewAction = activityValue["botMessagePreviewAction"];

                //This is the initial card response sent after the task module is submitted
                if (botMessagePreviewAction is null)
                {
                    string text = activityValue.data.cardMessage;

                    AdaptiveCard card = new AdaptiveCard(new AdaptiveSchemaVersion("1.0"));
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = "This card will be inserted into the conversation by the bot.",
                        Size = AdaptiveTextSize.Large,
                        Wrap = true
                    });
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = "The text below is what you provided."
                    });
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = text,
                    });

                    string cardJson = card.ToJson();

                    string cardMessage = $@"{{
                        'composeExtension': {{
                        'type': 'botMessagePreview',
                        'activityPreview': {{
                            'type': 'message',
                            'attachments': [{{
                                'contentType': 'application/vnd.microsoft.card.adaptive',
                                'content': {cardJson}
                            }}]
                        }}
                        }}
                    }}";

                    JObject res = JObject.Parse(cardMessage);
                    return Request.CreateResponse(HttpStatusCode.OK, res);

                }
                else
                {
                    //This is the "send the card to the channel" event
                    if (botMessagePreviewAction.Equals("send"))
                    {
                        string cardJson = JsonConvert.SerializeObject(activityValue.botActivityPreview[0].attachments[0].content);

                        AdaptiveCardParseResult cardResult = AdaptiveCard.FromJson(cardJson);
                        AdaptiveCard card = cardResult.Card;
                        Attachment cardAttachment = new Attachment
                        {
                            ContentType = AdaptiveCard.ContentType,
                            Content = card
                        };


                        Activity response = activity.CreateReply();
                        response.Attachments.Add(cardAttachment);

                        var result = await connectorClient.Conversations.SendToConversationAsync(response);
                    }
                    //This is fired if the user edits the card before sending it
                    else if (botMessagePreviewAction.Equals("edit"))
                    {
                        string task = GetTaskModule();

                        return Request.CreateResponse(HttpStatusCode.OK, JObject.Parse(task));
                    }
                    else
                    {
                        return Request.CreateResponse(HttpStatusCode.NotImplemented);
                    }
                }
            }
        }

        return Request.CreateResponse(HttpStatusCode.NotImplemented);

    }

    private static string GetTaskModule()
    {
        AdaptiveCard card = new AdaptiveCard(new AdaptiveSchemaVersion("1.0"));
        card.Body.Add(new AdaptiveTextBlock()
        {
            Text = "Please enter the following information:",
            Size = AdaptiveTextSize.Large
        });
        card.Body.Add(new AdaptiveTextBlock()
        {
            Text = "Card Message:"
        });
        card.Body.Add(new AdaptiveTextInput()
        {
            Id = "cardMessage",
            Spacing = AdaptiveSpacing.None,
            Placeholder = "Card message goes here."
        });
        card.Actions.Add(new AdaptiveSubmitAction()
        {
            Title = "Submit"
        });

        string cardJson = card.ToJson();

        //Create the task module response
        string task = $@"{{
                            'task': {{
                                'type': 'continue',
                                'value': {{
                                    'card': {{
                                        'contentType': 'application/vnd.microsoft.card.adaptive',
                                        'content': {cardJson}
                                        }}
                                    }}
                                }}
                            }}";
        return task;
    }

}
```
