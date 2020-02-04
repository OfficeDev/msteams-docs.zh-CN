## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="8b516-101">将您的选项卡上传给具有应用程序 Studio 的团队</span><span class="sxs-lookup"><span data-stu-id="8b516-101">Upload your tab to Teams with App Studio</span></span>

>[!NOTE]
> <span data-ttu-id="8b516-102">我们使用应用程序 Studio 编辑您的**清单 json**文件并将已完成的包上载到团队。</span><span class="sxs-lookup"><span data-stu-id="8b516-102">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="8b516-103">如果愿意，也可以手动编辑**清单 json**文件。</span><span class="sxs-lookup"><span data-stu-id="8b516-103">You can also manually edit the **manifest.json** file if you prefer.</span></span> <span data-ttu-id="8b516-104">如果这样做，请务必再次生成解决方案，以创建要上载的**tab .zip**文件。</span><span class="sxs-lookup"><span data-stu-id="8b516-104">If you do, be sure to build the solution again to create the **tab.zip** file to upload.</span></span>

- <span data-ttu-id="8b516-105">打开 Microsoft 团队客户端。</span><span class="sxs-lookup"><span data-stu-id="8b516-105">Open the Microsoft Teams client.</span></span> <span data-ttu-id="8b516-106">如果您使用的是[基于 web 的版本](https://teams.microsoft.com)，则可以使用浏览器的[开发人员工具](~/tabs/how-to/developer-tools.md)检查您的前端代码。</span><span class="sxs-lookup"><span data-stu-id="8b516-106">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="8b516-107">打开应用程序 Studio 应用，然后选择 "**清单编辑器**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="8b516-107">Open the App Studio app and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="8b516-108">选择 "在清单编辑器中**导入现有的应用程序**磁贴" 以开始更新选项卡的应用程序包。源代码附带其自己完整的清单。</span><span class="sxs-lookup"><span data-stu-id="8b516-108">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="8b516-109">您的应用程序包的名称为 **"tab .zip**"。</span><span class="sxs-lookup"><span data-stu-id="8b516-109">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="8b516-110">应在此处找到：</span><span class="sxs-lookup"><span data-stu-id="8b516-110">It should be found here:</span></span>

```bash
/bin/Debug/netcoreapp2.2/tab.zip
```

- <span data-ttu-id="8b516-111">将**选项卡**上传到应用程序 Studio。</span><span class="sxs-lookup"><span data-stu-id="8b516-111">Upload **tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="8b516-112">使用清单编辑器更新应用程序包</span><span class="sxs-lookup"><span data-stu-id="8b516-112">Update your app package with Manifest editor</span></span>

<span data-ttu-id="8b516-113">将应用程序包上载到应用程序 Studio 后，需要完成对其进行配置。</span><span class="sxs-lookup"><span data-stu-id="8b516-113">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="8b516-114">在清单编辑器的 "欢迎" 页的右面板中，为新导入的选项卡选择磁贴。</span><span class="sxs-lookup"><span data-stu-id="8b516-114">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="8b516-115">清单编辑器的左侧有一个步骤列表，在右侧是需要为每个步骤的值提供值的属性的列表。</span><span class="sxs-lookup"><span data-stu-id="8b516-115">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="8b516-116">大部分信息已由您的*清单 json*提供，但有几个字段需要更新：</span><span class="sxs-lookup"><span data-stu-id="8b516-116">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="8b516-117">详细信息：应用程序详细信息</span><span class="sxs-lookup"><span data-stu-id="8b516-117">Details: App details</span></span>

- <span data-ttu-id="8b516-118">在 "*标识*" 下，选择 "**生成**" 以生成应用程序的新应用 Id。</span><span class="sxs-lookup"><span data-stu-id="8b516-118">Under *Identification* select **Generate** to generate a new App Id for your app.</span></span>

- <span data-ttu-id="8b516-119">在 "*开发人员信息*" 下，使用您的*ngrok* HTTPS URL 更新**网站 URL**字段。</span><span class="sxs-lookup"><span data-stu-id="8b516-119">Under *Developer information* update the **Website URL** field with your *ngrok* HTTPS URL.</span></span>

- <span data-ttu-id="8b516-120">在 *"应用程序 url* " 下， `https://<yourngrokurl>/privacy`更新**隐私声明**，并将`https://<yourngrokurl>/tou` **使用条款**更新为>。</span><span class="sxs-lookup"><span data-stu-id="8b516-120">Under *App URLs* update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="8b516-121">功能：选项卡</span><span class="sxs-lookup"><span data-stu-id="8b516-121">Capabilities: Tabs</span></span>

<span data-ttu-id="8b516-122">在 "*选项卡*" 部分：</span><span class="sxs-lookup"><span data-stu-id="8b516-122">In the *Tabs* section:</span></span>

- <span data-ttu-id="8b516-123">在 "*团队" 选项卡*下选择 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="8b516-123">Under *Team Tab* select **Add**.</span></span>

- <span data-ttu-id="8b516-124">在 "团队" 选项卡弹出窗口中，将*配置 URL*更新为`https://<yourngrokurl>/tab`。</span><span class="sxs-lookup"><span data-stu-id="8b516-124">In the Team tab pop-up window update the *Configuration URL* to `https://<yourngrokurl>/tab`.</span></span>

- <span data-ttu-id="8b516-125">最后，请确保*可以更新配置？* 将选中 "团队" 和 "*组" 聊天*框，然后选择 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="8b516-125">Finally, make sure the *can update configuration? Team*, and *Group chat* boxes are checked and select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="8b516-126">完成：域和权限</span><span class="sxs-lookup"><span data-stu-id="8b516-126">Finish: Domains and permissions</span></span>

<span data-ttu-id="8b516-127">在 "*域和权限*" 部分中，"*选项卡*" 字段中的域应包含不带 HTTPS 前缀`<yourngrokurl>.ngrok.io/`的 ngrok URL。</span><span class="sxs-lookup"><span data-stu-id="8b516-127">In the *Domains and permissions* section, the *Domains from your tabs* field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

#### <a name="finish-test-and-distribute"></a><span data-ttu-id="8b516-128">完成：测试和分发</span><span class="sxs-lookup"><span data-stu-id="8b516-128">Finish: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="8b516-129">在右侧的 "**说明**" 字段中，将看到以下警告：</span><span class="sxs-lookup"><span data-stu-id="8b516-129">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="8b516-130">&#9888; "**validDomains" 数组不能包含隧道站点 ...**"</span><span class="sxs-lookup"><span data-stu-id="8b516-130">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="8b516-131">在测试选项卡时可以忽略此警告。</span><span class="sxs-lookup"><span data-stu-id="8b516-131">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="8b516-132">在 "*测试和分发*" 部分：</span><span class="sxs-lookup"><span data-stu-id="8b516-132">In the *Test and distribute* section:</span></span>

- <span data-ttu-id="8b516-133">选择“**安装**”。</span><span class="sxs-lookup"><span data-stu-id="8b516-133">Select **Install**.</span></span>

- <span data-ttu-id="8b516-134">在弹出窗口的 "*添加到团队" 或 "聊天*" 字段中，输入您的团队并选择 "**安装**"。</span><span class="sxs-lookup"><span data-stu-id="8b516-134">In the pop-up window's *Add to a team or chat* field enter your team and select **Install**.</span></span>

- <span data-ttu-id="8b516-135">在下一个弹出窗口中，选择要在其中显示选项卡的团队频道，然后选择 "**设置**"。</span><span class="sxs-lookup"><span data-stu-id="8b516-135">In the next pop-up window choose the team channel where you would like the tab displayed and select **Set up**.</span></span>

- <span data-ttu-id="8b516-136">在最终弹出窗口中，选择选项卡页的值（红色或灰色图标），然后选择 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="8b516-136">In the final pop-up window select a value for the tab page (either a red or gray icon) and select **Save**.</span></span>

<span data-ttu-id="8b516-137">若要查看您的选项卡，请导航到安装它的团队，然后从选项卡栏中选择它。</span><span class="sxs-lookup"><span data-stu-id="8b516-137">To view your tab, navigate to the team you installed it on, and select it from the tab bar.</span></span> <span data-ttu-id="8b516-138">应显示在配置过程中选择的页面。</span><span class="sxs-lookup"><span data-stu-id="8b516-138">The page that you chose during configuration should be displayed.</span></span>
