---
title: 测试应用概述
description: 介绍在自定义应用中Teams自定义应用Microsoft 365
ms.topic: how-to
localization_priority: Normal
keywords: 配置Microsoft 365测试Teams租户配置
ms.openlocfilehash: 37f917727aba1a0f9828434b1519b4bb787df7aa
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631004"
---
# <a name="test-your-app"></a><span data-ttu-id="fe6a5-104">测试应用</span><span class="sxs-lookup"><span data-stu-id="fe6a5-104">Test your app</span></span>

<span data-ttu-id="fe6a5-105">将应用与Microsoft Teams集成后，必须在发布应用之前测试它。</span><span class="sxs-lookup"><span data-stu-id="fe6a5-105">After integrating your app with Microsoft Teams, you must test your app before publishing it.</span></span> <span data-ttu-id="fe6a5-106">因此，最终目标是为你的应用获取数量多的用户，因此，请确保在用户可以使用的多个设备上测试该应用。</span><span class="sxs-lookup"><span data-stu-id="fe6a5-106">The ultimate goal is to get as many users for your app, therefore, ensure to test the app on multiple devices that users could use.</span></span> <span data-ttu-id="fe6a5-107">对于测试你的应用：</span><span class="sxs-lookup"><span data-stu-id="fe6a5-107">For testing your app:</span></span>

* <span data-ttu-id="fe6a5-108">准备Microsoft 365租户。</span><span class="sxs-lookup"><span data-stu-id="fe6a5-108">Prepare your Microsoft 365 tenant.</span></span>
* <span data-ttu-id="fe6a5-109">选择一个工作区来测试和调试你的应用。</span><span class="sxs-lookup"><span data-stu-id="fe6a5-109">Choose a workspace to test and debug your app.</span></span>
* <span data-ttu-id="fe6a5-110">将测试数据添加到Microsoft 365租户。</span><span class="sxs-lookup"><span data-stu-id="fe6a5-110">Add test data to your Microsoft 365 tenant.</span></span>

## <a name="prepare-your-microsoft-365-tenant"></a><span data-ttu-id="fe6a5-111">准备 Microsoft 365 租户</span><span class="sxs-lookup"><span data-stu-id="fe6a5-111">Prepare your Microsoft 365 tenant</span></span>

