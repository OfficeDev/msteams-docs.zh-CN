---
title: 使用邮件扩展进行搜索
description: 介绍如何开发基于搜索的邮件扩展插件
keywords: 工作组邮件传递扩展邮件扩展搜索
ms.date: 07/20/2019
ms.openlocfilehash: b791e7cc8f9a311d0610573f2fa3659578c29c7d
ms.sourcegitcommit: 6c786434b56cc8c2765a14aa1f6149870245f309
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2020
ms.locfileid: "44801166"
---
# <a name="search-with-messaging-extensions"></a><span data-ttu-id="76bb5-104">使用邮件扩展进行搜索</span><span class="sxs-lookup"><span data-stu-id="76bb5-104">Search with messaging extensions</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="76bb5-105">基于搜索的邮件扩展允许您查询服务并以卡片形式发送该信息，并将其发布到您的邮件中</span><span class="sxs-lookup"><span data-stu-id="76bb5-105">Search based messaging extensions allow you to query your service and post that information in the form of a card, right into your message</span></span>

![邮件扩展卡的示例](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="76bb5-107">以下各节介绍如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="76bb5-107">The following sections describe how to do this.</span></span>

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="search-type-message-extensions"></a><span data-ttu-id="76bb5-108">搜索类型邮件扩展名</span><span class="sxs-lookup"><span data-stu-id="76bb5-108">Search type message extensions</span></span>

<span data-ttu-id="76bb5-109">对于基于搜索的邮件扩展，请将 `type` 参数设置为 `query` 。</span><span class="sxs-lookup"><span data-stu-id="76bb5-109">For search based messaging extension set the `type` parameter to `query`.</span></span> <span data-ttu-id="76bb5-110">下面是包含单个搜索命令的清单示例。</span><span class="sxs-lookup"><span data-stu-id="76bb5-110">Below is an example of a manifest with a single search command.</span></span> <span data-ttu-id="76bb5-111">单个消息传递扩展最长可以有10个不同的命令与之关联。</span><span class="sxs-lookup"><span data-stu-id="76bb5-111">A single messaging extension can have up to 10 different commands associated with it.</span></span> <span data-ttu-id="76bb5-112">这可以包括多个搜索和多个基于操作的命令。</span><span class="sxs-lookup"><span data-stu-id="76bb5-112">This can include both multiple search and multiple Action-based commands.</span></span>

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="76bb5-113">完整的应用程序清单示例</span><span class="sxs-lookup"><span data-stu-id="76bb5-113">Complete app manifest example</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.bing",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://bingbotservice.azurewebsites.net/",
    "privacyUrl": "http://bingbotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://bingbotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "Bing",
    "full": "Bing"
  },
  "description": {
    "short": "Find Bing search results",
    "full": "Find Bing search results and share them with your team members."
  },
  "icons": {
    "outline": "bing-outline.jpg",
    "color": "bing-color.jpg"
  },
  "accentColor": "#ff6a00",
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
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "bingbotservice.azurewebsites.net",
    "*.bingbotservice.azurewebsites.net"
  ]
}
```

### <a name="test-via-uploading"></a><span data-ttu-id="76bb5-114">通过上传进行测试</span><span class="sxs-lookup"><span data-stu-id="76bb5-114">Test via uploading</span></span>

<span data-ttu-id="76bb5-115">您可以通过上载您的应用程序来测试您的邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="76bb5-115">You can test your messaging extension by uploading your app.</span></span>

<span data-ttu-id="76bb5-116">若要打开邮件扩展插件，请导航到任何聊天或频道。</span><span class="sxs-lookup"><span data-stu-id="76bb5-116">To open your messaging extension, navigate to any of your chats or channels.</span></span> <span data-ttu-id="76bb5-117">选择 "撰写" 框中的 "**更多选项**（**&#8943;**）" 按钮，然后选择您的邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="76bb5-117">Choose the **More options** (**&#8943;**) button in the compose box, and choose your messaging extension.</span></span>

## <a name="add-event-handlers"></a><span data-ttu-id="76bb5-118">添加事件处理程序</span><span class="sxs-lookup"><span data-stu-id="76bb5-118">Add event handlers</span></span>

<span data-ttu-id="76bb5-119">大部分工作都涉及 `onQuery` 事件，后者处理邮件扩展窗口中的所有交互。</span><span class="sxs-lookup"><span data-stu-id="76bb5-119">Most of your work involves the `onQuery` event, which handles all interactions in the messaging extension window.</span></span>

<span data-ttu-id="76bb5-120">如果 `canUpdateConfiguration` `true` 在清单中设置为，则会为邮件扩展启用 "**设置**" 菜单项，还必须处理 `onQuerySettingsUrl` 和 `onSettingsUpdate` 。</span><span class="sxs-lookup"><span data-stu-id="76bb5-120">If you set `canUpdateConfiguration` to `true` in the manifest, you enable the **Settings** menu item for your messaging extension and must also handle `onQuerySettingsUrl` and `onSettingsUpdate`.</span></span>

### <a name="handle-onquery-events"></a><span data-ttu-id="76bb5-121">处理 onQuery 事件</span><span class="sxs-lookup"><span data-stu-id="76bb5-121">Handle onQuery events</span></span>

<span data-ttu-id="76bb5-122">邮件扩展 `onQuery` 在邮件扩展窗口中发生任何事情或发送到窗口时，都会收到事件。</span><span class="sxs-lookup"><span data-stu-id="76bb5-122">A messaging extension receives an `onQuery` event when anything happens in the messaging extension window or is sent to the window.</span></span>

<span data-ttu-id="76bb5-123">如果您的消息扩展使用配置页，则您的处理程序 `onQuery` 应首先检查任何存储的配置信息; 如果未配置邮件扩展，则返回一个 `config` 包含指向您的配置页面的链接的响应。</span><span class="sxs-lookup"><span data-stu-id="76bb5-123">If your messaging extension uses a configuration page, your handler for `onQuery` should first check for any stored configuration information; if the messaging extension isn't configured, return a `config` response with a link to your configuration page.</span></span> <span data-ttu-id="76bb5-124">请注意，来自配置页面的响应也由处理 `onQuery` 。</span><span class="sxs-lookup"><span data-stu-id="76bb5-124">Be aware that the response from the configuration page is also handled by `onQuery`.</span></span> <span data-ttu-id="76bb5-125">（唯一的例外是处理程序调用配置页面时 `onQuerySettingsUrl` ;请参阅下一节。</span><span class="sxs-lookup"><span data-stu-id="76bb5-125">(The sole exception is when the configuration page is called by the handler for `onQuerySettingsUrl`; see the following section.)</span></span>

<span data-ttu-id="76bb5-126">如果您的邮件扩展需要身份验证，请检查用户状态信息;如果用户未登录，请按照本主题后面的 "[身份验证](#authentication)" 一节中的说明操作。</span><span class="sxs-lookup"><span data-stu-id="76bb5-126">If your messaging extension requires authentication, check the user state information; if the user isn't signed in, follow the instructions in the [Authentication](#authentication) section later in this topic.</span></span>

<span data-ttu-id="76bb5-127">接下来，检查是否 `initialRun` 已设置; 如果是，请采取相应的操作，如提供说明或响应列表。</span><span class="sxs-lookup"><span data-stu-id="76bb5-127">Next, check whether `initialRun` is set; if so, take appropriate action, such as providing instructions or a list of responses.</span></span>

<span data-ttu-id="76bb5-128">用于提示用户输入信息的处理程序的其余部分 `onQuery` ，显示预览卡的列表，并返回用户选择的卡片。</span><span class="sxs-lookup"><span data-stu-id="76bb5-128">The remainder of your handler for `onQuery` prompts the user for information, displays a list of preview cards, and returns the card selected by the user.</span></span>

### <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a><span data-ttu-id="76bb5-129">处理 onQuerySettingsUrl 和 onSettingsUpdate 事件</span><span class="sxs-lookup"><span data-stu-id="76bb5-129">Handle onQuerySettingsUrl and onSettingsUpdate events</span></span>

<span data-ttu-id="76bb5-130">`onQuerySettingsUrl`和 `onSettingsUpdate` 事件一起使用，以启用 "**设置**" 菜单项。</span><span class="sxs-lookup"><span data-stu-id="76bb5-130">The `onQuerySettingsUrl` and `onSettingsUpdate` events work together to enable the **Settings** menu item.</span></span>

!["设置" 菜单项的位置的屏幕截图](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

<span data-ttu-id="76bb5-132">您的处理程序用于 `onQuerySettingsUrl` 返回配置页面的 URL; 配置页面关闭后，您的处理程序用于 `onSettingsUpdate` 接受并保存返回的状态。</span><span class="sxs-lookup"><span data-stu-id="76bb5-132">Your handler for `onQuerySettingsUrl` returns the URL for the configuration page; after the configuration page closes, your handler for `onSettingsUpdate` accepts and saves the returned state.</span></span> <span data-ttu-id="76bb5-133">（这是一种 `onQuery`*不*会从配置页收到响应。）</span><span class="sxs-lookup"><span data-stu-id="76bb5-133">(This is the one case in which `onQuery` *doesn't* receive the response from the configuration page.)</span></span>

## <a name="receive-and-respond-to-queries"></a><span data-ttu-id="76bb5-134">接收和响应查询</span><span class="sxs-lookup"><span data-stu-id="76bb5-134">Receive and respond to queries</span></span>

<span data-ttu-id="76bb5-135">对邮件扩展的每个请求都是通过 `Activity` 发布到您的回调 URL 的对象来完成的。</span><span class="sxs-lookup"><span data-stu-id="76bb5-135">Every request to your messaging extension is done via an `Activity` object that is posted to your callback URL.</span></span> <span data-ttu-id="76bb5-136">请求包含有关用户命令的信息，如 ID 和参数值。</span><span class="sxs-lookup"><span data-stu-id="76bb5-136">The request contains information about the user command, such as ID and parameter values.</span></span> <span data-ttu-id="76bb5-137">该请求还提供有关在其中调用扩展的上下文的元数据，包括用户和租户 ID，以及聊天 ID 或频道和团队 Id。</span><span class="sxs-lookup"><span data-stu-id="76bb5-137">The request also supplies metadata about the context in which your extension was invoked, including user and tenant ID, along with chat ID or channel and team IDs.</span></span>

### <a name="receive-user-requests"></a><span data-ttu-id="76bb5-138">接收用户请求</span><span class="sxs-lookup"><span data-stu-id="76bb5-138">Receive user requests</span></span>

<span data-ttu-id="76bb5-139">当用户执行查询时，Microsoft 团队会将您的服务发送到一个标准的 Bot 框架 `Activity` 对象。</span><span class="sxs-lookup"><span data-stu-id="76bb5-139">When a user performs a query, Microsoft Teams sends your service a standard Bot Framework `Activity` object.</span></span> <span data-ttu-id="76bb5-140">对于 `Activity` 已 `type` 设置为并设置为受支持的类型的，您的服务应执行其逻辑 `invoke` `name` ，如下 `composeExtension` 表所示。</span><span class="sxs-lookup"><span data-stu-id="76bb5-140">Your service should perform its logic for an `Activity` that has `type` set to `invoke` and `name` set to a supported `composeExtension` type, as shown in the following table.</span></span>

<span data-ttu-id="76bb5-141">除了标准 bot 活动属性之外，有效负载还包含以下请求元数据：</span><span class="sxs-lookup"><span data-stu-id="76bb5-141">In addition to the standard bot activity properties, the payload contains the following request metadata:</span></span>

|<span data-ttu-id="76bb5-142">属性名称</span><span class="sxs-lookup"><span data-stu-id="76bb5-142">Property name</span></span>|<span data-ttu-id="76bb5-143">用途</span><span class="sxs-lookup"><span data-stu-id="76bb5-143">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="76bb5-144">请求类型;必须为 `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="76bb5-144">Type of request; must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="76bb5-145">向您的服务发出的命令的类型。</span><span class="sxs-lookup"><span data-stu-id="76bb5-145">Type of command that is issued to your service.</span></span> <span data-ttu-id="76bb5-146">目前支持以下类型：</span><span class="sxs-lookup"><span data-stu-id="76bb5-146">Currently the following types are supported:</span></span> <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| <span data-ttu-id="76bb5-147">发送请求的用户的 ID。</span><span class="sxs-lookup"><span data-stu-id="76bb5-147">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="76bb5-148">发送请求的用户的名称。</span><span class="sxs-lookup"><span data-stu-id="76bb5-148">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="76bb5-149">发送请求的用户的 Azure Active Directory 对象 id。</span><span class="sxs-lookup"><span data-stu-id="76bb5-149">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="76bb5-150">Azure Active Directory 租户 ID。</span><span class="sxs-lookup"><span data-stu-id="76bb5-150">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="76bb5-151">通道 ID （如果请求是在通道中发出的）。</span><span class="sxs-lookup"><span data-stu-id="76bb5-151">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="76bb5-152">"工作组 ID" （如果请求是在通道中进行的）。</span><span class="sxs-lookup"><span data-stu-id="76bb5-152">Team ID (if the request was made in a channel).</span></span> |
|`clientInfo`|<span data-ttu-id="76bb5-153">有关用于发送用户消息的客户端软件的可选元数据。</span><span class="sxs-lookup"><span data-stu-id="76bb5-153">Optional metadata about the client software used to send a user's message.</span></span> <span data-ttu-id="76bb5-154">实体可以包含两个属性：</span><span class="sxs-lookup"><span data-stu-id="76bb5-154">The entity can contain two properties:</span></span><br><span data-ttu-id="76bb5-155">`country`字段包含用户检测到的位置。</span><span class="sxs-lookup"><span data-stu-id="76bb5-155">The `country` field contains the user's detected location.</span></span><br><span data-ttu-id="76bb5-156">`platform`字段描述邮件客户端平台。</span><span class="sxs-lookup"><span data-stu-id="76bb5-156">The `platform` field describes the messaging client platform.</span></span> <br><span data-ttu-id="76bb5-157">有关其他信息，请*参阅*[非 IRI 实体类型-clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)。</span><span class="sxs-lookup"><span data-stu-id="76bb5-157">For additional information, please *see* [Non-IRI entity types — clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>|

<span data-ttu-id="76bb5-158">请求参数本身位于 value 对象中，其中包括以下属性：</span><span class="sxs-lookup"><span data-stu-id="76bb5-158">The request parameters itself are found in the value object, which includes the following properties:</span></span>

| <span data-ttu-id="76bb5-159">属性名称</span><span class="sxs-lookup"><span data-stu-id="76bb5-159">Property name</span></span> | <span data-ttu-id="76bb5-160">用途</span><span class="sxs-lookup"><span data-stu-id="76bb5-160">Purpose</span></span> |
|---|---|
| `commandId` | <span data-ttu-id="76bb5-161">用户调用的命令的名称，与应用程序清单中声明的命令之一相匹配。</span><span class="sxs-lookup"><span data-stu-id="76bb5-161">The name of the command invoked by the user, matching one of the commands declared in the app manifest.</span></span> |
| `parameters` | <span data-ttu-id="76bb5-162">参数数组。</span><span class="sxs-lookup"><span data-stu-id="76bb5-162">Array of parameters.</span></span> <span data-ttu-id="76bb5-163">每个 parameter 对象包含参数名称，以及用户提供的参数值。</span><span class="sxs-lookup"><span data-stu-id="76bb5-163">Each parameter object contains the parameter name, along with the parameter value provided by the user.</span></span> |
| `queryOptions` | <span data-ttu-id="76bb5-164">分页参数：</span><span class="sxs-lookup"><span data-stu-id="76bb5-164">Pagination parameters:</span></span> <br><span data-ttu-id="76bb5-165">`skip`：跳过此查询的计数</span><span class="sxs-lookup"><span data-stu-id="76bb5-165">`skip`: skip count for this query</span></span> <br><span data-ttu-id="76bb5-166">`count`：要返回的元素数</span><span class="sxs-lookup"><span data-stu-id="76bb5-166">`count`: number of elements to return</span></span> |

#### <a name="request-example"></a><span data-ttu-id="76bb5-167">请求示例</span><span class="sxs-lookup"><span data-stu-id="76bb5-167">Request example</span></span>

```json
{
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "searchKeywords",
        "value": "Toronto"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  "type": "invoke",
  "timestamp": "2017-05-01T15:45:51.876Z",
  "localTimestamp": "2017-05-01T08:45:51.876-07:00",
  "id": "f:622749630322482883",
  "channelId": "msteams",
  "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
  "from": {
    "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
    "name": "Larry Jin",
    "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
  },
  "conversation": {
    "id": "19:skypespaces_8198cfe0dd2647ae91930f0974768a40@thread.skype"
  },
  "recipient": {
    "id": "28:b4922ea1-5315-4fd0-9b21-d941ab06e39f",
    "name": "TheComposeExtensionDev"
  },
  "entities": [
    {
    "type": "clientInfo",
      "country": "US",
      "platform": "Windows"
    }
  ]
}
```

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a><span data-ttu-id="76bb5-168">接收来自插入到撰写消息框中的链接的请求</span><span class="sxs-lookup"><span data-stu-id="76bb5-168">Receive requests from links inserted into the compose message box</span></span>

<span data-ttu-id="76bb5-169">作为用于搜索外部服务的替代（或补充），您可以使用插入到 "撰写" 消息框中的 URL 来查询服务并返回一个卡片。</span><span class="sxs-lookup"><span data-stu-id="76bb5-169">As an alternative (or in addition) to searching your external service, you can use a URL inserted into the compose message box to query your service and return a card.</span></span> <span data-ttu-id="76bb5-170">在下面的屏幕截图中，用户已在 Azure DevOps 中的工作项的 URL 中粘贴了邮件扩展已将其解析为卡片。</span><span class="sxs-lookup"><span data-stu-id="76bb5-170">In the screenshot below a user has pasted in a URL for a work item in Azure DevOps which the messaging extension has resolved into a card.</span></span>

![Link unfurling 的示例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

<span data-ttu-id="76bb5-172">若要使您的邮件扩展能够与链接进行交互，这种方法首先需要将该 `messageHandlers` 数组添加到应用程序清单中，如下例所示：</span><span class="sxs-lookup"><span data-stu-id="76bb5-172">To enable your messaging extension to interact with links this way you'll first need to add the `messageHandlers` array to your app manifest as in the example below:</span></span>

```json
"composeExtensions": [
  {
    "botId": "abc123456-ab12-ab12-ab12-abcdef123456",
    "messageHandlers": [
      {
        "type": "link",
        "value": {
          "domains": [
            "*.trackeddomain.com"
          ]
        }
      }
    ]
  }
]
```

<span data-ttu-id="76bb5-173">在添加了要侦听应用程序清单的域之后，您需要更改您的 bot 代码以[响应](#respond-to-user-requests)以下调用请求。</span><span class="sxs-lookup"><span data-stu-id="76bb5-173">Once you've added the domain to listen on to the app manifest, you'll need to change your bot code to [respond](#respond-to-user-requests) to the below invoke request.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="76bb5-174">如果您的应用程序返回多个项目，则仅使用第一个项目。</span><span class="sxs-lookup"><span data-stu-id="76bb5-174">If your app returns multiple items only the first will be used.</span></span>

### <a name="respond-to-user-requests"></a><span data-ttu-id="76bb5-175">响应用户请求</span><span class="sxs-lookup"><span data-stu-id="76bb5-175">Respond to user requests</span></span>

<span data-ttu-id="76bb5-176">当用户执行查询时，Microsoft 团队会向您的服务发出同步 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="76bb5-176">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service.</span></span> <span data-ttu-id="76bb5-177">在这种情况下，您的代码有5秒的时间来提供对请求的 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="76bb5-177">At that point, your code has 5 seconds to provide an HTTP response to the request.</span></span> <span data-ttu-id="76bb5-178">在这段时间内，您的服务可以执行其他查找，或提供服务请求所需的任何其他业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="76bb5-178">During this time, your service can perform additional lookup, or any other business logic needed to serve the request.</span></span>

<span data-ttu-id="76bb5-179">您的服务应使用与用户查询匹配的结果进行响应。</span><span class="sxs-lookup"><span data-stu-id="76bb5-179">Your service should respond with the results matching the user query.</span></span> <span data-ttu-id="76bb5-180">响应必须指示 HTTP 状态代码 `200 OK` ，以及具有以下正文的有效 application/json 对象：</span><span class="sxs-lookup"><span data-stu-id="76bb5-180">The response must indicate an HTTP status code of `200 OK` and a valid application/json object with the following body:</span></span>

|<span data-ttu-id="76bb5-181">属性名称</span><span class="sxs-lookup"><span data-stu-id="76bb5-181">Property name</span></span>|<span data-ttu-id="76bb5-182">用途</span><span class="sxs-lookup"><span data-stu-id="76bb5-182">Purpose</span></span>|
|---|---|
|`composeExtension`|<span data-ttu-id="76bb5-183">顶级响应信封。</span><span class="sxs-lookup"><span data-stu-id="76bb5-183">Top-level response envelope.</span></span>|
|`composeExtension.type`|<span data-ttu-id="76bb5-184">响应的类型。</span><span class="sxs-lookup"><span data-stu-id="76bb5-184">Type of response.</span></span> <span data-ttu-id="76bb5-185">支持以下类型：</span><span class="sxs-lookup"><span data-stu-id="76bb5-185">The following types are supported:</span></span> <br><span data-ttu-id="76bb5-186">`result`：显示搜索结果列表</span><span class="sxs-lookup"><span data-stu-id="76bb5-186">`result`: displays a list of search results</span></span> <br><span data-ttu-id="76bb5-187">`auth`：要求用户进行身份验证</span><span class="sxs-lookup"><span data-stu-id="76bb5-187">`auth`: asks the user to authenticate</span></span> <br><span data-ttu-id="76bb5-188">`config`：要求用户设置邮件扩展</span><span class="sxs-lookup"><span data-stu-id="76bb5-188">`config`: asks the user to set up the messaging extension</span></span> <br><span data-ttu-id="76bb5-189">`message`：显示纯文本消息</span><span class="sxs-lookup"><span data-stu-id="76bb5-189">`message`: displays a plain text message</span></span> |
|`composeExtension.attachmentLayout`|<span data-ttu-id="76bb5-190">指定附件的布局。</span><span class="sxs-lookup"><span data-stu-id="76bb5-190">Specifies the layout of the attachments.</span></span> <span data-ttu-id="76bb5-191">用于类型的响应 `result` 。</span><span class="sxs-lookup"><span data-stu-id="76bb5-191">Used for responses of type `result`.</span></span> <br><span data-ttu-id="76bb5-192">目前支持以下类型：</span><span class="sxs-lookup"><span data-stu-id="76bb5-192">Currently the following types are supported:</span></span> <br><span data-ttu-id="76bb5-193">`list`：包含缩略图、标题和文本字段的卡片对象的列表</span><span class="sxs-lookup"><span data-stu-id="76bb5-193">`list`: a list of card objects containing thumbnail, title, and text fields</span></span> <br><span data-ttu-id="76bb5-194">`grid`：缩略图图像的网格</span><span class="sxs-lookup"><span data-stu-id="76bb5-194">`grid`: a grid of thumbnail images</span></span> |
|`composeExtension.attachments`|<span data-ttu-id="76bb5-195">有效的附件对象的数组。</span><span class="sxs-lookup"><span data-stu-id="76bb5-195">Array of valid attachment objects.</span></span> <span data-ttu-id="76bb5-196">用于类型的响应 `result` 。</span><span class="sxs-lookup"><span data-stu-id="76bb5-196">Used for responses of type `result`.</span></span> <br><span data-ttu-id="76bb5-197">目前支持以下类型：</span><span class="sxs-lookup"><span data-stu-id="76bb5-197">Currently the following types are supported:</span></span> <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|<span data-ttu-id="76bb5-198">建议的操作。</span><span class="sxs-lookup"><span data-stu-id="76bb5-198">Suggested actions.</span></span> <span data-ttu-id="76bb5-199">用于类型或的响应 `auth` `config` 。</span><span class="sxs-lookup"><span data-stu-id="76bb5-199">Used for responses of type `auth` or `config`.</span></span> |
|`composeExtension.text`|<span data-ttu-id="76bb5-200">要显示的消息。</span><span class="sxs-lookup"><span data-stu-id="76bb5-200">Message to display.</span></span> <span data-ttu-id="76bb5-201">用于类型的响应 `message` 。</span><span class="sxs-lookup"><span data-stu-id="76bb5-201">Used for responses of type `message`.</span></span> |

#### <a name="response-card-types-and-previews"></a><span data-ttu-id="76bb5-202">响应卡片类型和预览</span><span class="sxs-lookup"><span data-stu-id="76bb5-202">Response card types and previews</span></span>

<span data-ttu-id="76bb5-203">我们支持以下附件类型：</span><span class="sxs-lookup"><span data-stu-id="76bb5-203">We support the following attachment types:</span></span>

* [<span data-ttu-id="76bb5-204">缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="76bb5-204">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="76bb5-205">英雄卡片</span><span class="sxs-lookup"><span data-stu-id="76bb5-205">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="76bb5-206">Office 365 连接器卡</span><span class="sxs-lookup"><span data-stu-id="76bb5-206">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="76bb5-207">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="76bb5-207">Adaptive card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="76bb5-208">请参阅[卡片](~/task-modules-and-cards/what-are-cards.md)获取概述。</span><span class="sxs-lookup"><span data-stu-id="76bb5-208">See [Cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

<span data-ttu-id="76bb5-209">若要了解如何使用缩略图和英雄卡片类型，请参阅[添加卡片和卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="76bb5-209">To learn how to use the thumbnail and hero card types, see [Add cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="76bb5-210">有关 Office 365 连接器卡的其他文档，请参阅[使用 office 365 连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)。</span><span class="sxs-lookup"><span data-stu-id="76bb5-210">For additional documentation regarding the Office 365 Connector card, see [Using Office 365 Connector cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="76bb5-211">结果列表显示在 Microsoft 团队 UI 中，每个项目都有一个预览。</span><span class="sxs-lookup"><span data-stu-id="76bb5-211">The result list is displayed in the Microsoft Teams UI with a preview of each item.</span></span> <span data-ttu-id="76bb5-212">将通过以下两种方式之一生成预览：</span><span class="sxs-lookup"><span data-stu-id="76bb5-212">The preview is generated in one of two ways:</span></span>

* <span data-ttu-id="76bb5-213">在 `preview` 对象中使用属性 `attachment` 。</span><span class="sxs-lookup"><span data-stu-id="76bb5-213">Using the `preview` property within the `attachment` object.</span></span> <span data-ttu-id="76bb5-214">该 `preview` 附件只能是一个英雄或缩略图卡片。</span><span class="sxs-lookup"><span data-stu-id="76bb5-214">The `preview` attachment can only be a Hero or Thumbnail card.</span></span>
* <span data-ttu-id="76bb5-215">从附件的基本 `title` 、 `text` 和属性中提取 `image` 。</span><span class="sxs-lookup"><span data-stu-id="76bb5-215">Extracted from the basic `title`, `text`, and `image` properties of the attachment.</span></span> <span data-ttu-id="76bb5-216">仅当 `preview` 未设置该属性且这些属性可用时，才使用这些属性。</span><span class="sxs-lookup"><span data-stu-id="76bb5-216">These are used only if the `preview` property is not set and these properties are available.</span></span>

<span data-ttu-id="76bb5-217">您可以仅通过设置其预览属性，在结果列表中显示自适应或 Office 365 连接器卡的预览。如果结果已经是英雄或缩略图卡片，则无需执行此步骤。</span><span class="sxs-lookup"><span data-stu-id="76bb5-217">You can display a preview of an Adaptive or Office 365 Connector card in the result list simply by setting its preview property; this is not necessary if the results are already hero or thumbnail cards.</span></span> <span data-ttu-id="76bb5-218">如果使用预览附件，则它必须是英雄或缩略图卡片。</span><span class="sxs-lookup"><span data-stu-id="76bb5-218">If you use the preview attachment, it must be either a Hero or Thumbnail card.</span></span> <span data-ttu-id="76bb5-219">如果未指定 preview 属性，卡片的预览将会失败，并且不会显示任何内容。</span><span class="sxs-lookup"><span data-stu-id="76bb5-219">If no preview property is specified, the preview of the card will fail and nothing will be displayed.</span></span>

#### <a name="response-example"></a><span data-ttu-id="76bb5-220">响应示例</span><span class="sxs-lookup"><span data-stu-id="76bb5-220">Response example</span></span>

<span data-ttu-id="76bb5-221">本示例显示一个响应，其中包含两个结果，混合不同的卡片格式： Office 365 连接器和自适应。</span><span class="sxs-lookup"><span data-stu-id="76bb5-221">This example shows a response with two results, mixing different card formats: Office 365 Connector and Adaptive.</span></span> <span data-ttu-id="76bb5-222">虽然您可能想要在响应中使用一种卡片格式，但它会显示 `preview` 集合中每个元素的属性如何以 `attachments` 所述的英雄或缩略图格式显式定义预览。</span><span class="sxs-lookup"><span data-stu-id="76bb5-222">While you'll likely want to stick with one card format in your response, it shows how the `preview` property of each element in the `attachments` collection must explicitly define a preview in hero or thumbnail format as described above.</span></span>

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
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
        },
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
        }
      },
      {
        "contentType": "application/vnd.microsoft.card.adaptive",
        "content": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Container",
              "items": [
                {
                  "type": "TextBlock",
                  "text": "Microsoft Corp (NASDAQ: MSFT)",
                  "size": "medium",
                  "isSubtle": true
                },
                {
                  "type": "TextBlock",
                  "text": "September 19, 4:00 PM EST",
                  "isSubtle": true
                }
              ]
            },
            {
              "type": "Container",
              "spacing": "none",
              "items": [
                {
                  "type": "ColumnSet",
                  "columns": [
                    {
                      "type": "Column",
                      "width": "stretch",
                      "items": [
                        {
                          "type": "TextBlock",
                          "text": "75.30",
                          "size": "extraLarge"
                        },
                        {
                          "type": "TextBlock",
                          "text": "▼ 0.20 (0.32%)",
                          "size": "small",
                          "color": "attention",
                          "spacing": "none"
                        }
                      ]
                    },
                    {
                      "type": "Column",
                      "width": "auto",
                      "items": [
                        {
                          "type": "FactSet",
                          "facts": [
                            {
                              "title": "Open",
                              "value": "62.24"
                            },
                            {
                              "title": "High",
                              "value": "62.98"
                            },
                            {
                              "title": "Low",
                              "value": "62.20"
                            }
                          ]
                        }
                      ]
                    }
                  ]
                }
              ]
            }
          ],
          "version": "1.0"
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "Microsoft Corp (NASDAQ: MSFT)",
            "text": "75.30 ▼ 0.20 (0.32%)"
          }
        }
      }
    ]
  }
}
```

### <a name="default-query"></a><span data-ttu-id="76bb5-223">默认查询</span><span class="sxs-lookup"><span data-stu-id="76bb5-223">Default query</span></span>

<span data-ttu-id="76bb5-224">如果 `initialRun` `true` 在清单中设置为，Microsoft 团队会在用户第一次打开邮件扩展时发出 "默认" 查询。</span><span class="sxs-lookup"><span data-stu-id="76bb5-224">If you set `initialRun` to `true` in the manifest, Microsoft Teams issues a "default" query when the user first opens the messaging extension.</span></span> <span data-ttu-id="76bb5-225">您的服务可以使用一组预填充的结果对此查询做出响应。</span><span class="sxs-lookup"><span data-stu-id="76bb5-225">Your service can respond to this query with a set of prepopulated results.</span></span> <span data-ttu-id="76bb5-226">这对于显示（例如，最近查看的项目、收藏夹或其他不依赖于用户输入的信息）可能很有用。</span><span class="sxs-lookup"><span data-stu-id="76bb5-226">This can be useful for displaying, for instance, recently viewed items, favorites, or any other information that is not dependent on user input.</span></span>

<span data-ttu-id="76bb5-227">默认查询的结构与任何常规用户查询相同，但 `initialRun` 其字符串值为的参数除外 `true` 。</span><span class="sxs-lookup"><span data-stu-id="76bb5-227">The default query has the same structure as any regular user query, except with a parameter `initialRun` whose string value is `true`.</span></span>

#### <a name="request-example-for-a-default-query"></a><span data-ttu-id="76bb5-228">默认查询的请求示例</span><span class="sxs-lookup"><span data-stu-id="76bb5-228">Request example for a default query</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "initialRun",
        "value": "true"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  ⋮
}
```

