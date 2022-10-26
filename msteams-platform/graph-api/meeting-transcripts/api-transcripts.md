---
title: 使用图形 API 提取脚本
description: 介绍用于提取会议脚本的 API
ms.localizationpriority: high
ms.topic: conceptual
ms.openlocfilehash: 2142bc1346a032f27d8612f6081156d2c4927e8f
ms.sourcegitcommit: 372aade09e62ac7e5936215173a6632fbb042c9d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2022
ms.locfileid: "68699176"
---
# <a name="use-graph-apis-to-fetch-transcript"></a>使用图形 API 提取脚本

使用 Graph REST API 获取特定会议的脚本。 应用根据会议组织者的用户 ID 和会议 ID 提取脚本。

以下为用于提取脚本的 API：

- [列出 callTranscripts](#list-calltranscripts)
- [获取 callTranscript](#get-calltranscript)
- [获取 callTranscript 内容](#get-calltranscript-content)

### <a name="list-calltranscripts"></a>列出 callTranscripts

此 API 用于根据用户 ID 和会议 ID 获取所有 `callTranscript` 对象的列表。 它会返回会议脚本的元数据，其中包含脚本 ID 以及该脚本的创建日期和时间。

**HTTP 请求**

```http
GET /me/onlineMeetings('{meetingId}')/transcripts
GET /users('{userId}')/onlineMeetings('{meetingId}')/transcripts
```

**可选的查询参数**

此方法支持使用 `$skipToken` 和 `$top` [OData 查询参数 ](/graph/query-parameters) 以帮助自定义响应。

**支持的查询模式**

| 模式                | 受支持 | 语法                                 | 注释 |
| ---------------------- | ------- | -------------------------------------- | ----- |
| 服务器端分页 |     ✓     | `@odata.nextLink`                      | 当结果集跨多个页面时，在响应中获取延续标记。 |
| 页面限制             |     ✓     | `/transcripts?$top=20` | 获取页面大小为 20 的脚本。 默认页面限制为 10。 最大页面限制为 100。 |

**请求头**

| 标头       | 值 |
|:---------------|:--------|
| Authorization  | Bearer {token}. Required.  |

**请求正文**

请勿提供此方法的请求正文。

**响应**

如果成功，此方法在响应正文中返回 `200 OK` 响应代码和 `callTranscript` 对象集合。

<br>
<details>
<summary><b>示例：callTranscript 列表</b></summary>
<br>
<b>请求</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts
```

<br>
<b>响应</b>
<br>

> [!NOTE]
> 为了提高可读性，可能缩短了此处显示的响应对象。

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('ba321e0d-79ee-478d-8e28-85a19507f456')/onlineMeetings('MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ')/transcripts",
    "@odata.count": 3,
    "@odata.nextLink": "https://graph.microsoft.com/beta/users('ba321e0d-79ee-478d-8e28-85a19507f456')/onlineMeetings('MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ')/transcripts?$skiptoken=MSMjMCMjMjAyMS0wOS0xNlQxMzo1OToyNy4xMjEwMzgzWg%3d%3d",
    "value": [
        {
            "id": "MSMjMCMjZDAwYWU3NjUtNmM2Yi00NjQxLTgwMWQtMTkzMmFmMjEzNzdh",
            "createdDateTime": "2021-09-17T06:09:24.8968037Z"
        },
        {
            "id": "MSMjMCMjMzAxNjNhYTctNWRmZi00MjM3LTg5MGQtNWJhYWZjZTZhNWYw",
            "createdDateTime": "2021-09-16T18:58:58.6760692Z"
        },
        {
            "id": "MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4",
            "createdDateTime": "2021-09-16T18:56:00.9038309Z"
        }        
    ]
}
```

</details>

### <a name="get-calltranscript"></a>获取 callTranscript

应用会分析作为 `List callTranscripts` API 的响应接收的脚本 ID 列表，以获取所需的脚本 ID。 此 API 用于根据用户 ID、会议 ID 和脚本 ID 获取单个脚本元数据。

**HTTP 请求**

```http
GET me/onlineMeetings('{meetingId}')/transcripts('{transcriptId}')
GET users('{userId}')/onlineMeetings('{meetingId}')/transcripts('{transcriptId}')
```

**请求头**

| 标头       | 值 |
|:---------------|:--------|
| Authorization  | Bearer {token}. Required.  |

**请求正文**

请勿提供此方法的请求正文。

**响应**

如果成功，此方法在响应正文中返回 `200 OK` 响应代码和 `callTranscript` 对象。

<br>
<details>
<summary><b>示例：获取 callTranscript</b></summary>
<br>
<b>请求</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4
```

<br>
<b>响应</b>
<br>

> [!NOTE]
> 为了提高可读性，可能缩短了此处显示的响应对象。

```http
HTTP/1.1 200 OK
Content-type: application/json

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('ba321e0d-79ee-478d-8e28-85a19507f456')/onlineMeetings('MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ')/transcripts/$entity",
    "id": "MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4",
    "createdDateTime": "2021-09-17T06:09:24.8968037Z"
}
```

</details>

### <a name="get-calltranscript-content"></a>获取 callTranscript 内容

此 API 用于获取在响应 `Get callTranscript` API 时获取的所选脚本 ID 的脚本。 它将返回脚本的内容。

**HTTP 请求**

```http
GET me/onlineMeetings('{meetingId}')/transcripts('{transcriptId}')/content
GET users('{userId}')/onlineMeetings('{meetingId}')/transcripts('{transcriptId}')/content
```

**可选的查询参数**

此方法支持使用 `$format` [OData 查询参数](/graph/query-parameters)，允许自定义响应。

支持的格式类型为 vtt 支持 `text/vtt` 或 docx 支持 `application/vnd.openxmlformats-officedocument.wordprocessingml.document`。

**请求头**

| 标头       | 值 |
|:---------------|:--------|
| Authorization  | Bearer {token}. Required.  |
| 接受  | text/vtt OR  application/vnd.openxmlformats-officedocument.wordprocessingml.document. 可选。  |

**请求正文**

请勿提供此方法的请求正文。

**响应**

如果成功，此方法将返回 `200 OK` 响应代码，并在响应正文中包含 callTranscript 对象的字节。 `content-type` 标头指定脚本内容的类型。

**示例**
<br>
<details>
<summary><b>示例：获取 callTranscript 内容</b></summary>
<br>
<b>请求</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4/content
```

<br>
<b>响应</b>
<br>

响应包含正文中脚本的字节。 `content-type` 标头指定脚本内容的类型。

> [!NOTE]
> 为了提高可读性，可能缩短了此处显示的响应对象。

```http
HTTP/1.1 200 OK
Content-type: text/vtt

WEBVTT
    
0:0:0.0 --> 0:0:5.320
<v User Name>This is a transcript test.</v>
```

</details>
<br>
<details>
<summary><b>示例：获取指定 $format 查询参数的 callTranscript 内容</b></summary>
<br>
<b>请求</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4/content?$format=text/vtt
 ```

<br>
<b>响应</b>
<br>

响应包含正文中脚本的字节。 `content-type` 标头指定脚本内容的类型。

> [!NOTE]
> 为了提高可读性，可能缩短了此处显示的响应对象。

```http
HTTP/1.1 200 OK
Content-type: text/vtt
    
WEBVTT
    
0:0:0.0 --> 0:0:5.320
<v User Name>This is a transcript test.</v>
```

</details>
<br>
<details>
<summary><b>示例：获取指定 Accept 标头的 callTranscript 内容</b></summary>
<br>
<b>请求</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4/content
Accept: application/vnd.openxmlformats-officedocument.wordprocessingml.document
```

<br>
<b>响应</b>
<br>

响应包含正文中脚本的字节。 `content-Type` 标头指定脚本内容的类型。

> [!NOTE]
> 为了提高可读性，可能缩短了此处显示的响应对象。

```http
HTTP/1.1 200 OK
Content-type: application/vnd.openxmlformats-officedocument.wordprocessingml.document
    
0:0:0.0 --> 0:0:5.320
User Name
This is a transcript test.
```

</details>
<br>
<details>
<summary><b>示例：获取 callTranscript 内容，$format 优先于 accept 标头</b></summary>
<br>
<b>请求</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4/content?$format=text/vtt
Accept: application/vnd.openxmlformats-officedocument.wordprocessingml.document
```

<br>
<b>响应</b>
<br>

响应包含正文中脚本的字节。 `content-Type` 标头指定脚本内容的类型。

> [!NOTE]
> 为了提高可读性，可能缩短了此处显示的响应对象。

```http
HTTP/1.1 200 OK
Content-type: text/vtt
    
WEBVTT
   
0:0:0.0 --> 0:0:5.320
<v User Name>This is a transcript test.</v>
```

</details>

