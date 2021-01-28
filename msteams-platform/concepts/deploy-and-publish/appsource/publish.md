---
title: 了解 Teams 应用商店提交过程
description: 介绍将应用发布到 Microsoft Teams 应用商店的审批提交过程
ms.topic: overview
keywords: teams 发布应用商店 Office 发布发布 AppSource 合作伙伴中心帐户验证应用帐户未发布符合条件的应用提交
ms.openlocfilehash: d2dc624c6dd13896397041c5c69ce5c5eb471a5b
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014409"
---
# <a name="submit-your-app-to-appsource"></a>将应用提交到 AppSource

## <a name="teams-app-submission"></a>Teams 应用提交

将你的应用发布到 [AppSource，](https://appsource.microsoft.com)使其在 Microsoft Teams 应用目录和 Web 上可用。 在高级别上，将应用提交到 AppSource 的过程如下所示：

1. 按照设计指南开发 [应用](~/concepts/design/understand-use-cases.md)。 选项卡必须遵循桌面、Web 和移动的选项卡[设计](~/tabs/design/tabs.md)[指南](~/tabs/design/tabs-mobile.md)。 机器人必须遵循机器人 [设计指南](~/bots/design/bots.md)。
1. 确保你的应用符合 Microsoft Teams [的应用验证](/legal/marketplace/certification-policies) 策略。 
1. 使用清单验证 [工具测试你的应用](prepare/submission-checklist.md#teams-app-validation-tool)。
1. 在合作伙伴 [中心中](/office/dev/store/open-a-developer-account) 设置 [开发人员帐户](https://support.microsoft.com/help/4499930/partner-center-overview)。 *另请参阅*[常见问题部分中的"](#how-do-i-create-a-partner-center-account)如何创建合作伙伴中心帐户"。
1. 按照提交清单准备应用 [进行提交](prepare/submission-checklist.md)。
1. 查看 [失败最多的测试用例，以便更快地进行应用质量审批](prepare/frequently-failed-cases.md)。
1. 通过合作伙伴中心将程序包[提交到 AppSource。](/office/dev/store/use-partner-center-to-submit-to-appsource)
1. 在合作伙伴中心仪表板上跟踪审批流程。 *请参阅*[合作伙伴中心概述](https://support.microsoft.com/help/4499930/partner-center-overview)。
1. 提交后，请查看有关 [维护和支持已发布应用的指南](post-publish/overview.md)。

>[!NOTE]
>
>- 你的 Teams 应用必须是移动响应式应用，并且符合 [iOS](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#-mobile-responsiveness-no-direct-upsell-or-payment) 和 Android (移动操作系统上的) 。 
>- 如果你的 Teams 应用包含机器人，你必须遵守 Bot 开发人员框架 [行为准则](https://aka.ms/bf-conduct)。
>- 如果你的应用包含 Office 365 连接器，则其他条款可能适用。 请参阅[连接器开发人员仪表板](https://aka.ms/connectorsdashboard)[和应用开发人员协议](https://sellerdashboard.microsoft.com/Assets/Content/Agreements/Office_Store_Seller_Agreement_20120927.htm)。
>- 若要使你的应用可用于政府社区云 (GCC) 用户，并避免应用商店中重复的应用列表，身份验证过程或流必须标识用户，并路由到 GCC 用户的指定或预期内容 URL。

## <a name="faqs--teams-apps-and-partner-account-verification-process-in-partner-center"></a>常见问题解答 — 合作伙伴中心中的 Teams 应用和合作伙伴帐户验证过程

## <a name="how-do-i-create-a-partner-center-account"></a>如何创建合作伙伴中心帐户？

创建合作伙伴中心帐户的方法有两种：

- 如果你是合作伙伴中心的新用户，并且 Microsoft 网络中没有帐户，则使用合作伙伴中心注册 [页面创建一个帐户](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment)。
- 如果你已在合作伙伴网络中注册，请直接使用现有注册页面在合作伙伴 [ 中心创建帐户](/office/dev/store/)。

## <a name="what-if-i-cannot-find-my-office-store-account-in-partner-center"></a>如果我在合作伙伴中心中找不到我的 Office 应用商店帐户，该做什么？

打开合作伙伴 [中心支持票证](https://partner.microsoft.com/support/v2/?stage=1) ，然后从下拉菜单中选择以下内容：

| 菜单 | 选项 |
| -------   | -------  |
|类别| 商业市场|
| 主题 | 一般市场帮助和帮助问题 |
| 子标题| Office 加载项 |

## <a name="where-can-i-get-support-for-my-partner-center-account-issues"></a>在哪里可以获取对合作伙伴中心帐户问题的支持？

访问 [发布者支持页面](https://aka.ms/marketplacepublishersupport) ，搜索问题主题并查找指南。 如果提供的指南没有帮助，请提出 [合作伙伴中心支持票证](/azure/marketplace/partner-center-portal/support#how-to-open-a-support-ticket)。

## <a name="how-do-i-manage-my-office-store-account-in-partner-center"></a>如何在合作伙伴中心管理我的 Office 应用商店帐户？

通过 [合作伙伴中心访问管理 Office 应用商店帐户，](/office/dev/store/manage-account-settings-and-profile) 获得指导。

## <a name="how-do-i-add-my-phone-number-to-the-partner-profile-contact-section"></a>如何将我的电话号码添加到合作伙伴配置文件联系人部分？

电话号码包含三个部分：国家/地区代码、区号和电话号码。 如果电话号码不包含区号，则保留第二个框为空，并填写第三个框。

## <a name="how-do-i-manage-my-account-settings-and-partner-profile-in-partner-center"></a>如何在合作伙伴中心管理我的帐户设置和合作伙伴配置文件？

访问 ["管理帐户设置和配置文件信息](/windows/uwp/publish/manage-account-settings-and-profile#additional-settings-and-info) "页，获取有关管理合作伙伴中心帐户设置的指南。

## <a name="why-do-i-receive-the-message-this-account-is-not-publish-eligible-when-i-try-to-submit-my-add-in-through-partner-center"></a>当我尝试通过合作伙伴中心提交我的外接程序时，为什么会收到消息"此帐户不符合发布条件"？

帐户验证状态挂起时，您将收到 [上述](/partner-center/verification-responses) 错误消息。 在合作伙伴中心仪表板中检查你的帐户验证  [状态](https://partner.microsoft.com/dashboard)。 选择 **"** 设置"，即页面标题外壳右上角的齿轮图标。 选择 **"开发人员设置**  =>  **帐户**   =>  **帐户设置"。**

![合作伙伴中心帐户设置页](../../../assets/images/partner-center-accts-page.png)

![合作伙伴中心验证状态](../../../assets/images/partner-center-verification-status.png)

每个必需步骤（如 **电子邮件** 所有权、雇佣验证和业务验证）的状态都显示在帐户验证过程中。 验证过程完成后，配置文件页上注册的验证 *状态会从* 挂起状态更改为 *已授权*。 不再显示过程步骤。

![合作伙伴中心验证错误](../../../assets/images/partner-center-acct-verification-error.png)

## <a name="what-is-verified-in-the-partner-center-account-verification-process-and-how-to-respond"></a>合作伙伴中心帐户验证过程中验证了哪些功能以及如何响应？
有三个验证区域：**电子邮件所有权****、雇佣** 关系 **和业务**。 有关验证过程详细信息，请参阅"已 [验证"和如何响应](/partner-center/verification-responses#what-is-verified-and-how-to-respond)。
如果你是主要联系人、全局管理员或帐户管理员，请转到合作伙伴配置文件以监视验证状态并跟踪进度。

验证过程完成后，配置文件页上注册的验证 *状态会从* 挂起状态更改为 *已授权*。 授权后，处理步骤及其状态在页面上不再可用。 主要联系人在验证完成后的几天内收到来自 Microsoft 的电子邮件。

## <a name="my-account-verification-status-has-not-advanced-beyond-email-ownership-in-the-partner-center-how-should-i-proceed"></a>我的帐户验证状态未超出合作伙伴中心中的电子邮件所有权。 如何继续？

在 **电子邮件所有权** 验证过程中，验证电子邮件将发送到主要联系人电子邮件地址。 检查主联系人收件箱中是否包含来自 **<span>maccount@ microsoft</span>.com** 的电子邮件，主题行为"需要操作：使用 *Microsoft 验证你的电子邮件帐户"。* 完成电子邮件验证过程。 验证电子邮件将发送到合作伙伴中心帐户设置页面中列出的电子邮件地址。

> [!NOTE]
> * 电子邮件验证链接仅在七天内有效。 
> * 可以通过访问合作伙伴配置文件页面并选择"重新发送验证电子邮件"链接，请求我们 **重新发送电子邮件** 。
> * 若要确保收到电子邮件，请安全microsoft.com安全域发送的电子邮件，并检查垃圾邮件文件夹。

## <a name="how-do-i-get-further-support-for-my-account-related-issues"></a>如何进一步支持我的帐户相关问题？

有关 [创建支持票证](/azure/marketplace/partner-center-portal/support) 的指导和步骤，请访问"合作伙伴中心"页面中对商业市场计划的支持。

## <a name="ive-checked-my-mail-folders-and-havent-received-the-verification-email-what-must-i-do-next"></a>我检查了邮件文件夹，但没有收到验证电子邮件。 接下来必须做什么？

请尝试执行以下操作：
* 检查垃圾邮件文件夹。
* 清除浏览器缓存，转到合作伙伴中心帐户仪表板，然后选择"重新发送验证 **电子邮件** "链接，将验证电子邮件重新发送到你的电子邮件地址。
* 请尝试从不同的 **浏览器访问** "重新发送验证电子邮件"链接。
* 与 IT 部门合作，确保电子邮件服务器不会阻止验证电子邮件。
* 调整服务器的垃圾邮件筛选器，以允许或安全列出来自 **maccount@microsoft。 <span></span>com**。

## <a name="how-long-does-the-employment-verification-process-usually-take"></a>雇佣验证过程通常需要多久？

如果所有提交的详细信息都正确，则雇佣验证过程需要大约两个小时才能完成。

## <a name="how-long-does-the-business-verification-process-usually-take"></a>业务验证过程通常需要多久？

如果提交所有所需的文档，则业务验证需要一到两个工作日才能完成。

## <a name="if-i-reach-out-to-the-support-team-will-my-ticket-be-expedited"></a>如果我联系支持团队，我的票证是否将被加速？

支持票证在一周内解决。 检查发送到在引发支持票证时提供的电子邮件 ID 的更新。

## <a name="my-issue-is-not-listed-here-are-there-other-pages-i-can-reference-for-partner-center-issues"></a>我的问题未在此处列出。 我是否有其他页面可以参考合作伙伴中心问题？

有关更多 [帮助，请参阅商业](/azure/marketplace/) 市场文档。

## <a name="ive-created-a-support-ticket-it-has-been-7-business-days-and-i-havent-received-an-update-where-can-i-get-additional-help"></a>我创建了一个支持票证，已经 7 个工作日，并且我没有收到更新。 在哪里可以获取其他帮助？

将电子邮件 **<teamsubm@microsoft.com>** 发送到以下详细信息：

* **主题行**：合作伙伴中心帐户问题<App_Name> (指定应用名称) 。
* **电子邮件正文**：
    * 支持票证编号
    * 卖家 ID
    * 如果可能，问题 (屏幕截图) 
    
## <a name="app-category-mapping"></a>应用类别映射

| Teams 类别       | 电脑类别  |
|:---------------------|:---------------|
| 分析和 BI | 分析、数据可视化和 BI |
| 开发人员和 IT | 开发人员工具、IT 管理员 |
| 教育 | 教育 |
| 人力资源 | 人力资源和招聘 |
| 工作效率 | 内容管理、文件和文档、生产力、培训和教程以及实用程序 |
| 项目管理 | 通信、项目管理、工作流和业务管理 |
| 销售和支持 | 客户和联系人管理、客户支持、财务管理、销售和市场营销 |
| 社交和有趣 | 图像和视频库、生活方式、新闻和天气、社交、旅行和导航 |

>
> [!div class="nextstepaction"]
> [详细了解 Microsoft Teams 的应用验证策略](/legal/marketplace/certification-policies)
