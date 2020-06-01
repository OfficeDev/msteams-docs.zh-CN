---
title: 在 Microsoft 团队中上传自定义应用程序
description: 介绍如何在 Microsoft 团队中上传您的应用程序
keywords: 团队应用上传
ms.openlocfilehash: 256a9bea48ed816f2e9912006dd2fe7301743919
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/31/2020
ms.locfileid: "44453880"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a><span data-ttu-id="bca1a-104">将一个应用程序包上传到 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="bca1a-104">Upload an app package to Microsoft Teams</span></span>

<span data-ttu-id="bca1a-105">若要在 Microsoft 团队中测试应用程序体验，您需要将您的应用程序上传到团队。</span><span class="sxs-lookup"><span data-stu-id="bca1a-105">To test your app experience within Microsoft Teams, you need to upload your app to Teams.</span></span> <span data-ttu-id="bca1a-106">上载操作将向您选择的团队添加应用程序，你和你的团队成员可以与最终用户进行交互。</span><span class="sxs-lookup"><span data-stu-id="bca1a-106">Uploading adds the app to the team you select, and you and your team members can interact with it like end users.</span></span>

> [!NOTE]
> <span data-ttu-id="bca1a-107">使用 bot 上载现有应用程序的已更新包时，在通过对话窗口查看时，可能不会显示选项卡更改。</span><span class="sxs-lookup"><span data-stu-id="bca1a-107">Uploading an updated package for an existing app with a bot might not show tab changes when viewed through the Conversations window.</span></span> <span data-ttu-id="bca1a-108">最好是通过应用程序飞出方式进行访问，也可以在干净的测试环境中进行测试。</span><span class="sxs-lookup"><span data-stu-id="bca1a-108">It's better to access it via the Apps fly-out, or test on a clean test environment.</span></span>

## <a name="create-your-upload-package"></a><span data-ttu-id="bca1a-109">创建你的上载包</span><span class="sxs-lookup"><span data-stu-id="bca1a-109">Create your upload package</span></span>

<span data-ttu-id="bca1a-110">对于开发和 AppSource （以前称为 "Office 应用商店"）提交，您必须创建一个 uploadable 程序包，其中包含描述您的体验的信息。</span><span class="sxs-lookup"><span data-stu-id="bca1a-110">For development as well as AppSource (formerly Office Store) submission you must create an uploadable package that contains the information to describe your experience.</span></span> <span data-ttu-id="bca1a-111">该包（.zip 文件）包含应用程序清单和用于唯一定义您的体验的图标。</span><span class="sxs-lookup"><span data-stu-id="bca1a-111">The package, a .zip file, contains the application manifest and icons that uniquely define your experience.</span></span>

<span data-ttu-id="bca1a-112">若要创建上载包，请参阅为[Microsoft 团队应用程序创建程序包](../build-and-test/apps-package.md)。</span><span class="sxs-lookup"><span data-stu-id="bca1a-112">To create an upload package, see [Create the package for your Microsoft Teams app](../build-and-test/apps-package.md).</span></span>

<span data-ttu-id="bca1a-113">创建包后，即可将其上载到团队中。</span><span class="sxs-lookup"><span data-stu-id="bca1a-113">With your package created, you can now upload it into a team.</span></span> <span data-ttu-id="bca1a-114">上载后，将对所选团队中的所有用户和该团队的用户可用。</span><span class="sxs-lookup"><span data-stu-id="bca1a-114">Once uploaded it will be available for all users in the selected team, and only the users of that team.</span></span>

## <a name="load-your-package-into-teams"></a><span data-ttu-id="bca1a-115">将包加载到团队</span><span class="sxs-lookup"><span data-stu-id="bca1a-115">Load your package into Teams</span></span>

<span data-ttu-id="bca1a-116">您可以通过将您的程序包上载到团队来对其进行测试。</span><span class="sxs-lookup"><span data-stu-id="bca1a-116">You can test your package by uploading it into Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="bca1a-117">若要上载工作，租户管理员必须首先[启用上载应用](/microsoftteams/admin-settings)。</span><span class="sxs-lookup"><span data-stu-id="bca1a-117">For uploading to work, your tenant admin must first [enable uploading of apps](/microsoftteams/admin-settings).</span></span>

<span data-ttu-id="bca1a-118">有两种方法可将您的应用程序上载到团队：</span><span class="sxs-lookup"><span data-stu-id="bca1a-118">There are two ways to upload your app to Teams:</span></span>

