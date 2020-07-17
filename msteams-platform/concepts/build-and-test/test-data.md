---
title: 将测试数据添加到 Office 365 测试租户
description: 设置 Office 365 开发人员计划订阅，以成功测试 Microsoft 团队应用
keywords: 测试应用程序开发人员计划团队
ms.date: 11/01/2019
ms.openlocfilehash: 87e9dc280c192f013098c3e9f604f72238bfafdf
ms.sourcegitcommit: fdc50183f3f4bec9e4b83bcfe5e016b591402f7c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/24/2020
ms.locfileid: "44867089"
---
# <a name="add-test-data-to-your-office-365-test-tenant"></a><span data-ttu-id="ee622-104">将测试数据添加到 Office 365 测试租户</span><span class="sxs-lookup"><span data-stu-id="ee622-104">Add test data to your Office 365 test tenant</span></span>

<span data-ttu-id="ee622-105">设置您的 O365 开发人员计划订阅（或其他测试租户），以使您能够轻松测试您构建的应用程序。</span><span class="sxs-lookup"><span data-stu-id="ee622-105">Set up your O365 developer program subscription (or other test tenant) to make it easy for you to test the apps that you've built.</span></span>  <span data-ttu-id="ee622-106">它将帮助您：</span><span class="sxs-lookup"><span data-stu-id="ee622-106">It will help you:</span></span>

- <span data-ttu-id="ee622-107">在您的组织中创建新的团队和频道</span><span class="sxs-lookup"><span data-stu-id="ee622-107">Create new teams and channels in your organization</span></span>

- <span data-ttu-id="ee622-108">将通过用户内容包创建的用户添加到这些团队。</span><span class="sxs-lookup"><span data-stu-id="ee622-108">Add the users that are created via the User content pack to those teams.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="ee622-109">准备工作</span><span class="sxs-lookup"><span data-stu-id="ee622-109">Before you start</span></span>

<span data-ttu-id="ee622-110">如果尚不具有测试租户，则需要加入 Office 365 开发人员计划并注册开发人员订阅。</span><span class="sxs-lookup"><span data-stu-id="ee622-110">If you don't already have a test tenant, you will need to join the Office 365 developer program and sign up for a developer subscription.</span></span> <span data-ttu-id="ee622-111">你还需要安装必要的 PowerShell 模块。</span><span class="sxs-lookup"><span data-stu-id="ee622-111">You'll also need to install the necessary PowerShell modules.</span></span> <span data-ttu-id="ee622-112">对于您使用的任何租户，都需要具有全局管理员权限才能运行脚本。</span><span class="sxs-lookup"><span data-stu-id="ee622-112">For whatever tenant you use you'll need to have global administrator permissions to run the scripts.</span></span>

