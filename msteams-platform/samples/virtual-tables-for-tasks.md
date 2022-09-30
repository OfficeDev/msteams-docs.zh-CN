---
title: 协作控制应用中任务、会议和文件的虚拟表
author: surbhigupta
description: 在本模块中，了解 Microsoft Teams 中协作控制应用中任务、会议和文件的虚拟表。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 2571787d5fba47c4ada3765dd13dd36ef1f8f63a
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243043"
---
# <a name="virtual-tables-for-tasks-meetings-files"></a>任务、会议、文件的虚拟表

此版本的新功能是一组虚拟表。 这些功能使开发人员能够通过 OData API 与 Graph 交互。

协作控制核心解决方案包括一组 [虚拟表](/power-apps/developer/data-platform/virtual-entities/get-started-ve)，可用于以编程方式访问协作控件创建的数据。

> [!NOTE]
> 目前，协作控件仅在 [公共开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中可用。

> [!TIP]
> [虚拟表](/power-apps/developer/data-platform/virtual-entities/get-started-ve) 也称为虚拟实体，通过将该数据无缝地表示为 Microsoft Dataverse 中的表来实现驻留在外部系统中的数据的集成，而无需复制数据，而且通常无需自定义编码。

协作控件使用的外部系统是 Microsoft Graph。 有用于组日历事件、预订约会、规划程序计划或任务以及 SharePoint 驱动器、文件夹和文件的虚拟表。

本文提供示例，演示如何使用 Dataverse REST API 访问虚拟表，以执行 CRUD (创建、读取、更新和删除) 操作。

> [!TIP]
> 有关 Dataverse REST API 的详细信息，请参阅 [使用 Microsoft Dataverse Web API](/power-apps/developer/data-platform/webapi/overview)。

* 虚拟表使用标准 Dataverse Web API，这样就可以轻松地使用虚拟表填充应用程序中的数据。
* 虚拟表实现支持协作控件所需的复杂工作流，这些工作流在 Microsoft 数据中心内执行，以获得最佳性能。  
* 虚拟表使用标准 Dataverse 日志记录和监视功能。

安装协作控件后，可将虚拟表视为应用程序可以依赖的另一项服务。

:::image type="content" source="~/assets/images/collaboration-control/vt-overview.png" alt-text="虚拟表概述":::

**先决条件**

若要遵循本文，需要：

1. 已安装协作控件的 Dataverse 环境。
1. Dataverse 环境中的用户帐户，其中分配了 **协作控制用户** 角色。
1. 第三方工具（例如，Post man 或一些自定义 C# 代码）允许你对 Microsoft Dataverse 实例进行身份验证，并撰写和发送 Web API 请求并查看响应。  

> [!TIP]
> Microsoft 提供有关如何配置连接到 Dataverse 实例的 Postman 环境以及如何使用 Postman 使用 Web API 执行操作的信息。 请参阅 [将 Postman 与 Microsoft Dataverse Web API 配合使用](/power-apps/developer/data-platform/webapi/use-postman-web-api)。

## <a name="virtual-tables-sample-scenario"></a>虚拟表示例方案

本指南中介绍的方案使用 Planner 计划和任务虚拟表。 所述方案与任务协作控件使用的方案相同。 从用户的角度来看，该方案演示如何创建 Planner 计划和多个任务并与特定业务记录相关联。 此方案继续演示如何检索与业务记录关联的任务，以及如何读取、更新和删除特定的规划器任务。

下面的序列图说明了客户端之间的交互，即任务协作控制、 [协作 API](/rest/api/industry/collaboration-controls/) 以及 Planner 计划和任务虚拟表。

:::image type="content" source="~/assets/images/collaboration-control/vt-sequence.png" alt-text="此图显示了虚拟表的序列图。":::

## <a name="virtual-tables-basic-operations"></a>虚拟表基本操作

本部分介绍示例方案中每个步骤的 HTTP 请求和响应。

**任务 1：检索组 ID**

检索协作 [设置](~/samples/app-with-collaboration-controls.md#define-settings-for-your-collaboration)中使用的组 ID。

> [!NOTE]
> 用于在后续任务中创建计划的用户必须是此组的成员。 如果没有，你将获得 403 禁止的响应。

**任务 2：开始协作会话**

协作会话是协作根表中的记录，可用于将多个协作（例如任务、事件、约会）与业务记录相关联。

通过协作会话，可以执行与业务记录关联的日历事件列表等操作，例如检查应用程序。

# <a name="request"></a>[请求](#tab/request)

```http
    HTTP/1.1 POST https://[Organization URI]/api/data/v9.0/m365_begincollaborationsession  
```

```json
{
    "applicationName": "{{applicationName}}", 
    "collaborationRootEntityId": "{{collaborationRootEntityId}}", 
    "collaborationRootEntityName": "{{entityName}}" 
}
```

* `applicationName`：应用程序的唯一名称
* `collaborationRootEntityName`：业务记录实体的名称  
* `collaborationRootEntityId`：特定业务记录的主键 (ID) 

# <a name="response"></a>[响应](#tab/response)

```http
    HTTP/1.1 200 OK 
```

```json
{ 
    "@odata.context": "https:// [Organization URI]/api/data/v9.0/$metadata#Microsoft.Dynamics.CRM.m365_begincollaborationsessionResponse", 
    "collaborationRootId": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f" 
}
```

---

`collaborationRootId`跟踪后续请求中所需的信息。

**任务 3：创建 Planner 计划**

创建 Planner 计划，并将其与上面`Group ID`创建的协作会话相关联，`collaborationRootId`

# <a name="request"></a>[请求](#tab/request1)

```http
    HTTP/1.1 POST https://[Organization URI]/api/data/v9.0/m365_graphplannerplans  
```

```json

{ 
    "m365_collaborationrootid": "{{collaborationRootId}}", 
    "m365_owner": "{{groupId}}", 
    "m365_title": "{{planTitle}}" 
}

```

* `collaborationRootId`：标识要将此计划与之关联的协作会话，使用任务 2 中的值

* `groupId`：标识拥有此计划的组，使用步骤 1 中的值

* `planTitle`：计划标题

# <a name="response"></a>[响应](#tab/response1)

```http
    HTTP/1.1 201 Created 
```

```json

{ 
    "@odata.context": "https:// [Organization URI]/api/data/v9.0/$metadata#m365_graphplannerplans/$entity", 
    "@odata.etag": "W/\"JzEtUGxhbiAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
    "m365_createdby": "{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null}", 
    "m365_createddatetime": "2022-05-16T16:58:33.1833561Z", 
    "m365_owner": "03614cef-8f5b-4265-9944-080d013c55d6", 
    "m365_title": "Multi-byte plan", 
    "m365_id": "8I6fu1kNS0elsbTxd67bi2UADnJu", 
    "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f", 
    "m365_graphplannerplanid": "5c9c3ecf-f157-0f67-dcd9-733a77ad593e", 
    "m365_details": null 
} 

```

---

`m365_id`跟踪后续请求中所需的信息。

**任务 4：创建 Planner 任务**

使用和 . 创建 Planner 任务`PlanId`。`collaborationRootId` 可以创建多个 Planner 任务，并将其与之前创建的协作会话相关联。

# <a name="request"></a>[请求](#tab/request2)

```http
    HTTP/1.1 POST https://[Organization URI]/api/data/v9.0/m365_graphplannertasks  
```

```json
{ 
    "m365_collaborationrootid": "{{collaborationRootId}}", 
    "m365_planid": "{{planId}}", 
    "m365_title": "{{taskTitle}}", 
    "m365_duedatetime": "2022-05-04T08:00:00Z", 
    "m365_assignments": "{\"me\":{\"orderHint\":\" !\",\"@odata.type\":\"#microsoft.graph.plannerAssignment\"}}" 
} 

```

* `collaborationRootId`：标识要将此计划与之关联的协作会话，使用任务 2 中的值
* `planId`：标识此任务将分配到的计划，使用上一步中的值
* `taskTitle`：任务的标题

# <a name="response"></a>[响应](#tab/response2)

```http
    HTTP/1.1 201 Created 
```

```json

{ 
    "@odata.context": "https://mwtmarkwallaceunmanaged.crm10.dynamics.com/api/data/v9.0/$metadata#m365_graphplannertasks/$entity", 
    "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
    "m365_activechecklistitemcount": 0, 
    "m365_appliedcategories": "{}", 
    "m365_assigneepriority": "8585488865579062167", 
    "m365_assignments": "{\"be330617-0e2b-48e9-8bf7-429a09c78e65\":{\"assignedBy\":{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null},\"assignedDateTime\":\"2022-05-16T16:58:47.571364+00:00\",\"orderHint\":\"8585488866179218449P`\",\"@odata.type\":\"#microsoft.graph.plannerAssignment\"}}", 
    "m365_checklistitemcount": 0, 
    "m365_createdby": "{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null}", 
    "m365_createddatetime": "2022-05-16T16:58:47Z", 
    "m365_duedatetime": "2022-05-04T08:00:00Z", 
    "m365_hasdescription": false, 
    "m365_orderhint": "8585488865579062167", 
    "m365_percentcomplete": 0, 
    "m365_priority": 5, 
    "m365_planid": "8I6fu1kNS0elsbTxd67bi2UADnJu", 
    "m365_previewtype": "automatic", 
    "m365_referencecount": 0, 
    "m365_title": "Team-oriented discrete time-frame", 
    "m365_id": "8WSKWaEqAU-aZV4h9VUn0GUALXbH", 
    "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f", 
    "m365_graphplannertaskid": "0a2115b9-8b03-90ee-b450-42005d906ce8", 
    "m365_completedby": null, 
    "m365_details": null, 
    "m365_completeddatetime": null, 
    "m365_conversationthreadid": null, 
    "m365_bucketid": null, 
    "m365_startdatetime": null 
} 

```

---

`m365_graphplannertaskid`跟踪后续请求中所需的信息。

> [!NOTE]
> 这是 `m365_graphplannertaskid` Planner Task 虚拟表中记录的主键。 对虚拟表进行与此记录交互的所有后续请求都必须使用此主键。 此操作将称为 `plannerTaskId` 本文档后续步骤。

应重复此步骤，在计划中创建多个任务。

**任务 5：检索关联的 Planner 任务**

检索与 `collaborationRootId` 之前创建的协作会话关联的关联 Planner 任务。

# <a name="request"></a>[请求](#tab/request3)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/ m365_graphplannertasks?$filter=m365_collaborationrootid eq '{{collaborationRootId}}'&$select=m365_graphplannertaskid,m365_title,m365_createddatetime  
```

* `$filter`：使用$filter系统查询通过指定协作根记录) 的 ID 来请求与协作会话 (关联的记录。
* `$select`：使用$select系统查询选项请求特定属性。

# <a name="response"></a>[响应](#tab/response3)

```http
    HTTP/1.1 200 OK 
```

```json

{ 

    "@odata.context": "https://mwtmarkwallaceunmanaged.crm10.dynamics.com/api/data/v9.0/$metadata#m365_graphplannertasks(m365_graphplannertaskid,m365_title,m365_createddatetime)", 
    "value": [ 
        { 
            "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
            "m365_graphplannertaskid": "8537731e-9414-1091-8d7d-ce5b74fc2477", 
            "m365_title": "Diverse executive core", 
            "m365_createddatetime": "2022-05-16T16:58:45Z", 
            "m365_id": "N_A2qmo3j0uvZZY1yd6V_GUADDEg", 
            "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f" 
        }, 
        { 
            "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
            "m365_graphplannertaskid": "4a89895a-050e-9165-a6e4-19c3850f22ec", 
            "m365_title": "Cloned didactic open architecture", 
            "m365_createddatetime": "2022-05-16T16:58:41Z", 
            "m365_id": "--U0zbgsO0us084C0yCyEWUALbWw", 
            "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f" 
        }, 
        { 
            "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
            "m365_graphplannertaskid": "20a08b8c-394b-b3fb-f9d1-47496df7a67b", 
            "m365_title": "Synergized zero defect interface", 
            "m365_createddatetime": "2022-05-16T16:58:43Z", 
            "m365_id": "AMn3RtbmV0m6cvkp5HKDCWUAKI0_", 
            "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f" 
        } 
    ] 
} 

```

---

跟踪 `m365_id‘s` 后续请求中所需的 ID。

**任务 6：检索 Planner 任务**

检索 Planner 任务，以便 `PlannerTaskID` 对前面创建的其中一个规划器任务执行读取操作。

# <a name="request"></a>[请求](#tab/request4)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})  
```

* `plannerTaskId`：规划器任务记录的主键是 `m365_graphplannertaskid` 属性。

# <a name="response"></a>[响应](#tab/response4)

```http
    HTTP/1.1 200 OK 
```

```json
{ 
    "@odata.context": "https://mwtmarkwallaceunmanaged.crm10.dynamics.com/api/data/v9.0/$metadata#m365_graphplannertasks/$entity", 
    "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
    "m365_activechecklistitemcount": 0, 
    "m365_appliedcategories": "{}", 
    "m365_assigneepriority": "8585488204334528131", 
    "m365_assignments": "{\"be330617-0e2b-48e9-8bf7-429a09c78e65\":{\"assignedBy\":{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null},\"assignedDateTime\":\"2022-05-17T11:20:52.0247676+00:00\",\"orderHint\":\"8585488204934840644P2\",\"@odata.type\":\"#microsoft.graph.plannerAssignment\"}}", 
    "m365_checklistitemcount": 0, 
    "m365_createdby": "{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null}", 
    "m365_createddatetime": "2022-05-17T11:20:52Z", 
    "m365_duedatetime": "2022-05-04T08:00:00Z", 
    "m365_orderhint": "8585488204334528131", 
    "m365_percentcomplete": 0, 
    "m365_priority": 5, 
    "m365_planid": "8I6fu1kNS0elsbTxd67bi2UADnJu", 
    "m365_previewtype": "automatic", 
    "m365_referencecount": 0, 
    "m365_title": "Secured content-based customer loyalty", 
    "m365_id": "SXmz1hxiOk-E3MKJUyhj0mUABvix", 
    "m365_details": "{\"@odata.context\":\"https://graph.microsoft.com/beta/$metadata#planner/tasks('SXmz1hxiOk-E3MKJUyhj0mUABvix')/details/$entity\",\"@odata.etag\":\"W/\\\"JzEtVGFza0RldGFpbHMgQEBAQEBAQEBAQEBAQEBARCc=\\\"\",\"description\":null,\"previewType\":\"automatic\",\"id\":\"SXmz1hxiOk-E3MKJUyhj0mUABvix\",\"references\":{},\"checklist\":{}}", 
    "m365_graphplannertaskid": "1b326015-bb43-945c-85bc-9b2a4ed16c73", 
    "m365_completedby": null, 
    "m365_hasdescription": null, 
    "m365_collaborationrootid": null, 
    "m365_completeddatetime": null, 
    "m365_conversationthreadid": null, 
    "m365_bucketid": null, 
    "m365_startdatetime": null 
}

```

---

`@odata.etag`跟踪属性和属性，`m365_graphplannertaskid`因为执行更新或删除操作需要这些属性。

**任务 7：更新 Planner 任务**

使用更新 Planner 任务 `PlannerTask ID` ，对上一步中创建的其中一个规划器任务执行更新操作。 若要更新规划器任务，请执行以下请求：

# <a name="request"></a>[请求](#tab/request5)

```http
    HTTP/1.1 PATCH https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

* 标头：If-Match： {{@odata.etag}}

```json

{
    "m365_title": "{{$planTitle}}" 
}   

```

* `@odata.etag`：对于任务的 Etag，必须执行读取才能检索最新版本。

* `planTitle`：更新了任务的标题

# <a name="response"></a>[响应](#tab/response5)

```http
    HTTP/1.1 204 No Content 
```

---

**任务 8：删除 Planner 任务**

删除 Planner 任务，以便 `PlannerTask ID` 对上一步中创建的其中一个规划器任务执行删除操作。 若要删除规划器任务，请执行以下请求：

# <a name="request"></a>[请求](#tab/request6)

```http
    HTTP/1.1 DELETE https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

* `@odata.etag`：对于任务的 Etag，必须执行读取才能检索最新版本。

# <a name="response"></a>[响应](#tab/response6)

```http
    HTTP/1.1 204 No Content
```

---

**任务 9：更新 Planner 任务详细信息**

使用更新 Planner 任务 `PlannerTask ID` ，对上一步中创建的其中一个规划器任务执行更新操作。

# <a name="request"></a>[请求](#tab/request7)

```http
    HTTP/1.1 PATCH https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

标头：If-Match： {{@odata.etag}}

```json

{ 

    "m365_title": "{{$planTitle}}", 
    "m365_details": "{\"@odata.etag\":\"{{details.etag}}\",\"description\":\"Updated Task Description\"}" 

}   
```

* `@odata.etag`：对于任务的 Etag，必须执行读取才能检索最新的版本。
* `planTitle`：更新了任务的标题。
* `@details.etag`：对于任务详细信息，必须使用查询$select查询参数执行读取，以包含 `m365_details` 列以检索最新的版本。 此值将包含在响应的列中 `m365_details` 。 此值与此值不同， `@odata.etag` 因为在 Planner 后端中，任务及其详细信息单独存储。

# <a name="response"></a>[响应](#tab/response7)

```http
HTTP/1.1 204 No Content 
```

---

> [!NOTE]
> 可以将标头设置为 `If-Match` “*”，然后无需提供任何 etag 值，但更改将始终覆盖任务及其详细信息。

## <a name="virtual-tables-authorization"></a>虚拟表授权

以下是使用协作控件解决方案中的虚拟表发出 HTTP 请求所需的授权步骤。

### <a name="azure-app-registration"></a>Azure 应用注册

若要获取正确的持有者令牌，需要在 Azure 中注册应用。 有关应用注册的详细信息，请参阅 [注册应用](/azure/active-directory/develop/quickstart-register-app)。

1. 在Azure 门户中创建应用注册以进行身份验证。
1. 浏览到 **证书&机密**。
1. 创建新的客户端机密。

     > [!IMPORTANT]
     > 请确保复制机密值并存储以供以后使用。 离开当前页面后，将无法再次访问它。

1. 浏览到 **API 权限**。
1. 从 Dynamics CRM 添加 **user_impersonation** 委派权限。
1. 为此权限授予管理员许可。

     :::image type="content" source="../assets/images/collaboration-control/power-automate-api-permission.png" alt-text="屏幕截图是显示 Power Automate API 权限的示例":::

1. 浏览到 **清单**。
1. 将以下属性的值设置为 true：

   * oauth2AllowIdTokenImplicitFlow
   * oauth2AllowImplicitFlow

1. 选择“保存”。

     :::image type="content" source="../assets/images/collaboration-control/power-automate-manifest.png" alt-text="屏幕截图是显示 Power Automate 清单的示例":::

### <a name="powerapps-environment-permissions"></a>PowerApps 环境权限

设置应用注册后，必须在 PowerApps 环境中设置应用程序用户。 这将允许使用前面配置的正确 Dynamics 范围进行身份验证。

1. 打开 [Power Platform 管理员中心](https://admin.powerplatform.microsoft.com/)。
1. 浏览到 **“用户****应用用户”列表****Your_Environment** >  > 环境 > 。
1. 选择 **“新建应用用户** ”，然后选择 Azure 应用注册。
1. 选择 **“编辑安全角色** ”并将 **系统管理员** 角色分配给应用用户。

   1. **系统管理员** 角色用于允许任何具有较低安全角色的用户进行身份验证。 例如， **协作控制用户**。
   1. 可以通过向应用程序应用较低的角色来限制此操作。 例如， **协作控制管理员**。

     :::image type="content" source="../assets/images/collaboration-control/power-automate-admin-center.png" alt-text="屏幕截图是显示 Power automate 管理中心的示例":::

### <a name="getting-the-bearer-token"></a>获取持有者令牌

完成 Azure 应用注册和 PowerApps 环境权限后，发送以下 HTTP 请求以获取持有者令牌。

```http
POST https://login.microsoftonline.com/<AZURE_APP_TENANT_ID>/oauth2/token
```

* **Content-Type**：application/x-www-form-urlencoded
* **client_id**：<AZURE_APP_CLIENT_ID>
* **&client_secret**：<AZURE_APP_CLIENT_ID>
* **&资源**：https://\<RESOURCEURL\>/
* **&用户名**： \<USERNAME\>
* **&密码**： \<PASSWORD\>
* **&grant_type**：密码

> [!IMPORTANT]
> 请确保在资源参数上包含尾随正斜杠。 如果没有，则在调用虚拟表时会收到与 Graph 范围相关的错误。

从响应有效负载中，复制 **access_token** 属性的值。 然后，在向虚拟表发出请求时，可以将此持有者令牌作为授权标头的一部分传递。

:::image type="content" source="../assets/images/collaboration-control/power-automate-authorization.png" alt-text="屏幕截图是显示 Power 自动授权的示例":::

## <a name="virtual-tables-error-handling"></a>虚拟表错误处理

虚拟表错误处理描述了常见的错误方案以及虚拟表的响应方式。

### <a name="attempt-to-create-a-virtual-record-without-a-collaboration-session"></a>尝试在没有协作会话的情况下创建虚拟记录

每个创建虚拟记录的请求都需要有效的协作会话。  创建虚拟记录时，虚拟表将创建协作映射记录，其中包括虚拟记录主键、实体名称和外部 ID（即 Graph 资源 ID）。 此协作映射与协作会话相关联，这是协作控件跟踪与业务记录关联的协作方式。

# <a name="request"></a>[请求](#tab/request8)

```http
    HTTP/1.1 POST https://[Organization URI]/api/data/v9.0/m365_graphplannertasks  
```

```json

{ 
    "m365_planid": "{{planId}}", 
    "m365_title": "{{taskTitle}}", 
    "m365_duedatetime": "2022-05-04T08:00:00Z", 
    "m365_assignments": "{\"me\":{\"orderHint\":\" !\",\"@odata.type\":\"#microsoft.graph.plannerAssignment\"}}" 
}

```

请求 `collaborationRootId` 中缺少该属性。

# <a name="response"></a>[响应](#tab/response8)

```http
    HTTP/1.1 400 Bad Request 
```

```json

{ 
    "error": { 
        "code": "0x80048d0b", 
        "message": "Parameter 'm365_collaborationrootid' is null, empty, or white-space." 
    } 
} 

```

---

若要解决此问题，必须在创建虚拟记录时始终提供有效的 `collaborationRootId` 属性。

### <a name="attempt-to-read-a-virtual-record-without-a-collaboration-map"></a>尝试在没有协作映射的情况下读取虚拟记录

虚拟表允许你执行请求，这些请求返回虚拟记录的集合。 我们之前在本文档中看到了这一点，我们请求了与特定协作会话关联的所有规划器任务。 也可以使用如下所示的$filter系统查询来请求与特定规划器计划关联的所有规划器任务：$filter=m365_planid eq`{{planId}}`。 如果使用此类查询，将发生一个问题：将返回规划器任务的记录，这些任务与协作会话（即使用协作控件以外的方法创建的规划器任务）无关。 如果尝试读取、更新或删除此类记录，则请求将失败，因为虚拟表找不到关联的协作映射。  

# <a name="request"></a>[请求](#tab/request9)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

该 `plannerTaskId` 属性与规划器任务相关联，该任务是使用 Planner Web 接口创建的，因此没有协作映射记录。

# <a name="response"></a>[响应](#tab/response9)

```http
    HTTP/1.1 404 Not Found 
```

```json
{ 
    "error": { 
        "code": "0x80048d02", 
        "message": "A record with the specified key values does not exist in m365_collaborationmap entity" 
    }
} 
```

---

若要解决此问题，必须检查响应中的错误消息，如果该错误消息设置为上面显示的消息，则表示虚拟记录未关联。 若要为此记录创建关联，必须调用 [关联协作映射 - REST API](/rest/api/industry/collaboration-controls/collaboration-custom-ap-is/associate-collaboration-map)。

### <a name="attempt-to-read-a-virtual-record-and-the-graph-resource-has-been-deleted"></a>尝试读取虚拟记录和 Graph 资源已被删除

与上一个错误相关，需要处理 Graph 资源已删除但客户端仍具有对已删除虚拟记录的引用的情况。 如果另一个用户删除了记录，则可能会发生这种情况。 如果尝试读取、更新或删除此类记录，则请求将失败，因为虚拟表无法从 Graph 检索资源。

# <a name="request"></a>[请求](#tab/request10)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

该 `plannerTaskId` 属性与已删除的规划器任务相关联。

# <a name="response"></a>[响应](#tab/response10)

```http
    HTTP/1.1 404 Not Found 
```

```json
{ 
    "error": { 
        "code": "0x80048d02", 
        "message": "REST call failed because: Reason - NotFound, Full error - {\"error\":{\"code\":\"\",\"message\":\"The requested item is not found.\",\"innerError\":{\"date\":\"2022-05-17T16:30:51\",\"request-id\":\"b692a31a-312d-490c-8dce-d258459a0211\",\"client-request-id\":\"b692a31a-312d-490c-8dce-d258459a0211\"}}}." 
    } 
} 
```

---

此情况必须由任何客户端代码处理，因为另一个用户可以随时删除关联的 Graph 资源，从而检索虚拟记录。

### <a name="attempt-to-update-a-virtual-record-with-an-invalid-odataetag"></a>尝试使用无效的 @odata.etag 更新虚拟记录

该 `@odata.etag` 属性用于数据并发，如果其他用户已更新，则防止过度写入同一条记录。 当读取记录时，将返回当前 etag，并在更改记录之前保持有效。 etag 应包含在任何更新请求中，并在操作完成之前进行检查。 如果由于当前用户读取记录而由另一个用户更改了记录，则当前用户更新请求将失败。

如果使用相同的 @odata.etag 执行两个更新请求，则第二个请求将失败：

# <a name="request"></a>[请求](#tab/request11)

```http
    HTTP/1.1 PATCH https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

标头：If-Match： {{@odata.etag}}

```json
{
    "m365_title": "{{$planTitle}}" 
}

```

# <a name="response"></a>[响应](#tab/response11)

```http
    HTTP/1.1 409 Conflict 
```

```json
{ 
    "error": { 
        "code": "0x80048d08", 
        "message": "REST call failed because: Reason - Conflict, Full error - {\"error\":{\"code\":\"\",\"message\":\"The attempted changes conflicted with already accepted changes. Read the latest state and resolve differences.\",\"innerError\":{\"date\":\"2022-05-18T06:54:55\",\"request-id\":\"dc6cd2b7-1509-4e81-91ff-22cf35b86e18\",\"client-request-id\":\"dc6cd2b7-1509-4e81-91ff-22cf35b86e18\"}}}." 
    }
} 
```

---

### <a name="querying-for-associated-virtual-records"></a>查询关联的虚拟记录

在上述任务 5 中，介绍了如何检索关联的 Planner 任务。 所有虚拟表都支持此操作。 执行此请求时，必须包含一个 `$filter` 查询，该查询指定协作根 ID，如下所示：

# <a name="request"></a>[请求](#tab/request12)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/ m365_graphplannertasks?$filter=m365_collaborationrootid eq '{{collaborationRootId}}'&$select=m365_graphplannertaskid,m365_title,m365_createddatetime  
```

---

* 其他筛选选项不能与此 `$filter` 查询结合使用，如果存在，则会忽略这些选项。
* 必须直接对来自请求的响应执行其他筛选。

### <a name="querying-for-virtual-records-with-required-key-attributes"></a>查询具有所需密钥属性的虚拟记录

当调用 Dataverse Web API 以从以下虚拟表中检索多个记录时，需要必需的密钥属性。 Graph Booking Appointments 要求查询中包含有效 `m365_bookingbusinessid` 内容。 如果未提供密钥属性，则请求将失败，如下所示：

# <a name="response"></a>[响应](#tab/response13)

```http
    HTTP/1.1 400 Bad Request 
```

```json

{ 
  "error": { 
    "code": "0x80048d0b", 
    "message": "Key attribute is missing: 'm365_bookingbusinessid'.", 
    ….
  } 
} 

```

---

若要解决此问题，请将请求更改为以下格式：

# <a name="request"></a>[请求](#tab/request14)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/ m365_graphbookingappointments?$filter=m365_bookingbusinessid eq '{{bookingBusinessId}}'
```

---

### <a name="creating-virtual-records-and-graph-access-control"></a>创建虚拟记录和图形访问控制

虚拟表遵循为 Microsoft Graph 指定的访问控制。 虚拟表不允许用户无法使用 Microsoft 图形 API 执行的操作。 例如，如果用于创建计划的用户是任务 3，并且不是你使用的组的成员，则会收到 403 个禁止的响应。
