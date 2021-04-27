---
title: 使用 Teams 身份验证和选项卡Toolkit Visual Studio单一登录身份验证
description: 使用 Microsoft Teams 管理中心在 Visual Studio Code 中生成支持单一登录和 Microsoft Graph Toolkit
keywords: teams visual studio code toolkit tabs sso graph authentication Azure identity platform
localization_priority: Normal
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: daf9a1b0bb64fee9584d0f58d749cf2b1ccaa4ef
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52018423"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a>使用 Teams 身份验证和选项卡Toolkit Visual Studio单一登录身份验证

Microsoft Teams Toolkit使你可以直接在 (代码中为选项卡) 创建单一登录Visual Studio SSO 身份验证。 该工具包将指导你完成该过程，并提供你所需的一切，包括在 Azure 门户中预配 Microsoft 标识平台注册。

## <a name="get-started--create-a-project"></a>入门 — 创建项目

1. 在工具包中创建新项目。
1. 选择选项卡作为你要创建的扩展类型。
1. 选择支持 SSO 的选项。

> [!TIP]
> 安装后，你应该会看到 Teams Toolkit代码Visual Studio栏中。 如果没有，请在活动栏中右键单击并选择 Microsoft **Teams** 固定工具包，方便访问。

## <a name="configure-your-project"></a>配置项目

1. 若要在 Teams 中启用 SSO，应用必须具有 Azure 应用注册资源。 Teams Toolkit将代表你预配应用注册。
1. 输入你的应用将托管的 URL，然后选择下一 **步**。 你的应用注册将使用提供的 URL 进行配置。
1. 应用注册的配置详细信息将存储在项目的源代码 `.env` 中的文件中。

若要详细了解如何预配 Azure 应用注册，请参阅我们的单一登录[ (SSO](../tabs/how-to/authentication/auth-aad-sso.md)) 支持选项卡文档。 

> [!TIP]
> 你将需要转到 Azure **应用注册** 并更新 API *URI，* 并重定向 *URL，只要* 更改此 URL。

## <a name="run-your-project"></a>运行项目

1. 从 **文件夹选择 npm** `api-server` 安装。 然后 **npm 启动**。
1. 从 **文件夹选择 npm** `.src` 安装。 然后 **npm 启动**。
1. 如果你使用的是像 [ngrok](https://ngrok.com/)这样的隧道服务，请运行它并确保 URL 与你在项目创建向导中输入的内容相匹配。 如果没有，则需要在 Azure 中创建的应用注册中更新 _API URI_ 和重定向 URL。 
1. 导航到"代码"窗口左侧的活动Visual Studio栏。
1. 选择" **运行** "图标以显示 **"运行和调试"** 视图。
1. 您还可以使用键盘快捷方式 **Ctrl+Shift+D**。

> [!TIP]
> 如果为浏览器禁用了弹出窗口，则你可能不会在浏览器中看到应用安装对话。 如果发生这种情况，请启用弹出窗口并刷新页面。

> [!div class="nextstepaction"]
> [了解更多信息：使用 Microsoft Teams Toolkit和 Visual Studio 代码生成应用](visual-studio-code-overview.md)
