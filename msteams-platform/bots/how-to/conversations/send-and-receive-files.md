---
title: 发送和接收文件
author: clearab
description: 如何使用 Microsoft 团队 bot 发送和接收文件。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: e7d703f30dffaf317f22529ab56b76d859ebd8b6
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673394"
---
# <a name="send-and-receive-files-with-a-bot"></a><span data-ttu-id="98fd9-103">使用 bot 发送和接收文件</span><span class="sxs-lookup"><span data-stu-id="98fd9-103">Send and receive files with a bot</span></span>

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="98fd9-104">本文介绍如何与你的 bot 在一对一聊天中与用户交换文件。</span><span class="sxs-lookup"><span data-stu-id="98fd9-104">This article describe how to exchange files with a user in a one-to-one chat with your bot.</span></span> <span data-ttu-id="98fd9-105">您不能使用此功能在团队或组聊天中交换文件。</span><span class="sxs-lookup"><span data-stu-id="98fd9-105">You cannot use this functionality to exchange files in a team or group chat.</span></span>

<span data-ttu-id="98fd9-106">有两种方法可供选择：</span><span class="sxs-lookup"><span data-stu-id="98fd9-106">There are two approaches to choose from:</span></span>

1. <span data-ttu-id="98fd9-107">支持所有三个作用域的**Microsoft Graph api** `personal`： `channel`、和`groupchat`</span><span class="sxs-lookup"><span data-stu-id="98fd9-107">**Microsoft Graph APIs**, which supports all three scopes: `personal`, `channel`, and `groupchat`</span></span>
2. <span data-ttu-id="98fd9-108">仅支持`personal`作用域的**团队 bot api**。</span><span class="sxs-lookup"><span data-stu-id="98fd9-108">**Teams bot APIs**, which only support the `personal` scope.</span></span>

> [!NOTE] 
> <span data-ttu-id="98fd9-109">不支持在移动设备上向 bot 发送和接收文件。</span><span class="sxs-lookup"><span data-stu-id="98fd9-109">Sending and receiving files to bots on mobile devices is not supported.</span></span>

## <a name="using-the-microsoft-graph-apis"></a><span data-ttu-id="98fd9-110">使用 Microsoft Graph Api</span><span class="sxs-lookup"><span data-stu-id="98fd9-110">Using the Microsoft Graph APIs</span></span>

