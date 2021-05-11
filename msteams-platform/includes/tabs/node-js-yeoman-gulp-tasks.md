## <a name="create-the-app-package"></a>创建应用包

你需要一个应用包来测试应用中的Teams。 它是包含以下所需文件的 zip 文件夹：

- 全 **色图标** ，大小为 192 x 192 像素。
- 一 **个 32** x 32 像素的透明边框图标。
- 指定 **manifest.js** 属性的 on 文件。

该包是通过 gulp 任务创建的，该任务验证 manifest.json 文件，并生成 中的 zip 文件夹 `./package directory` 。 在命令提示符中输入：

```bash
gulp manifest
```

## <a name="build-your-application"></a>生成应用程序

生成命令将解决方案转换为 *./dist* 文件夹。 接下来，输入：

```bash
gulp build
```

## <a name="run-your-application-in-localhost"></a>在 localhost 中运行应用程序

通过输入以下内容启动本地 Web 服务器：

```bash
gulp serve
```

`http://localhost:3007/<yourDefaultAppNameTab>/`在浏览器中输入 ，然后查看应用程序的主页：

![主页屏幕截图](~/assets/images/tab-images/homePage.png)