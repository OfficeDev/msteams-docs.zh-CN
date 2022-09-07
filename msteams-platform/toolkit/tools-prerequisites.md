---
title: 使用Visual Studio Code创建 Teams 应用的先决条件
author: zyxiaoyuer
description: 在本模块中，了解工具和 SDK 所需的先决条件
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
ms.openlocfilehash: 412b7bfedb6ba39f1d38f42aac56cc793ea385b1
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617046"
---
# <a name="prerequisites-for-creating-your-teams-app"></a>创建 Teams 应用的先决条件

在开始创建 Teams 应用之前，请确保满足以下先决条件：

* [生成 Teams 应用的基本要求](#basic-requirements-to-build-your-teams-app)
* [准备帐户以生成 Teams 应用](#accounts-to-build-your-teams-app)
* [旁加载权限](#sideloading-permission)

## <a name="basic-requirements-to-build-your-teams-app"></a>生成 Teams 应用的基本要求

在开始生成 Teams 应用之前，请确保满足以下要求：

| &nbsp; | 基本要求 | 用于使用| 对于环境类型|
   | --- | --- | --- |
   | **必需** | &nbsp; | &nbsp; | &nbsp; |
   | &nbsp; | Teams 工具包| Microsoft Visual Studio Code扩展，用于为应用创建项目基架。 使用最新版本。 | JavaScript 和 SPFx|
   | &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | 通过聊天、会议、呼叫等应用与你协作的所有人协作 - 全部位于一个位置。| JavaScript 和 SPFx|
   | &nbsp; | [Node.js](https://nodejs.org/en/download/) | 后端 JavaScript 运行时环境。 使用最新的 v16 LTS 版本。| JavaScript 和 SPFx|
   | &nbsp; |[NPM (节点包管理器) ](https://www.npmjs.com/package/@microsoft/teamsfx) | 安装和管理包，以便在Node.js和 ASP.NET Core应用程序中使用。| JavaScript 和 SPFx|
   | &nbsp; | [微软&nbsp;边缘](https://www.microsoft.com/edge) (建议) 或 [Google Chrome](https://www.google.com/chrome/) | 包含开发人员工具的浏览器。 | JavaScript 和 SPFx|
   | &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download) | JavaScript、TypeScript 或 SharePoint 框架 (SPFx) 生成环境。 使用版本 1.55 或更高版本。 | JavaScript 和 SPFx|
   | **可选** | &nbsp; | &nbsp; | &nbsp; |
   | &nbsp; | [用于Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack)和 [Azure CLI 的 Azure](/cli/azure/install-azure-cli) 工具 | 访问存储的数据或为 Azure 中的 Teams 应用部署基于云的后端。 | JavaScript|
   | &nbsp; | [React适用于 Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi) 或 [React Microsoft&nbsp;Edge 开发人员工具的开发人员工具](https://microsoftedge.microsoft.com/addons/detail/react-developer-tools/gpphkfbcpidddadnkolkpfckpihlkkil) | 开源 React JavaScript 库的浏览器 DevTools 扩展。 | JavaScript|
   | &nbsp; | [Microsoft Graph 浏览器](https://developer.microsoft.com/graph/graph-explorer) | 一种基于浏览器的工具，可用于从 Microsoft Graph 数据运行查询。 | JavaScript 和 SPFx|
   | &nbsp; | [Teams 开发人员门户](https://dev.teams.microsoft.com/) | 基于 Web 的门户，用于配置、管理和分发 Teams 应用，包括组织或 Teams 应用商店。| JavaScript 和 SPFx|

   > [!NOTE]
   >
   > * 使用 Teams 工具包版本 4.0.0 和 Nodejs 版本 16 测试文档。
   > * 将 Microsoft Graph 资源管理器书签为书签，了解 Microsoft Graph 服务。 此基于浏览器的工具允许在应用外部查询和访问 Microsoft Graph。

## <a name="accounts-to-build-your-teams-app"></a>用于生成 Teams 应用的帐户

在开始生成 Teams 应用之前，请确保拥有以下帐户：

| 帐户 | 用于使用| 对于环境类型|
| --- | --- |
|[具有有效订阅的 Microsoft 365 帐户](#microsoft-365-developer-program)|开发应用时，Teams 开发人员帐户。| JavaScript 和 SPFx|
|[Azure 帐户](accounts.md#azure-account-to-host-backend-resources)|Azure 上的后端资源。| JavaScript 和 SPFx|
|[SharePoint 集合网站管理员帐户](#sharepoint-collection-site-administrator-account) |用于托管的部署。| SPFx|

### <a name="microsoft-365-developer-program"></a>Microsoft 365 开发人员计划

若要创建 Microsoft 365 帐户，请注册 Microsoft 365 开发人员计划订阅。 订阅免费使用 90 天，只要将订阅用于开发活动，就可以继续续订。

如果你有 Visual Studio Enterprise 或 Professional 订阅，则这两个计划都包含免费 Microsoft 365 [开发人员订阅](https://aka.ms/MyVisualStudioBenefits)。 只要你的 Visual Studio 订阅处于活动状态，它就处于活动状态。 有关详细信息，请参阅 [Microsoft 365 开发人员订阅](https://developer.microsoft.com/microsoft-365/dev-program)。

可以使用以下帐户类型之一注册开发人员计划:

* **Microsoft 帐户供个人使用**

  :::row:::

    :::column span="3":::

       该帐户提供对 Microsoft 产品和云服务 (如 Outlook、Messenger、OneDrive、MSN、Xbox Live 或 Microsoft 365) 的访问权限。 

       可以注册 Outlook.com 邮箱来创建 Microsoft 帐户，该Microsoft 帐户可用于访问与消费者相关的 Microsoft 云服务或 Azure。

    :::column-end:::
    :::column span="1":::
             :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/personal-account-icon.png" alt-text="个人帐户。":::
   :::column-end:::

  :::row-end:::

* **Microsoft 商业版工作帐户**

  :::row:::

    :::column span="3":::

       该帐户提供对所有小型、中型和企业级 Microsoft 云服务的访问权限。 这些服务包括 Azure、Microsoft Intune 或 Microsoft 365。 

       作为组织注册此类服务时，会在 Azure AD 中自动预配一个基于云的目录，来表示你的组织。

    :::column-end:::
    :::column span="1":::
             :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/work-account-icon.png" alt-text="工作帐户。":::
    :::column-end:::

  :::row-end:::

#### <a name="create-a-free-microsoft-365-developer-account"></a>创建免费的 Microsoft 365 开发人员帐户

若要创建免费的 Microsoft 365 开发人员帐户，请加入 Microsoft 365 开发人员计划并执行以下帐户：

1. 转到 [Microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program)。
1. 选择“**立即加入**”。
1. 设置管理员帐户。

   订阅完成后，可以看到以下图像:

    :::image type="content" source="../assets/images/teams-toolkit-v2/m365-account.png" alt-text="M365 帐户":::

### <a name="azure-account"></a>Azure 帐户

需要一个 Azure 帐户才能在 Visual Studio Code 中使用 Teams 工具包托管 Teams 应用或 Teams 应用的后端资源。 在以下情况下，必须需要 Azure 订阅：

* 如果已在除 Azure 以外的其他云提供商上拥有现有应用，并且想要在 Teams 平台上集成该应用，则必须具有 Azure 订阅。
* 可以选择一个 Azure 订阅，以使用另一个云提供商托管后端资源，或者在你自己的服务器上（如果从公共域中可用）。

> [!NOTE]
> 在开始之前，需要 [创建一个免费帐户](https://azure.microsoft.com/free/) 。

### <a name="sharepoint-collection-site-administrator-account"></a>SharePoint 集合网站管理员帐户

使用 SPFx 环境创建 Teams 应用时，需要在部署时使用 SharePoint 集合网站管理员帐户进行托管。 如果使用的是 Microsoft 365 开发人员计划租户，则可以使用当时创建的管理员帐户。

## <a name="sideloading-permission"></a>旁加载权限

创建应用后，必须在 Teams 中加载应用，而无需分发它。 此过程称为“旁加载”。 登录到 Microsoft 365 帐户以查看此选项。

可以使用 Visual Studio Code 或 Teams 客户端验证是否启用了旁加载权限。

<br>
<details>
<summary><b>使用 Visual Studio Code 验证旁加载权限</b></summary>

1. 打开 **Visual Studio Code**。
1. 从 Teams 工具包工具栏中选择 Teams 工具包 :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: 图标。

   > [!NOTE]
   > 如果看不到此选项，请参阅[安装 Teams 工具包](install-Teams-Toolkit.md)以在 Visual Studio Code 中安装 Teams 工具包扩展。
1. 选择 **“登录到帐户”下的 M365** 并登录到 Microsoft 365 帐户。

    :::image type="content" source="../assets/images/teams-toolkit-v2/accounts.png" alt-text="帐户详细信息":::

1. 检查是否可以查看选项“**已启用旁加载**”，如下图所示：

    :::image type="content" source="../assets/images/teams-toolkit-v2/sideloading.png" alt-text="启用旁加载":::

</details>
<br>
<details>
<summary><b>使用 Teams 客户端验证旁加载权限</b></summary>

1. 在 Teams 客户端中，选择 **“应用**”。
1. 选择 **“管理应用**”。
1. 选择 **“上传应用**”。

    :::image type="content" source="../assets/images/teams-toolkit-v2/upload-app.png" alt-text="发布应用":::

4. 检查是否可以看到选项“**上传自定义应用**”，如下图所示：

    :::image type="content" source="../assets/images/teams-toolkit-v2/upload-custom-app1.png" alt-text="上传自定义应用":::

</details>

### <a name="enable-sideloading-using-admin-center"></a>使用管理中心启用旁加载

如果无法查看“ **上传自定义应用”选项，** 则表示您没有旁加载所需的权限。

* 对于租户管理员，请在 Teams 管理中心为租户或组织启用旁加载设置。
* 如果你不是租户管理员，则需要联系租户管理员以启用旁加载。

如果拥有管理员权限，请执行以下步骤，使用管理中心上传自定义应用：

  1. 请使用管理员帐户登录到 [Microsoft 365 管理中心](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/)。

  1. :::image type="icon" source="../assets/images/teams-toolkit-v2/showall icon.PNG":::选择 Teams >图 **标。**

       :::image type="content" source="../assets/images/teams-toolkit-v2/m365-admin-center.png" alt-text="Microsoft 365 管理中心":::

     > [!Note]
     > 可能 **至多 24 小时** 后 **Teams** 选项才会出现。 可以[将自定义应用上传到 Teams 环境](/microsoftteams/upload-custom-apps)进行测试和验证。

  1. 使用管理员凭据登录到 Microsoft Teams 管理中心。
  1. :::image type="icon" source="../assets/images/teams-toolkit-v2/showall icon.PNG":::选择 **Teams 应用** > **设置策略**>图标。

     :::image type="content" source="../assets/images/teams-toolkit-v2/m365-admin-center1.png" alt-text="Microsoft 365 管理 center1":::

  1. 选择 **全局 (组织范围的默认)**

     :::image type="content" source="../assets/images/teams-toolkit-v2/select-manage-policies.png" alt-text="选择“管理策略”":::

  1. 将“**上传自定义应用**”切换到“**开**”位置。

     :::image type="content" source="../assets/images/teams-toolkit-v2/Upload-custom-apps.png" alt-text="上传自定义应用":::

  5. 选择 **保存**。

     > [!Note]
     > 旁加载最长可能需要 24 小时才能生效。 在此期间，可以使用“**为租户上传**”来测试应用。 若要上传应用的 .zip 包文件，请参阅“[上传自定义应用](/microsoftteams/teams-app-setup-policies)”。

     请确保现在已使用[使用 Visual Studio Code 或 Teams 客户端验证旁加载权限](#sideloading-permission)时所述的步骤获得旁加载权限。

</details>

## <a name="see-also"></a>另请参阅

* [在 Teams 中管理自定义应用策略和设置](/microsoftteams/teams-custom-app-policies-and-settings)
* [在 Teams 中管理应用设置策略](/microsoftteams/teams-app-setup-policies)
* [上传自定义应用](/microsoftteams/teams-app-setup-policies)
* [使用 Teams 工具包预配云资源](provision.md)
* [将 Teams 应用部署到云](deploy.md)
