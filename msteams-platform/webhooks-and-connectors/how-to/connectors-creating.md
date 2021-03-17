---
title: Office 365 连接器
description: 介绍如何在 Microsoft Teams 中开始使用 Office 365 连接器
keywords: Teams o365 连接器
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: d0fe380cd168b8dcbddc5af0de96160e0bc259a9
ms.sourcegitcommit: 1ce74ed167bb81bf09f7f6f8d518093efafb549e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2021
ms.locfileid: "50827919"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a>为 Microsoft Teams 创建 Office 365 连接器

>使用 Microsoft Teams 应用，可以添加现有 Office 365 连接器或生成要包括在 Microsoft Teams 中的新连接器。 有关详细信息 [，请参阅构建](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) 你自己的连接器。

## <a name="adding-a-connector-to-your-teams-app"></a>将连接器添加到 Teams 应用

你可以将已注册的连接器作为 Teams 应用包的一部分进行分发。 无论是作为独立解决方案，还是体验在 Teams 中启用的多种功能之一，都可以将[](~/concepts/build-and-test/apps-package.md)连接器打包[](~/concepts/deploy-and-publish/apps-publish.md)并发布为 AppSource 提交的一部分，也可以直接向用户提供连接器以在 Teams 中上传。 [](~/concepts/extensibility-points.md)

