---
title: 安装 Moodle LMS
description: 如何安装和配置适用于 Windows 的一Microsoft Teams
keywords: Teams一流应用集成插件
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: surbhigupta
ms.openlocfilehash: 54f4fec4e240f866c686ed715bd5093a319a2a48
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069175"
---
# <a name="install-moodle-lms"></a><span data-ttu-id="3984c-104">安装 Moodle LMS</span><span class="sxs-lookup"><span data-stu-id="3984c-104">Install Moodle LMS</span></span>

<span data-ttu-id="3984c-105">本文将学习如何安装一个将安装为 LmS 的一部分。</span><span class="sxs-lookup"><span data-stu-id="3984c-105">In this article you'll learn how to install the Moodle LMS.</span></span>

> [!NOTE]
> <span data-ttu-id="3984c-106">为了帮助 IT 管理员轻松设置一系列 Teams 和集成，Microsoft 365更新 Open-source Microsoft 365 Plugins：</span><span class="sxs-lookup"><span data-stu-id="3984c-106">To help IT admins to easily set-up Moodle and Teams integration, open-source Microsoft 365 Moodle Plugins is updated for the following:</span></span>
>
> * <span data-ttu-id="3984c-107">使用[Azure AD ](https://azure.microsoft.com/services/active-directory/)Azure Active Directory (自动注册 Your Your Moodle) 。</span><span class="sxs-lookup"><span data-stu-id="3984c-107">Auto-registration of your Moodle server with [Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/).</span></span>
>
> * <span data-ttu-id="3984c-108">只需单击一下即可将你的 Your Assistant bot 部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="3984c-108">One-click deployment of your Moodle Assistant bot to Azure.</span></span>
>
> * <span data-ttu-id="3984c-109">自动预配团队以及自动同步所有或选择"一流"课程的团队注册。</span><span class="sxs-lookup"><span data-stu-id="3984c-109">Auto-provisioning of teams and auto-synchronization of team enrollments for all or select Moodle courses.</span></span>
>
> * <span data-ttu-id="3984c-110">自动将"一页"选项卡和"将一个将一位"的"将一位"助手自动安装到每个同步的团队中。</span><span class="sxs-lookup"><span data-stu-id="3984c-110">Auto-installation of the Moodle tab and the Moodle assistant bot into each synchronized team.</span></span>
>
> <span data-ttu-id="3984c-111">若要详细了解此集成提供的功能，请参阅 Microsoft Teams[和一个。](https://education.microsoft.com/resource/3dffb3a8)</span><span class="sxs-lookup"><span data-stu-id="3984c-111">To learn more about the functionality this integration provides, see [Microsoft Teams and Moodle](https://education.microsoft.com/resource/3dffb3a8).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3984c-112">先决条件</span><span class="sxs-lookup"><span data-stu-id="3984c-112">Prerequisites</span></span>

<span data-ttu-id="3984c-113">以下是安装一个将一位用户安装在一起的先决条件：</span><span class="sxs-lookup"><span data-stu-id="3984c-113">Following are the prerequisites to install Moodle:</span></span>

* <span data-ttu-id="3984c-114">获取管理员凭据。</span><span class="sxs-lookup"><span data-stu-id="3984c-114">Moodle administrator credentials.</span></span>

* <span data-ttu-id="3984c-115">Azure AD 管理员凭据。</span><span class="sxs-lookup"><span data-stu-id="3984c-115">Azure AD administrator credentials.</span></span>

* <span data-ttu-id="3984c-116">可在其中创建新资源的 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="3984c-116">An Azure subscription where you can create new resources.</span></span>

## <a name="1-install-the-microsoft-365-moodle-plugins"></a><span data-ttu-id="3984c-117">1. 安装 Microsoft 365 Plugins</span><span class="sxs-lookup"><span data-stu-id="3984c-117">1. Install the Microsoft 365 Moodle Plugins</span></span>

<span data-ttu-id="3984c-118">企业中的Microsoft Teams由开放源代码Microsoft 365[一个插件集提供支持](https://github.com/Microsoft/o365-moodle)。</span><span class="sxs-lookup"><span data-stu-id="3984c-118">Moodle integration in Microsoft Teams is powered by the open source [Microsoft 365 Moodle plugins set](https://github.com/Microsoft/o365-moodle).</span></span>

### <a name="requisite-applications-and-plugins"></a><span data-ttu-id="3984c-119">必需的应用程序和插件</span><span class="sxs-lookup"><span data-stu-id="3984c-119">Requisite applications and plugins</span></span>

<span data-ttu-id="3984c-120">请确保先安装和下载以下内容，然后再继续安装 Microsoft 365 Pluginle 插件：</span><span class="sxs-lookup"><span data-stu-id="3984c-120">Ensure to install and download the following before proceeding with the Microsoft 365 Moodle plugins installation:</span></span>

1. <span data-ttu-id="3984c-121">确保安装 [Stablele 的当前稳定版本](https://download.moodle.org/releases/latest/)。</span><span class="sxs-lookup"><span data-stu-id="3984c-121">Ensure to install a [current stable version of Moodle](https://download.moodle.org/releases/latest/).</span></span>

1. <span data-ttu-id="3984c-122">下载并保存一个将 连接[和](https://moodle.org/plugins/auth_oidc)Microsoft 365[集成](https://moodle.org/plugins/local_o365)插件保存到本地计算机。</span><span class="sxs-lookup"><span data-stu-id="3984c-122">Download and save the Moodle [OpenID Connect](https://moodle.org/plugins/auth_oidc) and the [Microsoft 365 Integration](https://moodle.org/plugins/local_o365) plugins to your local computer.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3984c-123">安装 OpenID 连接和Microsoft 365集成插件是集成Teams要求。</span><span class="sxs-lookup"><span data-stu-id="3984c-123">Installing the OpenID Connect and Microsoft 365 Integration plugins are required for the Teams integration.</span></span>
    >
    > <span data-ttu-id="3984c-124">此外，[强烈建议Microsoft 365 Teams](https://moodle.org/plugins/theme_boost_o365teams)主题插件。</span><span class="sxs-lookup"><span data-stu-id="3984c-124">In addition, the [Microsoft 365 Teams Theme](https://moodle.org/plugins/theme_boost_o365teams) plugins is highly recommended.</span></span>

### <a name="microsoft-365-moodle-plugins"></a><span data-ttu-id="3984c-125">Microsoft 365中式插件</span><span class="sxs-lookup"><span data-stu-id="3984c-125">Microsoft 365 Moodle plugins</span></span>

1. <span data-ttu-id="3984c-126">以管理员角色登录到 Your Moodle server，然后从左侧导航面板设置[网站](https://docs.moodle.org/22/en/Settings_block)管理"块中选择"网站管理"。</span><span class="sxs-lookup"><span data-stu-id="3984c-126">Sign in to your Moodle server as an administrator and select **Site administration** from the [Settings block](https://docs.moodle.org/22/en/Settings_block) located in the left navigation panel.</span></span>

1. <span data-ttu-id="3984c-127">选择 **"插件"** 选项卡，然后选择"**安装插件"。**</span><span class="sxs-lookup"><span data-stu-id="3984c-127">Select the **Plugins** tab, and then select **Install plugins**.</span></span>

1. <span data-ttu-id="3984c-128">从"**从 ZIP 文件安装** 插件"部分，选择 **"选择文件"。**</span><span class="sxs-lookup"><span data-stu-id="3984c-128">From the **Install plugins from ZIP file** section, select **Choose a file**.</span></span>

1. <span data-ttu-id="3984c-129">Select **Upload a file** option from the left navigation panel， browse for the file that you downloaded， and select Upload this **file**.</span><span class="sxs-lookup"><span data-stu-id="3984c-129">Select **Upload a file** option from the left navigation panel, browse for the file that you downloaded, and select **Upload this file**.</span></span>

1. <span data-ttu-id="3984c-130">从 **左侧导航面板** 中选择"网站管理"以返回到管理员仪表板。</span><span class="sxs-lookup"><span data-stu-id="3984c-130">Select **Site administration** from the left navigation panel to return to your admin dashboard.</span></span> <span data-ttu-id="3984c-131">向下滚动到"**本地插件"** 并选择"Microsoft 365 **集成"** 链接。</span><span class="sxs-lookup"><span data-stu-id="3984c-131">Scroll down to the **Local plugins** and select the **Microsoft 365 Integration** link.</span></span>

    > [!IMPORTANT]
    >
    > * <span data-ttu-id="3984c-132">在Microsoft 365返回到这组页面时，在单独的浏览器选项卡中保持打开您的"Your Microsoft 365 Pluginle 插件配置"页面。</span><span class="sxs-lookup"><span data-stu-id="3984c-132">Keep your Microsoft 365 Moodle Plugins configuration page open in a separate browser tab as you need to return to this set of pages throughout the process.</span></span>  
    >
    > * <span data-ttu-id="3984c-133">如果你没有现有的一个一流网站，请转到 Azure 存储库上的 [设置](https://github.com/azure/moodle) ，并快速部署一个一个一流实例并根据需要自定义它。</span><span class="sxs-lookup"><span data-stu-id="3984c-133">If you do not have an existing Moodle site, go to the [Moodle on Azure](https://github.com/azure/moodle) repo, and quickly deploy a Moodle instance and customize it to your needs.</span></span>

## <a name="2-configure-the-connection-between-the-microsoft-365-plugins-and-azure-active-directory-azure-ad"></a><span data-ttu-id="3984c-134">2. 配置 Azure AD Microsoft 365应用程序Azure Active Directory (连接) </span><span class="sxs-lookup"><span data-stu-id="3984c-134">2. Configure the connection between the Microsoft 365 plugins and Azure Active Directory (Azure AD)</span></span>

<span data-ttu-id="3984c-135">你必须配置应用程序插件Microsoft 365 Azure AD 之间的连接。</span><span class="sxs-lookup"><span data-stu-id="3984c-135">You must configure the connection between the Microsoft 365 plugins and Azure AD.</span></span>

### <a name="requisites"></a><span data-ttu-id="3984c-136">先决条件</span><span class="sxs-lookup"><span data-stu-id="3984c-136">Requisites</span></span>

<span data-ttu-id="3984c-137">使用 PowerShell 脚本在 Azure AD 中将用户注册为应用程序。</span><span class="sxs-lookup"><span data-stu-id="3984c-137">Register Moodle as an application in your Azure AD, using the PowerShell script.</span></span> <span data-ttu-id="3984c-138">Powershell 脚本设置以下内容：</span><span class="sxs-lookup"><span data-stu-id="3984c-138">The Powershell script provisions the following:</span></span>

* <span data-ttu-id="3984c-139">适用于你的 Microsoft 365 租户的新 Azure AD 应用程序，由 Microsoft 365 Plugins 使用。</span><span class="sxs-lookup"><span data-stu-id="3984c-139">A new Azure AD application for your Microsoft 365 tenant, which is used by the Microsoft 365 Moodle Plugins.</span></span>
* <span data-ttu-id="3984c-140">你的租户Microsoft 365，为预配的应用设置所需的回复 URL 和权限，并返回 `AppID` 和 `Key` 。</span><span class="sxs-lookup"><span data-stu-id="3984c-140">The app for your Microsoft 365 tenant, set up the required reply URLs and permissions for the provisioned app, and returns the `AppID` and `Key`.</span></span>

<span data-ttu-id="3984c-141">使用生成的 和 在 Microsoft 365 `AppID` `Key` Plugins 设置页中，使用 Azure AD 配置 Your Your Moodle 服务器网站。</span><span class="sxs-lookup"><span data-stu-id="3984c-141">Use the generated `AppID` and `Key` in your Microsoft 365 Moodle Plugins setup page to configure your Moodle server site with Azure AD.</span></span>

> [!IMPORTANT]
>
> * <span data-ttu-id="3984c-142">PowerShell 脚本没有使用最新的配置项进行更新，因此，你必须按照在一个 [3.8.0.4 和 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) 以及 [3.8.0.5 和 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) 发行版页面中概述的步骤手动完成配置。</span><span class="sxs-lookup"><span data-stu-id="3984c-142">The PowerShell script is not updated with the latest configuration items, therefore, you must complete the configuration manually following the steps outlined in the Moodle [3.8.0.4 and 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) and [3.8.0.5 and 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) release pages.</span></span>
>
> * <span data-ttu-id="3984c-143">有关手动注册你的一个将你的一个将你的一个设置实例注册到应用程序上的信息，请参阅将 [你的一个将你的一个将一个你的一个实例注册为一个应用程序](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)。</span><span class="sxs-lookup"><span data-stu-id="3984c-143">For more information on registering your Moodle instance manually, see [Register your Moodle instance as an application](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application).</span></span>

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a><span data-ttu-id="3984c-144">用于信息流的"Microsoft Teams选项卡</span><span class="sxs-lookup"><span data-stu-id="3984c-144">The Moodle tab for Microsoft Teams information flow</span></span>

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. <span data-ttu-id="3984c-145">从"Microsoft 365集成插件"页中，选择"设置 **"** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="3984c-145">From the Microsoft 365 Integration plugins page, select the **Setup** tab.</span></span>

1. <span data-ttu-id="3984c-146">选择" **下载 PowerShell 脚本"** 按钮，并将其另存为 ZIP 文件夹到本地计算机。</span><span class="sxs-lookup"><span data-stu-id="3984c-146">Select the **Download PowerShell Script** button and save it as a ZIP folder to your local computer.</span></span>

1. <span data-ttu-id="3984c-147">从 ZIP 文件准备 PowerShell 脚本，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3984c-147">Prepare the PowerShell script from the ZIP file as follows:</span></span> 

    1. <span data-ttu-id="3984c-148">下载并解压缩 `Moodle-AzureAD-Powershell.zip` 文件。</span><span class="sxs-lookup"><span data-stu-id="3984c-148">Download and extract the `Moodle-AzureAD-Powershell.zip` file.</span></span>
    1. <span data-ttu-id="3984c-149">打开提取的文件夹。</span><span class="sxs-lookup"><span data-stu-id="3984c-149">Open the extracted folder.</span></span>
    1. <span data-ttu-id="3984c-150">右键单击文件 `Moodle-AzureAD-Script.ps1` ，然后选择属性。</span><span class="sxs-lookup"><span data-stu-id="3984c-150">Right-click on the `Moodle-AzureAD-Script.ps1` file and select **Properties**.</span></span>
    1. <span data-ttu-id="3984c-151">在"**属性**"窗口的"常规"选项卡下，选中位于窗口底部的 Security 属性旁边的 `Unblock` 复选框。 </span><span class="sxs-lookup"><span data-stu-id="3984c-151">Under the **General** tab of the Properties window, select the `Unblock` checkbox next to the **Security** attribute located at the bottom of the window.</span></span>
    1. <span data-ttu-id="3984c-152">选择“**确定**”。</span><span class="sxs-lookup"><span data-stu-id="3984c-152">Select **OK**.</span></span>
    1. <span data-ttu-id="3984c-153">将目录路径复制到提取的文件夹。</span><span class="sxs-lookup"><span data-stu-id="3984c-153">Copy the directory path to the extracted folder.</span></span>

1. <span data-ttu-id="3984c-154">以管理员角色运行 PowerShell：</span><span class="sxs-lookup"><span data-stu-id="3984c-154">Run PowerShell as an administrator:</span></span>

    1. <span data-ttu-id="3984c-155">选择“开始”。</span><span class="sxs-lookup"><span data-stu-id="3984c-155">Select Start.</span></span>
    1. <span data-ttu-id="3984c-156">键入 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="3984c-156">Type PowerShell.</span></span>
    1. <span data-ttu-id="3984c-157">右键单击 **"Windows PowerShell"。**</span><span class="sxs-lookup"><span data-stu-id="3984c-157">Right-click on **Windows PowerShell**.</span></span>
    1. <span data-ttu-id="3984c-158">选择 **"以管理员角色运行"。**</span><span class="sxs-lookup"><span data-stu-id="3984c-158">Select **Run as Administrator**.</span></span>

1. <span data-ttu-id="3984c-159">通过键入 where 是目录的路径，导航到 `cd .../.../Moodle-AzureAD-Powershell` `.../...` 解压缩目录。</span><span class="sxs-lookup"><span data-stu-id="3984c-159">Navigate to the unzipped directory by typing `cd .../.../Moodle-AzureAD-Powershell` where `.../...` is the path to the directory.</span></span>

1. <span data-ttu-id="3984c-160">执行 PowerShell 脚本：</span><span class="sxs-lookup"><span data-stu-id="3984c-160">Execute the PowerShell script:</span></span>

    1. <span data-ttu-id="3984c-161">输入 `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` 。</span><span class="sxs-lookup"><span data-stu-id="3984c-161">Enter `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`.</span></span>
    1. <span data-ttu-id="3984c-162">输入 `./Moodle-AzureAD-Script.ps1` 。</span><span class="sxs-lookup"><span data-stu-id="3984c-162">Enter `./Moodle-AzureAD-Script.ps1`.</span></span>
    1. <span data-ttu-id="3984c-163">在弹出窗口中Microsoft 365你的管理员帐户。</span><span class="sxs-lookup"><span data-stu-id="3984c-163">Sign in to your Microsoft 365 administrator account in the pop-up window.</span></span>
    1. <span data-ttu-id="3984c-164">输入 Azure AD 应用程序的名称，例如，一个，一个，一个，一个 Pluginle 或一个 Pluginle 插件。</span><span class="sxs-lookup"><span data-stu-id="3984c-164">Enter the name of the Azure AD Application, for example, Moodle or Moodle plugins.</span></span>
    1. <span data-ttu-id="3984c-165">输入 Your Your Moodle 服务器的 URL。</span><span class="sxs-lookup"><span data-stu-id="3984c-165">Enter the URL for your Moodle server.</span></span>
    1. <span data-ttu-id="3984c-166">复制 **脚本生成的 `AppID` ()** 应用程序 ID () 并保存 **`Key`** 它们。</span><span class="sxs-lookup"><span data-stu-id="3984c-166">Copy the **Application ID (`AppID`)** and **Application Key(`Key`)** generated by the script and save them.</span></span>

1. <span data-ttu-id="3984c-167">接下来，你必须将 `AppID` 和 `Key` 添加到 Microsoft 365 Plugins。</span><span class="sxs-lookup"><span data-stu-id="3984c-167">Next you must add the `AppID` and `Key` to the Microsoft 365 Moodle Plugins.</span></span> <span data-ttu-id="3984c-168">返回到插件管理页面，网站管理>插件> Microsoft 365集成。</span><span class="sxs-lookup"><span data-stu-id="3984c-168">Return to the plugins administration page, Site administration > Plugins > Microsoft 365 Integration.</span></span>

1. <span data-ttu-id="3984c-169">在"**设置**"选项卡上，添加 和之前复制的 ， `AppID` `Key` 然后选择"保存 **更改"。**</span><span class="sxs-lookup"><span data-stu-id="3984c-169">On the **Setup** tab add the `AppID` and `Key` you copied previously, and then select **Save changes**.</span></span> <span data-ttu-id="3984c-170">刷新页面后，可以看到新部分选择 **连接方法**。</span><span class="sxs-lookup"><span data-stu-id="3984c-170">After the page refreshes, you can see a new section **Choose connection method**.</span></span>

1. <span data-ttu-id="3984c-171">在"**选择连接方法**"中，选中标记为"默认"的复选框，然后再次选择"**保存更改**"。</span><span class="sxs-lookup"><span data-stu-id="3984c-171">In the **Choose connection method**, select the checkbox labeled **Default**, and then select **Save changes** again.</span></span>

1. <span data-ttu-id="3984c-172">刷新页面后，你可以看到另一个新部分管理员同意& **其他信息**。</span><span class="sxs-lookup"><span data-stu-id="3984c-172">After the page refreshes you can see another new section **Admin consent & additional information**.</span></span>
    1. <span data-ttu-id="3984c-173">选择 **"提供管理员同意**"链接，Microsoft 365全局管理员凭据，然后 **接受** 以授予权限。</span><span class="sxs-lookup"><span data-stu-id="3984c-173">Select **Provide Admin Consent** link, enter your Microsoft 365 Global Administrator credentials, then **Accept** to grant the permissions.</span></span>
    1. <span data-ttu-id="3984c-174">在 **"Azure AD 租户** "字段旁边，选择" **检测"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="3984c-174">Next to the **Azure AD Tenant** field, select the **Detect** button.</span></span>
    1. <span data-ttu-id="3984c-175">在 URL **OneDrive for Business，** 选择"检测 **"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="3984c-175">Next to the **OneDrive for Business URL**, select the **Detect** button.</span></span>
    1. <span data-ttu-id="3984c-176">填充字段后，再次选择 **"保存更改"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="3984c-176">After the fields populate, select the **Save changes** button again.</span></span>

1. <span data-ttu-id="3984c-177">选择"**更新"** 按钮以验证安装，然后选择"保存 **更改"。**</span><span class="sxs-lookup"><span data-stu-id="3984c-177">Select the **Update** button to verify the installation, and then select **Save changes**.</span></span>

1. <span data-ttu-id="3984c-178">在将用户同步到你的一台将你的服务器与 Azure AD 之间。</span><span class="sxs-lookup"><span data-stu-id="3984c-178">Synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="3984c-179">首先，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="3984c-179">To get started:</span></span>

    > [!NOTE]
    > <span data-ttu-id="3984c-180">根据你的环境，你可以在此阶段选择不同的选项。</span><span class="sxs-lookup"><span data-stu-id="3984c-180">Depending on your environment, you can select different options during this stage.</span></span>

1. <span data-ttu-id="3984c-181">在将用户同步到你的一台将你的服务器与 Azure AD 之间。</span><span class="sxs-lookup"><span data-stu-id="3984c-181">Synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="3984c-182">根据你的环境，你可以在此阶段选择不同的选项。</span><span class="sxs-lookup"><span data-stu-id="3984c-182">Depending on your environment, you can select different options during this stage.</span></span> <span data-ttu-id="3984c-183">首先，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="3984c-183">To get started:</span></span>
    1. <span data-ttu-id="3984c-184">切换到"同步 **设置选项卡**。</span><span class="sxs-lookup"><span data-stu-id="3984c-184">Switch to the **Sync Settings tab**.</span></span>

    1. <span data-ttu-id="3984c-185">在 **"将用户与 Azure AD** 同步"部分中，选中适用于你的环境的复选框。</span><span class="sxs-lookup"><span data-stu-id="3984c-185">In the **Sync users with Azure AD** section, select the checkboxes that apply to your environment.</span></span> <span data-ttu-id="3984c-186">您必须选择以下选项：</span><span class="sxs-lookup"><span data-stu-id="3984c-186">You must select the following:</span></span>  

        <span data-ttu-id="3984c-187">✔ Azure AD 中的用户创建在在一起的帐户。</span><span class="sxs-lookup"><span data-stu-id="3984c-187">✔ Create accounts in Moodle for users in Azure AD.</span></span>

        <span data-ttu-id="3984c-188">✔ Azure AD 中的用户更新在在一起的所有帐户。</span><span class="sxs-lookup"><span data-stu-id="3984c-188">✔ Update all accounts in Moodle for users in Azure AD.</span></span>

    1. <span data-ttu-id="3984c-189">在 **"用户创建限制** "部分，可以设置筛选器以限制同步到一台的 Azure AD 用户。</span><span class="sxs-lookup"><span data-stu-id="3984c-189">In the **User Creation Restriction** section, you can setup a filter to limit the Azure AD users that is synced to Moodle.</span></span>
    1. <span data-ttu-id="3984c-190">通过 **"用户字段映射** "部分，你可以自定义 Azure AD 到一些用户个人资料字段映射。</span><span class="sxs-lookup"><span data-stu-id="3984c-190">The **User Field Mapping** section allows you to customize the Azure AD to Moodle User Profile field mapping.</span></span>
    1. <span data-ttu-id="3984c-191">在 **"Teams同步**"部分，可以选择自动创建组，例如某些或所有现有一些（或全部）的 Teams。</span><span class="sxs-lookup"><span data-stu-id="3984c-191">In the **Teams Sync** section, you can select to automatically create Groups, such as teams for some, or all, of your existing Moodle courses.</span></span>

13. <span data-ttu-id="3984c-192">若要验证 [cron](https://docs.moodle.org/310/en/Cron)作业并首次运行时手动运行它们，请选择"将用户与 **Azure AD** 同步"部分中的"计划任务管理"页链接。</span><span class="sxs-lookup"><span data-stu-id="3984c-192">To validate [cron](https://docs.moodle.org/310/en/Cron) jobs and run them manually for the first run, select the **Scheduled tasks management page** link in the **Sync users with Azure AD** section.</span></span> <span data-ttu-id="3984c-193">这会将您带至 **"计划任务"** 页。</span><span class="sxs-lookup"><span data-stu-id="3984c-193">This takes you to the **Scheduled Tasks** page.</span></span>

    1. <span data-ttu-id="3984c-194">向下滚动并查找"使用 **Azure AD 同步用户"** 作业，然后选择"**立即运行"。**</span><span class="sxs-lookup"><span data-stu-id="3984c-194">Scroll down and find the **Sync users with Azure AD** job and select **Run now**.</span></span>
    1. <span data-ttu-id="3984c-195">如果选择基于现有课程创建组，还可以在作业中运行创建 **Microsoft 365** 组。</span><span class="sxs-lookup"><span data-stu-id="3984c-195">If you select to create Groups based on existing courses, you can also run the **Create user groups in Microsoft 365** job.</span></span>

    > [!NOTE]
    >
    > <span data-ttu-id="3984c-196">将按照任务 [计划](https://docs.moodle.org/310/en/Cron) 运行一个将运行一个在一起。</span><span class="sxs-lookup"><span data-stu-id="3984c-196">The Moodle [Cron](https://docs.moodle.org/310/en/Cron) runs according to the task schedule.</span></span> <span data-ttu-id="3984c-197">默认计划为每天一次。</span><span class="sxs-lookup"><span data-stu-id="3984c-197">The default schedule is once a day.</span></span> <span data-ttu-id="3984c-198">但是，cron 必须更频繁地运行，以保持所有内容同步。</span><span class="sxs-lookup"><span data-stu-id="3984c-198">However, the cron must run more frequently to keep everything in sync.</span></span>

1. <span data-ttu-id="3984c-199">返回到"插件管理"页"网站管理>**插件> Microsoft 365集成**"，然后选择"Teams 设置 **页。**</span><span class="sxs-lookup"><span data-stu-id="3984c-199">Return to the plugins administration page, **Site administration > Plugins > Microsoft 365 Integration**, and select the **Teams Settings** page.</span></span>

1. <span data-ttu-id="3984c-200">在 **"Teams 设置"** 页上，配置所需的设置以启用Teams集成。</span><span class="sxs-lookup"><span data-stu-id="3984c-200">On the **Teams Settings** page, configure the required settings to enable the Teams app integration.</span></span>

    1. <span data-ttu-id="3984c-201">若要启用 **OpenID 连接，** 请选择"管理身份验证"链接，并选择 **OpenId** 连接（如果显示为灰色）上的目视图标。</span><span class="sxs-lookup"><span data-stu-id="3984c-201">To enable **OpenID Connect**, select the **Manage Authentication** link, and select the eye icon on the **OpenId Connect** line if it is greyed out.</span></span>
    1. <span data-ttu-id="3984c-202">若要启用帧嵌入，请选择 **"HTTP 安全** "链接，然后选中"允许嵌入帧 **"旁边的复选框**。</span><span class="sxs-lookup"><span data-stu-id="3984c-202">To enable frame embedding, select the **HTTP Security** link, and then select the checkbox next to **Allow frame embedding**.</span></span>
    1. <span data-ttu-id="3984c-203">若要启用启用用户 API 功能的 Web 服务，请选择"高级功能"链接，然后确保选中"启用 **Web** 服务"旁边的复选框。</span><span class="sxs-lookup"><span data-stu-id="3984c-203">To enable web services, which enables the Moodle API features, select the **Advanced Features** link, and then ensure the checkbox next to **Enable web services** is selected.</span></span>
    1. <span data-ttu-id="3984c-204">若要为外部服务启用Microsoft 365，请选择"**外部服务**"链接，然后：</span><span class="sxs-lookup"><span data-stu-id="3984c-204">To enable the external services for Microsoft 365, select the **External services** link, and then:</span></span>  

        <span data-ttu-id="3984c-205">✔在 **"Webservices"行Microsoft 365选择"编辑**"。 </span><span class="sxs-lookup"><span data-stu-id="3984c-205">✔ Select **Edit** on the **Moodle Microsoft 365 Webservices** row.</span></span>

        <span data-ttu-id="3984c-206">✔ 选中"已启用"旁边的 **复选框，然后选择**" **保存更改"**</span><span class="sxs-lookup"><span data-stu-id="3984c-206">✔ Select the checkbox next to **Enabled**, then select **Save Changes**</span></span>

    1. <span data-ttu-id="3984c-207">编辑经过身份验证的用户权限，以允许他们创建 Web 服务令牌。</span><span class="sxs-lookup"><span data-stu-id="3984c-207">Edit your authenticated user permissions to allow them to create web service tokens.</span></span>

        <span data-ttu-id="3984c-208">✔选择 **"编辑角色经过身份验证的用户"** 链接。</span><span class="sxs-lookup"><span data-stu-id="3984c-208">✔ Select the **Editing role Authenticated user** link.</span></span>

        <span data-ttu-id="3984c-209">✔向下滚动并找到"创建 **Web** 服务令牌"功能，然后选中" **允许"** 复选框。</span><span class="sxs-lookup"><span data-stu-id="3984c-209">✔ Scroll down and find the **Create a web service token** capability and select the **Allow** checkbox.</span></span>

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a><span data-ttu-id="3984c-210">3. 将用户助理机器人部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="3984c-210">3. Deploy the Moodle Assistant Bot to Azure</span></span>

<span data-ttu-id="3984c-211">适用于教育的免费一Microsoft Teams自动程序可帮助教师和学生回答有关其课程、作业、成绩和其他在一起的问题。</span><span class="sxs-lookup"><span data-stu-id="3984c-211">The free Moodle assistant bot for Microsoft Teams helps teachers and students answer questions about their courses, assignments, grades, and other information in Moodle.</span></span> <span data-ttu-id="3984c-212">机器人还会向用户内的学生和教师发送一Teams。</span><span class="sxs-lookup"><span data-stu-id="3984c-212">The bot also sends Moodle notifications to students and teachers within Teams.</span></span> <span data-ttu-id="3984c-213">自动程序是由 Microsoft 维护的开放源代码项目，可用于[GitHub。](https://github.com/microsoft/Moodle-Teams-Bot)</span><span class="sxs-lookup"><span data-stu-id="3984c-213">The bot is an open-source project maintained by Microsoft, and is available on [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).</span></span>

> [!NOTE]
>
> * <span data-ttu-id="3984c-214">将资源部署到 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="3984c-214">Deploy resources to your Azure subscription.</span></span> <span data-ttu-id="3984c-215">所有资源均使用免费 **层** 进行配置。</span><span class="sxs-lookup"><span data-stu-id="3984c-215">All resources were configured using the **free** tier.</span></span> <span data-ttu-id="3984c-216">根据自动程序使用情况，你可能必须扩展这些资源。</span><span class="sxs-lookup"><span data-stu-id="3984c-216">Depending on the usage of your bot, you may have to scale these resources.</span></span>
>
> * <span data-ttu-id="3984c-217">若要在没有自动程序的情况下使用"操作方式"选项卡，请跳到 [4](#4-deploy-your-microsoft-teams-app)。</span><span class="sxs-lookup"><span data-stu-id="3984c-217">To use the Moodle tab without the bot, skip to [4](#4-deploy-your-microsoft-teams-app).</span></span>

### <a name="moodle-bot-information-flow"></a><span data-ttu-id="3984c-218">自动程序信息流</span><span class="sxs-lookup"><span data-stu-id="3984c-218">Moodle bot information flow</span></span>

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

<span data-ttu-id="3984c-219">若要安装自动程序，必须在 Microsoft 标识平台上 [注册它](https://identity.microsoft.com/Landing)。</span><span class="sxs-lookup"><span data-stu-id="3984c-219">To install the bot, you must register it on the [Microsoft Identity Platform](https://identity.microsoft.com/Landing).</span></span> <span data-ttu-id="3984c-220">这允许机器人针对 Microsoft 终结点进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="3984c-220">This allows your bot to authenticate against your Microsoft endpoints.</span></span> 

<span data-ttu-id="3984c-221">**注册自动程序**</span><span class="sxs-lookup"><span data-stu-id="3984c-221">**To register your bot**</span></span>

1. <span data-ttu-id="3984c-222">转到"插件管理"页，然后选择"**插件"。**</span><span class="sxs-lookup"><span data-stu-id="3984c-222">Go to the plugins administration page, and then select **Plugins**.</span></span> <span data-ttu-id="3984c-223">在 **Microsoft 365集成"** 下，选择 **"Teams 设置"** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="3984c-223">Under **Microsoft 365 Integration**, select the **Teams Settings** tab.</span></span>

1. <span data-ttu-id="3984c-224">选择 **"Microsoft 应用程序注册门户** "链接，然后使用 Microsoft ID 登录。</span><span class="sxs-lookup"><span data-stu-id="3984c-224">Select the **Microsoft Application Registration Portal** link and sign in with your Microsoft ID.</span></span>

1. <span data-ttu-id="3984c-225">输入你的应用的名称，例如，一个在一起， **然后选择创建按钮** 。</span><span class="sxs-lookup"><span data-stu-id="3984c-225">Enter a name for your app, such as MoodleBot and select the **Create** button.</span></span>

1. <span data-ttu-id="3984c-226">复制应用程序 **ID 并将其** 粘贴到"团队管理"页上的"自动程序应用程序 **ID"设置** 字段中。 </span><span class="sxs-lookup"><span data-stu-id="3984c-226">Copy the **Application ID** and paste it into the **Bot Application ID** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="3984c-227">选择" **生成新密码"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="3984c-227">Select the **Generate New Password** button.</span></span> <span data-ttu-id="3984c-228">复制生成的密码，并将其粘贴到"团队密码"页上的"自动程序应用程序 **设置** 字段中。</span><span class="sxs-lookup"><span data-stu-id="3984c-228">Copy the generated password and and paste it into the **Bot Application Password** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="3984c-229">滚动到表单底部，然后选择"保存 **更改"。**</span><span class="sxs-lookup"><span data-stu-id="3984c-229">Scroll to the bottom of the form and select **Save Changes**.</span></span>

<span data-ttu-id="3984c-230">生成应用程序 ID 和密码后，将机器人部署到 Azure：</span><span class="sxs-lookup"><span data-stu-id="3984c-230">After generating your application ID and password, deploy your bot to Azure:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3984c-231">选择 **"部署到 Azure"，** 然后使用必要的信息（如"自动程序应用程序 ID"、"自动程序应用程序密码"和"Teams 设置密码 **）填写** 表单。</span><span class="sxs-lookup"><span data-stu-id="3984c-231">Select **Deploy to Azure** and complete the form with the necessary information, such as the Bot Application ID, Bot Application Password, and the Moodle Secret on the **Teams Settings** page.</span></span> <span data-ttu-id="3984c-232">Azure 信息位于"设置 **"** 页面上。</span><span class="sxs-lookup"><span data-stu-id="3984c-232">The Azure information is on the **Setup** page.</span></span> 
> * <span data-ttu-id="3984c-233">完成表单后，选中复选框以同意条款和条件。</span><span class="sxs-lookup"><span data-stu-id="3984c-233">After completing the form, select the checkbox to agree to the terms and conditions.</span></span>
> * <span data-ttu-id="3984c-234">选择 **购买**。</span><span class="sxs-lookup"><span data-stu-id="3984c-234">Select **Purchase**.</span></span> <span data-ttu-id="3984c-235">所有 Azure 资源都部署到免费层。</span><span class="sxs-lookup"><span data-stu-id="3984c-235">All Azure resources are deployed to the free tier.</span></span>

<span data-ttu-id="3984c-236">资源部署到 Azure 后，必须使用消息终结点Microsoft 365一个设置一个将一个"一Microsoft 365一个 Pluginle 插件。</span><span class="sxs-lookup"><span data-stu-id="3984c-236">After the resources have completed deploying to Azure, you must configure the Microsoft 365 Moodle plugins with a messaging endpoint.</span></span> <span data-ttu-id="3984c-237">你必须从 Azure 中的机器人获取终结点：</span><span class="sxs-lookup"><span data-stu-id="3984c-237">You must get the endpoint from your bot in Azure:</span></span>

1. <span data-ttu-id="3984c-238">登录 [Azure 门户](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="3984c-238">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="3984c-239">在左侧窗格中，选择" **资源组** "，并选择你使用或创建的资源组，同时部署机器人。</span><span class="sxs-lookup"><span data-stu-id="3984c-239">In the left pane, select **Resource groups** and select the resource group you used or created, while deploying your bot.</span></span>

1. <span data-ttu-id="3984c-240">从 **组的资源列表中选择 WebApp** Bot 资源。</span><span class="sxs-lookup"><span data-stu-id="3984c-240">Select the **WebApp Bot** resource from the list of resources in the group.</span></span>

1. <span data-ttu-id="3984c-241">从" **概述"部分** 复制 **消息终结点** 。</span><span class="sxs-lookup"><span data-stu-id="3984c-241">Copy the **Messaging Endpoint** from the **Overview** section.</span></span>

1. <span data-ttu-id="3984c-242">在"在将 **"设置"** 中，打开"Team Microsoft 365 Plugins"页面。</span><span class="sxs-lookup"><span data-stu-id="3984c-242">In Moodle, open the **Team Settings** page of your Microsoft 365 Moodle Plugins.</span></span>

1. <span data-ttu-id="3984c-243">在 **自动程序终结点** 字段中粘贴你刚刚复制的 URL，然后将单词 *消息* 更改为 *webhook*。</span><span class="sxs-lookup"><span data-stu-id="3984c-243">In the **Bot Endpoint** field paste the URL you just copied and change the word *messages* to *webhook*.</span></span> <span data-ttu-id="3984c-244">URL 必须如下所示： `https://botname.azurewebsites.net/api/webhook`</span><span class="sxs-lookup"><span data-stu-id="3984c-244">The URL must appear as follows: `https://botname.azurewebsites.net/api/webhook`</span></span>

1. <span data-ttu-id="3984c-245">选择 **"保存更改"。**</span><span class="sxs-lookup"><span data-stu-id="3984c-245">Select **Save Changes**.</span></span>

1. <span data-ttu-id="3984c-246">保存更改后，返回到"团队设置选项卡，选择"下载清单文件"按钮，将应用清单包保存到计算机以进一步使用。</span><span class="sxs-lookup"><span data-stu-id="3984c-246">After saving the changes, go back to the **Team Settings** tab, select the **Download manifest file** button, and save the app manifest package to your computer for further use.</span></span>

## <a name="4-deploy-your-microsoft-teams-app"></a><span data-ttu-id="3984c-247">4. 部署Microsoft Teams应用程序</span><span class="sxs-lookup"><span data-stu-id="3984c-247">4. Deploy your Microsoft Teams app</span></span>

<span data-ttu-id="3984c-248">在将机器人部署到 Azure 并配置为与你的 Talkle 服务器通信后，你必须部署你的 Microsoft Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="3984c-248">After your bot deployed to Azure and configured to talk to your Moodle server, you must deploy your Microsoft Teams app.</span></span> <span data-ttu-id="3984c-249">为此，你必须加载从上一步中从"Microsoft 365 Plugins Team 设置"页面中下载的应用清单文件。</span><span class="sxs-lookup"><span data-stu-id="3984c-249">To do this you must load the app manifest file that you downloaded from the Microsoft 365 Moodle Plugins Team Settings page in the previous step.</span></span>

<span data-ttu-id="3984c-250">在安装应用之前，必须确保启用外部应用和上传应用。</span><span class="sxs-lookup"><span data-stu-id="3984c-250">Before you install the app you must ensure to enable external apps and uploading of apps.</span></span> <span data-ttu-id="3984c-251">有关详细信息，请参阅[准备你的Microsoft 365租户](../concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="3984c-251">For more information, see [Prepare your Microsoft 365 tenant](../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span> 

<span data-ttu-id="3984c-252">**部署应用**</span><span class="sxs-lookup"><span data-stu-id="3984c-252">**To deploy your app**</span></span> 

1. <span data-ttu-id="3984c-253">打开 **Microsoft Teams**。</span><span class="sxs-lookup"><span data-stu-id="3984c-253">Open **Microsoft Teams**.</span></span> 

1. <span data-ttu-id="3984c-254">选择 **导航** 栏左下角区域的应用图标。</span><span class="sxs-lookup"><span data-stu-id="3984c-254">Select the **App** icon on the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="3984c-255">从 **Upload选择**"自定义应用"链接。</span><span class="sxs-lookup"><span data-stu-id="3984c-255">Select the **Upload a custom app** link from the list of options.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3984c-256">如果以全局管理员身份登录，则必须选择将应用程序上载到组织的应用程序目录，否则只能为作为成员的团队加载应用程序。</span><span class="sxs-lookup"><span data-stu-id="3984c-256">If you are logged in as a global administrator, you must have the option of uploading the app to your organization's app catalog, otherwise you can only load the app for a team in which you are a member.</span></span>

4. <span data-ttu-id="3984c-257">选择 `manifest.zip` 之前下载的程序包，然后选择保存。 </span><span class="sxs-lookup"><span data-stu-id="3984c-257">Select the `manifest.zip` package you downloaded previously and select **Save**.</span></span> <span data-ttu-id="3984c-258">如果尚未下载应用清单包，可以从在将插件配置页的 **"team 设置"** 选项卡下载到在一起。</span><span class="sxs-lookup"><span data-stu-id="3984c-258">If you have not downloaded the app manifest package, you can download from the **Team Settings** tab of the plugins configuration page in Moodle.</span></span>

<span data-ttu-id="3984c-259">现在，你已安装应用，你可以将选项卡添加到你有权访问的任何频道。</span><span class="sxs-lookup"><span data-stu-id="3984c-259">Now that you have the app installed, you can add the tab to any channel that you have access to.</span></span> <span data-ttu-id="3984c-260">为此，请导航到通道，选择 **加 (➕) 符号** ，然后从列表中选择你的应用。</span><span class="sxs-lookup"><span data-stu-id="3984c-260">To do so, navigate to the channel, select the **plus** (➕) symbol and select your app from the list.</span></span> <span data-ttu-id="3984c-261">按照提示完成向频道添加 Your Moodle 课程选项卡。</span><span class="sxs-lookup"><span data-stu-id="3984c-261">Follow the prompts to finish adding your Moodle course tab to a channel.</span></span>

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a><span data-ttu-id="3984c-262">5. 允许自动在 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3984c-262">5. Allow automatic creation of Moodle tabs in Microsoft Teams</span></span>

<span data-ttu-id="3984c-263">尽管在课程同步中手动创建"Microsoft Teams"选项卡，但你可以决定在通过课程同步创建团队时自动创建它们。</span><span class="sxs-lookup"><span data-stu-id="3984c-263">Although the Moodle tabs are created manually in Microsoft Teams, you can decide to create them automatically when teams are created from course synchronization.</span></span> <span data-ttu-id="3984c-264">为此，你必须在一个位于在一起配置Microsoft Teams应用的 ID。</span><span class="sxs-lookup"><span data-stu-id="3984c-264">To do this, you must configure the ID of the uploaded Microsoft Teams app in Moodle.</span></span>

<span data-ttu-id="3984c-265">**允许自动创建"设置"选项卡**</span><span class="sxs-lookup"><span data-stu-id="3984c-265">**To allow automatic creation of Moodle tabs**</span></span>

1. <span data-ttu-id="3984c-266">打开 Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="3984c-266">Open Microsoft Teams.</span></span>

1. <span data-ttu-id="3984c-267">从导航栏的左下角区域选择"应用"图标。</span><span class="sxs-lookup"><span data-stu-id="3984c-267">Select the Apps icon from the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="3984c-268">找到已上传 **的一>** 选择 **选项** 图标>选择 **复制链接**。</span><span class="sxs-lookup"><span data-stu-id="3984c-268">Locate the uploaded **Moodle app** > select the **options** icon > select **copy link**.</span></span>

1. <span data-ttu-id="3984c-269">在文本编辑器中，粘贴复制的内容。</span><span class="sxs-lookup"><span data-stu-id="3984c-269">In a text editor, paste the copied content.</span></span> <span data-ttu-id="3984c-270">它必须包含 URL，如 ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff。</span><span class="sxs-lookup"><span data-stu-id="3984c-270">It must contain a URL such as ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff.</span></span> <span data-ttu-id="3984c-271">复制 URL 的最后一部分，例如 ，这是应用Microsoft Teams `00112233-4455-6677-8899-aabbccddeeff` ID。</span><span class="sxs-lookup"><span data-stu-id="3984c-271">Copy the last part of the URL, such as  `00112233-4455-6677-8899-aabbccddeeff`, which is the ID of the Microsoft Teams app.</span></span>

1. <span data-ttu-id="3984c-272">在"在"在 **Teams"中**，从你的"Microsoft 365 Plugins 配置"页面打开"一个"将一个Microsoft 365一个"完成"应用选项卡。</span><span class="sxs-lookup"><span data-stu-id="3984c-272">In Moodle, open the **Teams Moodle app** tab from your Microsoft 365 Moodle Plugins configuration page.</span></span>

1. <span data-ttu-id="3984c-273">将应用 ID 粘贴到 Microsoft Teams 应用 ID 字段中，并保存更改。</span><span class="sxs-lookup"><span data-stu-id="3984c-273">Paste the ID of the Microsoft Teams app into the Moodle app ID field, and save changes.</span></span>

<span data-ttu-id="3984c-274">同步一个一个一流课程后，Microsoft Teams 会自动在团队中安装一个一流应用，在 Teams 的常规频道中创建一个"一个设置"选项卡，并对其进行配置以包含从中同步到的一个与一流课程课程的课程页面。</span><span class="sxs-lookup"><span data-stu-id="3984c-274">When a Moodle course is synced, Microsoft Teams automatically installs the Moodle app in the team, creates a Moodle tab in the General channel of Teams, and configures it to contain the course page for the Moodle course from which it is synced.</span></span> <span data-ttu-id="3984c-275">现在可以直接从你的组织开始使用你的Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="3984c-275">You can now start working with your Moodle courses directly from Microsoft Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="3984c-276">若要与我们共享任何功能请求或反馈，请访问我们的用户 [语音页面](https://microsoftteams.uservoice.com/forums/916759-moodle)。</span><span class="sxs-lookup"><span data-stu-id="3984c-276">To share any feature requests or feedback with us, visit our [User Voice page](https://microsoftteams.uservoice.com/forums/916759-moodle).</span></span>

## <a name="see-also"></a><span data-ttu-id="3984c-277">另请参阅</span><span class="sxs-lookup"><span data-stu-id="3984c-277">See also</span></span>

- [<span data-ttu-id="3984c-278">集成 web 应用</span><span class="sxs-lookup"><span data-stu-id="3984c-278">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
- [<span data-ttu-id="3984c-279">一位</span><span class="sxs-lookup"><span data-stu-id="3984c-279">Moodle</span></span>](https://moodle.org/)
- <span data-ttu-id="3984c-280">[一个文档](https://docs.moodle.org/34/en/Installing_plugins)。</span><span class="sxs-lookup"><span data-stu-id="3984c-280">[Moodle documentation](https://docs.moodle.org/34/en/Installing_plugins).</span></span>

