---
title: 应用程序托管的媒体机器人的要求和注意事项
description: 了解与使用代码示例和样本为 Microsoft Teams 创建应用程序托管的媒体机器人相关的重要要求和注意事项，以及可扩展性和性能。
ms.topic: conceptual
ms.localizationpriority: medium
keywords: 应用程序托管的媒体 Windows 服务器 Azure VM
ms.date: 11/16/2018
ms.openlocfilehash: 987bb26ba7ad91f11228f7072d3e268ebd87dc5a
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2022
ms.locfileid: "65756609"
---
# <a name="requirements-and-considerations-for-application-hosted-media-bots"></a>应用程序托管的媒体机器人的要求和注意事项

应用程序托管的媒体机器人需要 [`Microsoft.Graph.Communications.Calls.Media` .NET 库](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) 才能访问音频和视频媒体流。机器人必须部署在 Windows Server 本地计算机或 Azure 中的 Windows Server 来宾操作系统 (OS) 上。

> [!NOTE]
>
> * 开发消息传递和互动语音响应 (IVR) 机器人的指南并不完全适用于构建应用程序托管的媒体机器人。
> * 由于适用于机器人的 Microsoft 实时媒体平台是开发人员预览版，因此本文档中的指南可能会更改。

## <a name="c-or-net-and-windows-server-for-development"></a>用于开发的 C# 或 .NET 和 Windows 服务器

应用程序托管的媒体机器人需要满足以下条件：

* 机器人必须在 C# 和标准的 .NET Framework 中开发并部署在 Microsoft Azure 中。 不能使用 C++ 或 Node.js API 访问实时媒体，应用程序托管的媒体机器人不支持 .NET 核心。

* 机器人可以托管在以下 Azure 服务环境之一中：
  * 云服务。
  * 使用虚拟机规模集 (VMSS) 的 Service Fabric。
  * 基础结构即服务 (IaaS) 虚拟机 (VM)。  
  
* 无法将机器人部署为 Azure Web 应用。

* 机器人必须在最新版本的 `Microsoft.Graph.Communications.Calls.Media` .NET 库上运行。 机器人必须使用最新版本的 [NuGet 工具包](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)，或不超过三个月的版本。 库的较旧版本已弃用，几个月后将不起作用。 使 `Microsoft.Graph.Communications.Calls.Media` 库保持最新状态可确保机器人与 Microsoft Teams 之间的最佳互操作性。

下一部分提供有关实时媒体调用所在位置的详细信息。

## <a name="real-time-media-calls-stay-where-theyre-created"></a>实时媒体呼叫保留创建位置

实时媒体调用保留在创建它们的计算机上。 实时媒体调用固定到已接受或启动调用的虚拟机 (VM) 实例。 来自 Microsoft Teams 调用或会议的媒体流向该 VM 实例，机器人发送回 Microsoft Teams 的媒体也必须来自该 VM。 如果 VM 停止时有任何实时媒体调用正在进行，这些调用会立即终止。 如果机器人事先知道挂起的 VM 关闭，则可以结束调用。

下一部分提供有关应用程序托管的媒体机器人的辅助功能的详细信息。

## <a name="application-hosted-media-bots-accessible-on-the-internet"></a>可在 Internet 上访问的应用程序托管的媒体机器人

必须直接在 Internet 上访问应用程序托管的媒体机器人。 这些机器人必须包括以下功能：

