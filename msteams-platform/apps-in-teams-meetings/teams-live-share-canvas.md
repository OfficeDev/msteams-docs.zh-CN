---
title: Live Share 画布概述
author: surbhigupta
description: 在本模块中，详细了解 Live Share 画布、启用墨迹书写、激光指针和会议应用游标的扩展。
ms.topic: conceptual
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 10/04/2022
ms.openlocfilehash: 3845d890de365eca8029a3f28d770586a6929743
ms.sourcegitcommit: 0fa0bc081da05b2a241fd8054488d9fd0104e17b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2022
ms.locfileid: "68552603"
---
# <a name="live-share-canvas-overview"></a>Live Share 画布概述

:::image type="content" source="../assets/images/teams-live-share/live-share-canvas-docs-feature-1.png" alt-text="Teams Live Share 媒体同步":::

在全球各地的会议室和教室中，白板是合作的关键部分。 然而，在现代，白板已经不够了。 由于 PowerPoint 等众多数字工具是现代协作的焦点，因此必须具有相同的创意潜力。

为了实现更无缝的协作，Microsoft 创建了PowerPoint Live，这对于用户在 Teams 中的工作方式起到了重要作用。 演示者可以使用笔、荧光笔和激光笔在幻灯片上进行批注，以吸引大家对关键概念的关注。 使用 Live Share 画布，你的应用可以以最少的精力PowerPoint Live墨迹书写工具。

## <a name="install"></a>安装

若要使用 npm 将最新版本的 SDK 添加到应用程序，请执行以下操作：

```bash
npm install @microsoft/live-share@next --save
npm install @microsoft/live-share-canvas@next --save
```

OR

