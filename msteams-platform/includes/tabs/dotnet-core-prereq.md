## <a name="prerequisites"></a>先决条件

- 若要完成此快速入门，你需要一个Microsoft 365租户和一个配置了"允许上载自定义应用 *"的团队*。 若要了解更多信息，请参阅[准备Microsoft 365租户。](~/concepts/build-and-test/prepare-your-o365-tenant.md)
  - 如果你当前没有Microsoft 365帐户，可以通过 Microsoft 开发人员计划注册免费[订阅](https://developer.microsoft.com/en-us/microsoft-365/dev-program)。 只要将订阅用于正在进行的开发，订阅就会保持活动状态。

- 你将使用 App Studio 将应用程序导入到Teams。 若要安装 App  Studio，请选择应用应用商店应用（位于 Teams 应用左下 ![ ](~/assets/images/tab-images/storeApp.png) 角）并搜索 App Studio。 找到磁贴后，选择该磁贴，然后选择弹出窗口对话框中的"安装"。

此外，此项目要求在开发环境中安装以下内容：

- 当前版本 IDE Visual Studio **安装 .NET CORE 跨平台开发** 工作负载。 如果尚未安装Visual Studio，可免费下载和安装[Microsoft Visual Studio Community版本。](https://visualstudio.microsoft.com/downloads)

- [ngrok](https://ngrok.com)反向代理工具。 将使用 ngrok 创建到本地运行的 Web 服务器的公开可用的 HTTPS 终结点的隧道。 你可以 [在此处下载它](https://ngrok.com/download)。
