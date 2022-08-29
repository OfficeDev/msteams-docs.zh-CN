---
title: 实时共享概述
author: surbhigupta
description: 在本模块中，了解什么是 Microsoft 实时共享 SDK 及其用户方案。
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: 3738ee1037c87f283fd31ebdaba53b57f1784bb2
ms.sourcegitcommit: 134ce9381891e51e6327f1f611fdfd60c90cca18
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2022
ms.locfileid: "67425622"
---
---

# <a name="live-share-sdk"></a>实时共享 SDK

> [!NOTE]
> Live Share SDK 当前在 [公共开发人员预览版](../resources/dev-preview/developer-preview-intro.md)中可用。 必须是 Microsoft Teams 的公共开发人员预览版的一部分才能使用 Live Share。

实时共享是一种 SDK，旨在将 Teams 应用转换为协作式多用户体验，而无需编写任何专用的后端代码。 Live Share 将会议与 [Fluid Framework](https://fluidframework.com/) 无缝集成。 Fluid Framework 是用于分发和同步共享状态的客户端库集合。 实时共享提供完全托管的免费功能，并可随时使用由 Teams 安全和全局缩放提供支持的 [Azure Fluid Relay](/azure/azure-fluid-relay/)。

> [!div class="nextstepaction"]
> [入门](teams-live-share-quick-start.md)

Live Share 包含一个 `TeamsFluidClient` 类，用于连接到几行代码中与每个会议关联的特殊 Fluid 容器。 除了 Fluid Framework 提供的数据结构之外，实时共享还支持一组新的分布式数据结构 (DDS) 类，以简化常见会议方案（如共享媒体播放）的应用程序构建。

:::image type="content" source="../assets/images/teams-live-share/teams-live-share-contoso-video.gif" alt-text="实时共享 视频共享体验":::

## <a name="why-build-apps-with-live-share"></a>为什么要使用 Live Share 生成应用？

构建协作应用可能很困难、耗时、成本高昂，并且涉及大规模且复杂的合规性要求。 Teams 用户花费大量时间与团队成员共同审阅工作、一起观看视频，并通过屏幕共享来集思广益，以提出新的想法。 借助实时共享 SDK，能够将应用转换为协作性更强但投资最少的项目。

下面是实时共享 SDK 的一些关键优势：

- 无障碍会话管理和安全性。
- 有状态和无状态分布式数据结构。
- 媒体扩展可轻松同步视频和音频。
- 使用角色验证尊重会议权限。
- 提供低延迟的免费和完全托管服务。
- 智能音频闪避。

:::image type="content" source="../assets/images/teams-live-share/Teams-live-share-schematics.png" alt-text="Teams Live Share":::

若要了解 Live Share 是否适合你的协作方案，了解 Live Share 与其他协作框架之间的差异很有帮助，包括：

- [Web 套接字](#web-sockets)
- [Azure Fluid Relay](#azure-fluid-relay)
- [Live Share](#live-share-hosted-service)

### <a name="web-sockets"></a>Web 套接字

Web 套接字是一种在 Web 中进行实时通信的普遍技术，某些应用可能更愿意使用自己的自定义 Web 套接字后端。 与 REST API 不同，Web 套接字在会话中的服务器和客户端之间保持开放连接。

与其他自定义 API 服务一样，要求通常包括对会话进行身份验证、区域映射、维护和缩放。 许多协作方案还需要在服务器中保持会话状态，这需要存储基础结构、冲突解决等。

### <a name="azure-fluid-relay"></a>Azure Fluid Relay

[Azure Fluid Relay](/azure/azure-fluid-relay/) 是 Fluid Framework 的托管产品/服务，可帮助开发人员跨连接的 JavaScript 客户端生成实时协作体验和复制状态。 Microsoft Whiteboard、Loop 和 OneNote 都是当前使用 Fluid Framework 生成的应用的示例。

与其他 Azure 服务一样，Azure Fluid Relay 旨在以最少的复杂性定制单个项目需求。 要求包括为 Fluid 容器开发身份验证案例和区域符合性。 配置后，开发人员可以专注于提供高质量的协作体验。

### <a name="live-share-hosted-service"></a>Live Share 托管服务

Live Share 提供由 Microsoft Teams 会议安全性支持的交钥匙 Azure Fluid Relay 服务。 Live Share 容器仅限于会议参与者、维护租户驻留要求，并且可以在几行客户端代码中访问。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { TeamsFluidClient, EphemeralPresence } from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { presence: EphemeralPresence },
};
const { container } = await client.joinContainer(schema);

// ... ready to start app sync logic
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { TeamsFluidClient, EphemeralPresence } from "@microsoft/live-share";
import { ContainerSchema } from "fluid-framework";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema: ContainerSchema = {
  initialObjects: { presence: EphemeralPresence },
};
const { container } = await client.joinContainer(schema);

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
