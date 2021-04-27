---
title: 应用的本地化
description: 介绍本地化 Microsoft Teams 应用的注意事项。
ms.topic: conceptual
localization_priority: Normal
keywords: Teams 发布应用商店 Office 发布 AppSource 本地化语言
ms.date: 05/15/2018
ms.openlocfilehash: 8490230ad0b268d402a9ad7deb5f8b1e3f420f9d
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020847"
---
# <a name="localization-for-microsoft-teams-apps"></a><span data-ttu-id="dccd8-104">Microsoft Teams 应用的本地化</span><span class="sxs-lookup"><span data-stu-id="dccd8-104">Localization for Microsoft Teams apps</span></span>

<span data-ttu-id="dccd8-105">本地化 Microsoft Teams 应用时，需要考虑三个主要方面。</span><span class="sxs-lookup"><span data-stu-id="dccd8-105">When localizing your Microsoft Teams app there are three major areas you need to consider.</span></span>

1. <span data-ttu-id="dccd8-106">如果你发布到 (应用商店，AppSource 一览) 。</span><span class="sxs-lookup"><span data-stu-id="dccd8-106">Your AppSource listing (if you're publishing to the app store).</span></span>
1. <span data-ttu-id="dccd8-107">应用清单中面向最终用户的字符串 (自动程序命令) 。</span><span class="sxs-lookup"><span data-stu-id="dccd8-107">The end-user facing strings in your app manifest (for example bot commands).</span></span>
1. <span data-ttu-id="dccd8-108">响应从用户提交的本地化文本。</span><span class="sxs-lookup"><span data-stu-id="dccd8-108">Responding to localized text submitted from your users.</span></span>

## <a name="localizing-your-appsource-listing"></a><span data-ttu-id="dccd8-109">本地化 AppSource 一览</span><span class="sxs-lookup"><span data-stu-id="dccd8-109">Localizing your AppSource listing</span></span>

<span data-ttu-id="dccd8-110">若要发布到应用商店，需要注意，尚不支持本地化 AppSource 一览。</span><span class="sxs-lookup"><span data-stu-id="dccd8-110">If you're publishing to the app store, you need to be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="dccd8-111">但是，在准备支持应用商店中的本地化一览时，你可以向一览添加其他语言。</span><span class="sxs-lookup"><span data-stu-id="dccd8-111">However, in preparation for support for localized listings in the app store you can add additional languages to your listing.</span></span> <span data-ttu-id="dccd8-112">目前，只有 (在合作伙伴中心) 中为一览提供的默认语言语言信息将显示在[](/office/dev/store/submit-to-appsource-via-partner-center)[应用的 AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1)网站一览中。</span><span class="sxs-lookup"><span data-stu-id="dccd8-112">Currently only the default (English) language information you provide in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) for your listing will appear in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) listing for your app.</span></span>

<span data-ttu-id="dccd8-113">若要为应用配置其他语言，请在合作伙伴中心[](/office/dev/store/submit-to-appsource-via-partner-center)中选择英语和应用的其他语言。</span><span class="sxs-lookup"><span data-stu-id="dccd8-113">To configure an additional language for your app, in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center), select both English and the additional language of the app.</span></span> <span data-ttu-id="dccd8-114">本示例使用法语。</span><span class="sxs-lookup"><span data-stu-id="dccd8-114">French is used in this example.</span></span>

