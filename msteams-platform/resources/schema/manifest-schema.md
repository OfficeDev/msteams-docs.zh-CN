---
title: 清单架构参考
description: 描述列表的清单Microsoft Teams
ms.topic: reference
ms.author: lajanuar
localization_priority: Normal
keywords: teams 清单架构
ms.openlocfilehash: eeffd97c5cbe62b66cab343bfe650b7f617ce9f2
ms.sourcegitcommit: 808a203fb963eeade3a8e32db88d64677e37df7a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2021
ms.locfileid: "52304010"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="4d353-104">参考：Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="4d353-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="4d353-105">Teams清单介绍了应用如何集成到 Microsoft Teams 产品。</span><span class="sxs-lookup"><span data-stu-id="4d353-105">The Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="4d353-106">清单必须符合 托管在 的架构 [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json) 。</span><span class="sxs-lookup"><span data-stu-id="4d353-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="4d353-107">早期版本 1.0-1.4 也受 URL ("v1.x") 。</span><span class="sxs-lookup"><span data-stu-id="4d353-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="4d353-108">以下架构示例显示了所有扩展性选项。</span><span class="sxs-lookup"><span data-stu-id="4d353-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="4d353-109">示例完整清单</span><span class="sxs-lookup"><span data-stu-id="4d353-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json",
  "manifestVersion": "1.10",
  "version": "1.0.0",
  "id": "%MICROSOFT-APP-ID%",
  "packageName": "com.example.myapp",
  "localizationInfo": {
    "defaultLanguageTag": "en-us",
    "additionalLanguages": [
      {
        "languageTag": "es-es",
        "file": "en-us.json"
      }
    ]
  },
  "developer": {
    "name": "Publisher Name",
    "websiteUrl": "https://website.com/",
    "privacyUrl": "https://website.com/privacy",
    "termsOfUseUrl": "https://website.com/app-tos",
    "mpnId": "1234567890"
  },
  "name": {
    "short": "Name of your app (<=30 chars)",
    "full": "Full name of app, if longer than 30 characters (<=100 chars)"
  },
  "description": {
    "short": "Short description of your app (<= 80 chars)",
    "full": "Full description of your app (<= 4000 chars)"
  },
  "icons": {
    "outline": "A relative path to a transparent .png icon — 32px X 32px",
    "color": "A relative path to a full color .png icon — 192px X 192px"
  },
  "accentColor": "A valid HTML color code.",
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "scopes": [
        "team",
        "groupchat"
      ],
      "canUpdateConfiguration": true,
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel",
        "meetingStage"
      ],
      "sharePointPreviewImage": "Relative path to a tab preview image for use in SharePoint — 1024px X 768",
      "supportedSharePointHosts": [
         "sharePointFullPage",
         "sharePointWebPart"
      ]
    }
  ],
  "staticTabs": [
    {
      "entityId": "unique Id for the page entity",
      "scopes": [
        "personal"
      ],
      "context":[
        "personalTab",
        "channelTab"
        ],
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content (displayed in Teams canvas)",
      "websiteUrl": "https://contoso.com/content (displayed in web browser)",
       "searchUrl":  "https://contoso.com/content (displayed in web browser)"
    }
  ],
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "scopes": [
        "team",
        "personal",
        "groupchat"
      ],
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "supportsFiles": true,
      "supportsCalling": false,
      "supportsVideo": true,
      "commandLists": [
        {
          "scopes": [
            "team",
            "groupchat"
          ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command 2",
              "description": "Description of Command 2"
            }
          ]
        },
        {
          "scopes": [
            "personal",
            "groupchat"
          ],
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
      "scopes": [
        "team"
      ],
      "configurationUrl": "https://contoso.com/teamsconnector/configure"
    }
  ],
  "composeExtensions": [
    {
      "canUpdateConfiguration": true,
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "commands": [
        {
          "id": "exampleCmd1",
          "title": "Example Command",
          "type": "query",
          "context": [
            "compose",
            "commandBox"
          ],
          "description": "Command Description; e.g., Search on the web",
          "initialRun": true,
          "fetchTask": false,
          "parameters": [
            {
              "name": "keyword",
              "title": "Search keywords",
              "inputType": "text",
              "description": "Enter the keywords to search for",
              "value": "Initial value for the parameter",
              "choices": [
                {
                  "title": "Title of the choice",
                  "value": "Value of the choice"
                }
              ]
            }
          ]
        },
        {
          "id": "exampleCmd2",
          "title": "Example Command 2",
          "type": "action",
          "context": [
            "message"
          ],
          "description": "Command Description; e.g., Search for a customer",
          "initialRun": true,
          "fetchTask": true,
          "parameters": [
            {
              "name": "custinfo",
              "title": "Customer name",
              "description": "Enter a customer name",
              "inputType": "text"
            }
          ]
        }
      ],
      "taskInfo": {
        "title": "Initial dialog title",
        "width": "Dialog width",
        "height": "Dialog height",
        "url": "Initial webview URL"
      },
      "messageHandlers": [
        {
          "type": "link",
          "value": {
            "domains": [
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
  "devicePermissions": [
    "geolocation",
    "media",
    "notifications",
    "midi",
    "openExternal"
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
  "showLoadingIndicator": false,
  "isFullScreen": false,
  "activities": {
    "activityTypes": [
      {
        "type": "taskCreated",
        "description": "Task created activity",
        "templateText": "<team member> created task <taskId> for you"
      },
      {
        "type": "userMention",
        "description": "Personal mention activity",
        "templateText": "<team member> mentioned you"
      }
    ]
  },
  "defaultInstallScope": "meetings",
  "defaultGroupCapability": {
    "meetings": "tab", 
    "team": "bot", 
    "groupchat": "bot"
  },
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
  ]              
}
```

<span data-ttu-id="4d353-110">该架构定义以下属性：</span><span class="sxs-lookup"><span data-stu-id="4d353-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="4d353-111">$schema</span><span class="sxs-lookup"><span data-stu-id="4d353-111">$schema</span></span>

<span data-ttu-id="4d353-112">可选，但推荐 — 字符串</span><span class="sxs-lookup"><span data-stu-id="4d353-112">Optional, but recommended — string</span></span>

<span data-ttu-id="4d353-113">引用 https:// JSON 架构的 URL。</span><span class="sxs-lookup"><span data-stu-id="4d353-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="4d353-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="4d353-114">manifestVersion</span></span>

<span data-ttu-id="4d353-115">**必需** — 字符串</span><span class="sxs-lookup"><span data-stu-id="4d353-115">**Required** — string</span></span>

<span data-ttu-id="4d353-116">此清单使用的清单架构版本。</span><span class="sxs-lookup"><span data-stu-id="4d353-116">The version of manifest schema this manifest is using.</span></span> <span data-ttu-id="4d353-117">必须为 1.10。</span><span class="sxs-lookup"><span data-stu-id="4d353-117">It must be 1.10.</span></span>

## <a name="version"></a><span data-ttu-id="4d353-118">version</span><span class="sxs-lookup"><span data-stu-id="4d353-118">version</span></span>

<span data-ttu-id="4d353-119">**必需** — 字符串</span><span class="sxs-lookup"><span data-stu-id="4d353-119">**Required** — string</span></span>

<span data-ttu-id="4d353-120">特定应用的版本。</span><span class="sxs-lookup"><span data-stu-id="4d353-120">The version of a specific app.</span></span> <span data-ttu-id="4d353-121">如果更新清单中的某些内容，则版本也必须递增。</span><span class="sxs-lookup"><span data-stu-id="4d353-121">If you update something in your manifest, the version must be incremented too.</span></span> <span data-ttu-id="4d353-122">这样，在安装新清单时，它将覆盖现有清单，并且用户会收到新功能。</span><span class="sxs-lookup"><span data-stu-id="4d353-122">This way, when the new manifest is installed, it overwrites the existing one and the user receives the new functionality.</span></span> <span data-ttu-id="4d353-123">如果此应用已提交到应用商店，则必须重新提交和重新验证新的清单。</span><span class="sxs-lookup"><span data-stu-id="4d353-123">If this app was submitted to the store, the new manifest must be re-submitted and re-validated.</span></span> <span data-ttu-id="4d353-124">应用用户会在清单获得批准后的数小时内自动收到新的更新清单。</span><span class="sxs-lookup"><span data-stu-id="4d353-124">The app users receive the new updated manifest automatically within few hours after the manifest is approved.</span></span>

<span data-ttu-id="4d353-125">如果应用对权限的请求发生变化，将提示用户升级并重新同意应用。</span><span class="sxs-lookup"><span data-stu-id="4d353-125">If the app requests for permissions change, the users are prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="4d353-126">此版本字符串必须遵循 [Semver](http://semver.org/) 标准 (MAJOR。MINOR。PATCH) 。</span><span class="sxs-lookup"><span data-stu-id="4d353-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="4d353-127">id</span><span class="sxs-lookup"><span data-stu-id="4d353-127">id</span></span>

<span data-ttu-id="4d353-128">**必需** - Microsoft 应用 ID</span><span class="sxs-lookup"><span data-stu-id="4d353-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="4d353-129">ID 是 Microsoft 为应用生成的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="4d353-129">The ID is a unique Microsoft-generated identifier for the app.</span></span> <span data-ttu-id="4d353-130">如果你的自动程序通过 Microsoft Bot Framework，或者你的选项卡的 Web 应用已经使用 Microsoft 登录，则你有一个 ID。</span><span class="sxs-lookup"><span data-stu-id="4d353-130">You have an ID if your bot is registered through the Microsoft Bot Framework or your tab's web app already signs in with Microsoft.</span></span> <span data-ttu-id="4d353-131">必须在此处输入 ID。</span><span class="sxs-lookup"><span data-stu-id="4d353-131">You must enter the ID here.</span></span> <span data-ttu-id="4d353-132">否则，必须在 Microsoft 应用程序注册门户[中生成一个新 ID。](https://aka.ms/appregistrations)</span><span class="sxs-lookup"><span data-stu-id="4d353-132">Otherwise, you must generate a new ID at the [Microsoft Application Registration Portal](https://aka.ms/appregistrations).</span></span> <span data-ttu-id="4d353-133">如果添加自动程序，请使用同一 ID。</span><span class="sxs-lookup"><span data-stu-id="4d353-133">Use the same ID if you add a bot.</span></span>

> [!NOTE]
> <span data-ttu-id="4d353-134">如果你要向 AppSource 中的现有应用提交更新，则清单中的 ID 不得修改。</span><span class="sxs-lookup"><span data-stu-id="4d353-134">If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="4d353-135">developer</span><span class="sxs-lookup"><span data-stu-id="4d353-135">developer</span></span>

<span data-ttu-id="4d353-136">**必需** — object</span><span class="sxs-lookup"><span data-stu-id="4d353-136">**Required** — object</span></span>

<span data-ttu-id="4d353-137">指定有关你的公司的信息。</span><span class="sxs-lookup"><span data-stu-id="4d353-137">Specifies information about your company.</span></span> <span data-ttu-id="4d353-138">对于提交到应用商店Teams，这些值必须与应用商店一览中的信息匹配。</span><span class="sxs-lookup"><span data-stu-id="4d353-138">For apps submitted to the Teams store, these values must match the information in your store listing.</span></span> <span data-ttu-id="4d353-139">有关详细信息，请参阅应用商店Teams[指南](~/concepts/deploy-and-publish/appsource/publish.md)。</span><span class="sxs-lookup"><span data-stu-id="4d353-139">For more information, see the [Teams store publishing guidelines](~/concepts/deploy-and-publish/appsource/publish.md).</span></span>

|<span data-ttu-id="4d353-140">名称</span><span class="sxs-lookup"><span data-stu-id="4d353-140">Name</span></span>| <span data-ttu-id="4d353-141">最大大小</span><span class="sxs-lookup"><span data-stu-id="4d353-141">Maximum size</span></span> | <span data-ttu-id="4d353-142">必需</span><span class="sxs-lookup"><span data-stu-id="4d353-142">Required</span></span> | <span data-ttu-id="4d353-143">说明</span><span class="sxs-lookup"><span data-stu-id="4d353-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="4d353-144">32 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-144">32 characters</span></span>|<span data-ttu-id="4d353-145">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-145">✔</span></span>|<span data-ttu-id="4d353-146">开发人员显示名称的指南。</span><span class="sxs-lookup"><span data-stu-id="4d353-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="4d353-147">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-147">2048 characters</span></span>|<span data-ttu-id="4d353-148">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-148">✔</span></span>|<span data-ttu-id="4d353-149">the https:// URL to the developer's website.</span><span class="sxs-lookup"><span data-stu-id="4d353-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="4d353-150">此链接必须将用户指向你的公司或特定于产品的登陆页面。</span><span class="sxs-lookup"><span data-stu-id="4d353-150">This link must take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="4d353-151">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-151">2048 characters</span></span>|<span data-ttu-id="4d353-152">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-152">✔</span></span>|<span data-ttu-id="4d353-153">the https:// URL to the developer's privacy policy.</span><span class="sxs-lookup"><span data-stu-id="4d353-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="4d353-154">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-154">2048 characters</span></span>|<span data-ttu-id="4d353-155">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-155">✔</span></span>|<span data-ttu-id="4d353-156">the https:// URL to the developer's use terms.</span><span class="sxs-lookup"><span data-stu-id="4d353-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="4d353-157">10 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-157">10 characters</span></span>| |<span data-ttu-id="4d353-158">**可选** 标识生成应用的合作伙伴组织的 Microsoft 合作伙伴网络 ID。</span><span class="sxs-lookup"><span data-stu-id="4d353-158">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="4d353-159">name</span><span class="sxs-lookup"><span data-stu-id="4d353-159">name</span></span>

<span data-ttu-id="4d353-160">**必需** — object</span><span class="sxs-lookup"><span data-stu-id="4d353-160">**Required** — object</span></span>

<span data-ttu-id="4d353-161">应用体验的名称，在应用体验中向Teams显示。</span><span class="sxs-lookup"><span data-stu-id="4d353-161">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="4d353-162">对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。</span><span class="sxs-lookup"><span data-stu-id="4d353-162">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="4d353-163">和 `short` `full` 的值必须不同。</span><span class="sxs-lookup"><span data-stu-id="4d353-163">The values of `short` and `full` must be different.</span></span>

|<span data-ttu-id="4d353-164">名称</span><span class="sxs-lookup"><span data-stu-id="4d353-164">Name</span></span>| <span data-ttu-id="4d353-165">最大大小</span><span class="sxs-lookup"><span data-stu-id="4d353-165">Maximum size</span></span> | <span data-ttu-id="4d353-166">必需</span><span class="sxs-lookup"><span data-stu-id="4d353-166">Required</span></span> | <span data-ttu-id="4d353-167">说明</span><span class="sxs-lookup"><span data-stu-id="4d353-167">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="4d353-168">30 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-168">30 characters</span></span>|<span data-ttu-id="4d353-169">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-169">✔</span></span>|<span data-ttu-id="4d353-170">应用的显示名称。</span><span class="sxs-lookup"><span data-stu-id="4d353-170">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="4d353-171">100 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-171">100 characters</span></span>||<span data-ttu-id="4d353-172">应用的完整名称，在完整应用名称超过 30 个字符时使用。</span><span class="sxs-lookup"><span data-stu-id="4d353-172">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="4d353-173">说明</span><span class="sxs-lookup"><span data-stu-id="4d353-173">description</span></span>

<span data-ttu-id="4d353-174">**必需** — object</span><span class="sxs-lookup"><span data-stu-id="4d353-174">**Required** — object</span></span>

<span data-ttu-id="4d353-175">向用户描述你的应用。</span><span class="sxs-lookup"><span data-stu-id="4d353-175">Describes your app to users.</span></span> <span data-ttu-id="4d353-176">对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。</span><span class="sxs-lookup"><span data-stu-id="4d353-176">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="4d353-177">确保你的描述准确地描述了你的体验，并提供相关信息来帮助潜在客户了解你的体验。</span><span class="sxs-lookup"><span data-stu-id="4d353-177">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="4d353-178">如果需要使用外部帐户，则必须在完整说明中记下。</span><span class="sxs-lookup"><span data-stu-id="4d353-178">You must note in the full description, if an external account is required for use.</span></span> <span data-ttu-id="4d353-179">和 `short` `full` 的值必须不同。</span><span class="sxs-lookup"><span data-stu-id="4d353-179">The values of `short` and `full` must be different.</span></span> <span data-ttu-id="4d353-180">简短说明不得在详细说明中重复，且不得包含任何其他应用名称。</span><span class="sxs-lookup"><span data-stu-id="4d353-180">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="4d353-181">名称</span><span class="sxs-lookup"><span data-stu-id="4d353-181">Name</span></span>| <span data-ttu-id="4d353-182">最大大小</span><span class="sxs-lookup"><span data-stu-id="4d353-182">Maximum size</span></span> | <span data-ttu-id="4d353-183">必需</span><span class="sxs-lookup"><span data-stu-id="4d353-183">Required</span></span> | <span data-ttu-id="4d353-184">说明</span><span class="sxs-lookup"><span data-stu-id="4d353-184">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="4d353-185">80 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-185">80 characters</span></span>|<span data-ttu-id="4d353-186">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-186">✔</span></span>|<span data-ttu-id="4d353-187">应用体验的简短说明，在空间有限时使用。</span><span class="sxs-lookup"><span data-stu-id="4d353-187">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="4d353-188">4000 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-188">4000 characters</span></span>|<span data-ttu-id="4d353-189">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-189">✔</span></span>|<span data-ttu-id="4d353-190">应用的完整说明。</span><span class="sxs-lookup"><span data-stu-id="4d353-190">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="4d353-191">packageName</span><span class="sxs-lookup"><span data-stu-id="4d353-191">packageName</span></span>

<span data-ttu-id="4d353-192">**可选** — 字符串</span><span class="sxs-lookup"><span data-stu-id="4d353-192">**Optional** — string</span></span>

<span data-ttu-id="4d353-193">反向域表示法的应用的唯一标识符;例如，com.example.myapp。</span><span class="sxs-lookup"><span data-stu-id="4d353-193">A unique identifier for the app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="4d353-194">最大长度：64 个字符。</span><span class="sxs-lookup"><span data-stu-id="4d353-194">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="4d353-195">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="4d353-195">localizationInfo</span></span>

<span data-ttu-id="4d353-196">**可选** — object</span><span class="sxs-lookup"><span data-stu-id="4d353-196">**Optional** — object</span></span>

<span data-ttu-id="4d353-197">允许指定默认语言，以及指向其他语言文件的指针。</span><span class="sxs-lookup"><span data-stu-id="4d353-197">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="4d353-198">请参阅 [本地化](~/concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="4d353-198">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="4d353-199">名称</span><span class="sxs-lookup"><span data-stu-id="4d353-199">Name</span></span>| <span data-ttu-id="4d353-200">最大大小</span><span class="sxs-lookup"><span data-stu-id="4d353-200">Maximum size</span></span> | <span data-ttu-id="4d353-201">必需</span><span class="sxs-lookup"><span data-stu-id="4d353-201">Required</span></span> | <span data-ttu-id="4d353-202">说明</span><span class="sxs-lookup"><span data-stu-id="4d353-202">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="4d353-203">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-203">✔</span></span>|<span data-ttu-id="4d353-204">此顶级清单文件中字符串的语言标记。</span><span class="sxs-lookup"><span data-stu-id="4d353-204">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="4d353-205">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="4d353-205">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="4d353-206">指定其他语言翻译的对象数组。</span><span class="sxs-lookup"><span data-stu-id="4d353-206">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="4d353-207">名称</span><span class="sxs-lookup"><span data-stu-id="4d353-207">Name</span></span>| <span data-ttu-id="4d353-208">最大大小</span><span class="sxs-lookup"><span data-stu-id="4d353-208">Maximum size</span></span> | <span data-ttu-id="4d353-209">必需</span><span class="sxs-lookup"><span data-stu-id="4d353-209">Required</span></span> | <span data-ttu-id="4d353-210">说明</span><span class="sxs-lookup"><span data-stu-id="4d353-210">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="4d353-211">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-211">✔</span></span>|<span data-ttu-id="4d353-212">提供的文件中字符串的语言标记。</span><span class="sxs-lookup"><span data-stu-id="4d353-212">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="4d353-213">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-213">✔</span></span>|<span data-ttu-id="4d353-214">包含已翻译字符串的 .json 文件的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="4d353-214">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="4d353-215">图标</span><span class="sxs-lookup"><span data-stu-id="4d353-215">icons</span></span>

<span data-ttu-id="4d353-216">**必需** — object</span><span class="sxs-lookup"><span data-stu-id="4d353-216">**Required** — object</span></span>

<span data-ttu-id="4d353-217">在应用内使用的Teams图标。</span><span class="sxs-lookup"><span data-stu-id="4d353-217">Icons used within the Teams app.</span></span> <span data-ttu-id="4d353-218">图标文件必须作为上传程序包的一部分包含在内。</span><span class="sxs-lookup"><span data-stu-id="4d353-218">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="4d353-219">有关详细信息 [，](../../concepts/build-and-test/apps-package.md#app-icons) 请参阅图标。</span><span class="sxs-lookup"><span data-stu-id="4d353-219">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="4d353-220">名称</span><span class="sxs-lookup"><span data-stu-id="4d353-220">Name</span></span>| <span data-ttu-id="4d353-221">最大大小</span><span class="sxs-lookup"><span data-stu-id="4d353-221">Maximum size</span></span> | <span data-ttu-id="4d353-222">必需</span><span class="sxs-lookup"><span data-stu-id="4d353-222">Required</span></span> | <span data-ttu-id="4d353-223">说明</span><span class="sxs-lookup"><span data-stu-id="4d353-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="4d353-224">32 x 32 像素</span><span class="sxs-lookup"><span data-stu-id="4d353-224">32 x 32 pixels</span></span>|<span data-ttu-id="4d353-225">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-225">✔</span></span>|<span data-ttu-id="4d353-226">指向透明 32x32 PNG 大纲图标的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="4d353-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="4d353-227">192 x 192 像素</span><span class="sxs-lookup"><span data-stu-id="4d353-227">192 x 192 pixels</span></span>|<span data-ttu-id="4d353-228">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-228">✔</span></span>|<span data-ttu-id="4d353-229">完整颜色 192x192 PNG 图标的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="4d353-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="4d353-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="4d353-230">accentColor</span></span>

<span data-ttu-id="4d353-231">**可选** — HTML 十六进制颜色代码</span><span class="sxs-lookup"><span data-stu-id="4d353-231">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="4d353-232">要与 和 结合使用用作大纲图标背景的颜色。</span><span class="sxs-lookup"><span data-stu-id="4d353-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="4d353-233">该值必须是以"#"开头的有效 HTML 颜色代码，例如 `#4464ee` 。</span><span class="sxs-lookup"><span data-stu-id="4d353-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="4d353-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="4d353-234">configurableTabs</span></span>

<span data-ttu-id="4d353-235">**可选** — 数组</span><span class="sxs-lookup"><span data-stu-id="4d353-235">**Optional** — array</span></span>

<span data-ttu-id="4d353-236">当你的应用体验具有团队频道选项卡体验时，需要在添加前进行额外配置。</span><span class="sxs-lookup"><span data-stu-id="4d353-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="4d353-237">可配置的选项卡仅在团队范围内受支持，你可以多次配置相同的选项卡。</span><span class="sxs-lookup"><span data-stu-id="4d353-237">Configurable tabs are supported only in the teams scope and you can configure the same tabs multiple times.</span></span> <span data-ttu-id="4d353-238">但是，只能在清单中定义它一次。</span><span class="sxs-lookup"><span data-stu-id="4d353-238">However, you can define it in the manifest only once.</span></span>

|<span data-ttu-id="4d353-239">名称</span><span class="sxs-lookup"><span data-stu-id="4d353-239">Name</span></span>| <span data-ttu-id="4d353-240">类型</span><span class="sxs-lookup"><span data-stu-id="4d353-240">Type</span></span>| <span data-ttu-id="4d353-241">最大大小</span><span class="sxs-lookup"><span data-stu-id="4d353-241">Maximum size</span></span> | <span data-ttu-id="4d353-242">必需</span><span class="sxs-lookup"><span data-stu-id="4d353-242">Required</span></span> | <span data-ttu-id="4d353-243">说明</span><span class="sxs-lookup"><span data-stu-id="4d353-243">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="4d353-244">string</span><span class="sxs-lookup"><span data-stu-id="4d353-244">string</span></span>|<span data-ttu-id="4d353-245">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-245">2048 characters</span></span>|<span data-ttu-id="4d353-246">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-246">✔</span></span>|<span data-ttu-id="4d353-247">配置 https:// 时将使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="4d353-247">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="4d353-248">枚举数组</span><span class="sxs-lookup"><span data-stu-id="4d353-248">array of enums</span></span>|<span data-ttu-id="4d353-249">1</span><span class="sxs-lookup"><span data-stu-id="4d353-249">1</span></span>|<span data-ttu-id="4d353-250">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-250">✔</span></span>|<span data-ttu-id="4d353-251">目前，可配置的选项卡仅支持 `team` 和 `groupchat` 作用域。</span><span class="sxs-lookup"><span data-stu-id="4d353-251">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="4d353-252">boolean</span><span class="sxs-lookup"><span data-stu-id="4d353-252">boolean</span></span>|||<span data-ttu-id="4d353-253">一个值，指示用户创建后是否可以更新选项卡配置的实例。</span><span class="sxs-lookup"><span data-stu-id="4d353-253">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="4d353-254">默认值 **：true**。</span><span class="sxs-lookup"><span data-stu-id="4d353-254">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="4d353-255">枚举数组</span><span class="sxs-lookup"><span data-stu-id="4d353-255">array of enums</span></span>|<span data-ttu-id="4d353-256">6 </span><span class="sxs-lookup"><span data-stu-id="4d353-256">6</span></span>||<span data-ttu-id="4d353-257">支持选项卡的范围 `contextItem` [集](../../tabs/how-to/access-teams-context.md)。</span><span class="sxs-lookup"><span data-stu-id="4d353-257">The set of `contextItem` scopes where a [tab is supported](../../tabs/how-to/access-teams-context.md).</span></span> <span data-ttu-id="4d353-258">默认值 **：[channelTab、privateChatTab、meetingChatTab、meetingDetailsTab]**。</span><span class="sxs-lookup"><span data-stu-id="4d353-258">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="4d353-259">string</span><span class="sxs-lookup"><span data-stu-id="4d353-259">string</span></span>|<span data-ttu-id="4d353-260">2048</span><span class="sxs-lookup"><span data-stu-id="4d353-260">2048</span></span>||<span data-ttu-id="4d353-261">选项卡预览图像的相对文件路径，用于SharePoint。</span><span class="sxs-lookup"><span data-stu-id="4d353-261">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="4d353-262">大小 1024x768。</span><span class="sxs-lookup"><span data-stu-id="4d353-262">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="4d353-263">枚举数组</span><span class="sxs-lookup"><span data-stu-id="4d353-263">array of enums</span></span>|<span data-ttu-id="4d353-264">1</span><span class="sxs-lookup"><span data-stu-id="4d353-264">1</span></span>||<span data-ttu-id="4d353-265">定义选项卡如何可用于SharePoint。</span><span class="sxs-lookup"><span data-stu-id="4d353-265">Defines how your tab is made available in SharePoint.</span></span> <span data-ttu-id="4d353-266">选项为 `sharePointFullPage` 和 `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="4d353-266">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="4d353-267">staticTabs</span><span class="sxs-lookup"><span data-stu-id="4d353-267">staticTabs</span></span>

<span data-ttu-id="4d353-268">**可选** — 数组</span><span class="sxs-lookup"><span data-stu-id="4d353-268">**Optional** — array</span></span>

<span data-ttu-id="4d353-269">定义一组默认情况下可以"固定"的选项卡，而无需用户手动添加它们。</span><span class="sxs-lookup"><span data-stu-id="4d353-269">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="4d353-270">范围中声明 `personal` 的静态选项卡始终固定到应用的个人体验。</span><span class="sxs-lookup"><span data-stu-id="4d353-270">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="4d353-271">作用域中声明的 `team` 静态选项卡当前不受支持。</span><span class="sxs-lookup"><span data-stu-id="4d353-271">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="4d353-272">此项是一个数组 (类型的所有元素) 最多包含 16 个元素 `object` 。</span><span class="sxs-lookup"><span data-stu-id="4d353-272">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="4d353-273">只有提供静态选项卡解决方案的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="4d353-273">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="4d353-274">名称</span><span class="sxs-lookup"><span data-stu-id="4d353-274">Name</span></span>| <span data-ttu-id="4d353-275">类型</span><span class="sxs-lookup"><span data-stu-id="4d353-275">Type</span></span>| <span data-ttu-id="4d353-276">最大大小</span><span class="sxs-lookup"><span data-stu-id="4d353-276">Maximum size</span></span> | <span data-ttu-id="4d353-277">必需</span><span class="sxs-lookup"><span data-stu-id="4d353-277">Required</span></span> | <span data-ttu-id="4d353-278">说明</span><span class="sxs-lookup"><span data-stu-id="4d353-278">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="4d353-279">string</span><span class="sxs-lookup"><span data-stu-id="4d353-279">string</span></span>|<span data-ttu-id="4d353-280">64 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-280">64 characters</span></span>|<span data-ttu-id="4d353-281">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-281">✔</span></span>|<span data-ttu-id="4d353-282">选项卡显示的实体的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="4d353-282">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="4d353-283">string</span><span class="sxs-lookup"><span data-stu-id="4d353-283">string</span></span>|<span data-ttu-id="4d353-284">128 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-284">128 characters</span></span>|<span data-ttu-id="4d353-285">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-285">✔</span></span>|<span data-ttu-id="4d353-286">选项卡显示名称界面中的列数。</span><span class="sxs-lookup"><span data-stu-id="4d353-286">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="4d353-287">string</span><span class="sxs-lookup"><span data-stu-id="4d353-287">string</span></span>||<span data-ttu-id="4d353-288">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-288">✔</span></span>|<span data-ttu-id="4d353-289">指向要 https:// 画布中的实体 UI 的 Teams URL。</span><span class="sxs-lookup"><span data-stu-id="4d353-289">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="4d353-290">string</span><span class="sxs-lookup"><span data-stu-id="4d353-290">string</span></span>|||<span data-ttu-id="4d353-291">用户 https:// 在浏览器中查看时指向的 URL。</span><span class="sxs-lookup"><span data-stu-id="4d353-291">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="4d353-292">string</span><span class="sxs-lookup"><span data-stu-id="4d353-292">string</span></span>|||<span data-ttu-id="4d353-293">用于 https:// 搜索查询的 URL。</span><span class="sxs-lookup"><span data-stu-id="4d353-293">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="4d353-294">枚举数组</span><span class="sxs-lookup"><span data-stu-id="4d353-294">array of enums</span></span>|<span data-ttu-id="4d353-295">1</span><span class="sxs-lookup"><span data-stu-id="4d353-295">1</span></span>|<span data-ttu-id="4d353-296">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-296">✔</span></span>|<span data-ttu-id="4d353-297">目前，静态选项卡仅支持范围，这意味着只能将作用域预配 `personal` 为个人体验的一部分。</span><span class="sxs-lookup"><span data-stu-id="4d353-297">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="4d353-298">枚举数组</span><span class="sxs-lookup"><span data-stu-id="4d353-298">array of enums</span></span>| <span data-ttu-id="4d353-299">2</span><span class="sxs-lookup"><span data-stu-id="4d353-299">2</span></span>|| <span data-ttu-id="4d353-300">支持选项卡的范围 `contextItem` 集。</span><span class="sxs-lookup"><span data-stu-id="4d353-300">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
>  <span data-ttu-id="4d353-301">第三方开发人员无法使用 searchUrl 功能。</span><span class="sxs-lookup"><span data-stu-id="4d353-301">The searchUrl feature is not available for the third-party developers.</span></span>
> <span data-ttu-id="4d353-302">如果你的选项卡需要与上下文相关的信息来显示相关内容或启动身份验证流，请参阅获取你的Microsoft Teams[上下文。](../../tabs/how-to/access-teams-context.md)</span><span class="sxs-lookup"><span data-stu-id="4d353-302">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="4d353-303">bots</span><span class="sxs-lookup"><span data-stu-id="4d353-303">bots</span></span>

<span data-ttu-id="4d353-304">**可选** — 数组</span><span class="sxs-lookup"><span data-stu-id="4d353-304">**Optional** — array</span></span>

<span data-ttu-id="4d353-305">定义自动程序解决方案以及默认命令属性等可选信息。</span><span class="sxs-lookup"><span data-stu-id="4d353-305">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="4d353-306">该项目是一个 (，当前每个应用仅允许一个自动程序) 类型的所有元素 &mdash; `object` 。</span><span class="sxs-lookup"><span data-stu-id="4d353-306">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="4d353-307">只有提供自动程序体验的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="4d353-307">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="4d353-308">名称</span><span class="sxs-lookup"><span data-stu-id="4d353-308">Name</span></span>| <span data-ttu-id="4d353-309">类型</span><span class="sxs-lookup"><span data-stu-id="4d353-309">Type</span></span>| <span data-ttu-id="4d353-310">最大大小</span><span class="sxs-lookup"><span data-stu-id="4d353-310">Maximum size</span></span> | <span data-ttu-id="4d353-311">必需</span><span class="sxs-lookup"><span data-stu-id="4d353-311">Required</span></span> | <span data-ttu-id="4d353-312">说明</span><span class="sxs-lookup"><span data-stu-id="4d353-312">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="4d353-313">string</span><span class="sxs-lookup"><span data-stu-id="4d353-313">string</span></span>|<span data-ttu-id="4d353-314">64 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-314">64 characters</span></span>|<span data-ttu-id="4d353-315">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-315">✔</span></span>|<span data-ttu-id="4d353-316">使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="4d353-316">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="4d353-317">这可能与整个应用 [ID 相同](#id)。</span><span class="sxs-lookup"><span data-stu-id="4d353-317">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="4d353-318">枚举数组</span><span class="sxs-lookup"><span data-stu-id="4d353-318">array of enums</span></span>|<span data-ttu-id="4d353-319">3</span><span class="sxs-lookup"><span data-stu-id="4d353-319">3</span></span>|<span data-ttu-id="4d353-320">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-320">✔</span></span>|<span data-ttu-id="4d353-321">指定自动程序是在 `team` 内的频道上下文中提供体验、在群组聊天 (`groupchat`) 中提供体验，还是仅在单个用户 (`personal`) 范围内提供体验。</span><span class="sxs-lookup"><span data-stu-id="4d353-321">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="4d353-322">这些选项不具排他性。</span><span class="sxs-lookup"><span data-stu-id="4d353-322">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="4d353-323">boolean</span><span class="sxs-lookup"><span data-stu-id="4d353-323">boolean</span></span>|||<span data-ttu-id="4d353-324">描述自动程序是否利用用户提示将自动程序添加到特定频道。</span><span class="sxs-lookup"><span data-stu-id="4d353-324">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="4d353-325">默认值： **`false`**</span><span class="sxs-lookup"><span data-stu-id="4d353-325">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="4d353-326">boolean</span><span class="sxs-lookup"><span data-stu-id="4d353-326">boolean</span></span>|||<span data-ttu-id="4d353-327">指示自动程序是否为单向、仅通知的自动程序，而不是对话自动程序。</span><span class="sxs-lookup"><span data-stu-id="4d353-327">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="4d353-328">默认值： **`false`**</span><span class="sxs-lookup"><span data-stu-id="4d353-328">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="4d353-329">boolean</span><span class="sxs-lookup"><span data-stu-id="4d353-329">boolean</span></span>|||<span data-ttu-id="4d353-330">指示自动程序是否支持在个人聊天中上传/下载文件。</span><span class="sxs-lookup"><span data-stu-id="4d353-330">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="4d353-331">默认值： **`false`**</span><span class="sxs-lookup"><span data-stu-id="4d353-331">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="4d353-332">boolean</span><span class="sxs-lookup"><span data-stu-id="4d353-332">boolean</span></span>|||<span data-ttu-id="4d353-333">指示机器人支持音频呼叫位置的值。</span><span class="sxs-lookup"><span data-stu-id="4d353-333">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="4d353-334">**重要** 提示：此属性当前为实验属性。</span><span class="sxs-lookup"><span data-stu-id="4d353-334">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="4d353-335">实验属性可能不完整，并且可能在完全可用之前发生更改。</span><span class="sxs-lookup"><span data-stu-id="4d353-335">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="4d353-336">它仅供测试和探索之用，不得在生产应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="4d353-336">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="4d353-337">默认值： **`false`**</span><span class="sxs-lookup"><span data-stu-id="4d353-337">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="4d353-338">boolean</span><span class="sxs-lookup"><span data-stu-id="4d353-338">boolean</span></span>|||<span data-ttu-id="4d353-339">指示机器人支持视频呼叫位置的值。</span><span class="sxs-lookup"><span data-stu-id="4d353-339">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="4d353-340">**重要** 提示：此属性当前为实验属性。</span><span class="sxs-lookup"><span data-stu-id="4d353-340">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="4d353-341">实验属性可能不完整，并且可能在完全可用之前发生更改。</span><span class="sxs-lookup"><span data-stu-id="4d353-341">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="4d353-342">它仅供测试和探索之用，不得在生产应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="4d353-342">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="4d353-343">默认值： **`false`**</span><span class="sxs-lookup"><span data-stu-id="4d353-343">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="4d353-344">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="4d353-344">bots.commandLists</span></span>

<span data-ttu-id="4d353-345">自动程序可以推荐给用户的命令的可选列表。</span><span class="sxs-lookup"><span data-stu-id="4d353-345">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="4d353-346">对象是一个 (，最多包含 2 个元素) 所有类型元素;您必须为自动程序支持的每个范围定义单独的 `object` 命令列表。</span><span class="sxs-lookup"><span data-stu-id="4d353-346">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="4d353-347">有关详细信息 [，](~/bots/how-to/create-a-bot-commands-menu.md) 请参阅自动程序菜单。</span><span class="sxs-lookup"><span data-stu-id="4d353-347">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="4d353-348">名称</span><span class="sxs-lookup"><span data-stu-id="4d353-348">Name</span></span>| <span data-ttu-id="4d353-349">类型</span><span class="sxs-lookup"><span data-stu-id="4d353-349">Type</span></span>| <span data-ttu-id="4d353-350">最大大小</span><span class="sxs-lookup"><span data-stu-id="4d353-350">Maximum size</span></span> | <span data-ttu-id="4d353-351">必需</span><span class="sxs-lookup"><span data-stu-id="4d353-351">Required</span></span> | <span data-ttu-id="4d353-352">说明</span><span class="sxs-lookup"><span data-stu-id="4d353-352">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="4d353-353">枚举数组</span><span class="sxs-lookup"><span data-stu-id="4d353-353">array of enums</span></span>|<span data-ttu-id="4d353-354">3</span><span class="sxs-lookup"><span data-stu-id="4d353-354">3</span></span>|<span data-ttu-id="4d353-355">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-355">✔</span></span>|<span data-ttu-id="4d353-356">指定命令列表有效的作用域。</span><span class="sxs-lookup"><span data-stu-id="4d353-356">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="4d353-357">选项包括 `team`、`personal` 和 `groupchat`。</span><span class="sxs-lookup"><span data-stu-id="4d353-357">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="4d353-358">对象数组</span><span class="sxs-lookup"><span data-stu-id="4d353-358">array of objects</span></span>|<span data-ttu-id="4d353-359">10  </span><span class="sxs-lookup"><span data-stu-id="4d353-359">10</span></span>|<span data-ttu-id="4d353-360">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-360">✔</span></span>|<span data-ttu-id="4d353-361">自动程序支持的命令数组：</span><span class="sxs-lookup"><span data-stu-id="4d353-361">An array of commands the bot supports:</span></span><br><span data-ttu-id="4d353-362">`title`：自动程序命令名称（字符串，32）</span><span class="sxs-lookup"><span data-stu-id="4d353-362">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="4d353-363">`description`：命令语法及其参数的简单描述或示例（字符串，128）</span><span class="sxs-lookup"><span data-stu-id="4d353-363">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="4d353-364">bots.commandLists.commands</span><span class="sxs-lookup"><span data-stu-id="4d353-364">bots.commandLists.commands</span></span>

|<span data-ttu-id="4d353-365">名称</span><span class="sxs-lookup"><span data-stu-id="4d353-365">Name</span></span>| <span data-ttu-id="4d353-366">类型</span><span class="sxs-lookup"><span data-stu-id="4d353-366">Type</span></span>| <span data-ttu-id="4d353-367">最大大小</span><span class="sxs-lookup"><span data-stu-id="4d353-367">Maximum size</span></span> | <span data-ttu-id="4d353-368">必需</span><span class="sxs-lookup"><span data-stu-id="4d353-368">Required</span></span> | <span data-ttu-id="4d353-369">说明</span><span class="sxs-lookup"><span data-stu-id="4d353-369">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="4d353-370">title</span><span class="sxs-lookup"><span data-stu-id="4d353-370">title</span></span>|<span data-ttu-id="4d353-371">string</span><span class="sxs-lookup"><span data-stu-id="4d353-371">string</span></span>|<span data-ttu-id="4d353-372">12 </span><span class="sxs-lookup"><span data-stu-id="4d353-372">12</span></span>|<span data-ttu-id="4d353-373">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-373">✔</span></span>|<span data-ttu-id="4d353-374">自动程序命令名称</span><span class="sxs-lookup"><span data-stu-id="4d353-374">The bot command name</span></span>|
|<span data-ttu-id="4d353-375">说明</span><span class="sxs-lookup"><span data-stu-id="4d353-375">description</span></span>|<span data-ttu-id="4d353-376">string</span><span class="sxs-lookup"><span data-stu-id="4d353-376">string</span></span>|<span data-ttu-id="4d353-377">128 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-377">128 characters</span></span>|<span data-ttu-id="4d353-378">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-378">✔</span></span>|<span data-ttu-id="4d353-379">简单文本说明或命令语法及其参数的示例。</span><span class="sxs-lookup"><span data-stu-id="4d353-379">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="4d353-380">连接器</span><span class="sxs-lookup"><span data-stu-id="4d353-380">connectors</span></span>

<span data-ttu-id="4d353-381">**可选** — 数组</span><span class="sxs-lookup"><span data-stu-id="4d353-381">**Optional** — array</span></span>

<span data-ttu-id="4d353-382">`connectors`块为应用Office 365连接器。</span><span class="sxs-lookup"><span data-stu-id="4d353-382">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="4d353-383">对象是一个数组， (类型的所有元素) 1 个元素 `object` 。</span><span class="sxs-lookup"><span data-stu-id="4d353-383">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="4d353-384">只有提供连接器的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="4d353-384">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="4d353-385">名称</span><span class="sxs-lookup"><span data-stu-id="4d353-385">Name</span></span>| <span data-ttu-id="4d353-386">类型</span><span class="sxs-lookup"><span data-stu-id="4d353-386">Type</span></span>| <span data-ttu-id="4d353-387">最大大小</span><span class="sxs-lookup"><span data-stu-id="4d353-387">Maximum size</span></span> | <span data-ttu-id="4d353-388">必需</span><span class="sxs-lookup"><span data-stu-id="4d353-388">Required</span></span> | <span data-ttu-id="4d353-389">说明</span><span class="sxs-lookup"><span data-stu-id="4d353-389">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="4d353-390">string</span><span class="sxs-lookup"><span data-stu-id="4d353-390">string</span></span>|<span data-ttu-id="4d353-391">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-391">2048 characters</span></span>|<span data-ttu-id="4d353-392">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-392">✔</span></span>|<span data-ttu-id="4d353-393">配置 https:// 时将使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="4d353-393">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="4d353-394">枚举数组</span><span class="sxs-lookup"><span data-stu-id="4d353-394">array of enums</span></span>|<span data-ttu-id="4d353-395">1</span><span class="sxs-lookup"><span data-stu-id="4d353-395">1</span></span>|<span data-ttu-id="4d353-396">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-396">✔</span></span>|<span data-ttu-id="4d353-397">指定连接器是提供在 中频道上下文中的体验，还是仅针对单个用户 `team` `personal` () 。</span><span class="sxs-lookup"><span data-stu-id="4d353-397">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="4d353-398">目前，仅 `team` 支持范围。</span><span class="sxs-lookup"><span data-stu-id="4d353-398">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="4d353-399">string</span><span class="sxs-lookup"><span data-stu-id="4d353-399">string</span></span>|<span data-ttu-id="4d353-400">64 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-400">64 characters</span></span>|<span data-ttu-id="4d353-401">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-401">✔</span></span>|<span data-ttu-id="4d353-402">连接器的唯一标识符，与连接器开发人员仪表板中的 ID [相匹配](https://aka.ms/connectorsdashboard)。</span><span class="sxs-lookup"><span data-stu-id="4d353-402">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="4d353-403">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="4d353-403">composeExtensions</span></span>

<span data-ttu-id="4d353-404">**可选** — 数组</span><span class="sxs-lookup"><span data-stu-id="4d353-404">**Optional** — array</span></span>

<span data-ttu-id="4d353-405">为应用定义消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="4d353-405">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="4d353-406">2017 年 11 月，功能名称从"撰写扩展"更改为"邮件扩展"，但清单名称保持不变，以便现有扩展继续工作。</span><span class="sxs-lookup"><span data-stu-id="4d353-406">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="4d353-407">项目是一个数组， (类型的所有元素) 1 个元素 `object` 。</span><span class="sxs-lookup"><span data-stu-id="4d353-407">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="4d353-408">只有提供邮件扩展的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="4d353-408">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="4d353-409">名称</span><span class="sxs-lookup"><span data-stu-id="4d353-409">Name</span></span>| <span data-ttu-id="4d353-410">类型</span><span class="sxs-lookup"><span data-stu-id="4d353-410">Type</span></span> | <span data-ttu-id="4d353-411">最大大小</span><span class="sxs-lookup"><span data-stu-id="4d353-411">Maximum Size</span></span> | <span data-ttu-id="4d353-412">必需</span><span class="sxs-lookup"><span data-stu-id="4d353-412">Required</span></span> | <span data-ttu-id="4d353-413">说明</span><span class="sxs-lookup"><span data-stu-id="4d353-413">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="4d353-414">string</span><span class="sxs-lookup"><span data-stu-id="4d353-414">string</span></span>|<span data-ttu-id="4d353-415">64</span><span class="sxs-lookup"><span data-stu-id="4d353-415">64</span></span>|<span data-ttu-id="4d353-416">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-416">✔</span></span>|<span data-ttu-id="4d353-417">自动程序支持消息传递扩展的唯一 Microsoft 应用 ID，在 Bot Framework 中注册。</span><span class="sxs-lookup"><span data-stu-id="4d353-417">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="4d353-418">这可能与整个应用 ID 相同。</span><span class="sxs-lookup"><span data-stu-id="4d353-418">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="4d353-419">对象数组</span><span class="sxs-lookup"><span data-stu-id="4d353-419">array of objects</span></span>|<span data-ttu-id="4d353-420">10  </span><span class="sxs-lookup"><span data-stu-id="4d353-420">10</span></span>|<span data-ttu-id="4d353-421">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-421">✔</span></span>|<span data-ttu-id="4d353-422">邮件扩展支持的命令数组</span><span class="sxs-lookup"><span data-stu-id="4d353-422">Array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="4d353-423">boolean</span><span class="sxs-lookup"><span data-stu-id="4d353-423">boolean</span></span>|||<span data-ttu-id="4d353-424">一个值，指示用户是否可以更新邮件扩展的配置。</span><span class="sxs-lookup"><span data-stu-id="4d353-424">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="4d353-425">默认值：**False**。</span><span class="sxs-lookup"><span data-stu-id="4d353-425">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="4d353-426">对象数组</span><span class="sxs-lookup"><span data-stu-id="4d353-426">array of Objects</span></span>|<span data-ttu-id="4d353-427">5 </span><span class="sxs-lookup"><span data-stu-id="4d353-427">5</span></span>||<span data-ttu-id="4d353-428">允许满足某些条件时调用应用的处理程序列表。</span><span class="sxs-lookup"><span data-stu-id="4d353-428">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="4d353-429">string</span><span class="sxs-lookup"><span data-stu-id="4d353-429">string</span></span>|||<span data-ttu-id="4d353-430">消息处理程序的类型。</span><span class="sxs-lookup"><span data-stu-id="4d353-430">The type of message handler.</span></span> <span data-ttu-id="4d353-431">必须是 `"link"`。</span><span class="sxs-lookup"><span data-stu-id="4d353-431">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="4d353-432">字符串数组</span><span class="sxs-lookup"><span data-stu-id="4d353-432">array of Strings</span></span>|||<span data-ttu-id="4d353-433">链接邮件处理程序可以注册的域数组。</span><span class="sxs-lookup"><span data-stu-id="4d353-433">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="4d353-434">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="4d353-434">composeExtensions.commands</span></span>

<span data-ttu-id="4d353-435">邮件扩展必须声明一个或多个命令。</span><span class="sxs-lookup"><span data-stu-id="4d353-435">Your messaging extension must declare one or more commands.</span></span> <span data-ttu-id="4d353-436">每个命令都Microsoft Teams UI 入口点的潜在交互。</span><span class="sxs-lookup"><span data-stu-id="4d353-436">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="4d353-437">最多有 10 个命令。</span><span class="sxs-lookup"><span data-stu-id="4d353-437">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="4d353-438">每个命令项都是具有以下结构的对象：</span><span class="sxs-lookup"><span data-stu-id="4d353-438">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="4d353-439">名称</span><span class="sxs-lookup"><span data-stu-id="4d353-439">Name</span></span>| <span data-ttu-id="4d353-440">类型</span><span class="sxs-lookup"><span data-stu-id="4d353-440">Type</span></span>| <span data-ttu-id="4d353-441">最大大小</span><span class="sxs-lookup"><span data-stu-id="4d353-441">Maximum size</span></span> | <span data-ttu-id="4d353-442">必需</span><span class="sxs-lookup"><span data-stu-id="4d353-442">Required</span></span> | <span data-ttu-id="4d353-443">说明</span><span class="sxs-lookup"><span data-stu-id="4d353-443">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="4d353-444">string</span><span class="sxs-lookup"><span data-stu-id="4d353-444">string</span></span>|<span data-ttu-id="4d353-445">64 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-445">64 characters</span></span>|<span data-ttu-id="4d353-446">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-446">✔</span></span>|<span data-ttu-id="4d353-447">命令的 ID。</span><span class="sxs-lookup"><span data-stu-id="4d353-447">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="4d353-448">string</span><span class="sxs-lookup"><span data-stu-id="4d353-448">string</span></span>|<span data-ttu-id="4d353-449">32 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-449">32 characters</span></span>|<span data-ttu-id="4d353-450">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-450">✔</span></span>|<span data-ttu-id="4d353-451">用户友好命令名称。</span><span class="sxs-lookup"><span data-stu-id="4d353-451">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="4d353-452">string</span><span class="sxs-lookup"><span data-stu-id="4d353-452">string</span></span>|<span data-ttu-id="4d353-453">64 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-453">64 characters</span></span>||<span data-ttu-id="4d353-454">命令的类型。</span><span class="sxs-lookup"><span data-stu-id="4d353-454">Type of the command.</span></span> <span data-ttu-id="4d353-455">或 `query` `action` 之一。</span><span class="sxs-lookup"><span data-stu-id="4d353-455">One of `query` or `action`.</span></span> <span data-ttu-id="4d353-456">默认值 **：query**。</span><span class="sxs-lookup"><span data-stu-id="4d353-456">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="4d353-457">string</span><span class="sxs-lookup"><span data-stu-id="4d353-457">string</span></span>|<span data-ttu-id="4d353-458">128 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-458">128 characters</span></span>||<span data-ttu-id="4d353-459">向用户显示以指示此命令用途的说明。</span><span class="sxs-lookup"><span data-stu-id="4d353-459">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="4d353-460">boolean</span><span class="sxs-lookup"><span data-stu-id="4d353-460">boolean</span></span>|||<span data-ttu-id="4d353-461">布尔值指示命令最初是否运行，没有参数。</span><span class="sxs-lookup"><span data-stu-id="4d353-461">A boolean value indicates whether the command runs initially with no parameters.</span></span> <span data-ttu-id="4d353-462">默认为 **false**。</span><span class="sxs-lookup"><span data-stu-id="4d353-462">Default is **false**.</span></span>|
|`context`|<span data-ttu-id="4d353-463">字符串数组</span><span class="sxs-lookup"><span data-stu-id="4d353-463">array of Strings</span></span>|<span data-ttu-id="4d353-464">3</span><span class="sxs-lookup"><span data-stu-id="4d353-464">3</span></span>||<span data-ttu-id="4d353-465">定义可以从何处调用邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="4d353-465">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="4d353-466">、 `compose` 、 的任意 `commandBox` 组合 `message` 。</span><span class="sxs-lookup"><span data-stu-id="4d353-466">Any combination of`compose`,`commandBox`,`message`.</span></span> <span data-ttu-id="4d353-467">默认值为“`["compose","commandBox"]`”。</span><span class="sxs-lookup"><span data-stu-id="4d353-467">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="4d353-468">boolean</span><span class="sxs-lookup"><span data-stu-id="4d353-468">boolean</span></span>|||<span data-ttu-id="4d353-469">一个布尔值，指示它是否必须动态提取任务模块。</span><span class="sxs-lookup"><span data-stu-id="4d353-469">A boolean value that indicates if it must fetch the task module dynamically.</span></span> <span data-ttu-id="4d353-470">默认为 **false**。</span><span class="sxs-lookup"><span data-stu-id="4d353-470">Default is **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="4d353-471">object</span><span class="sxs-lookup"><span data-stu-id="4d353-471">object</span></span>|||<span data-ttu-id="4d353-472">指定在使用消息传递扩展命令时要预加载的任务模块。</span><span class="sxs-lookup"><span data-stu-id="4d353-472">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="4d353-473">string</span><span class="sxs-lookup"><span data-stu-id="4d353-473">string</span></span>|<span data-ttu-id="4d353-474">64 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-474">64 characters</span></span>||<span data-ttu-id="4d353-475">初始对话框标题。</span><span class="sxs-lookup"><span data-stu-id="4d353-475">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="4d353-476">string</span><span class="sxs-lookup"><span data-stu-id="4d353-476">string</span></span>|||<span data-ttu-id="4d353-477">对话框宽度 - 以像素为单位的一个数字或默认布局，例如"large"、"medium"或"small"。</span><span class="sxs-lookup"><span data-stu-id="4d353-477">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="4d353-478">string</span><span class="sxs-lookup"><span data-stu-id="4d353-478">string</span></span>|||<span data-ttu-id="4d353-479">对话框高度 - 以像素为单位的一个数字或默认布局，例如"large"、"medium"或"small"。</span><span class="sxs-lookup"><span data-stu-id="4d353-479">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="4d353-480">string</span><span class="sxs-lookup"><span data-stu-id="4d353-480">string</span></span>|||<span data-ttu-id="4d353-481">初始 Web 视图 URL。</span><span class="sxs-lookup"><span data-stu-id="4d353-481">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="4d353-482">对象数组</span><span class="sxs-lookup"><span data-stu-id="4d353-482">array of object</span></span>|<span data-ttu-id="4d353-483">5 个项目</span><span class="sxs-lookup"><span data-stu-id="4d353-483">5 items</span></span>|<span data-ttu-id="4d353-484">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-484">✔</span></span>|<span data-ttu-id="4d353-485">命令采用的参数列表。</span><span class="sxs-lookup"><span data-stu-id="4d353-485">The list of parameters the command takes.</span></span> <span data-ttu-id="4d353-486">最小值：1;最大值：5。</span><span class="sxs-lookup"><span data-stu-id="4d353-486">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="4d353-487">string</span><span class="sxs-lookup"><span data-stu-id="4d353-487">string</span></span>|<span data-ttu-id="4d353-488">64 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-488">64 characters</span></span>|<span data-ttu-id="4d353-489">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-489">✔</span></span>|<span data-ttu-id="4d353-490">显示在客户端中的参数的名称。</span><span class="sxs-lookup"><span data-stu-id="4d353-490">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="4d353-491">这包括在用户请求中。</span><span class="sxs-lookup"><span data-stu-id="4d353-491">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="4d353-492">string</span><span class="sxs-lookup"><span data-stu-id="4d353-492">string</span></span>|<span data-ttu-id="4d353-493">32 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-493">32 characters</span></span>|<span data-ttu-id="4d353-494">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-494">✔</span></span>|<span data-ttu-id="4d353-495">参数的用户友好标题。</span><span class="sxs-lookup"><span data-stu-id="4d353-495">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="4d353-496">string</span><span class="sxs-lookup"><span data-stu-id="4d353-496">string</span></span>|<span data-ttu-id="4d353-497">128 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-497">128 characters</span></span>||<span data-ttu-id="4d353-498">描述此参数用途的用户友好字符串。</span><span class="sxs-lookup"><span data-stu-id="4d353-498">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="4d353-499">string</span><span class="sxs-lookup"><span data-stu-id="4d353-499">string</span></span>|<span data-ttu-id="4d353-500">512 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-500">512 characters</span></span>||<span data-ttu-id="4d353-501">参数的初始值。</span><span class="sxs-lookup"><span data-stu-id="4d353-501">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="4d353-502">string</span><span class="sxs-lookup"><span data-stu-id="4d353-502">string</span></span>|<span data-ttu-id="4d353-503">128 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-503">128 characters</span></span>||<span data-ttu-id="4d353-504">定义在任务模块上显示的控件的类型 `fetchTask: true` 。</span><span class="sxs-lookup"><span data-stu-id="4d353-504">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="4d353-505">之一 `text, textarea, number, date, time, toggle, choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="4d353-505">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="4d353-506">对象数组</span><span class="sxs-lookup"><span data-stu-id="4d353-506">array of objects</span></span>|<span data-ttu-id="4d353-507">10 个项目</span><span class="sxs-lookup"><span data-stu-id="4d353-507">10 items</span></span>||<span data-ttu-id="4d353-508">的选项 `choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="4d353-508">The choice options for the`choiceset`.</span></span> <span data-ttu-id="4d353-509">仅在 为 `parameter.inputType` `choiceset` 时使用 。</span><span class="sxs-lookup"><span data-stu-id="4d353-509">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="4d353-510">string</span><span class="sxs-lookup"><span data-stu-id="4d353-510">string</span></span>|<span data-ttu-id="4d353-511">128 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-511">128 characters</span></span>|<span data-ttu-id="4d353-512">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-512">✔</span></span>|<span data-ttu-id="4d353-513">选项的标题。</span><span class="sxs-lookup"><span data-stu-id="4d353-513">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="4d353-514">string</span><span class="sxs-lookup"><span data-stu-id="4d353-514">string</span></span>|<span data-ttu-id="4d353-515">512 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-515">512 characters</span></span>|<span data-ttu-id="4d353-516">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-516">✔</span></span>|<span data-ttu-id="4d353-517">选项的值。</span><span class="sxs-lookup"><span data-stu-id="4d353-517">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="4d353-518">权限</span><span class="sxs-lookup"><span data-stu-id="4d353-518">permissions</span></span>

<span data-ttu-id="4d353-519">**可选** — 字符串数组</span><span class="sxs-lookup"><span data-stu-id="4d353-519">**Optional** — array of strings</span></span>

<span data-ttu-id="4d353-520">一个数组，指定应用请求哪些权限，使最终用户 `string` 知道扩展的执行方式。</span><span class="sxs-lookup"><span data-stu-id="4d353-520">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension performs.</span></span> <span data-ttu-id="4d353-521">以下选项非独占：</span><span class="sxs-lookup"><span data-stu-id="4d353-521">The following options are non-exclusive:</span></span>

* <span data-ttu-id="4d353-522">`identity`&emsp;需要用户标识信息</span><span class="sxs-lookup"><span data-stu-id="4d353-522">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="4d353-523">`messageTeamMembers`&emsp;需要向团队成员发送直接消息的权限</span><span class="sxs-lookup"><span data-stu-id="4d353-523">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="4d353-524">在应用更新期间更改这些权限，会导致用户在运行更新后的应用后重复同意过程。</span><span class="sxs-lookup"><span data-stu-id="4d353-524">Changing these permissions during app update, causes your users to repeat the consent process after they run the updated app.</span></span> <span data-ttu-id="4d353-525">有关详细信息 [，请参阅更新](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) 应用。</span><span class="sxs-lookup"><span data-stu-id="4d353-525">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="4d353-526">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="4d353-526">devicePermissions</span></span>

<span data-ttu-id="4d353-527">**可选** — 字符串数组</span><span class="sxs-lookup"><span data-stu-id="4d353-527">**Optional** — array of strings</span></span>

<span data-ttu-id="4d353-528">在应用请求访问的用户设备上提供本机功能。</span><span class="sxs-lookup"><span data-stu-id="4d353-528">Provides the native features on a user's device that your app requests access to.</span></span> <span data-ttu-id="4d353-529">选项有：</span><span class="sxs-lookup"><span data-stu-id="4d353-529">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="4d353-530">validDomains</span><span class="sxs-lookup"><span data-stu-id="4d353-530">validDomains</span></span>

<span data-ttu-id="4d353-531">**可选**，但 **已指出的必需** 项除外</span><span class="sxs-lookup"><span data-stu-id="4d353-531">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="4d353-532">应用预期在客户端内加载的网站的有效Teams列表。</span><span class="sxs-lookup"><span data-stu-id="4d353-532">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="4d353-533">域列表可以包含通配符，例如 `*.example.com` ， 。</span><span class="sxs-lookup"><span data-stu-id="4d353-533">Domain listings can include wildcards, for example, `*.example.com`.</span></span> <span data-ttu-id="4d353-534">这完全匹配域的一个段;如果需要匹配，请使用 `a.b.example.com` `*.*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="4d353-534">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="4d353-535">如果你的选项卡配置或内容 UI 需要导航到除用于选项卡配置的其他任何其他域，则必须在此处指定该域。</span><span class="sxs-lookup"><span data-stu-id="4d353-535">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="4d353-536">不需要 **在** 应用中包含要支持的标识提供程序的域。</span><span class="sxs-lookup"><span data-stu-id="4d353-536">It is **not** necessary to include the domains of identity providers you want to support in your app.</span></span> <span data-ttu-id="4d353-537">例如，若要使用 Google ID 进行身份验证，必须重定向到 accounts.google.com，但不得在 `validDomains[]` accounts.google.com。</span><span class="sxs-lookup"><span data-stu-id="4d353-537">For example, to authenticate using a Google ID, it is required to redirect to accounts.google.com, however, you must not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="4d353-538">Teams需要自己的 sharepoint URL 正常运行的应用程序，请包括其有效域列表中的"{teamsitedomain}"。</span><span class="sxs-lookup"><span data-stu-id="4d353-538">Teams apps that require their own sharepoint URLs to function well, includes "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d353-539">不要直接添加或通过通配符添加超出您控制的域。</span><span class="sxs-lookup"><span data-stu-id="4d353-539">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="4d353-540">例如， `yourapp.onmicrosoft.com` 是有效的，但 `*.onmicrosoft.com` 是 无效。</span><span class="sxs-lookup"><span data-stu-id="4d353-540">For example, `yourapp.onmicrosoft.com` is valid, however, `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="4d353-541">对象是包含类型 的所有元素的数组 `string` 。</span><span class="sxs-lookup"><span data-stu-id="4d353-541">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="4d353-542">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="4d353-542">webApplicationInfo</span></span>

<span data-ttu-id="4d353-543">**可选** — object</span><span class="sxs-lookup"><span data-stu-id="4d353-543">**Optional** — object</span></span>

<span data-ttu-id="4d353-544">提供你的Azure Active Directory (AAD) 应用 ID 和 Microsoft Graph 信息，以帮助用户无缝登录你的应用。</span><span class="sxs-lookup"><span data-stu-id="4d353-544">Provide your Azure Active Directory (AAD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="4d353-545">如果你的应用在 AAD 中注册，则必须提供应用 ID，以便管理员可以轻松地查看权限，并授予管理员Teams许可。</span><span class="sxs-lookup"><span data-stu-id="4d353-545">If your app is registered in AAD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="4d353-546">名称</span><span class="sxs-lookup"><span data-stu-id="4d353-546">Name</span></span>| <span data-ttu-id="4d353-547">类型</span><span class="sxs-lookup"><span data-stu-id="4d353-547">Type</span></span>| <span data-ttu-id="4d353-548">最大大小</span><span class="sxs-lookup"><span data-stu-id="4d353-548">Maximum size</span></span> | <span data-ttu-id="4d353-549">必需</span><span class="sxs-lookup"><span data-stu-id="4d353-549">Required</span></span> | <span data-ttu-id="4d353-550">说明</span><span class="sxs-lookup"><span data-stu-id="4d353-550">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="4d353-551">string</span><span class="sxs-lookup"><span data-stu-id="4d353-551">string</span></span>|<span data-ttu-id="4d353-552">36 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-552">36 characters</span></span>|<span data-ttu-id="4d353-553">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-553">✔</span></span>|<span data-ttu-id="4d353-554">应用的 AAD 应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="4d353-554">AAD application id of the app.</span></span> <span data-ttu-id="4d353-555">此 ID 必须是 GUID。</span><span class="sxs-lookup"><span data-stu-id="4d353-555">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="4d353-556">string</span><span class="sxs-lookup"><span data-stu-id="4d353-556">string</span></span>|<span data-ttu-id="4d353-557">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-557">2048 characters</span></span>|<span data-ttu-id="4d353-558">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-558">✔</span></span>|<span data-ttu-id="4d353-559">用于获取 SSO 身份验证令牌的应用的资源 URL。</span><span class="sxs-lookup"><span data-stu-id="4d353-559">Resource URL of app for acquiring auth token for SSO.</span></span> </br> <span data-ttu-id="4d353-560">**注意：** 如果不使用 SSO，请确保在此字段中向应用清单输入虚拟字符串值，以避免 https://notapplicable 错误响应。</span><span class="sxs-lookup"><span data-stu-id="4d353-560">**NOTE:** If you are not using SSO, ensure that you enter a dummy string value in this field to your app manifest, for example, https://notapplicable to avoid an error response.</span></span> |
|`applicationPermissions`|<span data-ttu-id="4d353-561">array of strings</span><span class="sxs-lookup"><span data-stu-id="4d353-561">array of strings</span></span>|<span data-ttu-id="4d353-562">128 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-562">128 characters</span></span>||<span data-ttu-id="4d353-563">指定具体 [资源特定许可](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="4d353-563">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="4d353-564">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="4d353-564">showLoadingIndicator</span></span>

<span data-ttu-id="4d353-565">**可选** — 布尔值</span><span class="sxs-lookup"><span data-stu-id="4d353-565">**Optional** — boolean</span></span>

<span data-ttu-id="4d353-566">指示在加载应用或选项卡时是否显示加载指示器。</span><span class="sxs-lookup"><span data-stu-id="4d353-566">Indicates whether or not to show the loading indicator when an app or tab is loading.</span></span> <span data-ttu-id="4d353-567">默认为 **false**。</span><span class="sxs-lookup"><span data-stu-id="4d353-567">Default is **false**.</span></span>
>[!NOTE]
><span data-ttu-id="4d353-568">如果在应用清单中选择 true，若要正确加载页面，请修改选项卡和任务模块的内容页，如显示本机加载指示器文档 `showLoadingIndicator` 中所述。 [](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)</span><span class="sxs-lookup"><span data-stu-id="4d353-568">If you select`showLoadingIndicator` as true in your app manifest, to load the page correctly, modify the content pages of your tabs and task modules as described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="4d353-569">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="4d353-569">isFullScreen</span></span>

 <span data-ttu-id="4d353-570">**可选** — 布尔值</span><span class="sxs-lookup"><span data-stu-id="4d353-570">**Optional** — boolean</span></span>

<span data-ttu-id="4d353-571">指示在具有或没有选项卡标题栏的情况下呈现个人应用。</span><span class="sxs-lookup"><span data-stu-id="4d353-571">Indicate where a personal app is rendered with or without a tab header bar.</span></span> <span data-ttu-id="4d353-572">默认为 **false**。</span><span class="sxs-lookup"><span data-stu-id="4d353-572">Default is **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="4d353-573">activities</span><span class="sxs-lookup"><span data-stu-id="4d353-573">activities</span></span>

<span data-ttu-id="4d353-574">**可选** — object</span><span class="sxs-lookup"><span data-stu-id="4d353-574">**Optional** — object</span></span>

<span data-ttu-id="4d353-575">定义应用用于发布用户活动源的属性。</span><span class="sxs-lookup"><span data-stu-id="4d353-575">Define the properties your app uses to post a user activity feed.</span></span>

|<span data-ttu-id="4d353-576">名称</span><span class="sxs-lookup"><span data-stu-id="4d353-576">Name</span></span>| <span data-ttu-id="4d353-577">类型</span><span class="sxs-lookup"><span data-stu-id="4d353-577">Type</span></span>| <span data-ttu-id="4d353-578">最大大小</span><span class="sxs-lookup"><span data-stu-id="4d353-578">Maximum size</span></span> | <span data-ttu-id="4d353-579">必需</span><span class="sxs-lookup"><span data-stu-id="4d353-579">Required</span></span> | <span data-ttu-id="4d353-580">说明</span><span class="sxs-lookup"><span data-stu-id="4d353-580">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="4d353-581">对象数组</span><span class="sxs-lookup"><span data-stu-id="4d353-581">array of Objects</span></span>|<span data-ttu-id="4d353-582">128 项</span><span class="sxs-lookup"><span data-stu-id="4d353-582">128 items</span></span>| | <span data-ttu-id="4d353-583">提供你的应用可以发布给用户活动源的活动类型。</span><span class="sxs-lookup"><span data-stu-id="4d353-583">Provide the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="4d353-584">activities.activityTypes</span><span class="sxs-lookup"><span data-stu-id="4d353-584">activities.activityTypes</span></span>

|<span data-ttu-id="4d353-585">名称</span><span class="sxs-lookup"><span data-stu-id="4d353-585">Name</span></span>| <span data-ttu-id="4d353-586">类型</span><span class="sxs-lookup"><span data-stu-id="4d353-586">Type</span></span>| <span data-ttu-id="4d353-587">最大大小</span><span class="sxs-lookup"><span data-stu-id="4d353-587">Maximum size</span></span> | <span data-ttu-id="4d353-588">必需</span><span class="sxs-lookup"><span data-stu-id="4d353-588">Required</span></span> | <span data-ttu-id="4d353-589">说明</span><span class="sxs-lookup"><span data-stu-id="4d353-589">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="4d353-590">string</span><span class="sxs-lookup"><span data-stu-id="4d353-590">string</span></span>|<span data-ttu-id="4d353-591">32 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-591">32 characters</span></span>|<span data-ttu-id="4d353-592">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-592">✔</span></span>|<span data-ttu-id="4d353-593">通知类型。</span><span class="sxs-lookup"><span data-stu-id="4d353-593">The notification type.</span></span> <span data-ttu-id="4d353-594">*请参阅下文*。</span><span class="sxs-lookup"><span data-stu-id="4d353-594">*See below*.</span></span>|
|`description`|<span data-ttu-id="4d353-595">string</span><span class="sxs-lookup"><span data-stu-id="4d353-595">string</span></span>|<span data-ttu-id="4d353-596">128 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-596">128 characters</span></span>|<span data-ttu-id="4d353-597">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-597">✔</span></span>|<span data-ttu-id="4d353-598">通知的简要说明。</span><span class="sxs-lookup"><span data-stu-id="4d353-598">A brief description of the notification.</span></span> <span data-ttu-id="4d353-599">*请参阅下文*。</span><span class="sxs-lookup"><span data-stu-id="4d353-599">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="4d353-600">string</span><span class="sxs-lookup"><span data-stu-id="4d353-600">string</span></span>|<span data-ttu-id="4d353-601">128 个字符</span><span class="sxs-lookup"><span data-stu-id="4d353-601">128 characters</span></span>|<span data-ttu-id="4d353-602">✔</span><span class="sxs-lookup"><span data-stu-id="4d353-602">✔</span></span>|<span data-ttu-id="4d353-603">例如："{actor} 已创建任务 {taskId}"</span><span class="sxs-lookup"><span data-stu-id="4d353-603">Ex: "{actor} created task {taskId} for you"</span></span>|

```json
{
   "activities":{
      "activityTypes":[
         {
            "type":"taskCreated",
            "description":"Task Created Activity",
            "templateText":"{actor} created task {taskId} for you"
         },
         {
            "type":"teamMention",
            "description":"Team Mention Activity",
            "templateText":"{actor} mentioned team"
         },
         {
            "type":"channelMention",
            "description":"Channel Mention Activity",
            "templateText":"{actor} mentioned channel"
         },
         {
            "type":"userMention",
            "description":"Personal Mention Activity",
            "templateText":"{actor} mentioned user"
         },
         {
            "type":"calendarForward",
            "description":"Forwarding a Calendar Event",
            "templateText":"{actor} sent user an invite on behalf of {eventOwner}"
         },
         {
            "type":"calendarForward",
            "description":"Forwarding a Calendar Event",
            "templateText":"{actor} sent user an invite on behalf of {eventOwner}"
         },
         {
            "type":"creatorTaskCreated",
            "description":"Created Task Created",
            "templateText":"The Creator created task {taskId} for you"
         }
      ]
   }
}
```

***

## <a name="defaultinstallscope"></a><span data-ttu-id="4d353-604">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="4d353-604">defaultInstallScope</span></span>

<span data-ttu-id="4d353-605">**可选** - string</span><span class="sxs-lookup"><span data-stu-id="4d353-605">**Optional** - string</span></span>

<span data-ttu-id="4d353-606">指定默认情况下为此应用定义的安装范围。</span><span class="sxs-lookup"><span data-stu-id="4d353-606">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="4d353-607">定义的范围将是当用户尝试添加应用时按钮上显示的选项。</span><span class="sxs-lookup"><span data-stu-id="4d353-607">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="4d353-608">选项有：</span><span class="sxs-lookup"><span data-stu-id="4d353-608">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="4d353-609">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="4d353-609">defaultGroupCapability</span></span>

<span data-ttu-id="4d353-610">**可选** - object</span><span class="sxs-lookup"><span data-stu-id="4d353-610">**Optional** - object</span></span>

<span data-ttu-id="4d353-611">选择组安装范围后，它将在用户安装应用时定义默认功能。</span><span class="sxs-lookup"><span data-stu-id="4d353-611">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="4d353-612">选项有：</span><span class="sxs-lookup"><span data-stu-id="4d353-612">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="4d353-613">名称</span><span class="sxs-lookup"><span data-stu-id="4d353-613">Name</span></span>| <span data-ttu-id="4d353-614">类型</span><span class="sxs-lookup"><span data-stu-id="4d353-614">Type</span></span>| <span data-ttu-id="4d353-615">最大大小</span><span class="sxs-lookup"><span data-stu-id="4d353-615">Maximum size</span></span> | <span data-ttu-id="4d353-616">必需</span><span class="sxs-lookup"><span data-stu-id="4d353-616">Required</span></span> | <span data-ttu-id="4d353-617">说明</span><span class="sxs-lookup"><span data-stu-id="4d353-617">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="4d353-618">string</span><span class="sxs-lookup"><span data-stu-id="4d353-618">string</span></span>|||<span data-ttu-id="4d353-619">当选择的安装范围为 `team` 时，此字段指定可用的默认功能。</span><span class="sxs-lookup"><span data-stu-id="4d353-619">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="4d353-620">选项 `tab` ：、 `bot` 或 `connector` 。</span><span class="sxs-lookup"><span data-stu-id="4d353-620">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="4d353-621">string</span><span class="sxs-lookup"><span data-stu-id="4d353-621">string</span></span>|||<span data-ttu-id="4d353-622">当选择的安装范围为 `groupchat` 时，此字段指定可用的默认功能。</span><span class="sxs-lookup"><span data-stu-id="4d353-622">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="4d353-623">选项 `tab` ：、 `bot` 或 `connector` 。</span><span class="sxs-lookup"><span data-stu-id="4d353-623">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="4d353-624">string</span><span class="sxs-lookup"><span data-stu-id="4d353-624">string</span></span>|||<span data-ttu-id="4d353-625">当选择的安装范围为 `meetings` 时，此字段指定可用的默认功能。</span><span class="sxs-lookup"><span data-stu-id="4d353-625">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="4d353-626">选项 `tab` ：、 `bot` 或 `connector` 。</span><span class="sxs-lookup"><span data-stu-id="4d353-626">Options: `tab`, `bot`, or `connector`.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="4d353-627">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="4d353-627">configurableProperties</span></span>

<span data-ttu-id="4d353-628">**可选** - 数组</span><span class="sxs-lookup"><span data-stu-id="4d353-628">**Optional** - array</span></span>

<span data-ttu-id="4d353-629">`configurableProperties`此块定义管理员可Teams应用属性。</span><span class="sxs-lookup"><span data-stu-id="4d353-629">The `configurableProperties` block defines the app properties that Teams admin can customize.</span></span> <span data-ttu-id="4d353-630">有关详细信息，请参阅自定义[应用程序中Microsoft Teams。](/MicrosoftTeams/customize-apps)</span><span class="sxs-lookup"><span data-stu-id="4d353-630">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="4d353-631">必须定义至少一个属性。</span><span class="sxs-lookup"><span data-stu-id="4d353-631">A minimum of one property must be defined.</span></span> <span data-ttu-id="4d353-632">最多可以在此块中定义九个属性。</span><span class="sxs-lookup"><span data-stu-id="4d353-632">You can define a maximum of nine properties in this block.</span></span>
> <span data-ttu-id="4d353-633">最佳做法是，你必须提供自定义指南，以便应用用户和客户在自定义应用时遵循这些准则。</span><span class="sxs-lookup"><span data-stu-id="4d353-633">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span>

<span data-ttu-id="4d353-634">可以定义以下任一属性：</span><span class="sxs-lookup"><span data-stu-id="4d353-634">You can define any of the following properties:</span></span>
* <span data-ttu-id="4d353-635">`name`：允许管理员更改应用显示名称。</span><span class="sxs-lookup"><span data-stu-id="4d353-635">`name`: Allows admin to change the app's display name.</span></span>
* <span data-ttu-id="4d353-636">`shortDescription`：允许管理员更改应用的简短说明。</span><span class="sxs-lookup"><span data-stu-id="4d353-636">`shortDescription`: Allows admin to change the app's short description.</span></span>
* <span data-ttu-id="4d353-637">`longDescription`：允许管理员更改应用的详细说明。</span><span class="sxs-lookup"><span data-stu-id="4d353-637">`longDescription`: Allows admin to change the app's detailed description.</span></span>
* <span data-ttu-id="4d353-638">`smallImageUrl`：它是 `outline` 清单块 `icons` 中的 属性。</span><span class="sxs-lookup"><span data-stu-id="4d353-638">`smallImageUrl`: It is the `outline` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="4d353-639">`largeImageUrl`：它是 `color` 清单块 `icons` 中的 属性。</span><span class="sxs-lookup"><span data-stu-id="4d353-639">`largeImageUrl`: It is the `color` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="4d353-640">`accentColor`：它是要与 和 一起使用的颜色，作为大纲图标的背景。</span><span class="sxs-lookup"><span data-stu-id="4d353-640">`accentColor`: It is the color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="4d353-641">`websiteUrl`：它是 https:// 网站的 URL。</span><span class="sxs-lookup"><span data-stu-id="4d353-641">`websiteUrl`: It is the https:// URL to the developer's website.</span></span>
* <span data-ttu-id="4d353-642">`privacyUrl`：它是 https:// 隐私策略的 URL。</span><span class="sxs-lookup"><span data-stu-id="4d353-642">`privacyUrl`: It is the https:// URL to the developer's privacy policy.</span></span>
* <span data-ttu-id="4d353-643">`termsOfUseUrl`：它是 https:// 使用条款的 URL。</span><span class="sxs-lookup"><span data-stu-id="4d353-643">`termsOfUseUrl`: It is the https:// URL to the developer's terms of use.</span></span>


