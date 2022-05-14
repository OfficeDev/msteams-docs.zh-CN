---
title: 注册 Microsoft Teams 的通话和会议机器人
description: 了解如何为 Microsoft Teams 注册新的音频/视频通话机器人、创建新机器人或添加通话功能以及添加图形权限。
ms.topic: conceptual
ms.localizationpriority: medium
keywords: 通话机器人音频/视频音频视频媒体
ms.openlocfilehash: 71ab66ab6c5f53405897447b8d531ed0ce6dac99
ms.sourcegitcommit: 430bf416bb8d1b74f926c8b5d5ffd3dbb0782286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2022
ms.locfileid: "65297161"
---
# <a name="register-calls-and-meetings-bot-for-microsoft-teams"></a>注册 Microsoft Teams 的通话和会议机器人

参与音频或视频通话和联机会议的机器人是常规 Microsoft Teams 机器人，具有以下用于注册机器人的额外功能：

* 有一个新版本的 Teams 应用清单与两个额外的设置：`supportsCalling` 和 `supportsVideo`。 这些设置包含在 [Microsoft Teams 的清单架构](../../resources/schema/manifest-schema.md)中。
* 必须为机器人的 Microsoft 应用 ID 配置 [Microsoft Graph 权限](./registering-calling-bot.md#add-graph-permissions)。
* Graph 通话和联机会议 API 权限需要租户管理员同意。

## <a name="new-manifest-settings"></a>新的清单设置

通话和联机会议机器人在 manifest.json 中具有以下两个附加设置，用于在 Teams 中为机器人启用音频或视频。

* `bots[0].supportsCalling`。如果存在且设置为 `true`，则 Teams 允许机器人参与通话和联机会议。
* `bots[0].supportsVideo`。如果存在且设置为 `true`，则 Teams 知道机器人支持视频。

如果希望 IDE 针对这些值正确验证通话和会议机器人的 manifest.json 架构，则可以更改 `$schema` 属性，如下所示：

```json
"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
```

下一部分使你能够创建新的机器人或将通话功能添加到现有机器人。

## <a name="create-new-bot-or-add-calling-capabilities"></a>创建新机器人或添加通话功能

有关创建机器人的信息，请参阅[为 Teams 创建机器人](../how-to/create-a-bot-for-teams.md)。

若要为 Teams 创建新机器人，请执行以下操作：

1. 使用此链接创建新机器人，`https://dev.botframework.com/bots/new`。或者，如果在 Bot Framework 门户中选择“**创建机器人**”按钮，则在 Microsoft Azure 中创建机器人，必须为其创建 Azure 帐户。
1. 添加 Teams 频道。
1. 选择 Teams 频道页面上的“**通话**”选项卡。 选择“**启用通话**”，然后使用接收传入通知的 HTTPS URL 更新 **Webhook（用于通话）**，例如 `https://contoso.com/teamsapp/api/calling`。 有关详细信息，请参阅[配置频道](/bot-framework/portal-configure-channels)。

    ![配置 Teams 频道信息](~/assets/images/calls-and-meetings/configure-msteams-channel.png)

下一部分提供通话和联机会议支持的应用程序权限列表。

## <a name="add-graph-permissions"></a>添加 Graph 权限

Graph 提供精细的权限来控制应用对资源的访问权限。 你可以决定应用请求哪些 Graph 权限。 Graph 调用 API 支持应用程序权限，这些权限由在没有已登录用户的情况下运行的应用使用。 租户管理员必须授予对应用程序权限的许可。

### <a name="application-permissions-for-calls"></a>通话的应用程序权限

下表提供了通话的应用程序权限列表：

|权限    |显示字符串   |说明 |需经过管理员同意 |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| Calls.Initiate.All |从应用发起一对一拨出通话（预览版）。 |允许应用在没有登录用户的情况下，向单个用户发起播出通话并将通话转接到组织目录中的用户。|是|
| Calls.InitiateGroupCall.All |从应用发起组拨出通话（预览版）。 |允许应用在没有登录用户的情况下，向多个用户发起播出通话并向组织中的会议添加参与者。|是|
| Calls.JoinGroupCall.All |作为应用加入组通话和会议（预览版）。 |允许应用在没有登录用户的情况下，加入组织中的组通话和计划会议。 应用加入到租户的会议中并获得目录用户特权。|是|
| Calls.JoinGroupCallasGuest.All |作为来宾加入组通话和会议（预览版）。 |允许应用在没有登录用户的情况下，以匿名方式加入组织中的组通话和计划会议。 应用作为来宾加入租户的会议。|是|
| Calls.AccessMedia.All |作为应用访问通话中的媒体数据流（预览版）。 |允许应用在没有登录用户的情况下，直接访问通话中的媒体数据流。|是|

> [!IMPORTANT]
> 不得使用媒体访问 API 进行记录，否则保留来自应用程序访问的通话或会议的媒体内容，或派生自该媒体内容或录制文件的数据。 必须先调用 [`updateRecordingStatus` API](/graph/api/call-updaterecordingstatus) 以指示录制已开始，并从该 API 收到成功回复。 如果应用程序开始录制任何会议或通话，则必须先结束录制，然后再调用 `updateRecordingStatus` API 以指示录制已结束。

### <a name="application-permissions-for-online-meetings"></a>联机会议的应用程序权限

下表提供了联机会议的应用程序权限列表：

|权限    |显示字符串   |说明 |需经过管理员同意 |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| OnlineMeetings.Read.All |从应用阅读联机会议详细信息（预览版）|允许应用在没有登录用户的情况下读取组织中的联机会议详细信息。|是|
| OnlineMeetings.ReadWrite.All |代表用户从应用读取和创建联机会议（预览版）|允许应用在没有登录用户的情况下代表用户创建组织中的联机会议。|是|

### <a name="assign-permissions"></a>分配权限

如果想要使用 [Microsoft Azure Active Directory (Azure AD) V1 端点](/azure/active-directory/develop/azure-ad-endpoint-comparison)，则必须使用 [Microsoft Azure 门户](https://portal.azure.com)提前配置机器人的应用程序权限。

### <a name="get-tenant-administrator-consent"></a>获取租户管理员同意

对于使用 Azure AD V1 端点的应用，当应用安装在其组织中时，租户管理员可以使用 [Microsoft Azure 门户](https://portal.azure.com)许可应用程序权限。或者，你可以在应用中提供注册体验，管理员可以通过该体验同意你配置的权限。Azure AD 记录下管理员许可后，应用无需再次请求许可即可请求令牌。

你可让管理员在 [Microsoft Azure 门户](https://portal.azure.com)授予你的应用所需的权限；但更好的方法是通过使用 Azure AD V2 `/adminconsent` 端点为管理员提供注册体验。有关详细信息，请参阅[构造管理员同意 URL 的说明](/graph/auth-v2-service#3-get-administrator-consent)。

> [!NOTE]
> 若要构造租户管理员同意 URL，需要在[应用注册门户](https://apps.dev.microsoft.com/)中配置重定向 URI 或回复 URL。 若要为机器人添加回复 URL，请访问机器人注册，选择“**高级选项**” > “**编辑应用程序清单**”。 将重定向 URL 添加到 `replyUrls` 集合。

> [!IMPORTANT]
> 任何时候更改应用程序的权限都必须重复管理员同意过程。 租户管理员重新应用同意之后，才会反映应用注册门户中所做的更改。

## <a name="code-sample"></a>代码示例

| **示例名称** | **说明** | **Graph** |
|---------------|----------|--------|
| 通话和会议机器人 | 示例应用演示了机器人如何创建通话、加入会议和转移通话。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-calling-meeting/csharp) |

## <a name="step-by-step-guide"></a>分步指南

按照[分步指南](../../sbs-calling-and-meeting.yml)在机器人中设置通话和会议。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [来电通知](~/bots/calls-and-meetings/call-notifications.md)

## <a name="see-also"></a>另请参阅

* [来电通知](~/bots/calls-and-meetings/call-notifications.md)
* [在本地电脑上开发通话和联机会议机器人](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
* [查看应用权限并授予管理员许可](/MicrosoftTeams/app-permissions-admin-center)