<span data-ttu-id="98fd9-111">您可以使用适用于[OneDrive 和 SharePoint](https://docs.microsoft.com/onedrive/developer/rest-api/)的 Microsoft Graph api，使用包含卡片附件的邮件发布引用现有 SharePoint 文件的邮件。</span><span class="sxs-lookup"><span data-stu-id="98fd9-111">You can post messages with card attachments referencing existing SharePoint files using the Microsoft Graph APIs for [OneDrive and SharePoint](https://docs.microsoft.com/onedrive/developer/rest-api/).</span></span> <span data-ttu-id="98fd9-112">使用图形 Api 需要通过标准 OAuth 2.0 流获取经过身份验证的访问权限，以：</span><span class="sxs-lookup"><span data-stu-id="98fd9-112">Using the Graph APIs requires obtaining authenticated access, through the standard OAuth 2.0 flow, to:</span></span>

- <span data-ttu-id="98fd9-113">用户的 OneDrive 文件夹（用于`personal`和`groupchat`文件）。</span><span class="sxs-lookup"><span data-stu-id="98fd9-113">A user's OneDrive folder (for `personal` and `groupchat` files).</span></span>
- <span data-ttu-id="98fd9-114">或团队频道中的文件（对于`channel`文件）。</span><span class="sxs-lookup"><span data-stu-id="98fd9-114">Or to the files in a team's channels (for `channel` files).</span></span> <span data-ttu-id="98fd9-115">此方法适用于所有团队作用域。</span><span class="sxs-lookup"><span data-stu-id="98fd9-115">This method works in all Teams scopes.</span></span>

## <a name="using-the-teams-bot-apis"></a><span data-ttu-id="98fd9-116">使用团队 Bot Api</span><span class="sxs-lookup"><span data-stu-id="98fd9-116">Using the Teams Bot APIs</span></span>

<span data-ttu-id="98fd9-117">你的 bot 可以使用团队 Api 直接在`personal`上下文中的用户发送和接收文件（也称为个人聊天）。</span><span class="sxs-lookup"><span data-stu-id="98fd9-117">Your bot can directly send and receive files with users in the `personal` context, also known as personal chats, using Teams APIs.</span></span> <span data-ttu-id="98fd9-118">这使您可以实现费用报告、图像识别、文件存档、电子签名以及涉及直接操作文件内容的其他方案等应用场景。</span><span class="sxs-lookup"><span data-stu-id="98fd9-118">This lets you implement scenarios such expense reporting, image recognition, file archival, e-signatures, and other scenarios involving direct manipulation of file content.</span></span> <span data-ttu-id="98fd9-119">在团队中共享的文件通常显示为卡片，并允许进行丰富的应用程序内查看。</span><span class="sxs-lookup"><span data-stu-id="98fd9-119">Files shared in Teams typically appear as cards, and allow rich in-app viewing.</span></span>  <span data-ttu-id="98fd9-120">API 作为**Microsoft 团队 Bot 平台**的一部分提供。</span><span class="sxs-lookup"><span data-stu-id="98fd9-120">The API is provided as part of the **Microsoft Teams Bot Platform**.</span></span>

> [!NOTE]
> <span data-ttu-id="98fd9-121">此方法仅在`personal`上下文中有效。</span><span class="sxs-lookup"><span data-stu-id="98fd9-121">This method works only in the `personal` context.</span></span> <span data-ttu-id="98fd9-122">它在`channel`或`groupchat`上下文中不起作用。</span><span class="sxs-lookup"><span data-stu-id="98fd9-122">It does not work in the `channel` or `groupchat` context.</span></span>

### <a name="configure-your-bot-to-support-files"></a><span data-ttu-id="98fd9-123">将你的 bot 配置为支持文件</span><span class="sxs-lookup"><span data-stu-id="98fd9-123">Configure your bot to support files</span></span>

<span data-ttu-id="98fd9-124">若要在你的 bot 中发送和接收文件，您`supportsFiles`必须将清单中的`true`属性设置为。</span><span class="sxs-lookup"><span data-stu-id="98fd9-124">To send and receive files in your bot, you must set the `supportsFiles` property in the manifest to `true`.</span></span> <span data-ttu-id="98fd9-125">此属性在清单参考的 " [bot](https://docs.microsoft.com/microsoftteams/platform/resources/schema/manifest-schema#bots
) " 部分中进行描述。</span><span class="sxs-lookup"><span data-stu-id="98fd9-125">This property is described in the [bots](https://docs.microsoft.com/microsoftteams/platform/resources/schema/manifest-schema#bots
) section of the Manifest reference.</span></span>

<span data-ttu-id="98fd9-126">设置如下所示： `"supportsFiles": true`。</span><span class="sxs-lookup"><span data-stu-id="98fd9-126">The setting looks like this: `"supportsFiles": true`.</span></span>

## <a name="invoke-activity-when-the-user-accepts-the-file-upload"></a><span data-ttu-id="98fd9-127">用户接受文件上传时调用活动</span><span class="sxs-lookup"><span data-stu-id="98fd9-127">Invoke activity when the user accepts the file upload</span></span>

<span data-ttu-id="98fd9-128">在同意上载后，文件将上传到用户的**OneDrive**存储。</span><span class="sxs-lookup"><span data-stu-id="98fd9-128">The file is uploaded to the user's **OneDrive** storage after the consent to upload is issued.</span></span> <span data-ttu-id="98fd9-129">Bot 将收到包含文件元数据的邮件活动，如名称和内容 URL。</span><span class="sxs-lookup"><span data-stu-id="98fd9-129">The bot will receive a message activity which contains file metadata, such as its name and the content URL.</span></span> <span data-ttu-id="98fd9-130">请按以下步骤操作：</span><span class="sxs-lookup"><span data-stu-id="98fd9-130">Follow these steps:</span></span>

1. <span data-ttu-id="98fd9-131">向用户发送一封邮件，请求写入该文件的权限。</span><span class="sxs-lookup"><span data-stu-id="98fd9-131">Send a message to the user requesting permission to write the file.</span></span> <span data-ttu-id="98fd9-132">此邮件必须包含要`FileConsentCard`上载的文件的名称附件。</span><span class="sxs-lookup"><span data-stu-id="98fd9-132">This message must contain a `FileConsentCard` attachment with the name of the file to be uploaded.</span></span>

    ![bot 文件上传权限卡片](../../../assets/images/bots/bot-file-upload-permission-card.png)

