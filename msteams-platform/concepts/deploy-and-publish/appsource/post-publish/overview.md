---
title: 维护和支持已发布的应用
description: 了解如何维护已发布的 Microsoft Teams 应用，以及在 Teams 应用商店和 AppSource 上列出应用商店后要考虑的操作。
ms.topic: conceptual
ms.localizationpriority: high
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: e01b5b8dc053559248bc3217a0807b69ec014669
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123046"
---
# <a name="maintain-your-published-microsoft-teams-app"></a>维护已发布的 Microsoft Teams 应用

在 Microsoft Teams 应用商店中列出你的应用后，请开始考虑如何继续维护应用，并增加下载和使用量。

## <a name="analyze-app-usage"></a>分析应用使用情况

可以在合作伙伴中心中的 [Teams 应用使用情况报告](/office/dev/store/teams-apps-usage) 中跟踪应用使用情况。 指标包括每月、每日、每周活动用户，以及可跟踪改动率和使用频率的保留期和强度图表。

新发布的应用的数据大约需要一周时间才会显示在报表中。

## <a name="publish-updates-to-your-app"></a>将更新发布到应用

> [!NOTE]
> Teams 应用商店已演变:
>
> 以前，可通过在应用磁贴上选择省略号来复制链接。 借助更新的 Teams 应用商店体验，你将从应用的详细信息选项卡访问同一内容。 此更新将于 2022 年 3 月 1 日正式发布 (GA)。

可以在合作伙伴中心中将更改提交到应用（例如新增功能，甚至元数据）。 这些更改需要新的评审过程。

发布更新时，请确保满足以下要求：

* 请勿更改应用 ID。
* 递增应用的版本号。
* 在合作伙伴中心中，不要选择“**添加新应用**”来执行更新。请改为转到应用的页面。

### <a name="app-updates-requiring-user-consent"></a>需要用户同意的应用更新

当用户安装应用时，必须向应用授予访问应用运行所需的服务和信息的权限。 大多数情况下，用户必须执行此操作一次，之后将自动安装应用的新版本。
但如果对应用进行了以下任何更改，则现有用户必须接受另一个权限请求才能安装更新：

* 添加或删除机器人。
* 更改机器人 ID。
* 修改机器人的单向通知配置。
* 修改机器人对上传和下载文件的支持。
* 添加或删除邮件扩展。
* 添加个人选项卡。
* 添加频道和群组选项卡。
* 添加连接器。
* 修改与 Microsoft Azure Active Directory (Azure AD) 应用注册相关的配置。有关详细信息，请参阅 [`webApplicationInfo`](~/resources/schema/manifest-schema.md#webapplicationinfo)。

## <a name="fix-issues-with-your-published-app"></a>修复已发布应用的问题

Microsoft 针对在 Teams 应用商店中列出的应用运行每日自动化测试。 如果发现与应用相关的问题，我们将与你联系，并提供关于如何重现问题和解决建议的详细报告。。 如果无法在规定的日程表中修复问题，可能会从应用商店中删除你的应用一览。

## <a name="promote-your-app-on-another-site"></a>在其他网站上推广应用

当你的应用在 Teams 应用商店中列出时，你可以创建一个链接来启动 Teams 并显示一个对话框来安装你的应用。 例如，可以在产品的市场推广页面上包含此链接和下载按钮。

使用追加应用 ID 的以下 URL 创建链接：`https://teams.microsoft.com/l/app/<your-app-id>`。

## <a name="complete-microsoft-365-certification"></a>完成 Microsoft 365 认证

[Microsoft 365 认证](/microsoft-365-app-certification/docs/certification) 保证在 Microsoft 365 生态系统中安装第三方 Office 应用或外接程序时，数据和隐私受到充分保护。 认证确认了应用兼容于 Microsoft 技术、符合云应用安全最佳做法且受到 Microsoft 支持。

## <a name="stop-app-distribution"></a>停止应用分发

可以从 [Microsoft 商业市场](/azure/marketplace/overview) 中删除应用，以防止其发现和使用。

若要在发布应用后停止分发，请按照以下步骤操作：

1. 在“**产品概述**”页上，选择“**停止销售**”。 它会从 Microsoft AppSource 中删除该应用。
1. 若要启动应用的取消列表，请在“**合作伙伴中心**”选择“**概述**”页，然后选择“**停止销售**”。

停止分发应用后，仍可以在合作伙伴中心中看到它，状态为“**不可用**”。 如果决定再次发布该应用，请按照说明 [将应用发布到 Microsoft Teams 应用商店](/concepts/deploy-and-publish/appsource/publish#teams-app-submission)。

## <a name="see-also"></a>另请参阅

[通过 Microsoft 商业市场利用应用盈利](/office/dev/store/monetize-addins-through-microsoft-commercial-marketplace)
