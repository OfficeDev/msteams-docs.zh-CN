## <a name="prerequisites"></a>先决条件

- 若要完成此快速入门，你需要一个Office 365租户和一个配置了"允许上载自定义应用 *"的团队*。 若要了解更多信息，请参阅[准备Office 365租户](~/concepts/build-and-test/prepare-your-o365-tenant.md)。

  - 如果你当前没有Office 365帐户，可以通过开发人员计划注册Office 365订阅。 只要将订阅用于正在进行的开发，订阅就会保持活动状态。 请参阅[欢迎使用 Office 365 开发人员计划](/office/developer-program/microsoft-365-developer-program)。

此外，此项目要求在开发环境中安装以下内容：

- 任何文本编辑器或 IDE。 你可以免费安装和[Visual Studio Code](https://code.visualstudio.com/download)应用程序。

- [Node.js/npm](https://nodejs.org/en/)。 你应该使用最新的 LTS 版本。 Node 程序包管理器 (npm) 将在安装 Node.js 时安装到系统中。

- 在成功安装 Node.js，在命令提示符中键入以下内容来安装 [Yeoman](https://yeoman.io/) 和 [gulp-cli](https://www.npmjs.com/package/gulp-cli) 程序包：

    ```bash
    npm install yo gulp-cli --global
    ```

- 在命令Microsoft Teams键入以下内容，安装应用生成器：

    ```bash
    npm install generator-teams --global
    ```

## <a name="generate-your-project"></a>生成项目

- 打开命令提示符，为选项卡项目创建新目录。

- 若要启动生成器，请导航到新目录并键入以下命令：

    ```bash
    yo teams
    ```

- 接下来，您将提供一系列值，这些值将用于应用程序的 on **manifest.js文件中** ：

    ![生成器打开屏幕截图](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    **你的解决方案名称是什么？**

    这是项目名称。 可以通过按 Enter 接受建议的名称。

    **要将文件存放在哪里?**

    您当前在项目目录中。 按 Enter。

    **你的应用Microsoft Teams标题？**

    这是你的应用包名称，将在应用清单和说明中使用。

    **你的 (公司) 名称？ (最多 32 个字符)**

    你的公司名称将在应用清单中使用。

    **要使用哪个清单版本？**

    选择默认架构。

    **快速基架？ (Y/n)**

    默认值为 yes;输入 **n** 以输入你的 Microsoft 合作伙伴 ID。

    **输入你的 Microsoft 合作伙伴 ID（如果有） (留空可跳过)**

    此字段不是必需的，并且只应在你已是 Microsoft 合作伙伴网络的一 [部分时使用](https://partner.microsoft.com)。

    **要向项目添加哪些内容？**

    选择 &ast; () 选项卡"。

    **将在其中托管此解决方案的 URL？**

    默认情况下，生成器建议 Azure 网站 URL。 你将仅在本地测试你的应用，因此，完成此快速入门不需要有效的 URL。

    **是否包含测试框架和初始测试？ (y/N)**

    选择 **不包括** 此项目的测试框架。 默认值为 yes;输入 **n**。

    **是否对遥测使用 Azure 应用程序见解？ (y/N)**

    选择 **不包括** [Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md)。 默认值为"否";输入 **n**。

    **默认选项卡名称 (最多为 16 个字符) ？**

    命名选项卡。此选项卡名称将在整个项目中用作文件/URL 路径组件。
