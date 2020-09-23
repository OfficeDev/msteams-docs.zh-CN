---
title: 构建并运行 "Hello，World！" Teams 应用
author: heath-hamilton
description: 生成并运行您的首个 Microsoft 团队应用程序（一个显示 "Hello，World！" 的个人选项卡）
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: quickstart
ms.openlocfilehash: 5be2e8f2932a91ed11137f3a7be544e12bd65559
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210149"
---
# <a name="build-a-hello-world-teams-app"></a>构建 "Hello，World！" Teams 应用

您可以通过构建显示为 "Hello，World！" 的个人选项卡，直接跳转到 Microsoft 团队平台开发。

## <a name="create-your-app-project"></a>创建您的应用程序项目

使用 Visual Studio Code 中的 Microsoft 团队工具包设置您的首个应用程序项目。

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队**"， :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 " **创建新的团队应用**"。
:::image type="content" source="../assets/images/build-your-first-app/create-teams-app.png" alt-text="显示如何使用 Visual Studio Code 团队工具包创建新应用程序的屏幕截图。":::
1. 为你的团队应用输入名称。  (这是您的应用程序的默认名称，也是本地计算机上的应用程序项目目录的名称。 ) 
1. 在 " **添加功能** " 屏幕上，依次选择 **"** **下一步**"。
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="显示如何使用 Visual Studio Code 团队工具包配置应用程序项目的屏幕截图。":::
1. 检查 " **个人" 选项卡** 选项，然后选择屏幕底部的 " **完成** " 以配置项目。

## <a name="understand-important-app-project-components"></a>了解重要的应用程序项目组件

工具包配置项目后，您就可以使用组件为团队构建基本的个人选项卡。 项目目录和文件显示在 Visual Studio Code 的 "资源管理器" 区域中。

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="显示 Visual Studio Code 中的 "个人" 选项卡的应用程序项目文件的屏幕截图。":::

让我们花点时间了解一些主要文件团队应用程序开发人员使用的。

### <a name="app-manifest-manifestjson"></a>应用程序清单 (`manifest.json`) 

在目录中 `.publish` ，应用程序清单是任何应用程序项目的起始点。 清单定义您的应用程序的基本属性并指向所需的资源。 在安装应用程序时，团队会对清单进行分析，以了解如何在客户端中呈现您的应用程序。

### <a name="app-scaffolding"></a>应用程序基架

该工具包将根据您在安装过程中添加的功能，在目录中自动为您创建基架 `src` 。

例如，如果在安装过程中创建选项卡，则该 `App.js` 目录中的文件 `src/components` 很重要，因为它会处理您的应用程序的初始化和路由。 它调用 [Microsoft 团队 SDK](../tabs/how-to/using-teams-client-sdk.md) 以在您的应用程序和团队之间建立通信。

### <a name="app-package-developmentzip"></a>应用程序包 (`Development.zip`) 

位于目录中 `.publish` ，您需要应用程序包以在团队中 [旁加载您的应用程序](../concepts/deploy-and-publish/overview.md#upload-your-app-directly) 。 [发布到组织的应用程序目录](../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog)或[AppSource](../concepts/deploy-and-publish/appsource/publish.md)时，也可以使用包。

以下是有关应用程序包文件的一些详细信息：

|名称|类型|Size|清单位置|工具包文件名|
|---|---|:---:|:---:|-----|
|**应用程序清单**|`.json`| — | — |`.publish/manifest.json`|
|**颜色徽标**|`.png`|192 &times; 192 像素|`icon.color`|`.publish/color.png`|
|**大纲徽标**|`.png`|32 &times; 32 像素|`icon.outline`|`.publish/outline.png`|

## <a name="run-your-app"></a>运行应用程序

在时间方面，你将在本地构建和运行应用程序。

 (工具包中也提供了此信息 `README` 。 ) 

1. 在终端中，转到您的应用程序项目的根目录并运行该目录 `npm install` 。
1. 运行 `npm start` 。 完成后，已 **成功编译了！** 终端中的邮件。
1. 打开浏览器并转到 `https://localhost:3000` 以查看名为 **Microsoft 团队选项卡**的空白网页。 (不会担心您无法看到页面上的任何内容。 ) <br/>
   :::image type="content" source="../assets/images/build-your-first-app/local-host-tab.png" alt-text="显示要在浏览器中查看正在运行的应用程序的外观的屏幕截图。":::

## <a name="set-up-a-secure-tunnel-to-your-app"></a>设置到您的应用程序的安全隧道

您的应用程序已启动并在本地 web 服务器上运行。 若要在团队中运行您的应用程序，您必须 `localhost` 通过 HTTPS 进行访问。

如果还未安装 [ngrok](https://ngrok.com/download) ，请安装。 运行此工具时，将创建两个全局可用的 Url，它们指向您的本地 web 服务器 (`http://localhost:3000`) 。 您需要以的开头的转发 URL `HTTPS` 。

1. 打开一个新的终端并运行 `ngrok http 3000` 。
1. 复制你提供的 HTTPS URL (请参阅以下示例) 。
:::image type="content" source="../assets/images/build-your-first-app/ngrok-running.png" alt-text="显示 ngrok 正在运行的终端的屏幕截图。":::
1. 在 `.publish` 目录中，打开 `Development.env` 。
1. 将 `baseUrl0` 值替换为复制的 URL。  (例如，改 `baseUrl0=http://localhost:3000` 为 `baseUrl0=https://85528b2b3ba5.ngrok.io` 。 ) 

您的应用程序清单现在指向您在其中承载应用程序的位置。

## <a name="sideload-your-app-in-teams"></a>在团队中旁加载您的应用程序

通过 HTTPS 运行并可访问应用程序后，即可将其上载到团队。

> [!TIP]
> 在向您的应用程序进行旁加载之前，请使用 [工具包的验证功能](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)检查是否存在问题。 必须修复错误才能成功旁加载应用。

1. 使用允许应用旁加载的帐户登录到团队客户端。  (如果您不能确定，请了解如何获取 [团队开发帐户](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)。 ) 
1. 选择 " **应用**"，然后选择 " **上载自定义应用**"。
1. 转到您的应用程序项目 `.publish` 文件夹，然后选择 `Development.zip` 。 将显示安装模式。
:::image type="content" source="../assets/images/build-your-first-app/add-teams-app.png" alt-text="显示团队应用安装模式示例的屏幕截图。":::
1. 选择 " **添加** " 以安装您的应用程序。
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="显示在团队中运行的示例 "Hello，World！" 个人选项卡应用程序的屏幕截图。":::

🎉祝贺！ 你的应用程序正在团队中运行。

## <a name="next-step"></a>后续步骤

展开刚创建的 "个人" 选项卡或生成另一种类型的 "团队" 应用。

> [!div class="nextstepaction"]
> [添加到你的个人选项卡](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [生成通道选项卡](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [构建 bot](../build-your-first-app/build-bot.md)
