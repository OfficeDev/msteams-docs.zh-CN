---
title: 跨 Microsoft 365 扩展 Teams 个人选项卡应用
description: 跨 Microsoft 365 扩展 Teams 个人选项卡应用
ms.date: 02/11/2022
ms.topic: tutorial
ms.custom: Microsoft 365 apps
ms.localizationpriority: high
ms.openlocfilehash: 873a6fa6207d122581e18cef0ae922ffca87762f
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111519"
---
# <a name="extend-a-teams-personal-tab-across-microsoft-365"></a>跨 Microsoft 365 扩展 Teams 个人选项卡

> [!NOTE]
> *跨 Microsoft 365 扩展 Teams 个人选项卡* 目前仅在 [ 公共开发人员预览](../resources/dev-preview/developer-preview-intro.md) 版中可用。 预览版中包含的功能可能不完整，并且在公开发布之前可能会发生更改。 它们仅用于测试和探索目的。 不应在生产应用程序中使用它们。

个人选项卡提供了增强 Microsoft Teams 体验的好方法。 使用个人选项卡，可以在 Teams 中提供用户对其应用程序的访问权限，无需用户离开体验或再次登录。 使用此预览版，个人选项卡可以在其他 Microsoft 365 应用程序中亮起。 本教程演示了使用现有 Teams 个人选项卡、并将其更新用于在桌面和网页版 Outlook 以及 Office 网页版 (office.com) 体验中运行的过程。

更新个人应用以在 Outlook 和 Office 主页中运行涉及以下步骤：

> [!div class="checklist"]
>
> * 更新应用清单
> * 更新 TeamsJS SDK 引用
> * 修改内容安全策略标题
> * 更新 Microsoft Azure Active Directory (Azure AD) 单一登录应用注册 (SSO)

测试应用需要执行以下步骤：

> [!div class="checklist"]
>
> * 在 *Office 365 目标版本* 中注册 Microsoft 365 租户
> * 配置帐户配置，以访问 Outlook 和 Office 应用的预览版本
> * 在 Teams 中旁加载更新后的应用

完成这些步骤后，Outlook 和 Office 应用的预览版本中应显示应用。

## <a name="prerequisites"></a>先决条件

完成本教程需要：

