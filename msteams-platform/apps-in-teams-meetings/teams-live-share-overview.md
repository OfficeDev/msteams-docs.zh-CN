---
title: 实时共享概述
author: surbhigupta
description: 在本模块中，了解什么是 Microsoft 实时共享 SDK 及其用户方案。
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: 38157dea1c2d24b82cf1f48829639fd1d92392c1
ms.sourcegitcommit: 0fa0bc081da05b2a241fd8054488d9fd0104e17b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2022
ms.locfileid: "68552524"
---
---

# <a name="live-share-sdk"></a>实时共享 SDK

> [!VIDEO https://www.youtube.com/embed/971YIvosuUk]

实时共享是一种 SDK，旨在将 Teams 应用转换为协作式多用户体验，而无需编写任何专用的后端代码。 使用 Live Share，用户可以在会议期间共同观看、共同创建和共同编辑。

有时屏幕共享是不够的，这就是为什么 Microsoft 将 PowerPoint Live 和 Whiteboard 等工具直接构建到 Teams 中的原因。 通过将 Web 应用程序直接引入会议界面的中心阶段，用户可以在会议和通话期间无缝协作。

> [!div class="nextstepaction"]
> [入门](teams-live-share-quick-start.md)

## <a name="feature-overview"></a>功能概述

Live Share 有三个支持无限协作方案的包。 这些包 (DDS) 公开一组分布式数据结构，包括基元构建基块和交钥方案。

Live Share 将会议与 [Fluid Framework](https://fluidframework.com/) 无缝集成。 Fluid Framework 是用于分发和同步共享状态的客户端库集合。 实时共享提供完全托管的免费功能，并可随时使用由 Teams 安全和全局缩放提供支持的 [Azure Fluid Relay](/azure/azure-fluid-relay/)。

### <a name="live-share-core"></a>Live Share core

使用 Live Share，可以连接到几行代码中与每个会议关联的特殊 Fluid 容器。 除了 Fluid Framework 提供的数据结构外，Live Share 还支持一组新的 DDS 类，以简化会议中的同步应用状态。

Live Share 核心包支持的功能包括：

- 加入会议的 Live Share 会话 `LiveShareClient`。
- 跟踪会议状态并同步用户元数据 `LivePresence`。
- 将实时事件发送到会话中的其他客户端 `LiveEvent`。
- 协调用户离开会话 `LiveState`时消失的应用状态。
- 将倒计时计时器与 `LiveTimer`.
- 利用 Fluid Framework 的任何功能，例如 `SharedMap` 和 `SharedString`。

可以在 [核心功能页](./teams-live-share-capabilities.md)上找到有关此包的详细信息。

### <a name="live-share-media"></a>实时共享媒体

:::image type="content" source="../assets/images/teams-live-share/teams-live-share-contoso-video.gif" alt-text="实时共享 视频共享体验":::

视频和音频是现代世界和工作场所的重要部分。 Live Share 媒体为只有几行代码的任何媒体播放器启用 **媒体同步** 。 通过在播放器状态和传输控件层同步媒体，可以单独属性视图，同时提供可通过应用获得的最高质量。 由于 Microsoft 未重新广播媒体内容，因此许可和访问要求保持不变。

Live Share 媒体支持的功能包括：

- 同步媒体播放器状态并跟踪 `MediaPlayerSynchronizer`。
- 用户在会议期间交谈时对媒体卷进行智能调整。
- 限制哪些用户可以修改玩家状态。
- 在飞行时或在计划的等待点暂停和恢复媒体同步。

可以在 [Live Share 媒体页面](./teams-live-share-media-capabilities.md)上找到有关此包的详细信息。

> [!NOTE]
> Live Share 不会重新广播媒体内容。 它专为用于嵌入式 Web 播放器（如 HTML5 `<video>` 或 Azure Media Player）而设计。

### <a name="live-share-canvas"></a>Live Share 画布

:::image type="content" source="../assets/images/teams-live-share/Teams-live-share-schematics.png" alt-text="Teams Live Share":::

在会议中协作时，用户必须能够指出和强调屏幕上的内容。 使用 Live Share 画布，可以轻松地将墨迹、激光指针和游标添加到应用以实现无缝协作。

Live Share 画布支持的功能包括：

- 将协作 `<canvas>` 添加到应用 `LiveCanvas`。
- 使用笔、荧光笔、线条和箭头工具传达想法。
- 使用激光指针有效呈现。
- 与实时鼠标游标一起使用。
- 配置变量设备的设置和视图状态。
- 使用完全支持的鼠标、触控和触笔输入。

可以在 [Live Share 画布页](./teams-live-share-canvas.md)上找到有关此包的详细信息。

## <a name="why-build-apps-with-live-share"></a>为什么要使用 Live Share 生成应用？

构建协作应用可能很困难、耗时、成本高昂，并且涉及大规模且复杂的合规性要求。 Teams 用户花费大量时间与团队成员共同审阅工作、一起观看视频，并通过屏幕共享来集思广益，以提出新的想法。 借助实时共享 SDK，能够将应用转换为协作性更强但投资最少的项目。

下面是实时共享 SDK 的一些关键优势：

- 无障碍会话管理和安全性。
- 有状态和无状态分布式数据结构。
- 媒体扩展可轻松同步视频和音频。
- 轮键墨迹墨迹、激光指针和游标。
- 使用角色验证尊重会议权限。
- 提供低延迟的免费和完全托管服务。

若要了解 Live Share 是否适合你的协作方案，了解 Live Share 与其他协作框架之间的差异很有帮助，包括：

- [Web 套接字](#web-sockets)
- [Azure Fluid Relay](#azure-fluid-relay)
- [Live Share](#live-share-hosted-service)

### <a name="web-sockets"></a>Web 套接字

Web 套接字是一种在 Web 中进行实时通信的普遍技术，某些应用可能更愿意使用自己的自定义 Web 套接字后端。 与 REST API 不同，Web 套接字在会话中的服务器和客户端之间保持开放连接。

与其他自定义 API 服务一样，要求通常包括对会话进行身份验证、区域映射、维护和缩放。 许多协作方案还需要在服务器中保持会话状态，这需要存储基础结构、冲突解决等。

通过使用 Live Share，可以获得 Web 套接字的所有功能，而无需开销。

### <a name="azure-fluid-relay"></a>Azure Fluid Relay

[Azure Fluid Relay](/azure/azure-fluid-relay/) 是 Fluid Framework 的托管产品/服务，可帮助开发人员跨连接的 JavaScript 客户端生成实时协作体验和复制状态。 Microsoft Whiteboard、Loop 和 OneNote 都是当前使用 Fluid Framework 生成的应用的示例。

与其他 Azure 服务一样，Azure Fluid Relay 旨在以最少的复杂性定制单个项目需求。 要求包括为 Fluid 容器开发身份验证案例和区域符合性。 配置后，开发人员可以专注于提供高质量的协作体验。

### <a name="live-share-hosted-service"></a>Live Share 托管服务

Live Share 提供由 Microsoft Teams 会议安全性支持的交钥匙 Azure Fluid Relay 服务。 Live Share 容器仅限于会议参与者、维护租户驻留要求，并且可以在几行客户端代码中访问。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient, LivePresence } from "@microsoft/live-share";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { presence: LivePresence },
};
const { container } = await liveShare.joinContainer(schema);

// ... ready to start app sync logic
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { LiveShareClient, LivePresence } from "@microsoft/live-share";
import { ContainerSchema } from "fluid-framework";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema: ContainerSchema = {
  initialObjects: { presence: LivePresence },
};
const { container } = await liveShare.joinContainer(schema);

// ... ready to start app sync logic
```

---

> [!IMPORTANT]
> 通过 Live Share SDK 托管的 Azure Fluid Relay 服务发送或存储的任何数据最长可在 24 小时内访问。 有关详细信息，请参阅 [实时共享常见问题解答](teams-live-share-faq.md)。

#### <a name="using-a-custom-azure-fluid-relay-service"></a>使用自定义 Azure Fluid Relay 服务

虽然大多数人认为最好使用我们的免费托管服务，但在某些情况下，使用自己的 Azure Fluid Relay 服务来使用 Live Share 应用还是有好处的。

如果有以下事项，请考虑使用自定义服务：

- 需要在会议生存期之后将数据存储在 Fluid 容器中。
- 通过需要自定义安全策略的服务传输敏感数据。
- 例如 `SharedMap`，通过 Fluid Framework 为 Teams 外部的应用程序开发功能。

有关详细信息，请参阅自定义 Azure Fluid Relay 服务 [操作指南](./teams-live-share-how-to/how-to-custom-azure-fluid-relay.md)。

## <a name="user-scenarios"></a>用户方案

| 应用场景                                                                                | 示例                                                                                                                                                                                            |
| :-------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 在市场营销评审期间，用户希望收集有关其最新视频编辑的反馈。 | 用户将视频共享到会议阶段并启动视频。 根据需要，用户暂停视频以讨论场景，参与者在屏幕的各个部分上绘制以强调要点。 |
| 项目经理在规划期间与团队一起玩敏捷扑克。                    | 经理将敏捷扑克应用共享到会议阶段，以便在团队达成共识之前玩计划游戏。                                                                        |
| 财务顾问在签名前与客户一起查看 PDF 文档。                  | 财务顾问将 PDF 合同共享到会议阶段。 所有与会者都可以在 PDF 中看到其他游标和突出显示的文本，然后双方签署协议。        |

> [!IMPORTANT]
> Live Share 根据 [Microsoft Live Share SDK 许可证获得许可](https://github.com/microsoft/live-share-sdk/blob/main/LICENSE)。 若要在应用中使用这些功能，必须先阅读并同意这些条款。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [入门](teams-live-share-quick-start.md)

## <a name="see-also"></a>另请参阅

- [GitHub 存储库](https://github.com/microsoft/live-share-sdk)
- [Live Share SDK 参考文档](/javascript/api/@microsoft/live-share/)
- [Live Share 媒体 SDK 参考文档](/javascript/api/@microsoft/live-share-media/)
- [Live Share 功能](teams-live-share-capabilities.md)
- [Live Share 媒体功能](teams-live-share-media-capabilities.md)
- [Live Share 常见问题解答](teams-live-share-faq.md)
- [会议中的 Teams 应用](teams-apps-in-meetings.md)
