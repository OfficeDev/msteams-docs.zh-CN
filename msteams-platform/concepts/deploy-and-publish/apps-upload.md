---
title: 上传自定义应用
description: 了解如何在 Microsoft Teams 中旁加载应用。 在开发过程中测试和调试应用时，旁加载很常见。
ms.topic: how-to
author: surbhigupta
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: ab833f3472091d6727ad584c923a83cae2842c0c
ms.sourcegitcommit: 024be23411bc0f2573d19f48f9266021f9b76f0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2022
ms.locfileid: "67488283"
---
# <a name="upload-your-app-in-teams"></a>在 Teams 中上传应用

在以下情况下，无需发布到组织或 Teams 应用商店即可旁加载 Microsoft Teams 应用：

* 你希望自己或与其他开发人员一起在本地测试和调试应用。
* 你为自己构建了一个应用来自动执行工作流。
* 你为一小部分用户 (例如你的工作组) 构建了一个应用。

> [!NOTE]
> 多次旁加载应用会显示消息传递扩展的多个实例。

> [!IMPORTANT]
>
> * 目前，仅在政府社区云 (GCC) 中可以旁加载应用，GCC-High和国防部 (DOD) 中无法旁加载应用。
> * 仅 Teams 桌面应用支持应用安装。

## <a name="prerequisites"></a>先决条件

* 请确保创建[应用包](~/concepts/build-and-test/apps-package.md)，并[验证其](https://dev.teams.microsoft.com/appvalidation.html)是否存在错误。
* 在 Teams 中 [启用自定义应用上传](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。
* 确保应用正在运行并可使用 HTTPs 进行访问。

## <a name="upload-your-app"></a>上传应用

可以将应用旁加载到团队、聊天、会议或个人使用，具体取决于应用范围的配置方式。

1. 使用你的 [Microsoft 365开发帐户](https://developer.microsoft.com/en-us/microsoft-365/dev-program) 登录到 Teams 客户端。
1. 选择“**应用**” > “**管理应用**”和“**发布应用**”。

    :::image type="content" source="~/assets/images/publish-app/manage-apps.png" alt-text="发布应用":::

1. 选择“**上传自定义应用**”。

   :::image type="content" source="~/assets/images/publish-app/publish-app.png" alt-text="上传自定义应用":::

1. 选择应用包 .zip 文件。
1. 根据要求将应用添加到 Teams:</br>

   a. 选择 **添加** 以添加个人应用。</br> b. 使用下拉菜单将应用添加到团队或聊天中。

    :::image type="content" source="~/assets/images/publish-app/teams-app-detail.png" alt-text="应用说明":::

## <a name="troubleshoot"></a>排除故障

如果应用无法旁加载或上传遇到问题，请检查以下选项：

1. 确保已按照[创建应用包](../../concepts/build-and-test/apps-package.md)的所有说明进行操作。
1. [验证应用包](https://dev.teams.microsoft.com/appvalidation.html)。
1. 确保应用清单与最新的 [架构](../../resources/schema/manifest-schema.md)匹配。

## <a name="manage-your-apps"></a>管理应用

通过管理应用，用户可以在 Teams 客户端上专门管理、更新和删除其应用、权限和订阅。用户可以从 **管理应用** 中安装应用。

### <a name="access-your-app"></a>访问你的应用

要通过“**管理应用**”访问应用，请按照以下步骤操作：

1. 转到“**应用**”，然后在 Teams 中选择“**管理应用**”以查看所有频道中安装的应用或以列表格式供个人使用。

    :::image type="content" source="~/assets/images/publish-app/manage-apps-list.png" alt-text="访问团队应用列表":::

1. 选择应用下拉列表以查看安装应用的所有范围。

    :::image type="content" source="~/assets/images/publish-app/app-scopes.png" alt-text="访问团队应用范围":::

1. 选择应用范围以转到频道或个人视图中的应用。 范围列表仅包含个人范围和团队范围。 群聊范围内安装的应用当前不显示在此视图中。

Teams 提供了几种打开应用的方法。 有关详细信息，请参阅 [在 Teams 中访问应用](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a)。

### <a name="update-your-app"></a>更新应用

如果进行代码更改 (这些更改已实时反映在 Teams 中)，则无需再次旁加载应用。 但是，如果更改了任何应用配置，则必须重新安装。

如果应用有可用更新，则启用“**更新可用**”选项。 如果要更新，请按照以下步骤操作：

1. 选择“**更新可用**”以查看更新。

     :::image type="content" source="~/assets/images/publish-app/update-available.png" alt-text="更新 Teams 应用。":::

1. 选择“**查看更新**”，将显示具有更新选项的窗口。
1. 选择“**更新**”按钮以更新应用。

     :::image type="content" source="~/assets/images/publish-app/update-window.png" alt-text="在管理应用中更新 Teams 应用。":::

     :::image type="content" source="~/assets/images/publish-app/updated-app.png" alt-text="已更新的应用。":::

### <a name="remove-your-app"></a>删除应用

要从 Teams 中删除应用，请按照以下步骤操作：

1. 在“**管理应用**”中查找应用。

1. 在已安装应用的范围内选择&nbsp;“:::image type="content" source="~/assets/images/publish-app/bin-icon.png" alt-text="在 Teams 中删除应用":::”&nbsp;。

    :::image type="content" source="~/assets/images/publish-app/uninstall-from-channel.png" alt-text="在频道中删除应用。":::

1. 选择“**删除**”以删除应用。

    :::image type="content" source="~/assets/images/publish-app/remove-app-teams.png" alt-text="从 Teams 中删除应用。":::

> [!NOTE]
>
> * 不能完全删除个人机器人活动。如果删除并再次添加该应用，则与机器人的新通信将追加到与该应用的上一个对话中。
> * 目前，无法将自定义应用迁移到 Teams 应用商店。 若要将应用列到 Teams 应用商店中，请参阅 [将应用发布到 Microsoft Teams 应用商店](appsource/publish.md)。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
>[创建适用于 Teams 会议的应用](../../apps-in-teams-meetings/teams-apps-in-meetings.md)

## <a name="see-also"></a>另请参阅

* [配置默认安装选项](~/concepts/deploy-and-publish/add-default-install-scope.md)
* [维护已发布的 Microsoft Teams 应用](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)
* [将应用添加到聊天](/graph/api/chat-post-installedapps)
