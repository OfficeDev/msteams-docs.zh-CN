---
title: 上传自定义应用
description: 介绍如何在 Microsoft Teams 中上传应用
ms.topic: how-to
keywords: teams 应用上载
ms.openlocfilehash: 2e7a21dc27fdfe824ecacebabbb61a3b99ae8e79
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014339"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a><span data-ttu-id="498b1-104">将一个应用程序包上传到 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="498b1-104">Upload an app package to Microsoft Teams</span></span>

<span data-ttu-id="498b1-105">若要在 Microsoft Teams 中测试应用体验，需要将应用上传到 Teams。</span><span class="sxs-lookup"><span data-stu-id="498b1-105">To test your app experience within Microsoft Teams, you need to upload your app to Teams.</span></span> <span data-ttu-id="498b1-106">上载会将应用添加到你选择的团队，并且你和团队成员可以像最终用户一样与其交互。</span><span class="sxs-lookup"><span data-stu-id="498b1-106">Uploading adds the app to the team you select, and you and your team members can interact with it like end users.</span></span>

> [!NOTE]
> <span data-ttu-id="498b1-107">通过"对话"窗口查看时，使用自动程序为现有应用上载更新的程序包可能不会显示选项卡更改。</span><span class="sxs-lookup"><span data-stu-id="498b1-107">Uploading an updated package for an existing app with a bot might not show tab changes when viewed through the Conversations window.</span></span> <span data-ttu-id="498b1-108">最好通过应用飞出来访问它，或在干净测试环境中进行测试。</span><span class="sxs-lookup"><span data-stu-id="498b1-108">It's better to access it via the Apps fly-out, or test on a clean test environment.</span></span>

## <a name="create-your-upload-package"></a><span data-ttu-id="498b1-109">创建上传包</span><span class="sxs-lookup"><span data-stu-id="498b1-109">Create your upload package</span></span>

<span data-ttu-id="498b1-110">对于开发以及 AppSource (Office 应用商店) 提交，你必须创建一个可上传的程序包，其中包含描述你的体验的信息。</span><span class="sxs-lookup"><span data-stu-id="498b1-110">For development as well as AppSource (formerly Office Store) submission you must create an uploadable package that contains the information to describe your experience.</span></span> <span data-ttu-id="498b1-111">该包是一个 .zip 文件，其中包含唯一定义体验的应用程序清单和图标。</span><span class="sxs-lookup"><span data-stu-id="498b1-111">The package, a .zip file, contains the application manifest and icons that uniquely define your experience.</span></span>

<span data-ttu-id="498b1-112">若要创建上传程序包，请参阅为 Microsoft Teams 应用 [创建程序包](../build-and-test/apps-package.md)。</span><span class="sxs-lookup"><span data-stu-id="498b1-112">To create an upload package, see [Create the package for your Microsoft Teams app](../build-and-test/apps-package.md).</span></span>

<span data-ttu-id="498b1-113">创建程序包后，现在可以将其上载到团队中。</span><span class="sxs-lookup"><span data-stu-id="498b1-113">With your package created, you can now upload it into a team.</span></span> <span data-ttu-id="498b1-114">上载后，它将可供选定团队中的所有用户使用，并且仅可供该团队的用户使用。</span><span class="sxs-lookup"><span data-stu-id="498b1-114">Once uploaded it will be available for all users in the selected team, and only the users of that team.</span></span>

## <a name="load-your-package-into-teams"></a><span data-ttu-id="498b1-115">将程序包加载到 Teams 中</span><span class="sxs-lookup"><span data-stu-id="498b1-115">Load your package into Teams</span></span>

<span data-ttu-id="498b1-116">可以通过将程序包上传到 Teams 来测试它。</span><span class="sxs-lookup"><span data-stu-id="498b1-116">You can test your package by uploading it into Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="498b1-117">若要上传工作，租户管理员必须先 [启用应用上载](/microsoftteams/admin-settings)。</span><span class="sxs-lookup"><span data-stu-id="498b1-117">For uploading to work, your tenant admin must first [enable uploading of apps](/microsoftteams/admin-settings).</span></span>

<span data-ttu-id="498b1-118">有两种方法将应用上传到 Teams：</span><span class="sxs-lookup"><span data-stu-id="498b1-118">There are two ways to upload your app to Teams:</span></span>

