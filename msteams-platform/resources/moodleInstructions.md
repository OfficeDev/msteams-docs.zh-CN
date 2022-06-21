---
title: 安装 Moodle LMS
description: 本文介绍如何安装和配置 Moodle 集成应用以进行Microsoft Teams
ms.topic: how-to
ms.localizationpriority: medium
ms.author: lajanuar
author: surbhigupta
ms.openlocfilehash: 0c19d8bc4e3919fe49f6594c8ec738bafc1c76d3
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189636"
---
# <a name="install-moodle-lms"></a>安装 Moodle LMS

本文介绍如何安装 Moodle LMS。

> [!NOTE]
> 为了帮助 IT 管理员轻松设置 Moodle 和 Teams 集成，将针对以下内容更新开源Microsoft 365 Moodle 插件：
>
> * 使用 [Microsoft Azure Active Directory (Azure AD) ](https://azure.microsoft.com/services/active-directory/)自动注册 Moodle 服务器。
>
> * 将 Moodle 助手机器人一键式部署到 Azure。
>
> * 为所有或选择 Moodle 课程自动预配团队和自动同步团队注册。
>
> * 将 Moodle 选项卡和 Moodle 助手机器人自动安装到每个同步团队中。
>
> 若要详细了解此集成提供的功能，请[参阅 Microsoft Teams 和 Moodle](https://education.microsoft.com/resource/3dffb3a8)。

## <a name="prerequisites"></a>先决条件

以下是安装 Moodle 的先决条件：

* Moodle 管理员凭据。

* Azure AD 管理员凭据。

* 可在其中创建新资源的 Azure 订阅。

## <a name="1-install-the-microsoft-365-moodle-plugins"></a>1. 安装Microsoft 365 Moodle 插件

Microsoft Teams中的 Moodle 集成由开放源代码[Microsoft 365 Moodle 插件集](https://github.com/Microsoft/o365-moodle)提供支持。

### <a name="requisite-applications-and-plugins"></a>必需的应用程序和插件

在继续安装Microsoft 365 Moodle 插件之前，请确保安装和下载以下内容：

1. 确保安装 [当前稳定版本的 Moodle](https://download.moodle.org/releases/latest/)。

1. 将 Moodle [OpenID 连接](https://moodle.org/plugins/auth_oidc)和[Microsoft 365集成](https://moodle.org/plugins/local_o365)插件下载并保存到本地计算机。

    > [!NOTE]
    > 安装 OpenID 连接 和 Microsoft 365 集成插件是Teams集成所必需的。
    >
    > 此外，强烈建议[使用Microsoft 365 Teams主题](https://moodle.org/plugins/theme_boost_o365teams)插件。

### <a name="microsoft-365-moodle-plugins"></a>Microsoft 365 Moodle 插件

1. 以管理员身份登录到 Moodle 服务器，并从位于左侧导航面板 [的设置块](https://docs.moodle.org/22/en/Settings_block)中选择 **站点管理**。

1. 选择 **“插件** ”选项卡，然后选择 **“安装插件**”。

1. 从 **ZIP 文件部分的“安装插件** ”部分中， **选择一个文件**。

1. 从左侧导航面板 **中选择Upload文件** 选项，浏览下载的文件，然后选择 **此文件Upload**。

1. 从左侧导航面板中选择 **“站点管理** ”以返回到管理员仪表板。 向下滚动到 **本地插件**，然后选择 **Microsoft 365集成** 链接。

    > [!IMPORTANT]
    >
    > * 将Microsoft 365 Moodle 插件配置页保留在单独的浏览器选项卡中打开，因为在整个过程中需要返回到这组页面。  
    >
    > * 如果没有现有的 Moodle 网站，请转到 [Azure 存储库上的 Moodle](https://github.com/azure/moodle) ，并快速部署 Moodle 实例并根据需要对其进行自定义。

## <a name="2-configure-the-connection-between-the-microsoft-365-plugins-and-azure-ad"></a>2.配置Microsoft 365插件与 Azure AD 之间的连接

必须配置Microsoft 365插件与 Azure AD 之间的连接。

### <a name="requisites"></a>先决条件

使用 PowerShell 脚本将 Moodle 注册为 Azure AD 中的应用程序。 该脚本预配以下内容：

* Microsoft 365租户的新 Azure AD 应用程序，由 Microsoft 365 Moodle 插件使用。
* Microsoft 365租户的应用，为预配的应用设置所需的回复 URL 和权限，并返回`AppID``Key`和 。

使用生成`AppID``Key`的和在Microsoft 365 Moodle 插件设置页中使用 Azure AD 配置 Moodle 服务器站点。

> [!IMPORTANT]
>
> * PowerShell 脚本不会使用最新的配置项进行更新，因此，必须按照 Moodle [3.8.0.4、3.9.1、](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release)[3.8.0.5 和 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) 发行页中所述的步骤手动完成配置。
>
> * 有关手动注册 Moodle 实例的详细信息，请参阅 [将 Moodle 实例注册为应用程序](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)。

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a>Microsoft Teams信息流的“Moodle”选项卡

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. 在“Microsoft 365集成插件”页中，选择 **“设置”** 选项卡。

1. 选择 **“下载 PowerShell 脚本”** 按钮，并将其作为 ZIP 文件夹保存到本地计算机。

1. 从 ZIP 文件准备 PowerShell 脚本，如下所示：

    1. 下载并提取 `Moodle-AzureAD-Powershell.zip` 文件。
    1. 打开提取的文件夹。
    1. 右键单击该 `Moodle-AzureAD-Script.ps1` 文件并选择 **“属性**”。
    1. 在属性窗口的“**常规**”选项卡下，选中`Unblock`位于窗口底部 **的安全** 属性旁边的复选框。
    1. 选择“**确定**”。
    1. 将目录路径复制到提取的文件夹。

1. 以管理员身份运行 PowerShell：

    1. 选择“开始”。
    1. 键入 PowerShell。
    1. 右键单击 **Windows PowerShell**。
    1. 选择 **“以管理员身份运行**”。

1. 通过键入 `cd .../.../Moodle-AzureAD-Powershell` 目录路径的位置 `.../...` ，导航到解压缩的目录。

1. 执行 PowerShell 脚本：

    1. 输入 `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`。
    1. 输入 `./Moodle-AzureAD-Script.ps1`。
    1. 在弹出窗口中登录到Microsoft 365管理员帐户。
    1. 输入 Azure AD 应用程序的名称，例如 Moodle 或 Moodle 插件。
    1. 输入 Moodle 服务器的 URL。
    1. 复制脚本生成 **的应用程序 ID (`AppID`)** 和 **应用程序密钥 (`Key`)** 并保存它们。

1. 接下来，必须添加和添加`AppID``Key`到Microsoft 365 Moodle 插件。 返回到插件管理页，站点管理>插件> Microsoft 365集成。

1. 在 **“设置”** 选项卡上 `AppID` ，添加之前复制的选项 `Key` 卡，然后选择 **“保存更改**”。 页面刷新后，可以看到新的“**选择连接”部分。**

1. 在 **“选择连接”方法** 中，选择标记为 **“默认**”的复选框，然后再次选择 **“保存更改** ”。

1. 页面刷新后，可以看到另一个新部分 **管理员同意&其他信息**。
    1. 选择 **“提供管理员同意**”链接，输入Microsoft 365全局管理员凭据，然后 **接受** 以授予权限。
    1. 在 **Azure AD 租户** 字段旁边，选择“ **检测”** 按钮。
    1. 在 **OneDrive for Business URL** 旁边，选择 **“检测”** 按钮。
    1. 填充字段后，再次选择 **“保存更改** ”按钮。

1. 选择 **“更新”** 按钮以验证安装，然后选择 **“保存更改**”。

1. 在 Moodle 服务器和 Azure AD 之间同步用户。 首先，请执行以下操作：

    > [!NOTE]
    > 根据你的环境，你可以在此阶段选择不同的选项。

1. 在 Moodle 服务器和 Azure AD 之间同步用户。 根据你的环境，你可以在此阶段选择不同的选项。 首先，请执行以下操作：
    1. 切换到 **“同步设置”选项卡**。

    1. 在 **“使用 Azure AD 同步用户** ”部分中，选择适用于环境的复选框。 必须选择以下内容：  

        ✔ 在 Moodle 中为 Azure AD 中的用户创建帐户。

        ✔ 为 Azure AD 中的用户更新 Moodle 中的所有帐户。

    1. 在 **“用户创建限制** ”部分中，可以设置筛选器以限制同步到 Moodle 的 Azure AD 用户。
    1. 用户 **字段映射** 部分允许自定义 Azure AD 到 Moodle 用户配置文件字段映射。
    1. 在 **“Teams同步**”部分中，可以选择为现有 Moodle 课程的某些或全部课程自动创建组（例如团队）。

13. 若要验证 [cron](https://docs.moodle.org/310/en/Cron) 作业并在第一次运行时手动运行它们，请在 **“使用 Azure AD 同步用户**”部分中选择 **“计划任务管理”页** 链接。 这会转到 **“计划任务”** 页。

    1. 向下滚动并找到 **具有 Azure AD 作业的同步用户** ，然后选择 **“立即运行**”。
    1. 如果选择基于现有课程创建组，也可以 **在Microsoft 365作业中运行“创建用户组**”。

    > [!NOTE]
    >
    > Moodle [Cron](https://docs.moodle.org/310/en/Cron) 根据任务计划运行。 默认计划为每天一次。 但是，cron 必须更频繁地运行才能使所有内容保持同步。

1. 返回到插件管理页、**站点管理>插件> Microsoft 365集成**，然后选择 **Teams 设置** 页。

1. 在 **Teams 设置** 页上，配置所需的设置以启用Teams应用集成。

    1. 若要启用 **OpenID 连接**，请选择 **“管理身份验证”** 链接，并在 **OpenId 连接** 行上选择眼睛图标（如果不可用）。
    1. 若要启用帧嵌入，请选择 **HTTP 安全** 链接，然后选中 **“允许帧嵌入**”旁边的复选框。
    1. 若要启用启用 Moodle API 功能的 Web 服务，请选择 **“高级功能** ”链接，然后确保选中 **“启用 Web 服务”** 旁边的复选框。
    1. 若要为Microsoft 365启用外部服务，请选择 **外部服务** 链接，然后：  

        ✔ 在 **Moodle Microsoft 365 Webservices 行上** 选择 **“编辑**”。

        ✔ 选择 **“启用”** 旁边的复选框，然后选择 **“保存更改”**

    1. 编辑经过身份验证的用户权限，以允许他们创建 Web 服务令牌。

        ✔ 选择 **“编辑角色经过身份验证的用户** ”链接。

        ✔ 向下滚动并找到 **“创建 Web 服务令牌** ”功能，然后选择“ **允许** ”复选框。

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a>3. 将 Moodle 助手机器人部署到 Azure

免费的穆德尔助理机器人Microsoft Teams帮助教师和学生回答有关他们的课程，作业，成绩和其他信息在穆德尔的问题。 机器人还会向Teams中的学生和教师发送 Moodle 通知。 机器人是 Microsoft 维护的开源项目，可在[GitHub](https://github.com/microsoft/Moodle-Teams-Bot)上使用。

> [!NOTE]
>
> * 将资源部署到 Azure 订阅。 所有资源都是使用 **免费** 层配置的。 根据机器人的使用情况，可能需要缩放这些资源。
>
> * 若要使用没有机器人的 Moodle 选项卡，请跳到 [4](#4-deploy-your-microsoft-teams-app)。

### <a name="moodle-bot-information-flow"></a>Moodle 机器人信息流

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

若要安装机器人，必须在 [Microsoft 标识平台](https://identity.microsoft.com/Landing)上注册它。 这样机器人就可以对 Microsoft 终结点进行身份验证。

注册机器人：

1. 转到插件管理页，然后选择 **“插件**”。 在 **“Microsoft 365集成**”下，选择 **“Teams 设置**”选项卡。

1. 选择 **Microsoft 应用程序注册门户** 链接并使用 Microsoft ID 登录。

1. 输入应用的名称，例如 MoodleBot，然后选择 **“创建”** 按钮。

1. 复制 **应用程序 ID** 并将其粘贴到 **Team 设置** 页上的 **机器人应用程序 ID** 字段中。

1. 选择 **“生成新密码”** 按钮。 复制生成的密码并将其粘贴到 **Team 设置** 页上的 **Bot Application Password** 字段中。

1. 滚动到窗体底部，然后选择 **“保存更改**”。

生成应用程序 ID 和密码后，将机器人部署到 Azure：

> [!div class="checklist"]
>
> * 选择 **“部署到 Azure**”，并在 **Teams 设置** 页上使用必需的信息（例如机器人应用程序 ID、机器人应用程序密码和 Moodle 机密）完成表单。 Azure 信息位于 **“设置** ”页上。
> * 完成窗体后，选中该复选框以同意条款和条件。
> * 选择 **“购买**”。 所有 Azure 资源都部署到免费层。

资源完成部署到 Azure 后，必须使用消息传送终结点配置Microsoft 365 Moodle 插件。 必须从 Azure 中的机器人获取终结点：

1. 登录到 [Microsoft Azure 门户](https://portal.azure.com)。

1. 在左窗格中，选择 **“资源组** ”，然后在部署机器人时选择使用或创建的资源组。

1. 从组中的资源列表中选择 **WebApp 机器人** 资源。

1. 从“**概述**”部分复制 **消息传送终结点**。

1. 在 Moodle 中，打开 **Microsoft 365** Moodle 插件的“团队设置”页面。

1. 在 **Bot Endpoint** 字段中，粘贴复制的 URL 并将单词 *消息* 更改为 *Webhook*。 URL 必须如下所示： `https://botname.azurewebsites.net/api/webhook`

1. 选择“保存更改”。

1. 保存更改后，返回到 **“团队设置**”选项卡，选择 **“下载清单文件”** 按钮，并将应用清单包保存到计算机以供进一步使用。

## <a name="4-deploy-your-microsoft-teams-app"></a>4. 部署Microsoft Teams应用

将机器人部署到 Azure 并配置为与 Moodle 服务器通信后，必须部署Microsoft Teams应用。 为此，必须加载上一步中从 Microsoft 365 Moodle 插件团队设置页下载的应用清单文件。

安装应用之前，必须确保启用外部应用和上传应用。 有关详细信息，请参阅[准备Microsoft 365租户](../concepts/build-and-test/prepare-your-o365-tenant.md)。

若要部署应用，请执行以下操作：

1. 打开 **Microsoft Teams**。

1. 选择导航栏左下方区域上的 **“应用** ”图标。

1. 从选项列表 **中选择Upload自定义应用** 链接。

   > [!NOTE]
   > 如果以全局管理员身份登录，则必须可以选择将应用上传到组织的应用目录，否则只能为你所属团队加载应用。

4. 选择之前下载的 `manifest.zip` 包，然后选择 **“保存**”。 如果尚未下载应用清单包，则可以从 Moodle 中插件配置页的 **“团队设置**”选项卡下载。

安装应用后，可以将选项卡添加到有权访问的任何通道。 为此，请导航到通道，选择 **加号** () ➕符号，然后从列表中选择应用。 按照提示完成将 Moodle 课程选项卡添加到频道。

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a>5. 允许在Microsoft Teams中自动创建 Moodle 选项卡

尽管 Moodle 选项卡是在Microsoft Teams中手动创建的，但你可以决定在从课程同步创建团队时自动创建它们。 为此，必须在 Moodle 中配置上传Microsoft Teams应用的 ID。

若要允许自动创建 Moodle 选项卡，请执行以下操作：

1. 打开 Microsoft Teams。

1. 从左下窗格中选择“应用”图标。

1. 找到上传的 **Moodle 应用** >选择 **选项** 图标>选择 **复制链接**。

1. 在文本编辑器中，粘贴复制的内容。 它必须包含 URL，例如 `https://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff`。 复制 URL 的最后一部分，例如`00112233-4455-6677-8899-aabbccddeeff`，这是Microsoft Teams应用的 ID。

1. 在 Moodle 中，从 **Microsoft 365 Moodle** 插件配置页打开Teams Moodle 应用选项卡。

1. 将Microsoft Teams应用的 ID 粘贴到 Moodle 应用 ID 字段中，并保存更改。

同步 Moodle 课程后，Teams自动在团队中安装 Moodle 应用，在 Teams 的“常规”频道中创建一个 Moodle 选项卡，并将其配置为包含从中同步的 Moodle 课程的课程页面。 现在可以直接从Teams开始使用 Moodle 课程。

> [!NOTE]
> 若要与我们共享任何功能请求或反馈，请访问我们的 [“用户语音”页面](https://support.microsoft.com/en-us/office/uservoice-pages-430e1a78-e016-472a-a10f-dc2a3df3450a)。

## <a name="see-also"></a>另请参阅

* [集成 web 应用](~/samples/integrate-web-apps-overview.md)
* [穆德尔](https://moodle.org/)
* [Moodle 文档](https://docs.moodle.org/34/en/Installing_plugins)。
