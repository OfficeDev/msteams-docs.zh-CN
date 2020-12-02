---
title: 清单架构参考
description: 介绍 Microsoft 团队的清单架构
keywords: 团队清单架构
author: laujan
ms.author: lajanuar
ms.openlocfilehash: 26c6ca0ed6edceb9b34c84c28a43a63f65a348de
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552554"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="11093-104">参考： Microsoft 团队的清单架构</span><span class="sxs-lookup"><span data-stu-id="11093-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="11093-105">Microsoft 团队清单介绍了应用程序如何集成到 Microsoft 团队产品中。</span><span class="sxs-lookup"><span data-stu-id="11093-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="11093-106">您的清单必须符合托管的架构 [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json) 。</span><span class="sxs-lookup"><span data-stu-id="11093-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="11093-107">在 URL) 中使用 "v1" 时，也 (支持早期版本 1.0-1.4。</span><span class="sxs-lookup"><span data-stu-id="11093-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="11093-108">以下架构示例显示了所有扩展性选项。</span><span class="sxs-lookup"><span data-stu-id="11093-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="11093-109">完整清单示例</span><span class="sxs-lookup"><span data-stu-id="11093-109">Sample full manifest</span></span>

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

<span data-ttu-id="11093-110">架构定义了以下属性：</span><span class="sxs-lookup"><span data-stu-id="11093-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="11093-111">$schema</span><span class="sxs-lookup"><span data-stu-id="11093-111">$schema</span></span>

<span data-ttu-id="11093-112">*可选，但建议* —字符串</span><span class="sxs-lookup"><span data-stu-id="11093-112">*Optional, but recommended* — string</span></span>

<span data-ttu-id="11093-113">引用清单的 JSON 架构的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="11093-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="11093-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="11093-114">manifestVersion</span></span>

<span data-ttu-id="11093-115">**必需** -字符串</span><span class="sxs-lookup"><span data-stu-id="11093-115">**Required** — string</span></span>

<span data-ttu-id="11093-116">此清单使用的清单架构的版本。</span><span class="sxs-lookup"><span data-stu-id="11093-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="11093-117">它应为 "1.7"。</span><span class="sxs-lookup"><span data-stu-id="11093-117">It should be "1.7".</span></span>

## <a name="version"></a><span data-ttu-id="11093-118">version</span><span class="sxs-lookup"><span data-stu-id="11093-118">version</span></span>

<span data-ttu-id="11093-119">**必需** -字符串</span><span class="sxs-lookup"><span data-stu-id="11093-119">**Required** — string</span></span>

<span data-ttu-id="11093-120">特定应用程序的版本。</span><span class="sxs-lookup"><span data-stu-id="11093-120">The version of the specific app.</span></span> <span data-ttu-id="11093-121">如果您更新清单中的某些内容，该版本还必须递增。</span><span class="sxs-lookup"><span data-stu-id="11093-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="11093-122">这样一来，在安装新的清单时，它将覆盖现有的版本，用户将获得新的功能。</span><span class="sxs-lookup"><span data-stu-id="11093-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="11093-123">如果此应用程序已提交到应用商店，则必须重新提交新清单，然后再对其进行重新验证。</span><span class="sxs-lookup"><span data-stu-id="11093-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="11093-124">然后，此应用程序的用户将在几小时内自动获取新更新的清单（在批准后）。</span><span class="sxs-lookup"><span data-stu-id="11093-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="11093-125">如果应用程序要求更改权限，则系统将提示用户升级并重新同意该应用。</span><span class="sxs-lookup"><span data-stu-id="11093-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="11093-126">此版本字符串必须遵循 [semver](http://semver.org/) STANDARD (主要版本。网格.PATCH) 。</span><span class="sxs-lookup"><span data-stu-id="11093-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="11093-127">id</span><span class="sxs-lookup"><span data-stu-id="11093-127">id</span></span>

<span data-ttu-id="11093-128">**必需** — MICROSOFT app ID</span><span class="sxs-lookup"><span data-stu-id="11093-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="11093-129">Microsoft 为此应用程序生成的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="11093-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="11093-130">如果你已通过 Microsoft Bot 框架注册了 bot，或者你的选项卡的 web 应用已使用 Microsoft 登录，则你应该已经有 ID，应在此处输入它。</span><span class="sxs-lookup"><span data-stu-id="11093-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="11093-131">否则，应在 Microsoft 应用程序注册门户 ([我的应用程序](https://apps.dev.microsoft.com) ") 上生成一个新的 ID，在此处输入它，然后在添加机器人时重用它。注意：如果您在 AppSource 中提交对现有应用程序的更新，您的清单中的 ID 不得修改。</span><span class="sxs-lookup"><span data-stu-id="11093-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="11093-132">developer</span><span class="sxs-lookup"><span data-stu-id="11093-132">developer</span></span>

<span data-ttu-id="11093-133">**必需** -对象</span><span class="sxs-lookup"><span data-stu-id="11093-133">**Required** — object</span></span>

<span data-ttu-id="11093-134">指定有关贵公司的信息。</span><span class="sxs-lookup"><span data-stu-id="11093-134">Specifies information about your company.</span></span> <span data-ttu-id="11093-135">对于提交到 AppSource 的应用程序 (以前的 Office 应用商店) ，这些值必须与您的 AppSource 条目中的信息相匹配。</span><span class="sxs-lookup"><span data-stu-id="11093-135">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="11093-136">有关详细信息，请参阅我们的 [发布指南](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) 。</span><span class="sxs-lookup"><span data-stu-id="11093-136">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="11093-137">名称</span><span class="sxs-lookup"><span data-stu-id="11093-137">Name</span></span>| <span data-ttu-id="11093-138">最大大小</span><span class="sxs-lookup"><span data-stu-id="11093-138">Maximum size</span></span> | <span data-ttu-id="11093-139">必需</span><span class="sxs-lookup"><span data-stu-id="11093-139">Required</span></span> | <span data-ttu-id="11093-140">说明</span><span class="sxs-lookup"><span data-stu-id="11093-140">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="11093-141">32个字符</span><span class="sxs-lookup"><span data-stu-id="11093-141">32 characters</span></span>|<span data-ttu-id="11093-142">✔</span><span class="sxs-lookup"><span data-stu-id="11093-142">✔</span></span>|<span data-ttu-id="11093-143">开发人员的显示名称。</span><span class="sxs-lookup"><span data-stu-id="11093-143">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="11093-144">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="11093-144">2048 characters</span></span>|<span data-ttu-id="11093-145">✔</span><span class="sxs-lookup"><span data-stu-id="11093-145">✔</span></span>|<span data-ttu-id="11093-146">开发人员网站的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="11093-146">The https:// URL to the developer's website.</span></span> <span data-ttu-id="11093-147">此链接应将用户带到您的公司或特定于产品的登陆页面。</span><span class="sxs-lookup"><span data-stu-id="11093-147">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="11093-148">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="11093-148">2048 characters</span></span>|<span data-ttu-id="11093-149">✔</span><span class="sxs-lookup"><span data-stu-id="11093-149">✔</span></span>|<span data-ttu-id="11093-150">开发人员的隐私策略的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="11093-150">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="11093-151">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="11093-151">2048 characters</span></span>|<span data-ttu-id="11093-152">✔</span><span class="sxs-lookup"><span data-stu-id="11093-152">✔</span></span>|<span data-ttu-id="11093-153">开发人员使用条款的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="11093-153">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="11093-154">10个字符</span><span class="sxs-lookup"><span data-stu-id="11093-154">10 characters</span></span>| |<span data-ttu-id="11093-155">**可选** 用于标识合作伙伴组织构建应用程序的 Microsoft 合作伙伴网络 ID。</span><span class="sxs-lookup"><span data-stu-id="11093-155">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="11093-156">name</span><span class="sxs-lookup"><span data-stu-id="11093-156">name</span></span>

<span data-ttu-id="11093-157">**必需** -对象</span><span class="sxs-lookup"><span data-stu-id="11093-157">**Required** — object</span></span>

