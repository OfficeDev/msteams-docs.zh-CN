---
title: 在 App Studio 中使用 C# 部署第一个应用
description: 了解如何使用 C# 或 .NET 部署 Microsoft Teams 应用。 在 App Studio 中
keywords: 入门 .net c# csharp app studio
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.localizationpriority: medium
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 6fa0b290b0d0918c02427959b96eb897931aa4de
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558455"
---
# <a name="update-c-app-package-in-app-studio"></a>更新 App Studio 中的 C# 应用包

> [!TIP]
> **试用开发人员门户**：App Studio 已演变。 使用新的[开发人员门户](https://dev.teams.microsoft.com/)配置、分发和管理 Teams 应用。

App Studio 是可从 Teams 应用商店安装的 Teams 应用。 它简化了应用的创建和注册。

完成以下步骤以更新应用包：

1. 若要在 Teams 中安装 App Studio，请选择左侧栏底部的 **“应用** ”图标，然后搜索 **App Studio**：

    <img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

1. 选择 **App Studio** 磁贴并选择 **“安装**”。 已安装 App Studio：

    <img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

1. 若要为 Teams 应用创建应用包，请在 **App Studio** 中选择 **“清单编辑器**”选项卡：

    <img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

    该示例随附其自己的清单，设计用于在生成项目时生成应用包。 manifest.json 文件可位于清单下 ```Microsoft.Teams.Samples.HelloWorld.Web```的 Visual Studio 中。

     在 Visual Studio 中，manifest.json 文件位于 **Manifest** in `Microsoft.Teams.Samples.HelloWorld.Web`下。 下图描述了此步骤：  

    <img  width="450px" alt="Build the app package on .NET with Visual Studio" src="~/assets/images/get-started/app-package-on-.NET-with-Visual-Studio.png"/>

1. 现在，若要修改此应用包，请在 **清单编辑器** 中选择“**导入现有应用**”：

    <img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

1. 为新导入的应用选择 **Hello World** 磁贴：

    <img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

    下图显示了 App Studio 中导入的应用包：

    <img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

    清单编辑器的左侧有一个步骤列表。 右侧有一个属性列表，每个步骤都需要填写这些属性。 开始使用示例应用时，大部分信息已完成。 接下来的步骤可更新Hello World应用的属性。

## <a name="app-details"></a>应用详细信息

在 **“详细信息**”下选择 **“应用详细信息**”。 选择 **“生成** ”按钮以创建新的应用 ID。

你的新应用 ID 类似于 `2322041b-72bf-459d-b107-f4f335bc35bd`。

在右侧窗格中查看应用详细信息，包括 **开发人员信息** 和 **品牌** 打造详细信息。 如果要编写用于分发的新应用，这些详细信息非常重要。

## <a name="tabs"></a>选项卡

将选项卡添加到 Teams 应用非常简单。 示例应用已支持多个选项卡，可以启用它们。

### <a name="team-tab"></a>“团队”选项卡

你的应用只能有一个“团队”选项卡：

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

在此示例中，“团队”选项卡是显示配置页的位置。 选择 **Tab 配置 URL** 的 **...** 符号，然后从下拉菜单中选择 **“编辑**”。 将 URL 更改为 `https://yourteamsapp.ngrok.io/configure` 托管应用时必须替换为使用的 URL 的位置 `yourteamsapp.ngrok.io` 。

### <a name="personal-tabs"></a>个人选项卡

你的应用最多可以有 16 个选项卡，包括“团队”选项卡。

个人选项卡与“团队”选项卡不同。 **Hello Tab** 已在具有占位符值 `com.contoso.helloworld.hellotab`的个人选项卡列表中列出。 选择 **Tab 配置 URL** 的 **...** 符号，然后从下拉菜单中选择 **“编辑**”。 将显示以下对话框：

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

使用应用 URL 更新以下框：

- 将 **“内容 URL** ”框更改为 `https://yourteamsapp.ngrok.io/hello`
- 将 **网站 URL** 框更改为 `https://yourteamsapp.ngrok.io/hello`

替换 `yourteamsapp.ngrok.io` 为托管应用时使用的 URL。

#### <a name="bots"></a>机器人

将机器人功能添加到应用很容易。 **Hello World** 示例应用已将机器人作为示例的一部分，但必须将其注册到 Microsoft：

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

从示例导入的机器人没有关联的应用 ID。 必须创建新的机器人，以便 App Studio 可以创建新的应用 ID 并将其注册到 Microsoft。

> [!NOTE]
> App Studio 为机器人创建的应用 ID 不同于为应用创建的应用 ID。 应用中的每个机器人都需要自己的应用 ID。

完成以下步骤以设置机器人：

1. 选择机器人列表中导入的机器人旁边的 **“删除** ”。 现在没有机器人可显示。
1. 选择 **“设置** ”以显示 **“设置机器人** ”对话框。

    <img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

1. 添加机器人名称 **Contoso 机器人** ，然后选择 **“作用域**”下的所有三个复选框。
1. 选择 **“保存** ”以退出对话框。 App Studio 将机器人注册到 Microsoft，并在机器人列表中显示新机器人。
1. 现在，在记事本中打开一个文本文件，并将新的机器人 ID 复制并粘贴到其中。
1. 单击 **“生成新密码**”，并记下记下机器人应用 ID 的同一文本文件中的密码。
1. 将 **机器人终结点地址** 更新为 `https://yourteamsapp.ngrok.io/api/messages`托管应用时使用的 URL，并替换 `yourteamsapp.ngrok.io` 为该 URL。
1. 现在保存文本文件，因为必须将文件中的信息添加到托管应用，以便与机器人进行安全通信。

#### <a name="messaging-extensions"></a>消息传递扩展

消息传递扩展允许用户从服务中请求信息并发布该信息。 信息以卡的形式发布到频道对话中。 消息传递扩展显示在撰写框的底部。

完成以下步骤以设置消息传递扩展：

1. 在 App Studio 左侧窗格的“**功能**”下选择 **消息传递扩展**，以配置消息传递扩展：

    <img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

    “消息传递扩展插件”窗格中列出 **了** 示例消息传递扩展。

1. 选择 **“删除** ”以删除消息传递扩展，选择 **“设置**”，然后 [按照机器人使用的](#bots)相同步骤操作。 将显示 **“消息传递扩展** ”对话框。
1. 选择“ **使用现有机器人** ”选项卡， **然后从现有机器人之一中选择**。
1. 从下拉菜单中选择创建的机器人。 添加 **机器人名称** ，然后选择 **“保存** ”以关闭对话框。
1. 在 **“命令** ”部分下，选择 **“添加**”。 若要添加基于搜索的命令，请选择 **“允许用户查询服务信息”并将其插入消息** 选项。
1. 在 **“新建命令** ”对话框中，输入以下值：

    在 **“新建”命令** 下：

    - **命令 ID**：输入随机文本
    - **标题**：输入随机标题
    - **说明**：输入随机说明

    在 **参数** 下：

    - **名称**：输入参数名称
    - **标题**：输入卡片标题
    - **说明**：输入卡片说明

1. 输入信息后，选择 **“保存** ”以关闭对话框。

#### <a name="register-your-app-in-teams"></a>在 Teams 中注册应用

输入应用的详细信息后，完成以下步骤，在 Teams 中注册应用：

1. 使用 App Studio 的 **测试和分发** 在 Teams 中安装应用。
1. 使用机器人的应用 ID 和密码更新托管应用程序。 对于示例应用，对机器人和消息传递扩展使用相同的应用 ID 和密码。
1. 在 App Studio 的左侧窗格中选择 **“测试”并分发**  到 **“完成”** 下：

    <img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

1. 若要将应用上传到 Teams，请选择“**测试和分发**”下的 **“安装**”按钮：

    <img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

    > [!NOTE]
    > 如果无法旁加载应用，请验证是否 [已启用自定义应用上传](../get-started/get-started-dotnet-app-studio.md#enable-sideloading-option)。

1. 选择 **“添加到团队**”部分中的 **“搜索**”框，然后选择要添加示例应用的团队。 可以设置一个特别团队进行测试。
1. 选择对话框底部的 **“安装** ”按钮。

    你的应用现在在 Teams 中可用。 但是，在使用应用 ID 和密码更新托管应用程序环境之前，机器人和消息传递扩展将不起作用。

    <img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>

## <a name="register-your-app-in-teams"></a>在 Teams 中注册应用

输入应用的详细信息后，完成以下步骤，在 Teams 中注册应用：

1. 使用开发人员门户 **预览** 版在 Teams 中安装应用。

    :::image type="content" source="../assets/images/teams-toolkit-v2/preview-in-teams.png" alt-text="显示预览按钮的图像":::

1. 使用机器人的应用 ID 和密码更新托管应用程序。 对于示例应用，对机器人和消息传递扩展使用相同的应用 ID 和密码。

1. 在开发人员门户的左侧窗格中选择“ **发布”以存储**  在 **“发布** ”下：

    :::image type="content" source="../assets/images/teams-toolkit-v2/devp-publish-left-pane.png" alt-text="显示左窗格中的“发布”选项的图像":::

    > [!NOTE]
    > 如果无法旁加载应用，请验证是否 [已启用自定义应用上传](../get-started/get-started-dotnet-app-studio.md#enable-sideloading-option)。

1. 选择 **“添加** ”以在 Teams 上安装应用。

    你的应用现在在 Teams 中可用。 但是，在使用应用 ID 和密码更新托管应用程序环境之前，机器人和消息传递扩展将不起作用。

## <a name="update-the-credentials-for-your-hosted-app"></a>更新托管应用的凭据

示例应用要求将环境变量设置为在文本文件中保存的值。

1. 打开解决方案资源管理器。

    :::image type="content" source="../assets/images/get-started/csharp-repo-cloned.png" alt-text="c# Teams 应用的示例存储库":::

1. 打开 `appsettings.json`文件。

    :::image type="content" source="../assets/images/teams-toolkit-v2/csharp-appsetting-json.png" alt-text="显示 appsettings.json 文件的图像":::

1. 使用保存在文本文件中的机器人 ID 更新 **MicrosoftAppId** 值。
1. 使用保存的机器人密码更新 **MicrosoftAppPassword** 。

    :::image type="content" source="../assets/images/get-started/get-started-net-azure-add-keys.png" alt-text="显示添加 Azure 密钥的图像":::

    进行这些更改后，重新生成应用。 如果使用的是 ngrok，则可以在本地运行应用，如果已将其托管在 Azure 中，则重新部署应用。

## <a name="test-the-app-capabilities-in-teams"></a>在 Teams 中测试应用功能

### <a name="test-your-tab"></a>测试选项卡

将应用安装到 Teams 后，将其配置为显示要加载应用的选项卡。

若要配置应用选项卡，请执行以下操作：

1. 转到安装了示例应用的团队中的频道，然后选择 **“+”** 按钮以添加新选项卡。
1. 从 **“添加选项卡**”列表中选择 **Hello World**。 此时会显示一个配置对话框，可选择要在此通道中显示的选项卡。
1. 选择“**保存**”。 该 `Hello World` 选项卡随选项卡一起加载。

    <img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>在 Teams 中测试机器人

现在可以在 Teams 中测试机器人。

若要测试机器人，请执行以下操作：

- 在注册应用并键 `@your-bot-name`入的团队中选择一个频道。 这种类型的消息称为 **\@提及**。 机器人会回复你发送的任何消息。

    <img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>测试消息传递扩展

若要测试消息传递扩展插件，请执行以下操作：

1. 在对话视图的输入框下方选择 **...** 将显示“**Hello World”应用的** 菜单。
1. 选择菜单，显示一组随机文本。 可以选择其中一个随机文本，并将其插入到对话中。

    <img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

    <img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

1. 选择其中一个随机文本。 将显示一张格式化且可以随自己的消息一起发送的卡片。

    <img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

| &nbsp; | &nbsp; |
|:--- | ---:|
|[Back](get-started-overview.md) | &nbsp; |
|
