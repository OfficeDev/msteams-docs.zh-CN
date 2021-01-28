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
# <a name="reference-localization-file-json-schema"></a><span data-ttu-id="27c35-104">参考：本地化文件 JSON 架构</span><span class="sxs-lookup"><span data-stu-id="27c35-104">Reference: Localization file JSON schema</span></span>

<span data-ttu-id="27c35-105">Microsoft Teams 本地化文件描述了将基于客户端语言设置提供的语言翻译。</span><span class="sxs-lookup"><span data-stu-id="27c35-105">The Microsoft Teams localization file describes language translations that will be served based on the client language settings.</span></span> <span data-ttu-id="27c35-106">你的文件必须符合托管在 的架构 [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json) 。</span><span class="sxs-lookup"><span data-stu-id="27c35-106">Your file must conform to the schema hosted at [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json).</span></span> <span data-ttu-id="27c35-107">有关其他信息，请参阅 [应用本地化](~/concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="27c35-107">For additional information see [app localization](~/concepts/build-and-test/apps-localization.md).</span></span>

## <a name="sample"></a><span data-ttu-id="27c35-108">示例</span><span class="sxs-lookup"><span data-stu-id="27c35-108">Sample</span></span>

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

<span data-ttu-id="27c35-109">架构定义以下属性：</span><span class="sxs-lookup"><span data-stu-id="27c35-109">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="27c35-110">$schema</span><span class="sxs-lookup"><span data-stu-id="27c35-110">$schema</span></span>

<span data-ttu-id="27c35-111">**URI**</span><span class="sxs-lookup"><span data-stu-id="27c35-111">**URI**</span></span>

<span data-ttu-id="27c35-112">引用https:// JSON 架构的 URL。</span><span class="sxs-lookup"><span data-stu-id="27c35-112">The https:// URL referencing the JSON Schema for the manifest.</span></span>

> [!TIP]
> <span data-ttu-id="27c35-113">在清单的开头指定架构，以IntelliSense代码编辑器提供类似支持： `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`</span><span class="sxs-lookup"><span data-stu-id="27c35-113">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`</span></span>

## <a name="nameshort"></a><span data-ttu-id="27c35-114">name.short</span><span class="sxs-lookup"><span data-stu-id="27c35-114">name.short</span></span>

<span data-ttu-id="27c35-115">**字符串，最大长度 30**</span><span class="sxs-lookup"><span data-stu-id="27c35-115">**String, Max Length 30**</span></span>

<span data-ttu-id="27c35-116">将应用清单中的相应字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="27c35-116">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="namefull"></a><span data-ttu-id="27c35-117">name.full</span><span class="sxs-lookup"><span data-stu-id="27c35-117">name.full</span></span>

<span data-ttu-id="27c35-118">**字符串，最大长度 100**</span><span class="sxs-lookup"><span data-stu-id="27c35-118">**String, Max Length 100**</span></span>

<span data-ttu-id="27c35-119">将应用清单中的相应字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="27c35-119">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionshort"></a><span data-ttu-id="27c35-120">description.short</span><span class="sxs-lookup"><span data-stu-id="27c35-120">description.short</span></span>

<span data-ttu-id="27c35-121">**字符串，最大长度 80**</span><span class="sxs-lookup"><span data-stu-id="27c35-121">**String, Max Length 80**</span></span>

<span data-ttu-id="27c35-122">将应用清单中的相应字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="27c35-122">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionfull"></a><span data-ttu-id="27c35-123">description.full</span><span class="sxs-lookup"><span data-stu-id="27c35-123">description.full</span></span>

<span data-ttu-id="27c35-124">**字符串，最大长度 4000**</span><span class="sxs-lookup"><span data-stu-id="27c35-124">**String, Max Length 4000**</span></span>

<span data-ttu-id="27c35-125">将应用清单中的相应字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="27c35-125">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="statictabs0-910-5name"></a><span data-ttu-id="27c35-126">staticTabs \\ [ ([0-9]|1[0-5]) \\ ] \\ .name</span><span class="sxs-lookup"><span data-stu-id="27c35-126">staticTabs\\[([0-9]|1[0-5])\\]\\.name</span></span>

<span data-ttu-id="27c35-127">**字符串，最大长度 128**</span><span class="sxs-lookup"><span data-stu-id="27c35-127">**String, Max Length 128**</span></span>

<span data-ttu-id="27c35-128">将应用清单 () 字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="27c35-128">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9title"></a><span data-ttu-id="27c35-129">bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="27c35-129">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="27c35-130">**字符串，最大长度 32**</span><span class="sxs-lookup"><span data-stu-id="27c35-130">**String, Max Length 32**</span></span>

<span data-ttu-id="27c35-131">将应用清单 () 字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="27c35-131">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9description"></a><span data-ttu-id="27c35-132">bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="27c35-132">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="27c35-133">**字符串，最大长度 128**</span><span class="sxs-lookup"><span data-stu-id="27c35-133">**String, Max Length 128**</span></span>

<span data-ttu-id="27c35-134">将应用清单 () 字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="27c35-134">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9title"></a><span data-ttu-id="27c35-135">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="27c35-135">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="27c35-136">**字符串，最大长度 32**</span><span class="sxs-lookup"><span data-stu-id="27c35-136">**String, Max Length 32**</span></span>

<span data-ttu-id="27c35-137">将应用清单 () 字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="27c35-137">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9description"></a><span data-ttu-id="27c35-138">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="27c35-138">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="27c35-139">**字符串，最大长度 128**</span><span class="sxs-lookup"><span data-stu-id="27c35-139">**String, Max Length 128**</span></span>

<span data-ttu-id="27c35-140">将应用清单 () 字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="27c35-140">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4title"></a><span data-ttu-id="27c35-141">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="27c35-141">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title</span></span>

<span data-ttu-id="27c35-142">**字符串，最大长度 32**</span><span class="sxs-lookup"><span data-stu-id="27c35-142">**String, Max Length 32**</span></span>

<span data-ttu-id="27c35-143">将应用清单 () 字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="27c35-143">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4description"></a><span data-ttu-id="27c35-144">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="27c35-144">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description</span></span>

<span data-ttu-id="27c35-145">**字符串，最大长度 128**</span><span class="sxs-lookup"><span data-stu-id="27c35-145">**String, Max Length 128**</span></span>

<span data-ttu-id="27c35-146">将应用清单 () 字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="27c35-146">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4value"></a><span data-ttu-id="27c35-147">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .value</span><span class="sxs-lookup"><span data-stu-id="27c35-147">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value</span></span>

<span data-ttu-id="27c35-148">**字符串，最大长度 512**</span><span class="sxs-lookup"><span data-stu-id="27c35-148">**String, Max Length 512**</span></span>

<span data-ttu-id="27c35-149">将应用清单 () 字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="27c35-149">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a><span data-ttu-id="27c35-150">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .choices \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="27c35-150">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="27c35-151">**字符串，最大长度 128**</span><span class="sxs-lookup"><span data-stu-id="27c35-151">**String, Max Length 128**</span></span>

<span data-ttu-id="27c35-152">将应用清单 () 字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="27c35-152">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9taskinfotitle"></a><span data-ttu-id="27c35-153">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .taskInfo \\ .title</span><span class="sxs-lookup"><span data-stu-id="27c35-153">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title</span></span>

<span data-ttu-id="27c35-154">**字符串，最大长度 64**</span><span class="sxs-lookup"><span data-stu-id="27c35-154">**String, Max Length 64**</span></span>

<span data-ttu-id="27c35-155">将应用清单 () 字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="27c35-155">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>
