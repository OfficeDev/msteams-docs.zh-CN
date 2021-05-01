---
title: 设计适用于桌面和 Web 的选项卡
description: 了解如何在桌面和 web Teams设计 (选项卡) 并获取 Microsoft Teams UI 工具包。
author: heath-hamilton
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 9dc5489f4a6a4c6f0e1188250a9e2a9bc5793690
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101847"
---
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a><span data-ttu-id="a40b7-103">设计适用于桌面Microsoft Teams Web 的选项卡</span><span class="sxs-lookup"><span data-stu-id="a40b7-103">Designing your tab for Microsoft Teams desktop and web</span></span>

<span data-ttu-id="a40b7-104">选项卡是内容的大型画布。</span><span class="sxs-lookup"><span data-stu-id="a40b7-104">A tab is a large canvas for your content.</span></span> <span data-ttu-id="a40b7-105">为了指导应用设计，以下信息介绍了并说明了用户如何在应用中添加、使用和管理选项卡Teams。</span><span class="sxs-lookup"><span data-stu-id="a40b7-105">To guide your app design, the following information describes and illustrates how people can add, use, and manage tabs in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="a40b7-106">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="a40b7-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="a40b7-107">你可以找到全面的选项卡设计指南，包括你可以根据需要获取和修改的元素，Microsoft Teams UI 工具包。</span><span class="sxs-lookup"><span data-stu-id="a40b7-107">You can find comprehensive tab design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="a40b7-108">UI 工具包还具有辅助功能和响应式大小调整等基本主题，此处未介绍这些主题。</span><span class="sxs-lookup"><span data-stu-id="a40b7-108">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a40b7-109">获取 Microsoft Teams UI Kit （用户）</span><span class="sxs-lookup"><span data-stu-id="a40b7-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a><span data-ttu-id="a40b7-110">添加选项卡</span><span class="sxs-lookup"><span data-stu-id="a40b7-110">Add a tab</span></span>

<span data-ttu-id="a40b7-111">你可以从 AppSource Teams应用商店 (选项卡) 以下上下文之一：</span><span class="sxs-lookup"><span data-stu-id="a40b7-111">You can add a tab from the Teams store (AppSource) or in one of the following contexts:</span></span>

* <span data-ttu-id="a40b7-112">聊天</span><span class="sxs-lookup"><span data-stu-id="a40b7-112">Chat</span></span>
* <span data-ttu-id="a40b7-113">频道</span><span class="sxs-lookup"><span data-stu-id="a40b7-113">Channel</span></span>
* <span data-ttu-id="a40b7-114">会议 (之前、期间或之后) </span><span class="sxs-lookup"><span data-stu-id="a40b7-114">Meeting (before, during, or after the meeting)</span></span>

<span data-ttu-id="a40b7-115">下面的示例演示如何在频道中添加选项卡。</span><span class="sxs-lookup"><span data-stu-id="a40b7-115">The following example shows how a tab is added in a channel.</span></span>

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="示例显示正在频道中添加的选项卡。" border="false":::

## <a name="set-up-a-tab"></a><span data-ttu-id="a40b7-117">设置选项卡</span><span class="sxs-lookup"><span data-stu-id="a40b7-117">Set up a tab</span></span>

<span data-ttu-id="a40b7-118">有一个简短的设置过程，可以将应用添加为频道、聊天或会议选项卡。体验很大程度上取决于你。</span><span class="sxs-lookup"><span data-stu-id="a40b7-118">There's a short setup process to add an app as a channel, chat, or meeting tab. The experience is largely up to you.</span></span> <span data-ttu-id="a40b7-119">例如，你可以拥有如何使用应用的说明和一些可选设置。</span><span class="sxs-lookup"><span data-stu-id="a40b7-119">For example, you could have a description of how to use the app and some optional settings.</span></span> <span data-ttu-id="a40b7-120">如果需要对用户进行身份验证，请在此处包括登录步骤。</span><span class="sxs-lookup"><span data-stu-id="a40b7-120">Include a sign-in step here if you need to authenticate users.</span></span>

