---
title: 创建个人选项卡
author: laujan
description: 了解如何构建个人选项卡。选择Node.js、ASP.NET Core或 ASP.NET Core MVC 环境。 生成应用、添加内容、创建包、生成和运行应用。
ms.localizationpriority: high
ms.topic: quickstart
ms.author: lajanuar
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: 5afb145bdba5639b71a7b56ac8884dc465127d35
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2022
ms.locfileid: "68820001"
---
# <a name="create-a-personal-tab"></a>创建个人选项卡

个人选项卡和个人范围的机器人一样，是个人应用的一部分，只作用于一个用户。 可以将它们固定到左侧窗格以方便访问。 还可以将个人选项卡 [ 重新排序 ](#reorder-static-personal-tabs)。

确保具备构建个人选项卡的所有“[先决条件](~/tabs/how-to/tab-requirements.md)”。

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

::: zone pivot="node-java-script"

## <a name="create-a-personal-tab-with-nodejs"></a>使用 Node.js 创建个人选项卡

1. 在命令提示符下，安装 Node.js 后，输入以下命令安装 [Yeoman](https://yeoman.io/) and [gulp-cli](https://www.npmjs.com/package/gulp-cli) 包：

    ```cmd
    npm install yo gulp-cli --global
    ```

1. 在命令提示符下，通过输入以下命令安装 Microsoft Teams 应用生成器：

    ```cmd
    npm install generator-teams --global
    ```

以下是创建个人选项卡的步骤：

1. [ 使用个人选项卡生成应用程序 ](#generate-your-application-with-a-personal-tab)
1. [ 将内容页添加到个人选项卡 ](#add-a-content-page-to-the-personal-tab)
1. [创建应用包](#create-your-app-package)
1. [ 构建并运行应用程序 ](#build-and-run-your-application)
1. [ 建立到个人选项卡的安全隧道 ](#establish-a-secure-tunnel-to-your-tab)
1. [ 将应用程序上传到 Teams ](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>使用个人选项卡生成应用程序

1. 在命令提示符下，为个人选项卡创建新目录。

1. 在新目录中输入以下命令以启动 Microsoft Teams 应用生成器：

    ```cmd
    yo teams
    ```

1. 向 Microsoft Teams 应用生成器提示的一系列问题提供值以更新文件 `manifest.json` 。

    :::image type="content" source="~/assets/images/tab-images/teamsTabScreenshot.PNG" alt-text=" Teams生成器 ":::

    <details>
    <summary><b> 更新 manifest.json 文件的一系列问题 </b></summary>

    * **解决方案名称是什么？**

      解决方案名称是项目名称。 可以通过选择“**Enter**”接受建议的名称。

    * **要将文件存放在哪里?**

      当前位于项目目录中。 选择“**Enter**”。

    * **Microsoft Teams 应用项目的标题是什么?**

      标题是应用包名称，在应用清单和说明中使用。 输入标题或选择“**Enter**”以接受默认名称。

    * **你的 (公司) 名称是什么? (最多 32 个字符)**

      你的公司名称将用于应用清单。 输入公司名称或选择“**Enter**”以接受默认名称。

    * **要使用哪个清单版本?**

      选择默认架构。

    * **快速基架? (Y/n)**

      默认值为 yes;输入“**n**”以输入 Microsoft 合作伙伴 ID。

    * **如果有 Microsoft 合作伙伴 ID，请输入: (留空跳过)**

      此字段不是必需的，仅当你已是 [Microsoft 合作伙伴网络](https://partner.microsoft.com)的一部分时才必须使用。

    * **要向项目添加哪些内容?**

      选择 **( &ast; ) 选项卡**。

    * **要托管此解决方案的 URL 是什么?**

      默认情况下，生成器会建议 Azure 网站 URL。 仅在本地测试应用，因此不需要有效的 URL。

    * **加载应用/选项卡时，是否希望显示加载指示器?**

      加载应用或选项卡时，选择“**NOT**”以包含加载指示器。 默认值为“否”，输入“**n**”。

    * **是否希望在无选项卡标题栏的情况下呈现个人应用?**

      选择“**NOT**”以包含没有选项卡标题栏的情况下要呈现的个人应用。 默认值为否，输入“**n**”。

    * **是否希望包含测试框架和初始测试? (y/N)**

      选择“**NOT**”以包含此项目的测试框架。 默认值为“否”，输入“**n**”。

    * **是否要包括 ESLint 支持? (y/N)**

      选择不包含 ESLint 支持。 默认值为“否”，输入“**n**”。

    * **是否希望将 Azure 应用程序见解用于遥测? (y/N)**

      选择“**NOT**”以包含 [Azure 应用程序见解](/azure/azure-monitor/app/app-insights-overview)。 默认值为否;输入“**n**”。

    * **默认选项卡名称是什么 (最多 16 个字符)?**

      为选项卡命名。此选项卡名称在整个项目中用作文件或 URL 路径组件。

    * **要创建哪种类型的选项卡？**

      使用箭头键选择 **个人（静态）**。

    * **是否需要 Microsoft Azure Active Directory (Azure AD) 对该选项卡的单点登录支持？**

      选择 **不要** 包含对该选项卡的 Azure AD 单点登录支持。默认值为“是”，输入 **n**。
    > [!NOTE]
    > 在选项卡中，仅当用户选择“后退”按钮 (或移出选项卡) 并返回到主页时，选项卡主页才会显示。 根据设计，选项卡不会保留或保留以前的状态。
    </details>

### <a name="add-a-content-page-to-the-personal-tab"></a>将内容页添加到个人选项卡

创建内容页并更新个人选项卡应用程序的现有文件：

1. 使用以下标记在 Visual Studio Code 中创建一个新的 **personal.html** 文件：

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

1. 将 **personal.html** 保存在应用程序 **公用** 文件夹中的以下位置：

    ```
    ./src/public/<yourDefaultTabNameTab>/personal.html
    ```

1. 从 Visual Studio Code 中的以下位置打开`manifest.json`：

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
    > 路径组件 **yourDefaultTabNameTab** 是在 **默认选项卡名称** 的生成器中输入的值以及 **Tab** 一词。
    >
    > 例如：DefaultTabName 为 **MyTab**，然后为 **/MyTabTab/**

1. 使用实际的选项卡名称更新 **contentURL** 路径组件 **yourDefaultTabNameTab**。

1. 保存更新的 `manifest.json` 文件。

1. 从以下路径打开 Visual Studio Code中的 **Tab.ts**，以在 iFrame 中提供内容页：

    ```bash
    ./src/server/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

1. 将以下内容添加到 iFrame 修饰器列表：

    ```typescript
     @PreventIframe("/<yourDefaultTabName Tab>/personal.html")
    ```

1. 保存更新的文件。 选项卡代码已经完成。

### <a name="create-your-app-package"></a>创建应用包

必须有一个应用包才能在 Teams 中生成和运行应用程序。 应用包是通过验证 `manifest.json` 文件并在 `./package` 目录中生成压缩文件夹的 gulp 任务创建的。 在命令提示符处，使用命令 `gulp manifest`。

### <a name="build-and-run-your-application"></a>构建并运行应用程序

#### <a name="build-your-application"></a>构建应用程序

在命令提示符处输入以下命令，将解决方案转译到 **./dist** 文件夹中：

```cmd
gulp build
```

#### <a name="run-your-application"></a>运行应用程序

1. 在命令提示符下，输入以下命令以启动本地 Web 服务器：

    ```cmd
    gulp serve
    ```

1. 在浏览器中输入 `http://localhost:3007/<yourDefaultAppNameTab>/` 以查看应用程序主页。

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text=" 默认选项卡 ":::

1. 浏览 `http://localhost:3007/<yourDefaultAppNameTab>/personal.html` 以查看个人选项卡。

    :::image type="content" source="~/assets/images/tab-images/personalTab.PNG" alt-text=" 默认 html 选项卡 ":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>建立到选项卡的安全隧道

在命令提示符处，退出 localhost 并输入以下命令，以建立到选项卡的安全隧道：

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> 通过 **ngrok** 将选项卡上传到 Microsoft Teams 并成功保存后，可以在 Teams 中查看它，直到隧道会话结束。

### <a name="upload-your-application-to-teams"></a>将应用程序上传到 Teams

1. 转到 Teams 并选择 **应用**&nbsp;:::image type="content" source="~/assets/images/tab-images/store.png" alt-text="Teams Store":::。
1. 选择“ **管理应用** > **”“上传应用** > **上传自定义应用**”。
1. 转到项目目录，浏览到 **./package** 文件夹，选择压缩文件夹，然后选择“**打开**”。

    :::image type="content" source="~/assets/images/tab-images/addingpersonaltab.png" alt-text=" 添加个人选项卡 ":::

1. 在对话框中选择“**添加**”。 选项卡已上传到 Teams。

    :::image type="content" source="~/assets/images/tab-images/personaltabuploaded.png" alt-text=" 上传的个人选项卡 ":::

1. 在 Teams 的左窗格中，选择省略号 &#x25CF;&#x25CF;&#x25CF；然后选择上传的应用以查看个人选项卡。

   现在，你已成功在 Teams 中创建并添加了个人选项卡。
  
   Teams 中含有个人选项卡时，还可以将个人选项卡 [ 重新排序 ](#reorder-static-personal-tabs)。

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-personal-tab-with-aspnet-core"></a>使用 ASP.NET Core 创建个人选项卡

1. 在命令提示符处，为选项卡项目创建新目录。

1. 使用以下命令将示例存储库克隆到新目录中，也可以下载 [ 源代码 ](https://github.com/OfficeDev/Microsoft-Teams-Samples) 并提取文件：

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

以下是创建个人选项卡的步骤：

1. [ 使用个人选项卡生成应用程序 ](#generate-your-application-with-a-personal-tab-1)
1. [ 更新并运行应用程序 ](#update-and-run-your-application)
1. [ 建立到选项卡的安全隧道 ](#establish-a-secure-tunnel-to-your-tab-1)
1. [ 使用开发人员门户更新应用包 ](#update-your-app-package-with-developer-portal)
1. [ 在 Teams 中预览应用 ](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>使用个人选项卡生成应用程序

1. 打开 Visual Studio，然后选择“**打开项目或解决方案**”。

1. 转到 **Microsoft-Teams-Samples** > **samples** > **tab-personal** > **razor-csharp** 文件夹并打开 **PersonalTab.sln**。

1. 在 Visual Studio 中，选择 **F5** 或从应用程序的“**调试**”菜单中选择“**开始调试**”，以验证应用程序是否已正确加载。 在浏览器中，转到以下 URL：

    * `<http://localhost:3978/>`
    * `<http://localhost:3978/personalTab>`
    * `<http://localhost:3978/privacy>`
    * `<http://localhost:3978/tou>`

<details>
<summary><b>查看源代码</b></summary>

#### <a name="startupcs"></a>Startup.cs

此项目是从 ASP.NET Core 3.1 Web 应用程序空模板创建的，在设置时选中了“**高级 - 配置 HTTPS**”复选框。 MVC 服务通过依赖注入框架 `ConfigureServices()` 的方法注册。 此外，默认情况下，空模板不支持提供静态内容，因此使用以下代码将静态文件中间件添加到 `Configure()` 方法：

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

在 ASP.NET Core 中，Web 根文件夹是应用程序查找静态文件的位置。

#### <a name="indexcshtml"></a>Index.cshtml

ASP.NET Core 将名为“**索引**”的文件视为网站的默认或主页。 当浏览器 URL 指向站点的根目录时， **Index.cshtml** 将显示为应用程序的主页。

#### <a name="appmanifest-folder"></a>AppManifest 文件夹

此文件夹包含以下必需的应用包文件：

* 一个全色图标，尺寸为 192 x 192 像素。
* 一个透明轮廓图标，尺寸为 32 x 32 像素。
* 一个 `manifest.json` 指定应用属性的文件。

这些文件必须压缩在应用包中，以便将选项卡上传到 Teams。 Teams 会加载清单中指定的 `contentUrl`，将其嵌入 <iframe\> 中，并在选项卡中呈现。

#### <a name="csproj"></a>.csproj

在 Visual Studio 解决方案资源管理器中，右键单击项目，然后选择“**编辑项目文件**”。 在文件末尾，可以看到以下代码，用于在应用程序构建时创建和更新压缩文件夹：

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

1. 打开 Visual Studio 解决方案资源管理器，转到“**共享** > **页面**”文件夹，打开 **_Layout.cshtml** 并将以下内容添加到 `<head>` 标记部分：

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js" integrity="sha384-QtTBFeFlfRDZBfwHJHYQp7MdLJ2C3sfAEB1Qpy+YblvjavBye+q87TELpTnvlXw4" crossorigin="anonymous"></script>
    ```

1. 在 Visual Studio გადაწყვეტების მნახველი中，从 **Pages** 文件夹打开 **PersonalTab.cshtml** 并添加`microsoftTeams.app.initialize()``<script>`标记。

1. 选择“**保存**”。

1. 在 Visual Studio 中，选择 **F5** 或从应用程序的“**调试**”菜单中选择“**开始调试**”。

### <a name="establish-a-secure-tunnel-to-your-tab"></a>建立到选项卡的安全隧道

在项目目录根目录中的命令提示符下，运行以下命令，建立到选项卡的安全隧道：

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>使用“开发人员门户”更新应用包

1. 转到“[**开发人员门户**](https://dev.teams.microsoft.com/home)”。

1. 打开“**应用**”并选择“**导入引用**”。

1. 应用包文件名为 `tab.zip` ，且在路径中 `/bin/Debug/netcoreapp3.1/tab.zip` 可用。

1. 在“开发人员门户”中选择 `tab.zip` 并将其打开。

1. 在“**基本信息**”部分创建并填充默认 **应用 ID**。

1. 在“**说明**”中添加应用的短说明和长说明。

1. 在“**开发人员信息**”中，添加所需详细信息，并在 **网站 (必须是有效的 HTTPS URL)** 中提供 ngrok HTTPS URL。

1. 在 **“应用 URL**”中，将“隐私策略”更新为 `https://<yourngrokurl>/privacy` `https://<yourngrokurl>/tou` 和“使用条款”，然后选择“ **保存**”。

1. 在 **“应用功能**”中，选择“**个人应用** > **”“创建你的第一个个人应用”选项卡**，然后输入名称并使用 更新 **内容 URL**`https://<yourngrokurl>/personalTab`。 将“网站 URL”字段留空，从下拉列表中选择“ **上下文** ”作为“个人选项卡”，然后选择“ **确认**”。

1. 选择“保存”。

1. 在“域”部分中，选项卡中的域必须包含没有 HTTPS 前缀 `<yourngrokurl>.ngrok.io` 的 ngrok URL。

### <a name="preview-your-app-in-teams"></a>在 Teams 中预览应用

1. 在开发人员门户工具栏中选择“**在 Teams 中预览**”，开发人员门户会通知你应用已成功旁加载。 应用的“**添加**”页将显示在 Teams 中。

1. 选择“**添加**”以加载 Teams 中的选项卡。 选项卡此时在 Teams 中可用。

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetuploaded.png" alt-text=" 默认选项卡 ":::

   现在，你已成功在 Teams 中创建并添加了个人选项卡。
  
   Teams 中含有个人选项卡时，还可以将个人选项卡 [ 重新排序 ](#reorder-static-personal-tabs)。

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-personal-tab-with-aspnet-core-mvc"></a>使用 ASP.NET Core MVC 创建个人选项卡

1. 在命令提示符处，为选项卡项目创建新目录。

1. 使用以下命令将示例存储库克隆到新目录中，也可以下载 [ 源代码 ](https://github.com/OfficeDev/Microsoft-Teams-Samples) 并提取文件：

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

以下是创建个人选项卡的步骤：

1. [ 使用个人选项卡生成应用程序 ](#generate-your-application-with-a-personal-tab-2)
1. [ 更新和运行应用程序 ](#update-and-run-your-application-1)
1. [ 建立到选项卡的安全隧道 ](#establish-a-secure-tunnel-to-your-tab-2)
1. [ 使用开发人员门户更新应用包 ](#update-your-app-package-with-developer-portal-1)
1. [ 在 Teams 中预览应用 ](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-personal-tab"></a>使用个人选项卡生成应用程序

1. 打开 Visual Studio，然后选择“**打开项目或解决方案**”。

1. 转到 **Microsoft-Teams-Samples** > **samples** > **tab-personal** > **mvc-csharp** 文件夹，并在 Visual Studio 中打开 **PersonalTabMVC.sln**。

1. 在 Visual Studio 中，选择 **F5** 或从应用程序的“**调试**”菜单中选择“**开始调试**”，以验证应用程序是否已正确加载。 在浏览器中，转到以下 URL：

    * `<http://localhost:3978>`
    * `<http://localhost:3978/personalTab>`
    * `<http://localhost:3978/privacy>`
    * `<http://localhost:3978/tou>`

<details>
<summary><b>查看源代码</b></summary>

#### <a name="startupcs"></a>Startup.cs

此项目是从 ASP.NET Core 3.1 Web 应用程序空模板创建的，在设置时选中了“**高级 - 配置 HTTPS**”复选框。 MVC 服务通过依赖注入框架 `ConfigureServices()` 的方法注册。 此外，默认情况下，空模板不支持提供静态内容，因此使用以下代码将静态文件中间件添加到 `Configure()` 方法：

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

在 ASP.NET Core 中，Web 根文件夹是应用程序查找静态文件的位置。

#### <a name="appmanifest-folder"></a>AppManifest 文件夹

此文件夹包含以下必需的应用包文件：

* 一个 **全色图标**，尺寸为 192 x 192 像素。
* 一个 **透明轮廓图标**，尺寸为 32 x 32 像素。
* 一个 `manifest.json` 指定应用属性的文件。

这些文件必须压缩在应用包中，以便将选项卡上传到 Teams。 Teams 加载 `contentUrl` 清单中指定的 ，将其嵌入 iFrame 中，并将其呈现在选项卡中。

#### <a name="csproj"></a>.csproj

在 Visual Studio 解决方案资源管理器中，右键单击项目，然后选择“**编辑项目文件**”。 在文件末尾，会看到以下代码，用于在应用程序构建时创建和更新压缩文件夹：

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

当用户在 **PersonalTab** 视图中选择按钮时，**PersonalTab.cs** 会显示从 **PersonalTabController** 调用的消息对象和方法。

#### <a name="views"></a>视图

这些视图是 ASP.NET Core MVC 中的不同视图：

* 主页：ASP.NET Core 将名为“**索引**”的文件视为网站的默认或主页。 当浏览器 URL 指向站点的根目录时， **Index.cshtml** 将显示为应用程序的主页。

* 共享：部分视图标记 **_Layout.cshtml** 包含应用程序的整体页面结构和共享的视觉元素。 它还引用 Teams 库。

#### <a name="controllers"></a>控制器

控制器使用该 `ViewBag` 属性动态地将值传输到“视图”。

</details>

### <a name="update-and-run-your-application"></a>更新并运行应用程序

1. 打开 Visual Studio 解决方案资源管理器，转到 “**视图**” > “**共享**”文件夹，打开 **_Layout.cshtml**，并将以下内容添加到 `<head>` 标记部分：

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js" integrity="sha384-QtTBFeFlfRDZBfwHJHYQp7MdLJ2C3sfAEB1Qpy+YblvjavBye+q87TELpTnvlXw4" crossorigin="anonymous"></script>
    ```

1. 在 Visual Studio გადაწყვეტების მნახველი中，从 **Views** >  **PersonalTab 文件夹打开 PersonalTab.cshtml**，并在`microsoftTeams.app.initialize()`标记中添加 。`<script>`

1. 选择“**保存**”。

1. 在 Visual Studio 中，选择 **F5** 或从应用程序的“**调试**”菜单中选择“**开始调试**”。

### <a name="establish-a-secure-tunnel-to-your-tab"></a>建立到选项卡的安全隧道

在项目目录根目录中的命令提示符下，运行以下命令，建立到选项卡的安全隧道：

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>使用“开发人员门户”更新应用包

1. 转到“[**开发人员门户**](https://dev.teams.microsoft.com/home)”。

1. 打开“**应用**”并选择“**导入引用**”。

1. 应用包的名称是 **tab.zip**。 它可在以下路径中使用：

    ```
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. 选择 **tab.zip** 并在开发人员门户中将其打开。

1. 在“**基本信息**”部分创建并填充默认 **应用 ID**。

1. 在“**说明**”中添加应用的短说明和长说明。

1. 在 **“开发人员信息**”中，添加所需的详细信息，并在 **“网站 (必须是有效的 HTTPS URL)** 提供 ngrok HTTPS URL。

1. 在 **“应用 URL**”中，将“隐私策略”更新为 `https://<yourngrokurl>/privacy` `https://<yourngrokurl>/tou` 和“使用条款”，然后选择“ **保存**”。

1. 在 **“应用功能**”中，选择“**个人应用** > **”“创建你的第一个个人应用”选项卡**，然后输入名称并使用 更新 **内容 URL**`https://<yourngrokurl>/personalTab`。 将“网站 URL”字段留空，从下拉列表中选择“ **上下文** ”作为“个人选项卡”，然后选择“ **确认**”。

1. 选择“保存”。

1. 在“域”部分中，选项卡中的域必须包含没有 HTTPS 前缀 `<yourngrokurl>.ngrok.io` 的 ngrok URL。

### <a name="preview-your-app-in-teams"></a>在 Teams 中预览应用

1. 在开发人员门户工具栏中选择“**在 Teams 中预览**”，开发人员门户会通知你应用已成功旁加载。 应用的“**添加**”页将显示在 Teams 中。

1. 选择“**添加**”以加载 Teams 上的选项卡。 选项卡此时在 Teams 中可用。

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetmvccoreuploaded.png" alt-text="个人选项卡":::
  
   现在，你已成功在 Teams 中创建并添加了个人选项卡。

   Teams 中含有个人选项卡时，还可以将个人选项卡 [ 重新排序 ](#reorder-static-personal-tabs)。

::: zone-end

## <a name="reorder-static-personal-tabs"></a>将静态个人选项卡重新排序

从清单版本 1.7 开始，开发人员可以重新排列其个人应用中的所有选项卡。 可以移动 **机器人聊天** 选项卡，该选项卡始终默认为个人应用选项卡标题中的第一个位置。 声明了两个保留选项卡 `entityId` 关键字，即“ **对话**”和“**相关内容**”。

如果创建具有 **个人** 范围的机器人，则默认显示在个人应用的第一个选项卡位置。 如果要将其移动到另一个位置，则必须使用保留的关键字“**对话**”将静态选项卡对象添加到清单。 “**对话**”选项卡显示在 Web 或桌面上，具体取决于在 `staticTabs` 数组中添加“**对话**”选项卡的位置。

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

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [ 创建频道或组选项卡 ](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>另请参阅

* [Teams 的生成选项卡](../what-are-tabs.md)
* [创建频道选项卡或组选项卡](create-channel-group-tab.md)
* [从个人应用或选项卡共享到 Teams](~/concepts/build-and-test/share-to-teams-from-personal-app-or-tab.md)
* [Teams 开发人员门户](../../concepts/build-and-test/teams-developer-portal.md)
* [Teams 的应用清单架构](../../resources/schema/manifest-schema.md)
* [具有自适应卡片的生成选项卡](build-adaptive-card-tabs.md)
* [移动设备上的选项卡](../design/tabs-mobile.md)
