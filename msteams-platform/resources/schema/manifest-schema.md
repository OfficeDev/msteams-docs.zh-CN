---
title: 清单架构参考
description: 介绍 Microsoft Teams 的清单架构
keywords: teams 清单架构
author: laujan
ms.author: lajanuar
ms.openlocfilehash: c66add190b0492170acf9756980ee16fb1fdf1fd
ms.sourcegitcommit: 5f1d6c12d80d48f403b73586f68bacf15785c855
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/30/2020
ms.locfileid: "49739054"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="156b2-104">参考：Microsoft Teams 的清单架构</span><span class="sxs-lookup"><span data-stu-id="156b2-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="156b2-105">Microsoft Teams 清单介绍了应用如何集成到 Microsoft Teams 产品。</span><span class="sxs-lookup"><span data-stu-id="156b2-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="156b2-106">清单必须符合托管在 中的架构 [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json) 。</span><span class="sxs-lookup"><span data-stu-id="156b2-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="156b2-107">早期版本 1.0-1.4 也受支持 (URL 地址中的"v1.x") 。</span><span class="sxs-lookup"><span data-stu-id="156b2-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="156b2-108">以下架构示例显示了所有扩展性选项。</span><span class="sxs-lookup"><span data-stu-id="156b2-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="156b2-109">示例完整清单</span><span class="sxs-lookup"><span data-stu-id="156b2-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.8",
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
  }
}
```

<span data-ttu-id="156b2-110">架构定义以下属性：</span><span class="sxs-lookup"><span data-stu-id="156b2-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="156b2-111">$schema</span><span class="sxs-lookup"><span data-stu-id="156b2-111">$schema</span></span>

<span data-ttu-id="156b2-112">*可选，但建议* 使用字符串</span><span class="sxs-lookup"><span data-stu-id="156b2-112">*Optional, but recommended* — string</span></span>

<span data-ttu-id="156b2-113">引用https:// JSON 架构的 URL。</span><span class="sxs-lookup"><span data-stu-id="156b2-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="156b2-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="156b2-114">manifestVersion</span></span>

<span data-ttu-id="156b2-115">**必需** — 字符串</span><span class="sxs-lookup"><span data-stu-id="156b2-115">**Required** — string</span></span>

<span data-ttu-id="156b2-116">此清单使用的清单架构版本。</span><span class="sxs-lookup"><span data-stu-id="156b2-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="156b2-117">它应为"1.7"。</span><span class="sxs-lookup"><span data-stu-id="156b2-117">It should be "1.7".</span></span>

## <a name="version"></a><span data-ttu-id="156b2-118">version</span><span class="sxs-lookup"><span data-stu-id="156b2-118">version</span></span>

<span data-ttu-id="156b2-119">**必需** — 字符串</span><span class="sxs-lookup"><span data-stu-id="156b2-119">**Required** — string</span></span>

<span data-ttu-id="156b2-120">特定应用的版本。</span><span class="sxs-lookup"><span data-stu-id="156b2-120">The version of the specific app.</span></span> <span data-ttu-id="156b2-121">如果更新清单中的某些内容，则还必须增加版本。</span><span class="sxs-lookup"><span data-stu-id="156b2-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="156b2-122">这样一来，在安装新的清单时，它将覆盖现有的版本，用户将获得新的功能。</span><span class="sxs-lookup"><span data-stu-id="156b2-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="156b2-123">如果此应用已提交到应用商店，则新清单必须重新提交和重新验证。</span><span class="sxs-lookup"><span data-stu-id="156b2-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="156b2-124">然后，此应用的用户将在经过批准后数小时内自动获取新的更新清单。</span><span class="sxs-lookup"><span data-stu-id="156b2-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="156b2-125">如果应用请求的权限更改，将提示用户升级并重新同意应用。</span><span class="sxs-lookup"><span data-stu-id="156b2-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="156b2-126">此版本字符串必须遵循 [Semver](http://semver.org/) 标准 (MAJOR。MINOR。PATCH) 。</span><span class="sxs-lookup"><span data-stu-id="156b2-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="156b2-127">id</span><span class="sxs-lookup"><span data-stu-id="156b2-127">id</span></span>

<span data-ttu-id="156b2-128">**必需** — Microsoft 应用 ID</span><span class="sxs-lookup"><span data-stu-id="156b2-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="156b2-129">此应用由 Microsoft 生成的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="156b2-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="156b2-130">如果你已经通过 Microsoft Bot Framework 注册了自动程序，或者你的选项卡的 Web 应用已经向 Microsoft 登录，你应该已经拥有 ID，应在此处输入它。</span><span class="sxs-lookup"><span data-stu-id="156b2-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="156b2-131">否则，应在"我的应用程序" (Microsoft 应用程序注册门户) ID，[](https://apps.dev.microsoft.com)在此处输入，然后在添加自动程序时重复使用它。注意：如果你在 AppSource 中向现有应用提交更新，则不得修改清单中的 ID。</span><span class="sxs-lookup"><span data-stu-id="156b2-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="156b2-132">developer</span><span class="sxs-lookup"><span data-stu-id="156b2-132">developer</span></span>

<span data-ttu-id="156b2-133">**必需** — 对象</span><span class="sxs-lookup"><span data-stu-id="156b2-133">**Required** — object</span></span>

<span data-ttu-id="156b2-134">指定有关你的公司的信息。</span><span class="sxs-lookup"><span data-stu-id="156b2-134">Specifies information about your company.</span></span> <span data-ttu-id="156b2-135">对于提交到 AppSource (Office 应用商店) ，这些值必须与 AppSource 条目中的信息匹配。</span><span class="sxs-lookup"><span data-stu-id="156b2-135">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="156b2-136">有关其他 [信息，](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) 请参阅我们的发布指南。</span><span class="sxs-lookup"><span data-stu-id="156b2-136">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="156b2-137">名称</span><span class="sxs-lookup"><span data-stu-id="156b2-137">Name</span></span>| <span data-ttu-id="156b2-138">最大大小</span><span class="sxs-lookup"><span data-stu-id="156b2-138">Maximum size</span></span> | <span data-ttu-id="156b2-139">必需</span><span class="sxs-lookup"><span data-stu-id="156b2-139">Required</span></span> | <span data-ttu-id="156b2-140">说明</span><span class="sxs-lookup"><span data-stu-id="156b2-140">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="156b2-141">32 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-141">32 characters</span></span>|<span data-ttu-id="156b2-142">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-142">✔</span></span>|<span data-ttu-id="156b2-143">开发人员显示名称的指南。</span><span class="sxs-lookup"><span data-stu-id="156b2-143">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="156b2-144">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-144">2048 characters</span></span>|<span data-ttu-id="156b2-145">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-145">✔</span></span>|<span data-ttu-id="156b2-146"> https://开发人员网站的 URL。</span><span class="sxs-lookup"><span data-stu-id="156b2-146">The https:// URL to the developer's website.</span></span> <span data-ttu-id="156b2-147">此链接应让用户访问你的公司或特定于产品的登陆页面。</span><span class="sxs-lookup"><span data-stu-id="156b2-147">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="156b2-148">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-148">2048 characters</span></span>|<span data-ttu-id="156b2-149">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-149">✔</span></span>|<span data-ttu-id="156b2-150"> Https://开发人员隐私策略的 URL。</span><span class="sxs-lookup"><span data-stu-id="156b2-150">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="156b2-151">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-151">2048 characters</span></span>|<span data-ttu-id="156b2-152">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-152">✔</span></span>|<span data-ttu-id="156b2-153"> https://开发人员使用条款的 URL。</span><span class="sxs-lookup"><span data-stu-id="156b2-153">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="156b2-154">10 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-154">10 characters</span></span>| |<span data-ttu-id="156b2-155">**可选** 标识生成应用的合作伙伴组织的 Microsoft 合作伙伴网络 ID。</span><span class="sxs-lookup"><span data-stu-id="156b2-155">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="156b2-156">name</span><span class="sxs-lookup"><span data-stu-id="156b2-156">name</span></span>

<span data-ttu-id="156b2-157">**必需** — 对象</span><span class="sxs-lookup"><span data-stu-id="156b2-157">**Required** — object</span></span>

<span data-ttu-id="156b2-158">在 Teams 体验中向用户显示的应用体验的名称。</span><span class="sxs-lookup"><span data-stu-id="156b2-158">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="156b2-159">对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。</span><span class="sxs-lookup"><span data-stu-id="156b2-159">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="156b2-160">值 `short` 和 `full` 不应相同。</span><span class="sxs-lookup"><span data-stu-id="156b2-160">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="156b2-161">名称</span><span class="sxs-lookup"><span data-stu-id="156b2-161">Name</span></span>| <span data-ttu-id="156b2-162">最大大小</span><span class="sxs-lookup"><span data-stu-id="156b2-162">Maximum size</span></span> | <span data-ttu-id="156b2-163">必需</span><span class="sxs-lookup"><span data-stu-id="156b2-163">Required</span></span> | <span data-ttu-id="156b2-164">说明</span><span class="sxs-lookup"><span data-stu-id="156b2-164">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="156b2-165">30 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-165">30 characters</span></span>|<span data-ttu-id="156b2-166">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-166">✔</span></span>|<span data-ttu-id="156b2-167">应用的显示名称代码。</span><span class="sxs-lookup"><span data-stu-id="156b2-167">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="156b2-168">100 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-168">100 characters</span></span>||<span data-ttu-id="156b2-169">应用的完整名称，当完整应用名称超过 30 个字符时使用。</span><span class="sxs-lookup"><span data-stu-id="156b2-169">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="156b2-170">说明</span><span class="sxs-lookup"><span data-stu-id="156b2-170">description</span></span>

<span data-ttu-id="156b2-171">**必需** — 对象</span><span class="sxs-lookup"><span data-stu-id="156b2-171">**Required** — object</span></span>

<span data-ttu-id="156b2-172">向用户描述你的应用。</span><span class="sxs-lookup"><span data-stu-id="156b2-172">Describes your app to users.</span></span> <span data-ttu-id="156b2-173">对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。</span><span class="sxs-lookup"><span data-stu-id="156b2-173">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="156b2-174">确保你的说明准确地描述了你的体验，并提供了信息来帮助潜在客户了解你的体验。</span><span class="sxs-lookup"><span data-stu-id="156b2-174">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="156b2-175">还应在完整说明中注意，如果需要使用外部帐户。</span><span class="sxs-lookup"><span data-stu-id="156b2-175">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="156b2-176">值 `short` 和 `full` 不应相同。</span><span class="sxs-lookup"><span data-stu-id="156b2-176">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="156b2-177">简短说明不得在详细说明中重复，且不得包含任何其他应用名称。</span><span class="sxs-lookup"><span data-stu-id="156b2-177">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="156b2-178">名称</span><span class="sxs-lookup"><span data-stu-id="156b2-178">Name</span></span>| <span data-ttu-id="156b2-179">最大大小</span><span class="sxs-lookup"><span data-stu-id="156b2-179">Maximum size</span></span> | <span data-ttu-id="156b2-180">必需</span><span class="sxs-lookup"><span data-stu-id="156b2-180">Required</span></span> | <span data-ttu-id="156b2-181">说明</span><span class="sxs-lookup"><span data-stu-id="156b2-181">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="156b2-182">80 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-182">80 characters</span></span>|<span data-ttu-id="156b2-183">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-183">✔</span></span>|<span data-ttu-id="156b2-184">应用体验的简短说明，在空间有限时使用。</span><span class="sxs-lookup"><span data-stu-id="156b2-184">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="156b2-185">4000 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-185">4000 characters</span></span>|<span data-ttu-id="156b2-186">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-186">✔</span></span>|<span data-ttu-id="156b2-187">应用的完整说明。</span><span class="sxs-lookup"><span data-stu-id="156b2-187">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="156b2-188">packageName</span><span class="sxs-lookup"><span data-stu-id="156b2-188">packageName</span></span>

<span data-ttu-id="156b2-189">**可选** — 字符串</span><span class="sxs-lookup"><span data-stu-id="156b2-189">**Optional** — string</span></span>

<span data-ttu-id="156b2-190">此应用的唯一标识符，使用反向域表示法;例如，com.example.myapp。</span><span class="sxs-lookup"><span data-stu-id="156b2-190">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="156b2-191">最大长度：64 个字符。</span><span class="sxs-lookup"><span data-stu-id="156b2-191">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="156b2-192">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="156b2-192">localizationInfo</span></span>

<span data-ttu-id="156b2-193">**可选** — 对象</span><span class="sxs-lookup"><span data-stu-id="156b2-193">**Optional** — object</span></span>

<span data-ttu-id="156b2-194">允许指定默认语言，以及指向其他语言文件的指针。</span><span class="sxs-lookup"><span data-stu-id="156b2-194">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="156b2-195">请参阅[本地化。](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="156b2-195">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="156b2-196">名称</span><span class="sxs-lookup"><span data-stu-id="156b2-196">Name</span></span>| <span data-ttu-id="156b2-197">最大大小</span><span class="sxs-lookup"><span data-stu-id="156b2-197">Maximum size</span></span> | <span data-ttu-id="156b2-198">必需</span><span class="sxs-lookup"><span data-stu-id="156b2-198">Required</span></span> | <span data-ttu-id="156b2-199">说明</span><span class="sxs-lookup"><span data-stu-id="156b2-199">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="156b2-200">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-200">✔</span></span>|<span data-ttu-id="156b2-201">此顶级清单文件中字符串的语言标记。</span><span class="sxs-lookup"><span data-stu-id="156b2-201">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="156b2-202">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="156b2-202">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="156b2-203">指定其他语言翻译的对象数组。</span><span class="sxs-lookup"><span data-stu-id="156b2-203">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="156b2-204">名称</span><span class="sxs-lookup"><span data-stu-id="156b2-204">Name</span></span>| <span data-ttu-id="156b2-205">最大大小</span><span class="sxs-lookup"><span data-stu-id="156b2-205">Maximum size</span></span> | <span data-ttu-id="156b2-206">必需</span><span class="sxs-lookup"><span data-stu-id="156b2-206">Required</span></span> | <span data-ttu-id="156b2-207">说明</span><span class="sxs-lookup"><span data-stu-id="156b2-207">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="156b2-208">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-208">✔</span></span>|<span data-ttu-id="156b2-209">提供的文件中字符串的语言标记。</span><span class="sxs-lookup"><span data-stu-id="156b2-209">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="156b2-210">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-210">✔</span></span>|<span data-ttu-id="156b2-211">包含已翻译字符串的 .json 文件的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="156b2-211">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="156b2-212">图标</span><span class="sxs-lookup"><span data-stu-id="156b2-212">icons</span></span>

<span data-ttu-id="156b2-213">**必需** — 对象</span><span class="sxs-lookup"><span data-stu-id="156b2-213">**Required** — object</span></span>

<span data-ttu-id="156b2-214">Teams 应用中使用的图标。</span><span class="sxs-lookup"><span data-stu-id="156b2-214">Icons used within the Teams app.</span></span> <span data-ttu-id="156b2-215">图标文件必须作为上传程序包的一部分包含在内。</span><span class="sxs-lookup"><span data-stu-id="156b2-215">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="156b2-216">有关详细信息 [，](../../concepts/build-and-test/apps-package.md#app-icons) 请参阅"图标"。</span><span class="sxs-lookup"><span data-stu-id="156b2-216">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="156b2-217">名称</span><span class="sxs-lookup"><span data-stu-id="156b2-217">Name</span></span>| <span data-ttu-id="156b2-218">最大大小</span><span class="sxs-lookup"><span data-stu-id="156b2-218">Maximum size</span></span> | <span data-ttu-id="156b2-219">必需</span><span class="sxs-lookup"><span data-stu-id="156b2-219">Required</span></span> | <span data-ttu-id="156b2-220">说明</span><span class="sxs-lookup"><span data-stu-id="156b2-220">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="156b2-221">32 x 32 像素</span><span class="sxs-lookup"><span data-stu-id="156b2-221">32 x 32 pixels</span></span>|<span data-ttu-id="156b2-222">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-222">✔</span></span>|<span data-ttu-id="156b2-223">指向透明 32x32 PNG 大纲图标的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="156b2-223">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="156b2-224">192 x 192 像素</span><span class="sxs-lookup"><span data-stu-id="156b2-224">192 x 192 pixels</span></span>|<span data-ttu-id="156b2-225">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-225">✔</span></span>|<span data-ttu-id="156b2-226">完整颜色 192x192 PNG 图标的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="156b2-226">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="156b2-227">accentColor</span><span class="sxs-lookup"><span data-stu-id="156b2-227">accentColor</span></span>

<span data-ttu-id="156b2-228">**可选** — HTML 十六进制颜色代码</span><span class="sxs-lookup"><span data-stu-id="156b2-228">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="156b2-229">要与大纲图标一起使用并用作背景的颜色。</span><span class="sxs-lookup"><span data-stu-id="156b2-229">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="156b2-230">例如，该值必须是以"#"开头的有效 HTML 颜色代码 `#4464ee` 。</span><span class="sxs-lookup"><span data-stu-id="156b2-230">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="156b2-231">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="156b2-231">configurableTabs</span></span>

