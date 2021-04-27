---
title: 安装 Moodle LMS
description: 如何安装和配置 Microsoft Teams 的一流集成应用
keywords: Teams 一流应用集成插件
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 091192054c5add7cfbdc1e7baabc86e34cef7631
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020594"
---
# <a name="install-moodle-lms"></a><span data-ttu-id="b86dd-104">安装 Moodle LMS</span><span class="sxs-lookup"><span data-stu-id="b86dd-104">Install Moodle LMS</span></span>

<span data-ttu-id="b86dd-105">在 LMS 中，一个受欢迎的开放源代码 (系统) 。</span><span class="sxs-lookup"><span data-stu-id="b86dd-105">Moodle is a popular open-source Learning Management System (LMS).</span></span> <span data-ttu-id="b86dd-106">它现在已与 Microsoft Teams 集成。</span><span class="sxs-lookup"><span data-stu-id="b86dd-106">It is now integrated with Microsoft Teams.</span></span> <span data-ttu-id="b86dd-107">此集成可帮助教师和教师围绕 Teams 课程展开协作，提出有关成绩和作业的问题，并直接在 Teams 中通过通知保持更新。</span><span class="sxs-lookup"><span data-stu-id="b86dd-107">This integration helps educators and teachers to collaborate around Moodle courses, ask questions about grades and assignments, and stay updated with notifications directly within Teams.</span></span>

<span data-ttu-id="b86dd-108">为了帮助 IT 管理员轻松设置此集成，开放源代码 Microsoft 365 用户插件更新了以下功能：</span><span class="sxs-lookup"><span data-stu-id="b86dd-108">To help IT admins easily set-up this integration, open-source Microsoft 365 Moodle Plugin is updated with the following capabilities:</span></span>

