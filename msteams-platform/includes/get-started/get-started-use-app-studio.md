### <a name="use-app-studio-to-update-the-app-package"></a><span data-ttu-id="f3ce5-101">使用 App Studio 更新应用包</span><span class="sxs-lookup"><span data-stu-id="f3ce5-101">Use App Studio to update the app package</span></span>

<span data-ttu-id="f3ce5-102">App Studio 是Teams应用商店中安装的应用Teams应用。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-102">App Studio is a Teams app that you can install from the Teams store.</span></span> <span data-ttu-id="f3ce5-103">它简化了应用程序的创建和注册过程。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-103">It simplifies the creation and registration of an app.</span></span>

<span data-ttu-id="f3ce5-104">完成以下步骤以更新应用包：</span><span class="sxs-lookup"><span data-stu-id="f3ce5-104">Complete the following steps to update the app package:</span></span>

1. <span data-ttu-id="f3ce5-105">若要在Teams App Studio，请选择左侧栏底部的"应用"图标，然后搜索 **App Studio：**</span><span class="sxs-lookup"><span data-stu-id="f3ce5-105">To install App Studio in Teams, select the **Apps** icon at the bottom of the left-hand bar, and search for **App Studio**:</span></span>

    <img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

1. <span data-ttu-id="f3ce5-106">选择 **App Studio** 磁贴，然后选择"安装 **"。**</span><span class="sxs-lookup"><span data-stu-id="f3ce5-106">Select the **App Studio** tile and choose **Install**.</span></span> <span data-ttu-id="f3ce5-107">安装了 App Studio：</span><span class="sxs-lookup"><span data-stu-id="f3ce5-107">The App Studio is installed:</span></span>

    <img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

1. <span data-ttu-id="f3ce5-108">若要为应用创建应用包Teams，请选择 **App Studio\*\*\*\*中的** 清单编辑器选项卡：</span><span class="sxs-lookup"><span data-stu-id="f3ce5-108">To create the app package for your Teams app, select the **Manifest editor** tab in **App Studio**:</span></span>

    <img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

    <span data-ttu-id="f3ce5-109">该示例附带自己的清单，旨在生成项目时生成应用包。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-109">The sample comes with its own manifest and is designed to build an app package when the project is built.</span></span> <span data-ttu-id="f3ce5-110">在 .NET 上，此操作在 Visual Studio 中完成Node.js在项目根目录中的命令行中 `gulp` 键入这一点。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-110">On .NET this is done in Visual Studio and on Node.js this is done by typing `gulp` at the command line in the root directory of the project.</span></span>

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

    <span data-ttu-id="f3ce5-111">生成的应用包的名称 **helloworldapp.zip。**</span><span class="sxs-lookup"><span data-stu-id="f3ce5-111">The name of the generated app package is **helloworldapp.zip**.</span></span> <span data-ttu-id="f3ce5-112">如果当前使用的工具中的位置不明确，可以搜索此文件。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-112">You can search for this file if the location is not clear in the tool you are using.</span></span>

1. <span data-ttu-id="f3ce5-113">现在要修改此应用包，请选择 **"在清单编辑器** 中导入现有 **应用"：**</span><span class="sxs-lookup"><span data-stu-id="f3ce5-113">Now to modify this app package, select **Import an existing app** in the **Manifest editor**:</span></span>

    <img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

1. <span data-ttu-id="f3ce5-114">为新 **导入的应用** 选择 Hello World 磁贴：</span><span class="sxs-lookup"><span data-stu-id="f3ce5-114">Select the **Hello World** tile for your newly imported app:</span></span>

    <img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

<span data-ttu-id="f3ce5-115">下图显示了 App Studio 中导入的应用包：</span><span class="sxs-lookup"><span data-stu-id="f3ce5-115">The following image shows the imported app package in App Studio:</span></span>

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

<span data-ttu-id="f3ce5-116">在清单编辑器的左侧有一个步骤列表。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-116">On the left-hand side of the Manifest editor there is a list of steps.</span></span> <span data-ttu-id="f3ce5-117">右侧有一个属性列表，需要针对每个步骤进行填充。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-117">On the right-hand side there is a list of properties that need to be filled in for each step.</span></span> <span data-ttu-id="f3ce5-118">当你开始使用示例应用时，大部分信息已经完成。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-118">As you started with a sample app, much of the information is already completed.</span></span> <span data-ttu-id="f3ce5-119">接下来的步骤将使您能够更新 Hello World 应用的属性。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-119">The next steps enable you to update the properties of the Hello World app.</span></span>

