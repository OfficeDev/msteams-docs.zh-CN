---
title: 向 Teams 应用添加单一登录
author: zyxiaoyuer
description: 在本模块中，了解如何 (Teams 工具包的 SSO) 添加单一登录、启用 SSO 支持、更新应用程序以使用 SSO
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/20/2022
ms.openlocfilehash: 9c221b0903d4541c4b0601e14ea347680140dfb9
ms.sourcegitcommit: 3aaccc48906fc6f6fbf79916af5664bf55537250
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2022
ms.locfileid: "68295961"
---
# <a name="add-single-sign-on-to-teams-app"></a>向 Teams 应用添加单一登录

Microsoft Teams 为应用程序提供单一登录函数，以获取登录 Teams 用户令牌以访问 Microsoft Graph 和其他 API。 Teams 工具包通过抽象某些简单 API 背后的一些 Azure AD 流和集成来促进交互。 这使你可以轻松地将单一登录 (SSO) 功能添加到 Teams 应用程序。

对于在聊天、团队或频道中与用户交互的应用程序，SSO 清单作为自适应卡片，用户可以与该卡片交互以调用 Azure AD 同意流。

## <a name="enable-sso-support"></a>启用 SSO 支持

Teams 工具包可帮助你将 SSO 添加到以下 Teams 功能：

* Tab
* Bot
* 通知机器人：恢复服务器
* 命令机器人

### <a name="add-sso-using-visual-studio-code"></a>使用Visual Studio Code添加 SSO

以下步骤可帮助你在Visual Studio Code中使用 Teams 工具包添加 SSO

1. 打开 **Microsoft Visual Studio Code**。
2. 从左侧导航栏中选择 Teams 工具包 :::image type="content" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png" alt-text="sso 添加边栏"::: 。
3. 选择 **“开发**”下 **的“添加功能**”。

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/sso-add features.png" alt-text="sso 添加功能":::

    * 还可以打开命令面板并选择 **Teams：添加功能**

4. 选择 **单一登录**。

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/sso-select features.png" alt-text="sso select":::

### <a name="add-sso-using-teamsfx-cli"></a>使用 TeamsFx CLI 添加 SSO

可以在 **项目根目录** 中运行`teamsfx add sso`命令

> [!Note]
> 该功能为所有现有的适用功能启用 SSO。 如果稍后将功能添加到项目，请按照相同的步骤启用 SSO。

## <a name="customize-your-project-using-teams-toolkit"></a>使用 Teams 工具包自定义项目

下表列出了 Teams 工具包对项目所做的更改：

   |**类型**|**文件**|**用途**|
   |--------|--------|-----------|
   |创建|`aad.template.json` 下 `template/appPackage`|Azure AD 应用程序清单表示 Azure AD 应用。 `template/appPackage` 有助于在本地调试或预配阶段注册 Azure AD 应用。|
   |修改|`manifest.template.json` 下 `template/appPackage`|对象 `webApplicationInfo` 将添加到 Teams 应用清单模板中。 Teams 需要此字段才能启用 SSO。 触发本地调试或预配时，更改生效。|
   |创建|`auth/tab`|在此路径中为选项卡项目生成引用代码、身份验证重定向页面和 `README.md` 文件。|
   |创建|`auth/bot`|在此路径中为机器人项目生成引用代码、身份验证重定向页面和 `README.md` 文件。|

> [!Note]
> 通过添加 SSO，Teams 工具包在触发本地调试之前不会更改云中的任何内容。 更新代码以确保 SSO 在项目中正常工作。

## <a name="update-your-application-to-use-sso"></a>更新应用程序以使用 SSO

以下步骤可帮助你在应用程序中启用 SSO：

> [!NOTE]
> 这些更改基于我们基架的模板。

---
<br>
<br><details>
<summary><b>Tab 项目 </b></summary>

1. 将文件夹中的 `auth/public` **复制`auth-start.html`到 `tabs/public/``auth-end.htm`。 Teams 工具包在 Azure AD 中为 Azure AD 的重定向流注册这两个终结点。

