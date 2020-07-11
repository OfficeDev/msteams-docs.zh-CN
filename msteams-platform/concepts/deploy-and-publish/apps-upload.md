---
title: 在 Microsoft 团队中上传自定义应用程序
description: 介绍如何在 Microsoft 团队中上传您的应用程序
keywords: 团队应用上传
ms.openlocfilehash: c130ef48d3ad7476de9ca5afeb7b613197c43f18
ms.sourcegitcommit: 3ba5a5a7d9d9d906abc3ee1df9c2177de0cfd767
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2020
ms.locfileid: "45103024"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a>将一个应用程序包上传到 Microsoft Teams

若要在 Microsoft 团队中测试应用程序体验，您需要将您的应用程序上传到团队。 上载操作将向您选择的团队添加应用程序，你和你的团队成员可以与最终用户进行交互。

> [!NOTE]
> 使用 bot 上载现有应用程序的已更新包时，在通过对话窗口查看时，可能不会显示选项卡更改。 最好是通过应用程序飞出方式进行访问，也可以在干净的测试环境中进行测试。

## <a name="create-your-upload-package"></a>创建你的上载包

对于开发和 AppSource (以前的 Office 应用商店) 提交，您必须创建一个 uploadable 程序包，其中包含描述您的体验的信息。 该包（.zip 文件）包含应用程序清单和用于唯一定义您的体验的图标。

若要创建上载包，请参阅为[Microsoft 团队应用程序创建程序包](../build-and-test/apps-package.md)。

创建包后，即可将其上载到团队中。 上载后，将对所选团队中的所有用户和该团队的用户可用。

## <a name="load-your-package-into-teams"></a>将包加载到团队

您可以通过将您的程序包上载到团队来对其进行测试。

> [!NOTE]
> 若要上载工作，租户管理员必须首先[启用上载应用](/microsoftteams/admin-settings)。

有两种方法可将您的应用程序上载到团队：

* 使用 Store
* 使用 "应用" 选项卡

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a>使用 Microsoft Store 将你的程序包上载到团队或对话中

1. 在 "团队" 的左下角，选择 "存储" 图标。 在 "应用商店" 页上，选择 "上载自定义应用程序"。

   ![查看团队](../../assets/images/store-upload-a-custom-app.png)

2. 在 "*打开*" 对话框中，导航到要上载的包，然后选择 "*打开*"。

已上载的包现在应可在同意对话框中指定的团队或对话中使用。 如果未显示您的应用程序，最常见的原因是清单中的一个错误，尤其是应用程序、bot 和邮件扩展的 id。 如果应用程序的作用范围不适合对话，则不会显示该选项。

>[!NOTE]
> 对话中的应用程序当前处于[开发人员预览版](../../resources/dev-preview/developer-preview-intro.md)中，如果团队未在该模式下运行，则不会显示该选项。

![上载的 bot 列表中的 bot 的示例](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a>使用 "应用程序" 选项卡将您的包上传到团队

1. 在目标团队中，选择 "*更多选项*" (**&#8943;** ") "，然后选择 "*管理团队*"。

   > [!NOTE]
   > 您必须是团队所有者，或者所有者必须允许用户添加相应的应用程序类型，才能显示此功能。

2. 选择 "应用" 选项卡，然后选择右下方的 "*上传自定义应用程序*"。

   ![上载入口点](../../assets/images/UploadACustomApp.png)

3. 浏览到您的计算机上的 .zip 包并将其从计算机中选择。

4. 在短暂停顿之后，你将在列表中看到上传的应用。

   ![上载的 bot 列表中的 bot 的示例](../../assets/images/botinlist.jpg)

如果您的应用程序未加载，最常见的原因是清单中存在错误，尤其是应用程序、bot 和邮件扩展的 id。

## <a name="accessing-your-uploaded-configurable-tab"></a>访问上传的 "可配置" 选项卡

如果应用程序包含选项卡，则用户可以使用标准的选项卡库流将它们固定到任何对话或团队频道：

1. 转到团队中的频道。 选择 *+* (*将选项卡添加*) 在现有选项卡的右侧。

2. 从显示的库中选择您的选项卡。

3. 接受同意提示。

4. 通过[配置页面](../../tabs/how-to/create-tab-pages/configuration-page.md)配置您的选项卡，然后选择 "*保存*"。

  !["添加选项卡" 对话框，带有可用选项卡的库](../../assets/images/tab_gallery.png)

## <a name="accessing-your-uploaded-bot"></a>访问上载的 bot

当您向团队中添加机器人时，该团队的任何人都可以使用该团队中的任何人、团队频道内部和外部，具体取决于 bot 的作用域定义。 您和其他团队成员将在 "常规" 频道中看到一篇文章，表示已将该 bot 添加到团队。

对于已启用工作组的 bot，您可以通过 @mentioning bot 的名称（应自动完成）来开始调用你的 bot。

若要测试与你的 bot 的直接聊天，可以通过应用程序主页访问它，在频道中 @mention 它，也可以在**新聊天**窗口中搜索它。

将你的 bot 添加到对话以测试与你的 bot 的直接聊天时，可以在对话中 @mention 它，也可以在**新聊天**窗口中搜索它。

## <a name="accessing-your-uploaded-connector"></a>访问上载的连接器

在团队或对话中加载应用程序后，用户可以使用标准的 "连接器" 库流设置连接器：

1. 转到团队中的频道。 选择 "*更多选项*" (*&#8943;*) 然后选择 "*连接器*"。

2. 从底部的 "**旁加载**" 部分选择连接器。

3. 通过[配置页面](../../webhooks-and-connectors/how-to/connectors-creating.md)配置连接器，然后选择 "*保存*"。

  !["添加选项卡" 对话框，带有可用选项卡库。](../../assets/images/connector_gallery.png)

## <a name="accessing-your-uploaded-messaging-extension"></a>访问上载的邮件扩展插件

带有邮件扩展功能的已上载应用程序将自动显示在 "撰写" 框中 (*&#8943;*) "菜单中的"*更多选项*"中。

![消息传递扩展](../../assets/images/compose-extensions/cesampleapp.png)

## <a name="removing-or-updating-your-app"></a>删除或更新应用程序

如果要删除您的应用程序，请在 "查看团队 bot" 列表中选择应用程序名称旁边的 "垃圾桶" 图标。

如果更改了清单信息，则必须先删除该应用程序，然后将更新的包 (添加到团队) 中的每个[加载包中](#load-your-package-into-teams)。 请注意，通常情况下，您的服务上的代码更改不要求您重新上载清单，除非这些更改需要清单更新 (例如，对其 bot 的 URL 或 Microsoft app ID 的更改) 。

> [!NOTE]
> 无法从个人上下文中完全删除机器人。 如果卸载并重新添加了 bot，则与 bot 的其他通信将追加到之前的会话中。

## <a name="troubleshooting-notes"></a>疑难解答说明

* 如果未加载清单，请仔细检查是否遵循 "[创建包](../../concepts/build-and-test/apps-package.md)" 和 "根据[架构](../../resources/schema/manifest-schema.md)验证清单" 中的所有说明操作。

