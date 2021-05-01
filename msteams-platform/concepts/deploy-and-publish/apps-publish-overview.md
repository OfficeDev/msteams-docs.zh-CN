---
title: 概述 - 分发应用
description: 介绍发布应用Microsoft Teams选项。
ms.topic: conceptual
author: KirtiPereira
ms.author: surbhigupta
ms.openlocfilehash: 81a266d0bdaf2a65651dc1beca171b72cf1a20a6
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101870"
---
# <a name="distribute-your-microsoft-teams-app"></a><span data-ttu-id="dc8cf-103">分发Microsoft Teams应用</span><span class="sxs-lookup"><span data-stu-id="dc8cf-103">Distribute your Microsoft Teams app</span></span>

<span data-ttu-id="dc8cf-104">你可以向Microsoft Teams、团队、组织或想要使用它的任何人提供你的应用。</span><span class="sxs-lookup"><span data-stu-id="dc8cf-104">You can provide your Microsoft Teams app to an individual, team, organization, or anyone who wants to use it.</span></span> <span data-ttu-id="dc8cf-105">分配方式取决于多个因素，包括用户需求、业务和技术要求以及应用的目标。</span><span class="sxs-lookup"><span data-stu-id="dc8cf-105">How you distribute depends on several factors, including users' needs, business and technical requirements, and your goals for the app.</span></span>

## <a name="upload-your-app-in-teams"></a><span data-ttu-id="dc8cf-106">Upload应用Teams</span><span class="sxs-lookup"><span data-stu-id="dc8cf-106">Upload your app in Teams</span></span>

<span data-ttu-id="dc8cf-107">旁加载应用供个人使用、与团队协作或测试和调试。</span><span class="sxs-lookup"><span data-stu-id="dc8cf-107">Sideload an app for personal use, collaborating with your team, or testing and debugging.</span></span> <span data-ttu-id="dc8cf-108">这种分发不需要正式的审阅过程。</span><span class="sxs-lookup"><span data-stu-id="dc8cf-108">This kind of distribution doesn't require a formal review process.</span></span>

<span data-ttu-id="dc8cf-109">有关详细信息，请参阅上传[应用Teams。](apps-upload.md)</span><span class="sxs-lookup"><span data-stu-id="dc8cf-109">For more information, see [upload your app in Teams](apps-upload.md).</span></span>

## <a name="publish-your-app-to-your-org"></a><span data-ttu-id="dc8cf-110">将应用发布到组织</span><span class="sxs-lookup"><span data-stu-id="dc8cf-110">Publish your app to your org</span></span>

<span data-ttu-id="dc8cf-111">使你的应用可供组织中的人员使用。此类分发需要Teams管理员的批准。</span><span class="sxs-lookup"><span data-stu-id="dc8cf-111">Make your app available to people in your org. This kind of distribution requires your Teams admin's approval.</span></span>

<span data-ttu-id="dc8cf-112">有关详细信息，请参阅在管理[中心管理Teams应用](https://docs.microsoft.com/MicrosoftTeams/manage-apps?toc=%2Fmicrosoftteams%2Fplatform%2Ftoc.json&bc=%2FMicrosoftTeams%2Fbreadcrumb%2Ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="dc8cf-112">For more information, see [manage your apps in the Teams admin center](https://docs.microsoft.com/MicrosoftTeams/manage-apps?toc=%2Fmicrosoftteams%2Fplatform%2Ftoc.json&bc=%2FMicrosoftTeams%2Fbreadcrumb%2Ftoc.json).</span></span>

### <a name="government-community-cloud-gcc-organizations"></a><span data-ttu-id="dc8cf-113">政府社区云 (GCC) 组织</span><span class="sxs-lookup"><span data-stu-id="dc8cf-113">Government Community Cloud (GCC) organizations</span></span>

<span data-ttu-id="dc8cf-114">在GCC Teams环境中，默认情况下会启用合规的 Microsoft 应用。</span><span class="sxs-lookup"><span data-stu-id="dc8cf-114">In GCC Teams environments, compliant Microsoft apps are enabled by default.</span></span> <span data-ttu-id="dc8cf-115">但是，在发布应用之前，请确保应用的所有终结点都GCC组织的要求。</span><span class="sxs-lookup"><span data-stu-id="dc8cf-115">Before publishing an app, however, make sure that all the app's endpoints comply with your GCC organization's requirements.</span></span>

> [!IMPORTANT]
><span data-ttu-id="dc8cf-116">如果你的应用包含自动程序或消息传递扩展，则必须在 Azure 中设置自动程序与 Teams 之间的通道时，选择"Microsoft Teams政府"选项。</span><span class="sxs-lookup"><span data-stu-id="dc8cf-116">If your app includes a bot or messaging extension, you must select the **Microsoft Teams for Government** option when setting up a channel between your bot and Teams in Azure.</span></span> <span data-ttu-id="dc8cf-117">有关详细信息，请参阅 [将机器人连接到频道](/azure/bot-service/bot-service-manage-channels?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="dc8cf-117">For more information, see [connect a bot to channels](/azure/bot-service/bot-service-manage-channels?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="publish-your-app-to-the-teams-store"></a><span data-ttu-id="dc8cf-118">将应用发布到应用商店Teams应用商店</span><span class="sxs-lookup"><span data-stu-id="dc8cf-118">Publish your app to the Teams store</span></span>

<span data-ttu-id="dc8cf-119">使应用可供所有人使用。</span><span class="sxs-lookup"><span data-stu-id="dc8cf-119">Make your app available to everyone.</span></span> <span data-ttu-id="dc8cf-120">此类分发需要 Microsoft 批准。</span><span class="sxs-lookup"><span data-stu-id="dc8cf-120">This kind of distribution requires Microsoft approval.</span></span>

<span data-ttu-id="dc8cf-121">有关详细信息，请参阅发布到[Teams 应用商店](~/concepts/deploy-and-publish/appsource/publish.md)。</span><span class="sxs-lookup"><span data-stu-id="dc8cf-121">For more information, see [publish to the Teams store](~/concepts/deploy-and-publish/appsource/publish.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="dc8cf-122">另请参阅</span><span class="sxs-lookup"><span data-stu-id="dc8cf-122">See also</span></span>

* [<span data-ttu-id="dc8cf-123">Microsoft 365 应用合规计划</span><span class="sxs-lookup"><span data-stu-id="dc8cf-123">Microsoft 365 App Compliance Program</span></span>](/microsoft-365-app-certification/overview)

## <a name="next-step"></a><span data-ttu-id="dc8cf-124">后续步骤</span><span class="sxs-lookup"><span data-stu-id="dc8cf-124">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dc8cf-125">创建应用包</span><span class="sxs-lookup"><span data-stu-id="dc8cf-125">Create your app package</span></span>](~/concepts/build-and-test/apps-package.md)
