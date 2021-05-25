---
title: 分发应用
description: 了解如何使用开发人员门户为用户分配Microsoft Teams。
keywords: 开发人员门户团队入门
localization_priority: Normal
ms.topic: Conceptual
ms.openlocfilehash: d1d098b295492a7dc3b691db4625307b6c3170ce
ms.sourcegitcommit: d972953994e405c6afc42e4d4a76b48c6d4cfb5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52635076"
---
# <a name="distribute-your-apps"></a>分发应用

## <a name="distribute"></a>分散对齐

定义完应用程序后，"分发"部分允许您将应用的定义导出为 zip 文件，然后可以共享该文件并将其上载到 Teams 客户端进行测试。 单击"导出"以 **appname.zip** 下载默认下载目录中的 zip 文件。

:::image type="content" source="~/assets/images/tdp/tdp_distribute_1.png" alt-text="Screenshot showing the Distribute page of Teams Developer Portal.":::

### <a name="manifest"></a>清单

清单介绍了如何配置应用，包括应用的功能、必需资源以及其他重要属性。 有关详细信息 [，请参阅](~/resources/schema/manifest-schema.md) 清单架构。

### <a name="flights"></a>Flights

控制获取应用更新的人。 例如，你可以向 Microsoft 员工发布更新，以在将 Bug 发布给公众之前识别和修复 Bug。 选择 **"新建请求"** 以创建新的航班请求。

### <a name="publish-to-org"></a>发布到组织

使你的应用可供组织中的人员使用。IT 管理员批准后，你的应用将在"专为Teams构建的应用>下特别推荐。

### <a name="publish-your-app-to-teams-store"></a>将应用发布到Teams应用商店

在项目主页上，你可以将应用上载到团队、将应用提交到公司自定义应用商店供你组织的用户使用，或将应用提交到所有 Teams 用户的应用源。 IT 管理员将审阅这些提交。 可返回" **发布** 页面，检查提交状态，并了解应用是否已获 IT 管理员批准或拒绝。这也是提交应用更新或取消当前任何活动提交的地方。

## <a name="see-also"></a>另请参阅

* [开发人员Teams概述](~/concepts/build-and-test/teams-developer-portal.md)
* [配置Teams开发人员门户](~/concepts/tdp-configuration.md)
* [开发人员门户Teams中的工具](~/concepts/tdp-tools.md)