#### <a name="app-details"></a><span data-ttu-id="f3ce5-120">应用详细信息</span><span class="sxs-lookup"><span data-stu-id="f3ce5-120">App details</span></span>

<span data-ttu-id="f3ce5-121">在 **详细信息下选择** 应用 **详细信息**。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-121">Select **App details** under **Details**.</span></span> <span data-ttu-id="f3ce5-122">选择" **生成** "按钮以创建新的应用 ID。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-122">Select the **Generate** button to create a new App ID.</span></span>

<span data-ttu-id="f3ce5-123">新的应用 ID 类似于 `2322041b-72bf-459d-b107-f4f335bc35bd` 。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-123">Your new App ID is similar to `2322041b-72bf-459d-b107-f4f335bc35bd`.</span></span>

<span data-ttu-id="f3ce5-124">在右侧窗格中查看应用详细信息，包括 **开发人员信息和\*\*\*\*品牌打造** 详细信息。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-124">Go through the app details in the right-hand pane including **Developer information** and **Branding** details.</span></span> <span data-ttu-id="f3ce5-125">如果你要编写要分发的新应用，这些详细信息非常重要。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-125">These details are important if you are writing a new app for distribution.</span></span>

#### <a name="tabs"></a><span data-ttu-id="f3ce5-126">选项卡</span><span class="sxs-lookup"><span data-stu-id="f3ce5-126">Tabs</span></span>

<span data-ttu-id="f3ce5-127">向应用程序添加选项卡Teams非常简单。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-127">It is simple to add tabs to a Teams app.</span></span> <span data-ttu-id="f3ce5-128">示例应用已支持多个选项卡，你可以启用它们。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-128">The sample app already supports several tabs, and you can enable them.</span></span>

##### <a name="team-tab"></a><span data-ttu-id="f3ce5-129">"团队"选项卡</span><span class="sxs-lookup"><span data-stu-id="f3ce5-129">Team tab</span></span>

<span data-ttu-id="f3ce5-130">你的应用只能有一个"团队"选项卡：</span><span class="sxs-lookup"><span data-stu-id="f3ce5-130">Your app can only have one Team tab:</span></span>

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

<span data-ttu-id="f3ce5-131">在此示例中，"团队"选项卡是显示配置页面的地方。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-131">In this sample, the Team tab is where your configuration page is displayed.</span></span> <span data-ttu-id="f3ce5-132">Select the **...** symbol of the **Tab configuration url** and choose **Edit** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="f3ce5-132">Select the **...** symbol of the **Tab configuration url** and choose **Edit** from the drop-down menu.</span></span> <span data-ttu-id="f3ce5-133">将 URL 更改为 ，其中 必须替换为托管应用时所使用的 `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` [URL。](#host-the-sample-app)</span><span class="sxs-lookup"><span data-stu-id="f3ce5-133">Change the URL to `https://yourteamsapp.ngrok.io/configure` where `yourteamsapp.ngrok.io` must be replaced with the URL that you used when [hosting your app](#host-the-sample-app).</span></span>

##### <a name="personal-tabs"></a><span data-ttu-id="f3ce5-134">个人选项卡</span><span class="sxs-lookup"><span data-stu-id="f3ce5-134">Personal tabs</span></span>

<span data-ttu-id="f3ce5-135">你的应用可具有最多 16 个选项卡，包括"团队"选项卡。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-135">Your app can have up to 16 tabs, including the Team tab.</span></span>

<span data-ttu-id="f3ce5-136">个人选项卡不同于"团队"选项卡 **。"Hello"选项卡** 已列在具有占位符值 的个人选项卡列表中 `com.contoso.helloworld.hellotab` 。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-136">Personal tabs are different from the Team tab. **Hello Tab** is already listed in the personal tabs list with a placeholder value `com.contoso.helloworld.hellotab`.</span></span> <span data-ttu-id="f3ce5-137">Select the **...** symbol of the **Tab configuration url** and choose **Edit** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="f3ce5-137">Select the **...** symbol of the **Tab configuration url** and choose **Edit** from the drop-down menu.</span></span> <span data-ttu-id="f3ce5-138">将显示以下对话框：</span><span class="sxs-lookup"><span data-stu-id="f3ce5-138">The following dialog box appears:</span></span>

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

