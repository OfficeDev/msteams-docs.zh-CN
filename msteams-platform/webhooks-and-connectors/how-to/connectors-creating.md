---
title: Office 365 连接器
description: 介绍如何开始使用 Office 365 中的连接器Microsoft Teams
keywords: Teams o365 连接器
localization_priority: Normal
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 1598b84fc1c36547aa4c814cdf03404a3833779e
ms.sourcegitcommit: c55b0d2a4c1f8945e49b0b7c0b08c0eb3da3d2be
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2021
ms.locfileid: "52646319"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a><span data-ttu-id="84a7f-104">创建Office 365连接器Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="84a7f-104">Creating Office 365 Connectors for Microsoft Teams</span></span>

<span data-ttu-id="84a7f-105">通过Microsoft Teams应用，你可以添加现有 Office 365 连接器或生成要包括在 Microsoft Teams 中的新连接器。</span><span class="sxs-lookup"><span data-stu-id="84a7f-105">With Microsoft Teams apps, you can add your existing Office 365 Connector or build a new one to include in Microsoft Teams.</span></span> <span data-ttu-id="84a7f-106">有关详细信息 [，请参阅构建](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) 你自己的连接器。</span><span class="sxs-lookup"><span data-stu-id="84a7f-106">See [Build your own Connector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) for more information.</span></span>

## <a name="adding-a-connector-to-your-teams-app"></a><span data-ttu-id="84a7f-107">将连接器添加到 Teams 应用</span><span class="sxs-lookup"><span data-stu-id="84a7f-107">Adding a Connector to your Teams App</span></span>

