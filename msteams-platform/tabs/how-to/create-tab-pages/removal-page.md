---
title: 创建选项卡删除页
author: laujan
description: 如何创建选项卡删除页
keywords: teams 选项卡组频道可配置删除删除
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 49e2df47095999e9f9eea76ea341a44215bfacb3
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797881"
---
# <a name="modify-or-remove-a-channel-group-tab"></a>修改或删除频道组选项卡

可以通过在应用中支持删除和修改选项来扩展和增强用户体验。 Teams 允许用户重命名或删除频道/组选项卡，并且你可以允许用户在安装后重新配置选项卡。 此外，选项卡删除体验可能包括指定在删除选项卡时对内容会发生什么情况，或者为用户提供删除后选项（如删除或存档内容）。

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>启用在安装后重新配置选项卡

打开 **manifest.js** 定义选项卡的特性和功能。 选项卡实例属性采用一个布尔值，该值指示用户是否可以在选项卡创建后修改 `canUpdateConfiguration` 或重新配置它：

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`canUpdateConfiguration`|Boolean|||一个值，指示用户创建后是否可以更新选项卡配置的实例。 默认值： `true`|

将选项卡上传到频道或群聊后，Teams 会为选项卡添加右键单击下拉菜单。可用选项由以下设置 `canUpdateConfiguration` 决定：

| `canUpdateConfiguration`| true   | false | 说明 |
| ----------------------- | :----: | ----- | ----------- |
|     设置            |   √    |       |页面 `configurationUrl` 在 IFrame 中重新加载，允许用户重新配置选项卡。  |
|     重命名              |   √    |   √   | 用户可以更改选项卡名称，因为它显示在选项卡栏中。          |
|     删除              |   √    |   √   |  如果属性和值包含在配置页中，则删除页将加载到 `removeURL` IFrame 中，并呈现给用户。   如果未包含删除页，则向用户显示确认对话框。          |
|||||

## <a name="create-a-tab-removal-page-for-your-application"></a>为应用程序创建选项卡删除页

可选删除页是一个您托管的 HTML 页，在删除选项卡时会显示该页。 删除页面 URL 由配置 `setSettings()` 页中的方法指定。 与应用内的所有页面一样，删除页面必须符合 Teams [选项卡要求](../../../tabs/how-to/tab-requirements.md)。

### <a name="register-a-remove-handler"></a>注册删除处理程序

（可选）在删除页面逻辑中，可以在用户删除现有选项卡配置时 `registerOnRemoveHandler((RemoveEvent) => {}` 调用事件处理程序。 当用户尝试删除内容时，该方法将采用该接口并执行处理程序 [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) 中的代码。 它用于执行清理操作，例如删除支持选项卡内容的基础资源。 一次只能注册一个删除处理程序。

该 `RemoveEvent` 接口使用两种方法描述对象：

* `notifySuccess()`此函数是必需的。 它表示已成功删除基础资源，并可以删除其内容。

* 该 `notifyFailure(string)` 函数是可选的。 它指示删除基础资源失败，并且无法删除其内容。 可选字符串参数指定失败的原因。 如果提供，则向用户显示此字符串;否则将显示一个泛型错误。

#### <a name="use-the-getsettings-function"></a>使用 `getSettings()` 函数

可用于 `getSettings()` 指定要删除的选项卡内容。 `getSettings((Settings) =>{})`该函数接受 [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) 并提供可检索的有效设置属性值。

#### <a name="use-the-getcontext-function"></a>使用 `getContext()` 函数

可用于检索运行 `getContext()` 帧的当前上下文。 该函数接受并提供可在删除页面逻辑中用于确定要显示在删除页 `getContext((Context) =>{})` [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) 中的内容 `Context` 的有效属性值。

#### <a name="include-authentication"></a>包括身份验证

在允许用户删除选项卡内容之前，可能需要进行身份验证。 上下文信息可用于帮助构建身份验证请求和授权页面 URL。 请参阅 [选项卡的 Microsoft Teams 身份验证流](~/tabs/how-to/authentication/auth-flow-tab.md)。 确保选项卡页中使用的所有域都列在 `manifest.json` `validDomains` 数组中。

下面是一个示例选项卡删除代码块：

```html
<body>
  <button onclick="onClick()">Delete this tab and all underlying data?</button>
  <script>
    microsoftTeams.initialize();
    microsoftTeams.settings.registerOnRemoveHandler((removeEvent) => {
      // Here you can designate the tab content to be removed and/or archived.
        microsoftTeams.settings.getSettings((settings) => {
        settings.contentUrl = "..."
        });
        removeEvent.notifySuccess();
    });

    const onClick() => {
        microsoftTeams.settings.setValidityState(true);
    }
  </script>
</body>

```

当用户从选项卡的下拉菜单中选择"删除"时，Teams 将 (页面中指定的可选页面) `removeUrl` IFrame 中。  此处，向用户显示一个加载了函数的按钮，该按钮调用并启用位于删除页面 IFrame 底部附近的"删除" `onClick()` `microsoftTeams.settings.setValidityState(true)` 按钮。 

执行删除处理程序后， `removeEvent.notifySuccess()` 或 `removeEvent.notifyFailure()` 通知 Teams 内容删除结果。

>[!NOTE]
>为了确保授权用户对选项卡的控制不会受到抑制，Teams 将在成功和失败情况下删除该选项卡。
>Teams 在 5 **秒后** 启用"删除"按钮，即使你的选项卡尚未 `setValidityState()` 调用 。\
>当用户选择"删除 **Teams"** 时，将在 30 秒后删除选项卡，无论操作是否已完成。
