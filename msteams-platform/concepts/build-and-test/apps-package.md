---
title: 打包应用程序
description: 了解如何打包 Microsoft 团队应用程序以进行测试、上载和存储发布。
ms.topic: conceptual
ms.openlocfilehash: 6929375c8d6a1602f01d83d15bfa0dab7f02a664
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605265"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a>为 Microsoft 团队应用程序创建应用程序包

团队中的应用程序由应用程序清单 JSON 文件定义，并捆绑到应用程序包及其图标中。 您需要一个应用程序包来上载和安装团队中的应用程序，并发布到您的业务线应用程序目录或 AppSource。

团队应用程序包是一个 .zip 文件，其中包含以下内容：

* 一个名为的清单文件 `manifest.json` ，它指定应用程序的属性，并指向您的体验所需的资源，如其选项卡配置页或其机器人的 Microsoft 应用 ID 的位置。
* [您的应用程序的颜色和边框图标](#app-icons)。

## <a name="creating-a-manifest"></a>创建指令清单

*团队应用程序 Studio* 可帮助配置你的清单。 它还包含 React 控件库和卡的可配置示例。 请参阅 [App Studio 概述](~/concepts/build-and-test/app-studio-overview.md)。

您的清单文件必须命名为 "manifest.json"，并且必须是上载包的最高级别。 请注意，以前生成的清单和包可能支持较旧版本的架构。 对于团队应用程序，尤其是 AppSource (以前的 Office 应用商店) 提交，必须使用当前 [清单架构](~/resources/schema/manifest-schema.md)。

> [!TIP]
> 指定清单开头的架构，以从代码编辑器中启用 IntelliSense 或类似支持：
>
> `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="app-icons"></a>应用程序图标

您的应用程序包必须包含应用程序图标的两个 PNG 版本（彩色图标和大纲图标）。 为了使您的应用程序通过 AppSource 审阅，这些图标必须满足以下大小要求。

> [!Note]
> 如果你的应用程序具有机器人或邮件扩展，你的图标也将包含在 Microsoft Azure Bot 服务注册中。

### <a name="color-icon"></a>颜色图标

您的图标的颜色版本在大多数团队场景中显示，并且必须为192x192 像素。 您的图标符号 (96x96 像素) 可以是任何颜色或颜色，但它必须位于一个纯或完全透明的方形背景上。

团队将自动裁剪图标，以在多个场景中显示带圆角的方形，在 bot 方案中显示一个六角形。 在符号周围包含48像素的填充，以便可以进行这些裁剪，而不会丢失任何细节。

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="团队颜色图标设计指南。" border="false":::

### <a name="outline-icon"></a>大纲图标

在以下两种情况下，大纲图标将显示：

* 当您的应用程序在团队左侧的应用程序栏上使用并 "已提升"。
* 当用户锁定您的应用程序的邮件扩展时。

图标必须是32x32 像素。 它可以是白色的透明背景，也可以是透明的白色背景 (不允许任何其他颜色) 。 大纲图标周围的符号不应包含任何额外的填充。

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="团队颜色图标设计指南。" border="false":::

### <a name="best-practices"></a>最佳做法

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="演示如何设计应用图标。" border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a>操作：遵循精确的大纲图标准则

您的图标中使用的白色的 RGB 值必须为红色：255、绿色：255、蓝色：255。 大纲图标的所有其他部分必须完全透明，alpha 通道设置为0。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="演示如何不设计应用图标。" border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a>不：在圆形或圆角方形形状中裁剪

您的应用程序包中提交的颜色图标必须是方形。 不四舍五入图标的角。 团队自动调整拐角的半径。

   :::column-end:::
:::row-end:::

### <a name="examples"></a>示例

下面介绍了应用程序图标在不同的团队功能和上下文中的显示方式。

#### <a name="personal-app"></a>个人应用程序

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="示例：显示应用程序图标在个人应用程序中的外观。" border="false":::

#### <a name="bot-channel"></a>Bot (频道) 

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="示例：显示应用程序图标在频道内的机器人的外观。" border="false":::

#### <a name="messaging-extension"></a>消息扩展

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<alt 文本>" border="false":::