<span data-ttu-id="11093-158">在团队体验中向用户显示的应用程序体验的名称。</span><span class="sxs-lookup"><span data-stu-id="11093-158">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="11093-159">对于提交到 AppSource 的应用程序，这些值必须与您的 AppSource 条目中的信息相匹配。</span><span class="sxs-lookup"><span data-stu-id="11093-159">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="11093-160">和的值 `short` `full` 不应相同。</span><span class="sxs-lookup"><span data-stu-id="11093-160">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="11093-161">名称</span><span class="sxs-lookup"><span data-stu-id="11093-161">Name</span></span>| <span data-ttu-id="11093-162">最大大小</span><span class="sxs-lookup"><span data-stu-id="11093-162">Maximum size</span></span> | <span data-ttu-id="11093-163">必需</span><span class="sxs-lookup"><span data-stu-id="11093-163">Required</span></span> | <span data-ttu-id="11093-164">说明</span><span class="sxs-lookup"><span data-stu-id="11093-164">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="11093-165">30 个字符</span><span class="sxs-lookup"><span data-stu-id="11093-165">30 characters</span></span>|<span data-ttu-id="11093-166">✔</span><span class="sxs-lookup"><span data-stu-id="11093-166">✔</span></span>|<span data-ttu-id="11093-167">应用程序的短显示名称。</span><span class="sxs-lookup"><span data-stu-id="11093-167">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="11093-168">100 个字符</span><span class="sxs-lookup"><span data-stu-id="11093-168">100 characters</span></span>||<span data-ttu-id="11093-169">应用程序的全名，如果完整的应用程序名称超过30个字符，则使用该名称。</span><span class="sxs-lookup"><span data-stu-id="11093-169">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="11093-170">说明</span><span class="sxs-lookup"><span data-stu-id="11093-170">description</span></span>

<span data-ttu-id="11093-171">**必需** -对象</span><span class="sxs-lookup"><span data-stu-id="11093-171">**Required** — object</span></span>

<span data-ttu-id="11093-172">向用户介绍你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="11093-172">Describes your app to users.</span></span> <span data-ttu-id="11093-173">对于提交到 AppSource 的应用程序，这些值必须与您的 AppSource 条目中的信息相匹配。</span><span class="sxs-lookup"><span data-stu-id="11093-173">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="11093-174">确保你的说明准确描述你的体验，并提供信息，以帮助潜在客户了解你的体验。</span><span class="sxs-lookup"><span data-stu-id="11093-174">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="11093-175">如果需要使用外部帐户，还应在完整说明中说明。</span><span class="sxs-lookup"><span data-stu-id="11093-175">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="11093-176">和的值 `short` `full` 不应相同。</span><span class="sxs-lookup"><span data-stu-id="11093-176">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="11093-177">您的简短说明不得在详细说明中重复，并且不得包含任何其他应用程序名称。</span><span class="sxs-lookup"><span data-stu-id="11093-177">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="11093-178">名称</span><span class="sxs-lookup"><span data-stu-id="11093-178">Name</span></span>| <span data-ttu-id="11093-179">最大大小</span><span class="sxs-lookup"><span data-stu-id="11093-179">Maximum size</span></span> | <span data-ttu-id="11093-180">必需</span><span class="sxs-lookup"><span data-stu-id="11093-180">Required</span></span> | <span data-ttu-id="11093-181">说明</span><span class="sxs-lookup"><span data-stu-id="11093-181">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="11093-182">80个字符</span><span class="sxs-lookup"><span data-stu-id="11093-182">80 characters</span></span>|<span data-ttu-id="11093-183">✔</span><span class="sxs-lookup"><span data-stu-id="11093-183">✔</span></span>|<span data-ttu-id="11093-184">在空间有限时使用的应用程序体验的简短说明。</span><span class="sxs-lookup"><span data-stu-id="11093-184">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="11093-185">4000个字符</span><span class="sxs-lookup"><span data-stu-id="11093-185">4000 characters</span></span>|<span data-ttu-id="11093-186">✔</span><span class="sxs-lookup"><span data-stu-id="11093-186">✔</span></span>|<span data-ttu-id="11093-187">您的应用程序的完整说明。</span><span class="sxs-lookup"><span data-stu-id="11093-187">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="11093-188">packageName</span><span class="sxs-lookup"><span data-stu-id="11093-188">packageName</span></span>

<span data-ttu-id="11093-189">**Optional** -string</span><span class="sxs-lookup"><span data-stu-id="11093-189">**Optional** — string</span></span>

<span data-ttu-id="11093-190">此应用的以反向域表示法表示的唯一标识符;例如，.com. myapp。</span><span class="sxs-lookup"><span data-stu-id="11093-190">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="11093-191">最大长度：64 个字符。</span><span class="sxs-lookup"><span data-stu-id="11093-191">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="11093-192">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="11093-192">localizationInfo</span></span>

<span data-ttu-id="11093-193">**Optional** —对象</span><span class="sxs-lookup"><span data-stu-id="11093-193">**Optional** — object</span></span>

