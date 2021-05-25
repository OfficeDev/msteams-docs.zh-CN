---
title: 设计适用于桌面和 Web 的选项卡
description: 了解如何在桌面和 web Teams设计 (选项卡) 并获取 Microsoft Teams UI 工具包。
author: heath-hamilton
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 38eb7e400de63beb0d2840ee573bbfd16299cfbd
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644711"
---
# <a name="designing-your-tab-for-microsoft-teams"></a><span data-ttu-id="46ad8-103">为用户设计选项卡Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="46ad8-103">Designing your tab for Microsoft Teams</span></span>

<span data-ttu-id="46ad8-104">选项卡是应用内容的大型画布。</span><span class="sxs-lookup"><span data-stu-id="46ad8-104">A tab is a large canvas for your app content.</span></span> <span data-ttu-id="46ad8-105">为了指导应用设计，以下信息介绍了并说明了用户如何在应用中添加、使用和管理选项卡Teams。</span><span class="sxs-lookup"><span data-stu-id="46ad8-105">To guide your app design, the following information describes and illustrates how people can add, use, and manage tabs in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="46ad8-106">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="46ad8-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="46ad8-107">你可以找到全面的选项卡设计指南，包括你可以根据需要获取和修改的元素，Microsoft Teams UI 工具包。</span><span class="sxs-lookup"><span data-stu-id="46ad8-107">You can find comprehensive tab design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="46ad8-108">UI 工具包还具有辅助功能和响应式大小调整等基本主题，此处未介绍这些主题。</span><span class="sxs-lookup"><span data-stu-id="46ad8-108">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="46ad8-109">获取 Microsoft Teams UI Kit （用户）</span><span class="sxs-lookup"><span data-stu-id="46ad8-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a><span data-ttu-id="46ad8-110">添加选项卡</span><span class="sxs-lookup"><span data-stu-id="46ad8-110">Add a tab</span></span>

<span data-ttu-id="46ad8-111">你可以从 AppSource Teams应用商店 (选项卡) 以下上下文之一：</span><span class="sxs-lookup"><span data-stu-id="46ad8-111">You can add a tab from the Teams store (AppSource) or in one of the following contexts:</span></span>

* <span data-ttu-id="46ad8-112">聊天</span><span class="sxs-lookup"><span data-stu-id="46ad8-112">Chat</span></span>
* <span data-ttu-id="46ad8-113">频道</span><span class="sxs-lookup"><span data-stu-id="46ad8-113">Channel</span></span>
* <span data-ttu-id="46ad8-114">会议 (之前、期间或之后) </span><span class="sxs-lookup"><span data-stu-id="46ad8-114">Meeting (before, during, or after the meeting)</span></span>

# <a name="desktop"></a>[<span data-ttu-id="46ad8-115">桌面</span><span class="sxs-lookup"><span data-stu-id="46ad8-115">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="46ad8-116">下面的示例展示了用户如何在频道中添加选项卡。</span><span class="sxs-lookup"><span data-stu-id="46ad8-116">The following example shows how users can add a tab in a channel.</span></span>

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="示例显示正在频道中添加的选项卡。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="46ad8-118">移动</span><span class="sxs-lookup"><span data-stu-id="46ad8-118">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="46ad8-119">用户可以通过选择频道中的"更多"按钮来访问选项卡 (例如) 添加这些选项卡的聊天或聊天。</span><span class="sxs-lookup"><span data-stu-id="46ad8-119">Users can access tabs by selecting the **More** button in the channel (example below) or chat in which they've been added.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-design-access-tab.png" alt-text="示例显示正在频道中添加的移动选项卡。" border="false":::

---

## <a name="set-up-a-tab"></a><span data-ttu-id="46ad8-121">设置选项卡</span><span class="sxs-lookup"><span data-stu-id="46ad8-121">Set up a tab</span></span>

