---
title: 启用要自定义的应用
author: heath-hamilton
description: 了解Teams如何为组织自定义你的应用。
localization_priority: Normal
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: bf1b43629c87dd4123520c634772e5dea14e0bb5
ms.sourcegitcommit: 64c1cf2a268ef101a519bc31d171618d0f6cd12a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2021
ms.locfileid: "52915081"
---
# <a name="enable-your-microsoft-teams-app-to-be-customized"></a>启用Microsoft Teams自定义应用

你可以允许客户在管理中心中Microsoft Teams应用的某些Teams方面。 仅发布到应用商店的应用支持Teams此功能。 无法自定义为组织发布的旁加载应用。

此功能的一些可能示例包括：

* 更改应用主题色以匹配组织品牌。
* 将应用程序名称从 *Contoso* 更新到 *Contoso 代理*，这是组织中的用户将看到的名称。  (注意：向聊天或频道添加连接器的用户仍将看到原始应用名称 *Contoso*.) 

可以在开发人员门户中启用此功能[Teams。](https://dev.teams.microsoft.com/home) 这将配置 `configurableProperties` ，这不适用于 1.10 之前版本的应用Teams清单。

## <a name="test-your-app"></a>测试应用

无法在开发期间测试此功能。 不支持将应用自定义项旁加载或发布到组织的应用程序目录。

## <a name="user-considerations"></a>用户注意事项

作为应用发布者，向管理员中的客户提供Teams信息：
* 包括一条注释，建议在测试租户中测试Teams更改，然后再更改其生产环境。 
* 提供如何自定义应用的最佳方案。

## <a name="see-also"></a>另请参阅

* [在管理中心Teams应用](/MicrosoftTeams/customize-apps)
