---
title: 设计应用 - 了解应用结构
description: 了解在设计应用时可在Microsoft Teams中自定义的内容和不能自定义的内容。
author: heath-hamilton
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: surbhigupta
keywords: 有线帧频道聊天会议消息扩展移动桌面
ms.openlocfilehash: 8353fa74dce12642e5ca96c85c34dc06fc0da203
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103283"
---
# <a name="understand-the-microsoft-teams-app-structure"></a>了解Microsoft Teams结构

生成应用时，请务必知道可以在Microsoft Teams中自定义哪些内容和不能自定义的内容。 此信息可以帮助你更好地了解你控制的应用体验的哪些部分。

以下线框显示：

* 可以在每个Teams应用功能中自定义的图面 (用粉红色) 勾勒出。
* 每个功能支持的范围。

> [!TIP]
> **范围意味着什么？** 范围是Teams中的一个区域，用户可以在其中使用你的应用。 应用可以有一个或多个范围，包括个人、频道、聊天和会议。

## <a name="personal-apps"></a>个人应用

个人应用提供了一个大画布，用于为单个用户托管你的应用内容。

***支持的范围**：个人*

### <a name="mobile"></a>移动设备

画布是一个 Web 视图，因此可以完全自定义体验。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-mobile.png" alt-text="概念图显示了开发人员可以在移动设备上为个人应用自定义的Teams中的前端区域。" border="false":::

### <a name="desktop"></a>桌面

画布是一个 iframe，因此你可以完全自定义体验。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-desktop.png" alt-text="显示开发人员可以在桌面上为个人应用自定义Teams中前端区域的概念图。" border="false":::

## <a name="tabs"></a>选项卡

选项卡提供一个大画布，用于托管一组用户的应用内容。 可以在共享空间（如频道、聊天和会议邀请）中包含选项卡。

***支持的范围**：频道、聊天、会议*

### <a name="mobile"></a>移动设备

画布是一个 Web 视图，因此可以完全自定义体验。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-mobile.png" alt-text="显示Teams中前端区域的概念图，开发人员可以在移动设备上自定义选项卡。" border="false":::

### <a name="desktop"></a>桌面

画布是一个 iframe，因此你可以完全自定义体验。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-desktop.png" alt-text="显示开发人员可在桌面上自定义选项卡的Teams前端区域的概念图。" border="false":::

## <a name="bots"></a>机器人

机器人是与Teams本机消息传送功能集成的会话应用，因此会为你处理 UI 工作。 从设计的角度来看，我们仍有机会通过自然语言处理 (NLP) 支持和自适应卡片平台来添加个性、自定义功能和丰富的可操作信息。

***支持的范围**：个人、频道、聊天、会议*

### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-mobile.png" alt-text="概念图显示了开发人员可以在移动设备上为机器人自定义的Teams中的前端区域。" border="false":::

### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-desktop.png" alt-text="显示开发人员可为桌面上的机器人自定义的Teams中前端区域的概念图。" border="false":::

## <a name="message-extensions"></a>消息扩展

消息扩展是插入应用内容或在消息上操作而不导航离开对话的快捷方式。 基于操作的消息扩展使你能够更好地控制体验，而Teams处理基于搜索的消息扩展的大部分呈现。

***支持的范围**：个人、频道、聊天、会议*

### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-mobile.png" alt-text="概念图显示了开发人员可以在移动设备上为消息扩展自定义的Teams中的前端区域。" border="false":::

### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-desktop.png" alt-text="显示开发人员可以在桌面上为消息扩展自定义Teams前端区域的概念图。" border="false":::

## <a name="meeting-extensions"></a>会议扩展

会议扩展是用于增强实时会议的应用。 可以在多个方案（包括会议之前、期间和之后）中托管应用内容。

***支持的范围**：会议、聊天*

### <a name="mobile"></a>移动设备

图面是一个 Web 视图，允许你自定义体验，但请记住，在会议期间，这些应用使用深色主题。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-mobile.png" alt-text="概念图显示了开发人员可在移动设备上为会议扩展自定义的Teams前端区域。" border="false":::

### <a name="desktop"></a>桌面

图面是一个 iframe，允许你自定义体验，但请记住，在会议期间，这些应用使用深色主题，并且很窄。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-desktop.png" alt-text="显示开发人员可为桌面上的会议扩展自定义的Teams中的前端区域的概念图。" border="false":::
