---
title: TeamsFx SDK
author: MuyangAmigo
description: 关于 TeamsFx SDK
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: ade31e39d48b92cca4309b16762dc95afccf1925
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073095"
---
# <a name="teamsfx-sdk"></a>TeamsFx SDK

TeamsFx 通过利用 Teams SSO，将云资源访问到具有零配置的单行语句来帮助减少开发人员任务。 TeamsFx SDK 内置用于浏览器和Node.js环境，常见方案包括：

* Teams选项卡应用程序
* Azure 函数
* Teams机器人

可以使用 TeamsFx SDK 执行以下操作：

* 访问客户端和服务器环境中的核心功能 
* 以简化的方式编写用户身份验证代码

## <a name="prerequisites"></a>先决条件

安装以下工具并设置开发环境：

* 最新版本的Node.js
* 如果项目已将相关[包](https://github.com/Microsoft/botbuilder-js#packages)安装`botbuilder`为依赖项，请确保它们的版本相同。 目前，所需的版本为 4.15.0 或更高版本，有关详细信息，请参阅 [机器人生成器包的版本应该相同](https://github.com/BotBuilderCommunity/botbuilder-community-js/issues/57#issuecomment-508538548)。

必须具备以下工作知识：

* [源代码](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk)
* [ (NPM) 打包 ](https://www.npmjs.com/package/@microsoft/teamsfx)
* [API 参考文档](https://aka.ms/teamsfx-sdk-help)
* [示例](https://github.com/OfficeDev/TeamsFx-Samples)

## <a name="get-started"></a>入门

TeamsFx SDK 是使用 TeamsFx Toolkit 或 CLI 在基架项目中预配置的。
有关详细信息，请参阅[Teams应用项目](https://github.com/OfficeDev/TeamsFx/blob/main/packages/vscode-extension/README.md)。

### <a name="install-the-microsoftteamsfx-package"></a>`@microsoft/teamsfx`安装包

使用以下内容安装 TeamsFx SDK for TypeScript 或 JavaScript `npm`：

```bash
npm install @microsoft/teamsfx
```

### <a name="create-microsoftgraphclient-service"></a>创建 `MicrosoftGraphClient` 服务

若要创建图形客户端对象并访问 Microsoft 图形 API，需要凭据进行身份验证。 SDK 提供用于为开发人员配置的 API。

<br>

<details>
<summary><b>代表Teams用户 (用户标识) 调用图形 API</b></summary>

使用以下代码片段：

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
<summary><b>在没有用户 (应用程序标识) 的情况下调用图形 API</b></summary>

它不需要与Teams用户交互。 可以将 Microsoft Graph调用为应用程序标识。

使用以下代码片段：

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

默认情况下，TeamsFx 类实例从环境变量访问所有 TeamsFx 设置。 还可以设置自定义配置值以替代默认值。 有关详细信息，请查看 [替代配置](#override-configuration) 。 创建 TeamsFx 实例时，还需要指定标识类型。 存在以下两种标识类型：

* 用户标识
* 应用程序标识

#### <a name="user-identity"></a>用户标识

| 命令 | 说明 |
|----------------|-------------|
| `new TeamsFx(IdentityType.User)`| 应用程序将作为当前Teams用户进行身份验证。 |
| `TeamsFx:setSsoToken()`| Node.js环境中的用户标识 (没有浏览器) 。 |
| `TeamsFx:getUserInfo()` | 获取用户的基础信息。 |
| `TeamsFx:login()` | 如果要使用 SSO 获取某些 OAuth 范围的访问令牌，则使用它来让用户执行同意过程。 |

> [!NOTE]
> 可以代表当前Teams用户访问资源。

#### <a name="application-identity"></a>应用程序标识

| 命令 | 说明 |
|----------------|-------------|
| `new TeamsFx(IdentityType.App)`| 应用程序将作为应用程序进行身份验证。权限通常需要管理员的批准。|
| `TeamsFx:getCredential()`| 它提供与标识类型自动对应的凭据实例。 |

> [!NOTE]
> 需要管理员同意资源。

### <a name="credential"></a>Credential

初始化 TeamsFx 时，必须选择标识类型。 在初始化 TeamsFx 时指定标识类型后，SDK 使用不同类型的凭据类来表示标识，并通过相应的身份验证流获取访问令牌。

有三个凭据类可以简化身份验证。 [凭据文件夹](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/credential)。 凭据类实现 `TokenCredential` 接口，该接口广泛用于 Azure 库 API，旨在为特定范围提供访问令牌。 其他 API 依赖于凭据调用`TeamsFx:getCredential()`来获取实例。`TokenCredential`

下面是每个凭据类目标的相应方案。

#### <a name="user-identity-in-browser-environment"></a>浏览器环境中的用户标识
`TeamsUserCredential`表示Teams当前用户的标识。 使用此凭据将首次请求用户同意。 它利用Teams SSO 和代理流进行令牌交换。 当开发人员在浏览器环境中选择用户标识时，SDK 使用此凭据。

所需配置： `initiateLoginEndpoint`， `clientId`.

#### <a name="user-identity-in-nodejs-environment"></a>Node.js环境中的用户标识
`OnBehalfOfUserCredential`使用代理流，需要Teams SSO 令牌。 它设计用于 Azure 函数或机器人方案。 当开发人员在Node.js环境中选择用户标识时，SDK 使用此凭据。

必需的配置：`authorityHost`、`tenantId`、`clientId``clientSecret`或 `certificateContent`。

#### <a name="application-identity-in-nodejs-environment"></a>Node.js环境中的应用程序标识
`AppCredential` 表示应用程序标识。 当用户不参与时（如时间触发的自动化作业）时，通常会使用它。 当开发人员在Node.js环境中选择应用标识时，SDK 使用此凭据。

必需配置：`tenantId`或 `clientSecret` `clientId``certificateContent`.

### <a name="bot-sso"></a>Bot SSO

机器人相关类存储在 [机器人文件夹](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/bot)下。

`TeamsBotSsoPrompt` 与机器人框架有良好的集成。 开发机器人应用程序并想要利用机器人 SSO 时，它会简化身份验证过程。

必需的配置： `initiateLoginEndpoint`、 `tenantId`、 `clientId`和 `applicationIdUri`.

### <a name="supported-functions"></a>支持的函数

TeamsFx SDK 提供了多个函数，用于简化第三方库的配置。 它们位于 [核心文件夹](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/core)下。

*  Microsoft Graph服务：`createMicrosoftGraphClient`并`MsGraphAuthProvider`帮助创建经过身份验证的Graph实例。
*  SQL：`getTediousConnectionConfig`返回繁琐的连接配置。

所需的配置：
* `sqlServerEndpoint``sqlPassword`，`sqlUsername`如果要使用用户标识
* `sqlServerEndpoint`， `sqlIdentityId` 如果要使用 MSI 标识

### <a name="error-handling"></a>错误处理

API 错误响应包含 `ErrorWithCode`错误代码和错误消息。 例如，若要筛选出特定错误，可以使用以下代码片段：

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

如果在其他库（如 Microsoft Graph）中使用凭据实例，则可能会捕获并转换错误。

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

以下部分为常见方案提供了多个代码片段：

<br>

<details>
<summary><b>在选项卡应用中使用图形 API</b></summary>
 
使用 `TeamsFx` 和 `createMicrosoftGraphClient`.

```ts
const teamsfx = new TeamsFx();
const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]);
const profile = await graphClient.api("/me").get();
```

</details>

<br>

<details>
<summary><b>在选项卡应用中调用 Azure 函数</b></summary>

使用 `axios` 库向 Azure 函数发出 HTTP 请求。

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
<summary><b>访问 Azure 函数中的SQL数据库</b></summary>


使用`tedious`库访问SQL并利用`DefaultTediousConnectionConfiguration`它来管理身份验证。
此外`tedious`，还可以根据结果编写其他SQL库的`sqlConnectionConfig.getConfig()`连接配置。

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
<summary><b>在 Azure 函数中使用基于证书的身份验证</b></summary>

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
<summary><b>在机器人应用程序中使用图形 API</b></summary>

添加 `TeamsBotSsoPrompt` 到对话集。

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

使用此库时，可以设置客户日志级别并重定向输出。 默认情况下，日志记录已关闭，可以通过设置日志级别将其打开。

#### <a name="enable-log-by-setting-log-level"></a>通过设置日志级别启用日志

仅在设置日志级别时才启用日志记录。 默认情况下，它将日志信息打印到控制台。

使用以下代码片段设置日志级别：

```ts
// Only need the warning and error messages.
setLogLevel(LogLevel.Warn);
```

可以通过设置自定义记录器或日志函数来重定向日志输出。

#### <a name="redirect-by-setting-custom-logger"></a>通过设置自定义记录器重定向

```ts
setLogLevel(LogLevel.Info);
// Set another logger if you want to redirect to Application Insights in Azure Function
setLogger(context.log);
```

#### <a name="redirect-by-setting-custom-log-function"></a>通过设置自定义日志函数重定向

> [!NOTE]
> 如果设置自定义记录器，日志函数将不会生效。

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

## <a name="override-configuration"></a>替代配置
创建 TeamsFx 实例时，可以传递自定义配置，以便在缺少环境变量时重写默认配置或设置所需字段。

- 如果已使用VS Code Toolkit创建选项卡项目，则将从预配置的环境变量中使用以下配置值：
  * authorityHost (REACT_APP_AUTHORITY_HOST) 
  * tenantId (REACT_APP_TENANT_ID) 
  * clientId (REACT_APP_CLIENT_ID) 
  * initiateLoginEndpoint (REACT_APP_START_LOGIN_PAGE_URL) 
  * applicationIdUri (REACT_APP_START_LOGIN_PAGE_URL) 
  * apiEndpoint (REACT_APP_FUNC_ENDPOINT) 
  * apiName (REACT_APP_FUNC_NAME) 

- 如果已使用VS Code Toolkit创建 Azure Function/bot 项目，则将从预配置的环境变量中使用以下配置值：
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

## <a name="upgrade-latest-sdk-version"></a>升级最新 SDK 版本

如果使用的是 SDK 版本， `loadConfiguration()`可以按照以下步骤升级到最新的 SDK 版本。
1. 使用 >a0/a0> 删除 `loadConfiguration()` 和传递自定义设置 `new TeamsFx(IdentityType.User, { ...customConfig })`
2. 替换 `new TeamsUserCredential()` 为 `new TeamsFx()`
3. 替换 `new M365TenantCredential()` 为 `new TeamsFx(IdentityType.App)`
4. 替换 `new OnBehalfOfUserCredential(ssoToken)` 为 `new TeamsFx().setSsoToken(ssoToken)`
5. 传递帮助程序函数的 `TeamsFx` 实例以替换凭据实例

有关详细信息，请参阅 [TeamsFx 类](#teamsfx-class)。

## <a name="next-step"></a>后续步骤

有关如何使用 TeamsFx SDK 的详细示例的[示例](https://github.com/OfficeDev/TeamsFx-Samples)项目。

## <a name="see-also"></a>另请参阅

[Microsoft TeamsFx 示例库](https://github.com/OfficeDev/TeamsFx-Samples)。
