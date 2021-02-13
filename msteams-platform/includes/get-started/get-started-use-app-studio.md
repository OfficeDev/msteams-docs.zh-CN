### <a name="use-app-studio-to-update-the-app-package"></a><span data-ttu-id="28aab-101">使用 App Studio 更新应用包</span><span class="sxs-lookup"><span data-stu-id="28aab-101">Use App Studio to update the app package</span></span>

<span data-ttu-id="28aab-102">App Studio 是一款可以从 Teams 应用商店安装的 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="28aab-102">App Studio is a Teams app that you can install from the Teams store.</span></span> <span data-ttu-id="28aab-103">它简化了应用程序的创建和注册。</span><span class="sxs-lookup"><span data-stu-id="28aab-103">It simplifies the creation and registration of an app.</span></span>

<span data-ttu-id="28aab-104">若要在 Teams 中安装 App  Studio，请选择左侧栏底部的"应用"图标，然后搜索 **App Studio。**</span><span class="sxs-lookup"><span data-stu-id="28aab-104">To install App Studio in Teams, select the **Apps** icon at the bottom of the left-hand bar, and search for **App Studio**.</span></span>

<img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

<span data-ttu-id="28aab-105">选择 **App Studio** 磁贴，然后选择"**安装"。**</span><span class="sxs-lookup"><span data-stu-id="28aab-105">Select the **App Studio** tile and choose **Install**.</span></span> <span data-ttu-id="28aab-106">安装了 App Studio。</span><span class="sxs-lookup"><span data-stu-id="28aab-106">The App Studio is installed.</span></span>

<img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

<span data-ttu-id="28aab-107">选择 **"清单编辑器** "选项卡，为 Teams 应用创建应用包。</span><span class="sxs-lookup"><span data-stu-id="28aab-107">Select the **Manifest editor** tab to create the app package for your Teams app.</span></span>

<img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

<span data-ttu-id="28aab-108">该示例附带自己的预建清单，旨在生成项目时生成应用包。</span><span class="sxs-lookup"><span data-stu-id="28aab-108">The sample comes with its own pre-made manifest and is designed to build an app package when the project is built.</span></span> <span data-ttu-id="28aab-109">在 .NET 上，此操作在 Visual Studio 中完成，在 Node JS 上，通过键入项目的根目录中的命令行 `gulp` 完成此操作。</span><span class="sxs-lookup"><span data-stu-id="28aab-109">On .NET this is done in Visual Studio, and on Node JS this is done by typing `gulp` at the command line in the root directory of the project.</span></span>

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

<span data-ttu-id="28aab-110">生成的应用包的名称 **helloworldapp.zip。**</span><span class="sxs-lookup"><span data-stu-id="28aab-110">The name of the generated app package is **helloworldapp.zip**.</span></span> <span data-ttu-id="28aab-111">如果正在使用的工具中的位置不明确，可以搜索此文件。</span><span class="sxs-lookup"><span data-stu-id="28aab-111">You can search for this file if the location is not clear in the tool you are using.</span></span>

<span data-ttu-id="28aab-112">现在要修改此应用包，请在清单 **编辑器** 中选择"导入现有应用 **磁贴"。**</span><span class="sxs-lookup"><span data-stu-id="28aab-112">Now to modify this app package, select the **Import an existing app** tile in the **Manifest editor**.</span></span>

<img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

<span data-ttu-id="28aab-113">单击 **新导入的应用** 的 Hello World 磁贴。</span><span class="sxs-lookup"><span data-stu-id="28aab-113">Click the **Hello World** tile for your newly imported app.</span></span>

<img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

<span data-ttu-id="28aab-114">下图显示了 App Studio 中导入的应用包：</span><span class="sxs-lookup"><span data-stu-id="28aab-114">The following image shows the imported app package in App Studio:</span></span>

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

