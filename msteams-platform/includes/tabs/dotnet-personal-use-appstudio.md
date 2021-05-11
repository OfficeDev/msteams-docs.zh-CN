## <a name="upload-your-tab-to-teams-with-app-studio"></a>Upload选项卡以Teams App Studio

>[!NOTE]
> 我们使用 App Studio 编辑你的manifest.js **文件**，将已完成的程序包上传到Teams。 如果需要，还可以手动 **编辑manifest.js** 打开。 如果这样做，请务必再次构建解决方案，以创建要 **Tab.zip** 文件。

- 打开 Microsoft Teams 客户端。 如果使用基于 [Web 的版本，](https://teams.microsoft.com) 可以使用浏览器的开发人员工具检查前端 [代码](~/tabs/how-to/developer-tools.md)。

- 打开 App Studio 并选择清单 **编辑器** 选项卡。

- 选择清单 **编辑器中的** "导入现有应用"磁贴，开始为选项卡更新应用包。源代码附带其自己的部分完整清单。 应用包的名称 **tab.zip。** 应在此处找到它：

```bash
/bin/Debug/netcoreapp2.2/Tab.zip
```

- UploadTab.zipApp  Studio。

### <a name="update-your-app-package-with-manifest-editor"></a>使用清单编辑器更新应用包

将应用包上传到 App Studio 后，你将需要完成它的配置。

- 在清单编辑器欢迎页面的右侧面板中选择新导入选项卡的磁贴。

清单编辑器左侧有一个步骤列表，右侧是一个属性列表，其中每个步骤都需要有值。 大部分信息已由你的manifest.js *提供* ，但是有一些字段需要更新：

#### <a name="details-app-details"></a>详细信息：应用详细信息

在" *应用详细信息"* 部分中：

- 在 *"标识***"下，** 选择"生成"，为应用生成新的应用 ID。

- 在 *"开发人员信息* "下 **，** 使用 *ngrok* HTTPS URL 更新网站 URL。

- 在 *"应用程序 URL"* 下 **，将隐私声明** 更新为 `https://<yourngrokurl>/privacy` 和 **使用条款** 以 `https://<yourngrokurl>/tou`>。

#### <a name="capabilities-tabs"></a>功能：选项卡

在" *选项卡"* 部分：

- 在 *"添加个人"选项卡下，选择*"***添加"。*** 系统将会显示一个弹出对话窗口。

- 填写" *名称"* 字段。

- 完成 *"实体 ID"* 字段。

- 将" *内容 URL"* 字段更新为 `https://<yourngrokurl>/personalTab` 。

- 将" *网站 URL"* 字段留空。

- 选择“***保存***”。

#### <a name="finish-domains-and-permissions"></a>完成时间：域和权限

在 *"域和权限"* 部分，选项卡字段中的"域"应包含不包含 HTTPS 前缀的 ngrok URL- `<yourngrokurl>.ngrok.io/` 。

##### <a name="finish-test-and-distribute"></a>完成：测试和分发

>[!IMPORTANT]
>在 **右侧** "说明"字段中，你将看到以下警告：
>
>&#9888; "**'validDomains' array cannot contain a tunneling site..."**
>
>在测试选项卡时，可以忽略此警告。

在" *测试和分发"部分* ：

- 选择“**安装**”。

- 在弹出窗口中，确保"为用户添加"设置为"是"，"添加到团队或 *聊天"设置为*"否 *"。* 

- 选择“**安装**”。

- In the next pop-up window select **Open** and your tab will be displayed.

## <a name="view-your-personal-tab"></a>查看个人选项卡

- 在位于应用最左侧的导航栏中，Teams菜单 `...` 。 你将看到个人应用列表。

- 从列表中选择要查看的选项卡。
