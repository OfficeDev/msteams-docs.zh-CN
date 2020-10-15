---
title: Microsoft 团队应用程序审批提交过程指南
description: 介绍用于获取发布到 Microsoft 团队应用商店的应用程序的提交审批过程
keywords: 团队发布 microsoft store office 发布发布 AppSource 合作伙伴中心帐户验证应用帐户未发布资格
ms.openlocfilehash: 6cc38e29d02935cf023bb26d3a317554493b0fe2
ms.sourcegitcommit: 25afe104d10c9a6a2849decf5ec1d08969d827c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2020
ms.locfileid: "48465927"
---
# <a name="submit-your-app-to-appsource"></a>将您的应用程序提交到 AppSource

## <a name="teams-app-submission"></a>团队应用程序提交

将应用程序发布到 [AppSource](https://appsource.microsoft.com) 使其在团队应用程序目录和 web 上可用。 从较高的层次来看，将应用程序提交到 AppSource 的过程如下：

1. 遵循我们的 [设计准则](~/concepts/design/understand-use-cases.md)来开发您的应用程序。 选项卡应遵循我们的 [选项卡设计准则](~/tabs/design/tabs.md)。 Bot 应遵循 [bot 设计指南](~/bots/design/bots.md)。
1. 确保您的应用程序符合 Microsoft 团队的应用程序 [验证策略](/legal/marketplace/certification-policies) 。
1. 在 "[合作伙伴中心](https://support.microsoft.com/help/4499930/partner-center-overview)" 中[设置开发人员帐户](/office/dev/store/open-a-developer-account)。 另*请参阅*下面的 FAQ 部分中的[如何创建合作伙伴中心帐户](#how-do-i-create-a-partner-center-account)。
1. 按照 [提交清单](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)，准备要提交的应用程序。
1. 查看我们 [关于成功提交应用程序的提示](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)。
1. [通过合作伙伴中心](/office/dev/store/use-partner-center-to-submit-to-appsource)将您的包提交到 AppSource。
1. 跟踪合作伙伴中心仪表板上的审批流程。 *请参阅*[合作伙伴中心概述](https://support.microsoft.com/help/4499930/partner-center-overview)。
1. 提交后提交—查看有关 [维护和支持您发布的应用程序](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)的指南。

>[!NOTE]
>
>- 如果您的团队应用程序包含 bot，则必须遵守 Bot 开发人员框架 [行为准则](https://aka.ms/bf-conduct)。
>- 如果您的应用程序包含 Office 365 连接器，可能会应用其他条款。 *请参阅*[连接器开发人员仪表板](https://aka.ms/connectorsdashboard)和[应用程序开发人员协议](https://sellerdashboard.microsoft.com/Assets/Content/Agreements/Office_Store_Seller_Agreement_20120927.htm)。
>- 若要使您的应用程序可供 GCC 用户使用，并在存储中避免出现重复的应用程序列表，则身份验证进程/流应标识用户并将其传送到适用于 GCC 用户的指定/预期内容 URL。

## <a name="faqs--teams-apps-and-partner-account-verification-process-in-partner-center"></a>Faq —合作伙伴中心的团队应用和合作伙伴帐户验证流程

## <a name="how-do-i-create-a-partner-center-account"></a>如何创建合作伙伴中心帐户？

有两种创建合作伙伴中心帐户的方法：

- 如果你不熟悉合作伙伴中心，并且在 Microsoft 网络中没有帐户，请 [使用 "合作伙伴中心注册" 页创建帐户](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment)。
- 如果你已在合作伙伴网络中注册，请 [使用现有注册直接在合作伙伴中心中创建帐户](/office/dev/store/)。

## <a name="what-if-i-cannot-find-my-office-store-account-in-partner-center"></a>如果我无法在合作伙伴中心找到我的 Office 应用商店帐户，该怎么办？

请打开 [合作伙伴中心支持票证](https://partner.microsoft.com/support/v2/?stage=1) ，然后从下拉菜单中选择以下内容：

| 菜单 | 选项 |
| -------   | -------  |
|类别| 商业市场|
| 主题 | 常规市场帮助和操作方法问题 |
| 子| Office 加载项 |

## <a name="where-can-i-get-support-for-my-partner-center-account-issues"></a>在哪里可以获得对我的合作伙伴中心帐户问题的支持？

请访问我们的 [发布者支持页面](https://aka.ms/marketplacepublishersupport) 以搜索你的问题主题并查找指南。 如果提供的指南不起作用，请 [打开合作伙伴中心支持票证](/azure/marketplace/partner-center-portal/support#how-to-open-a-support-ticket)。

## <a name="how-do-i-manage-my-office-store-account-in-partner-center"></a>如何在合作伙伴中心管理我的 Office 应用商店帐户？

若要了解如何通过合作伙伴中心管理 Office 应用商店帐户，请访问 "  [合作伙伴中心" 中的 "管理你的 Office 应用商店帐户](/office/dev/store/manage-account-settings-and-profile) "。

## <a name="how-do-i-add-my-phone-number-to-the-partner-profile-contact-section"></a>如何将我的电话号码添加到合作伙伴配置文件联系人部分？

电话号码包含三个部分：国家/地区代码、区号和电话号码。 如果你的电话号码不包含区号，则将第二个框留空，然后完成第三个框。

## <a name="how-do-i-manage-my-account-settings-and-partner-profile-in-partner-center"></a>如何在合作伙伴中心管理我的帐户设置和合作伙伴配置文件？

有关管理合作伙伴中心帐户设置的指南，请访问我们的 " [管理帐户设置和配置文件信息](/windows/uwp/publish/manage-account-settings-and-profile#additional-settings-and-info) " 页面。

## <a name="why-do-i-receive-the-message-this-account-is-not-publish-eligible-when-i-try-to-submit-my-add-in-through-partner-center"></a>为什么我会收到邮件：当我尝试通过合作伙伴中心提交我的加载项时，"此帐户未发布合格"。

当您的 [帐户验证状态](/partner-center/verification-responses) 为 "挂起" 时，您将收到上述错误消息。 您可以在 "合作伙伴中心"[仪表板](https://partner.microsoft.com/dashboard)中通过选择 "**设置**" 选项 ("齿轮" 图标) 在页面页眉命令行管理程序的右上角，然后选择 "**开发人员设置**" 帐户 "帐户  =>  **Account**   =>  **设置**" 来检查您的帐户验证状态。

![合作伙伴中心帐户设置页](../../../assets/images/partner-center-accts-page.png)

![合作伙伴中心验证状态](../../../assets/images/partner-center-verification-status.png)

在帐户验证过程中，将显示每个所需步骤的状态（电子邮件所有权、雇用验证和商业验证）。 成功完成验证过程后，配置文件页上的注册的验证状态将从 "挂起" 更改为 "已授权"，并且不会再显示进程步骤。

![合作伙伴中心验证错误](../../../assets/images/partner-center-acct-verification-error.png)

## <a name="what-is-verified-in-partner-center-account-verification-process-and-how-to-respond"></a>合作伙伴中心帐户验证过程中验证了哪些内容以及如何进行响应？
有三个验证区域-电子邮件所有权、雇用和业务。 如果你是主要联系人 (全局管理员 "或" 帐户管理员 ") ，请查看已验证内容的详细信息 [以及如何响应](/partner-center/verification-responses#what-is-verified-and-how-to-respond) 。我们建议你转到合作伙伴配置文件以监视验证状态并跟踪进度。

验证过程完成后，配置文件页面上的注册的验证状态将从 " *待定* " 更改为 "已 *授权* "，并且在该页面上显示的 "进程步骤" 状态将消失。 主要联系人会在验证完成后的几个工作日内收到来自 Microsoft 的电子邮件。

## <a name="my-account-verification-status-has-not-advanced-beyond-email-ownership-in-partner-center-how-should-i-proceed"></a>我的帐户验证状态除了合作伙伴中心的电子邮件所有权之外，尚未提前。 我应该如何继续？

在 **电子邮件所有权** 验证过程中，会将验证电子邮件发送到主要联系人电子邮件地址。 请检查主要联系人收件箱中是否有需要主题行操作的电子邮件 **maccount@<span>microsoft</span>.Com** *：使用 microsoft 验证您的电子邮件帐户*，请求您完成电子邮件验证过程。 验证电子邮件将发送到合作伙伴中心的 "帐户设置" 页上列出的电子邮件地址。

> [!NOTE]
 >电子邮件验证链接仅在7天内有效。 你可以通过访问合作伙伴配置文件页面并选择 " **重新发送验证电子邮件** " 链接，请求重新向你发送电子邮件。 若要确保收到电子邮件，请将安全列表电子邮件从 microsoft.com 为安全域，并检查 "垃圾邮件" 文件夹。

## <a name="how-i-do-get-further-support-for-my-account-related-issues"></a>如何获取对与我的帐户相关的问题的进一步支持？

若要了解如何创建支持票证，请访问 [合作伙伴中心计划中的商业市场计划的支持人员](/azure/marketplace/partner-center-portal/support) 和步骤。

## <a name="ive-checked-my-mail-folders-and-havent-received-the-verification-email-what--should-i-do-next"></a>我已检查我的邮件文件夹，但尚未收到验证电子邮件。 接下来我该怎么办？

请尝试以下操作：

1. 检查您的垃圾邮件文件夹。
1. 清除浏览器缓存，转到合作伙伴中心帐户仪表板，然后选择 " **重新发送验证电子邮件** " 链接，将验证电子邮件发送到您的电子邮件地址。
1. 尝试从其他浏览器访问  **重新发送验证电子邮件** 链接。
1. 与 IT 部门合作，以确保电子邮件服务器不会阻止验证电子邮件。
1. 调整您的服务器的垃圾邮件筛选器，以允许/通过 maccount@microsoft 的所有电子邮件进行安全列表 **。 <span></span>com**。

## <a name="how-long-does-the-employment-verification-process-usually-take"></a>雇用验证过程通常需要多长时间？

如果所有提交的详细信息都是正确的，则雇用验证将在1到2小时内完成。

## <a name="how-long-does-the-business-verification-process-usually-take"></a>"业务验证" 过程通常需要多长时间？

业务验证需要1到2个工作日才能完成，只要提交了所有必需的文档。

## <a name="if-i-reach-out-to-the-support-team-will-my-ticket-be-expedited"></a>如果我转到支持团队，我的票证将会加快吗？

支持票证将在一周内得到解决。 请查找将发送到在发出支持票证时提供的电子邮件的更新。

## <a name="my-issue-is-not-listed-here--are-there-other-pages-i-can-reference-for-partner-center-issues"></a>我的问题未在此处列出。  是否有其他页面可供我参考以获取合作伙伴中心问题？

请参阅我们的 [商业市场文档](/azure/marketplace/) 以获取更多帮助。

## <a name="ive-created-a-support-ticket-it-has-been-7-business-days-and-i-havent-received-an-update-where-can-i-get-additional-help"></a>我已经创建了一个支持票证，它已有7个工作日，但尚未收到更新。 在哪里可以获得更多帮助？

请 **<teamsubm@microsoft.com>** 使用以下详细信息发送电子邮件：

1. **主题行**。 *<App_Name>的合作伙伴中心帐户问题 * (指定您的应用程序) 的名称。
1. **电子邮件正文：**
    * 支持票证号码：
    * 卖家 ID：
    *  (的问题的屏幕截图（如果可能）) ：

>
> [!div class="nextstepaction"]
> [了解有关 Microsoft 团队的应用验证策略的详细信息](/legal/marketplace/certification-policies)
