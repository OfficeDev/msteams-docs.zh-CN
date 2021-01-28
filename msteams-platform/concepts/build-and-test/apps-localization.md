---
title: 应用的本地化
description: 介绍本地化 Microsoft Teams 应用的注意事项。
ms.topic: conceptual
keywords: teams 发布应用商店 Office 发布 AppSource 本地化语言
ms.date: 05/15/2018
ms.openlocfilehash: 69bee0ee11238dc0e461e4fddf8ed01f0cfcccde
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014297"
---
# <a name="localization-for-microsoft-teams-apps"></a>Microsoft Teams 应用的本地化

本地化 Microsoft Teams 应用时，需要考虑三个主要方面。

1. 如果你要发布到 (应用商店，AppSource 一览) 。
1. 应用清单中面向最终用户的字符串 (自动程序命令) 。
1. 响应从用户提交的本地化文本。

## <a name="localizing-your-appsource-listing"></a>本地化 AppSource 一览

如果你要发布到应用商店，你需要知道本地化 AppSource 一览尚不受支持。 但是，在准备在应用商店中支持本地化一览时，你可以向一览添加其他语言。 目前，在合作伙伴中心 (一览) 中提供的默认英语和语言信息将显示在应用的[](/office/dev/store/submit-to-appsource-via-partner-center) [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1)网站一览中。

若要为应用配置其他语言，请在合作伙伴 [中心](/office/dev/store/submit-to-appsource-via-partner-center)中选择英语以及应用的其他语言。 本示例使用法语。

1. 添加英语
    * 填写应用名称。
    * 以英语填写应用的简短说明。
    * 以英语填写应用的详细说明。
    * 在详细说明中，还要添加行"此应用在"法语"中可用。
    * 以英语或英语 (应用 UI) 。
2. 添加法语
    * 填写应用名称。
    * 使用法语填写应用的简短说明。
    * 使用法语填写应用的详细说明。
    * 使用法语上传应用 UI (图像) 。

使用英语上传的图像将是 AppSource 中使用的图像。

## <a name="localizing-the-strings-in-your-app-manifest"></a>本地化应用清单中的字符串

必须使用 Microsoft Teams 应用架构 v1.5+ 来正确本地化你的应用。 为此，可以将文件上的 manifest.js`$schema` 属性设置为 https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json "'"，将"manifestVersion"属性更新为"1.7"。

### <a name="example-manifestjson-change"></a>更改manifest.js示例

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

然后，您需要使用应用程序支持的默认语言添加"localizationInfo"属性。 如果用户的客户端设置与任何其他语言不匹配，则默认语言将用作最终回退语言。

### <a name="example-manifestjson-change"></a>更改manifest.js示例

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

可以在清单中提供包含面向用户的字符串的翻译的其他 .json 文件。 这些文件必须遵守本地化文件 [JSON 架构](../../resources/schema/localization-schema.md) ，并且必须添加到清单的"localizationInfo"属性中。 每个文件与 Teams 客户端用来选择相应字符串的语言标记相关。 语言标记采用其形式，但建议省略该部分，以面向支持所需 <language> - <region> <region> 语言的所有区域。

Teams 客户端将按以下顺序应用字符串：默认语言字符串 -> 用户的语言仅字符串 -> 用户的语言 + 用户的区域字符串。

例如，你提供默认语言"fr" (法语、所有区域) 以及"en" (英语的其他语言文件、所有地区的) 和"en-gb" (英语、英国) 。 如果用户的语言设置为"en-gb"：

1. Teams 客户端将接受"fr"字符串，用"en"字符串覆盖它们。
2. 使用"en-gb"字符串覆盖这些字符串。

如果用户的语言设置为"en-ca"： 

1. Teams 客户端将接受"fr"字符串，用"en"字符串覆盖它们。
2. 由于未提供"en-ca"本地化，因此将使用"en"本地化。

如果用户的语言设置为"es-es"，Teams 客户端将接受"fr"字符串，并且不会用任何语言文件替代它们。

因此，强烈建议在清单 ("en"（而不是"en-us") ）中提供顶级的仅语言翻译，并仅为需要这些翻译的少数字符串提供区域级别的替代。

### <a name="example-manifestjson-change"></a>更改manifest.js示例

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en",
    "additionalLanguages": [
      {
        "languageTag": "en-gb",
        "file": "en-gb.json"
      },
      {
        "languageTag": "fr",
        "file": "fr.json"
      },
      {
        "languageTag": "pl",
        "file": "pl.json"
      }
    ]
  }
  ...
}
```

### <a name="example-localization-json-file"></a>示例本地化 .json 文件

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "name.short": "Le App",
  "name.full": "App pour Microsoft Teams",
  "description.short": "Créez d'excellentes applications pour Microsoft Teams avec App.",
  "description.full": "Créez de nouvelles applications Microsoft Teams, concevez et prévisualisez des cartes bot, et explorez la documentation avec App.",
  "staticTabs[0].name": "Editeur de manifest",
  "staticTabs[1].name": "Editeur de cartes",
  "staticTabs[2].name": "Bibliothèque de contrôles",
  "bots[0].commandLists[0].commands[0].title": "chercher",
  "bots[0].commandLists[0].commands[0].description": "Rechercher la documentation Teams pertinente"
}
```

## <a name="handling-localized-text-submissions-from-your-users"></a>处理用户的本地化文本提交

如果你提供应用程序的本地化版本，你的用户很可能将使用相同的语言进行响应。 Teams 不会将用户提交翻译回默认语言，因此你的应用将需要处理这一问题。 例如，如果你提供本地化后，对自动程序的响应将是命令的本地化文本， `commandList` 而不是默认语言。 你的应用将需要做出相应的响应。