## <a name="identify-the-user"></a><span data-ttu-id="76bb5-229">标识用户</span><span class="sxs-lookup"><span data-stu-id="76bb5-229">Identify the user</span></span>

<span data-ttu-id="76bb5-230">对服务的每个请求都包括执行请求的用户的已模糊处理 ID，以及用户的显示名称和 Azure Active Directory 对象 ID。</span><span class="sxs-lookup"><span data-stu-id="76bb5-230">Every request to your services includes the obfuscated ID of the user that performed the request, as well as the user's display name and Azure Active Directory object ID.</span></span>

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

<span data-ttu-id="76bb5-231">`id`和 `aadObjectId` 值保证已通过身份验证的团队用户的。</span><span class="sxs-lookup"><span data-stu-id="76bb5-231">The `id` and `aadObjectId` values are guaranteed to be that of the authenticated Teams user.</span></span> <span data-ttu-id="76bb5-232">它们可用作在您的服务中查找凭据或任何缓存状态时使用的键。</span><span class="sxs-lookup"><span data-stu-id="76bb5-232">They can be used as keys to look up credentials or any cached state in your service.</span></span> <span data-ttu-id="76bb5-233">此外，每个请求都包含用户的 Azure Active Directory 租户 ID，可用于标识用户的组织。</span><span class="sxs-lookup"><span data-stu-id="76bb5-233">In addition, each request contains the Azure Active Directory tenant ID of the user, which can be used to identify the user’s organization.</span></span> <span data-ttu-id="76bb5-234">如果适用，该请求还包含发出请求的团队和频道 Id。</span><span class="sxs-lookup"><span data-stu-id="76bb5-234">If applicable, the request also contains the team and channel IDs from which the request originated.</span></span>

