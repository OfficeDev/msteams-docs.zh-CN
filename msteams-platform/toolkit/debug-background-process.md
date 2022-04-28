---
title: 调试后台进程
author: zyxiaoyuer
description: 本地调试期间 Visual Studio Code 和 Teams 工具包的功能
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/03/2022
ms.openlocfilehash: 33e1e00165119af1e1b63d024097bd3a1a1b13c2
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073828"
---
# <a name="debug-background-process"></a>调试后台进程

本地调试工作流涉及 `.vscode/launch.json` 和 `.vscode/tasks.json` 文件，以在 VS Code 中配置调试器， 然后，VS Code 会启动调试器，Microsoft Edge 或 Chrome 调试器会启动新的浏览器实例，如下所示：

1. `launch.json` 文件在 VS Code 中配置调试器

2. VS Code 会在 `.vscode/tasks.json` 文件中运行复合 **preLaunchTask**、**预调试检查和启动全部**

3. 然后，VS Code 会启动复合配置中指定的调试器，例如 **附加到到自动程序**、**附加到后端**、**附加到前段**、**启动自动程序**

4.  Microsoft Edge 或 Chrome 调试器会启动新的浏览器实例，并打开网页以加载 Teams 客户端

## <a name="prerequisites"></a>先决条件

Teams 工具包在调试过程中检查以下先决条件：

* Node.js，适用于以下项目类型：

  |项目类型|Node.js LTS 版本|
  |----------|--------------------------------|
  |不带 Azure Functions 的选项卡 | 10, 12, **14（推荐）**, 16 |
  |带 Azure Functions 的选项卡 | 10, 12, **14（推荐）**|
  |Bot |  10, 12, **14（推荐）**, 16|
  |消息传递扩展 | 10, 12, **14（推荐）**, 16 |

   
* 具有有效凭据的 Microsoft 365 帐户，如果尚未登录，Teams 工具包会提示你登录到 Microsoft 365 帐户

* 已启用开发人员租户的自定义应用上传或旁加载，否则本地调试将终止

* Ngrok 二进制版本 2.3 适用于机器人和消息传递扩展，如果未安装 Ngrok 或版本不符合要求，Teams 工具包会在 `~/.fx/bin/ngrok` 中安装 Ngrok NPM 包 `ngrok@4.2.2`。 Ngrok 二进制文件由 Ngrok NPM 包在 `/.fx/bin/ngrok/node modules/ngrok/bin` 中管理

* Azure Functions Core Tools 版本 3。如果未安装 Azure Functions Core Tools 或版本不符合要求，Teams 工具包将安装 Azure Functions Core Tools NPM 包 azure-functions-core-tools@3，适用于 **Windows**，适用于 `~/.fx/bin/func` 中的 **macOs**。 `~/.fx/bin/func/node_modules/azure-functions-core-tools/bin` 中的 Azure Functions Core Tools NPM 包负责管理 Azure Functions Core Tools 二进制文件。 对于 Linux，本地调试终止

* 适用于 Azure Functions 的 .NET Core SDK 版本，如果未安装 .NET Core SDK 或版本不符合要求，Teams 工具包会在 `~/.fx/bin/dotnet` 中安装适用于 Windows 和 MacOS 的 .NET Core SDK。 对于 Linux，本地调试终止

  下表列出了 .NET Core 版本：

  | 平台  | 软件|
  | --- | --- |
  |Windows、macO (x64) 和 Linux | **3.1（推荐）**, 5.0, 6.0 |
  |macOs (arm64) |6.0 |

* 开发证书，如果未为 Windows 或 macOS 中的选项卡安装 localhost 的开发证书，Teams 工具包会提示你安装它

* `api/extensions.csproj` 中定义的 Azure Functions 绑定扩展，如果未安装 Azure Functions 绑定扩展，Teams 工具包将安装 Azure Functions 绑定扩展

* NPM 包，适用于 Tab 应用、机器人应用、消息传递扩展应用、Azure Functions。 如果未安装 NPM，Teams 工具包将安装所有 NPM 包

