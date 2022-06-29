---
title: App Studio for Microsoft Teams 入门
description: 在本文中，你将了解如何使用适用于 Microsoft Teams 的应用工作室和安装应用工作室来生成和管理应用。
ms.localizationpriority: medium
ms.topic: overview
ms.openlocfilehash: 6ec2e1dfc064302de096cb356641a773e7dceb35
ms.sourcegitcommit: c7fbb789b9654e9b8238700460b7ae5b2a58f216
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2022
ms.locfileid: "66485704"
---
# <a name="manage-your-apps-with-app-studio-for-microsoft-teams"></a>使用 App Studio for Microsoft Teams 管理应用

> [!WARNING]
> **试用开发人员门户**：App Studio 已演变。 使用新的[开发人员门户](https://dev.teams.microsoft.com/)配置、分发和管理 Teams 应用。 <br> App Studio 将于 2022 年 8 月 1 日前弃用。

无论你为企业开发自定义应用还是为世界各地的团队开发 SaaS 应用程序，App Studio 都可以轻松创建或集成你自己的 Microsoft Teams 应用，其方式包括简化应用程序的清单和包的创建，并提供卡片编辑器和响应控制库等有用工具。

> [!IMPORTANT]
> App Studio 当前在以下类型的 Teams 组织中不可用：
>
> * 政府社区云 (GCC)
> * GCC 高
> * DoD

## <a name="installing-app-studio"></a>安装 App Studio

App Studio 是 Teams 应用，可在 Teams 应用商店中找到。 请按照此链接直接下载 [App Studio](https://aka.ms/InstallTeamsAppStudio)。 还可以在应用商店中找到该应用。

在应用商店中，搜索 App Studio。

:::image type="content" source="../../assets/images/get-started/StoreTeamsAppStudio.png" alt-text="App studio 的应用商店条目":::

选择 App Studio 磁贴以打开应用安装页面：

:::image type="content" source="../../assets/images/get-started/teamsAppStudioConfiguration.png" alt-text="配置 app studio":::

选择“**安装**”。

:::image type="content" source="../../assets/images/get-started/TeamsAppStudio.png" alt-text="app studio":::

进入 App Studio 后，在 **“清单编辑** 器”选项卡上选择可导入现有应用或创建新应用的位置。

## <a name="app-studio-features"></a>App Studio 功能

本部分介绍聊天、清单编辑器、详细信息和功能等功能。 可以使用应用自定义自定义功能。

### <a name="conversation"></a>对话

你可以在这里查看在 App Studio [在 App Studio](#card-editor) 将卡片发送到你自己来测试这些卡片在 Teams 中的外观。

### <a name="manifest-editor"></a>清单编辑器

如前所述，Teams 应用包最重要的部分是其 manifest.json 文件。 此文件必须符合 [Teams 应用架构](~/resources/schema/manifest-schema.md)，包含元数据，使 Teams 能够将应用正确呈现给用户。

App Studio 中的“清单编辑器”选项卡简化了创建清单，允许你描述应用、上传图标、添加应用功能，并生成一个.zip文件，该文件可以轻松上传到 Teams 进行测试或分发，供其他人使用。 App Studio 不会为应用生成功能代码，也不会托管应用。 应用必须已在应用上传流程的清单中列出的 URL 上托管并运行，以产生工作应用。

#### <a name="details"></a>详细信息

清单编辑器的详细信息部分定义了要创建的应用的高级说明。 这包括应用的名称、说明和视觉品牌等内容。 可以自动生成应用程序的 GUID，并提供隐私声明和使用条款的 URL。

#### <a name="capabilities"></a>功能

清单编辑器的功能部分介绍定义应用的功能并列出其中每个功能的详细信息。

> [!NOTE]
> 最佳做法是，在自定义应用时，必须为应用用户和客户提供自定义指南。 有关详细信息，请参阅 [Microsoft Teams 中的自定义应用](/MicrosoftTeams/customize-apps)。

##### <a name="tabs"></a>选项卡

* **团队选项卡。** 团队选项卡将成为频道的一部分，可提供对团队信息和资源的快速访问。 例如，频道的"Planner"选项卡包含单个计划;Power BI 选项卡映射到特定报表。 用户可以向下钻取到相关上下文，但不应在选项卡外导航。例如，Power BI 选项卡不启用对其他 Power BI 报表的导航，但它确实启用了在主 Power BI 网站中启动报表的 *“转到网站* ”按钮。

  对于团队选项卡，必须使用 *配置 URL* 显示选项并收集信息，以便用户可以自定义选项卡的内容和体验。当用户首次将选项卡添加到频道时，将显示此 HTML 表格。

  你还必须提供选项卡期望从其加载或链接到的任何其他域。

* **个人选项卡。** 可以定义默认情况下在个人应用体验中显示的一组选项卡， (用户在团队或频道) 的上下文之外对应用拥有的体验。 在这部分内容中，提供选项卡名称、唯一标识符、指向将在 Teams 中显示的 UI 的 URL，以及用户选择在浏览器中查看选项卡时使用的 URL（可选）。 使用 Teams 选项卡，提供选项卡需要从中加载或链接到的任何其他域。

##### <a name="bots"></a>机器人

通过此部分，可以将一 [对话自动](~/bots/what-are-bots.md) 添加到应用中。 如果已向 Bot Framework 注册了机器人，则可以通过单击 *“设置* ”并提供机器人的名称 Bot Framework ID 并定义机器人的工作范围来添加该机器人。

如果尚未向 Bot Framework 注册机器人，请选择 **“注册** ”以创建新机器人。 完成注册自动程序后，请返回清单编辑器的此部分，输入其名称和 Bot Framework ID。

提供机器人信息后，现在可以选择定义机器人可以向用户建议的命令列表。 添加命令的名称、命令的说明（指示其语法和参数）以及此命令应应用到的范围 () 。

> [!NOTE]
> 如果已将机器人定义为仅支持一个作用域，则会忽略为不受支持的范围指定的命令。 你随时都可以编辑你的自动程序支持的范围。

##### <a name="connectors"></a>连接器

此部分允许向应用添加连接器。 如果已注册 Office 365 连接器，请选择" **设置** 并输入连接器的名称和 ID。 如果希望有新的连接器，请选择“ **注册** ”转到浏览器中的“连接器开发人员仪表板”。

##### <a name="message-extensions"></a>消息扩展

[消息扩展](~/messaging-extensions/what-are-messaging-extensions.md) 是用户在 Teams 中与应用互动的强大方式。 用户可以查询服务的信息，将该信息以卡片形式发布到频道或聊天对话中。

消息扩展由 Bot Framework 机器人提供支持，因此它们需要配置的机器人才能运行。 如果具有要为消息扩展提供电源的机器人的名称和 Bot Framework ID，请输入它。 否则，请选择 **“注册** ”以创建一个，然后输入信息。 选择用户是否可以更新消息扩展的配置。

配置基础机器人后，定义消息扩展可以接受的命令和参数。

每个命令都需要标题和 ID。 命令可以选择性地包含用户说明。 每个命令可支持最多五个参数，每个参数要求：

* 参数的名称，因为它显示在 Teams 客户端中，并包含在用户请求中。
* 用户友好的标题。
* 可选说明。

> [!NOTE]
> 若要使用 app studio 创建消息扩展，请参阅 [使用 app studio 创建消息扩展](~/resources/create-messaging-extension-using-appstudio.md)。

#### <a name="test-and-distribute"></a>测试和分发

定义完应用程序后，“测试和分发”部分允许将应用的定义导出为 zip 文件，然后可以将其共享并上传到 Teams 客户端进行测试。 单击"导出"以 *appname.zip* 下载默认下载目录中的 zip 文件。

##### <a name="publish-your-app-to-teams"></a>将应用发布到 Teams

在项目主页上，你可以将应用上载到团队、将应用提交到公司自定义应用商店供你组织的用户使用，或将应用提交到所有 Teams 用户的应用源。 IT 管理员会评审这些提交。 可返回" *发布* 页面，检查提交状态，并了解应用是否已获 IT 管理员批准或拒绝。这也是提交应用更新或取消当前任何活动提交的地方。

### <a name="card-editor"></a>卡片编辑器

卡片是包含短信息或相关信息的容器。 Teams 支持可具有多个属性和附件的卡片。 卡片是自动程序和连接器将可操作的信息中继给用户的一种重要方式。

为了使此过程更轻松且不易出错，“卡片编辑器”选项卡允许你使用窗体生成 Hero Card 或缩略图卡，并验证和测试生成的卡片 (完全与用户通过机器人) 一样。 它还为卡片提供相应的 JSON 或 Node.js 代码，可将其复制/粘贴到 C# 应用的源代码中。

如果已有要验证的卡片，可在 Teams 中将该卡的 JSON 粘贴到 *"添加卡信息"下的 JSON 选项卡中* 然后将其发送给自己以查看聊天中的外观。

### <a name="react-control-library"></a>反应控件库

>[!Note]
> 将来将弃用此React控件库。 请考虑使用 [Fluent-UI 响应控件作为](https://microsoft.github.io/fluent-ui-react/) 以前星尘 UI 的替代方法。

创建遵循 Teams 最佳做法的应用是使应用的外观与 Teams 客户端体验完美契合的一种好方法。 你使用的 UI 控件对于实现这一目标至关重要。 为了更轻松地创建一致的 UI，App Studio 提供了多种类别的 UI 控件，这些控件遵循 Teams 设计原则。

提供了控件和相应的"响应"组件的示例，可准备在构建应用时使用。

#### <a name="controls"></a>控件

控件包括：

* 按钮
* 下拉列表
* 复选框
* 单选按钮
* 切换
* 文本区域
* 链接
* 选项卡
* 表格
* 图标

## <a name="app-studio-to-developer-portal"></a>App Studio 到开发人员门户

App Studio 将被弃用，可以使用开发人员门户。 下表提供了开发人员门户中支持的功能的详细信息：

| 功能 | 应用程序 Studio | 开发人员门户 |
| --- | --- | --- |
| 应用分析* | ❌ | ✔️ |
| 应用功能-机器人 | ✔️ | ✔️ |
| 应用功能连接器 | ✔️ | ✔️ |
| 应用功能-消息传递扩展 | ✔️ | ✔️ |
| 应用功能会议扩展 | ❌ | ✔️ |
| 应用功能-个人应用 | ✔️ | ✔️ |
| 应用功能-选项卡 | ✔️ | ✔️ |
| 应用环境 | ❌ | ✔️ |
| 应用语言 | ✔️ | ✔️ |
| 应用清单预览和下载 | ✔️ | ✔️ |
| 应用计划和定价 | ❌ | ✔️ |
| 应用发布 | ✔️ | ✔️ |
| 应用权限 | ❌ | ✔️ |
| 与共同开发人员共享应用 | ❌ | ✔️ |
| 应用验证 | ✔️ | ✔️ |
| 创建新应用 | ✔️ | ✔️ |
| 传递 zip 包 | ✔️ | ✔️ |

\**应用分析将很快可用于 GA。*

## <a name="see-also"></a>另请参阅

[使用 Microsoft Teams 开发人员门户管理应用](~/concepts/build-and-test/teams-developer-portal.md)
