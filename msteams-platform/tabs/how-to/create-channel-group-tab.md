---
title: 创建通道或组选项卡
author: laujan
description: 使用 Yeoman Generator for Microsoft Teams 创建通道和组选项卡的快速入门指南，包括查看包含代码示例的源代码。
ms.localizationpriority: medium
ms.topic: quickstart
ms.author: lajanuar
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: 736b8821a7d0f9e1eda35377bc4937e68c035c75
ms.sourcegitcommit: b2f6599e44a418b4cce92f28843b7e013fd6e86d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2022
ms.locfileid: "64686674"
---
# <a name="channel-or-group-tab"></a>频道或组选项卡

通道或组选项卡将内容传递到频道和群组聊天，是围绕基于 Web 的专用内容创建协作空间的好方法。

::: zone pivot="node-java-script"

## <a name="create-a-custom-channel-or-group-tab-with-nodejs"></a>使用Node.js创建自定义通道或组选项卡

1. 在命令提示符下，在安装 **Node.js** 后输入以下命令，安装 [Yeoman](https://yeoman.io/) 和 [gulp-cli](https://www.npmjs.com/package/gulp-cli) 包：

    ```cmd
    npm install yo gulp-cli --global
    ```

2. 在命令提示符下，输入以下命令安装Microsoft Teams应用生成器：

    ```cmd
    npm install generator-teams --global
    ```

下面是创建通道或组选项卡的步骤：

* [使用通道或组选项卡生成应用程序](#generate-your-application-with-a-channel-or-group-tab)
* [创建应用包](#create-your-app-package)
* [生成并运行应用程序](#build-and-run-your-application)
* [建立到选项卡的安全隧道](#establish-a-secure-tunnel-to-your-tab)
* [Upload应用程序以Teams](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>使用通道或组选项卡生成应用程序

1. 在命令提示符下，为频道或组选项卡创建新目录。

1. 在新目录中输入以下命令以启动Microsoft Teams应用生成器：

    ```cmd
    yo teams
    ```

1. 向Microsoft Teams应用生成器提示的更新 **manifest.json** 文件的一系列问题提供值：

    ![生成器打开屏幕截图](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    <details>
    <summary><b>更新 manifest.json 文件的一系列问题</b></summary>

    * **解决方案名称是什么？**

        解决方案名称是项目名称。 可以通过选择 **Enter** 接受建议的名称。

    * **要将文件存放在哪里?**

        你目前位于项目目录中。 选择 **Enter**。

    * **Microsoft Teams应用项目的标题？**

        标题是你的应用包名称，在应用清单和说明中使用。 输入标题或选择 **Enter** 以接受默认名称。

    * **你的 (公司) 名称？ (最大 32 个字符)**

        你的公司名称将用于应用清单。 输入公司名称或选择 **Enter** 以接受默认名称。

    * **要使用哪个清单版本？**

        选择默认架构。

    * **快速基架？ (Y/n)**

        默认值为 yes;输入 **n** 以输入 Microsoft 合作伙伴 ID。

    * **输入 Microsoft 合作伙伴 ID（如果有）？ (留空以跳过)**

        此字段不是必需的，必须仅在你已是 [Microsoft 合作伙伴网络](https://partner.microsoft.com)的一部分时使用。

    * **要向项目添加哪些内容？**

        **选择 ( &ast; ) 选项卡**。

    * **要在其中托管此解决方案的 URL？**

        默认情况下，生成器建议使用 Azure 网站 URL。 仅在本地测试应用，因此不需要有效的 URL。

    * **你想要在应用/选项卡加载时显示加载指示器吗？**

        当你的应用或选项卡加载时，选择 **不** 包含加载指示器。 默认值为"否"，输入 **n**。

    * **是否希望在无选项卡标题栏的情况下呈现个人应用?**

        选择 **不** 包含要在没有选项卡标题栏的情况下呈现的个人应用。 默认值为否，输入 **n**。

    * **是否要包括测试框架和初始测试？ (y/N)**

        选择 **不** 包含此项目的测试框架。 默认值为"否"，输入 **n**。

    * **是否包括 ESLint 支持？ (y/N)**

        选择不包含 ESLint 支持。 默认值为"否"，输入 **n**。

    * **是否要将 Azure 应用程序Insights用于遥测？ (y/N)**

        选择 **不** 包含 [Azure 应用程序 Insights](/azure/azure-monitor/app/app-insights-overview)。 默认值为否;输入 **n**。

    * **默认选项卡名称 (最多 16 个字符) ？**

        为选项卡命名。此选项卡名称在整个项目中用作文件或 URL 路径组件。

    * **你想要创建哪种类型的选项卡？**

        使用箭头键选择 **"可配置"** 选项卡。

    * **你打算为选项卡使用哪些范围？**

        可以选择团队或群聊。

    * **是否需要对选项卡Microsoft Azure Active Directory (Azure AD) 单一登录支持？**

        选择 **不** 包含选项卡的Microsoft Azure Active Directory (Azure AD) 单一登录支持。默认值为"是"，输入 **n**。

    * **是否希望此选项卡在 SharePoint Online 中可用？ (Y/n)**

        输入 **n**。

    </details>

> [!IMPORTANT]
> **你的DefaultTabNameTab** 的路径组件是在 **"默认选项卡名称**"的生成器中输入的值以及"**Tab"** 一词。
>
> 例如：DefaultTabName 为 **MyTab** ，然后 **为 /MyTabTab/**

### <a name="create-your-app-package"></a>创建应用包

必须有一个应用包才能在Teams中生成和运行应用程序。 应用包是通过验证 **manifest.json** 文件并在 **./package** 目录中生成 zip 文件夹的 gulp 任务创建的。 在命令提示符处，输入以下命令：

```cmd
gulp manifest
```

### <a name="build-and-run-your-application"></a>生成并运行应用程序

#### <a name="build-your-application"></a>生成应用程序

在命令提示符处输入以下命令，将解决方案转译到 **./dist** 文件夹中：

```cmd
gulp build
```

#### <a name="run-your-application"></a>运行应用程序

1. 在命令提示符处输入以下命令以启动本地 Web 服务器：

    ```bash
    gulp serve
    ```

1. 在浏览器中输入 `http://localhost:3007/<yourDefaultAppNameTab>/` 以查看应用程序的主页。

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="默认选项卡" border="true":::

1. 若要查看选项卡配置页，请转到 `http://localhost:3007/<yourDefaultAppNameTab>/config.html`。 如下所示：

    :::image type="content" source="~/assets/images/tab-images/configurationPage.png" alt-text="选项卡配置页" border="true":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>建立到选项卡的安全隧道

若要建立到选项卡的安全隧道，请退出 localhost 并输入以下命令：

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> 通过 **ngrok** 将选项卡上传到Microsoft Teams并成功保存后，可以在Teams中查看它，直到隧道会话结束。 如果重启 ngrok 会话，则必须使用新的 URL 更新应用。

### <a name="upload-your-application-to-teams"></a>Upload应用程序以Teams

1. 转到Microsoft Teams，然后选择 **"应用**&nbsp;:::image type="content" source="~/assets/images/tab-images/store.png" alt-text="Teams应用商店":::。
1. 选择 **"管理应用****"并Upload自定义应用**。
1. 转到项目目录，浏览到 **./package** 文件夹，选择应用包 zip 文件夹，然后选择 **"打开**"。
    
    :::image type="content" source="~/assets/images/tab-images/channeltabadded.png" alt-text="上传的频道选项卡" border="true":::

1. 在对话框中选择 **"添加** "。 选项卡上传到Teams。
    
    > [!NOTE]
    > 如果  **"添加** "未显示在对话框中，则从上传的应用包 zip 文件夹的清单中删除以下代码。 再次压缩文件夹并将其上传到Teams。
    >
    >```Json
    >"staticTabs": [],
    >"bots": [],
    >"connectors": [],
    >"composeExtensions": [],
    >```

1. 按照添加选项卡的说明操作。频道或组选项卡有一个自定义配置对话框。
1. 选择 **"保存** "，将选项卡添加到频道的选项卡栏中。

    :::image type="content" source="~/assets/images/tab-images/channeltabuploaded.png" alt-text="上传的&quot;频道&quot;选项卡" border="true":::
    
    现在，你已成功创建并在Teams中添加了频道或组选项卡。

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core"></a>使用 ASP.NET Core创建自定义通道或组选项卡

1. 在命令提示符处，为 Tab 项目创建新目录。

1. 使用以下命令将示例存储库克隆到新目录中，也可以下载 [源代码](https://github.com/OfficeDev/Microsoft-Teams-Samples) 并提取文件：

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

下面是创建通道或组选项卡的步骤：

* [使用通道或组选项卡生成应用程序](#generate-your-application-with-a-channel-or-group-tab-1)
* [建立到选项卡的安全隧道](#establish-a-secure-tunnel-to-your-tab-1)
* [更新应用程序](#update-your-application)
* [生成并运行应用程序](#build-and-run-your-application-1)
* [使用开发人员门户更新应用包](#update-your-app-package-with-developer-portal)
* [在 Teams 中预览应用](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>使用通道或组选项卡生成应用程序

1. 打开Visual Studio，然后选择 **"打开项目或解决方案**"。

1. 转到 Microsoft-Teams-Samplessamplestab-channel-grouprazor-csharp  >  >  >  文件夹并打开 **channelGroupTab.sln**。

1. 在Visual Studio中，选择 **F5** 或从应用程序的"调试"菜单中选择 **"开始** 调 **试**"，以验证应用程序是否已正确加载。 在浏览器中，转到以下 URL：

    * https://localhost:3978/
    * https://localhost:3978/privacy
    * https://localhost:3978/tou

<details>
<summary><b>查看源代码</b></summary>

#### <a name="startupcs"></a>Startup.cs

此项目是从 ASP.NET Core 3.1 Web 应用程序空模板创建的，安装时选中了 **"高级 * 配置 HTTPS**"复选框。 MVC 服务由依赖关系注入框架 `ConfigureServices()` 的方法注册。 此外，默认情况下，空模板不启用提供静态内容，因此使用以下代码将静态文件中间件添加到 `Configure()` 方法：

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

ASP.NET Core将名为"**索引**"的文件视为网站的默认或主页。 当浏览器 URL 指向站点的根目录时， **Index.cshtml** 将显示为应用程序的主页。

#### <a name="tabcs"></a>Tab.cs

此 C# 文件包含在配置期间从 **Tab.cshtml** 调用的方法。

#### <a name="appmanifest-folder"></a>AppManifest 文件夹

此文件夹包含以下必需的应用包文件：

* **一个全色图标**，尺寸为 192 x 192 像素。
* 一个 **透明轮廓图标** ，尺寸为 32 x 32 像素。
* 一个 **manifest.json** 文件，指定应用的属性。

这些文件需要压缩在应用包中，以便用于将选项卡上传到Teams。 当用户选择添加或更新选项卡时，Microsoft Teams加载`configurationUrl`清单中指定的选项卡，将其嵌入 IFrame 中，并将其呈现在选项卡中。

#### <a name="csproj"></a>.csproj

在Visual Studio 解决方案资源管理器窗口中，右键单击项目，然后选择 **"编辑Project文件**"。 在文件末尾，会看到以下代码，用于在应用程序生成时创建和更新 zip 文件夹：

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

### <a name="establish-a-secure-tunnel-to-your-tab"></a>建立到选项卡的安全隧道

在项目目录根目录的命令提示符处运行以下命令，以建立到选项卡的安全隧道：

```cmd
ngrok http 3978 --host-header=localhost
```

确保在 ngrok 运行时保持命令提示符，并记下 URL。

### <a name="update-your-application"></a>更新应用程序

1. 打开Visual Studio 解决方案资源管理器并转到 **PagesShared**  >  文件夹并打开 **_Layout.cshtml**，并将以下内容添加到 <head> "标记"部分：

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```
    
    > [!IMPORTANT]
    > 请勿从此页面复制和粘贴 `<script src="...">` URL，因为它们不表示最新版本。 若要获取最新版本的 SDK，请始终转到 [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js)。
    
1. 在标记中`script`插入调`microsoftTeams.initialize();`用。

1. 在Visual Studio 解决方案资源管理器转到 **Pages** 文件夹并打开 **Tab.cshtml**

    在 **Tab.cshtml** 中，应用程序向用户提供两个选项按钮，用于显示带有红色或灰色图标的选项卡。 选择 **"选择灰色** "或 **"选择红色** "按钮触发器 `saveGray()` ，或 `saveRed()`分别设置 `settings.setValidityState(true)`和启用配置页上的 **"保存** "按钮。 此代码让Teams知道你已完成配置要求，并且安装可以继续进行。 已设置参数 `settings.setSettings` 。 最后， `saveEvent.notifySuccess()` 调用以指示已成功解析内容 URL。

1. `websiteUrl`使用 HTTPS ngrok URL 将每个函数中的值更新`contentUrl`到选项卡。

    代码现在应包含以下 **内容，其中 y8rCgT2b** 替换为 ngrok URL：

    ```javascript
        
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

1. 保存更新的 **Tab.cshtml**。

### <a name="build-and-run-your-application"></a>生成并运行应用程序

1. 在Visual Studio中，选择 **F5** 或从"**调试**"菜单中选择 **"开始** 调试"。

1. 通过打开浏览器并通过命令提示符窗口中提供的 ngrok HTTPS URL 转到内容页，验证 **ngrok** 是否正常运行和正常工作。

    > [!TIP]
    > 需要运行Visual Studio和 ngrok 中的应用程序才能完成本文中提供的步骤。 如果需要停止在Visual Studio中运行应用程序以处理它，**请保持 ngrok 运行**。 当应用程序在Visual Studio中重新启动时，它会侦听并恢复其请求的路由。 如果必须重启 ngrok 服务，它将返回一个新的 URL，并且必须使用新 URL 更新应用程序。

### <a name="update-your-app-package-with-developer-portal"></a>使用开发人员门户更新应用包

1. 转到Microsoft Teams。 如果使用 [基于 Web 的版本](https://teams.microsoft.com)，可以使用浏览器的 [开发人员工具](~/tabs/how-to/developer-tools.md)检查前端代码。

1. 转到 [**开发人员门户**](https://dev.teams.microsoft.com/home)。

1. 打开 **应用** 并选择 **"导入"应用**。

1. 应用包的名称 **tab.zip**。 它可在以下路径中使用：

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. 选择 **tab.zip** 并在开发人员门户中打开它。

1. 在 **"基本信息**"部分创建并填充默认 **应用 ID**。

1. 在 **"说明**"中添加应用的短和长说明。

1. 在 **开发人员信息** 中，添加所需的详细信息，在 **网站 (必须是有效的 HTTPS URL)** 提供 ngrok HTTPS URL。

1. 在 **应用 URL** 中，将隐私策略更新为`https://<yourngrokurl>/privacy``https://<yourngrokurl>/tou`和保存使用条款。

1. 在 **应用功能** 中，选择"组"和"频道"应用。 使用并选择选项卡 **范围** 更新 **配置 URL**`https://<yourngrokurl>/tab`。

1. 选择 **“保存”**。

1. 在"域"部分中，选项卡中的域必须包含没有 HTTPS 前缀 `<yourngrokurl>.ngrok.io`的 ngrok URL。

### <a name="preview-your-app-in-teams"></a>在 Teams 中预览应用

1. 从开发人员门户工具栏 **中选择Teams预览** 版，开发人员门户会通知你应用已成功旁加载。 **应用的"添加**"页将显示在Teams中。

1. 选择 **"添加到团队** "以在团队中设置选项卡。 配置选项卡并选择 **"保存**"。 选项卡现在在Teams中可用。

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="上传的&quot;频道&quot;选项卡 ASPNET" border="true":::
    
    现在，你已成功创建并在Teams中添加了频道或组选项卡。

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core-mvc"></a>使用 ASP.NET Core MVC 创建自定义通道或组选项卡

1. 在命令提示符处，为 Tab 项目创建新目录。

1. 使用以下命令将示例存储库克隆到新目录中，也可以下载 [源代码](https://github.com/OfficeDev/Microsoft-Teams-Samples) 并提取文件：

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

下面是创建通道或组选项卡的步骤：

* [使用通道或组选项卡生成应用程序](#generate-your-application-with-a-channel-or-group-tab-2)
* [建立到选项卡的安全隧道](#establish-a-secure-tunnel-to-your-tab-2)
* [更新应用程序](#update-your-application-1)
* [生成并运行应用程序](#build-and-run-your-application-2)
* [使用开发人员门户更新应用包](#update-your-app-package-with-developer-portal-1)
* [在 Teams 中预览应用](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>使用通道或组选项卡生成应用程序

1. 打开Visual Studio，然后选择 **"打开项目或解决方案**"。

1. 转到 Microsoft-Teams-Samplessamplestab-channel-groupmvc-csharp  >  >  >  文件夹并打开 **ChannelGroupTabMVC.sln**。

1. 在Visual Studio中，选择 **F5** 或从应用程序的"调试"菜单中选择 **"开始** 调 **试**"，以验证应用程序是否已正确加载。 在浏览器中，转到以下 URL：

    * https://localhost:3978/
    * https://localhost:3978/privacy
    * https://localhost:3978/tou

<details>
<summary><b>查看源代码</b></summary>

#### <a name="startupcs"></a>Startup.cs

此项目是从 ASP.NET Core 3.1 Web 应用程序空模板创建的，安装时选中了 **"高级 - 配置 HTTPS**"复选框。 MVC 服务由依赖关系注入框架 `ConfigureServices()` 的方法注册。 此外，默认情况下，空模板不启用提供静态内容，因此使用以下代码将静态文件中间件添加到 `Configure()` 方法：

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

#### <a name="appmanifest-folder"></a>AppManifest 文件夹

此文件夹包含以下必需的应用包文件：

* **一个全色图标**，尺寸为 192 x 192 像素。
* 一个 **透明轮廓图标** ，尺寸为 32 x 32 像素。
* 一个 **manifest.json** 文件，指定应用的属性。

这些文件需要压缩在应用包中，以便用于将选项卡上传到Teams。

#### <a name="csproj"></a>.csproj

在Visual Studio 解决方案资源管理器窗口中，右键单击项目，然后选择 **"编辑Project文件**"。 在文件末尾，你会看到以下代码，该代码在应用程序生成时创建和更新 zip 文件夹：

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

#### <a name="models"></a>模型

**ChannelGroup.cs** 显示一个 Message 对象和方法，将在配置期间从控制器调用。

#### <a name="views"></a>视图

这些是 MVC ASP.NET Core中的不同视图：

* 主页：ASP.NET Core将名为"**索引**"的文件视为网站的默认或主页。 当浏览器 URL 指向站点的根目录时， **Index.cshtml** 将显示为应用程序的主页。

* 共享：部分视图标记 **_Layout.cshtml** 包含应用程序的整体页面结构和共享的视觉元素。 它还将引用Teams库。

#### <a name="controllers"></a>控制器

控制器使用该 `ViewBag` 属性动态地将值传输到视图。

</details>

### <a name="establish-a-secure-tunnel-to-your-tab"></a>建立到选项卡的安全隧道

在项目目录根目录的命令提示符处运行以下命令，以建立到选项卡的安全隧道：

```cmd
ngrok http 3978 --host-header=localhost
```

确保在 ngrok 运行时保持命令提示符，并记下 URL。

### <a name="update-your-application"></a>更新应用程序

1. 打开Visual Studio 解决方案资源管理器并转到 **ViewsShared**  >  文件夹并打开 **_Layout.cshtml**，并将以下内容添加到 <head> "标记"部分：

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```
    
    > [!IMPORTANT]
    > 请勿从此页面复制和粘贴 `<script src="...">` URL，因为它们不表示最新版本。 若要获取最新版本的 SDK，请始终转到 [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js)。
    
1. 在标记中`script`插入调`microsoftTeams.initialize();`用。

1. 在Visual Studio 解决方案资源管理器转到 **Tab** 文件夹并打开 **Tab.cshtml**

    在 **Tab.cshtml** 中，应用程序向用户提供两个选项按钮，用于显示带有红色或灰色图标的选项卡。 选择 **"选择灰色** "或 **"选择红色** "按钮触发器 `saveGray()` ，或 `saveRed()`分别设置 `settings.setValidityState(true)`和启用配置页上的 **"保存** "按钮。 此代码让Teams知道你已完成配置要求，并且安装可以继续进行。 已设置参数 `settings.setSettings` 。 最后， `saveEvent.notifySuccess()` 调用以指示已成功解析内容 URL。 

1. `websiteUrl`使用 HTTPS ngrok URL 将每个函数中的值更新`contentUrl`到选项卡。

    代码现在应包含以下 **内容，其中 y8rCgT2b** 替换为 ngrok URL：

    ```javascript

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

1. 请确保保存更新的 **Tab.cshtml**。

### <a name="build-and-run-your-application"></a>生成并运行应用程序

1. 在Visual Studio中，选择 **F5** 或从"**调试**"菜单中选择 **"开始** 调试"。

1. 通过打开浏览器并通过命令提示符窗口中提供的 ngrok HTTPS URL 转到内容页，验证 **ngrok** 是否正常运行和正常工作。

    > [!TIP]
    > 需要运行Visual Studio和 ngrok 中的应用程序才能完成本文中提供的步骤。 如果需要停止在Visual Studio中运行应用程序以处理它，**请保持 ngrok 运行**。 当应用程序在Visual Studio中重新启动时，它会侦听并恢复其请求的路由。 如果必须重启 ngrok 服务，它将返回一个新的 URL，并且必须使用新 URL 更新应用程序。

### <a name="update-your-app-package-with-developer-portal"></a>使用开发人员门户更新应用包

1. 转到Microsoft Teams。 如果使用 [基于 Web 的版本](https://teams.microsoft.com)，可以使用浏览器的 [开发人员工具](~/tabs/how-to/developer-tools.md)检查前端代码。

1. 转到 [**开发人员门户**](https://dev.teams.microsoft.com/home)。

1. 打开 **应用** 并选择 **"导入"应用**。

1. 应用包的名称 **tab.zip**。 它可在以下路径中使用：

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. 选择 **tab.zip** 并在开发人员门户中打开它。

1. 在 **"基本信息**"部分创建并填充默认 **应用 ID**。

1. 在 **"说明**"中添加应用的短和长说明。

1. 在 **开发人员信息** 中，添加所需的详细信息，在 **网站 (必须是有效的 HTTPS URL)** 提供 ngrok HTTPS URL。

1. 在 **应用 URL** 中，将隐私策略更新为`https://<yourngrokurl>/privacy``https://<yourngrokurl>/tou`和保存使用条款。

1. 在 **应用功能** 中，选择"组"和"频道"应用。 使用并选择选项卡 **范围** 更新 **配置 URL**`https://<yourngrokurl>/tab`。

1. 选择 **“保存”**。

1. 在"域"部分中，选项卡中的域必须包含没有 HTTPS 前缀 `<yourngrokurl>.ngrok.io`的 ngrok URL。

### <a name="preview-your-app-in-teams"></a>在 Teams 中预览应用

1. 从开发人员门户工具栏 **中选择Teams预览** 版，开发人员门户会通知你应用已成功旁加载。 **应用的"添加**"页将显示在Teams中。

1. 选择 **"添加到团队** "以在团队中设置选项卡。 配置选项卡并选择 **"保存**"。 选项卡现在在Teams中可用。

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="上传的通道选项卡 ASPNET MVC" border="true":::
    
    现在，你已成功创建并在Teams中添加了频道或组选项卡。

::: zone-end

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [创建内容页](~/tabs/how-to/create-tab-pages/content-page.md)

## <a name="see-also"></a>另请参阅

* [Teams选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [移动设备上的选项卡](~/tabs/design/tabs-mobile.md)
* [具有自适应卡片的生成选项卡](~/tabs/how-to/build-adaptive-card-tabs.md)
* [创建删除页面](~/tabs/how-to/create-tab-pages/removal-page.md)
