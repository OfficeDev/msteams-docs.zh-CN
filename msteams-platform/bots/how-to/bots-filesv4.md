---
title: 通过自动程序发送和接收文件
description: 介绍如何通过自动程序发送和接收文件
keywords: teams 自动程序文件发送接收
ms.date: 05/20/2019
ms.topic: how-to
ms.openlocfilehash: 81799e3079026a678d78a9e20b8dd3a026d2a4a6
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51697066"
---
# <a name="send-and-receive-files-through-the-bot"></a><span data-ttu-id="52b64-104">通过自动程序发送和接收文件</span><span class="sxs-lookup"><span data-stu-id="52b64-104">Send and receive files through the bot</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52b64-105">本文档中的文章基于 v4 Bot Framework SDK。</span><span class="sxs-lookup"><span data-stu-id="52b64-105">The articles in this document are based on the v4 Bot Framework SDK.</span></span>

<span data-ttu-id="52b64-106">有两种方法向自动程序发送和接收文件：</span><span class="sxs-lookup"><span data-stu-id="52b64-106">There are two ways to send files to and receive files from a bot:</span></span>

* <span data-ttu-id="52b64-107">[**使用 Microsoft Graph API：**](#use-the-graph-apis) 此方法适用于所有 Microsoft Teams 作用域中的聊天机器人：</span><span class="sxs-lookup"><span data-stu-id="52b64-107">[**Use the Microsoft Graph APIs:**](#use-the-graph-apis) This method works for bots in all Microsoft Teams scopes:</span></span>
  * `personal`
  * `channel`
  * `groupchat`

* <span data-ttu-id="52b64-108">[**使用 Teams 机器人 API：**](#use-the-teams-bot-apis) 这些仅支持上下文中 `personal` 的文件。</span><span class="sxs-lookup"><span data-stu-id="52b64-108">[**Use the Teams bot APIs:**](#use-the-teams-bot-apis) These only support files in `personal` context.</span></span>

## <a name="use-the-graph-apis"></a><span data-ttu-id="52b64-109">使用 Graph API</span><span class="sxs-lookup"><span data-stu-id="52b64-109">Use the Graph APIs</span></span>

<span data-ttu-id="52b64-110">使用 [适用于 OneDrive](/onedrive/developer/rest-api/)和 SharePoint 的 Graph API 发布包含引用现有 SharePoint 文件的卡片附件的邮件。</span><span class="sxs-lookup"><span data-stu-id="52b64-110">Post messages with card attachments that refer to existing SharePoint files, using the Graph APIs for [OneDrive and SharePoint](/onedrive/developer/rest-api/).</span></span> <span data-ttu-id="52b64-111">若要使用 Graph API，请通过标准 OAuth 2.0 授权流获取对以下任一项的访问权限：</span><span class="sxs-lookup"><span data-stu-id="52b64-111">To use the Graph APIs, obtain access to either of the following through the standard OAuth 2.0 authorization flow:</span></span>

* <span data-ttu-id="52b64-112">用户的 OneDrive 文件夹用于 `personal` 和 `groupchat` 文件。</span><span class="sxs-lookup"><span data-stu-id="52b64-112">A user's OneDrive folder for `personal` and `groupchat` files.</span></span>
* <span data-ttu-id="52b64-113">团队频道 `channel` 中的文件。</span><span class="sxs-lookup"><span data-stu-id="52b64-113">The files in a team's channel for `channel` files.</span></span>

<span data-ttu-id="52b64-114">Graph API 在所有 Teams 范围内都工作。</span><span class="sxs-lookup"><span data-stu-id="52b64-114">Graph APIs work in all Teams scopes.</span></span> <span data-ttu-id="52b64-115">有关详细信息，请参阅 [发送聊天消息文件附件](/graph/api/chatmessage-post?view=graph-rest-beta&tabs=http#example-4-file-attachments&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="52b64-115">For more information, see [send chat message file attachments](/graph/api/chatmessage-post?view=graph-rest-beta&tabs=http#example-4-file-attachments&preserve-view=true).</span></span>

<span data-ttu-id="52b64-116">或者，可以使用 Teams 自动程序 API 将文件发送到自动程序，也可以从机器人接收文件。</span><span class="sxs-lookup"><span data-stu-id="52b64-116">Alternately, you can send files to and receive files from a bot using the Teams bot APIs.</span></span>

## <a name="use-the-teams-bot-apis"></a><span data-ttu-id="52b64-117">使用 Teams 机器人 API</span><span class="sxs-lookup"><span data-stu-id="52b64-117">Use the Teams bot APIs</span></span>

> [!NOTE]
> <span data-ttu-id="52b64-118">Teams 自动程序 API 仅在上下文中 `personal` 工作。</span><span class="sxs-lookup"><span data-stu-id="52b64-118">Teams bot APIs work only in the `personal` context.</span></span> <span data-ttu-id="52b64-119">它们在 或 上下文中 `channel` `groupchat` 不起作用。</span><span class="sxs-lookup"><span data-stu-id="52b64-119">They do not work in the `channel` or `groupchat` context.</span></span>

<span data-ttu-id="52b64-120">使用 Teams API，机器人可以直接在上下文中与用户一起发送和接收文件，也称为 `personal` 个人聊天。</span><span class="sxs-lookup"><span data-stu-id="52b64-120">Using Teams APIs, the bot can directly send and receive files with users in the `personal` context, also known as personal chats.</span></span> <span data-ttu-id="52b64-121">实现涉及文件内容编辑的费用报告、图像识别、文件存档和电子签名等功能。</span><span class="sxs-lookup"><span data-stu-id="52b64-121">Implement features, such as expense reporting, image recognition, file archival, and e-signatures involving the editing of file content.</span></span> <span data-ttu-id="52b64-122">Teams 中共享的文件通常显示为卡片并允许丰富的应用内查看。</span><span class="sxs-lookup"><span data-stu-id="52b64-122">Files shared in Teams typically appear as cards and allow rich in-app viewing.</span></span>

<span data-ttu-id="52b64-123">以下各节介绍如何以直接用户交互方式发送文件内容，如发送消息。</span><span class="sxs-lookup"><span data-stu-id="52b64-123">The next sections describe how to send file content as direct user interaction, like sending a message.</span></span> <span data-ttu-id="52b64-124">此 API 作为 Teams 机器人平台的一部分提供。</span><span class="sxs-lookup"><span data-stu-id="52b64-124">This API is provided as part of the Teams bot platform.</span></span>

### <a name="configure-the-bot-to-support-files"></a><span data-ttu-id="52b64-125">配置自动程序以支持文件</span><span class="sxs-lookup"><span data-stu-id="52b64-125">Configure the bot to support files</span></span>

<span data-ttu-id="52b64-126">若要在自动程序中发送和接收文件，请将清单中的 属性 `supportsFiles` 设置为 `true` 。</span><span class="sxs-lookup"><span data-stu-id="52b64-126">To send and receive files in the bot, set the `supportsFiles` property in the manifest to `true`.</span></span> <span data-ttu-id="52b64-127">此属性在清单引用 [的自动程序](~/resources/schema/manifest-schema.md#bots) 部分中介绍。</span><span class="sxs-lookup"><span data-stu-id="52b64-127">This property is described in the [bots](~/resources/schema/manifest-schema.md#bots) section of the Manifest reference.</span></span>

<span data-ttu-id="52b64-128">定义如下所示： `"supportsFiles": true` 。</span><span class="sxs-lookup"><span data-stu-id="52b64-128">The definition looks like this, `"supportsFiles": true`.</span></span> <span data-ttu-id="52b64-129">如果自动程序未启用 `supportsFiles` ，本部分中列出的功能将不起作用。</span><span class="sxs-lookup"><span data-stu-id="52b64-129">If the bot does not enable `supportsFiles`, the features listed in this section do not work.</span></span>

### <a name="receive-files-in-personal-chat"></a><span data-ttu-id="52b64-130">接收个人聊天中的文件</span><span class="sxs-lookup"><span data-stu-id="52b64-130">Receive files in personal chat</span></span>

<span data-ttu-id="52b64-131">当用户向自动程序发送文件时，文件将首先上传到用户的 OneDrive for Business 存储。</span><span class="sxs-lookup"><span data-stu-id="52b64-131">When a user sends a file to the bot, the file is first uploaded to the user's OneDrive for business storage.</span></span> <span data-ttu-id="52b64-132">然后，机器人会收到一条消息活动，通知用户有关用户上载的信息。</span><span class="sxs-lookup"><span data-stu-id="52b64-132">The bot then receives a message activity notifying the user about the user upload.</span></span> <span data-ttu-id="52b64-133">活动包含文件元数据，例如其名称和内容 URL。</span><span class="sxs-lookup"><span data-stu-id="52b64-133">The activity contains file metadata, such as its name and the content URL.</span></span> <span data-ttu-id="52b64-134">用户可以直接从此 URL 读取，以提取其二进制内容。</span><span class="sxs-lookup"><span data-stu-id="52b64-134">The user can directly read from this URL to fetch its binary content.</span></span>

#### <a name="message-activity-with-file-attachment-example"></a><span data-ttu-id="52b64-135">包含文件附件的邮件活动示例</span><span class="sxs-lookup"><span data-stu-id="52b64-135">Message activity with file attachment example</span></span>

<span data-ttu-id="52b64-136">以下代码显示了包含文件附件的邮件活动示例：</span><span class="sxs-lookup"><span data-stu-id="52b64-136">The following code shows an example of message activity with file attachment:</span></span>

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

<span data-ttu-id="52b64-137">下表介绍了附件的内容属性：</span><span class="sxs-lookup"><span data-stu-id="52b64-137">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="52b64-138">属性</span><span class="sxs-lookup"><span data-stu-id="52b64-138">Property</span></span> | <span data-ttu-id="52b64-139">用途</span><span class="sxs-lookup"><span data-stu-id="52b64-139">Purpose</span></span> |
| --- | --- |
| `downloadUrl` | <span data-ttu-id="52b64-140">用于提取文件内容的 OneDrive URL。</span><span class="sxs-lookup"><span data-stu-id="52b64-140">OneDrive URL for fetching the content of the file.</span></span> <span data-ttu-id="52b64-141">用户可以直接从此 `HTTP GET` URL 发出 。</span><span class="sxs-lookup"><span data-stu-id="52b64-141">The user can issue an `HTTP GET` directly from this URL.</span></span> |
| `uniqueId` | <span data-ttu-id="52b64-142">唯一文件 ID。</span><span class="sxs-lookup"><span data-stu-id="52b64-142">Unique file ID.</span></span> <span data-ttu-id="52b64-143">这是 OneDrive 驱动器项 ID，以防用户向自动程序发送文件。</span><span class="sxs-lookup"><span data-stu-id="52b64-143">This is the OneDrive drive item ID, in case the user sends a file to the bot.</span></span> |
| `fileType` | <span data-ttu-id="52b64-144">文件类型，如 .pdf 或 .docx。</span><span class="sxs-lookup"><span data-stu-id="52b64-144">Type of file, such as .pdf or .docx.</span></span> |

<span data-ttu-id="52b64-145">最佳做法是，通过向用户发送回一条消息来确认文件上载。</span><span class="sxs-lookup"><span data-stu-id="52b64-145">As a best practice, acknowledge the file upload by sending a message back to the user.</span></span>

### <a name="upload-files-to-personal-chat"></a><span data-ttu-id="52b64-146">将文件上载到个人聊天</span><span class="sxs-lookup"><span data-stu-id="52b64-146">Upload files to personal chat</span></span>

<span data-ttu-id="52b64-147">**将文件上载到用户**</span><span class="sxs-lookup"><span data-stu-id="52b64-147">**To upload a file to a user**</span></span>

1. <span data-ttu-id="52b64-148">向请求写入文件权限的用户发送邮件。</span><span class="sxs-lookup"><span data-stu-id="52b64-148">Send a message to the user requesting permission to write the file.</span></span> <span data-ttu-id="52b64-149">此邮件必须 `FileConsentCard` 包含包含要上载的文件名称的附件。</span><span class="sxs-lookup"><span data-stu-id="52b64-149">This message must contain a `FileConsentCard` attachment with the name of the file to be uploaded.</span></span>
2. <span data-ttu-id="52b64-150">如果用户接受文件下载，机器人将收到包含位置 URL 的调用活动。</span><span class="sxs-lookup"><span data-stu-id="52b64-150">If the user accepts the file download, the bot receives an invoke activity with a location URL.</span></span>
3. <span data-ttu-id="52b64-151">若要传输文件，机器人将直接执行 `HTTP POST` 到提供的位置 URL。</span><span class="sxs-lookup"><span data-stu-id="52b64-151">To transfer the file, the bot performs an `HTTP POST` directly into the provided location URL.</span></span>
4. <span data-ttu-id="52b64-152">（可选）如果不希望用户接受同一文件的进一步上载，请删除原始同意卡。</span><span class="sxs-lookup"><span data-stu-id="52b64-152">Optionally, remove the original consent card if you do not want the user to accept further uploads of the same file.</span></span>

#### <a name="message-requesting-permission-to-upload"></a><span data-ttu-id="52b64-153">请求上传权限的邮件</span><span class="sxs-lookup"><span data-stu-id="52b64-153">Message requesting permission to upload</span></span>

<span data-ttu-id="52b64-154">以下桌面邮件包含一个简单的 attachment 对象，该对象请求用户上载文件的权限：</span><span class="sxs-lookup"><span data-stu-id="52b64-154">The following desktop message contains a simple attachment object requesting user permission to upload the file:</span></span>

![请求用户上传文件权限的许可卡](../../assets/images/bots/bot-file-consent-card.png)

<span data-ttu-id="52b64-156">以下手机信息包含一个附件对象，该对象请求用户上载文件的权限：</span><span class="sxs-lookup"><span data-stu-id="52b64-156">The following mobile message contains an attachment object requesting user permission to upload the file:</span></span>

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

<span data-ttu-id="52b64-157">下表介绍了附件的内容属性：</span><span class="sxs-lookup"><span data-stu-id="52b64-157">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="52b64-158">属性</span><span class="sxs-lookup"><span data-stu-id="52b64-158">Property</span></span> | <span data-ttu-id="52b64-159">用途</span><span class="sxs-lookup"><span data-stu-id="52b64-159">Purpose</span></span> |
| --- | --- |
| `description` | <span data-ttu-id="52b64-160">描述文件的用途或总结其内容。</span><span class="sxs-lookup"><span data-stu-id="52b64-160">Describes the purpose of the file or summarizes its content.</span></span> |
| `sizeInBytes` | <span data-ttu-id="52b64-161">为用户提供估计的文件大小及其在 OneDrive 中占用的空间量。</span><span class="sxs-lookup"><span data-stu-id="52b64-161">Provides the user an estimate of the file size and the amount of space it takes in OneDrive.</span></span> |
| `acceptContext` | <span data-ttu-id="52b64-162">当用户接受文件时以静默方式传输到机器人的其他上下文。</span><span class="sxs-lookup"><span data-stu-id="52b64-162">Additional context that is silently transmitted to the bot when the user accepts the file.</span></span> |
| `declineContext` | <span data-ttu-id="52b64-163">当用户拒绝文件时以静默方式传输到自动程序的其他上下文。</span><span class="sxs-lookup"><span data-stu-id="52b64-163">Additional context that is silently transmitted to the bot when the user declines the file.</span></span> |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a><span data-ttu-id="52b64-164">当用户接受文件时调用活动</span><span class="sxs-lookup"><span data-stu-id="52b64-164">Invoke activity when the user accepts the file</span></span>

<span data-ttu-id="52b64-165">如果用户接受文件，则调用活动将发送给机器人。</span><span class="sxs-lookup"><span data-stu-id="52b64-165">An invoke activity is sent to the bot if and when the user accepts the file.</span></span> <span data-ttu-id="52b64-166">它包含 OneDrive for Business 占位符 URL，然后机器人可以发出 以 `PUT` 传输文件内容。</span><span class="sxs-lookup"><span data-stu-id="52b64-166">It contains the OneDrive for Business placeholder URL that the bot can then issue a `PUT` to transfer the file contents.</span></span> <span data-ttu-id="52b64-167">有关上传到 OneDrive URL 的信息，请参阅 [将字节上传到上传会话](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)。</span><span class="sxs-lookup"><span data-stu-id="52b64-167">For information on uploading to the OneDrive URL, see [upload bytes to the upload session](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).</span></span>

<span data-ttu-id="52b64-168">以下代码显示了机器人收到的调用活动的简洁版本示例：</span><span class="sxs-lookup"><span data-stu-id="52b64-168">The following code shows an example of a concise version of the invoke activity that the bot receives:</span></span>

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

<span data-ttu-id="52b64-169">同样，如果用户拒绝文件，机器人会收到包含相同整体活动名称的以下事件：</span><span class="sxs-lookup"><span data-stu-id="52b64-169">Similarly, if the user declines the file, the bot receives the following event with the same overall activity name:</span></span>

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

### <a name="notifying-the-user-about-an-uploaded-file"></a><span data-ttu-id="52b64-170">通知用户已上传文件</span><span class="sxs-lookup"><span data-stu-id="52b64-170">Notifying the user about an uploaded file</span></span>

<span data-ttu-id="52b64-171">将文件上传到用户的 OneDrive 后，向用户发送确认消息。</span><span class="sxs-lookup"><span data-stu-id="52b64-171">After uploading a file to the user's OneDrive, send a confirmation message to the user.</span></span> <span data-ttu-id="52b64-172">邮件必须包含用户可以选择的以下附件，以在 OneDrive 中预览或打开它， `FileCard` 或在本地下载：</span><span class="sxs-lookup"><span data-stu-id="52b64-172">The message must contain the following `FileCard` attachment that the user can select, either to preview or open it in OneDrive, or download locally:</span></span>

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

<span data-ttu-id="52b64-173">下表介绍了附件的内容属性：</span><span class="sxs-lookup"><span data-stu-id="52b64-173">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="52b64-174">属性</span><span class="sxs-lookup"><span data-stu-id="52b64-174">Property</span></span> | <span data-ttu-id="52b64-175">用途</span><span class="sxs-lookup"><span data-stu-id="52b64-175">Purpose</span></span> |
| --- | --- |
| `uniqueId` | <span data-ttu-id="52b64-176">OneDrive 或 SharePoint 驱动器项 ID。</span><span class="sxs-lookup"><span data-stu-id="52b64-176">OneDrive or SharePoint drive item ID.</span></span> |
| `fileType` | <span data-ttu-id="52b64-177">文件类型，如 .pdf 或 .docx。</span><span class="sxs-lookup"><span data-stu-id="52b64-177">Type of file, such as .pdf or .docx.</span></span> |

### <a name="fetch-inline-images-from-message"></a><span data-ttu-id="52b64-178">从邮件提取内嵌图像</span><span class="sxs-lookup"><span data-stu-id="52b64-178">Fetch inline images from message</span></span>

<span data-ttu-id="52b64-179">使用 Bot 的访问令牌提取作为邮件一部分的内嵌图像。</span><span class="sxs-lookup"><span data-stu-id="52b64-179">Fetch inline images that are part of the message using the Bot's access token.</span></span>

![内联图像](../../assets/images/bots/inline-image.png)

<span data-ttu-id="52b64-181">以下代码显示从邮件提取内嵌图像的示例：</span><span class="sxs-lookup"><span data-stu-id="52b64-181">The following code shows an example of fetching inline images from message:</span></span>

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

### <a name="basic-example-in-c"></a><span data-ttu-id="52b64-182">C 中的基本示例#</span><span class="sxs-lookup"><span data-stu-id="52b64-182">Basic example in C#</span></span>

<span data-ttu-id="52b64-183">以下代码显示了如何在机器人对话框中处理文件上载和发送文件同意请求的示例：</span><span class="sxs-lookup"><span data-stu-id="52b64-183">The following code shows an example of how to handle file uploads and send file consent requests in the bot's dialog:</span></span>

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

## <a name="code-sample"></a><span data-ttu-id="52b64-184">代码示例</span><span class="sxs-lookup"><span data-stu-id="52b64-184">Code sample</span></span>

|<span data-ttu-id="52b64-185">示例名称</span><span class="sxs-lookup"><span data-stu-id="52b64-185">Sample name</span></span> | <span data-ttu-id="52b64-186">说明</span><span class="sxs-lookup"><span data-stu-id="52b64-186">Description</span></span> | <span data-ttu-id="52b64-187">.NETCore</span><span class="sxs-lookup"><span data-stu-id="52b64-187">.NETCore</span></span> | <span data-ttu-id="52b64-188">Javascript</span><span class="sxs-lookup"><span data-stu-id="52b64-188">Javascript</span></span> | <span data-ttu-id="52b64-189">Python</span><span class="sxs-lookup"><span data-stu-id="52b64-189">Python</span></span> |
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="52b64-190">File upload</span><span class="sxs-lookup"><span data-stu-id="52b64-190">File upload</span></span> | <span data-ttu-id="52b64-191">演示如何获取文件同意，以及如何从机器人将文件上载到 Teams。</span><span class="sxs-lookup"><span data-stu-id="52b64-191">Demonstrates how to obtain file consent and upload files to Teams from a bot.</span></span> <span data-ttu-id="52b64-192">此外，如何接收发送到自动程序的文件。</span><span class="sxs-lookup"><span data-stu-id="52b64-192">Also, how to receive a file sent to a bot.</span></span> | [<span data-ttu-id="52b64-193">View</span><span class="sxs-lookup"><span data-stu-id="52b64-193">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/csharp_dotnetcore/56.teams-file-upload) | [<span data-ttu-id="52b64-194">View</span><span class="sxs-lookup"><span data-stu-id="52b64-194">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/56.teams-file-upload) | [<span data-ttu-id="52b64-195">View</span><span class="sxs-lookup"><span data-stu-id="52b64-195">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/python/56.teams-file-upload) |

## <a name="next-step"></a><span data-ttu-id="52b64-196">后续步骤</span><span class="sxs-lookup"><span data-stu-id="52b64-196">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="52b64-197">通过团队中的速率限制来优化你的智能机器人</span><span class="sxs-lookup"><span data-stu-id="52b64-197">Optimize your bot with rate limiting in Teams</span></span>](~/bots/how-to/rate-limit.md)
