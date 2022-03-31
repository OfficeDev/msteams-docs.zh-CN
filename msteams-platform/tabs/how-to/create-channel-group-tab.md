---
title: 创建频道或组选项卡
author: laujan
description: 使用 Yeoman 生成器创建适用于 Microsoft Teams 的频道和组选项卡的快速入门指南，包括使用代码示例查看源代码。
ms.localizationpriority: medium
ms.topic: quickstart
ms.author: lajanuar
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: 7d74a49ff85986b27ec30eeffbc15ca836a6a94b
ms.sourcegitcommit: 52af681132e496a57b18f468c5b73265a49a5f44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2022
ms.locfileid: "64590662"
---
# <a name="channel-or-group-tab"></a>"频道"或"组"选项卡

通道或组选项卡将内容传递到频道和群组聊天，是围绕基于 Web 的专用内容创建协作空间的好方法。

::: zone pivot="node-java-script"

## <a name="create-a-custom-channel-or-group-tab-with-nodejs"></a>使用自定义频道或组选项卡Node.js

1. 在命令提示符下，在安装以下命令后输入以下命令，以安装 [Yeoman](https://yeoman.io/) 和 [gulp-cli](https://www.npmjs.com/package/gulp-cli) **Node.js**：

    ```cmd
    npm install yo gulp-cli --global
    ```

2. 在命令提示符下，Microsoft Teams命令安装应用生成器：

    ```cmd
    npm install generator-teams --global
    ```

以下是创建频道或组选项卡的步骤：

* [使用通道或组选项卡生成应用程序](#generate-your-application-with-a-channel-or-group-tab)
* [创建应用包](#create-your-app-package)
* [生成并运行应用程序](#build-and-run-your-application)
* [建立到选项卡的安全隧道](#establish-a-secure-tunnel-to-your-tab)
* [Upload应用程序以Teams](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>使用通道或组选项卡生成应用程序

1. 在命令提示符下，为频道或组选项卡创建新目录。

1. 在你的新目录中输入以下命令，以启动Microsoft Teams生成器：

    ```cmd
    yo teams
    ```

1. 向应用生成器提示的一系列问题Microsoft Teams更新 **manifest.json** 文件：

    ![生成器打开屏幕截图](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

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

        使用箭头键选择"可 **配置"** 选项卡。

    * **您打算对 Tab 使用哪些范围？**

        可以选择团队或群聊。

    * **是否需要Microsoft Azure Active Directory (Azure AD) 选项卡提供单一登录支持？**

        选择 **"** 不包括Microsoft Azure Active Directory (Azure AD) "选项卡的"单一登录"支持。默认值为"是"，输入 **n**。

    * **是否希望此选项卡在 SharePoint Online 中可用？ (Y/n)**

        输入 **n**。

    </details>

> [!IMPORTANT]
> path 组件 **yourDefaultTabNameTab** 是在生成器中为 **"默认** 选项卡名称"加上单词 **"Tab**"输入的值。
>
> 例如：DefaultTabName 是 **MyTab** then **/MyTabTab/**

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

    ```bash
    gulp serve
    ```

1. 在 `http://localhost:3007/<yourDefaultAppNameTab>/` 浏览器中输入 以查看应用程序的主页。

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="默认选项卡" border="true":::

1. 若要查看选项卡配置页面，请转到 `https://localhost:3007/<yourDefaultAppNameTab>/config.html`。 如下所示：

    :::image type="content" source="~/assets/images/tab-images/configurationPage.png" alt-text="选项卡配置页" border="true":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>建立到选项卡的安全隧道

若要建立选项卡的安全隧道，请退出 localhost 并输入以下命令：

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> 通过 **ngrok** 将选项卡上传到 Microsoft Teams并成功保存后，可以在 Teams 中查看它，直到隧道会话结束。 如果重新启动 ngrok 会话，则必须使用新 URL 更新应用。

### <a name="upload-your-application-to-teams"></a>Upload应用程序以Teams

1. 转到"Microsoft Teams"**，然后选择"**&nbsp;应用商店 :::image type="content" source="~/assets/images/tab-images/store.png" alt-text="Teams应用商店&quot;":::。
1. 选择 **"管理应用"**。
1. 选择 **"发布应用"****，Upload自定义应用"**。

    :::image type="content" source="~/assets/images/tab-images/publish-app.png" alt-text="Upload自定义应用" border="true":::

1. 转到项目目录，浏览到 **./package** 文件夹，选择应用包 zip 文件夹，然后选择"打开 **"**。
    
    :::image type="content" source="~/assets/images/tab-images/channeltabadded.png" alt-text="&quot;已上载的频道&quot;选项卡" border="true":::

1. 选择 **弹出窗口** 中的"添加"。 您的选项卡将上载到Teams。
    
    > [!NOTE]
    > If  **Add** doesn't display in the dialog box then remove the following code from the manifest of the uploaded app package zip folder. 再次压缩文件夹并将其上载到Teams。
    >
    >```Json
    >"staticTabs": [],
    >"bots": [],
    >"connectors": [],
    >"composeExtensions": [],
    >```

1. 返回到团队，选择要➕添加选项卡的频道，从选项卡栏中选择，然后从列表中选择您的选项卡。
1. 按照添加选项卡的说明操作。频道或组选项卡有一个自定义配置对话框。
1. 选择 **"** 保存"，您的选项卡将添加到频道的选项卡栏中。

    :::image type="content" source="~/assets/images/tab-images/channeltabuploaded.png" alt-text="已上载&quot;频道&quot;选项卡" border="true":::

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core"></a>使用自定义频道或组选项卡 ASP.NET Core

1. 在命令提示符下，为选项卡项目创建新目录。

1. 使用下面的命令将示例存储库克隆到新目录中，也可以下载 [源代码](https://github.com/OfficeDev/Microsoft-Teams-Samples) 并解压缩文件：

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

以下是创建频道或组选项卡的步骤：

* [使用通道或组选项卡生成应用程序](#generate-your-application-with-a-channel-or-group-tab-1)
* [建立到选项卡的安全隧道](#establish-a-secure-tunnel-to-your-tab-1)
* [更新应用程序](#update-your-application)
* [生成并运行应用程序](#build-and-run-your-application-1)
* [使用开发人员门户更新应用包](#update-your-app-package-with-developer-portal)
* [在应用中预览Teams](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>使用通道或组选项卡生成应用程序

1. 打开Visual Studio并选择"**打开项目或解决方案"**。

1. 转到 Microsoft-Teams-Samplessamplestab-channel-group >  >  > **或 csharp** 文件夹，然后打开 **channelGroupTab.sln**。

1. In Visual Studio， press **F5** or choose **Start Debugging** from your application's **Debug** menu to verify if the application has loaded properly. 在浏览器中，转到以下 URL：

    * https://localhost:3978/
    * https://localhost:3978/privacy
    * https://localhost:3978/tou

<details>
<summary><b>查看源代码</b></summary>

#### <a name="startupcs"></a>Startup.cs

此项目从 3.1 ASP.NET Core 3.1 Web 应用程序空模板创建，在设置时选中了"高级 *** 配置 HTTPS**"复选框。 MVC 服务由依赖关系注入框架的方法注册 `ConfigureServices()` 。 此外，空模板默认情况下 `Configure()` 不支持为静态内容提供服务，因此，将静态文件中间件添加到 以下代码的方法中：

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

#### <a name="tabcs"></a>Tab.cs

此C#文件包含在配置过程中从 **Tab.cshtml** 调用的方法。

#### <a name="appmanifest-folder"></a>AppManifest 文件夹

此文件夹包含以下所需的应用包文件：

* 全 **色图标** ，大小为 192 x 192 像素。
* 一 **个** 32 x 32 像素的透明边框图标。
* **一个 manifest.json** 文件，用于指定应用的属性。

这些文件需要在应用包中压缩，以用于将选项卡上传到Teams。 当用户选择添加或更新`configurationUrl`选项卡时，Microsoft Teams清单中指定的内容，将其嵌入 IFrame 中，并将其呈现在选项卡中。

#### <a name="csproj"></a>.csproj

在"Visual Studio 解决方案资源管理器窗口中，右键单击项目并选择"编辑Project **文件"**。 在文件末尾，你将看到以下代码，该代码在应用程序生成时创建和更新 zip 文件夹：

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

在项目目录根目录的命令提示符下，运行以下命令以建立到选项卡的安全隧道：

```cmd
ngrok http 3978 --host-header=localhost
```

确保使命令提示符保持运行 ngrok，并记下 URL。

### <a name="update-your-application"></a>更新应用程序

1. 转到 **PagesShared**  >  文件夹并打开 **_Layout.cshtml**，然后向 <head> tags 节：

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```
    
    > [!IMPORTANT]
    > 不要复制并粘贴 `<script src="...">` 此页中的 URL，因为它们不表示最新版本。 若要获取最新版本的 SDK，请始终转到 [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js)。
    
1. 在 标记顶部 `script` ，插入对 的调用 `microsoftTeams.initialize();`。

1. 转到" **页面"** 文件夹并打开 **Tab.cshtml**

    在 **Tab.cshtml** 中，应用程序向用户显示两个选项按钮，用于显示带红色或灰色图标的选项卡。 分别选择 **"选择灰色**  **"或**"`saveGray()``saveRed()``settings.setValidityState(true)`选择红色"按钮触发器或 ，设置 并启用配置页上的"保存"按钮。 此代码Teams您已完成配置要求，并且可以继续安装。 设置 的参数 `settings.setSettings` 。 最后， `saveEvent.notifySuccess()` 调用 以指示已成功解析内容 URL。

1. 将每个 `websiteUrl` 函数 `contentUrl` 中的 和 值更新为选项卡的 HTTPS ngrok URL。

    现在，您的代码应包含以下内容， **其中 y8rCgT2b** 替换为您的 ngrok URL：

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

1. In Visual Studio， press **F5** or choose **Start Debugging** from the **Debug** menu.

1. 通过打开浏览器，然后通过命令提示符窗口中提供的 ngrok HTTPS URL 进入内容页面，验证 **ngrok** 是否正常运行。

    > [!TIP]
    > 你需要让应用程序在 Visual Studio 和 ngrok 中运行才能完成本文中提供的步骤。 如果需要停止运行应用程序，Visual Studio运行应用程序，请 **保持 ngrok 运行**。 当应用程序在应用程序中重新启动时，它会侦听并恢复Visual Studio。 如果必须重新启动 ngrok 服务，它将返回一个新 URL，并且您必须使用新 URL 更新应用程序。

### <a name="update-your-app-package-with-developer-portal"></a>使用开发人员门户更新应用包

1. 转到Microsoft Teams。 如果使用基于 [Web 的版本，](https://teams.microsoft.com)可以使用浏览器的开发人员工具检查前端 [代码](~/tabs/how-to/developer-tools.md)。

1. 导航到开发人员 **门户中的** Teams。

1. 打开 **"应用** "，然后选择 **"导入应用"**。

1. 应用包的名称 **tab.zip。** 它可在以下路径中使用：

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. 选择 **tab.zip** ，在开发人员门户中打开它。

1. 在" **基本信息** "部分创建并填充默认 **应用 ID** 。

1. 在"说明"中添加应用的 **简短和详细说明**。

1. 在 **"开发人员信息**"中，添加所需详细信息，在"网站 (必须是有效的 **HTTPS URL** ，) 您的 ngrok HTTPS URL。

1. 在 **"应用 URL"** 中，将隐私策略 `https://<yourngrokurl>/privacy` 更新为 ，将使用条款更新为 `https://<yourngrokurl>/tou` 并保存。

1. 在 **"应用功能**"中，选择"个人应用"，然后输入"名称"，然后 **使用 更新内容 URL**`https://<yourngrokurl>/personalTab`。 将"网站 URL"字段留空。 

1. 选择“保存”。

1. 在"域"部分，选项卡中的域必须包含不带 HTTPS 前缀的 ngrok URL `<yourngrokurl>.ngrok.io`。

### <a name="preview-your-app-in-teams"></a>在应用中预览Teams

1. 从 **开发人员门户Teams** 中选择"预览"。 开发人员门户会通知你你的应用已成功旁加载。

1. 选择 **"管理应用"**。 你的应用在旁加载的应用中列出。

1. 使用搜索查找应用，选择" &#x25CF;&#x25CF;&#x25CF;"。

1. 选择" **查看详细信息"** 选项。 将显示应用的应用详细信息窗口。

1. Select &nbsp;:::image type="content" source="~/assets/images/tab-images/app-dropdown.png" alt-text="App details dropdownAdd" border="true":::&nbsp; >  **to team** to load the tab in a team. 您的选项卡现已在 Teams 中提供。

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="频道选项卡 ASPNET 已上载" border="true":::

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core-mvc"></a>使用 MVC 创建自定义频道或 ASP.NET Core选项卡

1. 在命令提示符下，为选项卡项目创建新目录。

1. 使用下面的命令将示例存储库克隆到新目录中，也可以下载 [源代码](https://github.com/OfficeDev/Microsoft-Teams-Samples) 并解压缩文件：

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

以下是创建频道或组选项卡的步骤：

* [使用通道或组选项卡生成应用程序](#generate-your-application-with-a-channel-or-group-tab-2)
* [建立到选项卡的安全隧道](#establish-a-secure-tunnel-to-your-tab-2)
* [更新应用程序](#update-your-application-1)
* [生成并运行应用程序](#build-and-run-your-application-2)
* [使用开发人员门户更新应用包](#update-your-app-package-with-developer-portal-1)
* [在应用中预览Teams](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>使用通道或组选项卡生成应用程序

1. 打开Visual Studio并选择"**打开项目或解决方案"**。

1. 转到 Microsoft-Teams-Samplessamplestab-channel-groupmvc-csharp  >  >  >  文件夹，然后打开 **ChannelGroupTabMVC.sln**。

1. In Visual Studio， press **F5** or choose **Start Debugging** from your application's **Debug** menu to verify if the application has loaded properly. 在浏览器中，转到以下 URL：

    * https://localhost:3978/
    * https://localhost:3978/privacy
    * https://localhost:3978/tou

<details>
<summary><b>查看源代码</b></summary>

#### <a name="startupcs"></a>Startup.cs

此项目从 3.1 ASP.NET Core Web 应用程序空模板创建，在设置时选中了"高级 **- 配置 HTTPS**"复选框。 MVC 服务由依赖关系注入框架的方法注册 `ConfigureServices()` 。 此外，空模板默认情况下 `Configure()` 不支持为静态内容提供服务，因此，将静态文件中间件添加到 以下代码的方法中：

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

此文件夹包含以下所需的应用包文件：

* 全 **色图标** ，大小为 192 x 192 像素。
* 一 **个** 32 x 32 像素的透明边框图标。
* **一个 manifest.json** 文件，用于指定应用的属性。

这些文件需要在应用包中压缩，以用于将选项卡上传到Teams。

#### <a name="csproj"></a>.csproj

在"Visual Studio 解决方案资源管理器窗口中，右键单击项目并选择"编辑Project **文件"**。 在文件末尾，你将看到以下代码，该代码在应用程序生成时创建和更新 zip 文件夹：

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

**ChannelGroup.cs** 提供 Message 对象和方法，将在配置过程中从控制器调用该对象和方法。

#### <a name="views"></a>视图

这些是 MVC 中 ASP.NET Core视图：

* 主页：ASP.NET Core将名为 **Index** 的文件视为网站的默认页面或主页。 当浏览器 URL 指向网站的根目录时， **Index.cshtml** 将显示为应用程序的主页。

* Shared：部分视图标记 **_Layout.cshtml** 包含应用程序的整体页面结构和共享的可视元素。 它还将引用Teams库。

#### <a name="controllers"></a>控制器

控制器使用 `ViewBag` 属性将值动态传输给视图。

</details>

### <a name="establish-a-secure-tunnel-to-your-tab"></a>建立到选项卡的安全隧道

在项目目录根目录的命令提示符下，运行以下命令以建立到选项卡的安全隧道：

```cmd
ngrok http 3978 --host-header=localhost
```

确保使命令提示符保持运行 ngrok，并记下 URL。

### <a name="update-your-application"></a>更新应用程序

1. 转到 **ViewsShared**  >  文件夹并打开 **_Layout.cshtml**，然后向 <head> tags 节：

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```
    
    > [!IMPORTANT]
    > 不要复制并粘贴 `<script src="...">` 此页中的 URL，因为它们不表示最新版本。 若要获取最新版本的 SDK，请始终转到 [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js)。
    
1. 在 标记顶部 `script` ，插入对 的调用 `microsoftTeams.initialize();`。

1. 转到 **Tab 文件夹并** 打开 **Tab.cshtml**

    在 **Tab.cshtml** 中，应用程序向用户显示两个选项按钮，用于显示带红色或灰色图标的选项卡。 分别选择 **"选择灰色**  **"或**"`saveGray()``saveRed()``settings.setValidityState(true)`选择红色"按钮触发器或 ，设置 并启用配置页上的"保存"按钮。 此代码Teams您已完成配置要求，并且可以继续安装。 设置 的参数 `settings.setSettings` 。 最后， `saveEvent.notifySuccess()` 调用 以指示已成功解析内容 URL。 

1. 将每个 `websiteUrl` 函数 `contentUrl` 中的 和 值更新为选项卡的 HTTPS ngrok URL。

    现在，您的代码应包含以下内容， **其中 y8rCgT2b** 替换为您的 ngrok URL：

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

1. 确保保存更新的 **Tab.cshtml**。

### <a name="build-and-run-your-application"></a>生成并运行应用程序

1. In Visual Studio， press **F5** or choose **Start Debugging** from the **Debug** menu.

1. 通过打开浏览器，然后通过命令提示符窗口中提供的 ngrok HTTPS URL 进入内容页面，验证 **ngrok** 是否正常运行。

    > [!TIP]
    > 你需要让应用程序在 Visual Studio 和 ngrok 中运行才能完成本文中提供的步骤。 如果需要停止运行应用程序，Visual Studio运行应用程序，请 **保持 ngrok 运行**。 当应用程序在应用程序中重新启动时，它会侦听并恢复Visual Studio。 如果必须重新启动 ngrok 服务，它将返回一个新 URL，并且您必须使用新 URL 更新应用程序。

### <a name="update-your-app-package-with-developer-portal"></a>使用开发人员门户更新应用包

1. 转到Microsoft Teams。 如果使用基于 [Web 的版本，](https://teams.microsoft.com)可以使用浏览器的开发人员工具检查前端 [代码](~/tabs/how-to/developer-tools.md)。

1. 转到 **Teams 中的** 开发人员门户。

1. 打开 **"应用** "，然后选择 **"导入应用"**。

1. 应用包的名称 **tab.zip。** 它可在以下路径中使用：

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. 选择 **tab.zip** ，在开发人员门户中打开它。

1. 在" **基本信息** "部分创建并填充默认 **应用 ID** 。

1. 在"说明"中添加应用的 **简短和详细说明**。

1. 在 **"开发人员信息**"中，添加所需详细信息，在"网站 (必须是有效的 **HTTPS URL** ，) 您的 ngrok HTTPS URL。

1. 在 **"应用 URL"** 中，将隐私策略 `https://<yourngrokurl>/privacy` 更新为 ，将使用条款更新为 `https://<yourngrokurl>/tou` 并保存。

1. 在 **"应用功能**"中，选择"个人应用"，然后输入"名称"，然后 **使用 更新内容 URL**`https://<yourngrokurl>/personalTab`。 将"网站 URL"字段留空。

1. 选择“保存”。

1. 在"域"部分，选项卡中的域必须包含不带 HTTPS 前缀的 ngrok URL `<yourngrokurl>.ngrok.io`。

### <a name="preview-your-app-in-teams"></a>在应用中预览Teams

1. 从 **开发人员门户Teams** 中选择"预览"。 开发人员门户会通知你你的应用已成功旁加载。

1. 选择 **"管理应用"**。 你的应用在旁加载的应用中列出。

1. 使用搜索查找应用，选择" &#x25CF;&#x25CF;&#x25CF;"。

1. 选择" **查看详细信息"** 选项。 将显示应用的应用详细信息窗口。

1. Select &nbsp;:::image type="content" source="~/assets/images/tab-images/app-dropdown.png" alt-text="Channel tab ASPNET uploadedAdd" border="true":::&nbsp; >  **to team** to load the tab on Teams. 您的选项卡现已在 Teams 中提供。

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="频道选项卡 ASPNET MVC 已上载" border="true":::

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
