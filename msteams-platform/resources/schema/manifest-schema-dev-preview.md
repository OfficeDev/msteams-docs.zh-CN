---
title: 开发人员预览版清单架构参考
description: 介绍 Microsoft 团队清单支持的架构
keywords: 团队清单架构开发人员预览
ms.date: 05/20/2019
ms.openlocfilehash: b99e1ae99b7fd1edd4c695f43f3ac25270f0c710
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673018"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="b1912-104">Microsoft 团队的开发人员预览版清单架构</span><span class="sxs-lookup"><span data-stu-id="b1912-104">Developer preview manifest schema for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="b1912-105">有关程序的信息和加入方式的信息，请参阅[开发人员预览](~/resources/dev-preview/developer-preview-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="b1912-105">See [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for information on the program and how you can join.</span></span>
> <span data-ttu-id="b1912-106">如果不使用开发人员预览，则不应使用此版本的清单。</span><span class="sxs-lookup"><span data-stu-id="b1912-106">If you are not using the developer preview you should not be using this version of the manifest.</span></span> <span data-ttu-id="b1912-107">有关清单的公开版本，请参阅[参考： Microsoft 团队的清单架构](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="b1912-107">See [Reference: Manifest schema for Microsoft Teams](~/resources/schema/manifest-schema.md) for the public version of the manifest.</span></span>

<span data-ttu-id="b1912-108">Microsoft 团队清单介绍了应用程序如何集成到 Microsoft 团队产品中。</span><span class="sxs-lookup"><span data-stu-id="b1912-108">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="b1912-109">您的清单必须符合托管的架构[`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json)。</span><span class="sxs-lookup"><span data-stu-id="b1912-109">Your manifest must conform to the schema hosted at [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span></span>

<span data-ttu-id="b1912-110">有关可用功能的详细信息，请参阅： [Microsoft 团队的公共开发人员预览版中的功能](~/resources/dev-preview/developer-preview-features.md)。</span><span class="sxs-lookup"><span data-stu-id="b1912-110">For more information on the features available see: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="b1912-111">完整清单示例</span><span class="sxs-lookup"><span data-stu-id="b1912-111">Sample full manifest</span></span>

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
  ]
}
```

<span data-ttu-id="b1912-112">架构定义了以下属性：</span><span class="sxs-lookup"><span data-stu-id="b1912-112">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="b1912-113">$schema</span><span class="sxs-lookup"><span data-stu-id="b1912-113">$schema</span></span>

<span data-ttu-id="b1912-114">*可选，但建议* &ndash;的字符串</span><span class="sxs-lookup"><span data-stu-id="b1912-114">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="b1912-115">引用清单的 JSON 架构的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="b1912-115">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="b1912-116">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="b1912-116">manifestVersion</span></span>

<span data-ttu-id="b1912-117">**必需** &ndash;的字符串</span><span class="sxs-lookup"><span data-stu-id="b1912-117">**Required** &ndash; String</span></span>

<span data-ttu-id="b1912-118">此清单使用的清单架构的版本。</span><span class="sxs-lookup"><span data-stu-id="b1912-118">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="b1912-119">应为 "devPreview"。</span><span class="sxs-lookup"><span data-stu-id="b1912-119">It should be "devPreview".</span></span>

## <a name="version"></a><span data-ttu-id="b1912-120">version</span><span class="sxs-lookup"><span data-stu-id="b1912-120">version</span></span>

<span data-ttu-id="b1912-121">**必需** &ndash;的字符串</span><span class="sxs-lookup"><span data-stu-id="b1912-121">**Required** &ndash; String</span></span>

<span data-ttu-id="b1912-122">特定应用程序的版本。</span><span class="sxs-lookup"><span data-stu-id="b1912-122">The version of the specific app.</span></span> <span data-ttu-id="b1912-123">如果您更新清单中的某些内容，该版本还必须递增。</span><span class="sxs-lookup"><span data-stu-id="b1912-123">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="b1912-124">这样一来，在安装新的清单时，它将覆盖现有的版本，用户将获得新的功能。</span><span class="sxs-lookup"><span data-stu-id="b1912-124">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="b1912-125">如果此应用程序已提交到应用商店，则必须重新提交新清单，然后再对其进行重新验证。</span><span class="sxs-lookup"><span data-stu-id="b1912-125">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="b1912-126">然后，此应用程序的用户将在几小时内自动获取新更新的清单（在批准后）。</span><span class="sxs-lookup"><span data-stu-id="b1912-126">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="b1912-127">如果应用程序要求更改权限，则系统将提示用户升级并重新同意该应用。</span><span class="sxs-lookup"><span data-stu-id="b1912-127">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="b1912-128">此版本字符串必须遵循[semver](http://semver.org/) STANDARD （主要。网格.修补程序）。</span><span class="sxs-lookup"><span data-stu-id="b1912-128">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="b1912-129">id</span><span class="sxs-lookup"><span data-stu-id="b1912-129">id</span></span>

<span data-ttu-id="b1912-130">**必需** &ndash;的 Microsoft 应用程序 ID</span><span class="sxs-lookup"><span data-stu-id="b1912-130">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="b1912-131">Microsoft 为此应用程序生成的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="b1912-131">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="b1912-132">如果你已通过 Microsoft Bot 框架注册了 bot，或者你的选项卡的 web 应用已使用 Microsoft 登录，则你应该已经有 ID，应在此处输入它。</span><span class="sxs-lookup"><span data-stu-id="b1912-132">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="b1912-133">否则，应在 Microsoft 应用注册门户（[我的应用程序](https://apps.dev.microsoft.com)）上生成一个新的 ID，在此处输入它，然后在[添加机器人](~/bots/how-to/create-a-bot-for-teams.md)时重用它。</span><span class="sxs-lookup"><span data-stu-id="b1912-133">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you [add a bot](~/bots/how-to/create-a-bot-for-teams.md).</span></span>

## <a name="packagename"></a><span data-ttu-id="b1912-134">packageName</span><span class="sxs-lookup"><span data-stu-id="b1912-134">packageName</span></span>

<span data-ttu-id="b1912-135">**必需** &ndash;的字符串</span><span class="sxs-lookup"><span data-stu-id="b1912-135">**Required** &ndash; String</span></span>

<span data-ttu-id="b1912-136">此应用的以反向域表示法表示的唯一标识符;例如，.com. myapp。</span><span class="sxs-lookup"><span data-stu-id="b1912-136">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="b1912-137">developer</span><span class="sxs-lookup"><span data-stu-id="b1912-137">developer</span></span>

<span data-ttu-id="b1912-138">**Required**</span><span class="sxs-lookup"><span data-stu-id="b1912-138">**Required**</span></span>

<span data-ttu-id="b1912-139">指定有关贵公司的信息。</span><span class="sxs-lookup"><span data-stu-id="b1912-139">Specifies information about your company.</span></span> <span data-ttu-id="b1912-140">对于提交到 AppSource （以前称为 "Office 应用商店"）的应用程序，这些值必须与您的 AppSource 条目中的信息相匹配。</span><span class="sxs-lookup"><span data-stu-id="b1912-140">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span>

|<span data-ttu-id="b1912-141">姓名</span><span class="sxs-lookup"><span data-stu-id="b1912-141">Name</span></span>| <span data-ttu-id="b1912-142">最大大小</span><span class="sxs-lookup"><span data-stu-id="b1912-142">Maximum size</span></span> | <span data-ttu-id="b1912-143">必需</span><span class="sxs-lookup"><span data-stu-id="b1912-143">Required</span></span> | <span data-ttu-id="b1912-144">说明</span><span class="sxs-lookup"><span data-stu-id="b1912-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="b1912-145">32个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-145">32 characters</span></span>|<span data-ttu-id="b1912-146">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-146">✔</span></span>|<span data-ttu-id="b1912-147">开发人员的显示名称。</span><span class="sxs-lookup"><span data-stu-id="b1912-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="b1912-148">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-148">2048 characters</span></span>|<span data-ttu-id="b1912-149">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-149">✔</span></span>|<span data-ttu-id="b1912-150">开发人员网站的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="b1912-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="b1912-151">此链接应将用户带到您的公司或特定于产品的登陆页面。</span><span class="sxs-lookup"><span data-stu-id="b1912-151">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="b1912-152">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-152">2048 characters</span></span>|<span data-ttu-id="b1912-153">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-153">✔</span></span>|<span data-ttu-id="b1912-154">开发人员的隐私策略的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="b1912-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="b1912-155">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-155">2048 characters</span></span>|<span data-ttu-id="b1912-156">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-156">✔</span></span>|<span data-ttu-id="b1912-157">开发人员使用条款的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="b1912-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="b1912-158">10个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-158">10 characters</span></span>|<span data-ttu-id="b1912-159">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-159">✔</span></span>|<span data-ttu-id="b1912-160">**可选**用于标识合作伙伴组织构建应用程序的 Microsoft 合作伙伴网络 ID。</span><span class="sxs-lookup"><span data-stu-id="b1912-160">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="b1912-161">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="b1912-161">localizationInfo</span></span>

<span data-ttu-id="b1912-162">**可选**</span><span class="sxs-lookup"><span data-stu-id="b1912-162">**Optional**</span></span>

<span data-ttu-id="b1912-163">允许指定默认语言，以及指向其他语言文件的指针。</span><span class="sxs-lookup"><span data-stu-id="b1912-163">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="b1912-164">请参阅[本地化](~/concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="b1912-164">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="b1912-165">姓名</span><span class="sxs-lookup"><span data-stu-id="b1912-165">Name</span></span>| <span data-ttu-id="b1912-166">最大大小</span><span class="sxs-lookup"><span data-stu-id="b1912-166">Maximum size</span></span> | <span data-ttu-id="b1912-167">必需</span><span class="sxs-lookup"><span data-stu-id="b1912-167">Required</span></span> | <span data-ttu-id="b1912-168">说明</span><span class="sxs-lookup"><span data-stu-id="b1912-168">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`|<span data-ttu-id="b1912-169">4个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-169">4 characters</span></span>|<span data-ttu-id="b1912-170">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-170">✔</span></span>|<span data-ttu-id="b1912-171">此顶级清单文件中的字符串的语言标记。</span><span class="sxs-lookup"><span data-stu-id="b1912-171">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="b1912-172">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="b1912-172">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="b1912-173">指定其他语言翻译的对象的数组。</span><span class="sxs-lookup"><span data-stu-id="b1912-173">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="b1912-174">姓名</span><span class="sxs-lookup"><span data-stu-id="b1912-174">Name</span></span>| <span data-ttu-id="b1912-175">最大大小</span><span class="sxs-lookup"><span data-stu-id="b1912-175">Maximum size</span></span> | <span data-ttu-id="b1912-176">必需</span><span class="sxs-lookup"><span data-stu-id="b1912-176">Required</span></span> | <span data-ttu-id="b1912-177">说明</span><span class="sxs-lookup"><span data-stu-id="b1912-177">Description</span></span>|
|---|---|---|---|
|`languageTag`|<span data-ttu-id="b1912-178">4个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-178">4 characters</span></span>|<span data-ttu-id="b1912-179">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-179">✔</span></span>|<span data-ttu-id="b1912-180">所提供文件中的字符串的语言标记。</span><span class="sxs-lookup"><span data-stu-id="b1912-180">The language tag of the strings in the provided file.</span></span>|
|`file`|<span data-ttu-id="b1912-181">4个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-181">4 characters</span></span>|<span data-ttu-id="b1912-182">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-182">✔</span></span>|<span data-ttu-id="b1912-183">包含翻译字符串的 json 文件的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="b1912-183">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="b1912-184">name</span><span class="sxs-lookup"><span data-stu-id="b1912-184">name</span></span>

<span data-ttu-id="b1912-185">**Required**</span><span class="sxs-lookup"><span data-stu-id="b1912-185">**Required**</span></span>

<span data-ttu-id="b1912-186">在团队体验中向用户显示的应用程序体验的名称。</span><span class="sxs-lookup"><span data-stu-id="b1912-186">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="b1912-187">对于提交到 AppSource 的应用程序，这些值必须与您的 AppSource 条目中的信息相匹配。</span><span class="sxs-lookup"><span data-stu-id="b1912-187">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="b1912-188">`short`和`full`的值不应相同。</span><span class="sxs-lookup"><span data-stu-id="b1912-188">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="b1912-189">姓名</span><span class="sxs-lookup"><span data-stu-id="b1912-189">Name</span></span>| <span data-ttu-id="b1912-190">最大大小</span><span class="sxs-lookup"><span data-stu-id="b1912-190">Maximum size</span></span> | <span data-ttu-id="b1912-191">必需</span><span class="sxs-lookup"><span data-stu-id="b1912-191">Required</span></span> | <span data-ttu-id="b1912-192">说明</span><span class="sxs-lookup"><span data-stu-id="b1912-192">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="b1912-193">30 个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-193">30 characters</span></span>|<span data-ttu-id="b1912-194">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-194">✔</span></span>|<span data-ttu-id="b1912-195">应用程序的短显示名称。</span><span class="sxs-lookup"><span data-stu-id="b1912-195">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="b1912-196">100 个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-196">100 characters</span></span>||<span data-ttu-id="b1912-197">应用程序的全名，如果完整的应用程序名称超过30个字符，则使用该名称。</span><span class="sxs-lookup"><span data-stu-id="b1912-197">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="b1912-198">说明</span><span class="sxs-lookup"><span data-stu-id="b1912-198">description</span></span>

<span data-ttu-id="b1912-199">**Required**</span><span class="sxs-lookup"><span data-stu-id="b1912-199">**Required**</span></span>

<span data-ttu-id="b1912-200">向用户介绍你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="b1912-200">Describes your app to users.</span></span> <span data-ttu-id="b1912-201">对于提交到 AppSource 的应用程序，这些值必须与您的 AppSource 条目中的信息相匹配。</span><span class="sxs-lookup"><span data-stu-id="b1912-201">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="b1912-202">确保你的说明准确描述你的体验，并提供信息，以帮助潜在客户了解你的体验。</span><span class="sxs-lookup"><span data-stu-id="b1912-202">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="b1912-203">如果需要使用外部帐户，还应在完整说明中说明。</span><span class="sxs-lookup"><span data-stu-id="b1912-203">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="b1912-204">`short`和`full`的值不应相同。</span><span class="sxs-lookup"><span data-stu-id="b1912-204">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="b1912-205">您的简短说明不得在详细说明中重复，并且不得包含任何其他应用程序名称。</span><span class="sxs-lookup"><span data-stu-id="b1912-205">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="b1912-206">姓名</span><span class="sxs-lookup"><span data-stu-id="b1912-206">Name</span></span>| <span data-ttu-id="b1912-207">最大大小</span><span class="sxs-lookup"><span data-stu-id="b1912-207">Maximum size</span></span> | <span data-ttu-id="b1912-208">必需</span><span class="sxs-lookup"><span data-stu-id="b1912-208">Required</span></span> | <span data-ttu-id="b1912-209">说明</span><span class="sxs-lookup"><span data-stu-id="b1912-209">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="b1912-210">80个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-210">80 characters</span></span>|<span data-ttu-id="b1912-211">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-211">✔</span></span>|<span data-ttu-id="b1912-212">在空间有限时使用的应用程序体验的简短说明。</span><span class="sxs-lookup"><span data-stu-id="b1912-212">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="b1912-213">4000个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-213">4000 characters</span></span>|<span data-ttu-id="b1912-214">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-214">✔</span></span>|<span data-ttu-id="b1912-215">您的应用程序的完整说明。</span><span class="sxs-lookup"><span data-stu-id="b1912-215">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="b1912-216">图标</span><span class="sxs-lookup"><span data-stu-id="b1912-216">icons</span></span>

<span data-ttu-id="b1912-217">**Required**</span><span class="sxs-lookup"><span data-stu-id="b1912-217">**Required**</span></span>

<span data-ttu-id="b1912-218">在团队应用程序中使用的图标。</span><span class="sxs-lookup"><span data-stu-id="b1912-218">Icons used within the Teams app.</span></span> <span data-ttu-id="b1912-219">图标文件必须作为上载包的一部分包括在内。</span><span class="sxs-lookup"><span data-stu-id="b1912-219">The icon files must be included as part of the upload package.</span></span>

|<span data-ttu-id="b1912-220">姓名</span><span class="sxs-lookup"><span data-stu-id="b1912-220">Name</span></span>| <span data-ttu-id="b1912-221">最大大小</span><span class="sxs-lookup"><span data-stu-id="b1912-221">Maximum size</span></span> | <span data-ttu-id="b1912-222">必需</span><span class="sxs-lookup"><span data-stu-id="b1912-222">Required</span></span> | <span data-ttu-id="b1912-223">说明</span><span class="sxs-lookup"><span data-stu-id="b1912-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="b1912-224">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-224">2048 characters</span></span>|<span data-ttu-id="b1912-225">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-225">✔</span></span>|<span data-ttu-id="b1912-226">指向透明 32x32 PNG 边框图标的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="b1912-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="b1912-227">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-227">2048 characters</span></span>|<span data-ttu-id="b1912-228">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-228">✔</span></span>|<span data-ttu-id="b1912-229">完整颜色 192x192 PNG 图标的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="b1912-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="b1912-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="b1912-230">accentColor</span></span>

<span data-ttu-id="b1912-231">**必需** &ndash;的字符串</span><span class="sxs-lookup"><span data-stu-id="b1912-231">**Required** &ndash; String</span></span>

<span data-ttu-id="b1912-232">与大纲图标的背景一起使用的颜色。</span><span class="sxs-lookup"><span data-stu-id="b1912-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="b1912-233">值必须是以 "#" 开头的有效 HTML 颜色代码，例如`#4464ee`。</span><span class="sxs-lookup"><span data-stu-id="b1912-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="b1912-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="b1912-234">configurableTabs</span></span>

<span data-ttu-id="b1912-235">**可选**</span><span class="sxs-lookup"><span data-stu-id="b1912-235">**Optional**</span></span>

<span data-ttu-id="b1912-236">当您的应用程序体验具有在添加之前需要额外配置的团队频道选项卡体验时使用。</span><span class="sxs-lookup"><span data-stu-id="b1912-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="b1912-237">仅在团队作用域中支持可配置的选项卡，并且每个应用程序目前仅支持一个选项卡。</span><span class="sxs-lookup"><span data-stu-id="b1912-237">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="b1912-238">对象是一个包含所有类型`object`的元素的数组。</span><span class="sxs-lookup"><span data-stu-id="b1912-238">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="b1912-239">仅在提供可配置的通道选项卡解决方案的解决方案中，此块才是必需的。</span><span class="sxs-lookup"><span data-stu-id="b1912-239">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="b1912-240">名称</span><span class="sxs-lookup"><span data-stu-id="b1912-240">Name</span></span>| <span data-ttu-id="b1912-241">类型</span><span class="sxs-lookup"><span data-stu-id="b1912-241">Type</span></span>| <span data-ttu-id="b1912-242">最大大小</span><span class="sxs-lookup"><span data-stu-id="b1912-242">Maximum size</span></span> | <span data-ttu-id="b1912-243">必需</span><span class="sxs-lookup"><span data-stu-id="b1912-243">Required</span></span> | <span data-ttu-id="b1912-244">说明</span><span class="sxs-lookup"><span data-stu-id="b1912-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="b1912-245">String</span><span class="sxs-lookup"><span data-stu-id="b1912-245">String</span></span>|<span data-ttu-id="b1912-246">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-246">2048 characters</span></span>|<span data-ttu-id="b1912-247">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-247">✔</span></span>|<span data-ttu-id="b1912-248">配置选项卡时要使用的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="b1912-248">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="b1912-249">Boolean</span><span class="sxs-lookup"><span data-stu-id="b1912-249">Boolean</span></span>|||<span data-ttu-id="b1912-250">一个值，指示是否可在用户创建之后更新该选项卡的配置实例。</span><span class="sxs-lookup"><span data-stu-id="b1912-250">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="b1912-251">设置`true`</span><span class="sxs-lookup"><span data-stu-id="b1912-251">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="b1912-252">枚举数组</span><span class="sxs-lookup"><span data-stu-id="b1912-252">Array of enum</span></span>|<span data-ttu-id="b1912-253">1 </span><span class="sxs-lookup"><span data-stu-id="b1912-253">1</span></span>|<span data-ttu-id="b1912-254">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-254">✔</span></span>|<span data-ttu-id="b1912-255">目前，可配置的`team`选项卡仅`groupchat`支持和范围。</span><span class="sxs-lookup"><span data-stu-id="b1912-255">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="b1912-256">String</span><span class="sxs-lookup"><span data-stu-id="b1912-256">String</span></span>|<span data-ttu-id="b1912-257">2048</span><span class="sxs-lookup"><span data-stu-id="b1912-257">2048</span></span>||<span data-ttu-id="b1912-258">要在 SharePoint 中使用的选项卡预览图像的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="b1912-258">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="b1912-259">字号（1024x768）。</span><span class="sxs-lookup"><span data-stu-id="b1912-259">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="b1912-260">枚举数组</span><span class="sxs-lookup"><span data-stu-id="b1912-260">Array of enum</span></span>|<span data-ttu-id="b1912-261">1 </span><span class="sxs-lookup"><span data-stu-id="b1912-261">1</span></span>||<span data-ttu-id="b1912-262">定义您的选项卡在 SharePoint 中的可用方式。</span><span class="sxs-lookup"><span data-stu-id="b1912-262">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="b1912-263">选项包括`sharePointFullPage`和`sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="b1912-263">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="b1912-264">staticTabs</span><span class="sxs-lookup"><span data-stu-id="b1912-264">staticTabs</span></span>

<span data-ttu-id="b1912-265">**可选**</span><span class="sxs-lookup"><span data-stu-id="b1912-265">**Optional**</span></span>

<span data-ttu-id="b1912-266">定义一组可在默认情况下 "固定" 的选项卡，而无需用户手动添加它们。</span><span class="sxs-lookup"><span data-stu-id="b1912-266">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="b1912-267">在范围内声明`personal`的静态制表符始终固定到应用的个人体验中。</span><span class="sxs-lookup"><span data-stu-id="b1912-267">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="b1912-268">当前不支持在`team`范围中声明的静态选项卡。</span><span class="sxs-lookup"><span data-stu-id="b1912-268">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="b1912-269">对象是包含类型`object`的所有元素的数组（最多16个元素）。</span><span class="sxs-lookup"><span data-stu-id="b1912-269">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="b1912-270">仅在提供静态选项卡解决方案的解决方案中，此块是必需的。</span><span class="sxs-lookup"><span data-stu-id="b1912-270">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="b1912-271">名称</span><span class="sxs-lookup"><span data-stu-id="b1912-271">Name</span></span>| <span data-ttu-id="b1912-272">类型</span><span class="sxs-lookup"><span data-stu-id="b1912-272">Type</span></span>| <span data-ttu-id="b1912-273">最大大小</span><span class="sxs-lookup"><span data-stu-id="b1912-273">Maximum size</span></span> | <span data-ttu-id="b1912-274">必需</span><span class="sxs-lookup"><span data-stu-id="b1912-274">Required</span></span> | <span data-ttu-id="b1912-275">说明</span><span class="sxs-lookup"><span data-stu-id="b1912-275">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="b1912-276">String</span><span class="sxs-lookup"><span data-stu-id="b1912-276">String</span></span>|<span data-ttu-id="b1912-277">64个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-277">64 characters</span></span>|<span data-ttu-id="b1912-278">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-278">✔</span></span>|<span data-ttu-id="b1912-279">选项卡显示的实体的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="b1912-279">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="b1912-280">String</span><span class="sxs-lookup"><span data-stu-id="b1912-280">String</span></span>|<span data-ttu-id="b1912-281">128个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-281">128 characters</span></span>|<span data-ttu-id="b1912-282">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-282">✔</span></span>|<span data-ttu-id="b1912-283">该选项卡在通道接口中的显示名称。</span><span class="sxs-lookup"><span data-stu-id="b1912-283">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="b1912-284">String</span><span class="sxs-lookup"><span data-stu-id="b1912-284">String</span></span>|<span data-ttu-id="b1912-285">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-285">2048 characters</span></span>|<span data-ttu-id="b1912-286">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-286">✔</span></span>|<span data-ttu-id="b1912-287">指向要在团队画布中显示的实体 UI 的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="b1912-287">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="b1912-288">String</span><span class="sxs-lookup"><span data-stu-id="b1912-288">String</span></span>|<span data-ttu-id="b1912-289">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-289">2048 characters</span></span>||<span data-ttu-id="b1912-290">要指向的 https://URL，如果用户要在浏览器中查看。</span><span class="sxs-lookup"><span data-stu-id="b1912-290">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="b1912-291">枚举数组</span><span class="sxs-lookup"><span data-stu-id="b1912-291">Array of enum</span></span>|<span data-ttu-id="b1912-292">1 </span><span class="sxs-lookup"><span data-stu-id="b1912-292">1</span></span>|<span data-ttu-id="b1912-293">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-293">✔</span></span>|<span data-ttu-id="b1912-294">目前，静态选项卡仅支持`personal`作用域，这意味着它只能作为个人体验的一部分进行预配。</span><span class="sxs-lookup"><span data-stu-id="b1912-294">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="b1912-295">bot</span><span class="sxs-lookup"><span data-stu-id="b1912-295">bots</span></span>

<span data-ttu-id="b1912-296">**可选**</span><span class="sxs-lookup"><span data-stu-id="b1912-296">**Optional**</span></span>

<span data-ttu-id="b1912-297">定义机器人解决方案以及可选信息，如默认的命令属性。</span><span class="sxs-lookup"><span data-stu-id="b1912-297">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="b1912-298">该对象是数组（每个应用程序最多&mdash;只能有一个一个 bot 仅允许一个 bot）和所有类型`object`的元素。</span><span class="sxs-lookup"><span data-stu-id="b1912-298">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="b1912-299">仅在提供机器人体验的解决方案中，此块才是必需的。</span><span class="sxs-lookup"><span data-stu-id="b1912-299">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="b1912-300">名称</span><span class="sxs-lookup"><span data-stu-id="b1912-300">Name</span></span>| <span data-ttu-id="b1912-301">类型</span><span class="sxs-lookup"><span data-stu-id="b1912-301">Type</span></span>| <span data-ttu-id="b1912-302">最大大小</span><span class="sxs-lookup"><span data-stu-id="b1912-302">Maximum size</span></span> | <span data-ttu-id="b1912-303">必需</span><span class="sxs-lookup"><span data-stu-id="b1912-303">Required</span></span> | <span data-ttu-id="b1912-304">说明</span><span class="sxs-lookup"><span data-stu-id="b1912-304">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="b1912-305">String</span><span class="sxs-lookup"><span data-stu-id="b1912-305">String</span></span>|<span data-ttu-id="b1912-306">64个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-306">64 characters</span></span>|<span data-ttu-id="b1912-307">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-307">✔</span></span>|<span data-ttu-id="b1912-308">与 Bot 框架一起注册的 bot 的唯一 Microsoft 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="b1912-308">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="b1912-309">这可能与整体[应用程序 ID](#id)很好。</span><span class="sxs-lookup"><span data-stu-id="b1912-309">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="b1912-310">Boolean</span><span class="sxs-lookup"><span data-stu-id="b1912-310">Boolean</span></span>|||<span data-ttu-id="b1912-311">描述 bot 是否利用用户提示将机器人添加到特定频道。</span><span class="sxs-lookup"><span data-stu-id="b1912-311">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="b1912-312">设置`false`</span><span class="sxs-lookup"><span data-stu-id="b1912-312">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="b1912-313">Boolean</span><span class="sxs-lookup"><span data-stu-id="b1912-313">Boolean</span></span>|||<span data-ttu-id="b1912-314">指示 bot 是否为单向仅通知 bot，而不是对话机器人。</span><span class="sxs-lookup"><span data-stu-id="b1912-314">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="b1912-315">设置`false`</span><span class="sxs-lookup"><span data-stu-id="b1912-315">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="b1912-316">Boolean</span><span class="sxs-lookup"><span data-stu-id="b1912-316">Boolean</span></span>|||<span data-ttu-id="b1912-317">指示 bot 是否支持在个人聊天中上载/下载文件的功能。</span><span class="sxs-lookup"><span data-stu-id="b1912-317">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="b1912-318">设置`false`</span><span class="sxs-lookup"><span data-stu-id="b1912-318">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="b1912-319">枚举数组</span><span class="sxs-lookup"><span data-stu-id="b1912-319">Array of enum</span></span>|<span data-ttu-id="b1912-320">3 </span><span class="sxs-lookup"><span data-stu-id="b1912-320">3</span></span>|<span data-ttu-id="b1912-321">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-321">✔</span></span>|<span data-ttu-id="b1912-322">指定机器人是在中的频道上下文中`team`、在组中的聊天（`groupchat`）中，还是在仅限于单个用户（`personal`）的体验中提供体验。</span><span class="sxs-lookup"><span data-stu-id="b1912-322">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="b1912-323">这些选项是非独占的。</span><span class="sxs-lookup"><span data-stu-id="b1912-323">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="b1912-324">commandLists</span><span class="sxs-lookup"><span data-stu-id="b1912-324">bots.commandLists</span></span>

<span data-ttu-id="b1912-325">你的 bot 可以向用户推荐的命令的可选列表。</span><span class="sxs-lookup"><span data-stu-id="b1912-325">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="b1912-326">对象是包含所有类型`object`元素的数组（最多2个元素）;您必须为你的 bot 支持的每个作用域定义单独的命令列表。</span><span class="sxs-lookup"><span data-stu-id="b1912-326">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="b1912-327">有关详细信息，请参阅[Bot 菜单](~/bots/how-to/create-a-bot-commands-menu.md)。</span><span class="sxs-lookup"><span data-stu-id="b1912-327">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="b1912-328">名称</span><span class="sxs-lookup"><span data-stu-id="b1912-328">Name</span></span>| <span data-ttu-id="b1912-329">类型</span><span class="sxs-lookup"><span data-stu-id="b1912-329">Type</span></span>| <span data-ttu-id="b1912-330">最大大小</span><span class="sxs-lookup"><span data-stu-id="b1912-330">Maximum size</span></span> | <span data-ttu-id="b1912-331">必需</span><span class="sxs-lookup"><span data-stu-id="b1912-331">Required</span></span> | <span data-ttu-id="b1912-332">说明</span><span class="sxs-lookup"><span data-stu-id="b1912-332">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="b1912-333">枚举数组</span><span class="sxs-lookup"><span data-stu-id="b1912-333">array of enum</span></span>|<span data-ttu-id="b1912-334">3 </span><span class="sxs-lookup"><span data-stu-id="b1912-334">3</span></span>|<span data-ttu-id="b1912-335">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-335">✔</span></span>|<span data-ttu-id="b1912-336">指定命令列表有效的范围。</span><span class="sxs-lookup"><span data-stu-id="b1912-336">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="b1912-337">选项包括`team`、 `personal`和`groupchat`。</span><span class="sxs-lookup"><span data-stu-id="b1912-337">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="b1912-338">对象数组</span><span class="sxs-lookup"><span data-stu-id="b1912-338">array of objects</span></span>|<span data-ttu-id="b1912-339">10 </span><span class="sxs-lookup"><span data-stu-id="b1912-339">10</span></span>|<span data-ttu-id="b1912-340">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-340">✔</span></span>|<span data-ttu-id="b1912-341">机器人支持的命令数组：</span><span class="sxs-lookup"><span data-stu-id="b1912-341">An array of commands the bot supports:</span></span><br><span data-ttu-id="b1912-342">`title`： bot 命令名称（string，32）</span><span class="sxs-lookup"><span data-stu-id="b1912-342">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="b1912-343">`description`：命令语法及其参数的简单说明或示例（string，128）</span><span class="sxs-lookup"><span data-stu-id="b1912-343">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

## <a name="connectors"></a><span data-ttu-id="b1912-344">插槽</span><span class="sxs-lookup"><span data-stu-id="b1912-344">connectors</span></span>

<span data-ttu-id="b1912-345">**可选**</span><span class="sxs-lookup"><span data-stu-id="b1912-345">**Optional**</span></span>

<span data-ttu-id="b1912-346">`connectors` Block 定义了应用程序的 Office 365 连接器。</span><span class="sxs-lookup"><span data-stu-id="b1912-346">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="b1912-347">对象是包含所有类型`object`元素的数组（最多1个元素）。</span><span class="sxs-lookup"><span data-stu-id="b1912-347">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="b1912-348">仅对提供连接器的解决方案而言，此块是必需的。</span><span class="sxs-lookup"><span data-stu-id="b1912-348">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="b1912-349">名称</span><span class="sxs-lookup"><span data-stu-id="b1912-349">Name</span></span>| <span data-ttu-id="b1912-350">类型</span><span class="sxs-lookup"><span data-stu-id="b1912-350">Type</span></span>| <span data-ttu-id="b1912-351">最大大小</span><span class="sxs-lookup"><span data-stu-id="b1912-351">Maximum size</span></span> | <span data-ttu-id="b1912-352">必需</span><span class="sxs-lookup"><span data-stu-id="b1912-352">Required</span></span> | <span data-ttu-id="b1912-353">说明</span><span class="sxs-lookup"><span data-stu-id="b1912-353">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="b1912-354">String</span><span class="sxs-lookup"><span data-stu-id="b1912-354">String</span></span>|<span data-ttu-id="b1912-355">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-355">2048 characters</span></span>|<span data-ttu-id="b1912-356">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-356">✔</span></span>|<span data-ttu-id="b1912-357">配置连接器时要使用的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="b1912-357">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="b1912-358">String</span><span class="sxs-lookup"><span data-stu-id="b1912-358">String</span></span>|<span data-ttu-id="b1912-359">64个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-359">64 characters</span></span>|<span data-ttu-id="b1912-360">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-360">✔</span></span>|<span data-ttu-id="b1912-361">与[连接器开发人员仪表板](https://aka.ms/connectorsdashboard)中的 ID 相匹配的连接器的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="b1912-361">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="b1912-362">枚举数组</span><span class="sxs-lookup"><span data-stu-id="b1912-362">Array of enum</span></span>|<span data-ttu-id="b1912-363">1 </span><span class="sxs-lookup"><span data-stu-id="b1912-363">1</span></span>|<span data-ttu-id="b1912-364">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-364">✔</span></span>|<span data-ttu-id="b1912-365">指定连接器是在中的频道上下文中`team`，还是在仅限于单个用户的体验（`personal`）中提供体验。</span><span class="sxs-lookup"><span data-stu-id="b1912-365">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="b1912-366">目前，仅支持`team`作用域。</span><span class="sxs-lookup"><span data-stu-id="b1912-366">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="b1912-367">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="b1912-367">composeExtensions</span></span>

<span data-ttu-id="b1912-368">**可选**</span><span class="sxs-lookup"><span data-stu-id="b1912-368">**Optional**</span></span>

<span data-ttu-id="b1912-369">定义应用程序的消息扩展。</span><span class="sxs-lookup"><span data-stu-id="b1912-369">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="b1912-370">功能的名称已从11月2017的 "撰写分机" 更改为 "消息扩展"，但清单名称保持不变，以便现有扩展能够继续正常工作。</span><span class="sxs-lookup"><span data-stu-id="b1912-370">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="b1912-371">对象是包含所有类型`object`元素的数组（最多1个元素）。</span><span class="sxs-lookup"><span data-stu-id="b1912-371">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="b1912-372">仅对提供邮件扩展的解决方案而言，此块是必需的。</span><span class="sxs-lookup"><span data-stu-id="b1912-372">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="b1912-373">名称</span><span class="sxs-lookup"><span data-stu-id="b1912-373">Name</span></span>| <span data-ttu-id="b1912-374">类型</span><span class="sxs-lookup"><span data-stu-id="b1912-374">Type</span></span> | <span data-ttu-id="b1912-375">最大大小</span><span class="sxs-lookup"><span data-stu-id="b1912-375">Maximum Size</span></span> | <span data-ttu-id="b1912-376">必需</span><span class="sxs-lookup"><span data-stu-id="b1912-376">Required</span></span> | <span data-ttu-id="b1912-377">说明</span><span class="sxs-lookup"><span data-stu-id="b1912-377">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="b1912-378">String</span><span class="sxs-lookup"><span data-stu-id="b1912-378">String</span></span>|<span data-ttu-id="b1912-379">64</span><span class="sxs-lookup"><span data-stu-id="b1912-379">64</span></span>|<span data-ttu-id="b1912-380">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-380">✔</span></span>|<span data-ttu-id="b1912-381">与 Bot 框架一起注册的支持邮件扩展的 bot 的唯一 Microsoft 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="b1912-381">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="b1912-382">这可能与整体[应用程序 ID](#id)很好。</span><span class="sxs-lookup"><span data-stu-id="b1912-382">This may well be the same as the overall [app ID](#id).</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="b1912-383">Boolean</span><span class="sxs-lookup"><span data-stu-id="b1912-383">Boolean</span></span>|||<span data-ttu-id="b1912-384">一个值，指示用户是否可以更新邮件扩展的配置。</span><span class="sxs-lookup"><span data-stu-id="b1912-384">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="b1912-385">默认值为`false`。</span><span class="sxs-lookup"><span data-stu-id="b1912-385">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="b1912-386">对象数组</span><span class="sxs-lookup"><span data-stu-id="b1912-386">Array of object</span></span>|<span data-ttu-id="b1912-387">10 </span><span class="sxs-lookup"><span data-stu-id="b1912-387">10</span></span>|<span data-ttu-id="b1912-388">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-388">✔</span></span>|<span data-ttu-id="b1912-389">邮件扩展支持的命令数组</span><span class="sxs-lookup"><span data-stu-id="b1912-389">Array of commands the messaging extension supports</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="b1912-390">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="b1912-390">composeExtensions.commands</span></span>

<span data-ttu-id="b1912-391">您的邮件扩展应声明一个或多个命令。</span><span class="sxs-lookup"><span data-stu-id="b1912-391">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="b1912-392">在 Microsoft 团队中，每个命令都显示为从基于 UI 的入口点的潜在交互。</span><span class="sxs-lookup"><span data-stu-id="b1912-392">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="b1912-393">最多可以有10个命令。</span><span class="sxs-lookup"><span data-stu-id="b1912-393">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="b1912-394">每个命令项都是一个具有以下结构的对象：</span><span class="sxs-lookup"><span data-stu-id="b1912-394">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="b1912-395">名称</span><span class="sxs-lookup"><span data-stu-id="b1912-395">Name</span></span>| <span data-ttu-id="b1912-396">类型</span><span class="sxs-lookup"><span data-stu-id="b1912-396">Type</span></span>| <span data-ttu-id="b1912-397">最大大小</span><span class="sxs-lookup"><span data-stu-id="b1912-397">Maximum size</span></span> | <span data-ttu-id="b1912-398">必需</span><span class="sxs-lookup"><span data-stu-id="b1912-398">Required</span></span> | <span data-ttu-id="b1912-399">说明</span><span class="sxs-lookup"><span data-stu-id="b1912-399">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="b1912-400">String</span><span class="sxs-lookup"><span data-stu-id="b1912-400">String</span></span>|<span data-ttu-id="b1912-401">64个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-401">64 characters</span></span>|<span data-ttu-id="b1912-402">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-402">✔</span></span>|<span data-ttu-id="b1912-403">命令的 ID</span><span class="sxs-lookup"><span data-stu-id="b1912-403">The ID for the command</span></span>|
|`type`|<span data-ttu-id="b1912-404">String</span><span class="sxs-lookup"><span data-stu-id="b1912-404">String</span></span>|<span data-ttu-id="b1912-405">64个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-405">64 characters</span></span>||<span data-ttu-id="b1912-406">命令的类型。</span><span class="sxs-lookup"><span data-stu-id="b1912-406">Type of the command.</span></span> <span data-ttu-id="b1912-407">一个`query`或`action`。</span><span class="sxs-lookup"><span data-stu-id="b1912-407">One of `query` or `action`.</span></span> <span data-ttu-id="b1912-408">设置`query`</span><span class="sxs-lookup"><span data-stu-id="b1912-408">Default: `query`</span></span>|
|`title`|<span data-ttu-id="b1912-409">String</span><span class="sxs-lookup"><span data-stu-id="b1912-409">String</span></span>|<span data-ttu-id="b1912-410">32个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-410">32 characters</span></span>|<span data-ttu-id="b1912-411">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-411">✔</span></span>|<span data-ttu-id="b1912-412">用户友好的命令名称</span><span class="sxs-lookup"><span data-stu-id="b1912-412">The user-friendly command name</span></span>|
|`description`|<span data-ttu-id="b1912-413">String</span><span class="sxs-lookup"><span data-stu-id="b1912-413">String</span></span>|<span data-ttu-id="b1912-414">128个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-414">128 characters</span></span>||<span data-ttu-id="b1912-415">对用户显示的说明，以指示此命令的用途</span><span class="sxs-lookup"><span data-stu-id="b1912-415">The description that appears to users to indicate the purpose of this command</span></span>|
|`initialRun`|<span data-ttu-id="b1912-416">Boolean</span><span class="sxs-lookup"><span data-stu-id="b1912-416">Boolean</span></span>|||<span data-ttu-id="b1912-417">一个布尔值，指示是否在最初不使用任何参数的情况之下运行该命令。</span><span class="sxs-lookup"><span data-stu-id="b1912-417">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="b1912-418">设置`false`</span><span class="sxs-lookup"><span data-stu-id="b1912-418">Default: `false`</span></span>|
|`context`|<span data-ttu-id="b1912-419">Array of Strings</span><span class="sxs-lookup"><span data-stu-id="b1912-419">Array of Strings</span></span>|<span data-ttu-id="b1912-420">3 </span><span class="sxs-lookup"><span data-stu-id="b1912-420">3</span></span>||<span data-ttu-id="b1912-421">定义可以从中调用邮件扩展的位置。</span><span class="sxs-lookup"><span data-stu-id="b1912-421">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="b1912-422">、 `commandBox`、 `message`的`compose`的任意组合。</span><span class="sxs-lookup"><span data-stu-id="b1912-422">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="b1912-423">默认值为`["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="b1912-423">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="b1912-424">Boolean</span><span class="sxs-lookup"><span data-stu-id="b1912-424">Boolean</span></span>|||<span data-ttu-id="b1912-425">一个布尔值，指示是否应动态获取任务模块</span><span class="sxs-lookup"><span data-stu-id="b1912-425">A boolean value that indicates if it should fetch the task module dynamically</span></span>|
|`taskInfo`|<span data-ttu-id="b1912-426">对象</span><span class="sxs-lookup"><span data-stu-id="b1912-426">Object</span></span>|||<span data-ttu-id="b1912-427">指定在使用消息扩展命令时要预加载的任务模块</span><span class="sxs-lookup"><span data-stu-id="b1912-427">Specify the task module to preload when using a messaging extension command</span></span>|
|`taskInfo.title`|<span data-ttu-id="b1912-428">String</span><span class="sxs-lookup"><span data-stu-id="b1912-428">String</span></span>|<span data-ttu-id="b1912-429">64</span><span class="sxs-lookup"><span data-stu-id="b1912-429">64</span></span>||<span data-ttu-id="b1912-430">初始对话框标题</span><span class="sxs-lookup"><span data-stu-id="b1912-430">Initial dialog title</span></span>|
|`taskInfo.width`|<span data-ttu-id="b1912-431">String</span><span class="sxs-lookup"><span data-stu-id="b1912-431">String</span></span>|||<span data-ttu-id="b1912-432">对话框宽度-以像素为单位的数字或默认布局，如 "大"、"中" 或 "small"</span><span class="sxs-lookup"><span data-stu-id="b1912-432">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.height`|<span data-ttu-id="b1912-433">String</span><span class="sxs-lookup"><span data-stu-id="b1912-433">String</span></span>|||<span data-ttu-id="b1912-434">对话框高度-以像素为单位的数字或默认布局，如 "大"、"中" 或 "small"</span><span class="sxs-lookup"><span data-stu-id="b1912-434">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.url`|<span data-ttu-id="b1912-435">String</span><span class="sxs-lookup"><span data-stu-id="b1912-435">String</span></span>|||<span data-ttu-id="b1912-436">初始 web 视图 URL</span><span class="sxs-lookup"><span data-stu-id="b1912-436">Initial webview URL</span></span>|
|`messageHandlers`|<span data-ttu-id="b1912-437">对象数组</span><span class="sxs-lookup"><span data-stu-id="b1912-437">Array of Objects</span></span>|<span data-ttu-id="b1912-438">5 </span><span class="sxs-lookup"><span data-stu-id="b1912-438">5</span></span>||<span data-ttu-id="b1912-439">允许在满足特定条件时调用应用程序的处理程序列表。</span><span class="sxs-lookup"><span data-stu-id="b1912-439">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="b1912-440">域也必须列在`validDomains`</span><span class="sxs-lookup"><span data-stu-id="b1912-440">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="b1912-441">String</span><span class="sxs-lookup"><span data-stu-id="b1912-441">String</span></span>|||<span data-ttu-id="b1912-442">消息处理程序的类型。</span><span class="sxs-lookup"><span data-stu-id="b1912-442">The type of message handler.</span></span> <span data-ttu-id="b1912-443">必须是 `"link"`。</span><span class="sxs-lookup"><span data-stu-id="b1912-443">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="b1912-444">Array of Strings</span><span class="sxs-lookup"><span data-stu-id="b1912-444">Array of Strings</span></span>|||<span data-ttu-id="b1912-445">链接消息处理程序可以为其注册的域的数组。</span><span class="sxs-lookup"><span data-stu-id="b1912-445">Array of domains that the link message handler can register for.</span></span>|
|`parameters`|<span data-ttu-id="b1912-446">对象数组</span><span class="sxs-lookup"><span data-stu-id="b1912-446">Array of object</span></span>|<span data-ttu-id="b1912-447">5 </span><span class="sxs-lookup"><span data-stu-id="b1912-447">5</span></span>|<span data-ttu-id="b1912-448">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-448">✔</span></span>|<span data-ttu-id="b1912-449">命令所采用的参数的列表。</span><span class="sxs-lookup"><span data-stu-id="b1912-449">The list of parameters the command takes.</span></span> <span data-ttu-id="b1912-450">最小值： 1;最大值：5</span><span class="sxs-lookup"><span data-stu-id="b1912-450">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="b1912-451">String</span><span class="sxs-lookup"><span data-stu-id="b1912-451">String</span></span>|<span data-ttu-id="b1912-452">64个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-452">64 characters</span></span>|<span data-ttu-id="b1912-453">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-453">✔</span></span>|<span data-ttu-id="b1912-454">在客户端中显示的参数的名称。</span><span class="sxs-lookup"><span data-stu-id="b1912-454">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="b1912-455">此项包含在用户请求中。</span><span class="sxs-lookup"><span data-stu-id="b1912-455">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="b1912-456">String</span><span class="sxs-lookup"><span data-stu-id="b1912-456">String</span></span>|<span data-ttu-id="b1912-457">32个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-457">32 characters</span></span>|<span data-ttu-id="b1912-458">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-458">✔</span></span>|<span data-ttu-id="b1912-459">参数的用户友好标题。</span><span class="sxs-lookup"><span data-stu-id="b1912-459">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="b1912-460">String</span><span class="sxs-lookup"><span data-stu-id="b1912-460">String</span></span>|<span data-ttu-id="b1912-461">128个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-461">128 characters</span></span>||<span data-ttu-id="b1912-462">描述此参数用途的用户友好字符串。</span><span class="sxs-lookup"><span data-stu-id="b1912-462">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="b1912-463">String</span><span class="sxs-lookup"><span data-stu-id="b1912-463">String</span></span>|<span data-ttu-id="b1912-464">128个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-464">128 characters</span></span>||<span data-ttu-id="b1912-465">定义在的任务模块上显示的控件的类型`fetchTask: true`。</span><span class="sxs-lookup"><span data-stu-id="b1912-465">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="b1912-466">一个`text` `textarea`、 `number` `date`、、、、 `time` `toggle``choiceset`</span><span class="sxs-lookup"><span data-stu-id="b1912-466">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`</span></span>|
|`parameter.choices`|<span data-ttu-id="b1912-467">对象数组</span><span class="sxs-lookup"><span data-stu-id="b1912-467">Array of Objects</span></span>|<span data-ttu-id="b1912-468">10 </span><span class="sxs-lookup"><span data-stu-id="b1912-468">10</span></span>||<span data-ttu-id="b1912-469">的选项选项`choiceset`。</span><span class="sxs-lookup"><span data-stu-id="b1912-469">The choice options for the `choiceset`.</span></span> <span data-ttu-id="b1912-470">仅在何时`parameter.inputType`使用`choiceset`</span><span class="sxs-lookup"><span data-stu-id="b1912-470">Use only when `parameter.inputType` is `choiceset`</span></span>|
|`parameter.choices.title`|<span data-ttu-id="b1912-471">String</span><span class="sxs-lookup"><span data-stu-id="b1912-471">String</span></span>|<span data-ttu-id="b1912-472">128</span><span class="sxs-lookup"><span data-stu-id="b1912-472">128</span></span>||<span data-ttu-id="b1912-473">选项的标题</span><span class="sxs-lookup"><span data-stu-id="b1912-473">Title of the choice</span></span>|
|`parameter.choices.value`|<span data-ttu-id="b1912-474">String</span><span class="sxs-lookup"><span data-stu-id="b1912-474">String</span></span>|<span data-ttu-id="b1912-475">512</span><span class="sxs-lookup"><span data-stu-id="b1912-475">512</span></span>||<span data-ttu-id="b1912-476">选项的值</span><span class="sxs-lookup"><span data-stu-id="b1912-476">Value of the choice</span></span>|

## <a name="permissions"></a><span data-ttu-id="b1912-477">permissions</span><span class="sxs-lookup"><span data-stu-id="b1912-477">permissions</span></span>

<span data-ttu-id="b1912-478">**可选**</span><span class="sxs-lookup"><span data-stu-id="b1912-478">**Optional**</span></span>

<span data-ttu-id="b1912-479">一个数组， `string`它指定应用程序请求的权限，这样最终用户就可以知道扩展将如何执行。</span><span class="sxs-lookup"><span data-stu-id="b1912-479">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="b1912-480">以下选项是非独占的：</span><span class="sxs-lookup"><span data-stu-id="b1912-480">The following options are non-exclusive:</span></span>

* <span data-ttu-id="b1912-481">`identity`&emsp;需要用户标识信息</span><span class="sxs-lookup"><span data-stu-id="b1912-481">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="b1912-482">`messageTeamMembers`&emsp;需要向团队成员发送直接消息的权限</span><span class="sxs-lookup"><span data-stu-id="b1912-482">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="b1912-483">在更新应用程序时更改这些权限将导致用户在首次运行更新的应用程序时重复同意过程。</span><span class="sxs-lookup"><span data-stu-id="b1912-483">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="b1912-484">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="b1912-484">devicePermissions</span></span>

<span data-ttu-id="b1912-485">**可选**字符串数组</span><span class="sxs-lookup"><span data-stu-id="b1912-485">**Optional** Array of Strings</span></span>

<span data-ttu-id="b1912-486">在用户的设备上指定您的应用程序可能会请求访问的本机功能。</span><span class="sxs-lookup"><span data-stu-id="b1912-486">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="b1912-487">选项包括：</span><span class="sxs-lookup"><span data-stu-id="b1912-487">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="b1912-488">validDomains</span><span class="sxs-lookup"><span data-stu-id="b1912-488">validDomains</span></span>

<span data-ttu-id="b1912-489">**可选**，但**所需**的除外</span><span class="sxs-lookup"><span data-stu-id="b1912-489">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="b1912-490">应用程序预期从中加载任何内容的有效域的列表。</span><span class="sxs-lookup"><span data-stu-id="b1912-490">A list of valid domains from which the app expects to load any content.</span></span> <span data-ttu-id="b1912-491">例如`*.example.com`，域列表可以包含通配符。</span><span class="sxs-lookup"><span data-stu-id="b1912-491">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="b1912-492">这与域的一段完全匹配;如果需要匹配`a.b.example.com` ，请使用`*.*.example.com`。</span><span class="sxs-lookup"><span data-stu-id="b1912-492">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="b1912-493">如果您的选项卡配置或内容 UI 需要导航到其他任何域，除了用于选项卡配置之外，则必须在此处指定该域。</span><span class="sxs-lookup"><span data-stu-id="b1912-493">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="b1912-494">但是，**不**需要在您的应用程序中包含要支持的标识提供程序的域。</span><span class="sxs-lookup"><span data-stu-id="b1912-494">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="b1912-495">例如，若要使用 Google ID 进行身份验证，需要重定向到 accounts.google.com，但不应在中`validDomains[]`包含 accounts.google.com。</span><span class="sxs-lookup"><span data-stu-id="b1912-495">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b1912-496">不要直接或通过通配符添加位于控件外部的域。</span><span class="sxs-lookup"><span data-stu-id="b1912-496">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="b1912-497">例如， `yourapp.onmicrosoft.com`是有效的，但`*.onmicrosoft.com`无效。</span><span class="sxs-lookup"><span data-stu-id="b1912-497">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="b1912-498">对象是一个包含所有类型`string`的元素的数组。</span><span class="sxs-lookup"><span data-stu-id="b1912-498">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="b1912-499">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="b1912-499">webApplicationInfo</span></span>

<span data-ttu-id="b1912-500">**可选**</span><span class="sxs-lookup"><span data-stu-id="b1912-500">**Optional**</span></span>

<span data-ttu-id="b1912-501">指定 AAD 应用 ID 和 Graph 信息，以帮助用户无缝登录 AAD 应用。</span><span class="sxs-lookup"><span data-stu-id="b1912-501">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="b1912-502">名称</span><span class="sxs-lookup"><span data-stu-id="b1912-502">Name</span></span>| <span data-ttu-id="b1912-503">类型</span><span class="sxs-lookup"><span data-stu-id="b1912-503">Type</span></span>| <span data-ttu-id="b1912-504">最大大小</span><span class="sxs-lookup"><span data-stu-id="b1912-504">Maximum size</span></span> | <span data-ttu-id="b1912-505">必需</span><span class="sxs-lookup"><span data-stu-id="b1912-505">Required</span></span> | <span data-ttu-id="b1912-506">说明</span><span class="sxs-lookup"><span data-stu-id="b1912-506">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="b1912-507">String</span><span class="sxs-lookup"><span data-stu-id="b1912-507">String</span></span>|<span data-ttu-id="b1912-508">36个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-508">36 characters</span></span>|<span data-ttu-id="b1912-509">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-509">✔</span></span>|<span data-ttu-id="b1912-510">应用程序的 AAD 应用程序 id。</span><span class="sxs-lookup"><span data-stu-id="b1912-510">AAD application id of the app.</span></span> <span data-ttu-id="b1912-511">此 id 必须为 GUID。</span><span class="sxs-lookup"><span data-stu-id="b1912-511">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="b1912-512">String</span><span class="sxs-lookup"><span data-stu-id="b1912-512">String</span></span>|<span data-ttu-id="b1912-513">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="b1912-513">2048 characters</span></span>|<span data-ttu-id="b1912-514">✔</span><span class="sxs-lookup"><span data-stu-id="b1912-514">✔</span></span>|<span data-ttu-id="b1912-515">用于获取 SSO 的身份验证令牌的应用程序的资源 url。</span><span class="sxs-lookup"><span data-stu-id="b1912-515">Resource url of app for acquiring auth token for SSO.</span></span>|