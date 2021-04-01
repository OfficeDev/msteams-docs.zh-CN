---
title: Microsoft Teams 应用模板
description: Microsoft Teams 平台的应用模板的链接和说明
ms.topic: reference
keywords: Microsoft Teams 模板示例演示
ms.author: lajanuar
author: laujan
ms.openlocfilehash: ac2062e8f62ee52a53c6e129301e2a5615110789
ms.sourcegitcommit: 3bd2627b7a334568f61ccc606395e3d89aa521d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "51475953"
---
# <a name="app-templates-for-microsoft-teams"></a>Microsoft Teams 的应用模板

应用模板是 Microsoft Teams 的完整应用示例，这些应用是开源的，可在 GitHub 上获取。 每个应用模板都包含有关为组织部署和安装该应用的详细说明。 它还提供一个示例应用，你可以立即安装并开始使用该应用。 完整的源代码也可用，这允许你详细浏览它或分叉代码，并更改它以满足你的特定要求。
所有应用模板都根据 MIT 许可 [条款](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE) 提供。
>[!NOTE] 
>你（而非 Microsoft）必须许可和支持使用用户和组织的应用模板创建的应用。

**&#9734;指示新发布的应用模板。**

### <a name="key-benefits"></a>主要优势

* **直接部署到云：** 所有应用模板均包括部署脚本，允许你在 Microsoft Azure 或 Power Platform 中托管所有必需服务。 
* **建议的示例代码：** 应用模板遵循有关安全性和基础结构的建议最佳做法。 审查所有社区提交的对应用模板的更改以确保一致性。
* **可自定义和可扩展：** 尽管所有应用模板都可以以最少的配置进行部署，但我们提供了整个代码库和部署脚本，以便你可以轻松自定义或扩展它们以满足你的独特需求。
* **详细文档：** 所有应用模板都附带了有关解决方案体系结构、部署和配置步骤的端到端文档。  

## <a name="adoption-bot-9734"></a>采用自动程序&#9734;

采用机器人是一种用户关注聊天机器人，使用 Power Virtual Agent for Teams (PVA) 。 它可视为常见问题增强版的 PVA 版本。 采用自动程序解答了有关 Microsoft 365 和 Teams 的 100 多个常见问题。 可以编辑现有主题、添加自己的主题以及加入现有常见问题解答。 如果用户需要其他帮助，采用机器人可以将其与专家联系，甚至可以扩展为使用高级流连接器打开服务票证。此机器人可以安装在它自己的上，也可以内置到自定义应用（如采用 [中心）中](https://github.com/akporzondek/adoption_hub)。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-adopt-bot)

## <a name="appointment-manager-9734"></a>约会管理器&#9734;

约会管理器是一个 Teams 应用模板，可帮助企业通过 Teams 创建、管理和与消费者进行虚拟约会。 来自客户的新约会请求在 Teams 频道中可见，可在 Teams 频道中快速分配这些请求并将其重新分配到团队中的员工。 可以通过自定义选项卡在团队或个人级别查看约会请求。 每个约会都与 Teams 联机会议关联，因此员工和使用者可以在计划的时间轻松加入会议。

该应用模板与 Microsoft Bookings 集成，便于进行约会管理。 安排的约会会自动显示在已分配员工成员的日历上，并且消费者通过嵌入的会议链接接收可自定义的电子邮件通知和提醒。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-appointment-manager)

![Teams 中的 ](../assets/images/appointment-manager-overview.png)
 ![ 约会管理器概述约会管理器](../assets/images/appointment-manager-2.png)

## <a name="ask-away"></a>询问离开

"离开时询问"是一个 [Microsoft Teams](../bots/what-are-bots.md) 自动程序，允许用户在 Teams 中&问答 (问答) 问答。 使用"&询问离开"自动程序，团队成员可以提交和投票支持同事共享的问题，从而允许问答主机轻松地在频道或聊天中收集首要问题。 机器人可用于在 Teams 会议&实时问答，并允许与会者通过聊天实时提交问题。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-askaway)

:::row:::
  :::column span="2":::
    ![用户对问题进行投票的排行榜弹出对话框视图](../assets/images/ask-away-app.png)  
:::column-end:::
:::row-end:::

## <a name="associate-insights"></a>员工见解

