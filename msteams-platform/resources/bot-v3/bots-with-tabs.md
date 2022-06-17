---
title: 将机器人与选项卡组合在一起
description: 本文介绍如何结合使用选项卡和机器人、构造指向机器人消息中选项卡的深层链接，以及团队机器人选项卡开发
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 03/15/2018
ms.openlocfilehash: f8199b65fded8c43af45cb303a400652e5516db2
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142092"
---
# <a name="combine-bots-with-tabs"></a>将机器人与选项卡组合在一起

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

机器人和选项卡协同工作，通常组合成单个后端服务。 本部分介绍将选项卡和机器人一起使用的最佳做法和常见模式。

## <a name="associating-user-identities-across-bot-and-tab"></a>跨机器人和选项卡关联用户标识

例如：假设 Tab 应用程序使用专有 ID 系统来保护其内容。 假设你还有一个可以与用户交互的机器人。 通常，需要在特定于查看用户的选项卡中显示内容。 挑战在于，系统中的用户 ID 可能不同于Microsoft Teams用户 ID。 那么，如何关联这两个标识呢？
通常，建议的方法是使用用于为选项卡内容提供身份验证的同一标识系统将用户登录到机器人。 可以通过登录操作实现，该操作通常通过 OAuth 流登录用户。

如果标识提供者实现 OAuth 2.0 协议，则此流效果最佳。 然后，可以从自己的标识服务将Teams用户 ID 与用户的凭据相关联。

   ![关联标识](~/assets/images/bots/associating_contexts.png)

## <a name="constructing-deep-links-to-tabs-in-messages-from-your-bot"></a>构造指向来自机器人的消息中的选项卡的深层链接

你希望使用选项卡显示的内容多于卡片内的内容，或提供使用选项卡画布完成复杂表单填充任务的方法。 例如，当用户单击机器人中的卡时，请考虑导航到选项卡。 若要实现此目的，需要对机器人的消息进行编码，以包含 [深度链接](~/concepts/build-and-test/deep-links.md) URL，无论是通过标记还是作为 openUrl 操作的目标。

深层链接依赖于 entityId，这是映射到系统中唯一实体的不透明值。 创建选项卡时，最好存储一些简单的状态。 例如，后端上指示已在通道中创建选项卡的标志。 当机器人构造消息时，它可以将与该选项卡关联的 entityId 作为目标。

> [!NOTE]
> 在个人聊天中，由于选项卡是“静态”且随应用一起安装，因此你始终可以假设它们的存在，从而相应地构造深层链接。

## <a name="sending-notifications-for-tab-updates"></a>发送选项卡更新通知

通常，每当选项卡中发生更新或用户操作时，都需要通知最终用户。示例方案是将任务或票证分配给其他团队成员，然后通知该团队成员。

实现此方案的方法有两种：

1. 如果要通知整个通道，机器人可以异步向通道帖子消息。 如果未使用选项卡创建选项卡，则机器人无法主动创建选项卡对话。

2. 如果只想通知参与操作的收件人或相关方，机器人可以向用户发送个人聊天消息。 应首先检查机器人与用户之间的个人对话是否存在。 如果没有，可以调用 `CreateConversation` 以启动个人聊天。

在这两种情况下，都明智地使用事件通知，从不向用户发送不必要的更新垃圾邮件。
