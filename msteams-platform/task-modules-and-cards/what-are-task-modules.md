---
title: 任务模块
author: surbhigupta
description: 在本模块中，了解如何添加模式弹出体验，以便从Microsoft Teams应用收集或显示用户信息
ms.localizationpriority: medium
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: f5bed6e92200d19fc99f8f91d632dd04d61a1722
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143597"
---
# <a name="task-modules"></a>任务模块

任务模块允许你在 Teams 应用程序中创建模式弹出体验。 在弹出窗口中，可以：

* 运行自己的自定义 HTML 或 JavaScript 代码。
* `<iframe>`显示基于 YouTube 或Microsoft Stream视频等小组件。
* 显示 [自适应卡片](/adaptive-cards/)。

任务模块可用于启动和完成任务或显示丰富的信息，例如视频或 Power Business Intelligence (BI) 仪表板。 与选项卡或基于聊天的机器人体验相比，启动和完成任务的用户通常更自然地使用弹出式体验。

任务模块以Microsoft Teams选项卡为基础构建。 它们本质上是弹出窗口内的选项卡。 它们使用相同的 SDK，因此，如果已生成选项卡，则你已熟悉如何创建任务模块。

可通过 3 种方式调用任务模块：

* 频道或个人选项卡：使用Microsoft Teams选项卡 SDK，可以从选项卡上的按钮、链接或菜单调用任务模块。有关详细信息，请参阅[选项卡中的使用任务模块](~/task-modules-and-cards/task-modules/task-modules-tabs.md)。
* 机器人：在从机器人发送的 [卡](~/task-modules-and-cards/cards/cards-reference.md) 片上使用按钮。 当你不需要频道中的每个人查看你正在对机器人执行的操作时，这非常有用。 例如，让用户在频道中响应投票时，查看正在创建的轮询记录并不有用。 有关详细信息，请参阅[Teams机器人使用任务模块](~/task-modules-and-cards/task-modules/task-modules-bots.md)。
* 在深层链接Teams之外：还可以创建 URL 从任意位置调用任务模块。 有关详细信息，请参阅 [任务模块深度链接语法](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)。

## <a name="components-of-a-task-module"></a>任务模块的组件

下面是从机器人调用任务模块时的外观：

:::image type="content" source="../assets/images/task-module/task-module-example.png" alt-text="任务模块示例":::

任务模块包括以下内容，如上图所示：

1. 应用的 [`color` 图标](~/resources/schema/manifest-schema.md#icons)。
2. 应用的 [`short` 名称](~/resources/schema/manifest-schema.md#name)。
3. [在 TaskInfo 对象](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)的属性中`title`指定的任务模块的标题。
4. 任务模块的关闭或取消按钮。 如果用户选择此按钮，应用将收到一个 `err` 事件。 有关详细信息，请参阅 [提交任务模块结果的示例](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module)。

    > [!NOTE]
    > 当前无法 `err` 检测从机器人调用任务模块时的事件。

5. 如果要使用 `url` [TaskInfo 对象](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)的属性加载自己的网页，则会显示蓝色矩形。 有关详细信息，请参阅[任务模块大小调整](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-sizing)。
6. 如果使用 `card` [TaskInfo 对象](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) 的属性显示自适应卡片，则会为你添加填充。 有关详细信息，请参阅 [HTML 或 JavaScript 任务模块的任务模块 CSS](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-css-for-html-or-javascript-task-modules)。
7. 选择 **“注册**”后，自适应卡片按钮呈现。 使用自己的页面时，请创建自己的按钮。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [调用和关闭任务模块](~/task-modules-and-cards/task-modules/invoking-task-modules.md)

## <a name="see-also"></a>另请参阅

[卡片](~/task-modules-and-cards/what-are-cards.md)
