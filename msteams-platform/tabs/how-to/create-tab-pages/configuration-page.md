---
title: 创建配置页
author: laujan
description: 如何创建配置页
keywords: teams 选项卡组频道可配置
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: c041c311245bb5bfc5e2655ef8d596b2839fdb70
ms.sourcegitcommit: d0e71ea63af2f67eba75ba283ec46cc7cdf87d75
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/24/2020
ms.locfileid: "49731963"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="af602-104">创建配置页</span><span class="sxs-lookup"><span data-stu-id="af602-104">Create a configuration page</span></span>

<span data-ttu-id="af602-105">配置页面是一种特殊类型 [的内容](content-page.md) 页，允许用户配置 Teams 应用的一些方面。</span><span class="sxs-lookup"><span data-stu-id="af602-105">A configuration page is a special type of [content page](content-page.md) that allows your users to configure some aspect of your Teams app.</span></span> <span data-ttu-id="af602-106">通常，这些用作以下部分：</span><span class="sxs-lookup"><span data-stu-id="af602-106">Typically these are used as part of:</span></span>

* <span data-ttu-id="af602-107">频道或群聊选项卡 - 配置页允许您从用户收集信息，并设置要 `contentUrl` 显示的内容页。</span><span class="sxs-lookup"><span data-stu-id="af602-107">A channel or group chat tab - The configuration page allows you to collect information from your users and set the `contentUrl` of the content page to display.</span></span>
* <span data-ttu-id="af602-108">[邮件扩展](~/messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="af602-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md)</span></span>
* <span data-ttu-id="af602-109">[Office 365 连接器](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span><span class="sxs-lookup"><span data-stu-id="af602-109">A [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span></span>

## <a name="configuring-a-channel-or-group-chat-tab"></a><span data-ttu-id="af602-110">配置频道或群聊选项卡</span><span class="sxs-lookup"><span data-stu-id="af602-110">Configuring a channel or group chat tab</span></span>

<span data-ttu-id="af602-111">配置页通知内容页应如何呈现。</span><span class="sxs-lookup"><span data-stu-id="af602-111">A configuration page informs the content page how it should render.</span></span> <span data-ttu-id="af602-112">您的应用程序必须引用 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) 并调用 `microsoft.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="af602-112">Your application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="af602-113">此外，URL 必须是安全的 HTTPS 终结点，并且可从云中访问。</span><span class="sxs-lookup"><span data-stu-id="af602-113">Additionally, your URLs must be secure HTTPS endpoints and available from the cloud.</span></span> <span data-ttu-id="af602-114">下面是一个配置页面示例。</span><span class="sxs-lookup"><span data-stu-id="af602-114">Below is a configuration page example.</span></span>

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

<span data-ttu-id="af602-115">用户在此处显示两个选项按钮，即"选择灰色"或"选择红色"，以使用红色或灰色图标显示选项卡内容。</span><span class="sxs-lookup"><span data-stu-id="af602-115">Here, the user is presented with two option buttons, **Select Gray** or **Select Red** to display the tab content with either a red or gray icon.</span></span> <span data-ttu-id="af602-116">选择相对按钮将触发 `saveGray()` `saveRed()` 或调用以下内容：</span><span class="sxs-lookup"><span data-stu-id="af602-116">Choosing the relative button fires `saveGray()` or `saveRed()` and invokes the following:</span></span>

1. <span data-ttu-id="af602-117">设置为 `settings.setValidityState(true)` true。</span><span class="sxs-lookup"><span data-stu-id="af602-117">The `settings.setValidityState(true)` is set to true.</span></span>
1. <span data-ttu-id="af602-118">`microsoftTeams.settings.registerOnSaveHandler()`触发事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="af602-118">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
1. <span data-ttu-id="af602-119">应用 **配置** 页面上的"保存"按钮（在 Teams 中上载）已启用。</span><span class="sxs-lookup"><span data-stu-id="af602-119">The **Save** button on the app's configuration page, uploaded in Teams, is enabled.</span></span>

<span data-ttu-id="af602-120">此代码可让 Teams 知道已满足配置要求，并且可以继续安装。</span><span class="sxs-lookup"><span data-stu-id="af602-120">This code lets Teams know that the configuration requirements have been satisfied and the installation can proceed.</span></span> <span data-ttu-id="af602-121">在 **Save** 中，将按接口为当前实例 `settings.setSettings()` `Settings` 设置参数。</span><span class="sxs-lookup"><span data-stu-id="af602-121">On **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface, for the current instance.</span></span> <span data-ttu-id="af602-122">有关详细信息，请参阅"设置 ["界面](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="af602-122">For more information, see [Settings interface](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="af602-123">最后 `saveEvent.notifySuccess()` ，调用它以指示内容 URL 已成功解析。</span><span class="sxs-lookup"><span data-stu-id="af602-123">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="af602-124">如果使用保存处理程序注册 `microsoftTeams.settings.registerOnSaveHandler()` ，则回调 `saveEvent.notifySuccess()` 必须调用或 `saveEvent.notifyFailure()` 指示配置的结果。</span><span class="sxs-lookup"><span data-stu-id="af602-124">If a save handler was registered using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="af602-125">如果未注册保存处理程序，则用户选择"保存"按钮 `saveEvent.notifySuccess()` 后，将立即 **进行** 调用。</span><span class="sxs-lookup"><span data-stu-id="af602-125">If no save handler was registered, the `saveEvent.notifySuccess()` call is automatically made immediately upon the user selecting the **Save** button.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="af602-126">获取选项卡设置的上下文数据</span><span class="sxs-lookup"><span data-stu-id="af602-126">Get context data for your tab settings</span></span>

<span data-ttu-id="af602-127">您的选项卡可能需要上下文信息来显示相关内容。</span><span class="sxs-lookup"><span data-stu-id="af602-127">Your tab might require contextual information to display relevant content.</span></span> <span data-ttu-id="af602-128">通过提供更加自定义的用户体验，上下文信息可以进一步增强选项卡的吸引力。</span><span class="sxs-lookup"><span data-stu-id="af602-128">Contextual information can further enhance your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="af602-129">Teams [上下文接口](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) 定义可用于选项卡配置的属性。</span><span class="sxs-lookup"><span data-stu-id="af602-129">The Teams [Context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) defines the properties that can be used for your tab configuration.</span></span> <span data-ttu-id="af602-130">可以通过两种方式收集上下文数据变量的值：</span><span class="sxs-lookup"><span data-stu-id="af602-130">You can collect the values of context data variables in two ways:</span></span>

1. <span data-ttu-id="af602-131">在清单中插入 URL 查询字符串占位符 `configurationURL` 。</span><span class="sxs-lookup"><span data-stu-id="af602-131">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

1. <span data-ttu-id="af602-132">使用 [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{}` 方法。</span><span class="sxs-lookup"><span data-stu-id="af602-132">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{}` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="af602-133">在 `configurationURL`</span><span class="sxs-lookup"><span data-stu-id="af602-133">Insert placeholders in the `configurationURL`</span></span>

<span data-ttu-id="af602-134">上下文接口占位符可以添加到你的基本 `configurationUrl` 。</span><span class="sxs-lookup"><span data-stu-id="af602-134">Context interface placeholders can be added to your base `configurationUrl`.</span></span> <span data-ttu-id="af602-135">例如：</span><span class="sxs-lookup"><span data-stu-id="af602-135">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="af602-136">基 URL</span><span class="sxs-lookup"><span data-stu-id="af602-136">Base Url</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="af602-137">包含查询字符串的基 URL</span><span class="sxs-lookup"><span data-stu-id="af602-137">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="af602-138">上传页面后，Teams 将用相关值更新查询字符串占位符。</span><span class="sxs-lookup"><span data-stu-id="af602-138">After your page has uploaded, the query string placeholders will be updated by Teams with the relevant values.</span></span> <span data-ttu-id="af602-139">可以在配置页中包括逻辑以检索和使用这些值。</span><span class="sxs-lookup"><span data-stu-id="af602-139">You can include logic in your configuration page to retrieve and use those values.</span></span> <span data-ttu-id="af602-140">有关使用 URL 查询字符串的信息，请参阅 MDN Web 文档中的 [URLSearchParams。](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) 下面是如何从上述属性中提取值 `configurationURL` 的示例：</span><span class="sxs-lookup"><span data-stu-id="af602-140">For more information on working with URL query strings see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN web docs. Here is an example of how to extract a value from the above `configurationURL` property:</span></span>

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="af602-141">使用 `getContext()` 函数检索上下文</span><span class="sxs-lookup"><span data-stu-id="af602-141">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="af602-142">调用该函数 `microsoftTeams.getContext((context) => {})` 时，将检索 [上下文接口](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="af602-142">When invoked, the `microsoftTeams.getContext((context) => {})` function retrieves the [Context interface](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="af602-143">可以将此函数添加到配置页面以检索上下文值：</span><span class="sxs-lookup"><span data-stu-id="af602-143">You can add this function to your configuration page to retrieve context values:</span></span>

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

## <a name="context-and-authentication"></a><span data-ttu-id="af602-144">上下文和身份验证</span><span class="sxs-lookup"><span data-stu-id="af602-144">Context and Authentication</span></span>

<span data-ttu-id="af602-145">在允许用户配置应用之前，可能需要进行身份验证，或者内容可能包括具有其自己的身份验证协议的源。</span><span class="sxs-lookup"><span data-stu-id="af602-145">You might require authentication before allowing a user to configure your app or your content might include sources that have their own authentication protocols.</span></span> <span data-ttu-id="af602-146">请参阅 ["在 Microsoft Teams 选项卡中](~/tabs/how-to/authentication/auth-flow-tab.md) 对用户进行身份验证"上下文信息可用于帮助构建身份验证请求和授权页面 URL。</span><span class="sxs-lookup"><span data-stu-id="af602-146">See [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md) Context information can be used to help construct authentication requests and authorization page URLs.</span></span>
<span data-ttu-id="af602-147">确保选项卡页中使用的所有域都列在 `manifest.json` `validDomains` 数组中。</span><span class="sxs-lookup"><span data-stu-id="af602-147">Make sure that all domains used in your tab pages are listed in the `manifest.json` `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="af602-148">修改或删除选项卡</span><span class="sxs-lookup"><span data-stu-id="af602-148">Modify or remove a tab</span></span>

<span data-ttu-id="af602-149">支持的删除选项可以进一步优化用户体验。</span><span class="sxs-lookup"><span data-stu-id="af602-149">Supported removal options can further refine the user experience.</span></span> <span data-ttu-id="af602-150">您可以通过将清单的属性设置为来允许用户修改、重新配置或重命名组/频道 `canUpdateConfiguration` 选项卡 `true` 。</span><span class="sxs-lookup"><span data-stu-id="af602-150">You can enable users to modify, reconfigure, or rename a group/channel tab by setting your manifest's `canUpdateConfiguration` property to `true`.</span></span>  <span data-ttu-id="af602-151">此外，你可以指定在删除选项卡时内容会发生什么情况，方法为在应用中包括删除选项页，并设置配置中的 (值 `removeUrl`  `setSettings()` ，) 。</span><span class="sxs-lookup"><span data-stu-id="af602-151">In addition, you can designate what happens to the content when a tab is removed by including a removal options page in your app and setting a value for the `removeUrl` property in the  `setSettings()` configuration (see below).</span></span> <span data-ttu-id="af602-152">个人选项卡不能修改，但用户可以卸载。</span><span class="sxs-lookup"><span data-stu-id="af602-152">Personal tabs can't be modified but can be uninstalled by the user.</span></span> <span data-ttu-id="af602-153">有关详细信息，请参阅 [为选项卡创建删除页](~/tabs/how-to/create-tab-pages/removal-page.md)。</span><span class="sxs-lookup"><span data-stu-id="af602-153">For more information, see [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

## <a name="mobile-clients"></a><span data-ttu-id="af602-154">移动客户端</span><span class="sxs-lookup"><span data-stu-id="af602-154">Mobile clients</span></span>

<span data-ttu-id="af602-155">如果你选择让频道/组选项卡显示在 Teams 移动客户端上，则配置必须具有属性值， (`setSettings()` `websiteUrl` 请参阅下面的) 。</span><span class="sxs-lookup"><span data-stu-id="af602-155">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span> <span data-ttu-id="af602-156">请参阅 [移动选项卡指南](~/tabs/design/tabs-mobile.md)。</span><span class="sxs-lookup"><span data-stu-id="af602-156">See [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span></span>

<span data-ttu-id="af602-157">用于删除页面和/ (移动客户端的 Microsoft Teams setSettings () 配置：</span><span class="sxs-lookup"><span data-stu-id="af602-157">Microsoft Teams setSettings() configuration for removal page and/or mobile clients:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "URL REQUIRED FOR MOBILE CLIENTS",
    removeUrl: "ADD REMOVAL PAGE URL HERE"
});
```
