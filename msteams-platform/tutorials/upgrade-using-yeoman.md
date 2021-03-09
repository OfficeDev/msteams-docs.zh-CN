---
title: 教程 - 使用 Microsoft Teams Yeoman 生成器升级 Teams
description: 了解如何使用 Microsoft Teams Yeoman 生成器升级 Teams。
ms.topic: tutorial
ms.openlocfilehash: 0c52dd15703000a1c0f99ddd28401dd686e1b1bb
ms.sourcegitcommit: afe4bc0336663e496d03c52e4b206217c02fae63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2021
ms.locfileid: "50528631"
---
# <a name="upgrade-teams-using-microsoft-teams-yeoman-generator"></a><span data-ttu-id="ffb54-103">使用 Microsoft Teams Yeoman 生成器升级 Teams</span><span class="sxs-lookup"><span data-stu-id="ffb54-103">Upgrade Teams using Microsoft Teams Yeoman generator</span></span>
<span data-ttu-id="ffb54-104">本教程帮助你使用 Microsoft Teams Yeoman 生成器将当前 Microsoft Teams 应用版本升级到最新版本。</span><span class="sxs-lookup"><span data-stu-id="ffb54-104">This tutorial helps you to upgrade your current Microsoft Teams app version to the latest version using the Microsoft Teams Yeoman generator.</span></span>

## <a name="get-current-version-of-teams"></a><span data-ttu-id="ffb54-105">获取 Teams 的当前版本</span><span class="sxs-lookup"><span data-stu-id="ffb54-105">Get current version of Teams</span></span>
```PowerShell
 yo teams --version
```

## <a name="update-teams"></a><span data-ttu-id="ffb54-106">更新 Teams</span><span class="sxs-lookup"><span data-stu-id="ffb54-106">Update Teams</span></span>
<span data-ttu-id="ffb54-107">yo 命令列出了从创建项目到更新生成器的各种选项。</span><span class="sxs-lookup"><span data-stu-id="ffb54-107">The yo command lists out various options ranging from creating project to updating generator.</span></span> <span data-ttu-id="ffb54-108">使用以下命令选择更新生成器：</span><span class="sxs-lookup"><span data-stu-id="ffb54-108">Use the following command to select update generator:</span></span>
```PowerShell
 yo
```

<span data-ttu-id="ffb54-109">使用箭头键选择 **更新生成器**。</span><span class="sxs-lookup"><span data-stu-id="ffb54-109">Use the arrow keys to choose **Update Generators**.</span></span>
<span data-ttu-id="ffb54-110">![YoSelectUpdatGen 的图像](~/assets/images/Update-Teams/YoSelectUpdateGen.png)</span><span class="sxs-lookup"><span data-stu-id="ffb54-110">![image of YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)</span></span>

<span data-ttu-id="ffb54-111">该列表显示所有可用的生成器。</span><span class="sxs-lookup"><span data-stu-id="ffb54-111">The list displays all the available generators.</span></span> <span data-ttu-id="ffb54-112">若要从可用选项中选择或取消选择 Teams 版本，请使用空格 **键** 并选择特定的生成器。</span><span class="sxs-lookup"><span data-stu-id="ffb54-112">To select or unselect Teams version from the available options, use the **space bar** and choose a specific generator.</span></span>
<span data-ttu-id="ffb54-113">![UseSpaceToSelectGenerators 的图像](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)</span><span class="sxs-lookup"><span data-stu-id="ffb54-113">![image of UseSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)</span></span>

<span data-ttu-id="ffb54-114">Teams 安装需要几秒钟到几分钟才能完成。</span><span class="sxs-lookup"><span data-stu-id="ffb54-114">It takes few seconds to minutes for Teams installation to complete.</span></span>

<span data-ttu-id="ffb54-115">安装完成后，使用以下命令检查安装的版本：</span><span class="sxs-lookup"><span data-stu-id="ffb54-115">After the installation is complete, use the following command to check the installed version:</span></span>

```PowerShell
yo teams --version
```

![FindVersionAfterInstallation 的图像](~/assets/images/Update-Teams/FindVersionAfterInstallation.png)

<span data-ttu-id="ffb54-117">恭喜！</span><span class="sxs-lookup"><span data-stu-id="ffb54-117">Congrats!</span></span> <span data-ttu-id="ffb54-118">你已升级 Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="ffb54-118">You have upgraded Microsoft Teams.</span></span>

