---
title: 协作控制应用中的 Power Automate
author: surbhigupta
description: 在本模块中，了解 Microsoft Teams 中协作控制应用中的 Power Automate 以及如何创建 Azure 应用。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: deda9f0178c51410e2208e81263b315de4ca1da4
ms.sourcegitcommit: 0bb822b30739e4a532a36764dad2dbf35a81ba29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2022
ms.locfileid: "67178869"
---
# <a name="power-automate"></a>Power Automate

Power Automate 可用于在Collaboration Manager应用程序周围自动执行工作流。 例如，在创建新记录时自动创建任务。

借助协作控制连接器，开发人员可以通过 Microsoft Power Automate、Microsoft Power Apps 和 Azure 逻辑应用中的自动化工作流中的触发器或操作来访问协作控制 API。

> [!NOTE]
> 目前，协作控件仅在 [公共开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中可用。

在此版本中，连接器使制造商能够设置触发器：

1. 创建协作会话时。
1. 创建或修改规划器任务时。

它还包括一组可使用流调用的协作控制 API 和任务。 连接器操作在工作流步骤选择中找到。 连接器本身会在具有可配置选项的自定义连接器上找到。 若要在解决方案中使用连接器，必须创建环境信任的Azure 应用才能执行流。

## <a name="create-an-azure-app"></a>创建Azure 应用

在 [Azure](https://ms.portal.azure.com/#home) Active Directory 管理Azure 门户中，使用以下步骤，使用足够的权限登录到帐户，将用户应用程序添加到环境中：

1. 在Azure 门户主页中，选择 **Azure Active Directory**。 在 Azure Active Directory 中，选择 **“添加** ”下拉列表，然后选择 **“应用注册**”。

   :::image type="content" source="../assets/images/collaboration-control/azure-active-directory-home-portal.png" alt-text="屏幕截图是演示如何添加新应用注册的示例":::

   :::image type="content" source="../assets/images/collaboration-control/new-app-registration.png" alt-text="屏幕截图是演示如何添加新应用注册的示例":::

1. 在应用注册中，设置应用程序名称并将 Web 重定向 URI 添加到 `https://global.consent.azure-apim.net/redirect`。

   :::image type="content" source="../assets/images/collaboration-control/register-an-application.png" alt-text="屏幕截图是演示如何注册应用程序的示例":::

1. 在“隐式授予”和“混合流”部分中，选择访问令牌和 ID 令牌。

   :::image type="content" source="../assets/images/collaboration-control/authorisation-endpoint-tokens.png" alt-text="屏幕截图是显示令牌和 ID 令牌的示例":::

1. 在左窗格中选择 API 权限，然后选择 **“添加权限**”，然后搜索 **动态 CRM** 权限。

   :::image type="content" source="../assets/images/collaboration-control/dynamic-crm.png" alt-text="屏幕截图是演示如何添加权限的示例":::

1. 选择 Dynamics CRM 后，请确保在权限中选择 **user_impersonation** 。

   :::image type="content" source="../assets/images/collaboration-control/admin-consent-required.png" alt-text="屏幕截图是演示如何启用复选框的示例user_impersonation":::

1. 在“证书&机密”页中，添加 **新的客户端机密** 并保存该值以供以后在设置连接器安全性时使用。

   :::image type="content" source="../assets/images/collaboration-control/copy-new-secret-value.png" alt-text="屏幕截图是演示如何复制新机密值的示例":::

1. 在应用程序概述页中，复制 **应用程序 (客户端) ID** ，并在设置连接器安全性时将其保存供以后使用。

   :::image type="content" source="../assets/images/collaboration-control/application-client-ID.png" alt-text="屏幕截图是演示如何保存客户端 ID 的示例":::

现在，Azure 应用已全部设置，需要将其添加为环境中的用户应用程序。

## <a name="add-azure-app-to-power-automate-environment"></a>将 Azure 应用添加到 Power Automate 环境

1. 打开 Power Apps 门户，在右上角选择 **设置** 并打开 **管理员中心**。

   :::image type="content" source="../assets/images/collaboration-control/power-apps-interface.png" alt-text="屏幕截图是显示 Power Apps 界面的示例":::

1. 在管理中心，从左窗格中选择 **“环境** ”，然后在要添加连接器应用的列表中选择环境。

   :::image type="content" source="../assets/images/collaboration-control/power-platform-admin-center.png" alt-text="屏幕截图是演示如何添加连接器应用的示例":::

1. 在“环境详细信息”页中，选择 **“设置**”。

   :::image type="content" source="../assets/images/collaboration-control/settings-environment.png" alt-text="屏幕截图是演示如何选择设置的示例":::

1. 在“设置详细信息”页中，选择 **“用户 + 权限”** 部分，然后选择 **“应用程序用户**”。

   :::image type="content" source="../assets/images/collaboration-control/users-link.png" alt-text="屏幕截图是显示应用程序用户链接的示例":::

1. 在“应用用户”页中，选择 **+新建应用用户**。 **将显示“新建应用用户** ”窗口。

   :::image type="content" source="../assets/images/collaboration-control/new-app-user.png" alt-text="屏幕截图是显示新应用用户的示例":::

1. 选择 **+添加应用**。

   :::image type="content" source="../assets/images/collaboration-control/create-new-app-user.png" alt-text="屏幕截图是演示如何创建新应用用户的示例":::

1. 从搜索框中选择应用，然后再次选择“添加”。

   :::image type="content" source="../assets/images/collaboration-control/add-app-aad.png" alt-text="屏幕截图是演示如何从 Azure Active Directory 添加应用的示例":::

添加应用后，将 **业务单元****和安全角色** 设置为连接器应用程序。 选择 **“创建”** ，应用将位于列表中。 在环境中设置应用用户后，我们可以继续进行自定义连接器配置。

## <a name="custom-connector-configuration"></a>自定义连接器配置

1. 打开 PowerApps 或 Power Automate，然后选择 **“自定义连接器”** 菜单。 为协作连接器选择 **“编辑** ”。

   :::image type="content" source="../assets/images/collaboration-control/collaboration-connector.png" alt-text="自定义连接器菜单":::

1. 在“常规信息”选项卡中，输入具有 Dynamic 365 实例域 (地址的主机，而不使用 https：//) 。

   :::image type="content" source="../assets/images/collaboration-control/general-information.png" alt-text="屏幕截图是显示“常规”信息的示例":::

1. 在“安全”选项卡中，输入以下输入：

   * 客户端机密：在输入中使用保存的应用机密值。
   * 客户端 ID：Azure 应用 (客户端 ID) 。
   * 资源 URL：Dynamic 365 实例的 URL (`https://org.crm.dynamics.com/`) 。
   * 范围：与上面相同。 默认后缀 () `https://org.crm.dynamics.com/.default` 。

   :::image type="content" source="../assets/images/collaboration-control/dynamic-365-instance.png" alt-text="屏幕截图是显示 Dynamic 365 实例的示例。":::

1. 选择 **更新连接器** 以保存更改，并允许流建立连接。

   :::image type="content" source="../assets/images/collaboration-control/custom-connector.png" alt-text="他的屏幕截图是显示自定义连接器的示例。":::

## <a name="how-to-invoke-the-connector"></a>如何调用连接器  

触发器和操作是预定义的，可配置输入和输出作为工作流步骤。 使用正确的输入和输出配置将工作流步骤添加到正确的工作流位置，以定义何时调用触发器或操作。

  :::image type="content" source="../assets/images/collaboration-control/invoke-the-connector.png" alt-text="屏幕截图是演示如何调用连接器的示例。":::

### <a name="triggers-and-actions-supported-with-connector"></a>连接器支持的触发器和操作

流中支持以下触发器和操作：

* **触发器**

  1. 创建协作会话时。

      :::image type="content" source="../assets/images/collaboration-control/colab-session-created-preview.png" alt-text="创建的协作会话":::

      **范围：** 要限制的范围，哪些行可以触发流。

      **运行方式：** 正在运行的用户，用于使用调用器连接的步骤。

  1. 创建或修改任务时

      :::image type="content" source="../assets/images/collaboration-control/task-created.png" alt-text="屏幕截图是显示创建或修改任务的示例":::

      默认情况下，触发器 Planner 任务将被禁用，并且不会触发。 若要启用它，租户管理员必须完成以下步骤：

      * 在路径 Power Apps/协作控件/设置下创建支持票证。
      * 请求为协作连接器启用环境并提供环境 URL (首选) 或组织 ID。  
      * 可以将以下示例文本添加到支持请求：“为协作连接器启用环境 URL `url` ”。
      * 若要打开支持票证，请参阅 [“获取帮助 + 支持”](/power-platform/admin/get-help-support)

* **操作**

  1. 开始协作会话

      :::image type="content" source="../assets/images/collaboration-control/begin-collab-session.png" alt-text="屏幕截图是演示如何开始协作会话的示例":::

     此步骤操作为 Dataverse 业务实体创建新的协作会话：

      * **应用程序名称：** 例如，关联应用程序的名称可以是“贷款Collaboration Manager”或“用于封闭式贷款审核的Collaboration Manager”。
      * **协作根实体名称：** 例如，应用程序记录 (表名称) 的类型可以是贷款应用程序Collaboration Manager的“msfi_loanapplication”。
      * **协作根实体 ID：** 关联应用程序记录的 ID，例如贷款应用程序记录的 ID。  

      ***高级选项***

      **高级)  (元数据：** 为协作会话添加元数据。

        * **OData 类型：** 如果设置了另一个键/值，并且需要与#Microsoft.Dynamics.CRM.m365_collaborationmetadata 完全匹配，则需要提供此字段。
        * **钥匙：** 与元数据属性关联的键。
        * **价值：** 与元数据属性关联的值。

  1. 检索协作会话

      ：：image type=“content” source=“../assets/images/collaboration-control/retrieve-collab-session.png“ alt-text=”屏幕截图是演示如何检索协作会话的示例。“：：

     此步骤操作返回与提供的输入匹配的协作会话：

     * **应用程序名称：** 协作会话的应用程序名称上下文。
     * **协作根实体 ID：** 协作会话的业务实体 ID。  
     * **协作根实体名称：** 协作会话的业务实体类型。

  1. 更新协作会话

      :::image type="content" source="../assets/images/collaboration-control/update-collab-session.png" alt-text="屏幕截图是演示如何更新协作会话的示例。":::

     此步骤操作更新现有协作会话：

     * **协作根 ID：** 目标协作会话/根记录的 GUID。
     * **协作根实体 ID：** 协作会话引用的业务实体 ID。
     * **协作根实体名称：** 协作会话引用的业务实体类型名称。

     ***高级选项：***

      **创建元数据 (高级) ：** 将更多元数据添加到协作会话记录。

      * **OData 类型：** 如果设置了另一个键/值，并且需要与#Microsoft.Dynamics.CRM.m365_collaborationmetadata 完全匹配，则需要提供此字段。
      * **钥匙：** 与元数据属性关联的键。
      * **价值：** 与元数据属性关联的值。

      **更新元数据 (高级) ：** 汇报协作会话记录上的现有元数据。

      * **OData 类型：** 如果设置了另一个键/值，并且需要与#Microsoft.Dynamics.CRM.m365_collaborationmetadata 完全匹配，则需要提供此字段。
      * **钥匙：** 与要更新的元数据属性关联的密钥。
      * **价值：** 与元数据属性关联的值。

      **删除高级)  (元数据：** 删除协作会话记录上的任何现有元数据。

      * **OData 类型：** 如果设置了另一个键/值，并且需要与#Microsoft.Dynamics.CRM.m365_collaborationmetadata 完全匹配，则需要提供此字段。
      * **钥匙：** 与要删除的元数据属性关联的键。

  1. 关联协作映射 (外部) 

      :::image type="content" source="../assets/images/collaboration-control/associate-collab-map.png" alt-text="屏幕截图是演示如何关联协作映射的示例。":::

     此步骤操作使用协作会话在 dataverse) 外部创建外部协作实体 (映射：

     * **协作根 ID：** 要映射到协作实体的协作会话唯一标识符。
     * **协作映射外部 ID：** 要映射的外部协作资源 ID。
     * **协作映射实体名称：** 要映射的外部协作实体类型名称。

     ***高级选项：***

     **元数据：** 为协作映射添加元数据。
     * **OData 类型：** 如果设置了另一个键/值，并且需要与#Microsoft.Dynamics.CRM.m365_collaborationmetadata 完全匹配，则需要提供此字段。
     * **钥匙：** 与元数据属性关联的键。
     * **价值：** 与元数据属性关联的值。

  1. 关联协作映射 (内部) 

      :::image type="content" source="../assets/images/collaboration-control/associate-collab-map-internal.png" alt-text="屏幕截图是演示如何在内部关联协作映射的示例。":::

     此步骤操作创建协作实体的映射 (与协作会话) dataverse 表。 内部仅用于在内部 Dataverse 实体/表之间创建映射。

     * **协作根 ID：** 要映射到协作实体的协作会话唯一标识符。
     * **协作映射实体 ID：** 要映射的 Dataverse 协作实体 ID。
     * **协作映射实体名称：** 要映射的 Dataverse 协作实体类型名称。

     ***高级选项：***

     **高级)  (元数据** 为协作映射添加元数据。

     * **OData 类型：** 如果设置了另一个键/值，并且需要与#Microsoft.Dynamics.CRM.m365_collaborationmetadata 完全匹配，则需要提供此字段
     * **钥匙：** 与元数据属性关联的密钥
     * **价值：** 与元数据属性关联的值

  1. 更新协作映射

      :::image type="content" source="../assets/images/collaboration-control/update-collab-map.png" alt-text="屏幕截图是演示如何更新协作映射的示例。":::

     此步骤操作更新现有协作映射：

     * **协作映射 ID：** 要更新的协作映射唯一标识符。
     * **协作映射实体 ID：** 要映射的协作实体 ID。 如果提供了外部 ID，则此值必须为空
     * **协作映射实体名称**
     * **协作映射外部 ID：** 要映射的外部协作资源 ID。 如果提供了实体 ID，则此值必须为空。  

     ***高级选项：***

     **创建元数据：** 将更多元数据添加到协作映射记录。

     * **OData 类型：** 如果设置了另一个键/值，并且需要与#Microsoft.Dynamics.CRM.m365_collaborationmetadata 完全匹配，则需要提供此字段。
     * **钥匙：** 与元数据属性关联的键。
     * **价值：** 与元数据属性关联的值。

     **更新元数据：** 汇报协作映射记录上的现有元数据。

     * **OData 类型：** 如果设置了另一个键/值，并且需要与#Microsoft.Dynamics.CRM.m365_collaborationmetadata 完全匹配，则需要提供此字段
     * **钥匙：** 与要更新的元数据属性关联的密钥
     * **价值：** 与元数据属性关联的值

     **删除元数据：** 删除协作映射记录上的任何现有元数据。

     * **OData 类型：** 如果设置了另一个键/值，并且需要与#Microsoft.Dynamics.CRM.m365_collaborationmetadata 完全匹配，则需要提供此字段。
     * **钥匙：** 与要删除的元数据属性关联的键。

  1. 获取协作元数据

      :::image type="content" source="../assets/images/collaboration-control/get-collab-metadata.png" alt-text="屏幕截图是演示如何获取协作元数据的示例。":::

     此步骤操作列出了与指定筛选器匹配的所有元数据。

     **滤波器：** 要应用于元数据查询的筛选器。
     检索与协作映射实体 ID 相关的所有元数据的示例  
     m365_entityname eq “m365_collaborationmap” 和 m365_entityid eq “GUID”

  1. 创建 Planner 任务

      :::image type="content" source="../assets/images/collaboration-control/create-planner-task.png" alt-text="屏幕截图是演示如何创建规划器任务的示例。":::

     此步骤操作使用协作控制 Planner 任务虚拟表创建 Graph Planner 任务：

     * **协作根 ID (必需) ：** 协作会话唯一标识符
     * **计划 ID (必需) ：** 任务所属的计划 ID
     * **游戏 (必需) ：** 任务的标题
     * **作业：** 一个 json 格式化对象，表示任务的所有分配。 请参阅 [plannerAssignments 资源类型](/graph/api/resources/plannerassignments)
     * **Bucket ID：** 任务所属的存储桶 ID。
     * **优先权：** 任务的优先级。 0 和 10 (非独占) 增加值优先级较低。

     ***高级选项：***

     * **活动清单项计数** (高级) ：值设置为 false 的清单项数，表示不完整的项。
     * **应用的类别：** 一个 json formatter 对象，表示要为任务应用的所有类别。 请参阅 [plannerAppliedCategories 资源类型](/graph/api/resources/plannerappliedcategories)。
     * **分配者优先级：** 用于在列表视图中对此类项进行排序的字符串值提示。 请参阅 [Planner 中的订单提示](/graph/api/resources/planner-order-hint-format)
     * **清单项计数：** 任务上存在的清单项数。
     * **完成者：** 一个 json 格式化对象，表示完成任务的用户的标识。 请参阅 [identitySet 资源类型](/graph/api/resources/identityset)
     * **对话线程 ID：** 任务上会话的线程 ID。 这是在组中创建的会话线程对象的 ID。
     * **创建者：** 一个 json 格式化对象，表示创建任务的用户的标识。 请参阅 [identitySet 资源类型](/graph/api/resources/identityset)
     * **截止日期时间：** 任务到期的日期和时间。 时间戳类型表示采用 ISO 8601 格式的日期和时间信息，始终采用 UTC 时区。 例如，2014 年 1 月 1 日午夜 UTC 为 2014-01-01T00：00：00Z。
     * **订单提示：** 用于在列表视图中订购此类项的提示。 使用 [Planner 中的顺序提示](/graph/api/resources/planner-order-hint-format)定义格式。
     * **完成百分比：** 任务完成百分比 (0-100) 
     * **预览类型：** 这会设置任务上显示的预览版类型。 可能的值为：自动、noPreview、清单、说明、引用。
     * **引用计数：** 任务上存在的外部引用数。
     * **开始日期时间：** 任务开始的日期和时间。 时间戳类型表示采用 ISO 8601 格式的日期和时间信息，始终采用 UTC 时区。 例如，2014 年 1 月 1 日午夜 UTC 为 2014-01-01T00：00：00Z。

  1. 获取 Planner 任务

      :::image type="content" source="../assets/images/collaboration-control/get-planner-task.png" alt-text="屏幕截图是显示 get Planner 任务的示例。":::

     此步骤操作使用协作控制 Planner 任务虚拟表返回 Planner 任务数据：

     **任务 ID (必需) ：** 任务唯一标识符

  1. 更新 Planner 任务

      :::image type="content" source="../assets/images/collaboration-control/update-planner-task-preview.png" alt-text="更新 planner 任务":::

     此步骤操作使用协作控制 Planner 任务虚拟表更新规划器任务记录

     * **任务 ID (必需) ：** 任务唯一标识符。
     * **作业：** 一个 json 格式化对象，表示任务的所有分配。 看。 plannerAssignments 资源类型 - Microsoft Graph v1.0 |Microsoft Docs  
     * **Bucket ID：** 任务所属位置的存储桶 ID。  
     * **Planner 任务详细信息：** 表示有关任务的其他信息。
     * **截止日期时间：** 任务到期的日期和时间。 时间戳类型表示采用 ISO 8601 格式的日期和时间信息，始终采用 UTC 时区。 例如，2014 年 1 月 1 日午夜 UTC 为 2014-01-01T00：00：00Z。
     * **优先权：** 任务的优先级。 0 和 10 (非独占) 增加值优先级较低。  
     * **完成百分比：** 任务完成百分比 (0-100) 
     * **标题：** 任务的标题

     ***高级选项：***

     * **应用的类别：** 一个 json 格式化对象，表示要为任务应用的所有类别。 请参阅 [plannerAppliedCategories 资源类型](/graph/api/resources/plannerappliedcategories)。
     * **分配者优先级：** 用于在列表视图中对此类项进行排序的字符串值提示。 请参阅， [在 Planner 中使用订单提示](/graph/api/resources/planner-order-hint-format)。
     * **对话线程 ID：** 任务上会话的线程 ID。 这是在组中创建的会话线程对象的 ID。
     * **协作根 ID：** 协作会话唯一标识符。
     * **订单提示：** 用于在列表视图中订购此类项的提示。 此处将格式定义为大纲。
     * **开始日期时间：** 任务开始的日期和时间。 时间戳类型表示采用 ISO 8601 格式的日期和时间信息，始终采用 UTC 时区。 例如，2014 年 1 月 1 日午夜 UTC 为 2014-01-01T00：00：00Z。

**示例流方案**

下面是流的一些示例：

1. 从 Microsoft 表单获取响应，创建协作会话和关联的任务。

   :::image type="content" source="../assets/images/collaboration-control/response-submitted.png" alt-text="屏幕截图是演示如何提交新响应的示例。":::

1. 每次创建协作会话时，捕获详细信息并发送电子邮件通知。

   :::image type="content" source="../assets/images/collaboration-control/colab-session-created-preview.png" alt-text="屏幕截图是显示创建的协作会话的示例":::

> [!NOTE]
> 可以通过这种方式触发多个流，以使用协作会话创建响应中的数据执行不同的操作。
