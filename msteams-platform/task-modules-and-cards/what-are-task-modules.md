---
title: 任务模块
author: surbhigupta
description: 添加模式弹出窗口体验，以从你的应用收集信息或向用户Microsoft Teams信息
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 257ca54ab53d310116cc301dded01a7582c11532
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140535"
---
# <a name="task-modules"></a><span data-ttu-id="a9d1e-103">任务模块</span><span class="sxs-lookup"><span data-stu-id="a9d1e-103">Task modules</span></span>

<span data-ttu-id="a9d1e-104">任务模块允许在任务应用程序中创建模式弹出Teams体验。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-104">Task modules permit you to create modal pop-up experiences in your Teams application.</span></span> <span data-ttu-id="a9d1e-105">在弹出窗口中，您可以：</span><span class="sxs-lookup"><span data-stu-id="a9d1e-105">In the pop-up, you can:</span></span>

* <span data-ttu-id="a9d1e-106">运行你自己的自定义 HTML 或 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-106">Run your own custom HTML or JavaScript code.</span></span>
* <span data-ttu-id="a9d1e-107">显示 `<iframe>` 基于小部件（如 YouTube 或 Microsoft Stream 视频）。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-107">Show an `<iframe>`-based widget such as a YouTube or Microsoft Stream video.</span></span>
* <span data-ttu-id="a9d1e-108">显示 [自适应卡片](/adaptive-cards/)。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-108">Display an [Adaptive Card](/adaptive-cards/).</span></span>

<span data-ttu-id="a9d1e-109">任务模块可用于启动和完成任务或显示丰富的信息，例如视频或 POWER Business Intelligence (BI) 仪表板。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-109">Task modules are useful for initiating and completing tasks or displaying rich information, such as videos or Power Business Intelligence (BI) dashboards.</span></span> <span data-ttu-id="a9d1e-110">与选项卡或基于对话的机器人体验相比，用户启动和完成任务通常更自然。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-110">A pop-up experience is often more natural for users initiating and completing tasks compared to a tab or a conversation-based bot experience.</span></span>

<span data-ttu-id="a9d1e-111">任务模块基于选项卡Microsoft Teams构建。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-111">Task modules build on the foundation of Microsoft Teams tabs.</span></span> <span data-ttu-id="a9d1e-112">它们实质上是弹出窗口中的一个选项卡。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-112">They are essentially a tab inside a pop-up window.</span></span> <span data-ttu-id="a9d1e-113">它们使用相同的 SDK，因此如果你已生成了一个选项卡，则你已经熟悉如何创建任务模块。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-113">They use the same SDK, so if you have built a tab you are already familiar with creating a task module.</span></span>

<span data-ttu-id="a9d1e-114">可通过 3 种方式调用任务模块：</span><span class="sxs-lookup"><span data-stu-id="a9d1e-114">Task modules can be invoked in three ways:</span></span>

