---
title: 应用程序托管的媒体机器人的要求和注意事项
description: 了解与为 Microsoft Teams 创建应用程序托管的媒体机器人相关的重要要求和注意事项。
ms.topic: conceptual
localization_priority: Normal
keywords: 应用程序托管的媒体 Windows 服务器 azure vm
ms.date: 11/16/2018
ms.openlocfilehash: 731cc53573d5c2b65eaed36d75793901fde86e54
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020054"
---
# <a name="requirements-and-considerations-for-application-hosted-media-bots"></a><span data-ttu-id="c5147-104">应用程序托管的媒体机器人的要求和注意事项</span><span class="sxs-lookup"><span data-stu-id="c5147-104">Requirements and considerations for application-hosted media bots</span></span>

<span data-ttu-id="c5147-105">应用程序托管的媒体机器人需要[ `Microsoft.Graph.Communications.Calls.Media` .NET 库](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)来访问音频和视频媒体流。</span><span class="sxs-lookup"><span data-stu-id="c5147-105">An application-hosted media bot requires the [`Microsoft.Graph.Communications.Calls.Media` .NET library](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) to access the audio and video media streams.</span></span> <span data-ttu-id="c5147-106">必须在 Azure 中的 Windows Server 计算机或 Windows Server 来宾操作系统 (操作系统) 自动程序。</span><span class="sxs-lookup"><span data-stu-id="c5147-106">The bot must be deployed on a Windows Server machine or Windows Server guest Operating System (OS) in Azure.</span></span>

> [!NOTE]
> * <span data-ttu-id="c5147-107">使用 IVR 自动程序开发消息传递和 (语音响应) 指南并不完全适用于构建应用程序托管的媒体机器人。</span><span class="sxs-lookup"><span data-stu-id="c5147-107">The guidance for developing messaging and Interactive Voice Response (IVR) bots does not completely apply to building application-hosted media bots.</span></span>
> * <span data-ttu-id="c5147-108">由于适用于机器人的 Microsoft 实时媒体平台在开发人员预览版中，本文档中的指南可能会更改。</span><span class="sxs-lookup"><span data-stu-id="c5147-108">As the Microsoft Real-time Media Platform for bots is in developer preview, the guidance in this document is subject to change.</span></span>

## <a name="c-or-net-and-windows-server-for-development"></a><span data-ttu-id="c5147-109">C# .NET 和 Windows Server 进行开发</span><span class="sxs-lookup"><span data-stu-id="c5147-109">C# or .NET and Windows Server for development</span></span>

<span data-ttu-id="c5147-110">应用程序托管的媒体自动程序需要以下各项：</span><span class="sxs-lookup"><span data-stu-id="c5147-110">An application-hosted media bot requires the following:</span></span>

- <span data-ttu-id="c5147-111">必须在 Microsoft Azure 中C#和标准.NET Framework和部署自动程序。</span><span class="sxs-lookup"><span data-stu-id="c5147-111">The bot must be developed in C# and the standard .NET Framework and deployed in Microsoft Azure.</span></span> <span data-ttu-id="c5147-112">不能使用 C++ 或 Node.js API 访问实时媒体，应用程序托管的媒体机器人不支持 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="c5147-112">You cannot use C++ or Node.js APIs to access real-time media and .NET Core is not supported for an application-hosted media bot.</span></span>

- <span data-ttu-id="c5147-113">机器人可以托管在下列 Azure 服务环境之一中：</span><span class="sxs-lookup"><span data-stu-id="c5147-113">The bot can be hosted within one of the following Azure service environments:</span></span>
    - <span data-ttu-id="c5147-114">云服务。</span><span class="sxs-lookup"><span data-stu-id="c5147-114">Cloud Service.</span></span>
    - <span data-ttu-id="c5147-115">Service Fabric with Virtual Machine Scale Sets (VMSS) 。</span><span class="sxs-lookup"><span data-stu-id="c5147-115">Service Fabric with Virtual Machine Scale Sets (VMSS).</span></span>
    - <span data-ttu-id="c5147-116">IaaS (服务基础结构) 虚拟机 (VM) 。</span><span class="sxs-lookup"><span data-stu-id="c5147-116">Infrastructure as a Service (IaaS) Virtual Machine (VM).</span></span>  
  
