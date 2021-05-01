---
title: 维护和支持已发布的应用
description: 在应用商店和 AppSource 上列出应用商店后Teams的考虑。
ms.topic: conceptual
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 57b57e268a4f2eafc14d0372b8b8383e410a80d5
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101749"
---
# <a name="maintain-your-published-microsoft-teams-app"></a><span data-ttu-id="1c9f5-103">维护已发布Microsoft Teams应用程序</span><span class="sxs-lookup"><span data-stu-id="1c9f5-103">Maintain your published Microsoft Teams app</span></span>

<span data-ttu-id="1c9f5-104">在应用商店中Microsoft Teams应用后，开始考虑如何继续维护应用并增加下载量和使用。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-104">With your app listed on the Microsoft Teams store, start thinking about how you'll maintain the app going forward and increase downloads and usage.</span></span>

## <a name="publish-updates-to-your-app"></a><span data-ttu-id="1c9f5-105">将更新发布到应用</span><span class="sxs-lookup"><span data-stu-id="1c9f5-105">Publish updates to your app</span></span>

<span data-ttu-id="1c9f5-106">你可以向应用提交更改 (如合作伙伴中心中的新功能) 元数据。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-106">You can submit changes to your app (such as new features or even metadata) in Partner Center.</span></span> <span data-ttu-id="1c9f5-107">这些更改需要新的审阅过程。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-107">These changes requires a new review process.</span></span>

<span data-ttu-id="1c9f5-108">发布更新时，请确保以下各项：</span><span class="sxs-lookup"><span data-stu-id="1c9f5-108">Ensure the following when publishing updates:</span></span>

* <span data-ttu-id="1c9f5-109">不要更改应用 ID。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-109">Don't change your app ID.</span></span>
* <span data-ttu-id="1c9f5-110">递增应用的版本号。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-110">Increment your app's version number.</span></span>
* <span data-ttu-id="1c9f5-111">在合作伙伴中心中，不要选择" **添加新应用** "以执行更新。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-111">In Partner Center, don't select **Add a new app** to do the update.</span></span> <span data-ttu-id="1c9f5-112">改为转到应用页面。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-112">Go to your app's page instead.</span></span>

### <a name="app-updates-requiring-user-consent"></a><span data-ttu-id="1c9f5-113">需要用户同意的应用更新</span><span class="sxs-lookup"><span data-stu-id="1c9f5-113">App updates requiring user consent</span></span>

<span data-ttu-id="1c9f5-114">当用户安装你的应用时，他们必须向应用授予访问应用正常运行所需的服务和信息的权限。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-114">When a user installs your app, they must give the app permission to access the services and information the app requires to function.</span></span> <span data-ttu-id="1c9f5-115">在大多数情况下，用户只需执行一次此操作，并自动安装新版本的应用。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-115">In most cases, users only have to do this once and new versions of your app install automatically.</span></span>

<span data-ttu-id="1c9f5-116">但是，如果你对应用进行以下任何更改，则现有用户必须接受另一个权限请求才能安装更新：</span><span class="sxs-lookup"><span data-stu-id="1c9f5-116">If you make any of the following changes to your app, however, your existing users must accept another permission request to install the update:</span></span>

