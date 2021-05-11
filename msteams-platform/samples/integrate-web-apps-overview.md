---
title: 集成 web 应用
author: Rajeshwari-v
description: 将 Web 应用程序和设备功能与应用集成Microsoft Teams概述。
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 01977e22d79f7e39986367e647a2d48ea9b2905c
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058654"
---
# <a name="integrate-web-apps"></a><span data-ttu-id="85ecb-103">集成 web 应用</span><span class="sxs-lookup"><span data-stu-id="85ecb-103">Integrate web apps</span></span>

<span data-ttu-id="85ecb-104">通过将现有 Web 应用程序的功能集成到新平台，可以提供丰富的Microsoft Teams体验。</span><span class="sxs-lookup"><span data-stu-id="85ecb-104">You can provide an enriched user experience by integrating the features of an existing web application into Microsoft Teams platform.</span></span> <span data-ttu-id="85ecb-105">确保遵循[Teams准则](~/concepts/design/understand-use-cases.md)，使应用成为本机应用Teams。</span><span class="sxs-lookup"><span data-stu-id="85ecb-105">Ensure to follow [Teams design guidelines](~/concepts/design/understand-use-cases.md) to make your app native to Teams.</span></span>
<span data-ttu-id="85ecb-106">本文档概述了将 Web 应用程序与 Teams 集成的先决条件、用于创建 Power 应用、Power Virtual Agents、虚拟助手、应用模板、Shift 连接器、将 LmS、为您的网站创建"共享到 Teams"按钮、在 SharePoint 中添加 Microsoft Teams 选项卡、创建深层链接以及集成设备功能的先决条件。</span><span class="sxs-lookup"><span data-stu-id="85ecb-106">This document gives an overview of prerequisites to integrate web applications with Teams, Power platform to create Power apps, Power Virtual Agents, Virtual Assistant, app templates, Shift connectors, Moodle LMS, creating a Share-to-Teams button for your website, adding a Microsoft Teams tab in SharePoint, creating deep links, and integrating device capabilities.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85ecb-107">先决条件</span><span class="sxs-lookup"><span data-stu-id="85ecb-107">Prerequisites</span></span>   

<span data-ttu-id="85ecb-108">为了进行有效的集成，请确保更好地了解以下先决条件：</span><span class="sxs-lookup"><span data-stu-id="85ecb-108">For effective integration, ensure to have a better understanding of the following prerequisites:</span></span>
* <span data-ttu-id="85ecb-109">Teams功能。</span><span class="sxs-lookup"><span data-stu-id="85ecb-109">Teams capabilities.</span></span> 
* <span data-ttu-id="85ecb-110">SharePoint文件和数据存储的要求。</span><span class="sxs-lookup"><span data-stu-id="85ecb-110">SharePoint requirements for file and data storage.</span></span>
* <span data-ttu-id="85ecb-111">API 要求。</span><span class="sxs-lookup"><span data-stu-id="85ecb-111">API requirements.</span></span>
* <span data-ttu-id="85ecb-112">身份验证。</span><span class="sxs-lookup"><span data-stu-id="85ecb-112">Authentication.</span></span>
* <span data-ttu-id="85ecb-113">将应用与应用进行深层Teams。</span><span class="sxs-lookup"><span data-stu-id="85ecb-113">Deep linking of your app with Teams.</span></span>
* <span data-ttu-id="85ecb-114">将应用的用例映射到Teams功能。</span><span class="sxs-lookup"><span data-stu-id="85ecb-114">Map your app's use cases to Teams platform capabilities.</span></span>
* <span data-ttu-id="85ecb-115">确定应用的入口点，例如个人使用和/或协作。</span><span class="sxs-lookup"><span data-stu-id="85ecb-115">Determine your app's entry points, such as personal use, collaboration, or both.</span></span>

## <a name="low-code-platforms"></a><span data-ttu-id="85ecb-116">低代码平台</span><span class="sxs-lookup"><span data-stu-id="85ecb-116">Low code platforms</span></span>

