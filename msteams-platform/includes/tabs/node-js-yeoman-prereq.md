## <a name="prerequisites"></a>先决条件

- 若要完成此快速入门，你将需要 Office 365 租户和配置了 "*允许上载自定义应用程序*" 的团队。 若要了解详细信息，请参阅[准备 Office 365 租户](~/concepts/build-and-test/prepare-your-o365-tenant.md)。

  - 如果当前没有 Office 365 帐户，可以通过 Office 365 开发人员计划注册免费订阅。 只要您使用它进行持续开发，订阅将保持活动状态。 请参阅[欢迎使用 Office 365 开发人员计划](/OfficeDev/office-dev-program-docs/docs/office-365-developer-program.md)。

此外，此项目要求在开发环境中安装以下各项：

- 任何文本编辑器或 IDE。 您可以免费安装和使用[Visual Studio Code](https://code.visualstudio.com/download) 。

- [Node.js/npm](https://nodejs.org/en/)。 应使用最新的 LTS 版本。 节点包管理器（npm）将在安装 node.js 的情况中安装到系统中。

- 成功安装 node.js 后，在命令提示符处键入以下命令，以安装[Yeoman](https://yeoman.io/)和[gulp](https://www.npmjs.com/package/gulp-cli)程序包：

```bash
npm install yo gulp-cli --global
```

- 通过在命令提示符处键入以下内容来安装 Microsoft 团队应用生成器：

```bash
npm install generator-teams --global
```

## <a name="generate-your-project"></a>生成项目

- 打开命令提示符并为您的选项卡项目创建一个新目录。

- 若要启动生成器，请导航到新目录并键入以下命令：

```bash
yo teams
```

- 接下来，你将提供将在应用程序的**清单 json**文件中使用的一系列值：

![生成器打开屏幕截图](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

**您的解决方案名称是什么？**

这是您的项目名称。 您可以按 enter 接受建议的名称。

**要将文件存放在哪里?**

您当前位于项目目录中。 按 enter。

**Microsoft 团队应用程序项目的标题？**

这是您的应用程序包名称，将在应用程序清单和说明中使用。

**您的（公司）名称？（最多32个字符）**

你的公司名称将在应用部件清单（manifest）中使用。

<br>**您要使用哪个清单版本？**

选择默认架构。

**如果你有一个，请输入你的 Microsoft 合作伙伴 Id？（保留为空将跳过）**

此字段不是必需的，仅当您已经是[Microsoft 合作伙伴网络](https://partner.microsoft.com)的一部分时才应使用此字段。

**您想要将什么添加到你的项目？**

选择 " &ast; （）" 选项卡。

**你将在其中承载此解决方案的 URL？**

默认情况下，生成器会建议使用 Azure 网站 URL。 您只会在本地测试您的应用程序，因此，不需要使用有效的 URL 即可完成此快速入门。

**是否要包括测试框架和初始测试？（y/N）**

选择**不**包含此项目的测试框架。 默认值为 "是";输入**n**。

**您是否要使用适用于遥测的 Azure 应用程序见解？（y/N）**

选择**不**包含[Azure application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md)。 默认值为 no;输入**n**。

**默认选项卡名称（最多16个字符）？**

命名您的选项卡。此选项卡名称将在整个项目中用作文件/URL 路径组件。
