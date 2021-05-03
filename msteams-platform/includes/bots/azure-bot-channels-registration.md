---
title: Azure 自动程序通道注册
description: 介绍了用于注册的 Azure 自动程序通道
localization_priority: Normal
ms.topic: overview
ms.author: surbhigupta12
ms.openlocfilehash: 3cbbd204daf98f1c3528dcb6efcfde299a402912
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020946"
---
1. 在 [Azure 门户的](https://ms.portal.azure.com/#home)"Azure 服务"下，选择 **"创建资源"。**
1. 在搜索框中输入"bot"。 在下拉列表中，选择自动 **程序频道注册**。
1. 选择" **创建"** 按钮。
1. 在" **自动程序通道注册"** 边栏选项卡中，提供有关自动程序的请求信息。
1. 现在 **，将"消息** 终结点"框留空，将在部署自动程序后输入所需的 URL。 下图显示了注册设置的示例：

    ![自动程序应用通道注册](../../assets/images/authentication/auth-bot-channels-registration.png)

1. 单击 **"Microsoft 应用 ID 和密码"，** 然后单击"**新建"。**

    ![创建 Microsoft 应用 ID ](../../assets/images/authentication/CreateMicrosoftAppID.png) ![ 创建新的 Microsoft 应用 ID](../../assets/images/authentication/CreateNewMicrosoftAppID.png)    

1. 单击 **"应用注册门户"链接中的"创建应用 ID"。**

   ![应用注册](../../assets/images/authentication/AppRegistration.png)
   
1. 在显示的 **"应用注册"** 窗口中，单击左上角 **的** "新建注册"选项卡。
1. 输入要注册的自动程序应用程序的名称，我们使用了 *BotTeamsAuth* (你需要选择自己的唯一名称) 。
1. 对于"支持的帐户类型"，选择"任何组织目录中的帐户 (任何 Azure AD 目录 - 多租户) 和个人 Microsoft 帐户 (例如 *Skype、Xbox) 。*
1. 单击" **注册"** 按钮。 完成后，Azure 将显示 *应用程序的* "概述"页。
1. 复制并保存到应用程序客户端 (**ID**) 文件。
1. 在左侧面板中，单击"**证书和密码"。**
    1. 在 *"客户端密码"* 下，单击 **"新建客户端密码"。**
    1. 添加描述，以便从可能需要为此应用创建的其他人识别此密码。
    1. 设置 *到期* 到你的选择。
    1. 单击“**添加**”。
    1. 复制客户端密码并将其保存到文件中。
1. 返回到自动 **程序通道注册** 窗口，并分别复制 **Microsoft 应用 ID** 和密码框中的应用 *ID* 和 **客户端** 密码。
1. 单击“**确定**”。
1. 最后，单击"**创建"。**

Azure 创建注册资源后，它将包含在资源组列表中。  

![自动程序应用通道注册组](~/assets/images/authentication/auth-bot-channels-registration-group.PNG)

创建自动程序通道注册后，你需要启用Teams通道。

1. 在 [Azure 门户的](https://ms.portal.azure.com/#home)"Azure 服务"下，选择刚 **创建的** 自动程序通道注册。
1. 在左侧面板中，单击"**频道"。**
1. 单击"Microsoft Teams图标，然后选择"保存 **"。**
