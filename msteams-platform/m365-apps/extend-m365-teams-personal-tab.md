---
title: 跨Teams扩展个人选项卡Microsoft 365
description: 跨Teams扩展个人选项卡Microsoft 365
ms.date: 11/15/2021
ms.topic: tutorial
ms.openlocfilehash: 8dcdb04b995206af05430bfdfb7c27992c8cd781
ms.sourcegitcommit: f77750f2e60f63d1e2f66a96c169119683c66950
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2021
ms.locfileid: "60960294"
---
# <a name="extend-a-teams-personal-tab-across-microsoft-365"></a>跨Teams扩展个人选项卡Microsoft 365

> [!NOTE]
> *目前Teams开发人员预览* 版中Microsoft 365个人选项卡。 [](../resources/dev-preview/developer-preview-intro.md) 预览版中包含的功能可能不完整，在公开发布之前可能会发生更改。 它们仅供测试和探索使用。 它们不应在生产应用程序中使用。

个人选项卡提供了一种增强用户体验Microsoft Teams方式。 使用个人选项卡，你可以为用户提供对 Teams 应用程序的访问权限，而无需离开体验或重新登录。 借助此预览，个人选项卡可以在其他应用程序Microsoft 365显示。 本教程演示采用现有个人选项卡Teams更新它以在 Outlook 桌面和 Web 体验中运行的过程，以及使用 Microsoft Office Home (office.com) 。

更新个人应用以在 Outlook Office 主页中运行涉及以下步骤：

> [!div class="checklist"]
> * 更新应用清单
> * 更新 TeamsJS SDK 引用 
> * 修改内容安全策略标头
> * 为 SSO AAD单一登录 (应用) 

测试应用需要以下步骤：

> [!div class="checklist"]
> * 在目标版本中注册 *Office 365 M365 租户*
> * 配置帐户以访问预览版本的 Outlook 和 Office 应用
> * 将更新后的应用旁加载到Teams

执行这些步骤后，你的应用应显示在 Outlook 和 Office 预览版本中。

## <a name="prerequisites"></a>先决条件

若要完成本教程，你需要：