<span data-ttu-id="28aab-115">清单编辑器左侧和右侧有一个步骤列表，每个步骤都需要填充的属性列表。</span><span class="sxs-lookup"><span data-stu-id="28aab-115">There is a list of steps on the left-hand side of the Manifest editor and on the right-hand side, a list of properties that need to be filled in for each of those steps.</span></span> <span data-ttu-id="28aab-116">自你开始使用示例应用后，大部分信息已填写。接下来的步骤将演练如何更改仍然需要更新的部件。</span><span class="sxs-lookup"><span data-stu-id="28aab-116">Since you started with a sample app, much of the information is already filled out. The next steps will walk you through changing the parts that still need to be updated.</span></span>

#### <a name="app-details"></a><span data-ttu-id="28aab-117">应用详细信息</span><span class="sxs-lookup"><span data-stu-id="28aab-117">App details</span></span>

<span data-ttu-id="28aab-118">单击"详细信息 *"下的"应用* 详细信息 *"条目*。</span><span class="sxs-lookup"><span data-stu-id="28aab-118">Click on the *App details* entry under *Details*.</span></span> <span data-ttu-id="28aab-119">单击 *"生成* "按钮以创建新的应用 ID。</span><span class="sxs-lookup"><span data-stu-id="28aab-119">Click the *Generate* button to create a new app id.</span></span>

<span data-ttu-id="28aab-120">你的新应用 ID 应如下所示： `2322041b-72bf-459d-b107-f4f335bc35bd` .</span><span class="sxs-lookup"><span data-stu-id="28aab-120">Your new app id should look something like: `2322041b-72bf-459d-b107-f4f335bc35bd`.</span></span>

<span data-ttu-id="28aab-121">查看右侧窗格中的其余应用详细信息，并熟悉一些条目，如开发人员 *信息和\*\*品牌。*</span><span class="sxs-lookup"><span data-stu-id="28aab-121">Look through the rest of the App details in the right-hand pane, and familiarize yourself with some of the entries such as *Developer information* and *Branding*.</span></span> <span data-ttu-id="28aab-122">如果你要编写要分发的新应用，这些部分非常重要。</span><span class="sxs-lookup"><span data-stu-id="28aab-122">These sections are important if you are writing a new app for distribution.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="28aab-123">功能：选项卡</span><span class="sxs-lookup"><span data-stu-id="28aab-123">Capabilities: Tabs</span></span>

<span data-ttu-id="28aab-124">选项卡是添加到 Teams 应用的最简单元素之一。</span><span class="sxs-lookup"><span data-stu-id="28aab-124">Tabs are among the simplest elements to add to a Teams app.</span></span> <span data-ttu-id="28aab-125">示例应用已经支持多个选项卡，你可以按如下方式启用它们。</span><span class="sxs-lookup"><span data-stu-id="28aab-125">The sample app already supports several tabs, and you can enable them as follows.</span></span>

##### <a name="team-tab"></a><span data-ttu-id="28aab-126">团队选项卡</span><span class="sxs-lookup"><span data-stu-id="28aab-126">Team tab</span></span>

<span data-ttu-id="28aab-127">你的应用只能有一个"团队"选项卡。</span><span class="sxs-lookup"><span data-stu-id="28aab-127">Your app can only have one Team tab.</span></span>

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

<span data-ttu-id="28aab-128">在此示例中，"团队"选项卡是配置页的去向。</span><span class="sxs-lookup"><span data-stu-id="28aab-128">In this sample, the Team tab is where your configuration page goes.</span></span> <span data-ttu-id="28aab-129">单击 *条目末尾* 的 ... 符号， *然后从下拉列表* 中选择"编辑"。</span><span class="sxs-lookup"><span data-stu-id="28aab-129">Click on the *...* symbol at the end of the entry and choose *Edit* from the drop-down.</span></span> <span data-ttu-id="28aab-130">将 URL 更改为应在什么位置替换为你在托管应用时上面 `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` 使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="28aab-130">Change the URL to `https://yourteamsapp.ngrok.io/configure` where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

