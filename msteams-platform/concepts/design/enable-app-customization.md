---
title: 启用应用自定义并阻止应用，直至管理员允许
author: heath-hamilton
description: 在本模块中，了解 Teams 管理员如何为其组织自定义 Teams 应用，并在管理员批准之前隐藏 Teams 应用。
ms.localizationpriority: medium
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 7d71e341bd1613e9efe6c900f29e1bd340006b49
ms.sourcegitcommit: d92e14fad6567fe91fd52ee6c213836740316683
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2022
ms.locfileid: "67604950"
---
# <a name="enable-app-customization-and-block-apps-till-admin-allows"></a>启用应用自定义并阻止应用，直至管理员允许

Microsoft Teams 允许管理员自定义 Teams 应用，以增强应用商店体验并保留其组织的品牌。 应用开发人员可以允许 Teams 管理员自定义其应用。有关详细信息，请参阅 [Teams 管理中心中的自定义应用](/MicrosoftTeams/customize-apps)。

## <a name="enable-customization-for-your-microsoft-teams-app"></a>为 Microsoft Teams 应用启用自定义

你可以允许客户在 Teams 管理中心自定义 Microsoft Teams 应用的某些方面。 此功能仅支持发布到 Teams 应用商店的应用。 无法自定义旁加载的应用和为组织发布的应用。

此功能的一些可能示例包括：

* 更改应用的主题色以匹配组织品牌形象。
* 将应用名称从 *Contoso* 更新为 *Contoso Agent*，这是组织中用户将看到的名称。
（注意：将连接器添加到聊天或频道的用户仍会看到原始应用名称，即 *Contoso*。）

可以从版本 1.11 开始，通过定义客户可在 [Teams 应用清单部分中`configurableProperties`](/microsoftteams/platform/resources/schema/manifest-schema#configurableproperties)自定义的应用属性来启用此功能。 如果选择使用开发人员门户编辑应用的清单，则可以在 Teams 开发人员 [门户](https://dev.teams.microsoft.com/home) 中完成此操作。

> [!IMPORTANT]
> 开发过程中无法测试此功能。 旁加载或发布到组织应用目录时，不支持自定义应用。

### <a name="user-considerations"></a>用户注意事项

为想要自定义应用的客户（特别是 Teams 管理员）提供指南。 有关详细信息，请参阅[在 Teams 中自定义应用](/MicrosoftTeams/customize-apps)。

## <a name="block-apps-by-default-for-users-until-an-admin-approves"></a>默认情况下阻止用户的应用，直到管理员批准

为了增强 Teams 应用体验，默认情况下可以对用户隐藏应用，直到管理员允许取消隐藏应用。 例如，Contoso Electronics 为 Teams 创建了一个技术支持应用。 为了使该应用能够正常运行，Contoso Electronics 希望客户先设置应用的特定属性。 默认情况下，该应用处于隐藏状态，并且仅在管理员允许后才可供用户使用。

若要隐藏应用，请在应用清单文件中将 `defaultBlockUntilAdminAction` 属性设置为 `true`。 当属性设置为 `true` 时，在 Teams 管理中心>“**管理应用**”中，“**已被发布者阻止**”会显示在应用的“**状态**”中：

:::image type="content" source="../../assets/images/manage-apps-status.png" alt-text="屏幕截图是显示被发布者阻止的应用的示例。" lightbox="../../assets/images/manage-apps-status-expanded.png":::

在用户能够访问应用之前，管理员会收到采取操作的请求。 在“**管理应用**”下，管理员可以选择“**允许**”以允许具有“**已被发布者阻止**”状态的应用：

:::image type="content" source="../../assets/images/manage-apps-allow.png" alt-text="屏幕截图是一个示例，其中显示了发布者阻止的应用的允许选项。" lightbox="../../assets/images/manage-apps-allow-expanded.png":::

如果默认情况下不希望应用被隐藏，则可以将 `defaultBlockUntilAdminAction` 属性更新为 `false`。 当新版本的应用获得批准时，默认情况下，只要管理员未采取任何显式操作，就会允许该应用。

> [!NOTE]
> 对于 LOB 应用， `defaultBlockUntilAdminAction` 不受支持。 如果使用此属性上传 LOB 应用，则不会阻止该应用。

## <a name="see-also"></a>另请参阅

* [应用程序清单架构](/microsoftteams/platform/resources/schema/manifest-schema)
* [在 Teams 管理中心自定义应用](/MicrosoftTeams/customize-apps)
