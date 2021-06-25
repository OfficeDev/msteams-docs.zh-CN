---
title: 在应用程序内测试特定于资源的许可Teams
description: 使用 Postman 在 Teams中测试资源特定许可的详细信息
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: tutorial
keywords: teams 授权 OAuth SSO AAD rsc Postman Graph
ms.openlocfilehash: 8f5b293557ef7de9e4d551c5ae2bd7216e6e3fc0
ms.sourcegitcommit: 261058171f1e3bbc822c5bcc0e9fba5a4de68000
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/24/2021
ms.locfileid: "53111126"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a><span data-ttu-id="6d7c4-104">在应用程序内测试特定于资源的许可Teams</span><span class="sxs-lookup"><span data-stu-id="6d7c4-104">Test resource-specific consent permissions in Teams</span></span>

> [!NOTE]
> <span data-ttu-id="6d7c4-105">聊天范围的特定于资源的同意仅适用于 [公共开发人员预览](../../resources/dev-preview/developer-preview-intro.md) 版。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-105">Resource-specific consent for chat scope is available in [public developer preview](../../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="6d7c4-106">资源特定的同意 (RSC) 是一种 Microsoft Teams 和 Graph API 集成，使你的应用可以使用 API 终结点来管理组织中特定的资源（团队或聊天）。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-106">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific resources—either teams or chats—within an organization.</span></span> <span data-ttu-id="6d7c4-107">有关详细信息，请参阅[资源特定的同意 (RSC) — Microsoft Teams Graph API](resource-specific-consent.md)。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-107">For more information, see [Resource-specific consent (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6d7c4-108">若要测试 RSC 权限，Teams清单文件必须包含填充了以下字段的 **webApplicationInfo** 密钥：</span><span class="sxs-lookup"><span data-stu-id="6d7c4-108">To test the RSC permissions, your Teams app manifest file must include a **webApplicationInfo** key populated with the following fields:</span></span>
>
> - <span data-ttu-id="6d7c4-109">**id**：Azure AD 应用 ID，请参阅在 [Azure AD 门户中注册应用](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-aad-portal)。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-109">**id**: Your Azure AD app ID, see [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-aad-portal).</span></span>
> - <span data-ttu-id="6d7c4-110">**resource**：任何字符串，请参阅更新你的Teams [清单中的注释](resource-specific-consent.md#update-your-teams-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-110">**resource**: Any string, see the note in  [Update your Teams app manifest](resource-specific-consent.md#update-your-teams-app-manifest).</span></span>
> - <span data-ttu-id="6d7c4-111">**应用程序权限**：应用的 RSC 权限，请参阅 [特定于资源的权限](resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-111">**application permissions**: RSC permissions for  your app, see [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

## <a name="example-for-a-team"></a><span data-ttu-id="6d7c4-112">团队示例</span><span class="sxs-lookup"><span data-stu-id="6d7c4-112">Example for a team</span></span>
```json
"webApplicationInfo":{
      "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
      "resource":"https://AnyString",
      "applicationPermissions":[
         "Channel.Create.Group",
         "Channel.Delete.Group",
         "ChannelMessage.Read.Group",
         "ChannelSettings.Read.Group",
         "ChannelSettings.Edit.Group",
         "Member.Read.Group",
         "Owner.Read.Group",
         "TeamsApp.Read.Group",
         "TeamsTab.Read.Group",
         "TeamsTab.Create.Group",
         "TeamsTab.Edit.Group",
         "TeamsTab.Delete.Group",
         "TeamSettings.Read.Group",
         "TeamSettings.Edit.Group"
      ]
   }
```

## <a name="example-for-a-chat"></a><span data-ttu-id="6d7c4-113">聊天示例</span><span class="sxs-lookup"><span data-stu-id="6d7c4-113">Example for a chat</span></span>
```json
"webApplicationInfo":{
      "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
      "resource":"https://AnyString",
      "applicationPermissions":[
          "ChatSettings.Read.Chat",
          "ChatSettings.ReadWrite.Chat",
          "ChatMessage.Read.Chat",
          "ChatMember.Read.Chat",
          "Chat.Manage.Chat",
          "TeamsTab.Read.Chat",
          "TeamsTab.Create.Chat",
          "TeamsTab.Delete.Chat",
          "TeamsTab.ReadWrite.Chat",
          "TeamsAppInstallation.Read.Chat",
          "OnlineMeeting.ReadBasic.Chat"
      ]
   }
```

> [!IMPORTANT]
> <span data-ttu-id="6d7c4-114">在应用清单中，仅包含希望应用具有的 RSC 权限。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-114">In your app manifest, only include the RSC permissions that you want your app to have.</span></span>

>[!NOTE]
><span data-ttu-id="6d7c4-115">如果应用旨在支持在团队和聊天范围内安装，可以在 下的同一清单中指定团队和聊天权限 `applicationPermissions` 。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-115">If the app is meant to support installation in both team and chat scopes, then both team and chat permissions can be specified in the same manifest under `applicationPermissions`.</span></span>

## <a name="test-added-rsc-permissions-to-a-team-using-the-postman-app"></a><span data-ttu-id="6d7c4-116">使用 Postman 应用测试向团队添加的 RSC 权限</span><span class="sxs-lookup"><span data-stu-id="6d7c4-116">Test added RSC permissions to a team using the Postman app</span></span>

<span data-ttu-id="6d7c4-117">若要检查 API 请求有效负载是否接受 RSC 权限，需要将团队的 [RSC JSON](test-team-rsc-json-file.md) 测试代码复制到本地环境并更新以下值：</span><span class="sxs-lookup"><span data-stu-id="6d7c4-117">To check whether the RSC permissions are being honored by the API request payload, you need to copy the [RSC JSON test code for team](test-team-rsc-json-file.md) into your local environment and update the following values:</span></span>

* <span data-ttu-id="6d7c4-118">`azureADAppId`：应用的 Azure AD 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-118">`azureADAppId`: Your app's Azure AD app ID.</span></span>
* <span data-ttu-id="6d7c4-119">`azureADAppSecret`：你的 Azure AD 应用密码。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-119">`azureADAppSecret`: Your Azure AD app password.</span></span>
* <span data-ttu-id="6d7c4-120">`token_scope`：获取令牌需要 范围。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-120">`token_scope`: The scope is required to get a token.</span></span> <span data-ttu-id="6d7c4-121">将值设置为 https://graph.microsoft.com/.default 。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-121">set the value to https://graph.microsoft.com/.default.</span></span>
* <span data-ttu-id="6d7c4-122">`teamGroupId`：可以从客户端获取团队Teams ID，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6d7c4-122">`teamGroupId`: You can get the team group id from the Teams client as follows:</span></span>

    1. <span data-ttu-id="6d7c4-123">在 Teams 客户端 **中，Teams** 左侧导航栏中选择"导航"。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-123">In the Teams client, select **Teams** from the far left navigation bar.</span></span>
    2. <span data-ttu-id="6d7c4-124">从下拉菜单中选择安装应用的团队。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-124">Select the team where the app is installed from the dropdown menu.</span></span>
    3. <span data-ttu-id="6d7c4-125">选择" **更多选项"** 图标 (&#8943;) 。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-125">Select the **More options** icon (&#8943;).</span></span>
    4. <span data-ttu-id="6d7c4-126">选择 **获取团队链接**。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-126">Select **Get link to team**.</span></span> 
    5. <span data-ttu-id="6d7c4-127">复制并保存字符串中的 **groupId** 值。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-127">Copy and save the **groupId** value from the string.</span></span>

## <a name="test-added-rsc-permissions-to-a-chat-using-the-postman-app"></a><span data-ttu-id="6d7c4-128">使用 Postman 应用测试向聊天添加的 RSC 权限</span><span class="sxs-lookup"><span data-stu-id="6d7c4-128">Test added RSC permissions to a chat using the Postman app</span></span>

<span data-ttu-id="6d7c4-129">若要检查 API 请求有效负载是否接受 RSC 权限，需要将聊天的 [RSC JSON](test-chat-rsc-json-file.md) 测试代码复制到本地环境并更新以下值：</span><span class="sxs-lookup"><span data-stu-id="6d7c4-129">To check whether the RSC permissions are being honored by the API request payload, you need to copy the [RSC JSON test code for chats](test-chat-rsc-json-file.md) into your local environment and update the following values:</span></span>

* <span data-ttu-id="6d7c4-130">`azureADAppId`：应用的 Azure AD 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-130">`azureADAppId`: Your app's Azure AD app ID.</span></span>
* <span data-ttu-id="6d7c4-131">`azureADAppSecret`：你的 Azure AD 应用密码。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-131">`azureADAppSecret`: Your Azure AD app password.</span></span>
* <span data-ttu-id="6d7c4-132">`token_scope`：获取令牌需要 范围。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-132">`token_scope`: The scope is required to get a token.</span></span> <span data-ttu-id="6d7c4-133">将值设置为 https://graph.microsoft.com/.default 。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-133">set the value to https://graph.microsoft.com/.default.</span></span>
* <span data-ttu-id="6d7c4-134">`tenantId`：租户的名称或 AAD 对象 ID。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-134">`tenantId`: The name or the AAD Object ID of your tenant.</span></span>
* <span data-ttu-id="6d7c4-135">`chatId`：可以从 Web 客户端获取聊天Teams *ID，* 如下所示：</span><span class="sxs-lookup"><span data-stu-id="6d7c4-135">`chatId`: You can get the chat thread id from the Teams *web* client as follows:</span></span>

    1. <span data-ttu-id="6d7c4-136">在 Teams 客户端中 **，从最** 左侧导航栏中选择"聊天"。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-136">In the Teams web client, select **Chat** from the far left navigation bar.</span></span>
    2. <span data-ttu-id="6d7c4-137">从下拉菜单中选择应用安装位置的聊天。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-137">Select the chat where the app is installed from the dropdown menu.</span></span>
    3. <span data-ttu-id="6d7c4-138">复制 Web URL，然后从字符串中保存聊天线程 ID。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-138">Copy the web URL and save the chat thread id from the string.</span></span>
<span data-ttu-id="6d7c4-139">![来自 Web URL 的聊天线程 ID。](../../assets/images/chat-thread-id.png)</span><span class="sxs-lookup"><span data-stu-id="6d7c4-139">![Chat thread id from web URL.](../../assets/images/chat-thread-id.png)</span></span>

### <a name="use-postman"></a><span data-ttu-id="6d7c4-140">使用 Postman</span><span class="sxs-lookup"><span data-stu-id="6d7c4-140">Use Postman</span></span>

1. <span data-ttu-id="6d7c4-141">打开 [Postman](https://www.postman.com) 应用。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-141">Open the [Postman](https://www.postman.com) app.</span></span>
2. <span data-ttu-id="6d7c4-142">选择 **"**  >  **文件**  >  **导入导入文件**"，从环境中上载更新的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-142">Select **File** > **Import** > **Import file** to upload the updated JSON file from your environment.</span></span>  
3. <span data-ttu-id="6d7c4-143">选择" **集合"** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-143">Select the **Collections** tab.</span></span> 
4. <span data-ttu-id="6d7c4-144">选择"测试 **>** **RSC"** 旁边的 V 形以展开详细信息视图并查看 API 请求。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-144">Select the chevron **>** next to the **Test RSC** to expand the details view and see the API requests.</span></span>

<span data-ttu-id="6d7c4-145">针对每个 API 调用执行整个权限集合。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-145">Execute the entire permissions collection for each API call.</span></span> <span data-ttu-id="6d7c4-146">在应用程序清单中指定的权限必须成功，而未指定的权限必须使用 HTTP 403 状态代码失败。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-146">The permissions that you specified in your app manifest must succeed, while those not specified must fail with an HTTP 403 status code.</span></span> <span data-ttu-id="6d7c4-147">检查所有响应状态代码，确认应用中 RSC 权限的行为符合预期。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-147">Check all of the response status codes to confirm that the behavior of the RSC permissions in your app meet expectations.</span></span>

> [!NOTE]
> <span data-ttu-id="6d7c4-148">若要测试特定的 DELETE 和 READ API 调用，请向 JSON 文件添加这些实例方案。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-148">To test specific DELETE and READ API calls, add those instance scenarios to the JSON file.</span></span>

## <a name="test-revoked-rsc-permissions-using-postman"></a><span data-ttu-id="6d7c4-149">使用[Postman](https://www.postman.com/)测试吊销的 RSC 权限</span><span class="sxs-lookup"><span data-stu-id="6d7c4-149">Test revoked RSC permissions using [Postman](https://www.postman.com/)</span></span>

1. <span data-ttu-id="6d7c4-150">从特定资源卸载应用。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-150">Uninstall the app from the specific resource.</span></span>
2. <span data-ttu-id="6d7c4-151">按照聊天或团队的步骤操作：</span><span class="sxs-lookup"><span data-stu-id="6d7c4-151">Follow the steps for either chat or team:</span></span> 
    1. <span data-ttu-id="6d7c4-152">[使用 Postman 测试向团队添加了 RSC 权限](#test-added-rsc-permissions-to-a-team-using-the-postman-app)。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-152">[Test added RSC permissions to a team using Postman](#test-added-rsc-permissions-to-a-team-using-the-postman-app).</span></span>
    2. <span data-ttu-id="6d7c4-153">[使用 Postman 测试向聊天添加的 RSC 权限](#test-added-rsc-permissions-to-a-chat-using-the-postman-app)。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-153">[Test added RSC permissions to a chat using Postman](#test-added-rsc-permissions-to-a-chat-using-the-postman-app).</span></span>
3. <span data-ttu-id="6d7c4-154">检查所有响应状态代码，确认特定 API 调用失败，并 **包含 HTTP 403 状态代码**。</span><span class="sxs-lookup"><span data-stu-id="6d7c4-154">Check all the response status codes to confirm that the specific API calls **have failed with an HTTP 403 status code**.</span></span>

## <a name="see-also"></a><span data-ttu-id="6d7c4-155">另请参阅</span><span class="sxs-lookup"><span data-stu-id="6d7c4-155">See also</span></span>

[<span data-ttu-id="6d7c4-156">Microsoft Graph API 和 Teams</span><span class="sxs-lookup"><span data-stu-id="6d7c4-156">Microsoft Graph API and Teams</span></span>](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)

