---
title: 提示和频繁失败的情况
description: 描述提交和大多数失败策略的提示
author: laujan
ms.author: lajanuar
ms.topic: how to
ms.openlocfilehash: 52225bd082059430a9804cf8fb225ac539781b33
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "43914572"
---
# <a name="tips-for-a-successful-app-submission"></a><span data-ttu-id="1836c-103">成功提交应用程序的提示</span><span class="sxs-lookup"><span data-stu-id="1836c-103">Tips for a successful app submission</span></span>

<span data-ttu-id="1836c-104">本文解决了提交的应用程序验证失败的常见原因。</span><span class="sxs-lookup"><span data-stu-id="1836c-104">This article addresses common reasons submitted apps fail validation.</span></span> <span data-ttu-id="1836c-105">尽管它并不是您的应用程序的所有潜在问题的详尽列表，但遵循本指南将增加您的应用程序提交第一次的可能性。</span><span class="sxs-lookup"><span data-stu-id="1836c-105">While it's not intended to be an exhaustive list of all potential issues with your app, following this guide will increase the likelihood that your app submission will pass the first time.</span></span> <span data-ttu-id="1836c-106">有关验证策略的详细列表，*请参阅*[商业市场认证策略](/legal/marketplace/certification-policies)。</span><span class="sxs-lookup"><span data-stu-id="1836c-106">*See* [Commercial marketplace certification policies](/legal/marketplace/certification-policies) for an extensive list of validation policies.</span></span>

