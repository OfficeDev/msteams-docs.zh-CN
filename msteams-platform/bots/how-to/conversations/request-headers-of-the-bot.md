---
title: 将租户 ID 和对话 ID 发送到机器人的请求标头
description: 介绍如何将租户 ID 和对话 ID 发送到机器人的请求标头。
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 76f667453114ab202d43217b9a4c01a6d14cc1a8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565891"
---
# <a name="send-tenant-id-and-conversation-id-to-the-request-headers-of-the-bot"></a><span data-ttu-id="de39b-103">将租户 ID 和对话 ID 发送到机器人的请求标头</span><span class="sxs-lookup"><span data-stu-id="de39b-103">Send tenant ID and conversation ID to the request headers of the bot</span></span>

<span data-ttu-id="de39b-104">当前向自动程序发出的传出请求在标头或 URL 中不包含任何有助于机器人在不解压缩整个负载的情况下路由流量的信息。</span><span class="sxs-lookup"><span data-stu-id="de39b-104">The current outgoing requests to the bot do not contain in the header or URL any information that helps bots route the traffic without unpacking the entire payload.</span></span> <span data-ttu-id="de39b-105">活动通过类似于 https：//<your_domain>/api/messages 的 URL 发送给机器人。</span><span class="sxs-lookup"><span data-stu-id="de39b-105">The activities are sent to the bot through a URL similar to https://<your_domain>/api/messages.</span></span> <span data-ttu-id="de39b-106">收到在标头中显示对话 ID 和租户 ID 的请求。</span><span class="sxs-lookup"><span data-stu-id="de39b-106">Requests are received to show the conversation ID and tenant ID in the headers.</span></span>

## <a name="request-header-fields"></a><span data-ttu-id="de39b-107">请求头字段</span><span class="sxs-lookup"><span data-stu-id="de39b-107">Request header fields</span></span>

<span data-ttu-id="de39b-108">对于异步流和同步流，两个非标准请求头字段将添加到发送到自动程序的所有请求中。</span><span class="sxs-lookup"><span data-stu-id="de39b-108">Two non-standard request header fields are added to all the requests sent to bots, for both asynchronous flow and synchronous flow.</span></span> <span data-ttu-id="de39b-109">下表提供了请求标头字段及其值：</span><span class="sxs-lookup"><span data-stu-id="de39b-109">The following table provides the request header fields and their values:</span></span>

| <span data-ttu-id="de39b-110">字段键</span><span class="sxs-lookup"><span data-stu-id="de39b-110">Field key</span></span> | <span data-ttu-id="de39b-111">值</span><span class="sxs-lookup"><span data-stu-id="de39b-111">Value</span></span> |
|----------------|-----------------|
| <span data-ttu-id="de39b-112">x-ms-conversation-id</span><span class="sxs-lookup"><span data-stu-id="de39b-112">x-ms-conversation-id</span></span> | <span data-ttu-id="de39b-113">与请求活动对应的对话 ID（如果适用，经确认或验证）。</span><span class="sxs-lookup"><span data-stu-id="de39b-113">The conversation ID corresponding to the request activity if applicable and confirmed or verified.</span></span> |
| <span data-ttu-id="de39b-114">x-ms-tenant-id</span><span class="sxs-lookup"><span data-stu-id="de39b-114">x-ms-tenant-id</span></span> | <span data-ttu-id="de39b-115">与请求活动中的对话对应的租户 ID。</span><span class="sxs-lookup"><span data-stu-id="de39b-115">The tenant ID corresponding to the conversation in the request activity.</span></span> |

<span data-ttu-id="de39b-116">如果租户或对话 ID 不存在于活动中，或者未在服务端进行验证，则值为空。</span><span class="sxs-lookup"><span data-stu-id="de39b-116">If the tenant or conversation ID is not present in the activity or was not validated on the service side, the value is empty.</span></span>

![请求头字段](~/assets/images/bots/requestheaderfields.png)
