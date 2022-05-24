---
title: 发布Teams应用以Microsoft 365
description: 使已启用Microsoft 365的Teams应用在Teams、Outlook和Office中可供用户发现
ms.date: 05/24/2022
ms.topic: conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 66b5adb6162222da155318aeb818fd681a664816
ms.sourcegitcommit: 264d3cc84d6eec4ab025cf86a7a6f4865f1aed07
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2022
ms.locfileid: "65653699"
---
# <a name="publish-teams-apps-for-microsoft-365"></a>发布Teams应用以Microsoft 365

Microsoft Teams中支持启用Microsoft 365 Teams应用进行生产使用。 可以将这些应用分发给预览使用目标 *版本* 的 outlook.com 和 office.com 的受众，以及用于Windows桌面的 *Beta 频道* Outlook版本。 已启用Microsoft 365 Teams应用的分发选项和流程与传统Teams应用相同。

发布后，除了Teams存储之外，你的应用将作为可安装的应用从Outlook和Office 应用存储中发现。 应用使用Outlook和Office Teams中定义的权限。 Teams管理员可以管理对组织中用户[跨Microsoft 365 Teams应用的访问权限](/MicrosoftTeams/manage-third-party-teams-apps)。

:::image type="content" source="images/outlook-office-app-store.png" alt-text="Outlook和 Office.com 安装 SurveyMonkey 和 MURAL Teams 应用的屏幕":::

## <a name="single-tenant-distribution"></a>单租户分发

Outlook启用的消息扩展插件可以通过多种方式分发到测试和生产租户：

### <a name="teams-client"></a>Teams 客户端

在 *“应用* ”菜单中，选择 *“管理应用* > *”，将应用* > **提交到组织**。这需要 IT 管理员的批准。

### <a name="teams-developer-portal"></a>Teams开发人员门户

使用[Teams开发人员门户](https://dev.teams.microsoft.com/)将应用上载并发布到组织。 这需要 IT 管理员的批准。有关详细信息，请参阅开发[人员门户为Microsoft Teams管理应用](../concepts/build-and-test/teams-developer-portal.md)。

### <a name="microsoft-teams-admin-center"></a>Microsoft Teams 管理中心

作为Teams管理员，可以从[Teams管理中心](https://admin.teams.microsoft.com/)上传并预安装组织的租户的应用包。 有关详细信息，请参阅[Microsoft Teams管理中心Upload自定义应用](/MicrosoftTeams/upload-custom-apps)。

### <a name="microsoft-admin-center"></a>Microsoft 管理中心

作为全局管理员，可以从 [Microsoft 管理员](https://admin.microsoft.com/)上传并预安装应用包。有关详细信息，请参阅[集成应用门户中合作伙伴的测试和部署Microsoft 365 应用版](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps)。

## <a name="multitenant-distribution"></a>多租户分布

[Microsoft AppSource](https://appsource.microsoft.com/) (Microsoft 商业市场) 为Outlook和Office启用的Teams应用的提交过程与传统Teams应用相同;唯一的区别是需要在应用包中使用Teams应用清单[版本 1.13](../tabs/how-to/using-teams-client-sdk.md)，这为Teams 跨Microsoft 365运行的应用。

> [!TIP]
> 使用Teams开发人员门户[验证应用包](https://dev.teams.microsoft.com/validation)，以便在通过 [Microsoft 合作伙伴网络](https://partner.microsoft.com/)) 提交到Teams存储 (之前解决任何错误或警告。

若要开始，请参阅[“分发Microsoft Teams应用](../concepts/deploy-and-publish/apps-publish-overview.md)。
