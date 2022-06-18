---
title: 添加 Power Virtual Agent 聊天机器人
author: surbhigupta
description: 了解如何在 Teams 平台中集成 Power Virtual Agents 聊天机器人，以创建对话聊天机器人并将其与 Teams 集成
ms.topic: how-to
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: 0f66a42cecbac25f82980c16e7f979c5d613816d
ms.sourcegitcommit: 9d318eda5589ea8f5519d05cb83e0acf3e13e2f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66150846"
---
# <a name="add-power-virtual-agents-chatbot"></a>添加 Power Virtual Agent 聊天机器人

Power Virtual Agents 是一种无代码引导式图形界面解决方案，可支持团队的每个成员创建可轻松与 Teams 平台集成的丰富对话聊天机器人。 在 Power Virtual Agents 中创作的所有内容都会在 Teams 中自然呈现。 Power Virtual Agents 机器人可与用户在 Teams 本机聊天画布中进行互动。 IT 管理员、业务分析师、域专家和熟练的应用开发人员可以为 Teams 设计、开发和发布智能虚拟代理，而无需设置开发环境。 他们可以创建 Web 服务，或直接在 Bot Framework 中注册。

本文档介绍如何通过 Power Virtual Agents 门户使聊天机器人在 Teams 中可用，以及如何使用 App Studio 将机器人添加到 Teams。

Power Virtual Agents 可让你创建功能强大的聊天机器人，它们可回答客户、其他员工或者网站或服务访问者提出的问题。

无需数据科学家或开发人员即可轻松创建这些机器人。

> [!NOTE]
>
> * 通过将聊天机器人添加到Microsoft Teams，某些数据（如机器人内容和用户聊天内容）与Teams共享。 这意味着数据可在[组织的合规性和地理或区域边界](/power-virtual-agents/data-location)之外流动。 <br/>
> * 不得使用 Microsoft Power Platform 创建要发布到 Teams 应用商店的应用。 Microsoft Power Platform 应用只能发布到组织的应用商店。

## <a name="make-your-chatbot-available-in-teams-through-the-power-virtual-agents-portal"></a>通过 Power Virtual Agents 门户使聊天机器人在 Teams 中可用

若要通过 Power Virtual Agents 门户使聊天机器人在 Teams 中可用，必须执行以下流程步骤：

若要使聊天机器人在 Teams 中可用，请执行以下操作：

1. **发布最新的机器人内容**  
在 Power Virtual Agents 门户中创建聊天机器人后，必须先发布机器人，然后 Teams 用户才能与它交互。 有关详细信息，请参阅[发布最新的机器人内容](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content)。

   ![在 Power Virtual Agents 门户中发布](../../assets/images/pva-publish.png)

1. **配置 Teams 频道**  
发布机器人后，添加 Teams 频道以使机器人可供 Teams 用户使用。

   ![Power Virtual Agents 门户中的频道](../../assets/images/pva-channels.png)

1. **为聊天机器人生成应用 ID**  
在为聊天机器人添加 Teams 频道后，系统会在对话框中生成 **应用 ID**。 应用 ID 是 Microsoft 为机器人生成的唯一标识符。 保存应用 ID 以创建用于 Teams 的应用包。

## <a name="add-your-bot-to-teams-using-app-studio"></a>使用 App Studio 将机器人添加到 Teams

如果已在 Teams 实例中[启用上传自定义应用](/microsoftteams/admin-settings)，则可以使用 Teams App Studio 直接上传聊天机器人并立即开始使用它。 若要共享聊天机器人，可以请求管理员在租户应用目录中提供机器人，也可以将应用包发送给其他人，并要求他们单独上传。

1. **在 Teams 安装 App Studio**  
App Studio 是一款 Teams 应用。 从 Teams 应用商店安装 App Studio，它可简化在 Teams 中创建和注册机器人的过程：

   1. 从 Teams 实例中选择应用商店图标，并搜索“**App Studio**”。

      &emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="../../assets/images/get-started/app-studio-store.png"/>

   1. 选择“**App Studio**”磁贴，然后在弹出对话框中选择“**安装**”。

      &emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

1. **在 App Studio 中创建 Teams 应用清单**  
Teams 中的机器人由应用清单 JSON 文件定义，该文件提供有关机器人及其功能的基本信息。 在 **App Studio** 中，选择“**清单编辑器**”，然后选择“**创建新应用**”。

    ![创建新应用](../../assets/images/get-started/create-new-app.png)

1. **添加机器人详细信息**  
完成所有必填字段。 有关每个字段的完整说明，请参阅[清单架构定义](../../resources/schema/manifest-schema.md)。

    ![添加应用详细信息](../../assets/images/get-started/add-app-details.png)

1. **设置机器人** 若要设置机器人，请执行以下步骤：
     1. 打开“**机器人**”选项卡。
     1. 选择“**设置**” > “**现有机器人**”，然后输入机器人的名称。

   ![机器人设置](../../assets/images/get-started/bot-set-up.png)

   下图描述了如何设置现有机器人：

   ![现有机器人设置](../../assets/images/get-started/existing-bot-set-up.png)

1. **添加应用 ID**  
若要添加应用 ID，请执行以下步骤：  
    1. 选择“**连接到其他机器人 ID**”，然后粘贴之前复制的 **应用 ID**。
    1. 选择“**范围**” > “**个人**” > “**保存**”。

    ![添加应用 ID](../../assets/images/get-started/add-app-id.png)

1. **为机器人添加有效域**  
仅当机器人要求用户登录时，才需要执行此步骤。 选择“**域和权限**”，然后在“**有效域**”字段中提供以下输入：

    ```bash
       token.botframework.com
    ```

1. **测试和分发机器人**  
打开“**测试和分发**”选项卡，然后选择“**安装**”，以将机器人直接添加到 Teams 实例。 或者，可以下载已完成的应用包以与 Teams 用户共享，或将其提供给管理员，以使机器人在租户应用目录中可用。

1. **开始聊天** 将 Power Virtual Agents 聊天机器人添加到 Teams 的设置过程已完成。 现在，你可以在个人聊天中开始与机器人对话。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [创建虚拟助手](~/samples/virtual-assistant.md)

## <a name="see-also"></a>另请参阅

* [Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)  
* [使用 Microsoft Power Virtual Agents 为 Teams 创建聊天机器人](../bot-features.md#bots-with-power-virtual-agents)
* [Power Virtual Agents 门户](https://powervirtualagents.microsoft.com)
* [发布 Power Virtual Agents 机器人](/power-virtual-agents/publication-fundamentals-publish-channels)
* [Microsoft Teams 中的安全性和合规性](/MicrosoftTeams/security-compliance-overview)
