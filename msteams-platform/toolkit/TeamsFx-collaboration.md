---
title: 使用 Teams 工具包协作处理 TeamsFx 项目
author: yanjiang
description: 使用 Teams 工具包协作处理 TeamsFx 项目
ms.author: rentu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: be36cf1af9741d65d66ede498f5ac2fff31df148
ms.sourcegitcommit: ff31cbe4840191f004d8fc61dd4fd93d35fcaecb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2022
ms.locfileid: "65938868"
---
# <a name="collaborate-on-teams-project-using-teams-toolkit"></a>使用 Teams 工具包协作处理 Teams 项目

多个开发人员可以共同为同一 TeamsFx 项目进行调试、预配和部署，但它需要手动设置 Teams 应用和 Microsoft Azure Active Directory (Azure AD) 应用的适当权限。 Teams 工具包支持协作功能，使开发人员和项目所有者能够邀请其他开发人员或协作者加入 TeamsFx 项目，以调试、预配和部署相同的 TeamsFx 项目。

## <a name="prerequisites"></a>先决条件

* Microsoft 365 订阅
* 具有有效订阅的 Azure
  
  有关不同帐户的详细信息，请参阅 [准备帐户以生成 Teams 应用](accounts.md)。

* [安装 Teams 工具包](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) 版本 v3.0.0+

> [!TIP]
> 确保在 Visual Studio Code 中打开了 Teams 应用项目。

## <a name="collaborate-with-other-developers"></a>与其他开发人员协作

以下列表指导我们了解协作过程及其限制：

* 作为项目所有者

  > [!NOTE]
  > 在为环境添加协作者之前，项目所有者需要先 [预配](provision.md) 项目。

  1. 在 Teams 工具包的 **“环境** ”部分中，选择 **协作者**。 它显示将 **Microsoft 365 Teams 应用 (与 Azure AD 应用) 所有者一起添加** 和 **列出 Microsoft 365 Teams 应用 (与 Azure AD 应用) 所有者** 的选项，如下图所示：

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/add collaborators.png" alt-text="合作":::

  2. 选择 **使用 Azure AD 应用) 所有者添加 Microsoft 365 Teams 应用 (** ，并添加其他 Microsoft 365 帐户电子邮件地址作为协作者。 要添加的帐户必须与远程调试的项目所有者位于同一租户上，如下图所示：

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="add envi":::

  3. 若要查看当前环境中的合作者，请选择 **“列出 Microsoft 365 Teams 应用 (与 Azure AD 应用) 所有者**，然后协作者在输出通道中列出，如下图所示：

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/list of collaborators.png" alt-text="列表":::

  4. 将项目推送到 GitHub

     > [!NOTE]
     > 新添加的合作者不会收到任何通知。 项目所有者需要通知协作者。

* 作为项目协作者

  1. 从 GitHub 克隆项目。
  2. 登录到 Microsoft 365 帐户。
  3. 登录到 Azure 帐户，它对项目中使用的所有 Azure 资源具有参与者权限。
  4. 若要预览 Teams 应用，请将项目部署到远程。
  5. 启动远程以预览 Teams 应用。

     > [!NOTE]
     > 协作者必须使用项目所有者与项目所有者在同一租户下添加的帐户登录。 有关详细信息，请参阅在 [远程环境中生成和运行 Teams 应用](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=3&branch)。

### <a name="limitations"></a>限制

若要从 Teams 工具包扩展中删除协作者，需要手动删除，因为无法直接删除协作者。 执行以下步骤以手动删除协作者：

* 使用开发人员门户

  * 转到 [Teams 开发人员门户](https://dev.teams.microsoft.com/home) ，按名称或应用 ID 选择 Teams 应用
  * 从左侧面板中选择 **“所有者”**
  * 选择并删除协作者

* 使用 Azure Active Directory

  * 转到 [Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)，从左侧面板中选择 **应用注册** ，然后找到 Azure AD 应用
  * 在 Azure AD 应用管理页的左侧面板中选择 **“所有者”**
  * 选择并删除协作者

   > [!NOTE]
   >
   > * 添加到项目的合作者不会收到任何通知。 项目所有者需要脱机通知协作者。
   > * Azure 门户上的 Azure 订阅管理员必须手动设置 Azure 相关权限。 Azure 帐户必须具有订阅的参与者角色，以便开发人员可以协同工作来预配和部署 TeamsFx 项目。

## <a name="see-also"></a>另请参阅

* [预配云资源](provision.md)
* [将 Teams 应用部署到云](deploy.md)
* [管理多个环境](TeamsFx-multi-env.md)