* <span data-ttu-id="498b1-119">使用应用商店</span><span class="sxs-lookup"><span data-stu-id="498b1-119">Using the Store</span></span>
* <span data-ttu-id="498b1-120">使用"应用"选项卡</span><span class="sxs-lookup"><span data-stu-id="498b1-120">Using the Apps tab</span></span>

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a><span data-ttu-id="498b1-121">使用应用商店将程序包上传到团队或对话</span><span class="sxs-lookup"><span data-stu-id="498b1-121">Upload your package into a team or conversation using the Store</span></span>

1. <span data-ttu-id="498b1-122">在 Teams 的左下角，选择"应用商店"图标。</span><span class="sxs-lookup"><span data-stu-id="498b1-122">In the lower left corner of Teams, choose the Store icon.</span></span> <span data-ttu-id="498b1-123">在"应用商店"页面上，选择"上载自定义应用"。</span><span class="sxs-lookup"><span data-stu-id="498b1-123">On the Store page, choose "Upload a custom app".</span></span>

  ![查看团队](../../assets/images/store-upload-a-custom-app2.png)

2. <span data-ttu-id="498b1-125">在 *"打开*"对话框中，导航到要上载的程序包，然后选择"*打开"。*</span><span class="sxs-lookup"><span data-stu-id="498b1-125">In the *Open* dialog, navigate to the package you want to upload and choose *Open*.</span></span>

   ![添加菜单](../../assets/images/NewappAddmenudropdown.png)

<span data-ttu-id="498b1-127">上载的程序包现在应该可用于在同意对话框中指定的团队或对话中。</span><span class="sxs-lookup"><span data-stu-id="498b1-127">The uploaded package should now be available for use in the team or conversation specified in the consent dialog.</span></span> <span data-ttu-id="498b1-128">如果应用未显示，最常见的原因是清单中的错误，尤其是应用、机器人和消息扩展的 ID。</span><span class="sxs-lookup"><span data-stu-id="498b1-128">If your app does not appear, the most common reason is an error in the manifest, particularly ids for the app, bot and messaging extensions.</span></span> <span data-ttu-id="498b1-129">如果应用未针对对话进行范围设置，则不显示该选项。</span><span class="sxs-lookup"><span data-stu-id="498b1-129">If the app is not scoped for conversations, that option will not appear.</span></span>

>[!NOTE]
> <span data-ttu-id="498b1-130">对话中的应用 [当前处于](../../resources/dev-preview/developer-preview-intro.md)开发者预览版，如果 Teams 未处于该模式下运行，则不显示此选项。</span><span class="sxs-lookup"><span data-stu-id="498b1-130">Apps in conversations is currently in [Developer Preview](../../resources/dev-preview/developer-preview-intro.md), and the option will not appear if Teams is not running in that mode.</span></span>

![上传的机器人列表中的自动程序示例](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a><span data-ttu-id="498b1-132">使用"应用"选项卡将程序包上传到团队</span><span class="sxs-lookup"><span data-stu-id="498b1-132">Upload your package into a team using the Apps tab</span></span>

1. <span data-ttu-id="498b1-133">在目标团队中，选择 *" (&#8943;)* 选项，然后选择 *"管理团队"。*</span><span class="sxs-lookup"><span data-stu-id="498b1-133">In the target team, choose *More options* (**&#8943;**) and choose *Manage team*.</span></span>

   > [!NOTE]
   > <span data-ttu-id="498b1-134">你必须是团队所有者，或者所有者必须允许用户添加相应的应用类型，此功能显示。</span><span class="sxs-lookup"><span data-stu-id="498b1-134">You must be the team owner, or the owner must allow users to add the appropriate app types for this functionality to appear.</span></span>

2. <span data-ttu-id="498b1-135">选择"应用"选项卡，然后选择右下角 *的* "上载自定义应用"。</span><span class="sxs-lookup"><span data-stu-id="498b1-135">Select the Apps tab, and then choose *Upload a custom app* on the lower right.</span></span>

   ![上载入口点](../../assets/images/UploadACustomApp.png)

3. <span data-ttu-id="498b1-137">浏览到计算机，然后从计算机中选择 .zip 程序包。</span><span class="sxs-lookup"><span data-stu-id="498b1-137">Browse to and select your .zip package from your computer.</span></span>

4. <span data-ttu-id="498b1-138">短暂暂停后，你将在列表中看到已上传的应用。</span><span class="sxs-lookup"><span data-stu-id="498b1-138">After a brief pause you will see your uploaded app in the list.</span></span>

   ![上传的机器人列表中的自动程序示例](../../assets/images/botinlist.jpg)

<span data-ttu-id="498b1-140">如果你的应用未加载，最常见的原因是清单中的错误，尤其是应用、机器人和消息扩展的 ID。</span><span class="sxs-lookup"><span data-stu-id="498b1-140">If your app does not load, the most common reason is an error in the manifest, particularly ids for the app, bot and messaging extensions.</span></span>

## <a name="accessing-your-uploaded-configurable-tab"></a><span data-ttu-id="498b1-141">访问已上载的可配置选项卡</span><span class="sxs-lookup"><span data-stu-id="498b1-141">Accessing your uploaded configurable tab</span></span>

<span data-ttu-id="498b1-142">如果应用包含选项卡，用户可以使用标准选项卡库流将其固定到任何对话或团队频道：</span><span class="sxs-lookup"><span data-stu-id="498b1-142">If the app contains tabs, users can pin them to any conversation or team channel using the standard tab gallery flow:</span></span>

1. <span data-ttu-id="498b1-143">转到团队中的频道。</span><span class="sxs-lookup"><span data-stu-id="498b1-143">Go to a channel in the team.</span></span> <span data-ttu-id="498b1-144">Choose *+* (Add a *tab*) ) to the right of the existing tabs.</span><span class="sxs-lookup"><span data-stu-id="498b1-144">Choose *+* (*Add a tab*) to the right of the existing tabs.</span></span>