<span data-ttu-id="85ecb-117">低代码平台提供了一种直观的软件开发方法，并且几乎不需要编码即可构建应用程序和流程。</span><span class="sxs-lookup"><span data-stu-id="85ecb-117">Low code platforms provide an intuitive approach to software development and require little or no coding to build applications and processes.</span></span> <span data-ttu-id="85ecb-118">可以使用低代码平台轻松创建自定义应用。</span><span class="sxs-lookup"><span data-stu-id="85ecb-118">You can create custom apps easily with low code platforms.</span></span> <span data-ttu-id="85ecb-119">这些平台包括可视界面、后端服务的连接器以及用于构建、调试、部署和维护应用程序的内置应用生命周期管理系统。</span><span class="sxs-lookup"><span data-stu-id="85ecb-119">These platforms consist of a visual interface, connectors to back end services, and a built-in app lifecycle management system to build, debug, deploy, and maintain applications.</span></span> <span data-ttu-id="85ecb-120">Microsoft 提供以下创新网关，以使用Teams代码属性快速构建兼容应用程序：</span><span class="sxs-lookup"><span data-stu-id="85ecb-120">Microsoft provides the following innovative gateways to rapidly build Teams-compatible apps using low code attributes:</span></span>
* <span data-ttu-id="85ecb-121">Microsoft Power 平台</span><span class="sxs-lookup"><span data-stu-id="85ecb-121">Microsoft Power platform</span></span>
* <span data-ttu-id="85ecb-122">Microsoft Teams应用模板</span><span class="sxs-lookup"><span data-stu-id="85ecb-122">Microsoft Teams app templates</span></span>

## <a name="microsoft-power-platform"></a><span data-ttu-id="85ecb-123">Microsoft Power 平台</span><span class="sxs-lookup"><span data-stu-id="85ecb-123">Microsoft Power platform</span></span>

<span data-ttu-id="85ecb-124">Microsoft Power 平台将四项强大的 Microsoft 技术（如 Power BI、Power Apps、Power Automate 和 Power Virtual Agents）组合在一个功能强大的应用程序平台中。</span><span class="sxs-lookup"><span data-stu-id="85ecb-124">Microsoft Power platform combines four robust Microsoft technologies, such as Power BI, Power Apps, Power Automate, and Power Virtual Agents in one powerful application platform.</span></span> <span data-ttu-id="85ecb-125">这些技术使您可以在统一集成的环境中生成解决方案、自动处理、分析数据以及创建虚拟代理。</span><span class="sxs-lookup"><span data-stu-id="85ecb-125">These technologies empower you to build solutions, automate processes, analyze data, and create virtual agents within a unified and integrated environment.</span></span>

### <a name="power-apps"></a><span data-ttu-id="85ecb-126">Power Apps</span><span class="sxs-lookup"><span data-stu-id="85ecb-126">Power Apps</span></span>

<span data-ttu-id="85ecb-127">通过Power Apps，你可以构建连接到业务数据并针对组织需求定制的业务应用。</span><span class="sxs-lookup"><span data-stu-id="85ecb-127">With Power Apps, you can build business apps that connect to your business data and are tailored to your organization's needs.</span></span> <span data-ttu-id="85ecb-128">Power Apps支持多种应用方案，以通过画布应用解决业务挑战。</span><span class="sxs-lookup"><span data-stu-id="85ecb-128">Power Apps enable a wide range of app scenarios to solve business challenges through canvas apps.</span></span> <span data-ttu-id="85ecb-129">生成应用后，你可以将其从 Power Apps 制造商门户导出并嵌入Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="85ecb-129">After building the app, you can export it from the Power Apps maker portal and embed in Microsoft Teams.</span></span>

### <a name="power-virtual-agents"></a><span data-ttu-id="85ecb-130">Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="85ecb-130">Power Virtual Agents</span></span>

