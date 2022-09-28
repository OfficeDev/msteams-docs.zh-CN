---
title: 创建 Office 365 连接器
author: laujan
description: Office 365连接器入门。 将连接器添加到 Microsoft Teams 中的 Teams 应用。 示例 (.NET，Node.js) Office 365连接器向 Teams 通道生成通知。
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 06/16/2021
ms.openlocfilehash: 977bcac5daa3185177fbc9a3b441c245541914df
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100726"
---
# <a name="create-office-365-connectors"></a>创建 Office 365 连接器

With Microsoft Teams apps, you can add your existing Office 365 Connector or build a new one within Teams. For more information, see [build your own connector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector).

请参阅以下视频，了解如何创建Office 365连接器：
<br>

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4OIzv]
<br>

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="add-a-connector-to-teams-app"></a>将连接器添加到 Teams 应用

可以在 AppSource 提交过程中创建[文件包](~/concepts/build-and-test/apps-package.md)并[发布 ](~/concepts/deploy-and-publish/apps-publish.md) 连接器。 可以将已注册的连接器作为 Teams 应用文件包的一部分进行分发。 有关 Teams 应用的入口点的信息，请参阅[功能](~/concepts/extensibility-points.md)。 还可以直接向用户提供文件包，以便在 Teams 中上传。

