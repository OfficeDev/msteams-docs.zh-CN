---
title: 为 Teams 会议生成会议内通知
author: v-sdhakshina
description: 本文介绍如何为 Microsoft Teams 会议及其代码示例生成会议内通知。
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.openlocfilehash: 2bdf63ab597c00627c14b909d51efa753e0cd1b0
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615403"
---
# <a name="build-in-meeting-notification-for-teams-meeting"></a>为 Teams 会议生成会议内通知

会议内通知用于吸引参与者并在会议期间收集信息或反馈。 使用 [会议内通知有效负载](meeting-apps-apis.md#send-an-in-meeting-notification) 触发会议内通知。 作为通知有效负载请求的一部分，包括要显示的内容托管的 URL。

外部资源 URL 用于显示会议内通知。 可以使用该 `submitTask` 方法在会议聊天中提交数据。

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-dialogbox.png" alt-text="屏幕截图是演示如何使用会议内对话框的示例。":::

还可以将用户的 Teams 显示图片和人员卡添加到会议内通知中，具体取决于`onBehalfOf`具有用户 MRI 的令牌以及传入有效负载的显示名称。 下面是一个示例有效负载：

```json
    {
       "type": "message",
       "text": "John Phillips assigned you a weekly todo",
       "summary": "Don't forget to meet with Marketing next week",
       "channelData": {
           onBehalfOf: [
             { 
               itemId: 0, 
               mentionType: 'person', 
               mri: context.activity.from.id, 
               displayname: context.activity.from.name 
             }
            ],
           "notification": {
           "alertInMeeting": true,
           "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
            }
        },
       "replyToId": "1493070356924"
    }
```

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-people-card.png" alt-text="此屏幕截图显示了 Teams 如何将图片和人员卡片用于会议内对话框。" border="true":::

## <a name="code-sample"></a>代码示例

示例名称 | Description | C# | Node.js |
|----------------|-----------------|--------------|----------------|
| 会议内通知 | 演示如何使用机器人实现会议内通知。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs) |

## <a name="step-by-step-guides"></a>分步指南

按照 [分步指南](../sbs-meeting-content-bubble.yml) 在 Teams 会议中生成会议内通知。

## <a name="see-also"></a>另请参阅

* [会议的生成选项卡](~/apps-in-teams-meetings/build-tabs-for-meeting.md)
* [为 Teams 会议阶段生成应用](build-apps-for-teams-meeting-stage.md)
* [为会议聊天生成可扩展对话](build-extensible-conversation-for-meeting-chat.md)
* [为匿名用户生成应用](build-apps-for-anonymous-user.md)
* [高级会议 API](meeting-apps-apis.md)