<span data-ttu-id="85ecb-131">Power Virtual Agent 是无代码、引导的图形界面解决方案。</span><span class="sxs-lookup"><span data-stu-id="85ecb-131">Power Virtual Agent is a no code, guided graphical interface solution.</span></span> <span data-ttu-id="85ecb-132">它基于 Microsoft Power Platform 和 Bot Framework 构建。</span><span class="sxs-lookup"><span data-stu-id="85ecb-132">It is built on the Microsoft Power Platform and the Bot Framework.</span></span> <span data-ttu-id="85ecb-133">它使团队的每位成员能够创建和维护丰富的对话聊天机器人，这些聊天机器人可轻松与Teams集成。</span><span class="sxs-lookup"><span data-stu-id="85ecb-133">It empowers every member of your team to create and maintain rich conversational chatbots that easily integrate with the Teams platform.</span></span> <span data-ttu-id="85ecb-134">你可以设计、开发和发布智能虚拟代理Teams而无需设置开发环境、创建 Web 服务或直接在 Bot Framework 中注册。</span><span class="sxs-lookup"><span data-stu-id="85ecb-134">You can design, develop, and publish intelligent virtual agents for Teams without having to setup a development environment, create a web service, or directly register with the Bot Framework.</span></span>

### <a name="create-virtual-assistant"></a><span data-ttu-id="85ecb-135">创建虚拟助手</span><span class="sxs-lookup"><span data-stu-id="85ecb-135">Create Virtual Assistant</span></span>

<span data-ttu-id="85ecb-136">虚拟助理是一个 Microsoft 开放源代码模板，它使您能够创建可靠的对话解决方案，同时保持对用户体验、组织品牌和必要数据的完全控制。</span><span class="sxs-lookup"><span data-stu-id="85ecb-136">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> 

## <a name="app-templates"></a><span data-ttu-id="85ecb-137">应用模板</span><span class="sxs-lookup"><span data-stu-id="85ecb-137">App templates</span></span>

<span data-ttu-id="85ecb-138">可以使用应用模板创建自定义应用以满足组织需求。</span><span class="sxs-lookup"><span data-stu-id="85ecb-138">You can use app template to create custom made apps to suit your organizational needs.</span></span> <span data-ttu-id="85ecb-139">这些是生产就绪型应用Microsoft Teams社区驱动的开放源代码，可在 GitHub。</span><span class="sxs-lookup"><span data-stu-id="85ecb-139">These are production-ready apps for Microsoft Teams that are community driven, open-source, and available on GitHub.</span></span> <span data-ttu-id="85ecb-140">每个模板都包含为组织部署和安装应用的详细说明。</span><span class="sxs-lookup"><span data-stu-id="85ecb-140">Each template contains detailed instructions to deploy and install the app for your organization.</span></span> <span data-ttu-id="85ecb-141">它提供了一个现成的应用程序，您可以立即安装并开始使用该应用程序。</span><span class="sxs-lookup"><span data-stu-id="85ecb-141">It provides a ready-to-use application that you can install and start using immediately.</span></span> 

## <a name="teams-shifts-work-force-management-connectors"></a><span data-ttu-id="85ecb-142">TeamsShifts Work Force Management 连接器</span><span class="sxs-lookup"><span data-stu-id="85ecb-142">Teams Shifts Work Force Management connectors</span></span>

<span data-ttu-id="85ecb-143">Teams轮班工作组管理连接器是生产就绪型、开放源代码和社区驱动的集成。</span><span class="sxs-lookup"><span data-stu-id="85ecb-143">Teams Shifts Work Force Management connectors are production-ready, open-source, and community-driven integrations.</span></span> <span data-ttu-id="85ecb-144">它们通过 Shift 为一线员工的数字转换提供了无缝体验Teams流程。</span><span class="sxs-lookup"><span data-stu-id="85ecb-144">They offer a seamless experience and quick process for the digital transformation of firstline workers with Teams Shifts.</span></span>

## <a name="install-moodle-lms"></a><span data-ttu-id="85ecb-145">安装 Moodle LMS</span><span class="sxs-lookup"><span data-stu-id="85ecb-145">Install Moodle LMS</span></span>

