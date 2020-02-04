---
title: 安装与 Microsoft 团队的 Moodle 集成
description: 如何为 Microsoft 团队安装和配置 Moodle 集成应用程序
keywords: 团队 Moodle 应用集成插件
ms.date: 01/31/2019
ms.openlocfilehash: 012d6e9c979386e892b5a47b7655208eca95e11a
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41672966"
---
# <a name="installing-the-moodle-integration-with-microsoft-teams"></a>安装与 Microsoft 团队的 Moodle 集成

> [!VIDEO https://www.youtube.com/embed/OHlPt22nKoE]

[Moodle](https://moodle.org/)是世界上最受欢迎和开放源代码的学习管理系统（LMS）现已与 Microsoft 团队集成！ 此集成可帮助教师和教师在 Moodle 课程中进行协作，询问有关其成绩和工作分配的问题，并在团队中及时更新通知！

为了帮助 IT 管理员轻松设置这种集成，我们已使用以下功能更新了我们的开放源代码 Office 365 Moodle 插件：

* 使用 Azure AD 自动注册 Moodle 服务器。
* 将 Moodle 助手 bot 的一次单击部署到 Azure。
* 自动预配团队和自动同步团队注册的所有或选择 Moodle 课程。
* 将 Moodle 选项卡和 Moodle 助手 bot 自动安装到每个已同步的团队中。 （即将推出）
* 单击一次，将 Moodle 应用发布到私有团队应用商店中。 （即将推出）

若要了解此集成提供的功能的详细信息，请转到[此处](https://education.microsoft.com/courses-and-resources/resources/microsoft-teams-moodle)。

## <a name="prerequisites"></a>先决条件

若要安装和配置此应用程序，你将需要：

1. Moodle 管理员凭据
2. Azure AD 管理员凭据
3. Azure 订阅可以在中创建新资源

## <a name="step-1-install-the-office-365-moodle-plugin"></a>步骤1：安装 Office 365 Moodle 插件

> [!VIDEO https://www.youtube.com/embed/SETEC5nzMgk]

Microsoft 团队中的 Moodle 集成由开放源[Office 365 Moodle 插件集](https://github.com/Microsoft/o365-moodle)提供支持。 若要在 Moodle 服务器上安装插件，请执行以下操作：

1. 首先，下载[Office 365 插件集](https://moodle.org/plugins/pluginversions.php?plugin=local_o365)并将其保存到本地计算机。 您需要使用版本3.5 或更高版本。
    * 安装 local_o365 插件也将安装[auth_oidc](https://moodle.org/plugins/auth_oidc)和[boost_o365Teams](https://moodle.org/plugins/pluginversions.php?plugin=theme_boost_o365teams)插件。
1. 以管理员身份登录到您的 Moodle 服务器，然后从左侧导航面板中选择 "**网站管理**"。
1. 选择 "**插件**" 选项卡，然后单击 "**安装插件**"。
1. 在 "**从 ZIP 文件安装插件**" 部分下，单击 "**选择文件**" 按钮。
1. 从左侧导航中选择 "**上传文件**" 选项，浏览上面下载的文件，然后单击 "**上载此文件**"。
1. 再次从左侧导航面板中选择 "**网站管理**" 选项，以返回到您的管理仪表板。 向下滚动到**本地插件**，然后单击 " **Microsoft Office 365 集成**" 链接。 将此配置页在单独的浏览器选项卡中打开，因为在此过程的其余部分将使用它。

您可以在[Moodle 文档](https://docs.moodle.org/34/en/Installing_plugins)中找到有关如何安装 Moodle 插件的详细信息。

**重要说明：** 保留 Office 365 Moodle 插件配置页在单独的浏览器选项卡中打开，因为您将在整个过程中返回到这组页面。

*尚无 Moodle 网站？* 您可能需要在 Azure 存储库中查看我们的 Moodle，在该存储库中，您可以在[azure 中快速](https://github.com/azure/moodle)部署 Moodle 实例，并根据需要对其进行自定义。

## <a name="step-2-configure-the-connection-between-the-office-365-plugin-and-azure-active-directory"></a>步骤2：配置 Office 365 插件与 Azure Active Directory 之间的连接

> [!VIDEO https://www.youtube.com/embed/FpGEezaJ3SA]

接下来，你需要将 Moodle 注册为 Azure Active Directory 中的应用程序。 我们提供了 PowerShell 脚本，可帮助你完成此过程。 PowerShell 脚本为 Office 365 租户预配新的 Azure AD 应用程序，Office 365 Moodle 插件将使用该应用程序。 该脚本将为您的 O365 租户设置应用程序，为设置的应用程序设置所有必需的回复 Url 和权限，并返回 AppID 和 Key。 您可以使用 O365 Moodle 插件设置页面中生成的 AppID 和 Key 为 Moodle server 配置 Azure AD。 若要查看 PowerShell 脚本自动化的详细手动步骤，可以在完整文档中查找[插件](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)。

### <a name="moodle-tab-for-microsoft-teams-information-flow"></a>Microsoft 团队信息流的 Moodle 选项卡

<img width="530px" src="~/assets/images/MoodleTabInformationFlow.png" title="Microsoft 团队信息流的 Moodle 选项卡" />

1. 从 "Microsoft Office 365 集成插件" 页中选择 "**设置**" 选项卡。
1. 单击 "**下载 PowerShell 脚本**" 按钮，并将其保存到本地计算机。
1. 您需要从 ZIP 文件准备 PowerShell 脚本。 为此，请执行以下操作：
    * 下载并解压缩`Moodle-AzureAD-Powershell.zip`文件。
    * 打开提取的文件夹。
    * 右键单击该文件， `Moodle-AzureAD-Script.ps1`然后选择 "**属性**"。
    * 在 "属性" 窗口的 "**常规**" 选项卡`Unblock`上，选中底部**安全**属性旁边的框。
    * 单击“**确定**”。
    * 复制提取的文件夹的目录路径。
1. 接下来，你将以管理员身份运行 PowerShell：
    * 单击“开始”。
    * 类型 PowerShell。
    * 右键单击 "Windows PowerShell"。
    * 单击 "以管理员身份运行"。
1. 通过键入`cd ...\...\Moodle-AzureAD-Powershell`目录路径的位置`...\...`定位到已解压缩的目录。
1. 通过以下方式执行 PowerShell 脚本：
    * Enter `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`。
    * Enter `.\Moodle-AzureAD-Script.ps1`。
    * 在弹出窗口中登录到 O365 管理员帐户。
    * 输入 Azure AD 应用程序的名称（例如 Moodle/Moodle 插件）。
    * 输入 Moodle 服务器的 URL。
    * 复制脚本生成的**应用程序 ID**和**应用程序密钥**并保存它们。
1. 接下来，你需要将 Id 和密钥添加到 Office 365 Moodle 插件。 返回到插件管理页（网站管理 > 插件 > Microsoft Office 365 集成）。
1. 在 "**设置**" 选项卡上，添加之前复制的**应用程序 Id**和**应用程序密钥**，然后单击 "**保存更改**"。
1. 页面刷新后，您现在应该可以看到一个新的 "**选择连接方法**" 一节。 单击标签为 "**默认**" 的复选框，然后再次单击 "**保存更改**"。
1. 页面刷新后，你将看到另一个新的**管理员同意 & 其他信息**。
    * 单击 "**提供管理员同意**" 链接，输入您的 Office3 365 全局管理员凭据，然后**接受**授予这些权限。
    * 在 " **AZURE AD 租户**" 字段旁边，单击 "**检测**" 按钮。
    * 在**OneDrive For BUSINESS URL**旁边，单击 "**检测到**" 按钮。
    * 填充字段后，再次单击 "**保存更改**" 按钮。
1. 单击 "**更新**" 按钮验证安装，然后**保存所做的更改**。
1. 接下来，你需要在你的 Moodle 服务器和 Azure Active Directory 之间同步用户。 根据您的环境，您可以在此阶段中选择不同的选项。 请注意，您在此处设置的配置将在每个 Moodle cron 运行（通常一天一天）内运行，以保持所有内容同步。若要开始，请执行以下操作：
    * 切换到 "**同步设置" 选项卡**
    * 在 "将**用户与 AZURE AD 同步**" 部分中，选择适用于您的环境的复选框。 通常情况下，至少要选择：
        * 在 Moodle 中为 Azure AD 中的用户创建帐户
        * 为 Azure AD 中的用户更新 Moodle 中的所有帐户
    * 在 "**用户创建限制**" 部分，可以设置筛选器，以限制将同步到 Moodle 的 Azure AD 用户。
    * **用户字段映射**部分将允许你将 Azure AD 自定义为 Moodle 用户配置文件字段映射。
    * 在 "**团队同步**" 部分中，您可以选择自动为您的现有 Moodle 课程创建组（即 "团队"）。
1. 若要验证 cron 作业（并在希望第一次运行时手动运行它们），请单击 "将**用户与 AZURE AD 同步**" 一节中的 "**计划任务管理" 页面**链接。 此操作将转到 "**任务计划**" 页。
    * 向下滚动并找到**与 AZURE AD 作业同步用户**，然后单击 "**立即运行**"。
    * 如果选择基于现有课程创建组，则还可以在**Office 365 作业中运行 "创建用户组**"。
1. 返回到插件管理页（网站管理 > 插件 > Microsoft Office 365 集成），然后选择 "**团队设置**" 页。 您需要配置一些安全设置以启用团队应用集成。
    * 若要启用 OpenID Connect，请单击 "**管理身份验证**" 链接，然后在**OpenID 连接**线上单击 "眼睛" 图标（如果它是灰显的）。
    * 接下来，你需要启用框架嵌入。 单击 " **HTTP 安全**" 链接，然后单击 "**允许框架嵌入**" 旁边的复选框。
    * 下一步是启用 web 服务，这将启用 Moodle API 功能。 单击 "**高级功能**" 链接，然后确保选中 "**启用 web 服务**" 旁边的复选框。
    * 最后，你将需要启用适用于 Office 365 的外部服务。 单击 "**外部服务**" 链接，然后执行以下操作：
        * 单击 " **Moodle Office 365 Webservices** " 行上的 "**编辑**"。
        * 选中 "**启用**" 旁边的复选框，然后单击 "**保存更改**"
    * 接下来，你需要编辑经过身份验证的用户权限以允许他们创建 web 服务令牌。 单击**编辑角色的 "已验证用户"** 链接。 向下滚动并找到 "**创建 web 服务令牌**" 功能，并标记 "**允许**" 复选框。

## <a name="step-3-deploy-the-moodle-assistant-bot-to-azure"></a>步骤3：将 Moodle 助理 Bot 部署到 Azure

> [!VIDEO https://www.youtube.com/embed/gbkJxf8FlfY]

Microsoft 团队免费的 Moodle 助理 Bot 可帮助教师和学生解答有关 Moodle 中的课程、工作分配、成绩和其他信息的问题。 自动程序还会向团队中的学生和教师发送 Moodle 通知。 此 bot 是由 Microsoft 维护的开放源项目，[在 GitHub 上提供](https://github.com/microsoft/Moodle-Teams-Bot)。

> [!NOTE]
> 在本节中，您将把资源部署到 Azure 订阅，所有资源都将使用**免费**的层进行配置。 根据你的 bot 的使用情况，你可能需要扩展这些资源。
> 如果只想使用不带机器人的 Moodle 选项卡，请跳到[步骤 4](#step-4-deploy-your-microsoft-teams-app)。

### <a name="moodle-bot-information-flow"></a>Moodle bot 信息流

<img width="530px" src="~/assets/images/MoodleBotInformationFlow.png" title="Microsoft 团队的 Moodle bot 信息流" />

若要安装机器人，首先需要在[Microsoft Identity 平台](https://identity.microsoft.com/Landing)上注册它。 这将允许你的 Bot 针对你的 Microsoft 终结点进行身份验证。 若要注册你的 bot：

1. 返回到插件管理页（网站管理 > 插件 > Microsoft Office 365 集成），然后选择 "**团队设置**" 选项卡。
1. 单击 " **Microsoft 应用程序注册门户**" 链接，并使用你的 microsoft Id 登录。
1. 输入您的应用程序的名称（例如， MoodleBot），然后单击 "**创建**" 按钮。
1. 复制**应用程序 Id** ，并将其粘贴到 "**团队设置**" 页上的 " **Bot 应用程序 id** " 字段中。
1. 单击 "**生成新密码**" 按钮。 复制生成的密码并将其粘贴到 "**团队设置**" 页上的 "**机器人应用程序密码**" 字段中。
1. 滚动到窗体底部，然后单击 "**保存更改**"。

现在，您已经生成了应用程序 Id 和密码，现在可以将机器人部署到 Azure 了。 单击 "**部署到 Azure** " 按钮，并填写包含必要信息的表单（Bot 应用程序 Id、Bot 应用程序密码和 Moodle 密码位于 "**团队设置**" 页上，并且 Azure 信息在 "**设置**" 页上）。 填写填写表单后，单击复选框以接受条款和条件，然后单击 "**购买**" 按钮（所有 Azure 资源都将部署到 "免费" 层）。

将资源部署到 Azure 后，需要使用 it 的邮件终结点配置 Office 365 Moodle 插件。 首先，你需要从 Azure 中的你的 Bot 获取终结点。 为此，请执行以下操作：

1. 如果您尚未登录到 Azure 门户，请登录到[Azure 门户](https://portal.azure.com)。
2. 在左窗格中，选择 "**资源组**"。
3. 从列表中选择您刚刚使用（或创建）的您在部署 Bot 时使用的资源组。
4. 从组中资源列表的列表中选择 " **WebApp Bot** " 资源。
5. 从 "**概述**" 部分复制**邮件终结点**。
6. 在 Moodle 中，打开 Office 365 Moodle 插件的 "**团队设置**" 页。
7. 在**机器人终结点**字段中粘贴刚复制的 URL，并将 word*消息*更改为*webhook*。 该 URL 现在应如下所示`https://botname.azurewebsites.net/api/webhook`
8. 单击 "**保存更改**"
9. 保存更改后，返回到 "**团队设置**" 选项卡，单击 "**下载清单文件**" 按钮并将清单包保存到您的计算机上（将在下一节中使用它）。

## <a name="step-4-deploy-your-microsoft-teams-app"></a>步骤4：部署 Microsoft 团队应用程序

> [!VIDEO https://www.youtube.com/embed/2rMb7gtM_ZM]

现在，你已将你的 Bot 部署到 Azure 并配置为与你的 Moodle 服务器通信，现在是部署 Microsoft 团队应用的时候了。 为此，您将从上一步中加载从 "Office 365 Moodle 插件团队设置" 页下载的清单文件。

在安装应用程序之前，您需要确保已启用外部应用和应用程序上传。 若要执行此操作，您可以执行[以下步骤](https://docs.microsoft.com/microsoftteams/platform/get-started/get-started-tenant)。 确保已启用外部应用程序后，您可以按照以下步骤部署您的应用程序。

1. 打开 Microsoft 团队。
2. 单击导航栏左上角的 "**存储**" 图标。
3. 从选项列表中单击 "**上载自定义应用程序**" 链接。 *注意：* 如果以全局管理方式登录，则可以选择将应用上载到组织的应用商店，否则您将只能为您所属的团队加载应用程序。
4. 选择以前`manifest.zip`下载的包，然后单击 "**保存**"。 如果您尚未下载清单包，可以从 Moodle 中的 "插件配置" 页的 "**团队设置**" 选项卡执行此操作。

现在，您已安装应用程序，可以将选项卡添加到您有权访问的任何频道。 若要执行此操作，请导航到频道**+** ，单击符号并从列表中选择您的应用程序。 按照提示完成将 Moodle 课程选项卡添加到频道中。

就是这么简单。 你和你的团队现在可以直接从 Microsoft 团队开始使用你的 Moodle 课程。

若要与我们共享任何功能请求或反馈，请访问我们的[用户语音页面](https://microsoftteams.uservoice.com/forums/916759-moodle)。
