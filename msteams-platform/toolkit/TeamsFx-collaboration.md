---
title: 使用 Teams Toolkit 协作处理 TeamsFx Project
author: yanjiang
description: 使用 Teams Toolkit 协作处理 TeamsFx Project
ms.author: rentu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 099820252fd83a2d916e8d61f3b83b63291695e9
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2022
ms.locfileid: "66124016"
---
# <a name="collaborate-on-teams-project-using-teams-toolkit"></a>使用 Teams 工具包协作处理 Teams 项目

多个开发人员可以协同工作，为同一 TeamsFx 项目进行调试、预配和部署，但它需要手动设置Teams应用的适当权限，并Microsoft Azure Active Directory (Azure AD) 应用。 Teams Toolkit支持协作功能，使开发人员和项目所有者能够邀请其他开发人员或协作者加入 TeamsFx 项目来调试、预配和部署同一 TeamsFx 项目。

## <a name="prerequisites"></a>先决条件

* Microsoft 365 订阅
* 具有有效订阅的 Azure
  
  有关不同帐户的详细信息，请参阅[准备帐户以生成Teams应用](accounts.md)。

* [安装Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)版本 v3.0.0+

> [!TIP]
> 确保已在Visual Studio Code中打开Teams应用项目。

## <a name="collaborate-with-other-developers"></a>与其他开发人员协作

以下列表指导我们了解协作过程及其限制：

* 作为项目所有者

  > [!NOTE]
  > 在为环境添加协作者之前，项目所有者需要先 [预配](provision.md) 项目。

  1. 在Teams Toolkit的 **“环境**”部分中，选择 **协作者**。 它显示使用 **Azure AD 应用) 所有者添加Microsoft 365 Teams应用 (** 的选项，以及 **Azure AD 应用) 所有者的列表Microsoft 365 Teams应用 (**，如下图所示：

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/add collaborators.png" alt-text="合作":::

  2. 选择 **“使用 Azure AD 应用) 所有者添加Microsoft 365 Teams应用 (**，并将其他Microsoft 365帐户电子邮件地址添加为协作者。 要添加的帐户必须与远程调试的项目所有者位于同一租户上，如下图所示：

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="add envi":::

  3. 若要查看当前环境中的合作者，请选择 **Azure AD 应用) 所有者的“列出Microsoft 365 Teams应用 (”**，然后在输出通道中列出协作者，如下图所示：

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/list of collaborators.png" alt-text="列表":::

  4. 将项目推送到GitHub

     > [!NOTE]
     > 新添加的合作者不会收到任何通知。 Project所有者需要通知协作者。

* 作为项目协作者

  1. 从 GitHub 克隆项目。
  2. 登录到Microsoft 365帐户。
  3. 登录到 Azure 帐户，它对项目中使用的所有 Azure 资源具有参与者权限。
  4. 若要预览Teams应用，请将项目部署到远程。
  5. 启动远程以预览Teams应用。

     > [!NOTE]
     > 协作者必须使用项目所有者与项目所有者在同一租户下添加的帐户登录。 有关详细信息，请参阅[在远程环境中生成和运行Teams应用](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=3&branch)。

### <a name="limitations"></a>限制

如果要从Teams Toolkit扩展中删除协作者，则需要手动删除，因为无法直接删除它们。 执行以下步骤以手动删除协作者：

* 使用开发人员门户

  * 转到[Teams开发人员门户](https://dev.teams.microsoft.com/home)，按名称或应用 ID 选择Teams应用。
  * 从左侧面板中选择 **“所有者** ”。
  * 选择并删除协作者。

* 使用Azure Active Directory

  * 转到 [Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)，从左侧面板中选择 **“应用注册**”，然后找到 Azure AD 应用。
  * 在 Azure AD 应用管理页的左侧面板中选择 **“所有者** ”。
  * 选择并删除协作者。

   > [!NOTE]
   >
   > * 添加到项目的合作者不会收到任何通知。 Project所有者需要脱机通知协作者。
   > * Azure 相关权限必须在Azure 门户时由 Azure 订阅管理员手动设置。 Azure 帐户必须具有订阅的参与者角色，以便开发人员可以协同工作来预配和部署 TeamsFx 项目。

## <a name="see-also"></a>另请参阅

* [预配云资源](provision.md)
* [将 Teams 应用部署到云](deploy.md)
* [管理多个环境](TeamsFx-multi-env.md)
