---
title: 开发者预览版清单架构参考
description: 介绍清单支持的架构Microsoft Teams
ms.topic: reference
keywords: teams 清单架构开发者预览版
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: c2009038341a22664b0f055fa9756a9d1eba87b9
ms.sourcegitcommit: 64c1cf2a268ef101a519bc31d171618d0f6cd12a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2021
ms.locfileid: "52915088"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="71eac-104">开发人员预览清单架构Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="71eac-104">Developer preview manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="71eac-105">若要了解如何启用开发人员预览，请参阅公共[开发人员预览Microsoft Teams。](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="71eac-105">For information on how to enable developer preview, see [public developer preview for Microsoft Teams](~/resources/dev-preview/developer-preview-intro.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="71eac-106">如果不使用开发人员预览功能，请改为使用 GA [功能的应用清单](~/resources/schema/manifest-schema.md) 。</span><span class="sxs-lookup"><span data-stu-id="71eac-106">If you aren't using developer preview features, use the [app manifest for GA features](~/resources/schema/manifest-schema.md) instead.</span></span>

<span data-ttu-id="71eac-107">Microsoft Teams清单介绍了应用如何集成到 Microsoft Teams 产品。</span><span class="sxs-lookup"><span data-stu-id="71eac-107">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="71eac-108">清单必须符合 托管在 的架构 [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) 。</span><span class="sxs-lookup"><span data-stu-id="71eac-108">Your manifest must conform to the schema hosted at [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span></span>

<span data-ttu-id="71eac-109">有关可用功能详细信息，请参阅公共更新开发者预览版[中的Microsoft Teams。](~/resources/dev-preview/developer-preview-features.md)</span><span class="sxs-lookup"><span data-stu-id="71eac-109">For more information on the features available see: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="71eac-110">示例完整清单</span><span class="sxs-lookup"><span data-stu-id="71eac-110">Sample full manifest</span></span>

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
      "contentBotId": "Specifies to the app that tab is an Adaptive Card Tab. You can either provide the contentBotId or contentUrl.",
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
  "webApplicationInfo": {
    "id": "AAD App ID",
    "resource": "Resource URL for acquiring auth token for SSO",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelSettings.Read.Group",
      "ChannelSettings.Edit.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "ChannelMessage.Read.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.Edit.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group",
      "Member.ReadWrite.Group",
      "Owner.ReadWrite.Group"
    ],
  },
   "configurableProperties": [
     "name",
     "shortDescription",
     "longDescription",
     "smallImageUrl", 
     "largeImageUrl", 
     "accentColor",
     "developerUrl",
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

<span data-ttu-id="71eac-111">该架构定义以下属性：</span><span class="sxs-lookup"><span data-stu-id="71eac-111">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="71eac-112">$schema</span><span class="sxs-lookup"><span data-stu-id="71eac-112">$schema</span></span>

<span data-ttu-id="71eac-113">*可选，但建议* &ndash; 字符串</span><span class="sxs-lookup"><span data-stu-id="71eac-113">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="71eac-114">引用 https:// JSON 架构的 URL。</span><span class="sxs-lookup"><span data-stu-id="71eac-114">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="71eac-115">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="71eac-115">manifestVersion</span></span>

<span data-ttu-id="71eac-116">**必需** &ndash; 字符串</span><span class="sxs-lookup"><span data-stu-id="71eac-116">**Required** &ndash; String</span></span>

<span data-ttu-id="71eac-117">此清单使用的清单架构版本。</span><span class="sxs-lookup"><span data-stu-id="71eac-117">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="71eac-118">它应为"devPreview"。</span><span class="sxs-lookup"><span data-stu-id="71eac-118">It should be "devPreview".</span></span>

## <a name="version"></a><span data-ttu-id="71eac-119">version</span><span class="sxs-lookup"><span data-stu-id="71eac-119">version</span></span>

<span data-ttu-id="71eac-120">**必需** &ndash; 字符串</span><span class="sxs-lookup"><span data-stu-id="71eac-120">**Required** &ndash; String</span></span>

<span data-ttu-id="71eac-121">特定应用的版本。</span><span class="sxs-lookup"><span data-stu-id="71eac-121">The version of the specific app.</span></span> <span data-ttu-id="71eac-122">如果更新清单中的某些内容，则版本也必须递增。</span><span class="sxs-lookup"><span data-stu-id="71eac-122">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="71eac-123">这样一来，在安装新的清单时，它将覆盖现有的版本，用户将获得新的功能。</span><span class="sxs-lookup"><span data-stu-id="71eac-123">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="71eac-124">如果此应用已提交到应用商店，则新清单必须重新提交和重新验证。</span><span class="sxs-lookup"><span data-stu-id="71eac-124">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="71eac-125">然后，此应用的用户将在经过批准后数小时内自动获取新的更新清单。</span><span class="sxs-lookup"><span data-stu-id="71eac-125">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="71eac-126">如果应用请求的权限更改，将提示用户升级并重新同意应用。</span><span class="sxs-lookup"><span data-stu-id="71eac-126">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="71eac-127">此版本字符串必须遵循 [Semver](http://semver.org/) 标准 (MAJOR。MINOR。PATCH) 。</span><span class="sxs-lookup"><span data-stu-id="71eac-127">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="71eac-128">id</span><span class="sxs-lookup"><span data-stu-id="71eac-128">id</span></span>

<span data-ttu-id="71eac-129">**必需** &ndash; Microsoft 应用 ID</span><span class="sxs-lookup"><span data-stu-id="71eac-129">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="71eac-130">此应用的唯一 Microsoft 生成的标识符。</span><span class="sxs-lookup"><span data-stu-id="71eac-130">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="71eac-131">如果你已经通过 Microsoft Bot Framework 注册了自动程序，或者你的选项卡的 Web 应用已经使用 Microsoft 登录，你应该已经拥有 ID，并且应在此处输入它。</span><span class="sxs-lookup"><span data-stu-id="71eac-131">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="71eac-132">否则，应在"我的应用程序" (Microsoft 应用程序注册门户 [) 生成](https://apps.dev.microsoft.com) 一个新 ID，在此处输入，然后在添加自动程序时重复使用 [它](~/bots/how-to/create-a-bot-for-teams.md)。</span><span class="sxs-lookup"><span data-stu-id="71eac-132">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you [add a bot](~/bots/how-to/create-a-bot-for-teams.md).</span></span>

## <a name="packagename"></a><span data-ttu-id="71eac-133">packageName</span><span class="sxs-lookup"><span data-stu-id="71eac-133">packageName</span></span>

<span data-ttu-id="71eac-134">**必需** &ndash; 字符串</span><span class="sxs-lookup"><span data-stu-id="71eac-134">**Required** &ndash; String</span></span>

<span data-ttu-id="71eac-135">反向域表示法中此应用程序的唯一标识符;例如，com.example.myapp。</span><span class="sxs-lookup"><span data-stu-id="71eac-135">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="71eac-136">developer</span><span class="sxs-lookup"><span data-stu-id="71eac-136">developer</span></span>

<span data-ttu-id="71eac-137">**Required**</span><span class="sxs-lookup"><span data-stu-id="71eac-137">**Required**</span></span>

<span data-ttu-id="71eac-138">指定有关你的公司的信息。</span><span class="sxs-lookup"><span data-stu-id="71eac-138">Specifies information about your company.</span></span> <span data-ttu-id="71eac-139">对于提交到 AppSource (之前Office应用商店) ，这些值必须与 AppSource 条目中的信息匹配。</span><span class="sxs-lookup"><span data-stu-id="71eac-139">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span>

|<span data-ttu-id="71eac-140">名称</span><span class="sxs-lookup"><span data-stu-id="71eac-140">Name</span></span>| <span data-ttu-id="71eac-141">最大大小</span><span class="sxs-lookup"><span data-stu-id="71eac-141">Maximum size</span></span> | <span data-ttu-id="71eac-142">必需</span><span class="sxs-lookup"><span data-stu-id="71eac-142">Required</span></span> | <span data-ttu-id="71eac-143">说明</span><span class="sxs-lookup"><span data-stu-id="71eac-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="71eac-144">32 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-144">32 characters</span></span>|<span data-ttu-id="71eac-145">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-145">✔</span></span>|<span data-ttu-id="71eac-146">开发人员显示名称的指南。</span><span class="sxs-lookup"><span data-stu-id="71eac-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="71eac-147">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-147">2048 characters</span></span>|<span data-ttu-id="71eac-148">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-148">✔</span></span>|<span data-ttu-id="71eac-149">the https:// URL to the developer's website.</span><span class="sxs-lookup"><span data-stu-id="71eac-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="71eac-150">此链接应让用户访问你的公司或特定于产品的登陆页面。</span><span class="sxs-lookup"><span data-stu-id="71eac-150">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="71eac-151">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-151">2048 characters</span></span>|<span data-ttu-id="71eac-152">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-152">✔</span></span>|<span data-ttu-id="71eac-153">the https:// URL to the developer's privacy policy.</span><span class="sxs-lookup"><span data-stu-id="71eac-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="71eac-154">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-154">2048 characters</span></span>|<span data-ttu-id="71eac-155">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-155">✔</span></span>|<span data-ttu-id="71eac-156">the https:// URL to the developer's use terms.</span><span class="sxs-lookup"><span data-stu-id="71eac-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="71eac-157">10 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-157">10 characters</span></span>|<span data-ttu-id="71eac-158">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-158">✔</span></span>|<span data-ttu-id="71eac-159">**可选** 标识生成应用的合作伙伴组织的 Microsoft 合作伙伴网络 ID。</span><span class="sxs-lookup"><span data-stu-id="71eac-159">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="71eac-160">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="71eac-160">localizationInfo</span></span>

<span data-ttu-id="71eac-161">**可选**</span><span class="sxs-lookup"><span data-stu-id="71eac-161">**Optional**</span></span>

<span data-ttu-id="71eac-162">允许指定默认语言，以及指向其他语言文件的指针。</span><span class="sxs-lookup"><span data-stu-id="71eac-162">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="71eac-163">请参阅 [本地化](~/concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="71eac-163">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="71eac-164">名称</span><span class="sxs-lookup"><span data-stu-id="71eac-164">Name</span></span>| <span data-ttu-id="71eac-165">最大大小</span><span class="sxs-lookup"><span data-stu-id="71eac-165">Maximum size</span></span> | <span data-ttu-id="71eac-166">必需</span><span class="sxs-lookup"><span data-stu-id="71eac-166">Required</span></span> | <span data-ttu-id="71eac-167">说明</span><span class="sxs-lookup"><span data-stu-id="71eac-167">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`|<span data-ttu-id="71eac-168">4 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-168">4 characters</span></span>|<span data-ttu-id="71eac-169">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-169">✔</span></span>|<span data-ttu-id="71eac-170">此顶级清单文件中字符串的语言标记。</span><span class="sxs-lookup"><span data-stu-id="71eac-170">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="71eac-171">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="71eac-171">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="71eac-172">指定其他语言翻译的对象数组。</span><span class="sxs-lookup"><span data-stu-id="71eac-172">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="71eac-173">名称</span><span class="sxs-lookup"><span data-stu-id="71eac-173">Name</span></span>| <span data-ttu-id="71eac-174">最大大小</span><span class="sxs-lookup"><span data-stu-id="71eac-174">Maximum size</span></span> | <span data-ttu-id="71eac-175">必需</span><span class="sxs-lookup"><span data-stu-id="71eac-175">Required</span></span> | <span data-ttu-id="71eac-176">说明</span><span class="sxs-lookup"><span data-stu-id="71eac-176">Description</span></span>|
|---|---|---|---|
|`languageTag`|<span data-ttu-id="71eac-177">4 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-177">4 characters</span></span>|<span data-ttu-id="71eac-178">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-178">✔</span></span>|<span data-ttu-id="71eac-179">提供的文件中字符串的语言标记。</span><span class="sxs-lookup"><span data-stu-id="71eac-179">The language tag of the strings in the provided file.</span></span>|
|`file`|<span data-ttu-id="71eac-180">4 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-180">4 characters</span></span>|<span data-ttu-id="71eac-181">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-181">✔</span></span>|<span data-ttu-id="71eac-182">包含已翻译字符串的 .json 文件的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="71eac-182">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="71eac-183">name</span><span class="sxs-lookup"><span data-stu-id="71eac-183">name</span></span>

<span data-ttu-id="71eac-184">**Required**</span><span class="sxs-lookup"><span data-stu-id="71eac-184">**Required**</span></span>

<span data-ttu-id="71eac-185">应用体验的名称，在应用体验中向Teams显示。</span><span class="sxs-lookup"><span data-stu-id="71eac-185">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="71eac-186">对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。</span><span class="sxs-lookup"><span data-stu-id="71eac-186">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="71eac-187">和 `short` `full` 的值不应相同。</span><span class="sxs-lookup"><span data-stu-id="71eac-187">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="71eac-188">名称</span><span class="sxs-lookup"><span data-stu-id="71eac-188">Name</span></span>| <span data-ttu-id="71eac-189">最大大小</span><span class="sxs-lookup"><span data-stu-id="71eac-189">Maximum size</span></span> | <span data-ttu-id="71eac-190">必需</span><span class="sxs-lookup"><span data-stu-id="71eac-190">Required</span></span> | <span data-ttu-id="71eac-191">说明</span><span class="sxs-lookup"><span data-stu-id="71eac-191">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="71eac-192">30 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-192">30 characters</span></span>|<span data-ttu-id="71eac-193">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-193">✔</span></span>|<span data-ttu-id="71eac-194">应用的显示名称。</span><span class="sxs-lookup"><span data-stu-id="71eac-194">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="71eac-195">100 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-195">100 characters</span></span>||<span data-ttu-id="71eac-196">应用的完整名称，在完整应用名称超过 30 个字符时使用。</span><span class="sxs-lookup"><span data-stu-id="71eac-196">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="71eac-197">说明</span><span class="sxs-lookup"><span data-stu-id="71eac-197">description</span></span>

<span data-ttu-id="71eac-198">**Required**</span><span class="sxs-lookup"><span data-stu-id="71eac-198">**Required**</span></span>

<span data-ttu-id="71eac-199">向用户描述你的应用。</span><span class="sxs-lookup"><span data-stu-id="71eac-199">Describes your app to users.</span></span> <span data-ttu-id="71eac-200">对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。</span><span class="sxs-lookup"><span data-stu-id="71eac-200">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="71eac-201">确保你的描述准确地描述了你的体验，并提供相关信息来帮助潜在客户了解你的体验。</span><span class="sxs-lookup"><span data-stu-id="71eac-201">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="71eac-202">还应在完整说明中注意，如果需要使用外部帐户。</span><span class="sxs-lookup"><span data-stu-id="71eac-202">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="71eac-203">和 `short` `full` 的值不应相同。</span><span class="sxs-lookup"><span data-stu-id="71eac-203">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="71eac-204">简短说明不得在详细说明中重复，且不得包含任何其他应用名称。</span><span class="sxs-lookup"><span data-stu-id="71eac-204">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="71eac-205">名称</span><span class="sxs-lookup"><span data-stu-id="71eac-205">Name</span></span>| <span data-ttu-id="71eac-206">最大大小</span><span class="sxs-lookup"><span data-stu-id="71eac-206">Maximum size</span></span> | <span data-ttu-id="71eac-207">必需</span><span class="sxs-lookup"><span data-stu-id="71eac-207">Required</span></span> | <span data-ttu-id="71eac-208">说明</span><span class="sxs-lookup"><span data-stu-id="71eac-208">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="71eac-209">80 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-209">80 characters</span></span>|<span data-ttu-id="71eac-210">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-210">✔</span></span>|<span data-ttu-id="71eac-211">应用体验的简短说明，在空间有限时使用。</span><span class="sxs-lookup"><span data-stu-id="71eac-211">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="71eac-212">4000 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-212">4000 characters</span></span>|<span data-ttu-id="71eac-213">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-213">✔</span></span>|<span data-ttu-id="71eac-214">应用的完整说明。</span><span class="sxs-lookup"><span data-stu-id="71eac-214">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="71eac-215">图标</span><span class="sxs-lookup"><span data-stu-id="71eac-215">icons</span></span>

<span data-ttu-id="71eac-216">**Required**</span><span class="sxs-lookup"><span data-stu-id="71eac-216">**Required**</span></span>

<span data-ttu-id="71eac-217">在应用内使用的Teams图标。</span><span class="sxs-lookup"><span data-stu-id="71eac-217">Icons used within the Teams app.</span></span> <span data-ttu-id="71eac-218">图标文件必须作为上传程序包的一部分包含在内。</span><span class="sxs-lookup"><span data-stu-id="71eac-218">The icon files must be included as part of the upload package.</span></span>

|<span data-ttu-id="71eac-219">名称</span><span class="sxs-lookup"><span data-stu-id="71eac-219">Name</span></span>| <span data-ttu-id="71eac-220">最大大小</span><span class="sxs-lookup"><span data-stu-id="71eac-220">Maximum size</span></span> | <span data-ttu-id="71eac-221">必需</span><span class="sxs-lookup"><span data-stu-id="71eac-221">Required</span></span> | <span data-ttu-id="71eac-222">说明</span><span class="sxs-lookup"><span data-stu-id="71eac-222">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="71eac-223">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-223">2048 characters</span></span>|<span data-ttu-id="71eac-224">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-224">✔</span></span>|<span data-ttu-id="71eac-225">指向透明 32x32 PNG 大纲图标的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="71eac-225">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="71eac-226">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-226">2048 characters</span></span>|<span data-ttu-id="71eac-227">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-227">✔</span></span>|<span data-ttu-id="71eac-228">完整颜色 192x192 PNG 图标的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="71eac-228">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="71eac-229">accentColor</span><span class="sxs-lookup"><span data-stu-id="71eac-229">accentColor</span></span>

<span data-ttu-id="71eac-230">**必需** &ndash; 字符串</span><span class="sxs-lookup"><span data-stu-id="71eac-230">**Required** &ndash; String</span></span>

<span data-ttu-id="71eac-231">要与 和 结合使用用作大纲图标背景的颜色。</span><span class="sxs-lookup"><span data-stu-id="71eac-231">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="71eac-232">该值必须是以"#"开头的有效 HTML 颜色代码，例如 `#4464ee` 。</span><span class="sxs-lookup"><span data-stu-id="71eac-232">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="71eac-233">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="71eac-233">configurableTabs</span></span>

<span data-ttu-id="71eac-234">**可选**</span><span class="sxs-lookup"><span data-stu-id="71eac-234">**Optional**</span></span>

<span data-ttu-id="71eac-235">当你的应用体验具有团队频道选项卡体验时，需要在添加前进行额外配置。</span><span class="sxs-lookup"><span data-stu-id="71eac-235">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="71eac-236">可配置的选项卡仅在团队范围内受支持，并且当前每个应用仅支持一个选项卡。</span><span class="sxs-lookup"><span data-stu-id="71eac-236">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="71eac-237">对象是包含类型 的所有元素的数组 `object` 。</span><span class="sxs-lookup"><span data-stu-id="71eac-237">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="71eac-238">只有提供可配置通道选项卡解决方案的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="71eac-238">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="71eac-239">名称</span><span class="sxs-lookup"><span data-stu-id="71eac-239">Name</span></span>| <span data-ttu-id="71eac-240">类型</span><span class="sxs-lookup"><span data-stu-id="71eac-240">Type</span></span>| <span data-ttu-id="71eac-241">最大大小</span><span class="sxs-lookup"><span data-stu-id="71eac-241">Maximum size</span></span> | <span data-ttu-id="71eac-242">必需</span><span class="sxs-lookup"><span data-stu-id="71eac-242">Required</span></span> | <span data-ttu-id="71eac-243">说明</span><span class="sxs-lookup"><span data-stu-id="71eac-243">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="71eac-244">String</span><span class="sxs-lookup"><span data-stu-id="71eac-244">String</span></span>|<span data-ttu-id="71eac-245">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-245">2048 characters</span></span>|<span data-ttu-id="71eac-246">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-246">✔</span></span>|<span data-ttu-id="71eac-247">配置 https:// 时将使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="71eac-247">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="71eac-248">Boolean</span><span class="sxs-lookup"><span data-stu-id="71eac-248">Boolean</span></span>|||<span data-ttu-id="71eac-249">一个值，指示用户创建后是否可以更新选项卡配置的实例。</span><span class="sxs-lookup"><span data-stu-id="71eac-249">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="71eac-250">默认值： `true`</span><span class="sxs-lookup"><span data-stu-id="71eac-250">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="71eac-251">枚举数组</span><span class="sxs-lookup"><span data-stu-id="71eac-251">Array of enum</span></span>|<span data-ttu-id="71eac-252">1</span><span class="sxs-lookup"><span data-stu-id="71eac-252">1</span></span>|<span data-ttu-id="71eac-253">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-253">✔</span></span>|<span data-ttu-id="71eac-254">目前，可配置的选项卡仅支持 `team` 和 `groupchat` 作用域。</span><span class="sxs-lookup"><span data-stu-id="71eac-254">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="71eac-255">String</span><span class="sxs-lookup"><span data-stu-id="71eac-255">String</span></span>|<span data-ttu-id="71eac-256">2048</span><span class="sxs-lookup"><span data-stu-id="71eac-256">2048</span></span>||<span data-ttu-id="71eac-257">选项卡预览图像的相对文件路径，用于SharePoint。</span><span class="sxs-lookup"><span data-stu-id="71eac-257">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="71eac-258">大小 1024x768。</span><span class="sxs-lookup"><span data-stu-id="71eac-258">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="71eac-259">枚举数组</span><span class="sxs-lookup"><span data-stu-id="71eac-259">Array of enum</span></span>|<span data-ttu-id="71eac-260">1</span><span class="sxs-lookup"><span data-stu-id="71eac-260">1</span></span>||<span data-ttu-id="71eac-261">定义选项卡在页面SharePoint。</span><span class="sxs-lookup"><span data-stu-id="71eac-261">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="71eac-262">选项为 `sharePointFullPage` 和 `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="71eac-262">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="71eac-263">staticTabs</span><span class="sxs-lookup"><span data-stu-id="71eac-263">staticTabs</span></span>

<span data-ttu-id="71eac-264">**可选**</span><span class="sxs-lookup"><span data-stu-id="71eac-264">**Optional**</span></span>

<span data-ttu-id="71eac-265">定义一组默认情况下可以"固定"的选项卡，而无需用户手动添加它们。</span><span class="sxs-lookup"><span data-stu-id="71eac-265">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="71eac-266">范围中声明 `personal` 的静态选项卡始终固定到应用的个人体验。</span><span class="sxs-lookup"><span data-stu-id="71eac-266">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="71eac-267">作用域中声明的 `team` 静态选项卡当前不受支持。</span><span class="sxs-lookup"><span data-stu-id="71eac-267">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="71eac-268">通过指定 而不是 在 staticTabs 块中呈现带自适应 `contentBotId` `contentUrl` **卡片的** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="71eac-268">Render tabs with Adaptive Cards by specifying `contentBotId` instead of `contentUrl` in the **staticTabs** block.</span></span>

<span data-ttu-id="71eac-269">对象是一个数组 (类型的所有元素) 最多包含 16 个元素 `object` 。</span><span class="sxs-lookup"><span data-stu-id="71eac-269">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="71eac-270">只有提供静态选项卡解决方案的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="71eac-270">This block is required only for solutions that provide a static tab solution.</span></span>


|<span data-ttu-id="71eac-271">名称</span><span class="sxs-lookup"><span data-stu-id="71eac-271">Name</span></span>| <span data-ttu-id="71eac-272">类型</span><span class="sxs-lookup"><span data-stu-id="71eac-272">Type</span></span>| <span data-ttu-id="71eac-273">最大大小</span><span class="sxs-lookup"><span data-stu-id="71eac-273">Maximum size</span></span> | <span data-ttu-id="71eac-274">必需</span><span class="sxs-lookup"><span data-stu-id="71eac-274">Required</span></span> | <span data-ttu-id="71eac-275">说明</span><span class="sxs-lookup"><span data-stu-id="71eac-275">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="71eac-276">字符串</span><span class="sxs-lookup"><span data-stu-id="71eac-276">String</span></span>|<span data-ttu-id="71eac-277">64 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-277">64 characters</span></span>|<span data-ttu-id="71eac-278">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-278">✔</span></span>|<span data-ttu-id="71eac-279">选项卡显示的实体的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="71eac-279">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="71eac-280">String</span><span class="sxs-lookup"><span data-stu-id="71eac-280">String</span></span>|<span data-ttu-id="71eac-281">128 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-281">128 characters</span></span>|<span data-ttu-id="71eac-282">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-282">✔</span></span>|<span data-ttu-id="71eac-283">选项卡显示名称界面中的列数。</span><span class="sxs-lookup"><span data-stu-id="71eac-283">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="71eac-284">String</span><span class="sxs-lookup"><span data-stu-id="71eac-284">String</span></span>|<span data-ttu-id="71eac-285">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-285">2048 characters</span></span>|<span data-ttu-id="71eac-286">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-286">✔</span></span>|<span data-ttu-id="71eac-287">指向要 https:// 画布中的实体 UI 的 Teams URL。</span><span class="sxs-lookup"><span data-stu-id="71eac-287">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`contentBotId`|   | | | <span data-ttu-id="71eac-288">自动Microsoft Teams门户中为自动程序指定的应用 ID。</span><span class="sxs-lookup"><span data-stu-id="71eac-288">The Microsoft Teams app ID specified for the bot in the Bot Framework portal.</span></span> |
|`websiteUrl`|<span data-ttu-id="71eac-289">String</span><span class="sxs-lookup"><span data-stu-id="71eac-289">String</span></span>|<span data-ttu-id="71eac-290">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-290">2048 characters</span></span>||<span data-ttu-id="71eac-291">用户 https:// 在浏览器中查看时指向的 URL。</span><span class="sxs-lookup"><span data-stu-id="71eac-291">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="71eac-292">枚举数组</span><span class="sxs-lookup"><span data-stu-id="71eac-292">Array of enum</span></span>|<span data-ttu-id="71eac-293">1</span><span class="sxs-lookup"><span data-stu-id="71eac-293">1</span></span>|<span data-ttu-id="71eac-294">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-294">✔</span></span>|<span data-ttu-id="71eac-295">目前，静态选项卡仅支持范围，这意味着只能将作用域预配 `personal` 为个人体验的一部分。</span><span class="sxs-lookup"><span data-stu-id="71eac-295">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="71eac-296">bots</span><span class="sxs-lookup"><span data-stu-id="71eac-296">bots</span></span>

<span data-ttu-id="71eac-297">**可选**</span><span class="sxs-lookup"><span data-stu-id="71eac-297">**Optional**</span></span>

<span data-ttu-id="71eac-298">定义自动程序解决方案以及默认命令属性等可选信息。</span><span class="sxs-lookup"><span data-stu-id="71eac-298">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="71eac-299">对象是一个 (，当前每个应用仅允许一个自动程序) 类型的所有元素 &mdash; `object` 。</span><span class="sxs-lookup"><span data-stu-id="71eac-299">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="71eac-300">只有提供自动程序体验的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="71eac-300">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="71eac-301">名称</span><span class="sxs-lookup"><span data-stu-id="71eac-301">Name</span></span>| <span data-ttu-id="71eac-302">类型</span><span class="sxs-lookup"><span data-stu-id="71eac-302">Type</span></span>| <span data-ttu-id="71eac-303">最大大小</span><span class="sxs-lookup"><span data-stu-id="71eac-303">Maximum size</span></span> | <span data-ttu-id="71eac-304">必需</span><span class="sxs-lookup"><span data-stu-id="71eac-304">Required</span></span> | <span data-ttu-id="71eac-305">说明</span><span class="sxs-lookup"><span data-stu-id="71eac-305">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="71eac-306">字符串</span><span class="sxs-lookup"><span data-stu-id="71eac-306">String</span></span>|<span data-ttu-id="71eac-307">64 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-307">64 characters</span></span>|<span data-ttu-id="71eac-308">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-308">✔</span></span>|<span data-ttu-id="71eac-309">使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="71eac-309">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="71eac-310">这可能与整个应用 [ID 相同](#id)。</span><span class="sxs-lookup"><span data-stu-id="71eac-310">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="71eac-311">布尔值</span><span class="sxs-lookup"><span data-stu-id="71eac-311">Boolean</span></span>|||<span data-ttu-id="71eac-312">描述自动程序是否利用用户提示将自动程序添加到特定频道。</span><span class="sxs-lookup"><span data-stu-id="71eac-312">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="71eac-313">默认值： `false`</span><span class="sxs-lookup"><span data-stu-id="71eac-313">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="71eac-314">布尔值</span><span class="sxs-lookup"><span data-stu-id="71eac-314">Boolean</span></span>|||<span data-ttu-id="71eac-315">指示自动程序是否为单向、仅通知的自动程序，而不是对话自动程序。</span><span class="sxs-lookup"><span data-stu-id="71eac-315">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="71eac-316">默认值： `false`</span><span class="sxs-lookup"><span data-stu-id="71eac-316">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="71eac-317">布尔值</span><span class="sxs-lookup"><span data-stu-id="71eac-317">Boolean</span></span>|||<span data-ttu-id="71eac-318">指示自动程序是否支持在个人聊天中上传/下载文件。</span><span class="sxs-lookup"><span data-stu-id="71eac-318">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="71eac-319">默认值： `false`</span><span class="sxs-lookup"><span data-stu-id="71eac-319">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="71eac-320">枚举数组</span><span class="sxs-lookup"><span data-stu-id="71eac-320">Array of enum</span></span>|<span data-ttu-id="71eac-321">3</span><span class="sxs-lookup"><span data-stu-id="71eac-321">3</span></span>|<span data-ttu-id="71eac-322">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-322">✔</span></span>|<span data-ttu-id="71eac-323">指定自动程序是在 `team` 内的频道上下文中提供体验、在群组聊天 (`groupchat`) 中提供体验，还是仅在单个用户 (`personal`) 范围内提供体验。</span><span class="sxs-lookup"><span data-stu-id="71eac-323">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="71eac-324">这些选项不具排他性。</span><span class="sxs-lookup"><span data-stu-id="71eac-324">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="71eac-325">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="71eac-325">bots.commandLists</span></span>

<span data-ttu-id="71eac-326">自动程序可以推荐给用户的命令的可选列表。</span><span class="sxs-lookup"><span data-stu-id="71eac-326">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="71eac-327">对象是一个 (，最多包含 2 个元素) 所有类型元素;您必须为自动程序支持的每个范围定义单独的 `object` 命令列表。</span><span class="sxs-lookup"><span data-stu-id="71eac-327">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="71eac-328">有关详细信息，请参阅自动 [程序菜单](~/bots/how-to/create-a-bot-commands-menu.md)。</span><span class="sxs-lookup"><span data-stu-id="71eac-328">For more information, see [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md).</span></span>

|<span data-ttu-id="71eac-329">名称</span><span class="sxs-lookup"><span data-stu-id="71eac-329">Name</span></span>| <span data-ttu-id="71eac-330">类型</span><span class="sxs-lookup"><span data-stu-id="71eac-330">Type</span></span>| <span data-ttu-id="71eac-331">最大大小</span><span class="sxs-lookup"><span data-stu-id="71eac-331">Maximum size</span></span> | <span data-ttu-id="71eac-332">必需</span><span class="sxs-lookup"><span data-stu-id="71eac-332">Required</span></span> | <span data-ttu-id="71eac-333">说明</span><span class="sxs-lookup"><span data-stu-id="71eac-333">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="71eac-334">枚举数组</span><span class="sxs-lookup"><span data-stu-id="71eac-334">array of enum</span></span>|<span data-ttu-id="71eac-335">3</span><span class="sxs-lookup"><span data-stu-id="71eac-335">3</span></span>|<span data-ttu-id="71eac-336">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-336">✔</span></span>|<span data-ttu-id="71eac-337">指定命令列表有效的作用域。</span><span class="sxs-lookup"><span data-stu-id="71eac-337">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="71eac-338">选项包括 `team`、`personal` 和 `groupchat`。</span><span class="sxs-lookup"><span data-stu-id="71eac-338">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="71eac-339">对象数组</span><span class="sxs-lookup"><span data-stu-id="71eac-339">array of objects</span></span>|<span data-ttu-id="71eac-340">10  </span><span class="sxs-lookup"><span data-stu-id="71eac-340">10</span></span>|<span data-ttu-id="71eac-341">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-341">✔</span></span>|<span data-ttu-id="71eac-342">自动程序支持的命令数组：</span><span class="sxs-lookup"><span data-stu-id="71eac-342">An array of commands the bot supports:</span></span><br><span data-ttu-id="71eac-343">`title`：自动程序命令名称 (字符串，32) 。</span><span class="sxs-lookup"><span data-stu-id="71eac-343">`title`: the bot command name (string, 32).</span></span><br><span data-ttu-id="71eac-344">`description`：命令语法及其参数的简单说明或示例， (字符串，128) 。</span><span class="sxs-lookup"><span data-stu-id="71eac-344">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

## <a name="connectors"></a><span data-ttu-id="71eac-345">连接器</span><span class="sxs-lookup"><span data-stu-id="71eac-345">connectors</span></span>

<span data-ttu-id="71eac-346">**可选**</span><span class="sxs-lookup"><span data-stu-id="71eac-346">**Optional**</span></span>

<span data-ttu-id="71eac-347">`connectors`块为应用Office 365连接器。</span><span class="sxs-lookup"><span data-stu-id="71eac-347">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="71eac-348">对象是一个数组， (类型的所有元素) 1 个元素 `object` 。</span><span class="sxs-lookup"><span data-stu-id="71eac-348">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="71eac-349">只有提供连接器的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="71eac-349">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="71eac-350">名称</span><span class="sxs-lookup"><span data-stu-id="71eac-350">Name</span></span>| <span data-ttu-id="71eac-351">类型</span><span class="sxs-lookup"><span data-stu-id="71eac-351">Type</span></span>| <span data-ttu-id="71eac-352">最大大小</span><span class="sxs-lookup"><span data-stu-id="71eac-352">Maximum size</span></span> | <span data-ttu-id="71eac-353">必需</span><span class="sxs-lookup"><span data-stu-id="71eac-353">Required</span></span> | <span data-ttu-id="71eac-354">说明</span><span class="sxs-lookup"><span data-stu-id="71eac-354">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="71eac-355">String</span><span class="sxs-lookup"><span data-stu-id="71eac-355">String</span></span>|<span data-ttu-id="71eac-356">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-356">2048 characters</span></span>|<span data-ttu-id="71eac-357">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-357">✔</span></span>|<span data-ttu-id="71eac-358">配置 https:// 时将使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="71eac-358">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="71eac-359">字符串</span><span class="sxs-lookup"><span data-stu-id="71eac-359">String</span></span>|<span data-ttu-id="71eac-360">64 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-360">64 characters</span></span>|<span data-ttu-id="71eac-361">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-361">✔</span></span>|<span data-ttu-id="71eac-362">连接器的唯一标识符，与连接器开发人员仪表板中的 ID [相匹配](https://aka.ms/connectorsdashboard)。</span><span class="sxs-lookup"><span data-stu-id="71eac-362">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="71eac-363">枚举数组</span><span class="sxs-lookup"><span data-stu-id="71eac-363">Array of enum</span></span>|<span data-ttu-id="71eac-364">1</span><span class="sxs-lookup"><span data-stu-id="71eac-364">1</span></span>|<span data-ttu-id="71eac-365">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-365">✔</span></span>|<span data-ttu-id="71eac-366">指定连接器是提供在 中频道上下文中的体验，还是仅针对单个用户 `team` `personal` () 。</span><span class="sxs-lookup"><span data-stu-id="71eac-366">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="71eac-367">目前，仅 `team` 支持范围。</span><span class="sxs-lookup"><span data-stu-id="71eac-367">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="71eac-368">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="71eac-368">composeExtensions</span></span>

<span data-ttu-id="71eac-369">**可选**</span><span class="sxs-lookup"><span data-stu-id="71eac-369">**Optional**</span></span>

<span data-ttu-id="71eac-370">为应用定义消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="71eac-370">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="71eac-371">2017 年 11 月，功能名称从"撰写扩展"更改为"邮件扩展"，但清单名称保持不变，以便现有扩展继续工作。</span><span class="sxs-lookup"><span data-stu-id="71eac-371">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="71eac-372">对象是一个数组， (类型的所有元素) 1 个元素 `object` 。</span><span class="sxs-lookup"><span data-stu-id="71eac-372">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="71eac-373">只有提供邮件扩展的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="71eac-373">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="71eac-374">名称</span><span class="sxs-lookup"><span data-stu-id="71eac-374">Name</span></span>| <span data-ttu-id="71eac-375">类型</span><span class="sxs-lookup"><span data-stu-id="71eac-375">Type</span></span> | <span data-ttu-id="71eac-376">最大大小</span><span class="sxs-lookup"><span data-stu-id="71eac-376">Maximum Size</span></span> | <span data-ttu-id="71eac-377">必需</span><span class="sxs-lookup"><span data-stu-id="71eac-377">Required</span></span> | <span data-ttu-id="71eac-378">说明</span><span class="sxs-lookup"><span data-stu-id="71eac-378">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="71eac-379">String</span><span class="sxs-lookup"><span data-stu-id="71eac-379">String</span></span>|<span data-ttu-id="71eac-380">64</span><span class="sxs-lookup"><span data-stu-id="71eac-380">64</span></span>|<span data-ttu-id="71eac-381">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-381">✔</span></span>|<span data-ttu-id="71eac-382">自动程序支持消息传递扩展的唯一 Microsoft 应用 ID，在 Bot Framework 中注册。</span><span class="sxs-lookup"><span data-stu-id="71eac-382">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="71eac-383">这可能与整个应用 [ID 相同](#id)。</span><span class="sxs-lookup"><span data-stu-id="71eac-383">This may well be the same as the overall [app ID](#id).</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="71eac-384">Boolean</span><span class="sxs-lookup"><span data-stu-id="71eac-384">Boolean</span></span>|||<span data-ttu-id="71eac-385">一个值，指示用户是否可以更新邮件扩展的配置。</span><span class="sxs-lookup"><span data-stu-id="71eac-385">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="71eac-386">默认值为 `false`。</span><span class="sxs-lookup"><span data-stu-id="71eac-386">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="71eac-387">对象数组</span><span class="sxs-lookup"><span data-stu-id="71eac-387">Array of object</span></span>|<span data-ttu-id="71eac-388">10  </span><span class="sxs-lookup"><span data-stu-id="71eac-388">10</span></span>|<span data-ttu-id="71eac-389">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-389">✔</span></span>|<span data-ttu-id="71eac-390">邮件扩展支持的命令数组</span><span class="sxs-lookup"><span data-stu-id="71eac-390">Array of commands the messaging extension supports</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="71eac-391">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="71eac-391">composeExtensions.commands</span></span>

<span data-ttu-id="71eac-392">邮件扩展应声明一个或多个命令。</span><span class="sxs-lookup"><span data-stu-id="71eac-392">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="71eac-393">每个命令都Microsoft Teams UI 入口点的潜在交互。</span><span class="sxs-lookup"><span data-stu-id="71eac-393">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="71eac-394">最多有 10 个命令。</span><span class="sxs-lookup"><span data-stu-id="71eac-394">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="71eac-395">每个命令项都是具有以下结构的对象：</span><span class="sxs-lookup"><span data-stu-id="71eac-395">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="71eac-396">名称</span><span class="sxs-lookup"><span data-stu-id="71eac-396">Name</span></span>| <span data-ttu-id="71eac-397">类型</span><span class="sxs-lookup"><span data-stu-id="71eac-397">Type</span></span>| <span data-ttu-id="71eac-398">最大大小</span><span class="sxs-lookup"><span data-stu-id="71eac-398">Maximum size</span></span> | <span data-ttu-id="71eac-399">必需</span><span class="sxs-lookup"><span data-stu-id="71eac-399">Required</span></span> | <span data-ttu-id="71eac-400">说明</span><span class="sxs-lookup"><span data-stu-id="71eac-400">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="71eac-401">字符串</span><span class="sxs-lookup"><span data-stu-id="71eac-401">String</span></span>|<span data-ttu-id="71eac-402">64 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-402">64 characters</span></span>|<span data-ttu-id="71eac-403">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-403">✔</span></span>|<span data-ttu-id="71eac-404">命令的 ID。</span><span class="sxs-lookup"><span data-stu-id="71eac-404">The ID for the command.</span></span>|
|`type`|<span data-ttu-id="71eac-405">字符串</span><span class="sxs-lookup"><span data-stu-id="71eac-405">String</span></span>|<span data-ttu-id="71eac-406">64 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-406">64 characters</span></span>||<span data-ttu-id="71eac-407">命令的类型。</span><span class="sxs-lookup"><span data-stu-id="71eac-407">Type of the command.</span></span> <span data-ttu-id="71eac-408">或 `query` `action` 之一。</span><span class="sxs-lookup"><span data-stu-id="71eac-408">One of `query` or `action`.</span></span> <span data-ttu-id="71eac-409">默认值： `query`</span><span class="sxs-lookup"><span data-stu-id="71eac-409">Default: `query`</span></span>|
|`title`|<span data-ttu-id="71eac-410">String</span><span class="sxs-lookup"><span data-stu-id="71eac-410">String</span></span>|<span data-ttu-id="71eac-411">32 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-411">32 characters</span></span>|<span data-ttu-id="71eac-412">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-412">✔</span></span>|<span data-ttu-id="71eac-413">用户友好命令名称。</span><span class="sxs-lookup"><span data-stu-id="71eac-413">The user-friendly command name.</span></span>|
|`description`|<span data-ttu-id="71eac-414">String</span><span class="sxs-lookup"><span data-stu-id="71eac-414">String</span></span>|<span data-ttu-id="71eac-415">128 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-415">128 characters</span></span>||<span data-ttu-id="71eac-416">向用户显示以指示此命令用途的说明。</span><span class="sxs-lookup"><span data-stu-id="71eac-416">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="71eac-417">Boolean</span><span class="sxs-lookup"><span data-stu-id="71eac-417">Boolean</span></span>|||<span data-ttu-id="71eac-418">一个布尔值，指示命令最初是否应该没有参数运行。</span><span class="sxs-lookup"><span data-stu-id="71eac-418">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="71eac-419">默认值： `false`</span><span class="sxs-lookup"><span data-stu-id="71eac-419">Default: `false`</span></span>|
|`context`|<span data-ttu-id="71eac-420">Array of Strings</span><span class="sxs-lookup"><span data-stu-id="71eac-420">Array of Strings</span></span>|<span data-ttu-id="71eac-421">3</span><span class="sxs-lookup"><span data-stu-id="71eac-421">3</span></span>||<span data-ttu-id="71eac-422">定义可以从何处调用邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="71eac-422">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="71eac-423">、 `compose` 、 的任意 `commandBox` 组合 `message` 。</span><span class="sxs-lookup"><span data-stu-id="71eac-423">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="71eac-424">默认值为 `["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="71eac-424">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="71eac-425">Boolean</span><span class="sxs-lookup"><span data-stu-id="71eac-425">Boolean</span></span>|||<span data-ttu-id="71eac-426">一个布尔值，指示它应动态提取任务模块。</span><span class="sxs-lookup"><span data-stu-id="71eac-426">A boolean value that indicates if it should fetch the task module dynamically.</span></span>|
|`taskInfo`|<span data-ttu-id="71eac-427">对象</span><span class="sxs-lookup"><span data-stu-id="71eac-427">Object</span></span>|||<span data-ttu-id="71eac-428">指定在使用消息传递扩展命令时要预加载的任务模块。</span><span class="sxs-lookup"><span data-stu-id="71eac-428">Specify the task module to preload when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="71eac-429">String</span><span class="sxs-lookup"><span data-stu-id="71eac-429">String</span></span>|<span data-ttu-id="71eac-430">64</span><span class="sxs-lookup"><span data-stu-id="71eac-430">64</span></span>||<span data-ttu-id="71eac-431">初始对话框标题。</span><span class="sxs-lookup"><span data-stu-id="71eac-431">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="71eac-432">String</span><span class="sxs-lookup"><span data-stu-id="71eac-432">String</span></span>|||<span data-ttu-id="71eac-433">对话框宽度 - 以像素为单位的一个数字或默认布局，例如"large"、"medium"或"small"。</span><span class="sxs-lookup"><span data-stu-id="71eac-433">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="71eac-434">String</span><span class="sxs-lookup"><span data-stu-id="71eac-434">String</span></span>|||<span data-ttu-id="71eac-435">对话框高度 - 以像素为单位的一个数字或默认布局，例如"large"、"medium"或"small"。</span><span class="sxs-lookup"><span data-stu-id="71eac-435">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="71eac-436">String</span><span class="sxs-lookup"><span data-stu-id="71eac-436">String</span></span>|||<span data-ttu-id="71eac-437">初始 Web 视图 URL。</span><span class="sxs-lookup"><span data-stu-id="71eac-437">Initial webview URL.</span></span>|
|`messageHandlers`|<span data-ttu-id="71eac-438">对象数组</span><span class="sxs-lookup"><span data-stu-id="71eac-438">Array of Objects</span></span>|<span data-ttu-id="71eac-439">5 </span><span class="sxs-lookup"><span data-stu-id="71eac-439">5</span></span>||<span data-ttu-id="71eac-440">允许满足某些条件时调用应用的处理程序列表。</span><span class="sxs-lookup"><span data-stu-id="71eac-440">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="71eac-441">还必须在 中列出域 `validDomains` 。</span><span class="sxs-lookup"><span data-stu-id="71eac-441">Domains must also be listed in `validDomains`.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="71eac-442">String</span><span class="sxs-lookup"><span data-stu-id="71eac-442">String</span></span>|||<span data-ttu-id="71eac-443">消息处理程序的类型。</span><span class="sxs-lookup"><span data-stu-id="71eac-443">The type of message handler.</span></span> <span data-ttu-id="71eac-444">必须是 `"link"`。</span><span class="sxs-lookup"><span data-stu-id="71eac-444">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="71eac-445">Array of Strings</span><span class="sxs-lookup"><span data-stu-id="71eac-445">Array of Strings</span></span>|||<span data-ttu-id="71eac-446">链接邮件处理程序可以注册的域数组。</span><span class="sxs-lookup"><span data-stu-id="71eac-446">Array of domains that the link message handler can register for.</span></span>|
|`parameters`|<span data-ttu-id="71eac-447">对象数组</span><span class="sxs-lookup"><span data-stu-id="71eac-447">Array of object</span></span>|<span data-ttu-id="71eac-448">5 </span><span class="sxs-lookup"><span data-stu-id="71eac-448">5</span></span>|<span data-ttu-id="71eac-449">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-449">✔</span></span>|<span data-ttu-id="71eac-450">命令采用的参数列表。</span><span class="sxs-lookup"><span data-stu-id="71eac-450">The list of parameters the command takes.</span></span> <span data-ttu-id="71eac-451">最小值：1;最大值：5</span><span class="sxs-lookup"><span data-stu-id="71eac-451">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="71eac-452">字符串</span><span class="sxs-lookup"><span data-stu-id="71eac-452">String</span></span>|<span data-ttu-id="71eac-453">64 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-453">64 characters</span></span>|<span data-ttu-id="71eac-454">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-454">✔</span></span>|<span data-ttu-id="71eac-455">显示在客户端中的参数的名称。</span><span class="sxs-lookup"><span data-stu-id="71eac-455">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="71eac-456">这包括在用户请求中。</span><span class="sxs-lookup"><span data-stu-id="71eac-456">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="71eac-457">String</span><span class="sxs-lookup"><span data-stu-id="71eac-457">String</span></span>|<span data-ttu-id="71eac-458">32 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-458">32 characters</span></span>|<span data-ttu-id="71eac-459">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-459">✔</span></span>|<span data-ttu-id="71eac-460">参数的用户友好标题。</span><span class="sxs-lookup"><span data-stu-id="71eac-460">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="71eac-461">String</span><span class="sxs-lookup"><span data-stu-id="71eac-461">String</span></span>|<span data-ttu-id="71eac-462">128 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-462">128 characters</span></span>||<span data-ttu-id="71eac-463">描述此参数用途的用户友好字符串。</span><span class="sxs-lookup"><span data-stu-id="71eac-463">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="71eac-464">String</span><span class="sxs-lookup"><span data-stu-id="71eac-464">String</span></span>|<span data-ttu-id="71eac-465">128 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-465">128 characters</span></span>||<span data-ttu-id="71eac-466">定义在任务模块上显示的控件的类型 `fetchTask: true` 。</span><span class="sxs-lookup"><span data-stu-id="71eac-466">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="71eac-467">`text` `textarea` `number` `date` `time` 、、、、、、、 `toggle` 之一 `choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="71eac-467">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`.</span></span>|
|`parameter.choices`|<span data-ttu-id="71eac-468">对象数组</span><span class="sxs-lookup"><span data-stu-id="71eac-468">Array of Objects</span></span>|<span data-ttu-id="71eac-469">10  </span><span class="sxs-lookup"><span data-stu-id="71eac-469">10</span></span>||<span data-ttu-id="71eac-470">的选项 `choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="71eac-470">The choice options for the `choiceset`.</span></span> <span data-ttu-id="71eac-471">仅在 为 `parameter.inputType` `choiceset` 时使用 。</span><span class="sxs-lookup"><span data-stu-id="71eac-471">Use only when `parameter.inputType` is `choiceset`.</span></span>|
|`parameter.choices.title`|<span data-ttu-id="71eac-472">String</span><span class="sxs-lookup"><span data-stu-id="71eac-472">String</span></span>|<span data-ttu-id="71eac-473">128</span><span class="sxs-lookup"><span data-stu-id="71eac-473">128</span></span>||<span data-ttu-id="71eac-474">选项的标题。</span><span class="sxs-lookup"><span data-stu-id="71eac-474">Title of the choice.</span></span>|
|`parameter.choices.value`|<span data-ttu-id="71eac-475">String</span><span class="sxs-lookup"><span data-stu-id="71eac-475">String</span></span>|<span data-ttu-id="71eac-476">512</span><span class="sxs-lookup"><span data-stu-id="71eac-476">512</span></span>||<span data-ttu-id="71eac-477">选项的值。</span><span class="sxs-lookup"><span data-stu-id="71eac-477">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="71eac-478">权限</span><span class="sxs-lookup"><span data-stu-id="71eac-478">permissions</span></span>

<span data-ttu-id="71eac-479">**可选**</span><span class="sxs-lookup"><span data-stu-id="71eac-479">**Optional**</span></span>

<span data-ttu-id="71eac-480">一个数组，指定应用请求哪些权限，让最终用户 `string` 知道扩展将执行什么操作。</span><span class="sxs-lookup"><span data-stu-id="71eac-480">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="71eac-481">以下选项非独占：</span><span class="sxs-lookup"><span data-stu-id="71eac-481">The following options are non-exclusive:</span></span>

* <span data-ttu-id="71eac-482">`identity`&emsp;需要用户标识信息。</span><span class="sxs-lookup"><span data-stu-id="71eac-482">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="71eac-483">`messageTeamMembers`&emsp;需要向团队成员发送直接消息的权限。</span><span class="sxs-lookup"><span data-stu-id="71eac-483">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="71eac-484">在更新应用时更改这些权限将导致用户在首次运行更新后的应用时重复同意过程。</span><span class="sxs-lookup"><span data-stu-id="71eac-484">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="71eac-485">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="71eac-485">devicePermissions</span></span>

<span data-ttu-id="71eac-486">**可选** 字符串数组</span><span class="sxs-lookup"><span data-stu-id="71eac-486">**Optional** Array of Strings</span></span>

<span data-ttu-id="71eac-487">指定应用可能请求访问的用户设备上本机功能。</span><span class="sxs-lookup"><span data-stu-id="71eac-487">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="71eac-488">选项有：</span><span class="sxs-lookup"><span data-stu-id="71eac-488">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="71eac-489">validDomains</span><span class="sxs-lookup"><span data-stu-id="71eac-489">validDomains</span></span>

<span data-ttu-id="71eac-490">**可选**，但 **已指出的必需** 项除外</span><span class="sxs-lookup"><span data-stu-id="71eac-490">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="71eac-491">应用预期从其中加载任何内容的有效域的列表。</span><span class="sxs-lookup"><span data-stu-id="71eac-491">A list of valid domains from which the app expects to load any content.</span></span> <span data-ttu-id="71eac-492">域列表可以包含通配符，例如 `*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="71eac-492">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="71eac-493">这完全匹配域的一个段;如果需要匹配，请使用 `a.b.example.com` `*.*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="71eac-493">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="71eac-494">如果你的选项卡配置或内容 UI 需要导航到除用于选项卡配置的其他任何其他域，则必须在此处指定该域。</span><span class="sxs-lookup"><span data-stu-id="71eac-494">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="71eac-495">但是 **，** 不需要在应用中包含要支持的标识提供程序的域。</span><span class="sxs-lookup"><span data-stu-id="71eac-495">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="71eac-496">例如，若要使用 Google ID 进行身份验证，必须重定向到 accounts.google.com，但不应将 accounts.google.com 包括在 `validDomains[]` 中。</span><span class="sxs-lookup"><span data-stu-id="71eac-496">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="71eac-497">不要直接或通过通配符添加超出你控制的域。</span><span class="sxs-lookup"><span data-stu-id="71eac-497">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="71eac-498">例如， `yourapp.onmicrosoft.com` 有效，但 `*.onmicrosoft.com` 无效。</span><span class="sxs-lookup"><span data-stu-id="71eac-498">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="71eac-499">对象是包含类型 的所有元素的数组 `string` 。</span><span class="sxs-lookup"><span data-stu-id="71eac-499">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="71eac-500">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="71eac-500">webApplicationInfo</span></span>

<span data-ttu-id="71eac-501">**可选**</span><span class="sxs-lookup"><span data-stu-id="71eac-501">**Optional**</span></span>

<span data-ttu-id="71eac-502">指定 AAD 应用 ID 和Graph信息以帮助用户无缝登录到 AAD 应用。</span><span class="sxs-lookup"><span data-stu-id="71eac-502">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="71eac-503">名称</span><span class="sxs-lookup"><span data-stu-id="71eac-503">Name</span></span>| <span data-ttu-id="71eac-504">类型</span><span class="sxs-lookup"><span data-stu-id="71eac-504">Type</span></span>| <span data-ttu-id="71eac-505">最大大小</span><span class="sxs-lookup"><span data-stu-id="71eac-505">Maximum size</span></span> | <span data-ttu-id="71eac-506">必需</span><span class="sxs-lookup"><span data-stu-id="71eac-506">Required</span></span> | <span data-ttu-id="71eac-507">说明</span><span class="sxs-lookup"><span data-stu-id="71eac-507">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="71eac-508">String</span><span class="sxs-lookup"><span data-stu-id="71eac-508">String</span></span>|<span data-ttu-id="71eac-509">36 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-509">36 characters</span></span>|<span data-ttu-id="71eac-510">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-510">✔</span></span>|<span data-ttu-id="71eac-511">应用的 AAD 应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="71eac-511">AAD application id of the app.</span></span> <span data-ttu-id="71eac-512">此 ID 必须是 GUID。</span><span class="sxs-lookup"><span data-stu-id="71eac-512">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="71eac-513">String</span><span class="sxs-lookup"><span data-stu-id="71eac-513">String</span></span>|<span data-ttu-id="71eac-514">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="71eac-514">2048 characters</span></span>|<span data-ttu-id="71eac-515">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-515">✔</span></span>|<span data-ttu-id="71eac-516">用于获取 SSO 身份验证令牌的应用的资源 URL。</span><span class="sxs-lookup"><span data-stu-id="71eac-516">Resource url of app for acquiring auth token for SSO.</span></span>|
|`applicationPermissions`|<span data-ttu-id="71eac-517">数组</span><span class="sxs-lookup"><span data-stu-id="71eac-517">Array</span></span>|<span data-ttu-id="71eac-518">最多 100 个项目</span><span class="sxs-lookup"><span data-stu-id="71eac-518">Maximum 100 items</span></span>|<span data-ttu-id="71eac-519">✔</span><span class="sxs-lookup"><span data-stu-id="71eac-519">✔</span></span>|<span data-ttu-id="71eac-520">应用程序的资源权限。</span><span class="sxs-lookup"><span data-stu-id="71eac-520">Resource permissions for application.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="71eac-521">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="71eac-521">configurableProperties</span></span>

<span data-ttu-id="71eac-522">**可选** - 数组</span><span class="sxs-lookup"><span data-stu-id="71eac-522">**Optional** - array</span></span>

<span data-ttu-id="71eac-523">`configurableProperties`此块定义管理员可Teams的应用程序属性。</span><span class="sxs-lookup"><span data-stu-id="71eac-523">The `configurableProperties` block defines the app properties that Teams admins can customize.</span></span> <span data-ttu-id="71eac-524">有关详细信息，请参阅启用 [应用自定义](~/concepts/design/enable-app-customization.md)。</span><span class="sxs-lookup"><span data-stu-id="71eac-524">For more information, see [enable app customization](~/concepts/design/enable-app-customization.md).</span></span>

> [!NOTE]
> <span data-ttu-id="71eac-525">必须定义至少一个属性。</span><span class="sxs-lookup"><span data-stu-id="71eac-525">A minimum of one property must be defined.</span></span> <span data-ttu-id="71eac-526">最多可以在此块中定义九个属性。</span><span class="sxs-lookup"><span data-stu-id="71eac-526">You can define a maximum of nine properties in this block.</span></span>

<span data-ttu-id="71eac-527">可以定义以下任一属性：</span><span class="sxs-lookup"><span data-stu-id="71eac-527">You can define any of the following properties:</span></span>

* <span data-ttu-id="71eac-528">`name`：应用显示名称。</span><span class="sxs-lookup"><span data-stu-id="71eac-528">`name`: The app's display name.</span></span>
* <span data-ttu-id="71eac-529">`shortDescription`：应用的简短说明。</span><span class="sxs-lookup"><span data-stu-id="71eac-529">`shortDescription`: The app's short description.</span></span>
* <span data-ttu-id="71eac-530">`longDescription`：应用的详细说明。</span><span class="sxs-lookup"><span data-stu-id="71eac-530">`longDescription`: The app's detailed description.</span></span>
* <span data-ttu-id="71eac-531">`smallImageUrl`：应用的大纲图标。</span><span class="sxs-lookup"><span data-stu-id="71eac-531">`smallImageUrl`: The app's outline icon.</span></span>
* <span data-ttu-id="71eac-532">`largeImageUrl`：应用的颜色图标。</span><span class="sxs-lookup"><span data-stu-id="71eac-532">`largeImageUrl`: The app's color icon.</span></span>
* <span data-ttu-id="71eac-533">`accentColor`：要与 和 结合使用用作大纲图标背景的颜色。</span><span class="sxs-lookup"><span data-stu-id="71eac-533">`accentColor`: The color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="71eac-534">`developerUrl`：开发人员网站的 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="71eac-534">`developerUrl`: The HTTPS URL of the developer's website.</span></span>
* <span data-ttu-id="71eac-535">`privacyUrl`：开发人员隐私策略的 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="71eac-535">`privacyUrl`: The HTTPS URL of the developer's privacy policy.</span></span>
* <span data-ttu-id="71eac-536">`termsOfUseUrl`：开发人员使用条款的 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="71eac-536">`termsOfUseUrl`: The HTTPS URL of the developer's terms of use.</span></span>

## <a name="defaultinstallscope"></a><span data-ttu-id="71eac-537">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="71eac-537">defaultInstallScope</span></span>

<span data-ttu-id="71eac-538">**可选** - string</span><span class="sxs-lookup"><span data-stu-id="71eac-538">**Optional** - string</span></span>

<span data-ttu-id="71eac-539">指定默认情况下为此应用定义的安装范围。</span><span class="sxs-lookup"><span data-stu-id="71eac-539">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="71eac-540">定义的范围将是当用户尝试添加应用时按钮上显示的选项。</span><span class="sxs-lookup"><span data-stu-id="71eac-540">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="71eac-541">选项有：</span><span class="sxs-lookup"><span data-stu-id="71eac-541">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="71eac-542">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="71eac-542">defaultGroupCapability</span></span>

<span data-ttu-id="71eac-543">**可选** - object</span><span class="sxs-lookup"><span data-stu-id="71eac-543">**Optional** - object</span></span>

<span data-ttu-id="71eac-544">选择组安装范围后，它将在用户安装应用时定义默认功能。</span><span class="sxs-lookup"><span data-stu-id="71eac-544">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="71eac-545">选项有：</span><span class="sxs-lookup"><span data-stu-id="71eac-545">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="71eac-546">名称</span><span class="sxs-lookup"><span data-stu-id="71eac-546">Name</span></span>| <span data-ttu-id="71eac-547">类型</span><span class="sxs-lookup"><span data-stu-id="71eac-547">Type</span></span>| <span data-ttu-id="71eac-548">最大大小</span><span class="sxs-lookup"><span data-stu-id="71eac-548">Maximum size</span></span> | <span data-ttu-id="71eac-549">必需</span><span class="sxs-lookup"><span data-stu-id="71eac-549">Required</span></span> | <span data-ttu-id="71eac-550">说明</span><span class="sxs-lookup"><span data-stu-id="71eac-550">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="71eac-551">string</span><span class="sxs-lookup"><span data-stu-id="71eac-551">string</span></span>|||<span data-ttu-id="71eac-552">当选择的安装范围为 `team` 时，此字段指定可用的默认功能。</span><span class="sxs-lookup"><span data-stu-id="71eac-552">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="71eac-553">选项 `tab` ：、 `bot` 或 `connector` 。</span><span class="sxs-lookup"><span data-stu-id="71eac-553">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="71eac-554">string</span><span class="sxs-lookup"><span data-stu-id="71eac-554">string</span></span>|||<span data-ttu-id="71eac-555">当选择的安装范围为 `groupchat` 时，此字段指定可用的默认功能。</span><span class="sxs-lookup"><span data-stu-id="71eac-555">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="71eac-556">选项 `tab` ：、 `bot` 或 `connector` 。</span><span class="sxs-lookup"><span data-stu-id="71eac-556">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="71eac-557">string</span><span class="sxs-lookup"><span data-stu-id="71eac-557">string</span></span>|||<span data-ttu-id="71eac-558">当选择的安装范围为 `meetings` 时，此字段指定可用的默认功能。</span><span class="sxs-lookup"><span data-stu-id="71eac-558">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="71eac-559">选项 `tab` ：、 `bot` 或 `connector` 。</span><span class="sxs-lookup"><span data-stu-id="71eac-559">Options: `tab`, `bot`, or `connector`.</span></span>|
