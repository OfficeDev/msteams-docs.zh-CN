---
title: 工作组应用程序的本地化
description: 介绍有关本地化应用程序的问题
keywords: 团队发布 microsoft store office 发布 AppSource 本地化语言
ms.date: 05/15/2018
ms.openlocfilehash: 30e4a2589bf5c1093723406c78cff2258554c486
ms.sourcegitcommit: 6c786434b56cc8c2765a14aa1f6149870245f309
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2020
ms.locfileid: "44590856"
---
# <a name="localization-for-microsoft-teams-apps"></a><span data-ttu-id="fa90b-104">Microsoft 团队应用程序的本地化</span><span class="sxs-lookup"><span data-stu-id="fa90b-104">Localization for Microsoft Teams apps</span></span>

<span data-ttu-id="fa90b-105">在本地化 Microsoft 团队应用程序时，需要考虑三个主要方面。</span><span class="sxs-lookup"><span data-stu-id="fa90b-105">When localizing your Microsoft Teams app there are three major areas you need to consider.</span></span>

1. <span data-ttu-id="fa90b-106">您的 AppSource 列表（如果您正在发布到应用商店）。</span><span class="sxs-lookup"><span data-stu-id="fa90b-106">Your AppSource listing (if you're publishing to the app store).</span></span>
1. <span data-ttu-id="fa90b-107">应用程序清单中面向最终用户的字符串（例如 bot 命令）。</span><span class="sxs-lookup"><span data-stu-id="fa90b-107">The end-user facing strings in your app manifest (for example bot commands).</span></span>
1. <span data-ttu-id="fa90b-108">对从用户提交的本地化文本做出响应。</span><span class="sxs-lookup"><span data-stu-id="fa90b-108">Responding to localized text submitted from your users.</span></span>

## <a name="localizing-your-appsource-listing"></a><span data-ttu-id="fa90b-109">本地化您的 AppSource 列表</span><span class="sxs-lookup"><span data-stu-id="fa90b-109">Localizing your AppSource listing</span></span>

<span data-ttu-id="fa90b-110">如果您正在发布到应用商店，您需要注意，尚不支持本地化 AppSource 列表。</span><span class="sxs-lookup"><span data-stu-id="fa90b-110">If you're publishing to the app store, you need to be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="fa90b-111">但是，在对应用商店中的本地化列表进行支持的准备过程中，可以向列表中添加其他语言。</span><span class="sxs-lookup"><span data-stu-id="fa90b-111">However, in preparation for support for localized listings in the app store you can add additional languages to your listing.</span></span> <span data-ttu-id="fa90b-112">目前，仅在[合作伙伴中心](/dev/store/use-partner-center-to-submit-to-appsource)提供的默认（英语）语言信息将显示在您的应用程序的[AppSource 网站](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1)列表中。</span><span class="sxs-lookup"><span data-stu-id="fa90b-112">Currently only the default (English) language information you provide in [Partner Center](/dev/store/use-partner-center-to-submit-to-appsource) for your listing will appear in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) listing for your app.</span></span>

<span data-ttu-id="fa90b-113">若要为您的应用程序配置其他语言，请在 "[合作伙伴中心](/dev/store/use-partner-center-to-submit-to-appsource)" 中，选择 "英语" 和 "应用程序的其他语言"。</span><span class="sxs-lookup"><span data-stu-id="fa90b-113">To configure an additional language for your app, in [Partner Center](/dev/store/use-partner-center-to-submit-to-appsource), select both English and the additional language of the app.</span></span> <span data-ttu-id="fa90b-114">在此示例中使用的是法语。</span><span class="sxs-lookup"><span data-stu-id="fa90b-114">French is used in this example.</span></span>

1. <span data-ttu-id="fa90b-115">添加英语语言</span><span class="sxs-lookup"><span data-stu-id="fa90b-115">Add English language</span></span>
    * <span data-ttu-id="fa90b-116">填写应用程序名称。</span><span class="sxs-lookup"><span data-stu-id="fa90b-116">Fill in the app name.</span></span>
    * <span data-ttu-id="fa90b-117">使用英语填写应用程序的简短说明。</span><span class="sxs-lookup"><span data-stu-id="fa90b-117">Fill in a short description of the app in English.</span></span>
    * <span data-ttu-id="fa90b-118">用英语填写应用程序的详细说明。</span><span class="sxs-lookup"><span data-stu-id="fa90b-118">Fill in the long description of the app in English.</span></span>
    * <span data-ttu-id="fa90b-119">在详细说明中，请同时添加 "此应用程序在 ' 法语 ' 中可用" 这一行。</span><span class="sxs-lookup"><span data-stu-id="fa90b-119">In the long description, please also add the line “This app is available in “French”.</span></span>
    * <span data-ttu-id="fa90b-120">上载应用程序 UI 的图像（英文）。</span><span class="sxs-lookup"><span data-stu-id="fa90b-120">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="fa90b-121">添加法语语言</span><span class="sxs-lookup"><span data-stu-id="fa90b-121">Add French language</span></span>
    * <span data-ttu-id="fa90b-122">填写应用程序名称。</span><span class="sxs-lookup"><span data-stu-id="fa90b-122">Fill in the app name.</span></span>
    * <span data-ttu-id="fa90b-123">以法语填写应用程序的简短说明。</span><span class="sxs-lookup"><span data-stu-id="fa90b-123">Fill in a short description of the app in French.</span></span>
    * <span data-ttu-id="fa90b-124">以法语填写应用程序的详细说明。</span><span class="sxs-lookup"><span data-stu-id="fa90b-124">Fill in the long description of the app in French.</span></span>
    * <span data-ttu-id="fa90b-125">上载应用程序 UI 的图像（以法语为单位）。</span><span class="sxs-lookup"><span data-stu-id="fa90b-125">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="fa90b-126">以英语语言上传的图像将是 AppSource 中使用的图像。</span><span class="sxs-lookup"><span data-stu-id="fa90b-126">The images you upload with the English language will be the ones used in AppSource.</span></span>

## <a name="localizing-the-strings-in-your-app-manifest"></a><span data-ttu-id="fa90b-127">本地化应用程序清单中的字符串</span><span class="sxs-lookup"><span data-stu-id="fa90b-127">Localizing the strings in your app manifest</span></span>

<span data-ttu-id="fa90b-128">您必须使用 Microsoft 团队应用程序架构 v1.0 + 以正确本地化您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="fa90b-128">You must use the Microsoft Teams app schema v1.5+ to properly localize your app.</span></span> <span data-ttu-id="fa90b-129">为此，可以将 `$schema` 清单. json 文件中的属性设置为 " https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json "，并将 "manifestVersion" 属性更新为 "1.5"。</span><span class="sxs-lookup"><span data-stu-id="fa90b-129">You can do this by setting the `$schema` attribute in your manifest.json file to 'https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json' and updating the 'manifestVersion' property to '1.5'.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="fa90b-130">示例清单 json 更改</span><span class="sxs-lookup"><span data-stu-id="fa90b-130">Example manifest.json change</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

<span data-ttu-id="fa90b-131">然后，您需要使用您的应用程序支持的默认语言添加 "localizationInfo" 属性。</span><span class="sxs-lookup"><span data-stu-id="fa90b-131">You will then want to add the 'localizationInfo' property with the default language that your application supports.</span></span> <span data-ttu-id="fa90b-132">如果用户的客户端设置与任何其他语言都不匹配，则将默认语言用作最终回退语言。</span><span class="sxs-lookup"><span data-stu-id="fa90b-132">The default language is used as the final fallback language if the user's client settings do not match any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="fa90b-133">示例清单 json 更改</span><span class="sxs-lookup"><span data-stu-id="fa90b-133">Example manifest.json change</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

<span data-ttu-id="fa90b-134">您可以提供附加的 json 文件，其中包含清单中所有面向用户的字符串的转换。</span><span class="sxs-lookup"><span data-stu-id="fa90b-134">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="fa90b-135">这些文件必须遵循[本地化文件 JSON 架构](../../resources/schema/localization-schema.md)，并且必须将其添加到清单的 "localizationInfo" 属性。</span><span class="sxs-lookup"><span data-stu-id="fa90b-135">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the 'localizationInfo' property of your manifest.</span></span> <span data-ttu-id="fa90b-136">每个文件都与一个语言标记相关联，团队客户端使用这些标记来选择适当的字符串。</span><span class="sxs-lookup"><span data-stu-id="fa90b-136">Each file correlates to a language tag which the Teams client uses to choose the appropriate strings.</span></span> <span data-ttu-id="fa90b-137">语言标记采用的形式为， <language> - <region> 但建议省略 <region> 部分，以面向支持所需语言的所有区域。</span><span class="sxs-lookup"><span data-stu-id="fa90b-137">The language tag takes the form of <language>-<region> but it is recommended to omit the <region> portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="fa90b-138">团队客户端将按如下顺序应用这些字符串：默认语言字符串-> 用户的语言仅为字符串-> 用户的语言 + 用户的区域字符串。</span><span class="sxs-lookup"><span data-stu-id="fa90b-138">The Teams client will apply the strings in this order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="fa90b-139">例如，您提供了默认语言 ' fr ' （法语、所有区域）和用于 ' en ' 的其他语言文件（英语、所有区域）和 ' en gb ' （英语、英国）。</span><span class="sxs-lookup"><span data-stu-id="fa90b-139">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain).</span></span> <span data-ttu-id="fa90b-140">如果用户的语言设置为 "en-gb"：</span><span class="sxs-lookup"><span data-stu-id="fa90b-140">If the user's language is set to 'en-gb':</span></span>

