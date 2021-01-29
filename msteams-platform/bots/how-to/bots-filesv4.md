---
title: 通过自动程序发送和接收文件
description: 介绍如何通过自动程序发送和接收文件
keywords: teams 机器人文件发送接收
ms.date: 05/20/2019
ms.topic: how-to
ms.openlocfilehash: 1699b9339bd6a49194240130d16795e8febcb76e
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037052"
---
# <a name="send-and-receive-files-through-the-bot"></a><span data-ttu-id="13dd8-104">通过自动程序发送和接收文件</span><span class="sxs-lookup"><span data-stu-id="13dd8-104">Send and receive files through the bot</span></span>

> [!IMPORTANT]
> <span data-ttu-id="13dd8-105">本文档中的文章基于 v4 Bot Framework SDK。</span><span class="sxs-lookup"><span data-stu-id="13dd8-105">The articles in this document are based on the v4 Bot Framework SDK.</span></span>

<span data-ttu-id="13dd8-106">有两种方法向自动程序发送和接收文件：</span><span class="sxs-lookup"><span data-stu-id="13dd8-106">There are two ways to send files to and receive files from a bot:</span></span>

* <span data-ttu-id="13dd8-107">**使用 Microsoft Graph API：** 此方法适用于所有 Microsoft Teams 作用域中的自动程序：</span><span class="sxs-lookup"><span data-stu-id="13dd8-107">**Using the Microsoft Graph APIs:** This method works for bots in all Microsoft Teams scopes:</span></span>
  * `personal`
  * `channel`
  * `groupchat`

* <span data-ttu-id="13dd8-108">**使用 Teams 机器人 API：** 这些仅支持上下文中 `personal` 的文件。</span><span class="sxs-lookup"><span data-stu-id="13dd8-108">**Using the Teams bot APIs:** These only support files in `personal` context.</span></span>

## <a name="using-the-graph-apis"></a><span data-ttu-id="13dd8-109">使用 Graph API</span><span class="sxs-lookup"><span data-stu-id="13dd8-109">Using the Graph APIs</span></span>

<span data-ttu-id="13dd8-110">使用 [适用于 OneDrive](/onedrive/developer/rest-api/)和 SharePoint 的 Graph API 发布包含引用现有 SharePoint 文件的卡片附件的邮件。</span><span class="sxs-lookup"><span data-stu-id="13dd8-110">Post messages with card attachments that refer to existing SharePoint files, using the Graph APIs for [OneDrive and SharePoint](/onedrive/developer/rest-api/).</span></span> <span data-ttu-id="13dd8-111">若要使用 Graph API，请通过标准 OAuth 2.0 授权流获取对以下任一项的访问权限：</span><span class="sxs-lookup"><span data-stu-id="13dd8-111">To use the Graph APIs, obtain access to either of the following through the standard OAuth 2.0 authorization flow:</span></span>
* <span data-ttu-id="13dd8-112">用户的 OneDrive 文件夹和 `personal` `groupchat` 文件。</span><span class="sxs-lookup"><span data-stu-id="13dd8-112">A user's OneDrive folder for `personal` and `groupchat` files.</span></span>
* <span data-ttu-id="13dd8-113">团队频道中的 `channel` 文件。</span><span class="sxs-lookup"><span data-stu-id="13dd8-113">The files in a team's channel for `channel` files.</span></span>

<span data-ttu-id="13dd8-114">图形 API 在所有 Teams 范围内都工作。</span><span class="sxs-lookup"><span data-stu-id="13dd8-114">Graph APIs work in all Teams scopes.</span></span>

## <a name="using-the-teams-bot-apis"></a><span data-ttu-id="13dd8-115">使用 Teams 机器人 API</span><span class="sxs-lookup"><span data-stu-id="13dd8-115">Using the Teams bot APIs</span></span>

> [!NOTE]
> <span data-ttu-id="13dd8-116">Teams 自动程序 API 仅在上下文中 `personal` 工作。</span><span class="sxs-lookup"><span data-stu-id="13dd8-116">Teams bot APIs work only in the `personal` context.</span></span> <span data-ttu-id="13dd8-117">它们在或上下文中 `channel` `groupchat` 不起作用。</span><span class="sxs-lookup"><span data-stu-id="13dd8-117">They do not work in the `channel` or `groupchat` context.</span></span>

