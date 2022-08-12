---
title: 自定义同框场景模式
author: surbhigupta
description: 使用自定义"协同模式"场景
ms.topic: conceptual
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: d54d2ffaa6035778ba195c9e2eba44c2e096892e
ms.sourcegitcommit: 69a45722c5c09477bbff3ba1520e6c81d2d2d997
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/11/2022
ms.locfileid: "67311965"
---
# <a name="custom-together-mode-scenes-in-teams"></a>在 Teams 中自定义同框场景模式

Microsoft Teams 中的"自定义在一起"模式场景提供沉浸式且极具吸引力的会议环境，并执行以下操作：

* 将人们汇集在一起，鼓励他们打开视频。
* 将参与者以数字方式合并到单个虚拟场景中。
* 将参与者的视频流置于由场景创建者设计和修复的预先确定的席位中。

在自定义"协同模式"场景中，场景是一个项目。 场景由场景开发人员使用 Microsoft Scene Studio 创建。 在场景设置中，参与者具有包含视频流的席位。 这些视频将呈现在这些座位中。 建议使用仅场景应用，因为此类应用的体验是明确的。

以下过程概述了如何创建仅场景应用：

:::image type="content" source="../assets/images/apps-in-meetings/create-together-mode-scene-flow.png" alt-text="仅创建场景应用。":::

仅场景应用仍然是 Teams 中的应用。 Scene Studio 在后台处理应用包创建。 单个应用包中的多个场景显示为用户的平面列表。

> [!NOTE]
> 用户无法从移动端启动同框场景模式。但是，在用户通过移动设备加入会议并从桌面打开“同框场景模式”后，打开视频的移动用户将显示在桌面上的“同框场景模式”中。

## <a name="prerequisites"></a>先决条件

必须基本了解以下内容才能使用自定义"同一模式"场景：

* 定义场景中的场景和座位。
* 拥有 Microsoft 开发人员帐户并熟悉 Teams [开发人员门户](../concepts/build-and-test/teams-developer-portal.md)。
* 了解[应用旁加载的概念](../concepts/deploy-and-publish/apps-upload.md)。
* 确保管理员已授予 [**上传自定义应用**](../concepts/deploy-and-publish/apps-upload.md)的权限，并分别选择所有筛选器作为应用设置和会议策略的一部分。

## <a name="best-practices"></a>最佳做法

对于场景生成体验，请考虑以下做法：

* 确保所有图像均采用 PNG 格式。
* 确保包含所有映像的最终包的分辨率不得超过 1920x1080。 分辨率为偶数。 要成功显示场景，需要此分辨率。
* 确保最大场景大小为 10 MB。
* 确保每个图像的最大大小为 5 MB。 场景是多个图像的集合。 限制是针对每个单独图像。
* 确保根据需要选择 **透明**。 选中图像后，此复选框在右侧面板上可用。 重叠图像必须标记为 **透明** ，以指示它们与场景中的图像重叠。

## <a name="build-a-scene-using-the-scene-studio"></a>使用 Scene Studio 生成场景

