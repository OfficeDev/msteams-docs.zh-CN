---
title: 在整个 Microsoft 365 中扩展 Teams 邮件扩展
description: 下面介绍如何更新基于搜索的 Teams 邮件扩展以在 Outlook 中运行
ms.date: 02/11/2022
ms.topic: tutorial
ms.custom: m365apps
ms.localizationpriority: high
ms.openlocfilehash: 7e3a0d772367952c1726648fce2f10e1d8b885b2
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111372"
---
# <a name="extend-a-teams-message-extension-across-microsoft-365"></a>在整个 Microsoft 365 中扩展 Teams 邮件扩展

> [!NOTE]
> 在整个 Microsoft 365 中 *扩展 Teams 邮件扩展* 目前仅提供 [公共开发人员预览版](../resources/dev-preview/developer-preview-intro.md)。 预览版中包含的功能可能不完整，并且在公开发布之前可能会发生更改。 它们仅用于测试和探索目的。 不应在生产应用程序中使用它们。

基于搜索的[邮件扩展](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions)允许用户搜索外部系统，并通过 Microsoft Teams 客户端的撰写邮件区域共享结果。 通过[在整个 Microsoft 365 中扩展 Teams 应用（预览版）](overview.md)，现在可以将基于搜索的 Teams 邮件扩展引入 Outlook Windows 桌面版和网页版体验。

更新基于搜索的 Teams 邮件扩展以运行 Outlook 的过程涉及以下步骤：

> [!div class="checklist"]
>
> * 更新应用清单
> * 为机器人添加 Outlook 通道
> * 在 Teams 中旁加载更新后的应用

本指南的其余部分将指导你完成这些步骤，并演示如何在 Outlook Windows 桌面版和网页版中预览邮件扩展。

## <a name="prerequisites"></a>先决条件

完成本教程需要：

* Microsoft 365 开发人员计划沙盒租户
* *在 Office 365 目标版本* 中注册的沙盒租户
* 从 Microsoft 365 应用 *beta 版通道安装了 Office 应用的测试环境*
* 带有 Teams 工具包（预览版）扩展的 Microsoft Visual Studio Code（可选）

> [!div class="nextstepaction"]
> [安装先决条件](prerequisites.md)

## <a name="prepare-your-message-extension-for-the-upgrade"></a>为升级准备邮件扩展

如果已有邮件扩展，请创建生产项目的副本或分支以进行测试，并在应用清单中更新应用 ID 以使用新标识符（不同于生产应用 ID）。