- <span data-ttu-id="c5147-117">自动程序无法部署为 Azure Web 应用。</span><span class="sxs-lookup"><span data-stu-id="c5147-117">The bot cannot be deployed as an Azure web app.</span></span>

- <span data-ttu-id="c5147-118">自动程序必须在最新版本的 `Microsoft.Graph.Communications.Calls.Media` .NET 库上运行。</span><span class="sxs-lookup"><span data-stu-id="c5147-118">The bot must be running on a recent version of the `Microsoft.Graph.Communications.Calls.Media` .NET library.</span></span> <span data-ttu-id="c5147-119">自动程序必须使用 [NuGet](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)程序包的最新版本或不超过三个月的版本。</span><span class="sxs-lookup"><span data-stu-id="c5147-119">The bot must use either the newest available version of the [NuGet package](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/), or a version that is not more than three months old.</span></span> <span data-ttu-id="c5147-120">旧版本的库已弃用，在几个月后将不起作用。</span><span class="sxs-lookup"><span data-stu-id="c5147-120">Older versions of the library are deprecated and do not work after a few months.</span></span> <span data-ttu-id="c5147-121">使库保持最新状态可确保自动程序与 Microsoft Teams 之间的最佳 `Microsoft.Graph.Communications.Calls.Media` 互操作性。</span><span class="sxs-lookup"><span data-stu-id="c5147-121">Keeping the `Microsoft.Graph.Communications.Calls.Media` library up-to-date ensures the best interoperability between the bot and Microsoft Teams.</span></span>

<span data-ttu-id="c5147-122">下一节提供有关实时媒体呼叫的位置的详细信息。</span><span class="sxs-lookup"><span data-stu-id="c5147-122">The next section provides details on where real-time media calls are located.</span></span>

## <a name="real-time-media-calls-stay-where-they-are-created"></a><span data-ttu-id="c5147-123">实时媒体呼叫将一直留在其创建位置</span><span class="sxs-lookup"><span data-stu-id="c5147-123">Real-time media calls stay where they are created</span></span>

<span data-ttu-id="c5147-124">实时媒体呼叫将留在创建媒体呼叫的计算机上。</span><span class="sxs-lookup"><span data-stu-id="c5147-124">Real-time media calls stay on the computer where they were created.</span></span> <span data-ttu-id="c5147-125">实时媒体呼叫固定到接受或启动 (虚拟机) 虚拟机。</span><span class="sxs-lookup"><span data-stu-id="c5147-125">A real-time media call is pinned to the virtual machine (VM) instance that accepted or started the call.</span></span> <span data-ttu-id="c5147-126">来自 Microsoft Teams 呼叫或会议的媒体流到该 VM 实例，机器人发送回 Microsoft Teams 的媒体也必须源自该 VM。</span><span class="sxs-lookup"><span data-stu-id="c5147-126">Media from a Microsoft Teams call or meeting flows to that VM instance, and media the bot sends back to Microsoft Teams must also originate from that VM.</span></span> <span data-ttu-id="c5147-127">如果 VM 停止时有任何实时媒体调用正在进行，则这些调用会突然终止。</span><span class="sxs-lookup"><span data-stu-id="c5147-127">If there are any real-time media calls in progress when the VM is stopped, those calls are abruptly terminated.</span></span> <span data-ttu-id="c5147-128">如果机器人事先知道挂起的虚拟机关闭，它可以结束调用。</span><span class="sxs-lookup"><span data-stu-id="c5147-128">If the bot has prior knowledge of the pending VM shutdown, it can end the calls.</span></span>

