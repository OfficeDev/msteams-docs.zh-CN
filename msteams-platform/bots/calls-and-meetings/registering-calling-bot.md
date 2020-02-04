---
title: 为 Microsoft 团队注册呼叫和会议机器人
description: 了解如何为 Microsoft 团队注册新的音频/视频呼叫机器人
keywords: 呼叫机器人音频/视频音频视频媒体
ms.openlocfilehash: 9a246c9b1a5aae230881b468afef6c205d5bdecf
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673408"
---
# <a name="registering-a-calling-bot-for-microsoft-teams"></a>为 Microsoft 团队注册呼叫机器人

参与音频/视频呼叫和联机会议的 bot 是一个普通的 Microsoft 团队 bot，其中包含几个额外的功能：

* 有一个新版本的团队应用程序清单，其中有两个附加`supportsCalling`设置`supportsVideo`，和。 这些设置包括在 Microsoft 团队应用程序清单的[开发人员预览](../../resources/dev-preview/developer-preview-intro.md)版本中。
* 必须为你的 bot 的 Microsoft 应用 ID 配置[Microsoft Graph 权限](./registering-calling-bot.md#add-microsoft-graph-permissions)。
* Microsoft Graph 呼叫和联机会议 Api 权限需要租户管理员同意。

让我们更详细地讨论上面的内容。

## <a name="new-manifest-settings"></a>新清单设置

呼叫和联机会议 bot 在 manifest 中有两个附加设置，可在团队中为你的 bot 启用音频/视频。

* `bots[0].supportsCalling`. 如果存在并设置为`true`，则团队将允许你的 bot 参与呼叫和联机会议。
* `bots[0].supportsVideo`. 如果存在并设置为`true`，则团队会意识到你的 bot 支持视频。

如果您希望 IDE 正确验证这些值的通话和会议 bot 的清单 json 架构，可以更改`$schema`属性，如下所示：

```json
"$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
```

## <a name="creating-a-new-bot-or-adding-calling-capabilities-to-an-existing-bot"></a>创建新的 bot 或向现有 bot 添加呼叫功能

在 "[创建 Microsoft 团队的 bot](../how-to/create-a-bot-for-teams.md) " 主题中将更详细地介绍了如何创建新的 bot，但我们将在此处重复执行以下操作：

1. 使用此链接可创建新的 bot： `https://dev.botframework.com/bots/new`。 如果改为在 Bot 框架门户中选择 "*创建机器人*" 按钮，则会在 Microsoft Azure 中创建你需要 Azure 帐户的你的 bot。
1. 添加 Microsoft 团队频道。 单击 "Microsoft 团队频道" 页面上的 "通话" 选项卡，选择 "**启用呼叫**"，然后使用你的 HTTPS URL 更新**Webhook （用于呼叫）** ，你将收到传入通知`https://contoso.com/teamsapp/api/calling`（例如，）。 有关如何配置频道的详细信息，请参阅[配置频道](/bot-framework/portal-configure-channels)。
  ![配置 Microsoft 团队频道信息](~/assets/images/calls-and-meetings/configure-msteams-channel.png)

## <a name="add-microsoft-graph-permissions"></a>添加 Microsoft Graph 权限

Microsoft Graph 公开了控制应用程序对资源的访问权限的精细权限。 作为开发人员，你可以决定应用请求哪些 Microsoft Graph 权限。  Microsoft Graph 调用 Api 支持_应用程序权限_，这些权限由在没有登录用户的情况下运行的应用程序使用。  租户管理员必须授予应用程序权限许可。 以下是这些权限的列表：

### <a name="application-permissions-calls"></a>应用程序权限：调用

|权限    |显示字符串   |说明 |需经过管理员同意 |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
|_Calls.Initiate.All_|从应用发起一对一拨出通话（预览版）|允许应用在没有登录用户的情况下，向单个用户发起播出通话并将通话转接到组织目录中的用户。|是|
|_Calls.InitiateGroupCall.All_|从应用发起组拨出通话（预览版）|允许应用在没有登录用户的情况下，向多个用户发起播出通话并向组织中的会议添加参与者。|是|
|_Calls.JoinGroupCall.All_|作为应用加入组通话和会议（预览版）|允许应用在没有登录用户的情况下，加入组织中的组通话和计划会议。 应用将加入到租户的会议中并获得目录用户特权。|是|
|_Calls.JoinGroupCallasGuest.All_|作为来宾加入组通话和会议（预览版）|允许应用在没有登录用户的情况下，以匿名方式加入组织中的组通话和计划会议。 应用将作为来宾加入租户的会议。|是|
|_AccessMedia。_ <sup>_请参阅下面_的</sup>|作为应用访问通话中的媒体数据流（预览版）|允许应用在没有登录用户的情况下，直接访问通话中的媒体数据流。|是|

> [!IMPORTANT]
> 您**不能**使用 Microsoft. Media API 来记录或以其他方式保留你的 bot 访问的呼叫或会议中的媒体内容。

### <a name="application-permissions-online-meetings"></a>应用程序权限：联机会议

|权限    |显示字符串   |说明 |需经过管理员同意 |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
|_OnlineMeetings.Read.All_|从应用阅读联机会议详细信息（预览版）|允许应用在没有登录用户的情况下读取组织中的联机会议详细信息。|是|
|_OnlineMeetings.ReadWrite.All_|代表用户从应用读取和创建联机会议（预览版）|允许应用在没有登录用户的情况下代表用户创建组织中的联机会议。|是|

### <a name="assigning-permissions"></a>分配权限

你必须提前为你的 bot 配置应用程序权限。 我们建议使用[Microsoft 应用注册门户](https://apps.dev.microsoft.com/) [，如下所述，](/graph/docs/concepts/auth_register_app_v2)因为它是配置机器人的地方;但是，如果您更喜欢使用[AZURE AD V1 终结点](/azure/active-directory/develop/azure-ad-endpoint-comparison)，仍可以使用[azure 门户](https://aka.ms/aadapplist)。

### <a name="getting-tenant-administrator-consent"></a>获取租户管理员同意

对于使用 Azure AD V1 终结点的应用程序，租户管理员可以在其组织中安装应用程序时同意使用[Azure 门户](https://portal.azure.com)的应用程序权限，也可以在您的应用程序中提供注册权限，管理员可通过该体验来同意您配置的权限。 在 Azure AD 中记录管理员同意后，您的应用程序可以请求令牌，而无需再次请求许可。

你可以依靠管理员授予你的应用程序在[Azure 门户](https://portal.azure.com)上所需的权限;不过，通常情况下，更好的选择是使用 Azure AD V2 `/adminconsent`终结点为管理员提供注册体验。  有关详细信息，请参阅[构建管理员同意 URL 的说明](https://developer.microsoft.com/graph/docs/concepts/auth_v2_service#3-get-administrator-consent)。

> [!NOTE]
> 构造租户管理员同意 URL 需要在[应用注册门户](https://apps.dev.microsoft.com/)中配置的重定向 URI/回复 url。 若要为你的 bot 添加回复 Url，请访问你的 bot 注册，选择 "高级选项-> 编辑应用程序清单"。  将重定向 URL 添加到`replyUrls`集合中。

> [!IMPORTANT]
> 无论何时对应用程序的权限进行更改，还必须重复管理员同意过程。 租户管理员重新应用同意之后，才会反映应用注册门户中所做的更改。
