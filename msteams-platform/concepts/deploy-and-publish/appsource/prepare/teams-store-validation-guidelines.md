---
title: Microsoft Teams应用商店验证准则
description: 介绍每个提交到 AppSource 应用商店Teams应用 (必须遵循) 准则。
author: heath-hamilton
ms.author: surbhigupta
ms.topic: reference
ms.localizationpriority: none
ms.openlocfilehash: 43cd037eb6f14dee4ee58cd34b1db834478ae3f5
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155269"
---
# <a name="microsoft-teams-store-validation-guidelines"></a>Microsoft Teams应用商店验证准则

遵循这些指南会增加你的应用通过应用商店Microsoft Teams提交过程的可能性。 这些Teams准则[补充了](/legal/marketplace/certification-policies)Microsoft 商业市场认证策略，并经常进行更新以反映新功能、用户反馈和业务规则更改。

> [!NOTE]
> 某些指南可能不适用于你的应用。 例如，如果你的应用不包括自动程序，你可以忽略与机器人相关的指南。

## <a name="value-proposition"></a>价值主张

### <a name="app-name"></a>应用名称

应用名称在用户如何在应用商店中发现它中扮演关键角色。 对于应用名称，请记住以下事项：

* 该名称必须包含与用户相关的术语。
* 核心 Teams 功能的名称&#8212;如聊天、联系人、日历、呼叫、**文件**、活动 **、Teams、** 应用和帮助 **&#8212;不应** 包含在你的应用名称中。  
* 常用名词必须以开发人员的姓名作为前缀或后缀 (例如 **，Contoso Tasks** 而不是 **Tasks**) 。
* 不得使用 **Teams** 或可能错误地表示共同品牌或共同销售的其他 Microsoft 产品名称。  (有关引用 Microsoft 软件、产品和服务的信息，请参阅 [Microsoft 商标和](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general) 品牌) 。
* 如果你的应用是与 Microsoft 官方合作关系的一部分，则应用名称必须先 (例如 **Contoso Connector for Microsoft Teams**) 。
* 不得复制应用商店中列出的应用名称或商业市场的其他产品/服务。
* 不得包含冒犯性或冒犯性术语。 该名称不得包含种族或文化不敏感的语言。
* 必须是唯一的。 例如，你不能为同一名称和功能不同的区域列出多个应用。

### <a name="suitable-for-workplace-consumption"></a>适合工作场所使用

