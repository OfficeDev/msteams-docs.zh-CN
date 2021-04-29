---
title: 创建“共享到 Teams”按钮
description: 如何在网站上添加"共享到 Teams"嵌入按钮
ms.topic: reference
localization_priority: Normal
keywords: 共享 Teams 共享到 Teams
ms.openlocfilehash: d3e23c50cbaa38a53fa02c19cec69061478d9a57
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075645"
---
# <a name="create-share-to-teams-button"></a><span data-ttu-id="851c5-104">创建“共享到 Teams”按钮</span><span class="sxs-lookup"><span data-stu-id="851c5-104">Create Share-to-Teams button</span></span>

<span data-ttu-id="851c5-105">第三方网站可以使用启动器脚本在其网页上嵌入 Share-to-Teams 按钮。</span><span class="sxs-lookup"><span data-stu-id="851c5-105">Third-party websites can use the launcher script to embed Share-to-Teams buttons on their webpages.</span></span> <span data-ttu-id="851c5-106">选择后，它将在弹出窗口中启动"共享到 Teams"体验。</span><span class="sxs-lookup"><span data-stu-id="851c5-106">When you select, it launches the Share-to-Teams experience in a pop-up window.</span></span> <span data-ttu-id="851c5-107">这允许你直接将链接共享给任何人或 Microsoft Teams 频道，而无需切换上下文。</span><span class="sxs-lookup"><span data-stu-id="851c5-107">This allows you to share a link directly to any person or Microsoft Teams channel without switching the context.</span></span> <span data-ttu-id="851c5-108">本文档指导你了解如何为网站创建和嵌入"共享到 Teams"按钮、制作网站预览以及扩展 Share-to-Teams 教育版。</span><span class="sxs-lookup"><span data-stu-id="851c5-108">This document guides you on how to create, and embed a Share-to-Teams button for your website, craft your website preview, and extend Share-to-Teams for Education.</span></span>

> [!NOTE]
> * <span data-ttu-id="851c5-109">仅支持桌面版 Edge 和 Chrome。</span><span class="sxs-lookup"><span data-stu-id="851c5-109">Only the desktop versions of Edge and Chrome are supported.</span></span>
> * <span data-ttu-id="851c5-110">不支持使用免费增值帐户或来宾帐户。</span><span class="sxs-lookup"><span data-stu-id="851c5-110">Use of Freemium or guest accounts is not supported.</span></span>  

<span data-ttu-id="851c5-111">下图显示了"共享到 Teams"弹出体验：</span><span class="sxs-lookup"><span data-stu-id="851c5-111">The following image displays the Share-to-Teams pop-up experience:</span></span>

!["共享到 Teams"弹出窗口](~/assets/images/share-to-teams-popup.png)

## <a name="embed-a-share-to-teams-button"></a><span data-ttu-id="851c5-113">嵌入"共享到 Teams"按钮</span><span class="sxs-lookup"><span data-stu-id="851c5-113">Embed a Share to Teams button</span></span>

1. <span data-ttu-id="851c5-114">在 `launcher.js` 网页上添加脚本。</span><span class="sxs-lookup"><span data-stu-id="851c5-114">Add the `launcher.js` script on your webpage.</span></span>

    ```html
    <script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
    ```

