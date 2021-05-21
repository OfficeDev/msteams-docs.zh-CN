---
title: App Studio for Microsoft Teams 入门
description: 开始使用 App Studio 在 Microsoft Teams 中构建出色的应用
keywords: 应用室团队入门
localization_priority: Normal
ms.topic: overview
ms.openlocfilehash: 391086b85f0e68e1a864c3d4254bdbe62b5eaa1a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565198"
---
# <a name="quickly-develop-apps-with-app-studio-for-microsoft-teams"></a>使用 App Studio for Microsoft Teams 快速开发应用

无论你为企业开发自定义应用还是为世界各地的团队开发 SaaS 应用程序，App Studio 都可以轻松创建或集成你自己的 Microsoft Teams 应用，其方式包括简化应用程序的清单和包的创建，并提供卡片编辑器和响应控制库等有用工具。

## <a name="installing-app-studio"></a>安装 App Studio

App Studio 是一款可在 Teams 商店找到的 Teams 应用。 按照此链接直接下载[App Studio。](https://aka.ms/InstallTeamsAppStudio) 还可以在应用商店中查找该应用。

在应用商店中，搜索 App Studio。

![App studio 的应用商店条目](~/assets/images/get-started/storeteamsappstudio.png)

选择 App Studio 磁贴以打开应用安装页面：

![配置 app studio](~/assets/images/get-started/teamsappstudioconfiguration.png)

选择“**安装**”。

![app studio](~/assets/images/get-started/teamsappstudio.png)

在 App Studio 中后，单击 **清单编辑器** 选项卡，可在其中导入现有应用或创建新应用。

## <a name="app-studio-features"></a>App Studio 功能

本节介绍对话、清单编辑器、详细信息和功能等功能。 可以使用应用自定义自定义自定义功能。

### <a name="conversation"></a>对话

你可以在这里查看在 App Studio [在 App Studio](#card-editor) 将卡片发送到你自己来测试这些卡片在 Teams 中的外观。

### <a name="manifest-editor"></a>清单编辑器

如前文所述，Microsoft Teams 应用包最重要的部分就是其 manifest.json 文件。 此文件必须遵循 [Teams 应用架构](~/resources/schema/manifest-schema.md)，包含可使 Teams 向用户正确呈现应用的元数据。

App Studio 中的"清单编辑器"选项卡简化了清单的创建，可用于描述应用、上传图标、添加应用功能并生成 .zip 文件，可轻松上传到 Teams，以便进行测试或分发供其他人使用。 请注意，App Studio 不会为应用生成功能代码，也不托管应用。 应用必须已在应用上传流程的清单中列出的 URL 上托管并运行，以产生工作应用。

#### <a name="details"></a>详细信息

清单编辑器的详细信息部分定义所创建应用的详细信息。 这包括应用的名称、说明和视觉品牌等内容。 可以自动生成应用程序的 GUID，并提供隐私声明和使用条款的 URL。

#### <a name="capabilities"></a>功能

清单编辑器的功能部分介绍定义应用的功能并列出其中每个功能的详细信息。

> [!NOTE]
> 最佳做法是，你必须提供自定义指南，以便应用用户和客户在自定义应用时遵循这些准则。 有关详细信息，请参阅自定义[应用程序中Microsoft Teams。](/MicrosoftTeams/customize-apps)


##### <a name="tabs"></a>选项卡

* **团队选项卡。** 团队选项卡将成为频道的一部分，可提供对团队信息和资源的快速访问。 例如，频道的"Planner"选项卡包含单个计划;Power BI 选项卡映射到特定报表。 用户可以向下钻取相关上下文，但无法导航到选项卡外部。例如，Power BI 选项卡不会启用到其他 Power BI 报表的导航，但它允许" *转到网站* "按钮，该按钮在 Power BI 主网站中启动报表。

  对于团队选项卡，必须使用 *配置 URL* 显示选项并收集信息，以便用户可以自定义选项卡的内容和体验。当用户首次将选项卡添加到频道时，将显示此 HTML 表格。

  你还必须提供选项卡期望从其加载或链接到的任何其他域。

* **个人选项卡。** 本部分允许你定义一组选项卡，这些选项卡默认在个人应用体验中显示 (用户在团队或频道应用的上下文之外使用你的应用时) 。 在这部分内容中，提供选项卡名称、唯一标识符、指向将在 Teams 中显示的 UI 的 URL，以及用户选择在浏览器中查看选项卡时使用的 URL（可选）。 使用Teams选项卡，提供选项卡预期从其中加载或链接到的其他任何域。

##### <a name="bots"></a>机器人

通过此部分，可以将一 [对话自动](~/bots/what-are-bots.md) 添加到应用中。 如果你已有注册了 Bot Framework 的自动程序，您可以通过单击 *"设置* 并单击自动程序的名称"自动框架 ID"并定义自动程序工作的范围来添加自动程序。

如果你尚未在 Bot Framework 中注册自动 **，请单击"注册** 自动程序"以创建新的自动程序。 完成注册自动程序后，请返回清单编辑器的此部分，输入其名称和 Bot Framework ID。

提供自动程序信息后，你现在可以选择定义自动程序可以建议给用户的命令列表。 添加命令的名称、指示其语法和参数的命令说明以及此命令应应用于的范围。

> [!NOTE]
> 如果已定义自动程序仅支持一个作用域，则忽略为不受支持的范围指定的命令。 你随时都可以编辑你的自动程序支持的范围。

##### <a name="connectors"></a>连接器

此部分允许向应用添加连接器。 如果已注册 Office 365 连接器，请选择" **设置** 并输入连接器的名称和 ID。 如果需要新的连接器，请单击 **注册** 以在浏览器中访问连接器开发人员仪表板。

> [!NOTE]
> 通过应用自定义，管理员可以更改通过机器人、消息传递扩展、选项卡和连接器加载的应用的外观。 例如，如果Teams将 **Contoso** 中的应用程序的名称自定义为 **Contoso 代理**，则应用将显示为用户的新名称 **Contoso Agent。** 但是，向聊天添加连接器时，连接器仍将在列表中显示应用的名称为 **Contoso**。


##### <a name="messaging-extensions"></a>消息扩展

[消息传递扩展](~/messaging-extensions/what-are-messaging-extensions.md) 是一种强大的方法，让用户在 Microsoft Teams 中参与你的应用。 用户可以查询服务的信息，将该信息以卡片形式发布到频道或聊天对话中。

消息扩展由 Bot Framework 自动程序支持，因此它们要求配置自动程序运行。 如果拥有要为消息扩展提供 Power 的自动程序的名称和 Bot Framework ID，请输入该 ID。 否则，请单击 **注册** 创建一个，然后输入信息。 选择用户是否可以更新消息扩展的配置。

配置基础自动程序后，定义邮件扩展可以接受的命令和参数。

每个命令都需要标题和 ID。 命令可以选择性地包含用户说明。 每个命令可支持最多五个参数，每个参数要求：

* 显示在客户端和用户请求Teams参数的名称。
* 用户友好标题。
* 可选说明。

> [!NOTE]
> 若要使用 app studio 创建消息传递扩展，请参阅 [使用 app studio 创建消息传递扩展](~/resources/create-messaging-extension-using-appstudio.md)。

#### <a name="test-and-distribute"></a>测试和分发

定义完应用程序后，"测试并分发"部分可导出应用定义为压缩文件，然后可将其共享并上传到 Teams 客户端进行测试。 单击"导出"以 *appname.zip* 下载默认下载目录中的 zip 文件。

##### <a name="publish-your-app-to-teams"></a>将应用发布到 Teams
在项目主页上，你可以将应用上载到团队、将应用提交到公司自定义应用商店供你组织的用户使用，或将应用提交到所有 Teams 用户的应用源。 IT 管理员将审阅这些提交。 可返回" *发布* 页面，检查提交状态，并了解应用是否已获 IT 管理员批准或拒绝。这也是提交应用更新或取消当前任何活动提交的地方。

### <a name="card-editor"></a>卡片编辑器

卡片是包含短信息或相关信息的容器。 Microsoft Teams 支持卡片，卡片可以有多个属性和附件。 卡片是自动程序和连接器将可操作的信息中继给用户的一种重要方式。 

为了简化此过程且减少出错，可以使用"卡片编辑器"选项卡使用窗体生成主卡或缩略图卡，并验证和测试生成的卡片 (就像用户通过自动程序) 看到它一样。 它还为卡片提供相应的 JSON 或 Node.js 代码，可将其复制/粘贴到 C# 应用的源代码中。

如果已有要验证的卡片，可在 Teams 中将该卡的 JSON 粘贴到 *"添加卡信息"下的 JSON 选项卡中* 然后将其发送给自己以查看聊天中的外观。

### <a name="react-control-library"></a>反应控件库

>[!Note]
> 以后React弃用此控件库。 请考虑将 [Fluent-UI react 控件用作](https://microsoft.github.io/fluent-ui-react/) 以前作为 Stardust UI 的替代项。

创建遵循 Teams 最佳做法的应用是使应用的外观与 Teams 客户端体验完美契合的一种好方法。 你使用的 UI 控件对于实现这一目标至关重要。 为更轻松地创建一致的 UI，App Studio 提供了几种符合 Teams 设计原则的 UI 控件类别。

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