<span data-ttu-id="85ecb-146">在 LMS 中，一个受欢迎的开放源代码 (系统) 。</span><span class="sxs-lookup"><span data-stu-id="85ecb-146">Moodle is a popular open-source Learning Management System (LMS).</span></span> <span data-ttu-id="85ecb-147">现在，它与 Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="85ecb-147">It is now integrated with Microsoft Teams.</span></span> <span data-ttu-id="85ecb-148">此集成可帮助教师和教师协作处理一些与开发方案课程有关的问题，提出有关成绩和作业的问题，并直接在 Teams。</span><span class="sxs-lookup"><span data-stu-id="85ecb-148">This integration helps educators and teachers to collaborate around Moodle courses, ask questions about grades and assignments, and stay updated with notifications directly within Teams.</span></span>

## <a name="create-a-share-to-teams-button-for-your-website"></a><span data-ttu-id="85ecb-149">为网站创建“共享到 Teams”按钮</span><span class="sxs-lookup"><span data-stu-id="85ecb-149">Create a Share-to-Teams button for your website</span></span>

<span data-ttu-id="85ecb-150">第三方网站可以使用启动器脚本将"共享"嵌入Teams网页上的"共享"按钮。</span><span class="sxs-lookup"><span data-stu-id="85ecb-150">Third-party websites can use the launcher script to embed Share to Teams buttons on their webpages.</span></span> <span data-ttu-id="85ecb-151">当你选择该按钮时，它将在弹出窗口中Teams共享以添加体验。</span><span class="sxs-lookup"><span data-stu-id="85ecb-151">When you select the button, it launches the Share to Teams experience in a pop-up window.</span></span> <span data-ttu-id="85ecb-152">这允许你直接将链接共享给任何人员或Microsoft Teams频道，而无需切换上下文。</span><span class="sxs-lookup"><span data-stu-id="85ecb-152">This allows you to share a link directly to any person or Microsoft Teams channel without switching context.</span></span>

## <a name="add-a-microsoft-teams-tab-in-sharepoint"></a><span data-ttu-id="85ecb-153">在Microsoft Teams中添加SharePoint</span><span class="sxs-lookup"><span data-stu-id="85ecb-153">Add a Microsoft Teams tab in SharePoint</span></span>

<span data-ttu-id="85ecb-154">通过将 Microsoft Teams 中的 Microsoft Teams 选项卡添加为 SharePoint Web 部件，Microsoft Teams和 SharePoint 之间SPFx丰富的集成体验。</span><span class="sxs-lookup"><span data-stu-id="85ecb-154">You can get a rich integration experience between Microsoft Teams and SharePoint by adding a Microsoft Teams tab in SharePoint as an SPFx web part.</span></span> 

## <a name="create-deep-link"></a><span data-ttu-id="85ecb-155">创建深层链接</span><span class="sxs-lookup"><span data-stu-id="85ecb-155">Create deep link</span></span>

<span data-ttu-id="85ecb-156">可以创建指向网站中的实体的深层Teams。</span><span class="sxs-lookup"><span data-stu-id="85ecb-156">You can create deep links to the entities in Teams.</span></span> <span data-ttu-id="85ecb-157">您可以创建指向网站内的信息和功能Teams。</span><span class="sxs-lookup"><span data-stu-id="85ecb-157">You can create links to information and features within Teams.</span></span> <span data-ttu-id="85ecb-158">这些深层链接可导航到选项卡中的内容和信息。可以使用深层链接将你的应用与Teams，因为它们将应用的多个部分关联在一起，获得更本机的Teams体验。</span><span class="sxs-lookup"><span data-stu-id="85ecb-158">These deep links navigate to content and information within your tab. You can use deep links to link your app with Teams as they tie together multiple pieces of an app for a more native Teams experience.</span></span>

## <a name="integrate-device-capabilities"></a><span data-ttu-id="85ecb-159">集成设备功能</span><span class="sxs-lookup"><span data-stu-id="85ecb-159">Integrate device capabilities</span></span>

