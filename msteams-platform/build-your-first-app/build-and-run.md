---
title: 入门 - 生成并运行你的第一个应用
author: heath-hamilton
description: 快速创建显示"Hello， World！" 的 Microsoft Teams 应用 消息 Toolkit。
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 46a92f54cdbf68e28510c0bd4cc0b7018cfaae3c
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093948"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a>生成并运行你的第一个 Microsoft Teams 应用

通过生成显示"Hello， World！"的个人选项卡开始 Microsoft Teams 开发。
按照以下步骤生成并运行你的第一个 Teams 应用：

## <a name="1-create-your-app-project"></a>1. 创建应用项目

使用 Microsoft Teams Toolkit代码Visual Studio设置你的第一个应用项目。 使用以下步骤创建应用项目：

1. 在Visual Studio代码中，选择左侧活动栏上的 **Microsoft Teams，** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 **"创建新的 Teams 应用"。**
1. 当系统提示时，使用 Microsoft 365 开发帐户登录。
1. 在"**添加功能"屏幕上**，选择 **"Tab"，** 然后选择"**下一步"。**
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Screenshot showing how to configure your app project with the Visual Studio Code Teams Toolkit.":::
1. 输入 Teams 应用的名称。  (这是应用的默认名称，也是本地计算机上应用项目目录的名称。) 
1. 仅选中 **"个人"选项卡****选项，然后选择** 屏幕底部的"完成"以配置项目。

## <a name="2-understand-important-app-project-components"></a>2. 了解重要的应用项目组件

工具包配置项目后，你即拥有为 Teams 生成基本个人选项卡的组件。 项目目录和文件显示在代码的资源管理器Visual Studio区域中。

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Screenshot showing app project files for a personal tab in Visual Studio Code.":::

### <a name="app-scaffolding"></a>应用基架

该工具包会基于你在设置过程中添加的功能在目录中自动 `src` 创建基架。

例如，如果在设置期间创建选项卡，则目录中的文件非常重要，因为它处理应用的初始化 `App.js` `src/components` 和路由。 它调用 [Microsoft Teams JavaScript 客户端 SDK](../tabs/how-to/using-teams-client-sdk.md) 以在应用和 Teams 之间建立通信。

### <a name="app-id"></a>应用程序 ID

使用 Teams 应用 ID 使用 App Studio 配置应用。 在位于项目文件中的对象中查找 `teamsAppId` `package.json` ID。

## <a name="3-build-and-run-your-app"></a>3. 生成并运行应用

在本地生成并运行应用以节省时间。 This information is also available in the toolkit `README` . 使用以下步骤生成并运行应用：

1. 在终端中，转到应用项目的根目录并运行 `npm install` 。
1. 运行 `npm start`。

完成后，将成功 **进行编译！** 消息。 你的应用正在运行 `https://localhost:3000` 。

## <a name="4-sideload-your-app-in-teams"></a>4. 在 Teams 中旁加载应用

你的应用已准备好在 Teams 中进行测试。 为此，你必须拥有允许应用旁加载的 Microsoft 365 开发帐户。 有关帐户打开详细信息，请参阅 [Teams 开发帐户](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)。 

> [!TIP]
> 使用 App [Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)中的验证功能（包含在工具包中）旁加载应用之前检查问题。 修复错误以成功旁加载应用。

使用以下步骤在 Teams 中旁加载应用：

> [!NOTE]
> 若要在 Teams 中旁加载应用之前启用旁加载，请按照"打开 [应用旁加载"中的步骤操作](../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。

1. 选择 **F5** 键以在 Visual Studio 代码中启动 Teams Web 客户端。
1. 若要在 Teams 中显示你的应用内容，请指定你的应用在哪些 () `localhost` 可信：
   1. 默认情况下，在 Google Chrome 的相同浏览器窗口中打开 (选项卡，) **按 F5 后打开**。
   1. 转到 `https://localhost:3000/tab` 并转到页面。
1. 返回到 Teams。 在对话框中，选择 **"为我添加** "以安装应用。
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="显示 Teams 中运行的个人选项卡应用示例&quot;Hello， World！&quot;的屏幕截图。":::

🎉恭喜！ 你的应用在 Teams 中运行。

## <a name="next-step"></a>后续步骤

在刚创建的个人选项卡上展开，或生成另一种类型的 Teams 应用。

> [!div class="nextstepaction"]
> [添加到个人选项卡](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [创建频道选项卡](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [创建机器人](../build-your-first-app/build-bot.md)
