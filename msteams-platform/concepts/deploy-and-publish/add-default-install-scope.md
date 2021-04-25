---
title: 为应用配置默认安装选项
description: 介绍如何指定应用的默认安装选项。
ms.topic: how-to
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: a4b70df70c7b9442e29953dae8a8c4e892cb72c1
ms.sourcegitcommit: 7b4f383b506d4bc68a1b5641d6e0f404edbfbc6d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2021
ms.locfileid: "51946486"
---
# <a name="add-a-default-install-scope-and-group-capability"></a>添加默认安装范围和组功能

应用通常支持 Teams 中的多个方案，但你在设计时可能记住了特定的范围和功能。 例如，如果你的应用主要用于团队或频道，你可以确保用户在应用商店中看到的第一个安装选项是添加到 **团队**。

![添加应用](../../assets/images/compose-extensions/addanapp.png)

如果你的应用的主要功能是自动程序，则还可以在用户将应用安装到团队时使机器人成为默认功能。 

## <a name="configure-your-apps-default-install-scope"></a>配置应用的默认安装作用域

为应用配置默认安装范围。 一次只能设置一个范围。

**在应用清单中配置默认安装作用域**

1. 打开应用清单并添加 `defaultInstallScope` 属性。
2. 设置 、 `personal` `team` 、 `groupchat` 或 `meetings` 值 (请参阅下面的示例) 。

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> 有关详细信息，请参阅应用 [清单架构](~/resources/schema/manifest-schema.md)。

## <a name="configure-the-default-capability-for-shared-scopes"></a>配置共享范围的默认功能

为团队、会议或聊天安装应用时配置默认功能。

**在应用清单中配置详细信息**

1. 打开应用清单，并添加 `defaultGroupCapability` 属性。
2. 保存更新。

    下面是一个 JSON 示例：

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```
> [!NOTE]
> 有关完整架构的信息，请参阅 [清单架构](~/resources/schema/manifest-schema.md)。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [选择如何发布应用程序](overview.md)