2. <span data-ttu-id="98fd9-134">如果用户接受文件上传，你的 bot 将收到带有位置 URL 的*调用*活动。</span><span class="sxs-lookup"><span data-stu-id="98fd9-134">If the user accepts the file upload, your bot will receive an *Invoke* activity with a location URL.</span></span>
3. <span data-ttu-id="98fd9-135">若要转移文件，你的 bot 将`HTTP POST`直接执行提供的位置 URL 中的。</span><span class="sxs-lookup"><span data-stu-id="98fd9-135">To transfer the file, your bot performs an `HTTP POST` directly into the provided location URL.</span></span>
4. <span data-ttu-id="98fd9-136">（可选）如果您不希望允许用户接受对同一文件的更多上载，则可以删除原始同意卡。</span><span class="sxs-lookup"><span data-stu-id="98fd9-136">Optionally, you can remove the original consent card if you do not want to allow the user to accept further uploads of the same file.</span></span>
 
<span data-ttu-id="98fd9-137">下面的示例展示了你的 bot 将接收的 invoke 活动的 abridged 版本：</span><span class="sxs-lookup"><span data-stu-id="98fd9-137">The following example shows an abridged version of the invoke activity that your bot will receive:</span></span>

```json
{
    "name": "fileConsent/invoke",
    "type": "invoke",
    "timestamp": "2019-10-24T20:22:37.875Z",
    "localTimestamp": "2019-10-24T13:22:37.875-07:00",
    "id": "f:8805947989118514037",

    ...

    "value": {
        "type": "fileUpload",
        "action": "accept",
        "context": {
            "filename": "teams-logo.png"
        },
        "uploadInfo": {
            "contentUrl": "https://contoso.sharepoint.com//personal/<user alias>/Documents/Applications/TeamsFilesBot/teams-logo.png",
            "name": "teams-logo.png",
            "uploadUrl": "https://contoso.sharepoint.com//personal/<user alias>/_api/v2.0/drive/items/01FED6KHQXVVCUCI6XVJCZZMU2WMUSA6JS/uploadSession?guid=<GUID>",
            "uniqueId": "<Unique ID>",
            "fileType": "png"
        }
    },

    "locale": "en-US"
}

```

<span data-ttu-id="98fd9-138">下表描述了附件的内容属性：</span><span class="sxs-lookup"><span data-stu-id="98fd9-138">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="98fd9-139">属性</span><span class="sxs-lookup"><span data-stu-id="98fd9-139">Property</span></span> | <span data-ttu-id="98fd9-140">用途</span><span class="sxs-lookup"><span data-stu-id="98fd9-140">Purpose</span></span> |
| --- | --- |
| `uploadUrl` | <span data-ttu-id="98fd9-141">用于上传文件内容的 OneDrive URL。</span><span class="sxs-lookup"><span data-stu-id="98fd9-141">OneDrive URL for uploading the content of the file.</span></span> |
| `uniqueId` | <span data-ttu-id="98fd9-142">唯一的文件 ID。</span><span class="sxs-lookup"><span data-stu-id="98fd9-142">Unique file ID.</span></span> <span data-ttu-id="98fd9-143">这将是 OneDrive 驱动器项目 ID。</span><span class="sxs-lookup"><span data-stu-id="98fd9-143">This will be the OneDrive drive item ID.</span></span> |
| `fileType` | <span data-ttu-id="98fd9-144">文件扩展名类型，如 pdf 或 \* png \* \*。</span><span class="sxs-lookup"><span data-stu-id="98fd9-144">File extension type, such as pdf or \*png\*\*.</span></span> |

<span data-ttu-id="98fd9-145">作为一种最佳做法，您应通过向用户发送回邮件来确认文件上载。</span><span class="sxs-lookup"><span data-stu-id="98fd9-145">As a best practice, you should acknowledge the file upload by sending back a message to the user.</span></span>

<span data-ttu-id="98fd9-146">如果用户拒绝该文件，则你的 bot 将收到以下事件，其中包含相同的总体活动名称：</span><span class="sxs-lookup"><span data-stu-id="98fd9-146">If the user declines the file, your bot will receive the following event, with the same overall activity name:</span></span>