## <a name="authentication"></a><span data-ttu-id="76bb5-235">身份验证</span><span class="sxs-lookup"><span data-stu-id="76bb5-235">Authentication</span></span>

<span data-ttu-id="76bb5-236">如果您的服务需要进行用户身份验证，则需要在用户登录后才能使用邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="76bb5-236">If your service requires user authentication, you need to sign in the user before he or she can use the messaging extension.</span></span> <span data-ttu-id="76bb5-237">如果您已编写用于用户签名的 bot 或选项卡，则应熟悉此部分。</span><span class="sxs-lookup"><span data-stu-id="76bb5-237">If you have written a bot or a tab that signs in the user, this section should be familiar.</span></span>

<span data-ttu-id="76bb5-238">序列如下所示：</span><span class="sxs-lookup"><span data-stu-id="76bb5-238">The sequence is as follows:</span></span>

1. <span data-ttu-id="76bb5-239">用户发出查询，或将默认查询自动发送到您的服务。</span><span class="sxs-lookup"><span data-stu-id="76bb5-239">User issues a query, or the default query is automatically sent to your service.</span></span>
2. <span data-ttu-id="76bb5-240">您的服务通过检查团队用户 ID 检查用户是否先进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="76bb5-240">Your service checks whether the user has first authenticated by inspecting the Teams user ID.</span></span>
3. <span data-ttu-id="76bb5-241">如果用户未通过身份验证，则发送回复， `auth` 并提供 `openUrl` 建议的操作，包括身份验证 URL。</span><span class="sxs-lookup"><span data-stu-id="76bb5-241">If the user has not authenticated, send back an `auth` response with an `openUrl` suggested action including the authentication URL.</span></span>
4. <span data-ttu-id="76bb5-242">Microsoft 团队客户端使用给定的身份验证 URL 启动承载你的网页的弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="76bb5-242">The Microsoft Teams client launches a pop-up window hosting your webpage using the given authentication URL.</span></span>
5. <span data-ttu-id="76bb5-243">用户登录后，应关闭窗口并向团队客户端发送 "身份验证代码"。</span><span class="sxs-lookup"><span data-stu-id="76bb5-243">After the user signs in, you should close your window and send an "authentication code" to the Teams client.</span></span>
6. <span data-ttu-id="76bb5-244">然后，团队客户端将查询重新发出到您的服务，其中包括在步骤5中传递的身份验证代码。</span><span class="sxs-lookup"><span data-stu-id="76bb5-244">The Teams client then reissues the query to your service, which includes the authentication code passed in step 5.</span></span>

