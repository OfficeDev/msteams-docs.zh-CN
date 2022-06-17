---
title: 开发消息扩展
description: 在本模块中，了解如何在Microsoft Teams中开始使用消息扩展
ms.topic: overview
ms.localizationpriority: medium
ms.openlocfilehash: c81df30b71bbdba19842e45f06b4c9bb930e4c0d
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143975"
---
# <a name="develop-message-extensions-for-microsoft-teams"></a>为Microsoft Teams开发消息扩展

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

消息扩展是用户从Microsoft Teams参与应用的强大方式。 借助此功能，用户可以查询或帖子服务中的信息，并将该信息以卡片的形式直接帖子到邮件中。

![消息扩展卡的示例](~/assets/images/compose-extensions/ceexample.png)

消息扩展显示在撰写框的底部。 其中一些是内置的，如表情符号、gif 和贴纸。 选择 **“更多选项** ” (**&#8943;**) 按钮查看其他消息扩展，包括从应用库添加或自行上传的消息扩展。

如何使用消息扩展？ 下面是一些可能性：

* 工作项和 bug。
* 客户支持票证。
* 使用情况图表和报表。
* 图像和媒体内容。
* 销售机会和潜在顾客。

## <a name="types-of-message-extensions"></a>邮件扩展类型

目前主要可以为Teams创建两种类型的消息扩展。 以下主题将指导你完成创建过程：

* [基于搜索的消息扩展插件](~/resources/messaging-extension-v3/search-extensions.md)：查询服务中的信息并将其插入消息中。 示例：查找工作项
* [基于操作的消息扩展](~/resources/messaging-extension-v3/create-extensions.md)：从用户收集信息，并将帖子到第三方服务。 示例：创建工作项
