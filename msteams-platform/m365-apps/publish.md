---
title: 发布适用于 Microsoft 365 的 Teams 应用
description: 了解如何通过单租户和多租户分发让 Teams、Outlook 和 Office 中的用户能够发现已启用 Microsoft 365 的 Teams 应用。
ms.date: 10/10/2022
ms.topic: conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: cfe650e676252a16c1665f078938adbff0d4c7d7
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789882"
---
# <a name="publish-teams-apps-for-microsoft-365"></a>发布适用于 Microsoft 365 的 Teams 应用

Microsoft Teams 支持支持 Microsoft 365 的 Teams 应用用于生产。 可以将这些应用分发给使用 *目标发布*  (开发人员预览版) Outlook.com 和 Office.com 版本、Outlook for Windows 桌面 *版 Beta 频道* 版本和 Office 当前频道 (开发预览版) Android 版 Office 应用的用户。 已启用 Microsoft 365 的 Teams 应用的分发选项和流程与传统 Teams 应用相同。

发布后，除了 Teams 应用商店外，你的应用还可以从 Outlook 和 Office 应用商店中发现为可安装的应用。 你的应用跨 Outlook 和 Office 使用 Teams 中定义的权限。 Teams 管理员可以管理组织中用户 [跨 Microsoft 365 对 Teams 应用的访问权限](/MicrosoftTeams/manage-third-party-teams-apps) 。

:::image type="content" source="images/outlook-office-app-store.png" alt-text="屏幕截图是显示 Outlook 和 Office.com SurveyMonkey 和 MURAL Teams 应用的安装屏幕的示例。":::

## <a name="single-tenant-distribution"></a>单租户分发

可以通过多种方式将已启用 Outlook 的邮件扩展分发到测试和生产租户：

### <a name="teams-client"></a>Teams 客户端

在“ **应用** ”菜单中，选择“ **管理应用** > **”“发布应用** > **”“将应用提交到组织**”。若要提交应用，需要 IT 管理员的批准。

### <a name="teams-developer-portal"></a>Teams 开发人员门户

使用 [Teams 开发人员门户](https://dev.teams.microsoft.com/) 为组织上传和发布应用。 上传和发布应用需要 IT 管理员的批准。有关详细信息，请参阅 [使用 Microsoft Teams 开发人员门户管理应用](../concepts/build-and-test/teams-developer-portal.md)。

### <a name="microsoft-teams-admin-center"></a>Microsoft Teams 管理中心

作为 Teams 管理员，你可以从 [Teams 管理中心](https://admin.teams.microsoft.com/)为组织的租户上传和预安装应用包。 有关详细信息，请参阅 [在 Microsoft Teams 管理中心上传自定义应用](/MicrosoftTeams/upload-custom-apps)。

### <a name="microsoft-admin-center"></a>Microsoft 管理中心

作为全局管理员，你可以从 [Microsoft 管理员](https://admin.microsoft.com/)上传和预安装应用包。有关详细信息，请参阅[测试和部署集成应用门户中的合作伙伴Microsoft 365 应用版](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps)。

## <a name="multitenant-distribution"></a>多租户分布

[Microsoft AppSource](https://appsource.microsoft.com/) (Microsoft 商业市场) 针对已启用 Outlook 和 Office 的 Teams 应用的提交过程与传统 Teams 应用相同。 唯一的区别在于，你需要在应用包中使用 Teams 应用清单 [版本 1.13](../tabs/how-to/using-teams-client-sdk.md) ，它引入了对跨 Microsoft 365 运行的 Teams 应用的支持。

> [!TIP]
> 在通过 [Microsoft 合作伙伴网络](https://partner.microsoft.com/)) 提交到 Teams 应用商店 (之前，使用 Teams 开发人员门户[验证应用包](https://dev.teams.microsoft.com/validation)以解决任何错误或警告。

若要开始，请参阅 [分发 Microsoft Teams 应用](../concepts/deploy-and-publish/apps-publish-overview.md)。
