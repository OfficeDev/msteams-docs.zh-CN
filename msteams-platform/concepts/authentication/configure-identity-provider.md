---
title: 配置 OAuth 2.0 标识提供程序
description: 介绍如何以 Azure AD 为焦点配置标识提供程序
ms.topic: how-to
localization_priority: Normal
keywords: teams 身份验证 AAD oauth 标识提供程序
ms.openlocfilehash: ffcf376ea6c4f1a94d797413af22af867dbd5b53
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020854"
---
# <a name="configure-identity-providers"></a><span data-ttu-id="663fd-104">配置标识提供程序</span><span class="sxs-lookup"><span data-stu-id="663fd-104">Configure identity providers</span></span>

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a><span data-ttu-id="663fd-105">配置应用程序以将 Azure Active Directory 用作标识提供程序</span><span class="sxs-lookup"><span data-stu-id="663fd-105">Configuring an application to use Azure Active Directory as an identity provider</span></span>

<span data-ttu-id="663fd-106">支持 OAuth 2.0 的身份提供程序不会对来自未知应用程序的请求进行身份验证;应用程序必须提前注册。</span><span class="sxs-lookup"><span data-stu-id="663fd-106">Identity providers supporting OAuth 2.0 will not authenticate requests from unknown applications; applications must be registered ahead of time.</span></span> <span data-ttu-id="663fd-107">若要使用 Azure AD 完成此操作，请按照以下步骤操作：</span><span class="sxs-lookup"><span data-stu-id="663fd-107">To do this with Azure AD, follow these steps:</span></span>

1. <span data-ttu-id="663fd-108">打开 [应用程序注册门户](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)。</span><span class="sxs-lookup"><span data-stu-id="663fd-108">Open the [Application Registration Portal](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).</span></span>

2. <span data-ttu-id="663fd-109">选择你的应用以查看其属性，或单击"新建注册"按钮。</span><span class="sxs-lookup"><span data-stu-id="663fd-109">Select your app to view its properties, or click the "New Registration" button.</span></span> <span data-ttu-id="663fd-110">查找 **应用的重定向 URI** 部分。</span><span class="sxs-lookup"><span data-stu-id="663fd-110">Find the **Redirect URI** section for the app.</span></span>

3. <span data-ttu-id="663fd-111">在下拉菜单中，确保 **已选择"Web"。**</span><span class="sxs-lookup"><span data-stu-id="663fd-111">In the dropdown menu, make sure **Web** is selected.</span></span> <span data-ttu-id="663fd-112">将 URL 更新到身份验证终结点。</span><span class="sxs-lookup"><span data-stu-id="663fd-112">Update the URL to your authentication endpoint.</span></span> <span data-ttu-id="663fd-113">对于 GitHub 上的 TypeScript/Node.js 和 C# 示例应用，重定向 URL 将类似于：</span><span class="sxs-lookup"><span data-stu-id="663fd-113">For the TypeScript/Node.js and C# sample apps on GitHub, the redirect URLs will be similar to this:</span></span>

    <span data-ttu-id="663fd-114">重定向 URL： `https://<hostname>/bot-auth/simple-start`</span><span class="sxs-lookup"><span data-stu-id="663fd-114">Redirect URLs: `https://<hostname>/bot-auth/simple-start`</span></span>

<span data-ttu-id="663fd-115">将 `<hostname>` 替换为实际主机。</span><span class="sxs-lookup"><span data-stu-id="663fd-115">Replace `<hostname>` with your actual host.</span></span> <span data-ttu-id="663fd-116">这可能是专用托管站点，如 Azure、Glitch 或开发计算机上 localhost 的 ngrok 隧道（如 `abcd1234.ngrok.io` ）。</span><span class="sxs-lookup"><span data-stu-id="663fd-116">This might be a dedicated hosting site such as Azure, Glitch, or an ngrok tunnel to localhost on your development machine such as `abcd1234.ngrok.io`.</span></span> <span data-ttu-id="663fd-117">如果你尚未完成或托管应用 (或上面提到的) 示例应用，可能还没有此信息，但当该信息已知时，你始终可以返回到此页面。</span><span class="sxs-lookup"><span data-stu-id="663fd-117">You may not have this information yet if you have not completed or hosted your app (or the sample app mentioned above), but you can always return to this page when that information is known.</span></span>

## <a name="other-authentication-providers"></a><span data-ttu-id="663fd-118">其他身份验证提供程序</span><span class="sxs-lookup"><span data-stu-id="663fd-118">Other authentication providers</span></span>

* <span data-ttu-id="663fd-119">**LinkedIn** 按照配置 [LinkedIn 应用程序中的说明操作](/linkedin/talent/apply-with-linkedin)</span><span class="sxs-lookup"><span data-stu-id="663fd-119">**LinkedIn** Follow the instructions in [Configuring your LinkedIn application](/linkedin/talent/apply-with-linkedin)</span></span>

* <span data-ttu-id="663fd-120">**Google** 从 Google API 控制台获取 OAuth 2.0 [客户端凭据](https://console.developers.google.com/)</span><span class="sxs-lookup"><span data-stu-id="663fd-120">**Google** Obtain OAuth 2.0 client credentials from the [Google API Console](https://console.developers.google.com/)</span></span>
