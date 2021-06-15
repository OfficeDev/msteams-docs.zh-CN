---
title: 启用要自定义的应用
author: heath-hamilton
description: 了解Teams如何为组织自定义你的应用。
localization_priority: Normal
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: bf1b43629c87dd4123520c634772e5dea14e0bb5
ms.sourcegitcommit: 64c1cf2a268ef101a519bc31d171618d0f6cd12a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2021
ms.locfileid: "52915081"
---
# <a name="enable-your-microsoft-teams-app-to-be-customized"></a><span data-ttu-id="5e13c-103">启用Microsoft Teams自定义应用</span><span class="sxs-lookup"><span data-stu-id="5e13c-103">Enable your Microsoft Teams app to be customized</span></span>

<span data-ttu-id="5e13c-104">你可以允许客户在管理中心中Microsoft Teams应用的某些Teams方面。</span><span class="sxs-lookup"><span data-stu-id="5e13c-104">You can allow customers to customize some aspects of your Microsoft Teams app in the Teams admin center.</span></span> <span data-ttu-id="5e13c-105">仅发布到应用商店的应用支持Teams此功能。</span><span class="sxs-lookup"><span data-stu-id="5e13c-105">This feature is supported only for apps published to the Teams store.</span></span> <span data-ttu-id="5e13c-106">无法自定义为组织发布的旁加载应用。</span><span class="sxs-lookup"><span data-stu-id="5e13c-106">Sideloaded apps and apps published for an org can't be customized.</span></span>

<span data-ttu-id="5e13c-107">此功能的一些可能示例包括：</span><span class="sxs-lookup"><span data-stu-id="5e13c-107">Some possible examples of this feature include:</span></span>

* <span data-ttu-id="5e13c-108">更改应用主题色以匹配组织品牌。</span><span class="sxs-lookup"><span data-stu-id="5e13c-108">Changing the app's accent color to match an org's brand.</span></span>
* <span data-ttu-id="5e13c-109">将应用程序名称从 *Contoso* 更新到 *Contoso 代理*，这是组织中的用户将看到的名称。</span><span class="sxs-lookup"><span data-stu-id="5e13c-109">Updating the app name from *Contoso* to *Contoso Agent*, which is the name users in the org will see.</span></span> <span data-ttu-id="5e13c-110"> (注意：向聊天或频道添加连接器的用户仍将看到原始应用名称 *Contoso*.) </span><span class="sxs-lookup"><span data-stu-id="5e13c-110">(Note: Users adding a connector to a chat or a channel will still see the original app name, *Contoso*.)</span></span>

<span data-ttu-id="5e13c-111">可以在开发人员门户中启用此功能[Teams。](https://dev.teams.microsoft.com/home)</span><span class="sxs-lookup"><span data-stu-id="5e13c-111">You can enable this feature in the [Developer Portal for Teams](https://dev.teams.microsoft.com/home).</span></span> <span data-ttu-id="5e13c-112">这将配置 `configurableProperties` ，这不适用于 1.10 之前版本的应用Teams清单。</span><span class="sxs-lookup"><span data-stu-id="5e13c-112">This configures `configurableProperties`, which aren't available in versions prior to 1.10 of the Teams app manifest.</span></span>

## <a name="test-your-app"></a><span data-ttu-id="5e13c-113">测试应用</span><span class="sxs-lookup"><span data-stu-id="5e13c-113">Test your app</span></span>

<span data-ttu-id="5e13c-114">无法在开发期间测试此功能。</span><span class="sxs-lookup"><span data-stu-id="5e13c-114">You cannot test this feature during development.</span></span> <span data-ttu-id="5e13c-115">不支持将应用自定义项旁加载或发布到组织的应用程序目录。</span><span class="sxs-lookup"><span data-stu-id="5e13c-115">App customization is not supported for sideloading or publishing to an organization's app catalog.</span></span>

## <a name="user-considerations"></a><span data-ttu-id="5e13c-116">用户注意事项</span><span class="sxs-lookup"><span data-stu-id="5e13c-116">User considerations</span></span>

<span data-ttu-id="5e13c-117">作为应用发布者，向管理员中的客户提供Teams信息：</span><span class="sxs-lookup"><span data-stu-id="5e13c-117">As the app publisher, provide the following information to customers in Teams admins:</span></span>
* <span data-ttu-id="5e13c-118">包括一条注释，建议在测试租户中测试Teams更改，然后再更改其生产环境。</span><span class="sxs-lookup"><span data-stu-id="5e13c-118">Include a note recommending to test customization changes in a Teams test tenant before making changes in their production environment.</span></span> 
* <span data-ttu-id="5e13c-119">提供如何自定义应用的最佳方案。</span><span class="sxs-lookup"><span data-stu-id="5e13c-119">Provide best practices for how to customize your app.</span></span>

## <a name="see-also"></a><span data-ttu-id="5e13c-120">另请参阅</span><span class="sxs-lookup"><span data-stu-id="5e13c-120">See also</span></span>

* [<span data-ttu-id="5e13c-121">在管理中心Teams应用</span><span class="sxs-lookup"><span data-stu-id="5e13c-121">Customize apps in the Teams admin center</span></span>](/MicrosoftTeams/customize-apps)