2. 将文件夹复制`sso`到`tabs/src/sso/`下`auth/tab`方 。

    * `InitTeamsFx`：该文件实现一个函数，该函数初始化 TeamsFx SDK 并在初始化 SDK 后打开 `GetUserProfile` 组件

    * `GetUserProfile`：该文件实现调用 Microsoft 图形 API以获取用户信息的函数

3. 在 `npm install @microsoft/teamsfx-react` .`tabs/`

4. 添加以下行以导`InitTeamsFx`入`tabs/src/components/sample/Welcome.tsx`：

    ```Bash

    import { InitTeamsFx } from "../../sso/InitTeamsFx";

    ```

5. 将以下行：

   `<AddSSO />` 用于 `<InitTeamsFx />` 将组件替换 `AddSso` 为 `InitTeamsFx` 组件。

</details>
<details>
<summary><b>机器人项目 </b></summary>

#### <a name="set-up-the-azure-ad-redirects"></a>设置 Azure AD 重定向

1. `auth/bot/public`将文件夹移动到 `bot/src`. 此文件夹包含机器人应用程序托管的 HTML 页面。 使用 Azure AD 启动单一登录流时，它会将用户重定向到 HTML 页面。
1. 修改你 `bot/src/index` 以将适当的 `restify` 路由添加到 HTML 页面。

    ```ts
    const path = require("path");

    server.get(
        "/auth-*.html",
        restify.plugins.serveStatic({
            directory: path.join(__dirname, "public"),
        })
    );
    ```

#### <a name="update-your-app"></a>更新应用

SSO 命令处理程序 `ProfileSsoCommandHandler` 使用 Azure AD 令牌调用 Microsoft Graph。 此令牌是使用登录的 Teams 用户令牌获取的。 如果需要，该流将汇集在显示同意对话框的对话框中。

1. 将文件夹下`auth/bot/sso`的文件移`profileSsoCommandHandler`到 `bot/src`. `ProfileSsoCommandHandler` 类是一个 SSO 命令处理程序，用于获取具有 SSO 令牌的用户信息、遵循此方法并创建自己的 SSO 命令处理程序。
1. 打开 `package.json` 文件并确保 teamsfx SDK 版本>= 1.2.0
1. 在 `npm install isomorphic-fetch --save` 文件夹中 `bot` 执行命令。
1. 对于 ts 脚本，请在文件夹中`bot`执行`npm install copyfiles --save-dev`命令，并替换以下行`package.json`：

    ```json
    "build": "tsc --build && shx cp -r ./src/adaptiveCards ./lib/src",
    ```

    具有  的 

    ```json
    "build": "tsc --build && shx cp -r ./src/adaptiveCards ./lib/src && copyfiles src/public/*.html lib/",
    ```

    这将复制生成机器人项目时用于身份验证重定向的 HTML 页面。

1. 若要使 SSO 同意流正常工作，请在文件中 `bot/src/index` 替换以下代码：

    ```ts
    server.post("/api/messages", async (req, res) => {
        await commandBot.requestHandler(req, res);
    });
    ```

    具有  的 

    ```ts
    server.post("/api/messages", async (req, res) => {
        await commandBot.requestHandler(req, res).catch((err) => {
            // Error message including "412" means it is waiting for user's consent, which is a normal process of SSO, sholdn't throw this error.
            if (!err.message.includes("412")) {
                throw err;
            }
        });
    });
    ```

1. 替换用于 `ConversationBot` 添加 SSO 配置和 SSO 命令处理程序的实 `bot/src/internal/initialize` 例选项：

    ```ts
    export const commandBot = new ConversationBot({
        ...
        command: {
            enabled: true,
            commands: [new HelloWorldCommandHandler()],
        },
    });
    ```

    具有  的 

    ```ts
    import { ProfileSsoCommandHandler } from "../profileSsoCommandHandler";

    export const commandBot = new ConversationBot({
        ...
        // To learn more about ssoConfig, please refer teamsfx sdk document: https://docs.microsoft.com/microsoftteams/platform/toolkit/teamsfx-sdk
        ssoConfig: {
            aad :{
                scopes:["User.Read"],
            },
        },
        command: {
            enabled: true,
            commands: [new HelloWorldCommandHandler() ],
            ssoCommands: [new ProfileSsoCommandHandler()],
        },
    });
    ```

