---
title: 测试团队中特定于资源的同意
description: 详细信息在使用 Postman 的团队中测试特定于资源的同意
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: How-to
keywords: 团队授权 OAuth SSO AAD rsc Postman Graph
ms.openlocfilehash: a7384222e5e4cba164f918186ce53b4c1b702016
ms.sourcegitcommit: 3e94edba28e9e1252b6a6ba35d4df32710dfc5d4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2020
ms.locfileid: "46531264"
---
# <a name="test-resource-specific-consent-permissions--in-teams"></a><span data-ttu-id="dafdc-104">在团队中测试特定于资源的同意权限</span><span class="sxs-lookup"><span data-stu-id="dafdc-104">Test resource-specific consent permissions  in Teams</span></span>

<span data-ttu-id="dafdc-105">特定于资源的同意（RSC）是 Microsoft 团队和图形 API 集成，使您的应用程序能够使用 API 终结点来管理组织中的特定团队。</span><span class="sxs-lookup"><span data-stu-id="dafdc-105">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="dafdc-106">请*参阅*  [特定于资源的同意（RSC）— MICROSOFT 团队 Graph API](resource-specific-consent.md)。</span><span class="sxs-lookup"><span data-stu-id="dafdc-106">Please *see*  [Resource-specific consent (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).</span></span>

> [!NOTE]
><span data-ttu-id="dafdc-107">若要测试 RSC 权限，您的团队应用程序清单文件必须包含使用以下字段填充的**webApplicationInfo**项：</span><span class="sxs-lookup"><span data-stu-id="dafdc-107">To test the RSC permissions, your Teams app manifest file must include a **webApplicationInfo** key populated with the following fields:</span></span>
>
> - <span data-ttu-id="dafdc-108">**id** -你的 azure ad 应用 id，*请参阅*[在 azure ad 门户中注册你的应用](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="dafdc-108">**id**  — your Azure AD app id, *see* [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="dafdc-109">**resource** —任何字符串，*请参阅*[更新团队应用程序清单](resource-specific-consent.md#update-your-teams-app-manifest)中的注释</span><span class="sxs-lookup"><span data-stu-id="dafdc-109">**resource**  — any string, *see* the note in  [Update your Teams app manifest](resource-specific-consent.md#update-your-teams-app-manifest)</span></span>
> - <span data-ttu-id="dafdc-110">**应用程序权限**-您的应用程序的 RSC 权限，*请参阅*[特定于资源的权限](resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="dafdc-110">**application permissions** — RSC permissions for  your app, *see* [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

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

>[!IMPORTANT]
><span data-ttu-id="dafdc-111">在您的应用程序清单中，仅包括您希望应用程序具有的 RSC 权限。</span><span class="sxs-lookup"><span data-stu-id="dafdc-111">In your app manifest, only include the RSC permissions that you want your app to have.</span></span>

## <a name="test-added-rsc-permissions-using-the-postman-app"></a><span data-ttu-id="dafdc-112">测试添加了使用 Postman 应用程序的 RSC 权限</span><span class="sxs-lookup"><span data-stu-id="dafdc-112">Test added RSC permissions using the Postman app</span></span>

<span data-ttu-id="dafdc-113">若要检查 API 请求负载是否符合 RSC 权限，需要将[RSC JSON 测试代码](test-rsc-json-file.md)复制到本地环境中并更新以下值：</span><span class="sxs-lookup"><span data-stu-id="dafdc-113">To check whether the RSC permissions are being honored by the API request payload, you'll need to copy the [RSC JSON test code](test-rsc-json-file.md) into your local environment and update the following values:</span></span>

1. <span data-ttu-id="dafdc-114">`azureADAppId`-你的应用程序的 Azure AD 应用 id。</span><span class="sxs-lookup"><span data-stu-id="dafdc-114">`azureADAppId`  — your app's Azure AD app id.</span></span>
1. <span data-ttu-id="dafdc-115">`azureADAppSecret`-你的 Azure AD 应用程序密钥（密码）</span><span class="sxs-lookup"><span data-stu-id="dafdc-115">`azureADAppSecret`  — your Azure AD app secret (password)</span></span>
1. <span data-ttu-id="dafdc-116">`token_scope`—获取令牌所需的作用域-将值设置为https://graph.microsoft.com/.default</span><span class="sxs-lookup"><span data-stu-id="dafdc-116">`token_scope`  — the scope is required to get a token - set the value to https://graph.microsoft.com/.default</span></span>
1. <span data-ttu-id="dafdc-117">`teamGroupId`—可以从团队客户端获取团队组 id，如下所示：</span><span class="sxs-lookup"><span data-stu-id="dafdc-117">`teamGroupId` — you can get the team group id from the Teams client as follows:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="dafdc-118">在团队客户端中，从最左侧的导航栏中选择 "**团队**"。</span><span class="sxs-lookup"><span data-stu-id="dafdc-118">In the Teams client, select **Teams** from the far left nav bar .</span></span>
> * <span data-ttu-id="dafdc-119">从下拉菜单中选择应用程序安装到的团队。</span><span class="sxs-lookup"><span data-stu-id="dafdc-119">Select the team where the app is installed from the dropdown menu.</span></span>
> * <span data-ttu-id="dafdc-120">选择 "**更多选项**" 图标（&#8943;）</span><span class="sxs-lookup"><span data-stu-id="dafdc-120">Select the **More options** icon (&#8943;)</span></span>
> * <span data-ttu-id="dafdc-121">选择 "**获取到团队的链接**"</span><span class="sxs-lookup"><span data-stu-id="dafdc-121">Select **Get link to team**</span></span> 
> * <span data-ttu-id="dafdc-122">复制并保存字符串中的**groupId**值。</span><span class="sxs-lookup"><span data-stu-id="dafdc-122">Copy and save the **groupId** value from the string.</span></span>

### <a name="using-postman"></a><span data-ttu-id="dafdc-123">使用 Postman</span><span class="sxs-lookup"><span data-stu-id="dafdc-123">Using Postman</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="dafdc-124">打开[Postman](https://www.postman.com)应用程序。</span><span class="sxs-lookup"><span data-stu-id="dafdc-124">Open the [Postman](https://www.postman.com) app.</span></span>
> * <span data-ttu-id="dafdc-125">选择 "**文件**  =>  **导入**  =>  **导入文件**" 以从您的环境中上载更新的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="dafdc-125">Select **File** => **Import** => **Import file** to upload the updated JSON file from your environment.</span></span>  
> * <span data-ttu-id="dafdc-126">选择 "**集合**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="dafdc-126">Select the **Collections** tab.</span></span> 
> * <span data-ttu-id="dafdc-127">选择**测试 RSC**旁边的 v 形（>）以展开详细信息视图，并查看 API 请求。</span><span class="sxs-lookup"><span data-stu-id="dafdc-127">Select the chevron (>) next to the **Test RSC** to expand the details view and see the API requests.</span></span>

<span data-ttu-id="dafdc-128">为每个 API 调用执行整个权限集。</span><span class="sxs-lookup"><span data-stu-id="dafdc-128">Execute the entire permissions collection for each API call.</span></span> <span data-ttu-id="dafdc-129">在应用程序清单中指定的权限应成功，而未指定的权限应失败，并出现 HTTP 403 状态代码。</span><span class="sxs-lookup"><span data-stu-id="dafdc-129">The permissions that you specified in your app manifest should succeed, while those not specified should fail with an HTTP 403 status code.</span></span> <span data-ttu-id="dafdc-130">检查所有响应状态代码，以确认您的应用程序中的 RSC 权限行为满足预期。</span><span class="sxs-lookup"><span data-stu-id="dafdc-130">Check all of the response status codes to confirm that the behavior of the RSC permissions in your app meet expectations.</span></span>

>[!NOTE]
><span data-ttu-id="dafdc-131">若要测试特定的 DELETE and READ API 调用，请将这些实例方案添加到 JSON 文件中。</span><span class="sxs-lookup"><span data-stu-id="dafdc-131">To test specific DELETE and READ API calls, please add those instance scenarios to the JSON file.</span></span>

## <a name="test--revoked-rsc-permissions-using-postman"></a><span data-ttu-id="dafdc-132">使用[Postman](https://www.postman.com/)测试已吊销的 RSC 权限</span><span class="sxs-lookup"><span data-stu-id="dafdc-132">Test  revoked RSC permissions using [Postman](https://www.postman.com/)</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="dafdc-133">从特定团队中卸载应用程序。</span><span class="sxs-lookup"><span data-stu-id="dafdc-133">Uninstall the app from the specific team.</span></span>
> * <span data-ttu-id="dafdc-134">按照上述步骤[使用 Postman 添加的 RSC 权限进行测试](#test-added-rsc-permissions-using-the-postman-app)。</span><span class="sxs-lookup"><span data-stu-id="dafdc-134">Follow the steps above for [Test added RSC permissions using Postman](#test-added-rsc-permissions-using-the-postman-app).</span></span>
> * <span data-ttu-id="dafdc-135">检查所有响应状态代码，以确认成功使用 HTTP 403 状态代码的特定 API 调用失败。</span><span class="sxs-lookup"><span data-stu-id="dafdc-135">Check all of the response status codes to confirm that the specific API calls that succeeded have failed with an HTTP 403 status code.</span></span>

> [!div class="nextstepaction"]
>
> [<span data-ttu-id="dafdc-136">了解有关图形 API 和团队的详细信息</span><span class="sxs-lookup"><span data-stu-id="dafdc-136">Learn more about the Graph API and Teams</span></span>](/graph/api/resources/teams-api-overview?view=graph-rest-1.0)
