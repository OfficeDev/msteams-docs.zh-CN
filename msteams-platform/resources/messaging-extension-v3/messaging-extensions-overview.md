---
title: 开发邮件扩展
description: 介绍如何在 Microsoft 团队中开始使用邮件扩展功能
keywords: 团队邮件传递扩展邮件扩展
ms.openlocfilehash: 6ba8f73d40f795a83f28707ef89c207c5d51d67c
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673022"
---
# <a name="develop-messaging-extensions-for-microsoft-teams"></a><span data-ttu-id="f29f2-104">为 Microsoft 团队开发邮件扩展</span><span class="sxs-lookup"><span data-stu-id="f29f2-104">Develop messaging extensions for Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="f29f2-105">邮件扩展是用户与 Microsoft 团队中的应用程序进行接洽的一种强大方式。</span><span class="sxs-lookup"><span data-stu-id="f29f2-105">Messaging extensions are a powerful way for users to engage with your app from Microsoft Teams.</span></span> <span data-ttu-id="f29f2-106">通过此功能，用户可以在服务中查询信息或向其发送信息，并将该信息以卡片形式发布到邮件中。</span><span class="sxs-lookup"><span data-stu-id="f29f2-106">With this capability, users can query or post information to and from your service and post that information, in the form of cards, right into a message.</span></span>

![邮件扩展卡的示例](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="f29f2-108">邮件扩展将沿着 "撰写" 框的底部显示。</span><span class="sxs-lookup"><span data-stu-id="f29f2-108">Messaging extensions appear along the bottom of the compose box.</span></span> <span data-ttu-id="f29f2-109">中内置了几个，如表情符号、Giphy 和不干胶标签。</span><span class="sxs-lookup"><span data-stu-id="f29f2-109">A few are built in, such as Emoji, Giphy, and Sticker.</span></span> <span data-ttu-id="f29f2-110">选择 "**更多选项**" （**&#8943;**）按钮以查看其他邮件扩展，包括从应用程序库添加的那些扩展或自行上载。</span><span class="sxs-lookup"><span data-stu-id="f29f2-110">Choose the **More Options** (**&#8943;**) button to see other messaging extensions, including those you add from the app gallery or upload yourself.</span></span>

<span data-ttu-id="f29f2-111">如何使用邮件扩展？</span><span class="sxs-lookup"><span data-stu-id="f29f2-111">How would you use messaging extensions?</span></span> <span data-ttu-id="f29f2-112">以下是几种可能的情况：</span><span class="sxs-lookup"><span data-stu-id="f29f2-112">Here are a few possibilities:</span></span>

* <span data-ttu-id="f29f2-113">工作项和 bug</span><span class="sxs-lookup"><span data-stu-id="f29f2-113">Work items and bugs</span></span>
* <span data-ttu-id="f29f2-114">客户支持票证</span><span class="sxs-lookup"><span data-stu-id="f29f2-114">Customer support tickets</span></span>
* <span data-ttu-id="f29f2-115">使用率图表和报告</span><span class="sxs-lookup"><span data-stu-id="f29f2-115">Usage charts and reports</span></span>
* <span data-ttu-id="f29f2-116">图像和媒体内容</span><span class="sxs-lookup"><span data-stu-id="f29f2-116">Images and media content</span></span>
* <span data-ttu-id="f29f2-117">销售机会和潜在客户</span><span class="sxs-lookup"><span data-stu-id="f29f2-117">Sales opportunities and leads</span></span>

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="f29f2-118">邮件扩展类型</span><span class="sxs-lookup"><span data-stu-id="f29f2-118">Types of messaging extensions</span></span>

<span data-ttu-id="f29f2-119">目前，可以为团队创建两种类型的邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="f29f2-119">There's primarily two kinds of messaging extensions you can create for Teams today.</span></span> <span data-ttu-id="f29f2-120">下列主题将指导您完成创建它们的过程：</span><span class="sxs-lookup"><span data-stu-id="f29f2-120">The following topics will guide you through the process of creating them:</span></span>

* <span data-ttu-id="f29f2-121">[基于搜索的邮件扩展](~/resources/messaging-extension-v3/search-extensions.md)：查询服务的信息并将其插入到邮件中。</span><span class="sxs-lookup"><span data-stu-id="f29f2-121">[Search based messaging extensions](~/resources/messaging-extension-v3/search-extensions.md): Query your service for information and insert that into a message.</span></span> <span data-ttu-id="f29f2-122">示例：查找工作项</span><span class="sxs-lookup"><span data-stu-id="f29f2-122">Example: Lookup a work item</span></span>
* <span data-ttu-id="f29f2-123">[基于操作的邮件扩展](~/resources/messaging-extension-v3/create-extensions.md)：收集用户的信息并发布到第三方服务。</span><span class="sxs-lookup"><span data-stu-id="f29f2-123">[Action-based messaging extensions](~/resources/messaging-extension-v3/create-extensions.md): Collect information from the user and post to a 3rd party service.</span></span> <span data-ttu-id="f29f2-124">示例：创建工作项</span><span class="sxs-lookup"><span data-stu-id="f29f2-124">Example: Create a work item</span></span>
