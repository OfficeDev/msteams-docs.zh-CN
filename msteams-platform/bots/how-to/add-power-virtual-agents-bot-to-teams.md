---
title: 将 Power Virtual Agents 聊天机器人添加到 Teams
author: laujan
description: 在 Teams 平台中集成 Power Virtual Agents 聊天机器人
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: d6d9f4292e22df7ca0f5841a2fc579b9e3b1d2f3
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020088"
---
# <a name="add-power-virtual-agents-chatbot"></a>添加 Power Virtual Agents 聊天机器人 

Power Virtual Agents 是无代码的引导式图形界面解决方案，它使团队的每位成员能够创建丰富的对话聊天机器人，这些聊天机器人可轻松与 Teams 平台集成。 在 Power Virtual Agents 中创作的所有内容在 Teams 中自然呈现。 Power Virtual Agents bots engage with users in the Teams native chat canvas. IT 管理员、业务分析师、域专家和经验丰富的应用开发人员无需设置开发环境即可为 Teams 设计、开发和发布智能虚拟代理。 他们可以创建 Web 服务，或直接在 Bot Framework 中注册。 

本文档指导你了解如何通过 Power Virtual Agents 门户在 Teams 中提供聊天机器人，以及如何使用 App Studio 将聊天机器人添加到 Teams。 

Power Virtual Agents 允许你创建功能强大的聊天机器人，这些聊天机器人可以回答客户、其他员工或您的网站或服务的访问者提出的问题。

无需数据工作者或开发人员，即可轻松创建这些机器人。

> [!NOTE]
> 通过将聊天机器人添加到 Microsoft Teams，一些数据（如聊天机器人内容和用户聊天内容）会与 Microsoft Teams 共享。 这意味着你的数据流在组织的合规性以及地理或 [区域边界之外](/power-virtual-agents/data-location)。 <br/>

## <a name="make-your-chatbot-available-in-teams-through-the-power-virtual-agents-portal"></a>通过 Power Virtual Agents 门户在 Teams 中提供聊天机器人

若要通过 Power Virtual Agents 门户在 Teams 中提供聊天机器人，必须执行以下过程步骤：

**使聊天机器人在 Teams 中可用**

1. **发布最新的自动程序内容**  
在 Power Virtual Agents 门户创建聊天机器人后，必须先发布聊天机器人，Teams 用户才能与之交互。 有关详细信息，请参阅发布 [最新的自动程序内容](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content)。

   ![在电源虚拟代理门户中发布](../../assets/images/pva-publish.png)

1. **配置 Teams 频道**  
发布自动程序后，添加 Teams 频道，使机器人可供 Teams 用户使用。

   ![电源虚拟代理门户中的通道](../../assets/images/pva-channels.png)

1. **为聊天机器人生成应用 ID**  
将 Teams 频道添加到聊天机器人 **后，在** 对话框中生成应用 ID。 应用 ID 是 Microsoft 为自动程序生成的唯一标识符。 保存应用 ID，为 Teams 创建应用包。

## <a name="add-your-bot-to-teams-using-app-studio"></a>使用 App Studio 将机器人添加到 Teams

如果在 [Teams 实例中](/microsoftteams/admin-settings) 启用了上载自定义应用，可以使用 Teams App Studio 直接上载聊天机器人并立即开始使用它。 若要共享聊天机器人，你可以请求管理员在租户应用目录中提供机器人，也可以将应用包发送给其他人，让他们单独上传它。

1. **在 Teams 安装 App Studio**  
App Studio 是一款 Teams 应用。 从 Teams 应用商店安装 App Studio，从而简化 Teams 中的机器人创建和注册过程： 

   1. 从 Teams 实例中选择应用商店图标，然后搜索 **App Studio**。

      &emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="../../assets/images/get-started/app-studio-store.png"/>   

   1. 选择 **App Studio** 磁贴 **，然后选择弹出** 对话框中的"安装"。

      &emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

1. **在 App Studio 创建 Teams 应用清单**  
Teams 中的聊天机器人由应用清单 JSON 文件定义，该文件提供有关机器人及其功能的基本信息。 在 **App Studio** 中， **选择清单编辑器**，然后选择 **创建新应用**。  
下图指导你在 App Studio 中创建新应用：  

   ![创建新应用](../../assets/images/get-started/create-new-app.png)

1. **添加机器人详细信息**  
完成所有必填字段。 有关每个字段的完整说明，请参阅 [清单架构定义](../../resources/schema/manifest-schema.md)。   
下图指导你添加应用详细信息：  

   ![添加应用详细信息](../../assets/images/get-started/add-app-details.png)

1. **设置自动程序** 若要设置自动程序，请执行以下步骤： 
     1. 打开 **"机器人"** 选项卡。 
     1. 选择 **"**  >  **设置现有自动** 程序"，然后输入机器人的名称。

   下图指导你设置自动程序：    

   ![自动程序设置](../../assets/images/get-started/bot-set-up.png) 

   下图指导你设置现有自动程序：      

   ![现有自动程序设置](../../assets/images/get-started/existing-bot-set-up.png)    
1. **添加应用 ID**  
若要添加应用 ID，请执行以下步骤：  
    1. 选择 **"连接到其他自动程序 ID"，****并粘贴** 之前复制的应用 ID。 
    1. 选择 **"作用域**  >  **个人**  >  **保存"。**      
下图指导你设置现有自动程序：    

   ![添加应用 ID](../../assets/images/get-started/add-app-id.png)

1. **为自动程序添加有效域**  
只有当机器人要求用户登录时，才需要执行此步骤。 选择 **"域和权限"，** 在" **有效域** "字段中提供以下输入：

    ```bash
       token.botframework.com
    ```

7.  **测试和分发机器人**  
打开 **"测试和分发"** 选项卡，然后选择 **"安装** "以将机器人直接添加到 Teams 实例。 或者，你可以下载已完成的应用包以与 Teams 用户共享，或提供给管理员，使机器人在租户应用目录中可用。

8. **启动聊天**   
将 Power Virtual Agents 聊天机器人添加到 Teams 的设置过程已完成。 现在可以在个人聊天中与机器人开始对话。

## <a name="see-also"></a>另请参阅
> [!div class="nextstepaction"]
> [Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)  

> [!div class="nextstepaction"]
> [使用 Microsoft Power Virtual Agents 为 Teams 创建聊天机器人](../bot-features.md#bots-and-the-microsoft-power-virtual-agents)。  

> [!div class="nextstepaction"]
>  [Power Virtual Agents 门户](https://powervirtualagents.microsoft.com)

> [!div class="nextstepaction"]
> [发布 Power Virtual Agents 机器人](/power-virtual-agents/publication-fundamentals-publish-channels)

> [!div class="nextstepaction"]
> [Microsoft Teams 中的安全性和合规性](/MicrosoftTeams/security-compliance-overview)。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [创建虚拟助理](~/samples/virtual-assistant.md)

