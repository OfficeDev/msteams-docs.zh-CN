---
title: 跨Microsoft 365扩展Teams消息扩展
description: 下面介绍如何更新基于搜索的Teams消息扩展以在Outlook中运行
ms.date: 02/11/2022
ms.topic: tutorial
ms.custom: m365apps
ms.openlocfilehash: 3bab70d85d071763ffbbae7cb1dae11534d0e812
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104537"
---
# <a name="extend-a-teams-message-extension-across-microsoft-365"></a>跨Microsoft 365扩展Teams消息扩展

> [!NOTE]
> *跨Microsoft 365扩展Teams消息扩展* 目前仅在 [公共开发人员预览版](../resources/dev-preview/developer-preview-intro.md)中可用。 预览版中包含的功能可能不完整，并且在公开发布之前可能会发生更改。 它们仅用于测试和探索目的。 不应在生产应用程序中使用它们。

基于搜索[的消息扩展](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions)允许用户搜索外部系统，并通过Microsoft Teams客户端的撰写消息区域共享结果。 通过[将Teams应用扩展到Microsoft 365 (预览版) ](overview.md)，现在可以将基于搜索的Teams消息扩展Outlook Windows桌面和 Web 体验。

更新基于搜索的Teams消息扩展以运行Outlook的过程涉及以下步骤：

> [!div class="checklist"]
>
> * 更新应用清单
> * 为机器人添加Outlook通道
> * 在 Teams 中旁加载更新后的应用

本指南的其余部分将指导你完成这些步骤，并演示如何在Windows桌面和 Web 的Outlook中预览消息扩展。

## <a name="prerequisites"></a>先决条件

若要完成本教程，需要：

* Microsoft 365开发人员计划沙盒租户
* 在 *Office 365目标版本* 中注册的沙盒租户
* 从 Microsoft 365 应用版 *beta 通道* 安装Office应用的测试环境
* Microsoft Visual Studio包含Teams Toolkit (预览) 扩展的代码 (可选) 

> [!div class="nextstepaction"]
> [安装先决条件](prerequisites.md)

## <a name="prepare-your-message-extension-for-the-upgrade"></a>为升级准备消息扩展

