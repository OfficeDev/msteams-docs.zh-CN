---
title: 使用 RSC 接收所有频道消息
author: surbhigupta12
description: 接收具有 RSC 权限的所有频道消息
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 833bdbc015cf852fcd899ce4e75f742448b89978
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631269"
---
# <a name="receive-all-channel-messages-with-rsc"></a><span data-ttu-id="70590-103">使用 RSC 接收所有频道消息</span><span class="sxs-lookup"><span data-stu-id="70590-103">Receive all channel messages with RSC</span></span>

> [!NOTE]
> <span data-ttu-id="70590-104">此功能目前仅适用于公共 [开发人员预览](../../../resources/dev-preview/developer-preview-intro.md) 版。</span><span class="sxs-lookup"><span data-stu-id="70590-104">This feature is currently available in [public developer preview](../../../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="70590-105">RSC (权限) （最初为 Teams Graph API 开发）的特定资源许可现在扩展到自动程序方案。</span><span class="sxs-lookup"><span data-stu-id="70590-105">The resource-specific consent (RSC) permissions model, originally developed for Teams Graph APIs, is now extended to bot scenarios.</span></span>

<span data-ttu-id="70590-106">目前，自动程序仅在收到用户频道消息时才能收到@mentioned。</span><span class="sxs-lookup"><span data-stu-id="70590-106">Currently, bots can only receive user channel messages when they are @mentioned.</span></span> <span data-ttu-id="70590-107">使用 RSC，你现在可以请求团队所有者同意自动程序在团队中跨标准频道接收用户消息，而无需@mentioned。</span><span class="sxs-lookup"><span data-stu-id="70590-107">Using RSC, you can now request team owners to consent for a bot to receive user messages across standard channels in a team without being @mentioned.</span></span> <span data-ttu-id="70590-108">此功能通过指定已启用 RSC 的应用清单中的权限Teams `ChannelMessage.Read.Group` 启用。</span><span class="sxs-lookup"><span data-stu-id="70590-108">This capability is enabled by specifying the `ChannelMessage.Read.Group` permission in the manifest of an RSC enabled Teams app.</span></span> <span data-ttu-id="70590-109">配置完成后，团队所有者可以在应用安装过程中授予同意。</span><span class="sxs-lookup"><span data-stu-id="70590-109">After configuration, team owners can grant consent during the app installation process.</span></span>

<span data-ttu-id="70590-110">有关为应用启用 RSC 的信息，请参阅 Teams 中[特定于资源Teams。](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest)</span><span class="sxs-lookup"><span data-stu-id="70590-110">For more information about enabling RSC for your app, see [resource-specific consent in Teams](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest).</span></span>

## <a name="enable-bots-to-receive-all-channel-messages"></a><span data-ttu-id="70590-111">使机器人能够接收所有频道消息</span><span class="sxs-lookup"><span data-stu-id="70590-111">Enable bots to receive all channel messages</span></span>

<span data-ttu-id="70590-112">`ChannelMessage.Read.Group`RSC 权限扩展到机器人。</span><span class="sxs-lookup"><span data-stu-id="70590-112">The `ChannelMessage.Read.Group` RSC permission is extended to bots.</span></span> <span data-ttu-id="70590-113">征得用户同意后，此权限允许图形应用程序获取对话中的所有消息，并允许聊天机器人接收所有频道消息，而无需@mentioned。</span><span class="sxs-lookup"><span data-stu-id="70590-113">With user consent, this permission allows graph applications to get all messages in a conversation and bots to receive all channel messages without being @mentioned.</span></span>

## <a name="update-app-manifest"></a><span data-ttu-id="70590-114">更新应用清单</span><span class="sxs-lookup"><span data-stu-id="70590-114">Update app manifest</span></span>

<span data-ttu-id="70590-115">若要使机器人接收所有频道消息，必须在应用清单中配置 RSC Teams属性中 `ChannelMessage.Read.Group` 指定 `webApplicationInfo` 的权限。</span><span class="sxs-lookup"><span data-stu-id="70590-115">For your bot to receive all channel messages, RSC must be configured in the Teams app manifest with the `ChannelMessage.Read.Group` permission specified in the `webApplicationInfo` property.</span></span>

![更新应用清单](~/bots/how-to/conversations/Media/appmanifest.png)

<span data-ttu-id="70590-117">以下是对象 `webApplicationInfo` 的示例：</span><span class="sxs-lookup"><span data-stu-id="70590-117">The following is an example of the `webApplicationInfo` object:</span></span>

* <span data-ttu-id="70590-118">**id**：你的Azure Active Directory (AAD) 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="70590-118">**id**: Your Azure Active Directory (AAD) app ID.</span></span> <span data-ttu-id="70590-119">它可以与自动程序 ID 相同。</span><span class="sxs-lookup"><span data-stu-id="70590-119">This can be the same as your bot ID.</span></span>
* <span data-ttu-id="70590-120">**resource**：任何字符串。</span><span class="sxs-lookup"><span data-stu-id="70590-120">**resource**: Any string.</span></span> <span data-ttu-id="70590-121">此字段在 RSC 中没有任何操作，但必须添加且具有值以避免错误响应。</span><span class="sxs-lookup"><span data-stu-id="70590-121">This field has no operation in RSC, but must be added and have a value to avoid error response.</span></span>
* <span data-ttu-id="70590-122">**applicationPermissions：** 必须指定应用的 RSC `ChannelMessage.Read.Group` 权限。</span><span class="sxs-lookup"><span data-stu-id="70590-122">**applicationPermissions**: RSC permissions for your app with `ChannelMessage.Read.Group` must be specified.</span></span> <span data-ttu-id="70590-123">有关详细信息，请参阅特定于 [资源的权限](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="70590-123">For more information, see [resource-specific permissions](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions).</span></span>

<span data-ttu-id="70590-124">以下代码提供了应用清单的示例：</span><span class="sxs-lookup"><span data-stu-id="70590-124">The following code provides an example of the app manifest:</span></span>

```json
"webApplicationInfo": {
"id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
"resource": "https://AnyString",
"applicationPermissions": [
"ChannelMessage.Read.Group"
    ]
  }
```

## <a name="sideload-in-a-team-to-test"></a><span data-ttu-id="70590-125">在团队中旁加载以进行测试</span><span class="sxs-lookup"><span data-stu-id="70590-125">Sideload in a team to test</span></span>

<span data-ttu-id="70590-126">若要在团队中旁加载以进行测试，是否收到具有 RSC 的团队中所有频道消息，而不@mentioned：</span><span class="sxs-lookup"><span data-stu-id="70590-126">To sideload in a team to test, whether all channel messages in a team with RSC are received without being @mentioned:</span></span>

1. <span data-ttu-id="70590-127">选择或创建团队。</span><span class="sxs-lookup"><span data-stu-id="70590-127">Select or create a team.</span></span>
1. <span data-ttu-id="70590-128">从左窗格中选择 &#x25CF;&#x25CF;&#x25CF; 省略号。</span><span class="sxs-lookup"><span data-stu-id="70590-128">Select the ellipses &#x25CF;&#x25CF;&#x25CF; from the left pane.</span></span> <span data-ttu-id="70590-129">将显示下拉菜单。</span><span class="sxs-lookup"><span data-stu-id="70590-129">The drop-down menu appears.</span></span>
1. <span data-ttu-id="70590-130">从 **下拉菜单中选择** "管理团队"。</span><span class="sxs-lookup"><span data-stu-id="70590-130">Select **Manage team** from the drop-down menu.</span></span> <span data-ttu-id="70590-131">将显示详细信息。</span><span class="sxs-lookup"><span data-stu-id="70590-131">The details appear.</span></span>

   ![管理团队中的应用](~/bots/how-to/conversations/Media/managingteam.png)

1. <span data-ttu-id="70590-133">选择“**应用**”。</span><span class="sxs-lookup"><span data-stu-id="70590-133">Select **Apps**.</span></span> <span data-ttu-id="70590-134">将显示多个应用。</span><span class="sxs-lookup"><span data-stu-id="70590-134">Multiple apps appear.</span></span>
1. <span data-ttu-id="70590-135">从 **Upload右下角** 选择自定义应用。</span><span class="sxs-lookup"><span data-stu-id="70590-135">Select **Upload a custom app** from the lower right corner.</span></span>

    ![上载自定义应用](~/bots/how-to/conversations/Media/uploadingcustomapp.png)

1. <span data-ttu-id="70590-137">从"打开"对话框中 **选择应用** 包。</span><span class="sxs-lookup"><span data-stu-id="70590-137">Select the app package from the **Open** dialog box.</span></span>
1. <span data-ttu-id="70590-138">选择 **“打开”**。</span><span class="sxs-lookup"><span data-stu-id="70590-138">Select **Open**.</span></span>

    ![选择应用包](~/bots/how-to/conversations/Media/selectapppackage.png)

1. <span data-ttu-id="70590-140">从 **应用** 详细信息弹出窗口中选择添加，将机器人添加到所选团队。</span><span class="sxs-lookup"><span data-stu-id="70590-140">Select **Add** from the app details pop-up, to add the bot to your selected team.</span></span>

    ![添加自动程序](~/bots/how-to/conversations/Media/addingbot.png)

1. <span data-ttu-id="70590-142">选择一个通道，在频道中为自动程序输入消息。</span><span class="sxs-lookup"><span data-stu-id="70590-142">Select a channel and enter a message in the channel for your bot.</span></span>

    <span data-ttu-id="70590-143">自动程序在不接收邮件的情况下接收@mentioned。</span><span class="sxs-lookup"><span data-stu-id="70590-143">The bot receives the message without being @mentioned.</span></span>

    ![机器人接收消息](~/bots/how-to/conversations/Media/botreceivingmessage.png)

## <a name="see-also"></a><span data-ttu-id="70590-145">另请参阅</span><span class="sxs-lookup"><span data-stu-id="70590-145">See also</span></span>

* [<span data-ttu-id="70590-146">智能机器人对话</span><span class="sxs-lookup"><span data-stu-id="70590-146">Bot conversations</span></span>](/microsoftteams/platform/bots/how-to/conversations/conversation-basics)
* [<span data-ttu-id="70590-147">特定于资源的同意</span><span class="sxs-lookup"><span data-stu-id="70590-147">Resource-specific consent</span></span>](/microsoftteams/resource-specific-consent)
* [<span data-ttu-id="70590-148">测试特定于资源的同意</span><span class="sxs-lookup"><span data-stu-id="70590-148">Test resource-specific consent</span></span>](/microsoftteams/platform/graph-api/rsc/test-resource-specific-consent)
* [<span data-ttu-id="70590-149">Upload自定义Teams</span><span class="sxs-lookup"><span data-stu-id="70590-149">Upload custom app in Teams</span></span>](~/concepts/deploy-and-publish/apps-upload.md)