Associate Insights 是一个 [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) 模板，它使一线员工可以直接捕获和提交客户的意见、情绪和认知。 一线员工通常是第一个在一对一联系点与客户互动的公司代表。 业务团队可以共享和协同使用收集的数据，例如通过 Power BI Teams 选项卡，以改进产品并增强客户体验。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

:::row:::
  :::column span="2":::
    ![应用生成的见解的反馈视图](../assets/images/associate-insights-app.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![应用生成的见解的 Power BI 视图](../assets/images/associate-insights-app2.png)
:::column-end:::
:::row-end:::

## <a name="attendance"></a>考勤

"考勤"应用是可以在团队中固定的 ["Power Apps"](/powerapps/maker/canvas-apps/embed-teams-app) 选项卡。 它旨在记录状态，通常位于学习和培训环境等设置中。 用户可以标记或编辑过去最多 30 天的出席时间，并查看整个组或单个与会者的汇总出席报告。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-attendance)

![参加应用演示](../assets/images/attendance-app.png)

## <a name="book-a-room"></a>预订聊天室

会议室预订是一个 [Microsoft Teams](../bots/what-are-bots.md) 自动程序，它允许用户从当前时间开始快速查找会议室并保留 30 (默认) 、60 或 90 分钟的会议室。 Book-a-room bot 作用域为个人对话或 1：1 对话。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom)

![会议室预订演示](../assets/images/book-a-room.png)

## <a name="building-access"></a>Building Access

Building Access 是一款基于 Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)的应用，通过允许设施控制器管理、跟踪和报告员工现场状态，支持对建筑物阈值和社会性解除规范进行管理。 使用 Microsoft Power [Apps](/powerapps/powerapps-overview)和 [Power Automate](/power-automate/getting-started)构建的应用与 Microsoft Teams 深度集成，使组织可以确定构建就绪情况、建立现场访问的资格标准，并收集未来规划的见解。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess)

:::row:::
   :::column span="":::
     ![Building Access 预订卡](../assets/images/building-access-reservation.png)
   :::column-end:::
   :::column span="":::
      ![生成访问键视图](../assets/images/building-access-access-key.png)
   :::column-end:::
:::row-end:::

## <a name="celebrations"></a>Celebrations

庆祝是一款 Teams 应用，可帮助团队成员庆祝彼此的生日、周年纪念日和其他定期活动。 它记住所有团队成员的特殊场合，并发送在事件创建时选定的所有团队中的友好消息，使团队成员在一天中感觉特别。

该应用提供了一个简单的界面，供所有团队成员个人添加和查看其事件，还允许用户选择共享事件的团队。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="checklist"></a>清单

清单是一个自定义 Microsoft Teams [消息传递](../messaging-extensions/what-are-messaging-extensions.md) 扩展应用，使你能够在聊天或频道中通过创建共享清单与团队协作。 该应用在所有 Teams 平台客户端（桌面、浏览器、iOS 和 Android）中均受支持，并且已准备好部署为 Microsoft 365 订阅的一部分。  

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-checklist-app )

:::row:::
:::column span="2":::
    ![在 Teams 视图中创建清单](../assets/images/checklist-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="classroom-drop-in-9734"></a>课堂放置&#9734;

Classroom Drop-in 是一款基于 Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)的应用，系统领导可根据需要查找课堂团队 (虚拟教室) 并根据需要将自己或其他人员添加到这些课堂团队中。 使用 Microsoft [Power Apps](/powerapps/powerapps-overview) 和 [Power Automate](/power-automate/getting-started)构建的应用与 Microsoft Teams 深度集成，以确保教育机构可以针对每个业务要求向相关利益干系人提供访问权限，从而优化他们在混合学习环境中的操作。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-classroom-dropin)

![课堂下拉请求](../assets/images/classroom-drop-in-request.png)

## <a name="company-communicator"></a>Company Communicator

公司Communicator应用允许公司团队通过聊天创建和发送面向多个团队或大量员工的消息，从而允许组织在员工协作的地方与员工联系。 将此模板用于多种方案，例如新计划公告、员工入职培训、新式学习与开发或组织范围的广播。

该应用为指定用户提供了一个简单的界面，用于创建、预览、协作和发送邮件。

它为构建自定义目标通信功能（如有关确认或与邮件交互的用户数的自定义遥测）提供了基础。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![jCompany Communicator撰写框视图](../assets/images/CompanyCommunicatorCompose.png)