应用内容必须适用于常规工作场所使用，并遵守商业市场认证策略中列出的所有限制。 禁止与政治、时政、娱乐和长期娱乐相关的内容。 有关详细信息，请参阅商业 [市场认证策略](/legal/marketplace/certification-policies#10010-inappropriate-content)。

你的应用必须促进组协作、提高个人的工作效率或同时提高这两者。 用于团队绑定和社交的应用必须协作且专为多个参与者设计。 这些类型的应用也不应要求大量时间投资或对工作效率产生明显影响。

### <a name="similar-platforms-and-services"></a>类似的平台和服务

应用必须专注于Teams体验，不包括其他类似的基于聊天的协作平台或服务的名称、图标或图像，除非你的应用提供特定的互操作性。

### <a name="feature-names"></a>功能名称

按钮和其他 UI 文本中的应用功能名称不得与为 microsoft Teams和其他 Microsoft 产品保留的术语冲突。 例如，"**开始会议****"、"呼叫"** 或"**开始聊天"。** 如果无法完全避免这种情况，请包含你的应用名称，例如"开始 **Contoso 会议**"，而不是"**开始会议"。**

## <a name="security"></a>安全性

### <a name="microsoft-365-app-compliance-program"></a>Microsoft 365 应用合规计划

应用[Microsoft 365计划](/microsoft-365-app-certification/overview)旨在帮助组织通过评估应用的安全性和合规性信息来评估和管理风险。 如果要将应用发布到应用商店Teams应用商店，则必须完成程序的以下层：

* [Publisher验证](/azure/active-directory/develop/publisher-verification-overview)：帮助管理员和最终用户了解与应用程序开发人员集成的应用程序开发人员Microsoft 标识平台。 完成后，Azure AD 对话框和其他屏幕上将显示蓝色Azure Active Directory (") "锁屏提醒。 有关详细信息，请参阅 [常见问题](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)、 [如何将](/azure/active-directory/develop/mark-app-as-publisher-verified)你的应用标记为发布者验证和发布者 [验证疑难解答](/azure/active-directory/develop/troubleshoot-publisher-verification)。
* [Publisher证明](/microsoft-365-app-certification/docs/attestation)：一个共享常规、数据处理以及安全性和合规性信息以帮助潜在客户做出有关使用你的应用的明智决定的过程。

> [!NOTE]
> 如果你要提交之前未列出的应用，则你无法正式完成 Publisher 证明，直到你的应用位于 Teams 应用商店中。 如果要更新列出的应用，请Publisher应用最新版本之前填写证明。

### <a name="bots"></a>机器人

对于使用 Microsoft Azure Bot Service (（如机器人和消息传递扩展) ）的应用，必须遵循 Microsoft Online Services 条款中定义[的所有要求](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46)。

自动程序必须始终请求上传文件的权限，在文件上载后显示确认消息。

### <a name="external-domains"></a>外部域

在大多数情况下，不得将组织控制权限之外的域 (包括通配符) 和应用的域配置中的隧道服务。 以下例外包括：

* 如果你的应用使用 Azure Bot Service 的 OAuthCard，则必须包含为有效的域，否则"登录 `token.botframework.com` "按钮将不起作用。 
* 如果你的应用依赖于SharePoint，可以使用 context 属性将关联的根SharePoint网站作为有效 `{teamSiteDomain}` 域。

### <a name="authentication"></a>身份验证

若要了解如何实现应用身份验证，请参阅 Teams 中的[身份验证](~/concepts/authentication/authentication.md)。

#### <a name="authenticating-with-external-services"></a>使用外部服务进行身份验证

如果你的应用使用外部服务对用户进行身份验证，请记住以下事项。

* **登录、注销和注册体验**：
  * 依赖于外部帐户或服务的应用必须提供清晰而简单的登录、注销和注册体验。
  * 当用户注销时，他们只能从应用注销，并仍登录到Teams。
* 内容共享体验：需要与外部服务进行身份验证以在 Teams 通道中共享内容的应用必须在帮助文档 (或类似资源) 如果外部服务支持该功能，则必须清楚地说明如何断开或取消共享内容。 这并不意味着取消共享内容的能力必须存在于你的Teams应用中。

#### <a name="government-community-cloud-listings"></a>政府社区云列表

若要将应用分发给政府社区云 (GCC) 用户，同时避免在 Teams 商店中出现重复列表，身份验证过程必须标识用户并将其路由到GCC URL 或预期 URL。

### <a name="sensitive-content"></a>敏感内容

你的应用不得发布敏感数据，例如信用卡或财务付款方式数据。 应用程序还不得向不适合查看该内容 (访问群体) 运行状况、联系人跟踪或其他个人身份信息。

在应用将任何文件或可执行文件下载到 (.exe) 计算机或环境中之前警告用户。

### <a name="financial-information"></a>财务信息

应用不得要求用户在 Teams 界面中付款。 不得通过自动程序界面将财务资料传送给用户。

只有在用户同意使用应用之前，在使用条款、隐私策略或任何配置文件页或网站中进行了适当的披露，才能链接到安全的外部付款服务。

在 iOS 或 Android 版本上运行Teams必须遵守以下准则：

* 应用不得包括旨在向上销售付费版本的应用内购买、试用产品/服务或 UI，或指向在线商店（用户可以购买或获取其他内容、应用或外接程序）的链接。
* 如果你的应用需要帐户，用户必须能够免费注册帐户。 禁止使用"免费 **"或****"免费帐户**"一词。
* 你可以确定帐户是无限期处于活动状态还是有限时间处于活动状态，但如果帐户过期，则可能不会显示任何指示需要付款的 UI、文本或链接。
* 您的应用程序的隐私策略和使用条款页面不得包含任何与商业相关的 UI 或链接。

## <a name="general-functionality-and-performance"></a>常规功能和性能

### <a name="launching-external-functionality"></a>启动外部功能

应用不得使用户无法Teams核心用户方案。 应用内容和交互可以在Teams（如机器人、卡片和任务模块）内发生。

您应将用户链接到 Teams，而不是外部站点或应用。 对于需要外部功能的方案，你的应用必须具有启动该功能的显式用户权限。

### <a name="compatibility"></a>兼容性

应用必须在以下操作系统和浏览器中完全正常工作：

* Microsoft Windows 7 及更高版本
* macOS 10.10 及更高版本
* Microsoft Edge 12 及更高版本
* Mozilla Firefox 47.0 及更高版本
* Google Chrome 51.0 及更高版本
* iOS 9.0 及更高版本
* Android 4.4 及更高版本

### <a name="response-time"></a>响应时间

Teams应用必须在合理的时间范围内做出响应，这因功能而异。

* 选项卡必须在三秒钟内做出响应，或者显示加载的消息或警告。
* 机器人必须在两秒钟内响应用户命令或显示键入指示器。
* 消息扩展必须在五秒钟内响应用户命令。
* 通知必须在用户操作五秒钟内显示。

## <a name="app-package-and-store-listing"></a>应用包和应用商店一览

应用包的格式必须正确，并且必须包括所有必需的信息和组件。

### <a name="app-manifest"></a>应用部件清单

应用Teams清单定义应用配置。

* 清单必须符合最新的清单架构。 有关信息，请参阅 [清单参考](~/resources/schema/manifest-schema.md)。
* 如果你的应用包含自动程序或消息传递扩展，则清单必须与 Bot Framework 元数据（包括自动程序名称、徽标、隐私策略链接和服务条款链接）一致。
* 如果你的应用使用 Azure Active Directory (Azure AD) 进行身份验证，在清单中包括 Azure AD 应用程序 (客户端) ID。 有关详细信息，请参阅清单 [参考](~/resources/schema/manifest-schema.md#webapplicationinfo)。

### <a name="app-icons"></a>应用图标

图标是用户浏览应用商店时看到的主要Teams之一。 图标应传达应用的品牌和用途，同时遵循以下要求：

* 应用包必须包含两个 PNG 版本的应用图标：颜色图标和大纲图标。
* 图标的颜色版本在大多数情况下都Teams，并且必须为 192x192 像素。 图标符号 (96x96 像素) 可以是任何颜色，但它必须位于纯色或完全透明的方形背景上。
* 图标的大纲版本在应用使用和在 Teams 左侧的应用栏上显示"弯曲"时，以及当用户固定应用的消息扩展时。 它必须是 32x32 像素，并且可以是白色（背景透明）或透明（白色背景 (不允许使用任何其他颜色) 。 图标不应在符号周围有任何额外的填充。
* 应用包中必须包含大小正确和格式正确的图标。 图标还必须与使用应用商店一览元数据提交内容匹配。

有关详细信息、最佳做法和示例，请参阅应用Teams[指南](~/concepts/build-and-test/apps-package.md#app-icons)。

### <a name="app-descriptions"></a>应用说明

必须对你的应用进行简短而详细的说明。 应用配置和合作伙伴中心中的说明必须相同。

说明不应直接或通过输入来说明 Microsoft 拥有 (品牌或其他) 。 确保你的说明不包含无法被 (例如，"保证效率提高 200%") 。

#### <a name="short-description"></a>简短说明

简短说明是应用的简要摘要，突出显示了它的价值主张，并面向目标受众。

**应做：**

* 将简短说明保留为一个句子。
* 首先放置最重要的信息。
* 包括客户可能搜索的关键字。

**不应做：**

* 重复应用名称。
* 使用简短 **说明中的"应用** "一词。

#### <a name="long-description"></a>较长说明

长描述可提供极具吸引力的叙述，重点介绍应用的价值主张、主要受众和目标行业。 虽然此说明可以有 4，000 个字符，但大多数用户只能阅读 300 到 500 个单词。

**应做：**

* 使用 [Markdown](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) 设置说明的格式。
* 使用活动语音并直接与用户通话。 例如， *可以 ...*。
* 列出带项目符号的功能，以便更轻松地扫描说明。
* 在用户安装应用之前，请清楚地描述列表和相关材料中所述的功能、功能和可交付结果的限制、条件或例外。 应用Teams的功能必须与一览描述的核心功能相关。
* 包括帮助或支持链接。
* 请参阅 **Microsoft 365** 而不是 **Office 365**。
* 如果需要引用 Teams **，请** 编写第一个引用作为 **Microsoft Teams**。 后续引用可以缩短为 **Teams**。
* 在描述应用如何与应用或应用Teams (或Microsoft 365) ：
  * "...适用于Microsoft Teams。"
  * "...使用 Microsoft Teams。"
  * "...内部Microsoft Teams。"
  * "...for Microsoft Teams."
  * "...与 Microsoft Teams 集成。"
  * "...专为..."
  * "...针对..."
  * "...专为..."


**不应做：**

* 超过 500 个单词。
* 将 **Microsoft** 缩写为 **MS 或** **MSFT**。
* 指示应用是 Microsoft 提供的产品/服务，包括使用 Microsoft 标志或标签。
* 使用您不拥有的受版权保护的品牌名称。
* 包括拼写错误、语法错误和不必要的大写 (例如 **，Users（** 而不是 **用户** ）) 。
* 包括指向 AppSource 的链接。
* 除非你是经过认证的 Microsoft 合作伙伴，否则请使用以下语言：
  * "...认证..."
  * "...由 ..."

### <a name="screenshots"></a>屏幕截图

Screenshots provide a prominent visual preview of your app to complement your app name， icon， and descriptions. 请记住以下有关屏幕截图：

* 每个列表最多可以有五张屏幕截图。
* 受支持的文件类型包括 PNG、JPEG 和 GIF。
* 尺寸应为 1366x768 像素。
* 最大大小为 1，024 KB。

**应做：**

* 专注于你的应用的功能，例如 (用户如何与自动程序通信) 。
* 包括准确表示你的应用的内容。
* 使用文本时要十分明智。
* 具有反映品牌和包含营销内容的颜色的帧屏幕截图，与 [Freshdesk](https://appsource.microsoft.com/product/office/WA104381505?src=office&tab=Overview) 一览示例类似 (维度要求适用于整个图像，而不只是应用于) 。

**不应做：**

* 显示特定设备，如手机或笔记本电脑。
* 显示不在应用中的部件版式或 UI。
* 捕获Teams中的任意浏览器或浏览器 UI。
* 包括不精确反映应用实际 UI 的模型，例如显示正在应用外部Teams。

> [!TIP]
> 视频可能是传达人们为什么应该使用你的应用的最有效方式。 默认情况下，视频也是用户在一览中看到的第一 (，视频会在屏幕截图显示之前) 。 有关详细信息，请参阅 [为应用商店一览创建视频](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#create-a-video)。

### <a name="privacy-policy"></a>隐私策略

隐私策略可以特定于你的Teams应用，也可以特定于你的所有服务的整体策略。

* 如果使用通用隐私策略模板，则必须引用 **服务**、应用程序和平台，以包括Teams应用和服务或网站。
* 必须包括如何处理用户数据存储、保留和删除。 还必须介绍用于数据保护的安全控件。
* 必须包含您的联系信息。
* 不应包含损坏的 URL 或用于 beta 或暂存目的的 URL。
* 不得包含指向 AppSource 的链接。

### <a name="terms-of-use"></a>使用条款

你的使用条款应特定于你的产品/服务。

### <a name="support-links"></a>支持链接

应用的支持 URL 不应要求身份验证。 例如，用户不应登录来联系您。

### <a name="localization"></a>本地化

如果你的应用支持本地化，你的应用包必须包含一个文件，该文件具有基于语言设置显示Teams翻译。 该文件必须符合本地化Teams。 有关详细信息，请参阅本地化[Teams架构](~/concepts/build-and-test/apps-localization.md)。

## <a name="tabs"></a>选项卡

如果你的应用包含一个选项卡，请确保它遵守这些指南。

> [!TIP]
> 有关创建高质量应用体验的信息，请参阅 Teams[选项卡设计指南](~/tabs/design/tabs.md)。

### <a name="setup"></a>安装

* 选项卡设置不得使新用户死台。 提供有关如何完成操作或工作流的消息。
* 身份验证应在选项卡设置期间而不是之后发生。

### <a name="views"></a>视图

* 登录屏幕区域不得使用大型徽标或显示整个网页。
* 可以通过跨多个选项卡对内容进行分解来简化内容。
* 选项卡不应具有重复的标题。 从 iframe 中删除徽标，因为选项卡框架已显示应用图标和名称。

### <a name="navigation"></a>导航

* 选项卡的导航级别不能超过三个。
* 选项卡不得提供与主导航或主Teams冲突。
* 选项卡中的辅助页面和第三页必须在主选项卡区域（通过痕迹导航或左侧导航导航）的二级和三级视图中打开。 还可以包括以下组件来帮助选项卡导航：
    * 后退按钮
    * 页面页眉
    * 汉堡包菜单
* 选项卡不应具有水平滚动。
* 选项卡中的深层链接不得链接到外部网页，而是链接到Teams。 例如，任务模块或其他选项卡。
* 选项卡不应允许用户在外部导航Teams核心应用体验。

### <a name="usability"></a>可用性

* 选项卡必须提供超越托管现有网站的价值。
* 用户必须能够撤消选项卡中的最后一个操作。
* 个人上下文中的选项卡可以聚合来自应用的共享实例的内容。
* 选项卡必须响应Teams主题。 当用户更改主题时，应用的主题必须反映选择。
* 选项卡必须Teams样式的组件，如Teams字体、字体渐变、调色板、网格系统、动作、语音音调等。
* 必须包含一个 **设置** 选项卡。
* 选项卡必须遵循Teams设计，如页内导航、对话框的位置和使用、信息层次结构等。
* iframe 中的选项卡内容不得包含模拟Teams功能的功能。 例如，机器人、消息传递分机、呼叫、会议等。

> [!TIP]
>
> * 将个人自动程序与个人选项卡一起包含。
> * 允许用户共享其个人选项卡中的内容。

## <a name="bots"></a>机器人

如果你的应用包含自动程序，请确保它遵守这些指南。

> [!TIP]
> 有关创建高质量应用体验的信息，请参阅自动程序Teams[指南](~/bots/design/bots.md)。

### <a name="bot-commands"></a>自动程序命令

分析用户输入和预测用户意图非常困难。 自动程序命令为用户提供了一组机器人可以理解的字词或短语， (自动程序) 也不必猜到。

* 强烈建议在应用配置中列出受支持的自动程序命令。 这些命令在用户尝试向自动程序发送消息时显示在撰写框中。
* 自动程序支持的所有命令必须正常工作，包括 **Hi、Hello** 和 **Help** 命令。

> [!TIP]
> 对于个人机器人 **，包括进** 一步描述机器人可以执行哪些操作的帮助选项卡。

### <a name="bot-welcome-messages"></a>机器人欢迎消息

* 自动程序几乎应始终在首次运行时发送欢迎消息。 为了获得最佳体验，消息应包括自动程序的价值主张、如何配置自动程序，并简要描述所有受支持的自动程序命令。 可以使用带按钮的自适应卡片显示消息，从而提供更好的可用性。 有关详细信息，请参阅 [如何触发机器人欢迎消息](~/bots/how-to/conversations/send-proactive-messages.md)。
* 首次运行时，频道和聊天中的聊天机器人欢迎消息是可选的，尤其是在自动程序可供个人使用并执行类似操作时。 如果自动程序确实发送欢迎邮件，则不得将其分别发送给用户 [ (这被视为](#bot-message-spamming) 垃圾邮件) 。 邮件还应提及添加自动程序的人。
* 仅通知机器人必须发送一条欢迎消息，传达将不会回复用户的消息。

> [!TIP]
> 在向单个用户发送的欢迎消息中，可进行一次环行导览，以有效概览自动程序以及任何其他应用功能。 建议包括允许用户试用自动程序命令的按钮。 例如， **创建任务**。

### <a name="bot-message-spamming"></a>自动程序邮件垃圾邮件

自动程序不得通过短时间连续发送多个邮件来向用户发送垃圾邮件。

* **频道和聊天中的** 聊天机器人消息：不要通过创建单独的帖子来向用户发送垃圾邮件。 在同一线程中创建一个回复帖子。
* **个人应用中的自动** 程序消息：不要快速连续发送多个邮件。 发送一条包含完整信息的邮件。 避免多轮对话以完成单个工作流。 相反，请考虑使用窗体模块 (任务) 一次收集用户的所有输入。
* **欢迎邮件**：不允许和视为垃圾邮件，并定期重复相同的欢迎邮件。 例如，将新成员添加到团队时，不要向其他成员发送欢迎消息。 改为以个人身份向新成员发送消息。

### <a name="bot-notifications"></a>自动程序通知

自动程序通知必须包含与为聊天机器人组、团队、聊天或个人 (范围相关的) 。

### <a name="bots-and-adaptive-cards"></a>机器人和自适应卡片

自适应卡片是高度推荐的显示自动程序消息的方法。 你的卡片必须轻量，并且仅包含 1-3 个操作。 如果需要显示更多内容，请考虑使用任务模块或选项卡。

有关更多信息，请参阅以下资源：

* [设计自适应卡片](~/task-modules-and-cards/cards/design-effective-cards.md)
* [卡参考](~/task-modules-and-cards/cards/cards-reference.md#types-of-cards)

## <a name="messaging-extensions"></a>消息传递扩展

如果你的应用包括消息传递扩展，请确保它遵守这些准则。

> [!TIP]
> 有关创建高质量应用体验的信息，请参阅Teams[扩展设计指南](~/messaging-extensions/design/messaging-extension-design.md)。

### <a name="action-commands"></a>操作命令

基于操作的邮件扩展应执行以下操作：

* 允许用户在未完成中间步骤（如登录）的情况下触发对邮件的操作。
* 将消息上下文传递到下一个工作状态。

### <a name="preview-links-link-unfurling"></a>预览链接 (链接取消) 

邮件扩展应在"撰写"框中预览Teams的链接。 不要添加位于您控制之外的域 (绝对 URL 或通配符) 。 例如， `yourapp.onmicrosoft.com` 有效， `*.onmicrosoft.com` 但无效。 顶级域也被禁止 (例如， `*.com` 或 `*.org`) 。

### <a name="search-commands"></a>搜索命令

* 基于搜索的消息扩展必须提供可帮助用户有效搜索的文本。
* @mention可执行文件必须清晰、易于理解且可读。

## <a name="task-modules"></a>任务模块

任务模块必须包含一个图标和与其关联的应用的短名称。

> [!TIP]
> 有关创建高质量应用体验的信息，请参阅Teams[模块设计指南](~/task-modules-and-cards/task-modules/design-teams-task-modules.md)。

## <a name="meeting-extensions"></a>会议扩展

如果你的应用包括会议扩展，请确保它遵守这些准则。

> [!TIP]
> 有关创建高质量应用体验的信息，请参阅Teams[扩展设计指南](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)。

### <a name="pre--and-post-meeting-experience"></a>会议前和会议后体验

* 会议前和会议后屏幕必须遵守常规选项卡设计准则。 有关详细信息，请参阅设计[Teams指南](~/tabs/design/tabs.md)。
* 选项卡不得具有水平滚动。
* 当显示多个项目时，选项卡应具有有序布局。 例如，超过 10 次投票或调查。 请参阅示例 [布局](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#after-a-meeting)。
* 当导出调查或投票的结果时，应用必须通知用户"已成功下载结果"。

### <a name="in-meeting-experience"></a>会议内体验

* 应用在会议期间只能使用深色主题。 有关详细信息，请参阅设计[Teams指南](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#theming)。
* 在会议期间将鼠标悬停在应用图标上时，工具提示应显示应用名称。
* 在会议期间，消息传递扩展的功能必须与在会议外相同。

### <a name="in-meeting-tabs"></a>会议内选项卡

* 必须响应。 确保保持填充和组件大小。
* 如果存在多个导航层，则必须有一个后退按钮。
* 不得包含多个消除或关闭按钮。 这可能会导致用户混淆，因为已有一个可消除选项卡的内置标题按钮。
* 不得具有水平滚动。

### <a name="in-meeting-dialogs"></a>会议内对话框

* 应谨慎使用，并且应用于轻型和面向任务的场景。
* 必须在单个列中显示内容，并且不能有多个导航级别。
* 不得使用任务模块。
* 必须与会议阶段的中心对齐。
* 用户选择按钮或执行某个操作后应消除。

## <a name="notifications"></a>通知

如果你的应用使用[Microsoft Graph](/graph/teams-send-activityfeednotifications)提供的活动源 API，请确保它遵守以下准则。

### <a name="general"></a>概要

* 在应用配置中指定的所有通知触发器都应在应用中收到通知。
* 通知必须按为应用配置的受支持语言进行本地化。
* 通知必须在用户操作五秒钟内显示。

### <a name="avatars"></a>头像

* 通知头像应匹配应用的颜色图标。
* 用户触发的通知应包括用户的头像。

### <a name="spamming"></a>垃圾邮件

* 应用每分钟向用户发送的通知数不能超过 10 个。
* 自动程序和活动源不应触发重复通知。
* 通知必须为用户提供一些值，并且不能用于普通或不相关的事件。

### <a name="navigation-and-layout"></a>导航和布局

* 通知必须遵循活动Teams布局和体验。
* 选择通知时，用户必须定向到 Teams 内的相关内容，并且不会从 Teams体验。

## <a name="advertising"></a>广告

应用不得在消息中显示广告，包括动态广告、横幅广告和广告。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [创建合作伙伴中心帐户](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)
