---
title: 创建选项卡删除页
author: laujan
description: 如何创建选项卡删除页
keywords: teams 选项卡组频道可配置删除删除
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 8f01780dce9aa0450169d4c699471bb2ac5bd9a0
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019585"
---
# <a name="modify-or-remove-a-channel-group-tab"></a><span data-ttu-id="80939-104">修改或删除频道组选项卡</span><span class="sxs-lookup"><span data-stu-id="80939-104">Modify or remove a channel group tab</span></span>

<span data-ttu-id="80939-105">可以通过在应用中支持删除和修改选项来扩展和增强用户体验。</span><span class="sxs-lookup"><span data-stu-id="80939-105">You can extend and enhance the user experience by supporting removal and modification options in your app.</span></span> <span data-ttu-id="80939-106">Teams 允许用户重命名或删除频道/组选项卡，并且你可以允许用户在安装后重新配置选项卡。</span><span class="sxs-lookup"><span data-stu-id="80939-106">Teams enables users to rename or remove a channel/group tab and you can permit users to reconfigure your tab after installation.</span></span> <span data-ttu-id="80939-107">此外，选项卡删除体验可能包括指定在删除选项卡时对内容会发生什么情况，或者为用户提供删除后选项（如删除或存档内容）。</span><span class="sxs-lookup"><span data-stu-id="80939-107">Additionally, your tab removal experience can include designating what happens to the content when your tab is removed or giving users post-removal options such as deleting or archiving the content.</span></span>

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a><span data-ttu-id="80939-108">启用选项卡以在安装后重新配置</span><span class="sxs-lookup"><span data-stu-id="80939-108">Enable your tab to be reconfigured after installation</span></span>

<span data-ttu-id="80939-109">你的 **manifest.js** 定义选项卡的特性和功能。</span><span class="sxs-lookup"><span data-stu-id="80939-109">Your **manifest.json** defines your tab's features and capabilities.</span></span> <span data-ttu-id="80939-110">选项卡实例属性采用一个布尔值，该值指示用户是否可以在选项卡创建后修改 `canUpdateConfiguration` 或重新配置它：</span><span class="sxs-lookup"><span data-stu-id="80939-110">The tab instance `canUpdateConfiguration` property takes a Boolean value that indicates whether a user can modify or reconfigure the tab after it is created:</span></span>

|<span data-ttu-id="80939-111">名称</span><span class="sxs-lookup"><span data-stu-id="80939-111">Name</span></span>| <span data-ttu-id="80939-112">类型</span><span class="sxs-lookup"><span data-stu-id="80939-112">Type</span></span>| <span data-ttu-id="80939-113">最大大小</span><span class="sxs-lookup"><span data-stu-id="80939-113">Maximum size</span></span> | <span data-ttu-id="80939-114">必需</span><span class="sxs-lookup"><span data-stu-id="80939-114">Required</span></span> | <span data-ttu-id="80939-115">说明</span><span class="sxs-lookup"><span data-stu-id="80939-115">Description</span></span>|
|---|---|---|---|---|
|`canUpdateConfiguration`|<span data-ttu-id="80939-116">Boolean</span><span class="sxs-lookup"><span data-stu-id="80939-116">Boolean</span></span>|||<span data-ttu-id="80939-117">一个值，指示用户创建后是否可以更新选项卡配置的实例。</span><span class="sxs-lookup"><span data-stu-id="80939-117">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="80939-118">默认值： `true`</span><span class="sxs-lookup"><span data-stu-id="80939-118">Default: `true`</span></span>|

<span data-ttu-id="80939-119">将选项卡上传到频道或群聊后，Teams 会为选项卡添加右键单击下拉菜单。可用选项由以下设置 `canUpdateConfiguration` 决定：</span><span class="sxs-lookup"><span data-stu-id="80939-119">When your tab is uploaded to a channel or group chat, Teams will add a right-click drop-down menu for your tab. The available options are determined by the `canUpdateConfiguration` setting:</span></span>

