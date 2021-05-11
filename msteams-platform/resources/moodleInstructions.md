---
title: 安装 Moodle LMS
description: 如何安装和配置适用于 Windows 的一Microsoft Teams
keywords: Teams一流应用集成插件
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 2a99acbe9bc618ea940af3bbe898b30d342ad0cf
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058353"
---
# <a name="install-moodle-lms"></a>安装 Moodle LMS

在 LMS 中，一个受欢迎的开放源代码 (系统) 。 现在，它与 Microsoft Teams。 此集成可帮助教师和教师协作处理一些与开发方案课程有关的问题，提出有关成绩和作业的问题，并直接在 Teams。

为了帮助 IT 管理员轻松设置此集成，Microsoft 365功能更新 Open-source Microsoft 365 Plugin：

* 使用 Azure AD Azure Active Directory [ (自动](https://azure.microsoft.com/services/active-directory/)注册 Your Moodle) 。
* 只需单击一下即可将你的 Your Assistant bot 部署到 Azure。
* 自动预配团队以及自动同步所有或选择"一流"课程的团队注册。
* 自动将"一页"选项卡和"将一个将一位"的"将一位"助手自动安装到每个同步的团队中。

若要详细了解此集成提供的功能，请参阅 Microsoft Teams[和一个。](https://education.microsoft.com/resource/3dffb3a8)

## <a name="prerequisites"></a>先决条件

以下是安装和配置一个与设置一个组织应用程序有关的先决条件： 

1. 获取管理员凭据。

1. Azure AD 管理员凭据。

1. 可在其中创建新资源的 Azure 订阅。

**安装和配置一个一流应用程序** 

执行下列步骤以安装和配置一个在部署中安装并配置一个组织应用程序： 

## <a name="1-install-the-microsoft-365-moodle-plugins"></a>1. 安装 Microsoft 365 Plugins

企业中的一Microsoft Teams由开放源代码和[Microsoft 365插件集提供支持](https://github.com/Microsoft/o365-moodle)。 若要在将插件安装到你的一台将 Plugin 安装在你的一台开发工具服务器中，必须安装以下应用程序：

1. 一 [个当前稳定版本的一个，即，一个 Stablele 版本](https://download.moodle.org/releases/latest/)。

1. 将一[个 连接](https://moodle.org/plugins/auth_oidc)和 Microsoft 365[集成](https://moodle.org/plugins/local_o365)插件下载并保存到本地计算机。

   > [!NOTE]
   > 安装 OpenID 连接和Microsoft 365集成插件是集成Teams要求。 此外，[强烈建议Microsoft 365 Teams](https://moodle.org/plugins/theme_boost_o365teams)主题插件。

1. 以管理员角色登录到 Your Moodle server，然后从左侧导航面板设置[网站](https://docs.moodle.org/22/en/Settings_block)管理"块中选择"网站管理"。

1. 选择 **"插件"** 选项卡，然后选择"**安装插件"。**

1. 从" **从 ZIP 文件安装插件"部分** ，选择 **"选择文件"** 按钮。

1. Select **Upload a file** option from the left navigation， browse for the file that you downloaded， and select Upload this **file**.

1. 从左侧 **导航面板** 中选择"网站管理"以返回到管理员仪表板。 向下滚动到"**本地插件"** 并选择"Microsoft 365 **集成"** 链接。 

> [!IMPORTANT]
>
> * 在整个Microsoft 365返回到这组页面时，请让 Your Microsoft 365 Plugin Configuration page 在单独的浏览器选项卡中打开。  <br/><br/>
> * 如果你没有现有的一个一流网站，你可以查看 [Azure](https://github.com/azure/moodle) 存储库上的将一个在 Azure 存储库上快速部署一个一流实例并根据需要自定义它。

## <a name="2-configure-the-connection-between-the-microsoft-365-plugin-and-azure-active-directory-azure-ad"></a>2. 配置 Azure AD Microsoft 365和 azure AD Azure Active Directory (之间的连接) 

你必须在 Azure AD 中将一个操作注册为应用程序。 使用 PowerShell 脚本完成此过程。 PowerShell 脚本为 Microsoft 365 租户设置新的 Azure AD 应用程序，Microsoft 365使用。 该脚本会预配 Microsoft 365 租户的应用，为预配的应用设置所需的回复 URL 和权限，并返回 `AppID` 和 `Key` 。 可以使用生成的 和 在 Your Microsoft 365 Plugin setup page 中，使用 `AppID` `Key` Azure AD 配置你的一个将你的一个将你的一个部署服务器网站。

> [!IMPORTANT]
> * PowerShell 脚本没有使用最新的配置项进行更新，因此你必须按照在一个 [3.8.0.4 和 3.9.1、3.8.0.5](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) 和 [3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) 发行版页面中概述的步骤手动完成配置。 </br></br>
> * 若要查看 PowerShell 脚本正在自动执行的详细手动步骤，请参阅 [将你的一个一体机实例注册为应用程序](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)。

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a>用于信息流的"Microsoft Teams选项卡

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. 从"Microsoft 365集成插件"页中，选择"设置 **"** 选项卡。

1. 选择" **下载 PowerShell 脚本"** 按钮，并将其保存到本地计算机。

1. 必须从 ZIP 文件准备 PowerShell 脚本。 执行以下步骤以从 ZIP 文件准备 PowerShell 脚本：

    1. 下载并解压缩 `Moodle-AzureAD-Powershell.zip` 文件。
    1. 打开提取的文件夹。
    1. 右键单击文件 `Moodle-AzureAD-Script.ps1` ，然后选择属性。
    1. 在" **属性** "窗口的"常规"选项卡下，选中位于窗口底部的 `Unblock` **Security** 属性旁边的框。
    1. 选择“**确定**”。
    1. 将目录路径复制到提取的文件夹。

1. 以管理员角色运行 PowerShell：

    1. 选择“开始”。
    1. 键入 PowerShell。
    1. 右键单击"Windows PowerShell"。
    1. 选择 **"以管理员角色运行"。**

1. 通过键入 where 是目录的路径，导航到 `cd .../.../Moodle-AzureAD-Powershell` `.../...` 解压缩目录。

1. 执行 PowerShell 脚本：

    1. 输入 `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` 。
    1. 输入 `./Moodle-AzureAD-Script.ps1` 。
    1. 在弹出窗口中Microsoft 365你的管理员帐户。
    1. 输入 Azure AD 应用程序名称 (，例如，在 Azure AD 应用程序名称中输入一) 。
    1. 输入 Your Your Moodle 服务器的 URL。
    1. 复制 **脚本生成的****应用程序** ID 和应用程序密钥并保存它们。

1. 接下来，你必须将 `AppID` 和 添加到 `Key` "Microsoft 365 Plugin"中。 返回到插件管理页。 流程为：网站管理➡插件➡ Microsoft 365集成。

1. 在"**安装**"选项卡上，添加之前复制的应用程序 **ID** 和应用程序密钥，然后选择"保存 **更改"。**

1. 刷新页面后，可以看到新部分选择 **连接方法**。 选中标记为"默认 **"的复选框** ，然后再次 **选择"保存更改** "。

1. 刷新页面后，你可以看到另一个新部分管理员同意& **其他信息**。
    1. 选择 **"提供管理员同意**"链接，Microsoft 365全局管理员凭据，然后 **接受** 以授予权限。
    1. 在 **"Azure AD 租户** "字段旁边，选择" **检测"** 按钮。
    1. 在 URL **OneDrive for Business，** 选择"检测 **"** 按钮。
    1. 填充字段后，再次选择 **"保存更改"** 按钮。

1. 选择"**更新"** 按钮以验证安装，然后选择"**保存更改"。**

1. 在将用户同步到你的一台将你的服务器与 Azure AD 之间。 根据你的环境，你可以在此阶段选择不同的选项。 首先，请执行以下操作：
    1. 切换到"同步 **设置选项卡**
    1. 在 **"将用户与 Azure AD** 同步"部分中，选中适用于你的环境的复选框。 您必须选择以下选项：  

        ✔ Azure AD 中的用户创建在在一起的帐户。 
        ✔ Azure AD 中的用户更新在在一起的所有帐户。  

    1. 在 **"用户创建限制** "部分，可以设置筛选器以限制同步到一台的 Azure AD 用户。
    1. 通过 **"用户字段映射** "部分，你可以自定义 Azure AD 到一些用户个人资料字段映射。
    1. 在 **"Teams同步**"部分，可以选择自动创建组，例如某些或所有现有一些（或全部）的 Teams。

> [!NOTE]
> 将按照任务 [计划](https://docs.moodle.org/310/en/Cron) 运行一个将运行一个在一起。 默认计划为每天一次。 但是，cron 必须更频繁地运行，以保持所有内容同步。

13. 若要验证 [cron](https://docs.moodle.org/310/en/Cron)作业并首次运行时手动运行它们，请选择"将用户与 **Azure AD** 同步"部分中的"计划任务管理"页链接。 这会将您带至 **"计划任务"** 页。

    1. 向下滚动并查找"使用 **Azure AD 同步用户"** 作业，然后选择"**立即运行"。**
    1. 如果选择基于现有课程创建组，还可以在作业中运行创建 **Microsoft 365** 组。

1. 返回到插件管理页。 导航流为：网站管理➡插件➡ Microsoft 365 Integratio。 然后 **，选择Teams 设置** 页。 必须配置某些设置才能启用Teams集成。

    1. 若要启用 **OpenID 连接，** 请选择"管理身份验证"链接，并选择 **OpenId** 连接（如果显示为灰色）上的目视图标。
    1. 启用帧嵌入。 选择 **"HTTP 安全性"** 链接，然后选中"允许嵌入框架 **"旁边的复选框**。
    1. 启用 Web 服务，从而启用一些用户 API 功能。 选择" **高级功能"** 链接，然后确保选中"启用 **Web** 服务"旁边的复选框。
    1. 为外部服务启用Microsoft 365。 选择" **外部服务"** 链接，然后下一步：  

        ✔在 **"Webservices"行Microsoft 365选择"编辑**"。   
        ✔选中"已启用"旁边的复选框，然后选择"**保存更改"**

    1. 编辑经过身份验证的用户权限，以允许他们创建 Web 服务令牌。 选择 **"编辑角色'经过身份验证的用户'"** 链接。 向下滚动并找到创建 **Web 服务令牌** 功能并标记 **"允许"** 复选框。

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a>3. 将用户助理机器人部署到 Azure

适用于教育的免费一Microsoft Teams自动程序可帮助教师和学生回答有关其课程、作业、成绩和其他在一起的问题。 机器人还会向用户内的学生和教师发送一Teams。 自动程序是由 Microsoft 维护的开放源代码项目，可用于[GitHub。](https://github.com/microsoft/Moodle-Teams-Bot)

> [!NOTE]
> * 在此部分中，你必须将资源部署到 Azure 订阅。 使用免费层配置的所有 **资源** 软件。 根据机器人的使用情况，你可以扩展这些资源。
> * 若要在没有自动程序的情况下使用"操作方式"选项卡，请跳到 [4](#4-deploy-your-microsoft-teams-app)。

### <a name="moodle-bot-information-flow"></a>自动程序信息流

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

若要安装自动程序，必须在 Microsoft 标识平台上 [注册它](https://identity.microsoft.com/Landing)。 这允许机器人针对 Microsoft 终结点进行身份验证。 

**若要注册自动程序**：

1. 转到插件管理页面。 转到 **插件**。 在 **Microsoft 365集成"** 下，选择 **"Teams 设置"** 选项卡。

1. 选择 **"Microsoft 应用程序注册门户** "链接，然后使用 Microsoft ID 登录。

1. 输入你的应用的名称，例如，一个在一起， **然后选择创建按钮** 。

1. 复制应用程序 **ID 并将其** 粘贴到"团队管理"页上的"自动程序应用程序 **ID"设置** 字段中。 

1. 选择" **生成新密码"** 按钮。 复制生成的密码，并将其粘贴到"团队密码"页上的"自动程序应用程序 **设置** 字段中。

1. 滚动到表单底部，然后选择"保存 **更改"。**

生成应用程序 ID 和密码时，下一步是将机器人部署到 Azure：

> [!div class="checklist"]
> * 选择 **"部署到 Azure"** 按钮，然后使用必要的信息完成表单，例如"团队部署"页上的"自动程序应用程序 ID"、自动程序应用程序密码和"设置密码"。 Azure 信息位于"设置 **"页面**) 。 
> * 完成表单后，选中复选框以同意条款和条件。
> * 选择" **购买"** 按钮。 所有 Azure 资源都部署到免费层。

在资源部署到 Azure 后，必须使用消息终结点Microsoft 365一个设置一个与一个"一Microsoft 365一插件。 你必须从 Azure 中的机器人获取终结点：

**使用消息Microsoft 365配置"一个"的"一流"插件**  
1. 登录到 [Azure 门户](https://portal.azure.com)。

1. 在左侧窗格中，选择" **资源组** "，并选择你使用或创建的资源组，同时部署机器人。

1. 从 **组的资源列表中选择 WebApp** Bot 资源。

1. 从" **概述"部分** 复制 **消息终结点** 。

1. 在"在将 **"设置"** 中，打开"Microsoft 365插件"的"团队Microsoft 365页面。

1. 在 **自动程序终结点** 字段中粘贴你刚刚复制的 URL，然后将单词 *消息* 更改为 *webhook*。 URL 现在应如下所示： `https://botname.azurewebsites.net/api/webhook`

1. 选择 **"保存更改"。**

1. 保存更改后，返回到"团队设置选项卡，选择"下载清单文件"按钮，将应用清单包保存到计算机以进一步使用。

## <a name="4-deploy-your-microsoft-teams-app"></a>4. 部署Microsoft Teams应用程序

在将机器人部署到 Azure 并配置为与你的 Talkle 服务器通信后，你必须部署你的 Microsoft Teams 应用。 为此，你必须加载从上一步中从"Microsoft 365 Plugin Team 设置页面下载的应用清单文件。

在安装应用之前，必须确保启用外部应用和上传应用。 为此，可以按照准备租户Teams[中的Microsoft 365步骤](../concepts/build-and-test/prepare-your-o365-tenant.md)操作。 你可以执行以下步骤来部署应用： 

**部署应用**

1. 打开 **Microsoft Teams**。 

1. 选择 **导航** 栏左下角区域的应用图标。

1. 从 **Upload选择**"自定义应用"链接。

   > [!NOTE]
   > 如果以全局管理员身份登录，则必须选择将应用程序上载到组织的应用程序目录，否则只能为作为成员的团队加载应用程序。

4. 选择 `manifest.zip` 之前下载的程序包，然后选择保存。  如果尚未下载应用清单包，可以从在将插件配置页的 **"team 设置"** 选项卡中下载。

现在，你已安装应用，你可以将选项卡添加到你有权访问的任何频道。 为此，请导航到通道，选择 **加 (➕) 符号** ，然后从列表中选择你的应用。 按照提示完成向频道添加 Your Moodle 课程选项卡。

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a>5. 允许自动在 Microsoft Teams

尽管在课程同步中手动创建"Microsoft Teams"选项卡，但你可以决定在通过课程同步创建团队时自动创建它们。 为此，你必须在一台位于Microsoft Teams中配置已上传应用 ID：

1. 打开 Microsoft Teams。

1. 从导航栏的左下角区域选择"应用"图标。

1. 找到已上传 **的一➡** 选择 **选项** 图标➡选择 **复制链接**。

1. 在文本编辑器中，粘贴复制的内容。 它必须包含 URL，如 ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff。 复制 URL 的最后一部分，例如 ，这是应用Microsoft Teams `00112233-4455-6677-8899-aabbccddeeff` ID。

1. 在"在一个 **Teams，从你的"Your Microsoft 365** Plugin configuration"页面打开"Your Microsoft 365一应用"选项卡。

1. 将应用 ID 粘贴到 Microsoft Teams 应用 ID 字段中，并保存更改。

同步一个一流课程后，Microsoft Teams 会自动在团队中安装一个一流应用，在 Teams 的常规频道中创建一个"一般"选项卡，并对其进行配置以包含用于同步其的一流课程的课程页面。 现在可以直接从你的组织开始使用你的Microsoft Teams。

若要与我们共享任何功能请求或反馈，请访问我们的用户 [语音页面](https://microsoftteams.uservoice.com/forums/916759-moodle)。

## <a name="see-also"></a>另请参阅

- [集成 web 应用](~/samples/integrate-web-apps-overview.md)

- [一位](https://moodle.org/)

- [一个文档](https://docs.moodle.org/34/en/Installing_plugins)。
