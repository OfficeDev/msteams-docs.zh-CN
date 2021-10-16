---
title: Microsoft Teams 商店验证指南
description: 介绍了每个提交给团队商店 (AppSource) 的应用程序必须遵循的准则。
author: heath-hamilton
ms.author: surbhigupta
ms.topic: reference
ms.localizationpriority: high
ms.openlocfilehash: e54581a809cd72257ad7c285f9c36acc0691f922
ms.sourcegitcommit: ece03efbb0e9d1fea5bd01c9c05a2bc232c1a1c3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2021
ms.locfileid: "60378896"
---
# <a name="microsoft-teams-store-validation-guidelines"></a>Microsoft Teams 商店验证指南

遵循这些准则会增加应用通过 Microsoft Teams 应用商店提交程序的可能性。 这些特定于 Teams 的准则是对 Microsoft [商业市场认证策略](/legal/marketplace/certification-policies) 的补充，并经常更新以反映新功能、用户反馈和业务规则更改。

> [!NOTE]
> 某些准则可能不适用于你的应用。 例如，如果应用不包含机器人，则可以忽略与机器人相关的准则。

## <a name="value-proposition"></a>价值主张

### <a name="app-name"></a>应用名称

应用名称在用户在应用商店中发现它的方式中起着至关重要的作用。请记住有关应用名称的以下几点:

* 该名称必须包括与用户相关的术语。
* Teams 核心功能的名称&#8212;例如 **聊天**、 **联系人**、 **日历**、 **呼叫**、 **文件**、 **活动**、 **Teams**、**应用** 和 **帮助**&#8212;不应包含在应用程序名称中。
* 公用名词必须以开发人员名称为前缀或后缀 (例如，**Contoso Tasks** 而不是 **任务**)。
* 不得使用 **Teams** 或其他 Microsoft 产品的名称，以免错误地表明联合品牌或联合销售。 (关于引用 Microsoft 软件、产品和服务的更多信息，请参阅 [Microsoft 商标和品牌指南](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general))。
* 如果应用程序是与 Microsoft 官方合作的一部分，则应用程序的名称必须放在前面 (例如，**适用于 Microsoft Teams 的 Contoso 连接器**)。
* 不得复制商店中列出的应用程序的名称或商业市场中的其他报价。
* 不得包含亵渎或贬损性的词汇。 该名称也不得包括对种族或文化不敏感的语言。
* 必须是唯一的。例如，不能为不同地区列出具有相同名称和功能的多个应用程序。

### <a name="suitable-for-workplace-consumption"></a>适用于工作区使用

