---
title: TeamsFx SDK
author: surbhigupta
description: 在本模块中，了解 TeamsFx SDK、核心概念和代码结构、高级自定义和方案
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: e28e726a1915cdbc8fddf501b0352d160673516c
ms.sourcegitcommit: 637b8f93b103297b1ff9f1af181680fca6f4499d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2022
ms.locfileid: "68499165"
---
# <a name="teamsfx-sdk"></a>TeamsFx SDK

TeamsFx 通过使用 Microsoft Teams 单一登录 (Teams SSO) ，并将云资源访问到零配置的单行语句来帮助减少任务。 可以在浏览器和Node.js环境中使用 TeamsFx SDK。 可以在客户端和服务器环境中访问 TeamsFx 核心功能。 可以采用简化的方式编写用户身份验证代码，

* Teams 选项卡
* Teams 机器人
* Azure Function

## <a name="prerequisites"></a>先决条件

需要安装以下工具并设置开发环境：

| &nbsp; | 安装 | 用于使用... |
   | --- | --- | --- |
   | &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download) | JavaScript、TypeScript 或 SharePoint 框架 (SPFx) 生成环境。 使用版本 1.55 或更高版本。 |
   | &nbsp; | [Teams 工具包](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)| Microsoft Visual Studio Code扩展，用于为应用创建项目基架。 使用 4.0.0 版本。 |
   | &nbsp; | [Node.js](https://nodejs.org/en/download/) | 后端 JavaScript 运行时环境。 使用最新的 v16 LTS 版本。|
   | &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | 通过聊天、会议、通话等应用与每一位同事进行协作的 Microsoft Teams - 一个地方完成所有操作。|
   | &nbsp; | [微软&nbsp;边缘](https://www.microsoft.com/edge) (建议) 或 [Google Chrome](https://www.google.com/chrome/) | 包含开发人员工具的浏览器。 |

> [!NOTE]
> 如果项目已将 `botbuilder` 相关的 [包](https://github.com/Microsoft/botbuilder-js#packages) 安装为依赖项，请确保它们的版本相同。

必须具备以下工作知识：

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

## <a name="teamsfx-core-functionalities"></a>TeamsFx 核心功能

### <a name="teamsfx-class"></a>TeamsFx 类

默认情况下，TeamsFx 类实例从环境变量访问所有 TeamsFx 设置。 还可以设置自定义配置值以替换默认值。 请查看 [替换配置](#override-configuration) 以了解详细信息。
创建 TeamsFx 实例时，还需要指定标识类型。
存在以下两种标识类型：

* **用户标识**：表示 Teams 的当前用户。
* **应用程序标识**：表示应用程序本身。

    > [!NOTE]
    > 对于这两种标识类型，TeamsFx 构造函数和方法不同。

可在以下部分了解有关用户标识和应用程序标识的详细信息：

<details>
<summary><b> 用户标识 </b></summary>

| 命令 | 说明 |
|----------------|-------------|
| `new TeamsFx(IdentityType.User)`| 应用程序作为当前 Teams 用户进行身份验证。 |
| `TeamsFx:setSsoToken()`| Node.js 环境(无浏览器)中的用户标识。 |
| `TeamsFx:getUserInfo()` | 要获取用户的基础信息。 |
| `TeamsFx:login()` | 如果要使用 SSO 获取某些 OAuth 作用域的访问令牌，则将其用于允许用户执行同意流程。 |

> [!NOTE]
> 可以代表当前 Teams 用户访问资源。
</details>

<details>
<summary><b> 应用程序标识 </b></summary>

| 命令 | 说明 |
|----------------|-------------|
| `new TeamsFx(IdentityType.App)`| Application  is authenticated as an application. The permission usually needs administrator's approval.|
| `TeamsFx:getCredential()`| 它提供与标识类型自动对应的凭据实例。 |

> [!NOTE]
> 需要管理员同意以获取资源。
</details>

### <a name="credential"></a>Credential

若要初始化 TeamsFx，必须选择所需的标识类型。 指定标识类型 SDK 后，使用不同类型的凭据类。 这些表示标识并通过相应的身份验证流获取访问令牌。 凭据类实现 `TokenCredential` 在 Azure 库 API 中广泛使用的接口，旨在为特定范围提供访问令牌。 其他 API 依赖于凭据调用 `TeamsFx:getCredential()` 来获取 `TokenCredential` 实例。 有关凭据和身份验证流相关类的详细信息，请参阅 [凭据文件夹](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/credential)。

有三个凭据类可以简化身份验证。 以下是每个凭据类目标的相应场景。

<details>
<summary><b> 浏览器环境中的用户标识 </b></summary>

`TeamsUserCredential` 表示 Teams 当前用户的标识。 首次对用户的凭据进行身份验证时，Teams SSO 会为令牌交换执行代理流。 在浏览器环境中选择用户标识时，SDK 使用此凭据。

所需的配置为： `initiateLoginEndpoint` 和 `clientId`.
</details>

<details>
<summary><b> Node.js环境中的用户标识 </b></summary>

`OnBehalfOfUserCredential` 在 Azure 函数或机器人方案中，使用代表流并需要 Teams SSO 令牌。 在Node.js环境中选择用户标识时，TeamsFx SDK 使用以下凭据。

所需配置: `authorityHost`、`tenantId`、`clientId`、`clientSecret` 或 `certificateContent`。
</details>

<details>
<summary><b> Node.js环境中的应用标识 </b></summary>

`AppCredential` 表示应用标识。 当用户未参与时（例如，在时间触发的自动化作业中）时，可以使用应用标识。 在Node.js环境中选择应用标识时，TeamsFx SDK 使用以下凭据。

所需配置: `tenantId`、`clientId`、`clientSecret` 或 `certificateContent`。
</details>

### <a name="bot-sso"></a>机器人 SSO

机器人相关类存储在 [机器人文件夹](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/bot) 下。

`TeamsBotSsoPrompt` 与机器人框架集成。 开发机器人应用程序并想要使用机器人 SSO 时，它会简化身份验证过程。

所需配置: `initiateLoginEndpoint`、`tenantId`、`clientId`和 `applicationIdUri`。

### <a name="supported-functions"></a>受支持的函数

TeamsFx SDK provides several functions to ease the configuration for third-party libraries. They're located under [core folder](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/core).

* Microsoft Graph 服务: `createMicrosoftGraphClient` 和 `MsGraphAuthProvider` 有助于创建经过身份验证的 Graph 实例。
* SQL: `getTediousConnectionConfig` 返回繁琐的连接配置。

    所需配置:

  * 如果要使用用户标识，则`sqlServerEndpoint``sqlUsername``sqlPassword`是必需的。
  * 如果要使用 MSI 标识，则`sqlServerEndpoint``sqlIdentityId`是必需的。

### <a name="override-configuration"></a>替换配置

创建新 `TeamsFx` 实例时，可以传递自定义配置，以替代默认配置或在缺少时 `environment variables` 设置所需的字段。

<details>
<summary><b> 对于选项卡项目 </b> </summary>

如果已使用 Microsoft Visual Studio Code Toolkit 创建选项卡项目，则将从预配置的环境变量中使用以下配置值：

* authorityHost (REACT_APP_AUTHORITY_HOST)
* tenantId (REACT_APP_TENANT_ID)
* clientId (REACT_APP_CLIENT_ID)
* initiateLoginEndpoint (REACT_APP_START_LOGIN_PAGE_URL)
* applicationIdUri (REACT_APP_START_LOGIN_PAGE_URL)
* 仅当有后端函数时才使用 apiEndpoint (REACT_APP_FUNC_ENDPOINT) //
* 仅当有后端函数时才使用 apiName (REACT_APP_FUNC_NAME) //

</details>

<details>
<summary><b> 对于 Azure 函数或机器人项目 </b></summary>

如果已使用 Visual Studio Code Toolkit 创建了 Azure 函数或机器人项目，则将从预配置的环境变量中使用以下配置值：

* initiateLoginEndpoint (INITIATE_LOGIN_ENDPOINT)
* authorityHost (M365_AUTHORITY_HOST)
* tenantId (M365_TENANT_ID)
* clientId (M365_CLIENT_ID)
* clientSecret (M365_CLIENT_SECRET)
* applicationIdUri (M365_APPLICATION_ID_URI)
* apiEndpoint (API_ENDPOINT)

* 仅当有 sql 实例时才使用 sqlServerEndpoint (SQL_ENDPOINT) //
* 仅当有 sql 实例时才使用 sqlUsername (SQL_USER_NAME) //
* 仅当有 sql 实例时才使用 sqlPassword (SQL_PASSWORD) //
* sqlDatabaseName (SQL_DATABASE_NAME) // 仅在存在 sql 实例时使用
* sqlIdentityId (IDENTITY_ID) // 仅在存在 sql 实例时使用

</details>

### <a name="error-handling"></a>错误处理

API 错误响应的基本类型是 `ErrorWithCode`包含错误代码和错误消息。 例如，要筛选出特定错误，可以使用以下代码片段:

```typescript
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

## <a name="microsoft-graph-scenarios"></a>Microsoft Graph 方案

本部分为与 Microsoft Graph 相关的常见方案提供多个代码片段。 在这种情况下，用户可以使用不同端的不同权限调用 API， (前端/后端) 。

* 前端的用户委托权限 (使用 TeamsUserCredential) <details>
    <summary><b>在选项卡应用中使用图形 API</b></summary>

    此代码片段演示如何使用 `TeamsFx` 和 `createMicrosoftGraphClient` 从 Microsoft Graph 获取用户配置文件。 它还向你展示了如何捕获和解决 a `GraphError`.

    1. 导入所需的类。

    ```typescript
    import {
      createMicrosoftGraphClient,
      TeamsFx,
    } from "@microsoft/teamsfx";
    ```

    2. 用于 `TeamsFx.login()` 获取用户同意。

    ```typescript
    // Put these code in a call-to-action callback function to avoid browser blocking automatically showing up pop-ups.
    await teamsfx.login(["User.Read"]); // Login with scope
    ```

    3. 可以初始化 TeamsFx 实例和图形客户端，并从此客户端的 MS Graph 获取信息。

    ```typescript
    try {
      const teamsfx = new TeamsFx();
      const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
      const profile = await graphClient.api("/me").get();
    } catch (err: unknown) {
      // ErrorWithCode is handled by Graph client
      if (err instanceof GraphError && err.code?.includes(ErrorCode.UiRequiredError)) {
        // Need to show login button to ask for user consent.
      }
    }
    ```

    有关在选项卡应用中使用图形 API的示例的详细信息，请参阅 [hello-world-tab 示例](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/hello-world-tab)。

    </details>

    <details>
    <summary><b>与 Microsoft Graph 工具包集成</b></summary>

    [Microsoft Graph 工具包](https://aka.ms/mgt)库是由 Microsoft Graph 提供的各种身份验证提供程序和 UI 组件的集合。

    该 `@microsoft/mgt-teamsfx-provider` 包公开 `TeamsFxProvider` 类，该类使用 `TeamsFx` 类来登录用户并获取要与 Microsoft Graph 一起使用的令牌。

    1. 可以安装以下必需的包：

    ```bash
    npm install @microsoft/mgt-element @microsoft/mgt-teamsfx-provider @microsoft/teamsfx
    ```

    2. 在组件中初始化提供程序。

    ```typescript
     // Import the providers and credential at the top of the page
    import {Providers} from '@microsoft/mgt-element';
    import {TeamsFxProvider} from '@microsoft/mgt-teamsfx-provider';
    import {TeamsUserCredential} from "@microsoft/teamsfx";

    const scope = ["User.Read"];
    const teamsfx = new TeamsFx();
    const provider = new TeamsFxProvider(teamsfx, scope);
    Providers.globalProvider = provider;   
    ```

    3. 可以使用该 `teamsfx.login(scopes)` 方法获取所需的访问令牌。

    ```typescript
    // Put these code in a call-to-action callback function to avoid browser blocking automatically showing up pop-ups. 
    await teamsfx.login(this.scope);
    Providers.globalProvider.setState(ProviderState.SignedIn);
    ```

    4. 现在可以在 HTML 页面或方法中`render()`添加任何组件，并使用React使用`TeamsFx`上下文访问 Microsoft Graph。

    ```html
    <mgt-person query="me" view="threeLines"></mgt-person>
    ```

    ```typescript
    public render(): void {
    return (
        <div>
            <Person personQuery="me" view={PersonViewType.threelines}></Person>
        </div>
    );
    }    
    ```

    有关用于初始化 TeamsFx 提供程序的示例的详细信息，请参 [阅联系人导出程序示例](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/graph-toolkit-contact-exporter)。

    </details>

* 后端 (使用 OnBehalfOfUserCredential) 中的用户委托权限 <details>
    <summary><b>在机器人应用程序中使用图形 API</b></summary>

    此代码片段演示如何使用 `TeamsBotSsoPrompt` 设置对话框，然后登录以获取访问令牌。

    1. 初始化并添加 `TeamsBotSsoPrompt` 到对话集。

    ```typescript
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
    ```

    2. 开始对话框并登录。

    ```typescript
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

    有关在机器人应用程序中使用图形 API 的示例的详细信息，请参阅 [bot-sso 示例](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/bot-sso)。

    </details>

    <details>
    <summary><b>在消息扩展插件中使用图形 API</b></summary>

    此代码片段演示如何替代 `handleTeamsMessagingExtensionQuery` 扩展 `TeamsActivityHandler`，以及如何使用 `handleMessageExtensionQueryWithToken` TeamsFx sdk 提供的登录来获取访问令牌：

    ```typescript
    public async handleTeamsMessagingExtensionQuery(context: TurnContext, query: any): Promise<any> {
      return await handleMessageExtensionQueryWithToken(context, null, 'User.Read', 
        async (token: MessageExtensionTokenResponse) => {
          // ... continue to query with access token ...
        });
    }    
    ```

    有关在消息扩展插件中使用图形 API 的示例的详细信息，请参阅 [message-extension-sso-sample](https://aka.ms/teamsfx-me-sso-sample)。
    </details>

    <details>
    <summary><b>在命令机器人中使用图形 API</b></summary>

    此代码片段演示如何实现 `TeamsFxBotSsoCommandHandler` 命令机器人调用 Microsoft API。

    ```typescript
    import { Activity, TurnContext } from "botbuilder";
    import {
      CommandMessage,
      TriggerPatterns,
      TeamsFx,
      createMicrosoftGraphClient,
      TeamsFxBotSsoCommandHandler,
      TeamsBotSsoPromptTokenResponse,
    } from "@microsoft/teamsfx";

    export class ProfileSsoCommandHandler implements TeamsFxBotSsoCommandHandler {
      triggerPatterns: TriggerPatterns = "profile";

      async handleCommandReceived(
        context: TurnContext,
        message: CommandMessage,
        tokenResponse: TeamsBotSsoPromptTokenResponse,
      ): Promise<string | Partial<Activity> | void> {
        // Init TeamsFx instance with SSO token
        const teamsfx = new TeamsFx().setSsoToken(tokenResponse.ssoToken);

        // Add scope for your Azure AD app. For example: Mail.Read, etc.
        const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]);
      
        // Call graph api use `graph` instance to get user profile information
        const me = await graphClient.api("/me").get();

        if (me) {
          // Bot will send the user profile info to user
          return `Your command is '${message.text}' and you're logged in as ${me.displayName}`;
        } else {
          return "Could not retrieve profile information from Microsoft Graph.";
        }
      }
    }    
    ```

    有关如何在命令机器人中使用此类的详细信息， [请参阅向 Teams 应用添加单一登录](add-single-sign-on.md)。 此外还有一个 [command-bot-with-sso](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/command-bot-with-sso) 示例项目，你可以尝试使用 sso 命令机器人。

    </details>

    <details>
    <summary><b>在选项卡应用中调用 Azure 函数：代表流</b></summary>

    此代码片段演示如何使用`CreateApiClient`或`axios`库调用 Azure 函数，以及如何在 Azure 函数中调用图形 API以获取用户配置文件。

    1. 可以使用 TeamsFx sdk 提供的调用 `CreateApiClient` Azure 函数：

    ```typescript
    async function callFunction(teamsfx?: TeamsFx) {
      const teamsfx = new TeamsFx();

      // Get the credential.
      const credential = teamsfx.getCredential(); 
      // Create an API client by providing the token and endpoint.
      const apiClient = CreateApiClient(
        teamsfx.getConfig("YOUR_API_ENDPOINT"), // Create an API Client that uses SSO token to authenticate requests
        new BearerTokenAuthProvider(async () =>  (await credential.getToken(""))!.token) // Call API hosted in Azure Functions on behalf of user to inject token to request header
      );

      // Send a GET request to "RELATIVE_API_PATH", "/api/functionName" for example.
      const response = await apiClient.get("RELATIVE_API_PATH");
      return response.data;
    }    
    ```

    还可以使用 `axios` 库调用 Azure 函数。

    ```typescript
    async function callFunction(teamsfx?: TeamsFx) {
      const accessToken = await teamsfx.getCredential().getToken(""); // Get SSO token 
      // teamsfx.getConfig("apiEndpoint") will read REACT_APP_FUNC_ENDPOINT environment variable 
      const endpoint = teamsfx.getConfig("apiEndpoint");
      const response = await axios.default.get(endpoint + "/api/" + functionName, {
        headers: {
          authorization: "Bearer " + accessToken.token,
        },
      });
      return response.data;
    }    
    ```

    2. 在 Azure 函数中代表用户调用图形 API作为响应。

    ```typescript
    export default async function run(
      context: Context,
      req: HttpRequest,
      teamsfxContext: TeamsfxContext
    ): Promise<Response> {
      const res: Response = { status: 200, body: {},};
      // ...
      teamsfx = new TeamsFx().setSsoToken(accessToken);
      // Query user's information from the access token.
      try {
        const currentUser: UserInfo = await teamsfx.getUserInfo();
        if (currentUser && currentUser.displayName) {
          res.body.userInfoMessage = `User display name is ${currentUser.displayName}.`;
        } else {
          res.body.userInfoMessage = "No user information was found in access token.";
        }
      } catch (e) {
      }
      // Create a graph client to access user's Microsoft 365 data after user has consented.
      try {
        const graphClient: Client = createMicrosoftGraphClient(teamsfx, [".default"]);
        const profile: any = await graphClient.api("/me").get();
        res.body.graphClientMessage = profile;
      } catch (e) {
      }
      return res;
    }    
    ```

    有关在机器人应用程序中使用图形 API 的示例的详细信息，  [请参阅 hello-world-tab-with-backend 示例](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/hello-world-tab-with-backend)。

    </details>

* 后端中的应用程序权限 <details>
    <summary><b>在 Azure Function 中使用基于证书的身份验证</b></summary>

    此代码片段演示如何使用基于证书的应用程序权限获取可用于调用图形 API的令牌。

    1. 你可以 `authConfig` 通过提供一个 `PEM-encoded key certificate`。

    ```typescript
    const authConfig = {
      clientId: process.env.M365_CLIENT_ID,
      certificateContent: "The content of a PEM-encoded public/private key certificate",
      authorityHost: process.env.M365_AUTHORITY_HOST,
      tenantId: process.env.M365_TENANT_ID,
    };    
    ```

    2. 可以使用该 `authConfig` 令牌获取令牌。

    ```typescript
    const teamsfx = new TeamsFx(IdentityType.App);
    teamsfx.setCustomeConfig(authConfig);
    const token = teamsfx.getCredential().getToken();    
    ```

    </details>

    <details>
    <summary><b>在 Azure 函数中使用客户端机密身份验证</b></summary>

    此代码片段演示如何使用客户端机密应用程序权限获取可用于调用图形 API的令牌。

    1. 你可以 `authConfig` 通过提供一个 `client secret`。

    ```typescript
    const authConfig = {
      clientId: process.env.M365_CLIENT_ID,
      clientSecret: process.env.M365_CLIENT_SECRET,
      authorityHost: process.env.M365_AUTHORITY_HOST,
      tenantId: process.env.M365_TENANT_ID,
    };    
    ```

    2. 可以使用该 `authConfig` 令牌获取令牌。

    ```typescript
    const teamsfx = new TeamsFx(IdentityType.App);
    teamsfx.setCustomeConfig(authConfig);
    const token = teamsfx.getCredential().getToken();    
    ```

    有关在机器人应用程序中使用图形 API 的示例的详细信息，请参阅 [hello-world-tab-with-backend 示例](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/hello-world-tab-with-backend)。

    </details>

## <a name="other-scenarios"></a>其他情景

本部分为其他与 Microsoft Graph 相关的方案提供多个代码片段。 可以在 Bot 或 Azure Function 中创建 API 客户端，并在 Azure Function 中访问 SQL 数据库。

  <details>
  <summary><b>创建 API 客户端以调用机器人或 Azure 函数中的现有 API</b></summary>

  此代码片段演示如何调 `ApiKeyProvider`用机器人中的现有 API。

  ```typescript
  const teamsfx = new TeamsFx();

  // Create an API Key auth provider. In addition to APiKeyProvider, following auth providers are also available:
  // BearerTokenAuthProvider, BasicAuthProvider, CertificateAuthProvider.
  const authProvider = new ApiKeyProvider("YOUR_API_KEY_NAME",
    teamsfx.getConfig("YOUR_API_KEY_VALUE"), // This reads the value of YOUR_API_KEY_VALUE environment variable.
    ApiKeyLocation.Header
  );

  // Create an API client using above auth provider.
  // You can also implement AuthProvider interface and use it here.
  const apiClient = createApiClient(
    teamsfx.getConfig("YOUR_API_ENDPOINT"), // This reads YOUR_API_ENDPOINT environment variable.
    authProvider
  );

  // Send a GET request to "RELATIVE_API_PATH", "/api/apiname" for example.
  const response = await apiClient.get("RELATIVE_API_PATH");  
  ```

  </details>

  <details>
  <summary><b>访问 Azure Function 中的 SQL 数据库</b></summary>

  使用 `tedious` 库访问 SQL 并使用 `DefaultTediousConnectionConfiguration` 它来管理身份验证。 还可以根据结果撰写其他 SQL 库的 `sqlConnectionConfig.getConfig()`连接配置。

  1. 设置连接配置。

  ```typescript
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
  const config2 = await getTediousConnectionConfig(teamsfx, "your database name");  
  ```

  2. 连接到数据库。

  ```typescript
  const connection = new Connection(config);
  connection.on("connect", (error) => {
    if (error) {
      console.log(error);
    }
  });  
  ```

  > [!NOTE]
  > 有关在 Azure 函数中访问 SQL 数据库的示例的详细信息，请参阅 [share-now 示例](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/share-now)。

</details>

## <a name="advanced-customization"></a>高级自定义

### <a name="configure-log"></a>配置日志

使用此库时，可以设置客户日志级别并重定向输出。

> [!NOTE]
> 日志记录默认处于禁用状态，可以设置日志级别以启用。

#### <a name="enable-log-by-setting-log-level"></a>设置日志级别以启用日志

设置日志级别时，将启用日志记录。 默认情况下，它将日志信息打印到控制台。

使用以下代码片段设置日志级别:

```typescript
// Only need the warning and error messages.
setLogLevel(LogLevel.Warn);
```

> [!NOTE]
> 可以设置自定义记录器或日志函数，从而重定向日志输出。

#### <a name="redirect-by-setting-custom-logger"></a>设置自定义记录器以重定向

```typescript
setLogLevel(LogLevel.Info);
// Set another logger if you want to redirect to Application Insights in Azure Function
setLogger(context.log);
```

#### <a name="redirect-by-setting-custom-log-function"></a>设置自定义日志函数以重定向

```typescript
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

> [!NOTE]
> 如果设置了自定义记录器，则日志函数不会生效。

## <a name="upgrade-latest-sdk-version"></a>升级最新的 SDK 版本

如果使用的是 SDK 版本， `loadConfiguration()`可以按照以下步骤升级到最新的 SDK 版本：

1. 删除 `loadConfiguration()` 并使用 `new TeamsFx(IdentityType.User, { ...customConfig })` 传递自定义设置
2. 将 `new TeamsUserCredential()` 替换为 `new TeamsFx()`。
3. 将 `new M365TenantCredential()` 替换为 `new TeamsFx(IdentityType.App)`。
4. 将 `new OnBehalfOfUserCredential(ssoToken)` 替换为 `new TeamsFx().setSsoToken(ssoToken)`。
5. 传递帮助程序函数的 `TeamsFx` 实例以替换凭据实例。

## <a name="next-step"></a>后续步骤

有关如何使用 TeamsFx SDK [示例](https://github.com/OfficeDev/TeamsFx-Samples) 项目的详细示例。

## <a name="see-also"></a>另请参阅

[Microsoft TeamsFx 示例库](https://github.com/OfficeDev/TeamsFx-Samples)。
