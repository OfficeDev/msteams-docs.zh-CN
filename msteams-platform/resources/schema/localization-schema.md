---
title: 本地化 JSON 架构参考
description: 介绍本地化文件支持的本地化架构，Microsoft Teams使用示例架构
ms.topic: reference
ms.localizationpriority: medium
keywords: teams 清单架构本地化
ms.date: 05/20/2019
ms.openlocfilehash: cbe408deb8788c9b047eb6bd954f79c73dbd057f
ms.sourcegitcommit: 2d5bdda6c52693ed682bbd543b0aa66e1feb3392
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2022
ms.locfileid: "61768390"
---
# <a name="localize-json-schema-reference"></a>本地化 JSON 架构参考

本地化Microsoft Teams介绍基于客户端语言设置提供的语言翻译。 你的文件必须符合 托管在 的架构 [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json) 。

> [!TIP]
> 在清单的开头指定架构，以从 `IntelliSense` 代码编辑器启用或类似支持： `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

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

该架构定义以下属性：

|属性|类型|最大长度|说明|
|---------------|--------|---------|------------------|
|`$schema`|URI|NA|引用 https:// JSON 架构的 URL。|
|`name.short`|String|30|将应用清单中的相应字符串替换为此处提供的值。|
|`name.full`|字符串|100|将应用清单中的相应字符串替换为此处提供的值。|
|`description.short`|String|80|将应用清单中的相应字符串替换为此处提供的值。|
|`description.full`|String|4000|将应用清单中的相应字符串替换为此处提供的值。|
|`staticTabs\\[([0-9]|1[0-5])\\]\\.name`|String|128|将应用清单中的相应字符串替换为此处提供的值。|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title`|String|32|将应用清单中的相应字符串替换为此处提供的值。|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description`|String|128|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title`|String|32|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description`|String|128|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title`|String|32|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description`|String|128|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value`|String|512|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title`|String|128|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title`|String|64|将应用清单中的相应字符串替换为此处提供的值。|
|`activities.activityTypes\\[\\b([0-9]|[1-8][0-9]|9[0-9]|1[01][0-9]|12[0-7])\\b]\\.description`|String|128|通知的简要说明|
|`activities.activityTypes\\[\\b([0-9]|[1-8][0-9]|9[0-9]|1[01][0-9]|12[0-7])\\b]\\.templateText`|String|128|例如："{actor} 已创建任务 {taskId}"|

## <a name="see-also"></a>另请参阅

[本地化应用](~/concepts/build-and-test/apps-localization.md)
