---
title: 上传自定义应用
description: 介绍如何在 Microsoft Teams 中上传应用
ms.topic: how-to
ms.author: lajanuar
keywords: teams 应用上传
ms.openlocfilehash: c9102fa5b7056dda0db8d3e260bfb3e94b7f4e56
ms.sourcegitcommit: 7b4f383b506d4bc68a1b5641d6e0f404edbfbc6d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2021
ms.locfileid: "51946478"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a><span data-ttu-id="e6f97-104">将一个应用程序包上传到 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e6f97-104">Upload an app package to Microsoft Teams</span></span>

<span data-ttu-id="e6f97-105">若要在 Microsoft Teams 中测试应用体验，需要将应用上传到 Teams。</span><span class="sxs-lookup"><span data-stu-id="e6f97-105">To test your app experience within Microsoft Teams, you need to upload your app to Teams.</span></span> <span data-ttu-id="e6f97-106">上载会将应用添加到所选团队，所有团队成员都可以像最终用户一样与其交互。</span><span class="sxs-lookup"><span data-stu-id="e6f97-106">Uploading adds the app to the selected team and all the team members can interact with it like end users.</span></span>

> [!NOTE]
> <span data-ttu-id="e6f97-107">通过对话窗口查看时，使用自动程序上传现有应用的已更新程序包可能不会显示选项卡更改。</span><span class="sxs-lookup"><span data-stu-id="e6f97-107">Uploading an updated package for an existing app with a bot might not show tab changes when viewed through the conversations window.</span></span> <span data-ttu-id="e6f97-108">可以通过应用飞出或在干净环境中进行测试来访问应用。</span><span class="sxs-lookup"><span data-stu-id="e6f97-108">You can access the app through the apps fly-out or test in a clean environment.</span></span>

## <a name="create-your-upload-package"></a><span data-ttu-id="e6f97-109">创建上传包</span><span class="sxs-lookup"><span data-stu-id="e6f97-109">Create your upload package</span></span>

<span data-ttu-id="e6f97-110">对于开发和 AppSource 提交，必须创建可上传的程序包。</span><span class="sxs-lookup"><span data-stu-id="e6f97-110">For development and AppSource submission, you must create a package that you can upload.</span></span> <span data-ttu-id="e6f97-111">程序包必须包含描述你体验的信息。</span><span class="sxs-lookup"><span data-stu-id="e6f97-111">The package must contain the information to describe your experience.</span></span> <span data-ttu-id="e6f97-112">该包是一个 .zip 文件，其中包含唯一定义体验的应用程序清单和图标。</span><span class="sxs-lookup"><span data-stu-id="e6f97-112">The package is a .zip file that contains the application manifest and icons that uniquely define your experience.</span></span>

<span data-ttu-id="e6f97-113">若要创建上传程序包，请参阅 [为 Microsoft Teams 应用创建程序包](../build-and-test/apps-package.md)。</span><span class="sxs-lookup"><span data-stu-id="e6f97-113">To create an upload package, see [Create the package for your Microsoft Teams app](../build-and-test/apps-package.md).</span></span>

<span data-ttu-id="e6f97-114">创建包后，将其上传到团队。</span><span class="sxs-lookup"><span data-stu-id="e6f97-114">After you create the package, upload it into a team.</span></span> <span data-ttu-id="e6f97-115">上载的程序包仅对所选团队的用户可用。</span><span class="sxs-lookup"><span data-stu-id="e6f97-115">The uploaded package is only available to the users of the selected team.</span></span>

## <a name="load-your-package-into-teams"></a><span data-ttu-id="e6f97-116">将程序包加载到 Teams 中</span><span class="sxs-lookup"><span data-stu-id="e6f97-116">Load your package into Teams</span></span>

<span data-ttu-id="e6f97-117">可以通过将程序包上传到 Teams 来测试它。</span><span class="sxs-lookup"><span data-stu-id="e6f97-117">You can test your package by uploading it into Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="e6f97-118">若要上传工作，租户管理员必须先 [启用应用上传](/microsoftteams/admin-settings)。</span><span class="sxs-lookup"><span data-stu-id="e6f97-118">For uploading to work, your tenant admin must first [enable uploading of apps](/microsoftteams/admin-settings).</span></span>

<span data-ttu-id="e6f97-119">有两种方法将应用上传到 Teams：</span><span class="sxs-lookup"><span data-stu-id="e6f97-119">There are two ways to upload your app to Teams:</span></span>

