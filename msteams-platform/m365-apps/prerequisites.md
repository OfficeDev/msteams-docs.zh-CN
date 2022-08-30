---
title: 设置开发环境以跨 Microsoft 365 扩展 Teams 应用
description: 在本文中，你将了解运行预览版本以跨Microsoft 365扩展 Teams 应用所需的先决条件。
ms.date: 05/24/2022
ms.custom: m365apps
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 965c9d8b7b05141aa6add18bba51512bd9e0a213
ms.sourcegitcommit: b13361f342c76d637321df21d2ef900471bf0eef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2022
ms.locfileid: "67457289"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-microsoft-365"></a>设置开发环境以跨 Microsoft 365 扩展 Teams 应用

跨 Microsoft 365 扩展 Teams 应用的开发环境类似于 Microsoft Teams 开发环境。 本文讨论运行 Microsoft Teams 和 Microsoft Office 应用程序的预览内部版本以预览在 Outlook 和 Office 中运行 Teams 应用所需的特定配置。

设置开发环境：

> [!div class="checklist"]
>
> * [获取 Microsoft 365 开发人员（沙盒）租户并启用旁加载](#prepare-a-developer-tenant-for-testing)
> * [在 *Office 365 目标发布* 中注册 Microsoft 365 租户](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [在测试环境中安装 Microsoft 365 应用的 Beta 版频道内部版本](#install-office-apps-in-your-test-environment)
> * [切换到开发人员预览版 Teams](#switch-to-the-developer-preview-version-of-teams)
> * [*可选*] [安装 Microsoft Visual Studio Code 的 Teams 工具包扩展](#install-visual-studio-code-and-teams-toolkit-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>准备开发人员租户以进行测试

需要 Microsoft 365 开发人员订阅沙盒租户来设置开发环境。 如果还没有沙盒租户，请创建[沙盒租户](/office/developer-program/microsoft-365-developer-program-get-started)或通过组织获取测试租户。

还需要为租户启用旁加载：

 1. 使用测试租户凭据登录到 [Teams 管理中心](https://admin.teams.microsoft.com/dashboard) 。

 1. 转到 **Teams 应用** > **管理应用**。

 1. 在右上角，选择 **组织范围的应用设置**。

 1. 在“自定义应用”下，打开 **与自定义应用** 切换和保存的交互。

    :::image type="content" source="images/teams-admin-enable-sideloading.png" alt-text="屏幕截图是一个示例，用于从 Teams 管理员中心旁加载自定义应用":::

 1. 除了组织范围的应用设置外，自定义应用策略设置还允许用户将自定义应用上传到 Teams。 有关详细信息，请参阅 [管理自定义应用策略和设置](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)。

 1. 在 Teams 管理中心，转到 **Teams 应用** > **设置策略**，然后选择 **全局 (组织范围的默认) 策略**。

 1. 打开 **“上传自定义应用**”，然后选择 **“保存**”。

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>为 Office 365 目标发布注册开发人员租户

> [!IMPORTANT]
> 创建 [Microsoft 365 开发人员沙盒租户](/office/developer-program/microsoft-365-developer-program-get-started)并注册 [Office 365 目标版本](#enroll-your-developer-tenant-for-office-365-targeted-releases)后，旁加载的 Teams 应用最多可能需要五天时间才能显示在 Outlook 和 Office 中。

要为 Office 365 目标版本注册测试租户：

1. 请使用测试租户凭据登录到“[Microsoft 365 管理中心](https://admin.microsoft.com)”。
1. 转到“**设置**” > “**组织设置**” > “**组织配置文件**”。
1. 选择“**发布首选项**”。
1. 选择任何“*目标发布*”首选项：
    1. **针对所有人的目标发布**
    1. **选定用户的目标发布**

    :::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="Microsoft 365 管理中心“发布首选项”菜单，其中选择了“目标发布”选项":::

1. 选择“保存”。

有关 Office 365 发布选项的详细信息，请参阅 *Microsoft 365 管理中心帮助* 中的 [设置标准或目标发布选项](/microsoft-365/admin/manage/release-options-in-office-365?view=o365-worldwide&preserve-view=true#targeted-release)。

## <a name="install-office-apps-in-your-test-environment"></a>在测试环境中安装 Office 应用

可以使用最近的 *Beta 版频道* 预览在 Windows 桌面的 Outlook 中运行的 Teams 应用。 检查是否必须为测试租户[更改 Microsoft 365 应用更新通道](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016)才能安装 Office 365 Beta 版频道内部版本。

要在测试环境中安装 Office 365 Beta 版频道应用程序：

1. 请使用测试租户凭据登录到测试环境。
1. 下载 [Office部署工具](https://www.microsoft.com/download/details.aspx?id=49117)并提取到本地文件夹。
1. 转到本地文件夹并在文本编辑器中打开 *configuration-Office365-x86.xml*（或 **x64.xml*，具体取决于环境），并将 *频道* 值更新为 `BetaChannel`。
1. 打开命令提示符并导航到本地文件夹路径。
1. 运行 `setup.exe /configure configuration-Office365-x86.xml`（或使用 **x64.xml* 文件，具体取决于设置）。
1. 打开 Outlook（桌面客户端）并使用测试租户凭据设置邮件帐户。
1. 打开“**文件**” > “**Office 帐户**” > “**关于 Outlook**”，确认你正在运行 Outlook 的 Microsoft 365 *Beta 版频道* 版本。

    :::image type="content" source="images/outlook-about-beta-channel.png" alt-text="从 Office 帐户转到“关于 Outlook”，验证你是否正在运行 Beta 版频道版本。":::

1. 验证是否已安装 *Microsoft Edge WebView2 运行时*。 打开 Windows“**开始**” > “**应用和功能**”，然后搜索 **webview**：

    :::image type="content" source="images/windows-addremove-webview2.png" alt-text="在 Windows 设置的“应用和功能”下搜索“webview”":::

    如果未列出，则将 [Microsoft Edge WebView2](https://developer.microsoft.com/microsoft-edge/webview2/) 安装到测试环境。

## <a name="switch-to-the-developer-preview-version-of-teams"></a>切换到开发人员预览版 Teams

确保从 Microsoft Teams 客户端切换到[公共开发人员预览版](../resources/dev-preview/developer-preview-intro.md)。

1. 使用沙盒租户凭据登录 Teams。
1. 从用户配置文件旁边的省略号 (**...**) 菜单中，选择“**关于**” > “**开发人员预览版**”。 将出现对话框，选择“**切换到开发人员预览版**”。
1. Teams 应用重启后，转到用户配置文件旁边的省略号 (**...**) 菜单，并检查是否选中了“**开发人员预览版**”。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Teams 中的公共开发人员预览版选项":::

## <a name="install-visual-studio-code-and-teams-toolkit-extension"></a>安装 Visual Studio Code 和 Teams 工具包扩展

或者，可以使用 [Visual Studio Code](https://code.visualstudio.com/) 将 Teams 应用扩展到 Office 和 Outlook。

扩展[适用于 Visual Studio Code 的 Teams 工具包](https://aka.ms/teams-toolkit)（`v2.10.0` 或更高版本）提供有助于修改现有 Teams 代码以与 Outlook 和 Office 兼容的命令。有关详细信息，请参阅[为 Office 和 Outlook 启用 Teams 个人选项卡](extend-m365-teams-personal-tab.md)。

## <a name="next-step"></a>后续步骤

创建或更新 Teams 应用以跨 Microsoft 365 运行：

> [!div class="nextstepaction"]
> [为 Office 和 Outlook 启用 Teams 个人选项卡](extend-m365-teams-personal-tab.md)
> [!div class="nextstepaction"]
> [为 Outlook 启用 Teams 消息扩展](extend-m365-teams-message-extension.md)
