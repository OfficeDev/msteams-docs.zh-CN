---
title: 教程 - 使用 Yeoman 生成器创建第一个应用
description: 了解如何开始使用 Yeoman Microsoft Teams生成应用。
keywords: nodejs yeoman node.js入门
ms.localizationpriority: medium
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: 90bd997de1e5bbfc92e366d466c156f052cbe3bf
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155767"
---
# <a name="build-your-first-microsoft-teams-app-using-the-yeoman-generator"></a>使用 Yeoman Microsoft Teams生成首个应用

> [!Note]
> 本教程来自适用于 wiki 的[Yeoman Teams生成器](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)。

本教程介绍如何使用 Yeoman Microsoft Teams生成首个Microsoft Teams应用。 它还指导你完成使用 Yeoman 生成器Teams升级应用程序的过程。 在开始之前，你必须拥有一个Teams允许[应用旁加载的帐户](~/concepts/build-and-test/prepare-your-o365-tenant.md)。

![yeoman 生成器 git](~/assets/yeoman-demo.gif)

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>获取先决条件

在开始使用 Yeoman 生成器之前，你需要在计算机上安装以下组件：

* Node.js

   你需要在计算机上安装Node.js软件。 你应该使用最新的 [LTS 版本](https://nodejs.org)。

* 代码编辑器

   你需要一个代码编辑器。 本文档和图像中的大多数内容[都指使用](https://code.visualstudio.com)Visual Studio Code。 但是，您可以随意使用您喜欢的任何文本编辑器。

* Yeoman 和 Gulp CLI

   若要使用生成器搭建项目基架，必须安装 Yeoman 工具和 Gulp CLI 任务管理器。

   打开命令提示符并键入以下内容：

   ```bash
   npm install yo gulp-cli --global
   ```

## <a name="install-the-generator"></a>安装生成器

使用Teams安装 Yeoman 生成器：

```bash
npm init yo teams
```

使用下列命令安装生成器的预览版本：

```bash
npm init yo teams@preview
```

## <a name="generate-your-project"></a>生成项目

本节将指导你完成生成项目的步骤。

**生成项目**

1. 打开命令提示符并创建要创建项目的新目录。
1. 转到 目录，然后运行命令 `yo teams` 。 生成器启动。
1. 响应生成器提示的一组问题：

   ![yo teams](~/assets/yeoman-images/teams-first-app-1.png)

   1. 输入项目的名称。 按 Enter 可保持其为 。
   1. 如果要创建新目录，请输入新目录的路径。 由于你已进入你需要的目录中，只需按 Enter。
   1. 输入项目的标题。 此标题将在应用的清单和说明中使用。 
   1. 输入还将在清单中使用的公司名称。
   1. 输入想要使用的清单版本。 对于本教程，请选择 `v1.5` ，这是当前可用的常规架构。
   1. 选择要添加到项目中的项目。 可以选择单个项目或任意项目组合。 对于本教程，只需选择 *一个选项卡*：

    ![项目选择](~/assets/yeoman-images/teams-first-app-2.png)

1. 根据在步骤 3 中选定的项目回答出现的下一组后续问题。
1. 输入解决方案的托管位置的 URL。 

   > [!NOTE]
   > 该 URL 可以是任何 URL，但默认情况下，生成器建议 Azure 网站 URL。

1. 确认是否要包含解决方案的单元测试。 默认响应为 **"是"。** 如果选择包括单元测试，则生成的项目将具有一个单元测试框架和一些针对基架的不同项目的默认单元测试。 
   > [!NOTE]
   > * 对于本教程，选择不包括测试框架。
   > * 生成器具有许多内置高级功能，你可以选择加入或选择退出。

1. 为了便于你登录，还将询问你是否要使用 Azure 应用程序Insights登录。 如果选择"**是"，** 则需要提供 Azure 应用程序Insights密钥。 

   > [!NOTE]
   > 对于本教程，选择退出使用应用程序Insights。

   下一组问题将基于之前选定的项目。 对于选项卡，你只需提供一个名称，并可以选择是否希望能够使用此应用作为 SharePoint Online Web 部件。 提供名称后，生成器将生成项目并安装所有依赖项。 这可能需要一两分钟的时间。

## <a name="add-code-to-your-tab"></a>将代码添加到选项卡

生成器完成后，可以在最喜爱的代码编辑器中打开解决方案。 请花一两分钟的时间，熟悉代码的整理方式。 有关详细信息，请参阅Project[结构](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure)文档。

您的选项卡位于 `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` 文件中。 这是选项卡React基于 TypeScript 的类。 

1. 找到 `render()` 方法，在控件中添加一 `<PanelBody>` 行代码，如下所示：

   ``` TypeScript
   <PanelBody>
      <div style={styles.section}>
      Hello World! Yo Teams rocks!
      </div>
   </PanelBody>
   ```
1. 保存文件并返回到命令提示符。

## <a name="build-your-app"></a>生成应用程序

现在可以生成项目。 此操作分两步完成。

1. 为Teams应用创建应用清单Microsoft Teams。 这由 Gulp 任务完成 `gulp manifest` 。 这将验证清单，并创建目录中的 zip `./package` 文件。
1. 运行 `gulp build` 命令以生成解决方案。 这会将解决方案转换为 `./dist` 文件夹。 

## <a name="run-your-app"></a>运行应用

若要运行应用，请使用 `gulp serve` 命令。 这将生成并启动本地 Web 服务器，供你测试应用。 每次在项目中保存文件时，该命令也将重新生成应用程序。 

现在应转到 ， `http://localhost:3007/myFirstAppTab/` 并确保选项卡正在呈现。 但是，它尚未Microsoft Teams中。 

**在页面呈现选项卡Microsoft Teams**

![在浏览器中查看网站](~/assets/yeoman-images/teams-first-app-3.png)

### <a name="run-your-app-in-microsoft-teams"></a>在应用商店中Microsoft Teams

Microsoft Teams不允许将应用托管在 localhost 上，因此你需要将其发布到公用 URL 或使用代理（如 ngrok）。 好消息是，搭建的项目具有此内置功能。 

**在应用程序中运行Teams**

1. 在 `gulp ngrok-serve` 终端中运行。 运行 ngrok 服务时，将在后台启动具有唯一的公用 DNS 条目，并且它还会使用该唯一 URL 打包清单，然后执行与 完全相同 `gulp ngrok-serve` 的相同操作 `gulp serve` 。
1. 创建新的团队Microsoft Teams团队。
1. 选择"团队名称> Teams 设置 >应用"。
1. 从右下角，选择Upload **应用"。**
1. 转到项目 `package` 文件夹下的文件夹。 
1. 选择该文件夹中的 zip 文件，然后选择"打开"。 
   你的应用现在旁加载至Microsoft Teams：

   ![旁加载的应用](~/assets/yeoman-images/teams-first-app-4.png)
1. 返回到 **常规频道，** 然后选择 **+** 添加新的选项卡。你应该在选项卡列表中看到您的选项卡： ![ 配置选项卡](~/assets/yeoman-images/teams-first-app-5.png)
1. 选择您的选项卡，然后按照说明添加它。 请注意，有一个自定义配置对话框，您可以编辑源。 选择 *"保存* "将选项卡添加到频道。 现在选项卡已加载到 Microsoft Teams！

   ![teams 中的"运行"选项卡](~/assets/yeoman-images/teams-first-app-6.png)

### <a name="upgrade-microsoft-teams"></a>升级Microsoft Teams

您还可以使用 Yeoman Microsoft Teams将当前版本升级到最新版本Microsoft Teams版本。

**升级Microsoft Teams**

1. 通过以下Teams获取当前版本的版本：

   ```PowerShell
    yo teams --version
   ```
2. 使用以下命令选择和更新生成器：

   ```PowerShell
    yo
   ```
3. 使用箭头键选择更新 **生成器**：

   ![YoSelectUpdatGen 的图像](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

4. 从生成器列表中选择你需要的生成器：
   > [!NOTE]
   > 使用空格键从可用选项中选择或清除Teams版本。

    ![UseSpaceToSelectGenerators 的图像](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)
    

   > [!NOTE]
   > 完成安装需要几秒钟到Teams分钟。

5. 安装完成后，使用以下命令检查安装的版本：

   ```PowerShell
    yo teams --version
   ```
   恭喜！ 生成并部署了第一个Microsoft Teams应用。 你还升级了Microsoft Teams。

 ## <a name="see-also"></a>另请参阅

* [教程概述](code-samples.md)
* [创建对话机器人应用](first-app-bot.md)
* [创建邮件扩展](first-message-extension.md)
* [代码示例](https://github.com/OfficeDev/Microsoft-Teams-Samples)
