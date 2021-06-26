---
title: 删除选项卡页边距Microsoft Teams
author: surbhigupta
description: 介绍删除制表位将如何增强开发人员的体验。
keywords: 删除边距填充的选项卡
ms.topic: reference
localization_priority: Normal
ms.author: lomeybur
ms.openlocfilehash: 086ce3a375416291a64e3222e698d7e363a651e6
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140570"
---
# <a name="tab-margin-changes"></a>选项卡边距更改

本文档介绍删除文档中所有选项卡的边距Microsoft Teams如何在生成应用时增强开发人员的体验。 这是 2021 年 Microsoft Teams中引入的增强功能。
删除所有选项卡周围的边距将允许开发人员生成看起来更本机的Teams。 这也符合我们的 UI [工具包设计](~/tabs/design/tabs.md)。 大多数应用已看起来更好，没有围绕其体验的边距。 但是，某些选项卡会受此更改的视觉影响，开发人员必须进行必要的更改。

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="选项卡上没有边距" border="false":::

> [!NOTE]
> 此功能不适用于移动客户端，因为移动客户端中查看的选项卡没有边距。 

## <a name="timelines"></a>日程表

* 2021 年 3 月 5 日 - 在 Public 开发者预览版 [中删除边距](~/resources/dev-preview/developer-preview-intro.md)。
* 2021 年 6 月 15 日 - 将在生产中删除边距。

## <a name="guidelines"></a>准则

Microsoft Teams选项卡的应用将受此更改的影响。 开发人员必须切换到 [公共开发者预览版，](~/resources/dev-preview/developer-preview-intro.md) 以确定其选项卡会受到哪些影响，并进行必要的更改。

选项卡开发人员不得依赖Teams选项卡周围的边距。 建议开发人员根据需要在选项卡设计周围添加边距。 生产中的应用设计可能看起来有额外的填充，即由Teams提供的边距和选项卡提供的边距。但是，额外的填充只是临时的，将在几周后消失，仅留下应用提供的填充。

## <a name="faq"></a>常见问题

**应用部件版式（如标题栏或任务栏）是否适合触摸我们设计的边缘？**

是的，这很好，建议这样做。 这有助于应用感觉本机。

**对于文本、徽标和图像等应用内容，触摸设计的左右边缘是否正常？**

否，你必须在所有应用内容的左侧和右侧提供自己的填充或边距，以确保它不会触摸 UI 的边缘。 如果需要，还可以在选项卡顶部添加边距。

**之前应用的边距Teams的大小？**

* 左右：20px
* 顶部：16px
* 底部：0px

> [!IMPORTANT]
> * 删除所有选项卡的边距：个人选项卡、 (组) 聊天选项卡、会议选项卡和频道选项卡。
> * 无法选择加入或选择退出此更改。 它将应用于所有选项卡。
> * 此更改可能会影响依赖其 UI Microsoft Teams提供边距的选项卡。

## <a name="see-also"></a>另请参阅

* [Teams选项卡](~/tabs/what-are-tabs.md)
* [先决条件](~/tabs/how-to/tab-requirements.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建频道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)
* [创建内容页](~/tabs/how-to/create-tab-pages/content-page.md)
* [创建配置页](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [为选项卡创建删除页](~/tabs/how-to/create-tab-pages/removal-page.md)
* [移动设备上的选项卡](~/tabs/design/tabs-mobile.md)
* [获取选项卡的上下文](~/tabs/how-to/access-teams-context.md)
* [具有自适应卡片的生成选项卡](~/tabs/how-to/build-adaptive-card-tabs.md)
* [选项卡链接展开和阶段视图](~/tabs/tabs-link-unfurling.md)
* [创建对话选项卡](~/tabs/how-to/conversational-tabs.md)
