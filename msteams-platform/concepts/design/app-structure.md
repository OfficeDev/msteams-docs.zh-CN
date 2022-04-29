---
title: 设计应用 - 了解应用结构
description: 了解设计应用时在 Microsoft Teams 中可以自定义的内容和不能自定义的内容。
author: heath-hamilton
ms.topic: conceptual
ms.localizationpriority: high
ms.author: surbhigupta
keywords: 线框频道聊天会议消息扩展移动桌面
ms.openlocfilehash: 5bda408a015c646f993fe2c70efa0b7904b64842
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111379"
---
# <a name="understand-the-microsoft-teams-app-structure"></a>了解Microsoft Teams结构

构建应用时，必须知道 Microsoft Teams 中哪些内容可以自定义，哪些内容不能自定义。 此信息可以帮助你更好地了解可以控制应用体验的哪些部分。

以下线框显示：

* 可以在每个 Teams 应用功能中自定义的图面（用粉红色勾勒出）。
* 每个功能支持的范围。

> [!TIP]
> **范围是什么意思？** 范围是 Teams 中的一个区域，用户可以在其中使用你的应用。 应用可以有一个或多个范围，包括个人、频道、聊天和会议。

## <a name="personal-apps"></a>个人应用

个人应用提供为单个用户托管应用内容的大型画布。

***支持的范围**：个人*

### <a name="mobile"></a>移动设备

画布是一个 Web 视图，因此可以完全自定义体验。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-mobile.png" alt-text="显示开发人员可以为移动设备上的个人应用自定义的 Teams 前端区域的概念图。" border="false":::

### <a name="desktop"></a>桌面

画布是一个 iframe，因此你可以完全自定义体验。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-desktop.png" alt-text="显示开发人员可以为桌面设备上的个人应用自定义的 Teams 前端区域的概念图。" border="false":::

## <a name="tabs"></a>选项卡

选项卡提供为一组用户托管应用内容的大型画布。 可以在共享空间（如频道、聊天和会议邀请）中包含选项卡。

***支持的范围**：频道、聊天、会议*

### <a name="mobile"></a>移动设备

画布是一个 Web 视图，因此可以完全自定义体验。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-mobile.png" alt-text="显示开发人员可以为移动设备上的选项卡自定义的 Teams 前端区域的概念图。" border="false":::

### <a name="desktop"></a>桌面

画布是一个 iframe，因此你可以完全自定义体验。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-desktop.png" alt-text="显示开发人员可以为桌面设备上的选项卡自定义的 Teams 前端区域的概念图。" border="false":::

## <a name="bots"></a>机器人

机器人是与 Teams 原生消息传送功能集成的会话应用，因此 UI 工作已替你处理。 从设计的角度来看，我们仍有机会通过自然语言处理 (NLP) 支持和自适应卡片平台来添加个性化内容、自定义功能和丰富的可操作信息。

***支持的范围**：个人、频道、聊天、会议*

### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-mobile.png" alt-text="显示开发人员可以为移动设备上的机器人自定义的 Teams 前端区域的概念图。" border="false":::

### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-desktop.png" alt-text="显示开发人员可以为桌面设备上的机器人自定义的 Teams 前端区域的概念图。" border="false":::

## <a name="message-extensions"></a>消息扩展

消息扩展是插入应用内容或处理消息而无需离开对话的捷径。 基于操作的消息扩展给予你更多对体验的控制力，而 Teams 则会为基于搜索的消息扩展处理大部分渲染工作。

***支持的范围**：个人、频道、聊天、会议*

### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-mobile.png" alt-text="显示开发人员可以为移动设备上的消息扩展自定义的 Teams 前端区域的概念图。" border="false":::

### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-desktop.png" alt-text="显示开发人员可以为桌面设备上的消息扩展自定义 Teams 前端区域的概念图。" border="false":::

## <a name="meeting-extensions"></a>会议扩展

会议扩展是用于增强实时会议的应用。 你可以通过多个方案（包括会议前、会议期间和会议后）托管应用内容。

***支持的范围**：会议、聊天*

### <a name="mobile"></a>移动设备

图面是一个 Web 视图，允许你自定义体验，但请记住，在会议期间这些应用使用深色主题。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-mobile.png" alt-text="显示开发人员可以为移动设备上的会议扩展自定义的 Teams 前端区域的概念图。" border="false":::

### <a name="desktop"></a>桌面

图面是一个 iframe，允许你自定义体验，但请记住，在会议期间这些应用使用深色主题，并且很窄。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-desktop.png" alt-text="显示开发人员可以为桌面上的会议扩展自定义的 Teams 前端区域的概念图。" border="false":::
