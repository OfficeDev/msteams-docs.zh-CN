---
title: 开发邮件扩展
description: 介绍如何在 Microsoft 团队中开始使用邮件扩展功能
keywords: 团队邮件传递扩展邮件扩展
ms.openlocfilehash: 6ba8f73d40f795a83f28707ef89c207c5d51d67c
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673022"
---
# <a name="develop-messaging-extensions-for-microsoft-teams"></a>为 Microsoft 团队开发邮件扩展

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

邮件扩展是用户与 Microsoft 团队中的应用程序进行接洽的一种强大方式。 通过此功能，用户可以在服务中查询信息或向其发送信息，并将该信息以卡片形式发布到邮件中。

![邮件扩展卡的示例](~/assets/images/compose-extensions/ceexample.png)

邮件扩展将沿着 "撰写" 框的底部显示。 中内置了几个，如表情符号、Giphy 和不干胶标签。 选择 "**更多选项**" （**&#8943;**）按钮以查看其他邮件扩展，包括从应用程序库添加的那些扩展或自行上载。

如何使用邮件扩展？ 以下是几种可能的情况：

* 工作项和 bug
* 客户支持票证
* 使用率图表和报告
* 图像和媒体内容
* 销售机会和潜在客户

## <a name="types-of-messaging-extensions"></a>邮件扩展类型

目前，可以为团队创建两种类型的邮件扩展。 下列主题将指导您完成创建它们的过程：

* [基于搜索的邮件扩展](~/resources/messaging-extension-v3/search-extensions.md)：查询服务的信息并将其插入到邮件中。 示例：查找工作项
* [基于操作的邮件扩展](~/resources/messaging-extension-v3/create-extensions.md)：收集用户的信息并发布到第三方服务。 示例：创建工作项
