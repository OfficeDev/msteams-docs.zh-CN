## <a name="deploy-your-app-to-azure"></a>将应用部署到 Azure

部署包含两个步骤。  首先，创建必要的云资源 (也称为预配) 。 然后，你的应用的代码将复制到已创建的云资源中。 在本教程中，你将部署选项卡应用。

> <details>
> <summary>预配和部署之间有什么区别？</summary>
>
> 预配 **步骤** 在 Azure 和 Microsoft 365 中为你的应用创建资源， (HTML、CSS、JavaScript 等 ) 代码复制到资源。 **部署** 步骤将应用的代码复制到预配步骤中创建的资源。 通常无需预配新资源即可多次部署。 由于设置步骤可能需要一些时间才能完成，因此该步骤与部署步骤是分开的。
</details>

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

在 Visual Studio Code 边栏中选择 Teams 工具包 :::image type="icon" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png"::: 图标。

1. 选择 **"在云中预配"**。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="显示设置命令的屏幕截图" border="false":::

1. 选择要用于 Azure 资源的订阅。

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/select-resource.png" alt-text="显示用于预配的资源的屏幕截图" border="false":::

   > [!NOTE]
   > 始终有一些用于托管应用的 Azure 资源。

    对话框警告你在 Azure 中运行资源时可能会产生成本。

1. 选择 **"预配"**。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provision-warning.png" alt-text="预配对话框的屏幕截图。" border="false":::

   预配过程在 Azure 云中创建资源。 可能需要一些时间。 可以通过查看右下角的对话框来监视进度。 几分钟后，你将看到以下通知：

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-provision-success.png" alt-text="显示预配完成对话框的屏幕截图。" border="false":::

    如果需要，可以查看预配的资源。 对于本教程，你无需查看资源。

    预配的资源将显示在"环境 **"** 部分。

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provisioned-resources-env.png" alt-text="显示预配完成对话框的屏幕截图。" border="false":::

1. 预配 **完成后，** 从部署面板 **中选择** "部署到云"。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-cloud.png" alt-text="Screenshot showing the where to click to deploy to cloud." border="false":::

   与预配一样，部署需要一些时间。 可以通过查看右下角的对话框来监视该过程。 几分钟后，你将看到完成通知。

现在，你可以使用相同的过程将自动程序应用和邮件扩展应用部署到 Azure。

# <a name="command-line"></a>[命令行](#tab/cli)

在终端窗口中：

1. 运行 `teamsfx provision`。

   ``` bash
   teamsfx provision
   ```

   当系统提示时，选择 Azure 订阅以使用 Azure 资源。

   > [!NOTE]
   > 始终有一些用于托管应用的 Azure 资源。

1. 运行 `teamsfx deploy`。

   ``` bash
   teamsfx deploy
   ```

---

## <a name="run-the-deployed-app"></a>运行已部署的应用

设置和部署步骤完成后：

1. 打开调试面板 (**Ctrl+Shift+D** / **⌘⇧-D****"或**"查看>从) 运行Visual Studio Code。
1. 从 **启动 ()** "选择"启动远程部署边缘部署"。
1. 选择"播放"按钮以从 Azure 启动应用。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/launch-remote.png" alt-text="显示远程启动应用的屏幕截图。" border="false":::

1. 选择“**添加**”。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/remote-app-client.png" alt-text="显示要安装的应用的屏幕截图。" border="false":::

   你的应用在 Azure 网站上加载。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/azure-deployed-app.png" alt-text="显示要安装的应用的屏幕截图。" border="false":::

    恭喜！ 你的选项卡应用现在从 Azure 远程运行！