<span data-ttu-id="76bb5-245">您的服务应验证步骤6中收到的身份验证代码是否与步骤5中的验证代码相匹配。</span><span class="sxs-lookup"><span data-stu-id="76bb5-245">Your service should verify that the authentication code received in step 6 matches the one from step 5.</span></span> <span data-ttu-id="76bb5-246">这可确保恶意用户不会尝试欺骗或危害登录流。</span><span class="sxs-lookup"><span data-stu-id="76bb5-246">This ensures that a malicious user does not try to spoof or compromise the sign-in flow.</span></span> <span data-ttu-id="76bb5-247">这将有效地 "关闭循环" 以完成安全身份验证序列。</span><span class="sxs-lookup"><span data-stu-id="76bb5-247">This effectively "closes the loop" to finish the secure authentication sequence.</span></span>

### <a name="respond-with-a-sign-in-action"></a><span data-ttu-id="76bb5-248">使用登录操作进行响应</span><span class="sxs-lookup"><span data-stu-id="76bb5-248">Respond with a sign-in action</span></span>

<span data-ttu-id="76bb5-249">若要提示未经过身份验证的用户登录，请使用 `openUrl` 包含身份验证 URL 的 "类型" 建议操作进行响应。</span><span class="sxs-lookup"><span data-stu-id="76bb5-249">To prompt an unauthenticated user to sign in, respond with a suggested action of type `openUrl` that includes the authentication URL.</span></span>

