---
title: 教程 - 使用 Yeoman 生成器创建第一个应用
description: 了解如何开始使用 Yeoman Microsoft Teams生成应用。
keywords: nodejs yeoman node.js入门
localization_priority: Normal
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: 9efbe6f6e6502120f1afdadb9b538182f1406c56
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52018430"
---
# <a name="create-your-first-microsoft-teams-app-using-the-yeoman-generator"></a>使用 Yeoman Microsoft Teams创建你的第一个应用

> [!Note]
> 本教程来自适用于 wiki[的 Yeoman Teams生成器](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)。

本教程介绍如何使用 Yeoman Microsoft Teams创建首个Microsoft Teams应用。 它还指导你完成使用 Yeoman 生成器Teams升级应用程序的过程。 从本教程开始的先决条件是，你拥有一个Teams允许[应用旁加载的帐户](~/concepts/build-and-test/prepare-your-o365-tenant.md)。

![yeoman 生成器 git](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a>设置和准备计算机

在开始使用 Yeoman 生成器之前，你需要在计算机上安装以下组件。

### <a name="install-nodejs"></a>安装 Node.js

你需要将Node.js计算机上安装。 你应该使用最新的 [LTS 版本](https://nodejs.org)。

### <a name="install-a-code-editor"></a>安装代码编辑器

你需要一个代码编辑器。 本文档和图像中的大多数内容都指使用[Visual Studio Code。](https://code.visualstudio.com) 但是，您可以随意使用您喜欢的任何文本编辑器。

### <a name="install-yeoman-and-gulp-cli"></a>安装 Yeoman 和 Gulp CLI

若要使用生成器搭建项目基架，必须安装 Yeoman 工具和 Gulp CLI 任务管理器。

打开命令提示符并键入以下内容：

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-generator"></a>安装生成器

使用Teams安装 Yeoman 生成器：

```bash
npm install generator-teams --global
```

使用下列命令安装生成器的预览版本：

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a>生成项目

本节将指导你完成生成项目的步骤。

**生成项目**

1. 打开命令提示符并创建要创建项目的新目录，并运行命令 `yo teams` 。 生成器启动。
1. 响应生成器提示的一组问题。

   ![yo teams](~/assets/yeoman-images/teams-first-app-1.png)

   1. 第一个问题是有关您的项目名称，您可以通过按 Enter 来保留它。
   1. 下一个问题询问您是否要创建新目录或使用当前目录。 由于你已进入你需要的目录中，只需按 Enter。
   1. 在下一个问题中，键入项目的标题。 此标题将在应用的清单和说明中使用。 
   1. 接下来，将要求您输入公司名称，该名称也将在清单中使用。
   1. 第五个问题询问您想要使用的清单版本。 对于本教程，请选择 `v1.5` ，这是当前可用的常规架构。
   1. 接下来，生成器将询问要添加到项目中的项目。 可以选择单个项目或任意项目组合。 对于本教程，只需选择一 *个选项卡*。

    ![项目选择](~/assets/yeoman-images/teams-first-app-2.png)

1. 响应下一组基于在步骤 2 中选定的项目出现的后续问题。
1. 输入解决方案的托管位置的 URL。 

   > [!NOTE]
   > 该 URL 可以是任何 URL，但默认情况下，生成器建议 Azure 网站 URL。

1. 在下一个问题中，确认是否要包含解决方案的单元测试。 默认 *响应是*。 如果选择包括单元测试，则生成的项目将具有一个单元测试框架和一些用于搭建基架的不同项目的默认单元测试。 
   > [!NOTE]
   > * 对于本教程，选择不包括测试框架。
   > * 生成器具有许多内置高级功能，你可以选择加入或选择退出。

1. 为了便于你登录，还将询问你是否要使用 Azure Application Insights 进行登录。 如果选择" *是"，* 则需要提供 Azure Application Insights 密钥。 

   > [!NOTE]
   > 对于本教程，选择退出使用 Application Insights。

下一组问题将基于之前选定的项目。 对于选项卡，你只需提供一个名称，并可以选择是否希望能够使用此应用作为 SharePoint Online Web 部件。 提供名称后，生成器将生成项目并安装所有依赖项。 这可能需要一两分钟的时间。

## <a name="add-some-code-to-your-tab"></a>向选项卡添加一些代码

生成器完成后，可以在最喜爱的代码编辑器中打开解决方案。 请花一两分钟的时间，熟悉代码的整理方式。 有关详细信息，请参阅Project[结构](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure)文档。

您的选项卡位于 `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` 文件中。 这是选项卡React TypeScript 类。找到 `render()` 方法，在控件中添加一 `<PanelBody>` 行代码，如下所示：

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

保存文件并返回到命令提示符。

## <a name="build-your-app"></a>生成应用程序

现在可以生成项目。 此操作分两个步骤完成， (一个步骤，请参阅下面的) 。

首先，你需要创建Teams清单文件，将该文件上载/旁加载到Microsoft Teams。 这由 Gulp 任务完成 `gulp manifest` 。 这将验证清单，并创建目录中的 zip `./package` 文件。

若要生成解决方案，请使用 `gulp build` 命令。 这会将解决方案转换为 `./dist` 文件夹。 

## <a name="run-your-app"></a>运行应用

若要运行应用，请使用 `gulp serve` 命令。 这将生成并启动本地 Web 服务器，以测试你的应用。 每次在项目中保存文件时，该命令也将重新生成应用程序。 

现在，你应该能够浏览以确保 `http://localhost:3007/myFirstAppTab/` 选项卡正在呈现。 但是，尚不Microsoft Teams中。

![在浏览器中查看网站](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a>在应用商店中Microsoft Teams

Microsoft Teams不允许将应用托管在 localhost 上，因此你需要将其发布到公用 URL 或使用代理（如 ngrok）。

好消息是，搭建的项目具有此内置功能。 运行 ngrok 服务时，将在后台启动具有唯一的公用 DNS 条目，并且它还将清单打包为此唯一 URL，然后执行与 完全相同 `gulp ngrok-serve` 的操作 `gulp serve` 。

运行 `gulp ngrok-serve` 后，创建新的Microsoft Teams团队，创建团队时单击团队名称，转到团队设置，然后选择应用。  在右下角，你应该会看到自定义Upload *的链接，* 选择它，然后浏览到项目文件夹和名为 的子文件夹 `package` 。 选择该文件夹中的 zip 文件，然后选择"打开"。 你的应用现在旁加载到Microsoft Teams。

![旁加载的应用](~/assets/yeoman-images/teams-first-app-4.png)

返回到 *常规频道，* 然后选择 *+* 添加新的选项卡。你应该在选项卡列表中看到您的选项卡。

![配置选项卡](~/assets/yeoman-images/teams-first-app-5.png)

选择您的选项卡，然后按照说明添加它。 请注意，有一个自定义配置对话框，您可以编辑其源。 选择 *"保存* "将选项卡添加到频道。 完成后，您的选项卡应加载到 Microsoft Teams！

![teams 中的"运行"选项卡](~/assets/yeoman-images/teams-first-app-6.png)

## <a name="upgrade-microsoft-teams"></a>升级Microsoft Teams

还可使用 Yeoman Microsoft Teams将当前 Microsoft Teams 版本升级到最新版本。

**升级Microsoft Teams**

1. 通过以下命令Teams获取当前版本的版本：

   ```PowerShell
    yo teams --version
   ```
2. 使用以下命令选择更新生成器：

   ```PowerShell
    yo
   ```
3. 使用箭头键选择更新 **生成器**。

   ![YoSelectUpdatGen 的图像](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

4. 从生成器列表中选择你需要的生成器。
   > [!NOTE]
   > 使用空格键从可用选项Teams或清除所选版本。

    ![UseSpaceToSelectGenerators 的图像](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)
    

   > [!NOTE]
   > 完成安装需要几秒钟到Teams分钟。

5. 安装完成后，使用以下命令检查安装的版本：

   ```PowerShell
    yo teams --version
   ```
   
**恭喜！生成并部署了第一个Microsoft Teams应用。你还升级了Microsoft Teams。**
