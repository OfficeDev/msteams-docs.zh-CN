---
title: 将测试数据添加到 Microsoft 365 测试租户
description: 设置 Office 365 开发人员计划订阅以成功测试 Microsoft Teams 应用
ms.topic: how-to
keywords: 测试应用开发人员计划团队
ms.date: 11/01/2019
ms.openlocfilehash: 863f1d9843bb3ebe968ca180ee70a5b6bfa6cd7a
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596187"
---
# <a name="add-test-data-to-your-microsoft-365-test-tenant"></a>将测试数据添加到 Microsoft 365 测试租户

通过 Microsoft 365 开发人员订阅，可以将 Microsoft Teams 应用与测试团队、渠道和用户一同使用。

## <a name="before-you-start"></a>准备工作

如果还没有测试租户，则需要加入 Office 365 开发人员计划并注册开发人员订阅。 你还需要安装必要的 PowerShell 模块。 对于你使用的任何租户，你都需要具有运行脚本的全局管理员权限。

1. [加入 Microsoft 365 开发人员计划团队](/office/developer-program/office-365-developer-program)
2. [设置 Microsoft 365 开发人员订阅](/office/developer-program/office-365-developer-program-get-started)
3. [将示例数据包与 Microsoft 365 开发人员订阅一起用于安装 Users 内容包](/office/developer-program/install-sample-packs)
4. [安装 Teams PowerShell 模块](https://www.powershellgallery.com/packages/MicrosoftTeams/1.0.2)
5. [安装 Azure AD PowerShell 模块](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0#installing-the-azure-ad-module&preserve-view=true)

## <a name="optional-enable-custom-app-sideloading"></a> (可选) 启用自定义应用旁加载

默认情况下，只有全局管理员或 Teams 服务管理员可以将自定义应用上传到租户应用目录。 还可以允许用户将自定义应用上载到 Teams。 有关详细信息，请参阅 [在 Teams 中管理应用设置策略](/microsoftteams/teams-app-setup-policies)。

## <a name="create-teams-and-channels"></a>创建团队和频道

将以下代码段另存为 XML (.xml) 并记下保存位置。  此 XML 定义将创建的团队和频道的结构及其成员。

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

将以下代码段另存为 PowerShell 脚本 (.ps1) 并记下保存位置。  此脚本执行创建团队和频道并添加成员的步骤。

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

在管理员Windows PowerShell打开一个会话会话。  运行刚保存的脚本。  系统将提示你提供凭据 - 使用首次注册开发人员订阅时收到的全局管理员凭据。

> [!Note]
> 脚本需要几分钟才能执行 - 请勿关闭 PowerShell 会话。  如果修改了订阅中的用户，但从默认内容包中创建的内容进行了修改，则某些用户可能不会添加到团队中。  当脚本执行时，它将输出成功或失败的操作。

脚本执行完成后，可以使用其中一个用户帐户登录到 Teams 客户端并查看新创建的团队。
