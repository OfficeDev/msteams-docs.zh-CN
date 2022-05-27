---
title: 创建机器人
description: 介绍如何在 Microsoft Teams 中创建机器人
ms.topic: how-to
keywords: 团队机器人创建
ms.localizationpriority: medium
ms.date: 12/07/2018
ms.openlocfilehash: 92d4593290d1332b86b370a49b20daaf43868a51
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757386"
---
# <a name="create-a-bot"></a>创建机器人

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

使用Microsoft Bot Framework创建的所有机器人都已配置并可在Microsoft Teams中工作。

有关详细信息，请参阅 [Bot Framework 文档](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true) ，了解有关机器人的一般信息。

## <a name="create-a-bot-for-microsoft-teams"></a>为 Microsoft Teams 创建自动程序

**Teams App Studio** 是一种可帮助创建机器人的工具，以及引用机器人的应用包。 它还包含 React 控件库和卡的可配置示例。 有关详细信息，请参阅 [Teams App Studio 入门](~/concepts/build-and-test/app-studio-overview.md)。 以下步骤假定你正在手动配置机器人，而不使用 **Teams App Studio**：

1. 使用 [Bot Framework 创建机器人](https://dev.botframework.com/bots/new)。 **创建自动程序后，请确保从特色频道列表中将 Microsoft Teams 添加为频道。** 如果你已经创建应用程序包/清单，请随意重复使用你生成的任何 Microsoft 应用 ID。

   ![Bot Framework 注册页面](~/assets/images/bots/bfregister.png)

> [!NOTE]
> 如果不希望在 Azure 中创建机器人， **则必须** 使用此链接创建新的机器人： [Bot Framework](https://dev.botframework.com/bots/new)。 如果在 Bot Framework 门户中单击 **“创建机器人**”，则会 [改为在Microsoft Azure中创建机器人](#bots-and-microsoft-azure)。

2. 使用 [Microsoft.Bot.Connector.Teams NuGet](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)包、[Bot Framework SDK](https://github.com/microsoft/botframework-sdk) 或 [Bot Connector API 生成机器人](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)。

3. 使用[Bot Framework Emulator](/bot-framework/debug-bots-emulator)测试机器人。

4. 将机器人部署到云服务，例如[Microsoft Azure](https://azure.microsoft.com/)。 或者，在本地运行应用，并使用隧道服务（例如 [ngrok）](https://ngrok.com) 为机器人公开 https:// 终结点，例如 `https://45az0eb1.ngrok.io/api/messages`。

> [!NOTE]
>
> ## <a name="bots-and-microsoft-azure"></a>机器人和Microsoft Azure
>
> 自 2017 年 12 月起，Bot Framework 门户已针对在 Microsoft Azure 中注册机器人进行了优化。 以下是几个注意事项：
>
> * 在 Azure 中注册的自动程序的 Microsoft Teams 频道是免费的。 通过Teams通道发送的消息将不计入机器人使用的邮件。
> * 虽然无需使用 Azure 即可 [创建新的 Bot Framework 机器人](https://dev.botframework.com/bots/new) ，但必须使用 [创建新的 Bot Framework 机器人](https://dev.botframework.com/bots/new)，该机器人不再在 Bot Framework 门户中公开。
> * 在 Bot Framework 中编辑机器人列表中现有[机器人的](https://dev.botframework.com/bots)属性（例如，首次开发机器人时常见的“消息终结点”）时，尤其是使用 [ngrok](https://ngrok.com) 时，会看到“迁移状态”列和蓝色“迁移”按钮，该按钮会将你带入Microsoft Azure门户。 不要单击“迁移”按钮，除非这是你要做的;请单击机器人的名称，然后编辑其属性：</br>
   ![编辑自动程序属性](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * 如果使用Microsoft Azure注册机器人，则无需在 Microsoft Azure 上 *托管* 机器人代码。
> * 如果使用Azure 门户注册机器人，则必须有一个Microsoft Azure帐户。 你可以[免费创建一个](https://azure.microsoft.com/free/)。 若要在创建信用卡时验证身份，必须提供信用卡，但不会收取费用;始终可以使用Microsoft Teams创建和使用机器人。
> * 现在可以使用 App Studio 直接在Microsoft Teams中注册/更新应用和机器人信息。 只需使用Azure 门户添加或配置其他 Bot Framework 通道，如 Direct Line、Web 聊天、Skype 和 Facebook Messenger。

> [!WARNING]
>* 如果你一直使用 App Studio，我们建议你尝试使用开发人员门户来配置、分发和管理 Teams 应用。App Studio 将在 2022 年 6 月 30 日弃用

## <a name="see-also"></a>另请参阅

[Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。
