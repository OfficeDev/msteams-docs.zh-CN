---
title: 使用 Azure AD 注册选项卡应用
description: 通过配置应用 ID URI、访问令牌范围和预授权受信任客户端，配置 Azure AD 的单一登录 (SSO) 。
ms.topic: how-to
ms.localizationpriority: high
keywords: Microsoft Azure Active Directory (Azure AD) 访问令牌 SSO 租户范围的 Teams 身份验证选项卡
ms.openlocfilehash: 1387b1f426e433ea98bc950c932f271785fa5dd4
ms.sourcegitcommit: 82c585d287d61924ce3a3bba3e9caeff35c9a27a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2022
ms.locfileid: "67586796"
---
# <a name="register-your-tab-app-in-azure-ad"></a>在 Azure AD 中注册选项卡应用

Azure AD 基于应用用户的 Teams 标识提供对选项卡应用的访问权限。 需要将选项卡应用注册到 Azure AD，以便可以向已登录 Teams 的应用用户授予对选项卡应用的访问权限。

## <a name="enabling-sso-on-azure-ad"></a>在 Azure AD 上启用 SSO

在 Azure AD 中注册选项卡应用并将其启用为 SSO 需要进行应用配置，例如生成应用 ID、定义 API 范围，以及预授权受信任应用程序的客户端 ID。

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/register-azure-ad.png" alt-text="配置 Azure AD 以将访问令牌发送到 Teams 客户端应用":::

在 Azure AD 中创建新的应用注册，并使用范围（权限）公开其 (Web) API。 在 Azure AD 上公开的 API 与应用之间配置信任关系。 这允许 Teams 客户端代表应用程序和登录用户获取访问令牌。 可以为要预先授权的受信任的移动、桌面和 Web 应用程序添加客户端 ID。

可能还需要配置其他详细信息，例如，在想要定位选项卡应用的平台或设备上对应用用户进行身份验证。

仅支持用户级图形 API 权限，即电子邮件、配置文件、offline_access、OpenId。 如果需要访问其他 Microsoft Graph 作用域，如 `User.Read` 或 `Mail.Read`，请参阅[获取具有 Graph 权限的访问令牌](tab-sso-graph-api.md)。

Azure AD 配置为 Teams 中的选项卡应用启用 SSO。 它使用访问令牌进行响应，以验证应用用户。

> [!NOTE]
> Microsoft Teams 工具包在 SSO 项目中注册 Azure AD 应用程序。

### <a name="before-you-register-with-azure-ad"></a>在向 Azure AD 注册之前

如果事先了解在 Azure AD 上注册应用的配置，这很有帮助。 在注册应用之前，请确保已准备好配置以下详细信息：

- **单租户或多租户选项**：应用程序将仅在注册它的 Microsoft 365 租户中使用，还是许多 Microsoft 365 租户使用它？ 为一家企业编写的应用程序通常是单租户；由独立软件供应商编写且由许多客户使用的应用程序需要是多租户，以便每个客户的租户都可以访问该应用程序。
- **应用程序 ID URI**：它是一个全局唯一的 URI，用于标识通过范围访问应用时公开的 Web API。 它也称为标识符 URI。 应用程序 ID URI 包括应用 ID 和托管应用的子域。 应用程序的域名和为 Azure AD 应用程序注册的域名应相同。 目前不支持每个应用有多个域。
- **范围**：可以授予授权应用用户或应用访问 API 公开资源的权限。

> [!NOTE]
>
> - **LOB 应用程序**：组织可以通过 Microsoft Store 提供 LOB 应用程序。 这些应用是组织的自定义应用。 它们属于内部或特定的组织或企业。
> - **客户拥有的应用**：Azure AD B2C 租户中的客户拥有的应用也支持 SSO。

若要在 Azure AD 中创建和配置应用以启用 SSO，请执行以下操作：

