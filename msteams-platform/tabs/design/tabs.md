---
title: 设计桌面和 web 的选项卡
description: 了解如何设计 "团队" 选项卡 (桌面和 web) 并获取 Microsoft 团队 UI 工具包。
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 692a21c78dc86cbca5bf248e55d0332bd71c6b92
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604654"
---
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a><span data-ttu-id="3be5e-103">设计用于 Microsoft 团队桌面和 web 的选项卡</span><span class="sxs-lookup"><span data-stu-id="3be5e-103">Designing your tab for Microsoft Teams desktop and web</span></span>

<span data-ttu-id="3be5e-104">选项卡是用于便于协作的内容的大型画布。</span><span class="sxs-lookup"><span data-stu-id="3be5e-104">A tab is a large canvas for content that facilitates collaboration.</span></span> <span data-ttu-id="3be5e-105">若要指导您的应用程序设计，以下信息介绍并说明了用户如何在团队中添加、使用和管理选项卡。</span><span class="sxs-lookup"><span data-stu-id="3be5e-105">To guide your app design, the following information describes and illustrates how people can add, use, and manage tabs in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="3be5e-106">Microsoft 团队 UI 工具包</span><span class="sxs-lookup"><span data-stu-id="3be5e-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="3be5e-107">您可以在 Microsoft 团队 UI 工具包中找到全面的选项卡设计指南，包括您可以在需要时获取和修改的元素。</span><span class="sxs-lookup"><span data-stu-id="3be5e-107">You can find comprehensive tab design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="3be5e-108">UI 工具包还包含此处未介绍的辅助功能和响应大小等基本主题。</span><span class="sxs-lookup"><span data-stu-id="3be5e-108">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3be5e-109"> (Figma) 获取 Microsoft 团队 UI 工具包 </span><span class="sxs-lookup"><span data-stu-id="3be5e-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a><span data-ttu-id="3be5e-110">添加选项卡</span><span class="sxs-lookup"><span data-stu-id="3be5e-110">Add a tab</span></span>

<span data-ttu-id="3be5e-111">您可以从 "团队" 存储 ("AppSource") 或以下上下文之一添加选项卡：</span><span class="sxs-lookup"><span data-stu-id="3be5e-111">You can add a tab from the Teams store (AppSource) or in one of the following contexts:</span></span>

* <span data-ttu-id="3be5e-112">聊天</span><span class="sxs-lookup"><span data-stu-id="3be5e-112">Chat</span></span>
* <span data-ttu-id="3be5e-113">频道</span><span class="sxs-lookup"><span data-stu-id="3be5e-113">Channel</span></span>
* <span data-ttu-id="3be5e-114">会议 (之前、会议期间或会议之后) </span><span class="sxs-lookup"><span data-stu-id="3be5e-114">Meeting (before, during, or after the meeting)</span></span>

<span data-ttu-id="3be5e-115">下面的示例演示如何在通道中添加制表符。</span><span class="sxs-lookup"><span data-stu-id="3be5e-115">The following example shows how a tab is added in a channel.</span></span>

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="示例显示在通道中添加的选项卡。" border="false":::

## <a name="set-up-a-tab"></a><span data-ttu-id="3be5e-117">设置选项卡</span><span class="sxs-lookup"><span data-stu-id="3be5e-117">Set up a tab</span></span>

<span data-ttu-id="3be5e-118">有一个将应用添加为频道、聊天或会议选项卡的短安装过程。体验主要由你来掌握。</span><span class="sxs-lookup"><span data-stu-id="3be5e-118">There's a short setup process to add an app as a channel, chat, or meeting tab. The experience is largely up to you.</span></span> <span data-ttu-id="3be5e-119">例如，您可以对如何使用应用程序和一些可选设置进行说明。</span><span class="sxs-lookup"><span data-stu-id="3be5e-119">For example, you could have a description of how to use the app and some optional settings.</span></span> <span data-ttu-id="3be5e-120">如果需要对用户进行身份验证，请在此处加入登录步骤。</span><span class="sxs-lookup"><span data-stu-id="3be5e-120">Include a sign-in step here if you need to authenticate users.</span></span>

