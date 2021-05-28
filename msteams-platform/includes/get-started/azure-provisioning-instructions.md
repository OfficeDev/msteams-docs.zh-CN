## <a name="deploy-your-app-to-azure"></a><span data-ttu-id="8aed3-101">将应用部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="8aed3-101">Deploy your app to Azure</span></span>

<span data-ttu-id="8aed3-102">部署包含两个步骤。</span><span class="sxs-lookup"><span data-stu-id="8aed3-102">Deployment consists of two steps.</span></span>  <span data-ttu-id="8aed3-103">首先，创建必要的云 (也称为预配) ，然后将应用的代码复制到已创建的云资源中。</span><span class="sxs-lookup"><span data-stu-id="8aed3-103">First, necessary cloud resources are created (also known as provisioning), then the code that makes up your app is copied into the created cloud resources.</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="8aed3-104">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="8aed3-104">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="8aed3-105">打开Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="8aed3-105">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="8aed3-106">选择Teams Toolkit图标，从边栏Teams图标。</span><span class="sxs-lookup"><span data-stu-id="8aed3-106">Select the Teams Toolkit from the sidebar by selecting the Teams icon.</span></span>
1. <span data-ttu-id="8aed3-107">选择 **"在云中预配"。**</span><span class="sxs-lookup"><span data-stu-id="8aed3-107">Select **Provision in the Cloud**.</span></span>

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="显示设置命令的屏幕截图":::

1. <span data-ttu-id="8aed3-109">如果需要，请选择用于 Azure 资源的订阅。</span><span class="sxs-lookup"><span data-stu-id="8aed3-109">If required, select a subscription to use for the Azure resources.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8aed3-110">始终有一些用于托管应用的 Azure 资源。</span><span class="sxs-lookup"><span data-stu-id="8aed3-110">There are always some Azure resources used for hosting your app.</span></span>

1. <span data-ttu-id="8aed3-111">对话框警告你在 Azure 中运行资源时可能会产生成本。</span><span class="sxs-lookup"><span data-stu-id="8aed3-111">A dialog warns you that costs may be incurred when running resources in Azure.</span></span>  <span data-ttu-id="8aed3-112">按 **"设置"。**</span><span class="sxs-lookup"><span data-stu-id="8aed3-112">Press **Provision**.</span></span>

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provision-warning.png" alt-text="预配对话框的屏幕截图。":::

   <span data-ttu-id="8aed3-114">预配过程将在 Azure 云中创建资源。</span><span class="sxs-lookup"><span data-stu-id="8aed3-114">The provisioning process will create resources in the Azure cloud.</span></span>  <span data-ttu-id="8aed3-115">这将需要一些时间。</span><span class="sxs-lookup"><span data-stu-id="8aed3-115">This will take some time.</span></span>  <span data-ttu-id="8aed3-116">可以通过查看右下角的对话框来监视进度。</span><span class="sxs-lookup"><span data-stu-id="8aed3-116">You can monitor the progress by watching the dialogs in the bottom right corner.</span></span>  <span data-ttu-id="8aed3-117">几分钟后，你将看到以下通知：</span><span class="sxs-lookup"><span data-stu-id="8aed3-117">After a few minutes, you will see the following notice:</span></span>

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provision-complete.png" alt-text="显示预配完成对话框的屏幕截图。":::

