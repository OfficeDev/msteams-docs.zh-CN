---
title: 调试后台进程
author: surbhigupta
description: 在本模块中，Visual Studio 代码和 Teams 工具包在本地调试过程中的工作原理，以及如何注册和配置 Teams 应用
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/03/2022
ms.openlocfilehash: b8f85f092f9a99e9931a5ff0ea5e763c0b4fb0fe
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616785"
---
# <a name="debug-background-process"></a>调试后台进程

本地调试过程涉及`.vscode/launch.json`在 Microsoft Visual Studio Code 中配置调试器的和`.vscode/tasks.json`文件。 Visual Studio Code启动调试器，Microsoft Edge 或 Google Chrome 将启动新的浏览器实例。

调试进程工作流如下所示：

1. `launch.json`文件在Visual Studio Code中配置调试器。

2. Visual Studio Code运行复合 **preLaunchTask**，**预调试检查&在** 文件中`.vscode/tasks.json`全部启动。

3. 然后，Visual Studio Code 启动复合配置中指定的调试器，例如 **附加到到自动程序**、**附加到后端**、**附加到前段**、**启动自动程序**。

4. Microsoft Edge 或 Google Chrome 会启动新的浏览器实例，并打开网页以加载 Teams 客户端。

## <a name="teams-toolkit-verification-of-prerequisites"></a>Teams 工具包验证先决条件

Teams 工具包在调试过程中检查以下先决条件：

* Node.js，适用于以下项目类型：

  |项目类型|Node.js LTS 版本|
  |----------|--------------------------------|
  |Tab | 14、16（推荐） |
  |SPFx 选项卡 | 14、16（推荐）|
  |Bot |  14、16（推荐）|
  |消息扩展 | 14、16（推荐） |

* 如果尚未使用有效凭据登录，Teams 工具包会提示你登录到 Microsoft 365 帐户。
* 已启用开发人员租户的自定义应用上传或旁加载，以防止本地调试终止。
* 如果未安装 Ngrok 或版本不符合要求，Teams 工具包将安装 Ngrok NPM 包`ngrok@4.2.2``~/.fx/bin/ngrok`。 Ngrok NPM 包管理 `/.fx/bin/ngrok/node modules/ngrok/bin` 适用于机器人和消息扩展的 Ngrok 二进制版本 2.3。
* Teams 工具包安装Azure Functions核心工具 NPM 包、适用于 **Windows** 和 **macO** `~/.fx/bin/func`的 azure-functions-core-tools@3（如果未安装 Azure Functions Core Tools 版本 3 或版本不符合要求）。 `~/.fx/bin/func/node_modules/azure-functions-core-tools/bin` 中的 Azure Functions Core Tools NPM 包负责管理 Azure Functions Core Tools 二进制文件。 对于 Linux，本地调试终止。
* 如果未安装适用于Azure Functions的 .NET Core SDK 版本或版本不符合要求，Teams 工具包将安装适用于 **Windows** 和 **MacOS** `~/.fx/bin/dotnet`的 .NET Core SDK。 对于 Linux，本地调试终止。
* 如果未安装 Ngrok 或版本不符合要求，Teams 工具包将安装 Ngrok NPM 包`ngrok@4.2.2``~/.fx/bin/ngrok`。 Ngrok 二进制版本 2.3 适用于机器人和消息扩展。 Ngrok 二进制文件由 Ngrok NPM 包在 `/.fx/bin/ngrok/node modules/ngrok/bin` 中管理。
* Teams 工具包安装Azure Functions核心工具 NPM 包、适用于 **Windows** 和 **MacO** `~/.fx/bin/func`的 azure-functions-core-tools@3（如果未安装 Azure Functions Core Tools 版本 4 或版本不符合要求）。 `~/.fx/bin/func/node_modules/azure-functions-core-tools/bin` 中的 Azure Functions Core Tools NPM 包负责管理 Azure Functions Core Tools 二进制文件。 对于 Linux，本地调试终止。
* 如果未安装 .NET Core SDK 或版本不符合要求，Teams 工具包将在适用于 Azure Functions 的 .NET Core SDK 版本中`~/.fx/bin/dotnet`安装适用于 **Windows** 和 **MacOS** 的 .NET Core SDK。 对于 Linux，本地调试终止。

  下表列出了 .NET Core 版本：

  | 平台  | 软件|
  | --- | --- |
  |Windows、macO (x64) 和 Linux | **3.1（推荐）**, 5.0, 6.0 |
  |macOS (arm64) |6.0 |