<span data-ttu-id="85ecb-160">Microsoft Teams平台持续增强开发人员功能，以与内置第一方体验保持一致。</span><span class="sxs-lookup"><span data-stu-id="85ecb-160">Microsoft Teams platform is continuously enhancing developer capabilities aligning with built-in first-party experiences.</span></span> <span data-ttu-id="85ecb-161">借助增强的 Teams 平台，合作伙伴可以使用 Microsoft Teams JavaScript 客户端 SDK 中提供的专用 API 访问和集成本机设备功能，例如相机、QR 或条形码扫描仪、照片库、麦克风和位置。</span><span class="sxs-lookup"><span data-stu-id="85ecb-161">The enhanced Teams platform allows partners to access and integrate the native device capabilities, such as camera, QR or barcode scanner, photo gallery, microphone, and location using dedicated APIs available in Microsoft Teams JavaScript client SDK.</span></span> 

## <a name="see-also"></a><span data-ttu-id="85ecb-162">另请参阅</span><span class="sxs-lookup"><span data-stu-id="85ecb-162">See also</span></span>

- [<span data-ttu-id="85ecb-163">将应用的用例映射到Teams功能</span><span class="sxs-lookup"><span data-stu-id="85ecb-163">Map your app's use cases to Teams platform capabilities</span></span>](~/concepts/design/map-use-cases.md)

- [<span data-ttu-id="85ecb-164">确定应用的入口点</span><span class="sxs-lookup"><span data-stu-id="85ecb-164">Determine your app's entry points</span></span>](~/concepts/extensibility-points.md)

- [<span data-ttu-id="85ecb-165">集成 web 应用</span><span class="sxs-lookup"><span data-stu-id="85ecb-165">Integrate web apps</span></span>](~/samples/integrating-web-apps.md)

- [<span data-ttu-id="85ecb-166">为用户创建低代码自定义Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="85ecb-166">Create low-code custom apps for Microsoft Teams</span></span>](~/samples/teams-low-code-solutions.md)

- [<span data-ttu-id="85ecb-167">添加强大的虚拟代理聊天机器人</span><span class="sxs-lookup"><span data-stu-id="85ecb-167">Add a Power Virtual Agents chatbot</span></span>](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)

- [<span data-ttu-id="85ecb-168">创建虚拟助理</span><span class="sxs-lookup"><span data-stu-id="85ecb-168">Create virtual assistant</span></span>](~/samples/virtual-assistant.md)

- [<span data-ttu-id="85ecb-169">Microsoft Teams 的应用模板</span><span class="sxs-lookup"><span data-stu-id="85ecb-169">App templates for Microsoft Teams</span></span>](~/samples/app-templates.md)

- [<span data-ttu-id="85ecb-170">生产就绪 Shift 连接器</span><span class="sxs-lookup"><span data-stu-id="85ecb-170">Production-ready Shift Connectors</span></span>](~/samples/shifts-wfm-connectors.md)

- [<span data-ttu-id="85ecb-171">安装 Moodle LMS</span><span class="sxs-lookup"><span data-stu-id="85ecb-171">Install Moodle LMS</span></span>](~/resources/moodleinstructions.md)

- [<span data-ttu-id="85ecb-172">创建“共享到Teams”按钮</span><span class="sxs-lookup"><span data-stu-id="85ecb-172">Create a Share-to-Teams button</span></span>](~/concepts/build-and-test/share-to-teams.md)

- [<span data-ttu-id="85ecb-173">向 SharePoint 添加Teams选项卡</span><span class="sxs-lookup"><span data-stu-id="85ecb-173">Add a Teams tab to SharePoint</span></span>](~/tabs/how-to/tabs-in-sharepoint.md)

- [<span data-ttu-id="85ecb-174">创建深层链接</span><span class="sxs-lookup"><span data-stu-id="85ecb-174">Create deep links</span></span>](~/concepts/build-and-test/deep-links.md)

- [<span data-ttu-id="85ecb-175">设备功能</span><span class="sxs-lookup"><span data-stu-id="85ecb-175">Device capabilities</span></span>](~/concepts/device-capabilities/device-capabilities-overview.md)