* <span data-ttu-id="e6f97-120">使用应用商店</span><span class="sxs-lookup"><span data-stu-id="e6f97-120">Using the Store</span></span>
* <span data-ttu-id="e6f97-121">使用"应用"选项卡</span><span class="sxs-lookup"><span data-stu-id="e6f97-121">Using the Apps tab</span></span>

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a><span data-ttu-id="e6f97-122">使用应用商店将程序包上传到团队或对话</span><span class="sxs-lookup"><span data-stu-id="e6f97-122">Upload your package into a team or conversation using the Store</span></span>

1. <span data-ttu-id="e6f97-123">在 Teams 的左下角，选择 **"应用商店"** 图标。</span><span class="sxs-lookup"><span data-stu-id="e6f97-123">In the lower left corner of Teams, choose the **Store** icon.</span></span> <span data-ttu-id="e6f97-124">在应用商店页面上，选择 **上传自定义应用**。</span><span class="sxs-lookup"><span data-stu-id="e6f97-124">On the Store page, choose **Upload a custom app**.</span></span>

  ![查看团队](../../assets/images/store-upload-a-custom-app2.png)

2. <span data-ttu-id="e6f97-126">在 **"打开** "对话框中，导航到要上载的程序包，然后选择"打开"。</span><span class="sxs-lookup"><span data-stu-id="e6f97-126">In the **Open** dialog, navigate to the package you want to upload and choose Open.</span></span>

   ![添加菜单](../../assets/images/NewappAddmenudropdown.png)

<span data-ttu-id="e6f97-128">上载的程序包必须可用于在同意对话框中指定的团队或对话中。</span><span class="sxs-lookup"><span data-stu-id="e6f97-128">The uploaded package must be available for use in the team or conversation specified in the consent dialog.</span></span> <span data-ttu-id="e6f97-129">如果应用未显示，最常见的原因是清单中的错误，尤其是应用、机器人和消息扩展的 ID。</span><span class="sxs-lookup"><span data-stu-id="e6f97-129">If your app does not appear, the most common reason is an error in the manifest, particularly IDs for the app, bot, and messaging extensions.</span></span> <span data-ttu-id="e6f97-130">如果应用未针对对话进行范围限制，则不显示该选项。</span><span class="sxs-lookup"><span data-stu-id="e6f97-130">If the app is not scoped for conversations that option does not appear.</span></span>

>[!NOTE]
> <span data-ttu-id="e6f97-131">对话中的应用当前位于 [开发者预览版](../../resources/dev-preview/developer-preview-intro.md)中，如果 Teams 未以该模式运行，则不显示此选项。</span><span class="sxs-lookup"><span data-stu-id="e6f97-131">Apps in conversations is currently in [Developer Preview](../../resources/dev-preview/developer-preview-intro.md), and the option does not appear if Teams is not running in that mode.</span></span>