<span data-ttu-id="f3ce5-139">使用你的应用 URL 更新以下框：</span><span class="sxs-lookup"><span data-stu-id="f3ce5-139">Update the following boxes with your app URL:</span></span>

- <span data-ttu-id="f3ce5-140">将" **内容 URL"** 框更改为 `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="f3ce5-140">Change the **Content URL** box to `https://yourteamsapp.ngrok.io/hello`</span></span>
- <span data-ttu-id="f3ce5-141">将" **网站 URL"** 框更改为 `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="f3ce5-141">Change the **Website URL** box to `https://yourteamsapp.ngrok.io/hello`</span></span>

<span data-ttu-id="f3ce5-142">将 `yourteamsapp.ngrok.io` 替换为托管应用时所使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-142">Replace `yourteamsapp.ngrok.io` by the URL that you used when hosting your app.</span></span>

#### <a name="bots"></a><span data-ttu-id="f3ce5-143">机器人</span><span class="sxs-lookup"><span data-stu-id="f3ce5-143">Bots</span></span>

<span data-ttu-id="f3ce5-144">将聊天机器人功能添加到你的应用很简单。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-144">It is easy to add the bots functionality to your app.</span></span> <span data-ttu-id="f3ce5-145">Hello **World** 示例应用已包含自动程序作为示例的一部分，但你必须向 Microsoft 注册它：</span><span class="sxs-lookup"><span data-stu-id="f3ce5-145">The **Hello World** sample app already has a bot as part of the sample, but you must register it with Microsoft:</span></span>

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

<span data-ttu-id="f3ce5-146">从示例导入的机器人没有关联的应用 ID。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-146">The bot that was imported from the sample does not have an associated App ID.</span></span> <span data-ttu-id="f3ce5-147">必须创建新的自动程序，以便 App Studio 可以创建新的应用 ID，然后向 Microsoft 注册它。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-147">You must create a new bot so that App Studio can create a new App ID and register it with Microsoft.</span></span>

> [!NOTE]
> <span data-ttu-id="f3ce5-148">App Studio 为自动程序创建的应用 ID 与为应用创建的应用 ID 不同。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-148">The App ID created by App Studio for the bot is different from the App ID created for the app.</span></span> <span data-ttu-id="f3ce5-149">应用的每个自动程序都需要自己的应用 ID。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-149">Each bot in an app requires its own App ID.</span></span>

<span data-ttu-id="f3ce5-150">完成以下步骤以设置自动程序：</span><span class="sxs-lookup"><span data-stu-id="f3ce5-150">Complete the following steps to setup your bot:</span></span>

1. <span data-ttu-id="f3ce5-151">选择 **"** 自动程序"列表中导入的机器人旁边的"删除"。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-151">Select **Delete** next to the imported bot in the bot list.</span></span> <span data-ttu-id="f3ce5-152">现在，没有要展示的机器人。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-152">Now there are no bots left to show.</span></span> 
1. <span data-ttu-id="f3ce5-153">选择 **"** 设置" **以显示"设置自动程序** "对话框。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-153">Select **Setup** to display the **Set up a bot** dialog box.</span></span>

    <img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

1. <span data-ttu-id="f3ce5-154">添加自动程序名称 **Contoso 自动** 程序，并选中范围 下的所有三 **个复选框**。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-154">Add a bot name **Contoso bot** and select all three check boxes under **Scope**.</span></span>
1. <span data-ttu-id="f3ce5-155">选择 **"保存** "退出对话框。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-155">Choose **Save** to exit the dialog box.</span></span> <span data-ttu-id="f3ce5-156">App Studio 向 Microsoft 注册你的自动程序，在机器人列表中显示你的新机器人。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-156">App Studio registers your bot with Microsoft and displays your new bot in the bot list.</span></span> 
1. <span data-ttu-id="f3ce5-157">现在，在记事本中打开一个文本文件，然后将新的自动程序 ID 复制并粘贴到该文件中。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-157">Now open a text file in notepad and copy and paste your new bot ID into it.</span></span>
1. <span data-ttu-id="f3ce5-158">单击 **"生成新密码**"，并记下你记录自动程序应用 ID 的同一文本文件中的密码。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-158">Click **Generate New Password**, and note the password in the same text file you noted your bot App ID.</span></span>
1. <span data-ttu-id="f3ce5-159">将 **Bot 终结点地址更新** 为 `https://yourteamsapp.ngrok.io/api/messages` ，将 替换为托管应用 `yourteamsapp.ngrok.io` 时所使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-159">Update the **Bot endpoint address** to `https://yourteamsapp.ngrok.io/api/messages`, and replace `yourteamsapp.ngrok.io` with the URL that you used when hosting your app.</span></span>
1. <span data-ttu-id="f3ce5-160">现在保存您的文本文件，因为您必须将文件中的信息添加到托管应用，以允许与自动程序进行安全通信。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-160">Now save your text file as you must add the information from the file to your hosted app to allow secure communication with your bot.</span></span>

