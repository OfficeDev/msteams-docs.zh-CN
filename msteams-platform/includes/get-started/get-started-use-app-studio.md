### <a name="use-app-studio-to-update-the-app-package"></a><span data-ttu-id="5095e-101">使用应用程序 Studio 更新应用程序包</span><span class="sxs-lookup"><span data-stu-id="5095e-101">Use App Studio to update the app package</span></span>

<span data-ttu-id="5095e-102">应用程序 Studio 是一个团队应用程序，可以从团队存储中进行安装。</span><span class="sxs-lookup"><span data-stu-id="5095e-102">App Studio is a Teams app that you can install from the Teams store.</span></span> <span data-ttu-id="5095e-103">它简化了应用程序的创建和注册。</span><span class="sxs-lookup"><span data-stu-id="5095e-103">It simplifies the creation and registration of an app.</span></span>

<span data-ttu-id="5095e-104">若要在团队中安装应用程序 Studio，请单击左侧右侧栏底部的 "应用商店" 图标，然后搜索应用程序 Studio。</span><span class="sxs-lookup"><span data-stu-id="5095e-104">To install App Studio in Teams, click on the app store icon at the bottom of the left hand bar, and search for App Studio.</span></span>

<img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

<span data-ttu-id="5095e-105">找到应用程序 Studio 的磁贴后，单击它，然后在弹出的对话框中选择 " *安装* "。</span><span class="sxs-lookup"><span data-stu-id="5095e-105">Once you find the tile for App Studio, click on it and choose *install* in the dialog that pops up.</span></span>

<img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

<span data-ttu-id="5095e-106">安装应用程序 Studio 后，单击 "清单编辑器" 选项卡，开始为你的团队应用创建应用程序包。</span><span class="sxs-lookup"><span data-stu-id="5095e-106">Once App Studio is installed click on the Manifest editor tab to begin creating the app package for your Teams app.</span></span>

<img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

<span data-ttu-id="5095e-107">该示例附带自己的预设清单，旨在在生成项目时生成应用程序包。</span><span class="sxs-lookup"><span data-stu-id="5095e-107">The sample comes with its own pre-made manifest, and is designed to build an app package when the project is built.</span></span> <span data-ttu-id="5095e-108">在 .NET 中，这是在 Visual Studio 中完成的，在节点 JS 上，通过在 `gulp` 项目的根目录中的命令行键入来完成此操作。</span><span class="sxs-lookup"><span data-stu-id="5095e-108">On .NET this is done in Visual Studio, and on Node JS this is done by typing `gulp` at the command line in the root directory of the project.</span></span>

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

<span data-ttu-id="5095e-109">生成的应用程序包的名称为 *helloworldapp.zip*。</span><span class="sxs-lookup"><span data-stu-id="5095e-109">The name of the generated app package is *helloworldapp.zip*.</span></span> <span data-ttu-id="5095e-110">如果您正在使用的工具中的位置不明确，则可以搜索此文件。</span><span class="sxs-lookup"><span data-stu-id="5095e-110">You can search for this file if the location is not clear in the tool you are using.</span></span>

<span data-ttu-id="5095e-111">在本演练的下一部分，您将通过在清单编辑器中选择 " *导入现有应用程序* " 磁贴来修改此应用程序包。</span><span class="sxs-lookup"><span data-stu-id="5095e-111">In the next part of this walkthrough you are going to modify this app package by selecting the *Import an existing app* tile in the Manifest Editor.</span></span>

<img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

<span data-ttu-id="5095e-112">导入应用程序包后，应用程序 Studio 应如下所示：</span><span class="sxs-lookup"><span data-stu-id="5095e-112">Once the app package has been imported App Studio should look like this:</span></span>

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

<span data-ttu-id="5095e-113">单击新导入的应用程序的磁贴（ *Hello World*）。</span><span class="sxs-lookup"><span data-stu-id="5095e-113">Click on the tile for your newly imported app, *Hello World*.</span></span>

<img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

