---
title: 使用高级 UI 组件设计应用
author: heath-hamilton
description: 了解跨应用程序使用的 UI Teams。
ms.author: surbhigupta
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: ae1c2793586dc638d56051e105482aac92e01091
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644920"
---
# <a name="designing-your-microsoft-teams-app-with-advanced-ui-components"></a><span data-ttu-id="70ab4-103">使用高级 UI Microsoft Teams设计应用</span><span class="sxs-lookup"><span data-stu-id="70ab4-103">Designing your Microsoft Teams app with advanced UI components</span></span>

<span data-ttu-id="70ab4-104">以下组件是基本[UI](~/concepts/design/design-teams-app-basic-ui-components.md)组件的组合，可用于常见Teams设计情况，如导航。</span><span class="sxs-lookup"><span data-stu-id="70ab4-104">The following components are a combination of [basic UI components](~/concepts/design/design-teams-app-basic-ui-components.md) that you can use for common Teams design situations, such as navigation.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="70ab4-105">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="70ab4-105">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="70ab4-106">基于<a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent UI，Microsoft Teams</a>UI 工具包包括专为生成应用程序而设计的组件Teams模式。</span><span class="sxs-lookup"><span data-stu-id="70ab4-106">Based on <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent UI</a>, the Microsoft Teams UI Kit includes components and patterns that are designed specifically for building Teams apps.</span></span> <span data-ttu-id="70ab4-107">在 UI 工具包中，你可以将此处列出的组件直接获取并插入设计中，并查看如何使用每个组件的更多示例。</span><span class="sxs-lookup"><span data-stu-id="70ab4-107">In the UI kit, you can grab and insert the components listed here directly into your design and see more examples of how to use each component.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="70ab4-108">获取 Microsoft Teams UI Kit （用户）</span><span class="sxs-lookup"><span data-stu-id="70ab4-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="breadcrumb"></a><span data-ttu-id="70ab4-109">痕迹导航栏</span><span class="sxs-lookup"><span data-stu-id="70ab4-109">Breadcrumb</span></span>

<span data-ttu-id="70ab4-110">痕迹导航是一种导航帮助，可传达应用的层次结构。</span><span class="sxs-lookup"><span data-stu-id="70ab4-110">Breadcrumbs are a navigational aid that convey your app’s hierarchy.</span></span> <span data-ttu-id="70ab4-111">它们可帮助用户了解他们查看的页面如何适应整体体验，并提供了对层次结构中较高级别的一键访问。</span><span class="sxs-lookup"><span data-stu-id="70ab4-111">They help users understand how the page they’re viewing fits into the overall experience and afford one-click access to higher levels in that hierarchy.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="70ab4-112">热门用例</span><span class="sxs-lookup"><span data-stu-id="70ab4-112">Top use cases</span></span>

* <span data-ttu-id="70ab4-113">通信层次结构</span><span class="sxs-lookup"><span data-stu-id="70ab4-113">Communicate hierarchy</span></span>
* <span data-ttu-id="70ab4-114">导航</span><span class="sxs-lookup"><span data-stu-id="70ab4-114">Navigation</span></span>

# <a name="desktop"></a>[<span data-ttu-id="70ab4-115">桌面</span><span class="sxs-lookup"><span data-stu-id="70ab4-115">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="示例在桌面上显示痕迹导航模板。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="70ab4-117">移动</span><span class="sxs-lookup"><span data-stu-id="70ab4-117">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-breadcrumb.png" alt-text="示例演示移动版痕迹导航模板。" border="false":::

---

## <a name="left-nav"></a><span data-ttu-id="70ab4-119">左导航</span><span class="sxs-lookup"><span data-stu-id="70ab4-119">Left nav</span></span>

<span data-ttu-id="70ab4-120">使用左侧导航键浏览"导航"选项卡Teams页面。在下面的示例中，左侧导航位于通道列表和选项卡内容之间。</span><span class="sxs-lookup"><span data-stu-id="70ab4-120">Use the left nav to browse multiple pages within your Teams tab. In the following example, the left nav is between the channel list and tab content.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="70ab4-121">热门用例</span><span class="sxs-lookup"><span data-stu-id="70ab4-121">Top use cases</span></span>

* <span data-ttu-id="70ab4-122">浏览"页面"选项卡Teams页面。</span><span class="sxs-lookup"><span data-stu-id="70ab4-122">Browse multiple pages within a Teams tab.</span></span>
* <span data-ttu-id="70ab4-123">将复杂应用分解为多个页面。</span><span class="sxs-lookup"><span data-stu-id="70ab4-123">Break down complex apps into multiple pages.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="70ab4-124">桌面</span><span class="sxs-lookup"><span data-stu-id="70ab4-124">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="示例在桌面上显示左侧导航模板。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="70ab4-126">移动</span><span class="sxs-lookup"><span data-stu-id="70ab4-126">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-left-nav.png" alt-text="示例显示移动版上的左侧导航模板。" border="false":::

---

## <a name="notification-bar"></a><span data-ttu-id="70ab4-128">通知栏</span><span class="sxs-lookup"><span data-stu-id="70ab4-128">Notification bar</span></span>

