---
title: 创建传入 Webhook
author: laujan
description: 介绍如何将传入 Webhook Teams应用程序，以及将外部请求Teams传入 Webhook
keywords: teams 选项卡传出 Webhook
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: c07456288a26e3152a552644b704e2c6e6de38cc
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155263"
---
# <a name="create-incoming-webhook"></a>创建传入 Webhook

传入 Webhook 允许任何外部应用在Teams内容。 这些 Webhook 用作跟踪和通知工具。 它们提供唯一的 URL，你可以将 JSON 有效负载与卡片格式的邮件一起发送到该 URL。 卡片是包含与单个主题相关的内容和操作的用户界面容器。 Teams以下功能内使用卡片：

* 机器人
* 消息传递扩展
* 连接器

## <a name="key-features-of-incoming-webhook"></a>传入 Webhook 的主要功能

下表提供了传入 Webhook 的功能和说明：

| 功能 | 说明 |
| ------- | ----------- |
|使用传入 Webhook 的自适应卡片|自适应卡片可以通过传入 Webhook 发送。 有关详细信息，请参阅使用 [传入 Webhook 发送自适应卡片](../../webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook)。|
|可操作邮件支持|可操作邮件卡在所有邮件组中Office 365，包括Teams。 如果通过卡片发送邮件，则必须使用可操作邮件卡片格式。 有关详细信息，请参阅旧版可[操作邮件卡参考](/outlook/actionable-messages/message-card-reference)[和邮件卡的场](https://messagecardplayground.azurewebsites.net)。|
|独立 HTTPS 消息支持|卡片清晰且一致地提供信息。 任何可以发送 HTTPS POST 请求的工具或框架都可以通过传入 Webhook Teams消息。|
|Markdown 支持|可操作邮件卡中所有文本字段都支持基本 Markdown。 请勿在卡片中使用 HTML 标记。 HTML 会遭忽略并被视为纯文本。|
|作用域配置|传入 Webhook 在通道级别进行范围设置和配置。|
|安全资源定义|邮件的格式设置为 JSON 有效负载。 此声明性消息结构可防止插入恶意代码。|

> [!NOTE]
> * Teams自动程序、消息传递扩展、传入 Webhook 和 Bot Framework 支持自适应卡片，这是一个开放的跨卡平台框架。 目前[，Teams](../../webhooks-and-connectors/how-to/connectors-creating.md)连接器不支持自适应卡片。 但是，可以创建一个将自适应卡片[](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/)张贴到新频道Teams流。
> * 有关卡片和 Webhook 的信息，请参阅[自适应卡片和传入 Webhook。](~/task-modules-and-cards/what-are-cards.md#adaptive-cards-and-incoming-webhooks)

## <a name="create-incoming-webhook"></a>创建传入 Webhook

**将传入 Webhook 添加到 Teams 通道**

1. 转到要添加 Webhook 的频道，然后从顶部导航 &#8226;&#8226;&#8226; 选择"更多选项"。
1. 从 **下拉菜单中选择** "连接器"：

    ![选择连接器](~/assets/images/connectors.png)

1. 搜索"**传入 Webhook"，** 然后选择"添加 **"。**
1. 选择 **"配置**"，提供名称，并上传 Webhook 图像（如果需要）：

    ![配置按钮](~/assets/images/configure.png)

1. 对话框窗口显示映射到通道的唯一 URL。 复制并保存 webhook URL，以将信息Microsoft Teams并选择"完成 **"：**

    ![唯一 URL](~/assets/images/url.png)

webhook 在 Teams 中可用。

> [!NOTE]
> 在Teams"中，设置"成员权限""允许成员创建、更新和删除连接器"，以便任何团队成员都可以添加、修改  >    >  或删除连接器。

## <a name="remove-incoming-webhook"></a>删除传入 Webhook

**从传入 Webhook 通道中删除Teams Webhook**

1. 转到频道。
1. Select &#8226;&#8226;&#8226; **More options** from the top navigation bar.
1. 从 **下拉菜单中选择** "连接器"。
1. 在左侧的"管理 **"下，** 选择"**已配置"。**
1. 选择 **< *"1*>"** 以查看当前连接器的列表：

    ![已配置的 Webhook](~/assets/images/configured.png)

1. 选择要 **删除** 的连接器旁边的"管理"：

    ![管理 webhook](~/assets/images/manage.png)

1. 选择 **"删除"：**

    ![删除 webhook](~/assets/images/remove.png)

    将显示 **"删除配置** "对话框：

    ![删除配置](~/assets/images/removeconfiguration.png)

1. 填写对话框字段和复选框， **然后选择删除**：

    ![最终删除](~/assets/images/finalremove.png)

    Webhook 已从 webhook Teams中删除。

## <a name="see-also"></a>另请参阅

* [创建传出 Webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [创建 Office 365 连接器](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [创建和发送邮件](~/webhooks-and-connectors/how-to/connectors-using.md)
