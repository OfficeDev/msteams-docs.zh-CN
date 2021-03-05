---
title: Office 365 连接器
description: 介绍如何在 Microsoft Teams 中开始使用 Office 365 连接器
keywords: Teams o365 连接器
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 8f9fcc40ca0634ead0a6c5d7d0653ad4ab993860
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449253"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a><span data-ttu-id="ad2f3-104">为 Microsoft Teams 创建 Office 365 连接器</span><span class="sxs-lookup"><span data-stu-id="ad2f3-104">Creating Office 365 Connectors for Microsoft Teams</span></span>

><span data-ttu-id="ad2f3-105">使用 Microsoft Teams 应用，可以添加现有 Office 365 连接器或生成要包括在 Microsoft Teams 中的新连接器。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-105">With Microsoft Teams apps, you can add your existing Office 365 Connector or build a new one to include in Microsoft Teams.</span></span> <span data-ttu-id="ad2f3-106">有关详细信息 [，请参阅"生成您自己的](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) 连接器"。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-106">See [Build your own Connector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) for more information.</span></span>

## <a name="adding-a-connector-to-your-teams-app"></a><span data-ttu-id="ad2f3-107">将连接器添加到 Teams 应用</span><span class="sxs-lookup"><span data-stu-id="ad2f3-107">Adding a Connector to your Teams App</span></span>

<span data-ttu-id="ad2f3-108">你可以将已注册的连接器作为 Teams 应用包的一部分进行分发。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-108">You can distribute your registered Connector as part of your Teams app package.</span></span> <span data-ttu-id="ad2f3-109">无论是作为独立解决方案，还是体验在 Teams 中启用的多种功能之一，都可以将[](~/concepts/build-and-test/apps-package.md)连接器打包[](~/concepts/deploy-and-publish/apps-publish.md)并发布为 AppSource 提交的一部分，也可以直接向用户提供连接器以在 Teams 中上传。 [](~/concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="ad2f3-109">Whether as a standalone solution, or one of several [capabilities](~/concepts/extensibility-points.md) that your experience enables in Teams, you can [package](~/concepts/build-and-test/apps-package.md) and [publish](~/concepts/deploy-and-publish/apps-publish.md) your Connector as part of your AppSource submission, or you can provide it to users directly for uploading within Teams.</span></span>

