---
title: 清单架构参考
description: 介绍 Microsoft 团队清单支持的架构
keywords: 团队清单架构
author: laujan
ms.author: lajanuar
ms.openlocfilehash: b514bbe8e04e674f5aafb3dff3acfe08072d814f
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452734"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="3f7b8-104">参考： Microsoft 团队的清单架构</span><span class="sxs-lookup"><span data-stu-id="3f7b8-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="3f7b8-105">Microsoft 团队清单介绍了应用程序如何集成到 Microsoft 团队产品中。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="3f7b8-106">您的清单必须符合托管的架构 [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json) 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="3f7b8-107">早期版本 1.0-1.6 在 URL) 中使用 "v1" (也是支持的。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-107">Previous versions 1.0-1.6 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="3f7b8-108">以下架构示例显示了所有扩展性选项。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="3f7b8-109">完整清单示例</span><span class="sxs-lookup"><span data-stu-id="3f7b8-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
  "manifestVersion": "1.7",
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
      "sharePointPreviewImage": "Relative path to a tab preview image for use in SharePoint — 1024px X 768",
      "supportedSharePointHosts": "Define how your tab wil be made available in SharePoint (full page or web part)"
    }
  ],
  "staticTabs": [
    {
      "entityId": "unique Id for the page entity",
      "scopes": [
        "personal"
      ],
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content (displayed in Teams canvas)",
      "websiteUrl": "https://contoso.com/content (displayed in web browser"
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

<span data-ttu-id="3f7b8-110">架构定义了以下属性：</span><span class="sxs-lookup"><span data-stu-id="3f7b8-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="3f7b8-111">$schema</span><span class="sxs-lookup"><span data-stu-id="3f7b8-111">$schema</span></span>

<span data-ttu-id="3f7b8-112">*可选，但建议* —字符串</span><span class="sxs-lookup"><span data-stu-id="3f7b8-112">*Optional, but recommended* — string</span></span>

<span data-ttu-id="3f7b8-113">引用清单的 JSON 架构的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="3f7b8-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="3f7b8-114">manifestVersion</span></span>

<span data-ttu-id="3f7b8-115">**必需** -字符串</span><span class="sxs-lookup"><span data-stu-id="3f7b8-115">**Required** — string</span></span>

<span data-ttu-id="3f7b8-116">此清单使用的清单架构的版本。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="3f7b8-117">它应为 "1.7"。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-117">It should be "1.7".</span></span>

## <a name="version"></a><span data-ttu-id="3f7b8-118">version</span><span class="sxs-lookup"><span data-stu-id="3f7b8-118">version</span></span>

<span data-ttu-id="3f7b8-119">**必需** -字符串</span><span class="sxs-lookup"><span data-stu-id="3f7b8-119">**Required** — string</span></span>

<span data-ttu-id="3f7b8-120">特定应用程序的版本。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-120">The version of the specific app.</span></span> <span data-ttu-id="3f7b8-121">如果您更新清单中的某些内容，该版本还必须递增。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="3f7b8-122">这样一来，在安装新的清单时，它将覆盖现有的版本，用户将获得新的功能。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="3f7b8-123">如果此应用程序已提交到应用商店，则必须重新提交新清单，然后再对其进行重新验证。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="3f7b8-124">然后，此应用程序的用户将在几小时内自动获取新更新的清单（在批准后）。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="3f7b8-125">如果应用程序要求更改权限，则系统将提示用户升级并重新同意该应用。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="3f7b8-126">此版本字符串必须遵循 [semver](http://semver.org/) STANDARD (主要版本。网格.PATCH) 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="3f7b8-127">id</span><span class="sxs-lookup"><span data-stu-id="3f7b8-127">id</span></span>

<span data-ttu-id="3f7b8-128">**必需** — MICROSOFT app ID</span><span class="sxs-lookup"><span data-stu-id="3f7b8-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="3f7b8-129">Microsoft 为此应用程序生成的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="3f7b8-130">如果你已通过 Microsoft Bot 框架注册了 bot，或者你的选项卡的 web 应用已使用 Microsoft 登录，则你应该已经有 ID，应在此处输入它。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="3f7b8-131">否则，应在 Microsoft 应用程序注册门户 ([我的应用程序](https://apps.dev.microsoft.com) ") 上生成一个新的 ID，在此处输入它，然后在添加机器人时重用它。注意：如果您在 AppSource 中提交对现有应用程序的更新，您的清单中的 ID 不得修改。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="3f7b8-132">developer</span><span class="sxs-lookup"><span data-stu-id="3f7b8-132">developer</span></span>

<span data-ttu-id="3f7b8-133">**必需** -对象</span><span class="sxs-lookup"><span data-stu-id="3f7b8-133">**Required** — object</span></span>

<span data-ttu-id="3f7b8-134">指定有关贵公司的信息。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-134">Specifies information about your company.</span></span> <span data-ttu-id="3f7b8-135">对于提交到 AppSource 的应用程序 (以前的 Office 应用商店) ，这些值必须与您的 AppSource 条目中的信息相匹配。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-135">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="3f7b8-136">有关详细信息，请参阅我们的 [发布指南](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-136">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="3f7b8-137">名称</span><span class="sxs-lookup"><span data-stu-id="3f7b8-137">Name</span></span>| <span data-ttu-id="3f7b8-138">最大大小</span><span class="sxs-lookup"><span data-stu-id="3f7b8-138">Maximum size</span></span> | <span data-ttu-id="3f7b8-139">必需</span><span class="sxs-lookup"><span data-stu-id="3f7b8-139">Required</span></span> | <span data-ttu-id="3f7b8-140">说明</span><span class="sxs-lookup"><span data-stu-id="3f7b8-140">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="3f7b8-141">32个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-141">32 characters</span></span>|<span data-ttu-id="3f7b8-142">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-142">✔</span></span>|<span data-ttu-id="3f7b8-143">开发人员的显示名称。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-143">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="3f7b8-144">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-144">2048 characters</span></span>|<span data-ttu-id="3f7b8-145">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-145">✔</span></span>|<span data-ttu-id="3f7b8-146">开发人员网站的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-146">The https:// URL to the developer's website.</span></span> <span data-ttu-id="3f7b8-147">此链接应将用户带到您的公司或特定于产品的登陆页面。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-147">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="3f7b8-148">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-148">2048 characters</span></span>|<span data-ttu-id="3f7b8-149">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-149">✔</span></span>|<span data-ttu-id="3f7b8-150">开发人员的隐私策略的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-150">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="3f7b8-151">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-151">2048 characters</span></span>|<span data-ttu-id="3f7b8-152">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-152">✔</span></span>|<span data-ttu-id="3f7b8-153">开发人员使用条款的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-153">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="3f7b8-154">10个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-154">10 characters</span></span>| |<span data-ttu-id="3f7b8-155">**可选** 用于标识合作伙伴组织构建应用程序的 Microsoft 合作伙伴网络 ID。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-155">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="3f7b8-156">name</span><span class="sxs-lookup"><span data-stu-id="3f7b8-156">name</span></span>

<span data-ttu-id="3f7b8-157">**必需** -对象</span><span class="sxs-lookup"><span data-stu-id="3f7b8-157">**Required** — object</span></span>

<span data-ttu-id="3f7b8-158">在团队体验中向用户显示的应用程序体验的名称。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-158">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="3f7b8-159">对于提交到 AppSource 的应用程序，这些值必须与您的 AppSource 条目中的信息相匹配。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-159">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="3f7b8-160">和的值 `short` `full` 不应相同。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-160">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="3f7b8-161">名称</span><span class="sxs-lookup"><span data-stu-id="3f7b8-161">Name</span></span>| <span data-ttu-id="3f7b8-162">最大大小</span><span class="sxs-lookup"><span data-stu-id="3f7b8-162">Maximum size</span></span> | <span data-ttu-id="3f7b8-163">必需</span><span class="sxs-lookup"><span data-stu-id="3f7b8-163">Required</span></span> | <span data-ttu-id="3f7b8-164">说明</span><span class="sxs-lookup"><span data-stu-id="3f7b8-164">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="3f7b8-165">30 个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-165">30 characters</span></span>|<span data-ttu-id="3f7b8-166">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-166">✔</span></span>|<span data-ttu-id="3f7b8-167">应用程序的短显示名称。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-167">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="3f7b8-168">100 个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-168">100 characters</span></span>||<span data-ttu-id="3f7b8-169">应用程序的全名，如果完整的应用程序名称超过30个字符，则使用该名称。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-169">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="3f7b8-170">说明</span><span class="sxs-lookup"><span data-stu-id="3f7b8-170">description</span></span>

<span data-ttu-id="3f7b8-171">**必需** -对象</span><span class="sxs-lookup"><span data-stu-id="3f7b8-171">**Required** — object</span></span>

<span data-ttu-id="3f7b8-172">向用户介绍你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-172">Describes your app to users.</span></span> <span data-ttu-id="3f7b8-173">对于提交到 AppSource 的应用程序，这些值必须与您的 AppSource 条目中的信息相匹配。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-173">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="3f7b8-174">确保你的说明准确描述你的体验，并提供信息，以帮助潜在客户了解你的体验。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-174">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="3f7b8-175">如果需要使用外部帐户，还应在完整说明中说明。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-175">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="3f7b8-176">和的值 `short` `full` 不应相同。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-176">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="3f7b8-177">您的简短说明不得在详细说明中重复，并且不得包含任何其他应用程序名称。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-177">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="3f7b8-178">名称</span><span class="sxs-lookup"><span data-stu-id="3f7b8-178">Name</span></span>| <span data-ttu-id="3f7b8-179">最大大小</span><span class="sxs-lookup"><span data-stu-id="3f7b8-179">Maximum size</span></span> | <span data-ttu-id="3f7b8-180">必需</span><span class="sxs-lookup"><span data-stu-id="3f7b8-180">Required</span></span> | <span data-ttu-id="3f7b8-181">说明</span><span class="sxs-lookup"><span data-stu-id="3f7b8-181">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="3f7b8-182">80个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-182">80 characters</span></span>|<span data-ttu-id="3f7b8-183">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-183">✔</span></span>|<span data-ttu-id="3f7b8-184">在空间有限时使用的应用程序体验的简短说明。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-184">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="3f7b8-185">4000个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-185">4000 characters</span></span>|<span data-ttu-id="3f7b8-186">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-186">✔</span></span>|<span data-ttu-id="3f7b8-187">您的应用程序的完整说明。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-187">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="3f7b8-188">packageName</span><span class="sxs-lookup"><span data-stu-id="3f7b8-188">packageName</span></span>

<span data-ttu-id="3f7b8-189">**Optional** -string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-189">**Optional** — string</span></span>

<span data-ttu-id="3f7b8-190">此应用的以反向域表示法表示的唯一标识符;例如，.com. myapp。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-190">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="3f7b8-191">最大长度：64 个字符。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-191">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="3f7b8-192">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="3f7b8-192">localizationInfo</span></span>

<span data-ttu-id="3f7b8-193">**Optional** —对象</span><span class="sxs-lookup"><span data-stu-id="3f7b8-193">**Optional** — object</span></span>

<span data-ttu-id="3f7b8-194">允许指定默认语言，以及指向其他语言文件的指针。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-194">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="3f7b8-195">请参阅 [本地化](~/concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-195">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="3f7b8-196">名称</span><span class="sxs-lookup"><span data-stu-id="3f7b8-196">Name</span></span>| <span data-ttu-id="3f7b8-197">最大大小</span><span class="sxs-lookup"><span data-stu-id="3f7b8-197">Maximum size</span></span> | <span data-ttu-id="3f7b8-198">必需</span><span class="sxs-lookup"><span data-stu-id="3f7b8-198">Required</span></span> | <span data-ttu-id="3f7b8-199">说明</span><span class="sxs-lookup"><span data-stu-id="3f7b8-199">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="3f7b8-200">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-200">✔</span></span>|<span data-ttu-id="3f7b8-201">此顶级清单文件中的字符串的语言标记。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-201">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="3f7b8-202">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="3f7b8-202">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="3f7b8-203">指定其他语言翻译的对象的数组。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-203">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="3f7b8-204">名称</span><span class="sxs-lookup"><span data-stu-id="3f7b8-204">Name</span></span>| <span data-ttu-id="3f7b8-205">最大大小</span><span class="sxs-lookup"><span data-stu-id="3f7b8-205">Maximum size</span></span> | <span data-ttu-id="3f7b8-206">必需</span><span class="sxs-lookup"><span data-stu-id="3f7b8-206">Required</span></span> | <span data-ttu-id="3f7b8-207">说明</span><span class="sxs-lookup"><span data-stu-id="3f7b8-207">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="3f7b8-208">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-208">✔</span></span>|<span data-ttu-id="3f7b8-209">所提供文件中的字符串的语言标记。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-209">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="3f7b8-210">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-210">✔</span></span>|<span data-ttu-id="3f7b8-211">包含翻译字符串的 json 文件的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-211">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="3f7b8-212">图标</span><span class="sxs-lookup"><span data-stu-id="3f7b8-212">icons</span></span>

<span data-ttu-id="3f7b8-213">**必需** -对象</span><span class="sxs-lookup"><span data-stu-id="3f7b8-213">**Required** — object</span></span>

<span data-ttu-id="3f7b8-214">在团队应用程序中使用的图标。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-214">Icons used within the Teams app.</span></span> <span data-ttu-id="3f7b8-215">图标文件必须作为上载包的一部分包括在内。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-215">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="3f7b8-216">有关详细信息，请参阅 [图标](~/concepts/build-and-test/apps-package.md#icons) 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-216">See [Icons](~/concepts/build-and-test/apps-package.md#icons) for more information.</span></span>

|<span data-ttu-id="3f7b8-217">名称</span><span class="sxs-lookup"><span data-stu-id="3f7b8-217">Name</span></span>| <span data-ttu-id="3f7b8-218">最大大小</span><span class="sxs-lookup"><span data-stu-id="3f7b8-218">Maximum size</span></span> | <span data-ttu-id="3f7b8-219">必需</span><span class="sxs-lookup"><span data-stu-id="3f7b8-219">Required</span></span> | <span data-ttu-id="3f7b8-220">说明</span><span class="sxs-lookup"><span data-stu-id="3f7b8-220">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="3f7b8-221">32 x 32 像素</span><span class="sxs-lookup"><span data-stu-id="3f7b8-221">32 x 32 pixels</span></span>|<span data-ttu-id="3f7b8-222">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-222">✔</span></span>|<span data-ttu-id="3f7b8-223">指向透明 32x32 PNG 边框图标的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-223">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="3f7b8-224">192 x 192 像素</span><span class="sxs-lookup"><span data-stu-id="3f7b8-224">192 x 192 pixels</span></span>|<span data-ttu-id="3f7b8-225">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-225">✔</span></span>|<span data-ttu-id="3f7b8-226">完整颜色 192x192 PNG 图标的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-226">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="3f7b8-227">accentColor</span><span class="sxs-lookup"><span data-stu-id="3f7b8-227">accentColor</span></span>

<span data-ttu-id="3f7b8-228">**可选** — HTML 十六进制颜色代码</span><span class="sxs-lookup"><span data-stu-id="3f7b8-228">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="3f7b8-229">与大纲图标的背景一起使用的颜色。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-229">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="3f7b8-230">值必须是以 "#" 开头的有效 HTML 颜色代码，例如 `#4464ee` 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-230">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="3f7b8-231">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="3f7b8-231">configurableTabs</span></span>

<span data-ttu-id="3f7b8-232">**Optional** — array</span><span class="sxs-lookup"><span data-stu-id="3f7b8-232">**Optional** — array</span></span>

<span data-ttu-id="3f7b8-233">当您的应用程序体验具有在添加之前需要额外配置的团队频道选项卡体验时使用。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-233">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="3f7b8-234">只有在不是个人) 的团队 (范围中支持可配置的选项卡，并且每个应用程序目前仅支持 **一个** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-234">Configurable tabs are supported only in the teams scope (not personal), and currently only **one** tab per app is supported.</span></span>

|<span data-ttu-id="3f7b8-235">名称</span><span class="sxs-lookup"><span data-stu-id="3f7b8-235">Name</span></span>| <span data-ttu-id="3f7b8-236">类型</span><span class="sxs-lookup"><span data-stu-id="3f7b8-236">Type</span></span>| <span data-ttu-id="3f7b8-237">最大大小</span><span class="sxs-lookup"><span data-stu-id="3f7b8-237">Maximum size</span></span> | <span data-ttu-id="3f7b8-238">必需</span><span class="sxs-lookup"><span data-stu-id="3f7b8-238">Required</span></span> | <span data-ttu-id="3f7b8-239">说明</span><span class="sxs-lookup"><span data-stu-id="3f7b8-239">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="3f7b8-240">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-240">string</span></span>|<span data-ttu-id="3f7b8-241">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-241">2048 characters</span></span>|<span data-ttu-id="3f7b8-242">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-242">✔</span></span>|<span data-ttu-id="3f7b8-243">配置选项卡时要使用的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-243">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="3f7b8-244">枚举数组</span><span class="sxs-lookup"><span data-stu-id="3f7b8-244">array of enum</span></span>|<span data-ttu-id="3f7b8-245">1</span><span class="sxs-lookup"><span data-stu-id="3f7b8-245">1</span></span>|<span data-ttu-id="3f7b8-246">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-246">✔</span></span>|<span data-ttu-id="3f7b8-247">目前，可配置的选项卡仅支持 `team` 和 `groupchat` 范围。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-247">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="3f7b8-248">boolean</span><span class="sxs-lookup"><span data-stu-id="3f7b8-248">boolean</span></span>|||<span data-ttu-id="3f7b8-249">一个值，指示是否可在用户创建之后更新该选项卡的配置实例。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-249">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="3f7b8-250">默认值： **true**。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-250">Default: **true**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="3f7b8-251">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-251">string</span></span>|<span data-ttu-id="3f7b8-252">2048</span><span class="sxs-lookup"><span data-stu-id="3f7b8-252">2048</span></span>||<span data-ttu-id="3f7b8-253">要在 SharePoint 中使用的选项卡预览图像的相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-253">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="3f7b8-254">字号（1024x768）。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-254">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="3f7b8-255">枚举数组</span><span class="sxs-lookup"><span data-stu-id="3f7b8-255">array of enum</span></span>|<span data-ttu-id="3f7b8-256">1</span><span class="sxs-lookup"><span data-stu-id="3f7b8-256">1</span></span>||<span data-ttu-id="3f7b8-257">定义您的选项卡在 SharePoint 中的可用方式。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-257">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="3f7b8-258">选项包括 `sharePointFullPage` 和 `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="3f7b8-258">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="3f7b8-259">staticTabs</span><span class="sxs-lookup"><span data-stu-id="3f7b8-259">staticTabs</span></span>

<span data-ttu-id="3f7b8-260">**Optional** — array</span><span class="sxs-lookup"><span data-stu-id="3f7b8-260">**Optional** — array</span></span>

<span data-ttu-id="3f7b8-261">定义一组可在默认情况下 "固定" 的选项卡，而无需用户手动添加它们。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-261">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="3f7b8-262">在范围内声明的静态制表符 `personal` 始终固定到应用的个人体验中。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-262">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="3f7b8-263">当前不支持在范围中声明的静态选项卡 `team` 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-263">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="3f7b8-264">此项是一个数组， (最多16个元素，) 与所有类型的元素一起使用 `object` 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-264">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="3f7b8-265">仅在提供静态选项卡解决方案的解决方案中，此块是必需的。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-265">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="3f7b8-266">名称</span><span class="sxs-lookup"><span data-stu-id="3f7b8-266">Name</span></span>| <span data-ttu-id="3f7b8-267">类型</span><span class="sxs-lookup"><span data-stu-id="3f7b8-267">Type</span></span>| <span data-ttu-id="3f7b8-268">最大大小</span><span class="sxs-lookup"><span data-stu-id="3f7b8-268">Maximum size</span></span> | <span data-ttu-id="3f7b8-269">必需</span><span class="sxs-lookup"><span data-stu-id="3f7b8-269">Required</span></span> | <span data-ttu-id="3f7b8-270">说明</span><span class="sxs-lookup"><span data-stu-id="3f7b8-270">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="3f7b8-271">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-271">string</span></span>|<span data-ttu-id="3f7b8-272">64 个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-272">64 characters</span></span>|<span data-ttu-id="3f7b8-273">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-273">✔</span></span>|<span data-ttu-id="3f7b8-274">选项卡显示的实体的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-274">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="3f7b8-275">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-275">string</span></span>|<span data-ttu-id="3f7b8-276">128个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-276">128 characters</span></span>|<span data-ttu-id="3f7b8-277">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-277">✔</span></span>|<span data-ttu-id="3f7b8-278">该选项卡在通道接口中的显示名称。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-278">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="3f7b8-279">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-279">string</span></span>|<span data-ttu-id="3f7b8-280">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-280">2048 characters</span></span>|<span data-ttu-id="3f7b8-281">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-281">✔</span></span>|<span data-ttu-id="3f7b8-282">指向要在团队画布中显示的实体 UI 的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-282">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="3f7b8-283">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-283">string</span></span>|<span data-ttu-id="3f7b8-284">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-284">2048 characters</span></span>||<span data-ttu-id="3f7b8-285">要指向的 https://URL，如果用户要在浏览器中查看。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-285">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="3f7b8-286">枚举数组</span><span class="sxs-lookup"><span data-stu-id="3f7b8-286">array of enum</span></span>|<span data-ttu-id="3f7b8-287">1</span><span class="sxs-lookup"><span data-stu-id="3f7b8-287">1</span></span>|<span data-ttu-id="3f7b8-288">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-288">✔</span></span>|<span data-ttu-id="3f7b8-289">目前，静态选项卡仅支持 `personal` 作用域，这意味着它只能作为个人体验的一部分进行预配。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-289">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

> [!NOTE]
> <span data-ttu-id="3f7b8-290">如果您的选项卡需要上下文相关信息来显示相关内容或启动身份验证流，*请参阅*[获取 Microsoft 团队的上下文选项卡](../../tabs/how-to/access-teams-context.md)。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-290">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="3f7b8-291">bot</span><span class="sxs-lookup"><span data-stu-id="3f7b8-291">bots</span></span>

<span data-ttu-id="3f7b8-292">**Optional** — array</span><span class="sxs-lookup"><span data-stu-id="3f7b8-292">**Optional** — array</span></span>

<span data-ttu-id="3f7b8-293">定义机器人解决方案以及可选信息，如默认的命令属性。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-293">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="3f7b8-294">Item 是数组 (每个元素最多只能包含1个元素， &mdash; 每个应用程序) 只允许一个 bot 与所有类型的元素一起使用 `object` 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-294">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="3f7b8-295">仅在提供机器人体验的解决方案中，此块才是必需的。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-295">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="3f7b8-296">名称</span><span class="sxs-lookup"><span data-stu-id="3f7b8-296">Name</span></span>| <span data-ttu-id="3f7b8-297">类型</span><span class="sxs-lookup"><span data-stu-id="3f7b8-297">Type</span></span>| <span data-ttu-id="3f7b8-298">最大大小</span><span class="sxs-lookup"><span data-stu-id="3f7b8-298">Maximum size</span></span> | <span data-ttu-id="3f7b8-299">必需</span><span class="sxs-lookup"><span data-stu-id="3f7b8-299">Required</span></span> | <span data-ttu-id="3f7b8-300">说明</span><span class="sxs-lookup"><span data-stu-id="3f7b8-300">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="3f7b8-301">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-301">string</span></span>|<span data-ttu-id="3f7b8-302">64 个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-302">64 characters</span></span>|<span data-ttu-id="3f7b8-303">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-303">✔</span></span>|<span data-ttu-id="3f7b8-304">使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-304">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="3f7b8-305">这可能与整体 [应用程序 ID](#id)很好。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-305">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="3f7b8-306">枚举数组</span><span class="sxs-lookup"><span data-stu-id="3f7b8-306">array of enum</span></span>|<span data-ttu-id="3f7b8-307">第三章</span><span class="sxs-lookup"><span data-stu-id="3f7b8-307">3</span></span>|<span data-ttu-id="3f7b8-308">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-308">✔</span></span>|<span data-ttu-id="3f7b8-309">指定自动程序是在 `team` 内的频道上下文中提供体验、在群组聊天 (`groupchat`) 中提供体验，还是仅在单个用户 (`personal`) 范围内提供体验。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-309">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="3f7b8-310">这些选项不具排他性。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-310">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="3f7b8-311">boolean</span><span class="sxs-lookup"><span data-stu-id="3f7b8-311">boolean</span></span>|||<span data-ttu-id="3f7b8-312">描述自动程序是否利用用户提示将自动程序添加到特定频道。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-312">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="3f7b8-313">设置 **`false`**</span><span class="sxs-lookup"><span data-stu-id="3f7b8-313">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="3f7b8-314">boolean</span><span class="sxs-lookup"><span data-stu-id="3f7b8-314">boolean</span></span>|||<span data-ttu-id="3f7b8-315">指示自动程序是否为单向、仅通知的自动程序，而不是对话自动程序。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-315">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="3f7b8-316">设置 `**false**`</span><span class="sxs-lookup"><span data-stu-id="3f7b8-316">Default: `**false**`</span></span>|
|`supportsFiles`|<span data-ttu-id="3f7b8-317">boolean</span><span class="sxs-lookup"><span data-stu-id="3f7b8-317">boolean</span></span>|||<span data-ttu-id="3f7b8-318">指示自动程序是否支持在个人聊天中上传/下载文件。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-318">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="3f7b8-319">设置 **`false`**</span><span class="sxs-lookup"><span data-stu-id="3f7b8-319">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="3f7b8-320">commandLists</span><span class="sxs-lookup"><span data-stu-id="3f7b8-320">bots.commandLists</span></span>

<span data-ttu-id="3f7b8-321">你的 bot 可以向用户推荐的命令的可选列表。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-321">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="3f7b8-322">对象是数组 (最多为2个元素) 的所有类型的元素 `object` ; 您必须为你的 bot 支持的每个作用域定义单独的命令列表。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-322">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="3f7b8-323">有关详细信息，请参阅 [Bot 菜单](~/bots/how-to/create-a-bot-commands-menu.md) 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-323">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="3f7b8-324">名称</span><span class="sxs-lookup"><span data-stu-id="3f7b8-324">Name</span></span>| <span data-ttu-id="3f7b8-325">类型</span><span class="sxs-lookup"><span data-stu-id="3f7b8-325">Type</span></span>| <span data-ttu-id="3f7b8-326">最大大小</span><span class="sxs-lookup"><span data-stu-id="3f7b8-326">Maximum size</span></span> | <span data-ttu-id="3f7b8-327">必需</span><span class="sxs-lookup"><span data-stu-id="3f7b8-327">Required</span></span> | <span data-ttu-id="3f7b8-328">说明</span><span class="sxs-lookup"><span data-stu-id="3f7b8-328">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="3f7b8-329">枚举数组</span><span class="sxs-lookup"><span data-stu-id="3f7b8-329">array of enum</span></span>|<span data-ttu-id="3f7b8-330">第三章</span><span class="sxs-lookup"><span data-stu-id="3f7b8-330">3</span></span>|<span data-ttu-id="3f7b8-331">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-331">✔</span></span>|<span data-ttu-id="3f7b8-332">指定命令列表有效的作用域。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-332">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="3f7b8-333">选项包括 `team`、`personal` 和 `groupchat`。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-333">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="3f7b8-334">对象数组</span><span class="sxs-lookup"><span data-stu-id="3f7b8-334">array of objects</span></span>|<span data-ttu-id="3f7b8-335">10  </span><span class="sxs-lookup"><span data-stu-id="3f7b8-335">10</span></span>|<span data-ttu-id="3f7b8-336">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-336">✔</span></span>|<span data-ttu-id="3f7b8-337">自动程序支持的命令数组：</span><span class="sxs-lookup"><span data-stu-id="3f7b8-337">An array of commands the bot supports:</span></span><br><span data-ttu-id="3f7b8-338">`title`：自动程序命令名称（字符串，32）</span><span class="sxs-lookup"><span data-stu-id="3f7b8-338">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="3f7b8-339">`description`：命令语法及其参数的简单描述或示例（字符串，128）</span><span class="sxs-lookup"><span data-stu-id="3f7b8-339">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="3f7b8-340">commandLists</span><span class="sxs-lookup"><span data-stu-id="3f7b8-340">bots.commandLists.commands</span></span>

|<span data-ttu-id="3f7b8-341">名称</span><span class="sxs-lookup"><span data-stu-id="3f7b8-341">Name</span></span>| <span data-ttu-id="3f7b8-342">类型</span><span class="sxs-lookup"><span data-stu-id="3f7b8-342">Type</span></span>| <span data-ttu-id="3f7b8-343">最大大小</span><span class="sxs-lookup"><span data-stu-id="3f7b8-343">Maximum size</span></span> | <span data-ttu-id="3f7b8-344">必需</span><span class="sxs-lookup"><span data-stu-id="3f7b8-344">Required</span></span> | <span data-ttu-id="3f7b8-345">说明</span><span class="sxs-lookup"><span data-stu-id="3f7b8-345">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="3f7b8-346">title</span><span class="sxs-lookup"><span data-stu-id="3f7b8-346">title</span></span>|<span data-ttu-id="3f7b8-347">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-347">string</span></span>|<span data-ttu-id="3f7b8-348">12 </span><span class="sxs-lookup"><span data-stu-id="3f7b8-348">12</span></span>|<span data-ttu-id="3f7b8-349">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-349">✔</span></span>|<span data-ttu-id="3f7b8-350">Bot 命令名称</span><span class="sxs-lookup"><span data-stu-id="3f7b8-350">The bot command name</span></span>|
|<span data-ttu-id="3f7b8-351">说明</span><span class="sxs-lookup"><span data-stu-id="3f7b8-351">description</span></span>|<span data-ttu-id="3f7b8-352">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-352">string</span></span>|<span data-ttu-id="3f7b8-353">128个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-353">128 characters</span></span>|<span data-ttu-id="3f7b8-354">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-354">✔</span></span>|<span data-ttu-id="3f7b8-355">一个简单的文本说明或一个命令语法及其参数的示例。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-355">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="3f7b8-356">插槽</span><span class="sxs-lookup"><span data-stu-id="3f7b8-356">connectors</span></span>

<span data-ttu-id="3f7b8-357">**Optional** — array</span><span class="sxs-lookup"><span data-stu-id="3f7b8-357">**Optional** — array</span></span>

<span data-ttu-id="3f7b8-358">`connectors`Block 定义了应用程序的 Office 365 连接器。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-358">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="3f7b8-359">对象是数组 (最大值为1的元素) 与所有类型的元素一起使用 `object` 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-359">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="3f7b8-360">仅对提供连接器的解决方案而言，此块是必需的。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-360">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="3f7b8-361">名称</span><span class="sxs-lookup"><span data-stu-id="3f7b8-361">Name</span></span>| <span data-ttu-id="3f7b8-362">类型</span><span class="sxs-lookup"><span data-stu-id="3f7b8-362">Type</span></span>| <span data-ttu-id="3f7b8-363">最大大小</span><span class="sxs-lookup"><span data-stu-id="3f7b8-363">Maximum size</span></span> | <span data-ttu-id="3f7b8-364">必需</span><span class="sxs-lookup"><span data-stu-id="3f7b8-364">Required</span></span> | <span data-ttu-id="3f7b8-365">说明</span><span class="sxs-lookup"><span data-stu-id="3f7b8-365">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="3f7b8-366">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-366">string</span></span>|<span data-ttu-id="3f7b8-367">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-367">2048 characters</span></span>|<span data-ttu-id="3f7b8-368">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-368">✔</span></span>|<span data-ttu-id="3f7b8-369">配置连接器时要使用的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-369">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="3f7b8-370">枚举数组</span><span class="sxs-lookup"><span data-stu-id="3f7b8-370">array of enum</span></span>|<span data-ttu-id="3f7b8-371">1</span><span class="sxs-lookup"><span data-stu-id="3f7b8-371">1</span></span>|<span data-ttu-id="3f7b8-372">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-372">✔</span></span>|<span data-ttu-id="3f7b8-373">指定连接器是在中频道的上下文中 `team` ，还是在仅限于单个用户 () 的体验中提供体验 `personal` 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-373">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="3f7b8-374">目前，仅 `team` 支持作用域。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-374">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="3f7b8-375">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-375">string</span></span>|<span data-ttu-id="3f7b8-376">64 个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-376">64 characters</span></span>|<span data-ttu-id="3f7b8-377">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-377">✔</span></span>|<span data-ttu-id="3f7b8-378">与 [连接器开发人员仪表板](https://aka.ms/connectorsdashboard)中的 ID 相匹配的连接器的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-378">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="3f7b8-379">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="3f7b8-379">composeExtensions</span></span>

<span data-ttu-id="3f7b8-380">**Optional** — array</span><span class="sxs-lookup"><span data-stu-id="3f7b8-380">**Optional** — array</span></span>

<span data-ttu-id="3f7b8-381">定义应用程序的消息扩展。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-381">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="3f7b8-382">功能的名称已从11月2017的 "撰写分机" 更改为 "消息扩展"，但清单名称保持不变，以便现有扩展能够继续正常工作。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-382">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="3f7b8-383">Item 是一个数组， (最多1个元素) 与所有类型的元素一起使用 `object` 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-383">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="3f7b8-384">仅对提供邮件扩展的解决方案而言，此块是必需的。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-384">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="3f7b8-385">名称</span><span class="sxs-lookup"><span data-stu-id="3f7b8-385">Name</span></span>| <span data-ttu-id="3f7b8-386">类型</span><span class="sxs-lookup"><span data-stu-id="3f7b8-386">Type</span></span> | <span data-ttu-id="3f7b8-387">最大大小</span><span class="sxs-lookup"><span data-stu-id="3f7b8-387">Maximum Size</span></span> | <span data-ttu-id="3f7b8-388">必需</span><span class="sxs-lookup"><span data-stu-id="3f7b8-388">Required</span></span> | <span data-ttu-id="3f7b8-389">说明</span><span class="sxs-lookup"><span data-stu-id="3f7b8-389">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="3f7b8-390">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-390">string</span></span>|<span data-ttu-id="3f7b8-391">64</span><span class="sxs-lookup"><span data-stu-id="3f7b8-391">64</span></span>|<span data-ttu-id="3f7b8-392">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-392">✔</span></span>|<span data-ttu-id="3f7b8-393">与 Bot 框架一起注册的支持邮件扩展的 bot 的唯一 Microsoft 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-393">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="3f7b8-394">这可能与整体应用程序 ID 很好。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-394">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="3f7b8-395">对象数组</span><span class="sxs-lookup"><span data-stu-id="3f7b8-395">array of objects</span></span>|<span data-ttu-id="3f7b8-396">10  </span><span class="sxs-lookup"><span data-stu-id="3f7b8-396">10</span></span>|<span data-ttu-id="3f7b8-397">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-397">✔</span></span>|<span data-ttu-id="3f7b8-398">邮件扩展支持的命令数组</span><span class="sxs-lookup"><span data-stu-id="3f7b8-398">array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="3f7b8-399">boolean</span><span class="sxs-lookup"><span data-stu-id="3f7b8-399">boolean</span></span>|||<span data-ttu-id="3f7b8-400">一个值，指示用户是否可以更新邮件扩展的配置。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-400">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="3f7b8-401">默认值：**False**。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-401">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="3f7b8-402">对象数组</span><span class="sxs-lookup"><span data-stu-id="3f7b8-402">array of Objects</span></span>|<span data-ttu-id="3f7b8-403">5 </span><span class="sxs-lookup"><span data-stu-id="3f7b8-403">5</span></span>||<span data-ttu-id="3f7b8-404">允许在满足特定条件时调用应用程序的处理程序列表。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-404">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="3f7b8-405">域也必须列在 `validDomains`</span><span class="sxs-lookup"><span data-stu-id="3f7b8-405">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="3f7b8-406">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-406">string</span></span>|||<span data-ttu-id="3f7b8-407">消息处理程序的类型。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-407">The type of message handler.</span></span> <span data-ttu-id="3f7b8-408">必须是 `"link"`。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-408">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="3f7b8-409">字符串数组</span><span class="sxs-lookup"><span data-stu-id="3f7b8-409">array of Strings</span></span>|||<span data-ttu-id="3f7b8-410">链接消息处理程序可以为其注册的域的数组。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-410">array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="3f7b8-411">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="3f7b8-411">composeExtensions.commands</span></span>

<span data-ttu-id="3f7b8-412">您的邮件扩展应声明一个或多个命令。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-412">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="3f7b8-413">在 Microsoft 团队中，每个命令都显示为从基于 UI 的入口点的潜在交互。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-413">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="3f7b8-414">最多可以有10个命令。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-414">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="3f7b8-415">每个命令项都是一个具有以下结构的对象：</span><span class="sxs-lookup"><span data-stu-id="3f7b8-415">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="3f7b8-416">名称</span><span class="sxs-lookup"><span data-stu-id="3f7b8-416">Name</span></span>| <span data-ttu-id="3f7b8-417">类型</span><span class="sxs-lookup"><span data-stu-id="3f7b8-417">Type</span></span>| <span data-ttu-id="3f7b8-418">最大大小</span><span class="sxs-lookup"><span data-stu-id="3f7b8-418">Maximum size</span></span> | <span data-ttu-id="3f7b8-419">必需</span><span class="sxs-lookup"><span data-stu-id="3f7b8-419">Required</span></span> | <span data-ttu-id="3f7b8-420">说明</span><span class="sxs-lookup"><span data-stu-id="3f7b8-420">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="3f7b8-421">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-421">string</span></span>|<span data-ttu-id="3f7b8-422">64 个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-422">64 characters</span></span>|<span data-ttu-id="3f7b8-423">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-423">✔</span></span>|<span data-ttu-id="3f7b8-424">命令的 ID。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-424">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="3f7b8-425">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-425">string</span></span>|<span data-ttu-id="3f7b8-426">32个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-426">32 characters</span></span>|<span data-ttu-id="3f7b8-427">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-427">✔</span></span>|<span data-ttu-id="3f7b8-428">用户友好的命令名称。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-428">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="3f7b8-429">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-429">string</span></span>|<span data-ttu-id="3f7b8-430">64 个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-430">64 characters</span></span>||<span data-ttu-id="3f7b8-431">命令的类型。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-431">Type of the command.</span></span> <span data-ttu-id="3f7b8-432">一个 `query` 或 `action` 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-432">One of `query` or `action`.</span></span> <span data-ttu-id="3f7b8-433">默认值： **query**。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-433">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="3f7b8-434">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-434">string</span></span>|<span data-ttu-id="3f7b8-435">128个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-435">128 characters</span></span>||<span data-ttu-id="3f7b8-436">对用户显示的说明，用于指示此命令的用途。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-436">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="3f7b8-437">boolean</span><span class="sxs-lookup"><span data-stu-id="3f7b8-437">boolean</span></span>|||<span data-ttu-id="3f7b8-438">一个布尔值，指示是否在最初不使用任何参数的情况之下运行该命令。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-438">A boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="3f7b8-439">默认值：**False**。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-439">Default: **false**.</span></span>|
|`context`|<span data-ttu-id="3f7b8-440">字符串数组</span><span class="sxs-lookup"><span data-stu-id="3f7b8-440">array of Strings</span></span>|<span data-ttu-id="3f7b8-441">第三章</span><span class="sxs-lookup"><span data-stu-id="3f7b8-441">3</span></span>||<span data-ttu-id="3f7b8-442">定义可以从中调用邮件扩展的位置。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-442">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="3f7b8-443">、、的的任意组合 `compose` `commandBox` `message` 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-443">Any combination of`compose`,`commandBox`,`message` .</span></span> <span data-ttu-id="3f7b8-444">默认值为 `["compose","commandBox"]`。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-444">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="3f7b8-445">boolean</span><span class="sxs-lookup"><span data-stu-id="3f7b8-445">boolean</span></span>|||<span data-ttu-id="3f7b8-446">一个布尔值，指示是否应动态获取任务模块。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-446">A boolean value that indicates if it should fetch the task module dynamically.</span></span> <span data-ttu-id="3f7b8-447">默认值：**False**。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-447">Default: **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="3f7b8-448">object</span><span class="sxs-lookup"><span data-stu-id="3f7b8-448">object</span></span>|||<span data-ttu-id="3f7b8-449">使用消息扩展命令指定要预加载的任务模块。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-449">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="3f7b8-450">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-450">string</span></span>|<span data-ttu-id="3f7b8-451">64 个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-451">64 characters</span></span>||<span data-ttu-id="3f7b8-452">初始对话框标题。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-452">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="3f7b8-453">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-453">string</span></span>|||<span data-ttu-id="3f7b8-454">对话框宽度-以像素为单位的数字或默认布局，如 "大"、"中" 或 "small"。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-454">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="3f7b8-455">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-455">string</span></span>|||<span data-ttu-id="3f7b8-456">对话框高度-以像素为单位的数字或默认布局，如 "大"、"中" 或 "small"。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-456">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="3f7b8-457">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-457">string</span></span>|||<span data-ttu-id="3f7b8-458">初始的 web 视图 URL。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-458">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="3f7b8-459">对象数组</span><span class="sxs-lookup"><span data-stu-id="3f7b8-459">array of object</span></span>|<span data-ttu-id="3f7b8-460">5项</span><span class="sxs-lookup"><span data-stu-id="3f7b8-460">5 items</span></span>|<span data-ttu-id="3f7b8-461">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-461">✔</span></span>|<span data-ttu-id="3f7b8-462">命令所采用的参数的列表。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-462">The list of parameters the command takes.</span></span> <span data-ttu-id="3f7b8-463">最小值： 1;最大值：5。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-463">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="3f7b8-464">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-464">string</span></span>|<span data-ttu-id="3f7b8-465">64 个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-465">64 characters</span></span>|<span data-ttu-id="3f7b8-466">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-466">✔</span></span>|<span data-ttu-id="3f7b8-467">在客户端中显示的参数的名称。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-467">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="3f7b8-468">此项包含在用户请求中。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-468">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="3f7b8-469">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-469">string</span></span>|<span data-ttu-id="3f7b8-470">32个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-470">32 characters</span></span>|<span data-ttu-id="3f7b8-471">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-471">✔</span></span>|<span data-ttu-id="3f7b8-472">参数的用户友好标题。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-472">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="3f7b8-473">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-473">string</span></span>|<span data-ttu-id="3f7b8-474">128个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-474">128 characters</span></span>||<span data-ttu-id="3f7b8-475">描述此参数用途的用户友好字符串。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-475">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="3f7b8-476">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-476">string</span></span>|<span data-ttu-id="3f7b8-477">512个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-477">512 characters</span></span>||<span data-ttu-id="3f7b8-478">参数的初始值。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-478">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="3f7b8-479">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-479">string</span></span>|<span data-ttu-id="3f7b8-480">128个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-480">128 characters</span></span>||<span data-ttu-id="3f7b8-481">定义在的任务模块上显示的控件的类型 `fetchTask: true` 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-481">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="3f7b8-482">其中一个 `text, textarea, number, date, time, toggle, choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-482">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="3f7b8-483">对象数组</span><span class="sxs-lookup"><span data-stu-id="3f7b8-483">array of objects</span></span>|<span data-ttu-id="3f7b8-484">10项</span><span class="sxs-lookup"><span data-stu-id="3f7b8-484">10 items</span></span>||<span data-ttu-id="3f7b8-485">的选项选项 `choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-485">The choice options for the`choiceset`.</span></span> <span data-ttu-id="3f7b8-486">仅在时 `parameter.inputType` 使用 `choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-486">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="3f7b8-487">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-487">string</span></span>|<span data-ttu-id="3f7b8-488">128个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-488">128 characters</span></span>|<span data-ttu-id="3f7b8-489">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-489">✔</span></span>|<span data-ttu-id="3f7b8-490">选项的标题。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-490">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="3f7b8-491">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-491">string</span></span>|<span data-ttu-id="3f7b8-492">512个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-492">512 characters</span></span>|<span data-ttu-id="3f7b8-493">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-493">✔</span></span>|<span data-ttu-id="3f7b8-494">选项的值。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-494">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="3f7b8-495">permissions</span><span class="sxs-lookup"><span data-stu-id="3f7b8-495">permissions</span></span>

<span data-ttu-id="3f7b8-496">**Optional** -字符串数组</span><span class="sxs-lookup"><span data-stu-id="3f7b8-496">**Optional** — array of strings</span></span>

<span data-ttu-id="3f7b8-497">一个数组 `string` ，它指定应用程序请求的权限，这样最终用户就可以知道扩展将如何执行。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-497">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="3f7b8-498">以下选项是非独占的：</span><span class="sxs-lookup"><span data-stu-id="3f7b8-498">The following options are non-exclusive:</span></span>

* <span data-ttu-id="3f7b8-499">`identity`&emsp;需要用户标识信息</span><span class="sxs-lookup"><span data-stu-id="3f7b8-499">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="3f7b8-500">`messageTeamMembers`&emsp;需要向团队成员发送直接消息的权限</span><span class="sxs-lookup"><span data-stu-id="3f7b8-500">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="3f7b8-501">在更新应用程序时更改这些权限将导致用户在首次运行更新的应用程序时重复同意过程。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-501">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="3f7b8-502">有关详细信息，请参阅 [更新应用](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-502">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="3f7b8-503">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="3f7b8-503">devicePermissions</span></span>

<span data-ttu-id="3f7b8-504">**Optional** -字符串数组</span><span class="sxs-lookup"><span data-stu-id="3f7b8-504">**Optional** — array of strings</span></span>

<span data-ttu-id="3f7b8-505">在用户的设备上指定您的应用程序可能会请求访问的本机功能。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-505">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="3f7b8-506">选项包括：</span><span class="sxs-lookup"><span data-stu-id="3f7b8-506">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="3f7b8-507">validDomains</span><span class="sxs-lookup"><span data-stu-id="3f7b8-507">validDomains</span></span>

<span data-ttu-id="3f7b8-508">**可选**，但 **所需** 的除外</span><span class="sxs-lookup"><span data-stu-id="3f7b8-508">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="3f7b8-509">应用程序希望在团队客户端中加载的网站的有效域列表。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-509">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="3f7b8-510">例如，域列表可以包含通配符 `*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-510">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="3f7b8-511">这与域的一段完全匹配;如果需要匹配， `a.b.example.com` 请使用 `*.*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-511">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="3f7b8-512">如果您的选项卡配置或内容 UI 需要导航到其他任何域，除了用于选项卡配置之外，则必须在此处指定该域。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-512">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="3f7b8-513">但是， **不** 需要在您的应用程序中包含要支持的标识提供程序的域。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-513">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="3f7b8-514">例如，若要使用 Google ID 进行身份验证，需要重定向到 accounts.google.com，但不应在中包含 accounts.google.com `validDomains[]` 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-514">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="3f7b8-515">需要其自己的 sharepoint Url 的团队应用程序能够正常工作，可能会在其有效的域列表中包含 "{teamsitedomain}"。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-515">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3f7b8-516">不要直接或通过通配符添加位于控件外部的域。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-516">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="3f7b8-517">例如， `yourapp.onmicrosoft.com` 是有效的，但 `*.onmicrosoft.com` 无效。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-517">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="3f7b8-518">对象是一个包含所有类型的元素的数组 `string` 。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-518">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="3f7b8-519">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="3f7b8-519">webApplicationInfo</span></span>

<span data-ttu-id="3f7b8-520">**Optional** —对象</span><span class="sxs-lookup"><span data-stu-id="3f7b8-520">**Optional** — object</span></span>

<span data-ttu-id="3f7b8-521">指定 AAD 应用 ID 和 Graph 信息，以帮助用户无缝登录 AAD 应用。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-521">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="3f7b8-522">名称</span><span class="sxs-lookup"><span data-stu-id="3f7b8-522">Name</span></span>| <span data-ttu-id="3f7b8-523">类型</span><span class="sxs-lookup"><span data-stu-id="3f7b8-523">Type</span></span>| <span data-ttu-id="3f7b8-524">最大大小</span><span class="sxs-lookup"><span data-stu-id="3f7b8-524">Maximum size</span></span> | <span data-ttu-id="3f7b8-525">必需</span><span class="sxs-lookup"><span data-stu-id="3f7b8-525">Required</span></span> | <span data-ttu-id="3f7b8-526">说明</span><span class="sxs-lookup"><span data-stu-id="3f7b8-526">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="3f7b8-527">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-527">string</span></span>|<span data-ttu-id="3f7b8-528">36个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-528">36 characters</span></span>|<span data-ttu-id="3f7b8-529">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-529">✔</span></span>|<span data-ttu-id="3f7b8-530">应用程序的 AAD 应用程序 id。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-530">AAD application id of the app.</span></span> <span data-ttu-id="3f7b8-531">此 id 必须为 GUID。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-531">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="3f7b8-532">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-532">string</span></span>|<span data-ttu-id="3f7b8-533">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-533">2048 characters</span></span>||<span data-ttu-id="3f7b8-534">用于获取 SSO 的身份验证令牌的应用程序的资源 url。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-534">Resource url of app for acquiring auth token for SSO.</span></span>|
|`applicationPermissions`|<span data-ttu-id="3f7b8-535">array of strings</span><span class="sxs-lookup"><span data-stu-id="3f7b8-535">array of strings</span></span>|<span data-ttu-id="3f7b8-536">128个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-536">128 characters</span></span>||<span data-ttu-id="3f7b8-537">指定精确的 [资源特定许可](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="3f7b8-537">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="3f7b8-538">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="3f7b8-538">showLoadingIndicator</span></span>

<span data-ttu-id="3f7b8-539">**可选** -boolean</span><span class="sxs-lookup"><span data-stu-id="3f7b8-539">**Optional** — boolean</span></span>

<span data-ttu-id="3f7b8-540">指示在加载应用程序/选项卡时是否显示加载指示器。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-540">Indicate whether or not to show the loading indicator when an app/tab is loading.</span></span> <span data-ttu-id="3f7b8-541">默认值：**False**。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-541">Default: **false**.</span></span>
>[!NOTE]
><span data-ttu-id="3f7b8-542">如果您在应用程序清单中设置 "showLoadingIndicator： true"，然后要正确加载页面，则必须按照 [显示本机加载指示器](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) 文档中所述的协议修改选项卡和任务模块的内容页面。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-542">If you set "showLoadingIndicator : true" in your app manifest, then for the page to load correctly, you must modify the content pages of your tabs and task modules as per the protocol described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="3f7b8-543">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="3f7b8-543">isFullScreen</span></span>

 <span data-ttu-id="3f7b8-544">**可选** -boolean</span><span class="sxs-lookup"><span data-stu-id="3f7b8-544">**Optional** — boolean</span></span>

<span data-ttu-id="3f7b8-545">使用或不使用 tab 头条指示个人应用程序的呈现位置。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-545">Indicate where a personal app is rendered with or without a tab-header bar.</span></span> <span data-ttu-id="3f7b8-546">默认值：**False**。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-546">Default: **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="3f7b8-547">activities</span><span class="sxs-lookup"><span data-stu-id="3f7b8-547">activities</span></span>

<span data-ttu-id="3f7b8-548">**Optional** —对象</span><span class="sxs-lookup"><span data-stu-id="3f7b8-548">**Optional** — object</span></span>

<span data-ttu-id="3f7b8-549">定义您的应用程序将用于发布到用户活动源的属性。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-549">Define the properties your app will use to post to a user activity feed.</span></span>

|<span data-ttu-id="3f7b8-550">名称</span><span class="sxs-lookup"><span data-stu-id="3f7b8-550">Name</span></span>| <span data-ttu-id="3f7b8-551">类型</span><span class="sxs-lookup"><span data-stu-id="3f7b8-551">Type</span></span>| <span data-ttu-id="3f7b8-552">最大大小</span><span class="sxs-lookup"><span data-stu-id="3f7b8-552">Maximum size</span></span> | <span data-ttu-id="3f7b8-553">必需</span><span class="sxs-lookup"><span data-stu-id="3f7b8-553">Required</span></span> | <span data-ttu-id="3f7b8-554">说明</span><span class="sxs-lookup"><span data-stu-id="3f7b8-554">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="3f7b8-555">对象数组</span><span class="sxs-lookup"><span data-stu-id="3f7b8-555">array of Objects</span></span>|<span data-ttu-id="3f7b8-556">128项</span><span class="sxs-lookup"><span data-stu-id="3f7b8-556">128 items</span></span>| | <span data-ttu-id="3f7b8-557">指定您的应用程序可以发布到用户活动源的活动类型。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-557">Specify the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="3f7b8-558">activityTypes</span><span class="sxs-lookup"><span data-stu-id="3f7b8-558">activities.activityTypes</span></span>

|<span data-ttu-id="3f7b8-559">名称</span><span class="sxs-lookup"><span data-stu-id="3f7b8-559">Name</span></span>| <span data-ttu-id="3f7b8-560">类型</span><span class="sxs-lookup"><span data-stu-id="3f7b8-560">Type</span></span>| <span data-ttu-id="3f7b8-561">最大大小</span><span class="sxs-lookup"><span data-stu-id="3f7b8-561">Maximum size</span></span> | <span data-ttu-id="3f7b8-562">必需</span><span class="sxs-lookup"><span data-stu-id="3f7b8-562">Required</span></span> | <span data-ttu-id="3f7b8-563">说明</span><span class="sxs-lookup"><span data-stu-id="3f7b8-563">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="3f7b8-564">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-564">string</span></span>|<span data-ttu-id="3f7b8-565">32个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-565">32 characters</span></span>|<span data-ttu-id="3f7b8-566">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-566">✔</span></span>|<span data-ttu-id="3f7b8-567">通知类型。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-567">The notification type.</span></span> <span data-ttu-id="3f7b8-568">*请参阅下文*。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-568">*See below*.</span></span>|
|`description`|<span data-ttu-id="3f7b8-569">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-569">string</span></span>|<span data-ttu-id="3f7b8-570">128个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-570">128 characters</span></span>|<span data-ttu-id="3f7b8-571">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-571">✔</span></span>|<span data-ttu-id="3f7b8-572">通知的简短说明。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-572">A brief description of the notification.</span></span> <span data-ttu-id="3f7b8-573">*请参阅下文*。</span><span class="sxs-lookup"><span data-stu-id="3f7b8-573">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="3f7b8-574">string</span><span class="sxs-lookup"><span data-stu-id="3f7b8-574">string</span></span>|<span data-ttu-id="3f7b8-575">128个字符</span><span class="sxs-lookup"><span data-stu-id="3f7b8-575">128 characters</span></span>|<span data-ttu-id="3f7b8-576">✔</span><span class="sxs-lookup"><span data-stu-id="3f7b8-576">✔</span></span>|<span data-ttu-id="3f7b8-577">Ex： "{主角} 为您创建任务 {taskId}"</span><span class="sxs-lookup"><span data-stu-id="3f7b8-577">Ex: "{actor} created task {taskId} for you"</span></span>|

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
