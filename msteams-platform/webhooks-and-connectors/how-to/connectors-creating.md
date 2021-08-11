---
title: 创建 Office 365 连接器
author: laujan
description: 介绍如何开始使用 Office 365 中的连接器Microsoft Teams
keywords: Teams o365 连接器
localization_priority: Normal
ms.topic: conceptual
ms.date: 06/16/2021
ms.openlocfilehash: e52402e841b675de7d0c19302b8c8090bcb90cef27ac61e8ac3d6dd69a0bb076
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2021
ms.locfileid: "57709316"
---
# <a name="create-office-365-connectors"></a>创建 Office 365 连接器

借助Microsoft Teams，你可以添加现有 Office 365 连接器，或在 Teams 中生成一个新的连接器。 有关详细信息，请参阅构建 [你自己的连接器](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector)。

## <a name="add-a-connector-to-teams-app"></a>向应用添加Teams连接器

可以将[连接器](~/concepts/build-and-test/apps-package.md)[打包并发布](~/concepts/deploy-and-publish/apps-publish.md)为 AppSource 提交的一部分。 你可以将注册的连接器作为应用包的一Teams分发。 有关应用入口点Teams，请参阅[功能](~/concepts/extensibility-points.md)。 还可以直接向用户提供程序包，以在 Teams。

