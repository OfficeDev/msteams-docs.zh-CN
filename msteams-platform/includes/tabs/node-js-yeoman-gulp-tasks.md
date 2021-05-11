## <a name="create-the-app-package"></a><span data-ttu-id="06114-101">创建应用包</span><span class="sxs-lookup"><span data-stu-id="06114-101">Create the app package</span></span>

<span data-ttu-id="06114-102">你需要一个应用包来测试应用中的Teams。</span><span class="sxs-lookup"><span data-stu-id="06114-102">You'll need an app package to test your tab in Teams.</span></span> <span data-ttu-id="06114-103">它是包含以下所需文件的 zip 文件夹：</span><span class="sxs-lookup"><span data-stu-id="06114-103">It's a zip folder that contains the following required files:</span></span>

- <span data-ttu-id="06114-104">全 **色图标** ，大小为 192 x 192 像素。</span><span class="sxs-lookup"><span data-stu-id="06114-104">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="06114-105">一 **个 32** x 32 像素的透明边框图标。</span><span class="sxs-lookup"><span data-stu-id="06114-105">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="06114-106">指定 **manifest.js** 属性的 on 文件。</span><span class="sxs-lookup"><span data-stu-id="06114-106">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="06114-107">该包是通过 gulp 任务创建的，该任务验证 manifest.json 文件，并生成 中的 zip 文件夹 `./package directory` 。</span><span class="sxs-lookup"><span data-stu-id="06114-107">The package is created via a gulp task that validates the manifest.json file and generates the zip folder in the `./package directory`.</span></span> <span data-ttu-id="06114-108">在命令提示符中输入：</span><span class="sxs-lookup"><span data-stu-id="06114-108">In the command prompt enter:</span></span>

```bash
gulp manifest
```

## <a name="build-your-application"></a><span data-ttu-id="06114-109">生成应用程序</span><span class="sxs-lookup"><span data-stu-id="06114-109">Build your application</span></span>

<span data-ttu-id="06114-110">生成命令将解决方案转换为 *./dist* 文件夹。</span><span class="sxs-lookup"><span data-stu-id="06114-110">The build command transpiles your solution into the *./dist* folder.</span></span> <span data-ttu-id="06114-111">接下来，输入：</span><span class="sxs-lookup"><span data-stu-id="06114-111">Next,enter:</span></span>

```bash
gulp build
```

## <a name="run-your-application-in-localhost"></a><span data-ttu-id="06114-112">在 localhost 中运行应用程序</span><span class="sxs-lookup"><span data-stu-id="06114-112">Run your application in localhost</span></span>

<span data-ttu-id="06114-113">通过输入以下内容启动本地 Web 服务器：</span><span class="sxs-lookup"><span data-stu-id="06114-113">Start a local web server by entering the following:</span></span>

```bash
gulp serve
```

<span data-ttu-id="06114-114">`http://localhost:3007/<yourDefaultAppNameTab>/`在浏览器中输入 ，然后查看应用程序的主页：</span><span class="sxs-lookup"><span data-stu-id="06114-114">Enter `http://localhost:3007/<yourDefaultAppNameTab>/` in your browser and view your application's home page:</span></span>

![主页屏幕截图](~/assets/images/tab-images/homePage.png)