若要使用示例代码完成本教程，请按照 [Teams 邮件扩展搜索示例](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search)中的设置步骤快速生成 Microsoft Teams 基于搜索的邮件扩展。 或者，可以从[为 TeamsJS SDK v2 预览版更新的同一 Teams 邮件扩展搜索示例](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2/NPM-search-connector-M365)开始，然后继续[在 Outlook 中预览邮件扩展](#preview-your-message-extension-in-outlook)。 更新后的示例也在 Teams 工具包扩展中可用：*“开发”* > *“查看示例”* > **“NPM 搜索连接器**”。

:::image type="content" source="images/toolkit-search-sample.png" alt-text="Teams 工具包中的 NPM 搜索连接器示例":::

## <a name="update-the-app-manifest"></a>更新应用清单

需要使用 [Teams 开发人员预览清单](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview)架构和 `m365DevPreview` 清单版本，以使 Teams 邮件扩展能够在 Outlook 中运行。

可通过两个选项更新应用清单：

# <a name="teams-toolkit"></a>[Teams 工具包](#tab/manifest-teams-toolkit)

1. 打开 *命令面板*：`Ctrl+Shift+P`
1. 运行 `Teams: Upgrade Teams manifest to support Outlook and Office apps` 命令并选择应用清单文件。 将就地进行更改。

# <a name="manual-steps"></a>[手动步骤](#tab/manifest-manual)

打开 Teams 应用清单，使用以下值更新 `$schema` 和 `manifestVersion`：

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```

---

如果使用 Teams 工具包创建了邮件扩展应用，则可以使用它来验证清单文件的更改并识别任何错误。 打开命令面板 (`Ctrl+Shift+P`) 并找到“**Teams: 验证清单文件**”，或者从 Teams 工具包的“部署”菜单中选择该选项（查找 Visual Studio Code 左侧的 Teams 图标）。

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams 工具包“部署”菜单下的“验证清单文件”选项":::

## <a name="add-an-outlook-channel-for-your-bot"></a>为机器人添加 Outlook 通道

在 Microsoft Teams 中，邮件扩展包含托管的 Web 服务和应用清单，该清单定义了 Web 服务的托管位置。 该 Web 服务通过为机器人注册的 Teams 通道，利用 [Bot Framework SDK](/azure/bot-service/bot-service-overview) 的消息传递架构和安全通信协议。

为了让用户与 Outlook 中的邮件扩展进行交互，需要向机器人添加 Outlook 通道：

1. 从 [Microsoft Azure 门户](https://portal.azure.com)（或 [Bot Framework 门户](https://dev.botframework.com)，如果之前在此门户中注册）中，导航到你的机器人资源。

1. 从 *“设置”* 中，选择“**通道**”。

1. 单击“**Outlook**”，选择“**邮件扩展**”选项卡，然后单击“**保存**”。

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="从“Azure 机器人通道”窗格为机器人添加 Outlook“邮件扩展”通道":::

1. 确认 Outlook 通道随 Microsoft Teams 一起列在机器人的“**通道**”窗格中：

    :::image type="content" source="images/azure-bot-channels.png" alt-text="“Azure 机器人通道”窗格，其中列出了 Microsoft Teams 和 Outlook 通道":::

## <a name="update-microsoft-azure-active-directory-azure-ad-app-registration-for-sso"></a>更新 Microsoft Azure Active Directory (Azure AD) 应用注册以实现 SSO

> [!NOTE]
> 如果使用 [Teams 邮件扩展搜索示例](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search)，则可以跳过此步骤，因为该方案不涉及 Azure Active Directory (AAD) 单一登录身份验证。

邮件扩展的 Azure Active Directory 单一登录 (SSO) 在 Outlook [中的工作方式与在 Teams](/microsoftteams/platform/bots/how-to/authentication/auth-aad-sso-bots)中的工作方式相同，但是需要在租户的 *应用注册* 门户中，将多个客户端应用程序标识符添加到机器人的 Azure AD 应用注册。

1. 使用沙盒租户帐户登录 [Azure 门户](https://portal.azure.com)。
1. 打开“**应用注册**”。
1. 选择应用程序的名称以打开其应用注册。
1. 在 *“管理”* 下选择“**公开 API**”。

在“**授权客户端应用程序**”部分中，确保列出了以下所有 `Client Id` 值：

|Microsoft 365 客户端应用程序 | 客户端 ID |
|--|--|
|Teams 桌面和移动版 |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
|Teams Web |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
|Outlook 桌面版 | d3590ed6-52b3-4102-aeff-aad2292ab01c |
|Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
|Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-updated-message-extension-in-teams"></a>在 Teams 中旁加载更新后的邮件扩展

最后一步是在 Microsoft Teams 中旁加载更新后的邮件扩展（[应用包](/microsoftteams/platform/concepts/build-and-test/apps-package)）。 完成后，邮件扩展将显示在已安装 *应用* 的撰写邮件区域中。

1. 将 Teams 应用（清单和应用[图标](/microsoftteams/platform/resources/schema/manifest-schema#icons)）打包为一个 zip 文件。 如果使用 Teams 工具包创建应用，则可以使用 Teams 工具包的 *“部署”* 菜单中的“**压缩 Teams 元数据包**”选项轻松完成此操作：

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="适用于 Visual Studio Code 的 Teams 工具包扩展中的“压缩 Teams 元数据包”选项":::

1. 使用沙盒租户帐户登录到 Teams，通过单击用户配置文件旁的省略号 (**...**) 菜单并打开“**关于**”来检查 *“开发人员预览版”* 选项是否处于打开状态，从而验证你是否在使用 *公共开发人员预览版*。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="从 Teams 省略号菜单中打开“关于”，并验证是否选中了“开发人员预览版”选项":::

1. 打开 *“应用”* 窗格，然后依次单击“**上传自定义应用**”和“**为我或我的团队上传**”。

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Teams“应用”窗格中的“上传自定义应用”按钮":::

1. 选择应用包，然后单击 *“打开”*。

通过 Teams 进行旁加载后，邮件扩展将在 Office 网页版中可用。

## <a name="preview-your-message-extension-in-outlook"></a>在 Outlook 中预览邮件扩展

现在可以测试在 Outlook Windows 桌面版和网页版中运行的邮件扩展。 虽然更新后的邮件扩展将继续在具有完整[邮件扩展功能支持](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions)的 Teams 中运行，但需要注意在启用了 Outlook 的体验的早期预览版中存在一些限制：

* Outlook 中的邮件扩展仅限于邮件 [*撰写* 上下文](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions)。 即使 Teams 邮件扩展在其清单中包含 `commandBox` 作为 *上下文*，当前预览版也仅限于邮件撰写 (`compose`) 选项。 不支持从全局 Outlook *“搜索”* 框中调用邮件扩展。
* Outlook 不支持[基于操作的邮件扩展](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS)命令。 如果应用同时具有基于搜索和基于操作的命令，则其将出现在 Outlook 中，但操作菜单将不可用。
* 不支持在电子邮件中插入超过五个[自适应卡片](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design)；不支持自适应卡片 v1.4 及更高版本。
* 插入的卡片不支持 `messageBack`、`imBack`、`invoke` 和 `signin` 类型的[卡片操作](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json)。 支持仅限于 `openURL`：单击时，用户将被重定向到新标签页中的指定 URL。

在测试邮件扩展时，可以通过 [Activity](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md) 对象的 [channelId](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) 识别机器人请求的来源（来自 Teams 与 Outlook）。 当用户执行查询时，服务会收到一个标准 Bot Framework `Activity` 对象。 Activity 对象中的一个属性是 `channelId`，其值为 `msteams` 或 `outlook`，具体取决于机器人请求的来源。 有关详细信息，请参阅[基于搜索的邮件扩展 SDK](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions)。

### <a name="outlook-on-the-web"></a>Outlook 网页版

预览在 Outlook 网页版中运行的应用：

1. 使用测试租户凭据登录 [outlook.com](https://www.outlook.com)。
1. 选择“**新建邮件**”。
1. 在撰写窗口底部打开“**更多应用**”浮出菜单。

:::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="单击邮件撰写窗口底部的“更多应用”菜单以使用邮件扩展":::

邮件扩展随即列出。 可以从其中调用它，并像在 Teams 中撰写邮件时一样使用它。

### <a name="outlook"></a>Outlook

> [!IMPORTANT]
> 请参阅 [Microsoft Teams - Microsoft 365 开发人员博客](https://devblogs.microsoft.com/microsoft365dev/)上的最新更新，以检查你的测试租户是否可以使用 Outlook Windows 桌面版对 Teams 个人应用的支持。

预览在 Outlook Windows 桌面版中运行的应用：

1. 启动使用测试租户凭据登录的 Outlook。 1. 单击“**新建电子邮件**”。
1. 打开顶部功能区上的“**更多应用**”浮出菜单。

邮件扩展随即列出。 可以从其中调用它，并像在 Teams 中撰写邮件时一样使用它。

## <a name="next-steps"></a>后续步骤

启用了 Outlook 的 Teams 邮件扩展处于预览阶段，不支持用于生产环境。 下面介绍如何将启用了 Outlook 的邮件扩展分发给预览受众以进行测试。

### <a name="single-tenant-distribution"></a>单租户分发

可以通过以下三种方式之一将启用了 Outlook 和 Office 的个人选项卡分发给一个测试（或生产）租户中的预览受众：

#### <a name="teams-client"></a>Teams 客户端

在 *“应用”* 菜单中，选择 *“管理应用”* > “**将应用提交到组织**”。这需要 IT 管理员的批准。

#### <a name="microsoft-teams-admin-center"></a>Microsoft Teams 管理中心

作为 Teams 管理员，可以从 [Teams 管理中心](https://admin.teams.microsoft.com/)为组织的租户上传和预安装应用包。有关详细信息，请参阅[在 Microsoft Teams 管理中心上传自定义应用](/MicrosoftTeams/upload-custom-apps)。

#### <a name="microsoft-admin-center"></a>Microsoft 管理中心

作为全局管理员，可以从 [Microsoft 管理中心](https://admin.microsoft.com/)上传和预安装应用包。有关详细信息，请参阅[合作伙伴在集成应用门户中测试和部署 Microsoft 365 应用](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps)。

### <a name="multitenant-distribution"></a>多租户分发

在启用了 Outlook 的 Teams 邮件扩展的早期开发人员预览期间，尚不支持分发到 Microsoft AppSource。
