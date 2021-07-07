---
title: 创建配置页
author: surbhigupta
description: 如何创建配置页
keywords: teams 选项卡组频道可配置
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 6f79480fb3ec6eb50de622e0b67b70e021d8cce7
ms.sourcegitcommit: a6253e89cb8c8c34d45b06e08c9668daeebc30a3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2021
ms.locfileid: "53300310"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="d8d6a-104">创建配置页</span><span class="sxs-lookup"><span data-stu-id="d8d6a-104">Create a configuration page</span></span>

<span data-ttu-id="d8d6a-105">配置页是一种特殊类型 [的内容页](content-page.md)。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-105">A configuration page is a special type of [content page](content-page.md).</span></span> <span data-ttu-id="d8d6a-106">用户使用配置页面配置 Microsoft Teams应用的一些方面，并使用以下配置：</span><span class="sxs-lookup"><span data-stu-id="d8d6a-106">The users configure some aspects of the Microsoft Teams app using the configuration page and use that configuration as part of the following:</span></span>

* <span data-ttu-id="d8d6a-107">频道或群聊选项卡：从用户收集信息，并设置要 `contentUrl` 显示的内容页的 。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-107">A channel or group chat tab: Collect information from the users and set the `contentUrl` of the content page to be displayed.</span></span>
* <span data-ttu-id="d8d6a-108">消息传递 [扩展](~/messaging-extensions/what-are-messaging-extensions.md)。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md).</span></span>
* <span data-ttu-id="d8d6a-109">一[Office 365连接器](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-109">An [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

## <a name="configure-a-channel-or-group-chat-tab"></a><span data-ttu-id="d8d6a-110">配置频道或群聊选项卡</span><span class="sxs-lookup"><span data-stu-id="d8d6a-110">Configure a channel or group chat tab</span></span>

<span data-ttu-id="d8d6a-111">应用程序必须引用[JavaScript Microsoft Teams SDK 并](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)调用 `microsoft.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-111">The application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="d8d6a-112">使用的 URL 必须是安全的 HTTPS 终结点，并且可从云中访问。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-112">The URLs used must be secured HTTPS endpoints and available from the cloud.</span></span>

### <a name="example"></a><span data-ttu-id="d8d6a-113">示例</span><span class="sxs-lookup"><span data-stu-id="d8d6a-113">Example</span></span>

<span data-ttu-id="d8d6a-114">配置页的示例如下图所示：</span><span class="sxs-lookup"><span data-stu-id="d8d6a-114">An example of a configuration page is shown in the following image:</span></span>

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

<span data-ttu-id="d8d6a-115">以下代码是配置页的相应代码示例：</span><span class="sxs-lookup"><span data-stu-id="d8d6a-115">The following code is an example of corresponding code for the configuration page:</span></span>

```html
<head>
    <script src='https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js'></script>
</head>
<body>
    <button onclick="(document.getElementById('icon').src = '/images/iconGray.png'); colorClickGray()">Select Gray</button>
    <img id="icon" src="/images/teamsIcon.png" alt="icon" style="width:100px" />
    <button onclick="(document.getElementById('icon').src = '/images/iconRed.png'); colorClickRed()">Select Red</button>

    <script>
        microsoftTeams.initialize();
        let saveGray = () => {
            microsoftTeams.settings.registerOnSaveHandler((saveEvent) => {
                microsoftTeams.settings.setSettings({
                    websiteUrl: "https://yourWebsite.com",
                    contentUrl: "https://yourWebsite.com/gray",
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }
        let saveRed = () => {
            microsoftTeams.settings.registerOnSaveHandler((saveEvent) => {
                microsoftTeams.settings.setSettings({
                    websiteUrl: "https://yourWebsite.com",
                    contentUrl: "https://yourWebsite.com/red",
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }

        let gr = document.getElementById("gray").style;
        let rd = document.getElementById("red").style;

        const colorClickGray = () => {
            gr.display = "block";
            rd.display = "none";
            microsoftTeams.settings.setValidityState(true);
            saveGray()
        }

        const colorClickRed = () => {
            rd.display = "block";
            gr.display = "none";
            microsoftTeams.settings.setValidityState(true);
            saveRed();
        }
    </script>
    ...
</body>
```

<span data-ttu-id="d8d6a-116">选择配置 **页中的**"选择灰色"或"选择红色"按钮，以显示带灰色或红色图标的选项卡内容。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-116">Choose either **Select Gray** or **Select Red** button in the configuration page, to display the tab content with a gray or red icon.</span></span>

<span data-ttu-id="d8d6a-117">下图显示带灰色图标的选项卡内容：</span><span class="sxs-lookup"><span data-stu-id="d8d6a-117">The following image displays the tab content with a gray icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

<span data-ttu-id="d8d6a-118">下图显示带红色图标的选项卡内容：</span><span class="sxs-lookup"><span data-stu-id="d8d6a-118">The following image displays the tab content with a red icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

<span data-ttu-id="d8d6a-119">选择相应的按钮将触发 `saveGray()` 或 `saveRed()` ，并调用以下内容：</span><span class="sxs-lookup"><span data-stu-id="d8d6a-119">Choosing the appropriate button triggers either `saveGray()` or `saveRed()`, and invokes the following:</span></span>

* <span data-ttu-id="d8d6a-120">设置为 `settings.setValidityState(true)` true。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-120">Set `settings.setValidityState(true)` to true.</span></span> 
* <span data-ttu-id="d8d6a-121">`microsoftTeams.settings.registerOnSaveHandler()`将触发事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-121">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
* <span data-ttu-id="d8d6a-122">**在** 应用的配置页面上保存已启用。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-122">**Save** on the app's configuration page, is enabled.</span></span>

<span data-ttu-id="d8d6a-123">配置页面代码Teams配置要求，并可以继续安装。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-123">The configuration page code informs Teams that the configuration requirements are satisfied and the installation can proceed.</span></span> <span data-ttu-id="d8d6a-124">当用户选择"保存 **"** 时，将设置 的参数 `settings.setSettings()` ，如 接口 `Settings` 所定义。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-124">When the user selects **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface.</span></span> <span data-ttu-id="d8d6a-125">有关详细信息，请参阅设置 [接口](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-125">For more information, see [settings interface](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="d8d6a-126">`saveEvent.notifySuccess()` 调用 以指示已成功解析内容 URL。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-126">`saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="d8d6a-127">如果使用 注册保存处理程序 `microsoftTeams.settings.registerOnSaveHandler()` ，回调必须调用 或 `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` 以指示配置的结果。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-127">If you register a save handler using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="d8d6a-128">如果未注册保存处理程序，则当用户选择"保存"时 `saveEvent.notifySuccess()` 会自动 **进行调用**。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-128">If you do not register a save handler, the `saveEvent.notifySuccess()` call is made automatically when the user selects **Save**.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="d8d6a-129">获取选项卡设置的上下文数据</span><span class="sxs-lookup"><span data-stu-id="d8d6a-129">Get context data for your tab settings</span></span>

<span data-ttu-id="d8d6a-130">您的选项卡需要上下文信息来显示相关内容。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-130">Your tab requires contextual information to display relevant content.</span></span> <span data-ttu-id="d8d6a-131">上下文信息通过提供更加自定义的用户体验进一步增强选项卡的吸引力。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-131">Contextual information further enhances your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="d8d6a-132">有关用于选项卡配置的属性详细信息，请参阅 [上下文接口](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-132">For more information on the properties used for tab configuration, see [context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="d8d6a-133">通过以下两种方式收集上下文数据变量的值：</span><span class="sxs-lookup"><span data-stu-id="d8d6a-133">Collect the values of context data variables in the following two ways:</span></span>

* <span data-ttu-id="d8d6a-134">在清单 中插入 URL 查询字符串占位符 `configurationURL` 。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-134">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

* <span data-ttu-id="d8d6a-135">使用[Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` 方法。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-135">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="d8d6a-136">在 中插入占位符 `configurationUrl`</span><span class="sxs-lookup"><span data-stu-id="d8d6a-136">Insert placeholders in the `configurationUrl`</span></span>

<span data-ttu-id="d8d6a-137">将上下文接口占位符添加到基本 `configurationUrl` 。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-137">Add context interface placeholders to your base `configurationUrl`.</span></span> <span data-ttu-id="d8d6a-138">例如：</span><span class="sxs-lookup"><span data-stu-id="d8d6a-138">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="d8d6a-139">基 URL</span><span class="sxs-lookup"><span data-stu-id="d8d6a-139">Base URL</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="d8d6a-140">包含查询字符串的基 URL</span><span class="sxs-lookup"><span data-stu-id="d8d6a-140">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="d8d6a-141">上载页面后，Teams使用相关值更新查询字符串占位符。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-141">After your page uploads, Teams updates the query string placeholders with relevant values.</span></span> <span data-ttu-id="d8d6a-142">在配置页中包括用于检索和使用这些值的逻辑。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-142">Include logic in the configuration page to retrieve and use those values.</span></span> <span data-ttu-id="d8d6a-143">有关使用 URL 查询字符串的信息，请参阅 MDN Web Docs 中的 [URLSearchParams。](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) 下面的代码示例提供了从 属性中提取值 `configurationUrl` 的方法：</span><span class="sxs-lookup"><span data-stu-id="d8d6a-143">For more information on working with URL query strings, see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. The following code example provides the way to extract a value from the `configurationUrl` property:</span></span>

```html
<script>
   microsoftTeams.initialize();
   const getId = () => {
        let urlParams = new URLSearchParams(document.location.search.substring(1));
        let blueTeamId = urlParams.get('team');
        return blueTeamId
    }
//For testing, you can invoke the following to view the pertinent value:
document.write(getId());
</script>
```

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="d8d6a-144">使用 `getContext()` 函数检索上下文</span><span class="sxs-lookup"><span data-stu-id="d8d6a-144">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="d8d6a-145">`microsoftTeams.getContext((context) => {})`函数在调用[时检索](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true)上下文接口。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-145">The `microsoftTeams.getContext((context) => {})` function retrieves the [context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) when invoked.</span></span>

<span data-ttu-id="d8d6a-146">以下代码提供了一个向配置页添加此函数以检索上下文值的示例：</span><span class="sxs-lookup"><span data-stu-id="d8d6a-146">The following code provides an example of adding this function to the configuration page to retrieve context values:</span></span>

```html
<!-- `userPrincipalName` will render in the span with the id "user". -->

<span id="user"></span>
...
<script>
    microsoftTeams.getContext((context) =>{
        let userId = document.getElementById('user');
        userId.innerHTML = context.userPrincipalName;
    });
</script>
...
```

## <a name="context-and-authentication"></a><span data-ttu-id="d8d6a-147">上下文和身份验证</span><span class="sxs-lookup"><span data-stu-id="d8d6a-147">Context and authentication</span></span>

<span data-ttu-id="d8d6a-148">在允许用户配置你的应用之前进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-148">Authenticate before allowing a user to configure your app.</span></span> <span data-ttu-id="d8d6a-149">否则，您的内容可能包括具有其身份验证协议的源。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-149">Otherwise, your content might include sources that have their authentication protocols.</span></span> <span data-ttu-id="d8d6a-150">有关详细信息，请参阅在"身份验证["选项卡中Microsoft Teams用户。](~/tabs/how-to/authentication/auth-flow-tab.md)使用上下文信息构建身份验证请求和授权页面 URL。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-150">For more information, see [authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md). Use context information to construct the authentication requests and authorization page URLs.</span></span> <span data-ttu-id="d8d6a-151">确保 选项卡页中使用的所有域都列在 `manifest.json` 和 `validDomains` 数组中。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-151">Ensure that all domains used in your tab pages are listed in the `manifest.json` and `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="d8d6a-152">修改或删除选项卡</span><span class="sxs-lookup"><span data-stu-id="d8d6a-152">Modify or remove a tab</span></span>

<span data-ttu-id="d8d6a-153">将清单的 属性设置为 ，以便用户能够修改、重新配置或 `canUpdateConfiguration` `true` 重命名频道或组选项卡。此外，通过包括应用中的删除选项页面和在配置中设置属性的值，指示删除选项卡时内容会发生什么 `removeUrl`  `setSettings()` 情况。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-153">Set your manifest's `canUpdateConfiguration` property to `true`, that enables the users to modify, reconfigure, or rename a channel or group tab. Also, indicate what happens to the content when a tab is removed, by including a removal options page in the app and setting a value for the `removeUrl` property in the  `setSettings()` configuration.</span></span> <span data-ttu-id="d8d6a-154">用户可以卸载个人选项卡，但不能修改它们。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-154">The user can uninstall personal tabs but cannot modify them.</span></span> <span data-ttu-id="d8d6a-155">有关详细信息，请参阅 [为选项卡创建删除页面](~/tabs/how-to/create-tab-pages/removal-page.md)。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-155">For more information, see [create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

<span data-ttu-id="d8d6a-156">`setSettings()`Microsoft Teams删除页面的配置：</span><span class="sxs-lookup"><span data-stu-id="d8d6a-156">Microsoft Teams `setSettings()` configuration for removal page:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a><span data-ttu-id="d8d6a-157">移动客户端</span><span class="sxs-lookup"><span data-stu-id="d8d6a-157">Mobile clients</span></span>

<span data-ttu-id="d8d6a-158">如果选择让频道或组选项卡显示在移动客户端Teams，则配置必须具有 `setSettings()` 的值 `websiteUrl` 。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-158">If you choose to have your channel or group tab appear on the Teams mobile clients, the `setSettings()` configuration must have a value for `websiteUrl`.</span></span> <span data-ttu-id="d8d6a-159">有关详细信息，请参阅 [移动选项卡指南](~/tabs/design/tabs-mobile.md)。</span><span class="sxs-lookup"><span data-stu-id="d8d6a-159">For more information, see [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="d8d6a-160">另请参阅</span><span class="sxs-lookup"><span data-stu-id="d8d6a-160">See also</span></span>

* [<span data-ttu-id="d8d6a-161">Teams选项卡</span><span class="sxs-lookup"><span data-stu-id="d8d6a-161">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="d8d6a-162">创建个人选项卡</span><span class="sxs-lookup"><span data-stu-id="d8d6a-162">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="d8d6a-163">创建频道或组选项卡</span><span class="sxs-lookup"><span data-stu-id="d8d6a-163">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="d8d6a-164">创建内容页</span><span class="sxs-lookup"><span data-stu-id="d8d6a-164">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
* [<span data-ttu-id="d8d6a-165">移动设备上的选项卡</span><span class="sxs-lookup"><span data-stu-id="d8d6a-165">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)

## <a name="next-step"></a><span data-ttu-id="d8d6a-166">后续步骤</span><span class="sxs-lookup"><span data-stu-id="d8d6a-166">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d8d6a-167">为选项卡创建删除页</span><span class="sxs-lookup"><span data-stu-id="d8d6a-167">Create a removal page for your tab</span></span>](~/tabs/how-to/create-tab-pages/removal-page.md)
