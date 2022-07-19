---
title: Live Share 常见问题解答
author: surbhigupta
description: 在本模块中，详细了解 Live Share 常见问题解答。
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: d29318397e388faca93695040914493ecae369a5
ms.sourcegitcommit: 79d525c0be309200e930cdd942bc2c753d0b718c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2022
ms.locfileid: "66841867"
---
---

# <a name="live-share-sdk-faq"></a>Live Share SDK 常见问题解答

获取使用 Live Share 时常见问题的解答。<br>

<br>

<details>

<summary><b>我是否可以使用自己的 Azure Fluid Relay 服务？</b></summary>

是。 构造 `TeamsFluidClient` 类时，可以定义自己的 `AzureConnectionConfig`。 Live Share 将创建的容器与会议相关联，但需要创建自己的 Azure `ITokenProvider` 才能为容器和区域要求签名令牌。 有关详细信息，请参阅 Azure [Fluid Relay 文档](/azure/azure-fluid-relay/)。

<br>

</details>

<details>

<summary><b>Live Share 托管服务中存储的数据可访问多长时间？</b></summary>

可在 24 小时内访问通过 Live Share 托管的 Azure Fluid Relay 服务创建的 Fluid 容器发送或存储的任何数据。 如果希望将数据保留超过 24 小时，可以将托管的 Azure Fluid Relay 服务替换为你自己的服务。 或者，可以并行使用自己的存储服务提供商和 Live Share 托管服务。

<br>

</details>

<details>

<summary><b>Live Share 支持什么会议类型？</b></summary>

目前，仅支持计划的会议，并且所有参与者都必须在会议日历上。 不支持一对一通话、群组呼叫、立即开会等会议类型。

<br>

</details>

<details>

<summary><b>Live Share 的媒体包是否适用于 DRM 内容？</b></summary>

否。 Teams 目前不支持 Tab 应用程序的加密媒体。

<br>

</details>

<details>
<summary><b>多少人可以参加 Live Share 会话？</b></summary>

目前，Live Share 每个会话最多支持 100 名与会者。

<br>

</details>

## <a name="have-more-questions-or-feedback"></a>有更多问题或反馈？

将问题和功能请求提交到适用于 [Live Share SDK](https://github.com/microsoft/live-share-sdk) 的 SDK 存储库。 使用 `live-share` 和 `microsoft-teams` 标记在 [Stack Overflow](https://stackoverflow.com/questions/tagged/live-share+microsoft-teams) 发布有关 SDK 的操作方法问题。

## <a name="see-also"></a>另请参阅

- [GitHub 存储库](https://github.com/microsoft/live-share-sdk)
- [Live Share SDK 参考文档](/javascript/api/@microsoft/live-share/)
- [Live Share 媒体 SDK 参考文档](/javascript/api/@microsoft/live-share-media/)
- [会议中的 Teams 应用](teams-apps-in-meetings.md)