* Microsoft 365 开发人员计划沙盒租户
* 在 *Office 365 目标版本* 中注册的沙盒租户
* 从 Microsoft 365 应用 *beta 版通道* 安装了 Office 应用的计算机
* （可选）Microsoft Visual Studio Code 的 [ Teams 工具包 ](https://aka.ms/teams-toolkit) 扩展，用于帮助更新代码

> [!div class="nextstepaction"]
> [安装先决条件](prerequisites.md)

## <a name="prepare-your-personal-tab-for-the-upgrade"></a>准备好个人选项卡进行升级

如果已有个人选项卡应用，请创建生产项目的副本或分支以进行测试，并在应用清单中更新应用 ID，以使用新标识符（不同于生产应用 ID）。

若要使用示例代码完成本教程，请按照 [ 待办事项列表示例入门 ](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend) 中的设置步骤，使用用于 Visual Studio Code 的 Teams 工具包扩展构建个人选项卡应用。 或者，可以从为 [ TeamsJS SDK v2 预览版 ](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend-M365) 更新的同一待办事项列表示例开始，然后继续 [ 在其他 Microsoft 365 体验中预览个人选项卡 ](#preview-your-personal-tab-in-other-microsoft-365-experiences)。 更新后的示例也可以在 Teams 工具包扩展中使用：“*开发*” > “*查看示例*” > “**待办事项列表（在 Teams、Outlook 和 Office 中工作）**。

:::image type="content" source="images/toolkit-todo-sample.png" alt-text=" Teams 工具包中的待办事项列表示例（Teams、Outlook 和 Office 中的工作）":::

## <a name="update-the-app-manifest"></a>更新应用清单

需要使用 [ Teams 开发人员预览清单 ](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview) 架构和 `Microsoft 365 DevPreview` 清单版本，使 Teams 个人选项卡能够在 Office 和 Outlook 中运行。

可以使用 Teams 工具包更新应用清单，也可以手动应用更改：

# <a name="teams-toolkit"></a>[Teams 工具包](#tab/manifest-teams-toolkit)

1. 打开 *命令面板*：`Ctrl+Shift+P`
1. 运行该 `Teams: Upgrade Teams manifest to support Outlook and Office apps` 命令并选择应用清单文件。 将进行更改。

# <a name="manual-steps"></a>[ 手动步骤 ](#tab/manifest-manual)

打开 Teams 应用清单，使用以下值更新 `$schema` 和 `manifestVersion`：

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```

---

如果使用 Teams 工具包创建了个人应用，则还可以使用它来验证清单文件的更改并识别任何错误。 打开命令面板 `Ctrl+Shift+P` 并找到“**Teams：验证清单文件**”，或者从 Teams 工具包的“部署”菜单中选择选项（查找 Visual Studio Code 左侧的 Teams 图标）。

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text=" Teams 工具包“部署”菜单下的“验证清单文件”选项":::

## <a name="update-sdk-references"></a>更新 SDK 引用

若要在 Outlook 和 Office 中运行，应用将需要依赖于 npm 包`@microsoft/teams-js@2.0.0-beta.1`（或更高的 *beta* 版本）。 虽然 Outlook 和 Office 支持低版本 `@microsoft/teams-js` 的代码，但是会记录弃用警告，并且 Outlook 和 Office 最终将会停止对低版本的 `@microsoft/teams-js` 支持。

可以使用 Teams 工具包帮助自动执行一些代码更改，以采用下一版本 `@microsoft/teams-js`，但如果要手动执行这些步骤，请参阅 [ Microsoft Teams JavaScript 客户端 SDK 预览版 ](using-teams-client-sdk-preview.md)，了解详细信息。

1. 打开 *命令面板*：`Ctrl+Shift+P`
1. 运行命令 `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`。

完成后，实用工具将使用 TeamsJS SDK 预览版（`@microsoft/teams-js@2.0.0-beta.1` 或更高版本）依赖项更新 `package.json` 文件，`*.js/.ts` 和 `*.jsx/.tsx` 文件将更新为：

> [!div class="checklist"]
>
> * `package.json` 对 TeamsJS SDK 预览版的引用
> * TeamsJS SDK 预览版的导入语句
> * 对 TeamsJS SDK 预览版的 [ 函数、枚举和接口调用 ](using-teams-client-sdk-preview.md#apis-organized-into-capabilities)
> * `TODO` 注释提醒，查看可能受 [ 上下文 ](using-teams-client-sdk-preview.md#updates-to-the-context-interface) 接口更改影响的区域
> * `TODO` 注释提醒，确保 [ 从回调样式函数转换为 promise 函数 ](using-teams-client-sdk-preview.md#callbacks-converted-to-promises) 在该工具找到的每个调用站点上运行良好

> [!IMPORTANT]
> 升级工具不支持 *.html* 文件中的代码，需要手动更改。

> [!NOTE]
> 若要手动更新代码，请参阅 [ Microsoft Teams JavaScript 客户端 SDK 预览版 ](using-teams-client-sdk-preview.md)，了解所需的更改。

## <a name="configure-content-security-policy-headers"></a>配置内容安全策略标题

[ 正如在 Microsoft Teams 中一样 ](/microsoftteams/platform/tabs/what-are-tabs)，选项卡应用程序托管在Office 和 Outlook 网页版客户端的（[ iframe 元素 ](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe)）中。

如果应用使用 [ 内容安全策略 ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) 标题，请确保在 CSP 标题中允许以下所有的 [ 框架上级元素 ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors)：

|Microsoft 365 主机| 框架上级元素权限|
|--|--|
| Teams | `teams.microsoft.com` |
| Office | `*.office.com` |
| Outlook | `outlook.office.com`, `outlook.office365.com`, `outlook-sdf.office.com`, `outlook-sdf.office365.com` |

## <a name="update-azure-ad-app-registration-for-sso"></a>更新 SSO 的 Azure AD 应用注册

个人选项卡的 Azure Active Directory 单一登录 (SSO) 在 Outlook [ 中的工作方式与在 Teams](/microsoftteams/platform/tabs/how-to/authentication/auth-aad-sso) 中的工作方式相同，但是需要在租户的 *应用注册* 门户中，将多个客户端应用程序标识符添加到选项卡应用的 Azure AD 应用注册。

1. 使用沙盒租户帐户登录到 [Microsoft Azure 门户 ](https://portal.azure.com)。
1. 打开 **应用注册** 边栏选项卡。
1. 选择个人选项卡应用程序的名称以打开其应用注册。
1. 在“*管理*”下选择“**公开 API**”。

:::image type="content" source="images/azure-app-registration-clients.png" alt-text=" 从 Azure 门户上的 *应用注册* 边栏选项卡授权客户端 ID ":::

在”**授权客户端应用程序**“部分中，确保添加了以下 `Client Id` 所有值：

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

最后一步是在 Microsoft Teams 中旁加载更新的个人选项卡（[ 应用包 ](/microsoftteams/platform/concepts/build-and-test/apps-package)）。 完成后，除了在 Teams 中，应用还可以在 Office 和 Outlook 中运行。

1. 将 Teams 应用程序（清单和应用 [ 图标 ](/microsoftteams/platform/resources/schema/manifest-schema#icons)）打包为一个 zip 文件。 如果使用 Teams 工具包创建了应用，则可以在 Teams 工具包的“*部署*”菜单或 Visual Studio Code 的命令面板 `Ctrl+Shift+P` 中使用 **压缩 Teams 元数据包** 选项轻松执行此操作：

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="适用于 Visual Studio Code 的 Teams 工具包扩展中的“压缩 Teams 元数据包”选项":::

1. 使用沙盒租户帐户登录 Teams，并确保处于公共开发人员预览版。 可以通过单击用户配置文件的省略号 (**...**) 菜单并打开“**关于**”，检查 *开发人员预览* 选项是否处于已开启状态，以此来验证是否在使用 Teams 客户端预览版。

    :::image type="content" source="images/teams-dev-preview.png" alt-text=" 从 Teams 省略号菜单中打开“关于”，并验证是否选中了“开发人员预览版”选项 ":::

1. 打开“*应用*”窗格，单击“**上传自定义应用**”和“**为我或我的团队上传**”。

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text=" Teams“应用”窗格中的“上传自定义应用”按钮 ":::

1. 选择应用包，然后单击“*打开*”。

通过 Teams 进行旁加载后，个人选项卡将可以在 Outlook 和 Office 中使用。 请务必使用与在 Teams 中旁加载应用时相同的凭据登录。

可以固定应用以进行快速访问，也可以在省略号 (**...**) 中找到应用左侧边栏中最近应用程序中的浮出控件。

> [!NOTE]
> 将应用固定在 Teams 中不会将其固定为 Office.com 或 Outlook 中的应用。

## <a name="preview-your-personal-tab-in-other-microsoft-365-experiences"></a>在其他 Microsoft 365 体验中预览个人选项卡

升级 Teams 个人选项卡并将其旁加载到 Teams 中时，它可以在Windows 和网页版本的 Outlook、Windows 和网页版本的 Office (office.com) 中运行。 下面介绍如何从 Microsoft 365 体验中预览它。

### <a name="outlook-on-windows"></a>Windows 版 Outlook

若要在 Windows 桌面上查看在 Outlook 中运行的应用：

1. 启动 Outlook 并使用开发租户帐户登录。
1. 单击侧边栏上的省略号 (**...**)。 旁加载的应用标题将显示在已安装的应用中。
1. 单击应用图标，在 Outlook 中启动应用。

:::image type="content" source="images/outlook-desktop-more-apps.png" alt-text=" 单击 Outlook 桌面客户端侧边栏上的省略号（“更多应用”）选项，查看已安装的个人选项卡 ":::

### <a name="outlook-on-the-web"></a>Outlook 网页版

若要查看 Outlook 网页版中的应用，请执行以下操作：

1. 导航到 [ Outlook 网页版 ](https://outlook.office.com) 并使用开发租户帐户登录。
1. 单击侧边栏上的省略号 (**...**)。 旁加载的应用标题将显示在已安装的应用中。
1. 单击应用图标，启动并预览在Outlook 网页版中运行的应用。

:::image type="content" source="images/outlook-web-more-apps.png" alt-text=" 单击 outlook.com 侧边栏上的省略号（“更多应用”）选项，查看已安装的个人选项卡 ":::

### <a name="office-on-windows"></a>Windows 版 Office

若要在 Windows 桌面上查看在 Office 中运行的应用，请执行以下操作：

1. 启动 Office 并使用开发租户帐户登录。
1. 单击侧边栏上的省略号 (**...**)。 旁加载的应用标题将显示在已安装的应用中。
1. 单击应用图标，在 Office 中启动应用。

:::image type="content" source="images/office-desktop-more-apps.png" alt-text=" 单击 Office 桌面客户端侧边栏上的省略号（“更多应用”）选项，查看已安装的个人选项卡 ":::

### <a name="office-on-the-web"></a>Office 网页版

若要预览在 Office 网页版中运行的应用，请执行以下操作：

1. 使用测试租户凭据登录到 office.com。
1. 单击侧边栏上的省略号 (**...**)。 旁加载的应用标题将显示在已安装的应用中。
1. 单击应用图标，在 Office 网页版中启动应用。

:::image type="content" source="images/office-web-more-apps.png" alt-text=" 单击 office.com 侧边栏上的省略号（“更多应用”）选项，查看已安装的个人选项卡 ":::

## <a name="next-steps"></a>后续步骤

启用 Outlook 和 Office 的个人选项卡处于预览状态，不支持生产使用。 下面介绍如何将个人选项卡应用分发给预览版受众以进行测试。

### <a name="single-tenant-distribution"></a>单租户分发

启用 Outlook 和 Office 的个人选项卡可以通过以下三种方式之一跨测试（或生产）租户分发给预览版受众：

#### <a name="teams-client"></a>Teams 客户端

在“*应用*”菜单中，选择“*管理应用*” > “**将应用提交到组织**”。这需要 IT 管理员的批准。

#### <a name="microsoft-teams-admin-center"></a>Microsoft Teams 管理中心

作为 Teams 管理员，可以从 [ Teams 管理中心 ](https://admin.teams.microsoft.com/) 为组织的租户上传和预安装应用包。有关详细信息，请参阅 [ 在 Microsoft Teams 管理中心上传自定义应用 ](/MicrosoftTeams/upload-custom-apps)。

#### <a name="microsoft-admin-center"></a>Microsoft 管理中心

作为全局管理员，可以从 [ Microsoft 管理中心 ](https://admin.microsoft.com/) 上传和预安装应用包。有关详细信息，请参阅 [ 合作伙伴在集成应用门户中测试和部署 Microsoft 365 应用 ](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps)。

### <a name="multitenant-distribution"></a>多租户分布

在启用了 Outlook 和 Office 的 Teams 个人选项卡的早期开发人员预览版中，尚不支持分发到 Microsoft AppSource。
