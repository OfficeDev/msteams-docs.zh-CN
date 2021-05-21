---
title: 从自动程序发送和接收文件
description: 介绍如何从自动程序发送和接收文件
keywords: teams 自动程序文件发送接收
ms.topic: how-to
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: f69a6ca9cfcdf3b1e559fbe8cf569accf3166f69
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566479"
---
# <a name="send-and-receive-files-through-your-bot"></a><span data-ttu-id="419a8-104">通过自动程序发送和接收文件</span><span class="sxs-lookup"><span data-stu-id="419a8-104">Send and receive files through your bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="419a8-105">有两种方法向自动程序发送文件和从自动程序发送文件：</span><span class="sxs-lookup"><span data-stu-id="419a8-105">There are two ways to send files to and from a bot:</span></span>

* <span data-ttu-id="419a8-106">使用 Microsoft Graph API。</span><span class="sxs-lookup"><span data-stu-id="419a8-106">Using the Microsoft Graph APIs.</span></span> <span data-ttu-id="419a8-107">此方法适用于所有范围内自动程序Teams：</span><span class="sxs-lookup"><span data-stu-id="419a8-107">This method works for bots in all scopes in Teams:</span></span>
  * `personal`
  * `channel`
  * `groupchat`
* <span data-ttu-id="419a8-108">使用 Teams API。</span><span class="sxs-lookup"><span data-stu-id="419a8-108">Using the Teams APIs.</span></span> <span data-ttu-id="419a8-109">这些仅支持一个上下文中的文件：</span><span class="sxs-lookup"><span data-stu-id="419a8-109">These only support files in one context:</span></span>
  * `personal`

## <a name="using-the-microsoft-graph-apis"></a><span data-ttu-id="419a8-110">使用 Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="419a8-110">Using the Microsoft Graph APIs</span></span>

<span data-ttu-id="419a8-111">可以使用 Microsoft Graph API 发布包含卡片附件的邮件，这些附件引用现有 SharePoint 文件[，OneDrive SharePoint。](/onedrive/developer/rest-api/)</span><span class="sxs-lookup"><span data-stu-id="419a8-111">You can post messages with card attachments referencing existing SharePoint files using the Microsoft Graph APIs for [OneDrive and SharePoint](/onedrive/developer/rest-api/).</span></span> <span data-ttu-id="419a8-112">使用 Graph API 需要通过标准 `personal` `groupchat` `channel` OAuth 2.0 授权流获取对用户的 OneDrive 文件夹 (和文件) 或团队通道 (中的文件) 的访问权限。</span><span class="sxs-lookup"><span data-stu-id="419a8-112">Using the Graph APIs requires obtaining access to a user's OneDrive folder (for `personal` and `groupchat` files) or the files in a team's channels (for `channel` files) through the standard OAuth 2.0 authorization flow.</span></span> <span data-ttu-id="419a8-113">此方法适用于所有Teams范围。</span><span class="sxs-lookup"><span data-stu-id="419a8-113">This method works in all Teams scopes.</span></span>

## <a name="using-the-teams-bot-apis"></a><span data-ttu-id="419a8-114">使用Teams程序 API</span><span class="sxs-lookup"><span data-stu-id="419a8-114">Using the Teams Bot APIs</span></span>

> [!NOTE]
> <span data-ttu-id="419a8-115">此方法仅在上下文中 `personal` 有效。</span><span class="sxs-lookup"><span data-stu-id="419a8-115">This method works only in the `personal` context.</span></span> <span data-ttu-id="419a8-116">它在 或 上下文中 `channel` `groupchat` 不起作用。</span><span class="sxs-lookup"><span data-stu-id="419a8-116">It does not work in the `channel` or `groupchat` context.</span></span>

<span data-ttu-id="419a8-117">自动程序可以直接在上下文中与用户一起发送和接收文件（也称为个人聊天）。使用 Teams `personal` API。</span><span class="sxs-lookup"><span data-stu-id="419a8-117">Your bot can directly send and receive files with users in the `personal` context, also known as personal chats, using Teams APIs.</span></span> <span data-ttu-id="419a8-118">这允许你实现费用报告、图像识别、文件存档、电子签名以及涉及直接处理文件内容的其他方案。</span><span class="sxs-lookup"><span data-stu-id="419a8-118">This lets you implement expense reporting, image recognition, file archival, e-signatures, and other scenarios involving direct manipulation of file content.</span></span> <span data-ttu-id="419a8-119">通常，Teams共享的文件显示为卡片，并允许丰富的应用内查看。</span><span class="sxs-lookup"><span data-stu-id="419a8-119">Files shared in Teams typically appear as cards, and allow rich in-app viewing.</span></span>