<span data-ttu-id="5095e-114">清单编辑器的左侧有一个步骤列表，在右侧是需要为每个步骤填充的属性的列表中的步骤。</span><span class="sxs-lookup"><span data-stu-id="5095e-114">There is a list of steps in the left-hand side of the Manifest editor, and on the right a list of properties that need to be filled in for each of those steps.</span></span> <span data-ttu-id="5095e-115">由于您已开始使用示例应用程序，因此已经填写了大部分信息。接下来的步骤将引导您完成更改仍需更新的部件。</span><span class="sxs-lookup"><span data-stu-id="5095e-115">Since you started with a sample app, much of the information is already filled out. The next steps will walk you through changing the parts that still need to be updated.</span></span>

#### <a name="app-details"></a><span data-ttu-id="5095e-116">应用程序详细信息</span><span class="sxs-lookup"><span data-stu-id="5095e-116">App details</span></span>

<span data-ttu-id="5095e-117">单击 "*详细信息*" 下的 "*应用详细信息*" 条目。</span><span class="sxs-lookup"><span data-stu-id="5095e-117">Click on the *App details* entry under *Details*.</span></span> <span data-ttu-id="5095e-118">单击 " *生成* " 按钮以创建新的应用程序 id。</span><span class="sxs-lookup"><span data-stu-id="5095e-118">Click the *Generate* button to create a new app id.</span></span>

<span data-ttu-id="5095e-119">您的新应用程序 id 应类似于： `2322041b-72bf-459d-b107-f4f335bc35bd` 。</span><span class="sxs-lookup"><span data-stu-id="5095e-119">Your new app id should look something like: `2322041b-72bf-459d-b107-f4f335bc35bd`.</span></span>

<span data-ttu-id="5095e-120">查看右侧窗格中的其余应用程序详细信息，并熟悉一些条目，如 *开发人员信息* 和 *品牌打造*。</span><span class="sxs-lookup"><span data-stu-id="5095e-120">Look through the rest of the App details in the right hand pane, and familiarize yourself with some of the entries such as *Developer information* and *Branding*.</span></span> <span data-ttu-id="5095e-121">如果要编写新的分发应用程序，则这些部分非常重要。</span><span class="sxs-lookup"><span data-stu-id="5095e-121">These sections are important if you are writing a new app for distribution.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="5095e-122">功能：选项卡</span><span class="sxs-lookup"><span data-stu-id="5095e-122">Capabilities: Tabs</span></span>

<span data-ttu-id="5095e-123">选项卡是要添加到团队应用程序中的最简单元素。</span><span class="sxs-lookup"><span data-stu-id="5095e-123">Tabs are among the simplest elements to add to a Teams app.</span></span> <span data-ttu-id="5095e-124">示例应用程序已经支持多个选项卡，您可以按如下所示启用它们。</span><span class="sxs-lookup"><span data-stu-id="5095e-124">The sample app already supports several tabs, and you can enable them as follows.</span></span>

##### <a name="team-tab"></a><span data-ttu-id="5095e-125">"团队" 选项卡</span><span class="sxs-lookup"><span data-stu-id="5095e-125">Team tab</span></span>

<span data-ttu-id="5095e-126">您的应用只能有一个 "团队" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="5095e-126">Your app can only have one Team tab.</span></span>

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

<span data-ttu-id="5095e-127">在此示例中，您的配置页面将转到 "团队" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="5095e-127">In this sample, the Team tab is where your configuration page goes.</span></span> <span data-ttu-id="5095e-128">单击条目末尾的 " *...* " 符号，然后从下拉中选择 " *编辑* "。</span><span class="sxs-lookup"><span data-stu-id="5095e-128">Click on the *...* symbol at the end of the entry and choose *Edit* from the drop-down.</span></span> <span data-ttu-id="5095e-129">将 URL 更改为 `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` 替换为您在托管应用程序时使用的 URL 的 url。</span><span class="sxs-lookup"><span data-stu-id="5095e-129">Change the URL to `https://yourteamsapp.ngrok.io/configure` where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