<span data-ttu-id="ad2f3-110">若要分发连接器，您需要使用连接器开发人员仪表板 [进行注册](https://outlook.office.com/connectors/home/login/#/publish)。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-110">To distribute your Connector, you need to register by using the [Connectors Developer Dashboard](https://outlook.office.com/connectors/home/login/#/publish).</span></span> <span data-ttu-id="ad2f3-111">默认情况下，注册连接器后，假定连接器将在支持连接器的所有 Office 365 产品（包括 Outlook 和 Teams）中工作。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-111">By default, once a Connector is registered, it's assumed that your Connector will work in all Office 365 products that support them, including Outlook and Teams.</span></span> <span data-ttu-id="ad2f3-112">如果不是这种情况 _，_ 并且你需要创建仅在 Microsoft Teams 中工作的连接器，请直接通过 Microsoft Teams [应用提交联系我们](mailto:teamsubm@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-112">If that is _not_ the case and you need to create a Connector that only works in Microsoft Teams, contact us directly at [Microsoft Teams App Submissions](mailto:teamsubm@microsoft.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad2f3-113">选择" **在** 连接器开发人员仪表板中保存"后，连接器即已注册。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-113">After you choose **Save** in the Connectors Developer Dashboard, your Connector is registered.</span></span> <span data-ttu-id="ad2f3-114">如果你想要在 AppSource 中发布连接器，请按照将 Microsoft [Teams 应用发布到 AppSource 中的说明操作](~/concepts/deploy-and-publish/apps-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-114">If you want to publish your Connector in AppSource, follow the instructions in [Publish your Microsoft Teams app to AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="ad2f3-115">如果不想在 AppSource 中发布应用，而只是直接将其分发到组织，可以通过发布到组织来 [这样做](#publish-connectors-for-your-organization)。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-115">If you do not wish to publish your app in AppSource, and rather simply distribute it directly to your organization only, you can do so by [publishing to your organization](#publish-connectors-for-your-organization).</span></span> <span data-ttu-id="ad2f3-116">如果只想发布到组织，则无需在连接器仪表板上执行进一步操作。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-116">If you only want to publish to your organization, no further action is necessary on the Connector dashboard.</span></span>

### <a name="integrating-the-configuration-experience"></a><span data-ttu-id="ad2f3-117">集成配置体验</span><span class="sxs-lookup"><span data-stu-id="ad2f3-117">Integrating the configuration experience</span></span>

<span data-ttu-id="ad2f3-118">用户无需离开 Teams 客户端即可完成整个连接器配置体验。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-118">Your users will complete the entire Connector configuration experience without having to leave the Teams client.</span></span> <span data-ttu-id="ad2f3-119">为了实现此体验，Teams 将直接在 iframe 中嵌入你的配置页面。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-119">To achieve this experience, Teams will embed your configuration page directly within an iframe.</span></span> <span data-ttu-id="ad2f3-120">操作顺序如下所示：</span><span class="sxs-lookup"><span data-stu-id="ad2f3-120">The sequence of operations is as follows:</span></span>

1. <span data-ttu-id="ad2f3-121">用户单击连接器开始配置过程。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-121">The user clicks on your connector to begin the configuration process.</span></span>
2. <span data-ttu-id="ad2f3-122">Teams 将在线加载你的配置体验。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-122">Teams will load your configuration experience in line.</span></span>
3. <span data-ttu-id="ad2f3-123">用户与 Web 体验交互以完成配置。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-123">The user interacts with your web experience to complete the configuration.</span></span>
4. <span data-ttu-id="ad2f3-124">用户按"保存"，这将触发代码中的回调。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-124">The user presses "Save", which triggers a callback in your code.</span></span>
5. <span data-ttu-id="ad2f3-125">您的代码将处理保存事件，方法为检索以下 (webhook) 。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-125">Your code will process the save event by retrieving the webhook settings (documented below).</span></span> <span data-ttu-id="ad2f3-126">然后，您的代码应存储 Webhook 以稍后发布事件。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-126">Your code should then store the webhook to post events later.</span></span>

<span data-ttu-id="ad2f3-127">可以重复使用现有 Web 配置体验或创建单独版本以专门托管在 Teams 中。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-127">You can reuse your existing web configuration experience or create a separate version to be hosted specifically in Teams.</span></span> <span data-ttu-id="ad2f3-128">代码应：</span><span class="sxs-lookup"><span data-stu-id="ad2f3-128">Your code should:</span></span>

1. <span data-ttu-id="ad2f3-129">包括 Microsoft Teams JavaScript SDK。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-129">Include the Microsoft Teams JavaScript SDK.</span></span> <span data-ttu-id="ad2f3-130">这样，代码可以访问 API 来执行常见操作，如获取当前用户/频道/团队上下文和启动身份验证流。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-130">This gives your code access to APIs to perform common operations like getting the current user/channel/team context and initiating authentication flows.</span></span> <span data-ttu-id="ad2f3-131">通过调用初始化 `microsoftTeams.initialize()` SDK。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-131">Initialize the SDK by calling `microsoftTeams.initialize()`.</span></span>
2. <span data-ttu-id="ad2f3-132">在 `microsoftTeams.settings.setValidityState(true)` 要启用"保存"按钮时调用。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-132">Call `microsoftTeams.settings.setValidityState(true)` when you want to enable the Save button.</span></span> <span data-ttu-id="ad2f3-133">应作为对有效用户输入（如选择或字段更新）的响应进行此操作。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-133">You should do this as a response to valid user input, such as a selection or field update.</span></span>
3. <span data-ttu-id="ad2f3-134">注册 `microsoftTeams.settings.registerOnSaveHandler()` 事件处理程序，该事件处理程序在用户单击"保存"时调用。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-134">Register a `microsoftTeams.settings.registerOnSaveHandler()` event handler, which gets called when the user clicks Save.</span></span>
4. <span data-ttu-id="ad2f3-135">调用 `microsoftTeams.settings.setSettings()` 以保存连接器设置。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-135">Call `microsoftTeams.settings.setSettings()` to save the connector settings.</span></span> <span data-ttu-id="ad2f3-136">用户尝试更新连接器的现有配置时，此处保存的也是将在配置对话框中显示内容。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-136">What's saved here is also what will be shown in the configuration dialog if the user tries to update an existing configuration for your connector.</span></span>
5. <span data-ttu-id="ad2f3-137">调用 `microsoftTeams.settings.getSettings()` 以提取 webhook 属性，包括 URL 本身。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-137">Call `microsoftTeams.settings.getSettings()` to fetch webhook properties, including the URL itself.</span></span> <span data-ttu-id="ad2f3-138">除了在保存事件期间，还应在重新配置的情况下首次加载页面时调用此调用。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-138">You should call this  In addition to during the save event, you should also call this when your page is first loaded in the case of a re-configuration.</span></span>
6. <span data-ttu-id="ad2f3-139"> (可选) 注册事件处理程序，该事件处理程序在用户删除连接器 `microsoftTeams.settings.registerOnRemoveHandler()` 时调用。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-139">(Optional) Register a `microsoftTeams.settings.registerOnRemoveHandler()` event handler, which gets called when the user removes your connector.</span></span> <span data-ttu-id="ad2f3-140">此事件为服务提供了执行任何清理操作的机会。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-140">This event gives your service an opportunity to perform any cleanup actions.</span></span>

<span data-ttu-id="ad2f3-141">下面是用于创建不带 CSS 的连接器配置页的示例 HTML：</span><span class="sxs-lookup"><span data-stu-id="ad2f3-141">Here's a sample HTML to create a Connector configuration page without the CSS:</span></span>

```html
<h2>Send notifications when tasks are:</h2>
<div class="col-md-8">
    <section id="configSection">
        <form id="configForm">
            <input type="radio" name="notificationType" value="Create" onclick="onClick()"> Created
            <br>
            <br>
            <input type="radio" name="notificationType" value="Update" onclick="onClick()"> Updated
        </form>
    </section>
</div>

<script src="https://statics.teams.microsoft.com/sdk/v1.5.2/js/MicrosoftTeams.min.js" crossorigin="anonymous"></script>
<script src="/Scripts/jquery-1.10.2.js"></script>

<script type="text/javascript">

        function onClick() {
            microsoftTeams.settings.setValidityState(true);
        }

        microsoftTeams.initialize();
        microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
            var radios = document.getElementsByName('notificationType');

            var eventType = '';
            if (radios[0].checked) {
                eventType = radios[0].value;
            } else {
                eventType = radios[1].value;
            }

            microsoftTeams.settings.setSettings({
                 entityId: eventType,
                contentUrl: "https://YourSite/Connector/Setup",
                removeUrl:"https://YourSite/Connector/Setup",
                 configName: eventType
                });

            microsoftTeams.settings.getSettings(function (settings) {
                // We get the Webhook URL in settings.webhookUrl which needs to be saved. 
                // This can be used later to send notification.
            });

            saveEvent.notifySuccess();
        });

        microsoftTeams.settings.registerOnRemoveHandler(function (removeEvent) {
            var removeCalled = true;
            alert("Removed" + JSON.stringify(removeEvent));
        });

</script>
```

#### <a name="getsettings-response-properties"></a><span data-ttu-id="ad2f3-142">`GetSettings()` 响应属性</span><span class="sxs-lookup"><span data-stu-id="ad2f3-142">`GetSettings()` response properties</span></span>

>[!Note]
><span data-ttu-id="ad2f3-143">此处调用返回的参数与从选项卡调用此方法时不同，并且 `getSettings` 不同于此处记录 [的参数](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-143">The parameters returned by the `getSettings` call here are different than if you were to invoke this method from a tab, and differ from those documented [here](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span>

| <span data-ttu-id="ad2f3-144">参数</span><span class="sxs-lookup"><span data-stu-id="ad2f3-144">Parameter</span></span>   | <span data-ttu-id="ad2f3-145">详细信息</span><span class="sxs-lookup"><span data-stu-id="ad2f3-145">Details</span></span> |
|-------------|---------|
| `entityId`       | <span data-ttu-id="ad2f3-146">实体 ID，由代码在调用时设置 `setSettings()` 。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-146">The entity ID, as set by your code when calling `setSettings()`.</span></span> |
| `configName`  | <span data-ttu-id="ad2f3-147">调用时由代码设置的配置名称 `setSettings()` 。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-147">The configuration name, as set by your code when calling `setSettings()`.</span></span> |
| `contentUrl` | <span data-ttu-id="ad2f3-148">配置页的 URL，由代码在调用时设置 `setSettings()`</span><span class="sxs-lookup"><span data-stu-id="ad2f3-148">The URL of the configuration page, as set by your code when calling `setSettings()`</span></span> |
| `webhookUrl` | <span data-ttu-id="ad2f3-149">为此连接器创建的 webhook URL。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-149">The webhook URL created for this connector.</span></span> <span data-ttu-id="ad2f3-150">保留 Webhook URL，并将其用于 POST 结构化 JSON 以将卡片发送到通道。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-150">Persist the webhook URL and use it to POST structured JSON to send cards to the channel.</span></span> <span data-ttu-id="ad2f3-151">仅在应用程序成功返回时返回。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-151">The `webhookUrl` is returned only when application returns successfully.</span></span> |
| `appType` | <span data-ttu-id="ad2f3-152">返回的值可以是 `mail`、`groups` 或 `teams`，分别对应 Office 365 邮件、Office 365 组或 Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-152">The values returned can be `mail`, `groups` or `teams` corresponding to the Office 365 Mail, Office 365 Groups or Microsoft Teams respectively.</span></span> |
| `userObjectId` | <span data-ttu-id="ad2f3-153">这是与启动连接器设置的 Office 365 用户对应的唯一 ID。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-153">This is the unique id corresponding to the Office 365 user who initiated setup of the connector.</span></span> <span data-ttu-id="ad2f3-154">应该具备安全性。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-154">It should be secured.</span></span> <span data-ttu-id="ad2f3-155">可以使用此值将 Office 365 中设置配置的用户与服务中的用户关联起来。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-155">This value can be used to associate the user in Office 365 who set up the configuration to the user in your service.</span></span> |

<span data-ttu-id="ad2f3-156">如果需要在加载以上步骤 2 中的页面时对用户进行身份验证，请参阅此链接，了解有关嵌入[](~/tabs/how-to/authentication/auth-flow-tab.md)页面时如何集成登录的详细信息。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-156">If you need to authenticate the user as part of loading your page in step 2 above, refer to [this link](~/tabs/how-to/authentication/auth-flow-tab.md) for details on how you can integrate login when your page is embedded.</span></span>

> [!NOTE]
> <span data-ttu-id="ad2f3-157">由于跨客户端兼容性原因，代码在调用之前将需要使用 URL 和 `microsoftTeams.authentication.registerAuthenticationHandlers()` 成功/失败回调方法进行调用 `authenticate()` 。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-157">Due to cross-client compatibility reasons, your code will need to call `microsoftTeams.authentication.registerAuthenticationHandlers()` with the URL and success/failure callback methods before calling `authenticate()`.</span></span>

#### <a name="handling-edits"></a><span data-ttu-id="ad2f3-158">处理编辑</span><span class="sxs-lookup"><span data-stu-id="ad2f3-158">Handling edits</span></span>

<span data-ttu-id="ad2f3-159">代码应处理用户返回以编辑现有连接器配置。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-159">Your code should handle users returning to edit an existing connector configuration.</span></span> <span data-ttu-id="ad2f3-160">为此，请通过以下参数在初始配置 `microsoftTeams.settings.setSettings()` 期间调用：</span><span class="sxs-lookup"><span data-stu-id="ad2f3-160">To do this, call `microsoftTeams.settings.setSettings()` during the initial configuration with the following parameters:</span></span>

- <span data-ttu-id="ad2f3-161">`entityId` 是服务可以理解的自定义 ID，表示用户配置了哪些功能。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-161">`entityId` is the custom ID that is understood by your service and represents what the user has configured.</span></span>
- <span data-ttu-id="ad2f3-162">`configName` 是配置代码可以检索的友好名称</span><span class="sxs-lookup"><span data-stu-id="ad2f3-162">`configName` is a friendly name that your configuration code can retrieve</span></span>
- <span data-ttu-id="ad2f3-163">`contentUrl` 是在用户编辑现有连接器配置时加载的自定义 URL。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-163">`contentUrl` is a custom URL that gets loaded when a user edits an existing connector configuration.</span></span> <span data-ttu-id="ad2f3-164">您可以使用此 URL 更轻松地让代码处理编辑案例。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-164">You can use this URL to make it easier for your code to handle the edit case.</span></span>

<span data-ttu-id="ad2f3-165">通常，此调用作为保存事件处理程序的一部分进行。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-165">Typically, this call is made as part of your save event handler.</span></span> <span data-ttu-id="ad2f3-166">然后， `contentUrl` 当加载上述内容时，代码应调用以预填充配置 UI 中的任何 `getSettings()` 设置或表单。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-166">Then, when the `contentUrl` above is loaded, your code should call `getSettings()` to prepopulate any settings or forms in your configuration UI.</span></span>

#### <a name="handling-removals"></a><span data-ttu-id="ad2f3-167">处理删除</span><span class="sxs-lookup"><span data-stu-id="ad2f3-167">Handling removals</span></span>

<span data-ttu-id="ad2f3-168">可以选择在用户删除现有连接器配置时执行事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-168">You can optionally execute an event handler when the user removes an existing connector configuration.</span></span> <span data-ttu-id="ad2f3-169">通过调用注册此处理程序 `microsoftTeams.settings.registerOnRemoveHandler()` 。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-169">You register this handler by calling `microsoftTeams.settings.registerOnRemoveHandler()`.</span></span> <span data-ttu-id="ad2f3-170">此处理程序可用于执行清理操作，例如从数据库中删除条目。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-170">This handler can be used to perform cleanup operations such as removing entries from a database.</span></span>

### <a name="including-the-connector-in-your-manifest"></a><span data-ttu-id="ad2f3-171">在清单中包括连接器</span><span class="sxs-lookup"><span data-stu-id="ad2f3-171">Including the Connector in your Manifest</span></span>

<span data-ttu-id="ad2f3-172">你可以从门户下载自动生成的 Teams 应用清单。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-172">You can download the auto-generated Teams app manifest from the portal.</span></span> <span data-ttu-id="ad2f3-173">但是，在使用它测试或发布应用之前，必须执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="ad2f3-173">Before you can use it to test or publish your app, though, you must do the following:</span></span>

- <span data-ttu-id="ad2f3-174">[包括两个图标](../../concepts/build-and-test/apps-package.md#app-icons)。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-174">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
- <span data-ttu-id="ad2f3-175">修改清单的 `icons` 部分，以便引用图标的文件名，而不是 URL。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-175">Modify the `icons` portion of the manifest to refer to the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="ad2f3-176">以下 manifest.json 文件包含测试和提交应用程序所需的基本元素。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-176">The following manifest.json file contains the basic elements needed to test and submit your app.</span></span>

> [!NOTE]
> <span data-ttu-id="ad2f3-177">将以下示例中的 `id` 和 `connectorId` 替换为连接器的 GUID。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-177">Replace `id` and `connectorId` in the following example with the GUID of your Connector.</span></span>

#### <a name="example-manifestjson-with-connector"></a><span data-ttu-id="ad2f3-178">带连接器的示例 manifest.json</span><span class="sxs-lookup"><span data-stu-id="ad2f3-178">Example manifest.json with Connector</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "id": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
  "version": "1.0",
  "packageName": "com.sampleapp",
  "developer": {
    "name": "Publisher",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.microsoft.com",
    "termsOfUseUrl": "https://www.microsoft.com"
  },
  "description": {
    "full": "This is a sample manifest for an app with a connector with an inline configuration experience.",
    "short": "This is a sample manifest for an app with a connector."
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "configurationUrl": "https://teamstodoappconnectorwithinlineconfig.azurewebsites.net/Connector/Setup",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App Long Name"
  },
  "accentColor": "#FFFFFF"
}
```

## <a name="testing-your-connector"></a><span data-ttu-id="ad2f3-179">测试连接器</span><span class="sxs-lookup"><span data-stu-id="ad2f3-179">Testing your Connector</span></span>

<span data-ttu-id="ad2f3-180">若要测试连接器，请将其上传到团队中，就像使用任何其他应用程序一样。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-180">To test your Connector, upload it to a team as you would with any other app.</span></span> <span data-ttu-id="ad2f3-181">可使用连接器开发人员仪表板中的清单文件（按照上一部分的说明进行修改）和两个图标文件来创建 .zip 包。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-181">You can create a .zip package using the manifest file from the Connectors Developer Dashboard (modified as directed in the preceding section) and the two icon files.</span></span>

<span data-ttu-id="ad2f3-182">上传应用程序后，从任意频道打开连接器列表。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-182">After you upload the app, open the Connectors list from any channel.</span></span> <span data-ttu-id="ad2f3-183">向下滚动到底部，查看 **“上传”** 部分中的应用程序。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-183">Scroll to the bottom to see your app in the **Uploaded** section.</span></span>

![“连接器”对话框中上传部分的屏幕截图](~/assets/images/connectors/connector_dialog_uploaded.png)

<span data-ttu-id="ad2f3-185">现在可启动配置体验。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-185">You can now launch the configuration experience.</span></span> <span data-ttu-id="ad2f3-186">请注意，此流完全作为托管体验在 Microsoft Teams 中发生。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-186">Be aware that this flow occurs entirely within Microsoft Teams as a hosted experience.</span></span>

<span data-ttu-id="ad2f3-187">若要验证操作 `HttpPOST` 是否正常工作， [请将邮件发送到连接器](~/webhooks-and-connectors/how-to/connectors-using.md)。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-187">To verify that an `HttpPOST` action is working correctly, [send messages to your connector](~/webhooks-and-connectors/how-to/connectors-using.md).</span></span>

## <a name="publish-connectors-for-your-organization"></a><span data-ttu-id="ad2f3-188">为组织发布连接器</span><span class="sxs-lookup"><span data-stu-id="ad2f3-188">Publish Connectors for your organization</span></span>

<span data-ttu-id="ad2f3-189">有时，你可能不希望将连接器应用发布到公共 AppSource/Store，但希望它仅对贵组织的用户可用。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-189">Sometimes, you may not want to publish your connector app to the public AppSource/Store but would like it to be available only to the users in your organization.</span></span> <span data-ttu-id="ad2f3-190">在这种情况下，你可以将自定义连接器应用程序上载到 [组织的应用程序目录](~/concepts/deploy-and-publish/apps-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-190">In such cases, you can upload your custom connector app to your [organization's App Catalog](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="ad2f3-191">这样，连接器应用将仅适用于该组织，你无需将连接器发布到公共应用商店。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-191">This way, your connector app will be available only to that organization, and you will not need to publish your connector to the public store.</span></span>

<span data-ttu-id="ad2f3-192">上传应用包后，若要在团队中配置和使用连接器，可以按照以下步骤从组织的应用程序目录中安装：</span><span class="sxs-lookup"><span data-stu-id="ad2f3-192">Once you've uploaded your app package, to configure and use the connector in a Team it can be installed from the organization's app catalog by following these steps:</span></span>

1. <span data-ttu-id="ad2f3-193">从最左侧垂直导航栏中选择应用图标。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-193">Select the apps icon from the far left vertical navigation bar.</span></span>
1. <span data-ttu-id="ad2f3-194">在"**应用"** 窗口中，**选择"连接器"。**</span><span class="sxs-lookup"><span data-stu-id="ad2f3-194">In the **Apps** window select **Connectors**.</span></span>
1. <span data-ttu-id="ad2f3-195">选择要添加的连接器，将显示一个弹出对话框窗口。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-195">Select the connector that you want to add and a pop-up dialog window will display.</span></span>
1. <span data-ttu-id="ad2f3-196">选择 **"添加到团队栏** "。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-196">Select the **Add to a team** bar.</span></span>
1. <span data-ttu-id="ad2f3-197">在下一个对话框窗口中键入团队或频道名称。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-197">In the next dialog window type a team or channel name.</span></span>
1. <span data-ttu-id="ad2f3-198">从 **对话框窗口的右** 下角选择"设置连接线"栏。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-198">Select the **Set up a connector** bar from the bottom right corner of dialog window.</span></span>
1. <span data-ttu-id="ad2f3-199">该连接器将在" &#9679;&#9679;&#9679; = *>"* 部分中提供，该团队的更多选项"连接器  =>    =>  *所有*  =>  连接器"可供团队使用。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-199">The connector will be available in the  section &#9679;&#9679;&#9679; => *More options* => *Connectors* => *All* => *Connectors for you team* for that team.</span></span> <span data-ttu-id="ad2f3-200">可以通过滚动到此部分或搜索连接器应用来导航。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-200">You can navigate by scrolling to this section or search for the connector app.</span></span>
1. <span data-ttu-id="ad2f3-201">若要配置或修改连接器，请选择" **配置"** 栏。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-201">To configure or modify the connector select the **Configure** bar.</span></span>

## <a name="code-sample"></a><span data-ttu-id="ad2f3-202">代码示例</span><span class="sxs-lookup"><span data-stu-id="ad2f3-202">Code sample</span></span>
|<span data-ttu-id="ad2f3-203">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="ad2f3-203">**Sample name**</span></span> | <span data-ttu-id="ad2f3-204">**说明**</span><span class="sxs-lookup"><span data-stu-id="ad2f3-204">**Description**</span></span> | <span data-ttu-id="ad2f3-205">**.NET**</span><span class="sxs-lookup"><span data-stu-id="ad2f3-205">**.NET**</span></span> | <span data-ttu-id="ad2f3-206">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="ad2f3-206">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="ad2f3-207">连接器</span><span class="sxs-lookup"><span data-stu-id="ad2f3-207">Connectors</span></span>    | <span data-ttu-id="ad2f3-208">生成团队频道通知的示例 Office 365 连接器。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-208">Sample Office 365 Connector generating notifications to teams channel.</span></span>|   [<span data-ttu-id="ad2f3-209">View</span><span class="sxs-lookup"><span data-stu-id="ad2f3-209">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [<span data-ttu-id="ad2f3-210">View</span><span class="sxs-lookup"><span data-stu-id="ad2f3-210">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| <span data-ttu-id="ad2f3-211">通用连接器示例</span><span class="sxs-lookup"><span data-stu-id="ad2f3-211">Generic connectors sample</span></span> |<span data-ttu-id="ad2f3-212">易于为支持 Webhook 的任何系统自定义的通用连接器的示例代码。</span><span class="sxs-lookup"><span data-stu-id="ad2f3-212">Sample code for a generic connector that's easy to customize for any system which supports webhooks.</span></span>|  | [<span data-ttu-id="ad2f3-213">View</span><span class="sxs-lookup"><span data-stu-id="ad2f3-213">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|
