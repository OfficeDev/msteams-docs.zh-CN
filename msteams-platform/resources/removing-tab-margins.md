---
title: 删除 Microsoft Teams 中的选项卡边距
author: laujan
description: 描述删除选项卡边距将如何增强开发人员的体验。
keywords: 选项卡删除边距填充
ms.topic: reference
ms.author: lomeybur
ms.openlocfilehash: 87766a40730fdaa2da80c2e0031eab655a993c33
ms.sourcegitcommit: 9cfbc44912980a33d2d7c7c85739aeea6ccb41de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "50479951"
---
# <a name="tab-margin-changes"></a>制表位边距更改

本文档介绍删除 Microsoft Teams 中所有选项卡的边距如何增强开发人员在生成应用时的体验。 这是 2021 年 Microsoft Teams 中引入的增强功能。
删除所有选项卡周围的边距将允许开发人员生成对 Teams 来说更本机的应用。 这也符合我们的 UI [工具包设计](~/tabs/design/tabs.md)。 大多数应用已经看起来更好，没有围绕其体验的边距。 但是，某些选项卡受此更改的视觉影响，开发人员必须进行必要的更改。

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="制表符和无边距" border="false":::

## <a name="timelines"></a>日程表

* 2021 年 3 月 5 日 - 在[公共开发者预览版。](~/resources/dev-preview/developer-preview-intro.md)
* 2021 年 5 月 1 日 - 将在生产中删除边距。

## <a name="guidelines"></a>准则

使用选项卡的 Microsoft Teams 应用将受此更改的影响。 开发人员应切换到 [公共开发者预览版，](~/resources/dev-preview/developer-preview-intro.md) 以确定其选项卡如何受到影响，并进行必要的更改。

选项卡开发人员不得依赖 Teams 提供其选项卡周围的边距。 建议开发人员根据需要添加选项卡设计周围的边距。 生产中的应用设计可能看起来有额外的填充，即 Teams 提供的边距和选项卡提供的边距。但是，额外的填充只是临时的，将在几周后消失，仅留下应用提供的填充。

## <a name="faq"></a>常见问题

**应用部件版式（如标题栏或任务栏）是否适合触摸我们设计的边缘？**

是的，这很好，建议这样做。 这有助于应用感觉本机。

**应用内容（如文本、徽标和图像）可以触摸我们设计的左右边缘吗？**

否，你必须在所有应用内容的左侧和右侧提供自己的填充或边距，以确保它不会接触 UI 的边缘。 如果需要，还可以在选项卡顶部添加边距。

**Teams 之前应用的边距大小如何？**

* 左右：20px
* 顶部：16px
* 底部：0px

> [!IMPORTANT]
> * 所有选项卡都删除了其边距：个人选项卡、 (组) 聊天选项卡、会议选项卡和频道选项卡。
> * 无法选择加入或选择退出此更改。 它将应用于所有选项卡。
> * 此更改可能会影响依赖 Microsoft Teams 提供 UI 周围边距的选项卡。
