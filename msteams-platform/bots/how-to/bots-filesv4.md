---
title: 通过自动程序发送和接收文件
description: 介绍如何通过自动程序发送和接收文件
keywords: teams 机器人文件发送接收
ms.date: 05/20/2019
ms.topic: how-to
ms.openlocfilehash: 07967ba4ce6d7e15e64c6f925fa588585f5a2c1d
ms.sourcegitcommit: f74b74d5bed1df193e59f46121ada443fb57277b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093272"
---
# <a name="send-and-receive-files-through-the-bot"></a>通过自动程序发送和接收文件

> [!IMPORTANT]
> 本文档中的文章基于 v4 Bot Framework SDK。

有两种方法向自动程序发送和接收文件：

* **使用 Microsoft Graph API：** 此方法适用于所有 Microsoft Teams 作用域中的自动程序：
  * `personal`
  * `channel`
  * `groupchat`

* **使用 Teams 机器人 API：** 这些仅支持上下文中 `personal` 的文件。

## <a name="using-the-graph-apis"></a>使用 Graph API

使用 [适用于 OneDrive](/onedrive/developer/rest-api/)和 SharePoint 的 Graph API 发布包含引用现有 SharePoint 文件的卡片附件的邮件。 若要使用 Graph API，请通过标准 OAuth 2.0 授权流获取对以下任一项的访问权限：
* 用户的 OneDrive 文件夹和 `personal` `groupchat` 文件。
* 团队频道中的 `channel` 文件。

图形 API 在所有 Teams 范围内都工作。

## <a name="using-the-teams-bot-apis"></a>使用 Teams 机器人 API

> [!NOTE]
> Teams 自动程序 API 仅在上下文中 `personal` 工作。 它们在或上下文中 `channel` `groupchat` 不起作用。

使用 Teams API，机器人可以直接在上下文中与用户一起发送和接收文件，也称为 `personal` 个人聊天。 实现涉及文件内容编辑的费用报告、图像识别、文件存档和电子签名等功能。 Teams 中共享的文件通常显示为卡片并允许丰富的应用内查看。

以下各节介绍如何以直接用户交互方式发送文件内容，如发送消息。 此 API 作为 Teams 自动程序平台的一部分提供。

### <a name="configuring-the-bot-to-support-files"></a>配置自动程序以支持文件

若要发送和接收自动程序中的文件，请将清单 `supportsFiles` 中的属性设置为 `true` 。 此属性在清单引用的 [自动](~/resources/schema/manifest-schema.md#bots) 程序部分中介绍。

定义如下所示 `"supportsFiles": true` 。 如果自动程序未启用 `supportsFiles` ，则本节中列出的功能将不起作用。

### <a name="receiving-files-in-personal-chat"></a>在个人聊天中接收文件

当用户将文件发送到自动程序时，文件将首先上载到用户的 OneDrive for Business 存储。 然后，自动程序会收到一个消息活动，通知用户有关用户上载的信息。 活动包含文件元数据，例如其名称和内容 URL。 用户可以直接从此 URL 读取以提取其二进制内容。

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

下表描述了附件的内容属性：

| 属性 | 用途 |
| --- | --- |
| `downloadUrl` | 用于提取文件内容的 OneDrive URL。 用户可以直接从此 `HTTP GET` URL 发出请求。 |
| `uniqueId` | 唯一文件 ID。 这是 OneDrive 驱动器项 ID，以防用户向自动程序发送文件。 |
| `fileType` | 文件类型，如 .pdf 或 .docx。 |

最佳做法是，通过向用户发送回一条消息来确认文件上载。

### <a name="uploading-files-to-personal-chat"></a>将文件上载到个人聊天

将文件上载到用户需要执行以下步骤：

1. 向请求写入文件权限的用户发送邮件。 此邮件必须包含 `FileConsentCard` 一个附件，其中包含要上载的文件的名称。
2. 如果用户接受文件下载，机器人将收到具有位置 URL 的调用活动。
3. 若要传输文件，机器人将直接 `HTTP POST` 执行输入提供的位置 URL。
4. （可选）如果不希望用户接受同一文件的进一步上载，请删除原始同意卡。

#### <a name="message-requesting-permission-to-upload"></a>请求上传权限的邮件

以下桌面邮件包含一个简单的附件对象，该对象请求用户上载文件的权限：

![请求用户上载文件权限的许可卡](../../assets/images/bots/bot-file-consent-card.png)

以下移动邮件包含一个附件对象，该对象请求用户上载文件的权限：

![请求用户权限以在移动设备上上传文件的许可卡](../../assets/images/bots/mobile-bot-file-consent-card.png)

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
| `description` | 描述文件的用途或总结其内容。 |
| `sizeInBytes` | 为用户提供估计的文件大小及其在 OneDrive 中占用的空间量。 |
| `acceptContext` | 用户接受文件时以静默方式传输到自动程序的其他上下文。 |
| `declineContext` | 用户拒绝文件时以静默方式传输到自动程序的其他上下文。 |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>当用户接受文件时调用活动

当用户接受文件时，将调用活动发送到机器人。 它包含 OneDrive for Business 占位符 URL，然后机器人可以发出 a 以 `PUT` 传输文件内容。 有关上传到 OneDrive URL 的信息，请参阅将 [字节上传到上传会话](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)。

以下示例显示了自动程序收到的调用活动的简洁版本：

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

同样，如果用户拒绝文件，机器人会收到以下事件，事件的总体活动名称相同：

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

### <a name="notifying-the-user-about-an-uploaded-file"></a>通知用户已上载文件

将文件上传到用户的 OneDrive 后，向用户发送确认消息。 邮件必须包含用户可以选择的以下附件，以在 OneDrive 中预览或打开它， `FileCard` 或在本地下载：

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
| `uniqueId` | OneDrive 或 SharePoint 驱动器项 ID。 |
| `fileType` | 文件类型，如 .pdf 或 .docx。 |

### <a name="fetching-inline-images-from-message"></a>从邮件提取内嵌图像

使用自动程序的访问令牌提取作为邮件一部分的内嵌图像。

![内联图像](../../assets/images/bots/inline-image.png)

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

以下示例演示如何在自动程序对话框中处理文件上载和发送文件同意请求：

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

### <a name="code-sample"></a>代码示例

|**示例名称** | **说明** | **.NETCore** | **Javascript** | **Python**|
|----------------|-----------------|--------------|----------------|-----------|
| File upload | 演示如何获取文件同意，以及如何从机器人将文件上载到 Teams。 此外，如何接收发送到自动程序的文件。 | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/csharp_dotnetcore/56.teams-file-upload) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/56.teams-file-upload) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/python/56.teams-file-upload) |
