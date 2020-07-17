---
title: Office 365 连接器
description: 介绍如何开始使用 Microsoft 团队中的 Office 365 连接器
keywords: Teams o365 连接器
ms.date: 04/19/2019
ms.openlocfilehash: 9c89463830d46512e622dcf4c256a867d419de83
ms.sourcegitcommit: d0ca6a4856ffd03d197d47338e633126723fa78a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2020
ms.locfileid: "45137652"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a><span data-ttu-id="5a6f6-104">为 Microsoft 团队创建 Office 365 连接器</span><span class="sxs-lookup"><span data-stu-id="5a6f6-104">Creating Office 365 Connectors for Microsoft Teams</span></span>

><span data-ttu-id="5a6f6-105">在 Microsoft 团队应用程序中，您可以添加现有的 Office 365 连接器或构建新的 Office 连接器以将其包含在 Microsoft 团队中。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-105">With Microsoft Teams apps, you can add your existing Office 365 Connector or build a new one to include in Microsoft Teams.</span></span> <span data-ttu-id="5a6f6-106">有关详细信息，请参阅[生成您自己的连接器](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector)。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-106">See [Build your own Connector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) for more information.</span></span>

## <a name="adding-a-connector-to-your-teams-app"></a><span data-ttu-id="5a6f6-107">将连接器添加到你的团队应用</span><span class="sxs-lookup"><span data-stu-id="5a6f6-107">Adding a Connector to your Teams App</span></span>

<span data-ttu-id="5a6f6-108">您可以将已注册的连接器作为团队应用程序包的一部分进行分发。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-108">You can distribute your registered Connector as part of your Teams app package.</span></span> <span data-ttu-id="5a6f6-109">无论是独立的解决方案还是你的经验在团队中启用的几项[功能](~/concepts/extensibility-points.md)之一，都可以[打包](~/concepts/build-and-test/apps-package.md)和[发布](~/concepts/deploy-and-publish/apps-publish.md)连接器作为 AppSource 提交的一部分，也可以直接将其提供给用户以在团队内上载。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-109">Whether as a standalone solution, or one of several [capabilities](~/concepts/extensibility-points.md) that your experience enables in Teams, you can [package](~/concepts/build-and-test/apps-package.md) and [publish](~/concepts/deploy-and-publish/apps-publish.md) your Connector as part of your AppSource submission, or you can provide it to users directly for uploading within Teams.</span></span>

