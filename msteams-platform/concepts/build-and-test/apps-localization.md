---
title: 本地化应用
description: 介绍本地化Microsoft Teams应用的注意事项。
ms.topic: conceptual
ms.localizationpriority: medium
keywords: teams 发布应用商店办公室发布 AppSource 本地化语言
ms.date: 05/15/2018
ms.openlocfilehash: 25a7694017cc8002ac23cf7075c59488ceb9773d
ms.sourcegitcommit: 61003a14e8a179e1268bbdbd9cf5e904c5259566
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2022
ms.locfileid: "64737042"
---
# <a name="localize-your-app"></a>本地化应用

请考虑以下因素来本地化Microsoft Teams应用：

1. [本地化 AppSource 列表](#localize-your-appsource-listing)。
1. [本地化应用清单中的字符串](#localize-strings-in-your-app-manifest)。
1. [处理来自用户的本地化文本提交](#handle-localized-text-submissions-from-your-users)。

## <a name="localize-your-appsource-listing"></a>本地化 AppSource 列表

如果要将应用发布到应用商店，请提供元数据 (说明、屏幕截图、希望应用在其中列出的语言中的名称) ，并在合作伙伴中心的 **“市场列表** ”页上显式指定这些语言。 有关详细信息，请参阅 [本地化的 Microsoft AppSource 正面](/office/dev/store/prepare-localized-solutions#localized-microsoft-appsource-fronts)。 若要支持应用商店中的本地化列表，可以将其他语言添加到列表中。 在 [合作伙伴中心](/office/dev/store/submit-to-appsource-via-partner-center) 为你的列表提供的默认语言信息将显示在应用的 [AppSource 网站](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1 "AppSource 是满足团队所有需求的一个位置。将聊天、会议、通话、文件和工具等所有内容汇集在一起，以实现更高效的团队合作。") 列表中。 目前，默认语言为英语。

### <a name="configure-localization"></a>配置本地化

若要为应用配置其他语言，请在 [合作伙伴中心](/office/dev/store/submit-to-appsource-via-partner-center)选择英语和应用的其他语言。 在以下示例中，法语用作其他语言：

1. 添加英语
    * 输入应用名称。
    * 输入英语应用的简短说明。
    * 输入该应用的英文长篇说明。
    * 在长描述中，输入： **此应用以法语提供**。
    * 使用英语) Upload应用 UI (的图像。
2. 添加法语
    * 输入应用名称。
    * 输入法语应用的简短说明。
    * 输入用法语对应用的长描述。
    * 使用法语) Upload应用 UI (的图像。

使用英语上传的图像在 AppSource 中使用。

## <a name="localize-strings-in-your-app-manifest"></a>本地化应用清单中的字符串

使用Microsoft Teams应用架构`v1.5`及更高版本本地化应用。 为此，可以将 manifest.json 文件中的属性设置 `$schema` 为 `https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json` 或更高版本，并将属性更新 `manifestVersion` 为 `$schema` 本例中的版本 (`1.5`) 。

`localizationInfo`使用应用程序支持的默认语言添加该属性。 如果用户的客户端设置与任何其他语言都不匹配，则默认语言将用作最终回退语言。

### <a name="example-manifestjson-change"></a>manifest.json 更改示例

以下内容 `manifest.json` 有助于使用应用程序支持的默认语言添加 `localizationInfo` 该属性，同时 `additionalLanguages`提供以下功能：

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  "name.short": "Localización",
  "name.full": "Aplicación de localización",
  ...
}
```

可以为其他 .json 文件提供清单中所有面向用户的字符串的翻译。 这些文件必须遵循 [本地化文件 JSON 架构](../../resources/schema/localization-schema.md) ，并且必须将其添加到 `localizationInfo` 清单的属性中。 每个文件都与语言标记相关联，Teams客户端使用该标记来选择相应的字符串。 语言标记采用某种形式 `<language>-<region>` ，但可以省略 `<region>` 该部分，以面向支持所需语言的所有区域。

Teams客户端按以下顺序应用字符串：默认语言字符串 ->用户的仅限语言的字符串 ->用户的语言 + 用户的区域字符串。

例如，你提供了“fr”的默认语言 (法语、所有区域) ，以及“en” (英语的其他语言文件，所有区域) 和“en-gb” (英语、大不列颠) ，用户的语言设置为“en-gb”。 根据语言选择进行以下更改：

1. Teams客户端采用“fr”字符串，并使用“en”字符串覆盖它们。
1. 使用“en-gb”字符串覆盖“en”字符串。

如果用户的语言设置为“en-ca”，则会根据语言选择进行以下更改：

1. Teams客户端采用“fr”字符串，并使用“en”字符串覆盖它们。
1. 由于未提供“en-ca”本地化，因此会使用“en”本地化。

如果用户的语言设置为“es-es”，则Teams客户端采用“fr”字符串。 Teams客户端不会使用任何语言文件替代字符串，因为未提供“es”或“es-es”翻译。

因此，必须在清单中提供顶级的仅限语言的翻译。 例如， `en` 而不是 `en-us`. 必须仅为需要它们的少数字符串提供区域级别重写。

### <a name="example-manifestjson-change"></a>manifest.json 更改示例

以下 `manifest.json` 示例中显示了此更改：

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

 以下 `localization.json` 示例中显示了此更改：

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
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

如果提供应用程序的本地化版本，则用户会使用相同的语言进行响应。 由于Teams不会将用户提交转换回默认语言，因此应用必须处理本地化语言响应。 例如，如果提供本地化 `commandList`，则对机器人的响应是命令的本地化文本，而不是默认语言。 你的应用必须做出适当的响应。

## <a name="code-sample"></a>代码示例

| 示例名称 | Description | .NET | Node.js |
|-------------|-------------|------|------|
| 应用本地化 | 使用机器人和选项卡Microsoft Teams应用本地化。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) |

## <a name="see-also"></a>另请参阅

[本地化 JSON 架构参考](~/resources/schema/localization-schema.md)