#### <a name="response-example-for-a-sign-in-action"></a><span data-ttu-id="76bb5-250">登录操作的响应示例</span><span class="sxs-lookup"><span data-stu-id="76bb5-250">Response example for a sign-in action</span></span>

```json
{
  "composeExtension":{
    "type":"auth",
    "suggestedActions":{
      "actions":[
        {
          "type": "openUrl",
          "value": "https://example.com/auth",
          "title": "Sign in to this app"
        }
      ]
    }
  }
}
```

> [!NOTE]
> <span data-ttu-id="76bb5-251">若要在团队弹出窗口中承载登录体验，URL 的域部分必须位于您的应用程序的有效域的列表中。</span><span class="sxs-lookup"><span data-stu-id="76bb5-251">For the sign-in experience to be hosted in a Teams pop-up, the domain portion of the URL must be in your app’s list of valid domains.</span></span> <span data-ttu-id="76bb5-252">（请参阅清单架构中的[validDomains](~/resources/schema/manifest-schema.md#validdomains) 。）</span><span class="sxs-lookup"><span data-stu-id="76bb5-252">(See [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema.)</span></span>

### <a name="start-the-sign-in-flow"></a><span data-ttu-id="76bb5-253">启动登录流</span><span class="sxs-lookup"><span data-stu-id="76bb5-253">Start the sign-in flow</span></span>

<span data-ttu-id="76bb5-254">您的登录体验应响应且适合弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="76bb5-254">Your sign-in experience should be responsive and fit within a popup window.</span></span> <span data-ttu-id="76bb5-255">它应与使用邮件传递的[Microsoft 团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client)集成。</span><span class="sxs-lookup"><span data-stu-id="76bb5-255">It should integrate with the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client), which uses message passing.</span></span>

