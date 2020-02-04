## <a name="prerequisites"></a>先决条件

- 若要完成此快速入门，你将需要 Office 365 租户和配置了 "*允许上载自定义应用程序*" 的团队。 若要了解详细信息，请参阅[准备 Office 365 租户](~/concepts/build-and-test/prepare-your-o365-tenant.md)。
  - 如果当前没有 Office 365 帐户，可以通过[office 365 开发人员计划](/OfficeDev/office-dev-program-docs/docs/office-365-developer-program)注册免费订阅。 只要您使用它进行持续开发，订阅将保持活动状态。

- 你将使用应用程序 Studio 将应用程序导入到团队。 若要在团队应用程序的左下](~/assets/images/tab-images/storeApp.png)角安装应用程序 Studio 选择**应用** ![商店应用程序，请搜索应用程序 studio。 找到该磁贴后，选择它并在弹出窗口对话框中选择 "安装"。

此外，此项目要求在开发环境中安装以下各项：

- 安装了 **.NET CORE 跨平台开发**工作负载的 VISUAL Studio IDE 的当前版本。 如果你还没有 Visual Studio，可以免费下载并安装最新的[Microsoft Visual Studio 社区](https://visualstudio.microsoft.com/downloads)版本。

- [Ngrok](https://ngrok.com)反向代理工具。 您将使用 ngrok 创建到本地运行的 web 服务器的公开可用 HTTPS 终结点的隧道。 你可以[在此处下载它](https://ngrok.com/download)。
