---
title: 创建 Office 365 连接器
author: laujan
description: 介绍如何开始使用 Office 365 中的连接器Microsoft Teams
keywords: Teams o365 连接器
localization_priority: Normal
ms.topic: conceptual
ms.date: 06/16/2021
ms.openlocfilehash: 28a2b35e868baf34e35a11a00e10b30b0f09c236
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179753"
---
# <a name="create-office-365-connectors"></a><span data-ttu-id="19421-104">创建 Office 365 连接器</span><span class="sxs-lookup"><span data-stu-id="19421-104">Create Office 365 Connectors</span></span>

<span data-ttu-id="19421-105">借助Microsoft Teams，你可以添加现有 Office 365 连接器，或在 Teams 中生成一个新的连接器。</span><span class="sxs-lookup"><span data-stu-id="19421-105">With Microsoft Teams apps, you can add your existing Office 365 Connector or build a new one within Teams.</span></span> <span data-ttu-id="19421-106">有关详细信息，请参阅构建 [你自己的连接器](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector)。</span><span class="sxs-lookup"><span data-stu-id="19421-106">For more information, see [build your own connector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector).</span></span>

## <a name="add-a-connector-to-teams-app"></a><span data-ttu-id="19421-107">向应用添加Teams连接器</span><span class="sxs-lookup"><span data-stu-id="19421-107">Add a connector to Teams app</span></span>

