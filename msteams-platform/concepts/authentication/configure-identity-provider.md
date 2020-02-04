---
title: 配置 OAuth 2.0 标识提供程序
description: 介绍如何在 Azure AD 上配置标识提供程序和焦点
keywords: 团队身份验证 AAD oauth 标识提供程序
ms.openlocfilehash: 799b0c20cda64456a4610acbdbedf758989bee55
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673377"
---
# <a name="configuring-identity-providers"></a><span data-ttu-id="10ce2-104">配置标识提供程序</span><span class="sxs-lookup"><span data-stu-id="10ce2-104">Configuring identity providers</span></span>

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a><span data-ttu-id="10ce2-105">将应用程序配置为使用 Azure Active Directory 作为标识提供程序</span><span class="sxs-lookup"><span data-stu-id="10ce2-105">Configuring an application to use Azure Active Directory as an identity provider</span></span>

<span data-ttu-id="10ce2-106">支持 OAuth 2.0 的标识提供程序将不会对来自未知应用程序的请求进行身份验证;必须提前注册应用程序。</span><span class="sxs-lookup"><span data-stu-id="10ce2-106">Identity providers supporting OAuth 2.0 will not authenticate requests from unknown applications; applications must be registered ahead of time.</span></span> <span data-ttu-id="10ce2-107">若要在 Azure AD 中执行此操作，请按照以下步骤操作：</span><span class="sxs-lookup"><span data-stu-id="10ce2-107">To do this with Azure AD, follow these steps:</span></span>

1. <span data-ttu-id="10ce2-108">打开 "[应用程序注册门户](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)"。</span><span class="sxs-lookup"><span data-stu-id="10ce2-108">Open the [Application Registration Portal](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).</span></span>

2. <span data-ttu-id="10ce2-109">选择您的应用程序以查看其属性，或单击 "新建注册" 按钮。</span><span class="sxs-lookup"><span data-stu-id="10ce2-109">Select your app to view its properties, or click the "New Registration" button.</span></span> <span data-ttu-id="10ce2-110">查找应用程序的 "**重定向 URI** " 部分。</span><span class="sxs-lookup"><span data-stu-id="10ce2-110">Find the **Redirect URI** section for the app.</span></span>

3. <span data-ttu-id="10ce2-111">在下拉菜单中，确保选择 " **Web** "。</span><span class="sxs-lookup"><span data-stu-id="10ce2-111">In the dropdown menu, make sure **Web** is selected.</span></span> <span data-ttu-id="10ce2-112">更新身份验证终结点的 URL。</span><span class="sxs-lookup"><span data-stu-id="10ce2-112">Update the URL to your authentication endpoint.</span></span> <span data-ttu-id="10ce2-113">对于 GitHub 上的 TypeScript/node.js 和 c # 示例应用程序，重定向 Url 将类似于以下内容：</span><span class="sxs-lookup"><span data-stu-id="10ce2-113">For the TypeScript/Node.js and C# sample apps on GitHub, the redirect URLs will be similar to this:</span></span>

    <span data-ttu-id="10ce2-114">重定向 Url：`https://<hostname>/bot-auth/simple-start`</span><span class="sxs-lookup"><span data-stu-id="10ce2-114">Redirect URLs: `https://<hostname>/bot-auth/simple-start`</span></span>

<span data-ttu-id="10ce2-115">将`<hostname>`替换为实际主机。</span><span class="sxs-lookup"><span data-stu-id="10ce2-115">Replace `<hostname>` with your actual host.</span></span> <span data-ttu-id="10ce2-116">这可能是一个专用的承载网站，如 Azure、问题或与开发计算机上的 localhost （如） `abcd1234.ngrok.io`的 ngrok 隧道。</span><span class="sxs-lookup"><span data-stu-id="10ce2-116">This might be a dedicated hosting site such as Azure, Glitch, or an ngrok tunnel to localhost on your development machine such as `abcd1234.ngrok.io`.</span></span> <span data-ttu-id="10ce2-117">如果尚未完成或托管您的应用程序（或上面提到的示例应用程序），则可能还没有这些信息，但在已知该信息时，您始终可以返回此页面。</span><span class="sxs-lookup"><span data-stu-id="10ce2-117">You may not have this information yet if you have not completed or hosted your app (or the sample app mentioned above), but you can always return to this page when that information is known.</span></span>

## <a name="other-authentication-providers"></a><span data-ttu-id="10ce2-118">其他身份验证提供程序</span><span class="sxs-lookup"><span data-stu-id="10ce2-118">Other authentication providers</span></span>

* <span data-ttu-id="10ce2-119">**LinkedIn**按照[配置 LinkedIn 应用程序](https://developer.linkedin.com/docs/oauth2)中的说明操作</span><span class="sxs-lookup"><span data-stu-id="10ce2-119">**LinkedIn** Follow the instructions in [Configuring your LinkedIn application](https://developer.linkedin.com/docs/oauth2)</span></span>

* <span data-ttu-id="10ce2-120">**Google**从[GOOGLE API 控制台](https://console.developers.google.com/)获取 OAuth 2.0 客户端凭据</span><span class="sxs-lookup"><span data-stu-id="10ce2-120">**Google** Obtain OAuth 2.0 client credentials from the [Google API Console](https://console.developers.google.com/)</span></span>
