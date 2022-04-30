---
title: TeamsFx SDK
author: MuyangAmigo
description: 关于 TeamsFx SDK
ms.author: nintan
ms.localizationpriority: high
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: d54c3d962ecc9d1fd703bd4126d71564f8358794
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111218"
---
# <a name="teamsfx-sdk"></a>TeamsFx SDK

TeamsFx 利用 Teams SSO 并将云资源向下访问到零配置的单行语句，从而帮助减少开发人员任务。 TeamsFx SDK 旨在用于浏览器和 Node.js 环境，常见场景包括:

* Teams 选项卡应用程序
* Azure Function
* Teams 机器人

可以使用 TeamsFx SDK 执行以下操作:

* 访问客户端和服务器环境中的核心功能 
* 以简化的方式编写用户身份验证代码

## <a name="prerequisites"></a>先决条件

安装以下工具并设置开发环境:

* Node.js 最新版本
* 如果项目已将 `botbuilder` 相关的 [包](https://github.com/Microsoft/botbuilder-js#packages) 安装为依赖项，请确保它们的版本相同。 目前，所需版本为 4.15.0 或更高版本，有关详细信息，请参阅 [机器人生成器包应为同一版本](https://github.com/BotBuilderCommunity/botbuilder-community-js/issues/57#issuecomment-508538548)。

必须具备以下工作知识:

* [源代码](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk)
* [包(NPM)](https://www.npmjs.com/package/@microsoft/teamsfx)
* [API 参考文档](https://aka.ms/teamsfx-sdk-help)
* [示例](https://github.com/OfficeDev/TeamsFx-Samples)

## <a name="get-started"></a>入门

使用 TeamsFx 工具包或 CLI 在基架项目中预配置 TeamsFx SDK。
有关详细信息，请参阅 [Teams 应用项目](https://github.com/OfficeDev/TeamsFx/blob/main/packages/vscode-extension/README.md)。

### <a name="install-the-microsoftteamsfx-package"></a>安装 `@microsoft/teamsfx` 包

使用 `npm` 安装适用于 TypeScript 或 JavaScript 的 TeamsFx SDK:

```bash
npm install @microsoft/teamsfx
```

### <a name="create-microsoftgraphclient-service"></a>创建 `MicrosoftGraphClient` 服务

要创建图形客户端对象并访问 Microsoft Graph API，需要凭据才可进行身份验证。 SDK 提供 API 以为开发人员进行配置。

<br>

<details>
<summary><b>代表 Teams 用户(用户标识)调用 Graph API</b></summary>

使用以下代码片段:

```ts
// Equivalent to:
// const teamsfx = new TeamsFx(IdentityType.User, {
//   initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
//   clientId: process.env.REACT_APP_CLIENT_ID,
// }
const teamsfx = new TeamsFx();
const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
const profile = await graphClient.api("/me").get(); // Get the profile of current user
```

</details>

<br>

<details>
<summary><b>在没有用户(应用程序标识)的情况下调用 Graph API</b></summary>

它无需与 Teams 用户交互。 可以将 Microsoft Graph 调用为应用程序标识。

使用以下代码片段:

```ts
// Equivalent to:
// const teamsfx = new TeamsFx(IdentityType.App, {
//   initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
//   clientId: process.env.REACT_APP_CLIENT_ID,
// });
const teamsfx = new TeamsFx(IdentityType.App);
const graphClient = createMicrosoftGraphClient(teamsfx);
const profile = await graphClient.api("/users/{object_id_of_another_people}").get(); // Get the profile of certain user
```

</details>

<br>

## <a name="core-concepts-and-code-structure"></a>核心概念和代码结构

### <a name="teamsfx-class"></a>TeamsFx 类

默认情况下，TeamsFx 类实例从环境变量访问所有 TeamsFx 设置。 还可以设置自定义配置值以替换默认值。 请查看 [替换配置](#override-configuration)，从而了解详细信息。 创建 TeamsFx 实例时，还需要指定标识类型。 存在以下两种标识类型：

* 用户标识
* 应用程序标识

#### <a name="user-identity"></a>用户标识

| 命令 | 说明 |
|----------------|-------------|
| `new TeamsFx(IdentityType.User)`| 应用程序作为当前 Teams 用户进行身份验证。 |
| `TeamsFx:setSsoToken()`| Node.js 环境(无浏览器)中的用户标识。 |
| `TeamsFx:getUserInfo()` | 要获取用户的基础信息。 |
| `TeamsFx:login()` | 如果要使用 SSO 获取某些 OAuth 作用域的访问令牌，则将其用于允许用户执行同意流程。 |

> [!NOTE]
> 可以代表当前 Teams 用户访问资源。

#### <a name="application-identity"></a>应用程序标识

| 命令 | 说明 |
|----------------|-------------|
| `new TeamsFx(IdentityType.App)`| 应用程序作为应用程序进行身份验证。权限通常需要管理员审批。|
| `TeamsFx:getCredential()`| 它提供与标识类型自动对应的凭据实例。 |

> [!NOTE]
> 需要管理员同意以获取资源。

### <a name="credential"></a>Credential

初始化 TeamsFx 时，必须选择标识类型。 在初始化 TeamsFx 时指定标识类型后，SDK 会使用不同类型的凭据类表示标识，并通过相应的身份验证流获取访问令牌。

有三个凭据类可以简化身份验证。 [凭据文件夹](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/credential)。 凭据类可实现 `TokenCredential` 接口，该接口广泛用于 Azure 库 API，旨在为特定作用域提供访问令牌。 其他 API 依赖于凭据调用 `TeamsFx:getCredential()` 来获取 `TokenCredential` 实例。

以下是每个凭据类目标的相应场景。

#### <a name="user-identity-in-browser-environment"></a>浏览器环境中的用户标识
`TeamsUserCredential` 表示 Teams 当前用户的标识。 首次使用此凭据将请求用户同意。 它利用 Teams SSO 和代理流进行令牌交换。 当开发人员在浏览器环境中选择用户标识时，SDK 会使用此凭据。

所需配置: `initiateLoginEndpoint`、`clientId`。

#### <a name="user-identity-in-nodejs-environment"></a>Node.js 环境中的用户标识
`OnBehalfOfUserCredential` 使用代理流，且需要 Teams SSO 令牌。 其旨在用于 Azure Function 或机器人场景。 当开发人员在 Node.js 环境中选择用户标识时，SDK 会使用此凭据。

所需配置: `authorityHost`、`tenantId`、`clientId`、`clientSecret` 或 `certificateContent`。

#### <a name="application-identity-in-nodejs-environment"></a>Node.js 环境中的应用程序标识
`AppCredential` 表示应用程序标识。 当用户不参与(例如时间触发的自动化作业)时，通常会使用该标识。 当开发人员在 Node.js 环境中选择应用标识时，SDK 会使用此凭据。

所需配置: `tenantId`、`clientId`、`clientSecret` 或 `certificateContent`。

### <a name="bot-sso"></a>机器人 SSO

机器人相关类存储在 [机器人文件夹](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/bot) 下。

`TeamsBotSsoPrompt` 与机器人框架很好地集成。 开发机器人应用程序并想要利用机器人 SSO 时，它会简化身份验证流程。

所需配置: `initiateLoginEndpoint`、`tenantId`、`clientId`和 `applicationIdUri`。

### <a name="supported-functions"></a>受支持的函数

TeamsFx SDK 提供多个函数，可用于简化第三方库的配置。 它们位于 [核心文件夹](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/core) 下。

*  Microsoft Graph 服务: `createMicrosoftGraphClient` 和 `MsGraphAuthProvider` 有助于创建经过身份验证的 Graph 实例。
*  SQL: `getTediousConnectionConfig` 返回繁琐的连接配置。

所需配置:
* `sqlServerEndpoint`、`sqlUsername`、`sqlPassword` (如果要使用用户标识)
* `sqlServerEndpoint`、`sqlIdentityId` (如果要使用 MSI 标识)

### <a name="error-handling"></a>错误处理

API 错误响应为 `ErrorWithCode`，其中包含错误代码和错误消息。 例如，要筛选出特定错误，可以使用以下代码片段:

```ts
try {
  const teamsfx = new TeamsFx();
  await teamsfx.login("User.Read");
} catch (err: unknown) {
  if (err instanceof ErrorWithCode && err.code !== ErrorCode.ConsentFailed) {
    throw err;
  } else {
    // Silently fail because user cancels the consent dialog
        return;
  }
}
```

如果在其他库(例如 Microsoft Graph)中使用凭据实例，则可能会捕获并转换错误。

```ts
try {
  const teamsfx = new TeamsFx();
  const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
  const profile = await graphClient.api("/me").get();
} catch (err: unknown) {
  // ErrorWithCode is handled by Graph client
  if (err instanceof GraphError && err.code?.includes(ErrorCode.UiRequiredError)) {
    this.setState({
      showLoginBtn: true,
    });
  }
}
```

## <a name="scenarios"></a>应用场景

以下节为常见场景提供了多个代码片段:

<br>

<details>
<summary><b>在选项卡应用中使用 Graph API</b></summary>
 
使用 `TeamsFx` 和 `createMicrosoftGraphClient`。

```ts
const teamsfx = new TeamsFx();
const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]);
const profile = await graphClient.api("/me").get();
```

</details>

<br>

<details>
<summary><b>在选项卡应用中调用 Azure Function</b></summary>

使用 `axios` 库向 Azure Function 发出 HTTP 请求。

```ts
const teamsfx = new TeamsFx();
const token = teamsfx.getCredential().getToken(""); // Get SSO token for the use
// Call API hosted in Azure Functions on behalf of user
const apiEndpoint = teamsfx.getConfig("apiEndpoint");
const response = await axios.default.get(apiEndpoint + "api/httptrigger1", {
  headers: {
    authorization: "Bearer " + token,
  },
});
```

</details>

<br>

<details>
<summary><b>访问 Azure Function 中的 SQL 数据库</b></summary>


使用 `tedious` 库访问 SQL，并利用管理身份验证的 `DefaultTediousConnectionConfiguration`。
除了 `tedious`，还可以根据 `sqlConnectionConfig.getConfig()` 的结果撰写其他 SQL 库的连接配置。

```ts
// Equivalent to:
// const sqlConnectConfig = new DefaultTediousConnectionConfiguration({
//    sqlServerEndpoint: process.env.SQL_ENDPOINT,
//    sqlUsername: process.env.SQL_USER_NAME,
//    sqlPassword: process.env.SQL_PASSWORD,
// });
const teamsfx = new TeamsFx();
// If there's only one SQL database
const config = await getTediousConnectionConfig(teamsfx);
// If there are multiple SQL databases
const config2 = await getTediousConnectionConfig(teamsfx "your database name");
const connection = new Connection(config);
connection.on("connect", (error) => {
  if (error) {
    console.log(error);
  }
});
```

</details>

<br>

<details>
<summary><b>在 Azure Function 中使用基于证书的身份验证</b></summary>

```ts
const authConfig = {
  clientId: process.env.M365_CLIENT_ID,
  certificateContent: "The content of a PEM-encoded public/private key certificate",
  authorityHost: process.env.M365_AUTHORITY_HOST,
  tenantId: process.env.M365_TENANT_ID,
};
const teamsfx = new TeamsFx(IdentityType.App);
teamsfx.setCustomeConfig({
  certificateContent: "The content of a PEM-encoded public/private key certificate"
});
const token = teamsfx.getCredential().getToken();
```

</details>

<br>

<details>
<summary><b>在机器人应用程序中使用 Graph API</b></summary>

将 `TeamsBotSsoPrompt` 添加到对话集。

```ts
const { ConversationState, MemoryStorage } = require("botbuilder");
const { DialogSet, WaterfallDialog } = require("botbuilder-dialogs");
const { TeamsBotSsoPrompt } = require("@microsoft/teamsfx");

const convoState = new ConversationState(new MemoryStorage());
const dialogState = convoState.createProperty("dialogState");
const dialogs = new DialogSet(dialogState);

const teamsfx = new TeamsFx();
dialogs.add(
  new TeamsBotSsoPrompt(teamsfx, "TeamsBotSsoPrompt", {
    scopes: ["User.Read"],
  })
);

dialogs.add(
  new WaterfallDialog("taskNeedingLogin", [
    async (step) => {
      return await step.beginDialog("TeamsBotSsoPrompt");
    },
    async (step) => {
      const token = step.result;
      if (token) {
        // ... continue with task needing access token ...
      } else {
        await step.context.sendActivity(`Sorry... We couldn't log you in. Try again later.`);
        return await step.endDialog();
      }
    },
  ])
);
```

</details>

<br>

## <a name="advanced-customization"></a>高级自定义

### <a name="configure-log"></a>配置日志

使用此库时，可以设置客户日志级别并重定向输出。 日志记录默认处于禁用状态，可以设置日志级别以启用。

#### <a name="enable-log-by-setting-log-level"></a>设置日志级别以启用日志

仅在设置日志级别时才启用日志记录。 默认情况下，它会将日志信息打印到控制台。

使用以下代码片段设置日志级别:

```ts
// Only need the warning and error messages.
setLogLevel(LogLevel.Warn);
```

可以设置自定义记录器或日志函数，从而重定向日志输出。

#### <a name="redirect-by-setting-custom-logger"></a>设置自定义记录器以重定向

```ts
setLogLevel(LogLevel.Info);
// Set another logger if you want to redirect to Application Insights in Azure Function
setLogger(context.log);
```

#### <a name="redirect-by-setting-custom-log-function"></a>设置自定义日志函数以重定向

> [!NOTE]
> 如果设置自定义记录器，则日志函数不会生效。

```ts
setLogLevel(LogLevel.Info);
// Only log error message to Application Insights in bot application.
setLogFunction((level: LogLevel, message: string) => {
  if (level === LogLevel.Error) {
    this.telemetryClient.trackTrace({
      message: message,
      severityLevel: Severity.Error,
    });
  }
});
```

## <a name="override-configuration"></a>替换配置
创建 TeamsFx 实例时，可以传递自定义配置，从而替换默认配置，或在缺少环境变量时设置必填字段。

- 如果已使用 VS Code Toolkit 创建选项卡项目，则将从预配置的环境变量使用以下配置值:
  * authorityHost (REACT_APP_AUTHORITY_HOST)
  * tenantId (REACT_APP_TENANT_ID)
  * clientId (REACT_APP_CLIENT_ID)
  * initiateLoginEndpoint (REACT_APP_START_LOGIN_PAGE_URL)
  * applicationIdUri (REACT_APP_START_LOGIN_PAGE_URL)
  * apiEndpoint (REACT_APP_FUNC_ENDPOINT)
  * apiName (REACT_APP_FUNC_NAME)

- 如果已使用 VS Code Toolkit 创建 Azure Function / 机器人项目，则将从预配置的环境变量使用以下配置值:
  * initiateLoginEndpoint (INITIATE_LOGIN_ENDPOINT)
  * authorityHost (M365_AUTHORITY_HOST)
  * tenantId (M365_TENANT_ID)
  * clientId (M365_CLIENT_ID)
  * clientSecret (M365_CLIENT_SECRET)
  * applicationIdUri (M365_APPLICATION_ID_URI)
  * apiEndpoint (API_ENDPOINT)
  * sqlServerEndpoint (SQL_ENDPOINT)
  * sqlUsername (SQL_USER_NAME)
  * sqlPassword (SQL_PASSWORD)
  * sqlDatabaseName (SQL_DATABASE_NAME)
  * sqlIdentityId (IDENTITY_ID)

## <a name="upgrade-latest-sdk-version"></a>升级最新的 SDK 版本

如果使用的是具有 `loadConfiguration()` 的 SDK 版本，则可以按照以下步骤升级到最新的 SDK 版本。
1. 删除 `loadConfiguration()` 并使用 `new TeamsFx(IdentityType.User, { ...customConfig })` 传递自定义设置
2. 将 `new TeamsUserCredential()` 替换为 `new TeamsFx()`
3. 将 `new M365TenantCredential()` 替换为 `new TeamsFx(IdentityType.App)`
4. 将 `new OnBehalfOfUserCredential(ssoToken)` 替换为 `new TeamsFx().setSsoToken(ssoToken)`
5. 将 `TeamsFx` 的实例传递给帮助程序函数，从而替换凭据实例

有关详细信息，请参阅 [TeamsFx 类](#teamsfx-class)。

## <a name="next-step"></a>后续步骤

有关如何使用 TeamsFx SDK 的详细示例的 [示例](https://github.com/OfficeDev/TeamsFx-Samples)项目。

## <a name="see-also"></a>另请参阅

[Microsoft TeamsFx 示例库](https://github.com/OfficeDev/TeamsFx-Samples)。
