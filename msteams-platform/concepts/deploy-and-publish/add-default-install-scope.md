---
title: 为应用配置默认安装选项
description: 了解如何为共享范围指定Teams应用的默认安装选项和默认功能。
ms.topic: how-to
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: 9055b765c30f83c4031ad0e2ba5f18f4e747ac3f
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2022
ms.locfileid: "66122899"
---
# <a name="configure-default-install-options-for-your-microsoft-teams-app"></a>为Microsoft Teams应用配置默认安装选项

应用通常支持Teams中的多个方案，但你可能已在设计它时考虑到了特定的范围和功能。 例如，如果应用主要用于团队或频道使用，则可以确保用户在应用商店中看到的第一个安装选项是 **“添加到团队**”。

:::row:::
   :::column span="2":::

![添加应用下拉列表示例](../../assets/images/compose-extensions/addanapp.png)

   :::column-end:::
   :::column span="2":::
   :::column-end:::
:::row-end:::

如果应用的主要功能是机器人，则当用户将应用安装到团队时，还可以使机器人成为默认功能。

## <a name="configure-your-apps-default-install-scope"></a>配置应用的默认安装范围

配置应用的默认安装范围。 一次只能设置一个范围。

若要在应用清单中配置默认安装范围，请执行以下操作：

1. 打开应用清单并添加属性 `defaultInstallScope` 。
2. 将默认安装范围值设置为、或 `personal``groupchat``team``meetings`.

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> 有关详细信息，请参阅 [应用清单架构](~/resources/schema/manifest-schema.md)。

## <a name="configure-the-default-capability-for-shared-scopes"></a>配置共享范围的默认功能

为团队、会议或组聊天安装应用时配置默认功能。

> [!NOTE]
> `defaultGroupCapability` 提供将添加到团队、组聊天或会议的默认功能。 选择选项卡、机器人或连接器作为应用的默认功能，但必须确保已在应用定义中提供所选功能。

若要在应用清单中配置详细信息，请执行以下操作：

1. 打开应用清单并将 `defaultGroupCapability` 属性添加到其中。
2. 设置一个值，`team``groupchat`或 `meetings`。
3. 对于所选的组功能，可用的组功能是，`bot``tab`或 `connector`。

    > [!NOTE]
    > 只能为所选的组功能选择一个默认功能`bot``tab``connector`。

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```

> [!NOTE]
> 有关详细信息，请参阅 [应用清单架构](~/resources/schema/manifest-schema.md)。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [创建应用包](~/concepts/build-and-test/apps-package.md)
