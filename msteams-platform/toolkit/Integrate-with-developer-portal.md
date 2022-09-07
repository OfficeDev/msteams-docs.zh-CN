---
title: 与 Teams 工具包中的开发人员门户集成
author: zyxiaoyuer
description: 在本模块中，了解如何与 Teams 工具包中的开发人员门户集成
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
ms.openlocfilehash: b54e833f5c8292c0b426e859e63d858102860a47
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617118"
---
# <a name="integrate-with-developer-portal"></a>与开发人员门户集成

可以在 Teams 工具包中的开发人员门户中配置和管理应用。

## <a name="to-publish-app-using-developer-portal"></a>使用开发人员门户发布应用

以下步骤可帮助你在开发人员门户中发布应用：

1. 选择 **部署** 下 **的 Teams 开发人员门户**。

    :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/dev-portal-ttk.png" alt-text="Teams 开发人员门户":::

   现在，开发人员门户将在浏览器中打开。

1. 使用相应的帐户登录到 [Teams 开发人员门户](https://dev.teams.microsoft.com) 。
1. 在 zip 中导入应用包，选择 **“应用****导入”** > 应用。
1. 选择 **“发布** > **到组织**”。

## <a name="to-update-manifest-file-and-app-package"></a>更新清单文件和应用包

如果有任何与 Teams 应用的清单文件相关的更改，可以更新清单并再次发布 Teams 应用。 若要手动发布 Teams 应用，可以利用 [Teams 版开发人员门户](https://dev.teams.microsoft.com/home)。

1. 使用相应的帐户登录到 [Teams 开发人员门户](https://dev.teams.microsoft.com) 。
1. 在 zip 中导入应用包，选择 **“应用****导入”** > 应用。<br>
   需要替换之前上传到开发人员门户的应用。
1. 若要发布应用，请选择 **“发布** > **到组织**”。

可以在开发人员门户中执行以下配置：

* **基本信息**：本部分显示并允许你编辑应用名称、应用 ID、说明、版本、开发人员信息、应用 URL、应用程序 (客户端) ID 和 Microsoft 合作伙伴网络 ID。
* **品牌**：此页显示应用图标详细信息。
* **应用功能**：可将以下功能添加到应用：
  * 个人应用
  * Bot
  * Connector
  * 现场
  * 组和通道应用
  * 消息传递扩展
  * 会议扩展
  * 活动源通知
* **权限**：本部分允许为应用授予设备权限、团队权限、聊天或会议权限以及用户权限。
* **单一登录**：可以将应用配置为使用单一登录 (SSO) 对用户进行身份验证。
* **语言**：可以设置或更改应用的语言。
* **域**：可以在 Teams 客户端中添加域以加载应用 (例如：*.example.com) 。

## <a name="see-also"></a>另请参阅

* [Teams 开发人员门户](../concepts/build-and-test/teams-developer-portal.md)
* [在开发人员门户中管理应用](../concepts/build-and-test/manage-your-apps-in-developer-portal.md)