<span data-ttu-id="76bb5-256">与在 Microsoft 团队中运行的其他嵌入式体验一样，窗口中的代码需要先调用 `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="76bb5-256">As with other embedded experiences running inside Microsoft Teams, your code inside the window needs to first call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="76bb5-257">如果你的代码执行 OAuth 流，则可以将团队用户 ID 传递到你的窗口，然后可以将其传递到 OAuth 登录 URL。</span><span class="sxs-lookup"><span data-stu-id="76bb5-257">If your code performs an OAuth flow, you can pass the Teams user ID into your window, which then can pass it to the OAuth sign-in URL.</span></span>

### <a name="complete-the-sign-in-flow"></a><span data-ttu-id="76bb5-258">完成登录流</span><span class="sxs-lookup"><span data-stu-id="76bb5-258">Complete the sign-in flow</span></span>

<span data-ttu-id="76bb5-259">当登录请求完成并重定向回您的页面时，应执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="76bb5-259">When the sign-in request completes and redirects back to your page, it should perform the following steps:</span></span>

1. <span data-ttu-id="76bb5-260">生成安全代码。</span><span class="sxs-lookup"><span data-stu-id="76bb5-260">Generate a security code.</span></span> <span data-ttu-id="76bb5-261">（可以是一个随机数字。）您需要将此代码与您的服务进行缓存，以及通过登录流（例如 OAuth 2.0 令牌）获取的凭据。</span><span class="sxs-lookup"><span data-stu-id="76bb5-261">(This can be a random number.) You need to cache this code on your service, along with the credentials obtained through the sign-in flow (such as OAuth 2.0 tokens).</span></span>
2. <span data-ttu-id="76bb5-262">调用 `microsoftTeams.authentication.notifySuccess` 并传递安全代码。</span><span class="sxs-lookup"><span data-stu-id="76bb5-262">Call `microsoftTeams.authentication.notifySuccess` and pass the security code.</span></span>

<span data-ttu-id="76bb5-263">此时，窗口将关闭，并将控制传递给团队客户端。</span><span class="sxs-lookup"><span data-stu-id="76bb5-263">At this point, the window closes and control is passed to the Teams client.</span></span> <span data-ttu-id="76bb5-264">客户端现在可以重新发出原始用户查询，以及属性中的安全代码 `state` 。</span><span class="sxs-lookup"><span data-stu-id="76bb5-264">The client now can reissue the original user query, along with the security code in the `state` property.</span></span> <span data-ttu-id="76bb5-265">您的代码可以使用安全代码查找之前存储的凭据以完成身份验证序列，然后完成用户请求。</span><span class="sxs-lookup"><span data-stu-id="76bb5-265">Your code can use the security code to look up the credentials stored earlier to complete the authentication sequence and then complete the user request.</span></span>

#### <a name="reissued-request-example"></a><span data-ttu-id="76bb5-266">重新颁发的请求示例</span><span class="sxs-lookup"><span data-stu-id="76bb5-266">Reissued request example</span></span>

```json
{
    "name": "composeExtension/query",
    "value": {
        "commandId": "insertWiki",
        "parameters": [{
            "name": "searchKeyword",
            "value": "lakers"
        }],
        "state": "12345",
        "queryOptions": {
            "skip": 0,
            "count": 25
        }
    },
    "type": "invoke",
    "timestamp": "2017-04-26T05:18:25.629Z",
    "localTimestamp": "2017-04-25T22:18:25.629-07:00",
    "entities": [{
        "type": "clientInfo",
        "country": "US",
        "platform": "Web",
        
    }],
    "text": "",
    "attachments": [],
    "address": {
        "id": "f:7638210432489287768",
        "channelId": "msteams",
        "user": {
            "id": "29:1A5TJWHkbOwSyu_L9Ktk9QFI1d_kBOEPeNEeO1INscpKHzHTvWfiau5AX_6y3SuiOby-r73dzHJ17HipUWqGPgw",
            "aadObjectId": "fc8ca1c0-d043-4af6-b09f-141536207403"
        },
        "conversation": {
            "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
        },
        "bot": {
            "id": "28:c073afa8-7e77-4f92-b3e7-aa589e952a3e",
            "name": "maotestbot2"
        },
        "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
        "useAuth": true
    },
    "source": "msteams"
}
```

## <a name="sdk-support"></a><span data-ttu-id="76bb5-267">SDK 支持</span><span class="sxs-lookup"><span data-stu-id="76bb5-267">SDK support</span></span>

### <a name="net"></a><span data-ttu-id="76bb5-268">.NET</span><span class="sxs-lookup"><span data-stu-id="76bb5-268">.NET</span></span>

<span data-ttu-id="76bb5-269">若要使用机器人生成器 SDK 为 .NET 接收和处理查询，您可以 `invoke` 在 "传入" 活动中检查操作类型，然后使用 NuGet 包["."](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)中的帮助程序方法来确定它是否为邮件扩展活动。</span><span class="sxs-lookup"><span data-stu-id="76bb5-269">To receive and handle queries with the Bot Builder SDK for .NET, you can check for the `invoke` action type on the incoming activity and then use the helper method in the NuGet package [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) to determine whether it’s a messaging extension activity.</span></span>

#### <a name="example-code-in-net"></a><span data-ttu-id="76bb5-270">.NET 中的示例代码</span><span class="sxs-lookup"><span data-stu-id="76bb5-270">Example code in .NET</span></span>

```csharp
public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
{
    if (activity.Type == ActivityTypes.Invoke) // Received an invoke
    {
        if (activity.IsComposeExtensionQuery())
        {
            // This is the response object that will get sent back to the messaging extension request.
            ComposeExtensionResponse invokeResponse = null;

            // This helper method gets the query as an object.
            var query = activity.GetComposeExtensionQueryData();

            if (query.CommandId != null && query.Parameters != null && query.Parameters.Count > 0)
            {
                // query.Parameters has the parameters sent by client
                var results = new ComposeExtensionResult()
                {
                    AttachmentLayout = "list",
                    Type = "result",
                    Attachments = new List<ComposeExtensionAttachment>(),
                };
                invokeResponse.ComposeExtension = results;
            }

            // Return the response
            return Request.CreateResponse<ComposeExtensionResponse>(HttpStatusCode.OK, invokeResponse);
        } else
        {
            // Handle other types of Invoke activities here.
        }
    } else {
      // Failure case catch-all.
      var response = Request.CreateResponse(HttpStatusCode.BadRequest);
      response.Content = new StringContent("Invalid request! This API supports only messaging extension requests. Check your query and try again");
      return response;
    }
}
```

### <a name="nodejs"></a><span data-ttu-id="76bb5-271">Node.js</span><span class="sxs-lookup"><span data-stu-id="76bb5-271">Node.js</span></span>

#### <a name="example-code-in-nodejs"></a><span data-ttu-id="76bb5-272">Node.js 中的示例代码</span><span class="sxs-lookup"><span data-stu-id="76bb5-272">Example code in Node.js</span></span>

```javascript
require('dotenv').config();

