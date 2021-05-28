### <a name="optional-adjust-your-browser-launch-settings"></a><span data-ttu-id="3e8f3-101"> (可选) 调整浏览器启动设置</span><span class="sxs-lookup"><span data-stu-id="3e8f3-101">(Optional) Adjust your browser launch settings</span></span>

<span data-ttu-id="3e8f3-102">在开发Teams应用时，通常使用备用开发人员租户或备用凭据运行应用。</span><span class="sxs-lookup"><span data-stu-id="3e8f3-102">When developing a Teams app, it is common to run your app in an alternate developer tenant or with alternate credentials.</span></span>  <span data-ttu-id="3e8f3-103">Microsoft Edge和 Google Chrome 都提供用于调整浏览器的启动设置设施。</span><span class="sxs-lookup"><span data-stu-id="3e8f3-103">Both Microsoft Edge and Google Chrome provide facilities to adjust the launch settings for your browser.</span></span>  <span data-ttu-id="3e8f3-104">例如，若要更新项目以支持 InPrivate 模式 (Microsoft Edge) ，请打开 `.vscode/launch.json` 项目中的文件。</span><span class="sxs-lookup"><span data-stu-id="3e8f3-104">For example, to update the project to support InPrivate mode (Microsoft Edge), open the `.vscode/launch.json` file in your project.</span></span>  <span data-ttu-id="3e8f3-105">查找相应的启动设置，并在每个设置中添加以下块：</span><span class="sxs-lookup"><span data-stu-id="3e8f3-105">Look for the appropriate launch settings, and add the following block to each one:</span></span>

``` json
"runtimeArgs": [ "--inprivate" ]
```

<span data-ttu-id="3e8f3-106">例如，在本地运行的启动设置如下所示：</span><span class="sxs-lookup"><span data-stu-id="3e8f3-106">For instance, the launch setting for running locally looks like this:</span></span>

``` json
{
   "name": "Start and Attach to Frontend (Edge)",
   "type": "pwa-msedge",
   "request": "launch",
   "url": "https://teams.microsoft.com/_#/l/app/${localTeamsAppId}?installAppPackage=true",
   "preLaunchTask": "Start Frontend",
   "postDebugTask": "Stop All Services",
   "presentation": {
         "group": "all",
         "hidden": true
   },
   "runtimeArgs": [ "--inprivate" ]
},
```

<span data-ttu-id="3e8f3-107">或者，可以将浏览器配置为使用上一个已知配置文件。</span><span class="sxs-lookup"><span data-stu-id="3e8f3-107">Alternatively, you can configure your browser to use the last known profile.</span></span> <span data-ttu-id="3e8f3-108">[在"新建配置文件"Microsoft Edge。](https://support.microsoft.com/topic/sign-in-and-create-multiple-profiles-in-microsoft-edge-df94e622-2061-49ae-ad1d-6f0e43ce6435)</span><span class="sxs-lookup"><span data-stu-id="3e8f3-108">[Create a new profile](https://support.microsoft.com/topic/sign-in-and-create-multiple-profiles-in-microsoft-edge-df94e622-2061-49ae-ad1d-6f0e43ce6435) in Microsoft Edge.</span></span>  <span data-ttu-id="3e8f3-109">然后，调整设置以将上一个已知配置文件用于新链接：</span><span class="sxs-lookup"><span data-stu-id="3e8f3-109">Then adjust the settings to use the last known profile for new links:</span></span>

- <span data-ttu-id="3e8f3-110">在Microsoft Edge中，打开 `edge://settings/profiles/multiProfileSettings` 。</span><span class="sxs-lookup"><span data-stu-id="3e8f3-110">In Microsoft Edge, open `edge://settings/profiles/multiProfileSettings`.</span></span>
- <span data-ttu-id="3e8f3-111">关闭自动 **配置文件切换**。</span><span class="sxs-lookup"><span data-stu-id="3e8f3-111">Turn off **Automatic profile switching**.</span></span>
- <span data-ttu-id="3e8f3-112">对于"**外部链接的默认配置文件"，选择**"上次 **使用 (默认) "。**</span><span class="sxs-lookup"><span data-stu-id="3e8f3-112">For the **Default profile for external links**, select **Last used (default)**.</span></span>

<span data-ttu-id="3e8f3-113">在调试应用之前，请确保浏览器已打开到正确的配置文件。</span><span class="sxs-lookup"><span data-stu-id="3e8f3-113">Ensure your browser is opened to the correct profile before debugging your app.</span></span>
