---
title: 入门 - 生成并运行你的第一个应用
author: girliemac
description: 快速创建显示"Hello， World！"的 Microsoft Teams 应用 message using the Microsoft Teams Toolkit.
ms.author: timura
ms.date: 03/22/2021
ms.topic: quickstart
ms.openlocfilehash: b34409919f073535c741a48edf30f3edd8c6bc8f
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068773"
---
# <a name="create-your-first-microsoft-teams-app"></a>创建你的第一个 Microsoft Teams 应用

本快速入门指导你生成并运行显示"Hello， World！"的 Microsoft Teams 应用

## <a name="prerequisites"></a>先决条件

开始之前，你需要设置 Teams [开发租户并](#set-up-your-teams-development-tenant) 安装 Teams [开发工具](#install-your-development-tools)。

### <a name="set-up-your-teams-development-tenant"></a>设置 Teams 开发租户

**租户** 就像组织的容器。 就 Teams 而言，租户是组织聊天、共享文件和运行会议的地方。 作为开发人员，你需要一个租户来旁加载和测试你正在构建的 Teams 应用。  

# <a name="do-not-have-a-tenant"></a>[没有租户](#tab/do-not-have-a-tenant)

通过加入 Microsoft 365 开发人员计划，你可以获取免费的 Teams 测试帐户，其中包括允许应用旁加载的租户。 注册过程大约需要两分钟。

**获取租户**

1. 转到 [Microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program)。
1. 选择 **立即加入** 并按照屏幕上的说明进行操作。
1. 在欢迎屏幕中，选择 **"设置 E5 订阅"。**
1. 设置 Microsoft 365 开发人员帐户。 
   完成后，将显示以下屏幕：

   :::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="注册 Microsoft 365 开发人员计划后看到的示例。":::

1. 使用新帐户登录 Teams。
1. 在 Teams 客户端中，选择"**应用"。**
1. 验证是否可以看到" **上载自定义应用"** 选项。 如果你这样做，这意味着你可以旁加载应用。

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="显示可以在 Teams 中上传自定义应用位置的图示。":::

# <a name="have-a-tenant"></a>[拥有租户](#tab/have-a-tenant)

如果你已有租户，请验证你能否在 Teams 中旁加载应用。

**验证你能否旁加载应用** 

1. 在 Teams 客户端中，选择"**应用"。** 
1.  验证是否可以看到" **上载自定义应用"** 选项。 如果你这样做，这意味着你可以旁加载应用。 

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="显示可以在 Teams 中上传自定义应用位置的图示。":::

---

### <a name="install-your-development-tools"></a>安装开发工具

若要生成此应用，请使用 Teams Toolkit for Visual Studio Code 快速入门。 您还可以使用你预先提供的任何工具构建 Teams 应用。 

> [!NOTE]
> Teams 仅通过 HTTPS 连接显示应用内容。 若要在本地调试某些类型的应用（如机器人），你将了解如何使用 ngrok 在 Teams 和你的应用之间设置安全隧道。
> 
> 生产 Teams 应用托管在云中。

**安装 Microsoft Teams 工具**

1. 安装 [Node.js](https://nodejs.org/en/)。
1. 如果你计划构建机器人或消息传递扩展，请安装[ngrok，](https://ngrok.com/download)然后使用[ngrok 将 localhost 公开到 Internet。](../tutorials/get-started-dotnet-app-studio.md#tunnel-using-ngrok)
1. 安装最新版本的 [Visual Studio Code](https://code.visualstudio.com/download)。 
   
   > [!NOTE]
   > 该工具包不支持早期版本的 Visual Studio Code。

1. 在左侧活动栏中，选择"**扩展"。** :::image type="icon" source="../assets/icons/vs-code-extensions.png":::
1. 在 **Microsoft Teams Toolkit** 中，选择"安装 **"。**

   :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="此插图显示Visual Studio代码可以安装 Microsoft Teams Toolkit扩展。":::

## <a name="1-create-your-app-project"></a>1. 创建应用项目

1. 打开Visual Studio代码。
1. 选择 **"Microsoft Teams Toolkit** :::image type="icon" source="../assets/icons/vsc-toolkit.png":::  >  **创建新的 Teams 应用"。**

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-02.png" alt-text="Screenshot showing how to create your app project with the Visual Studio Code Teams Toolkit.":::
   
1. 使用 Microsoft 365 开发帐户登录。 可以是你刚刚创建的帐户，或者是你已经拥有允许应用旁加载的帐户。
1. 在"**选择项目"屏幕上**，转到"个人应用"，然后选择 **"JS** (JavaScript) >**下一步"。**

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-03.png" alt-text="Screenshot showing how to configure your app project with the Visual Studio Code Teams Toolkit.":::

1. 输入 Teams 应用的名称。

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-04.png" alt-text="Screenshot showing how to add a name to your app project with the Visual Studio Code Teams Toolkit.":::

1. 选择 **“完成”**。 
   现已配置项目。 

## <a name="2-understand-your-app-project-components"></a>2. 了解应用项目组件

在工具包配置应用项目后，你拥有用于生成"Hello， World！"的组件。 Teams 应用。 项目的目录和文件位于"代码Visual Studio中。 

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-05.png" alt-text="Screenshot showing the scaffolding in your app project with the Visual Studio Code Teams Toolkit.":::

该工具包根据你在设置期间添加的功能，在目录中自动 `src` 创建应用基架。 由于你在设置期间创建了一个选项卡，因此目录中的文件将处理 `App.js` `src/components` 应用的初始化和路由。 该文件还调用 Microsoft Teams JavaScript 客户端 SDK 以在你的应用和 Teams 之间建立通信。 

## <a name="3-build-and-run-your-app"></a>3. 生成并运行应用

在本地生成并运行应用以节省时间。 

**生成和运行应用**

1. 在Visual Studio代码"中，选择"**查看终端**  >  **"。**
1. 运行 `npm install`。
1. 运行 `npm start`。
  
  编译 **成功！** 消息显示在终端中。 你的应用现在在 的 localhost 上运行 `https://localhost:3000` 。 

## <a name="4-sideload-your-app-in-teams"></a>4. 在 Teams 中旁加载应用

旁加载是在 Teams 中安装尚未由管理员或 Microsoft 批准的应用的过程。 旁加载在测试和调试 Teams 应用时很常见。

默认情况下，Teams 不允许应用旁加载。 可以在 Teams 管理中心更改此设置。

**在 Teams 中启用应用旁加载**

1. 使用管理员凭据登录 [Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) 管理中心。  
1. 选择 **"显示所有**  >  **团队"。** 

   ![管理中心菜单的图像](~/assets/images/prepare-test-tenant/admin-center.png)

   > [!Note] 
   > 可能需要 24 小时才能 **显示 Teams** 选项。 

1. 转到 **Teams 应用**  >  **设置策略**  >  全局 (组织范围内的默认) 。

   ![打开旁加载视图](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

1. 打开"上传 **自定义应用"** 切换。

1. 选择 **"保存** "保存更改。

   测试租户现在允许自定义应用旁加载。

   > [!Note]
   > 使用 App Studio 中的验证功能（包含在工具包中）旁加载应用之前检查问题。 修复错误以成功旁加载应用。


### <a name="sideload-your-app"></a>旁加载应用

1. 在Visual Studio代码"中，打开 Teams Toolkit。
1. 转到 **App Studio**。  
1. 选择 **"测试和分发**  >  **安装"。**

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-appstudio.png" alt-text="Screenshot showing how to sideload your app to Teams client with the Visual Studio Code Teams Toolkit.":::

**或者**

1. 选择 **F5** 键以打开要安装的浏览器窗口。 这将跳过 **App Studio** 中的安装过程，并关闭浏览器中的 Teams。
1. 在安装对话框中，选择 **"添加"** 将应用安装到 Teams。

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install.png" alt-text="显示如何将应用旁加载至 Teams 客户端的屏幕截图。":::

   > [!Note]
   > App Studio 还作为独立的 Teams 客户端应用提供。

### <a name="troubleshoot-sideloading-issues"></a>旁加载问题疑难解答

**安装失败**

如果在 `Manifest parsing has failed` 安装应用时显示错误消息，请验证应用信息输入是否正确。

**验证应用信息**

* In the Teams Toolkit， go to **App Studio**  >  **App details** and verify that all the required information is correctly entered.
*  如果手动编辑文件，请验证 JSON 在 App Studio 的应用清单工具 `manifest.json` 中是否定义良好。 

**不显示选项卡内容**

验证你的应用是否正在运行。 如果不是，请转到终端并运行 `npm start` 。

## <a name="see-also"></a>另请参阅

* [准备 Microsoft 365 租户](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant)
* [选择用于测试和调试 Microsoft Teams 应用的设置](../concepts/build-and-test/debug.md)
* [使用 Microsoft Teams JavaScript 客户端 SDK 生成选项卡和其他托管体验](../tabs/how-to/using-teams-client-sdk.md)
* [准备 AppSource 提交](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [使用 App Studio for Microsoft Teams 快速开发应用](../concepts/build-and-test/app-studio-overview.md)
* [创建频道选项卡](../build-your-first-app/build-channel-tab.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [为 Microsoft Teams 生成个人选项卡](../build-your-first-app/build-personal-tab.md)
