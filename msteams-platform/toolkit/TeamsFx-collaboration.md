---
title: 使用 TeamsFx Project协作Teams Toolkit
author: yanjiang
description: 使用 TeamsFx Project协作Teams Toolkit
ms.author: rentu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 423e03e373edb1980186ea3dc43f2817d2e25636
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2022
ms.locfileid: "63452562"
---
# <a name="collaborate-on-teams-project-using-teams-toolkit"></a>使用Teams协作处理Teams Toolkit

多个开发人员可以一起为同一个 TeamsFx 项目调试、预配和部署，但需要手动设置 Teams App 和 Microsoft Azure Active Directory (Azure AD) App.Teams Toolkit 支持协作功能，以允许开发人员和项目所有者邀请其他开发人员或协作者加入 TeamsFx 项目，以调试、预配和部署同一个 TeamsFx 项目。

## <a name="prerequisites"></a>先决条件

* 帐户先决条件

    若要预配云资源，你必须具有以下帐户。 有关详细信息，请参阅准备[帐户以生成Teams应用](accounts.md)。

  * Microsoft 365 订阅
  * 具有有效订阅的 Azure

* [安装Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)版本 v3.0.0+。

> [!TIP]
> 确保已使用Teams打开一个应用Microsoft Visual Studio项目。

## <a name="collaborate-with-other-developers"></a>与其他开发人员协作

下面的列表指导我们了解协作过程及其限制：

### <a name="as-project-owner"></a>作为项目所有者

> [!NOTE]
> 在添加环境的协作者之前，项目所有者需要 [先预配](provision.md) 项目。

* 在 **"** 环境"部分Teams Toolkit，选择 **协作者**。 它显示选项添加 **Microsoft 365 Teams App (with Azure AD App) Owners** 和 **List Microsoft 365 Teams App (with Azure AD App) Owners**，如下图所示：

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/add collaborators.png" alt-text="协作者":::

* 选择 **"Microsoft 365 Teams应用 (应用Azure AD** 所有者) 添加其他Microsoft 365帐户电子邮件地址作为协作者。 要添加的帐户必须与远程调试的项目所有者位于同一租户上，如图所示：

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="添加环境":::

* 若要在当前环境中查看协作者，请选择"列出 Microsoft 365 Teams **App (with Azure AD App) Owners**"，然后在输出通道中列出协作者，如下图所示：

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/list of collaborators.png" alt-text="列表":::

* 将项目推送到GitHub。

> [!NOTE]
> 新添加的协作者不会收到任何通知。 Project需要通知协作者。

### <a name="as-project-collaborator"></a>作为项目协作者

* 从项目复制GitHub。
* 登录到Microsoft 365帐户。
* 登录到 Azure 帐户，该帐户对此项目中使用的所有 Azure 资源具有参与者权限。
* 若要预览 Teams应用，请远程部署项目。
* 启动远程，预览 Teams 应用。

有关详细信息，请参阅在远程[环境中生成并Teams应用程序](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=3&branch)。

> [!NOTE]
> 协作者必须使用项目所有者添加的帐户登录，该帐户位于项目所有者的同一租户下。

### <a name="limitation"></a>限制

你无法直接从扩展中删除协作Teams Toolkit者。 执行以下步骤以手动删除协作者：

  1. 转到开发人员Teams，然后按名称或Teams ID 选择你的应用。
  2. 从 **左侧面板** 中选择"所有者"。
  3. 选择并删除协作者。
  4. 转到"[Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)"**，从左侧** 面板中选择"应用注册"，然后找到Azure AD应用。
  5. 从 **应用管理** 页的左侧Azure AD选择所有者。
  6. 选择并删除协作者。

> [!NOTE]
>
> * 添加到项目的协作者不会收到任何通知。 Project需要通知协作者脱机。
> * Azure 订阅管理员必须在 Azure 订阅门户上手动设置与 Azure Microsoft Azure权限。 Azure 帐户必须具有订阅的参与者角色，以便开发人员可以协同工作来预配和部署 TeamsFx 项目。

## <a name="see-also"></a>另请参阅

* [预配云资源](provision.md)
* [将 Teams 应用部署到云](deploy.md)
* [管理多个环境](TeamsFx-multi-env.md)