##### <a name="personal-tabs"></a><span data-ttu-id="28aab-131">个人选项卡</span><span class="sxs-lookup"><span data-stu-id="28aab-131">Personal tabs</span></span>

<span data-ttu-id="28aab-132">你的应用可具有最多 16 个选项卡，包括团队选项卡。</span><span class="sxs-lookup"><span data-stu-id="28aab-132">Your app can have up to 16 tabs, including the team tab.</span></span>

<span data-ttu-id="28aab-133">个人选项卡的表示方式与团队选项卡不同。你应该会看到 *Hello 选项卡* 已列在个人选项卡列表中。</span><span class="sxs-lookup"><span data-stu-id="28aab-133">Personal tabs are represented differently from the team tab. You should see *Hello Tab* already listed in the personal tabs list.</span></span> <span data-ttu-id="28aab-134">目前，它具有占位符值 `com.contoso.helloworld.hellotab` 。</span><span class="sxs-lookup"><span data-stu-id="28aab-134">At the moment it has a placeholder value `com.contoso.helloworld.hellotab`.</span></span> <span data-ttu-id="28aab-135">单击 *条目末尾* 的 ... 符号，然后从 *下拉列表中选择"* 编辑"。</span><span class="sxs-lookup"><span data-stu-id="28aab-135">Click on the *...* symbol at the end of the entry and choose *Edit* from the drop-down.</span></span> <span data-ttu-id="28aab-136">将显示以下对话框。</span><span class="sxs-lookup"><span data-stu-id="28aab-136">The following dialog will appear.</span></span>

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

<span data-ttu-id="28aab-137">有两个字段需要通过应用 URL 进行更新。</span><span class="sxs-lookup"><span data-stu-id="28aab-137">There are two fields that you need to update with your app URL.</span></span>

- <span data-ttu-id="28aab-138">将内容 URL 更改为 `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="28aab-138">Change Content URL to `https://yourteamsapp.ngrok.io/hello`</span></span>
- <span data-ttu-id="28aab-139">将网站 URL 更改为 `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="28aab-139">Change Website URL to `https://yourteamsapp.ngrok.io/hello`</span></span>

<span data-ttu-id="28aab-140">在 `yourteamsapp.ngrok.io` 托管应用时，应在何处替换为以上使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="28aab-140">Where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

#### <a name="bots"></a><span data-ttu-id="28aab-141">机器人</span><span class="sxs-lookup"><span data-stu-id="28aab-141">Bots</span></span>

<span data-ttu-id="28aab-142">自动程序是向应用添加功能的最常见方法。</span><span class="sxs-lookup"><span data-stu-id="28aab-142">Bots are the most common way to add functionality to your app.</span></span> <span data-ttu-id="28aab-143">Hello world 示例已包含自动程序作为示例的一部分，但尚未向 Microsoft 注册。</span><span class="sxs-lookup"><span data-stu-id="28aab-143">The hello world sample already has a bot as part of the sample, but it has not been registered with Microsoft yet.</span></span>

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

<span data-ttu-id="28aab-144">从示例导入的机器人尚未关联应用 ID。</span><span class="sxs-lookup"><span data-stu-id="28aab-144">The bot that was imported from the sample does not have an App ID associated with it yet.</span></span> <span data-ttu-id="28aab-145">你必须创建新的自动程序，以便 App Studio 可以创建新的应用 ID，并注册到 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="28aab-145">You will have to create a new bot so that App Studio can create a new App ID and register it with Microsoft.</span></span> <span data-ttu-id="28aab-146">请注意，这是自动程序的应用 ID，与为应用创建的应用 ID 不同。</span><span class="sxs-lookup"><span data-stu-id="28aab-146">Note that this is the App ID for the bot, which is different from the App ID created for the app.</span></span> <span data-ttu-id="28aab-147">应用的每个机器人都需要自己的应用 ID。</span><span class="sxs-lookup"><span data-stu-id="28aab-147">Each bot in an app requires its own App ID.</span></span>

