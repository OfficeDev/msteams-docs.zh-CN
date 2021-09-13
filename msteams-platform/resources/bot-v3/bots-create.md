---
title: 创建机器人
description: 介绍如何在 Microsoft Teams
ms.topic: how-to
keywords: 团队机器人创建
ms.localizationpriority: medium
ms.date: 12/07/2018
ms.openlocfilehash: d258f9e6713e6bb3d68aa19ef8a3b36d44dd3a07
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155871"
---
# <a name="create-a-bot"></a>创建机器人

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

已配置使用 Microsoft Bot Framework 创建的所有自动程序，并准备好在 Microsoft Teams。

有关详细信息，请参阅 [Bot Framework 文档，](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true) 了解机器人的一般信息。

## <a name="create-a-bot-for-microsoft-teams"></a>为 Microsoft Teams 创建自动程序

**Teams App Studio** 是一个可帮助创建自动程序的工具，以及引用机器人的应用包。 它还包含 React 控件库和卡的可配置示例。 有关详细信息，请参阅 App [Studio Teams入门](~/concepts/build-and-test/app-studio-overview.md)。 下面的步骤假定你正在手动配置机器人，而不是在 App Studio **Teams程序**：

1. 使用此链接创建机器人 https://dev.botframework.com/bots/new ：。 **创建自动程序后，请确保从特色频道列表中将 Microsoft Teams 添加为频道。** 如果你已经创建应用程序包/清单，请随意重复使用你生成的任何 Microsoft 应用 ID。

   ![Bot Framework 注册页面](~/assets/images/bots/bfregister.png)

> [!NOTE]
> 如果你不希望在 Azure 中创建自动程序， **则必须** 使用此链接创建新自动程序 https://dev.botframework.com/bots/new ：。 如果你改为单击在 **Bot** Framework 门户创建自动程序，你将改为在自动程序 [Microsoft Azure。](#bots-and-microsoft-azure)

2. 使用[Microsoft.Bot.Connector.Teams NuGet](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)程序包[、Bot Framework SDK](https://github.com/microsoft/botframework-sdk)或[Bot Connector API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)生成机器人。

3. 使用 Bot Framework Emulator 测试[机器人](/bot-framework/debug-bots-emulator)。

4. 将机器人部署到云服务，[例如Microsoft Azure。](https://azure.microsoft.com/) 或者，在本地运行你的应用并使用隧道服务（如 [ngrok）](https://ngrok.com) 为自动 https:// 公开一个 https:// 终结点，例如 `https://45az0eb1.ngrok.io/api/messages` 。

> [!NOTE]
> ## <a name="bots-and-microsoft-azure"></a>机器人和Microsoft Azure
> 截至 2017 年 12 月，Bot Framework 门户已针对在 Microsoft Azure 中注册自动程序进行了优化。 以下是几个注意事项：
>
> * 在 Azure 中注册的自动程序的 Microsoft Teams 频道是免费的。 通过自动Teams发送的消息不会计入自动程序使用的已用邮件。
> * 虽然无需使用 Azure 即可创建新的 [Bot Framework](https://dev.botframework.com/bots/new) 自动程序，但必须使用该 URL (，该 URL 不再在 Bot Framework 门户 https://dev.botframework.com/bots/new) 中公开。
> * 在[Bot Framework](https://dev.botframework.com/bots)中编辑自动程序列表中的现有自动程序的属性（如其"消息终结点"）时，首次开发自动程序时很常见，尤其是在使用[ngrok](https://ngrok.com)时，你将看到"迁移状态"列和一个蓝色"迁移"按钮，该按钮将进入 Microsoft Azure 门户。 不要单击"迁移"按钮，除非你希望这样做;相反，单击自动程序的名称，你可以编辑其属性：</br>
   ![编辑自动程序属性](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * 如果使用 Microsoft Azure 注册自动程序，则无需将机器人代码托管在 Microsoft Azure。 
> * 如果你使用 Microsoft Azure 门户注册自动程序，则必须拥有 Microsoft Azure 帐户。 你可以[免费创建一个](https://azure.microsoft.com/free/)。 若要创建信用卡时验证身份，必须提供信用卡，但不收费;始终可以自由地创建自动程序并使用Microsoft Teams。
> * 现在，你可以直接在应用中使用 App Studio 注册/更新应用和Microsoft Teams。 你只需使用 Microsoft Azure 门户添加或配置其他自动程序框架频道，如 Direct Line、Web Chat、Skype 和 Facebook Messenger。

## <a name="see-also"></a>另请参阅

[Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。