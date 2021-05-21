### <a name="_layoutcshtml"></a><span data-ttu-id="4390f-101">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="4390f-101">_Layout.cshtml</span></span>

<span data-ttu-id="4390f-102">若要在页面中显示选项卡Teams，必须包含 **Microsoft Teams JavaScript** 客户端 SDK，并包括页面加载 `microsoftTeams.initialize()` 后对 的调用。</span><span class="sxs-lookup"><span data-stu-id="4390f-102">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="4390f-103">这是选项卡和客户端Teams的方式：</span><span class="sxs-lookup"><span data-stu-id="4390f-103">This is how your tab and the Teams client communicate:</span></span>

- <span data-ttu-id="4390f-104">导航到 **"共享** "文件夹，打开 **_Layout.cshtml**，然后向 标记中添加 `<head>` 以下内容：</span><span class="sxs-lookup"><span data-stu-id="4390f-104">Navigate to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tag:</span></span>

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

>[!IMPORTANT]
><span data-ttu-id="4390f-105">不要复制/粘贴此页面中的 `<script src="...">` URL，因为它们可能并不代表最新版本。</span><span class="sxs-lookup"><span data-stu-id="4390f-105">Don't copy/paste the `<script src="...">` URLs from this page, as they may not represent the latest version.</span></span> <span data-ttu-id="4390f-106">若要获取最新版本的 SDK，请始终转到[：Microsoft Teams JavaScript API。](https://www.npmjs.com/package/@microsoft/teams-js)</span><span class="sxs-lookup"><span data-stu-id="4390f-106">To get the latest version of the SDK, always go to: [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js).</span></span>

### <a name="tabcshtml"></a><span data-ttu-id="4390f-107">Tab.cshtml</span><span class="sxs-lookup"><span data-stu-id="4390f-107">Tab.cshtml</span></span>

<span data-ttu-id="4390f-108">打开 **Tab.cshtml** 并更新嵌入 `<script>` 的内容，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4390f-108">Open **Tab.cshtml** and update the embedded `<script>` as follows:</span></span>

