---
title: 发布后
description: 发布应用程序后的操作
keywords: Teams 发布后更新证书
ms.openlocfilehash: d2cc6c5427c5b4f7320f0ec2e022f2c69467a33d
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819152"
---
# <a name="maintain-and-support-your-published-app"></a>维护和支持已发布的应用 

在应用程序获得批准并在公共应用目录中列出后，可以通过完成 Microsoft 365 应用合规性计划或在网站上添加下载按钮来提高覆盖范围。

## <a name="microsoft-365-certified"></a>Microsoft 365 认证

[Microsoft 365 应用合规性计划是](./application-certification.md)应用安全性和合规性的三层方法。 每个层基于下一层 - 提供分层计划来满足客户需求。 可通过访问合规性页面，了解有关 Teams 应用的安全性和合规 [状态的详细信息](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps)。

## <a name="add-a-download-button-to-your-product-site"></a>将下载按钮添加到产品网站

如果你的应用在 Microsoft Teams 应用商店中，则可为网站生成一个链接，用于启动 Teams 并显示许可和安装对话框，以便用户添加应用。
格式为：  `https://teams.microsoft.com/l/app/<appId>` 其中 appID 是其在提交清单中声明的 GUID。
示例： `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` 是安装 Trello 的链接。

## <a name="updating-your-existing-teams-app"></a>更新现有 Teams 应用

* 不要使用" *添加新应用"* 按钮重新提交应用。 改为在"概述"选项卡上为你的应用使用磁贴。
* 更新后清单中的 appId 应与当前清单中的 appId 相同，并具有增加的版本号。
* 当你对提交进行任何清单更改时，请增加清单中的版本号。
* 要求更新后的提交执行新的审查和验证流程。

## <a name="app-updates-and-the-user-consent-flow"></a>应用更新和用户同意流

当用户安装您的应用程序的第一个操作时，他们所执行的操作就是向应用授予访问服务和应用完成工作所需的信息的权限。 在大多数情况下，完成应用更新后，新版本将自动为最终用户显示。 但是，会有一些 Teams 应用 [清单更新](../../../../resources/schema/manifest-schema.md) 来要求用户接受才能完成并可以重新触发此同意行为：

 >[!div class="checklist"]
>
> * 已添加或删除自动程序。
> * 已更改的现有自动程序的 `botId` 唯一值。
> * 已有的机器人的 `isNotificationOnly` 布尔值已更改。
> * 已有的机器人的 `supportsFiles` 布尔值已更改。
> * 添加或删除 `composeExtensions` () 或) 消息扩展。
> * 添加了新的连接器。
> * 添加了新的静态/个人选项卡。
> * 添加了新的可配置组/频道选项卡。
> * 值 `webApplicationInfo` 已更改。
>
