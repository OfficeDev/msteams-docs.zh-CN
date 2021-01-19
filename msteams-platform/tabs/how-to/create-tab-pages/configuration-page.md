---
title: 创建配置页
author: laujan
description: 如何创建配置页
keywords: teams 选项卡组频道可配置
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 2544454fd06348fa41269f3a8fd57cc71a07d140
ms.sourcegitcommit: 84f408aa2854aa7a5cefaa66ce9a373b19e0864a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2021
ms.locfileid: "49886735"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="475d9-104">创建配置页</span><span class="sxs-lookup"><span data-stu-id="475d9-104">Create a configuration page</span></span>

<span data-ttu-id="475d9-105">配置页是一种特殊类型 [的内容页](content-page.md)。</span><span class="sxs-lookup"><span data-stu-id="475d9-105">A configuration page is a special type of [content page](content-page.md).</span></span> <span data-ttu-id="475d9-106">用户使用配置页面配置 Microsoft Teams 应用的某些方面，并使用以下配置：</span><span class="sxs-lookup"><span data-stu-id="475d9-106">The users configure some aspects of the Microsoft Teams app using the configuration page and use that configuration as part of the following:</span></span>

* <span data-ttu-id="475d9-107">频道或群聊选项卡 - 从用户收集信息，并设置 `contentUrl` 要显示的内容页。</span><span class="sxs-lookup"><span data-stu-id="475d9-107">A channel or group chat tab - Collect information from the users and set the `contentUrl` of the content page to display.</span></span>
* <span data-ttu-id="475d9-108">[邮件扩展](~/messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="475d9-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md)</span></span>
* <span data-ttu-id="475d9-109">[Office 365 连接器](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span><span class="sxs-lookup"><span data-stu-id="475d9-109">An [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span></span>

## <a name="configuring-a-channel-or-group-chat-tab"></a><span data-ttu-id="475d9-110">配置频道或群聊选项卡</span><span class="sxs-lookup"><span data-stu-id="475d9-110">Configuring a channel or group chat tab</span></span>

<span data-ttu-id="475d9-111">应用程序必须引用 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) 并调用 `microsoft.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="475d9-111">The application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="475d9-112">此外，使用的 URL 必须是安全的 HTTPS 终结点，并且可从云中访问。</span><span class="sxs-lookup"><span data-stu-id="475d9-112">Also, the URLs used must be secured HTTPS endpoints and available from the cloud.</span></span> <span data-ttu-id="475d9-113">以下代码是配置页的示例：</span><span class="sxs-lookup"><span data-stu-id="475d9-113">The following code is an example of a configuration page:</span></span>

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

<span data-ttu-id="475d9-114">选择配置 **页中的**"选择灰色"或"选择红色"按钮，以显示带灰色或红色图标的选项卡内容。</span><span class="sxs-lookup"><span data-stu-id="475d9-114">Choose either **Select Gray** or **Select Red** button in the configuration page, to display the tab content with a gray or red icon.</span></span> <span data-ttu-id="475d9-115">选择相对按钮将触发或 `saveGray()` `saveRed()` ，并调用以下内容：</span><span class="sxs-lookup"><span data-stu-id="475d9-115">Choosing the relative button fires either `saveGray()` or `saveRed()`, and invokes the following:</span></span>

1. <span data-ttu-id="475d9-116">设置为 `settings.setValidityState(true)` true。</span><span class="sxs-lookup"><span data-stu-id="475d9-116">The `settings.setValidityState(true)` is set to true.</span></span>
1. <span data-ttu-id="475d9-117">`microsoftTeams.settings.registerOnSaveHandler()`触发事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="475d9-117">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
1. <span data-ttu-id="475d9-118">应用 **配置** 页面上的"保存"按钮（在 Teams 中上载）已启用。</span><span class="sxs-lookup"><span data-stu-id="475d9-118">The **Save** button on the app's configuration page, uploaded in Teams, is enabled.</span></span>

<span data-ttu-id="475d9-119">配置页面代码通知 Teams 已满足配置要求，并且可以继续安装。</span><span class="sxs-lookup"><span data-stu-id="475d9-119">The configuration page code informs the Teams that the configuration requirements are satisfied and the installation can proceed.</span></span> <span data-ttu-id="475d9-120">当用户 **选择"保存**"时，将设置其参数 `settings.setSettings()` ，如界面 `Settings` 所定义。</span><span class="sxs-lookup"><span data-stu-id="475d9-120">When the user selects **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface.</span></span> <span data-ttu-id="475d9-121">有关详细信息，请参阅"设置 ["界面](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="475d9-121">For more information, see [Settings interface](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="475d9-122">在上一步 `saveEvent.notifySuccess()` 中，调用以指示内容 URL 已成功解析。</span><span class="sxs-lookup"><span data-stu-id="475d9-122">In the last step, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="475d9-123">如果使用注册保存处理程序 `microsoftTeams.settings.registerOnSaveHandler()` ，则回调 `saveEvent.notifySuccess()` 必须调用或 `saveEvent.notifyFailure()` 指示配置的结果。</span><span class="sxs-lookup"><span data-stu-id="475d9-123">If you register a save handler using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="475d9-124">如果未注册保存处理程序，则当用户选择"保存"时 `saveEvent.notifySuccess()` 将自动 **进行调用**。</span><span class="sxs-lookup"><span data-stu-id="475d9-124">If you don't register a save handler, the `saveEvent.notifySuccess()` call is made automatically when the user selects **Save**.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="475d9-125">获取选项卡设置的上下文数据</span><span class="sxs-lookup"><span data-stu-id="475d9-125">Get context data for your tab settings</span></span>

<span data-ttu-id="475d9-126">您的选项卡可能需要上下文信息来显示相关内容。</span><span class="sxs-lookup"><span data-stu-id="475d9-126">Your tab might require contextual information to display relevant content.</span></span> <span data-ttu-id="475d9-127">上下文信息通过提供更加自定义的用户体验来进一步增强选项卡的吸引力。</span><span class="sxs-lookup"><span data-stu-id="475d9-127">Contextual information further enhances your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="475d9-128">有关用于选项卡配置的属性详细信息，请参阅 [上下文接口](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="475d9-128">For more information on the properties used for tab configuration, see [Context interface](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="475d9-129">通过以下两种方式收集上下文数据变量的值：</span><span class="sxs-lookup"><span data-stu-id="475d9-129">Collect the values of context data variables in the following two ways:</span></span>

1. <span data-ttu-id="475d9-130">在清单中插入 URL 查询字符串占位符 `configurationURL` 。</span><span class="sxs-lookup"><span data-stu-id="475d9-130">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

1. <span data-ttu-id="475d9-131">使用 [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` 方法。</span><span class="sxs-lookup"><span data-stu-id="475d9-131">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="475d9-132">在 `configurationUrl`</span><span class="sxs-lookup"><span data-stu-id="475d9-132">Insert placeholders in the `configurationUrl`</span></span>

<span data-ttu-id="475d9-133">将上下文接口占位符添加到基本位置 `configurationUrl` 。</span><span class="sxs-lookup"><span data-stu-id="475d9-133">Add context interface placeholders to your base `configurationUrl`.</span></span> <span data-ttu-id="475d9-134">例如：</span><span class="sxs-lookup"><span data-stu-id="475d9-134">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="475d9-135">基 URL</span><span class="sxs-lookup"><span data-stu-id="475d9-135">Base URL</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="475d9-136">包含查询字符串的基 URL</span><span class="sxs-lookup"><span data-stu-id="475d9-136">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="475d9-137">上传页面后，Teams 会使用相关值更新查询字符串占位符。</span><span class="sxs-lookup"><span data-stu-id="475d9-137">After your page uploads, the Teams updates the query string placeholders with relevant values.</span></span> <span data-ttu-id="475d9-138">在配置页中包括逻辑以检索和使用这些值。</span><span class="sxs-lookup"><span data-stu-id="475d9-138">Include logic in the configuration page to retrieve and use those values.</span></span> <span data-ttu-id="475d9-139">有关使用 URL 查询字符串的信息，请参阅 MDN Web Docs 中的 [URLSearchParams。](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) 以下示例描述从属性中提取值 `configurationUrl` 的方法：</span><span class="sxs-lookup"><span data-stu-id="475d9-139">For more information on working with URL query strings, see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. The following example describes the way to extract a value from the `configurationUrl` property:</span></span>

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="475d9-140">使用 `getContext()` 函数检索上下文</span><span class="sxs-lookup"><span data-stu-id="475d9-140">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="475d9-141">`microsoftTeams.getContext((context) => {})`该函数在调用[时检索 Context](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)接口。</span><span class="sxs-lookup"><span data-stu-id="475d9-141">The `microsoftTeams.getContext((context) => {})` function retrieves the [Context interface](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) when invoked.</span></span> <span data-ttu-id="475d9-142">将此函数添加到配置页以检索上下文值：</span><span class="sxs-lookup"><span data-stu-id="475d9-142">Add this function to the configuration page to retrieve context values:</span></span>

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

## <a name="context-and-authentication"></a><span data-ttu-id="475d9-143">上下文和身份验证</span><span class="sxs-lookup"><span data-stu-id="475d9-143">Context and authentication</span></span>

 <span data-ttu-id="475d9-144">在允许用户配置你的应用之前进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="475d9-144">Authenticate before allowing a user to configure your app.</span></span> <span data-ttu-id="475d9-145">否则，您的内容可能包括具有其身份验证协议的源。</span><span class="sxs-lookup"><span data-stu-id="475d9-145">Otherwise, your content might include sources that have their authentication protocols.</span></span> <span data-ttu-id="475d9-146">有关详细信息，请参阅 Microsoft Teams 选项卡 [中的"对用户进行身份验证"。](~/tabs/how-to/authentication/auth-flow-tab.md)使用上下文信息构造身份验证请求和授权页面 URL。</span><span class="sxs-lookup"><span data-stu-id="475d9-146">For more information, see [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md). Use context information to construct the authentication requests and authorization page URLs.</span></span>
<span data-ttu-id="475d9-147">确保选项卡页中使用的所有域都列在和 `manifest.json` `validDomains` 数组中。</span><span class="sxs-lookup"><span data-stu-id="475d9-147">Ensure that all domains used in your tab pages are listed in the `manifest.json` and `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="475d9-148">修改或删除选项卡</span><span class="sxs-lookup"><span data-stu-id="475d9-148">Modify or remove a tab</span></span>

<span data-ttu-id="475d9-149">支持的删除选项可进一步优化用户体验。</span><span class="sxs-lookup"><span data-stu-id="475d9-149">Supported removal options further refine the user experience.</span></span> <span data-ttu-id="475d9-150">将清单的属性设置为 ，允许用户修改、重新配置或 `canUpdateConfiguration` `true` 重命名组或频道选项卡。此外，通过在应用中包括删除选项页和在配置中设置属性值，指示删除选项卡时内容会发生什么 `removeUrl`  `setSettings()` 情况。</span><span class="sxs-lookup"><span data-stu-id="475d9-150">Set your manifest's `canUpdateConfiguration` property to `true`, that enables the users to modify, reconfigure, or rename a group or channel tab. Also, indicate what happens to the content when a tab is removed, by including a removal options page in the app and setting a value for the `removeUrl` property in the  `setSettings()` configuration.</span></span> <span data-ttu-id="475d9-151">有关详细信息，请参阅移动 [客户端](#mobile-clients)。</span><span class="sxs-lookup"><span data-stu-id="475d9-151">For more information, see [Mobile clients](#mobile-clients).</span></span> <span data-ttu-id="475d9-152">用户可以卸载个人选项卡，但不能修改它们。</span><span class="sxs-lookup"><span data-stu-id="475d9-152">The user can uninstall the Personal tabs but cannot modify them.</span></span> <span data-ttu-id="475d9-153">有关详细信息，请参阅 [为选项卡创建删除页](~/tabs/how-to/create-tab-pages/removal-page.md)。</span><span class="sxs-lookup"><span data-stu-id="475d9-153">For more information, see [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

## <a name="mobile-clients"></a><span data-ttu-id="475d9-154">移动客户端</span><span class="sxs-lookup"><span data-stu-id="475d9-154">Mobile clients</span></span>

<span data-ttu-id="475d9-155">如果你选择让频道或组选项卡显示在 Teams 移动客户端上，则配置必须具有 `setSettings()` 属性的值 `websiteUrl` 。</span><span class="sxs-lookup"><span data-stu-id="475d9-155">If you choose to have your channel or group tab appear on the Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span> <span data-ttu-id="475d9-156">有关详细信息，请参阅 [移动选项卡指南](~/tabs/design/tabs-mobile.md)。</span><span class="sxs-lookup"><span data-stu-id="475d9-156">For more information, see [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span></span>

<span data-ttu-id="475d9-157">用于删除页面 (移动客户端的 Microsoft Teams setSettings () 配置：</span><span class="sxs-lookup"><span data-stu-id="475d9-157">Microsoft Teams setSettings() configuration for removal page or mobile clients:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "URL REQUIRED FOR MOBILE CLIENTS",
    removeUrl: "ADD REMOVAL PAGE URL HERE"
});
```
