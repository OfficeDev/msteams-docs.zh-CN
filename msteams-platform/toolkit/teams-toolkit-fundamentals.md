---
title: Teams 工具包概述
author: zyxiaoyuer
description: 在本模块中，了解 Teams 工具包、Teams 工具包的安装和 Teams 工具包的用户旅程
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: cb3508bdd22f9d05c48e71b1b90ec4ffbf4c56af
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833161"
---
# <a name="teams-toolkit-overview"></a>Teams 工具包概述

借助 Teams 工具包，可以轻松开始使用 Visual Studio 和 Visual Studio Code 为 Microsoft Teams 开发应用。

* 从项目模板或示例开始。
* 通过自动应用注册和配置节省设置时间。
* 直接从熟悉的工具运行和调试 Teams。
* 使用基础结构即代码和 Bicep 在 Azure 中托管的智能默认值。
* 使用环境功能创建独特的配置，例如开发、测试和生产。
* 使用内置发布工具将应用引入组织或 Teams App Store。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png" alt-text="Teams 工具包的用户旅程" lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png":::

## <a name="available-for-visual-studio-and-visual-studio-code"></a>适用于 Visual Studio 和 Visual Studio Code

Teams 工具包对Visual Studio Code免费提供，并支持 Visual Studio 2022 社区版、专业版和企业版。 有关安装和设置的详细信息，请访问 [安装 Teams 工具包文档](./install-Teams-Toolkit.md) 。

| Teams 工具包 | Visual Studio | Visual Studio Code |
| - | ------------- | ------------------ |
| 安装 | 在Visual Studio 安装程序中可用 | 在 VS 市场中可用 |
| 使用 生成 | C#、.NET、ASP.NET、Blazor | JavaScript、TypeScript、React、SPFx |

## <a name="features"></a>功能

### <a name="project-templates"></a>项目模板

Teams 工具包降低了常见业务线应用方案和智能默认值模板入门的复杂性，从而缩短了生产时间。 如果你已经熟悉 Teams 应用开发，也可以直接从以功能为中心的模板开始。 即选项卡、机器人、消息传递扩展。

::: zone pivot="visual-studio-code"
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create-new-app.png" alt-text="在 VS Code 中创建新的 Teams 应用菜单":::
::: zone-end

::: zone pivot="visual-studio"
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create-new-app-vs.png" alt-text="在 VS Code 中创建新的 Teams 应用菜单":::
::: zone-end

### <a name="automatic-registration-and-configuration"></a>自动注册和配置

节省时间，让工具包在 Teams 开发人员门户中自动注册应用，并在首次运行或调试应用时自动配置 Azure Active Directory 等设置。 使用 Microsoft 365 帐户登录，以控制配置应用的位置，并在需要更多灵活性时自定义包含的 Azure AD 清单。

::: zone pivot="visual-studio-code"

### <a name="multiple-environments"></a>多个环境

借助环境功能，可以创建不同的云资源分组，以便更轻松地运行和测试应用。 将“开发”环境与 Azure 订阅配合使用，或者创建具有不同订阅的新环境，用于过渡、测试和生产。

### <a name="quick-access-to-teams-developer-portal"></a>快速访问 Teams 开发人员门户

快速访问 Teams 开发人员门户，可在其中配置、分发和管理应用。 有关详细信息，请参阅 [使用开发人员门户管理 Teams 应用](../concepts/build-and-test/manage-your-apps-in-developer-portal.md)。

:::image type="content" source="../assets/images/teams-toolkit-v2/build-environment-developer-portal-1.png" alt-text="开发人员门户":::

::: zone-end

::: zone pivot="visual-studio"

#### <a name="teamsfx-net-sdk-reference-docs"></a>TeamsFx .NET SDK 参考文档

* [Microsoft.Extensions.DependencyInjection 命名空间](/../dotnet/api/Microsoft.Extensions.DependencyInjection)
* [Microsoft.TeamsFx 命名空间](/../dotnet/api/Microsoft.TeamsFx)
* [Microsoft.TeamsFx.Configuration 命名空间](/../dotnet/api/Microsoft.TeamsFx.Configuration)
* [Microsoft.TeamsFx.Conversation 命名空间](/../dotnet/api/Microsoft.TeamsFx.Conversation)
* [Microsoft.TeamsFx.Helper 命名空间](/../dotnet/api/Microsoft.TeamsFx.Helper)

::: zone-end

## <a name="see-also"></a>另请参阅

* [在 Visual Studio 中创建新的 Teams 应用](create-new-project.md)
* [使用 Visual Studio 预配云资源](provision-cloud-resources.md)
* [使用 Visual Studio 将 Teams 应用部署到云](deploy.md)
