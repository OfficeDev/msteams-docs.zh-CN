---
title: 本地化 JSON 架构参考
description: 介绍本地化文件支持的本地化架构Microsoft Teams
ms.topic: reference
localization_priority: Normal
keywords: teams 清单架构本地化
ms.date: 05/20/2019
ms.openlocfilehash: 6e8f666cc6bfa693d7f2f469fc58fd6ee4860a80
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140509"
---
# <a name="localize-json-schema-reference"></a><span data-ttu-id="19249-104">本地化 JSON 架构参考</span><span class="sxs-lookup"><span data-stu-id="19249-104">Localize JSON schema reference</span></span>

<span data-ttu-id="19249-105">本地化Microsoft Teams介绍基于客户端语言设置提供的语言翻译。</span><span class="sxs-lookup"><span data-stu-id="19249-105">The Microsoft Teams localization file describes language translations that are served based on the client language settings.</span></span> <span data-ttu-id="19249-106">你的文件必须符合 托管在 的架构 [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json) 。</span><span class="sxs-lookup"><span data-stu-id="19249-106">Your file must conform to the schema hosted at [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json).</span></span> 

> [!TIP]
> <span data-ttu-id="19249-107">在清单的开头指定架构，以从 `IntelliSense` 代码编辑器启用或类似支持： `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",`</span><span class="sxs-lookup"><span data-stu-id="19249-107">Specify the schema at the beginning of your manifest to enable `IntelliSense` or similar support from your code editor: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",`</span></span>

## <a name="example"></a><span data-ttu-id="19249-108">示例</span><span class="sxs-lookup"><span data-stu-id="19249-108">Example</span></span> 

<span data-ttu-id="19249-109">本地化 JSON 架构的示例如下所示：</span><span class="sxs-lookup"><span data-stu-id="19249-109">Example of localization JSON schema is as follows:</span></span>

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

<span data-ttu-id="19249-110">该架构定义以下属性：</span><span class="sxs-lookup"><span data-stu-id="19249-110">The schema defines the following properties:</span></span>

