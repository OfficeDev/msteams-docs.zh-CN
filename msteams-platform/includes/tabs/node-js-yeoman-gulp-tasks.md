## <a name="create-the-app-package"></a><span data-ttu-id="42798-101">创建应用程序包</span><span class="sxs-lookup"><span data-stu-id="42798-101">Create the app package</span></span>

<span data-ttu-id="42798-102">您需要一个应用程序包来测试您在团队中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="42798-102">You'll need an app package to test your tab in Teams.</span></span> <span data-ttu-id="42798-103">它是一个包含以下所需文件的 zip 文件夹：</span><span class="sxs-lookup"><span data-stu-id="42798-103">It's a zip folder that contains the following required files:</span></span>

- <span data-ttu-id="42798-104">以 192 x 192 像素为单位的**完整彩色图标**。</span><span class="sxs-lookup"><span data-stu-id="42798-104">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="42798-105">一个**透明的大纲图标**，用于度量 32 x 32 像素。</span><span class="sxs-lookup"><span data-stu-id="42798-105">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="42798-106">一个指定应用程序的属性的**清单 json**文件。</span><span class="sxs-lookup"><span data-stu-id="42798-106">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="42798-107">该包是通过验证清单 json 文件的 gulp 任务创建的，并在中生成 zip 文件夹`./package directory`。</span><span class="sxs-lookup"><span data-stu-id="42798-107">The package is created via a gulp task that validates the manifest.json file and generates the zip folder in the `./package directory`.</span></span> <span data-ttu-id="42798-108">在命令提示符下输入：</span><span class="sxs-lookup"><span data-stu-id="42798-108">In the command prompt enter:</span></span>

```bash
gulp manifest
```

## <a name="build-your-application"></a><span data-ttu-id="42798-109">生成应用程序</span><span class="sxs-lookup"><span data-stu-id="42798-109">Build your application</span></span>

<span data-ttu-id="42798-110">"生成" 命令将您的解决方案 transpiles 到 */dist*文件夹中。</span><span class="sxs-lookup"><span data-stu-id="42798-110">The build command transpiles your solution into the *./dist* folder.</span></span> <span data-ttu-id="42798-111">接下来，输入以下内容：</span><span class="sxs-lookup"><span data-stu-id="42798-111">Next,enter:</span></span>

```bash
gulp build
```

## <a name="run-your-application-in-localhost"></a><span data-ttu-id="42798-112">在 localhost 中运行应用程序</span><span class="sxs-lookup"><span data-stu-id="42798-112">Run your application in localhost</span></span>

<span data-ttu-id="42798-113">通过输入以下命令来启动本地 web 服务器：</span><span class="sxs-lookup"><span data-stu-id="42798-113">Start a local web server by entering the following:</span></span>

```bash
gulp serve
```

<span data-ttu-id="42798-114">在`http://localhost:3007/<yourDefaultAppNameTab>/`浏览器中输入并查看您的应用程序的主页：</span><span class="sxs-lookup"><span data-stu-id="42798-114">Enter `http://localhost:3007/<yourDefaultAppNameTab>/` in your browser and view your application's home page:</span></span>

![主页屏幕截图](~/assets/images/tab-images/homePage.png)