<span data-ttu-id="28aab-148">单击 *自动* 程序列表中导入的自动 *程序旁边的删除* 按钮。</span><span class="sxs-lookup"><span data-stu-id="28aab-148">Click the *delete* button next to the *Imported bot* in the bot list.</span></span>

<span data-ttu-id="28aab-149">现在，没有要展示的机器人。</span><span class="sxs-lookup"><span data-stu-id="28aab-149">Now there are no bots left to show.</span></span> <span data-ttu-id="28aab-150">单击 *"设置"。*</span><span class="sxs-lookup"><span data-stu-id="28aab-150">Click *Setup*.</span></span> <span data-ttu-id="28aab-151">这将显示" *设置自动程序"* 对话框。</span><span class="sxs-lookup"><span data-stu-id="28aab-151">This will display the *Set up a bot* dialog.</span></span>

<img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

<span data-ttu-id="28aab-152">添加自动程序名称，如 `Contoso bot` ，并选择范围下的所有三个 **按钮**。</span><span class="sxs-lookup"><span data-stu-id="28aab-152">Add a bot name such as `Contoso bot`, and select all three buttons under **Scope**.</span></span>

<span data-ttu-id="28aab-153">选择 *"创建自动* 程序"退出对话框。</span><span class="sxs-lookup"><span data-stu-id="28aab-153">Choose *Create bot* to exit the dialog.</span></span> <span data-ttu-id="28aab-154">App Studio 向 Microsoft 注册自动程序，在自动程序列表中显示新机器人。</span><span class="sxs-lookup"><span data-stu-id="28aab-154">App Studio registers your bot with Microsoft and displays your new bot in the bot list.</span></span> <span data-ttu-id="28aab-155">现在应该可以在记事本中打开文本文件，然后将新的自动程序 ID 复制并粘贴到该文件中。</span><span class="sxs-lookup"><span data-stu-id="28aab-155">Now would be a good time to open a text file in notepad and copy and paste your new bot id into it.</span></span> <span data-ttu-id="28aab-156">稍后将需要此 ID。</span><span class="sxs-lookup"><span data-stu-id="28aab-156">You will need this id later.</span></span>

<span data-ttu-id="28aab-157">单击 *"生成新* 密码"，并记下你记录自动程序应用 ID 的同一文本文件中的密码。</span><span class="sxs-lookup"><span data-stu-id="28aab-157">Click *Generate New Password*, and make a note of the password in the same text file you noted your Bot app ID in.</span></span> <span data-ttu-id="28aab-158">这是显示密码的唯一时间，因此请确保现在这样做。</span><span class="sxs-lookup"><span data-stu-id="28aab-158">This is the only time your password will be shown, so be sure to do this now.</span></span>

<span data-ttu-id="28aab-159">将 *Bot 终结点地址更新* 到 ，其中应替换为你在托管应用时上面 `https://yourteamsapp.ngrok.io/api/messages` 使用的 `yourteamsapp.ngrok.io` URL。</span><span class="sxs-lookup"><span data-stu-id="28aab-159">Update the *Bot endpoint address* to `https://yourteamsapp.ngrok.io/api/messages`, where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

<span data-ttu-id="28aab-160">如果尚未保存文本文件，那么现在是保存文本文件的一个好时间。</span><span class="sxs-lookup"><span data-stu-id="28aab-160">Now would be a good time to save your text file if you have not done so already.</span></span> <span data-ttu-id="28aab-161">稍后将在本演练中将此信息添加到托管应用，这将允许与机器人进行安全通信。</span><span class="sxs-lookup"><span data-stu-id="28aab-161">You will add this information to your hosted app later in this walkthrough, which will allow secure communication with your bot.</span></span>

#### <a name="messaging-extensions"></a><span data-ttu-id="28aab-162">消息扩展</span><span class="sxs-lookup"><span data-stu-id="28aab-162">Messaging extensions</span></span>

