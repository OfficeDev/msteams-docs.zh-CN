### <a name="use-app-studio-to-update-the-app-package"></a>使用 App Studio 更新应用包

> [!TIP]
> **试用开发人员门户**：App Studio 已发展。 使用新的开发人员门户 配置、Teams和管理你的[应用程序](https://dev.teams.microsoft.com/)。

App Studio 是Teams应用商店中安装的应用Teams应用。 它简化了应用程序的创建和注册过程。

完成以下步骤以更新应用包：

1. 若要在Teams App Studio，请选择左侧栏底部的"应用"图标，然后搜索 **App Studio：**

    <img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

1. 选择 **App Studio** 磁贴，然后选择"安装 **"。** 安装了 App Studio：

    <img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

1. 若要为应用创建应用包 **Teams，** 请选择 App Studio **中的清单编辑器** 选项卡：

    <img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>


    该示例附带自己的清单，旨在生成项目时生成应用包。 在 .NET 上，manifest.json 文件可以位于 清单Visual Studio下的 清单中 ```Microsoft.Teams.Samples.HelloWorld.Web``` 。 在Node.js，这是通过键入项目的根目录中的命令行 `gulp` 完成。

     在Visual Studio中，manifest.json 文件位于 中的 **清单** 下 `Microsoft.Teams.Samples.HelloWorld.Web` 。 此步骤如下图所示：  
    
    <img  width="450px" alt="Build the app package on .NET with Visual Studio" src="~/assets/images/get-started/app-package-on-.NET-with-Visual-Studio.png"/>
    
    可以通过在项目的根目录中Node.js命令行，在应用程序上 `gulp` 生成应用包。


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

    生成的应用包的名称 **helloworldapp.zip。** 如果当前使用的工具中的位置不明确，可以搜索此文件。

1. 现在要修改此应用包，请选择 **"在清单编辑器** 中导入现有 **应用"：**

    <img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

1. 为新 **导入的应用** 选择 Hello World 磁贴：

    <img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

    下图显示了 App Studio 中导入的应用包：

    <img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

    在清单编辑器的左侧有一个步骤列表。 右侧有一个属性列表，需要针对每个步骤进行填充。 当你开始使用示例应用时，大部分信息已经完成。 接下来的步骤将使您能够更新 Hello World 应用的属性。

#### <a name="app-details"></a>应用详细信息

在 **详细信息下选择** 应用 **详细信息**。 选择" **生成** "按钮以创建新的应用 ID。

新的应用 ID 类似于 `2322041b-72bf-459d-b107-f4f335bc35bd` 。

在右侧窗格中查看应用详细信息，包括 **开发人员信息和****品牌** 打造详细信息。 如果你要编写要分发的新应用，这些详细信息非常重要。

#### <a name="tabs"></a>选项卡

向应用添加选项卡Teams非常简单。 示例应用已支持多个选项卡，你可以启用它们。

##### <a name="team-tab"></a>"团队"选项卡

你的应用只能有一个"团队"选项卡：

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

本示例中，"团队"选项卡是显示配置页面的地方。 Select the **...** symbol of the **Tab configuration url** and choose **Edit** from the drop-down menu. 将 URL 更改为必须替换为托管应用时所使用的 `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` URL。

##### <a name="personal-tabs"></a>个人选项卡

你的应用可具有最多 16 个选项卡，包括"团队"选项卡。

个人选项卡不同于"团队"选项卡。Hello **选项卡** 已列在具有占位符值 的个人选项卡列表中 `com.contoso.helloworld.hellotab` 。 Select the **...** symbol of the **Tab configuration url** and choose **Edit** from the drop-down menu. 将显示以下对话框：

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

使用你的应用 URL 更新以下框：

- 将" **内容 URL"** 框更改为 `https://yourteamsapp.ngrok.io/hello`
- 将" **网站 URL"** 框更改为 `https://yourteamsapp.ngrok.io/hello`

将 `yourteamsapp.ngrok.io` 替换为托管应用时所使用的 URL。

#### <a name="bots"></a>机器人

将聊天机器人功能添加到你的应用很简单。 Hello **World** 示例应用已包含自动程序作为示例的一部分，但你必须向 Microsoft 注册它：

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

从示例导入的机器人没有关联的应用 ID。 必须创建新的自动程序，以便 App Studio 可以创建新的应用 ID，然后向 Microsoft 注册它。

> [!NOTE]
> App Studio 为自动程序创建的应用 ID 与为应用创建的应用 ID 不同。 应用的每个自动程序都需要自己的应用 ID。

完成以下步骤以设置自动程序：

1. 选择 **"** 自动程序"列表中导入的机器人旁边的"删除"。 现在，没有要展示的机器人。 
1. 选择 **"** 设置" **以显示"设置自动程序** "对话框。

    <img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

1. 添加自动程序名称 **Contoso 自动** 程序，并选中范围 下的所有三 **个复选框**。
1. 选择 **"保存** "退出对话框。 App Studio 向 Microsoft 注册你的自动程序，在机器人列表中显示你的新机器人。 
1. 现在，在记事本中打开一个文本文件，然后将新的自动程序 ID 复制并粘贴到该文件中。
1. 单击 **"生成新密码**"，并记下你记录自动程序应用 ID 的同一文本文件中的密码。
1. 将 **Bot 终结点地址更新** 为 `https://yourteamsapp.ngrok.io/api/messages` ，将 替换为托管应用 `yourteamsapp.ngrok.io` 时所使用的 URL。
1. 现在保存你的文本文件，因为你必须将文件中的信息添加到托管的应用，以允许与机器人进行安全通信。

#### <a name="messaging-extensions"></a>消息扩展

消息扩展允许用户从你的服务请求信息并发布该信息。 信息以卡片的形式张贴到频道对话中。 邮件扩展显示在撰写框的底部。

完成以下步骤以设置邮件扩展：

1. 在 **App** Studio **左侧窗格中的** "功能"下选择"邮件扩展"以配置邮件扩展：

    <img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

    邮件扩展示例在"邮件扩展"窗格中 **列出。**

1. 选择 **"** 删除"删除邮件扩展，选择" **设置"，** 然后按照用于机器人 [的相同步骤操作](#bots)。 将显示 **"消息传递扩展** "对话框。
1. 选择"**使用现有自动程序**"选项卡和 **"从我现有的自动程序之一中选择"。**
1. 从下拉菜单中选择你创建的自动程序。 添加自动 **程序名称，** 然后选择 **保存** 以关闭对话框。
1. 在"**命令"部分** 下，选择"**添加"。** 若要添加基于搜索的命令，请选择"允许用户查询 **服务信息并将其插入邮件"** 选项。
1. 在" **新建"** 命令对话框中，输入以下值：

    在 **"新建"命令下**：

    - **命令 ID：** 输入随机文本
    - **标题**：输入随机标题
    - **说明**：输入随机描述

    在 **"参数"下**：

    - **名称**：输入参数名称
    - **标题**：输入卡片标题
    - **说明**：输入卡片说明

1. 输入信息后，选择" **保存** "关闭对话框。

#### <a name="register-your-app-in-teams"></a>在应用商店中注册Teams

输入应用的详细信息后，完成以下步骤以在应用中注册Teams：

1. 使用 **测试和分发** App Studio 在 Teams 中安装应用。 
1. 使用自动程序的应用 ID 和密码更新托管的应用程序。 对于示例应用，请对机器人和消息传递扩展使用相同的应用 ID 和密码。 
1. 在 App Studio **的左侧**  窗格中 **，选择"** 测试和分发"下的"完成"：

    <img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

1. 若要将应用上传到Teams，请选择"测试和分发"下的"**安装"按钮**：

    <img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>
    
    > [!NOTE]
    > 如果无法旁加载应用，请验证是否已启用 [自定义应用上传](#prepare-your-development-environment)。

1. 选择 **"添加到** 团队 **"部分中的"搜索"** 框，然后选择一个团队以添加示例应用。 你可以设置一个特殊团队进行测试。
1. 选择 **对话框** 底部的"安装"按钮。

    你的应用现已在 Teams。 但是，在用应用 ID 和密码更新托管应用程序环境之前，机器人和消息扩展将不起作用。

    <img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
