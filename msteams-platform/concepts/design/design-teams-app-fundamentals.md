---
title: 设计应用 - 了解设计系统
description: 了解设计应用Microsoft Teams的基础知识，包括布局、配色方案等。
author: heath-hamilton
localization_priority: Normal
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 0af2a22200e62be9289f167b0306c9769366e46a
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630837"
---
# <a name="microsoft-teams-app-design-system"></a><span data-ttu-id="5794e-103">Microsoft Teams应用设计系统</span><span class="sxs-lookup"><span data-stu-id="5794e-103">Microsoft Teams app design system</span></span>

<span data-ttu-id="5794e-104">快速了解应用设计Teams基础。</span><span class="sxs-lookup"><span data-stu-id="5794e-104">Quickly learn about the fundamentals of Teams app design.</span></span> <span data-ttu-id="5794e-105">你可以从图块 UI 工具包Microsoft Teams <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Ui 工具包 (指南) 。 </a></span><span class="sxs-lookup"><span data-stu-id="5794e-105">You can find comprehensive guidance and examples in the <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft Teams UI Kit (Figma)</a>.</span></span>

## <a name="layout"></a><span data-ttu-id="5794e-106">布局</span><span class="sxs-lookup"><span data-stu-id="5794e-106">Layout</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="5794e-107">Teams依赖于网格布局，以确保设计组件之间保持一致和美观的关系。</span><span class="sxs-lookup"><span data-stu-id="5794e-107">Teams relies on a grid layout to ensure consistent and elegant relationships between design components.</span></span> <span data-ttu-id="5794e-108">网格的 4 像素基本单位允许组件在网格中跨所有显示大小一致Teams。</span><span class="sxs-lookup"><span data-stu-id="5794e-108">The grid’s 4-pixel base unit allows components to scale consistently across all display sizes in Teams.</span></span>

      * [<span data-ttu-id="5794e-109">请参阅图 (图的完整) </span><span class="sxs-lookup"><span data-stu-id="5794e-109">See full layout guidelines (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)
      * [<span data-ttu-id="5794e-110">使用 Fluent UI (实现布局) </span><span class="sxs-lookup"><span data-stu-id="5794e-110">Implement layout (Fluent UI)</span></span>](https://developer.microsoft.com/fluentui#/styles/web/layout)

   :::column-end:::
   :::column span="1":::
      :::image type="content" source="../../assets/images/design-guidelines/teams-layout.png" alt-text="布局的概念Teams图像。" border="false":::
   :::column-end:::

:::row-end:::

## <a name="avatars"></a><span data-ttu-id="5794e-112">头像</span><span class="sxs-lookup"><span data-stu-id="5794e-112">Avatars</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="5794e-113">头像是图像中人员、团队、机器人或实体的图形Teams。</span><span class="sxs-lookup"><span data-stu-id="5794e-113">An avatar is a graphical representation of a person, team, bot, or entity in Teams.</span></span> <span data-ttu-id="5794e-114">头像组通常用于以保留垂直空间的方式传达实时活动或代表名单。</span><span class="sxs-lookup"><span data-stu-id="5794e-114">An avatar group is often used to convey live activity or a represent a roster in a way that preserves vertical space.</span></span> 

      * <span data-ttu-id="5794e-115"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">请参阅完整头像指南 (图) </a></span><span class="sxs-lookup"><span data-stu-id="5794e-115"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">See full avatar guidelines (Figma)</a></span></span>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-avatars.png" alt-text="虚拟形象Teams图像。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="icons"></a><span data-ttu-id="5794e-117">图标</span><span class="sxs-lookup"><span data-stu-id="5794e-117">Icons</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="5794e-118">应用的主要图标在向用户传达品牌方面Teams长。</span><span class="sxs-lookup"><span data-stu-id="5794e-118">Your app's primary icon can go a long way in conveying your brand to Teams users.</span></span> <span data-ttu-id="5794e-119">正确设计图标对于将应用发布到应用商店[Teams](../../concepts/build-and-test/apps-package.md)很重要。</span><span class="sxs-lookup"><span data-stu-id="5794e-119">Getting your icon design right is also important for [publishing your app](../../concepts/build-and-test/apps-package.md) to the Teams store.</span></span>

      <span data-ttu-id="5794e-120">还可以在整个应用中使用 Fluent UI 图标：</span><span class="sxs-lookup"><span data-stu-id="5794e-120">You also can use Fluent UI icons throughout your app:</span></span>

      * <span data-ttu-id="5794e-121"><a href="https://www.figma.com/community/file/836835755999342788" target="_blank">获取"图 (的最新 Fluent 图标) </a></span><span class="sxs-lookup"><span data-stu-id="5794e-121"><a href="https://www.figma.com/community/file/836835755999342788" target="_blank">Get the latest Fluent icon set (Figma)</a></span></span>
      * [<span data-ttu-id="5794e-122">实现 Fluent UI (图标) </span><span class="sxs-lookup"><span data-stu-id="5794e-122">Implement the icons (Fluent UI)</span></span>](https://developer.microsoft.com/fluentui#/styles/web/icons)

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-iconography.png" alt-text="图标的概念Teams图像。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="type"></a><span data-ttu-id="5794e-124">类型</span><span class="sxs-lookup"><span data-stu-id="5794e-124">Type</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="5794e-125">Teams将 Segoe UI 用于其类型渐变以及不同的字体大小和权重，以帮助创建层次结构并确保可读性。</span><span class="sxs-lookup"><span data-stu-id="5794e-125">Teams uses Segoe UI for its type ramp and different font sizes and weights to help create hierarchy and ensure readability.</span></span>

      * <span data-ttu-id="5794e-126"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">请参阅图 (图的完整类型) </a></span><span class="sxs-lookup"><span data-stu-id="5794e-126"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">See full type guidelines (Figma)</a></span></span>
      * [<span data-ttu-id="5794e-127">使用 Fluent UI (实现版式) </span><span class="sxs-lookup"><span data-stu-id="5794e-127">Implement typography (Fluent UI)</span></span>](https://developer.microsoft.com/fluentui#/styles/web/typography)

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-typography.png" alt-text="版式Teams图像。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="colors"></a><span data-ttu-id="5794e-129">颜色</span><span class="sxs-lookup"><span data-stu-id="5794e-129">Colors</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="5794e-130">Teams Web 和桌面支持默认 (浅) 、深色和高对比度主题，而Teams支持浅色和深色主题。</span><span class="sxs-lookup"><span data-stu-id="5794e-130">Teams web and desktop supports default (light), dark, and high-contrast themes, while Teams mobile supports light and dark themes.</span></span> <span data-ttu-id="5794e-131">每个主题都有自己的配色方案。</span><span class="sxs-lookup"><span data-stu-id="5794e-131">Each theme has its own color scheme.</span></span>

      * <span data-ttu-id="5794e-132"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">请参阅图图ma 的完整颜色指南和 (颜色) </a></span><span class="sxs-lookup"><span data-stu-id="5794e-132"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">See full color guidelines and available color tokens (Figma)</a></span></span>
      * [<span data-ttu-id="5794e-133">使用 Fluent UI (实现) </span><span class="sxs-lookup"><span data-stu-id="5794e-133">Implement colors (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/0.51.7/colors)

   :::column-end:::
   :::column span="1":::
      :::image type="content" source="../../assets/images/design-guidelines/teams-color.png" alt-text="颜色的概念Teams图像。" border="false":::
   :::column-end:::

:::row-end:::

## <a name="shape-and-elevation"></a><span data-ttu-id="5794e-135">形状和仰角</span><span class="sxs-lookup"><span data-stu-id="5794e-135">Shape and elevation</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="5794e-136">可以使用形状和仰角在应用中创建其他层次结构。</span><span class="sxs-lookup"><span data-stu-id="5794e-136">You can use shape and elevation to create additional hierarchy in your app.</span></span> 

      * <span data-ttu-id="5794e-137"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">请参阅完整形状和海拔指南 (图) </a></span><span class="sxs-lookup"><span data-stu-id="5794e-137"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">See full shape and elevation guidelines (Figma)</a></span></span>
      * [<span data-ttu-id="5794e-138">使用 Fluent UI 对象 (形状和提升) </span><span class="sxs-lookup"><span data-stu-id="5794e-138">Implement shape and elevation (Fluent UI)</span></span>](https://developer.microsoft.com/fluentui#/styles/web/elevation)

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/shape-and-elevation.png" alt-text="形状和仰角的概念。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="copy-and-content"></a><span data-ttu-id="5794e-140">复制和内容</span><span class="sxs-lookup"><span data-stu-id="5794e-140">Copy and content</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="5794e-141">若要感觉这是Teams的一部分，应用副本通常应遵循[以下 Microsoft 语音](/style-guide/brand-voice-above-all-simple-human)原则：温和轻松、简洁明了且随时可供手用。</span><span class="sxs-lookup"><span data-stu-id="5794e-141">To feel part of Teams, your app copy in general should follow these [Microsoft voice principles](/style-guide/brand-voice-above-all-simple-human): warm and relaxed, crisp and clear, and ready to lend hand.</span></span>

      * <span data-ttu-id="5794e-142"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">请参阅完整副本和内容指南，包括为 Bot (使用图) </a></span><span class="sxs-lookup"><span data-stu-id="5794e-142"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">See full copy and content guidelines—including writing for bots (Figma)</a></span></span>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-copy-and-content.png" alt-text="复制和内容的概念图像。" border="false":::

   :::column-end:::
:::row-end:::
