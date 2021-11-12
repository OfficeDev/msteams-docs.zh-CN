---
title: 打包应用
description: 了解如何打包应用Microsoft Teams、上传和应用商店发布。
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: 1879bcab13ff9ba355bcebdf68e4c8c061f153a1
ms.sourcegitcommit: 1431dfe08d5a19a63dbf1542a2e6c661e4dd7fc1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2021
ms.locfileid: "60949073"
---
# <a name="create-a-microsoft-teams-app-package"></a>创建Microsoft Teams应用包

你需要应用包，但计划分配你的Microsoft Teams包。 有效包是包含以下内容的 ZIP 文件：

* **应用** 清单 ：描述如何配置应用，包括应用的功能、必需资源以及其他重要属性。
* **应用图标**：每个程序包都需要应用的颜色和轮廓图标。

## <a name="app-manifest"></a>应用部件清单

应用清单文件必须位于包的顶级，名称为 `manifest.json` 。 

发布到应用商店Teams，请确保清单对最新架构[的引用](~/resources/schema/manifest-schema.md)。

## <a name="app-icons"></a>应用图标

应用包必须包含应用图标的两个 PNG 版本：颜色和大纲版本。

> [!Note]
> 如果你的应用具有自动程序或消息传递扩展，你的图标也将包含在你的自动Microsoft Azure注册中。

若要使应用通过Teams评价，这些图标必须满足以下大小要求。

### <a name="color-icon"></a>颜色图标

图标的彩色版本在大多数 Teams 方案中显示，必须为 192x192 像素。 图标符号 (96x96 像素) 可以是任何颜色，但它必须位于纯色或完全透明的方形背景上。

Teams自动种图标，以在多个方案中显示圆角的正方形，以及自动程序方案中的六边形。 若要裁剪符号而不丢失任何细节，请在你的符号周围包含 48 像素的填充。

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Teams颜色图标和设计指南。" border="false":::

### <a name="outline-icon"></a>大纲图标

大纲图标在两种方案中显示：

* 当你的应用在使用中时，在应用栏的左侧应用栏上Teams。
* 当用户固定你的应用的消息扩展时。

图标必须为 32x32 像素。 它可以是白色且具有透明背景，或者使用白色背景 (不允许使用任何其他颜色) 。 大纲图标不应在符号周围有任何额外的填充。

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teams大纲图标设计指南。" border="false":::

### <a name="best-practices"></a>最佳实践

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="显示如何设计应用图标的图示。" border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a>应做：遵循精确的大纲图标指南

图标中使用的白色 RGB 值必须为红色：255、绿色：255、蓝色：255。 大纲图标的所有其他部分必须完全透明，alpha 通道设置为 0。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="显示如何不设计应用图标的图示。" border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a>不：以圆形或圆角正方形形状裁剪

在应用包中提交的颜色图标必须为正方形。 不要四角舍入图标。 Teams自动调整角半径。

   :::column-end:::
:::row-end:::

#### <a name="dont-copy-other-brands"></a>不要：复制其他品牌

图标不得模仿你未拥有的任何受版权保护的产品。 例如，类似于 Microsoft 产品或品牌的设计。

### <a name="examples"></a>示例

下面是应用图标在不同功能和上下文中Teams的方式。

#### <a name="personal-app"></a>个人应用

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="显示应用图标在个人应用中的外观的示例。" border="false":::

#### <a name="bot-channel"></a>自动 (频道) 

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="显示应用图标在频道内的自动程序上的外观的示例。" border="false":::

#### <a name="messaging-extension"></a>消息传递扩展

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<替换文字>" border="false":::

## <a name="next-step"></a>后续步骤

选择计划如何分配应用：

> [!div class="nextstepaction"]
> [在应用程序中旁加载Teams](~/concepts/deploy-and-publish/apps-upload.md)
> [!div class="nextstepaction"]
> [将应用发布到组织](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
> [!div class="nextstepaction"]
> [将应用发布到应用商店](~/concepts/deploy-and-publish/appsource/publish.md)

## <a name="see-also"></a>另请参阅

[使用开发人员门户管理应用Microsoft Teams](~/concepts/build-and-test/teams-developer-portal.md)