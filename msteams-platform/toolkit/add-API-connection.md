---
title: 连接到现有 API
author: MuyangAmigo
description: 本文介绍工具包如何帮助你启动对现有 API 的示例访问。 它提供不同身份验证类型的列表。
ms.author: zhany
ms.localizationpriority: medium
ms.topic: Overview
ms.date: 05/20/2022
ms.openlocfilehash: dc987718233801a6855fd534d561fe2f3d964aa7
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143296"
---
# <a name="add-api-connection-to-teams-app"></a>将 API 连接添加到 Teams 应用

Teams Toolkit可帮助你访问用于生成Teams应用程序的现有 API。 这些 API 由组织或第三方开发。

## <a name="advantage"></a>优点

如果没有适合语言的 SDK 来访问这些 API，Teams Toolkit可帮助你启动示例代码来访问 API。

## <a name="connect-to-the-api"></a>连接到 API

使用Teams Toolkit连接到现有 API 时，Teams Toolkit执行以下函数：

* 在或`./api`文件夹下`./bot`生成示例代码。
* 向其添加对包`package.json`的`@microsoft/teamsfx`引用。
* 在配置本地调试的 API 中  `.env.teamsfx.local` 添加应用程序设置。

### <a name="connect-to-api-in-visual-studio-code"></a>在 Visual Studio Code 中连接到 API

* 可以在Visual Studio Code中使用Teams Toolkit添加 API 连接：

    1. 打开 Microsoft Visual Studio Code。
    2. 从左侧导航栏中选择Teams Toolkit :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png" alt-text="api 图标":::。
    3. 选择 **“开发**”下 **的“添加功能**”：

        :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-add-features.png" alt-text="api add features":::

       * 还可以打开命令面板并输入 **Teams：添加云资源**。

    4. 在弹出窗口中，选择要添加到Teams应用项目的 **API 连接**：

        :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-select-features.png" alt-text="api 选择功能":::

    5. 选择“**确定**”。

    6. 输入 API 的终结点。 它已添加到项目的本地应用程序设置，它是 API 请求的基本 URL。

         :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-endpoint.png" alt-text="api 终结点":::

         > [!NOTE]
         > 确保终结点是有效的 http () URL。

    7. 选择访问 API 的组件。

    8. 选择“**确定**”。

         :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-invoke.png" alt-text="api invoke":::

    9. 输入 API 的别名。 别名为添加到项目的本地应用程序设置的 API 生成应用程序设置名称。

         :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-alias.png" alt-text="api 别名":::

    10. 从 **API 身份验证类型中选择 API 请求所需的身份验证**。 它生成适当的示例代码，并根据所选内容添加相应的本地应用程序设置。

         :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-auth.png" alt-text="api 身份验证":::

         > [!NOTE]
         > 根据所选的身份验证类型，需要其他配置。

### <a name="api-connection-in-teamsfx-cli"></a>TeamsFx CLI 中的 API 连接

此功能的基本命令是 `teamsfx add api-connection [authentication type]`。 下表提供了不同身份验证类型的列表及其相应的示例命令：

 > [!Tip]
 > 可以使用 `teamsfx add api-connection [authentication type] -h` 它来获取帮助文档。

   |**身份验证类型**|**示例命令**|
   |-----------------------|------------------|
   |基本|teamsfx 添加 api-connection basic --endpoint <https://example.com> --component bot --alias example--user-name exampleuser --interactive false|
   |API 密钥|teamsfx 添加 api-connection apikey --endpoint <https://example.com> --component bot --alias example --key-location header --key-name example-key-name --interactive false|
   |Azure AD|teamsfx 添加 api-connection aad --endpoint <https://example.com> --component bot --alias example --app-type custom --tenant-id your_tenant_id --app-id your_app_id --interactive false|
   |证书|teamsfx add api-connection cert --endpoint <https://example.com> --component bot --alias example --interactive false|
   |自定义警报|teamsfx 添加 api-connection 自定义 --endpoint <https://example.com> --component bot --alias example --interactive false|

## <a name="understand-toolkit-updates-to-your-project"></a>了解项目Toolkit更新

 Teams Toolkit根据所选内容修改`bot`或`api`修改文件夹：

1. 生成 `{your_api_alias}.js/ts` 文件。 该文件初始化 API 的 API 客户端并导出 API 客户端。

2. 将包添加 `@microsoft/teamsfx` 到 `package.json`. 该包提供对常见 API 身份验证方法的支持。

3. 将环境变量添加到 `.env.teamsfx.local`. 它们是所选身份验证类型的配置。 生成的代码从环境变量中读取值。

## <a name="test-api-connection-in-local-environment"></a>在本地环境中测试 API 连接