##### <a name="personal-tabs"></a><span data-ttu-id="5095e-130">个人选项卡</span><span class="sxs-lookup"><span data-stu-id="5095e-130">Personal tabs</span></span>

<span data-ttu-id="5095e-131">您的应用程序最长可以包含16个选项卡，其中包括 "团队" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="5095e-131">Your app can have up to 16 tabs, including the team tab.</span></span>

<span data-ttu-id="5095e-132">个人选项卡的表示方式不同于 "团队" 选项卡。您应该会看到 " *Hello" 选项卡* 已列在 "个人选项卡" 列表中。</span><span class="sxs-lookup"><span data-stu-id="5095e-132">Personal tabs are represented differently from the team tab. You should see *Hello Tab* already listed in the personal tabs list.</span></span> <span data-ttu-id="5095e-133">在它有占位符值的时候 `com.contoso.helloworld.hellotab` 。</span><span class="sxs-lookup"><span data-stu-id="5095e-133">At the moment it has a placeholder value `com.contoso.helloworld.hellotab`.</span></span> <span data-ttu-id="5095e-134">单击条目末尾的 " *...* " 符号，然后从下拉中选择 " *编辑* "。</span><span class="sxs-lookup"><span data-stu-id="5095e-134">Click on the *...* symbol at the end of the entry and choose *Edit* from the drop-down.</span></span> <span data-ttu-id="5095e-135">将显示以下对话框。</span><span class="sxs-lookup"><span data-stu-id="5095e-135">The following dialog will appear.</span></span>

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

<span data-ttu-id="5095e-136">有两个字段需要使用您的应用程序 URL 进行更新。</span><span class="sxs-lookup"><span data-stu-id="5095e-136">There are two fields that you need to update with your app URL.</span></span>

- <span data-ttu-id="5095e-137">将内容 URL 更改为 `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="5095e-137">Change Content URL to `https://yourteamsapp.ngrok.io/hello`</span></span>
- <span data-ttu-id="5095e-138">将网站 URL 更改为 `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="5095e-138">Change Website URL to `https://yourteamsapp.ngrok.io/hello`</span></span>

<span data-ttu-id="5095e-139">在 `yourteamsapp.ngrok.io` 托管应用程序时，应将其替换为您在上面使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="5095e-139">Where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

#### <a name="bots"></a><span data-ttu-id="5095e-140">机器人</span><span class="sxs-lookup"><span data-stu-id="5095e-140">Bots</span></span>

<span data-ttu-id="5095e-141">Bot 是向应用程序添加功能的最常见方法。</span><span class="sxs-lookup"><span data-stu-id="5095e-141">Bots are the most common way to add functionality to your app.</span></span> <span data-ttu-id="5095e-142">Hello world 示例已将 bot 作为示例的一部分，但尚未在 Microsoft 中注册它。</span><span class="sxs-lookup"><span data-stu-id="5095e-142">The hello world sample already has a bot as part of the sample, but it has not been registered with Microsoft yet.</span></span>

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

<span data-ttu-id="5095e-143">从示例导入的自动程序不具有与之关联的应用 ID。</span><span class="sxs-lookup"><span data-stu-id="5095e-143">The bot that was imported from the sample does not have an App ID associated with it yet.</span></span> <span data-ttu-id="5095e-144">您必须创建新的 bot，以便应用程序制作室可以创建新的应用 ID 并将其注册到 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="5095e-144">You will have to create a new bot so that App Studio can create a new App ID and register it with Microsoft.</span></span> <span data-ttu-id="5095e-145">请注意，这是 bot 的应用 ID，这与我们在前面的步骤中为应用创建的应用 ID 不同。</span><span class="sxs-lookup"><span data-stu-id="5095e-145">Note that this is the App ID for the bot, which is different from the App ID that we created for the app in a earlier step.</span></span> <span data-ttu-id="5095e-146">应用程序中的每个 bot 都需要自己的应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="5095e-146">Each bot in an app requires its own App ID.</span></span>

