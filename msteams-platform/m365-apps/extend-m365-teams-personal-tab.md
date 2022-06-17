---
title: 跨 Microsoft 365 扩展 Teams 个人选项卡应用
description: 跨 Microsoft 365 扩展 Teams 个人选项卡应用
ms.date: 05/24/2022
ms.topic: tutorial
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 957ad3e30ffc2a798f5737e031339fd2e5ebc21b
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144073"
---
# <a name="extend-a-teams-personal-tab-across-microsoft-365"></a>跨 Microsoft 365 扩展 Teams 个人选项卡

个人选项卡提供了增强 Microsoft Teams 体验的好方法。 使用个人选项卡，可以在 Teams 中提供用户对其应用程序的访问权限，无需用户离开体验或再次登录。 使用此预览版，个人选项卡可以在其他 Microsoft 365 应用程序中亮起。 本教程演示了使用现有 Teams 个人选项卡、并将其更新用于在桌面和网页版 Outlook 以及 Office 网页版 (office.com) 体验中运行的过程。

将个人应用更新为在Outlook和Office中运行涉及以下步骤：

> [!div class="checklist"]
>
> * 更新应用清单。
> * 更新 TeamsJS SDK 引用。
> * 修改内容安全策略标头。
> * 更新 Microsoft Azure Active Directory (Azure AD) 单一登录应用注册 (SSO) 。
> * 在Teams中旁加载更新后的应用。

本指南的其余部分将指导你完成这些步骤，并演示如何在其他Microsoft 365应用程序中预览个人选项卡。

## <a name="prerequisites"></a>先决条件

完成本教程需要：

