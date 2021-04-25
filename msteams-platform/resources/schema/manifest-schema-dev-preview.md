---
title: 开发者预览版清单架构参考
description: 介绍 Microsoft Teams 清单支持的架构
ms.topic: reference
keywords: teams 清单架构开发者预览版
ms.date: 05/20/2019
ms.openlocfilehash: adb178000d909c9031e4b4df187bbf6f74f6e783
ms.sourcegitcommit: 7b4f383b506d4bc68a1b5641d6e0f404edbfbc6d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2021
ms.locfileid: "51946471"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="89d69-104">Microsoft Teams 的开发人员预览清单架构</span><span class="sxs-lookup"><span data-stu-id="89d69-104">Developer preview manifest schema for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="89d69-105">有关 [开发者预览版](~/resources/dev-preview/developer-preview-intro.md) 和如何加入的信息，请参阅 开发者预览版。</span><span class="sxs-lookup"><span data-stu-id="89d69-105">See [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for information on the program and how you can join.</span></span>
> <span data-ttu-id="89d69-106">如果未使用开发人员预览版，则不应使用此版本的清单。</span><span class="sxs-lookup"><span data-stu-id="89d69-106">If you are not using the developer preview you should not be using this version of the manifest.</span></span> <span data-ttu-id="89d69-107">有关 [清单的公共版本，请参阅参考：Microsoft Teams](~/resources/schema/manifest-schema.md) 的清单架构。</span><span class="sxs-lookup"><span data-stu-id="89d69-107">See [Reference: Manifest schema for Microsoft Teams](~/resources/schema/manifest-schema.md) for the public version of the manifest.</span></span>

<span data-ttu-id="89d69-108">Microsoft Teams 清单介绍了应用如何集成到 Microsoft Teams 产品。</span><span class="sxs-lookup"><span data-stu-id="89d69-108">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="89d69-109">清单必须符合 托管在 的架构 [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) 。</span><span class="sxs-lookup"><span data-stu-id="89d69-109">Your manifest must conform to the schema hosted at [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span></span>

<span data-ttu-id="89d69-110">有关可用功能详细信息，请参阅 [：Microsoft Teams](~/resources/dev-preview/developer-preview-features.md)公共开发者预览版中的功能。</span><span class="sxs-lookup"><span data-stu-id="89d69-110">For more information on the features available see: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="89d69-111">示例完整清单</span><span class="sxs-lookup"><span data-stu-id="89d69-111">Sample full manifest</span></span>

```json
{
  "$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
  "manifestVersion": "devPreview",
  "version": "1.0.0",
  "id": "%MICROSOFT-APP-ID%",
  "packageName": "com.example.myapp",
  "devicePermissions" : [ "geolocation", "media" ],
  "developer": {
    "name": "Publisher Name",
    "websiteUrl": "https://website.com/",
    "privacyUrl": "https://website.com/privacy",
    "termsOfUseUrl": "https://website.com/app-tos",
    "mpnId": "1234567890"
  },
  "localizationInfo": {
    "defaultLanguageTag": "es-es",
    "additionalLanguages": [
      {
        "languageTag": "en-us",
        "file": "en-us.json"
      }
    ]
  },
  "name": {
    "short": "Name of your app (<=30 chars)",
    "full": "Full name of app, if longer than 30 characters"
  },
  "description": {
    "short": "Short description of your app",
    "full": "Full description of your app"
  },
  "icons": {
    "outline": "%FILENAME-32x32px%",
    "color": "%FILENAME-192x192px"
  },
  "accentColor": "%HEX-COLOR%",
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [ "team", "groupchat" ]
    }
  ],
  "staticTabs": [
    {
      "entityId": "idForPage",
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content?host=msteams",
      "websiteUrl": "https://contoso.com/content",
      "scopes": [ "personal" ]
    }
  ],
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "scopes": [ "team", "personal", "groupchat" ],
      "supportsFiles": true,
      "commandLists": [
        {
          "scopes": [ "team", "groupchat" ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command N",
              "description": "Description of Command N"
            }
          ]
        },
        {
          "scopes": [ "personal", "groupchat" ],
          "commands": [
            {
              "title": "Personal command 1",
              "description": "Description of Personal command 1"
            },
            {
              "title": "Personal command N",
              "description": "Description of Personal command N"
            }
          ]
        }
      ]
    }
  ],
  "connectors": [
    {
      "connectorId": "GUID-FROM-CONNECTOR-DEV-PORTAL%",
      "configurationUrl": "https://contoso.com/teamsconnector/configure",
      "scopes": [ "team"]
    }
  ],
  "composeExtensions": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "exampleCmd1",
          "title": "Example Command",
          "description": "Command Description; e.g., Search on the web",
          "initialRun": true,
          "type" : "search",
          "context" : ["compose", "commandBox"],
          "parameters": [
            {
              "name": "keyword",
              "title": "Search keywords",
              "description": "Enter the keywords to search for"
            }
          ]
        },
        {
          "id": "exampleCmd2",
          "title": "Example Command 2",
          "description": "Command Description; e.g., Search for a customer",
          "initialRun": true,
          "type" : "action",
          "fetchTask" : true,
          "context" : ["message"],
          "parameters": [
            {
              "name": "custinfo",
              "title": "Customer name",
              "description": "Enter a customer name",
              "inputType" : "text"
            }
          ]
        },
        {
          "id": "exampleMessageHandler",
          "title": "Message Handler",
          "description": "Domains that will create a preview when pasted into the compose box",
          "messageHandlers": [
            {
              "type" : "link",
              "value" : {
                "domains" : [
                  "mysite.someplace.com",
                  "othersite.someplace.com"
                ]
              }
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers",
  ],
  "validDomains": [
     "contoso.com",
     "mysite.someplace.com",
     "othersite.someplace.com"
  ],
   "configurableProperties": [
     "name",
     "shortDescription",
     "longDescription",
     "smallImageUrl", 
     "largeImageUrl", 
     "accentColor",
     "websiteUrl",
     "privacyUrl",
     "termsOfUseUrl"        
  ],
  "defaultInstallScope": "meetings",
  "defaultGroupCapability": {
    "meetings": "tab", 
    "team": "bot", 
    "groupchat": "bot"
  }
}
```

<span data-ttu-id="89d69-112">该架构定义以下属性：</span><span class="sxs-lookup"><span data-stu-id="89d69-112">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="89d69-113">$schema</span><span class="sxs-lookup"><span data-stu-id="89d69-113">$schema</span></span>

<span data-ttu-id="89d69-114">*可选，但建议* &ndash; 字符串</span><span class="sxs-lookup"><span data-stu-id="89d69-114">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="89d69-115">引用 https:// JSON 架构的 URL。</span><span class="sxs-lookup"><span data-stu-id="89d69-115">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="89d69-116">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="89d69-116">manifestVersion</span></span>

<span data-ttu-id="89d69-117">**必需** &ndash; 字符串</span><span class="sxs-lookup"><span data-stu-id="89d69-117">**Required** &ndash; String</span></span>

<span data-ttu-id="89d69-118">此清单使用的清单架构版本。</span><span class="sxs-lookup"><span data-stu-id="89d69-118">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="89d69-119">它应为"devPreview"。</span><span class="sxs-lookup"><span data-stu-id="89d69-119">It should be "devPreview".</span></span>

## <a name="version"></a><span data-ttu-id="89d69-120">version</span><span class="sxs-lookup"><span data-stu-id="89d69-120">version</span></span>

<span data-ttu-id="89d69-121">**必需** &ndash; 字符串</span><span class="sxs-lookup"><span data-stu-id="89d69-121">**Required** &ndash; String</span></span>

<span data-ttu-id="89d69-122">特定应用的版本。</span><span class="sxs-lookup"><span data-stu-id="89d69-122">The version of the specific app.</span></span> <span data-ttu-id="89d69-123">如果更新清单中的某些内容，则版本也必须递增。</span><span class="sxs-lookup"><span data-stu-id="89d69-123">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="89d69-124">这样一来，在安装新的清单时，它将覆盖现有的版本，用户将获得新的功能。</span><span class="sxs-lookup"><span data-stu-id="89d69-124">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="89d69-125">如果此应用已提交到应用商店，则新清单必须重新提交和重新验证。</span><span class="sxs-lookup"><span data-stu-id="89d69-125">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="89d69-126">然后，此应用的用户将在经过批准后数小时内自动获取新的更新清单。</span><span class="sxs-lookup"><span data-stu-id="89d69-126">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="89d69-127">如果应用请求的权限更改，将提示用户升级并重新同意应用。</span><span class="sxs-lookup"><span data-stu-id="89d69-127">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="89d69-128">此版本字符串必须遵循 [Semver](http://semver.org/) 标准 (MAJOR。MINOR。PATCH) 。</span><span class="sxs-lookup"><span data-stu-id="89d69-128">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="89d69-129">id</span><span class="sxs-lookup"><span data-stu-id="89d69-129">id</span></span>

<span data-ttu-id="89d69-130">**必需** &ndash; Microsoft 应用 ID</span><span class="sxs-lookup"><span data-stu-id="89d69-130">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="89d69-131">此应用的唯一 Microsoft 生成的标识符。</span><span class="sxs-lookup"><span data-stu-id="89d69-131">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="89d69-132">如果你已经通过 Microsoft Bot Framework 注册了自动程序，或者你的选项卡的 Web 应用已经使用 Microsoft 登录，你应该已经拥有 ID，并且应在此处输入它。</span><span class="sxs-lookup"><span data-stu-id="89d69-132">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="89d69-133">否则，应在"我的应用程序" (Microsoft 应用程序注册门户 [) 生成](https://apps.dev.microsoft.com) 一个新 ID，在此处输入，然后在添加自动程序时重复使用 [它](~/bots/how-to/create-a-bot-for-teams.md)。</span><span class="sxs-lookup"><span data-stu-id="89d69-133">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you [add a bot](~/bots/how-to/create-a-bot-for-teams.md).</span></span>

## <a name="packagename"></a><span data-ttu-id="89d69-134">packageName</span><span class="sxs-lookup"><span data-stu-id="89d69-134">packageName</span></span>

<span data-ttu-id="89d69-135">**必需** &ndash; 字符串</span><span class="sxs-lookup"><span data-stu-id="89d69-135">**Required** &ndash; String</span></span>

<span data-ttu-id="89d69-136">反向域表示法中此应用程序的唯一标识符;例如，com.example.myapp。</span><span class="sxs-lookup"><span data-stu-id="89d69-136">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="89d69-137">developer</span><span class="sxs-lookup"><span data-stu-id="89d69-137">developer</span></span>

<span data-ttu-id="89d69-138">**Required**</span><span class="sxs-lookup"><span data-stu-id="89d69-138">**Required**</span></span>

<span data-ttu-id="89d69-139">指定有关你的公司的信息。</span><span class="sxs-lookup"><span data-stu-id="89d69-139">Specifies information about your company.</span></span> <span data-ttu-id="89d69-140">对于提交到 AppSource (Office 应用商店) ，这些值必须与 AppSource 条目中的信息匹配。</span><span class="sxs-lookup"><span data-stu-id="89d69-140">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span>

|<span data-ttu-id="89d69-141">名称</span><span class="sxs-lookup"><span data-stu-id="89d69-141">Name</span></span>| <span data-ttu-id="89d69-142">最大大小</span><span class="sxs-lookup"><span data-stu-id="89d69-142">Maximum size</span></span> | <span data-ttu-id="89d69-143">必需</span><span class="sxs-lookup"><span data-stu-id="89d69-143">Required</span></span> | <span data-ttu-id="89d69-144">说明</span><span class="sxs-lookup"><span data-stu-id="89d69-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="89d69-145">32 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-145">32 characters</span></span>|<span data-ttu-id="89d69-146">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-146">✔</span></span>|<span data-ttu-id="89d69-147">开发人员显示名称的指南。</span><span class="sxs-lookup"><span data-stu-id="89d69-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="89d69-148">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-148">2048 characters</span></span>|<span data-ttu-id="89d69-149">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-149">✔</span></span>|<span data-ttu-id="89d69-150">the https:// URL to the developer's website.</span><span class="sxs-lookup"><span data-stu-id="89d69-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="89d69-151">此链接应让用户访问你的公司或特定于产品的登陆页面。</span><span class="sxs-lookup"><span data-stu-id="89d69-151">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="89d69-152">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-152">2048 characters</span></span>|<span data-ttu-id="89d69-153">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-153">✔</span></span>|<span data-ttu-id="89d69-154">the https:// URL to the developer's privacy policy.</span><span class="sxs-lookup"><span data-stu-id="89d69-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="89d69-155">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-155">2048 characters</span></span>|<span data-ttu-id="89d69-156">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-156">✔</span></span>|<span data-ttu-id="89d69-157">the https:// URL to the developer's use terms.</span><span class="sxs-lookup"><span data-stu-id="89d69-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="89d69-158">10 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-158">10 characters</span></span>|<span data-ttu-id="89d69-159">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-159">✔</span></span>|<span data-ttu-id="89d69-160">**可选** 标识生成应用的合作伙伴组织的 Microsoft 合作伙伴网络 ID。</span><span class="sxs-lookup"><span data-stu-id="89d69-160">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="89d69-161">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="89d69-161">localizationInfo</span></span>

<span data-ttu-id="89d69-162">**可选**</span><span class="sxs-lookup"><span data-stu-id="89d69-162">**Optional**</span></span>

<span data-ttu-id="89d69-163">允许指定默认语言，以及指向其他语言文件的指针。</span><span class="sxs-lookup"><span data-stu-id="89d69-163">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="89d69-164">请参阅 [本地化](~/concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="89d69-164">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="89d69-165">名称</span><span class="sxs-lookup"><span data-stu-id="89d69-165">Name</span></span>| <span data-ttu-id="89d69-166">最大大小</span><span class="sxs-lookup"><span data-stu-id="89d69-166">Maximum size</span></span> | <span data-ttu-id="89d69-167">必需</span><span class="sxs-lookup"><span data-stu-id="89d69-167">Required</span></span> | <span data-ttu-id="89d69-168">说明</span><span class="sxs-lookup"><span data-stu-id="89d69-168">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`|<span data-ttu-id="89d69-169">4 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-169">4 characters</span></span>|<span data-ttu-id="89d69-170">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-170">✔</span></span>|<span data-ttu-id="89d69-171">此顶级清单文件中字符串的语言标记。</span><span class="sxs-lookup"><span data-stu-id="89d69-171">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="89d69-172">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="89d69-172">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="89d69-173">指定其他语言翻译的对象数组。</span><span class="sxs-lookup"><span data-stu-id="89d69-173">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="89d69-174">名称</span><span class="sxs-lookup"><span data-stu-id="89d69-174">Name</span></span>| <span data-ttu-id="89d69-175">最大大小</span><span class="sxs-lookup"><span data-stu-id="89d69-175">Maximum size</span></span> | <span data-ttu-id="89d69-176">必需</span><span class="sxs-lookup"><span data-stu-id="89d69-176">Required</span></span> | <span data-ttu-id="89d69-177">说明</span><span class="sxs-lookup"><span data-stu-id="89d69-177">Description</span></span>|
|---|---|---|---|
|`languageTag`|<span data-ttu-id="89d69-178">4 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-178">4 characters</span></span>|<span data-ttu-id="89d69-179">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-179">✔</span></span>|<span data-ttu-id="89d69-180">提供的文件中字符串的语言标记。</span><span class="sxs-lookup"><span data-stu-id="89d69-180">The language tag of the strings in the provided file.</span></span>|
|`file`|<span data-ttu-id="89d69-181">4 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-181">4 characters</span></span>|<span data-ttu-id="89d69-182">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-182">✔</span></span>|<span data-ttu-id="89d69-183">包含已翻译字符串的 .json 文件的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="89d69-183">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="89d69-184">name</span><span class="sxs-lookup"><span data-stu-id="89d69-184">name</span></span>

<span data-ttu-id="89d69-185">**Required**</span><span class="sxs-lookup"><span data-stu-id="89d69-185">**Required**</span></span>

<span data-ttu-id="89d69-186">在 Teams 体验中向用户显示的应用体验名称。</span><span class="sxs-lookup"><span data-stu-id="89d69-186">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="89d69-187">对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。</span><span class="sxs-lookup"><span data-stu-id="89d69-187">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="89d69-188">和 `short` `full` 的值不应相同。</span><span class="sxs-lookup"><span data-stu-id="89d69-188">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="89d69-189">名称</span><span class="sxs-lookup"><span data-stu-id="89d69-189">Name</span></span>| <span data-ttu-id="89d69-190">最大大小</span><span class="sxs-lookup"><span data-stu-id="89d69-190">Maximum size</span></span> | <span data-ttu-id="89d69-191">必需</span><span class="sxs-lookup"><span data-stu-id="89d69-191">Required</span></span> | <span data-ttu-id="89d69-192">说明</span><span class="sxs-lookup"><span data-stu-id="89d69-192">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="89d69-193">30 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-193">30 characters</span></span>|<span data-ttu-id="89d69-194">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-194">✔</span></span>|<span data-ttu-id="89d69-195">应用的显示名称。</span><span class="sxs-lookup"><span data-stu-id="89d69-195">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="89d69-196">100 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-196">100 characters</span></span>||<span data-ttu-id="89d69-197">应用的完整名称，在完整应用名称超过 30 个字符时使用。</span><span class="sxs-lookup"><span data-stu-id="89d69-197">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="89d69-198">说明</span><span class="sxs-lookup"><span data-stu-id="89d69-198">description</span></span>

<span data-ttu-id="89d69-199">**Required**</span><span class="sxs-lookup"><span data-stu-id="89d69-199">**Required**</span></span>

<span data-ttu-id="89d69-200">向用户描述你的应用。</span><span class="sxs-lookup"><span data-stu-id="89d69-200">Describes your app to users.</span></span> <span data-ttu-id="89d69-201">对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。</span><span class="sxs-lookup"><span data-stu-id="89d69-201">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="89d69-202">确保你的描述准确地描述了你的体验，并提供相关信息来帮助潜在客户了解你的体验。</span><span class="sxs-lookup"><span data-stu-id="89d69-202">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="89d69-203">还应在完整说明中注意，如果需要使用外部帐户。</span><span class="sxs-lookup"><span data-stu-id="89d69-203">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="89d69-204">和 `short` `full` 的值不应相同。</span><span class="sxs-lookup"><span data-stu-id="89d69-204">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="89d69-205">简短说明不得在详细说明中重复，且不得包含任何其他应用名称。</span><span class="sxs-lookup"><span data-stu-id="89d69-205">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="89d69-206">名称</span><span class="sxs-lookup"><span data-stu-id="89d69-206">Name</span></span>| <span data-ttu-id="89d69-207">最大大小</span><span class="sxs-lookup"><span data-stu-id="89d69-207">Maximum size</span></span> | <span data-ttu-id="89d69-208">必需</span><span class="sxs-lookup"><span data-stu-id="89d69-208">Required</span></span> | <span data-ttu-id="89d69-209">说明</span><span class="sxs-lookup"><span data-stu-id="89d69-209">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="89d69-210">80 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-210">80 characters</span></span>|<span data-ttu-id="89d69-211">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-211">✔</span></span>|<span data-ttu-id="89d69-212">应用体验的简短说明，在空间有限时使用。</span><span class="sxs-lookup"><span data-stu-id="89d69-212">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="89d69-213">4000 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-213">4000 characters</span></span>|<span data-ttu-id="89d69-214">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-214">✔</span></span>|<span data-ttu-id="89d69-215">应用的完整说明。</span><span class="sxs-lookup"><span data-stu-id="89d69-215">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="89d69-216">图标</span><span class="sxs-lookup"><span data-stu-id="89d69-216">icons</span></span>

<span data-ttu-id="89d69-217">**Required**</span><span class="sxs-lookup"><span data-stu-id="89d69-217">**Required**</span></span>

<span data-ttu-id="89d69-218">Teams 应用中使用的图标。</span><span class="sxs-lookup"><span data-stu-id="89d69-218">Icons used within the Teams app.</span></span> <span data-ttu-id="89d69-219">图标文件必须作为上传程序包的一部分包含在内。</span><span class="sxs-lookup"><span data-stu-id="89d69-219">The icon files must be included as part of the upload package.</span></span>

|<span data-ttu-id="89d69-220">名称</span><span class="sxs-lookup"><span data-stu-id="89d69-220">Name</span></span>| <span data-ttu-id="89d69-221">最大大小</span><span class="sxs-lookup"><span data-stu-id="89d69-221">Maximum size</span></span> | <span data-ttu-id="89d69-222">必需</span><span class="sxs-lookup"><span data-stu-id="89d69-222">Required</span></span> | <span data-ttu-id="89d69-223">说明</span><span class="sxs-lookup"><span data-stu-id="89d69-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="89d69-224">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-224">2048 characters</span></span>|<span data-ttu-id="89d69-225">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-225">✔</span></span>|<span data-ttu-id="89d69-226">指向透明 32x32 PNG 大纲图标的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="89d69-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="89d69-227">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-227">2048 characters</span></span>|<span data-ttu-id="89d69-228">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-228">✔</span></span>|<span data-ttu-id="89d69-229">完整颜色 192x192 PNG 图标的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="89d69-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="89d69-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="89d69-230">accentColor</span></span>

<span data-ttu-id="89d69-231">**必需** &ndash; 字符串</span><span class="sxs-lookup"><span data-stu-id="89d69-231">**Required** &ndash; String</span></span>

<span data-ttu-id="89d69-232">要与 和 结合使用用作大纲图标背景的颜色。</span><span class="sxs-lookup"><span data-stu-id="89d69-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="89d69-233">该值必须是以"#"开头的有效 HTML 颜色代码，例如 `#4464ee` 。</span><span class="sxs-lookup"><span data-stu-id="89d69-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="89d69-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="89d69-234">configurableTabs</span></span>

<span data-ttu-id="89d69-235">**可选**</span><span class="sxs-lookup"><span data-stu-id="89d69-235">**Optional**</span></span>

<span data-ttu-id="89d69-236">当你的应用体验具有团队频道选项卡体验时，需要在添加前进行额外配置。</span><span class="sxs-lookup"><span data-stu-id="89d69-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="89d69-237">可配置的选项卡仅在团队范围内受支持，并且当前每个应用仅支持一个选项卡。</span><span class="sxs-lookup"><span data-stu-id="89d69-237">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="89d69-238">对象是包含类型 的所有元素的数组 `object` 。</span><span class="sxs-lookup"><span data-stu-id="89d69-238">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="89d69-239">只有提供可配置通道选项卡解决方案的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="89d69-239">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="89d69-240">名称</span><span class="sxs-lookup"><span data-stu-id="89d69-240">Name</span></span>| <span data-ttu-id="89d69-241">类型</span><span class="sxs-lookup"><span data-stu-id="89d69-241">Type</span></span>| <span data-ttu-id="89d69-242">最大大小</span><span class="sxs-lookup"><span data-stu-id="89d69-242">Maximum size</span></span> | <span data-ttu-id="89d69-243">必需</span><span class="sxs-lookup"><span data-stu-id="89d69-243">Required</span></span> | <span data-ttu-id="89d69-244">说明</span><span class="sxs-lookup"><span data-stu-id="89d69-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="89d69-245">String</span><span class="sxs-lookup"><span data-stu-id="89d69-245">String</span></span>|<span data-ttu-id="89d69-246">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-246">2048 characters</span></span>|<span data-ttu-id="89d69-247">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-247">✔</span></span>|<span data-ttu-id="89d69-248">配置 https:// 时将使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="89d69-248">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="89d69-249">布尔</span><span class="sxs-lookup"><span data-stu-id="89d69-249">Boolean</span></span>|||<span data-ttu-id="89d69-250">一个值，指示用户创建后是否可以更新选项卡配置的实例。</span><span class="sxs-lookup"><span data-stu-id="89d69-250">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="89d69-251">默认值： `true`</span><span class="sxs-lookup"><span data-stu-id="89d69-251">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="89d69-252">枚举数组</span><span class="sxs-lookup"><span data-stu-id="89d69-252">Array of enum</span></span>|<span data-ttu-id="89d69-253">1</span><span class="sxs-lookup"><span data-stu-id="89d69-253">1</span></span>|<span data-ttu-id="89d69-254">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-254">✔</span></span>|<span data-ttu-id="89d69-255">目前，可配置的选项卡仅支持 `team` 和 `groupchat` 作用域。</span><span class="sxs-lookup"><span data-stu-id="89d69-255">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="89d69-256">String</span><span class="sxs-lookup"><span data-stu-id="89d69-256">String</span></span>|<span data-ttu-id="89d69-257">2048</span><span class="sxs-lookup"><span data-stu-id="89d69-257">2048</span></span>||<span data-ttu-id="89d69-258">指向用于 SharePoint 的选项卡预览图像的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="89d69-258">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="89d69-259">大小 1024x768。</span><span class="sxs-lookup"><span data-stu-id="89d69-259">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="89d69-260">枚举数组</span><span class="sxs-lookup"><span data-stu-id="89d69-260">Array of enum</span></span>|<span data-ttu-id="89d69-261">1</span><span class="sxs-lookup"><span data-stu-id="89d69-261">1</span></span>||<span data-ttu-id="89d69-262">定义选项卡在 SharePoint 中的可用方法。</span><span class="sxs-lookup"><span data-stu-id="89d69-262">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="89d69-263">选项为 `sharePointFullPage` 和 `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="89d69-263">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="89d69-264">staticTabs</span><span class="sxs-lookup"><span data-stu-id="89d69-264">staticTabs</span></span>

<span data-ttu-id="89d69-265">**可选**</span><span class="sxs-lookup"><span data-stu-id="89d69-265">**Optional**</span></span>

<span data-ttu-id="89d69-266">定义一组默认情况下可以"固定"的选项卡，而无需用户手动添加它们。</span><span class="sxs-lookup"><span data-stu-id="89d69-266">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="89d69-267">范围中声明 `personal` 的静态选项卡始终固定到应用的个人体验。</span><span class="sxs-lookup"><span data-stu-id="89d69-267">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="89d69-268">作用域中声明的 `team` 静态选项卡当前不受支持。</span><span class="sxs-lookup"><span data-stu-id="89d69-268">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="89d69-269">对象是一个数组 (类型的所有元素) 最多包含 16 个元素 `object` 。</span><span class="sxs-lookup"><span data-stu-id="89d69-269">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="89d69-270">只有提供静态选项卡解决方案的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="89d69-270">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="89d69-271">名称</span><span class="sxs-lookup"><span data-stu-id="89d69-271">Name</span></span>| <span data-ttu-id="89d69-272">类型</span><span class="sxs-lookup"><span data-stu-id="89d69-272">Type</span></span>| <span data-ttu-id="89d69-273">最大大小</span><span class="sxs-lookup"><span data-stu-id="89d69-273">Maximum size</span></span> | <span data-ttu-id="89d69-274">必需</span><span class="sxs-lookup"><span data-stu-id="89d69-274">Required</span></span> | <span data-ttu-id="89d69-275">说明</span><span class="sxs-lookup"><span data-stu-id="89d69-275">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="89d69-276">字符串</span><span class="sxs-lookup"><span data-stu-id="89d69-276">String</span></span>|<span data-ttu-id="89d69-277">64 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-277">64 characters</span></span>|<span data-ttu-id="89d69-278">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-278">✔</span></span>|<span data-ttu-id="89d69-279">选项卡显示的实体的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="89d69-279">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="89d69-280">String</span><span class="sxs-lookup"><span data-stu-id="89d69-280">String</span></span>|<span data-ttu-id="89d69-281">128 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-281">128 characters</span></span>|<span data-ttu-id="89d69-282">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-282">✔</span></span>|<span data-ttu-id="89d69-283">选项卡显示名称界面中的列数。</span><span class="sxs-lookup"><span data-stu-id="89d69-283">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="89d69-284">String</span><span class="sxs-lookup"><span data-stu-id="89d69-284">String</span></span>|<span data-ttu-id="89d69-285">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-285">2048 characters</span></span>|<span data-ttu-id="89d69-286">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-286">✔</span></span>|<span data-ttu-id="89d69-287">指向要显示在 Teams 画布中的实体 UI 的 https:// URL。</span><span class="sxs-lookup"><span data-stu-id="89d69-287">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="89d69-288">String</span><span class="sxs-lookup"><span data-stu-id="89d69-288">String</span></span>|<span data-ttu-id="89d69-289">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-289">2048 characters</span></span>||<span data-ttu-id="89d69-290">用户 https:// 在浏览器中查看时指向的 URL。</span><span class="sxs-lookup"><span data-stu-id="89d69-290">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="89d69-291">枚举数组</span><span class="sxs-lookup"><span data-stu-id="89d69-291">Array of enum</span></span>|<span data-ttu-id="89d69-292">1</span><span class="sxs-lookup"><span data-stu-id="89d69-292">1</span></span>|<span data-ttu-id="89d69-293">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-293">✔</span></span>|<span data-ttu-id="89d69-294">目前，静态选项卡仅支持范围，这意味着只能将作用域预配 `personal` 为个人体验的一部分。</span><span class="sxs-lookup"><span data-stu-id="89d69-294">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="89d69-295">bots</span><span class="sxs-lookup"><span data-stu-id="89d69-295">bots</span></span>

<span data-ttu-id="89d69-296">**可选**</span><span class="sxs-lookup"><span data-stu-id="89d69-296">**Optional**</span></span>

<span data-ttu-id="89d69-297">定义自动程序解决方案以及默认命令属性等可选信息。</span><span class="sxs-lookup"><span data-stu-id="89d69-297">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="89d69-298">对象是一个 (，当前每个应用仅允许一个自动程序) 类型的所有元素 &mdash; `object` 。</span><span class="sxs-lookup"><span data-stu-id="89d69-298">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="89d69-299">只有提供自动程序体验的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="89d69-299">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="89d69-300">名称</span><span class="sxs-lookup"><span data-stu-id="89d69-300">Name</span></span>| <span data-ttu-id="89d69-301">类型</span><span class="sxs-lookup"><span data-stu-id="89d69-301">Type</span></span>| <span data-ttu-id="89d69-302">最大大小</span><span class="sxs-lookup"><span data-stu-id="89d69-302">Maximum size</span></span> | <span data-ttu-id="89d69-303">必需</span><span class="sxs-lookup"><span data-stu-id="89d69-303">Required</span></span> | <span data-ttu-id="89d69-304">说明</span><span class="sxs-lookup"><span data-stu-id="89d69-304">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="89d69-305">字符串</span><span class="sxs-lookup"><span data-stu-id="89d69-305">String</span></span>|<span data-ttu-id="89d69-306">64 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-306">64 characters</span></span>|<span data-ttu-id="89d69-307">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-307">✔</span></span>|<span data-ttu-id="89d69-308">使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="89d69-308">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="89d69-309">这可能与整个应用 [ID 相同](#id)。</span><span class="sxs-lookup"><span data-stu-id="89d69-309">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="89d69-310">布尔值</span><span class="sxs-lookup"><span data-stu-id="89d69-310">Boolean</span></span>|||<span data-ttu-id="89d69-311">描述自动程序是否利用用户提示将自动程序添加到特定频道。</span><span class="sxs-lookup"><span data-stu-id="89d69-311">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="89d69-312">默认值： `false`</span><span class="sxs-lookup"><span data-stu-id="89d69-312">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="89d69-313">布尔值</span><span class="sxs-lookup"><span data-stu-id="89d69-313">Boolean</span></span>|||<span data-ttu-id="89d69-314">指示自动程序是否为单向、仅通知的自动程序，而不是对话自动程序。</span><span class="sxs-lookup"><span data-stu-id="89d69-314">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="89d69-315">默认值： `false`</span><span class="sxs-lookup"><span data-stu-id="89d69-315">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="89d69-316">布尔值</span><span class="sxs-lookup"><span data-stu-id="89d69-316">Boolean</span></span>|||<span data-ttu-id="89d69-317">指示自动程序是否支持在个人聊天中上传/下载文件。</span><span class="sxs-lookup"><span data-stu-id="89d69-317">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="89d69-318">默认值： `false`</span><span class="sxs-lookup"><span data-stu-id="89d69-318">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="89d69-319">枚举数组</span><span class="sxs-lookup"><span data-stu-id="89d69-319">Array of enum</span></span>|<span data-ttu-id="89d69-320">3</span><span class="sxs-lookup"><span data-stu-id="89d69-320">3</span></span>|<span data-ttu-id="89d69-321">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-321">✔</span></span>|<span data-ttu-id="89d69-322">指定自动程序是在 `team` 内的频道上下文中提供体验、在群组聊天 (`groupchat`) 中提供体验，还是仅在单个用户 (`personal`) 范围内提供体验。</span><span class="sxs-lookup"><span data-stu-id="89d69-322">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="89d69-323">这些选项不具排他性。</span><span class="sxs-lookup"><span data-stu-id="89d69-323">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="89d69-324">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="89d69-324">bots.commandLists</span></span>

<span data-ttu-id="89d69-325">自动程序可以推荐给用户的命令的可选列表。</span><span class="sxs-lookup"><span data-stu-id="89d69-325">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="89d69-326">对象是一个 (，最多包含 2 个元素) 所有类型元素;您必须为自动程序支持的每个范围定义单独的 `object` 命令列表。</span><span class="sxs-lookup"><span data-stu-id="89d69-326">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="89d69-327">有关详细信息 [，](~/bots/how-to/create-a-bot-commands-menu.md) 请参阅自动程序菜单。</span><span class="sxs-lookup"><span data-stu-id="89d69-327">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="89d69-328">名称</span><span class="sxs-lookup"><span data-stu-id="89d69-328">Name</span></span>| <span data-ttu-id="89d69-329">类型</span><span class="sxs-lookup"><span data-stu-id="89d69-329">Type</span></span>| <span data-ttu-id="89d69-330">最大大小</span><span class="sxs-lookup"><span data-stu-id="89d69-330">Maximum size</span></span> | <span data-ttu-id="89d69-331">必需</span><span class="sxs-lookup"><span data-stu-id="89d69-331">Required</span></span> | <span data-ttu-id="89d69-332">说明</span><span class="sxs-lookup"><span data-stu-id="89d69-332">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="89d69-333">枚举数组</span><span class="sxs-lookup"><span data-stu-id="89d69-333">array of enum</span></span>|<span data-ttu-id="89d69-334">3</span><span class="sxs-lookup"><span data-stu-id="89d69-334">3</span></span>|<span data-ttu-id="89d69-335">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-335">✔</span></span>|<span data-ttu-id="89d69-336">指定命令列表有效的作用域。</span><span class="sxs-lookup"><span data-stu-id="89d69-336">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="89d69-337">选项包括 `team`、`personal` 和 `groupchat`。</span><span class="sxs-lookup"><span data-stu-id="89d69-337">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="89d69-338">对象数组</span><span class="sxs-lookup"><span data-stu-id="89d69-338">array of objects</span></span>|<span data-ttu-id="89d69-339">10  </span><span class="sxs-lookup"><span data-stu-id="89d69-339">10</span></span>|<span data-ttu-id="89d69-340">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-340">✔</span></span>|<span data-ttu-id="89d69-341">自动程序支持的命令数组：</span><span class="sxs-lookup"><span data-stu-id="89d69-341">An array of commands the bot supports:</span></span><br><span data-ttu-id="89d69-342">`title`：自动程序命令名称（字符串，32）</span><span class="sxs-lookup"><span data-stu-id="89d69-342">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="89d69-343">`description`：命令语法及其参数的简单描述或示例（字符串，128）</span><span class="sxs-lookup"><span data-stu-id="89d69-343">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

## <a name="connectors"></a><span data-ttu-id="89d69-344">连接器</span><span class="sxs-lookup"><span data-stu-id="89d69-344">connectors</span></span>

<span data-ttu-id="89d69-345">**可选**</span><span class="sxs-lookup"><span data-stu-id="89d69-345">**Optional**</span></span>

<span data-ttu-id="89d69-346">`connectors`此块为应用定义 Office 365 连接器。</span><span class="sxs-lookup"><span data-stu-id="89d69-346">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="89d69-347">对象是一个数组， (类型的所有元素) 1 个元素 `object` 。</span><span class="sxs-lookup"><span data-stu-id="89d69-347">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="89d69-348">只有提供连接器的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="89d69-348">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="89d69-349">名称</span><span class="sxs-lookup"><span data-stu-id="89d69-349">Name</span></span>| <span data-ttu-id="89d69-350">类型</span><span class="sxs-lookup"><span data-stu-id="89d69-350">Type</span></span>| <span data-ttu-id="89d69-351">最大大小</span><span class="sxs-lookup"><span data-stu-id="89d69-351">Maximum size</span></span> | <span data-ttu-id="89d69-352">必需</span><span class="sxs-lookup"><span data-stu-id="89d69-352">Required</span></span> | <span data-ttu-id="89d69-353">说明</span><span class="sxs-lookup"><span data-stu-id="89d69-353">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="89d69-354">String</span><span class="sxs-lookup"><span data-stu-id="89d69-354">String</span></span>|<span data-ttu-id="89d69-355">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-355">2048 characters</span></span>|<span data-ttu-id="89d69-356">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-356">✔</span></span>|<span data-ttu-id="89d69-357">配置 https:// 时将使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="89d69-357">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="89d69-358">字符串</span><span class="sxs-lookup"><span data-stu-id="89d69-358">String</span></span>|<span data-ttu-id="89d69-359">64 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-359">64 characters</span></span>|<span data-ttu-id="89d69-360">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-360">✔</span></span>|<span data-ttu-id="89d69-361">连接器的唯一标识符，与连接器开发人员仪表板中的 ID [相匹配](https://aka.ms/connectorsdashboard)。</span><span class="sxs-lookup"><span data-stu-id="89d69-361">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="89d69-362">枚举数组</span><span class="sxs-lookup"><span data-stu-id="89d69-362">Array of enum</span></span>|<span data-ttu-id="89d69-363">1</span><span class="sxs-lookup"><span data-stu-id="89d69-363">1</span></span>|<span data-ttu-id="89d69-364">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-364">✔</span></span>|<span data-ttu-id="89d69-365">指定连接器是提供在 中频道上下文中的体验，还是仅针对单个用户 `team` `personal` () 。</span><span class="sxs-lookup"><span data-stu-id="89d69-365">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="89d69-366">目前，仅 `team` 支持范围。</span><span class="sxs-lookup"><span data-stu-id="89d69-366">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="89d69-367">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="89d69-367">composeExtensions</span></span>

<span data-ttu-id="89d69-368">**可选**</span><span class="sxs-lookup"><span data-stu-id="89d69-368">**Optional**</span></span>

<span data-ttu-id="89d69-369">为应用定义消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="89d69-369">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="89d69-370">2017 年 11 月，功能名称从"撰写扩展"更改为"邮件扩展"，但清单名称保持不变，以便现有扩展继续工作。</span><span class="sxs-lookup"><span data-stu-id="89d69-370">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="89d69-371">对象是一个数组， (类型的所有元素) 1 个元素 `object` 。</span><span class="sxs-lookup"><span data-stu-id="89d69-371">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="89d69-372">只有提供邮件扩展的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="89d69-372">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="89d69-373">名称</span><span class="sxs-lookup"><span data-stu-id="89d69-373">Name</span></span>| <span data-ttu-id="89d69-374">类型</span><span class="sxs-lookup"><span data-stu-id="89d69-374">Type</span></span> | <span data-ttu-id="89d69-375">最大大小</span><span class="sxs-lookup"><span data-stu-id="89d69-375">Maximum Size</span></span> | <span data-ttu-id="89d69-376">必需</span><span class="sxs-lookup"><span data-stu-id="89d69-376">Required</span></span> | <span data-ttu-id="89d69-377">说明</span><span class="sxs-lookup"><span data-stu-id="89d69-377">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="89d69-378">String</span><span class="sxs-lookup"><span data-stu-id="89d69-378">String</span></span>|<span data-ttu-id="89d69-379">64</span><span class="sxs-lookup"><span data-stu-id="89d69-379">64</span></span>|<span data-ttu-id="89d69-380">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-380">✔</span></span>|<span data-ttu-id="89d69-381">自动程序支持消息传递扩展的唯一 Microsoft 应用 ID，在 Bot Framework 中注册。</span><span class="sxs-lookup"><span data-stu-id="89d69-381">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="89d69-382">这可能与整个应用 [ID 相同](#id)。</span><span class="sxs-lookup"><span data-stu-id="89d69-382">This may well be the same as the overall [app ID](#id).</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="89d69-383">布尔</span><span class="sxs-lookup"><span data-stu-id="89d69-383">Boolean</span></span>|||<span data-ttu-id="89d69-384">一个值，指示用户是否可以更新邮件扩展的配置。</span><span class="sxs-lookup"><span data-stu-id="89d69-384">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="89d69-385">默认值为 `false`。</span><span class="sxs-lookup"><span data-stu-id="89d69-385">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="89d69-386">对象数组</span><span class="sxs-lookup"><span data-stu-id="89d69-386">Array of object</span></span>|<span data-ttu-id="89d69-387">10  </span><span class="sxs-lookup"><span data-stu-id="89d69-387">10</span></span>|<span data-ttu-id="89d69-388">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-388">✔</span></span>|<span data-ttu-id="89d69-389">邮件扩展支持的命令数组</span><span class="sxs-lookup"><span data-stu-id="89d69-389">Array of commands the messaging extension supports</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="89d69-390">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="89d69-390">composeExtensions.commands</span></span>

<span data-ttu-id="89d69-391">邮件扩展应声明一个或多个命令。</span><span class="sxs-lookup"><span data-stu-id="89d69-391">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="89d69-392">每个命令在 Microsoft Teams 中显示为基于 UI 的入口点的潜在交互。</span><span class="sxs-lookup"><span data-stu-id="89d69-392">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="89d69-393">最多有 10 个命令。</span><span class="sxs-lookup"><span data-stu-id="89d69-393">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="89d69-394">每个命令项都是具有以下结构的对象：</span><span class="sxs-lookup"><span data-stu-id="89d69-394">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="89d69-395">名称</span><span class="sxs-lookup"><span data-stu-id="89d69-395">Name</span></span>| <span data-ttu-id="89d69-396">类型</span><span class="sxs-lookup"><span data-stu-id="89d69-396">Type</span></span>| <span data-ttu-id="89d69-397">最大大小</span><span class="sxs-lookup"><span data-stu-id="89d69-397">Maximum size</span></span> | <span data-ttu-id="89d69-398">必需</span><span class="sxs-lookup"><span data-stu-id="89d69-398">Required</span></span> | <span data-ttu-id="89d69-399">说明</span><span class="sxs-lookup"><span data-stu-id="89d69-399">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="89d69-400">字符串</span><span class="sxs-lookup"><span data-stu-id="89d69-400">String</span></span>|<span data-ttu-id="89d69-401">64 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-401">64 characters</span></span>|<span data-ttu-id="89d69-402">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-402">✔</span></span>|<span data-ttu-id="89d69-403">命令的 ID</span><span class="sxs-lookup"><span data-stu-id="89d69-403">The ID for the command</span></span>|
|`type`|<span data-ttu-id="89d69-404">字符串</span><span class="sxs-lookup"><span data-stu-id="89d69-404">String</span></span>|<span data-ttu-id="89d69-405">64 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-405">64 characters</span></span>||<span data-ttu-id="89d69-406">命令的类型。</span><span class="sxs-lookup"><span data-stu-id="89d69-406">Type of the command.</span></span> <span data-ttu-id="89d69-407">或 `query` `action` 之一。</span><span class="sxs-lookup"><span data-stu-id="89d69-407">One of `query` or `action`.</span></span> <span data-ttu-id="89d69-408">默认值： `query`</span><span class="sxs-lookup"><span data-stu-id="89d69-408">Default: `query`</span></span>|
|`title`|<span data-ttu-id="89d69-409">String</span><span class="sxs-lookup"><span data-stu-id="89d69-409">String</span></span>|<span data-ttu-id="89d69-410">32 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-410">32 characters</span></span>|<span data-ttu-id="89d69-411">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-411">✔</span></span>|<span data-ttu-id="89d69-412">用户友好命令名称</span><span class="sxs-lookup"><span data-stu-id="89d69-412">The user-friendly command name</span></span>|
|`description`|<span data-ttu-id="89d69-413">String</span><span class="sxs-lookup"><span data-stu-id="89d69-413">String</span></span>|<span data-ttu-id="89d69-414">128 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-414">128 characters</span></span>||<span data-ttu-id="89d69-415">向用户显示以指示此命令用途的说明</span><span class="sxs-lookup"><span data-stu-id="89d69-415">The description that appears to users to indicate the purpose of this command</span></span>|
|`initialRun`|<span data-ttu-id="89d69-416">布尔</span><span class="sxs-lookup"><span data-stu-id="89d69-416">Boolean</span></span>|||<span data-ttu-id="89d69-417">一个布尔值，指示命令最初是否应该没有参数运行。</span><span class="sxs-lookup"><span data-stu-id="89d69-417">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="89d69-418">默认值： `false`</span><span class="sxs-lookup"><span data-stu-id="89d69-418">Default: `false`</span></span>|
|`context`|<span data-ttu-id="89d69-419">Array of Strings</span><span class="sxs-lookup"><span data-stu-id="89d69-419">Array of Strings</span></span>|<span data-ttu-id="89d69-420">3</span><span class="sxs-lookup"><span data-stu-id="89d69-420">3</span></span>||<span data-ttu-id="89d69-421">定义可以从何处调用邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="89d69-421">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="89d69-422">、 `compose` 、 的任意 `commandBox` 组合 `message` 。</span><span class="sxs-lookup"><span data-stu-id="89d69-422">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="89d69-423">默认值为 `["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="89d69-423">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="89d69-424">布尔</span><span class="sxs-lookup"><span data-stu-id="89d69-424">Boolean</span></span>|||<span data-ttu-id="89d69-425">一个布尔值，指示它应动态提取任务模块</span><span class="sxs-lookup"><span data-stu-id="89d69-425">A boolean value that indicates if it should fetch the task module dynamically</span></span>|
|`taskInfo`|<span data-ttu-id="89d69-426">Object</span><span class="sxs-lookup"><span data-stu-id="89d69-426">Object</span></span>|||<span data-ttu-id="89d69-427">指定在使用消息传递扩展命令时要预加载的任务模块</span><span class="sxs-lookup"><span data-stu-id="89d69-427">Specify the task module to preload when using a messaging extension command</span></span>|
|`taskInfo.title`|<span data-ttu-id="89d69-428">String</span><span class="sxs-lookup"><span data-stu-id="89d69-428">String</span></span>|<span data-ttu-id="89d69-429">64</span><span class="sxs-lookup"><span data-stu-id="89d69-429">64</span></span>||<span data-ttu-id="89d69-430">初始对话框标题</span><span class="sxs-lookup"><span data-stu-id="89d69-430">Initial dialog title</span></span>|
|`taskInfo.width`|<span data-ttu-id="89d69-431">String</span><span class="sxs-lookup"><span data-stu-id="89d69-431">String</span></span>|||<span data-ttu-id="89d69-432">对话框宽度 - 一个数字（以像素为单位）或默认布局，例如"large"、"medium"或"small"</span><span class="sxs-lookup"><span data-stu-id="89d69-432">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.height`|<span data-ttu-id="89d69-433">String</span><span class="sxs-lookup"><span data-stu-id="89d69-433">String</span></span>|||<span data-ttu-id="89d69-434">对话框高度 - 一个数字（以像素为单位）或默认布局，例如"large"、"medium"或"small"</span><span class="sxs-lookup"><span data-stu-id="89d69-434">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.url`|<span data-ttu-id="89d69-435">String</span><span class="sxs-lookup"><span data-stu-id="89d69-435">String</span></span>|||<span data-ttu-id="89d69-436">初始 Web 视图 URL</span><span class="sxs-lookup"><span data-stu-id="89d69-436">Initial webview URL</span></span>|
|`messageHandlers`|<span data-ttu-id="89d69-437">对象数组</span><span class="sxs-lookup"><span data-stu-id="89d69-437">Array of Objects</span></span>|<span data-ttu-id="89d69-438">5 </span><span class="sxs-lookup"><span data-stu-id="89d69-438">5</span></span>||<span data-ttu-id="89d69-439">允许满足某些条件时调用应用的处理程序列表。</span><span class="sxs-lookup"><span data-stu-id="89d69-439">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="89d69-440">还必须在 中列出域 `validDomains`</span><span class="sxs-lookup"><span data-stu-id="89d69-440">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="89d69-441">String</span><span class="sxs-lookup"><span data-stu-id="89d69-441">String</span></span>|||<span data-ttu-id="89d69-442">消息处理程序的类型。</span><span class="sxs-lookup"><span data-stu-id="89d69-442">The type of message handler.</span></span> <span data-ttu-id="89d69-443">必须是 `"link"`。</span><span class="sxs-lookup"><span data-stu-id="89d69-443">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="89d69-444">Array of Strings</span><span class="sxs-lookup"><span data-stu-id="89d69-444">Array of Strings</span></span>|||<span data-ttu-id="89d69-445">链接邮件处理程序可以注册的域数组。</span><span class="sxs-lookup"><span data-stu-id="89d69-445">Array of domains that the link message handler can register for.</span></span>|
|`parameters`|<span data-ttu-id="89d69-446">对象数组</span><span class="sxs-lookup"><span data-stu-id="89d69-446">Array of object</span></span>|<span data-ttu-id="89d69-447">5 </span><span class="sxs-lookup"><span data-stu-id="89d69-447">5</span></span>|<span data-ttu-id="89d69-448">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-448">✔</span></span>|<span data-ttu-id="89d69-449">命令采用的参数列表。</span><span class="sxs-lookup"><span data-stu-id="89d69-449">The list of parameters the command takes.</span></span> <span data-ttu-id="89d69-450">最小值：1;最大值：5</span><span class="sxs-lookup"><span data-stu-id="89d69-450">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="89d69-451">字符串</span><span class="sxs-lookup"><span data-stu-id="89d69-451">String</span></span>|<span data-ttu-id="89d69-452">64 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-452">64 characters</span></span>|<span data-ttu-id="89d69-453">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-453">✔</span></span>|<span data-ttu-id="89d69-454">显示在客户端中的参数的名称。</span><span class="sxs-lookup"><span data-stu-id="89d69-454">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="89d69-455">这包括在用户请求中。</span><span class="sxs-lookup"><span data-stu-id="89d69-455">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="89d69-456">String</span><span class="sxs-lookup"><span data-stu-id="89d69-456">String</span></span>|<span data-ttu-id="89d69-457">32 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-457">32 characters</span></span>|<span data-ttu-id="89d69-458">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-458">✔</span></span>|<span data-ttu-id="89d69-459">参数的用户友好标题。</span><span class="sxs-lookup"><span data-stu-id="89d69-459">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="89d69-460">String</span><span class="sxs-lookup"><span data-stu-id="89d69-460">String</span></span>|<span data-ttu-id="89d69-461">128 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-461">128 characters</span></span>||<span data-ttu-id="89d69-462">描述此参数用途的用户友好字符串。</span><span class="sxs-lookup"><span data-stu-id="89d69-462">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="89d69-463">String</span><span class="sxs-lookup"><span data-stu-id="89d69-463">String</span></span>|<span data-ttu-id="89d69-464">128 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-464">128 characters</span></span>||<span data-ttu-id="89d69-465">定义在任务模块上显示的控件的类型 `fetchTask: true` 。</span><span class="sxs-lookup"><span data-stu-id="89d69-465">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="89d69-466">、 `text` `textarea` 、 `number` 、 、 `date` 、 `time` 之 `toggle` 一 `choiceset`</span><span class="sxs-lookup"><span data-stu-id="89d69-466">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`</span></span>|
|`parameter.choices`|<span data-ttu-id="89d69-467">对象数组</span><span class="sxs-lookup"><span data-stu-id="89d69-467">Array of Objects</span></span>|<span data-ttu-id="89d69-468">10  </span><span class="sxs-lookup"><span data-stu-id="89d69-468">10</span></span>||<span data-ttu-id="89d69-469">的选项 `choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="89d69-469">The choice options for the `choiceset`.</span></span> <span data-ttu-id="89d69-470">仅在为 `parameter.inputType` 时使用 `choiceset`</span><span class="sxs-lookup"><span data-stu-id="89d69-470">Use only when `parameter.inputType` is `choiceset`</span></span>|
|`parameter.choices.title`|<span data-ttu-id="89d69-471">String</span><span class="sxs-lookup"><span data-stu-id="89d69-471">String</span></span>|<span data-ttu-id="89d69-472">128</span><span class="sxs-lookup"><span data-stu-id="89d69-472">128</span></span>||<span data-ttu-id="89d69-473">选择的标题</span><span class="sxs-lookup"><span data-stu-id="89d69-473">Title of the choice</span></span>|
|`parameter.choices.value`|<span data-ttu-id="89d69-474">String</span><span class="sxs-lookup"><span data-stu-id="89d69-474">String</span></span>|<span data-ttu-id="89d69-475">512</span><span class="sxs-lookup"><span data-stu-id="89d69-475">512</span></span>||<span data-ttu-id="89d69-476">选择的值</span><span class="sxs-lookup"><span data-stu-id="89d69-476">Value of the choice</span></span>|

## <a name="permissions"></a><span data-ttu-id="89d69-477">权限</span><span class="sxs-lookup"><span data-stu-id="89d69-477">permissions</span></span>

<span data-ttu-id="89d69-478">**可选**</span><span class="sxs-lookup"><span data-stu-id="89d69-478">**Optional**</span></span>

<span data-ttu-id="89d69-479">一个数组，指定应用请求哪些权限，让最终用户 `string` 知道扩展将执行什么操作。</span><span class="sxs-lookup"><span data-stu-id="89d69-479">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="89d69-480">以下选项非独占：</span><span class="sxs-lookup"><span data-stu-id="89d69-480">The following options are non-exclusive:</span></span>

* <span data-ttu-id="89d69-481">`identity`&emsp;需要用户标识信息</span><span class="sxs-lookup"><span data-stu-id="89d69-481">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="89d69-482">`messageTeamMembers`&emsp;需要向团队成员发送直接消息的权限</span><span class="sxs-lookup"><span data-stu-id="89d69-482">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="89d69-483">在更新应用时更改这些权限将导致用户在首次运行更新后的应用时重复同意过程。</span><span class="sxs-lookup"><span data-stu-id="89d69-483">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="89d69-484">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="89d69-484">devicePermissions</span></span>

<span data-ttu-id="89d69-485">**可选** 字符串数组</span><span class="sxs-lookup"><span data-stu-id="89d69-485">**Optional** Array of Strings</span></span>

<span data-ttu-id="89d69-486">指定应用可能请求访问的用户设备上本机功能。</span><span class="sxs-lookup"><span data-stu-id="89d69-486">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="89d69-487">选项有：</span><span class="sxs-lookup"><span data-stu-id="89d69-487">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="89d69-488">validDomains</span><span class="sxs-lookup"><span data-stu-id="89d69-488">validDomains</span></span>

<span data-ttu-id="89d69-489">**可选**，但 **已指出的必需** 项除外</span><span class="sxs-lookup"><span data-stu-id="89d69-489">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="89d69-490">应用预期从其中加载任何内容的有效域的列表。</span><span class="sxs-lookup"><span data-stu-id="89d69-490">A list of valid domains from which the app expects to load any content.</span></span> <span data-ttu-id="89d69-491">域列表可以包含通配符，例如 `*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="89d69-491">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="89d69-492">这完全匹配域的一个段;如果需要匹配，请使用 `a.b.example.com` `*.*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="89d69-492">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="89d69-493">如果你的选项卡配置或内容 UI 需要导航到除用于选项卡配置的其他任何其他域，则必须在此处指定该域。</span><span class="sxs-lookup"><span data-stu-id="89d69-493">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="89d69-494">但是 **，** 不需要在应用中包含要支持的标识提供程序的域。</span><span class="sxs-lookup"><span data-stu-id="89d69-494">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="89d69-495">例如，若要使用 Google ID 进行身份验证，必须重定向到 accounts.google.com，但不应将 accounts.google.com 包括在 `validDomains[]` 中。</span><span class="sxs-lookup"><span data-stu-id="89d69-495">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89d69-496">不要直接或通过通配符添加超出你控制的域。</span><span class="sxs-lookup"><span data-stu-id="89d69-496">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="89d69-497">例如， `yourapp.onmicrosoft.com` 有效，但 `*.onmicrosoft.com` 无效。</span><span class="sxs-lookup"><span data-stu-id="89d69-497">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="89d69-498">对象是包含类型 的所有元素的数组 `string` 。</span><span class="sxs-lookup"><span data-stu-id="89d69-498">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="89d69-499">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="89d69-499">webApplicationInfo</span></span>

<span data-ttu-id="89d69-500">**可选**</span><span class="sxs-lookup"><span data-stu-id="89d69-500">**Optional**</span></span>

<span data-ttu-id="89d69-501">指定 AAD 应用 ID 和 Graph 信息，以帮助用户无缝登录 AAD 应用。</span><span class="sxs-lookup"><span data-stu-id="89d69-501">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="89d69-502">名称</span><span class="sxs-lookup"><span data-stu-id="89d69-502">Name</span></span>| <span data-ttu-id="89d69-503">类型</span><span class="sxs-lookup"><span data-stu-id="89d69-503">Type</span></span>| <span data-ttu-id="89d69-504">最大大小</span><span class="sxs-lookup"><span data-stu-id="89d69-504">Maximum size</span></span> | <span data-ttu-id="89d69-505">必需</span><span class="sxs-lookup"><span data-stu-id="89d69-505">Required</span></span> | <span data-ttu-id="89d69-506">说明</span><span class="sxs-lookup"><span data-stu-id="89d69-506">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="89d69-507">String</span><span class="sxs-lookup"><span data-stu-id="89d69-507">String</span></span>|<span data-ttu-id="89d69-508">36 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-508">36 characters</span></span>|<span data-ttu-id="89d69-509">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-509">✔</span></span>|<span data-ttu-id="89d69-510">应用的 AAD 应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="89d69-510">AAD application id of the app.</span></span> <span data-ttu-id="89d69-511">此 ID 必须是 GUID。</span><span class="sxs-lookup"><span data-stu-id="89d69-511">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="89d69-512">String</span><span class="sxs-lookup"><span data-stu-id="89d69-512">String</span></span>|<span data-ttu-id="89d69-513">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="89d69-513">2048 characters</span></span>|<span data-ttu-id="89d69-514">✔</span><span class="sxs-lookup"><span data-stu-id="89d69-514">✔</span></span>|<span data-ttu-id="89d69-515">用于获取 SSO 身份验证令牌的应用的资源 URL。</span><span class="sxs-lookup"><span data-stu-id="89d69-515">Resource url of app for acquiring auth token for SSO.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="89d69-516">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="89d69-516">configurableProperties</span></span>

<span data-ttu-id="89d69-517">**可选** - 数组</span><span class="sxs-lookup"><span data-stu-id="89d69-517">**Optional** - array</span></span>

<span data-ttu-id="89d69-518">`configurableProperties`此块定义 Teams 管理员可以自定义的应用属性。</span><span class="sxs-lookup"><span data-stu-id="89d69-518">The `configurableProperties` block defines the app properties that Teams admin can customize.</span></span> <span data-ttu-id="89d69-519">有关详细信息，请参阅在 [Microsoft Teams 中自定义应用](/MicrosoftTeams/customize-apps)。</span><span class="sxs-lookup"><span data-stu-id="89d69-519">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="89d69-520">必须定义至少一个属性。</span><span class="sxs-lookup"><span data-stu-id="89d69-520">A minimum of one property must be defined.</span></span> <span data-ttu-id="89d69-521">最多可以在此块中定义九个属性。</span><span class="sxs-lookup"><span data-stu-id="89d69-521">You can define a maximum of nine properties in this block.</span></span>
> <span data-ttu-id="89d69-522">最佳做法是，你必须提供自定义指南，以便应用用户和客户在自定义应用时遵循这些准则。</span><span class="sxs-lookup"><span data-stu-id="89d69-522">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> 

<span data-ttu-id="89d69-523">可以定义以下任一属性：</span><span class="sxs-lookup"><span data-stu-id="89d69-523">You can define any of the following properties:</span></span>
* <span data-ttu-id="89d69-524">`name`：允许管理员更改应用显示名称。</span><span class="sxs-lookup"><span data-stu-id="89d69-524">`name`: Allows admin to change the app's display name.</span></span>
* <span data-ttu-id="89d69-525">`shortDescription`：允许管理员更改应用的简短说明。</span><span class="sxs-lookup"><span data-stu-id="89d69-525">`shortDescription`: Allows admin to change the app's short description.</span></span>
* <span data-ttu-id="89d69-526">`longDescription`：允许管理员更改应用的详细说明。</span><span class="sxs-lookup"><span data-stu-id="89d69-526">`longDescription`: Allows admin to change the app's detailed description.</span></span>
* <span data-ttu-id="89d69-527">`smallImageUrl`：它是 `outline` 清单 `icons` 块中的 属性。</span><span class="sxs-lookup"><span data-stu-id="89d69-527">`smallImageUrl`: It is `outline` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="89d69-528">`largeImageUrl`：它是 `color` 清单块 `icons` 中的 属性。</span><span class="sxs-lookup"><span data-stu-id="89d69-528">`largeImageUrl`: It is the `color` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="89d69-529">`accentColor`：它是要与 和 一起使用的颜色，作为大纲图标的背景。</span><span class="sxs-lookup"><span data-stu-id="89d69-529">`accentColor`: It is the color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="89d69-530">`developerUrl`：它是 https:// 网站的 URL。</span><span class="sxs-lookup"><span data-stu-id="89d69-530">`developerUrl`: It is the https:// URL to the developer's website.</span></span>
* <span data-ttu-id="89d69-531">`privacyUrl`：它是 https:// 隐私策略的 URL。</span><span class="sxs-lookup"><span data-stu-id="89d69-531">`privacyUrl`: It is the https:// URL to the developer's privacy policy.</span></span>
* <span data-ttu-id="89d69-532">`termsOfUseUrl`：它是 https:// 使用条款的 URL。</span><span class="sxs-lookup"><span data-stu-id="89d69-532">`termsOfUseUrl`: It is the https:// URL to the developer's terms of use.</span></span>

## <a name="defaultinstallscope"></a><span data-ttu-id="89d69-533">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="89d69-533">defaultInstallScope</span></span>

<span data-ttu-id="89d69-534">**可选** - string</span><span class="sxs-lookup"><span data-stu-id="89d69-534">**Optional** - string</span></span>

<span data-ttu-id="89d69-535">指定默认情况下为此应用定义的安装范围。</span><span class="sxs-lookup"><span data-stu-id="89d69-535">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="89d69-536">定义的范围将是当用户尝试添加应用时按钮上显示的选项。</span><span class="sxs-lookup"><span data-stu-id="89d69-536">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="89d69-537">选项有：</span><span class="sxs-lookup"><span data-stu-id="89d69-537">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="89d69-538">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="89d69-538">defaultGroupCapability</span></span>

<span data-ttu-id="89d69-539">**可选** - object</span><span class="sxs-lookup"><span data-stu-id="89d69-539">**Optional** - object</span></span>

<span data-ttu-id="89d69-540">选择组安装范围后，它将在用户安装应用时定义默认功能。</span><span class="sxs-lookup"><span data-stu-id="89d69-540">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="89d69-541">选项有：</span><span class="sxs-lookup"><span data-stu-id="89d69-541">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="89d69-542">名称</span><span class="sxs-lookup"><span data-stu-id="89d69-542">Name</span></span>| <span data-ttu-id="89d69-543">类型</span><span class="sxs-lookup"><span data-stu-id="89d69-543">Type</span></span>| <span data-ttu-id="89d69-544">最大大小</span><span class="sxs-lookup"><span data-stu-id="89d69-544">Maximum size</span></span> | <span data-ttu-id="89d69-545">必需</span><span class="sxs-lookup"><span data-stu-id="89d69-545">Required</span></span> | <span data-ttu-id="89d69-546">说明</span><span class="sxs-lookup"><span data-stu-id="89d69-546">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="89d69-547">string</span><span class="sxs-lookup"><span data-stu-id="89d69-547">string</span></span>|||<span data-ttu-id="89d69-548">当选择的安装范围为 `team` 时，此字段指定可用的默认功能。</span><span class="sxs-lookup"><span data-stu-id="89d69-548">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="89d69-549">选项 `tab` ：、 `bot` 或 `connector` 。</span><span class="sxs-lookup"><span data-stu-id="89d69-549">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="89d69-550">string</span><span class="sxs-lookup"><span data-stu-id="89d69-550">string</span></span>|||<span data-ttu-id="89d69-551">当选择的安装范围为 `groupchat` 时，此字段指定可用的默认功能。</span><span class="sxs-lookup"><span data-stu-id="89d69-551">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="89d69-552">选项 `tab` ：、 `bot` 或 `connector` 。</span><span class="sxs-lookup"><span data-stu-id="89d69-552">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="89d69-553">string</span><span class="sxs-lookup"><span data-stu-id="89d69-553">string</span></span>|||<span data-ttu-id="89d69-554">当选择的安装范围为 `meetings` 时，此字段指定可用的默认功能。</span><span class="sxs-lookup"><span data-stu-id="89d69-554">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="89d69-555">选项 `tab` ：、 `bot` 或 `connector` 。</span><span class="sxs-lookup"><span data-stu-id="89d69-555">Options: `tab`, `bot`, or `connector`.</span></span>|

