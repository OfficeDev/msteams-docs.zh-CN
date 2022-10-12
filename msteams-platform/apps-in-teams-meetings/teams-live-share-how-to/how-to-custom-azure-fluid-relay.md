---
title: 如何使用自定义 Azure Fluid Relay 服务
author: surbhigupta
description: 在本模块中，了解如何将自定义 Azure Fluid Relay 服务与 Live Share 配合使用。
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 07/21/2022
ms.openlocfilehash: b8bec005450515fbef7dfb60e58fac1325235b62
ms.sourcegitcommit: 0fa0bc081da05b2a241fd8054488d9fd0104e17b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2022
ms.locfileid: "68552516"
---
---

# <a name="custom-azure-fluid-relay-service"></a>自定义 Azure Fluid Relay 服务

虽然你可能更喜欢使用我们的免费托管服务，但在某些情况下，将自己的 Azure Fluid Relay 服务用于 Live Share 应用是有益的。

## <a name="pre-requisites"></a>先决条件

1. 生成会议侧面板和阶段应用会议扩展，如 [骰子滚筒教程](../teams-live-share-tutorial.md)中所示。
2. 更新应用清单以包含所有 [必要的权限](../teams-live-share-capabilities.md#register-rsc-permissions)。
3. 预配 Azure Fluid Relay 服务，如本 [教程](/azure/azure-fluid-relay/how-tos/provision-fluid-azure-portal)中所述。

## <a name="connect-to-azure-fluid-relay-service"></a>连接到 Azure Fluid Relay 服务

调用初始化 `LiveShareClient`时，可以定义你自己的 `AzureConnectionConfig`。 Live Share 将创建的容器与会议相关联，但需要实现 `ITokenProvider` 接口来为容器签名令牌。 本示例介绍 Azure， `AzureFunctionTokenProvider`它使用 Azure 云函数从服务器请求访问令牌。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient, LivePresence } from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";
import { AzureFunctionTokenProvider } from "@fluidframework/azure-client";

// Define a custom connection for your app
const options = {
  connection: {
    tenantId: "MY_TENANT_ID",
    tokenProvider: new AzureFunctionTokenProvider(
      "MY_SERVICE_ENDPOINT_URL" + "/api/GetAzureToken",
      { userId: "userId", userName: "Test User" }
    ),
    endpoint: "MY_SERVICE_ENDPOINT_URL",
    type: "remote",
  },
};
// Join the Fluid container
const liveShare = new LiveShareClient(options);
const schema = {
  initialObjects: {
    presence: LivePresence,
    ticTacToePositions: SharedMap,
  },
};
const { container } = await liveShare.joinContainer(schema);

// ... ready to start app sync logic
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import {
  LiveShareClient,
  ILiveShareClientOptions,
  LivePresence,
} from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";
import { AzureFunctionTokenProvider } from "@fluidframework/azure-client";

// Define a custom connection for your app
const options: ILiveShareClientOptions = {
  connection: {
    tenantId: "MY_TENANT_ID",
    tokenProvider: new AzureFunctionTokenProvider(
      "MY_FUNCTION_ENDPOINT_URL" + "/api/GetAzureToken",
      { userId: "userId", userName: "Test User" }
    ),
    endpoint: "MY_SERVICE_ENDPOINT_URL",
    type: "remote",
  },
};
// Join the Fluid container
const liveShare = new LiveShareClient(options);
const schema = {
  initialObjects: {
    presence: LivePresence,
    ticTacToePositions: SharedMap,
  },
};
const { container } = await liveShare.joinContainer(schema);

// ... ready to start app sync logic
```

---

## <a name="why-use-a-custom-azure-fluid-relay-service"></a>为何使用自定义 Azure Fluid Relay 服务？

如果有以下事项，请考虑使用自定义 AFR 服务连接：

* 需要在会议生存期之后将数据存储在 Fluid 容器中。
* 通过需要自定义安全策略的服务传输敏感数据。
* 通过 Fluid Framework 为 Teams 外部的应用程序开发功能。

## <a name="why-use-live-share-with-your-custom-service"></a>为什么要将 Live Share 与自定义服务配合使用？

Azure Fluid Relay 设计用于任何基于 Web 的应用程序，这意味着它适用于或不适用于 Microsoft Teams。 这引发了一个重要的问题：如果我构建自己的 Azure Fluid Relay 服务，是否仍需要 Live Share？

Live Share 具有对增强应用中其他功能的常见会议方案有益的功能，包括：

* [容器映射](#container-mapping)
* [实时对象和角色验证](#live-objects-and-role-verification)
* [媒体同步](#media-synchronization)

### <a name="container-mapping"></a>容器映射

In `LiveShareClient` `@microsoft/live-share` 负责将唯一会议标识符映射到 Fluid 容器，这可确保所有会议参与者都加入同一容器。 在此过程中，客户端尝试连接到 `containerId` 映射到已存在的会议。 如果其中一个不存在， `AzureClient` 则用于使用你 `AzureConnectionConfig` 创建容器，然后将该 `containerId` 容器中继给其他会议参与者。

如果你的应用已有一种机制来创建 Fluid 容器并将其共享给其他成员，例如插入 `containerId` 到共享到会议阶段的 URL，则应用可能不需要这样做。

### <a name="live-objects-and-role-verification"></a>实时对象和角色验证

Live Share 的实时数据结构（例如`LivePresence``LiveState``LiveEvent`）是为会议中的协作量身定制的，因此在 Microsoft Teams 外部使用的 Fluid 容器中不受支持。 角色验证等功能可帮助应用符合用户的期望。

> [!NOTE]
> 此外，与传统的 Fluid 数据结构相比，实时对象还具有更快的消息延迟。

有关详细信息，请参阅 [核心功能](../teams-live-share-capabilities.md) 页。

### <a name="media-synchronization"></a>媒体同步

Microsoft Teams 外部使用的 Fluid 容器不支持来自 `@microsoft/live-share-media` 的包。

有关详细信息，请参阅 [媒体功能](../teams-live-share-media-capabilities.md) 页。

## <a name="see-also"></a>另请参阅

* [GitHub 存储库](https://github.com/microsoft/live-share-sdk)
* [Live Share SDK 参考文档](/javascript/api/@microsoft/live-share/)
* [Live Share 媒体 SDK 参考文档](/javascript/api/@microsoft/live-share-media/)
* [Live Share 功能](../teams-live-share-capabilities.md)
* [Live Share 媒体功能](../teams-live-share-media-capabilities.md)
* [Live Share 常见问题解答](../teams-live-share-faq.md)
* [会议中的 Teams 应用](../teams-apps-in-meetings.md)
