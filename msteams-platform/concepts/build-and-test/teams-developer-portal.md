---
title: Teams 开发人员门户
description: 在本文中，详细了解开发人员门户以及如何在 Teams 开发人员门户中创建全新应用和导入现有应用。
ms.localizationpriority: medium
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: b0619fc328e6bc30decfe5868692281037489654
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615133"
---
# <a name="developer-portal-for-teams"></a>Teams 开发人员门户

<a href="https://dev.teams.microsoft.com" target="_blank">Teams 开发人员门户</a>是配置、分发和管理 Microsoft Teams 应用的主要工具。 借助开发人员门户，你可以在应用上与同事协作、设置运行时环境等。

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="屏幕截图是显示 Teams 开发人员门户主页的示例。":::

> [!NOTE]
>
> * 目前，开发人员门户不适用于政府社区云 (GCC) -High 或国防部 (DOD) 租户。
> * 但是，可以使用常规租户在开发人员门户中构建应用、下载应用，并使用 [Microsoft Graph](/graph/api/teamsapp-publish?view=graph-rest-1.0&tabs=http&preserve-view=true) 将应用上传到国家云。 有关详细信息，请参阅[国家云部署](/graph/deployments)。

## <a name="register-an-app"></a>注册应用

开发人员门户提供以下注册 Teams 应用的方法：

* 创建并注册全新的应用。
* 导入现有应用包。

### <a name="create-and-register-a-brand-new-app"></a>创建和注册全新的应用

开发人员门户允许你创建全新的应用：

1. 登录到 [开发人员门户](https://dev.teams.microsoft.com)，从左窗格中选择 **“应用** ”。

   :::image type="content" source="../../assets/images/tdp/home-page.png" alt-text="屏幕截图是显示 Teams 开发人员门户主页的示例。":::

1. 选择 **“新建应用** ”并输入应用名称。

   :::image type="content" source="../../assets/images/tdp/enter-app-name-tdp.png" alt-text="屏幕截图显示了如何在 Teams 开发人员门户中创建全新的应用。" lightbox="../../assets/images/tdp/create-new-app-in-tdp.png":::

1. 选择“**添加**”。

现在，你已成功创建了一个全新的应用，可以看到新应用的所有基本信息。

:::image type="content" source="../../assets/images/tdp/basic-information-app-tdp.png" alt-text="屏幕截图是一个示例，其中显示了在 Teams 开发人员门户中创建的应用的基本信息。":::

### <a name="import-an-existing-app"></a>导入现有应用

按照步骤在开发人员门户中导入和管理现有应用。

1. 在开发人员门户中，从左窗格中选择 **“应用** ”。
1. 选择 **“导入应用**”。

   :::image type="content" source="../../assets/images/tdp/import-app.png" alt-text="屏幕截图显示如何在 Teams 开发人员门户中导入现有应用以管理应用。":::

1. 选择应用清单文件，然后选择 **“打开**”。
1. 选择“**导入**”。

> [!NOTE]
>
> * 开发人员门户创建唯一的应用 ID，并锁定已注册 Teams 应用的 ID。 无法编辑或提供所选 ID，这可防止多个应用具有重复的应用 ID。
> * 如果使用适用于Visual Studio Code的 Microsoft Teams 工具包创建应用，则可以在开发人员门户中管理应用。 有关详细信息，请参阅 [使用团队工具包和 Visual Studio 代码生成应用](~/toolkit/visual-studio-code-overview.md)。
> * 可以将在 App Studio 上创建的现有应用导入开发人员门户。

## <a name="see-also"></a>另请参阅

[Microsoft Teams 应用随附 SaaS 产品/服务](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
