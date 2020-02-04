---
title: 对应用程序进行故障排除
description: 在为 Microsoft 团队构建应用程序时解决问题或出现的错误
keywords: 团队应用程序开发故障排除
ms.date: 07/09/2018
ms.openlocfilehash: f7fe42e7c1f3ff2c4d8d1cbe81ed8f71e6c04384
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673017"
---
# <a name="troubleshoot-your-microsoft-teams-app"></a><span data-ttu-id="b5537-104">对 Microsoft 团队应用程序进行故障排除</span><span class="sxs-lookup"><span data-stu-id="b5537-104">Troubleshoot your Microsoft Teams app</span></span>

## <a name="troubleshooting-tabs"></a><span data-ttu-id="b5537-105">疑难解答选项卡</span><span class="sxs-lookup"><span data-stu-id="b5537-105">Troubleshooting tabs</span></span>

### <a name="accessing-the-devtools"></a><span data-ttu-id="b5537-106">访问 DevTools</span><span class="sxs-lookup"><span data-stu-id="b5537-106">Accessing the DevTools</span></span>

<span data-ttu-id="b5537-107">您可以在[团队客户端中打开 DevTools](~/tabs/how-to/developer-tools.md) ，使其类似于在浏览器中按 F12 （在 Windows 中）或命令-选项-I （在 MacOS 上）的类似体验。</span><span class="sxs-lookup"><span data-stu-id="b5537-107">You can open [DevTools in the Teams client](~/tabs/how-to/developer-tools.md) for a similar experience as pressing F12 (on Windows) or Command-Option-I (on MacOS) in a browser.</span></span>

### <a name="blank-tab-screen"></a><span data-ttu-id="b5537-108">空白选项卡屏幕</span><span class="sxs-lookup"><span data-stu-id="b5537-108">Blank tab screen</span></span>

<span data-ttu-id="b5537-109">如果您不在选项卡视图中看到您的内容，则可能是：</span><span class="sxs-lookup"><span data-stu-id="b5537-109">If you are not seeing your content in the tab view, it could be:</span></span>