#### <a name="messaging-extensions"></a><span data-ttu-id="f3ce5-161">消息扩展</span><span class="sxs-lookup"><span data-stu-id="f3ce5-161">Messaging extensions</span></span>

<span data-ttu-id="f3ce5-162">消息扩展允许用户从你的服务请求信息并发布该信息。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-162">Messaging extensions let users ask for information from your service and post that information.</span></span> <span data-ttu-id="f3ce5-163">信息以卡片的形式张贴到频道对话中。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-163">The information is posted in the form of cards into the channel conversation.</span></span> <span data-ttu-id="f3ce5-164">邮件扩展显示在撰写框的底部。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-164">Messaging extensions appear at the bottom of the compose box.</span></span>

<span data-ttu-id="f3ce5-165">完成以下步骤以设置邮件扩展：</span><span class="sxs-lookup"><span data-stu-id="f3ce5-165">Complete the following steps to setup your messaging extension:</span></span>

1. <span data-ttu-id="f3ce5-166">在 **App** Studio **左侧窗格中的** "功能"下选择"邮件扩展"以配置邮件扩展：</span><span class="sxs-lookup"><span data-stu-id="f3ce5-166">Select **Messaging extensions** under **Capabilities** in the left-hand pane of App Studio to configure the messaging extension:</span></span>

    <img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

    <span data-ttu-id="f3ce5-167">邮件扩展示例在"邮件扩展"窗格中 **列出。**</span><span class="sxs-lookup"><span data-stu-id="f3ce5-167">The sample messaging extension is listed in the **Messaging Extensions** pane.</span></span>

