---
title: 为会议启用和配置Teams应用程序
author: surbhigupta
description: 为会议启用和配置Teams应用程序
ms.topic: conceptual
ms.openlocfilehash: e31e241a61f40a8dc2b8a1221765bd4755d346ed
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068639"
---
# <a name="enable-and-configure-your-apps-for-teams-meetings"></a><span data-ttu-id="3df03-103">为会议启用和配置Teams应用程序</span><span class="sxs-lookup"><span data-stu-id="3df03-103">Enable and configure your apps for Teams meetings</span></span>

<span data-ttu-id="3df03-104">每个团队都有不同的通信和协作任务方式。</span><span class="sxs-lookup"><span data-stu-id="3df03-104">Every team has a different way of communicating and collaborating tasks.</span></span> <span data-ttu-id="3df03-105">可以通过使用会议应用自定义Teams实现这些不同的任务。</span><span class="sxs-lookup"><span data-stu-id="3df03-105">You can achieve these different tasks by customizing Teams with apps for meetings.</span></span> <span data-ttu-id="3df03-106">若要自定义和完成不同的任务，必须启用用于会议Teams应用程序，并在其应用清单内将应用配置为在会议范围内可用。</span><span class="sxs-lookup"><span data-stu-id="3df03-106">To customize and to achieve different tasks, you must enable your apps for Teams meetings and configure your apps to be available in meeting scope within their app manifest.</span></span>

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="3df03-107">为应用启用Teams会议</span><span class="sxs-lookup"><span data-stu-id="3df03-107">Enable your app for Teams meetings</span></span>

<span data-ttu-id="3df03-108">若要为应用启用Teams会议，必须更新应用清单，并使用上下文属性确定应用必须出现在何处。</span><span class="sxs-lookup"><span data-stu-id="3df03-108">To enable your app for Teams meetings, you must update your app manifest and use the context properties to determine where your app must appear.</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="3df03-109">更新应用清单</span><span class="sxs-lookup"><span data-stu-id="3df03-109">Update your app manifest</span></span>

<span data-ttu-id="3df03-110">会议应用功能使用 、 和 数组在应用清单 `configurableTabs` `scopes` `context` 中声明。</span><span class="sxs-lookup"><span data-stu-id="3df03-110">The meetings app capabilities are declared in your app manifest using the `configurableTabs`, `scopes`, and `context` arrays.</span></span> <span data-ttu-id="3df03-111">范围定义谁，上下文定义你的应用的可用位置。</span><span class="sxs-lookup"><span data-stu-id="3df03-111">Scope defines to whom and context defines where your app is available.</span></span>

> [!NOTE]
> * <span data-ttu-id="3df03-112">尝试使用清单架构更新 [应用清单](../resources/schema/manifest-schema-dev-preview.md)。</span><span class="sxs-lookup"><span data-stu-id="3df03-112">Try updating your app manifest with the [manifest schema](../resources/schema/manifest-schema-dev-preview.md).</span></span>
> * <span data-ttu-id="3df03-113">会议中的应用程序需要群聊范围。</span><span class="sxs-lookup"><span data-stu-id="3df03-113">Apps in meetings require groupchat scope.</span></span> <span data-ttu-id="3df03-114">团队作用域仅适用于频道中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="3df03-114">The team scope works for tabs in channels only.</span></span>

<span data-ttu-id="3df03-115">应用程序清单必须包含以下代码段：</span><span class="sxs-lookup"><span data-stu-id="3df03-115">The app manifest must include the following code snippet:</span></span>

```json

"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "team",
        "groupchat"
      ],
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```

