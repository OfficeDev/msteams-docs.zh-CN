---
title: 获取用于提取会议脚本的会议 ID 和组织者 ID
description: 介绍获取用于提取会议脚本的会议 ID 和组织者 ID 的流程
ms.localizationpriority: high
ms.topic: concept
ms.openlocfilehash: 316eabb77eb440a171ca6f357e1db8a2f3b18b6b
ms.sourcegitcommit: d5628e0d50c3f471abd91c3a3c2f99783b087502
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2022
ms.locfileid: "67434983"
---
# <a name="obtain-meeting-id-and-organizer-id"></a>获取会议 ID 和组织者 ID

你的应用可以使用会议组织者的会议 ID 和用户 ID（也称为组织者 ID）提取会议脚本。 Graph REST API 基于会议 ID 和组织者 ID 提取脚本，这些 ID 作为 API 中的参数传递。

> [!NOTE]
> 计划会议的会议 ID 可能会在几天内过期（如果未使用）。 可以通过使用会议 URL 加入会议将其恢复。 有关不同会议类型的会议过期时间线的详细信息，请参阅 [会议过期](/microsoftteams/limits-specifications-teams#meeting-expiration)。

若要获取用于提取脚本的会议 ID 和组织者 ID，请选择以下两种方法之一：

- [订阅变更通知](#subscribe-to-change-notifications)
- [使用 Bot Framework](#use-bot-framework-to-get-meeting-id-and-organizer-id)

### <a name="subscribe-to-change-notifications"></a>订阅变更通知

你可以订阅应用以接收计划会议事件的更改通知。 当应用收到有关订阅的会议事件的通知时，如果已通过所需的 Azure AD 权限获得授权，则可以获取脚本。

应用会收到其订阅的会议事件类型的通知：

- [用户级通知](#obtain-meeting-details-using-user-level-notification)
- [租户级通知](#obtain-meeting-details-using-tenant-level-notification)

当应用收到订阅的会议事件的通知时，它可以从通知消息中检索会议 ID 和组织者 ID。 根据获得的会议详细信息，应用可以在会议结束后提取会议脚本。

#### <a name="obtain-meeting-details-using-user-level-notification"></a>使用用户级通知获取会议详细信息

选择将应用订阅到用户级通知以获取特定用户会议事件的脚本。 当为该用户安排会议时，你的应用会收到通知。 应用也可以使用日历事件接收会议通知。

若要将日历事件订阅到应用，请参阅 [更改 Microsoft Graph 中 Outlook 资源的通知](/graph/outlook-change-notifications-overview)。

使用以下示例订阅用户级通知：

```http
    
POST https://graph.microsoft.com/v1.0/subscriptions/
{
    "changeType": "created,updated,deleted",
    "notificationUrl": "https://webhook.azurewebsites.net/api/send/myNotifyClient",
    "resource": "users('1273a016-201d-4f95-8083-1b7f99b3edeb')/events",
    "expirationDateTime": "2022-05-05T14:58:56.7951795+00:00",
    "clientState": "ClientSecret",
    "includeResourceData": false
}
```

当应用收到有关订阅会议事件的通知时，它会在通知中查找日历事件 ID。 使用事件 ID 获取检索特定聊天 ID 和订阅其消息的 `JoinWebUrl`。 应用订阅聊天消息后，请按照为 [租户级通知](#obtain-meeting-details-using-tenant-level-notification) 提供的步骤获取会议 ID 和组织者 ID。

若要从用户级通知中获取会议 ID 和组织者 ID，请执行以下操作：

1. **获取事件 ID**：应用从通知有效负载获取 `eventId` 属性。

    <details>
    <summary><b>示例</b>：通知有效负载</summary>

    ```json
    {
        "subscriptionId": "ef30cdc6-b5ae-4702-b924-f458fd9e5fc3",
        "changeType": "created",
        "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
        "clientState": "ClientSecret",
        "subscriptionExpirationDateTime": "2022-05-05T07:54:53.1886542-07:00",
        "resource": "Users/1273a016-201d-4f95-8083-1b7f99b3edeb/Events/AAMkADY0NjM1MjRhLTNiNjAtNDBiOC1hYTQxLThkMjAxN2QzMjZhYQBGAAAAAAC03Gz8aL_JQp2Kxvw5a29SBwDFFWHjtoMRTqdrVyQ1h8yLAAAAAAENAADFFWHjtoMRTqdrVyQ1h8yLAAFwC7nAAAA=",
        "resourceData": {}
    }
    ```

    在此示例中， `resource` 中包含的 `eventID` 为 *AAMkADY0NjM1MjRhLTNiNjAtNDBiOC1hYTQxLThkMjAxN2QzMjZhYQBGAAAAAAC03Gz8aL_JQp2Kxvw5a29SBwDFFWHjtoMRTqdrVyQ1h8yLAAAAAAENAADFFWHjtoMRTqdrVyQ1h8yLAAFwC7nAAAA=*。
    </details>

2. **获取会议 URL**：使用事件 ID 检索包含会议 URL 的 `joinUrl`。

    有关详细信息，请参阅 [获取事件](/graph/api/event-get)。

    使用以下示例请求会议 URL：

    ```http
    GET https://graph.microsoft.com/v1.0/users/1273a016-201d-4f95-8083-1b7f99b3edeb/events/AAMkADY0NjM1MjRhLTNiNjAtNDBiOC1hYTQxLThkMjAxN2QzMjZhYQBGAAAAAAC03Gz8aL_JQp2Kxvw5a29SBwDFFWHjtoMRTqdrVyQ1h8yLAAAAAAENAADFFWHjtoMRTqdrVyQ1h8yLAAFwC7nAAAA=
    ```

    响应有效负载包含 `joinURL`。

    <details>
    <summary><b>示例</b>：用于获取会议 URL 的响应有效负载</summary>

    ```json
    {
        "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users('1273a016-201d-4f95-8083-1b7f99b3edeb')/events/$entity",
        "@odata.etag": "W/\"xRVh47aDEU6na1ckNYfMiwABb2Twsg==\"",
        "id": "AAMkADY0NjM1MjRhLTNiNjAtNDBiOC1hYTQxLThkMjAxN2QzMjZhYQBGAAAAAAC03Gz8aL_JQp2Kxvw5a29SBwDFFWHjtoMRTqdrVyQ1h8yLAAAAAAENAADFFWHjtoMRTqdrVyQ1h8yLAAFwC7nAAAA=",    
        "start": {
            "dateTime": "2022-05-06T15:00:00.0000000",
            "timeZone": "UTC"
        },
        "end": {
            "dateTime": "2022-05-06T15:30:00.0000000",
            "timeZone": "UTC"
        },
            
        "onlineMeeting": {
            "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MjExYzJiMTItZDY1MS00ZGZkLWE5YzQtZTBmNWI1MDg2M2Uw%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%221273a016-201d-4f95-8083-1b7f99b3edeb%22%7d",
            "conferenceId": "438824583",
            "tollNumber": "+1 213-279-1007"
        }    
    }
    ```

    </details>

    会议 URL 包含在 `joinUrl` 中。

3. **获取聊天线程 ID**：使用在 `joinUrl` 中获取的会议 URL 获取聊天线程 ID。 在提取相关会议时，将此会议 URL 指定为 `joinWebUrl` 参数的值。

    使用以下示例请求线程 ID：

    ``` http
    GET https://graph.microsoft.com/v1.0/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings?$filter=JoinWebUrl%20eq%20'https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d'
    ```

    响应有效负载包含 `chatInfo` 属性中的 `threadID` 成员。
    <br>
    <details>
    <summary><b>示例</b>：响应具有线程 ID 的有效负载</summary>

    ```json
    {
        "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings",
        "value": [
            {
                "id": "MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19NVE01T1RZM01HVXRObVk0TWkwMFlqZzRMVGsyTURVdFkySXlaR1JsTm1VMVpqQTJAdGhyZWFkLnYy",
                "creationDateTime": "2022-04-26T07:41:17.3736455Z",
                "startDateTime": "2022-04-26T10:30:00Z",
                "endDateTime": "2022-04-26T11:00:00Z",
                "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                "joinWebUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                "chatInfo": {
                    "threadId": "19:meeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2@thread.v2",
                    "messageId": "0",
                    "replyChainMessageId": null
                }
            }
        ]
    }
    ```

    </details>

    聊天 ID 包含在 `threadId` 中。

4. **订阅聊天消息**：使用聊天 ID 订阅应用以接收该特定会议的聊天消息。 有关详细信息，请参阅 [订阅聊天中的消息](/graph/teams-changenotifications-chatmessage#subscribe-to-messages-in-a-chat)。

    如果希望应用订阅包含特定文本的消息，请参阅 [订阅聊天中包含特定文本的消息](/graph/teams-changenotifications-chatmessage#example-2-subscribe-to-messages-in-a-chat-that-contain-certain-text)。

5. 按照 [租户级通知的](#obtain-meeting-details-using-tenant-level-notification) 步骤获取会议 ID 和组织者 ID。

#### <a name="obtain-meeting-details-using-tenant-level-notification"></a>使用租户级通知获取会议详细信息

如果你的应用有权访问租户中的所有会议脚本，则租户级通知非常有用。 订阅应用，以便在听录开始或通话结束时收到有关已安排的在线 Teams 会议的事件通知。 会议结束后，应用可以访问和检索会议脚本。

若要将应用订阅到租户级通知，请参阅 [获取更改通知](/graph/teams-changenotifications-chatmessage#subscribe-to-messages-across-all-chats)。

当应用收到有关订阅的会议事件的通知时，它会在通知中搜索已开始听录和会议结束事件。 这些事件包含聊天 ID（用于获取聊天实体）以及最终的会议 ID 和组织者 ID。

若要从租户级通知中获取会议 ID 和组织者 ID，请执行以下操作：

1. **获取聊天 ID**：应用从通知中获取 `chatId` 属性以进行后续调用。 应用可以从以下负载获取聊天 ID：

    - 听录已启动事件：`callTranscriptEventMessageDetail` 事件类型

        <details>
        <summary><b>示例</b>：听录启动事件的有效负载</summary>

        ```json
        {
        "subscriptionId": "1217470f-564c-4fe3-b51f-ebd962cb8797",
        "changeType": "created",
        "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
        "resource": "chats('19:meeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk@thread.v2')/messages('1649787549174')",
        "contentDecryptedBySimulator": {
            "@odata.context": "https://graph.microsoft.com/$metadata#chats('19%3Ameeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk%40thread.v2')/messages/$entity",
            "messageType": "systemEventMessage",
            "createdDateTime": "2022-04-12T18:19:09.174Z",
            "lastModifiedDateTime": "2022-04-12T18:19:09.174Z",
            "chatId": "19:meeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk@thread.v2",
            "body": {
                "contentType": "html",
                "content": "<systemEventMessage/>"
            },
            "channelIdentity": null,
            "eventDetail": {
                "@odata.type": "#Microsoft.Teams.GraphSvc.callTranscriptEventMessageDetail",
                "callId": "16481de8-3262-419b-abc7-0139e6239515",
                "callTranscriptICalUid": "",
                "meetingOrganizer": {
                    "application": null,
                    "device": null,
                    "user": {
                    "userIdentityType": "aadUser",
                        "id": "14b779ae-cb64-47e7-a512-52fd50a4154d",
                        "displayName": null
                        }
                    }
                }
            },
            "encryptedContent": {}
        }
        ```

        </details>

    - 呼叫结束事件： `callEndedEventMessageDetail` 事件类型

        <details>
        <summary><b>示例</b>：呼叫结束事件的有效负载</summary>

        ```json
        {
            "subscriptionId": "1217470f-564c-4fe3-b51f-ebd962cb8797",
            "changeType": "created",
            "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
            "resource": "chats('19:meeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk@thread.v2')/messages('1649787585457')",
            "resourceData": {},
            "contentDecryptedBySimulator": {
                "@odata.context": "https://graph.microsoft.com/$metadata#chats('19%3Ameeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk%40thread.v2')/messages/$entity",
                "createdDateTime": "2022-04-12T18:19:45.457Z",
                "lastModifiedDateTime": "2022-04-12T18:19:45.457Z",     
                "chatId": "19:meeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk@thread.v2",
                "eventDetail": {
                    "@odata.type": "#Microsoft.Teams.GraphSvc.callEndedEventMessageDetail",
                    "callId": null,
                    "callDuration": "PT1M44S",
                    "callEventType": "meeting",
                    "callParticipants": [
                    ],
                    "initiator": {
        
                    }
                }
            },
            "encryptedContent": {
                    
            }
        }
        ```

        </details>

2. **获取聊天实体**：应用可以使用步骤 1 中获取的聊天 ID 检索聊天实体。 使用聊天实体获取加入呼叫的 URL。 `onlineMeetingInfo` 属性的 `joinWebUrl` 成员包含此 URL，并用于最终获取会议 ID。 组织者 ID 也是响应有效负载的一部分。

    有关聊天实体的详细信息，请参阅 [“获取聊天”](/graph/api/chat-get)。

    使用以下示例基于聊天 ID 请求聊天实体：

    ``` http
    GET https://graph.microsoft.com/v1.0/chats/19:meeting_NmU0NTkxYzMtM2Y2My00NzRlLWFmN2YtNTFiMGM5OWM3ZjY2@thread.v2
    ```

    响应有效负载包含以下元素：

    - **组织者 ID**：它包含在响应有效负载中 `organizer` 属性的 `id` 成员中。
    - **会议呼叫的 URL**：此 URL 用于检索会议 ID，在以下两种方案之一的响应有效负载中可用：
        - 如果会议是联机 Teams 会议，则 `onlineMeetingInfo` 属性的 `joinWebUrl` 成员包含此 URL。
        - 如果会议不是从 Teams 客户端或 Outlook 客户端创建为联机会议，则它包含 `onlineMeetingInfo` 属性中的 `calendarEventId` 成员。 应用可以使用 `calendarEventId` 获取 `joinUrl`，这与 `joinWebUrl` 相同。

      有关事件的详细信息，请参阅 [获取事件](/graph/api/event-get?view=graph-rest-1.0&tabs=http&preserve-view=true)。

      响应有效负载方案的示例，具体取决于加入会议 URL 的类型：

        - 提供 `joinWebUrl` 的联机 Teams 会议

            <details>
            <summary><b>示例</b>：联机会议的响应有效负载</b></summary>

            ```json
            {
                "@odata.context": "https://graph.microsoft.com/beta/$metadata#chats/$entity",
                "id": "19:meeting_NmU0NTkxYzMtM2Y2My00NzRlLWFmN2YtNTFiMGM5OWM3ZjY2@thread.v2",
                "topic": "Test Meet Create Online Meeting",
                "createdDateTime": "2022-04-14T11:30:45.903Z",
                "lastUpdatedDateTime": "2022-04-26T06:27:45.265Z",
                "chatType": "meeting",
                "webUrl": "https://teams.microsoft.com/l/chat/19%3Ameeting_NmU0NTkxYzMtM2Y2My00NzRlLWFmN2YtNTFiMGM5OWM3ZjY2%40thread.v2/0?tenantId=2432b57b-0abd-43db-aa7b-16eadd115d34",
                "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
                "viewpoint": null,
                "onlineMeetingInfo": {
                "calendarEventId": null,
                    "joinWebUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_NmU0NTkxYzMtM2Y2My00NzRlLWFmN2YtNTFiMGM5OWM3ZjY2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                    "organizer": {
                        "id": "14b779ae-cb64-47e7-a512-52fd50a4154d",
                        "displayName": null,
                        "userIdentityType": "aadUser"
                    }
                }
            }
            ```

            </details>

        - 通过 Teams 客户端或 Outlook 客户端安排的会议，未标记为在线会议，其中 `calendarEventId` 可用

            <details>
            <summary><b>示例</b>：会议响应有效负载未标记为联机</summary>

            ```json
            {
                "@odata.context": "https://graph.microsoft.com/beta/$metadata#chats/$entity",
                "id": "19:meeting_YzM1NGFiZWYtOGFiOS00NjM5LTg4OTktYmU0MjI4NTQyNGZm@thread.v2",
                "topic": "Non Online Meeting Teams Client",
                "createdDateTime": "2022-04-26T09:43:23.711Z",
                "lastUpdatedDateTime": "2022-04-26T09:43:46.157Z",
                "chatType": "meeting",
                "webUrl": "https://teams.microsoft.com/l/chat/19%3Ameeting_YzM1NGFiZWYtOGFiOS00NjM5LTg4OTktYmU0MjI4NTQyNGZm%40thread.v2/0?tenantId=2432b57b-0abd-43db-aa7b-16eadd115d34",
                "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
                "viewpoint": null,
                "onlineMeetingInfo": {
                    "calendarEventId": "AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQBGAAAAAAD3AG5jNnlgQJvdCL_KgXJIBwBsww5BlIxtT7iFyYWrXV3AAAAAAAENAABsww5BlIxtT7iFyYWrXV3AAACSDwYeAAA=",
                    "joinWebUrl": null,
                    "organizer": {
                        "id": "14b779ae-cb64-47e7-a512-52fd50a4154d",
                        "displayName": null,
                        "userIdentityType": "aadUser"
                    }
                }
            }
            ```

            </details>

            - 使用以下示例从 `calendarEventId` 获取 `joinWebUrl`：

              ``` http
                GET https://graph.microsoft.com/beta/users/14b779ae-cb64-47e7-a512-52fd50a4154d/events/AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQBGAAAAAAD3AG5jNnlgQJvdCL_KgXJIBwBsww5BlIxtT7iFyYWrXV3AAAAAAAENAABsww5BlIxtT7iFyYWrXV3AAACSDwYdAAA=
              ```

              在此示例中：

                - 组织者 ID 为 *14b779ae-cb64-47e7-a512-52fd50a4154d*。

              此请求的响应有效负载包含 `onlineMeeting` 属性中的 `joinUrl`。

                > [!NOTE]
                > `joinUrl` 与 `joinWebUrl` 相同。

              <br>
              <details>
              <summary><b>示例</b>：包含加入会议 URL 的响应有效负载</summary>

              ```json
              {
                "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('14b779ae-cb64-47e7-a512-52fd50a4154d')/events/$entity",
                "@odata.etag": "W/\"bMMOQZSMbU+4hcmFq11dwAAAkc3Tmw==\"",
                "id": "AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQBGAAAAAAD3AG5jNnlgQJvdCL_KgXJIBwBsww5BlIxtT7iFyYWrXV3AAAAAAAENAABsww5BlIxtT7iFyYWrXV3AAACSDwYdAAA=",    
                "start": {
                    "dateTime": "2022-04-26T10:30:00.0000000",
                    "timeZone": "UTC"
                },
                "end": {
                    "dateTime": "2022-04-26T11:00:00.0000000",
                    "timeZone": "UTC"
                },    
                "onlineMeeting": {
                    "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d"
                },
                "calendar@odata.associationLink": "https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/calendars('AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQAuAAAAAAD3AG5jNnlgQJvdCL_KgXJIAQBsww5BlIxtT7iFyYWrXV3AAAAAAAENAAA=')/$ref",
                "calendar@odata.navigationLink": "https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/calendars('AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQAuAAAAAAD3AG5jNnlgQJvdCL_KgXJIAQBsww5BlIxtT7iFyYWrXV3AAAAAAAENAAA=')"
                }
                ```

              </details>

3. **获取会议 ID**：现在，应用可以使用 `joinWebUrl` 获取会议 ID。

    使用以下示例请求联机会议 ID：

    ``` http
    GET https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings?$filter=JoinWebUrl%20eq%20'https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d'
    ```

    响应有效负载包含 `value` 属性的 `id` 成员中的会议 ID。
    <br>
    <details>
    <summary><b>示例</b>：响应具有会议 ID 的有效负载</summary>

    ```json
    {
        "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings",
        "value": [
            {
                "id": "MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19NVE01T1RZM01HVXRObVk0TWkwMFlqZzRMVGsyTURVdFkySXlaR1JsTm1VMVpqQTJAdGhyZWFkLnYy",
                "creationDateTime": "2022-04-26T07:41:17.3736455Z",
                "startDateTime": "2022-04-26T10:30:00Z",
                "endDateTime": "2022-04-26T11:00:00Z",
                "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                "joinWebUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                "chatInfo": {
                    "threadId": "19:meeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2@thread.v2",
                    "messageId": "0",
                    "replyChainMessageId": null
                }
            }
        ]
    }
    ```

    </details>

4. **提取脚本**：在步骤 2 和步骤 3 中获取的组织者 ID 和会议 ID 允许应用提取该特定会议事件的脚本。

    若要提取脚本，需要：

    1. **根据组织者 ID 和会议 ID 检索脚本 ID**：

       使用以下示例请求脚本 ID：

        ```http
        GET https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings('MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19ObVUwTlRreFl6TXRNMlkyTXkwME56UmxMV0ZtTjJZdE5URmlNR001T1dNM1pqWTJAdGhyZWFkLnYy')/transcripts
        ```

        在此示例中：

        - 会议 ID 包含为 `onlineMeetings` 的值：*MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bW VldGluZ1 9ObVUwTlRreFl6TXRNMlkyTXkwME56UmxMV0ZtTjZdE5URmlNR001T1dNM 1pqWTJAdGhyZWFkLnYy*。
        - 组织者 ID 为 *14b779ae-cb64-47e7-a512-52fd50a4154d*。

        响应有效负载在 `value` 属性的 `id` 成员中包含会议 ID 和组织者 ID 的脚本 ID。
        <br>
        <details>
        <summary><b>示例</b>：用于获取脚本 ID 的响应有效负载</summary>

        ```json
        {
            "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings('MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19ObVUwTlRreFl6TXRNMlkyTXkwME56UmxMV0ZtTjJZdE5URmlNR001T1dNM1pqWTJAdGhyZWFkLnYy')/transcripts",
            "@odata.count": 1,
            "value": [
                {
                    "id": "MSMjMCMjMDEyNjJmNjgtOTc2Zi00MzIxLTlhNDQtYThmMmY4ZjQ1ZjVh",
                    "createdDateTime": "2022-04-14T11:34:39.5662792Z"
                }
            ]
        }
        ```

        在此示例中，脚本 ID 为 *MSMjMCMjMDEyNjmNjgtOTc2Zi00MzIxLTlhNDQtYThmMmY4ZjQ1ZjVh*。

        </details>

    1. **根据脚本 ID 访问和获取会议脚本**：

        使用以下示例以 `.vtt` 格式请求特定会议的脚本：

        ```http
        GET https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings('MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19ObVUwTlRreFl6TXRNMlkyTXkwME56UmxMV0ZtTjJZdE5URmlNR001T1dNM1pqWTJAdGhyZWFkLnYy')/transcripts('MSMjMCMjMDEyNjJmNjgtOTc2Zi00MzIxLTlhNDQtYThmMmY4ZjQ1ZjVh')/content?$format=text/vtt
        ```

        响应有效负载将包含 `.vtt` 格式的脚本。

### <a name="use-bot-framework-to-get-meeting-id-and-organizer-id"></a>使用 Bot Framework 获取会议 ID 和组织者 ID

应用可以使用 Bot Framework 获取会议 ID 和组织者 ID。 机器人可以从所有计划的联机会议自动接收会议开始或结束的事件。

使用以下示例使用机器人应用获取会议 ID 和组织者 ID：

```json
GET /v1/meetings/{meetingId}
```

响应有效负载包含：

- `details` 属性 `msGraphResourceId` 成员中的会议 ID。
- `organizer` 属性 `id` 成员中的组织者 ID。
<br>
<details>
<summary><b>示例</b>：用于获取会议细节 </b> 的响应有效负载</summary>

```json
{
  details: {
    id: "MCMxOTptZWV0aW5nX05XTTFNVEk1TnpNdE5qZ3pNeTAwWVdRNExUaG1PV1F0WlRnM01UQm1PVGczWW1VekB0aHJlYWQudjIjMA==",
    msGraphResourceId: "MSo2NzAyYWZiNi0xMDliLTRjMzItYTE0MS02ZTY1NDY5NTAyYjkqMCoqMTk6bWVldGluZ19OV00xTVRJNU56TXROamd6TXkwMFlXUTRMVGhtT1dRdFpUZzNNVEJtT1RnM1ltVXpAdGhyZWFkLnYy",
    scheduledStartTime: {
    },
    scheduledEndTime: {
    },
    joinUrl: "https://teams.microsoft.com/l/meetup-join/19%3ameeting_NWM1MTI5NzMtNjgzMy00YWQ4LThmOWQtZTg3MTBmOTg3YmUz%40thread.v2/0?context=%7b%22Tid%22%3a%22b3cdf1c8-024a-49e2-a994-f67f830b02f3%22%2c%22Oid%22%3a%226702afb6-109b-4c32-a141-6e65469502b9%22%7d",
    title: "Testing meeting bot 1 - Hun",
    type: "Scheduled",
  },
  conversation: {
    id: "19:meeting_NWM1MTI5NzMtNjgzMy00YWQ4LThmOWQtZTg3MTBmOTg3YmUz@thread.v2",
    isGroup: true,
    conversationType: "groupChat",
  },
  organizer: {
    id: "29:1VZkVr77S3GW_RdAXKrfgFeytpqMegL3tkKvEbwrPqoCVvmqrlKtVrfKWUY7xIM-bZIx4Sq-p1MjdjSZnb5W20w",
    tenantId: "b3cdf1c8-024a-49e2-a994-f67f830b02f3",
    aadObjectId: "6702afb6-109b-4c32-a141-6e65469502b9",
  },
}
```

在此示例中：

- 会议 ID 包含为 `msGraphResourceId` 的值：*MSo2NzAyYWZiNi0xMDliLTRjMzItYTE0MS02ZTY1NDY5NTAyYjkqMCoqMTk6bWVl dGluZ19OV00xTVRJNU56TXROamd6TXkwMFlXUTRMVGhtT1dRdFpUZzNNVEJt1RnM 1ltVXpAdGhyZWFkLnYy*。
- 组织者 ID 包含为 `organizer` 的 `id`值：*29:1VZkVr77S3GW_RdAXKrfgFeytpqMegL3tkKvEbwrPqoCVvmqrlKtVrfKWUY7xIM-bZIx4Sq-p1MjdjSZnb5W20w*。

</details>

应用在获取会议 ID 和组织者 ID 后，会触发 Graph API 以使用这些会议详细信息提取脚本内容。

### <a name="code-samples"></a>代码示例

可以尝试机器人应用的以下代码示例：

| **示例名称** | **说明** | **C#** | **Node.js** |
|----------------|-----------------|--------------|--------------|--------------|
| 会议听录 | 这是一个示例应用程序，演示如何使用图形 API 获取脚本并在任务模块中显示它。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-transcription/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-transcription/nodejs) |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [用于提取脚本的图形 API](/graph/api/resources/calltranscript)
