---
title: 本地化文件 JSON 架构参考
description: 介绍 Microsoft Teams 的本地化文件支持的本地化架构
ms.topic: reference
keywords: teams 清单架构本地化
ms.date: 05/20/2019
ms.openlocfilehash: 696a65de70a63e767f8fcdb040364fe90cde8716
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014598"
---
# <a name="reference-localization-file-json-schema"></a>参考：本地化文件 JSON 架构

Microsoft Teams 本地化文件描述了将基于客户端语言设置提供的语言翻译。 你的文件必须符合托管在 的架构 [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json) 。 有关其他信息，请参阅 [应用本地化](~/concepts/build-and-test/apps-localization.md)。

## <a name="sample"></a>示例

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

## <a name="schema"></a>$schema

**URI**

引用https:// JSON 架构的 URL。

> [!TIP]
> 在清单的开头指定架构，以IntelliSense代码编辑器提供类似支持： `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="nameshort"></a>name.short

**字符串，最大长度 30**

将应用清单中的相应字符串替换为此处提供的值。

## <a name="namefull"></a>name.full

**字符串，最大长度 100**

将应用清单中的相应字符串替换为此处提供的值。

## <a name="descriptionshort"></a>description.short

**字符串，最大长度 80**

将应用清单中的相应字符串替换为此处提供的值。

## <a name="descriptionfull"></a>description.full

**字符串，最大长度 4000**

将应用清单中的相应字符串替换为此处提供的值。

## <a name="statictabs0-910-5name"></a>staticTabs \\ [ ([0-9]|1[0-5]) \\ ] \\ .name

**字符串，最大长度 128**

将应用清单 () 字符串替换为此处提供的值。

## <a name="bots0commandlists0-2commands0-9title"></a>bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title

**字符串，最大长度 32**

将应用清单 () 字符串替换为此处提供的值。

## <a name="bots0commandlists0-2commands0-9description"></a>bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description

**字符串，最大长度 128**

将应用清单 () 字符串替换为此处提供的值。

## <a name="composeextensions0commands0-9title"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title

**字符串，最大长度 32**

将应用清单 () 字符串替换为此处提供的值。

## <a name="composeextensions0commands0-9description"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description

**字符串，最大长度 128**

将应用清单 () 字符串替换为此处提供的值。

## <a name="composeextensions0commands0-9parameters0-4title"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .title

**字符串，最大长度 32**

将应用清单 () 字符串替换为此处提供的值。

## <a name="composeextensions0commands0-9parameters0-4description"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .description

**字符串，最大长度 128**

将应用清单 () 字符串替换为此处提供的值。

## <a name="composeextensions0commands0-9parameters0-4value"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .value

**字符串，最大长度 512**

将应用清单 () 字符串替换为此处提供的值。

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .choices \\ [[0-9] \\ ] \\ .title

**字符串，最大长度 128**

将应用清单 () 字符串替换为此处提供的值。

## <a name="composeextensions0commands0-9taskinfotitle"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .taskInfo \\ .title

**字符串，最大长度 64**

将应用清单 () 字符串替换为此处提供的值。
