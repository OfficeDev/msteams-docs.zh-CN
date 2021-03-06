---
title: 上传自定义应用
description: 介绍如何在 Microsoft Teams 中上传应用
ms.topic: how-to
ms.author: lajanuar
keywords: teams 应用上传
ms.openlocfilehash: 3ca086cf8dbb992de84b22b7499f739d7c80b9d6
ms.sourcegitcommit: 9cfbc44912980a33d2d7c7c85739aeea6ccb41de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "50479878"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a>将一个应用程序包上传到 Microsoft Teams

若要在 Microsoft Teams 中测试应用体验，需要将应用上传到 Teams。 上载会将应用添加到所选团队，所有团队成员都可以像最终用户一样与其交互。

> [!NOTE]
> 通过对话窗口查看时，使用自动程序为现有应用上载更新的程序包可能不会显示选项卡更改。 可以通过应用飞出或在干净环境中进行测试来访问应用。

## <a name="create-your-upload-package"></a>创建上传包

对于开发和 AppSource 提交，必须创建可上传的程序包。 程序包必须包含描述体验的信息。 该包是一个 .zip 文件，其中包含唯一定义体验的应用程序清单和图标。

若要创建上传程序包，请参阅 [为 Microsoft Teams 应用创建程序包](../build-and-test/apps-package.md)。

创建包后，将其上载到团队中。 上载的程序包仅对所选团队的用户可用。

## <a name="load-your-package-into-teams"></a>将程序包加载到 Teams 中

可以通过将程序包上传到 Teams 来测试它。

> [!NOTE]
> 若要使上传正常工作，租户管理员必须先 [启用应用上载](/microsoftteams/admin-settings)。

有两种方法将应用上传到 Teams：

* 使用应用商店
* 使用"应用"选项卡

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a>使用应用商店将程序包上传到团队或对话

1. 在 Teams 的左下角，选择 **"应用商店"** 图标。 在"应用商店"页上，选择 **"上载自定义应用"。**

  ![查看团队](../../assets/images/store-upload-a-custom-app2.png)

2. 在 **"打开** "对话框中，导航到要上载的程序包，然后选择"打开"。

   ![添加菜单](../../assets/images/NewappAddmenudropdown.png)

上载的程序包必须可用于在同意对话框中指定的团队或对话中。 如果应用未显示，最常见的原因是清单中的错误，尤其是应用、机器人和消息扩展的 ID。 如果应用未针对不显示该选项的对话范围。

>[!NOTE]
> 对话中的应用当前 [处于开发者预览版，](../../resources/dev-preview/developer-preview-intro.md)如果 Teams 未处于该模式下运行，则不显示此选项。

![上传的自动程序列表中的自动程序示例](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a>使用"应用"选项卡将程序包上传到团队

1. 在目标团队中，选择 **" (&#8943;) "，** 然后选择"**管理团队"。**

   > [!NOTE]
   > 你必须是团队所有者，或者所有者必须授予用户访问权限，以添加相应的应用类型，以便显示此功能。

2. 选择 **"应用** "选项卡，然后选择 **右** 下角的"上载自定义应用"。

   ![上载入口点](../../assets/images/UploadACustomApp.png)

3. 从计算机中选择 .zip 程序包。

4. 可以在列表中看到已上传的应用。

   ![上传的自动程序列表中的自动程序示例](../../assets/images/botinlist.jpg)

如果你的应用未加载，最常见的原因是清单中的错误，尤其是应用、机器人和消息扩展的 ID。

## <a name="access-your-uploaded-configurable-tab"></a>访问上传的可配置选项卡

如果应用包含选项卡，用户可以使用标准选项卡库流将其固定到任何对话或团队频道：

1. 转到团队中的频道。 选择 **+** 将选项卡添加到现有选项卡的右侧。

2. 从出现的库中选择选项卡。

3. 接受同意提示。

4. 通过其配置页面配置 [选项卡，然后选择](../../tabs/how-to/create-tab-pages/configuration-page.md)"保存 **"。**

  !["添加选项卡"对话框，包含可用选项卡的库](../../assets/images/tab_gallery.png)

## <a name="access-your-uploaded-bot"></a>访问上传的机器人

将机器人添加到团队后，该团队中的任何人必须在团队频道内外使用自动程序，具体取决于自动程序范围定义。 所有团队成员都可以在常规频道中看到一个帖子，指出机器人已添加到团队。

对于 Teams 自动程序，你可以首先调用@mentioning自动程序的名称。

若要测试与机器人的直接聊天，可以通过应用主页访问它，@mention频道中访问它，或在"新建聊天"窗口中 **搜索** 它。

你可以@mention聊天机器人，或在"新建聊天"窗口中搜索它，以测试与机器人的直接聊天。

## <a name="access-your-uploaded-connector"></a>访问上载的连接器

在团队或对话中加载应用后，用户可以使用标准连接器库流设置连接器：

1. 转到团队中的频道。 选择 **更多选项***(&#8943;)***连接器。**

2. 从底部的旁 **加载部分选择** 连接器。

3. 通过配置页面配置 [连接器，然后选择](../../webhooks-and-connectors/how-to/connectors-creating.md)"保存 **"。**

  !["添加选项卡"对话框，包含可用选项卡的库。](../../assets/images/connector_gallery.png)

## <a name="access-your-uploaded-messaging-extension"></a>访问上传的消息扩展

具有邮件扩展名的已上载应用自动显示在撰写框中的" (&#8943;) "菜单中的"更多选项"中。

![消息扩展](../../assets/images/compose-extensions/cesampleapp.png)

## <a name="add-a-default-install-scope-and-group-capability"></a>添加默认安装范围和组功能

> [!NOTE]
> 默认安装范围和组功能目前仅在开发人员预览版中可用。

虽然在个人范围内安装应用适用于大多数应用，但 Teams 应用商店中的一些应用支持个人和团队范围。
其中一些应用适用于团队、会议或群聊，个人应用体验为辅助应用。
默认安装范围选择可帮助你为发布的 `defaultInstallScope` 应用指定。 应用安装体验使默认选项可供用户使用，而其余选项在 V 下面移动，如图像中突出显示。

![添加应用](../../assets/images/compose-extensions/addanapp.png)

该属性 `defaultInstallScope` 支持个人、团队、群聊或会议等值。

> [!NOTE]
>`defaultGroupCapability` 提供添加到团队、群聊或会议的默认功能。 选择选项卡、自动程序或连接器作为应用的默认功能，但必须确保在应用定义中提供了所选功能。

## <a name="remove-or-update-your-app"></a>删除或更新应用

若要删除应用，请在"查看 **Teams** 机器人"列表中选择应用名称旁边的删除图标。 如果更改清单信息，请首先删除应用，然后添加更新的程序包，请参阅"将[程序包加载到团队"。](#load-your-package-into-teams) 服务上的代码更改不需要再次上载清单。 但是，如果代码更改需要清单更新，例如 URL 或其自动程序 Microsoft 应用 ID 的更改，则必须再次上载清单。

> [!NOTE]
> 无法从个人上下文中完全删除自动程序。 如果删除并再次添加自动程序，则与自动程序的其他通信将附加到上一对话中。

## <a name="troubleshooting-notes"></a>疑难解答说明

如果清单无法加载，请检查您是否已按照"创建程序包"中的所有说明[](../../concepts/build-and-test/apps-package.md)操作，并针对架构验证[清单](../../resources/schema/manifest-schema.md)。