要分发连接器，请从[连接器开发人员仪表板](https://aka.ms/connectorsdashboard)中注册。

若要使连接器仅在 Teams 中工作，请按照说明提交连接器，将 [应用发布到 Microsoft Teams 应用商店](~/concepts/deploy-and-publish/appsource/publish.md) 文章。 否则，注册的连接器适用于支持应用程序的所有 Office 365 产品，包括 Outlook 和 Teams。

> [!IMPORTANT]
> 在连接器开发人员仪表板中选择“**保存**”后，会注册连接器。 如果要在 AppSource 中发布连接器，请按照[将 Microsoft Teams 应用发布到 AppSource](~/concepts/deploy-and-publish/apps-publish.md) 中的说明操作。 如果不想在 AppSource 中发布应用，请将其直接分发给组织。 在为组织发布连接器以后，无需在连接器仪表板上执行进一步操作。

### <a name="integrate-the-configuration-experience"></a>集成配置体验

用户无需离开 Teams 客户端即可完成整个连接器配置体验。 为了获得体验，可以直接在 iframe 中将 Teams 嵌入配置页面。 操作序列如下：

1. 用户选择连接器，开始配置过程。
1. 用户与 Web 体验交互以完成配置。
1. 用户选择能触发代码回调的“**保存**”。

    > [!NOTE]
    >
    > * 代码可以通过检索 Webhook 设置来处理保存事件。 代码存储 Webhook 以在稍后发布事件。
    > * 配置体验在 Teams 中内联加载。

可以重用现有的 Web 配置体验，或创建单独的版本，专门托管在 Teams 中。 代码必须包括 Teams JavaScript SDK。 这使代码能够访问 API 来执行常见操作，例如获取当前用户、通道或团队上下文，并启动身份验证流。

要集成配置体验：

> [!NOTE]
> 从 Teams JavaScript 客户端 SDK (TeamsJS) v.2.0.0 开始，已弃用 *设置* 命名空间中的 API，以支持 *页面* 命名空间中的等效 API，包括 `pages.getConfig()` 子命名空间中 `pages.config` 的其他 API。 有关详细信息，请参阅 [TeamsJS 版本 2.0 中的新增功能](../../tabs/how-to/using-teams-client-sdk.md#whats-new-in-teamsjs-version-20)

1. 通过调用`app.initialize()`初始化 SDK。
1. 调用 `pages.config.setValidityState(true)` 以启用“**保存**”。

    > [!NOTE]
    > 必须调用 `microsoftTeams.pages.config.setValidityState(true)` 作为对用户选择或字段更新的响应。

1. 注册 `microsoftTeams.pages.config.registerOnSaveHandler()` 事件处理程序，当用户选择“**保存**”时调用。
1. Call `microsoftTeams.pages.config.setConfig()` to save the connector settings. The saved settings are also shown in the configuration dialog if the user tries to update an existing configuration for your connector.
1. 调用 `microsoftTeams.pages.getConfig()` 以提取 Webhook 属性，包括 URL。

    > [!NOTE]
    > 在重新配置的情况下，首次加载页面时必须调用 `microsoftTeams.pages.getConfig()`。

1. 注册 `microsoftTeams.pages.config.registerOnRemoveHandler()` 事件处理程序，当用户删除连接器时调用。

此事件使服务有机会执行任何清理操作。

以下代码提供了一个示例 HTML，可用于在没有客户服务和支持的情况下创建连接器配置页：

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

<script src="https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js" integrity="sha384-Q2Z9S56exI6Oz/ThvYaV0SUn8j4HwS8BveGPmuwLXe4CvCUEGlL80qSzHMnvGqee" crossorigin="anonymous"></script>
<script src="/Scripts/jquery-1.10.2.js"></script>

<script type="module">
        import {app, pages} from 'https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js';
        
        function onClick() {
            pages.config.setValidityState(true);
        }

        await app.initialize();
        pages.config.registerOnSaveHandler(function (saveEvent) {
            var radios = document.getElementsByName('notificationType');

            var eventType = '';
            if (radios[0].checked) {
                eventType = radios[0].value;
            } else {
                eventType = radios[1].value;
            }

            await pages.config.setConfig({
                entityId: eventType,
                contentUrl: "https://YourSite/Connector/Setup",
                removeUrl:"https://YourSite/Connector/Setup",
                configName: eventType
                });

            pages.getConfig().then(async (config) {
                // We get the Webhook URL from config.webhookUrl which needs to be saved. 
                // This can be used later to send notification.
            });

            saveEvent.notifySuccess();
        });

        pages.config.registerOnRemoveHandler(function (removeEvent) {
            alert("Removed" + JSON.stringify(removeEvent));
        });

</script>
```

要在加载页面时对用户进行身份验证，请参阅[选项卡中的身份验证流](~/tabs/how-to/authentication/auth-flow-tab.md)，以在嵌入页面时集成登录。

> [!NOTE]
> 在 TeamsJS v.2.0.0 之前，由于跨客户端兼容性原因，在调`authenticate()`用之前，代码必须使用 URL 和成功或失败回调方法进行调`microsoftTeams.authentication.registerAuthenticationHandlers()`用。 从 TeamsJS v.2.0.0 开始， *registerAuthenticationHandlers* 已被弃用，转而使用所需的身份验证参数直接调用 [身份验证 ()](/javascript/api/@microsoft/teams-js/authentication#@microsoft-teams-js-authentication-authenticate) 。

#### <a name="getconfig-response-properties"></a>`getConfig` 响应属性

>[!NOTE]
>从选项卡调用此方法时，调用返回的 `getConfig` 参数不同于引用中记录的 [参数](/javascript/api/@microsoft/teams-js/pages#@microsoft-teams-js-pages-getconfig)。

下表提供了参数和 `getConfig` 响应属性的详细信息：

| 参数   | 详细信息 |
|-------------|---------|
| `entityId`       | 实体 ID，在调用 `setConfig()` 时由代码设置。 |
| `configName`  | 配置名称，在调用 `setConfig()` 时由代码设置。 |
| `contentUrl` | 配置页的 URL，在调用 `setConfig()` 时由代码设置。 |
| `webhookUrl` | The webhook URL created for the connector. Use the webhook URL to POST structured JSON to send cards to the channel. The `webhookUrl` is returned only when the application returns data successfully. |
| `appType` | 返回的值可以`mail`是或`groups``teams`分别对应于Office 365邮件、Office 365组或 Teams。 |
| `userObjectId` | The unique ID corresponding to the Office 365 user who initiated the set up of the connector. It must be secured. This value can be used to associate the user in Office 365, who has set up the configuration in your service. |

#### <a name="handle-edits"></a>处理编辑

代码必须处理返回编辑现有连接器配置的用户。 为此，请在初始配置期间使用以下参数调用 `microsoftTeams.pages.config.setConfig()`：

* `entityId` 是自定义 ID，表示用户已由服务配置和理解的内容。
* `configName` 是可以检索的配置代码名称。
* `contentUrl` 是用户编辑现有连接器配置时加载的自定义 URL。

此调用作为保存事件处理程序的一部分进行。 然后，在加载 `contentUrl` 以后，代码必须调用 `getConfig()` 以预填充配置用户界面中的任何设置或表单。

#### <a name="handle-removals"></a>处理删除

可以在用户删除现有的连接器配置时执行事件处理程序。 通过调用 `microsoftTeams.pages.config.registerOnRemoveHandler()` 注册该处理程序。 此处理程序用于执行清理操作，如删除数据库中的条目。

### <a name="include-the-connector-in-your-manifest"></a>在清单中包含连接器

从开发人员门户 () <https://dev.teams.microsoft.com> 下载自动生成的 *Teams 应用清单*。 在测试或发布应用之前，请执行以下步骤：

1. [包括两个图标](../../concepts/build-and-test/apps-package.md#app-icons)。
1. 修改清单的 `icons` 部分以包括图标的文件名而不是 URL。

以下 *manifest.json* 文件包含测试和提交应用所需的元素：

> [!NOTE]
> 将以下示例中的 `id` 和 `connectorId` 替换为连接器的 GUID。

#### <a name="example-of-manifestjson-with-connector"></a>带连接器的 manifest.json 示例

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

## <a name="test-your-connector"></a>测试连接器

To test your connector, upload it to a team with any other app. You can create a .zip package using the manifest file from the two icon files and connectors Developer Dashboard, modified as directed in [Include the connector in your Manifest](#include-the-connector-in-your-manifest).

上传应用后，从任意频道打开连接器列表。 滚动到底部，查看“**上传**”部分中的应用：

![“连接器”对话框中“上传”部分的屏幕截图](~/assets/images/connectors/connector_dialog_uploaded.png)

> [!NOTE]
> 该流完全作为托管体验在 Teams 中发生。

要验证操作 `HttpPOST` 是否正常工作，[将消息发送到连接器](~/webhooks-and-connectors/how-to/connectors-using.md)。

按照 [分步指南](../../sbs-teams-connectors.yml) 在 Teams 中创建和测试连接器。

## <a name="distribute-webhook-and-connector"></a>分发 Webhook 和连接器

1. 直接为团队[设置传入 Webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md#create-an-incoming-webhook)。

1. 添加[配置页](~/webhooks-and-connectors/how-to/connectors-creating.md?#integrate-the-configuration-experience)并在Office 365连接器中发布传入 Webhook。

1. 在 [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) 提交过程中打包并发布连接器。

## <a name="code-sample"></a>代码示例

下表提供了示例名称及其说明：

|**示例名称** | **说明** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| 连接器 | 生成 Teams 通道通知的 Office 365 连接器示例。| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| 一般连接器示例 |对于支持 Webhook 的任何系统，可以轻松自定义的一般连接器代码的示例。| | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|

## <a name="step-by-step-guide"></a>分步指南

按照[分步指南](../../sbs-teams-connectors.yml)在 Teams 中生成和测试连接器。

## <a name="see-also"></a>另请参阅

* [创建和发送邮件](~/webhooks-and-connectors/how-to/connectors-using.md)
* [创建传入 Webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [创建 Office 365 连接器](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [管理员如何启用或禁用连接器](/MicrosoftTeams/office-365-custom-connectors#enable-or-disable-connectors-in-teams)
* [管理员如何在组织内发布自定义连接器](/MicrosoftTeams/office-365-custom-connectors)
* [使用 JavaScript 生成通知机器人](../../sbs-gs-notificationbot.yml)
* [使用 JavaScript 生成第一个机器人应用](../../sbs-gs-bot.yml)
