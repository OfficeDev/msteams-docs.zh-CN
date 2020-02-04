---
title: 准备 Office 365 租户
description: 如何开始使用 Office 365 中的团队
keywords: 配置 Office 365 租户团队上载
ms.openlocfilehash: 62cd640196631f50c72762253ff1bd75a143337d
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673359"
---
# <a name="prepare-your-office-365-tenant"></a>准备 Office 365 租户

若要为 Microsoft 团队开发应用程序，您必须是[Office 365 客户，且具有以下计划之一](https://products.office.com/business/compare-more-office-365-for-business-plans)。

* 商业协作版
* 商业高级版
* 企业版 E1、E3 和 E5
* Developer
* 教育版、教育版和教育版 E5

Microsoft 团队还将对在其退休前购买了 E4 的客户提供。

## <a name="just-need-a-development-environment"></a>只需要开发环境？

如果当前没有 Office 365 帐户，可以注册[office 365 开发人员计划](https://dev.office.com/devprogram)以获取*免费*的90天（只要你将其用于开发活动，就可以续订，只要你使用它进行开发活动） Office 365 开发人员租户。 此帐户仅可用于测试目的。 有关[设置测试帐户](https://support.office.com/article/Add-users-individually-or-in-bulk-to-Office-365-Admin-Help-1970f7d6-03b5-442f-b385-5880b9c256ec?ui=en-US&rs=en-US&ad=US)的详细信息，请参阅。

## <a name="enable-microsoft-teams-for-your-organization"></a>为你的组织启用 Microsoft 团队

如果尚未为你的组织启用 Microsoft 团队，你将需要先执行此操作。 请参阅我们为[你的组织启用团队](/microsoftteams/how-to-roll-out-teams)的详细指南。

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>启用自定义团队应用并启用自定义应用上传

> 注意：如果你正在使用 O365 开发人员组织生成应用，则应已将这些设置配置为允许你生成、上传和测试应用。

启用自定义应用程序和自定义应用程序上载涉及以下三个设置：

* **组织范围内的自定义应用设置**-此设置可启用或禁用组织的自定义应用程序。 需要打开它。 
* **团队自定义应用设置**-此设置适用于 Microsoft 团队中的每个团队。 如果要为特定团队安装您的应用程序，则需要为该团队启用此项。
* **用户自定义应用程序策略**-此设置可控制单个用户的权限。 你需要为你想要上载自定义应用的个人启用此。

有关这些设置如何交互的完整信息，请参阅在[Microsoft 团队中管理自定义应用程序策略和设置](/MicrosoftTeams/teams-custom-app-policies-and-settings)。