* <span data-ttu-id="bca1a-119">使用 Store</span><span class="sxs-lookup"><span data-stu-id="bca1a-119">Using the Store</span></span>
* <span data-ttu-id="bca1a-120">使用 "应用" 选项卡</span><span class="sxs-lookup"><span data-stu-id="bca1a-120">Using the Apps tab</span></span>

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a><span data-ttu-id="bca1a-121">使用 Microsoft Store 将你的程序包上载到团队或对话中</span><span class="sxs-lookup"><span data-stu-id="bca1a-121">Upload your package into a team or conversation using the Store</span></span>

1. <span data-ttu-id="bca1a-122">在 "团队" 的左下角，选择 "存储" 图标。</span><span class="sxs-lookup"><span data-stu-id="bca1a-122">In the lower left corner of Teams, choose the Store icon.</span></span> <span data-ttu-id="bca1a-123">在 "应用商店" 页上，选择 "上载自定义应用程序"。</span><span class="sxs-lookup"><span data-stu-id="bca1a-123">On the Store page, choose "Upload a custom app".</span></span>

   ![查看团队](../../assets/images/store-upload-a-custom-app.png)

2. <span data-ttu-id="bca1a-125">在 "*打开*" 对话框中，导航到要上载的包，然后选择 "*打开*"。</span><span class="sxs-lookup"><span data-stu-id="bca1a-125">In the *Open* dialog, navigate to the package you want to upload and choose *Open*.</span></span>

<span data-ttu-id="bca1a-126">已上载的包现在应可在同意对话框中指定的团队或对话中使用。</span><span class="sxs-lookup"><span data-stu-id="bca1a-126">The uploaded package should now be available for use in the team or conversation specified in the consent dialog.</span></span> <span data-ttu-id="bca1a-127">如果未显示您的应用程序，最常见的原因是清单中的一个错误，尤其是应用程序、bot 和邮件扩展的 id。</span><span class="sxs-lookup"><span data-stu-id="bca1a-127">If your app does not appear, the most common reason is an error in the manifest, particularly ids for the app, bot and messaging extensions.</span></span> <span data-ttu-id="bca1a-128">如果应用程序的作用范围不适合对话，则不会显示该选项。</span><span class="sxs-lookup"><span data-stu-id="bca1a-128">If the app is not scoped for conversations, that option will not appear.</span></span>

>[!NOTE]
> <span data-ttu-id="bca1a-129">对话中的应用程序当前处于[开发人员预览版](../../resources/dev-preview/developer-preview-intro.md)中，如果团队未在该模式下运行，则不会显示该选项。</span><span class="sxs-lookup"><span data-stu-id="bca1a-129">Apps in conversations is currently in [Developer Preview](../../resources/dev-preview/developer-preview-intro.md), and the option will not appear if Teams is not running in that mode.</span></span>

