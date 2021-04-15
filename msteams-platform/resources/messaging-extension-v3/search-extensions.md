---
title: 使用邮件扩展进行搜索
description: 介绍如何开发基于搜索的邮件扩展
keywords: teams 邮件扩展邮件扩展搜索
ms.topic: how-to
ms.date: 07/20/2019
ms.openlocfilehash: 7a4074fe4f3a15621729f4c549d31dc90d98e714
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696101"
---
# <a name="search-with-messaging-extensions"></a><span data-ttu-id="b3cf2-104">使用邮件扩展进行搜索</span><span class="sxs-lookup"><span data-stu-id="b3cf2-104">Search with messaging extensions</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="b3cf2-105">基于搜索的邮件扩展允许你查询服务，以卡片的形式将该信息张贴到邮件中</span><span class="sxs-lookup"><span data-stu-id="b3cf2-105">Search based messaging extensions allow you to query your service and post that information in the form of a card, right into your message</span></span>

![邮件扩展卡示例](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="b3cf2-107">以下各节介绍如何执行这一操作。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-107">The following sections describe how to do this.</span></span>

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="search-type-message-extensions"></a><span data-ttu-id="b3cf2-108">搜索类型邮件扩展</span><span class="sxs-lookup"><span data-stu-id="b3cf2-108">Search type message extensions</span></span>

<span data-ttu-id="b3cf2-109">对于基于搜索的邮件扩展，将 `type` 参数设置为 `query` 。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-109">For search based messaging extension set the `type` parameter to `query`.</span></span> <span data-ttu-id="b3cf2-110">下面是一个使用单个搜索命令的清单示例。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-110">Below is an example of a manifest with a single search command.</span></span> <span data-ttu-id="b3cf2-111">单个邮件扩展最多可以有 10 个不同的命令与之关联。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-111">A single messaging extension can have up to 10 different commands associated with it.</span></span> <span data-ttu-id="b3cf2-112">这可包括多个搜索和多个基于操作的命令。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-112">This can include both multiple search and multiple Action-based commands.</span></span>

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="b3cf2-113">完整的应用清单示例</span><span class="sxs-lookup"><span data-stu-id="b3cf2-113">Complete app manifest example</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
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

### <a name="test-via-uploading"></a><span data-ttu-id="b3cf2-114">通过上传进行测试</span><span class="sxs-lookup"><span data-stu-id="b3cf2-114">Test via uploading</span></span>

<span data-ttu-id="b3cf2-115">可以通过上传应用来测试邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-115">You can test your messaging extension by uploading your app.</span></span>

<span data-ttu-id="b3cf2-116">若要打开消息扩展，请导航到任何聊天或频道。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-116">To open your messaging extension, navigate to any of your chats or channels.</span></span> <span data-ttu-id="b3cf2-117">在撰写 **框中** 选择" (&#8943;) "按钮，然后选择邮件扩展。 </span><span class="sxs-lookup"><span data-stu-id="b3cf2-117">Choose the **More options** (**&#8943;**) button in the compose box, and choose your messaging extension.</span></span>

## <a name="add-event-handlers"></a><span data-ttu-id="b3cf2-118">添加事件处理程序</span><span class="sxs-lookup"><span data-stu-id="b3cf2-118">Add event handlers</span></span>

<span data-ttu-id="b3cf2-119">大多数工作都涉及 事件，该事件处理邮件扩展 `onQuery` 窗口中的所有交互。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-119">Most of your work involves the `onQuery` event, which handles all interactions in the messaging extension window.</span></span>

<span data-ttu-id="b3cf2-120">如果在清单中设置为 ，则启用邮件扩展的"设置"菜单项， `canUpdateConfiguration` `true` 并且还必须处理和 `onQuerySettingsUrl` `onSettingsUpdate` 。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-120">If you set `canUpdateConfiguration` to `true` in the manifest, you enable the **Settings** menu item for your messaging extension and must also handle `onQuerySettingsUrl` and `onSettingsUpdate`.</span></span>

### <a name="handle-onquery-events"></a><span data-ttu-id="b3cf2-121">处理 onQuery 事件</span><span class="sxs-lookup"><span data-stu-id="b3cf2-121">Handle onQuery events</span></span>

<span data-ttu-id="b3cf2-122">邮件扩展在邮件扩展窗口中发生任何事件或发送到该窗口时 `onQuery` 接收事件。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-122">A messaging extension receives an `onQuery` event when anything happens in the messaging extension window or is sent to the window.</span></span>

<span data-ttu-id="b3cf2-123">如果邮件扩展使用配置页，则 处理程序应首先检查任何存储的配置信息;如果未配置邮件扩展，则返回响应，并返回指向配置页面 `onQuery` `config` 的链接。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-123">If your messaging extension uses a configuration page, your handler for `onQuery` should first check for any stored configuration information; if the messaging extension isn't configured, return a `config` response with a link to your configuration page.</span></span> <span data-ttu-id="b3cf2-124">请注意，来自配置页面的响应也由 处理 `onQuery` 。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-124">Be aware that the response from the configuration page is also handled by `onQuery`.</span></span> <span data-ttu-id="b3cf2-125"> (唯一的例外是由 的处理程序调用配置页时; `onQuerySettingsUrl` 请参阅以下部分.) </span><span class="sxs-lookup"><span data-stu-id="b3cf2-125">(The sole exception is when the configuration page is called by the handler for `onQuerySettingsUrl`; see the following section.)</span></span>

<span data-ttu-id="b3cf2-126">如果邮件扩展需要身份验证，请检查用户状态信息;如果用户未登录，请按照本主题稍后的身份验证 [部分中](#authentication) 的说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-126">If your messaging extension requires authentication, check the user state information; if the user isn't signed in, follow the instructions in the [Authentication](#authentication) section later in this topic.</span></span>

<span data-ttu-id="b3cf2-127">接下来，检查是否已设置;如果是，则采取相应的操作，例如提供说明 `initialRun` 或响应列表。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-127">Next, check whether `initialRun` is set; if so, take appropriate action, such as providing instructions or a list of responses.</span></span>

<span data-ttu-id="b3cf2-128">其余处理程序会提示用户输入信息，显示预览卡片列表，并返回 `onQuery` 用户选择的卡片。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-128">The remainder of your handler for `onQuery` prompts the user for information, displays a list of preview cards, and returns the card selected by the user.</span></span>

### <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a><span data-ttu-id="b3cf2-129">处理 onQuerySettingsUrl 和 onSettingsUpdate 事件</span><span class="sxs-lookup"><span data-stu-id="b3cf2-129">Handle onQuerySettingsUrl and onSettingsUpdate events</span></span>

<span data-ttu-id="b3cf2-130">和 `onQuerySettingsUrl` `onSettingsUpdate` 事件协同工作以启用"设置 **"** 菜单项。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-130">The `onQuerySettingsUrl` and `onSettingsUpdate` events work together to enable the **Settings** menu item.</span></span>

!["设置"菜单项位置的屏幕截图](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

<span data-ttu-id="b3cf2-132">的处理程序返回配置页的 URL;配置页关闭后，您的 `onQuerySettingsUrl` 处理程序接受 `onSettingsUpdate` 并保存返回的状态。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-132">Your handler for `onQuerySettingsUrl` returns the URL for the configuration page; after the configuration page closes, your handler for `onSettingsUpdate` accepts and saves the returned state.</span></span> <span data-ttu-id="b3cf2-133"> (这是一个无法从配置页面接收响应 `onQuery` 的情况。) </span><span class="sxs-lookup"><span data-stu-id="b3cf2-133">(This is the one case in which `onQuery` *doesn't* receive the response from the configuration page.)</span></span>

## <a name="receive-and-respond-to-queries"></a><span data-ttu-id="b3cf2-134">接收和响应查询</span><span class="sxs-lookup"><span data-stu-id="b3cf2-134">Receive and respond to queries</span></span>

<span data-ttu-id="b3cf2-135">对消息扩展的每次请求都通过发布至回调 `Activity` URL 的对象完成。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-135">Every request to your messaging extension is done via an `Activity` object that is posted to your callback URL.</span></span> <span data-ttu-id="b3cf2-136">请求包含有关用户命令的信息，如 ID 和参数值。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-136">The request contains information about the user command, such as ID and parameter values.</span></span> <span data-ttu-id="b3cf2-137">请求还会提供有关调用扩展的上下文的元数据，包括用户和租户 ID，以及聊天 ID 或频道和团队 ID。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-137">The request also supplies metadata about the context in which your extension was invoked, including user and tenant ID, along with chat ID or channel and team IDs.</span></span>

### <a name="receive-user-requests"></a><span data-ttu-id="b3cf2-138">接收用户请求</span><span class="sxs-lookup"><span data-stu-id="b3cf2-138">Receive user requests</span></span>

<span data-ttu-id="b3cf2-139">当用户执行查询时，Microsoft Teams 会向服务发送标准 Bot Framework `Activity` 对象。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-139">When a user performs a query, Microsoft Teams sends your service a standard Bot Framework `Activity` object.</span></span> <span data-ttu-id="b3cf2-140">服务应执行其逻辑，该逻辑已设置为 并设置为支持 `Activity` `type` `invoke` `name` `composeExtension` 的类型，如下表所示。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-140">Your service should perform its logic for an `Activity` that has `type` set to `invoke` and `name` set to a supported `composeExtension` type, as shown in the following table.</span></span>

<span data-ttu-id="b3cf2-141">除了标准自动程序活动属性之外，有效负载还包含以下请求元数据：</span><span class="sxs-lookup"><span data-stu-id="b3cf2-141">In addition to the standard bot activity properties, the payload contains the following request metadata:</span></span>

|<span data-ttu-id="b3cf2-142">属性名称</span><span class="sxs-lookup"><span data-stu-id="b3cf2-142">Property name</span></span>|<span data-ttu-id="b3cf2-143">用途</span><span class="sxs-lookup"><span data-stu-id="b3cf2-143">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="b3cf2-144">请求类型;必须为 `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-144">Type of request; must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="b3cf2-145">向服务发出的命令类型。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-145">Type of command that is issued to your service.</span></span> <span data-ttu-id="b3cf2-146">目前支持以下类型：</span><span class="sxs-lookup"><span data-stu-id="b3cf2-146">Currently the following types are supported:</span></span> <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| <span data-ttu-id="b3cf2-147">发送请求的用户的 ID。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-147">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="b3cf2-148">发送请求的用户的名称。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-148">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="b3cf2-149">发送请求的用户的 Azure Active Directory 对象 ID。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-149">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="b3cf2-150">Azure Active Directory 租户 ID。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-150">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="b3cf2-151">如果 (通道请求，频道 ID 将) 。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-151">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="b3cf2-152">如果 (频道中提出请求，团队 ID 将) 。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-152">Team ID (if the request was made in a channel).</span></span> |
|`clientInfo`|<span data-ttu-id="b3cf2-153">有关用于发送用户消息的客户端软件的可选元数据。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-153">Optional metadata about the client software used to send a user's message.</span></span> <span data-ttu-id="b3cf2-154">实体可以包含两个属性：</span><span class="sxs-lookup"><span data-stu-id="b3cf2-154">The entity can contain two properties:</span></span><br><span data-ttu-id="b3cf2-155">`country`该字段包含用户的检测位置。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-155">The `country` field contains the user's detected location.</span></span><br><span data-ttu-id="b3cf2-156">`platform`字段描述消息客户端平台。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-156">The `platform` field describes the messaging client platform.</span></span> <br><span data-ttu-id="b3cf2-157">有关其他信息，请参阅 *非* [IRI 实体类型 — clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-157">For additional information, please *see* [Non-IRI entity types — clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>|

<span data-ttu-id="b3cf2-158">请求参数本身位于 value 对象中，其中包括以下属性：</span><span class="sxs-lookup"><span data-stu-id="b3cf2-158">The request parameters itself are found in the value object, which includes the following properties:</span></span>

| <span data-ttu-id="b3cf2-159">属性名称</span><span class="sxs-lookup"><span data-stu-id="b3cf2-159">Property name</span></span> | <span data-ttu-id="b3cf2-160">用途</span><span class="sxs-lookup"><span data-stu-id="b3cf2-160">Purpose</span></span> |
|---|---|
| `commandId` | <span data-ttu-id="b3cf2-161">用户调用的命令的名称，与在应用清单中声明的命令之一匹配。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-161">The name of the command invoked by the user, matching one of the commands declared in the app manifest.</span></span> |
| `parameters` | <span data-ttu-id="b3cf2-162">参数数组。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-162">Array of parameters.</span></span> <span data-ttu-id="b3cf2-163">每个参数对象都包含参数名称以及用户提供的参数值。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-163">Each parameter object contains the parameter name, along with the parameter value provided by the user.</span></span> |
| `queryOptions` | <span data-ttu-id="b3cf2-164">分页参数：</span><span class="sxs-lookup"><span data-stu-id="b3cf2-164">Pagination parameters:</span></span> <br><span data-ttu-id="b3cf2-165">`skip`：跳过此查询的计数</span><span class="sxs-lookup"><span data-stu-id="b3cf2-165">`skip`: skip count for this query</span></span> <br><span data-ttu-id="b3cf2-166">`count`：要返回的元素数</span><span class="sxs-lookup"><span data-stu-id="b3cf2-166">`count`: number of elements to return</span></span> |

#### <a name="request-example"></a><span data-ttu-id="b3cf2-167">请求示例</span><span class="sxs-lookup"><span data-stu-id="b3cf2-167">Request example</span></span>

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

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a><span data-ttu-id="b3cf2-168">从插入撰写消息框的链接接收请求</span><span class="sxs-lookup"><span data-stu-id="b3cf2-168">Receive requests from links inserted into the compose message box</span></span>

<span data-ttu-id="b3cf2-169">作为一 (或除了) 外部服务外，您还可以使用插入到撰写消息框中的 URL 查询您的服务并返回卡片。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-169">As an alternative (or in addition) to searching your external service, you can use a URL inserted into the compose message box to query your service and return a card.</span></span> <span data-ttu-id="b3cf2-170">在下面的屏幕截图中，用户已粘贴 Azure DevOps 中某个工作项的 URL，邮件扩展已解析为卡片。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-170">In the screenshot below a user has pasted in a URL for a work item in Azure DevOps which the messaging extension has resolved into a card.</span></span>

![链接取消链接示例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

<span data-ttu-id="b3cf2-172">若要使邮件扩展能够与链接进行交互，你首先需要将数组添加到应用清单， `messageHandlers` 如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="b3cf2-172">To enable your messaging extension to interact with links this way you'll first need to add the `messageHandlers` array to your app manifest as in the example below:</span></span>

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

<span data-ttu-id="b3cf2-173">添加域以侦听应用清单后，你需要更改自动程序代码以 [响应](#respond-to-user-requests) 以下调用请求。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-173">Once you've added the domain to listen on to the app manifest, you'll need to change your bot code to [respond](#respond-to-user-requests) to the below invoke request.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="b3cf2-174">如果你的应用返回多个项目，则只会使用第一个项目。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-174">If your app returns multiple items only the first will be used.</span></span>

### <a name="respond-to-user-requests"></a><span data-ttu-id="b3cf2-175">响应用户请求</span><span class="sxs-lookup"><span data-stu-id="b3cf2-175">Respond to user requests</span></span>

<span data-ttu-id="b3cf2-176">当用户执行查询时，Microsoft Teams 会向服务发送同步 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-176">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service.</span></span> <span data-ttu-id="b3cf2-177">此时，您的代码有 5 秒时间提供对请求的 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-177">At that point, your code has 5 seconds to provide an HTTP response to the request.</span></span> <span data-ttu-id="b3cf2-178">在此期间，你的服务可以执行其他查找，或执行为请求提供服务所需的任何其他业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-178">During this time, your service can perform additional lookup, or any other business logic needed to serve the request.</span></span>

<span data-ttu-id="b3cf2-179">服务应响应与用户查询匹配的结果。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-179">Your service should respond with the results matching the user query.</span></span> <span data-ttu-id="b3cf2-180">响应必须指示 的 HTTP 状态代码和具有以下正文的有效 `200 OK` application/json 对象：</span><span class="sxs-lookup"><span data-stu-id="b3cf2-180">The response must indicate an HTTP status code of `200 OK` and a valid application/json object with the following body:</span></span>

|<span data-ttu-id="b3cf2-181">属性名称</span><span class="sxs-lookup"><span data-stu-id="b3cf2-181">Property name</span></span>|<span data-ttu-id="b3cf2-182">用途</span><span class="sxs-lookup"><span data-stu-id="b3cf2-182">Purpose</span></span>|
|---|---|
|`composeExtension`|<span data-ttu-id="b3cf2-183">顶级响应信封。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-183">Top-level response envelope.</span></span>|
|`composeExtension.type`|<span data-ttu-id="b3cf2-184">响应类型。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-184">Type of response.</span></span> <span data-ttu-id="b3cf2-185">支持以下类型：</span><span class="sxs-lookup"><span data-stu-id="b3cf2-185">The following types are supported:</span></span> <br><span data-ttu-id="b3cf2-186">`result`：显示搜索结果列表</span><span class="sxs-lookup"><span data-stu-id="b3cf2-186">`result`: displays a list of search results</span></span> <br><span data-ttu-id="b3cf2-187">`auth`：要求用户进行身份验证</span><span class="sxs-lookup"><span data-stu-id="b3cf2-187">`auth`: asks the user to authenticate</span></span> <br><span data-ttu-id="b3cf2-188">`config`：要求用户设置邮件扩展</span><span class="sxs-lookup"><span data-stu-id="b3cf2-188">`config`: asks the user to set up the messaging extension</span></span> <br><span data-ttu-id="b3cf2-189">`message`: 显示纯文本邮件</span><span class="sxs-lookup"><span data-stu-id="b3cf2-189">`message`: displays a plain text message</span></span> |
|`composeExtension.attachmentLayout`|<span data-ttu-id="b3cf2-190">指定附件的布局。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-190">Specifies the layout of the attachments.</span></span> <span data-ttu-id="b3cf2-191">用于 类型 `result` 的响应。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-191">Used for responses of type `result`.</span></span> <br><span data-ttu-id="b3cf2-192">目前支持以下类型：</span><span class="sxs-lookup"><span data-stu-id="b3cf2-192">Currently the following types are supported:</span></span> <br><span data-ttu-id="b3cf2-193">`list`：包含缩略图、标题和文本字段的卡片对象列表</span><span class="sxs-lookup"><span data-stu-id="b3cf2-193">`list`: a list of card objects containing thumbnail, title, and text fields</span></span> <br><span data-ttu-id="b3cf2-194">`grid`：缩略图图像的网格</span><span class="sxs-lookup"><span data-stu-id="b3cf2-194">`grid`: a grid of thumbnail images</span></span> |
|`composeExtension.attachments`|<span data-ttu-id="b3cf2-195">有效 attachment 对象的数组。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-195">Array of valid attachment objects.</span></span> <span data-ttu-id="b3cf2-196">用于 类型 `result` 的响应。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-196">Used for responses of type `result`.</span></span> <br><span data-ttu-id="b3cf2-197">目前支持以下类型：</span><span class="sxs-lookup"><span data-stu-id="b3cf2-197">Currently the following types are supported:</span></span> <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|<span data-ttu-id="b3cf2-198">建议的操作。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-198">Suggested actions.</span></span> <span data-ttu-id="b3cf2-199">用于 或 类型的 `auth` 响应 `config` 。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-199">Used for responses of type `auth` or `config`.</span></span> |
|`composeExtension.text`|<span data-ttu-id="b3cf2-200">要显示的消息。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-200">Message to display.</span></span> <span data-ttu-id="b3cf2-201">用于 类型 `message` 的响应。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-201">Used for responses of type `message`.</span></span> |

#### <a name="response-card-types-and-previews"></a><span data-ttu-id="b3cf2-202">响应卡类型和预览</span><span class="sxs-lookup"><span data-stu-id="b3cf2-202">Response card types and previews</span></span>

<span data-ttu-id="b3cf2-203">我们支持以下附件类型：</span><span class="sxs-lookup"><span data-stu-id="b3cf2-203">We support the following attachment types:</span></span>

* [<span data-ttu-id="b3cf2-204">缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="b3cf2-204">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="b3cf2-205">Hero card</span><span class="sxs-lookup"><span data-stu-id="b3cf2-205">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="b3cf2-206">Office 365 连接器卡</span><span class="sxs-lookup"><span data-stu-id="b3cf2-206">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="b3cf2-207">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="b3cf2-207">Adaptive card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="b3cf2-208">有关 [概述](~/task-modules-and-cards/what-are-cards.md) ，请参阅卡片。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-208">See [Cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

<span data-ttu-id="b3cf2-209">若要了解如何使用缩略图和 Hero 卡片类型，请参阅 [添加卡片和卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-209">To learn how to use the thumbnail and hero card types, see [Add cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="b3cf2-210">有关 Office 365 连接器卡的其他文档，请参阅使用 [Office 365 连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-210">For additional documentation regarding the Office 365 Connector card, see [Using Office 365 Connector cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="b3cf2-211">结果列表显示在 Microsoft Teams UI 中，并预览每个项目。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-211">The result list is displayed in the Microsoft Teams UI with a preview of each item.</span></span> <span data-ttu-id="b3cf2-212">预览以以下两种方式之一生成：</span><span class="sxs-lookup"><span data-stu-id="b3cf2-212">The preview is generated in one of two ways:</span></span>

* <span data-ttu-id="b3cf2-213">在 `preview` 对象内使用 `attachment` 属性。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-213">Using the `preview` property within the `attachment` object.</span></span> <span data-ttu-id="b3cf2-214">附件 `preview` 只能是 Hero 或 Thumbnail 卡片。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-214">The `preview` attachment can only be a Hero or Thumbnail card.</span></span>
* <span data-ttu-id="b3cf2-215">从附件的基本 `title` 、 `text` 和 `image` 属性中提取。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-215">Extracted from the basic `title`, `text`, and `image` properties of the attachment.</span></span> <span data-ttu-id="b3cf2-216">只有在属性未设置且这些属性可用 `preview` 时，才使用这些属性。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-216">These are used only if the `preview` property is not set and these properties are available.</span></span>

<span data-ttu-id="b3cf2-217">只需设置自适应或 Office 365 连接器卡片的预览属性，就可以在结果列表中显示该卡片的预览;如果结果已是 hero 或 thumbnail 卡片，则不需要这样做。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-217">You can display a preview of an Adaptive or Office 365 Connector card in the result list simply by setting its preview property; this is not necessary if the results are already hero or thumbnail cards.</span></span> <span data-ttu-id="b3cf2-218">如果使用预览附件，它必须是 Hero 或 Thumbnail 卡片。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-218">If you use the preview attachment, it must be either a Hero or Thumbnail card.</span></span> <span data-ttu-id="b3cf2-219">如果未指定任何预览属性，则卡片预览将失败，并且不会显示任何内容。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-219">If no preview property is specified, the preview of the card will fail and nothing will be displayed.</span></span>

#### <a name="response-example"></a><span data-ttu-id="b3cf2-220">响应示例</span><span class="sxs-lookup"><span data-stu-id="b3cf2-220">Response example</span></span>

<span data-ttu-id="b3cf2-221">此示例显示了包含两个结果的响应，混合了不同的卡片格式：Office 365 连接器和自适应。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-221">This example shows a response with two results, mixing different card formats: Office 365 Connector and Adaptive.</span></span> <span data-ttu-id="b3cf2-222">虽然你可能想要在响应中坚持使用一个卡片格式，但它显示了集合中每个元素的 属性如何显式定义以 hero 或 thumbnail 格式的预览 `preview` `attachments` ，如上所述。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-222">While you'll likely want to stick with one card format in your response, it shows how the `preview` property of each element in the `attachments` collection must explicitly define a preview in hero or thumbnail format as described above.</span></span>

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

### <a name="default-query"></a><span data-ttu-id="b3cf2-223">默认查询</span><span class="sxs-lookup"><span data-stu-id="b3cf2-223">Default query</span></span>

<span data-ttu-id="b3cf2-224">如果在清单中设置为 ，Microsoft Teams 将在用户首次打开消息传递扩展时发送"默认 `initialRun` `true` "查询。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-224">If you set `initialRun` to `true` in the manifest, Microsoft Teams issues a "default" query when the user first opens the messaging extension.</span></span> <span data-ttu-id="b3cf2-225">你的服务可以使用一组预填充的结果来响应此查询。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-225">Your service can respond to this query with a set of prepopulated results.</span></span> <span data-ttu-id="b3cf2-226">这可用于显示最近查看的项目、收藏夹或其他不依赖于用户输入的信息。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-226">This can be useful for displaying, for instance, recently viewed items, favorites, or any other information that is not dependent on user input.</span></span>

<span data-ttu-id="b3cf2-227">默认查询的结构与任何常规用户查询相同，字符串值为 的参数除外 `initialRun` `true` 。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-227">The default query has the same structure as any regular user query, except with a parameter `initialRun` whose string value is `true`.</span></span>

#### <a name="request-example-for-a-default-query"></a><span data-ttu-id="b3cf2-228">默认查询的请求示例</span><span class="sxs-lookup"><span data-stu-id="b3cf2-228">Request example for a default query</span></span>

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

## <a name="identify-the-user"></a><span data-ttu-id="b3cf2-229">标识用户</span><span class="sxs-lookup"><span data-stu-id="b3cf2-229">Identify the user</span></span>

<span data-ttu-id="b3cf2-230">每个对服务的请求都包括执行请求的用户的模糊 ID，以及用户的 显示名称 和 Azure Active Directory 对象 ID。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-230">Every request to your services includes the obfuscated ID of the user that performed the request, as well as the user's display name and Azure Active Directory object ID.</span></span>

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

<span data-ttu-id="b3cf2-231">`id`和 `aadObjectId` 值保证为经过身份验证的 Teams 用户的值。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-231">The `id` and `aadObjectId` values are guaranteed to be that of the authenticated Teams user.</span></span> <span data-ttu-id="b3cf2-232">它们可用作在服务中查找凭据或任何缓存状态的密钥。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-232">They can be used as keys to look up credentials or any cached state in your service.</span></span> <span data-ttu-id="b3cf2-233">此外，每个请求都包含用户的 Azure Active Directory 租户 ID，可用于标识用户的组织。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-233">In addition, each request contains the Azure Active Directory tenant ID of the user, which can be used to identify the user’s organization.</span></span> <span data-ttu-id="b3cf2-234">如果适用，请求还包含源自请求的团队和频道的 ID。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-234">If applicable, the request also contains the team and channel IDs from which the request originated.</span></span>

## <a name="authentication"></a><span data-ttu-id="b3cf2-235">身份验证</span><span class="sxs-lookup"><span data-stu-id="b3cf2-235">Authentication</span></span>

<span data-ttu-id="b3cf2-236">如果服务需要用户身份验证，则需要先登录用户，然后才能使用消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-236">If your service requires user authentication, you need to sign in the user before he or she can use the messaging extension.</span></span> <span data-ttu-id="b3cf2-237">如果你已编写登录用户的自动程序或选项卡，应熟悉此部分。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-237">If you have written a bot or a tab that signs in the user, this section should be familiar.</span></span>

<span data-ttu-id="b3cf2-238">顺序如下所示：</span><span class="sxs-lookup"><span data-stu-id="b3cf2-238">The sequence is as follows:</span></span>

1. <span data-ttu-id="b3cf2-239">用户发出查询，或者默认查询将自动发送到您的服务。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-239">User issues a query, or the default query is automatically sent to your service.</span></span>
2. <span data-ttu-id="b3cf2-240">你的服务通过检查 Teams 用户 ID 来检查用户是否已首先进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-240">Your service checks whether the user has first authenticated by inspecting the Teams user ID.</span></span>
3. <span data-ttu-id="b3cf2-241">如果用户尚未进行身份验证，请发送回包含建议操作（包括身份验证 `auth` `openUrl` URL）的响应。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-241">If the user has not authenticated, send back an `auth` response with an `openUrl` suggested action including the authentication URL.</span></span>
4. <span data-ttu-id="b3cf2-242">Microsoft Teams 客户端使用给定的身份验证 URL 启动托管网页的弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-242">The Microsoft Teams client launches a pop-up window hosting your webpage using the given authentication URL.</span></span>
5. <span data-ttu-id="b3cf2-243">用户登录后，应关闭窗口，并将"身份验证代码"发送到 Teams 客户端。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-243">After the user signs in, you should close your window and send an "authentication code" to the Teams client.</span></span>
6. <span data-ttu-id="b3cf2-244">然后，Teams 客户端重新对服务进行查询，其中包括步骤 5 中传递的身份验证代码。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-244">The Teams client then reissues the query to your service, which includes the authentication code passed in step 5.</span></span>

<span data-ttu-id="b3cf2-245">服务应验证步骤 6 中收到的身份验证代码是否与步骤 5 中的身份验证代码匹配。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-245">Your service should verify that the authentication code received in step 6 matches the one from step 5.</span></span> <span data-ttu-id="b3cf2-246">这可确保恶意用户不会尝试欺骗或破坏登录流。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-246">This ensures that a malicious user does not try to spoof or compromise the sign-in flow.</span></span> <span data-ttu-id="b3cf2-247">这实际上"关闭循环"以完成安全身份验证序列。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-247">This effectively "closes the loop" to finish the secure authentication sequence.</span></span>

### <a name="respond-with-a-sign-in-action"></a><span data-ttu-id="b3cf2-248">使用登录操作响应</span><span class="sxs-lookup"><span data-stu-id="b3cf2-248">Respond with a sign-in action</span></span>

<span data-ttu-id="b3cf2-249">若要提示未经身份验证的用户登录，请通过包含身份验证 URL 的类型的建议操作 `openUrl` 进行响应。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-249">To prompt an unauthenticated user to sign in, respond with a suggested action of type `openUrl` that includes the authentication URL.</span></span>

#### <a name="response-example-for-a-sign-in-action"></a><span data-ttu-id="b3cf2-250">登录操作的响应示例</span><span class="sxs-lookup"><span data-stu-id="b3cf2-250">Response example for a sign-in action</span></span>

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
> <span data-ttu-id="b3cf2-251">若要在 Teams 弹出窗口中托管登录体验，URL 的域部分必须位于你的应用的有效域列表中。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-251">For the sign-in experience to be hosted in a Teams pop-up, the domain portion of the URL must be in your app’s list of valid domains.</span></span> <span data-ttu-id="b3cf2-252"> (清单架构中查看[validDomains。) ](~/resources/schema/manifest-schema.md#validdomains)</span><span class="sxs-lookup"><span data-stu-id="b3cf2-252">(See [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema.)</span></span>

### <a name="start-the-sign-in-flow"></a><span data-ttu-id="b3cf2-253">启动登录流程</span><span class="sxs-lookup"><span data-stu-id="b3cf2-253">Start the sign-in flow</span></span>

<span data-ttu-id="b3cf2-254">你的登录体验应响应迅速且适合弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-254">Your sign-in experience should be responsive and fit within a popup window.</span></span> <span data-ttu-id="b3cf2-255">它应与使用消息传递 [的 Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client)集成。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-255">It should integrate with the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client), which uses message passing.</span></span>

<span data-ttu-id="b3cf2-256">与在 Microsoft Teams 内运行的其他嵌入体验一样，窗口内的代码需要先调用 `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-256">As with other embedded experiences running inside Microsoft Teams, your code inside the window needs to first call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="b3cf2-257">如果你的代码执行 OAuth 流，你可以将 Teams 用户 ID 传递到你的窗口，然后可以将它传递到 OAuth 登录 URL。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-257">If your code performs an OAuth flow, you can pass the Teams user ID into your window, which then can pass it to the OAuth sign-in URL.</span></span>

### <a name="complete-the-sign-in-flow"></a><span data-ttu-id="b3cf2-258">完成登录流程</span><span class="sxs-lookup"><span data-stu-id="b3cf2-258">Complete the sign-in flow</span></span>

<span data-ttu-id="b3cf2-259">当登录请求完成并重定向回你的页面时，它应执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="b3cf2-259">When the sign-in request completes and redirects back to your page, it should perform the following steps:</span></span>

1. <span data-ttu-id="b3cf2-260">生成安全代码。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-260">Generate a security code.</span></span> <span data-ttu-id="b3cf2-261"> (这是一个随机数字。) 您需要在服务上缓存此代码，以及通过登录流获取的凭据 (如 OAuth 2.0 令牌) 。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-261">(This can be a random number.) You need to cache this code on your service, along with the credentials obtained through the sign-in flow (such as OAuth 2.0 tokens).</span></span>
2. <span data-ttu-id="b3cf2-262">调用 `microsoftTeams.authentication.notifySuccess` 并传递安全代码。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-262">Call `microsoftTeams.authentication.notifySuccess` and pass the security code.</span></span>

<span data-ttu-id="b3cf2-263">此时，窗口关闭，控制权将传递给 Teams 客户端。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-263">At this point, the window closes and control is passed to the Teams client.</span></span> <span data-ttu-id="b3cf2-264">客户端现在可以重新发送原始用户查询以及 属性中的安全 `state` 代码。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-264">The client now can reissue the original user query, along with the security code in the `state` property.</span></span> <span data-ttu-id="b3cf2-265">代码可以使用安全代码查找之前存储的凭据以完成身份验证序列，然后完成用户请求。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-265">Your code can use the security code to look up the credentials stored earlier to complete the authentication sequence and then complete the user request.</span></span>

#### <a name="reissued-request-example"></a><span data-ttu-id="b3cf2-266">重新请求示例</span><span class="sxs-lookup"><span data-stu-id="b3cf2-266">Reissued request example</span></span>

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

## <a name="sdk-support"></a><span data-ttu-id="b3cf2-267">SDK 支持</span><span class="sxs-lookup"><span data-stu-id="b3cf2-267">SDK support</span></span>

### <a name="net"></a><span data-ttu-id="b3cf2-268">.NET</span><span class="sxs-lookup"><span data-stu-id="b3cf2-268">.NET</span></span>

<span data-ttu-id="b3cf2-269">若要使用适用于 .NET 的 Bot Builder SDK 接收和处理查询，可以检查传入活动上的操作类型，然后使用 NuGet 程序包 `invoke` [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) 中的帮助程序方法确定它是否是消息传递扩展活动。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-269">To receive and handle queries with the Bot Builder SDK for .NET, you can check for the `invoke` action type on the incoming activity and then use the helper method in the NuGet package [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) to determine whether it’s a messaging extension activity.</span></span>

#### <a name="example-code-in-net"></a><span data-ttu-id="b3cf2-270">.NET 中的示例代码</span><span class="sxs-lookup"><span data-stu-id="b3cf2-270">Example code in .NET</span></span>

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

### <a name="nodejs"></a><span data-ttu-id="b3cf2-271">Node.js</span><span class="sxs-lookup"><span data-stu-id="b3cf2-271">Node.js</span></span>

#### <a name="example-code-in-nodejs"></a><span data-ttu-id="b3cf2-272">示例代码中Node.js</span><span class="sxs-lookup"><span data-stu-id="b3cf2-272">Example code in Node.js</span></span>

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
<span data-ttu-id="b3cf2-273">*另请参阅* [Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="b3cf2-273">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>
