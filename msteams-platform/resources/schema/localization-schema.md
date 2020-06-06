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
# <a name="reference-localization-file-json-schema"></a><span data-ttu-id="fb7bb-104">参考：本地化文件 JSON 架构</span><span class="sxs-lookup"><span data-stu-id="fb7bb-104">Reference: Localization file JSON schema</span></span>

<span data-ttu-id="fb7bb-105">Microsoft 团队本地化文件介绍将根据客户端语言设置提供的语言翻译。</span><span class="sxs-lookup"><span data-stu-id="fb7bb-105">The Microsoft Teams localization file describes language translations that will be served based on the client language settings.</span></span> <span data-ttu-id="fb7bb-106">您的文件必须符合托管的架构 [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json) 。</span><span class="sxs-lookup"><span data-stu-id="fb7bb-106">Your file must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="fb7bb-107">有关其他信息，请参阅[应用程序本地化](~/concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="fb7bb-107">For additional information see [app localization](~/concepts/build-and-test/apps-localization.md).</span></span>

## <a name="sample"></a><span data-ttu-id="fb7bb-108">示例</span><span class="sxs-lookup"><span data-stu-id="fb7bb-108">Sample</span></span>

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

<span data-ttu-id="fb7bb-109">架构定义了以下属性：</span><span class="sxs-lookup"><span data-stu-id="fb7bb-109">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="fb7bb-110">$schema</span><span class="sxs-lookup"><span data-stu-id="fb7bb-110">$schema</span></span>

<span data-ttu-id="fb7bb-111">**URI**</span><span class="sxs-lookup"><span data-stu-id="fb7bb-111">**URI**</span></span>

<span data-ttu-id="fb7bb-112">引用清单的 JSON 架构的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="fb7bb-112">The https:// URL referencing the JSON Schema for the manifest.</span></span>

> [!TIP]
> <span data-ttu-id="fb7bb-113">指定清单开头的架构，以从代码编辑器中启用 IntelliSense 或类似支持：`"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",`</span><span class="sxs-lookup"><span data-stu-id="fb7bb-113">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",`</span></span>

## <a name="nameshort"></a><span data-ttu-id="fb7bb-114">名称。 short</span><span class="sxs-lookup"><span data-stu-id="fb7bb-114">name.short</span></span>

<span data-ttu-id="fb7bb-115">**字符串，最大长度为30**</span><span class="sxs-lookup"><span data-stu-id="fb7bb-115">**String, Max Length 30**</span></span>

<span data-ttu-id="fb7bb-116">将应用程序清单中对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="fb7bb-116">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="namefull"></a><span data-ttu-id="fb7bb-117">名称。 full</span><span class="sxs-lookup"><span data-stu-id="fb7bb-117">name.full</span></span>

<span data-ttu-id="fb7bb-118">**字符串，最大长度为100**</span><span class="sxs-lookup"><span data-stu-id="fb7bb-118">**String, Max Length 100**</span></span>

<span data-ttu-id="fb7bb-119">将应用程序清单中对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="fb7bb-119">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionshort"></a><span data-ttu-id="fb7bb-120">说明。 short</span><span class="sxs-lookup"><span data-stu-id="fb7bb-120">description.short</span></span>

<span data-ttu-id="fb7bb-121">**字符串，最大长度为80**</span><span class="sxs-lookup"><span data-stu-id="fb7bb-121">**String, Max Length 80**</span></span>

<span data-ttu-id="fb7bb-122">将应用程序清单中对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="fb7bb-122">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionfull"></a><span data-ttu-id="fb7bb-123">描述。 full</span><span class="sxs-lookup"><span data-stu-id="fb7bb-123">description.full</span></span>

<span data-ttu-id="fb7bb-124">**字符串，最大长度为4000**</span><span class="sxs-lookup"><span data-stu-id="fb7bb-124">**String, Max Length 4000**</span></span>

<span data-ttu-id="fb7bb-125">将应用程序清单中对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="fb7bb-125">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="statictabs0-910-5name"></a><span data-ttu-id="fb7bb-126">staticTabs \\ [（[0-9] | 1 [0-5]） \\ ] \\ 。名称</span><span class="sxs-lookup"><span data-stu-id="fb7bb-126">staticTabs\\[([0-9]|1[0-5])\\]\\.name</span></span>

<span data-ttu-id="fb7bb-127">**字符串，最大长度为128**</span><span class="sxs-lookup"><span data-stu-id="fb7bb-127">**String, Max Length 128**</span></span>

<span data-ttu-id="fb7bb-128">将应用程序清单中对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="fb7bb-128">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9title"></a><span data-ttu-id="fb7bb-129">bot \\ [0 \\ ] \\ . commandLists \\ [[0-2] \\ ] \\ . 命令 \\ [[0-9] \\ ] \\ . 标题</span><span class="sxs-lookup"><span data-stu-id="fb7bb-129">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="fb7bb-130">**字符串，最大长度为32**</span><span class="sxs-lookup"><span data-stu-id="fb7bb-130">**String, Max Length 32**</span></span>

<span data-ttu-id="fb7bb-131">将应用程序清单中对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="fb7bb-131">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9description"></a><span data-ttu-id="fb7bb-132">bot \\ [0 \\ ]. \\ commandLists \\ [[0-2] \\ ] \\ . 命令 \\ [[0-9] \\ ] \\ . 说明</span><span class="sxs-lookup"><span data-stu-id="fb7bb-132">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="fb7bb-133">**字符串，最大长度为128**</span><span class="sxs-lookup"><span data-stu-id="fb7bb-133">**String, Max Length 128**</span></span>

<span data-ttu-id="fb7bb-134">将应用程序清单中对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="fb7bb-134">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9title"></a><span data-ttu-id="fb7bb-135">composeExtensions \\ [0 \\ ] \\ . 命令 \\ [[0-9] \\ ] \\ . title</span><span class="sxs-lookup"><span data-stu-id="fb7bb-135">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="fb7bb-136">**字符串，最大长度为32**</span><span class="sxs-lookup"><span data-stu-id="fb7bb-136">**String, Max Length 32**</span></span>

<span data-ttu-id="fb7bb-137">将应用程序清单中对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="fb7bb-137">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9description"></a><span data-ttu-id="fb7bb-138">composeExtensions \\ [0 \\ ] \\ . 命令 \\ [[0-9] \\ ] \\ . 说明</span><span class="sxs-lookup"><span data-stu-id="fb7bb-138">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="fb7bb-139">**字符串，最大长度为128**</span><span class="sxs-lookup"><span data-stu-id="fb7bb-139">**String, Max Length 128**</span></span>

<span data-ttu-id="fb7bb-140">将应用程序清单中对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="fb7bb-140">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4title"></a><span data-ttu-id="fb7bb-141">composeExtensions \\ [0 \\ ] \\ . 命令 \\ [[0-9] \\ ] \\ . parameters \\ [[0-4] \\ ] \\ . 标题</span><span class="sxs-lookup"><span data-stu-id="fb7bb-141">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title</span></span>

<span data-ttu-id="fb7bb-142">**字符串，最大长度为32**</span><span class="sxs-lookup"><span data-stu-id="fb7bb-142">**String, Max Length 32**</span></span>

<span data-ttu-id="fb7bb-143">将应用程序清单中对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="fb7bb-143">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4description"></a><span data-ttu-id="fb7bb-144">composeExtensions \\ [0 \\ ] \\ . 命令 \\ [[0-9] \\ ] \\ . parameters \\ [[0-4] \\ ] \\ . 说明</span><span class="sxs-lookup"><span data-stu-id="fb7bb-144">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description</span></span>

<span data-ttu-id="fb7bb-145">**字符串，最大长度为128**</span><span class="sxs-lookup"><span data-stu-id="fb7bb-145">**String, Max Length 128**</span></span>

<span data-ttu-id="fb7bb-146">将应用程序清单中对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="fb7bb-146">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4value"></a><span data-ttu-id="fb7bb-147">composeExtensions \\ [0 \\ ] \\ . 命令 \\ [[0-9] \\ ] \\ . 参数 \\ [[0-4] \\ ] \\ . 值</span><span class="sxs-lookup"><span data-stu-id="fb7bb-147">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value</span></span>

<span data-ttu-id="fb7bb-148">**字符串，最大长度为512**</span><span class="sxs-lookup"><span data-stu-id="fb7bb-148">**String, Max Length 512**</span></span>

<span data-ttu-id="fb7bb-149">将应用程序清单中对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="fb7bb-149">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a><span data-ttu-id="fb7bb-150">composeExtensions \\ [0 \\ ] \\ . 命令 \\ [[0-9] \\ ] \\ . parameters \\ [[0-4] \\ ] \\ . 选择 \\ [[0-9] \\ ] \\ . 标题</span><span class="sxs-lookup"><span data-stu-id="fb7bb-150">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="fb7bb-151">**字符串，最大长度为128**</span><span class="sxs-lookup"><span data-stu-id="fb7bb-151">**String, Max Length 128**</span></span>

<span data-ttu-id="fb7bb-152">将应用程序清单中对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="fb7bb-152">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9taskinfotitle"></a><span data-ttu-id="fb7bb-153">composeExtensions \\ [0 \\ ] \\ . 命令 \\ [[0-9] \\ ] \\ . taskInfo \\</span><span class="sxs-lookup"><span data-stu-id="fb7bb-153">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title</span></span>

<span data-ttu-id="fb7bb-154">**字符串，最大长度为64**</span><span class="sxs-lookup"><span data-stu-id="fb7bb-154">**String, Max Length 64**</span></span>

<span data-ttu-id="fb7bb-155">将应用程序清单中对应的字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="fb7bb-155">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>