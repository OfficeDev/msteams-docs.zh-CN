---
title: 维护和支持已发布的应用
description: 在应用商店和 AppSource 上列出应用商店后Teams的考虑。
ms.topic: conceptual
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 8e4656ea7ca9f373123026a50ecb837d1a64e3fa
ms.sourcegitcommit: 60561c7cd189c9d6fa5e09e0f2b6c24476f2dff5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2021
ms.locfileid: "52230915"
---
# <a name="maintain-your-published-microsoft-teams-app"></a>维护已发布Microsoft Teams应用程序

在应用商店中Microsoft Teams应用后，开始考虑如何继续维护应用并增加下载量和使用。

## <a name="publish-updates-to-your-app"></a>将更新发布到应用

你可以向应用提交更改 (如合作伙伴中心中的新功能) 元数据。 这些更改需要新的审阅过程。

发布更新时，请确保以下各项：

* 不要更改应用 ID。
* 递增应用的版本号。
* 在合作伙伴中心中，不要选择" **添加新应用** "以执行更新。 改为转到应用页面。

### <a name="app-updates-requiring-user-consent"></a>需要用户同意的应用更新

当用户安装你的应用时，他们必须向应用授予访问应用正常运行所需的服务和信息的权限。 在大多数情况下，用户只需执行一次此操作，并自动安装新版本的应用。

但是，如果你对应用进行以下任何更改，则现有用户必须接受另一个权限请求才能安装更新：

* 添加或删除机器人。
* 更改机器人 ID。
* 修改机器人的单向通知配置。
* 修改自动程序对上载和下载文件的支持。
* 添加或删除邮件扩展。
* 添加个人选项卡。
* 添加频道和组选项卡。
* 添加连接器。
* 修改与 Azure AD Azure Active Directory (应用) 相关的配置。 有关详细信息，请参阅 [`webApplicationInfo`](~/resources/schema/manifest-schema.md#webapplicationinfo) 。

## <a name="fix-issues-with-your-published-app"></a>修复已发布应用的问题

Microsoft 对应用商店中列出的应用运行每日Teams测试。 如果发现你的应用的问题，我们会通过详细报告联系你，以了解如何重现这些问题以及解决这些问题的建议。 如果无法修复已规定时间线中的问题，你的应用一览可能会从应用商店中删除。

## <a name="promote-your-app-on-another-site"></a>在另一个网站上推广你的应用

当你的应用在应用商店Teams时，你可以创建一个链接来启动Teams并显示用于安装应用的对话框。 例如，可以在产品的营销页面上包含此链接和下载按钮。

使用应用 ID 附加的以下 URL 创建链接 `https://teams.microsoft.com/l/app/<your-app-id>` ：。

## <a name="complete-microsoft-365-certification"></a>完成Microsoft 365认证

[Microsoft 365](/microsoft-365-app-certification/docs/certification)认证可保证当在 Office 应用 生态系统中安装第三方 Office 应用 或外接程序时，数据和隐私Microsoft 365受保护。 认证确认你的应用与 Microsoft 技术兼容，符合云应用安全最佳做法，并且受 Microsoft 支持。

## <a name="see-also"></a>另请参阅

[通过 Microsoft 商业市场利用应用盈利](/office/dev/store/monetize-addins-through-microsoft-commercial-marketplace)