<span data-ttu-id="156b2-232">**可选** — 数组</span><span class="sxs-lookup"><span data-stu-id="156b2-232">**Optional** — array</span></span>

<span data-ttu-id="156b2-233">当你的应用体验具有团队频道选项卡体验时，需要在添加前进行额外配置。</span><span class="sxs-lookup"><span data-stu-id="156b2-233">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="156b2-234">可配置的选项卡仅在团队范围内受支持， (个人) ，并且当前每个应用仅支持一个选项卡。 </span><span class="sxs-lookup"><span data-stu-id="156b2-234">Configurable tabs are supported only in the teams scope (not personal), and currently only **one** tab per app is supported.</span></span>

|<span data-ttu-id="156b2-235">名称</span><span class="sxs-lookup"><span data-stu-id="156b2-235">Name</span></span>| <span data-ttu-id="156b2-236">类型</span><span class="sxs-lookup"><span data-stu-id="156b2-236">Type</span></span>| <span data-ttu-id="156b2-237">最大大小</span><span class="sxs-lookup"><span data-stu-id="156b2-237">Maximum size</span></span> | <span data-ttu-id="156b2-238">必需</span><span class="sxs-lookup"><span data-stu-id="156b2-238">Required</span></span> | <span data-ttu-id="156b2-239">说明</span><span class="sxs-lookup"><span data-stu-id="156b2-239">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="156b2-240">string</span><span class="sxs-lookup"><span data-stu-id="156b2-240">string</span></span>|<span data-ttu-id="156b2-241">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-241">2048 characters</span></span>|<span data-ttu-id="156b2-242">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-242">✔</span></span>|<span data-ttu-id="156b2-243">配置https://使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="156b2-243">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="156b2-244">枚举数组</span><span class="sxs-lookup"><span data-stu-id="156b2-244">array of enums</span></span>|<span data-ttu-id="156b2-245">1 </span><span class="sxs-lookup"><span data-stu-id="156b2-245">1</span></span>|<span data-ttu-id="156b2-246">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-246">✔</span></span>|<span data-ttu-id="156b2-247">目前，可配置的选项卡仅支持 `team` 和 `groupchat` 范围。</span><span class="sxs-lookup"><span data-stu-id="156b2-247">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="156b2-248">boolean</span><span class="sxs-lookup"><span data-stu-id="156b2-248">boolean</span></span>|||<span data-ttu-id="156b2-249">一个值，指示用户创建后是否可以更新选项卡配置的实例。</span><span class="sxs-lookup"><span data-stu-id="156b2-249">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="156b2-250">默认值 **：true**。</span><span class="sxs-lookup"><span data-stu-id="156b2-250">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="156b2-251">枚举数组</span><span class="sxs-lookup"><span data-stu-id="156b2-251">array of enums</span></span>|<span data-ttu-id="156b2-252">6 </span><span class="sxs-lookup"><span data-stu-id="156b2-252">6</span></span>||<span data-ttu-id="156b2-253">支持 `contextItem` 选项卡的范围集。</span><span class="sxs-lookup"><span data-stu-id="156b2-253">The set of `contextItem` scopes where a tab is supported.</span></span> <span data-ttu-id="156b2-254">默认值 **：[channelTab、privateChatTab、meetingChatTab、meetingDetailsTab]**。</span><span class="sxs-lookup"><span data-stu-id="156b2-254">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="156b2-255">string</span><span class="sxs-lookup"><span data-stu-id="156b2-255">string</span></span>|<span data-ttu-id="156b2-256">2048</span><span class="sxs-lookup"><span data-stu-id="156b2-256">2048</span></span>||<span data-ttu-id="156b2-257">在 SharePoint 中使用的选项卡预览图像的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="156b2-257">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="156b2-258">大小 1024x768。</span><span class="sxs-lookup"><span data-stu-id="156b2-258">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="156b2-259">枚举数组</span><span class="sxs-lookup"><span data-stu-id="156b2-259">array of enums</span></span>|<span data-ttu-id="156b2-260">1 </span><span class="sxs-lookup"><span data-stu-id="156b2-260">1</span></span>||<span data-ttu-id="156b2-261">定义选项卡在 SharePoint 中的可用方法。</span><span class="sxs-lookup"><span data-stu-id="156b2-261">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="156b2-262">选项 `sharePointFullPage` 包括和 `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="156b2-262">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="156b2-263">staticTabs</span><span class="sxs-lookup"><span data-stu-id="156b2-263">staticTabs</span></span>

