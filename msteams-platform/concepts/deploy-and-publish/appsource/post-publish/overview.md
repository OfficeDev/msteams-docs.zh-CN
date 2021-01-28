---
title: 维护和支持已发布的应用
description: 发布应用后要执行哪些操作
ms.topic: how-to
keywords: teams 发布后更新认证应用更新清单
ms.openlocfilehash: ce63b840307f7e12a5cd05a1c67aed017cf6199b
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014325"
---
# <a name="maintain-and-support-your-published-app"></a>维护和支持已发布的应用 

在公共应用目录中批准并列出应用后，可以通过完成 Microsoft 365 应用合规性计划或在网站上添加下载按钮来扩大范围。

## <a name="microsoft-365-certified"></a>Microsoft 365 认证

[Microsoft 365 应用合规性计划](./application-certification.md)是应用安全性和合规性的三层方法。 每一层都构建于下一层 - 提供分层计划以满足客户的需求。 通过访问合规性页面，可以了解有关 Teams 应用的安全性和合规性[状态。](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps)

## <a name="add-a-download-button-to-your-product-site"></a>将下载按钮添加到产品网站

如果你的应用位于 Microsoft Teams 全局应用商店中，你可以为网站生成一个链接，用于启动 Teams，并显示用户添加应用的同意和安装对话框。
格式为：其中 appID 是它们在提交的清单  `https://teams.microsoft.com/l/app/<appId>` 中声明的 GUID。
示例： `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` 是安装 Trello 的链接。

## <a name="updating-your-existing-teams-app"></a>更新现有 Teams 应用

* 请勿使用" *添加新应用"* 按钮重新提交应用。 改为在"概述"选项卡上为你的应用使用磁贴。
* 更新后的清单中的 appId 应该与当前清单中的相同，并递增版本号。
* 如果你对提交（包括应用名称或清单中任何元数据）进行更改，则增加清单中的版本号。
* 需要更新的提交才能接受新的审阅和验证过程。

## <a name="app-updates-and-the-user-consent-flow"></a>应用更新和用户同意流

当用户安装您的应用程序时，他们首先会同意授予应用访问权限，以访问应用执行其作业所需的服务和信息。 在大多数情况下，完成应用更新后，将为最终用户自动显示新版本。 但是，Teams 应用清单有一[](../../../../resources/schema/manifest-schema.md)些更新需要用户接受才能完成，并可以重新触发此同意行为：

 >[!div class="checklist"]
>
> * 已添加或删除自动程序。
> * 现有自动程序的唯 `botId` 一值已更改。
> * 现有聊天机器人 `isNotificationOnly` 的布尔值已更改。
> * 现有聊天机器人 `supportsFiles` 的布尔值已更改。
> * 已添加或删除 `composeExtensions` () 邮件扩展名。
> * 添加了一个新连接器。
> * 添加了新的静态/个人选项卡。
> * 添加了新的可配置组/频道选项卡。
> * 值 `webApplicationInfo` 已更改。
>

### <a name="images-of-user-consent-flow"></a>用户同意流程的图像：

**设置连接器** - 此屏幕将仅为 Teams 用户显示。

![同意流设置连接器关系图](../../../../assets/images/connector-teams-consentflow.png)

**用户同意流** - 此屏幕对于个人和组范围都很常见。 在此处，选中"**代表你的组织** 同意"复选框，然后选择"**接受"。**

![权限图](../../../../assets/images/user-consent-flow.png)
