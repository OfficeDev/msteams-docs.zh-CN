---
title: Microsoft Teams 商店验证指南
description: 介绍了每个提交给团队商店 (AppSource) 的应用程序必须遵循的准则。
author: heath-hamilton
ms.author: surbhigupta
ms.topic: reference
ms.localizationpriority: medium
ms.openlocfilehash: 6326c8ff28857ab75436e61de5b8783842642acb
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2022
ms.locfileid: "63399133"
---
# <a name="microsoft-teams-store-validation-guidelines"></a>Microsoft Teams 商店验证指南

遵循这些准则会增加应用通过 Microsoft Teams 应用商店提交程序的机会。 这些特定于 Teams 的准则是对 Microsoft [商业市场认证策略](/legal/marketplace/certification-policies) 的补充，并经常更新以反映新功能、用户反馈和业务规则更改。

> [!NOTE]
>
> * 某些准则可能不适用于你的应用。 例如，如果应用不包含机器人，则可以忽略与机器人相关的准则。
> * 我们已将这些准则交叉引用到 Microsoft 商业认证策略，并添加了注意事项，其中包含验证过程中遇到的通过或失败情况的示例。
> * 某些准则标记为 *强制修复*。 如果你的应用提交不符合这些强制性准则，你将收到来自我们的失败报告，其中包含缓解措施。 仅在你修复了Microsoft Teams后，你的应用提交才能通过应用商店验证。
> * 其他准则标记为 *建议修复*。 为了获得理想的用户体验，我们建议你解决这些问题，但是，如果你选择不解决这些问题，也不会阻止你的应用提交在 Teams 应用商店上发布。

## <a name="value-proposition"></a>价值主张