### <a name="tab-configuration-modal"></a><span data-ttu-id="3be5e-121">选项卡配置模式</span><span class="sxs-lookup"><span data-stu-id="3be5e-121">Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="示例显示了选项卡配置模式。" border="false":::

### <a name="anatomy-tab-configuration-modal"></a><span data-ttu-id="3be5e-123">剖析：选项卡配置模式</span><span class="sxs-lookup"><span data-stu-id="3be5e-123">Anatomy: Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="显示选项卡配置模式的 UI 剖析的插图。" border="false":::

|<span data-ttu-id="3be5e-125">计数器</span><span class="sxs-lookup"><span data-stu-id="3be5e-125">Counter</span></span>|<span data-ttu-id="3be5e-126">说明</span><span class="sxs-lookup"><span data-stu-id="3be5e-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="3be5e-127">1</span><span class="sxs-lookup"><span data-stu-id="3be5e-127">1</span></span>|<span data-ttu-id="3be5e-128">**应用徽标**：应用的完整颜色应用徽标。</span><span class="sxs-lookup"><span data-stu-id="3be5e-128">**App logo**: Full color app logo of your app.</span></span>|
|<span data-ttu-id="3be5e-129">2 </span><span class="sxs-lookup"><span data-stu-id="3be5e-129">2</span></span>|<span data-ttu-id="3be5e-130">**应用程序名称**：应用程序的完整名称。</span><span class="sxs-lookup"><span data-stu-id="3be5e-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="3be5e-131">3 </span><span class="sxs-lookup"><span data-stu-id="3be5e-131">3</span></span>|<span data-ttu-id="3be5e-132">**iframe**：应用内容的响应空间 (例如，选项卡设置或身份验证) 。</span><span class="sxs-lookup"><span data-stu-id="3be5e-132">**iframe**: Responsive space for your app’s content (for example, tab settings or authentication).</span></span>|
|<span data-ttu-id="3be5e-133">4 </span><span class="sxs-lookup"><span data-stu-id="3be5e-133">4</span></span>|<span data-ttu-id="3be5e-134">**关于链接**：打开一个对话框，显示有关该应用程序的详细信息，如完整说明、应用程序所需的权限以及指向您的隐私策略和服务条款的链接。</span><span class="sxs-lookup"><span data-stu-id="3be5e-134">**About link**: Opens a dialog showing more information about the app, such as a full description, permissions required by the app, and links to your privacy policy and terms of service.</span></span>
|<span data-ttu-id="3be5e-135">5 </span><span class="sxs-lookup"><span data-stu-id="3be5e-135">5</span></span>|<span data-ttu-id="3be5e-136">"**关闭" 按钮**：关闭模式。</span><span class="sxs-lookup"><span data-stu-id="3be5e-136">**Close button**: Closes the modal.</span></span>|
|<span data-ttu-id="3be5e-137">6 </span><span class="sxs-lookup"><span data-stu-id="3be5e-137">6</span></span>|<span data-ttu-id="3be5e-138">**通知工作组成员选项**：模式询问您是否要创建一篇文章，让其他人知道您添加了一个选项卡。</span><span class="sxs-lookup"><span data-stu-id="3be5e-138">**Notify team members option**: The modal asks if you want to create a post letting others know you added a tab.</span></span>|
|<span data-ttu-id="3be5e-139">7 </span><span class="sxs-lookup"><span data-stu-id="3be5e-139">7</span></span>|<span data-ttu-id="3be5e-140">"**后退" 按钮**：根据对话框打开的位置转到上一步。</span><span class="sxs-lookup"><span data-stu-id="3be5e-140">**Back button**: Goes to the previous step based on where the dialog opened.</span></span>|
|<span data-ttu-id="3be5e-141">8 </span><span class="sxs-lookup"><span data-stu-id="3be5e-141">8</span></span>|<span data-ttu-id="3be5e-142">"**保存" 按钮**：完成选项卡设置。</span><span class="sxs-lookup"><span data-stu-id="3be5e-142">**Save button**: Completes tab setup.</span></span>|

