---
title: Teams Connect共享频道
author: Rajeshwari-v
description: 了解Teams Connect共享频道，无需切换租户即可在共享空间中安全地与内部和外部用户进行协作。
ms.author: surbhigupta
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: d1f2d212c33f80ce6a5d27e93bda0551d26542dd
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789924"
---
# <a name="microsoft-teams-connect-shared-channels"></a>Microsoft Teams Connect共享频道

Microsoft Teams Connect共享频道允许频道成员与其他团队和组织中的用户协作。 可以使用以下项创建和共享共享频道：

* 同一组织内另一个团队的成员。
* 同一组织中的个人。
* 个人和其他组织的其他团队。

Teams Connect共享通道有助于无缝进行安全协作。 允许组织外部的外部用户与 Teams 中的内部用户协作，而无需更改其用户上下文。 与使用来宾帐户不同，增强用户体验，例如，成员必须注销 Teams 并使用来宾帐户再次登录。 Teams 应用程序扩展了强大的协作空间。

:::image type="content" source="~/assets/images/app-fundamentals/shared-channels-teams.png" alt-text="显示组织 A 中的团队 B 和组织 B 的团队 C 作为团队 A 在共享频道中协作的示意图。" border="true" :::

## <a name="enable-your-app-for-shared-channels"></a>为共享频道启用应用

SupportedChannelTypes 是一个可选属性，可在非标准通道中启用应用。 如果你的应用支持团队范围并且定义了 属性，则 Teams 会相应地在每个频道类型中启用你的应用。 当前支持专用频道和共享频道。 有关详细信息，请参阅 [supportedChannelTypes](../../resources/schema/manifest-schema.md#supportedchanneltypes)。

```JSON
"supportedChannelTypes": {
      "type": "array",
      "description": "List of ‘non-standard’ channel types that the app supports. Note: Channels of standard type are supported by default if the app supports team scope. ",
      "maxItems": 2,
      "items": { 
        "enum": [
          "sharedChannels",
          "privateChannels"
        ]
      }
    }
```

> [!NOTE]
>
> * 如果你的应用支持团队范围，则无论此属性中定义了哪些值，它都在标准通道中运行。
> * 你的应用可能需要考虑每个通道类型的唯一属性才能正常工作。

## <a name="get-context-for-shared-channels"></a>获取共享频道的上下文

在共享通道中加载内容 UX 时，使用从 `getContext` 调用收到的数据来更改共享通道。 `getContext` 调用发布两个新属性 `hostTeamGroupID` 和 `hostTenantID`，用于使用 Microsoft Graph API 检索通道成员身份。 `hostTeam` 是创建共享频道的团队。

有关启用选项卡的详细信息，请参阅：

* [获取专用频道的选项卡的上下文](../../tabs/how-to/access-teams-context.md#retrieve-context-in-private-channels)
* [获取共享频道中的上下文](../../tabs/how-to/access-teams-context.md#get-context-in-shared-channels)

## <a name="apps-and-permissions-in-shared-channels"></a>共享频道中的应用和权限

可以使用共享频道与组织外部成员协作。 共享频道中的应用权限遵循主机团队的应用名单和主机租户的应用策略。

> [!NOTE]
> [活动源通知 API](/graph/teams-send-activityfeednotifications) 不支持共享通道中的应用的跨租户通知。

## <a name="get-shared-channel-membership"></a>获取共享频道成员身份

可以使用 中的 `getContext` 并按照以下步骤获取直接共享频道成员身份`hostTeamGroupID`：

1. 使用 [GET 通道成员 API](/graph/api/channel-list-members?view=graph-rest-beta&tabs=http&preserve-view=true) 获取直接成员。

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/members
    ```

2. 使用 GET `sharedWithTeams` API 获取每个共享团队。

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/sharedWithTeams
    ```

3. 将每个共享团队的 GET 成员 (X) 与 GET `sharedWithTeams` API 配合使用。

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/sharedWithTeams/{teamX}/members
    ```

## <a name="classify-members-in-the-shared-channel-as-in-tenant-or-out-tenant"></a>将共享频道中的成员分类为租户内或租户外

可以通过对 `tenantID` 成员或团队 `hostTeamTenantID` 进行比较，将成员分类为租户内或租户外成员，如下所示：

1. 获取要比较的成员。

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/members
    ```

2. 使用 `getContext`，将 成员的 与 `hostTenantID` 属性进行比较`tenantID`。

## <a name="azure-ad-native-identity"></a>Azure AD 本机标识

应用必须在安装和使用中跨租户运行。 下表列出了通道类型及其相应的组 ID：

|通道类型| groupId | hostTeamGroupId |
|----------|---------|-----------------|
|Regular | 团队 Azure AD 组 ID | 团队 Azure AD 组 ID |
|共享的内容 | Empty | 主机团队 Azure AD 组 ID |

## <a name="see-also"></a>另请参阅

* [Teams 的生成选项卡](../../tabs/what-are-tabs.md)
* [Teams 的应用清单架构](../../resources/schema/manifest-schema.md)
* [Microsoft Teams 中的共享频道](/MicrosoftTeams/shared-channels)
* [通道资源类型](/graph/api/resources/channel)
* [Teams 位置的保留策略](/microsoft-365/compliance/create-retention-policies)
