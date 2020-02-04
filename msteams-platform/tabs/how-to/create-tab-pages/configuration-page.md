---
title: 创建配置页
author: laujan
description: ''
keywords: 团队选项卡组频道可配置
ms.topic: conceptualF
ms.author: laujan
ms.openlocfilehash: c7b6b636a342c650667a1131e7899908744beedf
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673000"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="190f7-103">创建配置页</span><span class="sxs-lookup"><span data-stu-id="190f7-103">Create a configuration page</span></span>

<span data-ttu-id="190f7-104">配置页面是一种特殊类型的[内容页面](content-page.md)，允许您的用户配置团队应用程序的某些方面。</span><span class="sxs-lookup"><span data-stu-id="190f7-104">A configuration page is a special type of [content page](content-page.md) that allows your users to configure some aspect of your Teams app.</span></span> <span data-ttu-id="190f7-105">通常将它们用作以下部分：</span><span class="sxs-lookup"><span data-stu-id="190f7-105">Typically these are used as part of:</span></span>

* <span data-ttu-id="190f7-106">频道或组聊天选项卡-"配置" 页允许您收集用户的信息，并设置`contentUrl`要显示的内容页。</span><span class="sxs-lookup"><span data-stu-id="190f7-106">A channel or group chat tab - The configuration page allows you to collect information from your users and set the `contentUrl` of the content page to display.</span></span>
* <span data-ttu-id="190f7-107">[邮件扩展](~/messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="190f7-107">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md)</span></span>
* <span data-ttu-id="190f7-108">[Office 365 连接器](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span><span class="sxs-lookup"><span data-stu-id="190f7-108">A [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span></span>

## <a name="configuring-a-channel-or-group-chat-tab"></a><span data-ttu-id="190f7-109">配置频道或组聊天选项卡</span><span class="sxs-lookup"><span data-stu-id="190f7-109">Configuring a channel or group chat tab</span></span>

<span data-ttu-id="190f7-110">配置页面通知内容页面它应如何呈现。</span><span class="sxs-lookup"><span data-stu-id="190f7-110">A configuration page informs the content page how it should render.</span></span> <span data-ttu-id="190f7-111">您的应用程序必须引用[Microsoft 团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest)和调用`microsoft.initialize()`。</span><span class="sxs-lookup"><span data-stu-id="190f7-111">Your application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="190f7-112">此外，您的 Url 必须是安全的 HTTPS 终结点，并可从云中使用。</span><span class="sxs-lookup"><span data-stu-id="190f7-112">Additionally, your URLs must be secure HTTPS endpoints and available from the cloud.</span></span> <span data-ttu-id="190f7-113">下面是配置页面示例。</span><span class="sxs-lookup"><span data-stu-id="190f7-113">Below is a configuration page example.</span></span>

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

<span data-ttu-id="190f7-114">此时，用户会看到两个选项按钮，**选择 "灰色**" 或**选择 "红色**" 以显示带有红色或灰色图标的选项卡内容。</span><span class="sxs-lookup"><span data-stu-id="190f7-114">Here, the user is presented with two option buttons, **Select Gray** or **Select Red** to display the tab content with either a red or gray icon.</span></span> <span data-ttu-id="190f7-115">选择 "相对" 按钮`saveGray()`触发`saveRed()`或调用以下命令：</span><span class="sxs-lookup"><span data-stu-id="190f7-115">Choosing the relative button fires `saveGray()` or `saveRed()` and invokes the following:</span></span>

1. <span data-ttu-id="190f7-116">" `settings.setValidityState(true)` " 设置为 "true"。</span><span class="sxs-lookup"><span data-stu-id="190f7-116">The `settings.setValidityState(true)` is set to true.</span></span>
1. <span data-ttu-id="190f7-117">触发`microsoftTeams.settings.registerOnSaveHandler()`事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="190f7-117">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
1. <span data-ttu-id="190f7-118">启用 "在团队中上载的应用程序配置" 页上的 "**保存**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="190f7-118">The **Save** button on the app's configuration page, uploaded in Teams, is enabled.</span></span>

<span data-ttu-id="190f7-119">此代码使团队知道已满足配置要求，并且可以继续安装。</span><span class="sxs-lookup"><span data-stu-id="190f7-119">This code lets Teams know that the configuration requirements have been satisfied and the installation can proceed.</span></span> <span data-ttu-id="190f7-120">在**保存**时，由`Settings`接口`settings.setSettings()`定义的参数设置为当前实例（请参阅[Settings interface](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest) ）。</span><span class="sxs-lookup"><span data-stu-id="190f7-120">On **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface, for the current instance (See [Settings interface](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest) ).</span></span> <span data-ttu-id="190f7-121">最后， `saveEvent.notifySuccess()`将调用，以指示内容 URL 已成功解析。</span><span class="sxs-lookup"><span data-stu-id="190f7-121">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="190f7-122">如果保存的处理程序是使用`microsoftTeams.settings.registerOnSaveHandler()`注册的，则回调`saveEvent.notifySuccess()`必须`saveEvent.notifyFailure()`调用或以指示配置的结果。</span><span class="sxs-lookup"><span data-stu-id="190f7-122">If a save handler was registered using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="190f7-123">如果未注册保存处理程序，则`saveEvent.notifySuccess()`会在用户选择 "**保存**" 按钮后立即自动进行呼叫。</span><span class="sxs-lookup"><span data-stu-id="190f7-123">If no save handler was registered, the `saveEvent.notifySuccess()` call is automatically made immediately upon the user selecting the **Save** button.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="190f7-124">获取选项卡设置的上下文数据</span><span class="sxs-lookup"><span data-stu-id="190f7-124">Get context data for your tab settings</span></span>

<span data-ttu-id="190f7-125">您的选项卡可能需要上下文信息才能显示相关内容。</span><span class="sxs-lookup"><span data-stu-id="190f7-125">Your tab might require contextual information to display relevant content.</span></span> <span data-ttu-id="190f7-126">上下文信息可以通过提供更多自定义的用户体验来进一步增强您的选项卡的吸引力。</span><span class="sxs-lookup"><span data-stu-id="190f7-126">Contextual information can further enhance your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="190f7-127">团队[上下文界面](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest)定义可用于您的选项卡配置的属性。</span><span class="sxs-lookup"><span data-stu-id="190f7-127">The Teams [Context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) defines the properties that can be used for your tab configuration.</span></span> <span data-ttu-id="190f7-128">您可以通过两种方式收集上下文数据变量的值：</span><span class="sxs-lookup"><span data-stu-id="190f7-128">You can collect the values of context data variables in two ways:</span></span>

1. <span data-ttu-id="190f7-129">在清单中插入 URL 查询字符串占位符`configurationURL`。</span><span class="sxs-lookup"><span data-stu-id="190f7-129">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

1. <span data-ttu-id="190f7-130">使用 "[团队" SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) `microsoftTeams.getContext((context) =>{}`方法。</span><span class="sxs-lookup"><span data-stu-id="190f7-130">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) `microsoftTeams.getContext((context) =>{}` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="190f7-131">将占位符插入到`configurationURL`</span><span class="sxs-lookup"><span data-stu-id="190f7-131">Insert placeholders in the `configurationURL`</span></span>

