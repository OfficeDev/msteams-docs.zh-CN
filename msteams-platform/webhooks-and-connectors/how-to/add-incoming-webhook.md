---
title: 向具有传入 webhook 的 Microsoft 团队发布外部请求
author: laujan
description: ''
keywords: 团队选项卡传出 webhook *
ms.topic: conceptual
ms.author: laujan
ms.openlocfilehash: c2b3f5dd581441f89aff344c35fe7e110d4d2e68
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673429"
---
# <a name="post-external-requests-to-teams-with-incoming-webhooks"></a>向具有传入 webhook 的团队发布外部请求

## <a name="what-are-incoming-webhooks-in-teams"></a>哪些是团队中的传入 webhook？

传入 webhook 是在团队中提供的一种特殊类型的连接器，可提供一种简单的方法，让外部应用程序在团队频道中共享内容，并经常用作跟踪和通知工具。 团队提供一个唯一的 URL，您将 JSON 有效负载与要发布的邮件（通常采用卡片格式）一起发送。 卡片是用户界面（UI）容器，其中包含与单个主题相关的内容和操作，并且是以一致的方式显示邮件数据的一种方式。 团队使用三种功能中的卡片：

* 机器人
* 消息扩展
* 连接器

## <a name="incoming-webhook-key-features"></a>传入 webhook 密钥功能

| 功能 | 说明 |
| ------- | ----------- |
|作用域配置|传入 webhook 的范围和配置在通道级别（例如，传出 webhook 的范围和在团队级别配置）。|
|安全资源定义|将邮件格式化为 JSON 有效负载。 此声明性邮件结构阻止了恶意代码的注入，因为在客户端上没有执行任何代码。|
|可操作邮件支持|如果选择通过卡片发送邮件，则必须使用可**操作邮件卡片**格式。 所有 Office 365 组（包括团队）都支持可操作邮件卡。 下面是指向旧版可[操作邮件卡参考](/outlook/actionable-messages/message-card-reference)和[邮件卡样本](https://messagecardplayground.azurewebsites.net)的链接。|
|独立 HTTPS 消息支持| 卡片是以清晰一致的方式呈现信息的绝佳方式。 任何可发送 HTTPS POST 请求的工具或框架都可以通过传入 webhook 向团队发送邮件。|
|Markdown 支持|可操作邮件卡中的所有文本字段都支持基本 Markdown。 **请勿在卡片中使用 HTML 标记**。 将忽略 HTML 并将其视为纯文本。|

> [!Note]  
> 团队 bot、邮件扩展和 Bot 框架支持自适应卡，即开放式跨卡片平台框架。 工作组连接器目前不支持自适应卡片。 但是，可以创建将自适应卡发布到团队频道的[流](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/)。

## <a name="add-an-incoming-webhook-to-a-teams-channel"></a>将传入 webhook 添加到团队频道

> [!Important]  
> 如果您的团队的**设置** => **成员权限** => **允许成员创建、更新和删除连接器**，则任何团队成员都可以添加、修改或删除连接器。

1. 导航到要在其中添加 webhook 的通道，并从顶部导航栏中选择 "（&#8226;&#8226;&#8226;）*更多选项*"。
1. 从下拉菜单中选择 "**连接器**"，并搜索**传入的 Webhook**。
1. 选择 "**配置**" 按钮，提供一个名称，并为 webhook 上传图像头像（可选）。
1. 对话框窗口将提供一个将映射到通道的唯一 URL。 请确保**复制并保存该 URL**-您需要将其提供给外部服务。
1. 选择 "**完成**" 按钮。 将在团队频道中提供 webhook。

## <a name="remove-an-incoming-webhook-from-a-teams-channel"></a>从团队频道中删除传入 webhook

1. 导航到添加了 webhook 的通道，然后从顶部导航栏中选择（&#8226;&#8226;&#8226;）*更多选项*。
1. 从下拉菜单中选择 "**连接器**"。
1. 在左侧的 "**管理**" 下，选择 "**已配置**"。
1. 选择配置为查看当前连接器列表的*号码*。
1. 选择要删除的连接器旁边的 "**管理**"。
1. 选择 "**删除**" 按钮，将显示 "*删除配置*" 对话框。
1. （可选）在选择 "**删除**" 按钮之前填写对话框字段和复选框。 将从团队通道中删除 webhook。

## <a name="distribution"></a>分发

您有三个用于分发传入 webhook 的选项：

* 为你的团队直接设置传入 webhook。
* 添加配置页面并将传入 webhook 包装在[O365 连接器](~/webhooks-and-connectors/how-to/connectors-creating.md)中
* 将连接器打包并发布为您的[AppSource](~/concepts/deploy-and-publish/office-store-guidance.md)提交的一部分。

## <a name="learn-more"></a>了解更多

* [将邮件发送到连接器和 Webhook](~/webhooks-and-connectors/how-to/connectors-using.md)