> [!NOTE]  
> 本部分符合 [Microsoft 商业认证策略编号 1140.1](/legal/marketplace/certification-policies#11401-value-proposition-and-offer-requirements)，并为 Microsoft Teams 应用的开发人员提供有关其产品/服务价值主张的其他准则。

### <a name="app-name"></a>应用名称

[*强制修复*]

> [!NOTE]  
> 本部分符合 Microsoft [商业认证策略编号 1140.1.1](/legal/marketplace/certification-policies#114011-app-name)，并为 Microsoft Teams 应用的开发人员提供有关命名其应用的其他准则。

应用程序的名称对用户如何在商店中发现它起着关键作用。 使用以下准则命名应用：

* 该名称必须包括与用户相关的术语。
* 核心 Teams 功能的名称不得包含在应用名称中，例如：  
  * **聊天**
  * **联系人**
  * **Calendar**
  * **通话**
  * **Files**
  * **活动**
  * **应用**
  * **Help**
* 使用开发人员姓名作为常用名词的前缀或后缀。 例如，**Contoso Tasks** 而不是 **Tasks**。
* 不得使用 **Teams** 或其他 Microsoft 产品名称，如 Excel、PowerPoint、Word、OneDrive、SharePoint、OneNote、Azure、Surface、Xbox 等，这些名称可能会错误地指示品牌联合或联合销售。 有关引用 Microsoft 软件产品和服务的详细信息，请参阅 [Microsoft 商标和品牌准则](https://www.microsoft.com/legal/intellectualproperty/trademarks/usage/general)。
* 如果应用程序是与 Microsoft 官方合作的一部分，则应用程序的名称必须放在前面 (例如，**Contoso Connector for Microsoft Teams**)。
* 不得复制商店中列出的应用程序的名称或商业市场中的其他报价。
* 不得包含亵渎或贬损性的词汇。 该名称也不得包括对种族或文化不敏感的语言。
* 必须是唯一的。 如果你的应用 (Contoso) 在 Microsoft Teams 应用商店和 Microsoft AppSource 中列出，并且你想要列出特定于地理位置的另一个应用，例如 Contoso Mexico，你的提交必须满足以下条件：
  * 在标题、元数据、首次响应应用体验和帮助部分中，强调应用的特定区域功能。 例如，标题必须是 Contoso Mexico。 应用标题必须与出自同一开发人员的现有应用明确区分，以避免最终用户混淆。
  * 在合作伙伴中心上传应用包时，在 **可用性** 部分中选择应用可用的正确的 **市场**。

 > [!TIP]  
 > 你的应用在 Microsoft Teams 应用商店和 Microsoft AppSource 上的品牌打造，包括应用名称、开发人员名称、应用图标、Microsoft AppSource 屏幕截图、视频、简短说明和网站，无论单独还是一起，不得模仿官方 Microsoft 产品/服务，除非你的应用是官方 Microsoft 1P 产品/服务。

### <a name="suitable-for-workplace-consumption"></a>适用于工作区使用

[*强制修复*]

> [!NOTE]  
> 本部分符合 Microsoft 商业认证策略号 [1140.1.2](/legal/marketplace/certification-policies#114012-workplace-appropriateness)、[100.8](/legal/marketplace/certification-policies#1008-significant-value) 和 [100.10](/legal/marketplace/certification-policies#10010-inappropriate-content)，并为开发人员提供了有关构建适合工作场所的应用的其他准则。

应用内容必须适用于一般工作场所使用，并遵循商业市场认证策略中列出的所有限制。 禁止与宗教、政治、赌博和长时间娱乐相关的内容。

你的应用必须增进团队协作、提高个人工作效率，或同时满足两者。 用于团队联系和社交的应用必须是协作的，并且专为多个参与者设计。 应用不得要求每次会话投入时间超过 60 分钟或影响工作效率。

### <a name="similar-platforms-and-services"></a>类似的平台和服务

[*强制修复*]

> [!NOTE]  
> 本部分符合 [Microsoft 商业认证策略号 1140.1.3](/legal/marketplace/certification-policies#114013-other-platforms-and-services)。

应用必须专注于 Teams 体验，并且应用内容或应用元数据中不应包括其他类似的基于聊天的协作平台或服务的名称、图标或图像，除非应用提供特定的互操作性。

### <a name="feature-names"></a>功能名称

按钮和其他 UI 文本中的应用功能名称不得与为 Teams 和其他 Microsoft 产品保留的术语重复。 例如，**开始会议**、**拨打电话** 或 **开始聊天**。 如有必要，请包含你的应用名称，例如 **启动 Contoso 会议**。

### <a name="authentication"></a>身份验证

[*强制修复*]

> [!NOTE]  
> 本部分符合 [Microsoft 商业认证策略 1140.1.4](/legal/marketplace/certification-policies#114014-access-to-services)，并为开发人员提供额有关使用外部服务为其应用进行身份验证的准则。

若要详细了解如何实施应用身份验证，请参阅 [Teams 中的身份验证](~/concepts/authentication/authentication.md)。

#### <a name="authenticating-with-external-services"></a>与外部服务进行身份验证

 如果你的应用使用外部服务对用户进行身份验证，请遵循以下准则：

* **登录、注销和注册体验**:
  * 依赖于外部帐户或服务的应用必须提供清晰且简单的登录、注销和注册体验。
  * 当用户注销时，他们必须仅从应用中注销并保持登录到 Teams。
  * 依赖外部帐户或服务的应用必须为新用户提供一种前进的方法，以便注册或联系应用发布者，以了解有关服务以及获取服务访问权限的方法。
  前进方法必须在应用清单、AppSource 长描述以及应用首次运行体验 (机器人欢迎消息、选项卡设置或配置页面) 中可用。
  * 需要租户管理员完成一次性设置的应用必须强调对租户管理员配置应用的依赖性 (否则其他租户用户不能安装和使用应用)。  
  依赖性必须在应用清单、AppSource 长描述、所有首次运行体验接触点 (机器人欢迎消息、选项卡设置或配置页面)、被视为机器人响应、撰写扩展或静态选项卡内容中的必要部分的帮助文本中强调。
  
* **内容共享体验**: 需要通过外部服务进行身份验证以便在 Teams 频道中共享内容的应用，必须在帮助文档 (或类似资源) 中清楚地说明用户如何断开连接或取消共享内容 (如果外部服务支持此功能)。 这并不意味着取消共享内容的能力必须存在于你的 Teams 应用中。

## <a name="security"></a>安全性

> [!NOTE]  
> 本部分符合 [Microsoft 商业认证策略号 1140.3](/legal/marketplace/certification-policies#11403-security)。

### <a name="financial-information"></a>财务信息

[*强制修复*]

> [!NOTE]  
> 本部分符合 [Microsoft 商业认证策略号 1140.3.1](/legal/marketplace/certification-policies#114031-financial-transactions)，并提供了有关在 Teams 界面中传输财务信息的准则，并通知了开发人员其 Teams 应用的移动 (Android 和 iOS) 版本的受限付款方案。

应用不得要求用户在 Teams 界面中付款，并通过机器人界面将财务信息传输给用户。  

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![应用内付款](~/assets/images/submission/validation-financial-information-1.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

只有在用户同意使用应用之前，在使用条款、隐私策略、配置文件页面或网站中披露外部付款服务，你才能提供安全外部付款服务的链接。

请勿通过应用为 [常规策略编号 100.10 不适当的内容](/legal/marketplace/certification-policies#10010-inappropriate-content)禁止的商品或服务提供付款。

在 iOS 或 Android 版本的 Teams 上运行的应用必须遵循以下准则:

* 应用不得包括旨在向用户推销支付版本的应用内购买、试用优惠或 UI，或指向可以购买其他内容、应用程序或加载项的联机应用商店的链接。

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![应用内购买](~/assets/images/submission/validation-financial-information-in-app-purchase.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![联机应用商店](~/assets/images/submission/validation-financial-information-online-stores.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* 如果应用需要帐户，则用户必须能够免费注册帐户。 禁止使用 **免费** 或 **免费帐户** 的术语。
* 你可以决定帐户是无限期处于活动状态还是仅在有限时间内处于活动状态。 当帐户过期时，应用不得显示指示需要付款的 UI、文本或链接。
* 应用的隐私策略和使用条款页面必须不含任何与商业相关的 UI 或链接。

### <a name="bots"></a>机器人

[*强制修复*]

> [!NOTE]
> 本部分符合 [Microsoft 商业市场策略号 1140.3.2](/legal/marketplace/certification-policies#114032-bots-and-messaging-extension)。

对于使用 Microsoft Azure 机器人服务的应用 (如机器人和消息传递扩展)， 则必须遵循 Microsoft [在线服务条款](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46) 中定义的所有要求。

机器人必须始终请求上传文件的权限并显示确认消息。

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![确认消息](~/assets/images/submission/validation-bot-confirmation-message.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

### <a name="external-domains"></a>外部域

[*强制修复*]

> [!NOTE]
> 本部分与 [Microsoft 商业市场策略号 1140.3.3](/legal/marketplace/certification-policies#114033-external-domains)，并提供了有关在 `validDomains` 清单属性中使用受限域的开发人员指南。

不要在组织的控制范围外包括域 (包括) 域配置中的通配符和隧道服务。 以下的例外情况包括:

* 如果应用使用 Azure 机器人服务的 OAuthCard，则必须将 `token.botframework.com` 作为有效的域包含在内，否则 **登录** 按钮将无法工作。
* 如果应用依赖于 SharePoint，则可以使用 `{teamSiteDomain}` 上下文属性将关联的根 SharePoint 站点作为有效域包含。

#### <a name="government-community-cloud-listings"></a>政府社区云列表

若要将应用分发给政府社区云 (GCC) 用户，身份验证过程必须标识用户并将其路由到 GCC 特定 URL 或预期 URL，同时避免在 Teams 应用商店中重复列出。

### <a name="sensitive-content"></a>敏感内容

[*强制修复*]

你的应用不得将敏感数据（如信用卡、财务付款详细信息、健康情况、接触者追踪或其他个人身份信息 （PII））发布给不应该查看该内容的受众。

应用必须在将任何文件或可执行文件 (.exe) 下载到用户计算机或环境中之前警告用户。

## <a name="general-functionality-and-performance"></a>常规功能和性能

> [!NOTE]
> 本部分符合 [Microsoft 商业市场策略号 1140.4](/legal/marketplace/certification-policies#11404-functionality)。

### <a name="launching-external-functionality"></a>正在启动外部功能

[*强制修复*]

应用不得将用户带出 Teams 的核心用户场景。 应用内容和交互必须在 Teams 的功能中发生，如机器人、自适应卡片和任务模块。

应在 Teams 应用内链接用户，而不是链接到外部网站或应用。 对于需要外部功能的情况，你的应用必须获得明确的用户权限才能启动该功能。

启动外部功能的按钮 UI 文本必须包含指示用户已退出 Teams 实例的内容。 例如，包括如下文本，**由此转到 Contoso.com** 或 **在 Contoso.com 中查看**。

### <a name="compatibility"></a>兼容性

[*强制修复*]

应用必须能够在以下操作系统和浏览器的最新版本上正常运行:

* Microsoft Windows
* macOS
* MicrosoftEdge&nbsp;
* Google Chrome
* iOS
* Android

你的应用必须在不受支持的浏览器和操作系统上显示得体的失败消息。

### <a name="response-time"></a>答复时间

[*强制修复*]

Teams 应用必须在合理的时间范围内响应，或显示正在加载或键入的指示、消息或警告。

* 选项卡必须在两秒钟内响应，或显示正在加载的消息或警告。
* 机器人必须在两秒内响应用户命令或显示键入指示器。
* 消息传递扩展必须在两秒钟内响应用户命令。
* 通知必须在用户操作后两秒钟内显示。

## <a name="app-package-and-store-listing"></a>应用包和应用商店列表

[*强制修复*]

必须正确设置应用包的格式，并包含所有必需的信息和组件。

> [!TIP]  
> 必须包含以下详细的测试说明来验证应用提交：
>
> * 在应用依赖于外部帐户进行身份验证的情况下，**配置应用测试帐户的步骤**。
> * Teams 内核心工作流的 **预期应用行为** 摘要。
> * **清楚地描述** 应用长描述和相关材料中的功能、特性和可交付结果的限制、条件或例外情况。
> * 在验证应用提交时，为测试人员 **强调注意事项**。  
> * **使用虚拟数据预填充测试帐户**，以有助于测试。

### <a name="app-manifest"></a>应用部件清单

[*强制修复*]

Teams 应用清单定义应用的配置。

* 清单必须符合公开发布的清单架构。 有关详细信息，请参阅 [清单参考](~/resources/schema/manifest-schema.md)。 请勿使用清单的预览版本提交应用。
* 如果应用包括机器人或消息传递扩展，则应用清单中的详细信息必须与机器人框架元数据保持一致，包括机器人名称、徽标、隐私策略链接和服务条款链接。
* 如果你的应用使用 Azure Active Directory 进行身份验证，则Microsoft Azure Active Directory (Azure AD) 包含 (客户端) ID。 更多相关信息，请参阅 [清单参考](~/resources/schema/manifest-schema.md#webapplicationinfo)。

### <a name="app-icons"></a>应用图标

[*强制修复*]

图标是用户在浏览 Teams 应用商店时看到的主要元素之一。 图标必须传达应用的品牌和用途，同时遵循以下要求：

* 你的应用包必须包含两.png版本的应用图标：颜色图标和大纲图标。
* 图标的颜色版本必须为 192x192 像素。 图标符号可以是任何颜色，但必须位于纯色或完全透明的方形背景上。
* 以下情况中将显示图标的轮廓版本：
  * 你的应用正在使用并 **托管** 在 Teams 左侧应用栏上。
  * 当用户固定你的应用的消息传递扩展时。

* 轮廓版本必须为 32x32 像素，并且可以是白色（背景透明）或透明（白色背景）。 图标不得在符号周围有任何额外填充。

* 你的应用包必须包含大小正确且格式正确的图标。 图标必须与应用商店列表元数据中的信息匹配。

有关详细信息，请参阅 [图标准则](~/concepts/build-and-test/apps-package.md#app-icons)。

### <a name="app-descriptions"></a>应用说明

必须对应用有一个简短而长的介绍。 应用配置和合作伙伴中心中的说明必须相同。

说明不得直接或通过影射贬损其他品牌（Microsoft 所有或其他）。 请确保说明不包含无法证实的声明。 例如，**保证效率提高 200%**。

#### <a name="short-description"></a>简短说明

简短说明是应用的简要摘要，突出显示其价值主张，并面向目标受众。

**应做:**

* 将简短说明保留为一句话。
* 首先放置最重要的信息。
* 包括客户可能搜索的关键字。
* 有效使用可用字符限制。 例如，不要重复应用名称。

**不应做:**

[*建议修复*]

在简短说明中使用 **应用** 一词。

#### <a name="long-description"></a>较长说明

长描述可以提供具有吸引力的叙述，突出显示应用的价值主张、主要受众和目标行业。 虽然此说明可以长达 4，000 个字符，但大多数用户仅会阅读 300-500 个字。

**应做:**

* 使用 [Markdown](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) 设置说明的格式。
* 使用主动语音并直接与用户交谈。 例如，**可以...**。
* 列出带项目符号点的功能，以便更轻松地扫描说明。
* 在用户安装应用之前，请在列表和相关材料中清楚地描述功能以及可交付结果的限制、特性、条件或例外情况。 这些 Teams 功能必须与列表中描述的核心功能相关。
* 请确保应用说明与 Teams 应用内的功能相匹配。 对 Teams 应用外部工作流的任何引用都必须受到限制，并且必须在 Teams 应用功能中明确强调。
* 包括帮助或支持链接。
* 请参阅 **Microsoft 365**，而不是 **Office 365**。
* 如果需要引用 **Teams**，请将第一个引用写为 **Microsoft Teams**。 以后的引用可以缩短为 **Teams**。
* 在描述应用如何与 Teams (或 Microsoft 365) 配合使用时，请使用以下语言:
  * **“... 可用于 Microsoft Teams。”**
  * **“... 正用于 Microsoft Teams。”**
  * **“... 在 Microsoft Teams 内。”**
  * **“... 适用于 Microsoft Teams。”**
  * **“... 与 Microsoft Teams 集成。”**
  * **“...专为...构建”**
  * **“...专为...开发”**
  * **“...专为...设计”**

**不应做:**

[*强制修复*]

* 超过 500 字。
* 将 **Microsoft** 缩写为 **MS** 或 **MSFT**。
* 指示应用是来自 Microsoft 的产品/服务，包括使用 Microsoft 的标语或标志行。
* 使用未拥有的受版权保护的品牌名称。
* 除非你是经认证的 Microsoft 合作伙伴，否则请使用以下语言:
  * **“ ...通过...认证”**
  * **“...由...提供支持”**
* 包括拼写错误、语法错误。
* 不必要地将整个清单或 AppSource 长描述或应用内容大写。
* 包括指向 AppSource 的链接。
* 作出未经验证的声明。 例如，最好、顶级和排名，除非附带声明的来源。
* 将产品/服务与其他市场产品/服务进行比较。

### <a name="screenshots"></a>屏幕截图

屏幕截图提供了应用的突出视觉预览，以补充应用名称、图标和说明。 请记住以下事项：

* 每个列表最多可以有五个屏幕截图。
* 支持的文件类型包括 PNG、JPEG 和 GIF。
* 尺寸必须为 1366x768 像素。
* 最大尺寸为 1，024 KB。

**应做:**

* 专注于应用的功能。例如，用户如何与机器人沟通。
* 包括能准确代表应用程序的内容。
* 谨慎使用文本。
* 使用反映品牌和包含营销内容的颜色作为屏幕截图的边框。

**不应做:**

[*建议修复*]

* 显示特定设备，例如手机或笔记本电脑。
* 显示不在应用中的部件版式或 UI。
* 在屏幕截图中捕获任何 Teams 或浏览器 UI。
* 包括不准确反映应用实际 UI 模型，例如显示应用在 Teams 外部使用。

> [!TIP]  
> 视频可能是传达用户必须使用你的应用的原因的最有效方法。 用户也将在列表中首先看到视频。 有关详细信息，请参阅 [创建商店列表视频](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#create-a-video)。

### <a name="privacy-policy"></a>隐私策略

[*强制修复*]

隐私策略可以特定于 Teams 应用或所有服务的整体策略。

* 如果使用通用隐私策略模板，则必须添加对隐私策略范围中的 **服务**、**应用程序** 或 **平台** 的引用。  如果包含对 **服务**、**应用程序** 和 **平台** 的引用，则无需在范围内指定 Teams 应用。 应用验证过程将解释这些引用，以包括 Teams 应用以及其他服务或网站。
* 必须包括处理用户数据存储、保留和删除的方式。 你必须描述用于数据保护的安全控件。
* 必须包含联系人信息。
* 不得包括已损坏、用于 beta 或暂存目的的 URL。
* 不得包含指向 AppSource 的链接。
* 不得要求身份验证来访问隐私策略。
* 不得包含任何商务 UI 或商店链接。

### <a name="terms-of-use"></a>使用条款

[*强制修复*]

使用以下准则编写使用条款：

* 必须具体且适用于你的产品/服务。
* 必须托管在你自己的域中。
* 必须具有安全的 (HTTPS) 链接。
* 对使用条款的访问不得要求身份验证。

### <a name="support-links"></a>支持链接

应用的支持 URL 不得要求身份验证。 例如，用户不得登录来联系你。

支持 URL 必须包含你的联系方式详细信息或供用户提出支持票证的方式。 例如，如果你的支持 URL 托管在 GitHub 上，GitHub 页面必须处于你的所有权下，并且必须包括你的联系方式详细信息或供用户提出支持票证的方式。 [*强制修复*]

  ![支持 URL](~/assets/images/submission/validation-supportlinks-authentication.png)  

### <a name="localization"></a>本地化

[*强制修复*]

如果应用支持本地化，则应用包必须包含基于 Teams 语言设置显示的语言翻译文件。 该文件必须符合 Teams 本地化架构。 有关详细信息，请参阅 [Teams 本地化架构](~/concepts/build-and-test/apps-localization.md)。

## <a name="apps-linked-to-saas-offer"></a>链接到 SaaS 产品/服务的应用

* ISV 必须支持相同租户中的多个用户 (订阅者) 管理自己的订阅，并将许可证分配给租户中的用户。
* 产品/服务必须满足链接到 SaaS 产品/服务的 Teams 应用的所有[技术要求](/microsoftteams/platform/concepts/deploy-and-publish/appsource/prepare/include-saas-offer?branch=pr-en-us-2759)。
* 链接到 SaaS 产品/服务的 Teams 应用必须满足[1000 服务型软件 (SaaS)](/legal/marketplace/certification-policies#1000-software-as-a-service-saas) 中定义的所有要求。
* 清单文件中提到的 `subscriptionOffer` 详细信息必须正确。 在应用清单中，使用值 `publisherId.offerId` 添加或更新节点 `subscriptionOffer`。 例如，如果你的发布者 ID 是 `contoso1234`，并且你的产品/服务 ID 是 `offer01`，你在应用清单中指定的值必须是 `contoso1234.offer01`。
* 链接到 SaaS 产品/服务的 Teams 应用必须在 AppSource 中已推出，并且不接受预览产品/服务通过应用商店批准。

### <a name="offer-metadata"></a>产品/服务元数据

* 产品/服务元数据必须与 Teams 清单、AppSource 中的 Teams 应用列表和 AppSource 中的 SaaS 产品/服务匹配。
* Teams 应用和 SaaS 产品/服务必须来自同一发布者或开发人员。 应用清单中引用的 SaaS 产品/服务必须属于将 Teams 应用提交给商业市场时相同的发布者。
* 由于你提交的产品/服务是链接到 SaaS 产品/服务的 Teams 应用，因此你必须在产品/服务列表的合作伙伴中心产品设置部分中将 **其他购买** 选择为 **是，我的产品需要购买服务或提供其他应用内购买**。
* 计划说明和定价详细信息必须为用户提供足够的信息，以清楚地了解产品/服务列表。
* 必须在计划说明中准确指出所提供的功能的任何限制、对其他服务的依赖和例外。
* 链接到 SaaS 产品/服务的 Teams 应用旨在支持按姓名和用户分配许可证。 有时，SaaS 产品/服务是使用其他方法构建的，或者具有专门的购买流。 你必须在应用元数据和订阅计划详细信息中清楚地提及构建方法和购买流的详细信息。
* SaaS 产品/服务必须为购买流的所有适用状态中的所有用户提供消息和准则。

### <a name="saas-offer-home-page-and-license-management"></a>SaaS 产品/服务主页和许可证管理  

* 向订阅者提供有关如何使用产品的介绍。
* 允许订阅者分配许可证。
* 提供不同的与支持部门互动的方式以解决问题，例如常见问题解答、知识库和电子邮件地址。
* 验证用户以确保他们尚未通过其他用户分配许可证。
* 许可证分配后通知用户。
* 通过 Teams 聊天机器人或电子邮件，指导用户如何将应用添加到 Teams 并开始使用。

### <a name="usability-and-functionality"></a>可用性和功能  

* 成功购买和分配许可证后，必须提供以下内容：
  * 用户订阅计划功能的访问权限。
  * 用户订阅计划的价值增加和显著优势。
* 从 Teams 应用中，提供指向 SaaS 应用程序主页的链接，以便订阅者将来管理许可证。

### <a name="configure-and-test-saas-application"></a>配置和测试 SaaS 应用程序

如果出于测试目的的应用设置非常复杂，请提供端到端功能文档、链接的 SaaS 产品/服务配置步骤，以及作为"认证说明"一部分的许可证和用户管理说明。

> [!TIP]  
> 你可以添加一个有关应用和许可证管理工作原理的视频，以帮助团队进行测试。

## <a name="tabs"></a>选项卡

> [!NOTE]  
> 本部分符合 [Microsoft 商业市场策略号 1140.4.2](/legal/marketplace/certification-policies#114042-tabs)。
如果你的应用包含选项卡，请确保它遵守这些准则。
> [!TIP]
> 有关创建高质量应用体验的详细信息，请参阅 [Teams 设计指南](~/tabs/design/tabs.md)。

### <a name="setup"></a>安装

* 选项卡设置 **不得终止** 新用户。 提供有关如何完成操作或工作流的信息。 [*强制修复*]

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![创建新帐户](~/assets/images/submission/validation-tabs-setup-create-new-account.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![缺少前进指南](~/assets/images/submission/validation-tabs-missing-forward-guidance.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![新用户注册](~/assets/images/submission/validation-tabs-setup-new-user.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* 为了获得最佳首次运行体验，在选项卡设置过程中对用户进行身份验证，而不是之后进行身份验证。 身份验证可在选项卡配置窗口外发生。 [*建议修复*]

* 用户不得离开 Teams 内部的选项卡配置体验以在 Teams 外部创建内容，然后返回到 Teams 以固定内容。 选项卡配置屏幕必须说明配置值以及如何配置。 [*强制修复*]

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![获取配置文件名称](~/assets/images/submission/validation-tabs-setup-profile-name.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* 选项卡配置屏幕不得嵌入整个网站。 使配置体验保持专注。 例如，如果要构建允许用户在频道中配置项目的项目管理应用，请保持选项卡配置屏幕专注于允许用户从应用中选择要在频道中配置的项目。 [*强制修复*]

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![配置体验](~/assets/images/submission/validation-tabs-setup-configuration-experience.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![配置屏幕](~/assets/images/submission/validation-tabs-setup-configuration-screen.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* 选项卡配置屏幕不得要求用户嵌入 URL。 要求用户在选项卡设置期间配置 URL 是不好的 UX，用户离开选项卡配置屏幕，获取 URL，返回到配置屏幕并输入 URL。 预先存在的 Teams 功能已允许用户在频道中固定网站链接。 如果你的应用要求用户在选项卡配置期间嵌入网站 URL，并且应用限制为在频道选项卡中显示整个网站内容，则你的应用不会为用户提供重要价值。 [*强制修复*]

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![已配置的 URL](~/assets/images/submission/validation-tabs-setup-configured-url.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
         ![已配置的 URL 受限](~/assets/images/submission/validation-tabs-setup-configured-url-two.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

### <a name="views"></a>视图

* 登录屏幕区域不得使用大型徽标。 [*强制修复*]

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![查看大型徽标](~\assets\images\submission\validation-views-applogin.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* 可以通过跨多个选项卡进行分解来简化内容。 [*建议修复*]

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![多个选项卡](~/assets/images/submission/validation-views-multiple-tabs.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* 选项卡不应具有重复的标题。 从 iframe 中删除重复的徽标，因为选项卡框架已经显示应用图标和名称。 [*建议修复*]

 :::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![重复的标题徽标](~/assets/images/submission/validation-views-duplicate-header-logo.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  

### <a name="navigation"></a>导航

下面是导航准则：

* 选项卡不得提供与主要 Teams 导航冲突的导航。 如果在选项卡中提供左侧导航，则它不能只包含图标或具有堆叠文本的图标。 它不能是具有查看带有堆叠文本的图标的选项的可折叠的栏 (模仿 Teams 导航栏)。 包括带内联文本的图标或仅文本，或使用汉堡菜单而不是选项卡左栏。 [*强制修复*]

使用 [基本](~/concepts/design/design-teams-app-basic-ui-components.md) 和 [高级](~\concepts\design\design-teams-app-advanced-ui-components.md) Fluent UI 组件设计应用。

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![左侧导航](~/assets/images/submission/validation-navigation-left-navigation.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![图标和文本](~/assets/images/submission/validation-navigation-icon-text.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![可折叠的左栏](~/assets/images/submission/validation-navigation-collapsable-left-rail.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![静态选项卡](~/assets/images/submission/validation-navigation-static-tab.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![水平栏](~/assets/images/submission/validation-navigation-horizontal-rail.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* 左栏中具有工具栏的选项卡必须与 Teams 左侧导航保留 20px 的间距。 [*强制修复*]

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![工具栏之间的间距](~/assets/images/submission/validation-navigation-spacing-between-toolbar.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  

* 选项卡中的第二级页面和第三级页面必须在主选项卡区域的第二级 (L2) 和第三级 (L3) 视图中打开，该视图通过痕迹导航或左侧导航进行导航。 还可以包括以下组件来辅助选项卡导航： [*强制修复*]
  * 后退按钮
  * 页眉
  * 汉堡菜单
* 选项卡不能有水平滚动。 白板应用和其他需要较大画布以允许用户协作而不会造成不良应用体验的应用，可以使用水平滚动，具体取决于他们的业务需求。 [*建议修复*]

* 选项卡中的深层链接不能链接到外部网页，而应链接到 Teams 内部的某个位置。 例如，任务模块或其他选项卡。 [*强制修复*]

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![未链接的视图按钮](~/assets/images/submission/validation-navigation-view-button-not-linked-static-tab.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* 选项卡不得允许用户导航到 Teams 外部以获得核心应用体验。 对于非核心工作流，选项卡可以重定向到 Teams 外部。 例如，提出支持票证。 [*强制修复*]

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![配置选项卡内的核心工作流](~/assets/images/submission/validation-navigation-core-workflow-within-configuration.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![应用核心工作流重定向到外部](~/assets/images/submission/validation-navigation-core-workflow-redirects-outside.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

### <a name="usability"></a>可用性

* 选项卡必须提供价值，而不仅仅是托管现有网站。 [*强制修复*]

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![可用性应用提供工作流](~/assets/images/submission/validation-usability-app-provides-workflows.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![可用性网站 I-Frame](~/assets/images/submission/validation-usability-website-i-framed.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![可用性 Teams 应用相同](~/assets/images/submission/validation-usability-teams-app-identical-website.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* 内容不得在选项卡中截断或重叠。

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![可用性内容截断](~/assets/images/submission/validation-usability-content-truncation.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* 用户必须能够撤消其在选项卡中的最后一个操作。

* 个人上下文中的选项卡可以从应用的共享实例中聚合内容。 例如，具有可配置选项卡的项目管理应用程序（允许频道成员在看板卡上对项目进行注释）必须聚合此内容并显示在个人应用程序中。 [*建议修复*]

* 选项卡必须响应 Teams 主题。 当用户更改主题时，应用的主题必须反映所选内容。

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![可用性响应选项卡](~/assets/images/submission/validation-usability-responsive-tabs.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![可用性无响应选项卡](~/assets/images/submission/validation-usability-unresponsive-tabs.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* 选项卡必须尽可能使用 Teams 样式的组件，如 Teams 字体、类型渐变、调色板、网格系统、动作、语音音调等。 有关详细信息，请参阅[选项卡设计指南](/microsoftteams/platform/tabs/design/tabs)。 [*建议修复*]

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![可用性不同的字体](~/assets/images/submission/validation-usability-app-uses-diff-font.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* 如果你的应用功能需要更改设置，请包含一个 **设置** 选项卡。 [*建议修复*]
* 选项卡必须遵循 Teams 交互设计，例如页面内导航、对话的位置和使用、信息层次结构等。 有关详细信息，请参阅 [Microsoft Teams Fluent UI 工具包](~/concepts/design/design-teams-app-basic-ui-components.md)

* iframe 中的选项卡内容不得包含模拟 Teams 核心功能的功能。 例如，机器人、消息传递扩展、呼叫、会议等。

* 对于频道的所有成员，可配置选项卡的登录页面中的内容必须上下文相同。

* 可配置选项卡的登录页中的内容不得被限制为供个人使用，并不得包含个人内容，如"**我的任务**"或"**我的仪表板**"。

* 如果你的应用需要为用户提供个人范围视图以提高效率或工作场所的工作效率，请使用筛选视图、个人应用的深层链接，或导航到可配置选项卡内的 L2 或 L3 视图，并在使所有用户的登录页面保持上下文相同。

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![可用性可配置选项卡个人信息](~/assets/images/submission/validation-usability-configurable-tab-personal-info.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  

* 可配置选项卡必须具有重点功能。

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![可用性可配置的嵌套选项卡](~/assets/images/submission/validation-usability-configurable-nested-tabs.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* 选项卡体验必须在移动设备（Android 和 iOS）上完全响应。

> [!TIP]
>
> * 将个人机器人与个人选项卡一起包含在一起。
> * 允许用户从其个人选项卡中共享内容。

## <a name="bots"></a>机器人

> [!NOTE]
> 本部分符合 [Microsoft 商业市场策略号 1140.4.3](/legal/marketplace/certification-policies#114043-bots)。

如果你的应用包含机器人，请确保它遵守这些准则。

> [!TIP]
> 有关创建高质量应用体验的详细信息，请参阅 [Teams 机器人设计准则](~/bots/design/bots.md)。

### <a name="bot-commands"></a>机器人命令

很难分析用户输入和预测用户意向。 机器人命令为用户提供了一组供机器人理解的字词或短语。

* 强烈建议在应用配置中列出支持的机器人命令。 当用户尝试向机器人发送消息时，这些命令将显示在撰写框中。

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![列出的机器人命令](~/assets/images/submission/validation-bot-commands-listed.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::
  
:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![未列出的机器人命令](~/assets/images/submission/validation-bot-commands-not-listed.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* 机器人支持的所有命令必须正常工作，包括常规命令，如 **Hi**、**Hello** 和 **Help**。

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![机器人帮助命令](~/assets/images/submission/validation-bot-help-command.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* 机器人命令不得将用户引入死路，这些命令必须始终提供前进的方法。

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![机器人命令死路](~/assets/images/submission/validation-bot-commands-deadend.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

> [!TIP]
> 对于个人机器人，请包括一个 **帮助** 选项卡，进一步描述机器人可以执行的操作。

### <a name="bot-welcome-messages"></a>机器人欢迎消息

* 如果应用具有复杂的配置流 (需要企业许可证或缺少直观的注册流) ，则此类应用中的机器人必须在首次运行时始终发送欢迎消息。 为了获得最佳体验，欢迎消息必须包含机器人提供给用户的价值、在频道中安装机器人的用户、如何配置机器人并简要描述所有受支持的机器人命令。 可以使用带按钮的自适应卡片显示欢迎消息，以提供更好的可用性。 有关详细信息，请参阅 [如何触发机器人欢迎消息](~/bots/how-to/conversations/send-proactive-messages.md)。 对于没有复杂配置流的应用，你可以选择在机器人首次运行体验期间触发欢迎消息。 但是，如果触发欢迎消息，则必须遵循欢迎消息准则。

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![机器人欢迎消息](~/assets/images/submission/validation-bot-welcome-message.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![机器人无欢迎消息](~/assets/images/submission/validation-bot-no-welcome-message.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* 首次运行期间，频道和聊天中的机器人欢迎消息是可选的，尤其是在机器人可供个人使用并执行类似操作时。 机器人不得向用户单独发送欢迎 (将被视为[垃圾邮件](#bot-message-spamming))。 消息还必须提及添加机器人的用户。

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![欢迎消息未触发](~/assets/images/submission/validation-bot-welcome-message-not-triggered.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![欢迎消息已触发](~/assets/images/submission/validation-bot-welcome-message-triggered.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

> [!TIP]
> 在向单个用户发送的欢迎消息中，一次全方位介绍可以有效概述机器人和任何其他应用功能，鼓励用户尝试机器人命令。 例如，**创建任务**。

### <a name="bot-message-spamming"></a>机器人邮件垃圾邮件

机器人不得向用户发送垃圾邮件，即在短时间内发送多条消息。

* **频道和聊天中的机器人邮件**: 请勿通过创建单独的帖子向用户发送垃圾邮件。 创建单一的帖子，并在同一线程中进行回复。

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![机器人发送一条垃圾消息](~/assets/images/submission/validation-bot-message-spamming-one-message.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![机器人发送多条垃圾消息](~/assets/images/submission/validation-bot-message-spamming-multiple-messages.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* **个人应用中的机器人消息**：
  * 不要在短时间内发送多条消息。
  * 发送一条包含完整信息的消息。
  * 避免通过多轮对话完成单个重复工作流。
  * 使用窗体 (或任务模块) 一次性收集用户的所有输入。
  * 基于 NLP 的对话聊天机器人可以使用多轮对话使讨论更具吸引力并完成工作流。

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![机器人使用任务模块](~/assets/images/submission/validation-bot-messages-using-task-module.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![机器人使用多轮对话](~/assets/images/submission/validation-bot-messages-using-mutliple-conversation.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* **欢迎消息**：不要定期重复相同的欢迎消息。 例如，将新成员添加到团队时，不要向其他成员发送显示为欢迎消息的垃圾邮件。 向新成员单独发送消息。

### <a name="bot-notifications"></a>机器人通知

机器人通知必须包含与你为机器人 (团队、聊天或个人) 定义的范围相关的内容。

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![机器人通知相关](~/assets/images/submission/validation-bot-notifications-relevant.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
         ![机器人通知不相关](~/assets/images/submission/validation-bot-notifications-not-relevant.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

### <a name="bots-and-adaptive-cards"></a>机器人和自适应卡片

自适应卡片是强烈建议显示机器人消息的方法。 卡片必须轻量，并且最多只包含六个操作。 若要显示更多内容，请考虑使用任务模块或选项卡。

有关卡片的详细信息，请参阅：

* [设计自适应卡片](~/task-modules-and-cards/cards/design-effective-cards.md)
* [卡参考](~/task-modules-and-cards/cards/cards-reference.md#types-of-cards)

机器人体验必须在移动设备上完全响应。 机器人响应必须提供一种前进方法（如果适用）。 机器人必须快速响应，并且失败时会显示一条得体的失败错误消息。 基于协作范围内触发器在个人范围内发送给用户的机器人消息必须提供上下文信息 (包括消息的来源)。

### <a name="notification-only-bots"></a>仅通知机器人

由仅通知机器人组成的应用通过基于核心应用或后端中的特定触发器或事件触发用户通知，从而为用户提供价值。 例如，添加了新的销售线索或潜在客户，供销售团队跟进。

如果符合以下情况，则 Teams 中的通知将提供价值：

1. 已发布的卡片或文本提供了足够的详细信息，无需进一步的用户操作。
1. 已发布的卡片或文本提供足够的预览信息，供用户执行操作或决定在 Teams 外部打开的链接中查看更多详细信息。

仅提供包含内容的通知（如 **你有新通知，单击以查看**）并要求用户导航到 Teams 外部以进行其他所有操作的应用不会在 Teams 中提供重大价值。

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
          ![机器人不足信息](~/assets/images/submission/validation-bot-notification-only-inadequete-info.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
          ![机器人充足信息](~/assets/images/submission/validation-bot-notification-only-adequete-info.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

> [!TIP]
> 预览信息并在发布卡片中提供基本的内联用户操作，以便用户无需导航到 Teams 外部进行所有操作 (不考虑复杂性)。

## <a name="messaging-extensions"></a>消息传递扩展

> [!NOTE]
> 本部分符合 [Microsoft 商业市场策略号 1140.4.4](/legal/marketplace/certification-policies#114044-messaging-extensions)。

如果你的应用包括消息传递扩展，请确保它遵循这些准则。

> [!TIP]
> 有关创建高质量应用体验的详细信息，请参阅 [Teams 消息传递扩展设计准则](~/messaging-extensions/design/messaging-extension-design.md)。

### <a name="action-commands"></a>操作命令

基于操作的消息传递扩展必须执行以下操作：

* 允许用户在未完成中间步骤（如登录）的情况下对消息触发操作。

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
          ![无中间步骤 ](~/assets/images/submission/validation-messaging-extension-no-intermediate-step.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
         ![中间步骤可用](~/assets/images/submission/validation-messaging-extension-intermediate-step-available.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* 将消息上下文传递到下一个工作状态。 [*强制修复*]

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
         ![应用传递消息](~/assets/images/submission/validation-messaging-extension-app-passes-message.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![应用不传递消息](~/assets/images/submission/validation-messaging-extension-app-doesnot-pass-message.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* 包含主机应用名称，而不是从聊天消息、频道帖子或应用内操作调用触发的操作命令的通用动词。 例如，使用“**启动 Skype 会议**”代表“**开始会议**”、“**将文件上传到 DocuSign**”代表“**上传文件**”等。 [*建议修复*]

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
         ![操作命令主机名](~/assets/images/submission/validation-messaging-extension-action-command-host-name.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
          ![操作命令动词](~/assets/images/submission/validation-messaging-extension-action-command-verb.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

### <a name="preview-links-link-unfurling"></a>预览链接 (链接展开)

消息传递扩展必须预览在 Teams 撰写框中识别的链接。 不要添加不受控制的域 (无论是绝对 URL 或通配符)。 例如，`yourapp.onmicrosoft.com` 有效，但 `*.onmicrosoft.com` 无效。 也禁止使用顶级域。 例如，`*.com` 或 `*.org`。 [*强制修复*]

### <a name="search-commands"></a>搜索命令

* 基于搜索的消息传递扩展必须提供可帮助用户进行有效搜索的文本。 [*强制修复*]

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
         ![帮助文本可用](~/assets/images/submission/validation-search-commands-text-available.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* @提及可执行文件必须清晰、易于理解且可读。

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
         ![搜索命令不明确可执行](~/assets/images/submission/validation-search-command-unclear-executable.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

### <a name="search-based-messaging-extension-only-apps"></a>仅基于搜索的消息传递扩展应用

[*强制修复*]

由基于搜索的消息传递扩展组成的应用通过共享允许上下文对话而无需上下文切换的卡片为用户提供价值。

若要通过仅基于搜索的消息传递扩展应用的验证，需要将以下内容作为基准，以确保用户体验不受影响。 如果满足以下情况，通过消息传递扩展共享的卡片将在 Teams 中提供价值：

1. 已发布卡片提供了足够详细的信息，无需用户进一步操作。
1. 已发布卡片为用户提供了足够的预览信息，以便进行操作或决定在 Teams 外部打开的链接中进一步查看详细信息。

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![基于搜索的消息传递不足](~/assets/images/submission/validation-search-based-messaging-ext-inadequete-info.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
   ![基于搜索的消息传递足够](~/assets/images/submission/validation-search-based-messaging-ext-adequete-info.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

链接仅展开应用不会在 Teams 中提供重大价值。 如果应用仅支持链接展开且没有其他功能，请考虑在应用中构建其他工作流。

## <a name="task-modules"></a>任务模块

> [!NOTE]
> 本部分符合 [Microsoft 商业市场策略号 1140.4.5](/legal/marketplace/certification-policies#114045-task-modules)。

任务模块必须包含图标及其关联的应用的短名称。 任务模块不得嵌入整个应用，而只能显示完成特定操作所需的组件。 [*强制修复*]

有关详细信息，请参阅[Teams 任务模块设计准则](~\task-modules-and-cards\task-modules\design-teams-task-modules.md)。

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![任务模块显示组件](~/assets/images/submission/validation-task-module-displays-components.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![任务模块嵌入应用](~/assets/images/submission/validation-task-module-embeds-app.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

> [!TIP]
> 有关创建高质量应用体验的详细信息，请参阅 [Teams 任务模块设计准则](~/task-modules-and-cards/task-modules/design-teams-task-modules.md)。

## <a name="meeting-extensions"></a>会议扩展

> [!NOTE]
> 本部分符合 [Microsoft 商业市场策略号 1140.4.6](/legal/marketplace/certification-policies#114046-meeting-extensions)。[!TIP]
> 有关创建高质量应用体验的详细信息，请参阅 [Teams 会议扩展设计准则](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)。

对会议扩展使用以下准则：

* 会议扩展性应用必须提供快速响应的会议内体验，并与 Teams 会议体验保持一致。 会议内体验是强制性的，会议前和会议后体验并非必需。

  * 通过会议前应用体验，用户可以查找和添加会议应用。 用户还可以执行会议前任务，例如发起投票以调查会议参与者。 如果你的应用提供会议前体验，它必须与会议工作流相关。

  * 通过会议后应用体验，用户可以查看会议结果，例如投票调查结果或反馈以及其他应用内容。 如果你的应用提供会议后体验，它必须与会议工作流相关。

  * 通过会议内应用体验，可以在会议期间与会议参与者互动，并增强所有与会者的会议体验。 与会者不得在 Teams 会议之外完成应用的核心用户工作流。

* 除了在 Teams 中提供自定义同框场景模式之外，你的应用还必须提供额外价值。

* 共享会议阶段功能只能通过 Teams 桌面应用启动。 但是，在移动设备上查看时，共享会议阶段使用体验必须可用且不会中断。

> [!TIP]
> 必须将 `groupchat` 声明为 `configurableTabs` 和 `meetingDetailsTab`下的范围，或将 `meetingChatTab` 和 `meetingSidePanel` 声明为清单中的上下文属性，以便在 Teams 移动版上为会议启用你的应用。

### <a name="pre-and-post-meeting-experience"></a>会议前和会议后体验

* 会议前和会议后屏幕必须遵守常规选项卡设计准则。 有关详细信息，请参阅[Teams 设计准则](~/tabs/design/tabs.md)。
* 选项卡不得有水平滚动。
* 显示多个项时，选项卡应具有井然有序的布局。 例如，超过 10 个投票或调查，请参阅 [示例布局](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#after-a-meeting)。
* 当导出调查或投票的结果时，你的应用必须通知用户，表明“**结果已成功下载**”。

### <a name="in-meeting-experience"></a>会议内体验

* 在会议期间应用必须仅能使用深色主题。 有关详细信息，请参阅[Teams 设计准则](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#theming)。
* 在会议期间将鼠标悬停在应用图标上时，工具提示必须显示应用名称。

 :::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![工具提示显示应用名称](~/assets/images/submission/validation-in-meeting-exp-display-app-name.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* 消息传递扩展在会议期间的功能必须与在会议外部执行的相同。

### <a name="in-meeting-tabs"></a>会议内选项卡

* 必须具有响应能力。
* 必须保持填充和组件大小。
* 如果具有多个导航层，则必须有一个后退按钮。

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![会议内后退按钮可用](~/assets/images/submission/validation-in-meeting-exp-back-button.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![会议内后退按钮不存在](~/assets/images/submission/validation-in-meeting-exp-back-button-absent.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* 不得包含多个关闭按钮。 它可能会让用户混淆，因为已有一个可关闭选项卡的内置标题按钮。
* 不得有水平滚动。

### <a name="in-meeting-dialogs"></a>会议内对话

* 应谨慎使用并用于轻型和任务导向的场景。
* 必须在单栏中显示内容，而且不能有多个导航层。
* 不得使用任务模块。
* 必须与会议阶段的中心对齐。

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![会议内对话框未对齐](~/assets/images/submission/validation-in-meeting-dialog-not-aligned.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* 在用户选择按钮或执行某个操作后必须关闭。

* **同框场景模式**：确保考虑以下场景生成体验最佳做法：
  * 所有图像都采用.png格式。
  * 所有图像组合在一起的最终程序包的分辨率不得超过 1920x1080。 分辨率为偶数。 要成功显示场景，需要此分辨率。
  * 最大场景大小为 10 MB。
  * 每个图像的最大大小为 5 MB。 场景是多个图像的集合。 限制是针对每个单独图像。
  * 根据需要选择 **透明**。 选中图像后，此复选框在右侧面板上可用。 重叠的图像必须标记为透明，以指示它们是场景中的重叠图像。

## <a name="notifications"></a>通知

> [!NOTE]
> 本部分符合 [Microsoft 商业市场策略号 1140.4.7](/legal/marketplace/certification-policies#114047-notification-apis)。

如果你的应用使用[Microsoft Graph 提供的活动信息提要 API](/graph/teams-send-activityfeednotifications)，请确保它遵守以下准则。

### <a name="general"></a>常规

* 应用配置中指定的所有通知触发器都必须正常工作。
* 通知必须根据为应用配置的支持语言进行本地化。
* 通知必须在用户操作后的五秒内显示。

### <a name="avatars"></a>头像

* 通知头像必须与应用的颜色图标匹配。
* 用户触发的通知必须包含用户的头像。

### <a name="spamming"></a>垃圾邮件

* 应用每分钟不得向用户发送超过 10 条通知。
* 机器人和活动信息提要不得触发重复通知。
* 通知必须为用户提供一些值，并且不能用于琐碎或不相关的事件。

### <a name="navigation-and-layout"></a>导航和布局

* 通知必须遵循 Teams 活动源布局和体验。
* 在选择通知时，必须将用户定向到 Teams 内部的相关内容。

## <a name="microsoft-365-app-compliance-program"></a>Microsoft 365 应用合规性

> [!NOTE]
> 本部分符合 [Microsoft 商业市场策略号 1140.6](/legal/marketplace/certification-policies#11406-publisher-attestation)。

Microsoft 365 应用合规性计划 旨在帮助企业通过评估应用程序的安全和合规性信息来评估和管理风险。 如果要向 Teams 商店发布一个应用程序，则必须完成该程序的以下几层:

* **发布者验证**: 可帮助管理员和终端用户了解到应用开发人员与 Microsoft 标识平台集成的真实性。 完成后，许可对话框 **和其他屏幕上** 将显示蓝色Azure Active Directory锁屏提醒。 有关详细信息，请参阅 [将你的应用标记为经过发布者验证](/azure/active-directory/develop/mark-app-as-publisher-verified)。  

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![发布者验证](~/assets/images/submission/validation-365-compliance-publisher-verification.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* **发布者证明**: 共享常规、数据处理以及安全性和合规性信息的过程，以帮助潜在客户在使用应用时做出明智的决定。

> [!NOTE]
> 如果之前未列出所提交的应用，则在应用进入 Teams 商店之前，无法正式完成发布者证明。 如果正在更新列出的应用，请在提交最新版本的应用之前完成发布者证明。

## <a name="advertising"></a>广告

> [!NOTE]
> 本部分符合 [Microsoft 商业市场策略编号1140.7](/legal/marketplace/certification-policies#11407-advertising)。

应用不得显示广告，包括动态广告、横幅广告和消息内广告。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [创建合作伙伴中心帐户](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)

## <a name="see-also"></a>另请参阅

* [分发应用](~/concepts/deploy-and-publish/apps-publish-overview.md)
* [准备应用商店提交](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [测试和调试应用](~/concepts/build-and-test/debug.md)
* [创建合作伙伴中心开发人员帐户](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)
