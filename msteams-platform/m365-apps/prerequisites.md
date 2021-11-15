---
title: 设置开发环境以跨Teams扩展 Microsoft 365
description: 下面是跨应用程序扩展Teams应用的先决条件Microsoft 365
ms.date: 11/15/2021
ms.topic: how-to
ms.openlocfilehash: d9e6ecb9e0cdbdb4754de12dff4399c02bf88863
ms.sourcegitcommit: f77750f2e60f63d1e2f66a96c169119683c66950
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2021
ms.locfileid: "60960258"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-m365-preview"></a>设置开发环境以跨 M365 Teams预览版扩展 (应用) 

用于跨应用程序Teams应用程序Microsoft 365开发环境与用于开发Microsoft Teams环境类似。 本文讨论运行 Microsoft Teams 和 Microsoft Office 应用程序的预览版本，以便预览在 Teams 和 Office 中运行的 Outlook 应用所需的特定配置。 若要设置开发环境，需要：

> [!div class="checklist"]
> * [获取 M365 开发人员 (沙盒) 并启用旁加载](#prepare-a-developer-tenant-for-testing)
> * [在目标版本中注册 *Office 365 M365 租户*](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [配置帐户以访问预览版本的 Outlook 和 Office](#install-beta-office-apps-in-your-test-environment)
> * [切换到 开发者预览版 的 Teams](#switch-to-the-developer-preview-version-of-teams)
> * [*Optional*][安装Teams Toolkit扩展Visual Studio Code](#install-visual-studio-code-and-teams-toolkit-preview-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>准备开发人员租户进行测试

如果还没有沙盒租户，Microsoft 365开发人员[订阅沙盒](/office/developer-program/microsoft-365-developer-program-get-started)租户或通过组织获取测试租户。

拥有租户后，你需要通过登录 [Microsoft 365 管理中心](https://admin.microsoft.com)并 [](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)导航到"显示所有 > Teams > Teams 应用">设置策略 > 全局"来为租户启用旁 **加载**。  在自定义Upload **和保存上****切换**。

如果你有现有租户，请验证旁加载是否已启用，Teams应用 **"**。 如果为租户 **Upload** 旁加载，你将看到自定义应用选项。

:::image type="content" source="images/teams-sideloading-enabled.png" alt-text="如果你从&quot;应用&quot;面板看到&quot;Upload自定义应用&quot;选项，Teams租户旁加载":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>为开发人员租户注册Office 365定向版本

> [!IMPORTANT]
> 请参阅 Microsoft Teams [- Microsoft 365 开发人员](https://devblogs.microsoft.com/microsoft365dev/category/teams/)博客，以检查测试租户 outlook.com office.com 对 Teams 应用的支持是否可用。

若要预览Teams或 outlook.com office.com 中运行的应用，选择加入测试租户Office 365[定向版本](/microsoft-365/admin/manage/release-options-in-office-365#targeted-release)。

1. 使用测试Microsoft 365 管理中心凭据登录并导航到"组织配置文件"选项卡。选择"发布首选项 [](https://admin.microsoft.com/AdminPortal/Home?#/Settings/OrganizationProfile)"并选择"定向发布 *首选项"* 之一：

:::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="Microsoft 365 管理中心已选择定向发布选项的&quot;发布首选项&quot;菜单":::

有关发布选项Office 365，请参阅帮助中的设置标准或Microsoft 365 管理中心 [](/microsoft-365/admin/manage/release-options-in-office-365)*选项*。

1. 使用测试租户凭据Teams验证租户是否 office.com outlook.com 运行的个人选项卡。 如果在旁栏 (**...)** 选项 (旁加载的个人选项卡的入口点Teams省略号) ，租户) 支持。

:::image type="content" source="images/outlook-web-ellipses.png" alt-text="省略号&quot;...&quot;应用程序中的旁加载Teams选项卡应用的 outlook.com":::

1. 通过检查"撰写邮件"区域中的"更多应用"选项 outlook.com 测试租户对邮件Outlook支持。
``

> [!NOTE]
> 如果你已选择加入定向版本，但看不到这些选项，预览功能支持可能仍在向租户推出。 有关最新更新，请参阅开发人员[Microsoft Teams博客](https://devblogs.microsoft.com/microsoft365dev/category/teams/)。

## <a name="install-beta-office-apps-in-your-test-environment"></a>在测试Office安装 Beta 测试版应用

> [!IMPORTANT]
> 请参阅最新的 Microsoft Teams [- Microsoft 365 开发人员](https://devblogs.microsoft.com/microsoft365dev/category/teams/)博客，以检查 Outlook Windows 桌面对 Teams 消息扩展的支持是否可用于测试租户。

可以通过使用Teams Beta 渠道Outlook在 Windows 桌面版中预览在 Outlook *中运行* 的应用。 若要在Outlook环境中安装 Beta 渠道版本，你可能需要更改测试租户的 Microsoft 365 应用版 更新[](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016)频道。

下面是在测试环境中Office 365 *Beta 渠道* 应用程序的步骤：

1. 在测试环境中，Microsoft 365 管理中心 (为测试租户帐户创建的凭据登录 (例如用户名域 https://admin.microsoft.com)  @ .onmicrosoft.com) 。
1. 从管理中心，选择安装 **Office (***或转到*) 以在测试环境中安装桌面应用。 （可选）添加测试用户 (测试用户) 。
1. 下载 Office[部署工具](https://www.microsoft.com/download/details.aspx?id=49117)并提取到本地文件夹。
1. 打开 *configuration-Office365-x86.xml* (或 **x64.xml*，具体取决于) 编辑器中的环境，将 *Channel* 值更新为 `BetaChannel` 。
1. 从提升的命令提示符下 `setup.exe /configure configuration-Office365-x86.xml` ， (**x64.xml* 文件，具体取决于你的设置) 。
1. 打开Outlook (桌面) ，然后使用测试租户凭据设置邮件帐户。
1. In Outlook， open **File**  >  **Office Account** About  >  **Outlook**， and confirm that you are now on the *Beta Channel* and that your build number is **14416** or higher.
1. 在客户端 **窗口** 右上角的"即将推出"Outlook切换：

   :::image type="content" source="images/outlook-coming-soon.png" alt-text="桌面中的&quot;即将推出&quot;Outlook切换为&quot;开&quot;}":::

通过使用测试租户凭据登录并查找侧栏上的省略号 (**...**) 选项，可以验证租户是否支持在 Outlook for Windows 桌面版上运行的 Teams 个人选项卡 (旁加载 Teams 个人选项卡) 的入口点。

:::image type="content" source="images/outlook-desktop-ellipses.png" alt-text="省略号&quot;...&quot;桌面版中旁加载Teams选项卡应用的Outlook点":::

同样，可以通过检查 Outlook 撰写邮件功能区中的"更多应用"选项来验证 Outlook for Windows 桌面版中邮件扩展的测试Outlook支持。

如果你已选择加入定向版本，但看不到这些省略号选项，则预览功能支持可能仍在向租户推出。 有关最新更新，请参阅开发人员[Microsoft Teams博客](https://devblogs.microsoft.com/microsoft365dev/category/teams/)。

## <a name="switch-to-the-developer-preview-version-of-teams"></a>切换到 开发者预览版 的 Teams

确保从你的客户端选择 [*开发者预览版*](../resources/dev-preview/developer-preview-intro.md)公用Microsoft Teams应用程序。

1. 登录以Teams沙盒租户帐户登录。
1. 从用户配置文件旁边的 (**...) "** 菜单中，选择"关于"并选择"开发人员 **预览"** 选项。 
1. 对话框出现后，选择 **切换到开发人员** 预览以重新启动Teams并检查开发者预览版是否已启用。

:::image type="content" source="images/teams-dev-preview.png" alt-text="从Teams省略号菜单，打开&quot;关于&quot;并验证&quot;开发者预览版&quot;选项是否选中":::

## <a name="install-visual-studio-code-and-teams-toolkit-preview-extension"></a>安装 Visual Studio Code 和 Teams Toolkit Preview 扩展

（可选）你可以利用Visual Studio Code将Teams[](https://code.visualstudio.com/)扩展到Office Outlook。

Teams Toolkit [Visual Studio Code](https://aka.ms/teams-toolkit) (或更高版本) 的扩展提供的命令可帮助修改现有 Teams 代码，以与 Outlook 和 Office 兼容 `v2.10.0` 。 继续启用[Teams个人选项卡Office Outlook](extend-m365-teams-personal-tab.md)了解更多信息。

## <a name="next-steps"></a>后续步骤

- [为用户Teams个人选项卡Office Outlook](extend-m365-teams-personal-tab.md)
- [为Teams启用邮件Outlook](extend-m365-teams-message-extension.md)