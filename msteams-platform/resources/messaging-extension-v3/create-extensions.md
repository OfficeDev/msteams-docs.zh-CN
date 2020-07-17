---
title: 使用邮件扩展启动操作
description: 创建基于操作的消息扩展以允许用户触发外部服务
keywords: 工作组邮件传递扩展邮件扩展搜索
ms.openlocfilehash: 4eb5984f4a75f185accfe7ba87e9389361946959
ms.sourcegitcommit: 6c786434b56cc8c2765a14aa1f6149870245f309
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2020
ms.locfileid: "44801167"
---
# <a name="initiate-actions-with-messaging-extensions"></a><span data-ttu-id="ea011-104">使用邮件扩展启动操作</span><span class="sxs-lookup"><span data-stu-id="ea011-104">Initiate actions with messaging extensions</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="ea011-105">基于操作的消息传递扩展使用户能够在团队内触发外部服务中的操作。</span><span class="sxs-lookup"><span data-stu-id="ea011-105">Action-based messaging extensions allow your users to trigger actions in external services while inside of Teams.</span></span>

![邮件扩展卡的示例](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="ea011-107">以下各节介绍如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="ea011-107">The following sections describe how to do this.</span></span>

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a><span data-ttu-id="ea011-108">操作类型邮件扩展名</span><span class="sxs-lookup"><span data-stu-id="ea011-108">Action type message extensions</span></span>

<span data-ttu-id="ea011-109">若要从邮件扩展启动操作，请将 `type` 参数设置为 `action` 。</span><span class="sxs-lookup"><span data-stu-id="ea011-109">To initiate actions from a  messaging extension set the `type` parameter to `action`.</span></span> <span data-ttu-id="ea011-110">下面是一个带有搜索和创建命令的清单示例。</span><span class="sxs-lookup"><span data-stu-id="ea011-110">Below is an example of a manifest with a search and a create command.</span></span> <span data-ttu-id="ea011-111">单个邮件传递分机最长可包含10个不同的命令。</span><span class="sxs-lookup"><span data-stu-id="ea011-111">A single messaging extension can have up to 10 different commands.</span></span> <span data-ttu-id="ea011-112">这可以包括多个搜索和多个基于操作的命令。</span><span class="sxs-lookup"><span data-stu-id="ea011-112">This can include both multiple search and multiple action-based commands.</span></span>

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="ea011-113">完整的应用程序清单示例</span><span class="sxs-lookup"><span data-stu-id="ea011-113">Complete app manifest example</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
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

### <a name="initiate-actions-from-messages"></a><span data-ttu-id="ea011-114">从邮件中启动操作</span><span class="sxs-lookup"><span data-stu-id="ea011-114">Initiate actions from messages</span></span>

<span data-ttu-id="ea011-115">除了从撰写邮件区域中启动操作之外，还可以使用邮件扩展从邮件中启动操作。</span><span class="sxs-lookup"><span data-stu-id="ea011-115">In addition to initiating actions from the compose message area, you can also use your messaging extension to initiate an action from a message.</span></span> <span data-ttu-id="ea011-116">这将允许您将邮件的内容发送到你的 bot 以进行处理，还可以选择使用响应[提交](#responding-to-submit)中所述的方法，使用响应答复该邮件。</span><span class="sxs-lookup"><span data-stu-id="ea011-116">This will allow you to send the contents of the message to your bot for processing, and optionally reply to that message with a response using the method described in [Responding to submit](#responding-to-submit).</span></span> <span data-ttu-id="ea011-117">响应将作为回复插入到您的用户可以在提交前编辑的邮件。</span><span class="sxs-lookup"><span data-stu-id="ea011-117">The response will be inserted as a reply to the message that your users can edit before submitting.</span></span> <span data-ttu-id="ea011-118">您的用户可以从 "溢出" 菜单访问您的邮件扩展 `...` ，然后选择 `Take action` 下面的图像中的 "as"。</span><span class="sxs-lookup"><span data-stu-id="ea011-118">Your users can access your messaging extension from the overflow `...` menu and then selecting `Take action` as in the image below.</span></span>

![从邮件中启动操作的示例](~/assets/images/compose-extensions/messageextensions_messageaction.png)

<span data-ttu-id="ea011-120">若要使邮件扩展能够从邮件中运行，您需要将参数添加 `context` 到 `commands` 应用程序清单中的邮件扩展的对象，如下例所示。</span><span class="sxs-lookup"><span data-stu-id="ea011-120">To enable your messaging extension to work from a message you'll need to add the `context` parameter to your messaging extension's `commands` object in your app manifest as in the example below.</span></span> <span data-ttu-id="ea011-121">数组的有效字符串 `context` 为 `"message"` 、 `"commandBox"` 和 `"compose"` 。</span><span class="sxs-lookup"><span data-stu-id="ea011-121">Valid strings for the `context` array are `"message"`, `"commandBox"`, and `"compose"`.</span></span> <span data-ttu-id="ea011-122">默认值为 `["compose", "commandBox"]`。</span><span class="sxs-lookup"><span data-stu-id="ea011-122">The default value is `["compose", "commandBox"]`.</span></span> <span data-ttu-id="ea011-123">有关参数的完整详细信息，请参阅 "[定义命令](#define-commands)" 部分 `context` 。</span><span class="sxs-lookup"><span data-stu-id="ea011-123">See the [define commands](#define-commands) section for complete details on the `context` parameter.</span></span>

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

<span data-ttu-id="ea011-124">下面是一个对象的示例， `value` 其中包含将作为请求的一部分发送到你的 bot 的邮件详细信息 `composeExtension` 。</span><span class="sxs-lookup"><span data-stu-id="ea011-124">Below is an example of the `value` object containing the message details that will be sent as part of the `composeExtension` request be sent to your bot.</span></span>

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

### <a name="test-via-uploading"></a><span data-ttu-id="ea011-125">通过上传进行测试</span><span class="sxs-lookup"><span data-stu-id="ea011-125">Test via uploading</span></span>

<span data-ttu-id="ea011-126">您可以通过上载您的应用程序来测试您的邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="ea011-126">You can test your messaging extension by uploading your app.</span></span> <span data-ttu-id="ea011-127">有关详细信息，请参阅[在团队中上传你的应用](~/concepts/deploy-and-publish/apps-upload.md)。</span><span class="sxs-lookup"><span data-stu-id="ea011-127">See [Uploading your app in a team](~/concepts/deploy-and-publish/apps-upload.md) for details.</span></span>

<span data-ttu-id="ea011-128">若要打开邮件扩展插件，请导航到任何聊天或频道。</span><span class="sxs-lookup"><span data-stu-id="ea011-128">To open your messaging extension, navigate to any of your chats or channels.</span></span> <span data-ttu-id="ea011-129">选择 "撰写" 框中的 "**更多选项**（**&#8943;**）" 按钮，然后选择您的邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="ea011-129">Choose the **More options** (**&#8943;**) button in the compose box, and choose your messaging extension.</span></span>

## <a name="collecting-input-from-users"></a><span data-ttu-id="ea011-130">收集用户的输入</span><span class="sxs-lookup"><span data-stu-id="ea011-130">Collecting input from users</span></span>

<span data-ttu-id="ea011-131">有三种方法可以从工作组中的最终用户处收集信息。</span><span class="sxs-lookup"><span data-stu-id="ea011-131">There are three ways to collect information from an end user in Teams.</span></span>

### <a name="static-parameter-list"></a><span data-ttu-id="ea011-132">静态参数列表</span><span class="sxs-lookup"><span data-stu-id="ea011-132">Static parameter list</span></span>

<span data-ttu-id="ea011-133">在此方法中，您只需定义清单中的参数的静态列表，如上面的 "创建任务" 命令中所示。</span><span class="sxs-lookup"><span data-stu-id="ea011-133">In this method, all you need to do is define a static list of parameters in the manifest as shown above in the "Create To Do" command.</span></span> <span data-ttu-id="ea011-134">若要使用此方法，请确保 `fetchTask` 设置为 `false` ，并在清单中定义参数。</span><span class="sxs-lookup"><span data-stu-id="ea011-134">To use this method ensure `fetchTask` is set to `false` and that you define your parameters in the manifest.</span></span>

<span data-ttu-id="ea011-135">当用户选择带有静态参数的命令时，团队将在任务模块中使用清单中定义的参数生成窗体。</span><span class="sxs-lookup"><span data-stu-id="ea011-135">When a user chooses a command with static parameters, Teams will generate a form in a Task Module with the parameters defined in the manifest.</span></span> <span data-ttu-id="ea011-136">在 "命中提交 a" `composeExtension/submitAction` 发送到机器人。</span><span class="sxs-lookup"><span data-stu-id="ea011-136">On hitting Submit a `composeExtension/submitAction` is sent to the bot.</span></span> <span data-ttu-id="ea011-137">有关预期响应集的详细信息，请参阅主题[响应提交](#responding-to-submit)。</span><span class="sxs-lookup"><span data-stu-id="ea011-137">See the topic [Responding to submit](#responding-to-submit) for more information on the expected set of responses.</span></span>

### <a name="dynamic-input-using-an-adaptive-card"></a><span data-ttu-id="ea011-138">使用自适应卡片的动态输入</span><span class="sxs-lookup"><span data-stu-id="ea011-138">Dynamic input using an adaptive card</span></span>

<span data-ttu-id="ea011-139">在此方法中，服务可以定义自定义的自适应卡片以收集最终用户输入。</span><span class="sxs-lookup"><span data-stu-id="ea011-139">In this method, your service can define a custom adaptive card to collect the end user input.</span></span> <span data-ttu-id="ea011-140">对于此方法，请 `fetchTask` 在清单中将参数设置为 `true` 。</span><span class="sxs-lookup"><span data-stu-id="ea011-140">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span> <span data-ttu-id="ea011-141">请注意，如果您设置 `fetchTask` 为 `true` 将忽略为命令定义的任何静态参数。</span><span class="sxs-lookup"><span data-stu-id="ea011-141">Note that if you set `fetchTask` to `true` any static parameters defined for the command will be ignored.</span></span>

<span data-ttu-id="ea011-142">在此方法中，服务将接收 `composeExtension/fetchTask` 事件，并需要使用基于自适应卡的[任务模块响应](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)进行响应。</span><span class="sxs-lookup"><span data-stu-id="ea011-142">In this method your service will receive a `composeExtension/fetchTask` event and needs to respond with an adaptive card based [task module response](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="ea011-143">以下是使用自适应卡片的示例响应：</span><span class="sxs-lookup"><span data-stu-id="ea011-143">Below is an sample response with an adaptive card:</span></span>

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

<span data-ttu-id="ea011-144">如果用户需要在获取用户输入之前对扩展进行身份验证或配置，则 bot 还可以通过身份验证/配置响应进行响应。</span><span class="sxs-lookup"><span data-stu-id="ea011-144">The bot can also respond with an auth/config response if the user needs to authenticate or configure the extension before getting the user input.</span></span>

### <a name="dynamic-input-using-a-web-view"></a><span data-ttu-id="ea011-145">使用 web 视图的动态输入</span><span class="sxs-lookup"><span data-stu-id="ea011-145">Dynamic input using a web view</span></span>

<span data-ttu-id="ea011-146">在此方法中，您的服务可以显示一个 `<iframe>` 基于的小部件，以显示任何自定义 UI 并收集用户输入。</span><span class="sxs-lookup"><span data-stu-id="ea011-146">In this method your service can show an `<iframe>` based widget to show any custom UI and collect user input.</span></span> <span data-ttu-id="ea011-147">对于此方法，请 `fetchTask` 在清单中将参数设置为 `true` 。</span><span class="sxs-lookup"><span data-stu-id="ea011-147">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span>

<span data-ttu-id="ea011-148">就像在自适应卡流中，您的服务将发送 `fetchTask` 事件并需要使用基于 URL 的[任务模块响应](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)进行响应。</span><span class="sxs-lookup"><span data-stu-id="ea011-148">Just like in the adaptive card flow your service will be send a `fetchTask` event and needs to respond with a URL based [task module response](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="ea011-149">以下是使用自适应卡片的示例响应：</span><span class="sxs-lookup"><span data-stu-id="ea011-149">Below is an sample response with an Adaptive card:</span></span>

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

### <a name="request-to-install-your-conversational-bot"></a><span data-ttu-id="ea011-150">请求安装对话机器人</span><span class="sxs-lookup"><span data-stu-id="ea011-150">Request to install your conversational bot</span></span>

<span data-ttu-id="ea011-151">如果您的应用程序还包含一个对话机器人，则可能需要确保在加载任务模块之前在对话中安装你的 bot。</span><span class="sxs-lookup"><span data-stu-id="ea011-151">If your app also contains a conversational bot, it may be necessary to ensure that your bot is installed in the conversation before loading your task module.</span></span> <span data-ttu-id="ea011-152">在需要获取任务模块的其他上下文的情况下，这可能很有用。</span><span class="sxs-lookup"><span data-stu-id="ea011-152">This can be useful in situations where you need to get additional context for you task module.</span></span> <span data-ttu-id="ea011-153">例如，您可能需要提取名单以填充 "人员选取器" 控件或团队中的频道列表。</span><span class="sxs-lookup"><span data-stu-id="ea011-153">For example, you may need to fetch the roster to populate a people picker control, or the list of channels in a team.</span></span>

<span data-ttu-id="ea011-154">若要简化此流程，当邮件扩展程序首次收到 `composeExtension/fetchTask` 调用检查以查看您的 bot 是否已安装在当前上下文中时（例如，您可以通过尝试 get 名单调用来实现此目的）。</span><span class="sxs-lookup"><span data-stu-id="ea011-154">To facilitate this flow, when your messaging extension first receives the `composeExtension/fetchTask` invoke check to see if your bot is installed in the current context (you could accomplish this by attempting the get roster call, for example).</span></span> <span data-ttu-id="ea011-155">如果未安装你的 bot，请返回一个自适应卡片，其中包含一个请求用户安装你的 bot 的操作。请参阅下面的示例。</span><span class="sxs-lookup"><span data-stu-id="ea011-155">If your bot is not installed, you return an Adaptive Card with an action that requests the user to install your bot See the example below.</span></span> <span data-ttu-id="ea011-156">请注意，这要求用户具有在该位置安装应用程序的权限;如果不能，他们将看到一条消息，询问用户是否与管理员联系。</span><span class="sxs-lookup"><span data-stu-id="ea011-156">Note that this requires the user to have permission to install apps in that location; if they cannot they will be presented with a message asking them to contact their administrator.</span></span>

<span data-ttu-id="ea011-157">下面是一个响应示例：</span><span class="sxs-lookup"><span data-stu-id="ea011-157">Here's an example of the response:</span></span>

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

<span data-ttu-id="ea011-158">一旦用户完成安装，你的 bot 将收到另一条带和的 invoke 消息 `name = composeExtension/submitAction` `value.data.msteams.justInTimeInstall = true` 。</span><span class="sxs-lookup"><span data-stu-id="ea011-158">Once the user completes the installation, your bot will receive another invoke message with `name = composeExtension/submitAction`, and `value.data.msteams.justInTimeInstall = true`.</span></span>

<span data-ttu-id="ea011-159">下面是一个调用示例：</span><span class="sxs-lookup"><span data-stu-id="ea011-159">Here's an example of the invoke:</span></span>

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

<span data-ttu-id="ea011-160">您应使用与您进行响应的相同任务响应来响应此调用（如果已经安装了 bot）。</span><span class="sxs-lookup"><span data-stu-id="ea011-160">You should respond to this invoke with the same task response you would have responded with if the bot was already installed.</span></span>

## <a name="responding-to-submit"></a><span data-ttu-id="ea011-161">响应提交</span><span class="sxs-lookup"><span data-stu-id="ea011-161">Responding to submit</span></span>

<span data-ttu-id="ea011-162">用户完成输入后，你的 bot 将接收到 `composeExtension/submitAction` 设置了命令 id 和参数值的事件。</span><span class="sxs-lookup"><span data-stu-id="ea011-162">Once a user completes entering their input your bot will receive a `composeExtension/submitAction` event with the command id and parameter values set.</span></span>

<span data-ttu-id="ea011-163">这些是对的预期的不同响应 `submitAction` 。</span><span class="sxs-lookup"><span data-stu-id="ea011-163">These are the different expected responses to a `submitAction`.</span></span>

### <a name="task-module-response"></a><span data-ttu-id="ea011-164">任务模块响应</span><span class="sxs-lookup"><span data-stu-id="ea011-164">Task Module response</span></span>

<span data-ttu-id="ea011-165">当您的扩展需要将对话框链接在一起以获取详细信息时，将使用此信息。</span><span class="sxs-lookup"><span data-stu-id="ea011-165">This is used when your extension needs to chain dialogs together to get more information.</span></span> <span data-ttu-id="ea011-166">响应与前面提到的完全相同 `fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="ea011-166">The response is exactly the same as `fetchTask` mentioned earlier.</span></span>

### <a name="compose-extension-authconfig-response"></a><span data-ttu-id="ea011-167">撰写扩展身份验证/配置响应</span><span class="sxs-lookup"><span data-stu-id="ea011-167">Compose extension auth/config response</span></span>

<span data-ttu-id="ea011-168">当扩展需要进行身份验证或配置以便继续时，使用此方法。</span><span class="sxs-lookup"><span data-stu-id="ea011-168">This is used when your extension needs to either authenticate or configure in order to continue.</span></span> <span data-ttu-id="ea011-169">有关详细信息，请参阅 "搜索" 部分中的 "[身份验证" 部分](~/resources/messaging-extension-v3/search-extensions.md#authentication)。</span><span class="sxs-lookup"><span data-stu-id="ea011-169">See [authentication section](~/resources/messaging-extension-v3/search-extensions.md#authentication) in the search section for more details.</span></span>

### <a name="compose-extension-result-response"></a><span data-ttu-id="ea011-170">撰写扩展结果响应</span><span class="sxs-lookup"><span data-stu-id="ea011-170">Compose extension result response</span></span>

<span data-ttu-id="ea011-171">这用于将一个卡片作为命令插入到撰写框中。</span><span class="sxs-lookup"><span data-stu-id="ea011-171">This used to insert a card into the compose box as a result of a the command.</span></span> <span data-ttu-id="ea011-172">它与搜索命令中使用的响应相同，但仅限于一个卡片或阵列中的一个结果。</span><span class="sxs-lookup"><span data-stu-id="ea011-172">It's the same response that's used in the search command, but it's limited to one card or one result in the array.</span></span>

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
              "activityImage": "https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value": "[Larry Brown](mailto:larryb@example.com)"
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

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a><span data-ttu-id="ea011-173">使用从 bot 发送的自适应卡片邮件进行响应</span><span class="sxs-lookup"><span data-stu-id="ea011-173">Respond with an adaptive card message sent from a bot</span></span>

<span data-ttu-id="ea011-174">您还可以通过将带有自适应卡片的邮件插入到使用 bot 的频道中来响应提交操作。</span><span class="sxs-lookup"><span data-stu-id="ea011-174">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="ea011-175">你的用户将能够在提交邮件之前预览邮件，并可能对其进行编辑/与之交互。</span><span class="sxs-lookup"><span data-stu-id="ea011-175">Your user will be able to preview the message before submitting it, and potentially edit/interact with it as well.</span></span> <span data-ttu-id="ea011-176">这在您需要在创建自适应卡片响应之前从用户处收集信息的情况下可能非常有用。</span><span class="sxs-lookup"><span data-stu-id="ea011-176">This can be very useful in scenarios where you need to gather information from your users before creating an adaptive card response.</span></span> <span data-ttu-id="ea011-177">下面的方案演示如何使用此流配置轮询，而不在通道消息中包括配置步骤。</span><span class="sxs-lookup"><span data-stu-id="ea011-177">The following scenario shows how you can use this flow to configure a poll without including the configuration steps in the channel message.</span></span>

1. <span data-ttu-id="ea011-178">用户单击邮件扩展可触发任务模块。</span><span class="sxs-lookup"><span data-stu-id="ea011-178">The user clicks the messaging extension to trigger the task module.</span></span>
1. <span data-ttu-id="ea011-179">用户使用任务模块配置轮询。</span><span class="sxs-lookup"><span data-stu-id="ea011-179">The user uses the task module to configure the poll.</span></span>
1. <span data-ttu-id="ea011-180">提交配置任务模块后，应用使用任务模块中提供的信息来创建自适应卡片，并将其作为 `botMessagePreview` 对客户端的响应发送。</span><span class="sxs-lookup"><span data-stu-id="ea011-180">After submitting the configuration task module the app uses the information provided in the task module to craft an adaptive card and sends it as a `botMessagePreview` response to the client.</span></span>
1. <span data-ttu-id="ea011-181">然后，用户可以预览自适应卡片邮件，然后 bot 将其插入频道中。</span><span class="sxs-lookup"><span data-stu-id="ea011-181">The user can then preview the adaptive card message before the bot will inserts it into the channel.</span></span> <span data-ttu-id="ea011-182">如果 bot 尚不是频道的成员，则单击 "" `Send` 将添加机器人。</span><span class="sxs-lookup"><span data-stu-id="ea011-182">If the bot is not already a member of the channel, clicking `Send` will add the bot.</span></span>
1. <span data-ttu-id="ea011-183">与自适应卡片进行交互将会在发送邮件之前对其进行更改。</span><span class="sxs-lookup"><span data-stu-id="ea011-183">Interacting with the adaptive card will change the message before sending it.</span></span>
1. <span data-ttu-id="ea011-184">用户单击 bot 后， `Send` 会将邮件发送到频道。</span><span class="sxs-lookup"><span data-stu-id="ea011-184">Once the user clicks `Send` the bot will post the message to the channel.</span></span>

<span data-ttu-id="ea011-185">若要启用此流，您的任务模块应如下面的示例所示进行响应，这将向用户显示预览邮件。</span><span class="sxs-lookup"><span data-stu-id="ea011-185">To enable this flow your task module should respond as in the example below, which will present the preview message to the user.</span></span>

>[!Note]
><span data-ttu-id="ea011-186">`activityPreview`必须包含一个 `message` 只有1个自适应卡片附件的活动。</span><span class="sxs-lookup"><span data-stu-id="ea011-186">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span>

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

<span data-ttu-id="ea011-187">您的邮件扩展现在需要对两种新类型的交互和进行 `value.botMessagePreviewAction = "send"` 响应 `value.botMessagePreviewAction = "edit"` 。</span><span class="sxs-lookup"><span data-stu-id="ea011-187">Your message extension will now need to respond to two new types of interactions, `value.botMessagePreviewAction = "send"` and `value.botMessagePreviewAction = "edit"`.</span></span> <span data-ttu-id="ea011-188">下面是 `value` 需要处理的对象的示例：</span><span class="sxs-lookup"><span data-stu-id="ea011-188">Below is an example of the `value` object you will need to process:</span></span>

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

<span data-ttu-id="ea011-189">响应请求时，应响应，其中包含以 `edit` `task` 用户已提交的信息填充的值。</span><span class="sxs-lookup"><span data-stu-id="ea011-189">When responding to the `edit` request you should respond with a `task` response with the values populated with the information the user has already submitted.</span></span> <span data-ttu-id="ea011-190">响应 `send` 请求时，应向包含最终的自适应卡的频道发送一封邮件。</span><span class="sxs-lookup"><span data-stu-id="ea011-190">When responding to the `send` request you should send a message to the channel containing the finalized adaptive card.</span></span>

# <a name="typescriptnodejs"></a>[<span data-ttu-id="ea011-191">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="ea011-191">TypeScript/Node.js</span></span>](#tab/typescript)

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

<span data-ttu-id="ea011-192">*另请参阅* [Bot 框架示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="ea011-192">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="ea011-193">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="ea011-193">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="ea011-194">此示例演示如何使用[Microsoft Bot. 团队 SDK （v3）](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)进行传输。</span><span class="sxs-lookup"><span data-stu-id="ea011-194">This sample shows this flow using the [Microsoft.Bot.Connector.Teams SDK (v3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).</span></span>

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
