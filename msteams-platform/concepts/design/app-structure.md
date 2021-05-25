---
title: 设计应用 - 了解应用结构
description: 了解在设计应用时，可以在 Microsoft Teams自定义哪些内容。
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: bf84ad1d52cf46e9242bf4122dc5e900461ab806
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631261"
---
# <a name="understand-the-microsoft-teams-app-structure"></a>了解Microsoft Teams结构

生成应用时，了解在应用中可以自定义和不能自定义Microsoft Teams。 此信息可帮助你更好地了解你控制的应用体验的哪些部分。

以下框架图显示：

* 你可以在每个应用功能中自定义Teams以蓝色 (轮廓的) 。
* 每个功能支持的范围。

> [!NOTE]
> **范围意味着什么？** 范围是用户Teams应用中的一个区域。 应用可以具有一个或多个范围，包括个人、频道、聊天和会议。

## <a name="personal-apps"></a>个人应用

个人应用提供一个大型画布来为单个用户托管你的应用内容。 画布是 iframe，因此你可以完全自定义体验。

***支持的范围**：个人*

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps.png" alt-text="概念图像，显示开发人员可自定义Teams应用中的前端区域。" border="false":::

## <a name="tabs"></a>选项卡

选项卡提供了一个大型画布，用于为一组用户托管你的应用内容。 可以在共享空间（如频道、聊天和会议邀请）中包括选项卡。 画布是 iframe，因此你可以完全自定义体验。

***支持的范围**：频道、聊天、会议*

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs.png" alt-text="显示开发人员可以自定义选项卡的Teams区域的概念图像。" border="false":::

## <a name="bots"></a>机器人

自动程序是对话应用，Teams本机消息传递功能集成，因此会处理 UI 工作。 从设计的角度来看，仍有机会使用我们的自然语言处理 (NLP) 和自适应卡片平台添加个性、自定义功能和丰富且可操作的信息。

***支持的范围**：个人、频道、聊天、会议*

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots.png" alt-text="概念图像，显示开发人员可以自定义Teams中的前端区域。" border="false":::

## <a name="messaging-extensions"></a>消息扩展

消息传递扩展是插入应用内容或在离开对话的情况下对消息操作快捷方式。 基于操作的邮件扩展可让你更加控制体验，Teams处理大部分基于搜索的邮件扩展呈现内容。

***支持的范围**：个人、频道、聊天、会议*

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions.png" alt-text="概念图像，显示开发人员可Teams邮件扩展自定义的前端区域。" border="false":::

## <a name="meeting-extensions"></a>会议扩展

会议扩展是增强实时会议的应用。 可以在多种方案中托管应用内容，包括会议之前、期间和之后。 图面是 iframe，可让你自定义体验，但请记住，这些应用在会议期间深色且较窄。

***支持的范围**：会议、聊天*

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions.png" alt-text="概念图像，显示开发人员可针对会议Teams自定义的前端区域。" border="false":::
