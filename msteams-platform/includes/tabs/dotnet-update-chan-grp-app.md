### <a name="_layoutcshtml"></a><span data-ttu-id="10235-101">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="10235-101">_Layout.cshtml</span></span>

<span data-ttu-id="10235-102">若要在页面中显示选项卡Teams，必须包含 **Microsoft Teams JavaScript** 客户端 SDK，并包括页面加载 `microsoftTeams.initialize()` 后对 的调用。</span><span class="sxs-lookup"><span data-stu-id="10235-102">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="10235-103">这是选项卡和客户端Teams的方式：</span><span class="sxs-lookup"><span data-stu-id="10235-103">This is how your tab and the Teams client communicate:</span></span>

<span data-ttu-id="10235-104">转到" **共享"** 文件夹，打开 **_Layout.cshtml，** 然后向 标记中添加 `<head>` 以下内容：</span><span class="sxs-lookup"><span data-stu-id="10235-104">Go to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tag:</span></span>

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

>[!IMPORTANT]
> <span data-ttu-id="10235-105">不要复制并粘贴此页 `<script src="...">` 中的 URL，因为它们可能并不表示最新版本。</span><span class="sxs-lookup"><span data-stu-id="10235-105">Do not copy and paste the `<script src="...">` URLs from this page, as they may not represent the latest version.</span></span> <span data-ttu-id="10235-106">若要获取最新版本的 SDK，请始终转到[Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js)。</span><span class="sxs-lookup"><span data-stu-id="10235-106">To get the latest version of the SDK, always go to [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js).</span></span>

### <a name="tabcshtml"></a><span data-ttu-id="10235-107">Tab.cshtml</span><span class="sxs-lookup"><span data-stu-id="10235-107">Tab.cshtml</span></span>

<span data-ttu-id="10235-108">**更新嵌入的脚本**</span><span class="sxs-lookup"><span data-stu-id="10235-108">**To update the embedded script**</span></span>

1. <span data-ttu-id="10235-109">在Visual Studio中，打开 **Tab.cshtml** 以更新嵌入的 `<script>` 。</span><span class="sxs-lookup"><span data-stu-id="10235-109">In Visual Studio, open **Tab.cshtml** to update the embedded `<script>`.</span></span>