<span data-ttu-id="156b2-264">**可选** — 数组</span><span class="sxs-lookup"><span data-stu-id="156b2-264">**Optional** — array</span></span>

<span data-ttu-id="156b2-265">定义一组默认情况下可以"固定"的选项卡，无需用户手动添加它们。</span><span class="sxs-lookup"><span data-stu-id="156b2-265">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="156b2-266">范围中声明的 `personal` 静态选项卡始终固定到应用的个人体验。</span><span class="sxs-lookup"><span data-stu-id="156b2-266">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="156b2-267">当前不支持在范围 `team` 中声明的静态选项卡。</span><span class="sxs-lookup"><span data-stu-id="156b2-267">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="156b2-268">此项是一个数组 (类型的所有元素) 最多包含 16 个元素 `object` 。</span><span class="sxs-lookup"><span data-stu-id="156b2-268">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="156b2-269">只有提供静态选项卡解决方案的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="156b2-269">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="156b2-270">名称</span><span class="sxs-lookup"><span data-stu-id="156b2-270">Name</span></span>| <span data-ttu-id="156b2-271">类型</span><span class="sxs-lookup"><span data-stu-id="156b2-271">Type</span></span>| <span data-ttu-id="156b2-272">最大大小</span><span class="sxs-lookup"><span data-stu-id="156b2-272">Maximum size</span></span> | <span data-ttu-id="156b2-273">必需</span><span class="sxs-lookup"><span data-stu-id="156b2-273">Required</span></span> | <span data-ttu-id="156b2-274">说明</span><span class="sxs-lookup"><span data-stu-id="156b2-274">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="156b2-275">string</span><span class="sxs-lookup"><span data-stu-id="156b2-275">string</span></span>|<span data-ttu-id="156b2-276">64 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-276">64 characters</span></span>|<span data-ttu-id="156b2-277">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-277">✔</span></span>|<span data-ttu-id="156b2-278">选项卡显示的实体的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="156b2-278">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="156b2-279">string</span><span class="sxs-lookup"><span data-stu-id="156b2-279">string</span></span>|<span data-ttu-id="156b2-280">128 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-280">128 characters</span></span>|<span data-ttu-id="156b2-281">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-281">✔</span></span>|<span data-ttu-id="156b2-282">通道显示名称选项卡的显示对象。</span><span class="sxs-lookup"><span data-stu-id="156b2-282">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="156b2-283">string</span><span class="sxs-lookup"><span data-stu-id="156b2-283">string</span></span>||<span data-ttu-id="156b2-284">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-284">✔</span></span>|<span data-ttu-id="156b2-285">指向要显示在 Teams 画布中的实体 UI 的 https:// URL。</span><span class="sxs-lookup"><span data-stu-id="156b2-285">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="156b2-286">string</span><span class="sxs-lookup"><span data-stu-id="156b2-286">string</span></span>|||<span data-ttu-id="156b2-287">用户https://浏览器中查看时要指向的 URL。</span><span class="sxs-lookup"><span data-stu-id="156b2-287">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="156b2-288">string</span><span class="sxs-lookup"><span data-stu-id="156b2-288">string</span></span>|||<span data-ttu-id="156b2-289">要https://搜索查询的 URL。</span><span class="sxs-lookup"><span data-stu-id="156b2-289">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="156b2-290">枚举数组</span><span class="sxs-lookup"><span data-stu-id="156b2-290">array of enums</span></span>|<span data-ttu-id="156b2-291">1 </span><span class="sxs-lookup"><span data-stu-id="156b2-291">1</span></span>|<span data-ttu-id="156b2-292">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-292">✔</span></span>|<span data-ttu-id="156b2-293">目前，静态选项卡仅支持范围，这意味着只能将作用域预配 `personal` 为个人体验的一部分。</span><span class="sxs-lookup"><span data-stu-id="156b2-293">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="156b2-294">枚举数组</span><span class="sxs-lookup"><span data-stu-id="156b2-294">array of enums</span></span>| <span data-ttu-id="156b2-295">2 </span><span class="sxs-lookup"><span data-stu-id="156b2-295">2</span></span>|| <span data-ttu-id="156b2-296">支持 `contextItem` 选项卡的范围集。</span><span class="sxs-lookup"><span data-stu-id="156b2-296">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
> <span data-ttu-id="156b2-297">如果你的选项卡需要上下文相关信息来显示相关内容或启动身份验证流，请参阅"获取[Microsoft Teams"选项卡的上下文](../../tabs/how-to/access-teams-context.md)。</span><span class="sxs-lookup"><span data-stu-id="156b2-297">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="156b2-298">bots</span><span class="sxs-lookup"><span data-stu-id="156b2-298">bots</span></span>

