---
title: 在整个 Microsoft 365 中扩展 Teams 邮件扩展
description: 在本文中，你将了解如何通过更新应用清单、添加 Outlook 频道和旁加载更新的应用来更新基于搜索的 Teams 消息扩展以在 Outlook 中运行。
ms.date: 05/24/2022
ms.topic: tutorial
ms.custom: m365apps
ms.localizationpriority: high
ms.openlocfilehash: 790c6324f012da8aabe7c4489a414d9887e03640
ms.sourcegitcommit: 4ba6392eced76ba6baeb6d6dd9ba426ebf4ab24f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2022
ms.locfileid: "66919730"
---
# <a name="extend-a-teams-message-extension-across-microsoft-365"></a>在整个 Microsoft 365 中扩展 Teams 邮件扩展

基于搜索的[邮件扩展](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions)允许用户搜索外部系统，并通过 Microsoft Teams 客户端的撰写邮件区域共享结果。 通过[跨 Microsoft 365 扩展 Teams 应用](overview.md)，现在可以引入基于生产搜索的 Teams 邮件扩展，以便在 Outlook Windows 桌面版和 outlook.com 中预览受众。

更新基于搜索的 Teams 邮件扩展以运行 Outlook 的过程涉及以下步骤：

> [!div class="checklist"]
>
> * 更新应用清单。
> * 为机器人添加 Outlook 通道。
> * 在 Teams 中旁加载更新后的应用。

本指南的其余部分将指导你完成这些步骤，并演示如何在 Outlook Windows 桌面版和 outlook.com 中预览邮件扩展。

## <a name="prerequisites"></a>先决条件

完成本教程需要：

* Microsoft 365 开发人员计划沙盒租户。
* 为沙盒租户注册 *Office 365 目标版本*。
* 从 Microsoft 365 应用 *Beta 版频道* 安装了 Office 应用的测试环境。
* （可选）带有 Teams 工具包扩展的 Microsoft Visual Studio Code。

> [!div class="nextstepaction"]
> [发布针对 Microsoft 365 扩展的 Teams 应用](publish.md)

## <a name="prepare-your-message-extension-for-the-upgrade"></a>为升级准备邮件扩展

如果在生产中已有邮件扩展，请创建项目的副本或分支进行测试，并在应用清单中更新应用 ID 以使用新标识符（不同于生产应用 ID，用于测试）。

要使用示例代码完成有关更新现有 Teams 应用的完整教程，请按照 [Teams 邮件扩展搜索示例](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search)中的设置步骤快速构建基于 Microsoft Teams 搜索的邮件扩展。

