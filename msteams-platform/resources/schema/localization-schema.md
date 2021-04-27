---
title: 本地化文件 JSON 架构参考
description: 介绍 Microsoft Teams 本地化文件支持的本地化架构
ms.topic: reference
localization_priority: Normal
keywords: teams 清单架构本地化
ms.date: 05/20/2019
ms.openlocfilehash: 3e4207fb3e862eac18c80ffc49e7c5648ae05c28
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019704"
---
# <a name="reference-localization-file-json-schema"></a><span data-ttu-id="74edc-104">参考：本地化文件 JSON 架构</span><span class="sxs-lookup"><span data-stu-id="74edc-104">Reference: Localization file JSON schema</span></span>

<span data-ttu-id="74edc-105">Microsoft Teams 本地化文件介绍了将基于客户端语言设置提供的语言翻译。</span><span class="sxs-lookup"><span data-stu-id="74edc-105">The Microsoft Teams localization file describes language translations that will be served based on the client language settings.</span></span> <span data-ttu-id="74edc-106">你的文件必须符合 托管在 的架构 [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json) 。</span><span class="sxs-lookup"><span data-stu-id="74edc-106">Your file must conform to the schema hosted at [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json).</span></span> <span data-ttu-id="74edc-107">有关其他信息，请参阅 [应用本地化](~/concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="74edc-107">For additional information see [app localization](~/concepts/build-and-test/apps-localization.md).</span></span>

## <a name="sample"></a><span data-ttu-id="74edc-108">示例</span><span class="sxs-lookup"><span data-stu-id="74edc-108">Sample</span></span>

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

<span data-ttu-id="74edc-109">该架构定义以下属性：</span><span class="sxs-lookup"><span data-stu-id="74edc-109">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="74edc-110">$schema</span><span class="sxs-lookup"><span data-stu-id="74edc-110">$schema</span></span>

<span data-ttu-id="74edc-111">**URI**</span><span class="sxs-lookup"><span data-stu-id="74edc-111">**URI**</span></span>

<span data-ttu-id="74edc-112">引用 https:// JSON 架构的 URL。</span><span class="sxs-lookup"><span data-stu-id="74edc-112">The https:// URL referencing the JSON Schema for the manifest.</span></span>

> [!TIP]
> <span data-ttu-id="74edc-113">在清单的开头指定架构，以IntelliSense代码编辑器提供类似支持： `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`</span><span class="sxs-lookup"><span data-stu-id="74edc-113">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`</span></span>

## <a name="nameshort"></a><span data-ttu-id="74edc-114">name.short</span><span class="sxs-lookup"><span data-stu-id="74edc-114">name.short</span></span>

<span data-ttu-id="74edc-115">**String，最大长度 30**</span><span class="sxs-lookup"><span data-stu-id="74edc-115">**String, Max Length 30**</span></span>

<span data-ttu-id="74edc-116">将应用清单中的相应字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="74edc-116">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="namefull"></a><span data-ttu-id="74edc-117">name.full</span><span class="sxs-lookup"><span data-stu-id="74edc-117">name.full</span></span>

<span data-ttu-id="74edc-118">**String，最大长度 100**</span><span class="sxs-lookup"><span data-stu-id="74edc-118">**String, Max Length 100**</span></span>

<span data-ttu-id="74edc-119">将应用清单中的相应字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="74edc-119">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionshort"></a><span data-ttu-id="74edc-120">description.short</span><span class="sxs-lookup"><span data-stu-id="74edc-120">description.short</span></span>

<span data-ttu-id="74edc-121">**字符串，最大长度 80**</span><span class="sxs-lookup"><span data-stu-id="74edc-121">**String, Max Length 80**</span></span>

<span data-ttu-id="74edc-122">将应用清单中的相应字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="74edc-122">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionfull"></a><span data-ttu-id="74edc-123">description.full</span><span class="sxs-lookup"><span data-stu-id="74edc-123">description.full</span></span>

<span data-ttu-id="74edc-124">**String，Max Length 4000**</span><span class="sxs-lookup"><span data-stu-id="74edc-124">**String, Max Length 4000**</span></span>

<span data-ttu-id="74edc-125">将应用清单中的相应字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="74edc-125">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="statictabs0-910-5name"></a><span data-ttu-id="74edc-126">staticTabs \\ [ ([0-9]|1[0-5]) \\ ] \\ .name</span><span class="sxs-lookup"><span data-stu-id="74edc-126">staticTabs\\[([0-9]|1[0-5])\\]\\.name</span></span>

<span data-ttu-id="74edc-127">**字符串，最大长度 128**</span><span class="sxs-lookup"><span data-stu-id="74edc-127">**String, Max Length 128**</span></span>

<span data-ttu-id="74edc-128">将应用清单 () 对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="74edc-128">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9title"></a><span data-ttu-id="74edc-129">bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="74edc-129">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="74edc-130">**字符串，最大长度 32**</span><span class="sxs-lookup"><span data-stu-id="74edc-130">**String, Max Length 32**</span></span>

<span data-ttu-id="74edc-131">将应用清单 () 对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="74edc-131">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9description"></a><span data-ttu-id="74edc-132">bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="74edc-132">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="74edc-133">**字符串，最大长度 128**</span><span class="sxs-lookup"><span data-stu-id="74edc-133">**String, Max Length 128**</span></span>

<span data-ttu-id="74edc-134">将应用清单 () 对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="74edc-134">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9title"></a><span data-ttu-id="74edc-135">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="74edc-135">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="74edc-136">**字符串，最大长度 32**</span><span class="sxs-lookup"><span data-stu-id="74edc-136">**String, Max Length 32**</span></span>

<span data-ttu-id="74edc-137">将应用清单 () 对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="74edc-137">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9description"></a><span data-ttu-id="74edc-138">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="74edc-138">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="74edc-139">**字符串，最大长度 128**</span><span class="sxs-lookup"><span data-stu-id="74edc-139">**String, Max Length 128**</span></span>

<span data-ttu-id="74edc-140">将应用清单 () 对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="74edc-140">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4title"></a><span data-ttu-id="74edc-141">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="74edc-141">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title</span></span>

<span data-ttu-id="74edc-142">**字符串，最大长度 32**</span><span class="sxs-lookup"><span data-stu-id="74edc-142">**String, Max Length 32**</span></span>

<span data-ttu-id="74edc-143">将应用清单 () 对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="74edc-143">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4description"></a><span data-ttu-id="74edc-144">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="74edc-144">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description</span></span>

<span data-ttu-id="74edc-145">**字符串，最大长度 128**</span><span class="sxs-lookup"><span data-stu-id="74edc-145">**String, Max Length 128**</span></span>

<span data-ttu-id="74edc-146">将应用清单 () 对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="74edc-146">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4value"></a><span data-ttu-id="74edc-147">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .value</span><span class="sxs-lookup"><span data-stu-id="74edc-147">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value</span></span>

<span data-ttu-id="74edc-148">**字符串，最大长度 512**</span><span class="sxs-lookup"><span data-stu-id="74edc-148">**String, Max Length 512**</span></span>

<span data-ttu-id="74edc-149">将应用清单 () 对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="74edc-149">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a><span data-ttu-id="74edc-150">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .choices \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="74edc-150">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="74edc-151">**字符串，最大长度 128**</span><span class="sxs-lookup"><span data-stu-id="74edc-151">**String, Max Length 128**</span></span>

<span data-ttu-id="74edc-152">将应用清单 () 对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="74edc-152">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9taskinfotitle"></a><span data-ttu-id="74edc-153">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .taskInfo \\ .title</span><span class="sxs-lookup"><span data-stu-id="74edc-153">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title</span></span>

<span data-ttu-id="74edc-154">**字符串，最大长度 64**</span><span class="sxs-lookup"><span data-stu-id="74edc-154">**String, Max Length 64**</span></span>

<span data-ttu-id="74edc-155">将应用清单 () 对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="74edc-155">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>
