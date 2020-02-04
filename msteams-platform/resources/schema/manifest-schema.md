---
title: 清单架构参考
description: 介绍 Microsoft 团队清单支持的架构
keywords: 团队清单架构
ms.openlocfilehash: d4a2864c18a5066673bafab42a46733a0ab5f116
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673271"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="7765b-104">参考： Microsoft 团队的清单架构</span><span class="sxs-lookup"><span data-stu-id="7765b-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="7765b-105">Microsoft 团队清单介绍了应用程序如何集成到 Microsoft 团队产品中。</span><span class="sxs-lookup"><span data-stu-id="7765b-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="7765b-106">您的清单必须符合托管的架构[`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json)。</span><span class="sxs-lookup"><span data-stu-id="7765b-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="7765b-107">此外，还支持早期版本 1.0-1.4 （使用 URL 中的 "v1"）。</span><span class="sxs-lookup"><span data-stu-id="7765b-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="7765b-108">以下架构示例显示了所有扩展性选项。</span><span class="sxs-lookup"><span data-stu-id="7765b-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="7765b-109">完整清单示例</span><span class="sxs-lookup"><span data-stu-id="7765b-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
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
    "defaultLanguageTag": "en-us",
    "additionalLanguages": [
      {
        "languageTag": "es-es",
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
        }
      ],
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
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
     "contoso.com",
     "mysite.someplace.com",
     "othersite.someplace.com"
  ]
}
```

<span data-ttu-id="7765b-110">架构定义了以下属性：</span><span class="sxs-lookup"><span data-stu-id="7765b-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="7765b-111">$schema</span><span class="sxs-lookup"><span data-stu-id="7765b-111">$schema</span></span>

<span data-ttu-id="7765b-112">*可选，但建议* &ndash;的字符串</span><span class="sxs-lookup"><span data-stu-id="7765b-112">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="7765b-113">引用清单的 JSON 架构的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="7765b-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="7765b-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="7765b-114">manifestVersion</span></span>

<span data-ttu-id="7765b-115">**必需** &ndash;的字符串</span><span class="sxs-lookup"><span data-stu-id="7765b-115">**Required** &ndash; String</span></span>

<span data-ttu-id="7765b-116">此清单使用的清单架构的版本。</span><span class="sxs-lookup"><span data-stu-id="7765b-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="7765b-117">它应为 "1.5"。</span><span class="sxs-lookup"><span data-stu-id="7765b-117">It should be "1.5".</span></span>

## <a name="version"></a><span data-ttu-id="7765b-118">version</span><span class="sxs-lookup"><span data-stu-id="7765b-118">version</span></span>

<span data-ttu-id="7765b-119">**必需** &ndash;的字符串</span><span class="sxs-lookup"><span data-stu-id="7765b-119">**Required** &ndash; String</span></span>

<span data-ttu-id="7765b-120">特定应用程序的版本。</span><span class="sxs-lookup"><span data-stu-id="7765b-120">The version of the specific app.</span></span> <span data-ttu-id="7765b-121">如果您更新清单中的某些内容，该版本还必须递增。</span><span class="sxs-lookup"><span data-stu-id="7765b-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="7765b-122">这样一来，在安装新的清单时，它将覆盖现有的版本，用户将获得新的功能。</span><span class="sxs-lookup"><span data-stu-id="7765b-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="7765b-123">如果此应用程序已提交到应用商店，则必须重新提交新清单，然后再对其进行重新验证。</span><span class="sxs-lookup"><span data-stu-id="7765b-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="7765b-124">然后，此应用程序的用户将在几小时内自动获取新更新的清单（在批准后）。</span><span class="sxs-lookup"><span data-stu-id="7765b-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="7765b-125">如果应用程序要求更改权限，则系统将提示用户升级并重新同意该应用。</span><span class="sxs-lookup"><span data-stu-id="7765b-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="7765b-126">此版本字符串必须遵循[semver](http://semver.org/) STANDARD （主要。网格.修补程序）。</span><span class="sxs-lookup"><span data-stu-id="7765b-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="7765b-127">id</span><span class="sxs-lookup"><span data-stu-id="7765b-127">id</span></span>

<span data-ttu-id="7765b-128">**必需** &ndash;的 Microsoft 应用程序 ID</span><span class="sxs-lookup"><span data-stu-id="7765b-128">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="7765b-129">Microsoft 为此应用程序生成的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="7765b-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="7765b-130">如果你已通过 Microsoft Bot 框架注册了 bot，或者你的选项卡的 web 应用已使用 Microsoft 登录，则你应该已经有 ID，应在此处输入它。</span><span class="sxs-lookup"><span data-stu-id="7765b-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="7765b-131">否则，应在 Microsoft 应用注册门户（[我的应用程序](https://apps.dev.microsoft.com)）上生成一个新的 ID，在此处输入它，然后在添加机器人时重用它。注意：如果您在 AppSource 中提交对现有应用程序的更新，您的清单中的 ID 不得修改。</span><span class="sxs-lookup"><span data-stu-id="7765b-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="packagename"></a><span data-ttu-id="7765b-132">packageName</span><span class="sxs-lookup"><span data-stu-id="7765b-132">packageName</span></span>

<span data-ttu-id="7765b-133">**必需** &ndash;的字符串</span><span class="sxs-lookup"><span data-stu-id="7765b-133">**Required** &ndash; String</span></span>

<span data-ttu-id="7765b-134">此应用的以反向域表示法表示的唯一标识符;例如，.com. myapp。</span><span class="sxs-lookup"><span data-stu-id="7765b-134">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="7765b-135">developer</span><span class="sxs-lookup"><span data-stu-id="7765b-135">developer</span></span>

<span data-ttu-id="7765b-136">**Required**</span><span class="sxs-lookup"><span data-stu-id="7765b-136">**Required**</span></span>

<span data-ttu-id="7765b-137">指定有关贵公司的信息。</span><span class="sxs-lookup"><span data-stu-id="7765b-137">Specifies information about your company.</span></span> <span data-ttu-id="7765b-138">对于提交到 AppSource （以前称为 "Office 应用商店"）的应用程序，这些值必须与您的 AppSource 条目中的信息相匹配。</span><span class="sxs-lookup"><span data-stu-id="7765b-138">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="7765b-139">有关详细信息，请参阅我们的[发布指南](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)。</span><span class="sxs-lookup"><span data-stu-id="7765b-139">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="7765b-140">姓名</span><span class="sxs-lookup"><span data-stu-id="7765b-140">Name</span></span>| <span data-ttu-id="7765b-141">最大大小</span><span class="sxs-lookup"><span data-stu-id="7765b-141">Maximum size</span></span> | <span data-ttu-id="7765b-142">必需</span><span class="sxs-lookup"><span data-stu-id="7765b-142">Required</span></span> | <span data-ttu-id="7765b-143">说明</span><span class="sxs-lookup"><span data-stu-id="7765b-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="7765b-144">32个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-144">32 characters</span></span>|<span data-ttu-id="7765b-145">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-145">✔</span></span>|<span data-ttu-id="7765b-146">开发人员的显示名称。</span><span class="sxs-lookup"><span data-stu-id="7765b-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="7765b-147">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-147">2048 characters</span></span>|<span data-ttu-id="7765b-148">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-148">✔</span></span>|<span data-ttu-id="7765b-149">开发人员网站的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="7765b-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="7765b-150">此链接应将用户带到您的公司或特定于产品的登陆页面。</span><span class="sxs-lookup"><span data-stu-id="7765b-150">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="7765b-151">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-151">2048 characters</span></span>|<span data-ttu-id="7765b-152">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-152">✔</span></span>|<span data-ttu-id="7765b-153">开发人员的隐私策略的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="7765b-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="7765b-154">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-154">2048 characters</span></span>|<span data-ttu-id="7765b-155">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-155">✔</span></span>|<span data-ttu-id="7765b-156">开发人员使用条款的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="7765b-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="7765b-157">10个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-157">10 characters</span></span>| |<span data-ttu-id="7765b-158">**可选**用于标识合作伙伴组织构建应用程序的 Microsoft 合作伙伴网络 ID。</span><span class="sxs-lookup"><span data-stu-id="7765b-158">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="7765b-159">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="7765b-159">localizationInfo</span></span>

<span data-ttu-id="7765b-160">**可选**</span><span class="sxs-lookup"><span data-stu-id="7765b-160">**Optional**</span></span>

<span data-ttu-id="7765b-161">允许指定默认语言，以及指向其他语言文件的指针。</span><span class="sxs-lookup"><span data-stu-id="7765b-161">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="7765b-162">请参阅[本地化](~/concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="7765b-162">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="7765b-163">姓名</span><span class="sxs-lookup"><span data-stu-id="7765b-163">Name</span></span>| <span data-ttu-id="7765b-164">最大大小</span><span class="sxs-lookup"><span data-stu-id="7765b-164">Maximum size</span></span> | <span data-ttu-id="7765b-165">必需</span><span class="sxs-lookup"><span data-stu-id="7765b-165">Required</span></span> | <span data-ttu-id="7765b-166">说明</span><span class="sxs-lookup"><span data-stu-id="7765b-166">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="7765b-167">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-167">✔</span></span>|<span data-ttu-id="7765b-168">此顶级清单文件中的字符串的语言标记。</span><span class="sxs-lookup"><span data-stu-id="7765b-168">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="7765b-169">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="7765b-169">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="7765b-170">指定其他语言翻译的对象的数组。</span><span class="sxs-lookup"><span data-stu-id="7765b-170">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="7765b-171">姓名</span><span class="sxs-lookup"><span data-stu-id="7765b-171">Name</span></span>| <span data-ttu-id="7765b-172">最大大小</span><span class="sxs-lookup"><span data-stu-id="7765b-172">Maximum size</span></span> | <span data-ttu-id="7765b-173">必需</span><span class="sxs-lookup"><span data-stu-id="7765b-173">Required</span></span> | <span data-ttu-id="7765b-174">说明</span><span class="sxs-lookup"><span data-stu-id="7765b-174">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="7765b-175">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-175">✔</span></span>|<span data-ttu-id="7765b-176">所提供文件中的字符串的语言标记。</span><span class="sxs-lookup"><span data-stu-id="7765b-176">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="7765b-177">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-177">✔</span></span>|<span data-ttu-id="7765b-178">包含翻译字符串的 json 文件的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="7765b-178">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="7765b-179">name</span><span class="sxs-lookup"><span data-stu-id="7765b-179">name</span></span>

<span data-ttu-id="7765b-180">**Required**</span><span class="sxs-lookup"><span data-stu-id="7765b-180">**Required**</span></span>

<span data-ttu-id="7765b-181">在团队体验中向用户显示的应用程序体验的名称。</span><span class="sxs-lookup"><span data-stu-id="7765b-181">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="7765b-182">对于提交到 AppSource 的应用程序，这些值必须与您的 AppSource 条目中的信息相匹配。</span><span class="sxs-lookup"><span data-stu-id="7765b-182">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="7765b-183">`short`和`full`的值不应相同。</span><span class="sxs-lookup"><span data-stu-id="7765b-183">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="7765b-184">姓名</span><span class="sxs-lookup"><span data-stu-id="7765b-184">Name</span></span>| <span data-ttu-id="7765b-185">最大大小</span><span class="sxs-lookup"><span data-stu-id="7765b-185">Maximum size</span></span> | <span data-ttu-id="7765b-186">必需</span><span class="sxs-lookup"><span data-stu-id="7765b-186">Required</span></span> | <span data-ttu-id="7765b-187">说明</span><span class="sxs-lookup"><span data-stu-id="7765b-187">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="7765b-188">30 个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-188">30 characters</span></span>|<span data-ttu-id="7765b-189">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-189">✔</span></span>|<span data-ttu-id="7765b-190">应用程序的短显示名称。</span><span class="sxs-lookup"><span data-stu-id="7765b-190">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="7765b-191">100 个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-191">100 characters</span></span>||<span data-ttu-id="7765b-192">应用程序的全名，如果完整的应用程序名称超过30个字符，则使用该名称。</span><span class="sxs-lookup"><span data-stu-id="7765b-192">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="7765b-193">说明</span><span class="sxs-lookup"><span data-stu-id="7765b-193">description</span></span>

<span data-ttu-id="7765b-194">**Required**</span><span class="sxs-lookup"><span data-stu-id="7765b-194">**Required**</span></span>

<span data-ttu-id="7765b-195">向用户介绍你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="7765b-195">Describes your app to users.</span></span> <span data-ttu-id="7765b-196">对于提交到 AppSource 的应用程序，这些值必须与您的 AppSource 条目中的信息相匹配。</span><span class="sxs-lookup"><span data-stu-id="7765b-196">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="7765b-197">确保你的说明准确描述你的体验，并提供信息，以帮助潜在客户了解你的体验。</span><span class="sxs-lookup"><span data-stu-id="7765b-197">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="7765b-198">如果需要使用外部帐户，还应在完整说明中说明。</span><span class="sxs-lookup"><span data-stu-id="7765b-198">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="7765b-199">`short`和`full`的值不应相同。</span><span class="sxs-lookup"><span data-stu-id="7765b-199">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="7765b-200">您的简短说明不得在详细说明中重复，并且不得包含任何其他应用程序名称。</span><span class="sxs-lookup"><span data-stu-id="7765b-200">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="7765b-201">姓名</span><span class="sxs-lookup"><span data-stu-id="7765b-201">Name</span></span>| <span data-ttu-id="7765b-202">最大大小</span><span class="sxs-lookup"><span data-stu-id="7765b-202">Maximum size</span></span> | <span data-ttu-id="7765b-203">必需</span><span class="sxs-lookup"><span data-stu-id="7765b-203">Required</span></span> | <span data-ttu-id="7765b-204">说明</span><span class="sxs-lookup"><span data-stu-id="7765b-204">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="7765b-205">80个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-205">80 characters</span></span>|<span data-ttu-id="7765b-206">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-206">✔</span></span>|<span data-ttu-id="7765b-207">在空间有限时使用的应用程序体验的简短说明。</span><span class="sxs-lookup"><span data-stu-id="7765b-207">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="7765b-208">4000个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-208">4000 characters</span></span>|<span data-ttu-id="7765b-209">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-209">✔</span></span>|<span data-ttu-id="7765b-210">您的应用程序的完整说明。</span><span class="sxs-lookup"><span data-stu-id="7765b-210">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="7765b-211">图标</span><span class="sxs-lookup"><span data-stu-id="7765b-211">icons</span></span>

<span data-ttu-id="7765b-212">**Required**</span><span class="sxs-lookup"><span data-stu-id="7765b-212">**Required**</span></span>

<span data-ttu-id="7765b-213">在团队应用程序中使用的图标。</span><span class="sxs-lookup"><span data-stu-id="7765b-213">Icons used within the Teams app.</span></span> <span data-ttu-id="7765b-214">图标文件必须作为上载包的一部分包括在内。</span><span class="sxs-lookup"><span data-stu-id="7765b-214">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="7765b-215">有关详细信息，请参阅[图标](~/concepts/build-and-test/apps-package.md#icons)。</span><span class="sxs-lookup"><span data-stu-id="7765b-215">See [Icons](~/concepts/build-and-test/apps-package.md#icons) for more information.</span></span>

|<span data-ttu-id="7765b-216">姓名</span><span class="sxs-lookup"><span data-stu-id="7765b-216">Name</span></span>| <span data-ttu-id="7765b-217">最大大小</span><span class="sxs-lookup"><span data-stu-id="7765b-217">Maximum size</span></span> | <span data-ttu-id="7765b-218">必需</span><span class="sxs-lookup"><span data-stu-id="7765b-218">Required</span></span> | <span data-ttu-id="7765b-219">说明</span><span class="sxs-lookup"><span data-stu-id="7765b-219">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="7765b-220">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-220">2048 characters</span></span>|<span data-ttu-id="7765b-221">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-221">✔</span></span>|<span data-ttu-id="7765b-222">指向透明 32x32 PNG 边框图标的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="7765b-222">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="7765b-223">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-223">2048 characters</span></span>|<span data-ttu-id="7765b-224">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-224">✔</span></span>|<span data-ttu-id="7765b-225">完整颜色 192x192 PNG 图标的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="7765b-225">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="7765b-226">accentColor</span><span class="sxs-lookup"><span data-stu-id="7765b-226">accentColor</span></span>

<span data-ttu-id="7765b-227">**必需** &ndash;的字符串</span><span class="sxs-lookup"><span data-stu-id="7765b-227">**Required** &ndash; String</span></span>

<span data-ttu-id="7765b-228">与大纲图标的背景一起使用的颜色。</span><span class="sxs-lookup"><span data-stu-id="7765b-228">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="7765b-229">值必须是以 "#" 开头的有效 HTML 颜色代码，例如`#4464ee`。</span><span class="sxs-lookup"><span data-stu-id="7765b-229">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="7765b-230">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="7765b-230">configurableTabs</span></span>

