---
title: 设计准则参考
description: 介绍设计个人应用程序的指南
keywords: 团队设计准则参考框架个人应用程序
ms.openlocfilehash: f66691234149afa56a6753dd51379c9f2355318e
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/31/2020
ms.locfileid: "44455497"
---
# <a name="personal-apps"></a><span data-ttu-id="e49ab-104">个人应用</span><span class="sxs-lookup"><span data-stu-id="e49ab-104">Personal apps</span></span>

> [!NOTE]
> <span data-ttu-id="e49ab-105">团队中支持对移动客户端上的选项卡的完全支持。</span><span class="sxs-lookup"><span data-stu-id="e49ab-105">Full support for tabs on mobile clients is supported in Teams.</span></span> <span data-ttu-id="e49ab-106">为移动平台创建选项卡时，应遵循[移动电话上的选项卡指南](../../tabs/design/tabs-mobile.md)。</span><span class="sxs-lookup"><span data-stu-id="e49ab-106">You should follow the [guidance for tabs on mobile](../../tabs/design/tabs-mobile.md) when creating tabs for mobile platforms.</span></span>

<span data-ttu-id="e49ab-107">个人应用是具有个人作用域的团队应用程序。</span><span class="sxs-lookup"><span data-stu-id="e49ab-107">A personal app is a Teams application with a personal scope.</span></span>  <span data-ttu-id="e49ab-108">作为应用程序开发人员，您可以选择提供一个侧重于与单个用户的交互的应用程序版本。</span><span class="sxs-lookup"><span data-stu-id="e49ab-108">As an app developer, you have the option to provide a version of your app that focuses on interactions with a single user.</span></span> <span data-ttu-id="e49ab-109">它可以是一个[对话机器人](../../bots/what-are-bots.md)，可与用户或[个人选项卡](../../tabs/what-are-tabs.md)进行一对一对话，以提供内嵌的 web 体验。</span><span class="sxs-lookup"><span data-stu-id="e49ab-109">It can be a [conversational bot](../../bots/what-are-bots.md) to engage in one-to-one conversations with a user or a [personal tab](../../tabs/what-are-tabs.md) providing an embedded web experience.</span></span> <span data-ttu-id="e49ab-110">借助个人应用程序，用户可以在一个位置查看他们选择的内容。</span><span class="sxs-lookup"><span data-stu-id="e49ab-110">Personal apps enable users to view their select content in one place.</span></span> <span data-ttu-id="e49ab-111">在下面的屏幕截图中，Contoso 是个人应用浮出控件中的个人应用程序。</span><span class="sxs-lookup"><span data-stu-id="e49ab-111">In the following screenshot, Contoso is a personal app in the personal app flyout.</span></span>

![应用程序溢出菜单的图像](~/assets/images/Personal-apps-App-flyout.png)

---

## <a name="guidelines"></a><span data-ttu-id="e49ab-113">准则</span><span class="sxs-lookup"><span data-stu-id="e49ab-113">Guidelines</span></span>

<span data-ttu-id="e49ab-114">个人应用程序通常包含以下选项卡：</span><span class="sxs-lookup"><span data-stu-id="e49ab-114">A personal app typically contains the following tabs:</span></span>

### <a name="your-tab"></a><span data-ttu-id="e49ab-115">您的选项卡</span><span class="sxs-lookup"><span data-stu-id="e49ab-115">Your tab</span></span>

