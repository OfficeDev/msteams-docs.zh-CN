## <a name="deploy-your-app-to-azure"></a>将应用部署到 Azure。

部署包括两个步骤。  首先，创建必要的云资源 (也称为预配) 。 然后，应用的代码将复制到创建的云资源中。 在本教程中，你将部署选项卡应用。
<br> 
<br>
<details>
<summary>预配和部署有什么区别？</summary>
<br>
“<b>预配</b>”步骤在 Azure 中创建资源，并为应用Microsoft 365，但不会将 HTML、CSS、JavaScript 等代码 () 复制到资源。 “ <b>部署</b> ”步骤将应用的代码复制到预配步骤中创建的资源。 在不预配新资源的情况下多次部署是很常见的。 由于预配步骤可能需要一些时间才能完成，因此它与部署步骤是分开的。
</details>
<br>

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

在 Visual Studio Code 边栏中选择 Teams 工具包 :::image type="icon" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png"::: 图标。

1. 在 **云中选择“预配**”。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="显示预配命令的屏幕截图" border="false":::

1. 选择要用于 Azure 资源的订阅。

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/select-resource.png" alt-text="显示用于预配的资源的屏幕截图" border="false":::

   > [!NOTE]
   > 始终有一些用于托管应用的 Azure 资源。

    对话框警告在 Azure 中运行资源时可能会产生成本。

1. 选择 **“预配**”。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provision-warning.png" alt-text="预配对话框的屏幕截图。" border="true":::

   预配过程在 Azure 云中创建资源。 这可能需要一些时间。 可以通过查看右下角的对话来监视进度。 几分钟后，你会看到以下通知：

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-provision-successmsg.png" alt-text="显示预配完成对话框的屏幕截图。" border="false":::

    如果需要，可以查看预配的资源。 在本教程中，无需查看资源。

    预配的资源显示在 **“环境** ”部分。

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provisioned-resources-env.png" alt-text="显示预配完成对话框的屏幕截图。" border="false":::

1. 预配完成后，从 **部署** 面板中选择 **“部署到云**”。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-cloud.png" alt-text="显示要单击到云的部署位置的屏幕截图。" border="false":::

   与预配一样，部署需要一些时间。 可以通过查看右下角的对话来监视过程。 几分钟后，你将看到完成通知。

现在，可以使用相同的过程将机器人和消息扩展应用部署到 Azure。

# <a name="command-line"></a>[命令行](#tab/cli)

在终端窗口中：

1. 运行 `teamsfx provision`。

   ``` bash
   teamsfx provision
   ```

   出现提示时，选择 Azure 订阅以使用 Azure 资源。

   > [!NOTE]
   > 始终有一些用于托管应用的 Azure 资源。

1. 运行 `teamsfx deploy`。

   ``` bash
   teamsfx deploy
   ```

---

## <a name="run-the-deployed-app"></a>运行已部署的应用

完成预配和部署步骤后：

1. 打开调试面板 (**Ctrl+Shift+D** / ⌘⇧ **-D** 或 **视图>** 从Visual Studio Code运行) 。
1. 从启动配置下拉列表中选择 **“启动远程 (Edge)** ”。
1. 选择 **"开始"菜单调试 (F5)** 从 Azure 启动应用。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/launch-remote.png" alt-text="显示远程启动应用的屏幕截图。" border="false":::

1. 选择“**添加**”。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/add-mex-app.png" alt-text="显示正在安装的应用的屏幕截图。" border="false":::

   该工具包显示一条消息，指示应用已添加到Teams。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/mex-added-msg.png" alt-text="屏幕截图显示立即或更高版本尝试应用的消息" border="true":::
 
    - 如果选择 **“获取”**，可以稍后从旁加载应用列表中试用该应用。
    - 如果选择 **“试用**”，Teams加载应用。

   你的应用在 Azure 网站上加载。
   
1. 选择 **“试用**”。

   消息扩展应用在聊天机器人应用中加载。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/app-added-mex1.png" alt-text="显示在Teams中旁加载的应用的屏幕截图" border="false":::