>[!NOTE]
><span data-ttu-id="1836c-107">**[1140 节](/legal/marketplace/certification-policies#1140-teams)** 是专门针对团队应用程序的 Microsoft 团队和**[子节 1140.4](https://docs.microsoft.com/legal/marketplace/certification-policies#11404-functionality)** 解决功能要求的。</span><span class="sxs-lookup"><span data-stu-id="1836c-107">**[Section 1140](/legal/marketplace/certification-policies#1140-teams)** is specific to Microsoft Teams and **[sub-section 1140.4](https://docs.microsoft.com/legal/marketplace/certification-policies#11404-functionality)** addresses functionality requirements for Teams apps.</span></span>

## <a name="validation-guidelines"></a><span data-ttu-id="1836c-108">验证准则</span><span class="sxs-lookup"><span data-stu-id="1836c-108">Validation guidelines</span></span>

### <a name="9989-general-considerations"></a><span data-ttu-id="1836c-109">&#9989; 常规注意事项</span><span class="sxs-lookup"><span data-stu-id="1836c-109">&#9989; General considerations</span></span>

<span data-ttu-id="1836c-110">另*请参阅* [Section 100 —常规](/legal/marketplace/certification-policies#100-general)</span><span class="sxs-lookup"><span data-stu-id="1836c-110">*See also* [Section 100 — General](/legal/marketplace/certification-policies#100-general)</span></span>

* <span data-ttu-id="1836c-111">确保使用的是版本1.4.1 或更高版本的[Microsoft 团队 SDK](https://www.npmjs.com/package/@microsoft/teams-js)。</span><span class="sxs-lookup"><span data-stu-id="1836c-111">Ensure you are using version 1.4.1 or later of the [Microsoft Teams SDK](https://www.npmjs.com/package/@microsoft/teams-js).</span></span>
* <span data-ttu-id="1836c-112">在验证过程正在进行时，请勿对应用进行更改。</span><span class="sxs-lookup"><span data-stu-id="1836c-112">Don't make changes to your app while the validation process is in progress.</span></span> <span data-ttu-id="1836c-113">执行此操作将需要对应用进行完全重新验证。</span><span class="sxs-lookup"><span data-stu-id="1836c-113">Doing so will require a complete revalidation of your app.</span></span>
* <span data-ttu-id="1836c-114">您的应用程序不得停止响应、意外终止或包含编程错误。</span><span class="sxs-lookup"><span data-stu-id="1836c-114">Your app  must not stop responding, end unexpectedly, or contain programming errors.</span></span> <span data-ttu-id="1836c-115">如果遇到问题，您的应用程序应正常失败，并向用户提供有效的单向转发邮件。</span><span class="sxs-lookup"><span data-stu-id="1836c-115">If an issue is encountered, your app should fail gracefully and provide a valid-way-forward message to the user.</span></span>
* <span data-ttu-id="1836c-116">您的应用程序不得在用户环境中自动下载、安装或启动任何可执行代码。</span><span class="sxs-lookup"><span data-stu-id="1836c-116">Your app must not automatically download, install, or launch any executable code in the user environment.</span></span> <span data-ttu-id="1836c-117">所有下载都应从用户处寻求显式权限。</span><span class="sxs-lookup"><span data-stu-id="1836c-117">All downloads should seek explicit permission from the user.</span></span>
* <span data-ttu-id="1836c-118">与您的体验相关联的任何材料（如说明和支持文档）都必须是准确的。</span><span class="sxs-lookup"><span data-stu-id="1836c-118">Any material that you associate with your experience, such as descriptions and support documentation, must be accurate.</span></span> <span data-ttu-id="1836c-119">在您的说明和材料中，使用正确的拼写、大小写、标点符号和语法。</span><span class="sxs-lookup"><span data-stu-id="1836c-119">Use correct spelling, capitalization, punctuation, and grammar in your descriptions and materials.</span></span>
* <span data-ttu-id="1836c-120">提供帮助和支持信息。</span><span class="sxs-lookup"><span data-stu-id="1836c-120">Provide help and support information.</span></span> <span data-ttu-id="1836c-121">强烈建议您的应用程序包括首次运行的用户体验的帮助/常见问题解答链接。</span><span class="sxs-lookup"><span data-stu-id="1836c-121">It's highly recommended that your app include a help/FAQ link for the first-run user experience.</span></span> <span data-ttu-id="1836c-122">对于所有个人应用程序，我们建议将 "帮助" 页作为 "个人" 选项卡提供，以获得更好的用户体验。</span><span class="sxs-lookup"><span data-stu-id="1836c-122">For all personal apps, we recommend providing your help page as a personal tab for a better user experience.</span></span>
* <span data-ttu-id="1836c-123">如果对提交进行任何清单更改，请增加清单中的应用版本号。</span><span class="sxs-lookup"><span data-stu-id="1836c-123">Increment your app version number in the manifest if you make any manifest changes to your submission.</span></span>

### <a name="9989--provide-a-clear-and-simple-sign-insign-out-and-sign-up-experience"></a><span data-ttu-id="1836c-124">&#9989; 提供清晰且简单的登录/注销和注册体验</span><span class="sxs-lookup"><span data-stu-id="1836c-124">&#9989;  Provide a clear and simple sign in/sign out and sign-up experience</span></span>

<span data-ttu-id="1836c-125">另*请参阅* [Section 1100.5-客户控制](/legal/marketplace/certification-policies#11005-customer-control)</span><span class="sxs-lookup"><span data-stu-id="1836c-125">*See also* [Section 1100.5 — Customer control](/legal/marketplace/certification-policies#11005-customer-control)</span></span>

* <span data-ttu-id="1836c-126">如果您的应用程序或外接程序依赖于外部帐户或服务，则登录/注销和注册体验必须在应用程序中的所有功能上都显而易见且可访问。</span><span class="sxs-lookup"><span data-stu-id="1836c-126">If your app or add-in depends on external accounts or services, the sign in/sign out and sign-up experience must be apparent and reachable across all capabilities in your app.</span></span>
* <span data-ttu-id="1836c-127">如果向用户提供了显式登录选项，则必须有对应的注销选项（即使该应用程序使用的是 SSO/[缄默身份验证](~/tabs/how-to/authentication/auth-silent-aad.md)）也是如此。</span><span class="sxs-lookup"><span data-stu-id="1836c-127">If there is an explicit sign-in option provided to the user, there must be a corresponding sign-out option (even if the app is using SSO/[silent authentication](~/tabs/how-to/authentication/auth-silent-aad.md)).</span></span>
* <span data-ttu-id="1836c-128">注销选项必须仅将用户从应用程序功能中注销，而不能从团队客户端注销。</span><span class="sxs-lookup"><span data-stu-id="1836c-128">The sign-out option must only sign the user out of your app's capability and not out of the Teams client.</span></span>
* <span data-ttu-id="1836c-129">注销选项至少必须使用与登录选项相同的功能对用户进行签名即可。</span><span class="sxs-lookup"><span data-stu-id="1836c-129">At a minimum, the sign-out option must sign the user out of the same capabilities accessed with the sign-in option.</span></span> <span data-ttu-id="1836c-130">例如，如果登录选项同时包含邮件扩展和选项卡，则注销选项必须包括邮件扩展和选项卡。</span><span class="sxs-lookup"><span data-stu-id="1836c-130">For example, if the sign-in option includes both a messaging extension and tab, then the sign-out option must include both the messaging extension and tab.</span></span>

* <span data-ttu-id="1836c-131">确保始终有一种方法来撤消以下（或类似）行为：</span><span class="sxs-lookup"><span data-stu-id="1836c-131">Make sure there is always a way to reverse the following (or similar) behaviors:</span></span>
  * <span data-ttu-id="1836c-132">登录 => 注销。</span><span class="sxs-lookup"><span data-stu-id="1836c-132">Sign-in => sign-out.</span></span>
  * <span data-ttu-id="1836c-133">链接帐户/服务 => 取消链接帐户/服务。</span><span class="sxs-lookup"><span data-stu-id="1836c-133">Link an account/service => unlink an account/service.</span></span>
  * <span data-ttu-id="1836c-134">连接帐户/服务 => 断开帐户/服务的连接。</span><span class="sxs-lookup"><span data-stu-id="1836c-134">Connect an account/service => disconnect an account/service.</span></span>
  * <span data-ttu-id="1836c-135">授权帐户/服务 => deauthorize/拒绝帐户/服务。</span><span class="sxs-lookup"><span data-stu-id="1836c-135">Authorize an account/service => deauthorize/deny an account/service.</span></span>
  * <span data-ttu-id="1836c-136">注册帐户/服务 => 取消注册/取消订阅帐户/服务。</span><span class="sxs-lookup"><span data-stu-id="1836c-136">Register an account/service => unregister/unsubscribe an account/service.</span></span>
* <span data-ttu-id="1836c-137">如果您的应用程序需要帐户或服务，则必须为用户提供注册或创建注册请求的方法。</span><span class="sxs-lookup"><span data-stu-id="1836c-137">If your app requires an account or service, you must provide a way for the user to sign up or to create a sign-up request.</span></span> <span data-ttu-id="1836c-138">如果您的应用程序是企业应用程序，则可以授予异常。</span><span class="sxs-lookup"><span data-stu-id="1836c-138">An exception may be granted if your app is an Enterprise application.</span></span>
* <span data-ttu-id="1836c-139">登录/注销功能必须在移动客户端上工作。</span><span class="sxs-lookup"><span data-stu-id="1836c-139">Sign in/sign out functionality must work on mobile clients.</span></span> <span data-ttu-id="1836c-140">确保使用的是[Microsoft 团队 SDK](https://www.npmjs.com/package/@microsoft/teams-js)版本1.4.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="1836c-140">Ensure you're using the [Microsoft Teams SDK](https://www.npmjs.com/package/@microsoft/teams-js) version 1.4.1 or later.</span></span>

<span data-ttu-id="1836c-141">有关身份验证的其他信息，请参阅：</span><span class="sxs-lookup"><span data-stu-id="1836c-141">For additional information on authentication see:</span></span>

* [<span data-ttu-id="1836c-142">身份验证文档</span><span class="sxs-lookup"><span data-stu-id="1836c-142">Authentication documentation</span></span>](../../../authentication/authentication.md)
* [<span data-ttu-id="1836c-143">节点中的 Bot 身份验证示例</span><span class="sxs-lookup"><span data-stu-id="1836c-143">Bot authentication sample in Node</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
* [<span data-ttu-id="1836c-144">节点中的 Tab 身份验证示例</span><span class="sxs-lookup"><span data-stu-id="1836c-144">Tab authentication sample in Node</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)
* [<span data-ttu-id="1836c-145">C #/.NET 中的选项卡/机器人身份验证</span><span class="sxs-lookup"><span data-stu-id="1836c-145">Tab/bot authentication in C#/.NET</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)

### <a name="9989-response-times-must-be-reasonable"></a><span data-ttu-id="1836c-146">&#9989; 响应时间必须合理</span><span class="sxs-lookup"><span data-stu-id="1836c-146">&#9989; Response times must be reasonable</span></span>

* <span data-ttu-id="1836c-147">**选项卡**。</span><span class="sxs-lookup"><span data-stu-id="1836c-147">**Tabs**.</span></span> <span data-ttu-id="1836c-148">如果对操作的响应需要的时间超过三秒，则必须提供加载消息或警告。</span><span class="sxs-lookup"><span data-stu-id="1836c-148">If a response to an action takes more than three seconds, you must provide a loading message or warning.</span></span>
* <span data-ttu-id="1836c-149">**Bot**。</span><span class="sxs-lookup"><span data-stu-id="1836c-149">**Bots**.</span></span> <span data-ttu-id="1836c-150">对用户命令的响应必须在两秒内发生。</span><span class="sxs-lookup"><span data-stu-id="1836c-150">A response to a user command must occur within two seconds.</span></span> <span data-ttu-id="1836c-151">如果需要更长的处理，应用程序必须显示键入指示器。</span><span class="sxs-lookup"><span data-stu-id="1836c-151">If longer processing is required, your app must display a typing indicator.</span></span>
* <span data-ttu-id="1836c-152">**撰写扩展**。</span><span class="sxs-lookup"><span data-stu-id="1836c-152">**Compose extensions**.</span></span> <span data-ttu-id="1836c-153">对用户命令的响应必须在5秒内发生。</span><span class="sxs-lookup"><span data-stu-id="1836c-153">A response to a user command must occur within five seconds.</span></span>

> [!TIP]
> <span data-ttu-id="1836c-154">确保您的应用程序在您的应用程序需要响应的时间过长时显示加载指示器或某种形式的警告。</span><span class="sxs-lookup"><span data-stu-id="1836c-154">Make sure your app displays a loading indicator or some form of warning when your app is taking longer than expected to respond.</span></span>

### <a name="9989-tab-content-should-not-have-excessive-chrome-or-layered-navigation"></a><span data-ttu-id="1836c-155">&#9989; 选项卡内容不应具有过多的 chrome 或分层导航</span><span class="sxs-lookup"><span data-stu-id="1836c-155">&#9989; Tab content should not have excessive chrome or layered navigation</span></span>

* <span data-ttu-id="1836c-156">选项卡应提供重点内容并避免不必要的 UI 元素。</span><span class="sxs-lookup"><span data-stu-id="1836c-156">Tabs should provide focused content and avoid needless UI elements.</span></span> <span data-ttu-id="1836c-157">通常，这通常是指不必要的嵌套/分层导航，内容旁边的无关或不相关的 UI，或任何使用户不相关内容的链接。</span><span class="sxs-lookup"><span data-stu-id="1836c-157">In general, this usually refers to unnecessary nested/layered navigation, an extraneous or irrelevant UI next to the content, or any links that take the user to unrelated content.</span></span> <span data-ttu-id="1836c-158">例如，下面是一个选项卡视图，它省略了导航菜单，仅展示了主要内容：</span><span class="sxs-lookup"><span data-stu-id="1836c-158">For example, below is a tab view that omits navigation menus and only showcases the main content:</span></span>

<span data-ttu-id="1836c-159">![Sharepoint web 视图](~/assets/images/faq/web-sp.png)
![SharePoint 选项卡视图](~/assets/images/faq/tab-sp.png)</span><span class="sxs-lookup"><span data-stu-id="1836c-159">![SharePoint web view](~/assets/images/faq/web-sp.png)
![SharePoint tab view](~/assets/images/faq/tab-sp.png)</span></span>

* <span data-ttu-id="1836c-160">如果有多个视图选项，请考虑具有一个选项卡配置菜单供用户选择。</span><span class="sxs-lookup"><span data-stu-id="1836c-160">If there are multiple view options, consider having a tab config menu for the user to choose from.</span></span> <span data-ttu-id="1836c-161">例如，将菜单放在 "配置" 页中，以使实际的选项卡视图干净且具有焦点，而不是在选项卡中嵌入菜单。</span><span class="sxs-lookup"><span data-stu-id="1836c-161">For example, instead of embedding a menu inside the tab, put the menu in the configuration page so the actual tab view is clean and focused.</span></span>

!["广域观点配置" 页](~/assets/images/faq/wideidea.png)

### <a name="9989-tab-configuration-must-happen-in-the-configuration-screen"></a><span data-ttu-id="1836c-163">"&#9989;" 选项卡配置必须出现在 "配置" 屏幕中</span><span class="sxs-lookup"><span data-stu-id="1836c-163">&#9989; Tab configuration must happen in the configuration screen</span></span>

* <span data-ttu-id="1836c-164">配置屏幕应清楚地说明体验的价值以及如何配置选项卡。</span><span class="sxs-lookup"><span data-stu-id="1836c-164">The configuration screen should clearly explain the value of the experience and how to configure the tab.</span></span>
* <span data-ttu-id="1836c-165">配置过程不应终止用户体验，并始终为用户提供一种继续操作的方法。</span><span class="sxs-lookup"><span data-stu-id="1836c-165">The configuration process should not dead-end the user experience and always provide a way for users to continue.</span></span>
* <span data-ttu-id="1836c-166">即使用户无法立即找到要查找的内容，用户也应始终能够完成配置体验。</span><span class="sxs-lookup"><span data-stu-id="1836c-166">A user should always be able to finish the configuration experience, even if they can’t immediately find the content they’re looking for.</span></span>
* <span data-ttu-id="1836c-167">配置体验应为用户提供用于查找其内容、固定 URL 或创建新内容（如果不存在）的选项。</span><span class="sxs-lookup"><span data-stu-id="1836c-167">The configuration experience should provide options for the user to find their content, pin a URL, or create new content if it doesn’t exist.</span></span>
* <span data-ttu-id="1836c-168">用户不必保留配置体验即可创建内容，然后再返回到团队进行固定。</span><span class="sxs-lookup"><span data-stu-id="1836c-168">The user shouldn’t have to leave the configuration experience to create content and then come back to Teams to pin it.</span></span>

![OneNote 允许用户在无法找到案例备注时粘贴 OneNote 链接](~/assets/images/faq/tab-onenote-config.png)

![用户始终可以在规划器上创建新计划，以防不存在现有计划](~/assets/images/faq/tab-planner-config.png)

![SharePoint 还允许用户直接粘贴 SharePoint 链接](~/assets/images/faq/tab-sp-config.png)

### <a name="9989-bots-must-always-be-responsive-and-fail-gracefully"></a><span data-ttu-id="1836c-172">&#9989; Bot 必须始终响应并正常进行故障切换</span><span class="sxs-lookup"><span data-stu-id="1836c-172">&#9989; Bots must always be responsive and fail gracefully</span></span>

<span data-ttu-id="1836c-173">你的 bot 应响应任何命令，而不是用户的终止。</span><span class="sxs-lookup"><span data-stu-id="1836c-173">Your bot should be responsive to any command and not dead-end the user.</span></span> <span data-ttu-id="1836c-174">下面的一些提示可帮助你的机器人智能地对用户做出响应：</span><span class="sxs-lookup"><span data-stu-id="1836c-174">Here are some tips to help your bot intelligently respond to users:</span></span>

* <span data-ttu-id="1836c-175">**使用命令列表**。</span><span class="sxs-lookup"><span data-stu-id="1836c-175">**Use command lists**.</span></span> <span data-ttu-id="1836c-176">分析用户输入或预测用户意图非常困难。</span><span class="sxs-lookup"><span data-stu-id="1836c-176">Analyzing user input or predicting user intent is hard.</span></span> <span data-ttu-id="1836c-177">而不是让用户猜出你的 bot 可以执行的操作，而是提供你的 bot 理解的命令列表。</span><span class="sxs-lookup"><span data-stu-id="1836c-177">Instead of letting users guess what your bot can do, provide a list of commands your bot understands.</span></span>

![流命令列表](~/assets/images/faq/flow-bot.png)

* <span data-ttu-id="1836c-179">**包含 "帮助" 命令**。</span><span class="sxs-lookup"><span data-stu-id="1836c-179">**Include a help command**.</span></span> <span data-ttu-id="1836c-180">用户在丢失时或者在你的 bot 未按预期响应时，可能会键入 "帮助"。</span><span class="sxs-lookup"><span data-stu-id="1836c-180">Users are likely to type "Help" when they are lost or when your bot doesn't respond as expected.</span></span> <span data-ttu-id="1836c-181">包含一个帮助命令，该命令描述应用程序的值将如何与所有有效命令一起使用。</span><span class="sxs-lookup"><span data-stu-id="1836c-181">Include a help command that describes how your app's value will be experienced along with all valid commands.</span></span>

![流帮助命令](~/assets/images/faq/flow-help.png)

* <span data-ttu-id="1836c-183">**在你的 bot 丢失时包括帮助内容或指南**。</span><span class="sxs-lookup"><span data-stu-id="1836c-183">**Include help content or guidance when your bot is lost**.</span></span> <span data-ttu-id="1836c-184">当你的 bot 无法识别用户输入时，它应建议另一个操作。</span><span class="sxs-lookup"><span data-stu-id="1836c-184">When your bot can't understand the user input, it should suggest an alternative action.</span></span> <span data-ttu-id="1836c-185">例如， *"我很抱歉，我不理解。有关详细信息，请键入 "help"。*</span><span class="sxs-lookup"><span data-stu-id="1836c-185">For example, *"I'm sorry, I don't understand. Type "help" for more information."*</span></span> <span data-ttu-id="1836c-186">不要使用错误消息进行响应，也不要简单说出 *"我不知道"*。</span><span class="sxs-lookup"><span data-stu-id="1836c-186">Don't respond with an error message or simply, *"I don't understand"*.</span></span> <span data-ttu-id="1836c-187">使用此机会讲授你的用户。</span><span class="sxs-lookup"><span data-stu-id="1836c-187">Use this chance to teach your users.</span></span>

* <span data-ttu-id="1836c-188">请**考虑所有作用域**。</span><span class="sxs-lookup"><span data-stu-id="1836c-188">**Think through all scopes**.</span></span> <span data-ttu-id="1836c-189">在频道和个人对话中提到（`@*botname*`）时，请确保你的 bot 提供了适当的响应。</span><span class="sxs-lookup"><span data-stu-id="1836c-189">Be sure that your bot provides appropriate responses when mentioned (`@*botname*`) in a channel and in personal conversations.</span></span> <span data-ttu-id="1836c-190">如果你的 bot 未在个人或团队作用域内提供有意义的上下文，请通过清单禁用该作用域。</span><span class="sxs-lookup"><span data-stu-id="1836c-190">If your bot does not provide meaningful context within the personal or teams scope, disable that scope via the manifest.</span></span> <span data-ttu-id="1836c-191">（请参阅`bots` [Microsoft 团队清单架构参考](~/resources/schema/manifest-schema.md#bots)中的 "阻止"。）</span><span class="sxs-lookup"><span data-stu-id="1836c-191">(See the `bots` block in the [Microsoft Teams manifest schema reference](~/resources/schema/manifest-schema.md#bots).)</span></span>

### <a name="9989-bots-must-send-a-welcome-message-on-first-launch"></a><span data-ttu-id="1836c-192">&#9989; Bot 必须在首次启动时发送欢迎消息</span><span class="sxs-lookup"><span data-stu-id="1836c-192">&#9989; Bots must send a welcome message on first launch</span></span>

<span data-ttu-id="1836c-193">欢迎邮件是设置你的 bot 语气的最佳方式。</span><span class="sxs-lookup"><span data-stu-id="1836c-193">Welcome messages are the best way to set your bot's tone.</span></span> <span data-ttu-id="1836c-194">这是用户与 bot 的第一个交互操作。</span><span class="sxs-lookup"><span data-stu-id="1836c-194">This is the first interaction a user has with the bot.</span></span> <span data-ttu-id="1836c-195">最好的欢迎消息可以鼓励用户继续浏览应用。</span><span class="sxs-lookup"><span data-stu-id="1836c-195">A good welcome message can encourage the user to keep exploring the app.</span></span> <span data-ttu-id="1836c-196">如果欢迎或介绍性邮件令人困惑或不清楚，用户将不会立即看到应用程序的价值，也不会失去兴趣。</span><span class="sxs-lookup"><span data-stu-id="1836c-196">If the welcome or introductory message is confusing or unclear, users won't see the value of the app immediately and lose interests.</span></span> <span data-ttu-id="1836c-197">欢迎消息必须包含以下内容：</span><span class="sxs-lookup"><span data-stu-id="1836c-197">The welcome message must include the following:</span></span>

* <span data-ttu-id="1836c-198">帮助命令。</span><span class="sxs-lookup"><span data-stu-id="1836c-198">A help command.</span></span>
* <span data-ttu-id="1836c-199">价值主张</span><span class="sxs-lookup"><span data-stu-id="1836c-199">The value proposition</span></span>
* <span data-ttu-id="1836c-200">所有有效命令。</span><span class="sxs-lookup"><span data-stu-id="1836c-200">All valid commands.</span></span>

<span data-ttu-id="1836c-201">在设计欢迎消息时，需要注意以下几点：</span><span class="sxs-lookup"><span data-stu-id="1836c-201">Here are a few considerations when designing your welcome message:</span></span>

#### <a name="personal-scope"></a><span data-ttu-id="1836c-202">个人作用域</span><span class="sxs-lookup"><span data-stu-id="1836c-202">Personal Scope</span></span>

* <span data-ttu-id="1836c-203">**使您的邮件简洁和提供信息**。</span><span class="sxs-lookup"><span data-stu-id="1836c-203">**Make your message concise and informative**.</span></span> <span data-ttu-id="1836c-204">大多数情况下，用户对你的应用的体验和了解可能会有所不同。</span><span class="sxs-lookup"><span data-stu-id="1836c-204">Most likely, users' experiences with and knowledge of your app will vary.</span></span> <span data-ttu-id="1836c-205">他们可能在其他平台上使用过您的应用程序，或者对您的应用程序一无所知。</span><span class="sxs-lookup"><span data-stu-id="1836c-205">They might have used your app on another platform or know nothing about your app.</span></span> <span data-ttu-id="1836c-206">您想要将您的邮件量身定制给所有访问群体，并在几个句子中说明你的 bot 的功能和与之交互的方法。</span><span class="sxs-lookup"><span data-stu-id="1836c-206">You want to tailor your message to all audiences and in a couple sentences explain what your bot does and the ways to interact with it.</span></span> <span data-ttu-id="1836c-207">此外，还应说明应用程序的价值，以及用户将如何使用它。</span><span class="sxs-lookup"><span data-stu-id="1836c-207">You should also explain the value of the app and how the users will benefit from using it.</span></span>
<span data-ttu-id="1836c-208">![Cafe 和 Dinning bot](~/assets/images/faq/cafe-bot.png)</span><span class="sxs-lookup"><span data-stu-id="1836c-208">![Cafe and Dinning bot](~/assets/images/faq/cafe-bot.png)</span></span>

* <span data-ttu-id="1836c-209">**使您的邮件可操作**。</span><span class="sxs-lookup"><span data-stu-id="1836c-209">**Make your message actionable**.</span></span> <span data-ttu-id="1836c-210">请考虑安装您的应用程序后，您希望用户做的第一件事。</span><span class="sxs-lookup"><span data-stu-id="1836c-210">Think about the first thing you want users to do after installing your app.</span></span> <span data-ttu-id="1836c-211">是否有要尝试的酷命令？</span><span class="sxs-lookup"><span data-stu-id="1836c-211">Is there a cool command they should try?</span></span> <span data-ttu-id="1836c-212">是否有其他应知道的启动体验？</span><span class="sxs-lookup"><span data-stu-id="1836c-212">Is there another onboarding experience they should know about?</span></span> <span data-ttu-id="1836c-213">他们是否需要登录？</span><span class="sxs-lookup"><span data-stu-id="1836c-213">Do they need to sign in?</span></span> <span data-ttu-id="1836c-214">可以在自适应卡片上添加操作，也可以提供具体示例，如 *"请尝试 ..."*， *"这是我可以执行的操作 ..."*。</span><span class="sxs-lookup"><span data-stu-id="1836c-214">You can add actions on an adaptive card or provide specific examples such as *“Try asking….”*, *“This is what I can do…”*.</span></span>

#### <a name="team-scope"></a><span data-ttu-id="1836c-215">团队作用域</span><span class="sxs-lookup"><span data-stu-id="1836c-215">Team scope</span></span>

<span data-ttu-id="1836c-216">当 bot 第一次添加到频道时，有些不同。</span><span class="sxs-lookup"><span data-stu-id="1836c-216">Things are a little bit different when the bot is first added to a channel.</span></span> <span data-ttu-id="1836c-217">通常情况下，不应向团队中的每个人发送1:1 邮件，但机器人可以在频道中发送欢迎消息。</span><span class="sxs-lookup"><span data-stu-id="1836c-217">Normally, you shouldn't send a 1:1 message to everyone on the team, but the bot can send a welcome message in the channel.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1836c-218">了解有关团队应用程序审批策略的详细信息</span><span class="sxs-lookup"><span data-stu-id="1836c-218">Learn more about Teams app approval policies</span></span>](/legal/marketplace/certification-policies#1140-teams) 
