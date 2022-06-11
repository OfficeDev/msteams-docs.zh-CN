---
title: 排查应用问题
description: 排查为Microsoft Teams构建应用时出现的问题或错误
keywords: teams 应用开发故障排除
localization_priority: Normal
ms.topic: troubleshooting
ms.date: 07/09/2018
ms.openlocfilehash: 76a1a4d45757dff36d45c73f1ea5f2791fbe2e02
ms.sourcegitcommit: 12510f34b00bfdd0b0e92d35c8dbe6ea1f6f0be2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2022
ms.locfileid: "66032821"
---
# <a name="troubleshoot-your-microsoft-teams-app"></a>排查Microsoft Teams应用问题

## <a name="troubleshooting-tabs"></a>疑难解答选项卡

### <a name="accessing-the-devtools"></a>访问 DevTools

可以在[Teams客户端中打开 DevTools](~/tabs/how-to/developer-tools.md)，以获得与在浏览器中的 MacOS) 上的 Windows) 或 Command-Option-I (上按 F12 (类似的体验。

### <a name="blank-tab-screen"></a>空白选项卡屏幕

如果未在选项卡视图中看到内容，则可能是：

* 无法在 `<iframe>`其中显示内容。
* 内容域不在清单中的 [validDomains](~/resources/schema/manifest-schema.md#validdomains) 列表中。

### <a name="the-save-button-isnt-enabled-on-the-settings-dialog"></a>“设置”对话框上未启用“保存”按钮

用户在设置页上输入或选择所有必需数据以启用保存按钮后，请务必调用 `microsoftTeams.settings.setValidityState(true)` 。

### <a name="the-tab-settings-cant-be-saved-on-selecting-save"></a>选择“保存”时无法保存选项卡设置

添加选项卡时，如果选择 **“保存** ”但收到一条指示无法保存设置的错误消息，问题可能是以下两类问题之一：

* **保存成功消息从未收到**：如果使用 `microsoftTeams.settings.registerOnSaveHandler(handler)`保存处理程序注册，则必须调用 `saveEvent.notifySuccess()`回调。

  * 如果回调未在 30 秒内调用 `saveEvent.notifySuccess()` 或调用 `saveEvent.notifyFailure(reason)` ，则会显示此错误。
  * 如果未注册保存处理程序，则在 `saveEvent.notifySuccess()` 用户选择 **“保存**”时会自动进行调用。

* **提供的设置无效**：可能无法保存设置的另一个原因是调 `microsoftTeams.setSettings(settings)` 用提供的设置对象无效，或者根本没有进行调用。 请参阅下一部分：设置对象的常见问题。

### <a name="common-problems-with-the-settings-object"></a>设置对象的常见问题

* `settings.entityId` 缺少。 此字段属于必填字段。
* `settings.contentUrl` 缺少。 此字段属于必填字段。
* `settings.contentUrl` 或可选 `settings.removeUrl`，或 `settings.websiteUrl` 提供但无效。 URL 必须使用 HTTPS，并且必须与设置页相同或在清单列表 `validDomains` 中指定。

### <a name="cant-authenticate-the-user-or-display-your-auth-provider-in-your-tab"></a>无法对用户进行身份验证或在选项卡中显示身份验证提供程序

除非执行无提示身份验证，否则必须遵循 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 提供的身份验证过程。

> [!NOTE]
>我们需要在域上启动和结束所有身份验证流，该流必须在清单中的 `validDomains` 对象中列出。

有关身份验证的详细信息，请参阅 [对用户进行身份验证](~/concepts/authentication/authentication.md)。

### <a name="static-tabs-not-showing-up"></a>静态选项卡未显示

存在一个已知问题：使用新的或更新的静态选项卡更新现有机器人应用在从个人聊天聊天访问应用时不会显示该选项卡更改。  若要查看更改，应在新用户或测试实例上进行测试，或从“应用”浮出控件访问机器人。

## <a name="troubleshooting-bots"></a>机器人疑难解答

### <a name="cant-add-my-bot"></a>无法添加机器人

应用必须由Office 365租户管理员启用，才能由最终用户加载。 在某些情况下，Office 365租户可能具有多个与之关联的 SKU，机器人在任何情况下都可正常工作，必须在所有 SKU 中启用这些 SKU。 有关详细信息，请参阅[准备Office 365租户](~/concepts/build-and-test/prepare-your-o365-tenant.md)。

### <a name="cant-add-bot-as-a-member-of-a-team"></a>无法将机器人添加为团队成员

机器人必须先上传到团队，然后才能在该团队的任何频道中访问。 有关此过程的详细信息，请参阅 [在团队中上传应用](~/concepts/deploy-and-publish/apps-upload.md)。

### <a name="my-bot-doesnt-get-my-message-in-a-channel"></a>我的机器人不会在频道中收到我的消息

通道中的机器人仅在显式@mentioned时接收消息，即使你正在回复以前的机器人消息。 在邮件中可能看不到机器人名称的唯一例外是，如果机器人由于最初发送的 CardAction 而收到 `imBack` 操作。

### <a name="my-bot-doesnt-understand-my-commands-when-in-a-channel"></a>我的机器人在频道中时不了解我的命令

由于通道中的机器人仅在@mentioned时接收消息，因此机器人在通道中收到的所有消息都包括文本字段中@mention的消息。 最佳做法是在传递到分析逻辑之前，将机器人名称本身从所有传入的短信中剥离出来。 查看 [有关](../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions) 如何处理这种情况的提示。

## <a name="issues-with-packaging-and-uploading"></a>打包和上传问题

### <a name="error-while-reading-manifestjson"></a>读取 manifest.json 时出错

大多数清单错误将提示缺少或无效的特定字段。 但是，如果无法将 JSON 文件读取为 JSON，则会使用此泛型错误消息。

清单读取错误的常见原因：

* JSON 无效。 使用 IDE，例如[自动](https://code.visualstudio.com)验证 JSON 语法[的Visual Studio Code或Visual Studio](https://www.visualstudio.com/vs/)。
* 编码问题。 对 *manifest.json* 文件使用 UTF-8。 其他编码（特别是 BOM 编码）可能不可读。
* 格式不正确的.zip包。 *manifest.json* 文件必须位于.zip文件的顶层。 请注意，默认的 Mac 文件压缩可能会将 *manifest.json* 放置在子目录中，而子目录不会在Microsoft Teams中正确加载。

### <a name="another-extension-with-same-id-exists"></a>存在具有相同 ID 的另一个扩展

如果尝试再次上传具有相同 ID 的更新包，请选择选项卡表行末尾的 **“替换**”图标，而不是 **“Upload**”按钮。

如果不重新上传更新的包，请确保 ID 是唯一的。