1. 在 Teams 应用清单中注册命令。 在机器人中`commands``commandLists`打开`templates/appPackage/manifest.template.json`并添加以下行：

    ```json
    {
        "title": "profile",
        "description": "Show user profile using Single Sign On feature"
    }
    ```

#### <a name="add-a-new-sso-command-to-the-bot-optional"></a>将新的 SSO 命令添加到机器人 (可选) 

在项目中成功添加 SSO 后，可以添加新的 SSO 命令。

1. 创建新文件（例如`photoSsoCommandHandler.ts`或`photoSsoCommandHandler.js`加入`bot/src/`）并添加自己的 SSO 命令处理程序来调用图形 API：

    ```TypeScript
    // for TypeScript:
    import { Activity, TurnContext, ActivityTypes } from "botbuilder";
    import "isomorphic-fetch";
    import {
        CommandMessage,
        TriggerPatterns,
        TeamsFx,
        createMicrosoftGraphClient,
        TeamsFxBotSsoCommandHandler,
        TeamsBotSsoPromptTokenResponse,
    } from "@microsoft/teamsfx";

    export class PhotoSsoCommandHandler implements TeamsFxBotSsoCommandHandler {
        triggerPatterns: TriggerPatterns = "photo";

        async handleCommandReceived(
            context: TurnContext,
            message: CommandMessage,
            tokenResponse: TeamsBotSsoPromptTokenResponse,
        ): Promise<string | Partial<Activity> | void> {
            await context.sendActivity("Retrieving user information from Microsoft Graph ...");

            const teamsfx = new TeamsFx().setSsoToken(tokenResponse.ssoToken);

            const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]);

            let photoUrl = "";
            try {
                const photo = await graphClient.api("/me/photo/$value").get();
                const arrayBuffer = await photo.arrayBuffer();
                const buffer=Buffer.from(arrayBuffer, 'binary');
                photoUrl = "data:image/png;base64," + buffer.toString("base64");
            } catch {
                // Could not fetch photo from user's profile, return empty string as placeholder.
            }
            if (photoUrl) {
                const photoMessage: Partial<Activity> = {
                    type: ActivityTypes.Message, 
                    text: 'This is your photo:', 
                    attachments: [
                        {
                            name: 'photo.png',
                            contentType: 'image/png',
                            contentUrl: photoUrl
                        }
                    ]
                };
                return photoMessage;
            } else {
                return "Could not retrieve your photo from Microsoft Graph. Please make sure you have uploaded your photo.";
            }
        }
    }
    ```

    ```javascript
    // for JavaScript:
    const { ActivityTypes } = require("botbuilder");
    require("isomorphic-fetch");
    const { createMicrosoftGraphClient, TeamsFx } = require("@microsoft/teamsfx");

    class PhotoSsoCommandHandler {
        triggerPatterns = "photo";

        async handleCommandReceived(context, message, tokenResponse) {
            await context.sendActivity("Retrieving user information from Microsoft Graph ...");

            const teamsfx = new TeamsFx().setSsoToken(tokenResponse.ssoToken);

            const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]);
        
            let photoUrl = "";
            try {
                const photo = await graphClient.api("/me/photo/$value").get();
                const arrayBuffer = await photo.arrayBuffer();
                const buffer=Buffer.from(arrayBuffer, 'binary');
                photoUrl = "data:image/png;base64," + buffer.toString("base64");
            } catch {
            // Could not fetch photo from user's profile, return empty string as placeholder.
            }
            if (photoUrl) {
                const photoMessage = {
                    type: ActivityTypes.Message, 
                    text: 'This is your photo:', 
                    attachments: [
                        {
                            name: 'photo.png',
                            contentType: 'image/png',
                            contentUrl: photoUrl
                        }
                    ]
                };
                return photoMessage;
            } else {
                return "Could not retrieve your photo from Microsoft Graph. Please make sure you have uploaded your photo.";
            }
        }
    }

    module.exports = {
        PhotoSsoCommandHandler,
    };

    ```