<span data-ttu-id="13dd8-118">使用 Teams API，机器人可以直接在上下文中与用户一起发送和接收文件，也称为 `personal` 个人聊天。</span><span class="sxs-lookup"><span data-stu-id="13dd8-118">Using Teams APIs, the bot can directly send and receive files with users in the `personal` context, also known as personal chats.</span></span> <span data-ttu-id="13dd8-119">实现涉及文件内容编辑的费用报告、图像识别、文件存档和电子签名等功能。</span><span class="sxs-lookup"><span data-stu-id="13dd8-119">Implement features, such as expense reporting, image recognition, file archival, and e-signatures involving the editing of file content.</span></span> <span data-ttu-id="13dd8-120">Teams 中共享的文件通常显示为卡片并允许丰富的应用内查看。</span><span class="sxs-lookup"><span data-stu-id="13dd8-120">Files shared in Teams typically appear as cards and allow rich in-app viewing.</span></span>

<span data-ttu-id="13dd8-121">以下各节介绍如何以直接用户交互方式发送文件内容，如发送消息。</span><span class="sxs-lookup"><span data-stu-id="13dd8-121">The following sections describe how to send file content as a direct user interaction, like sending a message.</span></span> <span data-ttu-id="13dd8-122">此 API 作为 Teams 自动程序平台的一部分提供。</span><span class="sxs-lookup"><span data-stu-id="13dd8-122">This API is provided as part of the Teams bot platform.</span></span>

### <a name="configuring-the-bot-to-support-files"></a><span data-ttu-id="13dd8-123">配置自动程序以支持文件</span><span class="sxs-lookup"><span data-stu-id="13dd8-123">Configuring the bot to support files</span></span>

