---
title: 应用程序托管的媒体机器人的要求和注意事项
description: 了解重要要求和注意事项，以及与使用代码示例和示例创建应用程序托管的媒体Microsoft Teams程序相关的可伸缩性和性能注意事项。
ms.topic: conceptual
ms.localizationpriority: medium
keywords: 应用程序托管的媒体 Windows 服务器 azure vm
ms.date: 11/16/2018
ms.openlocfilehash: 0597e99b1933270ee4ee85d1adc18378da3c3114
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2021
ms.locfileid: "60887411"
---
# <a name="requirements-and-considerations-for-application-hosted-media-bots"></a>应用程序托管的媒体机器人的要求和注意事项

应用程序托管的媒体机器人需要[ `Microsoft.Graph.Communications.Calls.Media` .NET 库](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)来访问音频和视频媒体流。 必须在 Azure 中的 Windows Server 计算机或 Windows Server 来宾操作系统 (操作系统) 自动程序。

> [!NOTE]
> * 使用 IVR 自动程序 (互动语音响应) 指南并不完全适用于构建应用程序托管的媒体机器人。
> * 由于适用于机器人的 Microsoft 实时媒体平台在开发人员预览版中，本文档中的指南可能会更改。

## <a name="c-or-net-and-windows-server-for-development"></a>C# .NET 和 Windows Server 进行开发

应用程序托管的媒体机器人需要以下各项：

- 自动程序必须在C#和标准.NET Framework中部署Microsoft Azure。 不能使用 C++ 或 Node.js API 访问实时媒体，而应用程序托管的媒体机器人不支持 .NET Core。

- 机器人可以托管在下列 Azure 服务环境之一中：
    - 云服务。
    - Service Fabric VMSS (虚拟机缩放) 。
    - IaaS 虚拟机 (基础结构即) 虚拟机 (VM) 。  
  
- 自动程序无法部署为 Azure Web 应用。

- 自动程序必须在最新版本的 `Microsoft.Graph.Communications.Calls.Media` .NET 库上运行。 自动程序必须使用最新版本的 NuGet[程序包，](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)或使用不超过三个月的版本。 旧版本的库已弃用，在几个月后将不起作用。 使库保持最新状态可确保自动程序与自动程序之间的 `Microsoft.Graph.Communications.Calls.Media` 最佳Microsoft Teams。

下一节提供有关实时媒体呼叫的位置的详细信息。

## <a name="real-time-media-calls-stay-where-they-are-created"></a>实时媒体呼叫将一直留在其创建位置

实时媒体呼叫将留在创建媒体呼叫的计算机上。 实时媒体呼叫固定到接受或启动 (虚拟机) 虚拟机。 来自Microsoft Teams或会议的媒体流流到该 VM 实例，机器人发送回Microsoft Teams的媒体也必须源自该 VM。 如果 VM 停止时有任何实时媒体调用正在进行，则这些调用会突然终止。 如果机器人事先知道挂起的虚拟机关闭，它可以结束调用。

下一节提供有关应用程序托管的媒体机器人的辅助功能的详细信息。

## <a name="application-hosted-media-bots-accessible-on-the-internet"></a>可通过 Internet 访问应用程序托管的媒体机器人

应用程序托管的媒体机器人必须在 Internet 上直接访问。 这些机器人必须包含以下功能：

