---
title: 创建选项卡删除页
author: laujan
description: 如何创建选项卡删除页
keywords: 团队选项卡组通道可配置删除删除
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 4ee060b8ef1f439ed4f8e4007e63606ce34c3d24
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964590"
---
# <a name="modify-or-remove-a-channel-group-tab"></a>修改或删除频道组选项卡

您可以通过在应用中支持删除和修改选项来扩展和增强用户体验。 通过团队，用户可以重命名或删除频道/组选项卡，还可以允许用户在安装后重新配置您的选项卡。 此外，您的选项卡删除体验可以包括在删除选项卡或授予用户删除内容（如删除或存档内容）时，指定内容会发生什么情况。

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>允许在安装后重新配置您的选项卡

您 ** 的manifest.js** 定义您的选项卡的特性和功能。 Tab 实例 `canUpdateConfiguration` 属性采用一个布尔值，该值指示用户是否可以在创建选项卡后修改或重新配置该选项卡：

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`canUpdateConfiguration`|Boolean|||一个值，指示是否可在用户创建之后更新该选项卡的配置实例。 设置 `true`|

将选项卡上载到频道或组聊天后，团队将为您的选项卡添加一个右键单击下拉菜单。可用选项由 `canUpdateConfiguration` 以下设置决定：

| `canUpdateConfiguration`| true   | false | description |
| ----------------------- | :----: | ----- | ----------- |
|     设置            |   √    |       |`configurationUrl`页面在 IFrame 中重新加载，以允许用户重新配置选项卡。  |
|     重命名              |   √    |   √   | 用户可以更改在选项卡栏中显示的选项卡名称。          |
|     删除              |   √    |   √   |  如果  `removeURL` 属性和值包含在 **配置页面**中，则 **删除页面** 会加载到 IFrame 中，并向用户显示。 如果不包含删除页面，则会向用户显示确认对话框。          |
|||||

## <a name="create-a-tab-removal-page-for-your-application"></a>为应用程序创建选项卡删除页

可选的 "删除" 页面是您承载的 HTML 页面，在删除该选项卡时会显示该页面。 删除页面 URL 由 `setSettings()` 配置页面中的方法指定。 与应用程序中的所有页面一样，删除页必须符合 [团队选项卡要求](~/tabs/how-to/add-tab.md)。

### <a name="register-a-remove-handler"></a>注册删除处理程序

（可选）在删除页面逻辑中，可以在 `registerOnRemoveHandler((RemoveEvent) => {}` 用户删除现有的选项卡配置时调用事件处理程序。 [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true)当用户尝试删除内容时，该方法将采用接口，并在处理程序中执行代码。 它用于执行清理操作，例如，删除用于为选项卡内容加电的基础资源。 一次只能注册一个删除处理程序。

该 `RemoveEvent` 接口描述了具有以下两种方法的对象：

* `notifySuccess()`函数是必需的。 它指示已成功删除基础资源，并且可以删除其内容。

* `notifyFailure(string)`函数是可选的。 它指示删除基础资源失败且无法删除其内容。 可选的字符串参数指定失败的原因。 如果提供，则向用户显示此字符串;否则，将显示一个一般性错误。

#### <a name="use-the-getsettings-function"></a>使用 `getSettings()` 函数

您可以使用 `getSettings()` 来指定要删除的选项卡内容。 `getSettings((Settings) =>{})`函数采用 [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) 并提供可检索的有效设置属性值。

#### <a name="use-the-getcontext-function"></a>使用 `getContext()` 函数

您可以使用 `getContext()` 来检索运行该帧的当前上下文。 `getContext((Context) =>{})`函数采用 [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) 并提供 `Context` 可在删除页面逻辑中使用的有效属性值，以确定要在删除页面中显示的内容。

#### <a name="include-authentication"></a>包括身份验证

您可能需要先进行身份验证，然后才能允许用户删除选项卡内容。 上下文信息可用于帮助构造身份验证请求和授权页面 Url。 请参阅 [Microsoft 团队身份验证流的选项卡](~/tabs/how-to/authentication/auth-flow-tab.md)。 确保在您的选项卡页中使用的所有域都列在 `manifest.json` `validDomains` 数组中。

以下是选项卡删除代码块示例：

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

当用户从选项卡的下拉菜单中选择 " **删除** " 时，团队会将 " `removeUrl` 配置" **页面** 中指定的可选页面 () 到 IFrame 中。 此时，将向用户提供一个加载的按钮，该按钮 `onClick()` 调用 `microsoftTeams.settings.setValidityState(true)` 并启用位于删除页面 IFrame 底部附近的 " **删除** " 按钮。

执行删除处理程序后， `removeEvent.notifySuccess()` 或 `removeEvent.notifyFailure()` 通知团队内容删除结果。

>[!NOTE]
>为了确保授权用户对选项卡的控制不被禁止，团队将删除成功和失败案例中的选项卡。
>即使您的选项卡未被调用，团队也会在5秒后启用 " **删除** " 按钮 `setValidityState()` 。
>当用户选择 " **删除** 团队" 时，将在30秒后删除该选项卡，而不管您的操作是否已完成。
