### <a name="use-app-studio-to-update-the-app-package"></a>使用应用程序 Studio 更新应用程序包

应用程序 Studio 是一个团队应用程序，可以从团队存储中进行安装。 它简化了应用程序的创建和注册。

若要在团队中安装应用程序 Studio，请单击左侧右侧栏底部的 "应用商店" 图标，然后搜索应用程序 Studio。

<img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

找到应用程序 Studio 的磁贴后，单击它，然后在弹出的对话框中选择 " *安装* "。

<img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

安装应用程序 Studio 后，单击 "清单编辑器" 选项卡，开始为你的团队应用创建应用程序包。

<img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

该示例附带自己的预设清单，旨在在生成项目时生成应用程序包。 在 .NET 中，这是在 Visual Studio 中完成的，在节点 JS 上，通过在 `gulp` 项目的根目录中的命令行键入来完成此操作。

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

生成的应用程序包的名称为 *helloworldapp.zip*。 如果您正在使用的工具中的位置不明确，则可以搜索此文件。

在本演练的下一部分，您将通过在清单编辑器中选择 " *导入现有应用程序* " 磁贴来修改此应用程序包。

<img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

导入应用程序包后，应用程序 Studio 应如下所示：

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

单击新导入的应用程序的磁贴（ *Hello World*）。

<img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

清单编辑器的左侧有一个步骤列表，在右侧是需要为每个步骤填充的属性的列表中的步骤。 由于您已开始使用示例应用程序，因此已经填写了大部分信息。接下来的步骤将引导您完成更改仍需更新的部件。

#### <a name="app-details"></a>应用程序详细信息

单击 "*详细信息*" 下的 "*应用详细信息*" 条目。 单击 " *生成* " 按钮以创建新的应用程序 id。

您的新应用程序 id 应类似于： `2322041b-72bf-459d-b107-f4f335bc35bd` 。

查看右侧窗格中的其余应用程序详细信息，并熟悉一些条目，如 *开发人员信息* 和 *品牌打造*。 如果要编写新的分发应用程序，则这些部分非常重要。

#### <a name="capabilities-tabs"></a>功能：选项卡

选项卡是要添加到团队应用程序中的最简单元素。 示例应用程序已经支持多个选项卡，您可以按如下所示启用它们。

##### <a name="team-tab"></a>"团队" 选项卡

您的应用只能有一个 "团队" 选项卡。

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

在此示例中，您的配置页面将转到 "团队" 选项卡。 单击条目末尾的 " *...* " 符号，然后从下拉中选择 " *编辑* "。 将 URL 更改为 `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` 替换为您在托管应用程序时使用的 URL 的 url。

##### <a name="personal-tabs"></a>个人选项卡

您的应用程序最长可以包含16个选项卡，其中包括 "团队" 选项卡。

个人选项卡的表示方式不同于 "团队" 选项卡。您应该会看到 " *Hello" 选项卡* 已列在 "个人选项卡" 列表中。 在它有占位符值的时候 `com.contoso.helloworld.hellotab` 。 单击条目末尾的 " *...* " 符号，然后从下拉中选择 " *编辑* "。 将显示以下对话框。

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

有两个字段需要使用您的应用程序 URL 进行更新。

- 将内容 URL 更改为 `https://yourteamsapp.ngrok.io/hello`
- 将网站 URL 更改为 `https://yourteamsapp.ngrok.io/hello`

在 `yourteamsapp.ngrok.io` 托管应用程序时，应将其替换为您在上面使用的 URL。

#### <a name="bots"></a>机器人

Bot 是向应用程序添加功能的最常见方法。 Hello world 示例已将 bot 作为示例的一部分，但尚未在 Microsoft 中注册它。

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

从示例导入的自动程序不具有与之关联的应用 ID。 您必须创建新的 bot，以便应用程序制作室可以创建新的应用 ID 并将其注册到 Microsoft。 请注意，这是 bot 的应用 ID，这与我们在前面的步骤中为应用创建的应用 ID 不同。 应用程序中的每个 bot 都需要自己的应用程序 ID。