- [注册和配置 Azure AD 应用。](#create-an-app-registration-in-azure-ad)
- [配置访问令牌的范围。](#configure-scope-for-access-token)
- [配置访问令牌版本。](#configure-access-token-version)

## <a name="create-an-app-registration-in-azure-ad"></a>创建 Azure AD 应用注册

在 Azure AD 中注册新应用，并配置租户和应用的平台。 你将生成一个新的应用 ID，稍后将在 Teams 应用清单文件中更新。

### <a name="to-register-a-new-app-in-azure-ad"></a>在 Azure AD 中注册新应用

1. 在 Web 浏览器上打开 [Azure 门户](https://ms.portal.azure.com/)。
   Microsoft Azure AD 门户页随即打开。

2. 选择 **应用注册** 图标。

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-portal.png" alt-text="Azure AD 门户页。":::

   将显示 **应用注册** 页。

3. 选择 **+ 新建注册** 图标。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-registrations.png" alt-text="Azure AD 门户上的新注册页。":::

    将显示 **注册应用程序** 页。

4. 输入要显示给应用用户的应用名称。 如果需要，可以在以后的阶段更改此名称。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/register-app.png" alt-text="Azure AD 门户上的应用注册页。":::

5. 选择可以访问应用的用户帐户的类型。 可以从单租户或多租户选项或专用 Microsoft 帐户中进行选择。

    <details>
    <summary><b>支持的帐户类型的选项</b></summary>

    | 选项 | 选择此选项可... |
    | --- | --- |
    | 仅限此组织目录中的帐户（仅限 Microsoft - 单租户） | 生成仅供租户中（或来宾）用户使用的应用程序。 <br> 此应用通常称为 LOB 应用程序，是Microsoft 标识平台中的单租户应用程序。 |
    | 任何组织目录（任何 Azure AD 目录 - 多租户）中的帐户 | 允许任何 Azure AD 租户中的用户使用应用程序。 例如，如果要生成 SaaS 应用程序，并且打算将其提供给多个组织，则此选项非常合适。 <br> 此类应用在 Microsoft 标识平台中称为多租户应用程序。|
    | 任何组织目录中的帐户（任何 Azure AD 目录 - 多租户）和个人 Microsoft 帐户 | 面向最广泛的客户集。 <br> 通过选择此选项，你将注册一个可支持具有个人 Microsoft 帐户的应用用户的多租户应用程序。 |
    | 仅限个人 Microsoft 帐户 | 仅为拥有个人 Microsoft 帐户的用户生成应用程序。 |

    </details>

    > [!NOTE]
    > 无需输入 **重定向 URI** 即可为选项卡应用启用 SSO。

7. 选择“**注册**”。
    浏览器上弹出一条消息，指出应用已创建。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-created-msg.png" alt-text="在 Azure AD 门户上注册应用。":::

    将显示具有应用 ID 和其他配置的页面。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/tab-app-created.png" alt-text="应用注册成功。":::

8. 记下并保存 **应用程序（客户端）ID** 中的应用 ID。 稍后需要使用它来更新 Teams 应用清单。

    应用已在 Azure AD 中注册。 现在应为选项卡应用提供应用 ID。

## <a name="configure-scope-for-access-token"></a>配置访问令牌的范围

创建新的应用注册后，配置范围（权限）选项，以便将访问令牌发送到 Teams 客户端，并授权受信任的客户端应用程序启用 SSO。

若要配置范围并授权受信任的客户端应用程序，需要：

- [若要公开 API](#to-expose-an-api)：为应用配置范围（权限）选项。 你将公开 Web API，并配置应用程序 ID URI。
- [若要配置 API 范围](#to-configure-api-scope)：定义 API 的范围，以及可以同意某个范围的用户。 只能让管理员为特权较高的权限提供许可。
- [若要配置授权的客户端应用程序](#to-configure-authorized-client-application)：为要预先授权的应用程序创建授权的客户端 ID。 它允许应用用户访问你配置的应用范围（权限），而无需任何进一步的同意。 仅预先授权你信任的客户端应用程序，因为应用用户将无法拒绝同意。

### <a name="to-expose-an-api"></a>公开 API

1. 从左窗格中选择“**管理** > **公开 API**”。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/expose-api-menu.png" alt-text="公开 API 菜单选项。":::

    随即显示“**公开 API**”页。

1. 选择“**设置**”以生成应用 ID URI，格式为 `api://{AppID}`。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/expose-an-api.png" alt-text="设置应用 ID URI":::

    将显示用于设置应用程序 ID URI 的部分。

1. 以此处所述的格式输入应用程序 ID URI。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/set-app-id-uri.png" alt-text="应用程序 ID URI。":::

    - **应用程序 ID URI** 以格式 `api://{AppID}` 预填充应用 ID (GUID)。
    - 应用程序 ID URI 格式应为：`api://fully-qualified-domain-name.com/{AppID}`。
    - 在 `api://` 和 `{AppID}` 之间出入 `fully-qualified-domain-name.com`（即 GUID）。 例如，api://example.com/{AppID}。

    其中
    - `fully-qualified-domain-name.com` 是提供选项卡应用的人类可读域名。 应用程序的域名和为 Azure AD 应用程序注册的域名应相同。

      如果使用的是隧道服务（如 ngrok），则必须在 ngrok 子域发生更改时更新此值。
    - `AppID` 是注册应用时生成的 (GUID) 的应用 ID。 可以在“**概述**”部分中进行查看。

    > [!IMPORTANT]
    >
    > - **具有多种功能应用的应用程序 ID URI**：如果要生成具有机器人、消息传递扩展和选项卡的应用，请输入应用程序 ID URI 作为 `api://fully-qualified-domain-name.com/BotId-{YourClientId}`，其中 BotID 是机器人应用 ID。
    >
    > - **域名的格式**：对域名使用小写字母。 请勿使用大写。
    >
    >   例如，若要创建资源名称为“demoapplication”的应用服务或 Web 应用：
    >
    >   | 如果使用了基本资源名称 | URL 将为... | 支持格式... |
    >   | --- | --- | --- |
    >   | *demoapplication* | **<https://demoapplication.example.net>** | 所有平台|
    >   | *DemoApplication* | **<https://DemoApplication.example.net>** | 仅限桌面、Web 和 iOS。 Android 不支持此功能。 |
    >
    >    使用小写选项 *demoapplication* 作为基本资源名称。

1. 选择“保存”。

    浏览器上弹出一条消息，指出应用程序 ID URI 已更新。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-id-uri-msg.png" alt-text="应用程序 ID URI 消息":::

    应用程序 ID URI 显示在页面上。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-id-uri-added.png" alt-text="应用程序 ID URI 已更新":::

1. 记下并保存应用程序 ID URI。 稍后需要使用它来更新 Teams 应用清单。

### <a name="to-configure-api-scope"></a>配置 API 范围

1. 在此 API 部分定义的“**作用域**”中选择“**+ 添加作用域**”。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/select-scope.png" alt-text="选择作用域":::

    将显示 **“添加范围** ”页。

1. 输入配置范围的详细信息。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-scope.png" alt-text="添加范围详细信息":::

    1. 输入范围名称。 这是必填字段。
    2. 选择可以对此范围表示同意的用户。 默认选项为 **仅限管理员**。
    3. 输入 **管理员同意显示名称**。 这是必填字段。
    4. 输入管理员同意的说明。 这是必填字段。
    5. 输入 **用户同意显示名称**。
    6. 输入用户同意说明。
    7. 为状态选择“**启用**”选项。
    8. 选择“**添加作用域**”。

    浏览器上弹出一条消息，指出已添加范围。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/scope-added-msg.png" alt-text="范围添加的消息":::

    定义的新范围显示在页面上。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/scope-added.png" alt-text="添加和显示的范围":::

### <a name="to-configure-authorized-client-application"></a>配置已授权的客户端应用程序

1. 将“**公开 API** ”页移动到“**授权客户端应用程序**”部分，然后选择“**+ 添加客户端应用程序**”。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/auth-client-apps.png" alt-text="授权的客户端应用程序":::

    将显示“**添加客户端应用程序**”页。

1. 输入要为应用的 Web 应用程序授权的应用程序的 Teams 客户端的相应客户端 ID。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-client-app.png" alt-text="添加客户端应用程序":::。

    > [!NOTE]
    >
    > - Teams 移动、桌面和 Web 应用程序的客户端 ID 是应添加的实际 ID。
    > - 对于 Teams 选项卡应用，需要 Web 或 SPA，因为无法在 Teams 中拥有移动或桌面客户端应用程序。

    1. 选择以下客户端 ID 之一：

       | 使用客户端 ID | 用于授权... |
       | --- | --- |
       | 1fec8e78-bce4-4aaf-ab1b-5451cc387264 | Teams 移动或桌面应用程序 |
       | 5e3ce6c0-2b1f-4285-8d4b-75ee78787346 | Teams Web 应用程序 |

    1. 选择在 **授权范围内** 为应用创建的应用程序 ID URI，将范围添加到公开的 Web API。

    1. 选择“添加应用程序”。

    浏览器上弹出一条消息，指出已添加授权的客户端应用。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/update-app-auth-msg.png" alt-text="客户端应用程序添加了消息":::

    客户端 ID 显示在页面上。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/client-app-added.png" alt-text="添加并显示的客户端应用":::

> [!NOTE]
> 可以授权多个客户端应用程序。 重复此过程的步骤以配置另一个已授权的客户端应用程序。

## <a name="configure-access-token-version"></a>配置访问令牌版本

必须定义应用可接受的访问令牌版本。 此配置是在 Azure AD 应用程序清单中进行的。

### <a name="to-define-the-access-token-version"></a>定义访问令牌版本

1. 从左窗格中选择“**管理** > **清单** ”。

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-portal-manifest.png" alt-text="Azure AD 门户清单":::

    将显示 Azure AD 应用程序清单。

1. 输入 **2** 作为 `accessTokenAcceptedVersion` 属性的值。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-manifest-value.png" alt-text="接受的访问令牌版本的值":::

1. 选择“**保存**”

    浏览器上弹出一条消息，指出清单已成功更新。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/update-aad-manifest-msg.png" alt-text="清单更新的消息":::

恭喜！ 你已完成在 Azure AD 中为选项卡应用启用 SSO 所需的应用配置。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [添加代码以启用 SSO](tab-sso-code.md)

## <a name="see-also"></a>另请参阅

- [Azure Active Directory 中的租户](/azure/active-directory/develop/single-and-multi-tenant-apps)
- [使用 Microsoft Graph 权限和范围扩展选项卡应用](tab-sso-graph-api.md)
- [快速入门 - 向 Microsoft 标识平台注册应用程序](/azure/active-directory/develop/quickstart-register-app)
- [快速入门：配置应用程序以公开 Web API](/azure/active-directory/develop/quickstart-configure-app-expose-web-apis)
- [OAuth 2.0 授权代码授予流](/azure/active-directory/develop/v2-oauth2-auth-code-flow)
