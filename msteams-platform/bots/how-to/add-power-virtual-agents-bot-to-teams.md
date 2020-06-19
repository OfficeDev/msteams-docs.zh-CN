---
title: 向团队添加 Power Virtual 代理 chatbot
author: laujan
description: 在团队平台中集成电源虚拟代理 chatbot
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 4f32a3c13d9288c3e733e92369645bcf9e32d586
ms.sourcegitcommit: 28af65730884b788ff77a4ec4032219380df8b70
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "44801141"
---
# <a name="integrate-your-power-virtual-agents-chatbot-with-microsoft-teams"></a>将您的 Power Virtual Agent chatbot 与 Microsoft 团队集成

[Power Virtual agent](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)是一个无代码的、导向的图形界面解决方案，它使团队中的每个成员都能创建丰富的会话 chatbots，以便轻松地与团队平台集成。 在 Power Virtual Agent 中创作的所有内容都在团队中呈现为自然，电源虚拟代理程序 bot 与团队本机聊天画布中的用户接洽。 您的 IT 管理员、业务分析师、域专家和训练有素的应用程序开发人员可以设计、开发和发布用于团队的智能虚拟代理，而无需设置开发环境、创建 web 服务或直接在 Bot 框架中注册。  *请参阅*[为使用 Microsoft Power Virtual 代理的团队创建 chatbot](../what-are-bots.md#create-a-chatbot-for-teams-with-microsoft-power-virtual-agents)。

> [!NOTE]
> 通过将您的 chatbot 添加到 Microsoft 团队，可以与 Microsoft 团队共享某些数据（如 bot 内容和最终用户聊天内容），这意味着你的数据将在你的[组织的合规性和地理或区域边界](/power-virtual-agents/data-location)之外流动。 <br/>
> 有关详细信息，请参阅[Microsoft 团队中的安全性和合规性](/MicrosoftTeams/security-compliance-overview)。

## <a name="make-your-chatbot-reachable-in-teams-in-the-power-virtual-agents-portal"></a>使你的 chatbot 可在 Power Virtual Agent 门户中的团队中访问

1. **发布最新的 bot 内容**。  在[Power Virtual agent 门户](https://powervirtualagents.microsoft.com)中创建 chatbot 后，您至少需要在工作组用户可以与其进行交互之前发布你的机器人。 请参阅[发布最新的 bot 内容](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content)。

![在 power virtual agent 门户中发布](../../assets/images/pva-publish.png)

2. **配置团队频道**。 在发布你的 bot 后，你可以添加团队频道以使机器人可与团队用户访问。

![power virtual agent portal 中的频道](../../assets/images/pva-channels.png)

3. **为您的 Chatbot 生成应用程序 Id** 成功将团队频道添加到 chatbot 后，会在对话框中生成**应用 Id** 。 应用程序 Id 是你的 bot 的唯一 Microsoft 生成标识符。  复制并保存应用程序 Id —稍后将需要它来为团队创建应用程序包。

## <a name="add-your-bot-to-teams-using-app-studio"></a>使用应用程序 Studio 向团队添加你的机器人

如果在团队实例中启用了 "[上载自定义应用程序](/microsoftteams/admin-settings)"，则可以使用团队应用程序 Studio 直接上传您的 chatbot，并立即开始使用它。 如果要共享你的 chatbot，可以请求管理员让你的你的 bot 在租户应用程序目录中可用，或者可以向其他人发送应用程序包，并请求其独立上载。

1. **在团队中安装应用程序 Studio**。 应用程序 Studio 是一个团队应用程序，您可以从团队存储中进行安装，从而简化团队中机器人的创建和注册： 

  * 从 "团队" 实例的左侧导航栏底部选择 "应用商店" 图标，然后搜索**应用程序 Studio**。
>
&emsp;&emsp; <img  width="450px" title="在存储区中查找应用程序 Studio" src="../../assets/images/get-started/app-studio-store.png"/>    

  * 选择 "**应用程序制作室**" 磁贴，然后在弹出对话框中选择 "**安装**"。
>
&emsp;&emsp; <img  width="450px" title="安装应用程序 Studio" src="../../assets/images/get-started/app-studio-install.png"/>

2. **在应用程序 Studio 中创建团队应用程序清单**。  团队中的 bot 由应用程序清单（JSON）文件定义，该文件提供有关你的 bot 及其功能的基本信息。 在**应用程序 Studio**中选择**清单编辑器**   =>  **创建新的应用程序**。
3. **添加你的 bot 详细信息**。 有关每个字段的完整说明，请参阅[清单架构定义](../../resources/schema/manifest-schema.md)。 请务必填写所有必填字段。
4. **设置你的 bot**。 导航到 " **bot** " 选项卡，选择 "**设置**" 按钮，选择 "**现有机器人**"，然后输入你的 bot 名称。
5. **添加您的应用程序 Id**。导航到 "**连接到不同的 bot id** "，并粘贴到之前复制的**应用 id**中。 在 "范围" 下，选择 "**个人**"，然后选择 "**保存**"。
6. **为你的 Bot 添加有效的域**。  仅当你的 bot 要求用户登录时，才需要执行此步骤。 导航到 "**域和权限**"，并在 "**有效域**" 字段中输入以下内容：

```bash
token.botframework.com
```

7.  **测试和分发你的 bot**。 选择 "**测试和分布**" 选项卡，然后选择 "**安装**" 将你的 Bot 直接添加到团队实例中。 （可选）可以下载已完成的应用程序包以与团队用户共享，也可以将其提供给管理员，使你的 bot 在租户应用程序目录中可用。
8. **启动聊天**。 将电源虚拟代理聊天机器人添加到团队的安装过程已完成。 现在，你可以在个人聊天中开始与你的 bot 进行对话。

> [!div class="nextstepaction"]
> [了解有关发布 Power Virtual 代理 bot 的详细信息](/power-virtual-agents/publication-fundamentals-publish-channels)