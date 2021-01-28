---
title: 应用清单检查表
description: 将 Microsoft Teams 应用发布到 AppSource 的应用清单清单
ms.topic: reference
keywords: teams 发布应用商店 Office 发布清单
ms.openlocfilehash: f07c0d2693d12d56d6717724e1ef402cf79d5fff
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014395"
---
# <a name="app-manifest-checklist"></a>应用清单检查表

>[!IMPORTANT]
>我们正在将 Office 解决方案的管理从卖家面板迁移到合作伙伴中心。 有关详细信息，请参阅[从卖家面板移动到合作伙伴中心](https://developer.microsoft.com/office/blogs/moving-management-of-solutions-from-seller-dashboard-to-partner-center/)并阅读[常见问题解答](https://docs.microsoft.com/office/dev/store/partner-center-faq)。

应用清单需要遵循下面列出的准则。

>[!Tip]
> 使用 App Studio 帮助你生成应用清单。 它将验证下面的大部分要求，并显示"测试和分发"选项卡上的任何错误 **或警告。**

## <a name="tips"></a>提示

* 不要在应用名称中使用"Teams"、"Microsoft"或"app"。
* 清单中的 developerName 必须与合作伙伴中心中定义的提供商名称相同。
* 确保应用描述、屏幕截图、文本和促销图像仅描述应用，并且不包含任何其他广告、促销或受版权保护的品牌名称。
* 如果你的产品需要你的服务或其他服务上的帐户，则说明中列出此帐户，并确保存在用于注册、登录和注销的链接。
* 如果你的产品需要其他购买以正常运行，则说明中列出此内容。
* 在清单和合作伙伴中心或仪表板中提供必要的条款和隐私策略链接。 验证链接是否正确解析为正确的文档，最好是特定于 Teams 的文档。 对于自动程序，你必须在自动程序框架注册页的"提交"部分提供此信息。
* 确保清单中的元数据与合作伙伴中心中的元数据完全匹配 (自动程序框架注册中心中的) 。 请注意，合作伙伴中心条目可能包含更详细的格式化说明，以在 AppSource 产品页面中使用。
* 确保清单中使用的应用标题与合作伙伴中心提交中输入的应用标题完全匹配。 *请参阅* 在 Microsoft AppSource 和 Office 内创建有效的一览 [— 使用一致的加载项名称](https://docs.microsoft.com/office/dev/store/create-effective-office-store-listings#use-a-consistent-add-in-name)。

## <a name="metadata-requirement"></a>元数据要求

应用需要以下元数据。

|Data|类型|Size|清单|合作伙伴中心|说明|
|---|---|---|---|---|---|
|应用包|.zip|||✔|用于上传或 AppSource 提交的实际应用包。|
|颜色徽标|.png|192 &times; 192 像素|`icon.color`||要显示在 Teams 库中的产品页面一览中的图标。 这是全彩色产品徽标。|
|徽标大纲|.png|32 &times; 32 像素|`icon.outline`||在 Teams、Teams 聊天频道和其他位置显示的图标。 这是徽标呈现为白色边框，背景透明。|
|应用徽标|.png、.jpg、.jpeg、.gif|300 &times; 300 像素||✔|在 AppSource 中显示的图标。 这是全彩色产品徽标，与清单中使用的文件不同 `icon.color` 。 应小于 512 KB。|
|支持链接|URL|||✔|一个链接，用于为可能尚未安装你的应用的最终用户提供支持材料。 无需登录 HTTPS (即可访问公开) 。|
|隐私链接|URL||`developer.privacyUrl`|✔|指向您的隐私策略链接 (HTTPS) 。|
|视频链接|URL|||可选|指向有关你的应用的视频的链接。|
|EULA|.doc、.pdf 等|||可选|AppSource 需要 EULA (最终用户许可协议) 作为附件提供。 如果选择不提交 EULA，将代表你提供一个 EULA。|
|服务条款|URL||`developer.termsOfServiceUrl`||指向您的服务条款的链接 (HTTPS) 。|
|测试说明|填写指向公用 URL 的内嵌或链接|||有关如何分步测试应用程序的详细测试说明。 请包含两个登录凭据，用于测试管理员和非管理员方案。|

## <a name="localized-content"></a>本地化内容

> [!NOTE]
> AppSource 计划支持以下元数据的本地化内容。 目前，你的应用一览仅在 AppSource 中以英语显示，但将在 Teams 客户端中正确本地化。 有关详细信息 [，请参阅本地化](~/concepts/build-and-test/apps-localization.md) 你的应用。

|Data|类型|Size|清单|合作伙伴中心|说明|
|---|---|---|---|---|---|
|应用名称|String|30|`name.short`|✔|应显示在店面和产品中的应用程序名称。|
|长应用名称|String|30|`name.full`|✔|应显示在店面和产品中的应用程序名称。|
|简短说明|String|80|`description.short`|✔|应用的简短说明。|
|较长说明|String|4000|`description.full`|✔|应用的详细说明。 在清单文件中，准确的摘要已足够。 在合作伙伴中心中，你可以对 AppSource 产品页面使用更丰富且格式更丰富的说明。|
|屏幕快照 (1-5) |.png、.jpg 或 .gif|1366w x 768h 和小于 1024 KB||✔|至少一个显示应用体验的屏幕截图。 在应用详细信息页面上使用。|

## <a name="submission-extras-for-bots"></a>机器人的提交额外内容

必须使用 Bot Framework 创建 Microsoft Teams 中的聊天机器人。 有关 [说明，请参阅"创建](~/bots/how-to/create-a-bot-for-teams.md) 自动程序"。 在 Bot Framework 中为自动程序图标使用 96x96 颜色图标。
