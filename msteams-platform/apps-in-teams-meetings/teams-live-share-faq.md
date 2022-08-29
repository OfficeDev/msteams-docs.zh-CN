---
title: Live Share 常见问题解答
author: surbhigupta
description: 在本模块中，详细了解 Live Share 常见问题解答。
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: b53d7c01722faa51824e0df17586bc8a385438b0
ms.sourcegitcommit: 134ce9381891e51e6327f1f611fdfd60c90cca18
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2022
ms.locfileid: "67425608"
---
---

# <a name="live-share-sdk-faq"></a>Live Share SDK 常见问题解答

获取使用 Live Share 时常见问题的解答。<br>

<br>

<details>

<summary><b>我是否可以使用自己的 Azure Fluid Relay 服务？</b></summary>

可以！ 构造 `TeamsFluidClient` 类时，可以定义自己的 `AzureConnectionConfig`。 Live Share 将创建的容器与会议相关联，但需要实现 `ITokenProvider` 接口来为容器签名令牌。 例如，可以使用提供的 `AzureFunctionTokenProvider`，它使用 Azure 云函数从服务器请求访问令牌。

虽然大多数用户认为使用我们的免费托管服务非常有用，但有时仍可将自己的 Azure Fluid Relay 服务用于 Live Share 应用。 如果有以下事项，请考虑使用自定义 AFR 服务连接：

* 需要在会议生存期之后将数据存储在 Fluid 容器中。
* 通过需要自定义安全策略的服务传输敏感数据。
* 例如 `SharedMap`，通过 Fluid Framework 为 Teams 外部的应用程序开发功能。

有关详细信息，请参阅 [如何指导](./teams-live-share-how-to/how-to-custom-azure-fluid-relay.md) 或访问 [Azure Fluid Relay 文档](/azure/azure-fluid-relay/)。

<br>

</details>

<details>

<summary><b>Live Share 托管服务中存储的数据可访问多长时间？</b></summary>

可在 24 小时内访问通过 Live Share 托管的 Azure Fluid Relay 服务创建的 Fluid 容器发送或存储的任何数据。 如果希望将数据保留超过 24 小时，可以将托管的 Azure Fluid Relay 服务替换为你自己的服务。 或者，可以并行使用自己的存储服务提供商和 Live Share 托管服务。

<br>

</details>

<details>

<summary><b>Live Share 支持什么会议类型？</b></summary>

在预览期间，仅支持计划的会议，并且所有参与者都必须在会议日历上。 不支持一对一通话、群组呼叫、立即开会等会议类型。

<br>

</details>

<details>

<summary><b>Live Share 的媒体包是否适用于 DRM 内容？</b></summary>

否。 Teams 目前不支持桌面上选项卡应用程序的加密媒体。 支持 Chrome、Edge 和移动客户端。 有关详细信息，可以 [在此处跟踪问题](https://github.com/microsoft/live-share-sdk/issues/14)。

<br>

</details>

<details>
<summary><b>多少人可以参加 Live Share 会话？</b></summary>

目前，Live Share 每个会话最多支持 100 名与会者。 如果这是你感兴趣的内容，可以 [在此处开始讨论](https://github.com/microsoft/live-share-sdk/discussions)。

<br>

</details>

<details>
<summary><b>是否可以在 Teams 外部使用 Live Share 的临时数据结构？</b></summary>

目前，Live Share 包要求 Teams 客户端 SDK 正常运行。 `@microsoft/live-share` Microsoft Teams 外部的功能或`@microsoft/live-share-media`不起作用。 如果这是你感兴趣的内容，可以 [在此处开始讨论](https://github.com/microsoft/live-share-sdk/discussions)。

<br>

</details>

<details>
<summary><b>是否可以使用多个 Fluid 容器？</b></summary>

目前，Live Share 仅支持使用我们提供的 Azure Fluid Relay 服务创建一个容器。 但是，可以同时使用 Live Share 容器和由自己的 Azure Fluid Relay 实例创建的容器。

<br>

</details>

<details>
<summary><b>是否可以在创建容器后更改 Fluid 容器架构？</b></summary>

目前，Live Share 不支持在创建或加入容器后向 Fluid `ContainerSchema` 添加新`initialObjects`功能。 由于 Live Share 会话生存期较短，因此在将新功能添加到应用后，这通常是开发过程中出现的问题。

> [!NOTE]
> 如果在其中使用该 `dynamicObjectTypes` 属性 `ContainerSchema`，则可以在任何时候添加新类型。 如果以后从架构中删除类型，这些类型的现有 DDS 实例将正常失败。

若要 `initialObjects` 修复在浏览器中本地测试时更改导致的错误，请从 URL 中删除哈希容器 ID 并重新加载页面。 如果在 Teams 会议中进行测试，请启动新会议并重试。

如果计划频繁更新新应用 `SharedObject` 或 `EphemeralObject` 实例，应考虑如何将新架构更改部署到生产环境。 虽然实际风险相对较低且持续时间较短，但推出更改时可能会有活动会话。 会话中的现有用户不应受到影响，但部署中断性更改后加入该会话的用户在连接到会话时可能会遇到问题。 若要缓解此问题，可以考虑以下一些解决方案：

* 在正常工作时间之外为 Web 应用程序部署架构更改。
* 用于 `dynamicObjectTypes` 对架构所做的任何更改，而不是更改 `initialObjects`。

> [!NOTE]
> Live Share 目前不支持版本控制 `ContainerSchema`，也不支持任何专用于迁移的 API。

<br>

</details>

<details>
<summary><b>可以通过 Live Share 发出的更改事件数量是否有限制？</b></summary>

虽然 Live Share 处于预览状态，但不会强制执行通过 Live Share 发出的任何事件限制。 为了获得最佳性能，必须将通过 `SharedObject` 或 `EphemeralObject` 实例发出的更改取消为每 50 毫秒或更长一条消息。 在基于鼠标或触摸坐标发送更改（例如同步光标位置、墨迹书写和在页面周围拖动对象时）时，这一点尤为重要。

<br>

</details>

## <a name="have-more-questions-or-feedback"></a>有更多问题或反馈？

将问题和功能请求提交到适用于 [Live Share SDK](https://github.com/microsoft/live-share-sdk) 的 SDK 存储库。 使用 `live-share` 和 `microsoft-teams` 标记在 [Stack Overflow](https://stackoverflow.com/questions/tagged/live-share+microsoft-teams) 发布有关 SDK 的操作方法问题。

## <a name="see-also"></a>另请参阅

* [GitHub 存储库](https://github.com/microsoft/live-share-sdk)
* [Live Share SDK 参考文档](/javascript/api/@microsoft/live-share/)
* [Live Share 媒体 SDK 参考文档](/javascript/api/@microsoft/live-share-media/)
* [会议中的 Teams 应用](teams-apps-in-meetings.md)
