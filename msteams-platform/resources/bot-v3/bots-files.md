---
title: 从机器人收发文件
description: 了解如何使用个人、频道和群聊范围的Graph API 通过机器人发送和接收文件。
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: 96642885f6dd9581a5efdaba21249002282c5c9a
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143366"
---
# <a name="send-and-receive-files-through-your-bot"></a>通过机器人发送和接收文件

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

有两种方法可以将文件发送到机器人并从机器人发送文件:

* 使用 Microsoft Graph API。 此方法适用于 Teams 中所有作用域内的机器人:
  * `personal`
  * `channel`
  * `groupchat`
* 使用 Teams API。 这些仅支持一个上下文中的文件:
  * `personal`

## <a name="using-the-microsoft-graph-apis"></a>使用 Microsoft Graph API

可以使用适用于 [OneDrive 和 SharePoint](/onedrive/developer/rest-api/) 的 Microsoft Graph API，发布包含引用现有 SharePoint 文件的卡片附件的消息。 使用 Graph API 需要通过标准的 OAuth 2.0 授权流获取对用户的 OneDrive 文件夹(适用于 `personal` 和 `groupchat` 文件)或团队频道(适用于 `channel` 文件)中的文件的访问权限。 此方法适用于所有 Teams 作用域。

## <a name="using-the-teams-bot-apis"></a>使用 Teams 机器人 API

> [!NOTE]
> 此方法仅适用于 `personal` 上下文。 它在 `channel` 或 `groupchat` 上下文中不起作用。

使用 Teams API，机器人可以直接在 `personal` 上下文(也称为个人聊天)中与用户一同收发文件。 这使你能够实现费用报告、图像识别、文件存档、电子签名以及其他涉及直接操作文件内容的场景。 Teams 中共享的文件通常显示为卡片，且允许丰富的应用内查看。

下一节介绍了如何执行此操作以通过直接用户交互发送文件内容，例如发送消息。 此 API 作为 Microsoft Teams 机器人平台的一部分提供。

### <a name="configure-your-bot-to-support-files"></a>将机器人配置为支持文件

