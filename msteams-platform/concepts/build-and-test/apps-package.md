---
title: 打包应用
description: 了解如何打包 Microsoft Teams 应用以进行测试、上传和应用商店发布。
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: c8341f3d83b5e6610e44276d6732affa1d1c1e91
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020138"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a>为 Microsoft Teams 应用创建应用包

Teams 中的应用由应用清单 JSON 文件定义，并捆绑在带图标的应用包中。 你需要一个应用包，以在 Teams 中上传和安装应用，并发布到业务线应用目录或 AppSource。

Teams 应用包是包含以下内容的 .zip 文件：

* 一个名为 的清单文件，它指定应用的属性，并指向体验所需的资源，例如选项卡配置页的位置或其自动 `manifest.json` 程序 Microsoft 应用 ID 的位置。
* [应用的颜色和大纲图标](#app-icons)。

## <a name="creating-a-manifest"></a>创建指令清单

**Teams App Studio** 可帮助配置清单。 它还包含 React 控件库和卡的可配置示例。 有关详细信息，请参阅 [App Studio 概述](~/concepts/build-and-test/app-studio-overview.md)。

清单文件必须命名为"manifest.js打开"，并且位于上传程序包的顶层。 请注意，之前构建的清单和包可能支持较旧版本的架构。 对于 Teams 应用，尤其是 AppSource (Office 应用商店) 提交，必须使用当前的 [清单架构](~/resources/schema/manifest-schema.md)。

> [!TIP]
> 在清单的开头指定架构，以IntelliSense代码编辑器提供类似支持：
>
> `"$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.9/MicrosoftTeams.schema.json",`
 
## <a name="app-icons"></a>应用图标

应用包必须包含应用图标的两个 PNG 版本，即颜色图标和大纲图标。 若要使应用通过 AppSource 评价，这些图标必须满足以下大小要求。

> [!Note]
> 如果你的应用具有自动程序或消息传递扩展，则你的图标也将包含在 Microsoft Azure 自动程序服务注册中。

### <a name="color-icon"></a>颜色图标

图标的颜色版本在大多数 Teams 方案中显示，并且必须为 192x192 像素。 图标符号 (96x96 像素) 可以是任何颜色，但它必须位于纯色或完全透明的方形背景上。

Teams 自动将图标进行缩小，以在多个方案中显示圆角的正方形，以及自动程序方案中的六边形。 在符号周围包含 48 像素的填充，以便进行这些种种时不会丢失任何详细信息。

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Teams 颜色图标和设计指南。" border="false":::

### <a name="outline-icon"></a>大纲图标

大纲图标在两种方案中显示：

* 当你的应用在使用中并且 Teams 左侧的应用栏上"已打开"时。
* 当用户固定你的应用的消息扩展时。

图标必须为 32x32 像素。 它可以是白色且具有透明背景，或者使用白色背景 (不允许使用任何其他颜色) 。 大纲图标不应在符号周围有任何额外的填充。

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teams 大纲图标设计指南。" border="false":::

### <a name="best-practices"></a>最佳做法

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="显示如何设计应用图标的图示。" border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a>应做：遵循精确的大纲图标指南

图标中使用的白色 RGB 值必须为红色：255、绿色：255、蓝色：255。 大纲图标的所有其他部分必须完全透明，alpha 通道设置为 0。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="显示如何不设计应用图标的图示。" border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a>不：以圆形或圆角正方形形状裁剪

在应用包中提交的颜色图标必须为正方形。 不要四角舍入图标。 Teams 自动调整角半径。

   :::column-end:::
:::row-end:::

### <a name="examples"></a>示例

下面将说明应用图标在不同的 Teams 功能和上下文中的显示方式。

#### <a name="personal-app"></a>个人应用

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="显示应用图标在个人应用中的外观的示例。" border="false":::

#### <a name="bot-channel"></a>自动 (频道) 

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="显示应用图标在频道内的自动程序上的外观的示例。" border="false":::

#### <a name="messaging-extension"></a>消息传递扩展

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<替换文字>" border="false":::
