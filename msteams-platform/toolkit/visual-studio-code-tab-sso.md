---
title: 使用选项卡的 Teams 工具包和 Visual Studio Code 单一登录身份验证
description: 使用Microsoft Teams Toolkit直接在Visual Studio Code内生成支持单一登录和 Microsoft Graph调用的选项卡。
keywords: teams visual Studio code toolkit tabs sso graph authentication Azure 标识平台
localization_priority: Normal
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 7cca78c2ca3669d647dd76dd71e0a2b999b09dd1
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123869"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a>使用选项卡的 Teams 工具包和 Visual Studio Code 单一登录身份验证

> [!IMPORTANT]
> **本文档指的是旧版Teams Toolkit**
>
> 有关当前信息，请阅读 [先决条件](../get-started/prerequisites.md) 并遵循一个较新的教程。

通过Microsoft Teams Toolkit，可以直接在Visual Studio Code内为选项卡应用创建单一登录 (SSO) 身份验证。 该工具包指导你完成此过程，并提供所需的一切内容，包括在Microsoft Azure门户中预配Microsoft 标识平台注册。

## <a name="get-started--create-a-project"></a>开始 - 创建项目

1. 在工具包中创建新项目。
1. 选择选项卡作为要创建的扩展的类型。
1. 选择支持 SSO 的选项。

> [!TIP]
> 安装后，应会在Visual Studio Code活动栏中看到Teams Toolkit。 如果没有，请在活动栏中右键单击，然后选择 **Microsoft Teams** 固定工具包以便轻松访问。

## <a name="configure-your-project"></a>配置项目

1. 若要在Teams中启用 SSO，应用必须具有 Azure 应用注册资源。 Teams Toolkit将代表你预配应用注册。
1. 输入将托管应用的 URL，然后选择 **下一步**。 应用注册将使用提供的 URL 进行配置。
1. 应用注册的配置详细信息将存储在 `.env` 项目的源代码中的文件中。

若要详细了解如何预配 Azure 应用注册，请 *参阅*  我们的 [单一登录 (SSO) 选项卡](../tabs/how-to/authentication/tab-sso-overview.md) 文档的支持。

> [!TIP]
> 每次更改此 URL 时，都需要转到 **Azure 应用注册** 并更新 *API URI* 并 *重定向 URL*。

## <a name="run-your-project"></a>运行项目

1. 从`api-server`文件夹中选择 **npm安装**。 然后 **npm开始**。
1. 从`.src`文件夹中选择 **npm安装**。 然后 **npm开始**。
1. 如果使用的是 [ngrok](https://ngrok.com/) 等隧道服务，请运行它，并确保 URL 与在项目创建向导中输入的内容匹配。 如果没有，则需要在 Azure 中创建的应用注册中更新 *API URI* 并 *重定向 URL* 。
1. 导航到Visual Studio Code窗口左侧的活动栏。
1. 选择 **“运行** ”图标以显示 **“运行和调试** ”视图。
1. 还可以使用键盘快捷方式 **Ctrl+Shift+D**。

> [!TIP]
> 如果浏览器已禁用弹出窗口，则可能看不到应用在浏览器中安装对话。 如果发生这种情况，请启用弹出窗口并刷新页面。

## <a name="see-also"></a>另请参阅

[使用 Microsoft Teams 工具包和Visual Studio Code 生成应用](visual-studio-code-overview.md)
