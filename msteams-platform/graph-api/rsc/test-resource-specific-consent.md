---
title: 在 Teams 中测试特定于资源的同意权限
description: 使用 Postman 在 Teams 中测试特定于资源的同意的详细信息
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: tutorial
keywords: teams 授权 OAuth SSO AAD rsc Postman Graph
ms.openlocfilehash: 7f67df35954cd29810c387d05215eeec476a4ed4
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058325"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a><span data-ttu-id="a7128-104">在 Teams 中测试特定于资源的同意权限</span><span class="sxs-lookup"><span data-stu-id="a7128-104">Test resource-specific consent permissions in Teams</span></span>

<span data-ttu-id="a7128-105">RSC (特定于资源的) 是 Microsoft Teams 和 Graph API 集成，使你的应用可以使用 API 终结点来管理组织内的特定团队。</span><span class="sxs-lookup"><span data-stu-id="a7128-105">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="a7128-106">有关详细信息，请参阅 [RSC](resource-specific-consent.md) (特定) — Microsoft Teams Graph API。</span><span class="sxs-lookup"><span data-stu-id="a7128-106">For more information, see [Resource-specific consent (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a7128-107">若要测试 RSC 权限，Teams 应用清单文件必须包含填充了以下字段的 **webApplicationInfo** 密钥：</span><span class="sxs-lookup"><span data-stu-id="a7128-107">To test the RSC permissions, your Teams app manifest file must include a **webApplicationInfo** key populated with the following fields:</span></span>
>
> - <span data-ttu-id="a7128-108">**id**：Azure AD 应用 ID，请参阅在 [Azure AD 门户中注册应用](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="a7128-108">**id**: Your Azure AD app ID, see [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="a7128-109">**resource**：任何字符串，请参阅更新  [Teams 应用清单 中的注释](resource-specific-consent.md#update-your-teams-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="a7128-109">**resource**: Any string, see the note in  [Update your Teams app manifest](resource-specific-consent.md#update-your-teams-app-manifest).</span></span>
> - <span data-ttu-id="a7128-110">**应用程序权限**：应用的 RSC 权限，请参阅 [特定于资源的权限](resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="a7128-110">**application permissions**: RSC permissions for  your app, see [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

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

> [!IMPORTANT]
> <span data-ttu-id="a7128-111">在应用清单中，仅包含希望应用具有的 RSC 权限。</span><span class="sxs-lookup"><span data-stu-id="a7128-111">In your app manifest, only include the RSC permissions that you want your app to have.</span></span>

## <a name="test-added-rsc-permissions-using-the-postman-app"></a><span data-ttu-id="a7128-112">使用 Postman 应用测试添加的 RSC 权限</span><span class="sxs-lookup"><span data-stu-id="a7128-112">Test added RSC permissions using the Postman app</span></span>

<span data-ttu-id="a7128-113">若要检查 API 请求有效负载是否接受 RSC 权限，需要将 [RSC JSON](test-rsc-json-file.md) 测试代码复制到本地环境并更新以下值：</span><span class="sxs-lookup"><span data-stu-id="a7128-113">To check whether the RSC permissions are being honored by the API request payload, you need to copy the [RSC JSON test code](test-rsc-json-file.md) into your local environment and update the following values:</span></span>

* <span data-ttu-id="a7128-114">`azureADAppId`：应用的 Azure AD 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="a7128-114">`azureADAppId`: Your app's Azure AD app ID.</span></span>
* <span data-ttu-id="a7128-115">`azureADAppSecret`：你的 Azure AD 应用密码。</span><span class="sxs-lookup"><span data-stu-id="a7128-115">`azureADAppSecret`: Your Azure AD app password.</span></span>
* <span data-ttu-id="a7128-116">`token_scope`：获取令牌需要 范围。</span><span class="sxs-lookup"><span data-stu-id="a7128-116">`token_scope`: The scope is required to get a token.</span></span> <span data-ttu-id="a7128-117">将值设置为 https://graph.microsoft.com/.default 。</span><span class="sxs-lookup"><span data-stu-id="a7128-117">set the value to https://graph.microsoft.com/.default.</span></span>
* <span data-ttu-id="a7128-118">`teamGroupId`：可以从 Teams 客户端获取团队组 ID，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a7128-118">`teamGroupId`: You can get the team group id from the Teams client as follows:</span></span>

    1. <span data-ttu-id="a7128-119">在 Teams 客户端中，从 **最** 左侧导航栏中选择 Teams。</span><span class="sxs-lookup"><span data-stu-id="a7128-119">In the Teams client, select **Teams** from the far left navigation bar.</span></span>
    2. <span data-ttu-id="a7128-120">从下拉菜单中选择安装应用的团队。</span><span class="sxs-lookup"><span data-stu-id="a7128-120">Select the team where the app is installed from the dropdown menu.</span></span>
    3. <span data-ttu-id="a7128-121">选择" **更多选项"** 图标 (&#8943;) 。</span><span class="sxs-lookup"><span data-stu-id="a7128-121">Select the **More options** icon (&#8943;).</span></span>
    4. <span data-ttu-id="a7128-122">选择 **获取团队链接**。</span><span class="sxs-lookup"><span data-stu-id="a7128-122">Select **Get link to team**.</span></span> 
    5. <span data-ttu-id="a7128-123">复制并保存字符串中的 **groupId** 值。</span><span class="sxs-lookup"><span data-stu-id="a7128-123">Copy and save the **groupId** value from the string.</span></span>

### <a name="use-postman"></a><span data-ttu-id="a7128-124">使用 Postman</span><span class="sxs-lookup"><span data-stu-id="a7128-124">Use Postman</span></span>

1. <span data-ttu-id="a7128-125">打开 [Postman](https://www.postman.com) 应用。</span><span class="sxs-lookup"><span data-stu-id="a7128-125">Open the [Postman](https://www.postman.com) app.</span></span>
2. <span data-ttu-id="a7128-126">选择 **"**  >  **文件**  >  **导入导入文件**"，从环境中上载更新的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="a7128-126">Select **File** > **Import** > **Import file** to upload the updated JSON file from your environment.</span></span>  
3. <span data-ttu-id="a7128-127">选择" **集合"** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="a7128-127">Select the **Collections** tab.</span></span> 
4. <span data-ttu-id="a7128-128">选择"测试 **>** **RSC"** 旁边的 V 形以展开详细信息视图并查看 API 请求。</span><span class="sxs-lookup"><span data-stu-id="a7128-128">Select the chevron **>** next to the **Test RSC** to expand the details view and see the API requests.</span></span>

<span data-ttu-id="a7128-129">针对每个 API 调用执行整个权限集合。</span><span class="sxs-lookup"><span data-stu-id="a7128-129">Execute the entire permissions collection for each API call.</span></span> <span data-ttu-id="a7128-130">在应用程序清单中指定的权限必须成功，而未指定的权限必须使用 HTTP 403 状态代码失败。</span><span class="sxs-lookup"><span data-stu-id="a7128-130">The permissions that you specified in your app manifest must succeed, while those not specified must fail with an HTTP 403 status code.</span></span> <span data-ttu-id="a7128-131">检查所有响应状态代码，确认应用中 RSC 权限的行为符合预期。</span><span class="sxs-lookup"><span data-stu-id="a7128-131">Check all of the response status codes to confirm that the behavior of the RSC permissions in your app meet expectations.</span></span>

> [!NOTE]
> <span data-ttu-id="a7128-132">若要测试特定的 DELETE 和 READ API 调用，请向 JSON 文件添加这些实例方案。</span><span class="sxs-lookup"><span data-stu-id="a7128-132">To test specific DELETE and READ API calls, add those instance scenarios to the JSON file.</span></span>

## <a name="test-revoked-rsc-permissions-using-postman"></a><span data-ttu-id="a7128-133">使用[Postman](https://www.postman.com/)测试吊销的 RSC 权限</span><span class="sxs-lookup"><span data-stu-id="a7128-133">Test revoked RSC permissions using [Postman](https://www.postman.com/)</span></span>

1. <span data-ttu-id="a7128-134">从特定团队卸载应用。</span><span class="sxs-lookup"><span data-stu-id="a7128-134">Uninstall the app from the specific team.</span></span>
2. <span data-ttu-id="a7128-135">按照使用 [Postman 测试添加的 RSC 权限的步骤操作](#test-added-rsc-permissions-using-the-postman-app)。</span><span class="sxs-lookup"><span data-stu-id="a7128-135">Follow the steps for [Test added RSC permissions using Postman](#test-added-rsc-permissions-using-the-postman-app).</span></span>
3. <span data-ttu-id="a7128-136">检查所有响应状态代码，确认特定 API 调用已成功，但 **HTTP 403 状态代码失败**。</span><span class="sxs-lookup"><span data-stu-id="a7128-136">Check all the response status codes to confirm that the specific API calls, **succeeded, have failed with an HTTP 403 status code**.</span></span>

## <a name="see-also"></a><span data-ttu-id="a7128-137">另请参阅</span><span class="sxs-lookup"><span data-stu-id="a7128-137">See also</span></span>

- [<span data-ttu-id="a7128-138">Microsoft Graph API 和 Teams</span><span class="sxs-lookup"><span data-stu-id="a7128-138">Microsoft Graph API and Teams</span></span>](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)