<span data-ttu-id="11093-194">允许指定默认语言，以及指向其他语言文件的指针。</span><span class="sxs-lookup"><span data-stu-id="11093-194">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="11093-195">请参阅 [本地化](~/concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="11093-195">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="11093-196">名称</span><span class="sxs-lookup"><span data-stu-id="11093-196">Name</span></span>| <span data-ttu-id="11093-197">最大大小</span><span class="sxs-lookup"><span data-stu-id="11093-197">Maximum size</span></span> | <span data-ttu-id="11093-198">必需</span><span class="sxs-lookup"><span data-stu-id="11093-198">Required</span></span> | <span data-ttu-id="11093-199">说明</span><span class="sxs-lookup"><span data-stu-id="11093-199">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="11093-200">✔</span><span class="sxs-lookup"><span data-stu-id="11093-200">✔</span></span>|<span data-ttu-id="11093-201">此顶级清单文件中的字符串的语言标记。</span><span class="sxs-lookup"><span data-stu-id="11093-201">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="11093-202">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="11093-202">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="11093-203">指定其他语言翻译的对象的数组。</span><span class="sxs-lookup"><span data-stu-id="11093-203">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="11093-204">名称</span><span class="sxs-lookup"><span data-stu-id="11093-204">Name</span></span>| <span data-ttu-id="11093-205">最大大小</span><span class="sxs-lookup"><span data-stu-id="11093-205">Maximum size</span></span> | <span data-ttu-id="11093-206">必需</span><span class="sxs-lookup"><span data-stu-id="11093-206">Required</span></span> | <span data-ttu-id="11093-207">说明</span><span class="sxs-lookup"><span data-stu-id="11093-207">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="11093-208">✔</span><span class="sxs-lookup"><span data-stu-id="11093-208">✔</span></span>|<span data-ttu-id="11093-209">所提供文件中的字符串的语言标记。</span><span class="sxs-lookup"><span data-stu-id="11093-209">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="11093-210">✔</span><span class="sxs-lookup"><span data-stu-id="11093-210">✔</span></span>|<span data-ttu-id="11093-211">包含翻译字符串的 json 文件的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="11093-211">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="11093-212">图标</span><span class="sxs-lookup"><span data-stu-id="11093-212">icons</span></span>

<span data-ttu-id="11093-213">**必需** -对象</span><span class="sxs-lookup"><span data-stu-id="11093-213">**Required** — object</span></span>

<span data-ttu-id="11093-214">在团队应用程序中使用的图标。</span><span class="sxs-lookup"><span data-stu-id="11093-214">Icons used within the Teams app.</span></span> <span data-ttu-id="11093-215">图标文件必须作为上载包的一部分包括在内。</span><span class="sxs-lookup"><span data-stu-id="11093-215">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="11093-216">有关详细信息，请参阅 [图标](~/concepts/build-and-test/apps-package.md#icons) 。</span><span class="sxs-lookup"><span data-stu-id="11093-216">See [Icons](~/concepts/build-and-test/apps-package.md#icons) for more information.</span></span>

|<span data-ttu-id="11093-217">名称</span><span class="sxs-lookup"><span data-stu-id="11093-217">Name</span></span>| <span data-ttu-id="11093-218">最大大小</span><span class="sxs-lookup"><span data-stu-id="11093-218">Maximum size</span></span> | <span data-ttu-id="11093-219">必需</span><span class="sxs-lookup"><span data-stu-id="11093-219">Required</span></span> | <span data-ttu-id="11093-220">说明</span><span class="sxs-lookup"><span data-stu-id="11093-220">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="11093-221">32 x 32 像素</span><span class="sxs-lookup"><span data-stu-id="11093-221">32 x 32 pixels</span></span>|<span data-ttu-id="11093-222">✔</span><span class="sxs-lookup"><span data-stu-id="11093-222">✔</span></span>|<span data-ttu-id="11093-223">指向透明 32x32 PNG 边框图标的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="11093-223">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="11093-224">192 x 192 像素</span><span class="sxs-lookup"><span data-stu-id="11093-224">192 x 192 pixels</span></span>|<span data-ttu-id="11093-225">✔</span><span class="sxs-lookup"><span data-stu-id="11093-225">✔</span></span>|<span data-ttu-id="11093-226">完整颜色 192x192 PNG 图标的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="11093-226">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="11093-227">accentColor</span><span class="sxs-lookup"><span data-stu-id="11093-227">accentColor</span></span>

<span data-ttu-id="11093-228">**可选** — HTML 十六进制颜色代码</span><span class="sxs-lookup"><span data-stu-id="11093-228">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="11093-229">与大纲图标的背景一起使用的颜色。</span><span class="sxs-lookup"><span data-stu-id="11093-229">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="11093-230">值必须是以 "#" 开头的有效 HTML 颜色代码，例如 `#4464ee` 。</span><span class="sxs-lookup"><span data-stu-id="11093-230">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="11093-231">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="11093-231">configurableTabs</span></span>

<span data-ttu-id="11093-232">**Optional** — array</span><span class="sxs-lookup"><span data-stu-id="11093-232">**Optional** — array</span></span>

<span data-ttu-id="11093-233">当您的应用程序体验具有在添加之前需要额外配置的团队频道选项卡体验时使用。</span><span class="sxs-lookup"><span data-stu-id="11093-233">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="11093-234">只有在不是个人) 的团队 (范围中支持可配置的选项卡，并且每个应用程序目前仅支持 **一个** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="11093-234">Configurable tabs are supported only in the teams scope (not personal), and currently only **one** tab per app is supported.</span></span>

|<span data-ttu-id="11093-235">名称</span><span class="sxs-lookup"><span data-stu-id="11093-235">Name</span></span>| <span data-ttu-id="11093-236">类型</span><span class="sxs-lookup"><span data-stu-id="11093-236">Type</span></span>| <span data-ttu-id="11093-237">最大大小</span><span class="sxs-lookup"><span data-stu-id="11093-237">Maximum size</span></span> | <span data-ttu-id="11093-238">必需</span><span class="sxs-lookup"><span data-stu-id="11093-238">Required</span></span> | <span data-ttu-id="11093-239">说明</span><span class="sxs-lookup"><span data-stu-id="11093-239">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="11093-240">string</span><span class="sxs-lookup"><span data-stu-id="11093-240">string</span></span>|<span data-ttu-id="11093-241">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="11093-241">2048 characters</span></span>|<span data-ttu-id="11093-242">✔</span><span class="sxs-lookup"><span data-stu-id="11093-242">✔</span></span>|<span data-ttu-id="11093-243">配置选项卡时要使用的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="11093-243">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="11093-244">枚举数组</span><span class="sxs-lookup"><span data-stu-id="11093-244">array of enums</span></span>|<span data-ttu-id="11093-245">1</span><span class="sxs-lookup"><span data-stu-id="11093-245">1</span></span>|<span data-ttu-id="11093-246">✔</span><span class="sxs-lookup"><span data-stu-id="11093-246">✔</span></span>|<span data-ttu-id="11093-247">目前，可配置的选项卡仅支持 `team` 和 `groupchat` 范围。</span><span class="sxs-lookup"><span data-stu-id="11093-247">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="11093-248">boolean</span><span class="sxs-lookup"><span data-stu-id="11093-248">boolean</span></span>|||<span data-ttu-id="11093-249">一个值，指示是否可在用户创建之后更新该选项卡的配置实例。</span><span class="sxs-lookup"><span data-stu-id="11093-249">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="11093-250">默认值： **true**。</span><span class="sxs-lookup"><span data-stu-id="11093-250">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="11093-251">枚举数组</span><span class="sxs-lookup"><span data-stu-id="11093-251">array of enums</span></span>|<span data-ttu-id="11093-252">6 </span><span class="sxs-lookup"><span data-stu-id="11093-252">6</span></span>||<span data-ttu-id="11093-253">`contextItem`支持选项卡的作用域集。</span><span class="sxs-lookup"><span data-stu-id="11093-253">The set of `contextItem` scopes where a tab is supported.</span></span> <span data-ttu-id="11093-254">默认值： **[channelTab、privateChatTab、meetingChatTab、meetingDetailsTab]**。</span><span class="sxs-lookup"><span data-stu-id="11093-254">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="11093-255">string</span><span class="sxs-lookup"><span data-stu-id="11093-255">string</span></span>|<span data-ttu-id="11093-256">2048</span><span class="sxs-lookup"><span data-stu-id="11093-256">2048</span></span>||<span data-ttu-id="11093-257">要在 SharePoint 中使用的选项卡预览图像的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="11093-257">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="11093-258">字号（1024x768）。</span><span class="sxs-lookup"><span data-stu-id="11093-258">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="11093-259">枚举数组</span><span class="sxs-lookup"><span data-stu-id="11093-259">array of enums</span></span>|<span data-ttu-id="11093-260">1</span><span class="sxs-lookup"><span data-stu-id="11093-260">1</span></span>||<span data-ttu-id="11093-261">定义您的选项卡在 SharePoint 中的可用方式。</span><span class="sxs-lookup"><span data-stu-id="11093-261">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="11093-262">选项包括 `sharePointFullPage` 和 `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="11093-262">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="11093-263">staticTabs</span><span class="sxs-lookup"><span data-stu-id="11093-263">staticTabs</span></span>

<span data-ttu-id="11093-264">**Optional** — array</span><span class="sxs-lookup"><span data-stu-id="11093-264">**Optional** — array</span></span>

<span data-ttu-id="11093-265">定义一组可在默认情况下 "固定" 的选项卡，而无需用户手动添加它们。</span><span class="sxs-lookup"><span data-stu-id="11093-265">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="11093-266">在范围内声明的静态制表符 `personal` 始终固定到应用的个人体验中。</span><span class="sxs-lookup"><span data-stu-id="11093-266">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="11093-267">当前不支持在范围中声明的静态选项卡 `team` 。</span><span class="sxs-lookup"><span data-stu-id="11093-267">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="11093-268">此项是一个数组， (最多16个元素，) 与所有类型的元素一起使用 `object` 。</span><span class="sxs-lookup"><span data-stu-id="11093-268">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="11093-269">仅在提供静态选项卡解决方案的解决方案中，此块是必需的。</span><span class="sxs-lookup"><span data-stu-id="11093-269">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="11093-270">名称</span><span class="sxs-lookup"><span data-stu-id="11093-270">Name</span></span>| <span data-ttu-id="11093-271">类型</span><span class="sxs-lookup"><span data-stu-id="11093-271">Type</span></span>| <span data-ttu-id="11093-272">最大大小</span><span class="sxs-lookup"><span data-stu-id="11093-272">Maximum size</span></span> | <span data-ttu-id="11093-273">必需</span><span class="sxs-lookup"><span data-stu-id="11093-273">Required</span></span> | <span data-ttu-id="11093-274">说明</span><span class="sxs-lookup"><span data-stu-id="11093-274">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="11093-275">string</span><span class="sxs-lookup"><span data-stu-id="11093-275">string</span></span>|<span data-ttu-id="11093-276">64 个字符</span><span class="sxs-lookup"><span data-stu-id="11093-276">64 characters</span></span>|<span data-ttu-id="11093-277">✔</span><span class="sxs-lookup"><span data-stu-id="11093-277">✔</span></span>|<span data-ttu-id="11093-278">选项卡显示的实体的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="11093-278">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="11093-279">string</span><span class="sxs-lookup"><span data-stu-id="11093-279">string</span></span>|<span data-ttu-id="11093-280">128个字符</span><span class="sxs-lookup"><span data-stu-id="11093-280">128 characters</span></span>|<span data-ttu-id="11093-281">✔</span><span class="sxs-lookup"><span data-stu-id="11093-281">✔</span></span>|<span data-ttu-id="11093-282">该选项卡在通道接口中的显示名称。</span><span class="sxs-lookup"><span data-stu-id="11093-282">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="11093-283">string</span><span class="sxs-lookup"><span data-stu-id="11093-283">string</span></span>||<span data-ttu-id="11093-284">✔</span><span class="sxs-lookup"><span data-stu-id="11093-284">✔</span></span>|<span data-ttu-id="11093-285">指向要在团队画布中显示的实体 UI 的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="11093-285">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="11093-286">string</span><span class="sxs-lookup"><span data-stu-id="11093-286">string</span></span>|||<span data-ttu-id="11093-287">如果用户要在浏览器中查看，则为指向的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="11093-287">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="11093-288">string</span><span class="sxs-lookup"><span data-stu-id="11093-288">string</span></span>|||<span data-ttu-id="11093-289">指向用户搜索查询的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="11093-289">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="11093-290">枚举数组</span><span class="sxs-lookup"><span data-stu-id="11093-290">array of enums</span></span>|<span data-ttu-id="11093-291">1</span><span class="sxs-lookup"><span data-stu-id="11093-291">1</span></span>|<span data-ttu-id="11093-292">✔</span><span class="sxs-lookup"><span data-stu-id="11093-292">✔</span></span>|<span data-ttu-id="11093-293">目前，静态选项卡仅支持 `personal` 作用域，这意味着它只能作为个人体验的一部分进行预配。</span><span class="sxs-lookup"><span data-stu-id="11093-293">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="11093-294">枚举数组</span><span class="sxs-lookup"><span data-stu-id="11093-294">array of enums</span></span>| <span data-ttu-id="11093-295">双面</span><span class="sxs-lookup"><span data-stu-id="11093-295">2</span></span>|| <span data-ttu-id="11093-296">`contextItem`支持选项卡的作用域集。</span><span class="sxs-lookup"><span data-stu-id="11093-296">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
> <span data-ttu-id="11093-297">如果您的选项卡需要上下文相关信息来显示相关内容或启动身份验证流，*请参阅*[获取 Microsoft 团队的上下文选项卡](../../tabs/how-to/access-teams-context.md)。</span><span class="sxs-lookup"><span data-stu-id="11093-297">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="11093-298">bot</span><span class="sxs-lookup"><span data-stu-id="11093-298">bots</span></span>

<span data-ttu-id="11093-299">**Optional** — array</span><span class="sxs-lookup"><span data-stu-id="11093-299">**Optional** — array</span></span>

<span data-ttu-id="11093-300">定义机器人解决方案以及可选信息，如默认的命令属性。</span><span class="sxs-lookup"><span data-stu-id="11093-300">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="11093-301">Item 是数组 (每个元素最多只能包含1个元素， &mdash; 每个应用程序) 只允许一个 bot 与所有类型的元素一起使用 `object` 。</span><span class="sxs-lookup"><span data-stu-id="11093-301">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="11093-302">仅在提供机器人体验的解决方案中，此块才是必需的。</span><span class="sxs-lookup"><span data-stu-id="11093-302">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="11093-303">名称</span><span class="sxs-lookup"><span data-stu-id="11093-303">Name</span></span>| <span data-ttu-id="11093-304">类型</span><span class="sxs-lookup"><span data-stu-id="11093-304">Type</span></span>| <span data-ttu-id="11093-305">最大大小</span><span class="sxs-lookup"><span data-stu-id="11093-305">Maximum size</span></span> | <span data-ttu-id="11093-306">必需</span><span class="sxs-lookup"><span data-stu-id="11093-306">Required</span></span> | <span data-ttu-id="11093-307">说明</span><span class="sxs-lookup"><span data-stu-id="11093-307">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="11093-308">string</span><span class="sxs-lookup"><span data-stu-id="11093-308">string</span></span>|<span data-ttu-id="11093-309">64 个字符</span><span class="sxs-lookup"><span data-stu-id="11093-309">64 characters</span></span>|<span data-ttu-id="11093-310">✔</span><span class="sxs-lookup"><span data-stu-id="11093-310">✔</span></span>|<span data-ttu-id="11093-311">使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="11093-311">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="11093-312">这可能与整体 [应用程序 ID](#id)很好。</span><span class="sxs-lookup"><span data-stu-id="11093-312">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="11093-313">枚举数组</span><span class="sxs-lookup"><span data-stu-id="11093-313">array of enums</span></span>|<span data-ttu-id="11093-314">第三章</span><span class="sxs-lookup"><span data-stu-id="11093-314">3</span></span>|<span data-ttu-id="11093-315">✔</span><span class="sxs-lookup"><span data-stu-id="11093-315">✔</span></span>|<span data-ttu-id="11093-316">指定自动程序是在 `team` 内的频道上下文中提供体验、在群组聊天 (`groupchat`) 中提供体验，还是仅在单个用户 (`personal`) 范围内提供体验。</span><span class="sxs-lookup"><span data-stu-id="11093-316">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="11093-317">这些选项不具排他性。</span><span class="sxs-lookup"><span data-stu-id="11093-317">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="11093-318">boolean</span><span class="sxs-lookup"><span data-stu-id="11093-318">boolean</span></span>|||<span data-ttu-id="11093-319">描述自动程序是否利用用户提示将自动程序添加到特定频道。</span><span class="sxs-lookup"><span data-stu-id="11093-319">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="11093-320">设置 **`false`**</span><span class="sxs-lookup"><span data-stu-id="11093-320">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="11093-321">boolean</span><span class="sxs-lookup"><span data-stu-id="11093-321">boolean</span></span>|||<span data-ttu-id="11093-322">指示自动程序是否为单向、仅通知的自动程序，而不是对话自动程序。</span><span class="sxs-lookup"><span data-stu-id="11093-322">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="11093-323">设置 `**false**`</span><span class="sxs-lookup"><span data-stu-id="11093-323">Default: `**false**`</span></span>|
|`supportsFiles`|<span data-ttu-id="11093-324">boolean</span><span class="sxs-lookup"><span data-stu-id="11093-324">boolean</span></span>|||<span data-ttu-id="11093-325">指示自动程序是否支持在个人聊天中上传/下载文件。</span><span class="sxs-lookup"><span data-stu-id="11093-325">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="11093-326">设置 **`false`**</span><span class="sxs-lookup"><span data-stu-id="11093-326">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="11093-327">boolean</span><span class="sxs-lookup"><span data-stu-id="11093-327">boolean</span></span>|||<span data-ttu-id="11093-328">一个值，指示机器人支持音频呼叫的位置。</span><span class="sxs-lookup"><span data-stu-id="11093-328">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="11093-329">**重要说明**：此属性当前为实验性。</span><span class="sxs-lookup"><span data-stu-id="11093-329">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="11093-330">实验性属性可能不完整，并且可能会在完全可用之前进行更改。</span><span class="sxs-lookup"><span data-stu-id="11093-330">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="11093-331">它仅用于测试和研究目的，不应在生产应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="11093-331">It is provided for testing and exploration purposes only and should not be used in production applications.</span></span> <span data-ttu-id="11093-332">设置 **`false`**</span><span class="sxs-lookup"><span data-stu-id="11093-332">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="11093-333">boolean</span><span class="sxs-lookup"><span data-stu-id="11093-333">boolean</span></span>|||<span data-ttu-id="11093-334">一个值，指示机器人支持视频通话的位置。</span><span class="sxs-lookup"><span data-stu-id="11093-334">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="11093-335">**重要说明**：此属性当前为实验性。</span><span class="sxs-lookup"><span data-stu-id="11093-335">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="11093-336">实验性属性可能不完整，并且可能会在完全可用之前进行更改。</span><span class="sxs-lookup"><span data-stu-id="11093-336">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="11093-337">它仅用于测试和研究目的，不应在生产应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="11093-337">It is provided for testing and exploration purposes only and should not be used in production applications.</span></span> <span data-ttu-id="11093-338">设置 **`false`**</span><span class="sxs-lookup"><span data-stu-id="11093-338">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="11093-339">commandLists</span><span class="sxs-lookup"><span data-stu-id="11093-339">bots.commandLists</span></span>

<span data-ttu-id="11093-340">你的 bot 可以向用户推荐的命令的可选列表。</span><span class="sxs-lookup"><span data-stu-id="11093-340">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="11093-341">对象是数组 (最多为2个元素) 的所有类型的元素 `object` ; 您必须为你的 bot 支持的每个作用域定义单独的命令列表。</span><span class="sxs-lookup"><span data-stu-id="11093-341">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="11093-342">有关详细信息，请参阅 [Bot 菜单](~/bots/how-to/create-a-bot-commands-menu.md) 。</span><span class="sxs-lookup"><span data-stu-id="11093-342">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="11093-343">名称</span><span class="sxs-lookup"><span data-stu-id="11093-343">Name</span></span>| <span data-ttu-id="11093-344">类型</span><span class="sxs-lookup"><span data-stu-id="11093-344">Type</span></span>| <span data-ttu-id="11093-345">最大大小</span><span class="sxs-lookup"><span data-stu-id="11093-345">Maximum size</span></span> | <span data-ttu-id="11093-346">必需</span><span class="sxs-lookup"><span data-stu-id="11093-346">Required</span></span> | <span data-ttu-id="11093-347">说明</span><span class="sxs-lookup"><span data-stu-id="11093-347">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="11093-348">枚举数组</span><span class="sxs-lookup"><span data-stu-id="11093-348">array of enums</span></span>|<span data-ttu-id="11093-349">第三章</span><span class="sxs-lookup"><span data-stu-id="11093-349">3</span></span>|<span data-ttu-id="11093-350">✔</span><span class="sxs-lookup"><span data-stu-id="11093-350">✔</span></span>|<span data-ttu-id="11093-351">指定命令列表有效的作用域。</span><span class="sxs-lookup"><span data-stu-id="11093-351">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="11093-352">选项包括 `team`、`personal` 和 `groupchat`。</span><span class="sxs-lookup"><span data-stu-id="11093-352">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="11093-353">对象数组</span><span class="sxs-lookup"><span data-stu-id="11093-353">array of objects</span></span>|<span data-ttu-id="11093-354">10  </span><span class="sxs-lookup"><span data-stu-id="11093-354">10</span></span>|<span data-ttu-id="11093-355">✔</span><span class="sxs-lookup"><span data-stu-id="11093-355">✔</span></span>|<span data-ttu-id="11093-356">自动程序支持的命令数组：</span><span class="sxs-lookup"><span data-stu-id="11093-356">An array of commands the bot supports:</span></span><br><span data-ttu-id="11093-357">`title`：自动程序命令名称（字符串，32）</span><span class="sxs-lookup"><span data-stu-id="11093-357">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="11093-358">`description`：命令语法及其参数的简单描述或示例（字符串，128）</span><span class="sxs-lookup"><span data-stu-id="11093-358">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="11093-359">commandLists</span><span class="sxs-lookup"><span data-stu-id="11093-359">bots.commandLists.commands</span></span>

|<span data-ttu-id="11093-360">名称</span><span class="sxs-lookup"><span data-stu-id="11093-360">Name</span></span>| <span data-ttu-id="11093-361">类型</span><span class="sxs-lookup"><span data-stu-id="11093-361">Type</span></span>| <span data-ttu-id="11093-362">最大大小</span><span class="sxs-lookup"><span data-stu-id="11093-362">Maximum size</span></span> | <span data-ttu-id="11093-363">必需</span><span class="sxs-lookup"><span data-stu-id="11093-363">Required</span></span> | <span data-ttu-id="11093-364">说明</span><span class="sxs-lookup"><span data-stu-id="11093-364">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="11093-365">title</span><span class="sxs-lookup"><span data-stu-id="11093-365">title</span></span>|<span data-ttu-id="11093-366">string</span><span class="sxs-lookup"><span data-stu-id="11093-366">string</span></span>|<span data-ttu-id="11093-367">12 </span><span class="sxs-lookup"><span data-stu-id="11093-367">12</span></span>|<span data-ttu-id="11093-368">✔</span><span class="sxs-lookup"><span data-stu-id="11093-368">✔</span></span>|<span data-ttu-id="11093-369">Bot 命令名称</span><span class="sxs-lookup"><span data-stu-id="11093-369">The bot command name</span></span>|
|<span data-ttu-id="11093-370">说明</span><span class="sxs-lookup"><span data-stu-id="11093-370">description</span></span>|<span data-ttu-id="11093-371">string</span><span class="sxs-lookup"><span data-stu-id="11093-371">string</span></span>|<span data-ttu-id="11093-372">128个字符</span><span class="sxs-lookup"><span data-stu-id="11093-372">128 characters</span></span>|<span data-ttu-id="11093-373">✔</span><span class="sxs-lookup"><span data-stu-id="11093-373">✔</span></span>|<span data-ttu-id="11093-374">一个简单的文本说明或一个命令语法及其参数的示例。</span><span class="sxs-lookup"><span data-stu-id="11093-374">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="11093-375">插槽</span><span class="sxs-lookup"><span data-stu-id="11093-375">connectors</span></span>

<span data-ttu-id="11093-376">**Optional** — array</span><span class="sxs-lookup"><span data-stu-id="11093-376">**Optional** — array</span></span>

<span data-ttu-id="11093-377">`connectors`Block 定义了应用程序的 Office 365 连接器。</span><span class="sxs-lookup"><span data-stu-id="11093-377">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="11093-378">对象是数组 (最大值为1的元素) 与所有类型的元素一起使用 `object` 。</span><span class="sxs-lookup"><span data-stu-id="11093-378">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="11093-379">仅对提供连接器的解决方案而言，此块是必需的。</span><span class="sxs-lookup"><span data-stu-id="11093-379">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="11093-380">名称</span><span class="sxs-lookup"><span data-stu-id="11093-380">Name</span></span>| <span data-ttu-id="11093-381">类型</span><span class="sxs-lookup"><span data-stu-id="11093-381">Type</span></span>| <span data-ttu-id="11093-382">最大大小</span><span class="sxs-lookup"><span data-stu-id="11093-382">Maximum size</span></span> | <span data-ttu-id="11093-383">必需</span><span class="sxs-lookup"><span data-stu-id="11093-383">Required</span></span> | <span data-ttu-id="11093-384">说明</span><span class="sxs-lookup"><span data-stu-id="11093-384">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="11093-385">string</span><span class="sxs-lookup"><span data-stu-id="11093-385">string</span></span>|<span data-ttu-id="11093-386">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="11093-386">2048 characters</span></span>|<span data-ttu-id="11093-387">✔</span><span class="sxs-lookup"><span data-stu-id="11093-387">✔</span></span>|<span data-ttu-id="11093-388">配置连接器时要使用的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="11093-388">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="11093-389">枚举数组</span><span class="sxs-lookup"><span data-stu-id="11093-389">array of enums</span></span>|<span data-ttu-id="11093-390">1</span><span class="sxs-lookup"><span data-stu-id="11093-390">1</span></span>|<span data-ttu-id="11093-391">✔</span><span class="sxs-lookup"><span data-stu-id="11093-391">✔</span></span>|<span data-ttu-id="11093-392">指定连接器是在中频道的上下文中 `team` ，还是在仅限于单个用户 () 的体验中提供体验 `personal` 。</span><span class="sxs-lookup"><span data-stu-id="11093-392">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="11093-393">目前，仅 `team` 支持作用域。</span><span class="sxs-lookup"><span data-stu-id="11093-393">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="11093-394">string</span><span class="sxs-lookup"><span data-stu-id="11093-394">string</span></span>|<span data-ttu-id="11093-395">64 个字符</span><span class="sxs-lookup"><span data-stu-id="11093-395">64 characters</span></span>|<span data-ttu-id="11093-396">✔</span><span class="sxs-lookup"><span data-stu-id="11093-396">✔</span></span>|<span data-ttu-id="11093-397">与 [连接器开发人员仪表板](https://aka.ms/connectorsdashboard)中的 ID 相匹配的连接器的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="11093-397">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="11093-398">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="11093-398">composeExtensions</span></span>

<span data-ttu-id="11093-399">**Optional** — array</span><span class="sxs-lookup"><span data-stu-id="11093-399">**Optional** — array</span></span>

<span data-ttu-id="11093-400">定义应用程序的消息扩展。</span><span class="sxs-lookup"><span data-stu-id="11093-400">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="11093-401">功能的名称已从11月2017的 "撰写分机" 更改为 "消息扩展"，但清单名称保持不变，以便现有扩展能够继续正常工作。</span><span class="sxs-lookup"><span data-stu-id="11093-401">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="11093-402">Item 是一个数组， (最多1个元素) 与所有类型的元素一起使用 `object` 。</span><span class="sxs-lookup"><span data-stu-id="11093-402">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="11093-403">仅对提供邮件扩展的解决方案而言，此块是必需的。</span><span class="sxs-lookup"><span data-stu-id="11093-403">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="11093-404">名称</span><span class="sxs-lookup"><span data-stu-id="11093-404">Name</span></span>| <span data-ttu-id="11093-405">类型</span><span class="sxs-lookup"><span data-stu-id="11093-405">Type</span></span> | <span data-ttu-id="11093-406">最大大小</span><span class="sxs-lookup"><span data-stu-id="11093-406">Maximum Size</span></span> | <span data-ttu-id="11093-407">必需</span><span class="sxs-lookup"><span data-stu-id="11093-407">Required</span></span> | <span data-ttu-id="11093-408">说明</span><span class="sxs-lookup"><span data-stu-id="11093-408">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="11093-409">string</span><span class="sxs-lookup"><span data-stu-id="11093-409">string</span></span>|<span data-ttu-id="11093-410">64</span><span class="sxs-lookup"><span data-stu-id="11093-410">64</span></span>|<span data-ttu-id="11093-411">✔</span><span class="sxs-lookup"><span data-stu-id="11093-411">✔</span></span>|<span data-ttu-id="11093-412">与 Bot 框架一起注册的支持邮件扩展的 bot 的唯一 Microsoft 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="11093-412">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="11093-413">这可能与整体应用程序 ID 很好。</span><span class="sxs-lookup"><span data-stu-id="11093-413">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="11093-414">对象数组</span><span class="sxs-lookup"><span data-stu-id="11093-414">array of objects</span></span>|<span data-ttu-id="11093-415">10  </span><span class="sxs-lookup"><span data-stu-id="11093-415">10</span></span>|<span data-ttu-id="11093-416">✔</span><span class="sxs-lookup"><span data-stu-id="11093-416">✔</span></span>|<span data-ttu-id="11093-417">邮件扩展支持的命令数组</span><span class="sxs-lookup"><span data-stu-id="11093-417">array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="11093-418">boolean</span><span class="sxs-lookup"><span data-stu-id="11093-418">boolean</span></span>|||<span data-ttu-id="11093-419">一个值，指示用户是否可以更新邮件扩展的配置。</span><span class="sxs-lookup"><span data-stu-id="11093-419">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="11093-420">默认值：**False**。</span><span class="sxs-lookup"><span data-stu-id="11093-420">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="11093-421">对象数组</span><span class="sxs-lookup"><span data-stu-id="11093-421">array of Objects</span></span>|<span data-ttu-id="11093-422">5 </span><span class="sxs-lookup"><span data-stu-id="11093-422">5</span></span>||<span data-ttu-id="11093-423">允许在满足特定条件时调用应用程序的处理程序列表。</span><span class="sxs-lookup"><span data-stu-id="11093-423">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="11093-424">域也必须列在 `validDomains`</span><span class="sxs-lookup"><span data-stu-id="11093-424">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="11093-425">string</span><span class="sxs-lookup"><span data-stu-id="11093-425">string</span></span>|||<span data-ttu-id="11093-426">消息处理程序的类型。</span><span class="sxs-lookup"><span data-stu-id="11093-426">The type of message handler.</span></span> <span data-ttu-id="11093-427">必须是 `"link"`。</span><span class="sxs-lookup"><span data-stu-id="11093-427">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="11093-428">字符串数组</span><span class="sxs-lookup"><span data-stu-id="11093-428">array of Strings</span></span>|||<span data-ttu-id="11093-429">链接消息处理程序可以为其注册的域的数组。</span><span class="sxs-lookup"><span data-stu-id="11093-429">array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="11093-430">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="11093-430">composeExtensions.commands</span></span>

<span data-ttu-id="11093-431">您的邮件扩展应声明一个或多个命令。</span><span class="sxs-lookup"><span data-stu-id="11093-431">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="11093-432">在 Microsoft 团队中，每个命令都显示为从基于 UI 的入口点的潜在交互。</span><span class="sxs-lookup"><span data-stu-id="11093-432">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="11093-433">最多可以有10个命令。</span><span class="sxs-lookup"><span data-stu-id="11093-433">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="11093-434">每个命令项都是一个具有以下结构的对象：</span><span class="sxs-lookup"><span data-stu-id="11093-434">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="11093-435">名称</span><span class="sxs-lookup"><span data-stu-id="11093-435">Name</span></span>| <span data-ttu-id="11093-436">类型</span><span class="sxs-lookup"><span data-stu-id="11093-436">Type</span></span>| <span data-ttu-id="11093-437">最大大小</span><span class="sxs-lookup"><span data-stu-id="11093-437">Maximum size</span></span> | <span data-ttu-id="11093-438">必需</span><span class="sxs-lookup"><span data-stu-id="11093-438">Required</span></span> | <span data-ttu-id="11093-439">说明</span><span class="sxs-lookup"><span data-stu-id="11093-439">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="11093-440">string</span><span class="sxs-lookup"><span data-stu-id="11093-440">string</span></span>|<span data-ttu-id="11093-441">64 个字符</span><span class="sxs-lookup"><span data-stu-id="11093-441">64 characters</span></span>|<span data-ttu-id="11093-442">✔</span><span class="sxs-lookup"><span data-stu-id="11093-442">✔</span></span>|<span data-ttu-id="11093-443">命令的 ID。</span><span class="sxs-lookup"><span data-stu-id="11093-443">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="11093-444">string</span><span class="sxs-lookup"><span data-stu-id="11093-444">string</span></span>|<span data-ttu-id="11093-445">32个字符</span><span class="sxs-lookup"><span data-stu-id="11093-445">32 characters</span></span>|<span data-ttu-id="11093-446">✔</span><span class="sxs-lookup"><span data-stu-id="11093-446">✔</span></span>|<span data-ttu-id="11093-447">用户友好的命令名称。</span><span class="sxs-lookup"><span data-stu-id="11093-447">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="11093-448">string</span><span class="sxs-lookup"><span data-stu-id="11093-448">string</span></span>|<span data-ttu-id="11093-449">64 个字符</span><span class="sxs-lookup"><span data-stu-id="11093-449">64 characters</span></span>||<span data-ttu-id="11093-450">命令的类型。</span><span class="sxs-lookup"><span data-stu-id="11093-450">Type of the command.</span></span> <span data-ttu-id="11093-451">一个 `query` 或 `action` 。</span><span class="sxs-lookup"><span data-stu-id="11093-451">One of `query` or `action`.</span></span> <span data-ttu-id="11093-452">默认值： **query**。</span><span class="sxs-lookup"><span data-stu-id="11093-452">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="11093-453">string</span><span class="sxs-lookup"><span data-stu-id="11093-453">string</span></span>|<span data-ttu-id="11093-454">128个字符</span><span class="sxs-lookup"><span data-stu-id="11093-454">128 characters</span></span>||<span data-ttu-id="11093-455">对用户显示的说明，用于指示此命令的用途。</span><span class="sxs-lookup"><span data-stu-id="11093-455">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="11093-456">boolean</span><span class="sxs-lookup"><span data-stu-id="11093-456">boolean</span></span>|||<span data-ttu-id="11093-457">一个布尔值，指示是否在最初不使用任何参数的情况之下运行该命令。</span><span class="sxs-lookup"><span data-stu-id="11093-457">A boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="11093-458">默认值：**False**。</span><span class="sxs-lookup"><span data-stu-id="11093-458">Default: **false**.</span></span>|
|`context`|<span data-ttu-id="11093-459">字符串数组</span><span class="sxs-lookup"><span data-stu-id="11093-459">array of Strings</span></span>|<span data-ttu-id="11093-460">第三章</span><span class="sxs-lookup"><span data-stu-id="11093-460">3</span></span>||<span data-ttu-id="11093-461">定义可以从中调用邮件扩展的位置。</span><span class="sxs-lookup"><span data-stu-id="11093-461">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="11093-462">、、的的任意组合 `compose` `commandBox` `message` 。</span><span class="sxs-lookup"><span data-stu-id="11093-462">Any combination of`compose`,`commandBox`,`message` .</span></span> <span data-ttu-id="11093-463">默认值为 `["compose","commandBox"]`。</span><span class="sxs-lookup"><span data-stu-id="11093-463">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="11093-464">boolean</span><span class="sxs-lookup"><span data-stu-id="11093-464">boolean</span></span>|||<span data-ttu-id="11093-465">一个布尔值，指示是否应动态获取任务模块。</span><span class="sxs-lookup"><span data-stu-id="11093-465">A boolean value that indicates if it should fetch the task module dynamically.</span></span> <span data-ttu-id="11093-466">默认值：**False**。</span><span class="sxs-lookup"><span data-stu-id="11093-466">Default: **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="11093-467">object</span><span class="sxs-lookup"><span data-stu-id="11093-467">object</span></span>|||<span data-ttu-id="11093-468">使用消息扩展命令指定要预加载的任务模块。</span><span class="sxs-lookup"><span data-stu-id="11093-468">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="11093-469">string</span><span class="sxs-lookup"><span data-stu-id="11093-469">string</span></span>|<span data-ttu-id="11093-470">64 个字符</span><span class="sxs-lookup"><span data-stu-id="11093-470">64 characters</span></span>||<span data-ttu-id="11093-471">初始对话框标题。</span><span class="sxs-lookup"><span data-stu-id="11093-471">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="11093-472">string</span><span class="sxs-lookup"><span data-stu-id="11093-472">string</span></span>|||<span data-ttu-id="11093-473">对话框宽度-以像素为单位的数字或默认布局，如 "大"、"中" 或 "small"。</span><span class="sxs-lookup"><span data-stu-id="11093-473">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="11093-474">string</span><span class="sxs-lookup"><span data-stu-id="11093-474">string</span></span>|||<span data-ttu-id="11093-475">对话框高度-以像素为单位的数字或默认布局，如 "大"、"中" 或 "small"。</span><span class="sxs-lookup"><span data-stu-id="11093-475">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="11093-476">string</span><span class="sxs-lookup"><span data-stu-id="11093-476">string</span></span>|||<span data-ttu-id="11093-477">初始的 web 视图 URL。</span><span class="sxs-lookup"><span data-stu-id="11093-477">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="11093-478">对象数组</span><span class="sxs-lookup"><span data-stu-id="11093-478">array of object</span></span>|<span data-ttu-id="11093-479">5项</span><span class="sxs-lookup"><span data-stu-id="11093-479">5 items</span></span>|<span data-ttu-id="11093-480">✔</span><span class="sxs-lookup"><span data-stu-id="11093-480">✔</span></span>|<span data-ttu-id="11093-481">命令所采用的参数的列表。</span><span class="sxs-lookup"><span data-stu-id="11093-481">The list of parameters the command takes.</span></span> <span data-ttu-id="11093-482">最小值： 1;最大值：5。</span><span class="sxs-lookup"><span data-stu-id="11093-482">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="11093-483">string</span><span class="sxs-lookup"><span data-stu-id="11093-483">string</span></span>|<span data-ttu-id="11093-484">64 个字符</span><span class="sxs-lookup"><span data-stu-id="11093-484">64 characters</span></span>|<span data-ttu-id="11093-485">✔</span><span class="sxs-lookup"><span data-stu-id="11093-485">✔</span></span>|<span data-ttu-id="11093-486">在客户端中显示的参数的名称。</span><span class="sxs-lookup"><span data-stu-id="11093-486">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="11093-487">此项包含在用户请求中。</span><span class="sxs-lookup"><span data-stu-id="11093-487">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="11093-488">string</span><span class="sxs-lookup"><span data-stu-id="11093-488">string</span></span>|<span data-ttu-id="11093-489">32个字符</span><span class="sxs-lookup"><span data-stu-id="11093-489">32 characters</span></span>|<span data-ttu-id="11093-490">✔</span><span class="sxs-lookup"><span data-stu-id="11093-490">✔</span></span>|<span data-ttu-id="11093-491">参数的用户友好标题。</span><span class="sxs-lookup"><span data-stu-id="11093-491">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="11093-492">string</span><span class="sxs-lookup"><span data-stu-id="11093-492">string</span></span>|<span data-ttu-id="11093-493">128个字符</span><span class="sxs-lookup"><span data-stu-id="11093-493">128 characters</span></span>||<span data-ttu-id="11093-494">描述此参数用途的用户友好字符串。</span><span class="sxs-lookup"><span data-stu-id="11093-494">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="11093-495">string</span><span class="sxs-lookup"><span data-stu-id="11093-495">string</span></span>|<span data-ttu-id="11093-496">512个字符</span><span class="sxs-lookup"><span data-stu-id="11093-496">512 characters</span></span>||<span data-ttu-id="11093-497">参数的初始值。</span><span class="sxs-lookup"><span data-stu-id="11093-497">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="11093-498">string</span><span class="sxs-lookup"><span data-stu-id="11093-498">string</span></span>|<span data-ttu-id="11093-499">128个字符</span><span class="sxs-lookup"><span data-stu-id="11093-499">128 characters</span></span>||<span data-ttu-id="11093-500">定义在的任务模块上显示的控件的类型 `fetchTask: true` 。</span><span class="sxs-lookup"><span data-stu-id="11093-500">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="11093-501">其中一个 `text, textarea, number, date, time, toggle, choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="11093-501">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="11093-502">对象数组</span><span class="sxs-lookup"><span data-stu-id="11093-502">array of objects</span></span>|<span data-ttu-id="11093-503">10项</span><span class="sxs-lookup"><span data-stu-id="11093-503">10 items</span></span>||<span data-ttu-id="11093-504">的选项选项 `choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="11093-504">The choice options for the`choiceset`.</span></span> <span data-ttu-id="11093-505">仅在时 `parameter.inputType` 使用 `choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="11093-505">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="11093-506">string</span><span class="sxs-lookup"><span data-stu-id="11093-506">string</span></span>|<span data-ttu-id="11093-507">128个字符</span><span class="sxs-lookup"><span data-stu-id="11093-507">128 characters</span></span>|<span data-ttu-id="11093-508">✔</span><span class="sxs-lookup"><span data-stu-id="11093-508">✔</span></span>|<span data-ttu-id="11093-509">选项的标题。</span><span class="sxs-lookup"><span data-stu-id="11093-509">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="11093-510">string</span><span class="sxs-lookup"><span data-stu-id="11093-510">string</span></span>|<span data-ttu-id="11093-511">512个字符</span><span class="sxs-lookup"><span data-stu-id="11093-511">512 characters</span></span>|<span data-ttu-id="11093-512">✔</span><span class="sxs-lookup"><span data-stu-id="11093-512">✔</span></span>|<span data-ttu-id="11093-513">选项的值。</span><span class="sxs-lookup"><span data-stu-id="11093-513">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="11093-514">permissions</span><span class="sxs-lookup"><span data-stu-id="11093-514">permissions</span></span>

<span data-ttu-id="11093-515">**Optional** -字符串数组</span><span class="sxs-lookup"><span data-stu-id="11093-515">**Optional** — array of strings</span></span>

<span data-ttu-id="11093-516">一个数组 `string` ，它指定应用程序请求的权限，这样最终用户就可以知道扩展将如何执行。</span><span class="sxs-lookup"><span data-stu-id="11093-516">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="11093-517">以下选项是非独占的：</span><span class="sxs-lookup"><span data-stu-id="11093-517">The following options are non-exclusive:</span></span>

* <span data-ttu-id="11093-518">`identity`&emsp;需要用户标识信息</span><span class="sxs-lookup"><span data-stu-id="11093-518">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="11093-519">`messageTeamMembers`&emsp;需要向团队成员发送直接消息的权限</span><span class="sxs-lookup"><span data-stu-id="11093-519">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="11093-520">在更新应用程序时更改这些权限将导致用户在首次运行更新的应用程序时重复同意过程。</span><span class="sxs-lookup"><span data-stu-id="11093-520">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="11093-521">有关详细信息，请参阅 [更新应用](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) 。</span><span class="sxs-lookup"><span data-stu-id="11093-521">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="11093-522">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="11093-522">devicePermissions</span></span>

<span data-ttu-id="11093-523">**Optional** -字符串数组</span><span class="sxs-lookup"><span data-stu-id="11093-523">**Optional** — array of strings</span></span>

<span data-ttu-id="11093-524">在用户的设备上指定您的应用程序可能会请求访问的本机功能。</span><span class="sxs-lookup"><span data-stu-id="11093-524">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="11093-525">选项包括：</span><span class="sxs-lookup"><span data-stu-id="11093-525">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="11093-526">validDomains</span><span class="sxs-lookup"><span data-stu-id="11093-526">validDomains</span></span>

<span data-ttu-id="11093-527">**可选**，但 **所需** 的除外</span><span class="sxs-lookup"><span data-stu-id="11093-527">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="11093-528">应用程序希望在团队客户端中加载的网站的有效域列表。</span><span class="sxs-lookup"><span data-stu-id="11093-528">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="11093-529">例如，域列表可以包含通配符 `*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="11093-529">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="11093-530">这与域的一段完全匹配;如果需要匹配， `a.b.example.com` 请使用 `*.*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="11093-530">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="11093-531">如果您的选项卡配置或内容 UI 需要导航到其他任何域，除了用于选项卡配置之外，则必须在此处指定该域。</span><span class="sxs-lookup"><span data-stu-id="11093-531">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="11093-532">但是， **不** 需要在您的应用程序中包含要支持的标识提供程序的域。</span><span class="sxs-lookup"><span data-stu-id="11093-532">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="11093-533">例如，若要使用 Google ID 进行身份验证，需要重定向到 accounts.google.com，但不应在中包含 accounts.google.com `validDomains[]` 。</span><span class="sxs-lookup"><span data-stu-id="11093-533">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="11093-534">需要其自己的 sharepoint Url 的团队应用程序能够正常工作，可能会在其有效的域列表中包含 "{teamsitedomain}"。</span><span class="sxs-lookup"><span data-stu-id="11093-534">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11093-535">不要直接或通过通配符添加位于控件外部的域。</span><span class="sxs-lookup"><span data-stu-id="11093-535">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="11093-536">例如， `yourapp.onmicrosoft.com` 是有效的，但 `*.onmicrosoft.com` 无效。</span><span class="sxs-lookup"><span data-stu-id="11093-536">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="11093-537">对象是一个包含所有类型的元素的数组 `string` 。</span><span class="sxs-lookup"><span data-stu-id="11093-537">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="11093-538">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="11093-538">webApplicationInfo</span></span>

<span data-ttu-id="11093-539">**Optional** —对象</span><span class="sxs-lookup"><span data-stu-id="11093-539">**Optional** — object</span></span>

<span data-ttu-id="11093-540"> (Azure AD) 应用 ID 和 Microsoft Graph 信息指定 Azure Active Directory，以帮助用户无缝登录你的应用。</span><span class="sxs-lookup"><span data-stu-id="11093-540">Specify your Azure Active Directory (Azure AD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="11093-541">如果您的应用程序是在 Azure AD 中注册的，则必须提供应用 ID，以便管理员可以轻松查看权限并在团队管理中心中授予许可。</span><span class="sxs-lookup"><span data-stu-id="11093-541">If your app is registered in Azure AD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="11093-542">名称</span><span class="sxs-lookup"><span data-stu-id="11093-542">Name</span></span>| <span data-ttu-id="11093-543">类型</span><span class="sxs-lookup"><span data-stu-id="11093-543">Type</span></span>| <span data-ttu-id="11093-544">最大大小</span><span class="sxs-lookup"><span data-stu-id="11093-544">Maximum size</span></span> | <span data-ttu-id="11093-545">必需</span><span class="sxs-lookup"><span data-stu-id="11093-545">Required</span></span> | <span data-ttu-id="11093-546">说明</span><span class="sxs-lookup"><span data-stu-id="11093-546">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="11093-547">string</span><span class="sxs-lookup"><span data-stu-id="11093-547">string</span></span>|<span data-ttu-id="11093-548">36个字符</span><span class="sxs-lookup"><span data-stu-id="11093-548">36 characters</span></span>|<span data-ttu-id="11093-549">✔</span><span class="sxs-lookup"><span data-stu-id="11093-549">✔</span></span>|<span data-ttu-id="11093-550">应用程序的 AAD 应用程序 id。</span><span class="sxs-lookup"><span data-stu-id="11093-550">AAD application id of the app.</span></span> <span data-ttu-id="11093-551">此 id 必须为 GUID。</span><span class="sxs-lookup"><span data-stu-id="11093-551">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="11093-552">string</span><span class="sxs-lookup"><span data-stu-id="11093-552">string</span></span>|<span data-ttu-id="11093-553">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="11093-553">2048 characters</span></span>|<span data-ttu-id="11093-554">✔</span><span class="sxs-lookup"><span data-stu-id="11093-554">✔</span></span>|<span data-ttu-id="11093-555">用于获取 SSO 的身份验证令牌的应用程序的资源 url。</span><span class="sxs-lookup"><span data-stu-id="11093-555">Resource url of app for acquiring auth token for SSO.</span></span>|
|`applicationPermissions`|<span data-ttu-id="11093-556">array of strings</span><span class="sxs-lookup"><span data-stu-id="11093-556">array of strings</span></span>|<span data-ttu-id="11093-557">128个字符</span><span class="sxs-lookup"><span data-stu-id="11093-557">128 characters</span></span>||<span data-ttu-id="11093-558">指定精确的 [资源特定许可](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="11093-558">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="11093-559">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="11093-559">showLoadingIndicator</span></span>

<span data-ttu-id="11093-560">**可选** -boolean</span><span class="sxs-lookup"><span data-stu-id="11093-560">**Optional** — boolean</span></span>

<span data-ttu-id="11093-561">指示在加载应用程序/选项卡时是否显示加载指示器。</span><span class="sxs-lookup"><span data-stu-id="11093-561">Indicate whether or not to show the loading indicator when an app/tab is loading.</span></span> <span data-ttu-id="11093-562">默认值：**False**。</span><span class="sxs-lookup"><span data-stu-id="11093-562">Default: **false**.</span></span>
>[!NOTE]
><span data-ttu-id="11093-563">如果您在应用程序清单中设置 "showLoadingIndicator： true"，然后要正确加载页面，则必须按照 [显示本机加载指示器](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) 文档中所述的协议修改选项卡和任务模块的内容页面。</span><span class="sxs-lookup"><span data-stu-id="11093-563">If you set "showLoadingIndicator : true" in your app manifest, then for the page to load correctly, you must modify the content pages of your tabs and task modules as per the protocol described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="11093-564">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="11093-564">isFullScreen</span></span>

 <span data-ttu-id="11093-565">**可选** -boolean</span><span class="sxs-lookup"><span data-stu-id="11093-565">**Optional** — boolean</span></span>

<span data-ttu-id="11093-566">使用或不使用 tab 头条指示个人应用程序的呈现位置。</span><span class="sxs-lookup"><span data-stu-id="11093-566">Indicate where a personal app is rendered with or without a tab-header bar.</span></span> <span data-ttu-id="11093-567">默认值：**False**。</span><span class="sxs-lookup"><span data-stu-id="11093-567">Default: **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="11093-568">activities</span><span class="sxs-lookup"><span data-stu-id="11093-568">activities</span></span>

<span data-ttu-id="11093-569">**Optional** —对象</span><span class="sxs-lookup"><span data-stu-id="11093-569">**Optional** — object</span></span>

<span data-ttu-id="11093-570">定义您的应用程序将用于发布到用户活动源的属性。</span><span class="sxs-lookup"><span data-stu-id="11093-570">Define the properties your app will use to post to a user activity feed.</span></span>

|<span data-ttu-id="11093-571">名称</span><span class="sxs-lookup"><span data-stu-id="11093-571">Name</span></span>| <span data-ttu-id="11093-572">类型</span><span class="sxs-lookup"><span data-stu-id="11093-572">Type</span></span>| <span data-ttu-id="11093-573">最大大小</span><span class="sxs-lookup"><span data-stu-id="11093-573">Maximum size</span></span> | <span data-ttu-id="11093-574">必需</span><span class="sxs-lookup"><span data-stu-id="11093-574">Required</span></span> | <span data-ttu-id="11093-575">说明</span><span class="sxs-lookup"><span data-stu-id="11093-575">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="11093-576">对象数组</span><span class="sxs-lookup"><span data-stu-id="11093-576">array of Objects</span></span>|<span data-ttu-id="11093-577">128项</span><span class="sxs-lookup"><span data-stu-id="11093-577">128 items</span></span>| | <span data-ttu-id="11093-578">指定您的应用程序可以发布到用户活动源的活动类型。</span><span class="sxs-lookup"><span data-stu-id="11093-578">Specify the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="11093-579">activityTypes</span><span class="sxs-lookup"><span data-stu-id="11093-579">activities.activityTypes</span></span>

|<span data-ttu-id="11093-580">名称</span><span class="sxs-lookup"><span data-stu-id="11093-580">Name</span></span>| <span data-ttu-id="11093-581">类型</span><span class="sxs-lookup"><span data-stu-id="11093-581">Type</span></span>| <span data-ttu-id="11093-582">最大大小</span><span class="sxs-lookup"><span data-stu-id="11093-582">Maximum size</span></span> | <span data-ttu-id="11093-583">必需</span><span class="sxs-lookup"><span data-stu-id="11093-583">Required</span></span> | <span data-ttu-id="11093-584">说明</span><span class="sxs-lookup"><span data-stu-id="11093-584">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="11093-585">string</span><span class="sxs-lookup"><span data-stu-id="11093-585">string</span></span>|<span data-ttu-id="11093-586">32个字符</span><span class="sxs-lookup"><span data-stu-id="11093-586">32 characters</span></span>|<span data-ttu-id="11093-587">✔</span><span class="sxs-lookup"><span data-stu-id="11093-587">✔</span></span>|<span data-ttu-id="11093-588">通知类型。</span><span class="sxs-lookup"><span data-stu-id="11093-588">The notification type.</span></span> <span data-ttu-id="11093-589">*请参阅下文*。</span><span class="sxs-lookup"><span data-stu-id="11093-589">*See below*.</span></span>|
|`description`|<span data-ttu-id="11093-590">string</span><span class="sxs-lookup"><span data-stu-id="11093-590">string</span></span>|<span data-ttu-id="11093-591">128个字符</span><span class="sxs-lookup"><span data-stu-id="11093-591">128 characters</span></span>|<span data-ttu-id="11093-592">✔</span><span class="sxs-lookup"><span data-stu-id="11093-592">✔</span></span>|<span data-ttu-id="11093-593">通知的简短说明。</span><span class="sxs-lookup"><span data-stu-id="11093-593">A brief description of the notification.</span></span> <span data-ttu-id="11093-594">*请参阅下文*。</span><span class="sxs-lookup"><span data-stu-id="11093-594">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="11093-595">string</span><span class="sxs-lookup"><span data-stu-id="11093-595">string</span></span>|<span data-ttu-id="11093-596">128个字符</span><span class="sxs-lookup"><span data-stu-id="11093-596">128 characters</span></span>|<span data-ttu-id="11093-597">✔</span><span class="sxs-lookup"><span data-stu-id="11093-597">✔</span></span>|<span data-ttu-id="11093-598">Ex： "{主角} 为您创建任务 {taskId}"</span><span class="sxs-lookup"><span data-stu-id="11093-598">Ex: "{actor} created task {taskId} for you"</span></span>|

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
