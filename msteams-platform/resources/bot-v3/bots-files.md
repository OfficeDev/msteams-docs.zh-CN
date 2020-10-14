---
title: 从 bot 发送和接收文件
description: 介绍如何从 bot 发送和接收文件
keywords: 团队 bot 文件发送接收
ms.date: 05/20/2019
ms.openlocfilehash: b61e7f6934846b3abb1cfc16283cec1d264d7ecc
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452777"
---
# <a name="send-and-receive-files-through-your-bot"></a><span data-ttu-id="655d8-104">通过你的 bot 发送和接收文件</span><span class="sxs-lookup"><span data-stu-id="655d8-104">Send and receive files through your bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="655d8-105">有两种方法可以在 bot 之间发送文件：</span><span class="sxs-lookup"><span data-stu-id="655d8-105">There are two ways to send files to and from a bot:</span></span>

* <span data-ttu-id="655d8-106">使用 Microsoft Graph Api。</span><span class="sxs-lookup"><span data-stu-id="655d8-106">Using the Microsoft Graph APIs.</span></span> <span data-ttu-id="655d8-107">此方法适用于团队中所有范围内的 bot：</span><span class="sxs-lookup"><span data-stu-id="655d8-107">This method works for bots in all scopes in Teams:</span></span>
  * `personal`
  * `channel`
  * `groupchat`
* <span data-ttu-id="655d8-108">使用团队 Api。</span><span class="sxs-lookup"><span data-stu-id="655d8-108">Using the Teams APIs.</span></span> <span data-ttu-id="655d8-109">这些仅支持一个上下文中的文件：</span><span class="sxs-lookup"><span data-stu-id="655d8-109">These only support files in one context:</span></span>
  * `personal`

## <a name="using-the-microsoft-graph-apis"></a><span data-ttu-id="655d8-110">使用 Microsoft Graph Api</span><span class="sxs-lookup"><span data-stu-id="655d8-110">Using the Microsoft Graph APIs</span></span>

<span data-ttu-id="655d8-111">您可以使用适用于 [OneDrive 和 SharePoint](/onedrive/developer/rest-api/)的 Microsoft Graph api，使用包含卡片附件的邮件发布引用现有 SharePoint 文件的邮件。</span><span class="sxs-lookup"><span data-stu-id="655d8-111">You can post messages with card attachments referencing existing SharePoint files using the Microsoft Graph APIs for [OneDrive and SharePoint](/onedrive/developer/rest-api/).</span></span> <span data-ttu-id="655d8-112">使用 Graph Api 需要获取对用户的 OneDrive 文件夹 (和文件的访问 `personal` 权限 `groupchat`) 或团队通道中的文件 (`channel` 通过标准 OAuth 2.0 授权流) 的文件。</span><span class="sxs-lookup"><span data-stu-id="655d8-112">Using the Graph APIs requires obtaining access to a user's OneDrive folder (for `personal` and `groupchat` files) or the files in a team's channels (for `channel` files) through the standard OAuth 2.0 authorization flow.</span></span> <span data-ttu-id="655d8-113">此方法适用于所有团队作用域。</span><span class="sxs-lookup"><span data-stu-id="655d8-113">This method works in all Teams scopes.</span></span>

## <a name="using-the-teams-bot-apis"></a><span data-ttu-id="655d8-114">使用团队 Bot Api</span><span class="sxs-lookup"><span data-stu-id="655d8-114">Using the Teams Bot APIs</span></span>

> [!NOTE]
> <span data-ttu-id="655d8-115">此方法仅在上下文中有效 `personal` 。</span><span class="sxs-lookup"><span data-stu-id="655d8-115">This method works only in the `personal` context.</span></span> <span data-ttu-id="655d8-116">它在或上下文中不起作用 `channel` `groupchat` 。</span><span class="sxs-lookup"><span data-stu-id="655d8-116">It does not work in the `channel` or `groupchat` context.</span></span>

<span data-ttu-id="655d8-117">你的 bot 可以使用团队 Api 直接在上下文中的用户发送和接收文件 `personal` （也称为个人聊天）。</span><span class="sxs-lookup"><span data-stu-id="655d8-117">Your bot can directly send and receive files with users in the `personal` context, also known as personal chats, using Teams APIs.</span></span> <span data-ttu-id="655d8-118">这样，您就可以实现费用报告、图像识别、文件存档、电子签名和其他涉及直接操作文件内容的方案。</span><span class="sxs-lookup"><span data-stu-id="655d8-118">This lets you implement expense reporting, image recognition, file archival, e-signatures, and other scenarios involving direct manipulation of file content.</span></span> <span data-ttu-id="655d8-119">在团队中共享的文件通常显示为卡片，并允许进行丰富的应用程序内查看。</span><span class="sxs-lookup"><span data-stu-id="655d8-119">Files shared in Teams typically appear as cards, and allow rich in-app viewing.</span></span>

