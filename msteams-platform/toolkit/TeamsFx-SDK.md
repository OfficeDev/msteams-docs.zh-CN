---
title: TeamsFx SDK
author: MuyangAmigo
description: 关于 TeamsFx SDK
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 63c5fad9c795c513b476f305c09d94ffad7c5d61
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2021
ms.locfileid: "61227979"
---
# <a name="teamsfx-sdk-for-typescript-or-javascript"></a>适用于 TypeScript 或 JavaScript 的 TeamsFx SDK

TeamsFx 旨在将实现标识和访问云资源的任务减少为使用"零配置"的单行语句。

使用库可：

- 以类似方式访问客户端和服务器环境中的核心功能。
- 以简化的方式编写用户身份验证代码。

   * [源代码](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk) 
   * [包 (NPM) ](https://www.npmjs.com/package/@microsoft/teamsfx) 
   * [API 参考文档](https://aka.ms/teamsfx-sdk-help) 
   * [示例](https://github.com/OfficeDev/TeamsFx-Samples)

## <a name="get-started"></a>入门

TeamsFx SDK 使用 TeamsFx 工具包或 CLI 在基架项目中预配置。
有关应用项目Teams，请参阅[自述文件](https://github.com/OfficeDev/TeamsFx/blob/main/packages/vscode-extension/README.md)。

### <a name="prerequisites"></a>先决条件

- Node.js `10.x.x` 或更高版本。
- 如果你的项目安装了 `botbuilder` 相关 [包](https://github.com/Microsoft/botbuilder-js#packages) 作为依赖项，请确保它们的版本和 版本相同 `>= 4.9.3` 。  (问题 [- 所有 BOTBUILDER 程序包](https://github.com/BotBuilderCommunity/botbuilder-community-js/issues/57#issuecomment-508538548) 的版本应) 

> [!TIP]
> TeamsFx 工具包创建的项目VS Code扩展或 CLI 工具。

### <a name="install-the-microsoftteamsfx-package"></a>安装 `@microsoft/teamsfx` 程序包

使用 安装适用于 TypeScript 或 JavaScript 的 TeamsFx `npm` SDK：

```bash
npm install @microsoft/teamsfx
```

### <a name="create-and-authenticate-a-microsoftgraphclient"></a>创建和验证 `MicrosoftGraphClient`

若要创建图形客户端对象以访问 Microsoft Graph API，你将需要凭据执行身份验证。 SDK 提供了几个凭据类，可供选择以满足各种要求。您需要先加载配置，然后再使用任何凭据。

- 在浏览器环境中，需要显式传递配置参数。 基架项目React提供了使用的环境变量。

```ts
loadConfiguration({
  authentication: {
    initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
    simpleAuthEndpoint: process.env.REACT_APP_TEAMSFX_ENDPOINT,
    clientId: process.env.REACT_APP_CLIENT_ID,
  },
});
```

- 在 NodeJS 环境（如 Azure Function）中，只需调用 `loadConfiguration` 。 默认情况下，它将从环境变量加载。

```ts
loadConfiguration();
```

#### <a name="using-teams-app-user-credential"></a>使用Teams应用程序用户凭据

使用以下代码段：

> [注意]只能在浏览器应用程序（如"选项卡应用"Teams）中使用此凭据类。

```ts
loadConfiguration({
  authentication: {
    initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
    simpleAuthEndpoint: process.env.REACT_APP_TEAMSFX_ENDPOINT,
    clientId: process.env.REACT_APP_CLIENT_ID,
  },
});
const credential = new TeamsUserCredential();
const graphClient = createMicrosoftGraphClient(credential, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
const profile = await graphClient.api("/me").get();
```

#### <a name="using-microsoft-365-tenant-credential"></a>使用Microsoft 365租户凭据

它不需要与应用用户Teams交互。 你可以将 Microsoft Graph为应用程序。
使用以下代码段：

```ts
loadConfiguration();
const credential = new M365TenantCredential();
const graphClient = createMicrosoftGraphClient(credential);
const profile = await graphClient.api("/users/{object_id_of_another_people}").get();
```

## <a name="core-concepts-and-code-structure"></a>核心概念和代码结构

### <a name="credentials"></a>凭据

凭据文件夹下有 3 个 [凭据类，](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/credential) 可帮助简化身份验证。 

凭据类实现在 Azure 库 API `TokenCredential` 中广泛使用的接口。 它们旨在为特定范围提供访问令牌。
在某些方案中，凭据类表示不同的标识。

`TeamsUserCredential`表示Teams当前用户的标识。 使用此凭据将在第一次请求用户同意。
`M365TenantCredential`表示Microsoft 365租户标识。 它通常在用户未涉及时（如时间触发的自动化作业）使用。
`OnBehalfOfUserCredential` 使用代表流。 它需要访问令牌，你可以获取不同范围的新令牌。 它旨在用于 Azure 函数或自动程序方案。

### <a name="bots"></a>机器人

与机器人相关的类存储在自动 [程序文件夹](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/bot) 下。

`TeamsBotSsoPrompt` 与 Bot 框架具有良好的集成。 它简化了开发自动程序应用程序的身份验证过程。

### <a name="helper-functions"></a>帮助程序函数

TeamsFx SDK 提供了帮助程序函数，以便于第三方库的配置。 它们位于核心 [文件夹](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/core) 下。

### <a name="error-handling"></a>错误处理

如果发生错误，API `ErrorWithCode` 将引发。 每个 `ErrorWithCode` 包含错误代码和错误消息。

例如，若要筛选掉特定错误，可以使用以下检查：

```ts
try {
  const credential = new TeamsUserCredential();
  await credential.login("User.Read");
} catch (err: unknown) {
  if (err instanceof ErrorWithCode && err.code !== ErrorCode.ConsentFailed) {
    throw err;
  } else {
    // Silently fail because user cancels the consent dialog
    return;
  }
}
```

如果凭据实例在其他库（如 Microsoft Graph）中使用，则有可能捕获并转换错误。

```ts
try {
  const credential = new TeamsUserCredential();
  const graphClient = createMicrosoftGraphClient(credential, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
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

以下各节提供了几个代码段，这些代码段涵盖了一些最常见的方案：

- [在选项卡Graph API](#use-graph-api-in-tab-app)
- [在选项卡应用中调用 Azure 函数](#call-azure-function-in-tab-app)
- [访问 SQL Azure 函数中的数据库](#access-sql-database-in-azure-function)
- [在 Azure 函数中使用基于证书的身份验证](#use-certificate-based-authentication-in-azure-function)
- [在Graph应用程序中使用自动程序 API](#use-graph-api-in-bot-application)

### <a name="use-graph-api-in-tab-app"></a>在选项卡Graph API

使用 `TeamsUserCredential` `createMicrosoftGraphClient` 和 。

```ts
loadConfiguration({
  authentication: {
    initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
    simpleAuthEndpoint: process.env.REACT_APP_TEAMSFX_ENDPOINT,
    clientId: process.env.REACT_APP_CLIENT_ID,
  },
});
const credential: any = new TeamsUserCredential();
const graphClient = createMicrosoftGraphClient(credential, ["User.Read"]);
const profile = await graphClient.api("/me").get();
```

### <a name="call-azure-function-in-tab-app"></a>在选项卡应用中调用 Azure 函数

使用 `axios` 库向 Azure 函数进行 HTTP 请求。

```ts
loadConfiguration({
  authentication: {
    initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
    simpleAuthEndpoint: process.env.REACT_APP_TEAMSFX_ENDPOINT,
    clientId: process.env.REACT_APP_CLIENT_ID,
  },
});
const credential: any = new TeamsUserCredential();
const token = credential.getToken(""); // Get SSO token for the user
// Call API hosted in Azure Functions on behalf of user
const apiConfig = getResourceConfiguration(ResourceType.API);
const response = await axios.default.get(apiConfig.endpoint + "api/httptrigger1", {
  headers: {
    authorization: "Bearer " + token,
  },
});
```

### <a name="access-sql-database-in-azure-function"></a>访问 SQL Azure 函数中的数据库

使用 `tedious` 库访问SQL并利用 `DefaultTediousConnectionConfiguration` 管理身份验证。
除了 `tedious` ，还可以基于 的结果撰写其他SQL库的连接配置 `sqlConnectionConfig.getConfig()` 。

```ts
loadConfiguration();
const sqlConnectConfig = new DefaultTediousConnectionConfiguration();
const config = await sqlConnectConfig.getConfig();
const connection = new Connection(config);
connection.on("connect", (error) => {
  if (error) {
    console.log(error);
  }
});
```

### <a name="use-certificate-based-authentication-in-azure-function"></a>在 Azure 函数中使用基于证书的身份验证

```ts
loadConfiguration({
  authentication: {
    clientId: process.env.M365_CLIENT_ID,
    certificateContent: "The content of a PEM-encoded public/private key certificate",
    authorityHost: process.env.M365_AUTHORITY_HOST,
    tenantId: process.env.M365_TENANT_ID,
  },
});
```

### <a name="use-graph-api-in-bot-application"></a>在Graph应用程序中使用自动程序 API

添加到 `TeamsBotSsoPrompt` 对话框集。

```ts
const { ConversationState, MemoryStorage } = require("botbuilder");
const { DialogSet, WaterfallDialog } = require("botbuilder-dialogs");
const { TeamsBotSsoPrompt } = require("@microsoft/teamsfx");

const convoState = new ConversationState(new MemoryStorage());
const dialogState = convoState.createProperty("dialogState");
const dialogs = new DialogSet(dialogState);

loadConfiguration();
dialogs.add(
  new TeamsBotSsoPrompt("TeamsBotSsoPrompt", {
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

## <a name="troubleshooting"></a>疑难解答

### <a name="configure-log"></a>配置日志

使用此库时，可以设置客户日志级别并重定向输出。
默认情况下，日志记录已关闭，您可以通过设置日志级别来启用日志记录。

#### <a name="enable-log-by-setting-log-level"></a>通过设置日志级别启用日志

设置日志级别时，将启用日志记录。 默认情况下，它将日志信息打印到控制台。

使用下面的代码段设置日志级别：

```ts
// Only need the warning and error messages.
setLogLevel(LogLevel.Warn);
```

可以通过设置自定义日志记录器或日志函数重定向日志输出。

##### <a name="redirect-by-setting-custom-logger"></a>通过设置自定义记录器重定向

```ts
setLogLevel(LogLevel.Info);
// Set another logger if you want to redirect to Application Insights in Azure Function
setLogger(context.log);
```

##### <a name="redirect-by-setting-custom-log-function"></a>通过设置自定义日志函数重定向

请注意，如果设置自定义记录器，日志函数将不会生效。

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

## <a name="see-also"></a>另请参阅

[Microsoft TeamsFx 示例库](https://github.com/OfficeDev/TeamsFx-Samples)