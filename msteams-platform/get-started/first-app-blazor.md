---
title: 入门 - 使用 Blazor 生成Teams应用程序
author: adrianhall
description: 快速创建显示"Hello，World！"的 Microsoft Teams 应用。 message using the Microsoft Teams Toolkit and .NET Blazor.
ms.author: adhal
ms.date: 04/27/2021
ms.topic: quickstart
ms.localizationpriority: none
ms.openlocfilehash: d014ba82f8e499b8b38f1dbc13a9ee68ef29f1c9
ms.sourcegitcommit: 72de146d11e81fd9777374dd3915ad290fd07d82
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2021
ms.locfileid: "59360652"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-blazor"></a>使用 Blazor 生成Microsoft Teams应用程序

本教程介绍如何在 .NET/Blazor 中创建新的 Microsoft Teams 应用，该应用实现简单的个人应用，以从 Microsoft Graph。 例如，个人 *应用包括* 一组供个人使用的选项卡。 在本教程中，你将了解 Teams 应用的结构、如何在本地运行应用以及如何将应用部署到 Azure。

构建的应用将显示当前用户的基本用户信息。  授予权限后，应用会作为当前用户连接到 Microsoft Graph 以获取完整配置文件。

## <a name="before-you-begin"></a>准备工作

请确保通过安装必备组件来设置开发环境。

> [!div class="nextstepaction"]
> [安装先决条件](prerequisites.md)

## <a name="create-your-project"></a>创建项目

使用 Teams 工具包创建你的第一个项目:

1. 打开Visual Studio 2019。

1. 选择 **创建新项目**。

1. 选择 **Microsoft Teams应用**"，然后选择"下一 **步"。**  若要帮助您查找模板，请使用项目类型 **Microsoft Teams**。

1. 输入名称，然后选择下一 **步**。

1. 输入应用程序名称和公司名称。

1. 选择“**创建**”。  应用程序名称和公司名称将显示给最终用户。 将在数秒钟内创建你的 Teams 应用。  创建项目后，使用 M365 设置单一登录：

   1. 选择 **Project**  >  **TeamsFx**  >  **配置 SSO..."。**
   1. 系统提示时，登录到 M365 管理员帐户。

---

## <a name="take-a-tour-of-the-source-code"></a>浏览源代码

