## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="12793-101">将您的选项卡上传给具有应用程序 Studio 的团队</span><span class="sxs-lookup"><span data-stu-id="12793-101">Upload your tab to Teams with App Studio</span></span>

>[!NOTE]
> <span data-ttu-id="12793-102">我们使用应用程序 Studio 编辑您的**清单 json**文件并将已完成的包上载到团队。</span><span class="sxs-lookup"><span data-stu-id="12793-102">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="12793-103">如果愿意，您还可以手动编辑**清单 json** 。</span><span class="sxs-lookup"><span data-stu-id="12793-103">You can also manually edit **manifest.json** if you prefer.</span></span> <span data-ttu-id="12793-104">如果这样做，请务必再次生成解决方案，以创建要上载的**Tab .zip**文件。</span><span class="sxs-lookup"><span data-stu-id="12793-104">If you do, be sure to build the solution again to create the **Tab.zip** file to upload.</span></span>

- <span data-ttu-id="12793-105">打开 Microsoft 团队客户端。</span><span class="sxs-lookup"><span data-stu-id="12793-105">Open the Microsoft Teams client.</span></span> <span data-ttu-id="12793-106">如果您使用的是[基于 web 的版本](https://teams.microsoft.com)，则可以使用浏览器的[开发人员工具](~/tabs/how-to/developer-tools.md)检查您的前端代码。</span><span class="sxs-lookup"><span data-stu-id="12793-106">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="12793-107">打开应用程序 studio 并选择 "**清单编辑器**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="12793-107">Open App studio and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="12793-108">选择 "在清单编辑器中**导入现有的应用程序**磁贴" 以开始更新选项卡的应用程序包。源代码附带其自己完整的清单。</span><span class="sxs-lookup"><span data-stu-id="12793-108">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="12793-109">您的应用程序包的名称为 **"tab .zip**"。</span><span class="sxs-lookup"><span data-stu-id="12793-109">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="12793-110">应在此处找到：</span><span class="sxs-lookup"><span data-stu-id="12793-110">It should be found here:</span></span>

```bash
/bin/Debug/netcoreapp2.2/Tab.zip
```

- <span data-ttu-id="12793-111">将**选项卡**上传到应用程序 Studio。</span><span class="sxs-lookup"><span data-stu-id="12793-111">Upload **Tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="12793-112">使用清单编辑器更新应用程序包</span><span class="sxs-lookup"><span data-stu-id="12793-112">Update your app package with Manifest editor</span></span>

<span data-ttu-id="12793-113">将应用程序包上载到应用程序 Studio 后，需要完成对其进行配置。</span><span class="sxs-lookup"><span data-stu-id="12793-113">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="12793-114">在清单编辑器的 "欢迎" 页的右面板中，为新导入的选项卡选择磁贴。</span><span class="sxs-lookup"><span data-stu-id="12793-114">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="12793-115">清单编辑器的左侧有一个步骤列表，在右侧是需要为每个步骤的值提供值的属性的列表。</span><span class="sxs-lookup"><span data-stu-id="12793-115">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="12793-116">大部分信息已由您的*清单 json*提供，但有几个字段需要更新：</span><span class="sxs-lookup"><span data-stu-id="12793-116">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="12793-117">详细信息：应用程序详细信息</span><span class="sxs-lookup"><span data-stu-id="12793-117">Details: App details</span></span>

<span data-ttu-id="12793-118">在 "*应用程序详细信息*" 部分：</span><span class="sxs-lookup"><span data-stu-id="12793-118">In the *App details* section:</span></span>

- <span data-ttu-id="12793-119">在 "*标识*" 下，选择 "**生成**" 以生成应用程序的新应用 Id。</span><span class="sxs-lookup"><span data-stu-id="12793-119">Under *Identification* select **Generate** to generate a new App Id for your app.</span></span>

- <span data-ttu-id="12793-120">在 "*开发人员信息*" 下，使用您的*ngrok* HTTPS url 更新**网站 URL** 。</span><span class="sxs-lookup"><span data-stu-id="12793-120">Under *Developer information* update the **Website URL** with your *ngrok* HTTPS URL.</span></span>

- <span data-ttu-id="12793-121">在 *"应用程序 url* " 下， `https://<yourngrokurl>/privacy`更新**隐私声明**，并将`https://<yourngrokurl>/tou` **使用条款**更新为>。</span><span class="sxs-lookup"><span data-stu-id="12793-121">Under *App URLs* update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="12793-122">功能：选项卡</span><span class="sxs-lookup"><span data-stu-id="12793-122">Capabilities: Tabs</span></span>

<span data-ttu-id="12793-123">在 "*选项卡*" 部分：</span><span class="sxs-lookup"><span data-stu-id="12793-123">In the *Tabs* section:</span></span>

- <span data-ttu-id="12793-124">在 "*添加个人选项卡*" 下，选择 "***添加***"。</span><span class="sxs-lookup"><span data-stu-id="12793-124">Under *Add a personal tab* select ***Add***.</span></span> <span data-ttu-id="12793-125">将显示一个弹出对话框窗口。</span><span class="sxs-lookup"><span data-stu-id="12793-125">You will be presented with a pop-up dialogue window.</span></span>

- <span data-ttu-id="12793-126">填写 "*名称*" 字段。</span><span class="sxs-lookup"><span data-stu-id="12793-126">Complete the *Name* field.</span></span>

- <span data-ttu-id="12793-127">填写 "*实体 Id* " 字段。</span><span class="sxs-lookup"><span data-stu-id="12793-127">Complete the *Entity Id* field.</span></span>

- <span data-ttu-id="12793-128">使用将*内容 URL*字段更新为`https://<yourngrokurl>/personalTab`。</span><span class="sxs-lookup"><span data-stu-id="12793-128">Update the *Content URL* field with to `https://<yourngrokurl>/personalTab`.</span></span>

- <span data-ttu-id="12793-129">将 "*网站 URL* " 字段保留为空。</span><span class="sxs-lookup"><span data-stu-id="12793-129">Leave the *Website URL* field blank.</span></span>

- <span data-ttu-id="12793-130">选择“***保存***”。</span><span class="sxs-lookup"><span data-stu-id="12793-130">Select ***Save***.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="12793-131">完成：域和权限</span><span class="sxs-lookup"><span data-stu-id="12793-131">Finish: Domains and permissions</span></span>

<span data-ttu-id="12793-132">在 "*域和权限*" 部分中，"*选项卡*" 字段中的域应包含不带 HTTPS 前缀`<yourngrokurl>.ngrok.io/`的 ngrok URL。</span><span class="sxs-lookup"><span data-stu-id="12793-132">In the *Domains and permissions* section, the *Domains from your tabs* field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

##### <a name="finish-test-and-distribute"></a><span data-ttu-id="12793-133">完成：测试和分发</span><span class="sxs-lookup"><span data-stu-id="12793-133">Finish: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="12793-134">在右侧的 "**说明**" 字段中，将看到以下警告：</span><span class="sxs-lookup"><span data-stu-id="12793-134">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="12793-135">&#9888; "**validDomains" 数组不能包含隧道站点 ...**"</span><span class="sxs-lookup"><span data-stu-id="12793-135">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="12793-136">在测试选项卡时可以忽略此警告。</span><span class="sxs-lookup"><span data-stu-id="12793-136">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="12793-137">在 "*测试和分发*" 部分：</span><span class="sxs-lookup"><span data-stu-id="12793-137">In the *Test and distribute* section:</span></span>

- <span data-ttu-id="12793-138">选择“**安装**”。</span><span class="sxs-lookup"><span data-stu-id="12793-138">Select **Install**.</span></span>

- <span data-ttu-id="12793-139">在弹出窗口中，请确保将 "*添加*到" 设置为 *"是"* ，并*将 "添加到团队" 或 "聊天*" 设置为 "*否*"。</span><span class="sxs-lookup"><span data-stu-id="12793-139">In the pop-up window make sure that *Add for you* is set to *Yes* and *Add to a team or chat* is set to *No*.</span></span>

- <span data-ttu-id="12793-140">选择“**安装**”。</span><span class="sxs-lookup"><span data-stu-id="12793-140">Select **Install**.</span></span>

- <span data-ttu-id="12793-141">在下一个弹出窗口中，选择 "**打开**"，您的选项卡将显示出来。</span><span class="sxs-lookup"><span data-stu-id="12793-141">In the next pop-up window select **Open** and your tab will be displayed.</span></span>

## <a name="view-your-personal-tab"></a><span data-ttu-id="12793-142">查看您的个人选项卡</span><span class="sxs-lookup"><span data-stu-id="12793-142">View your personal tab</span></span>

- <span data-ttu-id="12793-143">在位于 "团队" 应用程序最左侧的导航栏中，选择 "" `...`菜单。</span><span class="sxs-lookup"><span data-stu-id="12793-143">In the navigation bar located at the far-left of the Teams App, select the `...` menu.</span></span> <span data-ttu-id="12793-144">将显示个人应用程序的列表。</span><span class="sxs-lookup"><span data-stu-id="12793-144">You'll be presented with a list of personal apps.</span></span>

- <span data-ttu-id="12793-145">从列表中选择要查看的选项卡。</span><span class="sxs-lookup"><span data-stu-id="12793-145">Select your tab from the list to view.</span></span>
