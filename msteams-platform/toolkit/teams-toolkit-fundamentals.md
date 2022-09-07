---
title: Teams 工具包概述
author: zyxiaoyuer
description: 在本模块中，了解 Teams 工具包、Teams 工具包安装和 Teams 工具包的用户旅程
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
ms.openlocfilehash: b614c73a9d15b058dcd01bb26b15bf35bd3030ce
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616885"
---
# <a name="teams-toolkit-overview"></a>Teams 工具包概述

Teams 工具包允许你直接从Visual Studio Code创建、调试和部署 Teams 应用。使用工具包进行应用开发具有以下优势：

* 集成标识
* 对云存储的访问权限
* 来自 Microsoft Graph 的数据
* 采用零配置方法的 Azure 和 Microsoft 365 服务。

对于 Teams 应用开发，类似于适用于 Visual Studio 的 Teams 工具包，可以使用 [CLI 工具](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md)，其中包括工具包 `teamsfx`。

## <a name="user-journey-of-teams-toolkit"></a>Teams 工具包的用户旅程

Teams 工具包可自动执行手动工作，并提供 Teams 和 Azure 资源的强大集成。 下图显示了 Teams 工具包用户旅程：

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png" alt-text="Teams 工具包的用户旅程" lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png":::

此旅程的主要里程碑包括：

1. 首先创建新项目或尝试示例 Teams 应用。
1. 根据需要添加功能或编辑清单文件。
1. 使用 Microsoft 365 帐户构建和调试 Teams 应用。
1. 使用 Azure 帐户预配应用并将其部署到云。
1. 将应用发布到 Teams。

下表可帮助你在Visual Studio Code中大致了解 Teams 工具包：

| 流程 | 说明 |
| ---- | ---- |
| 安装 Teams 工具包 | 可以通过两种方式安装 Teams 工具包： <br> - 使用Visual Studio Code <br> - 使用Visual Studio Code市场|
| 支持生成环境 | 你有两种不同类型的环境： <br> - Javascript 或 Typescript <br> - SPFx |
| 对应用类型和 Azure 函数的支持 | 有两种不同类型的应用： <br> - 基于功能的应用，如选项卡、机器人、消息扩展  <br> - 基于方案的 Teams 应用，例如通知机器人、命令机器人和启用了 SSO 的个人选项卡 |
| 开发 Teams 应用 | 它包含： <br> - 添加和管理环境 <br> - 创建多功能应用 <br> - 创建基于功能的云资源 <br> - 集成第三方 API <br> - 自定义清单文件 <br> - TeamsFx SDK |
| 调试 Teams 应用 | 它包含： <br> - 在本地调试 Teams 应用 <br> - 调试后台进程|
| 托管 Teams 应用 | 它包含： <br> - 将资源预配到云 <br> - 部署到云|
| 测试 Teams 应用 | 它包含： <br> - 集成和协作 <br> - Zip Teams 元数据包 <br> - Teams 环境中的旁加载和测试应用 <br> - 在不同的环境中测试应用行为|
| 发布 Teams 应用 | 它包含： <br> - 发布应用 <br> - 管理管理员审批 <br> - 发布到存储 <br> - 与开发人员门户集成 |

### <a name="entities-integrated-with-teams-toolkit"></a>与 Teams 工具包集成的实体

Teams 工具包是Visual Studio Code中的扩展。 它与 Teams 工具包中的以下实体集成，例如 Azure AD 和 Microsoft 365、开发人员门户和 Microsoft graph。 所有实体都集成在 Teams 工具包中，并帮助用户创建应用。

| 实体 | 说明 |
| ---- | ---- |
| Azure AD  | Azure Active Directory (Azure AD) 是基于云的标识和访问管理服务。 此服务可帮助员工访问外部资源，例如 Microsoft 365、Azure 门户 和数千个其他 SaaS 应用程序。 |
| Microsoft 365  | 开发应用时，Teams 开发人员帐户。|
| 开发人员门户 | Teams 开发人员门户是配置、分发和管理 Microsoft Teams 应用的主要工具。 借助开发人员门户，你可以在应用上与同事协作、设置运行时环境等。 |
| Microsoft Graph | Microsoft Graph 是 Microsoft 365 中通往数据和智能的网关。 它提供统一的可编程模型，可用于访问 Microsoft 365、Windows 10 和企业移动性 + 安全性中的海量数据。 |

Teams 工具包将构建 Teams 应用所需的所有工具集中在一处。

## <a name="manage-your-apps-using-developer-portal"></a>使用开发人员门户管理应用

由于 Teams 工具包与开发人员门户集成，因此可以在创建应用后，使用部署下 [的 Teams](../concepts/build-and-test/teams-developer-portal.md) 开发人员门户配置、分发和管理应用。 有关详细信息，请参阅 [使用开发人员门户管理 Teams 应用](../concepts/build-and-test/manage-your-apps-in-developer-portal.md)。

:::image type="content" source="../assets/images/teams-toolkit-v2/build-environment-developer-portal-1.png" alt-text="开发人员门户":::

## <a name="see-also"></a>另请参阅

* [创建新的 Teams 项目](create-new-project.md)
* [安装 Teams 工具包](install-Teams-Toolkit.md)
* [浏览 Teams 工具包](explore-Teams-Toolkit.md)
* [准备使用 Microsoft Teams 工具包生成应用](build-environments.md)