若要暂时跳过此部分，可以 [在本地运行应用](#run-your-app-locally)。

在Teams Toolkit项目后，你拥有组件来构建适用于用户的基本个人Teams。 项目目录和文件显示在 2019 年 10 月Visual Studio区域。

:::image type="content" source="../assets/images/teams-toolkit-v2/blazor-file-layout.png" alt-text="Screenshot showing app project files for a personal app in Visual Studio 2019.":::

- 应用图标在 `color.png` 和 `outline.png`中存储为 PNG 文件。
- 用于通过开发人员门户发布的应用程序清单Teams存储在 中 `Properties/manifest.json` 。
- 提供后端控制器以帮助 `Controllers/BackendController.cs` 进行身份验证。

由于在设置期间创建了选项卡应用程序，Teams Toolkit将基本选项卡的所有必要代码搭建为[Blazor Server](/aspnet/core/blazor)。

- `Pages/Tab.razor` 是前端应用程序的入口点。
- `TeamsFx.cs``JS/src/index.js`和 用于初始化与主机Teams通信。

可以通过向应用程序添加其他 ASP.NET Core添加后端功能。

## <a name="run-your-app-locally"></a>在本地运行应用

使用 Teams 工具包，你可以在本地运行应用。  这包含几个部分，是提供 Teams 所需的正确基础结构所必需的：

- 应用程序已注册 Azure Active Directory。  此应用程序具有与从加载应用的位置及其访问的任何后端资源相关联的权限。
- Web API 通过 (托管IIS Express) ，以帮助执行身份验证任务，充当应用和 Azure Active Directory 之间的代理。  
- 生成应用清单，存在于 Teams 开发人员门户中。  Teams 使用应用清单告诉已连接客户端从何处加载应用。

完成此操作后，应用可以在客户端Teams加载。  我们使用 Teams Web 客户端，以便可以在标准 Web 开发环境中查看 HTML、CSS 和 JavaScript 代码。

若要在本地构建并运行应用程序:


1. 在Visual Studio Code中，按 **F5** 键以在调试模式下运行应用程序。


1. 如果需要，请安装自签名 SSL 证书进行本地调试。

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="显示如何安装 SSL 证书以便 Teams 从 localhost 加载应用程序提示的屏幕截图。":::

1. 将在 Web 浏览器中加载 Teams，并提示进行登录。 如果系统提示打开 Microsoft Teams，请选择"取消"以保留在浏览器中。 使用 M365 帐户登录。

1. 当系统提示将应用安装到 Teams，选择"添加 **"。**

   此时将显示应用：

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-completed-app.png" alt-text="已完成应用的屏幕截图":::

   你可以执行调试活动，就像执行任何其他 Web 应用程序（如设置断点）一样。 该应用支持热重新加载。  如果更改了项目内的任何文件，将重新加载页面。

<!-- markdownlint-disable MD033 -->
<details>
<summary>在调试器中本地运行应用时，会发生什么情况。</summary>

按 **F5 键** 时，Teams Toolkit：

1. 向应用程序注册Azure Active Directory。
1. 将应用程序注册为"旁加载"Microsoft Teams。
1. 在本地运行启动应用程序后端。
1. 在本地托管应用程序前端启动。
1. 使用Microsoft Teams启动 Web 浏览器中的 url，以指示Teams在应用程序清单 (中注册 URL 时旁加载) 。

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary>了解如何在本地运行应用时解决常见问题。</summary>

若要在应用中成功运行Teams，你必须拥有一个Microsoft 365支持应用旁加载的一个开发帐户。 有关开设帐户的详细信息，请参阅 [先决条件](prerequisites.md#enable-sideloading)。

</details>

## <a name="deploy-your-app-to-azure"></a>将应用部署到 Azure

部署包含两个步骤： 

1. 创建必要的云资源。 这也称为预配。
1. 开始编码，将应用复制到已创建的云资源。

> **预览**
>
> 对 Blazor 应用的支持是 Teams Toolkit。  设置和部署是结合 Visual Studio 2019 和开发人员门户进行Teams。

## <a name="provision-and-deploy-your-app-to-azure-app-service"></a>预配应用并部署到 Azure 应用服务

1. 在"解决方案资源管理器"中，右键单击项目节点并选择"发布 **"。** 您还可以使用"生成  >  **发布"** 菜单项。

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish1.png" alt-text="选择项目的&quot;发布&quot;操作":::

1. 在"**发布"** 窗口中，选择 **"Azure"，** 然后选择"下一 **步"。**

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish2.png" alt-text="选择 Azure 作为发布目标":::

1. 选择 **Azure 应用服务 (Windows) ，** 然后选择下一 **步**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish3.png" alt-text="选择 Azure 应用服务作为发布目标":::

1. 选择 **+** 以创建新的应用服务实例。

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish4.png" alt-text="创建新实例。":::

1. 在"**创建应用服务 (Windows)** 对话框中，将填充"名称"、订阅名称、"资源组"和"**托管** 计划"条目字段。  如果已运行应用服务，则选择现有设置。  可以选择创建新的资源组和托管计划。  准备就绪后，选择"创建 **"。**

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish5.png" alt-text="选择托管计划和订阅":::

1. 在 **"发布** "对话框中，已自动选择新创建的实例。  准备就绪后，选择"**完成"。**

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish6.png" alt-text="选择新实例。":::

1. 选择部署 **(** 旁边的 **) 铅笔图标**"，然后选择"**自包含"。**

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish8.png" alt-text="选择自包含部署模式。":::

1. 选择“**发布**”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish7.png" alt-text="将应用发布到应用服务":::

   Visual Studio将应用部署到 Azure 应用服务，并且 Web 应用在浏览器中加载。  添加到 `/tab` URL 的末尾以查看你的页面。

   "项目属性 **发布** "窗格显示网站 URL 和其他详细信息。 记下网站 URL。

## <a name="create-an-environment-for-your-app"></a>为应用创建环境

开发人员门户 for Teams管理使用 Environment 加载应用的选项卡 **位置**。  

**创建环境：**

1. 打开[开发人员门户，Teams。](https://dev.teams.microsoft.com)  使用 M365 管理帐户登录。

1. 从边栏中，**选择应用。**

1. 如果只有一个应用，将自动选择它。  如果没有，请从列表中选择你的应用。

1. 选择 **"环境"。**

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments1.png" alt-text="选择环境":::

1. 选择 **"创建你的第一个环境"。**

1. 输入你的环境的名称， **然后选择添加**。 例如，`_Production_`。

1. 选择 **"创建第一个环境变量"。**

1. 输入 `azure_app_url` 名称。  输入 Azure 网站 URL，但不带 `https://` 值 。 

    :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments2.png" alt-text="创建环境变量":::

   按 **"添加"。**

## <a name="update-the-app-manifest"></a>更新应用清单

应用清单从 URL 加载 `localhost` 选项卡。  在此部分中，你将配置应用清单，以从刚创建的环境中列出的 URL 加载选项卡。

1. 从边栏中，选择 **"基本信息"。**

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments3.png" alt-text="选择基本信息":::

1. 清单中有几个位置将 列出为 `localhost:XXXXX` URL 的一部分。  将所有匹配项替换为 `{{azure_app_url}}` ，包括大括号。

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments4.png" alt-text="调整环境的基本信息":::

1. 完成后，**选择保存。**

1. 从边栏中，选择 **"功能"。**

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments5.png" alt-text="选择功能":::

1. 选择 **"个人"选项卡**。
1. 在"个人 **"选项卡旁边**，选择三个点，然后选择"编辑 **"。**

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments6.png" alt-text="编辑个人选项卡设置":::

1. 将 URL 替换为"内容 Url"和"网站 **Url"** 字段中 **的环境** 变量。

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments7.png" alt-text="编辑个人选项卡 URL":::

1. 选择“**更新**”。

1. 选择“**保存**”。

1. 从边栏中，选择 **"单一登录"。**

1. 将 `localhost` 应用程序 **ID URI 中的** 替换为 `{{azure_app_url}}` 。

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments8.png" alt-text="编辑单一登录应用程序 ID URI":::

1. 选择“**保存**”。

1. 从边栏中， **选择域**。

1. 选择“**添加域**”。

1. 如果未 `{{azure_app_url}}` 列为有效域，请将其添加为有效域，然后选择"添加 **"。**

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments9.png" alt-text="添加域":::

   现在，可以使用页面顶部的"Teams预览"选项在页面内启动Teams。

## <a name="see-also"></a>另请参阅

* [教程概述](code-samples.md)
* [创建对话机器人应用](first-app-bot.md)
* [创建邮件扩展](first-message-extension.md)
* [代码示例](https://github.com/OfficeDev/Microsoft-Teams-Samples)
