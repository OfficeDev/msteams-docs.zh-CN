### <a name="use-app-studio-to-update-the-app-package"></a>使用 App Studio 更新应用包

App Studio 是一款可以从 Teams 应用商店安装的 Teams 应用。 它简化了应用程序的创建和注册。

若要在 Teams 中安装 App  Studio，请选择左侧栏底部的"应用"图标，然后搜索 **App Studio。**

<img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

选择 **App Studio** 磁贴，然后选择"**安装"。** 安装了 App Studio。

<img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

选择 **"清单编辑器** "选项卡，为 Teams 应用创建应用包。

<img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

该示例附带自己的预建清单，旨在生成项目时生成应用包。 在 .NET 上，此操作在 Visual Studio 中完成，在 Node JS 上，通过键入项目的根目录中的命令行 `gulp` 完成此操作。

```bash
$ gulp
[13:39:27] Using gulpfile ~\documents\github\msteams-samples-hello-world-nodejs\gulpfile.js
[13:39:27] Starting 'clean'...
[13:39:27] Starting 'generate-manifest'...
[13:39:27] Finished 'generate-manifest' after 11 ms
[13:39:27] Finished 'clean' after 21 ms
[13:39:27] Starting 'default'...
Build completed. Output in manifest folder
[13:39:27] Finished 'default' after 62 μs
```

生成的应用包的名称 **helloworldapp.zip。** 如果正在使用的工具中的位置不明确，可以搜索此文件。

现在要修改此应用包，请在清单 **编辑器** 中选择"导入现有应用 **磁贴"。**

<img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

单击 **新导入的应用** 的 Hello World 磁贴。

<img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

下图显示了 App Studio 中导入的应用包：

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

清单编辑器左侧和右侧有一个步骤列表，每个步骤都需要填充的属性列表。 自你开始使用示例应用后，大部分信息已填写。接下来的步骤将演练如何更改仍然需要更新的部件。

#### <a name="app-details"></a>应用详细信息

单击"详细信息 *"下的"应用* 详细信息 *"条目*。 单击 *"生成* "按钮以创建新的应用 ID。

你的新应用 ID 应如下所示： `2322041b-72bf-459d-b107-f4f335bc35bd` .

查看右侧窗格中的其余应用详细信息，并熟悉一些条目，如开发人员 *信息和**品牌。* 如果你要编写要分发的新应用，这些部分非常重要。

#### <a name="capabilities-tabs"></a>功能：选项卡

选项卡是添加到 Teams 应用的最简单元素之一。 示例应用已经支持多个选项卡，你可以按如下方式启用它们。

##### <a name="team-tab"></a>团队选项卡

你的应用只能有一个"团队"选项卡。

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

在此示例中，"团队"选项卡是配置页的去向。 单击 *条目末尾* 的 ... 符号， *然后从下拉列表* 中选择"编辑"。 将 URL 更改为应在什么位置替换为你在托管应用时上面 `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` 使用的 URL。

##### <a name="personal-tabs"></a>个人选项卡

你的应用可具有最多 16 个选项卡，包括团队选项卡。

个人选项卡的表示方式与团队选项卡不同。你应该会看到 *Hello 选项卡* 已列在个人选项卡列表中。 目前，它具有占位符值 `com.contoso.helloworld.hellotab` 。 单击 *条目末尾* 的 ... 符号，然后从 *下拉列表中选择"* 编辑"。 将显示以下对话框。

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

有两个字段需要通过应用 URL 进行更新。

- 将内容 URL 更改为 `https://yourteamsapp.ngrok.io/hello`
- 将网站 URL 更改为 `https://yourteamsapp.ngrok.io/hello`

在 `yourteamsapp.ngrok.io` 托管应用时，应在何处替换为以上使用的 URL。

#### <a name="bots"></a>机器人

自动程序是向应用添加功能的最常见方法。 Hello world 示例已包含自动程序作为示例的一部分，但尚未向 Microsoft 注册。

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

