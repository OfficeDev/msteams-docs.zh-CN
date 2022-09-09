---
title: Teams Connect共享通道
author: Rajeshwari-v
description: 了解Teams Connect共享通道，以便在共享空间中安全地与内部和外部用户协作，而无需切换租户。
ms.author: surbhigupta
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: f063be5bce83484a259e67e94f4caa73ef8afa76
ms.sourcegitcommit: bd30d33af59dd870a309ae72b4c4496c9c1f920d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2022
ms.locfileid: "67635313"
---
# <a name="microsoft-teams-connect-shared-channels"></a>Microsoft Teams Connect共享通道

Microsoft Teams Connect共享频道允许频道成员与其他团队和组织中的用户协作。 可以使用以下方式创建和共享共享通道：

* 同一组织中另一个团队的成员。
* 同一组织内的个人。
* 其他组织的个人和其他团队。

Teams Connect共享通道可无缝地促进安全协作。 允许组织外部用户与 Teams 中的内部用户协作，而无需更改其用户上下文。 与使用来宾帐户不同，增强用户体验，例如，成员必须注销 Teams 并使用来宾帐户再次登录。 Teams 应用程序扩展了强大的协作空间。

:::image type="content" source="~/assets/images/app-fundamentals/shared-channels-teams.png" alt-text="显示组织 A 中的 B 团队和组织 B 中的团队 C 的 B 团队在共享频道中作为 A 团队协作的示意图。" border="true" :::

## <a name="enable-your-app-for-shared-channels"></a>为共享通道启用应用

SupportedChannelTypes 是一个可选属性，可在非标准通道中启用应用。 如果应用支持团队范围并定义了属性，Teams 会在每个通道类型中相应地启用应用。 目前支持专用频道和共享频道。 有关详细信息，请参阅 [supportedChannelTypes](../../resources/schema/manifest-schema.md#supportedchanneltypes)。

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
> * 如果应用支持团队范围，它将在标准通道中运行，而不考虑在此属性中定义了哪些值。
> * 应用可能需要考虑这些通道类型的唯一属性才能正常运行。

## <a name="get-context-for-shared-channels"></a>获取共享通道的上下文

在共享通道中加载内容 UX 时，使用从 `getContext` 调用收到的数据进行共享通道更改。 `getContext` 调用会发布两个新属性， `hostTeamGroupID` 用于 `hostTenantID`使用 Microsoft Graph API 检索频道成员身份。 `hostTeam` 是创建共享通道的团队。

有关启用选项卡的详细信息，请参阅：

* [获取专用频道选项卡的上下文](../../tabs/how-to/access-teams-context.md#retrieve-context-in-private-channels)
* [获取共享通道中的上下文](../../tabs/how-to/access-teams-context.md#get-context-in-shared-channels)

## <a name="apps-and-permissions-in-shared-channels"></a>共享通道中的应用和权限

可以使用共享渠道与组织外部的外部成员进行协作。 共享频道中的应用权限遵循主机团队的应用名册和主机租户的应用策略。

> [!NOTE]
> [活动源通知 API](/graph/teams-send-activityfeednotifications) 不支持共享通道中应用的跨租户通知。

## <a name="get-shared-channel-membership"></a>获取共享频道成员身份

可以使用 `hostTeamGroupID` 来自 `getContext` 和以下步骤获得直接共享频道成员身份：

1. 使用 [GET 通道成员 API API](/graph/api/channel-list-members?view=graph-rest-beta&tabs=http&preserve-view=true) 获取直接成员。

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/members
    ```

2. 使用 GET `sharedWithTeams` API 获取每个共享团队。

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/sharedWithTeams
    ```

3. 将每个共享团队 (X 团队) 的 GET 成员与 GET `sharedWithTeams` API 配合使用。

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/sharedWithTeams/{teamX}/members
    ```

## <a name="classify-members-in-the-shared-channel-as-in-tenant-or-out-tenant"></a>将共享通道中的成员分类为租户内或租户外

可以通过比较 `tenantID` 成员或团队 `hostTeamTenantID` ，将成员分类为租户内或租户外成员，如下所示：

1. 获取要比较的成员。

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/members
    ```

2. 使用`getContext`，将成员`hostTenantID`与属性进行比较`tenantID`。

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
* [Teams 位置的保留策略](/microsoft-365/compliance/create-retention-policies)