* 如果 **未为 Windows** 或 **MacOS** 中的选项卡安装 localhost 的开发证书，则 Teams 工具包会提示你安装它。
* Azure Functions定义的`api/extensions.csproj`绑定扩展，如果未安装Azure Functions绑定扩展，Teams 工具包将安装Azure Functions绑定扩展。
* NPM 包，适用于选项卡应用、自动程序应用、消息扩展应用和 Azure Functions 的应用程序。 如果未安装 NPM 包，Teams 工具包将安装所有 NPM 包。
* 机器人和消息扩展，Teams 工具包启动 Ngrok，为机器人和消息扩展创建 HTTP 隧道。
* 端口可用，如果选项卡、自动程序、消息扩展和 Azure Functions 端口不可用，则本地调试将终止。

  下表列出了可用于组件的端口：

  | 组件  | 端口 |
  | --- | --- |
  | Tab | 53000 |
  | 自动程序或消息扩展 | 3978 |
  | 自动程序或消息扩展的节点检查器 | 9239 |
  | Azure Functions | 7071 |
  | 用于 Azure Functions 的节点检查器 | 9229 |

<!-- The following table lists the limitations if the required software is unavailable for debugging:

|Project type|Installation| Limitation|
|----------|--------------------------------|-----|
|Tab without Azure functions | Node.js LTS versions 10, 12, **14 (recommended)**, 16 | The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Tab with Azure functions | Node.js LTS versions 10, 12, **14 (recommended)** |The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Bot | Node.js LTS versions 10, 12, **14 (recommended)**, 16|The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Message extension | Node.js LTS versions 10, 12, **14 (recommended)**, 16 |The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Sign-in to Microsoft 365 account | Microsoft 365 credentials |Teams Toolkit prompts you to sign-in to Microsoft 365 account, if you haven't signed in. |
|Bot, message extension | Ngrok version 2.3| • If Ngrok isn't installed or the version doesn't match the requirement, the Teams Toolkit installs Ngrok NPM package `ngrok@4.2.2` in `~/.fx/bin/ngrok`. </br> • The Ngrok binary is managed by Ngrok NPM package in `/.fx/bin/ngrok/node modules/ngrok/bin`.|
|Azure functions | Azure Functions Core Tools version 3| • If Azure Functions Core Tools isn't installed or the version doesn't match the requirement, the Teams Toolkit installs Azure Functions Core Tools NPM package, azure-functions-core-tools@3 for **Windows** and for **macOs** in  `~/.fx/bin/func`. </br> • The Azure Functions Core Tools NPM package in `~/.fx/bin/func/node_modules/azure-functions-core-tools/bin` manages Azure Functions Core Tools binary. For Linux, the local debug terminates.|
|Azure functions |.NET Core SDK version|• If .NET Core SDK isn't installed or the version  doesn't match the requirement, the Toolkit installs .NET Core SDK for Windows and macOS in `~/.fx/bin/dotnet`.</br> • For Linux, the local debug terminates.|
|Azure functions | Azure functions binding extensions defined in `api/extensions.csproj`| If Azure functions binding extensions isn't installed, the Toolkit installs Azure functions binding extensions.|
|NPM packages| NPM packages for tab app, bot app, message extension app, and Azure functions|If NPM isn't installed, the Toolkit installs all NPM packages.|
|Bot and message extension | Ngrok |Toolkit starts Ngrok to create a HTTP tunnel for bot and message extension. |

> [!NOTE]
> If tab, bot, message extension, and Azure functions ports are unavailable, the local debug terminates.

Use the following .NET Core versions:

| Platform  | Software|
| --- | --- |
|Windows, macOs (x64), Linux | **3.1 (recommended)**, 5.0, 6.0 |
|macOs (arm64) |6.0 |