从示例导入的机器人尚未关联应用 ID。 你必须创建新的自动程序，以便 App Studio 可以创建新的应用 ID，并注册到 Microsoft。 请注意，这是自动程序的应用 ID，与为应用创建的应用 ID 不同。 应用的每个机器人都需要自己的应用 ID。

单击 *自动* 程序列表中导入的自动 *程序旁边的删除* 按钮。

现在，没有要展示的机器人。 单击 *"设置"。* 这将显示" *设置自动程序"* 对话框。

<img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

添加自动程序名称，如 `Contoso bot` ，并选择范围下的所有三个 **按钮**。

选择 *"创建自动* 程序"退出对话框。 App Studio 向 Microsoft 注册自动程序，在自动程序列表中显示新机器人。 现在应该可以在记事本中打开文本文件，然后将新的自动程序 ID 复制并粘贴到该文件中。 稍后将需要此 ID。

单击 *"生成新* 密码"，并记下你记录自动程序应用 ID 的同一文本文件中的密码。 这是显示密码的唯一时间，因此请确保现在这样做。

将 *Bot 终结点地址更新* 到 ，其中应替换为你在托管应用时上面 `https://yourteamsapp.ngrok.io/api/messages` 使用的 `yourteamsapp.ngrok.io` URL。

如果尚未保存文本文件，那么现在是保存文本文件的一个好时间。 稍后将在本演练中将此信息添加到托管应用，这将允许与机器人进行安全通信。

#### <a name="messaging-extensions"></a>消息扩展

消息扩展允许用户从你的服务请求信息，并以卡片形式将该信息张贴到频道对话中。 邮件扩展沿撰写框底部显示。

在 **App** Studio左侧列中的功能下选择邮件扩展以配置邮件扩展。

<img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

示例邮件扩展列在"邮件扩展"下的右侧 **窗格中**。 再次 **选择**"删除"可删除此项，然后单击按照自动程序所遵循的相同步骤操作，单击"设置"按钮。 这将显示 *"消息扩展"* 对话框。

选择" *使用现有自动程序* "选项卡，然后 *从我现有的自动程序之一中选择*。 在下拉菜单中，选择在以上部分中创建的自动程序。 添加自动 *程序名称，* 然后单击 *"保存* "关闭对话框。

在"*命令"* 部分下，单击"*添加"。* 我们添加一个基于搜索的命令，因此选择"允许用户 *查询你的服务..."* 选项。

在 **"新建"命令** 对话框中，输入以下值。

在 *"新建"命令下*：

- *Command ID*  = getRandomText
- *Title*       = 获取一些随机文本作为娱乐
- *Description* = 获取一些随机文本和图像

在 *参数下*：

- *Name*        = cardTitle
- *Title*       = Card title
- *Description* = Card title to use

输入信息后，单击" *保存* "关闭对话框。

#### <a name="register-your-app-in-teams"></a>在 Teams 中注册应用

现在，你已完成输入应用的详细信息，但以下两个步骤仍然存在：
1. 使用 App Studio 的"测试和分发"部分在 Teams 中安装应用。
1. 使用自动程序的应用 ID 和密码更新托管的应用程序。 请记住，此示例希望对机器人和消息扩展使用相同的应用 ID 和密码。

选择 **App** Studio 左侧列中的"完成"下的"测试和分发项目"。

<img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

若要将应用上传到 Teams，请单击"测试和分发"*下的"安装"按钮*。

<img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

选择 **"** 添加到团队 **"部分中的"搜索** "框，然后选择要添加示例应用程序的团队。 通常，你可以设置一个特殊团队进行测试。

选择 **对话框** 底部的"安装"按钮。

这将完成本演练的 App Studio 部分。 现在，你应该会看到你的应用在 Teams 中运行，但是，在更新托管的应用程序环境以知道应用 ID 和密码是什么之前，机器人和消息扩展将不起作用。

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