1. 将实例添加 `PhotoSsoCommandHandler` 到 `ssoCommands` 数组中 `bot/src/internal/initialize.ts`：

    ```ts
    // for TypeScript:
    import { PhotoSsoCommandHandler } from "../photoSsoCommandHandler";

    export const commandBot = new ConversationBot({
        ...
        command: {
            ...
            ssoCommands: [new ProfileSsoCommandHandler(), new PhotoSsoCommandHandler()],
        },
    });
    ```

    ```javascript
    // for JavaScript:
    ...
    const { PhotoSsoCommandHandler } = require("../photoSsoCommandHandler");

    const commandBot = new ConversationBot({
        ...
        command: {
            ...
            ssoCommands: [new ProfileSsoCommandHandler(), new PhotoSsoCommandHandler()]
        },
    });
    ...

    ```

1. 在 Teams 应用清单中注册命令。 在机器人中`commands``commandLists`打开`templates/appPackage/manifest.template.json`并添加以下行：

    ```JSON

    {
        "title": "photo",
        "description": "Show user photo using Single Sign On feature"
    }

    ```

</details>
<br>

## <a name="debug-your-application"></a>调试应用程序

按 F5 调试应用程序。 Teams 工具包使用 Azure AD 清单文件注册适用于 SSO 的 Azure AD 应用程序。 有关 Teams 工具包本地调试功能，请参阅 [本地调试 Teams 应用](debug-local.md)。

## <a name="customize-azure-ad-application-registration"></a>自定义 Azure AD 应用程序注册

[使用 Azure AD 应用清单](/azure/active-directory/develop/reference-app-manifest)可以自定义应用程序注册的各个方面。 可以根据需要更新清单。 如果需要包含更多 API 权限来访问所需的 API，请参阅 [API 访问所需 API 的](https://github.com/OfficeDev/TeamsFx/wiki/#customize-aad-manifest-template)权限。
若要在Azure 门户中查看 Azure AD 应用程序，请参[阅Azure 门户中的查看 Azure AD 应用程序](https://github.com/OfficeDev/TeamsFx/wiki/Manage-AAD-application-in-Teams-Toolkit#How-to-view-the-AAD-app-on-the-Azure-portal)。

## <a name="sso-authentication-concepts"></a>SSO 身份验证概念

以下概念可帮助你进行 SSO 身份验证：

### <a name="working-of-sso-in-teams"></a>在 Teams 中使用 SSO

Microsoft Azure Active Directory (Azure AD 中的单一登录 (SSO) 身份验证) 以无提示方式刷新身份验证令牌，以尽量减少用户输入登录凭据所需的次数。 如果用户同意使用应用，则他们不必在另一台设备上再次同意，因为他们会自动登录。

Teams 选项卡和机器人具有类似的 SSO 支持流，有关详细信息，请参阅：

1. [在 Tabs 中单一登录 (SSO) 身份验证](../tabs/how-to/authentication/tab-sso-overview.md)
2. [机器人中的单一登录 (SSO) 身份验证](../bots/how-to/authentication/auth-aad-sso-bots.md)

### <a name="simplified-sso-with-teamsfx"></a>使用 TeamsFx 简化的 SSO

TeamsFx 通过使用 SSO 并将云资源访问到零配置的单行语句来帮助减少开发人员任务。

使用 TeamsFx SDK，可以使用凭据以简化的方式编写用户身份验证代码：

1. 浏览器环境中的用户标识： `TeamsUserCredential` 表示 Teams 当前用户的标识。
2. Node.js环境中的用户标识： `OnBehalfOfUserCredential` 使用代理流和 SSO 令牌。
3. Node.js环境中的应用程序标识： `AppCredential` 表示应用程序标识。

有关 TeamsFx SDK 的详细信息，请参阅：

* [TeamsFx SDK](TeamsFx-SDK.md) 或 [API 参考](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true)
* [Microsoft Teams 框架 (TeamsFx) 示例库](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2)

## <a name="see-also"></a>另请参阅

* [创建 Teams 应用的先决条件](tools-prerequisites.md)