![上传的机器人列表中的自动程序示例](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a><span data-ttu-id="e6f97-133">使用"应用"选项卡将程序包上传到团队</span><span class="sxs-lookup"><span data-stu-id="e6f97-133">Upload your package into a team using the Apps tab</span></span>

1. <span data-ttu-id="e6f97-134">在目标团队中，选择 **" (&#8943;) "** 管理团队 **"。**</span><span class="sxs-lookup"><span data-stu-id="e6f97-134">In the target team, choose **More options** (**&#8943;**) and select **Manage team**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e6f97-135">你必须是团队所有者，或者所有者必须授予用户访问权限，以添加相应的应用类型，此功能显示。</span><span class="sxs-lookup"><span data-stu-id="e6f97-135">You must be the team owner or the owner must give access to users to add the appropriate app types for this functionality to appear.</span></span>

2. <span data-ttu-id="e6f97-136">选择" **应用"** 选项卡，然后选择右下角 **的** "上载自定义应用"。</span><span class="sxs-lookup"><span data-stu-id="e6f97-136">Select the **Apps** tab and choose **Upload a custom app** on the lower right.</span></span>

   ![上载入口点](../../assets/images/UploadACustomApp.png)

3. <span data-ttu-id="e6f97-138">Select your .zip package from the computer.</span><span class="sxs-lookup"><span data-stu-id="e6f97-138">Select your .zip package from the computer.</span></span>

4. <span data-ttu-id="e6f97-139">可以在列表中看到已上传的应用。</span><span class="sxs-lookup"><span data-stu-id="e6f97-139">You can see your uploaded app in the list.</span></span>

   ![上传的机器人列表中的自动程序示例](../../assets/images/botinlist.jpg)

<span data-ttu-id="e6f97-141">如果你的应用未加载，最常见的原因是清单中的错误，尤其是应用、机器人和消息扩展的 ID。</span><span class="sxs-lookup"><span data-stu-id="e6f97-141">If your app does not load, the most common reason is an error in the manifest, particularly IDs for the app, bot, and messaging extensions.</span></span>

## <a name="access-your-uploaded-configurable-tab"></a><span data-ttu-id="e6f97-142">访问上传的可配置选项卡</span><span class="sxs-lookup"><span data-stu-id="e6f97-142">Access your uploaded configurable tab</span></span>

<span data-ttu-id="e6f97-143">如果应用包含选项卡，用户可以使用标准选项卡库流将其固定到任何对话或团队频道：</span><span class="sxs-lookup"><span data-stu-id="e6f97-143">If the app contains tabs, users can pin them to any conversation or team channel using the standard tab gallery flow:</span></span>

1. <span data-ttu-id="e6f97-144">转到团队中的频道。</span><span class="sxs-lookup"><span data-stu-id="e6f97-144">Go to a channel in the team.</span></span> <span data-ttu-id="e6f97-145">选择 **+** 将选项卡添加到现有选项卡的右侧。</span><span class="sxs-lookup"><span data-stu-id="e6f97-145">Choose **+** to add a tab to the right of the existing tabs.</span></span>

2. <span data-ttu-id="e6f97-146">从出现的库中选择您的选项卡。</span><span class="sxs-lookup"><span data-stu-id="e6f97-146">Select your tab from the gallery that appears.</span></span>

3. <span data-ttu-id="e6f97-147">接受同意提示。</span><span class="sxs-lookup"><span data-stu-id="e6f97-147">Accept the consent prompt.</span></span>

4. <span data-ttu-id="e6f97-148">通过配置页面配置 [您的选项卡，然后选择](../../tabs/how-to/create-tab-pages/configuration-page.md)"保存 **"。**</span><span class="sxs-lookup"><span data-stu-id="e6f97-148">Configure your tab through its [configuration page](../../tabs/how-to/create-tab-pages/configuration-page.md) and select **Save**.</span></span>

  !["添加选项卡"对话框，包含可用选项卡的库](../../assets/images/tab_gallery.png)

## <a name="access-your-uploaded-bot"></a><span data-ttu-id="e6f97-150">访问上传的机器人</span><span class="sxs-lookup"><span data-stu-id="e6f97-150">Access your uploaded bot</span></span>

<span data-ttu-id="e6f97-151">将机器人添加到团队后，该团队的任何人都可以在团队频道内外使用，具体取决于机器人范围定义。</span><span class="sxs-lookup"><span data-stu-id="e6f97-151">After adding the bot to a team, it must be usable by anyone on that team, inside and outside the team channels, depending on bot scope definition.</span></span> <span data-ttu-id="e6f97-152">所有团队成员都可以在常规频道中查看一个帖子，指示机器人已添加到团队。</span><span class="sxs-lookup"><span data-stu-id="e6f97-152">All team members can see a post in the **General** channel indicating that the bot has been added to the team.</span></span>

<span data-ttu-id="e6f97-153">对于 Teams 自动程序，你可以首先调用@mentioning自动程序的名称。</span><span class="sxs-lookup"><span data-stu-id="e6f97-153">For a Teams bot, you can start by invoking your bot by @mentioning the name of the bot.</span></span>

<span data-ttu-id="e6f97-154">若要测试与机器人的直接聊天，可以通过应用主页访问它，@mention频道中，或在"新建聊天"窗口中 **搜索** 它。</span><span class="sxs-lookup"><span data-stu-id="e6f97-154">To test direct chats with your bot, you can either access it through the App home, @mention it in a channel, or search for it in the **New Chat** window.</span></span>

<span data-ttu-id="e6f97-155">你可以@mention聊天机器人，或在"新建聊天"窗口中搜索它以测试与机器人的直接聊天。</span><span class="sxs-lookup"><span data-stu-id="e6f97-155">You can @mention the bot in a conversation or search for it in the **New Chat** window to test direct chats with your bot.</span></span>

## <a name="access-your-uploaded-connector"></a><span data-ttu-id="e6f97-156">访问上传的连接器</span><span class="sxs-lookup"><span data-stu-id="e6f97-156">Access your uploaded Connector</span></span>

<span data-ttu-id="e6f97-157">在团队或对话中加载应用后，用户可以使用标准连接器库流设置连接器：</span><span class="sxs-lookup"><span data-stu-id="e6f97-157">With the app loaded in the team or conversation, users can set up a Connector using the standard Connectors gallery flow:</span></span>

1. <span data-ttu-id="e6f97-158">转到团队中的频道。</span><span class="sxs-lookup"><span data-stu-id="e6f97-158">Go to a channel in the team.</span></span> <span data-ttu-id="e6f97-159">Choose **More options (** *&#8943;*) and choose **Connectors**.</span><span class="sxs-lookup"><span data-stu-id="e6f97-159">Choose **More options** (*&#8943;*) and choose **Connectors**.</span></span>

2. <span data-ttu-id="e6f97-160">从底部的旁 **加载部分选择** 连接器。</span><span class="sxs-lookup"><span data-stu-id="e6f97-160">Select your Connector from the **Sideloaded** section at the bottom.</span></span>

3. <span data-ttu-id="e6f97-161">通过配置页面配置 [连接器，然后选择](../../webhooks-and-connectors/how-to/connectors-creating.md)"保存 **"。**</span><span class="sxs-lookup"><span data-stu-id="e6f97-161">Configure your connector through its [configuration page](../../webhooks-and-connectors/how-to/connectors-creating.md) and select **Save**.</span></span>

  !["添加选项卡"对话框，包含可用选项卡的库。](../../assets/images/connector_gallery.png)

## <a name="access-your-uploaded-messaging-extension"></a><span data-ttu-id="e6f97-163">访问上传的消息扩展</span><span class="sxs-lookup"><span data-stu-id="e6f97-163">Access your uploaded messaging extension</span></span>

<span data-ttu-id="e6f97-164">具有邮件扩展名的已上传应用会自动显示在撰写框的" (&#8943;) "菜单中。</span><span class="sxs-lookup"><span data-stu-id="e6f97-164">An uploaded app with a messaging extension automatically appears in the **More options** (*&#8943;*) menu in the compose box.</span></span>

![消息扩展](../../assets/images/compose-extensions/cesampleapp.png)


## <a name="remove-or-update-your-app"></a><span data-ttu-id="e6f97-166">删除或更新应用</span><span class="sxs-lookup"><span data-stu-id="e6f97-166">Remove or update your app</span></span>

<span data-ttu-id="e6f97-167">若要删除应用，请在"查看 **Teams** 机器人"列表中选择应用名称旁边的删除图标。</span><span class="sxs-lookup"><span data-stu-id="e6f97-167">To remove your app, select the delete icon next to the app name in the **View Teams** bots list.</span></span> <span data-ttu-id="e6f97-168">如果你更改清单信息，首先删除应用，然后添加更新的程序包，请参阅 [将程序包加载到团队](#load-your-package-into-teams)。</span><span class="sxs-lookup"><span data-stu-id="e6f97-168">If you change manifest information, first remove the app and then add the updated package, see [Load your package into a team](#load-your-package-into-teams).</span></span> <span data-ttu-id="e6f97-169">服务上的代码更改不需要您再次上载清单。</span><span class="sxs-lookup"><span data-stu-id="e6f97-169">Code changes on your service do not require you to upload your manifest again.</span></span> <span data-ttu-id="e6f97-170">但是，如果代码更改需要清单更新（例如 URL 的更改或自动程序 Microsoft 应用 ID 的更改），则必须再次上载清单。</span><span class="sxs-lookup"><span data-stu-id="e6f97-170">However, if the code changes require manifest updates, such as changes to the URL or the Microsoft app ID for its bot, you must upload the manifest again.</span></span>

> [!NOTE]
> <span data-ttu-id="e6f97-171">无法从个人上下文中完全删除自动程序。</span><span class="sxs-lookup"><span data-stu-id="e6f97-171">You cannot remove a bot from a personal context entirely.</span></span> <span data-ttu-id="e6f97-172">如果删除并再次添加自动程序，则与自动程序的其他通信将附加到上一个对话中。</span><span class="sxs-lookup"><span data-stu-id="e6f97-172">If the bot is removed and added again, additional communication with the bot appends to the previous conversation.</span></span>

## <a name="troubleshooting-notes"></a><span data-ttu-id="e6f97-173">疑难解答说明</span><span class="sxs-lookup"><span data-stu-id="e6f97-173">Troubleshooting notes</span></span>

<span data-ttu-id="e6f97-174">如果清单无法加载，请检查是否按照创建程序包中的说明操作，并针对[](../../concepts/build-and-test/apps-package.md)架构验证[清单](../../resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="e6f97-174">If the manifest fails to load, check if you have followed all the instructions in [Create the package](../../concepts/build-and-test/apps-package.md) and validated your manifest against the [schema](../../resources/schema/manifest-schema.md).</span></span>
