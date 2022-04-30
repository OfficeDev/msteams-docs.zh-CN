---
title: 设置开发环境以跨 Microsoft 365 扩展 Teams 应用
description: 下面是跨 Microsoft 365 扩展 Teams 应用的先决条件
ms.date: 02/11/2022
ms.localizationpriority: high
ms.openlocfilehash: 483ae6982dd51a16573655ed14dc93577642ba4b
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111498"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-microsoft-365"></a>设置开发环境以跨 Microsoft 365 扩展 Teams 应用

> [!NOTE]
> 跨 Microsoft 365 扩展 Teams 应用目前仅在[公共开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中可用。

跨 Microsoft 365 扩展 Teams 应用的开发环境类似于 Microsoft Teams 开发环境。 本文讨论运行 Microsoft Teams 和 Microsoft Office 应用程序的预览内部版本以预览在 Outlook 和 Office 中运行 Teams 应用所需的特定配置。

设置开发环境：

> [!div class="checklist"]
>
> * [获取 Microsoft 365 开发人员（沙盒）租户并启用旁加载](#prepare-a-developer-tenant-for-testing)
> * [在 *Office 365 目标发布* 中注册 Microsoft 365 租户](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [将帐户配置为 Outlook 和 Office 的访问预览版](#install-office-apps-in-your-test-environment)
> * [切换到开发人员预览版 Teams](#switch-to-the-developer-preview-version-of-teams)
> * [*可选*] [安装 Microsoft Visual Studio Code 的 Teams 工具包扩展](#install-visual-studio-code-and-teams-toolkit-preview-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>准备开发人员租户以进行测试

需要 Microsoft 365 开发人员订阅沙盒租户来设置开发环境。 如果还没有沙盒租户，请创建[沙盒租户](/office/developer-program/microsoft-365-developer-program-get-started)或通过组织获取测试租户。

拥有租户后，需要为租户启用旁加载，请参阅[启用旁加载](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。 要验证是否已启用旁加载，请登录 Teams，选择“**应用**”，然后选中“**上传自定义应用**”选项。

:::image type="content" source="images/teams-sideloading-enabled.png" alt-text="上传自定义应用选项":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>为 Office 365 目标发布注册开发人员租户

> [!IMPORTANT]
> 请参阅 [Microsoft Teams - Microsoft 365开发人员博客](https://devblogs.microsoft.com/microsoft365dev/)上的最新更新，以检查测试租户是否可以使用 Teams 应用的 Outlook.com 和 Office.com。

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

> [!IMPORTANT]
> 请参阅 [Microsoft Teams - Microsoft 365开发人员博客](https://devblogs.microsoft.com/microsoft365dev/)上的最新更新，以检查测试租户是否可以使用 Windows 桌面的 Outlook 以支持 Teams 消息扩展。

可以使用最近的 *Beta 版频道* 预览在 Windows 桌面的 Outlook 中运行的 Teams 应用。 检查是否必须为测试租户[更改 Microsoft 365 应用更新通道](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016)才能安装 Office 365 Beta 版频道内部版本。

要在测试环境中安装 Office 365 Beta 版频道应用程序：

1. 请使用测试租户凭据登录到测试环境。
1. 下载 [Office部署工具](https://www.microsoft.com/download/details.aspx?id=49117)并提取到本地文件夹。
1. 转到本地文件夹并在文本编辑器中打开 *configuration-Office365-x86.xml*（或 **x64.xml*，具体取决于环境），并将 *频道* 值更新为 `BetaChannel`。
1. 打开命令提示符并导航到本地文件夹路径。
1. 运行 `setup.exe /configure configuration-Office365-x86.xml`（或使用 **x64.xml* 文件，具体取决于设置）。
1. 打开 Outlook（桌面客户端）并使用测试租户凭据设置邮件帐户。
1. 打开“**文件**” > “**Office 帐户**” > “**关于 Outlook**”。  
   如果内部版本号为 **14416** 或更高版本，并且频道为 *Beta 版频道*，则运行 Microsoft 365 Beta 版频道内部版本。
1. 在右上角，打开“**即将推出**”切换。

    :::image type="content" source="images/outlook-coming-soon.png" alt-text="Outlook 中的“即将推出”切换选项":::

> [!NOTE]
> 可能需要关闭 Outlook 并重启计算机，“*即将推出*”按钮才会显示。

可以验证租户帐户的测试租户是否支持：

* 对于在 office.com、outlook.com 和 Outlook Windows 桌面上运行的 Teams 个人选项卡，请使用测试租户凭据登录，并选中 Office 或 Outlook 左侧栏上的省略号 (**...**) 选项。

    :::image type="content" source="images/outlook-desktop-ellipses.png" alt-text="Outlook 左侧栏上的省略号 ('...') 选项":::

* 有关 Windows outlook.com 和 Outlook 中的消息扩展，请选中 Outlook 撰写消息窗格底部的“**更多应用**”选项。

    :::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="Outlook 撰写消息窗格中的“更多应用”选项":::

> [!NOTE]
> 如果已选择加入 Beta 版频道版本，但看不到这些省略号选项，则预览功能支持很可能即将向租户推出。 有关最新更新，请参阅 [Microsoft Teams开发人员博客](https://devblogs.microsoft.com/microsoft365dev/)。

## <a name="switch-to-the-developer-preview-version-of-teams"></a>切换到开发人员预览版 Teams

确保从 Microsoft Teams 客户端切换到[公共开发人员预览版](../resources/dev-preview/developer-preview-intro.md)。

1. 使用沙盒租户凭据登录 Teams。
1. 从用户配置文件旁边的省略号 (**...**) 菜单中，选择“**关于**” > “**开发人员预览版**”。 将出现对话框，选择“**切换到开发人员预览版**”。
1. Teams 应用重启后，转到用户配置文件旁边的省略号 (**...**) 菜单，并检查是否选中了“**开发人员预览版**”。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Teams 中的公共开发人员预览版选项":::

## <a name="install-visual-studio-code-and-teams-toolkit-preview-extension"></a>安装 Visual Studio Code 和 Teams 工具包预览版扩展

或者，可以使用 [Visual Studio Code](https://code.visualstudio.com/) 将 Teams 应用扩展到 Office 和 Outlook。

[Visual Studio Code 的 Teams 工具包扩展](https://aka.ms/teams-toolkit)（`v2.10.0` 或更高版本）提供了有助于修改现有 Teams 代码以与 Outlook 和 Office 兼容的命令。 有关详细信息，请参阅[为 Office 和 Outlook 启用 Teams 个人选项卡](extend-m365-teams-personal-tab.md)。

## <a name="next-steps"></a>后续步骤

* [为 Office 和 Outlook 启用 Teams 个人选项卡](extend-m365-teams-personal-tab.md)
* [为 Outlook 启用 Teams 消息扩展](extend-m365-teams-message-extension.md)
