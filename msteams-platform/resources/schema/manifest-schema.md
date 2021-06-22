---
title: 清单架构参考
description: 描述列表的清单Microsoft Teams
ms.topic: reference
ms.author: lajanuar
localization_priority: Normal
keywords: teams 清单架构
ms.openlocfilehash: 44bae986d5ea78a044cb66d48e6e093d489f4473
ms.sourcegitcommit: 99b1f151e4e36a86c6a5d2ccbde01bf45b61f526
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2021
ms.locfileid: "53037626"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="70560-104">参考：Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="70560-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="70560-105">Teams清单介绍了应用如何集成到 Microsoft Teams 产品。</span><span class="sxs-lookup"><span data-stu-id="70560-105">The Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="70560-106">清单必须符合 托管在 的架构 [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json) 。</span><span class="sxs-lookup"><span data-stu-id="70560-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="70560-107">早期版本 1.0、1.1,..., 1.6 等也受 URL ("v1.x"支持) 。</span><span class="sxs-lookup"><span data-stu-id="70560-107">Previous versions 1.0, 1.1,..., 1.6, and so on are also supported (using "v1.x" in the URL).</span></span>
<span data-ttu-id="70560-108">有关在每个版本中所做的更改详细信息，请参阅 [清单更改日志](https://github.com/OfficeDev/microsoft-teams-app-schema/releases)。</span><span class="sxs-lookup"><span data-stu-id="70560-108">For more information on the changes made in each version, see [manifest change log](https://github.com/OfficeDev/microsoft-teams-app-schema/releases).</span></span>

<span data-ttu-id="70560-109">以下架构示例显示了所有扩展性选项：</span><span class="sxs-lookup"><span data-stu-id="70560-109">The following schema sample shows all extensibility options:</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="70560-110">示例完整清单</span><span class="sxs-lookup"><span data-stu-id="70560-110">Sample full manifest</span></span>

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
    ]
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
     "developerUrl",
     "privacyUrl",
     "termsOfUseUrl"        
  ]              
}
```

<span data-ttu-id="70560-111">该架构定义以下属性：</span><span class="sxs-lookup"><span data-stu-id="70560-111">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="70560-112">$schema</span><span class="sxs-lookup"><span data-stu-id="70560-112">$schema</span></span>

<span data-ttu-id="70560-113">可选，但推荐 — 字符串</span><span class="sxs-lookup"><span data-stu-id="70560-113">Optional, but recommended — string</span></span>

<span data-ttu-id="70560-114">引用 https:// JSON 架构的 URL。</span><span class="sxs-lookup"><span data-stu-id="70560-114">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="70560-115">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="70560-115">manifestVersion</span></span>

<span data-ttu-id="70560-116">**必需** — 字符串</span><span class="sxs-lookup"><span data-stu-id="70560-116">**Required** — string</span></span>

<span data-ttu-id="70560-117">此清单使用的清单架构版本。</span><span class="sxs-lookup"><span data-stu-id="70560-117">The version of manifest schema this manifest is using.</span></span> <span data-ttu-id="70560-118">必须为 1.10。</span><span class="sxs-lookup"><span data-stu-id="70560-118">It must be 1.10.</span></span>

## <a name="version"></a><span data-ttu-id="70560-119">version</span><span class="sxs-lookup"><span data-stu-id="70560-119">version</span></span>

<span data-ttu-id="70560-120">**必需** — 字符串</span><span class="sxs-lookup"><span data-stu-id="70560-120">**Required** — string</span></span>

<span data-ttu-id="70560-121">特定应用的版本。</span><span class="sxs-lookup"><span data-stu-id="70560-121">The version of a specific app.</span></span> <span data-ttu-id="70560-122">如果更新清单中的某些内容，则版本也必须递增。</span><span class="sxs-lookup"><span data-stu-id="70560-122">If you update something in your manifest, the version must be incremented too.</span></span> <span data-ttu-id="70560-123">这样，在安装新清单时，它将覆盖现有清单，并且用户会收到新功能。</span><span class="sxs-lookup"><span data-stu-id="70560-123">This way, when the new manifest is installed, it overwrites the existing one and the user receives the new functionality.</span></span> <span data-ttu-id="70560-124">如果此应用已提交到应用商店，则必须重新提交和重新验证新的清单。</span><span class="sxs-lookup"><span data-stu-id="70560-124">If this app was submitted to the store, the new manifest must be re-submitted and re-validated.</span></span> <span data-ttu-id="70560-125">应用用户会在清单获得批准后的数小时内自动收到新的更新清单。</span><span class="sxs-lookup"><span data-stu-id="70560-125">The app users receive the new updated manifest automatically within few hours after the manifest is approved.</span></span>

<span data-ttu-id="70560-126">如果应用对权限的请求发生变化，将提示用户升级并重新同意应用。</span><span class="sxs-lookup"><span data-stu-id="70560-126">If the app requests for permissions change, the users are prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="70560-127">此版本字符串必须遵循 [Semver](http://semver.org/) 标准 (MAJOR。MINOR。PATCH) 。</span><span class="sxs-lookup"><span data-stu-id="70560-127">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="70560-128">id</span><span class="sxs-lookup"><span data-stu-id="70560-128">id</span></span>

<span data-ttu-id="70560-129">**必需** - Microsoft 应用 ID</span><span class="sxs-lookup"><span data-stu-id="70560-129">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="70560-130">ID 是 Microsoft 为应用生成的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="70560-130">The ID is a unique Microsoft-generated identifier for the app.</span></span> <span data-ttu-id="70560-131">如果你的自动程序通过 Microsoft Bot Framework，或者你的选项卡的 Web 应用已经使用 Microsoft 登录，则你有一个 ID。</span><span class="sxs-lookup"><span data-stu-id="70560-131">You have an ID if your bot is registered through the Microsoft Bot Framework or your tab's web app already signs in with Microsoft.</span></span> <span data-ttu-id="70560-132">必须在此处输入 ID。</span><span class="sxs-lookup"><span data-stu-id="70560-132">You must enter the ID here.</span></span> <span data-ttu-id="70560-133">否则，必须在 Microsoft 应用程序注册门户[中生成一个新 ID。](https://aka.ms/appregistrations)</span><span class="sxs-lookup"><span data-stu-id="70560-133">Otherwise, you must generate a new ID at the [Microsoft Application Registration Portal](https://aka.ms/appregistrations).</span></span> <span data-ttu-id="70560-134">如果添加自动程序，请使用同一 ID。</span><span class="sxs-lookup"><span data-stu-id="70560-134">Use the same ID if you add a bot.</span></span>

> [!NOTE]
> <span data-ttu-id="70560-135">如果你要向 AppSource 中的现有应用提交更新，则清单中的 ID 不得修改。</span><span class="sxs-lookup"><span data-stu-id="70560-135">If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="70560-136">developer</span><span class="sxs-lookup"><span data-stu-id="70560-136">developer</span></span>

<span data-ttu-id="70560-137">**必需** — object</span><span class="sxs-lookup"><span data-stu-id="70560-137">**Required** — object</span></span>

<span data-ttu-id="70560-138">指定有关你的公司的信息。</span><span class="sxs-lookup"><span data-stu-id="70560-138">Specifies information about your company.</span></span> <span data-ttu-id="70560-139">对于提交到应用商店Teams，这些值必须与应用商店一览中的信息匹配。</span><span class="sxs-lookup"><span data-stu-id="70560-139">For apps submitted to the Teams store, these values must match the information in your store listing.</span></span> <span data-ttu-id="70560-140">有关详细信息，请参阅应用商店Teams[指南](~/concepts/deploy-and-publish/appsource/publish.md)。</span><span class="sxs-lookup"><span data-stu-id="70560-140">For more information, see the [Teams store publishing guidelines](~/concepts/deploy-and-publish/appsource/publish.md).</span></span>

|<span data-ttu-id="70560-141">名称</span><span class="sxs-lookup"><span data-stu-id="70560-141">Name</span></span>| <span data-ttu-id="70560-142">最大大小</span><span class="sxs-lookup"><span data-stu-id="70560-142">Maximum size</span></span> | <span data-ttu-id="70560-143">必需</span><span class="sxs-lookup"><span data-stu-id="70560-143">Required</span></span> | <span data-ttu-id="70560-144">说明</span><span class="sxs-lookup"><span data-stu-id="70560-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="70560-145">32 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-145">32 characters</span></span>|<span data-ttu-id="70560-146">✔</span><span class="sxs-lookup"><span data-stu-id="70560-146">✔</span></span>|<span data-ttu-id="70560-147">开发人员显示名称的指南。</span><span class="sxs-lookup"><span data-stu-id="70560-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="70560-148">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-148">2048 characters</span></span>|<span data-ttu-id="70560-149">✔</span><span class="sxs-lookup"><span data-stu-id="70560-149">✔</span></span>|<span data-ttu-id="70560-150">the https:// URL to the developer's website.</span><span class="sxs-lookup"><span data-stu-id="70560-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="70560-151">此链接必须将用户指向你的公司或特定于产品的登陆页面。</span><span class="sxs-lookup"><span data-stu-id="70560-151">This link must take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="70560-152">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-152">2048 characters</span></span>|<span data-ttu-id="70560-153">✔</span><span class="sxs-lookup"><span data-stu-id="70560-153">✔</span></span>|<span data-ttu-id="70560-154">the https:// URL to the developer's privacy policy.</span><span class="sxs-lookup"><span data-stu-id="70560-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="70560-155">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-155">2048 characters</span></span>|<span data-ttu-id="70560-156">✔</span><span class="sxs-lookup"><span data-stu-id="70560-156">✔</span></span>|<span data-ttu-id="70560-157">the https:// URL to the developer's use terms.</span><span class="sxs-lookup"><span data-stu-id="70560-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="70560-158">10 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-158">10 characters</span></span>| |<span data-ttu-id="70560-159">**可选** 标识生成应用的合作伙伴组织的 Microsoft 合作伙伴网络 ID。</span><span class="sxs-lookup"><span data-stu-id="70560-159">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="70560-160">name</span><span class="sxs-lookup"><span data-stu-id="70560-160">name</span></span>

<span data-ttu-id="70560-161">**必需** — object</span><span class="sxs-lookup"><span data-stu-id="70560-161">**Required** — object</span></span>

<span data-ttu-id="70560-162">应用体验的名称，在应用体验中向Teams显示。</span><span class="sxs-lookup"><span data-stu-id="70560-162">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="70560-163">对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。</span><span class="sxs-lookup"><span data-stu-id="70560-163">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="70560-164">和 `short` `full` 的值必须不同。</span><span class="sxs-lookup"><span data-stu-id="70560-164">The values of `short` and `full` must be different.</span></span>

|<span data-ttu-id="70560-165">名称</span><span class="sxs-lookup"><span data-stu-id="70560-165">Name</span></span>| <span data-ttu-id="70560-166">最大大小</span><span class="sxs-lookup"><span data-stu-id="70560-166">Maximum size</span></span> | <span data-ttu-id="70560-167">必需</span><span class="sxs-lookup"><span data-stu-id="70560-167">Required</span></span> | <span data-ttu-id="70560-168">说明</span><span class="sxs-lookup"><span data-stu-id="70560-168">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="70560-169">30 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-169">30 characters</span></span>|<span data-ttu-id="70560-170">✔</span><span class="sxs-lookup"><span data-stu-id="70560-170">✔</span></span>|<span data-ttu-id="70560-171">应用的显示名称。</span><span class="sxs-lookup"><span data-stu-id="70560-171">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="70560-172">100 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-172">100 characters</span></span>||<span data-ttu-id="70560-173">应用的完整名称，在完整应用名称超过 30 个字符时使用。</span><span class="sxs-lookup"><span data-stu-id="70560-173">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="70560-174">说明</span><span class="sxs-lookup"><span data-stu-id="70560-174">description</span></span>

<span data-ttu-id="70560-175">**必需** — object</span><span class="sxs-lookup"><span data-stu-id="70560-175">**Required** — object</span></span>

<span data-ttu-id="70560-176">向用户描述你的应用。</span><span class="sxs-lookup"><span data-stu-id="70560-176">Describes your app to users.</span></span> <span data-ttu-id="70560-177">对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。</span><span class="sxs-lookup"><span data-stu-id="70560-177">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="70560-178">确保你的描述准确地描述了你的体验，并提供相关信息来帮助潜在客户了解你的体验。</span><span class="sxs-lookup"><span data-stu-id="70560-178">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="70560-179">如果需要使用外部帐户，则必须在完整说明中记下。</span><span class="sxs-lookup"><span data-stu-id="70560-179">You must note in the full description, if an external account is required for use.</span></span> <span data-ttu-id="70560-180">和 `short` `full` 的值必须不同。</span><span class="sxs-lookup"><span data-stu-id="70560-180">The values of `short` and `full` must be different.</span></span> <span data-ttu-id="70560-181">简短说明不得在详细说明中重复，且不得包含任何其他应用名称。</span><span class="sxs-lookup"><span data-stu-id="70560-181">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="70560-182">名称</span><span class="sxs-lookup"><span data-stu-id="70560-182">Name</span></span>| <span data-ttu-id="70560-183">最大大小</span><span class="sxs-lookup"><span data-stu-id="70560-183">Maximum size</span></span> | <span data-ttu-id="70560-184">必需</span><span class="sxs-lookup"><span data-stu-id="70560-184">Required</span></span> | <span data-ttu-id="70560-185">说明</span><span class="sxs-lookup"><span data-stu-id="70560-185">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="70560-186">80 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-186">80 characters</span></span>|<span data-ttu-id="70560-187">✔</span><span class="sxs-lookup"><span data-stu-id="70560-187">✔</span></span>|<span data-ttu-id="70560-188">应用体验的简短说明，在空间有限时使用。</span><span class="sxs-lookup"><span data-stu-id="70560-188">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="70560-189">4000 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-189">4000 characters</span></span>|<span data-ttu-id="70560-190">✔</span><span class="sxs-lookup"><span data-stu-id="70560-190">✔</span></span>|<span data-ttu-id="70560-191">应用的完整说明。</span><span class="sxs-lookup"><span data-stu-id="70560-191">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="70560-192">packageName</span><span class="sxs-lookup"><span data-stu-id="70560-192">packageName</span></span>

<span data-ttu-id="70560-193">**可选** — 字符串</span><span class="sxs-lookup"><span data-stu-id="70560-193">**Optional** — string</span></span>

<span data-ttu-id="70560-194">反向域表示法的应用的唯一标识符;例如，com.example.myapp。</span><span class="sxs-lookup"><span data-stu-id="70560-194">A unique identifier for the app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="70560-195">最大长度：64 个字符。</span><span class="sxs-lookup"><span data-stu-id="70560-195">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="70560-196">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="70560-196">localizationInfo</span></span>

<span data-ttu-id="70560-197">**可选** — object</span><span class="sxs-lookup"><span data-stu-id="70560-197">**Optional** — object</span></span>

<span data-ttu-id="70560-198">允许指定默认语言，以及指向其他语言文件的指针。</span><span class="sxs-lookup"><span data-stu-id="70560-198">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="70560-199">有关详细信息，请参阅 [本地化](~/concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="70560-199">For more information, see [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="70560-200">名称</span><span class="sxs-lookup"><span data-stu-id="70560-200">Name</span></span>| <span data-ttu-id="70560-201">最大大小</span><span class="sxs-lookup"><span data-stu-id="70560-201">Maximum size</span></span> | <span data-ttu-id="70560-202">必需</span><span class="sxs-lookup"><span data-stu-id="70560-202">Required</span></span> | <span data-ttu-id="70560-203">说明</span><span class="sxs-lookup"><span data-stu-id="70560-203">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="70560-204">✔</span><span class="sxs-lookup"><span data-stu-id="70560-204">✔</span></span>|<span data-ttu-id="70560-205">此顶级清单文件中字符串的语言标记。</span><span class="sxs-lookup"><span data-stu-id="70560-205">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="70560-206">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="70560-206">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="70560-207">指定其他语言翻译的对象数组。</span><span class="sxs-lookup"><span data-stu-id="70560-207">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="70560-208">名称</span><span class="sxs-lookup"><span data-stu-id="70560-208">Name</span></span>| <span data-ttu-id="70560-209">最大大小</span><span class="sxs-lookup"><span data-stu-id="70560-209">Maximum size</span></span> | <span data-ttu-id="70560-210">必需</span><span class="sxs-lookup"><span data-stu-id="70560-210">Required</span></span> | <span data-ttu-id="70560-211">说明</span><span class="sxs-lookup"><span data-stu-id="70560-211">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="70560-212">✔</span><span class="sxs-lookup"><span data-stu-id="70560-212">✔</span></span>|<span data-ttu-id="70560-213">提供的文件中字符串的语言标记。</span><span class="sxs-lookup"><span data-stu-id="70560-213">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="70560-214">✔</span><span class="sxs-lookup"><span data-stu-id="70560-214">✔</span></span>|<span data-ttu-id="70560-215">包含已翻译字符串的 .json 文件的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="70560-215">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="70560-216">图标</span><span class="sxs-lookup"><span data-stu-id="70560-216">icons</span></span>

<span data-ttu-id="70560-217">**必需** — object</span><span class="sxs-lookup"><span data-stu-id="70560-217">**Required** — object</span></span>

<span data-ttu-id="70560-218">在应用内使用的Teams图标。</span><span class="sxs-lookup"><span data-stu-id="70560-218">Icons used within the Teams app.</span></span> <span data-ttu-id="70560-219">图标文件必须作为上传程序包的一部分包含在内。</span><span class="sxs-lookup"><span data-stu-id="70560-219">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="70560-220">有关详细信息 [，](../../concepts/build-and-test/apps-package.md#app-icons) 请参阅图标。</span><span class="sxs-lookup"><span data-stu-id="70560-220">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="70560-221">名称</span><span class="sxs-lookup"><span data-stu-id="70560-221">Name</span></span>| <span data-ttu-id="70560-222">最大大小</span><span class="sxs-lookup"><span data-stu-id="70560-222">Maximum size</span></span> | <span data-ttu-id="70560-223">必需</span><span class="sxs-lookup"><span data-stu-id="70560-223">Required</span></span> | <span data-ttu-id="70560-224">说明</span><span class="sxs-lookup"><span data-stu-id="70560-224">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="70560-225">32 x 32 像素</span><span class="sxs-lookup"><span data-stu-id="70560-225">32 x 32 pixels</span></span>|<span data-ttu-id="70560-226">✔</span><span class="sxs-lookup"><span data-stu-id="70560-226">✔</span></span>|<span data-ttu-id="70560-227">指向透明 32x32 PNG 大纲图标的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="70560-227">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="70560-228">192 x 192 像素</span><span class="sxs-lookup"><span data-stu-id="70560-228">192 x 192 pixels</span></span>|<span data-ttu-id="70560-229">✔</span><span class="sxs-lookup"><span data-stu-id="70560-229">✔</span></span>|<span data-ttu-id="70560-230">完整颜色 192x192 PNG 图标的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="70560-230">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="70560-231">accentColor</span><span class="sxs-lookup"><span data-stu-id="70560-231">accentColor</span></span>

<span data-ttu-id="70560-232">**可选** — HTML 十六进制颜色代码</span><span class="sxs-lookup"><span data-stu-id="70560-232">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="70560-233">要与 和 结合使用用作大纲图标背景的颜色。</span><span class="sxs-lookup"><span data-stu-id="70560-233">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="70560-234">该值必须是以"#"开头的有效 HTML 颜色代码，例如 `#4464ee` 。</span><span class="sxs-lookup"><span data-stu-id="70560-234">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="70560-235">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="70560-235">configurableTabs</span></span>

<span data-ttu-id="70560-236">**可选** — 数组</span><span class="sxs-lookup"><span data-stu-id="70560-236">**Optional** — array</span></span>

<span data-ttu-id="70560-237">当你的应用体验具有团队频道选项卡体验时，需要在添加前进行额外配置。</span><span class="sxs-lookup"><span data-stu-id="70560-237">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="70560-238">可配置的选项卡仅在团队范围内受支持，你可以多次配置相同的选项卡。</span><span class="sxs-lookup"><span data-stu-id="70560-238">Configurable tabs are supported only in the teams scope and you can configure the same tabs multiple times.</span></span> <span data-ttu-id="70560-239">但是，只能在清单中定义它一次。</span><span class="sxs-lookup"><span data-stu-id="70560-239">However, you can define it in the manifest only once.</span></span>

|<span data-ttu-id="70560-240">名称</span><span class="sxs-lookup"><span data-stu-id="70560-240">Name</span></span>| <span data-ttu-id="70560-241">类型</span><span class="sxs-lookup"><span data-stu-id="70560-241">Type</span></span>| <span data-ttu-id="70560-242">最大大小</span><span class="sxs-lookup"><span data-stu-id="70560-242">Maximum size</span></span> | <span data-ttu-id="70560-243">必需</span><span class="sxs-lookup"><span data-stu-id="70560-243">Required</span></span> | <span data-ttu-id="70560-244">说明</span><span class="sxs-lookup"><span data-stu-id="70560-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="70560-245">string</span><span class="sxs-lookup"><span data-stu-id="70560-245">string</span></span>|<span data-ttu-id="70560-246">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-246">2048 characters</span></span>|<span data-ttu-id="70560-247">✔</span><span class="sxs-lookup"><span data-stu-id="70560-247">✔</span></span>|<span data-ttu-id="70560-248">配置 https:// 时将使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="70560-248">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="70560-249">枚举数组</span><span class="sxs-lookup"><span data-stu-id="70560-249">array of enums</span></span>|<span data-ttu-id="70560-250">1</span><span class="sxs-lookup"><span data-stu-id="70560-250">1</span></span>|<span data-ttu-id="70560-251">✔</span><span class="sxs-lookup"><span data-stu-id="70560-251">✔</span></span>|<span data-ttu-id="70560-252">目前，可配置的选项卡仅支持 `team` 和 `groupchat` 作用域。</span><span class="sxs-lookup"><span data-stu-id="70560-252">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="70560-253">boolean</span><span class="sxs-lookup"><span data-stu-id="70560-253">boolean</span></span>|||<span data-ttu-id="70560-254">一个值，指示用户创建后是否可以更新选项卡配置的实例。</span><span class="sxs-lookup"><span data-stu-id="70560-254">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="70560-255">默认值 **：true**。</span><span class="sxs-lookup"><span data-stu-id="70560-255">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="70560-256">枚举数组</span><span class="sxs-lookup"><span data-stu-id="70560-256">array of enums</span></span>|<span data-ttu-id="70560-257">6 </span><span class="sxs-lookup"><span data-stu-id="70560-257">6</span></span>||<span data-ttu-id="70560-258">支持选项卡的范围 `contextItem` [集](../../tabs/how-to/access-teams-context.md)。</span><span class="sxs-lookup"><span data-stu-id="70560-258">The set of `contextItem` scopes where a [tab is supported](../../tabs/how-to/access-teams-context.md).</span></span> <span data-ttu-id="70560-259">默认值 **：[channelTab、privateChatTab、meetingChatTab、meetingDetailsTab]**。</span><span class="sxs-lookup"><span data-stu-id="70560-259">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="70560-260">string</span><span class="sxs-lookup"><span data-stu-id="70560-260">string</span></span>|<span data-ttu-id="70560-261">2048</span><span class="sxs-lookup"><span data-stu-id="70560-261">2048</span></span>||<span data-ttu-id="70560-262">选项卡预览图像的相对文件路径，用于SharePoint。</span><span class="sxs-lookup"><span data-stu-id="70560-262">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="70560-263">大小 1024x768。</span><span class="sxs-lookup"><span data-stu-id="70560-263">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="70560-264">枚举数组</span><span class="sxs-lookup"><span data-stu-id="70560-264">array of enums</span></span>|<span data-ttu-id="70560-265">1</span><span class="sxs-lookup"><span data-stu-id="70560-265">1</span></span>||<span data-ttu-id="70560-266">定义选项卡如何可用于SharePoint。</span><span class="sxs-lookup"><span data-stu-id="70560-266">Defines how your tab is made available in SharePoint.</span></span> <span data-ttu-id="70560-267">选项为 `sharePointFullPage` 和 `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="70560-267">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="70560-268">staticTabs</span><span class="sxs-lookup"><span data-stu-id="70560-268">staticTabs</span></span>

<span data-ttu-id="70560-269">**可选** — 数组</span><span class="sxs-lookup"><span data-stu-id="70560-269">**Optional** — array</span></span>

<span data-ttu-id="70560-270">定义一组默认情况下可以"固定"的选项卡，而无需用户手动添加它们。</span><span class="sxs-lookup"><span data-stu-id="70560-270">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="70560-271">范围中声明 `personal` 的静态选项卡始终固定到应用的个人体验。</span><span class="sxs-lookup"><span data-stu-id="70560-271">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="70560-272">作用域中声明的 `team` 静态选项卡当前不受支持。</span><span class="sxs-lookup"><span data-stu-id="70560-272">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="70560-273">此项是一个数组 (类型的所有元素) 最多包含 16 个元素 `object` 。</span><span class="sxs-lookup"><span data-stu-id="70560-273">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="70560-274">只有提供静态选项卡解决方案的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="70560-274">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="70560-275">名称</span><span class="sxs-lookup"><span data-stu-id="70560-275">Name</span></span>| <span data-ttu-id="70560-276">类型</span><span class="sxs-lookup"><span data-stu-id="70560-276">Type</span></span>| <span data-ttu-id="70560-277">最大大小</span><span class="sxs-lookup"><span data-stu-id="70560-277">Maximum size</span></span> | <span data-ttu-id="70560-278">必需</span><span class="sxs-lookup"><span data-stu-id="70560-278">Required</span></span> | <span data-ttu-id="70560-279">说明</span><span class="sxs-lookup"><span data-stu-id="70560-279">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="70560-280">string</span><span class="sxs-lookup"><span data-stu-id="70560-280">string</span></span>|<span data-ttu-id="70560-281">64 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-281">64 characters</span></span>|<span data-ttu-id="70560-282">✔</span><span class="sxs-lookup"><span data-stu-id="70560-282">✔</span></span>|<span data-ttu-id="70560-283">选项卡显示的实体的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="70560-283">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="70560-284">string</span><span class="sxs-lookup"><span data-stu-id="70560-284">string</span></span>|<span data-ttu-id="70560-285">128 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-285">128 characters</span></span>|<span data-ttu-id="70560-286">✔</span><span class="sxs-lookup"><span data-stu-id="70560-286">✔</span></span>|<span data-ttu-id="70560-287">选项卡显示名称界面中的列数。</span><span class="sxs-lookup"><span data-stu-id="70560-287">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="70560-288">string</span><span class="sxs-lookup"><span data-stu-id="70560-288">string</span></span>||<span data-ttu-id="70560-289">✔</span><span class="sxs-lookup"><span data-stu-id="70560-289">✔</span></span>|<span data-ttu-id="70560-290">指向要 https:// 画布中的实体 UI 的 Teams URL。</span><span class="sxs-lookup"><span data-stu-id="70560-290">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="70560-291">string</span><span class="sxs-lookup"><span data-stu-id="70560-291">string</span></span>|||<span data-ttu-id="70560-292">用户 https:// 在浏览器中查看时指向的 URL。</span><span class="sxs-lookup"><span data-stu-id="70560-292">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="70560-293">string</span><span class="sxs-lookup"><span data-stu-id="70560-293">string</span></span>|||<span data-ttu-id="70560-294">用于 https:// 搜索查询的 URL。</span><span class="sxs-lookup"><span data-stu-id="70560-294">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="70560-295">枚举数组</span><span class="sxs-lookup"><span data-stu-id="70560-295">array of enums</span></span>|<span data-ttu-id="70560-296">1</span><span class="sxs-lookup"><span data-stu-id="70560-296">1</span></span>|<span data-ttu-id="70560-297">✔</span><span class="sxs-lookup"><span data-stu-id="70560-297">✔</span></span>|<span data-ttu-id="70560-298">目前，静态选项卡仅支持范围，这意味着只能将作用域预配 `personal` 为个人体验的一部分。</span><span class="sxs-lookup"><span data-stu-id="70560-298">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="70560-299">枚举数组</span><span class="sxs-lookup"><span data-stu-id="70560-299">array of enums</span></span>| <span data-ttu-id="70560-300">2</span><span class="sxs-lookup"><span data-stu-id="70560-300">2</span></span>|| <span data-ttu-id="70560-301">支持选项卡的范围 `contextItem` 集。</span><span class="sxs-lookup"><span data-stu-id="70560-301">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
>  <span data-ttu-id="70560-302">第三方开发人员无法使用 searchUrl 功能。</span><span class="sxs-lookup"><span data-stu-id="70560-302">The searchUrl feature is not available for the third-party developers.</span></span>
> <span data-ttu-id="70560-303">如果你的选项卡需要上下文相关信息来显示相关内容或启动身份验证流，有关详细信息，请参阅获取 Microsoft Teams[上下文选项卡](../../tabs/how-to/access-teams-context.md)。</span><span class="sxs-lookup"><span data-stu-id="70560-303">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, For more information, see [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="70560-304">bots</span><span class="sxs-lookup"><span data-stu-id="70560-304">bots</span></span>

<span data-ttu-id="70560-305">**可选** — 数组</span><span class="sxs-lookup"><span data-stu-id="70560-305">**Optional** — array</span></span>

<span data-ttu-id="70560-306">定义自动程序解决方案以及默认命令属性等可选信息。</span><span class="sxs-lookup"><span data-stu-id="70560-306">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="70560-307">该项目是一个 (，当前每个应用仅允许一个自动程序) 类型的所有元素 &mdash; `object` 。</span><span class="sxs-lookup"><span data-stu-id="70560-307">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="70560-308">只有提供自动程序体验的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="70560-308">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="70560-309">名称</span><span class="sxs-lookup"><span data-stu-id="70560-309">Name</span></span>| <span data-ttu-id="70560-310">类型</span><span class="sxs-lookup"><span data-stu-id="70560-310">Type</span></span>| <span data-ttu-id="70560-311">最大大小</span><span class="sxs-lookup"><span data-stu-id="70560-311">Maximum size</span></span> | <span data-ttu-id="70560-312">必需</span><span class="sxs-lookup"><span data-stu-id="70560-312">Required</span></span> | <span data-ttu-id="70560-313">说明</span><span class="sxs-lookup"><span data-stu-id="70560-313">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="70560-314">string</span><span class="sxs-lookup"><span data-stu-id="70560-314">string</span></span>|<span data-ttu-id="70560-315">64 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-315">64 characters</span></span>|<span data-ttu-id="70560-316">✔</span><span class="sxs-lookup"><span data-stu-id="70560-316">✔</span></span>|<span data-ttu-id="70560-317">使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="70560-317">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="70560-318">这可能与整个应用 [ID 相同](#id)。</span><span class="sxs-lookup"><span data-stu-id="70560-318">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="70560-319">枚举数组</span><span class="sxs-lookup"><span data-stu-id="70560-319">array of enums</span></span>|<span data-ttu-id="70560-320">3</span><span class="sxs-lookup"><span data-stu-id="70560-320">3</span></span>|<span data-ttu-id="70560-321">✔</span><span class="sxs-lookup"><span data-stu-id="70560-321">✔</span></span>|<span data-ttu-id="70560-322">指定自动程序是在 `team` 内的频道上下文中提供体验、在群组聊天 (`groupchat`) 中提供体验，还是仅在单个用户 (`personal`) 范围内提供体验。</span><span class="sxs-lookup"><span data-stu-id="70560-322">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="70560-323">这些选项不具排他性。</span><span class="sxs-lookup"><span data-stu-id="70560-323">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="70560-324">boolean</span><span class="sxs-lookup"><span data-stu-id="70560-324">boolean</span></span>|||<span data-ttu-id="70560-325">描述自动程序是否利用用户提示将自动程序添加到特定频道。</span><span class="sxs-lookup"><span data-stu-id="70560-325">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="70560-326">默认值： **`false`**</span><span class="sxs-lookup"><span data-stu-id="70560-326">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="70560-327">boolean</span><span class="sxs-lookup"><span data-stu-id="70560-327">boolean</span></span>|||<span data-ttu-id="70560-328">指示自动程序是否为单向、仅通知的自动程序，而不是对话自动程序。</span><span class="sxs-lookup"><span data-stu-id="70560-328">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="70560-329">默认值： **`false`**</span><span class="sxs-lookup"><span data-stu-id="70560-329">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="70560-330">boolean</span><span class="sxs-lookup"><span data-stu-id="70560-330">boolean</span></span>|||<span data-ttu-id="70560-331">指示自动程序是否支持在个人聊天中上传/下载文件。</span><span class="sxs-lookup"><span data-stu-id="70560-331">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="70560-332">默认值： **`false`**</span><span class="sxs-lookup"><span data-stu-id="70560-332">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="70560-333">boolean</span><span class="sxs-lookup"><span data-stu-id="70560-333">boolean</span></span>|||<span data-ttu-id="70560-334">指示机器人支持音频呼叫位置的值。</span><span class="sxs-lookup"><span data-stu-id="70560-334">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="70560-335">**重要** 提示：此属性当前为实验属性。</span><span class="sxs-lookup"><span data-stu-id="70560-335">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="70560-336">实验属性可能不完整，并且可能在完全可用之前发生更改。</span><span class="sxs-lookup"><span data-stu-id="70560-336">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="70560-337">它仅供测试和探索之用，不得在生产应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="70560-337">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="70560-338">默认值： **`false`**</span><span class="sxs-lookup"><span data-stu-id="70560-338">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="70560-339">boolean</span><span class="sxs-lookup"><span data-stu-id="70560-339">boolean</span></span>|||<span data-ttu-id="70560-340">指示机器人支持视频呼叫位置的值。</span><span class="sxs-lookup"><span data-stu-id="70560-340">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="70560-341">**重要** 提示：此属性当前为实验属性。</span><span class="sxs-lookup"><span data-stu-id="70560-341">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="70560-342">实验属性可能不完整，并且可能在完全可用之前发生更改。</span><span class="sxs-lookup"><span data-stu-id="70560-342">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="70560-343">它仅供测试和探索之用，不得在生产应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="70560-343">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="70560-344">默认值： **`false`**</span><span class="sxs-lookup"><span data-stu-id="70560-344">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="70560-345">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="70560-345">bots.commandLists</span></span>

<span data-ttu-id="70560-346">自动程序可以推荐给用户的命令的可选列表。</span><span class="sxs-lookup"><span data-stu-id="70560-346">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="70560-347">对象是一个 (，最多包含 2 个元素) 所有类型元素;您必须为自动程序支持的每个范围定义单独的 `object` 命令列表。</span><span class="sxs-lookup"><span data-stu-id="70560-347">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="70560-348">有关详细信息 [，](~/bots/how-to/create-a-bot-commands-menu.md) 请参阅自动程序菜单。</span><span class="sxs-lookup"><span data-stu-id="70560-348">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="70560-349">名称</span><span class="sxs-lookup"><span data-stu-id="70560-349">Name</span></span>| <span data-ttu-id="70560-350">类型</span><span class="sxs-lookup"><span data-stu-id="70560-350">Type</span></span>| <span data-ttu-id="70560-351">最大大小</span><span class="sxs-lookup"><span data-stu-id="70560-351">Maximum size</span></span> | <span data-ttu-id="70560-352">必需</span><span class="sxs-lookup"><span data-stu-id="70560-352">Required</span></span> | <span data-ttu-id="70560-353">说明</span><span class="sxs-lookup"><span data-stu-id="70560-353">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="70560-354">枚举数组</span><span class="sxs-lookup"><span data-stu-id="70560-354">array of enums</span></span>|<span data-ttu-id="70560-355">3</span><span class="sxs-lookup"><span data-stu-id="70560-355">3</span></span>|<span data-ttu-id="70560-356">✔</span><span class="sxs-lookup"><span data-stu-id="70560-356">✔</span></span>|<span data-ttu-id="70560-357">指定命令列表有效的作用域。</span><span class="sxs-lookup"><span data-stu-id="70560-357">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="70560-358">选项包括 `team`、`personal` 和 `groupchat`。</span><span class="sxs-lookup"><span data-stu-id="70560-358">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="70560-359">对象数组</span><span class="sxs-lookup"><span data-stu-id="70560-359">array of objects</span></span>|<span data-ttu-id="70560-360">10  </span><span class="sxs-lookup"><span data-stu-id="70560-360">10</span></span>|<span data-ttu-id="70560-361">✔</span><span class="sxs-lookup"><span data-stu-id="70560-361">✔</span></span>|<span data-ttu-id="70560-362">自动程序支持的命令数组：</span><span class="sxs-lookup"><span data-stu-id="70560-362">An array of commands the bot supports:</span></span><br><span data-ttu-id="70560-363">`title`：自动程序命令名称（字符串，32）</span><span class="sxs-lookup"><span data-stu-id="70560-363">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="70560-364">`description`：命令语法及其参数的简单说明或示例， (字符串，128) 。</span><span class="sxs-lookup"><span data-stu-id="70560-364">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="70560-365">bots.commandLists.commands</span><span class="sxs-lookup"><span data-stu-id="70560-365">bots.commandLists.commands</span></span>

|<span data-ttu-id="70560-366">名称</span><span class="sxs-lookup"><span data-stu-id="70560-366">Name</span></span>| <span data-ttu-id="70560-367">类型</span><span class="sxs-lookup"><span data-stu-id="70560-367">Type</span></span>| <span data-ttu-id="70560-368">最大大小</span><span class="sxs-lookup"><span data-stu-id="70560-368">Maximum size</span></span> | <span data-ttu-id="70560-369">必需</span><span class="sxs-lookup"><span data-stu-id="70560-369">Required</span></span> | <span data-ttu-id="70560-370">说明</span><span class="sxs-lookup"><span data-stu-id="70560-370">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="70560-371">title</span><span class="sxs-lookup"><span data-stu-id="70560-371">title</span></span>|<span data-ttu-id="70560-372">string</span><span class="sxs-lookup"><span data-stu-id="70560-372">string</span></span>|<span data-ttu-id="70560-373">12 </span><span class="sxs-lookup"><span data-stu-id="70560-373">12</span></span>|<span data-ttu-id="70560-374">✔</span><span class="sxs-lookup"><span data-stu-id="70560-374">✔</span></span>|<span data-ttu-id="70560-375">自动程序命令名称。</span><span class="sxs-lookup"><span data-stu-id="70560-375">The bot command name.</span></span>|
|<span data-ttu-id="70560-376">说明</span><span class="sxs-lookup"><span data-stu-id="70560-376">description</span></span>|<span data-ttu-id="70560-377">string</span><span class="sxs-lookup"><span data-stu-id="70560-377">string</span></span>|<span data-ttu-id="70560-378">128 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-378">128 characters</span></span>|<span data-ttu-id="70560-379">✔</span><span class="sxs-lookup"><span data-stu-id="70560-379">✔</span></span>|<span data-ttu-id="70560-380">简单文本说明或命令语法及其参数的示例。</span><span class="sxs-lookup"><span data-stu-id="70560-380">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="70560-381">连接器</span><span class="sxs-lookup"><span data-stu-id="70560-381">connectors</span></span>

<span data-ttu-id="70560-382">**可选** — 数组</span><span class="sxs-lookup"><span data-stu-id="70560-382">**Optional** — array</span></span>

<span data-ttu-id="70560-383">`connectors`块为应用Office 365连接器。</span><span class="sxs-lookup"><span data-stu-id="70560-383">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="70560-384">对象是一个数组， (类型的所有元素) 1 个元素 `object` 。</span><span class="sxs-lookup"><span data-stu-id="70560-384">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="70560-385">只有提供连接器的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="70560-385">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="70560-386">名称</span><span class="sxs-lookup"><span data-stu-id="70560-386">Name</span></span>| <span data-ttu-id="70560-387">类型</span><span class="sxs-lookup"><span data-stu-id="70560-387">Type</span></span>| <span data-ttu-id="70560-388">最大大小</span><span class="sxs-lookup"><span data-stu-id="70560-388">Maximum size</span></span> | <span data-ttu-id="70560-389">必需</span><span class="sxs-lookup"><span data-stu-id="70560-389">Required</span></span> | <span data-ttu-id="70560-390">说明</span><span class="sxs-lookup"><span data-stu-id="70560-390">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="70560-391">string</span><span class="sxs-lookup"><span data-stu-id="70560-391">string</span></span>|<span data-ttu-id="70560-392">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-392">2048 characters</span></span>|<span data-ttu-id="70560-393">✔</span><span class="sxs-lookup"><span data-stu-id="70560-393">✔</span></span>|<span data-ttu-id="70560-394">配置 https:// 时将使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="70560-394">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="70560-395">枚举数组</span><span class="sxs-lookup"><span data-stu-id="70560-395">array of enums</span></span>|<span data-ttu-id="70560-396">1</span><span class="sxs-lookup"><span data-stu-id="70560-396">1</span></span>|<span data-ttu-id="70560-397">✔</span><span class="sxs-lookup"><span data-stu-id="70560-397">✔</span></span>|<span data-ttu-id="70560-398">指定连接器是提供在 中频道上下文中的体验，还是仅针对单个用户 `team` `personal` () 。</span><span class="sxs-lookup"><span data-stu-id="70560-398">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="70560-399">目前，仅 `team` 支持范围。</span><span class="sxs-lookup"><span data-stu-id="70560-399">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="70560-400">string</span><span class="sxs-lookup"><span data-stu-id="70560-400">string</span></span>|<span data-ttu-id="70560-401">64 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-401">64 characters</span></span>|<span data-ttu-id="70560-402">✔</span><span class="sxs-lookup"><span data-stu-id="70560-402">✔</span></span>|<span data-ttu-id="70560-403">连接器的唯一标识符，与连接器开发人员仪表板中的 ID [相匹配](https://aka.ms/connectorsdashboard)。</span><span class="sxs-lookup"><span data-stu-id="70560-403">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="70560-404">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="70560-404">composeExtensions</span></span>

<span data-ttu-id="70560-405">**可选** — 数组</span><span class="sxs-lookup"><span data-stu-id="70560-405">**Optional** — array</span></span>

<span data-ttu-id="70560-406">为应用定义消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="70560-406">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="70560-407">2017 年 11 月，功能名称从"撰写扩展"更改为"邮件扩展"，但清单名称保持不变，以便现有扩展继续工作。</span><span class="sxs-lookup"><span data-stu-id="70560-407">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="70560-408">项目是一个数组， (类型的所有元素) 1 个元素 `object` 。</span><span class="sxs-lookup"><span data-stu-id="70560-408">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="70560-409">只有提供邮件扩展的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="70560-409">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="70560-410">名称</span><span class="sxs-lookup"><span data-stu-id="70560-410">Name</span></span>| <span data-ttu-id="70560-411">类型</span><span class="sxs-lookup"><span data-stu-id="70560-411">Type</span></span> | <span data-ttu-id="70560-412">最大大小</span><span class="sxs-lookup"><span data-stu-id="70560-412">Maximum Size</span></span> | <span data-ttu-id="70560-413">必需</span><span class="sxs-lookup"><span data-stu-id="70560-413">Required</span></span> | <span data-ttu-id="70560-414">说明</span><span class="sxs-lookup"><span data-stu-id="70560-414">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="70560-415">string</span><span class="sxs-lookup"><span data-stu-id="70560-415">string</span></span>|<span data-ttu-id="70560-416">64</span><span class="sxs-lookup"><span data-stu-id="70560-416">64</span></span>|<span data-ttu-id="70560-417">✔</span><span class="sxs-lookup"><span data-stu-id="70560-417">✔</span></span>|<span data-ttu-id="70560-418">自动程序支持消息传递扩展的唯一 Microsoft 应用 ID，在 Bot Framework 中注册。</span><span class="sxs-lookup"><span data-stu-id="70560-418">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="70560-419">这可能与整个应用 ID 相同。</span><span class="sxs-lookup"><span data-stu-id="70560-419">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="70560-420">对象数组</span><span class="sxs-lookup"><span data-stu-id="70560-420">array of objects</span></span>|<span data-ttu-id="70560-421">10  </span><span class="sxs-lookup"><span data-stu-id="70560-421">10</span></span>|<span data-ttu-id="70560-422">✔</span><span class="sxs-lookup"><span data-stu-id="70560-422">✔</span></span>|<span data-ttu-id="70560-423">邮件扩展支持的命令数组。</span><span class="sxs-lookup"><span data-stu-id="70560-423">Array of commands the messaging extension supports.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="70560-424">boolean</span><span class="sxs-lookup"><span data-stu-id="70560-424">boolean</span></span>|||<span data-ttu-id="70560-425">一个值，指示用户是否可以更新邮件扩展的配置。</span><span class="sxs-lookup"><span data-stu-id="70560-425">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="70560-426">默认值：**False**。</span><span class="sxs-lookup"><span data-stu-id="70560-426">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="70560-427">对象数组</span><span class="sxs-lookup"><span data-stu-id="70560-427">array of Objects</span></span>|<span data-ttu-id="70560-428">5 </span><span class="sxs-lookup"><span data-stu-id="70560-428">5</span></span>||<span data-ttu-id="70560-429">允许满足某些条件时调用应用的处理程序列表。</span><span class="sxs-lookup"><span data-stu-id="70560-429">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="70560-430">string</span><span class="sxs-lookup"><span data-stu-id="70560-430">string</span></span>|||<span data-ttu-id="70560-431">消息处理程序的类型。</span><span class="sxs-lookup"><span data-stu-id="70560-431">The type of message handler.</span></span> <span data-ttu-id="70560-432">必须是 `"link"`。</span><span class="sxs-lookup"><span data-stu-id="70560-432">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="70560-433">字符串数组</span><span class="sxs-lookup"><span data-stu-id="70560-433">array of Strings</span></span>|||<span data-ttu-id="70560-434">链接邮件处理程序可以注册的域数组。</span><span class="sxs-lookup"><span data-stu-id="70560-434">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="70560-435">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="70560-435">composeExtensions.commands</span></span>

<span data-ttu-id="70560-436">邮件扩展必须声明一个或多个命令。</span><span class="sxs-lookup"><span data-stu-id="70560-436">Your messaging extension must declare one or more commands.</span></span> <span data-ttu-id="70560-437">每个命令都Microsoft Teams UI 入口点的潜在交互。</span><span class="sxs-lookup"><span data-stu-id="70560-437">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="70560-438">最多有 10 个命令。</span><span class="sxs-lookup"><span data-stu-id="70560-438">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="70560-439">每个命令项都是具有以下结构的对象：</span><span class="sxs-lookup"><span data-stu-id="70560-439">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="70560-440">名称</span><span class="sxs-lookup"><span data-stu-id="70560-440">Name</span></span>| <span data-ttu-id="70560-441">类型</span><span class="sxs-lookup"><span data-stu-id="70560-441">Type</span></span>| <span data-ttu-id="70560-442">最大大小</span><span class="sxs-lookup"><span data-stu-id="70560-442">Maximum size</span></span> | <span data-ttu-id="70560-443">必需</span><span class="sxs-lookup"><span data-stu-id="70560-443">Required</span></span> | <span data-ttu-id="70560-444">说明</span><span class="sxs-lookup"><span data-stu-id="70560-444">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="70560-445">string</span><span class="sxs-lookup"><span data-stu-id="70560-445">string</span></span>|<span data-ttu-id="70560-446">64 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-446">64 characters</span></span>|<span data-ttu-id="70560-447">✔</span><span class="sxs-lookup"><span data-stu-id="70560-447">✔</span></span>|<span data-ttu-id="70560-448">命令的 ID。</span><span class="sxs-lookup"><span data-stu-id="70560-448">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="70560-449">string</span><span class="sxs-lookup"><span data-stu-id="70560-449">string</span></span>|<span data-ttu-id="70560-450">32 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-450">32 characters</span></span>|<span data-ttu-id="70560-451">✔</span><span class="sxs-lookup"><span data-stu-id="70560-451">✔</span></span>|<span data-ttu-id="70560-452">用户友好命令名称。</span><span class="sxs-lookup"><span data-stu-id="70560-452">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="70560-453">string</span><span class="sxs-lookup"><span data-stu-id="70560-453">string</span></span>|<span data-ttu-id="70560-454">64 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-454">64 characters</span></span>||<span data-ttu-id="70560-455">命令的类型。</span><span class="sxs-lookup"><span data-stu-id="70560-455">Type of the command.</span></span> <span data-ttu-id="70560-456">或 `query` `action` 之一。</span><span class="sxs-lookup"><span data-stu-id="70560-456">One of `query` or `action`.</span></span> <span data-ttu-id="70560-457">默认值 **：query**。</span><span class="sxs-lookup"><span data-stu-id="70560-457">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="70560-458">string</span><span class="sxs-lookup"><span data-stu-id="70560-458">string</span></span>|<span data-ttu-id="70560-459">128 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-459">128 characters</span></span>||<span data-ttu-id="70560-460">向用户显示以指示此命令用途的说明。</span><span class="sxs-lookup"><span data-stu-id="70560-460">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="70560-461">boolean</span><span class="sxs-lookup"><span data-stu-id="70560-461">boolean</span></span>|||<span data-ttu-id="70560-462">布尔值指示命令最初是否运行，没有参数。</span><span class="sxs-lookup"><span data-stu-id="70560-462">A boolean value indicates whether the command runs initially with no parameters.</span></span> <span data-ttu-id="70560-463">默认为 **false**。</span><span class="sxs-lookup"><span data-stu-id="70560-463">Default is **false**.</span></span>|
|`context`|<span data-ttu-id="70560-464">字符串数组</span><span class="sxs-lookup"><span data-stu-id="70560-464">array of Strings</span></span>|<span data-ttu-id="70560-465">3</span><span class="sxs-lookup"><span data-stu-id="70560-465">3</span></span>||<span data-ttu-id="70560-466">定义可以从何处调用邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="70560-466">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="70560-467">、 `compose` 、 的任意 `commandBox` 组合 `message` 。</span><span class="sxs-lookup"><span data-stu-id="70560-467">Any combination of`compose`,`commandBox`,`message`.</span></span> <span data-ttu-id="70560-468">默认值为“`["compose","commandBox"]`”。</span><span class="sxs-lookup"><span data-stu-id="70560-468">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="70560-469">boolean</span><span class="sxs-lookup"><span data-stu-id="70560-469">boolean</span></span>|||<span data-ttu-id="70560-470">一个布尔值，指示它是否必须动态提取任务模块。</span><span class="sxs-lookup"><span data-stu-id="70560-470">A boolean value that indicates if it must fetch the task module dynamically.</span></span> <span data-ttu-id="70560-471">默认为 **false**。</span><span class="sxs-lookup"><span data-stu-id="70560-471">Default is **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="70560-472">object</span><span class="sxs-lookup"><span data-stu-id="70560-472">object</span></span>|||<span data-ttu-id="70560-473">指定在使用消息传递扩展命令时要预加载的任务模块。</span><span class="sxs-lookup"><span data-stu-id="70560-473">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="70560-474">string</span><span class="sxs-lookup"><span data-stu-id="70560-474">string</span></span>|<span data-ttu-id="70560-475">64 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-475">64 characters</span></span>||<span data-ttu-id="70560-476">初始对话框标题。</span><span class="sxs-lookup"><span data-stu-id="70560-476">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="70560-477">string</span><span class="sxs-lookup"><span data-stu-id="70560-477">string</span></span>|||<span data-ttu-id="70560-478">对话框宽度 - 以像素为单位的一个数字或默认布局，例如"large"、"medium"或"small"。</span><span class="sxs-lookup"><span data-stu-id="70560-478">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="70560-479">string</span><span class="sxs-lookup"><span data-stu-id="70560-479">string</span></span>|||<span data-ttu-id="70560-480">对话框高度 - 以像素为单位的一个数字或默认布局，例如"large"、"medium"或"small"。</span><span class="sxs-lookup"><span data-stu-id="70560-480">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="70560-481">string</span><span class="sxs-lookup"><span data-stu-id="70560-481">string</span></span>|||<span data-ttu-id="70560-482">初始 Web 视图 URL。</span><span class="sxs-lookup"><span data-stu-id="70560-482">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="70560-483">对象数组</span><span class="sxs-lookup"><span data-stu-id="70560-483">array of object</span></span>|<span data-ttu-id="70560-484">5 个项目</span><span class="sxs-lookup"><span data-stu-id="70560-484">5 items</span></span>|<span data-ttu-id="70560-485">✔</span><span class="sxs-lookup"><span data-stu-id="70560-485">✔</span></span>|<span data-ttu-id="70560-486">命令采用的参数列表。</span><span class="sxs-lookup"><span data-stu-id="70560-486">The list of parameters the command takes.</span></span> <span data-ttu-id="70560-487">最小值：1;最大值：5。</span><span class="sxs-lookup"><span data-stu-id="70560-487">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="70560-488">string</span><span class="sxs-lookup"><span data-stu-id="70560-488">string</span></span>|<span data-ttu-id="70560-489">64 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-489">64 characters</span></span>|<span data-ttu-id="70560-490">✔</span><span class="sxs-lookup"><span data-stu-id="70560-490">✔</span></span>|<span data-ttu-id="70560-491">显示在客户端中的参数的名称。</span><span class="sxs-lookup"><span data-stu-id="70560-491">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="70560-492">这包括在用户请求中。</span><span class="sxs-lookup"><span data-stu-id="70560-492">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="70560-493">string</span><span class="sxs-lookup"><span data-stu-id="70560-493">string</span></span>|<span data-ttu-id="70560-494">32 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-494">32 characters</span></span>|<span data-ttu-id="70560-495">✔</span><span class="sxs-lookup"><span data-stu-id="70560-495">✔</span></span>|<span data-ttu-id="70560-496">参数的用户友好标题。</span><span class="sxs-lookup"><span data-stu-id="70560-496">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="70560-497">string</span><span class="sxs-lookup"><span data-stu-id="70560-497">string</span></span>|<span data-ttu-id="70560-498">128 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-498">128 characters</span></span>||<span data-ttu-id="70560-499">描述此参数用途的用户友好字符串。</span><span class="sxs-lookup"><span data-stu-id="70560-499">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="70560-500">string</span><span class="sxs-lookup"><span data-stu-id="70560-500">string</span></span>|<span data-ttu-id="70560-501">512 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-501">512 characters</span></span>||<span data-ttu-id="70560-502">参数的初始值。</span><span class="sxs-lookup"><span data-stu-id="70560-502">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="70560-503">string</span><span class="sxs-lookup"><span data-stu-id="70560-503">string</span></span>|<span data-ttu-id="70560-504">128 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-504">128 characters</span></span>||<span data-ttu-id="70560-505">定义在任务模块上显示的控件的类型 `fetchTask: true` 。</span><span class="sxs-lookup"><span data-stu-id="70560-505">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="70560-506">之一 `text, textarea, number, date, time, toggle, choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="70560-506">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="70560-507">对象数组</span><span class="sxs-lookup"><span data-stu-id="70560-507">array of objects</span></span>|<span data-ttu-id="70560-508">10 个项目</span><span class="sxs-lookup"><span data-stu-id="70560-508">10 items</span></span>||<span data-ttu-id="70560-509">的选项 `choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="70560-509">The choice options for the`choiceset`.</span></span> <span data-ttu-id="70560-510">仅在 为 `parameter.inputType` `choiceset` 时使用 。</span><span class="sxs-lookup"><span data-stu-id="70560-510">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="70560-511">string</span><span class="sxs-lookup"><span data-stu-id="70560-511">string</span></span>|<span data-ttu-id="70560-512">128 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-512">128 characters</span></span>|<span data-ttu-id="70560-513">✔</span><span class="sxs-lookup"><span data-stu-id="70560-513">✔</span></span>|<span data-ttu-id="70560-514">选项的标题。</span><span class="sxs-lookup"><span data-stu-id="70560-514">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="70560-515">string</span><span class="sxs-lookup"><span data-stu-id="70560-515">string</span></span>|<span data-ttu-id="70560-516">512 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-516">512 characters</span></span>|<span data-ttu-id="70560-517">✔</span><span class="sxs-lookup"><span data-stu-id="70560-517">✔</span></span>|<span data-ttu-id="70560-518">选项的值。</span><span class="sxs-lookup"><span data-stu-id="70560-518">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="70560-519">权限</span><span class="sxs-lookup"><span data-stu-id="70560-519">permissions</span></span>

<span data-ttu-id="70560-520">**可选** — 字符串数组</span><span class="sxs-lookup"><span data-stu-id="70560-520">**Optional** — array of strings</span></span>

<span data-ttu-id="70560-521">一个数组，指定应用请求哪些权限，使最终用户 `string` 知道扩展的执行方式。</span><span class="sxs-lookup"><span data-stu-id="70560-521">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension performs.</span></span> <span data-ttu-id="70560-522">以下选项非独占：</span><span class="sxs-lookup"><span data-stu-id="70560-522">The following options are non-exclusive:</span></span>

* <span data-ttu-id="70560-523">`identity`&emsp;需要用户标识信息。</span><span class="sxs-lookup"><span data-stu-id="70560-523">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="70560-524">`messageTeamMembers`&emsp;需要向团队成员发送直接消息的权限。</span><span class="sxs-lookup"><span data-stu-id="70560-524">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="70560-525">在应用更新期间更改这些权限，会导致用户在运行更新后的应用后重复同意过程。</span><span class="sxs-lookup"><span data-stu-id="70560-525">Changing these permissions during app update, causes your users to repeat the consent process after they run the updated app.</span></span> <span data-ttu-id="70560-526">有关详细信息 [，请参阅更新](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) 应用。</span><span class="sxs-lookup"><span data-stu-id="70560-526">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="70560-527">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="70560-527">devicePermissions</span></span>

<span data-ttu-id="70560-528">**可选** — 字符串数组</span><span class="sxs-lookup"><span data-stu-id="70560-528">**Optional** — array of strings</span></span>

<span data-ttu-id="70560-529">在应用请求访问的用户设备上提供本机功能。</span><span class="sxs-lookup"><span data-stu-id="70560-529">Provides the native features on a user's device that your app requests access to.</span></span> <span data-ttu-id="70560-530">选项有：</span><span class="sxs-lookup"><span data-stu-id="70560-530">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="70560-531">validDomains</span><span class="sxs-lookup"><span data-stu-id="70560-531">validDomains</span></span>

<span data-ttu-id="70560-532">**可选**，除非 **有说明** ，否则必选。</span><span class="sxs-lookup"><span data-stu-id="70560-532">**Optional**, except **Required** where noted.</span></span>

<span data-ttu-id="70560-533">应用预期在客户端内加载的网站的有效Teams列表。</span><span class="sxs-lookup"><span data-stu-id="70560-533">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="70560-534">域列表可以包含通配符，例如 `*.example.com` ， 。</span><span class="sxs-lookup"><span data-stu-id="70560-534">Domain listings can include wildcards, for example, `*.example.com`.</span></span> <span data-ttu-id="70560-535">这完全匹配域的一个段;如果需要匹配，请使用 `a.b.example.com` `*.*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="70560-535">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="70560-536">如果你的选项卡配置或内容 UI 需要导航到除用于选项卡配置的其他任何其他域，则必须在此处指定该域。</span><span class="sxs-lookup"><span data-stu-id="70560-536">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="70560-537">不需要 **在** 应用中包含要支持的标识提供程序的域。</span><span class="sxs-lookup"><span data-stu-id="70560-537">It is **not** necessary to include the domains of identity providers you want to support in your app.</span></span> <span data-ttu-id="70560-538">例如，若要使用 Google ID 进行身份验证，必须重定向到 accounts.google.com，但不得在 `validDomains[]` accounts.google.com。</span><span class="sxs-lookup"><span data-stu-id="70560-538">For example, to authenticate using a Google ID, it is required to redirect to accounts.google.com, however, you must not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="70560-539">Teams需要自己的 sharepoint URL 正常运行的应用程序，请包括其有效域列表中的"{teamsitedomain}"。</span><span class="sxs-lookup"><span data-stu-id="70560-539">Teams apps that require their own sharepoint URLs to function well, includes "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70560-540">不要直接添加或通过通配符添加超出您控制的域。</span><span class="sxs-lookup"><span data-stu-id="70560-540">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="70560-541">例如， `yourapp.onmicrosoft.com` 是有效的，但 `*.onmicrosoft.com` 是 无效。</span><span class="sxs-lookup"><span data-stu-id="70560-541">For example, `yourapp.onmicrosoft.com` is valid, however, `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="70560-542">对象是包含类型 的所有元素的数组 `string` 。</span><span class="sxs-lookup"><span data-stu-id="70560-542">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="70560-543">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="70560-543">webApplicationInfo</span></span>

<span data-ttu-id="70560-544">**可选** — object</span><span class="sxs-lookup"><span data-stu-id="70560-544">**Optional** — object</span></span>

<span data-ttu-id="70560-545">提供你的Azure Active Directory (AAD) 应用 ID 和 Microsoft Graph 信息，以帮助用户无缝登录你的应用。</span><span class="sxs-lookup"><span data-stu-id="70560-545">Provide your Azure Active Directory (AAD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="70560-546">如果你的应用在 AAD 中注册，则必须提供应用 ID，以便管理员可以轻松地查看权限，并授予管理员Teams许可。</span><span class="sxs-lookup"><span data-stu-id="70560-546">If your app is registered in AAD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="70560-547">名称</span><span class="sxs-lookup"><span data-stu-id="70560-547">Name</span></span>| <span data-ttu-id="70560-548">类型</span><span class="sxs-lookup"><span data-stu-id="70560-548">Type</span></span>| <span data-ttu-id="70560-549">最大大小</span><span class="sxs-lookup"><span data-stu-id="70560-549">Maximum size</span></span> | <span data-ttu-id="70560-550">必需</span><span class="sxs-lookup"><span data-stu-id="70560-550">Required</span></span> | <span data-ttu-id="70560-551">说明</span><span class="sxs-lookup"><span data-stu-id="70560-551">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="70560-552">string</span><span class="sxs-lookup"><span data-stu-id="70560-552">string</span></span>|<span data-ttu-id="70560-553">36 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-553">36 characters</span></span>|<span data-ttu-id="70560-554">✔</span><span class="sxs-lookup"><span data-stu-id="70560-554">✔</span></span>|<span data-ttu-id="70560-555">应用的 AAD 应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="70560-555">AAD application id of the app.</span></span> <span data-ttu-id="70560-556">此 ID 必须是 GUID。</span><span class="sxs-lookup"><span data-stu-id="70560-556">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="70560-557">string</span><span class="sxs-lookup"><span data-stu-id="70560-557">string</span></span>|<span data-ttu-id="70560-558">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-558">2048 characters</span></span>|<span data-ttu-id="70560-559">✔</span><span class="sxs-lookup"><span data-stu-id="70560-559">✔</span></span>|<span data-ttu-id="70560-560">用于获取 SSO 身份验证令牌的应用的资源 URL。</span><span class="sxs-lookup"><span data-stu-id="70560-560">Resource URL of app for acquiring auth token for SSO.</span></span> </br> <span data-ttu-id="70560-561">**注意：** 如果不使用 SSO，请确保在此字段中向应用清单输入虚拟字符串值，以避免 https://notapplicable 错误响应。</span><span class="sxs-lookup"><span data-stu-id="70560-561">**NOTE:** If you are not using SSO, ensure that you enter a dummy string value in this field to your app manifest, for example, https://notapplicable to avoid an error response.</span></span> |
|`applicationPermissions`|<span data-ttu-id="70560-562">array of strings</span><span class="sxs-lookup"><span data-stu-id="70560-562">array of strings</span></span>|<span data-ttu-id="70560-563">128 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-563">128 characters</span></span>||<span data-ttu-id="70560-564">指定具体 [资源特定许可](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="70560-564">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="70560-565">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="70560-565">showLoadingIndicator</span></span>

<span data-ttu-id="70560-566">**可选** — 布尔值</span><span class="sxs-lookup"><span data-stu-id="70560-566">**Optional** — boolean</span></span>

<span data-ttu-id="70560-567">指示在加载应用或选项卡时是否显示加载指示器。</span><span class="sxs-lookup"><span data-stu-id="70560-567">Indicates whether or not to show the loading indicator when an app or tab is loading.</span></span> <span data-ttu-id="70560-568">默认为 **false**。</span><span class="sxs-lookup"><span data-stu-id="70560-568">Default is **false**.</span></span>
>[!NOTE]
><span data-ttu-id="70560-569">如果在应用清单中选择 true，若要正确加载页面，请修改选项卡和任务模块的内容页，如显示本机加载指示器文档 `showLoadingIndicator` 中所述。 [](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)</span><span class="sxs-lookup"><span data-stu-id="70560-569">If you select`showLoadingIndicator` as true in your app manifest, to load the page correctly, modify the content pages of your tabs and task modules as described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="70560-570">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="70560-570">isFullScreen</span></span>

 <span data-ttu-id="70560-571">**可选** — 布尔值</span><span class="sxs-lookup"><span data-stu-id="70560-571">**Optional** — boolean</span></span>

<span data-ttu-id="70560-572">指示在具有或没有选项卡标题栏的情况下呈现个人应用。</span><span class="sxs-lookup"><span data-stu-id="70560-572">Indicate where a personal app is rendered with or without a tab header bar.</span></span> <span data-ttu-id="70560-573">默认为 **false**。</span><span class="sxs-lookup"><span data-stu-id="70560-573">Default is **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="70560-574">activities</span><span class="sxs-lookup"><span data-stu-id="70560-574">activities</span></span>

<span data-ttu-id="70560-575">**可选** — object</span><span class="sxs-lookup"><span data-stu-id="70560-575">**Optional** — object</span></span>

<span data-ttu-id="70560-576">定义应用用于发布用户活动源的属性。</span><span class="sxs-lookup"><span data-stu-id="70560-576">Define the properties your app uses to post a user activity feed.</span></span>

|<span data-ttu-id="70560-577">名称</span><span class="sxs-lookup"><span data-stu-id="70560-577">Name</span></span>| <span data-ttu-id="70560-578">类型</span><span class="sxs-lookup"><span data-stu-id="70560-578">Type</span></span>| <span data-ttu-id="70560-579">最大大小</span><span class="sxs-lookup"><span data-stu-id="70560-579">Maximum size</span></span> | <span data-ttu-id="70560-580">必需</span><span class="sxs-lookup"><span data-stu-id="70560-580">Required</span></span> | <span data-ttu-id="70560-581">说明</span><span class="sxs-lookup"><span data-stu-id="70560-581">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="70560-582">对象数组</span><span class="sxs-lookup"><span data-stu-id="70560-582">array of Objects</span></span>|<span data-ttu-id="70560-583">128 项</span><span class="sxs-lookup"><span data-stu-id="70560-583">128 items</span></span>| | <span data-ttu-id="70560-584">提供你的应用可以发布给用户活动源的活动类型。</span><span class="sxs-lookup"><span data-stu-id="70560-584">Provide the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="70560-585">activities.activityTypes</span><span class="sxs-lookup"><span data-stu-id="70560-585">activities.activityTypes</span></span>

|<span data-ttu-id="70560-586">名称</span><span class="sxs-lookup"><span data-stu-id="70560-586">Name</span></span>| <span data-ttu-id="70560-587">类型</span><span class="sxs-lookup"><span data-stu-id="70560-587">Type</span></span>| <span data-ttu-id="70560-588">最大大小</span><span class="sxs-lookup"><span data-stu-id="70560-588">Maximum size</span></span> | <span data-ttu-id="70560-589">必需</span><span class="sxs-lookup"><span data-stu-id="70560-589">Required</span></span> | <span data-ttu-id="70560-590">说明</span><span class="sxs-lookup"><span data-stu-id="70560-590">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="70560-591">string</span><span class="sxs-lookup"><span data-stu-id="70560-591">string</span></span>|<span data-ttu-id="70560-592">32 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-592">32 characters</span></span>|<span data-ttu-id="70560-593">✔</span><span class="sxs-lookup"><span data-stu-id="70560-593">✔</span></span>|<span data-ttu-id="70560-594">通知类型。</span><span class="sxs-lookup"><span data-stu-id="70560-594">The notification type.</span></span> <span data-ttu-id="70560-595">*请参阅下文*。</span><span class="sxs-lookup"><span data-stu-id="70560-595">*See below*.</span></span>|
|`description`|<span data-ttu-id="70560-596">string</span><span class="sxs-lookup"><span data-stu-id="70560-596">string</span></span>|<span data-ttu-id="70560-597">128 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-597">128 characters</span></span>|<span data-ttu-id="70560-598">✔</span><span class="sxs-lookup"><span data-stu-id="70560-598">✔</span></span>|<span data-ttu-id="70560-599">通知的简要说明。</span><span class="sxs-lookup"><span data-stu-id="70560-599">A brief description of the notification.</span></span> <span data-ttu-id="70560-600">*请参阅下文*。</span><span class="sxs-lookup"><span data-stu-id="70560-600">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="70560-601">string</span><span class="sxs-lookup"><span data-stu-id="70560-601">string</span></span>|<span data-ttu-id="70560-602">128 个字符</span><span class="sxs-lookup"><span data-stu-id="70560-602">128 characters</span></span>|<span data-ttu-id="70560-603">✔</span><span class="sxs-lookup"><span data-stu-id="70560-603">✔</span></span>|<span data-ttu-id="70560-604">例如："{actor} 已创建任务 {taskId}"</span><span class="sxs-lookup"><span data-stu-id="70560-604">Ex: "{actor} created task {taskId} for you"</span></span>|

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

## <a name="defaultinstallscope"></a><span data-ttu-id="70560-605">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="70560-605">defaultInstallScope</span></span>

<span data-ttu-id="70560-606">**可选** - string</span><span class="sxs-lookup"><span data-stu-id="70560-606">**Optional** - string</span></span>

<span data-ttu-id="70560-607">指定默认情况下为此应用定义的安装范围。</span><span class="sxs-lookup"><span data-stu-id="70560-607">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="70560-608">定义的范围将是当用户尝试添加应用时按钮上显示的选项。</span><span class="sxs-lookup"><span data-stu-id="70560-608">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="70560-609">选项有：</span><span class="sxs-lookup"><span data-stu-id="70560-609">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="70560-610">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="70560-610">defaultGroupCapability</span></span>

<span data-ttu-id="70560-611">**可选** - object</span><span class="sxs-lookup"><span data-stu-id="70560-611">**Optional** - object</span></span>

<span data-ttu-id="70560-612">选择组安装范围后，它将在用户安装应用时定义默认功能。</span><span class="sxs-lookup"><span data-stu-id="70560-612">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="70560-613">选项有：</span><span class="sxs-lookup"><span data-stu-id="70560-613">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="70560-614">名称</span><span class="sxs-lookup"><span data-stu-id="70560-614">Name</span></span>| <span data-ttu-id="70560-615">类型</span><span class="sxs-lookup"><span data-stu-id="70560-615">Type</span></span>| <span data-ttu-id="70560-616">最大大小</span><span class="sxs-lookup"><span data-stu-id="70560-616">Maximum size</span></span> | <span data-ttu-id="70560-617">必需</span><span class="sxs-lookup"><span data-stu-id="70560-617">Required</span></span> | <span data-ttu-id="70560-618">说明</span><span class="sxs-lookup"><span data-stu-id="70560-618">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="70560-619">string</span><span class="sxs-lookup"><span data-stu-id="70560-619">string</span></span>|||<span data-ttu-id="70560-620">当选择的安装范围为 `team` 时，此字段指定可用的默认功能。</span><span class="sxs-lookup"><span data-stu-id="70560-620">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="70560-621">选项 `tab` ：、 `bot` 或 `connector` 。</span><span class="sxs-lookup"><span data-stu-id="70560-621">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="70560-622">string</span><span class="sxs-lookup"><span data-stu-id="70560-622">string</span></span>|||<span data-ttu-id="70560-623">当选择的安装范围为 `groupchat` 时，此字段指定可用的默认功能。</span><span class="sxs-lookup"><span data-stu-id="70560-623">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="70560-624">选项 `tab` ：、 `bot` 或 `connector` 。</span><span class="sxs-lookup"><span data-stu-id="70560-624">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="70560-625">string</span><span class="sxs-lookup"><span data-stu-id="70560-625">string</span></span>|||<span data-ttu-id="70560-626">当选择的安装范围为 `meetings` 时，此字段指定可用的默认功能。</span><span class="sxs-lookup"><span data-stu-id="70560-626">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="70560-627">选项 `tab` ：、 `bot` 或 `connector` 。</span><span class="sxs-lookup"><span data-stu-id="70560-627">Options: `tab`, `bot`, or `connector`.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="70560-628">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="70560-628">configurableProperties</span></span>

<span data-ttu-id="70560-629">**可选** - 数组</span><span class="sxs-lookup"><span data-stu-id="70560-629">**Optional** - array</span></span>

<span data-ttu-id="70560-630">`configurableProperties`此块定义管理员可Teams的应用程序属性。</span><span class="sxs-lookup"><span data-stu-id="70560-630">The `configurableProperties` block defines the app properties that Teams admins can customize.</span></span> <span data-ttu-id="70560-631">有关详细信息，请参阅启用 [应用自定义](~/concepts/design/enable-app-customization.md)。</span><span class="sxs-lookup"><span data-stu-id="70560-631">For more information, see [enable app customization](~/concepts/design/enable-app-customization.md).</span></span>

> [!NOTE]
> <span data-ttu-id="70560-632">必须定义至少一个属性。</span><span class="sxs-lookup"><span data-stu-id="70560-632">A minimum of one property must be defined.</span></span> <span data-ttu-id="70560-633">最多可以在此块中定义九个属性。</span><span class="sxs-lookup"><span data-stu-id="70560-633">You can define a maximum of nine properties in this block.</span></span>

<span data-ttu-id="70560-634">可以定义以下任一属性：</span><span class="sxs-lookup"><span data-stu-id="70560-634">You can define any of the following properties:</span></span>

* <span data-ttu-id="70560-635">`name`：应用显示名称。</span><span class="sxs-lookup"><span data-stu-id="70560-635">`name`: The app's display name.</span></span>
* <span data-ttu-id="70560-636">`shortDescription`：应用的简短说明。</span><span class="sxs-lookup"><span data-stu-id="70560-636">`shortDescription`: The app's short description.</span></span>
* <span data-ttu-id="70560-637">`longDescription`：应用的详细说明。</span><span class="sxs-lookup"><span data-stu-id="70560-637">`longDescription`: The app's detailed description.</span></span>
* <span data-ttu-id="70560-638">`smallImageUrl`：应用的大纲图标。</span><span class="sxs-lookup"><span data-stu-id="70560-638">`smallImageUrl`: The app's outline icon.</span></span>
* <span data-ttu-id="70560-639">`largeImageUrl`：应用的颜色图标。</span><span class="sxs-lookup"><span data-stu-id="70560-639">`largeImageUrl`: The app's color icon.</span></span>
* <span data-ttu-id="70560-640">`accentColor`：要与 和 结合使用用作大纲图标背景的颜色。</span><span class="sxs-lookup"><span data-stu-id="70560-640">`accentColor`: The color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="70560-641">`developerUrl`：开发人员网站的 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="70560-641">`developerUrl`: The HTTPS URL of the developer's website.</span></span>
* <span data-ttu-id="70560-642">`privacyUrl`：开发人员隐私策略的 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="70560-642">`privacyUrl`: The HTTPS URL of the developer's privacy policy.</span></span>
* <span data-ttu-id="70560-643">`termsOfUseUrl`：开发人员使用条款的 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="70560-643">`termsOfUseUrl`: The HTTPS URL of the developer's terms of use.</span></span>