import * as restify from 'restify';
import * as builder from 'botbuilder';
import * as teamBuilder from 'botbuilder-teams';

class App {
    run() {
        const server = restify.createServer();
        let teamChatConnector = new teamBuilder.TeamsChatConnector({
            appId: process.env.MICROSOFT_APP_ID,
            appPassword: process.env.MICROSOFT_APP_PASSWORD
        });

        // Command ID must match what's defined in manifest
        teamChatConnector.onQuery('<%= commandId %>',
            (event: builder.IEvent,
            query: teamBuilder.ComposeExtensionQuery,
            callback: (err: Error, result: teamBuilder.IComposeExtensionResponse, statusCode: number) => void) => {
                // Check for initialRun; i.e., when you should return default results
                // if (query.parameters[0].name === 'initialRun') {}

                // Check query.queryOptions.count and query.queryOptions.skip for paging

                // Return auth response
                // let response = teamBuilder.ComposeExtensionResponse.auth().actions([
                //     builder.CardAction.openUrl(null, 'https://authUrl', 'Please sign in')
                // ]).toResponse();

                // Return config response
                // let response = teamBuilder.ComposeExtensionResponse.config().actions([
                //     builder.CardAction.openUrl(null, 'https://configUrl', 'Please sign in')
                // ]).toResponse();

                // Return result response
                let response = teamBuilder.ComposeExtensionResponse.result('list').attachments([
                    new builder.ThumbnailCard()
                        .title('Test thumbnail card')
                        .text('This is a test thumbnail card')
                        .images([new builder.CardImage().url('https://bot-framework.azureedge.net/bot-icons-v1/bot-framework-default-9.png')])
                        .toAttachment()
                ]).toResponse();
                callback(null, response, 200);
            });
        server.post('/api/composeExtension', teamChatConnector.listen());
        server.listen(process.env.PORT, () => console.log(`listening to port:` + process.env.PORT));
    }
}

const app = new App();
app.run();
```
<span data-ttu-id="76bb5-273">*另请参阅* [Bot 框架示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="76bb5-273">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>