<span data-ttu-id="419a8-120">以下各节介绍如何通过直接用户交互（如发送消息）来发送文件内容。</span><span class="sxs-lookup"><span data-stu-id="419a8-120">The following sections describe how to do this to send file content as a result of direct user interaction, like sending a message.</span></span> <span data-ttu-id="419a8-121">此 API 作为自动程序平台的一Microsoft Teams提供。</span><span class="sxs-lookup"><span data-stu-id="419a8-121">This API is provided as part of the Microsoft Teams Bot Platform.</span></span>

### <a name="configure-your-bot-to-support-files"></a><span data-ttu-id="419a8-122">配置自动程序以支持文件</span><span class="sxs-lookup"><span data-stu-id="419a8-122">Configure your bot to support files</span></span>

<span data-ttu-id="419a8-123">为了在自动程序中发送和接收文件，你必须将清单中的 属性设置为 `supportsFiles` `true` 。</span><span class="sxs-lookup"><span data-stu-id="419a8-123">In order to send and receive files in your bot, you have to set the `supportsFiles` property in the manifest to `true`.</span></span> <span data-ttu-id="419a8-124">此属性在清单引用 [的自动程序](~/resources/schema/manifest-schema.md#bots) 部分中介绍。</span><span class="sxs-lookup"><span data-stu-id="419a8-124">This property is described in the [bots](~/resources/schema/manifest-schema.md#bots) section of the Manifest reference.</span></span>

<span data-ttu-id="419a8-125">定义将如下所示 `"supportsFiles": true` ：。</span><span class="sxs-lookup"><span data-stu-id="419a8-125">The definition will look like this: `"supportsFiles": true`.</span></span> <span data-ttu-id="419a8-126">如果自动程序未启用 `supportsFiles` ，则以下功能将不起作用。</span><span class="sxs-lookup"><span data-stu-id="419a8-126">If your bot does not enable `supportsFiles`, the following features will not work.</span></span>

### <a name="receiving-files-in-personal-chat"></a><span data-ttu-id="419a8-127">在个人聊天中接收文件</span><span class="sxs-lookup"><span data-stu-id="419a8-127">Receiving files in personal chat</span></span>

<span data-ttu-id="419a8-128">当用户将文件发送到自动程序时，该文件将首先上载到用户的OneDrive for Business存储。</span><span class="sxs-lookup"><span data-stu-id="419a8-128">When a user sends a file to your bot, the file is first uploaded to the user's OneDrive for Business storage.</span></span> <span data-ttu-id="419a8-129">然后，自动程序将收到一条消息活动，通知您用户上载。</span><span class="sxs-lookup"><span data-stu-id="419a8-129">Your bot will then receive a message activity notifying you of the user upload.</span></span> <span data-ttu-id="419a8-130">活动将包含文件元数据，例如其名称和内容 URL。</span><span class="sxs-lookup"><span data-stu-id="419a8-130">The activity will contain file metadata, such as its name and the content URL.</span></span> <span data-ttu-id="419a8-131">可以直接从此 URL 读取，以提取其二进制内容。</span><span class="sxs-lookup"><span data-stu-id="419a8-131">You can directly read from this URL to fetch its binary content.</span></span>

#### <a name="message-activity-with-file-attachment-example"></a><span data-ttu-id="419a8-132">包含文件附件的邮件活动示例</span><span class="sxs-lookup"><span data-stu-id="419a8-132">Message activity with file attachment example</span></span>

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

<span data-ttu-id="419a8-133">下表介绍了附件的内容属性：</span><span class="sxs-lookup"><span data-stu-id="419a8-133">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="419a8-134">属性</span><span class="sxs-lookup"><span data-stu-id="419a8-134">Property</span></span> | <span data-ttu-id="419a8-135">用途</span><span class="sxs-lookup"><span data-stu-id="419a8-135">Purpose</span></span> |
| --- | --- |
| `downloadUrl` | <span data-ttu-id="419a8-136">OneDrive用于提取文件内容的 URL。</span><span class="sxs-lookup"><span data-stu-id="419a8-136">OneDrive URL for fetching the content of the file.</span></span> <span data-ttu-id="419a8-137">可以直接从此 URL `HTTP GET` 发出 。</span><span class="sxs-lookup"><span data-stu-id="419a8-137">You can issue an `HTTP GET` directly from this URL.</span></span> |
| `uniqueId` | <span data-ttu-id="419a8-138">唯一文件 ID。</span><span class="sxs-lookup"><span data-stu-id="419a8-138">Unique file ID.</span></span> <span data-ttu-id="419a8-139">如果用户将文件OneDrive自动程序，这将是驱动器项 ID。</span><span class="sxs-lookup"><span data-stu-id="419a8-139">This will be the OneDrive drive item ID, in the case of the user sending a file to your bot.</span></span> |
| `fileType` | <span data-ttu-id="419a8-140">文件扩展名类型，如 pdf 或 docx。</span><span class="sxs-lookup"><span data-stu-id="419a8-140">File extension type, such as pdf or docx.</span></span> |

<span data-ttu-id="419a8-141">作为最佳实践，您应通过向用户发送回一条消息来确认文件上载。</span><span class="sxs-lookup"><span data-stu-id="419a8-141">As a best practice, you should acknowledge the file upload by sending back a message to the user.</span></span>

### <a name="uploading-files-to-personal-chat"></a><span data-ttu-id="419a8-142">将文件上载到个人聊天</span><span class="sxs-lookup"><span data-stu-id="419a8-142">Uploading files to personal chat</span></span>

<span data-ttu-id="419a8-143">将文件上载到用户涉及以下步骤：</span><span class="sxs-lookup"><span data-stu-id="419a8-143">Uploading a file to a user involves the following steps:</span></span>

1. <span data-ttu-id="419a8-144">向请求写入文件权限的用户发送邮件。</span><span class="sxs-lookup"><span data-stu-id="419a8-144">Send a message to the user requesting permission to write the file.</span></span> <span data-ttu-id="419a8-145">此邮件必须 `FileConsentCard` 包含包含要上载的文件名称的附件。</span><span class="sxs-lookup"><span data-stu-id="419a8-145">This message must contain a `FileConsentCard` attachment with the name of the file to be uploaded.</span></span>
2. <span data-ttu-id="419a8-146">如果用户接受文件下载，机器人将收到包含位置 URL 的 *Invoke* 活动。</span><span class="sxs-lookup"><span data-stu-id="419a8-146">If the user accepts the file download, your bot will receive an *Invoke* activity with a location URL.</span></span>
3. <span data-ttu-id="419a8-147">若要传输文件，机器人将直接 `HTTP POST` 执行到提供的位置 URL。</span><span class="sxs-lookup"><span data-stu-id="419a8-147">To transfer the file, your bot performs an `HTTP POST` directly into the provided location URL.</span></span>
4. <span data-ttu-id="419a8-148">或者，如果不希望允许用户接受同一文件的进一步上载，可以删除原始同意卡。</span><span class="sxs-lookup"><span data-stu-id="419a8-148">Optionally, you can remove the original consent card if you do not want to allow the user to accept further uploads of the same file.</span></span>

#### <a name="message-requesting-permission-to-upload"></a><span data-ttu-id="419a8-149">请求上传权限的邮件</span><span class="sxs-lookup"><span data-stu-id="419a8-149">Message requesting permission to upload</span></span>

<span data-ttu-id="419a8-150">此桌面邮件包含一个简单的 attachment 对象，该对象请求用户上载文件的权限：</span><span class="sxs-lookup"><span data-stu-id="419a8-150">This desktop message contains a simple attachment object requesting user permission to upload the file:</span></span>

![请求用户上传文件权限的许可卡屏幕截图](../../assets/images/bots/bot-file-consent-card.png)

<span data-ttu-id="419a8-152">此手机信息包含请求用户上传文件的附件对象：</span><span class="sxs-lookup"><span data-stu-id="419a8-152">This mobile message contains an attachment object requesting user permission to upload the file:</span></span>

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

<span data-ttu-id="419a8-154">下表介绍了附件的内容属性：</span><span class="sxs-lookup"><span data-stu-id="419a8-154">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="419a8-155">属性</span><span class="sxs-lookup"><span data-stu-id="419a8-155">Property</span></span> | <span data-ttu-id="419a8-156">用途</span><span class="sxs-lookup"><span data-stu-id="419a8-156">Purpose</span></span> |
| --- | --- |
| `description` | <span data-ttu-id="419a8-157">文件的说明。</span><span class="sxs-lookup"><span data-stu-id="419a8-157">Description of the file.</span></span> <span data-ttu-id="419a8-158">可能会向用户显示以描述其用途或汇总其内容。</span><span class="sxs-lookup"><span data-stu-id="419a8-158">May be shown to the user to describe its purpose or to summarize its content.</span></span> |
| `sizeInBytes` | <span data-ttu-id="419a8-159">为用户提供估计的文件大小及其在文件空间OneDrive。</span><span class="sxs-lookup"><span data-stu-id="419a8-159">Provides the user an estimate of the file size and the amount of space it will take in OneDrive.</span></span> |
| `acceptContext` | <span data-ttu-id="419a8-160">当用户接受文件时，将静默传输到机器人的其他上下文。</span><span class="sxs-lookup"><span data-stu-id="419a8-160">Additional context that will be silently transmitted to your bot when the user accepts the file.</span></span> |
| `declineContext` | <span data-ttu-id="419a8-161">当用户拒绝文件时将静默传输到机器人的其他上下文。</span><span class="sxs-lookup"><span data-stu-id="419a8-161">Additional context that will be silently transmitted to your bot when the user declines the file.</span></span> |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a><span data-ttu-id="419a8-162">当用户接受文件时调用活动</span><span class="sxs-lookup"><span data-stu-id="419a8-162">Invoke activity when the user accepts the file</span></span>

<span data-ttu-id="419a8-163">当用户接受文件时，会向机器人发送调用活动。</span><span class="sxs-lookup"><span data-stu-id="419a8-163">An invoke activity is sent to your bot if and when the user accepts the file.</span></span> <span data-ttu-id="419a8-164">它包含一OneDrive for Business占位符 URL，然后机器人可以向 中发出 以 `PUT` 传输文件内容。</span><span class="sxs-lookup"><span data-stu-id="419a8-164">It contains the OneDrive for Business placeholder URL that your bot can then issue a `PUT` into to transfer the file contents.</span></span> <span data-ttu-id="419a8-165">有关上载到 url 的信息，OneDrive阅读本文：Upload[字节数](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)。</span><span class="sxs-lookup"><span data-stu-id="419a8-165">for information on uploading to the OneDrive URL read this article: [Upload bytes to the upload session](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).</span></span>

<span data-ttu-id="419a8-166">以下示例显示自动程序将收到的调用活动的精简版本：</span><span class="sxs-lookup"><span data-stu-id="419a8-166">The following example shows an abridged version of the invoke activity that your bot will receive:</span></span>

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

<span data-ttu-id="419a8-167">同样，如果用户拒绝文件，机器人将收到以下事件，其整体活动名称相同：</span><span class="sxs-lookup"><span data-stu-id="419a8-167">Similarly, if the user declines the file, your bot will receive the following event, with the same overall activity name:</span></span>

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

### <a name="notifying-the-user-about-an-uploaded-file"></a><span data-ttu-id="419a8-168">通知用户已上传文件</span><span class="sxs-lookup"><span data-stu-id="419a8-168">Notifying the user about an uploaded file</span></span>

<span data-ttu-id="419a8-169">将文件上载到用户OneDrive，无论使用上述机制还是 OneDrive 用户委派 API，都应向用户发送确认消息。</span><span class="sxs-lookup"><span data-stu-id="419a8-169">After uploading a file to the user's OneDrive, whether you use the mechanism described above or OneDrive user delegated APIs, you should send a confirmation message to the user.</span></span> <span data-ttu-id="419a8-170">此邮件应包含用户可单击的附件，以预览该附件、在 OneDrive 中打开它或 `FileCard` 在本地下载。</span><span class="sxs-lookup"><span data-stu-id="419a8-170">This message should contain  a `FileCard` attachment that the user can click on, either to preview it, open it in OneDrive, or download locally.</span></span>

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

<span data-ttu-id="419a8-171">下表介绍了附件的内容属性：</span><span class="sxs-lookup"><span data-stu-id="419a8-171">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="419a8-172">属性</span><span class="sxs-lookup"><span data-stu-id="419a8-172">Property</span></span> | <span data-ttu-id="419a8-173">用途</span><span class="sxs-lookup"><span data-stu-id="419a8-173">Purpose</span></span> |
| --- | --- |
| `uniqueId` | <span data-ttu-id="419a8-174">OneDrive/SharePoint驱动器项 ID。</span><span class="sxs-lookup"><span data-stu-id="419a8-174">OneDrive/SharePoint drive item ID.</span></span> |
| `fileType` | <span data-ttu-id="419a8-175">文件类型，如 pdf 或 docx。</span><span class="sxs-lookup"><span data-stu-id="419a8-175">File type, such as pdf or docx.</span></span> |

### <a name="basic-example-in-c"></a><span data-ttu-id="419a8-176">C 中的基本示例#</span><span class="sxs-lookup"><span data-stu-id="419a8-176">Basic example in C#</span></span>

<span data-ttu-id="419a8-177">以下示例演示如何在自动程序对话框中处理文件上载和发送文件同意请求：</span><span class="sxs-lookup"><span data-stu-id="419a8-177">The following sample shows how you can handle file uploads and send file consent requests in your bot's dialog:</span></span>

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
