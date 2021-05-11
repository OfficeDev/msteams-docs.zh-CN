---
title: 开发消息传递扩展
description: 介绍如何开始使用邮件扩展Microsoft Teams
ms.topic: overview
localization_priority: Normal
keywords: teams 消息传递扩展消息传递扩展
ms.openlocfilehash: 2301a9af7574c193c7327bb45e38f91bedc73793
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020602"
---
# <a name="develop-messaging-extensions-for-microsoft-teams"></a>开发适用于用户的邮件Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

消息传递扩展是一种功能强大的方法，用户可以从多个用户Microsoft Teams。 通过此功能，用户可以在服务中查询或发布信息，然后以卡片形式将该信息发布至消息中。

![邮件扩展卡示例](~/assets/images/compose-extensions/ceexample.png)

邮件扩展沿撰写框的底部显示。 一些内置，如表情符号、Giphy 和贴纸。 选择 **"更多选项**" (&#8943;) 查看其他消息传递扩展，包括从应用库添加或自己上传的邮件扩展。 

如何使用消息传递扩展？ 下面提供了一些可能性：

* 工作项和 Bug
* 客户支持票证
* 使用情况图表和报告
* 图像和媒体内容
* 销售机会和潜在客户

## <a name="types-of-messaging-extensions"></a>邮件扩展类型

目前，你主要可以创建两种邮件Teams扩展。 以下主题将指导你完成创建它们的过程：

* [基于搜索的消息扩展](~/resources/messaging-extension-v3/search-extensions.md)：在服务中查询信息并将其插入到邮件中。 示例：查找工作项
* [基于操作的消息扩展](~/resources/messaging-extension-v3/create-extensions.md)：从用户收集信息并张贴到第三方服务。 示例：创建工作项
