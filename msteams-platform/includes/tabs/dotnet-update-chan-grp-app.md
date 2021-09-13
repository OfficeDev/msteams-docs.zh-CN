### <a name="_layoutcshtml"></a>_Layout.cshtml

若要在页面中显示选项卡Teams，必须包含 **Microsoft Teams JavaScript** 客户端 SDK，并包括页面加载后的 `microsoftTeams.initialize()` 调用。 这是选项卡和客户端Teams的方式：

转到" **共享"** 文件夹，打开 **_Layout.cshtml，** 然后向 标记中添加 `<head>` 以下内容：

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

>[!IMPORTANT]
> 不要复制并粘贴此页 `<script src="...">` 中的 URL，因为它们可能并不表示最新版本。 若要获取最新版本的 SDK，请始终转到[Microsoft Teams JavaScript API。](https://www.npmjs.com/package/@microsoft/teams-js)

### <a name="tabcshtml"></a>Tab.cshtml

**更新嵌入的脚本**

1. 在Visual Studio中，打开 **Tab.cshtml** 以更新嵌入的 `<script>` 。

1. 在脚本顶部，调用 `microsoftTeams.initialize()` 。

1. 将每个 `websiteUrl` 函数 `contentUrl` 中的 和 值更新为选项卡的 HTTPS ngrok URL。

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

1. 确保保存更新的 **Tab.cshtml**。

## <a name="build-and-run-your-application"></a>生成并运行应用程序

In Visual Studio， press **F5** or choose **Start Debugging** from the **Debug** menu. 通过打开浏览器，然后通过命令提示符窗口中提供的 ngrok HTTPS URL 进入内容页面，验证 **ngrok** 是否正常运行。

> [!TIP]
> 你需要让应用程序在 Visual Studio 和 ngrok 中运行。 如果你需要停止运行应用程序，Visual Studio它使 **ngrok 保持运行**。 当应用程序在服务器中重新启动时，它将继续侦听并Visual Studio。 如果必须重新启动 ngrok 服务，它将返回一个新 URL，并且您必须使用新 URL 更新应用程序。

## <a name="upload-your-tab"></a>Upload选项卡

>[!Note]
> App Studio 可用于编辑 **文件上的** manifest.js，将已完成的程序包上传到Teams。 如果需要，还可以手动编辑 **manifest.js上的** 文件。 如果这样做，请务必再次生成解决方案，以创建要 **tab.zip** 文件。

**上传选项卡**

1. 转到Microsoft Teams。 如果使用基于 [Web 的版本，](https://teams.microsoft.com) 可以使用浏览器的开发人员工具检查前端 [代码](~/tabs/how-to/developer-tools.md)。

1. 转到 **App Studio** 并选择清单 **编辑器** 选项卡。

1. 在 **清单编辑器中选择** 导入现有应用，开始更新选项卡的应用包。源代码附带其自己的部分完整清单。 应用包的名称 **tab.zip。** 它在此处提供：

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. Uploadtab.zipApp  Studio。

### <a name="update-your-app-package-with-manifest-editor"></a>使用清单编辑器更新应用包

将应用包上传到 App Studio 后，必须完成配置。

在清单编辑器欢迎页面的右侧面板中选择新导入选项卡的磁贴。

清单编辑器左侧有一个步骤列表，右侧是一个属性列表，其中每个步骤都必须具有值。 大部分信息已由你的用户manifest.js，但是有一些字段必须更新：

#### <a name="details-app-details"></a>详细信息：应用详细信息

在" **应用详细信息"** 部分：

1. 在 **"标识****"下**，选择"生成"以将占位符 ID 替换为选项卡所需的 GUID。

1. 在 **"开发人员信息**" **下，使用** **ngrok** HTTPS URL 更新网站。

1. 在 **"应用程序 URL"** 下，将隐私声明更新为 和 `https://<yourngrokurl>/privacy` **使用条款** 以 `https://<yourngrokurl>/tou`>。

#### <a name="capabilities-tabs"></a>功能：选项卡

在" **选项卡"** 部分：

1. 在"**团队"选项卡** 下，选择"**添加"。**

1. 在" **团队"选项卡** 弹出窗口中，将" **配置 URL"更新** 为 `https://<yourngrokurl>/tab` 。

1. 确保选中 **了"可以更新配置****？"、"团队**"和"**群聊**"复选框，然后选择"保存 **"。**

#### <a name="finish-domains-and-permissions"></a>完成时间：域和权限

在" **域和权限"** 部分， **选项卡中的** "域"必须包含不带 HTTPS 前缀的 ngrok `<yourngrokurl>.ngrok.io/` URL。

#### <a name="finish-test-and-distribute"></a>完成：测试和分发

>[!IMPORTANT]
> 在右侧，在 **"说明"** 中，你将看到以下警告：
>
> &#9888; "**'validDomains' array cannot contain a tunneling site..."**
>
> 在测试您的选项卡时，可以忽略此警告。

1. 在"**测试和分发"部分**，选择"安装 **"。**

1. 在弹出对话框中，选择"添加到团队"或从下拉列表中选择"**添加到聊天"。**

1. 选择要显示选项卡的团队或聊天，然后选择"**设置选项卡"。**

1. 在下一个弹出对话框中，**选择"选择** 灰色"或"**选择红色**"，然后选择"保存 **"。**

1. 若要查看您的选项卡，请转到您安装选项卡的团队，然后从选项卡栏中选择它。 将显示在配置过程中选择的页面。

    ![频道选项卡 ASPNETMVC 已上载](../../assets/images/tab-images/channeltabaspnetmvcuploaded.png)

