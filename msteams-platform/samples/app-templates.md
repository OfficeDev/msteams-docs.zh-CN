---
title: Microsoft Teams 的应用模板
description: 了解如何使用 Microsoft Teams 平台的应用模板，这些模板均提供了有关部署和安装应用的详细说明。
ms.topic: reference
ms.localizationpriority: medium
ms.author: lajanuar
author: surbhigupta
ms.openlocfilehash: 5cba55e573420068b9b6a2a19168d7011dc64228
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143093"
---
# <a name="app-templates-for-microsoft-teams"></a>Microsoft Teams 的应用模板

应用模板是适用于 Microsoft Teams 的完整应用示例，它们是开源的，可在 GitHub 上获得。 每个应用模板都包含有关为组织部署和安装该应用的详细说明。 它还会提供一个示例应用，你可以立即安装并开始使用。 此外，还提供有完整的源代码，以供你进行详细研究，或者对代码进行分支开发和更改，使其满足特定要求。
所有应用模板都将根据 [MIT 许可](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE)条款提供。

> [!NOTE]
> 必须为用户和组织授权和支持从应用模板创建的应用。

使用应用模板的主要优点是：

* **直接部署到云：** 所有应用模板都包含部署脚本，可用于托管Microsoft Azure或 Power Platform 中所需的所有服务。
* **建议的示例代码：** 应用模板符合有关安全和基础结构的建议最佳做法。 我们会对社区提交的所有应用模板更改进行审核，以确保合规性。
* **可自定义且可扩展：** 虽然所有应用模板都以最少的配置进行部署，但会提供整个代码库和部署脚本，以便你可以轻松自定义或扩展这些模板，来满足你的独特需求。
* **详细文档：** 所有应用模板都附有有关解决方案体系结构、部署和配置步骤的端到端文档。  

## <a name="adoption-tool--champion-management-platform"></a>采用工具 - Champion Management Platform

Champion Management Platform (CMP) 应用模板可帮助你管理、扩大和激励团队冠军队伍，实现更多目标。 此应用模板基于 SharePoint 框架构建，并将加载到团队内的选项卡中。 小组可以利用此工具来帮助管理计划成员身份、提供用于日志记录的排行榜和事件类型，以及为计划参与者覆盖数字徽章的工具。