<span data-ttu-id="c5147-129">下一节提供有关应用程序托管的媒体机器人的辅助功能的详细信息。</span><span class="sxs-lookup"><span data-stu-id="c5147-129">The next section provides details on accessibility of application-hosted media bots.</span></span>

## <a name="application-hosted-media-bots-accessible-on-the-internet"></a><span data-ttu-id="c5147-130">可通过 Internet 访问应用程序托管的媒体机器人</span><span class="sxs-lookup"><span data-stu-id="c5147-130">Application-hosted media bots accessible on the internet</span></span>

<span data-ttu-id="c5147-131">应用程序托管的媒体机器人必须在 Internet 上直接访问。</span><span class="sxs-lookup"><span data-stu-id="c5147-131">Application-hosted media bots must be directly accessible on the internet.</span></span> <span data-ttu-id="c5147-132">这些机器人必须包含以下功能：</span><span class="sxs-lookup"><span data-stu-id="c5147-132">These bots must include the following features:</span></span>

- <span data-ttu-id="c5147-133">在 Azure 中托管应用程序托管的媒体自动程序的每个 VM 实例都必须可通过 Internet 使用 ILPIP (公共 IP 地址) 。</span><span class="sxs-lookup"><span data-stu-id="c5147-133">Each VM instance hosting an application-hosted media bot in Azure must be directly accessible from the internet using an instance-level public IP address (ILPIP).</span></span>
    - <span data-ttu-id="c5147-134">有关获取和配置 Azure 云服务的 ILPIP 的信息，请参阅实例 [级公共 IP 经典概述](/azure/virtual-network/virtual-networks-instance-level-public-ip)。</span><span class="sxs-lookup"><span data-stu-id="c5147-134">For obtaining and configuring an ILPIP for an Azure Cloud Service, see [instance level public IP classic overview](/azure/virtual-network/virtual-networks-instance-level-public-ip).</span></span>
    - <span data-ttu-id="c5147-135">有关为 VM 规模集配置 ILPIP，请参阅[每个虚拟机的公用 IPv4。](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking#public-ipv4-per-virtual-machine)</span><span class="sxs-lookup"><span data-stu-id="c5147-135">For configuring an ILPIP for a VM Scale Set, see [public IPv4 per virtual machine](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking#public-ipv4-per-virtual-machine).</span></span>
- <span data-ttu-id="c5147-136">承载应用程序托管的媒体机器人的服务还必须使用映射到特定实例的面向公众的端口配置每个 VM 实例。</span><span class="sxs-lookup"><span data-stu-id="c5147-136">The service hosting an application-hosted media bot must also configure each VM instance with a public-facing port which maps to the specific instance.</span></span>
    - <span data-ttu-id="c5147-137">对于 Azure 云服务，这需要实例输入终结点。</span><span class="sxs-lookup"><span data-stu-id="c5147-137">For an Azure Cloud Service, this requires an instance input endpoint.</span></span> <span data-ttu-id="c5147-138">有关详细信息，请参阅在 [Azure 中启用角色实例的通信](/azure/cloud-services/cloud-services-enable-communication-role-instances)。</span><span class="sxs-lookup"><span data-stu-id="c5147-138">For more information, see [enable communication for role instances in Azure](/azure/cloud-services/cloud-services-enable-communication-role-instances).</span></span>
    - <span data-ttu-id="c5147-139">对于 VM 规模集，必须配置负载平衡器上的 NAT 规则。</span><span class="sxs-lookup"><span data-stu-id="c5147-139">For a VM Scale Set, a NAT rule on the load balancer must be configured.</span></span> <span data-ttu-id="c5147-140">有关详细信息，请参阅 [Azure 中的虚拟网络和虚拟机](/azure/virtual-machines/windows/network-overview)。</span><span class="sxs-lookup"><span data-stu-id="c5147-140">For more information, see [virtual networks and virtual machines in Azure](/azure/virtual-machines/windows/network-overview).</span></span>
- <span data-ttu-id="c5147-141">Bot Framework Emulator 不支持应用程序托管的媒体机器人。</span><span class="sxs-lookup"><span data-stu-id="c5147-141">Application-hosted media bots are not supported by the Bot Framework Emulator.</span></span>

<span data-ttu-id="c5147-142">下一节提供有关应用程序托管的媒体机器人的可伸缩性和性能注意事项的详细信息。</span><span class="sxs-lookup"><span data-stu-id="c5147-142">The next section provides details on scalability and performance considerations of application-hosted media bots.</span></span>

## <a name="scalability-and-performance-considerations"></a><span data-ttu-id="c5147-143">可伸缩性和性能注意事项</span><span class="sxs-lookup"><span data-stu-id="c5147-143">Scalability and performance considerations</span></span>

<span data-ttu-id="c5147-144">应用程序托管的媒体机器人需要以下可伸缩性和性能注意事项：</span><span class="sxs-lookup"><span data-stu-id="c5147-144">Application-hosted media bots require the following scalability and performance considerations:</span></span>

## <a name="code-sample"></a><span data-ttu-id="c5147-145">代码示例</span><span class="sxs-lookup"><span data-stu-id="c5147-145">Code sample</span></span>

<span data-ttu-id="c5147-146">应用程序托管的媒体机器人示例如下所示：</span><span class="sxs-lookup"><span data-stu-id="c5147-146">Application-hosted media bots samples are as follows:</span></span>

| <span data-ttu-id="c5147-147">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="c5147-147">**Sample name**</span></span> | <span data-ttu-id="c5147-148">**描述**</span><span class="sxs-lookup"><span data-stu-id="c5147-148">**Description**</span></span> | <span data-ttu-id="c5147-149">**Graph**</span><span class="sxs-lookup"><span data-stu-id="c5147-149">**Graph**</span></span> |
|------------|-------------|-----------|
| <span data-ttu-id="c5147-150">本地媒体示例</span><span class="sxs-lookup"><span data-stu-id="c5147-150">Local media sample</span></span> | <span data-ttu-id="c5147-151">说明不同本地媒体方案的示例。</span><span class="sxs-lookup"><span data-stu-id="c5147-151">Samples that illustrates different local media scenarios.</span></span> | [<span data-ttu-id="c5147-152">View</span><span class="sxs-lookup"><span data-stu-id="c5147-152">View</span></span>](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples) |
| <span data-ttu-id="c5147-153">远程媒体示例</span><span class="sxs-lookup"><span data-stu-id="c5147-153">Remote media sample</span></span> | <span data-ttu-id="c5147-154">演示不同远程媒体方案的示例。</span><span class="sxs-lookup"><span data-stu-id="c5147-154">Samples that illustrates different remote media scenarios.</span></span> | [<span data-ttu-id="c5147-155">View</span><span class="sxs-lookup"><span data-stu-id="c5147-155">View</span></span>](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/RemoteMediaSamples) |

## <a name="see-also"></a><span data-ttu-id="c5147-156">另请参阅</span><span class="sxs-lookup"><span data-stu-id="c5147-156">See also</span></span>

- [<span data-ttu-id="c5147-157">Graph 调用 SDK 文档</span><span class="sxs-lookup"><span data-stu-id="c5147-157">Graph Calling SDK Documentation</span></span>](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
- <span data-ttu-id="c5147-158">机器人需要比消息机器人更多的计算和网络带宽容量，并且会产生更高的运营成本。</span><span class="sxs-lookup"><span data-stu-id="c5147-158">The bots require more compute and network bandwidth capacity than messaging bots and incur significantly higher operational costs.</span></span> <span data-ttu-id="c5147-159">实时媒体自动程序开发人员必须仔细衡量机器人的可伸缩性，并确保机器人接受的并发呼叫数不会超过它可以管理的时间。</span><span class="sxs-lookup"><span data-stu-id="c5147-159">A real-time media bot developer must carefully measure the bot's scalability, and ensure the bot does not accept more simultaneous calls than it can manage.</span></span> <span data-ttu-id="c5147-160">如果使用原始 RGB24 或 NV12 视频格式，启用视频的机器人只能维持每个 CPU 内核的一个或两个并发媒体会话。</span><span class="sxs-lookup"><span data-stu-id="c5147-160">A video-enabled bot can sustain only one or two concurrent media sessions per CPU core if using the raw RGB24 or NV12 video formats.</span></span>
- <span data-ttu-id="c5147-161">实时媒体平台当前不会利用 VM 上提供的任何图形处理单元 (GPU) 以对 H.264 视频编码或解码进行非负载处理。</span><span class="sxs-lookup"><span data-stu-id="c5147-161">The Real-time Media Platform does not currently take advantage of any Graphics Processing Units (GPU) available on the VM to off-load H.264 video encoding or decoding.</span></span> <span data-ttu-id="c5147-162">相反，视频编码和解码在 CPU 上的软件中完成。</span><span class="sxs-lookup"><span data-stu-id="c5147-162">Instead, video encode and decode are done in software on the CPU.</span></span> <span data-ttu-id="c5147-163">如果 GPU 可用，则机器人会利用它来呈现自己的图形，例如，如果机器人使用的是 3D 图形引擎。</span><span class="sxs-lookup"><span data-stu-id="c5147-163">If a GPU is available, the bot takes advantage of it for its own graphics rendering, for example, if the bot is using a 3D graphics engine.</span></span>
- <span data-ttu-id="c5147-164">托管实时媒体机器人的 VM 实例必须至少具有 2 个 CPU 内核。</span><span class="sxs-lookup"><span data-stu-id="c5147-164">The VM instance hosting the real-time media bot must have at least 2 CPU cores.</span></span> <span data-ttu-id="c5147-165">对于 Azure，建议使用 Dv2 系列虚拟机。</span><span class="sxs-lookup"><span data-stu-id="c5147-165">For Azure, a Dv2-series virtual machine is recommended.</span></span> <span data-ttu-id="c5147-166">对于其他 Azure VM 类型，具有 4 个虚拟 CPU (vCPU) 是所需的最小大小。</span><span class="sxs-lookup"><span data-stu-id="c5147-166">For other Azure VM types, a system with 4 virtual CPUs (vCPU) is the minimum size required.</span></span> <span data-ttu-id="c5147-167">有关 Azure VM 类型详细信息，请参阅 [Azure 文档](/azure/virtual-machines/windows/sizes-general)。</span><span class="sxs-lookup"><span data-stu-id="c5147-167">For more information about Azure VM types, see [Azure documentation](/azure/virtual-machines/windows/sizes-general).</span></span>

<span data-ttu-id="c5147-168">下一节提供了说明不同本地媒体方案的示例。</span><span class="sxs-lookup"><span data-stu-id="c5147-168">The next section provides samples that illustrate different local media scenarios.</span></span>

## <a name="samples-and-additional-resources"></a><span data-ttu-id="c5147-169">示例和其他资源</span><span class="sxs-lookup"><span data-stu-id="c5147-169">Samples and additional resources</span></span>

- [<span data-ttu-id="c5147-170">示例应用程序</span><span class="sxs-lookup"><span data-stu-id="c5147-170">Sample applications</span></span>](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples)
- [<span data-ttu-id="c5147-171">Graph 调用 SDK 文档</span><span class="sxs-lookup"><span data-stu-id="c5147-171">Graph calling SDK documentation</span></span>](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)

## <a name="next-step"></a><span data-ttu-id="c5147-172">后续步骤</span><span class="sxs-lookup"><span data-stu-id="c5147-172">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c5147-173">支持的媒体格式</span><span class="sxs-lookup"><span data-stu-id="c5147-173">Supported media formats</span></span>](~/resources/media-formats.md)
