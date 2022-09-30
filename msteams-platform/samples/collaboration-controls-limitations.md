---
title: 协作控制应用中的限制和已知问题
author: surbhigupta
description: 在本模块中，了解 Microsoft Teams 协作控制应用中的限制和已知问题。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: fe403c566b47be6509ff0d11113c34a8fc667cc9
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243386"
---
# <a name="limitations-and-known-issues"></a>限制和已知问题

> [!NOTE]
> 目前，协作控件仅在 [公共开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中可用。

下面是协作控件的限制：

* 组件不能在 Canvas 应用中使用。
* 组件仅支持完整选项卡视图。

     :::image type="content" source="../assets/images/collaboration-control/tasks-tab.png" alt-text="屏幕截图显示了任务。" border="true":::

* 未遵守所选的下格视图。 显示协作记录的所有任务、会议或笔记。

     :::image type="content" source="../assets/images/collaboration-control/subgrid-view.png" alt-text="屏幕截图显示了任务的下格视图。" border= "true":::

* 添加到时间线控件的活动不会显示在组件中创建的组件、任务、会议和备注中，不包括在时间线控件中。
* 在访问组件之前必须保存新记录，否则会看到空屏幕。
* 组件不会从添加到的窗体或应用继承主题。
* 仅当在 Microsoft Teams 中运行应用时，本地化才可用。
* 不支持 Microsoft Edge 严格模式，需要跨站点 Cookie。

**安装或升级完成时，管理员中心不会更新**

按照 [安装协作控](~/samples/install-collaboration-control.md)件中的安装步骤操作时，会重定向到 Power Platform 管理中心。 安装开始时会显示横幅，但安装完成后不会更新。 状态在安装期间列出，完成后，可能无法在列表中使用。 可以查看解决方案列表 [https://make.powerapps.com/](https://make.preview.powerapps.com/) ，确认安装已完成。

**安装期间的视图：**:::image type="content" source="../assets/images/collaboration-control/view-during-installation.png" alt-text="屏幕截图显示安装过程中的过程。" border="true":::

**安装后的视图：**:::image type="content" source="../assets/images/collaboration-control/view-after-installation.png" alt-text="屏幕截图显示安装完成。" border="true":::

将控件升级到更高版本时，会显示相同的安装启动横幅，但即使在升级完成后，控件状态仍会保持安装状态。 可以通过检查解决方案列表 [https://make.powerapps.com/](https://make.preview.powerapps.com/)来确认升级已完成，这大约需要 15 分钟。

在特定解决方案的历史记录中，还可以看到安装了更高版本，然后删除了以前的版本： :::image type="content" source="../assets/images/collaboration-control/history.png" alt-text="屏幕截图显示了已安装和删除的版本的特定解决方案的历史记录。" border="true":::

## <a name="bookings-meetings"></a>预订会议

使用 Bookings 与组织外部的用户互动时，会议控件支持一对一会议。 目前不支持使用协作控件的一对多会议。

**会议与会者状态不正确**

与会者到会议时，其响应状态可能无法在议程视图和会议详细信息中正确显示。 选择“拒绝”按钮可能会在屏幕上返回错误消息。

## <a name="tasks"></a>任务

**任务：未翻译筛选“clear”文本**

未翻译“任务”筛选器上显示的“清除”按钮上的文本。

**任务：显示已裁剪的网格上下文菜单**

当任务网格由少量的任务填充时，网格上下文菜单可能会显示为裁剪，并且需要使用滚动条。

**任务：关键字搜索筛选器使用“BeginsWith”运算符执行“来宾”任务**

使用关键字文本筛选器搜索任务时，“来宾”任务将使用“BeginsWith”运算符返回。 “Member”任务使用“Contains”运算符返回。

## <a name="files"></a>文件

存档文件后导航到存档文件夹时，用户可能会遇到重复的存档文件夹。  从存档文件夹导航 () 到文件主视图可解决此问题，并且不会删除存档的文件。

## <a name="controls"></a>控件

**控件无法保存**

如果控件无法保存任务或会议，则可能的原因可能是组 ID 或频道 ID 配置错误。  

解决方案 1：确认 ID 正确，并根据设置练习应用设置。  

解决方案 2：确保 Power Apps 环境和 Teams 环境位于同一租户中。  

**控件无法加载或显示错误**

如果控件无法加载或显示错误，则可能是暂时性问题。

示例：

:::image type="content" source="../assets/images/collaboration-control/sync-fail.png" alt-text="屏幕截图显示控件同步失败。":::

这会在控制台日志中呈现为：

:::image type="content" source="../assets/images/collaboration-control/control-fail.png" alt-text="屏幕截图是控制从 consol 日志故障的示例。" border="true":::

解决方案：刷新浏览器，或者在 Teams 应用中重新加载选项卡。

如果要在将应用名称、图标或说明上传到 Teams 后更改应用名称、图标或说明，请参阅 [自定义应用的外观](/MicrosoftTeams/customize-apps#customize-details-of-an-app)

## <a name="error-logging"></a>错误日志记录

这些控件提供以下方法来调试应用程序。

1. 调用 API 时插件事件的 **跟踪日志记录**。 此信息存储在 Dataverse 环境中。

    1. 若要启用跟踪日志记录，请执行 [日志记录和跟踪](/power-apps/developer/data-platform/logging-tracing?WT.mc_id=email)中的这些步骤。

1. UI 控 **件的浏览器日志记录**。 这是标准控制台日志记录。

    1. 使用浏览器通过 Power Platform 和 Teams Web 运行Collaboration Manager应用时支持此功能。
    1. 在控制台选项卡中，可以使用Collaboration Manager错误消息或搜索Collaboration Manager控制名称（如任务）来搜索错误。

> [!TIP]
> 如果 Teams 桌面客户端中发生错误，请尝试在 Teams Web 中复制以捕获错误日志。

## <a name="faq"></a>常见问题

<br>

<details>

<summary><b>预览版)  (协作控件是什么？</b></summary>

协作控制 (预览版) 使你可以将 Microsoft 365 功能添加到 Power Apps 业务线自定义应用程序，以便在 Teams 或 Power Apps 中协作处理业务流程时简化用户工作流。

<br>

</details>

<br>

<details>

<summary><b>协作控制 (预览版) 对制造商有什么好处？</b></summary>

借助这些新控件，你作为一名创建者可以拖放将 Microsoft 365 协作引入应用的控件。

<br>

</details>

<br>

<details>

<summary><b>协作控制 (预览版) 对用户有什么好处？</b></summary>

用户可以通过协作处理审批、文件、会议、笔记和任务来体验生产力提升并保持其流程，而无需离开应用的上下文。

<br>

</details>

<br>

<details>

<summary><b>如何实现 (预览版) 获取对协作控件的访问权限？</b></summary>

请求 Power Platform 管理员将控件从 AppSource 安装到 Power Apps 环境。

<br>

</details>

<br>

<details>

<summary><b>如何实现将控件添加到模型驱动应用？</b></summary>

转到窗体设计器，将控件从组件窗格拖动到窗体上。

<br>

</details>