### <a name="tab-configuration-modal"></a><span data-ttu-id="a40b7-121">选项卡配置模式</span><span class="sxs-lookup"><span data-stu-id="a40b7-121">Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="示例显示选项卡配置模式。" border="false":::

### <a name="anatomy-tab-configuration-modal"></a><span data-ttu-id="a40b7-123">结构：选项卡配置模式</span><span class="sxs-lookup"><span data-stu-id="a40b7-123">Anatomy: Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="显示选项卡配置模式 UI 分析的图示。" border="false":::

|<span data-ttu-id="a40b7-125">计数器</span><span class="sxs-lookup"><span data-stu-id="a40b7-125">Counter</span></span>|<span data-ttu-id="a40b7-126">说明</span><span class="sxs-lookup"><span data-stu-id="a40b7-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a40b7-127">1</span><span class="sxs-lookup"><span data-stu-id="a40b7-127">1</span></span>|<span data-ttu-id="a40b7-128">**应用徽标**：应用的全彩色应用徽标。</span><span class="sxs-lookup"><span data-stu-id="a40b7-128">**App logo**: Full color app logo of your app.</span></span>|
|<span data-ttu-id="a40b7-129">2</span><span class="sxs-lookup"><span data-stu-id="a40b7-129">2</span></span>|<span data-ttu-id="a40b7-130">**应用名称**：应用的完整名称。</span><span class="sxs-lookup"><span data-stu-id="a40b7-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="a40b7-131">3</span><span class="sxs-lookup"><span data-stu-id="a40b7-131">3</span></span>|<span data-ttu-id="a40b7-132">**iframe：** 应用内容响应空间 (例如选项卡设置或身份验证) 。</span><span class="sxs-lookup"><span data-stu-id="a40b7-132">**iframe**: Responsive space for your app’s content (for example, tab settings or authentication).</span></span>|
|<span data-ttu-id="a40b7-133">4 </span><span class="sxs-lookup"><span data-stu-id="a40b7-133">4</span></span>|<span data-ttu-id="a40b7-134">**关于链接**：打开一个对话框，其中显示有关应用的详细信息，例如完整说明、应用所需的权限以及指向隐私策略和服务条款的链接。</span><span class="sxs-lookup"><span data-stu-id="a40b7-134">**About link**: Opens a dialog showing more information about the app, such as a full description, permissions required by the app, and links to your privacy policy and terms of service.</span></span>
|<span data-ttu-id="a40b7-135">5 </span><span class="sxs-lookup"><span data-stu-id="a40b7-135">5</span></span>|<span data-ttu-id="a40b7-136">**关闭按钮**：关闭模式。</span><span class="sxs-lookup"><span data-stu-id="a40b7-136">**Close button**: Closes the modal.</span></span>|
|<span data-ttu-id="a40b7-137">6 </span><span class="sxs-lookup"><span data-stu-id="a40b7-137">6</span></span>|<span data-ttu-id="a40b7-138">**通知团队成员选项**：模式询问您是否要创建一个帖子，让其他人知道您添加了选项卡。</span><span class="sxs-lookup"><span data-stu-id="a40b7-138">**Notify team members option**: The modal asks if you want to create a post letting others know you added a tab.</span></span>|
|<span data-ttu-id="a40b7-139">7 </span><span class="sxs-lookup"><span data-stu-id="a40b7-139">7</span></span>|<span data-ttu-id="a40b7-140">**"后退**"按钮：根据对话框打开位置转到上一步。</span><span class="sxs-lookup"><span data-stu-id="a40b7-140">**Back button**: Goes to the previous step based on where the dialog opened.</span></span>|
|<span data-ttu-id="a40b7-141">8 </span><span class="sxs-lookup"><span data-stu-id="a40b7-141">8</span></span>|<span data-ttu-id="a40b7-142">**保存按钮**：完成选项卡设置。</span><span class="sxs-lookup"><span data-stu-id="a40b7-142">**Save button**: Completes tab setup.</span></span>|