如果有现有消息扩展名，请创建生产项目的副本或分支，以便在应用清单中测试和更新应用 ID，以使用与生产应用 ID) 不同的新标识符 (。

如果要使用示例代码完成本教程，请按照[Teams消息扩展搜索示例](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search)中的设置步骤快速生成基于搜索的Microsoft Teams消息扩展。 或者，可以从[针对 TeamsJS SDK v2 预览版更新的相同Teams消息扩展搜索示例](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2/NPM-search-connector-M365)开始，然后[在Outlook中继续预览邮件扩展](#preview-your-message-extension-in-outlook)。 更新后的示例也可在Teams Toolkit扩展中使用：*DevelopmentView* >  *samplesNPM* >  **搜索连接器**。

:::image type="content" source="images/toolkit-search-sample.png" alt-text="Teams Toolkit中的 NPM 搜索连接器示例":::

## <a name="update-the-app-manifest"></a>更新应用清单

需要使用[Teams开发人员预览清单](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview)架构和`m365DevPreview`清单版本，使Teams消息扩展在Outlook中运行。

你有两个用于更新应用清单的选项：

# <a name="teams-toolkit"></a>[Teams 工具包](#tab/manifest-teams-toolkit)

1. 打开 *命令面板*： `Ctrl+Shift+P`
1. 运行该 `Teams: Upgrade Teams manifest to support Outlook and Office apps` 命令并选择应用清单文件。 将就地进行更改。

# <a name="manual-steps"></a>[手动步骤](#tab/manifest-manual)

打开Teams应用清单并使用以下值更新和`manifestVersion`更新`$schema`：

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```

---

如果使用Teams Toolkit创建邮件扩展应用，则可以使用它来验证清单文件的更改并识别任何错误。 打开命令面板`Ctrl+Shift+P`并找到 **Teams：验证清单文件** 或从Teams Toolkit (的“部署”菜单中选择该选项，Teams查找Visual Studio Code) 左侧的Teams图标。

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams Toolkit“部署”菜单下的“验证清单文件”选项":::

## <a name="add-an-outlook-channel-for-your-bot"></a>为机器人添加Outlook通道

在Microsoft Teams中，消息扩展包含托管的 Web 服务和应用清单，用于定义 Web 服务的托管位置。 Web 服务通过为机器人注册的Teams通道利用 [Bot Framework SDK](/azure/bot-service/bot-service-overview) 消息传送架构和安全通信协议。

若要让用户从Outlook与消息扩展进行交互，需要向机器人添加Outlook通道：

1. 从[Microsoft Azure门户](https://portal.azure.com) (或 [Bot Framework 门户](https://dev.botframework.com)（如果之前在) 注册）导航到机器人资源。

1. 从 *设置* 中，选择 **“通道**”。

1. 单击 **Outlook**，选择 **“消息扩展”** 选项卡，然后单击 **“保存**”。

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="从 Azure 机器人通道窗格为机器人添加Outlook“消息扩展”通道":::

1. 确认Outlook通道与机器人 **通道窗格** 中的Microsoft Teams一起列出：

    :::image type="content" source="images/azure-bot-channels.png" alt-text="列出Microsoft Teams和Outlook通道的 Azure 机器人通道窗格":::

## <a name="update-microsoft-azure-active-directory-azure-ad-app-registration-for-sso"></a>更新 SSO 的Microsoft Azure Active Directory (Azure AD) 应用注册

> [!NOTE]
> 如果使用[Teams消息扩展搜索示例](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search)，则可以跳过此步骤，因为此方案不涉及Azure Active Directory (AAD) 单Sign-On身份验证。

Azure Active Directory消息扩展 (SSO) 的单一登录在Outlook中的工作方式与在 [Teams中](/microsoftteams/platform/bots/how-to/authentication/auth-aad-sso-bots)的工作方式相同，但需要将多个客户端应用程序标识符添加到租户应用注册门户中机器人的 *Azure AD* 应用注册。

1. 使用沙盒租户帐户登录[Azure 门户](https://portal.azure.com)。
1. 打开 **应用注册**。
1. 选择应用程序的名称以打开其应用注册。
1. 选择“*管理*) ”下的 **“公开 API** (”。

在 **“授权客户端应用程序** ”部分中，确保列出了以下 `Client Id` 所有值：

|Microsoft 365 客户端应用程序 | 客户端 ID |
|--|--|
|Teams桌面和移动设备 |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
|Teams Web |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
|Outlook 桌面版 | d3590ed6-52b3-4102-aeff-aad2292ab01c |
|Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
|Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-updated-message-extension-in-teams"></a>在 Teams 中旁加载更新的消息扩展

最后一步是在Microsoft Teams中旁加载更新的消息扩展 ([应用包](/microsoftteams/platform/concepts/build-and-test/apps-package)) 。 完成后，消息扩展将从撰写消息区域显示在已安装的 *“应用* ”中。

1. 将Teams应用程序 (清单和应用[图标](/microsoftteams/platform/resources/schema/manifest-schema#icons)打包) 在 zip 文件中。 如果使用Teams Toolkit创建应用，则可以在Teams Toolkit的 *“部署*”菜单中使用 **Zip Teams 元数据包** 选项轻松执行此操作：

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Teams Toolkit扩展中的“Zip Teams 元数据包”选项Visual Studio Code":::

1. 使用沙盒租户帐户登录到Teams *，并单* 击省略号 () **...**  

    :::image type="content" source="images/teams-dev-preview.png" alt-text="从Teams省略号菜单中，打开“关于”并验证是否选中了“开发人员预览”选项":::

1. 打开 *“应用*”窗格，**单击Upload自定义应用**，然后 **为我或我的团队Upload**。

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Teams“应用”窗格中的“Upload自定义应用”按钮":::

1. 选择应用包，然后单击 *“打开*”。

通过Teams旁加载后，消息扩展将在Outlook 网页版中提供。

## <a name="preview-your-message-extension-in-outlook"></a>在Outlook中预览邮件扩展

现在可以测试在桌面和 Web 上Windows Outlook中运行的消息扩展。 虽然更新的消息扩展将继续在具有[消息扩展](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions)功能完全支持的Teams中运行，但此已启用Outlook体验的早期预览中存在一些需要注意的限制：

* Outlook中的消息扩展仅限于邮件 [*撰写* 上下文](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions)。 即使Teams邮件扩展名包含`commandBox`在其清单中作为 *上下文*，当前预览版也仅限于邮件组合 () `compose` 选项。 不支持从全局Outlook *搜索* 框调用消息扩展。
* Outlook不支持[基于操作的消息扩展](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS)命令。 如果应用同时具有搜索和基于操作的命令，它将在Outlook中显示，但操作菜单将不可用。
* 不支持在电子邮件中插入五个以上的 [自适应卡](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design) 片;不支持自适应卡 v1.4 及更高版本。
* 插入的卡片的类型`messageBack``imBack`、`invoke`类型和`signin`不支持的卡[片操作](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json)。 支持限制为 `openURL`：单击时，用户将重定向到新选项卡中的指定 URL。

测试消息扩展时，可以标识源 (源自Teams，而不是由 [Activity](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md) 对象的 [channelId](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) Outlook) 机器人请求。 当用户执行查询时，服务将收到标准 Bot Framework `Activity` 对象。 Activity 对象中的一个属性是`channelId`，该属性的值或值`msteams``outlook`取决于机器人请求的来源。 有关详细信息，请参阅  [基于搜索的消息扩展 SDK](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions)。

### <a name="outlook-on-the-web"></a>Outlook 网页版

若要预览在 Outlook 网页版 中运行的应用，

1. 使用测试租户的凭据登录到 [outlook.com](https://www.outlook.com) 。
1. 选择 **“新建消息**”。
1. 在组合窗口底部打开 **“更多应用** ”浮出菜单。

:::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="单击邮件撰写窗口底部的“更多应用”菜单以使用邮件扩展插件":::

邮件扩展将列出。 你可以从那里调用它，并像在Teams中撰写消息时一样使用它。

### <a name="outlook"></a>Outlook

> [!IMPORTANT]
> 请参阅Microsoft Teams的最新更新 [- Microsoft 365开发人员博客](https://devblogs.microsoft.com/microsoft365dev/)，检查Windows桌面支持Teams个人应用Outlook是否可供测试租户使用。

若要在Windows桌面上预览Outlook中运行的应用：

1. 启动Outlook使用测试租户的凭据登录。 1. 单击 **“新建电子邮件**”。
1. 打开顶部功能区上的 **“更多应用** ”浮出菜单。

邮件扩展将列出。 你可以从那里调用它，并像在Teams中撰写消息时一样使用它。

## <a name="next-steps"></a>后续步骤

启用Outlook Teams消息扩展处于预览状态，不支持生产用途。 下面介绍如何将已启用Outlook的消息扩展分发给预览访问群体以进行测试。

### <a name="single-tenant-distribution"></a>单租户分布

Outlook和启用Office的个人选项卡可以通过以下三种方式之一跨测试 (或生产) 租户分发给预览版受众：

#### <a name="teams-client"></a>Teams 客户端

在 *“应用* ”菜单中，选择 *“管理应用* > **”，将应用提交到组织**。这需要 IT 管理员的批准。

#### <a name="microsoft-teams-admin-center"></a>Microsoft Teams管理中心

作为Teams管理员，可以从[Teams管理员](https://admin.teams.microsoft.com/)上传并预安装组织的租户的应用包。有关详细信息，请参阅[Microsoft Teams管理中心Upload自定义应用](/MicrosoftTeams/upload-custom-apps)。

#### <a name="microsoft-admin-center"></a>Microsoft 管理中心

作为全局管理员，可以从 [Microsoft 管理员](https://admin.microsoft.com/)上传并预安装应用包。有关详细信息，请参阅[集成应用门户中合作伙伴的测试和部署Microsoft 365 应用版](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps)。

### <a name="multitenant-distribution"></a>多租户分布

在启用了Outlook Teams消息扩展的早期开发人员预览期间，尚不支持分发到 Microsoft AppSource。