1. <span data-ttu-id="8aed3-119">预配完成后，选择"**部署到云"。**</span><span class="sxs-lookup"><span data-stu-id="8aed3-119">Once provisioning is complete, select **Deploy to the Cloud**.</span></span>  <span data-ttu-id="8aed3-120">与预配一样，此过程需要一些时间。</span><span class="sxs-lookup"><span data-stu-id="8aed3-120">As with provisioning, this process takes some time.</span></span>  <span data-ttu-id="8aed3-121">可以通过查看右下角的对话框来监视该过程。</span><span class="sxs-lookup"><span data-stu-id="8aed3-121">You can monitor the process by watching the dialogs in the bottom right corner.</span></span> <span data-ttu-id="8aed3-122">几分钟后，你将看到完成通知。</span><span class="sxs-lookup"><span data-stu-id="8aed3-122">After a few minutes, you will see a completion notice.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="8aed3-123">命令行</span><span class="sxs-lookup"><span data-stu-id="8aed3-123">Command Line</span></span>](#tab/cli)

<span data-ttu-id="8aed3-124">在终端窗口中：</span><span class="sxs-lookup"><span data-stu-id="8aed3-124">In your terminal window:</span></span>

1. <span data-ttu-id="8aed3-125">运行 `teamsfx provision`。</span><span class="sxs-lookup"><span data-stu-id="8aed3-125">Run `teamsfx provision`.</span></span>

   ``` bash
   teamsfx provision
   ```

   <span data-ttu-id="8aed3-126">系统可能会提示你登录到 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="8aed3-126">You may be prompted to log in to your Azure subscription.</span></span>  <span data-ttu-id="8aed3-127">如果需要，系统将提示你选择要用于 Azure 资源的 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="8aed3-127">If required, you will be prompted to select an Azure subscription to use for the Azure resources.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8aed3-128">始终有一些用于托管应用的 Azure 资源。</span><span class="sxs-lookup"><span data-stu-id="8aed3-128">There are always some Azure resources used for hosting your app.</span></span>

1. <span data-ttu-id="8aed3-129">运行 `teamsfx deploy`。</span><span class="sxs-lookup"><span data-stu-id="8aed3-129">Run `teamsfx deploy`.</span></span>

   ``` bash
   teamsfx deploy
   ```

---

> [!NOTE]
> <span data-ttu-id="8aed3-130">**预配和部署之间有什么区别？**</span><span class="sxs-lookup"><span data-stu-id="8aed3-130">**What's the difference between Provision and Deploy?**</span></span>
>
> <span data-ttu-id="8aed3-131">预配 **步骤** 将在 Azure 和 M365 中为应用创建资源， (HTML、CSS、JavaScript 等) 代码复制到资源。</span><span class="sxs-lookup"><span data-stu-id="8aed3-131">The **Provision** step will create resources in Azure and M365 for your app, but no code (HTML, CSS, JavaScript, etc.) is copied to the resources.</span></span>  <span data-ttu-id="8aed3-132">" **部署** "步骤将应用的代码复制到预配步骤中创建的资源。</span><span class="sxs-lookup"><span data-stu-id="8aed3-132">The **Deploy** step will copy the code for your app to the resources you created during the provision step.</span></span>  <span data-ttu-id="8aed3-133">通常无需预配新资源即可多次部署。</span><span class="sxs-lookup"><span data-stu-id="8aed3-133">It is common to deploy multiple times without provisioning new resources.</span></span> <span data-ttu-id="8aed3-134">由于设置步骤可能需要一些时间才能完成，因此该步骤与部署步骤是分开的。</span><span class="sxs-lookup"><span data-stu-id="8aed3-134">Since the provision step can take some time to complete, it is separate from the deployment step.</span></span>

<span data-ttu-id="8aed3-135">设置和部署步骤完成后：</span><span class="sxs-lookup"><span data-stu-id="8aed3-135">Once the provisioning and deployment steps are finished:</span></span>

1. <span data-ttu-id="8aed3-136">从Visual Studio Code中，打开调试面板 (**Ctrl+Shift+D**  /  **⌘⇧-D"** 或"查看>**运行**) </span><span class="sxs-lookup"><span data-stu-id="8aed3-136">From Visual Studio Code, open the debug panel (**Ctrl+Shift+D** / **⌘⇧-D** or **View > Run**)</span></span>
1. <span data-ttu-id="8aed3-137">从 **启动 ()** 选择"启动远程部署边缘部署"。</span><span class="sxs-lookup"><span data-stu-id="8aed3-137">Select **Launch Remote (Edge)** from the launch configuration drop-down.</span></span>
1. <span data-ttu-id="8aed3-138">按"播放"按钮启动你的应用 - 现在从 Azure 远程运行！</span><span class="sxs-lookup"><span data-stu-id="8aed3-138">Press the Play button to launch your app - now running remotely from Azure!</span></span>