<span data-ttu-id="28aab-163">消息扩展允许用户从你的服务请求信息，并以卡片形式将该信息张贴到频道对话中。</span><span class="sxs-lookup"><span data-stu-id="28aab-163">Messaging extensions let users ask for information from your service and post that information, in the form of cards, right into the channel conversation.</span></span> <span data-ttu-id="28aab-164">邮件扩展沿撰写框底部显示。</span><span class="sxs-lookup"><span data-stu-id="28aab-164">Messaging extensions appear along the bottom of the compose box.</span></span>

<span data-ttu-id="28aab-165">在 **App** Studio左侧列中的功能下选择邮件扩展以配置邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="28aab-165">Select **Messaging extensions** under **Capabilities** in the left-hand column of App Studio to configure the messaging extension.</span></span>

<img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

<span data-ttu-id="28aab-166">示例邮件扩展列在"邮件扩展"下的右侧 **窗格中**。</span><span class="sxs-lookup"><span data-stu-id="28aab-166">The sample messaging extension is listed in the right-hand pane under **Messaging Extensions**.</span></span> <span data-ttu-id="28aab-167">再次 **选择**"删除"可删除此项，然后单击按照自动程序所遵循的相同步骤操作，单击"设置"按钮。</span><span class="sxs-lookup"><span data-stu-id="28aab-167">Select **Delete** again to remove this entry, and then click the *Set up* button following the same steps as you followed for bots.</span></span> <span data-ttu-id="28aab-168">这将显示 *"消息扩展"* 对话框。</span><span class="sxs-lookup"><span data-stu-id="28aab-168">This will display the *Messaging Extension* dialog.</span></span>

<span data-ttu-id="28aab-169">选择" *使用现有自动程序* "选项卡，然后 *从我现有的自动程序之一中选择*。</span><span class="sxs-lookup"><span data-stu-id="28aab-169">Select the *Use existing bot* tab, then *Select from one of my existing bots*.</span></span> <span data-ttu-id="28aab-170">在下拉菜单中，选择在以上部分中创建的自动程序。</span><span class="sxs-lookup"><span data-stu-id="28aab-170">In the drop-down menu, select the bot you created in the section above.</span></span> <span data-ttu-id="28aab-171">添加自动 *程序名称，* 然后单击 *"保存* "关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="28aab-171">Add a *Bot name* and click *Save* to close the dialog.</span></span>

<span data-ttu-id="28aab-172">在"*命令"* 部分下，单击"*添加"。*</span><span class="sxs-lookup"><span data-stu-id="28aab-172">Under the *Command* section, click *Add*.</span></span> <span data-ttu-id="28aab-173">我们添加一个基于搜索的命令，因此选择"允许用户 *查询你的服务..."* 选项。</span><span class="sxs-lookup"><span data-stu-id="28aab-173">We're adding a search-based command, so choose the *Allow users to query your service...* option.</span></span>

<span data-ttu-id="28aab-174">在 **"新建"命令** 对话框中，输入以下值。</span><span class="sxs-lookup"><span data-stu-id="28aab-174">In the **New command** dialog, enter the following values.</span></span>

<span data-ttu-id="28aab-175">在 *"新建"命令下*：</span><span class="sxs-lookup"><span data-stu-id="28aab-175">Under *New command*:</span></span>

- <span data-ttu-id="28aab-176">*Command ID*  = getRandomText</span><span class="sxs-lookup"><span data-stu-id="28aab-176">*Command ID*  = getRandomText</span></span>
- <span data-ttu-id="28aab-177">*Title*       = 获取一些随机文本作为娱乐</span><span class="sxs-lookup"><span data-stu-id="28aab-177">*Title*       = Get some random text for fun</span></span>
- <span data-ttu-id="28aab-178">*Description* = 获取一些随机文本和图像</span><span class="sxs-lookup"><span data-stu-id="28aab-178">*Description* = Gets some random text and images</span></span>

<span data-ttu-id="28aab-179">在 *参数下*：</span><span class="sxs-lookup"><span data-stu-id="28aab-179">Under *Parameter*:</span></span>