<span data-ttu-id="7765b-231">**可选**</span><span class="sxs-lookup"><span data-stu-id="7765b-231">**Optional**</span></span>

<span data-ttu-id="7765b-232">当您的应用程序体验具有在添加之前需要额外配置的团队频道选项卡体验时使用。</span><span class="sxs-lookup"><span data-stu-id="7765b-232">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="7765b-233">仅在团队作用域中支持可配置的选项卡，并且每个应用程序目前仅支持一个选项卡。</span><span class="sxs-lookup"><span data-stu-id="7765b-233">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="7765b-234">对象是一个包含所有类型`object`的元素的数组。</span><span class="sxs-lookup"><span data-stu-id="7765b-234">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="7765b-235">仅在提供可配置的通道选项卡解决方案的解决方案中，此块才是必需的。</span><span class="sxs-lookup"><span data-stu-id="7765b-235">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="7765b-236">名称</span><span class="sxs-lookup"><span data-stu-id="7765b-236">Name</span></span>| <span data-ttu-id="7765b-237">类型</span><span class="sxs-lookup"><span data-stu-id="7765b-237">Type</span></span>| <span data-ttu-id="7765b-238">最大大小</span><span class="sxs-lookup"><span data-stu-id="7765b-238">Maximum size</span></span> | <span data-ttu-id="7765b-239">必需</span><span class="sxs-lookup"><span data-stu-id="7765b-239">Required</span></span> | <span data-ttu-id="7765b-240">说明</span><span class="sxs-lookup"><span data-stu-id="7765b-240">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="7765b-241">String</span><span class="sxs-lookup"><span data-stu-id="7765b-241">String</span></span>|<span data-ttu-id="7765b-242">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-242">2048 characters</span></span>|<span data-ttu-id="7765b-243">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-243">✔</span></span>|<span data-ttu-id="7765b-244">配置选项卡时要使用的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="7765b-244">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="7765b-245">Boolean</span><span class="sxs-lookup"><span data-stu-id="7765b-245">Boolean</span></span>|||<span data-ttu-id="7765b-246">一个值，指示是否可在用户创建之后更新该选项卡的配置实例。</span><span class="sxs-lookup"><span data-stu-id="7765b-246">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="7765b-247">设置`true`</span><span class="sxs-lookup"><span data-stu-id="7765b-247">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="7765b-248">枚举数组</span><span class="sxs-lookup"><span data-stu-id="7765b-248">Array of enum</span></span>|<span data-ttu-id="7765b-249">1 </span><span class="sxs-lookup"><span data-stu-id="7765b-249">1</span></span>|<span data-ttu-id="7765b-250">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-250">✔</span></span>|<span data-ttu-id="7765b-251">目前，可配置的`team`选项卡仅`groupchat`支持和范围。</span><span class="sxs-lookup"><span data-stu-id="7765b-251">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="7765b-252">String</span><span class="sxs-lookup"><span data-stu-id="7765b-252">String</span></span>|<span data-ttu-id="7765b-253">2048</span><span class="sxs-lookup"><span data-stu-id="7765b-253">2048</span></span>||<span data-ttu-id="7765b-254">要在 SharePoint 中使用的选项卡预览图像的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="7765b-254">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="7765b-255">字号（1024x768）。</span><span class="sxs-lookup"><span data-stu-id="7765b-255">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="7765b-256">枚举数组</span><span class="sxs-lookup"><span data-stu-id="7765b-256">Array of enum</span></span>|<span data-ttu-id="7765b-257">1 </span><span class="sxs-lookup"><span data-stu-id="7765b-257">1</span></span>||<span data-ttu-id="7765b-258">定义您的选项卡在 SharePoint 中的可用方式。</span><span class="sxs-lookup"><span data-stu-id="7765b-258">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="7765b-259">选项包括`sharePointFullPage`和`sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="7765b-259">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="7765b-260">staticTabs</span><span class="sxs-lookup"><span data-stu-id="7765b-260">staticTabs</span></span>