要在机器人中收发文件，须将清单中的 `supportsFiles` 属性设置为 `true`。 “清单”参考的 [机器人](~/resources/schema/manifest-schema.md#bots) 节中介绍了此属性。

定义将如下所示: `"supportsFiles": true`。 如果机器人未启用 `supportsFiles`，则以下功能将不起作用。

### <a name="receiving-files-in-personal-chat"></a>在个人聊天中接收文件

当用户将文件发送到机器人时，文件会首先上传到用户的 OneDrive for Business 存储。 然后，机器人将收到一则消息活动，通知你用户上传。 活动将包含文件元数据，例如其名称和内容 URL。 可以直接从此 URL 进行读取，从而获得其二进制内容。

#### <a name="message-activity-with-file-attachment-example"></a>包含文件附件的消息活动示例

```json
{
  "attachments": [{
    "contentType": "application/vnd.microsoft.teams.file.download.info",
    "contentUrl": "https://contoso.sharepoint.com/personal/johnadams_contoso_com/Documents/Applications/file_example.txt",
    "name": "file_example.txt",
    "content": {
      "downloadUrl" : "https://download.link",
      "uniqueId": "1150D938-8870-4044-9F2C-5BBDEBA70C9D",
      "fileType": "txt",
      "etag": "123"
    }
  }]
}
```

下表描述了附件的内容属性:

| 属性 | 用途 |
| --- | --- |
| `downloadUrl` | 用于提取文件内容的 OneDrive URL。 可以直接从此 URL 发出 `HTTP GET`。 |
| `uniqueId` | 唯一的文件 ID。 如果用户将文件发送到机器人，则此将为 OneDrive 驱动器项 ID。 |
| `fileType` | 文件扩展类型，例如 pdf 或 docx。 |

最佳做法是，应将消息发回给用户以确认文件上传。

### <a name="uploading-files-to-personal-chat"></a>将文件上传到个人聊天

将文件上传到用户涉及以下步骤:

1. 向请求编写文件权限的用户发送消息。 此消息必须包含 `FileConsentCard` 附件，其中带有要上传的文件的名称。
2. 如果用户接受文件下载，则机器人将收到包含位置 URL 的 *调用* 活动。
3. 要传输文件，机器人会直接将 `HTTP POST` 执行到提供的位置 URL。
4. 或者，如果不想允许用户接受同一文件的进一步上传，则可以删除原始同意卡。

#### <a name="message-requesting-permission-to-upload"></a>请求上传权限的消息

此桌面消息包含请求上传文件用户权限的简单附件对象:

:::image type="content" source="../../assets/images/bots/bot-file-consent-card.png" alt-text="请求上传文件用户权限的同意卡的屏幕截图" border="true":::

此移动消息包含请求上传文件用户权限的附件对象:

![请求在移动设备上上传文件用户权限的同意卡的屏幕截图](../../assets/images/bots/mobile-bot-file-consent-card.png)

```json
{
  "attachments": [{
    "contentType": "application/vnd.microsoft.teams.card.file.consent",
    "name": "file_example.txt",
    "content": {
      "description": "<Purpose of the file, such as: this is your monthly expense report>",
      "sizeInBytes": 1029393,
      "acceptContext": {
      },
      "declineContext": {
      }
    }
  }]
}
```

下表描述了附件的内容属性:

| 属性 | 用途 |
| --- | --- |
| `description` | 文件说明。 可以向用户显示以描述其用途或汇总其内容。 |
| `sizeInBytes` | 向用户提供估计值: 文件大小及其将在 OneDrive 中占用的空间量。 |
| `acceptContext` | 用户接受文件时将以无提示方式传输到机器人的其他上下文。 |
| `declineContext` | 用户拒绝文件时将以无提示方式传输到机器人的其他上下文。 |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>用户接受文件时的调用活动

如果用户接受文件，则会向机器人发送调用活动。 该活动包含 OneDrive for Business 占位符 URL，机器人随后可以向其中发出 `PUT` 以传输文件内容。 有关上传到 OneDrive URL 的信息，请参阅 [将字节上传到上传会话](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session) 一文。

以下示例展示了机器人将收到的调用活动的简要版本:

```json
{
  ...

  "name": "fileConsent/invoke",
  "value": {
    "type": "fileUpload",
    "action": "accept",
    "context": {
    },
    "uploadInfo": {
      "contentUrl": "https://contoso.sharepoint.com/personal/johnadams_contoso_com/Documents/Applications/file_example.txt",
      "name": "file_example.txt",
      "uploadUrl": "https://upload.link",
      "uniqueId": "1150D938-8870-4044-9F2C-5BBDEBA70C8C",
      "fileType": "txt",
      "etag": "123"
    }
  }
}
```

同样，如果用户拒绝文件，则机器人将收到整体活动名称相同的以下事件:

```json
{
  "name": "fileConsent/invoke",
  "value": {
    "type": "fileUpload",
    "action": "decline",
    "context": {
    }
  }
}
```

### <a name="notifying-the-user-about-an-uploaded-file"></a>通知用户有关已上传文件的信息

将文件上传到用户的 OneDrive 后，无论是使用上述机制还是 OneDrive 用户委派的 API，都应向用户发送确认消息。 此消息应包含`FileCard`用户可以选择的附件，可以对其进行预览、在OneDrive中打开或在本地下载。

```json
{
  "attachments": [{
    "contentType": "application/vnd.microsoft.teams.card.file.info",
    "contentUrl": "https://contoso.sharepoint.com/personal/johnadams_contoso_com/Documents/Applications/file_example.txt",
    "name": "file_example.txt",
    "content": {
      "uniqueId": "1150D938-8870-4044-9F2C-5BBDEBA70C8C",
      "fileType": "txt",
    }
  }]
}
```

下表描述了附件的内容属性:

| 属性 | 用途 |
| --- | --- |
| `uniqueId` | OneDrive/SharePoint 驱动器项 ID。 |
| `fileType` | 文件类型，例如 pdf 或 docx。 |

### <a name="basic-example-in-c"></a>采用 C# 的基本示例

以下示例展示了如何在机器人的对话框中处理文件上传并发送文件同意请求:

```csharp

// This sample dialog shows two simple flows:
// 1) A silly example of receiving a file from the user, processing the key elements,
//    and then constructing the attachment and sending it back.
// 2) Creating a new file consent card requesting user permission to upload a file.
private async Task MessageReceivedAsync(IDialogContext context, IAwaitable<object> result)
{
    var replyMessage = context.MakeMessage();
    Attachment returnCard;

    var message = await result as Activity;

    // Check to see if the user is sending the bot a file.
    if (message.Attachments != null && message.Attachments.Any())
    {
        var attachment = message.Attachments.First();

        if (attachment.ContentType == FileDownloadInfo.ContentType)
        {
            FileDownloadInfo downloadInfo = (attachment.Content as JObject).ToObject<FileDownloadInfo>();
            if (downloadInfo != null)
            {
                returnCard = CreateFileInfoAttachment(downloadInfo, attachment.Name, attachment.ContentUrl);
                replyMessage.Attachments.Add(returnCard);
            }
        }
    }
    else
    {
        // Illustrates creating a file consent card.
        returnCard = CreateFileConsentAttachment();
        replyMessage.Attachments.Add(returnCard);
    }
    await context.PostAsync(replyMessage);
}


private static Attachment CreateFileInfoAttachment(FileDownloadInfo downloadInfo, string name, string contentUrl)
{
    FileInfoCard card = new FileInfoCard()
    {
        FileType = downloadInfo.FileType,
        UniqueId = downloadInfo.UniqueId
    };

    Attachment att = card.ToAttachment();
    att.ContentUrl = contentUrl;
    att.Name = name;

    return att;
}

private static Attachment CreateFileConsentAttachment()
{
    JObject acceptContext = new JObject();
    // Fill in any additional context to be sent back when the user accepts the file.

    JObject declineContext = new JObject();
    // Fill in any additional context to be sent back when the user declines the file.

    FileConsentCard card = new FileConsentCard()
    {
        AcceptContext = acceptContext,
        DeclineContext = declineContext,
        SizeInBytes = 102635,
        Description = "File description"
    };

    Attachment att = card.ToAttachment();
    att.Name = "Example file";

    return att;
}
```