<span data-ttu-id="13dd8-124">若要发送和接收自动程序中的文件，请将清单 `supportsFiles` 中的属性设置为 `true` 。</span><span class="sxs-lookup"><span data-stu-id="13dd8-124">To send and receive files in the bot, set the `supportsFiles` property in the manifest to `true`.</span></span> <span data-ttu-id="13dd8-125">此属性在清单引用的 [自动](~/resources/schema/manifest-schema.md#bots) 程序部分中介绍。</span><span class="sxs-lookup"><span data-stu-id="13dd8-125">This property is described in the [bots](~/resources/schema/manifest-schema.md#bots) section of the Manifest reference.</span></span>

<span data-ttu-id="13dd8-126">定义如下所示 `"supportsFiles": true` 。</span><span class="sxs-lookup"><span data-stu-id="13dd8-126">The definition looks like this, `"supportsFiles": true`.</span></span> <span data-ttu-id="13dd8-127">如果自动程序未启用 `supportsFiles` ，则本节中列出的功能将不起作用。</span><span class="sxs-lookup"><span data-stu-id="13dd8-127">If the bot does not enable `supportsFiles`, the features listed in this section do not work.</span></span>

### <a name="receiving-files-in-personal-chat"></a><span data-ttu-id="13dd8-128">在个人聊天中接收文件</span><span class="sxs-lookup"><span data-stu-id="13dd8-128">Receiving files in personal chat</span></span>

<span data-ttu-id="13dd8-129">当用户将文件发送到自动程序时，文件将首先上载到用户的 OneDrive for Business 存储。</span><span class="sxs-lookup"><span data-stu-id="13dd8-129">When a user sends a file to the bot, the file is first uploaded to the user's OneDrive for Business storage.</span></span> <span data-ttu-id="13dd8-130">然后，自动程序会收到一个消息活动，通知用户有关用户上载的信息。</span><span class="sxs-lookup"><span data-stu-id="13dd8-130">The bot then receives a message activity notifying the user about the user upload.</span></span> <span data-ttu-id="13dd8-131">活动包含文件元数据，例如其名称和内容 URL。</span><span class="sxs-lookup"><span data-stu-id="13dd8-131">The activity contains file metadata, such as its name and the content URL.</span></span> <span data-ttu-id="13dd8-132">用户可以直接从此 URL 读取以提取其二进制内容。</span><span class="sxs-lookup"><span data-stu-id="13dd8-132">The user can directly read from this URL to fetch its binary content.</span></span>

#### <a name="message-activity-with-file-attachment-example"></a><span data-ttu-id="13dd8-133">包含文件附件的邮件活动示例</span><span class="sxs-lookup"><span data-stu-id="13dd8-133">Message activity with file attachment example</span></span>

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

<span data-ttu-id="13dd8-134">下表描述了附件的内容属性：</span><span class="sxs-lookup"><span data-stu-id="13dd8-134">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="13dd8-135">属性</span><span class="sxs-lookup"><span data-stu-id="13dd8-135">Property</span></span> | <span data-ttu-id="13dd8-136">用途</span><span class="sxs-lookup"><span data-stu-id="13dd8-136">Purpose</span></span> |
| --- | --- |
| `downloadUrl` | <span data-ttu-id="13dd8-137">用于提取文件内容的 OneDrive URL。</span><span class="sxs-lookup"><span data-stu-id="13dd8-137">OneDrive URL for fetching the content of the file.</span></span> <span data-ttu-id="13dd8-138">用户可以直接从此 `HTTP GET` URL 发出请求。</span><span class="sxs-lookup"><span data-stu-id="13dd8-138">The user can issue an `HTTP GET` directly from this URL.</span></span> |
| `uniqueId` | <span data-ttu-id="13dd8-139">唯一文件 ID。</span><span class="sxs-lookup"><span data-stu-id="13dd8-139">Unique file ID.</span></span> <span data-ttu-id="13dd8-140">这是 OneDrive 驱动器项 ID，以防用户向自动程序发送文件。</span><span class="sxs-lookup"><span data-stu-id="13dd8-140">This is the OneDrive drive item ID, in case the user sends a file to the bot.</span></span> |
| `fileType` | <span data-ttu-id="13dd8-141">文件类型，如 .pdf 或 .docx。</span><span class="sxs-lookup"><span data-stu-id="13dd8-141">Type of file, such as .pdf or .docx.</span></span> |

<span data-ttu-id="13dd8-142">最佳做法是，通过向用户发送回一条消息来确认文件上载。</span><span class="sxs-lookup"><span data-stu-id="13dd8-142">As a best practice, acknowledge the file upload by sending a message back to the user.</span></span>

### <a name="uploading-files-to-personal-chat"></a><span data-ttu-id="13dd8-143">将文件上载到个人聊天</span><span class="sxs-lookup"><span data-stu-id="13dd8-143">Uploading files to personal chat</span></span>

<span data-ttu-id="13dd8-144">将文件上载到用户需要执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="13dd8-144">The following steps are required to upload a file to a user:</span></span>

1. <span data-ttu-id="13dd8-145">向请求写入文件权限的用户发送邮件。</span><span class="sxs-lookup"><span data-stu-id="13dd8-145">Send a message to the user requesting permission to write the file.</span></span> <span data-ttu-id="13dd8-146">此邮件必须包含 `FileConsentCard` 包含要上载的文件的名称的附件。</span><span class="sxs-lookup"><span data-stu-id="13dd8-146">This message must contain a `FileConsentCard` attachment with the name of the file to be uploaded.</span></span>
2. <span data-ttu-id="13dd8-147">如果用户接受文件下载，机器人将收到包含位置 URL 的调用活动。</span><span class="sxs-lookup"><span data-stu-id="13dd8-147">If the user accepts the file download, the bot receives an invoke activity with a location URL.</span></span>
3. <span data-ttu-id="13dd8-148">若要传输文件，机器人将直接 `HTTP POST` 执行输入提供的位置 URL。</span><span class="sxs-lookup"><span data-stu-id="13dd8-148">To transfer the file, the bot performs an `HTTP POST` directly into the provided location URL.</span></span>
4. <span data-ttu-id="13dd8-149">（可选）如果不希望用户接受同一文件的进一步上载，请删除原始同意卡。</span><span class="sxs-lookup"><span data-stu-id="13dd8-149">Optionally, remove the original consent card if you do not want the user to accept further uploads of the same file.</span></span>

#### <a name="message-requesting-permission-to-upload"></a><span data-ttu-id="13dd8-150">请求上传权限的邮件</span><span class="sxs-lookup"><span data-stu-id="13dd8-150">Message requesting permission to upload</span></span>

<span data-ttu-id="13dd8-151">以下桌面邮件包含一个简单的附件对象，该对象请求用户上载文件的权限：</span><span class="sxs-lookup"><span data-stu-id="13dd8-151">The following desktop message contains a simple attachment object requesting user permission to upload the file:</span></span>

![请求用户上载文件权限的许可卡](../../assets/images/bots/bot-file-consent-card.png)

<span data-ttu-id="13dd8-153">以下移动邮件包含一个附件对象，该对象请求用户上载文件的权限：</span><span class="sxs-lookup"><span data-stu-id="13dd8-153">The following mobile message contains an attachment object requesting user permission to upload the file:</span></span>

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

<span data-ttu-id="13dd8-155">下表描述了附件的内容属性：</span><span class="sxs-lookup"><span data-stu-id="13dd8-155">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="13dd8-156">属性</span><span class="sxs-lookup"><span data-stu-id="13dd8-156">Property</span></span> | <span data-ttu-id="13dd8-157">用途</span><span class="sxs-lookup"><span data-stu-id="13dd8-157">Purpose</span></span> |
| --- | --- |
| `description` | <span data-ttu-id="13dd8-158">描述文件的用途或总结其内容。</span><span class="sxs-lookup"><span data-stu-id="13dd8-158">Describes the purpose of the file or summarizes its content.</span></span> |
| `sizeInBytes` | <span data-ttu-id="13dd8-159">为用户提供估计的文件大小及其在 OneDrive 中占用的空间量。</span><span class="sxs-lookup"><span data-stu-id="13dd8-159">Provides the user an estimate of the file size and the amount of space it takes in OneDrive.</span></span> |
| `acceptContext` | <span data-ttu-id="13dd8-160">用户接受文件时以静默方式传输到自动程序的其他上下文。</span><span class="sxs-lookup"><span data-stu-id="13dd8-160">Additional context that is silently transmitted to the bot when the user accepts the file.</span></span> |
| `declineContext` | <span data-ttu-id="13dd8-161">当用户拒绝文件时以静默方式传输到自动程序的其他上下文。</span><span class="sxs-lookup"><span data-stu-id="13dd8-161">Additional context that is silently transmitted to the bot when the user declines the file.</span></span> |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a><span data-ttu-id="13dd8-162">当用户接受文件时调用活动</span><span class="sxs-lookup"><span data-stu-id="13dd8-162">Invoke activity when the user accepts the file</span></span>

<span data-ttu-id="13dd8-163">当用户接受文件时，将调用活动发送到机器人。</span><span class="sxs-lookup"><span data-stu-id="13dd8-163">An invoke activity is sent to the bot if and when the user accepts the file.</span></span> <span data-ttu-id="13dd8-164">它包含 OneDrive for Business 占位符 URL，然后机器人可以发出 a `PUT` 以传输文件内容。</span><span class="sxs-lookup"><span data-stu-id="13dd8-164">It contains the OneDrive for Business placeholder URL that the bot can then issue a `PUT` into to transfer the file contents.</span></span> <span data-ttu-id="13dd8-165">有关上载到 OneDrive URL 的信息，请参阅"[将字节上载到上载会话"。](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)</span><span class="sxs-lookup"><span data-stu-id="13dd8-165">For information on uploading to the OneDrive URL, see [Upload bytes to the upload session](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).</span></span>

