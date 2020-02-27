---
title: Microsoft 团队应用程序模板
description: Microsoft 团队平台的应用程序模板的链接和说明
keywords: Microsoft 团队模板示例演示
ms.openlocfilehash: b8f38020761cfff7cd821694ffba2d85d2d925d1
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673264"
---
# <a name="app-templates-for-microsoft-teams"></a>Microsoft 团队的应用程序模板

应用程序模板是 Microsoft 团队的已准备好的应用程序，这些应用程序是社区驱动的开放源代码、开放源代码和在 GitHub 上可用的 Microsoft 团队。 每个都包含为您的组织部署和安装该应用程序的详细说明，提供可供安装并立即开始使用的现成应用程序。 完整的源代码也是可用的，因此您可以对其进行详细研究，也可以对代码进行更改，以满足您的特定需求。

## <a name="key-benefits-of-using-app-templates"></a>使用应用程序模板的主要好处

* **即插即用体验：** 所有应用程序模板都包含可让您在 Microsoft Azure 中托管所有必要服务的部署脚本。 部署应用程序不需要任何编码。
* **生产-就绪代码：** 应用程序模板符合建议的安全和基础结构最佳做法，并对其提交的所有社区更改进行检查，以确保继续符合标准。
* **可自定义和扩展：** 虽然所有应用程序模板都准备好部署，但我们提供了完整的代码库和部署脚本，以便您可以轻松地自定义或扩展它们以满足您的独特需求。
* **& 支持的详细文档：** 所有应用程序模板都附带了有关解决方案体系结构、部署和配置步骤的端到端文档。 存储库也将受到监视，因此，请通过在 GitHub 上提出问题来报告遇到的任何问题。

## <a name="celebrations"></a>Celebrations

Celebrations 是一种团队应用，可帮助工作组成员庆祝他人的生日、周年纪念和其他定期事件。 它会记住所有团队成员的特殊情况，并在创建事件时在选择的所有团队中发送一封友好的消息，以使工作组成员在自己的日期中感到特别。

该应用程序为所有团队成员提供了一个简单的界面，以供个人添加和查看他们的事件，还允许用户选择共享事件的团队。

