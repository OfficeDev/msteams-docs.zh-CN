---
title: 从自动程序发送和接收文件
description: 介绍如何从自动程序发送和接收文件
keywords: teams 自动程序文件发送接收
ms.topic: how-to
ms.date: 05/20/2019
ms.openlocfilehash: 80e5a4d7de6e58470e013e98787db8adbefde5d2
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696626"
---
# <a name="send-and-receive-files-through-your-bot"></a>通过自动程序发送和接收文件

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

有两种方法向自动程序发送文件和从自动程序发送文件：

* 使用 Microsoft Graph API。 此方法适用于 Teams 中所有作用域的机器人：
  * `personal`
  * `channel`
  * `groupchat`
* 使用 Teams API。 这些仅支持一个上下文中的文件：
  * `personal`

## <a name="using-the-microsoft-graph-apis"></a>使用 Microsoft Graph API

可以使用适用于 OneDrive 和 [SharePoint](/onedrive/developer/rest-api/)的 Microsoft Graph API 发布引用现有 SharePoint 文件的带卡片附件的邮件。 使用 Graph API 需要通过标准 `personal` `groupchat` `channel` OAuth 2.0 授权流获取对用户的 OneDrive 文件夹 (和文件) 或团队频道 (中的文件) 的访问权限。 此方法适用于所有 Teams 范围。

## <a name="using-the-teams-bot-apis"></a>使用 Teams 自动程序 API

> [!NOTE]
> 此方法仅在上下文中 `personal` 有效。 它在 或 上下文中 `channel` `groupchat` 不起作用。

机器人可以使用 Teams API 与上下文中的用户直接发送和接收文件（也称为个人 `personal` 聊天）。 这允许你实现费用报告、图像识别、文件存档、电子签名以及涉及直接处理文件内容的其他方案。 Teams 中共享的文件通常显示为卡片，并允许丰富的应用内查看。

以下各节介绍如何通过直接用户交互（如发送消息）来发送文件内容。 此 API 作为 Microsoft Teams 自动程序平台的一部分提供。

### <a name="configure-your-bot-to-support-files"></a>配置自动程序以支持文件

为了在自动程序中发送和接收文件，你必须将清单中的 属性设置为 `supportsFiles` `true` 。 此属性在清单引用 [的自动程序](~/resources/schema/manifest-schema.md#bots) 部分中介绍。

定义将如下所示 `"supportsFiles": true` ：。 如果自动程序未启用 `supportsFiles` ，则以下功能将不起作用。

### <a name="receiving-files-in-personal-chat"></a>在个人聊天中接收文件

当用户将文件发送到自动程序时，文件将首先上传到用户的 OneDrive for Business 存储。 然后，自动程序将收到一条消息活动，通知您用户上载。 活动将包含文件元数据，例如其名称和内容 URL。 可以直接从此 URL 读取，以提取其二进制内容。

#### <a name="message-activity-with-file-attachment-example"></a>包含文件附件的邮件活动示例

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

下表介绍了附件的内容属性：

| 属性 | 用途 |
| --- | --- |
| `downloadUrl` | 用于提取文件内容的 OneDrive URL。 可以直接从此 URL `HTTP GET` 发出 。 |
| `uniqueId` | 唯一文件 ID。 如果用户向自动程序发送文件，这将是 OneDrive 驱动器项 ID。 |
| `fileType` | 文件扩展名类型，如 pdf 或 docx。 |

作为最佳实践，您应通过向用户发送回一条消息来确认文件上载。

### <a name="uploading-files-to-personal-chat"></a>将文件上载到个人聊天

将文件上载到用户涉及以下步骤：

1. 向请求写入文件权限的用户发送邮件。 此邮件必须 `FileConsentCard` 包含包含要上载的文件名称的附件。
2. 如果用户接受文件下载，机器人将收到包含位置 URL 的 *Invoke* 活动。
3. 若要传输文件，机器人将直接 `HTTP POST` 执行到提供的位置 URL。
4. 或者，如果不希望允许用户接受同一文件的进一步上载，可以删除原始同意卡。

#### <a name="message-requesting-permission-to-upload"></a>请求上传权限的邮件

此桌面邮件包含一个简单的 attachment 对象，该对象请求用户上载文件的权限：

![请求用户上传文件权限的许可卡屏幕截图](../../assets/images/bots/bot-file-consent-card.png)

此手机信息包含请求用户上传文件的附件对象：

![请求用户许可以在移动设备上上载文件的许可卡屏幕截图](../../assets/images/bots/mobile-bot-file-consent-card.png)

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

下表介绍了附件的内容属性：

| 属性 | 用途 |
| --- | --- |
| `description` | 文件的说明。 可能会向用户显示以描述其用途或汇总其内容。 |
| `sizeInBytes` | 为用户提供估计的文件大小和在 OneDrive 中将占用的空间量。 |
| `acceptContext` | 当用户接受文件时，将静默传输到机器人的其他上下文。 |
| `declineContext` | 当用户拒绝文件时将静默传输到机器人的其他上下文。 |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>当用户接受文件时调用活动

当用户接受文件时，会向机器人发送调用活动。 它包含 OneDrive for Business 占位符 URL，然后自动程序可以向 中发出 以 `PUT` 传输文件内容。 有关上传到 OneDrive URL 的信息，请阅读以下文章： [将字节上传到上传会话](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)。

以下示例显示自动程序将收到的调用活动的精简版本：

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

同样，如果用户拒绝文件，机器人将收到以下事件，其整体活动名称相同：

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

### <a name="notifying-the-user-about-an-uploaded-file"></a>通知用户已上传文件

将文件上传到用户的 OneDrive 后，无论是使用上述机制还是 OneDrive 用户委派 API，都应向用户发送确认消息。 此邮件应包含用户可单击的附件，以预览、在 OneDrive 中打开或 `FileCard` 本地下载。

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

下表介绍了附件的内容属性：

| 属性 | 用途 |
| --- | --- |
| `uniqueId` | OneDrive/SharePoint 驱动器项 ID。 |
| `fileType` | 文件类型，如 pdf 或 docx。 |

### <a name="basic-example-in-c"></a>C 中的基本示例#

以下示例演示如何在自动程序对话框中处理文件上载和发送文件同意请求。

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
