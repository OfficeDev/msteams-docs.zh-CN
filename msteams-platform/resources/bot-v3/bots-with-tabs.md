---
title: 将 bot 与选项卡合并
description: 介绍如何将选项卡和 bot 一起使用
keywords: 团队 bot 选项卡开发
ms.date: 03/15/2018
ms.openlocfilehash: 59ae8bc01f82c70dd7ea6869cb870e26acae1293
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673290"
---
# <a name="combine-bots-with-tabs"></a>将 bot 与选项卡合并

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Bot 和选项卡协同工作，并且通常组合到一个后端服务中。 本节介绍了将选项卡和 bot 一起使用的最佳实践和常见模式。

## <a name="associating-user-identities-across-bot-and-tab"></a>在 bot 和选项卡之间关联用户标识

例如：假设您的选项卡应用程序使用专用 ID 系统来保护其内容。 假设您还具有可与用户进行交互的 bot。 通常情况下，您需要在特定于查看用户的选项卡中显示内容。 困难在于，系统中的用户 ID 可能与 Microsoft 团队用户 ID 不同。 那么，如何将这两种标识关联起来呢？
通常情况下，建议的方法是使用与用于为选项卡内容提供身份验证的相同标识系统在 bot 中登录用户。 您可以通过登录操作实现此目标，该操作通常通过 OAuth 流登录用户。

如果您的标识提供程序实现 OAuth 2.0 协议，则此流最适用。 然后，可以将团队用户 ID 与用户的凭据关联到您自己的标识服务。

   ![关联标识](~/assets/images/bots/associating_contexts.png)

## <a name="constructing-deep-links-to-tabs-in-messages-from-your-bot"></a>构建指向你的 bot 发来的邮件中的选项卡的深层链接

您可能需要使用选项卡来显示超出卡片内所能包含的内容的内容，或提供使用 tab 画布填写复杂表单填充任务的方法。 例如，当用户在你的 bot 上单击卡片时，请考虑将该用户导航到该选项卡。 为此，需要对你的 bot 的邮件进行编码，以包含[深层链接](~/concepts/build-and-test/deep-links.md)URL （通过标记）或 openUrl 操作的目标。

Deep links 依赖于 entityId，这是一个不透明的值，映射到系统中的唯一实体。 创建选项卡后，您最好在后端存储一些简单的状态（例如标志），指示该选项卡已在通道中创建。 当你的 bot 构造一条消息时，它可以将与该选项卡关联的 entityId 作为目标。

**注意：** 在个人聊天中，由于选项卡是 "静态" 的，并且随应用程序一起安装，因此您可以始终假定其存在，从而相应地构建深层链接。

## <a name="sending-notifications-for-tab-updates"></a>发送选项卡更新通知

通常，每当在选项卡中发生更新或用户操作时，您都需要通知最终用户。示例方案将任务或票证分配给同事的团队成员，然后通知团队成员。

有两种方法可以实现此方案：

1. 如果要通知整个频道，你的 bot 可以将邮件异步发布到频道。 如果 bot 不是通过选项卡创建的，则自动创建的选项卡对话将无法主动创建。

2. 如果你希望仅通知收件人或相关人员参与操作，你的 bot 可以向用户发送个人聊天消息。 您应首先查看您的 bot 和用户之间是否存在个人对话。 如果不是，则可以`CreateConversation`调用来启动个人聊天。

在这两种情况下，可合理地使用事件通知，并且决不会对用户发送不必要的更新。
