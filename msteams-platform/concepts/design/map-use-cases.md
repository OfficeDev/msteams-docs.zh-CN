---
title: 将用例映射到 Teams 应用特性和功能
author: surbhigupta
description: 确定应用的用例如何在 Teams 体验、应用功能和功能中工作; 使用功能映射常见用例。
ms.topic: conceptual
ms.localizationpriority: high
ms.author: anclear
ms.openlocfilehash: 9fdf2c56bab0a822d0c3769d6d7e9fdb6aa3a929
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103325"
---
# <a name="map-your-use-cases-to-teams-app-features"></a>将用例映射到 Teams 应用功能

定义完善的用例可帮助你绘制出 Teams 应用中所需的功能框架。 确定用户要求后，定义最适合你的应用的范围和 Teams 功能。

可以根据以下情况映射用例:

* 在外部系统中共享和协作处理项目。
* 启动工作流并向用户发送通知。
* 使用社交平台、对话机器人和组合多个功能。

## <a name="common-use-cases-mapped-to-teams-capabilities"></a>映射到 Teams 功能的常见用例

下一步是将用例与应用功能进行匹配。

下面是映射到 Teams 功能的常见用户方案列表。 这不是一个详尽的列表，但可以帮助你思考一些可供你使用的可能性。
</br>
</br>
<details>
<summary>创建、共享和协作处理外部系统中的项</summary>

用于与数据交互的应用

| **如果你想要...** | **试用...** |
| --- | --- |
| 搜索外部系统，并将结果共享为交互式卡片。 | 使用搜索命令的消息扩展 |
| 收集信息以插入数据存储或运行高级搜索。 | 使用操作命令的消息扩展 |
| 创建嵌入式 Web 体验以查看、处理和共享数据。 | 选项卡 |
| 推送数据并从 Teams 客户端发送数据。 | 连接器和 Webhook|
| 可从需要它们的任何位置收集或显示信息的交互式模式窗体。 | 任务模块 |

</details>
</br>
<details>
<summary>启动工作流和程序</summary>

在外部系统中启动进程或工作流的快速方法。

| **如果你想要...** | **试用...** |
| --- | --- |
| 触发消息，使用户能够快速将邮件内容发送到 Web 服务。 | 消息扩展操作命令 |
| 在启动工作流之前，打开来自选项卡、机器人或消息扩展的消息以收集信息。 | 任务模块 |
| 通过文本和富卡与用户交互。 | 对话机器人 |
| 在无需生成完整会话机器人时，这适合进行简单的来回交互。 |  传出 webhook |

</details>
</br>
<details>
<summary>发送通知和警报</summary>

在 Teams 中向用户发送异步通知和警报。

| **如果你想要...** | **试用...** |
| --- | --- |
| 向组、频道或单个用户发送主动消息。 | 对话机器人 |
| 允许频道订阅以接收消息。 连接器允许用户通过配置页定制订阅。 | 连接器和传入 Webhook |

</details>
</br>
<details>
<summary>提出问题并获取答案</summary>

与用户联系并解析其查询

| **如果你想要...** | **试用...** |
| --- | --- |
| 自然语言处理、AI、机器学习和所有流行语。 使用智能云支持的机器人将用户连接到所需的答案。 | 对话机器人 |
| 在 Teams 中嵌入现有 Web 门户，或创建 Teams 特定版本以添加功能。 | 选项卡 |

</details>

## <a name="app-capabilities-mapped-to-features"></a>映射到功能的应用功能

Microsoft Teams 平台提供各种功能。 每项功能都是一种与用户交互的方式，使 Teams 应用功能与用户需求相关。

让我们看看 Teams 功能如何为应用启用不同的功能。

:::image type="content" source="../../assets/images/overview/teams-apps-capabilities.png" alt-text="显示 Teams 功能的图像" border="true":::

例如：

* 使用 **选项卡** 功能显示任务模块、请求设备权限、显示<`iframe`>内容或使用深层链接。
* 使用 **消息扩展** 功能发送卡片、展开链接或对消息执行操作。

## <a name="see-also"></a>另请参阅

* [计划清单](../design/planning-checklist.md)
* [构建第一个 Microsoft Teams 应用](../../get-started/get-started-overview.md)
