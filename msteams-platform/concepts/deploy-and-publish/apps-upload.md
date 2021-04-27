---
title: 上传自定义应用
description: 介绍如何在 Microsoft Teams 中上传应用
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
keywords: teams 应用上传
ms.openlocfilehash: 3fa6a3ef00cbb55b5c663891deaabcc908de95d5
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020805"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a>将一个应用程序包上传到 Microsoft Teams

若要在 Microsoft Teams 中测试应用体验，需要将应用上传到 Teams。 上载会将应用添加到所选团队，所有团队成员都可以像最终用户一样与其交互。

> [!NOTE]
> 通过对话窗口查看时，使用自动程序上传现有应用的已更新程序包可能不会显示选项卡更改。 可以通过应用飞出或在干净环境中进行测试来访问应用。

## <a name="create-your-upload-package"></a>创建上传包

对于开发和 AppSource 提交，必须创建可上传的程序包。 程序包必须包含描述你体验的信息。 该包是一个 .zip 文件，其中包含唯一定义体验的应用程序清单和图标。

若要创建上传程序包，请参阅 [为 Microsoft Teams 应用创建程序包](../build-and-test/apps-package.md)。

创建包后，将其上传到团队。 上载的程序包仅对所选团队的用户可用。

## <a name="load-your-package-into-teams"></a>将程序包加载到 Teams 中

可以通过将程序包上传到 Teams 来测试它。

> [!NOTE]
> 若要上传工作，租户管理员必须先 [启用应用上传](/microsoftteams/admin-settings)。

有两种方法将应用上传到 Teams：

* 使用应用商店
* 使用"应用"选项卡

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a>使用应用商店将程序包上传到团队或对话

1. 在 Teams 的左下角，选择 **"应用商店"** 图标。 在应用商店页面上，选择 **上传自定义应用**。

  ![查看团队](../../assets/images/store-upload-a-custom-app2.png)

2. 在 **"打开** "对话框中，导航到要上载的程序包，然后选择"打开"。

   ![添加菜单](../../assets/images/NewappAddmenudropdown.png)

上载的程序包必须可用于在同意对话框中指定的团队或对话中。 如果应用未显示，最常见的原因是清单中的错误，尤其是应用、机器人和消息扩展的 ID。 如果应用未针对对话进行范围限制，则不显示该选项。

>[!NOTE]
> 对话中的应用当前位于 [开发者预览版](../../resources/dev-preview/developer-preview-intro.md)中，如果 Teams 未以该模式运行，则不显示此选项。

![上传的机器人列表中的自动程序示例](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a>使用"应用"选项卡将程序包上传到团队

1. 在目标团队中，选择 **" (&#8943;) "** 管理团队 **"。**

   > [!NOTE]
   > 你必须是团队所有者，或者所有者必须授予用户访问权限，以添加相应的应用类型，此功能显示。

2. 选择" **应用"** 选项卡，然后选择右下角 **的** "上载自定义应用"。

   ![上载入口点](../../assets/images/UploadACustomApp.png)

3. Select your .zip package from the computer.

4. 可以在列表中看到已上传的应用。

   ![上传的机器人列表中的自动程序示例](../../assets/images/botinlist.jpg)

如果你的应用未加载，最常见的原因是清单中的错误，尤其是应用、机器人和消息扩展的 ID。

## <a name="access-your-uploaded-configurable-tab"></a>访问上传的可配置选项卡

如果应用包含选项卡，用户可以使用标准选项卡库流将其固定到任何对话或团队频道：

1. 转到团队中的频道。 选择 **+** 将选项卡添加到现有选项卡的右侧。

2. 从出现的库中选择您的选项卡。

3. 接受同意提示。

4. 通过配置页面配置 [您的选项卡，然后选择](../../tabs/how-to/create-tab-pages/configuration-page.md)"保存 **"。**

  !["添加选项卡"对话框，包含可用选项卡的库](../../assets/images/tab_gallery.png)

## <a name="access-your-uploaded-bot"></a>访问上传的机器人

将机器人添加到团队后，该团队的任何人都可以在团队频道内外使用，具体取决于机器人范围定义。 所有团队成员都可以在常规频道中查看一个帖子，指示机器人已添加到团队。

对于 Teams 自动程序，你可以首先调用@mentioning自动程序的名称。

若要测试与机器人的直接聊天，可以通过应用主页访问它，@mention频道中，或在"新建聊天"窗口中 **搜索** 它。

你可以@mention聊天机器人，或在"新建聊天"窗口中搜索它以测试与机器人的直接聊天。

## <a name="access-your-uploaded-connector"></a>访问上传的连接器

在团队或对话中加载应用后，用户可以使用标准连接器库流设置连接器：

1. 转到团队中的频道。 Choose **More options (** *&#8943;*) and choose **Connectors**.

2. 从底部的旁 **加载部分选择** 连接器。

3. 通过配置页面配置 [连接器，然后选择](../../webhooks-and-connectors/how-to/connectors-creating.md)"保存 **"。**

  !["添加选项卡"对话框，包含可用选项卡的库。](../../assets/images/connector_gallery.png)

## <a name="access-your-uploaded-messaging-extension"></a>访问上传的消息扩展

具有邮件扩展名的已上传应用会自动显示在撰写框的" (&#8943;) "菜单中。

![消息扩展](../../assets/images/compose-extensions/cesampleapp.png)


## <a name="remove-or-update-your-app"></a>删除或更新应用

若要删除应用，请在"查看 **Teams** 机器人"列表中选择应用名称旁边的删除图标。 如果你更改清单信息，首先删除应用，然后添加更新的程序包，请参阅 [将程序包加载到团队](#load-your-package-into-teams)。 服务上的代码更改不需要您再次上载清单。 但是，如果代码更改需要清单更新（例如 URL 的更改或自动程序 Microsoft 应用 ID 的更改），则必须再次上载清单。

> [!NOTE]
> 无法从个人上下文中完全删除自动程序。 如果删除并再次添加自动程序，则与自动程序的其他通信将附加到上一个对话中。

## <a name="troubleshooting-notes"></a>疑难解答说明

如果清单无法加载，请检查是否按照创建程序包中的说明操作，并针对[](../../concepts/build-and-test/apps-package.md)架构验证[清单](../../resources/schema/manifest-schema.md)。
