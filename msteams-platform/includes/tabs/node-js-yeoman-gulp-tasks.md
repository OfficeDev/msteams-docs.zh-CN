## <a name="create-the-app-package"></a>创建应用程序包

您需要一个应用程序包来测试您在团队中的选项卡。 它是一个包含以下所需文件的 zip 文件夹：

- 以 192 x 192 像素为单位的**完整彩色图标**。
- 一个**透明的大纲图标**，用于度量 32 x 32 像素。
- 一个指定应用程序的属性的**清单 json**文件。

该包是通过验证清单 json 文件的 gulp 任务创建的，并在中生成 zip 文件夹`./package directory`。 在命令提示符下输入：

```bash
gulp manifest
```

## <a name="build-your-application"></a>生成应用程序

"生成" 命令将您的解决方案 transpiles 到 */dist*文件夹中。 接下来，输入以下内容：

```bash
gulp build
```

## <a name="run-your-application-in-localhost"></a>在 localhost 中运行应用程序

通过输入以下命令来启动本地 web 服务器：

```bash
gulp serve
```

在`http://localhost:3007/<yourDefaultAppNameTab>/`浏览器中输入并查看您的应用程序的主页：

![主页屏幕截图](~/assets/images/tab-images/homePage.png)