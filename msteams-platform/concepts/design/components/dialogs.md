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
# <a name="dialogs"></a>Dialogs

对话框应谨慎使用，因为它们可能会造成中断，并且应该有一种清楚的方法让用户退出。

---

## <a name="sizes"></a>大小

我们有3个对话框大小可供选择。 选择适合您的内容的大小。
[!include[Dialog sizes](~/includes/design/dialogs-image-sizes.html)]

---

## <a name="buttons"></a>按钮

按钮右对齐。
所有其他元素（复选框、帮助文本等）应左对齐。
不要重复负操作（永远不会同时提供 "X" 和 "取消" 按钮）。
"应用" 按钮应与 "取消" 按钮配对。
[!include[Dialog buttons](~/includes/design/dialogs-image-buttons.html)]

---

## <a name="scrolling"></a>上下

在某些情况下，将滚动内容。 对话框标题和其他重要信息将保持不变。
[!include[Dialog scrolling](~/includes/design/dialogs-image-scrolling.html)]

---

## <a name="padding"></a>填充

对话框中所有四个边的边距都应为32。
[!include[Dialog padding](~/includes/design/dialogs-image-padding.html)]

---

## <a name="typography"></a>版式

我们将 Microsoft Yahei UI SemiBold at 18pt （title2），并 $app-黑色的对话框标题。 对于正文文本，我们将 Microsoft Yahei UI 14pt （base）和 $app-黑色。
[!include[Dialog typography](~/includes/design/dialogs-image-typography.html)]