1. <span data-ttu-id="dccd8-115">添加英语语言</span><span class="sxs-lookup"><span data-stu-id="dccd8-115">Add English language</span></span>
    * <span data-ttu-id="dccd8-116">填写应用名称。</span><span class="sxs-lookup"><span data-stu-id="dccd8-116">Fill in the app name.</span></span>
    * <span data-ttu-id="dccd8-117">以英语填写应用的简短说明。</span><span class="sxs-lookup"><span data-stu-id="dccd8-117">Fill in a short description of the app in English.</span></span>
    * <span data-ttu-id="dccd8-118">使用英语填写应用的详细说明。</span><span class="sxs-lookup"><span data-stu-id="dccd8-118">Fill in the long description of the app in English.</span></span>
    * <span data-ttu-id="dccd8-119">在详细说明中，另请添加行"此应用在"法语"中可用。</span><span class="sxs-lookup"><span data-stu-id="dccd8-119">In the long description, please also add the line “This app is available in “French”.</span></span>
    * <span data-ttu-id="dccd8-120">将应用 UI 图像以英语 (上传) 。</span><span class="sxs-lookup"><span data-stu-id="dccd8-120">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="dccd8-121">添加法语</span><span class="sxs-lookup"><span data-stu-id="dccd8-121">Add French language</span></span>
    * <span data-ttu-id="dccd8-122">填写应用名称。</span><span class="sxs-lookup"><span data-stu-id="dccd8-122">Fill in the app name.</span></span>
    * <span data-ttu-id="dccd8-123">使用法语填写应用的简短说明。</span><span class="sxs-lookup"><span data-stu-id="dccd8-123">Fill in a short description of the app in French.</span></span>
    * <span data-ttu-id="dccd8-124">使用法语填写应用的详细说明。</span><span class="sxs-lookup"><span data-stu-id="dccd8-124">Fill in the long description of the app in French.</span></span>
    * <span data-ttu-id="dccd8-125">使用法语或法语 (应用 UI) 。</span><span class="sxs-lookup"><span data-stu-id="dccd8-125">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="dccd8-126">使用英语上传的图像将是 AppSource 中使用的图像。</span><span class="sxs-lookup"><span data-stu-id="dccd8-126">The images you upload with the English language will be the ones used in AppSource.</span></span>

## <a name="localizing-the-strings-in-your-app-manifest"></a><span data-ttu-id="dccd8-127">本地化应用清单中的字符串</span><span class="sxs-lookup"><span data-stu-id="dccd8-127">Localizing the strings in your app manifest</span></span>

<span data-ttu-id="dccd8-128">必须使用 Microsoft Teams 应用架构 v1.5+ 来正确本地化你的应用。</span><span class="sxs-lookup"><span data-stu-id="dccd8-128">You must use the Microsoft Teams app schema v1.5+ to properly localize your app.</span></span> <span data-ttu-id="dccd8-129">为此，可以将文件上的 manifest.js`$schema` 属性设置为""，将 https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json "manifestVersion"属性更新为"1.7"。</span><span class="sxs-lookup"><span data-stu-id="dccd8-129">You can do this by setting the `$schema` attribute in your manifest.json file to 'https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json' and updating the 'manifestVersion' property to '1.7'.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="dccd8-130">更改manifest.js示例</span><span class="sxs-lookup"><span data-stu-id="dccd8-130">Example manifest.json change</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

<span data-ttu-id="dccd8-131">然后，您需要使用应用程序支持的默认语言添加"localizationInfo"属性。</span><span class="sxs-lookup"><span data-stu-id="dccd8-131">You will then want to add the 'localizationInfo' property with the default language that your application supports.</span></span> <span data-ttu-id="dccd8-132">如果用户的客户端设置与任何其他语言不匹配，则默认语言将用作最终回退语言。</span><span class="sxs-lookup"><span data-stu-id="dccd8-132">The default language is used as the final fallback language if the user's client settings do not match any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="dccd8-133">更改manifest.js示例</span><span class="sxs-lookup"><span data-stu-id="dccd8-133">Example manifest.json change</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

<span data-ttu-id="dccd8-134">可以在清单中提供其他 .json 文件以及面向用户的字符串的翻译。</span><span class="sxs-lookup"><span data-stu-id="dccd8-134">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="dccd8-135">这些文件必须遵循本地化文件 [JSON 架构](../../resources/schema/localization-schema.md) ，并且必须添加到清单的"localizationInfo"属性中。</span><span class="sxs-lookup"><span data-stu-id="dccd8-135">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the 'localizationInfo' property of your manifest.</span></span> <span data-ttu-id="dccd8-136">每个文件与 Teams 客户端用来选择相应字符串的语言标记相关。</span><span class="sxs-lookup"><span data-stu-id="dccd8-136">Each file correlates to a language tag which the Teams client uses to choose the appropriate strings.</span></span> <span data-ttu-id="dccd8-137">语言标记采用 的形式，但建议省略 部分，以面向支持所需 <language> - <region> <region> 语言的所有区域。</span><span class="sxs-lookup"><span data-stu-id="dccd8-137">The language tag takes the form of <language>-<region> but it is recommended to omit the <region> portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="dccd8-138">Teams 客户端将按以下顺序应用字符串：默认语言字符串 ->用户的语言仅包含字符串 -> 用户的语言 + 用户的区域字符串。</span><span class="sxs-lookup"><span data-stu-id="dccd8-138">The Teams client will apply the strings in this order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="dccd8-139">例如，你提供默认语言"fr" (法语、所有区域) 以及"en" (英语、所有地区) 和"en-gb" (英语、大英国) 的其他语言文件。</span><span class="sxs-lookup"><span data-stu-id="dccd8-139">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain).</span></span> <span data-ttu-id="dccd8-140">如果用户的语言设置为"en-gb"：</span><span class="sxs-lookup"><span data-stu-id="dccd8-140">If the user's language is set to 'en-gb':</span></span>

