## <a name="upload-your-tab-with-app-studio"></a><span data-ttu-id="500ba-101">Upload App Studio 打开选项卡</span><span class="sxs-lookup"><span data-stu-id="500ba-101">Upload your tab with App Studio</span></span>

>[!NOTE]
> <span data-ttu-id="500ba-102">我们使用 **App Studio** 编辑 **你的manifest.js** 文件，将已完成的程序包上传到Teams。</span><span class="sxs-lookup"><span data-stu-id="500ba-102">We use **App Studio** to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="500ba-103">还可以在 上手动 **manifest.js文件**。</span><span class="sxs-lookup"><span data-stu-id="500ba-103">You can also manually edit **manifest.json**.</span></span> <span data-ttu-id="500ba-104">如果这样做，请确保再次生成解决方案以创建要 **Tab.zip文件。**</span><span class="sxs-lookup"><span data-stu-id="500ba-104">If you do, ensure that you build the solution again to create the **Tab.zip** file to upload.</span></span>

<span data-ttu-id="500ba-105">**使用 App Studio 上传选项卡**</span><span class="sxs-lookup"><span data-stu-id="500ba-105">**To upload your tab with App Studio**</span></span>

1. <span data-ttu-id="500ba-106">转到Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="500ba-106">Go to Microsoft Teams.</span></span> <span data-ttu-id="500ba-107">如果使用基于 [Web 的版本，](https://teams.microsoft.com) 可以使用浏览器的开发人员工具检查前端 [代码](~/tabs/how-to/developer-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="500ba-107">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

1. <span data-ttu-id="500ba-108">转到 **App Studio，** 然后选择清单 **编辑器** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="500ba-108">Go to **App Studio** and select the **Manifest editor** tab.</span></span>

1. <span data-ttu-id="500ba-109">选择 **"在清单编辑器** 中导入现有 **应用"** 开始为选项卡更新应用包。源代码附带其自己的部分完整清单。</span><span class="sxs-lookup"><span data-stu-id="500ba-109">Select **Import an existing app** in the **Manifest editor** to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="500ba-110">应用包的名称 **tab.zip。**</span><span class="sxs-lookup"><span data-stu-id="500ba-110">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="500ba-111">可从以下路径获得：</span><span class="sxs-lookup"><span data-stu-id="500ba-111">It is available from the following path:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. <span data-ttu-id="500ba-112">Uploadtab.zipApp  **Studio。**</span><span class="sxs-lookup"><span data-stu-id="500ba-112">Upload **tab.zip** to **App Studio**.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="500ba-113">使用清单编辑器更新应用包</span><span class="sxs-lookup"><span data-stu-id="500ba-113">Update your app package with Manifest editor</span></span>

<span data-ttu-id="500ba-114">将应用包上传到 App Studio 后，必须对其进行配置。</span><span class="sxs-lookup"><span data-stu-id="500ba-114">After you have uploaded your app package into App Studio, you must configure it.</span></span>

<span data-ttu-id="500ba-115">在清单编辑器欢迎页面的右侧面板中选择新导入选项卡的磁贴。</span><span class="sxs-lookup"><span data-stu-id="500ba-115">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="500ba-116">清单编辑器左侧有一个步骤列表，右侧是一个属性列表，其中每个步骤都必须具有值。</span><span class="sxs-lookup"><span data-stu-id="500ba-116">There is a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that must have values for each of those steps.</span></span> <span data-ttu-id="500ba-117">大部分信息已由你的用户 **manifest.js，但** 有些字段必须更新。</span><span class="sxs-lookup"><span data-stu-id="500ba-117">Much of the information has been provided by your **manifest.json** but there are fields that you must update.</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="500ba-118">详细信息：应用详细信息</span><span class="sxs-lookup"><span data-stu-id="500ba-118">Details: App details</span></span>

<span data-ttu-id="500ba-119">在" **应用详细信息"** 部分中：</span><span class="sxs-lookup"><span data-stu-id="500ba-119">In the **App details** section:</span></span>

1. <span data-ttu-id="500ba-120">在 **"标识**" **下，** 选择"生成"为应用生成新的应用 ID。</span><span class="sxs-lookup"><span data-stu-id="500ba-120">Under **Identification**, select **Generate** to generate a new App Id for your app.</span></span>

1. <span data-ttu-id="500ba-121">在 **"开发人员信息**"下，使用 **ngrok** HTTPS URL 更新网站。</span><span class="sxs-lookup"><span data-stu-id="500ba-121">Under **Developer information**, update the **Website** with your **ngrok** HTTPS URL.</span></span>

1. <span data-ttu-id="500ba-122">在 **"应用程序 URL"** 下，将隐私声明更新为 和 `https://<yourngrokurl>/privacy` **使用条款** 以 `https://<yourngrokurl>/tou`>。</span><span class="sxs-lookup"><span data-stu-id="500ba-122">Under **App URLs**, update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="500ba-123">功能：选项卡</span><span class="sxs-lookup"><span data-stu-id="500ba-123">Capabilities: Tabs</span></span>

<span data-ttu-id="500ba-124">在" **选项卡"** 部分：</span><span class="sxs-lookup"><span data-stu-id="500ba-124">In the **Tabs** section:</span></span>

1. <span data-ttu-id="500ba-125">在 **"添加个人"选项卡下**，选择"**添加"。**</span><span class="sxs-lookup"><span data-stu-id="500ba-125">Under **Add a personal tab**, select **Add**.</span></span> <span data-ttu-id="500ba-126">将出现一个弹出对话框。</span><span class="sxs-lookup"><span data-stu-id="500ba-126">A pop-up dialog box appears.</span></span>

1. <span data-ttu-id="500ba-127">在名称 中输入个人选项卡 **的名称**。</span><span class="sxs-lookup"><span data-stu-id="500ba-127">Enter a name for the personal tab in **Name**.</span></span>

1. <span data-ttu-id="500ba-128">输入实体 **ID**。</span><span class="sxs-lookup"><span data-stu-id="500ba-128">Enter the **Entity ID**.</span></span>

1. <span data-ttu-id="500ba-129">使用 **更新内容** `https://<yourngrokurl>/personalTab` URL。</span><span class="sxs-lookup"><span data-stu-id="500ba-129">Update **Content URL** with `https://<yourngrokurl>/personalTab`.</span></span>

    <span data-ttu-id="500ba-130">将" **网站 URL"** 字段留空。</span><span class="sxs-lookup"><span data-stu-id="500ba-130">Leave the **Website URL** field blank.</span></span>

1. <span data-ttu-id="500ba-131">选择“**保存**”。</span><span class="sxs-lookup"><span data-stu-id="500ba-131">Select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="500ba-132">完成时间：域和权限</span><span class="sxs-lookup"><span data-stu-id="500ba-132">Finish: Domains and permissions</span></span>

<span data-ttu-id="500ba-133">在"**域和权限"** 部分，选项卡字段中的"域"必须包含不带 HTTPS 前缀的 ngrok `<yourngrokurl>.ngrok.io/` URL。</span><span class="sxs-lookup"><span data-stu-id="500ba-133">In the **Domains and permissions** section, the **Domains from your tabs** field must contain your ngrok URL without the HTTPS prefix `<yourngrokurl>.ngrok.io/`.</span></span>

##### <a name="finish-test-and-distribute"></a><span data-ttu-id="500ba-134">完成：测试和分发</span><span class="sxs-lookup"><span data-stu-id="500ba-134">Finish: Test and distribute</span></span>

>[!IMPORTANT]
> <span data-ttu-id="500ba-135">在右侧，在 **"说明"** 中，你将看到以下警告：</span><span class="sxs-lookup"><span data-stu-id="500ba-135">On the right, in **Description**, you see the following warning:</span></span>
>
> <span data-ttu-id="500ba-136">**&#9888;"validDomains"数组不能包含隧道站点...**</span><span class="sxs-lookup"><span data-stu-id="500ba-136">&#9888; **The 'validDomains' array cannot contain a tunneling site...**</span></span>
>
><span data-ttu-id="500ba-137">在测试选项卡时，可以忽略此警告。</span><span class="sxs-lookup"><span data-stu-id="500ba-137">This warning can be ignored while testing your tab.</span></span>

1. <span data-ttu-id="500ba-138">在"**测试和分发"部分**，选择"安装 **"。**</span><span class="sxs-lookup"><span data-stu-id="500ba-138">In the **Test and Distribute** section, select **Install**.</span></span>

1. <span data-ttu-id="500ba-139">在弹出对话框中，选择"添加"，并显示包含两个选项的选项卡。</span><span class="sxs-lookup"><span data-stu-id="500ba-139">In the pop-up dialog box, select **Add** and your tab is displayed with two options.</span></span>

1. <span data-ttu-id="500ba-140">从选项卡中的选项中，选择"选择 **灰色"** 或"**选择红色"。**</span><span class="sxs-lookup"><span data-stu-id="500ba-140">From the options in the tab, choose either **Select Gray** or **Select Red**.</span></span> <span data-ttu-id="500ba-141">选项卡根据所选颜色显示。</span><span class="sxs-lookup"><span data-stu-id="500ba-141">The tab is displayed according to the color you selected.</span></span>
 
    ![已上载个人选项卡 ASPNETMVC](../../assets/images/tab-images/personaltabaspnetmvcuploaded.png)

## <a name="view-your-personal-tab"></a><span data-ttu-id="500ba-143">查看个人选项卡</span><span class="sxs-lookup"><span data-stu-id="500ba-143">View your personal tab</span></span>

1. <span data-ttu-id="500ba-144">在位于应用最左侧的导航Teams，选择省略号 &#x25CF;&#x25CF;&#x25CF;。</span><span class="sxs-lookup"><span data-stu-id="500ba-144">In the navigation bar located at the far left of the Teams app, select the ellipses &#x25CF;&#x25CF;&#x25CF;.</span></span> <span data-ttu-id="500ba-145">将显示个人应用列表。</span><span class="sxs-lookup"><span data-stu-id="500ba-145">A list of personal apps is shown.</span></span>

1. <span data-ttu-id="500ba-146">从列表中选择您的选项卡进行查看。</span><span class="sxs-lookup"><span data-stu-id="500ba-146">Select your tab from the list to view it.</span></span>
