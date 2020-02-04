---
title: 发布发布
description: 发布应用程序后要执行的操作
keywords: 团队发布更新证书
ms.openlocfilehash: 05e4ea47bbf81967ccf086230bf0ad8c633f6e0b
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673090"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="a6308-104">维护和支持您发布的应用程序</span><span class="sxs-lookup"><span data-stu-id="a6308-104">Maintain and support your published app</span></span> 

<span data-ttu-id="a6308-105">在应用程序获得批准并在公用应用程序目录中列出后，可以通过实现应用程序证书或添加网站的 "下载" 按钮来增加您的访问范围。</span><span class="sxs-lookup"><span data-stu-id="a6308-105">After your app is approved and listed in the public app catalog, you can increase your reach by achieving app certification, or adding a download button your website.</span></span>

## <a name="application-certificate"></a><span data-ttu-id="a6308-106">应用程序证书</span><span class="sxs-lookup"><span data-stu-id="a6308-106">Application Certificate</span></span>

<span data-ttu-id="a6308-107">Microsoft 提供了[应用程序认证计划](./application-certification.md)，用于编译应用程序信息，并将其呈现在[Microsoft 团队应用程序安全性和合规性页面](https://aka.ms/AppCertification)上。</span><span class="sxs-lookup"><span data-stu-id="a6308-107">Microsoft provides a [Application Certification program](./application-certification.md) that compiles your app information and presents it on [Microsoft Teams App Security and Compliance Page](https://aka.ms/AppCertification).</span></span> <span data-ttu-id="a6308-108">此信息旨在帮助管理员选择对其组织而言是安全的应用程序。</span><span class="sxs-lookup"><span data-stu-id="a6308-108">This information is intended to help admins to choose apps that are safe for their organizations.</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="a6308-109">将 "下载" 按钮添加到产品网站</span><span class="sxs-lookup"><span data-stu-id="a6308-109">Add a download button to your product site</span></span>

<span data-ttu-id="a6308-110">如果您的应用程序位于 Microsoft 团队存储中，则可以为您的网站生成一个链接，用于启动团队并显示用户添加应用程序的许可和安装对话框。</span><span class="sxs-lookup"><span data-stu-id="a6308-110">If your app is in the Microsoft Teams store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="a6308-111">格式为： `https://teams.microsoft.com/l/app/<appId>`其中 appID 是它们在提交的清单中声明的 GUID。</span><span class="sxs-lookup"><span data-stu-id="a6308-111">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="a6308-112">示例： `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd`是用于安装 Trello 的链接。</span><span class="sxs-lookup"><span data-stu-id="a6308-112">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="a6308-113">更新现有团队应用程序</span><span class="sxs-lookup"><span data-stu-id="a6308-113">Updating your existing Teams app</span></span>

* <span data-ttu-id="a6308-114">请勿使用 "*添加新应用*" 按钮重新提交您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="a6308-114">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="a6308-115">改为对 "概述" 选项卡上的应用程序使用磁贴。</span><span class="sxs-lookup"><span data-stu-id="a6308-115">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="a6308-116">更新后的清单中的 appId 应与当前清单中的 appId 相同，并增加了版本号。</span><span class="sxs-lookup"><span data-stu-id="a6308-116">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="a6308-117">在清单中增加版本号。</span><span class="sxs-lookup"><span data-stu-id="a6308-117">Increment your version number in your manifest.</span></span>

### <a name="when-does-updating-your-app-trigger-the-user-consent-flow"></a><span data-ttu-id="a6308-118">何时更新应用程序触发用户同意流？</span><span class="sxs-lookup"><span data-stu-id="a6308-118">When does updating your app trigger the user consent flow?</span></span>

<span data-ttu-id="a6308-119">当用户安装您的应用程序时，他们所做的第一件事是同意授予应用程序访问应用程序执行其工作所需的服务和信息的权限。</span><span class="sxs-lookup"><span data-stu-id="a6308-119">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="a6308-120">当您更新您的应用程序时，可能会重新触发此同意行为，尤其是在您进行了以下一个或多个更改时：</span><span class="sxs-lookup"><span data-stu-id="a6308-120">When you update your app, that can re-trigger this consent behavior, particularly if you have made one or more of the following changes:</span></span>

* <span data-ttu-id="a6308-121">将新功能添加到应用程序，例如仅将 bot 添加到仅选项卡应用程序中。</span><span class="sxs-lookup"><span data-stu-id="a6308-121">Adding a new capability to an app such as adding a bot to an tab only app.</span></span>
* <span data-ttu-id="a6308-122">更改清单中的权限数组。</span><span class="sxs-lookup"><span data-stu-id="a6308-122">Changing the permissions array in the manifest.</span></span>
* <span data-ttu-id="a6308-123">在清单中增加您的应用程序版本号。</span><span class="sxs-lookup"><span data-stu-id="a6308-123">Increment your app version number in your manifest.</span></span>