1. <span data-ttu-id="f3ce5-168">选择 **"** 删除"删除邮件扩展，选择" **设置"，** 然后按照用于机器人 [的相同步骤操作](#bots)。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-168">Select **Delete** to remove the messaging extension, select **Set up**, and follow the same steps used for [bots](#bots).</span></span> <span data-ttu-id="f3ce5-169">将显示 **"消息传递扩展** "对话框。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-169">The **Messaging Extension** dialog box is displayed.</span></span>
1. <span data-ttu-id="f3ce5-170">选择"**使用现有自动程序**"选项卡和 **"从我现有的自动程序之一中选择"。**</span><span class="sxs-lookup"><span data-stu-id="f3ce5-170">Select the **Use existing bot** tab and **Select from one of my existing bots**.</span></span>
1. <span data-ttu-id="f3ce5-171">从下拉菜单中选择你创建的自动程序。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-171">Select the bot you created from the drop-down menu.</span></span> <span data-ttu-id="f3ce5-172">添加自动 **程序名称，** 然后选择 **保存** 以关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-172">Add a **Bot name** and select **Save** to close the dialog box.</span></span>
1. <span data-ttu-id="f3ce5-173">在"**命令"部分** 下，选择"**添加"。**</span><span class="sxs-lookup"><span data-stu-id="f3ce5-173">Under the **Command** section, select **Add**.</span></span> <span data-ttu-id="f3ce5-174">若要添加基于搜索的命令，请选择"允许用户查询 **服务信息并将其插入邮件"** 选项。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-174">To add a search-based command, select the **Allow users to query your service for information and insert that into a message** option.</span></span>
1. <span data-ttu-id="f3ce5-175">在" **新建"** 命令对话框中，输入以下值：</span><span class="sxs-lookup"><span data-stu-id="f3ce5-175">In the **New command** dialog box, enter the following values:</span></span>

    <span data-ttu-id="f3ce5-176">在 **"新建"命令下**：</span><span class="sxs-lookup"><span data-stu-id="f3ce5-176">Under **New command**:</span></span>

    - <span data-ttu-id="f3ce5-177">**命令 ID：** 输入随机文本</span><span class="sxs-lookup"><span data-stu-id="f3ce5-177">**Command ID**: Enter random text</span></span>
    - <span data-ttu-id="f3ce5-178">**标题**：输入随机标题</span><span class="sxs-lookup"><span data-stu-id="f3ce5-178">**Title**: Enter random title</span></span>
    - <span data-ttu-id="f3ce5-179">**说明**：输入随机描述</span><span class="sxs-lookup"><span data-stu-id="f3ce5-179">**Description**: Enter random description</span></span>

    <span data-ttu-id="f3ce5-180">在 **"参数"下**：</span><span class="sxs-lookup"><span data-stu-id="f3ce5-180">Under **Parameter**:</span></span>

    - <span data-ttu-id="f3ce5-181">**名称**：输入参数名称</span><span class="sxs-lookup"><span data-stu-id="f3ce5-181">**Name**: Enter the parameter name</span></span>
    - <span data-ttu-id="f3ce5-182">**标题**：输入卡片标题</span><span class="sxs-lookup"><span data-stu-id="f3ce5-182">**Title**: Enter the card title</span></span>
    - <span data-ttu-id="f3ce5-183">**说明**：输入卡片说明</span><span class="sxs-lookup"><span data-stu-id="f3ce5-183">**Description**: Enter card description</span></span>

1. <span data-ttu-id="f3ce5-184">输入信息后，选择" **保存** "关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-184">After you enter the information, select **Save** to close the dialog box.</span></span>

#### <a name="register-your-app-in-teams"></a><span data-ttu-id="f3ce5-185">在应用商店中Teams</span><span class="sxs-lookup"><span data-stu-id="f3ce5-185">Register your app in Teams</span></span>

<span data-ttu-id="f3ce5-186">输入应用的详细信息后，完成以下步骤以在应用中注册Teams：</span><span class="sxs-lookup"><span data-stu-id="f3ce5-186">After entering the details of your app, complete the following steps to register your app in Teams:</span></span>

1. <span data-ttu-id="f3ce5-187">使用 **测试和分发** App Studio 在 Teams 中安装应用。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-187">Use **Test and distribute** of App Studio to install your app in Teams.</span></span> 
1. <span data-ttu-id="f3ce5-188">使用自动程序的应用 ID 和密码更新托管的应用程序。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-188">Update your hosted application with the App ID and password for your bot.</span></span> <span data-ttu-id="f3ce5-189">对于示例应用，请对机器人和消息扩展使用相同的应用 ID 和密码。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-189">For the sample app, use the same App ID and password for both bot and messaging extension.</span></span> 
1. <span data-ttu-id="f3ce5-190">在 App Studio **的左侧**  窗格中 **，选择"** 测试和分发"下的"完成"：</span><span class="sxs-lookup"><span data-stu-id="f3ce5-190">Select **Test and distribute**  under **Finish** in the left-hand pane of App Studio:</span></span>

    <img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

1. <span data-ttu-id="f3ce5-191">若要将应用上传到Teams，请选择 **"测试和分发**"下的"**安装"按钮**：</span><span class="sxs-lookup"><span data-stu-id="f3ce5-191">To upload your app to Teams, select the **Install** button under **Test and Distribute**:</span></span>

    <img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

1. <span data-ttu-id="f3ce5-192">选择 **"添加到** 团队 **"部分中的"搜索"** 框，然后选择一个团队以添加示例应用。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-192">Select the **Search** box in the **Add to a team** section and select a team to add the sample app.</span></span> <span data-ttu-id="f3ce5-193">你可以设置一个特殊的团队进行测试。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-193">You can set up a special team for testing.</span></span>
1. <span data-ttu-id="f3ce5-194">选择 **对话框** 底部的"安装"按钮。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-194">Select the **Install** button at the bottom of the dialog box.</span></span>

<span data-ttu-id="f3ce5-195">你的应用现已在 Teams 中提供。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-195">Your app is now available in Teams.</span></span> <span data-ttu-id="f3ce5-196">但是，在用应用 ID 和密码更新托管应用程序环境之前，机器人和消息扩展将不起作用。</span><span class="sxs-lookup"><span data-stu-id="f3ce5-196">However, the bot and the messaging extension will not work until you update the hosted applications environment with the App IDs and passwords.</span></span>

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
