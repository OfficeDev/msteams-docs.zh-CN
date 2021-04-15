---
title: 开发消息传递扩展
description: 介绍如何在 Microsoft Teams 中开始使用消息传递扩展
ms.topic: overview
keywords: teams 消息传递扩展消息传递扩展
ms.openlocfilehash: 1eb75371b1a8adbeadbcbdbc0d06c7d88f2f1ccc
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696547"
---
# <a name="develop-messaging-extensions-for-microsoft-teams"></a><span data-ttu-id="05841-104">为 Microsoft Teams 开发消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="05841-104">Develop messaging extensions for Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="05841-105">消息传递扩展是用户从 Microsoft Teams 使用你的应用的强大方式。</span><span class="sxs-lookup"><span data-stu-id="05841-105">Messaging extensions are a powerful way for users to engage with your app from Microsoft Teams.</span></span> <span data-ttu-id="05841-106">通过此功能，用户可以在服务中查询或发布信息，然后以卡片形式将该信息发布至消息中。</span><span class="sxs-lookup"><span data-stu-id="05841-106">With this capability, users can query or post information to and from your service and post that information, in the form of cards, right into a message.</span></span>

![邮件扩展卡示例](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="05841-108">邮件扩展沿撰写框的底部显示。</span><span class="sxs-lookup"><span data-stu-id="05841-108">Messaging extensions appear along the bottom of the compose box.</span></span> <span data-ttu-id="05841-109">一些内置，如表情符号、Giphy 和贴纸。</span><span class="sxs-lookup"><span data-stu-id="05841-109">A few are built in, such as Emoji, Giphy, and Sticker.</span></span> <span data-ttu-id="05841-110">选择 **"更多选项**" (&#8943;) 查看其他消息传递扩展，包括从应用库添加或自己上传的邮件扩展。 </span><span class="sxs-lookup"><span data-stu-id="05841-110">Choose the **More Options** (**&#8943;**) button to see other messaging extensions, including those you add from the app gallery or upload yourself.</span></span>

<span data-ttu-id="05841-111">如何使用消息传递扩展？</span><span class="sxs-lookup"><span data-stu-id="05841-111">How would you use messaging extensions?</span></span> <span data-ttu-id="05841-112">下面提供了一些可能性：</span><span class="sxs-lookup"><span data-stu-id="05841-112">Here are a few possibilities:</span></span>

* <span data-ttu-id="05841-113">工作项和 Bug</span><span class="sxs-lookup"><span data-stu-id="05841-113">Work items and bugs</span></span>
* <span data-ttu-id="05841-114">客户支持票证</span><span class="sxs-lookup"><span data-stu-id="05841-114">Customer support tickets</span></span>
* <span data-ttu-id="05841-115">使用情况图表和报告</span><span class="sxs-lookup"><span data-stu-id="05841-115">Usage charts and reports</span></span>
* <span data-ttu-id="05841-116">图像和媒体内容</span><span class="sxs-lookup"><span data-stu-id="05841-116">Images and media content</span></span>
* <span data-ttu-id="05841-117">销售机会和潜在客户</span><span class="sxs-lookup"><span data-stu-id="05841-117">Sales opportunities and leads</span></span>

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="05841-118">邮件扩展类型</span><span class="sxs-lookup"><span data-stu-id="05841-118">Types of messaging extensions</span></span>

<span data-ttu-id="05841-119">目前，你主要为 Teams 创建两种类型的消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="05841-119">There's primarily two kinds of messaging extensions you can create for Teams today.</span></span> <span data-ttu-id="05841-120">以下主题将指导你完成创建它们的过程：</span><span class="sxs-lookup"><span data-stu-id="05841-120">The following topics will guide you through the process of creating them:</span></span>

* <span data-ttu-id="05841-121">[基于搜索的消息扩展](~/resources/messaging-extension-v3/search-extensions.md)：在服务中查询信息并将其插入到邮件中。</span><span class="sxs-lookup"><span data-stu-id="05841-121">[Search based messaging extensions](~/resources/messaging-extension-v3/search-extensions.md): Query your service for information and insert that into a message.</span></span> <span data-ttu-id="05841-122">示例：查找工作项</span><span class="sxs-lookup"><span data-stu-id="05841-122">Example: Lookup a work item</span></span>
* <span data-ttu-id="05841-123">[基于操作的消息扩展](~/resources/messaging-extension-v3/create-extensions.md)：从用户收集信息并张贴到第三方服务。</span><span class="sxs-lookup"><span data-stu-id="05841-123">[Action-based messaging extensions](~/resources/messaging-extension-v3/create-extensions.md): Collect information from the user and post to a 3rd party service.</span></span> <span data-ttu-id="05841-124">示例：创建工作项</span><span class="sxs-lookup"><span data-stu-id="05841-124">Example: Create a work item</span></span>
