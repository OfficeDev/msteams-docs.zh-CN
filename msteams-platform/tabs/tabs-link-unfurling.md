---
title: 选项卡链接展开和阶段视图
author: Rajeshwari-v
description: 如何取消链接、打开"阶段视图"，然后使用"Microsoft Teams固定选项卡。
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: b54eb5942d19749b39bb9bb504dd8645f5655ef3
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179942"
---
# <a name="tabs-link-unfurling-and-stage-view"></a><span data-ttu-id="11e5f-103">选项卡链接展开和阶段视图</span><span class="sxs-lookup"><span data-stu-id="11e5f-103">Tabs link unfurling and Stage View</span></span>

> [!NOTE]
> <span data-ttu-id="11e5f-104">此功能仅在公共 [开发人员预览版中](../resources/dev-preview/developer-preview-intro.md) 可用。</span><span class="sxs-lookup"><span data-stu-id="11e5f-104">This feature is available in [public developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="11e5f-105">阶段视图是 UI (组件) 用户界面，允许你呈现在 Teams 中全屏打开并固定为选项卡的内容。</span><span class="sxs-lookup"><span data-stu-id="11e5f-105">Stage View is a new user interface (UI) component, which allows you to render the content that is opened in full screen in Teams and pinned as a tab.</span></span>
 
> [!NOTE]
> <span data-ttu-id="11e5f-106">目前，Teams客户端不支持选项卡链接取消展开和阶段视图。</span><span class="sxs-lookup"><span data-stu-id="11e5f-106">Currently, Teams mobile clients do no support tabs link unfurling and Stage View.</span></span> <span data-ttu-id="11e5f-107">移动客户端使用开发人员提供的 属性在设备的 Web 浏览器中 `websiteUrl` 打开页面。</span><span class="sxs-lookup"><span data-stu-id="11e5f-107">Mobile clients use the `websiteUrl` attribute provided by the developer to open the page in the device's web browser.</span></span>

## <a name="stage-view"></a><span data-ttu-id="11e5f-108">阶段视图</span><span class="sxs-lookup"><span data-stu-id="11e5f-108">Stage View</span></span>

<span data-ttu-id="11e5f-109">阶段视图是一个全屏 UI 组件，你可以调用它来显示 Web 内容。</span><span class="sxs-lookup"><span data-stu-id="11e5f-109">Stage View is a full screen UI component that you can invoke to surface your web content.</span></span> <span data-ttu-id="11e5f-110">现有链接取消点击服务已更新，以便它可用于使用自适应卡片和聊天服务将 URL 转换为选项卡。</span><span class="sxs-lookup"><span data-stu-id="11e5f-110">The existing link unfurling service is updated so that it is used to turn URLs into a tab using an Adaptive Card and Chat Services.</span></span> <span data-ttu-id="11e5f-111">当用户在聊天或频道中发送 URL 时，该 URL 将取消展开到自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="11e5f-111">When a user sends a URL in a chat or channel, the URL is unfurled to an Adaptive Card.</span></span> <span data-ttu-id="11e5f-112">用户可以 **选择卡片中的** "查看"，并直接从"阶段视图"将内容固定为选项卡。</span><span class="sxs-lookup"><span data-stu-id="11e5f-112">The user can select **View** in the card, and pin the content as a tab directly from Stage View.</span></span>

## <a name="advantage-of-stage-view"></a><span data-ttu-id="11e5f-113">阶段视图的优点</span><span class="sxs-lookup"><span data-stu-id="11e5f-113">Advantage of Stage View</span></span>

<span data-ttu-id="11e5f-114">阶段视图有助于提供在网站中查看内容的Teams。</span><span class="sxs-lookup"><span data-stu-id="11e5f-114">Stage View helps provide a more seamless experience of viewing content in Teams.</span></span> <span data-ttu-id="11e5f-115">用户无需离开上下文即可打开和查看应用提供的内容，并且可以将内容固定到聊天或频道，以便将来快速访问。</span><span class="sxs-lookup"><span data-stu-id="11e5f-115">Users can open and view the content provided by your app without leaving the context, and they can pin the content to the chat or channel for future quick access.</span></span> <span data-ttu-id="11e5f-116">这可提高用户对你的应用的参与度。</span><span class="sxs-lookup"><span data-stu-id="11e5f-116">This leads to a higher user engagement with your app.</span></span>

## <a name="stage-view-vs-task-module"></a><span data-ttu-id="11e5f-117">阶段视图与任务模块</span><span class="sxs-lookup"><span data-stu-id="11e5f-117">Stage View vs. Task module</span></span>

|<span data-ttu-id="11e5f-118">阶段视图</span><span class="sxs-lookup"><span data-stu-id="11e5f-118">Stage View</span></span>|<span data-ttu-id="11e5f-119">任务模块</span><span class="sxs-lookup"><span data-stu-id="11e5f-119">Task module</span></span>|
|:-----------|:-----------|
|<span data-ttu-id="11e5f-120">当您具有要向用户显示的丰富内容（如页面、仪表板、文件等）时，阶段视图非常有用。</span><span class="sxs-lookup"><span data-stu-id="11e5f-120">Stage View is useful when you have rich content to display to the users, such as a page, a dashboard, a file, and so on.</span></span> <span data-ttu-id="11e5f-121">它提供了丰富的功能，可帮助在全屏画布中呈现内容。</span><span class="sxs-lookup"><span data-stu-id="11e5f-121">It provides  rich features that helps to render your content in the full-screen canvas.</span></span>|<span data-ttu-id="11e5f-122">[任务模块](../task-modules-and-cards/task-modules/task-modules-tabs.md) 对于显示需要用户注意的消息或收集移动到下一步所需信息特别有用。</span><span class="sxs-lookup"><span data-stu-id="11e5f-122">[Task module](../task-modules-and-cards/task-modules/task-modules-tabs.md) is especially useful to display messages that require user attention, or collect information required to move to the next step.</span></span>|
  
## <a name="invoke-stage-view"></a><span data-ttu-id="11e5f-123">调用阶段视图</span><span class="sxs-lookup"><span data-stu-id="11e5f-123">Invoke Stage View</span></span>

<span data-ttu-id="11e5f-124">可以通过以下方法调用阶段视图：</span><span class="sxs-lookup"><span data-stu-id="11e5f-124">You can invoke Stage View in the following  ways:</span></span>

* [<span data-ttu-id="11e5f-125">从自适应卡片调用阶段视图</span><span class="sxs-lookup"><span data-stu-id="11e5f-125">Invoke Stage View from Adaptive Card</span></span>](#invoke-stage-view-from-adaptive-card)
* [<span data-ttu-id="11e5f-126">通过深层链接调用阶段视图</span><span class="sxs-lookup"><span data-stu-id="11e5f-126">Invoke Stage View through deep link</span></span>](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a><span data-ttu-id="11e5f-127">从自适应卡片调用阶段视图</span><span class="sxs-lookup"><span data-stu-id="11e5f-127">Invoke Stage View from Adaptive Card</span></span>

<span data-ttu-id="11e5f-128">当用户在桌面客户端上Teams URL 时，将调用自动程序并返回自适应卡片，并可选择在[](../task-modules-and-cards/cards/cards-actions.md)阶段中打开 URL。</span><span class="sxs-lookup"><span data-stu-id="11e5f-128">When the user enters a URL on the Teams desktop client, the bot is invoked and returns an [Adaptive Card](../task-modules-and-cards/cards/cards-actions.md) with the option to open the URL in a stage.</span></span> <span data-ttu-id="11e5f-129">启动阶段并提供了 后，你可以 `tabInfo` 添加将阶段固定为选项卡的能力。</span><span class="sxs-lookup"><span data-stu-id="11e5f-129">After a stage is launched and the `tabInfo` is provided, you can add the ability to pin the stage as a tab.</span></span>  

<span data-ttu-id="11e5f-130">下图显示从自适应卡片打开的阶段：</span><span class="sxs-lookup"><span data-stu-id="11e5f-130">The following images display a stage opened from an Adaptive Card:</span></span>

<img src="~/assets/images/tab-images/open-stage-from-adaptive-card1.png" alt="Open a stage from Adaptive Card" width="700"/>

<img src="~/assets/images/tab-images/open-stage-from-adaptive-card2.png" alt="Open a stage" width="700"/>

### <a name="example"></a><span data-ttu-id="11e5f-131">示例</span><span class="sxs-lookup"><span data-stu-id="11e5f-131">Example</span></span>

<span data-ttu-id="11e5f-132">下面是从自适应卡片打开阶段的代码：</span><span class="sxs-lookup"><span data-stu-id="11e5f-132">Following is the code to open a stage from an Adaptive Card:</span></span>

```json
{
    type: "Action.Submit",
    name: "View",
    data: {
          msteams: {
            type: "invoke",
            value: {
                type: "tab/tabInfoAction",
                tabInfo: {
                    contentUrl: contentUrl,
                    websiteUrl: websiteUrl,
                    name: "Tasks",
                    entityId: "entityId"
                 }
                }
            }
        }
} 
```

<span data-ttu-id="11e5f-133">请求 `invoke` 类型必须为 `composeExtension/queryLink` 。</span><span class="sxs-lookup"><span data-stu-id="11e5f-133">The `invoke` request type must be `composeExtension/queryLink`.</span></span>

> [!NOTE]
> * <span data-ttu-id="11e5f-134">`invoke` 工作流类似于当前 `appLinking` 工作流。</span><span class="sxs-lookup"><span data-stu-id="11e5f-134">`invoke` workflow is similar to the current `appLinking` workflow.</span></span> 
> * <span data-ttu-id="11e5f-135">为了保持一致性，建议将 名称 `Action.Submit` 为 `View` 。</span><span class="sxs-lookup"><span data-stu-id="11e5f-135">To maintain consistency, it is recommended to name `Action.Submit` as `View`.</span></span>
> * <span data-ttu-id="11e5f-136">`websiteUrl` 是对象中传递的必需 `TabInfo` 属性。</span><span class="sxs-lookup"><span data-stu-id="11e5f-136">`websiteUrl` is a required property to be passed in the `TabInfo` object.</span></span>

<span data-ttu-id="11e5f-137">以下是调用阶段视图的过程：</span><span class="sxs-lookup"><span data-stu-id="11e5f-137">Following is the process to invoke Stage View:</span></span>

* <span data-ttu-id="11e5f-138">当用户选择"查看 **"时**，机器人会收到 `invoke` 一个请求。</span><span class="sxs-lookup"><span data-stu-id="11e5f-138">When the user selects **View**, the bot receives an `invoke` request.</span></span> <span data-ttu-id="11e5f-139">请求类型为 `composeExtension/queryLink` 。</span><span class="sxs-lookup"><span data-stu-id="11e5f-139">The request type is `composeExtension/queryLink`.</span></span>
* <span data-ttu-id="11e5f-140">`invoke` 来自自动程序的响应包含包含类型为的 `tab/tabInfoAction` 自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="11e5f-140">`invoke` response from bot contains an Adaptive Card with type `tab/tabInfoAction` in it.</span></span>
* <span data-ttu-id="11e5f-141">机器人使用代码 `200` 进行响应。</span><span class="sxs-lookup"><span data-stu-id="11e5f-141">The bot responds with a `200` code.</span></span>

> [!NOTE]
> <span data-ttu-id="11e5f-142">目前，Teams客户端不支持阶段视图功能。</span><span class="sxs-lookup"><span data-stu-id="11e5f-142">Currently, Teams mobile clients do not support the Stage View capability.</span></span> <span data-ttu-id="11e5f-143">当用户在移动 **客户端上** 选择"查看"时，用户会访问设备的浏览器。</span><span class="sxs-lookup"><span data-stu-id="11e5f-143">When a user selects **View** on a mobile client, the user is taken to the device's browser.</span></span> <span data-ttu-id="11e5f-144">浏览器打开在 对象的 参数 `websiteUrl` 中指定的 `TabInfo` URL。</span><span class="sxs-lookup"><span data-stu-id="11e5f-144">The browser opens the URL specified in the `websiteUrl` parameter of the `TabInfo` object.</span></span>

## <a name="invoke-stage-view-through-deep-link"></a><span data-ttu-id="11e5f-145">通过深层链接调用阶段视图</span><span class="sxs-lookup"><span data-stu-id="11e5f-145">Invoke Stage View through deep link</span></span>

<span data-ttu-id="11e5f-146">若要通过选项卡中的深层链接调用阶段视图，必须在 API 中包装深层链接 `microsoftTeams.executeDeeplink(url)` URL。</span><span class="sxs-lookup"><span data-stu-id="11e5f-146">To invoke the Stage View through deep link from your tab, you must wrap the deep link URL in the `microsoftTeams.executeDeeplink(url)` API.</span></span> <span data-ttu-id="11e5f-147">深度链接也可通过卡片 `OpenURL` 中的操作传递。</span><span class="sxs-lookup"><span data-stu-id="11e5f-147">The deep link can also be passed through an `OpenURL` action in the card.</span></span>

<span data-ttu-id="11e5f-148">下图显示了通过深层链接调用的阶段视图：</span><span class="sxs-lookup"><span data-stu-id="11e5f-148">The following image displays a Stage View invoked through a deep link:</span></span>

<img src="~/assets/images/tab-images/invoke-stage-view-through-deep-link.png" alt="Invoke a Stage View through a deep link" width="400"/>

### <a name="syntax"></a><span data-ttu-id="11e5f-149">语法</span><span class="sxs-lookup"><span data-stu-id="11e5f-149">Syntax</span></span>

<span data-ttu-id="11e5f-150">以下是 deeplink 语法：</span><span class="sxs-lookup"><span data-stu-id="11e5f-150">Following is the deeplink syntax:</span></span>  
 
<span data-ttu-id="11e5f-151"> https://teams.microsoft.com/l/stage/{appId}/0?context={"contentUrl"："[contentUrl]"，"websiteUrl"："[websiteUrl]"，"name"："[name]"}</span><span class="sxs-lookup"><span data-stu-id="11e5f-151">https://teams.microsoft.com/l/stage/{appId}/0?context={“contentUrl”:”[contentUrl]”,“websiteUrl”:”[websiteUrl]”,“name”:”[name]”}</span></span>

### <a name="examples"></a><span data-ttu-id="11e5f-152">示例</span><span class="sxs-lookup"><span data-stu-id="11e5f-152">Examples</span></span>

<span data-ttu-id="11e5f-153">当用户输入 URL 时，该 URL 将取消展开到自适应卡片中。</span><span class="sxs-lookup"><span data-stu-id="11e5f-153">When a user enters a URL, it is unfurled into an Adaptive card.</span></span>

<span data-ttu-id="11e5f-154">以下是调用阶段视图的深层链接示例：</span><span class="sxs-lookup"><span data-stu-id="11e5f-154">Following are the deep link examples to invoke Stage View:</span></span>

<span data-ttu-id="11e5f-155">**示例 1**</span><span class="sxs-lookup"><span data-stu-id="11e5f-155">**Example 1**</span></span>

<span data-ttu-id="11e5f-156"> https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={"contentUrl"："https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx"，"websiteUrl"："https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx"，"name"："Contoso"}</span><span class="sxs-lookup"><span data-stu-id="11e5f-156">https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={“contentUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“websiteUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“name”:”Contoso”}</span></span>

<span data-ttu-id="11e5f-157">**示例 2**</span><span class="sxs-lookup"><span data-stu-id="11e5f-157">**Example 2**</span></span>

<span data-ttu-id="11e5f-158"> https://teams.microsoft.com/l/Meeting_Stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={"contentUrl"："https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx"，"websiteUrl"："https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx"，"name"："Contoso"}</span><span class="sxs-lookup"><span data-stu-id="11e5f-158">https://teams.microsoft.com/l/Meeting_Stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={“contentUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“websiteUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“name”:”Contoso”}</span></span>

> [!NOTE]
> * <span data-ttu-id="11e5f-159">在 `name` 深层链接中是可选的。</span><span class="sxs-lookup"><span data-stu-id="11e5f-159">The `name` is optional in deep link.</span></span> <span data-ttu-id="11e5f-160">如果未包含，则应用名称将替换它。</span><span class="sxs-lookup"><span data-stu-id="11e5f-160">If not included, the app name replaces it.</span></span>
> * <span data-ttu-id="11e5f-161">深度链接也可通过操作 `OpenURL` 传递。</span><span class="sxs-lookup"><span data-stu-id="11e5f-161">The deep link can also be passed through an `OpenURL` action.</span></span>
> * <span data-ttu-id="11e5f-162">目前，Teams客户端不支持阶段视图功能。</span><span class="sxs-lookup"><span data-stu-id="11e5f-162">Currently, Teams mobile clients do not support the Stage View capability.</span></span> <span data-ttu-id="11e5f-163">当用户选择到阶段视图的深层链接时，他们会进入其设备的 Web 浏览器。</span><span class="sxs-lookup"><span data-stu-id="11e5f-163">When users select a deep link to a Stage View, they are taken to their device's web browser.</span></span> <span data-ttu-id="11e5f-164">Web 浏览器将打开深层链接的 `websiteUrl` 参数中指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="11e5f-164">The web browser opens the URL specified in the `websiteUrl` parameter of the deep link.</span></span>
> * <span data-ttu-id="11e5f-165">当你从特定上下文启动阶段时，请确保你的应用在该上下文中工作。</span><span class="sxs-lookup"><span data-stu-id="11e5f-165">When you launch a Stage from a certain context, ensure that your app works in that context.</span></span> <span data-ttu-id="11e5f-166">例如，如果你的阶段视图从个人应用启动，则必须确保你的应用具有个人作用域。</span><span class="sxs-lookup"><span data-stu-id="11e5f-166">For example, if your Stage View is launched from a personal app, you must ensure your app has a personal scope.</span></span>

## <a name="tab-information-property"></a><span data-ttu-id="11e5f-167">选项卡信息属性</span><span class="sxs-lookup"><span data-stu-id="11e5f-167">Tab information property</span></span>

| <span data-ttu-id="11e5f-168">属性名称</span><span class="sxs-lookup"><span data-stu-id="11e5f-168">Property name</span></span> | <span data-ttu-id="11e5f-169">类型</span><span class="sxs-lookup"><span data-stu-id="11e5f-169">Type</span></span> | <span data-ttu-id="11e5f-170">字符数</span><span class="sxs-lookup"><span data-stu-id="11e5f-170">Number of characters</span></span> | <span data-ttu-id="11e5f-171">说明</span><span class="sxs-lookup"><span data-stu-id="11e5f-171">Description</span></span> |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | <span data-ttu-id="11e5f-172">String</span><span class="sxs-lookup"><span data-stu-id="11e5f-172">String</span></span> | <span data-ttu-id="11e5f-173">64</span><span class="sxs-lookup"><span data-stu-id="11e5f-173">64</span></span> | <span data-ttu-id="11e5f-174">此属性是选项卡显示的实体的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="11e5f-174">This property is a  unique identifier for the entity that the tab displays.</span></span> <span data-ttu-id="11e5f-175">这是必填字段。</span><span class="sxs-lookup"><span data-stu-id="11e5f-175">This is a required field.</span></span>|
| `name` | <span data-ttu-id="11e5f-176">String</span><span class="sxs-lookup"><span data-stu-id="11e5f-176">String</span></span> | <span data-ttu-id="11e5f-177">128</span><span class="sxs-lookup"><span data-stu-id="11e5f-177">128</span></span> | <span data-ttu-id="11e5f-178">此属性是显示名称界面中选项卡的控件。</span><span class="sxs-lookup"><span data-stu-id="11e5f-178">This property is the display name of the tab in the channel interface.</span></span> <span data-ttu-id="11e5f-179">这是一个可选字段。</span><span class="sxs-lookup"><span data-stu-id="11e5f-179">This is an optional field.</span></span>|
| `contentUrl` | <span data-ttu-id="11e5f-180">String</span><span class="sxs-lookup"><span data-stu-id="11e5f-180">String</span></span> | <span data-ttu-id="11e5f-181">2048</span><span class="sxs-lookup"><span data-stu-id="11e5f-181">2048</span></span> | <span data-ttu-id="11e5f-182">此属性是指向要 https:// 画布中的实体 UI 的 Teams URL。</span><span class="sxs-lookup"><span data-stu-id="11e5f-182">This property is the https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span> <span data-ttu-id="11e5f-183">这是必填字段。</span><span class="sxs-lookup"><span data-stu-id="11e5f-183">This is a required field.</span></span>|
| `websiteUrl?` | <span data-ttu-id="11e5f-184">String</span><span class="sxs-lookup"><span data-stu-id="11e5f-184">String</span></span> | <span data-ttu-id="11e5f-185">2048</span><span class="sxs-lookup"><span data-stu-id="11e5f-185">2048</span></span> | <span data-ttu-id="11e5f-186">如果用户选择在 https:// 查看，则此属性是指向的 URL。</span><span class="sxs-lookup"><span data-stu-id="11e5f-186">This property is the https:// URL to point at, if a user selects to view in a browser.</span></span> <span data-ttu-id="11e5f-187">这是必填字段。</span><span class="sxs-lookup"><span data-stu-id="11e5f-187">This is a required field.</span></span>|
| `removeUrl?` | <span data-ttu-id="11e5f-188">String</span><span class="sxs-lookup"><span data-stu-id="11e5f-188">String</span></span> | <span data-ttu-id="11e5f-189">2048</span><span class="sxs-lookup"><span data-stu-id="11e5f-189">2048</span></span> | <span data-ttu-id="11e5f-190">此属性是 https:// 选项卡时要显示的 UI 的 URL。这是一个可选字段。</span><span class="sxs-lookup"><span data-stu-id="11e5f-190">This property is the https:// URL that points to the UI to be displayed when the user deletes the tab. This is an optional field.</span></span>|

## <a name="see-also"></a><span data-ttu-id="11e5f-191">另请参阅</span><span class="sxs-lookup"><span data-stu-id="11e5f-191">See also</span></span>

* [<span data-ttu-id="11e5f-192">取消展开消息传递扩展链接</span><span class="sxs-lookup"><span data-stu-id="11e5f-192">Messaging extensions link unfurling</span></span>](~/messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="11e5f-193">Teams选项卡</span><span class="sxs-lookup"><span data-stu-id="11e5f-193">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="11e5f-194">创建个人选项卡</span><span class="sxs-lookup"><span data-stu-id="11e5f-194">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="11e5f-195">创建频道或组选项卡</span><span class="sxs-lookup"><span data-stu-id="11e5f-195">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)

## <a name="next-step"></a><span data-ttu-id="11e5f-196">后续步骤</span><span class="sxs-lookup"><span data-stu-id="11e5f-196">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="11e5f-197">创建对话选项卡</span><span class="sxs-lookup"><span data-stu-id="11e5f-197">Create conversational tabs</span></span>](~/tabs/how-to/conversational-tabs.md)