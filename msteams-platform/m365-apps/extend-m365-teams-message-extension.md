---
title: 跨Teams扩展邮件Microsoft 365
description: 下面将了解如何更新基于搜索Teams邮件扩展以在 Outlook
ms.date: 11/15/2021
ms.topic: tutorial
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 7ff02efe553d4b91c81ea184ae2b6b67b8464042
ms.sourcegitcommit: c65a868744e4108b5d786de2350981e3f1f05718
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2022
ms.locfileid: "62081120"
---
# <a name="extend-a-teams-message-extension-across-microsoft-365"></a>跨Teams扩展邮件Microsoft 365

> [!NOTE]
> *目前Teams开发人员预览版Microsoft 365* 跨应用程序扩展邮件 [扩展](../resources/dev-preview/developer-preview-intro.md)。 预览版中包含的功能可能不完整，并且在公开发布之前可能会发生更改。 它们仅用于测试和探索目的。 不应在生产应用程序中使用它们。

基于搜索[的邮件扩展](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions)允许用户搜索外部系统并通过客户端的撰写邮件区域共享Microsoft Teams结果。 通过跨 Microsoft 365 (预览) 扩展[Teams](overview.md)应用，现在可以将基于搜索的 Teams 邮件扩展引入 Outlook，从而Windows桌面和 Web 体验。

更新基于搜索的 Teams 邮件扩展以运行Outlook包括以下步骤：

> [!div class="checklist"]
> * 更新应用清单
> * 为自动Outlook添加频道
> * 在应用程序中旁加载更新Teams

本指南的其余部分将指导你完成这些步骤，并展示如何在桌面和 Web Outlook预览Windows扩展。

## <a name="prerequisites"></a>先决条件

若要完成本教程，你需要：

 - 开发人员Microsoft 365沙盒租户
 - 你的沙盒租户已注册 *Office 365定向版本*
 - 测试环境，Office beta 渠道安装Microsoft 365 应用版 *应用*
 - Visual Studio Code可选Teams Toolkit (预览)  (预览) 

> [!div class="nextstepaction"]
> [安装先决条件](prerequisites.md)

## <a name="prepare-your-messaging-extension-for-the-upgrade"></a>准备邮件扩展以用于升级

如果你有现有的消息传递扩展，请创建生产项目的副本或分支以在应用清单中测试并更新应用 ID，以使用与生产应用 ID (不同的新标识符) 。

