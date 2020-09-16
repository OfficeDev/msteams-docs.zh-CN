---
title: 创建选项卡删除页
author: laujan
description: 如何创建选项卡删除页
keywords: 团队选项卡组通道可配置删除删除
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: a8b40911de3e2519d8194415e2d8e467d0766ef2
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818897"
---
# <a name="modify-or-remove-a-channel-group-tab"></a><span data-ttu-id="91f56-104">修改或删除频道组选项卡</span><span class="sxs-lookup"><span data-stu-id="91f56-104">Modify or remove a channel group tab</span></span>

<span data-ttu-id="91f56-105">您可以通过在应用中支持删除和修改选项来扩展和增强用户体验。</span><span class="sxs-lookup"><span data-stu-id="91f56-105">You can extend and enhance the user experience by supporting removal and modification options in your app.</span></span> <span data-ttu-id="91f56-106">通过团队，用户可以重命名或删除频道/组选项卡，还可以允许用户在安装后重新配置您的选项卡。</span><span class="sxs-lookup"><span data-stu-id="91f56-106">Teams enables users to rename or remove a channel/group tab and you can permit users to reconfigure your tab after installation.</span></span> <span data-ttu-id="91f56-107">此外，您的选项卡删除体验可以包括在删除选项卡或授予用户删除内容（如删除或存档内容）时，指定内容会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="91f56-107">Additionally, your tab removal experience can include designating what happens to the content when your tab is removed or giving users post-removal options such as deleting or archiving the content.</span></span>

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a><span data-ttu-id="91f56-108">允许在安装后重新配置您的选项卡</span><span class="sxs-lookup"><span data-stu-id="91f56-108">Enable your tab to be reconfigured after installation</span></span>

<span data-ttu-id="91f56-109">您 \*\* 的manifest.js\*\* 定义您的选项卡的特性和功能。</span><span class="sxs-lookup"><span data-stu-id="91f56-109">Your **manifest.json** defines your tab's features and capabilities.</span></span> <span data-ttu-id="91f56-110">Tab 实例 `canUpdateConfiguration` 属性采用一个布尔值，该值指示用户是否可以在创建选项卡后修改或重新配置该选项卡：</span><span class="sxs-lookup"><span data-stu-id="91f56-110">The tab instance `canUpdateConfiguration` property takes a Boolean value that indicates whether a user can modify or reconfigure the tab after it is created:</span></span>

|<span data-ttu-id="91f56-111">名称</span><span class="sxs-lookup"><span data-stu-id="91f56-111">Name</span></span>| <span data-ttu-id="91f56-112">类型</span><span class="sxs-lookup"><span data-stu-id="91f56-112">Type</span></span>| <span data-ttu-id="91f56-113">最大大小</span><span class="sxs-lookup"><span data-stu-id="91f56-113">Maximum size</span></span> | <span data-ttu-id="91f56-114">必需</span><span class="sxs-lookup"><span data-stu-id="91f56-114">Required</span></span> | <span data-ttu-id="91f56-115">说明</span><span class="sxs-lookup"><span data-stu-id="91f56-115">Description</span></span>|
|---|---|---|---|---|
|`canUpdateConfiguration`|<span data-ttu-id="91f56-116">Boolean</span><span class="sxs-lookup"><span data-stu-id="91f56-116">Boolean</span></span>|||<span data-ttu-id="91f56-117">一个值，指示是否可在用户创建之后更新该选项卡的配置实例。</span><span class="sxs-lookup"><span data-stu-id="91f56-117">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="91f56-118">设置 `true`</span><span class="sxs-lookup"><span data-stu-id="91f56-118">Default: `true`</span></span>|

<span data-ttu-id="91f56-119">将选项卡上载到频道或组聊天后，团队将为您的选项卡添加一个右键单击下拉菜单。可用选项由 `canUpdateConfiguration` 以下设置决定：</span><span class="sxs-lookup"><span data-stu-id="91f56-119">When your tab is uploaded to a channel or group chat, Teams will add a right-click drop-down menu for your tab. The available options are determined by the `canUpdateConfiguration` setting:</span></span>

