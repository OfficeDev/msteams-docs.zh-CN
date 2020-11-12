---
title: Office 365 连接器
description: 介绍如何开始使用 Microsoft 团队中的 Office 365 连接器
keywords: Teams o365 连接器
ms.date: 04/19/2019
ms.openlocfilehash: dcd9f7e68dfe834fbcac245941944007beedf478
ms.sourcegitcommit: 0aeb60027f423d8ceff3b377db8c3efbb6da4d17
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/11/2020
ms.locfileid: "48998019"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a>为 Microsoft 团队创建 Office 365 连接器

>在 Microsoft 团队应用程序中，您可以添加现有的 Office 365 连接器或构建新的 Office 连接器以将其包含在 Microsoft 团队中。 有关详细信息，请参阅 [生成您自己的连接器](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) 。

## <a name="adding-a-connector-to-your-teams-app"></a>将连接器添加到你的团队应用

您可以将已注册的连接器作为团队应用程序包的一部分进行分发。 无论是独立的解决方案还是你的经验在团队中启用的几项 [功能](~/concepts/extensibility-points.md) 之一，都可以 [打包](~/concepts/build-and-test/apps-package.md) 和 [发布](~/concepts/deploy-and-publish/apps-publish.md) 连接器作为 AppSource 提交的一部分，也可以直接将其提供给用户以在团队内上载。

