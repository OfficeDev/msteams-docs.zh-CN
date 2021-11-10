---
title: 应用开发基础概述
author: heath-hamilton
description: 介绍应用平台开发Teams概念，如应用功能和入口点、了解用例以及将其映射到应用功能以及规划应用。
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
keywords: 入口点可扩展性用例设备功能
ms.openlocfilehash: 63a11c949a56bf024632efc7cad5ef38ce918c2b
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889270"
---
# <a name="microsoft-teams-app-development-fundamentals"></a>Microsoft Teams应用开发基础

Microsoft Teams应用基础为创建自定义应用提供Teams方向。 你可以识别规划应用所需的Teams框架。 本文档可帮助你了解用户-应用通信，并找出你需要使用的应用图面类型或你的应用在进程中可能需要的 API。 获得一些灵感，以在集成应用体验时融入交互性Teams。

## <a name="capabilities-and-entry-points"></a>功能和入口点

可以通过多种方式扩展Teams应用程序。 为了能够扩展你的应用，你必须了解在协作空间中工作的所有核心功能和入口点。 你可以尝试构建应用的扩展点。 重要应用项目组件可帮助你正确配置应用页面。 Teams应用可以[有多个功能和](../concepts/capabilities-overview.md)[入口点](../concepts/extensibility-points.md)。

## <a name="understand-your-use-cases"></a>了解用例

你可以识别用户问题并确定用户面临的一些常见问题的解答。 可以通过查找Teams组合来构建你的应用，以满足用户的需求。 [了解用例](../concepts/design/understand-use-cases.md) 以了解最终用户如何与你的应用交互。 了解如何了解用户及其问题。 回答的一些常见问题如下所示：

* 是否需要身份验证？
* 你的应用要解决什么问题？
* Who是应用的最终用户吗？
* 载入体验应该如何以及应用还可以执行哪些操作？

## <a name="map-your-use-cases-to-teams-app-capabilities"></a>将用例映射到Teams功能

[映射用例涵盖了](../concepts/design/map-use-cases.md) 一些常见方案以及如何选择应用的功能。 提供了在外部系统中共享应用和协作处理项目的信息。 您还可以了解如何启动工作流和向用户发送通知。 获取有关开始位置、如何与用户社交、对话机器人以及组合多个功能的其他提示。

## <a name="plan-responsive-tabs-for-teams-mobile"></a>规划 Teams 移动版的响应式选项卡
[Plan responsive tabs for Teams mobile](../concepts/design/plan-responsive-tabs-for-teams-mobile.md)涵盖了常见方案，有助于规划适用于移动Teams应用。 文档指南将指导如何对移动设备上的应用进行规范。 还可以了解应用应用的不同Teams类型。

## <a name="integrate-device-capabilities"></a>集成设备功能

Microsoft Teams平台持续增强开发人员功能，以与内置第一方体验保持一致。 借助增强的 Teams 平台，合作伙伴可以使用 Microsoft Teams JavaScript 客户端 SDK 中提供的专用 API 访问和集成本机设备功能，例如相机、QR 或条形码扫描仪、照片库、麦克风和位置。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [了解Teams应用功能](capabilities-overview.md)

## <a name="see-also"></a>另请参阅

* [将 Web 应用与 Teams](../samples/integrating-web-apps.md)
* [生成首个Microsoft Teams应用](../build-your-first-app/build-first-app-overview.md)