| `canUpdateConfiguration`| <span data-ttu-id="91f56-120">true</span><span class="sxs-lookup"><span data-stu-id="91f56-120">true</span></span>   | <span data-ttu-id="91f56-121">false</span><span class="sxs-lookup"><span data-stu-id="91f56-121">false</span></span> | <span data-ttu-id="91f56-122">description</span><span class="sxs-lookup"><span data-stu-id="91f56-122">description</span></span> |
| ----------------------- | :----: | ----- | ----------- |
|     <span data-ttu-id="91f56-123">设置</span><span class="sxs-lookup"><span data-stu-id="91f56-123">Settings</span></span>            |   <span data-ttu-id="91f56-124">√</span><span class="sxs-lookup"><span data-stu-id="91f56-124">√</span></span>    |       |<span data-ttu-id="91f56-125">`configurationUrl`页面在 IFrame 中重新加载，以允许用户重新配置选项卡。</span><span class="sxs-lookup"><span data-stu-id="91f56-125">The `configurationUrl` page is reloaded in an IFrame allowing the user to reconfigure the tab.</span></span>  |
|     <span data-ttu-id="91f56-126">重命名</span><span class="sxs-lookup"><span data-stu-id="91f56-126">Rename</span></span>              |   <span data-ttu-id="91f56-127">√</span><span class="sxs-lookup"><span data-stu-id="91f56-127">√</span></span>    |   <span data-ttu-id="91f56-128">√</span><span class="sxs-lookup"><span data-stu-id="91f56-128">√</span></span>   | <span data-ttu-id="91f56-129">用户可以更改在选项卡栏中显示的选项卡名称。</span><span class="sxs-lookup"><span data-stu-id="91f56-129">The user can change the tab name as it appears in the tab bar.</span></span>          |
|     <span data-ttu-id="91f56-130">删除</span><span class="sxs-lookup"><span data-stu-id="91f56-130">Remove</span></span>              |   <span data-ttu-id="91f56-131">√</span><span class="sxs-lookup"><span data-stu-id="91f56-131">√</span></span>    |   <span data-ttu-id="91f56-132">√</span><span class="sxs-lookup"><span data-stu-id="91f56-132">√</span></span>   |  <span data-ttu-id="91f56-133">如果  `removeURL` 属性和值包含在 **配置页面**中，则 **删除页面** 会加载到 IFrame 中，并向用户显示。</span><span class="sxs-lookup"><span data-stu-id="91f56-133">If the  `removeURL` property and value are included in the **configuration page**, the **removal page** is loaded into an IFrame and presented to the user.</span></span> <span data-ttu-id="91f56-134">如果不包含删除页面，则会向用户显示确认对话框。</span><span class="sxs-lookup"><span data-stu-id="91f56-134">If a removal page is not included the user is presented with a confirm dialog box.</span></span>          |
|||||

## <a name="create-a-tab-removal-page-for-your-application"></a><span data-ttu-id="91f56-135">为应用程序创建选项卡删除页</span><span class="sxs-lookup"><span data-stu-id="91f56-135">Create a tab removal page for your application</span></span>

