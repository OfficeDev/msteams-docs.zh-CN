---
title: Live Share 快速入门
description: 在本模块中，了解如何快速尝试 Dice Roller 示例
ms.topic: concept
ms.localizationpriority: high
ms.author: stevenic
ms.openlocfilehash: caf2e7386c22f01edb43cf0ad5ec444d5e068d07
ms.sourcegitcommit: c197fe4c721822b6195dfc5c7d8e9ccd47f142fe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2022
ms.locfileid: "65668218"
---
---

# <a name="quick-start-guide"></a>快速入门指南

使用 Dice Roller 示例开始使用 Live Share SDK。 此快速入门是 [Fluid Framework 快速入门](https://fluidframework.com/docs/start/quick-start/)的演变，旨在快速在计算机的 localhost 上运行基于 Live Share SDK 的 [Dice Scroll 示例](https://github.com/microsoft/live-share-sdk/tree/main/samples/01.dice-roller)。

:::image type="content" source="../assets/images/teams-live-share/dice-roller.png" alt-text="DiceRoller 示例":::

> [!NOTE]
> 本指南逐步讲解如何在浏览器中本地使用 Live Share。 若要详细了解如何在 Teams 会议中使用 SDK，请试用我们的 [Agile Poker 教程](../sbs-teams-live-share.yml)。

## <a name="set-up-your-development-environment"></a>设置开发环境

若要开始，请安装以下内容：

* [Node.js](https://nodejs.org/en/download)：Live Share SDK 支持 Node.js LTS 版本 12.17 及更高版本。
* [最新版本的 Visual Studio Code](https://code.visualstudio.com/)。
* [Git](https://git-scm.com/downloads)

## <a name="build-and-run-the-dice-roller-app"></a>构建并运行 Dice Roller 应用

1. 转至 [Dice Roller](https://github.com/microsoft/live-share-sdk/tree/main/samples/01.dice-roller) 示例应用。

1. 克隆 [Live Share SDK](https://github.com/microsoft/live-share-sdk) 存储库以测试示例应用：

    ```bash
    $ git clone https://github.com/microsoft/live-share-sdk.git
    ```

1. 运行以下命令以转到 Dice Roller 示例应用文件夹：

   ```bash
    $ cd live-share-sdk\samples\01.dice-roller
   ```

1. 运行以下命令以安装依赖项包：

    ```bash
    $ npm install
    ```

1. 运行以下命令以启动客户端和本地服务器：

   ```bash
   $ npm start
   ```
  
     新的浏览器选项卡将打开一个 `http://localhost:8080` URL，并显示 Dice Roller 游戏。

1. 复制浏览器中的完整 URL（包括 ID），并将 URL 粘贴到新窗口或其他浏览器中。

   将打开第二个用于 Dice Roller 应用程序的客户端。

1. 打开两个窗口，然后在一个窗口中选择“**滚动**”按钮。 两个客户端中的骰子状态都会发生变化。

    :::image type="content" source="../assets/images/teams-live-share/dice-roller.png" alt-text="Dice Roller 多个选项卡":::
  
   **恭喜**！你已了解如何使用 Live Share SDK 构建和运行应用。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [Dice Roller 教程](teams-live-share-tutorial.md)

## <a name="see-also"></a>另请参阅

* [GitHub 存储库](https://github.com/microsoft/live-share-sdk)
* [Live Share SDK 参考文档](/javascript/api/@microsoft/live-share/)
* [Live Share 媒体 SDK 参考文档](/javascript/api/@microsoft/live-share-media/)
* [Live Share 功能](teams-live-share-capabilities.md)
* [Live Share 常见问题解答](teams-live-share-faq.md)
* [会议中的 Teams 应用](teams-apps-in-meetings.md)
