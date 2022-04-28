---
title: 设置开发环境以跨Microsoft 365扩展Teams应用
description: 下面是跨Microsoft 365扩展Teams应用的先决条件
ms.date: 02/11/2022
ms.openlocfilehash: 094da29fdb871ef4af091e32e123e2d644b7445f
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104068"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-microsoft-365"></a>设置开发环境以跨Microsoft 365扩展Teams应用

> [!NOTE]
> 跨Microsoft 365扩展 teams 应用目前仅在[公共开发人员预览](~/resources/dev-preview/developer-preview-intro.md)版中可用。

跨Microsoft 365扩展Teams应用的开发环境类似于Microsoft Teams开发。 本文介绍运行Microsoft Teams和Microsoft Office应用程序的预览版本以预览Teams Outlook和Office中运行的应用所需的特定配置。

设置开发环境：

> [!div class="checklist"]
>
> * [获取Microsoft 365开发人员 (沙盒) 租户并启用旁加载](#prepare-a-developer-tenant-for-testing)
> * [在Office 365 *目标版本* 中注册Microsoft 365租户](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [将帐户配置为访问预览版Outlook和Office](#install-office-apps-in-your-test-environment)
> * [切换到开发人员预览版Teams](#switch-to-the-developer-preview-version-of-teams)
> * [*可选*][为Microsoft Visual Studio代码安装Teams Toolkit扩展](#install-visual-studio-code-and-teams-toolkit-preview-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>准备开发人员租户以进行测试

需要一个Microsoft 365开发人员订阅沙盒租户来设置开发环境。 如果还没有沙盒租户，请创建 [沙盒租户](/office/developer-program/microsoft-365-developer-program-get-started) 或通过组织获取测试租户。

拥有租户后，需要为租户启用旁加载，请参阅 [启用旁加载](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。 若要验证是否启用旁加载，请登录Teams，选择 **“应用**”，然后检查 **Upload自定义应用** 选项。

:::image type="content" source="images/teams-sideloading-enabled.png" alt-text="Upload自定义应用选项":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>为Office 365目标版本注册开发人员租户

> [!IMPORTANT]
> 请参阅[Microsoft Teams - Microsoft 365开发人员博客](https://devblogs.microsoft.com/microsoft365dev/)上的最新更新，检查Outlook.com 和 Office.com 是否支持测试租户Teams应用。

若要为Office 365定向版本注册测试租户：

1. 使用测试租户凭据登录到[Microsoft 365 管理中心](https://admin.microsoft.com)。
1. 转到 **设置** > **Org 设置** > **Organization 配置文件**。
1. 选择 **“发布首选项**”。
1. 选择任何 *目标发布* 首选项：
    1. **面向所有人的目标版本**
    1. **选择用户的目标版本**

    :::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="Microsoft 365 管理中心“发布首选项”菜单，其中选择了“目标发布”选项":::

1. 选择“保存”。

有关Office 365发布选项的详细信息，请参阅 *Microsoft 365 管理中心帮助* 中 [设置标准或目标发布选项](/microsoft-365/admin/manage/release-options-in-office-365?view=o365-worldwide&preserve-view=true#targeted-release)。

## <a name="install-office-apps-in-your-test-environment"></a>在测试环境中安装Office应用

> [!IMPORTANT]
> 请参阅 Microsoft Teams 上的最新更新 [- Microsoft 365开发人员博客](https://devblogs.microsoft.com/microsoft365dev/)，检查Windows桌面支持Teams消息扩展Outlook是否可供测试租户使用。

可以使用最近的 *Beta 频道版本* 预览Windows桌面上Outlook中运行的Teams应用。 检查是否必须[更改测试租户的Microsoft 365 应用版更新通道](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016)才能安装 Office 365 Beta Channel 生成。

若要在测试环境中安装 Office 365 Beta Channel 应用程序：

1. 使用测试租户凭据登录到测试环境。
1. 下载[Office部署工具](https://www.microsoft.com/download/details.aspx?id=49117)并提取到本地文件夹。
1. 转到本地文件夹并打开 *configuration-Office365-x86.xml(* 或 **x64.xml*，具体取决于你在文本编辑器中) 的环境，并将 *通道* 值更新为 `BetaChannel`。
1. 打开命令提示符并导航到本地文件夹路径。
1. 运行 `setup.exe /configure configuration-Office365-x86.xml` (或使用 **x64.xml* 文件，具体取决于设置) 。
1. 打开Outlook (桌面客户端) 并使用测试租户凭据设置邮件帐户。
1. 打开 **文件** > **Office** **AccountAbout** >  Outlook。  
   如果生成号为 **14416** 或更高版本，并且通道为 *Beta Channel*，则运行Microsoft 365 beta Channel 内部版本。
1. 在右上角，打开 **“即将推出”** 切换。

    :::image type="content" source="images/outlook-coming-soon.png" alt-text="Outlook中的“即将推出”切换选项":::

> [!NOTE]
> 可能需要关闭Outlook并重启计算机，以显示“*即将* 推出”按钮。

可以验证租户帐户的测试租户支持：

* 对于 office.com、outlook.com 和 Outlook Windows桌面上运行的Teams个人选项卡，请使用测试租户凭据登录，并检查Office或Outlook左侧栏上的省略号 (**...**) 选项。

    :::image type="content" source="images/outlook-desktop-ellipses.png" alt-text="省略号 ('...') Outlook左侧栏上的选项":::

* 有关Windows outlook.com 和Outlook中的消息扩展，请检查Outlook撰写消息窗格底部的 **“更多应用**”选项。

    :::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="Outlook撰写消息窗格中的“更多应用”选项":::

> [!NOTE]
> 如果你已选择加入 Beta Channel 版本，但看不到这些省略号选项，则预览功能支持很可能正在向租户推出。 有关最新更新，请参阅[Microsoft Teams开发人员博客](https://devblogs.microsoft.com/microsoft365dev/)。

## <a name="switch-to-the-developer-preview-version-of-teams"></a>切换到开发人员预览版Teams

确保从Microsoft Teams客户端切换到[公共开发人员预览](../resources/dev-preview/developer-preview-intro.md)版。

1. 使用沙盒租户凭据登录Teams。
1. 从省略号 (**...**) 用户配置文件旁边的菜单中，选择 **AboutDeveloper** >  预览版。 将出现一个对话框，选择 **“切换到开发人员预览**”。
1. Teams应用重启后，转到省略号 (**...**) 用户配置文件旁边的菜单，并检查是否选择了 **开发人员预览** 版。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Teams中的公共开发人员预览选项":::

## <a name="install-visual-studio-code-and-teams-toolkit-preview-extension"></a>安装Visual Studio Code和Teams Toolkit预览版扩展

（可选）可以使用[Visual Studio Code](https://code.visualstudio.com/)将Teams应用扩展到Office和Outlook。

[Visual Studio Code (](https://aka.ms/teams-toolkit)或更高版本的扩展Teams Toolkit`v2.10.0`) 提供了有助于修改现有Teams代码以与Outlook和Office兼容的命令。 有关详细信息，请参阅[为Office和Outlook启用Teams个人选项卡](extend-m365-teams-personal-tab.md)。

## <a name="next-steps"></a>后续步骤

* [为 Office 和 Outlook 启用 Teams 个人选项卡](extend-m365-teams-personal-tab.md)
* [为Outlook启用Teams消息扩展](extend-m365-teams-message-extension.md)
