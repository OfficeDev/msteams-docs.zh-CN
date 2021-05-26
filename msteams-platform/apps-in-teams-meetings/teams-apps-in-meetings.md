---
title: 会议Teams应用程序
author: laujan
description: 基于参与者和用户Teams会议的应用概述
ms.topic: overview
ms.author: lajanuar
localization_priority: Normal
keywords: teams 应用会议用户参与者角色 api
ms.openlocfilehash: 1fdf3d55219d80d6953ffa0865b223dd626053f6
ms.sourcegitcommit: 999f5c607671e088ea8a461fa7dbb63f8d61c39b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2021
ms.locfileid: "52649662"
---
# <a name="apps-for-teams-meetings"></a><span data-ttu-id="de2fd-104">会议Teams应用程序</span><span class="sxs-lookup"><span data-stu-id="de2fd-104">Apps for Teams meetings</span></span>

<span data-ttu-id="de2fd-105">会议支持协作、合作关系、明智沟通和在非独占活动论坛中共享反馈。</span><span class="sxs-lookup"><span data-stu-id="de2fd-105">Meetings enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="de2fd-106">会议应用可以针对会议生命周期的每个阶段提供用户体验，包括会议前、会议内和会议后应用体验，具体取决于与会者的状态。</span><span class="sxs-lookup"><span data-stu-id="de2fd-106">The meeting app can deliver a user experience for each stage of the meeting lifecycle including pre-meeting, in-meeting, and post-meeting app experience, depending on the attendee's status.</span></span>

<span data-ttu-id="de2fd-107">用户可以在会议期间使用选项卡库访问应用，例如：</span><span class="sxs-lookup"><span data-stu-id="de2fd-107">The users can access apps during meetings using the tab gallery, for example:</span></span>

* <span data-ttu-id="de2fd-108">预先阶段一个看板板。</span><span class="sxs-lookup"><span data-stu-id="de2fd-108">Pre-stage a Kanban board.</span></span>
* <span data-ttu-id="de2fd-109">启动会议内可操作对话框。</span><span class="sxs-lookup"><span data-stu-id="de2fd-109">Launch an in-meeting actionable dialog.</span></span>
* <span data-ttu-id="de2fd-110">创建会议后调查。</span><span class="sxs-lookup"><span data-stu-id="de2fd-110">Create a post-meeting survey.</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/nKAy5rNDus4]

<span data-ttu-id="de2fd-111">本文概述了会议应用的可扩展性、API 引用、为会议启用和配置应用，以及会议Teams。</span><span class="sxs-lookup"><span data-stu-id="de2fd-111">This article provides an overview of meeting app extensibility, API references, enable and configure apps for meetings, and Together Mode in Teams.</span></span>

<span data-ttu-id="de2fd-112">可以使用会议可扩展性功能增强会议体验，该功能使您能够将应用集成到会议中。</span><span class="sxs-lookup"><span data-stu-id="de2fd-112">You can enhance your meeting experience by using the meeting extensibility feature, which enables you to integrate your apps within meetings.</span></span> <span data-ttu-id="de2fd-113">它还包括会议生命周期的不同阶段，可在其中集成选项卡、聊天机器人和消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="de2fd-113">It also includes different stages of a meeting lifecycle, where you can integrate tabs, bots, and messaging extensions.</span></span> <span data-ttu-id="de2fd-114">使用会议扩展性 API，可以标识不同的参与者角色和用户类型、获取会议事件、生成会议内对话框等。</span><span class="sxs-lookup"><span data-stu-id="de2fd-114">With meetings extensibility APIs, you can identify different participant roles and user types, get meeting events, generate in-meeting dialogs, and so on.</span></span>

<span data-ttu-id="de2fd-115">若要Teams会议应用自定义应用，可以通过更新应用清单为 Teams 会议启用应用，还可以为会议方案配置应用。</span><span class="sxs-lookup"><span data-stu-id="de2fd-115">To customize Teams with apps for meetings, you can enable your apps for Teams meetings by updating your app manifest and you can also configure your apps for meeting scenarios.</span></span>

<span data-ttu-id="de2fd-116">新的"共同模式"功能使用户能够在一个地方与团队一起在一个会议中协作，而无需使用方框分隔。</span><span class="sxs-lookup"><span data-stu-id="de2fd-116">The new Together Mode feature enables users to collaborate in a meeting with their team in one place without being separated by boxes.</span></span>

## <a name="see-also"></a><span data-ttu-id="de2fd-117">另请参阅</span><span class="sxs-lookup"><span data-stu-id="de2fd-117">See also</span></span>

* [<span data-ttu-id="de2fd-118">Tab</span><span class="sxs-lookup"><span data-stu-id="de2fd-118">Tab</span></span>](../tabs/what-are-tabs.md#understand-how-tabs-work)
* [<span data-ttu-id="de2fd-119">机器人</span><span class="sxs-lookup"><span data-stu-id="de2fd-119">Bot</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="de2fd-120">消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="de2fd-120">Messaging extension</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="de2fd-121">设计应用</span><span class="sxs-lookup"><span data-stu-id="de2fd-121">Design your app</span></span>](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [<span data-ttu-id="de2fd-122">会议应用的先决条件和 API Teams参考</span><span class="sxs-lookup"><span data-stu-id="de2fd-122">Prerequisites and API references for apps in Teams meetings</span></span>](create-apps-for-teams-meetings.md)
* [<span data-ttu-id="de2fd-123">一起模式</span><span class="sxs-lookup"><span data-stu-id="de2fd-123">Together Mode</span></span>](~/apps-in-teams-meetings/teams-together-mode.md)

## <a name="next-step"></a><span data-ttu-id="de2fd-124">后续步骤</span><span class="sxs-lookup"><span data-stu-id="de2fd-124">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="de2fd-125">会议应用程序扩展性</span><span class="sxs-lookup"><span data-stu-id="de2fd-125">Meeting app extensibility</span></span>](meeting-app-extensibility.md)