- 在 Azure 中托管应用程序托管的媒体机器人的每个 VM 实例都必须可通过 Internet 使用 ILPIP (公共 IP 地址) 。
    - 有关获取和配置 Azure 云服务的 ILPIP 的信息，请参阅实例 [级公共 IP 经典概述](/azure/virtual-network/virtual-networks-instance-level-public-ip)。
    - 有关为 VM 规模集配置 ILPIP，请参阅[每个虚拟机的公用 IPv4。](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking#public-ipv4-per-virtual-machine)
- 承载应用程序托管的媒体机器人的服务还必须使用映射到特定实例的面向公众的端口配置每个 VM 实例。
    - 对于 Azure 云服务，这需要实例输入终结点。 有关详细信息，请参阅在 [Azure 中启用角色实例的通信](/azure/cloud-services/cloud-services-enable-communication-role-instances)。
    - 对于 VM 规模集，必须配置负载平衡器上的 NAT 规则。 有关详细信息，请参阅 [Azure 中的虚拟网络和虚拟机](/azure/virtual-machines/windows/network-overview)。
- 应用程序托管的媒体自动程序不受 Bot Framework Emulator。

下一节提供有关应用程序托管的媒体机器人的可伸缩性和性能注意事项的详细信息。

## <a name="scalability-and-performance-considerations"></a>可伸缩性和性能注意事项

应用程序托管的媒体自动程序需要以下可伸缩性和性能注意事项：
- 与邮件自动程序 (，应用程序托管的媒体) 需要更多的计算和网络带宽，并且可能会产生更高的运营成本。 实时媒体自动程序开发人员必须仔细衡量机器人的可伸缩性，并确保机器人不接受多于它可以管理的并发呼叫数。 如果使用的是"原始"RGB24 或 NV12 视频格式，则启用视频的机器人只能维持每个 CPU 内核的一个或两个并发媒体 (。) 。
- 实时媒体平台当前不会利用 VM 上提供的任何图形处理单元 (GPU) 以对 H.264 视频编码/解码进行非负载处理。 相反，视频编码和解码在 CPU 上的软件中完成。 如果 GPU 可用，机器人可能会利用它来呈现自己的图形，例如，如果机器人使用的是 3D 图形引擎。
- 托管实时媒体机器人的 VM 实例必须至少具有 2 个 CPU 内核。 对于 Azure，建议使用 Dv2 系列虚拟机。 对于其他 Azure VM 类型，具有四个虚拟 CPU (vCPU) 是所需的最小大小。 Azure 文档中提供了有关 Azure VM 类型 [的详细信息](/azure/virtual-machines/windows/sizes-general)。 

## <a name="code-sample"></a>代码示例

应用程序托管的媒体机器人示例如下所示：

| **示例名称** | **说明** | **Graph** |
|------------|-------------|-----------|
| 本地媒体示例 | 说明不同本地媒体方案的示例。 | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples) |
| 远程媒体示例 | 演示不同远程媒体方案的示例。 | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/RemoteMediaSamples) |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [支持的媒体格式](~/resources/media-formats.md)

## <a name="see-also"></a>另请参阅

- [Graph调用 SDK 文档](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
- 机器人需要比消息机器人更多的计算和网络带宽容量，并且会产生更高的运营成本。 实时媒体自动程序开发人员必须仔细衡量机器人的可伸缩性，并确保机器人不接受多于它可以管理的并发呼叫数。 如果使用原始 RGB24 或 NV12 视频格式，启用视频的机器人只能维持每个 CPU 内核的一个或两个并发媒体会话。
- 实时媒体平台当前不会利用 VM 上提供的任何图形处理单元 (GPU) 以对 H.264 视频编码或解码进行非负载处理。 相反，视频编码和解码在 CPU 上的软件中完成。 如果 GPU 可用，则机器人会利用它来呈现自己的图形，例如，如果机器人使用的是 3D 图形引擎。
- 托管实时媒体机器人的 VM 实例必须至少具有 2 个 CPU 内核。 对于 Azure，建议使用 Dv2 系列虚拟机。 对于其他 Azure VM 类型，具有 4 个虚拟 CPU (vCPU) 是所需的最小大小。 有关 Azure VM 类型详细信息，请参阅 [Azure 文档](/azure/virtual-machines/windows/sizes-general)。

下一节提供了说明不同本地媒体方案的示例。

## <a name="samples-and-additional-resources"></a>示例和其他资源

- [示例应用程序](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples)
- [Graph SDK 文档](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)