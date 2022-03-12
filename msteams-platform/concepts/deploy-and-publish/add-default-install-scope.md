---
title: 为应用配置默认安装选项
description: 介绍如何为共享范围指定应用的默认安装选项和默认功能。
ms.topic: how-to
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: a6857e549c688bd7078aeaceae4b9f5a885ae2c3
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453206"
---
# <a name="configure-default-install-options-for-your-microsoft-teams-app"></a>为应用配置默认安装Microsoft Teams选项

应用通常支持 Teams 中的多个方案，但你在设计时可能记住了特定的范围和功能。 例如，如果你的应用主要用于团队或频道使用，你可以确保用户在应用商店中看到的首个安装选项是添加到 **团队**。

:::row:::
   :::column span="2":::

![添加应用下拉列表示例](../../assets/images/compose-extensions/addanapp.png)

   :::column-end:::
   :::column span="2":::
   :::column-end:::
:::row-end:::

如果你的应用的主要功能是自动程序，还可以在用户将应用安装到团队时使机器人成为默认功能。

## <a name="configure-your-apps-default-install-scope"></a>配置应用的默认安装作用域

为应用配置默认安装范围。 一次只能设置一个范围。

若要在应用清单中配置默认安装作用域，请运行以下代码：

1. 打开应用清单并添加 `defaultInstallScope` 属性。
2. 将默认安装范围值设置为 、 `personal`、 `team`、 `groupchat`或 `meetings`。

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> 有关详细信息，请参阅 [应用清单架构](~/resources/schema/manifest-schema.md)。

## <a name="configure-the-default-capability-for-shared-scopes"></a>配置共享范围的默认功能

为团队、会议或群聊安装应用时配置默认功能。

> [!NOTE]
> `defaultGroupCapability` 提供将添加到团队、群聊或会议的默认功能。 选择选项卡、机器人或连接器作为应用的默认功能，但必须确保你在应用定义中提供了所选功能。

在应用清单中配置详细信息：

1. 打开应用清单，并添加 `defaultGroupCapability` 属性。
2. 设置 、 `team`或 `groupchat`的值 `meetings`。
3. 对于选定的组功能，可用的组功能是、 `bot`、 `tab`或 `connector`。

    > [!NOTE]
    > 只能为选定的组功能选择一个默认`bot``tab`功能 、 或 `connector` 。

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
