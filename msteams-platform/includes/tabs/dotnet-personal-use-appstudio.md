## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="71515-101">Upload选项卡以Teams App Studio</span><span class="sxs-lookup"><span data-stu-id="71515-101">Upload your tab to Teams with App Studio</span></span>

>[!NOTE]
> <span data-ttu-id="71515-102">我们使用 App Studio 编辑你的manifest.js **文件**，将已完成的程序包上传到Teams。</span><span class="sxs-lookup"><span data-stu-id="71515-102">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="71515-103">如果需要，还可以手动 **编辑manifest.js** 打开。</span><span class="sxs-lookup"><span data-stu-id="71515-103">You can also manually edit **manifest.json** if you prefer.</span></span> <span data-ttu-id="71515-104">如果这样做，请务必再次构建解决方案，以创建要 **Tab.zip** 文件。</span><span class="sxs-lookup"><span data-stu-id="71515-104">If you do, be sure to build the solution again to create the **Tab.zip** file to upload.</span></span>

- <span data-ttu-id="71515-105">打开 Microsoft Teams 客户端。</span><span class="sxs-lookup"><span data-stu-id="71515-105">Open the Microsoft Teams client.</span></span> <span data-ttu-id="71515-106">如果使用基于 [Web 的版本，](https://teams.microsoft.com) 可以使用浏览器的开发人员工具检查前端 [代码](~/tabs/how-to/developer-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="71515-106">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="71515-107">打开 App Studio 并选择清单 **编辑器** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="71515-107">Open App studio and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="71515-108">选择清单 **编辑器中的** "导入现有应用"磁贴，开始为选项卡更新应用包。源代码附带其自己的部分完整清单。</span><span class="sxs-lookup"><span data-stu-id="71515-108">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="71515-109">应用包的名称 **tab.zip。**</span><span class="sxs-lookup"><span data-stu-id="71515-109">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="71515-110">应在此处找到它：</span><span class="sxs-lookup"><span data-stu-id="71515-110">It should be found here:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/Tab.zip
    ```

- <span data-ttu-id="71515-111">UploadTab.zipApp  Studio。</span><span class="sxs-lookup"><span data-stu-id="71515-111">Upload **Tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="71515-112">使用清单编辑器更新应用包</span><span class="sxs-lookup"><span data-stu-id="71515-112">Update your app package with Manifest editor</span></span>

<span data-ttu-id="71515-113">将应用包上传到 App Studio 后，你将需要完成它的配置。</span><span class="sxs-lookup"><span data-stu-id="71515-113">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="71515-114">在清单编辑器欢迎页面的右侧面板中选择新导入选项卡的磁贴。</span><span class="sxs-lookup"><span data-stu-id="71515-114">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="71515-115">清单编辑器左侧有一个步骤列表，右侧是一个属性列表，其中每个步骤都需要有值。</span><span class="sxs-lookup"><span data-stu-id="71515-115">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="71515-116">大部分信息已由你的manifest.js *提供* ，但是有一些字段需要更新：</span><span class="sxs-lookup"><span data-stu-id="71515-116">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="71515-117">详细信息：应用详细信息</span><span class="sxs-lookup"><span data-stu-id="71515-117">Details: App details</span></span>

<span data-ttu-id="71515-118">在" **应用详细信息"** 部分中：</span><span class="sxs-lookup"><span data-stu-id="71515-118">In the **App details** section:</span></span>

- <span data-ttu-id="71515-119">在 **"标识\*\*\*\*"下，** 选择"生成"，为应用生成新的应用 ID。</span><span class="sxs-lookup"><span data-stu-id="71515-119">Under **Identification** select **Generate** to generate a new App Id for your app.</span></span>

- <span data-ttu-id="71515-120">在 **"开发人员信息** "下 **，** 使用 **ngrok** HTTPS URL 更新网站 URL。</span><span class="sxs-lookup"><span data-stu-id="71515-120">Under **Developer information** update the **Website URL** with your **ngrok** HTTPS URL.</span></span>

- <span data-ttu-id="71515-121">在 **"应用程序 URL"** 下 **，将隐私声明** 更新为 `https://<yourngrokurl>/privacy` 和 **使用条款** 以 `https://<yourngrokurl>/tou`>。</span><span class="sxs-lookup"><span data-stu-id="71515-121">Under **App URLs** update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="71515-122">功能：选项卡</span><span class="sxs-lookup"><span data-stu-id="71515-122">Capabilities: Tabs</span></span>

<span data-ttu-id="71515-123">在" *选项卡"* 部分：</span><span class="sxs-lookup"><span data-stu-id="71515-123">In the *Tabs* section:</span></span>

- <span data-ttu-id="71515-124">在 **"添加个人"选项卡下，选择**"**添加"。**</span><span class="sxs-lookup"><span data-stu-id="71515-124">Under **Add a personal tab** select **Add**.</span></span> <span data-ttu-id="71515-125">系统将会显示一个弹出对话窗口。</span><span class="sxs-lookup"><span data-stu-id="71515-125">You will be presented with a pop-up dialogue window.</span></span>

- <span data-ttu-id="71515-126">填写" **名称"** 字段。</span><span class="sxs-lookup"><span data-stu-id="71515-126">Complete the **Name** field.</span></span>

- <span data-ttu-id="71515-127">完成 **"实体 ID"** 字段。</span><span class="sxs-lookup"><span data-stu-id="71515-127">Complete the **Entity Id** field.</span></span>

- <span data-ttu-id="71515-128">将" **内容 URL"** 字段更新为 `https://<yourngrokurl>/personalTab` 。</span><span class="sxs-lookup"><span data-stu-id="71515-128">Update the **Content URL** field with to `https://<yourngrokurl>/personalTab`.</span></span>

- <span data-ttu-id="71515-129">将" **网站 URL"** 字段留空。</span><span class="sxs-lookup"><span data-stu-id="71515-129">Leave the **Website URL** field blank.</span></span>

- <span data-ttu-id="71515-130">选择“**保存**”。</span><span class="sxs-lookup"><span data-stu-id="71515-130">Select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="71515-131">完成时间：域和权限</span><span class="sxs-lookup"><span data-stu-id="71515-131">Finish: Domains and permissions</span></span>

<span data-ttu-id="71515-132">在 **"域和权限"** 部分，选项卡字段中的"域"应包含不包含 HTTPS 前缀的 ngrok URL- `<yourngrokurl>.ngrok.io/` 。</span><span class="sxs-lookup"><span data-stu-id="71515-132">In the **Domains and permissions** section, the **Domains from your tabs** field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

##### <a name="finish-test-and-distribute"></a><span data-ttu-id="71515-133">完成：测试和分发</span><span class="sxs-lookup"><span data-stu-id="71515-133">Finish: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="71515-134">在 **右侧** "说明"字段中，你将看到以下警告：</span><span class="sxs-lookup"><span data-stu-id="71515-134">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="71515-135">&#9888; "**'validDomains' array cannot contain a tunneling site..."**</span><span class="sxs-lookup"><span data-stu-id="71515-135">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="71515-136">在测试选项卡时，可以忽略此警告。</span><span class="sxs-lookup"><span data-stu-id="71515-136">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="71515-137">在" **测试和分发"部分** ：</span><span class="sxs-lookup"><span data-stu-id="71515-137">In the **Test and distribute** section:</span></span>

- <span data-ttu-id="71515-138">选择“**安装**”。</span><span class="sxs-lookup"><span data-stu-id="71515-138">Select **Install**.</span></span>

- <span data-ttu-id="71515-139">在弹出窗口中，确保"为用户添加"设置为"是"，"添加到团队或 **聊天"设置为**"否 **"。** </span><span class="sxs-lookup"><span data-stu-id="71515-139">In the pop-up window make sure that **Add for you** is set to **Yes** and **Add to a team or chat** is set to **No**.</span></span>

- <span data-ttu-id="71515-140">选择“**安装**”。</span><span class="sxs-lookup"><span data-stu-id="71515-140">Select **Install**.</span></span>

- <span data-ttu-id="71515-141">In the next pop-up window select **Open** and your tab will be displayed.</span><span class="sxs-lookup"><span data-stu-id="71515-141">In the next pop-up window select **Open** and your tab will be displayed.</span></span>

## <a name="view-your-personal-tab"></a><span data-ttu-id="71515-142">查看个人选项卡</span><span class="sxs-lookup"><span data-stu-id="71515-142">View your personal tab</span></span>

- <span data-ttu-id="71515-143">在位于应用最左侧的导航栏中，Teams菜单 `...` 。</span><span class="sxs-lookup"><span data-stu-id="71515-143">In the navigation bar located at the far-left of the Teams App, select the `...` menu.</span></span> <span data-ttu-id="71515-144">你将看到个人应用列表。</span><span class="sxs-lookup"><span data-stu-id="71515-144">You'll be presented with a list of personal apps.</span></span>

- <span data-ttu-id="71515-145">从列表中选择要查看的选项卡。</span><span class="sxs-lookup"><span data-stu-id="71515-145">Select your tab from the list to view.</span></span>
