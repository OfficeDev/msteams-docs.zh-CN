---
title: 使用 RSC 接收所有频道消息
author: surbhigupta12
description: 接收具有 RSC 权限的所有频道消息
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: ea247d7718b76f1e48bbb2c9839606dcb5cbab51
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155267"
---
# <a name="receive-all-channel-messages-with-rsc"></a>使用 RSC 接收所有频道消息

> [!NOTE]
> 此功能目前仅适用于公共 [开发人员预览](../../../resources/dev-preview/developer-preview-intro.md) 版。

RSC (权限) （最初针对 Teams Graph API 开发）的特定资源许可现在扩展到机器人方案。

目前，自动程序仅在收到用户频道消息时才能收到@mentioned。 使用 RSC，你现在可以请求团队所有者同意自动程序在团队中跨标准频道接收用户消息，而无需@mentioned。 此功能通过指定已启用 RSC 的应用清单中的权限Teams `ChannelMessage.Read.Group` 启用。 配置完成后，团队所有者可以在应用安装过程中授予同意。

有关为应用启用 RSC 的信息，请参阅 Teams 中的[资源特定许可](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest)。

## <a name="enable-bots-to-receive-all-channel-messages"></a>使机器人能够接收所有频道消息

`ChannelMessage.Read.Group`RSC 权限扩展到机器人。 征得用户同意后，此权限允许图形应用程序获取对话中的所有消息，并允许聊天机器人接收所有频道消息，而无需@mentioned。

## <a name="update-app-manifest"></a>更新应用清单

若要使机器人接收所有频道消息，必须在应用清单Teams属性中指定的权限配置 `ChannelMessage.Read.Group` `webApplicationInfo` RSC。

![更新应用清单](~/bots/how-to/conversations/Media/appmanifest.png)

以下是对象 `webApplicationInfo` 的示例：

* **id**：你的Azure Active Directory (AAD) 应用 ID。 它可以与自动程序 ID 相同。
* **resource**：任何字符串。 此字段在 RSC 中没有任何操作，但必须添加且具有值以避免错误响应。
* **applicationPermissions：** 必须指定应用的 RSC `ChannelMessage.Read.Group` 权限。 有关详细信息，请参阅特定于 [资源的权限](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions)。

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

## <a name="sideload-in-a-team-to-test"></a>在团队中旁加载以进行测试

若要在团队中旁加载以进行测试，是否收到具有 RSC 的团队中所有频道消息，而不@mentioned：

1. 选择或创建团队。
1. 从左窗格中选择 &#x25CF;&#x25CF;&#x25CF; 省略号。 将显示下拉菜单。
1. 从 **下拉菜单中选择** "管理团队"。 将显示详细信息。

   ![管理团队中的应用](~/bots/how-to/conversations/Media/managingteam.png)

1. 选择“**应用**”。 将显示多个应用。
1. 从 **Upload右下角选择** 自定义应用。

    ![上载自定义应用](~/bots/how-to/conversations/Media/uploadingcustomapp.png)

1. 从"打开"对话框中 **选择应用** 包。
1. 选择 **“打开”**。

    ![选择应用包](~/bots/how-to/conversations/Media/selectapppackage.png)

1. 从 **应用** 详细信息弹出窗口中选择添加，将机器人添加到所选团队。

    ![添加自动程序](~/bots/how-to/conversations/Media/addingbot.png)

1. 选择一个通道，在频道中为自动程序输入消息。

    自动程序在不接收邮件的情况下接收@mentioned。

    ![机器人接收消息](~/bots/how-to/conversations/Media/botreceivingmessage.png)

## <a name="code-sample"></a>代码示例

| 示例名称 | 说明 | C# |Node.js|
|-------------|-------------|------|----|
|具有 RSC 权限的频道消息| Microsoft Teams演示机器人如何使用 RSC 接收所有频道消息而不进行@mentioned。|  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/csharp) |    [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/nodejs) |

## <a name="see-also"></a>另请参阅

* [智能机器人对话](/microsoftteams/platform/bots/how-to/conversations/conversation-basics)
* [特定于资源的同意](/microsoftteams/resource-specific-consent)
* [测试特定于资源的同意](/microsoftteams/platform/graph-api/rsc/test-resource-specific-consent)
* [Upload自定义Teams](~/concepts/deploy-and-publish/apps-upload.md)
