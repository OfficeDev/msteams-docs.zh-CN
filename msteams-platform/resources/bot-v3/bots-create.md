---
title: 创建 bot
description: 介绍如何在 Microsoft 团队中创建 bot
keywords: 团队 bot 创建
ms.date: 12/07/2018
ms.openlocfilehash: cb2d0974baf1d36a4acf077c219eb12449a5721a
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673043"
---
# <a name="create-a-bot"></a>创建 bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

使用 Microsoft Bot 框架创建的所有 bot 都已配置好并可在 Microsoft 团队中工作。

有关 bot 的一般信息，请参阅[Bot 框架文档](/azure/bot-service/?view=azure-bot-service-3.0)。

## <a name="create-a-bot-for-microsoft-teams"></a>为 Microsoft 团队创建机器人

*团队应用程序 Studio*是一种可帮助创建你的 bot 的工具，以及一个引用你的 bot 的应用程序包。 它还包含一个反应控制库和可配置卡片的示例。 请参阅[开始使用团队应用 Studio](~/concepts/build-and-test/app-studio-overview.md)。 下面的步骤假定您要手动配置你的 bot，而不是使用*团队应用程序 Studio*。

1. 使用此链接创建 bot： https://dev.botframework.com/bots/new。 **创建你的 bot 后，请确保将 Microsoft 团队添加为来自特色频道列表的频道。** 如果您已经创建了应用程序包/清单，则可以自由地重新使用您生成的任何 Microsoft 应用程序 ID。

   ![Bot 框架注册页](~/assets/images/bots/bfregister.png)

> [!NOTE]
> 如果您不想在 Azure 中创建你的 bot，则**必须**使用此链接创建新的 bot： https://dev.botframework.com/bots/new。 如果你改为单击 Bot 框架门户中的 "*创建机器人*" 按钮，则会改[为在 Microsoft Azure 中创建你的 bot](#bots-and-microsoft-azure) 。

2. 使用 botbuilder NuGet 包、 [-团队](https://www.npmjs.com/package/botbuilder-teams)npm 程序包或[bot 连接器 API](https://docs.microsoft.com/bot-framework/rest-api/bot-framework-rest-connector-api-reference)生成[机器人。。](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)

3. 使用[Bot 框架仿真程序](https://docs.microsoft.com/bot-framework/debug-bots-emulator)测试机器人。

4. 将机器人部署到云服务，如[Microsoft Azure](https://azure.microsoft.com/)。 也可以在本地运行应用程序，并使用隧道服务（例如， [ngrok](https://ngrok.com) ）为你的 bot 公开 https://终结`https://45az0eb1.ngrok.io/api/messages`点。

> [!NOTE]
> ## <a name="bots-and-microsoft-azure"></a>Bot 和 Microsoft Azure
> 从2017年12月到，已针对在 Microsoft Azure 中注册 bot 而优化了 Bot 框架门户。 以下是要了解的一些事项：
>
> * 在 Azure 上注册的 bot 的 Microsoft 团队频道是免费的。 通过团队频道发送的邮件不会计送到这些 bot 的已消耗邮件。
> * 虽然可以在不使用 Azure 的情况下[创建新的 Bot 框架](https://dev.botframework.com/bots/new)自动程序，但必须使用该https://dev.botframework.com/bots/new)URL （不会再在 Bot 框架门户中公开）。
> * 当您[在 Bot 框架](https://dev.botframework.com/bots)（如 "消息终结点"）中编辑 bot 的属性时，这在首次开发 bot 时很常见，尤其是在使用[ngrok](https://ngrok.com)时，您将看到 "迁移状态" 列和一个蓝色的 "迁移" 按钮，该按钮将转到 Microsoft Azure 门户。 请勿单击 "迁移" 按钮，除非您要执行的操作;而是单击 bot 的名称，然后可以编辑其属性：</br>
   ![编辑机器人属性](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * 如果你使用 Microsoft Azure 注册你的 bot，则无需在 Microsoft Azure 上*托管*你的 bot 代码。
> * 如果你使用 Microsoft Azure 门户注册 bot，则必须拥有 Microsoft Azure 帐户。 你可以[免费创建一个](https://azure.microsoft.com/free/)。 若要在创建一个时验证你的身份，你必须提供一个信用卡，但不会被收取费用;在 Microsoft 团队中，始终可以免费创建和使用 bot。
> * 现在，你可以使用应用程序 Studio 直接在 Microsoft 团队中注册/更新 App 和机器人信息。 您只需使用 Microsoft Azure 门户添加/配置其他机器人框架通道（如直接线路、Web 聊天、Skype 和 Facebook Messenger）。