```json
{
  "name": "fileConsent/invoke",
  "value": {
    "type": "fileUpload",
    "action": "decline",
    "context": {
      ...
    }
  }
}
```

### <a name="notifying-the-user-about-an-uploaded-file"></a><span data-ttu-id="98fd9-147">通知用户有关上载的文件</span><span class="sxs-lookup"><span data-stu-id="98fd9-147">Notifying the user about an uploaded file</span></span>

<span data-ttu-id="98fd9-148">将文件上传到用户的 OneDrive 后，应向用户发送一封确认消息。</span><span class="sxs-lookup"><span data-stu-id="98fd9-148">After uploading a file to the user's OneDrive, you should send a confirmation message to the user.</span></span> <span data-ttu-id="98fd9-149">此邮件应包含用户`FileCard`可单击的附件，可在 OneDrive 中进行预览、在 OneDrive 中打开或在本地下载。</span><span class="sxs-lookup"><span data-stu-id="98fd9-149">This message should contain  a `FileCard` attachment that the user can click on, either to preview it, open it in OneDrive, or download locally.</span></span> <span data-ttu-id="98fd9-150">示例如下。</span><span class="sxs-lookup"><span data-stu-id="98fd9-150">The following is an example.</span></span> 

```json
{
  "attachments": [{
    "contentType": "application/vnd.microsoft.teams.card.file.info",
    "contentUrl": "https://contoso.sharepoint.com/personal/johnadams_contoso_com/Documents/Applications/file_example.txt",
    "name": "file_example.txt",
    "content": {
      "uniqueId": "<unique ID>",
      "fileType": "png",
    }
  }]
}

```

<span data-ttu-id="98fd9-151">下表描述了附件的内容属性：</span><span class="sxs-lookup"><span data-stu-id="98fd9-151">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="98fd9-152">属性</span><span class="sxs-lookup"><span data-stu-id="98fd9-152">Property</span></span> | <span data-ttu-id="98fd9-153">用途</span><span class="sxs-lookup"><span data-stu-id="98fd9-153">Purpose</span></span> |
| --- | --- |
| `uniqueId` | <span data-ttu-id="98fd9-154">OneDrive/SharePoint 驱动器项目 ID。</span><span class="sxs-lookup"><span data-stu-id="98fd9-154">OneDrive/SharePoint drive item ID.</span></span> |
| `fileType` | <span data-ttu-id="98fd9-155">文件类型，如 pdf 或 .docx。</span><span class="sxs-lookup"><span data-stu-id="98fd9-155">File type, such as pdf or docx.</span></span> |

## <a name="example-using-the-bot-framework-sdk"></a><span data-ttu-id="98fd9-156">使用 Bot 框架 SDK 的示例</span><span class="sxs-lookup"><span data-stu-id="98fd9-156">Example using the Bot Framework SDK</span></span>

<span data-ttu-id="98fd9-157">下面的示例展示了如何在 bot 的对话框中处理文件上载和向用户发送文件同意请求。</span><span class="sxs-lookup"><span data-stu-id="98fd9-157">The following example shows how you can handle file uploads and send file consent requests to the user in the bot's dialog.</span></span> <span data-ttu-id="98fd9-158">下一步显示的代码段属于可运行的完整示例，可在此位置下载：[文件](https://github.com/microsoft/botbuilder-dotnet/tree/master/tests/Teams/FileUpload)。</span><span class="sxs-lookup"><span data-stu-id="98fd9-158">The code snippets shown next, belong to a complete runnable example you can download at this location: [FileUpload](https://github.com/microsoft/botbuilder-dotnet/tree/master/tests/Teams/FileUpload).</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="98fd9-159">C #/.NET</span><span class="sxs-lookup"><span data-stu-id="98fd9-159">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    bool messageWithFileDownloadInfo = turnContext.Activity.Attachments?[0].ContentType == FileDownloadInfo.ContentType;
    if (messageWithFileDownloadInfo)
    {
        var file = turnContext.Activity.Attachments[0];
        var fileDownload = JObject.FromObject(file.Content).ToObject<FileDownloadInfo>();

        string filePath = Path.Combine("Files", file.Name);

        var client = _clientFactory.CreateClient();
        var response = await client.GetAsync(fileDownload.DownloadUrl);
        using (var fileStream = new FileStream(filePath, FileMode.Create, FileAccess.Write, FileShare.None))
        {
            await response.Content.CopyToAsync(fileStream);
        }

        var reply = ((Activity)turnContext.Activity).CreateReply();
        reply.TextFormat = "xml";
        reply.Text = $"Complete downloading <b>{file.Name}</b>";
        await turnContext.SendActivityAsync(reply, cancellationToken);
    }
    else
    {
        string filename = "teams-logo.png";
        string filePath = Path.Combine("Files", filename);
        long fileSize = new FileInfo(filePath).Length;
        await SendFileCardAsync(turnContext, filename, fileSize, cancellationToken);
    }
}