## <a name="contact-group-lookup"></a>联系人组查找

联系人组查找应用提供了一种方便且有用的方法，用于创建、访问和管理组织的联系人组 (以前称为通讯组列表或通讯组) 。 用户可以快速查看和与团队成员聊天、查看成员状态，以及创建与联系人组中选定成员的群聊，所有这些都在 Teams 环境中完成。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)

:::row:::
:::column span="2":::
    ![联系人组查找固定的收藏夹视图](../assets/images/contact-group-lookup-favorites.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![联系人组查找开始聊天演示](../assets/images/contact-group-lookup-chat.png)
:::column-end:::
:::row-end:::

## <a name="co-worker-appreciation-9734"></a>同事的"向内&#9734;

使用 Microsoft Teams 中的同事共同理解模板，用户可以在 Teams 上下文中识别其同事的成就。 当同事选择奖励同事时，将在频道对话中标记收件人和其他团队成员，并接收有关该频道的奖励详细信息的通知。 这些奖励记录在 Teams 应用中，安全、便携且易于共享。 这可视为基于 PowerApps 的开放锁屏提醒应用模板版本，具有排行榜。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-coworker-appreciation)

![总体](../assets/images/coworker-appreciation-1.png)

## <a name="crowdsourcer"></a>CrowdSourcer

众源是一个 [Microsoft Teams 机器人](../bots/what-are-bots.md) ，它向团队提供以协作方式从团队成员获取的查询信息。 这是一种很好的方法，可以回答常见问题，同时使参与者能够积极参与并参与一个有趣而有用的信息资源。

[在 Github 上获取](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![众包最终用户交互](../assets/images/crowdsourcer.png)

## <a name="custom-stickers"></a>自定义贴纸

自我表达是健康团队文化的核心。 此应用程序模板是 [一个消息扩展](~/messaging-extensions/what-are-messaging-extensions.md) ，使你的用户能够在 Microsoft Teams 内使用自定义贴纸和 GIF。 此模板提供基于 Web 的轻松配置体验，具有配置访问权限的任何人都可以上载他们希望最终用户拥有的 GIF/贴纸/图像，从而允许整个团队使用你选择的任何一组贴纸。

此应用程序还支持跨团队轻松共享图像/GIF/贴纸，而无需访问 SharePoint 网站或单个通道作为存储和共享机制。 例如，产品团队可以编程方式轻松地将产品图像和 GIF 共享到社交媒体、市场营销和销售团队。 还可以在提供新映像/GIF 时，通过向特定团队/个人触发通知流来扩展此应用。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![贴纸应用](../assets/images/stickers.png)

## <a name="employee-ideas"></a>员工想法

员工创意应用是基于 Azure 的"创意型创意"应用模板的 PowerApps 版本。 该应用使 Teams 用户能够设置和配置创意活动。 想法活动是围绕常见主题对想法进行分组的类别。

Teams 用户还可以执行以下活动：
* 配置员工需要为每个想法提交的标准提交表单。 
* 查看和管理活动的想法和列表。
* 修改和删除市场活动。
* 查看想法的排行榜。
* 投票支持并共享优先想法。
* 提交活动想法。
* 查看其他团队成员的想法。
* 对最喜欢的想法投票。
* 查看他们与市场活动中其他人相比想法的性能。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-employeeideas)

![管理市场活动视图](../assets/images/employee-ideas-manage-campaigns.png) 

## <a name="e-prescriptions"></a>E-Prescriptions 

E-Cares 是一款基于 [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)的应用，它通过自动执行向患者发布电子医疗方案的过程来增强远程医疗与虚拟医疗。 医疗专业人员可以直接在 Teams 平台中查看约会、生成电子医疗方案以及向患者发送电子邮件以及电子医疗附件。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-eprescription) 

:::row:::
:::column span="2":::
    ![E-Prescriptions 应用的屏幕截图。 显示医疗保健提供商如何选择一个生成按钮来为患者订购规定。](../assets/images/e-prescriptions-app-template.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![E-Prescriptions 应用的屏幕截图。 显示管理员如何管理使用该应用的医疗保健提供商。](../assets/images/e-prescriptions-app-template-admin.png)
:::column-end:::
:::row-end:::

## <a name="employee-training"></a>员工培训 

员工培训是一款 Microsoft Teams 应用，使组织者能够轻松发布、跟踪和提升组织的学习与培训活动。  借助该应用，事件规划人员可以向事件注册人发送提醒和通知，员工可以指示对即将发生事件的关注，及时了解当前事件，以及通过 Teams 消息传递扩展与同事共享事件详细信息。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-employeetraining)