| `canUpdateConfiguration`| <span data-ttu-id="80939-120">true</span><span class="sxs-lookup"><span data-stu-id="80939-120">true</span></span>   | <span data-ttu-id="80939-121">false</span><span class="sxs-lookup"><span data-stu-id="80939-121">false</span></span> | <span data-ttu-id="80939-122">说明</span><span class="sxs-lookup"><span data-stu-id="80939-122">description</span></span> |
| ----------------------- | :----: | ----- | ----------- |
|     <span data-ttu-id="80939-123">设置</span><span class="sxs-lookup"><span data-stu-id="80939-123">Settings</span></span>            |   <span data-ttu-id="80939-124">√</span><span class="sxs-lookup"><span data-stu-id="80939-124">√</span></span>    |       |<span data-ttu-id="80939-125">页面 `configurationUrl` 在 IFrame 中重新加载，允许用户重新配置选项卡。</span><span class="sxs-lookup"><span data-stu-id="80939-125">The `configurationUrl` page is reloaded in an IFrame allowing the user to reconfigure the tab.</span></span>  |
|     <span data-ttu-id="80939-126">重命名</span><span class="sxs-lookup"><span data-stu-id="80939-126">Rename</span></span>              |   <span data-ttu-id="80939-127">√</span><span class="sxs-lookup"><span data-stu-id="80939-127">√</span></span>    |   <span data-ttu-id="80939-128">√</span><span class="sxs-lookup"><span data-stu-id="80939-128">√</span></span>   | <span data-ttu-id="80939-129">用户可以更改选项卡名称，因为它显示在选项卡栏中。</span><span class="sxs-lookup"><span data-stu-id="80939-129">The user can change the tab name as it appears in the tab bar.</span></span>          |
|     <span data-ttu-id="80939-130">删除</span><span class="sxs-lookup"><span data-stu-id="80939-130">Remove</span></span>              |   <span data-ttu-id="80939-131">√</span><span class="sxs-lookup"><span data-stu-id="80939-131">√</span></span>    |   <span data-ttu-id="80939-132">√</span><span class="sxs-lookup"><span data-stu-id="80939-132">√</span></span>   |  <span data-ttu-id="80939-133">如果  `removeURL` 属性和值包含在配置 **页中，** 则删除 **页面** 将加载到 IFrame 中，并呈现给用户。</span><span class="sxs-lookup"><span data-stu-id="80939-133">If the  `removeURL` property and value are included in the **configuration page**, the **removal page** is loaded into an IFrame and presented to the user.</span></span> <span data-ttu-id="80939-134">如果未包含删除页，则向用户显示一个确认对话框。</span><span class="sxs-lookup"><span data-stu-id="80939-134">If a removal page is not included the user is presented with a confirm dialog box.</span></span>          |
|||||

## <a name="create-a-tab-removal-page-for-your-application"></a><span data-ttu-id="80939-135">为应用程序创建选项卡删除页</span><span class="sxs-lookup"><span data-stu-id="80939-135">Create a tab removal page for your application</span></span>