<span data-ttu-id="e49ab-116">你的用户将看到其所有内容。</span><span class="sxs-lookup"><span data-stu-id="e49ab-116">This is where your users will see all their stuff.</span></span> <span data-ttu-id="e49ab-117">其个人空间。</span><span class="sxs-lookup"><span data-stu-id="e49ab-117">It's their personal space.</span></span> <span data-ttu-id="e49ab-118">该选项卡可作为列表、网格、列或单个画布进行排列。。最适用于您的应用程序的任何功能。</span><span class="sxs-lookup"><span data-stu-id="e49ab-118">The tab can be arranged as a list, a grid, columns, or a single canvas...whatever works best for your application.</span></span> <span data-ttu-id="e49ab-119">有关设计有效选项卡的其他信息，请参阅：[选项卡设计](../../tabs/design/tabs.md)。</span><span class="sxs-lookup"><span data-stu-id="e49ab-119">For additional information on designing effective tabs see: [Tabs design](../../tabs/design/tabs.md).</span></span>

<span data-ttu-id="e49ab-120">由于此选项卡可以显示来自多个通道的项目，因此每个项目都应显示其自己的团队、频道和选项卡，以便用户可以轻松地查看它的来源。</span><span class="sxs-lookup"><span data-stu-id="e49ab-120">Since this tab can show items from multiple channels, each item should display its own team, channel, and tab so the user can easily see where it originated.</span></span>

!["个人任务" 选项卡](~/assets/images/Personal-apps-MY-tab.png)

### <a name="recent"></a><span data-ttu-id="e49ab-122">最近更新</span><span class="sxs-lookup"><span data-stu-id="e49ab-122">Recent</span></span>

<span data-ttu-id="e49ab-123">"**最近**" 选项卡允许某人浏览最近在您的应用程序中查看过的所有内容。</span><span class="sxs-lookup"><span data-stu-id="e49ab-123">The **Recent** tab lets someone browse everything they've recently viewed in your app.</span></span> <span data-ttu-id="e49ab-124">它按时间顺序列出（从最高到最新）。</span><span class="sxs-lookup"><span data-stu-id="e49ab-124">It's listed in chronological order (from most to least recent).</span></span> <span data-ttu-id="e49ab-125">单击此列表中的某个项目会将该用户导航到该项目的频道和选项卡。</span><span class="sxs-lookup"><span data-stu-id="e49ab-125">Clicking on an item in this list will navigate the user to that item's channel and tab.</span></span>

![最近选项卡](~/assets/images/Personal-apps-Recent-tab.png)

### <a name="all"></a><span data-ttu-id="e49ab-127">所有</span><span class="sxs-lookup"><span data-stu-id="e49ab-127">All</span></span>

<span data-ttu-id="e49ab-128">这是个人组织中的所有选项卡的列表（仍有权访问它们）。</span><span class="sxs-lookup"><span data-stu-id="e49ab-128">This is a list of all your tabs in the person's organization (the ones they have access to, anyway).</span></span> <span data-ttu-id="e49ab-129">换句话说，它在使用应用程序的任何位置显示它们。</span><span class="sxs-lookup"><span data-stu-id="e49ab-129">In other words, it shows them everywhere the app is being used.</span></span> <span data-ttu-id="e49ab-130">与**最近**的选项卡一样，选择列表中的内容会将用户直接带入相关频道和选项卡。</span><span class="sxs-lookup"><span data-stu-id="e49ab-130">As with the **Recent** tab, selecting something in the list will bring the user straight to the relevant channel and tab.</span></span>

### <a name="bot"></a><span data-ttu-id="e49ab-131">Bot</span><span class="sxs-lookup"><span data-stu-id="e49ab-131">Bot</span></span>

<span data-ttu-id="e49ab-132">Bot 不是必需的，但它是直接和私下与用户进行通信的绝佳方式。</span><span class="sxs-lookup"><span data-stu-id="e49ab-132">A bot isn't required, but it's a great way to communicate directly and privately with your users.</span></span> <span data-ttu-id="e49ab-133">通知是个人应用程序中最重要的功能之一，以及通知与直接通信是否更好的方法？</span><span class="sxs-lookup"><span data-stu-id="e49ab-133">Notification is one of the most important functions of a personal app, and what better way to notify than with direct communication?</span></span>