> [!NOTE]
> If the development certificate for localhost isn't installed for tab in Windows or MacOS, the Teams Toolkit prompts you to install it.</br> -->

选择 **开始调试 (F5)** 时，Teams 工具包输出通道会在检查先决条件后显示进度和结果。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/prerequisites-debugcheck.png" alt-text="先决条件检查摘要" lightbox="../assets/images/teams-toolkit-v2/debug/prerequisites-debugcheck.png":::

## <a name="register-and-configure-teams-app"></a>注册和配置 Teams 应用

在设置过程中，Teams 工具包为 Teams 应用准备了以下注册和配置：

1. [注册和配置Microsoft Azure Active Directory (Azure AD) 应用](#registers-and-configures-microsoft-azure-active-directoryazure-ad-app)

1. [注册和配置机器人](#registers-and-configures-bot)。

1. [注册和配置 Teams 应用](#registers-and-configures-teams-app)。

### <a name="registers-and-configures-microsoft-azure-active-directoryazure-ad-app"></a>注册和配置Microsoft Azure Active Directory (Azure AD) 应用

1. 注册 Azure AD 应用。

1. 创建客户端密码。

1. 公开 API。

    a. 配置应用程序 ID URI。 对于选项卡，`api://localhost/{appId}`。 对于自动程序或消息扩展 `api://botid-{botid}`。

    b. 添加名为 `access_as_user` 的作用域。 为 **管理员和用户** 启用它。

4. 配置 API 权限。 将 Microsoft Graph 权限添加到 **User.Read**。

    下表列出了身份验证的配置：

      | 项目类型 | Web 的重定向 URI | 单页应用程序的重定向 URI |
      | --- | --- | --- |
      | Tab | `https://localhost:53000/auth-end.html` | `https://localhost:53000/auth-end.html?clientId={appId>}` |
      | 自动程序或消息扩展 | `https://ngrok.io/auth-end.html` | 不适用 |

    下表列出了具有客户端 ID 的 Microsoft 365 客户端应用程序的配置:

      | Microsoft 365 客户端应用程序 | 客户端 ID |
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

对于选项卡应用或消息扩展应用：

1. 注册 Azure AD 应用程序。

1. 为 Azure AD 应用程序创建客户端密码。

1. 使用 Azure AD 应用程序在 [Microsoft Bot Framework](https://dev.botframework.com/)中注册自动程序。

1. 添加 Teams 频道。

1. 将消息传送终结点配置为 `https://{ngrokTunnelId}.ngrok.io/api/messages`。

### <a name="registers-and-configures-teams-app"></a>注册和配置 Teams 应用

使用清单模板在 [开发人员门户](https://dev.teams.microsoft.com/home) 中 `templates/appPackage/manifest.template.json`注册 Teams 应用。

注册和配置应用后，将生成本地调试文件。

## <a name="take-a-tour-of-your-app-source-code"></a>浏览你的应用源代码

在 Teams 工具包注册和配置应用后，可以在Visual Studio Code的 **“资源管理器**”下查看项目文件夹和文件。 下表列出了本地调试文件和配置类型：

| 文件夹名| 目录| 调试配置类型 |
| --- | --- | --- |
|  `.fx/configs/config.local.json` | 本地调试配置文件 | 在本地调试期间生成并保存每个配置的值。 |
|  `templates/appPackage/manifest.template.json` | 用于本地调试的 Teams 应用清单模板文件 | 本地调试期间文件中的占位符。 |
|  `tabs/.env.teams.local`  | 选项卡的环境变量文件 | 在本地调试期间生成并保存每个环境变量的值。 |
|  `bot/.env.teamsfx.local` | 自动程序和消息扩展的环境变量文件| 在本地调试期间生成并保存每个环境变量的值。 |
| `api/.env.teamsfx.local`  | 适用于 Azure Functions 的环境变量文件 | 在本地调试期间生成并保存每个环境变量的值。 |

## <a name="see-also"></a>另请参阅

* [使用 Teams 工具包调试 Teams 应用](debug-local.md)
* [使用 Teams 工具包预配云资源](provision.md)
* [部署到云](deploy.md)
* [预览和自定义 Teams 应用清单](TeamsFx-preview-and-customize-app-manifest.md)
