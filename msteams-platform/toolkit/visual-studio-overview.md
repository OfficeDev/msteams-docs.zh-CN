---
title: 使用 Teams Toolkit 和 Visual Studio
description: 开始使用自定义工具直接在Visual Studio生成出色的自定义Microsoft Teams Toolkit
keywords: teams visual studio 工具包
localization_priority: Normal
ms.topic: overview
ms.author: johmil
ms.openlocfilehash: 6a0f466ba0d95312695be8b5460fc949e3f70811
ms.sourcegitcommit: 4ac93d69927791a8ccf678ca5ee83e63b51566b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2021
ms.locfileid: "53095512"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a>使用 Teams Toolkit 和 Visual Studio

借助 Microsoft Teams 工具包，可以直接在 Visual Studio 集成开发环境（IDE）中创建自定义 Teams 应用程序。 Microsoft Teams 工具包将引导你完成整个过程，并提供构建、调试和启动 Teams 应用所需的一切资源。

## <a name="prerequisites"></a>先决条件

1. [启用开发人员预览](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)。

2. 确保已 ASP.NET **<span></span>和 Web** 开发模块添加到Visual Studio实例。 有关详细信息，请参阅通过Visual Studio[或删除工作负载](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)和组件来修改服务。

![Visual studio asp.net 模块](../assets/images/visual-studio-web-dev-module.png)

## <a name="install-the-teams-toolkit"></a>安装Teams Toolkit

可以从 Microsoft Teams Toolkit Visual Studio 应用商店或直接从 Visual Studio[内的](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit)"扩展"菜单中下载Visual Studio。 

## <a name="use-the-toolkit"></a>使用工具包

- [设置新项目](#set-up-a-new-teams-project)
- [配置应用程序](#configure-your-app)
- [在应用商店中Teams](#install-and-run-your-app-locally)
- [验证你的应用](#validate-your-app)
- [发布应用程序](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>设置新的Teams项目

1. 启动 Visual Studio 2019。
2. 选择 **创建新项目**。
3. 搜索 **"Microsoft Teams应用"，** 然后选择"下一 **步"。**
4. 在"**配置新项目"中**，输入Project **名称、****位置** 和 **解决方案名称**。
5. 选择 **"** 下一步"输入应用的名称。
6. 在"其他信息"屏幕中，输入应用程序名称和开发人员 **或公司名称**，Teams应用。

## <a name="configure-your-app"></a>配置应用程序

应用程序的核心是Teams三个组件：

- The Microsoft Teams client (web， desktop or mobile) where users interact with your app.
- 响应对网站中显示的内容的请求的服务器Teams。 例如，HTML 选项卡内容或自动程序自适应卡片。
- 应用Teams包包含三个文件：

    > [!div class="checklist"]
    >
    > - 打开manifest.js
    > - 要 [显示在](../resources/schema/manifest-schema.md#icons) 公共或组织应用程序目录中的应用的颜色图标。
    > - 显示在[活动](../resources/schema/manifest-schema.md#icons)栏上的Teams图标。

安装应用后，Teams客户端将分析清单文件以确定所需信息，如应用名称和服务所在的 URL。

> [!NOTE]
>如果尚未登录，则必须登录到 Microsoft 365 帐户，以继续进行开发过程。
>
> 如果你没有帐户，Microsoft 365注册开发人员计划[Microsoft 365订阅。](https://developer.microsoft.com/microsoft-365/dev-program) 它是免费的 90 天，只要你使用它进行开发活动，它将续订。 如果你有一个 Visual Studio Enterprise 或 Professional 订阅，这两个计划均Microsoft 365[免费](https://aka.ms/MyVisualStudioBenefits)开发人员订阅，在订阅生命周期内Visual Studio有效。 有关详细信息，请参阅[设置开发人员Microsoft 365订阅](/office/developer-program/office-365-developer-program-get-started)。

### <a name="configuration-steps"></a>配置步骤

1. 若要配置应用，请选择"Project > **TeamsFx >配置 SSO..."** 菜单。

当系统提示时，登录到具有 M365 租户的 Microsoft 帐户。

## <a name="install-and-run-your-app-locally"></a>在本地安装和运行应用

按 F5 开始调试。 应用程序安装对话框将显示在客户端Teams中。

## <a name="validate-your-app"></a>验证你的应用

通过 **Project > TeamsFx 验证> Teams清单**"菜单，你可以检查应用包是否有效。

## <a name="publish-your-app-to-teams"></a>将应用发布到 Teams

在[](https://dev.teams.microsoft.com/home)Teams 开发人员门户中，你可以将应用上载到团队、将应用提交到组织中用户的公司自定义应用商店，或将应用提交到所有 Teams 用户的应用源。

- IT 管理员将审阅这些提交。
- 你可以返回到发布 **页面** ，检查你的提交状态，并了解你的应用是否已被 IT 管理员批准或拒绝。这同样也是你可以向应用提交更新或取消任何当前处于活动状态的提交的地方。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 Blazor 生成Microsoft Teams应用程序](../get-started/first-app-blazor.md)