<span data-ttu-id="e49ab-134">Bot 以卡片形式传递邮件，这可以提供特定信息（如通知新内容可用）或广泛的更新（如日常待办情况列表）。</span><span class="sxs-lookup"><span data-stu-id="e49ab-134">Bots deliver messages in the form of cards, which can provide specific information (like an alert that new content is available) or broad updates (like a daily to-do list).</span></span> <span data-ttu-id="e49ab-135">有关设计有效的 bot 的其他信息，请参阅： [Bot 设计](../../bots/design/bots.md)。</span><span class="sxs-lookup"><span data-stu-id="e49ab-135">For additional information on designing effective bots see: [Bot design](../../bots/design/bots.md).</span></span>

![Bot 问候语](~/assets/images/Personal-apps-Bot.png)

### <a name="help-and-settings"></a><span data-ttu-id="e49ab-137">帮助和设置</span><span class="sxs-lookup"><span data-stu-id="e49ab-137">Help and Settings</span></span>

<span data-ttu-id="e49ab-138">帮助内容使用户能够发现您的应用程序的细微差别。</span><span class="sxs-lookup"><span data-stu-id="e49ab-138">Help content enables users to discover the nuances of your app.</span></span> <span data-ttu-id="e49ab-139">添加 "**设置**" 选项卡，让他们可以进一步自定义它。</span><span class="sxs-lookup"><span data-stu-id="e49ab-139">Add a **Settings** tab to give them the ability to further customize it.</span></span>

### <a name="about"></a><span data-ttu-id="e49ab-140">关于</span><span class="sxs-lookup"><span data-stu-id="e49ab-140">About</span></span>

<span data-ttu-id="e49ab-141">包括 "**关于**" 选项卡，以提供版本号码、功能、隐私和权限链接等信息。</span><span class="sxs-lookup"><span data-stu-id="e49ab-141">Include an **About** tab to provide information like version number, capabilities, privacy, and permissions links.</span></span>

## <a name="best-practices"></a><span data-ttu-id="e49ab-142">最佳做法</span><span class="sxs-lookup"><span data-stu-id="e49ab-142">Best practices</span></span>

### <a name="communicate-directly-with-your-users"></a><span data-ttu-id="e49ab-143">直接与您的用户通信</span><span class="sxs-lookup"><span data-stu-id="e49ab-143">Communicate directly with your users</span></span>

<span data-ttu-id="e49ab-144">使用 bot 向用户通知更改和新功能。</span><span class="sxs-lookup"><span data-stu-id="e49ab-144">Use a bot to notify users of changes and new features.</span></span>

### <a name="customize-your-tabs"></a><span data-ttu-id="e49ab-145">自定义选项卡 .。。</span><span class="sxs-lookup"><span data-stu-id="e49ab-145">Customize your tabs...</span></span>

<span data-ttu-id="e49ab-146">你可以随意添加其他选项卡，以帮助你的用户完成特定任务。</span><span class="sxs-lookup"><span data-stu-id="e49ab-146">Feel free to add other tabs that will help your users accomplish specific tasks.</span></span>

### <a name="and-make-them-relevant-to-every-user"></a><span data-ttu-id="e49ab-147">...并使其与每个用户相关</span><span class="sxs-lookup"><span data-stu-id="e49ab-147">...and make them relevant to every user</span></span>

<span data-ttu-id="e49ab-148">您在应用程序清单中声明的每个选项卡将对所有用户可见。</span><span class="sxs-lookup"><span data-stu-id="e49ab-148">Every tab you declare in your app manifest will be visible to all users.</span></span> <span data-ttu-id="e49ab-149">例如，如果您的个人应用程序是由经理和员工使用的费用报告工具，则 "**审批**" 选项卡应提供对这两个角色都有意义的内容。</span><span class="sxs-lookup"><span data-stu-id="e49ab-149">For example, if your personal app is an expense reporting tool that is used by both managers and employees, an **Approval** tab should provide content that is meaningful to both roles.</span></span>
