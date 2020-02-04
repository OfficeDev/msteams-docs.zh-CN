### <a name="_layoutcshtml"></a>_Layout cshtml

若要在团队中显示您的选项卡，您必须包含**Microsoft 团队 JavaScript 客户端 SDK** ，并`microsoftTeams.initialize()`在加载页面后包含一个调用。 这就是选项卡和团队客户端之间的通信方式：

- 导航到**共享**文件夹，打开 **_Layout. cshtml**，并将以下内容添加到`<head>`标记：

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

>[!IMPORTANT]
>请勿复制/粘贴此`<script src="...">`页面中的 url，因为它们可能不代表最新版本。 若要获取最新版本的 SDK，请始终转到： [Microsoft 团队 JAVASCRIPT API](https://www.npmjs.com/package/@microsoft/teams-js.com)。

### <a name="tabcshtml"></a>选项卡. cshtml

打开**选项卡. cshtml**并更新嵌入`<script>`的，如下所示：

- 在脚本的顶部，调用`microsoftTeams.initialize()`。

- 使用 HTTPS `websiteUrl` ngrok `contentUrl` URL 将每个函数中的和值更新到您的选项卡。

您的代码现在应如下所示， **y8rCgT2b**替换为您的 ngrok URL：

```javascript
    microsoftTeams.initialize();

    let saveGray = () => {
        microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
            microsoftTeams.settings.setSettings({
                websiteUrl: `https://y8rCgT2b.ngrok.io`,
                contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                entityId: "grayIconTab",
                suggestedDisplayName: "MyNewTab"
            });
            saveEvent.notifySuccess();
        });
    }

    let saveRed = () => {
        microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
            microsoftTeams.settings.setSettings({
                websiteUrl: `https://y8rCgT2b.ngrok.io`,
                contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                entityId: "redIconTab",
                suggestedDisplayName: "MyNewTab"
            });
            saveEvent.notifySuccess();
        });
    }
```

请务必保存更新的**选项卡. cshtml**。

## <a name="build-and-run-your-application"></a>生成并运行应用程序

- 在 Visual Studio 中按**F5**，或从 "**调试**" 菜单中选择 "**启动调试**"。 通过在命令提示符窗口中提供的 ngrok HTTPS URL 打开浏览器并转到内容页，验证**ngrok**是否正在运行并正常运行。

>[!TIP]
>您需要在 Visual Studio 和 ngrok 中同时运行应用程序，才能完成此快速入门。 如果需要在 Visual Studio 中停止运行应用程序以使用它，**请继续运行 ngrok**。 它将继续侦听，并将在 Visual Studio 中重新启动时继续路由应用程序的请求。 如果您必须重新启动 ngrok 服务，它将返回一个新的 URL，您必须使用新的 URL 更新应用程序。

## <a name="upload-your-tab-to-teams-with-app-studio"></a>将您的选项卡上传给具有应用程序 Studio 的团队

>[!Note]
> 我们使用应用程序 Studio 编辑您的**清单 json**文件并将已完成的包上载到团队。 如果愿意，也可以手动编辑**清单 json**文件。 如果这样做，请务必再次生成解决方案，以创建要上载的**tab .zip**文件。

- 打开 Microsoft 团队客户端。 如果您使用的是[基于 web 的版本](https://teams.microsoft.com)，则可以使用浏览器的[开发人员工具](~/tabs/how-to/developer-tools.md)检查您的前端代码。

- 打开应用程序 studio 并选择 "**清单编辑器**" 选项卡。

- 选择 "在清单编辑器中**导入现有的应用程序**磁贴" 以开始更新选项卡的应用程序包。源代码附带其自己完整的清单。 您的应用程序包的名称为 **"tab .zip**"。 应在此处找到：

```bash
/bin/Debug/netcoreapp2.2/tab.zip
```

- 将**选项卡**上传到应用程序 Studio。

### <a name="update-your-app-package-with-manifest-editor"></a>使用清单编辑器更新应用程序包

将应用程序包上载到应用程序 Studio 后，需要完成对其进行配置。

- 在清单编辑器的 "欢迎" 页的右面板中，为新导入的选项卡选择磁贴。

清单编辑器的左侧有一个步骤列表，在右侧是需要为每个步骤的值提供值的属性的列表。 大部分信息已由您的*清单 json*提供，但有几个字段需要更新：

#### <a name="details-app-details"></a>详细信息：应用程序详细信息

- 在 "*标识*" 下，选择 "***生成***" 以将占位符 id 替换为您的选项卡所需的 GUID。

- 在 "*开发人员信息*" 下，使用您的*ngrok* HTTPS URL 更新**网站 URL**字段。

- 在 "*应用程序 url* " 下，使用您的*ngrok* HTTPS Url 更新**隐私声明**和**使用条款**url 字段。 请记住将 */privacy*和 */tou*路径包含在 url 的末尾。

#### <a name="capabilities-tabs"></a>功能：选项卡

在 "*选项卡*" 部分：

- 在 "*团队" 选项卡*下选择 "**添加**"。

- 在 "团队" 选项卡弹出窗口中，将*配置 URL*更新为`https://<yourngrokurl>/tab`。

- 最后，请确保*可以更新配置？* 将选中 "团队" 和 "*组" 聊天*框，然后选择 "**保存**"。

#### <a name="finish-domains-and-permissions"></a>完成：域和权限

在 "*域和权限*" 部分中，"*选项卡*" 字段中的域应包含不带 HTTPS 前缀`<yourngrokurl>.ngrok.io/`的 ngrok URL。

#### <a name="test-and-distribute-test-and-distribute"></a>测试和分发：测试和分发

>[!IMPORTANT]
>在右侧的 "**说明**" 字段中，将看到以下警告：
>
>&#9888; "**validDomains" 数组不能包含隧道站点 ...**"
>
>在测试选项卡时可以忽略此警告。

在 "*测试和分发*" 部分：

- 选择“**安装**”。

- 在弹出窗口的 "*添加到团队" 或 "聊天*" 字段中，输入您的团队并选择 "**安装**"。

- 在下一个弹出窗口中，选择要在其中显示选项卡的团队频道，然后选择 "**设置**"。

- 在最终弹出窗口中，选择选项卡页的值（红色或灰色图标），然后选择 "**保存**"。

若要查看您的选项卡，请导航到安装它的团队，然后从选项卡栏中选择它。 应显示在配置过程中选择的页面。