* <span data-ttu-id="b5537-110">无法在中显示您的`<iframe>`内容。</span><span class="sxs-lookup"><span data-stu-id="b5537-110">your content cannot be displayed in an `<iframe>`.</span></span>
* <span data-ttu-id="b5537-111">内容域不在清单中的[validDomains](~/resources/schema/manifest-schema.md#validdomains)列表中。</span><span class="sxs-lookup"><span data-stu-id="b5537-111">the content domain is not in the [validDomains](~/resources/schema/manifest-schema.md#validdomains) list in the manifest.</span></span>

### <a name="the-save-button-isnt-enabled-on-the-settings-dialog"></a><span data-ttu-id="b5537-112">"设置" 对话框中未启用 "保存" 按钮</span><span class="sxs-lookup"><span data-stu-id="b5537-112">The Save button isn't enabled on the settings dialog</span></span>

<span data-ttu-id="b5537-113">在用户输入或`microsoftTeams.settings.setValidityState(true)`选择 "设置" 页上的 "所有需要的数据" 以启用 "保存" 按钮时，请务必调用。</span><span class="sxs-lookup"><span data-stu-id="b5537-113">Be sure to call `microsoftTeams.settings.setValidityState(true)` once the user has input or selected all required data on your settings page to enable the save button.</span></span>

### <a name="after-selecting-the-save-button-the-tab-settings-cannot-be-saved"></a><span data-ttu-id="b5537-114">选择 "保存" 按钮后，不能保存选项卡设置</span><span class="sxs-lookup"><span data-stu-id="b5537-114">After selecting the Save button, the tab settings cannot be saved</span></span>

<span data-ttu-id="b5537-115">添加选项卡时，如果单击 "保存" 按钮，但显示一条错误消息，指示无法保存设置，则问题可能是以下两类问题之一：</span><span class="sxs-lookup"><span data-stu-id="b5537-115">When adding a tab, if you click the save buttons but are presented with an error message indicating the settings cannot be saved, the problem could be one of two classes of issues:</span></span>

* <span data-ttu-id="b5537-116">从未收到 "保存成功" 消息。</span><span class="sxs-lookup"><span data-stu-id="b5537-116">The save success message was never received.</span></span> <span data-ttu-id="b5537-117">如果保存的处理程序是使用`microsoftTeams.settings.registerOnSaveHandler(handler)`注册的，则回调`saveEvent.notifySuccess()`必须调用。</span><span class="sxs-lookup"><span data-stu-id="b5537-117">If a save handler was registered using `microsoftTeams.settings.registerOnSaveHandler(handler)`, the callback must call `saveEvent.notifySuccess()`.</span></span> <span data-ttu-id="b5537-118">如果回调在30秒`saveEvent.notifyFailure(reason)`内不调用此请求，则将显示此错误。</span><span class="sxs-lookup"><span data-stu-id="b5537-118">If the callback doesn't call this within 30 seconds or calls `saveEvent.notifyFailure(reason)` instead, this error will be shown.</span></span>

* <span data-ttu-id="b5537-119">如果未注册保存处理程序，则`saveEvent.notifySuccess()`会在用户选择 "保存" 按钮后立即自动进行呼叫。</span><span class="sxs-lookup"><span data-stu-id="b5537-119">If no save handler was registered, the `saveEvent.notifySuccess()` call is automatically made immediately upon the user selecting the save button.</span></span>

* <span data-ttu-id="b5537-120">提供的设置无效。</span><span class="sxs-lookup"><span data-stu-id="b5537-120">The provided settings were invalid.</span></span> <span data-ttu-id="b5537-121">可能不会保存设置的另一个原因是，调用`microsoftTeams.setSettings(settings)`提供了无效的设置对象，或者根本没有进行呼叫。</span><span class="sxs-lookup"><span data-stu-id="b5537-121">The other reason the settings may not be saved is if the call to `microsoftTeams.setSettings(settings)` provided an invalid settings object, or the call wasn't made at all.</span></span> <span data-ttu-id="b5537-122">请参阅下一节常见的设置对象问题。</span><span class="sxs-lookup"><span data-stu-id="b5537-122">See the next section, Common problems with the settings object.</span></span>

### <a name="common-problems-with-the-settings-object"></a><span data-ttu-id="b5537-123">设置对象的常见问题</span><span class="sxs-lookup"><span data-stu-id="b5537-123">Common problems with the settings object</span></span>

* <span data-ttu-id="b5537-124">`settings.entityId`缺失。</span><span class="sxs-lookup"><span data-stu-id="b5537-124">`settings.entityId` is missing.</span></span> <span data-ttu-id="b5537-125">此字段属于必填字段。</span><span class="sxs-lookup"><span data-stu-id="b5537-125">This field is required.</span></span>
* <span data-ttu-id="b5537-126">`settings.contentUrl`缺失。</span><span class="sxs-lookup"><span data-stu-id="b5537-126">`settings.contentUrl` is missing.</span></span> <span data-ttu-id="b5537-127">此字段属于必填字段。</span><span class="sxs-lookup"><span data-stu-id="b5537-127">This field is required.</span></span>
* <span data-ttu-id="b5537-128">`settings.contentUrl`或者是可选`settings.removeUrl`的， `settings.websiteUrl`或者已提供但无效。</span><span class="sxs-lookup"><span data-stu-id="b5537-128">`settings.contentUrl` or the optional `settings.removeUrl`, or `settings.websiteUrl` are provided but not valid.</span></span> <span data-ttu-id="b5537-129">Url 必须使用 HTTPS，并且也必须与设置页面的域相同，或在清单的`validDomains`列表中指定。</span><span class="sxs-lookup"><span data-stu-id="b5537-129">The URLs must use HTTPS and also must either be the same domain as the settings page or specified in the manifest's `validDomains` list.</span></span>

### <a name="cant-authenticate-the-user-or-display-your-auth-provider-in-your-tab"></a><span data-ttu-id="b5537-130">无法对用户进行身份验证或在你的选项卡中显示你的身份验证提供程序</span><span class="sxs-lookup"><span data-stu-id="b5537-130">Can't authenticate the user or display your auth provider in your tab</span></span>

<span data-ttu-id="b5537-131">除非您正在进行无提示的身份验证，否则必须遵循[Microsoft 团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client.md)提供的身份验证过程。</span><span class="sxs-lookup"><span data-stu-id="b5537-131">Unless you are doing silent authentication, you must follow the authentication process provided by the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client.md).</span></span>

> [!NOTE]
><span data-ttu-id="b5537-132">我们需要所有身份验证流在你的域中开始和结束，这必须在你`validDomains`的清单中的对象中列出。</span><span class="sxs-lookup"><span data-stu-id="b5537-132">We require all authentication flow to start and end on your domain, which must be listed in the `validDomains` object in your manifest.</span></span>