<span data-ttu-id="5095e-147">单击 "机器人" 列表中*导入机器人*旁边的 "*删除*" 按钮。</span><span class="sxs-lookup"><span data-stu-id="5095e-147">Click the *delete* button next to the *Imported bot* in the bot list.</span></span>

<span data-ttu-id="5095e-148">现在没有要显示的 bot。</span><span class="sxs-lookup"><span data-stu-id="5095e-148">Now there are no bots left to show.</span></span> <span data-ttu-id="5095e-149">单击 " *设置*"。</span><span class="sxs-lookup"><span data-stu-id="5095e-149">Click *Setup*.</span></span> <span data-ttu-id="5095e-150">这将显示 " *设置机器人* " 对话框。</span><span class="sxs-lookup"><span data-stu-id="5095e-150">This will display the *Set up a bot* dialog.</span></span>

<img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

<span data-ttu-id="5095e-151">添加 bot 名称 `Contoso bot` ，例如，并选择 " *作用域*" 下的所有三个按钮。</span><span class="sxs-lookup"><span data-stu-id="5095e-151">Add a bot name such as `Contoso bot`, and select all three buttons under *scope*.</span></span>

<span data-ttu-id="5095e-152">选择 " *创建 bot* " 退出对话框。</span><span class="sxs-lookup"><span data-stu-id="5095e-152">Choose *Create bot* to exit the dialog.</span></span> <span data-ttu-id="5095e-153">应用程序 Studio 将花点时间向 Microsoft 注册你的 bot，然后应在 bot 列表中显示新的 bot。</span><span class="sxs-lookup"><span data-stu-id="5095e-153">App Studio will spend a moment registering your bot with Microsoft, and then should display your new bot in the bot list.</span></span> <span data-ttu-id="5095e-154">现在，在记事本中打开文本文件并将新的 bot id 复制并粘贴到该文件中是一个很合适的时机。</span><span class="sxs-lookup"><span data-stu-id="5095e-154">Now would be a good time to open a text file in notepad and copy and paste your new bot id into it.</span></span> <span data-ttu-id="5095e-155">稍后将需要此 id。</span><span class="sxs-lookup"><span data-stu-id="5095e-155">You will need this id later.</span></span>

<span data-ttu-id="5095e-156">单击 " *生成新密码*"，并记下与您在中记下你的 BOT 应用 ID 的同一文本文件中的密码。</span><span class="sxs-lookup"><span data-stu-id="5095e-156">Click *Generate New Password*, and make a note of the password in the same text file you noted your Bot app ID in.</span></span> <span data-ttu-id="5095e-157">这是仅显示你的密码的唯一时间，因此请务必立即执行此操作。</span><span class="sxs-lookup"><span data-stu-id="5095e-157">This is the only time your password will be shown, so be sure to do this now.</span></span>

<span data-ttu-id="5095e-158">将 *Bot 终结点地址* 更新为 `https://yourteamsapp.ngrok.io/api/messages` ，其中 `yourteamsapp.ngrok.io` 应替换为您在托管应用程序时使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="5095e-158">Update the *Bot endpoint address* to `https://yourteamsapp.ngrok.io/api/messages`, where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

<span data-ttu-id="5095e-159">现在，最好保存文本文件（如果尚未这样做的话）。</span><span class="sxs-lookup"><span data-stu-id="5095e-159">Now would be a good time to save your text file if you have not done so already.</span></span> <span data-ttu-id="5095e-160">你将在本演练后面的部分将此信息添加到托管应用，这将允许与你的 bot 进行安全通信。</span><span class="sxs-lookup"><span data-stu-id="5095e-160">You will add this information to your hosted app later in this walkthrough, which will allow secure communication with your bot.</span></span>

#### <a name="messaging-extensions"></a><span data-ttu-id="5095e-161">消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="5095e-161">Messaging extensions</span></span>

