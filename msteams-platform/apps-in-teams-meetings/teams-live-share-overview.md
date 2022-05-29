---
title: 实时共享概述
description: 在本模块中，了解什么是 Microsoft 实时共享 SDK 及其用户方案。
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.openlocfilehash: 5fa509ee7835db80a99487ed7d42ab7d6ed8341d
ms.sourcegitcommit: 09ee0305b827ad6d1368d892db3824c5dbad886f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2022
ms.locfileid: "65759653"
---
---

# <a name="live-share-sdk"></a>实时共享 SDK

> [!Note]
> 实时共享 SDK 当前仅在 [公共开发人员预览版](../resources/dev-preview/developer-preview-intro.md) 中可用。 你必须是 Microsoft Teams 公共开发人员预览版的成员，才能使用实时共享 SDK。

实时共享是一种 SDK，旨在将 Teams 应用转换为协作式多用户体验，而无需编写任何专用的后端代码。 实时共享 SDK 无缝集成了会议和 [Fluid Framework](https://fluidframework.com/)。 Fluid Framework 是用于分发和同步共享状态的客户端库集合。 实时共享提供完全托管的免费功能，并可随时使用由 Teams 安全和全局缩放提供支持的 [Azure Fluid Relay](/azure/azure-fluid-relay/)。

> [!div class="nextstepaction"]
> [入门](teams-live-share-quick-start.md)

实时共享 SDK 提供了一个 `TeamsFluidClient` 类，用于通过几行代码即可连接到与每个会议关联的特殊 Fluid 容器。 除了 Fluid Framework 提供的数据结构之外，实时共享还支持一组新的分布式数据结构 (DDS) 类，以简化常见会议方案（如共享媒体播放）的应用程序构建。

:::image type="content" source="../assets/images/teams-live-share/teams-live-share-contoso-video.gif" alt-text="实时共享 视频共享体验":::

## <a name="why-build-apps-using-the-live-share-sdk"></a>为什么使用实时共享 SDK 生成应用？

构建协作应用可能很困难、耗时、成本高昂，并且涉及大规模且复杂的合规性要求。 Teams 用户花费大量时间与团队成员共同审阅工作、一起观看视频，并通过屏幕共享来集思广益，以提出新的想法。 借助实时共享 SDK，能够将应用转换为协作性更强但投资最少的项目。

下面是实时共享 SDK 的一些关键优势：

* 无障碍会话管理和安全性
* 有状态和无状态分布式数据结构
* 媒体扩展可轻松同步视频和音频
* 使用角色验证尊重会议权限
* 提供低延迟的免费和完全托管服务
* 智能音频闪避

:::image type="content" source="../assets/images/teams-live-share/Teams-live-share-schematics.png" alt-text="Teams Live Share":::

## <a name="user-scenarios"></a>用户方案

|应用场景|示例|
| :------- | :--------------------- |
| 用户及其同事计划召开会议，以在即将举行的领导力评审中展示提前编辑的市场营销视频，并希望突出显示特定的反馈部分。 | 用户将视频共享到会议偃师区域并启动视频。 用户根据需要暂停视频以讨论方案。 用户可以轮流绘制屏幕的各个部分来强调要点。|
| 作为敏捷团队的项目经理，你和团队一起玩 Agile Poker 游戏，以估算即将开始的行动需要的工作量。| 你将 Agile Poker 规划应用共享到使用实时共享 SDK 的会议阶段，并在团队达成共识之前玩规划游戏。|

> [!IMPORTANT]
> 在 24 小时内，可以访问通过实时共享 SDK 托管的 Azure Fluid Relay 服务发送或存储的任何数据。 有关详细信息，请参阅 [实时共享常见问题解答](teams-live-share-faq.md)。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [入门](teams-live-share-quick-start.md)

## <a name="see-also"></a>另请参阅

* [GitHub 存储库](https://github.com/microsoft/live-share-sdk)
* [Live Share SDK 参考文档](/javascript/api/@microsoft/live-share/)
* [Live Share 媒体 SDK 参考文档](/javascript/api/@microsoft/live-share-media/)
* [Live Share 功能](teams-live-share-capabilities.md)
* [Live Share 媒体功能](teams-live-share-media-capabilities.md)
* [Live Share 常见问题解答](teams-live-share-faq.md)
* [会议中的 Teams 应用](teams-apps-in-meetings.md)
