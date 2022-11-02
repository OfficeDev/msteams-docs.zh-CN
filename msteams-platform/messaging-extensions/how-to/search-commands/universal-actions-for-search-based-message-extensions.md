---
title: 基于搜索的消息扩展的通用操作
author: v-ypalikila
description: 在本文中，了解基于搜索的消息扩展中的自适应卡片的通用操作和自动刷新。
ms.topic: conceptual
ms.author: v-ypalikila
ms.localizationpriority: medium
ms.openlocfilehash: 18f5b783797d69144aac82e5ebd95fc30dad57a2
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2022
ms.locfileid: "68819966"
---
# <a name="universal-actions-for-search-based-message-extensions"></a>基于搜索的消息扩展的通用操作

基于搜索的消息扩展中的自适应卡片现在支持通用操作。 若要为基于搜索的消息扩展启用通用操作，应用必须符合 [自适应卡片通用操作的架构](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Work-with-Universal-Actions-for-Adaptive-Cards.md#schema-for-universal-actions-for-adaptive-cards) 以及以下要求：

1. 应用必须在应用清单中定义聊天机器人。
1. 如果已有对话机器人，则必须使用消息扩展中使用的同一机器人。
1. 如果卡片以组形式发送，则应用必须在清单中指定 `team` 或 `groupchat` 限定其机器人的范围。

包含 `team` 和 `groupchat` 值的 JSON 架构示例：

```json
{
    "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
    "manifestVersion": "1.11",
    "version": "1.0.0",
    "id": "%MICROSOFT-APP-ID%",
    "bots": [
        {
            "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
            "scopes": [
                    "team",
                    "personal",
                    "groupchat"
                ]
        }
    ],
    "composeExtensions": [
        {
            "canUpdateConfiguration": true,
            "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%", // Use the same bot as what is specified in the bots section above
        }
    ]
}
```

## <a name="automatic-refresh-for-adaptive-cards-in-search-based-message-extensions"></a>在基于搜索的消息扩展中自动刷新自适应卡片

在基于搜索的消息扩展中为自适应卡片启用自动刷新，以确保用户始终看到最新信息。 若要启用，请在 属性中`29:<ID>`以 或 `8:orgid:<AAD ID>` 格式`refresh`定义`userIds`数组。 有关详细信息，请参阅 [使用自适应卡片的通用操作](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Work-with-Universal-Actions-for-Adaptive-Cards.md#user-ids-in-refresh)。

`userIds`属性中的`refresh`数组示例：

```json
    {
        "type": "AdaptiveCard",
        "refresh": {
            "userIds": [
                "8:orgid:<AADID>",
                "29:<id>"
            ],
            "action": {
                "type": "Action.Execute",
                "data": {}
            }
        },
        "body": [
            {
                "type": "TextBlock",
                "text": "Hello World!",
                "wrap": true
            }
        ],
        "actions": [
            {
                "type": "Action.Execute",
                "data": {},
                "title": "Hello"
            }
        ]
    }
```

> [!NOTE]
> 对于群聊或频道中用户 *少于或等于* 60 的所有用户，将启用自动刷新。 对于与 60 个以上的用户 (群组聊天或频道) 的对话，用户可以使用消息选项菜单中的“刷新”按钮获取最新结果。

`Action.Execute`属性中的 `refresh` 示例：

```json
    {
        "type": "AdaptiveCard",
        "refresh": {
            "action": {
                "type": "Action.Execute",
                "data": {}
            }
        },
        "body": [
            {
                "type": "TextBlock",
                "text": "Hello World!",
                "wrap": true
            }
        ],
        "actions": [
            {
                "type": "Action.Execute",
                "data": {},
                "title": "Hello"
            }
        ]
    }
```

## <a name="just-in-time-install"></a>实时安装

实时 (JIT) 允许在群组聊天或频道中为多个用户安装卡片或消息扩展。 为了在基于搜索的消息扩展中支持通用操作，机器人将添加到聊天中，其中卡 (由 `Action.Execute` 用户发送) 。

当用户选择卡片并在群组聊天或频道中发送该卡时，将显示 **JIT** 安装提示。 用户选择 **发送** 选项后，将在后台为聊天或频道中的所有用户添加应用。

> [!NOTE]
> 对于未 `Action.Execute` 定义 和 `refresh` 架构的应用，不会向用户显示安装提示。

动态 ME 和 JIT 安装用户流的示例：

  :::image type="content" source="../../../assets/videos/dynamic-me-jit-flow.gif" alt-text="GIF 显示动态消息扩展和 JIT 安装的用户流。":::

## <a name="see-also"></a>另请参阅

* [消息扩展](../../what-are-messaging-extensions.md)
* [自适应卡](../../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [自适应卡的通用操作](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Overview.md)
