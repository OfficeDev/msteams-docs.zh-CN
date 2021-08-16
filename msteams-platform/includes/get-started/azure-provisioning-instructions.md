## <a name="deploy-your-app-to-azure"></a>将应用部署到 Azure

部署包含两个步骤。  首先，创建必要的云资源 (也称为预配) ，然后将应用的代码复制到已创建的云资源中。

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. 打开 Visual Studio 代码。
1. 选择Teams Toolkit图标从边栏选择Teams图标。
1. 选择 **"在云中预配"。**

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="显示设置命令的屏幕截图":::

1. 如果需要，请选择用于 Azure 资源的订阅。

   > [!NOTE]
   > 始终有一些用于托管应用的 Azure 资源。

1. 对话框警告你在 Azure 中运行资源时可能会产生成本。  按 **"设置"。**

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provision-warning.png" alt-text="预配对话框的屏幕截图。":::

   预配过程在 Azure 云中创建资源。 这需要花费一些时间。 可以通过查看右下角的对话框来监视进度。 几分钟后，你将看到以下通知：

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provision-complete.png" alt-text="显示预配完成对话框的屏幕截图。":::

1. 预配完成后，选择"**部署到云"。**  与预配一样，此过程需要一些时间。  可以通过查看右下角的对话框来监视该过程。 几分钟后，你将看到完成通知。

# <a name="command-line"></a>[命令行](#tab/cli)

在终端窗口中：

1. 运行 `teamsfx provision`。

   ``` bash
   teamsfx provision
   ```

   系统可能会提示你登录到 Azure 订阅。 如果需要，系统将提示你选择要用于 Azure 资源的 Azure 订阅。

   > [!NOTE]
   > 始终有一些用于托管应用的 Azure 资源。

1. 运行 `teamsfx deploy`。

   ``` bash
   teamsfx deploy
   ```

---

> [!NOTE]
> **预配和部署之间有什么区别？**
>
> 预配 **步骤** 在 Azure 和 M365 中为应用创建资源， (HTML、CSS、JavaScript 等 ) 代码复制到资源。 **部署** 步骤将应用的代码复制到预配步骤中创建的资源。 通常无需预配新资源即可多次部署。 由于设置步骤可能需要一些时间才能完成，因此该步骤与部署步骤是分开的。

设置和部署步骤完成后：

1. 从Visual Studio Code中，打开调试面板 (**Ctrl+Shift+D**  /  **⌘⇧-D"** 或"查看>**运行**) 
1. 从 **启动 ()** 选择"启动远程部署边缘部署"。
1. 按"播放"按钮启动应用 - 现在从 Azure 远程运行！
