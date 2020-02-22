---
title: 创建 bot
description: 介绍如何在 Microsoft 团队中创建 bot
keywords: 团队 bot 创建
ms.date: 12/07/2018
ms.openlocfilehash: 6d8441cb3bc89ae7a923cad72567eb52dd99dc4b
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228015"
---
# <a name="create-a-bot"></a>创建 bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

使用 Microsoft Bot 框架创建的所有 bot 都已配置好并可在 Microsoft 团队中工作。

有关 bot 的一般信息，请参阅[Bot 框架文档](/azure/bot-service/?view=azure-bot-service-3.0)。

## <a name="create-a-bot-for-microsoft-teams"></a>为 Microsoft Teams 创建自动程序

*团队应用程序 Studio*是一种可帮助创建你的 bot 的工具，以及一个引用你的 bot 的应用程序包。 它还包含 React 控件库和卡的可配置示例。 请参阅[开始使用 Teams App Studio](~/concepts/build-and-test/app-studio-overview.md)。 下面的步骤假定您要手动配置你的 bot，而不是使用*团队应用程序 Studio*。

1. 使用此链接创建 bot： https://dev.botframework.com/bots/new。 **创建自动程序后，请确保从特色频道列表中将 Microsoft Teams 添加为频道。** 如果你已经创建应用程序包/清单，请随意重复使用你生成的任何 Microsoft 应用 ID。

   ![Bot Framework 注册页面](~/assets/images/bots/bfregister.png)

> [!NOTE]
> 如果您不想在 Azure 中创建你的 bot，则**必须**使用此链接创建新的 bot： https://dev.botframework.com/bots/new。 如果你改为单击 Bot 框架门户中的 "*创建机器人*" 按钮，则会改[为在 Microsoft Azure 中创建你的 bot](#bots-and-microsoft-azure) 。

2. 使用 " [Microsoft bot. 团队](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)" NuGet 包、 [bot 框架 SDK](https://github.com/microsoft/botframework-sdk)或[bot 连接器 API](https://docs.microsoft.com/bot-framework/rest-api/bot-framework-rest-connector-api-reference)构建机器人。 *另请参阅* [Bot 框架示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。

3. 使用[Bot 框架仿真程序](https://docs.microsoft.com/bot-framework/debug-bots-emulator)测试机器人。

4. 将机器人部署到云服务，如[Microsoft Azure](https://azure.microsoft.com/)。 也可以在本地运行应用程序，并使用隧道服务（例如， [ngrok](https://ngrok.com) ）为你的 bot 公开 https://终结`https://45az0eb1.ngrok.io/api/messages`点。

> [!NOTE]
> ## <a name="bots-and-microsoft-azure"></a>Bot 和 Microsoft Azure
> 从2017年12月到，已针对在 Microsoft Azure 中注册 bot 而优化了 Bot 框架门户。 以下是几个注意事项：
>
> * 在 Azure 中注册的自动程序的 Microsoft Teams 频道是免费的。 通过团队频道发送的邮件不会计送到这些 bot 的已消耗邮件。
> * 虽然可以在不使用 Azure 的情况下[创建新的 Bot 框架](https://dev.botframework.com/bots/new)自动程序，但必须使用该https://dev.botframework.com/bots/new)URL （不会再在 Bot 框架门户中公开）。
> * 当您[在 Bot 框架](https://dev.botframework.com/bots)（如 "消息终结点"）中编辑 bot 的属性时，这在首次开发 bot 时很常见，尤其是在使用[ngrok](https://ngrok.com)时，您将看到 "迁移状态" 列和一个蓝色的 "迁移" 按钮，该按钮将转到 Microsoft Azure 门户。 请勿单击 "迁移" 按钮，除非您要执行的操作;而是单击 bot 的名称，然后可以编辑其属性：</br>
   ![编辑自动程序属性](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * 如果你使用 Microsoft Azure 注册你的 bot，则无需在 Microsoft Azure 上*托管*你的 bot 代码。
> * 如果你使用 Microsoft Azure 门户注册自动程序，则必须拥有 Microsoft Azure 帐户。 你可以[免费创建一个](https://azure.microsoft.com/free/)。 若要在创建一个时验证你的身份，你必须提供一个信用卡，但不会被收取费用;在 Microsoft 团队中，始终可以免费创建和使用 bot。
> * 现在，你可以使用应用程序 Studio 直接在 Microsoft 团队中注册/更新 App 和机器人信息。 您只需使用 Microsoft Azure 门户添加/配置其他机器人框架通道（如直接线路、Web 聊天、Skype 和 Facebook Messenger）。