:::row:::
:::column span="2":::
    **查看员工培训计划** ![员工培训选项卡图像](../assets/images/employee-training-discover-tab.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    **创建员工培训计划** ![员工培训创建事件表单](../assets/images/employee-training-create-event.jpg)
:::column-end:::
:::row-end:::

## <a name="expert-finder"></a>专家查找器

专家查找器是一种 [Microsoft Teams 自动](../bots/what-are-bots.md) 程序，可基于特定组织成员的技能、兴趣和教育属性识别这些成员。 成员在组织中查找与 Azure Active Directory 用户配置文件的关键字搜索匹配的专家。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![专家查找器搜索结果演示](../assets/images/expert-finder.png)

## <a name="faq-plus"></a>常见问题 +

对话&聊天机器人是为用户提供常见问题解答的一种简单方法。 但是，大多数机器人无法以有意义的方式与用户互动，因为当机器人失败时循环中没有任何人。 常见问题自动程序是一&的问答，当机器人无法提供帮助时，它会在循环中引入用户。 用户可以向机器人提问，如果问题包含在知识库中，机器人会以答案进行响应。 如果没有，机器人允许用户提交查询，该查询随后会发布给预配置的专家团队，这些专家通过处理来自团队本身的通知来帮助提供支持。

> [!NOTE]
> 最新版 **FAQ Plus** 支持改进&问答解决方案，使专家团队能够完成以下任务：
>
> &#x2714;使用消息&将新的问答直接添加到知识库。
>
> &#x2714;编辑和删除&自动程序添加的问答。
>
> &#x2714;跟踪问答的&历史记录。
>
> &#x2714;配置包含其他详细信息的答案，以显示为自适应 [卡片](../task-modules-and-cards/cards/cards-reference.md#adaptive-card)。
>
[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![FAQ Plus gif](../assets/images/FAQPlusEndUser.gif)

## <a name="get-support-app-9734"></a>获取支持应用&#9734;

使用 Microsoft Teams 的组织可以使用"获取支持"应用，以允许任何一组用户向监督员请求帮助。 此应用包括各种功能，例如：
-   从 Power App 请求不同类别的帮助
-   发送给请求者的通知，告知其已分配人员 
-   发送给指定监督员的通知，告知他们谁需要协助 
-   分析 SharePoint 和 PowerBI 中的升级和模式

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-app-get-support/)

![获取支持 Gif](../assets/images/get-support.gif)

## <a name="goal-tracker"></a>目标跟踪器

目标跟踪器应用是一个全面的解决方案，可支持在 Microsoft Teams 中建立目标、观察进度和确认成功。 该应用使用户能够在专业、个人和团队级别设置、跟踪和更新目标。 团队成员还收到及时的提醒和状态更新，保持专注并保持跟踪状态。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-app-goaltracker)

:::row:::
  :::column span="2":::
    ![设置目标](../assets/images/goal-tracker-set-goals-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![查看设置目标](../assets/images/goal-tracker-your-goals-view.png)
:::column-end:::
:::row-end:::

## <a name="great-ideas"></a>出色的创意

出色的创意应用支持并增强组织内部的创造力和创造力。 利用该应用，你的员工可以与同事和领导分享想法、发现新提交、聚焦贡献以用于对等考虑，并投票选择 Microsoft Teams 中的最佳建议。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-greatideas)

:::row:::
  :::column span="2":::
    ![查看提交的想法](../assets/images/great-ideas-all-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![查看想法](../assets/images/great-ideas-digest-view.png)
:::column-end:::
:::row-end:::

## <a name="group-activities"></a>组活动

组活动是一款 Microsoft Teams 应用，使团队所有者可以轻松在 Microsoft Teams 上下文中快速创建活动组和管理协作工作流。 活动作者可以创建活动、在组中随机分配团队成员，并可以选择让机器人发送提醒，直到活动完成。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities)

