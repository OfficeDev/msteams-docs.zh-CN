---
title: 了解 Teams 应用功能
author: heath-hamilton
description: 说明的 Teams 应用功能
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 5336b36b52cf81be414f18ccaaf9e235c079e626
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034703"
---
# <a name="understanding-teams-app-capabilities"></a><span data-ttu-id="01e33-103">了解 Teams 应用功能</span><span class="sxs-lookup"><span data-stu-id="01e33-103">Understanding Teams app capabilities</span></span>

<span data-ttu-id="01e33-104">*功能* 是构建 Microsoft Teams 平台上应用的扩展点。</span><span class="sxs-lookup"><span data-stu-id="01e33-104">*Capabilities* are the extension points for building apps on the Microsoft Teams platform.</span></span>

<span data-ttu-id="01e33-105">有多种方法可以扩展 Teams，因此每个应用都是独一无二的：一些应用只有一个 (如 webhook) ，而另一些则有一些可以为用户提供选项。</span><span class="sxs-lookup"><span data-stu-id="01e33-105">There are multiple ways to extend Teams, so every app is unique: Some only have one capability (such as a webhook), while others have a few to give users options.</span></span> <span data-ttu-id="01e33-106">例如，你的应用可以在中心位置显示数据 (选项卡) ，并通过对话界面 (自动程序) 。</span><span class="sxs-lookup"><span data-stu-id="01e33-106">For instance, your app could display data in a central location (tab) and present that same information through a conversational interface (bot).</span></span>

<span data-ttu-id="01e33-107">Teams 应用具有以下一项或全部核心功能：</span><span class="sxs-lookup"><span data-stu-id="01e33-107">Your Teams app have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="01e33-108">选项卡</span><span class="sxs-lookup"><span data-stu-id="01e33-108">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="01e33-109">消息扩展</span><span class="sxs-lookup"><span data-stu-id="01e33-109">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="01e33-110">机器人</span><span class="sxs-lookup"><span data-stu-id="01e33-110">Bots</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="01e33-111">Webhook 和连接器</span><span class="sxs-lookup"><span data-stu-id="01e33-111">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

<span data-ttu-id="01e33-112">你的应用还可以利用高级功能，例如适用于 Teams 的[Microsoft Graph API。](https://docs.microsoft.com/graph/teams-concept-overview)</span><span class="sxs-lookup"><span data-stu-id="01e33-112">Your app can also take advantage of advanced capabilities, such as the [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>

<span data-ttu-id="01e33-113">请参阅下图，了解哪些功能将提供你需要的应用功能。</span><span class="sxs-lookup"><span data-stu-id="01e33-113">See the following illustration to get an idea which capabilities would provide the features you want in your app.</span></span>

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="说明什么是 Teams 应用功能的&quot;心图&quot;。":::

## <a name="doing-whats-best-for-your-users"></a><span data-ttu-id="01e33-115">执行最适合用户的事情</span><span class="sxs-lookup"><span data-stu-id="01e33-115">Doing what's best for your users</span></span>

<span data-ttu-id="01e33-116">当你熟悉 Teams 应用开发时，你将开始了解它的细微之处。</span><span class="sxs-lookup"><span data-stu-id="01e33-116">As you familiarize yourself with Teams app development, you'll begin to understand its subtleties.</span></span> <span data-ttu-id="01e33-117">生成某些功能的方法 (例如收集用户输入) 。</span><span class="sxs-lookup"><span data-stu-id="01e33-117">There's more than one way to build certain features (such as collecting user input).</span></span> <span data-ttu-id="01e33-118">例如，可以使用 在选项卡中嵌入基于 Web 的表单 `<iframe>` 。</span><span class="sxs-lookup"><span data-stu-id="01e33-118">For example, you could embed a web-based form in a tab using an `<iframe>`.</span></span> <span data-ttu-id="01e33-119">您还可以使用任务模块（Teams UI 约定）在选项卡中完成此操作，以便获得用户可能喜欢的更本机体验。</span><span class="sxs-lookup"><span data-stu-id="01e33-119">You could also do this in a tab using a task module, a Teams UI convention, for a more native experience your users may prefer.</span></span>

<span data-ttu-id="01e33-120">选择正确的功能和设计需要首先 [了解受众的用例](../concepts/design/understand-use-cases.md)。</span><span class="sxs-lookup"><span data-stu-id="01e33-120">Choosing the right capabilities and design comes down to first [understanding your audience's use cases](../concepts/design/understand-use-cases.md).</span></span>
