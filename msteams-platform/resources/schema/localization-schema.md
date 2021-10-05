---
title: 本地化 JSON 架构参考
description: 介绍本地化文件支持的本地化架构Microsoft Teams
ms.topic: reference
ms.localizationpriority: medium
keywords: teams 清单架构本地化
ms.date: 05/20/2019
ms.openlocfilehash: 7b9853772996764e185ed4de44683df9f5f57711
ms.sourcegitcommit: 6573881f7e69d8e5ec8861f54df84e7d519f0511
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2021
ms.locfileid: "60096533"
---
# <a name="localize-json-schema-reference"></a>本地化 JSON 架构参考

本地化Microsoft Teams介绍基于客户端语言设置提供的语言翻译。 你的文件必须符合 托管在 的架构 [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json) 。 

> [!TIP]
> 在清单的开头指定架构，以从 `IntelliSense` 代码编辑器启用或类似支持： `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",`

## <a name="example"></a>示例 

本地化 JSON 架构的示例如下所示：

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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

> [!NOTE]
>  App Studio 即将被弃用。 使用新的开发人员门户 配置、Teams和管理你的[应用程序](https://dev.teams.microsoft.com/)。

该架构定义以下属性：

|属性|类型|最大长度|说明|
|---------------|--------|---------|------------------|
|`$schema`|URI|不适用|引用 https:// JSON 架构的 URL。|
|`name.short`|String|30|将应用清单中的相应字符串替换为此处提供的值。|
|`name.full`|字符串|100|将应用清单中的相应字符串替换为此处提供的值。|
|`description.short`|String|80|将应用清单中的相应字符串替换为此处提供的值。|
|`description.full`|String|4000|将应用清单中的相应字符串替换为此处提供的值。|
|`staticTabs\\[([0-9]|1[0-5])\\]\\.name`|字符串|128|将应用清单中的相应字符串替换为此处提供的值。|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title`|String|32|将应用清单中的相应字符串替换为此处提供的值。|
|`## bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description`|String|128|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title`|String|32|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description`|String|128|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title`|String|32|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description`|String|128|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value`|String|512|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title`|String|128|将应用清单中的相应字符串替换为此处提供的值。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title`|String|64|将应用清单中的相应字符串替换为此处提供的值。|

## <a name="see-also"></a>另请参阅

> [本地化应用](~/concepts/build-and-test/apps-localization.md)