1. <span data-ttu-id="dccd8-141">Teams 客户端将"fr"字符串用"en"字符串覆盖它们。</span><span class="sxs-lookup"><span data-stu-id="dccd8-141">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="dccd8-142">使用"en-gb"字符串覆盖这些字符串。</span><span class="sxs-lookup"><span data-stu-id="dccd8-142">Overwrite those with the 'en-gb' strings.</span></span>

<span data-ttu-id="dccd8-143">如果用户的语言设置为"en-ca"：</span><span class="sxs-lookup"><span data-stu-id="dccd8-143">If the user's language is set to 'en-ca':</span></span> 

1. <span data-ttu-id="dccd8-144">Teams 客户端将"fr"字符串用"en"字符串覆盖它们。</span><span class="sxs-lookup"><span data-stu-id="dccd8-144">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="dccd8-145">由于未提供"en-ca"本地化，因此将使用"en"本地化。</span><span class="sxs-lookup"><span data-stu-id="dccd8-145">Since no 'en-ca' localization is supplied, the 'en' localizations will be used.</span></span>

<span data-ttu-id="dccd8-146">如果用户的语言设置为"es-es"，Teams 客户端将接受"fr"字符串，并且不会用任何语言文件替代它们。</span><span class="sxs-lookup"><span data-stu-id="dccd8-146">If the user's language is set to 'es-es', the Teams client will take the 'fr' strings and will not override them with any of the language files.</span></span>

<span data-ttu-id="dccd8-147">因此，强烈建议在清单 ("en"而非"en-us") 中提供顶级的仅语言翻译，并仅为需要这些翻译的一些字符串提供区域级替代。</span><span class="sxs-lookup"><span data-stu-id="dccd8-147">Therefore, it is strongly recommended to provide top-level, language-only translations in your manifest ('en' instead of 'en-us') and only provide region-level overrides for the few strings that need them.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="dccd8-148">更改manifest.js示例</span><span class="sxs-lookup"><span data-stu-id="dccd8-148">Example manifest.json change</span></span>

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

### <a name="example-localization-json-file"></a><span data-ttu-id="dccd8-149">示例本地化 .json 文件</span><span class="sxs-lookup"><span data-stu-id="dccd8-149">Example localization .json file</span></span>

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

## <a name="handling-localized-text-submissions-from-your-users"></a><span data-ttu-id="dccd8-150">处理来自用户的本地化文本提交</span><span class="sxs-lookup"><span data-stu-id="dccd8-150">Handling localized text submissions from your users</span></span>

<span data-ttu-id="dccd8-151">如果你提供应用程序的本地化版本，你的用户很可能将使用相同的语言进行响应。</span><span class="sxs-lookup"><span data-stu-id="dccd8-151">If your provide localized versions of your application it is very likely that your users will respond with the same language.</span></span> <span data-ttu-id="dccd8-152">Teams 不会将用户提交翻译回默认语言，因此你的应用将需要处理此情况。</span><span class="sxs-lookup"><span data-stu-id="dccd8-152">Teams does not translate the user submissions back to the default language, so your app will need to handle that.</span></span> <span data-ttu-id="dccd8-153">例如，如果你提供本地化的 ，则对自动程序的响应将是命令的本地化文本， `commandList` 而不是默认语言。</span><span class="sxs-lookup"><span data-stu-id="dccd8-153">For example, if you provide a localized `commandList`, the responses to your bot will be the localized text of the command, not the default language.</span></span> <span data-ttu-id="dccd8-154">你的应用将需要做出相应的响应。</span><span class="sxs-lookup"><span data-stu-id="dccd8-154">Your app will need to respond appropriately.</span></span>