1. <span data-ttu-id="851c5-115">在网页上添加一个 HTML 元素，其 `teams-share-button` 类属性和要共享的属性 `data-href` 链接。</span><span class="sxs-lookup"><span data-stu-id="851c5-115">Add a HTML element on your webpage with the `teams-share-button` class attribute and the link to share in the `data-href` attribute.</span></span>

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>">
    </div>
    ```

    <span data-ttu-id="851c5-116">完成此操作后，Microsoft Teams 图标将添加到你的网站。</span><span class="sxs-lookup"><span data-stu-id="851c5-116">After completing this, the Microsoft Teams icon gets added to your website.</span></span> <span data-ttu-id="851c5-117">下图显示了"共享到 Teams"图标：</span><span class="sxs-lookup"><span data-stu-id="851c5-117">The following image shows Share-to-Teams icon:</span></span>

    ![共享到 Teams 图标](~/assets/icons/share-to-teams-icon.png)

1. <span data-ttu-id="851c5-119">或者，如果你希望"共享到 Teams"按钮具有不同的图标大小，请使用 `data-icon-px-size` 属性。</span><span class="sxs-lookup"><span data-stu-id="851c5-119">Alternatively, if you want a different icon size for the Share-to Teams button, use the `data-icon-px-size` attribute.</span></span>

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```
1. <span data-ttu-id="851c5-120">如果共享链接需要用户身份验证，并且要共享的链接中的 URL 预览在 Teams 中无法很好地呈现，则可以通过将 属性设置为 来禁用 URL `data-preview` 预览 `false` 。</span><span class="sxs-lookup"><span data-stu-id="851c5-120">If the shared link requires user authentication, and the URL preview from your link to be shared does not render well in Teams then, you can disable the URL preview by adding the `data-preview` attribute set to `false`.</span></span>

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-preview="false">
    </div>
    ```

1. <span data-ttu-id="851c5-121">如果页面动态呈现内容，可以使用 方法强制"共享"按钮在管道 `shareToMicrosoftTeams.renderButtons()` 中的适当位置呈现。</span><span class="sxs-lookup"><span data-stu-id="851c5-121">If your page dynamically renders content, you can use the the `shareToMicrosoftTeams.renderButtons()` method to force the **Share** button to render at the appropriate place in the pipeline.</span></span>

## <a name="craft-your-website-preview"></a><span data-ttu-id="851c5-122">制作网站预览</span><span class="sxs-lookup"><span data-stu-id="851c5-122">Craft your website preview</span></span>

<span data-ttu-id="851c5-123">将你的网站共享到 Teams 时，插入到所选频道的卡片包含网站的预览。</span><span class="sxs-lookup"><span data-stu-id="851c5-123">When your website is shared to Teams, the card that is inserted into the selected channel contains a preview of your website.</span></span> <span data-ttu-id="851c5-124">您可以通过确保将适当的元数据添加到要共享的网站（如 URL）来控制此预览 `data-href` 的行为。</span><span class="sxs-lookup"><span data-stu-id="851c5-124">You can control the behavior of this preview by ensuring the appropriate meta-data is added to the website being shared, such as the `data-href` URL.</span></span>  

<span data-ttu-id="851c5-125">**显示预览**</span><span class="sxs-lookup"><span data-stu-id="851c5-125">**To display the preview**</span></span>

* <span data-ttu-id="851c5-126">必须包含缩略图 **图像，或** 标题 **和说明\*\*\*\*。**</span><span class="sxs-lookup"><span data-stu-id="851c5-126">You must include either a **Thumbnail image**, or both a **Title** and **Description**.</span></span> <span data-ttu-id="851c5-127">为了获得最佳结果，请全部包含这三者。</span><span class="sxs-lookup"><span data-stu-id="851c5-127">For best results, include all three.</span></span>
* <span data-ttu-id="851c5-128">共享 URL 不需要身份验证。</span><span class="sxs-lookup"><span data-stu-id="851c5-128">The shared URL does not require authentication.</span></span> <span data-ttu-id="851c5-129">如果要求进行身份验证，可以共享它，但不创建预览。</span><span class="sxs-lookup"><span data-stu-id="851c5-129">If it requires authentication, you can share it, but the preview is not created.</span></span>

<span data-ttu-id="851c5-130">下表概述了必要的标记：</span><span class="sxs-lookup"><span data-stu-id="851c5-130">The following table outlines the necessary tags:</span></span>

|<span data-ttu-id="851c5-131">值</span><span class="sxs-lookup"><span data-stu-id="851c5-131">Value</span></span>|<span data-ttu-id="851c5-132">Meta 标记</span><span class="sxs-lookup"><span data-stu-id="851c5-132">Meta tag</span></span>| <span data-ttu-id="851c5-133">Open Graph</span><span class="sxs-lookup"><span data-stu-id="851c5-133">Open Graph</span></span>|
|----|----|----|
|<span data-ttu-id="851c5-134">标题</span><span class="sxs-lookup"><span data-stu-id="851c5-134">Title</span></span>|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|<span data-ttu-id="851c5-135">描述</span><span class="sxs-lookup"><span data-stu-id="851c5-135">Description</span></span>|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|<span data-ttu-id="851c5-136">缩略图图像</span><span class="sxs-lookup"><span data-stu-id="851c5-136">Thumbnail Image</span></span>| <span data-ttu-id="851c5-137">无。</span><span class="sxs-lookup"><span data-stu-id="851c5-137">none.</span></span> |`<meta property="og:image" content="http://example.com/image.jpg">`|

<span data-ttu-id="851c5-138">可以使用 html 默认版本或 Open Graph 版本。</span><span class="sxs-lookup"><span data-stu-id="851c5-138">You can use either the html default versions, or the Open Graph version.</span></span>

## <a name="share-to-teams-for-education"></a><span data-ttu-id="851c5-139">共享到 Teams 教育</span><span class="sxs-lookup"><span data-stu-id="851c5-139">Share to Teams for Education</span></span>

<span data-ttu-id="851c5-140">对于使用"共享到 Teams"按钮的教师，还有一个附加选项 `Create an Assignment` 。</span><span class="sxs-lookup"><span data-stu-id="851c5-140">For teachers using the Share to Teams button, there is an additional option to `Create an Assignment`.</span></span> <span data-ttu-id="851c5-141">这使您能够基于共享链接在所选团队中快速创建工作分配。</span><span class="sxs-lookup"><span data-stu-id="851c5-141">This enables you to quickly create an assignment in the chosen Team, based on the shared link.</span></span> <span data-ttu-id="851c5-142">下图显示了适用于教育的 Share-to-Teams：</span><span class="sxs-lookup"><span data-stu-id="851c5-142">The following image displays Share-to-Teams for education:</span></span> 

![共享到 Teams 弹出式教育](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a><span data-ttu-id="851c5-144">完整launcher.js定义</span><span class="sxs-lookup"><span data-stu-id="851c5-144">Full launcher.js definition</span></span>

| <span data-ttu-id="851c5-145">Property</span><span class="sxs-lookup"><span data-stu-id="851c5-145">Property</span></span> | <span data-ttu-id="851c5-146">HTML 属性</span><span class="sxs-lookup"><span data-stu-id="851c5-146">HTML attribute</span></span> | <span data-ttu-id="851c5-147">类型</span><span class="sxs-lookup"><span data-stu-id="851c5-147">Type</span></span> | <span data-ttu-id="851c5-148">默认值</span><span class="sxs-lookup"><span data-stu-id="851c5-148">Default</span></span> | <span data-ttu-id="851c5-149">说明</span><span class="sxs-lookup"><span data-stu-id="851c5-149">Description</span></span> |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| <span data-ttu-id="851c5-150">href</span><span class="sxs-lookup"><span data-stu-id="851c5-150">href</span></span> | `data-href` | <span data-ttu-id="851c5-151">string</span><span class="sxs-lookup"><span data-stu-id="851c5-151">string</span></span> | <span data-ttu-id="851c5-152">不适用</span><span class="sxs-lookup"><span data-stu-id="851c5-152">n/a</span></span> | <span data-ttu-id="851c5-153">要共享的内容的 href。</span><span class="sxs-lookup"><span data-stu-id="851c5-153">The href of the content to share.</span></span> |
| <span data-ttu-id="851c5-154">preview</span><span class="sxs-lookup"><span data-stu-id="851c5-154">preview</span></span> | `data-preview` | <span data-ttu-id="851c5-155">boolean (字符串类型) </span><span class="sxs-lookup"><span data-stu-id="851c5-155">boolean (as a string)</span></span> | `true` | <span data-ttu-id="851c5-156">是否显示要共享的内容的预览。</span><span class="sxs-lookup"><span data-stu-id="851c5-156">Whether or not to show a preview of the content to share.</span></span> |
| <span data-ttu-id="851c5-157">iconPxSize</span><span class="sxs-lookup"><span data-stu-id="851c5-157">iconPxSize</span></span> | `data-icon-px-size` | <span data-ttu-id="851c5-158">数字 (字符串形式) </span><span class="sxs-lookup"><span data-stu-id="851c5-158">number (as a string)</span></span> | `32` | <span data-ttu-id="851c5-159">要呈现的"共享到 Teams"按钮的大小（以像素为单位）。</span><span class="sxs-lookup"><span data-stu-id="851c5-159">The size in pixels of the Share-to-Teams button to render.</span></span> |
| <span data-ttu-id="851c5-160">msgText</span><span class="sxs-lookup"><span data-stu-id="851c5-160">msgText</span></span> | `data-msg-text` | <span data-ttu-id="851c5-161">string</span><span class="sxs-lookup"><span data-stu-id="851c5-161">string</span></span> | <span data-ttu-id="851c5-162">不适用</span><span class="sxs-lookup"><span data-stu-id="851c5-162">n/a</span></span> | <span data-ttu-id="851c5-163">要插入到邮件撰写框中的链接之前的默认文本。</span><span class="sxs-lookup"><span data-stu-id="851c5-163">Default Text to be inserted before the link in the message compose box.</span></span> <span data-ttu-id="851c5-164">最大字符数为 200。</span><span class="sxs-lookup"><span data-stu-id="851c5-164">Maximum number of characters is 200.</span></span> |
| <span data-ttu-id="851c5-165">assignInstr</span><span class="sxs-lookup"><span data-stu-id="851c5-165">assignInstr</span></span> | `data-assign-instr` | <span data-ttu-id="851c5-166">string</span><span class="sxs-lookup"><span data-stu-id="851c5-166">string</span></span> | <span data-ttu-id="851c5-167">不适用</span><span class="sxs-lookup"><span data-stu-id="851c5-167">n/a</span></span> | <span data-ttu-id="851c5-168">要插入到工作分配"说明"字段中的默认文本。</span><span class="sxs-lookup"><span data-stu-id="851c5-168">Default Text to be inserted in the assignments "Instructions" field.</span></span> <span data-ttu-id="851c5-169">最大字符数为 200。</span><span class="sxs-lookup"><span data-stu-id="851c5-169">Maximum number of characters is 200.</span></span> |
| <span data-ttu-id="851c5-170">assignTitle</span><span class="sxs-lookup"><span data-stu-id="851c5-170">assignTitle</span></span> | `data-assign-title` | <span data-ttu-id="851c5-171">string</span><span class="sxs-lookup"><span data-stu-id="851c5-171">string</span></span> | <span data-ttu-id="851c5-172">不适用</span><span class="sxs-lookup"><span data-stu-id="851c5-172">n/a</span></span> | <span data-ttu-id="851c5-173">要插入到工作分配"标题"字段中的默认文本。</span><span class="sxs-lookup"><span data-stu-id="851c5-173">Default Text to be inserted in the assignments "Title" field.</span></span> <span data-ttu-id="851c5-174">最大字符数为 50。</span><span class="sxs-lookup"><span data-stu-id="851c5-174">Maximum number of characters is 50.</span></span> |

### <a name="methods"></a><span data-ttu-id="851c5-175">方法</span><span class="sxs-lookup"><span data-stu-id="851c5-175">Methods</span></span>

**`shareToMicrosoftTeams.renderButtons(options)`**

<span data-ttu-id="851c5-176">`options` (可选) ： `{ elements?: HTMLElement[] }`</span><span class="sxs-lookup"><span data-stu-id="851c5-176">`options` (optional): `{ elements?: HTMLElement[] }`</span></span>

<span data-ttu-id="851c5-177">目前，所有共享按钮都呈现在页面上。</span><span class="sxs-lookup"><span data-stu-id="851c5-177">Currently, all share buttons are rendered on the page.</span></span> <span data-ttu-id="851c5-178">如果随元素列表一起提供可选对象 `options` ，则这些元素将呈现到共享按钮中。</span><span class="sxs-lookup"><span data-stu-id="851c5-178">If an optional `options` object is supplied with a list of elements, those elements are rendered into share buttons.</span></span>

### <a name="set-default-form-values"></a><span data-ttu-id="851c5-179">设置默认表单值</span><span class="sxs-lookup"><span data-stu-id="851c5-179">Set default form values</span></span>

<span data-ttu-id="851c5-180">可以选择在"共享到 Teams"表单上设置以下字段的默认值：</span><span class="sxs-lookup"><span data-stu-id="851c5-180">You can select to set default values for the following fields on the Share to Teams form:</span></span>

* <span data-ttu-id="851c5-181">对此说一些： `msgText`</span><span class="sxs-lookup"><span data-stu-id="851c5-181">Say something about this: `msgText`</span></span>
* <span data-ttu-id="851c5-182">工作分配说明： `assignInstr`</span><span class="sxs-lookup"><span data-stu-id="851c5-182">Assignment Instructions: `assignInstr`</span></span>
* <span data-ttu-id="851c5-183">工作分配标题： `assignTitle`</span><span class="sxs-lookup"><span data-stu-id="851c5-183">Assignment Title: `assignTitle`</span></span>

#### <a name="example"></a><span data-ttu-id="851c5-184">示例</span><span class="sxs-lookup"><span data-stu-id="851c5-184">Example</span></span>

 <span data-ttu-id="851c5-185">下面的示例中给出默认表单值：</span><span class="sxs-lookup"><span data-stu-id="851c5-185">Default form values are given in the following example:</span></span>

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```

## <a name="see-also"></a><span data-ttu-id="851c5-186">另请参阅</span><span class="sxs-lookup"><span data-stu-id="851c5-186">See also</span></span>

[<span data-ttu-id="851c5-187">集成 web 应用</span><span class="sxs-lookup"><span data-stu-id="851c5-187">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
