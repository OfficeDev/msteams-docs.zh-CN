---
title: 本地化应用
description: 介绍本地化应用Microsoft Teams注意事项。
ms.topic: conceptual
localization_priority: Normal
keywords: Teams 发布应用商店 Office 发布 AppSource 本地化语言
ms.date: 05/15/2018
ms.openlocfilehash: c73188bb24960b9ef0706955d09d23b618c04e5c
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140038"
---
# <a name="localize-your-app"></a><span data-ttu-id="93a3a-104">本地化应用</span><span class="sxs-lookup"><span data-stu-id="93a3a-104">Localize your app</span></span>

<span data-ttu-id="93a3a-105">你必须考虑以下因素来本地化你的Microsoft Teams应用：</span><span class="sxs-lookup"><span data-stu-id="93a3a-105">You must consider the following factors to localize your Microsoft Teams app:</span></span>

1. <span data-ttu-id="93a3a-106">[本地化 AppSource 一览](#localize-your-appsource-listing)。</span><span class="sxs-lookup"><span data-stu-id="93a3a-106">[Localize your AppSource listing](#localize-your-appsource-listing).</span></span>
1. <span data-ttu-id="93a3a-107">[本地化应用清单 中的字符串](#localize-strings-in-your-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="93a3a-107">[Localize strings in your app manifest](#localize-strings-in-your-app-manifest).</span></span> 
1. <span data-ttu-id="93a3a-108">[处理来自用户的本地化文本提交](#handle-localized-text-submissions-from-your-users)。</span><span class="sxs-lookup"><span data-stu-id="93a3a-108">[Handle localized text submissions from your users](#handle-localized-text-submissions-from-your-users).</span></span>

## <a name="localize-your-appsource-listing"></a><span data-ttu-id="93a3a-109">本地化 AppSource 一览</span><span class="sxs-lookup"><span data-stu-id="93a3a-109">Localize your AppSource listing</span></span>

<span data-ttu-id="93a3a-110">如果要将应用发布到应用商店，则必须注意，尚不支持本地化 AppSource 一览。</span><span class="sxs-lookup"><span data-stu-id="93a3a-110">If you are publishing the app to the store, you must be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="93a3a-111">若要支持应用商店中的本地化一览，你可以向一览添加其他语言。</span><span class="sxs-lookup"><span data-stu-id="93a3a-111">To support localized listings in the app store, you can add additional languages to your listing.</span></span> <span data-ttu-id="93a3a-112">在合作伙伴中心中为一览 [提供](/office/dev/store/submit-to-appsource-via-partner-center) 的默认语言信息将显示在 [应用的 AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) 网站一览中。</span><span class="sxs-lookup"><span data-stu-id="93a3a-112">The default language information you provide in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) for your listing appears in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) listing for your app.</span></span> <span data-ttu-id="93a3a-113">目前，默认语言为英语。</span><span class="sxs-lookup"><span data-stu-id="93a3a-113">Currently, the default language is English.</span></span>

### <a name="configure-localization"></a><span data-ttu-id="93a3a-114">配置本地化</span><span class="sxs-lookup"><span data-stu-id="93a3a-114">Configure localization</span></span>

<span data-ttu-id="93a3a-115">若要为应用配置其他语言，请在合作伙伴中心[](/office/dev/store/submit-to-appsource-via-partner-center)中选择英语和应用的其他语言。</span><span class="sxs-lookup"><span data-stu-id="93a3a-115">To configure an additional language for your app, in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center), select both English and the additional language of the app.</span></span> <span data-ttu-id="93a3a-116">在下面的示例中，法语用作其他语言：</span><span class="sxs-lookup"><span data-stu-id="93a3a-116">French is used as an additional language in the following example:</span></span>

