---
title: 卡片和任务模块
description: 了解Teams机器人中支持的卡片类型，例如自适应卡片、英雄卡片和缩略图卡及其操作。
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 4f2f964307c4cc8dbd3033b52af88a9b2c38d474
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143933"
---
# <a name="cards-and-task-modules"></a>卡片和任务模块

卡片为用户在对话流中提供各种视频、音频、可选消息以及帮助。

使用任务模块，可以在 Microsoft Teams 中创建模式弹出体验。 对于启动和完成任务，或者显示视频或 Power 商业智能 (BI) 仪表板之类的丰富信息来说尤其有用。

Teams 机器人支持以下类型的卡片：

* 自适应卡片
* 主图卡片
* 列表卡
* Office 365 连接器卡
* 收据卡
* 登录卡
* 缩略图卡片
* 卡片集合

可以使用 XML 或 HTML 格式的子集或 Markdown 对卡片文本进行格式设置，具体取决于卡类型。

[自适应卡片中的人员选取器](cards/people-picker.md)有助于在聊天或频道中搜索、选择、重新分配和预选用户。

可以添加和响应以下卡片操作：

* 打开 URL。
* 将消息和有效负载发送到机器人。
* 启动 OAuth 流。

可以在大型数据集中使用自适应卡片中的超前类型控制提供 [动态搜索](~/task-modules-and-cards/cards/dynamic-search.md) 体验，并在有限数量的选择内执行超前类型静态搜索。 在频道或个人选项卡、机器人或深层链接中调用任务模块。 通过将任务模块添加到用户的选项卡，可以改善用户对需要数据输入的工作流的体验。可以使用自适应卡片和机器人框架卡上的按钮从 Teams机器人调用任务模块。

## <a name="see-also"></a>另请参阅

* [卡片](~/task-modules-and-cards/what-are-cards.md)
* [任务模块](~/task-modules-and-cards/what-are-task-modules.md)
