---
title: Microsoft Teams应用模板
description: 了解如何将应用模板用于Microsoft Teams平台，并提供有关部署和安装应用的详细说明。
ms.topic: reference
keywords: Microsoft Teams模板示例演示
ms.localizationpriority: medium
ms.author: lajanuar
author: surbhigupta
ms.openlocfilehash: 1e43410f81f87b35f6cedee6c2dfa87ee3d40099
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073734"
---
# <a name="app-templates-for-microsoft-teams"></a>Microsoft Teams 的应用模板

应用模板是Microsoft Teams的完整应用示例，这些应用是开源的，可在GitHub上使用。 每个应用模板都包含有关为组织部署和安装该应用的详细说明。 它还提供了一个示例应用，你可以立即安装并开始使用。 此外，还提供了完整的源代码，这使你可以详细浏览它或为代码创建分叉，并根据特定要求对其进行更改。
所有应用模板都根据 [MIT 许可](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE) 条款提供。

> [!NOTE]
> 必须为用户和组织许可和支持从应用模板创建的应用。

使用应用模板的主要优点是：

* **直接部署到云：** 所有应用模板都包含部署脚本，可用于托管Microsoft Azure或 Power Platform 中所需的所有服务。
* **建议的示例代码：** 应用模板符合有关安全和基础结构的建议最佳做法。 对所有社区提交的应用模板更改进行评审，以确保符合性。
* **可自定义和可扩展：** 虽然所有应用模板都以最少的配置进行部署，但会提供整个代码库和部署脚本，以便你可以轻松自定义或扩展这些模板以满足你的独特需求。
* **详细文档：** 所有应用模板都附有有关解决方案体系结构、部署和配置步骤的端到端文档。  

## <a name="adoption-tool--champion-management-platform"></a>采用工具 - 冠军管理平台

冠军管理平台 (CMP) 应用模板可帮助你管理、缩放和激励团队合作冠军实现更多目标。 此应用模板基于SharePoint 框架构建，并加载到团队中的选项卡中。 组可以利用此工具来帮助管理程序成员身份、为日志记录提供排行榜和事件类型，以及将数字徽章覆盖到程序参与者的工具。

