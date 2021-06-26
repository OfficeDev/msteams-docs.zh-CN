---
title: 创建选项卡删除页
author: surbhigupta
description: 如何创建选项卡删除页
keywords: teams 选项卡组频道可配置删除删除
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 1b4ef5435ad1be82726edbf02d7205c0b1feba06
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140192"
---
# <a name="create-a-removal-page"></a><span data-ttu-id="750a3-104">创建删除页面</span><span class="sxs-lookup"><span data-stu-id="750a3-104">Create a removal page</span></span>

<span data-ttu-id="750a3-105">可以通过在应用中支持删除和修改选项来扩展和增强用户体验。</span><span class="sxs-lookup"><span data-stu-id="750a3-105">You can extend and enhance the user experience by supporting removal and modification options in your app.</span></span> <span data-ttu-id="750a3-106">Teams用户可以重命名或删除频道或组选项卡，并且你可以允许用户在安装后重新配置选项卡。</span><span class="sxs-lookup"><span data-stu-id="750a3-106">Teams enables users to rename or remove a channel or group tab and you can permit users to reconfigure your tab after installation.</span></span> <span data-ttu-id="750a3-107">此外，选项卡删除体验为用户提供删除后选项，以删除或存档内容。</span><span class="sxs-lookup"><span data-stu-id="750a3-107">Additionally, the tab removal experience provides the users with post-removal options to delete or archive content.</span></span>

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a><span data-ttu-id="750a3-108">启用选项卡以在安装后重新配置</span><span class="sxs-lookup"><span data-stu-id="750a3-108">Enable your tab to be reconfigured after installation</span></span>

<span data-ttu-id="750a3-109">你的 **manifest.js** 定义选项卡的特性和功能。</span><span class="sxs-lookup"><span data-stu-id="750a3-109">Your **manifest.json** defines your tab's features and capabilities.</span></span> <span data-ttu-id="750a3-110">选项卡实例属性采用一个布尔值，该值指示用户是否可以在选项卡创建后修改或 `canUpdateConfiguration` 重新配置它。</span><span class="sxs-lookup"><span data-stu-id="750a3-110">The tab instance `canUpdateConfiguration` property takes a Boolean value that indicates whether a user can modify or reconfigure the tab after it is created.</span></span> <span data-ttu-id="750a3-111">下表提供了属性详细信息：</span><span class="sxs-lookup"><span data-stu-id="750a3-111">The following table provides the property details:</span></span>

|<span data-ttu-id="750a3-112">名称</span><span class="sxs-lookup"><span data-stu-id="750a3-112">Name</span></span>| <span data-ttu-id="750a3-113">类型</span><span class="sxs-lookup"><span data-stu-id="750a3-113">Type</span></span>| <span data-ttu-id="750a3-114">最大大小</span><span class="sxs-lookup"><span data-stu-id="750a3-114">Maximum size</span></span> | <span data-ttu-id="750a3-115">必需</span><span class="sxs-lookup"><span data-stu-id="750a3-115">Required</span></span> | <span data-ttu-id="750a3-116">说明</span><span class="sxs-lookup"><span data-stu-id="750a3-116">Description</span></span>|
|---|---|---|---|---|
|`canUpdateConfiguration`|<span data-ttu-id="750a3-117">Boolean</span><span class="sxs-lookup"><span data-stu-id="750a3-117">Boolean</span></span>|||<span data-ttu-id="750a3-118">一个值，指示用户创建后是否可以更新选项卡配置的实例。</span><span class="sxs-lookup"><span data-stu-id="750a3-118">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="750a3-119">默认值为“`true`”。</span><span class="sxs-lookup"><span data-stu-id="750a3-119">Default is `true`.</span></span> |

<span data-ttu-id="750a3-120">将选项卡上载到频道或群聊时，Teams为选项卡添加右键单击下拉菜单。可用选项由设置 `canUpdateConfiguration` 确定。</span><span class="sxs-lookup"><span data-stu-id="750a3-120">When your tab is uploaded to a channel or group chat, Teams adds a right-click drop-down menu for your tab. The available options are determined by the `canUpdateConfiguration` setting.</span></span> <span data-ttu-id="750a3-121">下表提供了设置详细信息：</span><span class="sxs-lookup"><span data-stu-id="750a3-121">The following table provides the setting details:</span></span>