应用程序内容必须适合一般工作场所消费，并遵守商业市场认证策略中所列出的所有限制。 禁止与宗教、政治、赌博和长时间娱乐相关的内容。 有关详细信息，请参阅 [商业市场认证策略](/legal/marketplace/certification-policies#10010-inappropriate-content)。

应用必须促进组协作、提高个人的工作效率，或者两者兼而有之。 用于团队联系和社交的应用必须是协作的，并且专为多个参与者设计。 这些类型的应用也不应需要大量时间投入或感知来影响工作效率。

### <a name="similar-platforms-and-services"></a>类似的平台和服务

应用必须以 Teams 体验为主，不包含其他基于聊天的类似协作平台或服务的名称、图标或图像，但应用提供特定互操作性时除外。

### <a name="feature-names"></a>功能名称

按钮和其他 UI 文本中的应用功能名称不得与为 Teams 和其他 Microsoft 产品保留的术语相冲突。 例如，**开始会议**、**拨打电话** 或 **开始聊天**。 如果无法完全避免此问题，请包括应用名称，例如 **启动 Contoso 会议** 而不是 **启动会议**。

## <a name="security"></a>安全性

### <a name="microsoft-365-app-compliance-program"></a>Microsoft 365 应用合规性

[Microsoft 365 应用合规性计划](/microsoft-365-app-certification/overview) 旨在帮助企业通过评估应用程序的安全和合规性信息来评估和管理风险。 如果要向 Teams 商店发布一个应用程序，则必须完成该程序的以下几层:

* [发布者验证](/azure/active-directory/develop/publisher-verification-overview): 可帮助管理员和终端用户了解到应用开发人员与 Microsoft 标识平台集成的真实性。 完成后，Azure Active Directory (Azure AD) 许可对话框和其他屏幕上会显示蓝色的“已验证”徽章。 有关详细信息，请参阅 [常见问题解答](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)，[如何将应用标记为发布者验证](/azure/active-directory/develop/mark-app-as-publisher-verified)，以及 [排除发布者验证的故障](/azure/active-directory/develop/troubleshoot-publisher-verification)。
* [发布者证明](/microsoft-365-app-certification/docs/attestation): 共享常规、数据处理以及安全性和合规性信息的过程，以帮助潜在客户在使用应用时做出明智的决定。

> [!NOTE]
> 如果之前未列出所提交的应用，则在应用进入 Teams 商店之前，无法正式完成发布者证明。 如果正在更新列出的应用，请在提交最新版本的应用之前完成发布者证明。

### <a name="bots"></a>机器人

对于使用 Microsoft Azure 机器人服务的应用 (如机器人和消息传递扩展)， 则必须遵循 Microsoft [在线服务条款](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46) 中定义的所有要求。

机器人必须始终请求上传文件的权限，并在文件上传后显示确认消息。

### <a name="external-domains"></a>外部域

在大多数情况下，不得在应用的域配置中包含组织控制之外的域 (包括通配符) 和隧道服务。以下的例外情况包括:

* 如果应用使用 Azure 机器人服务的 OAuthCard，则必须将 `token.botframework.com` 作为有效的域包含在内，否则 **登录** 按钮将无法工作。
* 如果应用依赖于 SharePoint，则可以使用 `{teamSiteDomain}` 上下文属性将关联的根 SharePoint 站点作为有效域包含。

### <a name="authentication"></a>身份验证

有关如何实现应用身份验证的信息，请参阅 [Teams 中的身份验证](~/concepts/authentication/authentication.md)。

#### <a name="authenticating-with-external-services"></a>与外部服务进行身份验证

如果应用使用外部服务对用户进行身份验证，请记住以下内容。

* **登录、注销和注册体验**:
  * 依赖于外部帐户或服务的应用必须提供清晰而简单的登录、注销和注册体验。
  * 当用户注销时，他们必须仅从应用中注销并保持登录到 Teams。
* **内容共享体验**：需要通过外部服务进行身份验证以便在 Teams 频道中共享内容的应用，必须在帮助文档 (或类似位置) 中清楚地说明用户如何断开连接或取消共享内容 (如果外部服务支持此功能)。这不意味着取消内容共享的功能必须在你的 Teams 应用中。

#### <a name="government-community-cloud-listings"></a>政府社区云列表

若要向政府社区云 (GCC) 用户分发你的应用，同时避免在 Teams 商店中的重复列表，则身份认证过程必须识别并将用户引向 GCC 专用或预期的 URL。

### <a name="sensitive-content"></a>敏感内容

应用不得发布敏感数据，如信用卡或金融支付工具数据。 该应用也不得向无意查看该内容的受众显示健康、联系人追踪或其他个人身份信息 (PII)。

在应用下载任何文件或可执行文件 (.exe) 到用户的机器或环境中之前向用户发出警告。

### <a name="financial-information"></a>财务信息

应用不得要求用户在 Teams 界面内进行支付。 财务工具详细信息不得通过机器人界面传输给用户。

只有在用户同意使用该应用之前，在使用条款、隐私策略或任何配置文件页面或网站中进行了适当的披露时，才可以链接到安全的外部支付服务。

在 iOS 或 Android 版本的 Teams 上运行的应用必须遵循以下准则:

* 应用不得包括应用内购买、试用优惠或旨在追加销售支付版本的 UI，或指向用户可以购买或获取其他内容、应用程序或插件的在线商店的链接。
* 如果应用需要帐户，则用户必须能够免费注册帐户。 禁止使用 **免费** 或 **免费帐户** 的术语。
* 可以决定账户是无限期的还是有限期的，但若账户过期，则可能无法显示表明需要支付的用户界面、文字或链接。
* 应用的隐私策略和使用条款页面必须不含任何与商业相关的 UI 或链接。

> [!NOTE]
> Teams 应用商店一览可以包括可供购买的应用订阅计划或许可证。 有关详细信息，请参阅[为你的用户添加 SaaS 产品/服务](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)。

## <a name="general-functionality-and-performance"></a>常规功能和性能

### <a name="launching-external-functionality"></a>正在启动外部功能

应用不得将用户带出 Teams 的核心用户场景。 应用内容和交互可以在 Teams 的功能中发生，如机器人、卡片和任务模块。

应将用户链接到 Teams 中的某个位置，而不是链接到外部网站或应用。 对于需要外部功能的方案，应用必须具有显式用户权限才能启动该功能。

### <a name="compatibility"></a>兼容性

应用必须能够在以下操作系统和浏览器上正常运行:

* Microsoft Windows 7 及更高版本
* macOS 10.10 及更高版本
* Microsoft Edge 12 及更高版本
* Mozilla Firefox 47.0 及更高版本
* Google Chrome 51.0 及更高版本
* iOS 9.0 及更高版本
* Android 4.4 及更高版本

### <a name="response-time"></a>答复时间

Teams 应用必须在合理的时间范围内做出响应，具体取决于功能。

* 选项卡必须在三秒内响应，或显示加载消息或警告。
* 机器人必须在两秒内响应用户命令或显示键入指示器。
* 消息传递扩展必须在五秒内响应用户命令。
* 通知必须在用户操作后的五秒内显示。

## <a name="app-package-and-store-listing"></a>应用包和应用商店列表

必须正确设置应用包的格式，并包含所有必需的信息和组件。

### <a name="app-manifest"></a>应用部件清单

Teams 应用清单定义应用的配置。

* 清单必须符合最新的清单架构。 相关信息，请参阅 [清单参考](~/resources/schema/manifest-schema.md)。
* 如果应用包括机器人或消息传递扩展，则清单必须与机器人框架元数据保持一致，包括机器人名称、徽标、隐私策略链接和服务条款链接。
* 如果应用使用 Azure Active Directory (Azure AD) 进行身份验证，请在清单中包含Azure AD应用程序 (客户端) ID。有关更多信息，请参阅[清单引用](~/resources/schema/manifest-schema.md#webapplicationinfo)。

### <a name="app-icons"></a>应用图标

图标是用户在浏览 Teams 应用商店时看到的主要元素之一。 图标应传达应用的品牌和用途，同时遵循以下要求:

* 应用包必须包含两个 PNG 版本的应用图标: 彩色图标和大纲图标。
* 图标的彩色版本在大多数 Teams 方案中显示，必须为 192x192 像素。 图标符号 (96x96 像素) 可以是任何颜色，但它必须位于纯色或完全透明的方形背景上。
* 当应用正在使用，并“悬挂”在 Teams 左侧的应用程序栏上时，以及当用户钉住应用的消息扩展时，则图标的轮廓版本会显示出来。 它必须是 32x32 像素，可以是带有透明背景的白色或带有白色背景的透明 (不允许有其他颜色)。 图标周围不应该有任何额外的填充。
* 应用包中必须包含正确尺寸和格式的图标。 图标也必须与所提交的商店清单元数据相匹配。

有关详细信息、最佳做法和示例，请参阅 Teams 应用 [图标指南](~/concepts/build-and-test/apps-package.md#app-icons)。

### <a name="app-descriptions"></a>应用说明

必须对应用有一个简短而长的介绍。 应用配置和合作伙伴中心中的说明必须相同。

描述不应直接或通过影射贬低其他品牌 (Microsoft 拥有的或其他的)。 请确保说明不包含无法实例化的声明 (例如，“保证效率提高 200%”)。

#### <a name="short-description"></a>简短说明

简短说明是应用的简要摘要，突出显示其价值主张，并面向目标受众。

**应做:**

* 将简短说明保留为一句话。
* 首先放置最重要的信息。
* 包括客户可能搜索的关键字。

**不应做:**

* 重复应用名称。
* 在简短说明中使用 **应用** 一词。

#### <a name="long-description"></a>较长说明

长描述可以提供具有吸引力的叙述，突出显示应用的价值主张、主要受众和目标行业。 虽然此说明可以长达 4，000 个字符，但大多数用户仅会阅读 300-500 个字。

**应做:**

* 使用 [Markdown](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) 设置说明的格式。
* 使用主动语音并直接与用户交谈。 例如，*可以...*。
* 列出带项目符号点的功能，以便更轻松地扫描说明。
* 在用户安装应用之前，清楚地描述列表和相关材料中所述的功能、特点和可交付结果的限制、条件或例外情况。 应用支持的 Teams 功能必须与列表描述的核心函数相关。
* 请确保应用说明与 Teams 应用内的功能相匹配。 对 Teams 应用外部工作流的任何引用都必须受到限制，并且必须从 Teams 应用功能中明确调用。
* 包括帮助或支持链接。
* 请参阅 **Microsoft 365**，而不是 **Office 365**。
* 如果需要引用 **Teams**，请将第一个引用写为 **Microsoft Teams**。 后续引用可以缩短为 **Teams**。
* 在描述应用如何与 Teams (或 Microsoft 365) 配合使用时，请使用以下语言:
  * “... 与 Microsoft Teams 一同工作。”
  * “... 正在与 Microsoft Teams 一同工作。”
  * “... 在 Microsoft Teams 内。”
  * “... 适用于 Microsoft Teams。”
  * “... 与 Microsoft Teams 集成。”
  * “...专为...而建”
  * “ ...专为...而开发”
  * “ ...专为...而设计”


**不应做:**

* 超过 500 字。
* 将 **Microsoft** 缩写为 **MS** 或 **MSFT**。
* 指示应用是来自 Microsoft 的产品/服务，包括使用 Microsoft 的标语或标志行。
* 使用未拥有的受版权保护的品牌名称。
 * 除非你是经认证的 Microsoft 合作伙伴，否则请使用以下语言:
  * “ ...认证为 ...”
  * “... 由 ... 驱动”
* 包括拼写错误、语法错误和不必要的大写，例如，**Users** 而不是 **users**。
* 包括指向 AppSource 的链接。
* 提出未经核实的主张 (例如: 最佳、顶级、排名)，除非附有声明的来源。
* 将产品/服务与其他市场产品/服务进行比较。



### <a name="screenshots"></a>屏幕截图

屏幕截图提供了应用的突出视觉预览，以补充应用名称、图标和说明。请记住关于屏幕截图的以下几点:

* 每个列表最多可以有五个屏幕截图。
* 支持的文件类型包括 PNG、JPEG 和 GIF。
* 尺寸应为 1366x768 像素。
* 最大尺寸为 1，024 KB。

**应做:**

* 专注于应用的功能 (例如，用户如何与机器人沟通)。
* 包括能准确代表应用程序的内容。
* 谨慎使用文本。
* 请使用带有反映品牌和包含营销内容的颜色框住屏幕截图，类似于 [Freshdesk 列表](https://appsource.microsoft.com/product/office/WA104381505?src=office&tab=Overview) 示例 (尺寸要求适用于整个图像，而不仅仅是屏幕截图)。

**不应做:**

* 显示特定设备，例如手机或笔记本电脑。
* 显示不在应用中的部件版式或 UI。
* 在屏幕截图中捕获任何 Teams 或浏览器 UI。
* 包括不准确反映应用实际 UI 模型，例如显示应用在 Teams 外部使用。

> [!TIP]
> 视频可以是传达人们为什么应使用该应用的最有效方法。 视频也是用户在列表中第一个看到的内容 (默认情况下，视频显示在屏幕截图之前)。 有关详细信息，请参阅 [创建商店列表视频](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#create-a-video)。

### <a name="privacy-policy"></a>隐私策略

隐私策略可以特定于 Teams 应用或所有服务的整体策略。

* 如果使用通用隐私策略模板，则必须引用 **服务**、 **应用程序** 和 **平台**，以包括 Teams 应用和服务或网站。
* 必须包括处理用户数据存储、保留和删除的方式。 还必须描述用于数据保护的安全控件。
* 必须包含联系人信息。
* 不应包含已损坏或用于 beta 版或暂存目的的 URL。
* 不得包含指向 AppSource 的链接。

### <a name="terms-of-use"></a>使用条款

使用条款应特定且适用于产品/服务。

### <a name="support-links"></a>支持链接

应用的支持 URL 不应要求身份验证。 例如，用户不必登录即可与你联系。

### <a name="localization"></a>本地化

如果应用支持本地化，则应用包必须包含基于 Teams 语言设置显示的语言翻译文件。 该文件必须符合 Teams 本地化架构。 有关详细信息，请参阅 [Teams 本地化架构](~/concepts/build-and-test/apps-localization.md)。

## <a name="tabs"></a>选项卡

如果应用包含选项卡，请确保它遵守这些准则。

> [!TIP]
> 有关创建高质量应用体验的信息，请参阅 [Teams 选项卡设计指南](~/tabs/design/tabs.md)。

### <a name="setup"></a>安装

* 选项卡设置不得终止新用户。 提供有关如何完成操作或工作流的信息。
* 身份验证应在选项卡设置期间而不是之后进行。

### <a name="views"></a>视图

* 登录屏幕区域不得使用大型徽标或显示整个网页。
* 可以通过跨多个选项卡将其分解来简化内容。
* 选项卡不应有重复的标题。从 iframe 中删除徽标，因为选项卡框架已显示应用图标和名称。

### <a name="navigation"></a>导航

* 选项卡不得有超过三级的导航。
* 选项卡不得提供与主要 Teams 导航冲突的导航。
* 选项卡中的第二级页和第三级页必须在主选项卡区域的第二级别和第三级别视图中打开，该视图通过痕迹导航或左侧导航进行导航。也可以包括以下组件来帮助选项卡导航:
    * 后退按钮
    * 页眉
    * 汉堡菜单
* 选项卡不应有水平滚动。
* 选项卡中的深层链接不能链接到外部网页，而应链接到 Teams 内部的某个位置。例如，任务模块或其他标签。
* 选项卡不应允许用户在 Teams 外部导航以获得核心应用体验。

### <a name="usability"></a>可用性

* 选项卡必须提供价值，而不仅仅是托管现有网站。
* 用户必须能够撤消其在选项卡中的最后一个操作。
* 个人上下文中的选项卡可以从应用的共享实例中聚合内容。
* 选项卡必须响应 Teams 主题。 当用户更改主题时，应用的主题必须反映所选内容。
* 选项卡必须尽可能使用 Teams 样式的组件，如 Teams 字体、类型渐变、调色板、网格系统、动作、语音音调等。
* 如果应用功能需要更改设置，请包括 **设置** 选项卡。
* 选项卡必须遵循 Teams 交互设计，例如页面内导航、对话的位置和使用、信息层次结构等 (在任何有可能的情况下)。
* iframe 中的选项卡内容不得包含模拟 Teams 核心功能的功能。 例如，机器人、消息传递扩展、呼叫、会议等。

> [!TIP]
>
> * 将个人机器人与个人选项卡一起包含在一起。
> * 允许用户从其个人选项卡中共享内容。

## <a name="bots"></a>机器人

如果应用包含机器人，请确保它遵守这些准则。

> [!TIP]
> 有关创建高质量应用体验的信息，请参阅 [Teams 机器人设计指南](~/bots/design/bots.md)。

### <a name="bot-commands"></a>机器人命令

很难分析用户输入和预测用户意图。机器人命令为用户提供机器人理解的单词或短语，以便他们 (和机器人) 不必猜测用户意图。

* 强烈建议在应用配置中列出支持的机器人命令。 当用户尝试向机器人发送消息时，这些命令将显示在撰写框中。
* 机器人支持的所有命令都必须正常工作，包括 **Hi**、 **Hello** 和 **帮助** 命令。

> [!TIP]
> 对于个人机器人，请包括一个 **帮助** 选项卡，进一步描述机器人可以执行的操作。

### <a name="bot-welcome-messages"></a>机器人欢迎消息

* 机器人在首次运行时几乎都应该发送欢迎信息。 为了获得最佳体验，该消息应包括机器人的价值主张、如何配置机器人以及简要描述所有受支持的机器人命令。 可以使用带按钮的自适应卡片显示消息，以提高可用性。 有关详细信息，请参阅 [如何触发机器人欢迎消息](~/bots/how-to/conversations/send-proactive-messages.md)。
* 首次运行期间，频道和聊天中的机器人欢迎消息是可选的，尤其是在机器人可供个人使用并执行类似操作时。 如果机器人确实已发送欢迎消息，则它不得单独向用户发送这些消息 (这被视为 [垃圾邮件](#bot-message-spamming))。 该消息还应提及添加机器人的人员。
* 仅发送通知的机器人必须发送欢迎消息，表示其不会回复用户的消息。

> [!TIP]
> 在向单个用户发送的欢迎消息中，传送教程可以提供机器人和任何其他应用功能的有效概述。 鼓励包括允许用户尝试自动命令的按钮。 例如，**创建任务**。

### <a name="bot-message-spamming"></a>机器人邮件垃圾邮件

机器人不得通过在短时间内连续发送多条邮件来向用户发送垃圾邮件。

* **频道和聊天中的机器人邮件**: 请勿通过创建单独的帖子向用户发送垃圾邮件。 创建单一的帖子，并在同一线程中进行回复。
* **个人应用中的机器人消息**: 请勿快速连续发送多条消息。 发送一条包含完整信息的消息。 避免为完成一个工作流程而进行多轮对话。 相反，请考虑使用窗体 (或任务模块) 一次收集性用户的所有输入。
* **欢迎消息**: 不允许定期重复相同的欢迎消息，并将其视为垃圾邮件。 例如，将新成员添加到团队时，不要向其他成员发送显示为欢迎消息的垃圾邮件。 改为向新成员发送消息。

### <a name="bot-notifications"></a>机器人通知

机器人通知必须包含与你为机器人 (团队、聊天或个人) 定义的范围相关的内容。

### <a name="bots-and-adaptive-cards"></a>机器人和自适应卡片

自适应卡片是强烈建议显示机器人消息的方法。 卡片必须是轻型的，且仅包含 1-3 个操作。 如果需要显示更多内容，请考虑使用任务模块或选项卡。

有关详细信息，请参阅下列资源:

* [设计自适应卡片](~/task-modules-and-cards/cards/design-effective-cards.md)
* [卡参考](~/task-modules-and-cards/cards/cards-reference.md#types-of-cards)

## <a name="messaging-extensions"></a>消息扩展

如果应用包含消息传递扩展，请确保它遵守这些准则。

> [!TIP]
> 有关创建高质量应用体验的信息，请参阅 [Teams 信息传递扩展设计指南](~/messaging-extensions/design/messaging-extension-design.md)。

### <a name="action-commands"></a>操作命令

基于操作的消息传递扩展应执行以下操作:

* 允许用户在不完成中间步骤 (例如登录) 的情况下触发对邮件的操作。
* 将消息上下文传递到下一个工作状态。

### <a name="preview-links-link-unfurling"></a>预览链接 (链接展开)

消息传递扩展应在 Teams 撰写框中预览已识别的链接。 不要添加不受控制的域 (无论是绝对 URL 或通配符)。 例如，`yourapp.onmicrosoft.com` 有效，但 `*.onmicrosoft.com` 无效。 也禁止使用顶级域 (例如，`*.com` 或 `*.org`)。

### <a name="search-commands"></a>搜索命令

* 基于搜索的消息传递扩展插件必须提供可帮助用户有效搜索的文本。
* @提及可执行文件必须清晰、易于理解且可读。

## <a name="task-modules"></a>任务模块

任务模块必须包含图标及其关联的应用的短名称。

> [!TIP]
> 有关创建高质量应用体验的信息，请参阅 [Teams 任务模块设计指南](~/task-modules-and-cards/task-modules/design-teams-task-modules.md)。

## <a name="meeting-extensions"></a>会议扩展

如果应用包含会议扩展，请确保它遵守这些准则。

> [!TIP]
> 有关创建高质量应用体验的信息，请参阅 [Teams 会议扩展设计指南](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)。

### <a name="pre--and-post-meeting-experience"></a>会议前和会议后体验

* 会议前和会议后屏幕必须遵循常规选项卡设计准则。 有关详细信息，请参阅 [Teams 设计指南](~/tabs/design/tabs.md)。
* 选项卡不得有水平滚动。
* 显示多个项时，选项卡应具有井然有序的布局。 例如，超过 10 个投票或调查。 请参阅 [示例布局](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#after-a-meeting)。
* 当导出调查或投票的结果时，应用程序必须通知用户，表明“结果成功下载”。

### <a name="in-meeting-experience"></a>会议内体验

* 在会议期间应用必须仅能使用深色主题。 有关详细信息，请参阅 [Teams 设计指南](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#theming)。
* 在会议期间将鼠标悬停在应用图标上时，工具提示应显示应用名称。
* 消息传递扩展在会议期间的功能必须与在会议外部执行的相同。

### <a name="in-meeting-tabs"></a>会议内选项卡

* 必须有反应。请确保保持填充和组件大小。
* 如果有多个导航层，则必须具有后退按钮。
* 不得包含多个取消或关闭按钮。 这可能会使用户感到困惑，因为已有一个内置标题按钮来关闭选项卡。
* 不得有水平滚动。

### <a name="in-meeting-dialogs"></a>会议内对话

* 应谨慎使用并用于轻型和任务导向的方案。
* 必须在单栏中显示内容，而且不能有多个导航层。
* 不得使用任务模块。
* 必须与会议阶段的中心对齐。
* 用户选择按钮或执行操作后，即应将其消除。

## <a name="notifications"></a>通知

如果应用使用 [Microsoft Graph 提供的活动源 API](/graph/teams-send-activityfeednotifications)，请确保它遵循以下准则。

### <a name="general"></a>常规

* 应用配置中指定的所有通知触发器都应在应用中收到通知。
* 通知必须根据为应用配置的支持语言进行本地化。
* 通知必须在用户操作后的五秒内显示。

### <a name="avatars"></a>头像

* 通知头像应与应用的颜色图标匹配。
* 用户触发的通知应包括用户的头像。

### <a name="spamming"></a>垃圾邮件

* 应用每分钟不得向用户发送超过 10 条通知。
* 机器人和活动源不应触发重复通知。
* 通知必须为用户提供一些值，并且不能用于琐碎或不相关的事件。

### <a name="navigation-and-layout"></a>导航和布局

* 通知必须遵循 Teams 活动源布局和体验。
* 选择通知时，用户必须定向到 Teams 中的相关内容，而不会退出 Teams 体验。

## <a name="advertising"></a>广告

应用不得显示广告，包括动态广告、横幅广告和消息中的广告。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [创建合作伙伴中心帐户](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)
