---
title: 虚拟表 Web API
author: surbhigupta
description: 在本模块中，了解 Microsoft Teams 中的虚拟表 Web API 协作控制应用、虚拟表排序和筛选。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: b15c7972dfc0152d458e4ad895ed6d4f7e45cd4c
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243547"
---
# <a name="virtual-tables-web-api"></a>虚拟表 Web API

使用 Dataverse Web API 从虚拟表检索多个记录时，可以包含其他查询参数，以支持排序、筛选和分页。 协作控制虚拟表不统一支持这些功能，因为它们依赖于 Microsoft 图形 API 提供的支持。 有关每个虚拟表支持的详细信息，请参阅虚拟表实体参考。

> [!NOTE]
> 目前，协作控件仅在 [公共开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中可用。

## <a name="virtual-table-sorting"></a>虚拟表排序

使用虚拟表，可以使用 OData $orderby查询参数来设置结果集的排序条件。 使用 asc 或 desc 后缀分别指定升序或降序。 如果未应用后缀，默认值将升序。  

**支持的表**：每个虚拟表都支持与相应的 Graph 资源相同的排序功能。 支持排序的虚拟表包括：  

* 图形驱动器项
* 图形事件

> [!NOTE]
> 不支持对相应 Graph 资源的所有属性进行排序。 如果用户尝试对具有不受支持的属性的虚拟表进行排序，则此结果集将具有默认顺序。 这与不支持排序的列上的 Dataverse Web API 的行为相同。

示例：

* GET [组织 URI]/api/data/v9.2/m365_graphdriveitems？$filter=m365_collaborationrootid eq '00000000-0000-0000-00000-00000000000000'&$orderby=m365_name desc
* GET [组织 URI]/api/data/v9.2/m365_graphevents？$filter=m365_groupid eq '00000000-0000-0000-00000-00000000000000'$orderby=m365_subject asc

## <a name="virtual-table-filtering"></a>虚拟表筛选

使用虚拟表，可以使用 OData $filter查询参数来设置返回行的条件。 使用 Dataverse Web API 支持的相同 OData 运算符查询虚拟表。

* **比较运算符**

  |运算符|说明|示例|
  |----|----|----|
  |eq|等于|$filter=m365_name eq 'Contoso'|
  |ne|不相等|$filter=m365_name ne 'Contoso'|
  |gt|大于|$filter=m365_price gt 50.0|
  |ge|大于或等于|$filter=m365_price ge 50.0|
  |lt|小于|$filter=m365_price lt 50.0|
  |le|小于或等于|$filter=m365_price le 50.0|

* **逻辑运算符**：逻辑运算符将一个或多个比较运算符捆绑在一起，并要求筛选器查询计算整个语句。

  |运算符|说明|示例|
  |----|----|----|
  |和|逻辑与 |$filter=m365_name eq “Contoso” 和 m365_price eq 50.0|
  |或|逻辑或 |$filter=m365_name ne 'Contoso' 或 m365_price eq 50.0|
  |
not|逻辑协商 |$filter=不包含 (m365_name，'Contoso') |

* **分组运算符**

  |运算符|说明|示例|
  |----|----|----|
  |( )|优先级分组 |$filter= (m365_name eq “Contoso” 和 m365_price eq 50.0) 或包含 (m365_subject，“Team Sync”) |

* **查询函数**

  |函数 |示例 |
  |----|----|
  |contains|$filter=包含 (m365_name，'Contoso') |
  |endswith|$filter=endswith (m365_name，'Contoso') |
  |startswith|$filter=startswith (m365_name，'Contoso') |

**支持的表**：每个虚拟表都支持与相应的 Graph 资源相同的筛选功能。 支持筛选的虚拟表包括：

* 图形预订约会
* 图形驱动器项
* 图形事件

> [!Note]
> 各自 Graph 资源的所有属性不支持筛选。 如果用户尝试使用不受支持的属性筛选虚拟表，则忽略此筛选器。 这与不支持筛选的列上的 Dataverse Web API 的行为相同。

示例：

* GET [组织 URI]/api/data/v9.2/m365_graphbookingappointments？$filter=m365_bookingbusinessid eq 'ContosoBank@Contoso.onmicrosoft.com' 和 m365_price eq 100.0
* GET [组织 URI]/api/data/v9.2/m365_graphdriveitems？$filter=m365_collaborationrootid eq '0000000-0000-0000-00000-00000000000000'，m365_name eq 'Meeting Notes.docx'
* GET [组织 URI]/api/data/v9.2/m365_graphevents？$filter=m365_groupid eq '00000000-0000-0000-00000-00000000000000'，m365_subject eq 'Monthly Sync'

## <a name="virtual-table-pagination"></a>虚拟表分页

分页是提取大量记录的有用资源。 可以通过三种不同的方式实现虚拟表分页。

可以使用 `odata.maxpagesize` 请求标头中的首选项值来指定页面大小。 如果结果集跨多个页面，则响应包括属性 `@odata.nextLink` 。 示例请求和响应如下所示：

# <a name="request"></a>[请求](#tab/request)

```http
  GET [Organization URI]/api/data/v9.2/m365_graphdriveitems 
  Accept: application/json 
  Prefer: odata.maxpagesize=2 
```

# <a name="response"></a>[响应](#tab/response)

```json
{ 

  "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#m365_graphdriveitems", 
  "value": [ 
   { 
      "@odata.etag": "W/\"{FA93AF7C-1F45-4714-85A5-BB95EB86E1E5}\"", 
      "m365_name": "Review.doc", 
      "m365_graphdriveitemid": "f50aae23-6644-3d35-66d7-e3c5a979dad3", 
      …
      },
      {
      "@odata.etag": "W/\"{3938D549-1AEF-46A5-BF3C-38472AD934C2}\"", 
      "m365_name": "Review.doc", 
      "m365_graphdriveitemid": "3d59a7e2-ec83-d0b3-270e-8ad676622027", 
      … 
      } 
      ],
      "@odata.nextLink": "[Organization URI]/api/data/v9.0/m365_graphdriveitems &$skiptoken=%3Ccookie%20pagenumber=%222%22%20pagingcookie=%22UGFnZWQ9VFJVRSZwX1NvcnRCZWhhdmlvcj0xJnBfRmlsZUxlYWZSZWY9dGVzdCZwX0lEPTI5%22%20istracking=%22False%22%20/%3E" 
} 
```

---

目前，以下虚拟表支持首选 `odata.maxpagesize` 项：

* 图形预订约会
* 图形日历事件
* 图形驱动器
* 图形驱动器项

可以通过在 URL 中传递 `$top` 选项来指定要返回的记录数。 如果还需要指定页码，则可以通过将分页 Cookie 作为 XML 编码的字符串作为 `$skiptoken` 选项传递来执行此操作。 若要提取特定页码，可以采用以下格式传递分页 Cookie：

  `<cookie pagenumber=3 />`

# <a name="request"></a>[请求](#tab/request1)

```http
     GET [Organization URL]/api/data/v9.2/m365_graphevents?$top=2&$skiptoken=<cookie pagenumber='3' /> 
```

# <a name="response"></a>[响应](#tab/response1)

```json

{
  "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#m365_graphevents", 
  "value": [
   { 
      "@odata.etag": "W/\"{FA93AF7C-1F45-4714-85A5-BB95EB86E1E5}\"", 
      "m365_graphdeventid": "3d59a7e2-ec83-d0b3-270e-8ad676622027", 
      "m365_subject": "Important meeting", 
      …
    }, 
    {
      "@odata.etag": "W/\"{3938D549-1AEF-46A5-BF3C-38472AD934C2}\"", 
      "m365_graphdeventid": "f50aae23-6644-3d35-66d7-e3c5a979dad3", 
      "m365_subject": "Another important meeting", 
      …
    } 
  ] 
}

```

---

> [!Note]
> 响应将不包括该 `@nextLink` 属性。 如果用例要求返回下一页链接，则可以使用第 1 节中所述的 odata.maxpagesize 首选项标头，而不是传递$top URI 参数。

目前，以下虚拟表支持提取特定页面：

* 图形预订约会
* 图形日历事件

可以将提取 XML 作为 XML 编码的字符串传递。 使用提取 XML 选项，可以指定多个查询首选项。 分页特定选项是页 (页码) 和计数 (页大小) 。 以下 XML 指定页码和大小：

  `<fetch version="1.0" mapping="logical" returntotalrecordcount="true" page="<Page Number>" count="<Page Size>"></fetch>`

# <a name="request"></a>[请求](#tab/request2)

```http
GET [Organization URL]/api/data/v9.2/m365_graphevents?$fetchXml=<fetch version="1.0" mapping="logical" returntotalrecordcount="true" page="3" count="2"></fetch> 

```

# <a name="response"></a>[响应](#tab/response2)

```json
{ 

    "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#m365_graphdevents", 
    "@Microsoft.Dynamics.CRM.fetchxmlpagingcookie": "<cookie pagenumber=\"3\" pagingcookie=\"\" istracking=\"False\" />", 
    "value": [ 
        { 
            "@odata.etag": "W/\"{FA93AF7C-1F45-4714-85A5-BB95EB86E1E5}\"", 
            "m365_graphdeventid": "3d59a7e2-ec83-d0b3-270e-8ad676622027", 
            "m365_subject": "Important meeting", 
            …
        }, 
        { 
            "@odata.etag": "W/\"{3938D549-1AEF-46A5-BF3C-38472AD934C2}\"", 
            "m365_graphdeventid": "f50aae23-6644-3d35-66d7-e3c5a979dad3", 
            "m365_subject": "Another important meeting", 
            …
        } 
    ] 
} 

```

---

以下虚拟表支持要作为 fetchXml 选项的一部分传递的 count 属性：

* 图形驱动器
* 图形驱动器项

以下虚拟表支持页面属性作为 fetchXml 选项的一部分：

* 图形预订约会
* 图形日历事件