- <span data-ttu-id="4390f-109">在脚本顶部，调用 `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="4390f-109">At the top of the script, call `microsoftTeams.initialize()`.</span></span>

- <span data-ttu-id="4390f-110">将每个 `websiteUrl` 函数 `contentUrl` 中的 和 值更新为选项卡的 HTTPS ngrok URL。</span><span class="sxs-lookup"><span data-stu-id="4390f-110">Update the `websiteUrl` and `contentUrl` values in each function with the HTTPS ngrok URL to your tab.</span></span>

<span data-ttu-id="4390f-111">现在，您的代码应如下所示，将 **y8rCgT2b** 替换为 ngrok URL：</span><span class="sxs-lookup"><span data-stu-id="4390f-111">Your code should now look like the following with **y8rCgT2b** replaced with your ngrok URL:</span></span>

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

<span data-ttu-id="4390f-112">确保保存更新的 **Tab.cshtml**。</span><span class="sxs-lookup"><span data-stu-id="4390f-112">Make sure to save the updated **Tab.cshtml**.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="4390f-113">生成并运行应用程序</span><span class="sxs-lookup"><span data-stu-id="4390f-113">Build and run your application</span></span>

- <span data-ttu-id="4390f-114">In Visual Studio press **F5**， or choose **Start Debugging** from the **Debug** menu.</span><span class="sxs-lookup"><span data-stu-id="4390f-114">In Visual Studio press **F5**, or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="4390f-115">通过打开浏览器，然后通过命令提示符窗口中提供的 ngrok HTTPS URL 进入内容页面，验证 **ngrok** 是否正常运行。</span><span class="sxs-lookup"><span data-stu-id="4390f-115">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

>[!TIP]
><span data-ttu-id="4390f-116">你需要让应用程序在 Visual Studio 和 ngrok 中运行才能完成此快速入门。</span><span class="sxs-lookup"><span data-stu-id="4390f-116">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="4390f-117">如果需要停止运行应用程序，Visual Studio运行 **ngrok。**</span><span class="sxs-lookup"><span data-stu-id="4390f-117">If you need to stop running your application in Visual Studio to work on it **keep ngrok running**.</span></span> <span data-ttu-id="4390f-118">当应用程序在服务器中重新启动时，它将继续侦听并Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="4390f-118">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="4390f-119">如果必须重新启动 ngrok 服务，它将返回一个新 URL，并且您必须使用新 URL 更新应用程序。</span><span class="sxs-lookup"><span data-stu-id="4390f-119">If you have to restart the ngrok service it will return a new URL and you'll have to update your application with the new URL.</span></span>

## <a name="upload-your-tab-to-teams"></a><span data-ttu-id="4390f-120">Upload选项卡以Teams</span><span class="sxs-lookup"><span data-stu-id="4390f-120">Upload your tab to Teams</span></span>

>[!Note]
> <span data-ttu-id="4390f-121">我们使用 App Studio 编辑你的manifest.js **文件**，将已完成的程序包上传到Teams。</span><span class="sxs-lookup"><span data-stu-id="4390f-121">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="4390f-122">如果需要，还可以手动编辑 **manifest.js** 上的文件。</span><span class="sxs-lookup"><span data-stu-id="4390f-122">You can also manually edit the **manifest.json** file if you prefer.</span></span> <span data-ttu-id="4390f-123">如果这样做，请务必再次构建解决方案，以创建要 **tab.zip** 文件。</span><span class="sxs-lookup"><span data-stu-id="4390f-123">If you do, be sure to build the solution again to create the **tab.zip** file to upload.</span></span>

- <span data-ttu-id="4390f-124">打开 Microsoft Teams 客户端。</span><span class="sxs-lookup"><span data-stu-id="4390f-124">Open the Microsoft Teams client.</span></span> <span data-ttu-id="4390f-125">如果使用基于 [Web 的版本，](https://teams.microsoft.com) 可以使用浏览器的开发人员工具检查前端 [代码](~/tabs/how-to/developer-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="4390f-125">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="4390f-126">打开 App Studio 并选择清单 **编辑器** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="4390f-126">Open App studio and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="4390f-127">选择清单 **编辑器中的** "导入现有应用"磁贴，开始为选项卡更新应用包。源代码附带其自己的部分完整清单。</span><span class="sxs-lookup"><span data-stu-id="4390f-127">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="4390f-128">应用包的名称 **tab.zip。**</span><span class="sxs-lookup"><span data-stu-id="4390f-128">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="4390f-129">应在此处找到它：</span><span class="sxs-lookup"><span data-stu-id="4390f-129">It should be found here:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

- <span data-ttu-id="4390f-130">Uploadtab.zipApp  Studio。</span><span class="sxs-lookup"><span data-stu-id="4390f-130">Upload **tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="4390f-131">使用清单编辑器更新应用包</span><span class="sxs-lookup"><span data-stu-id="4390f-131">Update your app package with Manifest editor</span></span>

<span data-ttu-id="4390f-132">将应用包上传到 App Studio 后，你将需要完成它的配置。</span><span class="sxs-lookup"><span data-stu-id="4390f-132">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="4390f-133">在清单编辑器欢迎页面的右侧面板中选择新导入选项卡的磁贴。</span><span class="sxs-lookup"><span data-stu-id="4390f-133">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="4390f-134">清单编辑器左侧有一个步骤列表，右侧是一个属性列表，其中每个步骤都需要有值。</span><span class="sxs-lookup"><span data-stu-id="4390f-134">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="4390f-135">大部分信息已由你的manifest.js *提供* ，但是有一些字段需要更新：</span><span class="sxs-lookup"><span data-stu-id="4390f-135">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="4390f-136">详细信息：应用详细信息</span><span class="sxs-lookup"><span data-stu-id="4390f-136">Details: App details</span></span>

<span data-ttu-id="4390f-137">在" *应用详细信息"* 部分中：</span><span class="sxs-lookup"><span data-stu-id="4390f-137">In the *App details* section:</span></span>

- <span data-ttu-id="4390f-138">*标识*： **选择"** 生成"以将占位符 ID 替换为选项卡所需的 GUID。</span><span class="sxs-lookup"><span data-stu-id="4390f-138">*Identification*: select **Generate** to replace the placeholder id with the required GUID for your tab.</span></span>

- <span data-ttu-id="4390f-139">*开发人员信息*：使用 *ngrok* **HTTPS URL** 更新"网站 URL"字段。</span><span class="sxs-lookup"><span data-stu-id="4390f-139">*Developer information*: update the **Website URL** field with your *ngrok* HTTPS URL.</span></span>

- <span data-ttu-id="4390f-140">*应用 URL：* 将 **隐私声明更新** 为 ，将使用条款 `https://<yourngrokurl>/privacy` **更新** 为 `https://<yourngrokurl>/tou`>。</span><span class="sxs-lookup"><span data-stu-id="4390f-140">*App URLs*: update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="4390f-141">功能：选项卡</span><span class="sxs-lookup"><span data-stu-id="4390f-141">Capabilities: Tabs</span></span>