* <span data-ttu-id="a9d1e-115">频道或个人选项卡：使用 Microsoft Teams 选项卡 SDK，可以从选项卡上的按钮、链接或菜单调用任务模块。有关详细信息，请参阅在[选项卡中使用任务模块](~/task-modules-and-cards/task-modules/task-modules-tabs.md)。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-115">Channel or personal tabs: Using the Microsoft Teams Tabs SDK, you can invoke task modules from buttons, links, or menus on your tab. For more information, see [using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>
* <span data-ttu-id="a9d1e-116">自动程序：使用从自动程序 [发送](~/task-modules-and-cards/cards/cards-reference.md) 的卡片上的按钮。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-116">Bots: Using buttons on [cards](~/task-modules-and-cards/cards/cards-reference.md) sent from your bot.</span></span> <span data-ttu-id="a9d1e-117">当你不要求频道中的每个人都查看你使用机器人执行什么操作时，这非常有用。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-117">This is useful when you do not require everyone in a channel to see what you are doing with a bot.</span></span> <span data-ttu-id="a9d1e-118">例如，当用户在频道中回复投票时，查看所创建的轮询记录将没有用。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-118">For example, when having users respond to a poll in a channel it is not useful to see a record of that poll being created.</span></span> <span data-ttu-id="a9d1e-119">有关详细信息，请参阅使用[自动程序中Teams模块](~/task-modules-and-cards/task-modules/task-modules-bots.md)。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-119">For more information, see [using task modules from Teams bots](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>
* <span data-ttu-id="a9d1e-120">在Teams链接之外：还可以创建 URL 以从任何位置调用任务模块。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-120">Outside of Teams from a deep link: You can also create URLs to invoke a task module from anywhere.</span></span> <span data-ttu-id="a9d1e-121">有关详细信息，请参阅任务 [模块深度链接语法](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-121">For more information, see [task module deep link syntax](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax).</span></span>

## <a name="components-of-a-task-module"></a><span data-ttu-id="a9d1e-122">任务模块的组件</span><span class="sxs-lookup"><span data-stu-id="a9d1e-122">Components of a task module</span></span>

<span data-ttu-id="a9d1e-123">下面是从自动程序调用任务模块时的外观：</span><span class="sxs-lookup"><span data-stu-id="a9d1e-123">Here is what a task module looks like when invoked from a bot:</span></span>

![任务模块示例](~/assets/images/task-module/task-module-example.png)

<span data-ttu-id="a9d1e-125">任务模块包括以下内容，如上图所示：</span><span class="sxs-lookup"><span data-stu-id="a9d1e-125">A task module includes the following as shown in the previous image:</span></span>

1. <span data-ttu-id="a9d1e-126">应用的[ `color` 图标](~/resources/schema/manifest-schema.md#icons)。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-126">Your app's [`color` icon](~/resources/schema/manifest-schema.md#icons).</span></span>
2. <span data-ttu-id="a9d1e-127">应用[ `short` 的名称](~/resources/schema/manifest-schema.md#name)。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-127">Your app's [`short` name](~/resources/schema/manifest-schema.md#name).</span></span>
3. <span data-ttu-id="a9d1e-128">任务模块的标题在 `title` [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)对象的 属性中指定。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-128">The task module's title specified in the `title` property of the [TaskInfo object](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object).</span></span>
4. <span data-ttu-id="a9d1e-129">任务模块的关闭或取消按钮。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-129">The task module's close or cancel button.</span></span> <span data-ttu-id="a9d1e-130">如果用户选择此按钮，你的应用将收到 `err` 事件。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-130">If the user selects this button, your app receives an `err` event.</span></span> <span data-ttu-id="a9d1e-131">有关详细信息，请参阅 [用于提交任务模块结果的示例](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module)。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-131">For more information, see [example for submitting the result of a task module](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module).</span></span>

    > [!NOTE]
    > <span data-ttu-id="a9d1e-132">当前无法从自动程序 `err` 调用任务模块时检测事件。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-132">It is currently not possible to detect the `err` event when a task module is invoked from a bot.</span></span>

5. <span data-ttu-id="a9d1e-133">如果正在使用 TaskInfo 对象的 属性加载自己的网页，则蓝色矩形是显示 `url` [网页的位置](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-133">The blue rectangle is where your web page appears if you are loading your own web page using the `url` property of the [TaskInfo object](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="a9d1e-134">有关详细信息，请参阅任务 [模块大小调整](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-sizing)。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-134">For more information, see [task module sizing](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-sizing).</span></span>
6. <span data-ttu-id="a9d1e-135">如果你使用 TaskInfo 对象的 属性显示自适应卡片 `card` [，](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) 则添加填充。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-135">If you are displaying an Adaptive Card using the `card` property of the [TaskInfo object](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) the padding is added for you.</span></span> <span data-ttu-id="a9d1e-136">有关详细信息，请参阅 HTML [任务模块 CSS 或 JavaScript 任务模块](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-css-for-html-or-javascript-task-modules)。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-136">For more information, see [task module CSS for HTML or JavaScript task modules](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-css-for-html-or-javascript-task-modules).</span></span>
7. <span data-ttu-id="a9d1e-137">选择注册 后，自适应卡片 **按钮呈现**。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-137">Adaptive Card buttons render after you select **Sign up**.</span></span> <span data-ttu-id="a9d1e-138">使用你自己的页面时，创建你自己的按钮。</span><span class="sxs-lookup"><span data-stu-id="a9d1e-138">When using your own page, create your own buttons.</span></span>

## <a name="see-also"></a><span data-ttu-id="a9d1e-139">另请参阅</span><span class="sxs-lookup"><span data-stu-id="a9d1e-139">See also</span></span>

[<span data-ttu-id="a9d1e-140">卡</span><span class="sxs-lookup"><span data-stu-id="a9d1e-140">Cards</span></span>](~/task-modules-and-cards/what-are-cards.md)

## <a name="next-step"></a><span data-ttu-id="a9d1e-141">后续步骤</span><span class="sxs-lookup"><span data-stu-id="a9d1e-141">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a9d1e-142">调用和消除任务模块</span><span class="sxs-lookup"><span data-stu-id="a9d1e-142">Invoke and dismiss task modules</span></span>](~/task-modules-and-cards/task-modules/invoking-task-modules.md)
