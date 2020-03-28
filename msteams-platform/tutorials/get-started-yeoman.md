---
title: Microsoft 团队的 Yeoman 生成器入门
description: 使用 Microsoft 团队的 Yeoman 生成器开始构建强大的应用程序
keywords: 入门节点 .js nodejs yeoman
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: 217c0900e067a61e083e7ffb0b121afdaa51c49f
ms.sourcegitcommit: b13b38a104946c32cd5245a7af706070e534927d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2020
ms.locfileid: "43034041"
---
# <a name="build-your-first-microsoft-teams-app"></a>构建你的首个 Microsoft 团队应用

>[!Note]
>本教程来自适用于[团队 wiki 的 yeoman 生成器](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)

在本教程中，我们将逐步介绍如何使用 Microsoft 团队 Yeoman 生成器创建首个 Microsoft 团队应用程序。 它假定您已[启用 Microsoft 团队应用程序的侧面加载](~/concepts/build-and-test/prepare-your-o365-tenant.md)。

![yeoman 生成器 git](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a>设置和准备计算机

您需要在您的计算机上安装以下程序，然后才能开始使用团队生成器。

### <a name="install-node"></a>安装节点

您需要在您的计算机上安装 NodeJS。 应使用最新的[LTS 版本](https://nodejs.org/dist/latest-v8.x/)。

### <a name="install-a-code-editor"></a>安装代码编辑器

此外，您还需要代码编辑器，可以随时使用您喜欢的任何文本编辑器。 但大部分文档和屏幕截图都是指使用[Visual Studio Code](https://code.visualstudio.com)。

### <a name="install-yeoman-and-gulp-cli"></a>安装 Yeoman 和 Gulp CLI

若要能够使用团队生成器搭建项目，您需要安装 Yeoman 工具以及 Gulp CLI 任务管理器。

打开命令提示符并键入以下命令：

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-microsoft-teams-apps-generator---yo-teams"></a>安装 Microsoft 团队应用生成器-Yo 团队

使用以下命令安装 Microsoft 团队应用的 Yeoman 生成器：

```bash
npm install generator-teams --global
```

#### <a name="install-preview-versions"></a>安装预览版本

如果要使用此命令安装团队生成器的预览版本，请执行以下操作：

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a>生成项目

打开命令提示符并创建要在其中创建项目的新目录，并在该目录中键入该命令`yo teams`。 这将启动 "团队应用生成器"，系统将会提示您一组问题。

![yo 团队](~/assets/yeoman-images/teams-first-app-1.png)

第一个问题是关于您的项目名称的，您可以通过按 enter 将其保留原样。 下一个问题会询问您是否要创建新目录或使用当前目录。 正如我们所需的目录中，我们只需按下 enter 键。

下面的步骤要求您提供项目的标题，此标题将用于您的应用程序的清单和说明。 然后，系统将要求你提供一个公司名称，该名称也将在清单中使用。

第五个问题会询问您要使用的清单版本。 对于此教程， `v1.5`请选择 "当前常规可用架构"。

在此之后，生成器将询问您要添加到项目中的项目。 您可以选择一个或多个项目组合。 现在，只需选择*一个选项卡*。

![项目选择](~/assets/yeoman-images/teams-first-app-2.png)

根据您选择的项目，系统会询问您一组后续问题。

现在，您需要输入将在其中承载解决方案的 URL。 它可以是任何 URL，但默认情况下生成器会建议 Azure 网站 URL。

生成器具有许多内置高级功能，您可以选择或选择退出。 按照 URL 提示问题，系统将提示您是否要包括解决方案的单元测试，默认值为 "是"。 如果选择此选项，则生成的项目将具有单元测试框架，并且会对要搭建的不同项目进行一些默认的单元测试。 对于本教程，请选择不包含测试框架。

为了使日志记录变得简单，系统也会询问您是否要使用 Azure Application Insights 进行日志记录。 如果你选择 "是"，你将需要提供 Azure Application Insights 密钥。 有关此教程，请退出使用 Application Insights。

接下来的一组问题将基于您以前选择的项。 对于选项卡，仅需要提供一个名称，并且可以选择是否希望能够将此应用用作 SharePoint Online web 部件。 提供此名称后，生成器将生成项目并安装所有依赖项。 这需要一分钟或两分钟。

## <a name="add-some-code-to-your-tab"></a>向您的选项卡添加一些代码

生成器完成后，您可以在最喜爱的代码编辑器中打开该解决方案。 花一分钟或两分钟，熟悉代码的组织方式-您可以在[项目结构](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure)文档中阅读有关该信息的详细信息。

您的选项卡将位于`./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx`文件中。 这是您的选项卡的基于 TypeScript 响应的类。 `render()`找到方法并在`<PanelBody>`控件中添加一行代码，使其如下所示：

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

保存文件并返回到命令提示符。

## <a name="build-your-app"></a>生成应用程序

现在可以生成项目。 为此，请执行两个步骤（或一个步骤，如下所示）。

首先，您需要创建团队应用程序清单文件，并将其上传/旁加载到 Microsoft 团队。 这是由 Gulp 任务`gulp manifest`完成的。 这将验证清单并在`./package`目录中创建 zip 文件。

若要生成解决方案，请使用`gulp build`命令。 这会将您的解决方案转换`./dist`到该文件夹中。 

## <a name="run-your-app"></a>运行应用程序

若要运行您的`gulp serve`应用程序，请使用命令。 这将为您生成并启动一个本地 web 服务器来测试您的应用程序。 当您在项目中保存文件时，该命令也会重新生成应用程序。 

现在，您应该能够浏览到`http://localhost:3007/myFirstAppTab/` ，以确保您的选项卡呈现。 但在 Microsoft 团队中尚不会。

![在浏览器中查看网站](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a>在 Microsoft 团队中运行应用程序

Microsoft 团队不允许您在 localhost 上托管您的应用程序，因此您需要将其发布到公用 URL 或使用代理（如 ngrok）。

好消息是搭建项目具有此内置的。 在运行`gulp ngrok-serve` ngrok 服务时，将在后台启动，并使用唯一的公共 DNS 条目，并将清单打包为该唯一的 URL，然后执行与相同的完全相同的任务`gulp serve`。

运行`gulp ngrok-serve`后，创建一个新的 Microsoft 团队团队，并在创建时单击团队名称，以转到 "团队设置"，然后选择 "*应用*"。 在右下角，您应该会看到一个链接 "*上传自定义应用程序*"，选择它，然后浏览到您的项目`package`文件夹和名为的子文件夹。 选择该文件夹中的 zip 文件，然后选择 "打开"。 现在，您的应用程序将旁加载到 Microsoft 团队中。

![旁加载应用程序](~/assets/yeoman-images/teams-first-app-4.png)

返回到*常规*频道并选择*+* 添加新的选项卡。您应该会在选项卡列表中看到您的选项卡。

![配置选项卡](~/assets/yeoman-images/teams-first-app-5.png)

选择您的选项卡，然后按照说明添加它。 请注意，您有一个自定义配置对话框，您可以在其中编辑该源。 选择 "*保存*" 将选项卡添加到频道。 完成后，应在 Microsoft 团队中加载您的选项卡！

![在团队中运行选项卡](~/assets/yeoman-images/teams-first-app-6.png)

**Congrats!你构建并部署了你的首个 Microsoft 团队应用**