Microsoft 有一个场景工作室，可用于生成场景。 它在 [场景编辑器 - Teams 开发人员门户](https://dev.teams.microsoft.com/scenes)上提供。 本文档引用 Teams 开发人员门户中的 Scene Studio。

Scene Studio 上下文中的场景是包含以下元素的项目：

* 为会议组织者和会议演示者保留的席位。 演示者不引用主动共享的用户。 它引用 [会议角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。

* 具有可调整宽度和高度的每个参与者的席位和图像。 图像仅支持 PNG 格式。

* 所有席位和图像的 XYZ 坐标。

* 作为一个图像的图像集合。

下图显示了表示为生成场景的虚拟形象的每个席位：

![场景工作室](../assets/images/apps-in-meetings/scene-design-studio.png)

若要使用 Scene Studio 生成场景，请执行以下步骤：

1. 转到 [场景编辑器 - Teams 开发人员门户](https://dev.teams.microsoft.com/scenes)。

    或者，若要打开 Scene Studio，可以转到 [Teams 的主页开发人员门户](https://dev.teams.microsoft.com/home)：
    * 选择 **为会议创建自定义场景**。
    * 从左侧部分选择 **工具**，然后从"**工具"** 部分中选择"**Scene Studio**"。

1. 在 **场景编辑器** 中，选择 **创建新场景**。

1. 在 **场景名称** 中，输入场景的名称。

    * 可以选择 **关闭** 以在关闭或重新打开右窗格之间切换。
    * 可以使用缩放栏放大或缩小场景，以便更好地查看场景。

1. 选择 **添加映像** 以将映像添加到环境中：

   :::image type="content" source="../assets/images/apps-in-meetings/addimages.png" alt-text="将图像添加到环境中。":::

    >[!NOTE]
    >可以下载 [SampleScene.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleScene.zip) ，并 [SampleApp.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleApp.zip) 包含图像的文件。

1. 选择已添加的映像。

1. 在右窗格中，选择图像的对齐方式，或使用 **调整** 大小来调整图像大小：

    ![图像对齐方式](../assets/images/apps-in-meetings/image-alignment.png)

1. 选择图像外部的区域。

1. 在右上角，选择 **层** 下 **参与者**。

1. 从"参与者 **数"框中选择场景的参与者数**，然后选择 **添加**。 传送场景后，虚拟形象位置将替换为实际参与者的视频流。 可以将参与者的图像拖动到场景周围，并将其置于所需位置。 可以使用调整大小箭头调整它们的大小。

1. 选择任何参与者图像，然后选择 **分配 Spot** 将位置分配给参与者。

1. 为参与者选择 **会议组织者** 或 **演示者** 角色。 在会议中，必须为一名参与者分配会议组织者的角色：

   :::image type="content" source="../assets/images/apps-in-meetings/assign-spot.png" alt-text="为参与者分配一个位置。":::

1. 选择“**保存**”，然后选择“**在 Teams 中查看**”，以在 Microsoft Teams 中快速测试场景。

    * 选择“**在 Teams 中查看视图**”会自动创建可在 Teams 开发人员门户的“**应用**”页中查看的 Teams 应用。
    * 在 Teams 中选择 **视图** 会自动创建场景后面的 appmanifest.json 应用包。 可以从菜单转到  **应用** 并访问自动创建的应用包。
    * 若要删除创建的场景，请选择顶部栏上的 **删除场景**。

1. 在 **“在 Teams 中查看”** 中，选择 **“在 Teams 中预览”**。
1. 在出现的对话框中，选择“**添加**”。

    通过创建测试会议并启动自定义"一起模式"场景来测试或访问场景。 有关详细信息，请参阅 [激活自定义"一起模式"场景](#activate-custom-together-mode-scenes)：

    ![启动自定义"一起使用模式"场景](../assets/images/apps-in-meetings/launchtogethermode.png)

    然后，可以在自定义的"协同模式"场景库中查看场景。

（可选）你可以从 **"保存**"下拉菜单中选择"**共享**"。 你可以创建一个可共享链接来分发场景供其他人使用。 用户可以打开链接以安装场景并开始使用它。

预览后，场景将按照应用提交步骤作为应用发送到 Teams。 此步骤需要应用包。 对于设计的场景，应用包与场景包不同。 自动创建的应用包位于 Teams 开发人员中心的" **应用** "部分。

（可选）通过从 **"保存**"下拉菜单中选择"**导出**"来检索场景包。 下载 .zip 文件（即场景包）。 场景包包括 scene.json 和用于生成场景的 PNG 资产。 查看场景包以合并其他更改：

![导出场景](../assets/images/apps-in-meetings/build-a-scene.png)

分步入门示例演示了使用 Z 轴的复杂场景。

## <a name="sample-scenejson"></a>示例 scene.json

Scene.json 与图像一起指示席位的确切位置。 场景由位图图像、子画面和矩形组成，用于将参与者视频放入其中。 这些子网站和参与者框是在世界坐标系统中定义的。 X 轴指向右侧，Y 轴向下。

自定义"一起"模式场景支持缩放当前参与者。 此功能有助于在大型场景中召开小型会议。 Sprite 是放置在世界上的静态位图图像。 Sprite 的 Z 值决定了子节的位置。 渲染以 Z 值最低的子节开头，因此 Z 值越高，表示离相机更近。 每个参与者都有自己的视频源，该源进行分段，因此仅呈现前台。

以下代码是 scene.json 示例：

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

每个场景都有唯一的 ID 和名称。 场景 JSON 还包含有关用于场景的所有资产的信息。 每个资产都包含 X 轴和 Y 轴上的文件名、宽度、高度和位置。 同样，每个席位都包含 X 轴和 Y 轴上的席位 ID、宽度、高度和位置。 将自动生成座位顺序，并根据首选项进行更改。 座位订单号对应于加入呼叫的人员的顺序。

`zOrder`表示沿 Z 轴放置图像和席位的顺序。 如果需要，它会提供深度或分区感。 请参阅分步入门示例。 该示例使用 `zOrder`。

现在，你已完成示例 scene.json，你可以激活自定义的"在一起模式"场景来参与场景。

## <a name="activate-custom-together-mode-scenes"></a>激活自定义"在一起"模式场景

获取有关用户如何在自定义"协同模式"场景中参与场景的详细信息。

若要选择场景并激活自定义“同框场景模式”场景，请按照这些步骤操作：

1. 创建新的测试会议。

    >[!NOTE]
    > 在 Scene Studio 中选择“**预览**”时，场景将作为应用安装在 Microsoft Teams 中。 这是开发人员在场景工作室中测试和试用场景的模型。 将场景作为应用提供后，用户会在场景库中看到这些场景。

1. 从左上角的" **库"** 下拉列表中，选择" **一起模式"**。 将显示 **选取器** 对话框，并且添加的场景可用。

1. 选择 **更改场景** 以更改默认场景。

1. 从 **场景库** 中，选择要用于会议的场景。

    或者，会议组织者和演示者可以为会议中的 **所有参与者更改场景**。

    >[!NOTE]
    > 在任何时候，只有一个场景用于会议。 如果演示者或组织者更改了场景，则会对所有场景进行更改。 切换到或退出自定义的"同一模式"场景取决于单个参与者，但在自定义"同一模式"场景中，所有参与者都具有相同的场景。

1. 选择“**应用**”。Teams 为用户安装应用并应用场景。

## <a name="open-a-custom-together-mode-scenes-scene-package"></a>打开自定义"一起"模式场景包

可以将场景包（即从 Scene Studio 检索到的 .zip 文件）共享给其他创建者，以进一步增强场景。 **导入场景** 功能有助于解包场景包，以便创建者继续生成场景。

![场景 zip 文件](../assets/images/apps-in-meetings/scene-zip-file.png)

## <a name="see-also"></a>另请参阅

* [Teams 会议应用](teams-apps-in-meetings.md)
* [通话和会议机器人](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)
* [使用 Microsoft Teams实时媒体通话和会议](~/bots/calls-and-meetings/real-time-media-concepts.md)
