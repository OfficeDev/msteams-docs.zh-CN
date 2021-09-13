---
title: 创建并发送任务模块
author: surbhigupta
description: 如何处理初始调用操作，以及使用操作消息扩展命令中的任务模块进行响应
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 891608b2346e09570ba88ee2b868177e1aca619c
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155265"
---
# <a name="create-and-send-the-task-module"></a>创建并发送任务模块

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

可以使用自适应卡片或嵌入式 Web 视图创建任务模块。 若要创建任务模块，必须执行称为初始调用请求的过程。 本文档涵盖初始调用请求、从一对一聊天、群聊、频道 (新帖子) 、频道 (回复线程) 和命令框调用任务模块时的有效负载活动属性。 
> [!NOTE]
> 如果没有使用应用清单中定义的参数填充任务模块，则必须为具有自适应卡片或嵌入式 Web 视图的用户创建任务模块。

## <a name="the-initial-invoke-request"></a>初始调用请求

在初始调用请求过程中，你的服务接收一个类型 为 的对象，并且你必须使用包含自适应卡片或嵌入 Web 视图 `Activity` `composeExtension/fetchTask` 的 URL `task` 的对象进行响应。 与标准自动程序活动属性一起，初始调用有效负载包含以下请求元数据：

|属性名称|用途|
|---|---|
|`type`| 请求的类型。 它必须是 `invoke` 。 |
|`name`| 向服务发出的命令类型。 它必须是 `composeExtension/fetchTask` 。 |
|`from.id`| 发送请求的用户的 ID。 |
|`from.name`| 发送请求的用户的名称。 |
|`from.aadObjectId`| Azure Active Directory发送请求的用户的对象 ID。 |
|`channelData.tenant.id`| Azure Active Directory 租户 ID。 |
|`channelData.channel.id`| 如果在 (通道中提出请求，频道 ID 将) 。 |
|`channelData.team.id`| 如果 (频道中提出请求，团队 ID 将) 。 |
|`value.commandId` | 包含已调用的命令的 ID。 |
|`value.commandContext` | 触发事件的上下文。 它必须是 `compose` 。 |
|`value.context.theme` | 用户的客户端主题，对嵌入式 Web 视图格式非常有用。 它必须是 `default` 、 `contrast` 或 `dark` 。 |

### <a name="example"></a>示例

初始调用请求的代码如下例所示：

```json
{
  "type": "invoke",
  "id": "f:bc319b1d-571a-194d-9ffb-11d7ab37c9ff",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  }
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "fe50f49e5c74440bb2ebf07f49e9553c",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-11-chat"></a>从一对一聊天调用任务模块时的有效负载活动属性 

从一对一聊天调用任务模块时的有效负载活动属性列出如下：

|属性名称|用途|
|---|---|
|`type`| 请求的类型。 它必须是 `invoke` 。 |
|`name`| 向服务发出的命令类型。 它必须是 `composeExtension/fetchTask` 。 |
|`from.id`| 发送请求的用户的 ID。 |
|`from.name`| 发送请求的用户的名称。 |
|`from.aadObjectId`| Azure Active Directory发送请求的用户的对象 ID。 |
|`channelData.tenant.id`| Azure Active Directory 租户 ID。 |
|`channelData.source.name`| 调用任务模块的源名称。 |
|`ChannelData.legacy. replyToId`| 获取或设置邮件的回复 ID。 |
|`value.commandId` | 包含已调用的命令的 ID。 |
|`value.commandContext` | 触发事件的上下文。 它必须是 `compose` 。 |
|`value.context.theme` | 用户的客户端主题，对嵌入式 Web 视图格式非常有用。 它必须是 `default` 、 `contrast` 或 `dark` 。 |

### <a name="example"></a>示例

以下示例提供从一对一聊天调用任务模块时的有效负载活动属性：

```json
{
  "type": "invoke",
  "id": "f:bc319b1d-571a-194d-9ffb-11d7ab37c9ff",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  }
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "fe50f49e5c74440bb2ebf07f49e9553c",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-group-chat"></a>从群聊中调用任务模块时的有效负载活动属性 

