---
title: 集成现有的第三方 API
author: MuyangAmigo
description: 本文介绍工具包如何帮助你启动对现有 API 的示例访问。 它提供不同身份验证类型的列表。
ms.author: zhany
ms.localizationpriority: medium
ms.topic: Overview
ms.date: 05/20/2022
ms.openlocfilehash: 5933227f9ba4c8b684d624a8857304c044761578
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616806"
---
# <a name="integrate-existing-third-party-apis"></a>集成现有的第三方 API

Teams 工具包可帮助你访问用于生成 Teams 应用程序的现有 API。 这些 API 由组织或第三方开发。 使用 Teams 工具包连接到现有 API 时，Teams 工具包将执行以下函数：

* 在或`./api`文件夹下`./bot`生成示例代码。
* 向其添加对包`package.json`的`@microsoft/teamsfx`引用。
* 在配置本地调试的 API 中  `.env.teamsfx.local` 添加应用程序设置。

## <a name="steps-to-connect-to-api"></a>连接到 API 的步骤

可以使用 Visual Studio Code 和 CLI 命令添加 API 连接。

### <a name="add-api-connection-using-visual-studio-code"></a>使用Visual Studio Code添加 API 连接

以下步骤可帮助你使用Visual Studio Code添加 API 连接：

1. 打开 Microsoft Visual Studio Code。
2. 从Visual Studio Code工具栏中选择 Teams 工具包 :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png" alt-text="api 图标":::。
3. 选择 **“开发**”下 **的“添加功能**”：

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-add-features.png" alt-text="api add features":::

    * 还可以打开命令面板并输入 **Teams：添加云资源**。

4. 在弹出窗口中，选择要添加到 Teams 应用项目的 **API 连接** ：

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

     :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/myAPI connection.png" alt-text="api 身份验证":::

     根据所选的身份验证类型，完成额外配置需要执行以下步骤

# <a name="basic"></a>[基本](#tab/basic)

* 输入基本身份验证的用户名。

  现在生成了示例代码，以便在bot\myAPI.js调用 API。

# <a name="certification"></a>[认证](#tab/certification)

   现在生成了示例代码，以便在bot\myAPI.js调用 API。

# <a name="azure-active-directory"></a>[Azure Active Directory](#tab/AAD)

  现在生成了示例代码，以便在bot\myAPI.js调用 API。

# <a name="api-key"></a>[API 密钥](#tab/apikey)

* 选择请求中所需的 API 密钥位置。

* 输入 API 密钥名称。

  现在生成了示例代码，以便在bot\myAPI.js调用 API。

# <a name="custom-auth-implementation"></a>[自定义身份验证实现](#tab/CustomAuthImplementation)

  现在生成了示例代码，以便在bot\myAPI.js调用 API。

---

## <a name="add-api-connection-using-cli"></a>使用 CLI 添加 API 连接

此功能的基本命令是 `teamsfx add api-connection [authentication type]`。 下表提供了不同身份验证类型的列表及其相应的示例命令：

 > [!TIP]
 > 可以使用 `teamsfx add api-connection [authentication type] -h` 它来获取帮助文档。

   |**身份验证类型**|**示例命令**|
   |-----------------------|------------------|
   |基本|teamsfx 添加 api-connection basic-endpoint <https://example.com> --component bot--alias example--user-name exampleuser--interactive false|
   |API 密钥|teamsfx 添加 api-connection apikey-endpoint <https://example.com> --component bot--alias example--key-location header--key-name example-key-name--interactive false|
   |Azure AD|teamsfx 添加 api-connection aad-endpoint <https://example.com> --component bot--alias example--app-type custom--tenant-id your_tenant_id--app-id your_app_id-interactive false|
   |证书|teamsfx add api-connection cert-endpoint <https://example.com> --component bot--alias example--interactive false|
   |自定义警报|teamsfx 添加 api-connection custom-endpoint <https://example.com> --component bot--alias example--interactive false|

---

## <a name="directory-structure-updates-to-your-project"></a>项目目录结构更新

 Teams 工具包根据所选内容修改 `bot` 或 `api` 修改文件夹：

1. 生成 `{your_api_alias}.js/ts` 文件。 该文件初始化 API 的 API 客户端并导出 API 客户端。

2. 将包添加 `@microsoft/teamsfx` 到 `package.json`. 该包提供对常见 API 身份验证方法的支持。

3. 将环境变量添加到 `.env.teamsfx.local`. 它们是所选身份验证类型的配置。 生成的代码从环境变量中读取值。

## <a name="advantages"></a>优点

如果没有适合语言的 SDK 来访问这些 API，Teams 工具包可帮助你启动示例代码来访问 API。

## <a name="see-also"></a>另请参阅

* [使用 Teams 工具包发布 Teams 应用](publish.md)
