---
title: 创建机器人
description: 介绍如何在 Microsoft Teams 中创建机器人
ms.topic: how-to
keywords: 团队机器人创建
ms.date: 12/07/2018
ms.openlocfilehash: d7c618adc99f814bd677e919923c4b616f293e17
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014087"
---
# <a name="create-a-bot"></a>创建机器人

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

使用 Microsoft Bot Framework 创建的所有机器人均已配置并已准备好在 Microsoft Teams 中运行。

有关 [自动程序的常规](/azure/bot-service/?view=azure-bot-service-3.0) 信息，请参阅 Bot Framework 文档。

## <a name="create-a-bot-for-microsoft-teams"></a>为 Microsoft Teams 创建自动程序

*Teams App Studio* 是一个可帮助创建自动程序的工具，以及引用机器人的应用包。 它还包含 React 控件库和卡的可配置示例。 请参阅[开始使用 Teams App Studio](~/concepts/build-and-test/app-studio-overview.md)。 后续步骤假定你正在手动配置机器人，而不是使用 Teams App *Studio。*

1. 使用此链接创建自动 https://dev.botframework.com/bots/new 程序： **创建自动程序后，请确保从特色频道列表中将 Microsoft Teams 添加为频道。** 如果你已经创建应用程序包/清单，请随意重复使用你生成的任何 Microsoft 应用 ID。

   ![Bot Framework 注册页面](~/assets/images/bots/bfregister.png)

> [!NOTE]
> 如果不想在 Azure 中创建自动程序 **，则必须使用此** 链接创建新的自动 https://dev.botframework.com/bots/new 程序： 如果你改为单击自动程序框架门户中的"创建自动程序"按钮，你将改为在[Microsoft Azure](#bots-and-microsoft-azure)中创建机器人。

2. 使用 [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet 程序包  [、Bot Framework SDK](https://github.com/microsoft/botframework-sdk)或 [Bot 连接器 API 生成机器人](https://docs.microsoft.com/bot-framework/rest-api/bot-framework-rest-connector-api-reference)。 *另请参阅* [Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。

3. 使用 Bot [Framework 模拟器测试机器人](https://docs.microsoft.com/bot-framework/debug-bots-emulator)。

4. 将机器人部署到云服务，如[Microsoft Azure。](https://azure.microsoft.com/) 或者，在本地运行你的应用并使用隧道服务（如 [ngrok）](https://ngrok.com) 为自动https://公开一个安全终结点，例如 `https://45az0eb1.ngrok.io/api/messages` 。

> [!NOTE]
> ## <a name="bots-and-microsoft-azure"></a>机器人和 Microsoft Azure
> 截至 2017 年 12 月，Bot Framework 门户已针对在 Microsoft Azure 中注册机器人进行了优化。 以下是几个注意事项：
>
> * 在 Azure 中注册的自动程序的 Microsoft Teams 频道是免费的。 通过 Teams 频道发送的消息不会计入自动程序使用的消息。
> * 虽然无需使用 Azure 即可创建新的 [Bot Framework](https://dev.botframework.com/bots/new) 自动程序，但必须使用该 URL (，该 URL 不再在 Bot https://dev.botframework.com/bots/new) Framework 门户中公开。
> * 在 [Bot Framework](https://dev.botframework.com/bots) 中编辑自动程序列表中现有自动程序的属性（如"消息终结点"）时，这一点在首次开发机器人时很常见，尤其是在使用 [ngrok](https://ngrok.com)时，你将看到"迁移状态"列和蓝色"迁移"按钮，该按钮将进入 Microsoft Azure 门户。 不要单击"迁移"按钮，除非您希望这样做;相反，单击自动程序的名称，你可以编辑其属性：</br>
   ![编辑自动程序属性](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * 如果使用 Microsoft Azure 注册自动程序，则无需在 Microsoft Azure 上 *托管* 自动程序代码。
> * 如果你使用 Microsoft Azure 门户注册自动程序，则必须拥有 Microsoft Azure 帐户。 你可以[免费创建一个](https://azure.microsoft.com/free/)。 若要在创建信用卡时验证身份，必须提供信用卡，但不收费;在 Microsoft Teams 中始终可以自由创建和使用机器人。
> * 你现在可以直接使用 App Studio 在 Microsoft Teams 中注册/更新应用和机器人信息。 你只需使用 Microsoft Azure 门户添加/配置其他自动程序框架频道，如 Direct Line、Web Chat、Skype 和 Facebook Messenger。
