---
title: 本地化 JSON 架构参考
description: 使用示例架构介绍 Microsoft Teams 本地化文件支持的本地化架构
ms.topic: reference
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: 23d02e845e4fcdc1c2fc76d8e9c376479fe1fa1f
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144274"
---
# <a name="localize-json-schema-reference"></a>本地化 JSON 架构参考

Microsoft Teams 本地化文件介绍了基于客户端语言设置提供的语言翻译。 文件必须符合托管在 [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json)的架构。

> [!TIP]
> 在清单开头指定架构以启用 `IntelliSense` 或提供类似的支持，使用你的代码编辑器：`"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="example"></a>示例

本地化 JSON 架构的示例如下所示：

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "name.short": "Le App Studio",
  "name.full": "App Studio pour Microsoft Teams",
  "description.short": "Créez d'excellentes applications pour Microsoft Teams avec App Studio.",
  "description.full": "Créez de nouvelles applications Microsoft Teams, concevez et prévisualisez des cartes bot, et explorez la documentation avec App Studio.",
  "staticTabs[0].name": "Editeur de manifest",
  "staticTabs[1].name": "Editeur de cartes",
  "staticTabs[2].name": "Bibliothèque de contrôles",
  "bots[0].commandLists[0].commands[0].title": "chercher",
  "bots[0].commandLists[0].commands[0].description": "Rechercher la documentation Teams pertinente"
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
|`staticTabs\\[([0-9]|1[0-5])\\]\\.name`|String|128|将应用清单中的相应字符串替换为此处提供的值。|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title`|String|32|将应用清单中的相应字符串替换为此处提供的值。|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description`|String|128|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title`|String|32|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description`|String|128|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title`|String|32|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description`|String|128|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value`|String|512|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title`|字符串|128|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title`|String|64|将应用清单中的相应字符串替换为此处提供的值。|
|`activities.activityTypes\\[\\b([0-9]|[1-8][0-9]|9[0-9]|1[01][0-9]|12[0-7])\\b]\\.description`|String|128|通知的简要说明|
|`activities.activityTypes\\[\\b([0-9]|[1-8][0-9]|9[0-9]|1[01][0-9]|12[0-7])\\b]\\.templateText`|String|128|例如："{actor} 为你创建了任务 {taskId}"|

## <a name="see-also"></a>另请参阅

[本地化应用](~/concepts/build-and-test/apps-localization.md)
