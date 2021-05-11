## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="93ea3-101">Upload选项卡以Teams App Studio</span><span class="sxs-lookup"><span data-stu-id="93ea3-101">Upload your tab to Teams with App Studio</span></span>

>[!NOTE]
> <span data-ttu-id="93ea3-102">我们使用 App Studio 编辑你的manifest.js **文件**，将已完成的程序包上传到Teams。</span><span class="sxs-lookup"><span data-stu-id="93ea3-102">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="93ea3-103">如果需要，还可以手动编辑 **manifest.js** 上的文件。</span><span class="sxs-lookup"><span data-stu-id="93ea3-103">You can also manually edit the **manifest.json** file if you prefer.</span></span> <span data-ttu-id="93ea3-104">如果这样做，请务必再次构建解决方案，以创建要 **tab.zip** 文件。</span><span class="sxs-lookup"><span data-stu-id="93ea3-104">If you do, be sure to build the solution again to create the **tab.zip** file to upload.</span></span>

- <span data-ttu-id="93ea3-105">打开 Microsoft Teams 客户端。</span><span class="sxs-lookup"><span data-stu-id="93ea3-105">Open the Microsoft Teams client.</span></span> <span data-ttu-id="93ea3-106">如果使用基于 [Web 的版本，](https://teams.microsoft.com) 可以使用浏览器的开发人员工具检查前端 [代码](~/tabs/how-to/developer-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="93ea3-106">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="93ea3-107">打开 App Studio 应用，然后选择清单 **编辑器** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="93ea3-107">Open the App Studio app and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="93ea3-108">选择清单 **编辑器中的** "导入现有应用"磁贴，开始为选项卡更新应用包。源代码附带其自己的部分完整清单。</span><span class="sxs-lookup"><span data-stu-id="93ea3-108">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="93ea3-109">应用包的名称 **tab.zip。**</span><span class="sxs-lookup"><span data-stu-id="93ea3-109">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="93ea3-110">应在此处找到它：</span><span class="sxs-lookup"><span data-stu-id="93ea3-110">It should be found here:</span></span>

```bash
/bin/Debug/netcoreapp2.2/tab.zip
```

- <span data-ttu-id="93ea3-111">Uploadtab.zipApp  Studio。</span><span class="sxs-lookup"><span data-stu-id="93ea3-111">Upload **tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="93ea3-112">使用清单编辑器更新应用包</span><span class="sxs-lookup"><span data-stu-id="93ea3-112">Update your app package with Manifest editor</span></span>

<span data-ttu-id="93ea3-113">将应用包上传到 App Studio 后，你将需要完成它的配置。</span><span class="sxs-lookup"><span data-stu-id="93ea3-113">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="93ea3-114">在清单编辑器欢迎页面的右侧面板中选择新导入选项卡的磁贴。</span><span class="sxs-lookup"><span data-stu-id="93ea3-114">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="93ea3-115">清单编辑器左侧有一个步骤列表，右侧是一个属性列表，其中每个步骤都需要有值。</span><span class="sxs-lookup"><span data-stu-id="93ea3-115">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="93ea3-116">大部分信息已由你的manifest.js *提供* ，但是有一些字段需要更新：</span><span class="sxs-lookup"><span data-stu-id="93ea3-116">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="93ea3-117">详细信息：应用详细信息</span><span class="sxs-lookup"><span data-stu-id="93ea3-117">Details: App details</span></span>

- <span data-ttu-id="93ea3-118">在 *"标识\*\*\*"下，*\* 选择"生成"，为应用生成新的应用 ID。</span><span class="sxs-lookup"><span data-stu-id="93ea3-118">Under *Identification* select **Generate** to generate a new App Id for your app.</span></span>

- <span data-ttu-id="93ea3-119">在 *"开发人员信息*"下，使用 *ngrok* HTTPS **URL** 更新"网站 URL"字段。</span><span class="sxs-lookup"><span data-stu-id="93ea3-119">Under *Developer information* update the **Website URL** field with your *ngrok* HTTPS URL.</span></span>

- <span data-ttu-id="93ea3-120">在 *"应用程序 URL"* 下 **，将隐私声明** 更新为 `https://<yourngrokurl>/privacy` 和 **使用条款** 以 `https://<yourngrokurl>/tou`>。</span><span class="sxs-lookup"><span data-stu-id="93ea3-120">Under *App URLs* update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="93ea3-121">功能：选项卡</span><span class="sxs-lookup"><span data-stu-id="93ea3-121">Capabilities: Tabs</span></span>

<span data-ttu-id="93ea3-122">在" *选项卡"* 部分：</span><span class="sxs-lookup"><span data-stu-id="93ea3-122">In the *Tabs* section:</span></span>

- <span data-ttu-id="93ea3-123">在"*团队选项卡"下*，选择"**添加"。**</span><span class="sxs-lookup"><span data-stu-id="93ea3-123">Under *Team Tab* select **Add**.</span></span>

- <span data-ttu-id="93ea3-124">在"团队"选项卡弹出窗口中，将 *"配置 URL"更新* 为 `https://<yourngrokurl>/tab` 。</span><span class="sxs-lookup"><span data-stu-id="93ea3-124">In the Team tab pop-up window update the *Configuration URL* to `https://<yourngrokurl>/tab`.</span></span>

- <span data-ttu-id="93ea3-125">最后，确保 *可以更新配置？选中*"团队"和"*群聊*"框，然后选择"保存 **"。**</span><span class="sxs-lookup"><span data-stu-id="93ea3-125">Finally, make sure the *can update configuration? Team*, and *Group chat* boxes are checked and select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="93ea3-126">完成时间：域和权限</span><span class="sxs-lookup"><span data-stu-id="93ea3-126">Finish: Domains and permissions</span></span>

<span data-ttu-id="93ea3-127">在 *"域和权限"* 部分，选项卡字段中的"域"应包含不包含 HTTPS 前缀的 ngrok URL- `<yourngrokurl>.ngrok.io/` 。</span><span class="sxs-lookup"><span data-stu-id="93ea3-127">In the *Domains and permissions* section, the *Domains from your tabs* field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

#### <a name="finish-test-and-distribute"></a><span data-ttu-id="93ea3-128">完成：测试和分发</span><span class="sxs-lookup"><span data-stu-id="93ea3-128">Finish: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="93ea3-129">在 **右侧** "说明"字段中，你将看到以下警告：</span><span class="sxs-lookup"><span data-stu-id="93ea3-129">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="93ea3-130">&#9888; "**'validDomains' array cannot contain a tunneling site..."**</span><span class="sxs-lookup"><span data-stu-id="93ea3-130">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="93ea3-131">在测试选项卡时，可以忽略此警告。</span><span class="sxs-lookup"><span data-stu-id="93ea3-131">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="93ea3-132">在" *测试和分发"部分* ：</span><span class="sxs-lookup"><span data-stu-id="93ea3-132">In the *Test and distribute* section:</span></span>

- <span data-ttu-id="93ea3-133">选择“**安装**”。</span><span class="sxs-lookup"><span data-stu-id="93ea3-133">Select **Install**.</span></span>

- <span data-ttu-id="93ea3-134">在弹出窗口的"添加到团队或聊天"字段中，输入你的团队，然后选择"安装 **"。**</span><span class="sxs-lookup"><span data-stu-id="93ea3-134">In the pop-up window's *Add to a team or chat* field enter your team and select **Install**.</span></span>

- <span data-ttu-id="93ea3-135">In the next pop-up window choose the team channel where you would like the tab displayed and select **Set up**.</span><span class="sxs-lookup"><span data-stu-id="93ea3-135">In the next pop-up window choose the team channel where you would like the tab displayed and select **Set up**.</span></span>

- <span data-ttu-id="93ea3-136">在最终弹出窗口中，选择选项卡页的值 (红色或灰色图标) 保存 **"。**</span><span class="sxs-lookup"><span data-stu-id="93ea3-136">In the final pop-up window select a value for the tab page (either a red or gray icon) and select **Save**.</span></span>

<span data-ttu-id="93ea3-137">若要查看您的选项卡，请导航到安装它的团队，然后从选项卡栏中选择它。</span><span class="sxs-lookup"><span data-stu-id="93ea3-137">To view your tab, navigate to the team you installed it on, and select it from the tab bar.</span></span> <span data-ttu-id="93ea3-138">应显示在配置期间选择的页面。</span><span class="sxs-lookup"><span data-stu-id="93ea3-138">The page that you chose during configuration should be displayed.</span></span>