1. <span data-ttu-id="fa90b-141">团队客户端将使用 ' en ' 字符串将其替换为 "fr" 字符串。</span><span class="sxs-lookup"><span data-stu-id="fa90b-141">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="fa90b-142">使用 ' en gb ' 字符串覆盖这些字符串。</span><span class="sxs-lookup"><span data-stu-id="fa90b-142">Overwrite those with the 'en-gb' strings.</span></span>

<span data-ttu-id="fa90b-143">如果用户的语言设置为 "en-ca"：</span><span class="sxs-lookup"><span data-stu-id="fa90b-143">If the user's language is set to 'en-ca':</span></span> 

1. <span data-ttu-id="fa90b-144">团队客户端将使用 ' en ' 字符串将其替换为 "fr" 字符串。</span><span class="sxs-lookup"><span data-stu-id="fa90b-144">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="fa90b-145">由于未提供 "en-ca" 本地化，将使用 "en" localizations。</span><span class="sxs-lookup"><span data-stu-id="fa90b-145">Since no 'en-ca' localization is supplied, the 'en' localizations will be used.</span></span>

<span data-ttu-id="fa90b-146">如果用户的语言设置为 "es"，则团队客户端将采用 "fr" 字符串，而不会使用任何语言文件覆盖这些字符串。</span><span class="sxs-lookup"><span data-stu-id="fa90b-146">If the user's language is set to 'es-es', the Teams client will take the 'fr' strings and will not override them with any of the language files.</span></span>

