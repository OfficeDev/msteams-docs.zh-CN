### <a name="_layoutcshtml"></a>_Layout.cshtml

若要在页面中显示选项卡Teams，必须包含 **Microsoft Teams JavaScript** 客户端 SDK，并包括页面加载 `microsoftTeams.initialize()` 后对 的调用。 这是选项卡和客户端Teams的方式：

- 导航到 **"共享** "文件夹，打开 **_Layout.cshtml**，然后向 标记中添加 `<head>` 以下内容：

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

>[!IMPORTANT]
>不要复制/粘贴此页面中的 `<script src="...">` URL，因为它们可能并不代表最新版本。 若要获取最新版本的 SDK，请始终转到[：Microsoft Teams JavaScript API。](https://www.npmjs.com/package/@microsoft/teams-js)

### <a name="tabcshtml"></a>Tab.cshtml

打开 **Tab.cshtml** 并更新嵌入 `<script>` 的内容，如下所示：

- 在脚本顶部，调用 `microsoftTeams.initialize()` 。

- 将每个 `websiteUrl` 函数 `contentUrl` 中的 和 值更新为选项卡的 HTTPS ngrok URL。

现在，您的代码应如下所示，将 **y8rCgT2b** 替换为 ngrok URL：

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

确保保存更新的 **Tab.cshtml**。

## <a name="build-and-run-your-application"></a>生成并运行应用程序

- In Visual Studio press **F5**， or choose **Start Debugging** from the **Debug** menu. 通过打开浏览器，然后通过命令提示符窗口中提供的 ngrok HTTPS URL 进入内容页面，验证 **ngrok** 是否正常运行。

>[!TIP]
>你需要让应用程序在 Visual Studio 和 ngrok 中运行才能完成此快速入门。 如果需要停止运行应用程序，Visual Studio运行 **ngrok。** 当应用程序在服务器中重新启动时，它将继续侦听并Visual Studio。 如果必须重新启动 ngrok 服务，它将返回一个新 URL，并且您必须使用新 URL 更新应用程序。

## <a name="upload-your-tab-to-teams-with-app-studio"></a>Upload选项卡以Teams App Studio

>[!Note]
> 我们使用 App Studio 编辑你的manifest.js **文件**，将已完成的程序包上传到Teams。 如果需要，还可以手动编辑 **manifest.js** 上的文件。 如果这样做，请务必再次构建解决方案，以创建要 **tab.zip** 文件。

- 打开 Microsoft Teams 客户端。 如果使用基于 [Web 的版本，](https://teams.microsoft.com) 可以使用浏览器的开发人员工具检查前端 [代码](~/tabs/how-to/developer-tools.md)。

- 打开 App Studio 并选择清单 **编辑器** 选项卡。

- 选择清单 **编辑器中的** "导入现有应用"磁贴，开始为选项卡更新应用包。源代码附带其自己的部分完整清单。 应用包的名称 **tab.zip。** 应在此处找到它：

```bash
/bin/Debug/netcoreapp2.2/tab.zip
```

- Uploadtab.zipApp  Studio。

### <a name="update-your-app-package-with-manifest-editor"></a>使用清单编辑器更新应用包

将应用包上传到 App Studio 后，你将需要完成它的配置。

- 在清单编辑器欢迎页面的右侧面板中选择新导入选项卡的磁贴。

清单编辑器左侧有一个步骤列表，右侧是一个属性列表，其中每个步骤都需要有值。 大部分信息已由你的manifest.js *提供* ，但是有一些字段需要更新：

#### <a name="details-app-details"></a>详细信息：应用详细信息

- Under *Identification* select ***Generate** _ to replace the placeholder id with the required GUID for your tab.

- 在_Developer信息*下，使用 *ngrok* HTTPS URL 更新"网站 **URL"** 字段。

- 在 *"应用程序 URL"***下，** 使用 *ngrok* HTTPS **URL** 更新隐私声明和使用条款 URL 字段。 请记住，在 URL 的末尾包含 */privacy* 和 */tou* 路径。

#### <a name="capabilities-tabs"></a>功能：选项卡

在" *选项卡"* 部分：

- 在"*团队选项卡"下*，选择"**添加"。**

- 在"团队"选项卡弹出窗口中，将 *"配置 URL"更新* 为 `https://<yourngrokurl>/tab` 。

- 最后，确保 *可以更新配置？选中*"团队"和"*群聊*"框，然后选择"保存 **"。**

#### <a name="finish-domains-and-permissions"></a>完成时间：域和权限

在 *"域和权限"* 部分，选项卡字段中的"域"应包含不包含 HTTPS 前缀的 ngrok URL- `<yourngrokurl>.ngrok.io/` 。

#### <a name="test-and-distribute-test-and-distribute"></a>测试和分发：测试和分发

>[!IMPORTANT]
>在 **右侧** "说明"字段中，你将看到以下警告：
>
>&#9888; "**'validDomains' array cannot contain a tunneling site..."**
>
>在测试选项卡时，可以忽略此警告。

在" *测试和分发"部分* ：

- 选择“**安装**”。

- 在弹出窗口的"添加到团队或聊天"字段中，输入你的团队，然后选择"安装 **"。**

- In the next pop-up window choose the team channel where you would like the tab displayed and select **Set up**.

- 在最终弹出窗口中，选择选项卡页的值 (红色或灰色图标) 保存 **"。**

若要查看您的选项卡，请导航到安装它的团队，然后从选项卡栏中选择它。 应显示在配置期间选择的页面。
