---
title: Microsoft Teams 商店验证指南
description: 了解如何增加应用通过 Microsoft Teams 应用商店提交过程的机会。 了解必需和建议的修补程序。 浏览验证准则。
author: heath-hamilton
ms.author: surbhigupta
ms.topic: reference
ms.localizationpriority: high
ms.openlocfilehash: 0a0151c72820baf1b6bd39ee00539cacbd3fa38b
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560864"
---
# <a name="microsoft-teams-store-validation-guidelines"></a>Microsoft Teams 商店验证指南

遵循这些准则会增加应用通过 Microsoft Teams 应用商店提交程序的机会。 这些特定于 Teams 的准则是对 Microsoft [商业市场认证策略](/legal/marketplace/certification-policies#1140-teams) 的补充，并经常更新以反映新功能、用户反馈和业务规则更改。

> [!NOTE]
>
> * 某些准则可能不适用于你的应用。 例如，如果应用不包含机器人，则可以忽略与机器人相关的准则。
> * 我们已将这些准则交叉引用到 Microsoft 商业认证策略，并添加了注意事项，其中包含验证过程中遇到的通过或失败情况的示例。
> * 某些准则标记为 *强制修复*。 如果你的应用提交不符合这些强制性准则，你将收到来自我们的失败报告，其中包含缓解措施。 只有在修复了问题后，应用提交才会通过 Microsoft Teams 应用商店验证。
> * Other guidelines are marked as *Suggested Fix*. For an ideal user experience, we suggest that you fix the issues, however, your app submission will not be blocked from publishing on the Teams store, if you choose not to fix the issues.

:::row:::
   :::column:::
      :::image type="icon" source="../../../../assets/icons/value-proposition.png" link="#value-proposition" border="false":::
   :::column-end:::
   :::column span="":::
     :::image type="icon" source="../../../../assets/icons/security.png" link="#security" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/function.png" link="#general-functionality-and-performance" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/package.png" link="#app-package-and-store-listing" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/saas-offer.PNG" link="#apps-linked-to-saas-offer" border="false":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/tab.png" link="#tabs" border="false":::
   :::column-end:::
   :::column:::
      :::image type="icon" source="../../../../assets/icons/bot.png" link="#bots-1" border="false":::
   :::column-end:::
   :::column span="":::
     :::image type="icon" source="../../../../assets/icons/messaging-extension.png" link="#message-extensions" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/task-module.png" link="#task-modules" border="false":::
   :::column-end:::
     :::column span="":::
      :::image type="icon" source="../../../../assets/icons/meeting.png" link="#meeting-extensions" border="false":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/notifications.png" link="#notifications" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/microsoft-365.png" link="#microsoft-365-app-compliance-program" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/advertising.png" link="#advertising" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/crypto-currency-based-apps-icon.png" link="#cryptocurrency-based-apps" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/app-functionality-icon.png" link="#app-functionality" border="false":::
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/mobile-experience-icon.png" link="#mobile-experience" border="false":::
   :::column-end:::
:::row-end:::

## <a name="value-proposition"></a>价值主张

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::本部分符合 [Microsoft 商业认证策略编号 1140.1](/legal/marketplace/certification-policies#11401-value-proposition-and-offer-requirements)，并为 Microsoft Teams 应用的开发人员提供有关其产品/服务价值主张的其他准则。

### <a name="app-name"></a>应用名称

[*强制修复*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::本部分符合 Microsoft [商业认证策略编号 1140.1.1](/legal/marketplace/certification-policies#114011-app-name)，并为开发人员提供有关命名其应用的其他准则。
<br></br>
<details><summary>展开以了解详细信息</summary>

应用程序的名称对用户如何在商店中发现它起着关键作用。 使用以下准则命名应用：

* 该名称必须包括与用户相关的术语。
* 使用开发人员姓名作为常用名词的前缀或后缀。 例如，**Contoso Tasks** 而不是 **Tasks**。
* 不得使用 **Teams** 或其他 Microsoft 产品名称，例如 Excel、PowerPoint、Word、OneDrive、SharePoint、OneNote、Azure、Surface 和 Xbox，这些名称可能错误地指示共同品牌或联合销售。 有关引用 Microsoft 软件产品和服务的详细信息，请参阅 [Microsoft 商标和品牌准则](https://www.microsoft.com/legal/intellectualproperty/trademarks/usage/general)。
* 不得复制商店中列出的应用程序的名称或商业市场中的其他报价。
* 不得包含亵渎或贬损性的词汇。 该名称也不得包括对种族或文化不敏感的语言。
* 必须是唯一的。 如果应用 (Contoso) 在 Microsoft Teams 应用商店和 Microsoft AppSource 中列出，并且要列出特定于 Contoso Mexico 等地理区域的另一个应用，则提交必须满足以下条件：
  * 在标题、元数据、首次响应应用体验和帮助部分中，强调应用的特定区域功能。 例如，标题必须是 Contoso Mexico。 应用标题必须与出自同一开发人员的现有应用明确区分，以避免最终用户混淆。
  * 在合作伙伴中心上传应用包时，在 **可用性** 部分中选择应用可用的正确的 **市场**。

* 应用名称不得以聊天、联系人、日历、呼叫、文件、活动、Teams、应用和帮助等核心 Teams 功能为主导。 应用名称可以缩短为聊天、联系人、日历、呼叫、文件、活动、Teams、应用和在左侧导航栏中安装的帮助。

* If your app is part of an official partnership with Microsoft, the name of your app must come first. For example, **Contoso Connector for Microsoft Teams**.

* 应用名称不得对 Microsoft 或 Microsoft 产品有任何引用。 除非应用与 Microsoft 正式合作，否则不要在应用名称中使用 **Teams**、 **Microsoft** 或 **App** 。 在此类实例中，应用名称必须先出现在对 Microsoft 的任何引用之前。 例如， **适用于 Microsoft Teams 的 Contoso 连接器**。

* 不要在命名中使用括号来包含 Microsoft 产品。

* 清单和 AppSource 中的开发人员名称必须相同。

* 提交的应用清单必须是生产清单。 因此，应用名称不能指示应用是预生产应用。 例如，应用名称不能包含 Beta、Dev、Preview 和 UAT 等字词。

 > [!TIP]
 > 你的应用在 Microsoft Teams 应用商店和 AppSource 上的品牌打造，包括你的应用名称、开发人员名称、应用图标、AppSource 屏幕截图、视频、简短说明和网站，除非你的应用是正式的 Microsoft 1P 产品/服务，否则不得模拟正式的 Microsoft 产品/服务。

</details>

### <a name="suitable-for-workplace-consumption"></a>适用于工作区使用

[*强制修复*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::本部分符合 Microsoft 商业认证策略号 [1140.1.2](/legal/marketplace/certification-policies#114012-workplace-appropriateness)、[100.8](/legal/marketplace/certification-policies#1008-significant-value) 和 [100.10](/legal/marketplace/certification-policies#10010-inappropriate-content)，并为开发人员提供了有关构建适合工作场所的应用的其他准则。
<br></br>
<details><summary>展开以了解详细信息</summary>

应用内容必须适用于一般工作场所使用，并遵循商业市场认证策略中列出的所有限制。 禁止与宗教、政治、赌博和长时间娱乐相关的内容。

你的应用必须增进团队协作、提高个人工作效率，或同时满足两者。 用于团队联系和社交的应用必须是协作的，并且专为多个参与者设计。 应用不得要求每次会话投入时间超过 60 分钟或影响工作效率。

</details>

### <a name="similar-platforms-and-services"></a>类似的平台和服务

[*强制修复*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::本部分符合 [Microsoft 商业认证策略号 1140.1.3](/legal/marketplace/certification-policies#114013-other-platforms-and-services)。

应用必须专注于 Teams 体验，并且应用内容或应用元数据中不应包括其他类似的基于聊天的协作平台或服务的名称、图标或图像，除非应用提供特定的互操作性。

### <a name="feature-names"></a>功能名称

按钮和其他 UI 文本中的应用功能名称不得使用为 Teams 和其他 Microsoft 产品保留的术语。 例如， **开始会议**、 **通话** 或 **开始聊天** 是 Microsoft 在 Microsoft Teams 中使用的功能名称。 如有必要，请包括应用名称以明确区分，例如 **启动 Contoso 会议**。

### <a name="authentication"></a>身份验证

[*强制修复*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::本部分符合 [Microsoft 商业认证策略 1140.1.4](/legal/marketplace/certification-policies#114014-access-to-services)，并为开发人员提供关使用外部服务为其应用进行身份验证的其他准则。

若要详细了解如何实施应用身份验证，请参阅 [Teams 中的身份验证](~/concepts/authentication/authentication.md)。
<br></br>
<details><summary>展开以了解详细信息</summary>

#### <a name="authenticating-with-external-services"></a>与外部服务进行身份验证

如果你的应用使用外部服务对用户进行身份验证，请遵循以下准则：

* **登录、注销和注册体验**:
  * 依赖于外部帐户或服务的应用必须提供清晰且简单的登录、注销和注册体验。
  * 当用户注销时，他们必须仅从应用中注销并保持登录到 Teams。
  * 依赖外部帐户或服务的应用必须为新用户提供一种前进的方法，以便注册或联系应用发布者，以了解有关服务以及获取服务访问权限的方法。
  前进方法必须在应用清单、AppSource 长描述以及应用首次运行体验 (机器人欢迎消息、选项卡设置或配置页面) 中可用。
  * 需要租户管理员完成一次性设置的应用必须强调对租户管理员配置应用的依赖性 (否则其他租户用户不能安装和使用应用)。
  依赖性必须在应用清单、AppSource 长描述、所有首次运行体验接触点 (机器人欢迎消息、选项卡设置或配置页面)、被视为机器人响应、撰写扩展或静态选项卡内容中的必要部分的帮助文本中强调。
  
* **内容共享体验**: 需要通过外部服务进行身份验证以便在 Teams 频道中共享内容的应用，必须在帮助文档 (或类似资源) 中清楚地说明用户如何断开连接或取消共享内容 (如果外部服务支持此功能)。 这并不意味着你的 Teams 应用中必须有取消共享内容功能。

</details>

## <a name="security"></a>安全性

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::本部分符合 [Microsoft 商业认证策略号 1140.3](/legal/marketplace/certification-policies#11403-security)。

### <a name="financial-information"></a>财务信息

[*强制修复*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: 本部分与 [Microsoft 商业认证策略编号 1140.3.1](/legal/marketplace/certification-policies#114031-financial-transactions) 内联，提供有关在 Teams 界面中传输财务信息的指导，并通知开发人员其 Teams 应用的移动 (Android 和 iOS) 版本的受限付款方案。
<br></br>
<details><summary>展开以了解详细信息</summary>

应用不得要求用户在 Teams 界面中付款，并通过机器人界面将财务信息传输给用户。

:::image type="content" source="../../../../assets/images/submission/validation-financial-information-1.png" alt-text="validation-financial-info":::

只有在用户同意使用应用之前，在使用条款、隐私策略、配置文件页面或网站中披露外部付款服务，你才能提供安全外部付款服务的链接。

请勿通过应用为 [常规策略编号 100.10 不适当的内容](/legal/marketplace/certification-policies#10010-inappropriate-content)禁止的商品或服务提供付款。

在 iOS 或 Android 版本的 Teams 上运行的应用必须遵循以下准则:

* 应用不得包括旨在向用户推销支付版本的应用内购买、试用优惠或 UI，或指向可以购买其他内容、应用程序或加载项的联机应用商店的链接。

    :::image type="content" source="../../../../assets/images/submission/validation-financial-information-in-app-purchase.png" alt-text="validation-financial-info-in-app-purchase":::

    :::image type="content" source="../../../../assets/images/submission/validation-financial-information-online-stores.png" alt-text="validation-online-store":::

* 如果应用需要帐户，则用户必须能够免费注册帐户。 禁止使用 **免费** 或 **免费帐户** 的术语。
* You can determine whether an account is active indefinitely or for a limited time. When the account expires the app must not show UI, text, or links indicating the need to pay.
* 应用的隐私策略和使用条款页面必须不含任何与商业相关的 UI 或链接。

</details>

### <a name="bots"></a>机器人

[*强制修复*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::本部分符合 [Microsoft 商业市场策略号 1140.3.2](/legal/marketplace/certification-policies#114032-bots-and-messaging-extension)。
<br></br>
<details><summary>展开以了解详细信息</summary>

对于使用 Microsoft Azure 机器人服务的应用（如机器人和消息扩展），必须遵循 Microsoft [在线服务条款](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46)中定义的所有要求。

机器人必须始终请求上传文件的权限并显示确认消息。

:::image type="content" source="../../../../assets/images/submission/validation-bot-confirmation-message.png" alt-text="validation-bot-confirmation":::

</details>

### <a name="external-domains"></a>外部域

[*强制修复*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::本部分符合 [Microsoft 商业市场策略号 1140.3.3](/legal/marketplace/certification-policies#114033-external-domains)，并提供了有关在 `validDomains` 清单属性中使用受限域的开发人员准则。
<br></br>
<details><summary>展开以了解详细信息</summary>

Don't include domains outside of your organization's control (including wildcards) and tunneling services in your app's domain configurations. The following exceptions include:

* 如果应用使用 Azure 机器人服务的 OAuthCard，则必须将 `token.botframework.com` 作为有效的域包含在内，否则 **登录** 按钮将无法工作。
* 如果应用依赖于 SharePoint，则可以使用 `{teamSiteDomain}` 上下文属性将关联的根 SharePoint 站点作为有效域包含。
* 请勿将顶级域（如 **.com**、 **.in** 和 **.org** ）用作有效域。 [*强制修复*]

* 请勿使用 **.onmicrosoft.com，或者** 将 **onmicrosoft** 不在控制之下的有效域。 但是，即使域包含通配符，也可以将 **yoursite.com** 用作控制你的 **网站** 所在的有效域。 [*强制修复*]

* 如果应用是在 Microsoft Power Platform 上构建的 PowerApp，则必须将 *apps.powerapps.com* 作为有效域包括在内，使应用能够在 Teams 中访问和正常运行。

</details>

### <a name="sensitive-content"></a>敏感内容

[*强制修复*]

你的应用不得将敏感数据（如信用卡、财务付款详细信息、健康情况、接触者追踪或其他个人身份信息 （PII））发布给不应该查看该内容的受众。

应用必须在将任何文件或可执行文件 (.exe) 下载到用户计算机或环境中之前警告用户。

## <a name="general-functionality-and-performance"></a>常规功能和性能

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::本部分符合 [Microsoft 商业市场策略号 1140.4](/legal/marketplace/certification-policies#11404-functionality)。

* 对于管理员和现有用户来说，前向指导是必需的。 可以添加前向指南作为超链接来注册、入门、联系我们、帮助链接或电子邮件。
* 在应用功能下调用帐户依赖项或限制不是必需的，但必须将其添加到清单长说明和 AppSource 应用一览中。
* 必须为新用户调用租户管理员的任何依赖项。 如果没有依赖项，则必须提供注册、联系我们、入门链接或电子邮件。

### <a name="launching-external-functionality"></a>正在启动外部功能

[*强制修复*]

应用不得将用户带出 Teams 的核心用户场景。 应用内容和交互必须在 Teams 的功能中发生，如机器人、自适应卡片和任务模块。
<br>
</br>

<details><summary>展开以了解详细信息</summary>

* 应在 Teams 应用内链接用户，而不是链接到外部网站或应用。 对于需要外部功能的情况，你的应用必须获得明确的用户权限才能启动该功能。

* 启动外部功能的按钮 UI 文本必须包含指示用户已退出 Teams 实例的内容。 例如，包括如下文本，**由此转到 Contoso.com** 或 **在 Contoso.com 中查看**。

* 添加 **弹出** 图标，让用户知道他们正在 Teams 外部导航。 可以使用链接右侧的弹出图标 :::image type="icon" source="../../../../assets/icons/pop-out-icon.png" ::: 。

* 如果无法添加 **弹出** 图标，可以实现以下任一选项，让用户知道他们正在 Teams 外部导航：
  * 在自适应卡片中添加一个说明，指出当用户 **选择使用此应用获取帮助** 时，它会将用户带出 Teams。
  * 添加间隙对话框。

</details>

### <a name="compatibility"></a>兼容性

[*强制修复*]

应用必须能够在以下操作系统和浏览器的最新版本上正常运行:

* Microsoft Windows
* macOS
* Microsoft Edge
* Google Chrome
* iOS
* Android

你的应用必须在不受支持的浏览器和操作系统上显示得体的失败消息。

### <a name="response-time"></a>答复时间

[*强制修复*]

Teams 应用必须在合理的时间范围内响应，或显示正在加载或键入的指示、消息或警告。

* 选项卡必须在两秒钟内响应，或显示正在加载的消息或警告。
* 机器人必须在两秒内响应用户命令或显示键入指示器。
* 消息扩展必须在两秒钟内响应用户命令。
* 通知必须在用户操作后两秒钟内显示。

## <a name="app-package-and-store-listing"></a>应用包和应用商店列表

[*强制修复*]

必须正确设置应用包的格式，并包含所有必需的信息和组件。

> [!TIP]
>
> * 必须确保提供的测试帐户或测试环境永久有效，即在商业市场中运行应用之前。
> * 必须包含以下详细的测试说明来验证应用提交：
>
>   * 在应用依赖于外部帐户进行身份验证的情况下，**配置应用测试帐户的步骤**。
>   * Teams 内核心工作流的 **预期应用行为** 摘要。
>   * **清楚地描述** 应用长描述和相关材料中的功能、特性和可交付结果的限制、条件或例外情况。
>   * 在验证应用提交时，为测试人员 **强调注意事项**。
>   * **使用虚拟数据预填充测试帐户**，以有助于测试。
>   * 如果要提供测试帐户，请确保启用第三方集成。 此外，禁用双因素或多重身份验证。

### <a name="app-manifest"></a>应用部件清单

[*强制修复*]

Teams 应用清单定义应用的配置。

* 清单必须符合公开发布的清单架构。 有关详细信息，请参阅 [清单参考](~/resources/schema/manifest-schema.md)。 请勿使用清单的预览版本提交应用。
* 如果应用包括机器人或消息扩展，则应用清单中的详细信息必须与机器人框架元数据保持一致，包括机器人名称、徽标、隐私策略链接和服务条款链接。
* 如果应用使用 Azure Active Directory 进行身份验证，请在清单中包括 Microsoft Azure Active Directory (Azure AD) 应用程序（客户端）ID。 更多相关信息，请参阅 [清单参考](~/resources/schema/manifest-schema.md#webapplicationinfo)。

### <a name="uses-of-latest-manifest-schema"></a>使用最新清单架构

* 如果应用使用单一登录 (SSO) ，则必须在清单中声明Microsoft Azure Active Directory (Azure AD) ID 以进行用户身份验证。 [*强制修复*]

* 必须使用公开发布的清单架构。 可以更新应用包以使用清单架构 1.10 或更高版本的公共版本。 [*强制修复*]

* 提交应用更新时，只需增加应用版本号。 更新后的应用的应用 ID 必须与已发布的应用的应用 ID 匹配。 [*强制修复*]

* 应用包中存在其他文件是不能接受的。 [*强制修复*]

* 在清单文件架构和其他语言清单架构中，版本号必须相同。 [*强制修复*]

* 必须使用 Teams 清单架构版本 1.5 或更高版本来本地化应用。 若要在 manifest.json 文件中使用应用架构版本 1.5 或更高版本，请将属性更新 `$schema` 为 1.5 或更高版本。 `manifestVersion`在这种情况下，将属性更新为`$schema`版本 (1.5) 。 [*强制修复*]

* 添加、更新或删除现有功能、添加或删除清单或合作伙伴中心元数据时，必须增加应用版本号并在合作伙伴中心帐户中提交新应用清单以进行验证。

* 版本字符串必须遵循语义版本控制规范 (SemVer) 标准 (MAJOR。小。PATCH) 。 [*强制修复*]

* 如果应用要求管理员在 Teams 管理中心查看权限并授予许可，则必须在清单中声明 `webapplicationinfo` 。 如果`webapplicationinfo`未在清单中声明，则 Teams 管理中心中应用 **的“权限**”页显示为 **...**

* 作为 Teams 应用认证的一部分，必须提交应用清单的生产版本。 [*强制修复*]

* 建议在清单中声明 Microsoft 合作伙伴网络 (MPN) ID。 MPN ID 可帮助标识生成应用的合作伙伴组织。 [*建议修复*]

### <a name="app-icons"></a>应用图标

[*强制修复*]

图标是用户在浏览 Teams 应用商店时看到的主要元素之一。
<br></br>
<details><summary>展开以了解详细信息</summary>

图标必须传达应用的品牌和用途，同时遵循以下要求：

* 应用包必须包含两个 PNG 版本的应用图标：彩色图标和大纲图标。
* 图标的颜色版本必须为 192x192 像素。 图标符号可以是任何颜色，但必须位于纯色或完全透明的方形背景上。
* 以下情况中将显示图标的轮廓版本：
  * 你的应用正在使用并 **托管** 在 Teams 左侧应用栏上。
  * 当用户固定应用的消息扩展时。

* 轮廓版本必须为 32x32 像素，并且可以是白色（背景透明）或透明（白色背景）。 图标不得在符号周围有任何额外填充。

* 你的应用包必须包含大小正确且格式正确的图标。 图标必须与应用商店列表元数据中的信息匹配。

有关详细信息，请参阅 [图标准则](~/concepts/build-and-test/apps-package.md#app-icons)。

</details>

### <a name="app-descriptions"></a>应用说明

你的应用必须具有简短且较长的说明。 应用配置和合作伙伴中心中的说明必须相同。

:::image type="content" source="../../../../assets/images/submission/validation-app-description-adequete-information.png" alt-text="图形显示 Teams 应用中充分应用说明的示例。":::

:::image type="content" source="../../../../assets/images/submission/validation-app-description-inadequete.png" alt-text="图形显示应用说明不足的失败方案。":::

<br></br>
<details><summary>展开以了解详细信息</summary>

说明不得直接或通过影射贬损其他品牌（Microsoft 所有或其他）。 确保说明不包含无法证实的声明。 例如，**保证效率提高 200%**。

* 应用说明不得包含比较营销信息。 例如，不要在产品/服务一览中使用竞争对手徽标或商标，包括引用竞争产品/服务或市场的标签或其他元数据。 [*强制修复*]

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-comparitive-marketing-fail.png" alt-text="图形显示应用说明中比较营销信息的示例。":::

* 超链接联系人详细信息、入门、帮助或注册应用说明。

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-contact-deatils-hyperlinked.png" alt-text="图形显示应用说明中超链接的联系人详细信息示例。":::

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-contact-deatils-not-hyperlinked.png" alt-text="图形显示在应用说明中未超链接的联系人详细信息示例。":::

* 应用说明必须标识预期受众，简要明确地解释其唯一和独特的价值，识别受支持的 Microsoft 产品和其他软件，并包含其使用的任何先决条件或要求。 在客户获取产品/服务之前，必须清楚地描述功能、功能和可交付结果的任何限制、条件或例外情况，如一览和相关材料中所述。 声明的功能必须与产品/服务的核心函数和说明相关。 [*强制修复*]

* 如果更新应用名称，请将旧应用名称替换为清单、AppSource 和适用情况中产品/服务元数据中的新应用名称。 [*强制修复*]

* 限制和帐户依赖项必须在清单应用说明、AppSource 和合作伙伴中心中注明。 例如：
  * 企业帐户
  * 付费订阅
  * 另一个许可证或帐户
  * 语言
  * 公共交换电话网络 (PSTN) 拨号
  * 区域依赖项
  * 预订翻译或实时代理的提前时间
  * 基于角色的功能
  * 对本机应用的依赖关系

  :::image type="content" source="../../../../assets/images/submission/validation-app-description-limitations-calledout-pass.png" alt-text="图形显示应用说明中所述的限制示例。":::
  
  :::image type="content" source="../../../../assets/images/submission/validation-app-description-limitations-not-calledout-fail.png" alt-text="图形显示应用说明中未注明的限制示例。":::

* 如果应用支持特定区域或地理位置，则必须在该产品/服务的清单、合作伙伴中心和 AppSource 中的应用说明中标出该特定区域依赖项。

* 如果需要引用 Teams，请将应用列表中的第一个引用写入 Microsoft Teams。 以后的引用可以缩短为 Teams。

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-teams-reference-pass.png" alt-text="图形显示在应用说明中正确引用 Teams 的示例。":::

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-teams-reference-fail.png" alt-text="图形显示应用说明中对 Teams 的引用不正确的示例。":::

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

* 确保应用说明与 Teams 应用中可用的功能匹配。 对 Teams 应用外部工作流的任何引用都必须受到限制，并且必须在 Teams 应用功能中明确强调。

* 包括帮助或支持链接。

* 请参阅 **Microsoft 365**，而不是 **Office 365**。

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

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-microsoft-abbreviated.png" alt-text="图形显示在应用说明中首次将 Microsoft 缩写为 MS 或 MSFT 的示例。":::

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-microsoft-not-abbreviated.png" alt-text="图形显示在应用说明中首次不将 Microsoft 缩写为 MS 或 MSFT 的示例。":::

* 指示应用是来自 Microsoft 的产品/服务，包括使用 Microsoft 的标语或标志行。

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-offering-from-microsoft.png" alt-text="图形显示如何在应用说明中指示 Microsoft 产品/服务的示例。":::

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-no-offering-indication-from-microsoft.png" alt-text="显示如何编写应用说明而不使用 Microsoft 标语和标记的示例的图形。":::

* 除非你是经认证的 Microsoft 合作伙伴，否则请使用以下语言:
  * **“ ...通过...认证”**
  * **“...由...提供支持”**
* 包括拼写错误、语法错误。
* 不必要地将整个清单或 AppSource 长描述或应用内容大写。

   :::image type="content" source="../../../../assets/images/submission/validation-long-description-typos-pass.png" alt-text="图形显示应用长描述的示例，不带错误。":::

   :::image type="content" source="../../../../assets/images/submission/validation-long-description-typos-fail.png" alt-text="图形显示具有拼写错误和错误的应用长描述示例。":::

* 包括指向 AppSource 的链接。

  :::image type="content" source="../../../../assets/images/submission/validation-app-description-link-to-appsource.png" alt-text="图形显示在应用长描述中链接到 AppSource 的故障方案的示例。":::

* 作出未经验证的声明。 例如，最好、顶级和排名，除非附带声明的来源。
* 将产品/服务与其他市场产品/服务进行比较。

</details>

### <a name="screenshots"></a>屏幕截图

屏幕截图提供了应用的突出视觉预览，以补充应用名称、图标和说明。
<br></br>
<details><summary>展开以了解详细信息</summary>

请记住以下事项：

* 每个列表最多可以有五个屏幕截图。
* 支持的文件类型包括 PNG、JPEG 和 GIF。
* 尺寸必须为 1366x768 像素。
* 最大尺寸为 1，024 KB。

**应做:**

* Focus on your app's capabilities. For example, how people can communicate with your bot.
* 包括能准确代表应用程序的内容。
* 谨慎使用文本。
* 使用反映品牌和包含营销内容的颜色作为屏幕截图的边框。
* 使用清晰且包含清晰可读文本的高分辨率屏幕截图。 [*强制修复*]
* 使用能够准确描述应用实际 UI 的模型，使最终用户受益。 [*强制修复*]
* 在应用的市场一览中至少提供三个屏幕截图。
* 如果 Teams 应用可扩展到其他 Microsoft 365 中心，则提供的屏幕截图必须描述其他 Microsoft 365 中心的应用功能。
* 至少一个屏幕截图必须描述移动设备上的应用功能。
* 建议在屏幕截图中提供标题，让用户清楚地了解应用功能。

**不应做:**

* 包括不准确地反映应用实际 UI 的模型，例如显示在 Teams 外部使用的应用。

> [!TIP]
>
> * 视频可能是传达用户必须使用你的应用的原因的最有效方法。 用户也将在列表中首先看到视频。
> * 如果选择在应用列表中提供视频，则在合作伙伴中心提交视频链接之前，必须关闭 YouTube 或 Vimeo 设置中的广告。 应用列表中提供的视频持续时间不得超过 90 秒，并且必须仅描述应用功能以及与 Microsoft Teams 的集成。 有关详细信息，请参阅 [创建商店列表视频](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#create-a-video)。

</details>

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

[*强制修复*]

应用的支持 URL 不得要求身份验证。 例如，用户不得登录来联系你。
<br></br>
<details><summary>展开以了解详细信息</summary>

支持 URL 必须包含你的联系方式详细信息或供用户提出支持票证的方式。 例如，如果你的支持 URL 托管在 GitHub 上，GitHub 页面必须处于你的所有权下，并且必须包括你的联系方式详细信息或供用户提出支持票证的方式。

:::image type="content" source="../../../../assets/images/submission/validation-supportlinks-authentication.png" alt-text="validation-support-links-auth":::

</details>

### <a name="localization"></a>本地化

[*强制修复*]

* 如果应用支持本地化，则应用包必须包含基于 Teams 语言设置显示的语言翻译文件。 该文件必须符合 Teams 本地化架构。 有关详细信息，请参阅 [Teams 本地化架构](~/concepts/build-and-test/apps-localization.md)。

* 应用元数据内容在和其他本地化语言中 `en-us` 必须相同。 [*强制修复*]

* 支持的语言必须显示在 AppSource 应用说明中。 例如，此应用以 X (X= 本地化语言) 提供。 [*强制修复*]

* 如果用户的客户端设置与任何其他语言都不匹配，则默认语言将用作最终回退语言。 `localizationInfo`使用应用程序支持的正确默认语言更新属性。 [*强制修复*]

* `localizationInfo`使用应用程序支持的正确默认语言更新属性，或添加清单和合作伙伴中心长短说明的本地化内容。 [*强制修复*]

## <a name="apps-linked-to-saas-offer"></a>链接到 SaaS 产品/服务的应用

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::本部分符合 [Microsoft 商业市场策略号 1140.5](/legal/marketplace/certification-policies?branch=pr-en-us-5673)。 如果要生成链接到 SaaS 产品/服务的 Teams 应用，请确保它遵守这些准则。
<br></br>
<details><summary>常规</summary>

* ISV 必须支持相同租户中的多个用户 (订阅者) 管理自己的订阅，并将许可证分配给租户中的用户。
* 产品/服务必须满足链接到 SaaS 产品/服务的 Teams 应用的所有[技术要求](/microsoftteams/platform/concepts/deploy-and-publish/appsource/prepare/include-saas-offer)。
* 链接到 SaaS 产品/服务的 Teams 应用必须满足[1000 服务型软件 (SaaS)](/legal/marketplace/certification-policies#1000-software-as-a-service-saas) 中定义的所有要求。
* 清单文件中提到的 `subscriptionOffer` 详细信息必须正确。 在应用清单中，使用值 `publisherId.offerId` 添加或更新节点 `subscriptionOffer`。 例如，如果你的发布者 ID 是 `contoso1234`，并且你的产品/服务 ID 是 `offer01`，你在应用清单中指定的值必须是 `contoso1234.offer01`。
* 链接到 SaaS 产品/服务的 Teams 应用必须在 AppSource 中已推出，并且不接受预览产品/服务通过应用商店批准。

</details>

</br>
<details><summary>产品/服务元数据</summary>

* 产品/服务元数据必须与 Teams 清单、AppSource 中的 Teams 应用列表和 AppSource 中的 SaaS 产品/服务匹配。
* Teams 应用和 SaaS 产品/服务必须来自同一发布者或开发人员。 应用清单中引用的 SaaS 产品/服务必须属于将 Teams 应用提交给商业市场时相同的发布者。
* 由于你提交的产品/服务是链接到 SaaS 产品/服务的 Teams 应用，因此你必须在产品/服务列表的合作伙伴中心产品设置部分中将 **其他购买** 选择为 **是，我的产品需要购买服务或提供其他应用内购买**。
* 计划说明和定价详细信息必须为用户提供足够的信息，以清楚地了解产品/服务列表。
* 必须在计划说明中准确指出所提供的功能的任何限制、对其他服务的依赖和例外。
* 链接到 SaaS 产品/服务的 Teams 应用旨在支持按姓名和用户分配许可证。 有时，SaaS 产品/服务是使用其他方法构建的，或者具有专门的购买流。 你必须在应用元数据和订阅计划详细信息中清楚地提及构建方法和购买流的详细信息。
* SaaS 产品/服务必须为购买流的所有适用状态中的所有用户提供消息和准则。

</details>
</br>

<details><summary>SaaS 产品/服务主页和许可证管理</summary>

* 向订阅者提供有关如何使用产品的介绍。
* 允许订阅者分配许可证。
* 提供不同的方式来参与对问题的支持，例如常见问题解答、知识库和电子邮件。
* 验证用户以确保他们尚未通过其他用户分配许可证。
* 许可证分配后通知用户。
* 指导用户了解如何将应用添加到 Teams 并通过 Teams 聊天机器人或电子邮件入门。

</details>
</br>

<details><summary>可用性和功能</summary>

* 成功购买和分配许可证后，必须提供以下内容：
  * 用户订阅计划功能的访问权限。
  * 用户订阅计划的价值增加和显著优势。
  * 从 Teams 应用中，提供指向 SaaS 应用程序主页的链接，以便订阅者将来管理许可证。

</details>
</br>

<details><summary>配置和测试 SaaS 应用程序</summary>

如果出于测试目的设置应用很复杂，请提供端到端功能文档、链接的 SaaS 产品/服务配置步骤以及许可证和用户管理说明，作为 *认证说明* 的一部分。

> [!TIP]
> 你可以添加一个有关应用和许可证管理工作原理的视频，以帮助团队进行测试。

</details>

## <a name="tabs"></a>选项卡

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::本部分符合 [Microsoft 商业市场策略号 1140.4.2](/legal/marketplace/certification-policies#114042-tabs)。
如果你的应用包含一个选项卡，请确保它遵守这些准则。
> [!TIP]
> 有关创建高质量应用体验的详细信息，请参阅 [Teams 设计指南](~/tabs/design/tabs.md)。

</br>
<details><summary>安装</summary>

* 选项卡设置 **不得终止** 新用户。 提供有关如何完成操作或工作流的信息。 [*强制修复*]

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-new-user.png" alt-text="图形显示设置上带有死胡同的 Tab 示例。":::

* 用户不得在 Teams 内部保留选项卡配置体验，以在 Teams 外部创建内容，然后返回 Teams 以固定内容。 选项卡配置屏幕必须说明配置值以及如何配置。 [*强制修复*]

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-profile-name.png" alt-text="validation-tabs-set-up-profile-name":::

* Tab configuration screen must not embed an entire website. Keep your configuration experience focused. For example, if you're building a project management app that lets users configure a project in a channel, keep the tab configuration screen focused on allowing the user to select a project from your app to configure in the channel. [*Mandatory Fix*]

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-configuration-experience.png" alt-text="validation-tabs-setup-configuration-exp":::

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-configuration-screen.png" alt-text="validation-tabs-set-up-configuration-screen":::

* 需要用户在配置选项卡时输入 URL 的应用必须：
  * 为用户获取或生成 URL 提供适当的前进指南。 [*强制修复*]
  * 根据应用说明检查与应用的功能相关或适合的 URL。 [*强制修复*]

    :::image type="content" source="../../../../assets/images/submission/validation-tab-configuration-way-forward-url-pass.png" alt-text="屏幕截图显示了选项卡配置的示例，其中提供了用户生成 URL 的前进方向。":::
  
    :::image type="content" source="../../../../assets/images/submission/validation-tab-configuration-way-forward-url-fail.png" alt-text="屏幕截图显示了选项卡配置的示例，而用户无需进一步生成 URL。":::

* 将配置屏幕中的信息与我们联系，而不是纯文本，以帮助用户联系你以获得支持要求。 [*强制修复*]

* 为了实现无缝的首次运行用户体验，建议在配置屏幕上超链接支持 URL 或电子邮件。 [*建议修复*]

</details>
</br>

<details><summary>视图</summary>

* The sign in screen area must not use large logos. [*Mandatory Fix*]

    :::image type="content" source="../../../../assets/images/submission/validation-views-applogin.png" alt-text="validation-views-app-login":::

* 可以通过跨多个选项卡进行分解来简化内容。

    :::image type="content" source="../../../../assets/images/submission/validation-views-multiple-tabs.png" alt-text="val-views-multiple-tabs":::

* 选项卡不应具有重复的标题。 从 I 帧中删除重复徽标，因为 Tab 框架已显示应用图标和名称。 [*建议修复*]

    :::image type="content" source="../../../../assets/images/submission/validation-views-no-duplicate-header-logo.png" alt-text="图形显示一个没有重复标头和徽标的选项卡示例。":::

    :::image type="content" source="../../../../assets/images/submission/validation-views-duplicate-header-logo.png" alt-text="图形显示具有重复标头和徽标的选项卡的示例。":::

</details>
</br>

<details><summary>导航</summary>

下面是导航准则：

* 选项卡不得提供与主要 Teams 导航冲突的导航。 如果在选项卡中提供左侧导航，则它不能只包含图标或具有堆叠文本的图标。 它不能是具有查看带有堆叠文本的图标的选项的可折叠的栏 (模仿 Teams 导航栏)。 包括带内联文本的图标或仅文本，或使用汉堡菜单而不是选项卡左栏。 [*强制修复*]

使用 [基本](~/concepts/design/design-teams-app-basic-ui-components.md) 和 [高级](~\concepts\design\design-teams-app-advanced-ui-components.md) Fluent UI 组件设计应用。

:::image type="content" source="../../../../assets/images/submission/validation-navigation-static-tab.png" alt-text="图形显示与主要 Teams 导航不冲突的选项卡中的导航示例。":::

:::image type="content" source="../../../../assets/images/submission/validation-navigation-left-navigation.png" alt-text="图形显示左侧导航轨与主要 Teams 导航冲突的示例。":::

* 在左侧导轨中使用工具栏的选项卡必须从 Teams 左侧导航留出 20 像素的间距。 [*强制修复*]

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-spacing-between-toolbar.png" alt-text="validation-nav-spacing-between-toolbar":::

* 选项卡中的辅助页和第三级页必须在 L2) 的二级 (打开，第三级 (L3) 主选项卡区域的视图，该视图通过痕迹痕迹或左侧导航进行导航。 还可以使用以下组件来帮助选项卡中的导航：
  * 后退按钮
  * 页眉
  * 汉堡菜单

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-improper-navigation-leveles.png" alt-text="显示具有多个导航级别的会议内对话的示例的屏幕截图。":::

* 选项卡中的深层链接不能链接到外部网页，而应链接到 Teams 内部的某个位置。 例如，任务模块或其他选项卡。 [*强制修复*]

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-view-button-not-linked-static-tab.png" alt-text="validation-nav-view-button-not-linked-static-tab":::

* 选项卡不得允许用户导航到 Teams 外部以获得核心应用体验。 对于非核心工作流，选项卡可以重定向到 Teams 外部。 例如，提出支持票证。 [*强制修复*]

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-core-workflow-within-configuration.png" alt-text="validation-nav-core-workflow-within-configuration":::

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-core-workflow-redirects-outside.png" alt-text="validation-nav-core-workflow-redirects-outside":::

* 会议内选项卡中不能显示水平滚动。[*强制修复*]

* 应用中使用的会议内对话框不得允许水平滚动。 请谨慎使用会议内对话框，并针对轻型和面向任务的方案使用对话框。 可以在受支持的大小范围内指定会议内对话框的 I 帧宽度，以考虑不同的方案。 [*强制修复*]
* 应用中使用的任务模块不得允许水平滚动。 任务模块允许你选择不同的大小，使内容响应，而无需水平滚动。 如果需要，可以使用全屏 UI 组件 (阶段视图来显示 Web 内容) 以完成工作流，而无需水平滚动。 [*强制修复*]

* 如果整个选项卡画布是可滚动的，则不允许在任何范围内的个人聊天、频道和会议中详细信息选项卡中显示水平滚动，除非选项卡使用具有固定 UI 元素的无限画布。 [*强制修复*]

   :::image type="content" source="../../../../assets/images/submission/validation-horizontal-scroll-allowed-scenarios.png" alt-text="图形显示移动中允许水平滚动的所有方案的示例。":::

   :::image type="content" source="../../../../assets/images/submission/validation-horizontal-scroll-allowed-kanban.png" alt-text="图形显示看板中水平滚动的示例。":::

   :::image type="content" source="../../../../assets/images/submission/validation-horizontal-scroll-list-view-components.png" alt-text="图形显示包含许多组件的列表视图示例。":::

   :::image type="content" source="../../../../assets/images/submission/validation-horizontal-scroll-fixed-board.png" alt-text="图形显示白板中水平滚动的示例，其中包含无限画布和固定板。":::

   :::image type="content" source="../../../../assets/images/submission/validation-horizontal-scroll-in-list-view.png" alt-text="图形显示列表视图中水平滚动的示例。":::

* 自适应卡片中的水平滚动不得存在于 Teams 中。 [*强制修复*]

* 在选项卡中用于导航的底轨不得与 Teams 本机移动应用导航冲突。 [*强制修复*]

  :::image type="content" source="../../../../assets/images/submission/validation-tab-bottom-rail-conflicts-with-teams-mobile.png" alt-text="图形显示与 Teams 本机移动应用导航冲突的选项卡的示例。":::

</details>
</br>

<details><summary>可用性</summary>

* 选项卡必须提供价值，而不仅仅是托管现有网站。 [*强制修复*]

    :::image type="content" source="../../../../assets/images/submission/validation-usability-app-provides-workflows.png" alt-text="图形显示了一个应用的示例，该应用的工作流对团队中的频道成员很有价值。":::

    :::image type="content" source="../../../../assets/images/submission/validation-usability-website-i-framed.png" alt-text="图形显示在 I 帧中包含整个网站且没有任何后退选项的应用的示例。":::

* 内容不得在选项卡中截断或重叠。

    :::image type="content" source="../../../../assets/images/submission/validation-usability-content-truncation.png" alt-text="validation-usability-content-truncations":::

* 用户必须能够撤消其在选项卡中的最后一个操作。

* 个人上下文中的选项卡可以从应用的共享实例中聚合内容。 例如，具有可配置选项卡的项目管理应用程序（允许频道成员在看板卡上对项目进行注释）必须聚合此内容并显示在个人应用程序中。 [*建议修复*]

* 选项卡必须响应 Teams 主题。 当用户更改主题时，应用的主题必须反映所选内容。

    :::image type="content" source="../../../../assets/images/submission/validation-usability-responsive-tabs.png" alt-text="图形显示在 Teams 中响应主题的选项卡的示例。":::

    :::image type="content" source="../../../../assets/images/submission/validation-usability-unresponsive-tabs.png" alt-text="图形显示 Tab 对 Teams 中的主题没有响应的示例。":::

* 选项卡必须尽可能使用 Teams 样式组件，例如 Teams 字体、类型渐变、调色板、网格系统、动作、语音音调。 有关详细信息，请参阅[选项卡设计指南](/microsoftteams/platform/tabs/design/tabs)。 [*建议修复*]

    :::image type="content" source="../../../../assets/images/submission/validation-usability-app-uses-diff-font.png" alt-text="屏幕截图显示了带有校准字体而不是本机 Teams 字体的选项卡的示例。":::

* 如果你的应用功能需要更改设置，请包含一个 **设置** 选项卡。 [*建议修复*]
* 选项卡必须遵循 Teams 交互设计，例如页面内导航、位置和对话的使用、信息层次结构。 有关详细信息，请参阅 [Microsoft Teams Fluent UI 工具包](~/concepts/design/design-teams-app-basic-ui-components.md)。

* 选项卡体验必须在移动设备（Android 和 iOS）上完全响应。

   > [!TIP]
   >
   > * 将个人机器人与个人选项卡一起包含在一起。
   > * 允许用户从其个人选项卡中共享内容。

* Tab 不能包含完全阻碍或阻碍选项卡内工作流的元素。例如，无法最小化选项卡内的机器人。

   :::image type="content" source="../../../../assets/images/submission/validation-tab-elements-impede-workflow.png" alt-text="图形显示一个选项卡示例，其中包含阻碍选项卡内工作流的元素。":::

* 选项卡不能具有损坏的功能。 产品/服务必须是一个可用的软件解决方案，并且必须提供一览和其他相关材料中所述的功能、功能和可交付结果。 [*强制修复*]

* 如果选项卡包含页脚，请确保从页脚中删除与应用功能无关的所有链接。

</details>
</br>

<details><summary>范围选择</summary>

* 可配置选项卡的登录页中的内容不得被限制为供个人使用，并不得包含个人内容，如"**我的任务**"或"**我的仪表板**"。

   :::image type="content" source="../../../../assets/images/submission/validation-configurable-tab-content-personal-scope.png" alt-text="图形显示可配置选项卡中包含个人范围的内容示例，例如“我的任务”或“我的仪表板”。":::

* 配置体验后，登陆页必须显示整个团队的协作视图。

* 如果你的应用需要为用户提供个人范围视图以提高效率或工作场所的工作效率，请使用筛选视图、个人应用的深层链接，或导航到可配置选项卡内的 L2 或 L3 视图，并在使所有用户的登录页面保持上下文相同。

* 对于频道的所有成员，可配置选项卡的登录页面中的内容必须上下文相同。

    :::image type="content" source="../../../../assets/images/submission/validation-usability-configurable-tab-personal-info.png" alt-text="图形显示可配置选项卡的登陆页中内容的示例，其上下文与所有成员的上下文不同。":::

* 可配置选项卡必须具有重点功能。

    :::image type="content" source="../../../../assets/images/submission/validation-usability-configurable-nested-tabs.png" alt-text="validation-usability-configurable-nested-tab":::

</details>
<br/>

## <a name="bots"></a>机器人

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::本部分符合 [Microsoft 商业市场策略号 1140.4.3](/legal/marketplace/certification-policies#114043-bots)。

如果应用包含机器人，请确保它遵守这些准则。

> [!TIP]
> 有关创建高质量应用体验的详细信息，请参阅 [Teams 机器人设计准则](~/bots/design/bots.md)。

</br>
<details><summary>机器人设计指南</summary>

* Teams 应用必须遵循 [Teams 机器人设计准则](../../../../bots/design/bots.md)。

* 当工作流涉及到用户执行重复性任务时，必须实现任务模块以避免多轮次机器人响应。 例如，使用任务模块重复捕获名称、dob、位置和指定，而不是使用多轮次对话。 [*强制修复*]

* 必须修复应用中任何断开的链接、响应或工作流。 [*强制修复*]

</details>

</br>
<details><summary>机器人命令</summary>

Analyzing user input and predicting user intent is difficult. Bot commands provide users a set of words or phrases for your bot to understand.

* 必须在应用清单部分中 `{commandList}` 列出至少一个受支持的机器人命令。 当用户尝试向机器人发送消息时，这些命令将显示在撰写框中。

   :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-listed.png" alt-text="图形显示应用清单中列出的机器人命令的示例。":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-not-listed.png" alt-text="图形显示未在应用清单中列出的机器人命令的示例。":::

* 机器人支持的所有命令必须正常工作，包括常规命令，如 **Hi**、**Hello** 和 **Help**。
  
  :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-generic-response-pass.png" alt-text="图形显示机器人响应泛型命令的示例。":::

  :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-generic-no-response.png" alt-text="图形显示机器人的示例，该示例对泛型命令没有响应。":::

* 机器人命令不得将用户引入死路，这些命令必须始终提供前进的方法。

   :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-deadend.png" alt-text="validation-bot-commands-dead-end":::

* 必须在清单部分中 `items.commands.title` 列出至少一个有效的机器人命令，并添加一个适当的说明，让用户清楚地了解机器人命令及其使用情况。 清单图面部分中 `commandLists` 列出的机器人命令作为机器人命令菜单中的预填充命令，并为新用户提供与机器人交互的前进道路。 [*强制修复*]

* 机器人响应不得包含任何官方的 Microsoft 产品映像或头像。 在应用中使用自己的资产。 不允许在应用中使用 Microsoft 产品映像。 如果在End-User许可协议 (EULA) 、内容附带的许可条款或 [Microsoft 商标和品牌准则](https://www.microsoft.com/legal/intellectualproperty/trademarks)中获得显式权限，则只能复制、修改、分发、显示、许可或销售 Microsoft 受版权保护的产品映像。 [*强制修复*]

* 机器人必须在不显示连续加载指示器的情况下响应用户命令。 [*强制修复*]

* 机器人帮助命令响应不得将用户重定向到 Teams 外部。 机器人帮助命令响应可以将用户重定向到 Teams 应用中的画布，或在自适应卡片中提供前进的响应。 [*强制修复*]

  :::image type="content" source="../../../../assets/images/submission/validation-bot-redirects-user-outside-teams.png" alt-text="图形显示机器人响应在 Teams 外部重定向用户的示例。":::

* 机器人必须始终对用户输入提供有效的响应，即使输入无关紧要或不正确。 [*强制修复*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-response-valid-improper-input.png" alt-text="图形显示针对机器人命令不当的有效响应的示例。":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-response-improper-response-invalid-command.png" alt-text="图形显示错误机器人命令的无效响应示例。":::

* 特殊字符（如斜杠 (**/**) ）不得以机器人命令为前缀。 [*强制修复*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-special-characters.png" alt-text="图形显示失败方案的示例，其中特殊字符以机器人命令为前缀。":::

* 机器人必须提供对无效用户命令的有效响应。 如果用户发送了无效的机器人命令，机器人不得将用户死角或显示错误。 [*强制修复*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-way-forward-for-invalid-command.png" alt-text="图形显示机器人为无效命令提供前进方向的示例。":::

   :::image type="content" source="../../../../assets/images/submission/validation-welcome-message-bot-dead-end-invalid-command.png" alt-text="图形显示失败方案的示例，其中机器人为有效和无效的命令发送相同的响应。":::

* 机器人功能必须与安装机器人的范围相关，并且机器人必须在安装的范围中提供值。 [*强制修复*]

* 机器人不得包含重复的命令。 [*强制修复*]

* 机器人在响应用户命令后不得显示键入指示器，但可以在响应用户命令时显示键入指示器。 [*强制修复*]

* 机器人必须提供对以小写或大写形式键入的 **帮助** 命令的有效响应，该命令为用户提供前进的道路，或允许用户访问与机器人使用情况相关的帮助内容。 即使用户尚未登录到应用，机器人也必须提供有效的响应。 [*强制修复*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-valid-response-lowercase.png" alt-text="图形显示机器人未以小写或大写形式为命令提供有效响应的示例。":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-valid-response-logged-app.png" alt-text="图形显示用户未登录到应用时没有有效响应的机器人的示例。":::

* 机器人必须提供有效的 **响应来帮助命令** 。

   :::image type="content" source="../../../../assets/images/submission/validation-bot-help-command.png" alt-text="图形显示机器人发送有效响应以帮助命令的示例。":::

* 移动设备上的机器人响应必须具有响应能力，而不会出现任何数据截断，从而妨碍最终用户的机器人使用以完成所需的工作流。 [*强制修复*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-response-no-truncate-mobile.png" alt-text="图形显示机器人消息的示例，而无需在移动设备上截断。":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-response-truncate-mobile.png" alt-text="图形显示在移动设备上截断机器人消息的示例。":::

* 机器人响应自适应卡片中的所有链接都必须具有响应能力。 将用户带入 Teams 平台之外的任何链接都必须具有清晰的重定向文本，例如 **“View in”。** 或 **此方式：.**，机器人响应操作按钮中的弹出图标，或在机器人响应消息正文中具有合适的重定向文本。 [*强制修复*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-action-button-redirect-warning.png" alt-text="图形显示具有重定向的机器人响应操作按钮的示例。":::

* 根据设计，如果机器人不响应或支持任何用户命令，并且是机器人仅用于通知用户的一种方式。 必须在清单中设置为 `isNotificationOnly` true。 [*强制修复*]

  :::image type="content" source="../../../../assets/images/submission/validation-bot-command-isnotification-only-true.png" alt-text="图形显示应用清单中设置为 true 的仅通知属性的示例。":::

  :::image type="content" source="../../../../assets/images/submission/validation-bot-command-isnotification-only-not-true.png" alt-text="图形显示仅通知机器人未响应用户消息的示例。":::

* 机器人用户体验不得在移动平台上中断。 机器人必须在移动设备上完全响应。 [*强制修复*]

> [!TIP]
> 对于个人机器人，请包括一个 **帮助** 选项卡，进一步描述机器人可以执行的操作。

</details>
</br>

<details><summary>机器人欢迎消息</summary>

* 如果应用具有复杂的配置流 (需要企业许可证或缺少直观的注册流) ，则此类应用中的机器人必须在首次运行时始终发送欢迎消息。

  为了获得最佳体验，欢迎消息必须包括机器人提供给用户的值、在通道中安装机器人的用户、如何配置机器人以及简要描述所有受支持的机器人命令。 可以使用带按钮的自适应卡片显示欢迎消息，以提供更好的可用性。 有关详细信息，请参阅 [如何触发机器人欢迎消息](~/bots/how-to/conversations/send-proactive-messages.md)。 对于没有复杂配置流的应用，你可以选择在机器人首次运行体验期间触发欢迎消息。 但是，如果触发欢迎消息，则必须遵循欢迎消息准则。

   :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-message.png" alt-text="图形显示了机器人在机器人具有复杂的配置工作流时发送欢迎消息的示例。":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-no-welcome-message.png" alt-text="图形显示机器人在具有复杂配置工作流时不发送欢迎消息的示例。":::

* 首次运行期间，频道和聊天中的机器人欢迎消息是可选的，尤其是在机器人可供个人使用并执行类似操作时。 机器人不得向用户单独发送欢迎 (将被视为[垃圾邮件](#botmessagespamming))。 消息还必须提及添加机器人的用户。

   :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-message-not-triggered.png" alt-text="validation-bot-welcome-message-not-trigger":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-message-triggered.png" alt-text="validation-bot-wel-message-trigger":::

* 仅通知机器人必须发送一条欢迎消息，其中阐明机器人是仅通知机器人且用户无法与机器人交互。 [*强制修复*]

   :::image type="content" source="../../../../assets/images/submission/validation-notification-only-welcome-message-pass.png" alt-text="图形显示机器人发送欢迎消息的示例，该消息是仅通知机器人。":::

* 欢迎消息不得使用户死胡同。 欢迎消息必须包括机器人提供给在通道中安装机器人的用户提供的值、如何配置机器人以及简要描述所有受支持的机器人命令。 可以使用带按钮的自适应卡片显示欢迎消息，以提供更好的可用性。 [*强制修复*]

   :::image type="content" source="../../../../assets/images/submission/validation-welcome-message-no-way-forward.png" alt-text="图形显示失败方案的示例，其中机器人无法在欢迎消息中为用户前进。":::

   :::image type="content" source="../../../../assets/images/submission/validation-welcome-message-clear-way-forward.png" alt-text="图形显示机器人欢迎消息的示例，其中为用户完成任务提供了清晰的前进道路。":::

* 在频道或群组聊天范围内安装的机器人不得在 1：1 聊天中向所有团队成员发送主动欢迎消息。 [*强制修复*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-send-proactive-message-to-all-members.png" alt-text="图形显示机器人向所有团队成员发送主动欢迎消息的示例。":::

* 仅当消息包含重要信息，供任何用户完成机器人配置或在触发通知时澄清方案时，仅通知机器人才能在通道中发送主动欢迎消息。 [*强制修复*]

* 安装在频道或群组聊天范围内的机器人不得发送主动消息 (不只是欢迎消息) 与频道或群聊中的所有用户无关，而必须通过 1：1 聊天向用户发送主动消息。 [*强制修复*]

* 在频道或组聊天范围内安装的机器人不得允许用户启动单个工作流。 机器人必须在与用户的 1：1 聊天中完成单个工作流。 [*强制修复*]

* 机器人欢迎消息必须明确指出与安装范围内的机器人使用相关的限制。 [*强制修复*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-messahe-with-app-limitation.png" alt-text="图形显示机器人欢迎消息中应用限制的示例。":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-messahe-without-app-limitation.png" alt-text="图形显示欢迎消息中没有应用限制的机器人的示例。":::

* 欢迎消息必须在个人范围内的应用安装时自动触发。 如果机器人未在个人范围内发送欢迎消息，则用户将导致死胡同。 如果应用不包括复杂的配置工作流，则开发人员可以选择在频道或组聊天范围内触发欢迎消息。 [*强制修复*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-no-welcome-message-in-personal-scope.png" alt-text="图形显示机器人未在个人范围内自动发送欢迎消息的示例。":::

* 欢迎消息必须在机器人安装时仅触发一次。 欢迎消息不得在用户每次调用帮助命令时触发。 帮助命令响应必须侧重于包含用户访问与机器人相关的帮助的方法。 [*强制修复*]

* 欢迎消息不得使用每个机器人命令触发。 这被视为垃圾邮件。 [*强制修复*]

  :::image type="content" source="../../../../assets/images/submission/validation-welcome-message-trigger-for-any-command.png" alt-text="图形显示机器人为任何命令触发欢迎消息的示例。":::

* 欢迎消息内容必须与应用的长描述和安装范围中提到的机器人工作流相关。 欢迎消息必须包括机器人提供给在通道中安装机器人的用户提供的值、如何配置机器人以及简要描述所有受支持的机器人命令。 [*强制修复*]

* 在应用安装上触发时，机器人不得发送多个欢迎消息。 [*强制修复*]

  :::image type="content" source="../../../../assets/images/submission/validation-bot-multiple-message-trigger-install.png" alt-text="图形显示机器人在应用安装时触发多个欢迎消息的示例。":::

* 欢迎消息中的应用名称必须与清单中的应用名称匹配。 [*强制修复*]

  :::image type="content" source="../../../../assets/images/submission/validation-app-name-mismatch-manifeast-and-welcome-message.png" alt-text="图形显示欢迎消息中应用名称与应用清单中的应用名称不匹配的示例。":::

* 欢迎消息不得显示基于竞争对手聊天的协作平台名称，除非应用提供特定的互操作性。

* 欢迎消息不得将用户重定向到另一个 Teams 应用，而是欢迎消息必须推动用户完成其第一个任务，并简要描述应用中所有受支持的机器人命令。 [*强制修复*]

* 欢迎消息不得包含指向任何应用市场（包括 AppSource）的链接。 [*强制修复*]

* 如果你的应用具有需要管理员主导的安装的复杂配置工作流，没有直观且随时可用的注册流，或者要求用户完成 Teams 体验之外的配置步骤并返回，则机器人必须在安装后在团队或组聊天范围内发送主动欢迎消息。 [*强制修复*]

* 如果机器人在通道中发送欢迎消息，则不能单独向用户发送它 (它被视为垃圾邮件) 。 欢迎消息还必须提及添加机器人的人员。 [*建议修复*]

> [!TIP]
> 在向单个用户发送的欢迎消息中，一次全方位介绍可以有效概述机器人和任何其他应用功能，鼓励用户尝试机器人命令。 例如，**创建任务**。

</details>
</br>

<details><summary><a id="botmessagespamming">机器人邮件垃圾邮件</a></summary>

机器人不得向用户发送垃圾邮件，即在短时间内发送多条消息。

* **频道和聊天中的机器人邮件**: 请勿通过创建单独的帖子向用户发送垃圾邮件。 创建单一的帖子，并在同一线程中进行回复。

    :::image type="content" source="../../../../assets/images/submission/validation-bot-message-spamming-one-message.png" alt-text="validation-bot-message-spam-one-message":::

    :::image type="content" source="../../../../assets/images/submission/validation-bot-message-spamming-multiple-messages.png" alt-text="validation-bot-message-spam-multiple-message":::

* **个人应用中的机器人消息**：
  * 请勿快速连续发送多个消息。

    :::image type="content" source="../../../../assets/images/submission/validation-bot-messages-multiple-message-quick-succession.png" alt-text="图形显示机器人快速连续发送多个消息的示例。":::

  * 发送一条包含完整信息的消息。
  * 避免通过多轮对话完成单个重复工作流。
  * 使用窗体 (或任务模块) 一次性收集用户的所有输入。
  * 基于 NLP 的对话聊天机器人可以使用多轮对话使讨论更具吸引力并完成工作流。

    :::image type="content" source="../../../../assets/images/submission/validation-bot-messages-using-task-module.png" alt-text="validation-bot-message-using-task-module":::

    :::image type="content" source="../../../../assets/images/submission/validation-bot-messages-using-mutliple-conversation.png" alt-text="图形显示使用多轮次消息完成单个对话的示例机器人。":::

* **欢迎消息**：不要定期重复相同的欢迎消息。 例如，将新成员添加到团队时，不要向其他成员发送显示为欢迎消息的垃圾邮件。 向新成员单独发送消息。

   :::image type="icon" source="../../../../assets/images/submission/validation-bot-send-proactive-message-to-all-members.png" alt-text="图形显示一个示例机器人使用相同的欢迎消息向用户发送垃圾邮件。":::

</details>
</br>

<details><summary>机器人通知</summary>

机器人通知必须包含与你为机器人 (团队、聊天或个人) 定义的范围相关的内容。

:::image type="content" source="../../../../assets/images/submission/validation-bot-notifications-relevant.png" alt-text="validation-bot-notification-relevant":::

:::image type="content" source="../../../../assets/images/submission/validation-bot-notifications-not-relevant.png" alt-text="validation-bot-notification-not-relevant":::

</details>
</br>
<details><summary>机器人和自适应卡片</summary>

自适应卡片是强烈建议显示机器人消息的方法。 卡片必须轻量，并且最多只包含六个操作。 若要显示更多内容，请考虑使用任务模块或选项卡。

有关卡片的详细信息，请参阅：

* [设计自适应卡片](~/task-modules-and-cards/cards/design-effective-cards.md)
* [卡参考](~/task-modules-and-cards/cards/cards-reference.md#types-of-cards)

机器人体验必须在移动设备上完全响应。 机器人响应必须提供一种前进方法（如果适用）。 机器人必须快速响应，并且失败时会显示一条得体的失败错误消息。 基于协作范围内触发器在个人范围内发送给用户的机器人消息必须提供上下文信息 (包括消息的来源)。

</details>
</br>

<details><summary>仅通知机器人</summary>

由仅通知机器人组成的应用通过基于核心应用或后端中的特定触发器或事件触发用户通知，从而为用户提供价值。 例如，添加了新的销售线索或潜在客户，供销售团队跟进。 高质量通知仅机器人会在某些事件完成（如工作流完成或警报）上定期通知用户。

如果符合以下情况，则 Teams 中的通知将提供价值：

1. 已发布的卡片或文本提供了足够的详细信息，无需进一步的用户操作。
1. 已发布的卡片或文本提供足够的预览信息，供用户执行操作或决定在 Teams 外部打开的链接中查看更多详细信息。

仅提供包含内容的通知的应用，例如， **你有一个新通知**、 **单击以查看** 并要求用户在 Teams 外部导航其他所有内容不会在 Teams 中提供显著价值。

   :::image type="content" source="../../../../assets/images/submission/validation-bot-notification-only-inadequete-info.png" alt-text="屏幕截图显示通知的示例，其中仅包含预览版中信息不足的位。":::

> [!TIP]
> 预览信息，并在张贴的卡片中提供基本的内联用户操作，以便用户无需在 Teams 外部导航，无论) 复杂性如何 (的所有操作。

</details>
<br/>

<details><summary>机器人元数据信息</summary>

* 应用清单中的机器人信息 (机器人名称、徽标、隐私链接和服务条款链接) 必须与 Bot Framework 元数据一致。 [*强制修复*]

* 机器人 ID 必须在应用清单和 Bot Framework 元数据中匹配。 [*强制修复*]

* 确保应用清单中的机器人 ID 与应用的上一个应用商店已发布版本中的机器人 ID 匹配。 更改应用更新中的机器人 ID 会导致应用现有用户与机器人的所有用户交互历史记录永久丢失，并使用新的机器人 ID 启动新的聊天链。 [*强制修复*]

* 对应用名称、元数据、机器人欢迎消息或机器人响应的任何更改都必须使用新名称进行更新。 [*强制修复*]

* 机器人欢迎消息或机器人响应中的应用名称必须与清单中的应用名称匹配。 [*强制修复*]

</details>
<br/>

<details><summary>协作范围内的机器人</summary>

* 在频道或组聊天范围内安装机器人以获取团队名单，以便为用户发送主动通知，因为不允许针对团队特定触发器进行 1：1 聊天。 例如，将用户配对以进行聚会的应用。 [*强制修复*]

* 频道或群聊中的机器人仅用于获取频道或群聊中的消息或帖子，以便为用户发送主动通知，因为不允许 1：1 聊天。 [*强制修复*]

* 安装在协作范围内的机器人必须在协作范围内提供用户值。 [*强制修复*]

</details>

## <a name="message-extensions"></a>消息扩展

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::本部分符合 [Microsoft 商业市场策略号 1140.4.4](/legal/marketplace/certification-policies#114044-messaging-extensions)。

如果应用包含消息扩展，请确保它遵守这些准则。

> [!TIP]
> 有关创建高质量应用体验的详细信息，请参阅 [Teams 消息扩展设计准则](~/messaging-extensions/design/messaging-extension-design.md)。

<br/>

<details><summary>消息扩展设计指南</summary>

* 如果 Teams 应用使用消息传递扩展功能，则应用必须遵循 [消息传递扩展设计准则](../../../../messaging-extensions/design/messaging-extension-design.md)。

   :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-design-guidelines-fail.png" alt-text="图形显示应用不符合扩展准则的示例。":::

* 消息传递是插入应用程序内容或对消息采取行动的快捷方式，而无需从对话中导航。 使消息传递扩展保持简单，并仅显示有效完成操作所需的组件。 在消息扩展插件中不得对完整网站进行 I 帧 [*强制修复*]

* 消息传递扩展插件中的自适应卡片中的预览图像必须正确加载。 [*强制修复*]

  :::image type="content" source="../../../../assets/images/submission/validation-preview-image-adaptive-card-loading.png" alt-text="图形显示自适应卡片中预览图像加载的示例。":::

  :::image type="content" source="../../../../assets/images/submission/validation-preview-image-adaptive-card-not-loading.png" alt-text="图形显示未在自适应卡片中加载预览图像的示例。":::

* 消息传递扩展响应卡必须包含应用图标，以避免最终用户混淆。 [*强制修复*]

* 你的应用不得有任何损坏的功能。 应用不得死胡同或阻止用户完成消息传递扩展中的工作流。 [*强制修复*]

* 消息传递扩展插件必须在群聊和频道范围中按预期响应或工作。 [*强制修复*]

* 必须包含用户登录或从消息传递扩展注销的方式。 [*强制修复*]

</details>
</br>

<details><summary>基于操作的消息扩展的操作命令</summary>

基于操作的消息扩展必须执行以下操作：

* 允许用户在未完成中间步骤（如登录）的情况下对消息触发操作。

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-no-intermediate-step.png" alt-text="validation-messaging-extension-no-intermediate-steps":::

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-intermediate-step-available.png" alt-text="validation-messaging-extension-intermediate-steps-available":::

* 将消息上下文传递到下一个工作状态。 [*强制修复*]

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-app-passes-message.png" alt-text="validation-messaging-extension-app-passes-messages":::

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-app-doesnot-pass-message.png" alt-text="validation-messaging-extension-app-doesnot-pass-messages":::

* 包含主机应用名称，而不是从聊天消息、频道帖子或应用内操作调用触发的操作命令的通用动词。 例如，使用“**开始会议****”Skype 会议**，**将文件上传到 DocuSign** 以 **上传文件**。 [*建议修复*]

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-action-command-host-name.png" alt-text="图形显示操作命令的主机应用名称示例。":::

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-action-command-verb.png" alt-text="图形显示操作命令的泛型谓词示例。":::

* 调用消息操作必须允许用户完成工作流。 无法显示错误、空白响应或连续加载指示器，使消息操作按预期正常运行。 [*强制修复*]

   :::image type="content" source="../../../../assets/images/submission/validation-continous-loading-indicator-action-command.png" alt-text="图形显示机器人调用操作命令时连续加载指示器的示例。":::

* 不能存在重复的操作命令。 [*强制修复*]

* 消息操作必须允许用户按预期完成工作流，而无无效响应。 [*强制修复*]

* 仅具有基于操作的消息传递扩展的应用必须具有以下结束状态：

  * 在调用消息扩展的上下文中或基于用户方案在 1：1 机器人聊天中发布相关操作作为通知。 [*强制修复*]

  * 允许用户根据所采取的操作与其他用户共享卡片。 这是为了确保应用不会采取无提示操作。 例如，票证是根据频道中的消息创建的，但应用不发送通知，也不提供在创建票证后请求用户共享票证详细信息的方法。 [*强制修复*]

</details>
</br>

<details><summary>预览链接 (链接展开)</summary>

[*强制修复*]

消息扩展必须预览在 Teams 撰写框中识别的链接。 不要添加不受控制的域 (无论是绝对 URL 或通配符)。 例如，`yourapp.onmicrosoft.com` 有效，但 `*.onmicrosoft.com` 无效。 也禁止使用顶级域。 例如，`*.com` 或 `*.org`。 [*强制修复*]

</details>
</br>

<details><summary>搜索命令</summary>

* 基于搜索的消息扩展必须提供可帮助用户进行有效搜索的文本。 [*强制修复*]

    :::image type="content" source="../../../../assets/images/submission/validation-search-commands-text-available.png" alt-text="图形显示消息扩展的示例，其中包含帮助文本，供用户有效搜索。":::

    :::image type="content" source="../../../../assets/images/submission/validation-search-commands-text-not-available.png" alt-text="图形显示消息扩展的示例，而用户无需帮助文本即可进行有效搜索。":::

* @提及可执行文件必须清晰、易于理解且可读。

    :::image type="content" source="../../../../assets/images/submission/validation-search-command-unclear-executable.png" alt-text="validation-search-commands-unclear-executable":::

</details>
</br>

<details><summary>基于搜索的消息扩展的操作命令</summary>

[*强制修复*]

由基于搜索的消息扩展组成的应用通过共享允许上下文对话而无需上下文切换的卡片为用户提供价值。

若要仅对基于搜索的消息扩展应用传递验证，需要将以下内容作为基线来确保用户体验不会中断。 如果满足以下情况，通过消息扩展共享的卡片将在 Teams 中提供价值：

1. 已发布卡片提供了足够详细的信息，无需用户进一步操作。
1. 已发布卡片为用户提供了足够的预览信息，以便进行操作或决定在 Teams 外部打开的链接中进一步查看详细信息。

    :::image type="content" source="../../../../assets/images/submission/validation-search-based-messaging-ext-adequete-info.png" alt-text="validation-search-base-messaging-ext-adequete-info":::

    :::image type="content" source="../../../../assets/images/submission/validation-search-based-messaging-ext-inadequete-info.png" alt-text="validation-search-base-messaging-ext-inadequete-info":::

链接仅展开应用不会在 Teams 中提供重大价值。 如果应用仅支持链接展开且没有其他功能，请考虑在应用中构建其他工作流。

</details>

## <a name="task-modules"></a>任务模块

[*强制修复*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::本部分符合 [Microsoft 商业市场策略号 1140.4.5](/legal/marketplace/certification-policies#114045-task-modules)。
<br></br>
<details><summary>展开以了解详细信息</summary>

任务模块必须包含图标及其关联的应用的短名称。 任务模块不得嵌入整个应用，而只能显示完成特定操作所需的组件。

有关详细信息，请参阅[Teams 任务模块设计准则](~\task-modules-and-cards\task-modules\design-teams-task-modules.md)。

:::image type="content" source="../../../../assets/images/submission/validation-task-module-displays-components.png" alt-text="validation-task-module-displays-component":::

:::image type="content" source="../../../../assets/images/submission/validation-task-module-embeds-app.png" alt-text="validation-task-module-embed-app":::

> [!TIP]
> 有关创建高质量应用体验的详细信息，请参阅 [Teams 任务模块设计准则](~/task-modules-and-cards/task-modules/design-teams-task-modules.md)。

</details>

## <a name="meeting-extensions"></a>会议扩展

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::本部分符合 [Microsoft 商业市场策略号 1140.4.6](/legal/marketplace/certification-policies#114046-meeting-extensions)。
> [!TIP]
> 有关创建高质量应用体验的详细信息，请参阅 [Teams 会议扩展设计准则](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)。

</br>
<details><summary>会议扩展设计指南</summary>

* Teams 应用必须遵循 [会议扩展设计准则](../../../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)。

* 借助会议内应用体验，可以使用会议内选项卡、对话框和会议内共享来暂存功能，在会议期间吸引参与者。 如果应用支持 Teams 会议扩展，则必须提供与 Teams 会议体验一致的响应式会议内体验。 [*强制修复*]

* 通过会议前应用体验，用户可以查找和添加会议应用。 用户还可以执行会前任务，例如开发投票来调查会议参与者。 提供会议前体验的应用必须与会议工作流相关，并向用户提供价值。 [*强制修复*]

* 使用会后应用体验，用户可以查看会议结果，例如轮询调查结果或反馈和其他应用内容。 提供会后体验的应用必须与会议工作流相关，并向用户提供价值。 [*强制修复*]

* 通过会议内应用体验，可以在会议期间与会议参与者互动，并增强所有与会者的会议体验。 不能将与会者带出 Teams 会议，以完成应用的核心用户工作流。 [*强制修复*]

   :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-outside-teams-core-workflows.png" alt-text="图形显示会议内体验的示例，该示例将用户重定向到 Teams 外部以完成核心应用功能。":::

* 你的应用必须提供价值，而不能在 Teams 中仅提供自定义的“一起模式”场景。 [*强制修复*]

* 必须声明`groupChat`为清单中`configurableTabs`的作用域和`meetingDetailsTab``meetingChatTab`上下文属性，`meetingSidePanel`才能为 Teams 移动版上的会议启用应用。 [*强制修复*]

* 会议画布不得终止会议与会者。 会议画布必须针对应用限制（例如区域特定依赖项）显示正常失败消息。 [*强制修复*]

* 会议画布的标头必须显示正确的应用名称，以避免混淆会议与会者。 [*强制修复*]

* 必须包含用户注销或注销会议扩展插件的选项。 [*强制修复*]

* 移动平台上的会议选项卡必须包含相关工作流。 会议选项卡中不得存在空白页。[*强制修复*]

* 会议阶段是一个专注、直观和协作参与的画布。 会议阶段不得嵌入完整的网站体验。 [*强制修复*]

* 应用不得显示连续加载屏幕、错误或损坏的功能，这些功能会使用户死胡同或阻止在会议方案中完成工作流。 [*强制修复*]

   :::image type="content" source="../../../../assets/images/submission/validation-app-shows-continous-loading-screen.png" alt-text="图形显示应用中连续加载屏幕的示例。":::

* 在启动会议时，应用不得打开新的 Teams 实例。 会议画布是 Teams 功能的扩展，可促进实时协作，并且新会议必须始终在当前活动的 Teams 实例中打开。 [*强制修复*]

* 会议应用必须在 Microsoft Teams 平台内完成工作流，而无需重定向到基于竞争对手聊天的平台。 [*强制修复*]

   :::image type="content" source="../../../../assets/images/submission/validation-apps-redirecting-competitor-chat-platform.png" alt-text="图形显示应用重定向到基于竞争对手聊天的平台的示例。":::

* 如果你的应用支持基于角色的视图，并且某些工作流对所有参与者都不可用，我们建议你为选项卡和侧面板中的参与者实施正确的消息传递，指出该应用当前适用于组织者的视图，并提供有关与会者如何接收会议笔记、操作项目和更新议程的详细信息。 [*强制修复*]

   :::image type="content" source="../../../../assets/images/submission/validation-way-forward-not-available-for-role-based-views.png" alt-text="图形显示应用的示例，而对于基于角色的视图中的参与者来说，没有前进的道路。":::

</details>
<br/>

<details><summary>常规</summary>

对会议扩展使用以下准则：

* 会议扩展性应用必须提供与 Teams 会议体验一致的响应式会议内体验。 对于支持会议扩展性的 Teams 应用，会议内体验是必需的，但会议前和会后体验不是必需的。

  * 通过会议前应用体验，用户可以查找和添加会议应用。 用户还可以执行会议前任务，例如开发投票来调查会议参与者。 如果你的应用提供会议前体验，它必须与会议工作流相关。

  * 使用会后应用体验，用户可以查看会议结果，例如轮询调查结果或反馈和其他应用内容。 如果你的应用提供会议后体验，它必须与会议工作流相关。

  * 通过会议内应用体验，可以在会议期间与会议参与者互动，并增强所有与会者的会议体验。 不能将与会者带出 Teams 会议，以完成应用的核心用户工作流。

* 除了在 Teams 中提供自定义同框场景模式之外，你的应用还必须提供额外价值。

* 共享会议阶段功能只能通过 Teams 桌面应用启动。 但是，在移动设备上查看时，共享会议阶段使用体验必须可用且不会中断。

> [!TIP]
> 必须声明`groupChat`为清单中`configurableTabs`的作用域和`meetingDetailsTab``meetingChatTab`上下文属性，`meetingSidePanel`才能为 Teams 移动版上的会议启用应用。

</details>
</br>

<details><summary>会议前和会议后体验</summary>

* 会议前和会议后屏幕必须遵守常规选项卡设计准则。 有关详细信息，请参阅[Teams 设计准则](~/tabs/design/tabs.md)。
* 显示多个项时，选项卡应具有井然有序的布局。 例如，超过 10 个投票或调查，请参阅 [示例布局](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#after-a-meeting)。
* 当导出调查或投票的结果时，你的应用必须通知用户，表明“**结果已成功下载**”。

   :::image type="content" source="../../../../assets/images/submission/validation-meeting-experience-tab-design-guidelines-fail.png" alt-text="图形显示选项卡不遵循选项卡设计准则的示例。":::

</details>

</br>
<details><summary>会议内体验</summary>

* 在会议期间应用必须仅能使用深色主题。 有关详细信息，请参阅[Teams 设计准则](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#theming)。
* 在会议期间将鼠标悬停在应用图标上时，工具提示必须显示应用名称。

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-exp-display-app-name.png" alt-text="validation-in-meeting-exp-display-app-names":::

* 消息扩展在会议期间的功能必须与在会议外部执行的相同。

</details>

</br>
<details><summary>会议内选项卡</summary>

* 必须具有响应能力。
* 必须保持填充和组件大小。
* 如果具有多个导航层，则必须有一个后退按钮。

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-exp-back-button.png" alt-text="图形显示显示的后退按钮示例。":::

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-exp-back-button-absent.png" alt-text="图形显示未显示的后退按钮示例。":::

* 不得包含多个关闭按钮。 它可能会让用户混淆，因为已有一个可关闭选项卡的内置标题按钮。
* 不得有水平滚动。

  :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-tab-vertical-scroll.png" alt-text="图形显示带有垂直滚动的会议内选项卡的示例。":::

  :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-tab-horizontal-scroll.png" alt-text="图形显示具有水平滚动的会议内选项卡的示例。":::

</details>

</br>
<details><summary>会议内对话</summary>

* 应谨慎使用并用于轻型和任务导向的场景。
* 必须在单栏中显示内容，而且不能有多个导航层。

  :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-single-column-layout.png" alt-text="图形显示会议内对话框的单列布局示例。":::

  :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-multiple-column-layout.png" alt-text="图形显示会议内对话框的多个列布局的示例。":::

* 不得使用任务模块。
* 必须与会议阶段的中心对齐。

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-dialog-not-aligned.png" alt-text="图形显示会议中对话框不与会议阶段中心对齐的示例。":::

* 在用户选择按钮或执行某个操作后必须关闭。

* **同框场景模式**：确保考虑以下场景生成体验最佳做法：
  * 所有图像都采用 .PNG 格式。
  * 所有图像组合在一起的最终程序包的分辨率不得超过 1920x1080。 分辨率为偶数。 要成功显示场景，需要此分辨率。
  * 最大场景大小为 10 MB。
  * 每个图像的最大大小为 5 MB。 场景是多个图像的集合。 限制是针对每个单独图像。
  * 根据需要选择 **透明**。 选中图像后，此复选框在右侧面板上可用。 重叠的图像必须标记为透明，以指示它们是场景中的重叠图像。

</details>

## <a name="notifications"></a>通知

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::本部分符合 [Microsoft 商业市场策略号 1140.4.7](/legal/marketplace/certification-policies#114047-notification-apis)。

如果应用使用 [Microsoft Graph 提供的活动源 API](/graph/teams-send-activityfeednotifications)，请确保它遵循以下准则。

> [!TIP]
> 如果应用支持在长时间间隔后触发通知的通知方案，例如，在一天或一个月后触发通知。 提交审阅之前，请确保在后台触发此类通知，以便我们测试通知。

<br></br>

<details><summary>通知设计指南</summary>

* Teams 应用必须遵循 [活动源通知设计准则](/graph/teams-send-activityfeednotifications)。

* 用户在 Teams 活动源中选择通知后，不得存在不相关、不正确、无响应或损坏的工作流。 在用户选择活动源通知后，不得阻止他们完成工作流。 [*强制修复*]

* 将应用的名称包含在活动源通知中，让最终用户了解通知的源或触发器，而不会造成混淆。 [*强制修复*]

* 应用必须针对应用长描述、应用首次运行体验以及清单中声明 `activityTypes` 的方案中提到的所有通知方案触发通知。 [*强制修复*]

* 通知必须在用户操作后的五秒内显示。 [*强制修复*]

* 如果应用长描述或应用的首次运行体验中有任何) ，则必须 (调用通知限制。 [*强制修复*]

</details>
<br/>

<details><summary>常规</summary>

* 应用配置中指定的所有通知触发器都必须正常工作。
* 通知必须根据为应用配置的支持语言进行本地化。
* 通知必须在用户操作后的五秒内显示。
* 必须根据应用兼容的所有平台支持的语言本地化通知。 [*强制修复*]

</details>
</br>

<details><summary>头像</summary>

* 通知头像必须与应用的颜色图标匹配。
* 用户触发的通知必须包含用户的头像。

</details>
</br>
<details><summary>垃圾邮件</summary>

* 应用每分钟不得向用户发送超过 10 条通知。
* 机器人和活动信息提要不得触发重复通知。
* 通知必须为用户提供一些值，并且不能用于琐碎或不相关的事件。

</details>
</br>
<details><summary>导航和布局</summary>

* 通知必须遵循 Teams 活动源布局和体验。
* 在选择通知时，必须将用户定向到 Teams 内部的相关内容。

</details>

## <a name="microsoft-365-app-compliance-program"></a>Microsoft 365 应用合规性

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::本部分符合 [Microsoft 商业市场策略号 1140.6](/legal/marketplace/certification-policies#11406-publisher-attestation)。
<br></br>
<details><summary>展开以了解详细信息</summary>

Microsoft 365 应用合规性计划 旨在帮助企业通过评估应用程序的安全和合规性信息来评估和管理风险。 如果要向 Teams 商店发布一个应用程序，则必须完成该程序的以下几层:

* **发布者验证**: 可帮助管理员和终端用户了解到应用开发人员与 Microsoft 标识平台集成的真实性。 完成后，Azure Active Directory 同意对话框和其他屏幕上将显示蓝色的“**已验证**”徽章。 有关详细信息，请参阅 [将你的应用标记为经过发布者验证](/azure/active-directory/develop/mark-app-as-publisher-verified)。

    :::image type="content" source="../../../../assets/images/submission/validation-365-compliance-publisher-verification.png" alt-text="图形显示 Azure Active Directory 许可对话框上的蓝色已验证徽章示例。":::

* **发布者证明**: 共享常规、数据处理以及安全性和合规性信息的过程，以帮助潜在客户在使用应用时做出明智的决定。

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::如果提交之前未列出的应用，则在应用进入 Teams 商店之前，无法正式完成发布者证明。 如果正在更新列出的应用，请在提交最新版本的应用之前完成发布者证明。

</details>

## <a name="advertising"></a>广告

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::本部分符合 [Microsoft 商业市场策略编号1140.7](/legal/marketplace/certification-policies#11407-advertising)。

应用不得显示广告，包括动态广告、横幅广告和消息内广告。

:::image type="content" source="../../../../assets/images/submission/validation-advertising-banners.png" alt-text="图形显示 Teams 中广告失败的示例。":::

## <a name="cryptocurrency-based-apps"></a>基于加密货币的应用

如果你的应用，则必须演示对分发应用的所有法律的符合性：

* 促进应用中的加密货币事务或传输。

* 提升与加密货币相关的内容。

* 使用户能够存储或访问其存储的加密货币。

* 鼓励或允许用户在 Teams 平台外部完成基于加密货币的事务或传输。

* 鼓励或促进挖掘加密货币令牌。

* 促进用户参与初始硬币产品/服务。

* 奖励或激励使用加密货币令牌的用户完成任务。

经过 Microsoft 内部评审后，如果符合性演示令人满意，Microsoft 可能会继续对应用进行进一步认证。 如果合规性演示不令人满意，Microsoft 会告知你不继续对应用进行认证的决定。

## <a name="app-functionality"></a>应用功能

* 应用中的工作流或内容必须与范围相关。 [*强制修复*]
* 所有应用功能都必须正常工作，并且必须正常工作，如 AppSource 或清单长说明中所述。 [*强制修复*]
* 在用户环境中下载任何文件或可执行文件之前，应用必须始终与用户保持亲密关系。 任何对操作的调用 (CTA) （基于文本还是以其他方式）向用户表明，在用户操作上下载文件或可执行文件是允许在应用中下载的。 [*强制修复*]

## <a name="mobile-experience"></a>移动体验

* 移动加载项必须免费。 不得有任何应用内内容或链接可以促进销售、在线商店或其他付款请求。 应用所需的任何帐户都必须不收取使用费用，如果时间有限，则不得包含任何指示需要付款的内容。

   :::image type="content" source="../../../../assets/images/submission/validation-mobile-add-in-charges.png" alt-text="图中显示了要求付款的移动加载项的示例。":::

* 桌面或 Web 应用体验中允许使用“ **免费**”、“ **免费试** 用”或“ **TRY FREE** ”一词，而无需任何限制或考虑。

* 在试用版或应用升级的上下文中，允许在移动设备上使用“ **免费** ”一词作为纯文本。

* 在试用版或应用升级的上下文中使用“ **免费** ”一词，其中包含一个链接，该链接可在移动设备上导致登陆页面，而无需付款或定价信息。 允许在移动设备上使用纯文本来表示应用是 **PAID** 。

* 在试用版或应用升级的上下文中，不允许将“ **免费** ”一词用作纯文本，并且不允许在移动设备上与定价详细信息相关联。

* 不允许在试用版或应用升级的上下文中使用“ **免费** ”一词，并将其与链接相关联，该链接会导致登陆页面上包含移动设备上的定价信息或付款详细信息。

* 不允许任何格式的移动设备定价详细信息，例如图像、文本或链接。 不允许使用 CTA（例如移动版上的 **视图计划** ）。 不允许使用移动设备上的联系人链接或电子邮件来了解没有定价详细信息的计划。 移动设备上不允许任何包含联系人详细信息链接或暗示付费升级的文本。 允许在移动设备上付款物理商品。 例如，你的应用可以允许付款预订出租车。

   :::image type="content" source="../../../../assets/images/submission/validation-mobile-exp-pricing-details-on-mobile-fail.png" alt-text="图形显示有关移动设备的定价详细信息的示例。":::

* 应用中的数字商品付款不允许在移动设备上使用。 [*强制修复*]

   :::image type="content" source="../../../../assets/images/submission/validation-mobile-exp-payments-digital-goods.png" alt-text="图示了移动设备上数字商品的付款示例。":::

* Teams 应用必须提供适当的跨设备移动体验。 [*强制修复*]

* 在移动设备上不受支持的功能不得使用户死胡同，并且必须在适用的情况下提供正常故障消息。 [*强制修复*]

## <a name="next-step"></a>后续步骤

> [!div class=*nextstepaction*]
> [创建合作伙伴中心帐户](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)

## <a name="see-also"></a>另请参阅

* [分发应用](~/concepts/deploy-and-publish/apps-publish-overview.md)
* [准备应用商店提交](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [测试和调试应用](~/concepts/build-and-test/debug.md)
* [创建合作伙伴中心开发人员帐户](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)