* Microsoft 365 开发人员计划沙盒租户
* 在 *Office 365 目标版本* 中注册的沙盒租户
* 从 Microsoft 365 应用 *beta 版通道* 安装了 Office 应用的计算机
* （可选）Microsoft Visual Studio Code 的 [ Teams 工具包 ](https://aka.ms/teams-toolkit) 扩展，用于帮助更新代码

> [!div class="nextstepaction"]
> [安装先决条件](prerequisites.md)

## <a name="prepare-your-personal-tab-for-the-upgrade"></a>准备好个人选项卡进行升级

如果你有一个现有的个人选项卡应用，请创建生产项目的副本或分支，用于测试和更新应用清单中的应用 ID，以使用与生产应用 ID 不同的新标识符 (用于测试) 。

如果要使用示例代码完成本教程，请按照 [Todo 列表示例](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend)中的设置步骤，使用Visual Studio Code的Teams Toolkit扩展生成个人选项卡应用，然后返回到本文以将其更新为Microsoft 365。

或者，可以使用以下快速入门部分中已启用的基本单Sign-On *hello world* 应用Microsoft 365，然后跳到 [Teams中旁加载应用](#sideload-your-app-in-teams)。

### <a name="quickstart"></a>快速入门

若要从已启用在Outlook和Office中运行[的个人选项卡](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend-M365)开始，请对Visual Studio Code使用Teams Toolkit扩展。

1. 从 Visual Studio Code 打开命令面板 (`Ctrl+Shift+P`)，键入 `Teams: Create a new Teams app`。
1. 选择 **启用了 SSO 的个人选项卡**。

    :::image type="content" source="images/toolkit-tab-sample.png" alt-text=" Teams 工具包中的待办事项列表示例（Teams、Outlook 和 Office 中的工作）":::

1. 在本地计算机上为工作区文件夹选择一个位置。
1. 打开命令面板 () `Ctrl+Shift+P` 并键入`Teams: Provision in the cloud`，在 Azure 帐户中创建所需的应用资源 (App 服务计划、存储帐户、函数应用、托管标识) 。
1. 打开命令面板（`Ctrl+Shift+P`）并键入 `Teams: Deploy to the cloud`，将示例代码部署到 Azure 中预配的资源并启动应用。

从此处，你可以跳到[Teams中旁加载应用](#sideload-your-app-in-teams)，并在Outlook和Office中预览应用。  (应用清单和 TeamsJS API 调用已更新为 Microsoft 365.) 

## <a name="update-the-app-manifest"></a>更新应用清单

需要使用[Teams开发人员清单](../resources/schema/manifest-schema.md)架构版本`1.13`，使Teams个人选项卡能够在Outlook和Office中运行。

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

如果使用 Teams 工具包创建了个人应用，则还可以使用它来验证清单文件的更改并识别任何错误。 打开命令面板 () `Ctrl+Shift+P` 并找到 **Teams：验证清单文件**。

## <a name="update-sdk-references"></a>更新 SDK 引用

若要在Outlook和Office中运行，应用需要引用npm包`@microsoft/teams-js@2.0.0` (或更高) 。 虽然Outlook和Office支持具有下层版本的代码，但会记录弃用警告，并且Outlook和Office中对 TeamsJS 的下层版本的支持最终将停止。

可以使用Teams Toolkit来帮助识别和自动化从 1.x TeamsJS 版本升级到 TeamsJS 版本 2.0.0 所需的代码更改。 或者，可以手动执行相同的步骤;有关详细信息，请参阅 [Microsoft Teams JavaScript 客户端 SDK](../tabs/how-to/using-teams-client-sdk.md#whats-new-in-teamsjs-version-20)。

1. 打开 *命令面板*： `Ctrl+Shift+P`.
1. 运行命令 `Teams: Upgrade Teams JS SDK and code references`。

完成后， *package.json* 文件将引用 `@microsoft/teams-js@2.0.0` (或更高) ，并且你的 `*.js/.ts` 和 `*.jsx/.tsx` 文件将使用以下内容进行更新：

> [!div class="checklist"]
>
> * teams-js@2.0.0 的导入语句
> * teams-js@2.0.0 的函数[、枚举和接口调](../tabs/how-to/using-teams-client-sdk.md#whats-new-in-teamsjs-version-20)用
> * `TODO` 注释提醒标记可能受 [上下文](../tabs/how-to/using-teams-client-sdk.md#updates-to-the-context-interface) 接口更改影响的区域
> * `TODO` 注释提醒，[将回调函数转换为 promise](../tabs/how-to/using-teams-client-sdk.md#callbacks-converted-to-promises)

> [!IMPORTANT]
> 升级工具不支持 *.html* 文件中的代码，需要手动更改。

## <a name="configure-content-security-policy-headers"></a>配置内容安全策略标题

与Microsoft Teams一样，选项卡应用程序托管在Office和Outlook Web 客户端的 [iframe 元素](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe)中。

如果应用使用[内容安全](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy)策略 (云解决方案提供商) 标头，请确保在云解决方案提供商标头中允许以下所有[帧上级](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors)：

|Microsoft 365 主机| 框架上级元素权限|
|--|--|
| Teams | `teams.microsoft.com` |
| Office | `*.office.com` |
| Outlook | `outlook.office.com`, `outlook.office365.com`, `outlook-sdf.office.com`, `outlook-sdf.office365.com` |

## <a name="update-azure-ad-app-registration-for-sso"></a>更新 SSO 的 Azure AD 应用注册

[Azure Active Directory (AD) 单一登录 (个人选项卡的 SSO) ](../tabs/how-to/authentication/tab-sso-overview.md)在Office和Outlook中的工作方式与在Teams中的工作方式相同。 但是，需要将多个客户端应用程序标识符添加到租户 *应用注册* 门户中 Tab 应用的 Azure AD 应用注册。

1. 使用沙盒租户帐户登录到 [Microsoft Azure 门户 ](https://portal.azure.com)。
1. 打开 **应用注册** 边栏选项卡。
1. 选择个人选项卡应用程序的名称以打开其应用注册。
1. 在“*管理*”下选择“**公开 API**”。

    :::image type="content" source="images/azure-app-registration-clients.png" alt-text=" 从 Azure 门户上的 *应用注册* 边栏选项卡授权客户端 ID ":::

1. 在”**授权客户端应用程序**“部分中，确保添加了以下 `Client Id` 所有值：

    |Microsoft 365 客户端应用程序 | 客户端 ID |
    |--|--|
    |Teams 桌面、移动设备 |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
    |Teams Web |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
    |Office.com  |4765445b-32c6-49b0-83e6-1d93765276ca|
    |Office 桌面版  | 0ec893e0-5785-4de6-99da-4ed124e5296c |
    |Outlook 桌面版 | d3590ed6-52b3-4102-aeff-aad2292ab01c |
    |Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
    |Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-app-in-teams"></a>在 Teams 中旁加载应用

在Office和Outlook中运行应用的最后一步是在Microsoft Teams中旁加载更新的个人选项卡[应用包](..//concepts/build-and-test/apps-package.md)。

1. 将Teams应用程序 ([清单](../resources/schema/manifest-schema.md)和[应用图标](/microsoftteams/platform/resources/schema/manifest-schema#icons)打包) zip 文件中。 如果使用 Teams 工具包创建应用，则可以使用 Teams 工具包的“**部署**”菜单中的“**压缩 Teams 元数据包**”选项轻松完成此操作。

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="适用于 Visual Studio Code 的 Teams 工具包扩展中的“压缩 Teams 元数据包”选项":::

1. 使用沙盒租户帐户登录 Teams，并切换到“*开发者预览版*”模式。 选择用户个人资料旁边的省略号 (**...**) 菜单，然后依次选择：“**关于**” > “**开发者预览版**”。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="从 Teams 省略号菜单中，打开“关于”，然后选择“开发者预览版”选项":::

1. 选择“**应用**”以打开“**管理你的应用**”窗格。 然后选择“**发布应用**”。

    :::image type="content" source="images/teams-manage-your-apps.png" alt-text="打开“管理应用”窗格，然后选择“发布应用”":::

1. 选择 **Upload自定义应用** 选项，然后选择应用包。

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Teams 中的“上传自定义应用”选项":::

旁加载到Teams后，个人选项卡在Outlook和Office中可用。 请务必使用用于登录Teams来旁加载应用的相同凭据登录。

可以固定应用以进行快速访问，也可以在省略号 (**...**) 中找到应用左侧边栏中最近应用程序中的浮出控件。 将应用固定在Teams不会将其固定为Office或Outlook中的应用。

## <a name="preview-your-personal-tab-in-other-microsoft-365-experiences"></a>在其他 Microsoft 365 体验中预览个人选项卡

下面介绍如何预览在Office和Outlook、Web 和Windows桌面客户端中运行的应用。

> [!NOTE]
> 从Teams卸载应用还会将其从Outlook和Office的 **“更多应用**”目录中删除。 如果使用的是上面提供的Teams Toolkit示例应用。

### <a name="outlook-on-windows"></a>Windows 版 Outlook

若要在 Windows 桌面上查看在 Outlook 中运行的应用：

1. 启动 Outlook 并使用开发租户帐户登录。
1. 在侧栏上，选择  **“更多应用**”。 旁加载的应用标题显示在已安装的应用中。
1. 选择应用图标以在Outlook中启动应用。

    :::image type="content" source="images/outlook-desktop-more-apps.png" alt-text=" 单击 Outlook 桌面客户端侧边栏上的省略号（“更多应用”）选项，查看已安装的个人选项卡 ":::

### <a name="outlook-on-the-web"></a>Outlook 网页版

若要查看 Outlook 网页版中的应用，请执行以下操作：

1. 导航到 [ Outlook 网页版 ](https://outlook.office.com) 并使用开发租户帐户登录。
1. 选择侧栏上的省略号 (**...**) 。 旁加载的应用标题显示在已安装的应用中。
1. 选择应用图标以启动和预览在Outlook 网页版中运行的应用。

    :::image type="content" source="images/outlook-web-more-apps.png" alt-text=" 单击 outlook.com 侧边栏上的省略号（“更多应用”）选项，查看已安装的个人选项卡 ":::

### <a name="office-on-windows"></a>Windows 版 Office

若要在 Windows 桌面上查看在 Office 中运行的应用，请执行以下操作：

1. 启动 Office 并使用开发租户帐户登录。
1. 选择侧栏上的省略号 (**...**) 。 旁加载的应用标题显示在已安装的应用中。
1. 选择应用图标以在Office中启动应用。

    :::image type="content" source="images/office-desktop-more-apps.png" alt-text=" 单击 Office 桌面客户端侧边栏上的省略号（“更多应用”）选项，查看已安装的个人选项卡 ":::

### <a name="office-on-the-web"></a>Office 网页版

若要预览在 Office 网页版中运行的应用，请执行以下操作：

1. 使用测试租户凭据登录 **到 office.com** 。
1. 选择侧栏上的 **“应用** ”图标。 旁加载的应用标题显示在已安装的应用中。
1. 选择应用图标以在Office web 版中启动应用。

    :::image type="content" source="images/office-web-more-apps.png" alt-text="单击 office.com 侧栏上的“更多应用”选项，查看已安装的个人选项卡":::

## <a name="troubleshooting"></a>疑难解答

目前，Outlook和Office客户端支持一部分Teams应用程序类型和功能。 此支持随时间推移而扩展。

请参阅[Microsoft 365支持](../tabs/how-to/using-teams-client-sdk.md#microsoft-365-support-running-teams-apps-in-office-and-outlook)来检查主机对各种 TeamsJS 功能的支持。

有关Microsoft 365主机和平台对Teams应用的支持的总体摘要，请[参阅跨Microsoft 365扩展Teams应用](overview.md)。

可以通过调用该功能上的函数 (命名空间) ，并根据需要调整应用行为，在运行时 `isSupported()` 检查给定功能的主机支持。 这样，应用就可以在支持它的主机中点亮 UI 和功能，并在不支持的主机上提供正常回退体验。 有关详细信息，请参阅 [“区分应用体验](../tabs/how-to/using-teams-client-sdk.md#differentiate-your-app-experience)”。

使用 [Microsoft Teams 开发人员社区频道](/microsoftteams/platform/feedback)报告问题并提供反馈。

### <a name="debugging"></a>调试

从Teams Toolkit，除了Teams，还可以调试 (`F5`) 在Office和Outlook中运行的选项卡应用程序。

:::image type="content" source="images/toolkit-debug-targets.png" alt-text="从Teams、Outlook和Office调试目标中选择Teams Toolkit":::

首次运行本地调试以Office或Outlook时，系统会提示你登录到Microsoft 365租户帐户并安装自签名测试证书。 系统还会提示你手动安装Teams。 选择 **“安装Teams** 打开浏览器窗口并手动安装应用。 然后单击“**继续**”，在Office/Outlook中继续调试应用。

:::image type="content" source="images/toolkit-dialog-teams-install.png" alt-text="Teams安装Toolkit对话框":::

在 [Microsoft Teams Framework (TeamsFx ](https://github.com/OfficeDev/TeamsFx/issues)) 中提供反馈并报告Teams Toolkit调试体验的任何问题。

## <a name="code-sample"></a>代码示例

| **示例名称** | **说明** | **Node.js** |
|---------------|--------------|--------|
| 待办事项列表 | 使用React和Azure Functions生成的 SSO 的可编辑待办事项列表。 仅适用于Teams (使用此示例应用来尝试本教程) 中所述的升级过程。 | [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend)  |
| 待办事项列表 (Microsoft 365)  | 使用React和Azure Functions生成的 SSO 的可编辑待办事项列表。 在Teams、Outlook、Office中工作。 | [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend-M365)|
| 图像编辑器 (Microsoft 365)  | 使用 Microsoft 图形 API 创建、编辑、打开和保存映像。 在Teams、Outlook、Office中工作。 | [View](https://github.com/OfficeDev/m365-extensibility-image-editor) |

## <a name="next-step"></a>后续步骤

发布应用以便在 Teams、Outlook 和 Office 中可以发现：

> [!div class="nextstepaction"]
> [发布适用于 Outlook 和 Office 的 Teams 应用](publish.md)
