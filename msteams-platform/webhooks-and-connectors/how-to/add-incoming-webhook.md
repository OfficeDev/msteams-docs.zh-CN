---
title: 创建传入 Webhook
author: laujan
description: 介绍如何将传入 Webhook 添加到 Teams 应用，以及如何使用传入 Webhook 将外部请求发布到 Teams
keywords: Teams 选项卡传出 Webhook
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 308eaf9f08e946f468f02d897ad556681d1cc832
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059761"
---
# <a name="create-incoming-webhook"></a>创建传入 Webhooks

传入 Webhook 允许任何外部应用在 Teams 频道中共享内容。 这些 Webhook 可以用作跟踪和通知工具。 它们提供唯一的 URL，可向其发送 JSON 有效负载，其中包含卡格式的消息。 卡片是包含与单个主题相关的内容和操作的用户界面容器。 Teams 使用以下功能中的卡片：

* 机器人
* 消息传递扩展
* 连接器

## <a name="key-features-of-incoming-webhook"></a>传入 Webhook 的主要功能

下表提供了传入 Webhook 的功能和说明：

| 功能 | Description |
| ------- | ----------- |
|使用传入 webhook 的自适应卡|可以通过传入 Webhook 发送自适应卡片。 有关详细信息，请参阅[使用传入 Webhook 发送自适应卡片](../../webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook)。|
|可操作消息传递支持|包括 Teams 在内的所有 Office 365 组都支持可操作消息卡片。 如果通过卡片发送消息，则必须使用可操作邮件卡格式。 有关详细信息，请参阅[可操作邮件卡参考](/outlook/actionable-messages/message-card-reference)和[消息卡片操场](https://messagecardplayground.azurewebsites.net)。|
|独立 HTTPS 消息传递支持|卡片提供清晰且一致的信息。 任何可以发送 HTTPS POST 请求的工具或框架可以通过传入 Webhook 发送消息到 Teams。|
|Markdown 支持|在可操作消息传递卡片中的所有文本字段都支持基础 Markdown。 请勿在卡片中使用 HTML 标记。 HTML 会遭忽略并被视为纯文本。|
|作用域配置|传入的 Webhook 在通道级别进行作用域化和配置。|
|保护资源定义|消息的格式设置为 JSON 有效负载。 此声明性消息传送结构阻止插入恶意代码。|

> [!NOTE]
> * Teams 机器人、消息传递扩展、传入 Webhook、Bot Framework 支持自适应卡片。 自适应卡片是可在所有平台（如 Windows、Android、iOS 等）中使用的开放式跨卡平台框架。 目前，[Teams 连接器](../../webhooks-and-connectors/how-to/connectors-creating.md)不支持自适应卡片。 但是，可以创建一个将自适应卡片发布到 Teams 频道的[流](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/)。
> * 有关卡片和 Webhook 的详细信息，请参阅[自适应卡片和传入 Webhook](~/task-modules-and-cards/what-are-cards.md#adaptive-cards-and-incoming-webhooks)。

## <a name="create-incoming-webhook"></a>创建传入 Webhooks

**将传入 Webhook 添加到 Teams 频道**

1. 转到要添加 Webhook 的频道，然后选择从顶部导航栏选择 &#8226;&#8226;&#8226; **更多选项**。
1. 从下拉菜单中选择 **连接器**：

    ![选择连接器](~/assets/images/connectors.png)

1. 搜索 **传入 Webhook** 并选择 **添加**。
1. 选择 **配置**，提供名称，并在需要时上传 Webhook 的图像：

    ![“配置”按钮](~/assets/images/configure.png)

1. 对话框窗口显示映射到通道的唯一 URL。 复制并保存 Webhook URL，将信息发送到 Microsoft Teams，然后选择 **完成**：

    ![唯一 URL](~/assets/images/url.png)

Webhook 在 Teams 频道中可用。

可以通过传入 Webhook 或 Office 365 连接器创建和发送可操作邮件。 有关详细信息，请参阅[创建和发送消息](~/webhooks-and-connectors/how-to/connectors-using.md)。

> [!NOTE]
> 在 Teams 中，选择“**设置**” > “**成员权限**” > “**允许成员创建、更新、删除连接器**，以便任何团队成员添加、修改或删除连接器。

## <a name="remove-incoming-webhook"></a>删除传入 Webhook

**从 Teams 频道中删除传入 Webhook**

1. 转到频道。
1. 从顶部导航栏选择 &#8226;&#8226;&#8226; **更多选项**。
1. 从下拉菜单中选择 **连接器**。
1. 在左侧“**管理**”下，选择 **已配置**。
1. 选择 **<*1*> 已配置** 查看当前连接器的列表：

    ![配置的 Webhook](~/assets/images/configured.png)

1. 选择要删除的连接器旁边的 **管理**：

    ![管理 Webhook](~/assets/images/manage.png)

1. 选择“**删除**”：

    ![删除 Webhook](~/assets/images/remove.png)

    **删除配置** 对话框出现：

    ![删除配置](~/assets/images/removeconfiguration.png)

1. 完成对话框字段和复选框，然后选择 **删除**：

    ![最终删除](~/assets/images/finalremove.png)

    将从 Teams 频道中删除 Webhook。

## <a name="see-also"></a>另请参阅

* [创建传出 Webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [创建 Office 365 连接器](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [创建和发送邮件](~/webhooks-and-connectors/how-to/connectors-using.md)
* [创建“共享到 Teams”按钮](../../concepts/build-and-test/share-to-teams.md#create-share-to-teams-button)
* [集成 web 应用](~/samples/integrate-web-apps-overview.md)
