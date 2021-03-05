---
title: 教程 - 使用 Microsoft Teams Yeoman 生成器升级 Teams
description: 了解如何使用 Microsoft Teams Yeoman 生成器升级 Teams。
ms.topic: tutorial
ms.openlocfilehash: 0c52dd15703000a1c0f99ddd28401dd686e1b1bb
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449601"
---
# <a name="upgrade-teams-using-microsoft-teams-yeoman-generator"></a>使用 Microsoft Teams Yeoman 生成器升级 Teams
本教程帮助你使用 Microsoft Teams Yeoman 生成器将当前 Microsoft Teams 应用版本升级到最新版本。

## <a name="get-current-version-of-teams"></a>获取 Teams 的当前版本
```PowerShell
 yo teams --version
```

## <a name="update-teams"></a>更新 Teams
yo 命令列出了从创建项目到更新生成器的各种选项。 使用以下命令选择更新生成器：
```PowerShell
 yo
```

使用箭头键选择 **更新生成器**。
![YoSelectUpdatGen 的图像](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

该列表显示所有可用的生成器。 若要从可用选项中选择或取消选择 Teams 版本，请使用空格 **键** 并选择特定的生成器。
![UseSpaceToSelectGenerators 的图像](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)

完成 Teams 安装需要几秒钟到几分钟的时间。

安装完成后，使用以下命令检查安装的版本：

```PowerShell
yo teams --version
```

![FindVersionAfterInstallation 的图像](~/assets/images/Update-Teams/FindVersionAfterInstallation.png)

恭喜！ 你已升级 Microsoft Teams。