<span data-ttu-id="80939-136">可选删除页是一个您托管的 HTML 页，在删除选项卡时将显示该页。</span><span class="sxs-lookup"><span data-stu-id="80939-136">The optional removal page is an HTML page that you host and is displayed when the tab is removed.</span></span> <span data-ttu-id="80939-137">删除页面 URL 由配置页 `setSettings()` 中的 方法指定。</span><span class="sxs-lookup"><span data-stu-id="80939-137">The removal page URL is designated by the `setSettings()` method within your configuration page.</span></span> <span data-ttu-id="80939-138">与应用中的所有页面一样，删除页面必须符合 [Teams 选项卡要求](../../../tabs/how-to/tab-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="80939-138">As with all pages in your app, the removal page must comply with [Teams tab requirements](../../../tabs/how-to/tab-requirements.md).</span></span>

### <a name="register-a-remove-handler"></a><span data-ttu-id="80939-139">注册删除处理程序</span><span class="sxs-lookup"><span data-stu-id="80939-139">Register a remove handler</span></span>

<span data-ttu-id="80939-140">（可选）在删除页面逻辑中，您可以在用户删除现有选项卡配置时 `registerOnRemoveHandler((RemoveEvent) => {}` 调用事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="80939-140">Optionally, within your removal page logic, you can  invoke the `registerOnRemoveHandler((RemoveEvent) => {}` event handler when the user removes an existing tab configuration.</span></span> <span data-ttu-id="80939-141">当用户尝试删除内容时，该方法将接受 接口并执行 [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) 处理程序中的代码。</span><span class="sxs-lookup"><span data-stu-id="80939-141">The  method takes in the [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) interface and executes the code in the handler when a user attempts to remove content.</span></span> <span data-ttu-id="80939-142">它用于执行清理操作，例如删除支持选项卡内容的基础资源。</span><span class="sxs-lookup"><span data-stu-id="80939-142">It is used to perform cleanup operations such as removing the underlying resource powering the tab content.</span></span> <span data-ttu-id="80939-143">一次只能注册一个删除处理程序。</span><span class="sxs-lookup"><span data-stu-id="80939-143">Only one remove handler can be registered at a time.</span></span>

<span data-ttu-id="80939-144">该 `RemoveEvent` 接口使用两种方法描述对象：</span><span class="sxs-lookup"><span data-stu-id="80939-144">The `RemoveEvent` interface describes an object with two methods:</span></span>

* <span data-ttu-id="80939-145">`notifySuccess()`此函数是必需的。</span><span class="sxs-lookup"><span data-stu-id="80939-145">The `notifySuccess()` function is required.</span></span> <span data-ttu-id="80939-146">它表示已成功删除基础资源，并且可删除其内容。</span><span class="sxs-lookup"><span data-stu-id="80939-146">It indicates that the removal of the underlying resource succeeded and its content can be removed.</span></span>

* <span data-ttu-id="80939-147">函数 `notifyFailure(string)` 是可选的。</span><span class="sxs-lookup"><span data-stu-id="80939-147">The `notifyFailure(string)` function is optional.</span></span> <span data-ttu-id="80939-148">它指示删除基础资源失败，并且无法删除其内容。</span><span class="sxs-lookup"><span data-stu-id="80939-148">It indicates that removal of the underlying resource failed and its content cannot be removed.</span></span> <span data-ttu-id="80939-149">可选字符串参数指定失败的原因。</span><span class="sxs-lookup"><span data-stu-id="80939-149">The optional string parameter specifies a reason for the failure.</span></span> <span data-ttu-id="80939-150">如果提供，则向用户显示此字符串;否则将显示一般性错误。</span><span class="sxs-lookup"><span data-stu-id="80939-150">If provided, this string is displayed to the user; otherwise a generic error is displayed.</span></span>

#### <a name="use-the-getsettings-function"></a><span data-ttu-id="80939-151">使用 `getSettings()` 函数</span><span class="sxs-lookup"><span data-stu-id="80939-151">Use the `getSettings()` function</span></span>

<span data-ttu-id="80939-152">可以使用 指定 `getSettings()` 要删除的选项卡内容。</span><span class="sxs-lookup"><span data-stu-id="80939-152">You can use `getSettings()`to designate the tab content to be removed.</span></span> <span data-ttu-id="80939-153">`getSettings((Settings) =>{})`函数接受 [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) 并提供可以检索的有效 settings 属性值。</span><span class="sxs-lookup"><span data-stu-id="80939-153">The `getSettings((Settings) =>{})` function takes in the [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) and provides the valid settings property values that can be retrieved.</span></span>

#### <a name="use-the-getcontext-function"></a><span data-ttu-id="80939-154">使用 `getContext()` 函数</span><span class="sxs-lookup"><span data-stu-id="80939-154">Use the `getContext()` function</span></span>

<span data-ttu-id="80939-155">可以使用 `getContext()` 检索正在运行帧的当前上下文。</span><span class="sxs-lookup"><span data-stu-id="80939-155">You can use `getContext()` to retrieves the current context in which the frame is running.</span></span> <span data-ttu-id="80939-156">函数接受 并提供可在删除页面逻辑中用于确定要显示在删除页 `getContext((Context) =>{})` [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) 中的内容 `Context` 的有效属性值。</span><span class="sxs-lookup"><span data-stu-id="80939-156">The `getContext((Context) =>{})` function takes in the [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) and provides valid `Context` property values that you can use in your removal page logic to determine the content to display in the removal page.</span></span>

#### <a name="include-authentication"></a><span data-ttu-id="80939-157">包括身份验证</span><span class="sxs-lookup"><span data-stu-id="80939-157">Include authentication</span></span>

<span data-ttu-id="80939-158">在允许用户删除选项卡内容之前，您可能需要进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="80939-158">You might require authentication before allowing a user to delete the tab content.</span></span> <span data-ttu-id="80939-159">上下文信息可用于帮助构建身份验证请求和授权页面 URL。</span><span class="sxs-lookup"><span data-stu-id="80939-159">Context information can be used to help construct authentication requests and authorization page URLs.</span></span> <span data-ttu-id="80939-160">有关 [选项卡，请参阅 Microsoft Teams 身份验证流](~/tabs/how-to/authentication/auth-flow-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="80939-160">See [Microsoft Teams authentication flow for tabs](~/tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="80939-161">确保选项卡页中使用的所有域都列在 `manifest.json` `validDomains` 数组中。</span><span class="sxs-lookup"><span data-stu-id="80939-161">Make sure that all domains used in your tab pages are listed in the `manifest.json` `validDomains` array.</span></span>

<span data-ttu-id="80939-162">下面是一个示例选项卡删除代码块：</span><span class="sxs-lookup"><span data-stu-id="80939-162">Below is a sample tab removal code block:</span></span>

```html
<body>
  <button onclick="onClick()">Delete this tab and all underlying data?</button>
  <script>
    microsoftTeams.initialize();
    microsoftTeams.settings.registerOnRemoveHandler((removeEvent) => {
      // Here you can designate the tab content to be removed and/or archived.
        microsoftTeams.settings.getSettings((settings) => {
        settings.contentUrl = "..."
        });
        removeEvent.notifySuccess();
    });

    const onClick() => {
        microsoftTeams.settings.setValidityState(true);
    }
  </script>
</body>

```

<span data-ttu-id="80939-163">当用户从选项卡的下拉菜单中选择"删除"时，Teams 将 (配置页中指定的可选页面) `removeUrl` IFrame 中。 </span><span class="sxs-lookup"><span data-stu-id="80939-163">When a user selects **Remove** from the tab's drop-down menu, Teams will load the optional `removeUrl` page (designated in your **configuration page**) into an IFrame.</span></span> <span data-ttu-id="80939-164">此处，用户会使用函数加载按钮，该按钮调用并启用位于删除页面 IFrame 底部附近的"删除" `onClick()` `microsoftTeams.settings.setValidityState(true)` 按钮。 </span><span class="sxs-lookup"><span data-stu-id="80939-164">Here, the user is presented with a button loaded with the `onClick()` function that calls `microsoftTeams.settings.setValidityState(true)` and enables the **Remove** button located near the bottom of the removal page IFrame.</span></span>

<span data-ttu-id="80939-165">执行删除处理程序后， `removeEvent.notifySuccess()` 或 `removeEvent.notifyFailure()` 通知 Teams 内容删除结果。</span><span class="sxs-lookup"><span data-stu-id="80939-165">Following the execution of the remove handler, `removeEvent.notifySuccess()` or `removeEvent.notifyFailure()` notifies Teams of the content removal outcome.</span></span>

>[!NOTE]
><span data-ttu-id="80939-166">为确保授权用户对选项卡的控制不会受到约束，Teams 将在成功和失败情况下删除选项卡。</span><span class="sxs-lookup"><span data-stu-id="80939-166">To ensure that an authorized user's control over a tab is not inhibited, Teams will remove the tab in both success and failure cases.</span></span>\
><span data-ttu-id="80939-167">Teams 在5 秒后启用"删除"按钮，即使你的选项卡未调用 `setValidityState()` 。</span><span class="sxs-lookup"><span data-stu-id="80939-167">Teams enables the **Remove** button after 5 seconds, even if your tab hasn't called `setValidityState()`.</span></span>\
><span data-ttu-id="80939-168">当用户选择" **删除** Teams"时，将在 30 秒后删除选项卡，无论操作是否已完成。</span><span class="sxs-lookup"><span data-stu-id="80939-168">When the user selects **Remove** Teams removes the tab after 30 seconds regardless of whether your actions have completed.</span></span>
