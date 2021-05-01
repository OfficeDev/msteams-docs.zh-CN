---
title: 将测试数据添加到Microsoft 365租户
description: 设置你的 Office 365 开发人员计划订阅，以成功测试 Microsoft Teams 应用
ms.topic: how-to
localization_priority: Normal
keywords: 测试应用开发人员计划团队
ms.date: 11/01/2019
ms.openlocfilehash: 9dcbd8f31c6ff68f0401e9fbb77297e8eebcf520
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101742"
---
# <a name="add-test-data-to-your-microsoft-365-test-tenant"></a><span data-ttu-id="f4284-104">将测试数据添加到Microsoft 365租户</span><span class="sxs-lookup"><span data-stu-id="f4284-104">Add test data to your Microsoft 365 test tenant</span></span>

<span data-ttu-id="f4284-105">可以使用开发人员订阅Microsoft Teams示例数据测试Microsoft 365应用。</span><span class="sxs-lookup"><span data-stu-id="f4284-105">You can test your Microsoft Teams app with sample data with a Microsoft 365 developer subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4284-106">先决条件</span><span class="sxs-lookup"><span data-stu-id="f4284-106">Prerequisites</span></span>

1. <span data-ttu-id="f4284-107">[如果您没有Microsoft 365，](/office/developer-program/office-365-developer-program)请加入开发人员计划。</span><span class="sxs-lookup"><span data-stu-id="f4284-107">[Join the Microsoft 365 Developer Program](/office/developer-program/office-365-developer-program), if you do not have a test tenant.</span></span>
2. <span data-ttu-id="f4284-108">[设置开发人员Microsoft 365订阅](/office/developer-program/office-365-developer-program-get-started)。</span><span class="sxs-lookup"><span data-stu-id="f4284-108">[Set up a Microsoft 365 Developer Subscription](/office/developer-program/office-365-developer-program-get-started).</span></span>
3. <span data-ttu-id="f4284-109">[将示例数据包与开发人员Microsoft 365一起安装 Users 内容包](/office/developer-program/install-sample-packs)。</span><span class="sxs-lookup"><span data-stu-id="f4284-109">[Use sample data packs with your Microsoft 365 developer subscription to install the Users content pack](/office/developer-program/install-sample-packs).</span></span>
4. <span data-ttu-id="f4284-110">[安装 Teams PowerShell 模块](https://www.powershellgallery.com/packages/MicrosoftTeams/1.0.2)。</span><span class="sxs-lookup"><span data-stu-id="f4284-110">[Install the Teams PowerShell module](https://www.powershellgallery.com/packages/MicrosoftTeams/1.0.2).</span></span>
5. <span data-ttu-id="f4284-111">[安装 Azure AD PowerShell 模块](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0#installing-the-azure-ad-module&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="f4284-111">[Install the Azure AD PowerShell module](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0#installing-the-azure-ad-module&preserve-view=true).</span></span>

> [!NOTE]
> <span data-ttu-id="f4284-112">必须在租户中具有全局管理员权限才能运行脚本。</span><span class="sxs-lookup"><span data-stu-id="f4284-112">You must have global admin permissions in the tenant to run the scripts.</span></span>

## <a name="allow-users-to-upload-apps"></a><span data-ttu-id="f4284-113">允许用户上载应用</span><span class="sxs-lookup"><span data-stu-id="f4284-113">Allow users to upload apps</span></span>

<span data-ttu-id="f4284-114">默认情况下，只有全局管理员或Teams管理员才能在租户 () 旁加载应用。</span><span class="sxs-lookup"><span data-stu-id="f4284-114">By default, only global admins or Teams service admins can upload (sideload) apps in a tenant.</span></span> <span data-ttu-id="f4284-115">还可以允许用户上载自定义应用供自己使用或上载到团队进行测试。</span><span class="sxs-lookup"><span data-stu-id="f4284-115">You can also allow users to upload custom apps for their own use or to teams for testing.</span></span> <span data-ttu-id="f4284-116">有关详细信息，请参阅管理自定义[应用策略和](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings)Teams。</span><span class="sxs-lookup"><span data-stu-id="f4284-116">For more information, see [manage custom app policies and settings in Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings).</span></span>

## <a name="create-teams-and-channels-for-testing"></a><span data-ttu-id="f4284-117">创建用于测试的团队和频道</span><span class="sxs-lookup"><span data-stu-id="f4284-117">Create teams and channels for testing</span></span>

1. <span data-ttu-id="f4284-118">将以下代码段另存 **为**.xml并记下文件路径。</span><span class="sxs-lookup"><span data-stu-id="f4284-118">Save the following snippet as a **.xml** file and note the file path.</span></span> <span data-ttu-id="f4284-119">此 XML 定义团队的结构和与其成员一起创建的频道：</span><span class="sxs-lookup"><span data-stu-id="f4284-119">This XML defines the structure of the team and channel that is created along with its members:</span></span>

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

2. <span data-ttu-id="f4284-120">将以下代码段另存为 PowerShell 脚本 (.ps1) 并记下保存位置。</span><span class="sxs-lookup"><span data-stu-id="f4284-120">Save the following snippet as a PowerShell script (.ps1) and note where you have saved it.</span></span> <span data-ttu-id="f4284-121">此脚本执行创建团队和频道的步骤，并添加成员：</span><span class="sxs-lookup"><span data-stu-id="f4284-121">This script executes the steps to create the team and channel, and add members to them:</span></span>

    ```powershell
    Param(
        [Parameter(Mandatory = $true)]

        # This specifies the location of your configuration XML.

        [string] $teamsFilePath 
    )

    [xml]$XmlDocument = Get-Content -Path $teamsFilePath.ToString()

    if ($XmlDocument.Teams.Team.Count -gt 0) {

        try {

            # 1. Login with the global administrator account for your O365 Developer Program tenant. This script uses these credentials to connect to the powershell modules for Azure Active Directory and Microsoft Teams

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

3. <span data-ttu-id="f4284-122">在管理员Windows PowerShell打开一个会话会话，然后运行刚保存的脚本。</span><span class="sxs-lookup"><span data-stu-id="f4284-122">Open a Windows PowerShell session in Administrator mode, and run the script that you just saved.</span></span>
4. <span data-ttu-id="f4284-123">当系统提示你提供凭据时，输入首次注册开发人员订阅时收到的全局管理员凭据。</span><span class="sxs-lookup"><span data-stu-id="f4284-123">When you are prompted to provide the credentials, enter the Global Administrator credentials you received when you first signed up for your developer subscription.</span></span>

    > [!Note]
    > <span data-ttu-id="f4284-124">不要关闭 PowerShell 会话，因为脚本需要几分钟时间才能执行。</span><span class="sxs-lookup"><span data-stu-id="f4284-124">Do not close your PowerShell session as the script takes several minutes to execute.</span></span> <span data-ttu-id="f4284-125">如果您修改了订阅中的用户，但从默认内容包中创建的内容进行了修改，则某些用户可能不会添加到Teams。</span><span class="sxs-lookup"><span data-stu-id="f4284-125">If you have modified the users in your subscription from what is created in the default content pack, some users may not be added to Teams.</span></span> <span data-ttu-id="f4284-126">当脚本执行时，它将显示成功或失败的操作。</span><span class="sxs-lookup"><span data-stu-id="f4284-126">As the script executes it displays successful or failed actions.</span></span>

5. <span data-ttu-id="f4284-127">脚本执行完毕后，可以使用其中一个用户帐户Teams登录客户端并查看新创建的团队。</span><span class="sxs-lookup"><span data-stu-id="f4284-127">After the script has finished execution, you can sign in to the Teams client with one of the user accounts and view the newly created teams.</span></span>

## <a name="see-also"></a><span data-ttu-id="f4284-128">另请参阅</span><span class="sxs-lookup"><span data-stu-id="f4284-128">See also</span></span>

* [<span data-ttu-id="f4284-129">调试选项卡</span><span class="sxs-lookup"><span data-stu-id="f4284-129">Debug your tab</span></span>](~/tabs/how-to/developer-tools.md) 
* [<span data-ttu-id="f4284-130">调试机器人</span><span class="sxs-lookup"><span data-stu-id="f4284-130">Debug your bots</span></span>](~/bots/how-to/debug/locally-with-an-ide.md)
* [<span data-ttu-id="f4284-131">测试 RSC 权限</span><span class="sxs-lookup"><span data-stu-id="f4284-131">Test RSC permissions</span></span>](~/graph-api/rsc/test-resource-specific-consent.md)