| `canUpdateConfiguration`| <span data-ttu-id="750a3-122">true</span><span class="sxs-lookup"><span data-stu-id="750a3-122">true</span></span>   | <span data-ttu-id="750a3-123">false</span><span class="sxs-lookup"><span data-stu-id="750a3-123">false</span></span> | <span data-ttu-id="750a3-124">说明</span><span class="sxs-lookup"><span data-stu-id="750a3-124">description</span></span> |
| ----------------------- | :----: | ----- | ----------- |
|     <span data-ttu-id="750a3-125">设置</span><span class="sxs-lookup"><span data-stu-id="750a3-125">Settings</span></span>            |   <span data-ttu-id="750a3-126">√</span><span class="sxs-lookup"><span data-stu-id="750a3-126">√</span></span>    |       |<span data-ttu-id="750a3-127">页面 `configurationUrl` 在 IFrame 中重新加载，允许用户重新配置选项卡。</span><span class="sxs-lookup"><span data-stu-id="750a3-127">The `configurationUrl` page is reloaded in an IFrame allowing the user to reconfigure the tab.</span></span> |
|     <span data-ttu-id="750a3-128">重命名</span><span class="sxs-lookup"><span data-stu-id="750a3-128">Rename</span></span>              |   <span data-ttu-id="750a3-129">√</span><span class="sxs-lookup"><span data-stu-id="750a3-129">√</span></span>    |   <span data-ttu-id="750a3-130">√</span><span class="sxs-lookup"><span data-stu-id="750a3-130">√</span></span>   | <span data-ttu-id="750a3-131">用户可以更改选项卡名称，因为它显示在选项卡栏中。</span><span class="sxs-lookup"><span data-stu-id="750a3-131">The user can change the tab name as it appears in the tab bar.</span></span>          |
|     <span data-ttu-id="750a3-132">删除</span><span class="sxs-lookup"><span data-stu-id="750a3-132">Remove</span></span>              |   <span data-ttu-id="750a3-133">√</span><span class="sxs-lookup"><span data-stu-id="750a3-133">√</span></span>    |   <span data-ttu-id="750a3-134">√</span><span class="sxs-lookup"><span data-stu-id="750a3-134">√</span></span>   |  <span data-ttu-id="750a3-135">如果  `removeURL` 属性和值包含在配置 **页中，** 则删除 **页面** 将加载到 IFrame 中，并呈现给用户。</span><span class="sxs-lookup"><span data-stu-id="750a3-135">If the  `removeURL` property and value are included in the **configuration page**, the **removal page** is loaded into an IFrame and presented to the user.</span></span> <span data-ttu-id="750a3-136">如果未包含删除页，则向用户显示一个确认对话框。</span><span class="sxs-lookup"><span data-stu-id="750a3-136">If a removal page is not included, the user is presented with a confirm dialog box.</span></span>          |

## <a name="create-a-tab-removal-page-for-your-application"></a><span data-ttu-id="750a3-137">为应用程序创建选项卡删除页</span><span class="sxs-lookup"><span data-stu-id="750a3-137">Create a tab removal page for your application</span></span>