:::row:::
  :::column span="2":::
    ![Teams 中的组活动列表](../assets/images/group-activities-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![频道中的组活动通知消息](../assets/images/group-activities-2.png)
:::column-end:::
:::row-end:::

## <a name="grow-your-skills"></a>提高技能

"发展你的技能"应用通过允许员工在同时学习新技能的同时为组织提供补充项目，从而支持专业增长和开发。 员工可以使用该应用找到满足其兴趣的机会，与同行进行有意义的协作，并获得新级别的专业技能和功能，所有这些都在 Teams 环境中实现。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)

:::row:::
  :::column span="2":::
    ![可用项目视图](../assets/images/grow-your-skills-all-projects-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![查看者获取的技能视图](../assets/images/grow-your-skills-acquired-skills-view.png)
:::column-end:::
:::row-end:::

## <a name="hr-support"></a>HR 支持

HR 支持机器人是一个友好的&聊天机器人，当无法提供帮助时，它会在循环中提供来自 HR 团队的支持专业人员/专家。 用户可以向机器人提问，如果问题包含在知识库中，机器人会以答案进行响应。 如果没有，机器人允许用户提交查询，该查询随后将在预配置的专家团队中发布，这些专家通过处理来自团队本身的通知提供帮助。 此外，机器人通过搜索问题中的预配置标记，提供指向建议的 HR 策略/问题的链接建议。 这些磁贴还可以在关联的选项卡中作为快速参考找到。 HR 支持适用于轻型 QnA，并且适用于在组织中启动新项目/计划时提供快速支持。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![HR 支持](../assets/images/expert-user.png)

## <a name="icebreaker"></a>Icebreaker

Icebreaker 是 [一](../bots/what-are-bots.md) 个 Microsoft Teams 机器人，通过每周配对两个随机团队成员来开会，可帮助你的团队建立关系。 自动程序通过自动建议适用于这两个成员的空闲时间来轻松安排日程。 通过此应用加强个人连接并构建紧密社区。

除了鼓励整个团队中的个人连接之外，Icebreaker 应用还可以帮助促进组织中基于兴趣的社区。 例如，你可以将此应用用于 DevOps 兴趣组，以帮助在组织中自然地传播想法和最佳做法。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Icebreaker 应用](../assets/images/icebreaker.png)

## <a name="incentives"></a>奖励

奖励是 [一个 Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) 模板，可管理和跟踪已激活的员工参与指定活动，如培训和变更管理计划。 管理员使用该应用建立指定活动、分配完成分数，并指定奖励所需的资格点级别。 员工使用应用查看累积的积分，在达到资格后，请求和申请可兑换奖励。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-incentives)

![奖励应用演示](../assets/images/incentives-app.png)

## <a name="incident-reporter"></a>事件报告者

事件报告程序 [是一](../bots/what-are-bots.md)  个 Microsoft Teams 自动程序，可优化对组织中事件的管理。 自动程序可促进自动事件数据收集、自定义事件报告、相关利益干系人通知和端到端事件跟踪。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport)

:::row:::
  :::column span="2":::
    ![事件报告器组范围视图](../assets/images/incident-reporter-02.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![事件报告器个人范围视图](../assets/images/incident-reporter-01.jpg)
:::column-end:::
:::row-end:::

## <a name="inspection-9734"></a>检查&#9734;

 检查是一款 Microsoft Teams 应用，使第一线工作人员可以检查从位置到资产和设备之间的任何内容。 例如，零售商店、制造工厂或车辆和计算机。 此解决方案中具有两个应用，每个应用都适用于不同类型的用户。

该应用使第一线工作人员能够检查资产或区域，管理产品和服务的质量，或维护工作场所的安全性。 它便于工作组成员之间的通信，以解决在检查过程中发现的问题。 该应用为经理提供了简单的报告，以加快问题解决并突出显示趋势。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-inspection)

 ![检查概述](../assets/images/inspection-app.png)  


## <a name="issue-reporting"></a>问题报告

问题报告应用程序使员工和经理能够提出和管理问题。 它包含两个应用：用于报告问题的"问题报告"应用和用于管理问题的"管理问题"应用。

团队经理使用"管理问题"应用配置应用体验，包括应用创建 Microsoft Teams 消息和 Planner 任务的频道。 管理员还使用该应用创建模板表单，以在用户报告问题时收集详细信息。 例如，查看、编辑或删除问题模板表单。 该应用还可用于查看团队问题、报告问题历史记录并高效管理问题解决。

