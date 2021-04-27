---
title: 分发应用
description: 介绍了分配应用的三个选项
ms.topic: conceptual
localization_priority: Normal
keywords: Teams 发布应用商店 Office 分发 AppSource 旁加载上传应用
ms.openlocfilehash: a033b90be436fbf20ef11fe95059d04388cefdf8
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020777"
---
# <a name="distribute-your-microsoft-teams-app"></a>分发 Microsoft Teams 应用

创建应用后，有三种分配应用的选项：

1. [直接上传应用](#upload-your-app-directly)。
2. [将应用发布到组织的应用程序目录](#publish-to-your-organizations-app-catalog)。
3. [通过 AppSource 发布应用](#publish-to-appsource)。

## <a name="enterprise-organizations"></a>企业组织

### <a name="upload-your-app-directly"></a>直接上传应用

这是测试和使用应用的最简单方法。 如果你是团队所有者并且 [/或上传](/microsoftteams/admin-settings)自定义应用已启用，可以直接上传 (或旁加载 [) ](./apps-upload.md) 应用并立即开始使用它。 但是，如果你想要与其他人共享该应用，你必须将应用包发送给他们，并要求他们单独上传它。

如果你想要更广泛地分发你的应用，Teams 会为用户提供一个应用内库来查找或发现高质量的 Teams 应用。 若要在库中提供你的解决方案， [你必须发布到你](#publish-to-your-organizations-app-catalog) 组织的应用目录或 [发布到 AppSource](./appsource/publish.md)。

### <a name="publish-to-your-organizations-app-catalog"></a>发布到组织的应用程序目录

组织的应用程序目录包含组织独有的应用，完全受组织控制。 可以在将应用程序发布到组织 [*的应用程序目录中一文找到详细信息*](/microsoftteams/tenant-apps-catalog-teams)。 此功能仅能由具有 365 Microsoft Office管理员权限的 Teams 用户进行管理。

### <a name="publish-to-appsource"></a>发布到 AppSource

AppSource (以前称为 Office 应用商店) ，它提供了分发 Microsoft Teams 应用以及其他 Office 365 扩展类型（如 Office 外接程序和 SharePoint 外接程序）的便捷位置。按照我们的指南[将应用提交到 AppSource。](./appsource/publish.md)

## <a name="government-community-cloud-gcc-organizations"></a>政府社区云 (GCC) 组织

### <a name="upload-your-custom-app-directly-to-teams"></a>将自定义应用直接上传到 Teams

 作为 GCC 租户管理员，你将决定是否将自定义应用上传到租户环境，以及是否将其发布到租户应用目录。 因此，Microsoft 不拥有或控制自定义应用程序，因此必须确保所有终结点都符合组织的要求。 此外，如果应用解决方案包括自动程序或邮件扩展，你将需要完成 [自动程序框架](https://dev.botframework.com/) 注册，如下所示：

1. 在"**连接到频道"页上** 的"**添加特色频道"下**，选择 **"Teams"。**
1. 导航到配置 **MSTeams** 页面 (*请参阅下面的*) 。
1. 在 **"消息"** 下，选择 **"Microsoft Teams 政府客户"** 单选按钮。
1. 在页面的左下角，选择"保存 **"。**  

>[!IMPORTANT]
> 不能使用 Teams 商业配置将自定义应用上载/旁加载到 GCC 环境，必须为符合 GCC 的配置选择 **Microsoft Teams 政府** 客户单选按钮。

![Teams 消息配置页](../../assets/images/gcc-configure.png)

> [!NOTE]
>
> * 上述 GCC 环境的上传说明适用于 Teams 自定义应用。 </br>
> * 默认情况下，合规性 Microsoft 应用在 GCC 环境中在 Teams 中启用。
> * 第三方应用在租户级别禁用，并且应该通过组织的应用程序权限策略 [进行管理](/microsoftteams/teams-app-permission-policies)。 确保查看所有第三方应用，以确保它们符合组织的策略和过程。

> [!TIP]
>
> Microsoft 365 开发人员合作伙伴通过 [Microsoft 365](/microsoft-365-app-certification/overview)应用认证计划为第三方 Teams 应用提供安全性、数据处理和合规性详细信息。 *另请参阅* [Microsoft Teams 应用认证](/microsoftteams/platform/concepts/deploy-and-publish/appsource/post-publish/application-certification)。
</br></br>