### <a name="tab-authentication-with-single-sign-on"></a><span data-ttu-id="3be5e-143">单一登录的选项卡身份验证</span><span class="sxs-lookup"><span data-stu-id="3be5e-143">Tab authentication with single sign-on</span></span>

<span data-ttu-id="3be5e-144">您可以添加用户首次使用其 Microsoft 凭据登录时必须登录的步骤。</span><span class="sxs-lookup"><span data-stu-id="3be5e-144">You can add a step in which users must first sign in with their Microsoft credentials.</span></span> <span data-ttu-id="3be5e-145">此身份验证方法称为 (SSO) 的单一登录。</span><span class="sxs-lookup"><span data-stu-id="3be5e-145">This authentication method is called single sign-on (SSO).</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="示例显示一个 tab 身份验证屏幕。" border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a><span data-ttu-id="3be5e-147">使用 UI 模板设计选项卡设置</span><span class="sxs-lookup"><span data-stu-id="3be5e-147">Designing a tab setup with UI templates</span></span>

<span data-ttu-id="3be5e-148">使用以下团队 UI 模板之一可帮助设计您的选项卡设置体验：</span><span class="sxs-lookup"><span data-stu-id="3be5e-148">Use one of the following Teams UI templates to help design your tab setup experience:</span></span>

