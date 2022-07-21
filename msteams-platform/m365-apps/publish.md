---
title: 发布适用于 Microsoft 365 的 Teams 应用
description: 本文介绍如何让 Teams、Outlook 和 Office 中的用户发现已启用 Microsoft 365 的 Teams 应用。
ms.date: 05/24/2022
ms.topic: conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: c99114ed397b9c20f699ffee165189ec7c4fd26d
ms.sourcegitcommit: 4ba6392eced76ba6baeb6d6dd9ba426ebf4ab24f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2022
ms.locfileid: "66919814"
---
# <a name="publish-teams-apps-for-microsoft-365"></a>发布适用于 Microsoft 365 的 Teams 应用

Microsoft Teams 中支持已启用 Microsoft 365 的 Teams 应用进行生产使用。 可以将这些应用分发给预览使用目标 *版本* outlook.com 和 office.com 的受众，以及 Outlook for Windows 桌面版 *Beta Channel* 版本。 已启用 Microsoft 365 的 Teams 应用的分发选项和流程与传统 Teams 应用相同。

发布后，除了 Teams 应用商店之外，你的应用将作为可安装的应用从 Outlook 和 Office 应用商店中发现。 你的应用使用在 Outlook 和 Office 的 Teams 中定义的权限。 对于组织中的用户，Teams 管理员可以 [管理对 Microsoft 365 中 Teams 应用的访问权限](/MicrosoftTeams/manage-third-party-teams-apps) 。

:::image type="content" source="images/outlook-office-app-store.png" alt-text="屏幕截图是显示 Outlook 和 Office.com 为 SurveyMonkey 和 MURAL Teams 应用安装屏幕的示例。":::

## <a name="single-tenant-distribution"></a>单租户分发

启用 Outlook 的消息扩展可以通过多种方式分发到测试和生产租户：

### <a name="teams-client"></a>Teams 客户端

在 **“应用** ”菜单中，选择 **“管理应用** > **发布应用** > **将应用提交到组织**”。这需要 IT 管理员的批准。

### <a name="teams-developer-portal"></a>Teams 开发人员门户

使用 [Teams 开发人员门户](https://dev.teams.microsoft.com/) 将应用上载并发布到组织。 这需要 IT 管理员的批准。有关详细信息，请参阅 Microsoft [Teams 的开发人员门户管理应用](../concepts/build-and-test/teams-developer-portal.md)。

### <a name="microsoft-teams-admin-center"></a>Microsoft Teams 管理中心

作为 Teams 管理员，可以从 [Teams 管理中心](https://admin.teams.microsoft.com/)上传并预安装组织的租户的应用包。 有关详细信息，请参阅 [Microsoft Teams 管理中心中的上传自定义应用](/MicrosoftTeams/upload-custom-apps)。

### <a name="microsoft-admin-center"></a>Microsoft 管理中心

作为全局管理员，可以从 [Microsoft 管理员](https://admin.microsoft.com/)上传并预安装应用包。有关详细信息，请参阅[集成应用门户中合作伙伴的测试和部署Microsoft 365 应用版](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps)。

## <a name="multitenant-distribution"></a>多租户分布

为 Outlook 和 Office 启用的 Teams 应用的 [Microsoft AppSource](https://appsource.microsoft.com/) (Microsoft 商业市场) 提交过程与传统的 Teams 应用相同。 唯一的区别是需要在应用包中使用 Teams 应用清单 [版本 1.13](../tabs/how-to/using-teams-client-sdk.md) ，这为跨 Microsoft 365 运行的 Teams 应用引入了支持。

> [!TIP]
> 在通过 [Microsoft 合作伙伴网络](https://partner.microsoft.com/)) 提交到 Teams 应用商店 (之前，使用 Teams 开发人员门户[验证应用包](https://dev.teams.microsoft.com/validation)以解决任何错误或警告。

若要开始，请参阅 [“分发 Microsoft Teams”应用](../concepts/deploy-and-publish/apps-publish-overview.md)。
