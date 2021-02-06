---
title: 安装与 Microsoft Teams 的一体式集成
description: 如何安装和配置 Microsoft Teams 的一流集成应用
keywords: Teams 2013 应用集成插件
ms.topic: how-to
ms.author: lajanuar
author: laujan
ms.openlocfilehash: bb3de6b3897105ff3564ecd332cba28a0db85b0f
ms.sourcegitcommit: a16590b2ccc46e1b6d17cbb367762a3c16ff779c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/05/2021
ms.locfileid: "50115739"
---
# <a name="installing-the-moodle-integration-with-microsoft-teams"></a>安装与 Microsoft Teams 的一体式集成

作为 LMS (的热门开源学习管理系统[) ，现在](https://moodle.org/)与 Microsoft Teams 集成在一起。 此集成可帮助教师和教师围绕 Teams 课程展开协作，提出有关成绩和作业的问题，并直接在 Teams 中通过通知保持更新。

为了帮助 IT 管理员轻松设置此集成，我们已使用以下功能更新了开放源代码 Microsoft 365 的"编辑插件"：

* 使用 Azure AD ([Azure Active Directory](https://azure.microsoft.com/services/active-directory/) 自动) 。
* 只需单击一下，即可将你的"Your Moodle 助手"机器人部署到 Azure。
* 自动预配团队，并自动同步所有或选择"一心"课程的团队注册。
* 自动将一个"一致"选项卡和一个"协调人"助手自动安装到每个同步的团队中。

若要详细了解此集成提供的功能 *，请参阅*[Microsoft Teams 和 Teams。](https://education.microsoft.com/resource/3dffb3a8)

## <a name="prerequisites"></a>先决条件

为了安装和配置此应用程序，你将需要：

1. 管理员凭据。

1. Azure AD 管理员凭据。

1. 可在其中创建新资源的 Azure 订阅。

## <a name="step-1-install-the-microsoft-365-moodle-plugins"></a>步骤 1：安装 Microsoft 365 的一流插件

Microsoft Teams 中的其集成由开放源代码 [Microsoft 365 的一个 Pluginle 插件集提供支持](https://github.com/Microsoft/o365-moodle)。 若要在 Your Moodle 服务器中安装插件，你需要安装以下内容：

1. A [current stable version of Moodle](https://download.moodle.org/releases/latest/).

1. 已下载和 [保存到本地计算机的一个将一体式 OpenID Connect](https://moodle.org/plugins/auth_oidc) 和 Microsoft [365](https://moodle.org/plugins/local_o365) 集成插件。

> [!NOTE]
> Teams 集成需要安装 OpenID Connect 和 Microsoft 365 集成插件。 此外， [强烈建议使用 Microsoft 365 Teams 主题](https://moodle.org/plugins/theme_boost_o365teams) 插件。

3. 以管理员角色登录到 Your Moodle 服务器，然后从左侧[](https://docs.moodle.org/22/en/Settings_block)导航面板中的"设置"块中选择"网站管理"。

1. 选择 **"插件"** 选项卡，然后选择"**安装插件"。**

1. 在 **"从 ZIP 文件安装** 插件"部分，选择 **"选择文件"** 按钮。

1. Select the **Upload a file** options from the left navigation， browse for the file you downloaded above， and choose Upload this **file.**

1. 从 **左侧导航面板** 中选择"网站管理"选项以返回到管理员仪表板。 向下滚动到 **本地插件并选择** **Microsoft 365 集成** 链接。 **在整个安装过程中，保持此配置页在单独的浏览器选项卡中打开**。

你可以找到有关 How to install Moodle 插件在 [Pressle 文档中详细信息](https://docs.moodle.org/34/en/Installing_plugins)。

> [!IMPORTANT]
>
> * 在单独的浏览器选项卡中保持 Microsoft 365 管理插件配置页面打开 ， 你将在整个过程中返回到这组页面。  <br/><br/>
>* 如果你没有现有的一个一流网站，可以在 [Azure](https://github.com/azure/moodle) 存储库上查看一下其，你可以快速部署一个一个其实例并根据需要对其进行自定义。

## <a name="step-2-configure-the-connection-between-the-microsoft-365-plugin-and-azure-active-directory-azure-ad"></a>步骤 2：配置 Microsoft 365 插件与 Azure AD (Azure Active Directory) 

接下来，你需要在 Azure AD 中将一个开发平台注册为应用程序。 我们提供了 PowerShell 脚本来帮助你完成此过程。 PowerShell 脚本会为 Microsoft 365 租户设置新的 Azure AD 应用程序，Microsoft 365 的 Pluginle 插件将使用该应用程序。 该脚本将为 Microsoft 365 租户设置应用，为预配的应用设置所需的回复 URL 和权限，并返回 `AppID` 和 `Key` 。 可以使用生成的和在 `AppID` Microsoft 365 的"管理插件"设置页中，使用 Azure AD 配置 `Key` Your Your Moodle 服务器网站。

>[!IMPORTANT]
> PowerShell 脚本不会使用最新的配置项进行更新，因此，您必须按照在一个 [3.8.0.4 和 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) 以及 [3.8.0.5 和 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) 发行页面中概述的步骤手动完成配置。 </br></br>
> 若要查看 PowerShell 脚本正在自动执行的详细手动步骤，请参阅 *"* 将 [Your Moodle 实例注册为应用程序"。](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a>Microsoft Teams 信息流的"选择"选项卡

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. 从 Microsoft 365 集成插件页面选择 **"设置"** 选项卡。

1. 选择 **"下载 PowerShell 脚本"** 按钮，并将其保存到本地计算机。

1. 你需要从 ZIP 文件准备 PowerShell 脚本。 为此，请执行以下操作：

    * 下载并解压缩 `Moodle-AzureAD-Powershell.zip` 文件。
    * 打开提取的文件夹。
    * 右键单击 `Moodle-AzureAD-Script.ps1` 该文件，然后选择"**属性"。**
    * 在 **"** 属性"窗口的"常规"选项卡下，选中位于窗口底部的 Security 属性旁边的 `Unblock` 框。 
    * 选择“确定”。
    * 将目录路径复制到提取的文件夹。

1. 接下来，您将以管理员角色运行 PowerShell：

    * 选择“开始”。
    * 键入 PowerShell。
    * 右键单击Windows PowerShell。
    * 选择"以管理员角色运行"。

1. 通过键入目录的路径导航到解压缩 `cd .../.../Moodle-AzureAD-Powershell` `.../...` 目录。

1. 执行 PowerShell 脚本：

    * Enter `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` 。
    * Enter `./Moodle-AzureAD-Script.ps1` 。
    * 在弹出窗口中登录到 Microsoft 365 管理员帐户。
    * 输入 Azure AD 应用程序应用程序的名称 (，例如，在) 。
    * 输入你的其服务器 URL。
    * 复制 **脚本生成的****应用程序** ID 和应用程序密钥，并保存它们。

1. 接下来，你需要将 And 添加到 ` AppID` `Key` Microsoft 365 的"一页"插件。 返回到 Microsoft 365 集成 (插件➡插件➡插件) 。

1. 在"**安装**"选项卡上，添加之前复制的应用程序 **ID** 和应用程序密钥，然后选择"**保存更改"。**

1. 刷新页面后，应该会看到新节 **"选择连接方法"。** 选中标记为"默认" **的复选框** ，然后再次选择 **"保存** 更改"。

1. 刷新页面后，你将看到另一个新分区管理员 **同意&其他信息**。
    * 选择" **提供管理员同意** "链接，输入 Microsoft 365 全局管理员凭据，然后 **接受** 以授予权限。
    * 在 **"Azure AD 租户"字段** 旁边，选择 **"检测"** 按钮。
    * 在 **OneDrive for Business URL 旁边，** 选择 **"检测"** 按钮。
    * 填充字段后，再次选择 **"保存更改"** 按钮。

1. 选择 **"更新** "按钮以验证安装，然后 **保存更改**。

1. 接下来，你需要将用户同步到你的其服务器和 Azure AD。 根据你的环境，你可以在此阶段选择不同的选项。 首先，请执行以下操作：
    * 切换到" **同步设置"选项卡**
    * 在 **"使用 Azure AD 同步** 用户"部分中，选中适用于你的环境的复选框。 通常，您至少应选择以下选项：  

        ✔为 Azure AD 中的用户创建在一起的帐户。 
        ✔ Azure AD 中的用户更新在一起的所有帐户。  

    * 在 **"用户创建限制** "部分，你可以设置筛选器以限制将同步到其的 Azure AD 用户。
    * " **用户字段映射** "部分将允许你自定义 Azure AD 到一位用户个人资料字段映射。
    * 在 **"Teams 同步** "部分，你可以选择自动 (组，例如，) 或所有现有 Teamsle 课程的 Teams 组。

> [!NOTE]
> 默认情况下，将[](https://docs.moodle.org/310/en/Cron)按照任务计划运行， (每天运行一次) 。 但是，cron 应更频繁地运行以保持所有内容保持同步。

13. 若要验证 [cron](https://docs.moodle.org/310/en/Cron)作业 (和/或手动运行它们进行首次运行) 请选择"使用 **Azure AD** 同步用户"部分中的"计划任务管理"页面链接。  这会将您带至 **"计划任务"** 页。

    * 向下滚动并找到使用 **Azure AD 作业的** 同步用户，然后选择"**立即运行"。**
    * 如果选择基于现有课程创建组，还可以在 **Microsoft 365** 作业中运行"创建用户组"。

1. 返回到 Microsoft 365 集成 (中的➡管理➡插件) 并选择 **"Teams** 设置"页。 你需要配置一些设置才能启用 Teams 应用集成。

    * 若要启用 **OpenID Connect，** 请选择"管理身份验证"链接，并选择 **OpenId Connect** 线路上的目视图标（如果显示为灰色）。
    * 接下来，你需要启用框架嵌入。 选择 **HTTP 安全** 链接，然后选择"允许嵌入帧 **"旁边的复选框**。
    * 下一步是启用 Web 服务，这将启用一些用户 API 功能。 选择 **"高级功能** "链接，然后确保选中"启用 **Web** 服务"旁边的复选框。
    * 最后，你需要为 Microsoft 365 启用外部服务。 选择 **"外部服务"** 链接，然后下一步：  

        ✔**选择****"Microsoft 365 Webservices"行上的"编辑**"。  
        ✔选中"已启用"旁边的 **复选框**，然后选择" **保存更改"**

    * 接下来，你需要编辑经过身份验证的用户权限，以允许他们创建 Web 服务令牌。 选择 **"编辑"角色"Authenticated user"** 链接。 向下滚动并找到" **创建 Web 服务令牌** "功能并标记 **"允许"** 复选框。

## <a name="step-3-deploy-the-moodle-assistant-bot-to-azure"></a>步骤 3：将 Botle 助手机器人部署到 Azure

适用于 Microsoft Teams 的免费一览助手机器人可帮助教师和学生回答有关其课程、作业、成绩和其他信息的问题。 机器人还会向 Teams 中的学生和教师发送一些通知。 机器人是由 Microsoft 维护的开放源代码项目，在 [GitHub 上可用](https://github.com/microsoft/Moodle-Teams-Bot)。

> [!NOTE]
> 在此部分中，你将向 Azure 订阅部署资源。 所有资源都将使用免费 **层** 进行配置。 根据机器人的使用情况，你可能需要扩展这些资源。
> 如果你想要在没有自动程序的情况下使用"下流"选项卡，请跳到[步骤 4。](#step-4-deploy-your-microsoft-teams-app)

### <a name="moodle-bot-information-flow"></a>自动程序信息流

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

若要安装自动程序，你首先需要在 Microsoft 标识平台上 [注册它](https://identity.microsoft.com/Landing)。 这样，机器人可以针对 Microsoft 终结点进行身份验证。 注册自动程序：

1. 返回到 Microsoft 365 集成 (中的➡插件➡管理) 并选择 **"Teams** 设置"选项卡。

1. 选择 **Microsoft 应用程序注册门户** 链接，然后使用 Microsoft ID 登录。

1. 输入应用名称， (，例如，一) 选择 **"创建"** 按钮。

1. 复制 **应用程序 ID 并将其** 粘贴到"团队设置"页上的"自动程序应用程序 **ID"** 字段中。 

1. 选择 **"生成新密码"** 按钮。 复制生成的密码并将其粘贴到"团队设置"页上的" **自动** 程序应用程序密码 **"** 字段中。

1. 滚动到窗体的底部，然后选择"**保存更改"。**

现在，你已生成应用程序 ID 和密码，是时候将机器人部署到 Azure 了：

> [!div class="checklist"]
> * 选择 **"部署到 Azure"** 按钮，然后使用" ("设置"页上的"自动程序应用程序 ID"、"Bot 应用程序密码"和"Secretle 密码"的必要信息 **填写表单。** Azure 信息位于"设置 **"页上**) 。 
> * 完成表单后，选中复选框以同意条款和条件。
> * 选择 **"购买** "按钮 (所有 Azure 资源都部署到免费层) 。

资源部署到 Azure 后，你将需要使用消息终结点配置 Microsoft 365 的"一线"插件。 你需要从 Azure 中的机器人获取终结点：

1. 登录到 [Azure 门户](https://portal.azure.com)。

1. 在左侧 **窗格中，选择** "资源组"，然后选择在部署自动程序 (或) 创建的资源组。

1. 从 **组中资源列表中选择 WebApp Bot** 资源。

1. 从 **"概述"部分** 复制 **消息终结点** 。

1. 在一个"开发工具"中，打开 Microsoft 365 的"Team **Settings"** 页面。

1. 在 **自动程序终结点** 字段中粘贴你刚刚复制的 URL，然后将单词 *消息更改为* *webhook。* URL 现在应如下所示：  `https://botname.azurewebsites.net/api/webhook`

1. 选择 **"保存更改"。**

1. 保存更改后，返回到"团队设置"选项卡，选择"下载清单文件"按钮，将应用清单包保存到计算机 (你将在) 下一节中使用它。

## <a name="step-4-deploy-your-microsoft-teams-app"></a>步骤 4：部署 Microsoft Teams 应用

现在，你已将机器人部署到 Azure 并配置为与你的 Talkle 服务器通信，是时候部署 Microsoft Teams 应用了。 为此，你将加载从上一步骤的"Microsoft 365 一代插件团队设置"页下载的应用清单文件。

在安装应用之前，你需要确保启用外部应用和上载应用。 为此，可以按照 Teams 准备 [Microsoft 365](../concepts/build-and-test/prepare-your-o365-tenant.md) 租户文档中的步骤操作。 确保启用外部应用后，可以按照以下步骤部署应用：

1. 打开 **Microsoft Teams。** 

1. 选择 **导航** 栏左下角区域的应用图标。

1. 从 **选项列表中选择"** 上载自定义应用"链接。

> [!Note]
> 如果以全局管理员身份登录，可以选择将应用上载到组织的应用程序目录，否则只能为作为成员的团队加载应用。

4. 选择 `manifest.zip` 之前下载的程序包，然后选择"保存 **"。** 如果尚未下载应用清单包，可以从 **Pluginle** 中插件配置页的"团队设置"选项卡进行下载。

现在，你已安装应用，你可以将选项卡添加到你有权访问的任何频道。 为此，请导航到通道，选择加 (➕) 符号，然后从列表中选择你的应用。 按照提示完成向频道添加 Your Moodle 课程选项卡。

## <a name="step-5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a>步骤 5：在 Microsoft Teams 中允许自动创建"开发工具"选项卡

尽管可以在 Microsoft Teams 中手动创建"开发方式"选项卡，但你可能会决定在通过课程同步创建团队时自动创建它们。 为此，你需要在一起配置已上传的 Microsoft Teams 应用的 ID：

1. 打开 Microsoft Teams。

1. 从导航栏的左下角区域选择"应用"图标。

1. 找到上传的 **一个➡** 选择 **选项** 图标➡选择 **复制链接**。

1. 在文本编辑器中，粘贴复制的内容。 它应包含 URL，如&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff。 复制 URL 的最后一部分，例如 `00112233-4455-6677-8899-aabbccddeeff` ，这是 Microsoft Teams 应用的 ID。

1. 在一个"开发工具"中，从 Microsoft 365"管理插件配置"页面打开 Teams 的" **其** 应用"选项卡。

1. 将 Microsoft Teams 应用的 ID 粘贴到"其应用 ID"字段中，并保存更改。

现在同步了一个将一去不二的课程时，Microsoft Teams 将自动在团队中安装一个"一般"选项卡，在 Teams 的"常规"频道中创建一个"一行"选项卡，并配置它以包含用于从中同步其的一流课程的课程页面。

### <a name="thats-it-you-and-your-team-can-now-start-working-with-your-moodle-courses-directly-from-microsoft-teams"></a>就是这么简单。 现在，你和团队可以直接从 Microsoft Teams 开始使用你的"Your Teams"课程。

若要与我们共享任何功能请求或反馈，请访问我们的用户 [语音页面](https://microsoftteams.uservoice.com/forums/916759-moodle)。
