---
title: 启用要自定义的应用
author: heath-hamilton
description: 了解Teams如何为组织自定义你的应用。
ms.localizationpriority: medium
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 193b4baeee16badb1dcb26139831d3e298de9a5c
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155320"
---
# <a name="enable-your-microsoft-teams-app-to-be-customized"></a>启用Microsoft Teams自定义应用

你可以允许客户在管理中心Microsoft Teams应用的某些Teams方面。 只有发布到应用商店的应用才支持Teams此功能。 无法自定义为组织发布的旁加载应用。

此功能的一些可能示例包括：

* 更改应用主题色以匹配组织品牌。
* 将应用程序名称从 *Contoso* 更新到 *Contoso 代理*，这是组织中的用户将看到的名称。  (注意：向聊天或频道添加连接器的用户仍将看到原始应用名称 *Contoso*.) 

可以在开发人员门户中启用此功能[Teams。](https://dev.teams.microsoft.com/home) 这将配置 `configurableProperties` ，此配置在 1.10 之前的版本中Teams清单。

## <a name="test-your-app"></a>测试应用

在开发期间，你无法测试此功能。 旁加载或发布到组织的应用程序目录时，不支持应用自定义。

## <a name="user-considerations"></a>用户注意事项

为特别需要 (应用的Teams管理员) 提供指南。 有关详细信息，请参阅自定义[Teams。](/MicrosoftTeams/customize-apps)

## <a name="see-also"></a>另请参阅

* [在管理中心Teams应用](/MicrosoftTeams/customize-apps)
