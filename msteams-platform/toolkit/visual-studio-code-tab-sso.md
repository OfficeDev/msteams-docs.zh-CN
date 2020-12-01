---
title: 单一登录身份验证与团队工具包和 Visual Studio Code for 选项卡
description: 使用 Microsoft 团队工具包生成支持在 Visual Studio Code 中直接进行单一登录和 Microsoft Graph 调用的选项卡
keywords: 团队 visual studio code 工具包选项卡 sso 图形身份验证 Azure 标识平台
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: fe734143975688cd35c510cd68cd0779a2200a18
ms.sourcegitcommit: 7e47bf158249050c36d97509eea00e77089a54e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2020
ms.locfileid: "49477732"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a>单一登录身份验证与团队工具包和 Visual Studio Code for 选项卡

Microsoft 团队工具包使您能够在 Visual Studio Code 中直接为选项卡应用程序创建单一登录 (SSO) 身份验证。 该工具包将引导您完成整个过程，并提供所需的所有内容，包括在 Azure 门户中预配 Microsoft identity platform 注册。

## <a name="get-started--create-a-project"></a>入门-创建项目

1. 在工具包中创建一个新项目。
1. 选择 "tab" 作为要创建的扩展类型。
1. 选择支持 SSO 的选项。

> [!TIP]
> 安装完成后，应在 Visual Studio Code 活动栏中看到 "团队" 工具包。 如果不是，请在活动栏中右键单击，然后选择 " **Microsoft 团队** " 以固定该工具包以方便访问。

## <a name="configure-your-project"></a>配置项目

1. 若要在团队中启用 SSO，应用必须具有 Azure 应用注册资源。 团队工具包将代表你预配应用注册。
1. 输入将托管您的应用程序的 URL，然后选择 " **下一步**"。 您的应用程序注册将使用提供的 URL 进行配置。
1. 应用注册的配置详细信息将存储在 `.env` 项目源代码的文件中。

如果你想要了解有关如何设置 Azure 应用注册的详细信息，请 _参阅_  我们 [的单一登录 (SSO) 支持的选项卡](../tabs/how-to/authentication/auth-aad-sso.md) 文档。

> [!TIP]
> 每当您更改此 URL 时，您都需要转到 **Azure 应用注册** 并更新 *API URI* 并 *重定向 url* 。

## <a name="run-your-project"></a>运行您的项目

1. 从文件夹中选择 " **npm 安装** " `api-server` 。 然后 **npm 启动**。
1. 从文件夹中选择 " **npm 安装** " `.src` 。 然后 **npm 启动**。
1. 如果使用的是隧道服务（如 [ngrok](https://ngrok.com/)），请运行它并确保 URL 与您在 "项目创建向导" 中输入的内容相匹配。 如果不是这样，您将需要更新在 Azure 中创建的应用注册中的 _API URI_ 并重 _定向 URL_ 。
1. 导航到 Visual Studio "代码" 窗口左侧的 "活动" 栏。
1. 选择 " **运行** " 图标以显示 " **运行" 和 "调试** " 视图。
1. 您还可以使用键盘快捷方式 **Ctrl + Shift + D**。

> [!TIP]
> 如果浏览器禁用了弹出窗口，则在浏览器中可能不会看到 "应用程序安装" 对话框。 如果发生这种情况，请启用弹出窗口并刷新页面。

> [!div class="nextstepaction"]
> [了解详细信息：使用 Microsoft 团队工具包和 Visual Studio Code 生成应用](visual-studio-code-overview.md)
