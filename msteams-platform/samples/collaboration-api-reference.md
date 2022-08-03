---
title: 协作控制和设置 REST API 参考
author: surbhigupta
description: 在本模块中，了解用于管理设置、启动、映射和检索协作活动的协作控制和设置 REST API 引用。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: bc0a5e6834077e199c1dff26568ef2acfeb72745
ms.sourcegitcommit: 0bb822b30739e4a532a36764dad2dbf35a81ba29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2022
ms.locfileid: "67178841"
---
# <a name="collaboration-control-and-settings-rest-api-reference"></a>协作控制和设置 REST API 参考

开发人员可以使用协作控件和设置 REST API 来管理设置、启动、映射和检索与其自己的业务模型实体的协作活动。

> [!NOTE]
> 目前，协作控件仅在 [公共开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中可用。

本文提供协作控制解决方案 REST API 的参考。

## <a name="rest-operations-collaboration---custom-api"></a>REST 操作：协作 - 自定义 API

|操作|说明|
|---------|-----------|
|[关联协作映射](/rest/api/industry/collaboration-toolkit/collaboration-custom-ap-is/associate-collaboration-map)|将协作实体关联到协作会话。|
|[开始协作会话](/rest/api/industry/collaboration-toolkit/collaboration-custom-ap-is/begin-collaboration-session)|创建链接到业务实体、应用程序上下文和可选元数据的协作会话记录。|
|[取消关联协作映射](/rest/api/industry/collaboration-toolkit/collaboration-custom-ap-is/disassociate-collaboration-map-custom-api)|从给定的协作会话中取消关联映射实体。|
|[检索协作地图](/rest/api/industry/collaboration-toolkit/collaboration-custom-ap-is/retrieve-collaboration-maps-custom-api)|获取特定实体类型的会话的协作映射列表。|
|[检索协作会话](/rest/api/industry/collaboration-toolkit/collaboration-custom-ap-is/retrieve-collaboration-session-custom-api)|根据提供的参数获取协作会话记录。|
|[更新协作映射](/rest/api/industry/collaboration-toolkit/collaboration-custom-ap-is/update-collaboration-map-custom-api)|汇报协作映射记录及其元数据（如果提供）。|
|[更新协作会话](/rest/api/industry/collaboration-toolkit/collaboration-custom-ap-is/update-collaboration-session)|汇报协作会话记录及其元数据（可选）。|

## <a name="rest-operations-collaboration---standard-odata-apis"></a>REST 操作：协作 - 标准 OData API

|操作|说明|
|---------|-----------|
|[按 ID 获取协作映射](/rest/api/industry/collaboration-toolkit/collaboration-standard-o-data-ap-is/get-collaboration-map-by-id)|从协作映射记录中获取详细信息。|
|[获取协作元数据](/rest/api/industry/collaboration-toolkit/collaboration-standard-o-data-ap-is/get-collaboration-metadata)|获取给定协作映射或协作根实体名称的协作元数据记录列表。|
|[获取协作根](/rest/api/industry/collaboration-toolkit/collaboration-standard-o-data-ap-is/get-collaboration-root)|列出创建的所有协作会话。|

## <a name="rest-operations-settings---custom-apis"></a>REST 操作：设置 - 自定义 API

|操作|说明|
|---------|-----------|
|[创建和更新设置](/rest/api/industry/collaboration-toolkit/settings-custom-ap-is/create-update-setting-custom-api)|创建或更新与组路径和设置定义名称匹配的设置。|
|[检索 Null 设置](/rest/api/industry/collaboration-toolkit/settings-custom-ap-is/retrieve-null-settings-custom-api)|返回没有值的设置定义的列表。|
|[检索设置](/rest/api/industry/collaboration-toolkit/settings-custom-ap-is/retrieve-settings-custom-api)|返回组中特定设置或设置的列表。|

## <a name="rest-operations-settings---standard-odata-apis"></a>REST 操作：设置 - 标准 OData API

|操作|说明|
|---------|-----------|
|[删除设置定义](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/delete-settings-definition)|删除设置定义。|
|[删除设置组](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/delete-settings-group)|删除设置组。|
|[删除设置类型](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/delete-settings-type)|删除设置类型。|
|[删除设置值](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/delete-settings-value)|删除设置值。|
|[获取设置定义](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/get-settings-definitions)|列出设置定义。|
|[获取设置组](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/get-settings-groups)|列出设置组。|
|[获取设置类型](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/get-settings-types)|列出设置类型。|
|[获取设置值](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/get-settings-value)|列出设置值。|
|[修补程序设置定义](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/patch-settings-definition)|汇报设置定义。|
|[修补程序设置组](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/patch-settings-group)|汇报设置组。|
|[修补程序设置类型](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/patch-settings-type)|汇报设置类型。|
|[修补程序设置值](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/patch-settings-value)|汇报设置值。|
|[发布设置定义](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/post-settings-definition)|创建新的设置定义。|
|[发布设置组](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/post-settings-group)|创建新的设置组。|
|[发布设置类型](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/post-settings-type)|创建新的设置类型。|
|[发布设置值](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/post-settings-value)|创建新的设置值。|
