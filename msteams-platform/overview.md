---
title: Microsoft Teams 开发人员平台
author: clearab
description: 介绍 Microsoft 团队开发人员平台的概述页面，以及如何开始为 Microsoft 团队构建应用程序。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: cb9d91f2de29bac00f4cdcd9672adf9d7d4ee734
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673491"
---
# <a name="what-are-microsoft-teams-apps"></a>什么是 Microsoft 团队应用？

Microsoft 团队是 Office 365 中的协作工作区，它与用户使用的应用程序和服务集成，以实现共同完成的工作。 Microsoft 团队开发人员平台使开发人员可以轻松地集成自己的应用程序和服务，以提高工作效率、更快地做出决策、提供焦点（通过减少上下文切换），并围绕现有内容创建协作并流会. 在 Microsoft 团队平台上构建的应用程序是团队客户端和您的服务和工作流之间的桥梁;将它们直接引入协作平台的上下文中。

## <a name="what-can-teams-apps-do"></a>团队应用程序可以做什么？

基于 Microsoft 团队平台构建的应用主要侧重于提高协作能力和提高生产率。 您的应用程序可能很简单，如从其他系统发布通知或复杂的多面应用程序。 只需记住，团队就是社会协作平台;最佳应用重点是帮助人员自己快速学习并更好地协同工作。

* **对外部系统中的项目进行协作。** 自定义团队应用程序的一个核心方案是，将信息或项目从某个其他地方引入到团队中，并围绕它进行对话。 您可以将信息推送到团队中，使用户能够按需搜索和请求，或使其在嵌入的 web 视图中可用。

* **触发对话中的工作流。** 通常，对话会导致需要启动一些工作流或完成某些操作;请记下有关这一点的说明，查看我的拉取请求，将其转换为销售线索等。您的团队应用可以在团队内部将访问工作流。

* **将重要事件的团队通知给团队。** 电子邮件通知的病假？ 改为向团队发送通知！ 将通知直接发送给用户、频道、活动源或订阅邮件的任何人。

* **从其他网站/服务嵌入功能。** 有时，您只需让您的应用程序更易于发现。 嵌入现有的单页面应用程序，或为团队从头开始构建一些内容。

## <a name="how-do-teams-apps-work"></a>团队应用程序的工作原理是什么？

有关 Microsoft 团队的自定义应用程序的第一件事（除了可以令人惊奇），团队不是托管服务。 您的应用程序包包含有关您的应用程序（名称、图标等）的元数据，以及指向承载该应用程序的 web 服务的指针。 Microsoft 团队提供了分发机制、UI/UX 构造以供您利用，并且您可以使用 Api 来扩充可用于您的应用程序的信息和操作。

团队应用程序包含三个主要部分：

* 用户将与您的应用程序进行交互**的 Microsoft 团队客户端（web、桌面或移动版）** 。
* **您的团队应用程序包**，用于创建用户安装的应用程序，并包含应用程序的元数据和指向服务的指针。
* 执行必要逻辑的**服务、工作流或网站**对应用程序供电的数据存储和 API 调用。

请务必记住，您在 Microsoft 团队应用程序中公开的任何功能在 internet 上都是公开的，除非您采取其他步骤来保护它。 如果你要提供对机密或受保护信息的访问权限，你需要确保你的服务至少对连接到你的应用的终结点进行身份验证，或对[你的用户进行身份验证](~/concepts/authentication/authentication.md)。

## <a name="how-can-you-share-your-teams-app"></a>如何共享你的团队应用？

当您准备好共享 Microsoft 团队应用程序时，您有三个选项，具体取决于您的目标访问群体。

* **[直接上载您的应用程序](~/concepts/deploy-and-publish/apps-upload.md)** 如果您的应用程序只需要与您的团队或组织中的少数几个人共享您的应用程序，则可以共享您的应用程序包并直接上载它。
* **[发布到你的组织应用程序目录](~/concepts/deploy-and-publish/apps-publish.md)** 您可以通过您的应用程序目录与整个组织共享您的应用程序。
* **[发布到公用应用商店](~/concepts/deploy-and-publish/apps-publish.md)** 如果你的应用程序适用于所有人，你可以将其发布到我们的公共应用商店。 根据你的目标，你可能有资格获取市场营销和销售帮助。

## <a name="get-started"></a>入门

* [在 C 中构建 bot 和选项卡应用#](~/tutorials/get-started-dotnet-app-studio.md)
* [构建 JavaScript/node.js 中的 bot 和选项卡应用程序](~/tutorials/get-started-nodejs-app-studio.md)

## <a name="learn-more"></a>了解更多

* [团队客户端中的可扩展性点](~/concepts/extensibility-points.md)
* [构建团队相关应用程序](~/concepts/building-an-app.md)
