---
title: 向Teams应用添加单一登录
author: zyxiaoyuer
description: 描述添加单一登录Teams Toolkit
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/20/2022
ms.openlocfilehash: db676795e394856f6e787086cae654efad79172a
ms.sourcegitcommit: 80edf3c964bb47a2ee13f9eda4334ad19e21f331
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2022
ms.locfileid: "65655050"
---
# <a name="add-single-sign-on-experience"></a>添加单一登录体验

Microsoft Teams为应用程序提供单一登录函数，以获取登录Teams用户令牌以访问 Microsoft Graph 和其他 API。 Teams Toolkit通过抽象一些简单的 API 背后的一些 Azure AD 流和集成来促进交互。 这样就可以轻松地将单一登录 (SSO) 功能添加到Teams应用程序。

对于在聊天、团队或频道中与用户交互的应用程序，SSO 将显示为自适应卡片，用户可以与该卡进行交互以调用 Azure AD 同意流。

## <a name="enable-sso-support"></a>启用 SSO 支持

Teams Toolkit可帮助你将 SSO 添加到以下Teams功能：

* Tab
* Bot
* 通知机器人：恢复服务器
* 命令机器人

### <a name="add-sso-using-visual-studio-code"></a>使用Visual Studio Code添加 SSO

以下步骤可帮助你在Visual Studio Code中使用Teams Toolkit添加 SSO

1. 打开 **Microsoft Visual Studio Code**。
2. 从左侧导航栏中选择:::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/teams-toolkit-sidebar-icon.png" alt-text="Teams Toolkit sso 添加边栏":::。
3. 选择 **“开发**”下 **的“添加功能**”。

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/sso-add features.png" alt-text="sso 添加功能":::

    * 还可以打开命令面板并选择 **Teams：添加功能**

4. 选择 **单一登录**。

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/sso-select features.png" alt-text="sso select":::

### <a name="add-sso-using-teamsfx-cli"></a>使用 TeamsFx CLI 添加 SSO

可以在 **项目根目录** 中运行`teamsfx add sso`命令

> [!Note]
> 该功能为所有现有的适用功能启用 SSO。 如果稍后将功能添加到项目，请按照相同的步骤启用 SSO。

## <a name="customize-your-project-using-teams-toolkit"></a>使用Teams Toolkit自定义项目

下表列出了Teams Toolkit对项目所做的更改：

   |**类型**|**文件**|**用途**|
   |--------|--------|-----------|
   |创建|`aad.template.json` 下 `template/appPackage`|Azure AD 应用程序清单表示 Azure AD 应用。 `template/appPackage` 有助于在本地调试或预配阶段注册 Azure AD 应用。|
   |修改|`manifest.template.json` 下 `template/appPackage`|对象`webApplicationInfo`将添加到Teams应用清单模板中。 Teams需要此字段才能启用 SSO。 触发本地调试或预配时，更改生效。|
   |创建|`auth/tab`|在此路径中为选项卡项目生成引用代码、身份验证重定向页面和 `README.md` 文件。|
   |创建|`auth/bot`|在此路径中为机器人项目生成引用代码、身份验证重定向页面和 `README.md` 文件。|

> [!Note]
> 通过添加 SSO，Teams Toolkit在触发本地调试之前不会更改云中的任何内容。 更新代码以确保 SSO 在项目中正常工作。

## <a name="update-your-application-to-use-sso"></a>更新应用程序以使用 SSO

以下步骤可帮助你在应用程序中启用 SSO。

> [!NOTE]
> 这些更改基于我们基架的模板。

---
<br>
<br><details>
<summary><b>Tab 项目 </b></summary>

1. 将文件夹中的 `auth/public` **复制`auth-start.html`到 `tabs/public/``auth-end.htm`。 Teams Toolkit在 Azure AD 中为 Azure AD 的重定向流注册这两个终结点。

2. 将文件夹复制`sso`到`tabs/src/sso/`下`auth/tab`方 。

    * `InitTeamsFx`：该文件实现一个函数，该函数初始化 TeamsFx SDK 并在初始化 SDK 后打开 `GetUserProfile` 组件

    * `GetUserProfile`：该文件实现调用 Microsoft 图形 API以获取用户信息的函数

3. 在 `npm install @microsoft/teamsfx-react` .`tabs/`

4. 添加以下行以导`InitTeamsFx`入`tabs/src/components/sample/Welcome.tsx`：

    ```Bash

    import { InitTeamsFx } from "../../sso/InitTeamsFx";

    ```

5. 将以下行替换为： `<AddSSO />` 用 `<InitTeamsFx />` 组件替换 `AddSso` 组件 `InitTeamsFx` 。

</details>
<details>
<summary><b>机器人项目 </b></summary>

