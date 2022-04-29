---
title: 打包应用
description: 了解如何打包 Microsoft Teams 应用以进行测试、上传和存储发布。
ms.localizationpriority: high
ms.topic: conceptual
ms.openlocfilehash: ec583ff0998baef7162156c8c5c5c07fde176321
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104089"
---
# <a name="create-a-microsoft-teams-app-package"></a>创建 Microsoft Teams 应用包

需要应用包，但你计划分发 Microsoft Teams 应用。 有效的包是包含以下内容的 ZIP 文件：

* **应用清单**：描述应用的配置方式，包括其功能、所需资源和其他重要属性。
* **应用图标**：每个包都需要应用的颜色和轮廓图标。

## <a name="teams-doesnt-host-your-app"></a>Teams 不托管你的应用

当用户在 Teams 中安装你的应用时，他们安装的应用包仅包含配置文件 (也称为应用清单) 以及应用的图标。 应用的逻辑和数据存储托管在其他地方，如开发期间的本地主机和 Azure Web 服务。 Teams 通过 HTTPS 访问这些资源。

:::image type="content" source="../../assets/images/teams-app-host.png" alt-text="显示 Teams 应用的应用托管插图" border="true":::

## <a name="app-manifest"></a>应用部件清单

应用清单文件必须位于包的顶层，其名称 `manifest.json`。

发布到 Teams 应用商店时，请确保清单引用最新的 [架构](~/resources/schema/manifest-schema.md)。

## <a name="app-icons"></a>应用图标

应用包必须包含应用图标的两个 .png 版本：颜色和大纲版本。

> [!Note]
> 如果应用具有自动程序或消息扩展，则图标也会包含在 Microsoft Azure 机器人服务注册中。

若要使应用通过 Teams 应用商店评审，这些图标必须满足以下大小要求。

### <a name="color-icon"></a>彩色图标

图标的彩色版本在大多数 Teams 方案中显示，必须为 192x192 像素。 图标符号（96x96 像素）可以是任何颜色，但它必须位于实心或完全透明的方形背景上。

Teams 会自动裁剪图标，以在多个方案中显示圆角的正方形，并在机器人方案中显示六边形。 若要在不丢失任何详细信息的情况下裁剪符号，请在符号周围包含 48 像素的填充。

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Teams 颜色图标和设计指南。" border="false":::

### <a name="outline-icon"></a>大纲图标

大纲图标显示在两种方案中：

* 你的应用正在使用并托管在 Teams 左侧应用栏上。
* 当用户固定应用的消息扩展时。

图标必须为 32x32 像素。 它可以是白色，背景透明或透明，背景为白色（不允许使用其他颜色）。 大纲图标不应在符号周围有任何额外的填充。

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teams 大纲图标设计指南。" border="false":::

### <a name="best-practices"></a>最佳做法

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="演示如何设计应用图标的插图。" border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a>执行：遵循精确的大纲图标准则

图标中使用的白色 RGB 值必须为红色：255、绿色：255、蓝色：255。 大纲图标的所有其他部分必须完全透明，alpha 通道设置为 0。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="演示如何不设计应用图标的插图。" border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a>不要：以圆形或圆角方形裁剪

应用包中提交的颜色图标必须为正方形。 不要在图标的圆角。 Teams 会自动调整角半径。

   :::column-end:::
:::row-end:::

#### <a name="dont-copy-other-brands"></a>不要：复制其他品牌

你的图标不得模仿你不拥有的任何受版权保护的产品。 例如，类似于 Microsoft 产品或品牌的设计。

### <a name="examples"></a>示例

下面介绍应用图标在不同 Teams 功能和上下文中的显示方式。

#### <a name="personal-app"></a>个人应用

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="显示应用图标在个人应用中的外观的示例。" border="false":::

#### <a name="bot-channel"></a>机器人（通道）

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="显示应用图标在通道内机器人上的外观的示例。" border="false":::

#### <a name="message-extension"></a>消息扩展

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<文本>" border="false":::

## <a name="next-step"></a>后续步骤

选择计划如何分发应用：

> [!div class="nextstepaction"]
> [在 Teams](~/concepts/deploy-and-publish/apps-upload.md) 中旁加载应用
> [!div class="nextstepaction"]
> [将应用发布到组织](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
> [!div class="nextstepaction"]
> [将应用发布到应用商店](~/concepts/deploy-and-publish/appsource/publish.md)

## <a name="see-also"></a>另请参阅

[使用 Microsoft Teams 开发人员门户管理应用](~/concepts/build-and-test/teams-developer-portal.md)
