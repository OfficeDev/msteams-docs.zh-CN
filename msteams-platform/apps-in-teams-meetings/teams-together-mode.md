---
title: 自定义一起模式场景
description: 使用自定义一起模式场景
ms.topic: conceptual
ms.openlocfilehash: 9b65a0ff32c2f895cd0330f49d985ba48369dccf
ms.sourcegitcommit: 3560ee1619e3ab6483a250f1d7f2ceb69353b2dc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2021
ms.locfileid: "53335373"
---
# <a name="custom-together-mode-scenes-in-teams"></a>在 Teams 中自定义同框场景模式

> [!NOTE]
> 此功能目前仅适用于公共 [开发人员预览](../resources/dev-preview/developer-preview-intro.md) 版。

Microsoft Teams中的自定义一起模式场景提供了一个沉浸式且极具吸引力的会议环境，将人们汇集在一起，并鼓励他们打开视频。 它以数字方式将参与者合并到单个虚拟场景，将其视频流放入场景创建者设计和修复的预定席位中。

> [!VIDEO https://www.youtube-nocookie.com/embed/MGsNmYKgeTA]

自定义一起模式场景中的场景是场景开发人员使用 Microsoft Scene studio 创建的项目。 在构想的场景设置中，参与者具有指定席位，视频流呈现在这些座位中。

> [!NOTE]
> 建议仅场景应用，因为此类应用的获取体验更加无缝。

以下过程概述了如何创建仅场景应用：

:::image type="content" source="../assets/images/apps-in-meetings/create-together-mode-scene-flow.png" alt-text="仅创建场景应用" border="false":::

> [!NOTE]
> * 仅场景应用仍然是应用中Microsoft Teams。 Scene studio 在后台处理应用包创建。
> * 单个应用包中的多个场景显示为简单列表场景的一部分。

## <a name="prerequisites"></a>先决条件

你必须对以下内容有基本的了解，以使用自定义"共同模式"场景：

* 场景中场景和座位的定义。
* 拥有 Microsoft 开发人员帐户，并熟悉 Microsoft Teams[门户和](../concepts/build-and-test/teams-developer-portal.md)App Studio。
* [应用旁加载的概念](../concepts/deploy-and-publish/apps-upload.md)。
* 确保管理员已授予访问自定义Upload **以及** 分别选择所有筛选器作为应用设置和会议策略的一部分的权限。

## <a name="best-practices"></a>最佳做法

在生成场景之前，请考虑以下事项，以打造无缝的场景生成体验：

* 确保所有图像都采用 PNG 格式。
* 确保所有图像组合在一起的最终程序包的分辨率不得超过 1920x1080。

    > [!NOTE]
    > 分辨率为一个数。 这是场景成功照明的要求。

* 确保最大场景大小为 10 MB。
* 确保每个图像的最大大小为 5 MB。

    > [!NOTE]
    > * 场景是多个图像的集合。 限制针对每个单独图像。
    > * 单个图像分辨率也必须是一个数。
  
* 如果图像 **是透明的** ，请确保选中"透明"复选框。 选中图像后，此复选框在右侧面板上可用。

    > [!NOTE]
    > 需要将重叠图像标记为 **透明** ，以指示它们是场景中的重叠图像。

## <a name="build-a-scene-using-the-scene-studio"></a>使用 Scene studio 生成场景

Microsoft 有一个 Scene studio，允许你生成场景。 它可以在场景编辑器[- Teams开发人员门户上提供](https://dev.teams.microsoft.com/scenes)。

> [!NOTE]
> 本文档引用了开发人员门户中的 scene studio Microsoft Teams。 在 App Studio 场景设计器中，界面和功能都相同。

Scene studio 上下文中的场景是一个包含以下内容的项目：

* 为会议组织者和会议演示者预留的座位。

    > [!NOTE]
    > 演示者不指当前正在共享的用户。 它指的是会议 [角色](https://support.microsoft.com/en-us/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。

* 具有可调整宽度和高度的每个参与者的席位和图像。

    > [!NOTE]
    > PNG 是唯一受支持的格式。

* 所有座位和图像的 XYZ 坐标。
* 隐藏为一个图像的图像的集合。

席位尺寸成为呈现参与者视频流的画布。 下图显示了每个展示为虚拟形象的席位，用于生成场景：

![Scene studio](../assets/images/apps-in-meetings/scene-design-studio.png)

**使用 Scene studio 生成场景**

1. 转到场景[编辑器 - Teams开发人员门户](https://dev.teams.microsoft.com/scenes)。

    >[!NOTE]
    > * 若要打开 Scene studio，你可以导航到开发人员门户的Teams [并选择](https://dev.teams.microsoft.com/home)**"为会议创建自定义场景"。**
    > * 若要打开 Scene studio，你可以导航到 Teams 开发人员门户的主页，从左侧部分选择"工具 ["，](https://dev.teams.microsoft.com/home)然后从"工具"部分选择 **"Scene studio"。**

1. 在"**场景编辑器"** 页中，选择 **"创建新场景"。**

1. 在 **"场景** "框中，输入场景的名称。

    >[!NOTE]
    > * 可以选择" **关闭"** 以在关闭或重新打开右窗格之间进行切换。
    > * 可以使用缩放栏放大或缩小场景，以更好地查看场景。

1. 将图像拖放到环境中，如下图所示：

    >[!NOTE]
    > * 你可以下载[包含SampleScene.zipSampleApp.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleScene.zip)[文件。](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleApp.zip)
    > * 或者，可以使用添加图像将背景图像添加到 **场景**。

    ![拖动到场景](../assets/images/apps-in-meetings/drag-and-drop-scene.png)

1. 选择已放置的图像。

1. 从右窗格中，选择图像的对齐方式或使用 **"** 调整大小"滑块调整图像大小。

    ![图像的对齐方式](../assets/images/apps-in-meetings/image-alignment.png)

1. 选择图像外部的区域。

1. 在右上角的"图层"下 **，选择"** 参与者 **"。**

1. 从"参与者数量"框中选择场景 **的参与者数量，** 然后选择"添加 **"。**

    >[!NOTE]
    > * 交付场景后，头像位置将替换为实际参与者的视频流。
    > * 你可以将参与者图像拖动到场景周围，并将其放在所需位置，然后使用调整大小箭头调整它们的大小。

1. 选择任何参与者图像，然后选中" **分配专** 色"复选框以将位置分配给参与者。

1. 选择 **参与者的会议** 组织者 **或** 演示者角色。

    >[!NOTE]
    > 在会议中，必须为一个参与者分配会议组织者的角色。

    ![分配专色](../assets/images/apps-in-meetings/assign-spot.png)

1. 选择 **"保存****"，** 然后选择"Teams"以快速测试场景中的Microsoft Teams。

    >[!NOTE]
    > 若要删除你创建的场景，请选择顶 **栏** 上的"删除场景"。

1. In the **View in Teams** dialog box， select Preview in **Teams**.
1. 在出现的对话框中， **选择添加**。

    可通过创建测试会议并启动自定义一起模式场景来测试或访问场景。 有关详细信息，请参阅激活 [自定义一起模式场景](#activate-custom-together-mode-scenes)。

    ![启动自定义一起模式场景](../assets/images/apps-in-meetings/launchtogethermode.png)

    >[!NOTE]
    > * 选择 **"** 预览"Microsoft Teams创建一个可在开发人员门户的"应用"Teams查看的应用。
    > * 选择 **"** 预览"会自动创建一个应用包appmanifest.js位于场景后面。 如前面所述，这是抽象的，但你可通过从菜单导航到应用 **来访问自动** 创建的应用包。
    > * 然后，可以在自定义"共同模式"场景库中查看场景。

1. （可选）可以从"保存"下拉菜单中选择"共享"，以创建可共享链接，以轻松分发场景供其他人使用。 打开此链接会为用户安装场景，他们可以开始使用它。

1. 预览后，可通过按照应用提交步骤将场景作为应用Teams交付到应用。

    >[!NOTE]
    > 对于已设计的场景，此步骤需要不同于场景包的应用包。 可在开发人员中心的应用部分找到自动创建Teams包。

1. （可选）可通过从"保存"下拉菜单中选择"导出"**来检索场景** 包。 下载.zip文件（即场景包）。

    ![导出场景](../assets/images/apps-in-meetings/build-a-scene.png)

    >[!NOTE]
    > 场景包由一个scene.js和用于生成场景的 PNG 资源组成。 可以审阅场景包以合并其他更改，如本文档scene.js示例部分所述。

分步入门示例中演示了利用 Z 轴的更复杂的场景。

## <a name="sample-scenejson"></a>示例scene.js打开

Scene.js和图像一起指示座位的确切位置。 场景包含用于放入参与者视频的位图图像、子画面和矩形。 这些子画面和参与者框在一个世界坐标系中定义，其中 X 轴指向右侧，Y 轴指向向下。 自定义一起模式场景支持放大当前参与者。 这对大型场景中的小会议很有用。 子画面是一种静态位图图像，位于世界。 子画面的 Z 值决定子画面的位置。 呈现从 Z 值最低的子画面开始，因此 Z 值越高，表示它离相机更近。 每个参与者都有自己的视频源，该源会进行分段，以便仅呈现前台。

下面是示例scene.js示例：

```json
{
   "protocolVersion": "1.0",
   "id": "A",
   "autoZoom": true,
   "mirrorParticipants ": true,
   "extent":{
      "left":0.0,
      "top":0.0,
      "width":16.0,
      "height":9.0
   },
   "sprites":[
      {
         "filename":"background.png",
         "cx":8.0,
         "cy":4.5,
         "width":16.0,
         "height":9.0,
         "zOrder":0.0,
   "isAlpha":false
      },
      {
         "filename":"table.png",
         "cx":8.0,
         "cy":7.0,
         "width":12.0,
         "height":4.0,
         "zOrder":3.0,
   "isAlpha":true
      },
      {
         "filename":"row0.png",
         "cx":12.0,
         "cy":15.0,
         "width":8.0,
         "height":4.0,
         "zOrder":2.0,
   "isAlpha":true
      }

   ],
   "participants":[
      {
         "cx":5.0,
         "cy":4.0,
         "width":4.0,
         "height":2.25,
         "zOrder":1.0,
         "seatingOrder":0
      },
      {
         "cx":11.0,
         "cy":4.0,
         "width":4.0,
         "height":2.25,
         "zOrder":1.0,
         "seatingOrder":1
      }
   ]
}
```

每个场景都有唯一的 ID 和名称。 场景 JSON 还包含有关用于场景的所有资源的信息。 每个资源都包含文件名、宽度、高度以及 X 和 Y 轴上的位置。 同样，每个座位都包含一个在 X 轴和 Y 轴上的座位 ID、宽度、高度和位置。 该订单会自动生成，并可以按偏好更改。

> [!NOTE]
> 呼叫订单号对应于加入呼叫者的顺序。

zOrder 表示沿 Z 轴放置图像和座位的顺序。 在许多情况下，如果需要，它会提供深度或分区感。 有关详细信息，请参阅分步入门示例。 此示例利用 zOrder。

现在，你已执行示例scene.js，你可以激活自定义"共同模式"场景以参与场景。

## <a name="activate-custom-together-mode-scenes"></a>激活自定义一起模式场景

获取最终用户如何在自定义"共同模式"场景中使用场景的端到端信息。

**选择场景并激活自定义一起模式场景**

1. 创建新的测试会议。

    >[!NOTE]
    > 在选择 **Scene** studio 中的"预览"时，场景会作为应用安装在Microsoft Teams。 这是开发人员在 Scene studio 中测试和试用场景的模型。 将场景作为应用交付后，用户将在场景库中看到这些场景。

1. 从左上角 **的"库**"下拉列表中，选择"共同 **模式"。** 将出现 **选取** 器对话框，并且添加的场景可用。

1. 选择 **"更改场景** "以更改默认场景。

1. 从 **"场景库"** 中，选择要用于会议的场景。

1. （可选）会议组织者和演示者可以更改 **会议中所有参与者** 的场景。

    >[!NOTE]
    > 在任意时间点，只能将一个场景用于会议。 如果演示者或组织者更改场景，则场景将全部更改。 切换为或退出自定义一起模式场景由单个参与者决定，但在自定义"共同模式"场景中，所有参与者具有相同的场景。

1. 选择“**应用**”。 Teams用户安装应用并应用场景。

## <a name="open-a-custom-together-mode-scenes-scene-package"></a>打开自定义一起模式场景场景包

你可以将场景包（从场景.zip中检索到的场景包）共享给其他创建者，以进一步增强场景。 可以利用 **"导入** 场景"功能。 此工具可帮助解包场景包，让创建者继续生成场景。

![场景 zip 文件](../assets/images/apps-in-meetings/scene-zip-file.png)

## <a name="see-also"></a>另请参阅

[会议Teams应用程序](teams-apps-in-meetings.md)