从群聊中调用任务模块时的有效负载活动属性列出如下：

|属性名称|用途|
|---|---|
|`type`| 请求的类型。 它必须是 `invoke` 。 |
|`name`| 向服务发出的命令类型。 它必须是 `composeExtension/fetchTask` 。 |
|`from.id`| 发送请求的用户的 ID。 |
|`from.name`| 发送请求的用户的名称。 |
|`from.aadObjectId`| Azure Active Directory发送请求的用户的对象 ID。 |
|`channelData.tenant.id`| Azure Active Directory 租户 ID。 |
|`channelData.source.name`| 调用任务模块的源名称。 |
|`ChannelData.legacy. replyToId`| 获取或设置邮件的回复 ID。 |
|`value.commandId` | 包含已调用的命令的 ID。 |
|`value.commandContext` | 触发事件的上下文。 它必须是 `compose` 。 |
|`value.context.theme` | 用户的客户端主题，对嵌入式 Web 视图格式非常有用。 它必须是 `default` 、 `contrast` 或 `dark` 。 |

### <a name="example"></a>示例

以下示例中提供从群聊调用任务模块时的有效负载活动属性：

```json
{
  "type": "invoke",
  "id": "f:bf72031f-a17e-f99c-48dc-5c0714950d87",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "groupChat",
    "id": "19:d77be72390a1416e9644261e9064fa00@thread.skype",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "213167a1e3b6428b93e186ea5407c759",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-meeting-chat"></a>从会议聊天中调用任务模块时的有效负载活动属性

以下示例中提供从会议聊天调用任务模块时的有效负载活动属性：

```json
{
   "type": "invoke",
   "id": "f:4d271f11-4eed-622f-e820-6d82bf91692f",
   "channelId": "msteams",
   "from": {
      "id": "29:1yLsdbTM1UjxqqD8cjduNUCI1jm8xZaH3lx9u5JQ04t2bknuTCkP45TXdfROTOWk1LzN1AqTgFZUEqHIVGn_qUA",
      "name": "MOD Administrator",
      "aadObjectId": "ef16aa89-5b26-4a2c-aebb-761b551577c0"
   },
   "conversation": {
      "tenantId": "c9f9aafd-64ac-4f38-8e05-12feba3fb090",
      "id": "19:meeting_NTk4ZDY4ZmYtOWEzZS00OTRkLThhY2EtZmUzZmUzMDQyM2M0@thread.v2",
      "name": "Test meeting"
   },   
   "channelData": {
      "tenant": {
         "id": "c9f9aafd-64ac-4f38-8e05-12feba3fb090"
      },
      "source": {
         "name": "compose"
      },
      "meeting": {
         "id": "MCMxOTptZWV0aW5nX05UazRaRFk0Wm1ZdE9XRXpaUzAwT1RSa0xUaGhZMkV0Wm1VelptVXpNRFF5TTJNMEB0aHJlYWQudjIjMA=="
      }
   },
   "value": {
      "commandId": "Test",
      "commandContext": "compose",
      "requestId": "c46a6b53573f42b5bc801716e5ccc960",
      "context": {
         "theme": "default"
      }
   },
   "name": "composeExtension/fetchTask",
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-new-post"></a>从频道调用任务模块时的有效负载活动属性 (发布)  

从频道调用任务模块时的有效负载活动属性 (发布) 如下所示：

|属性名称|用途|
|---|---|
|`type`| 请求的类型。 它必须是 `invoke` 。 |
|`name`| 向服务发出的命令类型。 它必须是 `composeExtension/fetchTask` 。 |
|`from.id`| 发送请求的用户的 ID。 |
|`from.name`| 发送请求的用户的名称。 |
|`from.aadObjectId`| Azure Active Directory发送请求的用户的对象 ID。 |
|`channelData.tenant.id`| Azure Active Directory 租户 ID。 |
|`channelData.channel.id`| 如果在 (通道中提出请求，频道 ID 将) 。 |
|`channelData.team.id`| 如果 (频道中提出请求，团队 ID 将) 。 |
|`channelData.source.name`| 调用任务模块的源名称。 |
|`ChannelData.legacy. replyToId`| 获取或设置邮件的回复 ID。 |
|`value.commandId` | 包含已调用的命令的 ID。 |
|`value.commandContext` | 触发事件的上下文。 它必须是 `compose` 。 |
|`value.context.theme` | 用户的客户端主题，对嵌入式 Web 视图格式非常有用。 它必须是 `default` 、 `contrast` 或 `dark` 。 |

### <a name="example"></a>示例

从频道调用任务模块时的有效负载活动属性 (以下示例) 新文章：

```json
{
  "type": "invoke",
  "id": "f:a5fbb109-c989-c449-ee83-71ac99919d4b",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "5336640edc7748b28ce2df43f5b45963",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-reply-to-thread"></a>从频道调用任务模块时的有效负载活动属性 (线程)  

从频道调用任务模块时的有效负载活动属性 (主题) 如下所示：

|属性名称|用途|
|---|---|
|`type`| 请求的类型。 它必须是 `invoke` 。 |
|`name`| 向服务发出的命令类型。 它必须是 `composeExtension/fetchTask` 。 |
|`from.id`| 发送请求的用户的 ID。 |
|`from.name`| 发送请求的用户的名称。 |
|`from.aadObjectId`| Azure Active Directory发送请求的用户的对象 ID。 |
|`channelData.tenant.id`| Azure Active Directory 租户 ID。 |
|`channelData.channel.id`| 如果在 (通道中提出请求，频道 ID 将) 。 |
|`channelData.team.id`| 如果 (频道中提出请求，团队 ID 将) 。 |
|`channelData.source.name`| 调用任务模块的源名称。 |
|`ChannelData.legacy. replyToId`| 获取或设置邮件的回复 ID。 |
|`value.commandId` | 包含已调用的命令的 ID。 |
|`value.commandContext` | 触发事件的上下文。 它必须是 `compose` 。 |
|`value.context.theme` | 用户的客户端主题，对嵌入式 Web 视图格式非常有用。 它必须是 `default` 、 `contrast` 或 `dark` 。 |

### <a name="example"></a>示例

从频道调用任务模块时的有效负载活动属性 (对线程) 如以下示例所示：

```json
{
  "type": "invoke",
  "id": "f:19ccc884-c792-35ef-2f40-d0ff43dcca71",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype;messageid=1611060744833",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "TEst",
    "commandContext": "message",
    "requestId": "7f7d22efe5414818becebcec649a7912",
    "messagePayload": {
      "linkToMessage": "https://teams.microsoft.com/l/message/19:6decf54d86d945e4b3924b63a9161a78@thread.skype/1611060744833",
      "id": "1611060744833",
      "replyToId": null,
      "createdDateTime": "2021-01-19T12:52:24.833Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "<div><div><at id=\"0\">Testing outgoing Webhook-Nikitha</at> - Hi</div>\n</div>"
      },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc",
          "displayName": "Olo Brockhouse"
        },
        "application": null
      },
      "reactions": [],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Testing outgoing Webhook-Nikitha",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": null,
            "application": {
              "applicationIdentityType": "webhook",
              "id": "b8c1c68c-e290-4bdd-81c3-266f310751dc",
              "displayName": "Testing outgoing Webhook-Nikitha"
            }
          }
        }
      ],
      "attachments": []
    },
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-command-box"></a>从命令框调用任务模块时的有效负载活动属性 