* 机器人和消息传递扩展，Teams 工具包会启动 Ngrok，为机器人和消息传递扩展创建 HTTP 隧道

* 端口可用，如果选项卡、自动程序、消息传递扩展、Azure Functions 端口不可用，则本地调试将终止

  下表列出了可用于组件的端口：

  | 组件  | 端口 |
  | --- | --- |
  | Tab | 53000 |
  | 自动程序或消息传递扩展 | 3978 |
  | 自动程序或消息传递扩展的节点检查器 | 9239 |
  | Azure Functions | 7071 |
  | 用于 Azure Functions 的节点检查器 | 9229 |


<!-- The following table lists the limitations if the required software is unavailable for debugging:

|Project type|Installation| Limitation|
|----------|--------------------------------|-----|
|Tab without Azure functions | Node.js LTS versions 10, 12, **14 (recommended)**, 16 | The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Tab with Azure functions | Node.js LTS versions 10, 12, **14 (recommended)** |The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Bot | Node.js LTS versions 10, 12, **14 (recommended)**, 16|The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Messaging extension | Node.js LTS versions 10, 12, **14 (recommended)**, 16 |The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Sign in to Microsoft 365 account | Microsoft 365 credentials |Teams toolkit prompts you to sign in to Microsoft 365 account, if you haven't signed in. |
|Bot, messaging extension | Ngrok version 2.3| • If Ngrok isn't installed or the version doesn't match the requirement, the Teams toolkit installs Ngrok NPM package `ngrok@4.2.2` in `~/.fx/bin/ngrok`. </br> • The Ngrok binary is managed by Ngrok NPM package in `/.fx/bin/ngrok/node modules/ngrok/bin`.|
|Azure functions | Azure Functions Core Tools version 3| • If Azure Functions Core Tools isn't installed or the version doesn't match the requirement, the Teams toolkit installs Azure Functions Core Tools NPM package, azure-functions-core-tools@3 for **Windows** and for **macOs** in  `~/.fx/bin/func`. </br> • The Azure Functions Core Tools NPM package in  `~/.fx/bin/func/node_modules/azure-functions-core-tools/bin` manages Azure Functions Core Tools binary. For Linux, the local debug terminates.|
|Azure functions |.NET Core SDK version|• If .NET Core SDK isn't installed or the version  doesn't match the requirement, the toolkit installs .NET Core SDK for Windows and macOS in `~/.fx/bin/dotnet`.</br> • For Linux, the local debug terminates.|
|Azure functions | Azure functions binding extensions defined in `api/extensions.csproj`| If Azure functions binding extensions isn't installed, the toolkit installs Azure functions binding extensions.|
|NPM packages| NPM packages for tab app, bot app, messaging extension app, and Azure functions|If NPM isn't installed, the toolkit installs all NPM packages.|
|Bot and messaging extension | Ngrok |Toolkit starts Ngrok to create a HTTP tunnel for bot and messaging extension. |

> [!NOTE]
> If tab, bot, messaging extension, and Azure functions ports are unavailable, the local debug terminates.

Use the following .NET Core versions:

| Platform  | Software|
| --- | --- |
|Windows, macOs (x64), Linux | **3.1 (recommended)**, 5.0, 6.0 |
|macOs (arm64) |6.0 |


> [!NOTE]
> If the development certificate for localhost isn't installed for tab in Windows or macOS, the Teams toolkit prompts you to install it.</br> -->


选择 **开始调试 (F5)** 时，Teams 工具包输出通道会在检查先决条件后显示进度和结果。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/prerequisites-debugcheck.png" alt-text="先决条件":::

## <a name="register-and-configure-your-teams-app"></a>注册和配置 Teams 应用

在设置过程中，Teams 工具包为 Teams 应用准备了以下注册和配置：