<span data-ttu-id="70ab4-129">通知栏是一个专用区域，用于显示无需用户立即采取措施的简短重要消息。</span><span class="sxs-lookup"><span data-stu-id="70ab4-129">A notification bar is a dedicated area for displaying a brief, important messages that do not require the user to take immediate action.</span></span> <span data-ttu-id="70ab4-130">特定背景颜色和图标与特定类型的邮件相关联， (请参阅下面的) 。</span><span class="sxs-lookup"><span data-stu-id="70ab4-130">Specific background colors and icons are associated with specific types of messages (see below).</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="70ab4-131">热门用例</span><span class="sxs-lookup"><span data-stu-id="70ab4-131">Top use cases</span></span>

* <span data-ttu-id="70ab4-132">关键消息、错误和警告</span><span class="sxs-lookup"><span data-stu-id="70ab4-132">Critical messages, errors, and warnings</span></span>
* <span data-ttu-id="70ab4-133">成功消息</span><span class="sxs-lookup"><span data-stu-id="70ab4-133">Success messages</span></span>
* <span data-ttu-id="70ab4-134">信息性或促销性消息</span><span class="sxs-lookup"><span data-stu-id="70ab4-134">Informational or promotional messages</span></span>

# <a name="desktop"></a>[<span data-ttu-id="70ab4-135">桌面</span><span class="sxs-lookup"><span data-stu-id="70ab4-135">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="示例显示桌面上的通知栏 UI 模板。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="70ab4-137">移动</span><span class="sxs-lookup"><span data-stu-id="70ab4-137">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-notification-bar.png" alt-text="示例显示移动设备上的通知栏 UI 模板。" border="false":::

---

## <a name="stage"></a><span data-ttu-id="70ab4-139">阶段</span><span class="sxs-lookup"><span data-stu-id="70ab4-139">Stage</span></span>

<span data-ttu-id="70ab4-140">Stage 为用户提供了一种在应用程序中打开实体（如图像、文件或网站Teams而不是在另一个应用或浏览器中打开它的方法。</span><span class="sxs-lookup"><span data-stu-id="70ab4-140">Stage offers a way for users to open an entity—like an image, file, or website—in Teams instead of opening it in another app or browser.</span></span> <span data-ttu-id="70ab4-141">阶段的主要用例是查看;图面不应用于复杂的交互。</span><span class="sxs-lookup"><span data-stu-id="70ab4-141">The primary use case of stage is viewing; the surface should not be used for complex interactions.</span></span>

<span data-ttu-id="70ab4-142"> (实现说明：使用大型任务模块[.) ](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)</span><span class="sxs-lookup"><span data-stu-id="70ab4-142">(Implementation note: Build your stage using a large [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).)</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="70ab4-143">热门用例</span><span class="sxs-lookup"><span data-stu-id="70ab4-143">Top use cases</span></span>

* <span data-ttu-id="70ab4-144">在浏览器中打开实体Teams而不是其他应用或浏览器</span><span class="sxs-lookup"><span data-stu-id="70ab4-144">Open an entity in Teams instead of another app or browser</span></span>
* <span data-ttu-id="70ab4-145">聚焦媒体或其他内容</span><span class="sxs-lookup"><span data-stu-id="70ab4-145">Spotlight media or other content</span></span>

# <a name="desktop"></a>[<span data-ttu-id="70ab4-146">桌面</span><span class="sxs-lookup"><span data-stu-id="70ab4-146">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="示例在桌面上显示阶段模板。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="70ab4-148">移动</span><span class="sxs-lookup"><span data-stu-id="70ab4-148">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="70ab4-149">你的应用可以从自适应卡片、共享链接或视觉组件启动阶段 (如图表) 。</span><span class="sxs-lookup"><span data-stu-id="70ab4-149">Your app can launch a stage from an Adaptive Card, shared link, or visual components (such as a chart).</span></span>

:::image type="content" source="../../assets/images/ui-templates/mobile-stage.png" alt-text="示例演示移动设备上的阶段模板。" border="false":::

---

## <a name="toolbar"></a><span data-ttu-id="70ab4-151">工具栏</span><span class="sxs-lookup"><span data-stu-id="70ab4-151">Toolbar</span></span>

<span data-ttu-id="70ab4-152">工具栏是一个容器，用于对一组控件进行分组。</span><span class="sxs-lookup"><span data-stu-id="70ab4-152">A toolbar is a container for grouping a set of controls.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="70ab4-153">热门用例</span><span class="sxs-lookup"><span data-stu-id="70ab4-153">Top use cases</span></span>

* <span data-ttu-id="70ab4-154">应用内容的上下文操作</span><span class="sxs-lookup"><span data-stu-id="70ab4-154">Contextual actions on app content</span></span>
* <span data-ttu-id="70ab4-155">上下文筛选器和查找</span><span class="sxs-lookup"><span data-stu-id="70ab4-155">Contextual filter and find</span></span>
* <span data-ttu-id="70ab4-156">导航和痕迹导航</span><span class="sxs-lookup"><span data-stu-id="70ab4-156">Navigation and breadcrumbs</span></span>

# <a name="desktop"></a>[<span data-ttu-id="70ab4-157">桌面</span><span class="sxs-lookup"><span data-stu-id="70ab4-157">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="示例在桌面上显示工具栏模板。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="70ab4-159">移动</span><span class="sxs-lookup"><span data-stu-id="70ab4-159">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-toolbar.png" alt-text="示例显示移动设备上的工具栏模板。" border="false":::

---