<span data-ttu-id="655d8-120">以下各节介绍如何执行此操作以通过直接用户交互（如发送邮件）发送文件内容。</span><span class="sxs-lookup"><span data-stu-id="655d8-120">The following sections describe how to do this to send file content as a result of direct user interaction, like sending a message.</span></span> <span data-ttu-id="655d8-121">此 API 作为 Microsoft 团队 Bot 平台的一部分提供。</span><span class="sxs-lookup"><span data-stu-id="655d8-121">This API is provided as part of the Microsoft Teams Bot Platform.</span></span>

### <a name="configure-your-bot-to-support-files"></a><span data-ttu-id="655d8-122">将你的 bot 配置为支持文件</span><span class="sxs-lookup"><span data-stu-id="655d8-122">Configure your bot to support files</span></span>

<span data-ttu-id="655d8-123">为了在你的 bot 中发送和接收文件，您必须将 `supportsFiles` 清单中的属性设置为 `true` 。</span><span class="sxs-lookup"><span data-stu-id="655d8-123">In order to send and receive files in your bot, you have to set the `supportsFiles` property in the manifest to `true`.</span></span> <span data-ttu-id="655d8-124">此属性在清单参考的 " [bot](~/resources/schema/manifest-schema.md#bots) " 部分中进行描述。</span><span class="sxs-lookup"><span data-stu-id="655d8-124">This property is described in the [bots](~/resources/schema/manifest-schema.md#bots) section of the Manifest reference.</span></span>

<span data-ttu-id="655d8-125">定义将如下所示： `"supportsFiles": true` 。</span><span class="sxs-lookup"><span data-stu-id="655d8-125">The definition will look like this: `"supportsFiles": true`.</span></span> <span data-ttu-id="655d8-126">如果你的 bot 未启用 `supportsFiles` ，以下功能将不起作用。</span><span class="sxs-lookup"><span data-stu-id="655d8-126">If your bot does not enable `supportsFiles`, the following features will not work.</span></span>

### <a name="receiving-files-in-personal-chat"></a><span data-ttu-id="655d8-127">在个人聊天中接收文件</span><span class="sxs-lookup"><span data-stu-id="655d8-127">Receiving files in personal chat</span></span>

<span data-ttu-id="655d8-128">当用户向你的 bot 发送文件时，首先将该文件上传到用户的 OneDrive for Business 存储。</span><span class="sxs-lookup"><span data-stu-id="655d8-128">When a user sends a file to your bot, the file is first uploaded to the user's OneDrive for Business storage.</span></span> <span data-ttu-id="655d8-129">然后，你的 bot 将收到一条消息活动，通知用户上传。</span><span class="sxs-lookup"><span data-stu-id="655d8-129">Your bot will then receive a message activity notifying you of the user upload.</span></span> <span data-ttu-id="655d8-130">该活动将包含文件元数据，例如其名称和内容 URL。</span><span class="sxs-lookup"><span data-stu-id="655d8-130">The activity will contain file metadata, such as its name and the content URL.</span></span> <span data-ttu-id="655d8-131">您可以直接从该 URL 读取以提取其二进制内容。</span><span class="sxs-lookup"><span data-stu-id="655d8-131">You can directly read from this URL to fetch its binary content.</span></span>

#### <a name="message-activity-with-file-attachment-example"></a><span data-ttu-id="655d8-132">带有文件附件的邮件活动示例</span><span class="sxs-lookup"><span data-stu-id="655d8-132">Message activity with file attachment example</span></span>

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

<span data-ttu-id="655d8-133">下表描述了附件的内容属性：</span><span class="sxs-lookup"><span data-stu-id="655d8-133">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="655d8-134">属性</span><span class="sxs-lookup"><span data-stu-id="655d8-134">Property</span></span> | <span data-ttu-id="655d8-135">用途</span><span class="sxs-lookup"><span data-stu-id="655d8-135">Purpose</span></span> |
| --- | --- |
| `downloadUrl` | <span data-ttu-id="655d8-136">OneDrive URL，用于提取文件内容。</span><span class="sxs-lookup"><span data-stu-id="655d8-136">OneDrive URL for fetching the content of the file.</span></span> <span data-ttu-id="655d8-137">您可以 `HTTP GET` 直接从此 URL 发出。</span><span class="sxs-lookup"><span data-stu-id="655d8-137">You can issue an `HTTP GET` directly from this URL.</span></span> |
| `uniqueId` | <span data-ttu-id="655d8-138">唯一的文件 ID。</span><span class="sxs-lookup"><span data-stu-id="655d8-138">Unique file ID.</span></span> <span data-ttu-id="655d8-139">如果用户将文件发送到你的 bot，这将是 OneDrive 驱动器项目 ID。</span><span class="sxs-lookup"><span data-stu-id="655d8-139">This will be the OneDrive drive item ID, in the case of the user sending a file to your bot.</span></span> |
| `fileType` | <span data-ttu-id="655d8-140">文件扩展名类型，如 pdf 或 .docx。</span><span class="sxs-lookup"><span data-stu-id="655d8-140">File extension type, such as pdf or docx.</span></span> |

<span data-ttu-id="655d8-141">作为一种最佳做法，您应通过向用户发送回邮件来确认文件上载。</span><span class="sxs-lookup"><span data-stu-id="655d8-141">As a best practice, you should acknowledge the file upload by sending back a message to the user.</span></span>

### <a name="uploading-files-to-personal-chat"></a><span data-ttu-id="655d8-142">将文件上传到个人聊天</span><span class="sxs-lookup"><span data-stu-id="655d8-142">Uploading files to personal chat</span></span>

<span data-ttu-id="655d8-143">将文件上传到用户涉及以下步骤：</span><span class="sxs-lookup"><span data-stu-id="655d8-143">Uploading a file to a user involves the following steps:</span></span>

1. <span data-ttu-id="655d8-144">向用户发送一封邮件，请求写入该文件的权限。</span><span class="sxs-lookup"><span data-stu-id="655d8-144">Send a message to the user requesting permission to write the file.</span></span> <span data-ttu-id="655d8-145">此邮件必须包含 `FileConsentCard` 要上载的文件的名称附件。</span><span class="sxs-lookup"><span data-stu-id="655d8-145">This message must contain a `FileConsentCard` attachment with the name of the file to be uploaded.</span></span>
2. <span data-ttu-id="655d8-146">如果用户接受文件下载，则你的 bot 将收到具有位置 URL 的 *调用* 活动。</span><span class="sxs-lookup"><span data-stu-id="655d8-146">If the user accepts the file download, your bot will receive an *Invoke* activity with a location URL.</span></span>
3. <span data-ttu-id="655d8-147">若要转移文件，你的 bot 将 `HTTP POST` 直接执行提供的位置 URL 中的。</span><span class="sxs-lookup"><span data-stu-id="655d8-147">To transfer the file, your bot performs an `HTTP POST` directly into the provided location URL.</span></span>
4. <span data-ttu-id="655d8-148">（可选）如果您不希望允许用户接受对同一文件的更多上载，则可以删除原始同意卡。</span><span class="sxs-lookup"><span data-stu-id="655d8-148">Optionally, you can remove the original consent card if you do not want to allow the user to accept further uploads of the same file.</span></span>

#### <a name="message-requesting-permission-to-upload"></a><span data-ttu-id="655d8-149">邮件请求上载的权限</span><span class="sxs-lookup"><span data-stu-id="655d8-149">Message requesting permission to upload</span></span>

<span data-ttu-id="655d8-150">此桌面邮件包含一个简单的附件对象，该对象请求用户上载文件的权限：</span><span class="sxs-lookup"><span data-stu-id="655d8-150">This desktop message contains a simple attachment object requesting user permission to upload the file:</span></span>

![同意卡的屏幕截图请求用户上载文件的权限](../../assets/images/bots/bot-file-consent-card.png)

<span data-ttu-id="655d8-152">此移动邮件包含一个附件对象，该对象请求用户上载文件的权限：</span><span class="sxs-lookup"><span data-stu-id="655d8-152">This mobile message contains an attachment object requesting user permission to upload the file:</span></span>

![同意卡的屏幕截图请求用户在移动时上载文件的权限](../../assets/images/bots/mobile-bot-file-consent-card.png)

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

<span data-ttu-id="655d8-154">下表描述了附件的内容属性：</span><span class="sxs-lookup"><span data-stu-id="655d8-154">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="655d8-155">属性</span><span class="sxs-lookup"><span data-stu-id="655d8-155">Property</span></span> | <span data-ttu-id="655d8-156">用途</span><span class="sxs-lookup"><span data-stu-id="655d8-156">Purpose</span></span> |
| --- | --- |
| `description` | <span data-ttu-id="655d8-157">文件的说明。</span><span class="sxs-lookup"><span data-stu-id="655d8-157">Description of the file.</span></span> <span data-ttu-id="655d8-158">可能会向用户显示描述其用途或汇总其内容的用户。</span><span class="sxs-lookup"><span data-stu-id="655d8-158">May be shown to the user to describe its purpose or to summarize its content.</span></span> |
| `sizeInBytes` | <span data-ttu-id="655d8-159">为用户提供文件大小和 OneDrive 中所需的空间量的估计值。</span><span class="sxs-lookup"><span data-stu-id="655d8-159">Provides the user an estimate of the file size and the amount of space it will take in OneDrive.</span></span> |
| `acceptContext` | <span data-ttu-id="655d8-160">用户接受文件时将以静默方式传输到你的 bot 的其他上下文。</span><span class="sxs-lookup"><span data-stu-id="655d8-160">Additional context that will be silently transmitted to your bot when the user accepts the file.</span></span> |
| `declineContext` | <span data-ttu-id="655d8-161">当用户拒绝文件时，将以静默方式传输到你的 bot 的其他上下文。</span><span class="sxs-lookup"><span data-stu-id="655d8-161">Additional context that will be silently transmitted to your bot when the user declines the file.</span></span> |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a><span data-ttu-id="655d8-162">用户接受文件时调用活动</span><span class="sxs-lookup"><span data-stu-id="655d8-162">Invoke activity when the user accepts the file</span></span>

<span data-ttu-id="655d8-163">当用户接受文件时，会向你的 bot 发送一个 invoke 活动。</span><span class="sxs-lookup"><span data-stu-id="655d8-163">An invoke activity is sent to your bot if and when the user accepts the file.</span></span> <span data-ttu-id="655d8-164">它包含 OneDrive for Business 占位符 URL，你的 bot 可以通过它发出 `PUT` 进入以转移文件内容。</span><span class="sxs-lookup"><span data-stu-id="655d8-164">It contains the OneDrive for Business placeholder URL that your bot can then issue a `PUT` into to transfer the file contents.</span></span> <span data-ttu-id="655d8-165">有关上载到 OneDrive URL 的信息，请参阅本文： [将字节上传到上传会话](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)。</span><span class="sxs-lookup"><span data-stu-id="655d8-165">for information on uploading to the OneDrive URL read this article: [Upload bytes to the upload session](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).</span></span>

<span data-ttu-id="655d8-166">下面的示例展示了你的 bot 将接收的 invoke 活动的 abridged 版本：</span><span class="sxs-lookup"><span data-stu-id="655d8-166">The following example shows an abridged version of the invoke activity that your bot will receive:</span></span>

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

<span data-ttu-id="655d8-167">同样，如果用户拒绝该文件，你的 bot 将收到以下事件，其中包含相同的总体活动名称：</span><span class="sxs-lookup"><span data-stu-id="655d8-167">Similarly, if the user declines the file, your bot will receive the following event, with the same overall activity name:</span></span>

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

### <a name="notifying-the-user-about-an-uploaded-file"></a><span data-ttu-id="655d8-168">通知用户有关上载的文件</span><span class="sxs-lookup"><span data-stu-id="655d8-168">Notifying the user about an uploaded file</span></span>

<span data-ttu-id="655d8-169">将文件上传到用户的 OneDrive 之后，无论您使用的是上述机制还是 OneDrive 用户委派 Api，都应向用户发送一条确认消息。</span><span class="sxs-lookup"><span data-stu-id="655d8-169">After uploading a file to the user's OneDrive, whether you use the mechanism described above or OneDrive user delegated APIs, you should send a confirmation message to the user.</span></span> <span data-ttu-id="655d8-170">此邮件应包含 `FileCard` 用户可单击的附件，可在 OneDrive 中进行预览、在 OneDrive 中打开或在本地下载。</span><span class="sxs-lookup"><span data-stu-id="655d8-170">This message should contain  a `FileCard` attachment that the user can click on, either to preview it, open it in OneDrive, or download locally.</span></span>

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

<span data-ttu-id="655d8-171">下表描述了附件的内容属性：</span><span class="sxs-lookup"><span data-stu-id="655d8-171">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="655d8-172">属性</span><span class="sxs-lookup"><span data-stu-id="655d8-172">Property</span></span> | <span data-ttu-id="655d8-173">用途</span><span class="sxs-lookup"><span data-stu-id="655d8-173">Purpose</span></span> |
| --- | --- |
| `uniqueId` | <span data-ttu-id="655d8-174">OneDrive/SharePoint 驱动器项目 ID。</span><span class="sxs-lookup"><span data-stu-id="655d8-174">OneDrive/SharePoint drive item ID.</span></span> |
| `fileType` | <span data-ttu-id="655d8-175">文件类型，如 pdf 或 .docx。</span><span class="sxs-lookup"><span data-stu-id="655d8-175">File type, such as pdf or docx.</span></span> |

### <a name="basic-example-in-c"></a><span data-ttu-id="655d8-176">C 中的基本示例#</span><span class="sxs-lookup"><span data-stu-id="655d8-176">Basic example in C#</span></span>

<span data-ttu-id="655d8-177">下面的示例展示了如何在你的 bot 对话框中处理文件上载和发送文件同意请求。</span><span class="sxs-lookup"><span data-stu-id="655d8-177">The following sample shows how you can handle file uploads and send file consent requests in your bot's dialog.</span></span>

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
