---
title: 选项卡边距更改
author: surbhigupta
description: 在本模块中，了解删除选项卡边距如何增强应用生成体验。
ms.topic: reference
ms.localizationpriority: medium
ms.author: lomeybur
ms.openlocfilehash: 270d8499ff917a5b95aeaeaa48ddf11215f77d03
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2022
ms.locfileid: "66190147"
---
# <a name="tab-margin-changes"></a>选项卡边距更改

本文档介绍如何删除Microsoft Teams中所有选项卡周围的边距，从而增强应用生成体验。 这是 2021 年在 Teams 中引入的增强功能。
可以通过删除所有选项卡周围的边距来生成看起来更本机的应用来Teams。 带删除边距的选项卡与Microsoft Teams的 [UI 工具包设计](~/tabs/design/tabs.md)一致。 大多数应用在不带边距的情况下体验增强的外观。

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="Tab wit 和无边距" border="false":::

> [!NOTE]
> 此功能不适用于移动客户端，因为在移动客户端中查看的选项卡没有边距。

## <a name="guidelines"></a>准则

删除选项卡边距会影响使用选项卡的Teams应用。 在这种情况下，可以在需要选项卡设计的位置添加边距。 生产中的应用设计具有额外的填充效果，即由选项卡提供的Teams和边距提供的边距。但是，额外的填充只是临时的，几周后就会消失，只留下应用提供的填充。

## <a name="faq"></a>常见问题

**应用部件版式（如标头栏或任务栏）可以触摸设计的边缘吗？**

是的，这很好，Teams鼓励这种设计。 它可帮助应用感觉原生。

**应用内容（如文本、徽标和图像）是否可以触摸设计左边缘和右边缘？**

否，必须向所有应用内容的左侧和右侧提供自己的填充或边距，以确保它不会触及 UI 的边缘。 如有必要，还可以在选项卡顶部添加边距。

**以前Teams应用的选项卡边距的大小是怎样的？**

* 左右：20 px
* 顶部：16 px
* 底部：0 px

> [!IMPORTANT]
>
> * 所有选项卡都删除了其边距：个人选项卡、 (组) 聊天选项卡、会议选项卡和频道选项卡。
> * 选项卡边距删除更改适用于所有选项卡。 无法选择加入或选择退出更改。
> * 选项卡边距的更改可能会影响依赖Microsoft Teams提供其 UI 周围的边距的选项卡。

## <a name="see-also"></a>另请参阅

* [Teams 选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建频道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)
* [移动设备上的选项卡](~/tabs/design/tabs-mobile.md)
