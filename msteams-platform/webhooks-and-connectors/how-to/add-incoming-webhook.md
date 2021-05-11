---
title: Post external requests to Microsoft Teams with incoming webhooks
author: laujan
description: 如何将传入 Webhook 添加到Teams应用
keywords: teams 选项卡传出 Webhook
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: bc4d768751d34ccf305ef99e126159123a83ef3f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52018416"
---
# <a name="post-external-requests-to-teams-with-incoming-webhooks"></a>Post external requests to Teams with incoming webhooks

## <a name="what-are-incoming-webhooks-in-teams"></a>什么是传入 webhook Teams？

传入 Webhook 是 Teams 中的特殊类型的连接器，可为外部应用提供一种在团队频道中共享内容的简单方法，并且通常用作跟踪和通知工具。 Teams提供一个唯一 URL，您通常会以卡片格式将 JSON 有效负载与要 POST 的邮件一起发送到该 URL。 卡片是用户界面 (UI) 容器，其中包含与单个主题相关的内容和操作，也是以一致的方式显示邮件数据的一种方式。 Teams三个功能内使用卡片：

* 机器人
* 消息传递扩展
* 连接器

## <a name="incoming-webhook-key-features"></a>传入 Webhook 关键功能

| 功能 | 说明 |
| ------- | ----------- |
|作用域配置|传入 Webhook 的范围和配置在频道级别 (例如，传出 Webhook 的范围和配置在团队级别) 。|
|安全资源定义|邮件的格式设置为 JSON 有效负载。 此声明性消息结构可防止注入恶意代码，因为客户端上没有执行代码。|
|可操作邮件支持|如果选择通过卡片发送邮件，则必须使用可 **操作邮件卡片** 格式。 可操作邮件卡在所有邮件组中Office 365，包括Teams。 以下是指向旧版可[操作邮件卡参考和](/outlook/actionable-messages/message-card-reference)[邮件卡片的编号的链接](https://messagecardplayground.azurewebsites.net)。|
|独立 HTTPS 消息支持| 卡片是一种以清晰且一致的方式呈现信息的方式。 任何可以发送 HTTPS POST 请求的工具或框架都可以通过传入 webhook Teams消息。|
|Markdown 支持|可操作邮件卡中所有文本字段都支持基本 Markdown。 **请勿在卡片中使用 HTML 标记**。 HTML 会遭忽略并被视为纯文本。|

> [!Note]
> Teams聊天机器人、消息传递扩展、传入 Webhook 和 Bot Framework 支持自适应卡片，这是一个开放的跨卡平台框架。 [Teams连接器](../../webhooks-and-connectors/how-to/connectors-creating.md)当前不支持自适应卡片。 但是，可以创建一个将[自适应卡片张贴](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/)到Teams流。

## <a name="add-an-incoming-webhook-to-a-teams-channel"></a>将传入 Webhook 添加到Teams通道

> [!Important]  
> 如果已选择设置"成员权限""允许成员创建、更新和删除连接器"，则任何团队成员都可以添加、修改  =>    =>  或删除连接器。

1. 导航到要添加 Webhook 的通道，然后从顶部导航栏中 (&#8226;&#8226;&#8226;) 选择 *"更多选项* "。
1. 从 **下拉菜单中选择**"连接器"，然后搜索"传入 **Webhook"。**
1. 选择 **"配置** "按钮，提供名称，并（可选）为 Webhook 上传图像头像。
1. 对话框窗口将显示将映射到通道的唯一 URL。 请确保复制 **并保存 URL，** 您需要将其提供给外部服务。
1. 选择" **完成"** 按钮。 webhook 将在团队频道中提供。

## <a name="remove-an-incoming-webhook-from-a-teams-channel"></a>从网络通道中删除Teams webhook

1. 导航到添加 webhook 的通道，然后从顶部导航 (&#8226;&#8226;&#8226;) *选择* "更多选项"。
1. 从 **下拉菜单中选择** "连接器"。
1. 在左侧的"管理 **"下，** 选择"**已配置"。**
1. 选择 *配置为* 查看当前连接器列表的号码。
1. 选择要 **删除** 的连接器旁边的"管理"。
1. 选择 **"删除** "按钮，你将看到"删除 *配置"* 对话框。
1. （可选）在选择"删除"按钮之前填写对话框字段 **和** 复选框。 Webhook 将从团队频道中删除。

## <a name="distribution"></a>分发

有三个选项用于分发传入的 Webhook：

* 直接为团队设置传入 Webhook。
* 添加配置页面，将传入的 Webhook 包装在 [O365 连接器中](~/webhooks-and-connectors/how-to/connectors-creating.md)
* 将连接器打包并发布为 [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) 提交的一部分。

## <a name="learn-more"></a>了解详细信息

* [将邮件发送到连接器和 Webhook](~/webhooks-and-connectors/how-to/connectors-using.md)