<span data-ttu-id="5095e-162">邮件分机允许用户从服务中请求信息，并以卡片形式从右到频道对话中发布该信息。</span><span class="sxs-lookup"><span data-stu-id="5095e-162">Messaging extensions let users ask for information from your service and post that information, in the form of cards, right into the channel conversation.</span></span> <span data-ttu-id="5095e-163">邮件扩展将沿着 "撰写" 框的底部显示。</span><span class="sxs-lookup"><span data-stu-id="5095e-163">Messaging extensions appear along the bottom of the compose box.</span></span>

<span data-ttu-id="5095e-164">在应用程序 Studio 的左栏中，单击 "*功能*" 下的 "*邮件扩展*" 以开始配置邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="5095e-164">Click on *Messaging extensions* under *Capabilities* in the left hand column of App Studio to begin configuring the messaging extension.</span></span>

<img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

<span data-ttu-id="5095e-165">示例邮件扩展在右侧窗格中列出在 " *邮件扩展*" 下方。</span><span class="sxs-lookup"><span data-stu-id="5095e-165">The sample messaging extension is listed in the right hand pane under *Messaging Extensions*.</span></span> <span data-ttu-id="5095e-166">再次单击 " *删除* " 以删除此条目，然后单击 " *设置* " 按钮，遵循与 "bot" 相同的步骤。</span><span class="sxs-lookup"><span data-stu-id="5095e-166">Click *Delete* again to remove this entry, and then click the *Set up* button following the same steps as you followed for bots.</span></span> <span data-ttu-id="5095e-167">这将显示 " *邮件扩展* " 对话框。</span><span class="sxs-lookup"><span data-stu-id="5095e-167">This will display the *Messaging Extension* dialog.</span></span>

<span data-ttu-id="5095e-168">选择 " *使用现有机器人* " 选项卡，然后 *从我的现有 bot 中选择一个*。</span><span class="sxs-lookup"><span data-stu-id="5095e-168">Select the *Use existing bot* tab, then *Select from one of my existing bots*.</span></span> <span data-ttu-id="5095e-169">在下拉菜单中，选择您在上一节中创建的 bot。</span><span class="sxs-lookup"><span data-stu-id="5095e-169">In the drop-down menu, select the bot you created in the section above.</span></span> <span data-ttu-id="5095e-170">添加 *Bot 名称* ，然后单击 " *保存* " 以关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="5095e-170">Add a *Bot name* and click *Save* to close the dialog.</span></span>

<span data-ttu-id="5095e-171">在 " *命令* " 部分，单击 " *添加*"。</span><span class="sxs-lookup"><span data-stu-id="5095e-171">Under the *Command* section, click *Add*.</span></span> <span data-ttu-id="5095e-172">我们正在添加基于搜索的命令，因此请选择 " *允许用户查询你的服务 ...* " 选项。</span><span class="sxs-lookup"><span data-stu-id="5095e-172">We're adding a search-based command, so choose the *Allow users to query your service...* option.</span></span>

<span data-ttu-id="5095e-173">在 " *新建命令* " 对话框中，输入以下值。</span><span class="sxs-lookup"><span data-stu-id="5095e-173">In the *New command* dialog enter the following values.</span></span>

<span data-ttu-id="5095e-174">在 " *新建命令*" 下：</span><span class="sxs-lookup"><span data-stu-id="5095e-174">Under *New command*:</span></span>

- <span data-ttu-id="5095e-175">*命令 ID*  = getRandomText</span><span class="sxs-lookup"><span data-stu-id="5095e-175">*Command ID*  = getRandomText</span></span>
- <span data-ttu-id="5095e-176">*Title*       = 获取一些随机文本以获得趣味</span><span class="sxs-lookup"><span data-stu-id="5095e-176">*Title*       = Get some random text for fun</span></span>
- <span data-ttu-id="5095e-177">*Description* = 获取一些随机文本和图像</span><span class="sxs-lookup"><span data-stu-id="5095e-177">*Description* = Gets some random text and images</span></span>

<span data-ttu-id="5095e-178">在 " *参数*" 下：</span><span class="sxs-lookup"><span data-stu-id="5095e-178">Under *Parameter*:</span></span>