<span data-ttu-id="7765b-261">**可选**</span><span class="sxs-lookup"><span data-stu-id="7765b-261">**Optional**</span></span>

<span data-ttu-id="7765b-262">定义一组可在默认情况下 "固定" 的选项卡，而无需用户手动添加它们。</span><span class="sxs-lookup"><span data-stu-id="7765b-262">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="7765b-263">在范围内声明`personal`的静态制表符始终固定到应用的个人体验中。</span><span class="sxs-lookup"><span data-stu-id="7765b-263">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="7765b-264">当前不支持在`team`范围中声明的静态选项卡。</span><span class="sxs-lookup"><span data-stu-id="7765b-264">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="7765b-265">对象是包含类型`object`的所有元素的数组（最多16个元素）。</span><span class="sxs-lookup"><span data-stu-id="7765b-265">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="7765b-266">仅在提供静态选项卡解决方案的解决方案中，此块是必需的。</span><span class="sxs-lookup"><span data-stu-id="7765b-266">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="7765b-267">名称</span><span class="sxs-lookup"><span data-stu-id="7765b-267">Name</span></span>| <span data-ttu-id="7765b-268">类型</span><span class="sxs-lookup"><span data-stu-id="7765b-268">Type</span></span>| <span data-ttu-id="7765b-269">最大大小</span><span class="sxs-lookup"><span data-stu-id="7765b-269">Maximum size</span></span> | <span data-ttu-id="7765b-270">必需</span><span class="sxs-lookup"><span data-stu-id="7765b-270">Required</span></span> | <span data-ttu-id="7765b-271">说明</span><span class="sxs-lookup"><span data-stu-id="7765b-271">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="7765b-272">String</span><span class="sxs-lookup"><span data-stu-id="7765b-272">String</span></span>|<span data-ttu-id="7765b-273">64个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-273">64 characters</span></span>|<span data-ttu-id="7765b-274">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-274">✔</span></span>|<span data-ttu-id="7765b-275">选项卡显示的实体的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="7765b-275">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="7765b-276">String</span><span class="sxs-lookup"><span data-stu-id="7765b-276">String</span></span>|<span data-ttu-id="7765b-277">128个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-277">128 characters</span></span>|<span data-ttu-id="7765b-278">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-278">✔</span></span>|<span data-ttu-id="7765b-279">该选项卡在通道接口中的显示名称。</span><span class="sxs-lookup"><span data-stu-id="7765b-279">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="7765b-280">String</span><span class="sxs-lookup"><span data-stu-id="7765b-280">String</span></span>|<span data-ttu-id="7765b-281">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-281">2048 characters</span></span>|<span data-ttu-id="7765b-282">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-282">✔</span></span>|<span data-ttu-id="7765b-283">指向要在团队画布中显示的实体 UI 的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="7765b-283">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="7765b-284">String</span><span class="sxs-lookup"><span data-stu-id="7765b-284">String</span></span>|<span data-ttu-id="7765b-285">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-285">2048 characters</span></span>||<span data-ttu-id="7765b-286">要指向的 https://URL，如果用户要在浏览器中查看。</span><span class="sxs-lookup"><span data-stu-id="7765b-286">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="7765b-287">枚举数组</span><span class="sxs-lookup"><span data-stu-id="7765b-287">Array of enum</span></span>|<span data-ttu-id="7765b-288">1 </span><span class="sxs-lookup"><span data-stu-id="7765b-288">1</span></span>|<span data-ttu-id="7765b-289">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-289">✔</span></span>|<span data-ttu-id="7765b-290">目前，静态选项卡仅支持`personal`作用域，这意味着它只能作为个人体验的一部分进行预配。</span><span class="sxs-lookup"><span data-stu-id="7765b-290">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="7765b-291">bot</span><span class="sxs-lookup"><span data-stu-id="7765b-291">bots</span></span>

