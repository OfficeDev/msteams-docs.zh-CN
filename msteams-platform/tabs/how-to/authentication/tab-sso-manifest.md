---
title: 用于为选项卡启用 SSO 的更新清单
description: 介绍为选项卡启用 SSO 的更新清单
ms.topic: how-to
ms.localizationpriority: medium
keywords: Azure AD) 图形 API Microsoft Azure Active Directory (团队身份验证选项卡
ms.openlocfilehash: 437c16763e918430e91fe543c2dbc62d95452c5c
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503478"
---
# <a name="update-manifest-for-sso-and-preview-app"></a>更新 SSO 和预览版应用的清单

在更新 Teams 应用清单之前，请确保已将代码配置为在选项卡应用中启用 SSO。

> [!div class="nextstepaction"]
> [配置代码](tab-sso-code.md)

你已在 Azure AD 中注册了 Tab 应用，并获得了应用 ID。 你还配置了代码以调用 `getAuthToken()` 和处理访问令牌。 现在，必须更新 Teams 应用清单才能为选项卡应用启用 SSO。 Teams 应用清单介绍应用如何集成到 Teams 中。

## <a name="webapplicationinfo-property"></a>webApplicationInfo 属性

在 Teams 应用清单文件中配置 `webApplicationInfo` 属性。 此属性使应用的 SSO 能够帮助应用用户无缝访问选项卡应用。

&nbsp;&nbsp;:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-manifest.png" alt-text="Teams 应用清单配置" border="false":::

`webApplicationInfo` 有两个元素， `id` 和 `resource`.

| 元素 | 说明 |
| --- | --- |
| id | 输入在 Azure AD 中创建 (GUID) 的应用 ID。 |
| resource | 在创建范围时输入应用的子域 URI 和在 Azure AD 中创建的应用程序 ID URI。 可以从 **Azure AD** > **“公开 API”** 部分复制它。 |

> [!NOTE]
> 使用清单版本 1.5 或更高版本来实现该 `webApplicationInfo` 属性。

在 Azure AD 中注册的应用程序 ID URI 配置为公开的 API 范围。 配置应用的子域 URI `resource` ，确保使用 `getAuthToken()` 的身份验证请求来自 Teams 应用清单中提供的域。

有关详细信息，请参阅 [webApplicationInfo](../../../resources/schema/manifest-schema.md#webapplicationinfo)。

## <a name="to-configure-teams-app-manifest"></a>配置 Teams 应用清单

1. 打开选项卡应用项目。
2. 打开清单文件夹。

  > [!NOTE]
  >
  > - 清单文件夹应位于项目的根目录。 有关详细信息，请参阅 [“创建 Microsoft Teams 应用包](../../../concepts/build-and-test/apps-package.md)”。
  > - 有关如何创建 manifest.json 的详细信息，请 [参阅参考：Microsoft Teams 的清单架构](../../../resources/schema/manifest-schema.md)。

1. 打开 manifest.json 文件
1. 将以下代码片段追加到清单文件以添加新属性：

    ```json
    "webApplicationInfo": {
    "id": "{Azure AD AppId}",
    "resource": "api://{Subdomain}.example.com/{Azure AD AppId}"
    }
    ```

    where，
    - {Azure AD AppId} 是在 Azure AD 中注册应用时创建的应用 ID。 是 GUID
    - {{Subdomain}.app ID URI} 是在 Azure AD 中创建范围时注册的应用程序 ID URI。

4. 更新 **ID** 属性中 Azure AD 中的应用 ID。
5. 更新以下属性中的子域 URL：
   1. `contentUrl`
   2. `configurationUrl`
   3. `validDomains`
6. 保存 Teams 应用清单文件。

<br>
<details>
<summary>下面是更新后应用清单的示例</summary>

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
> 在调试期间，可以使用 ngrok 在 Azure AD 中测试应用。 在这种情况下，需要将子域 `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` 替换为 ngrok url。 每当 ngrok 子域发生更改时，都需要更新 URL。例如，api://23c3-103-50-148-128.ngrok.io/bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c。

## <a name="sideload-and-preview-in-teams"></a>Teams 中的旁加载和预览版

你已将 Tab 应用配置为在 Azure AD、应用代码和 Teams 清单文件中启用 SSO。 现在可以在 Teams 中旁加载选项卡应用，并在 Teams 环境中预览它。

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-flow.png" alt-text="SSO 应用" border="false":::

若要在 Teams 中预览选项卡应用，请执行以下操作：

1. 创建应用包。

   应用包是包含应用清单文件和应用图标的 zip 文件。

1. 打开 Teams。

1. 选择 **“应用** > **管理应用** > **上传应用**”。

    将显示用于上传应用的选项。

1. 选择 **“上传自定义应用** ”以将选项卡应用旁加载到 Teams。

1. 选择应用包 zip 文件，然后选择 **“添加**”。

    选项卡应用已旁加载，对话框将显示为通知你可能需要的其他权限。

1. 选择 **继续**。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/teams-sso-consent.png" alt-text="“Teams”对话框，告知需要其他权限" border="true":::

    将显示 Azure AD 许可对话框。

1. 选择 **“接受** ”以同意开放 ID 范围。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/aad-sso-consent.png" alt-text="Azure AD 许可对话框" border="true":::

    Teams 会打开选项卡应用，你可以使用它。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/teams-sso-app.png" alt-text="启用了 SSO 的 Teams 选项卡应用示例" border="false":::

    恭喜！ 你已为选项卡应用启用了 SSO。

## <a name="see-also"></a>另请参阅

- [Microsoft Teams 的清单架构](../../../resources/schema/manifest-schema.md)
- [清单架构格式](https://developer.microsoft.com/json-schemas/teams/v1.12/MicrosoftTeams.schema.json)
- [创建 Microsoft Teams 应用包](../../../concepts/build-and-test/apps-package.md)