员工使用问题报告应用记录解决问题所需的问题和详细信息。 该应用还用于修改和解决现有问题，并获取个人或团队问题的高级别视图。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-issuereporting)

![问题报告团队视图](../assets/images/issue-reporting-team-view.png)  

## <a name="new-employee-onboarding"></a>新员工入职培训 

新员工入职培训是一个集成的 Microsoft Teams 和 [SharePoint](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) 新员工入职培训解决方案，使组织能够在新员工旅程中为员工提供一致、高质量的入职培训体验。 人力资源团队和招聘经理可以使用该应用在整个入职培训过程中和招聘过程中提供相关信息，由新员工用来共享反馈、提供简介和完成载入任务。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-newemployeeonboarding)

:::row:::
  :::column span="2":::
    **新员工欢迎卡片** ![新员工欢迎卡片的图像](../assets/images/new-employee-welcome-card.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    **新员工清单** ![新员工清单的图像](../assets/images/new-employee-checklist.png)  
:::column-end:::
:::row-end:::

## <a name="open-badges"></a>打开锁屏提醒

开放锁屏提醒是一款 Microsoft Teams 应用，使个人可以在 Teams 上下文中获取数字学习凭据锁屏提醒，并可在任何位置共享。 使用来自第三方数字锁屏提醒颁发机构 [Badgr](https://badgr.org/)的功能，已授予徽章记录在收件人的 Badgr 配置文件中，可用于生成和共享生命周期学习旅程的丰富图片。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-openbadges)

:::row:::
  :::column span="2":::
    ![可用锁屏提醒的图像](../assets/images/open-badges-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![奖励锁屏提醒视图](../assets/images/open-badges-2.png)
:::column-end:::
:::row-end:::

## <a name="poll"></a>投票 

投票是一个自定义 Microsoft Teams [消息传递](../messaging-extensions/what-are-messaging-extensions.md) 扩展应用，可用于在聊天或频道中快速创建和发送投票，以收集团队的意见和偏好。 该应用在所有 Teams 平台客户端（桌面、浏览器、iOS 和 Android）中均受支持，并且已准备好部署为 Microsoft 365 订阅的一部分。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-poll-app)

:::row:::
  :::column span="1":::
    ![在 Teams 视图中创建轮询](../assets/images/poll-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="quick-responses"></a>快速响应

快速响应是一款 Microsoft Teams 应用，可提供一个可靠的解决方案，有效回答用户对常见问题 (常见问题) 。 应用将构建响应库，以通过 Teams 消息扩展实现交互式用户体验，而不是手动回答每个查询并不断 [重复信息](../messaging-extensions/what-are-messaging-extensions.md)。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)

![响应示例视图](../assets/images/quick-responses.png)


## <a name="quiz--9734"></a>测验&#9734;

测验是一个 [自定义 Teams 消息传递](../messaging-extensions/what-are-messaging-extensions.md) 扩展应用，可让你在聊天或频道内创建测验，用于进行知识检查和即时结果。 可以使用测验、课堂和离线考试、团队内的知识检查，以及团队中的有趣测验。 测验应用支持跨多个平台，例如 Teams 桌面、浏览器、iOS 和 Android 客户端。 此应用已准备好作为现有 Microsoft 365 订阅的一部分进行部署。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-quiz)

:::row:::
  :::column span="1":::
    ![在 Teams 视图中创建测验](../assets/images/quiz-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="rapid-assist"></a>快速协助

快速协助是一款基于 Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) 的应用，面向客户的关联人员可以快速与专家联系，以快速获得答案、搜索信息、跟进打开的请求，并允许专家接收通知以快速接听电话以帮助回答问题。 使用 Microsoft [Power Apps](/powerapps/powerapps-overview) 和 [Power Automate](/power-automate/getting-started)构建的应用与 Microsoft Teams 深度集成，使组织能够轻松地将一线员工与公司代表联系，从而解决客户查询并提供出色的客户体验。 

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-rapid-assist)

:::row:::
   :::column span="":::
     ![最终用户请求界面](../assets/images/EndUserHome.png)
   :::column-end:::
   :::column span="":::
      ![专家请求视图](../assets/images/ExpertViewRequests.png)
   :::column-end:::
:::row-end:::

## <a name="reflect"></a>反射 