<span data-ttu-id="46ad8-122">有一个简短的设置过程，可以将应用添加为频道、聊天或会议选项卡。体验很大程度上取决于你。</span><span class="sxs-lookup"><span data-stu-id="46ad8-122">There's a short setup process to add an app as a channel, chat, or meeting tab. The experience is largely up to you.</span></span> <span data-ttu-id="46ad8-123">例如，你可以拥有如何使用应用的说明和一些可选设置。</span><span class="sxs-lookup"><span data-stu-id="46ad8-123">For example, you could have a description of how to use the app and some optional settings.</span></span> <span data-ttu-id="46ad8-124">如果需要对用户进行身份验证，请在此处包括登录步骤。</span><span class="sxs-lookup"><span data-stu-id="46ad8-124">Include a sign-in step here if you need to authenticate users.</span></span>

### <a name="tab-configuration-dialog"></a><span data-ttu-id="46ad8-125">选项卡配置对话框</span><span class="sxs-lookup"><span data-stu-id="46ad8-125">Tab configuration dialog</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="示例显示选项卡配置模式。" border="false":::

### <a name="anatomy-tab-configuration-dialog"></a><span data-ttu-id="46ad8-127">结构：选项卡配置对话框</span><span class="sxs-lookup"><span data-stu-id="46ad8-127">Anatomy: Tab configuration dialog</span></span>

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="显示选项卡配置模式 UI 分析的图示。" border="false":::

|<span data-ttu-id="46ad8-129">计数器</span><span class="sxs-lookup"><span data-stu-id="46ad8-129">Counter</span></span>|<span data-ttu-id="46ad8-130">说明</span><span class="sxs-lookup"><span data-stu-id="46ad8-130">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="46ad8-131">1</span><span class="sxs-lookup"><span data-stu-id="46ad8-131">1</span></span>|<span data-ttu-id="46ad8-132">**应用徽标**：应用的全彩色应用徽标。</span><span class="sxs-lookup"><span data-stu-id="46ad8-132">**App logo**: Full color app logo of your app.</span></span>|
|<span data-ttu-id="46ad8-133">2</span><span class="sxs-lookup"><span data-stu-id="46ad8-133">2</span></span>|<span data-ttu-id="46ad8-134">**应用名称**：应用的完整名称。</span><span class="sxs-lookup"><span data-stu-id="46ad8-134">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="46ad8-135">3</span><span class="sxs-lookup"><span data-stu-id="46ad8-135">3</span></span>|<span data-ttu-id="46ad8-136">**iframe：** 应用内容响应空间 (例如选项卡设置或身份验证) 。</span><span class="sxs-lookup"><span data-stu-id="46ad8-136">**iframe**: Responsive space for your app’s content (for example, tab settings or authentication).</span></span>|
|<span data-ttu-id="46ad8-137">4 </span><span class="sxs-lookup"><span data-stu-id="46ad8-137">4</span></span>|<span data-ttu-id="46ad8-138">**关于链接**：打开一个对话框，其中显示有关应用的详细信息，例如完整说明、应用所需的权限以及指向隐私策略和服务条款的链接。</span><span class="sxs-lookup"><span data-stu-id="46ad8-138">**About link**: Opens a dialog showing more information about the app, such as a full description, permissions required by the app, and links to your privacy policy and terms of service.</span></span>|
|<span data-ttu-id="46ad8-139">5 </span><span class="sxs-lookup"><span data-stu-id="46ad8-139">5</span></span>|<span data-ttu-id="46ad8-140">**关闭按钮**：关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="46ad8-140">**Close button**: Closes the dialog.</span></span>|
|<span data-ttu-id="46ad8-141">6 </span><span class="sxs-lookup"><span data-stu-id="46ad8-141">6</span></span>|<span data-ttu-id="46ad8-142">**通知团队成员选项**：对话框询问用户是否要创建一个帖子，让其他人知道他们添加了选项卡。</span><span class="sxs-lookup"><span data-stu-id="46ad8-142">**Notify team members option**: The dialog asks users if they want to create a post letting others know they added a tab.</span></span>|
|<span data-ttu-id="46ad8-143">7 </span><span class="sxs-lookup"><span data-stu-id="46ad8-143">7</span></span>|<span data-ttu-id="46ad8-144">**"后退**"按钮：根据对话框打开位置转到上一步。</span><span class="sxs-lookup"><span data-stu-id="46ad8-144">**Back button**: Goes to the previous step based on where the dialog opened.</span></span>|
|<span data-ttu-id="46ad8-145">8 </span><span class="sxs-lookup"><span data-stu-id="46ad8-145">8</span></span>|<span data-ttu-id="46ad8-146">**保存按钮**：完成选项卡设置。</span><span class="sxs-lookup"><span data-stu-id="46ad8-146">**Save button**: Completes tab setup.</span></span>|

