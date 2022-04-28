---
title: 开发消息扩展
description: 介绍如何在Microsoft Teams中开始使用消息扩展
ms.topic: overview
ms.localizationpriority: medium
keywords: teams 消息扩展消息扩展
ms.openlocfilehash: b1d219bbb8e79a99836ad20b35442e10ec537c4a
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104329"
---
# <a name="develop-message-extensions-for-microsoft-teams"></a>为Microsoft Teams开发消息扩展

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

消息扩展是用户从Microsoft Teams参与应用的强大方式。 借助此功能，用户可以查询或发布服务中的信息，并将该信息以卡的形式直接发布到邮件中。

![消息扩展卡的示例](~/assets/images/compose-extensions/ceexample.png)

消息扩展显示在撰写框的底部。 其中一些是内置的，如表情符号、Giphy 和贴纸。 选择 **“更多选项** ” (**&#8943;**) 按钮查看其他消息扩展，包括从应用库添加或自行上传的消息扩展。

如何使用消息扩展？ 下面是一些可能性：

* 工作项和 bug
* 客户支持票证
* 使用情况图表和报表
* 图像和媒体内容
* 销售机会和潜在顾客

## <a name="types-of-message-extensions"></a>消息扩展的类型

目前主要可以为Teams创建两种类型的消息扩展。 以下主题将指导你完成创建过程：

* [基于搜索的消息扩展插件](~/resources/messaging-extension-v3/search-extensions.md)：查询服务中的信息并将其插入消息中。 示例：查找工作项
* [基于操作的消息扩展插件](~/resources/messaging-extension-v3/create-extensions.md)：从用户收集信息并发布到第三方服务。 示例：创建工作项
