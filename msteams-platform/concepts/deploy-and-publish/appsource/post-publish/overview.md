---
title: 维护和支持已发布的应用
description: 发布应用后要执行哪些操作
ms.topic: how-to
keywords: teams 发布更新认证应用更新清单
ms.openlocfilehash: 8644db5e329e15d77062553eda4a41a36b2740ee
ms.sourcegitcommit: e78c9f51c4538212c53bb6c6a45a09d994896f09
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/05/2021
ms.locfileid: "51585832"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="1dc7f-104">维护和支持已发布的应用</span><span class="sxs-lookup"><span data-stu-id="1dc7f-104">Maintain and support your published app</span></span> 

<span data-ttu-id="1dc7f-105">在公共应用目录中批准并列出应用后，可以通过完成 Microsoft 365 应用合规性计划或在网站上添加下载按钮来扩大应用范围。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-105">After your app is approved and listed in the public app catalog, you can increase your reach by completing the Microsoft 365 App Compliance Program or by adding a download button on your website.</span></span>

## <a name="microsoft-365-certified"></a><span data-ttu-id="1dc7f-106">Microsoft 365 认证</span><span class="sxs-lookup"><span data-stu-id="1dc7f-106">Microsoft 365 Certified</span></span>

<span data-ttu-id="1dc7f-107">[Microsoft 365 应用合规性计划](./application-certification.md)是应用安全性和合规性的三层方法。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-107">The [Microsoft 365 App Compliance Program](./application-certification.md), is a three tier approach to app security and compliance.</span></span> <span data-ttu-id="1dc7f-108">每一层都基于下一层构建 - 提供分层计划以满足客户的需求。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-108">Each tier builds upon the next – offering a layered program to meet your customer’s needs.</span></span> <span data-ttu-id="1dc7f-109">可以通过访问合规性页面来了解有关 Teams 应用的安全性和合规性[状态。](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps)</span><span class="sxs-lookup"><span data-stu-id="1dc7f-109">You can learn more about the security and compliance posture of Teams apps by visiting the [compliance page](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps).</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="1dc7f-110">将下载按钮添加到产品网站</span><span class="sxs-lookup"><span data-stu-id="1dc7f-110">Add a download button to your product site</span></span>

<span data-ttu-id="1dc7f-111">如果你的应用位于 Microsoft Teams 全局应用商店中，你可以为网站生成一个链接，用于启动 Teams，并显示用户添加应用的同意和安装对话框。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-111">If your app is in the Microsoft Teams global store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="1dc7f-112">格式为：其中 appID 是它们在提交的清单中  `https://teams.microsoft.com/l/app/<appId>` 声明的 GUID。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-112">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="1dc7f-113">示例： `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` 是安装 Trello 的链接。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-113">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="1dc7f-114">更新现有 Teams 应用</span><span class="sxs-lookup"><span data-stu-id="1dc7f-114">Updating your existing Teams app</span></span>

* <span data-ttu-id="1dc7f-115">请勿使用 *"添加新应用"* 按钮重新提交应用。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-115">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="1dc7f-116">改为使用"概述"选项卡上的应用磁贴。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-116">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="1dc7f-117">更新后的清单中的 appId 应该与当前清单中的相同，并递增版本号。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-117">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="1dc7f-118">如果你对提交（包括应用名称或清单中任何元数据）进行更改，则增加清单中的版本号。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-118">Increment your version number in the manifest if you make any changes to your submission including app name or any metadata in the manifest.</span></span>
* <span data-ttu-id="1dc7f-119">更新的提交需要经过新的审阅和验证过程。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-119">Updated submissions are required to undergo a new review and validation process.</span></span>

## <a name="app-updates-and-the-user-consent-flow"></a><span data-ttu-id="1dc7f-120">应用更新和用户同意流</span><span class="sxs-lookup"><span data-stu-id="1dc7f-120">App updates and the user consent flow</span></span>

<span data-ttu-id="1dc7f-121">当用户安装您的应用程序时，他们首先执行的工作之一是同意向应用程序授予访问执行其作业所需的服务和信息的权限。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-121">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="1dc7f-122">在大多数情况下，完成应用更新后，将为最终用户自动显示新版本。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-122">In most cases, after you complete an app update the new version will automatically appear for end users.</span></span> <span data-ttu-id="1dc7f-123">但是，Teams 应用清单的一[](../../../../resources/schema/manifest-schema.md)些更新需要用户接受才能完成，并可以重新触发此同意行为：</span><span class="sxs-lookup"><span data-stu-id="1dc7f-123">However, there are some updates to the [Teams app manifest](../../../../resources/schema/manifest-schema.md) that require user acceptance to complete and can re-trigger this consent behavior:</span></span>

 >[!div class="checklist"]
>
> * <span data-ttu-id="1dc7f-124">添加或删除自动程序。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-124">A bot is added or removed.</span></span>
> * <span data-ttu-id="1dc7f-125">更改现有自动程序 `botId` 的唯一值。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-125">An existing bot's unique `botId` value is changed.</span></span>
> * <span data-ttu-id="1dc7f-126">现有自动程序 `isNotificationOnly` 布尔值已更改。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-126">An existing bot's `isNotificationOnly` boolean value is changed.</span></span>
> * <span data-ttu-id="1dc7f-127">现有自动程序 `supportsFiles` 或 `supportsCalling` 布尔值已更改。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-127">An existing bot's `supportsFiles` or `supportsCalling` boolean value is changed.</span></span>
> * <span data-ttu-id="1dc7f-128">添加或删除 `composeExtensions` 邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-128">A messaging extension `composeExtensions` is added or removed.</span></span>
> * <span data-ttu-id="1dc7f-129">添加了一个新连接器。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-129">A new connector is added.</span></span>
> * <span data-ttu-id="1dc7f-130">添加了新的静态或个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-130">A new static or personal tab is added.</span></span>
> * <span data-ttu-id="1dc7f-131">添加了新的可配置组或频道选项卡。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-131">A new configurable group or channel tab is added.</span></span>
> * <span data-ttu-id="1dc7f-132">内部的属性 `webApplicationInfo` 已更改。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-132">The properties inside `webApplicationInfo` are changed.</span></span> <span data-ttu-id="1dc7f-133">对于 的更改 `webApplicationInfo` ，仅在 Teams 范围内需要同意。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-133">For changes to `webApplicationInfo`, consent is only required in the Teams scope.</span></span>

### <a name="images-of-user-consent-flow"></a><span data-ttu-id="1dc7f-134">用户同意流程的图像：</span><span class="sxs-lookup"><span data-stu-id="1dc7f-134">Images of user consent flow:</span></span>

<span data-ttu-id="1dc7f-135">**设置连接器** - 此屏幕将仅为 Teams 用户显示。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-135">**Set up a connector** —  This screen will appear only for Teams users.</span></span>

![同意流设置连接器图](../../../../assets/images/connector-teams-consentflow.png)

<span data-ttu-id="1dc7f-137">**用户同意流** - 此屏幕在个人和组范围内都很常见。</span><span class="sxs-lookup"><span data-stu-id="1dc7f-137">**User consent flow** - This screen is common for both personal and group scope.</span></span> <span data-ttu-id="1dc7f-138">在此处，选中"**代表你的组织同意"复选框，** 然后选择"接受 **"。**</span><span class="sxs-lookup"><span data-stu-id="1dc7f-138">Here, select the **Consent on behalf of your organization** checkbox and choose **Accept**.</span></span>

![权限图](../../../../assets/images/user-consent-flow.png)