<span data-ttu-id="b5537-133">有关身份验证的详细信息，请参阅[对用户进行身份验证](~/concepts/authentication/authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="b5537-133">For more information about authentication, please see [Authenticate a user](~/concepts/authentication/authentication.md).</span></span>

### <a name="static-tabs-not-showing-up"></a><span data-ttu-id="b5537-134">未显示静态选项卡</span><span class="sxs-lookup"><span data-stu-id="b5537-134">Static tabs not showing up</span></span>

<span data-ttu-id="b5537-135">在使用新的或已更新的静态选项卡更新现有机器人应用程序时，将不会在从个人聊天对话中访问应用程序时显示该选项卡更改的已知问题。</span><span class="sxs-lookup"><span data-stu-id="b5537-135">There is a known issue where updating an existing bot app with a new or updated static tab will not show that tab change when accessing the app from a personal chat conversation.</span></span>  <span data-ttu-id="b5537-136">若要查看更改，应在新用户或测试实例上进行测试，或从 "应用" 浮出控件中访问机器人。</span><span class="sxs-lookup"><span data-stu-id="b5537-136">To see the change, you should test on a new user or test instance, or access the bot from the Apps flyout.</span></span>

## <a name="troubleshooting-bots"></a><span data-ttu-id="b5537-137">故障排除机器人</span><span class="sxs-lookup"><span data-stu-id="b5537-137">Troubleshooting bots</span></span>

### <a name="cant-add-my-bot"></a><span data-ttu-id="b5537-138">无法添加我的机器人</span><span class="sxs-lookup"><span data-stu-id="b5537-138">Can't add my bot</span></span>

<span data-ttu-id="b5537-139">若要由最终用户加载的应用程序必须由 Office 365 租户管理员启用。</span><span class="sxs-lookup"><span data-stu-id="b5537-139">Apps must be enabled by the Office 365 tenant admin for them to be loaded by end users.</span></span> <span data-ttu-id="b5537-140">请注意，在某些情况下，Office 365 租户可能会有多个与之关联的 Sku，并且要使用的 bot 必须在所有 Sku 中启用它们。</span><span class="sxs-lookup"><span data-stu-id="b5537-140">Note that in some cases, the Office 365 tenant might have multiple SKUs associated with it, and for bots to work in any, they must be enabled in all SKUs.</span></span> <span data-ttu-id="b5537-141">有关详细信息，请参阅[准备 Office 365 租户](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="b5537-141">See [Prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md) for more information.</span></span>

### <a name="cant-add-bot-as-a-member-of-a-team"></a><span data-ttu-id="b5537-142">无法将 bot 添加为团队成员</span><span class="sxs-lookup"><span data-stu-id="b5537-142">Can't add bot as a member of a team</span></span>

<span data-ttu-id="b5537-143">必须先将 bot 上载到团队中，然后才能在该团队的任何频道中访问它。</span><span class="sxs-lookup"><span data-stu-id="b5537-143">Bots must first be upload into a team before it is accessible within any channel of that team.</span></span> <span data-ttu-id="b5537-144">有关此过程的详细信息，请参阅在[团队中上传您的应用程序](~/concepts/deploy-and-publish/apps-upload.md)。</span><span class="sxs-lookup"><span data-stu-id="b5537-144">Please review [Uploading your app in a team](~/concepts/deploy-and-publish/apps-upload.md) for more information on this process.</span></span>

### <a name="my-bot-doesnt-get-my-message-in-a-channel"></a><span data-ttu-id="b5537-145">我的 bot 在频道中没有收到我的邮件</span><span class="sxs-lookup"><span data-stu-id="b5537-145">My bot doesn't get my message in a channel</span></span>

<span data-ttu-id="b5537-146">频道中的 bot 仅在明确 @mentioned 时才接收邮件，即使您要回复以前的 bot 邮件也是如此。</span><span class="sxs-lookup"><span data-stu-id="b5537-146">Bots in channels receive messages only when they are explicitly @mentioned, even if you are replying to a previous bot message.</span></span> <span data-ttu-id="b5537-147">您可能不会在邮件中看到 bot 名称的唯一例外是，如果 bot 收到的`imBack`操作是它最初发送的 CardAction 的结果。</span><span class="sxs-lookup"><span data-stu-id="b5537-147">The only exception where you might not see the bot name in a message is if the bot receives an `imBack` action as a result of a CardAction that it originally sent.</span></span>

### <a name="my-bot-doesnt-understand-my-commands-when-in-a-channel"></a><span data-ttu-id="b5537-148">在频道中时，我的 bot 不理解我的命令</span><span class="sxs-lookup"><span data-stu-id="b5537-148">My bot doesn't understand my commands when in a channel</span></span>

<span data-ttu-id="b5537-149">由于通道中的 bot 仅在 @mentioned 时收到邮件，因此你的 bot 在通道中接收的所有邮件都包含该 @mention 在文本字段中。</span><span class="sxs-lookup"><span data-stu-id="b5537-149">Because bots in channels only receive messages when they are @mentioned, all messages that your bot receives in a channel include that @mention in the text field.</span></span> <span data-ttu-id="b5537-150">最好将 bot 名称本身从所有传入的短信中去除，然后再传递给分析逻辑。</span><span class="sxs-lookup"><span data-stu-id="b5537-150">It is a best practice to strip the bot name itself out of all incoming text messages before passing along to your parsing logic.</span></span> <span data-ttu-id="b5537-151">查看[提及](~/bots/how-to/conversations/channel-and-group-conversations.md#working-with--mentions)，了解有关如何处理这种情况的提示。</span><span class="sxs-lookup"><span data-stu-id="b5537-151">Review [Mentions](~/bots/how-to/conversations/channel-and-group-conversations.md#working-with--mentions) for tips on how to handle this case.</span></span>

## <a name="issues-with-packaging-and-uploading"></a><span data-ttu-id="b5537-152">打包和上传时出现问题</span><span class="sxs-lookup"><span data-stu-id="b5537-152">Issues with packaging and uploading</span></span>

### <a name="error-while-reading-manifestjson"></a><span data-ttu-id="b5537-153">读取清单 json 时出错</span><span class="sxs-lookup"><span data-stu-id="b5537-153">Error while reading manifest.json</span></span>

<span data-ttu-id="b5537-154">大多数清单错误将在特定字段缺失或无效时提供提示。</span><span class="sxs-lookup"><span data-stu-id="b5537-154">Most  manifest errors will provide a hint at what specific field is missing or invalid.</span></span> <span data-ttu-id="b5537-155">但是，如果 JSON 文件根本无法作为 JSON 读取，则使用此一般性错误消息。</span><span class="sxs-lookup"><span data-stu-id="b5537-155">However, if the JSON file cannot be read as JSON at all, this generic error message is used.</span></span>

<span data-ttu-id="b5537-156">清单读取错误的常见原因：</span><span class="sxs-lookup"><span data-stu-id="b5537-156">Common reasons for manifest read errors:</span></span>

* <span data-ttu-id="b5537-157">JSON 无效。</span><span class="sxs-lookup"><span data-stu-id="b5537-157">Invalid JSON.</span></span> <span data-ttu-id="b5537-158">使用可自动验证 JSON 语法的 IDE （如[Visual Studio Code](https://code.visualstudio.com)或[visual studio](https://www.visualstudio.com/vs/) ）。</span><span class="sxs-lookup"><span data-stu-id="b5537-158">Use an IDE such as [Visual Studio Code](https://code.visualstudio.com) or [Visual Studio](https://www.visualstudio.com/vs/) that automatically validates the JSON syntax.</span></span>
* <span data-ttu-id="b5537-159">编码问题。</span><span class="sxs-lookup"><span data-stu-id="b5537-159">Encoding issues.</span></span> <span data-ttu-id="b5537-160">对*清单 json*文件使用 utf-8。</span><span class="sxs-lookup"><span data-stu-id="b5537-160">Use UTF-8 for the *manifest.json* file.</span></span> <span data-ttu-id="b5537-161">其他编码（尤其是 BOM）可能不可读。</span><span class="sxs-lookup"><span data-stu-id="b5537-161">Other encodings, specifically with the BOM, may not be readable.</span></span>
* <span data-ttu-id="b5537-162">Zip 包格式不正确。</span><span class="sxs-lookup"><span data-stu-id="b5537-162">Malformed .zip package.</span></span> <span data-ttu-id="b5537-163">*清单 json*文件必须位于 .zip 文件的顶层。</span><span class="sxs-lookup"><span data-stu-id="b5537-163">The *manifest.json* file must be at the top level of the .zip file.</span></span> <span data-ttu-id="b5537-164">请注意，默认 Mac 文件压缩可能会将*清单 json*放在不能在 Microsoft 团队中正确加载的子目录中。</span><span class="sxs-lookup"><span data-stu-id="b5537-164">Note that default Mac file compression might place the *manifest.json* in a subdirectory, which will not properly load in Microsoft Teams.</span></span>

### <a name="another-extension-with-same-id-exists"></a><span data-ttu-id="b5537-165">存在具有相同 ID 的另一个分机号</span><span class="sxs-lookup"><span data-stu-id="b5537-165">Another extension with same ID exists</span></span>

<span data-ttu-id="b5537-166">如果您尝试重新上载具有相同 ID 的更新的包，请选择该选项卡的表行结尾处的**替换**图标，而不是使用 "**上载**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="b5537-166">If you're attempting to re-upload an updated package with the same ID, choose the **Replace** icon at the end of the tab's table row rather than the **Upload** button.</span></span>

<span data-ttu-id="b5537-167">如果不重新上载已更新的包，请确保该 ID 是唯一的。</span><span class="sxs-lookup"><span data-stu-id="b5537-167">If you're not re-uploading an updated package, ensure that the ID is unique.</span></span>
