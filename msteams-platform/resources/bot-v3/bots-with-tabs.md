---
title: 将机器人与选项卡合并
description: 在本文中，你将了解如何同时使用选项卡和机器人，构建指向来自机器人的消息中的选项卡的深层链接，以及团队机器人选项卡开发
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 03/15/2018
ms.openlocfilehash: f993f3d8deb8b8a781c96627bf63c2eed350e6c8
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833021"
---
# <a name="combine-bots-with-tabs"></a>将机器人与选项卡合并

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

机器人和选项卡协同工作，通常合并到单个后端服务中。 本部分介绍将选项卡和机器人一起使用的最佳做法和常见模式。

## <a name="associating-user-identities-across-bot-and-tab"></a>跨机器人和选项卡关联用户标识

例如：假设选项卡应用程序使用专有 ID 系统来保护其内容。 假设你还有一个可以与用户交互的机器人。 通常，你需要在特定于查看用户的选项卡中显示内容。 挑战在于系统中的用户 ID 可能不同于 Microsoft Teams 用户 ID。 那么，如何关联这两个标识呢？
通常，建议的方法是使用用于为选项卡内容提供身份验证的相同标识系统通过机器人登录用户。 可以通过登录操作实现，该操作通常通过 OAuth 流登录用户。

如果标识提供者实现 OAuth 2.0 协议，则此流效果最佳。 然后，可以将 Teams 用户 ID 与自己的标识服务中的用户凭据相关联。

   :::image type="content" source="../../assets/images/bots/associating_contexts.png" alt-text="屏幕截图显示了关联标识。":::

## <a name="constructing-deep-links-to-tabs-in-messages-from-your-bot"></a>构造指向来自机器人的消息中的选项卡的深层链接

你希望使用选项卡来显示更多适合卡片内的内容，或者提供一种使用选项卡画布完成复杂表单填充任务的方法。 例如，当用户从机器人中选择卡片时，请考虑将用户导航到选项卡。 为此，需要对机器人的消息进行编码，以包含 [深层链接](~/concepts/build-and-test/deep-links.md) URL，无论是通过标记还是作为 openUrl 操作的目标。

深层链接依赖于 entityId，它是映射到系统中唯一实体的不透明值。 创建选项卡后，将存储一些简单状态。 例如，后端上的标志，指示在通道中创建选项卡。 当机器人构造消息时，它可以面向与该选项卡关联的 entityId。

> [!NOTE]
> 在个人聊天中，由于选项卡是 *静态* 的，并且随应用一起安装，因此你始终可以假设它们的存在，从而相应地构造深层链接。

## <a name="sending-notifications-for-tab-updates"></a>发送选项卡更新通知

通常，每当选项卡中发生更新或用户操作时，你都会通知最终用户。一个示例方案是将任务或票证分配给其他团队成员，然后通知该团队成员。

实现此方案的方法有两种：

1. 如果想要通知整个通道，机器人可以异步向通道发布消息。 如果未使用选项卡创建选项卡对话，则机器人无法主动创建选项卡对话。

2. 如果只想通知与操作相关的收件人或相关方，机器人可以向用户发送个人聊天消息。 应首先检查机器人与用户之间是否存在个人对话。 如果没有，可以调用 来 `CreateConversation` 启动个人聊天。

在这两种情况下，请明智地使用事件通知，并且不要向用户发送不必要的更新垃圾邮件。