<span data-ttu-id="84a7f-108">你可以将已注册的连接器作为 Teams 应用包的一部分进行分布。</span><span class="sxs-lookup"><span data-stu-id="84a7f-108">You can distribute your registered Connector as part of your Teams app package.</span></span> <span data-ttu-id="84a7f-109">无论是作为独立解决方案，还是体验在 Teams 中启用的多种功能之一，都可以将连接器打包[](~/concepts/build-and-test/apps-package.md)并发布[](~/concepts/deploy-and-publish/apps-publish.md)为 AppSource 提交的一部分，也可以直接向用户在 Teams 中上传。 [](~/concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="84a7f-109">Whether as a standalone solution, or one of several [capabilities](~/concepts/extensibility-points.md) that your experience enables in Teams, you can [package](~/concepts/build-and-test/apps-package.md) and [publish](~/concepts/deploy-and-publish/apps-publish.md) your Connector as part of your AppSource submission, or you can provide it to users directly for uploading within Teams.</span></span>

<span data-ttu-id="84a7f-110">若要分发连接器，你需要使用连接器开发人员仪表板 [进行注册](https://outlook.office.com/connectors/home/login/#/publish)。</span><span class="sxs-lookup"><span data-stu-id="84a7f-110">To distribute your Connector, you need to register by using the [Connectors Developer Dashboard](https://outlook.office.com/connectors/home/login/#/publish).</span></span> <span data-ttu-id="84a7f-111">默认情况下，注册连接器后，假定连接器将在支持连接器的所有 Office 365 产品中工作，包括 Outlook 和 Teams。</span><span class="sxs-lookup"><span data-stu-id="84a7f-111">By default, once a Connector is registered, it's assumed that your Connector will work in all Office 365 products that support them, including Outlook and Teams.</span></span> <span data-ttu-id="84a7f-112">如果并非如此 _，_ 并且你需要创建仅在 Microsoft Teams 中工作的连接器，请直接Microsoft Teams [应用提交。](mailto:teamsubm@microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="84a7f-112">If that is _not_ the case and you need to create a Connector that only works in Microsoft Teams, contact us directly at [Microsoft Teams App Submissions](mailto:teamsubm@microsoft.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84a7f-113">在连接器 **开发人员** 仪表板中选择"保存"后，连接器即已注册。</span><span class="sxs-lookup"><span data-stu-id="84a7f-113">After you choose **Save** in the Connectors Developer Dashboard, your Connector is registered.</span></span> <span data-ttu-id="84a7f-114">若要在 AppSource 中发布连接器，请按照将应用发布到[AppSource Microsoft Teams中的说明操作](~/concepts/deploy-and-publish/apps-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="84a7f-114">If you want to publish your Connector in AppSource, follow the instructions in [Publish your Microsoft Teams app to AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="84a7f-115">如果你不希望在 AppSource 中发布应用，而只是直接将其分发到你的组织，可以通过发布到你的组织 [来这样做](#publish-connectors-for-your-organization)。</span><span class="sxs-lookup"><span data-stu-id="84a7f-115">If you do not wish to publish your app in AppSource, and rather simply distribute it directly to your organization only, you can do so by [publishing to your organization](#publish-connectors-for-your-organization).</span></span> <span data-ttu-id="84a7f-116">如果只想发布到组织，则无需在连接器仪表板上执行任何进一步的操作。</span><span class="sxs-lookup"><span data-stu-id="84a7f-116">If you only want to publish to your organization, no further action is necessary on the Connector dashboard.</span></span>

### <a name="integrating-the-configuration-experience"></a><span data-ttu-id="84a7f-117">集成配置体验</span><span class="sxs-lookup"><span data-stu-id="84a7f-117">Integrating the configuration experience</span></span>

<span data-ttu-id="84a7f-118">您的用户将完成整个连接器配置体验，而无需离开 Teams 客户端。</span><span class="sxs-lookup"><span data-stu-id="84a7f-118">Your users will complete the entire Connector configuration experience without having to leave the Teams client.</span></span> <span data-ttu-id="84a7f-119">若要实现此体验，Teams将配置页面直接嵌入 iframe 中。</span><span class="sxs-lookup"><span data-stu-id="84a7f-119">To achieve this experience, Teams will embed your configuration page directly within an iframe.</span></span> <span data-ttu-id="84a7f-120">操作顺序如下所示：</span><span class="sxs-lookup"><span data-stu-id="84a7f-120">The sequence of operations is as follows:</span></span>

1. <span data-ttu-id="84a7f-121">用户单击连接器开始配置过程。</span><span class="sxs-lookup"><span data-stu-id="84a7f-121">The user clicks on your connector to begin the configuration process.</span></span>
2. <span data-ttu-id="84a7f-122">Teams将在线加载配置体验。</span><span class="sxs-lookup"><span data-stu-id="84a7f-122">Teams will load your configuration experience in line.</span></span>
3. <span data-ttu-id="84a7f-123">用户与 Web 体验交互以完成配置。</span><span class="sxs-lookup"><span data-stu-id="84a7f-123">The user interacts with your web experience to complete the configuration.</span></span>
4. <span data-ttu-id="84a7f-124">用户按"保存"，这将触发代码中的回调。</span><span class="sxs-lookup"><span data-stu-id="84a7f-124">The user presses "Save", which triggers a callback in your code.</span></span>
5. <span data-ttu-id="84a7f-125">代码将处理保存事件，方法为检索以下 (webhook) 。</span><span class="sxs-lookup"><span data-stu-id="84a7f-125">Your code will process the save event by retrieving the webhook settings (documented below).</span></span> <span data-ttu-id="84a7f-126">然后，代码应存储 Webhook 以稍后发布事件。</span><span class="sxs-lookup"><span data-stu-id="84a7f-126">Your code should then store the webhook to post events later.</span></span>

<span data-ttu-id="84a7f-127">可以重用现有 Web 配置体验，或创建一个单独的版本以专门托管在 Teams。</span><span class="sxs-lookup"><span data-stu-id="84a7f-127">You can reuse your existing web configuration experience or create a separate version to be hosted specifically in Teams.</span></span> <span data-ttu-id="84a7f-128">代码应：</span><span class="sxs-lookup"><span data-stu-id="84a7f-128">Your code should:</span></span>

1. <span data-ttu-id="84a7f-129">包括 Microsoft Teams JavaScript SDK。</span><span class="sxs-lookup"><span data-stu-id="84a7f-129">Include the Microsoft Teams JavaScript SDK.</span></span> <span data-ttu-id="84a7f-130">这样，代码可以访问 API 来执行常见操作，如获取当前用户/频道/团队上下文和启动身份验证流。</span><span class="sxs-lookup"><span data-stu-id="84a7f-130">This gives your code access to APIs to perform common operations like getting the current user/channel/team context and initiating authentication flows.</span></span> <span data-ttu-id="84a7f-131">通过调用`microsoftTeams.initialize()`初始化 SDK。</span><span class="sxs-lookup"><span data-stu-id="84a7f-131">Initialize the SDK by calling `microsoftTeams.initialize()`.</span></span>
2. <span data-ttu-id="84a7f-132">在 `microsoftTeams.settings.setValidityState(true)` 要启用"保存"按钮时调用。</span><span class="sxs-lookup"><span data-stu-id="84a7f-132">Call `microsoftTeams.settings.setValidityState(true)` when you want to enable the Save button.</span></span> <span data-ttu-id="84a7f-133">应作为对有效用户输入（如选择或字段更新）的响应来这样做。</span><span class="sxs-lookup"><span data-stu-id="84a7f-133">You should do this as a response to valid user input, such as a selection or field update.</span></span>
3. <span data-ttu-id="84a7f-134">注册 `microsoftTeams.settings.registerOnSaveHandler()` 事件处理程序，该事件处理程序在用户单击"保存"时调用。</span><span class="sxs-lookup"><span data-stu-id="84a7f-134">Register a `microsoftTeams.settings.registerOnSaveHandler()` event handler, which gets called when the user clicks Save.</span></span>
4. <span data-ttu-id="84a7f-135">调用 `microsoftTeams.settings.setSettings()` 以保存连接器设置。</span><span class="sxs-lookup"><span data-stu-id="84a7f-135">Call `microsoftTeams.settings.setSettings()` to save the connector settings.</span></span> <span data-ttu-id="84a7f-136">如果用户尝试更新连接器的现有配置，此处保存的也是将在配置对话框中显示内容。</span><span class="sxs-lookup"><span data-stu-id="84a7f-136">What's saved here is also what will be shown in the configuration dialog if the user tries to update an existing configuration for your connector.</span></span>
5. <span data-ttu-id="84a7f-137">调用 `microsoftTeams.settings.getSettings()` 以提取 webhook 属性，包括 URL 本身。</span><span class="sxs-lookup"><span data-stu-id="84a7f-137">Call `microsoftTeams.settings.getSettings()` to fetch webhook properties, including the URL itself.</span></span> <span data-ttu-id="84a7f-138">除了在保存事件期间之外，还应在重新配置的情况下首次加载页面时调用此调用。</span><span class="sxs-lookup"><span data-stu-id="84a7f-138">You should call this  In addition to during the save event, you should also call this when your page is first loaded in the case of a re-configuration.</span></span>
6. <span data-ttu-id="84a7f-139"> (可选) 注册事件处理程序，该事件处理程序在用户删除 `microsoftTeams.settings.registerOnRemoveHandler()` 连接器时调用。</span><span class="sxs-lookup"><span data-stu-id="84a7f-139">(Optional) Register a `microsoftTeams.settings.registerOnRemoveHandler()` event handler, which gets called when the user removes your connector.</span></span> <span data-ttu-id="84a7f-140">此事件为服务提供了执行任何清理操作的机会。</span><span class="sxs-lookup"><span data-stu-id="84a7f-140">This event gives your service an opportunity to perform any cleanup actions.</span></span>

<span data-ttu-id="84a7f-141">下面是用于创建不带 CSS 的连接器配置页的示例 HTML：</span><span class="sxs-lookup"><span data-stu-id="84a7f-141">Here's a sample HTML to create a Connector configuration page without the CSS:</span></span>

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
            alert("Removed" + JSON.stringify(removeEvent));
        });