|<span data-ttu-id="19249-111">属性</span><span class="sxs-lookup"><span data-stu-id="19249-111">Property</span></span>|<span data-ttu-id="19249-112">类型</span><span class="sxs-lookup"><span data-stu-id="19249-112">Type</span></span>|<span data-ttu-id="19249-113">最大长度</span><span class="sxs-lookup"><span data-stu-id="19249-113">Maximum length</span></span>|<span data-ttu-id="19249-114">说明</span><span class="sxs-lookup"><span data-stu-id="19249-114">Description</span></span>|
|---------------|--------|---------|------------------|
|`$schema`|<span data-ttu-id="19249-115">URI</span><span class="sxs-lookup"><span data-stu-id="19249-115">URI</span></span>|<span data-ttu-id="19249-116">不适用</span><span class="sxs-lookup"><span data-stu-id="19249-116">NA</span></span>|<span data-ttu-id="19249-117">引用 https:// JSON 架构的 URL。</span><span class="sxs-lookup"><span data-stu-id="19249-117">The https:// URL referencing the JSON Schema for the manifest.</span></span>|
|`name.short`|<span data-ttu-id="19249-118">String</span><span class="sxs-lookup"><span data-stu-id="19249-118">String</span></span>|<span data-ttu-id="19249-119">30</span><span class="sxs-lookup"><span data-stu-id="19249-119">30</span></span>|<span data-ttu-id="19249-120">将应用清单中的相应字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="19249-120">Replaces the corresponding string from the app manifest with the value provided here.</span></span>|
|`name.full`|<span data-ttu-id="19249-121">字符串</span><span class="sxs-lookup"><span data-stu-id="19249-121">String</span></span>|<span data-ttu-id="19249-122">100</span><span class="sxs-lookup"><span data-stu-id="19249-122">100</span></span>|<span data-ttu-id="19249-123">将应用清单中的相应字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="19249-123">Replaces the corresponding string from the app manifest with the value provided here.</span></span>|
|`description.short`|<span data-ttu-id="19249-124">String</span><span class="sxs-lookup"><span data-stu-id="19249-124">String</span></span>|<span data-ttu-id="19249-125">80</span><span class="sxs-lookup"><span data-stu-id="19249-125">80</span></span>|<span data-ttu-id="19249-126">将应用清单中的相应字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="19249-126">Replaces the corresponding string from the app manifest with the value provided here.</span></span>|
|`description.full`|<span data-ttu-id="19249-127">String</span><span class="sxs-lookup"><span data-stu-id="19249-127">String</span></span>|<span data-ttu-id="19249-128">4000</span><span class="sxs-lookup"><span data-stu-id="19249-128">4000</span></span>|<span data-ttu-id="19249-129">将应用清单中的相应字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="19249-129">Replaces the corresponding string from the app manifest with the value provided here.</span></span>|
|`staticTabs\\[([0-9]|1[0-5])\\]\\.name`|<span data-ttu-id="19249-130">String</span><span class="sxs-lookup"><span data-stu-id="19249-130">String</span></span>|<span data-ttu-id="19249-131">128</span><span class="sxs-lookup"><span data-stu-id="19249-131">128</span></span>|<span data-ttu-id="19249-132">将应用清单中的相应字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="19249-132">Replaces the corresponding strings from the app manifest with the value provided here.</span></span>|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title`|<span data-ttu-id="19249-133">String</span><span class="sxs-lookup"><span data-stu-id="19249-133">String</span></span>|<span data-ttu-id="19249-134">32</span><span class="sxs-lookup"><span data-stu-id="19249-134">32</span></span>|<span data-ttu-id="19249-135">将应用清单中的相应字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="19249-135">Replaces the corresponding strings from the app manifest with the value provided here.</span></span>|
|`## bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description`|<span data-ttu-id="19249-136">String</span><span class="sxs-lookup"><span data-stu-id="19249-136">String</span></span>|<span data-ttu-id="19249-137">128</span><span class="sxs-lookup"><span data-stu-id="19249-137">128</span></span>|<span data-ttu-id="19249-138">将应用清单中的相应字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="19249-138">Replaces the corresponding strings from the app manifest with the value provided here.</span></span>|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title`|<span data-ttu-id="19249-139">String</span><span class="sxs-lookup"><span data-stu-id="19249-139">String</span></span>|<span data-ttu-id="19249-140">32</span><span class="sxs-lookup"><span data-stu-id="19249-140">32</span></span>|<span data-ttu-id="19249-141">将应用清单中的相应字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="19249-141">Replaces the corresponding strings from the app manifest with the value provided here.</span></span>|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description`|<span data-ttu-id="19249-142">String</span><span class="sxs-lookup"><span data-stu-id="19249-142">String</span></span>|<span data-ttu-id="19249-143">128</span><span class="sxs-lookup"><span data-stu-id="19249-143">128</span></span>|<span data-ttu-id="19249-144">将应用清单中的相应字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="19249-144">Replaces the corresponding strings from the app manifest with the value provided here.</span></span>|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title`|<span data-ttu-id="19249-145">String</span><span class="sxs-lookup"><span data-stu-id="19249-145">String</span></span>|<span data-ttu-id="19249-146">32</span><span class="sxs-lookup"><span data-stu-id="19249-146">32</span></span>|<span data-ttu-id="19249-147">将应用清单中的相应字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="19249-147">Replaces the corresponding string from the app manifest with the value provided here.</span></span>|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description`|<span data-ttu-id="19249-148">String</span><span class="sxs-lookup"><span data-stu-id="19249-148">String</span></span>|<span data-ttu-id="19249-149">128</span><span class="sxs-lookup"><span data-stu-id="19249-149">128</span></span>|<span data-ttu-id="19249-150">将应用清单中的相应字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="19249-150">Replaces the corresponding strings from the app manifest with the value provided here.</span></span>|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value`|<span data-ttu-id="19249-151">String</span><span class="sxs-lookup"><span data-stu-id="19249-151">String</span></span>|<span data-ttu-id="19249-152">512</span><span class="sxs-lookup"><span data-stu-id="19249-152">512</span></span>|<span data-ttu-id="19249-153">将应用清单中的相应字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="19249-153">Replaces the corresponding string from the app manifest with the value provided here.</span></span>|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title`|<span data-ttu-id="19249-154">String</span><span class="sxs-lookup"><span data-stu-id="19249-154">String</span></span>|<span data-ttu-id="19249-155">128</span><span class="sxs-lookup"><span data-stu-id="19249-155">128</span></span>|<span data-ttu-id="19249-156">将应用清单中的相应字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="19249-156">Replaces the corresponding strings from the app manifest with the value provided here.</span></span>|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title`|<span data-ttu-id="19249-157">String</span><span class="sxs-lookup"><span data-stu-id="19249-157">String</span></span>|<span data-ttu-id="19249-158">64</span><span class="sxs-lookup"><span data-stu-id="19249-158">64</span></span>|<span data-ttu-id="19249-159">将应用清单中的相应字符串替换为此处提供的值。</span><span class="sxs-lookup"><span data-stu-id="19249-159">Replaces the corresponding strings from the app manifest with the value provided here.</span></span>|

## <a name="see-also"></a><span data-ttu-id="19249-160">另请参阅</span><span class="sxs-lookup"><span data-stu-id="19249-160">See also</span></span>

> [<span data-ttu-id="19249-161">本地化应用</span><span class="sxs-lookup"><span data-stu-id="19249-161">Localize your app</span></span>](~/concepts/build-and-test/apps-localization.md)
