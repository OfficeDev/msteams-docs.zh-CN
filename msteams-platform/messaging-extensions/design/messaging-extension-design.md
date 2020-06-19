---
title: 邮件扩展的设计准则
description: 介绍创建邮件扩展的准则
keywords: 团队设计准则参考邮件扩展提示最佳实践
author: EmilyyC
ms.author: qinch
ms.openlocfilehash: cf2862b8c8544efcab21616c420d66937fb7406a
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "44801121"
---
# <a name="start-sharing-with-powerful-messaging-extensions"></a>开始与强大的邮件扩展进行共享

邮件扩展用于共享可操作内容。 此功能表示在我们的堆栈中投资回报率最高（ROI）。 邮件扩展在聊天和频道中工作、支持多个查询终结点、启用新实体的创建以及使用链接 unfurling 创建自定义链接预览。 困难在于，虽然功能强大且非常有用，但它并不容易被发现。 本指南将帮助您创建可供多个用户使用的、易于使用的邮件扩展。

## <a name="design-guidelines"></a>设计准则

### <a name="show-content-as-a-user-type"></a>将内容显示为用户类型

邮件扩展提供了使用关键字搜索查找可与一个或多个用户共享的可操作内容的唯一方法。 此首选交互允许用户输入具有延迟自动查询的搜索词作为用户类型。 此模型为模拟建议结果和要求用户键入最少字符做了很好的工作。

> [!TIP]
>可能，但不适合要求用户 `enter` `search` 在发送查询时选择或之前。 当后端服务的压力较少时，此模型不是标准模型，可能会混淆用户。

### <a name="consider-zero-term-queries"></a>考虑零术语查询

零术语查询直接由用户操作触发，而不是由用户在搜索框中写入术语。 所有邮件扩展都受益于零期限查询，通常基于用户上次在服务中看到的内容。 优势在于，希望共享用户上次看到的内容相当高的可能性。 其他零术语查询可能基于该服务。 例如， `news` 可能显示最近发布的最近事件和即将到来的新闻扩展。

<img width="450px" title=""新建配置" 选项卡" src="../../assets/images/messaging-extension/zero-term-query.png" />

### <a name="include-link-unfurling"></a>包含链接 unfurling

在团队中共享内容的最常见方法之一是通过超链接，无论它是已在使用中的任务，还是您找到了有趣的视频。 当用户在团队中共享链接时，将显示包括图像、标题或说明的预览。 通过[链接 unfurling](../how-to/link-unfurling.md) ，您现在可以自定义这些预览。 用户在决定使用您的预览后，系统也会提示您安装您的应用程序。 向您的应用程序添加链接 unfurling 功能可大大增加您的应用程序可发现性。

### <a name="highlight-your-messaging-extension"></a>突出显示您的邮件扩展

消息传递扩展并不总是很容易找到。 在应用程序详细信息页面中添加应用屏幕截图和帮助文档，以确保邮件扩展的功能。 您还可以在 bot 教程中添加您的邮件扩展的操作*方法*文档，以突出显示 bot 交互之外的整个应用程序。

### <a name="add-actions-on-card"></a>在卡片上添加操作

不要只向用户显示文本。 具有可与之交互的内容，并执行下一个操作。 例如，"位置" 应用程序不只是在卡片上插入地图，还具有一个按钮，该按钮在选中时将向该位置显示行车路线。 在获取卡片后，用户可以执行更多任务。

<img width="450px" title=""新建配置" 选项卡" src="../../assets/images/messaging-extension/action-on-card.png" />

### <a name="keep-users-in-the-app-context"></a>将用户保留在应用上下文中

如果卡片不够，并且需要提供详细信息的链接，请考虑打开一个选项卡，而不是打开浏览器以获得更好的用户体验。 *请参阅*[扩展您的团队应用程序 wit 自定义选项卡](../../tabs/how-to/add-tab.md)
