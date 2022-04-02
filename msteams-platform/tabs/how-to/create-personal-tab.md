---
title: 创建个人选项卡
author: laujan
description: 使用 Yeoman 生成器、ASP.NET Core 或 ASP.NET Core MVC 为 Microsoft Teams 创建个人选项卡的快速入门Node.js，并更新应用清单。
ms.localizationpriority: medium
ms.topic: quickstart
ms.author: lajanuar
keywords: yeoman ASP.NET MVC 程序包 appmanifest 会话域权限存储
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: 25eb2c75ea59c52cb7fb8878e3cfddde02f0db6d
ms.sourcegitcommit: 2236204ff710f4eca606ceffb233572981f6edbe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/01/2022
ms.locfileid: "64614542"
---
# <a name="create-a-personal-tab"></a>创建个人选项卡

个人选项卡和个人范围的机器人一样，是个人应用的一部分，只作用于一个用户。 可以固定到左窗格，方便访问。 还可以为[个人选项卡重新](#reorder-static-personal-tabs)排序[和`registerOnFocused`添加 API](#add-registeronfocused-api-for-tabs-or-personal-apps)。

确保您具有生成 [个人选项卡的所有 prerequsites](~/tabs/how-to/tab-requirements.md) 。

::: zone pivot="node-java-script"

## <a name="create-a-personal-tab-with-nodejs"></a>创建具有"个人"选项卡Node.js

1. 在命令提示符下，在安装以下命令后输入以下命令，以安装 [Yeoman](https://yeoman.io/) 和 [gulp-cli](https://www.npmjs.com/package/gulp-cli) Node.js：

    ```cmd
    npm install yo gulp-cli --global
    ```

1. 在命令提示符下，Microsoft Teams命令安装应用生成器：

    ```cmd
    npm install generator-teams --global
    ```

以下是创建个人选项卡的步骤：

1. [使用个人选项卡生成应用程序](#generate-your-application-with-a-personal-tab)
1. [将内容页添加到个人选项卡](#add-a-content-page-to-the-personal-tab)
1. [创建应用包](#create-your-app-package)
1. [生成并运行应用程序](#build-and-run-your-application)
1. [建立到个人选项卡的安全隧道](#establish-a-secure-tunnel-to-your-tab)
1. [Upload应用程序以Teams](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>使用个人选项卡生成应用程序

1. 在命令提示符下，为个人选项卡创建新目录。

1. 在你的新目录中输入以下命令，以启动Microsoft Teams生成器：

    ```cmd
    yo teams
    ```

1. 向应用生成器提示的一系列问题Microsoft Teams更新 **manifest.json** 文件。

    :::image type="content" source="~/assets/images/tab-images/teamsTabScreenshot.PNG" alt-text="Teams生成器" border="true":::

    <details>
    <summary><b>更新 manifest.json 文件的一系列问题</b></summary>

    * **解决方案名称是什么？**

      解决方案名称是项目名称。 可以通过选择 Enter 接受建议 **的名称**。

    * **要将文件存放在哪里?**

      您当前在项目目录中。 选择 **Enter**。

    * **你的应用Microsoft Teams的标题？**

      标题是你的应用包名称，在应用清单和说明中使用。 输入标题或按 **Enter** 接受默认名称。

    * **你的 (公司) 名称？ (最多 32 个字符)**

      你的公司名称将在应用清单中使用。 输入公司名称或按 **Enter** 接受默认名称。

    * **要使用哪个清单版本？**

      选择默认架构。

    * **快速基架？ (Y/n)**

      默认值为 yes;输入 **n** 以输入你的 Microsoft 合作伙伴 ID。

    * **输入你的 Microsoft 合作伙伴 ID（如果有） (保留为空可跳过)**

      此字段不是必需的，并且必须仅在你已是 Microsoft 合作伙伴网络的一 [部分时使用](https://partner.microsoft.com)。

    * **要向项目添加哪些内容？**

      选择 **( &ast; ) 选项卡"**。

    * **将在其中托管此解决方案的 URL？**

      默认情况下，生成器建议 Azure 网站 URL。 你仅在本地测试应用，因此不需要有效的 URL。

    * **在应用/选项卡加载时是否显示加载指示器？**

      选择 **在** 应用或选项卡加载时不包括加载指示器。 默认值为"否"，输入 **n**。

    * **是否希望在无选项卡标题栏的情况下呈现个人应用?**

      选择 **不包括** 在没有选项卡标题栏的情况下呈现的个人应用。 默认值为"否"，输入 **n**。

    * **是否包含测试框架和初始测试？ (y/N)**

      选择 **不包括** 此项目的测试框架。 默认值为"否"，输入 **n**。

    * **是否包含 ESLint 支持？ (y/N)**

      选择不包括 ESLint 支持。 默认值为"否"，输入 **n**。

    * **是否希望将 Azure 应用程序Insights遥测？ (y/N)**

      选择 **不包括**[Azure 应用程序 Insights。](/azure/azure-monitor/app/app-insights-overview) 默认值为"否";输入 **n**。

    * **默认选项卡名称 (最多包含 16) ？**

      命名选项卡。此选项卡名称在整个项目中用作文件或 URL 路径组件。

    * **要创建哪种类型的选项卡？**

      使用箭头键选择个人 (**静态)**。

    * **是否需要Microsoft Azure Active Directory (Azure AD) 选项卡提供单一登录支持？**

      选择 **"** 不包括Azure AD"选项卡的"单一登录"支持。默认值为"是"，输入 **n**。

    </details>

### <a name="add-a-content-page-to-the-personal-tab"></a>将内容页添加到个人选项卡

创建内容页并更新个人选项卡应用程序的现有文件：

1. 使用以下 **personal.html** 在Visual Studio Code创建新的文件：

    ```html
    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="UTF-8">
            <title>
                <!-- Todo: add your a title here -->
            </title>
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <!-- inject:css -->
            <!-- endinject -->
        </head>
            <body>
                <h1>Personal Tab</h1>
                <p><img src="/assets/icon.png"></p>
                <p>This is your personal tab!</p>
            </body>
    </html>
    ```

1. 将 **personal.html** 保存在 **应用程序的公用文件夹中** 的以下位置：

    ```
    ./src/public/<yourDefaultTabNameTab>/personal.html
    ```

1. 从 **用户地址中的以下位置打开 manifest.json** Visual Studio Code：

    ```
     ./src/manifest/manifest.json
    ```

1. 将以下内容添加到空 `staticTabs` 数组 (`staticTabs":[]`) 并添加以下 JSON 对象：

    ```json
    {
        "entityId": "personalTab",
        "name": "Personal Tab ",
        "contentUrl": "https://{{PUBLIC_HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
        "websiteUrl": "https://{{PUBLIC_HOSTNAME}}",
        "scopes": ["personal"]
    }
    ```

    > [!IMPORTANT]
    > path 组件 **yourDefaultTabNameTab** 是在生成器中为 **"默认** 选项卡名称"加上单词 **"Tab**"输入的值。
    >
    > 例如：DefaultTabName 是 **MyTab** then **/MyTabTab/**

1. 使用实际 **选项卡** 名称 **更新 contentURL 路径组件 yourDefaultTabNameTab** 。

1. 保存更新后的 **manifest.json** 文件。

1. 从以下路径打开Visual Studio Code中的 **Tab.ts**，在 IFrame 中提供内容页面：

    ```bash
    ./src/server/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

1. 将以下内容添加到 IFrame 修饰符列表中：

    ```typescript
     @PreventIframe("/<yourDefaultTabName Tab>/personal.html")
    ```

1. 保存更新后的文件。 您的选项卡代码已完成。

### <a name="create-your-app-package"></a>创建应用包

你必须拥有一个应用包，以在 Teams 中生成和运行Teams。 应用包是通过 gulp 任务创建的，该任务验证 **manifest.json** 文件，并生成 **./package 目录中的** zip 文件夹。 在命令提示符处，输入以下命令：

```cmd
gulp manifest
```

### <a name="build-and-run-your-application"></a>生成并运行应用程序

#### <a name="build-your-application"></a>生成应用程序

在命令提示符下输入以下命令，将解决方案转换为 **./dist** 文件夹：

```cmd
gulp build
```

#### <a name="run-your-application"></a>运行应用程序

1. 在命令提示符下输入以下命令以启动本地 Web 服务器：

    ```cmd
    gulp serve
    ```

1. 在 `http://localhost:3007/<yourDefaultAppNameTab>/` 浏览器中输入 以查看应用程序的主页。

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="默认选项卡" border="true":::

1. 浏览 `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`，以查看你的个人选项卡。

    :::image type="content" source="~/assets/images/tab-images/personalTab.PNG" alt-text="默认 html 选项卡" border="true":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>建立到选项卡的安全隧道

在命令提示符处，退出 localhost 并输入以下命令以建立到选项卡的安全隧道：

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> 通过 **ngrok** 将选项卡上传到 Microsoft Teams并成功保存后，可以在 Teams 中查看它，直到隧道会话结束。

### <a name="upload-your-application-to-teams"></a>Upload应用程序以Teams

1. 转到"Microsoft Teams"**，然后选择"**&nbsp;应用商店 :::image type="content" source="~/assets/images/tab-images/store.png" alt-text="Teams应用商店&quot;":::。
1. 选择 **管理应用**
1. 选择 **"发布应用"****，Upload自定义应用"**。

    :::image type="content" source="~/assets/images/tab-images/publish-app.png" alt-text="Upload自定义应用" border="true":::

1. 转到项目目录，浏览到 **./package** 文件夹，选择 zip 文件夹，然后选择"打开 **"**。

    :::image type="content" source="~/assets/images/tab-images/addingpersonaltab.png" alt-text="添加个人选项卡" border="true":::

1. 选择 **弹出窗口** 中的"添加"。 您的选项卡将上载到Teams。

    :::image type="content" source="~/assets/images/tab-images/personaltabuploaded.png" alt-text="已上载&quot;个人&quot;选项卡" border="true":::

1. 在页面的Teams窗格中， &#x25CF;&#x25CF;&#x25CF; 省略号，然后选择已上传的应用以查看个人选项卡。

   现在，你已成功创建并添加了你的个人选项卡Teams。
  
   由于你的个人选项卡已Teams，因此还可以[`registerOnFocused`](#add-registeronfocused-api-for-tabs-or-personal-apps)为个人选项卡重新排序和[](#reorder-static-personal-tabs)添加 API。

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-personal-tab-with-aspnet-core"></a>创建具有"个人"选项卡 ASP.NET Core

1. 在命令提示符下，为选项卡项目创建新目录。

1. 使用下面的命令将示例存储库克隆到新目录中，也可以下载 [源代码](https://github.com/OfficeDev/Microsoft-Teams-Samples) 并解压缩文件：

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

以下是创建个人选项卡的步骤：

1. [使用个人选项卡生成应用程序](#generate-your-application-with-a-personal-tab-1)
1. [更新并运行应用程序](#update-and-run-your-application)
1. [建立到选项卡的安全隧道](#establish-a-secure-tunnel-to-your-tab-1)
1. [使用开发人员门户更新应用包](#update-your-app-package-with-developer-portal)
1. [在应用中预览Teams](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>使用个人选项卡生成应用程序

1. 打开Visual Studio并选择"**打开项目或解决方案"**。

1. 转到 **Microsoft-Teams-Samplessamplestab-personal** >  >  > **一or-csharp** 文件夹，然后打开 **PersonalTab.sln**。

1. In Visual Studio， select **F5** or choose **Start Debugging** from your application's **Debug** menu to verify if the application has loaded properly. 在浏览器中，转到以下 URL：

    * <http://localhost:3978/>
    * <http://localhost:3978/personalTab>
    * <http://localhost:3978/privacy>
    * <http://localhost:3978/tou>

<details>
<summary><b>查看源代码</b></summary>

#### <a name="startupcs"></a>Startup.cs

此项目从 3.1 ASP.NET Core Web 应用程序空模板创建，在设置时选中了"高级 **- 配置 HTTPS**"复选框。 MVC 服务由依赖关系注入框架的方法注册 `ConfigureServices()` 。 此外，默认情况下，空 `Configure()` 模板不支持为静态内容提供服务，因此，将静态文件中间件添加到 以下代码的方法中：

```csharp
public void ConfigureServices(IServiceCollection services)
  {
      services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
  }
public void Configure(IApplicationBuilder app)
  {
    app.UseStaticFiles();
    app.UseMvc();
  }
```

#### <a name="wwwroot-folder"></a>wwwroot 文件夹

在 ASP.NET Core中，Web 根文件夹是应用程序查找静态文件的位置。

#### <a name="indexcshtml"></a>Index.cshtml

ASP.NET Core将名为 **Index** 的文件视为网站的默认页面或主页。 当浏览器 URL 指向网站的根目录时， **Index.cshtml** 将显示为应用程序的主页。

#### <a name="appmanifest-folder"></a>AppManifest 文件夹

此文件夹包含以下所需的应用包文件：

* 全 **色图标** ，大小为 192 x 192 像素。
* 一 **个** 32 x 32 像素的透明边框图标。
* **一个 manifest.json** 文件，用于指定应用的属性。

必须将这些文件压缩到应用包中，以用于将选项卡上载到Teams。 Microsoft Teams清单`contentUrl`中指定的 ，将其嵌入 <iframe\>，并将其呈现在选项卡中。

#### <a name="csproj"></a>.csproj

In Visual Studio 解决方案资源管理器， right-click on the project and select **Edit Project File**. 在文件末尾，可以看到以下代码，可在应用程序生成时创建和更新 zip 文件夹：

```xml
<PropertyGroup>
    <PostBuildEvent>powershell.exe Compress-Archive -Path \"$(ProjectDir)AppManifest\*\" -DestinationPath \"$(TargetDir)tab.zip\" -Force</PostBuildEvent>
  </PropertyGroup>

  <ItemGroup>
    <EmbeddedResource Include="AppManifest\icon-outline.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\icon-color.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\manifest.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
  </ItemGroup>
```

</details>

### <a name="update-and-run-your-application"></a>更新并运行应用程序

1. 转到 **PagesShared**  >  文件夹并打开 **_Layout.cshtml**，然后向标记部分添加`<head>`以下内容：

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

1. 打开 **"页面"文件夹中的 PersonalTab.cshtml**，然后`microsoftTeams.initialize()`添加标记`<script>`并保存。

1. In Visual Studio， select **F5** or choose **Start Debugging** from your application's **Debug** menu.

### <a name="establish-a-secure-tunnel-to-your-tab"></a>建立到选项卡的安全隧道

在项目目录根目录的命令提示符下，运行以下命令以建立到选项卡的安全隧道：

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>使用开发人员门户更新应用包

1. 转到 **Teams 中的** 开发人员门户。

1. 打开 **"应用** "，然后选择 **"导入应用"**。

1. 应用包的名称 **tab.zip。** 它可在以下路径中使用：

    ```
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. 选择 **tab.zip** ，在开发人员门户中打开它。

1. 在" **基本信息** "部分创建并填充默认 **应用 ID** 。

1. 在"说明"中添加应用的 **简短和详细说明**。

1. 在 **"开发人员信息**"中，添加所需详细信息，在"网站 (必须是有效的 **HTTPS URL** ，) 您的 ngrok HTTPS URL。

1. 在 **"应用 URL"** 中，将隐私策略 `https://<yourngrokurl>/privacy` 更新为 ，将使用条款更新为 `https://<yourngrokurl>/tou` 并保存。

1. 在 **"应用功能**"中，选择"个人应用"，然后输入"名称"，然后 **使用 更新内容 URL**`https://<yourngrokurl>/personalTab`。 将"网站 URL"字段留空。

1. 选择“**保存**”。

1. 在"域"部分，选项卡中的域必须包含不带 HTTPS 前缀的 ngrok URL `<yourngrokurl>.ngrok.io`。

### <a name="preview-your-app-in-teams"></a>在应用中预览Teams

1. 从 **开发人员门户Teams** 中选择"预览"。 开发人员门户会通知你你的应用已成功旁加载。

1. 选择 **"管理应用"**。 你的应用在旁加载的应用中列出。

1. 使用搜索查找你的应用，选择其行中的三个点。

1. 选择" **视图"** 选项。 **将显示应用的**"添加"页面。

1. 选择 **"添加**"以加载选项卡Teams。 您的选项卡现已在 Teams 中提供。

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetuploaded.png" alt-text="默认选项卡" border="true":::

   现在，你已成功创建并添加了你的个人选项卡Teams。
  
   由于你的个人选项卡已Teams，因此还可以[`registerOnFocused`](#add-registeronfocused-api-for-tabs-or-personal-apps)为个人选项卡重新排序和[](#reorder-static-personal-tabs)添加 API。

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-personal-tab-with-aspnet-core-mvc"></a>使用 MVC 创建 ASP.NET Core选项卡

1. 在命令提示符下，为选项卡项目创建新目录。

1. 使用下面的命令将示例存储库克隆到新目录中，也可以下载 [源代码](https://github.com/OfficeDev/Microsoft-Teams-Samples) 并解压缩文件：

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

以下是创建个人选项卡的步骤：

1. [使用个人选项卡生成应用程序](#generate-your-application-with-a-personal-tab-2)
1. [更新并运行应用程序](#update-and-run-your-application-1)
1. [建立到选项卡的安全隧道](#establish-a-secure-tunnel-to-your-tab-2)
1. [使用开发人员门户更新应用包](#update-your-app-package-with-developer-portal-1)
1. [在应用中预览Teams](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-personal-tab"></a>使用个人选项卡生成应用程序

1. 打开Visual Studio并选择"**打开项目或解决方案"**。

1. Go to Microsoft-Teams-Samplessamplestab-personalmvc-csharp  >  >  >  folder and open **PersonalTabMVC.sln** in Visual Studio.

1. In Visual Studio， select **F5** or choose **Start Debugging** from your application's **Debug** menu to verify if the application has loaded properly. 在浏览器中，转到以下 URL：

    * <http://localhost:3978>
    * <http://localhost:3978/personalTab>
    * <http://localhost:3978/privacy>
    * <http://localhost:3978/tou>

<details>
<summary><b>查看源代码</b></summary>

#### <a name="startupcs"></a>Startup.cs

此项目从 3.1 ASP.NET Core Web 应用程序空模板创建，在设置时选中了"高级 **- 配置 HTTPS**"复选框。 MVC 服务由依赖关系注入框架的方法注册 `ConfigureServices()` 。 此外，默认情况下，空 `Configure()` 模板不支持为静态内容提供服务，因此，将静态文件中间件添加到 以下代码的方法中：

``` csharp
public void ConfigureServices(IServiceCollection services)
  {
    services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
  }
public void Configure(IApplicationBuilder app)
  {
    app.UseStaticFiles();
    app.UseMvc();
  }
```

#### <a name="wwwroot-folder"></a>wwwroot 文件夹

在 ASP.NET Core中，Web 根文件夹是应用程序查找静态文件的位置。

#### <a name="appmanifest-folder"></a>AppManifest 文件夹

此文件夹包含以下所需的应用包文件：

* 全 **色图标** ，大小为 192 x 192 像素。
* 一 **个** 32 x 32 像素的透明边框图标。
* **一个 manifest.json** 文件，用于指定应用的属性。

必须将这些文件压缩到应用包中，以用于将选项卡上载到Teams。 Microsoft Teams清单`contentUrl`中指定的内容，将其嵌入 IFrame 中，并将其呈现在选项卡中。

#### <a name="csproj"></a>.csproj

在Visual Studio 解决方案资源管理器中，右键单击项目并选择"编辑Project **文件"**。 在文件末尾，你将看到以下代码，该代码在应用程序生成时创建和更新 zip 文件夹：

``` xml
<PropertyGroup>
    <PostBuildEvent>powershell.exe Compress-Archive -Path \"$(ProjectDir)AppManifest\*\" -DestinationPath \"$(TargetDir)tab.zip\" -Force</PostBuildEvent>
  </PropertyGroup>

  <ItemGroup>
    <EmbeddedResource Include="AppManifest\icon-outline.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\icon-color.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\manifest.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
  </ItemGroup>
```

#### <a name="models"></a>模型

**PersonalTab.cs** 提供在用户选择 **PersonalTab** 视图中的按钮时从 **PersonalTabController** 调用的邮件对象和方法。

#### <a name="views"></a>视图

这些视图是 MVC 中 ASP.NET Core视图：

* 主页：ASP.NET Core将名为 **Index** 的文件视为网站的默认页面或主页。 当浏览器 URL 指向网站的根目录时， **Index.cshtml** 将显示为应用程序的主页。

* Shared：部分视图标记 **_Layout.cshtml** 包含应用程序的整体页面结构和共享的可视元素。 它还引用Teams库。

#### <a name="controllers"></a>控制器

控制器使用 属性 `ViewBag` 将值动态传输给 Views。

</details>

### <a name="update-and-run-your-application"></a>更新并运行应用程序

1. 转到 **ViewsShared**  >  文件夹并打开 **_Layout.cshtml**，然后向标记部分添加`<head>`以下内容：

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

1. 从 **ViewsPersonalTab** 文件夹中打开 **PersonalTab.cshtml** > ，并添加`microsoftTeams.initialize()`在`<script>`标记内并保存。

1. In Visual Studio， select **F5** or choose **Start Debugging** from your application's **Debug** menu.

### <a name="establish-a-secure-tunnel-to-your-tab"></a>建立到选项卡的安全隧道

在项目目录根目录的命令提示符下，运行以下命令以建立到选项卡的安全隧道：

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>使用开发人员门户更新应用包

1. 转到 **Teams 中的** 开发人员门户。

1. 打开 **"应用** "，然后选择 **"导入应用"**。

1. 应用包的名称 **tab.zip。** 它可在以下路径中使用：

    ```
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. 选择 **tab.zip** ，在开发人员门户中打开它。

1. 在" **基本信息** "部分创建并填充默认 **应用 ID** 。

1. 在"说明"中添加应用的 **简短和详细说明**。

1. 在 **"开发人员信息**"中，添加所需详细信息，在"网站 (必须是有效的 **HTTPS URL** ，) 您的 ngrok HTTPS URL。

1. 在 **"应用 URL"** 中，将隐私策略 `https://<yourngrokurl>/privacy` 更新为 ，将使用条款更新为 `https://<yourngrokurl>/tou` 并保存。

1. 在 **"应用功能**"中，选择"个人应用"，然后输入"名称"，然后 **使用 更新内容 URL**`https://<yourngrokurl>/personalTab`。 将"网站 URL"字段留空。

1. 选择“**保存**”。

1. 在"域"部分，选项卡中的"域"必须包含不带 HTTPS 前缀的 ngrok URL `<yourngrokurl>.ngrok.io`。

### <a name="preview-your-app-in-teams"></a>在应用中预览Teams

1. 从 **开发人员门户Teams** 中选择"预览"。 开发人员门户会通知你你的应用已成功旁加载。

1. 选择 **"管理应用"**。 你的应用在旁加载的应用中列出。

1. 使用搜索查找你的应用，选择其行中的三个点。

1. 选择 **"查看"** 选项。 **将显示应用的**"添加"页面。

1. 选择 **"添加**"以加载选项卡Teams。 您的选项卡现已在 Teams 中提供。

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetmvccoreuploaded.png" alt-text="个人选项卡" border="true":::
  
   现在，你已成功创建并添加了你的个人选项卡Teams。

   由于你的个人选项卡已Teams，因此还可以[`registerOnFocused`](#add-registeronfocused-api-for-tabs-or-personal-apps)为个人选项卡重新排序和[](#reorder-static-personal-tabs)添加 API。

::: zone-end

## <a name="reorder-static-personal-tabs"></a>对静态个人选项卡重新排序

从清单版本 1.7 开始，开发人员可以重新排列其个人应用的所有选项卡。 特别是，开发人员可以移动自动程序聊天选项卡，该选项卡始终默认位于个人应用选项卡标题中的任意位置。 声明了`entityId`两个保留的选项卡关键字 **，即对话和****关于**。

如果你创建具有个人范围的自动程序，它将默认出现在个人应用的第一个选项卡位置。 如果要将其移动到其他位置，则必须使用保留的关键字"对话"将静态选项卡对象添加到 **清单** 中。 对话 **选项卡** 显示在 Web 或桌面上，具体取决于在数组中添加对话选项卡`staticTabs`的什么位置。

``` JSON

{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}

```

## <a name="add-registeronfocused-api-for-tabs-or-personal-apps"></a>为 `registerOnFocused` 选项卡或个人应用添加 API

SDK `registerOnFocused` API 允许你在键盘上Teams。 借助 Ctrl、Shift 和 F6 键，你可以返回到个人应用并保持对选项卡或个人应用的焦点。 例如，你可以离开个人应用来搜索某些内容，然后返回到个人应用或使用 Ctrl+F6 在所需位置四处移动。

以下代码提供了 SDK 上的处理程序定义 `registerFocusEnterHandler` 示例，当焦点必须返回到选项卡或个人应用时：

``` C#

export function registerFocusEnterHandler(handler: (navigateForward: boolean) => void): 
void {
  HandlersPrivate.focusEnterHandler = handler;
  handler && sendMessageToParent('registerHandler', ['focusEnter']);
}
function handleFocusEnter(navigateForward: boolean): void
 {
  if (HandlersPrivate.focusEnterHandler)
   {
    HandlersPrivate.focusEnterHandler(navigateForward);
  }
}

```

After the handler is triggered with the keyword `focusEnter`， the handler `registerFocusEnterHandler` is invoked with a callback function `focusEnterHandler` that takes in a parameter called `navigateForward`. 的值 `navigateForward` 确定事件的类型。 仅 `focusEnterHandler` 由 Ctrl+F6 调用，而不是由 Tab 键调用。
键可用于移动事件Teams如下所示：

* Forward 事件：Ctrl+F6 键
* Backward 事件：Ctrl+Shift+F6 键

``` C#

case 'focusEnter':     
this.registerFocusEnterHandler((navigateForward: boolean = true) => {
this.sdkWindowMessageHandler.sendRequestMessage(this.frame, this.constants.SdkMessageTypes.focusEnter, [navigateForward]);
// Set focus on iframe or webview
if (this.frame && this.frame.sourceElem) {
  this.frame.sourceElem.focus();
}
return true;
});
}

// callback function to be passed to the handler
private focusEnterHandler: (navigateForward: boolean) => boolean;

// function that gets invoked after handler is registered.
private registerFocusEnterHandler(focusEnterHandler: (navigateForward: boolean) => boolean): void {
this.focusEnterHandler = focusEnterHandler;
this.layoutService.registerAppFocusEnterCallback(this.focusEnterHandler);
}

```

### <a name="personal-app"></a>个人应用

:::image type="content" source="../../assets/images/personal-apps/registerfocus.png" alt-text="示例显示用于添加 registerOnFocussed API 的选项" border="true":::

#### <a name="personal-app-forward-event"></a>个人应用：转发事件

:::image type="content" source="../../assets/images/personal-apps/registerfocus-forward-event.png" alt-text="示例显示用于添加 registerOnFocussed API 向前移动的选项" border="true":::

#### <a name="personal-app-backward-event"></a>个人应用：向后事件

:::image type="content" source="../../assets/images/personal-apps/registerfocus-backward-event.png" alt-text="示例显示用于添加 registerOnFocussed API 向后移动的选项" border="true":::

### <a name="tab"></a>选项卡

:::image type="content" source="../../assets/images/personal-apps/registerfocus-tab.png" alt-text="示例显示用于为选项卡添加 registerOnFocussed API 的选项" border="true":::

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [创建频道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>另请参阅

* [Teams选项卡](~/tabs/what-are-tabs.md)
* [移动设备上的选项卡](~/tabs/design/tabs-mobile.md)
* [具有自适应卡片的生成选项卡](~/tabs/how-to/build-adaptive-card-tabs.md)
* [创建对话选项卡](~/tabs/how-to/conversational-tabs.md)