<span data-ttu-id="7765b-292">**可选**</span><span class="sxs-lookup"><span data-stu-id="7765b-292">**Optional**</span></span>

<span data-ttu-id="7765b-293">定义机器人解决方案以及可选信息，如默认的命令属性。</span><span class="sxs-lookup"><span data-stu-id="7765b-293">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="7765b-294">该对象是数组（每个应用程序最多&mdash;只能有一个一个 bot 仅允许一个 bot）和所有类型`object`的元素。</span><span class="sxs-lookup"><span data-stu-id="7765b-294">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="7765b-295">仅在提供机器人体验的解决方案中，此块才是必需的。</span><span class="sxs-lookup"><span data-stu-id="7765b-295">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="7765b-296">名称</span><span class="sxs-lookup"><span data-stu-id="7765b-296">Name</span></span>| <span data-ttu-id="7765b-297">类型</span><span class="sxs-lookup"><span data-stu-id="7765b-297">Type</span></span>| <span data-ttu-id="7765b-298">最大大小</span><span class="sxs-lookup"><span data-stu-id="7765b-298">Maximum size</span></span> | <span data-ttu-id="7765b-299">必需</span><span class="sxs-lookup"><span data-stu-id="7765b-299">Required</span></span> | <span data-ttu-id="7765b-300">说明</span><span class="sxs-lookup"><span data-stu-id="7765b-300">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="7765b-301">String</span><span class="sxs-lookup"><span data-stu-id="7765b-301">String</span></span>|<span data-ttu-id="7765b-302">64个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-302">64 characters</span></span>|<span data-ttu-id="7765b-303">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-303">✔</span></span>|<span data-ttu-id="7765b-304">与 Bot 框架一起注册的 bot 的唯一 Microsoft 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="7765b-304">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="7765b-305">这可能与整体[应用程序 ID](#id)很好。</span><span class="sxs-lookup"><span data-stu-id="7765b-305">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="7765b-306">Boolean</span><span class="sxs-lookup"><span data-stu-id="7765b-306">Boolean</span></span>|||<span data-ttu-id="7765b-307">描述 bot 是否利用用户提示将机器人添加到特定频道。</span><span class="sxs-lookup"><span data-stu-id="7765b-307">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="7765b-308">设置`false`</span><span class="sxs-lookup"><span data-stu-id="7765b-308">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="7765b-309">Boolean</span><span class="sxs-lookup"><span data-stu-id="7765b-309">Boolean</span></span>|||<span data-ttu-id="7765b-310">指示 bot 是否为单向仅通知 bot，而不是对话机器人。</span><span class="sxs-lookup"><span data-stu-id="7765b-310">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="7765b-311">设置`false`</span><span class="sxs-lookup"><span data-stu-id="7765b-311">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="7765b-312">Boolean</span><span class="sxs-lookup"><span data-stu-id="7765b-312">Boolean</span></span>|||<span data-ttu-id="7765b-313">指示 bot 是否支持在个人聊天中上载/下载文件的功能。</span><span class="sxs-lookup"><span data-stu-id="7765b-313">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="7765b-314">设置`false`</span><span class="sxs-lookup"><span data-stu-id="7765b-314">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="7765b-315">枚举数组</span><span class="sxs-lookup"><span data-stu-id="7765b-315">Array of enum</span></span>|<span data-ttu-id="7765b-316">3 </span><span class="sxs-lookup"><span data-stu-id="7765b-316">3</span></span>|<span data-ttu-id="7765b-317">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-317">✔</span></span>|<span data-ttu-id="7765b-318">指定机器人是在中的频道上下文中`team`、在组中的聊天（`groupchat`）中，还是在仅限于单个用户（`personal`）的体验中提供体验。</span><span class="sxs-lookup"><span data-stu-id="7765b-318">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="7765b-319">这些选项是非独占的。</span><span class="sxs-lookup"><span data-stu-id="7765b-319">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="7765b-320">commandLists</span><span class="sxs-lookup"><span data-stu-id="7765b-320">bots.commandLists</span></span>

<span data-ttu-id="7765b-321">你的 bot 可以向用户推荐的命令的可选列表。</span><span class="sxs-lookup"><span data-stu-id="7765b-321">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="7765b-322">对象是包含所有类型`object`元素的数组（最多2个元素）;您必须为你的 bot 支持的每个作用域定义单独的命令列表。</span><span class="sxs-lookup"><span data-stu-id="7765b-322">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="7765b-323">有关详细信息，请参阅[Bot 菜单](~/bots/how-to/create-a-bot-commands-menu.md)。</span><span class="sxs-lookup"><span data-stu-id="7765b-323">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="7765b-324">名称</span><span class="sxs-lookup"><span data-stu-id="7765b-324">Name</span></span>| <span data-ttu-id="7765b-325">类型</span><span class="sxs-lookup"><span data-stu-id="7765b-325">Type</span></span>| <span data-ttu-id="7765b-326">最大大小</span><span class="sxs-lookup"><span data-stu-id="7765b-326">Maximum size</span></span> | <span data-ttu-id="7765b-327">必需</span><span class="sxs-lookup"><span data-stu-id="7765b-327">Required</span></span> | <span data-ttu-id="7765b-328">说明</span><span class="sxs-lookup"><span data-stu-id="7765b-328">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="7765b-329">枚举数组</span><span class="sxs-lookup"><span data-stu-id="7765b-329">array of enum</span></span>|<span data-ttu-id="7765b-330">3 </span><span class="sxs-lookup"><span data-stu-id="7765b-330">3</span></span>|<span data-ttu-id="7765b-331">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-331">✔</span></span>|<span data-ttu-id="7765b-332">指定命令列表有效的范围。</span><span class="sxs-lookup"><span data-stu-id="7765b-332">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="7765b-333">选项包括`team`、 `personal`和`groupchat`。</span><span class="sxs-lookup"><span data-stu-id="7765b-333">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="7765b-334">对象数组</span><span class="sxs-lookup"><span data-stu-id="7765b-334">array of objects</span></span>|<span data-ttu-id="7765b-335">10 </span><span class="sxs-lookup"><span data-stu-id="7765b-335">10</span></span>|<span data-ttu-id="7765b-336">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-336">✔</span></span>|<span data-ttu-id="7765b-337">机器人支持的命令数组：</span><span class="sxs-lookup"><span data-stu-id="7765b-337">An array of commands the bot supports:</span></span><br><span data-ttu-id="7765b-338">`title`： bot 命令名称（string，32）</span><span class="sxs-lookup"><span data-stu-id="7765b-338">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="7765b-339">`description`：命令语法及其参数的简单说明或示例（string，128）</span><span class="sxs-lookup"><span data-stu-id="7765b-339">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

## <a name="connectors"></a><span data-ttu-id="7765b-340">插槽</span><span class="sxs-lookup"><span data-stu-id="7765b-340">connectors</span></span>

<span data-ttu-id="7765b-341">**可选**</span><span class="sxs-lookup"><span data-stu-id="7765b-341">**Optional**</span></span>

<span data-ttu-id="7765b-342">`connectors` Block 定义了应用程序的 Office 365 连接器。</span><span class="sxs-lookup"><span data-stu-id="7765b-342">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="7765b-343">对象是包含所有类型`object`元素的数组（最多1个元素）。</span><span class="sxs-lookup"><span data-stu-id="7765b-343">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="7765b-344">仅对提供连接器的解决方案而言，此块是必需的。</span><span class="sxs-lookup"><span data-stu-id="7765b-344">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="7765b-345">名称</span><span class="sxs-lookup"><span data-stu-id="7765b-345">Name</span></span>| <span data-ttu-id="7765b-346">类型</span><span class="sxs-lookup"><span data-stu-id="7765b-346">Type</span></span>| <span data-ttu-id="7765b-347">最大大小</span><span class="sxs-lookup"><span data-stu-id="7765b-347">Maximum size</span></span> | <span data-ttu-id="7765b-348">必需</span><span class="sxs-lookup"><span data-stu-id="7765b-348">Required</span></span> | <span data-ttu-id="7765b-349">说明</span><span class="sxs-lookup"><span data-stu-id="7765b-349">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="7765b-350">String</span><span class="sxs-lookup"><span data-stu-id="7765b-350">String</span></span>|<span data-ttu-id="7765b-351">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-351">2048 characters</span></span>|<span data-ttu-id="7765b-352">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-352">✔</span></span>|<span data-ttu-id="7765b-353">配置连接器时要使用的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="7765b-353">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="7765b-354">String</span><span class="sxs-lookup"><span data-stu-id="7765b-354">String</span></span>|<span data-ttu-id="7765b-355">64个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-355">64 characters</span></span>|<span data-ttu-id="7765b-356">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-356">✔</span></span>|<span data-ttu-id="7765b-357">与[连接器开发人员仪表板](https://aka.ms/connectorsdashboard)中的 ID 相匹配的连接器的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="7765b-357">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="7765b-358">枚举数组</span><span class="sxs-lookup"><span data-stu-id="7765b-358">Array of enum</span></span>|<span data-ttu-id="7765b-359">1 </span><span class="sxs-lookup"><span data-stu-id="7765b-359">1</span></span>|<span data-ttu-id="7765b-360">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-360">✔</span></span>|<span data-ttu-id="7765b-361">指定连接器是在中的频道上下文中`team`，还是在仅限于单个用户的体验（`personal`）中提供体验。</span><span class="sxs-lookup"><span data-stu-id="7765b-361">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="7765b-362">目前，仅支持`team`作用域。</span><span class="sxs-lookup"><span data-stu-id="7765b-362">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="7765b-363">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="7765b-363">composeExtensions</span></span>

<span data-ttu-id="7765b-364">**可选**</span><span class="sxs-lookup"><span data-stu-id="7765b-364">**Optional**</span></span>

<span data-ttu-id="7765b-365">定义应用程序的消息扩展。</span><span class="sxs-lookup"><span data-stu-id="7765b-365">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="7765b-366">功能的名称已从11月2017的 "撰写分机" 更改为 "消息扩展"，但清单名称保持不变，以便现有扩展能够继续正常工作。</span><span class="sxs-lookup"><span data-stu-id="7765b-366">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="7765b-367">对象是包含所有类型`object`元素的数组（最多1个元素）。</span><span class="sxs-lookup"><span data-stu-id="7765b-367">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="7765b-368">仅对提供邮件扩展的解决方案而言，此块是必需的。</span><span class="sxs-lookup"><span data-stu-id="7765b-368">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="7765b-369">名称</span><span class="sxs-lookup"><span data-stu-id="7765b-369">Name</span></span>| <span data-ttu-id="7765b-370">类型</span><span class="sxs-lookup"><span data-stu-id="7765b-370">Type</span></span> | <span data-ttu-id="7765b-371">最大大小</span><span class="sxs-lookup"><span data-stu-id="7765b-371">Maximum Size</span></span> | <span data-ttu-id="7765b-372">必需</span><span class="sxs-lookup"><span data-stu-id="7765b-372">Required</span></span> | <span data-ttu-id="7765b-373">说明</span><span class="sxs-lookup"><span data-stu-id="7765b-373">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="7765b-374">String</span><span class="sxs-lookup"><span data-stu-id="7765b-374">String</span></span>|<span data-ttu-id="7765b-375">64</span><span class="sxs-lookup"><span data-stu-id="7765b-375">64</span></span>|<span data-ttu-id="7765b-376">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-376">✔</span></span>|<span data-ttu-id="7765b-377">与 Bot 框架一起注册的支持邮件扩展的 bot 的唯一 Microsoft 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="7765b-377">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="7765b-378">这可能与整体应用程序 ID 很好。</span><span class="sxs-lookup"><span data-stu-id="7765b-378">This may well be the same as the overall App ID.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="7765b-379">Boolean</span><span class="sxs-lookup"><span data-stu-id="7765b-379">Boolean</span></span>|||<span data-ttu-id="7765b-380">一个值，指示用户是否可以更新邮件扩展的配置。</span><span class="sxs-lookup"><span data-stu-id="7765b-380">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="7765b-381">默认值为`false`。</span><span class="sxs-lookup"><span data-stu-id="7765b-381">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="7765b-382">对象数组</span><span class="sxs-lookup"><span data-stu-id="7765b-382">Array of object</span></span>|<span data-ttu-id="7765b-383">10 </span><span class="sxs-lookup"><span data-stu-id="7765b-383">10</span></span>|<span data-ttu-id="7765b-384">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-384">✔</span></span>|<span data-ttu-id="7765b-385">邮件扩展支持的命令数组</span><span class="sxs-lookup"><span data-stu-id="7765b-385">Array of commands the messaging extension supports</span></span>|
|`messageHandlers`|<span data-ttu-id="7765b-386">对象数组</span><span class="sxs-lookup"><span data-stu-id="7765b-386">Array of Objects</span></span>|<span data-ttu-id="7765b-387">5 </span><span class="sxs-lookup"><span data-stu-id="7765b-387">5</span></span>||<span data-ttu-id="7765b-388">允许在满足特定条件时调用应用程序的处理程序列表。</span><span class="sxs-lookup"><span data-stu-id="7765b-388">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="7765b-389">域也必须列在`validDomains`</span><span class="sxs-lookup"><span data-stu-id="7765b-389">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="7765b-390">String</span><span class="sxs-lookup"><span data-stu-id="7765b-390">String</span></span>|||<span data-ttu-id="7765b-391">消息处理程序的类型。</span><span class="sxs-lookup"><span data-stu-id="7765b-391">The type of message handler.</span></span> <span data-ttu-id="7765b-392">必须是 `"link"`。</span><span class="sxs-lookup"><span data-stu-id="7765b-392">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="7765b-393">Array of Strings</span><span class="sxs-lookup"><span data-stu-id="7765b-393">Array of Strings</span></span>|||<span data-ttu-id="7765b-394">链接消息处理程序可以为其注册的域的数组。</span><span class="sxs-lookup"><span data-stu-id="7765b-394">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="7765b-395">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="7765b-395">composeExtensions.commands</span></span>

<span data-ttu-id="7765b-396">您的邮件扩展应声明一个或多个命令。</span><span class="sxs-lookup"><span data-stu-id="7765b-396">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="7765b-397">在 Microsoft 团队中，每个命令都显示为从基于 UI 的入口点的潜在交互。</span><span class="sxs-lookup"><span data-stu-id="7765b-397">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="7765b-398">最多可以有10个命令。</span><span class="sxs-lookup"><span data-stu-id="7765b-398">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="7765b-399">每个命令项都是一个具有以下结构的对象：</span><span class="sxs-lookup"><span data-stu-id="7765b-399">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="7765b-400">名称</span><span class="sxs-lookup"><span data-stu-id="7765b-400">Name</span></span>| <span data-ttu-id="7765b-401">类型</span><span class="sxs-lookup"><span data-stu-id="7765b-401">Type</span></span>| <span data-ttu-id="7765b-402">最大大小</span><span class="sxs-lookup"><span data-stu-id="7765b-402">Maximum size</span></span> | <span data-ttu-id="7765b-403">必需</span><span class="sxs-lookup"><span data-stu-id="7765b-403">Required</span></span> | <span data-ttu-id="7765b-404">说明</span><span class="sxs-lookup"><span data-stu-id="7765b-404">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="7765b-405">String</span><span class="sxs-lookup"><span data-stu-id="7765b-405">String</span></span>|<span data-ttu-id="7765b-406">64个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-406">64 characters</span></span>|<span data-ttu-id="7765b-407">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-407">✔</span></span>|<span data-ttu-id="7765b-408">命令的 ID</span><span class="sxs-lookup"><span data-stu-id="7765b-408">The ID for the command</span></span>|
|`type`|<span data-ttu-id="7765b-409">String</span><span class="sxs-lookup"><span data-stu-id="7765b-409">String</span></span>|<span data-ttu-id="7765b-410">64个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-410">64 characters</span></span>||<span data-ttu-id="7765b-411">命令的类型。</span><span class="sxs-lookup"><span data-stu-id="7765b-411">Type of the command.</span></span> <span data-ttu-id="7765b-412">一个`query`或`action`。</span><span class="sxs-lookup"><span data-stu-id="7765b-412">One of `query` or `action`.</span></span> <span data-ttu-id="7765b-413">设置`query`</span><span class="sxs-lookup"><span data-stu-id="7765b-413">Default: `query`</span></span>|
|`title`|<span data-ttu-id="7765b-414">String</span><span class="sxs-lookup"><span data-stu-id="7765b-414">String</span></span>|<span data-ttu-id="7765b-415">32个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-415">32 characters</span></span>|<span data-ttu-id="7765b-416">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-416">✔</span></span>|<span data-ttu-id="7765b-417">用户友好的命令名称</span><span class="sxs-lookup"><span data-stu-id="7765b-417">The user-friendly command name</span></span>|
|`description`|<span data-ttu-id="7765b-418">String</span><span class="sxs-lookup"><span data-stu-id="7765b-418">String</span></span>|<span data-ttu-id="7765b-419">128个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-419">128 characters</span></span>||<span data-ttu-id="7765b-420">对用户显示的说明，以指示此命令的用途</span><span class="sxs-lookup"><span data-stu-id="7765b-420">The description that appears to users to indicate the purpose of this command</span></span>|
|`initialRun`|<span data-ttu-id="7765b-421">Boolean</span><span class="sxs-lookup"><span data-stu-id="7765b-421">Boolean</span></span>|||<span data-ttu-id="7765b-422">一个布尔值，指示是否在最初不使用任何参数的情况之下运行该命令。</span><span class="sxs-lookup"><span data-stu-id="7765b-422">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="7765b-423">设置`false`</span><span class="sxs-lookup"><span data-stu-id="7765b-423">Default: `false`</span></span>|
|`context`|<span data-ttu-id="7765b-424">Array of Strings</span><span class="sxs-lookup"><span data-stu-id="7765b-424">Array of Strings</span></span>|<span data-ttu-id="7765b-425">3 </span><span class="sxs-lookup"><span data-stu-id="7765b-425">3</span></span>||<span data-ttu-id="7765b-426">定义可以从中调用邮件扩展的位置。</span><span class="sxs-lookup"><span data-stu-id="7765b-426">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="7765b-427">、 `commandBox`、 `message`的`compose`的任意组合。</span><span class="sxs-lookup"><span data-stu-id="7765b-427">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="7765b-428">默认值为`["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="7765b-428">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="7765b-429">Boolean</span><span class="sxs-lookup"><span data-stu-id="7765b-429">Boolean</span></span>|||<span data-ttu-id="7765b-430">一个布尔值，指示是否应动态获取任务模块</span><span class="sxs-lookup"><span data-stu-id="7765b-430">A boolean value that indicates if it should fetch the task module dynamically</span></span>|
|`taskInfo`|<span data-ttu-id="7765b-431">对象</span><span class="sxs-lookup"><span data-stu-id="7765b-431">Object</span></span>|||<span data-ttu-id="7765b-432">指定在使用消息扩展命令时要预加载的任务模块</span><span class="sxs-lookup"><span data-stu-id="7765b-432">Specify the task module to preload when using a messaging extension command</span></span>|
|`taskInfo.title`|<span data-ttu-id="7765b-433">String</span><span class="sxs-lookup"><span data-stu-id="7765b-433">String</span></span>|<span data-ttu-id="7765b-434">64</span><span class="sxs-lookup"><span data-stu-id="7765b-434">64</span></span>||<span data-ttu-id="7765b-435">初始对话框标题</span><span class="sxs-lookup"><span data-stu-id="7765b-435">Initial dialog title</span></span>|
|`taskInfo.width`|<span data-ttu-id="7765b-436">String</span><span class="sxs-lookup"><span data-stu-id="7765b-436">String</span></span>|||<span data-ttu-id="7765b-437">对话框宽度-以像素为单位的数字或默认布局，如 "大"、"中" 或 "small"</span><span class="sxs-lookup"><span data-stu-id="7765b-437">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.height`|<span data-ttu-id="7765b-438">String</span><span class="sxs-lookup"><span data-stu-id="7765b-438">String</span></span>|||<span data-ttu-id="7765b-439">对话框高度-以像素为单位的数字或默认布局，如 "大"、"中" 或 "small"</span><span class="sxs-lookup"><span data-stu-id="7765b-439">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.url`|<span data-ttu-id="7765b-440">String</span><span class="sxs-lookup"><span data-stu-id="7765b-440">String</span></span>|||<span data-ttu-id="7765b-441">初始 web 视图 URL</span><span class="sxs-lookup"><span data-stu-id="7765b-441">Initial webview URL</span></span>|
|`parameters`|<span data-ttu-id="7765b-442">对象数组</span><span class="sxs-lookup"><span data-stu-id="7765b-442">Array of object</span></span>|<span data-ttu-id="7765b-443">5 </span><span class="sxs-lookup"><span data-stu-id="7765b-443">5</span></span>|<span data-ttu-id="7765b-444">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-444">✔</span></span>|<span data-ttu-id="7765b-445">命令所采用的参数的列表。</span><span class="sxs-lookup"><span data-stu-id="7765b-445">The list of parameters the command takes.</span></span> <span data-ttu-id="7765b-446">最小值： 1;最大值：5</span><span class="sxs-lookup"><span data-stu-id="7765b-446">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="7765b-447">String</span><span class="sxs-lookup"><span data-stu-id="7765b-447">String</span></span>|<span data-ttu-id="7765b-448">64个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-448">64 characters</span></span>|<span data-ttu-id="7765b-449">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-449">✔</span></span>|<span data-ttu-id="7765b-450">在客户端中显示的参数的名称。</span><span class="sxs-lookup"><span data-stu-id="7765b-450">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="7765b-451">此项包含在用户请求中。</span><span class="sxs-lookup"><span data-stu-id="7765b-451">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="7765b-452">String</span><span class="sxs-lookup"><span data-stu-id="7765b-452">String</span></span>|<span data-ttu-id="7765b-453">32个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-453">32 characters</span></span>|<span data-ttu-id="7765b-454">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-454">✔</span></span>|<span data-ttu-id="7765b-455">参数的用户友好标题。</span><span class="sxs-lookup"><span data-stu-id="7765b-455">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="7765b-456">String</span><span class="sxs-lookup"><span data-stu-id="7765b-456">String</span></span>|<span data-ttu-id="7765b-457">128个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-457">128 characters</span></span>||<span data-ttu-id="7765b-458">描述此参数用途的用户友好字符串。</span><span class="sxs-lookup"><span data-stu-id="7765b-458">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="7765b-459">String</span><span class="sxs-lookup"><span data-stu-id="7765b-459">String</span></span>|<span data-ttu-id="7765b-460">128个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-460">128 characters</span></span>||<span data-ttu-id="7765b-461">定义在的任务模块上显示的控件的类型`fetchTask: true`。</span><span class="sxs-lookup"><span data-stu-id="7765b-461">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="7765b-462">一个`text` `textarea`、 `number` `date`、、、、 `time` `toggle``choiceset`</span><span class="sxs-lookup"><span data-stu-id="7765b-462">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`</span></span>|
|`parameter.choices`|<span data-ttu-id="7765b-463">对象数组</span><span class="sxs-lookup"><span data-stu-id="7765b-463">Array of Objects</span></span>|<span data-ttu-id="7765b-464">10 </span><span class="sxs-lookup"><span data-stu-id="7765b-464">10</span></span>||<span data-ttu-id="7765b-465">的选项选项`choiceset`。</span><span class="sxs-lookup"><span data-stu-id="7765b-465">The choice options for the `choiceset`.</span></span> <span data-ttu-id="7765b-466">仅在何时`parameter.inputType`使用`choiceset`</span><span class="sxs-lookup"><span data-stu-id="7765b-466">Use only when `parameter.inputType` is `choiceset`</span></span>|
|`parameter.choices.title`|<span data-ttu-id="7765b-467">String</span><span class="sxs-lookup"><span data-stu-id="7765b-467">String</span></span>|<span data-ttu-id="7765b-468">128</span><span class="sxs-lookup"><span data-stu-id="7765b-468">128</span></span>||<span data-ttu-id="7765b-469">选项的标题</span><span class="sxs-lookup"><span data-stu-id="7765b-469">Title of the choice</span></span>|
|`parameter.choices.value`|<span data-ttu-id="7765b-470">String</span><span class="sxs-lookup"><span data-stu-id="7765b-470">String</span></span>|<span data-ttu-id="7765b-471">512</span><span class="sxs-lookup"><span data-stu-id="7765b-471">512</span></span>||<span data-ttu-id="7765b-472">选项的值</span><span class="sxs-lookup"><span data-stu-id="7765b-472">Value of the choice</span></span>|

## <a name="permissions"></a><span data-ttu-id="7765b-473">permissions</span><span class="sxs-lookup"><span data-stu-id="7765b-473">permissions</span></span>

<span data-ttu-id="7765b-474">**可选**</span><span class="sxs-lookup"><span data-stu-id="7765b-474">**Optional**</span></span>

<span data-ttu-id="7765b-475">一个数组， `string`它指定应用程序请求的权限，这样最终用户就可以知道扩展将如何执行。</span><span class="sxs-lookup"><span data-stu-id="7765b-475">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="7765b-476">以下选项是非独占的：</span><span class="sxs-lookup"><span data-stu-id="7765b-476">The following options are non-exclusive:</span></span>

* <span data-ttu-id="7765b-477">`identity`&emsp;需要用户标识信息</span><span class="sxs-lookup"><span data-stu-id="7765b-477">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="7765b-478">`messageTeamMembers`&emsp;需要向团队成员发送直接消息的权限</span><span class="sxs-lookup"><span data-stu-id="7765b-478">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="7765b-479">在更新应用程序时更改这些权限将导致用户在首次运行更新的应用程序时重复同意过程。</span><span class="sxs-lookup"><span data-stu-id="7765b-479">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="7765b-480">有关详细信息，请参阅[更新应用](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7765b-480">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="7765b-481">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="7765b-481">devicePermissions</span></span>

<span data-ttu-id="7765b-482">**可选**字符串数组</span><span class="sxs-lookup"><span data-stu-id="7765b-482">**Optional** Array of Strings</span></span>

<span data-ttu-id="7765b-483">在用户的设备上指定您的应用程序可能会请求访问的本机功能。</span><span class="sxs-lookup"><span data-stu-id="7765b-483">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="7765b-484">选项包括：</span><span class="sxs-lookup"><span data-stu-id="7765b-484">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="7765b-485">validDomains</span><span class="sxs-lookup"><span data-stu-id="7765b-485">validDomains</span></span>

<span data-ttu-id="7765b-486">**可选**，但**所需**的除外</span><span class="sxs-lookup"><span data-stu-id="7765b-486">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="7765b-487">应用程序希望在团队客户端中加载的网站的有效域列表。</span><span class="sxs-lookup"><span data-stu-id="7765b-487">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="7765b-488">例如`*.example.com`，域列表可以包含通配符。</span><span class="sxs-lookup"><span data-stu-id="7765b-488">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="7765b-489">这与域的一段完全匹配;如果需要匹配`a.b.example.com` ，请使用`*.*.example.com`。</span><span class="sxs-lookup"><span data-stu-id="7765b-489">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="7765b-490">如果您的选项卡配置或内容 UI 需要导航到其他任何域，除了用于选项卡配置之外，则必须在此处指定该域。</span><span class="sxs-lookup"><span data-stu-id="7765b-490">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="7765b-491">但是，**不**需要在您的应用程序中包含要支持的标识提供程序的域。</span><span class="sxs-lookup"><span data-stu-id="7765b-491">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="7765b-492">例如，若要使用 Google ID 进行身份验证，需要重定向到 accounts.google.com，但不应在中`validDomains[]`包含 accounts.google.com。</span><span class="sxs-lookup"><span data-stu-id="7765b-492">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="7765b-493">需要其自己的 sharepoint Url 的团队应用程序能够正常工作，可能会在其有效的域列表中包含 "{teamsitedomain}"。</span><span class="sxs-lookup"><span data-stu-id="7765b-493">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7765b-494">不要直接或通过通配符添加位于控件外部的域。</span><span class="sxs-lookup"><span data-stu-id="7765b-494">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="7765b-495">例如， `yourapp.onmicrosoft.com`是有效的，但`*.onmicrosoft.com`无效。</span><span class="sxs-lookup"><span data-stu-id="7765b-495">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="7765b-496">对象是一个包含所有类型`string`的元素的数组。</span><span class="sxs-lookup"><span data-stu-id="7765b-496">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="7765b-497">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="7765b-497">webApplicationInfo</span></span>

<span data-ttu-id="7765b-498">**可选**</span><span class="sxs-lookup"><span data-stu-id="7765b-498">**Optional**</span></span>

<span data-ttu-id="7765b-499">指定 AAD 应用 ID 和 Graph 信息，以帮助用户无缝登录 AAD 应用。</span><span class="sxs-lookup"><span data-stu-id="7765b-499">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="7765b-500">名称</span><span class="sxs-lookup"><span data-stu-id="7765b-500">Name</span></span>| <span data-ttu-id="7765b-501">类型</span><span class="sxs-lookup"><span data-stu-id="7765b-501">Type</span></span>| <span data-ttu-id="7765b-502">最大大小</span><span class="sxs-lookup"><span data-stu-id="7765b-502">Maximum size</span></span> | <span data-ttu-id="7765b-503">必需</span><span class="sxs-lookup"><span data-stu-id="7765b-503">Required</span></span> | <span data-ttu-id="7765b-504">说明</span><span class="sxs-lookup"><span data-stu-id="7765b-504">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="7765b-505">String</span><span class="sxs-lookup"><span data-stu-id="7765b-505">String</span></span>|<span data-ttu-id="7765b-506">36个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-506">36 characters</span></span>|<span data-ttu-id="7765b-507">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-507">✔</span></span>|<span data-ttu-id="7765b-508">应用程序的 AAD 应用程序 id。</span><span class="sxs-lookup"><span data-stu-id="7765b-508">AAD application id of the app.</span></span> <span data-ttu-id="7765b-509">此 id 必须为 GUID。</span><span class="sxs-lookup"><span data-stu-id="7765b-509">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="7765b-510">String</span><span class="sxs-lookup"><span data-stu-id="7765b-510">String</span></span>|<span data-ttu-id="7765b-511">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="7765b-511">2048 characters</span></span>|<span data-ttu-id="7765b-512">✔</span><span class="sxs-lookup"><span data-stu-id="7765b-512">✔</span></span>|<span data-ttu-id="7765b-513">用于获取 SSO 的身份验证令牌的应用程序的资源 url。</span><span class="sxs-lookup"><span data-stu-id="7765b-513">Resource url of app for acquiring auth token for SSO.</span></span>|