从命令框调用任务模块时的有效负载活动属性列出如下：

|属性名称|用途|
|---|---|
|`type`| 请求的类型。 它必须是 `invoke` 。 |
|`name`| 向服务发出的命令类型。 它必须是 `composeExtension/fetchTask` 。 |
|`from.id`| 发送请求的用户的 ID。 |
|`from.name`| 发送请求的用户的名称。 |
|`from.aadObjectId`| Azure Active Directory发送请求的用户的对象 ID。 |
|`channelData.tenant.id`| Azure Active Directory 租户 ID。 |
|`channelData.source.name`| 调用任务模块的源名称。 |
|`value.commandId` | 包含已调用的命令的 ID。 |
|`value.commandContext` | 触发事件的上下文。 它必须是 `compose` 。 |
|`value.context.theme` | 用户的客户端主题，对嵌入式 Web 视图格式非常有用。 它必须是 `default` 、 `contrast` 或 `dark` 。 |

### <a name="example"></a>示例

下面的示例提供从命令框调用任务模块时的有效负载活动属性：

```json
{
  "type": "invoke",
  "id": "f:172560f1-95f9-3189-edb2-b7612cd1a3cd",
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "TEst",
    "commandContext": "compose",
    "requestId": "d2ce690cdc2b4920a538e75882610a30",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

### <a name="example"></a>示例 

以下代码部分是请求 `fetchTask` 的一个示例：

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "name": "composeExtension/fetchTask",
  "type": "invoke",
  "timestamp": "2019-07-01T22:57:22.175Z",
  "localTimestamp": "2019-07-01T15:57:22.175-07:00",
  "id": "f:0123456878990178955",
  "channelId": "msteams",
  "serviceURL": "https://smba.trafficmanager.net/amer/",
  "from": {
    "id": "29:1test2GgHIa0DXzDT_OGwL5vSMZdAxDlGR7hYxZ6_JBVqHz2Zq9Nm44FUNWqHCdGBwHg8WrlFRsYrd0cCAS7dig",
    "name": "John Smith",
    "aadObjectId": "1234567d-1234-462a-8952-35b75f16f1e1"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "tenantId": "1234abcd-1234-12ab-12ab-35b75f16f1e1",
    "id": "19:83ed1d507cb5427c93495cf914326310@thread.skype"
  },
  "recipient": {
    "id": "28:049566e0-4401-4bcf-86a1-ce22082ce03a",
    "name": "mess"
  },
  "entities": [
    {
      "locale": "en-US",
      "country": "US",
      "platform": "Windows",
      "type": "clientInfo"
    }
  ],
  "channelData": {
    "channel": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "team": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "tenant": {
      "id": "1234abcd-1234-12ab-12ab-35b75f16f1e1"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "hello",
    "commandContext": "compose",
    "context": {
      "theme": "dark"
    }
  },
  "locale": "en-US"
}
```

