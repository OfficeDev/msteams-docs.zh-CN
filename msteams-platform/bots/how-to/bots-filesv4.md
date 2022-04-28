---
title: 通过机器人发送和接收文件
description: 了解如何使用个人、通道和组聊天范围的Graph API 通过机器人发送和接收文件。 使用基于 v4 Bot Framework SDK 的代码示例Teams机器人 API。
keywords: teams 机器人文件发送接收
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: 22c88a435628c34942eb8f5652b9170f861a0446
ms.sourcegitcommit: e40383d9081bf117030f7e6270140e6b94214e8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65102526"
---
# <a name="send-and-receive-files-through-the-bot"></a>通过机器人发送和接收文件

> [!IMPORTANT]
> 本文档中的文章基于 v4 Bot Framework SDK。

可通过两种方法将文件发送到机器人并从机器人接收文件：

* [**使用 Microsoft Graph API：**](#use-the-graph-apis)此方法适用于所有Microsoft Teams范围内的机器人：
  * `personal`
  * `channel`
  * `groupchat`

* [**使用Teams机器人 API：这些 API**](#use-the-teams-bot-apis) 仅支持上下文中`personal`的文件。

## <a name="use-the-graph-apis"></a>使用Graph API

使用用于OneDrive和SharePoint的Graph API，使用卡片附件发布引用现有[SharePoint](/onedrive/developer/rest-api/)文件的消息。 若要使用Graph API，请通过标准 OAuth 2.0 授权流获取以下任一访问权限：

* 用户的OneDrive文件夹`personal`和`groupchat`文件。
* 团队用于文件的通道 `channel` 中的文件。

Graph API 在所有Teams范围内工作。 有关详细信息，请参阅 [发送聊天消息文件附件](/graph/api/chatmessage-post?view=graph-rest-beta&tabs=http#example-4-file-attachments&preserve-view=true)。

或者，可以使用Teams机器人 API 向机器人发送文件并接收文件。

## <a name="use-the-teams-bot-apis"></a>使用Teams机器人 API

> [!NOTE]
> Teams机器人 API 仅在上下文中`personal`工作。 它们在或`groupchat`上下文中`channel`不起作用。

使用Teams API，机器人可以直接与上下文中的`personal`用户一起发送和接收文件，也称为个人聊天。 实现涉及编辑文件内容的功能，例如费用报告、图像识别、文件存档和电子签名。 Teams中共享的文件通常显示为卡片，并允许在应用内查看丰富的内容。

下一部分介绍如何将文件内容作为直接用户交互发送，例如发送消息。 此 API 作为Teams机器人平台的一部分提供。

### <a name="configure-the-bot-to-support-files"></a>将机器人配置为支持文件

若要在机器人中发送和接收文件，请将 `supportsFiles` 清单中的属性设置为 `true`。 清单引用的 [机器人](~/resources/schema/manifest-schema.md#bots) 部分中描述了此属性。

定义如下所示 `"supportsFiles": true`。 如果机器人未启用 `supportsFiles`，则本部分中列出的功能不起作用。

### <a name="receive-files-in-personal-chat"></a>在个人聊天中接收文件

当用户将文件发送到机器人时，该文件将首先上传到用户的业务存储OneDrive。 然后，机器人将收到一条消息活动，通知用户有关用户上传的信息。 活动包含文件元数据，例如其名称和内容 URL。 用户可以直接从此 URL 读取其二进制内容。

#### <a name="message-activity-with-file-attachment-example"></a>包含文件附件的邮件活动示例

以下代码演示了包含文件附件的消息活动示例：

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

下表描述了附件的内容属性：

| 属性 | 用途 |
| --- | --- |
| `downloadUrl` | OneDrive用于提取文件内容的 URL。 用户可以直接从此 URL 发出 `HTTP GET` 问题。 |
| `uniqueId` | 唯一的文件 ID。 这是OneDrive驱动器项 ID，以防用户将文件发送到机器人。 |
| `fileType` | 文件类型，例如.pdf或.docx。 |

最佳做法是通过将消息发送回用户来确认文件上传。

### <a name="upload-files-to-personal-chat"></a>将文件Upload到个人聊天

将文件上传到用户：

1. 向请求写入文件权限的用户发送消息。 此消息必须包含一个 `FileConsentCard` 附件，其中包含要上传的文件的名称。
2. 如果用户接受文件下载，机器人将收到具有位置 URL 的调用活动。
3. 若要传输文件，机器人将直接执行 `HTTP POST` 到提供的位置 URL。
4. （可选）如果不希望用户接受同一文件的进一步上传，请删除原始同意卡。

#### <a name="message-requesting-permission-to-upload"></a>请求上传权限的消息

以下桌面消息包含请求用户上传文件权限的简单附件对象：

:::image type="content" source="../../assets/images/bots/bot-file-consent-card.png" alt-text="请求用户上传文件权限的许可卡"lightbox="../../assets/images/bots/bot-file-consent-card.png"border="true":::

以下移动消息包含一个附件对象，该对象请求用户上传文件的权限：

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

下表描述了附件的内容属性：

| 属性 | 用途 |
| --- | --- |
| `description` | 描述文件的用途或汇总其内容。 |
| `sizeInBytes` | 为用户提供文件大小的估算值及其占用的空间量OneDrive。 |
| `acceptContext` | 用户接受文件时以无提示方式传输到机器人的其他上下文。 |
| `declineContext` | 用户拒绝文件时以无提示方式传输到机器人的其他上下文。 |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>当用户接受文件时调用活动

如果用户接受该文件，则会将调用活动发送到机器人。 它包含OneDrive for Business占位符 URL，机器人随后可以发出`PUT`用于传输文件内容的 URL。 有关上传到OneDrive URL 的信息，请参阅[上传字节到上传会话](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)。

以下代码演示机器人收到的调用活动的简明版本示例：

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

同样，如果用户拒绝文件，机器人将收到具有相同整体活动名称的以下事件：

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

将文件上传到用户OneDrive后，向用户发送确认消息。 该消息必须包含用户可以选择的以下`FileCard`附件，以预览或在OneDrive中打开它，或在本地下载：

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

下表描述了附件的内容属性：

| 属性 | 用途 |
| --- | --- |
| `uniqueId` | OneDrive或SharePoint驱动器项 ID。 |
| `fileType` | 文件类型，例如.pdf或.docx。 |

### <a name="fetch-inline-images-from-message"></a>从消息中提取内联图像

使用机器人的访问令牌提取消息的内联图像。

:::image type="content" source="../../assets/images/bots/inline-image.png" alt-text="内联图像"border="true":::

以下代码演示从消息中提取内联图像的示例：

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

### <a name="basic-example-in-c"></a>C 中的基本示例#

以下代码演示了如何处理机器人对话框中的文件上传和发送文件同意请求的示例：

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

以下代码示例演示如何从机器人获取文件许可并将文件上传到Teams：

|**示例名称** | **说明** | **.NET** | **Javascript** | **Python**|
|----------------|-----------------|--------------|----------------|-----------|
| File upload | 演示如何从机器人获取文件许可并将文件上传到Teams。 此外，如何接收发送到机器人的文件。 | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/csharp_dotnetcore/56.teams-file-upload) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/56.teams-file-upload) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/python/56.teams-file-upload) |

## <a name="step-by-step-guide"></a>分步指南

按照[分步指南](../../sbs-file-handling-in-bot.yml)使用机器人在Teams中上传文件。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [通过团队中的速率限制来优化你的智能机器人](~/bots/how-to/rate-limit.md)
