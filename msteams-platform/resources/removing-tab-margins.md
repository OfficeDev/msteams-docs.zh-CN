---
title: 选项卡边距更改
author: surbhigupta
description: 了解如何使用 UI 工具包在 Microsoft Teams 中删除选项卡周围的边距。 了解额外的填充效果，以及左侧、右侧、顶部和底部的边距大小。
ms.topic: reference
ms.localizationpriority: medium
ms.author: lomeybur
ms.openlocfilehash: ba203cd89904acde77e1d9971175afc19c47d24d
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2022
ms.locfileid: "68820071"
---
# <a name="tab-margin-changes"></a>选项卡边距更改

本文档介绍删除 Microsoft Teams 中所有选项卡周围的边距如何增强应用生成体验。 这是 2021 年 Teams 中引入的增强功能。
通过删除所有选项卡周围的边距，可以生成看起来更原生 Teams 的应用。 带有删除边距的选项卡与 Microsoft Teams 的 [UI 工具包设计](~/tabs/design/tabs.md)保持一致。 大多数应用都体验到没有边距的增强外观。

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="制表符和不带边距":::

> [!NOTE]
> 此功能不适用于移动客户端，因为移动客户端中查看的选项卡没有边距。

## <a name="guidelines"></a>准则

选项卡边距删除会影响使用选项卡的 Teams 应用。 在这种情况下，可以根据需要在选项卡设计周围添加边距。 生产中的应用设计具有额外的填充效果，即 Teams 提供的边距和选项卡提供的边距。但是，额外的填充只是暂时的，几周后就会消失，只留下应用提供的填充。

## <a name="faq"></a>常见问题

**应用部件版式（如标题栏或任务栏）是否可以触摸我们设计的边缘？**

是的，这很好，Teams 鼓励此类设计。 它有助于应用感觉本机。

**是否允许应用内容（如文本、徽标和图像）触摸我们设计的左右边缘？**

否，你必须在所有应用内容的左侧和右侧提供自己的填充或边距，以确保它不会触及 UI 的边缘。 如有必要，还可以在选项卡顶部添加边距。

**Teams 以前应用的选项卡边距大小是多少？**

* 左侧和右侧：20 像素
* 顶部：16 像素
* 底部：0 像素

> [!IMPORTANT]
>
> * 删除所有选项卡的边距：个人选项卡、 (组) 聊天选项卡、会议选项卡和频道选项卡。
> * 选项卡边距删除更改适用于所有选项卡。 无法选择加入或选择退出更改。
> * 选项卡边距的更改可能会影响依赖 Microsoft Teams 在其 UI 周围提供边距的选项卡。

## <a name="see-also"></a>另请参阅

* [Teams 的生成选项卡](../tabs/what-are-tabs.md)
* [创建个人选项卡](../tabs/how-to/create-personal-tab.md)
* [创建频道选项卡或组选项卡](../tabs/how-to/create-channel-group-tab.md)
