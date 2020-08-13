---
title: 构建你的第一个团队应用
author: heath-hamilton
description: 构建真实 Microsoft 团队应用程序的教程
ms.openlocfilehash: 4915dde4ef5a852f4fc5d1e4c83e3349db2eaf6b
ms.sourcegitcommit: 80bf79a952bb14cbc38c0bd1e3cf8a346158e28e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2020
ms.locfileid: "46655672"
---
# <a name="learn-how-to-build-your-first-teams-app"></a>了解如何构建你的第一个团队应用

在 "**构建您的第一个应用程序**" 中，您将了解如何通过教程创建基本的团队应用程序。 本课将相互构建，指导您完成创建简单的实际团队应用程序的每个步骤。 我们将向你介绍常见工具、基本概念以及相关方法的有用链接。

首先，创建并运行 "Hello，World！"。 选项卡应用。 然后，你将创建一些简单的 UI，并了解如何使用 Microsoft 团队 Javascript SDK 获取有用的上下文。

## <a name="what-youll-learn"></a>你将了解的内容

> [!div class="checklist"]
  >
  > - **使用团队工具包快速启动和运行**： Visual Studio 代码的 Microsoft 团队工具包负责创建您的应用程序项目和基架，以便您可以在几分钟内运行应用程序。
  > - **使用清单定义您的应用程序**：清单是一个蓝图，可在其中指定团队应用使用的功能和服务。
  > - **确定访问群体的范围**：您可以构建一个工作组应用程序以供个人使用或协作。 在教程中，你将了解如何为单个用户或频道或聊天中的一组人员构建一个选项卡。
  > - **利用团队 SDK 获取上下文**：了解如何使用 Microsoft 团队 JavaScript SDK 执行主题更改或设置配置体验  
  > - **在您的应用程序上展开**：在整个教程中，我们将链接到您可能感兴趣的相关主题 (其中包括身份验证和设计准则) 。

## <a name="teams-app-fundamentals"></a>团队应用程序基础

在开始教程之前，您应该了解以下有关为团队生成应用程序的信息。

### <a name="apps-can-have-multiple-capabilities"></a>应用可以有多种功能

团队应用程序由一个或多个[平台功能](../capabilities-overview.md)组成，包括[选项卡](../doc-links/what-are-tabs.md)、 [bot](../doc-links/what-are-bots.md )、[邮件扩展](../doc-links/what-are-messaging-extensions.md)和[webhook 和连接器](../doc-links/what-are-webhooks-and-connectors.md)。 团队应用程序还具有许多[UI 约定和元素](../doc-links/teams-ui-conventions.md)（如卡片、任务模块和深层链接），您可以使用它们生成最佳的用户体验。

对于这些教程，你将仅构建选项卡，但可以根据需要将机器人或其他功能添加到你的应用。

### <a name="teams-doesnt-host-your-app"></a>团队不会托管您的应用程序  

团队应用程序包含三个主要部分：

1. Microsoft 团队客户端 (web、桌面或移动) ，用户与您的应用程序进行交互。
1. 执行必要的逻辑、数据存储和 API 调用以对应用程序供电的应用程序、服务、工作流或网站。
1. 您的应用程序包，可用于在团队中安装应用程序。 它包含应用程序元数据 (名称、图标等，以及指向服务的 ) 和指针。

## <a name="next-step"></a>后续步骤

这就是我们现在开始的一切吧！

> [!div class="nextstepaction"]
> [生成并运行您的第一个应用程序](build-and-run-with-toolkit.md)
