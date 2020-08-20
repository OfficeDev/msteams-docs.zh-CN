---
title: 发布后
description: 发布应用程序后的操作
keywords: Teams 发布后更新证书
ms.openlocfilehash: d2cc6c5427c5b4f7320f0ec2e022f2c69467a33d
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819152"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="71cc0-104">维护和支持已发布的应用</span><span class="sxs-lookup"><span data-stu-id="71cc0-104">Maintain and support your published app</span></span> 

<span data-ttu-id="71cc0-105">在应用程序获得批准并在公共应用目录中列出后，可以通过完成 Microsoft 365 应用合规性计划或在网站上添加下载按钮来提高覆盖范围。</span><span class="sxs-lookup"><span data-stu-id="71cc0-105">After your app is approved and listed in the public app catalog, you can increase your reach by completing the Microsoft 365 App Compliance Program or by adding a download button on your website.</span></span>

## <a name="microsoft-365-certified"></a><span data-ttu-id="71cc0-106">Microsoft 365 认证</span><span class="sxs-lookup"><span data-stu-id="71cc0-106">Microsoft 365 Certified</span></span>

<span data-ttu-id="71cc0-107">[Microsoft 365 应用合规性计划是](./application-certification.md)应用安全性和合规性的三层方法。</span><span class="sxs-lookup"><span data-stu-id="71cc0-107">The [Microsoft 365 App Compliance Program](./application-certification.md), is a three tier approach to app security and compliance.</span></span> <span data-ttu-id="71cc0-108">每个层基于下一层 - 提供分层计划来满足客户需求。</span><span class="sxs-lookup"><span data-stu-id="71cc0-108">Each tier builds upon the next – offering a layered program to meet your customer’s needs.</span></span> <span data-ttu-id="71cc0-109">可通过访问合规性页面，了解有关 Teams 应用的安全性和合规 [状态的详细信息](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps)。</span><span class="sxs-lookup"><span data-stu-id="71cc0-109">You can learn more about the security and compliance posture of Teams apps by visiting the [compliance page](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps).</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="71cc0-110">将下载按钮添加到产品网站</span><span class="sxs-lookup"><span data-stu-id="71cc0-110">Add a download button to your product site</span></span>

<span data-ttu-id="71cc0-111">如果你的应用在 Microsoft Teams 应用商店中，则可为网站生成一个链接，用于启动 Teams 并显示许可和安装对话框，以便用户添加应用。</span><span class="sxs-lookup"><span data-stu-id="71cc0-111">If your app is in the Microsoft Teams store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="71cc0-112">格式为：  `https://teams.microsoft.com/l/app/<appId>` 其中 appID 是其在提交清单中声明的 GUID。</span><span class="sxs-lookup"><span data-stu-id="71cc0-112">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="71cc0-113">示例： `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` 是安装 Trello 的链接。</span><span class="sxs-lookup"><span data-stu-id="71cc0-113">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="71cc0-114">更新现有 Teams 应用</span><span class="sxs-lookup"><span data-stu-id="71cc0-114">Updating your existing Teams app</span></span>

* <span data-ttu-id="71cc0-115">不要使用" *添加新应用"* 按钮重新提交应用。</span><span class="sxs-lookup"><span data-stu-id="71cc0-115">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="71cc0-116">改为在"概述"选项卡上为你的应用使用磁贴。</span><span class="sxs-lookup"><span data-stu-id="71cc0-116">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="71cc0-117">更新后清单中的 appId 应与当前清单中的 appId 相同，并具有增加的版本号。</span><span class="sxs-lookup"><span data-stu-id="71cc0-117">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="71cc0-118">当你对提交进行任何清单更改时，请增加清单中的版本号。</span><span class="sxs-lookup"><span data-stu-id="71cc0-118">Increment your version number in the manifest if you make any manifest changes to your submission.</span></span>
* <span data-ttu-id="71cc0-119">要求更新后的提交执行新的审查和验证流程。</span><span class="sxs-lookup"><span data-stu-id="71cc0-119">Updated submissions are required to undergo a new review and validation process.</span></span>

## <a name="app-updates-and-the-user-consent-flow"></a><span data-ttu-id="71cc0-120">应用更新和用户同意流</span><span class="sxs-lookup"><span data-stu-id="71cc0-120">App updates and the user consent flow</span></span>

<span data-ttu-id="71cc0-121">当用户安装您的应用程序的第一个操作时，他们所执行的操作就是向应用授予访问服务和应用完成工作所需的信息的权限。</span><span class="sxs-lookup"><span data-stu-id="71cc0-121">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="71cc0-122">在大多数情况下，完成应用更新后，新版本将自动为最终用户显示。</span><span class="sxs-lookup"><span data-stu-id="71cc0-122">In most cases, after you complete an app update the new version will automatically appear for end users.</span></span> <span data-ttu-id="71cc0-123">但是，会有一些 Teams 应用 [清单更新](../../../../resources/schema/manifest-schema.md) 来要求用户接受才能完成并可以重新触发此同意行为：</span><span class="sxs-lookup"><span data-stu-id="71cc0-123">However, there are some updates to the [Teams app manifest](../../../../resources/schema/manifest-schema.md) that require user acceptance to complete and can re-trigger this consent behavior:</span></span>

 >[!div class="checklist"]
>
> * <span data-ttu-id="71cc0-124">已添加或删除自动程序。</span><span class="sxs-lookup"><span data-stu-id="71cc0-124">A bot was added or removed.</span></span>
> * <span data-ttu-id="71cc0-125">已更改的现有自动程序的 `botId` 唯一值。</span><span class="sxs-lookup"><span data-stu-id="71cc0-125">An existing bot's unique `botId` value changed.</span></span>
> * <span data-ttu-id="71cc0-126">已有的机器人的 `isNotificationOnly` 布尔值已更改。</span><span class="sxs-lookup"><span data-stu-id="71cc0-126">An existing bot's `isNotificationOnly` boolean value changed.</span></span>
> * <span data-ttu-id="71cc0-127">已有的机器人的 `supportsFiles` 布尔值已更改。</span><span class="sxs-lookup"><span data-stu-id="71cc0-127">An existing bot's `supportsFiles` boolean value changed.</span></span>
> * <span data-ttu-id="71cc0-128">添加或删除 `composeExtensions` () 或) 消息扩展。</span><span class="sxs-lookup"><span data-stu-id="71cc0-128">A messaging extension (`composeExtensions`) was added or removed.</span></span>
> * <span data-ttu-id="71cc0-129">添加了新的连接器。</span><span class="sxs-lookup"><span data-stu-id="71cc0-129">A new connector was added.</span></span>
> * <span data-ttu-id="71cc0-130">添加了新的静态/个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="71cc0-130">A new static/personal tab was added.</span></span>
> * <span data-ttu-id="71cc0-131">添加了新的可配置组/频道选项卡。</span><span class="sxs-lookup"><span data-stu-id="71cc0-131">A new configurable group/channel tab was added.</span></span>
> * <span data-ttu-id="71cc0-132">值 `webApplicationInfo` 已更改。</span><span class="sxs-lookup"><span data-stu-id="71cc0-132">The `webApplicationInfo` values changed.</span></span>
>
