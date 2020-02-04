### <a name="_layoutcshtml"></a><span data-ttu-id="a848f-101">_Layout cshtml</span><span class="sxs-lookup"><span data-stu-id="a848f-101">_Layout.cshtml</span></span>

<span data-ttu-id="a848f-102">若要在团队中显示您的选项卡，您必须包含**Microsoft 团队 JavaScript 客户端 SDK** ，并`microsoftTeams.initialize()`在加载页面后包含一个调用。</span><span class="sxs-lookup"><span data-stu-id="a848f-102">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="a848f-103">这就是选项卡和团队客户端之间的通信方式：</span><span class="sxs-lookup"><span data-stu-id="a848f-103">This is how your tab and the Teams client communicate:</span></span>

- <span data-ttu-id="a848f-104">导航到**共享**文件夹，打开 **_Layout. cshtml**，并将以下内容添加到`<head>`标记：</span><span class="sxs-lookup"><span data-stu-id="a848f-104">Navigate to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tag:</span></span>

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

>[!IMPORTANT]
><span data-ttu-id="a848f-105">请勿复制/粘贴此`<script src="...">`页面中的 url，因为它们可能不代表最新版本。</span><span class="sxs-lookup"><span data-stu-id="a848f-105">Don't copy/paste the `<script src="...">` URLs from this page, as they may not represent the latest version.</span></span> <span data-ttu-id="a848f-106">若要获取最新版本的 SDK，请始终转到： [Microsoft 团队 JAVASCRIPT API](https://www.npmjs.com/package/@microsoft/teams-js.com)。</span><span class="sxs-lookup"><span data-stu-id="a848f-106">To get the latest version of the SDK, always go to: [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js.com).</span></span>

### <a name="tabcshtml"></a><span data-ttu-id="a848f-107">选项卡. cshtml</span><span class="sxs-lookup"><span data-stu-id="a848f-107">Tab.cshtml</span></span>

<span data-ttu-id="a848f-108">打开**选项卡. cshtml**并更新嵌入`<script>`的，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a848f-108">Open **Tab.cshtml** and update the embedded `<script>` as follows:</span></span>

- <span data-ttu-id="a848f-109">在脚本的顶部，调用`microsoftTeams.initialize()`。</span><span class="sxs-lookup"><span data-stu-id="a848f-109">At the top of the script, call `microsoftTeams.initialize()`.</span></span>

- <span data-ttu-id="a848f-110">使用 HTTPS `websiteUrl` ngrok `contentUrl` URL 将每个函数中的和值更新到您的选项卡。</span><span class="sxs-lookup"><span data-stu-id="a848f-110">Update the `websiteUrl` and `contentUrl` values in each function with the HTTPS ngrok URL to your tab.</span></span>

<span data-ttu-id="a848f-111">您的代码现在应如下所示， **y8rCgT2b**替换为您的 ngrok URL：</span><span class="sxs-lookup"><span data-stu-id="a848f-111">Your code should now look like the following with **y8rCgT2b** replaced with your ngrok URL:</span></span>

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

<span data-ttu-id="a848f-112">请务必保存更新的**选项卡. cshtml**。</span><span class="sxs-lookup"><span data-stu-id="a848f-112">Make sure to save the updated **Tab.cshtml**.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="a848f-113">生成并运行应用程序</span><span class="sxs-lookup"><span data-stu-id="a848f-113">Build and run your application</span></span>

- <span data-ttu-id="a848f-114">在 Visual Studio 中按**F5**，或从 "**调试**" 菜单中选择 "**启动调试**"。</span><span class="sxs-lookup"><span data-stu-id="a848f-114">In Visual Studio press **F5**, or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="a848f-115">通过在命令提示符窗口中提供的 ngrok HTTPS URL 打开浏览器并转到内容页，验证**ngrok**是否正在运行并正常运行。</span><span class="sxs-lookup"><span data-stu-id="a848f-115">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

>[!TIP]
><span data-ttu-id="a848f-116">您需要在 Visual Studio 和 ngrok 中同时运行应用程序，才能完成此快速入门。</span><span class="sxs-lookup"><span data-stu-id="a848f-116">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="a848f-117">如果需要在 Visual Studio 中停止运行应用程序以使用它，**请继续运行 ngrok**。</span><span class="sxs-lookup"><span data-stu-id="a848f-117">If you need to stop running your application in Visual Studio to work on it **keep ngrok running**.</span></span> <span data-ttu-id="a848f-118">它将继续侦听，并将在 Visual Studio 中重新启动时继续路由应用程序的请求。</span><span class="sxs-lookup"><span data-stu-id="a848f-118">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="a848f-119">如果您必须重新启动 ngrok 服务，它将返回一个新的 URL，您必须使用新的 URL 更新应用程序。</span><span class="sxs-lookup"><span data-stu-id="a848f-119">If you have to restart the ngrok service it will return a new URL and you'll have to update your application with the new URL.</span></span>

## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="a848f-120">将您的选项卡上传给具有应用程序 Studio 的团队</span><span class="sxs-lookup"><span data-stu-id="a848f-120">Upload your tab to Teams with App Studio</span></span>

>[!Note]
> <span data-ttu-id="a848f-121">我们使用应用程序 Studio 编辑您的**清单 json**文件并将已完成的包上载到团队。</span><span class="sxs-lookup"><span data-stu-id="a848f-121">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="a848f-122">如果愿意，也可以手动编辑**清单 json**文件。</span><span class="sxs-lookup"><span data-stu-id="a848f-122">You can also manually edit the **manifest.json** file if you prefer.</span></span> <span data-ttu-id="a848f-123">如果这样做，请务必再次生成解决方案，以创建要上载的**tab .zip**文件。</span><span class="sxs-lookup"><span data-stu-id="a848f-123">If you do, be sure to build the solution again to create the **tab.zip** file to upload.</span></span>

- <span data-ttu-id="a848f-124">打开 Microsoft 团队客户端。</span><span class="sxs-lookup"><span data-stu-id="a848f-124">Open the Microsoft Teams client.</span></span> <span data-ttu-id="a848f-125">如果您使用的是[基于 web 的版本](https://teams.microsoft.com)，则可以使用浏览器的[开发人员工具](~/tabs/how-to/developer-tools.md)检查您的前端代码。</span><span class="sxs-lookup"><span data-stu-id="a848f-125">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="a848f-126">打开应用程序 studio 并选择 "**清单编辑器**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="a848f-126">Open App studio and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="a848f-127">选择 "在清单编辑器中**导入现有的应用程序**磁贴" 以开始更新选项卡的应用程序包。源代码附带其自己完整的清单。</span><span class="sxs-lookup"><span data-stu-id="a848f-127">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="a848f-128">您的应用程序包的名称为 **"tab .zip**"。</span><span class="sxs-lookup"><span data-stu-id="a848f-128">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="a848f-129">应在此处找到：</span><span class="sxs-lookup"><span data-stu-id="a848f-129">It should be found here:</span></span>

```bash
/bin/Debug/netcoreapp2.2/tab.zip
```

- <span data-ttu-id="a848f-130">将**选项卡**上传到应用程序 Studio。</span><span class="sxs-lookup"><span data-stu-id="a848f-130">Upload **tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="a848f-131">使用清单编辑器更新应用程序包</span><span class="sxs-lookup"><span data-stu-id="a848f-131">Update your app package with Manifest editor</span></span>

<span data-ttu-id="a848f-132">将应用程序包上载到应用程序 Studio 后，需要完成对其进行配置。</span><span class="sxs-lookup"><span data-stu-id="a848f-132">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="a848f-133">在清单编辑器的 "欢迎" 页的右面板中，为新导入的选项卡选择磁贴。</span><span class="sxs-lookup"><span data-stu-id="a848f-133">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="a848f-134">清单编辑器的左侧有一个步骤列表，在右侧是需要为每个步骤的值提供值的属性的列表。</span><span class="sxs-lookup"><span data-stu-id="a848f-134">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="a848f-135">大部分信息已由您的*清单 json*提供，但有几个字段需要更新：</span><span class="sxs-lookup"><span data-stu-id="a848f-135">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="a848f-136">详细信息：应用程序详细信息</span><span class="sxs-lookup"><span data-stu-id="a848f-136">Details: App details</span></span>

- <span data-ttu-id="a848f-137">在 "*标识*" 下，选择 "***生成***" 以将占位符 id 替换为您的选项卡所需的 GUID。</span><span class="sxs-lookup"><span data-stu-id="a848f-137">Under *Identification* select ***Generate*** to replace the placeholder id with the required GUID for your tab.</span></span>

- <span data-ttu-id="a848f-138">在 "*开发人员信息*" 下，使用您的*ngrok* HTTPS URL 更新**网站 URL**字段。</span><span class="sxs-lookup"><span data-stu-id="a848f-138">Under *Developer information* update the **Website URL** field with your *ngrok* HTTPS URL.</span></span>

- <span data-ttu-id="a848f-139">在 "*应用程序 url* " 下，使用您的*ngrok* HTTPS Url 更新**隐私声明**和**使用条款**url 字段。</span><span class="sxs-lookup"><span data-stu-id="a848f-139">Under *App URLs* update the **Privacy statement** and **Terms of use** URL fields with your *ngrok* HTTPS URL.</span></span> <span data-ttu-id="a848f-140">请记住将 */privacy*和 */tou*路径包含在 url 的末尾。</span><span class="sxs-lookup"><span data-stu-id="a848f-140">Remember to include the */privacy* and */tou* paths at the end of the URLs.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="a848f-141">功能：选项卡</span><span class="sxs-lookup"><span data-stu-id="a848f-141">Capabilities: Tabs</span></span>

<span data-ttu-id="a848f-142">在 "*选项卡*" 部分：</span><span class="sxs-lookup"><span data-stu-id="a848f-142">In the *Tabs* section:</span></span>

- <span data-ttu-id="a848f-143">在 "*团队" 选项卡*下选择 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="a848f-143">Under *Team Tab* select **Add**.</span></span>

- <span data-ttu-id="a848f-144">在 "团队" 选项卡弹出窗口中，将*配置 URL*更新为`https://<yourngrokurl>/tab`。</span><span class="sxs-lookup"><span data-stu-id="a848f-144">In the Team tab pop-up window update the *Configuration URL* to `https://<yourngrokurl>/tab`.</span></span>

- <span data-ttu-id="a848f-145">最后，请确保*可以更新配置？* 将选中 "团队" 和 "*组" 聊天*框，然后选择 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="a848f-145">Finally, make sure the *can update configuration? Team*, and *Group chat* boxes are checked and select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="a848f-146">完成：域和权限</span><span class="sxs-lookup"><span data-stu-id="a848f-146">Finish: Domains and permissions</span></span>

<span data-ttu-id="a848f-147">在 "*域和权限*" 部分中，"*选项卡*" 字段中的域应包含不带 HTTPS 前缀`<yourngrokurl>.ngrok.io/`的 ngrok URL。</span><span class="sxs-lookup"><span data-stu-id="a848f-147">In the *Domains and permissions* section, the *Domains from your tabs* field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

#### <a name="test-and-distribute-test-and-distribute"></a><span data-ttu-id="a848f-148">测试和分发：测试和分发</span><span class="sxs-lookup"><span data-stu-id="a848f-148">Test and distribute: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="a848f-149">在右侧的 "**说明**" 字段中，将看到以下警告：</span><span class="sxs-lookup"><span data-stu-id="a848f-149">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="a848f-150">&#9888; "**validDomains" 数组不能包含隧道站点 ...**"</span><span class="sxs-lookup"><span data-stu-id="a848f-150">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="a848f-151">在测试选项卡时可以忽略此警告。</span><span class="sxs-lookup"><span data-stu-id="a848f-151">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="a848f-152">在 "*测试和分发*" 部分：</span><span class="sxs-lookup"><span data-stu-id="a848f-152">In the *Test and distribute* section:</span></span>

- <span data-ttu-id="a848f-153">选择“**安装**”。</span><span class="sxs-lookup"><span data-stu-id="a848f-153">Select **Install**.</span></span>

- <span data-ttu-id="a848f-154">在弹出窗口的 "*添加到团队" 或 "聊天*" 字段中，输入您的团队并选择 "**安装**"。</span><span class="sxs-lookup"><span data-stu-id="a848f-154">In the pop-up window's *Add to a team or chat* field enter your team and select **Install**.</span></span>

- <span data-ttu-id="a848f-155">在下一个弹出窗口中，选择要在其中显示选项卡的团队频道，然后选择 "**设置**"。</span><span class="sxs-lookup"><span data-stu-id="a848f-155">In the next pop-up window choose the team channel where you would like the tab displayed and select **Set up**.</span></span>

- <span data-ttu-id="a848f-156">在最终弹出窗口中，选择选项卡页的值（红色或灰色图标），然后选择 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="a848f-156">In the final pop-up window select a value for the tab page (either a red or gray icon) and select **Save**.</span></span>

<span data-ttu-id="a848f-157">若要查看您的选项卡，请导航到安装它的团队，然后从选项卡栏中选择它。</span><span class="sxs-lookup"><span data-stu-id="a848f-157">To view your tab, navigate to the team you installed it on, and select it from the tab bar.</span></span> <span data-ttu-id="a848f-158">应显示在配置过程中选择的页面。</span><span class="sxs-lookup"><span data-stu-id="a848f-158">The page that you chose during configuration should be displayed.</span></span>
