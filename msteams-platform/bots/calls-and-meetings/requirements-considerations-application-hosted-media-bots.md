---
title: 应用程序托管媒体 bot 的要求和注意事项
description: 了解与为 Microsoft 团队创建应用程序托管媒体 bot 相关的重要要求和注意事项。
keywords: 应用程序承载的媒体 windows server azure 虚拟机
ms.date: 11/16/2018
ms.openlocfilehash: f5b721edacb11e867d05c8213b74036cb51f419c
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801007"
---
# <a name="requirements-and-considerations-for-application-hosted-media-bots"></a>应用程序托管媒体 bot 的要求和注意事项

并非所有开发邮件和交互语音响应（IVR） bot 的指南都同样适用于生成应用程序托管的媒体 bot。 本文介绍了开发和运行应用程序托管媒体 bot 的一些重要要求和注意事项。

> [!NOTE]
> 由于用于 Bot 的 Microsoft 实时媒体平台是在开发人员预览版中，因此本文中的指导可能会发生变化。

## <a name="application-hosted-media-bot-development-requires-cnet-and-windows-server"></a>应用程序托管的媒体 bot 开发需要 c #/.NET 和 Windows Server

- 应用程序托管的媒体 bot 需要 `Microsoft.Graph.Communications.Calls.Media` .net 库（[可在此处](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)访问音频和视频媒体流，并且必须在 windows server 计算机（或 Azure 中的 WINDOWS server 来宾 OS）上部署 bot。 因此，必须在 c # 和 standard .NET Framework 中开发机器人并在 Microsoft Azure 中部署机器人。 不能使用 c + + 或 Node.js Api 访问实时媒体和 .NET Core 不支持应用程序托管的媒体 bot。

- 可以在以下 Azure 服务环境之一中托管应用程序托管的媒体 bot：
  - 云服务。
  - 具有虚拟机规模集的 Service Fabric （VMSS）。
  - 基础结构即服务（IaaS）虚拟机（VM）。  
  
- 无法将应用程序托管的媒体 bot 部署为 Azure Web 应用。

- 应用程序托管的媒体 bot 必须在 .Net 库的最新版本上运行 `Microsoft.Graph.Communications.Calls.Media` 。 Bot 应使用最新可用版本的[NuGet 包](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)，或使用的版本不超过三个月。 库的较旧版本将被弃用，并且在几个月后可能无法工作。 `Microsoft.Graph.Communications.Calls.Media`将库保持最新可确保机器人和 Microsoft 团队之间的最佳互操作性。

## <a name="real-time-media-calls-stay-on-the-machine-where-they-were-created"></a>实时媒体呼叫停留在创建它们的计算机上

- 实时媒体呼叫将固定到已接受或已启动呼叫的虚拟机（VM）实例。 来自 Microsoft 团队呼叫或会议的媒体将流向该 VM 实例，并且机器人发送回 Microsoft 团队的媒体也必须源自该 VM。
- 如果在停止 VM 时正在进行任何实时媒体呼叫，这些呼叫将突然终止。 如果 bot 事先了解挂起的 VM 关闭，它可能会尝试 "正常" 结束呼叫。

## <a name="application-hosted-media-bots-must-be-directly-accessible-on-the-internet"></a>应用程序托管的媒体 bot 必须可以直接在 internet 上进行访问

- 在 Azure 中托管应用程序托管媒体 bot 的每个 VM 实例都必须使用实例级公共 IP 地址（ILPIP）直接从 internet 进行访问。
  - 若要获取和配置 Azure 云服务的 ILPIP，请参阅[Instance level PUBLIC IP （经典）概述](/azure/virtual-network/virtual-networks-instance-level-public-ip)。
  - 若要为 VM 规模集配置 ILPIP，请参阅[Public IPv4 per virtual machine](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking#public-ipv4-per-virtual-machine)。
- 承载应用程序托管媒体 bot 的服务还必须使用映射到特定实例的面向公众的端口配置每个 VM 实例。
  - 对于 Azure 云服务，这需要一个实例输入终结点;请参阅[在 Azure 中启用角色实例的通信](/azure/cloud-services/cloud-services-enable-communication-role-instances)。
  - 对于 VM 规模集，必须配置负载平衡器上的 NAT 规则;请参阅[Azure 中的虚拟网络和虚拟机](/azure/virtual-machines/windows/network-overview)。
- Bot 框架仿真器不支持应用程序托管的媒体 bot。

## <a name="scalability-and-performance-considerations"></a>可伸缩性和性能注意事项

- 应用程序托管的媒体 bot 需要比邮件机器人更多的计算和网络（带宽）容量，并且可能会产生显著更高的运营成本。 实时媒体机器人开发人员必须仔细衡量 bot 的可伸缩性，并确保 bot 不会接受比它更多的同时呼叫数。 启用视频的 bot 可能只能承受每个 CPU 核心的一个或两个并发媒体会话（如果使用 "raw" RGB24 或 NV12 视频格式）。
- 实时媒体平台目前不会利用 VM 上提供的任何图形处理单元（GPU）来脱离加载 H-p 视频编码/解码。 相反，视频编码和解码是在 CPU 上的软件中完成的。 如果有 GPU 可用，则 bot 可以利用它进行自己的图形呈现（例如，如果 bot 使用的是3D 图形引擎）。
- 托管实时媒体 bot 的 VM 实例必须至少具有2个 CPU 内核。 对于 Azure，建议使用 Dv2 系列虚拟机。 对于其他 Azure VM 类型，具有4个虚拟 Cpu （vCPU）的系统是所需的最小大小。 Azure[文档](/azure/virtual-machines/windows/sizes-general)中提供了有关 azure VM 类型的详细信息。

## <a name="samples-and-additional-resources"></a>示例和其他资源

- [示例应用程序](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples)
- [图调用 SDK 文档](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
