---
title: 在 Microsoft Teams 中使用协作控件部署应用
author: surbhigupta
description: 在本模块中，了解如何在 Microsoft Teams 中使用协作控制部署应用，以及如何让其他人使用你的应用。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 75a2aa9d09247ac152c31df02f2bb8d4fb507619
ms.sourcegitcommit: c1032ea4f48c4bbf5446798ff7d46d7e6e9f55d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027303"
---
# <a name="deploy-collaboration-controls-to-microsoft-teams"></a>将协作控件部署到 Microsoft Teams

协作控制当前在 Microsoft Teams 中效果最佳。 可以创建一个新应用，该应用可以同时嵌入到 Teams 应用中，即个人应用和选项卡应用。

> [!NOTE]
> 目前，协作控件仅在 [公共开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中可用。

## <a name="configure-the-app-for-teams"></a>为 Teams 配置应用

在 [创建模型驱动](~/samples/app-with-collaboration-controls.md#create-a-model-driven-application) 应用程序时创建的应用只有一个左窗格，没有复杂的命令。 因此，在将应用添加到 Teams 之前，可以隐藏左窗格并创建更易于理解的标头视图。

> [!NOTE]
> 如果要向用户显示左窗格和高密度标头，请勿启用以下步骤。

为此，我们将使用 Power Apps **新应用** 设置。

1. 转到左窗格中的 **“解决方案** ”。

1. 转到解决方案列表的底部，然后选择 **“默认解决方案**”。

1. 搜索并选择 **“设置定义**”。

     :::image type="content" source="../assets/images/collaboration-control/settings-defnition.png" alt-text="设置定义":::

1. 搜索并从设置定义列表中选择 **“隐藏导航栏** ”。 这会隐藏应用程序中的左窗格。

     :::image type="content" source="../assets/images/collaboration-control/hide-the-nav-bar.png" alt-text="隐藏导航栏":::

1. 在编辑窗格中应用程序的右下角，有一个标题为 **“设置应用值”** 的部分。 如果使用新式应用设计器创建了应用，则应用将显示在列表中。 选择 **应用下的新应用值** 。

1. 将值从 **“否** ”更改为 **“是”。**

     :::image type="content" source="../assets/images/collaboration-control/value-to-yes.png" alt-text="将值更改为“是”":::

1. 选择 **“保存”。**

1. 从设置定义列表中搜索并选择 **“应用高密度”页眉** ，然后重复此过程。

     :::image type="content" source="../assets/images/collaboration-control/density-page-header.png" alt-text="密度页眉":::

1. 选择 **“返回到解决方案**”。

     :::image type="content" source="../assets/images/collaboration-control/default-solution.png" alt-text="默认解决方案":::

1. 选择 **“发布所有自定义项** ”以发布已完成的所有工作。

     :::image type="content" source="../assets/images/collaboration-control/publish-cusomization.png" alt-text="发布所有自定义项":::

## <a name="add-the-app-to-microsoft-teams-app-catalog"></a>将应用添加到 Microsoft Teams 应用目录

定义设置后，现在可以将应用添加到 Microsoft Teams。 首先，浏览到 Power Apps maker 门户中的 **“应用** ”页，找到已创建的应用并选择省略号 **...**。

若要将应用添加到 Teams，请选择 **“添加到 Teams**”。

:::image type="content" source="../assets/images/collaboration-control/add-to-teams.png" alt-text="添加到 Teams":::

选择 **“添加到 Teams** ”将打开一个对话框，可在其中查看详细信息并选择 **“下载应用**”，将 Microsoft Teams 应用清单保存到设备。

:::image type="content" source="../assets/images/collaboration-control/colab-manager-inspection.png" alt-text="屏幕截图是显示协作管理器检查的示例":::

若要将应用上传到 Teams，请参阅 [Team 中的上传应用](~/concepts/deploy-and-publish/apps-upload.md)。

## <a name="enable-others-to-use-your-application"></a>让其他人使用应用程序

若要使用户能够运行使用协作控件生成的已部署Collaboration Manager应用程序，需要执行以下操作：

* 创建协作团队
* 将成员添加到团队
* 创建安全角色
* 向团队成员分配安全角色

### <a name="create-a-collaboration-team"></a>创建协作团队

1. 登录 [到 Power Platform 管理中心](https://admin.powerplatform.microsoft.com/environments)。

     1. 选择部署应用的环境。
     1. 选择 **“设置** > **用户** + **”权限**。
     1. 选择 **Teams**。

1. 从页面顶部选择 **“+ 创建团队** ”按钮。

1. 添加所有必需字段：
     1. **团队名称：** 确保名称在业务单元中是唯一的。
     1. **描述：** 输入团队的说明。
     1. **业务部门：** 从下拉列表中选择业务单元。
     1. **管理员：** 通过输入字符在组织内搜索要分配为管理员的用户。
     1. **团队类型：** 选择团队类型。 以下步骤假定你已从下拉列表中选择了“所有者”。 其他团队类型 (Microsoft 365 团队和Microsoft Azure Active Directory团队) 从 Azure Active Directory 自动填充团队成员。

         :::image type="content" source="../assets/images/collaboration-control/new-team.png" alt-text="新团队":::

     1. 请确保记下团队名称。 稍后需要此项才能将此团队分配为记录的所有者。

     1. 选择 **“下一步”。**

### <a name="add-members-to-the-team"></a>将成员添加到团队

> [!NOTE]
> 如果团队类型为 Azure Active Directory 或 Microsoft 365，则不需要向团队添加成员。

1. 选择一个团队，然后选择 **“管理团队成员**”。

1. 若要添加新的团队成员，请选择 **+添加团队成员** ，然后从组织中选择要添加的用户。

     :::image type="content" source="../assets/images/collaboration-control/add-team-members.png" alt-text="屏幕截图介绍如何添加团队成员":::

1. 若要删除团队成员，请选择用户，然后选择 **“删除**”。

### <a name="create-a-security-role"></a>创建安全角色

1. 在部署应用的环境中选择 **“设置** > **用户** + ”**权** 限。

1. 选择 **安全角色**。

     :::image type="content" source="../assets/images/collaboration-control/users-permission.png" alt-text="用户权限":::

1. 选择页面左上角的 **“新建”角色** ，该角色现在将打开一个新页面。

1. 在 **“详细信息”选项卡上**，提供安全角色的名称。

1. 转到 **“自定义实体”** 选项卡。

     1. 为每个协作实体、 **协作映射**、 **协作元** 数据和协作 **根**) 授予组织 (完全绿色圆圈的权限。

         :::image type="content" source="../assets/images/collaboration-control/collab-map.png" alt-text="协作映射":::

1. 选择 **“保存** 并 **关闭**”。

### <a name="assign-security-roles"></a>分配安全角色

1. 在部署应用的环境中选择 **“设置** > **用户** + ”**权** 限。

1. 选择 **Teams**，然后选择在 [创建协作团队时创建的团队](#create-a-collaboration-team)。

1. 从标头中选择 **“管理安全角色** ”。

     :::image type="content" source="../assets/images/collaboration-control/edit-team.png" alt-text="编辑团队":::

1. 选择 [在安全角色中创建的角色](#create-a-security-role)。

1. 选择“**保存**”。

有关角色特权的详细信息，请参阅在 [环境中配置用户安全](/power-platform/admin/database-security)性。