<span data-ttu-id="13dd8-166">以下示例显示了自动程序收到的调用活动的简洁版本：</span><span class="sxs-lookup"><span data-stu-id="13dd8-166">The following example shows a concise version of the invoke activity that the bot receives:</span></span>

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

<span data-ttu-id="13dd8-167">同样，如果用户拒绝文件，自动程序将收到以下事件，事件的总体活动名称相同：</span><span class="sxs-lookup"><span data-stu-id="13dd8-167">Similarly, if the user declines the file, the bot receives the following event with the same overall activity name:</span></span>

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

### <a name="notifying-the-user-about-an-uploaded-file"></a><span data-ttu-id="13dd8-168">通知用户已上载文件</span><span class="sxs-lookup"><span data-stu-id="13dd8-168">Notifying the user about an uploaded file</span></span>

<span data-ttu-id="13dd8-169">将文件上传到用户的 OneDrive 后，向用户发送确认消息。</span><span class="sxs-lookup"><span data-stu-id="13dd8-169">After uploading a file to the user's OneDrive, send a confirmation message to the user.</span></span> <span data-ttu-id="13dd8-170">邮件必须包含用户可以选择的以下附件，以在 OneDrive 中预览或打开它， `FileCard` 或在本地下载：</span><span class="sxs-lookup"><span data-stu-id="13dd8-170">The message must contain the following `FileCard` attachment that the user can select, either to preview or open it in OneDrive, or download locally:</span></span>

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

<span data-ttu-id="13dd8-171">下表描述了附件的内容属性：</span><span class="sxs-lookup"><span data-stu-id="13dd8-171">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="13dd8-172">属性</span><span class="sxs-lookup"><span data-stu-id="13dd8-172">Property</span></span> | <span data-ttu-id="13dd8-173">用途</span><span class="sxs-lookup"><span data-stu-id="13dd8-173">Purpose</span></span> |
| --- | --- |
| `uniqueId` | <span data-ttu-id="13dd8-174">OneDrive 或 SharePoint 驱动器项 ID。</span><span class="sxs-lookup"><span data-stu-id="13dd8-174">OneDrive or SharePoint drive item ID.</span></span> |
| `fileType` | <span data-ttu-id="13dd8-175">文件类型，如 .pdf 或 .docx。</span><span class="sxs-lookup"><span data-stu-id="13dd8-175">Type of file, such as .pdf or .docx.</span></span> |

