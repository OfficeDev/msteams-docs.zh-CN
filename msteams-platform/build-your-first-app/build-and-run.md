---
title: 入门-构建并运行您的首个应用程序
author: heath-hamilton
description: 快速创建显示 "Hello，World！" 的 Microsoft 团队应用程序 使用 Microsoft 团队工具包的邮件。
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 62c4bd950183ceb64fb30b528661cf84e9210d89
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931772"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a>生成并运行你的首个 Microsoft 团队应用

您可以通过构建显示为 "Hello，World！" 的个人选项卡，直接跳转到 Microsoft 团队开发。

## <a name="1-create-your-app-project"></a>1. 创建您的应用程序项目

使用 Visual Studio Code 中的 Microsoft 团队工具包设置您的首个应用程序项目。

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队** "， :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 " **创建新的团队应用** "。
1. 出现提示时，使用 Microsoft 365 开发帐户登录。
1. 在 " **添加功能** " 屏幕上，依次选择 **"** **下一步** "。
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="显示如何使用 Visual Studio Code 团队工具包配置应用程序项目的屏幕截图。":::
1. 为你的团队应用输入名称。  (这是您的应用程序的默认名称，也是本地计算机上的应用程序项目目录的名称。 ) 
1. 仅检查 " **个人" 选项卡** 选项，然后选择屏幕底部的 " **完成** " 以配置项目。

## <a name="2-understand-important-app-project-components"></a>2. 了解重要的应用程序项目组件

工具包配置项目后，您就可以使用组件为团队构建基本的个人选项卡。 项目目录和文件显示在 Visual Studio Code 的 "资源管理器" 区域中。

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="显示 Visual Studio Code 中的 &quot;个人&quot; 选项卡的应用程序项目文件的屏幕截图。":::

### <a name="app-scaffolding"></a>应用程序基架

该工具包将根据您在安装过程中添加的功能，在目录中自动为您创建基架 `src` 。

例如，如果在安装过程中创建选项卡，则该 `App.js` 目录中的文件 `src/components` 很重要，因为它会处理您的应用程序的初始化和路由。 它调用 [Microsoft 团队 SDK](../tabs/how-to/using-teams-client-sdk.md) 以在您的应用程序和团队之间建立通信。

### <a name="app-id"></a>应用程序 ID

您的团队应用程序 ID 是使用应用程序 Studio 配置应用程序所必需的。 您可以在 `teamsAppId` 项目文件中找到该对象的 ID `package.json` 。

## <a name="3-build-and-run-your-app"></a>3. 生成并运行应用程序

在时间方面，你将在本地构建和运行应用程序。

 (工具包中也提供了此信息 `README` 。 ) 

1. 在终端中，转到您的应用程序项目的根目录并运行该目录 `npm install` 。
1. 运行 `npm start` 。

完成后，已 **成功编译了！** 终端中的邮件。 您的应用程序正在运行 `https://localhost:3000` 。

## <a name="4-sideload-your-app-in-teams"></a>4. 在团队中旁加载您的应用程序

您的应用程序已准备好在团队中进行测试。 若要执行此操作，您必须具有允许应用旁加载的帐户。  (如果您不能确定，请了解如何获取 [团队开发帐户](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)。 ) 

> [!TIP]
> 在添加您的应用程序之前，请使用 [应用程序中的验证功能](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)检查是否存在问题，该功能包含在工具包中。 必须修复错误才能成功旁加载应用。

1. 在 Visual Studio Code 中，按 **F5** 键以启动团队 web 客户端。
1. 若要在团队中显示应用内容，请指定您的应用程序的运行位置 (`localhost`) 是可信的：
   1. 默认情况下，在同一浏览器窗口中打开一个新选项卡 () 按 **F5** 后打开的。
   1. 转到 `https://localhost:3000/tab` ""，然后继续转到 "" 页。
1. 返回到 "团队"。 在对话框中，选择 "添加"，以安装您 **的** 应用程序。
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="显示在团队中运行的示例 &quot;Hello，World！&quot; 个人选项卡应用程序的屏幕截图。":::

🎉祝贺！ 你的应用程序正在团队中运行。

## <a name="next-step"></a>后续步骤

展开刚创建的 "个人" 选项卡或生成另一种类型的 "团队" 应用。

> [!div class="nextstepaction"]
> [添加到你的个人选项卡](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [创建频道选项卡](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [创建机器人](../build-your-first-app/build-bot.md)