<span data-ttu-id="fe6a5-112">在开始测试应用之前，请准备Microsoft 365测试租户并启用Teams应用，以便上传应用。</span><span class="sxs-lookup"><span data-stu-id="fe6a5-112">Before you start testing your app, prepare your Microsoft 365 test tenant and enable custom Teams app allow you to upload your app.</span></span> <span data-ttu-id="fe6a5-113">必须注册开发人员Microsoft 365并管理组织的 Teams 设置。</span><span class="sxs-lookup"><span data-stu-id="fe6a5-113">You must sign-up for Microsoft 365 developer program and manage the Teams settings for your organization.</span></span> <span data-ttu-id="fe6a5-114">设置开发人员订阅并通过准备你的租户Microsoft 365[订阅](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="fe6a5-114">Set up your developer subscription and configure it through [prepare your Microsoft 365 Tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

## <a name="test-and-debug"></a><span data-ttu-id="fe6a5-115">测试和调试</span><span class="sxs-lookup"><span data-stu-id="fe6a5-115">Test and debug</span></span>

<span data-ttu-id="fe6a5-116">若要测试和调试应用，必须创建至少一个工作区。</span><span class="sxs-lookup"><span data-stu-id="fe6a5-116">To test and debug your app, you must create at least one workspace.</span></span> <span data-ttu-id="fe6a5-117">可以选择测试设置，如本地主机或基于云的主机，以测试和调试应用。</span><span class="sxs-lookup"><span data-stu-id="fe6a5-117">You can select a test setup, such as local host or cloud-based host to test and debug the app.</span></span> <span data-ttu-id="fe6a5-118">提供了调试Teams应用以加载和运行应用体验的指南。</span><span class="sxs-lookup"><span data-stu-id="fe6a5-118">Guidance to debug your Teams app is provided to load and run your app experience.</span></span> <span data-ttu-id="fe6a5-119">有关详细信息，请参阅[选择设置并运行Microsoft Teams应用](~/concepts/build-and-test/debug.md)。</span><span class="sxs-lookup"><span data-stu-id="fe6a5-119">For more information, see [choose a set up and run your Microsoft Teams app](~/concepts/build-and-test/debug.md).</span></span>

<span data-ttu-id="fe6a5-120">在本地测试机器人。</span><span class="sxs-lookup"><span data-stu-id="fe6a5-120">Test your bot locally.</span></span> <span data-ttu-id="fe6a5-121">有关详细信息，请参阅使用 [IDE 在本地调试机器人](~/bots/how-to/debug/locally-with-an-ide.md)。</span><span class="sxs-lookup"><span data-stu-id="fe6a5-121">For more information, see [debug your bot locally with an IDE](~/bots/how-to/debug/locally-with-an-ide.md).</span></span> <span data-ttu-id="fe6a5-122">您还可以使用检查中间件和自适应 [工具](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) 调试 [自动程序](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="fe6a5-122">You can also debug your bot with [inspection middleware](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) and [adaptive tools](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true).</span></span> 

<span data-ttu-id="fe6a5-123">若要查看控制台日志，请在运行时查看或修改 html、css 和网络请求，向 JavaScript 代码添加断点，并执行交互式调试访问 DevTools。</span><span class="sxs-lookup"><span data-stu-id="fe6a5-123">To view the console logs, view or modify html, css, and network requests during runtime, add breakpoints to your JavaScript code, and perform interactive debugging access the DevTools.</span></span> <span data-ttu-id="fe6a5-124">有关详细信息，请参阅[Access the DevTools for Teams tabs](~/tabs/how-to/developer-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="fe6a5-124">For more information, see [Access the DevTools for Teams tabs](~/tabs/how-to/developer-tools.md).</span></span> 

## <a name="add-test-data-to-your-microsoft-365-tenant"></a><span data-ttu-id="fe6a5-125">将测试数据添加到Microsoft 365租户</span><span class="sxs-lookup"><span data-stu-id="fe6a5-125">Add test data to your Microsoft 365 tenant</span></span>

<span data-ttu-id="fe6a5-126">将测试数据添加到Microsoft 365租户。</span><span class="sxs-lookup"><span data-stu-id="fe6a5-126">Add the test data to Microsoft 365 test tenant.</span></span> <span data-ttu-id="fe6a5-127">有关详细信息，请参阅[将测试数据添加到](~/concepts/build-and-test/test-data.md)Office 365 测试租户，并完成所有先决条件，然后再开始上载测试数据。</span><span class="sxs-lookup"><span data-stu-id="fe6a5-127">For more information, see [add test data to your Office 365 test tenant](~/concepts/build-and-test/test-data.md), and complete all the prerequisites before you start uploading your test data.</span></span>

## <a name="see-also"></a><span data-ttu-id="fe6a5-128">另请参阅</span><span class="sxs-lookup"><span data-stu-id="fe6a5-128">See also</span></span>

* [<span data-ttu-id="fe6a5-129">调试选项卡</span><span class="sxs-lookup"><span data-stu-id="fe6a5-129">Debug your tab</span></span>](~/tabs/how-to/developer-tools.md)
* [<span data-ttu-id="fe6a5-130">调试机器人</span><span class="sxs-lookup"><span data-stu-id="fe6a5-130">Debug your bots</span></span>](~/bots/how-to/debug/locally-with-an-ide.md)
* [<span data-ttu-id="fe6a5-131">测试 RSC 权限</span><span class="sxs-lookup"><span data-stu-id="fe6a5-131">Test RSC permissions</span></span>](~/graph-api/rsc/test-resource-specific-consent.md)

## <a name="next-step"></a><span data-ttu-id="fe6a5-132">后续步骤</span><span class="sxs-lookup"><span data-stu-id="fe6a5-132">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fe6a5-133">准备 Microsoft 365 租户</span><span class="sxs-lookup"><span data-stu-id="fe6a5-133">Prepare your Microsoft 365 tenant</span></span>](~/concepts/build-and-test/prepare-your-o365-tenant.md)
