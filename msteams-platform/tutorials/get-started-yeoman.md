---
title: 教程 - 使用 Yeoman 生成器创建第一个应用
description: 了解如何开始使用 Yeoman 生成器生成 Microsoft Teams 应用。
keywords: nodejs yeoman node.js入门
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: f7f0fb3ba1be28dfa7d343be3af9d122b4ad090d
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037002"
---
# <a name="create-your-first-microsoft-teams-app-using-the-yeoman-generator"></a>使用 Yeoman 生成器创建你的第一个 Microsoft Teams 应用

>[!Note]
>本教程来自 Teams [Wiki 的 Yeoman 生成器](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)。

本教程介绍如何使用 Microsoft Teams Yeoman 生成器创建首个 Microsoft Teams 应用。 它假定你有一个允许应用旁 [加载的](~/concepts/build-and-test/prepare-your-o365-tenant.md)Teams 帐户。

![yeoman 生成器 git](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a>设置和准备计算机

在开始使用 Yeoman 生成器之前，你需要在计算机上安装以下组件。

### <a name="install-nodejs"></a>安装 Node.js

你需要将Node.js安装在计算机上。 你应该使用最新的 [LTS 版本](https://nodejs.org)。

### <a name="install-a-code-editor"></a>安装代码编辑器

你还需要一个代码编辑器，可以随意使用你喜欢的任何文本编辑器。 但是，本文档和屏幕截图中的大多数内容都指使用Visual Studio [代码](https://code.visualstudio.com)。

### <a name="install-yeoman-and-gulp-cli"></a>安装 Yeoman 和 Gulp CLI

若要能够使用 Teams 生成器搭建项目，需要安装 Yeoman 工具以及 Gulp CLI 任务管理器。

打开命令提示符并键入以下内容：

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-generator"></a>安装生成器

使用以下命令安装 Teams Yeoman 生成器：

```bash
npm install generator-teams --global
```

若要安装生成器的预览版本，请运行以下命令：

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a>生成项目

打开命令提示符并创建要创建项目的新目录，并运行命令 `yo teams` 。

这会启动生成器，这会提示您一组问题。

![yo teams](~/assets/yeoman-images/teams-first-app-1.png)

第一个问题与项目名称有关，可以通过按 Enter 来保留它。 下一个问题询问您是否要创建新目录或使用当前目录。 由于我们已在我们需要的目录中，只需按 Enter 键。

下一步需要项目的标题，此标题将在应用的清单和说明中使用。 然后，将要求您输入公司名称，该名称也将在清单中使用。

第五个问题询问您有关想要使用的清单版本。 对于本教程， `v1.5` 请选择当前可用的常规架构。

在此之后，生成器将询问要添加到项目中的项目。 可以选择单个项目或任意项目组合。 现在，只需选择 *一个选项卡*。

![项目选择](~/assets/yeoman-images/teams-first-app-2.png)

根据选择的项目，将询问一组后续问题。

现在您需要输入解决方案的托管位置的 URL。 这可以是任何 URL，但默认情况下，生成器建议使用 Azure 网站 URL。

生成器具有许多内置高级功能，你可以选择加入或选择退出。 在 URL 问题后，将询问您是否要包含解决方案的单元测试，默认值为"是"。 如果选择此选项，生成的项目将具有单元测试框架和一些用于搭建基架的不同项的默认单元测试。 对于本教程，选择不包括测试框架。

为了便于进行日志记录，还会询问您是否要使用 Azure 应用程序见解进行日志记录。 如果选择"是"，则需要提供 Azure 应用程序见解密钥。 对于本教程，选择退出使用 Application Insights。

下一组问题将基于你之前选择的项目。 对于选项卡，你只需提供一个名称，并且可以选择是否希望将此应用程序用作 SharePoint Online Web 部件。 提供此名称后，生成器将生成项目并安装所有依赖项。 这将需要一两分钟。

## <a name="add-some-code-to-your-tab"></a>向选项卡添加一些代码

生成器完成后，可以在你最喜爱的代码编辑器中打开解决方案。 请花一两分钟，熟悉代码的组织结构，您可以在项目结构文档中阅读 [有关该代码](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) 的更多内容。

您的选项卡将位于 `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` 文件中。 这是 Tab 的基于 TypeScript React 的类。找到该方法，在控件内添加一行代码，如下所示 `render()` `<PanelBody>` ：

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

保存文件并返回到命令提示符。

## <a name="build-your-app"></a>生成应用程序

现在可以生成项目。 此操作分两步完成， (一个步骤，请参阅下面的) 。

首先，你需要创建 Teams 应用清单文件，将其上载/旁加载到 Microsoft Teams 中。 这由 Gulp 任务完成 `gulp manifest` 。 这将验证清单，并创建目录中的 zip `./package` 文件。

若要生成解决方案，请使用 `gulp build` 该命令。 这会将解决方案转换为 `./dist` 文件夹。 

## <a name="run-your-app"></a>运行应用

若要运行应用，请使用 `gulp serve` 该命令。 这将生成并启动本地 Web 服务器，供你测试你的应用。 每次在项目中保存文件时，该命令也将重新生成应用程序。 

现在应该可以浏览以确保 `http://localhost:3007/myFirstAppTab/` 选项卡正在呈现。 但是，尚未在 Microsoft Teams 中。

![在浏览器中查看网站](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a>在 Microsoft Teams 中运行应用

Microsoft Teams 不允许你将应用托管在 localhost 上，因此你需要将其发布到公用 URL 或使用代理（如 ngrok）。

好消息是，基架项目具有此内置功能。 运行 ngrok 服务时，将在后台启动具有唯一的公用 DNS 条目，并且它还会使用该唯一 URL 打包清单，然后执行与相同 `gulp ngrok-serve` 操作 `gulp serve` 。

运行后，创建一个新的 Microsoft Teams 团队，当它创建时，单击团队名称，转到团队设置， `gulp ngrok-serve` 然后选择 *应用*。 在右下角，你应该会看到一个链接"上传自定义应用"，选择它，然后浏览到项目文件夹和名为的子文件夹 `package` 。 选择该文件夹中的 zip 文件，然后选择"打开"。 你的应用现在旁加载到 Microsoft Teams 中。

![旁加载的应用](~/assets/yeoman-images/teams-first-app-4.png)

返回到 *"常规"* 频道并选择 *+* 添加新的选项卡。你应该在选项卡列表中看到您的选项卡。

![配置选项卡](~/assets/yeoman-images/teams-first-app-5.png)

选择您的选项卡并按照说明添加它。 请注意，有一个自定义配置对话框，您可以编辑源。 选择 *"* 保存"将选项卡添加到频道。 完成后，你的选项卡应在 Microsoft Teams 中加载！

![在团队中运行选项卡](~/assets/yeoman-images/teams-first-app-6.png)

**恭喜！你生成并部署了你的第一个 Microsoft Teams 应用**
