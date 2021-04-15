---
title: 将机器人与选项卡组合在一起
description: 介绍如何将选项卡和自动程序一同使用
keywords: teams 机器人选项卡开发
ms.topic: conceptual
ms.date: 03/15/2018
ms.openlocfilehash: d8ef669f55d5edbb9795fa2d34277bd2e2dccc7c
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696596"
---
# <a name="combine-bots-with-tabs"></a>将机器人与选项卡组合在一起

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

机器人和选项卡可以很好地协同工作，并且通常组合到单个后端服务中。 本节介绍将选项卡和聊天机器人一同使用的最佳方案及通用模式。

## <a name="associating-user-identities-across-bot-and-tab"></a>跨自动程序与选项卡关联用户标识

例如：假设您的选项卡应用程序使用专有 ID 系统保护其内容。 假设您还有一个可以与用户交互的机器人。 通常，你需要在选项卡中显示特定于查看用户的内容。 挑战在于，系统中用户 ID 可能不同于 Microsoft Teams 用户 ID。 那么，如何关联这两个标识？
通常，建议的方法是使用用于为选项卡内容提供身份验证的相同身份系统，使用自动程序让用户登录。 可以通过登录操作实现此操作，此操作通常通过 OAuth 流在用户中登录。

如果标识提供程序实现 OAuth 2.0 协议，则此流最有效。 然后，可以将 Teams 用户 ID 与你自己的标识服务中的用户凭据关联。

   ![关联标识](~/assets/images/bots/associating_contexts.png)

## <a name="constructing-deep-links-to-tabs-in-messages-from-your-bot"></a>从自动程序构造消息中选项卡的深层链接

您可能需要使用选项卡来显示比卡片内部容纳更多的内容，或者提供一种使用选项卡画布完成复杂表单填写任务的方法。 例如，当用户从自动程序单击卡片时，请考虑将用户导航到选项卡。 为此，你需要对自动程序的消息进行编码，以包括深层链接 [URL（](~/concepts/build-and-test/deep-links.md) 通过标记或作为 openUrl 操作的目标）。

深度链接依赖于 entityId，它是映射到系统中唯一实体的不透明值。 创建选项卡时，最好存储一些简单的状态 (例如，) 标记标记指示该选项卡已在通道中创建。 当机器人构造消息时，它可以面向与该选项卡关联的 entityId。

**注意：** 在个人聊天中，由于选项卡是"静态"的，并且随应用一起安装，因此你始终可以假定它们存在，从而相应地构造深层链接。

## <a name="sending-notifications-for-tab-updates"></a>发送选项卡更新通知

通常，每当选项卡中发生更新或用户操作时，你会希望通知最终用户。示例方案是向同事团队成员分配任务或票证，然后通知该团队成员。

有两种方法可以实现此方案：

1. 如果你想要通知整个频道，机器人可以异步向频道发布消息。 如果没有使用选项卡创建选项卡对话，则自动程序无法主动创建该对话。

2. 如果你希望仅通知收件人或参与该操作的各方，则机器人可以向用户发送个人聊天消息。 应首先检查机器人和用户之间的个人对话是否存在。 如果没有，可以调用 `CreateConversation` 以启动个人聊天。

在这两种情况下，请明智使用事件通知，并且不要向用户发送不必要的更新。