如果你想要使用示例代码来完成本教程，请按照[Teams 邮件](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search)扩展搜索示例中的设置步骤快速生成基于Microsoft Teams的邮件扩展。 或者，你可以从为[TeamsJS SDK v2 预览](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2/NPM-search-connector-M365)版更新的相同 Teams 邮件扩展搜索示例开始，然后继续预览 Outlook 中的消息[扩展](#preview-your-message-extension-in-outlook)。 更新的示例还可用于以下扩展 *Teams Toolkit：开发*  >  *视图示例*  >  **NPM 搜索连接器**。

:::image type="content" source="images/toolkit-search-sample.png" alt-text="NPM Search Connector 示例Teams Toolkit":::

## <a name="update-the-app-manifest"></a>更新应用清单

你需要使用开发人员预览清单Teams和[](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview)清单版本，以使你的 Teams 邮件扩展在 Outlook `m365DevPreview` 中运行。

有两个选项用于更新应用清单：

# <a name="teams-toolkit"></a>[Teams Toolkit](#tab/manifest-teams-toolkit)

1. 打开命令 *调色板*： `Ctrl+Shift+P`
1. 运行 `Teams: Upgrade Teams manifest to support Outlook and Office apps` 命令并选择应用清单文件。 将就地进行更改。

# <a name="manual-steps"></a>[手动步骤](#tab/manifest-manual)

打开Teams应用清单，然后使用 `$schema` `manifestVersion` 下列值更新 和 ：

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```
---

如果使用 Teams Toolkit创建邮件扩展应用，可以使用它验证对清单文件所做的更改并识别任何错误。 打开命令调色板并找到"Teams：验证清单文件"，或者从 Teams Toolkit (的"部署"菜单中选择选项，查找 Teams 图标位于 Visual Studio Code) 左侧 `Ctrl+Shift+P` 。 

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams Toolkit&quot;部署&quot;菜单下的&quot;验证清单文件&quot;选项":::

## <a name="add-an-outlook-channel-for-your-bot"></a>为自动Outlook添加频道

在Microsoft Teams中，消息传递扩展由您托管的 Web 服务和定义 Web 服务的托管位置的应用程序清单组成。 Web 服务利用 Bot [Framework SDK](/azure/bot-service/bot-service-overview)消息传递架构，并通过为自动程序注册Teams安全通信协议。

若要让用户从 Outlook与消息扩展进行交互，你需要将Outlook添加到自动程序：

1. 从 [Azure 门户](https://portal.azure.com) (或 Bot [Framework](https://dev.botframework.com) 门户（如果你之前已注册) ）导航到自动程序资源。

1. From *设置，* select **Channels**.

1. 单击 **"Outlook"，** 选择"**邮件扩展"** 选项卡，然后单击"保存 **"。**

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="从 Azure Outlook&quot;频道&quot;窗格中为机器人添加&quot;消息扩展&quot;频道":::

1. 确认你的Outlook频道已与Microsoft Teams频道 **窗格中的频道** 一起列出：

    :::image type="content" source="images/azure-bot-channels.png" alt-text="Azure 自动程序频道窗格，Microsoft Teams和Outlook频道":::

## <a name="sideload-your-updated-messaging-extension-in-teams"></a>在客户端中旁加载更新的邮件Teams

最后一步是将更新的邮件扩展旁加载 ([程序包](/microsoftteams/platform/concepts/build-and-test/apps-package)) 应用程序Microsoft Teams。 完成后，邮件扩展将出现在从撰写邮件 *区域安装的"* 应用"中。

1. 将你的Teams打包 (清单和应用[图标](/microsoftteams/platform/resources/schema/manifest-schema#icons)) zip 文件中。 如果你使用Teams Toolkit创建应用，可以使用以下项的"部署"菜单中的 **Zip Teams 元数据** 包选项轻松Teams Toolkit： 

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Teams扩展中的&quot;Zip Teams元数据包&quot;Teams Toolkit&quot;Visual Studio Code":::

1. 使用沙盒租户帐户登录 Teams，然后通过按用户配置文件单击省略号" ( **...**) "菜单并打开"关于"来检查"开发人员预览"选项是否处于打开状态，以验证你是否位于"公共 开发者预览版"上。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="从Teams省略号菜单，打开&quot;关于&quot;并确认&quot;开发者预览版&quot;选项已选中":::

1. 打开应用程序 *窗格*，然后单击Upload **自定义应用，Upload****或我的团队。**

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="&quot;Upload&quot;窗格中的&quot;Teams自定义应用&quot;按钮":::

1. 选择你的应用包，*然后单击打开。*

通过旁加载Teams，你的消息传递扩展将在 Outlook 网页版。

## <a name="preview-your-message-extension-in-outlook"></a>在邮件中预览邮件Outlook

现在可以在桌面和 Web 上测试在 Outlook 中Windows消息扩展。 虽然更新后的邮件扩展将继续在 Teams 中运行，并且具有对邮件[](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions)扩展的完整功能支持，但此已启用 Outlook 的体验的早期预览存在一些限制，请注意：

* 邮件撰写Outlook限于邮件撰写[上下文](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions)。 即使您的邮件Teams包括在其清单中作为上下文，当前预览仅限于邮件组合 () `commandBox`  `compose` 选项。 不支持从全局搜索Outlook *消息* 扩展。
* [Outlook](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS)不支持基于操作的消息扩展Outlook。 如果你的应用同时具有基于搜索和基于操作的命令，它将Outlook但操作菜单将不可用。
* [邮件扩展不支持](/microsoftteams/platform/messaging-extensions/how-to/enable-sso-auth-me)单一登录无提示Outlook。
* 不支持在电子邮件 [中插入](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design) 5 张以上自适应卡片;不支持自适应卡片 v1.4 及更高版本。
* [插入](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json) 的卡片不支持 、 、 和 `messageBack` `imBack` `invoke` `signin` 类型的卡片操作。 支持仅限于 `openURL` ：单击时，用户将被重定向到新选项卡中的指定 URL。

在测试邮件扩展时，可以通过[Activity](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md)对象的[channelId](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) (来自 Teams Outlook) 自动程序请求的源服务器。 当用户执行查询时，你的服务会收到标准 Bot Framework `Activity` 对象。 Activity 对象中的属性之一是 ，它的值将为 `channelId` 或 `msteams` `outlook` ，具体取决于自动程序请求的发起位置。 有关详细信息，请参阅[基于搜索的邮件扩展 SDK。](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions)

### <a name="outlook-on-the-web"></a>Outlook 网页版

若要预览在 Outlook 网页版 中运行的应用，outlook.com[使用测试](https://www.outlook.com)租户的凭据登录。 单击"**新建邮件"。** 打开 **合成窗口** 底部的"更多应用"弹出菜单。 将列出你的邮件扩展名。 你可以从该调用调用并使用它，就像在邮件中撰写Teams。

:::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="单击邮件组合窗口底部的&quot;更多应用&quot;outlook.com 开始使用邮件扩展。":::

### <a name="outlook"></a>Outlook

> [!IMPORTANT]
> 请参阅 Microsoft Teams - Microsoft 365[开发人员](https://devblogs.microsoft.com/microsoft365dev/)博客上的最新更新，以检查 Outlook for Windows desktop support for Teams message extensions 是否可用于测试租户。

若要预览在桌面Outlook Windows中运行的应用，Outlook使用测试租户的凭据登录。 单击"**新建电子邮件"。** 打开 **顶部功能区** 上的"更多应用"弹出菜单。 将列出你的邮件扩展名。 你可以从该调用调用并使用它，就像在邮件中撰写Teams。

## <a name="next-steps"></a>后续步骤

Outlook启用Teams邮件扩展是预览版，不支持用于生产用途。 下面将了解如何分配启用Outlook邮件扩展，以预览访问群体以进行测试。

### <a name="single-tenant-distribution"></a>单租户分布

Outlook和Office个人选项卡可通过以下三种方式之一跨测试 (或生产) 租户分发给预览受众：

#### <a name="teams-client"></a>Teams客户端

From the *Apps* menu， select *Manage your apps* Submit an app to your  >  **org**.这需要 IT 管理员批准。

#### <a name="microsoft-teams-admin-center"></a>Microsoft Teams管理中心

作为Teams管理员，你可以从 上传并预安装组织租户的应用包 https://admin.teams.microsoft.com/ 。 有关详细信息[Upload管理中心Microsoft Teams自定义](/MicrosoftTeams/upload-custom-apps)应用。

#### <a name="microsoft-admin-center"></a>Microsoft 管理中心

作为全局管理员，你可以从 上传并预安装应用包 https://admin.microsoft.com/ 。 有关详细信息[，请参阅Microsoft 365 应用版应用门户中的测试](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps)并部署合作伙伴部署应用。

### <a name="multi-tenant-distribution"></a>多租户分布

在此早期开发人员预览期间，尚不支持分发到 Microsoft AppSource Outlook支持Teams扩展。
