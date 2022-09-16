---
title: 基于搜索的消息扩展的通用操作
author: v-ypalikila
description: 本文介绍基于搜索的消息扩展插件中的通用操作和自适应卡片的自动刷新。
ms.topic: conceptual
ms.author: v-ypalikila
ms.localizationpriority: medium
ms.openlocfilehash: b8515ca2a84d3c29ddfb384fde5038a68d953c33
ms.sourcegitcommit: 19f3e4e9088d0a07c9b567e76640d498b9d1981f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/16/2022
ms.locfileid: "67787193"
---
# <a name="universal-actions-for-search-based-message-extensions"></a>基于搜索的消息扩展的通用操作

基于搜索的消息扩展插件中的自适应卡片现在支持通用操作。 若要为基于搜索的消息扩展启用通用操作，应用必须符合适用于 [自适应卡片的通用操作的架构](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Work-with-Universal-Actions-for-Adaptive-Cards.md#schema-for-universal-actions-for-adaptive-cards) 以及以下要求：

1. 应用必须在应用清单中定义聊天机器人。
1. 如果已有对话机器人，则必须使用消息扩展插件中使用的同一机器人。
1. 如果卡片是在组中发送的，则应用必须在清单中的机器人上指定 `team` 或 `groupchat` 作用域。

包含 `team` 和 `groupchat` 值的 JSON 架构示例：

```json
{
    "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
    "manifestVersion": "1.11",
    "version": "1.0.0",
    "id": "%MICROSOFT-APP-ID%",
    "packageName": "com.example.myapp",
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

## <a name="automatic-refresh-for-adaptive-cards-in-search-based-message-extensions"></a>基于搜索的消息扩展插件中自适应卡片的自动刷新

在基于搜索的消息扩展插件中为自适应卡片启用自动刷新，以确保用户始终看到最新信息。 若要启用，请在属性中`29:<ID>``refresh`以或`8:orgid:<AAD ID>`格式定义`userIds`数组。 有关详细信息，请参阅 [使用适用于自适应卡片的通用操作](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Work-with-Universal-Actions-for-Adaptive-Cards.md#user-ids-in-refresh)。

`userIds`属性中的数组示`refresh`例：

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
> 对于组聊天或频道中用户少 *于或等于* 60 个用户的所有用户启用自动刷新。 对于 (群聊或频道) 超过 60 个用户的对话，用户可以使用消息选项菜单中的刷新按钮来获取最新结果。

`Action.Execute`属性中的`refresh`示例：

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

实时 (JIT) 允许你在群组聊天或频道中为多个用户安装卡片或消息扩展。 为了支持基于搜索的消息扩展插件中的通用操作，机器人会添加到对话中，用户会在对话中 (包含 `Action.Execute`) 的卡片。

当用户选择卡片并在群聊或频道中发送时，会显示 **JIT** 安装提示。 用户选择 **发送** 选项后，会为后台聊天或频道中的所有用户添加应用。

> [!NOTE]
> 对于未 `Action.Execute` 定义和 `refresh` 架构的应用，安装提示不会向用户显示。

动态 ME 和 JIT 安装用户流的示例：

  :::image type="content" source="../../../assets/videos/dynamic-me-jit-flow.gif" alt-text="GIF 显示动态消息扩展和 JIT 安装的用户流。":::

## <a name="see-also"></a>另请参阅

* [消息扩展](../../what-are-messaging-extensions.md)
* [自适应卡的通用操作](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Overview.md)
