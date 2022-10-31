---
title: 设置开发环境以跨 Microsoft 365 扩展 Teams 应用
description: 设置开发环境以跨 Microsoft 365 扩展 Teams 应用的要求。 了解运行 Microsoft Teams 和 Microsoft Office 应用程序内部版本所需的配置。
ms.date: 05/24/2022
ms.custom: m365apps
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 99050d8b8db4fac38e9d36c42a6c3efe7f1bf28d
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789910"
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

 1. 在右上角，选择 **“组织范围的应用设置**”。

 1. 在“自定义应用”下，打开“ **与自定义应用交互”** 切换和 **“保存**”。

    :::image type="content" source="images/teams-admin-enable-sideloading.png" alt-text="屏幕截图是一个从 Teams 管理员中心为自定义应用启用旁加载的示例":::

 1. 除了组织范围的应用设置外，自定义应用策略设置还允许用户将自定义应用上传到 Teams。 有关详细信息，请参阅 [管理自定义应用策略和设置](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)。

 1. 在 Teams 管理中心中，转到 **“Teams 应用** > **设置策略**”，然后选择“ **全局 (组织范围的默认) 策略**”。

 1. 打开 **“上传自定义应用**”，然后选择“ **保存**”。

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

    :::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="屏幕截图是一个示例，其中显示了选择了“目标发布”选项的Microsoft 365 管理中心“发布首选项”菜单。":::

1. 选择“**保存**”。

有关Office 365发布选项的详细信息，请参阅 *Microsoft 365 管理中心帮助* 中的 [设置标准或目标发布选项](/microsoft-365/admin/manage/release-options-in-office-365?view=o365-worldwide&preserve-view=true#targeted-release)。

## <a name="install-office-apps-in-your-test-environment"></a>在测试环境中安装 Office 应用

### <a name="desktop"></a>桌面

可以使用最近的 *Beta 版频道* 预览在 Windows 桌面的 Outlook 中运行的 Teams 应用。 检查是否必须更改测试租户[的Microsoft 365 应用版更新通道](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016)才能安装Office 365 Beta 频道版本。

要在测试环境中安装 Office 365 Beta 版频道应用程序：

1. 请使用测试租户凭据登录到测试环境。
1. 下载 [Office部署工具](https://www.microsoft.com/download/details.aspx?id=49117)并提取到本地文件夹。
1. 转到本地文件夹并在文本编辑器中打开 *configuration-Office365-x86.xml*（或 **x64.xml*，具体取决于环境），并将 *频道* 值更新为 `BetaChannel`。
1. 打开命令提示符并转到本地文件夹路径。
1. 运行 `setup.exe /configure configuration-Office365-x86.xml`（或使用 **x64.xml* 文件，具体取决于设置）。
1. 打开 Outlook（桌面客户端）并使用测试租户凭据设置邮件帐户。
1. 打开“**文件**” > “**Office 帐户**” > “**关于 Outlook**”，确认你正在运行 Outlook 的 Microsoft 365 *Beta 版频道* 版本。

    :::image type="content" source="images/outlook-about-beta-channel.png" alt-text="屏幕截图是一个示例，其中显示了有关 Outlook 的示例，用于验证你是否正在运行 Beta 频道版本。":::

1. 验证是否已安装 *Microsoft Edge WebView2 运行时*。 打开 Windows“**开始**” > “**应用和功能**”，然后搜索 **webview**：

    :::image type="content" source="images/windows-addremove-webview2.png" alt-text="屏幕截图是显示 Windows 设置中的搜索字段的示例。":::

    如果未列出，则将 [Microsoft Edge WebView2](https://developer.microsoft.com/microsoft-edge/webview2/) 安装到测试环境。

### <a name="mobile"></a>移动设备

通过加入 beta 计划，可以预览 Office for Android 应用中运行的 Teams 个人选项卡。

若要安装最新的 Office 应用 beta 版，请构建到物理 Android 设备或 Android 仿真器：

1. 确保使用 Google Play [支持的 Android 设备](https://support.google.com/googleplay/answer/1727131)。
1. 在 Android 设备上启动 **Play Store** 。
1. 搜索 Office 并选择 **“Microsoft Office：编辑&共享**”。
1. 选择“ **安装** ”按钮。

    :::image type="content" source="images/office-android-install.png" alt-text="屏幕截图显示了 Microsoft Office 的安装按钮：在 Google Play Store 中编辑&共享应用。":::

1. 安装完成后，选择“**加入 beta 版”部分** 下的“**加入**”。

    :::image type="content" source="images/office-android-join-beta.png" alt-text="屏幕截图是显示“加入 beta 版”屏幕的示例。":::

1. 启动 Office 应用并使用测试租户凭据登录。
1. **(我) >“设置”打开** 个人资料，然后滚动到菜单底部。
2. 确保使用适用于 Android 的 Office 应用版本 16.0.15726.20000 或更高版本。

## <a name="switch-to-the-developer-preview-version-of-teams"></a>切换到开发人员预览版 Teams

确保从 Microsoft Teams 客户端切换到[公共开发人员预览版](../resources/dev-preview/developer-preview-intro.md)。

1. 使用沙盒租户凭据登录 Teams。
1. 从用户配置文件旁边的省略号 (**...**) 菜单中，选择“**关于**” > “**开发人员预览版**”。 将出现对话框，选择“**切换到开发人员预览版**”。
1. Teams 应用重启后，转到用户配置文件旁边的省略号 (**...**) 菜单，并检查是否选中了“**开发人员预览版**”。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="屏幕截图是一个示例，显示了 Teams 中的公共开发人员预览版选项。":::

## <a name="install-visual-studio-code-and-teams-toolkit-extension"></a>安装 Visual Studio Code 和 Teams 工具包扩展

或者，可以使用 [Visual Studio Code](https://code.visualstudio.com/) 将 Teams 应用扩展到 Office 和 Outlook。

The extension [Teams Toolkit for Visual Studio Code](https://aka.ms/teams-toolkit) (`v2.10.0` or later) provides commands that can help modify your existing Teams code to be compatible with Outlook and Office. For more information, see [enable Teams personal tab for Office and Outlook](extend-m365-teams-personal-tab.md).

## <a name="next-step"></a>后续步骤

创建或更新 Teams 应用以跨 Microsoft 365 运行：

> [!div class="nextstepaction"]
> [为 Office 和 Outlook 启用 Teams 个人选项卡](extend-m365-teams-personal-tab.md)
> [!div class="nextstepaction"]
> [为 Outlook 启用 Teams 消息扩展](extend-m365-teams-message-extension.md)