<span data-ttu-id="fa90b-147">因此，强烈建议在清单中提供顶级的纯语言翻译（"en"，而不是 "en-us"），并仅为需要它们的少数几个字符串提供区域级别的重写。</span><span class="sxs-lookup"><span data-stu-id="fa90b-147">Therefore, it is strongly recommended to provide top-level, language-only translations in your manifest ('en' instead of 'en-us') and only provide region-level overrides for the few strings that need them.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="fa90b-148">示例清单 json 更改</span><span class="sxs-lookup"><span data-stu-id="fa90b-148">Example manifest.json change</span></span>

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

### <a name="example-localization-json-file"></a><span data-ttu-id="fa90b-149">示例本地化 json 文件</span><span class="sxs-lookup"><span data-stu-id="fa90b-149">Example localization .json file</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
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

## <a name="handling-localized-text-submissions-from-your-users"></a><span data-ttu-id="fa90b-150">处理用户的本地化文本提交</span><span class="sxs-lookup"><span data-stu-id="fa90b-150">Handling localized text submissions from your users</span></span>

<span data-ttu-id="fa90b-151">如果您提供了应用程序的本地化版本，则您的用户很可能会使用相同的语言进行响应。</span><span class="sxs-lookup"><span data-stu-id="fa90b-151">If your provide localized versions of your application it is very likely that your users will respond with the same language.</span></span> <span data-ttu-id="fa90b-152">团队不会将用户的提交翻译回默认语言，因此您的应用程序将需要处理该情况。</span><span class="sxs-lookup"><span data-stu-id="fa90b-152">Teams does not translate the user submissions back to the default language, so your app will need to handle that.</span></span> <span data-ttu-id="fa90b-153">例如，如果您提供本地化的 `commandList` ，则对你的 bot 的响应将是该命令的本地化文本，而不是默认语言。</span><span class="sxs-lookup"><span data-stu-id="fa90b-153">For example, if you provide a localized `commandList`, the responses to your bot will be the localized text of the command, not the default language.</span></span> <span data-ttu-id="fa90b-154">您的应用程序需要进行相应的响应。</span><span class="sxs-lookup"><span data-stu-id="fa90b-154">Your app will need to respond appropriately.</span></span>