1. <span data-ttu-id="93a3a-117">添加英语语言</span><span class="sxs-lookup"><span data-stu-id="93a3a-117">Add English language</span></span>
    * <span data-ttu-id="93a3a-118">输入应用名称。</span><span class="sxs-lookup"><span data-stu-id="93a3a-118">Enter the app name.</span></span>
    * <span data-ttu-id="93a3a-119">输入以英语表示的应用的简短说明。</span><span class="sxs-lookup"><span data-stu-id="93a3a-119">Enter a short description of the app in English.</span></span>
    * <span data-ttu-id="93a3a-120">输入英文版应用的详细说明。</span><span class="sxs-lookup"><span data-stu-id="93a3a-120">Enter the long description of the app in English.</span></span>
    * <span data-ttu-id="93a3a-121">In the long description， enter： **This app is available in French**.</span><span class="sxs-lookup"><span data-stu-id="93a3a-121">In the long description, enter: **This app is available in French**.</span></span>
    * <span data-ttu-id="93a3a-122">Upload应用 UI 图像以英语 (显示) 。</span><span class="sxs-lookup"><span data-stu-id="93a3a-122">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="93a3a-123">添加法语</span><span class="sxs-lookup"><span data-stu-id="93a3a-123">Add French language</span></span>
    * <span data-ttu-id="93a3a-124">输入应用名称。</span><span class="sxs-lookup"><span data-stu-id="93a3a-124">Enter the app name.</span></span>
    * <span data-ttu-id="93a3a-125">使用法语输入应用的简短说明。</span><span class="sxs-lookup"><span data-stu-id="93a3a-125">Enter a short description of the app in French.</span></span>
    * <span data-ttu-id="93a3a-126">使用法语输入应用的详细说明。</span><span class="sxs-lookup"><span data-stu-id="93a3a-126">Enter the long description of the app in French.</span></span>
    * <span data-ttu-id="93a3a-127">Upload使用法语或法语 (应用 UI) 。</span><span class="sxs-lookup"><span data-stu-id="93a3a-127">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="93a3a-128">使用英语上载的图像在 AppSource 中使用。</span><span class="sxs-lookup"><span data-stu-id="93a3a-128">The images that you upload with the English language are used in AppSource.</span></span>

## <a name="localize-strings-in-your-app-manifest"></a><span data-ttu-id="93a3a-129">本地化应用清单中的字符串</span><span class="sxs-lookup"><span data-stu-id="93a3a-129">Localize strings in your app manifest</span></span>

<span data-ttu-id="93a3a-130">你必须使用Microsoft Teams `v1.5` 架构和更高版本来本地化你的应用。</span><span class="sxs-lookup"><span data-stu-id="93a3a-130">You must use the Microsoft Teams app schema `v1.5` and later to localize your app.</span></span> <span data-ttu-id="93a3a-131">为此，可以将 on manifest.js中的 属性设置为或更高，并更新属性到 (版本，在这种情况下 `$schema` **https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json** `manifestVersion` `$schema` `1.5`) 。</span><span class="sxs-lookup"><span data-stu-id="93a3a-131">You can do this by setting the `$schema` attribute in your manifest.json file to **https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json** or higher and updating the `manifestVersion` property to `$schema` version (`1.5` in this case).</span></span> 

<span data-ttu-id="93a3a-132">必须使用应用程序 `localizationInfo` 支持的默认语言添加 属性。</span><span class="sxs-lookup"><span data-stu-id="93a3a-132">You must add the `localizationInfo` property with the default language that your application supports.</span></span> <span data-ttu-id="93a3a-133">如果用户的客户端设置与任何其他语言不匹配，则默认语言将用作最终回退语言。</span><span class="sxs-lookup"><span data-stu-id="93a3a-133">The default language is used as the final fallback language if the user's client settings do not match with any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="93a3a-134">更改manifest.js示例</span><span class="sxs-lookup"><span data-stu-id="93a3a-134">Example manifest.json change</span></span>

<span data-ttu-id="93a3a-135">下面的manifest.js可帮助使用应用程序支持的默认语言以及 添加 `localizationInfo` 属性 `additionalLanguages` ：</span><span class="sxs-lookup"><span data-stu-id="93a3a-135">The following manifest.json helps to add the `localizationInfo` property with the default language that your application supports along with `additionalLanguages`:</span></span>

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

### <a name="example-localization-json-change"></a><span data-ttu-id="93a3a-136">示例本地化 .json 更改</span><span class="sxs-lookup"><span data-stu-id="93a3a-136">Example localization .json change</span></span>