"反映"是一个自定义 Microsoft [Teams](../messaging-extensions/what-are-messaging-extensions.md) 消息传递扩展应用，可为团队成员提供安全且包含的资源，以直接与 Teams 中的同事和/或组领导分享其情绪状态。 该应用在频道、组、会议以及一对一聊天中可用，并且签入响应可以设置为公共、私人到发件人或完全匿名。

[在 GitHub 上获取](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect)

:::row:::
    :::column:::
    **健康投票**
    
    ![反映应用用户轮询](../assets/images/reflect-app-user-poll.png)
    :::column-end:::
:::row-end:::

## <a name="remote-support"></a>远程支持

远程支持是 [Microsoft Teams 自动](../bots/what-are-bots.md) 程序，在整个组织的支持请求者和内部支持团队之间提供一个集中的界面。  最终用户可以提交、编辑或撤消支持请求，支持团队可以在 Teams 平台内响应、管理和更新所有请求。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport)

:::row:::
  :::column span="2":::
    ![请求支持表单](../assets/images/remote-support-request-form.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![请求支持详细信息](../assets/images/remote-support-request-details.jpg)
:::column-end:::
:::row-end:::

## <a name="request-a-team"></a>请求团队

请求团队是一款 Microsoft Teams 应用，可优化企业组织的新团队创建。 应用通过集成向导引导的请求表单、嵌入式审批流程、请求状态仪表板和自动化团队生成来创建新团队实例时，支持标准化和最佳做法。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-requestateam)

:::row:::
  :::column span="2":::
    ![请求团队起始页视图](../assets/images/request-a-team-two.jpg)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![请求团队向导页面视图](../assets/images/request-a-team-three.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-channels"></a>适用于频道的 Scrums

适用于频道的 Scrums 是一款 scrum 助手应用，使用户能够在 Microsoft Teams 内的频道中安排和运行 scrum。 该应用非常适用于由来自不同地理位置和时区的成员组成的远程团队和团队，以共享每日更新并确保参与大量独立会议。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels)

> [!NOTE]
> 若要在群聊中召开 scrum 会议，请参阅我们的 [Scrums for Group Chat 应用](#scrums-for-group-chat) 模板。

:::row:::
  :::column span="2":::
    ![通道设置视图的 Scrum](../assets/images/scrum-for-channels-settings.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![频道团队成员状态视图的 Scrums](../assets/images/scrum-for-channels-status.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-group-chat"></a>用于群聊的 Scrums

> [!NOTE]
> Scrums 状态应用模板已更新，现在是用于群聊的 Scrums。

适用于群聊的 Scrums 是一种支持性的 scrum 助手，允许群聊成员运行异步独立会议并轻松共享其每日更新。 它允许群聊的所有成员参与 scrum，并查看运行中的 scrum 中其他人的更新。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat)

![用于群聊演示的 Scrums](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="share-now"></a>现在共享 

"现在共享"应用使用户可以轻松地在 Teams 环境中共享内容，从而促进同事之间的积极信息交换。 用户通过应用与团队成员共享感兴趣的项目、发现新的共享内容、设置首选项和书签收藏夹以便稍后阅读。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)

![选择内容视图](../assets/images/share-now-suggested-content.png)

## <a name="sharepoint-list-search"></a>SharePoint 列表搜索

Microsoft Teams 中的协作通常引用 SharePoint 列表中的项中包含的信息。 只需将链接粘贴到相关项目，将强制每个人从对话切换上下文，查找所需信息，然后返回到 Teams 以继续对话。 随着对话的继续，通常用户必须多次切换回引用项目，以验证新注释并刷新其对项目中包含的信息的刷新。 此上下文切换为顺利协作创建了障碍，也是解决失败问题的方式。

为了帮助缓解这种负担，我们乐意为你带来"列表搜索"应用模板。 数百万用户使用 SharePoint 为组织中某些核心工作流提供支持。 但是，围绕列表进行协作可能非常繁琐。 通过使用 Microsoft Teams 中的"列表搜索"应用模板，用户可以直接在聊天对话中插入 SharePoint 列表项的信息，以缓解仅将链接插入聊天时导致的上下文切换。 信息作为易于阅读的自动格式化卡片插入，帮助用户继续参与对话。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![列出搜索应用程序](../assets/images/list-search-template.png)

## <a name="staff-check-ins"></a>员工签入

员工签入是基于 [Power Apps](/powerapps/powerapps-overview)的应用，支持你的业务和现场人员之间的监督通信。 员工可以直接从 Teams 中按计划或临时提供时间关键信息和状态更新。 该应用支持实时位置、照片和笔记以及提醒通知和自动工作流。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)

![创建签入视图](../assets/images/staff-check-ins-create.png)

## <a name="survey"></a>调查

调查是一个自定义 Microsoft Teams [消息传递](../messaging-extensions/what-are-messaging-extensions.md) 扩展应用，它使您能够在聊天或频道中创建调查，以收集数据并获取可操作见解。  该应用在所有 Teams 平台客户端（桌面、浏览器、iOS 和 Android）中均受支持，并且已准备好部署为 Microsoft 365 订阅的一部分。  

[在 GitHub 上获取](https://github.com/OfficeDev/Microsoft-Teams-Survey-app)

:::row:::
  :::column span="2":::
    ![在 Teams 视图中创建调查](../assets/images/survey-app-template-compose-view.gif)
:::column-end:::
:::row-end:::

## <a name="time-tally-9734"></a>时间数据&#9734;

一个项目可以包含多个任务，并且可以将各种项目分配给员工。 经理必须了解在员工执行这些任务所花的时间内的项目进度。 这会是一项很麻烦的活动，因为员工需要填写时间表。 利用时间表应用程序，员工能够使用移动设备快速填写其时间表，经理也不需要跟进员工的时间表条目。 经理可以基于资源查看项目利用率，并可以批准或拒绝这些条目。 发送提醒通知以确保时间表合规性。 此外，历史数据和使用情况可用于分析。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-timetally)

![Time Tally](../assets/images/11zon_gif.gif)


## <a name="training--9734"></a>培训&#9734;

培训是一个自定义 [Teams 消息传递](../messaging-extensions/what-are-messaging-extensions.md) 扩展应用，允许用户在聊天或频道中发布培训，以便进行脱机知识共享和学习。 该应用在多个 Teams 平台客户端（如桌面、浏览器、iOS 和 Android）中受支持。 此应用已准备好部署为 Microsoft 365 订阅的一部分。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-training)

