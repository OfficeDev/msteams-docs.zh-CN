---
title: 创建选项卡删除页
author: laujan
description: 如何创建选项卡删除页
keywords: teams 选项卡组频道可配置删除删除
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 8f01780dce9aa0450169d4c699471bb2ac5bd9a0
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019585"
---
# <a name="modify-or-remove-a-channel-group-tab"></a>修改或删除频道组选项卡

可以通过在应用中支持删除和修改选项来扩展和增强用户体验。 Teams用户可以重命名或删除频道/组选项卡，并且你可以允许用户在安装后重新配置选项卡。 此外，选项卡删除体验可能包括指定在删除选项卡时对内容会发生什么情况，或者为用户提供删除后选项（如删除或存档内容）。

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>启用选项卡以在安装后重新配置

你的 **manifest.js** 定义选项卡的特性和功能。 选项卡实例属性采用一个布尔值，该值指示用户是否可以在选项卡创建后修改 `canUpdateConfiguration` 或重新配置它：

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`canUpdateConfiguration`|Boolean|||一个值，指示用户创建后是否可以更新选项卡配置的实例。 默认值： `true`|

将选项卡上载到频道或群聊时，Teams为选项卡添加右键单击下拉菜单。可用选项由以下设置 `canUpdateConfiguration` 决定：

| `canUpdateConfiguration`| true   | false | 说明 |
| ----------------------- | :----: | ----- | ----------- |
|     设置            |   √    |       |页面 `configurationUrl` 在 IFrame 中重新加载，允许用户重新配置选项卡。  |
|     重命名              |   √    |   √   | 用户可以更改选项卡名称，因为它显示在选项卡栏中。          |
|     删除              |   √    |   √   |  如果  `removeURL` 属性和值包含在配置 **页中，** 则删除 **页面** 将加载到 IFrame 中，并呈现给用户。 如果未包含删除页，则向用户显示一个确认对话框。          |
|||||

## <a name="create-a-tab-removal-page-for-your-application"></a>为应用程序创建选项卡删除页

可选删除页是一个您托管的 HTML 页，在删除选项卡时将显示该页。 删除页面 URL 由配置页 `setSettings()` 中的 方法指定。 与应用内的所有页面一样，删除页面必须符合Teams[要求](../../../tabs/how-to/tab-requirements.md)。

### <a name="register-a-remove-handler"></a>注册删除处理程序

（可选）在删除页面逻辑中，您可以在用户删除现有选项卡配置时 `registerOnRemoveHandler((RemoveEvent) => {}` 调用事件处理程序。 当用户尝试删除内容时，该方法将接受 接口并执行 [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) 处理程序中的代码。 它用于执行清理操作，例如删除支持选项卡内容的基础资源。 一次只能注册一个删除处理程序。

该 `RemoveEvent` 接口使用两种方法描述对象：

* `notifySuccess()`此函数是必需的。 它表示已成功删除基础资源，并且可删除其内容。

* 函数 `notifyFailure(string)` 是可选的。 它指示删除基础资源失败，并且无法删除其内容。 可选字符串参数指定失败的原因。 如果提供，则向用户显示此字符串;否则将显示一般性错误。

#### <a name="use-the-getsettings-function"></a>使用 `getSettings()` 函数

可以使用 指定 `getSettings()` 要删除的选项卡内容。 `getSettings((Settings) =>{})`函数接受 [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) 并提供可以检索的有效 settings 属性值。

#### <a name="use-the-getcontext-function"></a>使用 `getContext()` 函数

可以使用 `getContext()` 检索正在运行帧的当前上下文。 函数接受 并提供可在删除页面逻辑中用于确定要显示在删除页 `getContext((Context) =>{})` [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) 中的内容 `Context` 的有效属性值。

#### <a name="include-authentication"></a>包括身份验证

在允许用户删除选项卡内容之前，您可能需要进行身份验证。 上下文信息可用于帮助构建身份验证请求和授权页面 URL。 请参阅[Microsoft Teams的身份验证流](~/tabs/how-to/authentication/auth-flow-tab.md)。 确保选项卡页中使用的所有域都列在 `manifest.json` `validDomains` 数组中。

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

当用户从选项卡的下拉菜单中选择"删除"时，Teams将在配置 (中指定的可选页面) `removeUrl` IFrame 中。  此处，用户会使用函数加载按钮，该按钮调用并启用位于删除页面 IFrame 底部附近的"删除" `onClick()` `microsoftTeams.settings.setValidityState(true)` 按钮。 

执行删除处理程序后，或 `removeEvent.notifySuccess()` `removeEvent.notifyFailure()` 通知Teams删除结果。

>[!NOTE]
>为了确保授权用户对选项卡的控制不会受到阻止，Teams成功和失败时删除选项卡。\
>Teams 5 秒后启用 **"** 删除"按钮，即使选项卡未调用 `setValidityState()` 。\
>当用户选择 **"删除**"Teams 30 秒后删除选项卡，无论操作是否已完成。
