---
title: 向你的团队 bot 添加身份验证
author: clearab
description: 如何：将 OAuth 身份验证添加到 Microsoft 团队中的 bot。
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 403072efeccdd09e46ac93e2e811ee2d10131668
ms.sourcegitcommit: aabfd65a67e1889ec16f09476bc757dd4a46ec5b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2020
ms.locfileid: "48097884"
---
# <a name="add-authentication-to-your-teams-bot"></a>向你的团队 bot 添加身份验证

有时，您可能需要在 Microsoft 团队中创建可代表用户访问资源的 bot，如邮件服务。

本文演示如何使用基于 OAuth 2.0 的 Azure Bot 服务 v4 SDK 身份验证。 这样，就可以更轻松地开发可使用基于用户凭据的身份验证令牌的 bot。 关键是使用 **标识提供程序**，因为我们将在后面看到。

OAuth 2.0 是一种开放标准，用于 Azure Active Directory (Azure AD) 和许多其他标识提供程序使用的身份验证和授权。 对 OAuth 2.0 的基本了解是在团队中使用身份验证的先决条件。

有关基本了解，请参阅 [oauth 2 已简化](https://aka.ms/oauth2-simplified) ，有关完整规范，则为 [oauth 2.0](https://oauth.net/2/) 。

有关 Azure Bot 服务如何处理身份验证的详细信息，请参阅 [对话中的用户身份验证](https://aka.ms/azure-bot-authentication)。

在本文中，您将了解：

- **如何创建启用身份验证的 bot**。 你将使用 [cs-auth 示例][teams-auth-bot-cs] 来处理用户登录凭据和生成身份验证令牌。
- **如何将机器人部署到 Azure 并将其与标识提供程序关联**。 提供程序根据用户登录凭据发出令牌。 Bot 可以使用令牌访问需要身份验证的资源，如邮件服务。 有关详细信息，请参阅  [适用于 bot 的 Microsoft 团队身份验证流](auth-flow-bot.md)。
- **如何在 Microsoft 团队中集成机器人**。 将 bot 集成后，可以在聊天中登录并与之交换邮件。

## <a name="prerequisites"></a>先决条件

- 有关 [机器人基础][concept-basics]知识、 [管理状态][concept-state]、 [对话框库][concept-dialogs]以及如何 [实施顺序对话流][simple-dialog]的知识。
- Azure 和 OAuth 2.0 开发方面的知识。
- 当前版本的 Visual Studio 和 Git。
- Azure 帐户。 如果需要，可以创建 [Azure 免费帐户](https://azure.microsoft.com/free/)。
- 下面的示例。

    | 示例 | BotBuilder 版本 | 示 |
    |:---|:---:|:---|
    | Cs 中的**Bot 身份验证**- [auth-示例][teams-auth-bot-cs] | v4 | OAuthCard 支持 |
    | [Js-auth][teams-auth-bot-js]中的**Bot 身份验证**-示例 | v4| OAuthCard 支持  |
    | [Py-auth][teams-auth-bot-py]中的**Bot 身份验证**-示例 | v4 | OAuthCard 支持 |

## <a name="create-the-resource-group"></a>创建资源组

资源组和服务计划不是必需的，但它们使您可以方便地释放所创建的资源。 这对于保持资源的组织和可管理性来说是很好的做法。

您可以使用资源组为 Bot 框架创建单独的资源。 为了提高性能，请确保这些资源位于同一个 Azure 区域中。

1. 在您的浏览器中，登录到 [**Azure 门户**][azure-portal]。
1. 在左侧导航窗格中，选择 " **资源组**"。
1. 在显示的窗口的左上角，选择 " **添加** " 选项卡以创建新的资源组。 系统将提示你提供以下内容：
    1. **订阅**。 使用现有订阅。
    1. **资源组**。 输入资源组的名称。 例如，  *TeamsResourceGroup*。 请记住，该名称必须是唯一的。
    1. 从 " **区域** " 下拉菜单中，选择 " *美国西部*" 或 "接近您的应用程序的区域"。
    1. 选择 " **查看" 和 "创建** " 按钮。 您应该会看到标题为 "已 *通过验证*"。
    1. 选择 " **创建** " 按钮。 创建资源组可能需要几分钟的时间。

> [!TIP]
> 与本教程后面创建的资源一样，最好将此资源组固定到您的仪表板以便轻松访问。 如果您想要这样做，请选择 pin 图标 & # 128204;在仪表板的右上方。

## <a name="create-the-service-plan"></a>创建服务计划

1. 在 [**Azure 门户**][azure-portal]的左侧导航窗格中，选择 " **创建资源**"。
1. 在 "搜索" 框中，键入 *App Service Plan*。 从搜索结果中选择 **应用服务计划** 卡片。
1. 选择“创建”****。
1. 系统将要求你提供以下信息：
    1. **订阅**。 您可以使用现有订阅。
    1. **资源组**。 选择之前创建的组。
    1. **名称**。 输入服务计划的名称。 例如，  *TeamsServicePlan*。 请记住，此名称在组中必须是唯一的。
    1. **操作系统**。 选择 " *Windows* " 或 "适用的操作系统"。
    1. **区域**。 选择 " *西部* " 或 "区域接近您的应用程序"。
    1. **定价层**。 确保选择了 " *标准 S1* "。 此值应为默认值。
    1. 选择 " **查看" 和 "创建** " 按钮。 您应该会看到标题为 "已 *通过验证*"。
    1. 选择“创建”****。 可能需要几分钟的时间来创建应用服务计划。 该计划将列在资源组中。

## <a name="create-the-bot-channels-registration"></a>创建 bot 通道注册

如果你有 Microsoft 应用 Id 和应用密码 (客户端机密) ，bot 通道注册会将您的 web 服务注册为 bot 框架的 bot。

> [!IMPORTANT]
> 仅当你的 bot 未托管在 Azure 中时，才需要注册你的 bot。 如果你通过 Azure 门户 [创建了一个 bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) ，则它已向该服务注册。 如果你通过 [Bot 框架](https://dev.botframework.com/bots/new) 或 [AppStudio](~/concepts/build-and-test/app-studio-overview.md) 创建了你的 bot，你的 Bot 不会在 Azure 中注册。

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

> [!NOTE]
> 自动程序通道注册资源将显示 **全局** 区域，即使您选择了 "西部我们"。 这是预期的。

有关详细信息，请参阅为 [团队创建机器人](../create-a-bot-for-teams.md)。

## <a name="create-the-identity-provider"></a>创建标识提供程序

您需要可用于身份验证的标识提供程序。
在此过程中，你将使用 Azure AD 提供程序;此外，还可以使用其他受支持的 Azure AD 标识提供程序。

1. 在 [**Azure 门户**][azure-portal]的左侧导航窗格中，选择 " **Azure Active Directory**"。
    > [!TIP]
    > 你将需要在可同意委派应用程序请求的租户中创建并注册此 Azure AD 资源。
    > 有关创建租户的说明，请参阅 [访问门户和创建租户](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)。
1. 在左面板中，选择 " **应用注册**"。
1. 在右侧面板中，选择左上角的 " **新建注册** " 选项卡。
1. 系统将要求你提供以下信息：
   1. **名称**。 输入应用程序的名称。 例如，  *BotTeamsIdentity*。 请记住，该名称必须是唯一的。
   1. 为您的应用程序选择 **支持的帐户类型** 。 选择任何 * (任何 AZURE AD 目录-多租户) 和个人 Microsoft 帐户 (例如 Skype、Xbox) 的组织目录中的 "帐户" *。
   1. 对于 **重定向 URI**：<br/>
       &#x2713;选择 " **Web**"。 <br/>
       &#x2713; 将 URL 设置为 `https://token.botframework.com/.auth/web/redirect` 。
   1. 选择“**注册**”。

1. 创建后，Azure 将显示该应用程序的 " **概述** " 页。 将下面的信息复制并保存到一个文件中：

    1. **应用程序 (客户端) ID**值。 将此 Azure 标识应用程序注册到你的 bot 时，你将在稍后将此值用作 *客户端 ID* 。
    1. **目录 (租户) ID**值。 您还将此值用作 *租户 ID* ，以向你的 bot 注册此 Azure 标识应用程序。

1. 在左面板中，选择 " **证书 & 密码** " 以创建应用程序的客户端密码。

   1. 在 " **客户端密码**" 下，选择 &#x2795; **新的客户端密码**。
   1. 添加描述以标识来自其他用户可能需要为此应用程序创建的此机密，如 *团队中的 Bot 标识应用程序*。
   1. 将 **过期** 时间设置为您所做的选择。
   1. 选择“**添加**”。
   1. 在离开此页面之前，请 **记录此密码**。 在你将 Azure AD 应用程序注册到你的 bot 时，你将在稍后将此值用作 _客户端密码_ 。

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a>配置标识提供程序连接，并将其注册到机器人

注意-服务提供商有两个选项-Azure AD V1 和 Azure AD V2。  [这里](https://docs.microsoft.com/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison)汇总了两个提供程序之间的差异，但一般来说，V2 提供了有关更改 bot 权限的更多灵活性。  Graph API 权限在 "范围" 字段中列出，并在添加新权限时，bot 将允许用户在下一个登录时同意新权限。  对于 V1，用户必须删除机器人许可，以获取在 OAuth 对话框中提示的新权限。 

#### <a name="azure-ad-v1"></a>Azure AD V1

1. 在 [**Azure 门户**][azure-portal]中，从仪表板中选择资源组。
1. 选择你的 bot 频道注册链接。
1. 在 "资源" 页上，选择 " **设置**"。
1. 在页面底部附近的 " **OAuth 连接设置** " 下，选择 " **添加设置**"。
1. 如下所示完成表单：

    1. **名称**。 输入连接的名称。 您将在文件的 bot 中使用此名称 `appsettings.json` 。 例如 *BotTeamsAuthADv1*。
    1. **服务提供商**。 选择“**Azure Active Directory**”。 选择此项后，将显示 Azure AD 特有的字段。
    1. **客户端 id**。在上面的步骤中，输入您为 Azure 标识提供程序应用程序记录的应用程序 (客户端) ID。
    1. **客户端密码**。 在上面的步骤中，输入您为 Azure 标识提供程序应用程序记录的密码。
    1. **授予类型**。 Enter `authorization_code` 。
    1. **登录 URL**。 Enter `https://login.microsoftonline.com` 。
    1. **租户 ID**，输入您之前为您的 Azure 标识应用程序记录的 **目录 (租户) ID** ，或根据您创建标识提供程序应用程序时选择的受支持的帐户类型（ **常见** ）。 若要确定要分配的值，请执行以下条件：

        - 如果选择了 "仅 *在此组织目录中的帐户 * " （仅限 microsoft *AAD 目录-"多租户" 中 * 的 "仅 microsoft 单一租户) " 或 "帐户" (中的 "帐户" () 请输入您之前为 AAD 应用程序记录的 **租户 ID** 。 这将是与可以进行身份验证的用户关联的租户。

        - 如果您在 *任何 AAD 目录中选择了任何组织目录 (的帐户-多租户和个人 Microsoft 帐户（例如 Skype、Xbox、Outlook) * 输入 " **通用** 词" 而不是 "租户 ID"）。 否则，AAD 应用将通过已选择 ID 的租户进行验证，并排除个人 Microsoft 帐户。

    水平. 对于 " **资源 URL**"，请输入 `https://graph.microsoft.com/` 。 当前代码示例中不使用此代码。  
    i. 将 **范围** 保留为空。 下面的图像是一个示例：

    ![团队 bot 应用程序身份验证连接字符串 adv1 视图](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. 选择“**保存**”。

#### <a name="azure-ad-v2"></a>Azure AD V2

1. 在 [**Azure 门户**][azure-portal]中，从仪表板中选择资源组。
1. 选择你的 bot 频道注册链接。
1. 在 "资源" 页上，选择 " **设置**"。
1. 在页面底部附近的 " **OAuth 连接设置** " 下，选择 " **添加设置**"。
1. 如下所示完成表单：

    1. **名称**。 输入连接的名称。 您将在文件的 bot 中使用此名称 `appsettings.json` 。 例如 *BotTeamsAuthADv2*。
    1. **服务提供商**。 选择 " **Azure Active Directory v2**"。 选择此项后，将显示 Azure AD 特有的字段。
    1. **客户端 id**。在上面的步骤中，输入您为 Azure 标识提供程序应用程序记录的应用程序 (客户端) ID。
    1. **客户端密码**。 在上面的步骤中，输入您为 Azure 标识提供程序应用程序记录的密码。
    1. **令牌交换 URL**。 将此留空。
    1. **租户 ID**，输入您之前为您的 Azure 标识应用程序记录的 **目录 (租户) ID** ，或根据您创建标识提供程序应用程序时选择的受支持的帐户类型（ **常见** ）。 若要确定要分配的值，请执行以下条件：

        - 如果选择了 "仅 *在此组织目录中的帐户 * " （仅限 microsoft *AAD 目录-"多租户" 中 * 的 "仅 microsoft 单一租户) " 或 "帐户" (中的 "帐户" () 请输入您之前为 AAD 应用程序记录的 **租户 ID** 。 这将是与可以进行身份验证的用户关联的租户。

        - 如果您在 *任何 AAD 目录中选择了任何组织目录 (的帐户-多租户和个人 Microsoft 帐户（例如 Skype、Xbox、Outlook) * 输入 " **通用** 词" 而不是 "租户 ID"）。 否则，AAD 应用将通过已选择 ID 的租户进行验证，并排除个人 Microsoft 帐户。

    1. 对于 " **范围**"，请输入此应用程序需要的以空格分隔的图形权限列表，例如： User. User.readbasic.all。 read 

1. 选择“**保存**”。

### <a name="test-the-connection"></a>测试连接

1. 选择该连接条目以打开您刚创建的连接。
1. 在 "**服务提供程序连接" 设置**面板的顶部选择 "**测试连接**"。
1. 第一次执行此操作时，将打开一个新的浏览器窗口，要求您选择帐户。 选择要使用的一个。
1. 接下来，系统将要求您允许标识提供程序使用您的数据 (凭据) 。 下面的图像是一个示例：

    ![团队 bot 身份验证连接字符串 adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. 选择 " **接受**"。
1. 然后，这会将您重定向到 "成功" 页的 " **测试连接 \<your-connection-name> ** "。 如果遇到错误，请刷新页面。 下面的图像是一个示例：

  ![团队 bot 应用程序身份验证连接 str adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

Bot 代码使用连接名称来检索用户身份验证令牌。

## <a name="prepare-the-bot-sample-code"></a>准备机器人示例代码

完成初步设置后，我们将重点介绍如何创建要在本文中使用的 bot。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

1. 克隆： [cs-auth-示例][teams-auth-bot-cs]。
1. 启动 Visual Studio。
1. 在工具栏中，选择 " **文件-> 打开-> 项目/解决方案** "，然后打开 "bot" 项目。
1. 在 c # 中更新 **appsettings.js** ，如下所示：

    - 设置 `ConnectionName` 为你添加到 bot 通道注册的标识提供程序连接的名称。 本示例中使用的名称是 *BotTeamsAuthADv1*。
    - 设置 `MicrosoftAppId` 为在 bot 频道注册时保存的 **BOT 应用 ID** 。
    - 设置 `MicrosoftAppPassword` 为在 bot 频道注册时保存的 **客户机密** 。
    - 将设置 `ConnectionName` 为标识提供程序连接的名称。

    根据你的 bot 密码中的字符，你可能需要 XML 对密码进行转义。 例如，任何与 ( # A0) 的符号都需要编码为 `&amp;` 。

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. 在 "解决方案资源管理器" 中，导航到 " `TeamsAppManifest` 打开 `manifest.json` " 和 "设置" 文件夹， `id` 并转 `botId` 到在 bot 频道注册时保存的 **bot 应用 ID** 。

# <a name="javascript"></a>[JavaScript](#tab/node-js)

1. Clone [节点-auth-示例][teams-auth-bot-js]。
1. 在控制台中，导航到项目： </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. 安装模块</br></br>
`npm install`
1. 更新 **env** 配置，如下所示：

    - 设置 `MicrosoftAppId` 为在 bot 频道注册时保存的 **BOT 应用 ID** 。
    - 设置 `MicrosoftAppPassword` 为在 bot 频道注册时保存的 **客户机密** 。
    - 将设置 `connectionName` 为标识提供程序连接的名称。

    根据你的 bot 密码中的字符，你可能需要 XML 对密码进行转义。 例如，任何与 ( # A0) 的符号都需要编码为 `&amp;` 。

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. 在 `teamsAppManifest` 文件夹中，打开 `manifest.json` 并将 `id`  其设置为您的 **Microsoft 应用 id** ，并将 `botId` 其设置为在 bot 频道注册时保存的 **bot 应用 id** 。

# <a name="python"></a>[Python](#tab/python)

1. Clone 存储库中的 [py-auth-示例][teams-auth-bot-py] 。
1. 更新 **config.py**：

    - 设置 `ConnectionName` 为你添加到你的 bot 的 OAuth 连接设置的名称。
    - 将 `MicrosoftAppId` 和设置 `MicrosoftAppPassword` 为你的 bot 的应用 ID 和应用密码。

      根据你的 bot 密码中的字符，你可能需要 XML 对密码进行转义。 例如，任何与 ( # A0) 的符号都需要编码为 `&amp;` 。

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a>将机器人部署到 Azure

若要部署 bot，请按照 how to 将 [机器人部署到 Azure](https://aka.ms/azure-bot-deployment-cli)中的步骤操作。

或者，在 Visual Studio 中，可以按照以下步骤操作：

1. 在 Visual Studio " *解决方案资源管理器* " 中，选择并按住 (或右键单击) 项目名称。
1. 在下拉菜单中，选择 " **发布**"。
1. 在显示的窗口中，选择 " **新建** " 链接。
1. 在对话框窗口中，选择左侧的 " **App Service** "，在右侧 **创建 "新建** "。
1. 选择 " **发布** " 按钮。
1. 在下一个对话框窗口中，输入所需的信息。 示例如下：

   ![auth-应用程序-服务](../../../assets/images/authentication/auth-bot-app-service.png)

1. 选择“创建”****。
1. 如果部署成功完成，您应该会看到它在 Visual Studio 中反映出来。 此外，默认浏览器中会显示一个页面，指示 *你的 bot 已准备就绪！*。 该 URL 将类似于： `https://botteamsauth.azurewebsites.net/` 。 将其保存到文件中。
1. 在浏览器中，导航到 [**Azure 门户**][azure-portal]。
1. 检查您的资源组，应将 bot 与其他资源一起列出。 下面的图像是一个示例：

    ![团队-机器人-auth-应用程序-服务-组](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. 在 "资源" 组中，选择 "bot 频道注册名称" (链接) 。
1. 在左面板中，选择 " **设置**"。
1. 在 " **邮件终结点** " 框中，输入上面接下来的 URL `api/messages` 。 下面是一个示例： `https://botteamsauth.azurewebsites.net/api/messages` 。
1. 选择左上角的 " **保存** " 按钮。

## <a name="test-the-bot-using-the-emulator"></a>使用模拟器测试机器人

如果尚未执行此操作，请安装 [Microsoft Bot 框架模拟器](https://aka.ms/bot-framework-emulator-readme)。 另请参阅 [Debug with The 模拟器](https://aka.ms/bot-framework-emulator-debug-with-emulator)。

为了使 bot 示例登录正常工作，您必须配置仿真程序，如下所示。

### <a name="configure-the-emulator-for-authentication"></a>配置仿真程序以进行身份验证

如果 bot 需要身份验证，则必须配置仿真程序，如下所示。

1. 启动仿真程序。
1. 在仿真程序中，选择左下角 &#9881; 的齿轮图标，或右上角的 " **仿真程序设置** " 选项卡。
1. 通过 **使用版本1.0 身份验证令牌**选中此框。
1. 输入 **ngrok** 工具的本地路径。 *请参阅* Bot 框架仿真程序/ngrok 隧道集成 [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok))。 有关更多工具信息，请参阅 [ngrok](https://ngrok.com/)。
1. **在仿真程序启动时，通过运行 ngrok**选中该框。
1. 选择 " **保存** " 按钮。

当 bot 显示登录卡且用户选择登录按钮时，仿真程序将打开一个页面，用户可使用该页面使用身份验证提供程序进行登录。
一旦用户执行此操作，提供程序将生成用户令牌，并将其发送到 bot。 之后，bot 可以代表用户执行操作。

### <a name="test-the-bot-locally"></a>本地测试机器人

配置身份验证机制之后，可以执行实际的机器人测试。  

1. 通过 Visual Studio 在你的计算机上本地运行机器人示例（例如）。
1. 启动仿真程序。
1. 选择 " **打开 bot** " 按钮。
1. 在 **机器人 url**中，输入 bot 的本地 URL。 通常为 `http://localhost:3978/api/messages` 。
1. 在 **Microsoft 应用 id** 中，输入 bot 的应用 id `appsettings.json` 。
1. 在 **Microsoft App 密码** 中，输入 bot 的应用密码 `appsettings.json` 。
1. 选择 " **连接**"。
1. 在安装程序启动并运行后，输入任何文本以显示登录卡。
1. 选择 " **登录** " 按钮。
1. 将显示一个弹出对话框，以 **确认打开的 URL**。 这是为了让 bot 的用户 () 进行身份验证。  
1. 选择 " **确认**"。
1. 如果需要，请选择适用用户的帐户。
1. 根据您对仿真程序使用的配置，可以获取以下内容之一：
    1. **使用登录验证代码**  
      &#x2713; 打开显示验证代码的窗口。  
      &#x2713; 将验证代码复制并输入到聊天框中，以完成登录。
    1. **使用身份验证令牌**。  
      &#x2713; 您根据您的凭据登录。

    以下图像是登录后的 bot UI 的示例：

    ![auth bot 登录仿真程序](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. 如果你在 bot 询问*你是否要查看令牌*时选择 **"是"** ，则会收到类似于以下内容的响应：

    ![身份验证 bot 登录仿真程序令牌](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. 在 "输入聊天" 框中输入 **注销** 以注销。这将释放用户令牌，并且机器人将无法代表你进行操作，除非你再次登录。

> [!NOTE]
> Bot 身份验证需要使用 **Bot 连接器服务**。 服务访问你的 bot 的 bot 通道注册信息。

## <a name="test-the-deployed-bot"></a>测试部署的 bot

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. 在浏览器中，导航到 [**Azure 门户**][azure-portal]。
1. 查找您的资源组。
1. 选择 "资源" 链接。 将显示 "资源" 页。
1. 在 "资源" 页中，选择 " **在 Web 聊天中测试**"。 机器人将启动并显示预定义的问候语。
1. 在 "聊天" 框中键入任何内容。
1. 选择 " **登录** " 框。
1. 将显示一个弹出对话框，以 **确认打开的 URL**。 这是为了让 bot 的用户 () 进行身份验证。  
1. 选择 " **确认**"。
1. 如果需要，请选择适用用户的帐户。
    以下图像是登录后的 bot UI 的示例：

    ![已部署身份验证 bot 登录](../../../assets/images/authentication/auth-bot-login-deployed.PNG).

1. 选择 **"是"** 按钮以显示您的身份验证令牌。 下面的图像是一个示例：

    ![授权 bot 登录部署令牌](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG).

1. 输入注销以注销。

    ![已部署注销的身份验证机器人](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> 如果你在登录时遇到问题，请尝试再次测试连接，如前面步骤中所述。 这可能会重新创建身份验证令牌。
> 在 Azure 中使用 Bot 框架 Web 聊天客户端时，您可能需要在身份验证正确建立前多次进行登录。

## <a name="install-and-test-the-bot-in-teams"></a>在团队中安装和测试机器人

1. 在机器人项目中，确保 `TeamsAppManifest` 文件夹包含 `manifest.json` `outline.png` 和文件一起包含 `color.png` 。
1. 在 "解决方案资源管理器" 中，导航到该 `TeamsAppManifest` 文件夹。 `manifest.json`通过分配以下值进行编辑：
    1. 确保在将 bot 频道注册时收到的 **Bot 应用 ID** 分配给 `id` 和 `botId` 。
    1. 将此值分配给： `validDomains: [ "token.botframework.com" ]` 。
1. 选择和 **压缩** `manifest.json` 、 `outline.png` 和 `color.png` 文件。
1. 打开 **Microsoft 团队**。
1. 在左侧面板中的底部，选择 "应用" **图标**。
1. 在右侧面板的底部，选择 " **上传自定义应用程序**"。
1. 导航到该 `TeamsAppManifest` 文件夹并上传压缩清单。
将显示以下向导：

    ![授权 bot 团队上传](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. 选择 " **添加到团队** " 按钮。
1. 在下一个窗口中，选择要在其中使用 bot 的团队。
1. 选择 " **设置机器人** " 按钮。
1. 在左面板中选择 ( # A3) 的三个点。 然后，选择 " **App Studio** " 图标。
1. 选择 " **清单编辑器** " 选项卡。您应该会看到您上载的 bot 的图标。
1. 此外，您还应该能够在聊天列表中看到作为联系人列出的 bot，您可以使用它来与 bot 交换邮件。

### <a name="testing-the-bot-locally-in-teams"></a>在团队中本地测试机器人

Microsoft 团队是完全基于云的产品，它需要使用 HTTPS 终结点从云中获取所有 it 访问的服务。 因此，若要启用机器人 (我们的示例) 在团队中工作，您需要将代码发布到您选择的云，或使本地运行的实例可通过 **隧道** 工具进行外部访问。 我们建议  [ngrok](https://ngrok.com/download)，这将为您在您的计算机上本地打开的端口创建外部可寻址的 URL。
若要设置 ngrok 以准备在本地运行 Microsoft 团队应用程序，请按照以下步骤操作：

1. 在终端窗口中，转到已安装的目录 `ngrok.exe` 。 建议设置要指向的 *环境变量* 路径。
1. 例如，运行 `ngrok http 3978 --host-header=localhost:3978` 。 根据需要更换端口号。
这将启动 ngrok 以侦听您指定的端口。 在 return 中，它为您提供一个外部可寻址的 URL，只要 ngrok 正在运行，它就会有效。 下面的图像是一个示例：

    ![团队机器人应用程序身份验证连接字符串 adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG).

1. 复制转发 HTTPS 地址。 它应类似于以下内容： `https://dea822bf.ngrok.io/` 。
1. Append `/api/messages` 获取 `https://dea822bf.ngrok.io/api/messages` 。 这是在 Microsoft 团队的聊天中，在计算机上本地运行的 bot 的 **消息终结点** ，并可通过 web 访问。
1. 要执行的最后一个步骤是更新已部署的 bot 的消息终结点。 在此示例中，我们在 Azure 中部署了机器人。 因此，* * 我们将执行以下步骤：
    1. 在浏览器中导航到 [**Azure 门户**][azure-portal]。
    1. 选择你的 **Bot 频道注册**。
    1. 在左面板中，选择 " **设置**"。
    1. 在右侧面板中的 " **邮件终结点** " 框中，输入 ngrok URL （在我们的示例中） `https://dea822bf.ngrok.io/api/messages` 。
1. 在本地启动你的 bot，例如在 Visual Studio 调试模式下。
1. 使用 Bot 框架门户的 **测试 Web 聊天**在本地运行时测试机器人。 与模拟器一样，此测试不允许您访问特定于团队的功能。
1. 在运行的终端窗口中 `ngrok` ，可以查看 bot 和 web 聊天客户端之间的 HTTP 流量。 如果需要更详细的视图，请在浏览器窗口中输入 `http://127.0.0.1:4040` 从以前的终端窗口中获取的。 下面的图像是一个示例：

    ![auth bot 团队 ngrok 测试](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png).

> [!NOTE]
> 如果您停止并重新启动 ngrok，则 URL 会发生更改。 若要在项目中使用 ngrok，并根据所使用的功能，必须更新所有 URL 引用。
 

## <a name="additional-information"></a>其他信息

### <a name="teamsappmanifestmanifestjson"></a>上的 TeamsAppManifest/manifest.js

此清单包含 Microsoft 团队与 bot 连接所需的信息。  

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
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

通过身份验证，团队的行为与其他频道略有不同，如下所述。

### <a name="handling-invoke-activity"></a>处理调用活动

**调用活动**将发送到 bot，而不是其他通道使用的事件活动。
这是通过 **ActivityHandler**的 classing 完成的。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet-sample)

**Bot/DialogBot**

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

**Bot/TeamsBot**

如果使用了**OAuthPrompt** ，则必须将*调用活动*转发到对话框。

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

**bot/dialogBot.js**

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

**bot/teamsBot.js**

如果使用了**OAuthPrompt** ，则必须将*调用活动*转发到对话框。

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

**对话框/mainDialog.js**

在对话步骤中，使用 `beginDialog` "" 启动 OAuth 提示，这将要求用户登录。

- 如果用户已登录，则会生成令牌响应事件，而不会提示用户。
- 否则，这将提示用户登录。 Azure Bot 服务在用户尝试登录后发送令牌响应事件。

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

在下面的对话框步骤中，检查上一步的结果中是否存在令牌。 如果不为 null，则用户已成功登录。

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

**bot/logoutDialog.js**

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[Python](#tab/python-sample)

**bot/dialog_bot py**

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

**bot/teams_bot py**

如果使用了**OAuthPrompt** ，则必须将*调用活动*转发到对话框。

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

**对话框/main_dialog py**

在对话步骤中，使用 `begin_dialog` "" 启动 OAuth 提示，这将要求用户登录。

- 如果用户已登录，则会生成令牌响应事件，而不会提示用户。
- 否则，这将提示用户登录。 Azure Bot 服务在用户尝试登录后发送令牌响应事件。

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

在下面的对话框步骤中，检查上一步的结果中是否存在令牌。 如果不为 null，则用户已成功登录。

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

**对话框/logout_dialog py**

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

> [!div class="nextstepaction"]
> [了解如何通过 Azure Bot 服务添加身份验证](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: https://docs.microsoft.com/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0
[concept-state]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0
[concept-dialogs]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0
[simple-dialog]: https://docs.microsoft.com/azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0

[teams-auth-bot-cs]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[teams-auth-bot-js]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth

[azure-aad-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview
[aad-registration-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview
