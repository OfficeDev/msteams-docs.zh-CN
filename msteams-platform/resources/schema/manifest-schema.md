---
title: 清单架构参考
description: 介绍 Microsoft Teams 的清单架构
ms.topic: reference
ms.author: lajanuar
keywords: teams 清单架构
ms.openlocfilehash: fc7af73dd90ae74d76645281d9e761b91678873b
ms.sourcegitcommit: e78c9f51c4538212c53bb6c6a45a09d994896f09
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/05/2021
ms.locfileid: "51585839"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="f9d4e-104">参考：Microsoft Teams 的清单架构</span><span class="sxs-lookup"><span data-stu-id="f9d4e-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="f9d4e-105">Teams 清单介绍了应用如何集成到 Microsoft Teams 产品。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-105">The Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="f9d4e-106">清单必须符合 托管在 的架构 [`https://developer.microsoft.com/json-schemas/teams/v1.9/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.9/MicrosoftTeams.schema.json) 。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.9/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.9/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="f9d4e-107">早期版本 1.0-1.4 也受 URL ("v1.x") 。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="f9d4e-108">以下架构示例显示了所有扩展性选项。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="f9d4e-109">示例完整清单</span><span class="sxs-lookup"><span data-stu-id="f9d4e-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.9/MicrosoftTeams.schema.json",
  "manifestVersion": "1.9",
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
  "defaultGroupCapability": {"meetings": "tab" , "team": "bot", "groupchat": "bot"}
}
```

<span data-ttu-id="f9d4e-110">该架构定义以下属性：</span><span class="sxs-lookup"><span data-stu-id="f9d4e-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="f9d4e-111">$schema</span><span class="sxs-lookup"><span data-stu-id="f9d4e-111">$schema</span></span>

<span data-ttu-id="f9d4e-112">可选，但推荐 — 字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-112">Optional, but recommended — string</span></span>

<span data-ttu-id="f9d4e-113">引用 https:// JSON 架构的 URL。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="f9d4e-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="f9d4e-114">manifestVersion</span></span>

<span data-ttu-id="f9d4e-115">**必需** — 字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-115">**Required** — string</span></span>

<span data-ttu-id="f9d4e-116">此清单使用的清单架构版本。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-116">The version of manifest schema this manifest is using.</span></span> <span data-ttu-id="f9d4e-117">必须为 1.9。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-117">It must be 1.9.</span></span>

## <a name="version"></a><span data-ttu-id="f9d4e-118">version</span><span class="sxs-lookup"><span data-stu-id="f9d4e-118">version</span></span>

<span data-ttu-id="f9d4e-119">**必需** — 字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-119">**Required** — string</span></span>

<span data-ttu-id="f9d4e-120">特定应用的版本。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-120">The version of a specific app.</span></span> <span data-ttu-id="f9d4e-121">如果更新清单中的某些内容，则版本也必须递增。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-121">If you update something in your manifest, the version must be incremented too.</span></span> <span data-ttu-id="f9d4e-122">这样，在安装新清单时，它将覆盖现有清单，并且用户会收到新功能。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-122">This way, when the new manifest is installed, it overwrites the existing one and the user receives the new functionality.</span></span> <span data-ttu-id="f9d4e-123">如果此应用已提交到应用商店，则必须重新提交和重新验证新的清单。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-123">If this app was submitted to the store, the new manifest must be re-submitted and re-validated.</span></span> <span data-ttu-id="f9d4e-124">应用用户会在清单获得批准后的数小时内自动收到新的更新清单。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-124">The app users receive the new updated manifest automatically within few hours after the manifest is approved.</span></span>

<span data-ttu-id="f9d4e-125">如果应用对权限的请求发生变化，将提示用户升级并重新同意应用。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-125">If the app requests for permissions change, the users are prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="f9d4e-126">此版本字符串必须遵循 [Semver](http://semver.org/) 标准 (MAJOR。MINOR。PATCH) 。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="f9d4e-127">id</span><span class="sxs-lookup"><span data-stu-id="f9d4e-127">id</span></span>

<span data-ttu-id="f9d4e-128">**必需** - Microsoft 应用 ID</span><span class="sxs-lookup"><span data-stu-id="f9d4e-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="f9d4e-129">ID 是 Microsoft 为应用生成的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-129">The ID is a unique Microsoft-generated identifier for the app.</span></span> <span data-ttu-id="f9d4e-130">如果你的自动程序通过 Microsoft Bot Framework 注册，或者你的选项卡的 Web 应用已经使用 Microsoft 登录，则你有一个 ID。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-130">You have an ID if your bot is registered through the Microsoft Bot Framework or your tab's web app already signs in with Microsoft.</span></span> <span data-ttu-id="f9d4e-131">必须在此处输入 ID。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-131">You must enter the ID here.</span></span> <span data-ttu-id="f9d4e-132">否则，必须在"我的应用程序"门户的 Microsoft 应用程序注册门户 ([一](https://apps.dev.microsoft.com)) 。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-132">Otherwise, you must generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)).</span></span> <span data-ttu-id="f9d4e-133">如果添加自动程序，请使用同一 ID。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-133">Use the same ID if you add a bot.</span></span>

> [!NOTE]
> <span data-ttu-id="f9d4e-134">如果你要向 AppSource 中的现有应用提交更新，则清单中的 ID 不得修改。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-134">If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="f9d4e-135">developer</span><span class="sxs-lookup"><span data-stu-id="f9d4e-135">developer</span></span>

<span data-ttu-id="f9d4e-136">**必需** — object</span><span class="sxs-lookup"><span data-stu-id="f9d4e-136">**Required** — object</span></span>

<span data-ttu-id="f9d4e-137">提供有关你的公司的信息。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-137">Gives information about your company.</span></span> <span data-ttu-id="f9d4e-138">对于提交到 AppSource (Office 应用商店) ，这些值必须与 AppSource 条目中的信息匹配。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-138">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="f9d4e-139">有关 [其他信息，](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) 请参阅发布指南。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-139">See the [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="f9d4e-140">名称</span><span class="sxs-lookup"><span data-stu-id="f9d4e-140">Name</span></span>| <span data-ttu-id="f9d4e-141">最大大小</span><span class="sxs-lookup"><span data-stu-id="f9d4e-141">Maximum size</span></span> | <span data-ttu-id="f9d4e-142">必需</span><span class="sxs-lookup"><span data-stu-id="f9d4e-142">Required</span></span> | <span data-ttu-id="f9d4e-143">Description</span><span class="sxs-lookup"><span data-stu-id="f9d4e-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="f9d4e-144">32 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-144">32 characters</span></span>|<span data-ttu-id="f9d4e-145">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-145">✔</span></span>|<span data-ttu-id="f9d4e-146">开发人员显示名称的指南。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="f9d4e-147">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-147">2048 characters</span></span>|<span data-ttu-id="f9d4e-148">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-148">✔</span></span>|<span data-ttu-id="f9d4e-149">the https:// URL to the developer's website.</span><span class="sxs-lookup"><span data-stu-id="f9d4e-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="f9d4e-150">此链接必须将用户指向你的公司或特定于产品的登陆页面。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-150">This link must take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="f9d4e-151">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-151">2048 characters</span></span>|<span data-ttu-id="f9d4e-152">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-152">✔</span></span>|<span data-ttu-id="f9d4e-153">the https:// URL to the developer's privacy policy.</span><span class="sxs-lookup"><span data-stu-id="f9d4e-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="f9d4e-154">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-154">2048 characters</span></span>|<span data-ttu-id="f9d4e-155">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-155">✔</span></span>|<span data-ttu-id="f9d4e-156">the https:// URL to the developer's use terms.</span><span class="sxs-lookup"><span data-stu-id="f9d4e-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="f9d4e-157">10 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-157">10 characters</span></span>| |<span data-ttu-id="f9d4e-158">**可选** 标识生成应用的合作伙伴组织的 Microsoft 合作伙伴网络 ID。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-158">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="f9d4e-159">name</span><span class="sxs-lookup"><span data-stu-id="f9d4e-159">name</span></span>

<span data-ttu-id="f9d4e-160">**必需** — object</span><span class="sxs-lookup"><span data-stu-id="f9d4e-160">**Required** — object</span></span>

<span data-ttu-id="f9d4e-161">在 Teams 体验中向用户显示的应用体验名称。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-161">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="f9d4e-162">对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-162">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="f9d4e-163">和 `short` `full` 的值必须不同。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-163">The values of `short` and `full` must be different.</span></span>

|<span data-ttu-id="f9d4e-164">名称</span><span class="sxs-lookup"><span data-stu-id="f9d4e-164">Name</span></span>| <span data-ttu-id="f9d4e-165">最大大小</span><span class="sxs-lookup"><span data-stu-id="f9d4e-165">Maximum size</span></span> | <span data-ttu-id="f9d4e-166">必需</span><span class="sxs-lookup"><span data-stu-id="f9d4e-166">Required</span></span> | <span data-ttu-id="f9d4e-167">Description</span><span class="sxs-lookup"><span data-stu-id="f9d4e-167">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="f9d4e-168">30 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-168">30 characters</span></span>|<span data-ttu-id="f9d4e-169">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-169">✔</span></span>|<span data-ttu-id="f9d4e-170">应用的显示名称。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-170">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="f9d4e-171">100 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-171">100 characters</span></span>||<span data-ttu-id="f9d4e-172">应用的完整名称，在完整应用名称超过 30 个字符时使用。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-172">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="f9d4e-173">说明</span><span class="sxs-lookup"><span data-stu-id="f9d4e-173">description</span></span>

<span data-ttu-id="f9d4e-174">**必需** — object</span><span class="sxs-lookup"><span data-stu-id="f9d4e-174">**Required** — object</span></span>

<span data-ttu-id="f9d4e-175">向用户描述你的应用。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-175">Describes your app to users.</span></span> <span data-ttu-id="f9d4e-176">对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-176">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="f9d4e-177">确保你的描述准确地描述了你的体验，并提供相关信息来帮助潜在客户了解你的体验。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-177">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="f9d4e-178">如果需要使用外部帐户，则必须在完整说明中记下。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-178">You must note in the full description, if an external account is required for use.</span></span> <span data-ttu-id="f9d4e-179">和 `short` `full` 的值必须不同。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-179">The values of `short` and `full` must be different.</span></span> <span data-ttu-id="f9d4e-180">简短说明不得在详细说明中重复，且不得包含任何其他应用名称。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-180">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="f9d4e-181">名称</span><span class="sxs-lookup"><span data-stu-id="f9d4e-181">Name</span></span>| <span data-ttu-id="f9d4e-182">最大大小</span><span class="sxs-lookup"><span data-stu-id="f9d4e-182">Maximum size</span></span> | <span data-ttu-id="f9d4e-183">必需</span><span class="sxs-lookup"><span data-stu-id="f9d4e-183">Required</span></span> | <span data-ttu-id="f9d4e-184">Description</span><span class="sxs-lookup"><span data-stu-id="f9d4e-184">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="f9d4e-185">80 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-185">80 characters</span></span>|<span data-ttu-id="f9d4e-186">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-186">✔</span></span>|<span data-ttu-id="f9d4e-187">应用体验的简短说明，在空间有限时使用。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-187">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="f9d4e-188">4000 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-188">4000 characters</span></span>|<span data-ttu-id="f9d4e-189">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-189">✔</span></span>|<span data-ttu-id="f9d4e-190">应用的完整说明。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-190">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="f9d4e-191">packageName</span><span class="sxs-lookup"><span data-stu-id="f9d4e-191">packageName</span></span>

<span data-ttu-id="f9d4e-192">**可选** — 字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-192">**Optional** — string</span></span>

<span data-ttu-id="f9d4e-193">反向域表示法的应用的唯一标识符;例如，com.example.myapp。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-193">A unique identifier for the app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="f9d4e-194">最大长度：64 个字符。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-194">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="f9d4e-195">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="f9d4e-195">localizationInfo</span></span>

<span data-ttu-id="f9d4e-196">**可选** — object</span><span class="sxs-lookup"><span data-stu-id="f9d4e-196">**Optional** — object</span></span>

<span data-ttu-id="f9d4e-197">允许指定默认语言，以及指向其他语言文件的指针。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-197">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="f9d4e-198">请参阅 [本地化](~/concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-198">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="f9d4e-199">名称</span><span class="sxs-lookup"><span data-stu-id="f9d4e-199">Name</span></span>| <span data-ttu-id="f9d4e-200">最大大小</span><span class="sxs-lookup"><span data-stu-id="f9d4e-200">Maximum size</span></span> | <span data-ttu-id="f9d4e-201">必需</span><span class="sxs-lookup"><span data-stu-id="f9d4e-201">Required</span></span> | <span data-ttu-id="f9d4e-202">Description</span><span class="sxs-lookup"><span data-stu-id="f9d4e-202">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="f9d4e-203">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-203">✔</span></span>|<span data-ttu-id="f9d4e-204">此顶级清单文件中字符串的语言标记。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-204">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="f9d4e-205">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="f9d4e-205">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="f9d4e-206">指定其他语言翻译的对象数组。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-206">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="f9d4e-207">名称</span><span class="sxs-lookup"><span data-stu-id="f9d4e-207">Name</span></span>| <span data-ttu-id="f9d4e-208">最大大小</span><span class="sxs-lookup"><span data-stu-id="f9d4e-208">Maximum size</span></span> | <span data-ttu-id="f9d4e-209">必需</span><span class="sxs-lookup"><span data-stu-id="f9d4e-209">Required</span></span> | <span data-ttu-id="f9d4e-210">Description</span><span class="sxs-lookup"><span data-stu-id="f9d4e-210">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="f9d4e-211">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-211">✔</span></span>|<span data-ttu-id="f9d4e-212">提供的文件中字符串的语言标记。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-212">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="f9d4e-213">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-213">✔</span></span>|<span data-ttu-id="f9d4e-214">包含已翻译字符串的 .json 文件的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-214">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="f9d4e-215">图标</span><span class="sxs-lookup"><span data-stu-id="f9d4e-215">icons</span></span>

<span data-ttu-id="f9d4e-216">**必需** — object</span><span class="sxs-lookup"><span data-stu-id="f9d4e-216">**Required** — object</span></span>

<span data-ttu-id="f9d4e-217">Teams 应用中使用的图标。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-217">Icons used within the Teams app.</span></span> <span data-ttu-id="f9d4e-218">图标文件必须作为上传程序包的一部分包含在内。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-218">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="f9d4e-219">有关详细信息 [，](../../concepts/build-and-test/apps-package.md#app-icons) 请参阅图标。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-219">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="f9d4e-220">名称</span><span class="sxs-lookup"><span data-stu-id="f9d4e-220">Name</span></span>| <span data-ttu-id="f9d4e-221">最大大小</span><span class="sxs-lookup"><span data-stu-id="f9d4e-221">Maximum size</span></span> | <span data-ttu-id="f9d4e-222">必需</span><span class="sxs-lookup"><span data-stu-id="f9d4e-222">Required</span></span> | <span data-ttu-id="f9d4e-223">Description</span><span class="sxs-lookup"><span data-stu-id="f9d4e-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="f9d4e-224">32 x 32 像素</span><span class="sxs-lookup"><span data-stu-id="f9d4e-224">32 x 32 pixels</span></span>|<span data-ttu-id="f9d4e-225">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-225">✔</span></span>|<span data-ttu-id="f9d4e-226">指向透明 32x32 PNG 大纲图标的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="f9d4e-227">192 x 192 像素</span><span class="sxs-lookup"><span data-stu-id="f9d4e-227">192 x 192 pixels</span></span>|<span data-ttu-id="f9d4e-228">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-228">✔</span></span>|<span data-ttu-id="f9d4e-229">完整颜色 192x192 PNG 图标的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="f9d4e-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="f9d4e-230">accentColor</span></span>

<span data-ttu-id="f9d4e-231">**可选** — HTML 十六进制颜色代码</span><span class="sxs-lookup"><span data-stu-id="f9d4e-231">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="f9d4e-232">要与 和 结合使用用作大纲图标背景的颜色。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="f9d4e-233">该值必须是以"#"开头的有效 HTML 颜色代码，例如 `#4464ee` 。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="f9d4e-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="f9d4e-234">configurableTabs</span></span>

<span data-ttu-id="f9d4e-235">**可选** — 数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-235">**Optional** — array</span></span>

<span data-ttu-id="f9d4e-236">当你的应用体验具有团队频道选项卡体验时，需要在添加前进行额外配置。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="f9d4e-237">可配置的选项卡仅在团队范围内受支持， (个人) ，并且当前每个应用仅支持一个选项卡。 </span><span class="sxs-lookup"><span data-stu-id="f9d4e-237">Configurable tabs are supported only in the teams scope (not personal), and currently only **one** tab per app is supported.</span></span>

|<span data-ttu-id="f9d4e-238">名称</span><span class="sxs-lookup"><span data-stu-id="f9d4e-238">Name</span></span>| <span data-ttu-id="f9d4e-239">类型</span><span class="sxs-lookup"><span data-stu-id="f9d4e-239">Type</span></span>| <span data-ttu-id="f9d4e-240">最大大小</span><span class="sxs-lookup"><span data-stu-id="f9d4e-240">Maximum size</span></span> | <span data-ttu-id="f9d4e-241">必需</span><span class="sxs-lookup"><span data-stu-id="f9d4e-241">Required</span></span> | <span data-ttu-id="f9d4e-242">说明</span><span class="sxs-lookup"><span data-stu-id="f9d4e-242">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="f9d4e-243">string</span><span class="sxs-lookup"><span data-stu-id="f9d4e-243">string</span></span>|<span data-ttu-id="f9d4e-244">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-244">2048 characters</span></span>|<span data-ttu-id="f9d4e-245">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-245">✔</span></span>|<span data-ttu-id="f9d4e-246">配置 https:// 时将使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-246">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="f9d4e-247">枚举数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-247">array of enums</span></span>|<span data-ttu-id="f9d4e-248">1</span><span class="sxs-lookup"><span data-stu-id="f9d4e-248">1</span></span>|<span data-ttu-id="f9d4e-249">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-249">✔</span></span>|<span data-ttu-id="f9d4e-250">目前，可配置的选项卡仅支持 `team` 和 `groupchat` 作用域。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-250">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="f9d4e-251">boolean</span><span class="sxs-lookup"><span data-stu-id="f9d4e-251">boolean</span></span>|||<span data-ttu-id="f9d4e-252">一个值，指示用户创建后是否可以更新选项卡配置的实例。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-252">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="f9d4e-253">默认值 **：true**。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-253">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="f9d4e-254">枚举数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-254">array of enums</span></span>|<span data-ttu-id="f9d4e-255">6 </span><span class="sxs-lookup"><span data-stu-id="f9d4e-255">6</span></span>||<span data-ttu-id="f9d4e-256">支持选项卡的范围 `contextItem` 集。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-256">The set of `contextItem` scopes where a tab is supported.</span></span> <span data-ttu-id="f9d4e-257">默认值 **：[channelTab、privateChatTab、meetingChatTab、meetingDetailsTab]**。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-257">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="f9d4e-258">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-258">string</span></span>|<span data-ttu-id="f9d4e-259">2048</span><span class="sxs-lookup"><span data-stu-id="f9d4e-259">2048</span></span>||<span data-ttu-id="f9d4e-260">指向用于 SharePoint 的选项卡预览图像的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-260">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="f9d4e-261">大小 1024x768。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-261">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="f9d4e-262">枚举数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-262">array of enums</span></span>|<span data-ttu-id="f9d4e-263">1</span><span class="sxs-lookup"><span data-stu-id="f9d4e-263">1</span></span>||<span data-ttu-id="f9d4e-264">定义选项卡在 SharePoint 中的可用方法。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-264">Defines how your tab is made available in SharePoint.</span></span> <span data-ttu-id="f9d4e-265">选项为 `sharePointFullPage` 和 `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="f9d4e-265">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="f9d4e-266">staticTabs</span><span class="sxs-lookup"><span data-stu-id="f9d4e-266">staticTabs</span></span>

<span data-ttu-id="f9d4e-267">**可选** — 数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-267">**Optional** — array</span></span>

<span data-ttu-id="f9d4e-268">定义一组默认情况下可以"固定"的选项卡，而无需用户手动添加它们。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-268">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="f9d4e-269">范围中声明 `personal` 的静态选项卡始终固定到应用的个人体验。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-269">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="f9d4e-270">作用域中声明的 `team` 静态选项卡当前不受支持。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-270">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="f9d4e-271">此项是一个数组 (类型的所有元素) 最多包含 16 个元素 `object` 。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-271">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="f9d4e-272">只有提供静态选项卡解决方案的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-272">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="f9d4e-273">名称</span><span class="sxs-lookup"><span data-stu-id="f9d4e-273">Name</span></span>| <span data-ttu-id="f9d4e-274">类型</span><span class="sxs-lookup"><span data-stu-id="f9d4e-274">Type</span></span>| <span data-ttu-id="f9d4e-275">最大大小</span><span class="sxs-lookup"><span data-stu-id="f9d4e-275">Maximum size</span></span> | <span data-ttu-id="f9d4e-276">必需</span><span class="sxs-lookup"><span data-stu-id="f9d4e-276">Required</span></span> | <span data-ttu-id="f9d4e-277">说明</span><span class="sxs-lookup"><span data-stu-id="f9d4e-277">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="f9d4e-278">string</span><span class="sxs-lookup"><span data-stu-id="f9d4e-278">string</span></span>|<span data-ttu-id="f9d4e-279">64 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-279">64 characters</span></span>|<span data-ttu-id="f9d4e-280">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-280">✔</span></span>|<span data-ttu-id="f9d4e-281">选项卡显示的实体的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-281">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="f9d4e-282">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-282">string</span></span>|<span data-ttu-id="f9d4e-283">128 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-283">128 characters</span></span>|<span data-ttu-id="f9d4e-284">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-284">✔</span></span>|<span data-ttu-id="f9d4e-285">选项卡显示名称界面中的列数。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-285">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="f9d4e-286">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-286">string</span></span>||<span data-ttu-id="f9d4e-287">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-287">✔</span></span>|<span data-ttu-id="f9d4e-288">指向要显示在 Teams 画布中的实体 UI 的 https:// URL。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-288">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="f9d4e-289">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-289">string</span></span>|||<span data-ttu-id="f9d4e-290">用户 https:// 在浏览器中查看时指向的 URL。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-290">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="f9d4e-291">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-291">string</span></span>|||<span data-ttu-id="f9d4e-292">用于 https:// 搜索查询的 URL。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-292">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="f9d4e-293">枚举数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-293">array of enums</span></span>|<span data-ttu-id="f9d4e-294">1</span><span class="sxs-lookup"><span data-stu-id="f9d4e-294">1</span></span>|<span data-ttu-id="f9d4e-295">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-295">✔</span></span>|<span data-ttu-id="f9d4e-296">目前，静态选项卡仅支持范围，这意味着只能将作用域预配 `personal` 为个人体验的一部分。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-296">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="f9d4e-297">枚举数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-297">array of enums</span></span>| <span data-ttu-id="f9d4e-298">2</span><span class="sxs-lookup"><span data-stu-id="f9d4e-298">2</span></span>|| <span data-ttu-id="f9d4e-299">支持选项卡的范围 `contextItem` 集。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-299">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
> <span data-ttu-id="f9d4e-300">如果你的选项卡需要与上下文相关的信息来显示相关内容或启动身份验证流，请参阅获取[Microsoft Teams 选项卡的上下文](../../tabs/how-to/access-teams-context.md)。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-300">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="f9d4e-301">bots</span><span class="sxs-lookup"><span data-stu-id="f9d4e-301">bots</span></span>

<span data-ttu-id="f9d4e-302">**可选** — 数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-302">**Optional** — array</span></span>

<span data-ttu-id="f9d4e-303">定义自动程序解决方案以及默认命令属性等可选信息。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-303">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="f9d4e-304">该项目是一个 (，当前每个应用仅允许一个自动程序) 类型的所有元素 &mdash; `object` 。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-304">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="f9d4e-305">只有提供自动程序体验的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-305">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="f9d4e-306">名称</span><span class="sxs-lookup"><span data-stu-id="f9d4e-306">Name</span></span>| <span data-ttu-id="f9d4e-307">类型</span><span class="sxs-lookup"><span data-stu-id="f9d4e-307">Type</span></span>| <span data-ttu-id="f9d4e-308">最大大小</span><span class="sxs-lookup"><span data-stu-id="f9d4e-308">Maximum size</span></span> | <span data-ttu-id="f9d4e-309">必需</span><span class="sxs-lookup"><span data-stu-id="f9d4e-309">Required</span></span> | <span data-ttu-id="f9d4e-310">说明</span><span class="sxs-lookup"><span data-stu-id="f9d4e-310">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="f9d4e-311">string</span><span class="sxs-lookup"><span data-stu-id="f9d4e-311">string</span></span>|<span data-ttu-id="f9d4e-312">64 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-312">64 characters</span></span>|<span data-ttu-id="f9d4e-313">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-313">✔</span></span>|<span data-ttu-id="f9d4e-314">使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-314">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="f9d4e-315">这可能与整个应用 [ID 相同](#id)。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-315">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="f9d4e-316">枚举数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-316">array of enums</span></span>|<span data-ttu-id="f9d4e-317">3</span><span class="sxs-lookup"><span data-stu-id="f9d4e-317">3</span></span>|<span data-ttu-id="f9d4e-318">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-318">✔</span></span>|<span data-ttu-id="f9d4e-319">指定自动程序是在 `team` 内的频道上下文中提供体验、在群组聊天 (`groupchat`) 中提供体验，还是仅在单个用户 (`personal`) 范围内提供体验。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-319">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="f9d4e-320">这些选项不具排他性。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-320">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="f9d4e-321">boolean</span><span class="sxs-lookup"><span data-stu-id="f9d4e-321">boolean</span></span>|||<span data-ttu-id="f9d4e-322">描述自动程序是否利用用户提示将自动程序添加到特定频道。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-322">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="f9d4e-323">默认值： **`false`**</span><span class="sxs-lookup"><span data-stu-id="f9d4e-323">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="f9d4e-324">boolean</span><span class="sxs-lookup"><span data-stu-id="f9d4e-324">boolean</span></span>|||<span data-ttu-id="f9d4e-325">指示自动程序是否为单向、仅通知的自动程序，而不是对话自动程序。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-325">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="f9d4e-326">默认值： **`false`**</span><span class="sxs-lookup"><span data-stu-id="f9d4e-326">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="f9d4e-327">boolean</span><span class="sxs-lookup"><span data-stu-id="f9d4e-327">boolean</span></span>|||<span data-ttu-id="f9d4e-328">指示自动程序是否支持在个人聊天中上传/下载文件。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-328">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="f9d4e-329">默认值： **`false`**</span><span class="sxs-lookup"><span data-stu-id="f9d4e-329">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="f9d4e-330">boolean</span><span class="sxs-lookup"><span data-stu-id="f9d4e-330">boolean</span></span>|||<span data-ttu-id="f9d4e-331">指示机器人支持音频呼叫位置的值。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-331">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="f9d4e-332">**重要** 提示：此属性当前为实验属性。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-332">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="f9d4e-333">实验属性可能不完整，并且可能在完全可用之前发生更改。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-333">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="f9d4e-334">它仅供测试和探索之用，不得在生产应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-334">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="f9d4e-335">默认值： **`false`**</span><span class="sxs-lookup"><span data-stu-id="f9d4e-335">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="f9d4e-336">boolean</span><span class="sxs-lookup"><span data-stu-id="f9d4e-336">boolean</span></span>|||<span data-ttu-id="f9d4e-337">指示机器人支持视频呼叫位置的值。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-337">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="f9d4e-338">**重要** 提示：此属性当前为实验属性。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-338">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="f9d4e-339">实验属性可能不完整，并且可能在完全可用之前发生更改。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-339">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="f9d4e-340">它仅供测试和探索之用，不得在生产应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-340">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="f9d4e-341">默认值： **`false`**</span><span class="sxs-lookup"><span data-stu-id="f9d4e-341">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="f9d4e-342">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="f9d4e-342">bots.commandLists</span></span>

<span data-ttu-id="f9d4e-343">自动程序可以推荐给用户的命令的可选列表。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-343">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="f9d4e-344">对象是一个 (，最多包含 2 个元素) 所有类型元素;您必须为自动程序支持的每个范围定义单独的 `object` 命令列表。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-344">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="f9d4e-345">有关详细信息 [，](~/bots/how-to/create-a-bot-commands-menu.md) 请参阅自动程序菜单。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-345">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="f9d4e-346">名称</span><span class="sxs-lookup"><span data-stu-id="f9d4e-346">Name</span></span>| <span data-ttu-id="f9d4e-347">类型</span><span class="sxs-lookup"><span data-stu-id="f9d4e-347">Type</span></span>| <span data-ttu-id="f9d4e-348">最大大小</span><span class="sxs-lookup"><span data-stu-id="f9d4e-348">Maximum size</span></span> | <span data-ttu-id="f9d4e-349">必需</span><span class="sxs-lookup"><span data-stu-id="f9d4e-349">Required</span></span> | <span data-ttu-id="f9d4e-350">Description</span><span class="sxs-lookup"><span data-stu-id="f9d4e-350">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="f9d4e-351">枚举数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-351">array of enums</span></span>|<span data-ttu-id="f9d4e-352">3</span><span class="sxs-lookup"><span data-stu-id="f9d4e-352">3</span></span>|<span data-ttu-id="f9d4e-353">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-353">✔</span></span>|<span data-ttu-id="f9d4e-354">指定命令列表有效的作用域。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-354">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="f9d4e-355">选项包括 `team`、`personal` 和 `groupchat`。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-355">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="f9d4e-356">对象数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-356">array of objects</span></span>|<span data-ttu-id="f9d4e-357">10  </span><span class="sxs-lookup"><span data-stu-id="f9d4e-357">10</span></span>|<span data-ttu-id="f9d4e-358">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-358">✔</span></span>|<span data-ttu-id="f9d4e-359">自动程序支持的命令数组：</span><span class="sxs-lookup"><span data-stu-id="f9d4e-359">An array of commands the bot supports:</span></span><br><span data-ttu-id="f9d4e-360">`title`：自动程序命令名称（字符串，32）</span><span class="sxs-lookup"><span data-stu-id="f9d4e-360">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="f9d4e-361">`description`：命令语法及其参数的简单描述或示例（字符串，128）</span><span class="sxs-lookup"><span data-stu-id="f9d4e-361">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="f9d4e-362">bots.commandLists.commands</span><span class="sxs-lookup"><span data-stu-id="f9d4e-362">bots.commandLists.commands</span></span>

|<span data-ttu-id="f9d4e-363">名称</span><span class="sxs-lookup"><span data-stu-id="f9d4e-363">Name</span></span>| <span data-ttu-id="f9d4e-364">类型</span><span class="sxs-lookup"><span data-stu-id="f9d4e-364">Type</span></span>| <span data-ttu-id="f9d4e-365">最大大小</span><span class="sxs-lookup"><span data-stu-id="f9d4e-365">Maximum size</span></span> | <span data-ttu-id="f9d4e-366">必需</span><span class="sxs-lookup"><span data-stu-id="f9d4e-366">Required</span></span> | <span data-ttu-id="f9d4e-367">说明</span><span class="sxs-lookup"><span data-stu-id="f9d4e-367">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="f9d4e-368">title</span><span class="sxs-lookup"><span data-stu-id="f9d4e-368">title</span></span>|<span data-ttu-id="f9d4e-369">string</span><span class="sxs-lookup"><span data-stu-id="f9d4e-369">string</span></span>|<span data-ttu-id="f9d4e-370">12 </span><span class="sxs-lookup"><span data-stu-id="f9d4e-370">12</span></span>|<span data-ttu-id="f9d4e-371">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-371">✔</span></span>|<span data-ttu-id="f9d4e-372">自动程序命令名称</span><span class="sxs-lookup"><span data-stu-id="f9d4e-372">The bot command name</span></span>|
|<span data-ttu-id="f9d4e-373">说明</span><span class="sxs-lookup"><span data-stu-id="f9d4e-373">description</span></span>|<span data-ttu-id="f9d4e-374">string</span><span class="sxs-lookup"><span data-stu-id="f9d4e-374">string</span></span>|<span data-ttu-id="f9d4e-375">128 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-375">128 characters</span></span>|<span data-ttu-id="f9d4e-376">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-376">✔</span></span>|<span data-ttu-id="f9d4e-377">简单文本说明或命令语法及其参数的示例。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-377">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="f9d4e-378">连接器</span><span class="sxs-lookup"><span data-stu-id="f9d4e-378">connectors</span></span>

<span data-ttu-id="f9d4e-379">**可选** — 数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-379">**Optional** — array</span></span>

<span data-ttu-id="f9d4e-380">`connectors`此块为应用定义 Office 365 连接器。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-380">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="f9d4e-381">对象是一个数组， (类型的所有元素) 1 个元素 `object` 。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-381">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="f9d4e-382">只有提供连接器的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-382">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="f9d4e-383">名称</span><span class="sxs-lookup"><span data-stu-id="f9d4e-383">Name</span></span>| <span data-ttu-id="f9d4e-384">类型</span><span class="sxs-lookup"><span data-stu-id="f9d4e-384">Type</span></span>| <span data-ttu-id="f9d4e-385">最大大小</span><span class="sxs-lookup"><span data-stu-id="f9d4e-385">Maximum size</span></span> | <span data-ttu-id="f9d4e-386">必需</span><span class="sxs-lookup"><span data-stu-id="f9d4e-386">Required</span></span> | <span data-ttu-id="f9d4e-387">说明</span><span class="sxs-lookup"><span data-stu-id="f9d4e-387">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="f9d4e-388">string</span><span class="sxs-lookup"><span data-stu-id="f9d4e-388">string</span></span>|<span data-ttu-id="f9d4e-389">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-389">2048 characters</span></span>|<span data-ttu-id="f9d4e-390">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-390">✔</span></span>|<span data-ttu-id="f9d4e-391">配置 https:// 时将使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-391">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="f9d4e-392">枚举数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-392">array of enums</span></span>|<span data-ttu-id="f9d4e-393">1</span><span class="sxs-lookup"><span data-stu-id="f9d4e-393">1</span></span>|<span data-ttu-id="f9d4e-394">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-394">✔</span></span>|<span data-ttu-id="f9d4e-395">指定连接器是提供在 中频道上下文中的体验，还是仅针对单个用户 `team` `personal` () 。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-395">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="f9d4e-396">目前，仅 `team` 支持范围。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-396">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="f9d4e-397">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-397">string</span></span>|<span data-ttu-id="f9d4e-398">64 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-398">64 characters</span></span>|<span data-ttu-id="f9d4e-399">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-399">✔</span></span>|<span data-ttu-id="f9d4e-400">连接器的唯一标识符，与连接器开发人员仪表板中的 ID [相匹配](https://aka.ms/connectorsdashboard)。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-400">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="f9d4e-401">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="f9d4e-401">composeExtensions</span></span>

<span data-ttu-id="f9d4e-402">**可选** — 数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-402">**Optional** — array</span></span>

<span data-ttu-id="f9d4e-403">为应用定义消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-403">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="f9d4e-404">2017 年 11 月，功能名称从"撰写扩展"更改为"邮件扩展"，但清单名称保持不变，以便现有扩展继续工作。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-404">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="f9d4e-405">项目是一个数组， (类型的所有元素) 1 个元素 `object` 。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-405">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="f9d4e-406">只有提供邮件扩展的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-406">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="f9d4e-407">名称</span><span class="sxs-lookup"><span data-stu-id="f9d4e-407">Name</span></span>| <span data-ttu-id="f9d4e-408">类型</span><span class="sxs-lookup"><span data-stu-id="f9d4e-408">Type</span></span> | <span data-ttu-id="f9d4e-409">最大大小</span><span class="sxs-lookup"><span data-stu-id="f9d4e-409">Maximum Size</span></span> | <span data-ttu-id="f9d4e-410">必需</span><span class="sxs-lookup"><span data-stu-id="f9d4e-410">Required</span></span> | <span data-ttu-id="f9d4e-411">说明</span><span class="sxs-lookup"><span data-stu-id="f9d4e-411">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="f9d4e-412">string</span><span class="sxs-lookup"><span data-stu-id="f9d4e-412">string</span></span>|<span data-ttu-id="f9d4e-413">64</span><span class="sxs-lookup"><span data-stu-id="f9d4e-413">64</span></span>|<span data-ttu-id="f9d4e-414">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-414">✔</span></span>|<span data-ttu-id="f9d4e-415">自动程序支持消息传递扩展的唯一 Microsoft 应用 ID，在 Bot Framework 中注册。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-415">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="f9d4e-416">这可能与整个应用 ID 相同。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-416">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="f9d4e-417">对象数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-417">array of objects</span></span>|<span data-ttu-id="f9d4e-418">10  </span><span class="sxs-lookup"><span data-stu-id="f9d4e-418">10</span></span>|<span data-ttu-id="f9d4e-419">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-419">✔</span></span>|<span data-ttu-id="f9d4e-420">邮件扩展支持的命令数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-420">Array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="f9d4e-421">boolean</span><span class="sxs-lookup"><span data-stu-id="f9d4e-421">boolean</span></span>|||<span data-ttu-id="f9d4e-422">一个值，指示用户是否可以更新邮件扩展的配置。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-422">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="f9d4e-423">默认值：**False**。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-423">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="f9d4e-424">对象数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-424">array of Objects</span></span>|<span data-ttu-id="f9d4e-425">5 </span><span class="sxs-lookup"><span data-stu-id="f9d4e-425">5</span></span>||<span data-ttu-id="f9d4e-426">允许满足某些条件时调用应用的处理程序列表。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-426">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="f9d4e-427">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-427">string</span></span>|||<span data-ttu-id="f9d4e-428">消息处理程序的类型。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-428">The type of message handler.</span></span> <span data-ttu-id="f9d4e-429">必须是 `"link"`。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-429">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="f9d4e-430">字符串数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-430">array of Strings</span></span>|||<span data-ttu-id="f9d4e-431">链接邮件处理程序可以注册的域数组。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-431">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="f9d4e-432">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="f9d4e-432">composeExtensions.commands</span></span>

<span data-ttu-id="f9d4e-433">邮件扩展必须声明一个或多个命令。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-433">Your messaging extension must declare one or more commands.</span></span> <span data-ttu-id="f9d4e-434">每个命令在 Microsoft Teams 中显示为基于 UI 的入口点的潜在交互。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-434">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="f9d4e-435">最多有 10 个命令。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-435">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="f9d4e-436">每个命令项都是具有以下结构的对象：</span><span class="sxs-lookup"><span data-stu-id="f9d4e-436">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="f9d4e-437">名称</span><span class="sxs-lookup"><span data-stu-id="f9d4e-437">Name</span></span>| <span data-ttu-id="f9d4e-438">类型</span><span class="sxs-lookup"><span data-stu-id="f9d4e-438">Type</span></span>| <span data-ttu-id="f9d4e-439">最大大小</span><span class="sxs-lookup"><span data-stu-id="f9d4e-439">Maximum size</span></span> | <span data-ttu-id="f9d4e-440">必需</span><span class="sxs-lookup"><span data-stu-id="f9d4e-440">Required</span></span> | <span data-ttu-id="f9d4e-441">说明</span><span class="sxs-lookup"><span data-stu-id="f9d4e-441">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="f9d4e-442">string</span><span class="sxs-lookup"><span data-stu-id="f9d4e-442">string</span></span>|<span data-ttu-id="f9d4e-443">64 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-443">64 characters</span></span>|<span data-ttu-id="f9d4e-444">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-444">✔</span></span>|<span data-ttu-id="f9d4e-445">命令的 ID。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-445">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="f9d4e-446">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-446">string</span></span>|<span data-ttu-id="f9d4e-447">32 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-447">32 characters</span></span>|<span data-ttu-id="f9d4e-448">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-448">✔</span></span>|<span data-ttu-id="f9d4e-449">用户友好命令名称。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-449">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="f9d4e-450">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-450">string</span></span>|<span data-ttu-id="f9d4e-451">64 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-451">64 characters</span></span>||<span data-ttu-id="f9d4e-452">命令的类型。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-452">Type of the command.</span></span> <span data-ttu-id="f9d4e-453">或 `query` `action` 之一。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-453">One of `query` or `action`.</span></span> <span data-ttu-id="f9d4e-454">默认值 **：query**。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-454">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="f9d4e-455">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-455">string</span></span>|<span data-ttu-id="f9d4e-456">128 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-456">128 characters</span></span>||<span data-ttu-id="f9d4e-457">向用户显示以指示此命令用途的说明。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-457">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="f9d4e-458">boolean</span><span class="sxs-lookup"><span data-stu-id="f9d4e-458">boolean</span></span>|||<span data-ttu-id="f9d4e-459">布尔值指示命令最初是否运行，没有参数。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-459">A boolean value indicates whether the command runs initially with no parameters.</span></span> <span data-ttu-id="f9d4e-460">默认为 **false**。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-460">Default is **false**.</span></span>|
|`context`|<span data-ttu-id="f9d4e-461">字符串数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-461">array of Strings</span></span>|<span data-ttu-id="f9d4e-462">3</span><span class="sxs-lookup"><span data-stu-id="f9d4e-462">3</span></span>||<span data-ttu-id="f9d4e-463">定义可以从何处调用邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-463">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="f9d4e-464">、 `compose` 、 的任意 `commandBox` 组合 `message` 。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-464">Any combination of`compose`,`commandBox`,`message`.</span></span> <span data-ttu-id="f9d4e-465">默认值为“`["compose","commandBox"]`”。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-465">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="f9d4e-466">boolean</span><span class="sxs-lookup"><span data-stu-id="f9d4e-466">boolean</span></span>|||<span data-ttu-id="f9d4e-467">一个布尔值，指示它是否必须动态提取任务模块。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-467">A boolean value that indicates if it must fetch the task module dynamically.</span></span> <span data-ttu-id="f9d4e-468">默认为 **false**。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-468">Default is **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="f9d4e-469">object</span><span class="sxs-lookup"><span data-stu-id="f9d4e-469">object</span></span>|||<span data-ttu-id="f9d4e-470">指定在使用消息传递扩展命令时要预加载的任务模块。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-470">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="f9d4e-471">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-471">string</span></span>|<span data-ttu-id="f9d4e-472">64 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-472">64 characters</span></span>||<span data-ttu-id="f9d4e-473">初始对话框标题。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-473">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="f9d4e-474">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-474">string</span></span>|||<span data-ttu-id="f9d4e-475">对话框宽度 - 以像素为单位的一个数字或默认布局，例如"large"、"medium"或"small"。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-475">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="f9d4e-476">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-476">string</span></span>|||<span data-ttu-id="f9d4e-477">对话框高度 - 以像素为单位的一个数字或默认布局，例如"large"、"medium"或"small"。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-477">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="f9d4e-478">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-478">string</span></span>|||<span data-ttu-id="f9d4e-479">初始 Web 视图 URL。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-479">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="f9d4e-480">对象数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-480">array of object</span></span>|<span data-ttu-id="f9d4e-481">5 个项目</span><span class="sxs-lookup"><span data-stu-id="f9d4e-481">5 items</span></span>|<span data-ttu-id="f9d4e-482">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-482">✔</span></span>|<span data-ttu-id="f9d4e-483">命令采用的参数列表。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-483">The list of parameters the command takes.</span></span> <span data-ttu-id="f9d4e-484">最小值：1;最大值：5。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-484">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="f9d4e-485">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-485">string</span></span>|<span data-ttu-id="f9d4e-486">64 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-486">64 characters</span></span>|<span data-ttu-id="f9d4e-487">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-487">✔</span></span>|<span data-ttu-id="f9d4e-488">显示在客户端中的参数的名称。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-488">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="f9d4e-489">这包括在用户请求中。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-489">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="f9d4e-490">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-490">string</span></span>|<span data-ttu-id="f9d4e-491">32 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-491">32 characters</span></span>|<span data-ttu-id="f9d4e-492">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-492">✔</span></span>|<span data-ttu-id="f9d4e-493">参数的用户友好标题。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-493">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="f9d4e-494">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-494">string</span></span>|<span data-ttu-id="f9d4e-495">128 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-495">128 characters</span></span>||<span data-ttu-id="f9d4e-496">描述此参数用途的用户友好字符串。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-496">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="f9d4e-497">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-497">string</span></span>|<span data-ttu-id="f9d4e-498">512 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-498">512 characters</span></span>||<span data-ttu-id="f9d4e-499">参数的初始值。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-499">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="f9d4e-500">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-500">string</span></span>|<span data-ttu-id="f9d4e-501">128 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-501">128 characters</span></span>||<span data-ttu-id="f9d4e-502">定义在任务模块上显示的控件的类型 `fetchTask: true` 。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-502">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="f9d4e-503">之一 `text, textarea, number, date, time, toggle, choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-503">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="f9d4e-504">对象数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-504">array of objects</span></span>|<span data-ttu-id="f9d4e-505">10 个项目</span><span class="sxs-lookup"><span data-stu-id="f9d4e-505">10 items</span></span>||<span data-ttu-id="f9d4e-506">的选项 `choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-506">The choice options for the`choiceset`.</span></span> <span data-ttu-id="f9d4e-507">仅在 为 `parameter.inputType` `choiceset` 时使用 。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-507">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="f9d4e-508">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-508">string</span></span>|<span data-ttu-id="f9d4e-509">128 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-509">128 characters</span></span>|<span data-ttu-id="f9d4e-510">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-510">✔</span></span>|<span data-ttu-id="f9d4e-511">选项的标题。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-511">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="f9d4e-512">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-512">string</span></span>|<span data-ttu-id="f9d4e-513">512 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-513">512 characters</span></span>|<span data-ttu-id="f9d4e-514">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-514">✔</span></span>|<span data-ttu-id="f9d4e-515">选项的值。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-515">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="f9d4e-516">权限</span><span class="sxs-lookup"><span data-stu-id="f9d4e-516">permissions</span></span>

<span data-ttu-id="f9d4e-517">**可选** — 字符串数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-517">**Optional** — array of strings</span></span>

<span data-ttu-id="f9d4e-518">一个数组，指定应用请求哪些权限，使最终用户 `string` 知道扩展的执行方式。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-518">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension performs.</span></span> <span data-ttu-id="f9d4e-519">以下选项非独占：</span><span class="sxs-lookup"><span data-stu-id="f9d4e-519">The following options are non-exclusive:</span></span>

* <span data-ttu-id="f9d4e-520">`identity`&emsp;需要用户标识信息</span><span class="sxs-lookup"><span data-stu-id="f9d4e-520">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="f9d4e-521">`messageTeamMembers`&emsp;需要向团队成员发送直接消息的权限</span><span class="sxs-lookup"><span data-stu-id="f9d4e-521">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="f9d4e-522">在应用更新期间更改这些权限，会导致用户在运行更新后的应用后重复同意过程。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-522">Changing these permissions during app update, causes your users to repeat the consent process after they run the updated app.</span></span> <span data-ttu-id="f9d4e-523">有关详细信息 [，请参阅更新](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) 应用。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-523">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="f9d4e-524">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="f9d4e-524">devicePermissions</span></span>

<span data-ttu-id="f9d4e-525">**可选** — 字符串数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-525">**Optional** — array of strings</span></span>

<span data-ttu-id="f9d4e-526">在应用请求访问的用户设备上提供本机功能。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-526">Provides the native features on a user's device that your app requests access to.</span></span> <span data-ttu-id="f9d4e-527">选项有：</span><span class="sxs-lookup"><span data-stu-id="f9d4e-527">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="f9d4e-528">validDomains</span><span class="sxs-lookup"><span data-stu-id="f9d4e-528">validDomains</span></span>

<span data-ttu-id="f9d4e-529">**可选**，但 **已指出的必需** 项除外</span><span class="sxs-lookup"><span data-stu-id="f9d4e-529">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="f9d4e-530">应用预期在 Teams 客户端内加载的网站的有效域列表。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-530">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="f9d4e-531">域列表可以包含通配符，例如 `*.example.com` ， 。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-531">Domain listings can include wildcards, for example, `*.example.com`.</span></span> <span data-ttu-id="f9d4e-532">这完全匹配域的一个段;如果需要匹配，请使用 `a.b.example.com` `*.*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-532">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="f9d4e-533">如果你的选项卡配置或内容 UI 需要导航到除用于选项卡配置的其他任何其他域，则必须在此处指定该域。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-533">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="f9d4e-534">不需要 **在** 应用中包含要支持的标识提供程序的域。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-534">It is **not** necessary to include the domains of identity providers you want to support in your app.</span></span> <span data-ttu-id="f9d4e-535">例如，若要使用 Google ID 进行身份验证，必须重定向到 accounts.google.com，但不得在 `validDomains[]` accounts.google.com。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-535">For example, to authenticate using a Google ID, it is required to redirect to accounts.google.com, however, you must not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="f9d4e-536">需要自己的 sharepoint URL 正常运行的 Teams 应用在有效域列表中包括"{teamsitedomain}"。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-536">Teams apps that require their own sharepoint URLs to function well, includes "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f9d4e-537">不要直接添加或通过通配符添加超出您控制的域。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-537">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="f9d4e-538">例如， `yourapp.onmicrosoft.com` 是有效的，但 `*.onmicrosoft.com` 是 无效。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-538">For example, `yourapp.onmicrosoft.com` is valid, however, `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="f9d4e-539">对象是包含类型 的所有元素的数组 `string` 。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-539">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="f9d4e-540">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="f9d4e-540">webApplicationInfo</span></span>

<span data-ttu-id="f9d4e-541">**可选** — object</span><span class="sxs-lookup"><span data-stu-id="f9d4e-541">**Optional** — object</span></span>

<span data-ttu-id="f9d4e-542">提供 Azure Active Directory (AAD) 应用 ID 和 Microsoft Graph 信息，以帮助用户无缝登录你的应用。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-542">Provide your Azure Active Directory (AAD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="f9d4e-543">如果你的应用在 AAD 中注册，则必须提供应用 ID，以便管理员可以在 Teams 管理中心轻松查看权限并授予同意。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-543">If your app is registered in AAD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="f9d4e-544">名称</span><span class="sxs-lookup"><span data-stu-id="f9d4e-544">Name</span></span>| <span data-ttu-id="f9d4e-545">类型</span><span class="sxs-lookup"><span data-stu-id="f9d4e-545">Type</span></span>| <span data-ttu-id="f9d4e-546">最大大小</span><span class="sxs-lookup"><span data-stu-id="f9d4e-546">Maximum size</span></span> | <span data-ttu-id="f9d4e-547">必需</span><span class="sxs-lookup"><span data-stu-id="f9d4e-547">Required</span></span> | <span data-ttu-id="f9d4e-548">说明</span><span class="sxs-lookup"><span data-stu-id="f9d4e-548">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="f9d4e-549">string</span><span class="sxs-lookup"><span data-stu-id="f9d4e-549">string</span></span>|<span data-ttu-id="f9d4e-550">36 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-550">36 characters</span></span>|<span data-ttu-id="f9d4e-551">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-551">✔</span></span>|<span data-ttu-id="f9d4e-552">应用的 AAD 应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-552">AAD application id of the app.</span></span> <span data-ttu-id="f9d4e-553">此 ID 必须是 GUID。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-553">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="f9d4e-554">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-554">string</span></span>|<span data-ttu-id="f9d4e-555">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-555">2048 characters</span></span>|<span data-ttu-id="f9d4e-556">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-556">✔</span></span>|<span data-ttu-id="f9d4e-557">用于获取 SSO 身份验证令牌的应用的资源 URL。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-557">Resource URL of app for acquiring auth token for SSO.</span></span> </br> <span data-ttu-id="f9d4e-558">**注意：** 如果不使用 SSO，请确保在此字段中向应用清单输入虚拟字符串值，以避免 https://notapplicable 错误响应。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-558">**NOTE:** If you are not using SSO, ensure that you enter a dummy string value in this field to your app manifest, for example, https://notapplicable to avoid an error response.</span></span> |
|`applicationPermissions`|<span data-ttu-id="f9d4e-559">array of strings</span><span class="sxs-lookup"><span data-stu-id="f9d4e-559">array of strings</span></span>|<span data-ttu-id="f9d4e-560">128 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-560">128 characters</span></span>||<span data-ttu-id="f9d4e-561">指定具体 [资源特定许可](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-561">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="f9d4e-562">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="f9d4e-562">showLoadingIndicator</span></span>

<span data-ttu-id="f9d4e-563">**可选** — 布尔值</span><span class="sxs-lookup"><span data-stu-id="f9d4e-563">**Optional** — boolean</span></span>

<span data-ttu-id="f9d4e-564">指示在加载应用或选项卡时是否显示加载指示器。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-564">Indicates whether or not to show the loading indicator when an app or tab is loading.</span></span> <span data-ttu-id="f9d4e-565">默认为 **false**。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-565">Default is **false**.</span></span>
>[!NOTE]
><span data-ttu-id="f9d4e-566">如果在应用清单中选择 true，若要正确加载页面，请修改选项卡和任务模块的内容页，如显示本机加载指示器文档 `showLoadingIndicator` 中所述。 [](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)</span><span class="sxs-lookup"><span data-stu-id="f9d4e-566">If you select`showLoadingIndicator` as true in your app manifest, to load the page correctly, modify the content pages of your tabs and task modules as described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="f9d4e-567">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="f9d4e-567">isFullScreen</span></span>

 <span data-ttu-id="f9d4e-568">**可选** — 布尔值</span><span class="sxs-lookup"><span data-stu-id="f9d4e-568">**Optional** — boolean</span></span>

<span data-ttu-id="f9d4e-569">指示在具有或没有选项卡标题栏的情况下呈现个人应用。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-569">Indicate where a personal app is rendered with or without a tab header bar.</span></span> <span data-ttu-id="f9d4e-570">默认为 **false**。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-570">Default is **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="f9d4e-571">activities</span><span class="sxs-lookup"><span data-stu-id="f9d4e-571">activities</span></span>

<span data-ttu-id="f9d4e-572">**可选** — object</span><span class="sxs-lookup"><span data-stu-id="f9d4e-572">**Optional** — object</span></span>

<span data-ttu-id="f9d4e-573">定义应用用于发布用户活动源的属性。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-573">Define the properties your app uses to post a user activity feed.</span></span>

|<span data-ttu-id="f9d4e-574">名称</span><span class="sxs-lookup"><span data-stu-id="f9d4e-574">Name</span></span>| <span data-ttu-id="f9d4e-575">类型</span><span class="sxs-lookup"><span data-stu-id="f9d4e-575">Type</span></span>| <span data-ttu-id="f9d4e-576">最大大小</span><span class="sxs-lookup"><span data-stu-id="f9d4e-576">Maximum size</span></span> | <span data-ttu-id="f9d4e-577">必需</span><span class="sxs-lookup"><span data-stu-id="f9d4e-577">Required</span></span> | <span data-ttu-id="f9d4e-578">Description</span><span class="sxs-lookup"><span data-stu-id="f9d4e-578">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="f9d4e-579">对象数组</span><span class="sxs-lookup"><span data-stu-id="f9d4e-579">array of Objects</span></span>|<span data-ttu-id="f9d4e-580">128 项</span><span class="sxs-lookup"><span data-stu-id="f9d4e-580">128 items</span></span>| | <span data-ttu-id="f9d4e-581">提供你的应用可以发布给用户活动源的活动类型。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-581">Provide the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="f9d4e-582">activities.activityTypes</span><span class="sxs-lookup"><span data-stu-id="f9d4e-582">activities.activityTypes</span></span>

|<span data-ttu-id="f9d4e-583">名称</span><span class="sxs-lookup"><span data-stu-id="f9d4e-583">Name</span></span>| <span data-ttu-id="f9d4e-584">类型</span><span class="sxs-lookup"><span data-stu-id="f9d4e-584">Type</span></span>| <span data-ttu-id="f9d4e-585">最大大小</span><span class="sxs-lookup"><span data-stu-id="f9d4e-585">Maximum size</span></span> | <span data-ttu-id="f9d4e-586">必需</span><span class="sxs-lookup"><span data-stu-id="f9d4e-586">Required</span></span> | <span data-ttu-id="f9d4e-587">说明</span><span class="sxs-lookup"><span data-stu-id="f9d4e-587">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="f9d4e-588">string</span><span class="sxs-lookup"><span data-stu-id="f9d4e-588">string</span></span>|<span data-ttu-id="f9d4e-589">32 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-589">32 characters</span></span>|<span data-ttu-id="f9d4e-590">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-590">✔</span></span>|<span data-ttu-id="f9d4e-591">通知类型。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-591">The notification type.</span></span> <span data-ttu-id="f9d4e-592">*请参阅下文*。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-592">*See below*.</span></span>|
|`description`|<span data-ttu-id="f9d4e-593">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-593">string</span></span>|<span data-ttu-id="f9d4e-594">128 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-594">128 characters</span></span>|<span data-ttu-id="f9d4e-595">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-595">✔</span></span>|<span data-ttu-id="f9d4e-596">通知的简要说明。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-596">A brief description of the notification.</span></span> <span data-ttu-id="f9d4e-597">*请参阅下文*。</span><span class="sxs-lookup"><span data-stu-id="f9d4e-597">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="f9d4e-598">字符串</span><span class="sxs-lookup"><span data-stu-id="f9d4e-598">string</span></span>|<span data-ttu-id="f9d4e-599">128 个字符</span><span class="sxs-lookup"><span data-stu-id="f9d4e-599">128 characters</span></span>|<span data-ttu-id="f9d4e-600">✔</span><span class="sxs-lookup"><span data-stu-id="f9d4e-600">✔</span></span>|<span data-ttu-id="f9d4e-601">例如："{actor} 已创建任务 {taskId}"</span><span class="sxs-lookup"><span data-stu-id="f9d4e-601">Ex: "{actor} created task {taskId} for you"</span></span>|

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
>
>
