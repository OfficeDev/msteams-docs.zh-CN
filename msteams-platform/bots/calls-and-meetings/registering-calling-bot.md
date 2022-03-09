---
title: 注册 Microsoft Teams 的通话和会议机器人
description: 了解如何为用户注册新的音频/视频呼叫Microsoft Teams、创建新的机器人或添加呼叫功能以及添加图形权限。
ms.topic: conceptual
ms.localizationpriority: medium
keywords: 呼叫机器人音频/视频音频视频媒体
ms.openlocfilehash: c05f0e84dd0b56f9bdb503a73886cfa0cd5024fa
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2022
ms.locfileid: "63398664"
---
# <a name="register-calls-and-meetings-bot-for-microsoft-teams"></a>注册 Microsoft Teams 的通话和会议机器人

参与音频或视频通话和联机会议的机器人是Microsoft Teams自动程序，具有以下用于注册机器人的额外功能：

* 新版应用清单Teams两个附加设置和 `supportsCalling` `supportsVideo`。 这些设置包含在列表的[清单架构中Microsoft Teams](../../resources/schema/manifest-schema.md)。
* [必须为Graph](./registering-calling-bot.md#add-graph-permissions)的 Microsoft 应用 ID 配置 Microsoft 应用权限。
* 会议Graph联机会议 API 权限需要租户管理员同意。

## <a name="new-manifest-settings"></a>新清单设置

呼叫和联机会议自动程序在 manifest.json 中具有以下两个其他设置，这些设置在 Teams 中为机器人启用音频或Teams。

* `bots[0].supportsCalling`. 如果存在并设置为 ，Teams`true`自动程序可以参与通话和联机会议。
* `bots[0].supportsVideo`. 如果存在并设置为 `true`，Teams自动程序支持视频。

如果希望 IDE 正确验证通话和会议机器人的 manifest.json `$schema` 架构是否包含这些值，可以按如下方式更改 属性：

```json
"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
```

下一部分使你能够创建新的机器人或将呼叫功能添加到现有机器人。

## <a name="create-new-bot-or-add-calling-capabilities"></a>创建新的机器人或添加呼叫功能

有关创建自动程序的信息，请参阅[创建自动程序Teams](../how-to/create-a-bot-for-teams.md)。

若要为用户创建新自动程序Teams：

1. 使用此链接可创建新的自动程序 `https://dev.botframework.com/bots/new`。 或者，如果你选择 Bot Framework 门户中的"创建自动程序"按钮，你将在 Microsoft Azure 创建自动程序，你必须拥有 Azure 帐户。
1. 添加Teams通道。
1. 选择"**通话频道**"页面上Teams"选项卡。 选择 **"启用** 呼叫"，然后更新 Webhook (以) 接收传入通知的 HTTPS URL 调用 **Webhook** ，例如 `https://contoso.com/teamsapp/api/calling`。 有关详细信息，请参阅 [配置通道](/bot-framework/portal-configure-channels)。

    ![配置Teams频道信息](~/assets/images/calls-and-meetings/configure-msteams-channel.png)

下一节提供呼叫和联机会议支持的应用程序权限列表。

## <a name="add-graph-permissions"></a>添加Graph权限

应用程序Graph粒度权限来控制应用对资源的访问权限。 你可以决定应用请求Graph的权限。 调用GRAPH API 支持应用程序权限，这些权限由在没有登录用户的情况下运行的应用使用。 租户管理员必须同意应用程序权限。

### <a name="application-permissions-for-calls"></a>调用的应用程序权限

下表提供了用于调用的应用程序权限列表：

|权限    |显示字符串   |说明 |需要管理员同意 |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| Calls.Initiate.All |从应用预览启动传出 1：1 呼叫。 |允许应用在没有登录用户的情况下，向单个用户发起播出通话并将通话转接到组织目录中的用户。|是|
| Calls.InitiateGroupCall.All |从应用预览启动传出组呼叫。 |允许应用在没有登录用户的情况下，向多个用户发起播出通话并向组织中的会议添加参与者。|是|
| Calls.JoinGroupCall.All |以应用预览模式加入群组通话和会议。 |允许应用在没有登录用户的情况下，加入组织中的组通话和计划会议。 应用已使用目录用户的权限加入租户中的会议。|是|
| Calls.JoinGroupCallasGuest.All |以来宾预览模式加入群组通话和会议。 |允许应用在没有登录用户的情况下，以匿名方式加入组织中的组通话和计划会议。 应用作为来宾加入租户中的会议。|是|
| Calls.AccessMedia.All |以应用预览模式访问通话中的媒体流。 |允许应用在没有登录用户的情况下，直接访问通话中的媒体数据流。|是|

> [!IMPORTANT]
> 不能使用媒体访问 API 记录或以其他方式保留来自调用或会议的媒体内容，您的应用程序访问或派生来自该媒体内容记录或录制的数据。 必须先调用 [`updateRecordingStatus` API](/graph/api/call-updaterecordingstatus) 以指示录制已开始，然后从该 API 收到成功回复。 如果应用程序开始录制任何会议 `updateRecordingStatus` 或呼叫，则必须在调用 API 之前结束录制，以指示录制已结束。

### <a name="application-permissions-for-online-meetings"></a>联机会议的应用程序权限

下表提供了联机会议的应用程序权限列表：

|权限    |显示字符串   |说明 |需要管理员同意 |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| OnlineMeetings.Read.All |从应用预览中读取联机会议详细信息|允许应用在没有登录用户的情况下读取组织的联机会议详细信息。|是|
| OnlineMeetings.ReadWrite.All |代表用户从应用预览中读取和创建联机会议|允许应用在没有登录用户的情况下代表用户在你的组织中创建联机会议。|是|

### <a name="assign-permissions"></a>分配权限

如果你想要使用 Microsoft Azure Active Directory (Azure AD) V1 终结点，则必须使用 [Microsoft Azure](https://aka.ms/aadapplist) 门户提前配置[自动程序的应用程序权限](/azure/active-directory/develop/azure-ad-endpoint-comparison)。

### <a name="get-tenant-administrator-consent"></a>获取租户管理员同意

对于使用 Azure AD V1 终结点的应用，当应用安装在其组织中时，租户管理员可以使用 [Microsoft Azure](https://portal.azure.com) 门户同意应用程序权限。 或者，可以在应用中提供注册体验，管理员可通过此体验同意你配置的权限。 管理员同意由管理员记录Azure AD，应用无需再次请求同意即可请求令牌。

你可以依赖管理员在应用程序门户中授予Microsoft Azure[权限](https://portal.azure.com)。 更好的选择是使用 V2 `/adminconsent` 终结点为管理员提供Azure AD体验。 有关详细信息，请参阅 [有关构造管理员同意 URL 的说明](/graph/uth-v2-service#3-get-administrator-consent)。

> [!NOTE]
> 若要构建租户管理员同意 URL，需要应用注册门户中配置的重定向 URI 或回复 URL。[](https://apps.dev.microsoft.com/) 若要为自动程序添加回复 URL，请访问自动程序注册，选择"**高级** > 选项 **""添加应用程序清单"**。 将重定向 URL 添加到集合 `replyUrls` 。

> [!IMPORTANT]
> 无论何时更改应用程序权限，都必须重复管理员同意过程。 在租户管理员重新应用同意之前，不会反映应用注册门户中所做的更改。

## <a name="step-by-step-guide"></a>分步指南

按照 [分步指南在](../../sbs-calling-and-meeting.yml) 机器人中设置通话和会议。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [来电通知](~/bots/calls-and-meetings/call-notifications.md)

## <a name="see-also"></a>另请参阅

* [来电通知](~/bots/calls-and-meetings/call-notifications.md)
* [在本地电脑上开发通话和联机会议机器人](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
