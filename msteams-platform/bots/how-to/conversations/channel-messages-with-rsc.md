---
title: 使用 RSC 接收所有频道消息
author: surbhigupta12
description: 接收具有 RSC 权限的所有通道消息
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: a78910b083943e5296f3e0d50eae00a713f194aa
ms.sourcegitcommit: e40383d9081bf117030f7e6270140e6b94214e8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65102062"
---
# <a name="receive-all-channel-messages-with-rsc"></a>使用 RSC 接收所有频道消息

最初为Teams Graph API 开发的资源特定许可 (RSC) 权限模型已扩展到机器人方案。

使用 RSC，现在可以请求团队所有者同意机器人通过团队中的标准频道接收用户消息，而无需@mentioned。 通过在已启用 RSC 的Teams应用清单中指定`ChannelMessage.Read.Group`权限来启用此功能。 配置后，团队所有者可以在应用安装过程中授予许可。

有关为应用启用 RSC 的详细信息，请[参阅Teams中的资源特定许可](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest)。

## <a name="enable-bots-to-receive-all-channel-messages"></a>使机器人能够接收所有通道消息

RSC 权 `ChannelMessage.Read.Group` 限将扩展到机器人。 在用户同意的情况下，此权限允许图形应用程序获取会话和机器人中的所有消息，以接收所有通道消息，而无需@mentioned。

> [!NOTE]
>
> * 需要访问所有Teams消息数据的服务必须使用Graph API，这些 API 还提供对频道和聊天中存档数据的访问权限。
> * 机器人必须适当地使用 `ChannelMessage.Read.Group` RSC 权限来生成和增强团队中用户的参与体验，否则不会通过应用商店批准。 应用说明必须包括机器人如何使用它读取的数据。
> * `ChannelMessage.Read.Group`机器人可能无法使用 RSC 权限来提取大量客户数据。

## <a name="update-app-manifest"></a>更新应用清单

机器人必须使用属性中指定的权限在Teams应用清单`ChannelMessage.Read.Group`中`webApplicationInfo`配置 RSC 才能接收所有通道消息。

![更新应用清单](~/bots/how-to/conversations/Media/appmanifest.png)


下面是对象的 `webApplicationInfo` 示例：

* **id**：你的Microsoft Azure Active Directory (Azure AD) 应用 ID。 这可以与机器人 ID 相同。
* **resource**：任何字符串。 此字段在 RSC 中没有操作，但必须添加并具有一个值以避免错误响应。
* **applicationPermissions**：必须指定应用的 `ChannelMessage.Read.Group` RSC 权限。 有关详细信息，请参阅 [特定于资源的权限](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions)。

以下代码提供了应用清单的示例：

```json
"webApplicationInfo": {
"id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
"resource": "https://AnyString",
"applicationPermissions": [
"ChannelMessage.Read.Group"
    ]
  }
```

## <a name="sideload-in-a-team"></a>团队中的旁加载

若要旁加载团队以进行测试，是否在不@mentioned的情况下接收具有 RSC 的团队中的所有频道消息：

1. 选择或创建团队。
1. 从左窗格中选择省略号 &#x25CF;&#x25CF;&#x25CF; 。 将显示下拉菜单。
1. 从下拉菜单中选择 **“管理团队** ”。 将显示详细信息。

   ![在团队中管理应用](~/bots/how-to/conversations/Media/managingteam.png)

      :::image type="content" source="Media/managingteam.png" alt-text="管理团队"border="true":::

1. 选择“**应用**”。 会显示多个应用。
1. 从右下角选择 **Upload自定义应用**。

      :::image type="content" source="Media/uploadingcustomapp.png" alt-text="上传自定义应用":::
  
1. 从 **“打开** ”对话框中选择应用包。
1. 选择 **“打开”**。

      :::image type="content" source="Media/selectapppackage.png" alt-text="选择应用包"lightbox="Media/selectapppackage.png"border="true":::

1. 从应用详细信息弹出窗口中选择 **“添加** ”，将机器人添加到所选团队。

      :::image type="content" source="Media/addingbot.png" alt-text="添加机器人"lightbox="Media/addingbot.png"border="true":::

1. 选择一个通道，并在通道中为机器人输入一条消息。

    机器人在未@mentioned的情况下接收消息。

      :::image type="content" source="Media/botreceivingmessage.png" alt-text="机器人接收消息"lightbox="Media/botreceivingmessage.png"border="true":::

## <a name="code-snippets"></a>代码段

以下代码提供了 RSC 权限的示例：

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

// Handle when a message is addressed to the bot. 
// When rsc is enabled the method will be called even when bot is addressed without being @mentioned
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text("Using RSC the bot can recieve messages across channels in team without being @mentioned."));
}
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

// Handle when a message is addressed to the bot. 
// When rsc is enabled the method will be called even when bot is addressed without being @mentioned
this.onMessage(async (context, next) => {
   await context.sendActivity(MessageFactory.text("Using RSC the bot can recieve messages across channles in team without being @mentioned."))
   await next();
});
```

---

## <a name="code-sample"></a>代码示例

| 示例名称 | Description | C# |Node.js|
|-------------|-------------|------|----|
|具有 RSC 权限的通道消息| Microsoft Teams示例应用演示机器人如何通过 RSC 接收所有通道消息，而无需@mentioned。| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/nodejs) |

## <a name="see-also"></a>另请参阅

* [智能机器人对话](/microsoftteams/platform/bots/how-to/conversations/conversation-basics)
* [特定于资源的同意](/microsoftteams/resource-specific-consent)
* [测试特定于资源的同意](/microsoftteams/platform/graph-api/rsc/test-resource-specific-consent)
* [Upload Teams中的自定义应用](~/concepts/deploy-and-publish/apps-upload.md)