<span data-ttu-id="93a3a-137">下面是本地化 .json 的示例：</span><span class="sxs-lookup"><span data-stu-id="93a3a-137">Following is an example for localization .json:</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  "name.short": "Localización",
  "name.full": "Aplicación de localización",
  ...
}
```


<span data-ttu-id="93a3a-138">可以在清单中提供其他 .json 文件以及面向用户的字符串的翻译。</span><span class="sxs-lookup"><span data-stu-id="93a3a-138">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="93a3a-139">这些文件必须遵守本地化文件 [JSON 架构](../../resources/schema/localization-schema.md) ，并且必须添加到清单 `localizationInfo` 的 属性中。</span><span class="sxs-lookup"><span data-stu-id="93a3a-139">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the `localizationInfo` property of your manifest.</span></span> <span data-ttu-id="93a3a-140">每个文件与语言标记相关，Teams客户端使用该标记来选择适当的字符串。</span><span class="sxs-lookup"><span data-stu-id="93a3a-140">Each file correlates to a language tag, which the Teams client uses to select the appropriate strings.</span></span> <span data-ttu-id="93a3a-141">语言标记采用 的形式，但可以省略 部分，以面向支持 `<language>-<region>` `<region>` 所需语言的所有区域。</span><span class="sxs-lookup"><span data-stu-id="93a3a-141">The language tag takes the form of `<language>-<region>` but you can omit the `<region>` portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="93a3a-142">Teams客户端按以下顺序应用字符串：默认语言字符串 -> 用户的语言仅包含字符串 -> 用户的语言 + 用户的区域字符串。</span><span class="sxs-lookup"><span data-stu-id="93a3a-142">The Teams client applies the strings in the following order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="93a3a-143">例如，你提供默认语言"fr" (法语、所有地区) 以及"en" (英语、所有地区) 和"en-gb" (英语、英国) 的其他语言文件，用户的语言设置为"en-gb"。</span><span class="sxs-lookup"><span data-stu-id="93a3a-143">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain), the user's language is set to 'en-gb'.</span></span> <span data-ttu-id="93a3a-144">将基于语言选择进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="93a3a-144">The following changes take place based on the language selection:</span></span>

1. <span data-ttu-id="93a3a-145">客户端Teams"fr"字符串，然后用"en"字符串覆盖它们。</span><span class="sxs-lookup"><span data-stu-id="93a3a-145">The Teams client takes the 'fr' strings and overwrite them with the 'en' strings.</span></span>
1. <span data-ttu-id="93a3a-146">使用"en-gb"字符串覆盖"en"字符串。</span><span class="sxs-lookup"><span data-stu-id="93a3a-146">Overwrite the 'en' strings with the 'en-gb' strings.</span></span>

<span data-ttu-id="93a3a-147">如果用户的语言设置为"en-ca"，则根据语言选择进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="93a3a-147">If the user's language is set to 'en-ca', the following changes take place based on the language selection:</span></span> 

1. <span data-ttu-id="93a3a-148">客户端Teams"fr"字符串，然后用"en"字符串覆盖它们。</span><span class="sxs-lookup"><span data-stu-id="93a3a-148">The Teams client takes the 'fr' strings and overwrite them with the 'en' strings.</span></span>
1. <span data-ttu-id="93a3a-149">由于未提供"en-ca"本地化，因此使用"en"本地化。</span><span class="sxs-lookup"><span data-stu-id="93a3a-149">Since no 'en-ca' localization is supplied, the 'en\` localizations are used.</span></span>

<span data-ttu-id="93a3a-150">如果用户的语言设置为"es-es"，则客户端Teams"fr"字符串。</span><span class="sxs-lookup"><span data-stu-id="93a3a-150">If the user's language is set to 'es-es', the Teams client takes the 'fr' strings.</span></span> <span data-ttu-id="93a3a-151">客户端Teams不会覆盖任何语言文件的字符串，因为不提供"es"或"es-es"翻译。</span><span class="sxs-lookup"><span data-stu-id="93a3a-151">The Teams client does not override the strings with any of the language files as no 'es' or 'es-es' translation is provided.</span></span>

<span data-ttu-id="93a3a-152">因此，您必须在清单中提供顶级的仅语言翻译。</span><span class="sxs-lookup"><span data-stu-id="93a3a-152">Therefore, you must provide top level, language only translations in your manifest.</span></span> <span data-ttu-id="93a3a-153">例如，"en"而不是"en-us"。</span><span class="sxs-lookup"><span data-stu-id="93a3a-153">For example, 'en' instead of 'en-us'.</span></span> <span data-ttu-id="93a3a-154">您必须仅为需要这些替代的少数字符串提供区域级别替代。</span><span class="sxs-lookup"><span data-stu-id="93a3a-154">You must provide region level overrides only for the few strings that need them.</span></span> 

### <a name="example-manifestjson-change"></a><span data-ttu-id="93a3a-155">更改manifest.js示例</span><span class="sxs-lookup"><span data-stu-id="93a3a-155">Example manifest.json change</span></span>

<span data-ttu-id="93a3a-156">更改manifest.js如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="93a3a-156">The manifest.json change is shown in the following example:</span></span>

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

### <a name="example-localization-json-file"></a><span data-ttu-id="93a3a-157">示例本地化 .json 文件</span><span class="sxs-lookup"><span data-stu-id="93a3a-157">Example localization .json file</span></span>

 <span data-ttu-id="93a3a-158">更改localization.js如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="93a3a-158">The localization.json change is shown in the following example:</span></span>

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

## <a name="handle-localized-text-submissions-from-your-users"></a><span data-ttu-id="93a3a-159">处理来自用户的本地化文本提交</span><span class="sxs-lookup"><span data-stu-id="93a3a-159">Handle localized text submissions from your users</span></span>

<span data-ttu-id="93a3a-160">如果您提供应用程序的本地化版本，则用户使用相同的语言进行响应。</span><span class="sxs-lookup"><span data-stu-id="93a3a-160">If your provide localized versions of your application, the users respond with the same language.</span></span> <span data-ttu-id="93a3a-161">由于Teams提交不会将用户提交翻译回默认语言，因此你的应用必须处理本地化语言响应。</span><span class="sxs-lookup"><span data-stu-id="93a3a-161">As Teams does not translate the user submissions back to the default language, your app must handle the localized language responses.</span></span> <span data-ttu-id="93a3a-162">例如，如果你提供本地化的 ，则对自动程序的响应是命令的本地化文本， `commandList` 而不是默认语言。</span><span class="sxs-lookup"><span data-stu-id="93a3a-162">For example, if you provide a localized `commandList`, the responses to your bot are the localized text of the command, not the default language.</span></span> <span data-ttu-id="93a3a-163">你的应用必须做出相应的响应。</span><span class="sxs-lookup"><span data-stu-id="93a3a-163">Your app must respond appropriately.</span></span>

## <a name="code-sample"></a><span data-ttu-id="93a3a-164">代码示例</span><span class="sxs-lookup"><span data-stu-id="93a3a-164">Code sample</span></span>

| <span data-ttu-id="93a3a-165">示例名称</span><span class="sxs-lookup"><span data-stu-id="93a3a-165">Sample name</span></span> | <span data-ttu-id="93a3a-166">说明</span><span class="sxs-lookup"><span data-stu-id="93a3a-166">Description</span></span> | <span data-ttu-id="93a3a-167">.NET</span><span class="sxs-lookup"><span data-stu-id="93a3a-167">.NET</span></span> | <span data-ttu-id="93a3a-168">Node.js</span><span class="sxs-lookup"><span data-stu-id="93a3a-168">Node.js</span></span> |
|-------------|-------------|------|------|
| <span data-ttu-id="93a3a-169">应用本地化</span><span class="sxs-lookup"><span data-stu-id="93a3a-169">App Localization</span></span> | <span data-ttu-id="93a3a-170">Microsoft Teams自动程序和选项卡进行应用本地化。</span><span class="sxs-lookup"><span data-stu-id="93a3a-170">Microsoft Teams app localization using bot and tab.</span></span> | [<span data-ttu-id="93a3a-171">View</span><span class="sxs-lookup"><span data-stu-id="93a3a-171">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |[<span data-ttu-id="93a3a-172">View</span><span class="sxs-lookup"><span data-stu-id="93a3a-172">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) |

