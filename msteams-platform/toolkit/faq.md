---
title: 常见问题
author: MuyangAmigo
description: 在本模块中，请参阅使用 Visual Studio Code 的 Teams 工具包常见问题解答
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 6a6c6599ff036cf7b81dd30b00e5608db3dc4cc2
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243373"
---
# <a name="faq-for-teams-toolkit"></a>Teams 工具包常见问题解答

可以看到适用于Visual Studio Code的 Teams 工具包的所有部分的常见问题解答。

[使用 Teams 工具包预配云资源的](provision.md)常见问题解答

<br>

<details>

<summary><b>如何进行故障排除？</b></summary>

如果在 Visual Studio Code 中遇到 Teams 工具包错误，可以选择 **“获取** 有关错误通知的帮助”转到相关文档。 如果使用的是 TeamsFx CLI，则错误消息末尾会有一个指向帮助文档的超链接。也可以直接查看[预配帮助文档](https://aka.ms/teamsfx-arm-help)。

<br>

</details>

<details>

<summary><b>如何在预配时切换到另一个 Azure 订阅？</b></summary>

1. 在当前帐户中切换订阅或注销并选择新订阅。
2. 如果已预配当前环境，则需要创建新环境并执行预配，因为 ARM 不支持对资源进行移动。
3. 如果未预配当前环境，可以直接触发预配。

<br>

</details>

<details>

<summary><b>如何在预配时更改资源组？</b></summary>

在预配之前，该工具会询问是要创建新的资源组还是使用现有资源组。 你可以在此步骤中提供新的资源组名称或选择现有资源组名称。

<br>

</details>

<details>

<summary><b>如何预配基于 sharepoint 的应用？</b></summary>

可以按照[预配基于 SharePoint 的应用](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4)中的说明操作。

> [!NOTE]
> 目前，使用 Teams 工具包构建采用 Sharepoint 框架的 Teams 应用与 Azure 没有直接集成，文档中的内容不适用于基于 SPFx 的应用。

<br>

</details>