</script>
```

#### <a name="getsettings-response-properties"></a><span data-ttu-id="84a7f-142">`GetSettings()` 响应属性</span><span class="sxs-lookup"><span data-stu-id="84a7f-142">`GetSettings()` response properties</span></span>

>[!Note]
><span data-ttu-id="84a7f-143">此处调用返回的参数与从选项卡调用此方法时不同，并且 `getSettings` 与此处记录的参数 [不同](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="84a7f-143">The parameters returned by the `getSettings` call here are different than if you were to invoke this method from a tab, and differ from those documented [here](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span>

| <span data-ttu-id="84a7f-144">参数</span><span class="sxs-lookup"><span data-stu-id="84a7f-144">Parameter</span></span>   | <span data-ttu-id="84a7f-145">详细信息</span><span class="sxs-lookup"><span data-stu-id="84a7f-145">Details</span></span> |
|-------------|---------|
| `entityId`       | <span data-ttu-id="84a7f-146">实体 ID，由代码在调用 时设置 `setSettings()` 。</span><span class="sxs-lookup"><span data-stu-id="84a7f-146">The entity ID, as set by your code when calling `setSettings()`.</span></span> |
| `configName`  | <span data-ttu-id="84a7f-147">调用 时由代码设置的配置名称 `setSettings()` 。</span><span class="sxs-lookup"><span data-stu-id="84a7f-147">The configuration name, as set by your code when calling `setSettings()`.</span></span> |
| `contentUrl` | <span data-ttu-id="84a7f-148">配置页面的 URL，由代码在调用 时设置 `setSettings()` 。</span><span class="sxs-lookup"><span data-stu-id="84a7f-148">The URL of the configuration page, as set by your code when calling `setSettings()`.</span></span> |
| `webhookUrl` | <span data-ttu-id="84a7f-149">为此连接器创建的 webhook URL。</span><span class="sxs-lookup"><span data-stu-id="84a7f-149">The webhook URL created for this connector.</span></span> <span data-ttu-id="84a7f-150">保留 webhook URL，并将其用于 POST 结构化 JSON 以将卡片发送到频道。</span><span class="sxs-lookup"><span data-stu-id="84a7f-150">Persist the webhook URL and use it to POST structured JSON to send cards to the channel.</span></span> <span data-ttu-id="84a7f-151">仅在应用程序成功返回时返回。</span><span class="sxs-lookup"><span data-stu-id="84a7f-151">The `webhookUrl` is returned only when application returns successfully.</span></span> |
| `appType` | <span data-ttu-id="84a7f-152">返回的值可以是 `mail`、`groups` 或 `teams`，分别对应 Office 365 邮件、Office 365 组或 Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="84a7f-152">The values returned can be `mail`, `groups` or `teams` corresponding to the Office 365 Mail, Office 365 Groups or Microsoft Teams respectively.</span></span> |
| `userObjectId` | <span data-ttu-id="84a7f-153">这是与启动连接器设置的 Office 365 用户对应的唯一 ID。</span><span class="sxs-lookup"><span data-stu-id="84a7f-153">This is the unique id corresponding to the Office 365 user who initiated setup of the connector.</span></span> <span data-ttu-id="84a7f-154">应该具备安全性。</span><span class="sxs-lookup"><span data-stu-id="84a7f-154">It should be secured.</span></span> <span data-ttu-id="84a7f-155">可以使用此值将 Office 365 中设置配置的用户与服务中的用户关联起来。</span><span class="sxs-lookup"><span data-stu-id="84a7f-155">This value can be used to associate the user in Office 365 who set up the configuration to the user in your service.</span></span> |

<span data-ttu-id="84a7f-156">如果需要在加载以上步骤 2 中的页面时对用户进行身份验证，请参阅此链接，详细了解在[](~/tabs/how-to/authentication/auth-flow-tab.md)嵌入页面时如何集成登录。</span><span class="sxs-lookup"><span data-stu-id="84a7f-156">If you need to authenticate the user as part of loading your page in step 2 above, refer to [this link](~/tabs/how-to/authentication/auth-flow-tab.md) for details on how you can integrate login when your page is embedded.</span></span>

> [!NOTE]
> <span data-ttu-id="84a7f-157">由于跨客户端兼容性原因，代码在调用 之前将需要使用 `microsoftTeams.authentication.registerAuthenticationHandlers()` URL 和成功/失败回调方法调用 `authenticate()` 。</span><span class="sxs-lookup"><span data-stu-id="84a7f-157">Due to cross-client compatibility reasons, your code will need to call `microsoftTeams.authentication.registerAuthenticationHandlers()` with the URL and success/failure callback methods before calling `authenticate()`.</span></span>

#### <a name="handling-edits"></a><span data-ttu-id="84a7f-158">处理编辑</span><span class="sxs-lookup"><span data-stu-id="84a7f-158">Handling edits</span></span>

<span data-ttu-id="84a7f-159">代码应处理用户返回以编辑现有连接器配置。</span><span class="sxs-lookup"><span data-stu-id="84a7f-159">Your code should handle users returning to edit an existing connector configuration.</span></span> <span data-ttu-id="84a7f-160">为此，在初始 `microsoftTeams.settings.setSettings()` 配置期间调用以下参数：</span><span class="sxs-lookup"><span data-stu-id="84a7f-160">To do this, call `microsoftTeams.settings.setSettings()` during the initial configuration with the following parameters:</span></span>

- <span data-ttu-id="84a7f-161">`entityId` 是服务可以理解的自定义 ID，表示用户配置了哪些项。</span><span class="sxs-lookup"><span data-stu-id="84a7f-161">`entityId` is the custom ID that is understood by your service and represents what the user has configured.</span></span>
- <span data-ttu-id="84a7f-162">`configName` 是配置代码可以检索的友好名称</span><span class="sxs-lookup"><span data-stu-id="84a7f-162">`configName` is a friendly name that your configuration code can retrieve</span></span>
- <span data-ttu-id="84a7f-163">`contentUrl` 是用户编辑现有连接器配置时加载的自定义 URL。</span><span class="sxs-lookup"><span data-stu-id="84a7f-163">`contentUrl` is a custom URL that gets loaded when a user edits an existing connector configuration.</span></span> <span data-ttu-id="84a7f-164">您可以使用此 URL 更轻松地让代码处理编辑案例。</span><span class="sxs-lookup"><span data-stu-id="84a7f-164">You can use this URL to make it easier for your code to handle the edit case.</span></span>

<span data-ttu-id="84a7f-165">通常，此调用作为保存事件处理程序的一部分进行。</span><span class="sxs-lookup"><span data-stu-id="84a7f-165">Typically, this call is made as part of your save event handler.</span></span> <span data-ttu-id="84a7f-166">然后，当 `contentUrl` 加载上述内容时，代码应调用 `getSettings()` 以预填充配置 UI 中的任何设置或表单。</span><span class="sxs-lookup"><span data-stu-id="84a7f-166">Then, when the `contentUrl` above is loaded, your code should call `getSettings()` to prepopulate any settings or forms in your configuration UI.</span></span>

#### <a name="handling-removals"></a><span data-ttu-id="84a7f-167">处理删除</span><span class="sxs-lookup"><span data-stu-id="84a7f-167">Handling removals</span></span>

<span data-ttu-id="84a7f-168">可以选择在用户删除现有连接器配置时执行事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="84a7f-168">You can optionally execute an event handler when the user removes an existing connector configuration.</span></span> <span data-ttu-id="84a7f-169">通过调用 注册此处理程序 `microsoftTeams.settings.registerOnRemoveHandler()` 。</span><span class="sxs-lookup"><span data-stu-id="84a7f-169">You register this handler by calling `microsoftTeams.settings.registerOnRemoveHandler()`.</span></span> <span data-ttu-id="84a7f-170">此处理程序可用于执行清理操作，例如从数据库中删除条目。</span><span class="sxs-lookup"><span data-stu-id="84a7f-170">This handler can be used to perform cleanup operations such as removing entries from a database.</span></span>

### <a name="including-the-connector-in-your-manifest"></a><span data-ttu-id="84a7f-171">在清单中包括连接器</span><span class="sxs-lookup"><span data-stu-id="84a7f-171">Including the Connector in your Manifest</span></span>

<span data-ttu-id="84a7f-172">你可以从门户下载自动生成Teams应用程序清单。</span><span class="sxs-lookup"><span data-stu-id="84a7f-172">You can download the auto-generated Teams app manifest from the portal.</span></span> <span data-ttu-id="84a7f-173">但是，在使用它测试或发布应用之前，必须执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="84a7f-173">Before you can use it to test or publish your app, though, you must do the following:</span></span>

- <span data-ttu-id="84a7f-174">[包括两个图标](../../concepts/build-and-test/apps-package.md#app-icons)。</span><span class="sxs-lookup"><span data-stu-id="84a7f-174">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
- <span data-ttu-id="84a7f-175">修改清单的 `icons` 部分，以便引用图标的文件名，而不是 URL。</span><span class="sxs-lookup"><span data-stu-id="84a7f-175">Modify the `icons` portion of the manifest to refer to the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="84a7f-176">以下 manifest.json 文件包含测试和提交应用程序所需的基本元素。</span><span class="sxs-lookup"><span data-stu-id="84a7f-176">The following manifest.json file contains the basic elements needed to test and submit your app.</span></span>

> [!NOTE]
> <span data-ttu-id="84a7f-177">将以下示例中的 `id` 和 `connectorId` 替换为连接器的 GUID。</span><span class="sxs-lookup"><span data-stu-id="84a7f-177">Replace `id` and `connectorId` in the following example with the GUID of your Connector.</span></span>

#### <a name="example-manifestjson-with-connector"></a><span data-ttu-id="84a7f-178">带连接器的示例 manifest.json</span><span class="sxs-lookup"><span data-stu-id="84a7f-178">Example manifest.json with Connector</span></span>

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

## <a name="disable-or-enable-connectors-in-teams"></a><span data-ttu-id="84a7f-179">禁用或启用 Teams</span><span class="sxs-lookup"><span data-stu-id="84a7f-179">Disable or enable connectors in Teams</span></span>

<span data-ttu-id="84a7f-180">Exchange Online PowerShell V2 模块使用新式验证，并且与 MFA (MFA) 一起用于连接到 Microsoft 365 中所有与 Exchange 相关的 PowerShell 环境。</span><span class="sxs-lookup"><span data-stu-id="84a7f-180">The Exchange Online PowerShell V2 module uses modern authentication and works with multi-factor authentication (MFA) for connecting to all Exchange-related PowerShell environments in Microsoft 365.</span></span> <span data-ttu-id="84a7f-181">管理员可以使用 Exchange Online PowerShell 禁用整个租户或特定组邮箱的连接器，从而影响该租户或邮箱中的所有用户。</span><span class="sxs-lookup"><span data-stu-id="84a7f-181">Admins can use Exchange Online PowerShell to disable connectors for an entire tenant or a specific group mailbox, affecting all users in that tenant or mailbox.</span></span> <span data-ttu-id="84a7f-182">无法对部分（而非其他）禁用。</span><span class="sxs-lookup"><span data-stu-id="84a7f-182">It is not possible to disable for some and not others.</span></span> <span data-ttu-id="84a7f-183">此外，默认情况下会为租户禁用GCC连接器。</span><span class="sxs-lookup"><span data-stu-id="84a7f-183">Also, connectors are disabled by default for GCC tenants.</span></span>

<span data-ttu-id="84a7f-184">租户级别设置会覆盖组级别设置。</span><span class="sxs-lookup"><span data-stu-id="84a7f-184">The tenant-level setting overrides the group-level setting.</span></span> <span data-ttu-id="84a7f-185">例如，如果管理员为组启用连接器，并禁用租户上的连接器，则组连接器将被禁用。</span><span class="sxs-lookup"><span data-stu-id="84a7f-185">For example, if an admin enables connectors for the group and disables them on the tenant, connectors for the group will be disabled.</span></span> <span data-ttu-id="84a7f-186">若要在 Teams中启用连接器，Exchange Online带或不带 MFA 的新式验证连接到[PowerShell。](/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="84a7f-186">To enable a connector in Teams, [connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true) using modern authentication with or without MFA.</span></span>

### <a name="commands-to-disable-or-enable-connectors"></a><span data-ttu-id="84a7f-187">禁用或启用连接器的命令</span><span class="sxs-lookup"><span data-stu-id="84a7f-187">Commands to disable or enable connectors</span></span>

<span data-ttu-id="84a7f-188">**在 PowerShell 中Exchange Online命令**</span><span class="sxs-lookup"><span data-stu-id="84a7f-188">**Run the command in Exchange Online PowerShell**</span></span>

* <span data-ttu-id="84a7f-189">若要禁用租户的连接器 `Set-OrganizationConfig -ConnectorsEnabled:$false` ：。</span><span class="sxs-lookup"><span data-stu-id="84a7f-189">To disable connectors for the tenant: `Set-OrganizationConfig -ConnectorsEnabled:$false`.</span></span>
* <span data-ttu-id="84a7f-190">若要禁用租户的可操作邮件 `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false` ：。</span><span class="sxs-lookup"><span data-stu-id="84a7f-190">To disable actionable messages for the tenant: `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false`.</span></span>
* <span data-ttu-id="84a7f-191">若要为连接器启用Teams，请运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="84a7f-191">To enable connectors for Teams, run the following commands:</span></span>
    * `Set-OrganizationConfig -ConnectorsEnabled:$true `
    * `Set-OrganizationConfig -ConnectorsEnabledForTeams:$true`
    * `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$true`

<span data-ttu-id="84a7f-192">有关 PowerShell 模块交换功能详细信息，请参阅[Set-OrganizationConfig。](/powershell/module/exchange/Set-OrganizationConfig?view=exchange-ps&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="84a7f-192">For more information on PowerShell module exchange, see [Set-OrganizationConfig](/powershell/module/exchange/Set-OrganizationConfig?view=exchange-ps&preserve-view=true).</span></span> <span data-ttu-id="84a7f-193">若要启用或禁用Outlook连接器，[请将应用连接到](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab?ui=en-us&rs=en-us&ad=us)Outlook。</span><span class="sxs-lookup"><span data-stu-id="84a7f-193">To enable or disable Outlook connectors, [connect apps to your groups in Outlook](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab?ui=en-us&rs=en-us&ad=us).</span></span>

## <a name="testing-your-connector"></a><span data-ttu-id="84a7f-194">测试连接器</span><span class="sxs-lookup"><span data-stu-id="84a7f-194">Testing your Connector</span></span>

<span data-ttu-id="84a7f-195">若要测试连接器，请将其上传到团队中，就像使用任何其他应用程序一样。</span><span class="sxs-lookup"><span data-stu-id="84a7f-195">To test your Connector, upload it to a team as you would with any other app.</span></span> <span data-ttu-id="84a7f-196">可使用连接器开发人员仪表板中的清单文件（按照上一部分的说明进行修改）和两个图标文件来创建 .zip 包。</span><span class="sxs-lookup"><span data-stu-id="84a7f-196">You can create a .zip package using the manifest file from the Connectors Developer Dashboard (modified as directed in the preceding section) and the two icon files.</span></span>

<span data-ttu-id="84a7f-197">上传应用程序后，从任意频道打开连接器列表。</span><span class="sxs-lookup"><span data-stu-id="84a7f-197">After you upload the app, open the Connectors list from any channel.</span></span> <span data-ttu-id="84a7f-198">向下滚动到底部，查看 **“上传”** 部分中的应用程序。</span><span class="sxs-lookup"><span data-stu-id="84a7f-198">Scroll to the bottom to see your app in the **Uploaded** section.</span></span>

![“连接器”对话框中上传部分的屏幕截图](~/assets/images/connectors/connector_dialog_uploaded.png)

<span data-ttu-id="84a7f-200">现在可启动配置体验。</span><span class="sxs-lookup"><span data-stu-id="84a7f-200">You can now launch the configuration experience.</span></span> <span data-ttu-id="84a7f-201">请注意，此流完全作为托管体验Microsoft Teams内部发生。</span><span class="sxs-lookup"><span data-stu-id="84a7f-201">Be aware that this flow occurs entirely within Microsoft Teams as a hosted experience.</span></span>

<span data-ttu-id="84a7f-202">若要验证操作 `HttpPOST` 是否正常工作， [请将邮件发送到连接器](~/webhooks-and-connectors/how-to/connectors-using.md)。</span><span class="sxs-lookup"><span data-stu-id="84a7f-202">To verify that an `HttpPOST` action is working correctly, [send messages to your connector](~/webhooks-and-connectors/how-to/connectors-using.md).</span></span>

## <a name="publish-connectors-for-your-organization"></a><span data-ttu-id="84a7f-203">发布组织的连接器</span><span class="sxs-lookup"><span data-stu-id="84a7f-203">Publish Connectors for your organization</span></span>

<span data-ttu-id="84a7f-204">有时，你可能不希望将连接器应用发布到公共 AppSource/Store，但希望该应用仅对贵组织的用户可用。</span><span class="sxs-lookup"><span data-stu-id="84a7f-204">Sometimes, you may not want to publish your connector app to the public AppSource/Store but would like it to be available only to the users in your organization.</span></span> <span data-ttu-id="84a7f-205">在这种情况下，您可以将自定义连接器应用程序上载到[组织的"应用程序目录"。](~/concepts/deploy-and-publish/apps-publish.md)</span><span class="sxs-lookup"><span data-stu-id="84a7f-205">In such cases, you can upload your custom connector app to your [organization's App Catalog](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="84a7f-206">这样，连接器应用将仅适用于该组织，并且无需将连接器发布到公共应用商店。</span><span class="sxs-lookup"><span data-stu-id="84a7f-206">This way, your connector app will be available only to that organization, and you will not need to publish your connector to the public store.</span></span>

<span data-ttu-id="84a7f-207">上传应用包后，若要在团队中配置和使用连接器，可以按照以下步骤从组织的应用程序目录中安装：</span><span class="sxs-lookup"><span data-stu-id="84a7f-207">Once you've uploaded your app package, to configure and use the connector in a Team it can be installed from the organization's app catalog by following these steps:</span></span>

1. <span data-ttu-id="84a7f-208">从最左侧垂直导航栏中选择应用图标。</span><span class="sxs-lookup"><span data-stu-id="84a7f-208">Select the apps icon from the far left vertical navigation bar.</span></span>
1. <span data-ttu-id="84a7f-209">在"**应用"** 窗口中，选择 **"连接器"。**</span><span class="sxs-lookup"><span data-stu-id="84a7f-209">In the **Apps** window select **Connectors**.</span></span>
1. <span data-ttu-id="84a7f-210">选择要添加的连接器，将显示一个弹出对话框窗口。</span><span class="sxs-lookup"><span data-stu-id="84a7f-210">Select the connector that you want to add and a pop-up dialog window will display.</span></span>
1. <span data-ttu-id="84a7f-211">选择" **添加到团队"** 栏。</span><span class="sxs-lookup"><span data-stu-id="84a7f-211">Select the **Add to a team** bar.</span></span>
1. <span data-ttu-id="84a7f-212">在下一个对话框窗口中，键入团队或频道名称。</span><span class="sxs-lookup"><span data-stu-id="84a7f-212">In the next dialog window type a team or channel name.</span></span>
1. <span data-ttu-id="84a7f-213">从 **对话框窗口右下角** 选择"设置连接线栏"。</span><span class="sxs-lookup"><span data-stu-id="84a7f-213">Select the **Set up a connector** bar from the bottom right corner of dialog window.</span></span>
1. <span data-ttu-id="84a7f-214">该连接器将在该团队的" &#9679;&#9679;&#9679; ">""更多选项""连接器""所有连接器"  =>    =>    =>  部分中提供。</span><span class="sxs-lookup"><span data-stu-id="84a7f-214">The connector will be available in the  section &#9679;&#9679;&#9679; => *More options* => *Connectors* => *All* => *Connectors for you team* for that team.</span></span> <span data-ttu-id="84a7f-215">可以通过滚动到此部分或搜索连接器应用来导航。</span><span class="sxs-lookup"><span data-stu-id="84a7f-215">You can navigate by scrolling to this section or search for the connector app.</span></span>
1. <span data-ttu-id="84a7f-216">若要配置或修改连接器，请选择"配置 **"** 栏。</span><span class="sxs-lookup"><span data-stu-id="84a7f-216">To configure or modify the connector select the **Configure** bar.</span></span>

## <a name="code-sample"></a><span data-ttu-id="84a7f-217">代码示例</span><span class="sxs-lookup"><span data-stu-id="84a7f-217">Code sample</span></span>
|<span data-ttu-id="84a7f-218">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="84a7f-218">**Sample name**</span></span> | <span data-ttu-id="84a7f-219">**说明**</span><span class="sxs-lookup"><span data-stu-id="84a7f-219">**Description**</span></span> | <span data-ttu-id="84a7f-220">**.NET**</span><span class="sxs-lookup"><span data-stu-id="84a7f-220">**.NET**</span></span> | <span data-ttu-id="84a7f-221">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="84a7f-221">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="84a7f-222">连接器</span><span class="sxs-lookup"><span data-stu-id="84a7f-222">Connectors</span></span>    | <span data-ttu-id="84a7f-223">示例Office 365向团队频道生成通知的连接器。</span><span class="sxs-lookup"><span data-stu-id="84a7f-223">Sample Office 365 Connector generating notifications to teams channel.</span></span>|   [<span data-ttu-id="84a7f-224">View</span><span class="sxs-lookup"><span data-stu-id="84a7f-224">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [<span data-ttu-id="84a7f-225">View</span><span class="sxs-lookup"><span data-stu-id="84a7f-225">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| <span data-ttu-id="84a7f-226">通用连接器示例</span><span class="sxs-lookup"><span data-stu-id="84a7f-226">Generic connectors sample</span></span> |<span data-ttu-id="84a7f-227">易于为支持 Webhook 的任何系统自定义的通用连接器的示例代码。</span><span class="sxs-lookup"><span data-stu-id="84a7f-227">Sample code for a generic connector that's easy to customize for any system which supports webhooks.</span></span>|  | [<span data-ttu-id="84a7f-228">View</span><span class="sxs-lookup"><span data-stu-id="84a7f-228">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|