1. <span data-ttu-id="10235-110">在脚本顶部，调用 `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="10235-110">At the top of the script, call `microsoftTeams.initialize()`.</span></span>

1. <span data-ttu-id="10235-111">将每个 `websiteUrl` 函数 `contentUrl` 中的 和 值更新为选项卡的 HTTPS ngrok URL。</span><span class="sxs-lookup"><span data-stu-id="10235-111">Update the `websiteUrl` and `contentUrl` values in each function with the HTTPS ngrok URL to your tab.</span></span>

    <span data-ttu-id="10235-112">现在，您的代码应如下所示，将 **y8rCgT2b** 替换为 ngrok URL：</span><span class="sxs-lookup"><span data-stu-id="10235-112">Your code should now look like the following with **y8rCgT2b** replaced with your ngrok URL:</span></span>

    ```javascript
        microsoftTeams.initialize();
    
        let saveGray = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }

        let saveRed = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }
    ```

1. <span data-ttu-id="10235-113">确保保存更新的 **Tab.cshtml**。</span><span class="sxs-lookup"><span data-stu-id="10235-113">Make sure to save the updated **Tab.cshtml**.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="10235-114">生成并运行应用程序</span><span class="sxs-lookup"><span data-stu-id="10235-114">Build and run your application</span></span>

<span data-ttu-id="10235-115">In Visual Studio， press **F5** or choose **Start Debugging** from the **Debug** menu.</span><span class="sxs-lookup"><span data-stu-id="10235-115">In Visual Studio, press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="10235-116">通过打开浏览器，然后通过命令提示符窗口中提供的 ngrok HTTPS URL 进入内容页面，验证 **ngrok** 是否正常运行。</span><span class="sxs-lookup"><span data-stu-id="10235-116">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> [!TIP]
> <span data-ttu-id="10235-117">你需要让应用程序在 Visual Studio 和 ngrok 中运行。</span><span class="sxs-lookup"><span data-stu-id="10235-117">You need to have both your application in Visual Studio and ngrok running.</span></span> <span data-ttu-id="10235-118">如果需要停止运行应用程序，Visual Studio运行 **ngrok。**</span><span class="sxs-lookup"><span data-stu-id="10235-118">If you need to stop running your application in Visual Studio to work on it **keep ngrok running**.</span></span> <span data-ttu-id="10235-119">当应用程序在服务器中重新启动时，它将继续侦听并Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="10235-119">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="10235-120">如果必须重新启动 ngrok 服务，它将返回一个新 URL，并且您必须使用新 URL 更新应用程序。</span><span class="sxs-lookup"><span data-stu-id="10235-120">If you have to restart the ngrok service, it will return a new URL and you will have to update your application with the new URL.</span></span>

## <a name="upload-your-tab"></a><span data-ttu-id="10235-121">Upload选项卡</span><span class="sxs-lookup"><span data-stu-id="10235-121">Upload your tab</span></span>

>[!Note]
> <span data-ttu-id="10235-122">App Studio 可用于编辑 **文件上的** manifest.js，以及将已完成的程序包上传到Teams。</span><span class="sxs-lookup"><span data-stu-id="10235-122">App Studio can be used to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="10235-123">如果需要，还可以手动编辑 **manifest.js** 上的文件。</span><span class="sxs-lookup"><span data-stu-id="10235-123">You can also manually edit the **manifest.json** file if you prefer.</span></span> <span data-ttu-id="10235-124">如果这样做，请务必再次构建解决方案，以创建要 **tab.zip** 文件。</span><span class="sxs-lookup"><span data-stu-id="10235-124">If you do, be sure to build the solution again to create the **tab.zip** file to upload.</span></span>

<span data-ttu-id="10235-125">**上传选项卡**</span><span class="sxs-lookup"><span data-stu-id="10235-125">**To upload your tab**</span></span>

1. <span data-ttu-id="10235-126">转到Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="10235-126">Go to Microsoft Teams.</span></span> <span data-ttu-id="10235-127">如果使用基于 [Web 的版本，](https://teams.microsoft.com) 可以使用浏览器的开发人员工具检查前端 [代码](~/tabs/how-to/developer-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="10235-127">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

1. <span data-ttu-id="10235-128">转到 **App Studio，** 然后选择清单 **编辑器** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="10235-128">Go to **App Studio** and select the **Manifest editor** tab.</span></span>

1. <span data-ttu-id="10235-129">选择 **"在清单编辑器** 中导入现有应用"开始为选项卡更新应用包。源代码附带其自己的部分完整清单。</span><span class="sxs-lookup"><span data-stu-id="10235-129">Select **Import an existing app** in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="10235-130">应用包的名称 **tab.zip。**</span><span class="sxs-lookup"><span data-stu-id="10235-130">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="10235-131">它在此处提供：</span><span class="sxs-lookup"><span data-stu-id="10235-131">It is available here:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. <span data-ttu-id="10235-132">Uploadtab.zipApp  Studio。</span><span class="sxs-lookup"><span data-stu-id="10235-132">Upload **tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="10235-133">使用清单编辑器更新应用包</span><span class="sxs-lookup"><span data-stu-id="10235-133">Update your app package with Manifest editor</span></span>

<span data-ttu-id="10235-134">将应用包上传到 App Studio 后，必须完成配置。</span><span class="sxs-lookup"><span data-stu-id="10235-134">After you have uploaded your app package into App Studio, you must finish configuring it.</span></span>

<span data-ttu-id="10235-135">在清单编辑器欢迎页面的右侧面板中选择新导入选项卡的磁贴。</span><span class="sxs-lookup"><span data-stu-id="10235-135">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="10235-136">清单编辑器左侧有一个步骤列表，右侧是一个属性列表，其中每个步骤都必须具有值。</span><span class="sxs-lookup"><span data-stu-id="10235-136">There is a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that must have values for each of those steps.</span></span> <span data-ttu-id="10235-137">大部分信息已由你的manifest.js **提供** ，但是有一些字段必须更新：</span><span class="sxs-lookup"><span data-stu-id="10235-137">Much of the information has been provided by your **manifest.json** but there are a few fields that you must update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="10235-138">详细信息：应用详细信息</span><span class="sxs-lookup"><span data-stu-id="10235-138">Details: App details</span></span>

<span data-ttu-id="10235-139">在" **应用详细信息"** 部分中：</span><span class="sxs-lookup"><span data-stu-id="10235-139">In the **App details** section:</span></span>

1. <span data-ttu-id="10235-140">在 **"标识\*\*\*\*"下**，选择"生成"以将占位符 ID 替换为选项卡所需的 GUID。</span><span class="sxs-lookup"><span data-stu-id="10235-140">Under **Identification**, select **Generate** to replace the placeholder ID with the required GUID for your tab.</span></span>

1. <span data-ttu-id="10235-141">在 **"开发人员信息**" **下，使用** **ngrok** HTTPS URL 更新网站。</span><span class="sxs-lookup"><span data-stu-id="10235-141">Under **Developer information**, update **Website** with your **ngrok** HTTPS URL.</span></span>

1. <span data-ttu-id="10235-142">在 **"应用程序 URL"** 下，将隐私声明更新为 和 `https://<yourngrokurl>/privacy` **使用条款** 以 `https://<yourngrokurl>/tou`>。</span><span class="sxs-lookup"><span data-stu-id="10235-142">Under **App URLs**, update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="10235-143">功能：选项卡</span><span class="sxs-lookup"><span data-stu-id="10235-143">Capabilities: Tabs</span></span>