[在 GitHub 上获取该模板](https://github.com/OfficeDev/microsoft-teams-apps-champion-management)

## <a name="adoption-tool--microsoft-365-learning-pathways-get-started"></a>采用工具 - Microsoft 365 学习路径（入门）

通过“入门”应用模板，可以将 Microsoft 365 学习路径的功能引入 Microsoft Teams。 使用此应用模板，可轻松授予对特定培训页面或其他 Intranet 资产的访问权限，以及直接在 Teams 中加载内容。 你还可以更改应用名称或徽标以匹配公司品牌。

[在 GitHub 上获取该模板](https://github.com/msft-teams/tools/tree/master/M365%20Learning%20Pathways)

## <a name="company-communicator"></a>Company Communicator

通过 Company Communicator 应用，公司团队能够创建和发送面向多个团队或大量员工的聊天消息，从而使组织能够在员工进行协作的位置与员工联系。 将此模板可用于多种场景，例如新计划公告、员工入职、新式学习、开发或组织范围的广播。

该应用可为指定用户提供一个易于使用的界面，供其创建、预览、协作和发送消息。

它为构建自定义目标通信功能提供了基础，例如基于确认消息或与消息交互的用户数的自定义遥测。

[在 GitHub 上获取该应用](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![Company Communicator 撰写框视图](../assets/images/CompanyCommunicatorCompose.png)

## <a name="co-worker-appreciation"></a>同事感谢

使用 Microsoft Teams 中的同事感谢模板，用户可以在 Teams 环境中赞赏同事的成就。 当同事选择奖励同事时，接收者和其他团队成员会在频道对话中被标记，并收到有关频道奖励详细信息的通知。 奖励将记录在 Teams 应用中，该应用安全、可移植且易于共享。 这被视为 Open Badges 应用模板的 PowerApps 版，具有排行榜功能。

[在 GitHub 上获取该模板](https://github.com/OfficeDev/microsoft-teams-apps-coworker-appreciation)

![整体](../assets/images/coworker-appreciation-1.png)

## <a name="faq-plus"></a>常见问题 +

对话问答机器人是一种可对用户常见问题进行解答的简单方法。 但是，大多数机器人无法以有意义的方式与用户互动，因为当机器人失败时，循环中没有人。 常见问题解答机器人是一个友好的 Q&机器人，当用户无法提供帮助时，它会将用户引入循环中。 可以向机器人提问，如果机器人包含在知识库中，则机器人会回答问题。 如果没有，机器人允许用户提交查询，然后将查询发布到预先配置的专家团队，这些专家团队通过处理团队内部的通知来提供支持。

> [!NOTE]
> 最新版本的 **FAQ Plus** 支持改进的问答解决方案，可支持专家团队完成以下操作：
>
> &#x2714; 使用消息扩展直接向知识库添加新的问答。
>
> &#x2714; 编辑和删除机器人添加的问答对。
>
> &#x2714; 跟踪问答的修订历史记录。
>
> &#x2714; 配置包含其他详细信息的答案，以显示为[自适应卡](../task-modules-and-cards/cards/cards-reference.md#adaptive-card)。
>
[在 GitHub 上获取该机器人](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![FAQ Plus gif](../assets/images/FAQPlusEndUser.gif)

## <a name="icebreaker"></a>Icebreaker

Icebreaker 是一个 [Microsoft Teams 机器人](../bots/what-are-bots.md)，通过每周随机安排两名团队成员会面来帮助提高团队凝聚力。 该机器人通过自动建议对两个成员都有效的空闲时间来简化日程安排。 通过此应用，可加强个人联系并构建联系紧密的社区。

除了在整个团队中鼓励建立个人联系外，Icebreaker 应用还可以帮助在组织内培养基于兴趣的社区。 例如，可以将此应用用于开发运营兴趣小组，以便在组织中有机地传播各种创意和最佳实践。

[在 GitHub 上获取该应用](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Icebreaker 应用](../assets/images/icebreaker.png)

## <a name="new-employee-onboarding"></a>新员工入职

“新员工入职”是一种集成的 Microsoft Teams 和 [SharePoint 新员工入职解决方案](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19)，可帮助你的组织在新员工旅程中为员工提供一致、高质量的入职体验。 人力资源团队和招聘经理可使用该应用在整个任职培训和指导过程中提供相关信息，而新员工则可使用该应用来共享反馈、提供简介和完成入职任务。

[在 GitHub 上获取该解决方案](https://github.com/OfficeDev/microsoft-teams-apps-newemployeeonboarding)

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

应用模板代码示例是用于实现 Microsoft Teams 平台功能的示例应用的集合。

> [!NOTE]
> * Microsoft 没有主动管理源代码。完整的源代码是开放源代码，你可以浏览、分支和修改源代码以满足特定要求。
> * 请勿使用 Microsoft Power Platform 创建要发布到 Teams 应用商店的应用。 Microsoft Power Platform 应用只能发布到组织的应用商店。

下表描述了应用模板代码示例：  

|名称|应用场景|GitHub 链接| |---------|---------||-------| |Adoption Bot |Adoption Bot 是使用 Power Virtual Agent for Teams PVA 构建的用户服务聊天机器人。 它被视为常见问题解答 Plus 的 PVA 版本。 Adoption Bot 可解答有关 Microsoft 365 和 Teams 的 100 多个常见问题。 你可以编辑现有主题、添加自己的主题以及引入现有常见问题解答。 如果用户需要额外帮助，Adoption Bot 可以将其连接到专家，甚至可以为其扩展至使用高级流连接器的开放式服务票证。 此机器人是自安装的或内置于自定义应用（如[采用中心](https://github.com/akporzondek/adoption_hub)）中。 | [Adoption Bot](https://github.com/OfficeDev/microsoft-teams-apps-adopt-bot) | | Appointment Manager | Appointment Manager 是一个 Teams 应用模板，可帮助企业通过 Teams 创建、管理和执行与消费者的虚拟约会。 来自使用者的新约会请求在Teams频道中可见，这些请求会在其中快速分配并重新分配给团队中的员工。 用户将通过自定义选项卡在团队或个人级别查看约会请求。 每个约会都与 Teams 联机会议相关联，因此员工和消费者可以在计划的时间轻松加入会议。 该应用模板与 Microsoft Bookings 集成，以便轻松进行约会管理。 计划的约会会自动出现在所分配工作人员的日历上，消费者会收到可自定义的电子邮件通知和提醒，且其中包含嵌入式会议链接。| [Appointment Manager](https://github.com/OfficeDev/microsoft-teams-apps-appointment-manager) | | Ask Away | Ask Away 是一款 [Microsoft Teams 机器人](../bots/what-are-bots.md)，可支持用户在 Teams 中进行问答（称为问答会话）。 使用 Ask Away 机器人，团队成员可以提交和投票支持同事共享的问题，因此问答主持人可以轻松地在一个频道或聊天中收集最重要的问题。 该机器人用于在 Teams 会议中进行实时问答会话，并允许与会者通过聊天实时提交问题。 | [Ask Away](https://github.com/OfficeDev/microsoft-teams-apps-askaway) | | Associate Insights |Associate Insights 是一个 [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) 模板，使一线员工能够直接捕获和提交客户意见、情绪和看法。 一线员工通常是第一位与客户进行一对一联系的公司代表。 收集的数据由业务团队通过某种途径（例如 Power BI Teams 选项卡）共享和协作使用，以改进产品并增强客户体验。 | [关联Insights](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)| |出席人数|Attendance 应用是固定在团队中的[Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)选项卡。 它旨在记录设置中的状态，例如学习和训练环境。 用户可以标记或编辑过去最多 30 天的参加情况，并查看整个组或单个参与者的汇总参加情况报告。   | [Attendance](https://github.com/OfficeDev/microsoft-teams-apps-attendance) | |Book-a-room | Book-a-room 是一个 [Microsoft Teams 机器人](../bots/what-are-bots.md)，可帮助用户快速查找并从当前时间开始预定会议室 30、60 或 90 分钟。 默认时间为 30 分钟。 Book-a-room 机器人适用于个人或 1:1 对话。| [Book-a-room](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom) | | Building Access | Building Access 是基于 Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) 的应用，可帮助设施主管管理、跟踪和报告员工的现场状态，从而实现建筑物人员限流管理和社交距离规范管理。 该应用使用 Microsoft [Power Apps](/powerapps/powerapps-overview) 和 [Power Automate](/power-automate/getting-started) 构建而成，并与 Microsoft Teams 深度集成，可帮助组织确定建筑物的可用状态、建立出入现场的资格标准，并收集用于未来规划的见解。 | [Building Access](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess) | | Celebrations |Celebrations 是一个 Teams 应用，可帮助团队成员庆祝彼此的生日、纪念日和其他定期活动。 它会记住所有团队成员的特殊情况，并在创建活动时在选择的所有团队中发送友好消息，从而让团队成员在其个人的特殊日子感到特别。 该应用为所有团队成员提供了一个轻松的界面来亲自添加和查看其事件，还允许用户选择共享事件的团队。 | [Celebrations](https://github.com/OfficeDev/microsoft-teams-celebrations-app) | | Checklist | Checklist 是一款自定义 Microsoft Teams [消息扩展](../messaging-extensions/what-are-messaging-extensions.md)应用，可让你通过在聊天或频道中创建共享清单来与团队协作。 所有 Teams 平台客户端（如桌面、浏览器、iOS 和 Android）都支持该应用。 该应用可部署为 Microsoft 365 订阅的一部分。  | [Checklist](https://github.com/OfficeDev/microsoft-teams-checklist-app)| | Classroom Drop-in | Classroom Drop-in 是一种基于 Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) 的应用，可帮助系统负责人找到班级团队（即虚拟教室），并根据需要在指定的旁听时段内将自己或其他人添加到这些班级团队中。 该应用使用 Microsoft [Power Apps](/powerapps/powerapps-overview) 和 [Power Automate](/power-automate/getting-started) 构建而成，并与 Microsoft Teams 深度集成，可确保教育机构能够根据业务要求为相关利益干系人提供对班级团队的访问权限，从而优化其在混合学习环境中的运营。| [Classroom Drop-in](https://github.com/OfficeDev/microsoft-teams-apps-classroom-dropin) | | Contact Group Lookup | Contact Group Lookup 应用提供了一种方便且有用的方法来创建、访问和管理组织的联系人组（以前称为通讯组列表或通信组）。 用户可以快速查看组成员并与之聊天、查看成员状态，以及创建与联系人组中所选成员的群组聊天，所有这些均在 Teams 环境中完成。| [Contact Group Lookup](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)| | CrowdSourcer | CrowdSourcer 是一个 [Microsoft Teams 机器人](../bots/what-are-bots.md)，它为团队提供通过组成员协作获得的查询信息。 它有助于回答常见问题，同时使参与者能够积极参与完善一个有趣且有用的信息资源并与之互动。| [CrowdSourcer](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)| |Custom Stickers | 自我表达是健康的团队文化的核心。 此应用模板是一个[消息扩展](~/messaging-extensions/what-are-messaging-extensions.md)，它使用户能够在 Microsoft Teams 中使用自定义贴纸和 GIF。 此模板提供基于 Web 的简单配置体验，任何具有配置访问权限的人都可上传他们希望其用户拥有的 GIF、贴纸和图像，从而让整个团队均可使用你选择的任何贴纸集。 此应用还允许跨团队轻松共享图像、GIF、贴纸，而无需访问作为存储和共享机制的 SharePoint 网站或单个频道。 例如，产品团队可以以编程方式轻松地将产品图像和 GIF 共享到社交媒体、市场营销和销售团队。 此外，还可以通过在有新图像和 GIF 可用时，触发针对特定团队或个人的通知流来扩展此应用。| [Custom Stickers](https://github.com/OfficeDev/microsoft-teams-stickers-app) | | Employee Ideas | Employee Ideas 应用是基于 Azure 的 Great Ideas 应用模板的 PowerApps 版本。 该应用使 Teams 用户能够设置和配置创意活动。 创意活动是一个类别，用于围绕常见主题对创意进行分组。 Teams 用户还可以执行以下活动：<br/> 配置员工必须针对每个创意提交的标准提交表单。<br/>查看和管理活动创意和列表。 <br/>修改和删除活动。 <br/> 查看创意排行榜。 <br/> 投票支持并分享优先考虑的创意。 <br/> 提交活动的创意。 <br/> 查看其他团队成员的创意。 <br/>对最喜欢的创意进行投票。 <br/> 查看自己的创意相较于活动中其他创意的表现。|[Employee Ideas](https://github.com/OfficeDev/microsoft-teams-apps-employeeideas) | |E-Prescriptions| E-Prescriptions 是基于 [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) 的应用，它通过自动完成向患者开具电子处方的过程来增强远程医疗和虚拟护理。 医疗专业人员可以快速查看预约、生成电子处方，以及直接在 Teams 平台内向患者发送带有电子处方附件的电子邮件。|[E-Prescriptions](https://github.com/OfficeDev/microsoft-teams-apps-eprescription)| | Employee Training | Employee training 是一种 Microsoft Teams 应用，它使组织者能够轻松地发布、跟踪和推广组织的学习和培训活动。  借助该应用，活动策划人员可以向活动注册人发送提醒和通知，员工则可以表示对即将发生的活动的兴趣、随时了解当前活动，并通过 Teams 消息扩展与同事共享活动详细信息。|[Employee Training](https://github.com/OfficeDev/microsoft-teams-apps-employeetraining)| | Expert Finder| Expert Finder 是一个 [Microsoft Teams 机器人](../bots/what-are-bots.md)，它根据特定组织成员的技能、兴趣和教育属性来标识他们。 成员在组织中查找与 Microsoft Azure Active Directory (Azure AD) 用户配置文件的关键字搜索匹配的专家。| [Expert Finder](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)| | Get Support 应用| 使用 Microsoft Teams 的组织可以使用 Get Support 应用，支持任何一组用户向主管请求帮助。 此应用包括以下功能： <br/>从 Power App 请求不同类别的帮助。<br/>发送给请求者的通知，通知他们分配了谁。<br/> 发送给分配的主管的通知，告知他们谁需要帮助。 <br/>分析 SharePoint 和 Power BI 中的升级和模式。|[Get Support 应用](https://github.com/OfficeDev/microsoft-teams-app-get-support/) | | Goal Tracker|Goal Tracker 应用是一个全面的解决方案，可帮助组织在 Microsoft Teams 中建立目标、观察进展并确认成功。 该应用使用户能够在职业、个人和团队级别上设置、跟踪和更新目标。 团队成员还会及时收到提醒和状态更新，以保持专注并确保一切正常。|[Goal Tracker](https://github.com/OfficeDev/microsoft-teams-app-goaltracker) | | Great Ideas| Great Ideas 应用可在组织中支持并增强创新和创造力。 借助该应用，员工可以在 Microsoft Teams 中与同事和领导分享创意、发现新提交的内容、聚焦供同事考虑的贡献，以及投票选出最佳提案。 |[Great Ideas](https://github.com/OfficeDev/microsoft-teams-apps-greatideas) | |Group Activities | Group Activities 是一个 Microsoft Teams 应用，它使团队所有者能够轻松地在 Microsoft Teams 环境中快速创建活动组和管理协作工作流。 活动作者可以创建活动、在组中随机分配团队成员，并且可以选择让机器人发送提醒，直到活动完成。|[Group Activities](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities) | |Group Connect |Group Connect 是一种 Microsoft Teams 应用，可帮助组织成员发现员工组并查找与员工组相关的信息。 该应用内置了丰富的功能，可支持组织领导者与其员工就组、活动和资源进行沟通。 Group Connect 应用还可按所需频率将组成员相互匹配，以鼓励组内的人际交往和融合。 有关如何借助 Group Connect 应用在组织中培养员工组的详细信息，请参阅 GitHub 上的该应用。 |[Group Connect](https://github.com/OfficeDev/microsoft-teams-apps-groupconnect) | |Grow Your Skills | Grow Your Skills 应用可让员工在学习新技能的同时为组织的补充项目做出贡献，从而支持其职业成长和发展。 员工可以使用该应用查找满足他们兴趣的机会，与同行进行有意义的协作，并获得新的专业知识和功能，所有这些都位于Teams环境中。|[提高技能](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)| |HR 支持|HR支持机器人是一个友好的 Q&机器人，当 HR 团队无法提供帮助时，它会在循环中引入支持专业人员或专家。 可以向机器人提问，如果机器人包含在知识库中，则机器人会回答问题。 如果没有，机器人允许用户提交查询，然后将其发布到预配置的专家团队中，这些专家团队可通过处理来自其团队内部的通知来提供支持。 此外，该机器人还将通过搜索问题中的预配置标记来推荐指向建议的 HR 策略或问题的链接。 这些磁贴可作为快速参考在关联的选项卡中找到。 HR Support 适用于轻型问答，可在组织中启动新项目或计划时提供快速支持。 |[HR Support](https://github.com/OfficeDev/microsoft-teams-hrsupport-app) | |Incentives | Incentives 是一个 [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) 模板，用于管理和跟踪激励员工参与指定活动（如培训和变革管理计划）的情况。 管理员可使用该应用建立指定的活动、分配完成点，并指定获得奖励所需的资格点级别。 员工使用该应用查看其累积积分，并在获得资格后请求并申请可兑换的奖励。|[Incentives](https://github.com/OfficeDev/microsoft-teams-apps-incentives) | |Incident Reporter | Incident Reporter 是一个 [Microsoft Teams 机器人](../bots/what-are-bots.md)，可优化组织中事件的管理。 该机器人有助于自动完成事件数据收集、定制事件报告、相关利益相关者通知和端到端事件跟踪。|[Incident Reporter](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport) | | Inspection|Inspection 是一种 Microsoft Teams 应用，它使一线工作人员能够检查从位置到资产和设备的任何内容。 例如，零售商店、制造工厂或车辆和计算机。 此解决方案中有两个应用，每个应用面向不同类型的用户。 该应用使一线工作人员能够检查资产或区域、管理产品和服务的质量，或维护工作场所的安全。 它有助于团队成员之间的沟通，以解决在检查期间发现的问题。 该应用可为经理提供简单的报告，以加快问题解决并突出显示相应趋势。 |[Inspection](https://github.com/OfficeDev/microsoft-teams-apps-inspection) | |Issue Reporting | Issue Reporting 应用使员工和经理能够提出和管理问题。 它由两个应用组成：用于报告问题的 Issue Reporting 应用和用于管理问题的 Manage Issues 应用。 团队经理使用 Manage Issues 应用来配置应用体验，包括该应用用于创建 Microsoft Teams 消息和 Planner 任务的频道。 经理还可使用该应用创建模板表单，以便在用户报告问题时收集详细信息。 例如，查看、编辑或删除问题模板表单。 该应用还用于查看团队问题、报告问题历史记录以及高效管理问题解决。 员工使用 Issue Reporting 应用来记录问题和解决问题所需的详细信息。 该应用还可用于修改和解决现有问题，以及获取个人或团队问题的高级别视图。 |[Issue Reporting](https://github.com/OfficeDev/microsoft-teams-apps-issuereporting) | | Open Badges| Open Badges 是一个 Microsoft Teams 应用，它使个人能够在 Teams 环境中获得数字学习证书徽章，并在任何地方共享这些徽章。 使用来自第三方数字徽章颁发机构 [Badgr](https://badgr.org/) 的功能，奖励的徽章将记录在接收人的 Badgr 配置文件中，并可用于构建和共享丰富的生命周期学习旅程图片。|[Open Badges](https://github.com/OfficeDev/microsoft-teams-apps-openbadges) | | Poll| Poll 是自定义的 Microsoft Teams [消息扩展](../messaging-extensions/what-are-messaging-extensions.md)应用，可让你在聊天或频道中快速创建和发送投票，以收集团队意见和偏好。 该应用在所有 Teams 平台客户端（如桌面、浏览器、iOS 和 Android）中均受支持，并且可部署为 Microsoft 365 订阅的一部分。|[Poll](https://github.com/OfficeDev/microsoft-teams-poll-app) | | Quick Responses| Quick Responses 是一种 Microsoft Teams 应用，可提供可靠的解决方案来有效回答用户的常见问题。 该应用可通过 Teams [消息扩展](../messaging-extensions/what-are-messaging-extensions.md)生成响应库，而不是手动回答每个查询并不断重复相关信息。|[Quick Responses](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses) | |Quiz | Quiz 是自定义 [Teams 消息扩展](../messaging-extensions/what-are-messaging-extensions.md)应用，可用于在聊天或频道中创建测验以进行知识检查并即时提供结果。 你可以在团队中使用 Quiz 来进行课堂内和脱机考试、知识检查以及趣味测验。 Quiz 应用支持多个平台，例如 Teams 桌面、浏览器、iOS 和 Android 客户端。 此应用可部署为现有 Microsoft 365 订阅的一部分。|[Quiz](https://github.com/OfficeDev/microsoft-teams-apps-quiz) | | Rapid Assist|Rapid Assist 是基于 Microsoft [Power Platform](https://powerapps.microsoft.com/blog/) 的应用。借助该应用，面向客户的关联人员可快速与专家联系以快速获取答案、搜索信息、跟进打开的请求，而专家则可以接收通知以快速接听电话，帮助回答问题。 该应用使用 Microsoft [Power Apps](/powerapps/powerapps-overview) 和 [Power Automate](/power-automate/getting-started) 构建而成，并与 Microsoft Teams 深度集成，可帮助组织轻松地将一线员工与公司联络人员联系起来，以解决客户查询并提供出色的客户体验。 |[Rapid Assist](https://github.com/OfficeDev/microsoft-teams-apps-rapid-assist) | | Reflect|Reflect 是一个自定义 Microsoft Teams [消息扩展](../messaging-extensions/what-are-messaging-extensions.md)应用，可为团队成员提供安全且包容的资源，支持其直接在 Teams 内与同事或组领导分享他们的情绪健康状况。 该应用在频道、群组、会议和 1:1 聊天中可用，调查响应设置可为公开、仅发送方可知或完全匿名。 |[Reflect](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect) | |Remote Support | Remote Support 是一个 [Microsoft Teams 机器人](../bots/what-are-bots.md)，用于在整个组织的支持请求者与内部支持团队之间提供集中接口。  最终用户可以提交、编辑或撤回支持请求，支持团队则可以响应、管理和更新 Teams 平台内的所有请求。|[Remote Support](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport) | | Request-a-team|Request-a-team 是一个 Microsoft Teams 应用，可优化企业组织的新团队创建。 通过集成向导引导式请求表单、嵌入式审批流程、请求状态仪表板和自动化团队构建，该应用可在创建新的团队实例时支持标准化和最佳做法|[Request-a-team](https://github.com/OfficeDev/microsoft-teams-apps-requestateam) | |Scrums for Channels |Scrums for Channels 是一个 Scrum 助手应用，可让用户在 Microsoft Teams 的频道中计划和运行 Scrum。 该应用非常适合远程团队和成员来自不同地理位置和时区的团队，可支持他们共享每日更新并确保参与 Scrum 站会。|[Scrums for Channels](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels) | | Scrums for Group Chat| Scrums Status 应用模板进行了更新，现称为 Scrums for Group Chat。 Scrums for Group Chat 是一种支持性 Scrum 助手，它使群聊成员能够进行异步站会并轻松共享其每日更新。 它允许群聊的所有成员参与 Scrum，并查看其他人在正在运行的 Scrum 中所做的更新。 |[Scrums for Group Chat](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat) | |Share Now | Share Now 应用可支持用户在 Teams 环境中轻松共享内容，以促进同事之间的积极信息交换。 用户可使用该应用与团队成员共享感兴趣的项目、发现新的共享内容、设置首选项，以及为最喜爱的内容加书签以供以后阅读。 |[立即共享](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)| |SharePoint列表搜索|Microsoft Teams中的协作通常引用SharePoint列表中的项中包含的信息。 粘贴指向相关项目的链接会强制每个人离开对话背景、查找所需的信息，然后再返回到 Teams 以继续对话。 随着对话的继续，人们必须多次切换回引用项，以验证新注释并重新记忆项目中包含的信息。 这种背景切换为顺利合作制造了障碍。 若要解决此问题，请使用 List Search 应用模板。 许多用户使用 SharePoint 来为组织中的某些核心工作流提供支持。 但是，围绕列表进行协作是很困难的。 使用 Microsoft Teams 中的 List Search 应用模板，用户可以直接在聊天对话中插入 SharePoint 列表项中的信息，以缓解在聊天中插入链接时导致的背景切换。 信息作为易于阅读的自动格式卡片插入，可帮助用户继续进行对话。 |[SharePoint List Search](https://github.com/OfficeDev/microsoft-teams-list-search-app) | |Staff Check-ins | Staff Check-ins 是基于 [Power Apps](/powerapps/powerapps-overview) 的应用，可在业务和现场人员之间进行监督通信。 员工可以轻松地按计划或临时直接从 Teams 提供时间关键信息和状态更新。 该应用支持实时位置、照片、笔记、提醒通知和自动化工作流。|[Staff Check-ins](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins) | | Survey|Survey 是一个自定义 Microsoft Teams [消息扩展](../messaging-extensions/what-are-messaging-extensions.md)应用，可用于在聊天或频道中创建调查，以收集数据并获取可作为操作依据的见解。 该应用在所有 Teams 平台客户端（如桌面、浏览器、iOS 和 Android）中均受支持，并且可作为 Microsoft 365 订阅的一部分进行部署。 |[Survey](https://github.com/OfficeDev/Microsoft-Teams-Survey-app) | |Time Tally | 一个项目可以包含多个任务，并且可以将各种项目分配给员工。 经理需要根据员工在这些任务上花费的时间来了解项目进度。 这可能是一项繁琐的活动，因为员工需要填写时间表。 时间计数应用使员工能够使用移动设备快速填写时间表，并且经理无需在时间表条目中跟进员工。 经理可以根据资源查看项目利用率，并且他们可以批准或拒绝所填内容。 系统将发送提醒通知，以确保员工遵守时间表要求。 此外，历史数据和利用率也可用于分析。 |[Time Tally](https://github.com/OfficeDev/microsoft-teams-apps-timetally) | | Training | Training 是一种自定义 [Teams 消息扩展](../messaging-extensions/what-are-messaging-extensions.md)应用，它使用户能够在聊天或频道中发布培训以进行脱机知识共享和提升技能。 多个 Teams 平台客户端（如桌面、浏览器、iOS 和 Android）支持该应用。 此应用可部署为 Microsoft 365 订阅的一部分。|[Training](https://github.com/OfficeDev/microsoft-teams-apps-training) | |Virtual Rounding | 医院和急诊室的医务人员每天都要进行多次 **查房**。 这些对患者的快速检查旨在检查患者的状态，并确保患者的担忧得到解决。 虽然查房是确保患者可受到多种类型的医务人员监管的一项基本实践，但这意味着 PPE 的巨大消耗，因为每次就诊时，每个医务人员都会使用一个新口罩和一套新手套。 使用此应用模板，医务工作者可以通过医务人员和患者之间的 Microsoft Teams 会议轻松进行虚拟查房。 Microsoft 健康与生命科学[博客文章](https://aka.ms/teamsvirtualrounding)中也提到了 Virtual Rounding 解决方案。|[Virtual Rounding](https://github.com/SmartterHealth/Virtual-Rounding) | |Visitor Management | Visitor Management 应用使组织和员工能够直接从 Microsoft Teams 轻松高效地管理现场访客流程。 该应用使员工能够创建访客请求，通过访客仪表板集中跟踪请求状态，并在访客到达时接收实时通知。|[Visitor Management](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement) | |Water Cooler |Water Cooler 是一种自定义 Teams 应用，它使企业团队能够创建、加入和邀请他人加入队友之间的休闲对话，例如在冰水机旁或休息室进行的对话。 此模板可用于多个场景，例如新的非项目相关公告、感兴趣的主题、当前事件或有关兴趣爱好的对话。 任何人都可以使用该应用来轻松查找现有对话或开启新对话。 它是构建自定义目标通信功能的基础，促进同事之间的交互，否则他们可能没有机会在休息期间进行社交活动。 主要功能包括： <br/> **Water Cooler 主页**：你可以浏览现有聊天室，其中有团队成员正在与某些人或就感兴趣的主题在现有对话中进行交互。 **主页** 上的活动对话显示有聊天室名称、简短说明、通话持续时间和聊天室图像。 <br/>**加入聊天室**：使用 **加入聊天室** 功能，可立即加入正在进行的对话。 请从活动对话中选择“**加入**”以加入聊天室。<br/>**聊天室创建**：使用 **聊天室创建** 功能，可创建 Teams 通话或聊天，让所有参与者进行交互。 通过指定聊天室名称、简短说明、作为初始组的最多五位同事并从提供的聊天室图像集中进行选择，可轻松创建聊天室。 <br/>**查找聊天室**：使用 **“查找房间** ”功能搜索关键字，该关键字与主题或正在进行的对话的简短说明匹配。<br/>**参与者邀请**：使用 **参与者邀请** 功能在创建聊天室后邀请其他用户。 这类似于 Teams 通话。<br/>**应用徽章**：左侧菜单上的 **冷水机** 图标显示有一个徽章，其中包含在使用任何应用时从 Teams 中可见的活动对话数。 |[Water Cooler](https://github.com/microsoft/csapps-msteams-watercooler) | | Workplace Awards| Workplace Awards 是一个 Teams 应用模板，它提供了一个积极的框架，可在现代化的工作场所中促进互相认可并鼓励员工表达感谢。 通过该应用，你可以设置和管理员工奖励和认可（称为 R&R 计划），员工可以轻松地提名和认可同事，R&R 领导可以查看提交的提名、授予奖励和公布接收者。|[Workplace Awards](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards) |

若要提供反馈，请参阅[应用模板反馈](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u)。

## <a name="see-also"></a>另请参阅

* [集成 web 应用](~/samples/integrate-web-apps-overview.md)
* [了解 Microsoft Teams 应用功能](../concepts/capabilities-overview.md)
* [设计 Microsoft Teams 个人应用](../concepts/design/personal-apps.md)
* [设计系统](../concepts/design/design-teams-app-fundamentals.md)
* [将对话从机器人过渡到人类](/azure/bot-service/bot-service-design-pattern-handoff-human)
* [如何部署 Teams 应用模板](/microsoft-365/community/how-to-deploy-teams-app-templates)
