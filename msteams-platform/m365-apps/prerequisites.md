---
title: 设置开发环境以跨Teams扩展Microsoft 365
description: 下面是跨应用程序扩展 Teams 应用的先决条件Microsoft 365
ms.date: 02/11/2022
ms.openlocfilehash: 1f9b893c185d7cbae249ccc77de2a52cbdcb409a
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2022
ms.locfileid: "63452737"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-microsoft-365"></a>设置开发环境以跨Teams扩展Microsoft 365

> [!NOTE]
> 跨企业扩展Microsoft 365目前仅适用于公共[开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)。

跨应用程序扩展Teams开发Microsoft 365类似于Microsoft Teams开发。 本文讨论运行 Microsoft Teams 和 Microsoft Office 应用程序的预览版本以预览在 Outlook 和 Office 中运行的 Teams 应用所需的特定配置。

设置开发环境：

> [!div class="checklist"]
>
> * [获取Microsoft 365开发人员 (沙) 租户并启用旁加载](#prepare-a-developer-tenant-for-testing)
> * [在目标Microsoft 365中Office 365 *租户*](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [配置帐户以访问预览版本的 Outlook 和 Office](#install-office-apps-in-your-test-environment)
> * [切换到 开发者预览版 的 Teams](#switch-to-the-developer-preview-version-of-teams)
> * [*可选*][安装Teams Toolkit代码Microsoft Visual Studio扩展](#install-visual-studio-code-and-teams-toolkit-preview-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>准备开发人员租户进行测试

你需要一Microsoft 365开发人员订阅沙盒租户来设置你的开发环境。 如果还没有沙盒租户，请创建沙 [盒](/office/developer-program/microsoft-365-developer-program-get-started) 租户或通过组织获取测试租户。

拥有租户后，需要为租户启用旁加载，请参阅 [启用旁加载](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。 若要验证旁加载是否已启用，请登录到 Teams，选择"应用"，然后Upload  **自定义应用选项**。

:::image type="content" source="images/teams-sideloading-enabled.png" alt-text="Upload自定义应用选项":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>为开发人员租户注册Office 365定向版本

> [!IMPORTANT]
> 请参阅 [Microsoft Teams - Microsoft 365 开发人员](https://devblogs.microsoft.com/microsoft365dev/)博客上的最新更新，以检查 Outlook.com 和 Office.com 对 Teams 应用的支持是否可用于测试租户。

若要为测试租户注册Office 365定向版本：

1. 登录以[Microsoft 365 管理中心](https://admin.microsoft.com)测试租户凭据登录。
1. 转到 **设置** > **Org 设置** > **Organization 配置文件**。
1. 选择 **"发布首选项"**。
1. 选择任何 *定向发布* 首选项：
    1. **面向所有人发布**
    1. **选定用户的目标发布**

    :::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="Microsoft 365 管理中心已选择定向发布选项的&quot;发布首选项&quot;菜单":::

1. 选择“**保存**”。

有关发布选项Office 365，请参阅帮助中的设置 [标准](/microsoft-365/admin/manage/release-options-in-office-365?view=o365-worldwide&preserve-view=true#targeted-release)或Microsoft 365 管理中心 *选项*。

## <a name="install-office-apps-in-your-test-environment"></a>在Office安装应用

> [!IMPORTANT]
> 请参阅 Microsoft Teams [- Microsoft 365 开发人员](https://devblogs.microsoft.com/microsoft365dev/)博客上的最新更新，以检查 Outlook for Windows 桌面支持的 Teams 邮件扩展是否可用于测试租户。

可以通过使用Teams Beta 渠道Outlook在 Windows 桌面版中预览运行 *的应用。* 检查是否[必须更改测试](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016)租户的 Microsoft 365 应用版 更新频道，以安装 Office 365 Beta 渠道版本。

若要在Office 365安装 Beta 渠道应用程序：

1. 使用测试租户凭据登录测试环境。
1. 下载 [Office 部署工具](https://www.microsoft.com/download/details.aspx?id=49117)并解压缩到本地文件夹。
1. 转到本地文件夹并打开 *configuration-Office365-x86.xml(或* **x64.xml*，具体取决于) 编辑器中的环境，将 *Channel* 值更新为 `BetaChannel`。
1. 打开命令提示符并导航到本地文件夹路径。
1. 运行 `setup.exe /configure configuration-Office365-x86.xml` (或使用 **x64.xml* 文件，具体取决于你的安装程序) 。
1. 打开Outlook (桌面客户端) ，然后使用测试租户凭据设置邮件帐户。
1. 打开 **文件** > **Office Account** >  **关于Outlook**。  
   如果内部版本号为 **14416** 或更高版本，并且频道为 *Beta 渠道*，则Microsoft 365 beta 渠道版本。
1. 在右上角，打开"即将 **推出"** 切换。

    :::image type="content" source="images/outlook-coming-soon.png" alt-text="Outlook 中的&quot;即将推出&quot;切换Outlook":::

> [!NOTE]
> 你可能需要关闭Outlook重新启动计算机，"*即将* 推出"按钮才能显示。

你可以验证租户帐户的测试租户支持：

* For Teams personal tabs running on office.com， outlook.com， and Outlook for Windows desktop， sign in with your test tenant credentials and check for ellipses (**...**) option on the left sidebar of Office or Outlook.

    :::image type="content" source="images/outlook-desktop-ellipses.png" alt-text="省略号 (左侧) 栏上的&quot;...&quot;选项Outlook":::

* For messaging extensions in outlook.com and Outlook for Windows， check for **More Apps** option at the bottom of the Outlook compose message pane.

    :::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="&quot;撰写邮件&quot;窗格中的&quot;Outlook&quot;选项":::

> [!NOTE]
> 如果你已选择加入 Beta 渠道版本，但看不到这些省略号选项，则预览功能支持很可能正在向租户推出。 有关最新更新，请参阅开发人员[Microsoft Teams博客](https://devblogs.microsoft.com/microsoft365dev/)。

## <a name="switch-to-the-developer-preview-version-of-teams"></a>切换到 开发者预览版 的 Teams

确保从客户端[开发者预览版公用Microsoft Teams](../resources/dev-preview/developer-preview-intro.md)服务器。

1. 登录以Teams沙盒租户凭据登录。
1. 从用户配置文件旁边的 (**...**) "菜单中，选择" **关于** > **开发人员预览"**。 将出现一个对话框，选择 **切换到开发人员预览**。
1. 重新启动Teams后，转到用户配置文件旁边的省略号" (**...**) "菜单，并检查 **开发者预览版是否选中**。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="开发人员预览版中的公共Teams":::

## <a name="install-visual-studio-code-and-teams-toolkit-preview-extension"></a>安装 Visual Studio Code 和 Teams Toolkit Preview 扩展

（可选）[可以使用 Visual Studio Code 将](https://code.visualstudio.com/) Teams 应用扩展到Office Outlook。

[Teams Toolkit](https://aka.ms/teams-toolkit) `v2.10.0` Visual Studio Code (或更高版本) 的扩展提供可帮助修改现有 Teams 代码以与 Outlook 和 Office 兼容的命令。 有关详细信息，请参阅启用Teams[个人选项卡Office Outlook](extend-m365-teams-personal-tab.md)。

## <a name="next-steps"></a>后续步骤

* [为 Office 和 Outlook 启用 Teams 个人选项卡](extend-m365-teams-personal-tab.md)
* [为 Outlook 启用 Teams 消息传递扩展](extend-m365-teams-message-extension.md)