2. <span data-ttu-id="498b1-145">从出现的库中选择选项卡。</span><span class="sxs-lookup"><span data-stu-id="498b1-145">Select your tab from the gallery that appears.</span></span>

3. <span data-ttu-id="498b1-146">接受同意提示。</span><span class="sxs-lookup"><span data-stu-id="498b1-146">Accept the consent prompt.</span></span>

4. <span data-ttu-id="498b1-147">通过它的配置页面 [配置选项卡，](../../tabs/how-to/create-tab-pages/configuration-page.md)然后选择"*保存"。*</span><span class="sxs-lookup"><span data-stu-id="498b1-147">Configure your tab via its [configuration page](../../tabs/how-to/create-tab-pages/configuration-page.md) and choose *Save*.</span></span>

  !["添加选项卡"对话框，包含可用选项卡的库](../../assets/images/tab_gallery.png)

## <a name="accessing-your-uploaded-bot"></a><span data-ttu-id="498b1-149">访问上传的机器人</span><span class="sxs-lookup"><span data-stu-id="498b1-149">Accessing your uploaded bot</span></span>

<span data-ttu-id="498b1-150">向团队添加自动程序时，该团队中团队内外的任何人都可以使用自动程序，具体取决于自动程序范围定义。</span><span class="sxs-lookup"><span data-stu-id="498b1-150">When you add a bot to a team, it should be usable by anyone on that team, inside and outside the team channels, depending on bot scope definition.</span></span> <span data-ttu-id="498b1-151">你和其他团队成员将在常规频道中看到一个帖子，指示机器人已添加到团队。</span><span class="sxs-lookup"><span data-stu-id="498b1-151">You and other team members will see a post in the General channel indicating that the bot has been added to the team.</span></span>

<span data-ttu-id="498b1-152">对于支持团队的机器人，你可以首先调用自动程序@mentioning自动完成的名称。自动完成。</span><span class="sxs-lookup"><span data-stu-id="498b1-152">For a teams-enabled bot, you can start by invoking your bot by @mentioning the name of the bot, which should autocomplete.</span></span>

<span data-ttu-id="498b1-153">若要测试与机器人的直接聊天，可以通过应用主页访问它，@mention频道中，或在"新建聊天"窗口中 **搜索** 它。</span><span class="sxs-lookup"><span data-stu-id="498b1-153">To test direct chats with your bot, you can either access it via the App home, @mention it in a channel, or search for it in the **New Chat** window.</span></span>

<span data-ttu-id="498b1-154">将机器人添加到对话中以测试与自动程序的直接聊天时，@mention对话中，或在"新建聊天"窗口中 **搜索** 它。</span><span class="sxs-lookup"><span data-stu-id="498b1-154">When you add your bot to a conversation To test direct chats with your bot, you can @mention it in a conversation, or search for it in the **New Chat** window.</span></span>

## <a name="accessing-your-uploaded-connector"></a><span data-ttu-id="498b1-155">访问已上载的连接器</span><span class="sxs-lookup"><span data-stu-id="498b1-155">Accessing your uploaded Connector</span></span>

<span data-ttu-id="498b1-156">在团队或对话中加载应用后，用户可以使用标准连接器库流设置连接器：</span><span class="sxs-lookup"><span data-stu-id="498b1-156">With the app loaded in the team or conversation, users can set up a Connector using the standard Connectors gallery flow:</span></span>

