---
title: 测试应用概述
description: 介绍在自定义应用中测试和Teams自定义Microsoft 365
ms.topic: how-to
ms.localizationpriority: medium
keywords: 配置Microsoft 365测试Teams租户配置
ms.openlocfilehash: 9cbb650fc248d12fc310cc8b1aaaded7b9a87140
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889263"
---
# <a name="test-your-app"></a>测试应用

将应用与Microsoft Teams集成后，必须在发布应用之前测试它。 因此，最终目标是为你的应用获取数量多的用户，因此，请确保在用户可以使用的多个设备上测试该应用。 对于测试你的应用：

* 准备Microsoft 365租户。
* 选择一个工作区来测试和调试你的应用。
* 将测试数据添加到Microsoft 365租户。

## <a name="prepare-your-microsoft-365-tenant"></a>准备 Microsoft 365 租户

在开始测试应用之前，请Microsoft 365测试租户并启用自定义Teams应用，以便上传应用。 必须注册开发人员Microsoft 365并管理组织的 Teams 设置。 设置开发人员订阅并通过准备你的租户Microsoft 365[订阅](~/concepts/build-and-test/prepare-your-o365-tenant.md)。

## <a name="test-and-debug"></a>测试和调试

若要测试和调试应用，必须创建至少一个工作区。 可以选择测试设置，如本地主机或基于云的主机，以测试和调试应用。 提供了调试Teams应用以加载和运行应用体验的指南。 有关详细信息，请参阅[选择设置并运行Microsoft Teams应用](~/concepts/build-and-test/debug.md)。

在本地测试机器人。 有关详细信息，请参阅使用 [IDE 在本地调试机器人](~/bots/how-to/debug/locally-with-an-ide.md)。 您还可以使用检查中间件和自适应 [工具](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) 调试 [自动程序](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true)。 

若要查看控制台日志，请在运行时查看或修改 html、css 和网络请求，向 JavaScript 代码添加断点，并执行交互式调试访问 DevTools。 有关详细信息，请参阅访问开发人员工具[Teams选项卡](~/tabs/how-to/developer-tools.md)。 

## <a name="add-test-data-to-your-microsoft-365-tenant"></a>将测试数据添加到Microsoft 365租户

将测试数据添加到Microsoft 365租户。 有关详细信息，请参阅[将测试数据添加到](~/concepts/build-and-test/test-data.md)Office 365 测试租户，并完成所有先决条件，然后再开始上载测试数据。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [准备 Microsoft 365 租户](~/concepts/build-and-test/prepare-your-o365-tenant.md)

## <a name="see-also"></a>另请参阅

* [调试选项卡](~/tabs/how-to/developer-tools.md)
* [调试机器人](~/bots/how-to/debug/locally-with-an-ide.md)
* [测试 RSC 权限](~/graph-api/rsc/test-resource-specific-consent.md)
