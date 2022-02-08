---
title: 跨Teams扩展个人选项卡Microsoft 365
description: 跨Teams扩展个人选项卡Microsoft 365
ms.date: 11/15/2021
ms.topic: tutorial
ms.custom: Microsoft 365 apps
ms.localizationpriority: medium
---
# <a name="extend-a-teams-personal-tab-across-microsoft-365"></a>跨Teams扩展个人选项卡Microsoft 365

> [!NOTE]
> *目前，Teams个人选项卡* Microsoft 365仅在公共开发人员预览 [版中可用](../resources/dev-preview/developer-preview-intro.md)。 预览版中包含的功能可能不完整，并且在公开发布之前可能会发生更改。 它们仅用于测试和探索目的。 不应在生产应用程序中使用它们。

个人选项卡提供了一种增强用户体验Microsoft Teams方式。 使用个人选项卡，你可以为用户提供对 Teams 应用程序的访问权限，而无需离开体验或重新登录。 借助此预览，个人选项卡可以在其他应用程序Microsoft 365显示。 本教程演示采用现有个人选项卡Teams更新它以在桌面和 Web Outlook体验中运行的过程，以及Office web 版 (office.com) 。

更新个人应用以在 Outlook Office 主页中运行涉及以下步骤：

> [!div class="checklist"]
> * 更新应用清单
> * 更新 TeamsJS SDK 引用 
> * 修改内容安全策略标头
> * 为 SSO Azure AD单一登录 (应用) 

测试应用需要以下步骤：

> [!div class="checklist"]
> * 在定向Microsoft 365中注册 *Office 365租户*
> * 配置帐户以访问预览版本的 Outlook 和 Office 应用
> * 将更新的应用旁加载到Teams

执行这些步骤后，你的应用应显示在 Outlook 和 Office 预览版本中。

## <a name="prerequisites"></a>必备条件

若要完成本教程，你需要：