![上载的 bot 列表中的 bot 的示例](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a><span data-ttu-id="bca1a-131">使用 "应用程序" 选项卡将您的包上传到团队</span><span class="sxs-lookup"><span data-stu-id="bca1a-131">Upload your package into a team using the Apps tab</span></span>

1. <span data-ttu-id="bca1a-132">在目标团队中，选择 "*更多选项*（**&#8943;**）"，然后选择 "*管理团队*"。</span><span class="sxs-lookup"><span data-stu-id="bca1a-132">In the target team, choose *More options* (**&#8943;**) and choose *Manage team*.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bca1a-133">您必须是团队所有者，或者所有者必须允许用户添加相应的应用程序类型，才能显示此功能。</span><span class="sxs-lookup"><span data-stu-id="bca1a-133">You must be the team owner, or the owner must allow users to add the appropriate app types for this functionality to appear.</span></span>

2. <span data-ttu-id="bca1a-134">选择 "应用" 选项卡，然后选择右下方的 "*上传自定义应用程序*"。</span><span class="sxs-lookup"><span data-stu-id="bca1a-134">Select the Apps tab, and then choose *Upload a custom app* on the lower right.</span></span>

   ![上载入口点](../../assets/images/UploadACustomApp.png)

3. <span data-ttu-id="bca1a-136">浏览到您的计算机上的 .zip 包并将其从计算机中选择。</span><span class="sxs-lookup"><span data-stu-id="bca1a-136">Browse to and select your .zip package from your computer.</span></span>

4. <span data-ttu-id="bca1a-137">在短暂停顿之后，你将在列表中看到上传的应用。</span><span class="sxs-lookup"><span data-stu-id="bca1a-137">After a brief pause you will see your uploaded app in the list.</span></span>

   ![上载的 bot 列表中的 bot 的示例](../../assets/images/botinlist.jpg)

<span data-ttu-id="bca1a-139">如果您的应用程序未加载，最常见的原因是清单中存在错误，尤其是应用程序、bot 和邮件扩展的 id。</span><span class="sxs-lookup"><span data-stu-id="bca1a-139">If your app does not load, the most common reason is an error in the manifest, particularly ids for the app, bot and messaging extensions.</span></span>

## <a name="accessing-your-uploaded-configurable-tab"></a><span data-ttu-id="bca1a-140">访问上传的 "可配置" 选项卡</span><span class="sxs-lookup"><span data-stu-id="bca1a-140">Accessing your uploaded configurable tab</span></span>

<span data-ttu-id="bca1a-141">如果应用程序包含选项卡，则用户可以使用标准的选项卡库流将它们固定到任何对话或团队频道：</span><span class="sxs-lookup"><span data-stu-id="bca1a-141">If the app contains tabs, users can pin them to any conversation or team channel using the standard tab gallery flow:</span></span>

1. <span data-ttu-id="bca1a-142">转到团队中的频道。</span><span class="sxs-lookup"><span data-stu-id="bca1a-142">Go to a channel in the team.</span></span> <span data-ttu-id="bca1a-143">选择 *+* 现有选项卡右侧的 *"（添加选项卡*）"。</span><span class="sxs-lookup"><span data-stu-id="bca1a-143">Choose *+* (*Add a tab*) to the right of the existing tabs.</span></span>

2. <span data-ttu-id="bca1a-144">从显示的库中选择您的选项卡。</span><span class="sxs-lookup"><span data-stu-id="bca1a-144">Select your tab from the gallery that appears.</span></span>

3. <span data-ttu-id="bca1a-145">接受同意提示。</span><span class="sxs-lookup"><span data-stu-id="bca1a-145">Accept the consent prompt.</span></span>

4. <span data-ttu-id="bca1a-146">通过[配置页面](../../tabs/how-to/create-tab-pages/configuration-page.md)配置您的选项卡，然后选择 "*保存*"。</span><span class="sxs-lookup"><span data-stu-id="bca1a-146">Configure your tab via its [configuration page](../../tabs/how-to/create-tab-pages/configuration-page.md) and choose *Save*.</span></span>

  !["添加选项卡" 对话框，带有可用选项卡的库](../../assets/images/tab_gallery.png)

## <a name="accessing-your-uploaded-bot"></a><span data-ttu-id="bca1a-148">访问上载的 bot</span><span class="sxs-lookup"><span data-stu-id="bca1a-148">Accessing your uploaded bot</span></span>

<span data-ttu-id="bca1a-149">当您向团队中添加机器人时，该团队的任何人都可以使用该团队中的任何人、团队频道内部和外部，具体取决于 bot 的作用域定义。</span><span class="sxs-lookup"><span data-stu-id="bca1a-149">When you add a bot to a team, it should be usable by anyone on that team, inside and outside the team channels, depending on bot scope definition.</span></span> <span data-ttu-id="bca1a-150">您和其他团队成员将在 "常规" 频道中看到一篇文章，表示已将该 bot 添加到团队。</span><span class="sxs-lookup"><span data-stu-id="bca1a-150">You and other team members will see a post in the General channel indicating that the bot has been added to the team.</span></span>

<span data-ttu-id="bca1a-151">对于已启用工作组的 bot，您可以通过 @mentioning bot 的名称（应自动完成）来开始调用你的 bot。</span><span class="sxs-lookup"><span data-stu-id="bca1a-151">For a teams-enabled bot, you can start by invoking your bot by @mentioning the name of the bot, which should autocomplete.</span></span>

<span data-ttu-id="bca1a-152">若要测试与你的 bot 的直接聊天，可以通过应用程序主页访问它，在频道中 @mention 它，也可以在**新聊天**窗口中搜索它。</span><span class="sxs-lookup"><span data-stu-id="bca1a-152">To test direct chats with your bot, you can either access it via the App home, @mention it in a channel, or search for it in the **New Chat** window.</span></span>

<span data-ttu-id="bca1a-153">将你的 bot 添加到对话以测试与你的 bot 的直接聊天时，可以在对话中 @mention 它，也可以在**新聊天**窗口中搜索它。</span><span class="sxs-lookup"><span data-stu-id="bca1a-153">When you add your bot to a conversation To test direct chats with your bot, you can @mention it in a conversation, or search for it in the **New Chat** window.</span></span>

## <a name="accessing-your-uploaded-connector"></a><span data-ttu-id="bca1a-154">访问上载的连接器</span><span class="sxs-lookup"><span data-stu-id="bca1a-154">Accessing your uploaded Connector</span></span>

<span data-ttu-id="bca1a-155">在团队或对话中加载应用程序后，用户可以使用标准的 "连接器" 库流设置连接器：</span><span class="sxs-lookup"><span data-stu-id="bca1a-155">With the app loaded in the team or conversation, users can set up a Connector using the standard Connectors gallery flow:</span></span>

1. <span data-ttu-id="bca1a-156">转到团队中的频道。</span><span class="sxs-lookup"><span data-stu-id="bca1a-156">Go to a channel in the team.</span></span> <span data-ttu-id="bca1a-157">选择 "*更多选项*（*&#8943;*）"，然后选择 "*连接器*"。</span><span class="sxs-lookup"><span data-stu-id="bca1a-157">Choose *More options* (*&#8943;*) and choose *Connectors*.</span></span>

2. <span data-ttu-id="bca1a-158">从底部的 "**上传**" 部分选择连接器。</span><span class="sxs-lookup"><span data-stu-id="bca1a-158">Select your Connector from the **Uploaded** section at the bottom.</span></span>

3. <span data-ttu-id="bca1a-159">通过[配置页面](../../webhooks-and-connectors/how-to/connectors-creating.md)配置连接器，然后选择 "*保存*"。</span><span class="sxs-lookup"><span data-stu-id="bca1a-159">Configure your Connector via its [configuration page](../../webhooks-and-connectors/how-to/connectors-creating.md) and choose *Save*.</span></span>

  !["添加选项卡" 对话框，带有可用选项卡库。](../../assets/images/connector_gallery.png)

## <a name="accessing-your-uploaded-messaging-extension"></a><span data-ttu-id="bca1a-161">访问上载的邮件扩展插件</span><span class="sxs-lookup"><span data-stu-id="bca1a-161">Accessing your uploaded messaging extension</span></span>

<span data-ttu-id="bca1a-162">带有邮件扩展功能的已上载应用程序将自动显示在 "撰写" 框中的 "*更多选项*（*&#8943;*）" 菜单中。</span><span class="sxs-lookup"><span data-stu-id="bca1a-162">An uploaded app with a messaging extension automatically appears in the *More options* (*&#8943;*) menu in the compose box.</span></span>

![消息传递扩展](../../assets/images/compose-extensions/cesampleapp.png)

## <a name="removing-or-updating-your-app"></a><span data-ttu-id="bca1a-164">删除或更新应用程序</span><span class="sxs-lookup"><span data-stu-id="bca1a-164">Removing or updating your app</span></span>

<span data-ttu-id="bca1a-165">如果要删除您的应用程序，请在 "查看团队 bot" 列表中选择应用程序名称旁边的 "垃圾桶" 图标。</span><span class="sxs-lookup"><span data-stu-id="bca1a-165">If you want to remove your app, select the trash-can icon next to the app name in the View Teams bots list.</span></span>

<span data-ttu-id="bca1a-166">如果您更改了清单信息，则必须先删除该应用程序，然后再添加更新的程序包（每次将[您的包加载到团队中](#load-your-package-into-teams)）。</span><span class="sxs-lookup"><span data-stu-id="bca1a-166">If you change manifest information, you must first remove the app and then add the updated package (per [Load your package into a team](#load-your-package-into-teams)).</span></span> <span data-ttu-id="bca1a-167">请注意，通常情况下，您的服务上的代码更改不需要重新上载清单，除非这些更改需要清单更新（例如，对 URL 或其 bot 的 Microsoft 应用 ID 所做的更改）。</span><span class="sxs-lookup"><span data-stu-id="bca1a-167">Note that, in general, code changes on your service do not require you to re-upload your manifest, unless those changes require manifest updates (such as changes to the URL or the Microsoft app ID for its bot).</span></span>

> [!NOTE]
> <span data-ttu-id="bca1a-168">无法从个人上下文中完全删除机器人。</span><span class="sxs-lookup"><span data-stu-id="bca1a-168">There is no way to completely remove a bot from personal context.</span></span> <span data-ttu-id="bca1a-169">如果卸载并重新添加了 bot，则与 bot 的其他通信将追加到之前的会话中。</span><span class="sxs-lookup"><span data-stu-id="bca1a-169">If the bot is removed and re-added, additional communication with the bot will append to the previous conversation.</span></span>

## <a name="troubleshooting-notes"></a><span data-ttu-id="bca1a-170">疑难解答说明</span><span class="sxs-lookup"><span data-stu-id="bca1a-170">Troubleshooting notes</span></span>

* <span data-ttu-id="bca1a-171">如果未加载清单，请仔细检查是否遵循 "[创建包](../../concepts/build-and-test/apps-package.md)" 和 "根据[架构](../../resources/schema/manifest-schema.md)验证清单" 中的所有说明操作。</span><span class="sxs-lookup"><span data-stu-id="bca1a-171">If the manifest doesn't load, please double-check that you followed all the instructions in [Create the package](../../concepts/build-and-test/apps-package.md) and validated your manifest against the [schema](../../resources/schema/manifest-schema.md).</span></span>

