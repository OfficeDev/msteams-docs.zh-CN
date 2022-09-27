---
title: 具有协作控件的应用程序
author: surbhigupta
description: 在本模块中，了解如何使用 Teams 协作控件生成模型驱动应用，以及如何向应用添加协作控件。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: e712c55dd4543edda9115751be09d81d1795f02b
ms.sourcegitcommit: c1032ea4f48c4bbf5446798ff7d46d7e6e9f55d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027338"
---
# <a name="create-a-new-model-driven-app-with-collaboration-controls-for-teams"></a>使用 Teams 协作控件创建新的模型驱动应用

协作控件专为 [模型驱动的应用程序](/power-apps/maker/model-driven-apps/model-driven-app-overview)设计。 以下部分介绍如何创建模型驱动的应用。

> [!NOTE]
> 目前，协作控件仅在 [公共开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中可用。

## <a name="create-a-model-driven-application"></a>创建模型驱动的应用程序

1. 打开 [https://make.powerapps.com。](https://make.powerapps.com/) 或 [https://make.preview.powerapps.com.](https://make.preview.powerapps.com/)

1. 在左窗格中选择 **“解决方案** ”。

1. 选择 **“新建解决方案**”，以便你可以为将来的所有自定义项提供一个主页。

   :::image type="content" source="../assets/images/collaboration-control/new-solution.png" alt-text="屏幕截图是显示新解决方案的示例。":::

1. 提供新解决方案的名称和发布者，此解决方案将保留自定义Collaboration Manager。

   :::image type="content" source="../assets/images/collaboration-control/collaboration-manager.png" alt-text="屏幕截图是显示协作管理器的示例。":::

1. 选择 **“创建”**

1. 创建解决方案后，它将显示在解决方案列表中。 选择要打开的解决方案。

1. 在创建应用之前，请为数据创建一个主页。 选择 **“新建** > **表** ”以开始使用。

     :::image type="content" source="../assets/images/collaboration-control/create-table.png" alt-text="屏幕截图介绍了如何创建新表。":::

1. 为表命名。 在 **“高级”选项** 下，选择 **“创建新活动**”。

   :::image type="content" source="../assets/images/collaboration-control/new-activity.png" alt-text="屏幕截图介绍了如何创建新活动。":::

1. 选择“**保存**”。

1. 创建完表后，可以通过添加额外的列、关系和更多 (可选) 来自定义表。

1. 现在，可以通过选择“**新建** > **应用** > 模型驱动”应用来创建新的模型 **驱动应用。**

   :::image type="content" source="../assets/images/collaboration-control/model-driven-app.png" alt-text="屏幕截图是显示新模型驱动应用的示例。":::

1. 选择新的 **新式应用设计器 (预览)** 打开新应用。

   :::image type="content" source="../assets/images/collaboration-control/model-driven-app-blank.png" alt-text="屏幕截图是显示新的模型驱动应用空白的示例。":::

1. 选择 **“创建”。**

1. 为应用命名并选择 **“创建”。**

   :::image type="content" source="../assets/images/collaboration-control/collaboration-manager-for-inspection.png" alt-text="屏幕截图是显示要检查的协作管理器的示例。":::

1. 选择 **“添加”页。**

1. 选择 **基于表的视图和窗体。**

   :::image type="content" source="../assets/images/collaboration-control/table-based.png" alt-text="屏幕截图是显示基于表的视图和窗体的示例。":::

1. 选择 **“下一步”。**

1. 搜索并选择之前创建的表。

   :::image type="content" source="../assets/images/collaboration-control/table-view-form-pages.png" alt-text="屏幕截图是显示表格视图窗体页的示例。":::

1. 选择 **“添加”。**

1. 选择 **“发布** ”以保存和发布应用。

1. 选择 **“播放** ”以测试新应用。

现在，你已成功构建模型驱动应用。

## <a name="add-collaboration-controls-to-your-application"></a>将协作控件添加到应用程序

下面是将协作控制功能（如任务、会议、文件和备注体验）添加到创建的应用的步骤：

1. 若要包含“任务”、“会议”和“备注”选项卡，需要编辑“主信息”窗体。 若要开始，请返回到资源管理器并选择解决方案。

1. 选择在[为 Teams 创建新的模型驱动应用](#create-a-new-model-driven-app-with-collaboration-controls-for-teams)时创建的表。

1. 转到表的“窗体”选项卡。

     :::image type="content" source="../assets/images/collaboration-control/forms-tab.png" alt-text="屏幕截图是显示表的窗体选项卡的示例。":::

1. 选择窗体类型 **Main** 的信息窗体以在窗体设计器中打开它。

1. 进入窗体设计器后，在“**组件**”部分的 **1 列选项卡** 中按下并拖动。

     :::image type="content" source="../assets/images/collaboration-control/components.png" alt-text="屏幕截图是显示电源应用组件的示例。":::

1. 选择选项卡后，将选项卡重命名为属性窗格中的“任务”。

1. 选择选项卡名称以选择完整部分，然后在“属性”窗格中选择“ **展开第一个组件”以显示完整选项卡** 。 这是必需的，因为最好在完整选项卡视图中查看协作控件。

    :::image type="content" source="../assets/images/collaboration-control/tasks-pane.png" alt-text=" 屏幕截图介绍如何选择第一个组件以完整选项卡。":::

     :::image type="content" source="../assets/images/collaboration-control/expand-first-component.png" alt-text=" 屏幕截图介绍如何将第一个组件扩展到完整选项卡。":::

1. 展开控件抽屉上的“协作 (预览) ”类别，并将“任务 (预览) 控件拖动到”任务“窗体中的部分。

     :::image type="content" source="../assets/images/collaboration-control/collab-preview.png" alt-text="在任务窗体中将控件预览到节":::

3. 将表设置为“活动”&选择“完成”。

     :::image type="content" source="../assets/images/collaboration-control/select-table-activities.png" alt-text="选择要活动的表":::

5. 在属性上选择“隐藏标签”。

     :::image type="content" source="../assets/images/collaboration-control/hide-label-properties.png" alt-text="选择隐藏标签":::

1. 现在将显示“任务”控件。

     :::image type="content" source="../assets/images/collaboration-control/new-collab-control.png" alt-text="任务控件显示":::

1. 重复“任务”步骤，将审批、文件、会议和备注控件添加到应用。
1. 添加所有控件后，将在窗体设计器中看到下面呈现的控件。 如果控件未在窗体设计器中呈现，例如显示空白窗体，请在 Power Apps 中运行应用，并且存在“配置”页或“空状态”意味着控件已成功添加。

     :::image type="content" source="../assets/images/collaboration-control/new-collab-approval.png" alt-text="控件窗体设计器":::

1. 现在，可以通过选择 Power Apps 在 Power Apps 中运行电源应用。

     :::image type="content" source="../assets/images/collaboration-control/collaboration-manager-for-inspections-power-apps.png" alt-text="用于检查的协作管理器":::

1. 通过选择 **+New** 创建新记录，然后打开记录。

     :::image type="content" source="../assets/images/collaboration-control/power-apps-open-the-record.png" alt-text="屏幕截图是显示打开记录的电源应用的示例。":::

1. 现在，可以看到每个选项卡的视图，这些视图与下图类似：

     :::image type="content" source="../assets/images/collaboration-control/tabs.png" alt-text="屏幕截图是显示任务的示例。":::

     > [!TIP]
     > 只有在应用程序中保存记录后，控件才可见。 如果记录中未显示控件选项卡，请尝试刷新浏览器或从 Power Apps 重新发布应用。

现在，你已成功将协作控件添加到应用程序。 现在可以在 Power Apps 中运行应用程序并启动控件。 由于尚未配置设置，因此在添加这些实体之前，你将无法创建诸如任务或会议等实体。

## <a name="define-settings-for-your-collaboration"></a>定义协作设置

可以为业务实体定义协作控件的设置，例如 [在新的模型驱动应用](#create-a-new-model-driven-app-with-collaboration-controls-for-teams)中创建的表。

可以应用的设置如下所示：

|设置|使用方|
|---|---|
|组 ID|任务、内部会议、审批。|
|预订业务 ID|使用 Bookings 的外部会议 |
|站点 ID|SharePoint 文件 |
|驱动器 ID|SharePoint 文件|

> [!NOTE]
> 设置对启动应用具有关键性，因此请确保按照建议执行步骤。 如果启动和保存控件时遇到问题，请重新检查值。

可以通过创建新团队或使用 Microsoft Teams 中的现有团队来托管应用程序和创建设置变量来获取组 ID。

若要创建新团队，请参阅 [从头开始创建团队](https://support.microsoft.com/en-us/office/create-a-team-from-scratch-174adf5f-846b-4780-b765-de1a0a737e2b)。

使用以下说明检索 Teams 团队的组 ID 以进行审批、任务和内部会议：

1. 在团队列表中查找团队。

1. 选择省略号 **...** 

     :::image type="content" source="../assets/images/collaboration-control/get-link.png" alt-text="屏幕截图介绍如何将链接到团队。":::

1. 复制链接并记录 URL 中的 `groupId` 值。 稍后在定义解决方案设置时，将使用此值。

     `https://teams.microsoft.com/l/team/19%3akk_TuKhjXu92yJvg4TZ10S6rouLSCgvHIb5NOOTfRjg1%40thread.tacv2/conversations?groupId=4310f270-1aa5-4089-99f3-47eb3b4d69ad&tenantId=b699419b-e0df-47e3-9909-24076fdcf68b`

使用以下说明检索 SharePoint 网站 ID 和文件驱动器 ID：

1. 若要使用“文件”控件，需要配置到现有 SharePoint 网站或创建新的 SharePoint 网站。 若要创建新网站，请参阅 [创建网站](/sharepoint/create-site-collection)。

1. 现在，检索网站 ID 和驱动器 ID 的设置值，可使用 SharePoint 网站中的详细信息调用这些值。

     1. **网站 ID**：使用 [Graph 资源管理器](https://developer.microsoft.com/graph/graph-explorer)登录并授予 Directory.ReadWrite.All 和 User.ReadWrite.All 的权限

         :::image type="content" source="../assets/images/collaboration-control/graph-permissions.png" alt-text="屏幕截图是显示图形资源管理器的示例。":::

     1. 确保将主机名替换为主机名和站点路径的相对路径，并调用 `https://graph.microsoft.com/v1.0/sites/{hostname}:/{relative-path-to-site}`图形。 下面是一个示例：
         1. 如果网站 URL = `https://myhostname.sharepoint.com/sites/MySiteName`
         1. 主机名 = `myhostname.sharepoint.com`
         1. 站点的相对路径 = `sites/MySiteName`

              :::image type="content" source="../assets/images/collaboration-control/graph-call.png" alt-text="屏幕截图是显示 Graph 调用的示例。":::

            图形调用将是， `https://graph.microsoft.com/v1.0/sites/myhostname.sharepoint.com:/sites/MySiteName`.

     1. 收到的响应是表示站点的 Json 对象，例如站点 ID。`abcdef.sharepoint.com,0abe7394-6fce-4dcc-9884-7eaceb48cd41,8cb86762-16cd-495e-87cb-893cfdf94054`

     1. 保存站点 ID 值参数。

     1. **驱动器 ID**：使用 [Graph 资源管理器](https://developer.microsoft.com/graph/graph-explorer)，使用之前保存的站点 ID 值登录并进行图形调 `https://graph.microsoft.com/v1.0/sites/{site-id}/drives` 用。

     1. 返回 Json 响应，其参数值为类型数组或驱动器对象列表。 查看 Json，了解其名称参数与文档库名称匹配的 Json 对象。 保存驱动器 ID 参数的值。

若要与组织外部的用户（例如客户）创建会议，以及在应用中使用虚拟访问功能，需要提供 Bookings 业务。 有关详细信息，请参阅[Microsoft Bookings](/microsoft-365/bookings/bookings-overview?view=o365-worldwide&preserve-view=true)。

## <a name="add-settings-to-your-collaboration-manager-app"></a>将“设置”添加到Collaboration Manager应用

若要应用设置并在 Power Apps 中探索应用的协作功能，请打开之前创建的应用程序。 你将看到一个视图页，可在其中选择现有记录或创建新记录。 以打开或创建记录开头。

需要添加之前为应用程序保存的设置 ID

|设置|使用方|
|---|---|
|组 ID|任务、内部会议、审批。|
|预订业务 ID|使用 Bookings 的外部会议 |
|站点 ID|SharePoint 文件 |
|驱动器 ID|SharePoint 文件|

### <a name="add-settings-for-tasks-meetings-and-files"></a>添加任务、会议和文件的设置

1. 启动控件，可以看到一个窗口如下所示：

     :::image type="content" source="../assets/images/collaboration-control/launch-window.png" alt-text="屏幕截图是显示控件窗口的示例。":::

1. 选择 **“配置** ”并导航到“常规”选项卡以添加组 ID。

     :::image type="content" source="../assets/images/collaboration-control/groupid-general.png" alt-text="屏幕截图介绍如何在“常规”选项卡中添加组 ID。":::

1. 打开“文件”选项卡以添加网站 ID 和驱动器 ID。

     :::image type="content" source="../assets/images/collaboration-control/files-tab.png" alt-text="屏幕截图介绍如何在文件选项卡中添加网站 ID 和驱动器 ID。":::

Notes 控件不需要设置值。 现在可以在应用程序中创建任务和会议等实体。 如果在启动和保存控件时遇到问题，请重新检查设置值。

## <a name="explore-your-new-collaboration-manager-app"></a>探索新的Collaboration Manager应用

以下部分介绍如何使用任务、备注、会议、文件和审批控件。

### <a name="create-tasks"></a>创建任务

通过选择“任务”选项卡浏览“任务”选项卡中的协作，该选项卡将打开一个空页面，用户可在其中添加完成所需的所有相关任务。

1. 若要为团队创建新任务，请选择 **“添加任务**”。 它将打开一个对话框，你可以在其中提供有关任务的具体信息，并将其分配给团队中的相关人员，然后选择“保存”。

     :::image type="content" source="../assets/images/collaboration-control/add-task.png" alt-text="屏幕截图介绍了如何添加任务。":::

1. 已保存的任务将显示在任务列表中。

1. 由于所有任务都由Microsoft Planner提供支持。 用户可以使用 Microsoft Teams 中的 Tasks 应用查看分配的所有任务。 若要开始，请选择省略号 **...** 在 Teams 左窗格中。 按 Planner 和 To Do 搜索并选择任务。

     :::image type="content" source="../assets/images/collaboration-control/tasks-planner.png" alt-text="屏幕截图是 Planner 和 To Do 任务的示例。":::

1. 打开“任务由 Planner 和 To Do”应用后，用户可以在应用的 **“分配给我** ”部分中查看在应用中创建的所有任务。 用户还可以查看任务的详细信息、添加附件并将其标记为完整。

### <a name="create-notes"></a>创建备注

若要创建笔记，请从应用中选择 **“备注”** 选项卡，该选项卡将重定向到用户可在其中提供任何相关信息的空屏幕。 若要添加新笔记，请选择 **“新建笔记**”。
在备注中添加相关详细信息后，选择 **“保存**”。

### <a name="create-meetings"></a>创建会议

在记录中选择 **“会议** ”选项卡以安排内部和外部会议。

若要安排内部会议，请选择 **“新建会议** ”按钮旁边的下拉列表，然后选择 **“内部会议**”。

:::image type="content" source="../assets/images/collaboration-control/new-meeting-tab.png" alt-text="屏幕截图介绍如何安排内部会议。":::

> [!NOTE]
>
> 如果已为 Microsoft Booking 配置了有效的应用设置，则会启用客户预订。

在 **“新建会议** ”对话框中，用户可以提供有关会议的相关信息，然后选择 **“保存**”。 会议将显示在会议列表中。

:::image type="content" source="../assets/images/collaboration-control/new-meeting.png" alt-text="屏幕截图介绍了如何安排新会议。":::

若要安排与客户的外部会议，请选择 **“新建会议** ”按钮旁边的下拉列表，然后选择 **“客户预订**”。 如果 **“新会议**”下拉列表中没有“**客户预订**”选项，请确认应用是否配置为在“设置”中Microsoft Bookings，并且用户具有“预订管理员”角色。 有关详细信息，请参阅 [将员工添加到 Bookings](/microsoft-365/bookings/add-staff?view=o365-worldwide&preserve-view=true)。 可以通过在 Bookings 业务中添加其他服务来添加其他预订类型。

:::image type="content" source="../assets/images/collaboration-control/customer-booking.png" alt-text="屏幕截图介绍了如何计划客户预订。":::

用户可以在会议列表中看到内部会议和客户预订。 会议开始后，用户可以通过选择“ **加入** ”按钮加入，该按钮直接在 Microsoft Teams 中打开会议。

由于会议由 Outlook 提供支持，因此用户可以导航到 Bookings 或Outlook 日历查看单个日历中列出的所有会议。 内部会议在共享日历中列出。

下面是将共享日历添加到 Outlook (可选) 的步骤：

1. 在功能区的“开始”选项卡上的“管理日历”部分中，选择“打开日历”>“打开共享日历”。

1. 在“打开共享日历”对话框中，输入人员的姓名。 选择要查找的人员，然后选择“确定”。

在左窗格的“共享日历”下，现在应会看到一个包含该人员姓名的其他日历。

:::image type="content" source="../assets/images/collaboration-control/customer-booking.png" alt-text="屏幕截图介绍了如何计划客户预订。":::

### <a name="add-files"></a>添加文件

打开应用程序中的 **“文件”** 选项卡，然后选择 **“上传**”以从OneDrive for Business或计算机上传文件。 成功上传文件后，主列表视图会自动刷新以显示列表中的文件。

:::image type="content" source="../assets/images/collaboration-control/meeting-calendar.png" alt-text="屏幕截图介绍了如何打开共享日历。":::

### <a name="approvals"></a>审批

审批允许用户在记录中工作时请求他人注销。 例如，请求批准以完成任务或关闭记录。

1. 转到应用程序的 **“审批”** 选项卡。

1. 如果没有审批请求，用户将看到以下屏幕。

      :::image type="content" source="../assets/images/collaboration-control/no-approvals.png" alt-text="屏幕截图是显示无审批请求的示例。":::

1. 选择 **“新建审批请求** ”以打开审批请求表单。

      :::image type="content" source="../assets/images/collaboration-control/approval-request-form.png" alt-text="屏幕截图是显示新的审批请求表单的示例。":::

1. 在审批请求表单中，填写所需的字段并选择 **“发送**”，这将创建一个请求并添加到列表中。

      :::image type="content" source="../assets/images/collaboration-control/approvals-list.png" alt-text="屏幕截图是显示审批列表的示例。":::

1. 选择审批以查看详细信息。

有关审批的详细信息，请参阅 [创建审批](https://support.microsoft.com/en-us/office/create-an-approval-6548a338-f837-4e3c-ad02-8214fc165c84)。
