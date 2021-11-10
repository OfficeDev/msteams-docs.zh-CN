---
title: 本地化应用
description: 介绍本地化应用Microsoft Teams注意事项。
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Teams 发布应用商店 Office 发布 AppSource 本地化语言
ms.date: 05/15/2018
ms.openlocfilehash: 50dc306a5a06dd7a73a47fbcf94a8a70aa5d6aa6
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2021
ms.locfileid: "60887551"
---
# <a name="localize-your-app"></a>本地化应用

你必须考虑以下因素来本地化你的Microsoft Teams应用：

1. [本地化 AppSource 一览](#localize-your-appsource-listing)。
1. [本地化应用清单 中的字符串](#localize-strings-in-your-app-manifest)。 
1. [处理来自用户的本地化文本提交](#handle-localized-text-submissions-from-your-users)。

## <a name="localize-your-appsource-listing"></a>本地化 AppSource 一览

如果要将应用发布到应用商店，则必须注意，尚不支持本地化 AppSource 一览。 若要支持应用商店中的本地化一览，你可以向一览添加其他语言。 在合作伙伴中心中为一览 [提供](/office/dev/store/submit-to-appsource-via-partner-center) 的默认语言信息将显示在 [应用的 AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1 "AppSource 是满足团队所有需求的地方。将聊天、会议、通话、文件和工具等一切汇集在一起，以实现更高效的团队合作。") 网站一览中。 目前，默认语言为英语。

### <a name="configure-localization"></a>配置本地化

若要为应用配置其他语言，请在合作伙伴中心[](/office/dev/store/submit-to-appsource-via-partner-center)中选择英语和应用的其他语言。 在下面的示例中，法语用作其他语言：

1. 添加英语语言
    * 输入应用名称。
    * 输入以英语表示的应用的简短说明。
    * 输入英文版应用的详细说明。
    * In the long description， enter： **This app is available in French**.
    * Upload应用 UI 图像以英语 (显示) 。
2. 添加法语
    * 输入应用名称。
    * 使用法语输入应用的简短说明。
    * 使用法语输入应用的详细说明。
    * Upload法语或法语 (应用 UI) 。

使用英语上载的图像在 AppSource 中使用。

## <a name="localize-strings-in-your-app-manifest"></a>本地化应用清单中的字符串

你必须使用Microsoft Teams `v1.5` 架构和更高版本来本地化你的应用。 为此，可以将 manifest.json 文件中的属性设置为或更高，并更新属性到版本 (`$schema` **https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json** `manifestVersion` `$schema` `1.5` 在这种情况下) 。 

必须使用应用程序 `localizationInfo` 支持的默认语言添加 属性。 如果用户的客户端设置与任何其他语言不匹配，则默认语言将用作最终回退语言。

### <a name="example-manifestjson-change"></a>manifest.json 更改示例

以下 manifest.json 可帮助使用应用程序支持的默认语言以及 添加 `localizationInfo` 属性 `additionalLanguages` ：

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "localizationInfo": {
        "defaultLanguageTag": "en",
        "additionalLanguages": [
            {
                "languageTag": "es-mx",
                "file": "es-mx.json"
            }
        ]
    }
  ...
}
```

### <a name="example-localization-json-change"></a>示例本地化 .json 更改

下面是本地化 .json 的示例：

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  "name.short": "Localización",
  "name.full": "Aplicación de localización",
  ...
}
```


可以在清单中提供其他 .json 文件以及面向用户的字符串的翻译。 这些文件必须遵循本地化文件 [JSON 架构](../../resources/schema/localization-schema.md) ，并且必须添加到清单 `localizationInfo` 的 属性中。 每个文件与语言标记相关，Teams客户端使用该标记来选择适当的字符串。 语言标记采用 的形式，但可以省略 部分，以面向支持 `<language>-<region>` `<region>` 所需语言的所有区域。

Teams客户端按以下顺序应用字符串：默认语言字符串 -> 用户的语言仅字符串 -> 用户的语言 + 用户的区域字符串。

例如，你提供默认语言"fr" (法语、所有区域) 以及"en" (英语、所有地区) 和"en-gb" (英语、英国) ，用户的语言设置为"en-gb"。 将基于语言选择进行以下更改：

1. 客户端Teams"fr"字符串，然后用"en"字符串覆盖它们。
1. 使用"en-gb"字符串覆盖"en"字符串。

如果用户的语言设置为"en-ca"，则根据语言选择进行以下更改： 

1. 客户端Teams"fr"字符串，然后用"en"字符串覆盖它们。
1. 由于未提供"en-ca"本地化，因此使用"en"本地化。

如果用户的语言设置为"es-es"，则客户端Teams"fr"字符串。 由于Teams"es"或"es-es"翻译，因此客户端不会用任何语言文件替代字符串。

因此，您必须在清单中提供顶级的仅语言翻译。 例如，"en"而不是"en-us"。 您必须仅为需要这些替代的少数字符串提供区域级别替代。 

### <a name="example-manifestjson-change"></a>manifest.json 更改示例

manifest.json 更改如以下示例所示：

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

 以下示例显示了 localization.json 更改：

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

## <a name="handle-localized-text-submissions-from-your-users"></a>处理来自用户的本地化文本提交

如果你提供应用程序的本地化版本，则用户使用相同的语言进行响应。 由于Teams不会将用户提交翻译回默认语言，因此你的应用必须处理本地化语言响应。 例如，如果你提供本地化的 ，则对自动程序的响应是命令的本地化文本， `commandList` 而不是默认语言。 你的应用必须做出相应的响应。

## <a name="code-sample"></a>代码示例

| 示例名称 | 说明 | .NET | Node.js |
|-------------|-------------|------|------|
| 应用本地化 | Microsoft Teams自动程序和选项卡进行应用本地化。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) |

## <a name="see-also"></a>另请参阅

[本地化 JSON 架构参考](~/resources/schema/localization-schema.md)