若要分发连接器，必须通过连接器开发人员仪表板 [进行注册](https://outlook.office.com/connectors/home/login/#/publish)。 注册连接器时，假定它适用于支持应用程序的Office 365产品，包括 Outlook 和 Teams。 如果不是这种情况，并且你必须创建仅在 Microsoft Teams 中工作的连接器，请联系：Microsoft Teams[应用提交电子邮件](mailto:teamsubm@microsoft.com)。

> [!IMPORTANT]
> 连接器在连接器开发人员 **仪表板中选择"** 保存"后注册。 如果你想要在 AppSource 中发布连接器，请按照将应用发布到[AppSource Microsoft Teams中的说明操作](~/concepts/deploy-and-publish/apps-publish.md)。 如果不想在 AppSource 中发布应用，请将其直接分发到组织。 为 [组织发布连接器后](#publish-connectors-for-the-organization)，无需在连接器仪表板上执行其他操作。

### <a name="integrate-the-configuration-experience"></a>集成配置体验

用户可以完成整个连接器配置体验，而无需离开 Teams 客户端。 若要获取体验，Teams直接在 iframe 中嵌入配置页面。 操作顺序如下所示：

1. 用户选择连接器以开始配置过程。
1. 用户与 Web 体验交互以完成配置。
1. 用户选择" **保存"，** 这将在代码中触发回调。

    > [!NOTE]
    > * 代码可以通过检索 webhook 设置处理保存事件。 代码存储 Webhook 以稍后发布事件。
    > * 配置体验在 Teams 内内加载。

可以重用现有 Web 配置体验，或创建一个单独的版本以专门托管在 Teams。 您的代码必须包含 Microsoft Teams Sdk。 这样，代码可以访问 API 来执行常见操作，如获取当前用户、频道或团队上下文以及启动身份验证流程。

**集成配置体验**

1. 通过调用`microsoftTeams.initialize()`初始化 SDK。
1. 调用 `microsoftTeams.settings.setValidityState(true)` 以启用 **Save**。

    > [!NOTE]
    > 您必须调用 `microsoftTeams.settings.setValidityState(true)` 作为用户选择或字段更新的响应。

1. 注册 `microsoftTeams.settings.registerOnSaveHandler()` 事件处理程序，在用户选择"保存"时 **调用。**
1. 调用 `microsoftTeams.settings.setSettings()` 以保存连接器设置。 如果用户尝试更新连接器的现有配置，则配置对话框中也会显示保存的设置。
1. 调用 `microsoftTeams.settings.getSettings()` 以提取 webhook 属性，包括 URL。

    > [!NOTE]
    > 首次加载 `microsoftTeams.settings.getSettings()` 页面时必须调用 ，以防重新配置。

1. 注册 `microsoftTeams.settings.registerOnRemoveHandler()` 事件处理程序，在用户删除连接器时调用该处理程序。

此事件为服务提供了执行任何清理操作的机会。

以下代码提供了一个示例 HTML，用于创建没有客户服务和支持的连接器配置页：

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

若要在加载页面时对用户进行身份验证，请参阅在嵌入页面[](~/tabs/how-to/authentication/auth-flow-tab.md)时集成登录的选项卡的身份验证流。

> [!NOTE]
> 由于跨客户端兼容性原因，代码在调用 之前必须使用 URL 和 `microsoftTeams.authentication.registerAuthenticationHandlers()` 成功或失败回调方法调用 `authenticate()` 。

#### <a name="getsettings-response-properties"></a>`GetSettings` 响应属性

>[!NOTE]
>从选项卡调用此方法时，调用返回的参数是不同的，并且不同于 js 设置中 `getSettings` 记录 [的参数](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true)。

下表提供了参数和响应属性 `GetSetting` 的详细信息：

| 参数   | 详细信息 |
|-------------|---------|
| `entityId`       | 实体 ID，由代码在调用 时设置 `setSettings()` 。 |
| `configName`  | 调用 时由代码设置的配置名称 `setSettings()` 。 |
| `contentUrl` | 配置页面的 URL，由代码在调用 时设置 `setSettings()` 。 |
| `webhookUrl` | 为连接器创建的 webhook URL。 使用 POST 结构化 JSON 的 webhook URL 将卡片发送到频道。 `webhookUrl`仅在应用程序成功返回数据时返回 。 |
| `appType` | 返回的值可以是 、 `mail` 或 `groups` 分别对应于邮件Office 365组Office 365组Microsoft Teams `teams` 组。 |
| `userObjectId` | 与启动连接器Office 365的用户对应的唯一 ID。 它必须是安全的。 此值可用于关联服务中Office 365，该用户已在你的服务中设置配置。 |

#### <a name="handle-edits"></a>处理编辑

您的代码必须处理返回以编辑现有连接器配置的用户。 为此，在初始 `microsoftTeams.settings.setSettings()` 配置期间调用以下参数：

- `entityId` 是表示用户已配置和您的服务理解的自定义 ID。
- `configName` 是配置代码可以检索的名称。
- `contentUrl` 是用户编辑现有连接器配置时加载的自定义 URL。

此调用作为保存事件处理程序的一部分进行。 然后， `contentUrl` 在加载 时，代码必须调用 以预填充配置用户界面中任何 `getSettings()` 设置或表单。

#### <a name="handle-removals"></a>处理删除

您可以在用户删除现有连接器配置时执行事件处理程序。 通过调用 注册此处理程序 `microsoftTeams.settings.registerOnRemoveHandler()` 。 此处理程序用于执行清理操作，例如从数据库中删除条目。

### <a name="include-the-connector-in-your-manifest"></a>在清单中包括连接器

从门户下载 `Teams app manifest` 自动生成的 。 在测试或发布应用之前，请执行以下步骤：

1. [包括两个图标](../../concepts/build-and-test/apps-package.md#app-icons)。
1. 修改 `icons` 清单部分以包括图标的文件名，而不是 URL。

以下manifest.js文件包含测试和提交应用所需的元素：

> [!NOTE]
> 将 `id` `connectorId` 和 替换为连接器的 GUID。

#### <a name="example-of-manifestjson-with-connector"></a>连接器manifest.js打开的示例

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

## <a name="enable-or-disable-connectors-in-teams"></a>启用或禁用 Teams

PowerShell V2 模块Exchange Online新式验证，并适用于多重身份验证，称为 MFA，用于连接到 Exchange 中所有与 PowerShell 相关的Microsoft 365。 管理员可以使用 Exchange Online PowerShell 禁用整个租户或特定组邮箱的连接器，从而影响该租户或邮箱中的所有用户。 无法对部分（而非其他）禁用。 此外，默认情况下，连接器对 政府社区云（称为 GCC 租户）禁用。

租户级别设置会覆盖组级别设置。 例如，如果管理员为组启用连接器，并禁用租户上的连接器，则禁用该组的连接器。 若要在 Teams中启用连接器，Exchange Online带或不带 MFA 的新式验证连接到[PowerShell。](/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true)

### <a name="commands-to-enable-or-disable-connectors"></a>用于启用或禁用连接器的命令

在 Exchange Online PowerShell 中运行以下命令：

* 若要禁用租户的连接器 `Set-OrganizationConfig -ConnectorsEnabled:$false` ：。
* 若要禁用租户的可操作邮件 `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false` ：。
* 若要为连接器启用Teams，请运行以下命令：
  * `Set-OrganizationConfig -ConnectorsEnabled:$true `
  * `Set-OrganizationConfig -ConnectorsEnabledForTeams:$true`
  * `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$true`

有关 PowerShell 模块交换功能详细信息，请参阅[Set-OrganizationConfig。](/powershell/module/exchange/Set-OrganizationConfig?view=exchange-ps&preserve-view=true) 若要启用或禁用Outlook连接器，[请将应用连接到](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab?ui=en-us&rs=en-us&ad=us)Outlook。

## <a name="test-your-connector"></a>测试连接器

若要测试连接器，请通过任何其他应用将其上载到团队。 可以使用两个.zip图标文件和连接器开发人员仪表板中的清单文件创建一个程序包，按照在清单中包括连接器中的指示 [进行修改](#include-the-connector-in-your-manifest)。

上传应用后，从任何渠道打开连接器列表。 滚动到底部，在"已上载"部分 **查看** 你的应用：

!["连接器"对话框中已上载节的屏幕截图](~/assets/images/connectors/connector_dialog_uploaded.png)

> [!NOTE]
> 流完全在托管体验Microsoft Teams内部发生。

若要验证 `HttpPOST` 操作是否正常工作， [请将邮件发送到连接器](~/webhooks-and-connectors/how-to/connectors-using.md)。

## <a name="publish-connectors-for-the-organization"></a>发布组织的连接器

如果希望连接器仅对贵组织的用户可用，可以将自定义连接器应用程序上载到 [组织的应用程序目录](~/concepts/deploy-and-publish/apps-publish.md)。

上载应用包以在团队中配置和使用连接器后，从组织的应用程序目录中安装连接器。

**设置连接器**

1. 从 **左侧** 导航栏中选择"应用"。
1. 在"**应用"** 部分，选择"**连接器"。**
1. 选择要添加的连接器。 将出现一个弹出对话框窗口。
1. 从下拉菜单中，选择"**添加到团队"。**
1. 在搜索框中，键入团队或频道名称。
1. 从 **对话框窗口** 右下角的下拉菜单中选择"设置连接器"。

> [!IMPORTANT]
> 目前，自定义连接器在 doD 政府社区云 (GCC) 、GCC-High 和国防部 (不可用) 。

该连接器位于该团队的 &#9679;&#9679;&#9679; > "更多 **选项**""连接器  >    >    >  **""所有** 连接器"部分中。 可以通过滚动到此部分或搜索连接器应用来导航。 若要配置或修改连接器，请选择"配置 **"。**

## <a name="distribute-webhook-and-connector"></a>分发 Webhook 和连接器

1. [直接为团队设置传入 Webhook。](~/webhooks-and-connectors/how-to/add-incoming-webhook.md?branch=pr-en-us-3076#create-incoming-webhook)
1. 添加配置[页面，](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#integrate-the-configuration-experience)在 O365 连接器中发布传入[Webhook。](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#publish-connectors-for-the-organization)
1. 将连接器打包并发布为 [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) 提交的一部分。

## <a name="code-sample"></a>代码示例

下表提供了示例名称及其说明：

|**示例名称** | **说明** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| 连接器    | 示例Office 365将通知生成到Teams连接器。|   [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| 通用连接器示例 |通用连接器的示例代码，易于为支持 Webhook 的任何系统进行自定义。|  | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|

## <a name="see-also"></a>另请参阅

* [创建和发送邮件](~/webhooks-and-connectors/how-to/connectors-using.md)
* [创建传入 Webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [创建 Office 365 连接器](~/webhooks-and-connectors/how-to/connectors-creating.md)