或者，可以在以下部分使用支持 Outlook 的现成应用，并跳过本教程的 [*更新应用清单*](#update-the-app-manifest)部分。

### <a name="quickstart"></a>快速入门

要从已能够在 Outlook 中运行的[示例邮件扩展](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/NPM-search-connector-M365)开始，请使用适用于 Visual Studio Code 的 Teams 工具包扩展。

1. 从 Visual Studio Code 打开命令面板 (`Ctrl+Shift+P`)，键入 `Teams: Create a new Teams app`。
1. 选择“**新建 Teams 应用**”选项。
1. 选择“**基于搜索的邮件扩展**”以使用最新的 Teams 应用清单（版本 `1.13`）下载 Teams 邮件扩展的示例代码。

    :::image type="content" source="images/toolkit-palatte-search-sample.png" alt-text="在 VS Code 命令面板中键入“新建 Teams 应用”，以列出 Teams 示例选项":::

    该示例也可在 Teams 工具包示例库中以 *NPM 搜索连接器* 形式提供。 在“Teams 工具包”窗格中，选择“*开发*” > “*查看示例*” > “**NPM 搜索连接器**”。

    :::image type="content" source="images/toolkit-search-sample.png" alt-text="Teams 工具包示例库中的 NPM 搜索连接器示例":::

1. 在本地计算机上为工作区文件夹选择一个位置。
1. 打开命令面板（`Ctrl+Shift+P`）并键入 `Teams: Provision in the cloud`，以在 Azure 帐户中创建所需的应用资源（Azure 应用服务、应用服务计划、Azure 机器人和托管标识）。
1. 打开命令面板（`Ctrl+Shift+P`）并键入 `Teams: Deploy to the cloud`，将示例代码部署到 Azure 中预配的资源并启动应用。

在这里，你可以跳转到[为机器人添加 Outlook 频道](#add-an-outlook-channel-for-your-bot)，以完成使 Teams 邮件扩展能够在 Outlook 中正常工作的最后一步。 （应用清单已引用正确的版本，因此无需更新。）

## <a name="update-the-app-manifest"></a>更新应用清单

需要使用 [Teams 开发人员清单](../resources/schema/manifest-schema.md)架构版本 `1.13`，以使 Teams 邮件扩展能够在 Outlook 中运行。

可通过两个选项更新应用清单：

# <a name="teams-toolkit"></a>[Teams 工具包](#tab/manifest-teams-toolkit)

1. 打开命令面板：`Ctrl+Shift+P`。
1. 运行该 `Teams: Upgrade Teams manifest` 命令并选择应用清单文件。 将进行更改。

# <a name="manual-steps"></a>[ 手动步骤 ](#tab/manifest-manual)

打开 Teams 应用清单，使用以下值更新 `$schema` 和 `manifestVersion`：

```json
{
    "$schema" : "https://developer.microsoft.com/json-schemas/teams/v1.13/MicrosoftTeams.schema.json",
    "manifestVersion" : "1.13"
}
```

---

如果使用 Teams 工具包创建了邮件扩展应用，则可以使用它来验证清单文件的更改并识别任何错误。请打开命令面板 `Ctrl+Shift+P` 并找到“**Teams：验证清单文件**”。

## <a name="add-an-outlook-channel-for-your-bot"></a>为机器人添加 Outlook 通道

在 Microsoft Teams 中，邮件扩展包含托管的 Web 服务和应用清单，该清单定义了 Web 服务的托管位置。 该 Web 服务通过为机器人注册的 Teams 通道，利用 [Bot Framework SDK](/azure/bot-service/bot-service-overview) 的消息传递架构和安全通信协议。

为了让用户与 Outlook 中的邮件扩展进行交互，需要向机器人添加 Outlook 通道：

1. 从 [Microsoft Azure 门户](https://portal.azure.com)（或 [Bot Framework 门户](https://dev.botframework.com)，如果之前在此门户中注册）中，导航到你的机器人资源。

1. 从 *“设置”* 中，选择“**通道**”。

1. 在“*可用频道*”下，选择“**Outlook**”。 选择“**邮件扩展**”选项卡，然后单击“**应用**”。

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="从“Azure 机器人通道”窗格为机器人添加 Outlook“邮件扩展”通道":::

1. 确认你的 Outlook 频道与 Teams 一起列出在机器人的“**频道**”窗格中。

    :::image type="content" source="images/azure-bot-channels.png" alt-text="“Azure 机器人频道”窗格，其中列出了 Teams 和 Outlook 频道":::

## <a name="update-microsoft-azure-active-directory-azure-ad-app-registration-for-sso"></a>更新 Microsoft Azure Active Directory (Azure AD) 应用注册以实现 SSO

> [!NOTE]
> 如果使用本教程中提供的[示例应用](#quickstart)，则可以跳过此步骤，因为该方案不涉及 Azure Active Directory (AAD) 单一登录身份验证。

邮件扩展的 Azure Active Directory (AD) 单一登录 (SSO) 在 Outlook [中的工作方式与在 Teams 中的工作方式相同](/microsoftteams/platform/bots/how-to/authentication/auth-aad-sso-bots)。但是，你需要在租户的 *应用注册* 门户中，将多个客户端应用程序标识符添加到机器人的 Azure AD 应用注册。

1. 使用沙盒租户帐户登录 [Azure 门户](https://portal.azure.com)。
1. 打开“**应用注册**”。
1. 选择应用程序的名称以打开其应用注册。
1. 在 *“管理”* 下选择“**公开 API**”。
1. 在“**授权客户端应用程序**”部分中，确保列出了以下所有 `Client Id` 值：

   |Microsoft 365 客户端应用程序 | 客户端 ID |
   |--|--|
   |Teams 桌面和移动版 |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
   |Teams Web |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
   |Outlook 桌面版 | d3590ed6-52b3-4102-aeff-aad2292ab01c |
   |Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
   |Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-updated-message-extension-in-teams"></a>在 Teams 中旁加载更新后的邮件扩展

最后一步是在 Teams 中旁加载更新后的邮件扩展（[应用包](/microsoftteams/platform/concepts/build-and-test/apps-package)）。 完成后，邮件扩展将显示在已安装 *应用* 的撰写邮件区域中。

1. 将 Teams 应用（清单和应用[图标](/microsoftteams/platform/resources/schema/manifest-schema#icons)）打包为一个 zip 文件。 如果使用 Teams 工具包创建应用，则可以使用 Teams 工具包的“*部署*”菜单中的“**压缩 Teams 元数据包**”选项轻松完成此操作。

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="适用于 Visual Studio Code 的 Teams 工具包扩展中的“压缩 Teams 元数据包”选项":::

1. 使用沙盒租户帐户登录 Teams，并切换到“*开发者预览版*”模式。 选择用户个人资料旁边的省略号 (**...**) 菜单，然后依次选择：“**关于**” > “**开发者预览版**”。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="从 Teams 省略号菜单中，打开“关于”，然后选择“开发者预览版”选项":::

1. 选择“**应用**”以打开“**管理你的应用**”窗格。 然后选择“**发布应用**”。

    :::image type="content" source="images/teams-manage-your-apps.png" alt-text="打开“管理应用”窗格，然后选择“发布应用”":::

1. 选择“**上传自定义应用**”选项，选择应用包，然后将其安装（*添加*）到 Teams 客户端。

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Teams 中的“上传自定义应用”选项":::

通过 Teams 旁加载后，邮件扩展将在 outlook.com 和 Outlook Windows 桌面版中可用。

## <a name="preview-your-message-extension-in-outlook"></a>在 Outlook 中预览邮件扩展

下面介绍了如何测试在 Outlook Windows 桌面版和网页版中运行的邮件扩展。

### <a name="outlook-on-the-web"></a>Outlook 网页版

预览在 Outlook 网页版中运行的应用：

1. 使用测试租户的凭据登录 [outlook.com](https://www.outlook.com)。
1. 选择“**新建邮件**”。
1. 在撰写窗口底部打开“**更多应用**”浮出菜单。

    :::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="单击邮件撰写窗口底部的“更多应用”菜单以使用邮件扩展":::

你的邮件扩展已列出。可以从那里调用它，并像在 Teams 中撰写邮件时一样使用它。

### <a name="outlook"></a>Outlook

预览在 Outlook Windows 桌面版中运行的应用：

1. 启动使用测试租户凭据登录的 Outlook。
1. 选择“**新建电子邮件**”。
1. 打开顶部功能区上的“**更多应用**”浮出菜单。

    :::image type="content" source="images/outlook-desktop-compose-more-apps.png" alt-text="单击组合窗口功能区上的“更多应用”以使用邮件扩展":::

你的邮件扩展已列出，它将打开相邻窗格以显示搜索结果。

## <a name="troubleshooting"></a>疑难解答

 虽然更新后的邮件扩展将继续在具有完整[邮件扩展功能支持](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions)的 Teams 中运行，但需要注意在启用了 Outlook 的体验的早期预览版中存在一些限制：

* Outlook 中的邮件扩展仅限于邮件 [*撰写* 上下文](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions)。 即使 Teams 邮件扩展在其清单中包含 `commandBox` 作为 *上下文*，当前预览版也仅限于邮件撰写 (`compose`) 选项。 不支持从全局 Outlook“*搜索*”框中调用邮件扩展。
* Outlook 不支持[基于操作的邮件扩展](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS)命令。 如果应用同时具有基于搜索和基于操作的命令，则其将出现在 Outlook 中，但操作菜单将不可用。
* 不支持在电子邮件中插入超过五个[自适应卡片](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design)；不支持自适应卡片 v1.4 及更高版本。
* 插入的卡片不支持 `messageBack`、`imBack`、`invoke` 和 `signin` 类型的[卡片操作](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json)。 支持仅限于 `openURL`：单击时，用户将被重定向到新标签页中的指定 URL。

使用 [Microsoft Teams 开发人员社区频道](/microsoftteams/platform/feedback)报告问题并提供反馈。

### <a name="debugging"></a>调试

在测试邮件扩展时，可以通过 [Activity](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md) 对象的 [channelId](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) 识别机器人请求的来源（来自 Teams 与 Outlook）。 当用户执行查询时，服务会收到一个标准 Bot Framework `Activity` 对象。 Activity 对象中的一个属性是 `channelId`，其值为 `msteams` 或 `outlook`，具体取决于机器人请求的来源。 有关详细信息，请参阅[基于搜索的邮件扩展 SDK](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions)。

## <a name="code-sample"></a>代码示例

| **示例名称** | **说明** | **Node.js** |
|---------------|--------------|--------|
| NPM 搜索连接器 | 使用 Teams 工具包构建邮件扩展应用。 在 Teams、Outlook 中工作。 |  [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/NPM-search-connector-M365) |

## <a name="next-step"></a>后续步骤

发布应用以便在 Teams、Outlook 和 Office 中可以发现：

> [!div class="nextstepaction"]
> [发布适用于 Outlook 和 Office 的 Teams 应用](publish.md)
