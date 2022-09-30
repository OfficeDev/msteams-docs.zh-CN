---
title: 虚拟表实体引用
author: surbhigupta
description: 在本模块中，了解 Microsoft Teams 中的虚拟表实体引用及其属性。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 98e9ee6a2bc565c35a9b46c2990a7c548dab2e31
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243050"
---
# <a name="virtual-tables-entity-reference"></a>虚拟表实体引用

协作控制虚拟实体及其属性具有具有特定 Microsoft Graph 资源类型的一对一映射。 例如，Graph Planner 任务实体映射到 [Microsoft Graph Planner 任务资源类型](/graph/api/resources/plannertask)。 虚拟实体与资源类型共享相同的属性。

> [!NOTE]
> 目前，协作控件仅在 [公共开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中可用。

## <a name="collaboration-controls-virtual-entities"></a>协作控制虚拟实体

| 名称 | 说明 |
|---|---|
| Graph Planner 任务 | Graph Planner 任务表表示 Microsoft 365 中的 Planner 任务。 |
| Graph Planner Plan | Graph Planner Plan 表表示 Microsoft 365 中的 Planner 计划。 |
| 图形事件 | Graph 事件表表示用户日历中的事件或 Microsoft 365 组的默认日历。 |
| 图形预订约会 | Graph 预订约会表表示预订服务的客户约会，由一组工作人员执行，由Microsoft Bookings企业提供。 |
| 图形驱动器 | Graph 驱动器表表示表示用户的 OneDrive 或 SharePoint 中的文档库的顶级对象。 |
| 图形驱动器项 | Graph 驱动器项表表示存储在驱动器中的文件、文件夹或其他项。 |

## <a name="graph-planner-task"></a>Graph Planner 任务

* 实体名称：m365_graphplannertask。
* 图形资源： [plannerTask 资源类型](/graph/api/resources/plannertask)
* 不支持排序。
* 不支持筛选。
* 支持服务器驱动的分页，最大页面大小为 400。

### <a name="attributes-for-graph-planner-task"></a>Graph Planner 任务的属性

| Column  | Dataverse 类型 | 详细信息 |
|---|---|---|
| `m365_collaborationrootid` | String | 协作会话记录的协作根 ID 与多个协作会话相关联。 这会以逗号分隔字符串形式返回。 请注意，检索多个记录时不会返回此属性。 |
| `m365_activechecklistitemcount` | Int32 | 值设置为 false 的清单项数，表示不完整的项。 |
| `m365_graphplannertaskId` | Guid | 图形规划器任务的唯一标识符。 |
| `m365_appliedcategories` | String | 值设置为 false 的清单项数，表示不完整的项。 |
| `m365_appliedcategories` | String | 任务已应用到的类别。 此属性是 JSON 编码的字符串，例如“{ \"category1\"： true， \"category6\"： true， \"category9\"： true }” |
| `m365_assigneepriority` | String | 用于在列表视图中订购此类项的提示。 使用 [Planner 中的顺序提示](/graph/api/resources/planner-order-hint-format)定义格式。 |
| `m365_assignments` | String | 分配给任务的被分配者集。 此属性是 JSON 编码的字符串，例如“{\" 7be...\"： {\"assignedBy\"： {\"user\"： {\"displayName\"， email\"， \"\"ID\"：\" 7be...\"}， \"group\"： null， \"application\"： null \"device\"： null}” |
| `m365_bucketid` | String | 此任务所属的存储桶 ID。 存储桶需要位于任务所在的计划中。 长度为 28 个字符，区分大小写。 [格式验证](/graph/api/resources/planner-identifiers-disclaimer)在服务上完成。 |
| `m365_checklistitemcount` | Int32 | 任务上存在的核对清单项的数目。 |
| `m365_completedby` | String | 完成任务的用户的身份。 此属性是 JSON 编码的字符串，例如 {\"user\"： {\"displayName\"，\"ID\"：\"d55...\"}} |
| `m365_completeddatetime` | 日期时间 | 只读。 任务的“percentComplete”设置为“100”的日期和时间。 时间戳类型表示采用 ISO 8601 格式的日期和时间信息，始终采用 UTC 时区。 例如，2014 年 1 月 1 日午夜 UTC 为 2014-01-01T00：00：00Z |
| `m365_conversationthreadid` |String | 任务上会话的线程 ID。 这是在组中创建的会话线程对象的 ID。 |
| `m365_createdby` | String | 创建任务的用户的身份 此属性是 JSON 编码的字符串，例如 {\"user\"： {\"displayName\"，\"ID\"：\"d55...\"}} |
| `m365_createddatetime` | 日期时间 | 只读。 创建任务的日期和时间。 时间戳类型表示采用 ISO 8601 格式的日期和时间信息，始终采用 UTC 时区。 例如，2014 年 1 月 1 日午夜 UTC 为 2014-01-01T00：00：00Z |
| `m365_duedatetime` | 日期时间 | 任务截止的日期和时间。 时间戳类型表示采用 ISO 8601 格式的日期和时间信息，始终采用 UTC 时区。 例如，2014 年 1 月 1 日午夜 UTC 为 2014-01-01T00：00：00Z |
| `m365_hasdescription` | Boolean | 只读。 如果任务的详细信息对象具有非空说明，则值为 true，否则为 false。 |
| `m365_id` | String | 只读。 任务的 ID。 长度为 28 个字符，区分大小写。 [格式验证](/graph/api/resources/planner-identifiers-disclaimer)在服务上完成。|
| `m365_orderhint` | String | 用于在列表视图中订购此类项的提示。 使用 [Planner 中的顺序提示](/graph/api/resources/planner-order-hint-format)定义格式。 |
| `m365_percentcomplete` | Int32 | 任务完成百分比。 设置为 100 时，任务被视为已完成。 |
| `m365_priority` | Int32 | 任务优先级。 值的有效范围介于 0 和 10 之间，递增值的优先级较低 (0 具有最高优先级，10 的优先级最低) 。 目前，Planner 将值 0 和 1 解释为“紧急”，2、3 和 4 解释为“重要”，5、6 和 7 解释为“中等”，8、9 和 10 解释为“低”。 此外，Planner 将值 1 设置为“紧急”，3 表示“重要”，5 表示“中”，9 表示“低”。 |
| `m365_planid` | String | 任务所属的计划 ID。 |
| `m365_previewtype` | String | 这将设置显示在任务上的预览类型。 可能的值为：自动、noPreview、清单、说明、引用。 |
| `m365_referencecount` | Int32 | 任务上存在的外部引用的数量。|
| `m365_startdatetime` | 日期时间 | 任务开始的日期和时间。 时间戳类型表示采用 ISO 8601 格式的日期和时间信息，始终采用 UTC 时区。 例如，2014 年 1 月 1 日午夜 UTC 为 2014-01-01T00：00：00Z |
| `m365_title` | String |任务的标题。 主查阅列 |

## <a name="graph-planner-plan"></a>Graph Planner Plan

* 实体名称：m365_graphplannerplan。
* Graph 资源： [plannerPlan 资源类型](/graph/api/resources/plannerplan)。
* 不支持排序。
* 不支持筛选。
* 支持服务器驱动的分页，最大页面大小为 400。

### <a name="attributes-for-graph-planner-plan"></a>Graph Planner Plan 的属性

| Column  | Dataverse 类型 | 详细信息 |
|---|---|---|
| `m365_collaborationrootid` | String | 与记录关联的协作会话的协作根 ID。 如果记录与多个协作会话相关联，则会以逗号分隔字符串形式返回。 请注意，检索多个记录时不会返回此属性。|
| `m365_graphplannerplanid` |Guid |图形规划器计划的唯一标识符。|
| `m365_createdby` | String | 创建任务的用户的身份 此属性是 JSON 编码的字符串，例如 {\"user\"： {\"displayName\"，\"ID\"：\"d55...\"}} |
| `m365_createddatetime` | 日期时间 | 只读。 创建任务的日期和时间。 时间戳类型表示采用 ISO 8601 格式的日期和时间信息，始终采用 UTC 时区。 例如，2014 年 1 月 1 日午夜 UTC 为 2014-01-01T00：00：00Z |
| `m365_id` | String | 只读。 计划的 ID。 长度为 28 个字符，区分大小写。 [格式验证](/graph/api/resources/planner-identifiers-disclaimer)在服务上完成。|
| `m365_owner` | String | 拥有计划的[组](/graph/api/resources/group)的 ID。 设置后，无法更新此属性。|
| `m365_title` | String | 计划的标题。 主查阅列 |

## <a name="graph-event"></a>图形事件

* 实体名称：m365_graphevent
* 图形资源： [事件资源类型](/graph/api/resources/event)
* 以下列支持排序：
  * m365_lastmodifieddatetime
  * m365_createddatetime
  * m365_hasattachments
  * m365_importance
  * m365_responserequested
  * m365_sensitivity
  * m365_showas
  * m365_subject
* 以下列支持筛选：
  * m365_allownewtimeproposals
  * m365_lastmodifieddatetime
  * m365_createddatetime
  * m365_icaluID
  * m365_importance
  * m365_isallday
  * m365_iscancelled
  * m365_isdraft
  * m365_responserequested
  * m365_sensitivity
  * m365_showas
  * m365_subject
  * m365_type
* 支持服务器驱动的分页。

### <a name="attributes-for-graph-event"></a>Graph 事件的属性

| Column |Dataverse 类型 |详细信息 |
|---|---|---|
|`m365_collaborationrootid` |String |记录关联的协作会话的协作根。 如果记录与多个协作会话相关联，则会以逗号分隔字符串形式返回。 请注意，检索多个记录时不会返回此属性。 |
|`m365_allownewtimeproposals` |Boolean |如此，如果会议组织者允许受邀者在响应时提出新时间。 否则为 false，这是可选的。 默认值为 true。 |
|`m365_attendees` |String |事件的与会者集合。 此属性是 JSON 编码的字符串，最大长度为 15000。 例如，[{{type：required，status：{{\"response\"：\"none\"，\"time\"：\"0001-01-01T00：00：00Z\"}}，\"emailAddress\"：\"test@contoso.com\"}}]\"\"\"\"\"\" |
|`m365_body` |String |与事件相关联的邮件正文。 可以是 HTML 格式或文本格式。 此属性是 JSON 编码的字符串，最大长度为 15000。 例如 {contentType\"：\"html\"，\"content\"：\"html/html\"\"} |
|`m365_bodypreview` |String |与事件相关联的邮件预览。 文本格式。 |
|`m365_categories` |String |与事件相关联的类别。 每个类别对应于为用户定义的 outlookCategory 的 displayName 属性。 例如 [\"string\"] |
|`m365_changekey` |String |Identifies the version of the event object. Every time the event is changed, ChangeKey changes as well. This allows Exchange to apply changes to the correct version of the object. |
|`m365_createddatetime` |日期时间 |时间戳类型表示采用 ISO 8601 格式的日期和时间信息，始终采用 UTC 时区。 例如，2014 年 1 月 1 日午夜 UTC 为 2014-01-01T00：00：00Z |
|`m365_start` |日期时间 |事件的开始日期、时间和时区。 此属性是 JSON 编码的字符串，最大长度为 100。 例如 {\"dateTime\"：\"2022-01-19T11：00：00+00：00\"，\"timeZone\"：\"UTC\"}|
|`m365_end` |日期时间 |事件结束的日期、时间和时区。 此属性是 JSON 编码的字符串，最大长度为 100。 例如 {\"dateTime\"：\"2022-01-19T11：00：00+00：00\"，\"timeZone\"：\"UTC\"} |
|`m365_hasattachments` |Boolean |如果事件包含附件，则设置为 true。 |
|`m365_hideattendees` |Boolean |设置为 true 时，每个与会者只能在会议请求和会议跟踪列表中看到自己。 默认为 false。 |
|`m365_icaluid` |字符串 |跨日历事件的唯一标识符。 此 ID 对于定期系列中的每个单一事件来说是不同的。 只读。 |
|`m365_isallday`|Boolean |Set to true if the event lasts all day. If true, regardless of whether it's a single-day or multi-day event, start and end time must be set to midnight and be in the same time zone. |
|`m365_iscancelled` |布尔 |如果事件已取消，则设置为 true。 |
|`m365_id`| String |只读。 事件的 ID。 |
|`m365_isdraft` |Boolean |如果用户已在 Outlook 中更新会议，但尚未将更新发送给与会者，则设置为 true。 如果所有更改均已发送，或者如果事件是不带任何与会者的约会，则设置为 false。|
|`m365_isonlinemeeting`|Boolean|如此 如果此事件具有联机会议信息 (即 OnlineMeeting 指向 onlineMeetingInfo 资源) ，否则为 false。 默认值为 false (onlineMeeting 为 null) 。 可选。 将 isOnlineMeeting 设置为 true 后，Microsoft Graph 将初始化 onlineMeeting。 稍后，Outlook 将忽略对 isOnlineMeeting 所做的任何进一步更改，并且会议仍可联机访问。|
|`m365_isorganizer`|Boolean|如果日历所有者（通过“日历”的“所有者”属性指定）是事件的组织者（通过“事件”的“组织者”属性指定），设定为 true。 这也适用于代理人代表所有者组织事件。|
|`m365_isremindero`n|Boolean|如果设置警报以提醒用户有事件，则设置为 true。|
|`m365_lastmodifieddatetime`|日期时间|时间戳类型表示采用 ISO 8601 格式的日期和时间信息，始终采用 UTC 时区。 例如，2014 年 1 月 1 日午夜 UTC 为 2014-01-01T00：00：00Z|
|`m365_location`|String|事件的位置。 JSON 编码字符串，最大长度为 4000。 例如[{\"address\"：null，\"coordinates\"：null，\"displayName\"：\"Harry\'s Bar\"，\"locationEmailAddress\"：null，\"locationType\"：\"default\"，\"locationUri\"：null，\"uniqueId\"：\"Harry\'s Bar\"，\"uniqueIdType\"：\"private\"}|
|`m365_locations`|String|举办或参加活动的地点。 location 和 locations 属性总是相互对应。 如果更新 location 属性，locations 集合中所有以前的位置都将被删除并替换为新的 location 值。 JSON 编码字符串，长度最大为 4000。例如[{\"address\"：null，\"coordinates\"：null，\"displayName\"：\"Harry\'s Bar\"，\"locationEmailAddress\"：null，\"locationType\"：\"default\"，\"locationUri\"：null，\"uniqueId\"：\"Harry\'s Bar\"，\"uniqueIdType\"：\"private\"}]|
|`m365_onlinemeeting`|String|关于与会者如何加入联机会议的详细信息。 默认值为 Null。 只读。设置 isOnlineMeeting 和 onlineMeetingProvider 属性以启用联机会议后，Microsoft Graph 初始化 onlineMeeting。 设置后，会保持联机可用，无法再次更改 isOnlineMeeting、onlineMeetingProvider 和 onlneMeeting 属性。 JSON 编码的字符串，长度最大为 4000。例如{\"conferenceId\"： \"String\"，\"joinUrl\"： \"String\"，\"phone\"： [{\"@odata.type\"： \"microsoft.graph.phone\"}]\"，quickDial\"： \"String\"，\"tollFreeNumbers\"： [\"String\"]，\"tollNumber\"： \"String\"}|
|`m365_onlinemeetingprovider`|String|关于与会者如何加入联机会议的详细信息。 默认值为 Null。 只读。 设置 isOnlineMeeting 和 `onlineMeetingProvider` 属性以启用联机会议后，Microsoft Graph 初始化 onlineMeeting。 设置后，会保持联机可用，无法再次更改 isOnlineMeeting `onlineMeetingProvider`和 onlneMeeting 属性。|
|`m365_onlinemeetingurl`|String|联机会议的 URL。 仅当组织者在 Outlook 中将事件指定为联机会议（如 Skype）才会设置此属性。 只读。 若要访问 URL 以加入联机会议，请使用 `joinUrl`通过 `onlineMeeting` 事件属性公开的 URL。 该 `onlineMeetingUrl` 属性将在将来弃用。|
|`m365_organizer`|String|活动的组织者。JSON 编码字符串，最大长度为 4000。 {\"emailAddress\"：{\"@odata.type\"：\"microsoft.graph.emailAddress\"}}|
|`m365_originalendtimezone`|String|创建事件时设置的结束时区。 值 tzone://Microsoft/Custom 表示在桌面 Outlook 中设置了旧版自定义时区。|
|`m365_originalstart`|日期时间|表示事件最初在周期性序列中作为事件或异常创建时的开始时间。 对于单个实例的事件，不会返回此属性。 其日期和时间信息以 ISO 8601 格式表示，并且始终采用 UTC。 例如，2014 年 1 月 1 日午夜 UTC 为 2014-01-01T00：00：00Z|
|`m365_originalstarttimezone`|String|创建事件时设置的开始时区。 值 tzone://Microsoft/Custom 表示在桌面 Outlook 中设置了旧版自定义时区。|
|`m365_recurrence`|String|事件的定期模式。 JSON 编码的字符串， max 4000 in length.例如{pattern：{\"dayOfMonth\"：0，\"daysOfWeek\"：[\"monday\"，\"wednesday\"，\"friday\"]\"，firstDayOfWeek\"：\"sunday\"，\"index\"：\"first\"，\"interval\"：1，\"month\"：0，\"type\"：\"weekly\"}，\"range\"：{\"startDate\"：\"2017-08-14\"，\"endDate\"：\"2018-08-14\"，\"\"\"numberOfOccurrences\"：0，\"recurrenceTimeZone\"：\"东部标准时间\"，\"type\"：\"endDate\"}}|
|`m365_reminderminutesbeforestart`|Int32|事件开始时间（即提醒警报发生时间）之前的分钟数。|
|`m365_responserequested`|布尔值|默认值为 true，表示组织者愿意被邀请者发送事件响应。|
|`m365_responsestatus`|String|指示在事件消息的响应中发送的响应类型。 JSON 编码字符串，最大长度为 4000。{\"response\"： \"String\"，\"time\"： \"String (timestamp) \"}|
|`m365_sensitivity`|String|可能的值为：普通、个人、私人、机密。|
|`m365_seriesmasterid`|String|定期系列主项的 ID（如果此事件是定期系列的一部分）。|
|`m365_showas`|String|要显示的状态。 可能的值为：free、tentative、busy、oof、workingElsewhere、unknown。|
|`m365_subject`|String|事件的主题行文本。 主查阅列|
|`m365_transactionid`|String|客户端应用为服务器指定的自定义标识符，以避免客户端重试以创建同一事件时执行冗余 POST 操作。 当低网络连接性导致客户端在从服务器中收到客户端先前创建事件请求的响应之前超时时，此功能很有用。 创建事件时设置 `transactionId` 后，无法在后续更新中更改 transactionId。 如果应用已设置此属性，则仅在响应有效负载中返回此属性。 可选。|
|`m365_type`|String|事件类型。 可能的值为：singleInstance、occurrence、exception、seriesMaster。 只读|
|`m365_weblink`|String|要在 Web 上的 Outlook 中打开事件的 URL。 如果登录到邮箱，Outlook 网页版在浏览器中打开事件。 否则，Outlook 网页面会提示你进行登录。 无法从 iFrame 中访问此 URL。|
|`m365_grapheventid`|Guid|图形事件的唯一标识符。|
|`m365_groupid`|String|事件所属的组 ID。|

## <a name="graph-booking-appointment"></a>图形预订约会

* 实体名称：m365_graphbookingappointment
* 图形资源： [bookingAppointment 资源类型](/graph/api/resources/bookingappointment)
* 不支持排序。
* 以下列支持筛选：
  * m365_bookingbusinessID
  * m365_collaborationrootID
  * m365_customertimezone
  * m365_optoutofcustomeremail
  * m365_price
  * m365_pricetype
  * m365_serviceID
  * m365_servicename
* 不支持分页。

### <a name="attributes-for-graph-booking-appointment"></a>图形预订约会的属性

| Column  | Dataverse 类型 | 详细信息 |
|---|---|---|
| `m365_collaborationrootid`| String| 与记录关联的协作会话的协作根 ID。 如果记录与多个协作会话相关联，则会以逗号分隔字符串形式返回。 请注意，检索多个记录时不会返回此属性。|
| `m365_graphbookingappointmentid` | Guid | 图形预订约会的唯一标识符。|
| `m365_bookingbusinessid` | String | 计划约会的预订业务的唯一标识符。|
| `m365_additionalinformation` | String | 确认约会时发送给客户的额外信息。|
| `m365_customers` | String| 它列出了约会的客户属性。 约会将包含客户信息列表，每个单位将指示属于该约会的客户的属性。 可选[{\"customerID\"：\"d243c77b-f1ff-4615-a01f-1660b5cb0e79\"，\"customQuestionAnswers\"：[]，\"emailAddress\"：\"jordanm@contoso.com\"，\"location\"：{address\"：{\"city\"：\"\"，\"\"countryOrRegion\"：\"\"，\"postalCode\"：\"\"，\"postOfficeBox\"，\"state\"：\"\"，\"street\"：\"\"，\"type\" }，\"coordinates\"：{\"accuracy\"，\"altitude\"，\"altitudeAccuracy\"，\"latitude\"，\"longitude\" }，\"displayName\"：\"\"，\"locationEmailAddress\"，locationType\"，\"\"locationUri\"：\"\"，\"uniqueID，\"uniqueIDType\"\" }，\"name\"：\"Jordan Miller\"，\"notes\"，\"phone\"，\"timeZone\"，\"@odata.type\"：\"#microsoft.graph.bookingCustomerInformation\"}] |
| `m365_customertimezone` | String | 客户的时区。 有关可能值的列表，请参阅 [dateTimeTimeZone 资源类型](/graph/api/resources/datetimetimezone)。 |
| `m365_duration` | String | 约会的长度，以 ISO8601 格式表示。|
| `m365_enddatetime` | 日期时间 | 约会结束的日期、时间和时区。|
| `m365_filledattendeescount` | Int32 | 约会中的当前客户数。|
| `m365_id` | String | bookingAppointment 的 ID。 只读。|
| `m365_islocationonline` | Boolean | True 表示约会将联机进行。 默认值为 false。|
| `m365_joinweburl` | String | 约会的联机会议的 URL。|
| `m365_maximumattendeescount` | Int32 | 约会中允许的最大客户数。|
| `m365_optoutofcustomeremail` | Boolean | True 表示此约会的 bookingCustomer 不希望收到此约会的确认。|
| `m365_postbuffer` | String | 例如，约会结束后要保留的时间，用于清理。 该值以 ISO8601 格式表示。|
| `m365_prebuffer` | String | 例如，在约会开始之前，为准备而保留的时间量。 该值以 ISO8601 格式表示。|
| `m365_price` | DecimalType | 指定 bookingService 的约会的常规价格。|
| `m365_pricetype` | String | 一个设置，用于为服务的定价结构提供灵活性。 可能的值为：undefined、fixedPrice、startingAt、hourly、free、priceVaries、callUs、notSet。|
| `m365_reminders` | String | 为此约会发送的客户提醒的集合。 仅当按 ID 读取此 bookingAppointment 时，此属性的值才可用。 [{\"message\"：\"我们期待着看到你！\"，\"offset\"：\"P1D\"，\"recipients\"：\"customer\"}，{\"message\"：\"Reminder，你有约会！\"，\"offset\"：\"P1D\"，\"recipients\"：\"staff\"}] |
| `m365_selfserviceappointmentid` | String | 约会的另一个跟踪 ID（如果约会是由计划页面上的客户直接创建的，而不是由代表客户的工作人员创建的）。|
| `m365_serviceid` | String | 与此约会关联的 bookingService 的 ID。|
| `m365_servicelocation` | String | 服务的传送位置。 {\"address\"：{\"city\"：\"\"，\"countryOrRegion\"：，\"postalCode\"：\"\"\"\"，\"postOfficeBox\"，\"state\"：\"\"，\"street\"：\"\"，\"type\" }，\"coordinates\"：{\"accuracy\"，\"altitude，\"altitudeAccuracy\"\"，\"latitude\"，\"longitude\" }，\"displayName\"：\"我们的办公室地址\"，\"locationEmailAddress\"，\"locationType\"，\"locationUri\"：\"\"，\"uniqueID\"，\"uniqueIDType\" } |
| `m365_servicename` | String | 与此约会关联的 bookingService 的名称。 创建新约会时，此属性是可选的。 如果未指定，则会从 ServiceID 属性与约会关联的服务中进行计算。 |
| `m365_servicenotes` |String | bookingStaffMember 中的备注。 仅当按其 ID 读取此 bookingAppointment 时，此属性的值才可用。|
| `m365_smsnotificationsenabled` | Boolean | True 表示将向客户发送短信通知以进行约会。 默认值为 false。|
| `m365_staffmemberids` | String | 此约会中计划的每位 bookingStaffMember 的 ID。 存储为逗号分隔字符串。[\“string\”] |
| `m365_startdatetime` | 日期时间 | 约会开始的日期、时间和时区。|

## <a name="graph-drive"></a>图形驱动器

* 实体名称：m365_graphdrive
* 图形资源： [驱动器资源类型](/graph/api/resources/drive)
* 不支持排序。
* 不支持筛选。
* 支持服务器驱动的分页。

### <a name="attributes-for-graph-drive"></a>Graph 驱动器的属性

|Column |Dataverse 类型 |详细信息 |
|---|---|---|
|`m365_collaborationrootid` |String | 与记录关联的协作会话的协作根 ID。 如果记录与多个协作会话相关联，则会以逗号分隔字符串形式返回。 请注意，检索多个记录时不会返回此属性。 |
|`m365_createdby` |String |创建项的用户、设备或应用程序的标识。 只读。 此属性是 JSON 编码的字符串，例如 { “user”： { “displayName”： “System Account” } } |
|`m365_createddatetime` |日期时间 |创建项的日期和时间。 只读。 |
|`m365_description` |String |提供驱动器的用户可见说明。 只读。 |
|`m365_drivetype` |String |说明了由该资源表示的驱动器的类型。 OneDrive 个人驱动器将返回个人驱动器。 OneDrive for Business将返回业务。 SharePoint 文档库将返回 documentLibrary。 只读。 |
|`m365_graphdriveid` |Guid |图形驱动器的唯一标识符。 |
|`m365_id` |String |驱动器的唯一标识符。 只读。 |
|`m365_lastmodifiedby` | String |上次修改项的用户、设备和应用程序的标识。 只读。 此属性是 JSON 编码的字符串，例如 { “user”： { “email”： “user@contoso.com”， “ID”： “61de164e-21ff-4b1c-8cbd-77ac440894f8”， “displayName”： “User Name” } } |
|`m365_lastmodifieddatetime` |日期时间 |上次修改项目的日期和时间。 只读。|
|`m365_name` |String |项目名称。 只读。 |
|`m365_owner` |String |可选。 拥有此驱动器的用户帐户。 只读。 此属性是 JSON 编码的字符串。 例如 { “group”： { “ID”： “76c7286f-8645-4ba8-bc0f-c65a16424aaa”， “displayName”： “Group Name” }} |
|`m365_quota` |String |可选。 有关驱动器的存储空间配额的信息。 只读。 此属性是 JSON 编码的字符串。 例如 { “deleted”： 482586， “remaining”： 27487788645969， “state”： “normal”， “total”： 27487790694400， “used”： 1565845 } |
|`m365_sharepointids` |String |返回对 SharePoint REST 兼容性有用的标识符。 只读。 默认情况下不会返回此属性，必须使用$select查询参数进行选择。 此属性是 JSON 编码的字符串。 例如“sharePointIDs”： { “listID”： “29d8457a-8e26-4291-9901-09718a388aaa”， “siteID”： “93618739-b3ca-4107-a77c-fba278c48aaa”， “siteUrl”： “<https://contoso.sharepoint.com>”， “tenantID”： “53986071-de92-43ad-a41f-f3c4adb2beef”， “webID”： “a0d0e9ec-e547-4338-92d9-4c2c62e5beef” } |
| `m365_siteid` |String |包含文档库的网站的标识符。
|`m365_system` |String |如果存在，则表示这是系统管理的驱动器。 只读。
|`m365_weburl` |String |在浏览器中显示此资源的 URL。 只读。

### <a name="graph-drive-item"></a>图形驱动器项

* 实体名称：m365_graphdriveitem
* 图形资源： [driveItem 资源类型](/graph/api/resources/driveitem)
* 以下列支持排序：
  * m365_name
* 以下列支持筛选：
  * m365_name
* 支持服务器驱动的分页。

### <a name="attributes-for-graph-drive-item"></a>Graph 驱动器项的属性

|Column |Dataverse 类型 |详细信息 |
|---|---|---|
|`m365_audio` |String |音频元数据（如果此项是一个音频文件）。 只读。 仅在 OneDrive 个人版上。 此属性是 JSON 编码的字符串。 { “album”： “string”， “albumArtist”： “string”， artist“： ”string“， bitrate”： 128， “composers”： “string”， copyright“： ”string“， ”disc“： 0， ”discCount“： 0， ”duration“： 567， ”genre“： ”string“， ”hasDrm“： false， ”isVariableBitrate“： false， ”title“： ”string“， ”track“： 1， ”trackCount“： 16， ”year“： 2014 }|
|`M365_bundle` |String |捆绑包元数据（如果该项是捆绑包）。 只读。 此属性是 JSON 编码的字符串。 例如， { “childCount”： 3， “album”： { “@odata.type”： “microsoft.graph.album” }， } |
|`m365_collaborationrootid` |String |与记录关联的协作会话的协作根 ID。 如果记录与多个协作会话相关联，则会以逗号分隔字符串形式返回。 请注意，检索多个记录时不会返回此属性。 |
|`m365_copy` |String |如果请求中存在，则执行复制操作。 |
|`m365_createdby` |String |创建项的用户、设备和应用程序的标识。 只读。 此属性是 JSON 编码的字符串。 例如，{“user”：{“displayName”：“User Name”，“email”：“alias@contoso.com”，“ID”：“a298b975-3493-4d9e-b2d4-3cad78f00000”}，“group”： null，“application”，“device” } |
|`m365_createddatetime` |日期时间 |创建项的日期和时间。 只读。 |
|`m365_ctag` |String |项内容的 eTag。 如果仅更改元数据，则不会更改此 eTag。 注意。 如果项是文件夹，则不会返回此属性。 只读。 |
|`m365_deleted` |String |有关项目删除状态的信息。 只读。 此属性是 JSON 编码的字符串。 例如，{ “state”： “string” } |
|`m365_description` |String |提供项的用户可见的说明。 读写。 仅在 OneDrive 个人版上。 |
|`m365_driveid` |String |包含驱动器项的驱动器的标识符。|
|`m365_etag` |String |整个项目（元数据和内容）的 eTag。 只读。 |
| `m365_file` |String |文件元数据（如果项是文件的话）。 只读。 此属性是 JSON 编码的字符串。 例如，{“hashes”：{“crc32Hash”，“quickXorHash”：“Biuzvwdu+Tmu6yRefayD27hD9vD=”，“sha1Hash”，“sha256Hash”}，“mimeType”：“application/vnd.openxmlformats-officedocument.wordprocessingml.document”，“processingMetadata” } |
| `m365_filesysteminfo` |String |客户端上的文件系统信息。 此属性是 JSON 编码的字符串。 例如，{“createdDateTime”：“2022-07-21T15：02：47+00：00”，“lastAccessedDateTime”，“lastModifiedDateTime”：“2022-07-21T15：02：55+00：00”} |
|`m365_folder` |String | 文件夹元数据（如果此项是一个文件夹）。 只读。 此属性是 JSON 编码的字符串。 例如，{“childCount”：0，“view” } |
|`m365_graphdriveitemid` |Guid |图形驱动器项的唯一标识符。 |
|`m365_id` |String |驱动器中项的唯一标识符。 只读。 |
|`m365_image` |String |图像元数据（如果此项是一个图像）。 只读。 此属性是 JSON 编码的字符串。 例如，{“height”，“width” } |
|`m365_lastmodifiedby` |String |上次修改项的用户、设备和应用程序的标识。 只读。 此属性是 JSON 编码的字符串。 例如，{“user”：{“displayName”：“User Name”，“email”：“alias@contoso.com”，“ID”：“a298b975-3493-4d9e-b2d4-3cad78f9a00e”}，“group”，“application”，“device” } |
|`m365_lastmodifieddatetime` |日期时间 |上次修改项目的日期和时间。 只读。 |
|`m365_location` |String |位置元数据（如果此项包含位置数据）。 只读。 此属性是 JSON 编码的字符串。 例如，“location”： { “altitude”： 1.0， “latitude”： 1.0， “longitude”： 1.0 } |
|`m365_malware` |String |恶意软件元数据，如果检测到项目包含恶意软件。 只读。 此属性是 JSON 编码的字符串。 例如，{ “description”： “string” } |
|`m365_name` |String |项目名称（文件名和扩展名）。 读写。 |
|`m365_package` |String |如果存在，则表示此项是一个包，而不是文件夹或文件。 包被视为某些上下文中的文件和其他上下文中的文件夹。 只读。 此属性是 JSON 编码的字符串。 例如， { “type”： “oneNote” } |
|`m365_parentreference` |String |父信息（如果此项具有父级）。 此属性是 JSON 编码的字符串。 例如， {“driveID”：“b！qgK-8nOzX0qISvfGCiC2Smbv0m0RlNhDvNQDZsCMpbSnchFAhWAaQoiTLZcSo1gq”，“driveType”：“documentLibrary” “ID”：“01EYDCV4YHV77FE3EDDFHIVD6WJ2ETT3PP”，“name”，“path”：“/drives/b！qgK-8nOzX0qISvfGCiC2Smbv0m0RlNhDvNQDZsCMpbSnchFAhWAaQoiTLZcSo1no/root：/folder name”，“shareID”，“sharepointIDs”：{“listID”：“401172a8-6085-421a-8893-2d9712a35c3c”，“listItemID”，“listItemUniqueID”：“52feaf12-836c-4e19-8a8f-d64e8939ee52”，“siteID”：”f34e02aa-b373-4a5f-884a-f7c60a20b64a“，”siteUrl“：”https://contoso.sharepoint.com/sites/Contoso“，”tenantID“，”webID“：”6dd2ef66-9411-43d8-bcd4-0366c08ccabd“}，”siteID“ } |
|`m365_parentreferenceid` |String |作为驱动器项的父级的驱动器项的标识符。 |
|`m365_pendingoperations` |String |如果存在，则表示可能影响 driveItem 状态的一个或多个操作正在等待完成。 只读。 此属性是 JSON 编码的字符串。 例如，{ “pendingContentUpdate”： {“@odata.type”： “microsoft.graph.pendingContentUpdate”} } |
|`m365_photo` |String |照片元数据（如果此项包含照片）。 只读。 此属性是 JSON 编码的字符串。 例如， { “cameraMake”： “Camera Make”， “cameraModel”： “Camera Model”， “exposureDenominator”： 10000000， “exposureNumerator”： 41671， “focalLength”： 4.38， “fNumber”： 1.73， “iso”： 70， “orientation”： 6， “takenDateTime”： “2020-04-29T14：17：39Z” } |
|`m365_publication` |String |在支持此类操作的位置提供有关某个项目的已发布或签出状态信息。 默认情况下不会返回此属性。 只读。 此属性是 JSON 编码的字符串。 例如，{“level”：“published”，“versionID”：“2.0”} |
|`m365_remoteitem` |String |远程项目数据（如果此项是从驱动器共享的项目，而不是被访问的项目）。 只读。 此属性是 JSON 编码的字符串。 例如， { “ID”： “string”， “createdBy”： { “@odata.type”： “microsoft.graph.IdentitySet” }， “createdDateTime”： “timestamp”， “file”： { “@odata.type”： “microsoft.graph.file” }， “fileSystemInfo”： { “@odata.type”： “microsoft.graph.fileSystemInfo” }， “folder”： { “@odata.type”： “microsoft.graph.folder” }， “image”： { “@odata.type”： “microsoft.graph.image” }， “lastModifiedBy”： { “@odata.type”： “microsoft.graph.IdentitySet” }， “lastModifiedDateTime”： “timestamp”， “name”： “string”， “package”： {@odata.type“： ”microsoft.graph.package“ }， ”parentReference“： { ”@odata.type“： ”microsoft.graph.itemReference“ }， ”shared“： { ”@odata.type“： ”microsoft.graph.shared“ }， ”sharepointIDs“： { ”@odata.type“： ”microsoft.graph.sharepointIDs“ }， ”specialFolder“： { ”@odata.type“： ”microsoft.graph.specialFolder“ }， ”size“： 1024， ”video“： { ”@odata.type“： ”microsoft.graph.video“ }， ”webDavUrl“： ”url“， ”webUrl“： ”url“ } |
|`m365_root` |String |如果此属性为非 NULL，则表明 driveItem 是驱动器中最上面的 driveItem。 |
|`m365_searchresult` |String |搜索元数据（如果此项目来自搜索结果）。 只读。 此属性是 JSON 编码的字符串。 例如， { “onClickTelemetryUrl”： “url” } |
|`m365_shared` |String |表示此项已与他人共享，并提供有关项目共享状态的信息。 只读。 此属性是 JSON 编码的字符串。 例如，{ “scope”： “users”， “owner”： { “user”： { “displayName”： “User Name”， “ID”： “bbbb6fa48aaaaaaa” } } } } |
|`m365_sharepointids` |String |返回对 SharePoint REST 兼容性有用的标识符。 只读。 此属性是 JSON 编码的字符串。 e.g{“listID”：“401172a7-6085-421a-8893-2d9712a35aba”，“listItemID”：“338 ”，“listItemUniqueID”：“0edc89e5-24ea-4c6b-a019-dc51f45eeccc”，“siteID”：“f2be02aa-b37 3-4a5f-884a-f7c60a20bddd”，“siteUrl”：“https://contoso.sharepoint.com/sites/Contoso”，“tenantID”：“1c137272-0581-487f-b195-aeeb93cc4ccc”，“webID”：“6dd2ef66-9411-43d8-bcd4-0366c08caaaa”} |
|`m365_siteid` |String |包含文档库的网站的标识符。 |
|`m365_size` |IntType |项目大小，以字节为单位。 只读。 |
|`m365_specialfolder` |String |如果当前项同时也是一个特殊的文件夹，则返回此 facet。 只读。 此属性是 JSON 编码的字符串。 例如，{ “name”： “documents” } |
|`m365_thumbnail` |String |如果请求中存在，则将检索驱动器项缩略图。 |
|`m365_video` |String |如果当前项同时也是一个特殊的文件夹，则返回此 facet。 只读。 此属性是 JSON 编码的字符串。 例如，{“bitrate”：10646968、 “duration”： 1050683， “height”： 720， “width”： 1280， “audioBitsPerSample”： 16， “audioChannels”： 1， “audioFormat”： “PCM”， “audioSamplesPerSecond”： 32000， “fourCC”： “H264”， “frameRate”： 60} |
|`m365_webdavurl` |String | 项的可兼容 WebDAV 的 URL。 |
|`m365_weburl` |String |在浏览器中显示此资源的 URL。 只读。 |