### <a name="basic-example-in-c"></a><span data-ttu-id="13dd8-176">C 中的基本示例#</span><span class="sxs-lookup"><span data-stu-id="13dd8-176">Basic example in C#</span></span>

<span data-ttu-id="13dd8-177">以下示例演示如何在自动程序对话框中处理文件上载和发送文件同意请求：</span><span class="sxs-lookup"><span data-stu-id="13dd8-177">The following sample shows how to handle file uploads and send file consent requests in the bot's dialog:</span></span>

```csharp

protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    string filename = "teams-logo.png";
    string filePath = Path.Combine("Files", filename);
    long fileSize = new FileInfo(filePath).Length;
    await SendFileCardAsync(turnContext, filename, fileSize, cancellationToken);
}

private async Task SendFileCardAsync(ITurnContext turnContext, string filename, long filesize, CancellationToken cancellationToken)
{
    var consentContext = new Dictionary<string, string>
    {
        { "filename", filename 
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
    replyActivity.Attachments = new List<Attachment>() { asAttachment 
    };
    await turnContext.SendActivityAsync(replyActivity, cancellationToken);
}

protected override async Task OnTeamsFileConsentAcceptAsync(ITurnContext<IInvokeActivity> turnContext, FileConsentCardResponse fileConsentCardResponse, CancellationToken cancellationToken)
{
    try
    {
        JToken context = JObject.FromObject(fileConsentCardResponse.Context);

        string filePath = Path.Combine("Files", context["filename"].ToString());
        long fileSize = new FileInfo(filePath).Length;
        var client = _clientFactory.CreateClient();
        using (var fileStream = File.OpenRead(filePath))
        {
            var fileContent = new StreamContent(fileStream);
            fileContent.Headers.ContentLength = fileSize;
            fileContent.Headers.ContentRange = new ContentRangeHeaderValue(0, fileSize - 1, fileSize);
            await client.PutAsync(fileConsentCardResponse.UploadInfo.UploadUrl, fileContent, cancellationToken);
        }

        await FileUploadCompletedAsync(turnContext, fileConsentCardResponse, cancellationToken);
    }
    catch (Exception e)
    {
        await FileUploadFailedAsync(turnContext, e.ToString(), cancellationToken);
    }
}

protected override async Task OnTeamsFileConsentDeclineAsync(ITurnContext<IInvokeActivity> turnContext, FileConsentCardResponse fileConsentCardResponse, CancellationToken cancellationToken)
{
    JToken context = JObject.FromObject(fileConsentCardResponse.Context);

    var reply = MessageFactory.Text($"Declined. We won't upload file <b>{context["filename"]}</b>.");
    reply.TextFormat = "xml";
    await turnContext.SendActivityAsync(reply, cancellationToken);
}

private async Task FileUploadCompletedAsync(ITurnContext turnContext, FileConsentCardResponse fileConsentCardResponse, CancellationToken cancellationToken)
{
    var downloadCard = new FileInfoCard
    {
        UniqueId = fileConsentCardResponse.UploadInfo.UniqueId,
        FileType = fileConsentCardResponse.UploadInfo.FileType,
    };

    var asAttachment = new Attachment
    {
        Content = downloadCard,
        ContentType = FileInfoCard.ContentType,
        Name = fileConsentCardResponse.UploadInfo.Name,
        ContentUrl = fileConsentCardResponse.UploadInfo.ContentUrl,
    };

    var reply = MessageFactory.Text($"<b>File uploaded.</b> Your file <b>{fileConsentCardResponse.UploadInfo.Name}</b> is ready to download");
    reply.TextFormat = "xml";
    reply.Attachments = new List<Attachment> { asAttachment 
    };

    await turnContext.SendActivityAsync(reply, cancellationToken);
}

private async Task FileUploadFailedAsync(ITurnContext turnContext, string error, CancellationToken cancellationToken)
{
    var reply = MessageFactory.Text($"<b>File upload failed.</b> Error: <pre>{error}</pre>");
    reply.TextFormat = "xml";
    await turnContext.SendActivityAsync(reply, cancellationToken);
}
```
