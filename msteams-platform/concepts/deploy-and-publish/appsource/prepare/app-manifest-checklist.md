---
title: 应用部件清单（manifest）清单
description: 用于将 Microsoft 团队应用程序发布到 AppSource 的应用程序清单的清单
keywords: 团队发布 microsoft store office 发布清单
ms.openlocfilehash: e684bb4f578944c6f37eeb43541a491d42ec3479
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673334"
---
# <a name="app-manifest-checklist"></a>应用部件清单（manifest）清单

您的应用程序清单需要符合下面所述的准则。

>[!Tip]
> 使用应用程序 Studio 可帮助您生成应用程序清单。 它将验证以下大多数要求，并在 "**测试和分布**" 选项卡上显示任何错误或警告。

## <a name="tips"></a>提示

* 请勿在您的应用程序名称中使用 "团队"、"Microsoft" 或 "应用程序"。
* 应用程序清单中的 developerName 必须与在合作伙伴中心或卖家面板中定义的提供程序名称相同。
* 请确保应用程序说明、屏幕截图、文本和促销图像仅描述应用程序，并且不包含任何其他广告、促销或版权品牌名称。
* 如果你的产品需要服务或其他服务上的帐户，请列出说明中的，并确保有要注册的链接，请登录并注销。
* 如果你的产品需要额外购买才能正常运行，请在说明中列出。
* 在清单和合作伙伴中心或卖家面板中提供必备条款和隐私策略链接。 验证这些链接是否正确地解析为正确的文档，以及理想的工作组。 对于 bot，必须在 "Bot 框架注册" 页的 "提交" 部分提供相同的信息。
* 确保清单中的元数据与合作伙伴中心或卖家面板中的元数据完全匹配（以及 Bot 框架注册中的 bot）。 请注意，卖家面板条目应包含更详细和已设置格式的说明，以便在 AppSource 产品页面中使用。
* 请确保清单中使用的应用程序标题与在合作伙伴中心或卖方仪表板提交中输入的应用程序标题完全匹配

## <a name="metadata-requirement"></a>元数据要求

您的应用程序需要以下元数据。

|Data|类型|大小|清单|合作伙伴中心|说明|
|---|---|---|---|---|---|
|应用程序包|.zip|||✔|用于上传或 AppSource 提交的实际应用程序包。|
|颜色徽标|.png|192&times;192 像素|`icon.color`||要在团队库中的产品页列表中显示的图标。 这是您的全彩色产品徽标。|
|徽标轮廓|.png|32&times;32 像素|`icon.outline`||要在团队中的团队聊天频道和其他位置中显示的图标。 这是你的徽标呈现为带有透明背景的白色轮廓。|
|应用徽标|.png、.jpg、jpeg、.gif|300&times;300 像素||✔|要在 AppSource 中显示的图标。 这是全彩色产品徽标，与清单中使用的文件不同`icon.color`。 它应小于 512 KB。|
|支持链接|URL|||✔|为可能尚未安装您的应用程序的最终用户提供支持材料的链接。 可在没有任何登录名（HTTPS）的情况下公开提供链接。|
|隐私链接|URL||`developer.privacyUrl`|✔|指向你的隐私策略（HTTPS）的链接。|
|视频链接|URL|||可选|指向有关您的应用程序的视频的链接。|
|最终|.doc、.pdf 等。|||可选|AppSource 需要最终用户许可协议（EULA），您可以将其作为附件提供。 如果选择不提交 EULA，将代表你提供一个 EULA。|
|服务条款|URL||`developer.termsOfServiceUrl`||服务条款（HTTPS）的链接。|
|测试说明|内嵌填充或链接到公用 URL|||有关如何分步测试应用程序的详细测试说明。 请包含用于测试管理员和非管理员方案的两个登录凭据。|

## <a name="localized-content"></a>本地化内容

> [!NOTE]
> AppSource 计划支持以下元数据的本地化内容。 目前，您的应用程序清单将仅在 AppSource 中显示为英语，但将在团队客户端中正确显示本地化。 有关详细信息，请参阅[本地化您的应用程序](~/concepts/build-and-test/apps-localization.md)。

|Data|类型|大小|清单|合作伙伴中心|说明|
|---|---|---|---|---|---|
|应用名称|String|30|`name.short`|✔|您的应用程序的名称应显示在店面和产品中。|
|长应用程序名称|String|30|`name.full`|✔|您的应用程序的名称应显示在店面和产品中。|
|简短说明|String|80|`description.short`|✔|您的应用程序的简短说明。|
|较长说明|String|4000|`description.full`|✔|您的应用程序的更详细说明。 在清单文件中，准确的摘要就足够了。 在合作伙伴中心，您可以对 AppSource 产品页面使用更丰富的格式化说明。|
|屏幕截图（1-5）|.png、.jpg 或 .gif|1366w x 768h 和小于 1024 KB||✔|至少一个显示你的应用程序体验的屏幕截图。 在 "应用程序详细信息" 页上使用。|

## <a name="submission-extras-for-bots"></a>Bot 的提交额外内容

Microsoft 团队中的 bot 必须使用 Bot 框架创建。 有关说明，请参阅[创建 bot](~/bots/how-to/create-a-bot-for-teams.md) 。 在 Bot 框架中为你的 bot 图标使用96x96 彩色图标。