* 开发人员Microsoft 365沙盒租户
* 你的沙盒租户已注册 *Office 365定向版本*
* 从 Office beta 渠道安装 Microsoft 365 应用版 *应用的计算机*
*  (可选[) Teams Toolkit](https://aka.ms/teams-toolkit)扩展Visual Studio Code，以帮助更新代码

> [!div class="nextstepaction"]
> [安装先决条件](prerequisites.md)

## <a name="prepare-your-personal-tab-for-the-upgrade"></a>为升级准备个人选项卡

如果你有现有的个人选项卡应用，请制作生产项目的副本或分支，以在应用清单中测试并更新应用 ID，以使用与生产应用 ID (不同的新标识符) 。

若要使用示例代码完成本教程，请按照[Todo](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend)列表入门示例中的设置步骤，使用 Teams Toolkit for Visual Studio Code 扩展构建个人选项卡应用。 或者，你可以从为[TeamsJS SDK v2](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend-M365)预览版更新的相同"Todo 列表示例"开始，然后继续在其他"预览体验"中预览[Microsoft 365选项卡](#preview-your-personal-tab-in-other-microsoft-365-experiences)。 更新后的示例也可在 Teams Toolkit extension： *Development*  >  *View samples*  >  **Todo List (Works in Teams， Outlook and Office)**。

:::image type="content" source="images/toolkit-todo-sample.png" alt-text="{alt-text}":::


## <a name="update-the-app-manifest"></a>更新应用清单

你需要使用开发人员预览清单架构Teams[](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview)清单版本，以使 Teams 个人选项卡在 Office `m365DevPreview` 和 Outlook 中运行。

可以使用以下Teams Toolkit更新应用清单，也可以手动应用更改：

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

如果你使用Teams Toolkit创建个人应用，则还可以使用它来验证对清单文件所做的更改并识别任何错误。 打开命令调色板并找到"Teams：验证清单文件"，或从 Teams Toolkit (的"部署"菜单中选择选项，查找 Teams 左侧的 `Ctrl+Shift+P` Visual Studio Code) 。 

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams Toolkit&quot;部署&quot;菜单下的&quot;验证清单文件&quot;选项":::

## <a name="update-sdk-references"></a>更新 SDK 引用

若要在 Outlook 和 Office 中运行，你的应用将需要依赖 npm 程序包 `@microsoft/teams-js@2.0.0-beta.1` 或更高版本。 尽管 Outlook 和 Office 中支持具有下层版本的代码，但弃用警告将被记录，并且对 Outlook 和 Office 中的下层版本的支持 `@microsoft/teams-js` 将最终 `@microsoft/teams-js` 停止。

可以使用 Teams Toolkit 自动执行某些代码更改以采用下一版本的 ，但如果你想要手动执行这些步骤，请参阅 `@microsoft/teams-js` [Microsoft Teams JavaScript 客户端 SDK 预览](using-teams-client-sdk-preview.md)版了解详细信息。

1. 打开命令 *调色板*： `Ctrl+Shift+P`
1. 运行命令 `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`

完成后，该实用工具会使用 TeamsJS SDK 预览版更新你的文件 () 依赖项，并且你的 和 `package.json` `@microsoft/teams-js@2.0.0-beta.1` `*.js/.ts` `*.jsx/.tsx` 文件将更新为：

> [!div class="checklist"]
> * `package.json` 对 TeamsJS SDK 预览版的引用
> * 导入 TeamsJS SDK 预览版语句
> * 对 TeamsJS SDK[预览版的函数](using-teams-client-sdk-preview.md#apis-organized-into-capabilities)、枚举和接口调用
> * `TODO` 注释提醒，用于查看可能受 [上下文接口更改](using-teams-client-sdk-preview.md#updates-to-the-context-interface) 影响的区域
> * `TODO` 注释提醒以确保 [从回调](using-teams-client-sdk-preview.md#callbacks-converted-to-promises) 样式函数转换到承诺函数在工具找到的所有调用网站中都运行良好

> [!IMPORTANT]
> 升级 *.html* 不支持文件内的代码，并且需要手动更改。

> [!NOTE]
> 如果你想要手动更新代码，请参阅 Microsoft Teams [JavaScript 客户端 SDK 预览](using-teams-client-sdk-preview.md)版，了解所需的更改。

## <a name="configure-content-security-policy-headers"></a>配置内容安全策略标头

[就像在 Microsoft Teams](/microsoftteams/platform/tabs/what-are-tabs)中一样，选项卡应用程序托管在 ([) ](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe)和 Office Outlook 元素中。

如果你的应用使用云解决方案提供商[](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) ，请确保你在 CSP 标头中允许以下所有帧[上级](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors)：

|Microsoft 365主机| 帧-上级权限|
|--|--|
| Teams | `teams.microsoft.com` |
| 办公室 | `*.office.com` |
| Outlook | `outlook.office.com`, `outlook.office365.com` |

## <a name="update-aad-app-registration-for-sso"></a>更新AAD SSO 的应用注册

Azure Active Directory 个人选项卡的 (SSO) 单一登录的工作方式在 Office 和 Outlook 中的工作方式与[Teams](/microsoftteams/platform/tabs/how-to/authentication/auth-aad-sso)相同，但是你需要在租户的应用注册门户中将多个客户端应用程序标识符添加到选项卡应用的 AAD 应用注册中。 

1. 使用沙盒 [租户](https://portal.azure.com) 帐户登录 Azure 门户。
1. 打开应用 **注册** 边栏选项卡。
1. 选择个人选项卡应用程序的名称以打开其应用注册。 
1. 选择 **"管理 ("***下的"公开* API) "。

:::image type="content" source="images/azure-app-registration-clients.png" alt-text="从 Azure 门户上的 *应用注册* 边栏选项卡授权客户端 ID":::

在" **授权客户端应用程序"** 部分，确保添加以下 `Client Id` 所有值：

|Microsoft 365客户端应用程序 | 客户端 ID |
|--|--|
|Teams桌面、移动 |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
|Teams Web |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
|Office.com  |4345a7b9-9a63-4910-a426-35363201d503|
|Office.com  |4765445b-32c6-49b0-83e6-1d93765276ca|
|Office桌面  | 0ec893e0-5785-4de6-99da-4ed124e5296c |
|Outlook 桌面版 | d3590ed6-52b3-4102-aeff-aad2292ab01c |
|Outlook Web Access | 00000002-0000-0ff1-ce00-0000000000000 |
|Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-app-in-teams"></a>在应用程序中旁加载Teams

最后一步是将更新的个人选项卡旁加载 ([程序包) ](/microsoftteams/platform/concepts/build-and-test/apps-package)中Microsoft Teams。 完成后，除了在 Teams 中，你的应用Office和 Outlook 中Teams。

1. 将你的Teams打包[ (清单和应用](/microsoftteams/platform/resources/schema/manifest-schema#icons)图标) 压缩文件中。 如果使用 Teams Toolkit 创建应用，可以使用 Teams Toolkit 的"部署"菜单中的 **Zip Teams** 元数据包选项或以下命令调色板 `Ctrl+Shift+P` Visual Studio Code：

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Teams Toolkit扩展中的&quot;zip Teams 元数据包&quot;Visual Studio Code":::

1. 登录以Teams沙盒租户帐户登录，并确保使用公共开发者预览版。 通过按用户配置文件单击省略号 (**...**) 菜单并打开"关于"来检查"开发人员预览"选项是否处于打开状态，可以验证你是否位于 Teams 客户端中的"预览"上。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="从Teams省略号菜单，打开&quot;关于&quot;并验证&quot;开发者预览版&quot;选项是否选中":::

1. 打开应用程序 *窗格*，然后单击Upload **自定义应用，Upload****或我的团队。**

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="&quot;Upload&quot;窗格中的&quot;Teams自定义应用&quot;按钮":::

1. 选择你的应用包，*然后单击打开。*

通过旁加载Teams，你的个人选项卡将在 Outlook 和 Office。 请务必使用用于在你的应用中旁加载应用的相同凭据Teams。

你可以固定应用以便快速访问，或者可以在左侧边栏中的省略号 (**...**) 最近应用程序之间找到你的应用。

> [!NOTE]
> 将应用固定到 Teams不会将其固定为 Office.com 或 Outlook 中的应用。

## <a name="preview-your-personal-tab-in-other-microsoft-365-experiences"></a>在其他体验中预览Microsoft 365选项卡

在升级你的 Teams 个人选项卡，Teams中旁加载它时，它还将在 Outlook 桌面和 Web 客户端以及 Microsoft Office Home (office.com) 中运行。 下面将了解如何从这些体验中预览Microsoft 365体验。

### <a name="outlook"></a>Outlook

若要查看在桌面Outlook中Windows的应用，Outlook开发人员租户帐户进行登录。 单击边栏上的 **()** 省略号..."。 旁加载的应用标题将显示在已安装的应用中。

:::image type="content" source="images/outlook-desktop-more-apps.png" alt-text="单击边栏上的 (&quot;更多应用&quot;) 选项以查看已安装的个人选项卡":::

单击应用图标以在应用中启动Outlook。

### <a name="outlook-on-the-web"></a>Outlook 网页版

若要在应用中查看Outlook 网页版，请访问 https://outlook.office.com ，然后使用你的开发人员租户帐户登录。 单击边栏上的 **()** 省略号..."。 旁加载的应用标题将显示在已安装的应用中。

单击应用图标以启动和预览在 Outlook 网页版 中运行的应用。

### <a name="microsoft-office-home"></a>Microsoft Office 主页

若要预览在家庭Microsoft Office中运行的应用，office.com 租户凭据登录。 单击边栏上的 **()** 省略号..."。 旁加载的应用标题将显示在已安装的应用中。

单击应用图标，在"主页"中Office应用。

## <a name="next-steps"></a>后续步骤

Outlook和Office个人选项卡为预览版，不支持用于生产用途。 下面将了解如何分发你的个人选项卡应用以预览受众以进行测试。

### <a name="single-tenant-distribution"></a>单租户分布

Outlook和Office用户的个人选项卡可通过以下三种方式之一跨测试 (或生产) 租户分发给预览受众：

#### <a name="teams-client"></a>Teams客户端

From the *Apps* menu， select *Manage your apps* Submit an app to your  >  **org**.这需要 IT 管理员批准。

#### <a name="microsoft-teams-admin-center"></a>Microsoft Teams管理中心

作为Teams管理员，你可以从 上传并预安装组织租户的应用包 https://admin.teams.microsoft.com/ 。 有关详细信息[，Upload管理中心Microsoft Teams自定义](/MicrosoftTeams/upload-custom-apps)应用。

#### <a name="microsoft-admin-center"></a>Microsoft 管理中心

作为全局管理员，你可以从 上传并预安装应用包 https://admin.microsoft.com/ 。 有关详细信息[，请参阅Microsoft 365 应用版应用门户中的测试](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps)并部署合作伙伴部署应用。

### <a name="multi-tenant-distribution"></a>多租户分布

在此早期开发人员预览期间，不支持向 Microsoft AppSource 分发Outlook和Office支持Teams选项卡。
