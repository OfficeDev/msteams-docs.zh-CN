---
title: 向 Teams 机器人添加身份验证
author: surbhigupta
description: 了解如何使用 Azure AD 使用第三方 OAuth 提供程序在 Teams 中的机器人应用中启用身份验证。
ms.topic: how-to
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: ff7e4e8d3ffede250bd89ecca7b0e3d8054a646b
ms.sourcegitcommit: 0ac53c430c055897ecebc129eab49336820c18c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2022
ms.locfileid: "67618329"
---
# <a name="add-authentication-to-your-teams-bot"></a>向 Teams 机器人添加身份验证

有时，可能需要在可代表用户访问资源的Microsoft Teams 中创建机器人，例如邮件服务。

本文演示如何基于 OAuth 2.0 使用 Azure 机器人服务 v4 SDK 身份验证。 这样可以更轻松地开发可以基于用户凭据使用身份验证令牌的机器人。 这一切的关键是使用 **标识提供者**，我们将在稍后看到。

OAuth 2.0 是 Microsoft Azure Active Directory (Azure AD) 和许多其他身份提供程序用于身份验证和授权的开放标准。 对 OAuth 2.0 的基本理解是在 Teams 中使用身份验证的先决条件。

有关基本了解，请参阅 [OAuth 2 简化](https://aka.ms/oauth2-simplified)，有关完整规范，请参阅 [OAuth 2.0](https://oauth.net/2/)。

有关 Azure 机器人服务如何处理身份验证的详细信息，请参阅[对话中的用户身份验证](https://aka.ms/azure-bot-authentication)。 

在本文中，您将了解：

- **如何创建已启用身份验证的机器人**。 你将使用 [cs-auth-sample][teams-auth-bot-cs] 来处理用户登录凭据和生成身份验证令牌。
- **如何将机器人部署到 Azure 并将其与标识提供程序关联**。 提供程序根据用户登录凭据颁发令牌。 机器人可以使用令牌访问需要身份验证的资源，例如邮件服务。 有关详细信息，请参阅  [适用于机器人的 Microsoft Teams 身份验证流](auth-flow-bot.md)。
- **如何在 Microsoft Teams 中集成机器人**。 集成机器人后，可以在聊天中登录并与其交换消息。

## <a name="prerequisites"></a>先决条件

- 了解 [机器人基础知识][concept-basics]、[管理状态][concept-state]、[对话库][concept-dialogs]以及如何 [实现顺序会话流][simple-dialog]。
- 了解 Azure 和 OAuth 2.0 开发。
- Microsoft Visual Studio 和 Git 的当前版本。
- Azure AD 帐户。 如果需要，可以创建 [Azure 免费帐户](https://azure.microsoft.com/free/)。
- 下面是一些示例方案：

    | 示例 | BotBuilder 版本 | 演示 |
    |:---|:---:|:---|
    | [cs-auth-sample 中的][teams-auth-bot-cs]**机器人身份验证** | v4 | OAuthCard 支持 |
    | [js-auth-sample 中的][teams-auth-bot-js]**机器人身份验证** | v4| OAuthCard 支持  |
    | [py-auth-sample 中的][teams-auth-bot-py]**机器人身份验证** | v4 | OAuthCard 支持 |

## <a name="create-the-resource-group"></a>创建资源组

资源组和服务计划不是严格必需的，但它们允许你方便地释放创建的资源。 这是保持资源井然有序且可管理的好做法。

使用资源组为 Bot Framework 创建单个资源。 为了提高性能，请确保这些资源位于同一 Azure 区域。

1. 在浏览器中，登录到 [**Microsoft Azure 门户**][azure-portal]。
1. 在左侧导航面板中，选择“**资源组**”。
1. 在显示窗口左上角，选择“**添加** ”选项卡以创建新的资源组。 系统将提示你提供以下内容：
    1. **订阅**。 使用现有订阅。
    1. **资源组**。 请输入名称和资源组。 例如 *TeamsResourceGroup*。 请记住，该名称必须是唯一的。
    1. 在“**区域**”下拉菜单中，选择“*美国西部*”或“靠近应用程序的区域”。
    1. 选择“**审阅并创建**”按钮。 应会看到一条横幅，其中读取了 *传递的验证*。
    1. 选择“**创建**”按钮。 创建资源组可能需要几分钟时间。

> [!TIP]
> 与本教程稍后将创建的资源一样，最好将此资源组固定到仪表板，以便轻松访问。 如果要执行此操作，请在仪表板右上角选择固定图标 &#128204;。

## <a name="create-the-service-plan"></a>创建服务计划

1. 在 [**Azure 门户**][azure-portal]的左侧导航面板上，选择“**创建资源**”。
1. 在搜索框中，键入 *App 服务计划*。 从搜索结果中选择 **App 服务计划** 卡。
1. 选择“**创建**”。
1. 你将能够查看以下信息：
    1. **订阅**。 可以使用现有订阅。
    1. **资源组**。 选择之前创建的组。
    1. **名称**。 输入服务计划的名称。 例如 *TeamsServicePlan*。 请记住，该名称在组中必须是唯一的。
    1. **操作系统**。 选择 *Windows* 或适用的 OS。
    1. **区域**。 选择 *美国西部* 或靠近应用程序的区域。
    1. **定价层**。 确保已选择 *标准 S1* 。 这应该是默认值。
    1. 选择“**审阅并创建**”按钮。 应会看到一条横幅，其中读取了 *传递的验证*。
    1. 选择“**创建**”。 创建应用服务计划可能需要几分钟时间。 计划将列在资源组中。

## <a name="create-azure-bot-resource-registration"></a>创建 Azure 机器人资源注册

Azure 机器人资源注册将 Web 服务注册为 Bot Framework 的机器人，该机器人为你提供 Microsoft 应用 ID 和应用密码 (客户端机密) 。

> [!IMPORTANT]
> 仅当机器人未托管在 Azure 中时，才需要注册它。 如果通过 Azure 门户[创建了机器人](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true)，则该机器人已注册到服务。 如果通过 [Bot Framework](https://dev.botframework.com/bots/new) 或 [开发人员门户](../../../concepts/build-and-test/teams-developer-portal.md) 创建了机器人，则机器人不会在 Azure 中注册。

1. 在“**创建资源**”部分中访问 [**Azure 门户**][azure-portal]，并搜索 **Azure 机器人**。
1. 打开 **Azure 机器人**，并选择“**创建**”。
1. 在机器人句柄字段中输入 **机器人句柄** 名称。
1. 从下拉列表中选择 **订阅** 。
1. 从下拉列表中选择 **资源组** 。
1. 选择 **应用类型** 作为 **Microsoft 应用 ID** 的 **多租户**。

   :::image type="content" source="../../../assets/images/adaptive-cards/multi-tenant.png" alt-text="此屏幕截图显示了如何为 Microsoft AppID 选择多租户。":::

1. 然后“**审阅 + 创建**”。

   :::image type="content" source="../../../assets/images/adaptive-cards/create-azure-bot.png" alt-text="此屏幕截图显示了如何创建 Azure 机器人。":::

1. 如果验证通过，请选择“**创建**”。

    预配机器人服务需要一些时间。

   :::image type="content" source="../../../assets/images/adaptive-cards/validation-pane.png" alt-text="此屏幕截图显示 Azure 机器人验证如何通过。":::

1. 选择“**转到资源**”。 机器人和相关资源在资源组中列出。

   :::image type="content" source="../../../assets/images/adaptive-cards/go-to-resource-card.png" alt-text="此屏幕截图显示了如何选择资源组。":::

    现在，Azure 机器人已创建。

   :::image type="content" source="../../../assets/images/adaptive-cards/azure-bot-ui.png" alt-text="此屏幕截图显示了如何创建 Azure 机器人资源。":::

若要创建客户端机密，请执行以下操作：

1. 在 **设置** 中，选择“**配置**”。 保存 **Microsoft 应用 ID**（客户端 ID）供将来参考。

   :::image type="content" source="../../../assets/images/adaptive-cards/config-microsoft-app-id.png" alt-text="此屏幕截图显示了如何添加 Microsoft 应用 ID 以创建客户端机密。":::

1. 在 **Microsoft 应用 ID** 旁边，选择 **“管理**”。

   :::image type="content" source="~/assets/images/manage-bot-label.png" alt-text="此屏幕截图显示了如何创建管理机器人。":::

1. 在“**客户端机密**”部分中，选择“**新建客户端机密**”。将显示“**添加客户端机密**”窗口。

   :::image type="content" source="../../../assets/images/meetings-side-panel/newclientsecret.PNG" alt-text="此屏幕截图显示了如何创建新的客户端机密。":::

1. 输入“**说明**”并选择“**添加**”。

   :::image type="content" source="../../../assets/images/adaptive-cards/client-secret.png" alt-text="屏幕截图显示了如何输入客户端机密的说明。":::

1. 在“**值**”列中，选择“**复制到剪贴板**”并保存客户端机密 ID 以供将来参考。

   :::image type="content" source="../../../assets/images/adaptive-cards/client-secret-value.png" alt-text="屏幕截图显示了如何保存客户端机密 ID 以供将来参考。":::

若要添加 Microsoft Teams 频道：

1. 转到“**主页**”。

   :::image type="content" source="../../../assets/images/adaptive-cards/bot-home-page.png" alt-text="此屏幕截图显示机器人主页。":::

1. 打开“**最近资源**”部分中列出的机器人。

1. 在左窗格中选择“**频道**”，然后选择 **Microsoft Teams**:::image type="icon" source="../../../assets/icons/teams-icon.png":::。

   :::image type="content" source="../../../assets/images/adaptive-cards/channel-teams.png" alt-text="此屏幕截图显示了如何在频道中选择 Teams。":::

1. 选中该复选框以接受服务条款，然后选择 “**同意**”。</br>

   :::image type="content" source="../../../assets/images/adaptive-cards/select-terms-of-service.png" alt-text="此屏幕截图显示了如何在服务时设置条款。":::

1. 选择“**保存**”。

   :::image type="content" source="../../../assets/images/adaptive-cards/select-teams.png" alt-text="此屏幕截图显示了如何添加 Microsoft Teams 频道。":::

有关更多信息，请参阅“[为 Teams 创建应用](../create-a-bot-for-teams.md)”。

## <a name="create-the-identity-provider"></a>创建标识提供程序

你需要一个可用于身份验证的标识提供程序。
在此过程中，将使用 Azure AD 提供程序;还可以使用其他 Azure AD 支持的标识提供者。

1. 在 [**Azure 门户**][azure-portal]的左侧导航面板上，选择 **Azure Active Directory**。
    > [!TIP]
    > 需要在可以许可应用程序请求委托权限的租户中创建并注册 此Azure AD 资源。
    > 有关创建租户的说明，请参阅“[访问门户并创建租户](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)”。
1. 在左侧面板中，选择“**应用注册**”。
1. 在右侧面板中，选择左上角的“**新建注册**”选项卡。
1. 你将能够查看以下信息：
   1. **名称**。 为新的服务应用程序输入一个名称。 例如 *BotTeamsIdentity*。 请记住，该名称必须是唯一的。
   1. 选择应用程序“**支持的帐户类型**”。 *选择任何组织目录中的帐户 (任何Microsoft Azure Active Directory (Azure AD) - 多租户) 和个人 Microsoft 帐户 (，例如 Skype、Xbox)*。
   1. 对于 **重定向 URI**：<br/>
       &#x2713;选择 **Web**。<br/>
       &#x2713;将 URL 设置为 `https://token.botframework.com/.auth/web/redirect`.
   1. 选择“**注册**”。

1. 创建后，Azure 会显示应用的 **“概述** ”页。 将以下信息复制并保存到文件：

    1. **应用程序（客户端）ID** 值。 稍后在机器人中注册此 Azure 标识应用程序时，将使用此值作为 *客户端 ID* 。
    1. **目录 (租户) ID** 值。 稍后还将使用此值作为 *租户 ID* ，将此 Azure 标识应用程序注册到机器人。

1. 在左侧面板中，选择 **证书和机密** ，为应用程序创建客户端机密。

   1. 在“**客户端机密**”下，选择&#x2795;“**新建客户端机密**”。
   1. 添加说明，从可能需要为此应用创建的其他人（如 *Teams 中的 Bot 标识应用）* 中标识此机密。
   1. 将“**截止期限**”设置为所选内容。
   1. 选择“**添加**”。
   1. 在离开此页面之前，**请记录机密**。 稍后在向机器人注册 Azure AD 应用程序时，将使用此值作为“*客户端机密*”。

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a>配置标识提供程序连接，并将其注册到机器人

请注意，此处有两个服务提供商选项 - Azure AD V1 和 Azure AD V2。  [此](/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison)处汇总了两个提供程序之间的差异，但一般来说，V2 在更改机器人权限方面提供了更大的灵活性。  图形 API 权限列在范围字段中，并且随着新权限的添加，机器人将允许用户在下一次登录时同意新权限。  对于 V1，用户必须删除机器人同意，才能在 OAuth 对话框中提示新的权限。

#### <a name="microsoft-azure-active-directory-azure-ad-v1"></a>Microsoft Azure Active Directory (Azure AD) V1

1. 在 [**Azure 门户**][azure-portal]中，从仪表板中选择资源组。
1. 选择机器人注册链接。
1. 打开资源页，然后在“**设置**”下选择“**配置**”。
1. 选择“**添加 OAuth 连接设置**”按钮。
   下图在资源页中显示相应的选择：

   ![SampleAppDemoBot 配置](~/assets/images/authentication/sample-app-demo-bot-configuration.png)

1. 如下所示完成表单：

    1. **名称**。 输入连接的名称。 你将在 `appsettings.json` 文件的机器人中使用此名称。 例如， *BotTeamsAuthADv1*。
    1. **服务提供程序**。 选择 **Microsoft Azure Active Directory (Azure AD)**。 选择此选项后，将显示特定于 Azure AD 的字段。
    1. **客户端 ID**。在上述步骤中输入为 Azure 标识提供程序应用记录的应用程序 （客户端）ID。
    1. **客户端密码**。 在上述步骤中输入为 Azure 标识提供程序应用记录的机密。
    1. **授权类型**。 输入 `authorization_code`。
    1. **登录 URL**。 输入 `https://login.microsoftonline.com`。
    1. **租户 ID**，输入之前为 Azure 标识应用记录 **的目录（租户）ID** ，或创建标识提供程序应用时选择的受支持帐户类型的 **常见 ID** 。 若要确定要分配的值，请遵循以下条件：

        - 如果 *选择此组织目录中的帐户仅 (仅 Microsoft -* *Azure AD) - 多租户 (Microsoft Azure Active Directory (任何组织目录中的单租户) ) 或帐户，请* 输入前面记录的 **租户 ID** Microsoft Azure Active Directory (Azure AD) 应用。 这将是与可进行身份验证用户关联的租户。

        - 如果 *在任何组织目录中选择了帐户 (任何Microsoft Azure Active Directory (Azure AD) - 多租户和个人 Microsoft 帐户，例如 Skype、Xbox、Outlook)* 输入 **通用** 字词，而不是租户 ID。 否则，Azure AD (Azure AD) 应用将通过选中其 ID 的租户进行验证，并排除个人 Microsoft 帐户。

    h. 对于 **资源 URL**，请输入 `https://graph.microsoft.com/`。 当前代码示例中未使用此功能。  
    i. 将 **范围** 留空。 下图是一个示例：

    :::image type="content" source="../../../assets/images/authentication/auth-bot-identity-connection-adv1.PNG" alt-text="此屏幕截图显示了如何添加 Teams 机器人身份验证机器人标识连接 adv1。":::

1. 选择“保存”。

#### <a name="microsoft-azure-active-directory-azure-ad-v2"></a>Microsoft Azure Active Directory (Azure AD) V2

1. 在 [**Azure 门户**][azure-portal]中，从仪表板中选择 Azure 机器人。
1. 在资源页中，选择“**设置**”下的“**配置**”。
1. 选择“**添加 OAuth 连接设置**”按钮。  
   下图在资源页中显示相应的选择：

   :::image type="content" source="../../../assets/images/authentication/sample-app-demo-bot-configuration.png" alt-text="此屏幕截图显示了资源页中的相应选择。":::

1. 如下所示完成表单：

    1. **名称**。 输入连接的名称。 你将在 `appsettings.json` 文件的机器人中使用此名称。 例如， *BotTeamsAuthADv2*。
    1. **服务提供程序**。 选择 **Microsoft Azure Active Directory v2**。 选择此选项后，将显示特定于 Azure AD 的字段。
    1. **客户端 ID**。在上述步骤中输入为 Azure 标识提供程序应用记录的应用程序 （客户端）ID。
    1. **客户端密码**。 在上述步骤中输入为 Azure 标识提供程序应用记录的机密。
    1. **令牌 Exchange URL**。 将其留空。
    1. **租户 ID**，输入之前为 Azure 标识应用记录 **的目录（租户）ID** ，或创建标识提供程序应用时选择的受支持帐户类型的 **常见 ID** 。 若要确定要分配的值，请遵循以下条件：

        - 如果 *选择此组织目录中的帐户仅 (仅限 Microsoft - 单租户)* 或 *Microsoft Azure Active directory - 多租户)  (的任何组织目录中的帐户*，请输入之前为 Azure AD 应用记录的 **租户 ID** 。 这将是与可进行身份验证用户关联的租户。

        - 如果 *在任何组织目录中选择了帐户 (任何Microsoft Azure Active Directory (Azure AD) - 多租户和个人 Microsoft 帐户，例如 Skype、Xbox、Outlook)* 输入 **通用** 字词，而不是租户 ID。 否则，Azure AD 应用将通过选中其 ID 的租户进行验证，并排除个人 Microsoft 帐户。

    1. 对于 **作用域**，请输入此应用程序所需的图形权限的空间分隔列表，例如：User.Read User.ReadBasic.All Mail.Read

1. 选择“保存”。

### <a name="test-the-connection"></a>测试连接

1. 选择连接条目以打开创建的连接。
1. 在“**服务提供程序连接设置**”面板顶部选择“**测试连接**”。
1. 首次执行此操作时，将打开一个新的浏览器窗口，要求你选择一个帐户。 选择要使用的帐户。
1. 接下来，系统将要求你允许标识提供程序使用你的数据（凭据）。 下图是一个示例：

   :::image type="content" source="../../../assets/images/authentication/auth-bot-connection-test-accept.PNG" alt-text="屏幕截图显示了如何添加 Teams 机器人身份验证连接字符串 adv1。":::

1. 选择“**接受**”。
1. 然后，这应会将你重定向 到“**测试连接到\<your-connection-name>成功**”页。 如果收到错误，请刷新页面。 下图是一个示例：

   :::image type="content" source="../../../assets/images/authentication/auth-bot-connection-test-token.PNG" alt-text="屏幕截图显示了如何添加 Teams 应用身份验证连接字符串 adv1。":::

机器人代码使用连接名称检索用户身份验证令牌。

## <a name="prepare-the-bot-sample-code"></a>准备机器人示例代码

完成初步设置后，让我们重点介绍如何创建要在本文中使用的机器人。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

1. 克隆 [cs-auth-sample][teams-auth-bot-cs]。
1. 启动 Visual Studio。
1. 在工具栏中，选择 **“文件->打开->项目/解决方案** ”并打开机器人项目。
1. 在 C# 中，更新 **appsettings.json** ，如下所示：

    - 设置 `ConnectionName` 为添加到机器人注册的标识提供程序连接的名称。 本示例中使用的名称是 *BotTeamsAuthADv1*。
    - 设置 `MicrosoftAppId` 为机器人注册时保存的 **机器人应用 ID** 。
    - 设置 `MicrosoftAppPassword` 为机器人注册时保存的 **客户机密** 。

    根据机器人机密中的字符，可能需要 XML 转义密码。 例如，需要将任何 ampersands (&) 编码为 `&amp;`。

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. 在解决方案资源管理器中，导航到`TeamsAppManifest`文件夹，打开`manifest.json`并设置`id`和`botId`到机器人注册时保存的 **机器人应用 ID**。

# <a name="javascript"></a>[JavaScript](#tab/node-js)

1. 克隆 [node-auth-sample][teams-auth-bot-js]。
1. 在控制台中，导航到项目： </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. 安装模块</br></br>
`npm install`
1. 按如下所示更新 **.env** 配置：

    - 设置 `MicrosoftAppId` 为机器人注册时保存的 **机器人应用 ID** 。
    - 设置 `MicrosoftAppPassword` 为机器人注册时保存的 **客户机密** 。
    - 将 `connectionName` 设置为标识提供程序连接的名称。
    根据机器人机密中的字符，可能需要 XML 转义密码。 例如，需要将任何 ampersands (&) 编码为 `&amp;`。

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. 在 `teamsAppManifest` 文件夹中，打开 `manifest.json` 并设置 `id`  为 **Microsoft 应用 ID** 和 `botId` 机器人注册时保存的 **机器人应用 ID** 。

# <a name="python"></a>[Python](#tab/python)

1. 从 github 存储库克隆 [py-auth-sample][teams-auth-bot-py]。
1. 更新 **config.py**：

    - 设置 `ConnectionName` 为添加到机器人的 OAuth 连接设置的名称。
    - 设置 `MicrosoftAppId` 为机器人的应用 ID，以及 `MicrosoftAppPassword` 为应用机密。

      根据机器人机密中的字符，可能需要 XML 转义密码。 例如，需要将任何 ampersands (&) 编码为 `&amp;`。

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a>将机器人部署到 Azure

若要部署机器人，请按照“如何将 [机器人部署到 Azure](https://aka.ms/azure-bot-deployment-cli)”中的步骤进行操作。

或者，在 Visual Studio 中，可以执行以下步骤：

1. 在 Visual Studio *解决方案资源管理器* 中，选择并按住 (或右键单击) 项目名称。
1. 在显示的下拉菜单中，选择“**发布**”。
1. 在显示的窗口中，选择“**新建**”链接。
1. 在对话框窗口中，选择左侧的“**App 服务**”，并在右侧“**创建新建**”。
1. 选择“**发布**”按钮。
1. 在下一个对话框窗口中，输入所需的信息。 示例如下：

   :::image type="content" source="../../../assets/images/authentication/auth-bot-app-service.png" alt-text="此屏幕截图显示了如何输入身份验证应用服务所需的信息。":::

1. 选择“**创建**”。
1. 如果部署成功完成，应会在 Visual Studio 中看到它。 此外，默认浏览器中会显示一个页面，表示 *机器人已准备就绪！*。 URL 如下所示：`https://botteamsauth.azurewebsites.net/`。 将其保存到文件。
1. 在浏览器中，导航到 [**Azure 门户**][azure-portal]。
1. 检查资源组，机器人应与其他资源一起列出。 下图是一个示例：

   :::image type="content" source="../../../assets/images/authentication/auth-bot-app-service-in-group.png" alt-text="此屏幕截图显示了如何检查资源组和机器人。":::

1. 在资源组中，选择机器人注册名称（链接）。
1. 在左侧面板中，选择“**设置**”。
1. 在“**消息传送终结点**”框中，输入上述获取的 URL，然后输入 `api/messages`。 这是一个示例： `https://botteamsauth.azurewebsites.net/api/messages`。
    > [!NOTE]
    > 机器人只允许一个消息传送终结点。
1. 选择左上角的“**保存**”按钮。

## <a name="test-the-bot-using-the-emulator"></a>使用 Emulator 测试机器人

如果尚未完成，请安装 [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme)。 另请参阅[使用 Emulator 进行调试](https://aka.ms/bot-framework-emulator-debug-with-emulator)。

若要使机器人示例登录有效，必须配置Emulator。

### <a name="configure-the-emulator-for-authentication"></a>为身份验证配置 Emulator

如果机器人需要身份验证，则必须配置Emulator。 配置：

1. 启动 Emulator。
1. 在 Emulator 中，选择左下角的齿轮图标&#9881;或右上角的 **Emulator 设置** 选项卡。
1. 选中“**使用版本 1.0 身份验证令牌**”框。
1. 输入 **ngrok** 工具的本地路径。 *请参阅* Bot Framework Emulator/ngrok 隧道集成 [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok))。 有关详细工具信息，请参阅 [ngrok](https://ngrok.com/)。
1. **启动 Emulator 时，按“运行 ngrok”** 选中框。
1. 选择“**保存**”按钮。

当机器人显示登录卡，并且用户选择登录按钮时，Emulator 将打开一个页面，用户可以使用该页面与身份验证提供程序一起登录。
用户执行此操作后，提供程序将生成用户令牌并将其发送到机器人。 之后，机器人可以代表用户执行操作。

### <a name="test-the-bot-locally"></a>测试本地机器人

配置身份验证机制后，可以执行实际的机器人测试。  

1. 例如，通过 Visual Studio 在计算机上本地运行机器人示例。
1. 启动 Emulator。
1. 选择“**打开机器人**”按钮。
1. 在 **机器人 URL** 中，输入机器人的本地 URL。 路径通常为 `http://localhost:3978/api/messages`。
1. 在 **Microsoft 应用 ID** 中从 `appsettings.json` 输入机器人的应用 ID。
1. 在 **Microsoft 应用密码中** 从 `appsettings.json` 输入机器人的应用密码。
1. 选择“**连接**”。
1. 机器人启动并运行后，输入任何文本以显示登录卡。
1. 选择“**登录**”按钮。
1. 将显示一个弹出对话框以 **确认打开 URL**。 这是为了允许机器人的用户（你）进行身份验证。  
1. 选择“**确认**”。
1. 如果有要求，请选择适用用户的帐户。
1. 根据用于 Emulator 的配置，可获得以下配置之一：
    1. **使用登录验证码**  
      &#x2713;打开显示验证代码的窗口。  
      &#x2713;在聊天框中复制并输入验证代码以完成登录。
    1. **使用身份验证令牌**。  
      &#x2713;你已根据凭据登录。

    下图是登录后机器人 UI 的示例：

    :::image type="content" source="../../../assets/images/authentication/auth-bot-login-emulator.PNG" alt-text="此屏幕截图显示了登录后机器人 UI 的示例。":::

1. 如果在机器人询问 *是否要查看令牌* 时选择 **“是**”，你会得到如下所示的响应：

   :::image type="content" source="../../../assets/images/authentication/auth-bot-login-emulator-token.png" alt-text="此屏幕截图显示了如何选择同意。":::

1. 在输入聊天框中输入 **注销** 以注销。这会释放用户令牌，在你再次登录之前，机器人将无法代表你执行操作。

> [!NOTE]
> 机器人身份验证需要使用 **Bot Connector 服务**。 该服务访问机器人的机器人注册信息。

## <a name="test-the-deployed-bot"></a>测试部署机器人

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. 在浏览器中，导航到 [**Azure 门户**][azure-portal]。
1. 查找资源组。
1. 选择资源链接。 将显示资源页。
1. 在资源页中，选择“**在 Web 聊天测试**”。 机器人启动并显示预定义的问候语。
1. 在聊天框中键入任何内容。
1. 选择“**登录**”框。
1. 将显示一个弹出对话框以 **确认打开 URL**。 这是为了允许机器人的用户（你）进行身份验证。  
1. 选择“**确认**”。
1. 如果有要求，请选择适用用户的帐户。
    下图是登录后机器人 UI 的示例：

   :::image type="content" source="../../../assets/images/authentication/auth-bot-login-deployed.PNG" alt-text="此屏幕截图显示了登录后 Teams 机器人 UI 的示例。":::

1. 选择“**是**”按钮以显示身份验证令牌。 下图是一个示例：

   :::image type="content" source="../../../assets/images/authentication/auth-bot-login-deployed-token.PNG" alt-text="此屏幕截图显示了如何选择“是”按钮以显示身份验证令牌。":::

1. 输入注销以注销。

   :::image type="content" source="../../../assets/images/authentication/auth-bot-deployed-logout.PNG" alt-text="此屏幕截图显示了如何输入注销以注销。":::

> [!NOTE]
> 如果登录时遇到问题，请尝试再次测试连接，如前面的步骤中所述。 这可以重新创建身份验证令牌。
> 使用 Azure 中的 Bot Framework Web 聊天客户端，可能需要多次登录，然后才能正确建立身份验证。

## <a name="install-and-test-the-bot-in-teams"></a>在 Teams 中安装和测试机器人

1. 在机器人项目中，确保 `TeamsAppManifest` 文件夹包含 `manifest.json` 随附文件 `outline.png` 和 `color.png` 文件。
1. 在解决方案资源管理器中，导航到 `TeamsAppManifest` 文件夹。 通过分配以下值进行编辑 `manifest.json` ：
    1. 确保在机器人注册时收到的 **机器人应用 ID** 已分配到 `id` 和 `botId`分配。
    1. 分配此值：`validDomains: [ "token.botframework.com" ]`。
1. 选择并 **压缩**`manifest.json`、`outline.png`文件和`color.png`文件。
1. 打开 **Microsoft Teams**。
1. 在左侧面板的底部，选择“**应用图标**”。
1. 在右侧面板的底部，选择“**上传自定义应用**”。
1. 导航到 `TeamsAppManifest` 文件夹并上传压缩清单。
系统将显示导入作业向导：

   :::image type="content" source="../../../assets/images/authentication/auth-bot-teams-upload.png" alt-text="此屏幕截图显示了机器人上传到 Teams 后的示例。":::

1. 选择“**添加到团队**”按钮。
1. 在下一个窗口中，选择要在其中使用机器人的团队。
1. 选择“**设置机器人**”按钮。
1. 选择左侧面板中的三个点 (&#x25cf;&#x25cf;&#x25cf;) 。 然后选择 **“开发人员门户** ”图标。
1. 选择“**清单编辑器** ”选项卡。应该会看到上传的机器人的图标。
1. 此外，你应该能够在聊天列表中看到机器人作为联系人列出，可以使用该联系人与机器人交换消息。

### <a name="testing-the-bot-locally-in-teams"></a>在 Teams 中本地测试机器人

Teams 是一种完全基于云的产品，它要求其访问的所有服务都可使用 HTTPS 终结点从云中获取。 因此，若要使机器人（示例）在 Teams 中工作，需要将代码发布到所选云中，或者使本地运行的实例可通过 **隧道** 工具在外部访问。 我们建议使用 [ngrok](https://ngrok.com/download)，它为在计算机上本地打开的端口创建外部可寻址 URL。
若要设置 ngrok 以准备在本地运行 Teams 应用，请执行以下步骤：

1. 在终端窗口中，转到已安装 `ngrok.exe` 目录。 建议将 *环境变量* 路径设置为指向该变量。
1. 例如，运行 `ngrok http 3978 --host-header=localhost:3978`。 根据需要替换端口号。
这会启动 ngrok 来侦听指定的端口。 作为回报，它为你提供了一个外部可寻址的 URL，只要 ngrok 正在运行，该 URL 就有效。 下图是一个示例：

   :::image type="content" source="../../../assets/images/authentication/auth-bot-ngrok-start.PNG" alt-text="此屏幕截图显示 Teams 机器人应用身份验证连接字符串 adv1":::

1. 复制转发 HTTPS 地址。 具体应如下所示：`https://dea822bf.ngrok.io/`。
1. 追加 `/api/messages` 以获取 `https://dea822bf.ngrok.io/api/messages`。 这是在计算机上本地运行的机器人 **的消息终结点** ，可在 Teams 的聊天中通过 Web 访问。
1. 要执行的最后一步是更新已部署机器人的消息终结点。 在该示例中，我们在 Azure 中部署了机器人。 因此，让我们执行以下步骤：
    1. 在浏览器中，导航到 [**Azure 门户**][azure-portal]。
    1. 选择 **机器人注册**。
    1. 在左侧面板中，选择“**设置**”。
    1. 在右侧面板的“**消息传送**”终结点 框中，在示例 `https://dea822bf.ngrok.io/api/messages` 中输入 ngrok URL。
1. 在本地启动机器人，例如在 Visual Studio 下调试模型。
1. 使用 Bot Framework 门户的 **测试 Web 聊天** 在本地运行时测试机器人。 与 Emulator 一样，此测试不允许访问特定于 Teams 的功能。
1. 在运行的终端窗口 `ngrok` 中，可以看到机器人与 Web 聊天客户端之间的 HTTP 流量。 如果需要更详细的视图，请在浏览器窗口中输入 `http://127.0.0.1:4040` 从上一个终端窗口获取的视图。 下图是一个示例：

   :::image type="content" source="../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png" alt-text="此屏幕截图显示了身份验证机器人团队 ngrok 测试。":::

> [!NOTE]
> 如果停止并重新启动 ngrok，URL 会更改。 若要在项目中使用 ngrok，并且根据使用的功能，必须更新所有 URL 引用。

## <a name="additional-information"></a>其他信息

### <a name="teamsappmanifestmanifestjson"></a>TeamsAppManifest/manifest.json

此清单包含 Teams 与机器人连接所需的信息：  

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0.0",
  "id": "",
  "packageName": "com.teams.auth.bot",
  "developer": {
    "name": "TeamsBotAuth",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.teams.com/privacy",
    "termsOfUseUrl": "https://www.teams.com/termsofuse"
  },
  "icons": {
    "color": "color.png",
    "outline": "outline.png"
  },
  "name": {
    "short": "TeamsBotAuth",
    "full": "Teams Bot Authentication"
  },
  "description": {
    "short": "TeamsBotAuth",
    "full": "Teams Bot Authentication"
  },
  "accentColor": "#FFFFFF",
  "bots": [
    {
      "botId": "",
      "scopes": [
        "groupchat",
        "team"
      ],
      "supportsFiles": false,
      "isNotificationOnly": false
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [ "token.botframework.com" ]
}
```

通过身份验证，Teams 的行为与其他频道略有不同，如下所述。

### <a name="handling-invoke-activity"></a>处理调用活动

**调用活动** 将发送到机器人，而不是其他频道使用的事件活动。
这是通过对 **ActivityHandler** 进行子分类来完成的。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet-sample)

**Bots/DialogBot.cs**

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

**Bots/TeamsBot.cs**

如果使用 **OAuthPrompt**，则必须将“*调用活动*”转发到对话框。

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a>TeamsActivityHandler.cs

```csharp

protected virtual Task OnInvokeActivityAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    switch (turnContext.Activity.Name)
    {
        case "signin/verifyState":
            return OnSigninVerifyStateAsync(turnContext, cancellationToken);

        default:
            return Task.CompletedTask;
    }
}

protected virtual Task OnSigninVerifyStateAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    return Task.CompletedTask;
}
```

# <a name="javascript"></a>[JavaScript](#tab/node-js-dialog-sample)

**bots/dialogBot.js**

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

**bots/teamsBot.js**

如果使用 **OAuthPrompt**，则必须将“*调用活动*”转发到对话框。

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

**dialogs/mainDialog.js**

在对话步骤中，使用 `beginDialog` 启动 OAuth 提示符，要求用户登录。

- 如果用户已登录，则会生成令牌响应事件，而不会提示用户。
- 否则，这会提示用户登录。 Azure 机器人服务在用户尝试登录后发送令牌响应事件。

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

在以下对话步骤中，检查上一步的结果中是否存在令牌。 如果它不是 null，则用户将成功登录。

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

**bots/logoutDialog.js**

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[Python](#tab/python-sample)

**bots/dialog_bot.py**

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

**bots/teams_bot.py**

如果使用 **OAuthPrompt**，则必须将“*调用活动*”转发到对话框。

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

**dialogs/main_dialog.py**

在对话步骤中，使用 `begin_dialog` 启动 OAuth 提示符，要求用户登录。

- 如果用户已登录，则会生成令牌响应事件，而不会提示用户。
- 否则，这会提示用户登录。 Azure 机器人服务在用户尝试登录后发送令牌响应事件。

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

在以下对话步骤中，检查上一步的结果中是否存在令牌。 如果它不是 null，则用户将成功登录。

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

**dialogs/logout_dialog.py**

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

## <a name="code-sample"></a>代码示例

本部分提供机器人身份验证 v3 SDK 示例。

| **示例名称** | **说明** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| 机器人身份验证 | 此示例演示如何开始在适用于 Teams 的机器人中进行身份验证。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| 选项卡、机器人和消息扩展 (ME) SSO | 此示例演示用于选项卡、机器人和 ME 的 SSO - 搜索、操作、linkunfurl。 |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | 不可用 |

## <a name="see-also"></a>另请参阅

[通过 Azure 机器人服务添加身份验证](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: /azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true
[concept-state]: /azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0&preserve-view=true
[concept-dialogs]: /azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0&preserve-view=true
[simple-dialog]: /azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0&preserve-view=true

[teams-auth-bot-cs]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[teams-auth-bot-js]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth
