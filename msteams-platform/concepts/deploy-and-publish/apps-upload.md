---
title: 上传自定义应用
description: 介绍如何在 Microsoft Teams 中上传应用
ms.topic: how-to
keywords: teams 应用上载
ms.openlocfilehash: 2e7a21dc27fdfe824ecacebabbb61a3b99ae8e79
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014339"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a>将一个应用程序包上传到 Microsoft Teams

若要在 Microsoft Teams 中测试应用体验，需要将应用上传到 Teams。 上载会将应用添加到你选择的团队，并且你和团队成员可以像最终用户一样与其交互。

> [!NOTE]
> 通过"对话"窗口查看时，使用自动程序为现有应用上载更新的程序包可能不会显示选项卡更改。 最好通过应用飞出来访问它，或在干净测试环境中进行测试。

## <a name="create-your-upload-package"></a>创建上传包

对于开发以及 AppSource (Office 应用商店) 提交，你必须创建一个可上传的程序包，其中包含描述你的体验的信息。 该包是一个 .zip 文件，其中包含唯一定义体验的应用程序清单和图标。

若要创建上传程序包，请参阅为 Microsoft Teams 应用 [创建程序包](../build-and-test/apps-package.md)。

创建程序包后，现在可以将其上载到团队中。 上载后，它将可供选定团队中的所有用户使用，并且仅可供该团队的用户使用。

## <a name="load-your-package-into-teams"></a>将程序包加载到 Teams 中

可以通过将程序包上传到 Teams 来测试它。

> [!NOTE]
> 若要上传工作，租户管理员必须先 [启用应用上载](/microsoftteams/admin-settings)。

有两种方法将应用上传到 Teams：

* 使用应用商店
* 使用"应用"选项卡

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a>使用应用商店将程序包上传到团队或对话

1. 在 Teams 的左下角，选择"应用商店"图标。 在"应用商店"页面上，选择"上载自定义应用"。

  ![查看团队](../../assets/images/store-upload-a-custom-app2.png)

2. 在 *"打开*"对话框中，导航到要上载的程序包，然后选择"*打开"。*

   ![添加菜单](../../assets/images/NewappAddmenudropdown.png)

上载的程序包现在应该可用于在同意对话框中指定的团队或对话中。 如果应用未显示，最常见的原因是清单中的错误，尤其是应用、机器人和消息扩展的 ID。 如果应用未针对对话进行范围设置，则不显示该选项。

>[!NOTE]
> 对话中的应用 [当前处于](../../resources/dev-preview/developer-preview-intro.md)开发者预览版，如果 Teams 未处于该模式下运行，则不显示此选项。

![上传的机器人列表中的自动程序示例](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a>使用"应用"选项卡将程序包上传到团队

1. 在目标团队中，选择 *" (&#8943;)* 选项，然后选择 *"管理团队"。*

   > [!NOTE]
   > 你必须是团队所有者，或者所有者必须允许用户添加相应的应用类型，此功能显示。

2. 选择"应用"选项卡，然后选择右下角 *的* "上载自定义应用"。

   ![上载入口点](../../assets/images/UploadACustomApp.png)

3. 浏览到计算机，然后从计算机中选择 .zip 程序包。

4. 短暂暂停后，你将在列表中看到已上传的应用。

   ![上传的机器人列表中的自动程序示例](../../assets/images/botinlist.jpg)

如果你的应用未加载，最常见的原因是清单中的错误，尤其是应用、机器人和消息扩展的 ID。

## <a name="accessing-your-uploaded-configurable-tab"></a>访问已上载的可配置选项卡

如果应用包含选项卡，用户可以使用标准选项卡库流将其固定到任何对话或团队频道：

1. 转到团队中的频道。 Choose *+* (Add a *tab*) ) to the right of the existing tabs.

2. 从出现的库中选择选项卡。

3. 接受同意提示。

4. 通过它的配置页面 [配置选项卡，](../../tabs/how-to/create-tab-pages/configuration-page.md)然后选择"*保存"。*

  !["添加选项卡"对话框，包含可用选项卡的库](../../assets/images/tab_gallery.png)

## <a name="accessing-your-uploaded-bot"></a>访问上传的机器人

向团队添加自动程序时，该团队中团队内外的任何人都可以使用自动程序，具体取决于自动程序范围定义。 你和其他团队成员将在常规频道中看到一个帖子，指示机器人已添加到团队。

对于支持团队的机器人，你可以首先调用自动程序@mentioning自动完成的名称。自动完成。

若要测试与机器人的直接聊天，可以通过应用主页访问它，@mention频道中，或在"新建聊天"窗口中 **搜索** 它。

将机器人添加到对话中以测试与自动程序的直接聊天时，@mention对话中，或在"新建聊天"窗口中 **搜索** 它。

## <a name="accessing-your-uploaded-connector"></a>访问已上载的连接器

在团队或对话中加载应用后，用户可以使用标准连接器库流设置连接器：

1. 转到团队中的频道。 选择 *"其他选项**(&#8943;)* 连接器 *"。*

2. 从底部的 **旁加载部分选择** 连接器。

3. 通过连接器的配置页面 [配置连接器，然后选择](../../webhooks-and-connectors/how-to/connectors-creating.md)"*保存"。*

  !["添加选项卡"对话框，包含可用选项卡的库。](../../assets/images/connector_gallery.png)

## <a name="accessing-your-uploaded-messaging-extension"></a>访问上传的消息扩展

具有邮件扩展名的已上载应用会自动显示在撰写框中的" (&#8943;) "菜单中的"更多选项"中。

![消息扩展](../../assets/images/compose-extensions/cesampleapp.png)

## <a name="removing-or-updating-your-app"></a>删除或更新应用

如果要删除应用，请在"查看 Teams 机器人"列表中选择应用名称旁边的回收站图标。

如果更改清单信息，必须先删除应用，然后根据"将程序包加载到团队 (添加更新的程序包) 。 [](#load-your-package-into-teams) 请注意，一般情况下，服务的代码更改不需要您重新上载清单，除非这些更改需要清单更新 (例如，更改其自动程序应用的 URL 或 Microsoft 应用 ID) 。

> [!NOTE]
> 无法从个人上下文中完全删除自动程序。 如果删除并重新添加自动程序，则与自动程序的其他通信将附加到上一个对话中。

## <a name="troubleshooting-notes"></a>疑难解答说明

* 如果清单未加载，请仔细检查您是否遵循了"创建程序包"中的所有说明，并[](../../concepts/build-and-test/apps-package.md)针对架构验证[了清单](../../resources/schema/manifest-schema.md)。