<span data-ttu-id="19421-108">可以将[连接器](~/concepts/build-and-test/apps-package.md)[打包并发布](~/concepts/deploy-and-publish/apps-publish.md)为 AppSource 提交的一部分。</span><span class="sxs-lookup"><span data-stu-id="19421-108">You can [package](~/concepts/build-and-test/apps-package.md) and [publish](~/concepts/deploy-and-publish/apps-publish.md) your connector as part of your AppSource submission.</span></span> <span data-ttu-id="19421-109">你可以将注册的连接器作为应用包的一Teams分发。</span><span class="sxs-lookup"><span data-stu-id="19421-109">You can distribute your registered connector as part of your Teams app package.</span></span> <span data-ttu-id="19421-110">有关应用入口点Teams，请参阅[功能](~/concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="19421-110">For information on entry points for Teams app, see [capabilities](~/concepts/extensibility-points.md).</span></span> <span data-ttu-id="19421-111">还可以直接向用户提供程序包，以在 Teams。</span><span class="sxs-lookup"><span data-stu-id="19421-111">You can also provide the package to users directly for uploading within Teams.</span></span>

<span data-ttu-id="19421-112">若要分发连接器，必须通过连接器开发人员仪表板 [进行注册](https://outlook.office.com/connectors/home/login/#/publish)。</span><span class="sxs-lookup"><span data-stu-id="19421-112">To distribute your connector, you must register through [Connectors Developer Dashboard](https://outlook.office.com/connectors/home/login/#/publish).</span></span> <span data-ttu-id="19421-113">注册连接器时，假定它适用于支持应用程序的Office 365产品，包括 Outlook 和 Teams。</span><span class="sxs-lookup"><span data-stu-id="19421-113">When a connector is registered, it is assumed that it works in all Office 365 products that support applications, including Outlook and Teams.</span></span> <span data-ttu-id="19421-114">如果不是这种情况，并且你必须创建仅在 Microsoft Teams 中工作的连接器，请联系：Microsoft Teams[应用提交电子邮件](mailto:teamsubm@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="19421-114">If that is not the case and you must create a connector that only works in Microsoft Teams, contact: [Microsoft Teams App Submissions email](mailto:teamsubm@microsoft.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19421-115">连接器在连接器开发人员 **仪表板中选择"** 保存"后注册。</span><span class="sxs-lookup"><span data-stu-id="19421-115">Your connector is registered after you select **Save** in the Connectors Developer Dashboard.</span></span> <span data-ttu-id="19421-116">如果你想要在 AppSource 中发布连接器，请按照将应用发布到[AppSource Microsoft Teams中的说明操作](~/concepts/deploy-and-publish/apps-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="19421-116">If you want to publish your connector in AppSource, follow the instructions in [publish your Microsoft Teams app to AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="19421-117">如果不想在 AppSource 中发布应用，请将其直接分发到组织。</span><span class="sxs-lookup"><span data-stu-id="19421-117">If you do not want to publish your app in AppSource, distribute it directly to the organization.</span></span> <span data-ttu-id="19421-118">为 [组织发布连接器后](#publish-connectors-for-the-organization)，无需在连接器仪表板上执行其他操作。</span><span class="sxs-lookup"><span data-stu-id="19421-118">After [publishing connectors for your organization](#publish-connectors-for-the-organization), no further action is required on the Connector Dashboard.</span></span>

### <a name="integrate-the-configuration-experience"></a><span data-ttu-id="19421-119">集成配置体验</span><span class="sxs-lookup"><span data-stu-id="19421-119">Integrate the configuration experience</span></span>

<span data-ttu-id="19421-120">用户可以完成整个连接器配置体验，而无需离开 Teams 客户端。</span><span class="sxs-lookup"><span data-stu-id="19421-120">Users can complete the entire connector configuration experience without having to leave the Teams client.</span></span> <span data-ttu-id="19421-121">若要获取体验，Teams直接在 iframe 中嵌入配置页面。</span><span class="sxs-lookup"><span data-stu-id="19421-121">To get the experience, Teams can embed your configuration page directly within an iframe.</span></span> <span data-ttu-id="19421-122">操作顺序如下所示：</span><span class="sxs-lookup"><span data-stu-id="19421-122">The sequence of operations is as follows:</span></span>

1. <span data-ttu-id="19421-123">用户选择连接器以开始配置过程。</span><span class="sxs-lookup"><span data-stu-id="19421-123">The user selects the connector to begin the configuration process.</span></span>
1. <span data-ttu-id="19421-124">用户与 Web 体验交互以完成配置。</span><span class="sxs-lookup"><span data-stu-id="19421-124">The user interacts with the web experience to complete the configuration.</span></span>
1. <span data-ttu-id="19421-125">用户选择" **保存"，** 这将在代码中触发回调。</span><span class="sxs-lookup"><span data-stu-id="19421-125">The user selects **Save**, which triggers a callback in code.</span></span>

    > [!NOTE]
    > * <span data-ttu-id="19421-126">代码可以通过检索 webhook 设置处理保存事件。</span><span class="sxs-lookup"><span data-stu-id="19421-126">The code can process the save event by retrieving the webhook settings.</span></span> <span data-ttu-id="19421-127">代码存储 Webhook 以稍后发布事件。</span><span class="sxs-lookup"><span data-stu-id="19421-127">Your code stores the webhook to post events later.</span></span>
    > * <span data-ttu-id="19421-128">配置体验在 Teams 内内加载。</span><span class="sxs-lookup"><span data-stu-id="19421-128">The configuration experience is loaded inline within Teams.</span></span>

<span data-ttu-id="19421-129">可以重用现有 Web 配置体验，或创建一个单独的版本以专门托管在 Teams。</span><span class="sxs-lookup"><span data-stu-id="19421-129">You can reuse your existing web configuration experience or create a separate version to be hosted specifically in Teams.</span></span> <span data-ttu-id="19421-130">您的代码必须包含 Microsoft Teams Sdk。</span><span class="sxs-lookup"><span data-stu-id="19421-130">Your code must include the Microsoft Teams JavaScript SDK.</span></span> <span data-ttu-id="19421-131">这样，代码可以访问 API 来执行常见操作，如获取当前用户、频道或团队上下文以及启动身份验证流程。</span><span class="sxs-lookup"><span data-stu-id="19421-131">This gives your code access to APIs to perform common operations, such as getting the current user, channel, or team context and initiate authentication flows.</span></span>

<span data-ttu-id="19421-132">**集成配置体验**</span><span class="sxs-lookup"><span data-stu-id="19421-132">**To integrate the configuration experience**</span></span>

1. <span data-ttu-id="19421-133">通过调用`microsoftTeams.initialize()`初始化 SDK。</span><span class="sxs-lookup"><span data-stu-id="19421-133">Initialize the SDK by calling `microsoftTeams.initialize()`.</span></span>
1. <span data-ttu-id="19421-134">调用 `microsoftTeams.settings.setValidityState(true)` 以启用 **Save**。</span><span class="sxs-lookup"><span data-stu-id="19421-134">Call `microsoftTeams.settings.setValidityState(true)` to enable **Save**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="19421-135">您必须调用 `microsoftTeams.settings.setValidityState(true)` 作为用户选择或字段更新的响应。</span><span class="sxs-lookup"><span data-stu-id="19421-135">You must call `microsoftTeams.settings.setValidityState(true)` as a response to user selection or field update.</span></span>

1. <span data-ttu-id="19421-136">注册 `microsoftTeams.settings.registerOnSaveHandler()` 事件处理程序，在用户选择"保存"时 **调用。**</span><span class="sxs-lookup"><span data-stu-id="19421-136">Register  `microsoftTeams.settings.registerOnSaveHandler()` event handler, which is called when the user selects **Save**.</span></span>
1. <span data-ttu-id="19421-137">调用 `microsoftTeams.settings.setSettings()` 以保存连接器设置。</span><span class="sxs-lookup"><span data-stu-id="19421-137">Call `microsoftTeams.settings.setSettings()` to save the connector settings.</span></span> <span data-ttu-id="19421-138">如果用户尝试更新连接器的现有配置，则配置对话框中也会显示保存的设置。</span><span class="sxs-lookup"><span data-stu-id="19421-138">The saved settings are also shown in the configuration dialog if the user tries to update an existing configuration for your connector.</span></span>
1. <span data-ttu-id="19421-139">调用 `microsoftTeams.settings.getSettings()` 以提取 webhook 属性，包括 URL。</span><span class="sxs-lookup"><span data-stu-id="19421-139">Call `microsoftTeams.settings.getSettings()` to fetch webhook properties, including the URL.</span></span>

    > [!NOTE]
    > <span data-ttu-id="19421-140">首次加载 `microsoftTeams.settings.getSettings()` 页面时必须调用 ，以防重新配置。</span><span class="sxs-lookup"><span data-stu-id="19421-140">You must call `microsoftTeams.settings.getSettings()` when your page is first loaded in case of reconfiguration.</span></span>

1. <span data-ttu-id="19421-141">注册 `microsoftTeams.settings.registerOnRemoveHandler()` 事件处理程序，在用户删除连接器时调用该处理程序。</span><span class="sxs-lookup"><span data-stu-id="19421-141">Register `microsoftTeams.settings.registerOnRemoveHandler()` event handler, which is called when the user removes connector.</span></span>

<span data-ttu-id="19421-142">此事件为服务提供了执行任何清理操作的机会。</span><span class="sxs-lookup"><span data-stu-id="19421-142">This event gives your service an opportunity to perform any cleanup actions.</span></span>

<span data-ttu-id="19421-143">以下代码提供了一个示例 HTML，用于创建没有客户服务和支持的连接器配置页：</span><span class="sxs-lookup"><span data-stu-id="19421-143">The following code provides a sample HTML to create a connector configuration page without the customer service and support:</span></span>

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

<span data-ttu-id="19421-144">若要在加载页面时对用户进行身份验证，请参阅在嵌入页面[](~/tabs/how-to/authentication/auth-flow-tab.md)时集成登录的选项卡的身份验证流。</span><span class="sxs-lookup"><span data-stu-id="19421-144">To authenticate the user as part of loading your page, see [authentication flow for tabs](~/tabs/how-to/authentication/auth-flow-tab.md) to integrate sign in when your page is embedded.</span></span>

> [!NOTE]
> <span data-ttu-id="19421-145">由于跨客户端兼容性原因，代码在调用 之前必须使用 URL 和 `microsoftTeams.authentication.registerAuthenticationHandlers()` 成功或失败回调方法调用 `authenticate()` 。</span><span class="sxs-lookup"><span data-stu-id="19421-145">Due to cross client compatibility reasons, your code must call `microsoftTeams.authentication.registerAuthenticationHandlers()` with the URL and success or failure callback methods before calling `authenticate()`.</span></span>

#### <a name="getsettings-response-properties"></a><span data-ttu-id="19421-146">`GetSettings` 响应属性</span><span class="sxs-lookup"><span data-stu-id="19421-146">`GetSettings` response properties</span></span>

>[!NOTE]
><span data-ttu-id="19421-147">从选项卡调用此方法时，调用返回的参数是不同的，并且不同于 js 设置中 `getSettings` 记录 [的参数](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="19421-147">The parameters returned by the `getSettings` call are different when you invoke this method from a tab and differ from those documented in [js settings](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span>

<span data-ttu-id="19421-148">下表提供了参数和响应属性 `GetSetting` 的详细信息：</span><span class="sxs-lookup"><span data-stu-id="19421-148">The following table provides the parameters and the details of `GetSetting` response properties:</span></span>

| <span data-ttu-id="19421-149">参数</span><span class="sxs-lookup"><span data-stu-id="19421-149">Parameters</span></span>   | <span data-ttu-id="19421-150">详细信息</span><span class="sxs-lookup"><span data-stu-id="19421-150">Details</span></span> |
|-------------|---------|
| `entityId`       | <span data-ttu-id="19421-151">实体 ID，由代码在调用 时设置 `setSettings()` 。</span><span class="sxs-lookup"><span data-stu-id="19421-151">The entity ID, as set by your code when calling `setSettings()`.</span></span> |
| `configName`  | <span data-ttu-id="19421-152">调用 时由代码设置的配置名称 `setSettings()` 。</span><span class="sxs-lookup"><span data-stu-id="19421-152">The configuration name, as set by your code when calling `setSettings()`.</span></span> |
| `contentUrl` | <span data-ttu-id="19421-153">配置页面的 URL，由代码在调用 时设置 `setSettings()` 。</span><span class="sxs-lookup"><span data-stu-id="19421-153">The URL of the configuration page, as set by your code when calling `setSettings()`.</span></span> |
| `webhookUrl` | <span data-ttu-id="19421-154">为连接器创建的 webhook URL。</span><span class="sxs-lookup"><span data-stu-id="19421-154">The webhook URL created for the connector.</span></span> <span data-ttu-id="19421-155">使用 POST 结构化 JSON 的 webhook URL 将卡片发送到频道。</span><span class="sxs-lookup"><span data-stu-id="19421-155">Use the webhook URL to POST structured JSON to send cards to the channel.</span></span> <span data-ttu-id="19421-156">`webhookUrl`仅在应用程序成功返回数据时返回 。</span><span class="sxs-lookup"><span data-stu-id="19421-156">The `webhookUrl` is returned only when the application returns data successfully.</span></span> |
| `appType` | <span data-ttu-id="19421-157">返回的值可以是 、 `mail` 或 `groups` 分别对应于邮件Office 365组Office 365组Microsoft Teams `teams` 组。</span><span class="sxs-lookup"><span data-stu-id="19421-157">The values returned can be `mail`, `groups`, or `teams` corresponding to the Office 365 Mail, Office 365 Groups, or Microsoft Teams respectively.</span></span> |
| `userObjectId` | <span data-ttu-id="19421-158">与启动连接器Office 365的用户对应的唯一 ID。</span><span class="sxs-lookup"><span data-stu-id="19421-158">The unique ID corresponding to the Office 365 user who initiated the set up of the connector.</span></span> <span data-ttu-id="19421-159">它必须是安全的。</span><span class="sxs-lookup"><span data-stu-id="19421-159">It must be secured.</span></span> <span data-ttu-id="19421-160">此值可用于关联服务中Office 365，该用户已在你的服务中设置配置。</span><span class="sxs-lookup"><span data-stu-id="19421-160">This value can be used to associate the user in Office 365, who has set up the configuration in your service.</span></span> |

#### <a name="handle-edits"></a><span data-ttu-id="19421-161">处理编辑</span><span class="sxs-lookup"><span data-stu-id="19421-161">Handle edits</span></span>

<span data-ttu-id="19421-162">您的代码必须处理返回以编辑现有连接器配置的用户。</span><span class="sxs-lookup"><span data-stu-id="19421-162">Your code must handle users who return to edit an existing connector configuration.</span></span> <span data-ttu-id="19421-163">为此，在初始 `microsoftTeams.settings.setSettings()` 配置期间调用以下参数：</span><span class="sxs-lookup"><span data-stu-id="19421-163">To do this, call `microsoftTeams.settings.setSettings()` during the initial configuration with the following parameters:</span></span>

- <span data-ttu-id="19421-164">`entityId` 是表示用户已配置和您的服务理解的自定义 ID。</span><span class="sxs-lookup"><span data-stu-id="19421-164">`entityId` is the custom ID that represents what the user has configured and understood by your service.</span></span>
- <span data-ttu-id="19421-165">`configName` 是配置代码可以检索的名称。</span><span class="sxs-lookup"><span data-stu-id="19421-165">`configName` is a name that configuration code can retrieve.</span></span>
- <span data-ttu-id="19421-166">`contentUrl` 是用户编辑现有连接器配置时加载的自定义 URL。</span><span class="sxs-lookup"><span data-stu-id="19421-166">`contentUrl` is a custom URL that gets loaded when a user edits an existing connector configuration.</span></span>

<span data-ttu-id="19421-167">此调用作为保存事件处理程序的一部分进行。</span><span class="sxs-lookup"><span data-stu-id="19421-167">This call is made as part of your save event handler.</span></span> <span data-ttu-id="19421-168">然后， `contentUrl` 在加载 时，代码必须调用 以预填充配置用户界面中任何 `getSettings()` 设置或表单。</span><span class="sxs-lookup"><span data-stu-id="19421-168">Then, when the `contentUrl` is loaded, your code must call `getSettings()` to pre populate any settings or forms in your configuration user interface.</span></span>

#### <a name="handle-removals"></a><span data-ttu-id="19421-169">处理删除</span><span class="sxs-lookup"><span data-stu-id="19421-169">Handle removals</span></span>

<span data-ttu-id="19421-170">您可以在用户删除现有连接器配置时执行事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="19421-170">You can execute an event handler when the user removes an existing connector configuration.</span></span> <span data-ttu-id="19421-171">通过调用 注册此处理程序 `microsoftTeams.settings.registerOnRemoveHandler()` 。</span><span class="sxs-lookup"><span data-stu-id="19421-171">You register this handler by calling `microsoftTeams.settings.registerOnRemoveHandler()`.</span></span> <span data-ttu-id="19421-172">此处理程序用于执行清理操作，例如从数据库中删除条目。</span><span class="sxs-lookup"><span data-stu-id="19421-172">This handler is used to perform cleanup operations, such as removing entries from a database.</span></span>

### <a name="include-the-connector-in-your-manifest"></a><span data-ttu-id="19421-173">在清单中包括连接器</span><span class="sxs-lookup"><span data-stu-id="19421-173">Include the connector in your Manifest</span></span>

<span data-ttu-id="19421-174">从门户下载 `Teams app manifest` 自动生成的 。</span><span class="sxs-lookup"><span data-stu-id="19421-174">Download the auto generated `Teams app manifest` from the portal.</span></span> <span data-ttu-id="19421-175">在测试或发布应用之前，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="19421-175">Perform the following steps, before testing or publishing the app:</span></span>

1. <span data-ttu-id="19421-176">[包括两个图标](../../concepts/build-and-test/apps-package.md#app-icons)。</span><span class="sxs-lookup"><span data-stu-id="19421-176">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
1. <span data-ttu-id="19421-177">修改 `icons` 清单部分以包括图标的文件名，而不是 URL。</span><span class="sxs-lookup"><span data-stu-id="19421-177">Modify the `icons` portion of the manifest to include the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="19421-178">以下manifest.js文件包含测试和提交应用所需的元素：</span><span class="sxs-lookup"><span data-stu-id="19421-178">The following manifest.json file contains the elements needed to test and submit the app:</span></span>

> [!NOTE]
> <span data-ttu-id="19421-179">将 `id` `connectorId` 和 替换为连接器的 GUID。</span><span class="sxs-lookup"><span data-stu-id="19421-179">Replace `id` and `connectorId` in the following example with the GUID of the connector.</span></span>

#### <a name="example-of-manifestjson-with-connector"></a><span data-ttu-id="19421-180">连接器manifest.js打开的示例</span><span class="sxs-lookup"><span data-stu-id="19421-180">Example of manifest.json with connector</span></span>

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
    "full": "This is a small sample app we made for you! This app has samples of all capabilities Microsoft Teams supports.",
    "short": "This is a small sample app we made for you!"
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App"
  },
  "accentColor": "#FFFFFF",
  "needsIdentity": "true"
}
```

## <a name="enable-or-disable-connectors-in-teams"></a><span data-ttu-id="19421-181">启用或禁用 Teams</span><span class="sxs-lookup"><span data-stu-id="19421-181">Enable or disable connectors in Teams</span></span>

<span data-ttu-id="19421-182">PowerShell V2 模块Exchange Online新式验证，并适用于多重身份验证，称为 MFA，用于连接到 Exchange 中所有与 PowerShell 相关的Microsoft 365。</span><span class="sxs-lookup"><span data-stu-id="19421-182">The Exchange Online PowerShell V2 module uses modern authentication and works with multi factor authentication, called MFA for connecting to all Exchange related PowerShell environments in Microsoft 365.</span></span> <span data-ttu-id="19421-183">管理员可以使用 Exchange Online PowerShell 禁用整个租户或特定组邮箱的连接器，从而影响该租户或邮箱中的所有用户。</span><span class="sxs-lookup"><span data-stu-id="19421-183">Admins can use Exchange Online PowerShell to disable connectors for an entire tenant or a specific group mailbox, affecting all users in that tenant or mailbox.</span></span> <span data-ttu-id="19421-184">无法对部分（而非其他）禁用。</span><span class="sxs-lookup"><span data-stu-id="19421-184">It is not possible to disable for some and not others.</span></span> <span data-ttu-id="19421-185">此外，默认情况下，连接器对 政府社区云（称为 GCC 租户）禁用。</span><span class="sxs-lookup"><span data-stu-id="19421-185">Also, connectors are disabled by default for Government Community Cloud, called GCC tenants.</span></span>

<span data-ttu-id="19421-186">租户级别设置会覆盖组级别设置。</span><span class="sxs-lookup"><span data-stu-id="19421-186">The tenant level setting overrides the group level setting.</span></span> <span data-ttu-id="19421-187">例如，如果管理员为组启用连接器，并禁用租户上的连接器，则禁用该组的连接器。</span><span class="sxs-lookup"><span data-stu-id="19421-187">For example, if an admin enables connectors for the group and disables them on the tenant, connectors for the group is disabled.</span></span> <span data-ttu-id="19421-188">若要在 Teams中启用连接器，Exchange Online带或不带 MFA 的新式验证连接到[PowerShell。](/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="19421-188">To enable a connector in Teams, [connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true) using modern authentication with or without MFA.</span></span>

### <a name="commands-to-enable-or-disable-connectors"></a><span data-ttu-id="19421-189">用于启用或禁用连接器的命令</span><span class="sxs-lookup"><span data-stu-id="19421-189">Commands to enable or disable connectors</span></span>

<span data-ttu-id="19421-190">在 Exchange Online PowerShell 中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="19421-190">Run the following commands in Exchange Online PowerShell:</span></span>

* <span data-ttu-id="19421-191">若要禁用租户的连接器 `Set-OrganizationConfig -ConnectorsEnabled:$false` ：。</span><span class="sxs-lookup"><span data-stu-id="19421-191">To disable connectors for the tenant: `Set-OrganizationConfig -ConnectorsEnabled:$false`.</span></span>
* <span data-ttu-id="19421-192">若要禁用租户的可操作邮件 `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false` ：。</span><span class="sxs-lookup"><span data-stu-id="19421-192">To disable actionable messages for the tenant: `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false`.</span></span>
* <span data-ttu-id="19421-193">若要为连接器启用Teams，请运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="19421-193">To enable connectors for Teams, run the following commands:</span></span>
  * `Set-OrganizationConfig -ConnectorsEnabled:$true `
  * `Set-OrganizationConfig -ConnectorsEnabledForTeams:$true`
  * `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$true`

<span data-ttu-id="19421-194">有关 PowerShell 模块交换功能详细信息，请参阅[Set-OrganizationConfig。](/powershell/module/exchange/Set-OrganizationConfig?view=exchange-ps&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="19421-194">For more information on PowerShell module exchange, see [Set-OrganizationConfig](/powershell/module/exchange/Set-OrganizationConfig?view=exchange-ps&preserve-view=true).</span></span> <span data-ttu-id="19421-195">若要启用或禁用Outlook连接器，[请将应用连接到](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab?ui=en-us&rs=en-us&ad=us)Outlook。</span><span class="sxs-lookup"><span data-stu-id="19421-195">To enable or disable Outlook connectors, [connect apps to your groups in Outlook](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab?ui=en-us&rs=en-us&ad=us).</span></span>

## <a name="test-your-connector"></a><span data-ttu-id="19421-196">测试连接器</span><span class="sxs-lookup"><span data-stu-id="19421-196">Test your connector</span></span>

<span data-ttu-id="19421-197">若要测试连接器，请通过任何其他应用将其上载到团队。</span><span class="sxs-lookup"><span data-stu-id="19421-197">To test your connector, upload it to a team with any other app.</span></span> <span data-ttu-id="19421-198">可以使用两个.zip图标文件和连接器开发人员仪表板中的清单文件创建一个程序包，按照在清单中包括连接器中的指示 [进行修改](#include-the-connector-in-your-manifest)。</span><span class="sxs-lookup"><span data-stu-id="19421-198">You can create a .zip package using the manifest file from the two icon files and connectors Developer Dashboard, modified as directed in [Include the connector in your Manifest](#include-the-connector-in-your-manifest).</span></span>

<span data-ttu-id="19421-199">上传应用后，从任何渠道打开连接器列表。</span><span class="sxs-lookup"><span data-stu-id="19421-199">After you upload the app, open the connectors list from any channel.</span></span> <span data-ttu-id="19421-200">滚动到底部，在"已上载"部分 **查看** 你的应用：</span><span class="sxs-lookup"><span data-stu-id="19421-200">Scroll to the bottom to see your app in the **Uploaded** section:</span></span>

!["连接器"对话框中已上载节的屏幕截图](~/assets/images/connectors/connector_dialog_uploaded.png)

> [!NOTE]
> <span data-ttu-id="19421-202">流完全在托管体验Microsoft Teams内部发生。</span><span class="sxs-lookup"><span data-stu-id="19421-202">The flow occurs entirely within Microsoft Teams as a hosted experience.</span></span>

<span data-ttu-id="19421-203">若要验证 `HttpPOST` 操作是否正常工作， [请将邮件发送到连接器](~/webhooks-and-connectors/how-to/connectors-using.md)。</span><span class="sxs-lookup"><span data-stu-id="19421-203">To verify that `HttpPOST` action is working correctly, [send messages to your connector](~/webhooks-and-connectors/how-to/connectors-using.md).</span></span>

## <a name="publish-connectors-for-the-organization"></a><span data-ttu-id="19421-204">发布组织的连接器</span><span class="sxs-lookup"><span data-stu-id="19421-204">Publish connectors for the organization</span></span>

<span data-ttu-id="19421-205">如果希望连接器仅对贵组织的用户可用，可以将自定义连接器应用程序上载到 [组织的应用程序目录](~/concepts/deploy-and-publish/apps-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="19421-205">If you want the connector to be available only to the users in your organization, you can upload your custom connector app to your [organization's app catalog](~/concepts/deploy-and-publish/apps-publish.md).</span></span>

<span data-ttu-id="19421-206">上载应用包以在团队中配置和使用连接器后，从组织的应用程序目录中安装连接器。</span><span class="sxs-lookup"><span data-stu-id="19421-206">After uploading the app package to configure and use the connector in a team, install the connector from the organization's app catalog.</span></span>

<span data-ttu-id="19421-207">**设置连接器**</span><span class="sxs-lookup"><span data-stu-id="19421-207">**To set up a connector**</span></span>

1. <span data-ttu-id="19421-208">从 **左侧** 导航栏中选择"应用"。</span><span class="sxs-lookup"><span data-stu-id="19421-208">Select **Apps** from the left navigation bar.</span></span>
1. <span data-ttu-id="19421-209">在"**应用"** 部分，选择"**连接器"。**</span><span class="sxs-lookup"><span data-stu-id="19421-209">In the **Apps** section, select **Connectors**.</span></span>
1. <span data-ttu-id="19421-210">选择要添加的连接器。</span><span class="sxs-lookup"><span data-stu-id="19421-210">Select the connector that you want to add.</span></span> <span data-ttu-id="19421-211">将出现一个弹出对话框窗口。</span><span class="sxs-lookup"><span data-stu-id="19421-211">A pop up dialog window appears.</span></span>
1. <span data-ttu-id="19421-212">从下拉菜单中，选择"**添加到团队"。**</span><span class="sxs-lookup"><span data-stu-id="19421-212">From the dropdown menu, select **Add to a team**.</span></span>
1. <span data-ttu-id="19421-213">在搜索框中，键入团队或频道名称。</span><span class="sxs-lookup"><span data-stu-id="19421-213">In the search box, type a team or channel name.</span></span>
1. <span data-ttu-id="19421-214">从 **对话框窗口** 右下角的下拉菜单中选择"设置连接器"。</span><span class="sxs-lookup"><span data-stu-id="19421-214">Select **Set up a Connector** from the dropdown menu in the bottom right corner of the dialog window.</span></span>

<span data-ttu-id="19421-215">该连接器位于该团队的 &#9679;&#9679;&#9679; > "更多 **选项**""连接器  >    >    >  **""所有** 连接器"部分中。</span><span class="sxs-lookup"><span data-stu-id="19421-215">The connector is available in the section &#9679;&#9679;&#9679; > **More options** > **Connectors** > **All** > **Connectors for your team** for that team.</span></span> <span data-ttu-id="19421-216">可以通过滚动到此部分或搜索连接器应用来导航。</span><span class="sxs-lookup"><span data-stu-id="19421-216">You can navigate by scrolling to this section or search for the connector app.</span></span> <span data-ttu-id="19421-217">若要配置或修改连接器，请选择"配置 **"。**</span><span class="sxs-lookup"><span data-stu-id="19421-217">To configure or modify the connector, select **Configure**.</span></span>

## <a name="distribute-webhook-and-connector"></a><span data-ttu-id="19421-218">分发 Webhook 和连接器</span><span class="sxs-lookup"><span data-stu-id="19421-218">Distribute webhook and connector</span></span>

1. <span data-ttu-id="19421-219">[直接为团队设置传入 Webhook。](~/webhooks-and-connectors/how-to/add-incoming-webhook.md?branch=pr-en-us-3076#create-incoming-webhook)</span><span class="sxs-lookup"><span data-stu-id="19421-219">[Set up an Incoming Webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md?branch=pr-en-us-3076#create-incoming-webhook) directly for your team.</span></span>
1. <span data-ttu-id="19421-220">添加配置[页面，](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#integrate-the-configuration-experience)在 O365 连接器中发布传入[Webhook。](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#publish-connectors-for-the-organization)</span><span class="sxs-lookup"><span data-stu-id="19421-220">Add a [configuration page](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#integrate-the-configuration-experience) and [publish your Incoming Webhook](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#publish-connectors-for-the-organization) in a O365 Connector.</span></span>
1. <span data-ttu-id="19421-221">将连接器打包并发布为 [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) 提交的一部分。</span><span class="sxs-lookup"><span data-stu-id="19421-221">Package and publish your connector as part of your [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) submission.</span></span>

## <a name="code-sample"></a><span data-ttu-id="19421-222">代码示例</span><span class="sxs-lookup"><span data-stu-id="19421-222">Code sample</span></span>

<span data-ttu-id="19421-223">下表提供了示例名称及其说明：</span><span class="sxs-lookup"><span data-stu-id="19421-223">The following table provides the sample name and its description:</span></span>

|<span data-ttu-id="19421-224">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="19421-224">**Sample name**</span></span> | <span data-ttu-id="19421-225">**Description**</span><span class="sxs-lookup"><span data-stu-id="19421-225">**Description**</span></span> | <span data-ttu-id="19421-226">**.NET**</span><span class="sxs-lookup"><span data-stu-id="19421-226">**.NET**</span></span> | <span data-ttu-id="19421-227">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="19421-227">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="19421-228">连接器</span><span class="sxs-lookup"><span data-stu-id="19421-228">Connectors</span></span>    | <span data-ttu-id="19421-229">示例Office 365将通知生成到Teams连接器。</span><span class="sxs-lookup"><span data-stu-id="19421-229">Sample Office 365 Connector generating notifications to Teams channel.</span></span>|   [<span data-ttu-id="19421-230">View</span><span class="sxs-lookup"><span data-stu-id="19421-230">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [<span data-ttu-id="19421-231">View</span><span class="sxs-lookup"><span data-stu-id="19421-231">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| <span data-ttu-id="19421-232">通用连接器示例</span><span class="sxs-lookup"><span data-stu-id="19421-232">Generic connectors sample</span></span> |<span data-ttu-id="19421-233">通用连接器的示例代码，易于为支持 Webhook 的任何系统进行自定义。</span><span class="sxs-lookup"><span data-stu-id="19421-233">Sample code for a generic connector that is easy to customize for any system that supports webhooks.</span></span>|  | [<span data-ttu-id="19421-234">View</span><span class="sxs-lookup"><span data-stu-id="19421-234">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|

## <a name="see-also"></a><span data-ttu-id="19421-235">另请参阅</span><span class="sxs-lookup"><span data-stu-id="19421-235">See also</span></span>

* [<span data-ttu-id="19421-236">创建和发送邮件</span><span class="sxs-lookup"><span data-stu-id="19421-236">Create and send messages</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)
* [<span data-ttu-id="19421-237">创建传入 Webhook</span><span class="sxs-lookup"><span data-stu-id="19421-237">Create an Incoming Webhook</span></span>](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [<span data-ttu-id="19421-238">创建 Office 365 连接器</span><span class="sxs-lookup"><span data-stu-id="19421-238">Create an Office 365 Connector</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