<span data-ttu-id="190f7-132">可以将上下文界面占位符添加到您的`configurationUrl`基础。</span><span class="sxs-lookup"><span data-stu-id="190f7-132">Context interface placeholders can be added to your base `configurationUrl`.</span></span> <span data-ttu-id="190f7-133">例如：</span><span class="sxs-lookup"><span data-stu-id="190f7-133">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="190f7-134">基 Url</span><span class="sxs-lookup"><span data-stu-id="190f7-134">Base Url</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="190f7-135">包含查询字符串的基 URL</span><span class="sxs-lookup"><span data-stu-id="190f7-135">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="190f7-136">页面上载后，具有相关值的团队将更新查询字符串占位符。</span><span class="sxs-lookup"><span data-stu-id="190f7-136">After your page has uploaded, the query string placeholders will be updated by Teams with the relevant values.</span></span> <span data-ttu-id="190f7-137">您可以在配置页面中包含逻辑以检索和使用这些值。</span><span class="sxs-lookup"><span data-stu-id="190f7-137">You can include logic in your configuration page to retrieve and use those values.</span></span> <span data-ttu-id="190f7-138">有关使用 URL 查询字符串的详细信息，请参阅 MDN web 文档中的[URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) 。下面的示例展示了如何从上述`configurationURL`属性中提取值：</span><span class="sxs-lookup"><span data-stu-id="190f7-138">For more information on working with URL query strings see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN web docs. Here is an example of how to extract a value from the above `configurationURL` property:</span></span>

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="190f7-139">使用`getContext()`函数检索上下文</span><span class="sxs-lookup"><span data-stu-id="190f7-139">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="190f7-140">调用时，函数`microsoftTeams.getContext((context) => {})`将检索[上下文接口](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest)。</span><span class="sxs-lookup"><span data-stu-id="190f7-140">When invoked, the `microsoftTeams.getContext((context) => {})` function retrieves the [Context interface](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest).</span></span> <span data-ttu-id="190f7-141">您可以将此函数添加到您的配置页面以检索上下文值：</span><span class="sxs-lookup"><span data-stu-id="190f7-141">You can add this function to your configuration page to retrieve context values:</span></span>

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

