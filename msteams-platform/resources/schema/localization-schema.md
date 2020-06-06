---
title: 本地化文件 JSON 架构参考
description: 介绍了 Microsoft 团队本地化文件支持的本地化架构
keywords: 团队清单架构本地化
ms.date: 05/20/2019
ms.openlocfilehash: 14e08c582f065d1b09ff0f4906ca6788037460f1
ms.sourcegitcommit: 6c786434b56cc8c2765a14aa1f6149870245f309
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2020
ms.locfileid: "44590863"
---
# <a name="reference-localization-file-json-schema"></a>参考：本地化文件 JSON 架构

Microsoft 团队本地化文件介绍将根据客户端语言设置提供的语言翻译。 您的文件必须符合托管的架构 [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json) 。 有关其他信息，请参阅[应用程序本地化](~/concepts/build-and-test/apps-localization.md)。

## <a name="sample"></a>示例

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
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

架构定义了以下属性：

## <a name="schema"></a>$schema

**URI**

引用清单的 JSON 架构的 https://URL。

> [!TIP]
> 指定清单开头的架构，以从代码编辑器中启用 IntelliSense 或类似支持：`"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",`

## <a name="nameshort"></a>名称。 short

**字符串，最大长度为30**

将应用程序清单中对应的字符串替换为此处提供的值。

## <a name="namefull"></a>名称。 full

**字符串，最大长度为100**

将应用程序清单中对应的字符串替换为此处提供的值。

## <a name="descriptionshort"></a>说明。 short

**字符串，最大长度为80**

将应用程序清单中对应的字符串替换为此处提供的值。

## <a name="descriptionfull"></a>描述。 full

**字符串，最大长度为4000**

将应用程序清单中对应的字符串替换为此处提供的值。

## <a name="statictabs0-910-5name"></a>staticTabs \\ [（[0-9] | 1 [0-5]） \\ ] \\ 。名称

**字符串，最大长度为128**

将应用程序清单中对应的字符串替换为此处提供的值。

## <a name="bots0commandlists0-2commands0-9title"></a>bot \\ [0 \\ ] \\ . commandLists \\ [[0-2] \\ ] \\ . 命令 \\ [[0-9] \\ ] \\ . 标题

**字符串，最大长度为32**

将应用程序清单中对应的字符串替换为此处提供的值。

## <a name="bots0commandlists0-2commands0-9description"></a>bot \\ [0 \\ ]. \\ commandLists \\ [[0-2] \\ ] \\ . 命令 \\ [[0-9] \\ ] \\ . 说明

**字符串，最大长度为128**

将应用程序清单中对应的字符串替换为此处提供的值。

## <a name="composeextensions0commands0-9title"></a>composeExtensions \\ [0 \\ ] \\ . 命令 \\ [[0-9] \\ ] \\ . title

**字符串，最大长度为32**

将应用程序清单中对应的字符串替换为此处提供的值。

## <a name="composeextensions0commands0-9description"></a>composeExtensions \\ [0 \\ ] \\ . 命令 \\ [[0-9] \\ ] \\ . 说明

**字符串，最大长度为128**

将应用程序清单中对应的字符串替换为此处提供的值。

## <a name="composeextensions0commands0-9parameters0-4title"></a>composeExtensions \\ [0 \\ ] \\ . 命令 \\ [[0-9] \\ ] \\ . parameters \\ [[0-4] \\ ] \\ . 标题

**字符串，最大长度为32**

将应用程序清单中对应的字符串替换为此处提供的值。

## <a name="composeextensions0commands0-9parameters0-4description"></a>composeExtensions \\ [0 \\ ] \\ . 命令 \\ [[0-9] \\ ] \\ . parameters \\ [[0-4] \\ ] \\ . 说明

**字符串，最大长度为128**

将应用程序清单中对应的字符串替换为此处提供的值。

## <a name="composeextensions0commands0-9parameters0-4value"></a>composeExtensions \\ [0 \\ ] \\ . 命令 \\ [[0-9] \\ ] \\ . 参数 \\ [[0-4] \\ ] \\ . 值

**字符串，最大长度为512**

将应用程序清单中对应的字符串替换为此处提供的值。

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a>composeExtensions \\ [0 \\ ] \\ . 命令 \\ [[0-9] \\ ] \\ . parameters \\ [[0-4] \\ ] \\ . 选择 \\ [[0-9] \\ ] \\ . 标题

**字符串，最大长度为128**

将应用程序清单中对应的字符串替换为此处提供的值。

## <a name="composeextensions0commands0-9taskinfotitle"></a>composeExtensions \\ [0 \\ ] \\ . 命令 \\ [[0-9] \\ ] \\ . taskInfo \\

**字符串，最大长度为64**

将应用程序清单中对应的字符串替换为此处提供的值。