1. 将文件夹复制 `auth/bot/public` 到 `bot/src`. 这两个文件夹包含用于身份验证重定向的 HTML 页面，需要修改 `bot/src/index` 文件以将路由添加到这些页面。

2. 将文件夹复制 `auth/bot/sso` 到 `bot/src`. 这两个文件夹包含三个文件作为 SSO 实现的参考：

    * `showUserInfo`：它实现一个函数来获取具有 SSO 令牌的用户信息。 可以按照此操作创建自己的需要 SSO 令牌的方法。

    * `ssoDialog`：它创建一个用于 SSO 的 [ComponentDialog](/javascript/api/botbuilder-dialogs/componentdialog?view=botbuilder-ts-latest&preserve-view=true) 。

    * `teamsSsoBot`：它创建一个 [TeamsActivityHandler](/javascript/api/botbuilder/teamsactivityhandler?view=botbuilder-ts-latest&preserve-view=true) ，并 `ssoDialog` 将其添加 `showUserInfo` 为可触发的命令。

3. 按照代码示例操作，在此文件中注册自己的命令 `addCommand` (可选) 。

4. 在 `npm install isomorphic-fetch` .`bot/`

5. `bot/`在 package.json 中执行`npm install copyfiles`并替换以下行：
  
   ```JSON

   "build": "tsc --build",

    ```

   具有  的 

   ```JSON

   "build": "tsc --build && copyfiles public/*.html lib/",

   ```

   生成此机器人项目时，将复制用于身份验证重定向的 HTML 页面。

6. 添加以下文件后，需要在文件中`bot/src/index`创建一个新`teamsSsoBot`实例。 替换以下代码：

   ```Bash
  
   // Process Teams activity with Bot Framework.
   server.post("/api/messages", async (req, res) => {
   await commandBot.requestHandler(req, res);
   });  

   ```

   具有  的 

   ```Bash

   const handler = new TeamsSsoBot();
   // Process Teams activity with Bot Framework.
   server.post("/api/messages", async (req, res) => {
       await commandBot.requestHandler(req, res, async (context)=> {
           await handler.run(context);
       });
   });

   ```

7. 在文件中 `bot/src/index` 添加 HTML 路由：

   ```Bash

   server.get(
       "/auth-*.html",
       restify.plugins.serveStatic({
           directory: path.join(__dirname, "public"),
       })
   );

   ```

8. 添加以下行以 `bot/src/index` 进行导 `teamsSsoBot` 入，并 `path`执行以下操作：

   ```Bash

   // For ts:
   import { TeamsSsoBot } from "./sso/teamsSsoBot";
   const path = require("path");

   // For js:
   const { TeamsSsoBot } = require("./sso/teamsSsoBot");
   const path = require("path");

   ```

9. 在Teams应用清单中注册命令。 在机器人中`command``commandLists`打开`templates/appPackage/manifest.template.json`并添加以下行：

   ```JSON

   {
       "title": "show",
       "description": "Show user profile using Single Sign On feature"
   }

   ```
</details>
<details>
<summary><b>向机器人添加新命令 </b></summary>

> [!NOTE]
> 目前，这些说明适用于 `command bot`。 如果从一个 `bot`示例开始，请参阅 [bot-sso 示例](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2/bot-sso)。

在项目中添加 SSO 后，以下步骤可帮助你添加新命令：

1. 在下 (`todo.ts`或`todo.js`) `bot/src/`创建新文件，并添加自己的业务逻辑来调用图形 API：

# <a name="typescript"></a>[TypeScript](#tab/typescript)

   ```typescript
   // for TypeScript:
export async function showUserImage(
    context: TurnContext,
    ssoToken: string,
    param: any[]
): Promise<DialogTurnResult> {
    await context.sendActivity("Retrieving user photo from Microsoft Graph ...");

    // Init TeamsFx instance with SSO token
    const teamsfx = new TeamsFx().setSsoToken(ssoToken);

    // Update scope here. For example: Mail.Read, etc.
    const graphClient = createMicrosoftGraphClient(teamsfx, param[0]);
    
    // You can add following code to get your photo:
    // let photoUrl = "";
    // try {
    //   const photo = await graphClient.api("/me/photo/$value").get();
    //   photoUrl = URL.createObjectURL(photo);
    // } catch {
    //   // Could not fetch photo from user's profile, return empty string as placeholder.
    // }
    // if (photoUrl) {
    //   await context.sendActivity(
    //     `You can find your photo here: ${photoUrl}`
    //   );
    // } else {
    //   await context.sendActivity("Could not retrieve your photo from Microsoft Graph. Please make sure you have uploaded your photo.");
    // }

    return;
}  
   ```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

   ```javaScript
   // for JavaScript:
export async function showUserImage(context, ssoToken, param) {
    await context.sendActivity("Retrieving user photo from Microsoft Graph ...");

    // Init TeamsFx instance with SSO token
    const teamsfx = new TeamsFx().setSsoToken(ssoToken);

    // Update scope here. For example: Mail.Read, etc.
    const graphClient = createMicrosoftGraphClient(teamsfx, param[0]);
    
    // You can add following code to get your photo:
    // let photoUrl = "";
    // try {
    //   const photo = await graphClient.api("/me/photo/$value").get();
    //   photoUrl = URL.createObjectURL(photo);
    // } catch {
    //   // Could not fetch photo from user's profile, return empty string as placeholder.
    // }
    // if (photoUrl) {
    //   await context.sendActivity(
    //     `You can find your photo here: ${photoUrl}`
    //   );
    // } else {
    //   await context.sendActivity("Could not retrieve your photo from Microsoft Graph. Please make sure you have uploaded your photo.");
    // }

    return;
}
   ```

