---
title: 本地化 JSON 架构参考
description: 使用示例架构介绍 Microsoft Teams 本地化文件支持的本地化架构
ms.topic: reference
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: f4ffd9a4b722ccc414f70b19e3020ab39d1ce779
ms.sourcegitcommit: 69a45722c5c09477bbff3ba1520e6c81d2d2d997
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/11/2022
ms.locfileid: "67311944"
---
# <a name="localize-json-schema-reference"></a>本地化 JSON 架构参考

Microsoft Teams 本地化文件介绍了基于客户端语言设置提供的语言翻译。 文件必须符合托管在 [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json)的架构。

> [!TIP]
> 在清单开头指定架构以启用 `IntelliSense` 或提供类似的支持，使用你的代码编辑器：`"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="example"></a>示例

本地化 JSON 架构的示例如下所示：

```json
{
    "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.9/MicrosoftTeams.Localization.schema.json",
    "name.short": "Portail de Développement",
    "name.full": "Portail des développeurs",
    "description.short": "Configurer, distribuer et gérer vos applications Microsoft Teams",
    "description.full": "Anciennement App Studio, le portail des développeurs peut vous aider où que vous soyez dans votre parcours de développement d’applications Microsoft Teams.1. Configurez une nouvelle application ou importez une application existante.2. Configurez les fonctionnalités de votre application et d’autres métadonnées importantes.3. Obtenez des ressources pour vous aider à créer une application de haute qualité.3. Testez votre application directement dans Teams.4. Distribuez votre application dans votre organisation ou dans le Store Teams.5. Analysez l’utilisation, l’engagement et d’autres informations sur votre application. Le portail inclut également des outils pour concevoir des scènes virtuelles personnalisées, des cartes adaptatives et l’intégration à la Plateforme d’identités Microsoft.",
    "staticTabs[0].name": "Accueil",
    "staticTabs[1].name": "Applications",
    "staticTabs[2].name": "Outils",
    "staticTabs[3].name": "Developer Portal",
    "bots[0].commandLists[0].commands[0].title": "Rechercher",
    "bots[0].commandLists[0].commands[0].description": "Rechercher la documentation Teams appropriée"
}
```

架构定义以下属性：

|属性|类型|最大长度|说明|
|---------------|--------|---------|------------------|
|`$schema`|URI|不适用|引用清单的 JSON 架构的 https:// URL。|
|`name.short`|字符串|30|将应用清单中的相应字符串替换为此处提供的值。|
|`name.full`|字符串|100|将应用清单中的相应字符串替换为此处提供的值。|
|`description.short`|String|80|将应用清单中的相应字符串替换为此处提供的值。|
|`description.full`|字符串|4000|将应用清单中的相应字符串替换为此处提供的值。|
|`staticTabs\\[([0-9]|1[0-5])\\]\\.name`|字符串|128|将应用清单中的相应字符串替换为此处提供的值。|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title`|String|32|将应用清单中的相应字符串替换为此处提供的值。|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description`|String|128|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title`|String|32|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description`|String|128|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title`|String|32|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description`|字符串|128|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value`|String|512|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title`|字符串|128|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title`|String|64|将应用清单中的相应字符串替换为此处提供的值。|
|`activities.activityTypes\\[\\b([0-9]|[1-8][0-9]|9[0-9]|1[01][0-9]|12[0-7])\\b]\\.description`|String|128|通知的简要说明|
|`activities.activityTypes\\[\\b([0-9]|[1-8][0-9]|9[0-9]|1[01][0-9]|12[0-7])\\b]\\.templateText`|String|128|例如："{actor} 为你创建了任务 {taskId}"|

## <a name="see-also"></a>另请参阅

[本地化应用](~/concepts/build-and-test/apps-localization.md)
