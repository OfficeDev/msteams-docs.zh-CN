---
title: 发布发布
description: 发布应用程序后要执行的操作
keywords: 团队发布更新证书
ms.openlocfilehash: 887e18ac7e27cf12aa4319ac240e42f21f05fd75
ms.sourcegitcommit: e355f59d2d21a2d5ae36cc46acad5ed4765b42e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "45021571"
---
# <a name="maintain-and-support-your-published-app"></a>维护和支持您发布的应用程序 

在应用程序获得批准并在公用应用程序目录中列出后，可以通过完成 Microsoft 365 应用合规性计划或在网站上添加 "下载" 按钮来提高您的访问范围。

## <a name="m365-certified"></a>M365 认证

[Microsoft 365 应用合规性计划](./application-certification.md)是一种用于应用程序安全性和合规性的三层方法。 每个层都基于下一个分层计划，以满足客户的需求。 您可以通过访问[合规性页面](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps)来了解有关团队应用程序的安全和合规性状况的详细信息。

## <a name="add-a-download-button-to-your-product-site"></a>将 "下载" 按钮添加到产品网站

如果您的应用程序位于 Microsoft 团队存储中，则可以为您的网站生成一个链接，用于启动团队并显示用户添加应用程序的许可和安装对话框。
格式为： `https://teams.microsoft.com/l/app/<appId>` 其中 appID 是它们在提交的清单中声明的 GUID。
示例： `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` 是用于安装 Trello 的链接。

## <a name="updating-your-existing-teams-app"></a>更新现有团队应用程序

* 请勿使用 "*添加新应用*" 按钮重新提交您的应用程序。 改为对 "概述" 选项卡上的应用程序使用磁贴。
* 更新后的清单中的 appId 应与当前清单中的 appId 相同，并增加了版本号。
* 如果对提交内容进行任何清单更改，请增加清单中的版本号。
* 需要进行更新的提交，以进行新的审阅和验证过程。

## <a name="app-updates-and-the-user-consent-flow"></a>应用程序更新和用户同意流程

当用户安装您的应用程序时，他们所做的第一件事是同意授予应用程序访问应用程序执行其工作所需的服务和信息的权限。 在大多数情况下，在完成应用更新后，最终用户将自动显示新版本。 但是，对[团队应用程序清单](../../../../resources/schema/manifest-schema.md)的一些更新需要用户接受才能完成，并且可能会重新触发此同意行为：

 >[!div class="checklist"]
>
> * 添加或删除了一个 bot。
> * 现有 bot 的唯一 `botId` 值已更改。
> * 现有 bot 的 `isNotificationOnly` boolean 值已更改。
> * 现有 bot 的 `supportsFiles` boolean 值已更改。
> * 添加或删除了邮件扩展（ `composeExtensions` ）。
> * 添加了新的连接器。
> * 添加了一个新的静态/个人选项卡。
> * 添加了一个新的可配置组/通道选项卡。
> * `webApplicationInfo`值已更改。
>