## <a name="context-and-authentication"></a><span data-ttu-id="190f7-142">上下文和身份验证</span><span class="sxs-lookup"><span data-stu-id="190f7-142">Context and Authentication</span></span>

<span data-ttu-id="190f7-143">你可能需要进行身份验证，然后允许用户配置你的应用或你的内容可能包含具有自己的身份验证协议的源。</span><span class="sxs-lookup"><span data-stu-id="190f7-143">You might require authentication before allowing a user to configure your app or your content might include sources that have their own authentication protocols.</span></span> <span data-ttu-id="190f7-144">请参阅[对 Microsoft 团队中的用户进行身份验证选项卡](~/tabs/how-to/authentication/auth-flow-tab.md)上下文信息可用于帮助构造身份验证请求和授权页面 url。</span><span class="sxs-lookup"><span data-stu-id="190f7-144">See [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md) Context information can be used to help construct authentication requests and authorization page URLs.</span></span>
<span data-ttu-id="190f7-145">确保在您的选项卡页中使用的所有域都列`manifest.json` `validDomains`在数组中。</span><span class="sxs-lookup"><span data-stu-id="190f7-145">Make sure that all domains used in your tab pages are listed in the `manifest.json` `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="190f7-146">修改或删除选项卡</span><span class="sxs-lookup"><span data-stu-id="190f7-146">Modify or remove a tab</span></span>

<span data-ttu-id="190f7-147">支持的删除选项可进一步优化用户体验。</span><span class="sxs-lookup"><span data-stu-id="190f7-147">Supported removal options can further refine the user experience.</span></span> <span data-ttu-id="190f7-148">您可以通过将清单的`canUpdateConfiguration`属性设置为`true`，使用户能够修改、重新配置或重命名 "组/通道" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="190f7-148">You can enable users to modify, reconfigure, or rename a group/channel tab by setting your manifest's `canUpdateConfiguration` property to `true`.</span></span>  <span data-ttu-id="190f7-149">此外，通过在应用中添加 "删除选项" 页并在`removeUrl` `setSettings()`配置中设置属性值，可以指定在删除选项卡时内容会发生什么情况（请参阅下文）。</span><span class="sxs-lookup"><span data-stu-id="190f7-149">In addition, you can designate what happens to the content when a tab is removed by including a removal options page in your app and setting a value for the `removeUrl` property in the  `setSettings()` configuration (see below).</span></span> <span data-ttu-id="190f7-150">个人选项卡不能修改，但可由用户卸载。</span><span class="sxs-lookup"><span data-stu-id="190f7-150">Personal tabs can't be modified but can be uninstalled by the user.</span></span> <span data-ttu-id="190f7-151">有关详细信息，请参阅[创建选项卡的删除页](~/tabs/how-to/create-tab-pages/removal-page.md)。</span><span class="sxs-lookup"><span data-stu-id="190f7-151">For more information, see [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

## <a name="mobile-clients"></a><span data-ttu-id="190f7-152">移动客户端</span><span class="sxs-lookup"><span data-stu-id="190f7-152">Mobile clients</span></span>

<span data-ttu-id="190f7-153">如果选择在工作组移动客户端上显示频道/组选项卡，则`setSettings()`配置必须具有`websiteUrl`属性值（请参阅下文）。</span><span class="sxs-lookup"><span data-stu-id="190f7-153">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span> <span data-ttu-id="190f7-154">将很快发布对移动客户端上的选项卡的完全支持。</span><span class="sxs-lookup"><span data-stu-id="190f7-154">Full support for tabs on mobile clients will be released soon.</span></span> <span data-ttu-id="190f7-155">若要准备更新，应按照移动选项卡[上的选项卡指南中](~/tabs/design/tabs-mobile.md)的步骤创建选项卡。</span><span class="sxs-lookup"><span data-stu-id="190f7-155">To prepare for the update, you should follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span>

<span data-ttu-id="190f7-156">Microsoft 团队 setSettings （）配置，用于删除页面和/或移动客户端：</span><span class="sxs-lookup"><span data-stu-id="190f7-156">Microsoft Teams setSettings() configuration for removal page and/or mobile clients:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "URL REQUIRED FOR MOBILE CLIENTS",
    removeUrl: "ADD REMOVAL PAGE URL HERE"
});
```