* * *

## <a name="initial-invoke-request-from-a-message"></a>来自邮件的初始调用请求

从邮件调用自动程序时，初始调用请求中的对象必须包含从其中调用消息扩展 `value` 的消息的详细信息。 和 数组是可选的，如果原始邮件中没有任何反应或提及，则它们 `reactions` `mentions` 不存在。 以下部分是 对象 `value` 的示例：

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
...
  "value": {
    "commandId": "setReminder",
    "commandContext": "message",
    "messagePayload": {
      "id": "1111111111",
      "replyToId": null,
      "createdDateTime": "2019-02-25T21:29:36.065Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "subject": "Message subject",
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "This is the message the messaging extension was invoked from."
    },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "wxyz12ab8-ab12-cd34-ef56-098abc123876",
          "displayName": "Jamie Smythe"
        },
        "application": null
      },
      "reactions": [
        {
          "reactionType": "like",
          "createdDateTime": "2019-02-25T22:40:40.806Z",
          "user": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "qrst12346-ab12-cd34-ef56-098abc123876",
              "displayName": "Jim Brown"
            },
            "application": null
          }
        }
      ],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Sarah",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "ab12345678-ab12-cd34-ef56-098abc123876",
              "displayName": "Sarah"
            },
            "application": null
          }
        }
      ]
    }
  ...
