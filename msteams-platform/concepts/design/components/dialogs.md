---
title: 设计准则参考
description: 介绍在应用程序中使用对话的指南
keywords: 团队设计准则参考组件对话框
ms.openlocfilehash: d244eedde66085d41b1f356176a7775de304aaf4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673073"
---
# <a name="dialogs"></a><span data-ttu-id="30162-104">Dialogs</span><span class="sxs-lookup"><span data-stu-id="30162-104">Dialogs</span></span>

<span data-ttu-id="30162-105">对话框应谨慎使用，因为它们可能会造成中断，并且应该有一种清楚的方法让用户退出。</span><span class="sxs-lookup"><span data-stu-id="30162-105">Dialogs should be used sparingly since they can be disruptive, and should have a clear way for the user to exit.</span></span>

---

## <a name="sizes"></a><span data-ttu-id="30162-106">大小</span><span class="sxs-lookup"><span data-stu-id="30162-106">Sizes</span></span>

<span data-ttu-id="30162-107">我们有3个对话框大小可供选择。</span><span class="sxs-lookup"><span data-stu-id="30162-107">We have 3 dialog sizes to choose from.</span></span> <span data-ttu-id="30162-108">选择适合您的内容的大小。</span><span class="sxs-lookup"><span data-stu-id="30162-108">Choose the size that is appropriate for the content you have.</span></span>
[!include[Dialog sizes](~/includes/design/dialogs-image-sizes.html)]

---

## <a name="buttons"></a><span data-ttu-id="30162-109">按钮</span><span class="sxs-lookup"><span data-stu-id="30162-109">Buttons</span></span>

<span data-ttu-id="30162-110">按钮右对齐。</span><span class="sxs-lookup"><span data-stu-id="30162-110">Buttons are right-justified.</span></span>
<span data-ttu-id="30162-111">所有其他元素（复选框、帮助文本等）应左对齐。</span><span class="sxs-lookup"><span data-stu-id="30162-111">All other elements (checkboxes, help text, etc.) should be left-justified.</span></span>
<span data-ttu-id="30162-112">不要重复负操作（永远不会同时提供 "X" 和 "取消" 按钮）。</span><span class="sxs-lookup"><span data-stu-id="30162-112">Don’t duplicate negative actions (Never provide an ‘X’ and a ‘Cancel’ button at the same time.).</span></span>
<span data-ttu-id="30162-113">"应用" 按钮应与 "取消" 按钮配对。</span><span class="sxs-lookup"><span data-stu-id="30162-113">‘Apply’ buttons should be paired with ‘Cancel’ buttons.</span></span>
[!include[Dialog buttons](~/includes/design/dialogs-image-buttons.html)]

---

## <a name="scrolling"></a><span data-ttu-id="30162-114">上下</span><span class="sxs-lookup"><span data-stu-id="30162-114">Scrolling</span></span>

<span data-ttu-id="30162-115">在某些情况下，将滚动内容。</span><span class="sxs-lookup"><span data-stu-id="30162-115">In some cases, content will scroll.</span></span> <span data-ttu-id="30162-116">对话框标题和其他重要信息将保持不变。</span><span class="sxs-lookup"><span data-stu-id="30162-116">The dialog title and other important information remains in place.</span></span>
[!include[Dialog scrolling](~/includes/design/dialogs-image-scrolling.html)]

---

## <a name="padding"></a><span data-ttu-id="30162-117">填充</span><span class="sxs-lookup"><span data-stu-id="30162-117">Padding</span></span>

<span data-ttu-id="30162-118">对话框中所有四个边的边距都应为32。</span><span class="sxs-lookup"><span data-stu-id="30162-118">The padding around all four sides of the dialog should be 32px.</span></span>
[!include[Dialog padding](~/includes/design/dialogs-image-padding.html)]

---

## <a name="typography"></a><span data-ttu-id="30162-119">版式</span><span class="sxs-lookup"><span data-stu-id="30162-119">Typography</span></span>

<span data-ttu-id="30162-120">我们将 Microsoft Yahei UI SemiBold at 18pt （title2），并 $app-黑色的对话框标题。</span><span class="sxs-lookup"><span data-stu-id="30162-120">We use Segoe UI SemiBold at 18pt (title2) and $app-black for dialog titles.</span></span> <span data-ttu-id="30162-121">对于正文文本，我们将 Microsoft Yahei UI 14pt （base）和 $app-黑色。</span><span class="sxs-lookup"><span data-stu-id="30162-121">For body text, we use Segoe UI Regular at 14pt (base) and $app-black.</span></span>
[!include[Dialog typography](~/includes/design/dialogs-image-typography.html)]