1. [<span data-ttu-id="ee622-113">加入 Office 365 开发人员计划</span><span class="sxs-lookup"><span data-stu-id="ee622-113">Join the Office 365 Developer Program</span></span>](/office/developer-program/office-365-developer-program)
2. [<span data-ttu-id="ee622-114">设置 Microsoft 365 开发人员订阅</span><span class="sxs-lookup"><span data-stu-id="ee622-114">Set up a Microsoft 365 Developer Subscription</span></span>](/office/developer-program/office-365-developer-program-get-started)
3. [<span data-ttu-id="ee622-115">将示例数据包与 Office 365 开发人员订阅结合使用，以安装用户内容包</span><span class="sxs-lookup"><span data-stu-id="ee622-115">Use sample data packs with your Office 365 developer subscription to install the Users content pack</span></span>](/office/developer-program/install-sample-packs)
4. [<span data-ttu-id="ee622-116">安装团队 PowerShell 模块</span><span class="sxs-lookup"><span data-stu-id="ee622-116">Install the Teams PowerShell module</span></span>](https://www.powershellgallery.com/packages/MicrosoftTeams/1.0.2)
5. [<span data-ttu-id="ee622-117">安装 Azure AD PowerShell 模块</span><span class="sxs-lookup"><span data-stu-id="ee622-117">Install the Azure AD PowerShell module</span></span>](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0#installing-the-azure-ad-module)

### <a name="optional-step-allow-upload-of-custom-apps"></a><span data-ttu-id="ee622-118">可选步骤：允许上载自定义应用程序</span><span class="sxs-lookup"><span data-stu-id="ee622-118">Optional step: allow upload of custom apps</span></span>

<span data-ttu-id="ee622-119">默认情况下，只有全局管理员或团队服务管理员才能将自定义应用程序上载到租户应用程序目录中。</span><span class="sxs-lookup"><span data-stu-id="ee622-119">By default, only global admins or teams service admins can upload custom apps into the tenant app catalog.</span></span>  <span data-ttu-id="ee622-120">您还可以让所有用户上载自定义应用程序以供自己使用或用于团队进行测试。</span><span class="sxs-lookup"><span data-stu-id="ee622-120">You can also enable all users to upload custom apps for their own use or to teams for testing.</span></span>

<span data-ttu-id="ee622-121">若要启用此设置，您需要在团队管理门户中更新全局应用安装程序策略。</span><span class="sxs-lookup"><span data-stu-id="ee622-121">To enable this setting, you'll need to update the global App Setup Policy in your Teams Admin Portal.</span></span>

<img width="430px" src="~/assets/images/microsoft-teams-admin-center-screenshot.png" title="应用程序安装策略的屏幕截图" />

<span data-ttu-id="ee622-123">有关详细信息，请参阅：</span><span class="sxs-lookup"><span data-stu-id="ee622-123">For more information see:</span></span>

 - [<span data-ttu-id="ee622-124">在 Microsoft 团队中管理应用程序安装策略</span><span class="sxs-lookup"><span data-stu-id="ee622-124">Manage app setup policies in Microsoft Teams</span></span>](/microsoftteams/teams-app-setup-policies)

## <a name="create-teams-and-channels"></a><span data-ttu-id="ee622-125">创建团队和频道</span><span class="sxs-lookup"><span data-stu-id="ee622-125">Create teams and channels</span></span>

<span data-ttu-id="ee622-126">将以下代码段保存为 XML （.xml），并注意保存它的位置。</span><span class="sxs-lookup"><span data-stu-id="ee622-126">Save the following snippet as an XML (.xml) and note where you've saved it.</span></span>  <span data-ttu-id="ee622-127">此 XML 定义将创建的团队和通道的结构及其成员。</span><span class="sxs-lookup"><span data-stu-id="ee622-127">This XML defines the structure of the teams and channels that will be created - along with its members.</span></span>

```xml
<?xml version="1.0"?>
<Teams>
  <Team Name="Store Portal" ID="storeportal" Description="" Type="Private" Creator="admin">
    <Members>
      <Member UserName="AlexW" IsOwner="false"/>
      <Member UserName="PattiF" IsOwner="false"/>
      <Member UserName="PradeepG" IsOwner="false"/>
      <Member UserName="JoniS" IsOwner="false"/>
      <Member UserName="JohannaL" IsOwner="false"/>
      <Member UserName="NestorW" IsOwner="false"/>
      <Member UserName="IsaiahL" IsOwner="false"/>
      <Member UserName="AdeleV" IsOwner="false"/>
      <Member UserName="LeeG" IsOwner="false"/>
      <Member UserName="MeganB" IsOwner="true"/>
      <Member UserName="LynneR" IsOwner="false"/>
      <Member UserName="GradyA" IsOwner="false"/>
      <Member UserName="LidiaH" IsOwner="false"/>
      <Member UserName="DiegoS" IsOwner="false"/>
      <Member UserName="MiriamG" IsOwner="true"/>
    </Members>
    <Channels>
      <Channel Name="Sales" ID="sales" Description="" Creator="Admin" />
      <Channel Name="Inventory" ID="inventory" Description="" Creator="Admin" />
      <Channel Name="Los Angeles Store 239" ID="losangelesstore239" Description="" Creator="Admin" />
      <Channel Name="Seattle Store 121" ID="seattlestore121" Description="" Creator="Admin" />
      <Channel Name="Online" ID="online" Description="" Creator="Admin" />
      <Channel Name="Store Layout" ID="storelayout" Description="" Creator="Admin" />
      <Channel Name="Promotions" ID="promotions" Description="" Creator="Admin" />
    </Channels>
  </Team>
  <Team Name="Mark 8 Project Team" ID="Mark8ProjectTeam" Description="Welcome to the team that we've assembled to create the Mark 8." Type="Private" Creator="admin">
    <Members>
      <Member UserName="meganb" IsOwner="true" />
      <Member UserName="alexw" IsOwner="false" />
      <Member UserName="lynner" IsOwner="false" />
      <Member UserName="isaiahl" IsOwner="false" />
      <Member UserName="leeg" IsOwner="false" />
      <Member UserName="pradeepg" IsOwner="false" />
      <Member UserName="lidiah" IsOwner="false" />
      <Member UserName="diegos" IsOwner="false" />
      <Member UserName="johannal" IsOwner="false" />
      <Member UserName="miriamg" IsOwner="false" />
      <Member UserName="adelev" IsOwner="false" />
      <Member UserName="jonis" IsOwner="false" />
      <Member UserName="nestorw" IsOwner="false" />
      <Member UserName="gradya" IsOwner="false" />
      <Member UserName="pattif" IsOwner="false" />
    </Members>
    <Channels>
      <Channel Name="Research and Development" ID="researchanddevelopment" Description="Channel for Research and Development!" Creator="meganb" />
      <Channel Name="Design" ID="design" Description="Discuss design projects." Creator="meganb" />
      <Channel Name="Digital Assets Web" ID="digitalassetsweb" Description="Discuss digital assets." Creator="meganb" />
      <Channel Name="Go to Market Plan" ID="gotomarketplan" Description="Our go-to-market plan!" Creator="meganb" />
    </Channels>
  </Team>
  <Team Name="District 9 Road Safety Audit" ID="district9roadsafetyaudit" Description="" Type="Private" Creator="admin">
    <Members>
      <Member UserName="meganb" IsOwner="true" />
      <Member UserName="alexw" IsOwner="false" />
      <Member UserName="lynner" IsOwner="false" />
      <Member UserName="isaiahl" IsOwner="false" />
      <Member UserName="leeg" IsOwner="false" />
      <Member UserName="pradeepg" IsOwner="false" />
      <Member UserName="lidiah" IsOwner="false" />
      <Member UserName="diegos" IsOwner="false" />
      <Member UserName="johannal" IsOwner="false" />
      <Member UserName="miriamg" IsOwner="false" />
      <Member UserName="adelev" IsOwner="false" />
      <Member UserName="jonis" IsOwner="false" />
      <Member UserName="nestorw" IsOwner="false" />
      <Member UserName="gradya" IsOwner="false" />
      <Member UserName="pattif" IsOwner="false" />
    </Members>
    <Channels>
      <Channel Name="Audit Planning" ID="auditplanning" Description="" Creator="Admin" />
      <Channel Name="Delivery" ID="delivery" Description="" Creator="Admin" />
      <Channel Name="Findings" ID="findings" Description="" Creator="Admin" />
      <Channel Name="Recommended Actions" ID="recommendedactions" Description="" Creator="Admin" />
      <Channel Name="Survey" ID="survey" Description="" Creator="Admin" />
    </Channels>
  </Team>
  <Team Name="ACC-1000 Product Team" ID="acc1000productteam" Description="" Type="Private" Creator="admin" >
    <Members>
      <Member UserName="meganb" IsOwner="true" />
      <Member UserName="alexw" IsOwner="false" />
      <Member UserName="lynner" IsOwner="false" />
      <Member UserName="isaiahl" IsOwner="false" />
      <Member UserName="leeg" IsOwner="false" />
      <Member UserName="pradeepg" IsOwner="false" />
      <Member UserName="lidiah" IsOwner="false" />
      <Member UserName="diegos" IsOwner="false" />
      <Member UserName="johannal" IsOwner="false" />
      <Member UserName="miriamg" IsOwner="false" />
      <Member UserName="adelev" IsOwner="false" />
      <Member UserName="jonis" IsOwner="false" />
      <Member UserName="nestorw" IsOwner="false" />
      <Member UserName="gradya" IsOwner="false" />
      <Member UserName="pattif" IsOwner="false" />
    </Members>
    <Channels>
      <Channel Name="Corporate Communication" ID="corporatecommunication" Description="" Creator="Admin" />
      <Channel Name="Lean Process Improvement" ID="corporatecommunication" Description="" Creator="Admin" />
      <Channel Name="Training and Certification" ID="trainingandcertification" Description="" Creator="Admin" />
      <Channel Name="Production" ID="production" Description="" Creator="Admin" />
      <Channel Name="Research and Development" ID="researchanddevelopment" Description="" Creator="Admin" />
      <Channel Name="Supplier Collaboration" ID="suppliercollaboration" Description="" Creator="Admin" />
    </Channels>
  </Team>
</Teams>
```

<span data-ttu-id="ee622-128">将以下代码段另存为 PowerShell 脚本（. ps1），并注意保存它的位置。</span><span class="sxs-lookup"><span data-stu-id="ee622-128">Save the following snippet as a PowerShell script (.ps1) and note where you've saved it.</span></span>  <span data-ttu-id="ee622-129">此脚本执行创建团队和频道并向其添加成员的步骤。</span><span class="sxs-lookup"><span data-stu-id="ee622-129">This script executes the steps to create the teams and channels and add members to them.</span></span>

```powershell
Param(
    [Parameter(Mandatory = $true)]
    
    # This specifies the location of your configuration XML.
    
    [string] $teamsFilePath 
)
    
[xml]$XmlDocument = Get-Content -Path $teamsFilePath.ToString()

if ($XmlDocument.Teams.Team.Count -gt 0) {

    try {
        
        # 1. Login with the global administrator account for your O365 Developer Program tenant.  This script will then use these credentials to connect to the powershell modules for Azure Active Directory and Microsoft Teams
        
        $creds = Get-Credential

        # Connecting to AAD PowerShell
        Connect-AzureAD -Credential $creds | Out-Null

        # Connect to Microsoft Teams PowerShell
        Connect-MicrosoftTeams -Credential $creds | Out-Null

        Write-Host "Connected to Microsoft 365 and configuring your organization with test teams and channels"

        # 2. Create the teams as specified in the XML.
        
        foreach ($team in $XmlDocument.Teams.Team ) {
            try {
                $group = New-Team -DisplayName $team.Name -Description $teams.description -visibility public 
                Write-Host "Successfully created team: " $group.DisplayName
            }
            catch {
                Write-Host "Unable to create team: $_"
            }
                
            # 3. Add users to the newly created teams.
            foreach ($user in $team.Members.Member) {
                try {
                    $newUserPrincipalName = (Get-AzureADUser -SearchString $user.UserName).UserPrincipalName

                    if($user.IsOwner -eq $true){
                        Add-TeamUser -GroupId $group.GroupId -User $newUserPrincipalName -Role Owner | Out-Null
                    }else{
                        Add-TeamUser -GroupId $group.GroupId -User $newUserPrincipalName | Out-Null
                    }

                    Write-Host "Successfully added user : " $user.UserName
                }
                catch {
                    Write-Host "Unable to add team user: $_"
                }

            }

            # 4. Add a set of channels to each newly created team
            foreach ($channel in $team.Channels.Channel) {
                try {
                    # Adding each team channel
                    New-TeamChannel -GroupId $group.GroupId -DisplayName $channel.Name -Description $channel.Description | Out-Null
                    Write-Host "Successfully created channel: " $channel.Name
                }
                catch {
                    Write-Host "Unable to add new Team Channel: $_"
                }   
            }

            Clear-Variable -Name group
        }

        Clear-Variable -Name creds
        
        # 5. Disconnect from all PowerShell sessions
        
        Write-Host "Completed execution and disconnecting from Microsoft 365 PowerShell sessions."
        Disconnect-MicrosoftTeams
        Disconnect-AzureAD
    }
    catch {
        Write-Host "Unable to complete the operation: $_"
    }
}
else {
    Write-Host "Content file has invalid data."
}
```

<span data-ttu-id="ee622-130">在管理员模式下打开 Windows PowerShell 会话。</span><span class="sxs-lookup"><span data-stu-id="ee622-130">Open a Windows PowerShell session in Administrator mode.</span></span>  <span data-ttu-id="ee622-131">运行刚才保存的脚本。</span><span class="sxs-lookup"><span data-stu-id="ee622-131">Run the script that you just saved.</span></span>  <span data-ttu-id="ee622-132">系统将提示您提供凭据-使用您在首次注册开发人员订阅时收到的全局管理员凭据。</span><span class="sxs-lookup"><span data-stu-id="ee622-132">You'll be prompted to provide the credentials - use the Global Administrator credentials you received when you first signed up for your developer subscription.</span></span>

> [!Note]
> <span data-ttu-id="ee622-133">脚本需要几分钟的时间才能执行-请勿关闭 PowerShell 会话。</span><span class="sxs-lookup"><span data-stu-id="ee622-133">The script will take several minutes to execute - do not close your PowerShell session.</span></span>  <span data-ttu-id="ee622-134">如果您已从默认内容包中创建的内容中修改了订阅中的用户，则某些用户可能不会添加到团队中。</span><span class="sxs-lookup"><span data-stu-id="ee622-134">If you've modified the users in your subscription from what is created in the default content pack, some users may not be added to teams.</span></span>  <span data-ttu-id="ee622-135">当脚本执行此操作时，它将输出成功或失败的操作。</span><span class="sxs-lookup"><span data-stu-id="ee622-135">As the script executes it will output successful or failed actions.</span></span>

<span data-ttu-id="ee622-136">一旦脚本完成执行，您就可以使用其中一个用户帐户登录到团队客户端，并查看新创建的团队。</span><span class="sxs-lookup"><span data-stu-id="ee622-136">Once the script has finished execution, you can login to the Teams client with one of the user accounts and view the newly created teams.</span></span>
