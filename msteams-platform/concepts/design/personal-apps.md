---
title: 设计准则参考
description: 介绍设计个人应用程序的指南
keywords: 团队设计准则参考框架个人应用程序
ms.openlocfilehash: 6a07b618d78a3ad79850713052c88ef178c1ecc1
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673068"
---
# <a name="personal-apps"></a><span data-ttu-id="56609-104">个人应用程序</span><span class="sxs-lookup"><span data-stu-id="56609-104">Personal apps</span></span>

> [!Important]
> <span data-ttu-id="56609-105">对移动客户端上的选项卡的完全支持即将推出。</span><span class="sxs-lookup"><span data-stu-id="56609-105">Full support for tabs on mobile clients is coming soon.</span></span> <span data-ttu-id="56609-106">若要为此更改做准备，应按照移动选项卡[上的选项卡指南中](~/tabs/design/tabs-mobile.md)的步骤创建选项卡。</span><span class="sxs-lookup"><span data-stu-id="56609-106">To prepare for this change you should follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="56609-107">个人应用（静态选项卡）目前可在[开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中使用。</span><span class="sxs-lookup"><span data-stu-id="56609-107">Personal apps (static tabs) are currently available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
>
> <span data-ttu-id="56609-108">释放对选项卡的完全支持时：</span><span class="sxs-lookup"><span data-stu-id="56609-108">When full support for tabs is released:</span></span>
>
> * <span data-ttu-id="56609-109">所有选项卡将始终在移动设备上可用</span><span class="sxs-lookup"><span data-stu-id="56609-109">All tabs will always be available on mobile</span></span>
> * <span data-ttu-id="56609-110">您`contentUrl` **将在移动团队客户端中加载**。</span><span class="sxs-lookup"><span data-stu-id="56609-110">Your `contentUrl` **will be loaded in the mobile Teams client**.</span></span>
> * <span data-ttu-id="56609-111">对于频道/组选项卡，用户仍可以通过您`websiteUrl`在单独的浏览器中打开您的`contentUrl`选项卡，但您将首先加载。</span><span class="sxs-lookup"><span data-stu-id="56609-111">For channel/group tabs, users can still open your tab in a separate browser via your `websiteUrl`, however your `contentUrl` will be loaded first.</span></span>

<span data-ttu-id="56609-112">个人应用是具有个人作用域的应用程序。</span><span class="sxs-lookup"><span data-stu-id="56609-112">A personal app is an app with a personal scope.</span></span> <span data-ttu-id="56609-113">作为应用程序开发人员，您可以选择提供为单个用户生成的应用程序版本。</span><span class="sxs-lookup"><span data-stu-id="56609-113">As an app developer, you have the option to provide a version of your app that is built for the individual user.</span></span> <span data-ttu-id="56609-114">在此版本中，选项卡的集合（以及自动程序，如果您已加入）是为此人设计的。</span><span class="sxs-lookup"><span data-stu-id="56609-114">In this version, the collection of tabs (and the bot, if you've included one), are designed for the person.</span></span> <span data-ttu-id="56609-115">这样，你就能够创建与你的用户的一对一交互。</span><span class="sxs-lookup"><span data-stu-id="56609-115">This way, you're able to create a one-on-one interaction with your users.</span></span>

<span data-ttu-id="56609-116">个人应用程序是指有人可以查看其所有内容，以及最近在应用中查看的所有项目。</span><span class="sxs-lookup"><span data-stu-id="56609-116">A personal app is where someone can see everything that's theirs, and all the items they've recently viewed in the app.</span></span> <span data-ttu-id="56609-117">它将所有内容都放在一个位置。</span><span class="sxs-lookup"><span data-stu-id="56609-117">It puts everything in one place.</span></span> <span data-ttu-id="56609-118">在下面的屏幕截图中，Contoso 是个人应用浮出控件中的个人应用程序。</span><span class="sxs-lookup"><span data-stu-id="56609-118">In the following screenshot, Contoso is a personal app in the personal app flyout.</span></span>

![应用程序溢出菜单的图像](~/assets/images/Personal-apps-App-flyout.png)

---

## <a name="guidelines"></a><span data-ttu-id="56609-120">准则</span><span class="sxs-lookup"><span data-stu-id="56609-120">Guidelines</span></span>

<span data-ttu-id="56609-121">个人应用程序通常包含以下选项卡：</span><span class="sxs-lookup"><span data-stu-id="56609-121">A personal app typically contains the following tabs:</span></span>

### <a name="your-tab"></a><span data-ttu-id="56609-122">您的选项卡</span><span class="sxs-lookup"><span data-stu-id="56609-122">Your tab</span></span>

<span data-ttu-id="56609-123">你的用户将看到其所有内容。</span><span class="sxs-lookup"><span data-stu-id="56609-123">This is where your users will see all their stuff.</span></span> <span data-ttu-id="56609-124">其个人空间。</span><span class="sxs-lookup"><span data-stu-id="56609-124">It's their personal space.</span></span> <span data-ttu-id="56609-125">该选项卡可作为列表、网格、列或单个画布进行排列。。最适用于您的应用程序的任何功能。</span><span class="sxs-lookup"><span data-stu-id="56609-125">The tab can be arranged as a list, a grid, columns, or a single canvas...whatever works best for your application.</span></span> <span data-ttu-id="56609-126">有关设计有效选项卡的其他信息，请参阅： [选项卡设计（~/tabs/design/tabs.md）。</span><span class="sxs-lookup"><span data-stu-id="56609-126">For additional information on designing effective tabs see: [Tabs design(~/tabs/design/tabs.md).</span></span>

<span data-ttu-id="56609-127">由于此选项卡可以显示来自多个通道的项目，因此每个项目都应显示其自己的团队、频道和选项卡，以便用户可以轻松地查看它的来源。</span><span class="sxs-lookup"><span data-stu-id="56609-127">Since this tab can show items from multiple channels, each item should display its own team, channel, and tab so the user can easily see where it originated.</span></span>

!["个人任务" 选项卡](~/assets/images/Personal-apps-MY-tab.png)

### <a name="recent"></a><span data-ttu-id="56609-129">最近更新</span><span class="sxs-lookup"><span data-stu-id="56609-129">Recent</span></span>

<span data-ttu-id="56609-130">"**最近**" 选项卡允许某人浏览最近在您的应用程序中查看过的所有内容。</span><span class="sxs-lookup"><span data-stu-id="56609-130">The **Recent** tab lets someone browse everything they've recently viewed in your app.</span></span> <span data-ttu-id="56609-131">它按时间顺序列出（从最高到最新）。</span><span class="sxs-lookup"><span data-stu-id="56609-131">It's listed in chronological order (from most to least recent).</span></span> <span data-ttu-id="56609-132">单击此列表中的某个项目会将该用户导航到该项目的频道和选项卡。</span><span class="sxs-lookup"><span data-stu-id="56609-132">Clicking on an item in this list will navigate the user to that item's channel and tab.</span></span>

![最近选项卡](~/assets/images/Personal-apps-Recent-tab.png)

### <a name="all"></a><span data-ttu-id="56609-134">所有</span><span class="sxs-lookup"><span data-stu-id="56609-134">All</span></span>

<span data-ttu-id="56609-135">这是个人组织中的所有选项卡的列表（仍有权访问它们）。</span><span class="sxs-lookup"><span data-stu-id="56609-135">This is a list of all your tabs in the person's organization (the ones they have access to, anyway).</span></span> <span data-ttu-id="56609-136">换句话说，它在使用应用程序的任何位置显示它们。</span><span class="sxs-lookup"><span data-stu-id="56609-136">In other words, it shows them everywhere the app is being used.</span></span> <span data-ttu-id="56609-137">与**最近**的选项卡一样，选择列表中的内容会将用户直接带入相关频道和选项卡。</span><span class="sxs-lookup"><span data-stu-id="56609-137">As with the **Recent** tab, selecting something in the list will bring the user straight to the relevant channel and tab.</span></span>

### <a name="bot"></a><span data-ttu-id="56609-138">Bot</span><span class="sxs-lookup"><span data-stu-id="56609-138">Bot</span></span>

<span data-ttu-id="56609-139">Bot 不是必需的，但它是直接和私下与用户进行通信的绝佳方式。</span><span class="sxs-lookup"><span data-stu-id="56609-139">A bot isn't required, but it's a great way to communicate directly and privately with your users.</span></span> <span data-ttu-id="56609-140">通知是个人应用程序中最重要的功能之一，以及通知与直接通信是否更好的方法？</span><span class="sxs-lookup"><span data-stu-id="56609-140">Notification is one of the most important functions of a personal app, and what better way to notify than with direct communication?</span></span>

<span data-ttu-id="56609-141">Bot 以卡片形式传递邮件，这可以提供特定信息（如通知新内容可用）或广泛的更新（如日常待办情况列表）。</span><span class="sxs-lookup"><span data-stu-id="56609-141">Bots deliver messages in the form of cards, which can provide specific information (like an alert that new content is available) or broad updates (like a daily to-do list).</span></span> <span data-ttu-id="56609-142">有关设计有效的 bot 的详细信息，请参阅： [Bot 设计（~/bots/design/bots.md）。</span><span class="sxs-lookup"><span data-stu-id="56609-142">For additional information on designing effective bots see: [Bot design(~/bots/design/bots.md).</span></span>

![Bot 问候语](~/assets/images/Personal-apps-Bot.png)

### <a name="help-and-settings"></a><span data-ttu-id="56609-144">帮助和设置</span><span class="sxs-lookup"><span data-stu-id="56609-144">Help and Settings</span></span>

<span data-ttu-id="56609-145">帮助内容使用户能够发现您的应用程序的细微差别。</span><span class="sxs-lookup"><span data-stu-id="56609-145">Help content enables users to discover the nuances of your app.</span></span> <span data-ttu-id="56609-146">添加 "**设置**" 选项卡，让他们可以进一步自定义它。</span><span class="sxs-lookup"><span data-stu-id="56609-146">Add a **Settings** tab to give them the ability to further customize it.</span></span>

### <a name="about"></a><span data-ttu-id="56609-147">关于</span><span class="sxs-lookup"><span data-stu-id="56609-147">About</span></span>

<span data-ttu-id="56609-148">包括 "**关于**" 选项卡，以提供版本号码、功能、隐私和权限链接等信息。</span><span class="sxs-lookup"><span data-stu-id="56609-148">Include an **About** tab to provide information like version number, capabilities, privacy, and permissions links.</span></span>

## <a name="best-practices"></a><span data-ttu-id="56609-149">最佳做法</span><span class="sxs-lookup"><span data-stu-id="56609-149">Best practices</span></span>

### <a name="communicate-directly-with-your-users"></a><span data-ttu-id="56609-150">直接与您的用户通信</span><span class="sxs-lookup"><span data-stu-id="56609-150">Communicate directly with your users</span></span>

<span data-ttu-id="56609-151">使用 bot 向用户通知更改和新功能。</span><span class="sxs-lookup"><span data-stu-id="56609-151">Use a bot to notify users of changes and new features.</span></span>

### <a name="customize-your-tabs"></a><span data-ttu-id="56609-152">自定义选项卡 .。。</span><span class="sxs-lookup"><span data-stu-id="56609-152">Customize your tabs...</span></span>

<span data-ttu-id="56609-153">你可以随意添加其他选项卡，以帮助你的用户完成特定任务。</span><span class="sxs-lookup"><span data-stu-id="56609-153">Feel free to add other tabs that will help your users accomplish specific tasks.</span></span>

### <a name="and-make-them-relevant-to-every-user"></a><span data-ttu-id="56609-154">...并使其与每个用户相关</span><span class="sxs-lookup"><span data-stu-id="56609-154">...and make them relevant to every user</span></span>

<span data-ttu-id="56609-155">您在应用程序清单中声明的每个选项卡将对所有用户可见。</span><span class="sxs-lookup"><span data-stu-id="56609-155">Every tab you declare in your app manifest will be visible to all users.</span></span> <span data-ttu-id="56609-156">例如，如果您的个人应用程序是由经理和员工使用的费用报告工具，则 "**审批**" 选项卡应提供对这两个角色都有意义的内容。</span><span class="sxs-lookup"><span data-stu-id="56609-156">For example, if your personal app is an expense reporting tool that is used by both managers and employees, an **Approval** tab should provide content that is meaningful to both roles.</span></span>
