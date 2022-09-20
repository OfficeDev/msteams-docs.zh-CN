---
title: 准备使用 Teams 工具包生成应用
author: surbhigupta
description: 本文介绍如何在开发人员门户中生成 Teams 工具包环境和管理应用
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: dc3a51d393a6445c26dddd54c471ecb630580b94
ms.sourcegitcommit: dccb48902e08484692ab927415bcd3d61dc50db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2022
ms.locfileid: "67806906"
---
# <a name="prepare-to-build-apps-using-teams-toolkit"></a>准备使用 Teams 工具包生成应用

Teams 工具包支持用于创建应用的环境。 Teams 工具包还有助于在你构建的 Teams 应用中集成Azure Functions功能和云服务。

:::image type="content" source="../assets/images/buildapps-TTK.png" alt-text="准备使用 Teams 工具包生成应用":::

## <a name="build-environments"></a>生成环境

Microsoft Visual Studio Code中的 Teams 工具包提供一组环境来生成 Teams 应用。 可以选择以下最适合应用的下列环境中的任何人：

* JavaScript 或 TypeScript
* SharePoint 框架 (SPFx) 

### <a name="create-your-teams-app-using-javascript-or-typescript"></a>使用 JavaScript 或 TypeScript 创建 Teams 应用

使用 JavaScript 生成的应用具有以下优势：

* 应用附带其自己的 UI 和 UX 功能，这些功能丰富且用户友好。
* 提供对现有应用的快速升级。
* 在多个平台（如 Android 和 iOS）上分发应用。
* 与创建具有现有 API 的应用兼容。

Visual Studio Code中的 Teams 工具包支持使用 JavaScript 或 TypeScript 生成以下应用：

* Tab 应用：选项卡应用可以包含基于 Web 的内容，你可以在 Teams 中为 Web 内容设置自定义选项卡，或将特定于 Teams 的功能添加到 Web 内容。
* 机器人应用：机器人可以是聊天机器人或聊天机器人，可用于执行简单且重复的任务，如客户服务或支持人员。
* 通知机器人：可以使用 HTTP 请求通过通知机器人在 Teams 频道、组或个人聊天中发送消息。
* 命令机器人：可以使用命令机器人自动执行重复任务。 命令机器人可帮助你解答聊天中发送的简单查询或命令。
* 消息扩展：可以通过按钮和表单与 Web 服务交互。 消息扩展提供的功能。

### <a name="create-your-teams-app-using-spfx"></a>使用 SPFx 创建 Teams 应用

Visual Studio Code中的 Teams 工具包允许你使用 SPFx 创建选项卡应用。 这些应用具有以下优势：

* 提供与驻留在 SharePoint 中的数据与 Teams 的轻松集成。
* 可以将 SPFx 解决方案与受 Microsoft Azure Active Directory (Azure AD) 保护的业务 API 集成。
* 为你提供各种开源工具的访问权限。
* 为能够提供出色 UX 的强大应用程序创建。
* 与其他 Microsoft (Office) 365 工作负载轻松集成。
* 根据需要灵活地托管应用程序。

## <a name="support-for-azure-functions"></a>支持Azure Functions

可以使用 Teams 工具包将[Azure Functions](/azure/azure-functions/functions-overview)功能集成到构建应用中。 可以专注于最重要的代码片段，Azure Functions执行其余操作。
Azure Functions允许你实现：

1. 系统逻辑进入现成的代码块。 这些块称为函数。
1. 随着请求的增加，Azure Functions根据需要满足要求。

Azure Function 与 [云服务](add-resource.md#types-of-cloud-resources) 数组集成，提供功能丰富的实现。 下面只是Azure Functions的一些常见方案：

* 生成 Web API 时
* 处理数据库更改
* 处理 Iot 数据流
* 管理消息队列

## <a name="see-also"></a>另请参阅

* [Visual Studio 的Teams工具包](visual-studio-overview.md)
* [使用开发人员门户管理 Teams 应用](../concepts/build-and-test/teams-developer-portal.md)
* [使用 Teams 工具包创建新的 Teams 应用](create-new-project.md)