* <span data-ttu-id="1c9f5-117">添加或删除机器人。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-117">Add or remove a bot.</span></span>
* <span data-ttu-id="1c9f5-118">更改机器人 ID。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-118">Change the bot ID.</span></span>
* <span data-ttu-id="1c9f5-119">修改机器人的单向通知配置。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-119">Modify a bot's one-way notification configuration.</span></span>
* <span data-ttu-id="1c9f5-120">修改自动程序对上载和下载文件的支持。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-120">Modify a bot's support for uploading and downloading files.</span></span>
* <span data-ttu-id="1c9f5-121">添加或删除邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-121">Add or remove a messaging extension.</span></span>
* <span data-ttu-id="1c9f5-122">添加个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-122">Add a personal tab.</span></span>
* <span data-ttu-id="1c9f5-123">添加频道和组选项卡。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-123">Add a channel and group tab.</span></span>
* <span data-ttu-id="1c9f5-124">添加连接器。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-124">Add a connector.</span></span>
* <span data-ttu-id="1c9f5-125">修改与 Azure AD Azure Active Directory (应用) 相关的配置。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-125">Modify configurations related to your Azure Active Directory (Azure AD) app registration.</span></span> <span data-ttu-id="1c9f5-126">有关详细信息，请参阅 [`webApplicationInfo`](~/resources/schema/manifest-schema.md#webapplicationinfo) 。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-126">For more information, see [`webApplicationInfo`](~/resources/schema/manifest-schema.md#webapplicationinfo).</span></span>

## <a name="fix-issues-with-your-published-app"></a><span data-ttu-id="1c9f5-127">修复已发布应用的问题</span><span class="sxs-lookup"><span data-stu-id="1c9f5-127">Fix issues with your published app</span></span>

<span data-ttu-id="1c9f5-128">Microsoft 对应用商店中列出的应用运行每日Teams测试。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-128">Microsoft runs daily automation tests on apps listed on the Teams store.</span></span> <span data-ttu-id="1c9f5-129">如果发现你的应用的问题，我们会通过详细报告联系你，以了解如何重现这些问题以及解决这些问题的建议。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-129">If issues with your app are identified, we contact you with a detailed report on how to reproduce the issues and recommendations to resolve them.</span></span> <span data-ttu-id="1c9f5-130">如果无法修复已规定时间线中的问题，你的应用一览可能会从应用商店中删除。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-130">If you can't fix the problems within a stated timeline, your app listing may be removed from the store.</span></span>

## <a name="promote-your-app-on-another-site"></a><span data-ttu-id="1c9f5-131">在另一个网站上推广你的应用</span><span class="sxs-lookup"><span data-stu-id="1c9f5-131">Promote your app on another site</span></span>

<span data-ttu-id="1c9f5-132">当你的应用在应用商店Teams时，你可以创建一个链接来启动Teams并显示用于安装应用的对话框。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-132">When your app is listed in the Teams store, you can create a link that launches Teams and displays a dialog to install your app.</span></span> <span data-ttu-id="1c9f5-133">例如，可以在产品的营销页面上包含此链接和下载按钮。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-133">You could include this link, for example, with a download button on your product's marketing page.</span></span>

<span data-ttu-id="1c9f5-134">使用应用 ID 附加的以下 URL 创建链接 `https://teams.microsoft.com/l/app/<your-app-id>` ：。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-134">Create the link using the following URL appended with your app ID: `https://teams.microsoft.com/l/app/<your-app-id>`.</span></span>

## <a name="complete-microsoft-365-certification"></a><span data-ttu-id="1c9f5-135">完成Microsoft 365认证</span><span class="sxs-lookup"><span data-stu-id="1c9f5-135">Complete Microsoft 365 Certification</span></span>

<span data-ttu-id="1c9f5-136">[Microsoft 365](/microsoft-365-app-certification/docs/certification)认证可保证当在 Office 应用 生态系统中安装第三方 Office 应用 或外接程序时，数据和隐私Microsoft 365受保护。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-136">[Microsoft 365 Certification](/microsoft-365-app-certification/docs/certification) offers assurances that data and privacy are adequately secured and protected when a third-party Office app or add-in is installed in your Microsoft 365 ecosystem.</span></span> <span data-ttu-id="1c9f5-137">认证确认你的应用与 Microsoft 技术兼容，符合云应用安全最佳做法，并且受 Microsoft 支持。</span><span class="sxs-lookup"><span data-stu-id="1c9f5-137">Certification confirms that your app is compatible with Microsoft technologies, compliant with cloud app security best practices, and supported by Microsoft.</span></span>

## <a name="see-also"></a><span data-ttu-id="1c9f5-138">另请参阅</span><span class="sxs-lookup"><span data-stu-id="1c9f5-138">See also</span></span>

* [<span data-ttu-id="1c9f5-139">通过 Microsoft 商业市场利用应用盈利</span><span class="sxs-lookup"><span data-stu-id="1c9f5-139">Monetize your app through Microsoft Commercial Marketplace</span></span>](/office/dev/store/monetize-addins-through-microsoft-commercial-marketplace)
