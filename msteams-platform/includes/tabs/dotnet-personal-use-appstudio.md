## <a name="upload-your-tab-with-app-studio"></a>Upload App Studio 打开选项卡

>[!NOTE]
> 我们使用 **App Studio** 编辑 **你的manifest.js** 文件，将已完成的程序包上传到Teams。 还可以在 上手动 **manifest.js文件**。 如果这样做，请确保再次生成解决方案以创建要 **Tab.zip文件。**

**使用 App Studio 上传选项卡**

1. 转到Microsoft Teams。 如果使用基于 [Web 的版本，](https://teams.microsoft.com) 可以使用浏览器的开发人员工具检查前端 [代码](~/tabs/how-to/developer-tools.md)。

1. 转到 **App Studio，** 然后选择清单 **编辑器** 选项卡。

1. 选择 **"在清单编辑器** 中导入现有 **应用"** 开始为选项卡更新应用包。源代码附带其自己的部分完整清单。 应用包的名称 **tab.zip。** 可从以下路径获得：

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. Uploadtab.zipApp  **Studio。**

### <a name="update-your-app-package-with-manifest-editor"></a>使用清单编辑器更新应用包

将应用包上传到 App Studio 后，必须对其进行配置。

在清单编辑器欢迎页面的右侧面板中选择新导入选项卡的磁贴。

清单编辑器左侧有一个步骤列表，右侧是一个属性列表，其中每个步骤都必须具有值。 大部分信息已由你的用户 **manifest.js，但** 有些字段必须更新。

#### <a name="details-app-details"></a>详细信息：应用详细信息

在" **应用详细信息"** 部分中：

1. 在 **"标识**" **下，** 选择"生成"为应用生成新的应用 ID。

1. 在 **"开发人员信息**"下，使用 **ngrok** HTTPS URL 更新网站。

1. 在 **"应用程序 URL"** 下，将隐私声明更新为 和 `https://<yourngrokurl>/privacy` **使用条款** 以 `https://<yourngrokurl>/tou`>。

#### <a name="capabilities-tabs"></a>功能：选项卡

在" **选项卡"** 部分：

1. 在 **"添加个人"选项卡下**，选择"**添加"。** 将出现一个弹出对话框。

1. 在名称 中输入个人选项卡 **的名称**。

1. 输入实体 **ID**。

1. 使用 **更新内容** `https://<yourngrokurl>/personalTab` URL。

    将" **网站 URL"** 字段留空。

1. 选择“**保存**”。

#### <a name="finish-domains-and-permissions"></a>完成时间：域和权限

在"**域和权限"** 部分，选项卡字段中的"域"必须包含不带 HTTPS 前缀的 ngrok `<yourngrokurl>.ngrok.io/` URL。

##### <a name="finish-test-and-distribute"></a>完成：测试和分发

>[!IMPORTANT]
> 在右侧，在 **"说明"** 中，你将看到以下警告：
>
> **&#9888;"validDomains"数组不能包含隧道站点...**
>
>在测试选项卡时，可以忽略此警告。

1. 在"**测试和分发"部分**，选择"安装 **"。**

1. 在弹出对话框中，选择"添加"，并显示包含两个选项的选项卡。

1. 从选项卡中的选项中，选择"选择 **灰色"** 或"**选择红色"。** 选项卡根据所选颜色显示。
 
    ![已上载个人选项卡 ASPNETMVC](../../assets/images/tab-images/personaltabaspnetmvcuploaded.png)

## <a name="view-your-personal-tab"></a>查看个人选项卡

1. 在位于应用最左侧的导航Teams，选择省略号 &#x25CF;&#x25CF;&#x25CF;。 将显示个人应用列表。

1. 从列表中选择您的选项卡进行查看。
