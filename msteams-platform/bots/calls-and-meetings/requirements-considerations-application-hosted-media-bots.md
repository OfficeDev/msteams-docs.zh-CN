---
title: 应用程序托管的媒体机器人的要求和注意事项
description: 了解与为 Microsoft Teams 创建应用程序托管的媒体机器人相关的重要要求和注意事项。
ms.topic: conceptual
keywords: 应用程序托管的媒体 Windows 服务器 azure vm
ms.date: 11/16/2018
ms.openlocfilehash: bf75b7f689713f16cb3ff9ff4313ab829b5cc2d6
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014486"
---
# <a name="requirements-and-considerations-for-application-hosted-media-bots"></a>应用程序托管的媒体机器人的要求和注意事项

并非所有有关在 IVR 中开发消息传递和互动语音响应 (指南) 构建应用程序托管的媒体机器人同样适用。 本文介绍开发并运行应用程序托管的媒体机器人的一些重要要求和注意事项。

> [!NOTE]
> 由于适用于机器人的 Microsoft 实时媒体平台位于开发人员预览版中，因此本文中的指南可能会更改。

## <a name="application-hosted-media-bot-development-requires-cnet-and-windows-server"></a>应用程序托管的媒体机器人开发需要 C#/.NET 和 Windows Server

- 应用程序托管的媒体自动程序需要此处提供的 .NET 库 (来访问音频和视频媒体流，并且必须在 Windows Server 计算机 (或 Azure) 中的 Windows Server 来宾操作系统上部署机器人。 `Microsoft.Graph.Communications.Calls.Media` [](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) 因此，必须在 C# 和标准 .NET Framework 中开发自动程序，并部署在 Microsoft Azure 中。 你不能使用 C++ 或 Node.js API 访问实时媒体，应用程序托管的媒体自动程序不支持 .NET Core。

- 应用程序托管的媒体自动程序可以托管在下列 Azure 服务环境之一中：
  - 云服务。
  - 具有虚拟机缩放集的 Service Fabric (VMSS) 。
  - IaaS (服务基础结构) 虚拟机 (VM) 。  
  
- 应用程序托管的媒体机器人无法部署为 Azure Web App。

- 应用程序托管的媒体自动程序必须在 .NET 库的 `Microsoft.Graph.Communications.Calls.Media` 最新版本上运行。 机器人应该使用 [NuGet](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)程序包的最新版本或不超过三个月的版本。 较旧版本的库将被弃用，在几个月后可能不起作用。 使库保持最新将确保自动程序与 Microsoft Teams 之间的最佳 `Microsoft.Graph.Communications.Calls.Media` 互操作性。

## <a name="real-time-media-calls-stay-on-the-machine-where-they-were-created"></a>实时媒体呼叫将停留在创建它们时所位于的计算机上

- 实时媒体呼叫将固定到接受或 (虚拟机) 虚拟机实例。 来自 Microsoft Teams 呼叫或会议媒体将流动到该 VM 实例，机器人发送回 Microsoft Teams 的媒体也必须源自该 VM。
- 如果 VM 停止时正在进行任何实时媒体呼叫，则这些调用将突然终止。 如果机器人事先知道挂起的虚拟机关闭，可以尝试"正常"结束调用。

## <a name="application-hosted-media-bots-must-be-directly-accessible-on-the-internet"></a>应用程序托管的媒体机器人必须在 Internet 上直接访问

- 在 Azure 中托管应用程序托管的媒体自动程序的每个 VM 实例都必须使用 ILPIP (实例级公用 IP 地址直接从 internet 访问) 。
  - 有关获取和配置 Azure 云服务的 ILPIP 的信息，请参阅"实例级别公共 IP ([经典) 概述](/azure/virtual-network/virtual-networks-instance-level-public-ip)。
  - 有关为 VM 规模集配置 ILPIP，请参阅每个虚拟机[的公用 IPv4。](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking#public-ipv4-per-virtual-machine)
- 承载应用程序托管的媒体自动程序的服务还必须使用映射到特定实例的面向公众的端口配置每个 VM 实例。
  - 对于 Azure 云服务，这需要实例输入终结点;请参阅 [在 Azure 中启用角色实例的通信](/azure/cloud-services/cloud-services-enable-communication-role-instances)。
  - 对于 VM 规模集，必须配置负载平衡器上的 NAT 规则;请参阅 [Azure 中的虚拟网络和虚拟机](/azure/virtual-machines/windows/network-overview)。
- 自动程序框架仿真器不支持应用程序托管的媒体机器人。

## <a name="scalability-and-performance-considerations"></a>可伸缩性和性能注意事项

- 应用程序托管的媒体自动程序需要比 (机器人) 更多的计算和网络带宽，并且可能会产生更高的运营成本。 实时媒体自动程序开发人员必须仔细衡量机器人的可伸缩性，并确保机器人不接受多于它可以管理的并发呼叫数。 如果使用"原始"RGB24 或 NV12 视频格式 (则启用视频的机器人只能维持每个 CPU 内核的一个或两个并发媒体) 。
- 实时媒体平台当前不会利用 VM 上提供的任何图形处理单元 (GPU) 来对 H.264 视频编码/解码进行负载外加载。 相反，视频编码和解码在 CPU 上的软件中完成。 如果 GPU 可用，机器人可以利用它来呈现自己的图形 (例如，如果机器人使用 3D 图形引擎) 。
- 托管实时媒体自动程序的 VM 实例必须至少具有 2 个 CPU 内核。 对于 Azure，建议使用 Dv2 系列虚拟机。 对于其他 Azure VM 类型，具有 4 个虚拟 CPU (vCPU) 是最低大小所需的。 Azure 文档中提供了有关 Azure VM 类型 [的详细信息](/azure/virtual-machines/windows/sizes-general)。

## <a name="samples-and-additional-resources"></a>示例和其他资源

- [示例应用程序](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples)
- [Graph 调用 SDK 文档](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
