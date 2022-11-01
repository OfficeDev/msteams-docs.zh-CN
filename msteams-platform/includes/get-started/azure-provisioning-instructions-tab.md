## <a name="deploy-your-app-to-azure"></a>将应用部署到 Azure。

部署包括两个步骤。 首先， (也称为预配) 创建必要的云资源。 然后，应用的代码将复制到创建的云资源中。 在本教程中，你将部署选项卡应用。
<br>
<br>
<details>
<summary>预配和部署之间有什么区别？</summary>
<br>
<b>预配</b>步骤在 Azure 和 Microsoft 365 中为应用创建资源，但不会 (HTML、CSS、JavaScript 等代码) 复制到资源。 <b>部署</b>步骤将应用的代码复制到预配步骤期间创建的资源。 无需预配新资源即可多次部署，这很常见。 由于预配步骤可能需要一些时间才能完成，因此它与部署步骤是分开的。
</details>
<br>

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

在 Visual Studio Code 边栏中选择 Teams 工具包 :::image type="icon" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png"::: 图标。

1. 选择“ **在云中预配**”。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="显示预配命令的屏幕截图":::

1. 选择现有订阅中的任何一个。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/select-subscription.png" alt-text="显示现有订阅选择的屏幕截图":::

1. 选择要用于 Azure 资源的资源组。

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/select-resource.png" alt-text="显示用于预配的资源的屏幕截图":::

   > [!NOTE]
   > 应用使用 Azure 资源进行托管。
   >
   >有关详细信息，请参阅 [创建资源组。](/azure/azure-resource-manager/management/manage-resource-groups-portal)

    一个对话框警告你在 Azure 中运行资源时可能会产生成本。

1. 选择“ **预配**”。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provision-warning.png" alt-text="显示对话框预配的屏幕截图。":::

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provision-confirm1.png" alt-text="显示订阅选择的屏幕截图。":::

   预配过程在 Azure 云中创建资源。 这可能需要一些时间。 可以通过观看右下角的对话来监视进度。 几分钟后，会看到以下通知：

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-provision-successmsgext.png" alt-text="显示资源在云中成功预配的屏幕截图。":::

    如果需要，可以查看预配的资源。 在本教程中，无需查看资源。

    预配的资源将显示在 **“环境** ”部分中。

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provisioned-resources-env.png" alt-text="显示预配资源的屏幕截图。":::

1. 预配完成后，从 **“部署**”面板中选择“**部署到云**”。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-cloud.png" alt-text="显示部署到云的屏幕截图。":::

   与预配一样，部署需要一些时间。 可以通过观看右下角的对话来监视该过程。 几分钟后，你将看到完成通知。

现在，可以使用同一过程将机器人和消息扩展应用部署到 Azure。

# <a name="command-line"></a>[命令行](#tab/cli)

在终端窗口中：

1. 运行 `teamsfx provision`。

   ``` bash
   teamsfx provision
   ```

   出现提示时，选择 Azure 订阅以使用 Azure 资源。

1. 运行 `teamsfx deploy`。

   ``` bash
   teamsfx deploy
   ```

---

> [!NOTE]
> 应用使用 Azure 资源进行托管。

## <a name="run-the-deployed-app"></a>运行已部署的应用

完成预配和部署步骤后：

1. 打开调试面板 (**Ctrl+Shift+D** / **⌘⇧-D** 或 **查看>** 从Visual Studio Code运行) 。
1. 从启动配置下拉列表中选择“ **启动远程 (Edge)** ”。
1. 选择“ **开始调试 (F5)** 从 Azure 启动应用。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/launch-remote.png" alt-text="显示如何远程启动应用的屏幕截图。":::

1. 当系统提示将应用旁加载到 Teams 时，选择“ **添加** ”。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/remote-app-client.png" alt-text="显示正在安装的应用的屏幕截图。":::

    恭喜，你的第一个选项卡应用正在 Azure 环境中运行！

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/azure-deployed-apptab.png" alt-text="显示立即或稍后试用应用的消息的屏幕截图。":::