- <span data-ttu-id="28aab-180">*Name*        = cardTitle</span><span class="sxs-lookup"><span data-stu-id="28aab-180">*Name*        = cardTitle</span></span>
- <span data-ttu-id="28aab-181">*Title*       = Card title</span><span class="sxs-lookup"><span data-stu-id="28aab-181">*Title*       = Card title</span></span>
- <span data-ttu-id="28aab-182">*Description* = Card title to use</span><span class="sxs-lookup"><span data-stu-id="28aab-182">*Description* = Card title to use</span></span>

<span data-ttu-id="28aab-183">输入信息后，单击" *保存* "关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="28aab-183">Once you're entered the information, click *Save* to close the dialog.</span></span>

#### <a name="register-your-app-in-teams"></a><span data-ttu-id="28aab-184">在 Teams 中注册应用</span><span class="sxs-lookup"><span data-stu-id="28aab-184">Register your app in Teams</span></span>

<span data-ttu-id="28aab-185">现在，你已完成输入应用的详细信息，但以下两个步骤仍然存在：</span><span class="sxs-lookup"><span data-stu-id="28aab-185">You have now completed entering the details of your app, but the following two steps remain:</span></span>
1. <span data-ttu-id="28aab-186">使用 App Studio 的"测试和分发"部分在 Teams 中安装应用。</span><span class="sxs-lookup"><span data-stu-id="28aab-186">Use the Test and Distribute section of App Studio to install your app in Teams.</span></span>
1. <span data-ttu-id="28aab-187">使用自动程序的应用 ID 和密码更新托管的应用程序。</span><span class="sxs-lookup"><span data-stu-id="28aab-187">Update your hosted application with the App ID and password for your bot.</span></span> <span data-ttu-id="28aab-188">请记住，此示例希望对机器人和消息扩展使用相同的应用 ID 和密码。</span><span class="sxs-lookup"><span data-stu-id="28aab-188">Remember that the sample expects to use the same App ID and password for both the bot and the messaging extension.</span></span>

<span data-ttu-id="28aab-189">选择 **App** Studio 左侧列中的"完成"下的"测试和分发项目"。</span><span class="sxs-lookup"><span data-stu-id="28aab-189">Select the **Test and distribute** item under **Finish** in the left-hand column of App Studio.</span></span>

<img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

<span data-ttu-id="28aab-190">若要将应用上传到 Teams，请单击"测试和分发"*下的"安装"按钮*。</span><span class="sxs-lookup"><span data-stu-id="28aab-190">In order to upload your app to Teams, click the *Install* button under *Test and Distribute*.</span></span>

<img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

<span data-ttu-id="28aab-191">选择 **"** 添加到团队 **"部分中的"搜索** "框，然后选择要添加示例应用程序的团队。</span><span class="sxs-lookup"><span data-stu-id="28aab-191">Select the **Search** box in the **Add to a team** section and select a team to add the sample app to.</span></span> <span data-ttu-id="28aab-192">通常，你可以设置一个特殊团队进行测试。</span><span class="sxs-lookup"><span data-stu-id="28aab-192">Usually, you can set up a special team for testing.</span></span>

<span data-ttu-id="28aab-193">选择 **对话框** 底部的"安装"按钮。</span><span class="sxs-lookup"><span data-stu-id="28aab-193">Select the **Install** button at the bottom of the dialog.</span></span>

<span data-ttu-id="28aab-194">这将完成本演练的 App Studio 部分。</span><span class="sxs-lookup"><span data-stu-id="28aab-194">This finishes the App Studio portion of this walkthrough.</span></span> <span data-ttu-id="28aab-195">现在，你应该会看到你的应用在 Teams 中运行，但是，在更新托管的应用程序环境以知道应用 ID 和密码是什么之前，机器人和消息扩展将不起作用。</span><span class="sxs-lookup"><span data-stu-id="28aab-195">You should now see your app running in Teams, however, the bot and the messaging extension will not work until you update the hosted applications environment to know what the App IDs and passwords are.</span></span>

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