<span data-ttu-id="4390f-142">在" *选项卡"* 部分：</span><span class="sxs-lookup"><span data-stu-id="4390f-142">In the *Tabs* section:</span></span>

- <span data-ttu-id="4390f-143">*团队选项卡：* 选择 **添加**。</span><span class="sxs-lookup"><span data-stu-id="4390f-143">*Team Tab*: select **Add**.</span></span>

- <span data-ttu-id="4390f-144">在"团队"选项卡弹出窗口中，将 *"配置 URL"更新* 为 `https://<yourngrokurl>/tab` 。</span><span class="sxs-lookup"><span data-stu-id="4390f-144">In the Team tab pop-up window update the *Configuration URL* to `https://<yourngrokurl>/tab`.</span></span>

- <span data-ttu-id="4390f-145">最后，确保 *可以更新配置？选中*"团队"和"*群聊*"框，然后选择"保存 **"。**</span><span class="sxs-lookup"><span data-stu-id="4390f-145">Finally, make sure the *can update configuration? Team*, and *Group chat* boxes are checked and select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="4390f-146">完成时间：域和权限</span><span class="sxs-lookup"><span data-stu-id="4390f-146">Finish: Domains and permissions</span></span>

<span data-ttu-id="4390f-147">在 *"域和权限"* 部分：</span><span class="sxs-lookup"><span data-stu-id="4390f-147">In the *Domains and permissions* section:</span></span>

- <span data-ttu-id="4390f-148">选项卡 *字段中的"* 域"应包含没有 HTTPS 前缀的 ngrok URL- `<yourngrokurl>.ngrok.io/` 。</span><span class="sxs-lookup"><span data-stu-id="4390f-148">The *Domains from your tabs* field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

#### <a name="finish-test-and-distribute"></a><span data-ttu-id="4390f-149">完成：测试和分发</span><span class="sxs-lookup"><span data-stu-id="4390f-149">Finish: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="4390f-150">在 **右侧** "说明"字段中，你将看到以下警告：</span><span class="sxs-lookup"><span data-stu-id="4390f-150">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="4390f-151">&#9888; "**'validDomains' array cannot contain a tunneling site..."**</span><span class="sxs-lookup"><span data-stu-id="4390f-151">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="4390f-152">在测试选项卡时，可以忽略此警告。</span><span class="sxs-lookup"><span data-stu-id="4390f-152">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="4390f-153">在" *测试和分发"部分* ：</span><span class="sxs-lookup"><span data-stu-id="4390f-153">In the *Test and distribute* section:</span></span>

- <span data-ttu-id="4390f-154">选择“**安装**”。</span><span class="sxs-lookup"><span data-stu-id="4390f-154">Select **Install**.</span></span>

- <span data-ttu-id="4390f-155">在弹出窗口的"添加到团队或聊天"字段中，输入你的团队，然后选择"安装 **"。**</span><span class="sxs-lookup"><span data-stu-id="4390f-155">In the pop-up window's *Add to a team or chat* field enter your team and select **Install**.</span></span>

- <span data-ttu-id="4390f-156">In the next pop-up window choose the team channel where you would like the tab displayed and select **Set up**.</span><span class="sxs-lookup"><span data-stu-id="4390f-156">In the next pop-up window choose the team channel where you would like the tab displayed and select **Set up**.</span></span>

- <span data-ttu-id="4390f-157">在最终弹出窗口中，选择选项卡页的值 (红色或灰色图标) 保存 **"。**</span><span class="sxs-lookup"><span data-stu-id="4390f-157">In the final pop-up window select a value for the tab page (either a red or gray icon) and select **Save**.</span></span>

<span data-ttu-id="4390f-158">若要查看您的选项卡，请导航到安装它的团队，然后从选项卡栏中选择它。</span><span class="sxs-lookup"><span data-stu-id="4390f-158">To view your tab, navigate to the team you installed it on, and select it from the tab bar.</span></span> <span data-ttu-id="4390f-159">应显示在配置期间选择的页面。</span><span class="sxs-lookup"><span data-stu-id="4390f-159">The page that you chose during configuration should be displayed.</span></span>
