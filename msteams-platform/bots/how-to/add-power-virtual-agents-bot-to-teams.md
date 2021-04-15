---
title: 将 Power Virtual Agents 聊天机器人添加到 Teams
author: laujan
description: 在 Teams 平台中集成 Power Virtual Agents 聊天机器人
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 6103e3b58d7283eab6e9a9932f6dc7778d6fc697
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51697093"
---
# <a name="integrate-a-power-virtual-agents-chatbot-with-microsoft-teams"></a>将 Power Virtual Agents 聊天机器人与 Microsoft Teams 集成

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) 是无代码的引导式图形界面解决方案，它使团队的每位成员能够创建丰富的对话聊天机器人，这些聊天机器人可轻松与 Teams 平台集成。 在 Power Virtual Agents 中创作的所有内容自然呈现在 Teams 中，Power Virtual Agents 机器人与 Teams 本机聊天画布中的用户互动。 你的 IT 管理员、业务分析师、域专家和经验丰富的应用开发人员可以设计、开发和发布 Teams 的智能虚拟代理，而无需设置开发环境、创建 Web 服务或直接在 Bot Framework 中注册。  *请参阅*[使用 Microsoft Power Virtual Agents 为 Teams 创建聊天机器人](../bot-features.md#bots-and-the-microsoft-power-virtual-agents)。

> [!NOTE]
> 通过将聊天机器人添加到 Microsoft Teams，一些数据（如聊天机器人内容和最终用户聊天内容）将与 Microsoft Teams (这意味着你的数据将流出组织的合规性以及地理或区域边界[) 。](/power-virtual-agents/data-location) <br/>
> 有关详细信息，请参阅 Microsoft [Teams 中的安全性和合规性](/MicrosoftTeams/security-compliance-overview)。

## <a name="make-your-chatbot-available-in-teams-via-the-power-virtual-agents-portal"></a>通过 Power Virtual Agents 门户在 Teams 中提供聊天机器人

1. **发布最新的自动程序内容**。  在 Power [Virtual Agents](https://powervirtualagents.microsoft.com)门户中创建聊天机器人后，你至少需要发布一次聊天机器人，Teams 用户才能与之交互。 请参阅 [发布最新的自动程序内容](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content)。

![在电源虚拟代理门户中发布](../../assets/images/pva-publish.png)

2. **配置 Teams 频道**。 发布自动程序后，可以添加 Teams 频道，使机器人可供 Teams 用户使用。

![电源虚拟代理门户中的通道](../../assets/images/pva-channels.png)

3. **为 chatbot 生成应用 ID。**  成功将 Teams 频道添加到聊天机器人后，将在对话框中生成应用 ID。 应用 ID 是 Microsoft 为自动程序生成的唯一标识符。  复制并保存应用 ID，稍后将需要它来创建 Teams 应用包。

## <a name="add-your-bot-to-teams-using-app-studio"></a>使用 App Studio 将机器人添加到 Teams

如果在 [Teams 实例中启用了](/microsoftteams/admin-settings) 上传自定义应用，可以使用 Teams App Studio 直接上传聊天机器人并开始使用它。 如果你想要共享聊天机器人，你可以请求管理员在租户应用目录中提供机器人，也可以向其他人发送你的应用包，并让他们单独上传它。

1. **在 Teams 中安装 App Studio。** App Studio 是一款可以从 Teams 应用商店安装的 Teams 应用，可简化 Teams 中机器人的创建和注册过程： 

  * 从 Teams 实例的左侧导航栏底部选择应用商店图标，然后搜索 **App Studio**。
>

&emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="/msteams-docs/msteams-platform/assets/images/get-started/app-studio-store.png"/>   

  * 选择 **App Studio** 磁贴 **，然后选择** 弹出对话框中的"安装"。
>
&emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

2. **在 App Studio 中创建 Teams 应用清单**。  Teams 中的自动程序由应用清单 (JSON) 文件定义，该文件提供有关机器人及其功能的基本信息。 在 **App Studio 中****，选择"清单编辑器**   =>  **""新建应用"。**
3. **添加自动程序详细信息**。 有关每个字段的完整说明，请参阅 [清单架构定义](../../resources/schema/manifest-schema.md)。 请务必填写所有必填字段。
4. **设置自动程序**。 导航到 **"自动程序** "选项卡，选择" **设置"** 按钮，选择" **现有** 自动程序"，然后输入自动程序名称。
5. **添加应用 ID**。导航到 **"连接到其他自动程序 ID"，** 并粘贴之前复制的应用 ID。 在"作用域"下 **，选择"个人**"，然后选择"保存 **"。**
6. **为自动程序添加有效的域**。  只有当机器人要求用户登录时，才需要执行此步骤。 导航到 **"域和权限"，** 并在" **有效域** "字段中输入以下内容：

```bash
token.botframework.com
```

7.  **测试和分发机器人**。 选择" **测试和分发"** 选项卡，然后选择" **安装** "以将机器人直接添加到 Teams 实例。 （可选）你可以下载已完成的应用包以与 Teams 用户共享，或提供给管理员，以便自动程序在租户应用目录中可用。
8. **启动聊天**。 将 Power Virtual Agents 聊天机器人添加到 Teams 的安装过程已完成。 现在可以在个人聊天中与机器人开始对话。

> [!div class="nextstepaction"]
> [了解更多信息：发布 Power Virtual Agents 机器人](/power-virtual-agents/publication-fundamentals-publish-channels)
