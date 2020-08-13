---
title: 构建并运行您的第一个团队应用程序
author: heath-hamilton
description: 运行你的首个 Microsoft 团队应用。
ms.openlocfilehash: 98af8d8d6d89007e36c24bd34661ec21b33cbdf1
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651923"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a>生成并运行你的首个 Microsoft 团队应用

您可以通过快速构建和运行基本应用程序直接在 Microsoft 团队平台上进行开发。

> [!NOTE]
> 在遵循这些教程时， (特别对) 做出响应，有助于了解 JavaScript 的工作知识。

## <a name="set-up-your-development-account"></a>设置你的开发帐户

若要为团队构建应用程序，您需要一个允许旁加载 (的团队帐户。您的帐户可能已提供此) 。 如果不是，请注册 Microsoft 365 开发人员订阅，以便您可以获取测试租户。

1. 验证是否可以在团队中旁加载应用程序：
    1. 在 "团队客户端" 中，选择 "**应用**"。
    1. 查找用于**上传自定义应用程序**的选项。
1. 如果您有此选项，则可以开始构建。 如果不是，请执行以下操作：
    1. 注册[Microsoft 365 开发人员订阅](../doc-links/prepare-your-o365-tenant.md)。
    1. 为您的测试帐户[启用自定义应用程序旁加载](../doc-links/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。

## <a name="get-your-development-tools"></a>获取你的开发工具

您可以使用您的首选工具生成团队应用程序，但您需要使用 Visual Studio Code 和 Microsoft 团队工具包快速入门。

1. 安装最新版本的[Visual Studio Code](https://code.visualstudio.com/download)。
1. 在 Visual Studio Code 中， **Extensions**选择 ![ 左侧活动栏上的 "扩展 Visual Studio 工具包视图"， ](../doc-links/images/vs-code-extensions.png) 然后安装**Microsoft 团队工具包**。
1. 安装 [Node.js](https://nodejs.org/en/)。

## <a name="create-an-app-project"></a>创建应用程序项目

Microsoft 团队工具包可帮助您设置第一个应用程序项目。

1. 在 Visual Studio Code 中，通过选择 "团队" 图标打开工具包 ![团队图标](../doc-links/images/favicon-16x16.png) 在左侧的活动栏上。
1. 选择 "**创建新的团队应用程序**"。
1. 出现提示时，请输入您的应用程序的名称。 这是您的应用程序的默认名称，也是本地计算机上的项目目录的名称。
1. 在 "**添加功能**" 屏幕上，依次选择 **"** **下一步**"。
1. 检查 "**个人" 选项卡**选项，然后选择 "**完成**" 来配置项目。

![工具箱添加选项卡视图](../doc-links/images/toolkit-add-tabs.PNG)

完成后，您便拥有了用于构建个人选项卡的应用程序基架组件。

## <a name="run-your-app"></a>运行应用程序

按照 `README.md` 项目中的说明生成、运行应用程序并将其部署到团队。 通常情况下，这些说明可帮助您执行以下操作：

* 将您的应用程序托管在上 `localhost` 。
* [设置具有 ngrok 的安全隧道](../doc-links/debug.md#locally-hosted)，以便团队可以访问您的应用程序。  (安装[ngrok](https://ngrok.com/download)。 ) 
* 在使用文件夹中的团队客户端中[旁加载您的应用程序](../doc-links/apps-upload.md) `Development.zip` `.publish` 。

旁加载您的应用程序后，它应在团队客户端中如下所示。

![Hello world 示例选项卡](../doc-links/images/tab-running.png)

## <a name="important-app-project-files"></a>重要的应用程序项目文件

设置应用程序项目和基架后，请花些时间了解一些主要文件团队应用程序开发人员使用的文件。

### <a name="app-manifest-manifestjson"></a>应用程序清单 (`manifest.json`) 

在目录中 `.publish` ，应用程序清单是任何应用程序项目的起始点。 清单定义您的应用程序的基本属性并指向所需的资源。 在安装应用程序时，团队会对清单进行分析，以了解如何在客户端中呈现您的应用程序。

在下面的教程中，你将重点介绍用于构建个人和频道选项卡的应用程序清单的各个部分。

### <a name="package-developmentzip"></a>包 (`Development.zip`) 

也位于目录中 `.publish` ，您需要应用程序包才能在团队中[旁加载您的应用程序](../../overview.md#how-can-you-share-your-teams-app)。 在[发布到组织的应用程序目录](../../overview.md#how-can-you-share-your-teams-app)或[AppSource](../../concepts/deploy-and-publish/appsource/publish.md)时也使用它。

以下是有关应用程序包文件的一些详细信息：

|名称|类型|Size|清单位置|工具包文件名|
|---|---|:---:|:---:|-----|
|**应用程序清单**|`.json`| — | — |`.publish/manifest.json`|
|**颜色徽标**|`.png`|192 &times; 192 像素|`icon.color`|`.publish/color.png`|
|**大纲徽标**|`.png`|32 &times; 32 像素|`icon.outline`|`.publish/outline.png`|

### <a name="scaffolding-src"></a>基架 (`src`) 

该工具包将根据您在安装过程中添加的功能，在目录中自动为您创建基架 `src` 。

但无论您拥有哪种类型的应用程序，都会创建一些文件。 例如， `App.js` 目录中的文件 `src/components` 很重要，因为它处理您的应用程序的初始化和路由。 最重要的是，它调用[Microsoft 团队 SDK](../doc-links/using-teams-client-sdk.md)以在您的应用程序和团队之间建立通信。

您可以在教程中了解有关用于创建个人和频道选项卡的更多有关基架的信息。

## <a name="next-step"></a>后续步骤

🎉祝贺！ 您有一个正在运行的团队应用程序。 选择以下按钮以了解如何向其添加实际功能。

> [!div class="nextstepaction"]
> [生成个人选项卡](add-personal-tab.md)