<span data-ttu-id="91f56-136">可选的 "删除" 页面是您承载的 HTML 页面，在删除该选项卡时会显示该页面。</span><span class="sxs-lookup"><span data-stu-id="91f56-136">The optional removal page is an HTML page that you host and is displayed when the tab is removed.</span></span> <span data-ttu-id="91f56-137">删除页面 URL 由 `setSettings()` 配置页面中的方法指定。</span><span class="sxs-lookup"><span data-stu-id="91f56-137">The removal page URL is designated by the `setSettings()` method within your configuration page.</span></span> <span data-ttu-id="91f56-138">与应用程序中的所有页面一样，删除页必须符合 [团队选项卡要求](~/tabs/how-to/add-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="91f56-138">As with all pages in your app, the removal page must comply with [Teams tab requirements](~/tabs/how-to/add-tab.md).</span></span>

### <a name="register-a-remove-handler"></a><span data-ttu-id="91f56-139">注册删除处理程序</span><span class="sxs-lookup"><span data-stu-id="91f56-139">Register a remove handler</span></span>

<span data-ttu-id="91f56-140">（可选）在删除页面逻辑中，可以在 `registerOnRemoveHandler((RemoveEvent) => {}` 用户删除现有的选项卡配置时调用事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="91f56-140">Optionally, within your removal page logic, you can  invoke the `registerOnRemoveHandler((RemoveEvent) => {}` event handler when the user removes an existing tab configuration.</span></span> <span data-ttu-id="91f56-141">[`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest)当用户尝试删除内容时，该方法将采用接口，并在处理程序中执行代码。</span><span class="sxs-lookup"><span data-stu-id="91f56-141">The  method takes in the [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest) interface and executes the code in the handler when a user attempts to remove content.</span></span> <span data-ttu-id="91f56-142">它用于执行清理操作，例如，删除用于为选项卡内容加电的基础资源。</span><span class="sxs-lookup"><span data-stu-id="91f56-142">It is used to perform cleanup operations such as removing the underlying resource powering the tab content.</span></span> <span data-ttu-id="91f56-143">一次只能注册一个删除处理程序。</span><span class="sxs-lookup"><span data-stu-id="91f56-143">Only one remove handler can be registered at a time.</span></span>

<span data-ttu-id="91f56-144">该 `RemoveEvent` 接口描述了具有以下两种方法的对象：</span><span class="sxs-lookup"><span data-stu-id="91f56-144">The `RemoveEvent` interface describes an object with two methods:</span></span>

* <span data-ttu-id="91f56-145">`notifySuccess()`函数是必需的。</span><span class="sxs-lookup"><span data-stu-id="91f56-145">The `notifySuccess()` function is required.</span></span> <span data-ttu-id="91f56-146">它指示已成功删除基础资源，并且可以删除其内容。</span><span class="sxs-lookup"><span data-stu-id="91f56-146">It indicates that the removal of the underlying resource succeeded and its content can be removed.</span></span>

* <span data-ttu-id="91f56-147">`notifyFailure(string)`函数是可选的。</span><span class="sxs-lookup"><span data-stu-id="91f56-147">The `notifyFailure(string)` function is optional.</span></span> <span data-ttu-id="91f56-148">它指示删除基础资源失败且无法删除其内容。</span><span class="sxs-lookup"><span data-stu-id="91f56-148">It indicates that removal of the underlying resource failed and its content cannot be removed.</span></span> <span data-ttu-id="91f56-149">可选的字符串参数指定失败的原因。</span><span class="sxs-lookup"><span data-stu-id="91f56-149">The optional string parameter specifies a reason for the failure.</span></span> <span data-ttu-id="91f56-150">如果提供，则向用户显示此字符串;否则，将显示一个一般性错误。</span><span class="sxs-lookup"><span data-stu-id="91f56-150">If provided, this string is displayed to the user; otherwise a generic error is displayed.</span></span>

#### <a name="use-the-getsettings-function"></a><span data-ttu-id="91f56-151">使用 `getSettings()` 函数</span><span class="sxs-lookup"><span data-stu-id="91f56-151">Use the `getSettings()` function</span></span>

<span data-ttu-id="91f56-152">您可以使用 `getSettings()` 来指定要删除的选项卡内容。</span><span class="sxs-lookup"><span data-stu-id="91f56-152">You can use `getSettings()`to designate the tab content to be removed.</span></span> <span data-ttu-id="91f56-153">`getSettings((Settings) =>{})`函数采用 [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest) 并提供可检索的有效设置属性值。</span><span class="sxs-lookup"><span data-stu-id="91f56-153">The `getSettings((Settings) =>{})` function takes in the [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest) and provides the valid settings property values that can be retrieved.</span></span>

#### <a name="use-the-getcontext-function"></a><span data-ttu-id="91f56-154">使用 `getContext()` 函数</span><span class="sxs-lookup"><span data-stu-id="91f56-154">Use the `getContext()` function</span></span>

<span data-ttu-id="91f56-155">您可以使用 `getContext()` 来检索运行该帧的当前上下文。</span><span class="sxs-lookup"><span data-stu-id="91f56-155">You can use `getContext()` to retrieves the current context in which the frame is running.</span></span> <span data-ttu-id="91f56-156">`getContext((Context) =>{})`函数采用 [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) 并提供 `Context` 可在删除页面逻辑中使用的有效属性值，以确定要在删除页面中显示的内容。</span><span class="sxs-lookup"><span data-stu-id="91f56-156">The `getContext((Context) =>{})` function takes in the [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) and provides valid `Context` property values that you can use in your removal page logic to determine the content to display in the removal page.</span></span>

#### <a name="include-authentication"></a><span data-ttu-id="91f56-157">包括身份验证</span><span class="sxs-lookup"><span data-stu-id="91f56-157">Include authentication</span></span>

<span data-ttu-id="91f56-158">您可能需要先进行身份验证，然后才能允许用户删除选项卡内容。</span><span class="sxs-lookup"><span data-stu-id="91f56-158">You might require authentication before allowing a user to delete the tab content.</span></span> <span data-ttu-id="91f56-159">上下文信息可用于帮助构造身份验证请求和授权页面 Url。</span><span class="sxs-lookup"><span data-stu-id="91f56-159">Context information can be used to help construct authentication requests and authorization page URLs.</span></span> <span data-ttu-id="91f56-160">请参阅 [Microsoft 团队身份验证流的选项卡](~/tabs/how-to/authentication/auth-flow-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="91f56-160">See [Microsoft Teams authentication flow for tabs](~/tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="91f56-161">确保在您的选项卡页中使用的所有域都列在 `manifest.json` `validDomains` 数组中。</span><span class="sxs-lookup"><span data-stu-id="91f56-161">Make sure that all domains used in your tab pages are listed in the `manifest.json` `validDomains` array.</span></span>

<span data-ttu-id="91f56-162">以下是选项卡删除代码块示例：</span><span class="sxs-lookup"><span data-stu-id="91f56-162">Below is a sample tab removal code block:</span></span>

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

<span data-ttu-id="91f56-163">当用户从选项卡的下拉菜单中选择 " **删除** " 时，团队会将 " `removeUrl` 配置" **页面** 中指定的可选页面 () 到 IFrame 中。</span><span class="sxs-lookup"><span data-stu-id="91f56-163">When a user selects **Remove** from the tab's drop-down menu, Teams will load the optional `removeUrl` page (designated in your **configuration page**) into an IFrame.</span></span> <span data-ttu-id="91f56-164">此时，将向用户提供一个加载的按钮，该按钮 `onClick()` 调用 `microsoftTeams.settings.setValidityState(true)` 并启用位于删除页面 IFrame 底部附近的 " **删除** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="91f56-164">Here, the user is presented with a button loaded with the `onClick()` function that calls `microsoftTeams.settings.setValidityState(true)` and enables the **Remove** button located near the bottom of the removal page IFrame.</span></span>

<span data-ttu-id="91f56-165">执行删除处理程序后， `removeEvent.notifySuccess()` 或 `removeEvent.notifyFailure()` 通知团队内容删除结果。</span><span class="sxs-lookup"><span data-stu-id="91f56-165">Following the execution of the remove handler, `removeEvent.notifySuccess()` or `removeEvent.notifyFailure()` notifies Teams of the content removal outcome.</span></span>

>[!NOTE]
><span data-ttu-id="91f56-166">为了确保授权用户对选项卡的控制不被禁止，团队将删除成功和失败案例中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="91f56-166">To ensure that an authorized user's control over a tab is not inhibited, Teams will remove the tab in both success and failure cases.\</span></span>
><span data-ttu-id="91f56-167">即使您的选项卡未被调用，团队也会在5秒后启用 " **删除** " 按钮 `setValidityState()` 。</span><span class="sxs-lookup"><span data-stu-id="91f56-167">Teams enables the **Remove** button after 5 seconds, even if your tab hasn't called `setValidityState()`.\</span></span>
><span data-ttu-id="91f56-168">当用户选择 " **删除** 团队" 时，将在30秒后删除该选项卡，而不管您的操作是否已完成。</span><span class="sxs-lookup"><span data-stu-id="91f56-168">When the user selects **Remove** Teams removes the tab after 30 seconds regardless of whether your actions have completed.</span></span>