---

2. 注册新命令

   * 使用以下行进行新的命令注册，如下所示`addCommand``teamsSsoBot`：

   ```bash

   this.dialog.addCommand("ShowUserProfile", "show", showUserInfo);

   ```

   * 在上述行后添加以下行以注册新命令 `photo` 并挂接上面添加的方法 `showUserImage` ：

   ```bash

   // As shown here, you can add your own parameter into the `showUserImage` method
   // You can also use regular expression for the command here
   const scope = ["User.Read"];
   this.dialog.addCommand("ShowUserPhoto", new RegExp("photo\s*.*"), showUserImage, scope);

   ```

3. 在Teams应用清单中注册命令。 在机器人中`command``commandLists`打开`templates/appPackage/manifest.template.json`并添加以下行：

   ```JSON

   {
       "title": "photo",
       "description": "Show user photo using Single Sign On feature"
   }

   ```
</details>
<br>

## <a name="debug-your-application"></a>调试应用程序

按 F5 调试应用程序。 Teams Toolkit使用 Azure AD 清单文件注册适用于 SSO 的 Azure AD 应用程序。 有关Teams Toolkit本地调试功能，请参阅[本地调试Teams应用](debug-local.md)。

## <a name="customize-azure-ad-application-registration"></a>自定义 Azure AD 应用程序注册

[使用 Azure AD 应用清单](/azure/active-directory/develop/reference-app-manifest)可以自定义应用程序注册的各个方面。 可以根据需要更新清单。 如果需要包含其他 API 权限来访问所需的 API，请参阅 [API 访问所需 API 的权](https://github.com/OfficeDev/TeamsFx/wiki/#customize-aad-manifest-template)限。
若要在 Azure 门户中查看 Azure AD 应用程序，请参[阅Azure 门户中的 Azure AD 应用程序。](https://github.com/OfficeDev/TeamsFx/wiki/Manage-AAD-application-in-Teams-Toolkit#How-to-view-the-AAD-app-on-the-Azure-portal) 

## <a name="sso-authentication-concepts"></a>SSO 身份验证概念

以下概念可帮助你进行 SSO 身份验证：

### <a name="working-of-sso-in-teams"></a>在 Teams 中处理 SSO

Microsoft Azure Active Directory (Azure AD 中的单一登录 (SSO) 身份验证) 以无提示方式刷新身份验证令牌，以尽量减少用户输入登录凭据所需的次数。 如果用户同意使用应用，则他们不必在另一台设备上再次同意，因为他们会自动登录。

Teams选项卡和机器人具有类似的 SSO 支持流，有关详细信息，请参阅：

1. [在 Tabs 中单一登录 (SSO) 身份验证](../tabs/how-to/authentication/auth-aad-sso.md)
2. [机器人中的单一登录 (SSO) 身份验证](../bots/how-to/authentication/auth-aad-sso-bots.md)

### <a name="simplified-sso-with-teamsfx"></a>使用 TeamsFx 简化的 SSO

TeamsFx 使用 Teams SSO 并将云资源向下访问到零配置的单行语句，从而帮助减少开发人员任务。

使用 TeamsFx SDK，可以使用凭据以简化的方式编写用户身份验证代码：

1. 浏览器环境中的用户标识：`TeamsUserCredential`表示Teams当前用户的标识。
2. Node.js环境中的用户标识：`OnBehalfOfUserCredentail`使用代理流和Teams SSO 令牌。
3. Node.js环境中的应用程序标识： `AppCredential` 表示应用程序标识。

有关 TeamsFx SDK 的详细信息，请参阅：

* [TeamsFx SDK](TeamsFx-SDK.md) 或 [API 参考](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true)
* [Microsoft Teams Framework (TeamsFx) 示例库](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2)

## <a name="see-also"></a>另请参阅

* [准备帐户以生成 Teams 应用](accounts.md)
