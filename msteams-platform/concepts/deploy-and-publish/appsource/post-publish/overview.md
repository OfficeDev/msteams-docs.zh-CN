---
title: 发布发布
description: 发布应用程序后要执行的操作
keywords: 团队发布更新证书
ms.openlocfilehash: 887e18ac7e27cf12aa4319ac240e42f21f05fd75
ms.sourcegitcommit: e355f59d2d21a2d5ae36cc46acad5ed4765b42e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "45021571"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="b007c-104">维护和支持您发布的应用程序</span><span class="sxs-lookup"><span data-stu-id="b007c-104">Maintain and support your published app</span></span> 

<span data-ttu-id="b007c-105">在应用程序获得批准并在公用应用程序目录中列出后，可以通过完成 Microsoft 365 应用合规性计划或在网站上添加 "下载" 按钮来提高您的访问范围。</span><span class="sxs-lookup"><span data-stu-id="b007c-105">After your app is approved and listed in the public app catalog, you can increase your reach by completing the Microsoft 365 App Compliance Program or by adding a download button on your website.</span></span>

## <a name="m365-certified"></a><span data-ttu-id="b007c-106">M365 认证</span><span class="sxs-lookup"><span data-stu-id="b007c-106">M365 Certified</span></span>

<span data-ttu-id="b007c-107">[Microsoft 365 应用合规性计划](./application-certification.md)是一种用于应用程序安全性和合规性的三层方法。</span><span class="sxs-lookup"><span data-stu-id="b007c-107">The [Microsoft 365 App Compliance Program](./application-certification.md), is a three tier approach to app security and compliance.</span></span> <span data-ttu-id="b007c-108">每个层都基于下一个分层计划，以满足客户的需求。</span><span class="sxs-lookup"><span data-stu-id="b007c-108">Each tier builds upon the next – offering a layered program to meet your customer’s needs.</span></span> <span data-ttu-id="b007c-109">您可以通过访问[合规性页面](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps)来了解有关团队应用程序的安全和合规性状况的详细信息。</span><span class="sxs-lookup"><span data-stu-id="b007c-109">You can learn more about the security and compliance posture of Teams apps by visiting the [compliance page](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps).</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="b007c-110">将 "下载" 按钮添加到产品网站</span><span class="sxs-lookup"><span data-stu-id="b007c-110">Add a download button to your product site</span></span>

<span data-ttu-id="b007c-111">如果您的应用程序位于 Microsoft 团队存储中，则可以为您的网站生成一个链接，用于启动团队并显示用户添加应用程序的许可和安装对话框。</span><span class="sxs-lookup"><span data-stu-id="b007c-111">If your app is in the Microsoft Teams store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="b007c-112">格式为： `https://teams.microsoft.com/l/app/<appId>` 其中 appID 是它们在提交的清单中声明的 GUID。</span><span class="sxs-lookup"><span data-stu-id="b007c-112">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="b007c-113">示例： `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` 是用于安装 Trello 的链接。</span><span class="sxs-lookup"><span data-stu-id="b007c-113">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="b007c-114">更新现有团队应用程序</span><span class="sxs-lookup"><span data-stu-id="b007c-114">Updating your existing Teams app</span></span>

* <span data-ttu-id="b007c-115">请勿使用 "*添加新应用*" 按钮重新提交您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="b007c-115">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="b007c-116">改为对 "概述" 选项卡上的应用程序使用磁贴。</span><span class="sxs-lookup"><span data-stu-id="b007c-116">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="b007c-117">更新后的清单中的 appId 应与当前清单中的 appId 相同，并增加了版本号。</span><span class="sxs-lookup"><span data-stu-id="b007c-117">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="b007c-118">如果对提交内容进行任何清单更改，请增加清单中的版本号。</span><span class="sxs-lookup"><span data-stu-id="b007c-118">Increment your version number in the manifest if you make any manifest changes to your submission.</span></span>
* <span data-ttu-id="b007c-119">需要进行更新的提交，以进行新的审阅和验证过程。</span><span class="sxs-lookup"><span data-stu-id="b007c-119">Updated submissions are required to undergo a new review and validation process.</span></span>

## <a name="app-updates-and-the-user-consent-flow"></a><span data-ttu-id="b007c-120">应用程序更新和用户同意流程</span><span class="sxs-lookup"><span data-stu-id="b007c-120">App updates and the user consent flow</span></span>

<span data-ttu-id="b007c-121">当用户安装您的应用程序时，他们所做的第一件事是同意授予应用程序访问应用程序执行其工作所需的服务和信息的权限。</span><span class="sxs-lookup"><span data-stu-id="b007c-121">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="b007c-122">在大多数情况下，在完成应用更新后，最终用户将自动显示新版本。</span><span class="sxs-lookup"><span data-stu-id="b007c-122">In most cases, after you complete an app update the new version will automatically appear for end users.</span></span> <span data-ttu-id="b007c-123">但是，对[团队应用程序清单](../../../../resources/schema/manifest-schema.md)的一些更新需要用户接受才能完成，并且可能会重新触发此同意行为：</span><span class="sxs-lookup"><span data-stu-id="b007c-123">However, there are some updates to the [Teams app manifest](../../../../resources/schema/manifest-schema.md) that require user acceptance to complete and can re-trigger this consent behavior:</span></span>

 >[!div class="checklist"]
>
> * <span data-ttu-id="b007c-124">添加或删除了一个 bot。</span><span class="sxs-lookup"><span data-stu-id="b007c-124">A bot was added or removed.</span></span>
> * <span data-ttu-id="b007c-125">现有 bot 的唯一 `botId` 值已更改。</span><span class="sxs-lookup"><span data-stu-id="b007c-125">An existing bot's unique `botId` value changed.</span></span>
> * <span data-ttu-id="b007c-126">现有 bot 的 `isNotificationOnly` boolean 值已更改。</span><span class="sxs-lookup"><span data-stu-id="b007c-126">An existing bot's `isNotificationOnly` boolean value changed.</span></span>
> * <span data-ttu-id="b007c-127">现有 bot 的 `supportsFiles` boolean 值已更改。</span><span class="sxs-lookup"><span data-stu-id="b007c-127">An existing bot's `supportsFiles` boolean value changed.</span></span>
> * <span data-ttu-id="b007c-128">添加或删除了邮件扩展（ `composeExtensions` ）。</span><span class="sxs-lookup"><span data-stu-id="b007c-128">A messaging extension (`composeExtensions`) was added or removed.</span></span>
> * <span data-ttu-id="b007c-129">添加了新的连接器。</span><span class="sxs-lookup"><span data-stu-id="b007c-129">A new connector was added.</span></span>
> * <span data-ttu-id="b007c-130">添加了一个新的静态/个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="b007c-130">A new static/personal tab was added.</span></span>
> * <span data-ttu-id="b007c-131">添加了一个新的可配置组/通道选项卡。</span><span class="sxs-lookup"><span data-stu-id="b007c-131">A new configurable group/channel tab was added.</span></span>
> * <span data-ttu-id="b007c-132">`webApplicationInfo`值已更改。</span><span class="sxs-lookup"><span data-stu-id="b007c-132">The `webApplicationInfo` values changed.</span></span>
>
