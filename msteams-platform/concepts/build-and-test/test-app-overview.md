---
title: 测试应用概述
description: 介绍在 Microsoft 365 中测试和调试 Teams 自定义应用的过程
ms.topic: how-to
ms.localizationpriority: high
keywords: 配置 Microsoft 365 租户 Teams 上传测试应用
ms.openlocfilehash: 98c00ece54e1654570556bac122e6760b283b73f
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111526"
---
# <a name="test-your-app"></a>测试应用

将应用与 Microsoft Teams 集成后，必须在发布应用之前对其进行测试。 最终目标是为应用获取尽可能多的用户，因此，请确保在用户可以使用的多个设备上测试应用。 为了测试应用，请执行以下操作：

* 准备 Microsoft 365 租户。
* 选择要测试和调试应用的工作区。
* 将测试数据添加到 Microsoft 365 租户。

## <a name="prepare-your-microsoft-365-tenant"></a>准备 Microsoft 365 租户

在开始测试应用之前，请准备 Microsoft 365 测试租户，启用自定义 Teams 应用以便上传应用。 必须注册 Microsoft 365 开发人员计划，并管理组织的 Teams 设置。 设置开发人员订阅，并通过[准备 Microsoft 365 租户](~/concepts/build-and-test/prepare-your-o365-tenant.md)进行配置。

## <a name="test-and-debug"></a>测试和调试

若要测试和调试应用，必须至少创建一个工作区。 可以选择测试设置，例如本地主机或基于云的主机，来测试和调试应用。 我们提供了可加载和运行应用体验的 Teams 应用调试指南。 有关详细信息，请参阅[选择设置并运行 Microsoft Teams 应用](~/concepts/build-and-test/debug.md)。

在本地测试机器人。 有关详细信息，请参阅[使用 IDE 在本地调试机器人](~/bots/how-to/debug/locally-with-an-ide.md)。 还可以使用[检查中间件](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)和[自适应工具](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true)调试机器人。

若要在运行时查看控制台日志，查看或修改 html、css 和网络请求，请将断点添加到 JavaScript 代码，并执行交互式调试访问 DevTools。 有关详细信息，请参阅[访问 Teams 选项卡的 DevTools](~/tabs/how-to/developer-tools.md)。

## <a name="add-test-data-to-your-microsoft-365-tenant"></a>将测试数据添加到 Microsoft 365 租户

将测试数据添加到 Microsoft 365 测试租户。 有关详细信息，请参阅[将测试数据添加到 Office 365 测试租户](~/concepts/build-and-test/test-data.md)，并在开始上传测试数据之前完成所有先决条件。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [准备 Microsoft 365 租户](~/concepts/build-and-test/prepare-your-o365-tenant.md)

## <a name="see-also"></a>另请参阅

* [调试选项卡](~/tabs/how-to/developer-tools.md)
* [调试机器人](~/bots/how-to/debug/locally-with-an-ide.md)
* [测试 RSC 权限](~/graph-api/rsc/test-resource-specific-consent.md)