### <a name="tab-authentication-with-single-sign-on"></a><span data-ttu-id="46ad8-147">使用单一登录的选项卡身份验证</span><span class="sxs-lookup"><span data-stu-id="46ad8-147">Tab authentication with single sign-on</span></span>

<span data-ttu-id="46ad8-148">你可以添加一个步骤，用户必须先使用其 Microsoft 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="46ad8-148">You can add a step in which users must first sign in with their Microsoft credentials.</span></span> <span data-ttu-id="46ad8-149">此身份验证方法称为 SSO (单一) 。</span><span class="sxs-lookup"><span data-stu-id="46ad8-149">This authentication method is called single sign-on (SSO).</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="示例显示选项卡身份验证屏幕。" border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a><span data-ttu-id="46ad8-151">使用 UI 模板设计选项卡设置</span><span class="sxs-lookup"><span data-stu-id="46ad8-151">Designing a tab setup with UI templates</span></span>

<span data-ttu-id="46ad8-152">使用以下 UI 模板Teams之一来帮助设计选项卡设置体验：</span><span class="sxs-lookup"><span data-stu-id="46ad8-152">Use one of the following Teams UI templates to help design your tab setup experience:</span></span>

* <span data-ttu-id="46ad8-153">[列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可扫描的格式显示相关项，并允许用户对整个列表或单个项目采取操作。</span><span class="sxs-lookup"><span data-stu-id="46ad8-153">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="46ad8-154">[表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单用于以结构化方式收集、验证和提交用户输入。</span><span class="sxs-lookup"><span data-stu-id="46ad8-154">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="46ad8-155">[空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。</span><span class="sxs-lookup"><span data-stu-id="46ad8-155">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="view-a-tab"></a><span data-ttu-id="46ad8-156">查看选项卡</span><span class="sxs-lookup"><span data-stu-id="46ad8-156">View a tab</span></span>

<span data-ttu-id="46ad8-157">选项卡提供了全屏 Web 体验，Teams显示协作内容（如任务板和仪表板）和重要信息。</span><span class="sxs-lookup"><span data-stu-id="46ad8-157">Tabs provide a full-screen web experience in Teams where you can display collaborative content—such task boards and dashboards—and important information.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="46ad8-158">桌面</span><span class="sxs-lookup"><span data-stu-id="46ad8-158">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="示例显示一个包含任务板的选项卡。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="46ad8-160">移动</span><span class="sxs-lookup"><span data-stu-id="46ad8-160">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-view-tab.png" alt-text="示例显示一个包含任务板的移动选项卡。" border="false":::

---

### <a name="anatomy-tab"></a><span data-ttu-id="46ad8-162">结构：选项卡</span><span class="sxs-lookup"><span data-stu-id="46ad8-162">Anatomy: Tab</span></span>

# <a name="desktop"></a>[<span data-ttu-id="46ad8-163">桌面</span><span class="sxs-lookup"><span data-stu-id="46ad8-163">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="显示选项卡的 UI 分析的图示。" border="false":::

|<span data-ttu-id="46ad8-165">计数器</span><span class="sxs-lookup"><span data-stu-id="46ad8-165">Counter</span></span>|<span data-ttu-id="46ad8-166">说明</span><span class="sxs-lookup"><span data-stu-id="46ad8-166">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="46ad8-167">1</span><span class="sxs-lookup"><span data-stu-id="46ad8-167">1</span></span>|<span data-ttu-id="46ad8-168">**选项卡名称**：选项卡的导航标签。</span><span class="sxs-lookup"><span data-stu-id="46ad8-168">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="46ad8-169">2</span><span class="sxs-lookup"><span data-stu-id="46ad8-169">2</span></span>|<span data-ttu-id="46ad8-170">**Tab 溢出**：打开选项卡操作，如重命名和删除。</span><span class="sxs-lookup"><span data-stu-id="46ad8-170">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="46ad8-171">3</span><span class="sxs-lookup"><span data-stu-id="46ad8-171">3</span></span>|<span data-ttu-id="46ad8-172">**选项卡聊天**：在右侧打开聊天，允许用户在内容旁边进行对话。</span><span class="sxs-lookup"><span data-stu-id="46ad8-172">**Tab chat**: Opens a chat to the right, allowing users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="46ad8-173">4 </span><span class="sxs-lookup"><span data-stu-id="46ad8-173">4</span></span>|<span data-ttu-id="46ad8-174">**iframe：** 显示应用内容。</span><span class="sxs-lookup"><span data-stu-id="46ad8-174">**iframe**: Displays your app content.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="46ad8-175">移动</span><span class="sxs-lookup"><span data-stu-id="46ad8-175">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-view-tab-anatomy.png" alt-text="显示选项卡的 UI 分析的图示。" border="false":::

|<span data-ttu-id="46ad8-177">计数器</span><span class="sxs-lookup"><span data-stu-id="46ad8-177">Counter</span></span>|<span data-ttu-id="46ad8-178">说明</span><span class="sxs-lookup"><span data-stu-id="46ad8-178">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="46ad8-179">1</span><span class="sxs-lookup"><span data-stu-id="46ad8-179">1</span></span>|<span data-ttu-id="46ad8-180">**选项卡名称**：选项卡的导航标签。</span><span class="sxs-lookup"><span data-stu-id="46ad8-180">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="46ad8-181">2</span><span class="sxs-lookup"><span data-stu-id="46ad8-181">2</span></span>|<span data-ttu-id="46ad8-182">**选项卡聊天**：打开允许用户在内容旁进行对话的聊天。</span><span class="sxs-lookup"><span data-stu-id="46ad8-182">**Tab chat**: Opens a chat that allows users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="46ad8-183">3</span><span class="sxs-lookup"><span data-stu-id="46ad8-183">3</span></span>|<span data-ttu-id="46ad8-184">**webview：** 显示应用内容。</span><span class="sxs-lookup"><span data-stu-id="46ad8-184">**webview**: Displays your app content.</span></span>|

---

### <a name="designing-a-tab-with-ui-templates-and-advanced-components"></a><span data-ttu-id="46ad8-185">使用 UI 模板和高级组件设计选项卡</span><span class="sxs-lookup"><span data-stu-id="46ad8-185">Designing a tab with UI templates and advanced components</span></span>

<span data-ttu-id="46ad8-186">使用以下模板和Teams之一来帮助设计选项卡体验：</span><span class="sxs-lookup"><span data-stu-id="46ad8-186">Use one of the following Teams templates and components to help design your tab experience:</span></span>

* <span data-ttu-id="46ad8-187">[列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可扫描的格式显示相关项，并允许用户对整个列表或单个项目采取操作。</span><span class="sxs-lookup"><span data-stu-id="46ad8-187">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="46ad8-188">[任务板](../../concepts/design/design-teams-app-ui-templates.md#task-board)：任务板（有时称为看板或街道）是一组卡片，通常用于跟踪工作项或票证的状态。</span><span class="sxs-lookup"><span data-stu-id="46ad8-188">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="46ad8-189">[仪表板](../../concepts/design/design-teams-app-ui-templates.md#dashboard)：仪表板是包含多个卡片的画布，可提供数据或内容的概述。</span><span class="sxs-lookup"><span data-stu-id="46ad8-189">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="46ad8-190">[表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单用于以结构化方式收集、验证和提交用户输入。</span><span class="sxs-lookup"><span data-stu-id="46ad8-190">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="46ad8-191">[空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。</span><span class="sxs-lookup"><span data-stu-id="46ad8-191">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="46ad8-192">[左侧导航](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav)：如果你的选项卡需要一些导航，左侧导航组件会有所帮助。</span><span class="sxs-lookup"><span data-stu-id="46ad8-192">[Left nav](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav): The left nav component can help if your tab requires some navigation.</span></span> <span data-ttu-id="46ad8-193">通常，应使 Tab 键导航保持在最低程度。</span><span class="sxs-lookup"><span data-stu-id="46ad8-193">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-tab-to-collaborate"></a><span data-ttu-id="46ad8-194">使用选项卡进行协作</span><span class="sxs-lookup"><span data-stu-id="46ad8-194">Use a tab to collaborate</span></span>

<span data-ttu-id="46ad8-195">选项卡有助于就中心位置的内容展开对话。</span><span class="sxs-lookup"><span data-stu-id="46ad8-195">Tabs help facilitate conversations about content in a central location.</span></span>

### <a name="thread-discussion"></a><span data-ttu-id="46ad8-196">线程讨论</span><span class="sxs-lookup"><span data-stu-id="46ad8-196">Thread discussion</span></span>

<span data-ttu-id="46ad8-197">用户一旦添加了新选项卡，就可以自动发布至频道或聊天。这不仅向团队成员通知新内容并提供指向选项卡的链接，还允许用户开始讨论选项卡。</span><span class="sxs-lookup"><span data-stu-id="46ad8-197">Users can automatically post to a channel or chat once they’ve added a new tab. This not only notifies team members of the new content and provides a link to tab, it allows people to start talking about the tab.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="46ad8-198">桌面</span><span class="sxs-lookup"><span data-stu-id="46ad8-198">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="示例显示正在频道线程中讨论的选项卡。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="46ad8-200">移动</span><span class="sxs-lookup"><span data-stu-id="46ad8-200">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-use-tab-channel.png" alt-text="示例显示在频道线程中讨论的移动选项卡。" border="false":::

---

### <a name="tab-chat"></a><span data-ttu-id="46ad8-202">选项卡聊天</span><span class="sxs-lookup"><span data-stu-id="46ad8-202">Tab chat</span></span>

<span data-ttu-id="46ad8-203">用户可以在正在查看的选项卡内容旁边进行对话。</span><span class="sxs-lookup"><span data-stu-id="46ad8-203">Users can have a conversation next to the tab content they're viewing.</span></span> <span data-ttu-id="46ad8-204">在桌面上，聊天将打开到应用内容的一侧。</span><span class="sxs-lookup"><span data-stu-id="46ad8-204">On desktop, the chat opens to the side of the app content.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="46ad8-205">桌面</span><span class="sxs-lookup"><span data-stu-id="46ad8-205">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="示例显示一个在右侧打开聊天的选项卡。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="46ad8-207">移动</span><span class="sxs-lookup"><span data-stu-id="46ad8-207">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-use-tab-side-chat.png" alt-text="示例显示具有上下文内聊天区域的移动选项卡。" border="false":::

---

### <a name="permissions-and-role-based-views"></a><span data-ttu-id="46ad8-209">权限和基于角色的视图</span><span class="sxs-lookup"><span data-stu-id="46ad8-209">Permissions and role-based views</span></span>

<span data-ttu-id="46ad8-210">选项卡体验可能因用户的权限不同而不同。</span><span class="sxs-lookup"><span data-stu-id="46ad8-210">The tab experience may be different for users depending on their permissions.</span></span> <span data-ttu-id="46ad8-211">例如，一个用户无需登录即可访问选项卡。</span><span class="sxs-lookup"><span data-stu-id="46ad8-211">For example, one user can access the tab without having to sign in.</span></span> <span data-ttu-id="46ad8-212">但是，另一个用户必须签名，并且会看到略有不同的内容。</span><span class="sxs-lookup"><span data-stu-id="46ad8-212">Another user, however, must sign and will see slightly different content.</span></span>

## <a name="manage-a-tab"></a><span data-ttu-id="46ad8-213">管理选项卡</span><span class="sxs-lookup"><span data-stu-id="46ad8-213">Manage a tab</span></span>

<span data-ttu-id="46ad8-214">您可以包括用于重命名、删除或修改选项卡的选项。</span><span class="sxs-lookup"><span data-stu-id="46ad8-214">You can include options to rename, remove, or modify a tab.</span></span>

### <a name="anatomy-tab-menu"></a><span data-ttu-id="46ad8-215">结构：选项卡菜单</span><span class="sxs-lookup"><span data-stu-id="46ad8-215">Anatomy: Tab menu</span></span>

# <a name="desktop"></a>[<span data-ttu-id="46ad8-216">桌面</span><span class="sxs-lookup"><span data-stu-id="46ad8-216">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="显示选项卡菜单的 UI 分析的图示。" border="false":::

|<span data-ttu-id="46ad8-218">计数器</span><span class="sxs-lookup"><span data-stu-id="46ad8-218">Counter</span></span>|<span data-ttu-id="46ad8-219">说明</span><span class="sxs-lookup"><span data-stu-id="46ad8-219">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="46ad8-220">1</span><span class="sxs-lookup"><span data-stu-id="46ad8-220">1</span></span>|<span data-ttu-id="46ad8-221">**设置**： (可选) 允许用户在添加选项卡后修改其设置。</span><span class="sxs-lookup"><span data-stu-id="46ad8-221">**Settings**: (Optional) Allows users to modify a tab’s settings after it’s been added.</span></span>|
|<span data-ttu-id="46ad8-222">2</span><span class="sxs-lookup"><span data-stu-id="46ad8-222">2</span></span>|<span data-ttu-id="46ad8-223">**重命名**：用户可以为选项卡指定对频道、聊天或会议有意义的名称。</span><span class="sxs-lookup"><span data-stu-id="46ad8-223">**Rename**: Users can give the tab a name that’s meaningful to the channel, chat, or meeting.</span></span>|
|<span data-ttu-id="46ad8-224">3</span><span class="sxs-lookup"><span data-stu-id="46ad8-224">3</span></span>|<span data-ttu-id="46ad8-225">**删除**：从频道、聊天或会议中删除选项卡。</span><span class="sxs-lookup"><span data-stu-id="46ad8-225">**Remove**: Removes the tab from the channel, chat, or meeting.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="46ad8-226">移动</span><span class="sxs-lookup"><span data-stu-id="46ad8-226">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-manage-tab-menu-anatomy.png" alt-text="显示移动选项卡菜单的 UI 分析的图示。" border="false":::

|<span data-ttu-id="46ad8-228">计数器</span><span class="sxs-lookup"><span data-stu-id="46ad8-228">Counter</span></span>|<span data-ttu-id="46ad8-229">说明</span><span class="sxs-lookup"><span data-stu-id="46ad8-229">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="46ad8-230">1</span><span class="sxs-lookup"><span data-stu-id="46ad8-230">1</span></span>|<span data-ttu-id="46ad8-231">**在浏览器中打开**：在设备的默认浏览器中打开应用。</span><span class="sxs-lookup"><span data-stu-id="46ad8-231">**Open in browser**: Opens the app in the device’s default browser.</span></span>|
|<span data-ttu-id="46ad8-232">2</span><span class="sxs-lookup"><span data-stu-id="46ad8-232">2</span></span>|<span data-ttu-id="46ad8-233">**复制链接**：用户可以复制并共享指向选项卡的链接。</span><span class="sxs-lookup"><span data-stu-id="46ad8-233">**Copy link**: Users can copy and share a link to the tab.</span></span>|
|<span data-ttu-id="46ad8-234">3</span><span class="sxs-lookup"><span data-stu-id="46ad8-234">3</span></span>|<span data-ttu-id="46ad8-235">**设置： (** 选项卡) 后修改选项卡的设置的可选选项。</span><span class="sxs-lookup"><span data-stu-id="46ad8-235">**Settings**: (Optional) Modify a tab’s settings after it's been added.</span></span>|
|<span data-ttu-id="46ad8-236">4 </span><span class="sxs-lookup"><span data-stu-id="46ad8-236">4</span></span>|<span data-ttu-id="46ad8-237">**重命名**：用户可以为选项卡指定对频道、聊天或会议有意义的名称。</span><span class="sxs-lookup"><span data-stu-id="46ad8-237">**Rename**: Users can give the tab a name that's meaningful to the channel, chat, or meeting.</span></span>|
|<span data-ttu-id="46ad8-238">5 </span><span class="sxs-lookup"><span data-stu-id="46ad8-238">5</span></span>|<span data-ttu-id="46ad8-239">**删除**：从频道、聊天或会议中删除选项卡。</span><span class="sxs-lookup"><span data-stu-id="46ad8-239">**Delete**: Removes the tab from the channel, chat, or meeting.</span></span>|

---

## <a name="tab-notifications-and-deep-linking"></a><span data-ttu-id="46ad8-240">选项卡通知和深层链接</span><span class="sxs-lookup"><span data-stu-id="46ad8-240">Tab notifications and deep linking</span></span>

<span data-ttu-id="46ad8-241">你可以向选项卡发送包含深层链接的邮件。例如，卡片显示用户可选择在选项卡中查看整个 Bug 的 Bug 数据的摘要。发送有关选项卡活动的消息可提升感知度，而无需明确通知 (，即无噪音活动) 。</span><span class="sxs-lookup"><span data-stu-id="46ad8-241">You can send a message with a deep link to your tab. For example, a card shows a summary of bug data a user can select to see the entire bug in a tab. Sending messages about tab activity increases awareness without explicitly notifying everyone (i.e., activity without noise).</span></span> <span data-ttu-id="46ad8-242">如果需要，@mention特定用户。</span><span class="sxs-lookup"><span data-stu-id="46ad8-242">You also can @mention specific users if needed.</span></span>

<span data-ttu-id="46ad8-243">通过以下方法之一通知用户选项卡活动：</span><span class="sxs-lookup"><span data-stu-id="46ad8-243">Notify users of tab activity one of the following ways:</span></span>

* <span data-ttu-id="46ad8-244">**Bot：** 此方法是首选方法，尤其是在选项卡线程具有目标时。</span><span class="sxs-lookup"><span data-stu-id="46ad8-244">**Bot**: This method is preferred especially if the tab thread is targeted.</span></span> <span data-ttu-id="46ad8-245">选项卡的线程对话将移动到最近处于活动状态的视图中。</span><span class="sxs-lookup"><span data-stu-id="46ad8-245">The tab’s threaded conversation is moved into view as recently active.</span></span> <span data-ttu-id="46ad8-246">此方法还允许通知发送方式的一些复杂程度。</span><span class="sxs-lookup"><span data-stu-id="46ad8-246">This method also allows for some sophistication in how the notification is sent.</span></span>
* <span data-ttu-id="46ad8-247">**消息**：用户的活动源中显示一条消息，包含指向选项卡 [的深层链接](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="46ad8-247">**Message**: A message shows up in the user’s activity feed with a [deep link to the tab](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span></span>

## <a name="best-practices"></a><span data-ttu-id="46ad8-248">最佳做法</span><span class="sxs-lookup"><span data-stu-id="46ad8-248">Best practices</span></span>

<span data-ttu-id="46ad8-249">使用这些建议创建高质量的应用体验：</span><span class="sxs-lookup"><span data-stu-id="46ad8-249">Use these recommendations to create a quality app experience:</span></span>

### <a name="collaboration"></a><span data-ttu-id="46ad8-250">协作</span><span class="sxs-lookup"><span data-stu-id="46ad8-250">Collaboration</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="插图显示选项卡导航设计如何操作。" border="false":::

#### <a name="do-facilitate-conversation"></a><span data-ttu-id="46ad8-252">应做：促进对话</span><span class="sxs-lookup"><span data-stu-id="46ad8-252">Do: Facilitate conversation</span></span>

<span data-ttu-id="46ad8-253">包括用户可以讨论的内容和组件。</span><span class="sxs-lookup"><span data-stu-id="46ad8-253">Include content and components people can talk about.</span></span> <span data-ttu-id="46ad8-254">如果它不适合聊天、频道或会议上下文，则它不属于你的选项卡。</span><span class="sxs-lookup"><span data-stu-id="46ad8-254">If it doesn’t fit within the context of a chat, channel, or meeting, it doesn’t belong in your tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="示例显示不与选项卡导航设计一起执行哪些操作。" border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a><span data-ttu-id="46ad8-256">请勿：将选项卡视为任何其他网页</span><span class="sxs-lookup"><span data-stu-id="46ad8-256">Don't: Treat your tab like any other webpage</span></span>

<span data-ttu-id="46ad8-257">选项卡不是某人可能查看过一次的网页。</span><span class="sxs-lookup"><span data-stu-id="46ad8-257">A tab isn’t a webpage someone might view once.</span></span> <span data-ttu-id="46ad8-258">选项卡应显示用户共同完成某些任务所需的最重要的相关内容。</span><span class="sxs-lookup"><span data-stu-id="46ad8-258">A tab should display your most important, relevant content that people need to accomplish something together.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="46ad8-259">导航</span><span class="sxs-lookup"><span data-stu-id="46ad8-259">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="显示选项卡导航设计要执行哪些操作的示例。" border="false":::

#### <a name="do-limit-tasks-and-data"></a><span data-ttu-id="46ad8-261">操作：限制任务和数据</span><span class="sxs-lookup"><span data-stu-id="46ad8-261">Do: Limit tasks and data</span></span>

<span data-ttu-id="46ad8-262">选项卡在满足特定需求时效果最佳。</span><span class="sxs-lookup"><span data-stu-id="46ad8-262">Tabs work best when they address specific needs.</span></span> <span data-ttu-id="46ad8-263">包含一组有限的与团队或组相关的任务和数据。</span><span class="sxs-lookup"><span data-stu-id="46ad8-263">Include a limited set of tasks and data relevant to the team or group.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="插图显示不与选项卡导航设计有关的内容。" border="false":::

#### <a name="dont-embed-your-entire-app"></a><span data-ttu-id="46ad8-265">请勿：嵌入整个应用</span><span class="sxs-lookup"><span data-stu-id="46ad8-265">Don't: Embed your entire app</span></span>

<span data-ttu-id="46ad8-266">使用选项卡显示具有多级导航和复杂交互的整个应用会导致信息过载。</span><span class="sxs-lookup"><span data-stu-id="46ad8-266">Using a tab to display an entire app with multi-level navigation and complex interactions leads to information overload.</span></span>

   :::column-end:::
:::row-end:::

### <a name="setup"></a><span data-ttu-id="46ad8-267">设置</span><span class="sxs-lookup"><span data-stu-id="46ad8-267">Setup</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="插图显示选项卡设置设计要执行哪些操作。" border="false":::

#### <a name="do-keep-it-simple"></a><span data-ttu-id="46ad8-269">应做之事：保持简单</span><span class="sxs-lookup"><span data-stu-id="46ad8-269">Do: Keep it simple</span></span>

<span data-ttu-id="46ad8-270">如果你的应用需要身份验证，请尝试将 Microsoft 单一登录 (SSO) 集成，实现更加无缝的登录体验。</span><span class="sxs-lookup"><span data-stu-id="46ad8-270">If your app requires authentication, try integrating Microsoft single sign-on (SSO) for a more seamless sign-in experience.</span></span> <span data-ttu-id="46ad8-271">此外，仅包括添加选项卡的必需信息和步骤。</span><span class="sxs-lookup"><span data-stu-id="46ad8-271">Also, only include essential information and steps to add the tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="插图显示与选项卡设置设计不一样。" border="false":::

#### <a name="dont-have-too-many-steps"></a><span data-ttu-id="46ad8-273">不要：步骤过多</span><span class="sxs-lookup"><span data-stu-id="46ad8-273">Don't: Have too many steps</span></span>

<span data-ttu-id="46ad8-274">删除添加选项卡的不必要的步骤。</span><span class="sxs-lookup"><span data-stu-id="46ad8-274">Remove any unnecessary steps for adding a tab.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="46ad8-275">主题</span><span class="sxs-lookup"><span data-stu-id="46ad8-275">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="插图显示使用制表位设置要执行哪些操作。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="46ad8-277">应做：利用Teams令牌</span><span class="sxs-lookup"><span data-stu-id="46ad8-277">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="46ad8-278">每个Teams主题都有自己的配色方案。</span><span class="sxs-lookup"><span data-stu-id="46ad8-278">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="46ad8-279">若要自动处理主题更改，请 <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank"> (Fluent UI </a>) 颜色标记。</span><span class="sxs-lookup"><span data-stu-id="46ad8-279">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="插图显示不与选项卡设置有关的内容。" border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="46ad8-281">请勿：硬编码颜色值</span><span class="sxs-lookup"><span data-stu-id="46ad8-281">Don't: Hard code color values</span></span>

<span data-ttu-id="46ad8-282">如果不使用颜色令牌Teams，你的设计将不太可扩展，并且需要更多的时间进行管理。</span><span class="sxs-lookup"><span data-stu-id="46ad8-282">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::
