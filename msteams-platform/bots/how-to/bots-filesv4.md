---
title: 通过机器人收发文件
description: 了解如何使用个人、频道和群组聊天作用域的 Graph API 通过机器人收发文件。
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: 9ac04b912de87ac6e048e7cb7577c0a61b1f9f83
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189651"
---
# <a name="send-and-receive-files-through-the-bot"></a>通过机器人收发文件

> [!IMPORTANT]
> 本文档中的文章以 v4 Bot Framework SDK 为基础。

有两种方法可以将文件发送到机器人并从机器人接收文件:

* [**使用 Microsoft Graph API:**](#use-the-graph-apis) 此方法适用于所有 Microsoft Teams 作用域内的机器人:
  * `personal`
  * `channel`
  * `groupchat`

* [**使用 Teams 机器人 API:**](#use-the-teams-bot-apis) 这些 API 仅支持`personal` 上下文中的文件。

## <a name="use-the-graph-apis"></a>使用 Graph API

使用适用于 [OneDrive 和 SharePoint](/onedrive/developer/rest-api/) 的 Graph API，发布包含引用现有 SharePoint 文件的卡片附件的消息。 要使用 Graph API，请通过标准的 OAuth 2.0 授权流获取对以下其中一项的访问权限:

* 用户的 OneDrive 文件夹，适用于 `personal` 和 `groupchat` 文件。
* 团队频道中的文件，适用于 `channel` 文件。

Graph API 适用于所有 Teams 作用域。 有关详细信息，请参阅 [发送聊天消息文件附件](/graph/api/chatmessage-post?view=graph-rest-beta&tabs=http#example-4-file-attachments&preserve-view=true)。

或者，可以使用 Teams 机器人 API 将文件发送到机器人并从机器人接收文件。

## <a name="use-the-teams-bot-apis"></a>使用 Teams 机器人 API

> [!NOTE]
> Teams 机器人 API 仅适用于 `personal` 上下文。 它们在 `channel` 或 `groupchat` 上下文中不起作用。

使用 Teams API，机器人可以直接在 `personal` 上下文(也称为个人聊天)中与用户一同收发文件。 实现涉及文件内容编辑的功能，例如费用报告、图像识别、文件存档和电子签名。 Teams 中共享的文件通常显示为卡片，且允许丰富的应用内查看。

下一节介绍了如何将文件内容作为直接用户交互发送，例如发送消息。 此 API 作为 Teams 机器人平台的一部分提供。

### <a name="configure-the-bot-to-support-files"></a>将机器人配置为支持文件

要在机器人中收发文件，请将清单中的 `supportsFiles` 属性设置为 `true`。 “清单”参考的 [机器人](~/resources/schema/manifest-schema.md#bots) 节中介绍了此属性。

定义如下所示，`"supportsFiles": true`。 如果机器人未启用 `supportsFiles`，则本节中列出的功能不起作用。

### <a name="receive-files-in-personal-chat"></a>在个人聊天中接收文件

当用户将文件发送到机器人时，文件会首先上传到用户的 OneDrive for business 存储。 然后，机器人会收到一则消息活动，通知用户有关用户上传的信息。 活动包含文件元数据，例如其名称和内容 URL。 用户可以直接从此 URL 进行读取，从而获得其二进制内容。

#### <a name="message-activity-with-file-attachment-example"></a>包含文件附件的消息活动示例

以下代码演示了包含文件附件的消息活动:

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
| `downloadUrl` | 用于提取文件内容的 OneDrive URL。 用户可以直接从此 URL 发出 `HTTP GET`。 |
| `uniqueId` | 唯一的文件 ID。 此为 OneDrive 驱动器项 ID，以防用户将文件发送到机器人。 |
| `fileType` | 文件类型，例如 .pdf 或 .docx。 |

最佳做法是将消息发回给用户以确认文件上传。

### <a name="upload-files-to-personal-chat"></a>将文件上传到个人聊天

要将文件上传到用户:

1. 向请求编写文件权限的用户发送消息。 此消息必须包含 `FileConsentCard` 附件，其中带有要上传的文件的名称。
2. 如果用户接受文件下载，则机器人会收到包含位置 URL 的调用活动。
3. 要传输文件，机器人会直接将 `HTTP POST` 执行到提供的位置 URL。
4. (可选)如果不希望用户接受同一文件的进一步上传，请删除原始同意卡。

#### <a name="message-requesting-permission-to-upload"></a>请求上传权限的消息

以下桌面消息包含请求上传文件用户权限的简单附件对象:

:::image type="content" source="../../assets/images/bots/bot-file-consent-card.png" alt-text="请求上传文件用户权限的同意卡"lightbox="../../assets/images/bots/bot-file-consent-card.png"border="true":::

以下移动消息包含请求上传文件用户权限的附件对象:

<img src="../../assets/images/bots/mobile-bot-file-consent-card.png" alt="Consent card requesting user permission to upload file on mobile" width="350"/>

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
| `description` | 描述文件用途或汇总其内容。 |
| `sizeInBytes` | 向用户提供估计值: 文件大小及其在 OneDrive 中占用的空间量。 |
| `acceptContext` | 用户接受文件时以无提示方式传输到机器人的其他上下文。 |
| `declineContext` | 用户拒绝文件时以无提示方式传输到机器人的其他上下文。 |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>用户接受文件时的调用活动

如果用户接受文件，则会向机器人发送调用活动。 该活动包含 OneDrive for Business 占位符 URL，机器人随后可以发出 `PUT` 以传输文件内容。 有关上传到 OneDrive URL 的信息，请参阅 [将字节上传到上传会话](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)。

以下代码演示了机器人接收的调用活动的简洁版本:

```json
{
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

将文件上传到用户的 OneDrive 后，向用户发送确认消息。 消息必须包含以下用户可选择的 `FileCard` 附件，以便在 OneDrive 中预览或打开，或在本地下载:

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
| `uniqueId` | OneDrive 或 SharePoint 驱动器项 ID。 |
| `fileType` | 文件类型，例如 .pdf 或 .docx。 |

### <a name="fetch-inline-images-from-message"></a>从消息提取内联图像

使用机器人的访问令牌提取属于消息的内联图像。

:::image type="content" source="../../assets/images/bots/inline-image.png" alt-text="内联图像"border="true":::

以下代码演示了从消息提取内联图像:

```csharp
private async Task ProcessInlineImage(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var attachment = turnContext.Activity.Attachments[0];
    var client = _clientFactory.CreateClient();
    // Get Bot's access token to fetch inline image. 
    var token = await new MicrosoftAppCredentials(microsoftAppId, microsoftAppPassword).GetTokenAsync();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    var responseMessage = await client.GetAsync(attachment.ContentUrl);
    // Save the inline image to Files directory.
    var filePath = Path.Combine("Files", "ImageFromUser.png");
    using (var fileStream = new FileStream(filePath, FileMode.Create, FileAccess.Write, FileShare.None))
    {
        await responseMessage.Content.CopyToAsync(fileStream);
    }
    // Create reply with image.
    var reply = MessageFactory.Text($"Attachment of {attachment.ContentType} type and size of {responseMessage.Content.Headers.ContentLength} bytes received.");
    reply.Attachments = new List<Attachment>() { 
        GetInlineAttachment() 
    };
    await turnContext.SendActivityAsync(reply, cancellationToken);
}
private static Attachment GetInlineAttachment()
{
    var imagePath = Path.Combine("Files", "ImageFromUser.png");
    var imageData = Convert.ToBase64String(File.ReadAllBytes(imagePath));
    return new Attachment
    {
        Name = @"ImageFromUser.png",
        ContentType = "image/png",
        ContentUrl = $"data:image/png;base64,{imageData}",
    };
}
```

### <a name="basic-example-in-c"></a>C 中的基本示例 #

以下代码演示了如何在机器人对话框中处理文件上传并发送文件同意请求:

```csharp

protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    if (turnContext.Activity.Attachments?[0].ContentType.Contains("image/*") == true)
    {
        // Inline image.
        await ProcessInlineImage(turnContext, cancellationToken);
    }
    else
    {
        string filename = "teams-logo.png";
        string filePath = Path.Combine("Files", filename);
        long fileSize = new FileInfo(filePath).Length;
        await SendFileCardAsync(turnContext, filename, fileSize, cancellationToken);
    }
}
private async Task ProcessInlineImage(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var attachment = turnContext.Activity.Attachments[0];
    var client = _clientFactory.CreateClient();
    // Get Bot's access token to fetch inline image. 
    var token = await new MicrosoftAppCredentials(microsoftAppId, microsoftAppPassword).GetTokenAsync();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    var responseMessage = await client.GetAsync(attachment.ContentUrl);
    // Save the inline image to Files directory.
    var filePath = Path.Combine("Files", "ImageFromUser.png");
    using (var fileStream = new FileStream(filePath, FileMode.Create, FileAccess.Write, FileShare.None))
    {
        await responseMessage.Content.CopyToAsync(fileStream);
    }
    // Create reply with image.
    var reply = MessageFactory.Text($"Attachment of {attachment.ContentType} type and size of {responseMessage.Content.Headers.ContentLength} bytes received.");
    reply.Attachments = new List<Attachment>() { GetInlineAttachment() };
    await turnContext.SendActivityAsync(reply, cancellationToken);
}
private static Attachment GetInlineAttachment()
{
    var imagePath = Path.Combine("Files", "ImageFromUser.png");
    var imageData = Convert.ToBase64String(File.ReadAllBytes(imagePath));
    return new Attachment
    {
        Name = @"ImageFromUser.png",
        ContentType = "image/png",
        ContentUrl = $"data:image/png;base64,{imageData}",
    };
}
private async Task SendFileCardAsync(ITurnContext turnContext, string filename, long filesize, CancellationToken cancellationToken)
{
    var consentContext = new Dictionary<string, string>
    {
        { 
            "filename", filename 
        },
    };
    var fileCard = new FileConsentCard
    {
        Description = "This is the file I want to send you",
        SizeInBytes = filesize,
        AcceptContext = consentContext,
        DeclineContext = consentContext,
    };
    var asAttachment = new Attachment
    {
        Content = fileCard,
        ContentType = FileConsentCard.ContentType,
        Name = filename,
    };
    var replyActivity = turnContext.Activity.CreateReply();
    replyActivity.Attachments = new List<Attachment>() { asAttachment };
    await turnContext.SendActivityAsync(replyActivity, cancellationToken);
}
```

## <a name="code-sample"></a>代码示例

以下代码示例演示了如何从机器人获取文件同意并将文件上传到 Teams:

|**示例名称** | **说明** | **.NET** | **Javascript** | **Python**|
|----------------|-----------------|--------------|----------------|-----------|
| File upload | 演示了如何从机器人获取文件同意并将文件上传到 Teams。 以及，如何接收发送到机器人的文件。 | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/csharp_dotnetcore/56.teams-file-upload) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/56.teams-file-upload) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/python/56.teams-file-upload) |

## <a name="step-by-step-guide"></a>分步指南

按照 [分步指南](../../sbs-file-handling-in-bot.yml) 使用机器人在 Teams 中上传文件。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [通过团队中的速率限制来优化你的智能机器人](~/bots/how-to/rate-limit.md)

## <a name="see-also"></a>另请参阅

[Microsoft Teams 中的受保护 API](/graph/teams-protected-apis)