若要分发连接器，您需要使用 [连接器开发人员仪表板](https://outlook.office.com/connectors/home/login/#/publish)进行注册。 默认情况下，注册连接器后，系统会假定您的连接器能够在所有支持它们的 Office 365 产品（包括 Outlook 和团队）中工作。 如果 _不_ 是这种情况，并且需要创建仅在 microsoft 团队中工作的连接器，请直接在 [Microsoft 团队应用程序提交](mailto:teamsubm@microsoft.com)中与我们联系。

> [!IMPORTANT]
> 选择 "连接器" 开发人员仪表板中的 " **保存** " 后，将注册连接器。 如果要在 AppSource 中发布连接器，请按照 [发布 Microsoft 团队应用程序到 AppSource](~/concepts/deploy-and-publish/apps-publish.md)中的说明进行操作。 如果您不希望在 AppSource 中发布您的应用程序，而只是仅直接将其分发到您的组织，则可以通过 [发布到您的组织来](#publish-connectors-for-your-organization)执行此操作。 如果只想要发布到您的组织，则无需对连接器仪表板执行进一步操作。

### <a name="integrating-the-configuration-experience"></a>集成配置体验

您的用户将完成整个连接器配置体验，而无需离开团队客户端。 若要实现此体验，团队将在 iframe 中直接嵌入配置页面。 操作顺序如下所示：

1. 用户单击连接器即可开始配置过程。
2. 团队将以行为单位加载配置体验。
3. 用户可与您的 web 体验进行交互以完成配置。
4. 用户按 "保存"，这将在代码中触发回调。
5. 代码将通过检索) 下面记录 (的 webhook 设置来处理 save 事件。 随后，您的代码应将 webhook 存储在稍后发布事件。

您可以重复使用现有的 web 配置体验，也可以创建单独的版本以在团队中专门托管。 您的代码应：

1. 包括 Microsoft 团队 JavaScript SDK。 这使您的代码能够访问 Api，以执行常见操作，如获取当前用户/通道/团队上下文和启动身份验证流。 通过调用初始化 SDK `microsoftTeams.initialize()` 。
2. `microsoftTeams.settings.setValidityState(true)`当您想要启用 "保存" 按钮时调用。 应作为对有效用户输入（如选择或字段更新）的响应执行此操作。
3. 注册 `microsoftTeams.settings.registerOnSaveHandler()` 在用户单击 "保存" 时调用的事件处理程序。
4. 调用 `microsoftTeams.settings.setSettings()` 以保存连接器设置。 如果用户尝试更新连接器的现有配置，此处保存的内容也会显示在 "配置" 对话框中。
5. 调用 `microsoftTeams.settings.getSettings()` 获取 webhook 属性，包括 URL 本身。 除了在保存事件期间，如果第一次加载页面时，还应调用此过程，在重新配置的情况下。
6.  (可选) 注册在 `microsoftTeams.settings.registerOnRemoveHandler()` 用户删除连接器时调用的事件处理程序。 此事件为服务提供了执行任何清理操作的机会。

#### <a name="getsettings-response-properties"></a>`GetSettings()` 响应属性

>[!Note]
>此处的调用返回的参数 `getSettings` 不同于从选项卡调用此方法的参数，与 [此处](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true)记录的不同。

| 参数   | 详细信息 |
|-------------|---------|
| `entityId`       | 调用时由您的代码设置的实体 ID `setSettings()` 。 |
| `configName`  | 调用时由您的代码设置的配置名称 `setSettings()` 。 |
| `contentUrl` | 调用时由您的代码设置的配置页面的 URL `setSettings()` |
| `webhookUrl` | 为此连接器创建的 webhook URL。 保留 webhook URL 并使用它来发布结构化的 JSON，以向通道发送卡。 仅在应用程序成功返回时返回。 |
| `appType` | 返回的值可以是 `mail`、`groups` 或 `teams`，分别对应 Office 365 邮件、Office 365 组或 Microsoft Teams。 |
| `userObjectId` | 这是与启动连接器安装程序的 Office 365 用户相对应的唯一 id。 应该具备安全性。 可以使用此值将 Office 365 中设置配置的用户与服务中的用户关联起来。 |

如果需要在上述步骤2中加载页面时对用户进行身份验证，请参阅 [此链接](~/tabs/how-to/authentication/auth-flow-tab.md) ，以了解有关如何在嵌入页面时集成登录的详细信息。

> [!NOTE]
> 由于跨客户端的兼容性原因，在调用之前，您 `microsoftTeams.authentication.registerAuthenticationHandlers()` 的代码需要使用 URL 和成功/失败回调方法进行调用 `authenticate()` 。

#### <a name="handling-edits"></a>处理编辑

您的代码应处理返回以编辑现有连接器配置的用户。 为此，请 `microsoftTeams.settings.setSettings()` 在初始配置过程中使用以下参数进行调用：

- `entityId` 是您的服务可理解的自定义 ID，它表示用户已配置的内容。
- `configName` 是您的配置代码可以检索的友好名称
- `contentUrl` 是在用户编辑现有连接器配置时加载的自定义 URL。 您可以使用此 URL 使代码更易于处理编辑案例。

通常情况下，此调用是作为保存事件处理程序的一部分进行的。 然后，在 `contentUrl` 加载上述项时，代码应调用 `getSettings()` 以预填充配置 UI 中的任何设置或窗体。

#### <a name="handling-removals"></a>处理删除

当用户删除现有连接器配置时，您可以选择执行事件处理程序。 通过调用注册此处理程序 `microsoftTeams.settings.registerOnRemoveHandler()` 。 此处理程序可用于执行清理操作，例如从数据库中删除条目。

### <a name="including-the-connector-in-your-manifest"></a>在清单中包含连接器

您可以从门户下载自动生成的团队应用程序清单。 但是，必须先执行以下操作，然后才能使用它测试或发布应用程序：

- 包含两个图标，按照[“图标”](~/concepts/build-and-test/apps-package.md#icons)中的说明。
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

现在可启动配置体验。 请注意，此流程完全在 Microsoft 团队中作为托管体验发生。

若要验证 `HttpPOST` 操作是否正常运行，请 [将邮件发送到您的连接器](~/webhooks-and-connectors/how-to/connectors-using.md)。

## <a name="publish-connectors-for-your-organization"></a>为您的组织发布连接器

有时，您可能不希望将连接器应用程序发布到公用 AppSource/存储，但希望它仅供组织中的用户使用。 在这种情况下，可以将自定义连接器应用上传到 [组织的应用程序目录](~/concepts/deploy-and-publish/apps-publish.md)。 这样，你的连接器应用程序将仅可用于该组织，而无需将连接器发布到公用存储。

上载应用程序包后，若要配置和使用团队中的连接器，可以通过执行以下步骤，从组织的应用程序目录中进行安装：

1. 从最左侧垂直导航栏中选择 "应用" 图标。
1. 在 " **应用** " 窗口中选择 " **连接器** "。
1. 选择要添加的连接器，将显示一个弹出对话框窗口。
1. 选择 " **添加到团队** 栏"。
1. 在下一个对话框窗口中，键入团队或频道名称。
1. 从对话框窗口的右下角选择 " **设置连接符** " 栏。
1. 该连接器将在 " &#9679;&#9679;&#9679; => *更多选项* "  =>  *连接器*  =>  *All*  =>  *为* 该团队的所有连接器提供支持。 您可以通过滚动到此部分或搜索连接器应用来进行导航。
1. 若要配置或修改连接器，请选择 " **配置** " 栏。