[在GitHub上获取它](https://github.com/OfficeDev/microsoft-teams-apps-champion-management)

## <a name="adoption-tool--microsoft-365-learning-pathways-get-started"></a>采用工具- Microsoft 365 Learning路径 (入门) 

使用入门应用模板可以将Microsoft 365学习路径的功能引入Microsoft Teams。 使用此应用模板，可以轻松地访问特定训练页或其他 Intranet 资产，并直接在Teams中加载内容。 还可以更改应用名称或徽标以匹配公司品牌。

[在GitHub上获取它](https://github.com/msft-teams/tools/tree/master/M365%20Learning%20Pathways)

## <a name="company-communicator"></a>Company Communicator

公司Communicator应用使公司团队能够通过聊天创建和发送面向多个团队或大量员工的消息，使组织能够在员工协作的地方与员工联系。 将此模板用于多种方案，例如新计划公告、员工加入、新式学习、开发或组织范围广播。

该应用为指定用户提供了一个易于创建、预览、协作和发送消息的界面。

它提供了一个基础，用于生成自定义目标通信功能，例如，自定义遥测数据，了解有多少用户已确认或与消息交互。

[在GitHub上获取它](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![jCompany Communicator撰写框视图](../assets/images/CompanyCommunicatorCompose.png)

## <a name="co-worker-appreciation"></a>同事欣赏

使用Microsoft Teams中的同事欣赏模板，用户可以在Teams上下文中识别其同事的成就。 当同事选择奖励同事时，收件人和其他团队成员会在频道对话中标记，并且他们收到有关频道的奖励详细信息的通知。 奖项记录在Teams应用中，该应用安全、可移植且易于共享。 这被视为具有排行榜的基于 PowerApps 的 Open Badges 应用模板版本。

[在GitHub上获取它](https://github.com/OfficeDev/microsoft-teams-apps-coworker-appreciation)

![整体](../assets/images/coworker-appreciation-1.png)

## <a name="faq-plus"></a>常见问题 +

对话式 Q&机器人是一种简单的方法，可为用户常见问题提供解答。 但是，大多数机器人无法以有意义的方式与用户互动，因为当机器人失败时，循环中没有人。 常见问题解答机器人是一个友好的 Q&机器人，当用户无法提供帮助时，它会将用户引入循环中。 可以向机器人提出问题，如果机器人包含在知识库中，则机器人会回答该问题。 如果没有，机器人允许用户提交查询，然后将其发布到预配置的专家团队，这些专家团队通过处理来自团队内部的通知提供支持。

> [!NOTE]
> 最新发布的 **常见问题解答加支持** 改进的 Q&A 解决方案，使专家团队能够完成以下操作：
>
> &#x2714;使用消息扩展直接向知识库添加新的 Q&。
>
> &#x2714;编辑和删除机器人添加的 Q&A 对。
>
> &#x2714;跟踪 Q&As 的修订历史记录。
>
> &#x2714;使用要显示为 [自适应卡](../task-modules-and-cards/cards/cards-reference.md#adaptive-card)片的其他详细信息配置答案。
>
[在GitHub上获取它](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![常见问题解答加 gif](../assets/images/FAQPlusEndUser.gif)

## <a name="icebreaker"></a>Icebreaker

Icebreaker是一个[Microsoft Teams机器人](../bots/what-are-bots.md)，通过每周配对两个随机团队成员来帮助团队更紧密地联系。 机器人通过自动建议适用于两个成员的免费时间来简化日程安排。 通过此应用加强个人联系并构建紧密联系的社区。

除了鼓励整个团队之间的个人联系外，Icebreaker应用还可以帮助在组织中培养基于兴趣的社区。 例如，可以将此应用用于DevOps兴趣组，以帮助创意和最佳做法在组织中有机地传播。

[在GitHub上获取它](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Icebreaker应用](../assets/images/icebreaker.png)

## <a name="new-employee-onboarding"></a>新员工加入

新员工加入是一种集成的Microsoft Teams[和SharePoint新员工加入解决方案](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19)，使你的组织能够在其新员工旅程中为员工提供一致、高质量的载入体验。 人力资源团队和招聘经理使用该应用在整个定向和上岗过程中提供相关信息，新员工可以共享反馈、提供简介和完成载入任务。

[在GitHub上获取它](https://github.com/OfficeDev/microsoft-teams-apps-newemployeeonboarding)

:::row:::
  :::column span="2":::
    **新员工欢迎卡** ![新员工欢迎卡的图像](../assets/images/new-employee-welcome-card.png)
:::column-end:::
:::row-end:::
:::row:::
  :::column span="2":::
    **新员工清单** ![新员工清单的图像](../assets/images/new-employee-checklist.png)  
:::column-end:::
:::row-end:::

## <a name="app-template-code-samples"></a>应用模板代码示例

应用模板代码示例是用于Microsoft Teams平台功能的示例应用的集合。

> [!NOTE]
> * Microsoft 未主动管理源代码。 完整的源代码开放源代码，你可以浏览、分叉和修改源代码以满足特定要求。
> * 不得使用 Microsoft Power Platform 创建要发布到Teams应用商店的应用。 Microsoft Power Platform 应用只能发布到组织的应用商店。

下表描述了应用模板代码示例：  

|名称|方案|GitHub链接| |---------|---------||-------| |采用机器人|采用机器人是使用 Power Virtual Agent 为 Teams PVA 构建的用户关心聊天机器人。 它被视为常见问题解答加号的 PVA 版本。 采用机器人解答有关Microsoft 365和Teams的 100 多个常见问题。 可以编辑现有主题、添加自己的主题以及引入现有常见问题解答。 如果用户需要其他帮助，采用机器人可以将其连接到专家，甚至可以扩展为使用高级流连接器打开服务票证。 此机器人自安装或内置于自定义应用（如 [采用中心）中](https://github.com/akporzondek/adoption_hub)。 | [采用机器人](https://github.com/OfficeDev/microsoft-teams-apps-adopt-bot)| |约会管理器|约会管理器是一个Teams应用模板，可帮助企业通过Teams创建、管理和与使用者进行虚拟约会。 来自使用者的新约会请求在Teams频道中可见，这些请求会在其中快速分配并重新分配给团队中的员工。 通过自定义选项卡在团队或个人级别查看约会请求。 每个约会都与Teams联机会议相关联，因此工作人员和使用者可以在计划的时间轻松加入会议。 应用模板与Microsoft Bookings集成，以便轻松进行约会管理。 计划的约会会自动出现在分配的工作人员的日历上，使用者会收到可自定义的电子邮件通知和提醒，其中包含嵌入式会议链接。|[约会管理](https://github.com/OfficeDev/microsoft-teams-apps-appointment-manager)器| |询问离开|Ask Away 是一个[Microsoft Teams机器人](../bots/what-are-bots.md)，使用户能够在Teams中执行名为 Q&A 会话的问答。 使用“询问离开”机器人，团队成员可以提交同事共享的和向上投票的问题，使 Q&A 主机能够轻松地在频道或聊天中收集头脑清醒的问题。 机器人用于在Teams会议中进行实时 Q&A 会话，并允许与会者通过聊天实时提交问题。 | [询问离开](https://github.com/OfficeDev/microsoft-teams-apps-askaway)| |关联Insights |关联Insights是一个[Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)模板，使一线员工能够直接捕获和提交客户意见、情绪和感知。 第一线员工通常是第一位与客户进行一对一接触的公司代表。 收集的数据由业务团队（例如通过Power BI Teams选项卡）共享和协作使用，以改进产品并增强客户体验。 | [关联Insights](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)| |出席人数|Attendance 应用是固定在团队中的[Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)选项卡。 它旨在记录在学习和训练环境中的状态。 用户可以标记或编辑过去最多 30 天的出勤情况，并查看整个组或单个与会者的汇总出席情况报告。   | [出席人数](https://github.com/OfficeDev/microsoft-teams-apps-attendance)| |预订会议室|书房是一个[Microsoft Teams机器人](../bots/what-are-bots.md)，用户可以从当前时间开始快速查找和预留会议室 30、60 或 90 分钟。 默认时间为 30 分钟。 Book-a-room 机器人的作用域为个人对话或 1：1 对话。| [预订会议室](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom) | |生成访问|生成 Access 是基于 Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) 的应用，支持通过使设施主管能够管理、跟踪和报告员工的现场状态来管理构建占用阈值和社会疏远规范。 该应用使用 Microsoft [Power Apps](/powerapps/powerapps-overview) 和 [Power Automate](/power-automate/getting-started) 构建，与Microsoft Teams深度集成，使组织能够确定生成就绪性、建立现场访问的资格标准，并收集未来规划的见解。 | [生成访问](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess)| |庆祝活动|庆祝活动是一个Teams应用，可帮助团队成员庆祝彼此的生日、纪念日和其他定期活动。 它记得所有团队成员的特殊场合，并在创建活动时选择的所有团队中发送友好信息，使团队成员在当天感到特别。 该应用为所有团队成员提供了一个轻松的界面来亲自添加和查看其事件，还允许用户选择共享事件的团队。 | [庆祝活动](https://github.com/OfficeDev/microsoft-teams-celebrations-app)| |清单|清单是自定义Microsoft Teams[消息传递扩展](../messaging-extensions/what-are-messaging-extensions.md)应用，通过在聊天或频道中创建共享清单，可以与团队协作。 所有Teams平台客户端（如桌面浏览器、iOS 和 Android）都支持该应用。 应用已准备好部署为Microsoft 365订阅的一部分。  | [清单](https://github.com/OfficeDev/microsoft-teams-checklist-app)| |课堂下拉列表|Classroom Drop-in 是一种基于 Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) 的应用，使系统领导能够查找课堂团队，意味着虚拟教室，并根据需要将自己或其他人添加到这些课堂团队的指定下拉时间段。 使用 Microsoft [Power Apps](/powerapps/powerapps-overview)和[Power Automate](/power-automate/getting-started)构建的应用与Microsoft Teams深度集成，以确保教育机构能够通过根据业务要求为班级团队提供相关利益干系人的访问权限来优化其在混合学习环境中的运营。|[课堂下拉](https://github.com/OfficeDev/microsoft-teams-apps-classroom-dropin)| |联系人组查找|联系人组查找应用提供了一种方便且有用的方法来创建、访问和管理组织的联系人组（以前称为通讯组列表或通信组）。 用户可以快速查看和与组成员聊天，查看成员状态，并创建与联系人组中所选成员的群组聊天，所有成员都在Teams环境中。|[联系人组查找](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)| |CrowdSourcer |CrowdSourcer 是一个[Microsoft Teams机器人](../bots/what-are-bots.md)，它为团队提供从组成员协作来源的查询信息。 它有助于回答常见问题，同时使参与者能够积极参与并贡献一个有趣且有用的信息资源。| [CrowdSourcer](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)| |自定义贴纸|自我表达是健康团队文化的核心。 此应用模板是一种[消息传递扩展](~/messaging-extensions/what-are-messaging-extensions.md)，使用户能够在Microsoft Teams中使用自定义贴纸和 GIF。 此模板提供简单的基于 Web 的配置体验，任何具有配置访问权限的人都可上传他们希望其用户拥有的 GIF、贴纸和图像，使整个团队能够使用你选择的任何贴纸集。 此应用还允许跨团队轻松共享图像、GIF、贴纸，而无需访问SharePoint网站或单个频道作为存储和共享机制。 例如，产品团队可以轻松地以编程方式将产品映像和 GIF 共享到社交媒体、市场营销和销售团队。 此外，当提供新映像和 GIF 时，还可以通过向特定团队或个人触发通知流来扩展此应用。| [自定义贴纸](https://github.com/OfficeDev/microsoft-teams-stickers-app) | |员工想法|员工创意应用是基于 Azure 的 Great Ideas 应用模板的 PowerApps 版本。 该应用使Teams用户能够设置和配置创意活动。 创意活动是一个类别，用于围绕常见主题对想法进行分组。 Teams用户还可以执行以下活动：<br/> 配置员工必须针对每个想法提交的标准提交表单。<br/>查看和管理活动的想法和列表。 <br/>修改和删除市场活动。 <br/> 评审领导委员会的想法。 <br/> 投票赞成并分享优先级的想法。 <br/> 提交活动的想法。 <br/> 查看其他团队成员的想法。 <br/>对最喜欢的想法进行投票。 <br/> 回顾他们的想法与活动中其他人相比的表现。|[员工想法](https://github.com/OfficeDev/microsoft-teams-apps-employeeideas)| |E-Prescriptions|E-Prescriptions 是基于[Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)的应用，它通过自动向患者颁发电子处方的过程来增强远程医疗和虚拟护理。 医疗专业人员可以快速查看预约、生成电子处方，以及直接在Teams平台内向患者发送带有电子处方附件的电子邮件。|[E-Prescriptions](https://github.com/OfficeDev/microsoft-teams-apps-eprescription)| |员工培训|员工培训是一种Microsoft Teams应用，使组织者能够轻松地发布、跟踪和推广组织的学习和培训活动。  借助该应用，事件规划器可以向事件注册人发送提醒和通知，员工可以指示对即将发生的事件的兴趣，随时更新当前事件，并通过Teams消息传递扩展与同事共享事件详细信息。|[员工培训](https://github.com/OfficeDev/microsoft-teams-apps-employeetraining)| |专家查找器|专家查找器是一个[Microsoft Teams机器人](../bots/what-are-bots.md)，它根据特定组织成员的技能、兴趣和教育属性来标识他们。 成员在组织中查找与Microsoft Azure Active Directory (Azure AD) 用户配置文件的关键字搜索匹配的专家。|[专家查找器](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)| |获取支持应用|使用Microsoft Teams的组织使用 Get Support 应用，使任何一组用户都能够向主管请求帮助。 此应用包括以下功能： <br/>从 Power App 请求不同类别的帮助。<br/>发送给请求者的通知，通知他们分配了谁。<br/> 发送给分配的主管的通知，告知他们谁需要帮助。 <br/>分析SharePoint和Power BI.|中的升级和模式[获取支持应用](https://github.com/OfficeDev/microsoft-teams-app-get-support/)| |目标跟踪器|目标跟踪器应用是组织支持建立目标、观察进度和确认Microsoft Teams中的成功的综合解决方案。 该应用使用户能够在专业、个人和团队级别上设置、跟踪和更新目标。 团队成员还会及时收到提醒和状态更新，以保持专注并保持正轨。|[目标跟踪器](https://github.com/OfficeDev/microsoft-teams-app-goaltracker) | |伟大的想法|Great Ideas 应用支持并增强组织中的创新和创造力。 该应用使你的员工能够与同事和领导分享想法，发现新的提交，为对等考虑提供聚焦贡献，并为Microsoft Teams中的最佳建议投票。 |[伟大的想法](https://github.com/OfficeDev/microsoft-teams-apps-greatideas)| |组活动|组活动是一个Microsoft Teams应用，使团队所有者能够轻松地在Microsoft Teams上下文中快速创建活动组和管理协作工作流。 活动作者可以创建活动、在组中随机分配团队成员，并且可以选择让机器人发送提醒，直到活动完成。|[组活动](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities)| |组连接 |组连接是一种Microsoft Teams应用，可帮助组织成员发现员工组并查找与员工组相关的信息。 该应用内置了丰富的功能，组织领导可以与其员工就组、事件和资源进行通信。 Group 连接 应用还以所需的频率将组成员相互匹配，以鼓励组内的网络和凝聚力。 有关如何利用 Group 连接 应用帮助员工组在组织内培养的详细信息，请参阅GitHub上的应用。 |[组连接](https://github.com/OfficeDev/microsoft-teams-apps-groupconnect)| |提高技能|“成长技能”应用支持专业成长和发展，使员工能够为组织的补充项目做出贡献，同时学习新技能。 员工可以使用该应用查找满足他们兴趣的机会，与同行进行有意义的协作，并获得新的专业知识和功能，所有这些都位于Teams环境中。|[提高技能](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)| |HR Support|HR 支持机器人是一个友好的 Q&A 机器人，当 HR 团队无法提供帮助时，它会在循环中引入支持专业人员或专家。 可以向机器人提出问题，如果机器人包含在知识库中，则机器人会回答该问题。 如果没有，机器人允许用户提交查询，然后将其发布到预配置的专家团队中，这些专家团队会根据团队内部的通知采取行动来提供支持。 此外，机器人还通过搜索问题中的预配置标记来建议指向建议的 HR 策略或问题的链接。 这些磁贴作为快速参考在关联的选项卡中找到。 人力资源支持适用于轻型 Q&A，并在组织中启动新项目或计划时提供快速支持。 |[人力资源支持](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)| |奖励|奖励是一个[Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)模板，用于管理和跟踪激励员工参与指定活动（如培训和更改管理计划）。 管理员使用该应用建立指定的活动，分配完成点，并指定奖励所需的资格点级别。 员工使用该应用查看其累积积分，并在获得资格后请求并申请可兑换奖励。|[奖励](https://github.com/OfficeDev/microsoft-teams-apps-incentives)| |事件记者|事件记者是一[个Microsoft Teams机器人](../bots/what-are-bots.md)，可优化组织中事件的管理。 机器人有助于自动收集事件数据、自定义事件报告、相关利益干系人通知和端到端事件跟踪。|[事件记者](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport)| |检查|检查是一种Microsoft Teams应用，使一线工作人员能够检查从位置到资产和设备的任何内容。 例如，零售商店、制造工厂或车辆和计算机。 此解决方案中有两个应用，每个应用面向不同类型的用户。 该应用使一线工作人员能够检查资产或区域、管理产品和服务的质量，或维护工作场所的安全。 它有助于团队成员之间的沟通，以解决在检查期间发现的问题。 该应用为管理者提供简单的报告，以加快问题解决并突出显示趋势。 |[检查](https://github.com/OfficeDev/microsoft-teams-apps-inspection) | |问题报告|问题报告应用使员工和经理能够提出和管理问题。 它由两个应用组成：用于报告问题的问题报告应用和用于管理问题的管理问题应用。 团队经理使用“管理问题”应用来配置应用体验，包括应用在其中创建Microsoft Teams消息和 Planner 任务的通道。 管理器还使用应用创建模板表单，以便在用户报告问题时收集详细信息。 例如，查看、编辑或删除问题模板表单。 该应用还用于查看团队问题、报告问题历史记录以及高效管理问题解决。 员工使用问题报告应用记录解决问题所需的问题和详细信息。 该应用还用于修改和解决现有问题，并获取个人或团队问题的高级别视图。 |[问题报告](https://github.com/OfficeDev/microsoft-teams-apps-issuereporting)| |打开徽章|开放徽章是一个Microsoft Teams应用，使个人能够在Teams上下文中获得数字学习凭据徽章，并在任何地方共享它们。 使用来自第三方数字徽章颁发机构 [Badgr](https://badgr.org/) 的功能，授予的徽章记录在收件人的 Badgr 配置文件中，并可用于构建和共享终身学习旅程的丰富图片。|[打开锁屏提醒](https://github.com/OfficeDev/microsoft-teams-apps-openbadges)| |轮询|轮询是一个自定义Microsoft Teams[消息传递扩展](../messaging-extensions/what-are-messaging-extensions.md)应用，可用于快速在聊天或频道中创建和发送投票，以收集团队意见和偏好。 该应用在所有Teams平台客户端（如桌面、浏览器、iOS 和 Android）中受支持，并且已准备好部署为Microsoft 365订阅的一部分。|[轮询](https://github.com/OfficeDev/microsoft-teams-poll-app)| |快速响应|快速响应是一种Microsoft Teams应用，可提供可靠的解决方案来有效回答用户常见问题解答。 应用不是手动回答每个查询，而是持续重复信息，而是通过Teams[消息传递扩展](../messaging-extensions/what-are-messaging-extensions.md)生成交互式用户体验的响应库。|[快速响应](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)| |测验|测验是一个自定义[Teams消息传递扩展](../messaging-extensions/what-are-messaging-extensions.md)应用，可用于在聊天或频道中创建测验以进行知识检查和即时结果。 你可以在团队中使用测验、课堂内和脱机考试、知识检查以及团队中的趣味测验。 测验应用支持跨多个平台，例如Teams桌面、浏览器、iOS 和 Android 客户端。 此应用已准备好部署为现有Microsoft 365订阅的一部分。|[测验](https://github.com/OfficeDev/microsoft-teams-apps-quiz)| |快速协助|Quick Assist 是基于 Microsoft [Power Platform](https://powerapps.microsoft.com/blog/) 的应用，允许面向客户的关联人员快速与专家联系，以获取快速答案、搜索信息、跟进打开的请求，并允许专家接收通知以快速接听电话以帮助回答问题。 使用 Microsoft [Power Apps](/powerapps/powerapps-overview)和[Power Automate](/power-automate/getting-started)构建的应用与Microsoft Teams深度集成，使组织能够轻松地将一线员工与公司联络人员连接，以解决客户查询并提供出色的客户体验。 |[快速协助](https://github.com/OfficeDev/microsoft-teams-apps-rapid-assist)| |反应|反应是一个自定义Microsoft Teams[消息传递扩展](../messaging-extensions/what-are-messaging-extensions.md)应用，可为团队成员提供安全且包容的资源，以直接在Teams中与同事或组领导分享他们的情感福祉状态。 该应用在频道、组、会议和 1：1 聊天中可用，签入响应设置为公共、专用到发件人或完全匿名。 |[反应](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect)| |远程支持|远程支持是一个[Microsoft Teams机器人](../bots/what-are-bots.md)，在整个组织的支持请求者与内部支持团队之间提供重点接口。  最终用户可以提交、编辑或撤回支持请求，支持团队可以响应、管理和更新Teams平台内的所有请求。|[远程支持](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport)| |Request-a-team|请求团队是一个Microsoft Teams应用，可优化企业组织的新团队创建。 应用支持通过向导引导式请求表单、嵌入式审批过程、请求状态仪表板和自动化团队生成集成创建新的团队实例时的标准化和最佳做法。|[请求团队](https://github.com/OfficeDev/microsoft-teams-apps-requestateam)| |通道|的 ScrumScrums for Channels 是一个 Scrum 助手应用，使用户能够在Microsoft Teams内的通道中计划和运行 Scrum。 该应用非常适合远程团队和团队，这些团队由来自不同地理位置和时区的成员组成，可共享每日更新并确保参与 Scrum 站立会议。|[通道| |的 Scrum](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels) 群聊的 Scrum|会更新 Scrums 状态应用模板，并将其调用为群聊的 Scrum。 用于群聊的 Scrum 是一种支持性 Scrum 助手，使群聊成员能够运行异步站立会议并轻松共享其每日更新。 它允许群聊的所有成员参与 Scrum，并查看正在运行的 Scrum 中其他人所做的更新。 |[群聊的 Scrum](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat) | |立即共享|Share Now 应用通过使用户能够轻松地在Teams环境中共享内容，促进同事之间的积极信息交换。 用户参与应用以与团队成员共享感兴趣的项目、发现新的共享内容、设置首选项和书签收藏夹以供以后阅读。 |[立即共享](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)| |SharePoint列表搜索|Microsoft Teams中的协作通常引用SharePoint列表中的项中包含的信息。 粘贴相关项目的链接会强制每个人将上下文从对话中切换，查找所需的信息，然后返回Teams继续对话。 随着对话的继续，人们必须多次切换回引用项，以验证新注释并刷新对项目中包含的信息的记忆。 此上下文切换会创建一个用于平滑协作的屏障。 若要解决此问题，请使用列表搜索应用模板。 许多用户使用SharePoint为组织中的某些核心工作流提供电源。 但是，围绕列表进行协作是很困难的。 使用Microsoft Teams中的列表搜索应用模板，用户可以直接在聊天对话中插入SharePoint列表项中的信息，以缓解在聊天中插入链接时导致的上下文切换。 信息插入为易于阅读的自动格式卡片，可帮助用户继续参与对话。 |[SharePoint列表搜索](https://github.com/OfficeDev/microsoft-teams-list-search-app)| |工作人员签入|员工签入是基于[Power Apps](/powerapps/powerapps-overview)的应用，可在业务和现场人员之间进行监督通信。 工作人员可以直接从Teams定期或临时提供时间关键信息和状态更新。 该应用支持实时位置、照片、笔记、提醒通知和自动化工作流。|[工作人员签](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)入| |调查|调查是一个自定义Microsoft Teams[消息传递扩展](../messaging-extensions/what-are-messaging-extensions.md)应用，可用于在聊天或频道中创建调查，以收集数据并获取可操作的见解。 该应用在所有Teams平台客户端（如桌面、浏览器、iOS 和 Android）中受支持，并且已准备好作为Microsoft 365订阅的一部分进行部署。 |[调查](https://github.com/OfficeDev/Microsoft-Teams-Survey-app) | |时间计数|项目可以包含多个任务，并且可以将各种项目分配给员工。 经理需要通过员工在这些任务上花费的时间来了解项目进度。 这可能是一个繁琐的活动，因为员工需要填写时间表。 通过时间计数应用，员工可以使用移动设备快速填写时间表，并且经理无需在时间表条目中跟进员工。 管理者可以根据资源查看项目利用率，并且他们可以批准或拒绝这些条目。 发送提醒通知以确保时间表符合性。 此外，历史数据和利用率也可用于分析。 |[时间计数](https://github.com/OfficeDev/microsoft-teams-apps-timetally)| |培训|培训是一种自定义[Teams消息传递扩展](../messaging-extensions/what-are-messaging-extensions.md)应用，使用户能够在聊天或频道中发布培训以进行脱机知识共享和提升技能。 该应用在多个Teams平台客户端（如桌面、浏览器、iOS 和 Android）中受支持。 此应用已准备好部署为Microsoft 365订阅的一部分。|[训练](https://github.com/OfficeDev/microsoft-teams-apps-training)| |虚拟舍入|医院和急诊室提供程序每天进行多次 **轮次**。 这些对患者的快速签入旨在提供患者如何做状态检查，并确保病人的顾虑得到解决。 虽然舍入是确保患者受到多种类型的提供程序监视的基本做法，但它们代表着 PPE 的巨大流失，因为每次访问时，从每个提供程序，都会使用一个新的口罩和一组新的手套。 使用此应用模板，医务工作者可以通过提供程序和患者之间的Microsoft Teams会议轻松进行轮次。 Microsoft Health和生命科学[博客文章](https://aka.ms/teamsvirtualrounding)中也引用了虚拟舍入解决方案。|[虚拟舍入](https://github.com/SmartterHealth/Virtual-Rounding)| |访问者管理|访问者管理应用使组织和员工能够直接从Microsoft Teams轻松高效地管理现场访问者过程。 该应用使员工能够创建访问者请求，通过访问者仪表板集中跟踪请求状态，并在访问者到达时接收实时通知。|[访问者管理](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement)| |水冷却器|水冷却器是一种自定义Teams应用，使企业团队能够在队友之间创建、邀请和加入休闲对话，例如由水冷却器或休息室进行的对话。 将此模板用于多个方案，例如新的非项目相关公告、感兴趣的主题、当前事件或有关爱好的对话。 该应用为任何人都提供了一个轻松的界面来查找现有对话或启动新对话。 它是构建自定义定向通信功能的基础，促进同事之间的互动，否则，他们可能不会有机会在休息期间进行社交活动。 主要功能包括： <br/> **水冷却器主页**：可以浏览现有会议室，其中团队成员正在与某些感兴趣的人员或主题在现有对话中进行交互。 **主页** 上的活动对话显示会议室名称、简短说明、通话持续时间和会议室图像。 <br/>**加入室**：使用 **联接室** 功能立即加入正在进行的对话。 从活动对话中选择 **“加入** ”以加入会议室。<br/>**会议室创建**：使用 **会议室创建** 功能创建Teams呼叫或聊天，让所有与会者进行交互。 通过将会议室名称、简短说明、最多五位同事指定为初始组并从提供的房间图像集中进行选择，轻松创建会议室。 <br/>**查找聊天室**：使用 **“查找房间** ”功能搜索与主题匹配的关键字或正在进行的对话的简短说明。<br/>**与会者邀请**：使用 **与会者邀请** 功能在创建会议室后邀请其他用户。 这类似于Teams调用。<br/>**应用徽章**：左侧菜单上的 **“水冷却器**”图标显示一个徽章，其中包含使用任何应用时从Teams可见的活动对话数。 |[水冷却器](https://github.com/microsoft/csapps-msteams-watercooler)| |工作区奖|工作区奖是一个Teams应用模板，提供积极的框架，以促进认可和鼓励员工在现代工作场所的欣赏文化。 通过该应用，你可以设置和管理员工奖励和认可（称为 R&R 计划），员工可以轻松地提名和认可同事，R&R 领导可以查看提交的提名、授予奖励和公布收件人。|[工作区奖](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards) |

若要提供反馈，请参阅 [应用模板反馈](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u)。

## <a name="see-also"></a>另请参阅

* [集成 web 应用](~/samples/integrate-web-apps-overview.md)
* [了解Microsoft Teams应用功能](../concepts/capabilities-overview.md)
* [为个人应用设计Microsoft Teams](../concepts/design/personal-apps.md)
* [设计系统](../concepts/design/design-teams-app-fundamentals.md)
* [将对话从机器人过渡到人类](/azure/bot-service/bot-service-design-pattern-handoff-human)
* [如何部署Teams应用模板](/microsoft-365/community/how-to-deploy-teams-app-templates)