```

* * *

## <a name="respond-to-the-fetchtask"></a>响应 fetchTask

使用包含具有自适应卡片或 Web URL 的对象或简单的字符串消息的对象响应 `task` `taskInfo` 调用请求。

|属性名称|用途|
|---|---|
|`type`| 可以是显示 `continue` 窗体，也可以 `message` 用于简单的弹出式窗体。 |
|`value`| 窗体 `taskInfo` 的对象或邮件 `string` 的 。 |

taskInfo 对象的架构为：

|属性名称|用途|
|---|---|
|`title`| 任务模块的标题。|
|`height`| 它必须是整数值 (以像素为单位) 或 `small` 、 `medium` 、 `large` 。|
|`width`| 它必须是整数值 (以像素为单位) 或 `small` 、 `medium` 、 `large` 。|
|`card`| 定义表单的自适应卡片 (使用一个) 。
|`url`| 在任务模块内作为嵌入 Web 视图打开的 URL。|
|`fallbackUrl`| 如果客户端不支持任务模块功能，此 URL 在浏览器选项卡中打开。 |

### <a name="respond-to-the-fetchtask-with-an-adaptive-card"></a>使用自适应卡片响应 fetchTask

使用自适应卡片时，必须使用对象响应包含自适应卡片 `task` `value` 的对象。

#### <a name="example"></a>示例

以下代码部分是使用自适应 `fetchTask` 卡片响应的示例：

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

此示例除了使用 Bot Framework SDK NuGet还使用[AdaptiveCards](https://www.nuget.org/packages/AdaptiveCards) NuGet包。

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Card = new Attachment()
        {
          ContentType = AdaptiveCard.ContentType,
          Content = new AdaptiveCard("1.0")
          {
            Body = new List<AdaptiveElement>()
            {
              new AdaptiveTextInput() { Id = "FormField1", Placeholder = placeholder},
              new AdaptiveTextInput() { Id = "FormField2", Placeholder = "FormField2"},
              new AdaptiveTextInput() { Id = "FormField3", Placeholder = "FormField3"},
            },
            Actions = new List<AdaptiveAction>()
            {
              new AdaptiveSubmitAction()
              {
                Type = AdaptiveSubmitAction.TypeName,
                Title = "Submit",
              },
            },
          },
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    handleTeamsMessagingExtensionFetchTask(context, action) {
      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [{
          data: { submitLocation: 'messagingExtensionFetchTask'},
          title: 'Submit',
          type: 'Action.Submit'
        }],
        body: [
          { text: 'Task Module', type: 'TextBlock', weight: 'bolder'},
          { type: 'TextBlock', text: 'Enter text for Question:' },
          { id: 'Question', placeholder: 'Question text here', type: 'Input.Text', value: userText },
          { type: 'TextBlock', text: 'Options for Question:' },
          { type: 'TextBlock', text: 'Is Multi-Select:' },
          {
            choices: [{ title: 'True', value: 'true' }, { title: 'False', value: 'false' }],
            id: 'MultiSelect',
            isMultiSelect: false,
            style: 'expanded',
            type: 'Input.ChoiceSet',
            value: isMultiSelect ? 'true' : 'false'
          },
          { id: 'Option1', placeholder: 'Option 1 here', type: 'Input.Text', value: option1 },
          { id: 'Option2', placeholder: 'Option 2 here', type: 'Input.Text', value: option2 }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });

      return {
        task: {
          type: 'continue',
          value: {
            card: adaptiveCard,
            height: 450,
            title: 'Task Module Fetch Example',
            url: null,
            width: 500
          }
        }
      };
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
 {
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "card": {
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Input.Text",
            "placeholder": "FormField1",
            "id": "FormField1"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField2",
            "id": "FormField2"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField3",
            "id": "FormField3"
          },
          {
            "type": "ActionSet",
            "actions": [
              {
                "type": "Action.Submit",
                "title": "Action.Submit",
                "id": "submitAction"
              }
            ]
          }
        ]
      }
    }
  }
}
```

