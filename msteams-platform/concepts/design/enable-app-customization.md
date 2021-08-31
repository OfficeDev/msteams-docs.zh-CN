---
title: 启用要自定义的应用
author: heath-hamilton
description: 了解Teams如何为组织自定义你的应用。
localization_priority: Normal
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: ffc429d3dee0ab05e65951233b60ec17ae659b0e
ms.sourcegitcommit: 306b6e8cb3aac8bfda10ef3999467a797d64539d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2021
ms.locfileid: "58408662"
---
# <a name="enable-your-microsoft-teams-app-to-be-customized"></a>启用Microsoft Teams自定义应用

你可以允许客户在管理中心中Microsoft Teams应用的某些Teams方面。 只有发布到应用商店的应用才支持Teams此功能。 无法自定义为组织发布的旁加载应用。

此功能的一些可能示例包括：

* 更改应用主题色以匹配组织品牌。
* 将应用程序名称从 *Contoso* 更新到 *Contoso 代理*，这是组织中的用户将看到的名称。  (注意：向聊天或频道添加连接器的用户仍将看到原始应用名称 *Contoso*.) 

可以在开发人员门户中启用此功能[Teams。](https://dev.teams.microsoft.com/home) 这将配置 `configurableProperties` ，它不适用于 1.10 之前版本的应用Teams清单。

## <a name="test-your-app"></a>测试应用

在开发期间，你无法测试此功能。 旁加载或发布到组织的应用程序目录时，不支持应用自定义。

## <a name="user-considerations"></a>用户注意事项

为特别需要 (应用的Teams管理员) 提供指南。 有关详细信息，请参阅自定义[应用程序中Teams。](/MicrosoftTeams/customize-apps)

## <a name="see-also"></a>另请参阅

* [在管理中心Teams应用](/MicrosoftTeams/customize-apps)