<span data-ttu-id="156b2-299">**可选** — 数组</span><span class="sxs-lookup"><span data-stu-id="156b2-299">**Optional** — array</span></span>

<span data-ttu-id="156b2-300">定义自动程序解决方案以及可选信息（如默认命令属性）。</span><span class="sxs-lookup"><span data-stu-id="156b2-300">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="156b2-301">该项目是一个 (，当前每个应用仅允许使用一个自动程序) 类型的所有元素 &mdash; `object` 。</span><span class="sxs-lookup"><span data-stu-id="156b2-301">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="156b2-302">只有提供自动程序体验的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="156b2-302">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="156b2-303">名称</span><span class="sxs-lookup"><span data-stu-id="156b2-303">Name</span></span>| <span data-ttu-id="156b2-304">类型</span><span class="sxs-lookup"><span data-stu-id="156b2-304">Type</span></span>| <span data-ttu-id="156b2-305">最大大小</span><span class="sxs-lookup"><span data-stu-id="156b2-305">Maximum size</span></span> | <span data-ttu-id="156b2-306">必需</span><span class="sxs-lookup"><span data-stu-id="156b2-306">Required</span></span> | <span data-ttu-id="156b2-307">说明</span><span class="sxs-lookup"><span data-stu-id="156b2-307">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="156b2-308">string</span><span class="sxs-lookup"><span data-stu-id="156b2-308">string</span></span>|<span data-ttu-id="156b2-309">64 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-309">64 characters</span></span>|<span data-ttu-id="156b2-310">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-310">✔</span></span>|<span data-ttu-id="156b2-311">使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="156b2-311">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="156b2-312">这可能与整体应用 [ID 相同](#id)。</span><span class="sxs-lookup"><span data-stu-id="156b2-312">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="156b2-313">枚举数组</span><span class="sxs-lookup"><span data-stu-id="156b2-313">array of enums</span></span>|<span data-ttu-id="156b2-314">3 </span><span class="sxs-lookup"><span data-stu-id="156b2-314">3</span></span>|<span data-ttu-id="156b2-315">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-315">✔</span></span>|<span data-ttu-id="156b2-316">指定自动程序是在 `team` 内的频道上下文中提供体验、在群组聊天 (`groupchat`) 中提供体验，还是仅在单个用户 (`personal`) 范围内提供体验。</span><span class="sxs-lookup"><span data-stu-id="156b2-316">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="156b2-317">这些选项不具排他性。</span><span class="sxs-lookup"><span data-stu-id="156b2-317">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="156b2-318">boolean</span><span class="sxs-lookup"><span data-stu-id="156b2-318">boolean</span></span>|||<span data-ttu-id="156b2-319">描述自动程序是否利用用户提示将自动程序添加到特定频道。</span><span class="sxs-lookup"><span data-stu-id="156b2-319">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="156b2-320">默认值： **`false`**</span><span class="sxs-lookup"><span data-stu-id="156b2-320">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="156b2-321">boolean</span><span class="sxs-lookup"><span data-stu-id="156b2-321">boolean</span></span>|||<span data-ttu-id="156b2-322">指示自动程序是否为单向、仅通知的自动程序，而不是对话自动程序。</span><span class="sxs-lookup"><span data-stu-id="156b2-322">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="156b2-323">默认值： **`false`**</span><span class="sxs-lookup"><span data-stu-id="156b2-323">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="156b2-324">boolean</span><span class="sxs-lookup"><span data-stu-id="156b2-324">boolean</span></span>|||<span data-ttu-id="156b2-325">指示自动程序是否支持在个人聊天中上传/下载文件。</span><span class="sxs-lookup"><span data-stu-id="156b2-325">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="156b2-326">默认值： **`false`**</span><span class="sxs-lookup"><span data-stu-id="156b2-326">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="156b2-327">boolean</span><span class="sxs-lookup"><span data-stu-id="156b2-327">boolean</span></span>|||<span data-ttu-id="156b2-328">指示自动程序支持音频呼叫位置的值。</span><span class="sxs-lookup"><span data-stu-id="156b2-328">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="156b2-329">**重要** 提示：此属性当前为实验属性。</span><span class="sxs-lookup"><span data-stu-id="156b2-329">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="156b2-330">实验属性可能不完整，并且可能在完全可用之前发生更改。</span><span class="sxs-lookup"><span data-stu-id="156b2-330">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="156b2-331">它仅用于测试和探索目的，不应在生产应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="156b2-331">It is provided for testing and exploration purposes only and should not be used in production applications.</span></span> <span data-ttu-id="156b2-332">默认值： **`false`**</span><span class="sxs-lookup"><span data-stu-id="156b2-332">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="156b2-333">boolean</span><span class="sxs-lookup"><span data-stu-id="156b2-333">boolean</span></span>|||<span data-ttu-id="156b2-334">指示机器人支持视频呼叫位置的值。</span><span class="sxs-lookup"><span data-stu-id="156b2-334">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="156b2-335">**重要** 提示：此属性当前为实验属性。</span><span class="sxs-lookup"><span data-stu-id="156b2-335">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="156b2-336">实验属性可能不完整，并且可能在完全可用之前发生更改。</span><span class="sxs-lookup"><span data-stu-id="156b2-336">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="156b2-337">它仅用于测试和探索目的，不应在生产应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="156b2-337">It is provided for testing and exploration purposes only and should not be used in production applications.</span></span> <span data-ttu-id="156b2-338">默认值： **`false`**</span><span class="sxs-lookup"><span data-stu-id="156b2-338">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="156b2-339">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="156b2-339">bots.commandLists</span></span>

<span data-ttu-id="156b2-340">自动程序可以推荐给用户的命令的可选列表。</span><span class="sxs-lookup"><span data-stu-id="156b2-340">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="156b2-341">该对象是一个 (类型) 最多包含 2 个元素的数组;您必须为自动程序支持的每个范围定义单独的 `object` 命令列表。</span><span class="sxs-lookup"><span data-stu-id="156b2-341">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="156b2-342">有关详细信息 [，请参阅自动](~/bots/how-to/create-a-bot-commands-menu.md) 程序菜单。</span><span class="sxs-lookup"><span data-stu-id="156b2-342">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="156b2-343">名称</span><span class="sxs-lookup"><span data-stu-id="156b2-343">Name</span></span>| <span data-ttu-id="156b2-344">类型</span><span class="sxs-lookup"><span data-stu-id="156b2-344">Type</span></span>| <span data-ttu-id="156b2-345">最大大小</span><span class="sxs-lookup"><span data-stu-id="156b2-345">Maximum size</span></span> | <span data-ttu-id="156b2-346">必需</span><span class="sxs-lookup"><span data-stu-id="156b2-346">Required</span></span> | <span data-ttu-id="156b2-347">说明</span><span class="sxs-lookup"><span data-stu-id="156b2-347">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="156b2-348">枚举数组</span><span class="sxs-lookup"><span data-stu-id="156b2-348">array of enums</span></span>|<span data-ttu-id="156b2-349">3 </span><span class="sxs-lookup"><span data-stu-id="156b2-349">3</span></span>|<span data-ttu-id="156b2-350">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-350">✔</span></span>|<span data-ttu-id="156b2-351">指定命令列表有效的作用域。</span><span class="sxs-lookup"><span data-stu-id="156b2-351">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="156b2-352">选项包括 `team`、`personal` 和 `groupchat`。</span><span class="sxs-lookup"><span data-stu-id="156b2-352">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="156b2-353">对象数组</span><span class="sxs-lookup"><span data-stu-id="156b2-353">array of objects</span></span>|<span data-ttu-id="156b2-354">10 </span><span class="sxs-lookup"><span data-stu-id="156b2-354">10</span></span>|<span data-ttu-id="156b2-355">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-355">✔</span></span>|<span data-ttu-id="156b2-356">自动程序支持的命令数组：</span><span class="sxs-lookup"><span data-stu-id="156b2-356">An array of commands the bot supports:</span></span><br><span data-ttu-id="156b2-357">`title`：自动程序命令名称（字符串，32）</span><span class="sxs-lookup"><span data-stu-id="156b2-357">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="156b2-358">`description`：命令语法及其参数的简单描述或示例（字符串，128）</span><span class="sxs-lookup"><span data-stu-id="156b2-358">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="156b2-359">bots.commandLists.commands</span><span class="sxs-lookup"><span data-stu-id="156b2-359">bots.commandLists.commands</span></span>

|<span data-ttu-id="156b2-360">名称</span><span class="sxs-lookup"><span data-stu-id="156b2-360">Name</span></span>| <span data-ttu-id="156b2-361">类型</span><span class="sxs-lookup"><span data-stu-id="156b2-361">Type</span></span>| <span data-ttu-id="156b2-362">最大大小</span><span class="sxs-lookup"><span data-stu-id="156b2-362">Maximum size</span></span> | <span data-ttu-id="156b2-363">必需</span><span class="sxs-lookup"><span data-stu-id="156b2-363">Required</span></span> | <span data-ttu-id="156b2-364">说明</span><span class="sxs-lookup"><span data-stu-id="156b2-364">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="156b2-365">title</span><span class="sxs-lookup"><span data-stu-id="156b2-365">title</span></span>|<span data-ttu-id="156b2-366">string</span><span class="sxs-lookup"><span data-stu-id="156b2-366">string</span></span>|<span data-ttu-id="156b2-367">12 </span><span class="sxs-lookup"><span data-stu-id="156b2-367">12</span></span>|<span data-ttu-id="156b2-368">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-368">✔</span></span>|<span data-ttu-id="156b2-369">自动程序命令名称</span><span class="sxs-lookup"><span data-stu-id="156b2-369">The bot command name</span></span>|
|<span data-ttu-id="156b2-370">说明</span><span class="sxs-lookup"><span data-stu-id="156b2-370">description</span></span>|<span data-ttu-id="156b2-371">string</span><span class="sxs-lookup"><span data-stu-id="156b2-371">string</span></span>|<span data-ttu-id="156b2-372">128 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-372">128 characters</span></span>|<span data-ttu-id="156b2-373">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-373">✔</span></span>|<span data-ttu-id="156b2-374">简单文本说明或命令语法及其参数的示例。</span><span class="sxs-lookup"><span data-stu-id="156b2-374">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="156b2-375">连接器</span><span class="sxs-lookup"><span data-stu-id="156b2-375">connectors</span></span>

<span data-ttu-id="156b2-376">**可选** — 数组</span><span class="sxs-lookup"><span data-stu-id="156b2-376">**Optional** — array</span></span>

<span data-ttu-id="156b2-377">此 `connectors` 块为应用定义 Office 365 连接器。</span><span class="sxs-lookup"><span data-stu-id="156b2-377">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="156b2-378">对象是一个数组 (包含所有类型元素) 最多包含 1 个元素 `object` 。</span><span class="sxs-lookup"><span data-stu-id="156b2-378">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="156b2-379">只有提供连接器的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="156b2-379">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="156b2-380">名称</span><span class="sxs-lookup"><span data-stu-id="156b2-380">Name</span></span>| <span data-ttu-id="156b2-381">类型</span><span class="sxs-lookup"><span data-stu-id="156b2-381">Type</span></span>| <span data-ttu-id="156b2-382">最大大小</span><span class="sxs-lookup"><span data-stu-id="156b2-382">Maximum size</span></span> | <span data-ttu-id="156b2-383">必需</span><span class="sxs-lookup"><span data-stu-id="156b2-383">Required</span></span> | <span data-ttu-id="156b2-384">说明</span><span class="sxs-lookup"><span data-stu-id="156b2-384">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="156b2-385">string</span><span class="sxs-lookup"><span data-stu-id="156b2-385">string</span></span>|<span data-ttu-id="156b2-386">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-386">2048 characters</span></span>|<span data-ttu-id="156b2-387">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-387">✔</span></span>|<span data-ttu-id="156b2-388">配置https://使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="156b2-388">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="156b2-389">枚举数组</span><span class="sxs-lookup"><span data-stu-id="156b2-389">array of enums</span></span>|<span data-ttu-id="156b2-390">1 </span><span class="sxs-lookup"><span data-stu-id="156b2-390">1</span></span>|<span data-ttu-id="156b2-391">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-391">✔</span></span>|<span data-ttu-id="156b2-392">指定连接器是提供在频道上下文中的体验，还是仅针对单个用户提供体验 `team` `personal` ， () 。</span><span class="sxs-lookup"><span data-stu-id="156b2-392">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="156b2-393">目前，仅 `team` 支持范围。</span><span class="sxs-lookup"><span data-stu-id="156b2-393">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="156b2-394">string</span><span class="sxs-lookup"><span data-stu-id="156b2-394">string</span></span>|<span data-ttu-id="156b2-395">64 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-395">64 characters</span></span>|<span data-ttu-id="156b2-396">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-396">✔</span></span>|<span data-ttu-id="156b2-397">连接器的唯一标识符，与连接器开发人员仪表板中的 ID [相匹配](https://aka.ms/connectorsdashboard)。</span><span class="sxs-lookup"><span data-stu-id="156b2-397">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="156b2-398">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="156b2-398">composeExtensions</span></span>

<span data-ttu-id="156b2-399">**可选** — 数组</span><span class="sxs-lookup"><span data-stu-id="156b2-399">**Optional** — array</span></span>

<span data-ttu-id="156b2-400">定义应用的邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="156b2-400">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="156b2-401">2017 年 11 月，功能名称从"撰写扩展"更改为"邮件扩展"，但清单名称保持不变，以便现有扩展继续工作。</span><span class="sxs-lookup"><span data-stu-id="156b2-401">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="156b2-402">该项目是一个数组 (类型的所有元素) 最多包含 1 个元素 `object` 。</span><span class="sxs-lookup"><span data-stu-id="156b2-402">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="156b2-403">只有提供邮件扩展的解决方案才需要此块。</span><span class="sxs-lookup"><span data-stu-id="156b2-403">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="156b2-404">名称</span><span class="sxs-lookup"><span data-stu-id="156b2-404">Name</span></span>| <span data-ttu-id="156b2-405">类型</span><span class="sxs-lookup"><span data-stu-id="156b2-405">Type</span></span> | <span data-ttu-id="156b2-406">最大大小</span><span class="sxs-lookup"><span data-stu-id="156b2-406">Maximum Size</span></span> | <span data-ttu-id="156b2-407">必需</span><span class="sxs-lookup"><span data-stu-id="156b2-407">Required</span></span> | <span data-ttu-id="156b2-408">说明</span><span class="sxs-lookup"><span data-stu-id="156b2-408">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="156b2-409">string</span><span class="sxs-lookup"><span data-stu-id="156b2-409">string</span></span>|<span data-ttu-id="156b2-410">64</span><span class="sxs-lookup"><span data-stu-id="156b2-410">64</span></span>|<span data-ttu-id="156b2-411">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-411">✔</span></span>|<span data-ttu-id="156b2-412">自动程序支持消息传递扩展的唯一 Microsoft 应用 ID，在 Bot Framework 中注册。</span><span class="sxs-lookup"><span data-stu-id="156b2-412">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="156b2-413">这可能与整个应用 ID 相同。</span><span class="sxs-lookup"><span data-stu-id="156b2-413">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="156b2-414">对象数组</span><span class="sxs-lookup"><span data-stu-id="156b2-414">array of objects</span></span>|<span data-ttu-id="156b2-415">10 </span><span class="sxs-lookup"><span data-stu-id="156b2-415">10</span></span>|<span data-ttu-id="156b2-416">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-416">✔</span></span>|<span data-ttu-id="156b2-417">邮件扩展支持的命令数组</span><span class="sxs-lookup"><span data-stu-id="156b2-417">array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="156b2-418">boolean</span><span class="sxs-lookup"><span data-stu-id="156b2-418">boolean</span></span>|||<span data-ttu-id="156b2-419">一个值，指示用户是否可以更新邮件扩展的配置。</span><span class="sxs-lookup"><span data-stu-id="156b2-419">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="156b2-420">默认值：**False**。</span><span class="sxs-lookup"><span data-stu-id="156b2-420">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="156b2-421">对象数组</span><span class="sxs-lookup"><span data-stu-id="156b2-421">array of Objects</span></span>|<span data-ttu-id="156b2-422">5 </span><span class="sxs-lookup"><span data-stu-id="156b2-422">5</span></span>||<span data-ttu-id="156b2-423">允许当满足特定条件时调用应用的处理程序列表。</span><span class="sxs-lookup"><span data-stu-id="156b2-423">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="156b2-424">域还必须在 `validDomains`</span><span class="sxs-lookup"><span data-stu-id="156b2-424">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="156b2-425">string</span><span class="sxs-lookup"><span data-stu-id="156b2-425">string</span></span>|||<span data-ttu-id="156b2-426">消息处理程序的类型。</span><span class="sxs-lookup"><span data-stu-id="156b2-426">The type of message handler.</span></span> <span data-ttu-id="156b2-427">必须是 `"link"`。</span><span class="sxs-lookup"><span data-stu-id="156b2-427">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="156b2-428">字符串数组</span><span class="sxs-lookup"><span data-stu-id="156b2-428">array of Strings</span></span>|||<span data-ttu-id="156b2-429">链接消息处理程序可以注册的域数组。</span><span class="sxs-lookup"><span data-stu-id="156b2-429">array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="156b2-430">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="156b2-430">composeExtensions.commands</span></span>

<span data-ttu-id="156b2-431">邮件扩展应声明一个或多个命令。</span><span class="sxs-lookup"><span data-stu-id="156b2-431">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="156b2-432">每个命令在 Microsoft Teams 中显示为基于 UI 的入口点的潜在交互。</span><span class="sxs-lookup"><span data-stu-id="156b2-432">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="156b2-433">最多有 10 个命令。</span><span class="sxs-lookup"><span data-stu-id="156b2-433">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="156b2-434">每个命令项都是具有以下结构的对象：</span><span class="sxs-lookup"><span data-stu-id="156b2-434">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="156b2-435">名称</span><span class="sxs-lookup"><span data-stu-id="156b2-435">Name</span></span>| <span data-ttu-id="156b2-436">类型</span><span class="sxs-lookup"><span data-stu-id="156b2-436">Type</span></span>| <span data-ttu-id="156b2-437">最大大小</span><span class="sxs-lookup"><span data-stu-id="156b2-437">Maximum size</span></span> | <span data-ttu-id="156b2-438">必需</span><span class="sxs-lookup"><span data-stu-id="156b2-438">Required</span></span> | <span data-ttu-id="156b2-439">说明</span><span class="sxs-lookup"><span data-stu-id="156b2-439">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="156b2-440">string</span><span class="sxs-lookup"><span data-stu-id="156b2-440">string</span></span>|<span data-ttu-id="156b2-441">64 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-441">64 characters</span></span>|<span data-ttu-id="156b2-442">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-442">✔</span></span>|<span data-ttu-id="156b2-443">命令的 ID。</span><span class="sxs-lookup"><span data-stu-id="156b2-443">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="156b2-444">string</span><span class="sxs-lookup"><span data-stu-id="156b2-444">string</span></span>|<span data-ttu-id="156b2-445">32 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-445">32 characters</span></span>|<span data-ttu-id="156b2-446">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-446">✔</span></span>|<span data-ttu-id="156b2-447">用户友好命令名称。</span><span class="sxs-lookup"><span data-stu-id="156b2-447">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="156b2-448">string</span><span class="sxs-lookup"><span data-stu-id="156b2-448">string</span></span>|<span data-ttu-id="156b2-449">64 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-449">64 characters</span></span>||<span data-ttu-id="156b2-450">命令的类型。</span><span class="sxs-lookup"><span data-stu-id="156b2-450">Type of the command.</span></span> <span data-ttu-id="156b2-451">或 `query` `action` 之一。</span><span class="sxs-lookup"><span data-stu-id="156b2-451">One of `query` or `action`.</span></span> <span data-ttu-id="156b2-452">默认值： **查询**。</span><span class="sxs-lookup"><span data-stu-id="156b2-452">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="156b2-453">string</span><span class="sxs-lookup"><span data-stu-id="156b2-453">string</span></span>|<span data-ttu-id="156b2-454">128 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-454">128 characters</span></span>||<span data-ttu-id="156b2-455">向用户显示以指示此命令用途的说明。</span><span class="sxs-lookup"><span data-stu-id="156b2-455">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="156b2-456">boolean</span><span class="sxs-lookup"><span data-stu-id="156b2-456">boolean</span></span>|||<span data-ttu-id="156b2-457">一个布尔值，指示命令最初是否应该没有参数运行。</span><span class="sxs-lookup"><span data-stu-id="156b2-457">A boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="156b2-458">默认值：**False**。</span><span class="sxs-lookup"><span data-stu-id="156b2-458">Default: **false**.</span></span>|
|`context`|<span data-ttu-id="156b2-459">字符串数组</span><span class="sxs-lookup"><span data-stu-id="156b2-459">array of Strings</span></span>|<span data-ttu-id="156b2-460">3 </span><span class="sxs-lookup"><span data-stu-id="156b2-460">3</span></span>||<span data-ttu-id="156b2-461">定义可以从何处调用邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="156b2-461">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="156b2-462">`compose`， 的任意 `commandBox` 组合 `message` 。</span><span class="sxs-lookup"><span data-stu-id="156b2-462">Any combination of`compose`,`commandBox`,`message` .</span></span> <span data-ttu-id="156b2-463">默认值为 `["compose","commandBox"]`。</span><span class="sxs-lookup"><span data-stu-id="156b2-463">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="156b2-464">boolean</span><span class="sxs-lookup"><span data-stu-id="156b2-464">boolean</span></span>|||<span data-ttu-id="156b2-465">一个布尔值，指示它应动态获取任务模块。</span><span class="sxs-lookup"><span data-stu-id="156b2-465">A boolean value that indicates if it should fetch the task module dynamically.</span></span> <span data-ttu-id="156b2-466">默认值：**False**。</span><span class="sxs-lookup"><span data-stu-id="156b2-466">Default: **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="156b2-467">object</span><span class="sxs-lookup"><span data-stu-id="156b2-467">object</span></span>|||<span data-ttu-id="156b2-468">指定在使用邮件扩展命令时要预加载的任务模块。</span><span class="sxs-lookup"><span data-stu-id="156b2-468">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="156b2-469">string</span><span class="sxs-lookup"><span data-stu-id="156b2-469">string</span></span>|<span data-ttu-id="156b2-470">64 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-470">64 characters</span></span>||<span data-ttu-id="156b2-471">初始对话框标题。</span><span class="sxs-lookup"><span data-stu-id="156b2-471">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="156b2-472">string</span><span class="sxs-lookup"><span data-stu-id="156b2-472">string</span></span>|||<span data-ttu-id="156b2-473">对话框宽度 - 以像素为单位的一个数字或默认布局，例如"large"、"medium"或"small"。</span><span class="sxs-lookup"><span data-stu-id="156b2-473">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="156b2-474">string</span><span class="sxs-lookup"><span data-stu-id="156b2-474">string</span></span>|||<span data-ttu-id="156b2-475">对话框高度 - 一个数字（以像素为单位）或默认布局，如"large"、"medium"或"small"。</span><span class="sxs-lookup"><span data-stu-id="156b2-475">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="156b2-476">string</span><span class="sxs-lookup"><span data-stu-id="156b2-476">string</span></span>|||<span data-ttu-id="156b2-477">初始 webview URL。</span><span class="sxs-lookup"><span data-stu-id="156b2-477">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="156b2-478">对象数组</span><span class="sxs-lookup"><span data-stu-id="156b2-478">array of object</span></span>|<span data-ttu-id="156b2-479">5 项</span><span class="sxs-lookup"><span data-stu-id="156b2-479">5 items</span></span>|<span data-ttu-id="156b2-480">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-480">✔</span></span>|<span data-ttu-id="156b2-481">命令采用的参数列表。</span><span class="sxs-lookup"><span data-stu-id="156b2-481">The list of parameters the command takes.</span></span> <span data-ttu-id="156b2-482">最小值：1;最大值：5。</span><span class="sxs-lookup"><span data-stu-id="156b2-482">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="156b2-483">string</span><span class="sxs-lookup"><span data-stu-id="156b2-483">string</span></span>|<span data-ttu-id="156b2-484">64 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-484">64 characters</span></span>|<span data-ttu-id="156b2-485">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-485">✔</span></span>|<span data-ttu-id="156b2-486">显示在客户端中的参数的名称。</span><span class="sxs-lookup"><span data-stu-id="156b2-486">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="156b2-487">这包括在用户请求中。</span><span class="sxs-lookup"><span data-stu-id="156b2-487">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="156b2-488">string</span><span class="sxs-lookup"><span data-stu-id="156b2-488">string</span></span>|<span data-ttu-id="156b2-489">32 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-489">32 characters</span></span>|<span data-ttu-id="156b2-490">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-490">✔</span></span>|<span data-ttu-id="156b2-491">参数的用户友好标题。</span><span class="sxs-lookup"><span data-stu-id="156b2-491">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="156b2-492">string</span><span class="sxs-lookup"><span data-stu-id="156b2-492">string</span></span>|<span data-ttu-id="156b2-493">128 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-493">128 characters</span></span>||<span data-ttu-id="156b2-494">描述此参数用途的用户友好字符串。</span><span class="sxs-lookup"><span data-stu-id="156b2-494">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="156b2-495">string</span><span class="sxs-lookup"><span data-stu-id="156b2-495">string</span></span>|<span data-ttu-id="156b2-496">512 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-496">512 characters</span></span>||<span data-ttu-id="156b2-497">参数的初始值。</span><span class="sxs-lookup"><span data-stu-id="156b2-497">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="156b2-498">string</span><span class="sxs-lookup"><span data-stu-id="156b2-498">string</span></span>|<span data-ttu-id="156b2-499">128 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-499">128 characters</span></span>||<span data-ttu-id="156b2-500">定义在任务模块上显示的控件的类型 `fetchTask: true` 。</span><span class="sxs-lookup"><span data-stu-id="156b2-500">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="156b2-501">之一 `text, textarea, number, date, time, toggle, choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="156b2-501">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="156b2-502">对象数组</span><span class="sxs-lookup"><span data-stu-id="156b2-502">array of objects</span></span>|<span data-ttu-id="156b2-503">10 个项目</span><span class="sxs-lookup"><span data-stu-id="156b2-503">10 items</span></span>||<span data-ttu-id="156b2-504">`choiceset`的选项。</span><span class="sxs-lookup"><span data-stu-id="156b2-504">The choice options for the`choiceset`.</span></span> <span data-ttu-id="156b2-505">仅在为 `parameter.inputType` `choiceset` 时使用。</span><span class="sxs-lookup"><span data-stu-id="156b2-505">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="156b2-506">string</span><span class="sxs-lookup"><span data-stu-id="156b2-506">string</span></span>|<span data-ttu-id="156b2-507">128 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-507">128 characters</span></span>|<span data-ttu-id="156b2-508">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-508">✔</span></span>|<span data-ttu-id="156b2-509">选项的标题。</span><span class="sxs-lookup"><span data-stu-id="156b2-509">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="156b2-510">string</span><span class="sxs-lookup"><span data-stu-id="156b2-510">string</span></span>|<span data-ttu-id="156b2-511">512 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-511">512 characters</span></span>|<span data-ttu-id="156b2-512">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-512">✔</span></span>|<span data-ttu-id="156b2-513">选项的值。</span><span class="sxs-lookup"><span data-stu-id="156b2-513">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="156b2-514">permissions</span><span class="sxs-lookup"><span data-stu-id="156b2-514">permissions</span></span>

<span data-ttu-id="156b2-515">**可选** — 字符串数组</span><span class="sxs-lookup"><span data-stu-id="156b2-515">**Optional** — array of strings</span></span>

<span data-ttu-id="156b2-516">一个数组，指定应用请求哪些权限，使最终用户 `string` 知道扩展将执行什么操作。</span><span class="sxs-lookup"><span data-stu-id="156b2-516">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="156b2-517">以下选项非独占：</span><span class="sxs-lookup"><span data-stu-id="156b2-517">The following options are non-exclusive:</span></span>

* <span data-ttu-id="156b2-518">`identity`&emsp;需要用户标识信息</span><span class="sxs-lookup"><span data-stu-id="156b2-518">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="156b2-519">`messageTeamMembers`&emsp;需要向团队成员发送直接消息的权限</span><span class="sxs-lookup"><span data-stu-id="156b2-519">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="156b2-520">在更新应用时更改这些权限将导致用户在首次运行更新后的应用时重复同意过程。</span><span class="sxs-lookup"><span data-stu-id="156b2-520">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="156b2-521">有关详细信息 [，请参阅更新](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) 应用。</span><span class="sxs-lookup"><span data-stu-id="156b2-521">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="156b2-522">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="156b2-522">devicePermissions</span></span>

<span data-ttu-id="156b2-523">**可选** — 字符串数组</span><span class="sxs-lookup"><span data-stu-id="156b2-523">**Optional** — array of strings</span></span>

<span data-ttu-id="156b2-524">指定应用可能请求访问的用户设备上本机功能。</span><span class="sxs-lookup"><span data-stu-id="156b2-524">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="156b2-525">选项包括：</span><span class="sxs-lookup"><span data-stu-id="156b2-525">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="156b2-526">validDomains</span><span class="sxs-lookup"><span data-stu-id="156b2-526">validDomains</span></span>

<span data-ttu-id="156b2-527">**可选**，除非 **有说明的必需** 项</span><span class="sxs-lookup"><span data-stu-id="156b2-527">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="156b2-528">应用预期在 Teams 客户端内加载的网站的有效域列表。</span><span class="sxs-lookup"><span data-stu-id="156b2-528">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="156b2-529">域列表可以包括通配符，例如 `*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="156b2-529">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="156b2-530">这完全匹配域的一个段;如果需要匹配，请使用 `a.b.example.com` `*.*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="156b2-530">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="156b2-531">如果你的选项卡配置或内容 UI 需要导航到除用于选项卡配置的域之外的其他任何域，则必须在此处指定该域。</span><span class="sxs-lookup"><span data-stu-id="156b2-531">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="156b2-532">但是 **，** 不需要在应用中包括要支持的标识提供程序的域。</span><span class="sxs-lookup"><span data-stu-id="156b2-532">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="156b2-533">例如，若要使用 Google ID 进行身份验证，必须重定向到 accounts.google.com，但不应在 accounts.google.com 中 `validDomains[]` 。</span><span class="sxs-lookup"><span data-stu-id="156b2-533">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="156b2-534">需要自己的 sharepoint URL 正常运行的 Teams 应用可能将"{teamsitedomain}"包括在有效的域列表中。</span><span class="sxs-lookup"><span data-stu-id="156b2-534">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="156b2-535">不要直接或通过通配符添加超出你控制的域。</span><span class="sxs-lookup"><span data-stu-id="156b2-535">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="156b2-536">例如， `yourapp.onmicrosoft.com` 有效，但 `*.onmicrosoft.com` 无效。</span><span class="sxs-lookup"><span data-stu-id="156b2-536">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="156b2-537">对象是包含类型的所有元素的数组 `string` 。</span><span class="sxs-lookup"><span data-stu-id="156b2-537">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="156b2-538">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="156b2-538">webApplicationInfo</span></span>

<span data-ttu-id="156b2-539">**可选** — 对象</span><span class="sxs-lookup"><span data-stu-id="156b2-539">**Optional** — object</span></span>

<span data-ttu-id="156b2-540">指定 Azure Active Directory (Azure AD) 应用 ID 和 Microsoft Graph 信息，以帮助用户无缝登录你的应用。</span><span class="sxs-lookup"><span data-stu-id="156b2-540">Specify your Azure Active Directory (Azure AD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="156b2-541">如果你的应用在 Azure AD 中注册，则必须提供应用 ID，以便管理员可以轻松地在 Teams 管理中心查看权限并授予同意。</span><span class="sxs-lookup"><span data-stu-id="156b2-541">If your app is registered in Azure AD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="156b2-542">名称</span><span class="sxs-lookup"><span data-stu-id="156b2-542">Name</span></span>| <span data-ttu-id="156b2-543">类型</span><span class="sxs-lookup"><span data-stu-id="156b2-543">Type</span></span>| <span data-ttu-id="156b2-544">最大大小</span><span class="sxs-lookup"><span data-stu-id="156b2-544">Maximum size</span></span> | <span data-ttu-id="156b2-545">必需</span><span class="sxs-lookup"><span data-stu-id="156b2-545">Required</span></span> | <span data-ttu-id="156b2-546">说明</span><span class="sxs-lookup"><span data-stu-id="156b2-546">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="156b2-547">string</span><span class="sxs-lookup"><span data-stu-id="156b2-547">string</span></span>|<span data-ttu-id="156b2-548">36 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-548">36 characters</span></span>|<span data-ttu-id="156b2-549">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-549">✔</span></span>|<span data-ttu-id="156b2-550">应用的 AAD 应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="156b2-550">AAD application id of the app.</span></span> <span data-ttu-id="156b2-551">此 ID 必须是 GUID。</span><span class="sxs-lookup"><span data-stu-id="156b2-551">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="156b2-552">string</span><span class="sxs-lookup"><span data-stu-id="156b2-552">string</span></span>|<span data-ttu-id="156b2-553">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-553">2048 characters</span></span>|<span data-ttu-id="156b2-554">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-554">✔</span></span>|<span data-ttu-id="156b2-555">用于获取 SSO 身份验证令牌的应用的资源 URL。</span><span class="sxs-lookup"><span data-stu-id="156b2-555">Resource url of app for acquiring auth token for SSO.</span></span>|
|`applicationPermissions`|<span data-ttu-id="156b2-556">array of strings</span><span class="sxs-lookup"><span data-stu-id="156b2-556">array of strings</span></span>|<span data-ttu-id="156b2-557">128 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-557">128 characters</span></span>||<span data-ttu-id="156b2-558">指定 [具体资源特定许可](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="156b2-558">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="156b2-559">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="156b2-559">showLoadingIndicator</span></span>

<span data-ttu-id="156b2-560">**可选** — 布尔值</span><span class="sxs-lookup"><span data-stu-id="156b2-560">**Optional** — boolean</span></span>

<span data-ttu-id="156b2-561">指示加载应用/选项卡时是否显示加载指示器。</span><span class="sxs-lookup"><span data-stu-id="156b2-561">Indicate whether or not to show the loading indicator when an app/tab is loading.</span></span> <span data-ttu-id="156b2-562">默认值：**False**。</span><span class="sxs-lookup"><span data-stu-id="156b2-562">Default: **false**.</span></span>
>[!NOTE]
><span data-ttu-id="156b2-563">如果在应用清单中设置"showLoadingIndicator ： true"，那么，若要正确加载页面，必须按"显示本机加载指示器文档"中所述的协议修改选项卡和任务模块的内容页。 [](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)</span><span class="sxs-lookup"><span data-stu-id="156b2-563">If you set "showLoadingIndicator : true" in your app manifest, then for the page to load correctly, you must modify the content pages of your tabs and task modules as per the protocol described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="156b2-564">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="156b2-564">isFullScreen</span></span>

 <span data-ttu-id="156b2-565">**可选** — 布尔值</span><span class="sxs-lookup"><span data-stu-id="156b2-565">**Optional** — boolean</span></span>

<span data-ttu-id="156b2-566">指示使用选项卡标题栏或不带选项卡标题栏呈现个人应用的地方。</span><span class="sxs-lookup"><span data-stu-id="156b2-566">Indicate where a personal app is rendered with or without a tab-header bar.</span></span> <span data-ttu-id="156b2-567">默认值：**False**。</span><span class="sxs-lookup"><span data-stu-id="156b2-567">Default: **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="156b2-568">activities</span><span class="sxs-lookup"><span data-stu-id="156b2-568">activities</span></span>

<span data-ttu-id="156b2-569">**可选** — 对象</span><span class="sxs-lookup"><span data-stu-id="156b2-569">**Optional** — object</span></span>

<span data-ttu-id="156b2-570">定义应用用于向用户活动源发布的属性。</span><span class="sxs-lookup"><span data-stu-id="156b2-570">Define the properties your app will use to post to a user activity feed.</span></span>

|<span data-ttu-id="156b2-571">名称</span><span class="sxs-lookup"><span data-stu-id="156b2-571">Name</span></span>| <span data-ttu-id="156b2-572">类型</span><span class="sxs-lookup"><span data-stu-id="156b2-572">Type</span></span>| <span data-ttu-id="156b2-573">最大大小</span><span class="sxs-lookup"><span data-stu-id="156b2-573">Maximum size</span></span> | <span data-ttu-id="156b2-574">必需</span><span class="sxs-lookup"><span data-stu-id="156b2-574">Required</span></span> | <span data-ttu-id="156b2-575">说明</span><span class="sxs-lookup"><span data-stu-id="156b2-575">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="156b2-576">对象数组</span><span class="sxs-lookup"><span data-stu-id="156b2-576">array of Objects</span></span>|<span data-ttu-id="156b2-577">128 个项目</span><span class="sxs-lookup"><span data-stu-id="156b2-577">128 items</span></span>| | <span data-ttu-id="156b2-578">指定你的应用可以发布给用户活动源的活动类型。</span><span class="sxs-lookup"><span data-stu-id="156b2-578">Specify the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="156b2-579">activities.activityTypes</span><span class="sxs-lookup"><span data-stu-id="156b2-579">activities.activityTypes</span></span>

|<span data-ttu-id="156b2-580">名称</span><span class="sxs-lookup"><span data-stu-id="156b2-580">Name</span></span>| <span data-ttu-id="156b2-581">类型</span><span class="sxs-lookup"><span data-stu-id="156b2-581">Type</span></span>| <span data-ttu-id="156b2-582">最大大小</span><span class="sxs-lookup"><span data-stu-id="156b2-582">Maximum size</span></span> | <span data-ttu-id="156b2-583">必需</span><span class="sxs-lookup"><span data-stu-id="156b2-583">Required</span></span> | <span data-ttu-id="156b2-584">说明</span><span class="sxs-lookup"><span data-stu-id="156b2-584">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="156b2-585">string</span><span class="sxs-lookup"><span data-stu-id="156b2-585">string</span></span>|<span data-ttu-id="156b2-586">32 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-586">32 characters</span></span>|<span data-ttu-id="156b2-587">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-587">✔</span></span>|<span data-ttu-id="156b2-588">通知类型。</span><span class="sxs-lookup"><span data-stu-id="156b2-588">The notification type.</span></span> <span data-ttu-id="156b2-589">*请参阅下文*。</span><span class="sxs-lookup"><span data-stu-id="156b2-589">*See below*.</span></span>|
|`description`|<span data-ttu-id="156b2-590">string</span><span class="sxs-lookup"><span data-stu-id="156b2-590">string</span></span>|<span data-ttu-id="156b2-591">128 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-591">128 characters</span></span>|<span data-ttu-id="156b2-592">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-592">✔</span></span>|<span data-ttu-id="156b2-593">通知的简短说明。</span><span class="sxs-lookup"><span data-stu-id="156b2-593">A brief description of the notification.</span></span> <span data-ttu-id="156b2-594">*请参阅下文*。</span><span class="sxs-lookup"><span data-stu-id="156b2-594">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="156b2-595">string</span><span class="sxs-lookup"><span data-stu-id="156b2-595">string</span></span>|<span data-ttu-id="156b2-596">128 个字符</span><span class="sxs-lookup"><span data-stu-id="156b2-596">128 characters</span></span>|<span data-ttu-id="156b2-597">✔</span><span class="sxs-lookup"><span data-stu-id="156b2-597">✔</span></span>|<span data-ttu-id="156b2-598">例如："{actor} 已创建任务 {taskId} "</span><span class="sxs-lookup"><span data-stu-id="156b2-598">Ex: "{actor} created task {taskId} for you"</span></span>|

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
