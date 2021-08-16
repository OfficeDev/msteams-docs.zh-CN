---
title: 启用要自定义的应用
author: heath-hamilton
description: 了解Teams管理员如何为组织自定义你的应用。
localization_priority: Normal
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 0af96eebb50aeb650cdd5a1b3bd6a93439fb57b8
ms.sourcegitcommit: 2c4c77dc8344f2fab8ed7a3f7155f15f0dd6a5ce
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "58345563"
---
# <a name="enable-your-microsoft-teams-app-to-be-customized"></a>启用Microsoft Teams自定义应用

你可以允许客户在管理中心内自定义Microsoft Teams应用的Teams方面。 只有发布到应用商店的应用才支持Teams此功能。 无法自定义为组织发布的旁加载应用。

> [!IMPORTANT]
> 目前，旁加载应用在 政府社区云 (GCC) 中可用，但不适用于 GCC-High 和国防部 (DOD) 。

此功能的一些可能示例包括：

* 更改应用主题色以匹配组织品牌。
* 将应用程序名称从 *Contoso* 更新到 *Contoso 代理*，这是组织中的用户将看到的名称。  (注意：向聊天或频道添加连接器的用户仍将看到原始应用名称 *Contoso*.) 

可以在开发人员门户中启用此功能[Teams。](https://dev.teams.microsoft.com/home) 这将配置 `configurableProperties` ，在应用清单 1.10 之前的版本中Teams可用。

## <a name="test-your-app"></a>测试应用

无法在开发期间测试此功能。 不支持将应用自定义项旁加载或发布到组织的应用程序目录。

## <a name="user-considerations"></a>用户注意事项

作为应用发布者，向管理员中的客户提供Teams信息：
* 包括一条注释，建议在测试租户中Teams自定义更改，然后再更改其生产环境。 
* 提供如何自定义应用的最佳方案。

## <a name="see-also"></a>另请参阅

* [在管理中心Teams应用](/MicrosoftTeams/customize-apps)
