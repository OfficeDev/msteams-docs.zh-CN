---
title: 对应用程序进行故障排除
description: 在为 Microsoft 团队构建应用程序时解决问题或出现的错误
keywords: 团队应用程序开发故障排除
ms.date: 07/09/2018
ms.openlocfilehash: f7fe42e7c1f3ff2c4d8d1cbe81ed8f71e6c04384
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673017"
---
# <a name="troubleshoot-your-microsoft-teams-app"></a>对 Microsoft 团队应用程序进行故障排除

## <a name="troubleshooting-tabs"></a>疑难解答选项卡

### <a name="accessing-the-devtools"></a>访问 DevTools

您可以在[团队客户端中打开 DevTools](~/tabs/how-to/developer-tools.md) ，使其类似于在浏览器中按 F12 （在 Windows 中）或命令-选项-I （在 MacOS 上）的类似体验。

### <a name="blank-tab-screen"></a>空白选项卡屏幕

如果您不在选项卡视图中看到您的内容，则可能是：

* 无法在中显示您的`<iframe>`内容。
* 内容域不在清单中的[validDomains](~/resources/schema/manifest-schema.md#validdomains)列表中。

### <a name="the-save-button-isnt-enabled-on-the-settings-dialog"></a>"设置" 对话框中未启用 "保存" 按钮

在用户输入或`microsoftTeams.settings.setValidityState(true)`选择 "设置" 页上的 "所有需要的数据" 以启用 "保存" 按钮时，请务必调用。

### <a name="after-selecting-the-save-button-the-tab-settings-cannot-be-saved"></a>选择 "保存" 按钮后，不能保存选项卡设置

添加选项卡时，如果单击 "保存" 按钮，但显示一条错误消息，指示无法保存设置，则问题可能是以下两类问题之一：

* 从未收到 "保存成功" 消息。 如果保存的处理程序是使用`microsoftTeams.settings.registerOnSaveHandler(handler)`注册的，则回调`saveEvent.notifySuccess()`必须调用。 如果回调在30秒`saveEvent.notifyFailure(reason)`内不调用此请求，则将显示此错误。

* 如果未注册保存处理程序，则`saveEvent.notifySuccess()`会在用户选择 "保存" 按钮后立即自动进行呼叫。

* 提供的设置无效。 可能不会保存设置的另一个原因是，调用`microsoftTeams.setSettings(settings)`提供了无效的设置对象，或者根本没有进行呼叫。 请参阅下一节常见的设置对象问题。

### <a name="common-problems-with-the-settings-object"></a>设置对象的常见问题

* `settings.entityId`缺失。 此字段属于必填字段。
* `settings.contentUrl`缺失。 此字段属于必填字段。
* `settings.contentUrl`或者是可选`settings.removeUrl`的， `settings.websiteUrl`或者已提供但无效。 Url 必须使用 HTTPS，并且也必须与设置页面的域相同，或在清单的`validDomains`列表中指定。

### <a name="cant-authenticate-the-user-or-display-your-auth-provider-in-your-tab"></a>无法对用户进行身份验证或在你的选项卡中显示你的身份验证提供程序

除非您正在进行无提示的身份验证，否则必须遵循[Microsoft 团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client.md)提供的身份验证过程。

> [!NOTE]
>我们需要所有身份验证流在你的域中开始和结束，这必须在你`validDomains`的清单中的对象中列出。

有关身份验证的详细信息，请参阅[对用户进行身份验证](~/concepts/authentication/authentication.md)。

### <a name="static-tabs-not-showing-up"></a>未显示静态选项卡

在使用新的或已更新的静态选项卡更新现有机器人应用程序时，将不会在从个人聊天对话中访问应用程序时显示该选项卡更改的已知问题。  若要查看更改，应在新用户或测试实例上进行测试，或从 "应用" 浮出控件中访问机器人。

## <a name="troubleshooting-bots"></a>故障排除机器人

### <a name="cant-add-my-bot"></a>无法添加我的机器人

若要由最终用户加载的应用程序必须由 Office 365 租户管理员启用。 请注意，在某些情况下，Office 365 租户可能会有多个与之关联的 Sku，并且要使用的 bot 必须在所有 Sku 中启用它们。 有关详细信息，请参阅[准备 Office 365 租户](~/concepts/build-and-test/prepare-your-o365-tenant.md)。

### <a name="cant-add-bot-as-a-member-of-a-team"></a>无法将 bot 添加为团队成员

必须先将 bot 上载到团队中，然后才能在该团队的任何频道中访问它。 有关此过程的详细信息，请参阅在[团队中上传您的应用程序](~/concepts/deploy-and-publish/apps-upload.md)。

### <a name="my-bot-doesnt-get-my-message-in-a-channel"></a>我的 bot 在频道中没有收到我的邮件

频道中的 bot 仅在明确 @mentioned 时才接收邮件，即使您要回复以前的 bot 邮件也是如此。 您可能不会在邮件中看到 bot 名称的唯一例外是，如果 bot 收到的`imBack`操作是它最初发送的 CardAction 的结果。

### <a name="my-bot-doesnt-understand-my-commands-when-in-a-channel"></a>在频道中时，我的 bot 不理解我的命令

由于通道中的 bot 仅在 @mentioned 时收到邮件，因此你的 bot 在通道中接收的所有邮件都包含该 @mention 在文本字段中。 最好将 bot 名称本身从所有传入的短信中去除，然后再传递给分析逻辑。 查看[提及](~/bots/how-to/conversations/channel-and-group-conversations.md#working-with--mentions)，了解有关如何处理这种情况的提示。

## <a name="issues-with-packaging-and-uploading"></a>打包和上传时出现问题

### <a name="error-while-reading-manifestjson"></a>读取清单 json 时出错

大多数清单错误将在特定字段缺失或无效时提供提示。 但是，如果 JSON 文件根本无法作为 JSON 读取，则使用此一般性错误消息。

清单读取错误的常见原因：

* JSON 无效。 使用可自动验证 JSON 语法的 IDE （如[Visual Studio Code](https://code.visualstudio.com)或[visual studio](https://www.visualstudio.com/vs/) ）。
* 编码问题。 对*清单 json*文件使用 utf-8。 其他编码（尤其是 BOM）可能不可读。
* Zip 包格式不正确。 *清单 json*文件必须位于 .zip 文件的顶层。 请注意，默认 Mac 文件压缩可能会将*清单 json*放在不能在 Microsoft 团队中正确加载的子目录中。

### <a name="another-extension-with-same-id-exists"></a>存在具有相同 ID 的另一个分机号

如果您尝试重新上载具有相同 ID 的更新的包，请选择该选项卡的表行结尾处的**替换**图标，而不是使用 "**上载**" 按钮。

如果不重新上载已更新的包，请确保该 ID 是唯一的。