若要分发连接器，你需要使用连接器开发人员仪表板 [进行注册](https://outlook.office.com/connectors/home/login/#/publish)。 默认情况下，一旦注册连接器，就会假定连接器将在支持连接器的所有 Office 365 产品（包括 Outlook 和 Teams）中工作。 如果并非如此 _，_ 并且你需要创建仅在 Microsoft Teams 中工作的连接器，请直接通过 Microsoft Teams [应用提交联系我们](mailto:teamsubm@microsoft.com)。

> [!IMPORTANT]
> 在连接器 **开发人员** 仪表板中选择"保存"后，连接器即已注册。 如果你想要在 AppSource 中发布连接器，请按照将 Microsoft Teams 应用发布到 [AppSource 中的说明操作](~/concepts/deploy-and-publish/apps-publish.md)。 如果你不希望在 AppSource 中发布应用，而只是直接将其分发到你的组织，可以通过发布到你的组织 [来这样做](#publish-connectors-for-your-organization)。 如果只想发布到组织，则无需在连接器仪表板上执行任何进一步的操作。

### <a name="integrating-the-configuration-experience"></a>集成配置体验

用户无需离开 Teams 客户端即可完成整个连接器配置体验。 为了实现此体验，Teams 将直接在 iframe 中嵌入你的配置页面。 操作顺序如下所示：

1. 用户单击连接器开始配置过程。
2. Teams 将在线加载你的配置体验。
3. 用户与 Web 体验交互以完成配置。
4. 用户按"保存"，这将触发代码中的回调。
5. 代码将处理保存事件，方法为检索以下 (webhook) 。 然后，代码应存储 Webhook 以稍后发布事件。

可以重用现有 Web 配置体验或创建单独的版本以专门托管在 Teams 中。 代码应：

1. 包括 Microsoft Teams JavaScript SDK。 这样，代码可以访问 API 来执行常见操作，如获取当前用户/频道/团队上下文和启动身份验证流。 通过调用 初始化 `microsoftTeams.initialize()` SDK。
2. 在 `microsoftTeams.settings.setValidityState(true)` 要启用"保存"按钮时调用。 应作为对有效用户输入（如选择或字段更新）的响应来这样做。
3. 注册 `microsoftTeams.settings.registerOnSaveHandler()` 事件处理程序，该事件处理程序在用户单击"保存"时调用。
4. 调用 `microsoftTeams.settings.setSettings()` 以保存连接器设置。 如果用户尝试更新连接器的现有配置，此处保存的也是将在配置对话框中显示内容。
5. 调用 `microsoftTeams.settings.getSettings()` 以提取 webhook 属性，包括 URL 本身。 除了在保存事件期间之外，还应在重新配置的情况下首次加载页面时调用此调用。
6.  (可选) 注册事件处理程序，该事件处理程序在用户删除 `microsoftTeams.settings.registerOnRemoveHandler()` 连接器时调用。 此事件为服务提供了执行任何清理操作的机会。

下面是用于创建不带 CSS 的连接器配置页的示例 HTML：

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

#### <a name="getsettings-response-properties"></a>`GetSettings()` 响应属性

>[!Note]
>此处调用返回的参数与从选项卡调用此方法时不同，并且 `getSettings` 与此处记录的参数 [不同](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true)。

| 参数   | 详细信息 |
|-------------|---------|
| `entityId`       | 实体 ID，由代码在调用 时设置 `setSettings()` 。 |
| `configName`  | 调用 时由代码设置的配置名称 `setSettings()` 。 |
| `contentUrl` | 配置页面的 URL，由代码在调用时设置 `setSettings()` |
| `webhookUrl` | 为此连接器创建的 webhook URL。 保留 webhook URL，并将其用于 POST 结构化 JSON 以将卡片发送到频道。 仅在应用程序成功返回时返回。 |
| `appType` | 返回的值可以是 `mail`、`groups` 或 `teams`，分别对应 Office 365 邮件、Office 365 组或 Microsoft Teams。 |
| `userObjectId` | 这是与启动连接器设置的 Office 365 用户对应的唯一 ID。 应该具备安全性。 可以使用此值将 Office 365 中设置配置的用户与服务中的用户关联起来。 |

如果需要在加载以上步骤 2 中的页面时对用户进行身份验证，请参阅此链接，详细了解在[](~/tabs/how-to/authentication/auth-flow-tab.md)嵌入页面时如何集成登录。

> [!NOTE]
> 由于跨客户端兼容性原因，代码在调用 之前将需要使用 `microsoftTeams.authentication.registerAuthenticationHandlers()` URL 和成功/失败回调方法调用 `authenticate()` 。

#### <a name="handling-edits"></a>处理编辑

代码应处理用户返回以编辑现有连接器配置。 为此，在初始 `microsoftTeams.settings.setSettings()` 配置期间调用以下参数：

- `entityId` 是服务可以理解的自定义 ID，表示用户配置了哪些项。
- `configName` 是配置代码可以检索的友好名称
- `contentUrl` 是用户编辑现有连接器配置时加载的自定义 URL。 您可以使用此 URL 更轻松地让代码处理编辑案例。

通常，此调用作为保存事件处理程序的一部分进行。 然后，当 `contentUrl` 加载上述内容时，代码应调用 `getSettings()` 以预填充配置 UI 中的任何设置或表单。

#### <a name="handling-removals"></a>处理删除

可以选择在用户删除现有连接器配置时执行事件处理程序。 通过调用 注册此处理程序 `microsoftTeams.settings.registerOnRemoveHandler()` 。 此处理程序可用于执行清理操作，例如从数据库中删除条目。

### <a name="including-the-connector-in-your-manifest"></a>在清单中包括连接器

你可以从门户下载自动生成的 Teams 应用清单。 但是，在使用它测试或发布应用之前，必须执行以下操作：

- [包括两个图标](../../concepts/build-and-test/apps-package.md#app-icons)。
- 修改清单的 `icons` 部分，以便引用图标的文件名，而不是 URL。

以下 manifest.json 文件包含测试和提交应用程序所需的基本元素。

> [!NOTE]
> 将以下示例中的 `id` 和 `connectorId` 替换为连接器的 GUID。

#### <a name="example-manifestjson-with-connector"></a>带连接器的示例 manifest.json

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

## <a name="testing-your-connector"></a>测试连接器

若要测试连接器，请将其上传到团队中，就像使用任何其他应用程序一样。 可使用连接器开发人员仪表板中的清单文件（按照上一部分的说明进行修改）和两个图标文件来创建 .zip 包。

上传应用程序后，从任意频道打开连接器列表。 向下滚动到底部，查看 **“上传”** 部分中的应用程序。

![“连接器”对话框中上传部分的屏幕截图](~/assets/images/connectors/connector_dialog_uploaded.png)

现在可启动配置体验。 请注意，此流完全作为托管体验在 Microsoft Teams 中发生。

若要验证操作 `HttpPOST` 是否正常工作， [请将邮件发送到连接器](~/webhooks-and-connectors/how-to/connectors-using.md)。

## <a name="publish-connectors-for-your-organization"></a>发布组织的连接器

有时，你可能不希望将连接器应用发布到公共 AppSource/Store，但希望该应用仅对贵组织的用户可用。 在这种情况下，您可以将自定义连接器应用程序上载到[组织的"应用程序目录"。](~/concepts/deploy-and-publish/apps-publish.md) 这样，连接器应用将仅适用于该组织，并且无需将连接器发布到公共应用商店。

上传应用包后，若要在团队中配置和使用连接器，可以按照以下步骤从组织的应用程序目录中安装：

1. 从最左侧垂直导航栏中选择应用图标。
1. 在"**应用"** 窗口中，选择 **"连接器"。**
1. 选择要添加的连接器，将显示一个弹出对话框窗口。
1. 选择" **添加到团队"** 栏。
1. 在下一个对话框窗口中，键入团队或频道名称。
1. 从 **对话框窗口右下角** 选择"设置连接线栏"。
1. 该连接器将在该团队的" &#9679;&#9679;&#9679; ">""更多选项""连接器""所有连接器"  =>    =>    =>  部分中提供。 可以通过滚动到此部分或搜索连接器应用来导航。
1. 若要配置或修改连接器，请选择"配置 **"** 栏。

## <a name="code-sample"></a>代码示例
|**示例名称** | **说明** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| 连接器    | 向团队频道生成通知的示例 Office 365 连接器。|   [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| 通用连接器示例 |易于为支持 Webhook 的任何系统自定义的通用连接器的示例代码。|  | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|