- <span data-ttu-id="5095e-179">*Name*        = cardTitle</span><span class="sxs-lookup"><span data-stu-id="5095e-179">*Name*        = cardTitle</span></span>
- <span data-ttu-id="5095e-180">*标题*       = 卡片标题</span><span class="sxs-lookup"><span data-stu-id="5095e-180">*Title*       = Card title</span></span>
- <span data-ttu-id="5095e-181">*Description* = 要使用的卡片标题</span><span class="sxs-lookup"><span data-stu-id="5095e-181">*Description* = Card title to use</span></span>

<span data-ttu-id="5095e-182">输入完信息后，单击 " *保存* " 以关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="5095e-182">Once you're entered the information, click *Save* to close the dialog.</span></span>

#### <a name="register-your-app-in-teams"></a><span data-ttu-id="5095e-183">在团队中注册您的应用程序</span><span class="sxs-lookup"><span data-stu-id="5095e-183">Register your app in Teams</span></span>

<span data-ttu-id="5095e-184">现在，您已完成应用程序的详细信息输入，但仍需要执行两个步骤。</span><span class="sxs-lookup"><span data-stu-id="5095e-184">You have now completed entering the details of your app, but two steps remain.</span></span> <span data-ttu-id="5095e-185">首先，您必须使用应用程序 Studio 的 "测试和分发" 部分在团队中安装您的应用程序，其次，您必须使用您的 bot 的应用程序 ID 和密码更新托管应用程序。</span><span class="sxs-lookup"><span data-stu-id="5095e-185">First you must use the Test and Distribute section of App Studio to install your app in Teams, and second you must update your hosted application with the App ID and password for your bot.</span></span> <span data-ttu-id="5095e-186">请记住，该示例需要对 bot 和邮件扩展使用相同的应用程序 ID 和密码。</span><span class="sxs-lookup"><span data-stu-id="5095e-186">Remember that the sample expects to use the same App ID and password for both the bot and the messaging extension.</span></span>

<span data-ttu-id="5095e-187">单击 *测试，并* 在应用程序 Studio 的左侧列中的 " *完成* " 下分发项目。</span><span class="sxs-lookup"><span data-stu-id="5095e-187">Click on the *Test and distribute* item under *Finish* in the left hand column of App Studio.</span></span>

<img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

<span data-ttu-id="5095e-188">若要将应用程序上载到团队，请单击 "*测试和分发*" 下的 "*安装*" 按钮。</span><span class="sxs-lookup"><span data-stu-id="5095e-188">In order to upload your app to Teams, click the *Install* button under *Test and Distribute*.</span></span>

<img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

<span data-ttu-id="5095e-189">单击 "*添加到团队*中的搜索" 部分中的 "*搜索*" 框，然后选择要向其添加示例应用程序的团队。</span><span class="sxs-lookup"><span data-stu-id="5095e-189">Click on the *Search* box in the *Add to a team* section and select a team to add the sample app to.</span></span> <span data-ttu-id="5095e-190">通常情况下，您需要设置一个特殊的团队来进行测试。</span><span class="sxs-lookup"><span data-stu-id="5095e-190">Usually you will want to set up a special team for testing.</span></span>

<span data-ttu-id="5095e-191">单击对话框底部的 " *安装* " 按钮。</span><span class="sxs-lookup"><span data-stu-id="5095e-191">Click the *Install* button at the bottom of the dialog.</span></span>

<span data-ttu-id="5095e-192">这将完成本演练的应用程序 Studio 部分。</span><span class="sxs-lookup"><span data-stu-id="5095e-192">This finishes the App Studio portion of this walkthrough.</span></span> <span data-ttu-id="5095e-193">现在，您应该会看到在团队中运行的应用程序，但在更新托管应用程序环境以了解应用程序 Id 和密码的内容之前，bot 和邮件扩展将不起作用。</span><span class="sxs-lookup"><span data-stu-id="5095e-193">You should now see your app running in Teams, however the bot and the messaging extension will not work until you update the hosted applications environment to know what the App IDs and passwords are.</span></span>

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