1. <span data-ttu-id="498b1-157">转到团队中的频道。</span><span class="sxs-lookup"><span data-stu-id="498b1-157">Go to a channel in the team.</span></span> <span data-ttu-id="498b1-158">选择 *"其他选项\*\*(&#8943;)* 连接器 *"。*</span><span class="sxs-lookup"><span data-stu-id="498b1-158">Choose *More options* (*&#8943;*) and choose *Connectors*.</span></span>

2. <span data-ttu-id="498b1-159">从底部的 **旁加载部分选择** 连接器。</span><span class="sxs-lookup"><span data-stu-id="498b1-159">Select your Connector from the **Sideloaded** section at the bottom.</span></span>

3. <span data-ttu-id="498b1-160">通过连接器的配置页面 [配置连接器，然后选择](../../webhooks-and-connectors/how-to/connectors-creating.md)"*保存"。*</span><span class="sxs-lookup"><span data-stu-id="498b1-160">Configure your Connector via its [configuration page](../../webhooks-and-connectors/how-to/connectors-creating.md) and choose *Save*.</span></span>

  !["添加选项卡"对话框，包含可用选项卡的库。](../../assets/images/connector_gallery.png)

## <a name="accessing-your-uploaded-messaging-extension"></a><span data-ttu-id="498b1-162">访问上传的消息扩展</span><span class="sxs-lookup"><span data-stu-id="498b1-162">Accessing your uploaded messaging extension</span></span>

<span data-ttu-id="498b1-163">具有邮件扩展名的已上载应用会自动显示在撰写框中的" (&#8943;) "菜单中的"更多选项"中。</span><span class="sxs-lookup"><span data-stu-id="498b1-163">An uploaded app with a messaging extension automatically appears in the *More options* (*&#8943;*) menu in the compose box.</span></span>

![消息扩展](../../assets/images/compose-extensions/cesampleapp.png)

## <a name="removing-or-updating-your-app"></a><span data-ttu-id="498b1-165">删除或更新应用</span><span class="sxs-lookup"><span data-stu-id="498b1-165">Removing or updating your app</span></span>

<span data-ttu-id="498b1-166">如果要删除应用，请在"查看 Teams 机器人"列表中选择应用名称旁边的回收站图标。</span><span class="sxs-lookup"><span data-stu-id="498b1-166">If you want to remove your app, select the trash-can icon next to the app name in the View Teams bots list.</span></span>

<span data-ttu-id="498b1-167">如果更改清单信息，必须先删除应用，然后根据"将程序包加载到团队 (添加更新的程序包) 。 [](#load-your-package-into-teams)</span><span class="sxs-lookup"><span data-stu-id="498b1-167">If you change manifest information, you must first remove the app and then add the updated package (per [Load your package into a team](#load-your-package-into-teams)).</span></span> <span data-ttu-id="498b1-168">请注意，一般情况下，服务的代码更改不需要您重新上载清单，除非这些更改需要清单更新 (例如，更改其自动程序应用的 URL 或 Microsoft 应用 ID) 。</span><span class="sxs-lookup"><span data-stu-id="498b1-168">Note that, in general, code changes on your service do not require you to re-upload your manifest, unless those changes require manifest updates (such as changes to the URL or the Microsoft app ID for its bot).</span></span>

> [!NOTE]
> <span data-ttu-id="498b1-169">无法从个人上下文中完全删除自动程序。</span><span class="sxs-lookup"><span data-stu-id="498b1-169">There is no way to completely remove a bot from personal context.</span></span> <span data-ttu-id="498b1-170">如果删除并重新添加自动程序，则与自动程序的其他通信将附加到上一个对话中。</span><span class="sxs-lookup"><span data-stu-id="498b1-170">If the bot is removed and re-added, additional communication with the bot will append to the previous conversation.</span></span>

## <a name="troubleshooting-notes"></a><span data-ttu-id="498b1-171">疑难解答说明</span><span class="sxs-lookup"><span data-stu-id="498b1-171">Troubleshooting notes</span></span>

* <span data-ttu-id="498b1-172">如果清单未加载，请仔细检查您是否遵循了"创建程序包"中的所有说明，并[](../../concepts/build-and-test/apps-package.md)针对架构验证[了清单](../../resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="498b1-172">If the manifest doesn't load, please double-check that you followed all the instructions in [Create the package](../../concepts/build-and-test/apps-package.md) and validated your manifest against the [schema](../../resources/schema/manifest-schema.md).</span></span>
