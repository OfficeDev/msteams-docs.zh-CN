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
# <a name="installing-the-moodle-integration-with-microsoft-teams"></a><span data-ttu-id="3a25d-104">安装与 Microsoft Teams 的一体式集成</span><span class="sxs-lookup"><span data-stu-id="3a25d-104">Installing the Moodle integration with Microsoft Teams</span></span>

<span data-ttu-id="3a25d-105">作为 LMS (的热门开源学习管理系统[) ，现在](https://moodle.org/)与 Microsoft Teams 集成在一起。</span><span class="sxs-lookup"><span data-stu-id="3a25d-105">[Moodle](https://moodle.org/), a popular open-source Learning Management System (LMS), is now integrated with Microsoft Teams.</span></span> <span data-ttu-id="3a25d-106">此集成可帮助教师和教师围绕 Teams 课程展开协作，提出有关成绩和作业的问题，并直接在 Teams 中通过通知保持更新。</span><span class="sxs-lookup"><span data-stu-id="3a25d-106">This integration helps educators and teachers collaborate around Moodle courses, ask questions about grades and assignments, and stay updated with notifications directly within Teams.</span></span>

<span data-ttu-id="3a25d-107">为了帮助 IT 管理员轻松设置此集成，我们已使用以下功能更新了开放源代码 Microsoft 365 的"编辑插件"：</span><span class="sxs-lookup"><span data-stu-id="3a25d-107">To help IT admins easily set this integration up, we have updated our open-source Microsoft 365 Moodle Plugin with the following capabilities:</span></span>

* <span data-ttu-id="3a25d-108">使用 Azure AD ([Azure Active Directory](https://azure.microsoft.com/services/active-directory/) 自动) 。</span><span class="sxs-lookup"><span data-stu-id="3a25d-108">Auto-registration of your Moodle server with [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (Azure AD).</span></span>
* <span data-ttu-id="3a25d-109">只需单击一下，即可将你的"Your Moodle 助手"机器人部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="3a25d-109">One-click deployment of your Moodle Assistant bot to Azure.</span></span>
* <span data-ttu-id="3a25d-110">自动预配团队，并自动同步所有或选择"一心"课程的团队注册。</span><span class="sxs-lookup"><span data-stu-id="3a25d-110">Auto-provisioning of teams and auto-synchronization of team enrollments for all or select Moodle courses.</span></span>
* <span data-ttu-id="3a25d-111">自动将一个"一致"选项卡和一个"协调人"助手自动安装到每个同步的团队中。</span><span class="sxs-lookup"><span data-stu-id="3a25d-111">Auto-installation of the Moodle tab and the Moodle assistant bot into each synchronized team.</span></span>

<span data-ttu-id="3a25d-112">若要详细了解此集成提供的功能 *，请参阅*[Microsoft Teams 和 Teams。](https://education.microsoft.com/resource/3dffb3a8)</span><span class="sxs-lookup"><span data-stu-id="3a25d-112">To learn more about the functionality this integration provides, please *see* [Microsoft Teams and Moodle](https://education.microsoft.com/resource/3dffb3a8).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a25d-113">先决条件</span><span class="sxs-lookup"><span data-stu-id="3a25d-113">Prerequisites</span></span>

<span data-ttu-id="3a25d-114">为了安装和配置此应用程序，你将需要：</span><span class="sxs-lookup"><span data-stu-id="3a25d-114">In order to install and configure this application you'll need:</span></span>

1. <span data-ttu-id="3a25d-115">管理员凭据。</span><span class="sxs-lookup"><span data-stu-id="3a25d-115">Moodle administrator credentials.</span></span>

1. <span data-ttu-id="3a25d-116">Azure AD 管理员凭据。</span><span class="sxs-lookup"><span data-stu-id="3a25d-116">Azure AD administrator credentials.</span></span>

1. <span data-ttu-id="3a25d-117">可在其中创建新资源的 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="3a25d-117">An Azure subscription where you can create new resources.</span></span>

## <a name="step-1-install-the-microsoft-365-moodle-plugins"></a><span data-ttu-id="3a25d-118">步骤 1：安装 Microsoft 365 的一流插件</span><span class="sxs-lookup"><span data-stu-id="3a25d-118">Step 1: Install the Microsoft 365 Moodle Plugins</span></span>

<span data-ttu-id="3a25d-119">Microsoft Teams 中的其集成由开放源代码 [Microsoft 365 的一个 Pluginle 插件集提供支持](https://github.com/Microsoft/o365-moodle)。</span><span class="sxs-lookup"><span data-stu-id="3a25d-119">The Moodle integration in Microsoft Teams is powered by the open source [Microsoft 365 Moodle plugin set](https://github.com/Microsoft/o365-moodle).</span></span> <span data-ttu-id="3a25d-120">若要在 Your Moodle 服务器中安装插件，你需要安装以下内容：</span><span class="sxs-lookup"><span data-stu-id="3a25d-120">To install the plugin in your Moodle server you need to have the following installed:</span></span>

1. <span data-ttu-id="3a25d-121">A [current stable version of Moodle](https://download.moodle.org/releases/latest/).</span><span class="sxs-lookup"><span data-stu-id="3a25d-121">A [current stable version of Moodle](https://download.moodle.org/releases/latest/).</span></span>

1. <span data-ttu-id="3a25d-122">已下载和 [保存到本地计算机的一个将一体式 OpenID Connect](https://moodle.org/plugins/auth_oidc) 和 Microsoft [365](https://moodle.org/plugins/local_o365) 集成插件。</span><span class="sxs-lookup"><span data-stu-id="3a25d-122">The Moodle [OpenID Connect](https://moodle.org/plugins/auth_oidc) and the [Microsoft 365 Integration](https://moodle.org/plugins/local_o365) plugins downloaded and saved to your local computer.</span></span>

> [!NOTE]
> <span data-ttu-id="3a25d-123">Teams 集成需要安装 OpenID Connect 和 Microsoft 365 集成插件。</span><span class="sxs-lookup"><span data-stu-id="3a25d-123">Installing the OpenID Connect and Microsoft 365 Integration plugins are required for the Teams integration.</span></span> <span data-ttu-id="3a25d-124">此外， [强烈建议使用 Microsoft 365 Teams 主题](https://moodle.org/plugins/theme_boost_o365teams) 插件。</span><span class="sxs-lookup"><span data-stu-id="3a25d-124">Additionally the [Microsoft 365 Teams Theme](https://moodle.org/plugins/theme_boost_o365teams) plugin is highly recommended.</span></span>

3. <span data-ttu-id="3a25d-125">以管理员角色登录到 Your Moodle 服务器，然后从左侧[](https://docs.moodle.org/22/en/Settings_block)导航面板中的"设置"块中选择"网站管理"。</span><span class="sxs-lookup"><span data-stu-id="3a25d-125">Login to your Moodle server as an administrator and select **Site administration** from the [Settings block](https://docs.moodle.org/22/en/Settings_block) located in the left navigation panel.</span></span>

1. <span data-ttu-id="3a25d-126">选择 **"插件"** 选项卡，然后选择"**安装插件"。**</span><span class="sxs-lookup"><span data-stu-id="3a25d-126">Select the **Plugins** tab, and then choose **Install plugins**.</span></span>

1. <span data-ttu-id="3a25d-127">在 **"从 ZIP 文件安装** 插件"部分，选择 **"选择文件"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="3a25d-127">Under the **Install plugin from ZIP file** section select the **Choose a file** button.</span></span>

1. <span data-ttu-id="3a25d-128">Select the **Upload a file** options from the left navigation， browse for the file you downloaded above， and choose Upload this **file.**</span><span class="sxs-lookup"><span data-stu-id="3a25d-128">Select the **Upload a file** options from the left navigation, browse for the file you downloaded above, and choose **Upload this file**.</span></span>

1. <span data-ttu-id="3a25d-129">从 **左侧导航面板** 中选择"网站管理"选项以返回到管理员仪表板。</span><span class="sxs-lookup"><span data-stu-id="3a25d-129">Select the **Site administration** option from the left navigation panel to return to your admin dashboard.</span></span> <span data-ttu-id="3a25d-130">向下滚动到 **本地插件并选择** **Microsoft 365 集成** 链接。</span><span class="sxs-lookup"><span data-stu-id="3a25d-130">Scroll down to the **Local plugins** and select the **Microsoft 365 Integration** link.</span></span> <span data-ttu-id="3a25d-131">**在整个安装过程中，保持此配置页在单独的浏览器选项卡中打开**。</span><span class="sxs-lookup"><span data-stu-id="3a25d-131">**Keep this configuration page open in a separate browser tab throughout the installation process**.</span></span>

<span data-ttu-id="3a25d-132">你可以找到有关 How to install Moodle 插件在 [Pressle 文档中详细信息](https://docs.moodle.org/34/en/Installing_plugins)。</span><span class="sxs-lookup"><span data-stu-id="3a25d-132">You can find more information on how to install Moodle plugins in the [Moodle documentation](https://docs.moodle.org/34/en/Installing_plugins).</span></span>

> [!IMPORTANT]
>
> * <span data-ttu-id="3a25d-133">在单独的浏览器选项卡中保持 Microsoft 365 管理插件配置页面打开 ， 你将在整个过程中返回到这组页面。</span><span class="sxs-lookup"><span data-stu-id="3a25d-133">Keep your Microsoft 365 Moodle Plugin configuration page open in a separate browser tab — you'll be returning to this set of pages throughout the process.</span></span>  <br/><br/>
>* <span data-ttu-id="3a25d-134">如果你没有现有的一个一流网站，可以在 [Azure](https://github.com/azure/moodle) 存储库上查看一下其，你可以快速部署一个一个其实例并根据需要对其进行自定义。</span><span class="sxs-lookup"><span data-stu-id="3a25d-134">If you don't have an existing Moodle site, you can check out Moodle on Azure [repo](https://github.com/azure/moodle) where you can quickly deploy a Moodle instance and customize it to your needs.</span></span>

## <a name="step-2-configure-the-connection-between-the-microsoft-365-plugin-and-azure-active-directory-azure-ad"></a><span data-ttu-id="3a25d-135">步骤 2：配置 Microsoft 365 插件与 Azure AD (Azure Active Directory) </span><span class="sxs-lookup"><span data-stu-id="3a25d-135">Step 2: Configure the connection between the Microsoft 365 plugin and Azure Active Directory (Azure AD)</span></span>

<span data-ttu-id="3a25d-136">接下来，你需要在 Azure AD 中将一个开发平台注册为应用程序。</span><span class="sxs-lookup"><span data-stu-id="3a25d-136">Next, you'll need to register Moodle as an application in your Azure AD.</span></span> <span data-ttu-id="3a25d-137">我们提供了 PowerShell 脚本来帮助你完成此过程。</span><span class="sxs-lookup"><span data-stu-id="3a25d-137">We've provided a PowerShell script to help you complete this process.</span></span> <span data-ttu-id="3a25d-138">PowerShell 脚本会为 Microsoft 365 租户设置新的 Azure AD 应用程序，Microsoft 365 的 Pluginle 插件将使用该应用程序。</span><span class="sxs-lookup"><span data-stu-id="3a25d-138">The PowerShell script provisions a new Azure AD application for your Microsoft 365 tenant, which will be used by the Microsoft 365 Moodle Plugin.</span></span> <span data-ttu-id="3a25d-139">该脚本将为 Microsoft 365 租户设置应用，为预配的应用设置所需的回复 URL 和权限，并返回 `AppID` 和 `Key` 。</span><span class="sxs-lookup"><span data-stu-id="3a25d-139">The script will provision the app for your Microsoft 365 tenant, set up the required reply URLs and permissions for the provisioned app, and return the `AppID` and `Key`.</span></span> <span data-ttu-id="3a25d-140">可以使用生成的和在 `AppID` Microsoft 365 的"管理插件"设置页中，使用 Azure AD 配置 `Key` Your Your Moodle 服务器网站。</span><span class="sxs-lookup"><span data-stu-id="3a25d-140">You can use the generated `AppID` and `Key` in your Microsoft 365 Moodle Plugin setup page to configure your Moodle server site with Azure AD.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="3a25d-141">PowerShell 脚本不会使用最新的配置项进行更新，因此，您必须按照在一个 [3.8.0.4 和 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) 以及 [3.8.0.5 和 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) 发行页面中概述的步骤手动完成配置。</span><span class="sxs-lookup"><span data-stu-id="3a25d-141">The PowerShell script is not updated with the latest configuration items, so you'll have to complete the configuration manually following the steps outlined in the Moodle [3.8.0.4 and 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) and [3.8.0.5 and 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) release pages.</span></span> </br></br>
> <span data-ttu-id="3a25d-142">若要查看 PowerShell 脚本正在自动执行的详细手动步骤，请参阅 *"* 将 [Your Moodle 实例注册为应用程序"。](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)</span><span class="sxs-lookup"><span data-stu-id="3a25d-142">To view the manual steps that the PowerShell script is automating in detail , *see* [Register your Moodle instance as an Application](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application).</span></span>

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a><span data-ttu-id="3a25d-143">Microsoft Teams 信息流的"选择"选项卡</span><span class="sxs-lookup"><span data-stu-id="3a25d-143">The Moodle tab for Microsoft Teams information flow</span></span>

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. <span data-ttu-id="3a25d-144">从 Microsoft 365 集成插件页面选择 **"设置"** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="3a25d-144">From the Microsoft 365 Integration plugin page select the **Setup** tab.</span></span>

1. <span data-ttu-id="3a25d-145">选择 **"下载 PowerShell 脚本"** 按钮，并将其保存到本地计算机。</span><span class="sxs-lookup"><span data-stu-id="3a25d-145">Select the **Download PowerShell Script** button and save it to your local computer.</span></span>

1. <span data-ttu-id="3a25d-146">你需要从 ZIP 文件准备 PowerShell 脚本。</span><span class="sxs-lookup"><span data-stu-id="3a25d-146">You'll need to prepare the PowerShell script from the ZIP file.</span></span> <span data-ttu-id="3a25d-147">为此，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="3a25d-147">To do so:</span></span>

    * <span data-ttu-id="3a25d-148">下载并解压缩 `Moodle-AzureAD-Powershell.zip` 文件。</span><span class="sxs-lookup"><span data-stu-id="3a25d-148">Download and extract the `Moodle-AzureAD-Powershell.zip` file.</span></span>
    * <span data-ttu-id="3a25d-149">打开提取的文件夹。</span><span class="sxs-lookup"><span data-stu-id="3a25d-149">Open the extracted folder.</span></span>
    * <span data-ttu-id="3a25d-150">右键单击 `Moodle-AzureAD-Script.ps1` 该文件，然后选择"**属性"。**</span><span class="sxs-lookup"><span data-stu-id="3a25d-150">Right-click on the `Moodle-AzureAD-Script.ps1` file and select **Properties**.</span></span>
    * <span data-ttu-id="3a25d-151">在 **"** 属性"窗口的"常规"选项卡下，选中位于窗口底部的 Security 属性旁边的 `Unblock` 框。 </span><span class="sxs-lookup"><span data-stu-id="3a25d-151">Under the **General** tab of the Properties window, check the `Unblock` box next to the **Security** attribute located at the bottom of the window.</span></span>
    * <span data-ttu-id="3a25d-152">选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="3a25d-152">Select **OK**.</span></span>
    * <span data-ttu-id="3a25d-153">将目录路径复制到提取的文件夹。</span><span class="sxs-lookup"><span data-stu-id="3a25d-153">Copy the directory path to the extracted folder.</span></span>

1. <span data-ttu-id="3a25d-154">接下来，您将以管理员角色运行 PowerShell：</span><span class="sxs-lookup"><span data-stu-id="3a25d-154">Next you'll run PowerShell as an administrator:</span></span>

    * <span data-ttu-id="3a25d-155">选择“开始”。</span><span class="sxs-lookup"><span data-stu-id="3a25d-155">Select Start.</span></span>
    * <span data-ttu-id="3a25d-156">键入 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="3a25d-156">Type PowerShell.</span></span>
    * <span data-ttu-id="3a25d-157">右键单击Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="3a25d-157">Right-click Windows PowerShell.</span></span>
    * <span data-ttu-id="3a25d-158">选择"以管理员角色运行"。</span><span class="sxs-lookup"><span data-stu-id="3a25d-158">Select "Run as Administrator".</span></span>

1. <span data-ttu-id="3a25d-159">通过键入目录的路径导航到解压缩 `cd .../.../Moodle-AzureAD-Powershell` `.../...` 目录。</span><span class="sxs-lookup"><span data-stu-id="3a25d-159">Navigate to the unzipped directory by typing `cd .../.../Moodle-AzureAD-Powershell` where `.../...` is the path to the directory.</span></span>

1. <span data-ttu-id="3a25d-160">执行 PowerShell 脚本：</span><span class="sxs-lookup"><span data-stu-id="3a25d-160">Execute the PowerShell script:</span></span>

    * <span data-ttu-id="3a25d-161">Enter `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` 。</span><span class="sxs-lookup"><span data-stu-id="3a25d-161">Enter `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`.</span></span>
    * <span data-ttu-id="3a25d-162">Enter `./Moodle-AzureAD-Script.ps1` 。</span><span class="sxs-lookup"><span data-stu-id="3a25d-162">Enter `./Moodle-AzureAD-Script.ps1`.</span></span>
    * <span data-ttu-id="3a25d-163">在弹出窗口中登录到 Microsoft 365 管理员帐户。</span><span class="sxs-lookup"><span data-stu-id="3a25d-163">Login to your Microsoft 365 administrator account in the pop-up window.</span></span>
    * <span data-ttu-id="3a25d-164">输入 Azure AD 应用程序应用程序的名称 (，例如，在) 。</span><span class="sxs-lookup"><span data-stu-id="3a25d-164">Enter the name of the Azure AD Application (e.g., Moodle/Moodle plugin).</span></span>
    * <span data-ttu-id="3a25d-165">输入你的其服务器 URL。</span><span class="sxs-lookup"><span data-stu-id="3a25d-165">Enter the URL for your Moodle server.</span></span>
    * <span data-ttu-id="3a25d-166">复制 **脚本生成的\*\*\*\*应用程序** ID 和应用程序密钥，并保存它们。</span><span class="sxs-lookup"><span data-stu-id="3a25d-166">Copy the **Application ID** and **Application Key** generated by the script and save them.</span></span>

1. <span data-ttu-id="3a25d-167">接下来，你需要将 And 添加到 ` AppID` `Key` Microsoft 365 的"一页"插件。</span><span class="sxs-lookup"><span data-stu-id="3a25d-167">Next you'll need to add the` AppID` and `Key` to the Microsoft 365 Moodle Plugin.</span></span> <span data-ttu-id="3a25d-168">返回到 Microsoft 365 集成 (插件➡插件➡插件) 。</span><span class="sxs-lookup"><span data-stu-id="3a25d-168">Return to the plugin administration page (Site administration ➡ Plugins ➡ Microsoft 365 Integration).</span></span>

1. <span data-ttu-id="3a25d-169">在"**安装**"选项卡上，添加之前复制的应用程序 **ID** 和应用程序密钥，然后选择"**保存更改"。**</span><span class="sxs-lookup"><span data-stu-id="3a25d-169">On the **Setup** tab add the **Application ID** and **Application Key** you copied previously, then select **Save changes**.</span></span>

1. <span data-ttu-id="3a25d-170">刷新页面后，应该会看到新节 **"选择连接方法"。**</span><span class="sxs-lookup"><span data-stu-id="3a25d-170">Once the page refreshes you should see a new section **Choose connection method**.</span></span> <span data-ttu-id="3a25d-171">选中标记为"默认" **的复选框** ，然后再次选择 **"保存** 更改"。</span><span class="sxs-lookup"><span data-stu-id="3a25d-171">Select the checkbox labeled **Default** and then select **Save changes** again.</span></span>

1. <span data-ttu-id="3a25d-172">刷新页面后，你将看到另一个新分区管理员 **同意&其他信息**。</span><span class="sxs-lookup"><span data-stu-id="3a25d-172">Once the page refreshes you will see another new section **Admin consent & additional information**.</span></span>
    * <span data-ttu-id="3a25d-173">选择" **提供管理员同意** "链接，输入 Microsoft 365 全局管理员凭据，然后 **接受** 以授予权限。</span><span class="sxs-lookup"><span data-stu-id="3a25d-173">Select the **Provide Admin Consent** link, enter your Microsoft 365 Global Administrator credentials, then **Accept** to grant the permissions.</span></span>
    * <span data-ttu-id="3a25d-174">在 **"Azure AD 租户"字段** 旁边，选择 **"检测"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="3a25d-174">Next to the **Azure AD Tenant** field select the **Detect** button.</span></span>
    * <span data-ttu-id="3a25d-175">在 **OneDrive for Business URL 旁边，** 选择 **"检测"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="3a25d-175">Next to the **OneDrive for Business URL** select the **Detect** button.</span></span>
    * <span data-ttu-id="3a25d-176">填充字段后，再次选择 **"保存更改"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="3a25d-176">Once the fields populate, select the **Save changes** button again.</span></span>

1. <span data-ttu-id="3a25d-177">选择 **"更新** "按钮以验证安装，然后 **保存更改**。</span><span class="sxs-lookup"><span data-stu-id="3a25d-177">Select the **Update** button to verify the installation, then **Save changes**.</span></span>

1. <span data-ttu-id="3a25d-178">接下来，你需要将用户同步到你的其服务器和 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="3a25d-178">Next, you'll need to synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="3a25d-179">根据你的环境，你可以在此阶段选择不同的选项。</span><span class="sxs-lookup"><span data-stu-id="3a25d-179">Depending on your environment, you may select different options during this stage.</span></span> <span data-ttu-id="3a25d-180">首先，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="3a25d-180">To get started:</span></span>
    * <span data-ttu-id="3a25d-181">切换到" **同步设置"选项卡**</span><span class="sxs-lookup"><span data-stu-id="3a25d-181">Switch to the **Sync Settings tab**</span></span>
    * <span data-ttu-id="3a25d-182">在 **"使用 Azure AD 同步** 用户"部分中，选中适用于你的环境的复选框。</span><span class="sxs-lookup"><span data-stu-id="3a25d-182">In the **Sync users with Azure AD** section, select the checkboxes that apply to your environment.</span></span> <span data-ttu-id="3a25d-183">通常，您至少应选择以下选项：</span><span class="sxs-lookup"><span data-stu-id="3a25d-183">Typically, you would, at a minimum, select the following:</span></span>  

        <span data-ttu-id="3a25d-184">✔为 Azure AD 中的用户创建在一起的帐户。</span><span class="sxs-lookup"><span data-stu-id="3a25d-184">✔ Create accounts in Moodle for users in Azure AD .</span></span> 
        <span data-ttu-id="3a25d-185">✔ Azure AD 中的用户更新在一起的所有帐户。</span><span class="sxs-lookup"><span data-stu-id="3a25d-185">✔ Update all accounts in Moodle for users in Azure AD.</span></span>  

    * <span data-ttu-id="3a25d-186">在 **"用户创建限制** "部分，你可以设置筛选器以限制将同步到其的 Azure AD 用户。</span><span class="sxs-lookup"><span data-stu-id="3a25d-186">In the **User Creation Restriction** section, you can setup a filter to limit the Azure AD users that will be synced to Moodle.</span></span>
    * <span data-ttu-id="3a25d-187">" **用户字段映射** "部分将允许你自定义 Azure AD 到一位用户个人资料字段映射。</span><span class="sxs-lookup"><span data-stu-id="3a25d-187">The **User Field Mapping** section will allow you to customize the Azure AD to Moodle User Profile field mapping.</span></span>
    * <span data-ttu-id="3a25d-188">在 **"Teams 同步** "部分，你可以选择自动 (组，例如，) 或所有现有 Teamsle 课程的 Teams 组。</span><span class="sxs-lookup"><span data-stu-id="3a25d-188">In the **Teams Sync** section you can choose to automatically create Groups (i.e. teams) for some, or all, of your existing Moodle courses.</span></span>

> [!NOTE]
> <span data-ttu-id="3a25d-189">默认情况下，将[](https://docs.moodle.org/310/en/Cron)按照任务计划运行， (每天运行一次) 。</span><span class="sxs-lookup"><span data-stu-id="3a25d-189">The Moodle [Cron](https://docs.moodle.org/310/en/Cron) will run according to the task schedule (once a day by default).</span></span> <span data-ttu-id="3a25d-190">但是，cron 应更频繁地运行以保持所有内容保持同步。</span><span class="sxs-lookup"><span data-stu-id="3a25d-190">However, the cron should run more frequently to keep everything in sync.</span></span>

13. <span data-ttu-id="3a25d-191">若要验证 [cron](https://docs.moodle.org/310/en/Cron)作业 (和/或手动运行它们进行首次运行) 请选择"使用 **Azure AD** 同步用户"部分中的"计划任务管理"页面链接。 </span><span class="sxs-lookup"><span data-stu-id="3a25d-191">To validate [cron](https://docs.moodle.org/310/en/Cron) jobs (and/or run them manually for the first run) select the **Scheduled tasks management page** link in the **Sync users with Azure AD** section.</span></span> <span data-ttu-id="3a25d-192">这会将您带至 **"计划任务"** 页。</span><span class="sxs-lookup"><span data-stu-id="3a25d-192">This will take you to the **Scheduled Tasks** page.</span></span>

    * <span data-ttu-id="3a25d-193">向下滚动并找到使用 **Azure AD 作业的** 同步用户，然后选择"**立即运行"。**</span><span class="sxs-lookup"><span data-stu-id="3a25d-193">Scroll down and find the **Sync users with Azure AD** job and select **Run now**.</span></span>
    * <span data-ttu-id="3a25d-194">如果选择基于现有课程创建组，还可以在 **Microsoft 365** 作业中运行"创建用户组"。</span><span class="sxs-lookup"><span data-stu-id="3a25d-194">If you chose to create Groups based on existing courses, you can also run the **Create user groups in Microsoft 365** job.</span></span>

1. <span data-ttu-id="3a25d-195">返回到 Microsoft 365 集成 (中的➡管理➡插件) 并选择 **"Teams** 设置"页。</span><span class="sxs-lookup"><span data-stu-id="3a25d-195">Return to the plugin administration page (Site administration ➡ Plugins ➡ Microsoft 365 Integration) and select the **Teams Settings** page.</span></span> <span data-ttu-id="3a25d-196">你需要配置一些设置才能启用 Teams 应用集成。</span><span class="sxs-lookup"><span data-stu-id="3a25d-196">You'll need to configure some settings to enable the Teams app integration.</span></span>

    * <span data-ttu-id="3a25d-197">若要启用 **OpenID Connect，** 请选择"管理身份验证"链接，并选择 **OpenId Connect** 线路上的目视图标（如果显示为灰色）。</span><span class="sxs-lookup"><span data-stu-id="3a25d-197">To enable **OpenID Connect**, select the **Manage Authentication** link, and select the eye icon on the **OpenId Connect** line if it is greyed out.</span></span>
    * <span data-ttu-id="3a25d-198">接下来，你需要启用框架嵌入。</span><span class="sxs-lookup"><span data-stu-id="3a25d-198">Next, you'll need to enable frame embedding.</span></span> <span data-ttu-id="3a25d-199">选择 **HTTP 安全** 链接，然后选择"允许嵌入帧 **"旁边的复选框**。</span><span class="sxs-lookup"><span data-stu-id="3a25d-199">Select the **HTTP Security** link, then select the checkbox next to **Allow frame embedding**.</span></span>
    * <span data-ttu-id="3a25d-200">下一步是启用 Web 服务，这将启用一些用户 API 功能。</span><span class="sxs-lookup"><span data-stu-id="3a25d-200">The next step is to enable web services which will enable the Moodle API features.</span></span> <span data-ttu-id="3a25d-201">选择 **"高级功能** "链接，然后确保选中"启用 **Web** 服务"旁边的复选框。</span><span class="sxs-lookup"><span data-stu-id="3a25d-201">Select the **Advanced Features** link, then make sure the checkbox next to **Enable web services** is checked.</span></span>
    * <span data-ttu-id="3a25d-202">最后，你需要为 Microsoft 365 启用外部服务。</span><span class="sxs-lookup"><span data-stu-id="3a25d-202">Finally, you'll need to enable the external services for Microsoft 365.</span></span> <span data-ttu-id="3a25d-203">选择 **"外部服务"** 链接，然后下一步：</span><span class="sxs-lookup"><span data-stu-id="3a25d-203">Select the **External services** link then next:</span></span>  

        <span data-ttu-id="3a25d-204">✔**选择\*\*\*\*"Microsoft 365 Webservices"行上的"编辑**"。</span><span class="sxs-lookup"><span data-stu-id="3a25d-204">✔ Select **Edit** on the **Moodle Microsoft 365 Webservices** row.</span></span>  
        <span data-ttu-id="3a25d-205">✔选中"已启用"旁边的 **复选框**，然后选择" **保存更改"**</span><span class="sxs-lookup"><span data-stu-id="3a25d-205">✔ Mark the checkbox next to **Enabled**, then select **Save Changes**</span></span>

    * <span data-ttu-id="3a25d-206">接下来，你需要编辑经过身份验证的用户权限，以允许他们创建 Web 服务令牌。</span><span class="sxs-lookup"><span data-stu-id="3a25d-206">Next, you'll need to edit your authenticated user permissions to allow them to create web service tokens.</span></span> <span data-ttu-id="3a25d-207">选择 **"编辑"角色"Authenticated user"** 链接。</span><span class="sxs-lookup"><span data-stu-id="3a25d-207">Select the **Editing role 'Authenticated user'** link.</span></span> <span data-ttu-id="3a25d-208">向下滚动并找到" **创建 Web 服务令牌** "功能并标记 **"允许"** 复选框。</span><span class="sxs-lookup"><span data-stu-id="3a25d-208">Scroll down and find the **Create a web service token** capability and mark the **Allow** checkbox.</span></span>

## <a name="step-3-deploy-the-moodle-assistant-bot-to-azure"></a><span data-ttu-id="3a25d-209">步骤 3：将 Botle 助手机器人部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="3a25d-209">Step 3: Deploy the Moodle Assistant Bot to Azure</span></span>

<span data-ttu-id="3a25d-210">适用于 Microsoft Teams 的免费一览助手机器人可帮助教师和学生回答有关其课程、作业、成绩和其他信息的问题。</span><span class="sxs-lookup"><span data-stu-id="3a25d-210">The free Moodle assistant bot for Microsoft Teams helps teachers and students answer questions about their courses, assignments, grades and other information in Moodle.</span></span> <span data-ttu-id="3a25d-211">机器人还会向 Teams 中的学生和教师发送一些通知。</span><span class="sxs-lookup"><span data-stu-id="3a25d-211">The bot also sends Moodle notifications to students and teachers within Teams.</span></span> <span data-ttu-id="3a25d-212">机器人是由 Microsoft 维护的开放源代码项目，在 [GitHub 上可用](https://github.com/microsoft/Moodle-Teams-Bot)。</span><span class="sxs-lookup"><span data-stu-id="3a25d-212">The bot is an open-source project maintained by Microsoft, and is available on [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).</span></span>

> [!NOTE]
> <span data-ttu-id="3a25d-213">在此部分中，你将向 Azure 订阅部署资源。</span><span class="sxs-lookup"><span data-stu-id="3a25d-213">In this section you'll deploy resources to your Azure subscription.</span></span> <span data-ttu-id="3a25d-214">所有资源都将使用免费 **层** 进行配置。</span><span class="sxs-lookup"><span data-stu-id="3a25d-214">All resources will be configured using the **free** tier.</span></span> <span data-ttu-id="3a25d-215">根据机器人的使用情况，你可能需要扩展这些资源。</span><span class="sxs-lookup"><span data-stu-id="3a25d-215">Depending on the usage of your bot, you may need to scale these resources.</span></span>
> <span data-ttu-id="3a25d-216">如果你想要在没有自动程序的情况下使用"下流"选项卡，请跳到[步骤 4。](#step-4-deploy-your-microsoft-teams-app)</span><span class="sxs-lookup"><span data-stu-id="3a25d-216">If you want to use the Moodle tab without the bot, skip to [step 4](#step-4-deploy-your-microsoft-teams-app).</span></span>

### <a name="moodle-bot-information-flow"></a><span data-ttu-id="3a25d-217">自动程序信息流</span><span class="sxs-lookup"><span data-stu-id="3a25d-217">Moodle bot information flow</span></span>

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

<span data-ttu-id="3a25d-218">若要安装自动程序，你首先需要在 Microsoft 标识平台上 [注册它](https://identity.microsoft.com/Landing)。</span><span class="sxs-lookup"><span data-stu-id="3a25d-218">To install the bot, you'll first need to register it on the [Microsoft Identity Platform](https://identity.microsoft.com/Landing).</span></span> <span data-ttu-id="3a25d-219">这样，机器人可以针对 Microsoft 终结点进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="3a25d-219">This allows your bot to authenticate against your Microsoft endpoints.</span></span> <span data-ttu-id="3a25d-220">注册自动程序：</span><span class="sxs-lookup"><span data-stu-id="3a25d-220">To register your bot:</span></span>

1. <span data-ttu-id="3a25d-221">返回到 Microsoft 365 集成 (中的➡插件➡管理) 并选择 **"Teams** 设置"选项卡。</span><span class="sxs-lookup"><span data-stu-id="3a25d-221">Return to the plugin administration page (Site administration ➡ Plugins ➡ Microsoft 365 Integration) and select the **Teams Settings** tab.</span></span>

1. <span data-ttu-id="3a25d-222">选择 **Microsoft 应用程序注册门户** 链接，然后使用 Microsoft ID 登录。</span><span class="sxs-lookup"><span data-stu-id="3a25d-222">Select the **Microsoft Application Registration Portal** link and login with your Microsoft ID.</span></span>

1. <span data-ttu-id="3a25d-223">输入应用名称， (，例如，一) 选择 **"创建"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="3a25d-223">Enter a name for your app (e.g., MoodleBot) and select the **Create** button.</span></span>

1. <span data-ttu-id="3a25d-224">复制 **应用程序 ID 并将其** 粘贴到"团队设置"页上的"自动程序应用程序 **ID"** 字段中。 </span><span class="sxs-lookup"><span data-stu-id="3a25d-224">Copy the **Application ID** and paste it into the **Bot Application ID** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="3a25d-225">选择 **"生成新密码"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="3a25d-225">Select the **Generate New Password** button.</span></span> <span data-ttu-id="3a25d-226">复制生成的密码并将其粘贴到"团队设置"页上的" **自动** 程序应用程序密码 **"** 字段中。</span><span class="sxs-lookup"><span data-stu-id="3a25d-226">Copy the generated password and and paste it into the **Bot Application Password** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="3a25d-227">滚动到窗体的底部，然后选择"**保存更改"。**</span><span class="sxs-lookup"><span data-stu-id="3a25d-227">Scroll to the bottom of the form and select **Save Changes**.</span></span>

<span data-ttu-id="3a25d-228">现在，你已生成应用程序 ID 和密码，是时候将机器人部署到 Azure 了：</span><span class="sxs-lookup"><span data-stu-id="3a25d-228">Now that you've generated your Application ID and Password, it's time to deploy your bot to Azure:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3a25d-229">选择 **"部署到 Azure"** 按钮，然后使用" ("设置"页上的"自动程序应用程序 ID"、"Bot 应用程序密码"和"Secretle 密码"的必要信息 **填写表单。**</span><span class="sxs-lookup"><span data-stu-id="3a25d-229">Select the **Deploy to Azure** button and complete the form with the necessary information (the Bot Application ID, Bot Application Password and the Moodle Secret are on the **Team Settings** page.</span></span> <span data-ttu-id="3a25d-230">Azure 信息位于"设置 **"页上**) 。</span><span class="sxs-lookup"><span data-stu-id="3a25d-230">The Azure information is on the **Setup** page).</span></span> 
> * <span data-ttu-id="3a25d-231">完成表单后，选中复选框以同意条款和条件。</span><span class="sxs-lookup"><span data-stu-id="3a25d-231">Once you have the form completed, select the check box to agree to the terms and conditions.</span></span>
> * <span data-ttu-id="3a25d-232">选择 **"购买** "按钮 (所有 Azure 资源都部署到免费层) 。</span><span class="sxs-lookup"><span data-stu-id="3a25d-232">Select the **Purchase** button (all Azure resources are deployed to the free tier).</span></span>

<span data-ttu-id="3a25d-233">资源部署到 Azure 后，你将需要使用消息终结点配置 Microsoft 365 的"一线"插件。</span><span class="sxs-lookup"><span data-stu-id="3a25d-233">Once the resources have completed deploying to Azure, you'll need to configure the Microsoft 365 Moodle plugin with a messaging endpoint.</span></span> <span data-ttu-id="3a25d-234">你需要从 Azure 中的机器人获取终结点：</span><span class="sxs-lookup"><span data-stu-id="3a25d-234">You'll need to get the endpoint from your bot in Azure:</span></span>

1. <span data-ttu-id="3a25d-235">登录到 [Azure 门户](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="3a25d-235">Log into the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="3a25d-236">在左侧 **窗格中，选择** "资源组"，然后选择在部署自动程序 (或) 创建的资源组。</span><span class="sxs-lookup"><span data-stu-id="3a25d-236">In the left pane select **Resource groups** and choose the resource group you used (or created) while deploying your bot.</span></span>

1. <span data-ttu-id="3a25d-237">从 **组中资源列表中选择 WebApp Bot** 资源。</span><span class="sxs-lookup"><span data-stu-id="3a25d-237">Select the **WebApp Bot** resource from the list of resources in the group.</span></span>

1. <span data-ttu-id="3a25d-238">从 **"概述"部分** 复制 **消息终结点** 。</span><span class="sxs-lookup"><span data-stu-id="3a25d-238">Copy the **Messaging Endpoint** from the **Overview** section.</span></span>

1. <span data-ttu-id="3a25d-239">在一个"开发工具"中，打开 Microsoft 365 的"Team **Settings"** 页面。</span><span class="sxs-lookup"><span data-stu-id="3a25d-239">In Moodle, open the **Team Settings** page of your Microsoft 365 Moodle Plugin.</span></span>

1. <span data-ttu-id="3a25d-240">在 **自动程序终结点** 字段中粘贴你刚刚复制的 URL，然后将单词 *消息更改为* *webhook。*</span><span class="sxs-lookup"><span data-stu-id="3a25d-240">In the **Bot Endpoint** field paste the URL you just copied and change the word *messages* to *webhook*.</span></span> <span data-ttu-id="3a25d-241">URL 现在应如下所示：  `https://botname.azurewebsites.net/api/webhook`</span><span class="sxs-lookup"><span data-stu-id="3a25d-241">The URL should now appear as follows:  `https://botname.azurewebsites.net/api/webhook`</span></span>

1. <span data-ttu-id="3a25d-242">选择 **"保存更改"。**</span><span class="sxs-lookup"><span data-stu-id="3a25d-242">Select **Save Changes**.</span></span>

1. <span data-ttu-id="3a25d-243">保存更改后，返回到"团队设置"选项卡，选择"下载清单文件"按钮，将应用清单包保存到计算机 (你将在) 下一节中使用它。</span><span class="sxs-lookup"><span data-stu-id="3a25d-243">Once your changes have been saved, go back to the **Team Settings** tab, select the **Download manifest file** button, and save the app manifest package to your computer (you'll use it in the next section).</span></span>

## <a name="step-4-deploy-your-microsoft-teams-app"></a><span data-ttu-id="3a25d-244">步骤 4：部署 Microsoft Teams 应用</span><span class="sxs-lookup"><span data-stu-id="3a25d-244">Step 4: Deploy your Microsoft Teams app</span></span>

<span data-ttu-id="3a25d-245">现在，你已将机器人部署到 Azure 并配置为与你的 Talkle 服务器通信，是时候部署 Microsoft Teams 应用了。</span><span class="sxs-lookup"><span data-stu-id="3a25d-245">Now that you have your bot deployed to Azure and configured to talk to your Moodle server, it's time to deploy your Microsoft Teams app.</span></span> <span data-ttu-id="3a25d-246">为此，你将加载从上一步骤的"Microsoft 365 一代插件团队设置"页下载的应用清单文件。</span><span class="sxs-lookup"><span data-stu-id="3a25d-246">To do this you'll load the app manifest file that you downloaded from the Microsoft 365 Moodle Plugin Team Settings page in the previous step.</span></span>

<span data-ttu-id="3a25d-247">在安装应用之前，你需要确保启用外部应用和上载应用。</span><span class="sxs-lookup"><span data-stu-id="3a25d-247">Before you can install the app you'll need to make sure external apps and uploading of apps is enabled.</span></span> <span data-ttu-id="3a25d-248">为此，可以按照 Teams 准备 [Microsoft 365](../concepts/build-and-test/prepare-your-o365-tenant.md) 租户文档中的步骤操作。</span><span class="sxs-lookup"><span data-stu-id="3a25d-248">To do so, you can follow the steps in the Teams [Prepare your Microsoft 365 tenant](../concepts/build-and-test/prepare-your-o365-tenant.md) documentation.</span></span> <span data-ttu-id="3a25d-249">确保启用外部应用后，可以按照以下步骤部署应用：</span><span class="sxs-lookup"><span data-stu-id="3a25d-249">Once you've ensured that external apps are enabled, you can follow the steps below to deploy your app:</span></span>

1. <span data-ttu-id="3a25d-250">打开 **Microsoft Teams。**</span><span class="sxs-lookup"><span data-stu-id="3a25d-250">Open **Microsoft Teams**.</span></span> 

1. <span data-ttu-id="3a25d-251">选择 **导航** 栏左下角区域的应用图标。</span><span class="sxs-lookup"><span data-stu-id="3a25d-251">Select the **App** icon on the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="3a25d-252">从 **选项列表中选择"** 上载自定义应用"链接。</span><span class="sxs-lookup"><span data-stu-id="3a25d-252">Select the **Upload a custom app** link from the list of options.</span></span>

> [!Note]
> <span data-ttu-id="3a25d-253">如果以全局管理员身份登录，可以选择将应用上载到组织的应用程序目录，否则只能为作为成员的团队加载应用。</span><span class="sxs-lookup"><span data-stu-id="3a25d-253">If you're logged in as a global administrator you'll have the option of uploading the app to your organization's app catalog, otherwise you'll only be able to load the app for a team in which you are a member.</span></span>

4. <span data-ttu-id="3a25d-254">选择 `manifest.zip` 之前下载的程序包，然后选择"保存 **"。**</span><span class="sxs-lookup"><span data-stu-id="3a25d-254">Select the `manifest.zip` package you downloaded previously and select **Save**.</span></span> <span data-ttu-id="3a25d-255">如果尚未下载应用清单包，可以从 **Pluginle** 中插件配置页的"团队设置"选项卡进行下载。</span><span class="sxs-lookup"><span data-stu-id="3a25d-255">If you haven't downloaded the app manifest package, you can do so from the **Team Settings** tab of the plugin configuration page in Moodle.</span></span>

<span data-ttu-id="3a25d-256">现在，你已安装应用，你可以将选项卡添加到你有权访问的任何频道。</span><span class="sxs-lookup"><span data-stu-id="3a25d-256">Now that you have the app installed, you can add the tab to any channel that you have access to.</span></span> <span data-ttu-id="3a25d-257">为此，请导航到通道，选择加 (➕) 符号，然后从列表中选择你的应用。</span><span class="sxs-lookup"><span data-stu-id="3a25d-257">To do so, navigate to the channel, select the **plus** (➕) symbol and select your app from the list.</span></span> <span data-ttu-id="3a25d-258">按照提示完成向频道添加 Your Moodle 课程选项卡。</span><span class="sxs-lookup"><span data-stu-id="3a25d-258">Follow the prompts to finish adding your Moodle course tab to a channel.</span></span>

## <a name="step-5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a><span data-ttu-id="3a25d-259">步骤 5：在 Microsoft Teams 中允许自动创建"开发工具"选项卡</span><span class="sxs-lookup"><span data-stu-id="3a25d-259">Step 5: Allow automatic creation of Moodle tabs in Microsoft Teams</span></span>

<span data-ttu-id="3a25d-260">尽管可以在 Microsoft Teams 中手动创建"开发方式"选项卡，但你可能会决定在通过课程同步创建团队时自动创建它们。</span><span class="sxs-lookup"><span data-stu-id="3a25d-260">Although the Moodle tabs can be created manually in Microsoft Teams, you may decide to have them automatically created when teams are created from course synchronization.</span></span> <span data-ttu-id="3a25d-261">为此，你需要在一起配置已上传的 Microsoft Teams 应用的 ID：</span><span class="sxs-lookup"><span data-stu-id="3a25d-261">To do this, you'll configure the ID of the uploaded Microsoft Teams app in Moodle:</span></span>

1. <span data-ttu-id="3a25d-262">打开 Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="3a25d-262">Open Microsoft Teams.</span></span>

1. <span data-ttu-id="3a25d-263">从导航栏的左下角区域选择"应用"图标。</span><span class="sxs-lookup"><span data-stu-id="3a25d-263">Select the Apps icon from the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="3a25d-264">找到上传的 **一个➡** 选择 **选项** 图标➡选择 **复制链接**。</span><span class="sxs-lookup"><span data-stu-id="3a25d-264">Locate the uploaded **Moodle app** ➡ select the **options** icon ➡ select **copy link**.</span></span>

1. <span data-ttu-id="3a25d-265">在文本编辑器中，粘贴复制的内容。</span><span class="sxs-lookup"><span data-stu-id="3a25d-265">In a text editor, paste the copied content.</span></span> <span data-ttu-id="3a25d-266">它应包含 URL，如&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff。</span><span class="sxs-lookup"><span data-stu-id="3a25d-266">It should contain a URL such as ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff.</span></span> <span data-ttu-id="3a25d-267">复制 URL 的最后一部分，例如 `00112233-4455-6677-8899-aabbccddeeff` ，这是 Microsoft Teams 应用的 ID。</span><span class="sxs-lookup"><span data-stu-id="3a25d-267">Copy the last part of the URL, e.g. `00112233-4455-6677-8899-aabbccddeeff`, which is the ID of the Microsoft Teams app.</span></span>

1. <span data-ttu-id="3a25d-268">在一个"开发工具"中，从 Microsoft 365"管理插件配置"页面打开 Teams 的" **其** 应用"选项卡。</span><span class="sxs-lookup"><span data-stu-id="3a25d-268">In Moodle, open the **Teams Moodle app** tab from your Microsoft 365 Moodle Plugin configuration page.</span></span>

1. <span data-ttu-id="3a25d-269">将 Microsoft Teams 应用的 ID 粘贴到"其应用 ID"字段中，并保存更改。</span><span class="sxs-lookup"><span data-stu-id="3a25d-269">Paste the ID of the Microsoft Teams app into the Moodle app ID field, and save changes.</span></span>

<span data-ttu-id="3a25d-270">现在同步了一个将一去不二的课程时，Microsoft Teams 将自动在团队中安装一个"一般"选项卡，在 Teams 的"常规"频道中创建一个"一行"选项卡，并配置它以包含用于从中同步其的一流课程的课程页面。</span><span class="sxs-lookup"><span data-stu-id="3a25d-270">Now when a Moodle course is synced, Microsoft Teams will automatically install the Moodle app in the team, create a Moodle tab in the General channel of Teams, and configure it to contain the course page for the Moodle course from which it is synced.</span></span>

### <a name="thats-it-you-and-your-team-can-now-start-working-with-your-moodle-courses-directly-from-microsoft-teams"></a><span data-ttu-id="3a25d-271">就是这么简单。</span><span class="sxs-lookup"><span data-stu-id="3a25d-271">That's it!</span></span> <span data-ttu-id="3a25d-272">现在，你和团队可以直接从 Microsoft Teams 开始使用你的"Your Teams"课程。</span><span class="sxs-lookup"><span data-stu-id="3a25d-272">You and your team, can now start working with your Moodle courses directly from Microsoft Teams.</span></span>

<span data-ttu-id="3a25d-273">若要与我们共享任何功能请求或反馈，请访问我们的用户 [语音页面](https://microsoftteams.uservoice.com/forums/916759-moodle)。</span><span class="sxs-lookup"><span data-stu-id="3a25d-273">To share any feature requests or feedback with us, please visit our [User Voice page](https://microsoftteams.uservoice.com/forums/916759-moodle).</span></span>
