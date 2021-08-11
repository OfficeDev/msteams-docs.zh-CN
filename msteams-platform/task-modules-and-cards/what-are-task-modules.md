---
title: 任务模块
author: surbhigupta
description: 添加模式弹出窗口体验，以从你的应用收集信息或向用户Microsoft Teams信息
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 3b0e639acc8901a3637189e435fcfc159e992ae3a674a437733474087103193c
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2021
ms.locfileid: "57707680"
---
# <a name="task-modules"></a>任务模块

任务模块允许在任务应用程序中创建模式弹出Teams体验。 在弹出窗口中，您可以：

* 运行你自己的自定义 HTML 或 JavaScript 代码。
* 显示 `<iframe>` 基于小部件（如 YouTube 或 Microsoft Stream 视频）。
* 显示 [自适应卡片](/adaptive-cards/)。

任务模块可用于启动和完成任务或显示丰富的信息，例如视频或 POWER Business Intelligence (BI) 仪表板。 与选项卡或基于对话的机器人体验相比，用户启动和完成任务通常更自然。

任务模块基于选项卡Microsoft Teams构建。 它们实质上是弹出窗口中的一个选项卡。 它们使用相同的 SDK，因此如果你已生成了一个选项卡，则你已经熟悉如何创建任务模块。

可通过 3 种方式调用任务模块：

* 频道或个人选项卡：使用 Microsoft Teams 选项卡 SDK，可以从选项卡上的按钮、链接或菜单调用任务模块。有关详细信息，请参阅在[选项卡中使用任务模块](~/task-modules-and-cards/task-modules/task-modules-tabs.md)。
* 自动程序：使用从自动程序 [发送](~/task-modules-and-cards/cards/cards-reference.md) 的卡片上的按钮。 当你不要求频道中的每个人都查看你使用机器人执行什么操作时，这非常有用。 例如，当用户在频道中回复投票时，查看所创建的轮询记录将没有用。 有关详细信息，请参阅使用[自动程序中Teams模块](~/task-modules-and-cards/task-modules/task-modules-bots.md)。
* 在Teams链接之外：还可以创建 URL 以从任何位置调用任务模块。 有关详细信息，请参阅任务 [模块深度链接语法](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)。

## <a name="components-of-a-task-module"></a>任务模块的组件

下面是从自动程序调用任务模块时的外观：

![任务模块示例](~/assets/images/task-module/task-module-example.png)

任务模块包括以下内容，如上图所示：

1. 应用的[ `color` 图标](~/resources/schema/manifest-schema.md#icons)。
2. 应用[ `short` 的名称](~/resources/schema/manifest-schema.md#name)。
3. 任务模块的标题在 `title` [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)对象的 属性中指定。
4. 任务模块的关闭或取消按钮。 如果用户选择此按钮，你的应用将收到 `err` 事件。 有关详细信息，请参阅 [用于提交任务模块结果的示例](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module)。

    > [!NOTE]
    > 当前无法从自动程序 `err` 调用任务模块时检测事件。

5. 如果正在使用 TaskInfo 对象的 属性加载自己的网页，则蓝色矩形是显示 `url` [网页的位置](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)。 有关详细信息，请参阅任务 [模块大小调整](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-sizing)。
6. 如果你使用 TaskInfo 对象的 属性显示自适应卡片 `card` [，](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) 则添加填充。 有关详细信息，请参阅 HTML [任务模块 CSS 或 JavaScript 任务模块](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-css-for-html-or-javascript-task-modules)。
7. 选择注册 后，自适应卡片 **按钮呈现**。 使用你自己的页面时，创建你自己的按钮。

## <a name="see-also"></a>另请参阅

[卡片](~/task-modules-and-cards/what-are-cards.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [调用和关闭任务模块](~/task-modules-and-cards/task-modules/invoking-task-modules.md)