<span data-ttu-id="5a6f6-110">若要分发连接器，您需要使用[连接器开发人员仪表板](https://outlook.office.com/connectors/home/login/#/publish)进行注册。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-110">To distribute your Connector, you need to register by using the [Connectors Developer Dashboard](https://outlook.office.com/connectors/home/login/#/publish).</span></span> <span data-ttu-id="5a6f6-111">默认情况下，注册连接器后，系统会假定您的连接器能够在所有支持它们的 Office 365 产品（包括 Outlook 和团队）中工作。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-111">By default, once a Connector is registered, it's assumed that your Connector will work in all Office 365 products that support them, including Outlook and Teams.</span></span> <span data-ttu-id="5a6f6-112">如果_不_是这种情况，并且需要创建仅在 microsoft 团队中工作的连接器，请直接在[Microsoft 团队应用程序提交](mailto:teamsubm@microsoft.com)中与我们联系。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-112">If that is _not_ the case and you need to create a Connector that only works in Microsoft Teams, contact us directly at [Microsoft Teams App Submissions](mailto:teamsubm@microsoft.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a6f6-113">选择 "连接器" 开发人员仪表板中的 "**保存**" 后，将注册连接器。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-113">After you choose **Save** in the Connectors Developer Dashboard, your Connector is registered.</span></span> <span data-ttu-id="5a6f6-114">如果要在 AppSource 中发布连接器，请按照[发布 Microsoft 团队应用程序到 AppSource](~/concepts/deploy-and-publish/apps-publish.md)中的说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-114">If you want to publish your Connector in AppSource, follow the instructions in [Publish your Microsoft Teams app to AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="5a6f6-115">如果您不希望在 AppSource 中发布您的应用程序，而只是仅直接将其分发到您的组织，则可以通过[发布到您的组织来](#publish-connectors-for-your-organization)执行此操作。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-115">If you do not wish to publish your app in AppSource, and rather simply distribute it directly to your organization only, you can do so by [publishing to your organization](#publish-connectors-for-your-organization).</span></span> <span data-ttu-id="5a6f6-116">如果只想要发布到您的组织，则无需对连接器仪表板执行进一步操作。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-116">If you only want to publish to your organization, no further action is necessary on the Connector dashboard.</span></span>

### <a name="integrating-the-configuration-experience"></a><span data-ttu-id="5a6f6-117">集成配置体验</span><span class="sxs-lookup"><span data-stu-id="5a6f6-117">Integrating the configuration experience</span></span>

<span data-ttu-id="5a6f6-118">您的用户将完成整个连接器配置体验，而无需离开团队客户端。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-118">Your users will complete the entire Connector configuration experience without having to leave the Teams client.</span></span> <span data-ttu-id="5a6f6-119">若要实现此体验，团队将在 iframe 中直接嵌入配置页面。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-119">To achieve this experience, Teams will embed your configuration page directly within an iframe.</span></span> <span data-ttu-id="5a6f6-120">操作顺序如下所示：</span><span class="sxs-lookup"><span data-stu-id="5a6f6-120">The sequence of operations is as follows:</span></span>

1. <span data-ttu-id="5a6f6-121">用户单击连接器即可开始配置过程。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-121">The user clicks on your connector to begin the configuration process.</span></span>
2. <span data-ttu-id="5a6f6-122">团队将以行为单位加载配置体验。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-122">Teams will load your configuration experience in line.</span></span>
3. <span data-ttu-id="5a6f6-123">用户可与您的 web 体验进行交互以完成配置。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-123">The user interacts with your web experience to complete the configuration.</span></span>
4. <span data-ttu-id="5a6f6-124">用户按 "保存"，这将在代码中触发回调。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-124">The user presses "Save", which triggers a callback in your code.</span></span>
5. <span data-ttu-id="5a6f6-125">代码将通过检索 webhook 设置来处理 save 事件（如下所述）。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-125">Your code will process the save event by retrieving the webhook settings (documented below).</span></span> <span data-ttu-id="5a6f6-126">随后，您的代码应将 webhook 存储在稍后发布事件。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-126">Your code should then store the webhook to post events later.</span></span>

<span data-ttu-id="5a6f6-127">您可以重复使用现有的 web 配置体验，也可以创建单独的版本以在团队中专门托管。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-127">You can reuse your existing web configuration experience or create a separate version to be hosted specifically in Teams.</span></span> <span data-ttu-id="5a6f6-128">您的代码应：</span><span class="sxs-lookup"><span data-stu-id="5a6f6-128">Your code should:</span></span>

1. <span data-ttu-id="5a6f6-129">包括 Microsoft 团队 JavaScript SDK。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-129">Include the Microsoft Teams JavaScript SDK.</span></span> <span data-ttu-id="5a6f6-130">这使您的代码能够访问 Api，以执行常见操作，如获取当前用户/通道/团队上下文和启动身份验证流。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-130">This gives your code access to APIs to perform common operations like getting the current user/channel/team context and initiating authentication flows.</span></span> <span data-ttu-id="5a6f6-131">通过调用初始化 SDK `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-131">Initialize the SDK by calling `microsoftTeams.initialize()`.</span></span>
2. <span data-ttu-id="5a6f6-132">`microsoftTeams.settings.setValidityState(true)`当您想要启用 "保存" 按钮时调用。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-132">Call `microsoftTeams.settings.setValidityState(true)` when you want to enable the Save button.</span></span> <span data-ttu-id="5a6f6-133">应作为对有效用户输入（如选择或字段更新）的响应执行此操作。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-133">You should do this as a response to valid user input, such as a selection or field update.</span></span>
3. <span data-ttu-id="5a6f6-134">注册 `microsoftTeams.settings.registerOnSaveHandler()` 在用户单击 "保存" 时调用的事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-134">Register a `microsoftTeams.settings.registerOnSaveHandler()` event handler, which gets called when the user clicks Save.</span></span>
4. <span data-ttu-id="5a6f6-135">调用 `microsoftTeams.settings.setSettings()` 以保存连接器设置。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-135">Call `microsoftTeams.settings.setSettings()` to save the connector settings.</span></span> <span data-ttu-id="5a6f6-136">如果用户尝试更新连接器的现有配置，此处保存的内容也会显示在 "配置" 对话框中。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-136">What's saved here is also what will be shown in the configuration dialog if the user tries to update an existing configuration for your connector.</span></span>
5. <span data-ttu-id="5a6f6-137">调用 `microsoftTeams.settings.getSettings()` 获取 webhook 属性，包括 URL 本身。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-137">Call `microsoftTeams.settings.getSettings()` to fetch webhook properties, including the URL itself.</span></span> <span data-ttu-id="5a6f6-138">除了在保存事件期间，如果第一次加载页面时，还应调用此过程，在重新配置的情况下。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-138">You should call this  In addition to during the save event, you should also call this when your page is first loaded in the case of a re-configuration.</span></span>
6. <span data-ttu-id="5a6f6-139">Optional注册在 `microsoftTeams.settings.registerOnRemoveHandler()` 用户删除连接器时调用的事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-139">(Optional) Register a `microsoftTeams.settings.registerOnRemoveHandler()` event handler, which gets called when the user removes your connector.</span></span> <span data-ttu-id="5a6f6-140">此事件为服务提供了执行任何清理操作的机会。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-140">This event gives your service an opportunity to perform any cleanup actions.</span></span>

#### <a name="getsettings-response-properties"></a><span data-ttu-id="5a6f6-141">`GetSettings()`响应属性</span><span class="sxs-lookup"><span data-stu-id="5a6f6-141">`GetSettings()` response properties</span></span>

>[!Note]
><span data-ttu-id="5a6f6-142">此处的调用返回的参数 `getSettings` 不同于从选项卡调用此方法的参数，与[此处](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest)记录的不同。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-142">The parameters returned by the `getSettings` call here are different than if you were to invoke this method from a tab, and differ from those documented [here](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest).</span></span>

| <span data-ttu-id="5a6f6-143">参数</span><span class="sxs-lookup"><span data-stu-id="5a6f6-143">Parameter</span></span>   | <span data-ttu-id="5a6f6-144">详细信息</span><span class="sxs-lookup"><span data-stu-id="5a6f6-144">Details</span></span> |
|-------------|---------|
| `entityId`       | <span data-ttu-id="5a6f6-145">调用时由您的代码设置的实体 ID `setSettings()` 。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-145">The entity ID, as set by your code when calling `setSettings()`.</span></span> |
| `configName`  | <span data-ttu-id="5a6f6-146">调用时由您的代码设置的配置名称 `setSettings()` 。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-146">The configuration name, as set by your code when calling `setSettings()`.</span></span> |
| `contentUrl` | <span data-ttu-id="5a6f6-147">调用时由您的代码设置的配置页面的 URL`setSettings()`</span><span class="sxs-lookup"><span data-stu-id="5a6f6-147">The URL of the configuration page, as set by your code when calling `setSettings()`</span></span> |
| `webhookUrl` | <span data-ttu-id="5a6f6-148">为此连接器创建的 webhook URL。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-148">The webhook URL created for this connector.</span></span> <span data-ttu-id="5a6f6-149">保留 webhook URL 并使用它来发布结构化的 JSON，以向通道发送卡。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-149">Persist the webhook URL and use it to POST structured JSON to send cards to the channel.</span></span> <span data-ttu-id="5a6f6-150">仅在应用程序成功返回时返回。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-150">The `webhookUrl` is returned only when application returns successfully.</span></span> |
| `appType` | <span data-ttu-id="5a6f6-151">返回的值可以是 `mail`、`groups` 或 `teams`，分别对应 Office 365 邮件、Office 365 组或 Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-151">The values returned can be `mail`, `groups` or `teams` corresponding to the Office 365 Mail, Office 365 Groups or Microsoft Teams respectively.</span></span> |
| `userObjectId` | <span data-ttu-id="5a6f6-152">这是与启动连接器安装程序的 Office 365 用户相对应的唯一 id。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-152">This is the unique id corresponding to the Office 365 user who initiated setup of the connector.</span></span> <span data-ttu-id="5a6f6-153">应该具备安全性。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-153">It should be secured.</span></span> <span data-ttu-id="5a6f6-154">可以使用此值将 Office 365 中设置配置的用户与服务中的用户关联起来。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-154">This value can be used to associate the user in Office 365 who set up the configuration to the user in your service.</span></span> |

<span data-ttu-id="5a6f6-155">如果需要在上述步骤2中加载页面时对用户进行身份验证，请参阅[此链接](~/tabs/how-to/authentication/auth-flow-tab.md)，以了解有关如何在嵌入页面时集成登录的详细信息。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-155">If you need to authenticate the user as part of loading your page in step 2 above, refer to [this link](~/tabs/how-to/authentication/auth-flow-tab.md) for details on how you can integrate login when your page is embedded.</span></span>

> [!NOTE]
> <span data-ttu-id="5a6f6-156">由于跨客户端的兼容性原因，在调用之前，您 `microsoftTeams.authentication.registerAuthenticationHandlers()` 的代码需要使用 URL 和成功/失败回调方法进行调用 `authenticate()` 。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-156">Due to cross-client compatibility reasons, your code will need to call `microsoftTeams.authentication.registerAuthenticationHandlers()` with the URL and success/failure callback methods before calling `authenticate()`.</span></span>

#### <a name="handling-edits"></a><span data-ttu-id="5a6f6-157">处理编辑</span><span class="sxs-lookup"><span data-stu-id="5a6f6-157">Handling edits</span></span>

<span data-ttu-id="5a6f6-158">您的代码应处理返回以编辑现有连接器配置的用户。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-158">Your code should handle users returning to edit an existing connector configuration.</span></span> <span data-ttu-id="5a6f6-159">为此，请 `microsoftTeams.settings.setSettings()` 在初始配置过程中使用以下参数进行调用：</span><span class="sxs-lookup"><span data-stu-id="5a6f6-159">To do this, call `microsoftTeams.settings.setSettings()` during the initial configuration with the following parameters:</span></span>

- <span data-ttu-id="5a6f6-160">`entityId`是您的服务可理解的自定义 ID，它表示用户已配置的内容。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-160">`entityId` is the custom ID that is understood by your service and represents what the user has configured.</span></span>
- <span data-ttu-id="5a6f6-161">`configName`是您的配置代码可以检索的友好名称</span><span class="sxs-lookup"><span data-stu-id="5a6f6-161">`configName` is a friendly name that your configuration code can retrieve</span></span>
- <span data-ttu-id="5a6f6-162">`contentUrl`是在用户编辑现有连接器配置时加载的自定义 URL。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-162">`contentUrl` is a custom URL that gets loaded when a user edits an existing connector configuration.</span></span> <span data-ttu-id="5a6f6-163">您可以使用此 URL 使代码更易于处理编辑案例。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-163">You can use this URL to make it easier for your code to handle the edit case.</span></span>

<span data-ttu-id="5a6f6-164">通常情况下，此调用是作为保存事件处理程序的一部分进行的。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-164">Typically, this call is made as part of your save event handler.</span></span> <span data-ttu-id="5a6f6-165">然后，在 `contentUrl` 加载上述项时，代码应调用 `getSettings()` 以预填充配置 UI 中的任何设置或窗体。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-165">Then, when the `contentUrl` above is loaded, your code should call `getSettings()` to prepopulate any settings or forms in your configuration UI.</span></span>

#### <a name="handling-removals"></a><span data-ttu-id="5a6f6-166">处理删除</span><span class="sxs-lookup"><span data-stu-id="5a6f6-166">Handling removals</span></span>

<span data-ttu-id="5a6f6-167">当用户删除现有连接器配置时，您可以选择执行事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-167">You can optionally execute an event handler when the user removes an existing connector configuration.</span></span> <span data-ttu-id="5a6f6-168">通过调用注册此处理程序 `microsoftTeams.settings.registerOnRemoveHandler()` 。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-168">You register this handler by calling `microsoftTeams.settings.registerOnRemoveHandler()`.</span></span> <span data-ttu-id="5a6f6-169">此处理程序可用于执行清理操作，例如从数据库中删除条目。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-169">This handler can be used to perform cleanup operations such as removing entries from a database.</span></span>

### <a name="including-the-connector-in-your-manifest"></a><span data-ttu-id="5a6f6-170">在清单中包含连接器</span><span class="sxs-lookup"><span data-stu-id="5a6f6-170">Including the Connector in your Manifest</span></span>

<span data-ttu-id="5a6f6-171">您可以从门户下载自动生成的团队应用程序清单。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-171">You can download the auto-generated Teams app manifest from the portal.</span></span> <span data-ttu-id="5a6f6-172">但是，必须先执行以下操作，然后才能使用它测试或发布应用程序：</span><span class="sxs-lookup"><span data-stu-id="5a6f6-172">Before you can use it to test or publish your app, though, you must do the following:</span></span>

- <span data-ttu-id="5a6f6-173">包含两个图标，按照[“图标”](~/concepts/build-and-test/apps-package.md#icons)中的说明。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-173">Include two icons, following the instructions in [Icons](~/concepts/build-and-test/apps-package.md#icons).</span></span>
- <span data-ttu-id="5a6f6-174">修改清单的 `icons` 部分，以便引用图标的文件名，而不是 URL。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-174">Modify the `icons` portion of the manifest to refer to the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="5a6f6-175">以下 manifest.json 文件包含测试和提交应用程序所需的基本元素。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-175">The following manifest.json file contains the basic elements needed to test and submit your app.</span></span>

> [!NOTE]
> <span data-ttu-id="5a6f6-176">将以下示例中的 `id` 和 `connectorId` 替换为连接器的 GUID。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-176">Replace `id` and `connectorId` in the following example with the GUID of your Connector.</span></span>

#### <a name="example-manifestjson-with-connector"></a><span data-ttu-id="5a6f6-177">带连接器的示例 manifest.json</span><span class="sxs-lookup"><span data-stu-id="5a6f6-177">Example manifest.json with Connector</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
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

## <a name="testing-your-connector"></a><span data-ttu-id="5a6f6-178">测试连接器</span><span class="sxs-lookup"><span data-stu-id="5a6f6-178">Testing your Connector</span></span>

<span data-ttu-id="5a6f6-179">若要测试连接器，请将其上传到团队中，就像使用任何其他应用程序一样。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-179">To test your Connector, upload it to a team as you would with any other app.</span></span> <span data-ttu-id="5a6f6-180">可使用连接器开发人员仪表板中的清单文件（按照上一部分的说明进行修改）和两个图标文件来创建 .zip 包。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-180">You can create a .zip package using the manifest file from the Connectors Developer Dashboard (modified as directed in the preceding section) and the two icon files.</span></span>

<span data-ttu-id="5a6f6-181">上传应用程序后，从任意频道打开连接器列表。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-181">After you upload the app, open the Connectors list from any channel.</span></span> <span data-ttu-id="5a6f6-182">向下滚动到底部，查看 **“上传”** 部分中的应用程序。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-182">Scroll to the bottom to see your app in the **Uploaded** section.</span></span>

![“连接器”对话框中上传部分的屏幕截图](~/assets/images/connectors/connector_dialog_uploaded.png)

<span data-ttu-id="5a6f6-184">现在可启动配置体验。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-184">You can now launch the configuration experience.</span></span> <span data-ttu-id="5a6f6-185">请注意，此流程完全在 Microsoft 团队中作为托管体验发生。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-185">Be aware that this flow occurs entirely within Microsoft Teams as a hosted experience.</span></span>

<span data-ttu-id="5a6f6-186">若要验证 `HttpPOST` 操作是否正常运行，请[将邮件发送到您的连接器](~/webhooks-and-connectors/how-to/connectors-using.md)。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-186">To verify that an `HttpPOST` action is working correctly, [send messages to your connector](~/webhooks-and-connectors/how-to/connectors-using.md).</span></span>

## <a name="publish-connectors-for-your-organization"></a><span data-ttu-id="5a6f6-187">为您的组织发布连接器</span><span class="sxs-lookup"><span data-stu-id="5a6f6-187">Publish Connectors for your organization</span></span>

<span data-ttu-id="5a6f6-188">有时，您可能不希望将连接器应用程序发布到公用 AppSource/存储，但希望它仅供组织中的用户使用。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-188">Sometimes, you may not want to publish your connector app to the public AppSource/Store but would like it to be available only to the users in your organization.</span></span> <span data-ttu-id="5a6f6-189">在这种情况下，可以将自定义连接器应用上传到[组织的应用程序目录](~/concepts/deploy-and-publish/apps-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-189">In such cases, you can upload your custom connector app to your [organization's App Catalog](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="5a6f6-190">这样，你的连接器应用程序将仅可用于该组织，而无需将连接器发布到公用存储。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-190">This way, your connector app will be available only to that organization, and you will not need to publish your connector to the public store.</span></span>

<span data-ttu-id="5a6f6-191">上载应用程序包后，若要配置和使用团队中的连接器，可以通过执行以下步骤，从组织的应用程序目录中进行安装：</span><span class="sxs-lookup"><span data-stu-id="5a6f6-191">Once you've uploaded your app package, to configure and use the connector in a Team it can be installed from the organization's app catalog by following these steps:</span></span>

1. <span data-ttu-id="5a6f6-192">从最左侧垂直导航栏中选择 "应用" 图标。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-192">Select the apps icon from the far left vertical navigation bar.</span></span>
1. <span data-ttu-id="5a6f6-193">在 "**应用**" 窗口中选择 "**连接器**"。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-193">In the **Apps** window select **Connectors**.</span></span>
1. <span data-ttu-id="5a6f6-194">选择要添加的连接器，将显示一个弹出对话框窗口。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-194">Select the connector that you want to add and a pop-up dialog window will display.</span></span>
1. <span data-ttu-id="5a6f6-195">选择 "**添加到团队**栏"。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-195">Select the **Add to a team** bar.</span></span>
1. <span data-ttu-id="5a6f6-196">在下一个对话框窗口中，键入团队或频道名称。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-196">In the next dialog window type a team or channel name.</span></span>
1. <span data-ttu-id="5a6f6-197">从对话框窗口的右下角选择 "**设置连接符**" 栏。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-197">Select the **Set up a connector** bar from the bottom right corner of dialog window.</span></span>
1. <span data-ttu-id="5a6f6-198">该连接器将在 " &#9679;&#9679;&#9679; =>*更多选项*"  =>  *连接器*  =>  *All*  =>  *为*该团队的所有连接器提供支持。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-198">The connector will be available in the  section &#9679;&#9679;&#9679; => *More options* => *Connectors* => *All* => *Connectors for you team* for that team.</span></span> <span data-ttu-id="5a6f6-199">您可以通过滚动到此部分或搜索连接器应用来进行导航。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-199">You can navigate by scrolling to this section or search for the connector app.</span></span>
1. <span data-ttu-id="5a6f6-200">若要配置或修改连接器，请选择 "**配置**" 栏。</span><span class="sxs-lookup"><span data-stu-id="5a6f6-200">To configure or modify the connector select the **Configure** bar.</span></span>
