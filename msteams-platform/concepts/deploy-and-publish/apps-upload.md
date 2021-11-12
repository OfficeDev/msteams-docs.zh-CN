---
title: Upload自定义应用
description: 了解如何在应用中旁加载Microsoft Teams。 在开发期间测试和调试应用时，旁加载很常见。
ms.topic: how-to
author: KirtiPereira
ms.author: surbhigupta
ms.localizationpriority: none
ms.openlocfilehash: e14e521941d253a3f259cf93f36bff4d620d55f2
ms.sourcegitcommit: 1431dfe08d5a19a63dbf1542a2e6c661e4dd7fc1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2021
ms.locfileid: "60949059"
---
# <a name="upload-your-app-in-microsoft-teams"></a>Upload应用中Microsoft Teams

你可以旁加载Microsoft Teams应用，而无需发布到你的组织或Teams应用商店。 在下列情况下，这是有意义的：

* 你想要自己或与其他开发人员一起在本地测试和调试应用。
* 你只为自己生成了一个应用。 例如，自动化工作流。
* 你为一小组用户（如工作组）生成了一个应用。

> [!IMPORTANT]
> 目前，旁加载应用在 政府社区云 (GCC) 中可用，但不适用于 GCC-High 和国防部 (DOD) 。

## <a name="prerequisites"></a>先决条件

* 创建[应用包并](~/concepts/build-and-test/apps-package.md)[验证其](https://dev.teams.microsoft.com/appvalidation.html)是否出错。
* [在应用中启用自定义](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)Teams。
* 确保你的应用正在运行，并且可通过 HTTPs 访问。

## <a name="upload-your-app"></a>上传应用

你可以将应用旁加载至团队、聊天、会议或个人使用，具体取决于你配置应用的范围。

1. 使用你的Teams帐户登录到[Microsoft 365 客户端](~/build-your-first-app/build-and-run.md#prerequisites)。
1. 选择 **"** 应用 **"，Upload自定义应用"。**
1. 选择应用包.zip文件。 将显示安装对话框。
:::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="Screenshot showing an example of a Teams app install dialog.":::
1. 将应用添加到Teams。

## <a name="troubleshoot-upload-issues"></a>上传问题疑难解答

如果应用无法旁加载，请执行下列操作，直到问题解决：

1. 返回创建应用 [包的说明](../../concepts/build-and-test/apps-package.md)。
1. [再次验证应用](https://dev.teams.microsoft.com/appvalidation.html) 包。
1. 确保你的应用清单与最新的架构 [匹配](../../resources/schema/manifest-schema.md)。

## <a name="access-your-app"></a>访问应用

Teams提供了多种打开应用的方法。 有关详细信息，请参阅访问[Teams 中的应用](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a)。

## <a name="update-your-app"></a>更新应用

如果你更改了代码，则不必再次旁加载你的应用 (这些更改Teams实时) 。 但是，如果更改任何应用配置，则必须重新安装。

## <a name="remove-your-app"></a>删除应用

若要删除你的应用，请右键单击应用中Teams **并选择卸载**。

> [!NOTE]
> 你无法完全删除个人自动程序活动。 如果删除应用并再次添加它，则与机器人的新通信将附加到其上一次对话中。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [使用Teams应用](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)

## <a name="see-also"></a>另请参阅

* [配置默认安装选项](~/concepts/deploy-and-publish/add-default-install-scope.md)
* [维护已发布Microsoft Teams应用程序](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)
