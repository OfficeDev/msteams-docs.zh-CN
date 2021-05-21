---
title: 应用的本地化
description: 介绍本地化应用Microsoft Teams注意事项。
ms.topic: conceptual
localization_priority: Normal
keywords: Teams 发布应用商店 Office 发布 AppSource 本地化语言
ms.date: 05/15/2018
ms.openlocfilehash: a55b8af97e5306843858e5844a017dd402ab3516
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566045"
---
# <a name="localization-for-microsoft-teams-apps"></a>应用程序Microsoft Teams本地化

在本地化Microsoft Teams应用时，必须考虑以下事项：

1. 如果Teams， (应用商店一) 。
1. 应用清单中面向最终用户的字符串。 例如自动程序命令。
1. 响应从用户提交的本地化文本。

## <a name="localizing-your-appsource-listing"></a>本地化 AppSource 一览

若要发布到应用商店，需要注意，尚不支持本地化 AppSource 一览。 但是，在准备支持应用商店中的本地化一览时，你可以向一览添加其他语言。 目前，只有 (在合作伙伴中心) 中为一览提供的默认语言语言信息将显示在[](/office/dev/store/submit-to-appsource-via-partner-center)[应用的 AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1)网站一览中。

### <a name="example-of-configuring-localization"></a>配置本地化的示例

若要为应用配置其他语言，请在合作伙伴中心[](/office/dev/store/submit-to-appsource-via-partner-center)中选择英语和应用的其他语言。 本示例使用法语：

1. 添加英语语言
    * 填写应用名称。
    * 以英语填写应用的简短说明。
    * 使用英语填写应用的详细说明。
    * 在详细说明中，另请添加行"此应用在"法语"中可用。
    * Upload应用 UI 图像以英语 (显示) 。
2. 添加法语
    * 填写应用名称。
    * 使用法语填写应用的简短说明。
    * 使用法语填写应用的详细说明。
    * Upload使用法语或法语 (应用 UI) 。

使用英语上传的图像将是 AppSource 中使用的图像。

## <a name="localizing-the-strings-in-your-app-manifest"></a>本地化应用清单中的字符串

你必须使用 Microsoft Teams架构 v1.5+ 来正确本地化你的应用。 为此，可以将文件上的 manifest.js`$schema` 属性设置为""，将 https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json "manifestVersion"属性更新为"1.7"。

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

可以在清单中提供其他 .json 文件以及面向用户的字符串的翻译。 这些文件必须遵循本地化文件 [JSON 架构](../../resources/schema/localization-schema.md) ，并且必须添加到清单的"localizationInfo"属性中。 每个文件与语言标记相关，Teams客户端使用它来选择适当的字符串。 语言标记采用 的形式，但建议省略 部分，以面向支持所需 <language> - <region> <region> 语言的所有区域。

客户端Teams将按以下顺序应用字符串：默认语言字符串 -> 用户的语言仅字符串 -> 用户的语言 + 用户的区域字符串。

例如，你提供默认语言"fr" (法语、所有区域) 以及"en" (英语、所有地区) 和"en-gb" (英语、大英国) 的其他语言文件。 如果用户的语言设置为"en-gb"：

1. 客户端Teams将"fr"字符串用"en"字符串覆盖它们。
2. 使用"en-gb"字符串覆盖这些字符串。

如果用户的语言设置为"en-ca"： 

1. 客户端Teams将"fr"字符串用"en"字符串覆盖它们。
2. 由于未提供"en-ca"本地化，因此将使用"en"本地化。

如果用户的语言设置为"es-es"，Teams客户端将接受"fr"字符串，并且不会用任何语言文件替代它们。

因此，强烈建议在清单 ("en"而非"en-us") 中提供顶级的仅语言翻译，并仅为需要这些翻译的一些字符串提供区域级替代。

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

## <a name="handling-localized-text-submissions-from-your-users"></a>处理来自用户的本地化文本提交

如果你提供应用程序的本地化版本，你的用户很可能将使用相同的语言进行响应。 Teams不会将用户提交翻译回默认语言，因此你的应用将需要处理此情况。 例如，如果你提供本地化的 ，则对自动程序的响应将是命令的本地化文本， `commandList` 而不是默认语言。 你的应用将需要做出相应的响应。

## <a name="code-sample"></a>代码示例

| 示例名称 | 描述 | .NET |
|-------------|-------------|------|
| 应用本地化 | Microsoft Teams自动程序和选项卡进行应用本地化。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |


