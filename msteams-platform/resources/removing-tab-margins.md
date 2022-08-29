---
title: 选项卡边距更改
author: surbhigupta
description: 了解如何使用 UI 工具包删除 Microsoft Teams 中选项卡周围的边距。 了解额外的填充效果、左侧、右侧、顶部和底部的边距大小。
ms.topic: reference
ms.localizationpriority: medium
ms.author: lomeybur
ms.openlocfilehash: 715c6b735323e442490de8634384054be565e7a8
ms.sourcegitcommit: 87bba925d005eb331d876a0b9b75154f8100e911
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2022
ms.locfileid: "67450441"
---
# <a name="tab-margin-changes"></a>选项卡边距更改

本文档介绍删除 Microsoft Teams 中所有选项卡周围的边距如何增强应用生成体验。 这是 Teams 2021 中引入的增强功能。
可以通过删除所有选项卡周围的边距来生成看起来更本机到 Teams 的应用。 带删除边距的选项卡与 Microsoft Teams 的 [UI 工具包设计](~/tabs/design/tabs.md)一致。 大多数应用在不带边距的情况下体验增强的外观。

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="Tab wit 和无边距":::

> [!NOTE]
> 此功能不适用于移动客户端，因为在移动客户端中查看的选项卡没有边距。

## <a name="guidelines"></a>准则

删除选项卡边距会影响使用选项卡的 Teams 应用。 在这种情况下，可以在需要选项卡设计的位置添加边距。 生产中的应用设计具有额外的填充效果，即 Teams 提供的边距和选项卡提供的边距。但是，额外的填充只是临时的，几周后就会消失，只留下应用提供的填充。

## <a name="faq"></a>常见问题

**应用部件版式（如标头栏或任务栏）可以触摸设计的边缘吗？**

是的，这很好，Teams 鼓励这种设计。 它可帮助应用感觉原生。

**应用内容（如文本、徽标和图像）是否可以触摸设计左边缘和右边缘？**

否，必须向所有应用内容的左侧和右侧提供自己的填充或边距，以确保它不会触及 UI 的边缘。 如有必要，还可以在选项卡顶部添加边距。

**Teams 以前应用的选项卡边距的大小是怎样的？**

* 左右：20 像素
* 顶部：16 像素
* 底部：0 像素

> [!IMPORTANT]
>
> * 所有选项卡都删除了其边距：个人选项卡、 (组) 聊天选项卡、会议选项卡和频道选项卡。
> * 选项卡边距删除更改适用于所有选项卡。 无法选择加入或选择退出更改。
> * 选项卡边距的更改可能会影响依赖 Microsoft Teams 提供其 UI 周围的边距的选项卡。

## <a name="see-also"></a>另请参阅

* [Teams 选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建频道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)
* [移动设备上的选项卡](~/tabs/design/tabs-mobile.md)