<span data-ttu-id="10235-144">在" **选项卡"** 部分：</span><span class="sxs-lookup"><span data-stu-id="10235-144">In the **Tabs** section:</span></span>

1. <span data-ttu-id="10235-145">在"**团队"选项卡** 下，选择"**添加"。**</span><span class="sxs-lookup"><span data-stu-id="10235-145">Under **Team tab**, select **Add**.</span></span>

1. <span data-ttu-id="10235-146">在" **团队"选项卡** 弹出窗口中，将" **配置 URL"更新** 为 `https://<yourngrokurl>/tab` 。</span><span class="sxs-lookup"><span data-stu-id="10235-146">In the **Team tab** pop-up window, update the **Configuration URL** to `https://<yourngrokurl>/tab`.</span></span>

1. <span data-ttu-id="10235-147">确保选中 **了"可以更新配置\*\*\*\*？"、"团队**"和"**群聊**"复选框，然后选择"保存 **"。**</span><span class="sxs-lookup"><span data-stu-id="10235-147">Ensure the **Can update configuration?**, **Team**, and **Group chat** checkboxes are selected and select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="10235-148">完成时间：域和权限</span><span class="sxs-lookup"><span data-stu-id="10235-148">Finish: Domains and permissions</span></span>

<span data-ttu-id="10235-149">在" **域和权限"** 部分， **选项卡** 中的"域"必须包含不带 HTTPS 前缀的 ngrok `<yourngrokurl>.ngrok.io/` URL。</span><span class="sxs-lookup"><span data-stu-id="10235-149">In the **Domains and permissions** section, **Domains from your tabs** must contain your ngrok URL without the HTTPS prefix `<yourngrokurl>.ngrok.io/`.</span></span>

#### <a name="finish-test-and-distribute"></a><span data-ttu-id="10235-150">完成：测试和分发</span><span class="sxs-lookup"><span data-stu-id="10235-150">Finish: Test and distribute</span></span>

>[!IMPORTANT]
> <span data-ttu-id="10235-151">在右侧，在 **"说明"** 中，你将看到以下警告：</span><span class="sxs-lookup"><span data-stu-id="10235-151">On the right, in **Description**, you see the following warning:</span></span>
>
> <span data-ttu-id="10235-152">&#9888; "**'validDomains' array cannot contain a tunneling site..."**</span><span class="sxs-lookup"><span data-stu-id="10235-152">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
> <span data-ttu-id="10235-153">在测试选项卡时，可以忽略此警告。</span><span class="sxs-lookup"><span data-stu-id="10235-153">This warning can be ignored while testing your tab.</span></span>

1. <span data-ttu-id="10235-154">在"**测试和分发"部分**，选择"安装 **"。**</span><span class="sxs-lookup"><span data-stu-id="10235-154">In the **Test and Distribute** section, select **Install**.</span></span>

1. <span data-ttu-id="10235-155">在弹出对话框中，选择"添加到团队 **"** 或从下拉列表中选择"**添加到聊天"。**</span><span class="sxs-lookup"><span data-stu-id="10235-155">In the pop-up dialog box, select **Add to a team** or from the drop-down, select **Add to a chat**.</span></span>

1. <span data-ttu-id="10235-156">选择要显示选项卡的团队或聊天，然后选择"**设置选项卡"。**</span><span class="sxs-lookup"><span data-stu-id="10235-156">Choose the team or chat where you want the tab to be displayed and select **Set up a tab**.</span></span>

1. <span data-ttu-id="10235-157">在下一个弹出对话框中，**选择"选择** 灰色"或"**选择红色**"，然后选择"保存 **"。**</span><span class="sxs-lookup"><span data-stu-id="10235-157">In the next pop-up dialog box, choose either **Select Gray** or **Select Red**, and select **Save**.</span></span>

1. <span data-ttu-id="10235-158">若要查看您的选项卡，请转到您安装选项卡的团队，然后从选项卡栏中选择它。</span><span class="sxs-lookup"><span data-stu-id="10235-158">To view your tab, go to the team where you installed the tab, and select it from the tab bar.</span></span> <span data-ttu-id="10235-159">将显示在配置过程中选择的页面。</span><span class="sxs-lookup"><span data-stu-id="10235-159">The page that you chose during configuration is displayed.</span></span>

    ![频道选项卡 ASPNETMVC 已上载](../../assets/images/tab-images/channeltabaspnetmvcuploaded.png)

