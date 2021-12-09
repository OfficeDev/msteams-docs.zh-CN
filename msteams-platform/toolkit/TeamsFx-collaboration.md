---
title: 使用 TeamsFx Project协作Teams Toolkit
author: yanjiang
description: 使用 TeamsFx Project协作Teams Toolkit
ms.author: rentu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 42949c9cdd3cb8e117925f170b2ab44e3bda1a1d
ms.sourcegitcommit: 97a64453410edbd2ba28e7a04e9c3a54bf48f4f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2021
ms.locfileid: "61391678"
---
# <a name="collaborate-on-teams-project-using-teams-toolkit"></a>使用Teams协作处理Teams Toolkit

多个开发人员可以协作为同一个 TeamsFx 项目调试、预配和部署，但需要手动设置 Teams 应用和 AAD 应用的权限，这并不容易。

Teams Toolkit现在支持协作功能，以允许开发人员 (项目所有者) 邀请其他开发人员 (协作者) 访问 TeamsFx 项目，以调试、预配和部署同一个 TeamsFx 项目。

## <a name="prerequisites"></a>先决条件

* 帐户先决条件

    若要在 Azure 和 Microsoft 365中预配云资源，必须拥有以下具有适当权限的帐户。 有关详细信息[，请参阅准备Teams应用](accounts.md)。

    * Microsoft 365
    * 具有有效订阅的 Azure

* [安装Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)版本 v3.0.0+。

> [!TIP]
> 你应该已经拥有一个Teams VS 代码打开的应用项目。

## <a name="collaborate-with-other-developers"></a>与其他开发人员协作

### <a name="as-a-project-owner"></a>作为项目所有者

> [!NOTE]
> 在添加环境的协作者之前，项目所有者需要 [先预配](provision.md) 项目。

* 在Teams Toolkit 上的"环境"部分中，将鼠标悬停在环境名称上以查找协作者按钮，一个按钮是"添加 **M365 Teams** 应用 (与 AAD 应用) 所有者"按钮，另一个按钮是"列出 **M365 Teams App (** 与 AAD App) 所有者"按钮，如下图所示：

  ![协作按钮](./images/collaboration-buttons.png)

* 选择 **"添加 M365 Teams应用** (与 AAD 应用) 所有者"按钮，并添加另一个 M365 帐户电子邮件地址作为协作者。 要添加的帐户必须与远程调试的项目 **所有者** 位于同一租户上，如图所示：

  ![输入协作者电子邮件](./images/collaboration-add-owner-email.png)

* 若要在当前环境中查看协作者，请选择"使用 AAD 应用) 所有者"按钮列出 **M365 Teams App (，** 然后协作者将在输出通道中列出，如下图所示：

  ![协作列表所有者](./images/collaboration-list-owners.png)

* 将项目推送到GitHub。

> [!NOTE]
> 新添加的协作者不会收到任何通知。 Project需要通知协作者。

### <a name="as-a-project-collaborator"></a>作为项目协作者

* 从项目复制GitHub
* 登录 M365 帐户

> [!NOTE]
> 协作者应该使用项目所有者添加的帐户登录，该帐户位于项目所有者的同一 **租户下**。

* 登录 Azure 帐户，该帐户对此项目中使用的所有 Azure 资源具有参与者权限。
* 使用项目代码，然后当你认为应该预览你的应用时，将项目部署到远程Teams应用。
* 启动远程，预览 Teams 应用。 有关详细信息，请参阅在远程[环境中生成并Teams应用](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=3&branch)。

### <a name="limitations"></a>限制

> [!NOTE]
> Azure 订阅管理员应在 Azure 门户上手动设置与 Azure 相关的权限。 Azure 帐户至少应为订阅提供参与者角色，以便开发人员可以协同工作来预配和部署 TeamsFx 项目。

1. **无法删除**：不能直接从扩展中删除协作Teams Toolkit者。 按照以下步骤手动删除协作者：

      1. 转到开发人员[Teams，](https://  dev.teams.microsoft.com/apps)按名称Teams或应用 ID 查找你的应用。
      2. 在"Teams管理"页中，从 **左侧面板** 中选择"所有者"。
      3. 查找并删除协作者。
      4. 转到 ["Azure Active Directory"，](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)**从左侧** 面板中选择"应用注册"，AAD应用"。
      5. 在"AAD管理"页中，从 **左侧面板** 中选择"所有者"。
      6. 查找并删除协作者。


1. 添加到项目的协作者不会收到任何通知。 Project需要通知协作者脱机。

## <a name="see-also"></a>另请参阅

> [!div class="nextstepaction"]
> [预配云资源](provision.md)

> [!div class="nextstepaction"]
> [将Teams应用部署到云](deploy.md)

> [!div class="nextstepaction"]
> [管理多个环境](TeamsFx-multi-env.md)
