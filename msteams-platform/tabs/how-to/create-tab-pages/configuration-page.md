---
title: 创建配置页
author: laujan
description: 如何创建配置页
keywords: teams 选项卡组频道可配置
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: b8300f268f74bed4fd1180b7a97c3b21ddda820a
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52629961"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="59c28-104">创建配置页</span><span class="sxs-lookup"><span data-stu-id="59c28-104">Create a configuration page</span></span>

<span data-ttu-id="59c28-105">配置页是一种特殊类型 [的内容页](content-page.md)。</span><span class="sxs-lookup"><span data-stu-id="59c28-105">A configuration page is a special type of [content page](content-page.md).</span></span> <span data-ttu-id="59c28-106">用户使用配置页面配置 Microsoft Teams应用的一些方面，并使用以下配置：</span><span class="sxs-lookup"><span data-stu-id="59c28-106">The users configure some aspects of the Microsoft Teams app using the configuration page and use that configuration as part of the following:</span></span>

* <span data-ttu-id="59c28-107">频道或群聊选项卡：从用户收集信息，并设置要 `contentUrl` 显示的内容页的 。</span><span class="sxs-lookup"><span data-stu-id="59c28-107">A channel or group chat tab: Collect information from the users and set the `contentUrl` of the content page to display.</span></span>
* <span data-ttu-id="59c28-108">消息传递 [扩展](~/messaging-extensions/what-are-messaging-extensions.md)。</span><span class="sxs-lookup"><span data-stu-id="59c28-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md).</span></span>
* <span data-ttu-id="59c28-109">一[Office 365连接器](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="59c28-109">An [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

## <a name="configuring-a-channel-or-group-chat-tab"></a><span data-ttu-id="59c28-110">配置频道或群聊选项卡</span><span class="sxs-lookup"><span data-stu-id="59c28-110">Configuring a channel or group chat tab</span></span>

<span data-ttu-id="59c28-111">应用程序必须引用[JavaScript Microsoft Teams SDK 并](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)调用 `microsoft.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="59c28-111">The application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="59c28-112">此外，使用的 URL 必须是安全的 HTTPS 终结点，并且可从云中访问。</span><span class="sxs-lookup"><span data-stu-id="59c28-112">Also, the URLs used must be secured HTTPS endpoints and available from the cloud.</span></span> 

### <a name="example"></a><span data-ttu-id="59c28-113">示例</span><span class="sxs-lookup"><span data-stu-id="59c28-113">Example</span></span>

<span data-ttu-id="59c28-114">配置页的示例如下图所示：</span><span class="sxs-lookup"><span data-stu-id="59c28-114">An example of a configuration page is shown in the following image:</span></span> 

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

<span data-ttu-id="59c28-115">下一节显示了配置页的相应代码：</span><span class="sxs-lookup"><span data-stu-id="59c28-115">The corresponding code for configuration page is shown in the following section:</span></span>

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
    </body>
...
```

<span data-ttu-id="59c28-116">选择配置 **页中的**"选择灰色"或"选择红色"按钮，以显示带灰色或红色图标的选项卡内容。</span><span class="sxs-lookup"><span data-stu-id="59c28-116">Choose either **Select Gray** or **Select Red** button in the configuration page, to display the tab content with a gray or red icon.</span></span> 

<span data-ttu-id="59c28-117">下图显示带灰色图标的选项卡内容：</span><span class="sxs-lookup"><span data-stu-id="59c28-117">The following image displays the tab content with gray icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

<span data-ttu-id="59c28-118">下图显示带红色图标的选项卡内容：</span><span class="sxs-lookup"><span data-stu-id="59c28-118">The following image displays the tab content with red icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

<span data-ttu-id="59c28-119">选择相对按钮将触发 `saveGray()` 或 `saveRed()` ，并调用以下内容：</span><span class="sxs-lookup"><span data-stu-id="59c28-119">Choosing the relative button triggers either `saveGray()` or `saveRed()`, and invokes the following:</span></span>

1. <span data-ttu-id="59c28-120">`settings.setValidityState(true)`设置为 true。</span><span class="sxs-lookup"><span data-stu-id="59c28-120">The `settings.setValidityState(true)` is set to true.</span></span>
1. <span data-ttu-id="59c28-121">`microsoftTeams.settings.registerOnSaveHandler()`将触发事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="59c28-121">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
1. <span data-ttu-id="59c28-122">应用的 **配置** 页面上的"保存"按钮（在 Teams 中上载）已启用。</span><span class="sxs-lookup"><span data-stu-id="59c28-122">The **Save** button on the app's configuration page, uploaded in Teams, is enabled.</span></span>

<span data-ttu-id="59c28-123">配置页面代码通知Teams配置要求，并且可以继续安装。</span><span class="sxs-lookup"><span data-stu-id="59c28-123">The configuration page code informs the Teams that the configuration requirements are satisfied and the installation can proceed.</span></span> <span data-ttu-id="59c28-124">当用户选择"保存 **"** 时，将设置 的参数 `settings.setSettings()` ，如 接口 `Settings` 所定义。</span><span class="sxs-lookup"><span data-stu-id="59c28-124">When the user selects **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface.</span></span> <span data-ttu-id="59c28-125">有关详细信息，请参阅设置[接口](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="59c28-125">For more information, see [Settings interface](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="59c28-126">在上一步 `saveEvent.notifySuccess()` 中，调用 以指示已成功解析内容 URL。</span><span class="sxs-lookup"><span data-stu-id="59c28-126">In the last step, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="59c28-127">如果使用 注册保存处理程序 `microsoftTeams.settings.registerOnSaveHandler()` ，回调必须调用 或 `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` 以指示配置的结果。</span><span class="sxs-lookup"><span data-stu-id="59c28-127">If you register a save handler using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="59c28-128">如果未注册保存处理程序，则当用户选择"保存"时 `saveEvent.notifySuccess()` 会自动 **进行调用**。</span><span class="sxs-lookup"><span data-stu-id="59c28-128">If you don't register a save handler, the `saveEvent.notifySuccess()` call is made automatically when the user selects **Save**.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="59c28-129">获取选项卡设置的上下文数据</span><span class="sxs-lookup"><span data-stu-id="59c28-129">Get context data for your tab settings</span></span>

<span data-ttu-id="59c28-130">你的选项卡可能需要上下文信息以显示相关内容。</span><span class="sxs-lookup"><span data-stu-id="59c28-130">Your tab might require contextual information to display relevant content.</span></span> <span data-ttu-id="59c28-131">上下文信息通过提供更加自定义的用户体验进一步增强选项卡的吸引力。</span><span class="sxs-lookup"><span data-stu-id="59c28-131">Contextual information further enhances your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="59c28-132">有关用于选项卡配置的属性详细信息，请参阅 [上下文接口](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="59c28-132">For more information on the properties used for tab configuration, see [Context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="59c28-133">通过以下两种方式收集上下文数据变量的值：</span><span class="sxs-lookup"><span data-stu-id="59c28-133">Collect the values of context data variables in the following two ways:</span></span>

1. <span data-ttu-id="59c28-134">在清单 中插入 URL 查询字符串占位符 `configurationURL` 。</span><span class="sxs-lookup"><span data-stu-id="59c28-134">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

1. <span data-ttu-id="59c28-135">使用[Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` 方法。</span><span class="sxs-lookup"><span data-stu-id="59c28-135">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="59c28-136">在 中插入占位符 `configurationUrl`</span><span class="sxs-lookup"><span data-stu-id="59c28-136">Insert placeholders in the `configurationUrl`</span></span>

<span data-ttu-id="59c28-137">将上下文接口占位符添加到基本 `configurationUrl` 。</span><span class="sxs-lookup"><span data-stu-id="59c28-137">Add context interface placeholders to your base `configurationUrl`.</span></span> <span data-ttu-id="59c28-138">例如：</span><span class="sxs-lookup"><span data-stu-id="59c28-138">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="59c28-139">基 URL</span><span class="sxs-lookup"><span data-stu-id="59c28-139">Base URL</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="59c28-140">包含查询字符串的基 URL</span><span class="sxs-lookup"><span data-stu-id="59c28-140">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="59c28-141">上载页面后，Teams使用相关值更新查询字符串占位符。</span><span class="sxs-lookup"><span data-stu-id="59c28-141">After your page uploads, the Teams updates the query string placeholders with relevant values.</span></span> <span data-ttu-id="59c28-142">在配置页中包括用于检索和使用这些值的逻辑。</span><span class="sxs-lookup"><span data-stu-id="59c28-142">Include logic in the configuration page to retrieve and use those values.</span></span> <span data-ttu-id="59c28-143">有关使用 URL 查询字符串的信息，请参阅 MDN Web Docs 中的 [URLSearchParams。](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) 以下示例描述从 属性中提取值 `configurationUrl` 的方法：</span><span class="sxs-lookup"><span data-stu-id="59c28-143">For more information on working with URL query strings, see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. The following example describes the way to extract a value from the `configurationUrl` property:</span></span>

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="59c28-144">使用 `getContext()` 函数检索上下文</span><span class="sxs-lookup"><span data-stu-id="59c28-144">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="59c28-145">`microsoftTeams.getContext((context) => {})`函数在调用[时检索 Context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true)接口。</span><span class="sxs-lookup"><span data-stu-id="59c28-145">The `microsoftTeams.getContext((context) => {})` function retrieves the [Context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) when invoked.</span></span> <span data-ttu-id="59c28-146">将此函数添加到配置页以检索上下文值：</span><span class="sxs-lookup"><span data-stu-id="59c28-146">Add this function to the configuration page to retrieve context values:</span></span>

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

## <a name="context-and-authentication"></a><span data-ttu-id="59c28-147">上下文和身份验证</span><span class="sxs-lookup"><span data-stu-id="59c28-147">Context and authentication</span></span>

 <span data-ttu-id="59c28-148">在允许用户配置你的应用之前进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="59c28-148">Authenticate before allowing a user to configure your app.</span></span> <span data-ttu-id="59c28-149">否则，您的内容可能包括具有其身份验证协议的源。</span><span class="sxs-lookup"><span data-stu-id="59c28-149">Otherwise, your content might include sources that have their authentication protocols.</span></span> <span data-ttu-id="59c28-150">有关详细信息，请参阅在"验证[用户身份"选项卡Microsoft Teams用户。](~/tabs/how-to/authentication/auth-flow-tab.md)使用上下文信息构建身份验证请求和授权页面 URL。</span><span class="sxs-lookup"><span data-stu-id="59c28-150">For more information, see [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md). Use context information to construct the authentication requests and authorization page URLs.</span></span>
<span data-ttu-id="59c28-151">确保 选项卡页中使用的所有域都列在 `manifest.json` 和 `validDomains` 数组中。</span><span class="sxs-lookup"><span data-stu-id="59c28-151">Ensure that all domains used in your tab pages are listed in the `manifest.json` and `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="59c28-152">修改或删除选项卡</span><span class="sxs-lookup"><span data-stu-id="59c28-152">Modify or remove a tab</span></span>

<span data-ttu-id="59c28-153">支持的删除选项可进一步优化用户体验。</span><span class="sxs-lookup"><span data-stu-id="59c28-153">Supported removal options further refine the user experience.</span></span> <span data-ttu-id="59c28-154">将清单的 属性设置为 ，以便用户能够修改、重新配置或 `canUpdateConfiguration` `true` 重命名组或频道选项卡。此外，通过包括应用中的删除选项页面和在配置中设置属性的值，指示删除选项卡时内容会发生什么 `removeUrl`  `setSettings()` 情况。</span><span class="sxs-lookup"><span data-stu-id="59c28-154">Set your manifest's `canUpdateConfiguration` property to `true`, that enables the users to modify, reconfigure, or rename a group or channel tab. Also, indicate what happens to the content when a tab is removed, by including a removal options page in the app and setting a value for the `removeUrl` property in the  `setSettings()` configuration.</span></span> <span data-ttu-id="59c28-155">用户可以卸载"个人"选项卡，但不能修改它们。</span><span class="sxs-lookup"><span data-stu-id="59c28-155">The user can uninstall the Personal tabs but cannot modify them.</span></span> <span data-ttu-id="59c28-156">有关详细信息，请参阅为选项卡 [创建删除页](~/tabs/how-to/create-tab-pages/removal-page.md)。</span><span class="sxs-lookup"><span data-stu-id="59c28-156">For more information, see [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

<span data-ttu-id="59c28-157">Microsoft Teams删除 () 的 setSettings 配置：</span><span class="sxs-lookup"><span data-stu-id="59c28-157">Microsoft Teams setSettings() configuration for removal page:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a><span data-ttu-id="59c28-158">移动客户端</span><span class="sxs-lookup"><span data-stu-id="59c28-158">Mobile clients</span></span>

<span data-ttu-id="59c28-159">如果选择让频道或组选项卡显示在移动客户端Teams，则配置必须具有 `setSettings()` 的值 `websiteUrl` 。</span><span class="sxs-lookup"><span data-stu-id="59c28-159">If you choose to have your channel or group tab appear on the Teams mobile clients, the `setSettings()` configuration must have a value for `websiteUrl`.</span></span> <span data-ttu-id="59c28-160">有关详细信息，请参阅 [移动选项卡指南](~/tabs/design/tabs-mobile.md)。</span><span class="sxs-lookup"><span data-stu-id="59c28-160">For more information, see [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span></span>