单击 "机器人" 列表中*导入机器人*旁边的 "*删除*" 按钮。

现在没有要显示的 bot。 单击 " *设置*"。 这将显示 " *设置机器人* " 对话框。

<img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

添加 bot 名称 `Contoso bot` ，例如，并选择 " *作用域*" 下的所有三个按钮。

选择 " *创建 bot* " 退出对话框。 应用程序 Studio 将花点时间向 Microsoft 注册你的 bot，然后应在 bot 列表中显示新的 bot。 现在，在记事本中打开文本文件并将新的 bot id 复制并粘贴到该文件中是一个很合适的时机。 稍后将需要此 id。

单击 " *生成新密码*"，并记下与您在中记下你的 BOT 应用 ID 的同一文本文件中的密码。 这是仅显示你的密码的唯一时间，因此请务必立即执行此操作。

将 *Bot 终结点地址* 更新为 `https://yourteamsapp.ngrok.io/api/messages` ，其中 `yourteamsapp.ngrok.io` 应替换为您在托管应用程序时使用的 URL。

现在，最好保存文本文件（如果尚未这样做的话）。 你将在本演练后面的部分将此信息添加到托管应用，这将允许与你的 bot 进行安全通信。

#### <a name="messaging-extensions"></a>消息传递扩展

邮件分机允许用户从服务中请求信息，并以卡片形式从右到频道对话中发布该信息。 邮件扩展将沿着 "撰写" 框的底部显示。

在应用程序 Studio 的左栏中，单击 "*功能*" 下的 "*邮件扩展*" 以开始配置邮件扩展。

<img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

示例邮件扩展在右侧窗格中列出在 " *邮件扩展*" 下方。 再次单击 " *删除* " 以删除此条目，然后单击 " *设置* " 按钮，遵循与 "bot" 相同的步骤。 这将显示 " *邮件扩展* " 对话框。

选择 " *使用现有机器人* " 选项卡，然后 *从我的现有 bot 中选择一个*。 在下拉菜单中，选择您在上一节中创建的 bot。 添加 *Bot 名称* ，然后单击 " *保存* " 以关闭对话框。

在 " *命令* " 部分，单击 " *添加*"。 我们正在添加基于搜索的命令，因此请选择 " *允许用户查询你的服务 ...* " 选项。

在 " *新建命令* " 对话框中，输入以下值。

在 " *新建命令*" 下：

- *命令 ID*  = getRandomText
- *Title*       = 获取一些随机文本以获得趣味
- *Description* = 获取一些随机文本和图像

在 " *参数*" 下：

- *Name*        = cardTitle
- *标题*       = 卡片标题
- *Description* = 要使用的卡片标题

输入完信息后，单击 " *保存* " 以关闭对话框。

#### <a name="register-your-app-in-teams"></a>在团队中注册您的应用程序

现在，您已完成应用程序的详细信息输入，但仍需要执行两个步骤。 首先，您必须使用应用程序 Studio 的 "测试和分发" 部分在团队中安装您的应用程序，其次，您必须使用您的 bot 的应用程序 ID 和密码更新托管应用程序。 请记住，该示例需要对 bot 和邮件扩展使用相同的应用程序 ID 和密码。

单击 *测试，并* 在应用程序 Studio 的左侧列中的 " *完成* " 下分发项目。

<img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

若要将应用程序上载到团队，请单击 "*测试和分发*" 下的 "*安装*" 按钮。

<img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

单击 "*添加到团队*中的搜索" 部分中的 "*搜索*" 框，然后选择要向其添加示例应用程序的团队。 通常情况下，您需要设置一个特殊的团队来进行测试。

单击对话框底部的 " *安装* " 按钮。

这将完成本演练的应用程序 Studio 部分。 现在，您应该会看到在团队中运行的应用程序，但在更新托管应用程序环境以了解应用程序 Id 和密码的内容之前，bot 和邮件扩展将不起作用。

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
