---
title: 自定义 Teams 应用
author: heath-hamilton
description: 了解 Teams 管理员如何为其组织自定义应用。
ms.localizationpriority: high
ms.author: surbhigupta
ms.topic: overview
keywords: 主题色, 品牌, 隐藏应用, 审批
ms.openlocfilehash: 4728e6f34680d51983558d1ad96c47ffe3650234
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111197"
---
# <a name="customize-your-teams-app"></a>自定义 Teams 应用

## <a name="enable-your-microsoft-teams-app-to-be-customized"></a>允许自定义你的 Microsoft Team 应用

你可以允许客户在 Teams 管理中心自定义 Microsoft Teams 应用的某些方面。 此功能仅支持发布到 Teams 应用商店的应用。 无法自定义旁加载的应用和为组织发布的应用。

此功能的一些可能示例包括：

* 更改应用的主题色以匹配组织品牌形象。
* 将应用名称从 *Contoso* 更新为 *Contoso Agent*，这是组织中用户将看到的名称。 （注意：将连接器添加到聊天或频道的用户仍会看到原始应用名称，即 *Contoso*。）

你可以在 [Teams 开发人员门户](https://dev.teams.microsoft.com/home)中启用此功能。 这会配置 `configurableProperties`，这在 Teams 应用清单 1.10 之前的版本中不可用。

### <a name="test-your-app"></a>测试应用

开发过程中无法测试此功能。 旁加载或发布到组织应用目录时，不支持自定义应用。

### <a name="user-considerations"></a>用户注意事项

为想要自定义应用的客户（特别是 Teams 管理员）提供指南。 有关详细信息，请参阅[在 Teams 中自定义应用](/MicrosoftTeams/customize-apps)。

## <a name="hide-teams-app-until-admin-approves"></a>隐藏 Teams 应用，直到管理员批准

为了增强 Teams 应用体验，默认情况下可以对用户隐藏应用，直到管理员允许取消隐藏应用。 例如，Contoso Electronics 为 Teams 创建了一个技术支持应用。 为了使该应用能够正常运行，Contoso Electronics 希望客户先设置应用的特定属性。 默认情况下，该应用处于隐藏状态，并且仅在管理员允许后才可供用户使用。

> [!NOTE]
> Teams 应用商店已演变:
> 
> 以前，LOB 应用是通过选择磁贴上的省略号来更新的。 借助更新的 Teams 应用商店体验，现在可以通过登录到 [Teams 管理中心](https://admin.teams.microsoft.com) 来更新 LOB 应用。

若要隐藏应用，请在应用清单文件中将 `defaultBlockUntilAdminAction` 属性设置为 `true`。 当属性设置为 `true` 时，在 Teams 管理中心>“**管理应用**”中，“**已被发布者阻止**”会显示在应用的“**状态**”中：

![管理已被发布者阻止的应用](../../assets/images/apps-in-meetings/manageappsblockedapps.png)

在用户能够访问应用之前，管理员会收到采取操作的请求。 在“**管理应用**”下，管理员可以选择“**允许**”以允许具有“**已被发布者阻止**”状态的应用：

![管理应用](../../assets/images/apps-in-meetings/manageapp.png)

如果默认情况下不希望应用被隐藏，则可以将 `defaultBlockUntilAdminAction` 属性更新为 `false`。 当新版本的应用获得批准时，默认情况下，只要管理员未采取任何显式操作，就会允许该应用。

> [!NOTE]
> LOB 应用不支持 `defaultBlockUntilAdminAction`。 如果使用此属性上传 LOB 应用，则不会阻止该应用。

## <a name="see-also"></a>另请参阅

* [应用程序清单架构](/microsoftteams/platform/resources/schema/manifest-schema)
* [在 Teams 管理中心自定义应用](/MicrosoftTeams/customize-apps)