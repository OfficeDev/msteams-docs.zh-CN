---
title: 选项卡边距更改
author: surbhigupta
description: 介绍删除制表位如何增强应用生成体验。
keywords: 删除边距填充的选项卡
ms.topic: reference
localization_priority: Normal
ms.author: lomeybur
ms.openlocfilehash: 4ca8356bddc0e578bc58b38112fb1268302a5ad0e84631bf81864c70cffbcb64
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2021
ms.locfileid: "57704381"
---
# <a name="tab-margin-changes"></a>选项卡边距更改

本文档介绍删除文档中所有选项卡的边距Microsoft Teams增强应用生成体验。 这是 2021 年 Microsoft Teams中引入的增强功能。
可以通过删除所有选项卡周围的边距Teams看起来更本机的应用。 具有已删除边距的选项卡与Microsoft Teams [UI 工具包设计一致](~/tabs/design/tabs.md)。 大多数应用都体验无边距的增强外观。

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="选项卡上没有边距" border="false":::

> [!NOTE]
> 此功能不适用于移动客户端，因为在移动客户端中查看的选项卡没有边距。 

## <a name="guidelines"></a>准则

删除选项卡边距会影响Teams选项卡的应用。 在这种情况下，你可以根据需要在选项卡设计周围添加边距。 生产中的应用设计具有额外的填充效果，即由Teams提供的边距和选项卡提供的边距。但是，额外的填充只是临时的，在几周后会消失，仅留下应用提供的填充。

## <a name="faq"></a>常见问题

**应用部件版式（如标题栏或任务栏）是否适合触摸我们设计的边缘？**

是的，这没有问题，Teams此类设计。 它帮助应用感觉本机。

**对于文本、徽标和图像等应用内容，触摸设计的左右边缘是否正常？**

否，必须在所有应用内容的左右两侧提供自己的填充或边距，以确保它不会触摸 UI 的边缘。 如果需要，还可以在选项卡顶部添加边距。

**之前应用的制表位Teams的大小？**

* 左右：20px
* 顶部：16px
* 底部：0px

> [!IMPORTANT]
> * 删除所有选项卡的边距：个人选项卡、 (组) 聊天选项卡、会议选项卡和频道选项卡。
> * 制表位删除更改适用于所有选项卡。 无法选择加入或选择退出更改。 
> * 选项卡边距的变化可能会影响依赖标签的选项卡Microsoft Teams UI 周围的边距。

## <a name="see-also"></a>另请参阅

* [Teams选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建频道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)
* [移动设备上的选项卡](~/tabs/design/tabs-mobile.md)