1. [注册和配置Azure AD应用程序](#registers-and-configures-azure-ad-application)：Teams 工具包会注册并配置 Azure AD 应用程序

1. [注册并配置机器人](#registers-and-configures-bot)：Teams 工具包会注册并配置机器人以使用选项卡或消息传递扩展应用

1. [注册和配置 Teams 应用](#registers-and-configures-teams-app)：Teams 工具包会注册和配置 Teams 应用

### <a name="registers-and-configures-azure-ad-application"></a>注册和配置 Azure AD 应用程序

1. 注册 Azure AD 应用程序

1. 创建客户端密码

1. 公开 API

    a. 配置应用程序 ID URI。 对于选项卡，`api://localhost/{appId}`。 对于自动程序或消息传递扩展，`api://botid-{botid}`

    b. 添加名为 `access_as_user` 的作用域。 为 **管理员和用户** 启用它


4. 配置 API 权限。将 Microsoft Graph 权限添加到 **User.Read**

    下表列出了身份验证的配置，如下所示：
    
      | 项目类型 | Web 的重定向 URI | 单页应用程序的重定向 URI |
      | --- | --- | --- |
      | Tab | `https://localhost:53000/auth-end.html` | `https://localhost:53000/auth-end.html?clientId={appId>}` |
      | 自动程序或消息传递扩展 | `https://ngrok.io/auth-end.html` | 不适用 |
  

    下表列出了具有客户端 ID 的 Microsoft 365 客户端应用程序的配置：
    
      | Microsoft 365 客户端应用程序 |  客户端 ID  |
      | --- | --- |
      | Teams 桌面、移动设备 | 1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
      | Teams Web | 5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
      | Office.com | 4345a7b9-9a63-4910-a426-35363201d503 |
      | Office.com | 4765445b-32c6-49b0-83e6-1d93765276ca |
      | Office 桌面版 | 0ec893e0-5785-4de6-99da-4ed124e5296c |
      | Outlook 桌面版 | d3590ed6-52b3-4102-aeff-aad2292ab01c |
      | Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
      | Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |
    
### <a name="registers-and-configures-bot"></a>注册和配置自动程序 

对于 Tab 应用或消息传递扩展应用：

1. 注册 Azure AD 应用程序

1. 为 Azure AD 应用程序创建客户端密码

1. 使用 Azure AD 应用程序在 [Microsoft Bot Framework](https://dev.botframework.com/) 中注册自动程序

1. 添加 Microsoft Teams 频道

1. 将消息传递终结点配置为 `https://{ngrokTunnelId}.ngrok.io/api/messages`

### <a name="registers-and-configures-teams-app"></a>注册和配置 Teams 应用

在[开发人员](https://dev.teams.microsoft.com/home)中使用 `templates/appPackage/manifest.template.json` 中的清单模板注册 Teams 应用。

注册和配置应用后，将生成本地调试文件。

## <a name="take-a-tour-of-your-app-source-code"></a>浏览你的应用源代码

在 Teams 工具包注册和配置应用后，可以在 VS Code 的资源管理器区域中查看项目文件夹和文件。 下表列出了本地调试文件和配置类型：

| 文件夹名| 目录| 调试配置类型 |
| --- | --- | --- |
|  `.fx/configs/config.local.json` | 本地调试配置文件 | 每个配置的值会在本地调试期间生成并保存。 |
|  `templates/appPackage/manifest.template.json` | 用于本地调试的 Teams 应用清单模板文件 | 文件中的占位符会在本地调试期间解析。 |
|  `tabs/.env.teams.local`  | 选项卡的环境变量文件  | 每个环境变量的值会在本地调试期间生成并保存。 |
|  `bot/.env.teamsfx.local` | 机器人和消息传递扩展的环境变量文件| 每个环境变量的值会在本地调试期间生成并保存。 |
| `api/.env.teamsfx.local`  | 适用于 Azure Functions 的环境变量文件 | 每个环境变量的值会在本地调试期间生成并保存。 |


## <a name="see-also"></a>另请参阅

[使用 Teams 工具包调试 Teams 应用](debug-local.md)
