---
title: 为选项卡启用 SSO 的更新清单
description: 更新 Teams 清单，用于为选项卡启用单一登录 (SSO) ，并将其旁加载到 Teams 客户端以测试 SSO 身份验证。
ms.topic: how-to
ms.localizationpriority: high
keywords: Teams 身份验证选项卡 Microsoft Azure Active Directory (Azure AD) Graph API
ms.openlocfilehash: 1af4120914343b7fb2b37e6c2458ac43fcaa9d47
ms.sourcegitcommit: 82c585d287d61924ce3a3bba3e9caeff35c9a27a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2022
ms.locfileid: "67586999"
---
# <a name="update-manifest-for-sso-and-preview-app"></a>更新 SSO 清单并预览应用

在更新 Teams 应用清单之前，请确保已将代码配置为在选项卡应用中启用 SSO。

> [!div class="nextstepaction"]
> [配置代码](tab-sso-code.md)

你已在 Azure AD 中注册了选项卡应用，并已获得应用 ID。 你还配置了代码以调用 `getAuthToken()` 和处理访问令牌。 现在，必须更新 Teams 应用清单才能为选项卡应用启用 SSO。 Teams 应用清单介绍了应用如何集成到 Teams 中。

## <a name="webapplicationinfo-property"></a>webApplicationInfo 属性

在 Teams 应用清单文件中配置 `webApplicationInfo` 属性。 此属性为应用启用 SSO，以帮助应用用户无缝访问选项卡应用。

&nbsp;&nbsp;:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-manifest.png" alt-text="Teams 应用清单配置":::

`webApplicationInfo` 有两个元素，`id` 和 `resource`。

| 元素 | 说明 |
| --- | --- |
| id | 输入在 Azure AD 中创建的应用 ID (GUID)。 |
| resource | 创建范围时输入应用的子域 URI 和在 Azure AD 中创建的应用程序 ID URI。 可以从“**Azure AD**” > “**公开 API**”部分复制它。 |

> [!NOTE]
> 使用清单版本 1.5 或更高版本以实现 `webApplicationInfo` 属性。

在 Azure AD 中注册的应用程序 ID URI 已配置为公开的 API 范围。 在 `resource` 中配置应用的子域 URI，以确保使用 `getAuthToken()` 的身份验证请求来自 Teams 应用清单中给定的域。

有关详细信息，请参阅 [webApplicationInfo](../../../resources/schema/manifest-schema.md#webapplicationinfo)。

## <a name="to-configure-teams-app-manifest"></a>若要配置 Teams 应用清单

1. 请打开选项卡应用项目。
2. 请打开清单文件夹。

  > [!NOTE]
  >
  > - 清单文件夹应位于项目的根目录。 有关详细信息，请参阅 [创建 Microsoft Teams 应用包](../../../concepts/build-and-test/apps-package.md)。
  > - 有关了解如何创建 manifest.json 的详细信息，请参阅 [参考：Microsoft Teams 的清单架构](../../../resources/schema/manifest-schema.md)。

1. 打开 manifest.json 文件
1. 将以下代码片段附加到清单文件以添加新属性：

    ```json
    "webApplicationInfo": {
    "id": "{Azure AD AppId}",
    "resource": "api://{Subdomain}.example.com/{Azure AD AppId}"
    }
    ```

    其中，
    - {Azure AD AppId} 是在 Azure AD 中注册应用时创建的应用 ID。 这是 GUID。
    - {{Subdomain}.app ID URI} 是在 Azure AD 中创建搜索范围时注册的应用程序 ID URI。

4. 在 **ID** 属性中从 Azure AD 更新应用 ID。
5. 更新以下属性中的子域 URL：
   1. `contentUrl`
   2. `configurationUrl`
   3. `validDomains`
6. 保存 Teams 应用清单文件。

<br>
<details>
<summary>以下是更新后的应用清单示例</summary>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
  "manifestVersion": "1.11",
  "version": "1.0.0",
  "id": "bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c",
  "packageName": "com.contoso.teamsauthsso",
  "developer": {
    "name": "Microsoft",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.microsoft.com/privacy",
    "termsOfUseUrl": "https://www.microsoft.com/termsofuse"
  },
  "name": {
    "short": "Teams Auth SSO",
    "full": "Teams Auth SSO"
  },
  "description": {
    "short": "Teams Auth SSO app",
    "full": "The Teams Auth SSO app"
  },
  "icons": {
    "outline": "outline.png",
    "color": "color.png"
  },
  "accentColor": "#60A18E",
  "staticTabs": [
    {
      "entityId": "auth",
      "name": "Auth",
      "contentUrl": "https://contoso.com/Home/Index",
      "scopes": [ "personal" ]
    }
  ],
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/Home/Configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "team"
      ]
    }
  ],
  "permissions": [ "identity", "messageTeamMembers" ],
  "validDomains": [
    "contoso.com"
  ],
  "webApplicationInfo": {
    "id": "bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c",
    "resource": "api://contoso.com/bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c"
  }
}
```

</details>

> [!NOTE]
> 在调试期间，可以使用 ngrok 在 Azure AD 中测试应用。 在这种情况下，需要将 `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` 中的子域替换为 ngrok URL。 每当 ngrok 子域发生更改时，都需要更新 URL。例如，api://23c3-103-50-148-128.ngrok.io/bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c。

## <a name="sideload-and-preview-in-teams"></a>Teams 中的旁加载和预览

你已将选项卡应用配置为在 Azure AD、应用代码和 Teams 清单文件中启用 SSO。 现在可以在 Teams 中旁加载选项卡应用，并在 Teams 环境中预览它。

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-flow.png" alt-text="SSO 应用":::

若要在 Teams 中预览选项卡应用，请执行以下操作：

1. 创建应用包。

   应用包是包含应用清单文件和应用图标的 zip 文件。

1. 打开 Teams。

1. 选择“**应用**” > “**管理应用**” > “**上传应用**”。

    将出现用于上传应用的选项。

1. 选择“**上传自定义应用**”以将选项卡应用旁加载到 Teams。

1. 选择应用包 zip 文件，然后选择“**添加**”。

    选项卡应用已旁加载，此时会出现对话框，通知你可能需要其他权限。

1. 选择 **继续**。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/teams-sso-consent.png" alt-text="“Teams”对话框通知所需的其他权限":::

    将出现 Azure AD 许可对话框。

1. 选择“**接受**”以同意 Open-ID 范围。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/aad-sso-consent.png" alt-text="Azure AD 许可对话框":::

    Teams 将打开选项卡应用，你可以使用它。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/teams-sso-app.png" alt-text="已启用 SSO 的 Teams 选项卡应用示例":::

    恭喜！ 你已为选项卡应用启用 SSO。

## <a name="see-also"></a>另请参阅

- [Microsoft Teams 的清单架构](../../../resources/schema/manifest-schema.md)
- [清单架构格式](https://developer.microsoft.com/json-schemas/teams/v1.12/MicrosoftTeams.schema.json)
- [创建 Microsoft Teams 应用包](../../../concepts/build-and-test/apps-package.md)
