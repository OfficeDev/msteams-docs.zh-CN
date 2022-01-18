---
title: Microsoft Teams文档 - 术语表
description: 开发人员文档Microsoft Teams术语表
ms.localizationpriority: medium
ms.topic: reference
keywords: Microsoft Teams开发人员定义
ms.openlocfilehash: 0858d0cfb246e99871c02f81c82c1eaa30bb6edf
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059827"
---
# <a name="glossary"></a>术语表

开发人员文档中使用的Teams和定义。
<br>
<br>
<details>
<summary>A</summary>

| Term | 定义 |
| --- | --- |
| 操作命令 | 操作命令用于向用户显示用于收集或显示信息的模式弹出窗口。 <br>**另请参阅**：消息传递扩展;搜索命令 |
| 自适应卡片 | 自适应卡片是内容可操作的代码段，可以通过机器人或消息传递扩展添加到对话中。 这些卡片使用文本、图形和按钮为受众提供丰富的通信体验。 |
| 应用程序目录 | 应用程序目录用于存储适用于 SharePoint 和 Office 的应用程序，供组织内部使用。 |
| 应用部件清单 | Teams应用清单介绍了应用如何集成到 Microsoft Teams 产品。 清单必须符合 托管在 的架构 https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json 。 |
| 应用包 | 应用Teams包是一个 zip 文件，其中包含应用清单文件和应用图标 - 颜色图标和大纲图标。 |
| 应用权限 | 应用中的"应用Teams"选项允许你为应用启用应用的设备权限。 仅在应用的清单文件声明应用需要设备权限时可用。 <br> **另请参阅**：设备权限 |
| 应用程序范围 | 应用范围确定你的应用如何与用户交互。 应用可以具有个人范围、频道范围或团队作用域。 一Teams应用程序可以跨范围存在。 |
| 应用程序 Studio | App Studio 是一款应用，可开始创建或集成自己的Microsoft Teams应用。 它现在已发展为开发人员门户。 <br> **另请参阅**：开发人员门户 |
| Azure 资源 | 可通过 Azure 使用的服务，Teams应用可用于 Azure 部署。 它可以是存储帐户、Web 应用、数据库等。 |
| Azure Active Directory | Azure Active Directory (Azure AD) Microsoft 基于云的标识和访问管理服务。 它可帮助经过身份验证的用户访问内部和外部 Azure 资源的资源。 |
| 身份验证 | 身份验证是授权用户访问应用的一个过程。 可以使用 Microsoft Graph API 或基于 Web 的身份验证完成。 <br> **另请参阅**：标识提供程序 |
| 身份验证流 | 在Teams，有两种不同的身份验证流来验证用户使用应用：基于 Web 的身份验证和 OAuthPrompt 流。 |
|
</details>
<br>
<details>
<summary>B</summary>

| Term | 定义 |
| --- | --- |
| Blazor | Blazor 是一个免费的开源 Web 框架，使开发人员能够使用 C# 和 HTML 创建 Web 应用。 它允许你使用 C# 而不是 JavaScript 生成交互式 Web UIs。 Blazor 应用程序由使用 C#、HTML 和 CSS 实现的可重用 Web UI 组件组成。 它由 Microsoft 开发。 |
| Bicep | Bicep 是一种声明性语言，这意味着元素可以按任何顺序显示。 与强制性语言不同，元素的顺序不会影响部署的处理方式。 |
| Bot | 自动程序是执行编程的重复任务的应用。 <br> **另请参阅**：对话机器人;聊天机器人 |
| 自动Emulator | Bot Framework Emulator是一个桌面应用程序，允许你在本地或远程测试和调试机器人。 |
| 机器人框架 | Bot Framework 是一个丰富的 SDK，用于创建使用 C#、Java、Python 和 JavaScript 的聊天机器人。 如果你已有基于 Bot Framework 的自动程序，你可以轻松修改它以在 Teams。 |
</details>
<br>
<details>
<summary>C</summary>

| Term | 定义 |
| --- | --- |
| 呼叫机器人 | 参与音频或视频通话和联机会议的机器人。 <br> **另请参阅**：聊天机器人;会议机器人 |
| 功能 | 应用的功能称为Teams功能。 应用可能有一个或多个核心功能，如选项卡、机器人、消息传递扩展。 <br>**另请参阅**：设备功能;媒体功能 |
| 聊天机器人 | 聊天机器人也称为聊天机器人或对话机器人。 该应用由客户服务或支持人员等用户运行简单而重复的任务。 <br> **另请参阅**：对话机器人。 |
| 频道 | 频道是团队共享消息、工具和文件的单一位置。 在Teams中，团队协作和通信通过渠道实现。  |
| 客户端密码 | 客户端密码/密码或作为证书的公钥或私钥对。 这不是本机应用的必需项。 <br> **另请参阅**： Bot |
| 云资源 | 通过 Internet 在云中可用的服务，Teams应用可以使用。 它可以是存储帐户、Web 应用、数据库等。 |
| 协作应用 |  <br> **另请参阅**：独立应用 |
| 连接器 |  <br> **另请参阅**：Webhooks |
| 对话 | 对话是在自动程序与一个或多个用户Microsoft Teams发送的一系列消息。 对话可以有三个范围：频道、个人聊天和群聊。 <br>**另请参阅**：一对一聊天;群聊 |
| 对话机器人 |  对话机器人允许用户使用文本、交互式卡片和任务模块与 Web 服务交互。 <br>**请参阅 aso** 聊天机器人 |