:::row:::
  :::column span="1":::
    ![在 Teams 视图中创建培训](../assets/images/training-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="virtual-rounding"></a>虚拟舍入

医院和紧急会议室提供商每天进行数十次， **通常数百** 次。 这些患者快速签入旨在提供对患者情况的状态检查，并确保解决患者的问题。 尽管舍入是确保患者受到多种提供商监控的基本做法，但是它们表示 PPE 会消耗大量资源，因为每次访问时，每个提供商都必须使用一个新掩码和一组新的面罩。 使用此应用模板，医疗工作者可以通过提供商和患者之间的 Microsoft Teams 会议轻松地进行虚拟轮次。

Microsoft Health and Life Sciences 博客文章 也引用了虚拟舍入 [解决方案](https://aka.ms/teamsvirtualrounding)。

[在 GitHub 上获取](https://github.com/SmartterHealth/Virtual-Rounding)

![虚拟舍入](../assets/images/virtual-rounding-overview.png)

## <a name="visitor-management"></a>访问者管理

利用访问者管理应用，组织和员工可以直接从 Microsoft Teams 轻松高效地管理现场访问者流程。 利用该应用，员工可以创建访问者请求、通过访问者仪表板集中跟踪请求状态，以及当访问者到达时接收实时通知。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement)

:::row:::
  :::column span="2":::
    ![创建请求视图](../assets/images/visitor-management-create-request.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![访问者到达通知](../assets/images/visitor-management-notify-host.png)
:::column-end:::
:::row-end:::

## <a name="workplace-awards"></a>Workplace Awards

Workplace Workplace Workplace 是一个 Teams 应用模板，提供一个积极框架，以培养现代工作场所中员工的认知和鼓励员工文化。 通过该应用，你可以设置和管理员工奖励和识别 (R&R) 计划，员工可以在该计划中轻松指定和认可同事，R&R 领导者可以查看提交的候选人、授予奖励和通知收件人。

[在 GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards)

:::row:::
  :::column span="2":::
    ![工作区候选人卡 ](../assets/images/workplace-awards-nominate.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![工作区奖励列表选项卡](../assets/images/workplace-awards-champion-tab.png)
:::column-end:::
:::row-end:::

对要查看的应用模板有一个想法吗？ [请告诉我们](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u)。
