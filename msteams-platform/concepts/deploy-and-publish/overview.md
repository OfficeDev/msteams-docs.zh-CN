---
title: 分发应用程序
description: 介绍用于分发应用程序的三个选项
keywords: 团队发布商店 office 分发 AppSource 旁加载上传应用程序
ms.openlocfilehash: d3fd81e69f74b6332d9033412a7b6688239cd801
ms.sourcegitcommit: 02ab2cb7820dc8665bb4ec6a1a40c3b8b8f29d66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "47340955"
---
# <a name="distribute-your-microsoft-teams-app"></a>分发 Microsoft 团队应用程序

创建应用后，有三个选项可用于分发：

1. [直接上载您的应用程序](#upload-your-app-directly)。
2. [将您的应用程序发布到组织的应用程序目录](#publish-to-your-organizations-app-catalog)。
3. [通过 AppSource 发布您的应用程序](#publish-to-appsource)。

## <a name="enterprise-organizations"></a>企业组织

### <a name="upload-your-app-directly"></a>直接上载您的应用程序

这是测试和使用您的应用程序的最简单方法。 如果您是团队所有者和/或 [上传自定义应用程序](/microsoftteams/admin-settings)，则可以 [直接上传 (或旁加载) ](./apps-upload.md) 应用，然后立即开始使用它。 但是，如果要与其他人共享应用程序，则必须向其发送应用程序包，并要求他们独立上传它。

如果您想要更广泛地分发您的应用程序，团队会为用户提供一个应用程序库，以查找或发现高质量的团队应用程序。 若要使您的解决方案在库中可用，您必须 [发布到组织的应用程序目录](#publish-to-your-organizations-app-catalog) 或 [发布到 AppSource](./appsource/publish.md)。

### <a name="publish-to-your-organizations-app-catalog"></a>发布到你的组织的应用程序目录

您的组织的应用程序目录包含您的组织特有的应用程序，并且完全位于组织的控制之下。 有关详细信息，请参阅将 [*应用发布到组织的应用程序目录*](/microsoftteams/tenant-apps-catalog-teams)一文。 此功能只能由具有 Microsoft Office 365 租户管理员权限的团队用户来管理。

### <a name="publish-to-appsource"></a>发布到 AppSource

AppSource (以前称为 Office 应用商店) 为您分发 Microsoft 团队应用程序以及其他 Office 365 扩展性类型（如 Office 外接程序和 SharePoint 外接程序）提供了方便的位置。遵循我们的准则，将 [您的应用程序提交到 AppSource](./appsource/publish.md)。

## <a name="government-community-cloud-gcc-organizations"></a>政府社区云 (GCC) 组织

### <a name="upload-your-custom-app-directly-to-teams"></a>将您的自定义应用程序直接上载到团队

 作为 GCC 租户管理员，你将决定是将自定义应用上传到你的租户环境，还是将其发布到租户应用目录。 Microsoft 不拥有或控制您的自定义应用程序，因此，您必须确保所有终结点符合您组织的要求。 此外，如果应用程序解决方案包含 bot 或邮件扩展，则需要完成 [Bot 框架](https://dev.botframework.com/) 注册，如下所示：

1. 在 " **连接到通道** " 页上的 " **添加功能通道**" 下，选择 " **团队**"。
1. 导航到 " **配置 MSTeams** " 页 (*参阅* 以下) 。
1. 在 " **邮件** " 下，选择 " **适用于政府客户的 Microsoft 团队** " 单选按钮。
1. 在页面左下角，选择 " **保存**"。  

>[!IMPORTANT]
> 您不能使用 "团队商业配置" 将自定义应用上传/旁加载到 GCC 环境，您必须为符合 GCC 规范的配置选择 " **适用于政府客户的 Microsoft 团队** " 单选按钮。

![团队消息配置页](../../assets/images/gcc-configure.png)

> [!NOTE]
>
> * 以上提供的针对 GCC 环境的上传说明适用于团队自定义应用。 </br>
> * 默认情况下，在团队中启用合规性的 Microsoft 应用。
> * 第三方应用程序在租户级别被禁用，应通过组织的 [应用程序权限策略](/microsoftteams/teams-app-permission-policies)进行管理。 确保查看所有第三方应用程序，以确保它们与您的组织的策略和过程相一致。

> [!TIP]
>
> Microsoft 365 开发人员合作伙伴通过 [microsoft 365 应用认证计划](/microsoft-365-app-certification/overview)为其第三方团队应用提供安全性、数据处理和合规性详细信息。 *另请参阅* [Microsoft 团队应用认证](/microsoftteams/platform/concepts/deploy-and-publish/appsource/post-publish/application-certification)。
</br></br>
