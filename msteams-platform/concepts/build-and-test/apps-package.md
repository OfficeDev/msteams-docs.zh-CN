---
title: 打包应用程序
description: 了解如何打包应用程序以在 Microsoft 团队中进行测试、上载和发布
keywords: 团队应用程序打包
ms.topic: conceptual
ms.openlocfilehash: d2d49dcc5c4ccada0a75de5df6fda29a60e809f6
ms.sourcegitcommit: 560bf433129c16888135879e2703dbdeb38ec99f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "48397699"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a>为 Microsoft 团队应用程序创建应用程序包

团队中的应用程序由应用程序清单 JSON 文件定义，并捆绑到应用程序包及其图标中。 您需要一个应用程序包来上载和安装团队中的应用程序，并发布到您的业务线应用程序目录或 AppSource。

团队应用程序包是一个 .zip 文件，其中包含以下内容：

* 一个名为 "manifest.json" 的清单文件，它指定您的应用程序的属性，并指向您的体验所需的资源，如其选项卡配置页或其机器人的 Microsoft 应用 ID 的位置。
* 透明的 "大纲" 图标和完整的 "颜色" 图标。 有关详细信息，请参阅本主题后面的 [图标](#icons) 。

## <a name="creating-a-manifest"></a>创建指令清单

*团队应用程序 Studio* 可帮助配置你的清单。 它还包含 React 控件库和卡的可配置示例。 请参阅 [App Studio 概述](~/concepts/build-and-test/app-studio-overview.md)。

您的清单文件必须命名为 "manifest.json"，并且必须是上载包的最高级别。 请注意，以前生成的清单和包可能支持较旧版本的架构。 对于团队应用程序，尤其是 AppSource (以前的 Office 应用商店) 提交，必须使用当前 [清单架构](~/resources/schema/manifest-schema.md)。

> [!TIP]
> 指定清单开头的架构，以从代码编辑器中启用 IntelliSense 或类似支持：
>
> `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",`

## <a name="icons"></a>图标

> [!Note]
> 如果您的应用程序包含机器人或邮件扩展，则使用的图标将是上载到 bot 框架中的 bot 注册的图标。

Microsoft 团队需要两个图标来满足你的应用程序体验，才能在产品中使用。 图标必须包含在包中，并通过清单中的相对路径引用。 每个路径的最大长度为2048个字节，图标的格式为 .png。

### <a name="color"></a>颜色

该 `color` 图标在 Microsoft 团队中 (在应用程序和选项卡库、bot、flyouts 等) 中。 此图标应为192x192 像素。 您的图标可以是任何颜色 (或颜色) ，但背景应为您的品牌化的强调文字颜色。 它还应在图标周围具有少量的填充，以适应图标的 bot 版本的六角裁剪。

### <a name="outline"></a>outline

`outline`在以下位置使用图标：用户已将其标记为 "收藏夹" 的应用栏和邮件扩展。 此图标必须为32x32 像素。 大纲图标必须仅包含白色和透明度 (不) 其他颜色。 图标可以是白色背景，也可以是透明背景。 大纲图标周围的图标周围不应有额外的填充，应尽可能紧密地裁剪，同时仍保持32x32 尺寸。 以下是几个很棒的示例：

> [!TIP]
>  * 颜色必须是 RGB 中的 "白色"， (红色：255，绿色：255，蓝色： 255) 。
>  * 图标的所有其他部分都应是透明的。
>  * 对于传递，小图标必须为全透明，Alpha 通道为0，任何其他值都将失败。

![示例大纲图标](~/assets/images/icons/sample20x20s.png)

例如，假设您的公司是 Contoso。 您可以提交两个图标：

![图标展示](~/assets/images/framework/framework_submit_icon.png)

以下是图标在 UI 中的显示方式：

#### <a name="bot-and-chiclet-in-channel-view"></a>通道视图中的 Bot 和 chiclet

![Bot 和 chiclet UX](~/assets/images/icons/botandchiclet.png)

#### <a name="flyout"></a>弹出

![示例 Contoso 浮出控件](~/assets/images/icons/flyout.png)

#### <a name="app-bar-and-home-screen"></a>应用栏和主屏幕

![示例 Contoso 应用程序栏 homescreen](~/assets/images/icons/appbarhomescreen.png)