### <a name="tab-authentication-with-single-sign-on"></a><span data-ttu-id="a40b7-143">使用单一登录的选项卡身份验证</span><span class="sxs-lookup"><span data-stu-id="a40b7-143">Tab authentication with single sign-on</span></span>

<span data-ttu-id="a40b7-144">你可以添加一个步骤，用户必须先使用其 Microsoft 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="a40b7-144">You can add a step in which users must first sign in with their Microsoft credentials.</span></span> <span data-ttu-id="a40b7-145">此身份验证方法称为 SSO (单一) 。</span><span class="sxs-lookup"><span data-stu-id="a40b7-145">This authentication method is called single sign-on (SSO).</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="示例显示选项卡身份验证屏幕。" border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a><span data-ttu-id="a40b7-147">使用 UI 模板设计选项卡设置</span><span class="sxs-lookup"><span data-stu-id="a40b7-147">Designing a tab setup with UI templates</span></span>

<span data-ttu-id="a40b7-148">使用以下 UI 模板Teams之一来帮助设计选项卡设置体验：</span><span class="sxs-lookup"><span data-stu-id="a40b7-148">Use one of the following Teams UI templates to help design your tab setup experience:</span></span>

* <span data-ttu-id="a40b7-149">[列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可扫描的格式显示相关项，并允许用户对整个列表或单个项目采取操作。</span><span class="sxs-lookup"><span data-stu-id="a40b7-149">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="a40b7-150">[表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单用于以结构化方式收集、验证和提交用户输入。</span><span class="sxs-lookup"><span data-stu-id="a40b7-150">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="a40b7-151">[空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。</span><span class="sxs-lookup"><span data-stu-id="a40b7-151">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="view-a-tab"></a><span data-ttu-id="a40b7-152">查看选项卡</span><span class="sxs-lookup"><span data-stu-id="a40b7-152">View a tab</span></span>

<span data-ttu-id="a40b7-153">选项卡提供了全屏 Web 体验，Teams显示协作内容（如任务板和仪表板）和重要信息。</span><span class="sxs-lookup"><span data-stu-id="a40b7-153">Tabs provide a full-screen web experience in Teams where you can display collaborative content—such task boards and dashboards—and important information.</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="示例显示一个包含任务板的选项卡。" border="false":::

### <a name="anatomy-tab"></a><span data-ttu-id="a40b7-155">结构：选项卡</span><span class="sxs-lookup"><span data-stu-id="a40b7-155">Anatomy: Tab</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="显示选项卡的 UI 分析的图示。" border="false":::

|<span data-ttu-id="a40b7-157">计数器</span><span class="sxs-lookup"><span data-stu-id="a40b7-157">Counter</span></span>|<span data-ttu-id="a40b7-158">说明</span><span class="sxs-lookup"><span data-stu-id="a40b7-158">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a40b7-159">1</span><span class="sxs-lookup"><span data-stu-id="a40b7-159">1</span></span>|<span data-ttu-id="a40b7-160">**选项卡名称**：选项卡的导航标签。</span><span class="sxs-lookup"><span data-stu-id="a40b7-160">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="a40b7-161">2</span><span class="sxs-lookup"><span data-stu-id="a40b7-161">2</span></span>|<span data-ttu-id="a40b7-162">**Tab 溢出**：打开选项卡操作，如重命名和删除。</span><span class="sxs-lookup"><span data-stu-id="a40b7-162">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="a40b7-163">3</span><span class="sxs-lookup"><span data-stu-id="a40b7-163">3</span></span>|<span data-ttu-id="a40b7-164">**选项卡聊天**：在右侧打开聊天线程，允许用户在内容旁边进行对话。</span><span class="sxs-lookup"><span data-stu-id="a40b7-164">**Tab chat**: Opens a chat thread on the right, allowing users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="a40b7-165">4 </span><span class="sxs-lookup"><span data-stu-id="a40b7-165">4</span></span>|<span data-ttu-id="a40b7-166">**iframe：** 显示选项卡的内容。</span><span class="sxs-lookup"><span data-stu-id="a40b7-166">**iframe**: Displays your tab’s content.</span></span>

### <a name="designing-a-tab-with-ui-templates"></a><span data-ttu-id="a40b7-167">使用 UI 模板设计选项卡</span><span class="sxs-lookup"><span data-stu-id="a40b7-167">Designing a tab with UI templates</span></span>

<span data-ttu-id="a40b7-168">使用以下 UI 模板Teams之一来帮助设计选项卡体验：</span><span class="sxs-lookup"><span data-stu-id="a40b7-168">Use one of the following Teams UI templates to help design your tab experience:</span></span>

* <span data-ttu-id="a40b7-169">[列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可扫描的格式显示相关项，并允许用户对整个列表或单个项目采取操作。</span><span class="sxs-lookup"><span data-stu-id="a40b7-169">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="a40b7-170">[任务板](../../concepts/design/design-teams-app-ui-templates.md#task-board)：任务板（有时称为看板或街道）是一组卡片，通常用于跟踪工作项或票证的状态。</span><span class="sxs-lookup"><span data-stu-id="a40b7-170">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="a40b7-171">[仪表板](../../concepts/design/design-teams-app-ui-templates.md#dashboard)：仪表板是包含多个卡片的画布，可提供数据或内容的概述。</span><span class="sxs-lookup"><span data-stu-id="a40b7-171">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="a40b7-172">[表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单用于以结构化方式收集、验证和提交用户输入。</span><span class="sxs-lookup"><span data-stu-id="a40b7-172">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="a40b7-173">[空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。</span><span class="sxs-lookup"><span data-stu-id="a40b7-173">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="a40b7-174">[左侧导航](../../concepts/design/design-teams-app-ui-templates.md#left-nav)：如果你的选项卡需要一些导航，左侧导航模板可以提供帮助。</span><span class="sxs-lookup"><span data-stu-id="a40b7-174">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="a40b7-175">通常，应使 Tab 键导航保持在最低程度。</span><span class="sxs-lookup"><span data-stu-id="a40b7-175">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-tab-to-collaborate"></a><span data-ttu-id="a40b7-176">使用选项卡进行协作</span><span class="sxs-lookup"><span data-stu-id="a40b7-176">Use a tab to collaborate</span></span>

<span data-ttu-id="a40b7-177">选项卡有助于就中心位置的内容展开对话。</span><span class="sxs-lookup"><span data-stu-id="a40b7-177">Tabs help facilitate conversations about content in a central location.</span></span>

### <a name="thread-discussion"></a><span data-ttu-id="a40b7-178">线程讨论</span><span class="sxs-lookup"><span data-stu-id="a40b7-178">Thread discussion</span></span>

<span data-ttu-id="a40b7-179">用户一旦添加了新选项卡，就可以自动发布至频道或聊天。这不仅向团队成员通知新内容并提供指向选项卡的链接，还允许用户开始讨论选项卡。</span><span class="sxs-lookup"><span data-stu-id="a40b7-179">Users can automatically post to a channel or chat once they’ve added a new tab. This not only notifies team members of the new content and provides a link to tab, it allows people to start talking about the tab.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="示例显示正在频道线程中讨论的选项卡。" border="false":::

### <a name="side-by-side-discussion"></a><span data-ttu-id="a40b7-181">并行讨论</span><span class="sxs-lookup"><span data-stu-id="a40b7-181">Side-by-side discussion</span></span>

<span data-ttu-id="a40b7-182">在查看选项卡内容时，用户下次可以有对话。</span><span class="sxs-lookup"><span data-stu-id="a40b7-182">Users can have a conversation next while viewing the tab’s content.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="示例显示一个在右侧打开聊天的选项卡。" border="false":::

### <a name="permissions-and-role-based-views"></a><span data-ttu-id="a40b7-184">权限和基于角色的视图</span><span class="sxs-lookup"><span data-stu-id="a40b7-184">Permissions and role-based views</span></span>

<span data-ttu-id="a40b7-185">选项卡体验可能因用户的权限不同而不同。</span><span class="sxs-lookup"><span data-stu-id="a40b7-185">The tab experience may be different for users depending on their permissions.</span></span> <span data-ttu-id="a40b7-186">例如，一个用户无需登录即可访问选项卡。</span><span class="sxs-lookup"><span data-stu-id="a40b7-186">For example, one user can access the tab without having to sign in.</span></span> <span data-ttu-id="a40b7-187">但是，另一个用户必须签名，并且会看到略有不同的内容。</span><span class="sxs-lookup"><span data-stu-id="a40b7-187">Another user, however, must sign and will see slightly different content.</span></span>

## <a name="manage-a-tab"></a><span data-ttu-id="a40b7-188">管理选项卡</span><span class="sxs-lookup"><span data-stu-id="a40b7-188">Manage a tab</span></span>

<span data-ttu-id="a40b7-189">您可以包括用于重命名、删除或修改选项卡的选项。</span><span class="sxs-lookup"><span data-stu-id="a40b7-189">You can include options to rename, remove, or modify a tab.</span></span>

### <a name="anatomy-tab-menu"></a><span data-ttu-id="a40b7-190">结构：选项卡菜单</span><span class="sxs-lookup"><span data-stu-id="a40b7-190">Anatomy: Tab menu</span></span>

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="显示选项卡菜单的 UI 分析的图示。" border="false":::

|<span data-ttu-id="a40b7-192">计数器</span><span class="sxs-lookup"><span data-stu-id="a40b7-192">Counter</span></span>|<span data-ttu-id="a40b7-193">说明</span><span class="sxs-lookup"><span data-stu-id="a40b7-193">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a40b7-194">1</span><span class="sxs-lookup"><span data-stu-id="a40b7-194">1</span></span>|<span data-ttu-id="a40b7-195">**设置**： (可选) 允许用户在添加选项卡后修改其设置。</span><span class="sxs-lookup"><span data-stu-id="a40b7-195">**Settings**: (Optional) Allows users to modify a tab’s settings after it’s been added.</span></span>|
|<span data-ttu-id="a40b7-196">2</span><span class="sxs-lookup"><span data-stu-id="a40b7-196">2</span></span>|<span data-ttu-id="a40b7-197">**重命名**：允许用户为选项卡指定一个对团队更有意义的名称。</span><span class="sxs-lookup"><span data-stu-id="a40b7-197">**Rename**: Allows users to give the tab a name that’s more meaningful to the team.</span></span>|
|<span data-ttu-id="a40b7-198">3</span><span class="sxs-lookup"><span data-stu-id="a40b7-198">3</span></span>|<span data-ttu-id="a40b7-199">**删除**：从频道、聊天或会议中删除选项卡。</span><span class="sxs-lookup"><span data-stu-id="a40b7-199">**Remove**: Removes the tab from the channel, chat, or meeting.</span></span>|

## <a name="tab-notifications-and-deep-linking"></a><span data-ttu-id="a40b7-200">选项卡通知和深层链接</span><span class="sxs-lookup"><span data-stu-id="a40b7-200">Tab notifications and deep linking</span></span>

<span data-ttu-id="a40b7-201">你可以向选项卡发送包含深层链接的邮件。例如，卡片显示用户可选择在选项卡中查看整个 Bug 的 Bug 数据的摘要。发送有关选项卡活动的消息可提升感知度，而无需明确通知 (，即无噪音活动) 。</span><span class="sxs-lookup"><span data-stu-id="a40b7-201">You can send a message with a deep link to your tab. For example, a card shows a summary of bug data a user can select to see the entire bug in a tab. Sending messages about tab activity increases awareness without explicitly notifying everyone (i.e., activity without noise).</span></span> <span data-ttu-id="a40b7-202">如果需要，@mention特定用户。</span><span class="sxs-lookup"><span data-stu-id="a40b7-202">You also can @mention specific users if needed.</span></span>

<span data-ttu-id="a40b7-203">通过以下方法之一通知用户选项卡活动：</span><span class="sxs-lookup"><span data-stu-id="a40b7-203">Notify users of tab activity one of the following ways:</span></span>

* <span data-ttu-id="a40b7-204">**Bot：** 此方法是首选方法，尤其是在选项卡线程具有目标时。</span><span class="sxs-lookup"><span data-stu-id="a40b7-204">**Bot**: This method is preferred especially if the tab thread is targeted.</span></span> <span data-ttu-id="a40b7-205">选项卡的线程对话将移动到最近处于活动状态的视图中。</span><span class="sxs-lookup"><span data-stu-id="a40b7-205">The tab’s threaded conversation is moved into view as recently active.</span></span> <span data-ttu-id="a40b7-206">此方法还允许通知发送方式的一些复杂程度。</span><span class="sxs-lookup"><span data-stu-id="a40b7-206">This method also allows for some sophistication in how the notification is sent.</span></span>
* <span data-ttu-id="a40b7-207">**消息**：用户的活动源中显示一条消息，包含指向选项卡 [的深层链接](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="a40b7-207">**Message**: A message shows up in the user’s activity feed with a [deep link to the tab](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span></span>

## <a name="best-practices"></a><span data-ttu-id="a40b7-208">最佳做法</span><span class="sxs-lookup"><span data-stu-id="a40b7-208">Best practices</span></span>

<span data-ttu-id="a40b7-209">使用这些建议创建高质量的应用体验。</span><span class="sxs-lookup"><span data-stu-id="a40b7-209">Use these recommendations to create a quality app experience.</span></span>

### <a name="collaboration"></a><span data-ttu-id="a40b7-210">协作</span><span class="sxs-lookup"><span data-stu-id="a40b7-210">Collaboration</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="插图显示选项卡导航设计如何操作。" border="false":::

#### <a name="do-facilitate-conversation"></a><span data-ttu-id="a40b7-212">应做：促进对话</span><span class="sxs-lookup"><span data-stu-id="a40b7-212">Do: Facilitate conversation</span></span>

<span data-ttu-id="a40b7-213">包括用户可以讨论的内容和组件。</span><span class="sxs-lookup"><span data-stu-id="a40b7-213">Include content and components people can talk about.</span></span> <span data-ttu-id="a40b7-214">如果它不适合聊天、频道或会议上下文，则它不属于你的选项卡。</span><span class="sxs-lookup"><span data-stu-id="a40b7-214">If it doesn’t fit within the context of a chat, channel, or meeting, it doesn’t belong in your tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="示例显示不与选项卡导航设计一起执行哪些操作。" border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a><span data-ttu-id="a40b7-216">请勿：将选项卡视为任何其他网页</span><span class="sxs-lookup"><span data-stu-id="a40b7-216">Don't: Treat your tab like any other webpage</span></span>

<span data-ttu-id="a40b7-217">选项卡不是某人可能查看过一次的网页。</span><span class="sxs-lookup"><span data-stu-id="a40b7-217">A tab isn’t a webpage someone might view once.</span></span> <span data-ttu-id="a40b7-218">选项卡应显示用户共同完成某些任务所需的最重要的相关内容。</span><span class="sxs-lookup"><span data-stu-id="a40b7-218">A tab should display your most important, relevant content that people need to accomplish something together.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="a40b7-219">导航</span><span class="sxs-lookup"><span data-stu-id="a40b7-219">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="显示选项卡导航设计要执行哪些操作的示例。" border="false":::

#### <a name="do-limit-tasks-and-data"></a><span data-ttu-id="a40b7-221">操作：限制任务和数据</span><span class="sxs-lookup"><span data-stu-id="a40b7-221">Do: Limit tasks and data</span></span>

<span data-ttu-id="a40b7-222">选项卡在满足特定需求时效果最佳。</span><span class="sxs-lookup"><span data-stu-id="a40b7-222">Tabs work best when they address specific needs.</span></span> <span data-ttu-id="a40b7-223">包含一组有限的与团队或组相关的任务和数据。</span><span class="sxs-lookup"><span data-stu-id="a40b7-223">Include a limited set of tasks and data relevant to the team or group.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="插图显示不与选项卡导航设计有关的内容。" border="false":::

#### <a name="dont-embed-your-entire-app"></a><span data-ttu-id="a40b7-225">请勿：嵌入整个应用</span><span class="sxs-lookup"><span data-stu-id="a40b7-225">Don't: Embed your entire app</span></span>

<span data-ttu-id="a40b7-226">使用选项卡显示具有多级导航和复杂交互的整个应用会导致信息过载。</span><span class="sxs-lookup"><span data-stu-id="a40b7-226">Using a tab to display an entire app with multi-level navigation and complex interactions leads to information overload.</span></span>

   :::column-end:::
:::row-end:::

### <a name="setup"></a><span data-ttu-id="a40b7-227">设置</span><span class="sxs-lookup"><span data-stu-id="a40b7-227">Setup</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="插图显示选项卡设置设计要执行哪些操作。" border="false":::

#### <a name="do-keep-it-simple"></a><span data-ttu-id="a40b7-229">应做之事：保持简单</span><span class="sxs-lookup"><span data-stu-id="a40b7-229">Do: Keep it simple</span></span>

<span data-ttu-id="a40b7-230">如果你的应用需要身份验证，请尝试将 Microsoft 单一登录 (SSO) 集成，实现更加无缝的登录体验。</span><span class="sxs-lookup"><span data-stu-id="a40b7-230">If your app requires authentication, try integrating Microsoft single sign-on (SSO) for a more seamless sign-in experience.</span></span> <span data-ttu-id="a40b7-231">此外，仅包括添加选项卡的必需信息和步骤。</span><span class="sxs-lookup"><span data-stu-id="a40b7-231">Also, only include essential information and steps to add the tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="插图显示与选项卡设置设计不一样。" border="false":::

#### <a name="dont-have-too-many-steps"></a><span data-ttu-id="a40b7-233">不要：步骤过多</span><span class="sxs-lookup"><span data-stu-id="a40b7-233">Don't: Have too many steps</span></span>

<span data-ttu-id="a40b7-234">删除添加选项卡的不必要的步骤。</span><span class="sxs-lookup"><span data-stu-id="a40b7-234">Remove any unnecessary steps for adding a tab.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="a40b7-235">主题</span><span class="sxs-lookup"><span data-stu-id="a40b7-235">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="插图显示使用制表位设置要执行哪些操作。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="a40b7-237">应做：利用Teams令牌</span><span class="sxs-lookup"><span data-stu-id="a40b7-237">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="a40b7-238">每个Teams主题都有自己的配色方案。</span><span class="sxs-lookup"><span data-stu-id="a40b7-238">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="a40b7-239">若要自动处理主题更改，请 <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank"> (Fluent UI </a>) 颜色标记。</span><span class="sxs-lookup"><span data-stu-id="a40b7-239">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="插图显示不与选项卡设置有关的内容。" border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="a40b7-241">请勿：硬编码颜色值</span><span class="sxs-lookup"><span data-stu-id="a40b7-241">Don't: Hard code color values</span></span>

<span data-ttu-id="a40b7-242">如果不使用颜色令牌Teams，你的设计将不太可扩展，并且需要更多的时间进行管理。</span><span class="sxs-lookup"><span data-stu-id="a40b7-242">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::