若要使用 [Yarn](https://yarnpkg.com/) 将最新版本的 SDK 添加到应用程序，请执行以下操作：

```bash
yarn add @microsoft/live-share@next
yarn add @microsoft/live-share-canvas@next
```

## <a name="setting-up-the-package"></a>设置包

Live Share 画布有两个主要类，用于启用轮次键协作： `InkingManager` 和 `LiveCanvas`。 `InkingManager` 负责将功能齐全的 `<canvas>` 元素附加到应用，同时 `LiveCanvas` 管理与其他会议参与者的远程同步。 将应用一起使用，只需几行代码即可获得类似于白板的完整功能。

| 课程                                                                     | 说明                                                                                                                                                                                                                                      |
| --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [InkingManager](/javascript/api/@microsoft/live-share-canvas/inkingmanager) | 将元素附加 `<canvas>` 到给定 `<div>` 元素以自动管理笔划或荧光笔划、激光笔、线条和箭头以及橡皮擦的类。 公开一组 API (，以控制哪个工具处于活动状态) 和基本配置设置。 |
| [LiveCanvas](/javascript/api/@microsoft/live-share-canvas/livecanvas)      | 一个 `SharedObject` 类，用于同步 Live Share 会话中每个人的笔划和光标位置 `InkingManager` 。                                                                                                                   |

示例：

```html
<body>
  <div id="canvas-host"></div>
</body>
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient } from "@microsoft/live-share";
import { InkingManager, LiveCanvas } from "@microsoft/live-share-canvas";

// Setup the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { liveCanvas: LiveCanvas },
};
const { container } = await liveShare.joinContainer(schema);
const { liveCanvas } = container.initialObjects;

// Get the canvas host element
const canvasHostElement = document.getElementById("canvas-host");
const inkingManager = new InkingManager(canvasHostElement);

// Begin synchronization for LiveCanvas
await liveCanvas.initialize(inkingManager);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { LiveShareClient } from "@microsoft/live-share";
import { InkingManager, LiveCanvas } from "@microsoft/live-share-canvas";
import { ContainerSchema } from "fluid-framework";

// Setup the Fluid container
const liveShare = new LiveShareClient();
const schema: ContainerSchema = {
  initialObjects: { liveCanvas: LiveCanvas },
};
const { container } = await liveShare.joinContainer(schema);
const liveCanvas = container.initialObjects.liveCanvas as LiveCanvas;

// Get the canvas host element
const canvasHostElement = document.getElementById("canvas-host");
const inkingManager = new InkingManager(canvasHostElement);

// Begin synchronization for LiveCanvas
await liveCanvas.initialize(inkingManager);
```

---

## <a name="canvas-tools--cursors"></a>&游标的画布工具

设置并同步 Live Share 画布后，可以配置画布以进行用户交互，例如用于选择笔工具的按钮。 在本部分中，我们将讨论哪些工具可用以及如何使用它们。

### <a name="inking-tools"></a>墨迹书写工具

Live Share 画布中的每个墨迹书写工具都会在用户绘制时呈现笔划。 如果使用触摸屏或触笔，工具还支持压力动态，从而影响笔划宽度。 配置设置包括画笔颜色、粗细、形状和可选的端箭头。

#### <a name="pen-tool"></a>笔工具

:::image type="content" source="../assets/images/teams-live-share/canvas-pen-tool.gif" alt-text="Teams Live Share 画布笔工具":::

笔工具绘制存储在画布中的纯笔划。 默认提示形状是一个圆圈。

```html
<div>
  <button id="pen">Enable Pen</button>
  <label for="pen-color">Select a color:</label>
  <input type="color" id="color" name="color" value="#000000" />
  <button id="pen-tip-size">Increase pen size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
  fromCssColor,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to pen
document.getElementById("pen").onclick = () => {
  inkingManager.tool = InkingTool.pen;
};
// Change the selected color for pen
document.getElementById("pen-color").onchange = () => {
  const colorPicker = document.getElementById("color");
  inkingManager.penBrush.color = fromCssColor(colorPicker.value);
};
// Increase the tip size for pen
document.getElementById("pen-tip-size").onclick = () => {
  inkingManager.penBrush.tipSize = inkingManager.penBrush.tipSize + 1;
};
```

#### <a name="highlighter-tool"></a>荧光笔工具

:::image type="content" source="../assets/images/teams-live-share/canvas-highlighter-tool.gif" alt-text="Teams Live Share 画布荧光笔工具":::

荧光笔工具绘制存储在画布中的半透明笔划。 默认提示形状为正方形。

```html
<div>
  <button id="highlighter">Enable Highlighter</button><br />
  <label for="highlighter-color">Select a color:</label>
  <input type="color" id="highlighter-color" name="highlighter-color" value="#FFFC00" />
  <button id="highlighter-tip-size">Increase tip size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
  fromCssColor,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to highlighter
document.getElementById("highlighter").onclick = () => {
  inkingManager.tool = InkingTool.highlighter;
};
// Change the selected color for highlighter
document.getElementById("highlighter-color").onchange = () => {
  const colorPicker = document.getElementById("highlighter-color");
  inkingManager.highlighterBrush.color = fromCssColor(colorPicker.value);
};
// Increase the tip size for highlighter
document.getElementById("highlighter-tip-size").onclick = () => {
  inkingManager.highlighterBrush.tipSize = inkingManager.penBrush.tipSize + 1;
};
```

#### <a name="eraser-tool"></a>橡皮擦工具

:::image type="content" source="../assets/images/teams-live-share/canvas-eraser-tool.gif" alt-text="Teams Live Share 画布橡皮擦工具":::

橡皮擦工具擦除穿过其路径的整个笔划。

```html
<div>
  <button id="eraser">Enable Eraser</button><br />
  <button id="eraser-size">Increase eraser size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to eraser
document.getElementById("eraser").onclick = () => {
  inkingManager.tool = InkingTool.eraser;
};
// Increase the tip size for eraser
document.getElementById("eraser-size").onclick = () => {
  inkingManager.eraserSize = inkingManager.eraserSize + 1;
};
```

#### <a name="point-eraser-tool"></a>点橡皮擦工具

:::image type="content" source="../assets/images/teams-live-share/canvas-point-eraser-tool.gif" alt-text="Teams Live Share 画布点橡皮擦工具":::

点橡皮擦工具通过将现有笔划拆分为一半来清除跨越其路径的笔划中的各个点。 此工具的计算成本高昂，可能会使用户的帧速率降低。

> [!NOTE]
> 点橡皮擦与常规橡皮擦工具共享相同的橡皮擦点大小。

```html
<div>
  <button id="point-eraser">Enable Point Eraser</button><br />
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to eraser
document.getElementById("point-eraser").onclick = () => {
  inkingManager.tool = InkingTool.pointEraser;
};
```

#### <a name="laser-pointer"></a>激光指针

:::image type="content" source="../assets/images/teams-live-share/canvas-laser-tool.gif" alt-text="Teams Live Share 画布激光指针工具":::

激光笔是唯一的，因为在移动鼠标时激光尖具有尾随效果。 绘制笔划时，尾随效果会在完全消失之前呈现一小段时间。 此工具非常适合在会议期间指出屏幕上的信息，因为演示者不必在工具之间切换以擦除笔划。

```html
<div>
  <button id="laser">Enable Laser Pointer</button><br />
  <label for="laser-color">Select a color:</label>
  <input type="color" id="laser-color" name="laser-color" value="#000000" />
  <button id="laser-tip-size">Increase tip size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
  fromCssColor,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to laser pointer
document.getElementById("laser").onclick = () => {
  inkingManager.tool = InkingTool.highlighter;
};
// Change the selected color for laser pointer
document.getElementById("laser-color").onchange = () => {
  const colorPicker = document.getElementById("laser-color");
  inkingManager.laserPointerBrush.color = fromCssColor(colorPicker.value);
};
// Increase the tip size for laser pointer
document.getElementById("laser-tip-size").onclick = () => {
  inkingManager.laserPointerBrush.tipSize = inkingManager.laserPointerBrush.tipSize + 1;
};
```

#### <a name="line-and-arrow-tools"></a>线和箭头工具

:::image type="content" source="../assets/images/teams-live-share/canvas-line-tool.gif" alt-text="Teams Live Share 画布行工具":::

线条工具允许用户使用可应用于末尾的可选箭头从一个点到另一个点绘制直线。

```html
<div>
  <button id="line">Enable Line</button><br />
  <button id="line-arrow">Enable Arrow</button><br />
  <input type="color" id="line-color" name="line-color" value="#000000" />
  <button id="line-tip-size">Increase tip size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
  fromCssColor,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to line
document.getElementById("line").onclick = () => {
  inkingManager.tool = InkingTool.line;
  inkingManager.lineBrush.endArrow = "none";
};
// Change the selected tool to line
document.getElementById("line-arrow").onclick = () => {
  inkingManager.tool = InkingTool.line;
  inkingManager.lineBrush.endArrow = "open";
};
// Change the selected color for lineBrush
document.getElementById("line-color").onchange = () => {
  const colorPicker = document.getElementById("line-color");
  inkingManager.lineBrush.color = fromCssColor(colorPicker.value);
};
// Increase the tip size for lineBrush
document.getElementById("line-tip-size").onclick = () => {
  inkingManager.lineBrush.tipSize = inkingManager.lineBrush.tipSize + 1;
};
```

#### <a name="clear-all-strokes"></a>清除所有笔划

可以通过调用 `inkingManager.clear()`来清除画布中的所有笔划。 这会从画布中删除所有笔划。

### <a name="cursors"></a>游标

:::image type="content" source="../assets/images/teams-live-share/canvas-cursors.gif" alt-text="Teams Live Share 游标共享":::

可以在应用程序中启用实时游标，让用户在画布上跟踪彼此的游标位置。 与墨迹书写工具不同，游标完全通过类运行 `LiveCanvas` 。 可以选择提供名称和图片来标识每个用户。 可以单独启用游标，也可以使用墨迹化工具启用游标。

```javascript
// Optional. Set user display info
liveCanvas.onGetLocalUserInfo = () => {
  return {
    displayName: "YOUR USER NAME",
    pictureUri: "YOUR USER PICTURE URI",
  };
};
// Toggle Live Canvas cursor enabled state
liveCanvas.isCursorShared = !isCursorShared;
```

## <a name="optimizing-across-devices"></a>跨设备进行优化

对于 Web 上的大多数应用程序，内容呈现方式因屏幕大小或应用程序状态不同而异。 如果 `InkingManager` 应用未正确优化，可能会导致每个用户的笔划和游标出现不同。 Live Share 画布支持一组简单的 API，这允许 `<canvas>` 调整笔划位置以正确地与内容保持一致。

默认情况下，Live Share 画布的工作方式与白板应用非常类似，内容以中心方式与具有 1 倍缩放级别的视区对齐。 只有一部分内容呈现在可见边界 `<canvas>`内。 从概念上讲，这就像从鸟瞰图录制视频一样。 虽然相机的视区正在记录它下面的一部分世界，但现实世界几乎无限地向每一个方向延伸。

下面是一个帮助可视化此概念的简单关系图：

:::image type="content" source="../assets/images/teams-live-share/live-share-canvas-capabilities-docs-diagram-1.png" alt-text="Live Share 画布视区可视化效果":::

可以通过以下方式自定义此行为：

- 将起始引用点更改为画布的左上角。
- 更改视区的像素偏移量 x 和 y 位置。
- 更改视区的规模级别。

> [!NOTE]
> 引用点、偏移量和缩放级别是客户端的本地级别，不会在会议参与者之间同步。

示例：

```html
<body>
  <button id="pan-left">Pan left</button>
  <button id="pan-up">Pan up</button>
  <button id="pan-right">Pan right</button>
  <button id="pan-down">Pan down</button>
  <button id="zoom-out">Zoom out</button>
  <button id="zoom-in">Zoom in</button>
  <button id="change-reference">Change reference</button>
</body>
```

```javascript
// ...

// Pan left
document.getElementById("pan-left").onclick = () => {
  inkingManager.offset = {
    x: inkingManager.offset.x - 10,
    y: inkingManager.offset.y,
  };
};
// Pan up
document.getElementById("pan-up").onclick = () => {
  inkingManager.offset = {
    x: inkingManager.offset.x,
    y: inkingManager.offset.y - 10,
  };
};
// Pan right
document.getElementById("pan-right").onclick = () => {
  inkingManager.offset = {
    x: inkingManager.offset.x + 10,
    y: inkingManager.offset.y,
  };
};
// Pan down
document.getElementById("pan-down").onclick = () => {
  inkingManager.offset = {
    x: inkingManager.offset.x,
    y: inkingManager.offset.y + 10,
  };
};
// Zoom out
document.getElementById("zoom-out").onclick = () => {
  if (inkingManager.scale > 0.1) {
    inkingManager.scale -= 0.1;
  }
};
// Zoom in
document.getElementById("zoom-in").onclick = () => {
  inkingManager.scale += 0.1;
};
// Change reference
document.getElementById("change-reference").onclick = () => {
  if (inkingManager.referencePoint === "center") {
    inkingManager.referencePoint = "topLeft";
  } else {
    inkingManager.referencePoint = "center";
  }
};
```

## <a name="ideal-scenarios"></a>理想方案

由于网页具有各种形状和大小，因此无法使 Live Share 画布支持每个方案。 此包非常适合所有用户同时查看相同内容的方案。 虽然并非所有内容都需要在屏幕上可见，但它必须是跨设备线性缩放的内容。

下面是一些方案示例，其中 Live Share 画布是应用程序的绝佳选项：

- 覆盖在所有客户端上以相同的纵横比呈现的图像和视频。
- 从相同的旋转角度查看地图、3D 模型或白板。

这两种方案都运行良好，因为即使用户使用不同的缩放级别和偏移量查看内容，也可以在所有设备上查看相同的内容。 如果应用的布局或内容根据屏幕大小而变化，并且无法为所有参与者生成通用视图，则 Live Share 画布可能不适合你的方案。

## <a name="code-samples"></a>代码示例

| 示例名称          | Description                            | JavaScript                                                                                |
| -------------------- | -------------------------------------- | ----------------------------------------------------------------------------------------- |
| Live Canvas 演示     | 简单的白板应用程序。         | [View](https://github.com/microsoft/live-share-sdk/tree/main/samples/03.live-canvas-demo) |
| React 媒体模板 | 在同步的视频播放器上绘制。 | [View](https://aka.ms/liveshare-mediatemplate)                                            |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [Agile Poker 教程](../sbs-teams-live-share.yml)

## <a name="see-also"></a>另请参阅

- [Live Share SDK 常见问题解答](teams-live-share-faq.md)
- [Live Share SDK 参考文档](/javascript/api/@microsoft/live-share/)
- [Live Share Canvas SDK 参考文档](/javascript/api/@microsoft/live-share-canvas/)
- [会议中的 Teams 应用](teams-apps-in-meetings.md)