* <span data-ttu-id="b86dd-109">使用 Azure [Active Directory](https://azure.microsoft.com/services/active-directory/) (Azure AD) 自动注册 Your Moodle 服务器。</span><span class="sxs-lookup"><span data-stu-id="b86dd-109">Auto-registration of your Moodle server with [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (Azure AD).</span></span>
* <span data-ttu-id="b86dd-110">只需单击一下即可将你的 Your Assistant bot 部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="b86dd-110">One-click deployment of your Moodle Assistant bot to Azure.</span></span>
* <span data-ttu-id="b86dd-111">自动预配团队以及自动同步所有或选择"一流"课程的团队注册。</span><span class="sxs-lookup"><span data-stu-id="b86dd-111">Auto-provisioning of teams and auto-synchronization of team enrollments for all or select Moodle courses.</span></span>
* <span data-ttu-id="b86dd-112">自动将"一页"选项卡和"将一个将一位"的"将一位"助手自动安装到每个同步的团队中。</span><span class="sxs-lookup"><span data-stu-id="b86dd-112">Auto-installation of the Moodle tab and the Moodle assistant bot into each synchronized team.</span></span>

<span data-ttu-id="b86dd-113">若要详细了解此集成提供的功能，请参阅[Microsoft Teams 和 Teams。](https://education.microsoft.com/resource/3dffb3a8)</span><span class="sxs-lookup"><span data-stu-id="b86dd-113">To learn more about the functionality this integration provides, see [Microsoft Teams and Moodle](https://education.microsoft.com/resource/3dffb3a8).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b86dd-114">必备条件</span><span class="sxs-lookup"><span data-stu-id="b86dd-114">Prerequisites</span></span>

<span data-ttu-id="b86dd-115">以下是安装和配置一个与设置一个组织应用程序有关的先决条件：</span><span class="sxs-lookup"><span data-stu-id="b86dd-115">Following are the prerequisites to install and configure the Moodle application:</span></span> 

1. <span data-ttu-id="b86dd-116">获取管理员凭据。</span><span class="sxs-lookup"><span data-stu-id="b86dd-116">Moodle administrator credentials.</span></span>

1. <span data-ttu-id="b86dd-117">Azure AD 管理员凭据。</span><span class="sxs-lookup"><span data-stu-id="b86dd-117">Azure AD administrator credentials.</span></span>

1. <span data-ttu-id="b86dd-118">可在其中创建新资源的 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="b86dd-118">An Azure subscription where you can create new resources.</span></span>

<span data-ttu-id="b86dd-119">**安装和配置一个一流应用程序**</span><span class="sxs-lookup"><span data-stu-id="b86dd-119">**To install and configure the Moodle application**</span></span> 

<span data-ttu-id="b86dd-120">执行下列步骤以安装和配置一个在部署中安装并配置一个组织应用程序：</span><span class="sxs-lookup"><span data-stu-id="b86dd-120">Perform the following steps to install and configure the Moodle application:</span></span> 

## <a name="1-install-the-microsoft-365-moodle-plugins"></a><span data-ttu-id="b86dd-121">1. 安装 Microsoft 365 管理插件</span><span class="sxs-lookup"><span data-stu-id="b86dd-121">1. Install the Microsoft 365 Moodle Plugins</span></span>

<span data-ttu-id="b86dd-122">Microsoft Teams 中的一个将一个将一起集成在 Microsoft Teams 中由 [开源 Microsoft 365 的一个"Teams"插件集提供支持](https://github.com/Microsoft/o365-moodle)。</span><span class="sxs-lookup"><span data-stu-id="b86dd-122">The Moodle integration in Microsoft Teams is powered by the open source [Microsoft 365 Moodle plugin set](https://github.com/Microsoft/o365-moodle).</span></span> <span data-ttu-id="b86dd-123">若要在将插件安装到你的一台将 Plugin 安装在你的一台开发工具服务器中，必须安装以下应用程序：</span><span class="sxs-lookup"><span data-stu-id="b86dd-123">To install the plugin in your Moodle server you must have the following applications installed:</span></span>

1. <span data-ttu-id="b86dd-124">一 [个当前稳定版本的一个，即，一个 Stablele 版本](https://download.moodle.org/releases/latest/)。</span><span class="sxs-lookup"><span data-stu-id="b86dd-124">A [current stable version of Moodle](https://download.moodle.org/releases/latest/).</span></span>

1. <span data-ttu-id="b86dd-125">已下载并保存到本地计算机的一个一体式 [OpenID Connect](https://moodle.org/plugins/auth_oidc) 和 [Microsoft 365](https://moodle.org/plugins/local_o365) 集成插件。</span><span class="sxs-lookup"><span data-stu-id="b86dd-125">The Moodle [OpenID Connect](https://moodle.org/plugins/auth_oidc) and the [Microsoft 365 Integration](https://moodle.org/plugins/local_o365) plugins downloaded and saved to your local computer.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b86dd-126">Teams 集成需要安装 OpenID Connect 和 Microsoft 365 集成插件。</span><span class="sxs-lookup"><span data-stu-id="b86dd-126">Installing the OpenID Connect and Microsoft 365 Integration plugins are required for the Teams integration.</span></span> <span data-ttu-id="b86dd-127">此外， [强烈建议使用 Microsoft 365 Teams 主题](https://moodle.org/plugins/theme_boost_o365teams) 插件。</span><span class="sxs-lookup"><span data-stu-id="b86dd-127">Additionally, the [Microsoft 365 Teams Theme](https://moodle.org/plugins/theme_boost_o365teams) plugin is highly recommended.</span></span>

1. <span data-ttu-id="b86dd-128">以管理员角色登录到你的一台将你的一台服务器，然后从左侧导航[](https://docs.moodle.org/22/en/Settings_block)面板中的"设置"块中选择"网站管理"。</span><span class="sxs-lookup"><span data-stu-id="b86dd-128">Sign in to your Moodle server as an administrator and select **Site administration** from the [Settings block](https://docs.moodle.org/22/en/Settings_block) located in the left navigation panel.</span></span>

1. <span data-ttu-id="b86dd-129">选择 **"插件"** 选项卡，然后选择"**安装插件"。**</span><span class="sxs-lookup"><span data-stu-id="b86dd-129">Select the **Plugins** tab, and then select **Install plugins**.</span></span>

1. <span data-ttu-id="b86dd-130">从" **从 ZIP 文件安装插件"部分** ，选择 **"选择文件"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="b86dd-130">From the **Install plugin from ZIP file** section, select **Choose a file** button.</span></span>

1. <span data-ttu-id="b86dd-131">从 **左侧导航栏中** 选择"上载文件"选项，浏览下载的文件，然后选择"**上载此文件"。**</span><span class="sxs-lookup"><span data-stu-id="b86dd-131">Select **Upload a file** option from the left navigation, browse for the file that you downloaded, and select **Upload this file**.</span></span>

1. <span data-ttu-id="b86dd-132">从左侧 **导航面板** 中选择"网站管理"以返回到管理员仪表板。</span><span class="sxs-lookup"><span data-stu-id="b86dd-132">Select the **Site administration** from the left navigation panel to return to your admin dashboard.</span></span> <span data-ttu-id="b86dd-133">向下滚动到" **本地插件"，** 然后选择 **"Microsoft 365 集成"** 链接。</span><span class="sxs-lookup"><span data-stu-id="b86dd-133">Scroll down to the **Local plugins** and select the **Microsoft 365 Integration** link.</span></span> 

> [!IMPORTANT]
>
> * <span data-ttu-id="b86dd-134">保持 Microsoft 365 管理插件配置页面在单独的浏览器选项卡中打开，因为在整个过程中必须返回到这组页面。</span><span class="sxs-lookup"><span data-stu-id="b86dd-134">Keep your Microsoft 365 Moodle Plugin configuration page open in a separate browser tab as you have to  return to this set of pages throughout the process.</span></span>  <br/><br/>
> * <span data-ttu-id="b86dd-135">如果你没有现有的一个一流网站，你可以查看 [Azure](https://github.com/azure/moodle) 存储库上的将一个在 Azure 存储库上快速部署一个一流实例并根据需要自定义它。</span><span class="sxs-lookup"><span data-stu-id="b86dd-135">If you do not have an existing Moodle site, you can check out Moodle on Azure [repo](https://github.com/azure/moodle) where you can quickly deploy a Moodle instance and customize it to your needs.</span></span>

## <a name="2-configure-the-connection-between-the-microsoft-365-plugin-and-azure-active-directory-azure-ad"></a><span data-ttu-id="b86dd-136">2. 配置 Microsoft 365 插件与 Azure AD (Azure Active Directory) </span><span class="sxs-lookup"><span data-stu-id="b86dd-136">2. Configure the connection between the Microsoft 365 plugin and Azure Active Directory (Azure AD)</span></span>

<span data-ttu-id="b86dd-137">你必须在 Azure AD 中将一个操作注册为应用程序。</span><span class="sxs-lookup"><span data-stu-id="b86dd-137">You must register Moodle as an application in your Azure AD.</span></span> <span data-ttu-id="b86dd-138">使用 PowerShell 脚本完成此过程。</span><span class="sxs-lookup"><span data-stu-id="b86dd-138">Use PowerShell script to complete this process.</span></span> <span data-ttu-id="b86dd-139">PowerShell 脚本会为 Microsoft 365 租户设置新的 Azure AD 应用程序，Microsoft 365 的一个插件会使用该应用程序。</span><span class="sxs-lookup"><span data-stu-id="b86dd-139">The PowerShell script provisions a new Azure AD application for your Microsoft 365 tenant, which is used by the Microsoft 365 Moodle Plugin.</span></span> <span data-ttu-id="b86dd-140">该脚本为 Microsoft 365 租户预配应用，为预配的应用设置所需的回复 URL 和权限，并返回 `AppID` 和 `Key` 。</span><span class="sxs-lookup"><span data-stu-id="b86dd-140">The script provisions the app for your Microsoft 365 tenant, set up the required reply URLs and permissions for the provisioned app, and return the `AppID` and `Key`.</span></span> <span data-ttu-id="b86dd-141">可以使用生成的 和 在 Microsoft 365 的"部署插件设置"页中，使用 `AppID` `Key` Azure AD 配置你的一个"一流"服务器网站。</span><span class="sxs-lookup"><span data-stu-id="b86dd-141">You can use the generated `AppID` and `Key` in your Microsoft 365 Moodle Plugin setup page to configure your Moodle server site with Azure AD.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="b86dd-142">PowerShell 脚本没有使用最新的配置项进行更新，因此你必须按照在一个 [3.8.0.4 和 3.9.1、3.8.0.5](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) 和 [3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) 发行版页面中概述的步骤手动完成配置。</span><span class="sxs-lookup"><span data-stu-id="b86dd-142">The PowerShell script is not updated with the latest configuration items, so you must complete the configuration manually following the steps outlined in the Moodle [3.8.0.4 and 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) and [3.8.0.5 and 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) release pages.</span></span> </br></br>
> * <span data-ttu-id="b86dd-143">若要查看 PowerShell 脚本正在自动执行的详细手动步骤，请参阅 [将你的一个一体机实例注册为应用程序](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)。</span><span class="sxs-lookup"><span data-stu-id="b86dd-143">To view the manual steps that the PowerShell script is automating in detail, see [Register your Moodle instance as an Application](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application).</span></span>

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a><span data-ttu-id="b86dd-144">Microsoft Teams 信息流的"一页"</span><span class="sxs-lookup"><span data-stu-id="b86dd-144">The Moodle tab for Microsoft Teams information flow</span></span>

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. <span data-ttu-id="b86dd-145">从"Microsoft 365 集成插件"页中，选择" **设置"** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="b86dd-145">From the Microsoft 365 Integration plugin page, select the **Setup** tab.</span></span>

1. <span data-ttu-id="b86dd-146">选择" **下载 PowerShell 脚本"** 按钮，并将其保存到本地计算机。</span><span class="sxs-lookup"><span data-stu-id="b86dd-146">Select the **Download PowerShell Script** button and save it to your local computer.</span></span>

1. <span data-ttu-id="b86dd-147">必须从 ZIP 文件准备 PowerShell 脚本。</span><span class="sxs-lookup"><span data-stu-id="b86dd-147">You must prepare the PowerShell script from the ZIP file.</span></span> <span data-ttu-id="b86dd-148">执行以下步骤以从 ZIP 文件准备 PowerShell 脚本：</span><span class="sxs-lookup"><span data-stu-id="b86dd-148">Perform the following steps to prepare the PowerShell script from the ZIP file:</span></span>

    1. <span data-ttu-id="b86dd-149">下载并解压缩 `Moodle-AzureAD-Powershell.zip` 文件。</span><span class="sxs-lookup"><span data-stu-id="b86dd-149">Download and extract the `Moodle-AzureAD-Powershell.zip` file.</span></span>
    1. <span data-ttu-id="b86dd-150">打开提取的文件夹。</span><span class="sxs-lookup"><span data-stu-id="b86dd-150">Open the extracted folder.</span></span>
    1. <span data-ttu-id="b86dd-151">右键单击文件 `Moodle-AzureAD-Script.ps1` ，然后选择属性。</span><span class="sxs-lookup"><span data-stu-id="b86dd-151">Right-click on the `Moodle-AzureAD-Script.ps1` file and select **Properties**.</span></span>
    1. <span data-ttu-id="b86dd-152">在" **属性** "窗口的"常规"选项卡下，选中位于窗口底部的 `Unblock` **Security** 属性旁边的框。</span><span class="sxs-lookup"><span data-stu-id="b86dd-152">Under the **General** tab of the Properties window, check the `Unblock` box next to the **Security** attribute located at the bottom of the window.</span></span>
    1. <span data-ttu-id="b86dd-153">选择“**确定**”。</span><span class="sxs-lookup"><span data-stu-id="b86dd-153">Select **OK**.</span></span>
    1. <span data-ttu-id="b86dd-154">将目录路径复制到提取的文件夹。</span><span class="sxs-lookup"><span data-stu-id="b86dd-154">Copy the directory path to the extracted folder.</span></span>

1. <span data-ttu-id="b86dd-155">以管理员角色运行 PowerShell：</span><span class="sxs-lookup"><span data-stu-id="b86dd-155">Run PowerShell as an administrator:</span></span>

    1. <span data-ttu-id="b86dd-156">选择“开始”。</span><span class="sxs-lookup"><span data-stu-id="b86dd-156">Select Start.</span></span>
    1. <span data-ttu-id="b86dd-157">键入 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="b86dd-157">Type PowerShell.</span></span>
    1. <span data-ttu-id="b86dd-158">右键单击"Windows PowerShell"。</span><span class="sxs-lookup"><span data-stu-id="b86dd-158">Right-click Windows PowerShell.</span></span>
    1. <span data-ttu-id="b86dd-159">选择 **"以管理员角色运行"。**</span><span class="sxs-lookup"><span data-stu-id="b86dd-159">Select **Run as Administrator**.</span></span>

1. <span data-ttu-id="b86dd-160">通过键入 where 是目录的路径，导航到 `cd .../.../Moodle-AzureAD-Powershell` `.../...` 解压缩目录。</span><span class="sxs-lookup"><span data-stu-id="b86dd-160">Navigate to the unzipped directory by typing `cd .../.../Moodle-AzureAD-Powershell` where `.../...` is the path to the directory.</span></span>

1. <span data-ttu-id="b86dd-161">执行 PowerShell 脚本：</span><span class="sxs-lookup"><span data-stu-id="b86dd-161">Execute the PowerShell script:</span></span>

    1. <span data-ttu-id="b86dd-162">输入 `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` 。</span><span class="sxs-lookup"><span data-stu-id="b86dd-162">Enter `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`.</span></span>
    1. <span data-ttu-id="b86dd-163">输入 `./Moodle-AzureAD-Script.ps1` 。</span><span class="sxs-lookup"><span data-stu-id="b86dd-163">Enter `./Moodle-AzureAD-Script.ps1`.</span></span>
    1. <span data-ttu-id="b86dd-164">在弹出窗口中登录到 Microsoft 365 管理员帐户。</span><span class="sxs-lookup"><span data-stu-id="b86dd-164">Sign in to your Microsoft 365 administrator account in the pop-up window.</span></span>
    1. <span data-ttu-id="b86dd-165">输入 Azure AD 应用程序名称 (，例如，在 Azure AD 应用程序名称中输入一) 。</span><span class="sxs-lookup"><span data-stu-id="b86dd-165">Enter the name of the Azure AD Application (e.g., Moodle/Moodle plugin).</span></span>
    1. <span data-ttu-id="b86dd-166">输入 Your Your Moodle 服务器的 URL。</span><span class="sxs-lookup"><span data-stu-id="b86dd-166">Enter the URL for your Moodle server.</span></span>
    1. <span data-ttu-id="b86dd-167">复制 **脚本生成的\*\*\*\*应用程序** ID 和应用程序密钥并保存它们。</span><span class="sxs-lookup"><span data-stu-id="b86dd-167">Copy the **Application ID** and **Application Key** generated by the script and save them.</span></span>

1. <span data-ttu-id="b86dd-168">接下来，你必须将 `AppID` 和 `Key` 添加到 Microsoft 365 的"组织插件"中。</span><span class="sxs-lookup"><span data-stu-id="b86dd-168">Next you must add the `AppID` and `Key` to the Microsoft 365 Moodle Plugin.</span></span> <span data-ttu-id="b86dd-169">返回到插件管理页。</span><span class="sxs-lookup"><span data-stu-id="b86dd-169">Return to the plugin administration page.</span></span> <span data-ttu-id="b86dd-170">流程为：Microsoft 365 集成➡网站➡插件。</span><span class="sxs-lookup"><span data-stu-id="b86dd-170">The flow is: Site administration ➡ Plugins ➡ Microsoft 365 Integration.</span></span>

1. <span data-ttu-id="b86dd-171">在"**安装**"选项卡上，添加之前复制的应用程序 **ID** 和应用程序密钥，然后选择"保存 **更改"。**</span><span class="sxs-lookup"><span data-stu-id="b86dd-171">On the **Setup** tab add the **Application ID** and **Application Key** you copied previously, then select **Save changes**.</span></span>

1. <span data-ttu-id="b86dd-172">刷新页面后，可以看到新部分选择 **连接方法**。</span><span class="sxs-lookup"><span data-stu-id="b86dd-172">After the page refreshes, you can see a new section **Choose connection method**.</span></span> <span data-ttu-id="b86dd-173">选中标记为"默认 **"的复选框** ，然后再次 **选择"保存更改** "。</span><span class="sxs-lookup"><span data-stu-id="b86dd-173">Select the checkbox labeled **Default** and then select **Save changes** again.</span></span>

1. <span data-ttu-id="b86dd-174">刷新页面后，你可以看到另一个新部分管理员同意& **其他信息**。</span><span class="sxs-lookup"><span data-stu-id="b86dd-174">After the page refreshes you can see another new section **Admin consent & additional information**.</span></span>
    1. <span data-ttu-id="b86dd-175">选择 **"提供管理员同意** "链接，输入你的 Microsoft 365 全局管理员凭据， **然后选择接受以** 授予权限。</span><span class="sxs-lookup"><span data-stu-id="b86dd-175">Select **Provide Admin Consent** link, enter your Microsoft 365 Global Administrator credentials, then **Accept** to grant the permissions.</span></span>
    1. <span data-ttu-id="b86dd-176">在 **"Azure AD 租户** "字段旁边，选择" **检测"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="b86dd-176">Next to the **Azure AD Tenant** field, select the **Detect** button.</span></span>
    1. <span data-ttu-id="b86dd-177">在 **OneDrive for Business URL 旁边，** 选择"检测 **"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="b86dd-177">Next to the **OneDrive for Business URL**, select the **Detect** button.</span></span>
    1. <span data-ttu-id="b86dd-178">填充字段后，再次选择 **"保存更改"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="b86dd-178">After the fields populate, select the **Save changes** button again.</span></span>

1. <span data-ttu-id="b86dd-179">选择"**更新"** 按钮以验证安装，然后选择"**保存更改"。**</span><span class="sxs-lookup"><span data-stu-id="b86dd-179">Select the **Update** button to verify the installation, then **Save changes**.</span></span>

1. <span data-ttu-id="b86dd-180">在将用户同步到你的一台将你的服务器与 Azure AD 之间。</span><span class="sxs-lookup"><span data-stu-id="b86dd-180">Synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="b86dd-181">根据你的环境，你可以在此阶段选择不同的选项。</span><span class="sxs-lookup"><span data-stu-id="b86dd-181">Depending on your environment, you can select different options during this stage.</span></span> <span data-ttu-id="b86dd-182">首先，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="b86dd-182">To get started:</span></span>
    1. <span data-ttu-id="b86dd-183">切换到" **同步设置"选项卡**</span><span class="sxs-lookup"><span data-stu-id="b86dd-183">Switch to the **Sync Settings tab**</span></span>
    1. <span data-ttu-id="b86dd-184">在 **"将用户与 Azure AD** 同步"部分中，选中适用于你的环境的复选框。</span><span class="sxs-lookup"><span data-stu-id="b86dd-184">In the **Sync users with Azure AD** section, select the checkboxes that apply to your environment.</span></span> <span data-ttu-id="b86dd-185">您必须选择以下选项：</span><span class="sxs-lookup"><span data-stu-id="b86dd-185">You must select the following:</span></span>  

        <span data-ttu-id="b86dd-186">✔ Azure AD 中的用户创建在在一起的帐户。</span><span class="sxs-lookup"><span data-stu-id="b86dd-186">✔ Create accounts in Moodle for users in Azure AD .</span></span> 
        <span data-ttu-id="b86dd-187">✔ Azure AD 中的用户更新在在一起的所有帐户。</span><span class="sxs-lookup"><span data-stu-id="b86dd-187">✔ Update all accounts in Moodle for users in Azure AD.</span></span>  

    1. <span data-ttu-id="b86dd-188">在 **"用户创建限制** "部分，可以设置筛选器以限制同步到一台的 Azure AD 用户。</span><span class="sxs-lookup"><span data-stu-id="b86dd-188">In the **User Creation Restriction** section, you can setup a filter to limit the Azure AD users that is synced to Moodle.</span></span>
    1. <span data-ttu-id="b86dd-189">通过 **"用户字段映射** "部分，你可以自定义 Azure AD 到一些用户个人资料字段映射。</span><span class="sxs-lookup"><span data-stu-id="b86dd-189">The **User Field Mapping** section allows you to customize the Azure AD to Moodle User Profile field mapping.</span></span>
    1. <span data-ttu-id="b86dd-190">在 **"Teams 同步** "部分，可以选择自动创建组，例如现有一些或所有 Teams 的 Teams。</span><span class="sxs-lookup"><span data-stu-id="b86dd-190">In the **Teams Sync** section, you can select to automatically create Groups, such as teams for some, or all, of your existing Moodle courses.</span></span>

> [!NOTE]
> <span data-ttu-id="b86dd-191">将按照任务 [计划](https://docs.moodle.org/310/en/Cron) 运行一个将运行一个在一起。</span><span class="sxs-lookup"><span data-stu-id="b86dd-191">The Moodle [Cron](https://docs.moodle.org/310/en/Cron) runs according to the task schedule.</span></span> <span data-ttu-id="b86dd-192">默认计划为每天一次。</span><span class="sxs-lookup"><span data-stu-id="b86dd-192">The default schedule is once a day.</span></span> <span data-ttu-id="b86dd-193">但是，cron 必须更频繁地运行，以保持所有内容同步。</span><span class="sxs-lookup"><span data-stu-id="b86dd-193">However, the cron must run more frequently to keep everything in sync.</span></span>

13. <span data-ttu-id="b86dd-194">若要验证 [cron](https://docs.moodle.org/310/en/Cron)作业并首次运行时手动运行它们，请选择"将用户与 **Azure AD** 同步"部分中的"计划任务管理"页链接。</span><span class="sxs-lookup"><span data-stu-id="b86dd-194">To validate [cron](https://docs.moodle.org/310/en/Cron) jobs and run them manually for the first run, select the **Scheduled tasks management page** link in the **Sync users with Azure AD** section.</span></span> <span data-ttu-id="b86dd-195">这会将您带至 **"计划任务"** 页。</span><span class="sxs-lookup"><span data-stu-id="b86dd-195">This takes you to the **Scheduled Tasks** page.</span></span>

    1. <span data-ttu-id="b86dd-196">向下滚动并查找"使用 **Azure AD 同步用户"** 作业，然后选择"**立即运行"。**</span><span class="sxs-lookup"><span data-stu-id="b86dd-196">Scroll down and find the **Sync users with Azure AD** job and select **Run now**.</span></span>
    1. <span data-ttu-id="b86dd-197">如果选择基于现有课程创建组，还可以运行在 **Microsoft 365** 中创建用户组作业。</span><span class="sxs-lookup"><span data-stu-id="b86dd-197">If you select to create Groups based on existing courses, you can also run the **Create user groups in Microsoft 365** job.</span></span>

1. <span data-ttu-id="b86dd-198">返回到插件管理页。</span><span class="sxs-lookup"><span data-stu-id="b86dd-198">Return to the plugin administration page.</span></span> <span data-ttu-id="b86dd-199">导航流为：网站管理➡ Microsoft 365 ➡插件。</span><span class="sxs-lookup"><span data-stu-id="b86dd-199">The navigation flow is: Site administration ➡ Plugins ➡ Microsoft 365 Integratio.</span></span> <span data-ttu-id="b86dd-200">然后，选择 **"Teams 设置"** 页。</span><span class="sxs-lookup"><span data-stu-id="b86dd-200">Then, select the **Teams Settings** page.</span></span> <span data-ttu-id="b86dd-201">必须配置某些设置才能启用 Teams 应用集成。</span><span class="sxs-lookup"><span data-stu-id="b86dd-201">You must configure some settings to enable the Teams app integration.</span></span>

    1. <span data-ttu-id="b86dd-202">若要启用 **OpenID Connect，** 请选择" **管理** 身份验证"链接，并选择 **OpenId Connect** 线路上的目视图标（如果显示为灰色）。</span><span class="sxs-lookup"><span data-stu-id="b86dd-202">To enable **OpenID Connect**, select the **Manage Authentication** link, and select the eye icon on the **OpenId Connect** line if it is greyed out.</span></span>
    1. <span data-ttu-id="b86dd-203">启用帧嵌入。</span><span class="sxs-lookup"><span data-stu-id="b86dd-203">Enable frame embedding.</span></span> <span data-ttu-id="b86dd-204">选择 **"HTTP 安全性"** 链接，然后选中"允许嵌入框架 **"旁边的复选框**。</span><span class="sxs-lookup"><span data-stu-id="b86dd-204">Select the **HTTP Security** link, then select the checkbox next to **Allow frame embedding**.</span></span>
    1. <span data-ttu-id="b86dd-205">启用 Web 服务，从而启用一些用户 API 功能。</span><span class="sxs-lookup"><span data-stu-id="b86dd-205">Enable web services which enables the Moodle API features.</span></span> <span data-ttu-id="b86dd-206">选择" **高级功能"** 链接，然后确保选中"启用 **Web** 服务"旁边的复选框。</span><span class="sxs-lookup"><span data-stu-id="b86dd-206">Select the **Advanced Features** link, then make sure the checkbox next to **Enable web services** is checked.</span></span>
    1. <span data-ttu-id="b86dd-207">为 Microsoft 365 启用外部服务。</span><span class="sxs-lookup"><span data-stu-id="b86dd-207">Enable the external services for Microsoft 365.</span></span> <span data-ttu-id="b86dd-208">选择" **外部服务"** 链接，然后下一步：</span><span class="sxs-lookup"><span data-stu-id="b86dd-208">Select the **External services** link then next:</span></span>  

        <span data-ttu-id="b86dd-209">✔**在\*\*\*\*"Microsoft 365 Webservices"行上选择"编辑**"。</span><span class="sxs-lookup"><span data-stu-id="b86dd-209">✔ Select **Edit** on the **Moodle Microsoft 365 Webservices** row.</span></span>  
        <span data-ttu-id="b86dd-210">✔选中"已启用"旁边的复选框，然后选择"**保存更改"**</span><span class="sxs-lookup"><span data-stu-id="b86dd-210">✔ Mark the checkbox next to **Enabled**, then select **Save Changes**</span></span>

    1. <span data-ttu-id="b86dd-211">编辑经过身份验证的用户权限，以允许他们创建 Web 服务令牌。</span><span class="sxs-lookup"><span data-stu-id="b86dd-211">Edit your authenticated user permissions to allow them to create web service tokens.</span></span> <span data-ttu-id="b86dd-212">选择 **"编辑角色'经过身份验证的用户'"** 链接。</span><span class="sxs-lookup"><span data-stu-id="b86dd-212">Select the **Editing role 'Authenticated user'** link.</span></span> <span data-ttu-id="b86dd-213">向下滚动并找到创建 **Web 服务令牌** 功能并标记 **"允许"** 复选框。</span><span class="sxs-lookup"><span data-stu-id="b86dd-213">Scroll down and find the **Create a web service token** capability and mark the **Allow** checkbox.</span></span>

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a><span data-ttu-id="b86dd-214">3. 将用户助理机器人部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="b86dd-214">3. Deploy the Moodle Assistant Bot to Azure</span></span>

<span data-ttu-id="b86dd-215">适用于 Microsoft Teams 的免费一览助手机器人可帮助教师和学生回答有关其课程、作业、成绩和其他在一起的问题。</span><span class="sxs-lookup"><span data-stu-id="b86dd-215">The free Moodle assistant bot for Microsoft Teams helps teachers and students answer questions about their courses, assignments, grades and other information in Moodle.</span></span> <span data-ttu-id="b86dd-216">机器人还会向 Teams 中的学生和教师发送一些用户通知。</span><span class="sxs-lookup"><span data-stu-id="b86dd-216">The bot also sends Moodle notifications to students and teachers within Teams.</span></span> <span data-ttu-id="b86dd-217">机器人是由 Microsoft 维护的开放源代码项目，可在 [GitHub 上获取](https://github.com/microsoft/Moodle-Teams-Bot)。</span><span class="sxs-lookup"><span data-stu-id="b86dd-217">The bot is an open-source project maintained by Microsoft, and is available on [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).</span></span>

> [!NOTE]
> * <span data-ttu-id="b86dd-218">在此部分中，你必须将资源部署到 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="b86dd-218">In this section you must deploy resources to your Azure subscription.</span></span> <span data-ttu-id="b86dd-219">使用免费层配置的所有 **资源** 软件。</span><span class="sxs-lookup"><span data-stu-id="b86dd-219">All resources ware configured using the **free** tier.</span></span> <span data-ttu-id="b86dd-220">根据机器人的使用情况，你可以扩展这些资源。</span><span class="sxs-lookup"><span data-stu-id="b86dd-220">Depending on the usage of your bot, you mhave to scale these resources.</span></span>
> * <span data-ttu-id="b86dd-221">若要在没有自动程序的情况下使用"操作方式"选项卡，请跳到 [4](#4-deploy-your-microsoft-teams-app)。</span><span class="sxs-lookup"><span data-stu-id="b86dd-221">To use the Moodle tab without the bot, skip to [4](#4-deploy-your-microsoft-teams-app).</span></span>

### <a name="moodle-bot-information-flow"></a><span data-ttu-id="b86dd-222">自动程序信息流</span><span class="sxs-lookup"><span data-stu-id="b86dd-222">Moodle bot information flow</span></span>

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

<span data-ttu-id="b86dd-223">若要安装自动程序，必须在 Microsoft 标识平台上 [注册它](https://identity.microsoft.com/Landing)。</span><span class="sxs-lookup"><span data-stu-id="b86dd-223">To install the bot, you must register it on the [Microsoft Identity Platform](https://identity.microsoft.com/Landing).</span></span> <span data-ttu-id="b86dd-224">这允许机器人针对 Microsoft 终结点进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="b86dd-224">This allows your bot to authenticate against your Microsoft endpoints.</span></span> 

<span data-ttu-id="b86dd-225">**若要注册自动程序**：</span><span class="sxs-lookup"><span data-stu-id="b86dd-225">**To register your bot**:</span></span>

1. <span data-ttu-id="b86dd-226">转到插件管理页面。</span><span class="sxs-lookup"><span data-stu-id="b86dd-226">Go to the plugin administration page.</span></span> <span data-ttu-id="b86dd-227">转到 **插件**。</span><span class="sxs-lookup"><span data-stu-id="b86dd-227">Go to **Plugins**.</span></span> <span data-ttu-id="b86dd-228">在 **"Microsoft 365 集成"** 下，选择 **"Teams 设置"** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="b86dd-228">Under **Microsoft 365 Integration**, select the **Teams Settings** tab.</span></span>

1. <span data-ttu-id="b86dd-229">选择 **"Microsoft 应用程序注册门户** "链接，然后使用 Microsoft ID 登录。</span><span class="sxs-lookup"><span data-stu-id="b86dd-229">Select the **Microsoft Application Registration Portal** link and sign in with your Microsoft ID.</span></span>

1. <span data-ttu-id="b86dd-230">输入你的应用的名称，例如，一个在一起， **然后选择创建按钮** 。</span><span class="sxs-lookup"><span data-stu-id="b86dd-230">Enter a name for your app, such as MoodleBot and select the **Create** button.</span></span>

1. <span data-ttu-id="b86dd-231">复制应用程序 **ID 并将其** 粘贴到"团队设置"页上的"自动程序应用程序 **ID"** 字段中。 </span><span class="sxs-lookup"><span data-stu-id="b86dd-231">Copy the **Application ID** and paste it into the **Bot Application ID** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="b86dd-232">选择" **生成新密码"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="b86dd-232">Select the **Generate New Password** button.</span></span> <span data-ttu-id="b86dd-233">复制生成的密码并将其粘贴到"团队设置"页上的"自动程序应用程序 **密码"** 字段中。</span><span class="sxs-lookup"><span data-stu-id="b86dd-233">Copy the generated password and and paste it into the **Bot Application Password** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="b86dd-234">滚动到表单底部，然后选择"保存 **更改"。**</span><span class="sxs-lookup"><span data-stu-id="b86dd-234">Scroll to the bottom of the form and select **Save Changes**.</span></span>

<span data-ttu-id="b86dd-235">生成应用程序 ID 和密码时，下一步是将机器人部署到 Azure：</span><span class="sxs-lookup"><span data-stu-id="b86dd-235">As you generated your Application ID and Password, next step is to deploy your bot to Azure:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b86dd-236">选择" **部署到 Azure"** 按钮，然后使用必要的信息完成表单，例如"团队设置"页上的自动程序应用程序 ID、自动程序应用程序密码和"Botle **密码** "。</span><span class="sxs-lookup"><span data-stu-id="b86dd-236">Select the **Deploy to Azure** button and complete the form with the necessary information, such as the Bot Application ID, Bot Application Password and the Moodle Secret are on the **Team Settings** page.</span></span> <span data-ttu-id="b86dd-237">Azure 信息位于"设置 **"页面**) 。</span><span class="sxs-lookup"><span data-stu-id="b86dd-237">The Azure information is on the **Setup** page).</span></span> 
> * <span data-ttu-id="b86dd-238">完成表单后，选中复选框以同意条款和条件。</span><span class="sxs-lookup"><span data-stu-id="b86dd-238">After completing the form, select the check box to agree to the terms and conditions.</span></span>
> * <span data-ttu-id="b86dd-239">选择" **购买"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="b86dd-239">Select the **Purchase** button.</span></span> <span data-ttu-id="b86dd-240">所有 Azure 资源都部署到免费层。</span><span class="sxs-lookup"><span data-stu-id="b86dd-240">All Azure resources are deployed to the free tier.</span></span>

<span data-ttu-id="b86dd-241">资源部署到 Azure 后，必须使用消息终结点配置 Microsoft 365 的一个"一文包"插件。</span><span class="sxs-lookup"><span data-stu-id="b86dd-241">After the resources have completed deploying to Azure, you must configure the Microsoft 365 Moodle plugin with a messaging endpoint.</span></span> <span data-ttu-id="b86dd-242">你必须从 Azure 中的机器人获取终结点：</span><span class="sxs-lookup"><span data-stu-id="b86dd-242">You must get the endpoint from your bot in Azure:</span></span>

<span data-ttu-id="b86dd-243">**使用消息终结点配置 Microsoft 365 的一个部署插件**</span><span class="sxs-lookup"><span data-stu-id="b86dd-243">**Configure the Microsoft 365 Moodle plugin with a messaging endpoint**</span></span>  
1. <span data-ttu-id="b86dd-244">登录到 [Azure 门户](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b86dd-244">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="b86dd-245">在左侧窗格中，选择" **资源组** "，并选择你使用或创建的资源组，同时部署机器人。</span><span class="sxs-lookup"><span data-stu-id="b86dd-245">In the left pane, select **Resource groups** and select the resource group you used or created, while deploying your bot.</span></span>

1. <span data-ttu-id="b86dd-246">从 **组的资源列表中选择 WebApp** Bot 资源。</span><span class="sxs-lookup"><span data-stu-id="b86dd-246">Select the **WebApp Bot** resource from the list of resources in the group.</span></span>

1. <span data-ttu-id="b86dd-247">从" **概述"部分** 复制 **消息终结点** 。</span><span class="sxs-lookup"><span data-stu-id="b86dd-247">Copy the **Messaging Endpoint** from the **Overview** section.</span></span>

1. <span data-ttu-id="b86dd-248">在"在将 Microsoft 365 **管理插件** "打开"团队设置"页面。</span><span class="sxs-lookup"><span data-stu-id="b86dd-248">In Moodle, open the **Team Settings** page of your Microsoft 365 Moodle Plugin.</span></span>

1. <span data-ttu-id="b86dd-249">在 **自动程序终结点** 字段中粘贴你刚刚复制的 URL，然后将单词 *消息* 更改为 *webhook*。</span><span class="sxs-lookup"><span data-stu-id="b86dd-249">In the **Bot Endpoint** field paste the URL you just copied and change the word *messages* to *webhook*.</span></span> <span data-ttu-id="b86dd-250">URL 现在应如下所示： `https://botname.azurewebsites.net/api/webhook`</span><span class="sxs-lookup"><span data-stu-id="b86dd-250">The URL should now appear as follows: `https://botname.azurewebsites.net/api/webhook`</span></span>

1. <span data-ttu-id="b86dd-251">选择 **"保存更改"。**</span><span class="sxs-lookup"><span data-stu-id="b86dd-251">Select **Save Changes**.</span></span>

1. <span data-ttu-id="b86dd-252">保存更改后，返回到"团队设置"选项卡，选择"下载清单文件"按钮，将应用清单包保存到计算机以进一步使用。</span><span class="sxs-lookup"><span data-stu-id="b86dd-252">After saving the changes, go back to the **Team Settings** tab, select the **Download manifest file** button, and save the app manifest package to your computer for further use.</span></span>

## <a name="4-deploy-your-microsoft-teams-app"></a><span data-ttu-id="b86dd-253">4. 部署 Microsoft Teams 应用</span><span class="sxs-lookup"><span data-stu-id="b86dd-253">4. Deploy your Microsoft Teams app</span></span>

<span data-ttu-id="b86dd-254">在将机器人部署到 Azure 并配置为与你的 Talkle 服务器通信后，你必须部署 Microsoft Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="b86dd-254">After your bot deployed to Azure and configured to talk to your Moodle server, you must deploy your Microsoft Teams app.</span></span> <span data-ttu-id="b86dd-255">为此，你必须加载从上一步中的 Microsoft 365 管理插件团队设置页面下载的应用清单文件。</span><span class="sxs-lookup"><span data-stu-id="b86dd-255">To do this you must load the app manifest file that you downloaded from the Microsoft 365 Moodle Plugin Team Settings page in the previous step.</span></span>

<span data-ttu-id="b86dd-256">在安装应用之前，必须确保启用外部应用和上传应用。</span><span class="sxs-lookup"><span data-stu-id="b86dd-256">Before you install the app you must ensure to enable external apps and uploading of apps.</span></span> <span data-ttu-id="b86dd-257">为此，可以按照 Teams 准备 [Microsoft 365 租户文档中的步骤](../concepts/build-and-test/prepare-your-o365-tenant.md) 操作。</span><span class="sxs-lookup"><span data-stu-id="b86dd-257">To do so, you can follow the steps in the Teams [Prepare your Microsoft 365 tenant](../concepts/build-and-test/prepare-your-o365-tenant.md) documentation.</span></span> <span data-ttu-id="b86dd-258">你可以执行以下步骤来部署应用：</span><span class="sxs-lookup"><span data-stu-id="b86dd-258">You can perform th the following steps to deploy your app:</span></span> 

<span data-ttu-id="b86dd-259">**部署应用**</span><span class="sxs-lookup"><span data-stu-id="b86dd-259">**To deploy your app**</span></span>

1. <span data-ttu-id="b86dd-260">打开 **Microsoft Teams**。</span><span class="sxs-lookup"><span data-stu-id="b86dd-260">Open **Microsoft Teams**.</span></span> 

1. <span data-ttu-id="b86dd-261">选择 **导航** 栏左下角区域的应用图标。</span><span class="sxs-lookup"><span data-stu-id="b86dd-261">Select the **App** icon on the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="b86dd-262">从选项 **列表中选择"上载** 自定义应用"链接。</span><span class="sxs-lookup"><span data-stu-id="b86dd-262">Select the **Upload a custom app** link from the list of options.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b86dd-263">如果以全局管理员身份登录，则必须选择将应用程序上载到组织的应用程序目录，否则只能为作为成员的团队加载应用程序。</span><span class="sxs-lookup"><span data-stu-id="b86dd-263">If you are logged in as a global administrator, you must have the option of uploading the app to your organization's app catalog, otherwise you can only load the app for a team in which you are a member.</span></span>

4. <span data-ttu-id="b86dd-264">选择 `manifest.zip` 之前下载的程序包，然后选择保存。 </span><span class="sxs-lookup"><span data-stu-id="b86dd-264">Select the `manifest.zip` package you downloaded previously and select **Save**.</span></span> <span data-ttu-id="b86dd-265">如果尚未下载应用清单包，可以从在将插件配置页的"团队设置"选项卡下载到在一起。</span><span class="sxs-lookup"><span data-stu-id="b86dd-265">If you have not downloaded the app manifest package, you can download from the **Team Settings** tab of the plugin configuration page in Moodle.</span></span>

<span data-ttu-id="b86dd-266">现在，你已安装应用，你可以将选项卡添加到你有权访问的任何频道。</span><span class="sxs-lookup"><span data-stu-id="b86dd-266">Now that you have the app installed, you can add the tab to any channel that you have access to.</span></span> <span data-ttu-id="b86dd-267">为此，请导航到通道，选择 **加 (➕) 符号** ，然后从列表中选择你的应用。</span><span class="sxs-lookup"><span data-stu-id="b86dd-267">To do so, navigate to the channel, select the **plus** (➕) symbol and select your app from the list.</span></span> <span data-ttu-id="b86dd-268">按照提示完成向频道添加 Your Moodle 课程选项卡。</span><span class="sxs-lookup"><span data-stu-id="b86dd-268">Follow the prompts to finish adding your Moodle course tab to a channel.</span></span>

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a><span data-ttu-id="b86dd-269">5. 允许在 Microsoft Teams 中自动创建一个"设置"选项卡</span><span class="sxs-lookup"><span data-stu-id="b86dd-269">5. Allow automatic creation of Moodle tabs in Microsoft Teams</span></span>

<span data-ttu-id="b86dd-270">尽管在 Microsoft Teams 中手动创建"一页"选项卡，但你可以决定在通过课程同步创建团队时自动创建它们。</span><span class="sxs-lookup"><span data-stu-id="b86dd-270">Although the Moodle tabs are created manually in Microsoft Teams, you can decide to have them automatically created when teams are created from course synchronization.</span></span> <span data-ttu-id="b86dd-271">为此，你必须在 Teams 中配置上传的 Microsoft Teams 应用的 ID：</span><span class="sxs-lookup"><span data-stu-id="b86dd-271">To do this, you must configure the ID of the uploaded Microsoft Teams app in Moodle:</span></span>

1. <span data-ttu-id="b86dd-272">打开 Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="b86dd-272">Open Microsoft Teams.</span></span>

1. <span data-ttu-id="b86dd-273">从导航栏的左下角区域选择"应用"图标。</span><span class="sxs-lookup"><span data-stu-id="b86dd-273">Select the Apps icon from the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="b86dd-274">找到已上传 **的一➡** 选择 **选项** 图标➡选择 **复制链接**。</span><span class="sxs-lookup"><span data-stu-id="b86dd-274">Locate the uploaded **Moodle app** ➡ select the **options** icon ➡ select **copy link**.</span></span>

1. <span data-ttu-id="b86dd-275">在文本编辑器中，粘贴复制的内容。</span><span class="sxs-lookup"><span data-stu-id="b86dd-275">In a text editor, paste the copied content.</span></span> <span data-ttu-id="b86dd-276">它必须包含 URL，如 ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff。</span><span class="sxs-lookup"><span data-stu-id="b86dd-276">It must contain a URL such as ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff.</span></span> <span data-ttu-id="b86dd-277">复制 URL 的最后一部分，例如 ，  `00112233-4455-6677-8899-aabbccddeeff` 这是 Microsoft Teams 应用的 ID。</span><span class="sxs-lookup"><span data-stu-id="b86dd-277">Copy the last part of the URL, such as  `00112233-4455-6677-8899-aabbccddeeff`, which is the ID of the Microsoft Teams app.</span></span>

1. <span data-ttu-id="b86dd-278">在"在将 Teams **365 部署插件** 配置"页中，打开"Teams 的一流"应用选项卡。</span><span class="sxs-lookup"><span data-stu-id="b86dd-278">In Moodle, open the **Teams Moodle app** tab from your Microsoft 365 Moodle Plugin configuration page.</span></span>

1. <span data-ttu-id="b86dd-279">将 Microsoft Teams 应用的 ID 粘贴到"Teams 应用 ID"字段中，并保存更改。</span><span class="sxs-lookup"><span data-stu-id="b86dd-279">Paste the ID of the Microsoft Teams app into the Moodle app ID field, and save changes.</span></span>

<span data-ttu-id="b86dd-280">同步一个一流课程后，Microsoft Teams 会自动在团队中安装一个一流应用，在 Teams 的常规频道中创建一个"一般"选项卡，并对其进行配置以包含用于同步其的一流课程的"一流"课程页面。</span><span class="sxs-lookup"><span data-stu-id="b86dd-280">When a Moodle course is synced, Microsoft Teams automatically installs the Moodle app in the team, create a Moodle tab in the General channel of Teams, and configure it to contain the course page for the Moodle course from which it is synced.</span></span> <span data-ttu-id="b86dd-281">你现在可以直接从 Microsoft Teams 开始使用你的一流课程。</span><span class="sxs-lookup"><span data-stu-id="b86dd-281">You can now start working with your Moodle courses directly from Microsoft Teams.</span></span>

<span data-ttu-id="b86dd-282">若要与我们共享任何功能请求或反馈，请访问我们的用户 [语音页面](https://microsoftteams.uservoice.com/forums/916759-moodle)。</span><span class="sxs-lookup"><span data-stu-id="b86dd-282">To share any feature requests or feedback with us, visit our [User Voice page](https://microsoftteams.uservoice.com/forums/916759-moodle).</span></span>

## <a name="see-also"></a><span data-ttu-id="b86dd-283">另请参阅</span><span class="sxs-lookup"><span data-stu-id="b86dd-283">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b86dd-284">集成 web 应用</span><span class="sxs-lookup"><span data-stu-id="b86dd-284">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="b86dd-285">一位</span><span class="sxs-lookup"><span data-stu-id="b86dd-285">Moodle</span></span>](https://moodle.org/)

> [!div class="nextstepaction"]
> <span data-ttu-id="b86dd-286">[一个文档](https://docs.moodle.org/34/en/Installing_plugins)。</span><span class="sxs-lookup"><span data-stu-id="b86dd-286">[Moodle documentation](https://docs.moodle.org/34/en/Installing_plugins).</span></span>
