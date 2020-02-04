---
title: 提交内容清单
description: 将 Microsoft 团队应用程序发布到 AppSource 之前要使用的清单
keywords: 团队发布商店 office 发布清单提交准备
ms.openlocfilehash: b79e92b5cf8de01ec19c26c63814c6a6ae1e9a09
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673078"
---
# <a name="prepare-for-appsource-submission"></a>准备 AppSource 提交  

若要在 AppSource 上列出，您的应用程序必须经过审批过程。 这是 Microsoft 团队组提供的一项免费服务，它验证您的应用程序按所述方式工作，包含所有适当的元数据，并提供对最终用户有价值的内容。 为了帮助你获得快速批准，请确保你的应用满足以下要求和指南：

* **分发方法：** 请确保您的应用程序适用于商店。 在不发布到 AppSource 的情况下，分发应用程序的[其他选项](../../overview.md)。
* **应用程序详细信息页面：** 您的应用程序符合[应用程序详细信息页检查表](detail-page-checklist.md)
* **提示和频繁失败的情况：** 请特别注意这些[提示和频繁失败的情况](frequently-failed-cases.md)，以改进应用提交到审批时间。
* **应用程序清单：** 针对应用程序中的[应用程序清单检查表](app-manifest-checklist.md)和清单检查器检查应用程序清单
* **测试和调试：** 您已对[应用程序进行了充分测试和调试](../../../build-and-test/debug.md)。
* **验证策略：** 它必须传递工作组选项卡和 bot 的所有当前[AppSource 验证策略](https://dev.office.com/officestore/docs/validation-policies)。 请注意，这些策略可能会发生更改。
* **测试备注：** 包含[验证的测试说明](#test-notes-for-validation)
* **隐私策略：** 确保你的[隐私策略、使用条款和支持 url](#privacy-policy-terms-of-use-and-support-urls)遵循我们的准则。

完成上述所有要求后，即可通过[合作伙伴中心](/office/dev/store/use-partner-center-to-submit-to-appsource)将包提交到应用程序源。

## <a name="privacy-policy-terms-of-use-and-support-urls"></a>隐私策略、使用条款和支持 Url

### <a name="privacy-policy"></a>隐私策略

隐私策略指南：
* 隐私策略可以是特定于您的应用程序和/或外接程序，也可以是所有服务的整体策略。 
* 如果使用通用隐私策略，则必须引用 "服务/应用程序/平台" 以涵盖你的团队应用和你的网站。 
* 它必须包括您处理用户数据存储、用户数据保留、删除和安全控制信息的方式。
* 它必须包含您的联系信息。
* 它不应包含损坏的链接、beta Url 或暂存 Url。 


### <a name="terms-of-use"></a>使用条款

使用条款声明应是特定的，并适用于您的应用和/或外接程序产品。

### <a name="support-urls"></a>支持 Url

您的支持 Url 不应要求身份验证或登录凭据，以便与您联系，以解决应用程序中的任何问题。

## <a name="test-notes-for-validation"></a>验证的测试说明

必须至少提供两个登录凭据（一个管理员和一个），以便可以验证您的应用程序。

* 你提供的帐户应预先填充足够的数据以供验证之用。
* 对于企业应用程序、需要订阅的应用程序，或在其中有 office 365 租户/域依赖项进行测试时，您必须在尚未配置为使用您的应用程序的同一域中提供第三个帐户，以便我们可以验证首次运行的用户体验。
* 如果您的应用程序具有任何高级/升级功能，则必须提供具有必要访问权限的帐户来测试该体验。
* 您可以选择将测试笔记上传到 SharePoint。 在这种情况下，请提供指向文件的公用链接。