* 开发人员Microsoft 365沙盒租户
* 你的沙盒租户已注册 *Office 365定向版本*
* 从 Office beta 渠道安装 Microsoft 365 应用版 *应用的计算机*
*  (代码) [Teams Toolkit](https://aka.ms/teams-toolkit)代码Microsoft Visual Studio扩展，以帮助更新代码

> [!div class="nextstepaction"]
> [安装先决条件](prerequisites.md)

## <a name="prepare-your-personal-tab-for-the-upgrade"></a>为升级准备个人选项卡

如果你有现有的个人选项卡应用，请创建生产项目的副本或分支以在应用清单中测试并更新应用 ID，以使用与生产应用 ID (不同的新标识符) 。

如果您想使用示例代码完成本教程，请按照 [Todo 列表入门示例中](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend)的设置步骤，使用 Teams Toolkit for Visual Studio Code 扩展构建个人选项卡应用程序。 或者，你可以从为 [TeamsJS SDK v2](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend-M365) 预览版更新的同一个"Todo 列表示例"开始，然后继续在其他体验中预览[Microsoft 365选项卡](#preview-your-personal-tab-in-other-microsoft-365-experiences)。 更新的示例也可在 Teams Toolkit extension： *DevelopmentView* >  **samplesTodo List (Works in Teams， Outlook and Office)**。 > 

:::image type="content" source="images/toolkit-todo-sample.png" alt-text="Todo List sample (Works in Teams， Outlook and Office) in Teams Toolkit":::


## <a name="update-the-app-manifest"></a>更新应用清单

你需要使用开发人员预览[](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview) `Microsoft 365 DevPreview` Teams清单架构和清单版本，以使 Teams 个人选项卡在 Office 和 Outlook 中运行。

可以使用以下Teams Toolkit更新应用清单，也可以手动应用更改：

# <a name="teams-toolkit"></a>[Teams 工具包](#tab/manifest-teams-toolkit)

1. 打开命令 *调色板*： `Ctrl+Shift+P`
1. 运行 命令 `Teams: Upgrade Teams manifest to support Outlook and Office apps` 并选择应用清单文件。 将就地进行更改。

# <a name="manual-steps"></a>[手动步骤](#tab/manifest-manual)

打开Teams应用清单，然后使用`$schema``manifestVersion`下列值更新 和 ：

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```
---

如果你使用Teams Toolkit创建个人应用，则还可以使用它来验证对清单文件所做的更改并识别任何错误。 打开命令调色板并`Ctrl+Shift+P`找到"Teams **：** 验证清单文件"，或者从 Teams Toolkit (的"部署"菜单中选择选项，查找 Teams 左侧的 Visual Studio Code) 。

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams Toolkit&quot;部署&quot;菜单下的&quot;验证清单文件&quot;选项":::

## <a name="update-sdk-references"></a>更新 SDK 引用

若要在 Outlook 和 Office 中运行，你的应用将需要依赖 npm `@microsoft/teams-js@2.0.0-beta.1` 程序包 (或更高版本的) 。 `@microsoft/teams-js`尽管 Outlook 和 Office `@microsoft/teams-js` 中支持具有下层版本的代码，但弃用警告将被记录，并且对 Outlook 和 Office 中的下层版本的支持将最终停止。

可以使用 Teams Toolkit `@microsoft/teams-js`自动执行某些代码更改以采用下一版本的 ，但如果你想要手动执行这些步骤，请参阅 [Microsoft Teams JavaScript 客户端 SDK 预览](using-teams-client-sdk-preview.md)版了解详细信息。

1. 打开命令 *调色板*： `Ctrl+Shift+P`
1. 运行命令 `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`

完成后，该实用工具会`package.json`使用 TeamsJS SDK 预览版 (`@microsoft/teams-js@2.0.0-beta.1` 或更高版本) 更新你的文件`*.js/.ts``*.jsx/.tsx`，并且你的 和 文件将更新为：

> [!div class="checklist"]
> * `package.json` 对 TeamsJS SDK 预览版的引用
> * 导入 TeamsJS SDK 预览版语句
> * 对 TeamsJS SDK [预览版的函数](using-teams-client-sdk-preview.md#apis-organized-into-capabilities)、枚举和接口调用
> * `TODO` 注释提醒，用于查看可能受 [上下文接口更改](using-teams-client-sdk-preview.md#updates-to-the-context-interface) 影响的区域
> * `TODO` 注释提醒以确保 [从回调](using-teams-client-sdk-preview.md#callbacks-converted-to-promises) 样式函数转换到承诺函数在工具找到的所有调用网站中都运行良好

> [!IMPORTANT]
> 升级 *.html* 不支持文件内的代码，并且需要手动更改。

> [!NOTE]
> 如果你想要手动更新代码，请参阅 Microsoft Teams [JavaScript 客户端 SDK 预览](using-teams-client-sdk-preview.md)版，了解所需的更改。

## <a name="configure-content-security-policy-headers"></a>配置内容安全策略标头

[就像在 Microsoft Teams](/microsoftteams/platform/tabs/what-are-tabs) 中一样，选项卡应用程序托管在 () 和 Outlook 客户端中的 Office [iframe](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) 元素中。

如果你的应用使用云解决方案提供商[](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) ，请确保你在 CSP 标头中允许以下所有帧[上级](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors)：

|Microsoft 365主机| 帧-上级权限|
|--|--|
| Teams | `teams.microsoft.com` |
| Office | `*.office.com` |
| Outlook | `outlook.office.com`, `outlook.office365.com` |

## <a name="update-azure-ad-app-registration-for-sso"></a>更新Azure AD SSO 的应用注册

Azure Active Directory 个人选项卡的 (SSO) 单一登录的工作方式与在 [Office 和 Outlook](/microsoftteams/platform/tabs/how-to/authentication/auth-aad-sso) 中相同，但在 Teams 中，你需要将多个客户端应用程序标识符添加到租户的应用注册门户中选项卡应用的 Azure AD 应用注册中。

1. 使用沙[Microsoft Azure](https://portal.azure.com)帐户登录门户。
1. 打开应用 **注册** 边栏选项卡。
1. 选择个人选项卡应用程序的名称以打开其应用注册。 
1. 选择 **"管理 ("***下的"公开* API) "。

:::image type="content" source="images/azure-app-registration-clients.png" alt-text="从门户上的 *应用注册* 边栏选项卡授权Microsoft Azure ID":::

在" **授权客户端应用程序"** 部分，确保添加以下所有 `Client Id` 值：

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

## <a name="sideload-your-app-in-teams"></a>在 Teams 中旁加载应用

最后一步是将更新的个人选项卡旁加载 ([程序包) ](/microsoftteams/platform/concepts/build-and-test/apps-package)应用程序Microsoft Teams。 完成后，除了在 Teams 中，你的应用Office和 Outlook 中Teams。

1. 将应用程序Teams打包 (清单和应用[图标](/microsoftteams/platform/resources/schema/manifest-schema#icons)) zip 文件中。 如果使用 Teams Toolkit 创建应用，可以使用 Teams Toolkit  `Ctrl+Shift+P` 的"部署"菜单中的 **Zip Teams** 元数据包选项或以下命令调色板Visual Studio Code：

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Teams扩展中的&quot;Zip Teams 元数据包&quot;Visual Studio Code Teams Toolkit&quot;":::

1. 登录以Teams沙盒租户帐户登录，并确保使用公共开发者预览版。 通过按用户配置文件单击省略号" (**...**) "菜单并打开"关于"，检查"开发人员预览"选项是否处于打开状态，可以验证你是否位于 Teams 客户端中的"预览"上。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="从Teams省略号&quot;菜单中，打开&quot;关于&quot;并确认&quot;开发者预览版&quot;选项已选中":::

1. 打开"*应用"* 窗格，Upload **自定义应用，** 然后Upload **或我的团队。**

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Upload&quot;应用&quot;窗格中的&quot;Teams自定义应用&quot;按钮":::

1. 选择你的应用包，*然后单击打开。*

通过旁加载Teams，你的个人选项卡将在 Outlook 和 Office 中提供。 请务必使用用于在你的应用中旁加载应用的相同凭据Teams。

你可以固定应用以快速访问，或者可以在左侧边栏中的省略号 (**...**) 最近应用程序之间的飞出。

> [!NOTE]
> 将应用固定到Teams不会将其固定为 Office.com 或 Outlook 中的应用。

## <a name="preview-your-personal-tab-in-other-microsoft-365-experiences"></a>在其他体验中预览Microsoft 365选项卡

在升级你的 Teams 个人选项卡并旁加载它Teams，它还将在 Outlook 桌面和 Web 客户端和 Office web 版 (office.com) 中运行。 下面将了解如何从这些体验中预览Microsoft 365体验。

### <a name="outlook"></a>Outlook

若要查看在桌面Outlook中Windows的应用，Outlook开发人员租户帐户启动并登录。 单击边栏上的 (**省略**) ..."。 旁加载的应用标题将显示在已安装的应用中。

:::image type="content" source="images/outlook-desktop-more-apps.png" alt-text="单击桌面客户端的 (栏上的&quot;更多) &quot;选项的省略号，Office查看已安装的个人选项卡":::

单击应用图标以在应用中启动Outlook。

### <a name="outlook-on-the-web"></a>Outlook 网页版

若要在应用中查看Outlook 网页版，请访问https://outlook.office.com，然后使用你的开发人员租户帐户登录。 单击边栏上的 (**省略**) ..."。 旁加载的应用标题将显示在已安装的应用中。

:::image type="content" source="images/outlook-web-more-apps.png" alt-text="单击屏幕侧栏 (&quot;更多应用&quot;) 选项的省略号 outlook.com 查看已安装的个人选项卡":::

单击应用图标以启动和预览在 Outlook 网页版 中运行的应用。

### <a name="office-on-the-web"></a>Office 网页版

> [!IMPORTANT]
> 请参阅 Microsoft Teams [- Microsoft 365 开发人员](https://devblogs.microsoft.com/microsoft365dev/)博客上的最新更新，以检查测试租户是否Office.com Teams个人应用支持。

若要预览在 Office web 版 中运行的应用，office.com 测试租户凭据登录。 单击边栏上的 (**省略**) ..."。 旁加载的应用标题将显示在已安装的应用中。

单击应用图标，在"主页"中Office应用。

## <a name="next-steps"></a>后续步骤

Outlook和Office个人选项卡为预览版，不支持用于生产用途。 下面将了解如何分发你的个人选项卡应用以预览受众以进行测试。

### <a name="single-tenant-distribution"></a>单租户分布

Outlook和Office用户的个人选项卡可通过以下三种方式之一跨测试 (或生产) 租户分发给预览受众：

#### <a name="teams-client"></a>Teams客户端

从" *应用"* 菜单中， *选择"管理应用* > **""将应用提交到组织"**。这需要 IT 管理员批准。

#### <a name="microsoft-teams-admin-center"></a>Microsoft Teams管理中心

作为Teams管理员，你可以从 上传并预安装组织租户的应用包https://admin.teams.microsoft.com/。 有关详细信息[Upload管理中心Microsoft Teams自定义](/MicrosoftTeams/upload-custom-apps)应用。

#### <a name="microsoft-admin-center"></a>Microsoft 管理中心

作为全局管理员，你可以从 上传并预安装应用包 https://admin.microsoft.com/。 有关详细信息[，请参阅Microsoft 365 应用版应用门户中的测试](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps)并部署合作伙伴部署应用。

### <a name="multi-tenant-distribution"></a>多租户分布

在此早期开发人员预览版中，不支持向 Microsoft AppSource 分发Outlook和Office支持Teams选项卡。
