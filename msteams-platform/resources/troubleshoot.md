---
title: 应用疑难解答
description: 解决生成 Microsoft Teams 应用时的问题或错误
keywords: teams 应用开发疑难解答
ms.topic: troubleshooting
ms.date: 07/09/2018
ms.openlocfilehash: a870a19eac9295f841b44b3b0364c46ffbc2d1d5
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696505"
---
# <a name="troubleshoot-your-microsoft-teams-app"></a>Microsoft Teams 应用疑难解答

## <a name="troubleshooting-tabs"></a>疑难解答选项卡

### <a name="accessing-the-devtools"></a>访问 DevTools

可以在 Teams 客户端中打开 [DevTools，](~/tabs/how-to/developer-tools.md) 获得与在 Windows) 上按 F12 (或在 MacOS (上的 Command-Option-I) 类似的体验。

### <a name="blank-tab-screen"></a>空白选项卡屏幕

如果在选项卡视图中看不到内容，可能是：

* 内容无法在 中显示 `<iframe>` 。
* 内容域不在清单 [的 validDomains](~/resources/schema/manifest-schema.md#validdomains) 列表中。

### <a name="the-save-button-isnt-enabled-on-the-settings-dialog"></a>"保存"按钮未在设置对话框中启用

请确保在用户输入或选择了设置页面上的所有必需数据后调用以 `microsoftTeams.settings.setValidityState(true)` 启用保存按钮。

### <a name="after-selecting-the-save-button-the-tab-settings-cannot-be-saved"></a>选择"保存"按钮后，无法保存选项卡设置

添加选项卡时，如果单击保存按钮，但显示一条指示无法保存设置的错误消息，则问题可能是两类问题之一：

* 从未收到保存成功消息。 如果保存处理程序是使用 注册 `microsoftTeams.settings.registerOnSaveHandler(handler)` 的，则回调必须调用 `saveEvent.notifySuccess()` 。 如果回调未在 30 秒内调用它或改为调用， `saveEvent.notifyFailure(reason)` 将显示此错误。

* 如果未注册任何保存处理程序，将在用户选择保存按钮时 `saveEvent.notifySuccess()` 立即自动进行调用。

* 提供的设置无效。 无法保存设置的另一个原因是，如果调用提供的设置对象无效，或者根本不会 `microsoftTeams.setSettings(settings)` 进行调用。 请参阅下一部分设置对象的常见问题。

### <a name="common-problems-with-the-settings-object"></a>设置对象的常见问题

* `settings.entityId` 缺少。 此字段属于必填字段。
* `settings.contentUrl` 缺少。 此字段属于必填字段。
* `settings.contentUrl` 或可选 `settings.removeUrl` ， 或 `settings.websiteUrl` 提供，但无效。 URL 必须使用 HTTPS，并且还必须是设置页的同一域或在清单列表中 `validDomains` 指定。

### <a name="cant-authenticate-the-user-or-display-your-auth-provider-in-your-tab"></a>无法对用户进行身份验证或在选项卡中显示身份验证提供程序

除非执行无提示身份验证，否则必须遵循 [Microsoft Teams JavaScript](/javascript/api/overview/msteams-client.md)客户端 SDK 提供的身份验证过程。

> [!NOTE]
>要求所有身份验证流在域上开始和结束，必须在清单中的 `validDomains` 对象中列出。

有关身份验证详细信息，请参阅验证 [用户](~/concepts/authentication/authentication.md)。

### <a name="static-tabs-not-showing-up"></a>未显示静态选项卡

存在一个已知问题，即从个人聊天对话访问应用时，使用新的或更新的静态选项卡更新现有自动程序应用时不会显示该选项卡更改。  To see the change， you should test on a new user or test instance， or access the bot from the Apps flyout.

## <a name="troubleshooting-bots"></a>自动程序疑难解答

### <a name="cant-add-my-bot"></a>无法添加我的机器人

应用必须由 Office 365 租户管理员启用，最终用户才能加载它们。 请注意，在某些情况下，Office 365 租户可能有多个与其关联的 SK，并且只有在所有 SK 中启用自动程序，机器人可以在任何 SK 中运行。 有关详细信息 [，请参阅准备 Office 365](~/concepts/build-and-test/prepare-your-o365-tenant.md) 租户。

### <a name="cant-add-bot-as-a-member-of-a-team"></a>无法将机器人添加为团队成员

必须先将聊天机器人上传到团队，然后才能在团队的任何频道中访问它。 有关 [此过程详细信息](~/concepts/deploy-and-publish/apps-upload.md) ，请查看在团队中上载应用。

### <a name="my-bot-doesnt-get-my-message-in-a-channel"></a>我的机器人不会在频道中收到我的消息

频道中的自动程序仅在显式@mentioned接收消息，即使您回复的是以前的自动程序消息。 在邮件中可能看不到自动程序名称的唯一例外是，如果自动程序由于最初发送的 `imBack` CardAction 而收到操作。

### <a name="my-bot-doesnt-understand-my-commands-when-in-a-channel"></a>在频道中时，我的机器人无法理解我的命令

由于频道中的机器人仅在收到@mentioned时接收消息，因此机器人在频道中接收的所有消息@mention文本字段中。 最佳做法是在传入的文本消息中分离自动程序名称本身，然后再传递到分析逻辑。 查看 [提及](../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions) ，获取有关如何处理此案例的提示。

## <a name="issues-with-packaging-and-uploading"></a>打包和上载问题

### <a name="error-while-reading-manifestjson"></a>在打开时manifest.js错误

大多数清单错误都提供特定字段缺失或无效的提示。 但是，如果 JSON 文件无法读取为 JSON，则使用这个常规错误消息。

清单读取错误的常见原因：

* 无效的 JSON。 使用 IDE（如 [Visual Studio Code](https://code.visualstudio.com) 或 [Visual Studio）](https://www.visualstudio.com/vs/) 自动验证 JSON 语法。
* 编码问题。 对 on 文件使用 UTF-8 *manifest.jsUTF-8。* 其他编码（特别是 BOM 编码）可能无法读取。
* 格式错误的 .zip 包。 on *manifest.js* 文件必须位于 .zip 文件的顶层。 请注意，默认 Mac 文件压缩可能会将manifest.js放在子目录中，这不会在 Microsoft Teams 中正确加载。

### <a name="another-extension-with-same-id-exists"></a>存在另一个 ID 相同的扩展

如果试图重新上传 ID 相同的更新程序包，请选择选项卡的表格行末尾的"替换"图标，而不是"**上传"** 按钮。

如果未重新上载更新的程序包，请确保 ID 是唯一的。
