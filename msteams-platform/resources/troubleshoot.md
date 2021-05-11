---
title: 应用疑难解答
description: 解决生成适用于 Microsoft Teams 的应用时的问题或Microsoft Teams
keywords: teams 应用开发疑难解答
localization_priority: Normal
ms.topic: troubleshooting
ms.date: 07/09/2018
ms.openlocfilehash: ce45a75869e8b6694cd84c10f8fac1f9bd55bad4
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020427"
---
# <a name="troubleshoot-your-microsoft-teams-app"></a><span data-ttu-id="d8c6e-104">对应用Microsoft Teams疑难解答</span><span class="sxs-lookup"><span data-stu-id="d8c6e-104">Troubleshoot your Microsoft Teams app</span></span>

## <a name="troubleshooting-tabs"></a><span data-ttu-id="d8c6e-105">疑难解答选项卡</span><span class="sxs-lookup"><span data-stu-id="d8c6e-105">Troubleshooting tabs</span></span>

### <a name="accessing-the-devtools"></a><span data-ttu-id="d8c6e-106">访问 DevTools</span><span class="sxs-lookup"><span data-stu-id="d8c6e-106">Accessing the DevTools</span></span>

<span data-ttu-id="d8c6e-107">可以在 Teams 客户端中打开[DevTools，](~/tabs/how-to/developer-tools.md)获得与在浏览器中按 Windows) 上的 F12 (或 MacOS) 上的 Command-Option-I (类似的体验。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-107">You can open [DevTools in the Teams client](~/tabs/how-to/developer-tools.md) for a similar experience as pressing F12 (on Windows) or Command-Option-I (on MacOS) in a browser.</span></span>

### <a name="blank-tab-screen"></a><span data-ttu-id="d8c6e-108">空白选项卡屏幕</span><span class="sxs-lookup"><span data-stu-id="d8c6e-108">Blank tab screen</span></span>

<span data-ttu-id="d8c6e-109">如果在选项卡视图中看不到内容，可能是：</span><span class="sxs-lookup"><span data-stu-id="d8c6e-109">If you are not seeing your content in the tab view, it could be:</span></span>

* <span data-ttu-id="d8c6e-110">内容无法在 中显示 `<iframe>` 。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-110">your content cannot be displayed in an `<iframe>`.</span></span>
* <span data-ttu-id="d8c6e-111">内容域不在清单 [的 validDomains](~/resources/schema/manifest-schema.md#validdomains) 列表中。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-111">the content domain is not in the [validDomains](~/resources/schema/manifest-schema.md#validdomains) list in the manifest.</span></span>

### <a name="the-save-button-isnt-enabled-on-the-settings-dialog"></a><span data-ttu-id="d8c6e-112">"保存"按钮未在设置对话框中启用</span><span class="sxs-lookup"><span data-stu-id="d8c6e-112">The Save button isn't enabled on the settings dialog</span></span>

<span data-ttu-id="d8c6e-113">请确保在用户输入或选择了设置页面上的所有必需数据后调用以 `microsoftTeams.settings.setValidityState(true)` 启用保存按钮。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-113">Be sure to call `microsoftTeams.settings.setValidityState(true)` once the user has input or selected all required data on your settings page to enable the save button.</span></span>

### <a name="after-selecting-the-save-button-the-tab-settings-cannot-be-saved"></a><span data-ttu-id="d8c6e-114">选择"保存"按钮后，无法保存选项卡设置</span><span class="sxs-lookup"><span data-stu-id="d8c6e-114">After selecting the Save button, the tab settings cannot be saved</span></span>

<span data-ttu-id="d8c6e-115">添加选项卡时，如果单击保存按钮，但显示一条指示无法保存设置的错误消息，则问题可能是两类问题之一：</span><span class="sxs-lookup"><span data-stu-id="d8c6e-115">When adding a tab, if you click the save buttons but are presented with an error message indicating the settings cannot be saved, the problem could be one of two classes of issues:</span></span>

* <span data-ttu-id="d8c6e-116">从未收到保存成功消息。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-116">The save success message was never received.</span></span> <span data-ttu-id="d8c6e-117">如果保存处理程序是使用 注册 `microsoftTeams.settings.registerOnSaveHandler(handler)` 的，则回调必须调用 `saveEvent.notifySuccess()` 。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-117">If a save handler was registered using `microsoftTeams.settings.registerOnSaveHandler(handler)`, the callback must call `saveEvent.notifySuccess()`.</span></span> <span data-ttu-id="d8c6e-118">如果回调未在 30 秒内调用它或改为调用， `saveEvent.notifyFailure(reason)` 将显示此错误。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-118">If the callback doesn't call this within 30 seconds or calls `saveEvent.notifyFailure(reason)` instead, this error will be shown.</span></span>

* <span data-ttu-id="d8c6e-119">如果未注册任何保存处理程序，将在用户选择保存按钮时 `saveEvent.notifySuccess()` 立即自动进行调用。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-119">If no save handler was registered, the `saveEvent.notifySuccess()` call is automatically made immediately upon the user selecting the save button.</span></span>

* <span data-ttu-id="d8c6e-120">提供的设置无效。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-120">The provided settings were invalid.</span></span> <span data-ttu-id="d8c6e-121">无法保存设置的另一个原因是，如果调用提供的设置对象无效，或者根本不会 `microsoftTeams.setSettings(settings)` 进行调用。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-121">The other reason the settings may not be saved is if the call to `microsoftTeams.setSettings(settings)` provided an invalid settings object, or the call wasn't made at all.</span></span> <span data-ttu-id="d8c6e-122">请参阅下一部分设置对象的常见问题。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-122">See the next section, Common problems with the settings object.</span></span>

### <a name="common-problems-with-the-settings-object"></a><span data-ttu-id="d8c6e-123">设置对象的常见问题</span><span class="sxs-lookup"><span data-stu-id="d8c6e-123">Common problems with the settings object</span></span>

* <span data-ttu-id="d8c6e-124">`settings.entityId` 缺少。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-124">`settings.entityId` is missing.</span></span> <span data-ttu-id="d8c6e-125">此字段属于必填字段。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-125">This field is required.</span></span>
* <span data-ttu-id="d8c6e-126">`settings.contentUrl` 缺少。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-126">`settings.contentUrl` is missing.</span></span> <span data-ttu-id="d8c6e-127">此字段属于必填字段。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-127">This field is required.</span></span>
* <span data-ttu-id="d8c6e-128">`settings.contentUrl` 或可选 `settings.removeUrl` ， 或 `settings.websiteUrl` 提供，但无效。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-128">`settings.contentUrl` or the optional `settings.removeUrl`, or `settings.websiteUrl` are provided but not valid.</span></span> <span data-ttu-id="d8c6e-129">URL 必须使用 HTTPS，并且还必须是设置页的同一域或在清单列表中 `validDomains` 指定。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-129">The URLs must use HTTPS and also must either be the same domain as the settings page or specified in the manifest's `validDomains` list.</span></span>

### <a name="cant-authenticate-the-user-or-display-your-auth-provider-in-your-tab"></a><span data-ttu-id="d8c6e-130">无法对用户进行身份验证或在选项卡中显示身份验证提供程序</span><span class="sxs-lookup"><span data-stu-id="d8c6e-130">Can't authenticate the user or display your auth provider in your tab</span></span>

<span data-ttu-id="d8c6e-131">除非执行无提示身份验证，否则必须遵循 JavaScript 客户端 SDK Microsoft Teams[身份验证过程](/javascript/api/overview/msteams-client.md)。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-131">Unless you are doing silent authentication, you must follow the authentication process provided by the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client.md).</span></span>

> [!NOTE]
><span data-ttu-id="d8c6e-132">要求所有身份验证流在域上开始和结束，必须在清单中的 `validDomains` 对象中列出。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-132">We require all authentication flow to start and end on your domain, which must be listed in the `validDomains` object in your manifest.</span></span>

<span data-ttu-id="d8c6e-133">有关身份验证详细信息，请参阅验证 [用户](~/concepts/authentication/authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-133">For more information about authentication, please see [Authenticate a user](~/concepts/authentication/authentication.md).</span></span>

### <a name="static-tabs-not-showing-up"></a><span data-ttu-id="d8c6e-134">未显示静态选项卡</span><span class="sxs-lookup"><span data-stu-id="d8c6e-134">Static tabs not showing up</span></span>

<span data-ttu-id="d8c6e-135">存在一个已知问题，即从个人聊天对话访问应用时，使用新的或更新的静态选项卡更新现有自动程序应用时不会显示该选项卡更改。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-135">There is a known issue where updating an existing bot app with a new or updated static tab will not show that tab change when accessing the app from a personal chat conversation.</span></span>  <span data-ttu-id="d8c6e-136">To see the change， you should test on a new user or test instance， or access the bot from the Apps flyout.</span><span class="sxs-lookup"><span data-stu-id="d8c6e-136">To see the change, you should test on a new user or test instance, or access the bot from the Apps flyout.</span></span>

## <a name="troubleshooting-bots"></a><span data-ttu-id="d8c6e-137">自动程序疑难解答</span><span class="sxs-lookup"><span data-stu-id="d8c6e-137">Troubleshooting bots</span></span>

### <a name="cant-add-my-bot"></a><span data-ttu-id="d8c6e-138">无法添加我的机器人</span><span class="sxs-lookup"><span data-stu-id="d8c6e-138">Can't add my bot</span></span>

<span data-ttu-id="d8c6e-139">应用必须由租户管理员Office 365才能由最终用户加载。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-139">Apps must be enabled by the Office 365 tenant admin for them to be loaded by end users.</span></span> <span data-ttu-id="d8c6e-140">请注意，在某些情况下，Office 365租户可能有多个与其关联的 SK，并且对于在任何 SK 中工作的自动程序，必须在所有 SK 中启用它们。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-140">Note that in some cases, the Office 365 tenant might have multiple SKUs associated with it, and for bots to work in any, they must be enabled in all SKUs.</span></span> <span data-ttu-id="d8c6e-141">有关详细信息[，请参阅Office 365](~/concepts/build-and-test/prepare-your-o365-tenant.md)租户。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-141">See [Prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md) for more information.</span></span>

### <a name="cant-add-bot-as-a-member-of-a-team"></a><span data-ttu-id="d8c6e-142">无法将机器人添加为团队成员</span><span class="sxs-lookup"><span data-stu-id="d8c6e-142">Can't add bot as a member of a team</span></span>

<span data-ttu-id="d8c6e-143">必须先将聊天机器人上传到团队，然后才能在团队的任何频道中访问它。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-143">Bots must first be upload into a team before it is accessible within any channel of that team.</span></span> <span data-ttu-id="d8c6e-144">有关 [此过程详细信息](~/concepts/deploy-and-publish/apps-upload.md) ，请查看在团队中上载应用。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-144">Please review [Uploading your app in a team](~/concepts/deploy-and-publish/apps-upload.md) for more information on this process.</span></span>

### <a name="my-bot-doesnt-get-my-message-in-a-channel"></a><span data-ttu-id="d8c6e-145">我的机器人不会在频道中收到我的消息</span><span class="sxs-lookup"><span data-stu-id="d8c6e-145">My bot doesn't get my message in a channel</span></span>

<span data-ttu-id="d8c6e-146">频道中的自动程序仅在显式@mentioned接收消息，即使您回复的是以前的自动程序消息。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-146">Bots in channels receive messages only when they are explicitly @mentioned, even if you are replying to a previous bot message.</span></span> <span data-ttu-id="d8c6e-147">在邮件中可能看不到自动程序名称的唯一例外是，如果自动程序由于最初发送的 `imBack` CardAction 而收到操作。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-147">The only exception where you might not see the bot name in a message is if the bot receives an `imBack` action as a result of a CardAction that it originally sent.</span></span>

### <a name="my-bot-doesnt-understand-my-commands-when-in-a-channel"></a><span data-ttu-id="d8c6e-148">在频道中时，我的机器人无法理解我的命令</span><span class="sxs-lookup"><span data-stu-id="d8c6e-148">My bot doesn't understand my commands when in a channel</span></span>

<span data-ttu-id="d8c6e-149">由于频道中的机器人仅在收到@mentioned时接收消息，因此机器人在频道中接收的所有消息@mention文本字段中。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-149">Because bots in channels only receive messages when they are @mentioned, all messages that your bot receives in a channel include that @mention in the text field.</span></span> <span data-ttu-id="d8c6e-150">最佳做法是在传入的文本消息中分离自动程序名称本身，然后再传递到分析逻辑。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-150">It is a best practice to strip the bot name itself out of all incoming text messages before passing along to your parsing logic.</span></span> <span data-ttu-id="d8c6e-151">查看 [提及](../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions) ，获取有关如何处理此案例的提示。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-151">Review [mentions](../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions) for tips on how to handle this case.</span></span>

## <a name="issues-with-packaging-and-uploading"></a><span data-ttu-id="d8c6e-152">打包和上载问题</span><span class="sxs-lookup"><span data-stu-id="d8c6e-152">Issues with packaging and uploading</span></span>

### <a name="error-while-reading-manifestjson"></a><span data-ttu-id="d8c6e-153">在打开时manifest.js错误</span><span class="sxs-lookup"><span data-stu-id="d8c6e-153">Error while reading manifest.json</span></span>

<span data-ttu-id="d8c6e-154">大多数清单错误都提供特定字段缺失或无效的提示。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-154">Most  manifest errors will provide a hint at what specific field is missing or invalid.</span></span> <span data-ttu-id="d8c6e-155">但是，如果 JSON 文件无法读取为 JSON，则使用这个常规错误消息。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-155">However, if the JSON file cannot be read as JSON at all, this generic error message is used.</span></span>

<span data-ttu-id="d8c6e-156">清单读取错误的常见原因：</span><span class="sxs-lookup"><span data-stu-id="d8c6e-156">Common reasons for manifest read errors:</span></span>

* <span data-ttu-id="d8c6e-157">无效的 JSON。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-157">Invalid JSON.</span></span> <span data-ttu-id="d8c6e-158">使用 IDE（如[Visual Studio Code](https://code.visualstudio.com)或[Visual Studio）](https://www.visualstudio.com/vs/)自动验证 JSON 语法。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-158">Use an IDE such as [Visual Studio Code](https://code.visualstudio.com) or [Visual Studio](https://www.visualstudio.com/vs/) that automatically validates the JSON syntax.</span></span>
* <span data-ttu-id="d8c6e-159">编码问题。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-159">Encoding issues.</span></span> <span data-ttu-id="d8c6e-160">对 on 文件使用 UTF-8 *manifest.jsUTF-8。*</span><span class="sxs-lookup"><span data-stu-id="d8c6e-160">Use UTF-8 for the *manifest.json* file.</span></span> <span data-ttu-id="d8c6e-161">其他编码（特别是 BOM 编码）可能无法读取。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-161">Other encodings, specifically with the BOM, may not be readable.</span></span>
* <span data-ttu-id="d8c6e-162">程序包格式.zip格式。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-162">Malformed .zip package.</span></span> <span data-ttu-id="d8c6e-163">on *manifest.js* 文件必须位于文件.zip级别。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-163">The *manifest.json* file must be at the top level of the .zip file.</span></span> <span data-ttu-id="d8c6e-164">请注意，默认 Mac 文件压缩可能会将manifest.js放在子目录中，这样将不会在Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-164">Note that default Mac file compression might place the *manifest.json* in a subdirectory, which will not properly load in Microsoft Teams.</span></span>

### <a name="another-extension-with-same-id-exists"></a><span data-ttu-id="d8c6e-165">存在另一个 ID 相同的扩展</span><span class="sxs-lookup"><span data-stu-id="d8c6e-165">Another extension with same ID exists</span></span>

<span data-ttu-id="d8c6e-166">如果试图重新上传 ID 相同的更新程序包，请选择选项卡的表格行末尾的"替换"图标，而不是选择"Upload"**按钮**。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-166">If you're attempting to re-upload an updated package with the same ID, choose the **Replace** icon at the end of the tab's table row rather than the **Upload** button.</span></span>

<span data-ttu-id="d8c6e-167">如果未重新上载更新的程序包，请确保 ID 是唯一的。</span><span class="sxs-lookup"><span data-stu-id="d8c6e-167">If you're not re-uploading an updated package, ensure that the ID is unique.</span></span>