* 必须使用实例级公共 IP 地址 (ILPIP) 直接从 Internet 访问在 Azure 中托管应用程序托管媒体机器人的每个 VM 实例。
  * 要获取和配置 Azure 云服务的 ILPIP，请参阅[实例级公共 IP 经典概述](/azure/virtual-network/virtual-networks-instance-level-public-ip)。
  * 要为 VM 规模集配置 ILPIP，请参阅[每台虚拟机的公共 IPv4](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking#public-ipv4-per-virtual-machine)。
* 托管应用程序托管媒体机器人的服务还必须使用映射到特定实例的面向公众的端口配置每个 VM 实例。
  * 对于 Azure 云服务，这需要实例输入端点。 有关详细信息，请参阅[为 Azure 中的角色实例启用通信](/azure/cloud-services/cloud-services-enable-communication-role-instances)。
  * 对于 VM 规模集，必须在负载均衡器上配置 NAT 规则。 有关详细信息，请参阅 [Azure 中的虚拟网络和虚拟机](/azure/virtual-machines/windows/network-overview)。

* “机器人框架模拟器”不支持应用程序托管的媒体机器人。

下一部分提供有关应用程序托管媒体机器人的可扩展性和性能注意事项的详细信息。

## <a name="scalability-and-performance-considerations"></a>可伸缩性和性能注意事项

应用程序托管的媒体机器人需要考虑以下可扩展性和性能注意事项：

* 与消息传送机器人相比，应用程序托管媒体机器人需要更多的计算和网络 (带宽) 容量，并且可能会产生更高的运营成本。 实时媒体机器人开发人员必须仔细衡量机器人的可扩展性，并确保机器人不会接受比它所能管理的更多的同时呼叫。 启用视频的机器人的每个 CPU 内核只能维持一两个并发媒体会话（如果使用“原始”RGB24 或 NV12 视频格式）。
* 实时媒体平台当前不会利用 VM 上可用的任何图形处理单元 (GPU) 来卸载 H.264 视频编码/解码。 相反，视频编码和解码在软件的 CPU 中完成。 如果 GPU 可用，机器人可能会利用它进行自己的图形呈现，例如，如果机器人使用 3D 图形引擎。
* 托管实时媒体机器人的 VM 实例必须至少有 2 个 CPU 内核。 对于 Azure，建议使用 Dv2 系列虚拟机。 对于其他 Azure VM 类型，具有四个虚拟 CPU (vCPU) 的系统是所需的最小配置。 有关 Azure VM 类型的详细信息，请参阅 [Azure 文档](/azure/virtual-machines/windows/sizes-general)。

## <a name="code-sample"></a>代码示例

应用程序托管的媒体机器人示例如下所示：

| **示例名称** | **说明** | **Graph** |
|------------|-------------|-----------|
| 本地媒体示例 | 演示不同本地媒体方案的示例。 | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples) |
| 远程媒体示例 | 演示不同远程媒体方案的示例。 | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/RemoteMediaSamples) |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [支持的媒体格式](~/resources/media-formats.md)

## <a name="see-also"></a>另请参阅

* [Graph 调用 SDK 文档](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
* 与消息传送机器人相比，机器人需要更多的计算和网络带宽容量，并产生更高的运营成本。 实时媒体机器人开发人员必须仔细衡量机器人的可扩展性，并确保机器人不会接受比它所能管理的更多的同时呼叫。 如果使用原始 RGB24 或 NV12 视频格式，启用视频的机器人的每个 CPU 内核只能维持一两个并发媒体会话。
* 实时媒体平台当前不会利用 VM 上可用的任何图形处理单元 (GPU) 来卸载 H.264 视频编码或解码。 相反，视频编码和解码在软件的 CPU 中完成。 如果 GPU 可用，机器人会利用它进行自己的图形呈现，例如，如果机器人使用 3D 图形引擎。
* 托管实时媒体机器人的 VM 实例必须至少有 2 个 CPU 内核。 对于 Azure，建议使用 Dv2 系列虚拟机。 对于其他 Azure VM 类型，具有 4 个虚拟 CPU (vCPU) 的系统是所需的最低配置。 有关 Azure VM 类型的详细信息，请参阅 [Azure 文档](/azure/virtual-machines/windows/sizes-general)。

下一部分提供了说明不同本地媒体应用场景的示例。

## <a name="samples-and-additional-resources"></a>示例和其他资源

* [示例应用程序](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples)
* [Graph 调用 SDK 文档](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