<span data-ttu-id="750a3-138">可选删除页是一个您托管的 HTML 页，在删除选项卡时将显示该页。</span><span class="sxs-lookup"><span data-stu-id="750a3-138">The optional removal page is an HTML page that you host and is displayed when the tab is removed.</span></span> <span data-ttu-id="750a3-139">删除页面 URL 由配置页 `setSettings()` 中的 方法指定。</span><span class="sxs-lookup"><span data-stu-id="750a3-139">The removal page URL is designated by the `setSettings()` method within your configuration page.</span></span> <span data-ttu-id="750a3-140">与应用内的所有页面一样，删除页面必须符合Teams[先决条件](../../../tabs/how-to/tab-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="750a3-140">As with all pages in your app, the removal page must comply with [Teams tab prerequisites](../../../tabs/how-to/tab-requirements.md).</span></span>

### <a name="register-a-remove-handler"></a><span data-ttu-id="750a3-141">注册删除处理程序</span><span class="sxs-lookup"><span data-stu-id="750a3-141">Register a remove handler</span></span>

<span data-ttu-id="750a3-142">（可选）在删除页面逻辑中，您可以在用户删除现有选项卡配置时 `registerOnRemoveHandler((RemoveEvent) => {}` 调用事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="750a3-142">Optionally, within your removal page logic, you can  invoke the `registerOnRemoveHandler((RemoveEvent) => {}` event handler when the user removes an existing tab configuration.</span></span> <span data-ttu-id="750a3-143">当用户尝试删除内容时，该方法将接受 接口并执行 [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) 处理程序中的代码。</span><span class="sxs-lookup"><span data-stu-id="750a3-143">The method takes in the [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) interface and executes the code in the handler when a user attempts to remove content.</span></span> <span data-ttu-id="750a3-144">方法用于执行清理操作，例如删除支持选项卡内容的基础资源。</span><span class="sxs-lookup"><span data-stu-id="750a3-144">The method is used to perform cleanup operations such as removing the underlying resource powering the tab content.</span></span> <span data-ttu-id="750a3-145">一次只能注册一个删除处理程序。</span><span class="sxs-lookup"><span data-stu-id="750a3-145">At a time only one remove handler can be registered.</span></span>

<span data-ttu-id="750a3-146">该 `RemoveEvent` 接口使用两种方法描述对象：</span><span class="sxs-lookup"><span data-stu-id="750a3-146">The `RemoveEvent` interface describes an object with two methods:</span></span>

* <span data-ttu-id="750a3-147">`notifySuccess()`此函数是必需的。</span><span class="sxs-lookup"><span data-stu-id="750a3-147">The `notifySuccess()` function is required.</span></span> <span data-ttu-id="750a3-148">它表示已成功删除基础资源，并且可删除其内容。</span><span class="sxs-lookup"><span data-stu-id="750a3-148">It indicates that the removal of the underlying resource succeeded and its content can be removed.</span></span>

* <span data-ttu-id="750a3-149">函数 `notifyFailure(string)` 是可选的。</span><span class="sxs-lookup"><span data-stu-id="750a3-149">The `notifyFailure(string)` function is optional.</span></span> <span data-ttu-id="750a3-150">它指示删除基础资源失败，并且无法删除其内容。</span><span class="sxs-lookup"><span data-stu-id="750a3-150">It indicates that removal of the underlying resource failed and its content cannot be removed.</span></span> <span data-ttu-id="750a3-151">可选字符串参数指定失败的原因。</span><span class="sxs-lookup"><span data-stu-id="750a3-151">The optional string parameter specifies a reason for the failure.</span></span> <span data-ttu-id="750a3-152">如果提供，则向用户显示此字符串;否则将显示一个常规错误。</span><span class="sxs-lookup"><span data-stu-id="750a3-152">If provided, this string is displayed to the user; else a generic error is displayed.</span></span>

#### <a name="use-the-getsettings-function"></a><span data-ttu-id="750a3-153">使用 `getSettings()` 函数</span><span class="sxs-lookup"><span data-stu-id="750a3-153">Use the `getSettings()` function</span></span>

<span data-ttu-id="750a3-154">可以使用 分配 `getSettings()` 要删除的选项卡内容。</span><span class="sxs-lookup"><span data-stu-id="750a3-154">You can use `getSettings()`to assign the tab content to be removed.</span></span> <span data-ttu-id="750a3-155">`getSettings((Settings) =>{})`函数接受 [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) 并提供可以检索的有效 settings 属性值。</span><span class="sxs-lookup"><span data-stu-id="750a3-155">The `getSettings((Settings) =>{})` function takes in the [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) and provides the valid settings property values that can be retrieved.</span></span>

#### <a name="use-the-getcontext-function"></a><span data-ttu-id="750a3-156">使用 `getContext()` 函数</span><span class="sxs-lookup"><span data-stu-id="750a3-156">Use the `getContext()` function</span></span>

<span data-ttu-id="750a3-157">可以使用 `getContext()` 获取正在运行帧的当前上下文。</span><span class="sxs-lookup"><span data-stu-id="750a3-157">You can use `getContext()` to get the current context in which the frame is running.</span></span> <span data-ttu-id="750a3-158">`getContext((Context) =>{})`函数接受 [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) 。</span><span class="sxs-lookup"><span data-stu-id="750a3-158">The `getContext((Context) =>{})` function takes in the [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="750a3-159">函数提供可在删除页面逻辑中用于确定要显示在删除 `Context` 页中的内容的有效属性值。</span><span class="sxs-lookup"><span data-stu-id="750a3-159">The function provides valid `Context` property values that you can use in your removal page logic to determine the content to display in the removal page.</span></span>

#### <a name="include-authentication"></a><span data-ttu-id="750a3-160">包括身份验证</span><span class="sxs-lookup"><span data-stu-id="750a3-160">Include authentication</span></span>

<span data-ttu-id="750a3-161">在允许用户删除选项卡内容之前，需要进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="750a3-161">Authentication is required before allowing a user to delete the tab content.</span></span> <span data-ttu-id="750a3-162">上下文信息可用于帮助构建身份验证请求和授权页面 URL。</span><span class="sxs-lookup"><span data-stu-id="750a3-162">Context information can be used to help construct authentication requests and authorization page URLs.</span></span> <span data-ttu-id="750a3-163">请参阅[Microsoft Teams的身份验证流](~/tabs/how-to/authentication/auth-flow-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="750a3-163">See [Microsoft Teams authentication flow for tabs](~/tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="750a3-164">确保选项卡页中使用的所有域都列在 `manifest.json` `validDomains` 数组中。</span><span class="sxs-lookup"><span data-stu-id="750a3-164">Make sure that all domains used in your tab pages are listed in the `manifest.json` `validDomains` array.</span></span>

<span data-ttu-id="750a3-165">下面是一个示例选项卡删除代码块：</span><span class="sxs-lookup"><span data-stu-id="750a3-165">The following is a sample tab removal code block:</span></span>

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

<span data-ttu-id="750a3-166">当用户从选项卡的下拉菜单中选择"删除"时，Teams将配置页中分配的可选页面加载 `removeUrl` 至 IFrame 中。</span><span class="sxs-lookup"><span data-stu-id="750a3-166">When a user selects **Remove** from the tab's drop-down menu, Teams loads the optional `removeUrl` page assigned in your **configuration page**, into an IFrame.</span></span> <span data-ttu-id="750a3-167">向用户显示一个使用 函数加载的按钮，该按钮调用并启用删除页面 IFrame 底部显示的 `onClick()` `microsoftTeams.settings.setValidityState(true)` "删除"按钮。 </span><span class="sxs-lookup"><span data-stu-id="750a3-167">The user is shown a button loaded with the `onClick()` function that calls `microsoftTeams.settings.setValidityState(true)` and enables the **Remove** button shown at the bottom of the removal page IFrame.</span></span>

<span data-ttu-id="750a3-168">执行删除处理程序后， `removeEvent.notifySuccess()` 或 `removeEvent.notifyFailure()` 通知Teams删除结果。</span><span class="sxs-lookup"><span data-stu-id="750a3-168">After the remove handler is executed, `removeEvent.notifySuccess()` or `removeEvent.notifyFailure()` notifies Teams of the content removal outcome.</span></span>

>[!NOTE]
> * <span data-ttu-id="750a3-169">为了确保授权用户对选项卡的控制不会受到约束，Teams成功和失败情况下删除选项卡。</span><span class="sxs-lookup"><span data-stu-id="750a3-169">To ensure that an authorized user's control over a tab is not inhibited, Teams removes the tab in both success and failure cases.</span></span>
> * <span data-ttu-id="750a3-170">Teams五秒后启用 **"删除**"按钮，即使选项卡尚未调用 `setValidityState()` 。</span><span class="sxs-lookup"><span data-stu-id="750a3-170">Teams enables the **Remove** button after five seconds, even if your tab has not called `setValidityState()`.</span></span>
> * <span data-ttu-id="750a3-171">当用户选择删除 **时**，Teams 30 秒后删除选项卡，无论操作是否已完成。</span><span class="sxs-lookup"><span data-stu-id="750a3-171">When the user selects **Remove**, Teams removes the tab after 30 seconds regardless of whether the actions have been completed or not.</span></span>

## <a name="see-also"></a><span data-ttu-id="750a3-172">另请参阅</span><span class="sxs-lookup"><span data-stu-id="750a3-172">See also</span></span>

* [<span data-ttu-id="750a3-173">Teams选项卡</span><span class="sxs-lookup"><span data-stu-id="750a3-173">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="750a3-174">先决条件</span><span class="sxs-lookup"><span data-stu-id="750a3-174">Prerequisites</span></span>](~/tabs/how-to/tab-requirements.md)
* [<span data-ttu-id="750a3-175">创建个人选项卡</span><span class="sxs-lookup"><span data-stu-id="750a3-175">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="750a3-176">创建频道或组选项卡</span><span class="sxs-lookup"><span data-stu-id="750a3-176">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="750a3-177">创建内容页</span><span class="sxs-lookup"><span data-stu-id="750a3-177">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
* [<span data-ttu-id="750a3-178">创建配置页</span><span class="sxs-lookup"><span data-stu-id="750a3-178">Create a configuration page</span></span>](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [<span data-ttu-id="750a3-179">获取选项卡的上下文</span><span class="sxs-lookup"><span data-stu-id="750a3-179">Get context for your tab</span></span>](~/tabs/how-to/access-teams-context.md)
* [<span data-ttu-id="750a3-180">具有自适应卡片的生成选项卡</span><span class="sxs-lookup"><span data-stu-id="750a3-180">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)
* [<span data-ttu-id="750a3-181">选项卡链接展开和阶段视图</span><span class="sxs-lookup"><span data-stu-id="750a3-181">Tabs link unfurling and Stage View</span></span>](~/tabs/tabs-link-unfurling.md)
* [<span data-ttu-id="750a3-182">创建对话选项卡</span><span class="sxs-lookup"><span data-stu-id="750a3-182">Create conversational tabs</span></span>](~/tabs/how-to/conversational-tabs.md)
* [<span data-ttu-id="750a3-183">选项卡边距更改</span><span class="sxs-lookup"><span data-stu-id="750a3-183">Tab margin changes</span></span>](~/resources/removing-tab-margins.md)

## <a name="next-step"></a><span data-ttu-id="750a3-184">后续步骤</span><span class="sxs-lookup"><span data-stu-id="750a3-184">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="750a3-185">移动设备上的选项卡</span><span class="sxs-lookup"><span data-stu-id="750a3-185">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)