以下步骤有助于在Teams Toolkit本地环境中测试 API 连接：

 1. **运行npm安装**

    在或`api`文件夹下`bot`运行`npm install`以安装添加的包。

 2. **将 API 凭据添加到本地应用程序设置**

    Teams Toolkit不请求凭据，但它会将占位符保留在本地应用程序设置文件中。 将占位符替换为用于访问 API 的相应凭据。 本地应用程序设置文件是`.env.teamsfx.local`文件夹中`bot``api`的文件。

 3. **使用 API 客户端发出 API 请求**

    从需要访问 API 的源代码导入 API 客户端：

    ```BASH
    import { yourApiClient } from '{relative path to the generated file}'
    ```

 4. **使用 Axios) 生成 http (针对 API (的) 请求**

    生成的 API 客户端是 Axios API 客户端。 使用 Axios 客户端向 API 发出请求。

     > [!Note]
     > [Axios](https://www.npmjs.com/package/axios) 是一个常用的 nodejs 包，可帮助你处理 http (的) 请求。 有关如何发出 http () 请求的详细信息，请参阅 [Axios 示例文档](https://axios-http.com/docs/example) ，了解如何使 http () 。

## <a name="deploy-your-application-to-azure"></a>将应用程序部署到 Azure

若要将应用程序部署到 Azure，需要将身份验证添加到相应环境的应用程序设置。 例如，API 可能具有不同的凭据和凭据`dev``prod`。 根据环境需求配置Teams Toolkit。

Teams Toolkit配置本地环境。 启动的示例代码包含注释，告知需要配置哪些应用设置。 有关应用程序设置的详细信息，请参阅 [“添加应用设置](https://github.com/OfficeDev/TeamsFx/wiki/%5BDocument%5D-Add-app-settings)”。

## <a name="advanced-scenarios"></a>高级方案

  以下部分介绍高级方案：

<br>

<details>
<summary><b>自定义身份验证提供程序</b></summary>

除了包中`@microsoft/teamsfx`包含的身份验证提供程序外，还可以实现实现接口并将其用于函数`createApiClient(..)`的`AuthProvider`自定义身份验证提供程序：

```Bash
import { AuthProvider } from '@microsoft/teamsfx'

class CustomAuthProvider implements AuthProvider {
    constructor() {
        // You can add necessary parameters for your customized logic in constructor
    }

    AddAuthenticationInfo: (config: AxiosRequestConfig) => Promise<AxiosRequestConfig> = async (
        config
    ) => {
        /*
        * The config parameter contains all the request information and can be updated to include extra authentication info.
        * Refer https://axios-http.com/docs/req_config for detailed document for the config object.
        * 
        * Add your customized logic that returns updated config
        */
    };
}
```

</details>
<details>
<summary><b>连接 Azure AD 权限的 API</b></summary>
Azure AD 对某些服务进行身份验证。 以下列表有助于访问这些服务以配置 API 权限。

* [使用访问控制列表 (ACL) ](#access-control-lists-acls)
* [使用 Azure AD 应用程序权限](#azure-ad-application-permissions)

获取具有适当 API 资源范围的令牌取决于 API 的实现。

使用以下操作时，可以按照以下步骤访问这些 API：

#### <a name="access-control-lists-acls"></a>访问控制列表 (ACL) 

   1. "开始"菜单项目的云环境中的本地调试。 它会创建一个 Azure AD 应用程序注册Teams应用程序。
  
   2. 打开`.fx/states/state.{env}.json`并记下属性的`clientId``fx-resource-aad-app-for-teams`值。

   3. 向 API 提供程序提供客户端 ID，以便在 API 服务上配置 ACL。

#### <a name="azure-ad-application-permissions"></a>Azure AD 应用程序权限

  1. 打开 `templates/appPackage/aad.template.json` 以下内容并将其添加到 `requiredResourceAccess` 属性：

```JSON
 {
     "resourceAppId": "The AAD App Id for the service providing the API you are connecting to",
     "resourceAccess": [
         {
             "id": "Target API's application permission Id",
             "type": "Role"
         }
     ]
 }
```

   2. "开始"菜单项目的云环境中的本地调试。 它会创建一个 Azure AD 应用程序注册Teams应用程序。

   3. 打开`.fx/states/state.{env}.json`并记下属性的`clientId``fx-resource-aad-app-for-teams`值。 这是应用程序客户端 ID。

   4. 为所需的应用程序权限授予管理员许可，有关详细信息，请参阅 [授予管理员许可](/azure/active-directory/manage-apps/grant-admin-consent#grant-admin-consent-in-app-registrations)。

        > [!NOTE]
        > 对于应用程序权限，请使用客户端 ID。
        >
</details>

## <a name="see-also"></a>另请参阅

* [使用 Teams 工具包发布 Teams 应用](publish.md)