* <span data-ttu-id="3be5e-149">[列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可浏览的格式显示相关项目，并允许用户对整个列表或单个项目执行操作。</span><span class="sxs-lookup"><span data-stu-id="3be5e-149">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="3be5e-150">[表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单以结构化方式收集、验证和提交用户输入。</span><span class="sxs-lookup"><span data-stu-id="3be5e-150">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="3be5e-151">[空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。</span><span class="sxs-lookup"><span data-stu-id="3be5e-151">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="view-a-tab"></a><span data-ttu-id="3be5e-152">查看选项卡</span><span class="sxs-lookup"><span data-stu-id="3be5e-152">View a tab</span></span>

<span data-ttu-id="3be5e-153">选项卡在团队中提供了全屏 web 体验，您可以在其中显示协作内容（如任务板和仪表板）以及重要信息。</span><span class="sxs-lookup"><span data-stu-id="3be5e-153">Tabs provide a full-screen web experience in Teams where you can display collaborative content—such task boards and dashboards—and important information.</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="示例显示带有任务板的选项卡。" border="false":::

### <a name="anatomy-tab"></a><span data-ttu-id="3be5e-155">剖析： Tab</span><span class="sxs-lookup"><span data-stu-id="3be5e-155">Anatomy: Tab</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="显示选项卡的 UI 剖析的插图。" border="false":::

|<span data-ttu-id="3be5e-157">计数器</span><span class="sxs-lookup"><span data-stu-id="3be5e-157">Counter</span></span>|<span data-ttu-id="3be5e-158">说明</span><span class="sxs-lookup"><span data-stu-id="3be5e-158">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="3be5e-159">1</span><span class="sxs-lookup"><span data-stu-id="3be5e-159">1</span></span>|<span data-ttu-id="3be5e-160">**选项卡名称**：选项卡的导航标签。</span><span class="sxs-lookup"><span data-stu-id="3be5e-160">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="3be5e-161">2 </span><span class="sxs-lookup"><span data-stu-id="3be5e-161">2</span></span>|<span data-ttu-id="3be5e-162">**选项卡溢出**：打开选项卡操作，例如 "重命名" 和 "删除"。</span><span class="sxs-lookup"><span data-stu-id="3be5e-162">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="3be5e-163">3 </span><span class="sxs-lookup"><span data-stu-id="3be5e-163">3</span></span>|<span data-ttu-id="3be5e-164">**选项卡聊天**：在右侧打开聊天线程，使用户可以在内容旁边进行对话。</span><span class="sxs-lookup"><span data-stu-id="3be5e-164">**Tab chat**: Opens a chat thread on the right, allowing users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="3be5e-165">4 </span><span class="sxs-lookup"><span data-stu-id="3be5e-165">4</span></span>|<span data-ttu-id="3be5e-166">**iframe**：显示您的选项卡的内容。</span><span class="sxs-lookup"><span data-stu-id="3be5e-166">**iframe**: Displays your tab’s content.</span></span>

### <a name="designing-a-tab-with-ui-templates"></a><span data-ttu-id="3be5e-167">设计包含 UI 模板的选项卡</span><span class="sxs-lookup"><span data-stu-id="3be5e-167">Designing a tab with UI templates</span></span>

<span data-ttu-id="3be5e-168">使用以下团队 UI 模板之一来帮助设计您的选项卡体验：</span><span class="sxs-lookup"><span data-stu-id="3be5e-168">Use one of the following Teams UI templates to help design your tab experience:</span></span>

* <span data-ttu-id="3be5e-169">[列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可浏览的格式显示相关项目，并允许用户对整个列表或单个项目执行操作。</span><span class="sxs-lookup"><span data-stu-id="3be5e-169">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="3be5e-170">[任务板](../../concepts/design/design-teams-app-ui-templates.md#task-board)：任务板（有时称为 "看板母板" 或 "泳道"）是用于跟踪工作项或票证状态的卡片的集合。</span><span class="sxs-lookup"><span data-stu-id="3be5e-170">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="3be5e-171">[仪表板](../../concepts/design/design-teams-app-ui-templates.md#dashboard)：仪表板是一个包含多个卡片的画布，可提供数据或内容的概述。</span><span class="sxs-lookup"><span data-stu-id="3be5e-171">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="3be5e-172">[表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单以结构化方式收集、验证和提交用户输入。</span><span class="sxs-lookup"><span data-stu-id="3be5e-172">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="3be5e-173">[空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。</span><span class="sxs-lookup"><span data-stu-id="3be5e-173">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="3be5e-174">[左侧](../../concepts/design/design-teams-app-ui-templates.md#left-nav)导航：如果您的选项卡需要一些导航，则左侧导航模板可有所帮助。</span><span class="sxs-lookup"><span data-stu-id="3be5e-174">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="3be5e-175">通常情况下，应保持最小的选项卡导航。</span><span class="sxs-lookup"><span data-stu-id="3be5e-175">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-tab-to-collaborate"></a><span data-ttu-id="3be5e-176">使用选项卡进行协作</span><span class="sxs-lookup"><span data-stu-id="3be5e-176">Use a tab to collaborate</span></span>

<span data-ttu-id="3be5e-177">选项卡有助于促进有关中心位置中的内容的对话。</span><span class="sxs-lookup"><span data-stu-id="3be5e-177">Tabs help facilitate conversations about content in a central location.</span></span>

### <a name="thread-discussion"></a><span data-ttu-id="3be5e-178">线程讨论</span><span class="sxs-lookup"><span data-stu-id="3be5e-178">Thread discussion</span></span>

<span data-ttu-id="3be5e-179">用户在添加新选项卡后，可以自动将其发布到频道或聊天。这不仅会通知团队成员新内容并提供指向选项卡的链接，它还允许用户开始谈论选项卡。</span><span class="sxs-lookup"><span data-stu-id="3be5e-179">Users can automatically post to a channel or chat once they’ve added a new tab. This not only notifies team members of the new content and provides a link to tab, it allows people to start talking about the tab.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="示例显示了在通道线程中讨论的选项卡。" border="false":::

### <a name="side-by-side-discussion"></a><span data-ttu-id="3be5e-181">并排讨论</span><span class="sxs-lookup"><span data-stu-id="3be5e-181">Side-by-side discussion</span></span>

<span data-ttu-id="3be5e-182">在查看该选项卡的内容时，用户可以进行对话。</span><span class="sxs-lookup"><span data-stu-id="3be5e-182">Users can have a conversation next while viewing the tab’s content.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="示例显示右侧的 &quot;聊天&quot; 处于打开状态的选项卡。" border="false":::

### <a name="permissions-and-role-based-views"></a><span data-ttu-id="3be5e-184">权限和基于角色的视图</span><span class="sxs-lookup"><span data-stu-id="3be5e-184">Permissions and role-based views</span></span>

<span data-ttu-id="3be5e-185">根据用户的权限，用户的选项卡体验可能有所不同。</span><span class="sxs-lookup"><span data-stu-id="3be5e-185">The tab experience may be different for users depending on their permissions.</span></span> <span data-ttu-id="3be5e-186">例如，一个用户无需登录即可访问该选项卡。</span><span class="sxs-lookup"><span data-stu-id="3be5e-186">For example, one user can access the tab without having to sign in.</span></span> <span data-ttu-id="3be5e-187">但是，另一个用户必须签名，并且将看到略有不同的内容。</span><span class="sxs-lookup"><span data-stu-id="3be5e-187">Another user, however, must sign and will see slightly different content.</span></span>

## <a name="manage-a-tab"></a><span data-ttu-id="3be5e-188">管理选项卡</span><span class="sxs-lookup"><span data-stu-id="3be5e-188">Manage a tab</span></span>

<span data-ttu-id="3be5e-189">可以包括用于重命名、删除或修改选项卡的选项。</span><span class="sxs-lookup"><span data-stu-id="3be5e-189">You can include options to rename, remove, or modify a tab.</span></span>

### <a name="anatomy-tab-menu"></a><span data-ttu-id="3be5e-190">剖析：选项卡菜单</span><span class="sxs-lookup"><span data-stu-id="3be5e-190">Anatomy: Tab menu</span></span>

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="显示选项卡菜单的 UI 剖析的插图。" border="false":::

|<span data-ttu-id="3be5e-192">计数器</span><span class="sxs-lookup"><span data-stu-id="3be5e-192">Counter</span></span>|<span data-ttu-id="3be5e-193">说明</span><span class="sxs-lookup"><span data-stu-id="3be5e-193">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="3be5e-194">1</span><span class="sxs-lookup"><span data-stu-id="3be5e-194">1</span></span>|<span data-ttu-id="3be5e-195">**设置**： (可选) 允许用户在添加选项卡后修改该选项卡的设置。</span><span class="sxs-lookup"><span data-stu-id="3be5e-195">**Settings**: (Optional) Allows users to modify a tab’s settings after it’s been added.</span></span>|
|<span data-ttu-id="3be5e-196">2 </span><span class="sxs-lookup"><span data-stu-id="3be5e-196">2</span></span>|<span data-ttu-id="3be5e-197">**重命名**：允许用户为选项卡提供对团队更有意义的名称。</span><span class="sxs-lookup"><span data-stu-id="3be5e-197">**Rename**: Allows users to give the tab a name that’s more meaningful to the team.</span></span>|
|<span data-ttu-id="3be5e-198">3 </span><span class="sxs-lookup"><span data-stu-id="3be5e-198">3</span></span>|<span data-ttu-id="3be5e-199">**删除**：从频道、聊天或会议中删除选项卡。</span><span class="sxs-lookup"><span data-stu-id="3be5e-199">**Remove**: Removes the tab from the channel, chat, or meeting.</span></span>|

## <a name="tab-notifications-and-deep-linking"></a><span data-ttu-id="3be5e-200">选项卡通知和深层链接</span><span class="sxs-lookup"><span data-stu-id="3be5e-200">Tab notifications and deep linking</span></span>

<span data-ttu-id="3be5e-201">您可以向您的选项卡发送带有深层链接的邮件。例如，卡片显示了用户可以选择在选项卡中查看整个 bug 的 bug 数据的摘要。发送有关选项卡活动的邮件可提高感知功能，而无需明确通知每个人 (即，活动没有噪音) 。</span><span class="sxs-lookup"><span data-stu-id="3be5e-201">You can send a message with a deep link to your tab. For example, a card shows a summary of bug data a user can select to see the entire bug in a tab. Sending messages about tab activity increases awareness without explicitly notifying everyone (i.e., activity without noise).</span></span> <span data-ttu-id="3be5e-202">如果需要，还可以 @mention 特定用户。</span><span class="sxs-lookup"><span data-stu-id="3be5e-202">You also can @mention specific users if needed.</span></span>

<span data-ttu-id="3be5e-203">通过以下方式之一通知用户选项卡活动：</span><span class="sxs-lookup"><span data-stu-id="3be5e-203">Notify users of tab activity one of the following ways:</span></span>

* <span data-ttu-id="3be5e-204">**Bot**：此方法是首选的如果对 tab 线程线程设定。</span><span class="sxs-lookup"><span data-stu-id="3be5e-204">**Bot**: This method is preferred especially if the tab thread is targeted.</span></span> <span data-ttu-id="3be5e-205">该选项卡的线程对话在最近活动的视图中移动到视图中。</span><span class="sxs-lookup"><span data-stu-id="3be5e-205">The tab’s threaded conversation is moved into view as recently active.</span></span> <span data-ttu-id="3be5e-206">此方法还允许在通知的发送方式方面有一些复杂之处。</span><span class="sxs-lookup"><span data-stu-id="3be5e-206">This method also allows for some sophistication in how the notification is sent.</span></span>
* <span data-ttu-id="3be5e-207">**消息**：在用户的活动源中显示一条消息，其中包含 [指向该选项卡的深层链接](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="3be5e-207">**Message**: A message shows up in the user’s activity feed with a [deep link to the tab](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span></span>

## <a name="best-practices"></a><span data-ttu-id="3be5e-208">最佳做法</span><span class="sxs-lookup"><span data-stu-id="3be5e-208">Best practices</span></span>

### <a name="collaboration"></a><span data-ttu-id="3be5e-209">协作</span><span class="sxs-lookup"><span data-stu-id="3be5e-209">Collaboration</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="图示演示如何处理选项卡导航设计。" border="false":::

#### <a name="do-facilitate-conversation"></a><span data-ttu-id="3be5e-211">Do：促进对话</span><span class="sxs-lookup"><span data-stu-id="3be5e-211">Do: Facilitate conversation</span></span>

<span data-ttu-id="3be5e-212">包含人们可以谈论的内容和组件。</span><span class="sxs-lookup"><span data-stu-id="3be5e-212">Include content and components people can talk about.</span></span> <span data-ttu-id="3be5e-213">如果它不适合聊天、频道或会议的上下文，它不会显示在您的选项卡中。</span><span class="sxs-lookup"><span data-stu-id="3be5e-213">If it doesn’t fit within the context of a chat, channel, or meeting, it doesn’t belong in your tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="图示演示了不使用选项卡导航设计。" border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a><span data-ttu-id="3be5e-215">请勿：像其他网页那样处理选项卡</span><span class="sxs-lookup"><span data-stu-id="3be5e-215">Don't: Treat your tab like any other webpage</span></span>

<span data-ttu-id="3be5e-216">一个选项卡不是某人可能只查看一次的网页。</span><span class="sxs-lookup"><span data-stu-id="3be5e-216">A tab isn’t a webpage someone might view once.</span></span> <span data-ttu-id="3be5e-217">选项卡应显示用户在实现这些功能时所需的最重要的相关内容。</span><span class="sxs-lookup"><span data-stu-id="3be5e-217">A tab should display your most important, relevant content that people need to accomplish something together.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="3be5e-218">导航</span><span class="sxs-lookup"><span data-stu-id="3be5e-218">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="图示演示如何处理选项卡导航设计。" border="false":::

#### <a name="do-limit-tasks-and-data"></a><span data-ttu-id="3be5e-220">操作：限制任务和数据</span><span class="sxs-lookup"><span data-stu-id="3be5e-220">Do: Limit tasks and data</span></span>

<span data-ttu-id="3be5e-221">在满足特定需求时，选项卡的工作效果最佳。</span><span class="sxs-lookup"><span data-stu-id="3be5e-221">Tabs work best when they address specific needs.</span></span> <span data-ttu-id="3be5e-222">包含与团队或组相关的一组有限的任务和数据。</span><span class="sxs-lookup"><span data-stu-id="3be5e-222">Include a limited set of tasks and data relevant to the team or group.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="图示演示了不使用选项卡导航设计。" border="false":::

#### <a name="dont-embed-your-entire-app"></a><span data-ttu-id="3be5e-224">请勿：嵌入整个应用程序</span><span class="sxs-lookup"><span data-stu-id="3be5e-224">Don't: Embed your entire app</span></span>

<span data-ttu-id="3be5e-225">使用选项卡显示包含多级导航和复杂交互组件的整个应用程序将导致信息超载。</span><span class="sxs-lookup"><span data-stu-id="3be5e-225">Using a tab to display an entire app with multi-level navigation and complex interactions leads to information overload.</span></span>

   :::column-end:::
:::row-end:::

### <a name="setup"></a><span data-ttu-id="3be5e-226">设置</span><span class="sxs-lookup"><span data-stu-id="3be5e-226">Setup</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="图中显示如何处理选项卡设置设计。" border="false":::

#### <a name="do-keep-it-simple"></a><span data-ttu-id="3be5e-228">操作：将其简化</span><span class="sxs-lookup"><span data-stu-id="3be5e-228">Do: Keep it simple</span></span>

<span data-ttu-id="3be5e-229">如果您的应用程序需要身份验证，请尝试将 Microsoft single sign-on 集成 (SSO) ，以实现更无缝的登录体验。</span><span class="sxs-lookup"><span data-stu-id="3be5e-229">If your app requires authentication, try integrating Microsoft single sign-on (SSO) for a more seamless sign-in experience.</span></span> <span data-ttu-id="3be5e-230">此外，仅包含必要的信息和添加该选项卡的步骤。</span><span class="sxs-lookup"><span data-stu-id="3be5e-230">Also, only include essential information and steps to add the tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="图中显示与选项卡设置设计无关的操作。" border="false":::

#### <a name="dont-have-too-many-steps"></a><span data-ttu-id="3be5e-232">请勿：执行过多的步骤</span><span class="sxs-lookup"><span data-stu-id="3be5e-232">Don't: Have too many steps</span></span>

<span data-ttu-id="3be5e-233">删除添加选项卡的任何不必要的步骤。</span><span class="sxs-lookup"><span data-stu-id="3be5e-233">Remove any unnecessary steps for adding a tab.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="3be5e-234">主题</span><span class="sxs-lookup"><span data-stu-id="3be5e-234">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="图示演示如何处理选项卡主题。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="3be5e-236">Do：利用团队颜色令牌</span><span class="sxs-lookup"><span data-stu-id="3be5e-236">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="3be5e-237">每个团队主题都有自己的配色方案。</span><span class="sxs-lookup"><span data-stu-id="3be5e-237">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="3be5e-238">若要自动处理主题更改，请在设计中使用 <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank"> (熟知的 UI) 的颜色标记 </a> 。</span><span class="sxs-lookup"><span data-stu-id="3be5e-238">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="图中显示与选项卡主题无关的操作。" border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="3be5e-240">不：硬编码颜色值</span><span class="sxs-lookup"><span data-stu-id="3be5e-240">Don't: Hard code color values</span></span>

<span data-ttu-id="3be5e-241">如果您不使用团队颜色令牌，则设计的可伸缩性较小并需要更多时间来管理。</span><span class="sxs-lookup"><span data-stu-id="3be5e-241">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a><span data-ttu-id="3be5e-242">验证设计</span><span class="sxs-lookup"><span data-stu-id="3be5e-242">Validate your design</span></span>

<span data-ttu-id="3be5e-243">如果计划将应用程序发布到 AppSource，则应了解通常会在提交期间导致应用程序失败的设计问题。</span><span class="sxs-lookup"><span data-stu-id="3be5e-243">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3be5e-244">检查设计验证准则</span><span class="sxs-lookup"><span data-stu-id="3be5e-244">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
