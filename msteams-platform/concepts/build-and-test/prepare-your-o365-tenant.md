---
title: 准备 Office 365 租户
description: 如何开始使用 Office 365 中的团队
keywords: 配置 Office 365 租户团队上载
ms.openlocfilehash: e07ffe7f5325be1293a49934669f36c81613278b
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "43914565"
---
# <a name="prepare-your-office-365-tenant"></a>准备 Office 365 租户

如果你是 Office 365 订阅者，则可以使用以下[计划](https://products.office.com/business/compare-more-office-365-for-business-plans)之一为 Microsoft 团队开发应用程序：

* 商业协作版
* 商业高级版
* 企业版 E1、E3 和 E5
* 开发人员
* 教育版、教育版和教育版 E5

Microsoft 团队还将对在其[退休](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)前订阅 E4 的客户提供。

## <a name="just-need-a-development-environment"></a>只需要开发环境？

如果当前没有 Office 365 帐户，则可以注册[Microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program)订阅。 它在90天内*免费*使用，并且将持续更新，只要你将其用于开发活动即可。 如果你有 Visual Studio *Enterprise*或*专业版*订阅，这两个程序都包括一个免费的 Microsoft 365[开发人员订阅](https://aka.ms/MyVisualStudioBenefits)，在 Visual Studio 订阅的生命周期内处于活动状态。 *请参阅*[设置 Microsoft 365 开发人员订阅](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。

## <a name="enable-microsoft-teams-for-your-organization"></a>为你的组织启用 Microsoft 团队

如果尚未为你的组织启用 Microsoft 团队，你将需要先执行此操作。 请参阅我们为[你的组织启用团队](https://docs.microsoft.com/microsoftteams/enable-features-office-365)的详细指南。

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>启用自定义团队应用并启用自定义应用上传

> [!Note] 
> 如果使用的是 Office 365 开发人员平台来构建应用程序，则应已将这些设置配置为允许您生成、上载和测试应用程序。

有三个与启用自定义应用程序和自定义应用程序上载相关的设置：

* **组织范围的自定义应用设置** => **允许与中的自定义应用** => **On**程序进行交互—此设置可启用或禁用组织的自定义应用程序。 需要打开它。 
* **团队自定义应用设置** => **允许成员上载自定义应用程序** => **打开/关闭**—此设置适用于 Microsoft 团队中的每个单独团队。 如果要为特定团队安装您的应用程序，则需要为该团队启用此项。
* **用户自定义应用程序策略** => **用户可以上传自定义应用程序** => **On/Off** ，此设置控制单个用户的权限。 你需要为允许上传自定义应用的个人启用此。

有关这些设置如何交互的完整信息，*请参阅*在 microsoft 团队中[管理自定义应用策略和设置](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings)和[管理 microsoft 团队中的应用程序设置策略](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)。
