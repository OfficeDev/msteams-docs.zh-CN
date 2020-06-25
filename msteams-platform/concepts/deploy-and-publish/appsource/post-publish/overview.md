---
title: 发布发布
description: 发布应用程序后要执行的操作
keywords: 团队发布更新证书
ms.openlocfilehash: 77b74d77546de0ae93b0ae39aec925d2e3dec2cf
ms.sourcegitcommit: fdc50183f3f4bec9e4b83bcfe5e016b591402f7c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/24/2020
ms.locfileid: "44867090"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="c8df4-104">维护和支持您发布的应用程序</span><span class="sxs-lookup"><span data-stu-id="c8df4-104">Maintain and support your published app</span></span> 

<span data-ttu-id="c8df4-105">在应用程序获得批准并在公用应用程序目录中列出后，可以通过实现应用程序证书或添加网站的 "下载" 按钮来增加您的访问范围。</span><span class="sxs-lookup"><span data-stu-id="c8df4-105">After your app is approved and listed in the public app catalog, you can increase your reach by achieving app certification, or adding a download button your website.</span></span>

## <a name="application-certificate"></a><span data-ttu-id="c8df4-106">应用程序证书</span><span class="sxs-lookup"><span data-stu-id="c8df4-106">Application Certificate</span></span>

<span data-ttu-id="c8df4-107">Microsoft 提供了[应用程序认证计划](./application-certification.md)，用于编译应用程序信息，并将其呈现在[Microsoft 团队应用程序安全性和合规性页面](https://aka.ms/AppCertification)上。</span><span class="sxs-lookup"><span data-stu-id="c8df4-107">Microsoft provides a [Application Certification program](./application-certification.md) that compiles your app information and presents it on [Microsoft Teams App Security and Compliance Page](https://aka.ms/AppCertification).</span></span> <span data-ttu-id="c8df4-108">此信息旨在帮助管理员选择对其组织而言是安全的应用程序。</span><span class="sxs-lookup"><span data-stu-id="c8df4-108">This information is intended to help admins to choose apps that are safe for their organizations.</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="c8df4-109">将 "下载" 按钮添加到产品网站</span><span class="sxs-lookup"><span data-stu-id="c8df4-109">Add a download button to your product site</span></span>

<span data-ttu-id="c8df4-110">如果您的应用程序位于 Microsoft 团队存储中，则可以为您的网站生成一个链接，用于启动团队并显示用户添加应用程序的许可和安装对话框。</span><span class="sxs-lookup"><span data-stu-id="c8df4-110">If your app is in the Microsoft Teams store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="c8df4-111">格式为： `https://teams.microsoft.com/l/app/<appId>` 其中 appID 是它们在提交的清单中声明的 GUID。</span><span class="sxs-lookup"><span data-stu-id="c8df4-111">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="c8df4-112">示例： `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` 是用于安装 Trello 的链接。</span><span class="sxs-lookup"><span data-stu-id="c8df4-112">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="c8df4-113">更新现有团队应用程序</span><span class="sxs-lookup"><span data-stu-id="c8df4-113">Updating your existing Teams app</span></span>

* <span data-ttu-id="c8df4-114">请勿使用 "*添加新应用*" 按钮重新提交您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="c8df4-114">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="c8df4-115">改为对 "概述" 选项卡上的应用程序使用磁贴。</span><span class="sxs-lookup"><span data-stu-id="c8df4-115">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="c8df4-116">更新后的清单中的 appId 应与当前清单中的 appId 相同，并增加了版本号。</span><span class="sxs-lookup"><span data-stu-id="c8df4-116">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="c8df4-117">如果对提交内容进行任何清单更改，请增加清单中的版本号。</span><span class="sxs-lookup"><span data-stu-id="c8df4-117">Increment your version number in the manifest if you make any manifest changes to your submission.</span></span>
* <span data-ttu-id="c8df4-118">需要进行更新的提交，以进行新的审阅和验证过程。</span><span class="sxs-lookup"><span data-stu-id="c8df4-118">Updated submissions are required to undergo a new review and validation process.</span></span>

## <a name="app-updates-and-the-user-consent-flow"></a><span data-ttu-id="c8df4-119">应用程序更新和用户同意流程</span><span class="sxs-lookup"><span data-stu-id="c8df4-119">App updates and the user consent flow</span></span>

<span data-ttu-id="c8df4-120">当用户安装您的应用程序时，他们所做的第一件事是同意授予应用程序访问应用程序执行其工作所需的服务和信息的权限。</span><span class="sxs-lookup"><span data-stu-id="c8df4-120">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="c8df4-121">在大多数情况下，在完成应用更新后，最终用户将自动显示新版本。</span><span class="sxs-lookup"><span data-stu-id="c8df4-121">In most cases, after you complete an app update the new version will automatically appear for end users.</span></span> <span data-ttu-id="c8df4-122">但是，对[团队应用程序清单](../../../../resources/schema/manifest-schema.md)的一些更新需要用户接受才能完成，并且可能会重新触发此同意行为：</span><span class="sxs-lookup"><span data-stu-id="c8df4-122">However, there are some updates to the [Teams app manifest](../../../../resources/schema/manifest-schema.md) that require user acceptance to complete and can re-trigger this consent behavior:</span></span>

 >[!div class="checklist"]
>
> * <span data-ttu-id="c8df4-123">添加或删除了一个 bot。</span><span class="sxs-lookup"><span data-stu-id="c8df4-123">A bot was added or removed.</span></span>
> * <span data-ttu-id="c8df4-124">现有 bot 的唯一 `botId` 值已更改。</span><span class="sxs-lookup"><span data-stu-id="c8df4-124">An existing bot's unique `botId` value changed.</span></span>
> * <span data-ttu-id="c8df4-125">现有 bot 的 `isNotificationOnly` boolean 值已更改。</span><span class="sxs-lookup"><span data-stu-id="c8df4-125">An existing bot's `isNotificationOnly` boolean value changed.</span></span>
> * <span data-ttu-id="c8df4-126">现有 bot 的 `supportsFiles` boolean 值已更改。</span><span class="sxs-lookup"><span data-stu-id="c8df4-126">An existing bot's `supportsFiles` boolean value changed.</span></span>
> * <span data-ttu-id="c8df4-127">添加或删除了邮件扩展（ `composeExtensions` ）。</span><span class="sxs-lookup"><span data-stu-id="c8df4-127">A messaging extension (`composeExtensions`) was added or removed.</span></span>
> * <span data-ttu-id="c8df4-128">添加了新的连接器。</span><span class="sxs-lookup"><span data-stu-id="c8df4-128">A new connector was added.</span></span>
> * <span data-ttu-id="c8df4-129">添加了一个新的静态/个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="c8df4-129">A new static/personal tab was added.</span></span>
> * <span data-ttu-id="c8df4-130">添加了一个新的可配置组/通道选项卡。</span><span class="sxs-lookup"><span data-stu-id="c8df4-130">A new configurable group/channel tab was added.</span></span>
> * <span data-ttu-id="c8df4-131">`webApplicationInfo`值已更改。</span><span class="sxs-lookup"><span data-stu-id="c8df4-131">The `webApplicationInfo` values changed.</span></span>
>