---
title: 创建配置页
author: laujan
description: 如何创建配置页
keywords: 团队选项卡组频道可配置
ms.topic: conceptualF
ms.author: lajanuar
ms.openlocfilehash: 6288fc8c296ebf0aa85ffe8e08234e5faf22a1ef
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "47819023"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="ba588-104">创建配置页</span><span class="sxs-lookup"><span data-stu-id="ba588-104">Create a configuration page</span></span>

<span data-ttu-id="ba588-105">配置页面是一种特殊类型的 [内容页面](content-page.md) ，允许您的用户配置团队应用程序的某些方面。</span><span class="sxs-lookup"><span data-stu-id="ba588-105">A configuration page is a special type of [content page](content-page.md) that allows your users to configure some aspect of your Teams app.</span></span> <span data-ttu-id="ba588-106">通常将它们用作以下部分：</span><span class="sxs-lookup"><span data-stu-id="ba588-106">Typically these are used as part of:</span></span>

* <span data-ttu-id="ba588-107">频道或组聊天选项卡-"配置" 页允许您收集用户的信息，并设置 `contentUrl` 要显示的内容页。</span><span class="sxs-lookup"><span data-stu-id="ba588-107">A channel or group chat tab - The configuration page allows you to collect information from your users and set the `contentUrl` of the content page to display.</span></span>
* <span data-ttu-id="ba588-108">[邮件扩展](~/messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="ba588-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md)</span></span>
* <span data-ttu-id="ba588-109">[Office 365 连接器](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span><span class="sxs-lookup"><span data-stu-id="ba588-109">A [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span></span>

## <a name="configuring-a-channel-or-group-chat-tab"></a><span data-ttu-id="ba588-110">配置频道或组聊天选项卡</span><span class="sxs-lookup"><span data-stu-id="ba588-110">Configuring a channel or group chat tab</span></span>

<span data-ttu-id="ba588-111">配置页面通知内容页面它应如何呈现。</span><span class="sxs-lookup"><span data-stu-id="ba588-111">A configuration page informs the content page how it should render.</span></span> <span data-ttu-id="ba588-112">您的应用程序必须引用 [Microsoft 团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) 和调用 `microsoft.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="ba588-112">Your application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="ba588-113">此外，您的 Url 必须是安全的 HTTPS 终结点，并可从云中使用。</span><span class="sxs-lookup"><span data-stu-id="ba588-113">Additionally, your URLs must be secure HTTPS endpoints and available from the cloud.</span></span> <span data-ttu-id="ba588-114">下面是配置页面示例。</span><span class="sxs-lookup"><span data-stu-id="ba588-114">Below is a configuration page example.</span></span>

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

<span data-ttu-id="ba588-115">此时，用户会看到两个选项按钮， **选择 "灰色** " 或 **选择 "红色** " 以显示带有红色或灰色图标的选项卡内容。</span><span class="sxs-lookup"><span data-stu-id="ba588-115">Here, the user is presented with two option buttons, **Select Gray** or **Select Red** to display the tab content with either a red or gray icon.</span></span> <span data-ttu-id="ba588-116">选择 "相对" 按钮触发 `saveGray()` 或 `saveRed()` 调用以下命令：</span><span class="sxs-lookup"><span data-stu-id="ba588-116">Choosing the relative button fires `saveGray()` or `saveRed()` and invokes the following:</span></span>

1. <span data-ttu-id="ba588-117">"" `settings.setValidityState(true)` 设置为 "true"。</span><span class="sxs-lookup"><span data-stu-id="ba588-117">The `settings.setValidityState(true)` is set to true.</span></span>
1. <span data-ttu-id="ba588-118">`microsoftTeams.settings.registerOnSaveHandler()`触发事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="ba588-118">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
1. <span data-ttu-id="ba588-119">启用 "在团队中上载的应用程序配置" 页上的 " **保存** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="ba588-119">The **Save** button on the app's configuration page, uploaded in Teams, is enabled.</span></span>

<span data-ttu-id="ba588-120">此代码使团队知道已满足配置要求，并且可以继续安装。</span><span class="sxs-lookup"><span data-stu-id="ba588-120">This code lets Teams know that the configuration requirements have been satisfied and the installation can proceed.</span></span> <span data-ttu-id="ba588-121">在 **保存**时， `settings.setSettings()` 由接口定义的参数设置为 `Settings` 当前实例 (请参阅 [Settings interface](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest) ) 。</span><span class="sxs-lookup"><span data-stu-id="ba588-121">On **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface, for the current instance (See [Settings interface](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest) ).</span></span> <span data-ttu-id="ba588-122">最后， `saveEvent.notifySuccess()` 将调用，以指示内容 URL 已成功解析。</span><span class="sxs-lookup"><span data-stu-id="ba588-122">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="ba588-123">如果保存的处理程序是使用注册的 `microsoftTeams.settings.registerOnSaveHandler()` ，则回调必须调用 `saveEvent.notifySuccess()` 或 `saveEvent.notifyFailure()` 以指示配置的结果。</span><span class="sxs-lookup"><span data-stu-id="ba588-123">If a save handler was registered using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="ba588-124">如果未注册保存处理程序，则 `saveEvent.notifySuccess()` 会在用户选择 " **保存** " 按钮后立即自动进行呼叫。</span><span class="sxs-lookup"><span data-stu-id="ba588-124">If no save handler was registered, the `saveEvent.notifySuccess()` call is automatically made immediately upon the user selecting the **Save** button.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="ba588-125">获取选项卡设置的上下文数据</span><span class="sxs-lookup"><span data-stu-id="ba588-125">Get context data for your tab settings</span></span>

<span data-ttu-id="ba588-126">您的选项卡可能需要上下文信息才能显示相关内容。</span><span class="sxs-lookup"><span data-stu-id="ba588-126">Your tab might require contextual information to display relevant content.</span></span> <span data-ttu-id="ba588-127">上下文信息可以通过提供更多自定义的用户体验来进一步增强您的选项卡的吸引力。</span><span class="sxs-lookup"><span data-stu-id="ba588-127">Contextual information can further enhance your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="ba588-128">团队 [上下文界面](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) 定义可用于您的选项卡配置的属性。</span><span class="sxs-lookup"><span data-stu-id="ba588-128">The Teams [Context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) defines the properties that can be used for your tab configuration.</span></span> <span data-ttu-id="ba588-129">您可以通过两种方式收集上下文数据变量的值：</span><span class="sxs-lookup"><span data-stu-id="ba588-129">You can collect the values of context data variables in two ways:</span></span>

1. <span data-ttu-id="ba588-130">在清单中插入 URL 查询字符串占位符 `configurationURL` 。</span><span class="sxs-lookup"><span data-stu-id="ba588-130">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

1. <span data-ttu-id="ba588-131">使用 " [团队" SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) `microsoftTeams.getContext((context) =>{}` 方法。</span><span class="sxs-lookup"><span data-stu-id="ba588-131">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) `microsoftTeams.getContext((context) =>{}` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="ba588-132">将占位符插入到 `configurationURL`</span><span class="sxs-lookup"><span data-stu-id="ba588-132">Insert placeholders in the `configurationURL`</span></span>

<span data-ttu-id="ba588-133">可以将上下文界面占位符添加到您的基础 `configurationUrl` 。</span><span class="sxs-lookup"><span data-stu-id="ba588-133">Context interface placeholders can be added to your base `configurationUrl`.</span></span> <span data-ttu-id="ba588-134">例如：</span><span class="sxs-lookup"><span data-stu-id="ba588-134">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="ba588-135">基 Url</span><span class="sxs-lookup"><span data-stu-id="ba588-135">Base Url</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="ba588-136">包含查询字符串的基 URL</span><span class="sxs-lookup"><span data-stu-id="ba588-136">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="ba588-137">页面上载后，具有相关值的团队将更新查询字符串占位符。</span><span class="sxs-lookup"><span data-stu-id="ba588-137">After your page has uploaded, the query string placeholders will be updated by Teams with the relevant values.</span></span> <span data-ttu-id="ba588-138">您可以在配置页面中包含逻辑以检索和使用这些值。</span><span class="sxs-lookup"><span data-stu-id="ba588-138">You can include logic in your configuration page to retrieve and use those values.</span></span> <span data-ttu-id="ba588-139">有关使用 URL 查询字符串的详细信息，请参阅 MDN web 文档中的 [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) 。下面的示例展示了如何从上述属性中提取值 `configurationURL` ：</span><span class="sxs-lookup"><span data-stu-id="ba588-139">For more information on working with URL query strings see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN web docs. Here is an example of how to extract a value from the above `configurationURL` property:</span></span>

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="ba588-140">使用 `getContext()` 函数检索上下文</span><span class="sxs-lookup"><span data-stu-id="ba588-140">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="ba588-141">调用时， `microsoftTeams.getContext((context) => {})` 函数将检索 [上下文接口](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest)。</span><span class="sxs-lookup"><span data-stu-id="ba588-141">When invoked, the `microsoftTeams.getContext((context) => {})` function retrieves the [Context interface](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest).</span></span> <span data-ttu-id="ba588-142">您可以将此函数添加到您的配置页面以检索上下文值：</span><span class="sxs-lookup"><span data-stu-id="ba588-142">You can add this function to your configuration page to retrieve context values:</span></span>

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

## <a name="context-and-authentication"></a><span data-ttu-id="ba588-143">上下文和身份验证</span><span class="sxs-lookup"><span data-stu-id="ba588-143">Context and Authentication</span></span>

<span data-ttu-id="ba588-144">你可能需要进行身份验证，然后允许用户配置你的应用或你的内容可能包含具有自己的身份验证协议的源。</span><span class="sxs-lookup"><span data-stu-id="ba588-144">You might require authentication before allowing a user to configure your app or your content might include sources that have their own authentication protocols.</span></span> <span data-ttu-id="ba588-145">请参阅 [对 Microsoft 团队中的用户进行身份验证选项卡](~/tabs/how-to/authentication/auth-flow-tab.md) 上下文信息可用于帮助构造身份验证请求和授权页面 url。</span><span class="sxs-lookup"><span data-stu-id="ba588-145">See [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md) Context information can be used to help construct authentication requests and authorization page URLs.</span></span>
<span data-ttu-id="ba588-146">确保在您的选项卡页中使用的所有域都列在 `manifest.json` `validDomains` 数组中。</span><span class="sxs-lookup"><span data-stu-id="ba588-146">Make sure that all domains used in your tab pages are listed in the `manifest.json` `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="ba588-147">修改或删除选项卡</span><span class="sxs-lookup"><span data-stu-id="ba588-147">Modify or remove a tab</span></span>

<span data-ttu-id="ba588-148">支持的删除选项可进一步优化用户体验。</span><span class="sxs-lookup"><span data-stu-id="ba588-148">Supported removal options can further refine the user experience.</span></span> <span data-ttu-id="ba588-149">您可以通过将清单的属性设置为，使用户能够修改、重新配置或重命名 "组/通道" 选项卡 `canUpdateConfiguration` `true` 。</span><span class="sxs-lookup"><span data-stu-id="ba588-149">You can enable users to modify, reconfigure, or rename a group/channel tab by setting your manifest's `canUpdateConfiguration` property to `true`.</span></span>  <span data-ttu-id="ba588-150">此外，通过在应用中添加 "删除选项" 页并在配置 (中设置属性的值，可以指定在删除选项卡时对内容所发生的操作 `removeUrl`  `setSettings()` 。请参阅下面的) 。</span><span class="sxs-lookup"><span data-stu-id="ba588-150">In addition, you can designate what happens to the content when a tab is removed by including a removal options page in your app and setting a value for the `removeUrl` property in the  `setSettings()` configuration (see below).</span></span> <span data-ttu-id="ba588-151">个人选项卡不能修改，但可由用户卸载。</span><span class="sxs-lookup"><span data-stu-id="ba588-151">Personal tabs can't be modified but can be uninstalled by the user.</span></span> <span data-ttu-id="ba588-152">有关详细信息，请参阅 [创建选项卡的删除页](~/tabs/how-to/create-tab-pages/removal-page.md)。</span><span class="sxs-lookup"><span data-stu-id="ba588-152">For more information, see [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

## <a name="mobile-clients"></a><span data-ttu-id="ba588-153">移动客户端</span><span class="sxs-lookup"><span data-stu-id="ba588-153">Mobile clients</span></span>

<span data-ttu-id="ba588-154">如果选择在工作组移动客户端上显示 "频道/组" 选项卡，则该 `setSettings()` 配置必须具有该属性的值 `websiteUrl` (请参阅下) 。</span><span class="sxs-lookup"><span data-stu-id="ba588-154">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span> <span data-ttu-id="ba588-155">将很快发布对移动客户端上的选项卡的完全支持。</span><span class="sxs-lookup"><span data-stu-id="ba588-155">Full support for tabs on mobile clients will be released soon.</span></span> <span data-ttu-id="ba588-156">若要准备更新，应按照移动选项卡 [上的选项卡指南中](~/tabs/design/tabs-mobile.md) 的步骤创建选项卡。</span><span class="sxs-lookup"><span data-stu-id="ba588-156">To prepare for the update, you should follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span>

<span data-ttu-id="ba588-157">Microsoft 团队 setSettings ( 用于删除页面和/或移动客户端的 # A1 配置：</span><span class="sxs-lookup"><span data-stu-id="ba588-157">Microsoft Teams setSettings() configuration for removal page and/or mobile clients:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "URL REQUIRED FOR MOBILE CLIENTS",
    removeUrl: "ADD REMOVAL PAGE URL HERE"
});
```