> [!NOTE]
> <span data-ttu-id="3df03-116">`meetingStage` 当前仅适用于开发人员 [预览](../resources/dev-preview/developer-preview-intro.md) 版。</span><span class="sxs-lookup"><span data-stu-id="3df03-116">`meetingStage` is currently available in [developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

### <a name="context-property"></a><span data-ttu-id="3df03-117">Context 属性</span><span class="sxs-lookup"><span data-stu-id="3df03-117">Context property</span></span>

<span data-ttu-id="3df03-118">属性确定当用户在会议调用应用时必须显示哪些内容，具体取决于用户 `context` 调用该应用的地方。</span><span class="sxs-lookup"><span data-stu-id="3df03-118">The `context` property determines what must be shown when a user invokes an app in a meeting depending on where the user invokes the app.</span></span> <span data-ttu-id="3df03-119">选项卡 `context` 和 `scopes` 属性使你可以确定应用必须出现在何处。</span><span class="sxs-lookup"><span data-stu-id="3df03-119">The tab `context` and `scopes` properties enable you to determine where your app must appear.</span></span> <span data-ttu-id="3df03-120">或 作用域 `team` `groupchat` 中的选项卡可以具有多个上下文。</span><span class="sxs-lookup"><span data-stu-id="3df03-120">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="3df03-121">以下是可以使用所有或部分 `context` 值的 属性的值：</span><span class="sxs-lookup"><span data-stu-id="3df03-121">Following are the values for the `context` property from which you can use all or some of the values:</span></span>

|<span data-ttu-id="3df03-122">值</span><span class="sxs-lookup"><span data-stu-id="3df03-122">Value</span></span>|<span data-ttu-id="3df03-123">说明</span><span class="sxs-lookup"><span data-stu-id="3df03-123">Description</span></span>|
|---|---|
| <span data-ttu-id="3df03-124">**channelTab**</span><span class="sxs-lookup"><span data-stu-id="3df03-124">**channelTab**</span></span> | <span data-ttu-id="3df03-125">团队频道标题中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="3df03-125">A tab in the header of a team channel.</span></span> |
| <span data-ttu-id="3df03-126">**privateChatTab**</span><span class="sxs-lookup"><span data-stu-id="3df03-126">**privateChatTab**</span></span> | <span data-ttu-id="3df03-127">一组用户之间的群聊标题中的选项卡，不在团队或会议上下文中。</span><span class="sxs-lookup"><span data-stu-id="3df03-127">A tab in the header of a group chat between a set of users, not in the context of a team or meeting.</span></span> |
| <span data-ttu-id="3df03-128">**meetingChatTab**</span><span class="sxs-lookup"><span data-stu-id="3df03-128">**meetingChatTab**</span></span> | <span data-ttu-id="3df03-129">计划会议上下文中的一组用户之间的群聊标题中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="3df03-129">A tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span> |
| <span data-ttu-id="3df03-130">**meetingDetailsTab**</span><span class="sxs-lookup"><span data-stu-id="3df03-130">**meetingDetailsTab**</span></span> | <span data-ttu-id="3df03-131">日历的会议详细信息视图标题中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="3df03-131">A tab in the header of the meeting details view of the calendar.</span></span> |
| <span data-ttu-id="3df03-132">**meetingSidePanel**</span><span class="sxs-lookup"><span data-stu-id="3df03-132">**meetingSidePanel**</span></span> | <span data-ttu-id="3df03-133">通过统一栏打开的会议内面板 (U 条形图) 。</span><span class="sxs-lookup"><span data-stu-id="3df03-133">An in-meeting panel opened through the unified bar (U-bar).</span></span> |
| <span data-ttu-id="3df03-134">**meetingStage**</span><span class="sxs-lookup"><span data-stu-id="3df03-134">**meetingStage**</span></span> | <span data-ttu-id="3df03-135">meetingSidePanel 中的应用可以共享到会议阶段。</span><span class="sxs-lookup"><span data-stu-id="3df03-135">An app from the meetingSidePanel can be shared to the meeting stage.</span></span> |

> [!NOTE]
> <span data-ttu-id="3df03-136">`Context` 属性当前在移动客户端上不受支持。</span><span class="sxs-lookup"><span data-stu-id="3df03-136">`Context` property is currently not supported on mobile clients.</span></span>

<span data-ttu-id="3df03-137">为会议启用应用Teams，必须在会议前、会议期间和会议后配置应用。</span><span class="sxs-lookup"><span data-stu-id="3df03-137">After you enable your app for Teams meetings, you must configure your app before a meeting, during a meeting, and after a meeting.</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="3df03-138">为会议方案配置应用</span><span class="sxs-lookup"><span data-stu-id="3df03-138">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="3df03-139">若要使应用在选项卡库中可见，它必须支持可配置的选项卡和群聊范围。</span><span class="sxs-lookup"><span data-stu-id="3df03-139">For your app to be visible in the tab gallery, it must support configurable tabs and the group chat scope.</span></span>
> * <span data-ttu-id="3df03-140">移动客户端仅在会议前和会议后阶段支持选项卡。</span><span class="sxs-lookup"><span data-stu-id="3df03-140">Mobile clients support tabs only in pre and post meeting stages.</span></span>
> * <span data-ttu-id="3df03-141">移动客户端当前不支持会议内对话框和选项卡中的会议体验。</span><span class="sxs-lookup"><span data-stu-id="3df03-141">The in-meeting experiences that is in-meeting dialog box and tab is currently not supported on mobile clients.</span></span> <span data-ttu-id="3df03-142">有关详细信息，请参阅 [为移动设备创建选项卡](../tabs/design/tabs-mobile.md) 时有关移动选项卡的指南。</span><span class="sxs-lookup"><span data-stu-id="3df03-142">For more information, see [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) while creating your tabs for mobile.</span></span>

<span data-ttu-id="3df03-143">Teams会议可为组织提供独特的协作体验。</span><span class="sxs-lookup"><span data-stu-id="3df03-143">Teams meetings provides a unique collaborative experience for your organization.</span></span> <span data-ttu-id="3df03-144">它提供了为不同的会议方案配置应用的机会。</span><span class="sxs-lookup"><span data-stu-id="3df03-144">It provides the opportunity to configure your app for different meeting scenarios.</span></span> <span data-ttu-id="3df03-145">你可以配置应用，以基于参与者角色或用户类型增强会议体验。</span><span class="sxs-lookup"><span data-stu-id="3df03-145">You can configure your apps to enhance the meeting experience based on participant role or user type.</span></span> <span data-ttu-id="3df03-146">现在，您可以确定可以在以下会议方案中执行哪些操作：</span><span class="sxs-lookup"><span data-stu-id="3df03-146">Now you can identify what actions can be taken in the following meeting scenarios:</span></span>
* [<span data-ttu-id="3df03-147">会议前</span><span class="sxs-lookup"><span data-stu-id="3df03-147">Pre-meeting</span></span>](#pre-meeting)
* [<span data-ttu-id="3df03-148">会议内</span><span class="sxs-lookup"><span data-stu-id="3df03-148">In-meeting</span></span>](#in-meeting)
* [<span data-ttu-id="3df03-149">会议后</span><span class="sxs-lookup"><span data-stu-id="3df03-149">Post-meeting</span></span>](#post-meeting)

### <a name="pre-meeting"></a><span data-ttu-id="3df03-150">会议前</span><span class="sxs-lookup"><span data-stu-id="3df03-150">Pre-meeting</span></span>

<span data-ttu-id="3df03-151">在会议之前，用户可以添加选项卡、聊天机器人和消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="3df03-151">Before a meeting, users can add tabs, bots, and messaging extensions.</span></span> <span data-ttu-id="3df03-152">具有组织者和演示者角色的用户可以向会议添加选项卡。</span><span class="sxs-lookup"><span data-stu-id="3df03-152">Users with organizer and presenter roles can add tabs to a meeting.</span></span>

<span data-ttu-id="3df03-153">**向会议添加选项卡**</span><span class="sxs-lookup"><span data-stu-id="3df03-153">**To add a tab to a meeting**</span></span>

1. <span data-ttu-id="3df03-154">在日历中，选择要添加选项卡的会议。</span><span class="sxs-lookup"><span data-stu-id="3df03-154">In your calendar, select a meeting to which you want to add a tab.</span></span>
1. <span data-ttu-id="3df03-155">选择" **详细信息"** 选项卡并选择</span><span class="sxs-lookup"><span data-stu-id="3df03-155">Select the **Details** tab and select</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="3df03-156">.</span><span class="sxs-lookup"><span data-stu-id="3df03-156">.</span></span>

    ![会议前体验](../assets/images/apps-in-meetings/PreMeeting.png)

1. <span data-ttu-id="3df03-158">在出现的选项卡库中，选择要添加的应用并按照所需步骤操作。</span><span class="sxs-lookup"><span data-stu-id="3df03-158">In the tab gallery that appears, select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="3df03-159">应用作为选项卡安装。</span><span class="sxs-lookup"><span data-stu-id="3df03-159">The app is installed as a tab.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3df03-160">目前，在"会议"选项卡中，不支持获取会议详细信息和参与者信息。</span><span class="sxs-lookup"><span data-stu-id="3df03-160">Currently, in meetings tab, getting meeting details and participant information is not supported.</span></span>

<span data-ttu-id="3df03-161">**将消息传递扩展添加到会议**</span><span class="sxs-lookup"><span data-stu-id="3df03-161">**To add a messaging extension to a meeting**</span></span>

1. <span data-ttu-id="3df03-162">选择位于 &#x25CF;&#x25CF;&#x25CF; 撰写消息区域中的省略号。</span><span class="sxs-lookup"><span data-stu-id="3df03-162">Select the ellipses &#x25CF;&#x25CF;&#x25CF; located in the compose message area in the chat.</span></span>
1. <span data-ttu-id="3df03-163">选择要添加的应用并按照所需步骤操作。</span><span class="sxs-lookup"><span data-stu-id="3df03-163">Select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="3df03-164">应用作为消息传递扩展进行安装。</span><span class="sxs-lookup"><span data-stu-id="3df03-164">The app is installed as a messaging extension.</span></span>

<span data-ttu-id="3df03-165">**将机器人添加到会议**</span><span class="sxs-lookup"><span data-stu-id="3df03-165">**To add a bot to a meeting**</span></span>

<span data-ttu-id="3df03-166">在会议聊天中，输入 **@** 密钥并选择"**获取机器人"。**</span><span class="sxs-lookup"><span data-stu-id="3df03-166">In a meeting chat, enter the **@** key and select **Get bots**.</span></span>

> [!NOTE]
> * <span data-ttu-id="3df03-167">必须使用选项卡 SSO 确认 [用户标识](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="3df03-167">The user identity must be confirmed using [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="3df03-168">身份验证后，应用可以使用 API 检索用户 `GetParticipant` 角色。</span><span class="sxs-lookup"><span data-stu-id="3df03-168">After authentication, the app can retrieve the user role using the `GetParticipant` API.</span></span>
> * <span data-ttu-id="3df03-169">根据用户角色，应用能够提供特定于角色的体验。</span><span class="sxs-lookup"><span data-stu-id="3df03-169">Based on the user role, the app has the capability to provide role specific experiences.</span></span> <span data-ttu-id="3df03-170">例如，轮询应用仅允许组织者和演示者创建新的轮询。</span><span class="sxs-lookup"><span data-stu-id="3df03-170">For example, a polling app allows only organizers and presenters to create a new poll.</span></span>
> * <span data-ttu-id="3df03-171">可以在会议进行时更改角色分配。</span><span class="sxs-lookup"><span data-stu-id="3df03-171">Role assignments can be changed while a meeting is in progress.</span></span> <span data-ttu-id="3df03-172">有关详细信息，请参阅[会议Teams角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。</span><span class="sxs-lookup"><span data-stu-id="3df03-172">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

### <a name="in-meeting"></a><span data-ttu-id="3df03-173">会议内</span><span class="sxs-lookup"><span data-stu-id="3df03-173">In-meeting</span></span>

<span data-ttu-id="3df03-174">在会议期间，可以使用 meetingSidePanel 或会议内对话框为应用构建独特的体验。</span><span class="sxs-lookup"><span data-stu-id="3df03-174">During a meeting, you can use the meetingSidePanel or the in-meeting dialog box to build unique experiences for your apps.</span></span>

#### <a name="meetingsidepanel"></a><span data-ttu-id="3df03-175">meetingSidePanel</span><span class="sxs-lookup"><span data-stu-id="3df03-175">meetingSidePanel</span></span>

<span data-ttu-id="3df03-176">使用 meetingSidePanel，你可以自定义会议体验，使组织者和演示者拥有一组不同的视图和操作。</span><span class="sxs-lookup"><span data-stu-id="3df03-176">With the meetingSidePanel, you can customize experiences in a meeting that enable organizers and presenters to have different set of views and actions.</span></span> <span data-ttu-id="3df03-177">在应用清单中，必须将 meetingSidePanel 添加到上下文数组。</span><span class="sxs-lookup"><span data-stu-id="3df03-177">In your app manifest, you must add meetingSidePanel to the context array.</span></span> <span data-ttu-id="3df03-178">在会议以及所有方案中，应用在宽度为 320 像素的"会议内"选项卡中呈现。</span><span class="sxs-lookup"><span data-stu-id="3df03-178">In the meeting and in all scenarios, the app is rendered in an in-meeting tab that is 320 pixels in width.</span></span> <span data-ttu-id="3df03-179">有关详细信息，请参阅 [FrameContext 接口](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="3df03-179">For more information, see [FrameContext interface](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true).</span></span>

<span data-ttu-id="3df03-180">若要使用 `userContext` API 相应地路由请求，请参阅[Teams SDK。](../tabs/how-to/access-teams-context.md#user-context)</span><span class="sxs-lookup"><span data-stu-id="3df03-180">To use the `userContext` API to route requests accordingly, see [Teams SDK](../tabs/how-to/access-teams-context.md#user-context).</span></span> <span data-ttu-id="3df03-181">有关详细信息，请参阅Teams[身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="3df03-181">For more information, see [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="3df03-182">选项卡的身份验证流与网站的身份验证流非常相似。</span><span class="sxs-lookup"><span data-stu-id="3df03-182">Authentication flow for tabs is very similar to the authentication flow for websites.</span></span> <span data-ttu-id="3df03-183">因此选项卡可以直接使用 OAuth 2.0。</span><span class="sxs-lookup"><span data-stu-id="3df03-183">So tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="3df03-184">有关详细信息，请参阅 Microsoft 标识平台[和 OAuth 2.0 授权代码流](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。</span><span class="sxs-lookup"><span data-stu-id="3df03-184">For more information, see [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="3df03-185">当用户在会议视图中时，邮件扩展按预期方式工作，用户可以发布撰写邮件扩展卡。</span><span class="sxs-lookup"><span data-stu-id="3df03-185">Messaging extension works as expected when a user is in an in-meeting view, and the user can post compose message extension cards.</span></span> <span data-ttu-id="3df03-186">AppName 会议内是一个工具提示，用于指出会议 U 栏中的应用名称。</span><span class="sxs-lookup"><span data-stu-id="3df03-186">AppName in-meeting is a tooltip that states the app name in-meeting U-bar.</span></span>

> [!NOTE]
> <span data-ttu-id="3df03-187">使用版本 1.7.0 或更高版本[的 Teams SDK，](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)因为它之前的版本不支持侧面板。</span><span class="sxs-lookup"><span data-stu-id="3df03-187">Use version 1.7.0 or higher of [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), as versions prior to it do not support the side panel.</span></span>

#### <a name="in-meeting-dialog-box"></a><span data-ttu-id="3df03-188">"会议内"对话框</span><span class="sxs-lookup"><span data-stu-id="3df03-188">In-meeting dialog box</span></span>

<span data-ttu-id="3df03-189">会议内对话框可用于在会议期间与参与者互动，并收集会议期间的信息或反馈。</span><span class="sxs-lookup"><span data-stu-id="3df03-189">The in-meeting dialog box can be used to engage participants during the meeting and collect information or feedback during the meeting.</span></span> <span data-ttu-id="3df03-190">使用 [`NotificationSignal`](create-apps-for-teams-meetings.md#notificationsignal-api) API 指示必须触发气泡通知。</span><span class="sxs-lookup"><span data-stu-id="3df03-190">Use the [`NotificationSignal`](create-apps-for-teams-meetings.md#notificationsignal-api) API to signal that a bubble notification must be triggered.</span></span> <span data-ttu-id="3df03-191">作为通知请求有效负载的一部分，请包含要显示内容的托管 URL。</span><span class="sxs-lookup"><span data-stu-id="3df03-191">As part of the notification request payload, include the URL where the content to be shown is hosted.</span></span>

<span data-ttu-id="3df03-192">会议内对话框不得使用任务模块。</span><span class="sxs-lookup"><span data-stu-id="3df03-192">In-meeting dialog must not use task module.</span></span> <span data-ttu-id="3df03-193">会议聊天中不会调用任务模块。</span><span class="sxs-lookup"><span data-stu-id="3df03-193">Task module is not invoked in a meeting chat.</span></span> <span data-ttu-id="3df03-194">外部资源 URL 用于在会议中显示内容气泡。</span><span class="sxs-lookup"><span data-stu-id="3df03-194">An external resource URL is used to display content bubble in a meeting.</span></span> <span data-ttu-id="3df03-195">可以使用 方法 `submitTask` 在会议聊天中提交数据。</span><span class="sxs-lookup"><span data-stu-id="3df03-195">You can use the `submitTask` method to submit data in a meeting chat.</span></span>

> [!NOTE]
> * <span data-ttu-id="3df03-196">您必须调用 [submitTask () ](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 函数，以在用户执行 Web 视图中的操作后自动消除。</span><span class="sxs-lookup"><span data-stu-id="3df03-196">You must invoke the [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to dismiss automatically after a user takes an action in the web view.</span></span> <span data-ttu-id="3df03-197">这是应用提交的要求。</span><span class="sxs-lookup"><span data-stu-id="3df03-197">This is a requirement for app submission.</span></span> <span data-ttu-id="3df03-198">有关详细信息，请参阅Teams [SDK 任务模块](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="3df03-198">For more information, see [Teams SDK task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
> * <span data-ttu-id="3df03-199">如果希望你的应用支持匿名用户，则初始调用请求有效负载必须依赖于 对象中的请求元数据， `from.id` `from` 而不是 `from.aadObjectId` 请求元数据。</span><span class="sxs-lookup"><span data-stu-id="3df03-199">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id` request metadata in the `from` object, not the `from.aadObjectId` request metadata.</span></span> <span data-ttu-id="3df03-200">`from.id`是用户 `from.aadObjectId` ID，也是Azure Active Directory (AAD) ID。</span><span class="sxs-lookup"><span data-stu-id="3df03-200">`from.id` is the user ID and `from.aadObjectId` is the Azure Active Directory (AAD) ID of the user.</span></span> <span data-ttu-id="3df03-201">有关详细信息，请参阅在 [选项卡中使用任务模块](../task-modules-and-cards/task-modules/task-modules-tabs.md) 以及 [创建和发送任务模块](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)。</span><span class="sxs-lookup"><span data-stu-id="3df03-201">For more information, see [using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

#### <a name="share-to-stage"></a><span data-ttu-id="3df03-202">共享到阶段</span><span class="sxs-lookup"><span data-stu-id="3df03-202">Share to stage</span></span>

> [!NOTE]
> * <span data-ttu-id="3df03-203">此功能目前仅适用于开发人员 [预览](../resources/dev-preview/developer-preview-intro.md) 版。</span><span class="sxs-lookup"><span data-stu-id="3df03-203">This capability is currently available in [developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>
> * <span data-ttu-id="3df03-204">若要使用此功能，应用必须支持会议内 meetingSidePanel。</span><span class="sxs-lookup"><span data-stu-id="3df03-204">To use this feature, the app must support an in-meeting meetingSidePanel.</span></span>

<span data-ttu-id="3df03-205">此功能使开发人员能够将应用共享到会议阶段。</span><span class="sxs-lookup"><span data-stu-id="3df03-205">This capability gives developers the ability to share an app to the meeting stage.</span></span> <span data-ttu-id="3df03-206">通过启用共享到会议阶段，会议参与者可以实时协作。</span><span class="sxs-lookup"><span data-stu-id="3df03-206">By enabling share to the meeting stage, meeting participants can collaborate in real-time.</span></span>

<span data-ttu-id="3df03-207">必需的上下文 `meetingStage` 位于应用程序清单中。</span><span class="sxs-lookup"><span data-stu-id="3df03-207">The required context is `meetingStage` in the app manifest.</span></span> <span data-ttu-id="3df03-208">这样做的先决条件是拥有 `meetingSidePanel` 上下文。</span><span class="sxs-lookup"><span data-stu-id="3df03-208">A prerequisite for this is to have the `meetingSidePanel` context.</span></span> <span data-ttu-id="3df03-209">这将在 meetingSidePanel 中启用"共享"。</span><span class="sxs-lookup"><span data-stu-id="3df03-209">This enables **Share** in the meetingSidePanel.</span></span>

![在会议体验期间共享到阶段](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

<span data-ttu-id="3df03-211">启用此功能所需的清单更改如下所示：</span><span class="sxs-lookup"><span data-stu-id="3df03-211">The manifest change that is needed to enable this capability is as follows:</span></span>

```json
"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "groupchat"
      ],
      "context":[
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```

### <a name="post-meeting"></a><span data-ttu-id="3df03-212">会议后</span><span class="sxs-lookup"><span data-stu-id="3df03-212">Post-meeting</span></span>

<span data-ttu-id="3df03-213">会议后和 [会议前](#pre-meeting) 配置相同。</span><span class="sxs-lookup"><span data-stu-id="3df03-213">The post-meeting and [pre-meeting](#pre-meeting) configurations are the same.</span></span>

## <a name="code-sample"></a><span data-ttu-id="3df03-214">代码示例</span><span class="sxs-lookup"><span data-stu-id="3df03-214">Code sample</span></span>

|<span data-ttu-id="3df03-215">示例名称</span><span class="sxs-lookup"><span data-stu-id="3df03-215">Sample name</span></span> | <span data-ttu-id="3df03-216">说明</span><span class="sxs-lookup"><span data-stu-id="3df03-216">Description</span></span> | <span data-ttu-id="3df03-217">示例</span><span class="sxs-lookup"><span data-stu-id="3df03-217">Sample</span></span> |
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="3df03-218">会议应用程序</span><span class="sxs-lookup"><span data-stu-id="3df03-218">Meeting app</span></span> | <span data-ttu-id="3df03-219">演示如何使用会议令牌生成器应用请求令牌，该令牌按顺序生成，以便每个参与者都有机会进行互动。</span><span class="sxs-lookup"><span data-stu-id="3df03-219">Demonstrates how to use the Meeting Token Generator app to request a token, which is generated sequentially so that each participant has a fair opportunity to interact.</span></span> <span data-ttu-id="3df03-220">这可用于 scrum 会议、问答&等情况。</span><span class="sxs-lookup"><span data-stu-id="3df03-220">This can be useful in situations like scrum meetings, Q&A sessions, and so on.</span></span> | [<span data-ttu-id="3df03-221">View</span><span class="sxs-lookup"><span data-stu-id="3df03-221">View</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token) |

## <a name="see-also"></a><span data-ttu-id="3df03-222">另请参阅</span><span class="sxs-lookup"><span data-stu-id="3df03-222">See also</span></span>

* [<span data-ttu-id="3df03-223">会议内对话设计指南</span><span class="sxs-lookup"><span data-stu-id="3df03-223">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [<span data-ttu-id="3df03-224">Teams选项卡的身份验证流</span><span class="sxs-lookup"><span data-stu-id="3df03-224">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)
