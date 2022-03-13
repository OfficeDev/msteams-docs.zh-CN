---
title: 上传自定义应用
description: 了解如何在 Microsoft Teams 中旁加载应用。 在开发过程中测试和调试应用时，旁加载很常见。
ms.topic: how-to
author: surbhigupta
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: e3a22378819d8fb1e865e2122b7977bcbabbbb74
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453327"
---
# <a name="upload-your-app-in-microsoft-teams"></a>在 Microsoft Teams 中上传应用

在以下情况下，无需发布到组织或 Teams 应用商店即可旁加载 Microsoft Teams 应用：

* 你希望自己或与其他开发人员一起在本地测试和调试应用。
* 你为自己构建了一个应用来自动执行工作流。
* 你为一小部分用户 (例如你的工作组) 构建了一个应用。

> [!IMPORTANT]
> 目前，旁加载应用在政府社区云 (GCC) 中可用，但不适用于 GCC-High 和国防部 (DOD)。

## <a name="prerequisites"></a>先决条件

* 请确保创建[应用包](~/concepts/build-and-test/apps-package.md)，并[验证其](https://dev.teams.microsoft.com/appvalidation.html)是否存在错误。
* 在 Teams 中 [启用自定义应用上传](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。
* 确保应用正在运行并可使用 HTTPs 进行访问。

## <a name="upload-your-app"></a>上传应用

可以将应用旁加载到团队、聊天、会议或个人使用，具体取决于应用范围的配置方式。

1. 使用你的 [Microsoft 365开发帐户](~/build-your-first-app/build-and-run.md#prerequisites) 登录到 Teams 客户端。
1. 选择“**应用**”，然后选择“**管理应用**”。
1. 选择“**上传自定义应用**”。
1. 选择应用包 .zip 文件，将显示以下屏幕：

    :::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="显示 Teams 应用安装对话框示例的屏幕截图。":::

1. 选择“**添加**”将应用添加到 Teams。

    > [!NOTE]
    > `onInstallationUpdateActivityAsync()`方法用于获取 Microsoft Teams 区域设置，同时将机器人添加到Microsoft Teams。

## <a name="troubleshooting"></a>疑难解答

如果应用无法旁加载或上传遇到问题，请检查以下选项：

1. 确保已按照[创建应用包](../../concepts/build-and-test/apps-package.md)的所有说明进行操作。
1. [验证应用包](https://dev.teams.microsoft.com/appvalidation.html)。
1. 确保应用清单与最新的 [架构](../../resources/schema/manifest-schema.md)匹配。

## <a name="access-your-app"></a>访问你的应用

Teams 提供了几种打开应用的方法。 有关详细信息，请参阅 [在 Teams 中访问应用](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a)。

## <a name="update-your-app"></a>更新应用

如果进行代码更改 (这些更改已实时反映在 Teams 中)，则无需再次旁加载应用。 但是，如果更改了任何应用配置，则必须重新安装。

## <a name="remove-your-app"></a>删除应用

若要删除应用，请右键单击 Teams 中的应用图标，然后选择 **卸载**。

> [!NOTE]
> 不能完全删除个人机器人活动。如果删除并再次添加该应用，则与机器人的新通信将追加到与该应用的上一个对话中。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 Teams 应用](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)

## <a name="see-also"></a>另请参阅

* [配置默认安装选项](~/concepts/deploy-and-publish/add-default-install-scope.md)
* [维护已发布的 Microsoft Teams 应用](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)