private async Task SendFileCardAsync(ITurnContext turnContext, string filename, long filesize, CancellationToken cancellationToken)
{
    var consentContext = new Dictionary<string, string>
    {
        { "filename", filename },
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

    var reply = ((Activity)turnContext.Activity).CreateReply();
    reply.TextFormat = "xml";
    reply.Text = $"Declined. We won't upload file <b>{context["filename"]}</b>.";
    await turnContext.SendActivityAsync(reply, cancellationToken);
}
```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="98fd9-160">TypeScript/node.js</span><span class="sxs-lookup"><span data-stu-id="98fd9-160">TypeScript/Node.js</span></span>](#tab/typescript)

<!-- From sample: libraries\botbuilder\tests\teams\fileUpload\src\fileUploadBot.ts-->

```typescript

export class FileUploadBot extends TeamsActivityHandler {
    constructor() {
        super();

        this.onMessage(async (context, next) => {
            await this.sendFileCard(context);
            await next();
        });

        this.onMembersAdded(async (context, next) => {
            const membersAdded = context.activity.membersAdded;
            for (const member of membersAdded) {
                if (member.id !== context.activity.recipient.id) {
                    await context.sendActivity('Hello and welcome!');
                }
            }
            await next();
        });
    }

    private async sendFileCard(context: TurnContext): Promise<void> {
        let filename = "file name";
        let fs = require('fs'); 
        let path = require('path');
        let stats = fs.statSync(path.join('files', filename));
        let fileSizeInBytes = stats['size'];

        let fileContext = {
            filename: filename
        };

        let attachment = {
            content: <FileConsentCard>{
                description: 'This is the file I want to send you',
                fileSizeInBytes: fileSizeInBytes,
                acceptContext: fileContext,
                declineContext: fileContext
            },
            contentType: 'application/vnd.microsoft.teams.card.file.consent',
            name: filename
        } as Attachment;

        var replyActivity = this.createReply(context.activity);
        replyActivity.attachments = [ attachment ];
        await context.sendActivity(replyActivity);
    }

    protected async handleTeamsFileConsentAccept(context: TurnContext, fileConsentCardResponse: FileConsentCardResponse): Promise<void> {
        try {
            await this.sendFile(fileConsentCardResponse);
            await this.fileUploadCompleted(context, fileConsentCardResponse);
        }
        catch (err) {
            await this.fileUploadFailed(context, err.toString());
        }
    }

    protected async handleTeamsFileConsentDecline(context: TurnContext, fileConsentCardResponse: FileConsentCardResponse): Promise<void> {
        let reply = this.createReply(context.activity);
        reply.textFormat = "xml";
        reply.text = `Declined. We won't upload file <b>${fileConsentCardResponse.context["filename"]}</b>.`;
        await context.sendActivity(reply);
    }
...

}

```

<!-- Python samples verify -->

# <a name="pythontabpython"></a>[<span data-ttu-id="98fd9-161">Python</span><span class="sxs-lookup"><span data-stu-id="98fd9-161">Python</span></span>](#tab/python)

```python
class TeamsFileUploadBot(TeamsActivityHandler):
    async def on_message_activity(self, turn_context: TurnContext):
        message_with_file_download = (
            False
            if not turn_context.activity.attachments
            else turn_context.activity.attachments[0].content_type == ContentType.FILE_DOWNLOAD_INFO
        )

        if message_with_file_download:
            # Save an uploaded file locally
            file = turn_context.activity.attachments[0]
            file_download = FileDownloadInfo.deserialize(file.content)
            file_path = "files/" + file.name

            response = requests.get(file_download.download_url, allow_redirects=True)
            open(file_path, "wb").write(response.content)

            reply = self._create_reply(
                turn_context.activity, f"Complete downloading <b>{file.name}</b>", "xml"
            )
            await turn_context.send_activity(reply)
        else:
            # Attempt to upload a file to Teams.  This will display a confirmation to
            # the user (Accept/Decline card).  If they accept, on_teams_file_consent_accept
            # will be called, otherwise on_teams_file_consent_decline.
            filename = "teams-logo.png"
            file_path = "files/" + filename
            file_size = os.path.getsize(file_path)
            await self._send_file_card(turn_context, filename, file_size)

    async def _send_file_card(
            self, turn_context: TurnContext, filename: str, file_size: int
    ):
        """
        Send a FileConsentCard to get permission from the user to upload a file.
        """

        consent_context = {"filename": filename}

        file_card = FileConsentCard(
            description="This is the file I want to send you",
            size_in_bytes=file_size,
            accept_context=consent_context,
            decline_context=consent_context
        )

        as_attachment = Attachment(
            content=file_card.serialize(), content_type=ContentType.FILE_CONSENT_CARD, name=filename
        )

        reply_activity = self._create_reply(turn_context.activity)
        reply_activity.attachments = [as_attachment]
        await turn_context.send_activity(reply_activity)

    async def on_teams_file_consent_accept(
            self,
            turn_context: TurnContext,
            file_consent_card_response: FileConsentCardResponse
    ):
        """
        The user accepted the file upload request.  Do the actual upload now.
        """

        file_path = "files/" + file_consent_card_response.context["filename"]
        file_size = os.path.getsize(file_path)

        headers = {
            "Content-Length": f"\"{file_size}\"",
            "Content-Range": f"bytes 0-{file_size-1}/{file_size}"
        }
        response = requests.put(
            file_consent_card_response.upload_info.upload_url, open(file_path, "rb"), headers=headers
        )

        if response.status_code != 200:
            await self._file_upload_failed(turn_context, "Unable to upload file.")
        else:
            await self._file_upload_complete(turn_context, file_consent_card_response)

    async def on_teams_file_consent_decline(
            self,
            turn_context: TurnContext,
            file_consent_card_response: FileConsentCardResponse
    ):
        """
        The user declined the file upload.
        """

        context = file_consent_card_response.context

        reply = self._create_reply(
            turn_context.activity,
            f"Declined. We won't upload file <b>{context['filename']}</b>.",
            "xml"
        )
        await turn_context.send_activity(reply)

    async def _file_upload_complete(
            self,
            turn_context: TurnContext,
            file_consent_card_response: FileConsentCardResponse
    ):
        """
        The file was uploaded, so display a FileInfoCard so the user can view the
        file in Teams.
        """

        name = file_consent_card_response.upload_info.name

        download_card = FileInfoCard(
            unique_id=file_consent_card_response.upload_info.unique_id,
            file_type=file_consent_card_response.upload_info.file_type
        )

        as_attachment = Attachment(
            content=download_card.serialize(),
            content_type=ContentType.FILE_INFO_CARD,
            name=name,
            content_url=file_consent_card_response.upload_info.content_url
        )

        reply = self._create_reply(
            turn_context.activity,
            f"<b>File uploaded.</b> Your file <b>{name}</b> is ready to download",
            "xml"
        )
        reply.attachments = [as_attachment]

        await turn_context.send_activity(reply)

    async def _file_upload_failed(self, turn_context: TurnContext, error: str):
        reply = self._create_reply(
            turn_context.activity,
            f"<b>File upload failed.</b> Error: <pre>{error}</pre>",
            "xml"
        )
        await turn_context.send_activity(reply)

    def _create_reply(self, activity, text=None, text_format=None):
        return Activity(
            type=ActivityTypes.message,
            timestamp=datetime.utcnow(),
            from_property=ChannelAccount(
                id=activity.recipient.id, name=activity.recipient.name
            ),
            recipient=ChannelAccount(
                id=activity.from_property.id, name=activity.from_property.name
            ),
            reply_to_id=activity.id,
            service_url=activity.service_url,
            channel_id=activity.channel_id,
            conversation=ConversationAccount(
                is_group=activity.conversation.is_group,
                id=activity.conversation.id,
                name=activity.conversation.name,
            ),
            text=text or "",
            text_format=text_format or None,
            locale=activity.locale,
        )


```

---