* * *

### <a name="create-a-task-module-with-an-embedded-web-view"></a>使用嵌入式 Web 视图创建任务模块

使用嵌入式 Web 视图时，必须使用对象响应包含要加载的 Web 表单 `task` `value` 的 URL 的对象。 要加载的任何 URL 的域必须包含在应用清单的数组 `validDomains` 中。 有关生成嵌入式 Web 视图的信息，请参阅 [任务模块文档](~/task-modules-and-cards/what-are-task-modules.md)。 

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Url = "https://contoso.com/msteams/taskmodules/newcustomer",
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    return {
      task: {
        type: 'continue',
        value: {
          width: 500,
          height: 450,
          title: 'Task Module Fetch Example',
          url: 'https://contoso.com/msteams/taskmodules/newcustomer',
          fallbackUrl: 'https://contoso.com/msteams/taskmodules/newcustomer'
        }
      }
    };
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "url": "https://contoso.com/msteams/taskmodules/newcustomer",
      "fallbackUrl": "https://contoso.com/msteams/taskmodules/newcustomer"
    }
  }
}
```

* * *

### <a name="request-to-install-your-conversational-bot"></a>请求安装对话机器人

如果应用包含对话机器人，则安装对话中的机器人，然后加载任务模块。 自动程序可用于获取任务模块的其他上下文。 此方案的一个示例是提取名单以填充人员选取器控件或团队中的频道列表。

当消息扩展收到调用时，请检查自动程序是否安装在当前上下文中以便于 `composeExtension/fetchTask` 流。 例如，使用获取名单呼叫检查流程。 如果未安装自动程序，则返回自适应卡片以及请求用户安装自动程序的操作。 用户必须有权将应用安装到该位置进行检查。 如果应用安装不成功，用户将收到一条消息，联系管理员。

#### <a name="example"></a>示例 

以下代码部分是响应的一个示例：

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Looks like you haven't used Disco in this team/chat"
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Continue",
      "data": {
        "msteams": {
          "justInTimeInstall": true
        }
      }
    }
  ],
  "version": "1.0"
}
```

安装对话机器人后，它会收到另一条使用 和 的调用 `name = composeExtension/submitAction` 消息 `value.data.msteams.justInTimeInstall = true` 。

#### <a name="example"></a>示例 

以下代码部分是调用的任务响应示例：

```json
{
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "msteams": {
        "justInTimeInstall": true
      }
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  },
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith"
}
```

对调用的任务响应必须类似于已安装的机器人。

#### <a name="example"></a>示例 

以下代码部分是一个使用自适应卡片实时安装应用的示例： 

```csharp
private static Attachment GetAdaptiveCardAttachmentFromFile(string fileName)
  {
      //Read the card json and create attachment.
         string[] paths = { ".", "Resources", fileName };
         var adaptiveCardJson = File.ReadAllText(Path.Combine(paths));
         var adaptiveCardAttachment = new Attachment()
            {
                ContentType = "application/vnd.microsoft.card.adaptive",
                Content = JsonConvert.DeserializeObject(adaptiveCardJson),
            };
            return adaptiveCardAttachment;
        }
```

* * *

## <a name="code-sample"></a>代码示例

| 示例名称           | 说明 | .NET    | Node.js   |   
|:---------------------|:--------------|:---------|:--------|
|Teams邮件扩展操作| 介绍如何定义操作命令、创建任务模块和响应任务模块提交操作。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|Teams邮件扩展搜索   |  介绍如何定义搜索命令并响应搜索。        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="see-also"></a>另请参阅

[定义操作命令](~/messaging-extensions/how-to/action-commands/define-action-command.md)


## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"] 
> [响应操作命令](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