[请在 GitHub 上获取它](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="company-communicator"></a>公司 Communicator

公司 Communicator 应用程序使公司团队能够创建和发送邮件，以供多个团队或大量员工通过聊天，使组织能够向员工进行协作。 将此模板用于多种方案，如新的计划通知、员工加入、新式学习和开发或组织范围的广播。

该应用程序为指定用户提供了用于创建、预览、协作和发送邮件的简单界面。

它提供了构建自定义的目标通信功能（如自定义遥测）对邮件进行了多少用户的确认或交互的基础。

[请在 GitHub 上获取它](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![FAQ 加 gif](~/assets/images/CompanyCommunicatorCompose.png)

## <a name="faq-plus"></a>常见问题解答加上

对话 Q&bot 是一种简单的方法，可提供用户对常见问题的解答。 但是，大多数 bot 无法以有意义的方式与用户接洽，因为在 bot 发生故障时没有人在循环中。 FAQ bot 是一个友好的 Q，&在无法帮助的情况中将人体带到循环中的 bot。 如果某个问题包含在知识库中，则可以向该 bot 提供一个问题，并且机器人会做出响应。 如果不是，则机器人允许用户提交一个查询，然后将其发布到预先配置的专家团队中，这些专家将通过在团队内部对通知进行操作来提供支持。

[请在 GitHub 上获取它](https://github.com/OfficeDev/microsoft-teams-faqplusplus-app)

![FAQ 加 gif](~/assets/images/FAQPlusEndUser.gif)

## <a name="hr-support"></a>HR 支持

HR 支持机器人是一个友好的 Q&一个 bot，它将支持专业人员/专家从循环中的 HR 团队中引入帮助。 如果某个问题包含在知识库中，则可以向该 bot 提供一个问题，并且机器人会做出响应。 如果不是，则机器人允许用户提交一个查询，然后将其发布到预先配置的专家团队中，这些专家将通过在团队内部对通知进行操作来提供支持。 此外，机器人通过在问题中搜索预配置的标记来建议指向建议的 HR 策略/问题的链接。 此外，还可以在关联的选项卡中找到这些磁贴作为快速参考。 HR 支持适用于轻型 QnA，并可在组织中启动新项目/计划时提供快速支持。

[请在 GitHub 上获取它](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![HR 支持](~/assets/images/expert-user.png)

## <a name="list-search"></a>列表搜索

Microsoft 团队中的协作通常会引用 SharePoint 列表中项目中包含的信息。 只需粘贴指向相关项目的链接，即可强制每个人都切换上下文以离开对话，查找所需的信息，然后返回到团队以继续进行对话。 随着对话的持续不断，人们通常需要多次切换回参考项目，以验证新注释并刷新项目中包含的信息的记忆。 此上下文切换为平滑协作创建了一个障碍，并且是通过裂纹的方法实现的食谱。

为帮助缓解这一困难，我们很乐意向你推荐列表搜索应用程序模板。 数百万个用户使用 SharePoint 来为组织中的一些核心工作流加电。 但是，在列表方面进行协作可能会非常单调。 通过在 Microsoft 团队中使用列表搜索应用程序模板，用户可以直接在聊天对话中插入 SharePoint 列表项中的信息，以缓解在简单地将链接插入聊天时导致的上下文切换。 该信息作为一种易于阅读的自动格式化卡片插入，可帮助您的用户保持对话中的参与。

[请在 GitHub 上获取它](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![列表搜索应用程序](~/assets/images/list-search-template.png)

## <a name="custom-stickers"></a>自定义不干胶标签

自表达式是正常团队区域性的核心。 此应用程序模板是一种[消息扩展](~/messaging-extensions/what-are-messaging-extensions.md)，使用户能够在 Microsoft 团队中使用自定义不干胶标签和 gif。 此模板提供了简单的基于 web 的配置体验，其中任何具有配置访问权限的用户都可以上传他们希望最终用户拥有的 Gif/不干胶标签/图像，从而使整个团队能够使用您选择的任何一组不干胶标签。

此应用程序还可以跨团队轻松共享图像/Gif/不干胶标签，而无需像存储和共享机制那样访问 SharePoint 网站或单个通道。 例如，产品团队可以以编程方式轻松地将产品图像和 Gif 共享到社交媒体、市场营销和销售团队。 还可以通过触发新图像/Gif 时向特定团队/个人发出通知流来扩展此应用。

[请在 GitHub 上获取它](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![不干胶标签应用](~/assets/images/stickers.png)

## <a name="icebreaker"></a>Icebreaker

Icebreaker 是一种[Microsoft 团队 bot](~/bots/what-are-bots.md) ，可帮助您的团队更好地通过将两个随机团队成员与每周匹配来实现。 通过自动建议用于两个成员的空闲时间，机器人可简化日程安排。 加强个人连接并使用此应用构建一个紧密的 knit 社区。

除了鼓励整个团队中的个人连接，Icebreaker 应用还可以帮助您的组织内 cultivate 基于兴趣的社区。 例如，您可以将此应用用于 DevOps 兴趣组，以帮助在您的组织中分布的想法和最佳做法逐渐。

[请在 GitHub 上获取它](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Icebreaker 应用程序](~/assets/images/icebreaker.png)

## <a name="scrum-status-bot"></a>Scrum 状态 Bot

Scrum 状态 bot 是一个简单的 scrum 助手机器人，它使用户能够运行异步的独立式会议，并提供并轻松地让用户共享他们的每日更新。 它旨在在团队组聊天中工作，所有成员都可以参与 scrum。 一种方法可以开始和结束 scrum，并且可以在运行的 scrum 中查看其他人所做的更新。

[在 GitHub 上将其 Git 置于 GitHub 上](https://github.com/OfficeDev/microsoft-teams-app-scrumstatus/)

![Scrum 状态 Bot](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

您想要查看的应用程序模板有什么想法？ 请[在此处](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u)告知我们。