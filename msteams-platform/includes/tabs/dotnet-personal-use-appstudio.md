## <a name="upload-your-tab-to-teams-with-app-studio"></a>将您的选项卡上传给具有应用程序 Studio 的团队

>[!NOTE]
> 我们使用应用程序 Studio 编辑您的**清单 json**文件并将已完成的包上载到团队。 如果愿意，您还可以手动编辑**清单 json** 。 如果这样做，请务必再次生成解决方案，以创建要上载的**Tab .zip**文件。

- 打开 Microsoft 团队客户端。 如果您使用的是[基于 web 的版本](https://teams.microsoft.com)，则可以使用浏览器的[开发人员工具](~/tabs/how-to/developer-tools.md)检查您的前端代码。

- 打开应用程序 studio 并选择 "**清单编辑器**" 选项卡。

- 选择 "在清单编辑器中**导入现有的应用程序**磁贴" 以开始更新选项卡的应用程序包。源代码附带其自己完整的清单。 您的应用程序包的名称为 **"tab .zip**"。 应在此处找到：

```bash
/bin/Debug/netcoreapp2.2/Tab.zip
```

- 将**选项卡**上传到应用程序 Studio。

### <a name="update-your-app-package-with-manifest-editor"></a>使用清单编辑器更新应用程序包

将应用程序包上载到应用程序 Studio 后，需要完成对其进行配置。

- 在清单编辑器的 "欢迎" 页的右面板中，为新导入的选项卡选择磁贴。

清单编辑器的左侧有一个步骤列表，在右侧是需要为每个步骤的值提供值的属性的列表。 大部分信息已由您的*清单 json*提供，但有几个字段需要更新：

#### <a name="details-app-details"></a>详细信息：应用程序详细信息

在 "*应用程序详细信息*" 部分：

- 在 "*标识*" 下，选择 "**生成**" 以生成应用程序的新应用 Id。

- 在 "*开发人员信息*" 下，使用您的*ngrok* HTTPS url 更新**网站 URL** 。

- 在 *"应用程序 url* " 下， `https://<yourngrokurl>/privacy`更新**隐私声明**，并将`https://<yourngrokurl>/tou` **使用条款**更新为>。

#### <a name="capabilities-tabs"></a>功能：选项卡

在 "*选项卡*" 部分：

- 在 "*添加个人选项卡*" 下，选择 "***添加***"。 将显示一个弹出对话框窗口。

- 填写 "*名称*" 字段。

- 填写 "*实体 Id* " 字段。

- 使用将*内容 URL*字段更新为`https://<yourngrokurl>/personalTab`。

- 将 "*网站 URL* " 字段保留为空。

- 选择“***保存***”。

#### <a name="finish-domains-and-permissions"></a>完成：域和权限

在 "*域和权限*" 部分中，"*选项卡*" 字段中的域应包含不带 HTTPS 前缀`<yourngrokurl>.ngrok.io/`的 ngrok URL。

##### <a name="finish-test-and-distribute"></a>完成：测试和分发

>[!IMPORTANT]
>在右侧的 "**说明**" 字段中，将看到以下警告：
>
>&#9888; "**validDomains" 数组不能包含隧道站点 ...**"
>
>在测试选项卡时可以忽略此警告。

在 "*测试和分发*" 部分：

- 选择“**安装**”。

- 在弹出窗口中，请确保将 "*添加*到" 设置为 *"是"* ，并*将 "添加到团队" 或 "聊天*" 设置为 "*否*"。

- 选择“**安装**”。

- 在下一个弹出窗口中，选择 "**打开**"，您的选项卡将显示出来。

## <a name="view-your-personal-tab"></a>查看您的个人选项卡

- 在位于 "团队" 应用程序最左侧的导航栏中，选择 "" `...`菜单。 将显示个人应用程序的列表。

- 从列表中选择要查看的选项卡。
