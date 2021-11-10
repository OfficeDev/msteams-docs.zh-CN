---
title: 设计应用 - 了解应用结构
description: 了解在设计应用时，可以在 Microsoft Teams自定义哪些内容。
author: heath-hamilton
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: surbhigupta
keywords: 线框频道聊天会议消息传递扩展移动桌面
ms.openlocfilehash: 3d63cc705ac567b0b19db2e3caf4a84420dae9bd
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2021
ms.locfileid: "60887572"
---
# <a name="understand-the-microsoft-teams-app-structure"></a>了解Microsoft Teams结构

生成应用时，了解在应用中可以自定义和不能自定义Microsoft Teams。 此信息可帮助你更好地了解你控制的应用体验的哪些部分。

以下框架图显示：

* 你可以在每个应用功能中自定义Teams， (粉色) 。
* 每个功能支持的范围。

> [!TIP]
> **范围意味着什么？** 范围是用户Teams应用中的一个区域。 应用可以具有一个或多个范围，包括个人、频道、聊天和会议。

## <a name="personal-apps"></a>个人应用

个人应用提供一个大型画布来为单个用户托管你的应用内容。

***支持的范围**：个人*

### <a name="mobile"></a>移动设备

画布是 Web 视图，因此你可以完全自定义体验。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-mobile.png" alt-text="显示开发人员可以针对移动版个人Teams自定义的前端区域的概念图像。" border="false":::

### <a name="desktop"></a>桌面

画布是 iframe，因此你可以完全自定义体验。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-desktop.png" alt-text="概念图像，显示开发人员可Teams桌面应用自定义的前端区域。" border="false":::

## <a name="tabs"></a>选项卡

选项卡提供了一个大型画布，用于为一组用户托管你的应用内容。 可以在共享空间（如频道、聊天和会议邀请）中包括选项卡。

***支持的范围**：频道、聊天、会议*

### <a name="mobile"></a>移动设备

画布是 Web 视图，因此你可以完全自定义体验。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-mobile.png" alt-text="概念图像，显示开发人员可Teams移动选项卡自定义的前端区域。" border="false":::

### <a name="desktop"></a>桌面

画布是 iframe，因此你可以完全自定义体验。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-desktop.png" alt-text="概念图像，显示开发人员可自定义Teams桌面选项卡的前端区域。" border="false":::

## <a name="bots"></a>机器人

自动程序是对话应用，Teams本机消息传递功能集成，因此会处理 UI 工作。 从设计的角度来看，仍有机会使用我们的自然语言处理功能添加个性、自定义功能和丰富的可操作信息， (NLP) 和自适应卡片平台。

***支持的范围**：个人、频道、聊天、会议*

### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-mobile.png" alt-text="概念图像，显示开发人员可以针对Teams自动程序自定义的前端区域。" border="false":::

### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-desktop.png" alt-text="概念图像，显示开发人员可在Teams自动程序自定义的前端区域。" border="false":::

## <a name="messaging-extensions"></a>消息扩展

消息传递是插入应用程序内容或对消息采取行动的快捷方式，而无需从对话中导航。 基于操作的邮件扩展可让你更加控制体验，Teams处理大部分基于搜索的邮件扩展呈现内容。

***支持的范围**：个人、频道、聊天、会议*

### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-mobile.png" alt-text="概念图像，显示开发人员可以针对Teams邮件扩展自定义的前端区域。" border="false":::

### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-desktop.png" alt-text="概念图像，显示开发人员可自定义Teams桌面消息扩展的前端区域。" border="false":::

## <a name="meeting-extensions"></a>会议扩展

会议扩展是增强实时会议的应用。 可以在多种方案中托管应用内容，包括会议之前、期间和之后。

***支持的范围**：会议、聊天*

### <a name="mobile"></a>移动设备

图面是 Web 视图，可让你自定义体验，但请记住，在会议期间，这些应用使用深色主题。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-mobile.png" alt-text="概念图像，显示开发人员可Teams移动版会议扩展自定义的前端区域。" border="false":::

### <a name="desktop"></a>桌面

图面是 iframe，可让你自定义体验，但请记住，在会议期间，这些应用使用深色主题且较窄。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-desktop.png" alt-text="概念图像，显示开发人员可Teams桌面会议扩展自定义的前端区域。" border="false":::
