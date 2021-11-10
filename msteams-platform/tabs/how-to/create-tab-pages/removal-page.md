---
title: 创建选项卡删除页
author: surbhigupta
description: 如何创建选项卡删除页
keywords: teams 选项卡组频道可配置删除删除
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: a94578a065d1514d74d33638485be26b27c77718
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889235"
---
# <a name="create-a-removal-page"></a>创建删除页面

可以通过在应用中支持删除和修改选项来扩展和增强用户体验。 Teams用户可以重命名或删除频道或组选项卡，并且你可以允许用户在安装后重新配置选项卡。 此外，选项卡删除体验为用户提供删除后选项，以删除或存档内容。

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>启用选项卡以在安装后重新配置

**manifest.json** 定义选项卡的特性和功能。 选项卡实例属性采用一个布尔值，该值指示用户是否可以在选项卡创建后修改或 `canUpdateConfiguration` 重新配置它。 下表提供了属性详细信息：

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`canUpdateConfiguration`|Boolean|||一个值，指示用户创建后是否可以更新选项卡配置的实例。 默认值为 `true`。 |

将选项卡上载到频道或群聊时，Teams为选项卡添加右键单击下拉菜单。可用选项由设置 `canUpdateConfiguration` 决定。 下表提供了设置详细信息：

| `canUpdateConfiguration`| true   | false | 说明 |
| ----------------------- | :----: | ----- | ----------- |
|     设置            |   √    |       |页面 `configurationUrl` 在 IFrame 中重新加载，允许用户重新配置选项卡。 |
|     重命名              |   √    |   √   | 用户可以更改选项卡名称，因为它显示在选项卡栏中。          |
|     删除              |   √    |   √   |  如果  `removeURL` 属性和值包含在配置 **页中，** 则删除 **页面** 将加载到 IFrame 中，并呈现给用户。 如果未包含删除页，则向用户显示一个确认对话框。          |

## <a name="create-a-tab-removal-page-for-your-application"></a>为应用程序创建选项卡删除页

可选删除页是一个您托管的 HTML 页，在删除选项卡时将显示该页。 删除页面 URL 由配置页 `setSettings()` 中的 方法指定。 与应用内的所有页面一样，删除页面必须符合Teams[先决条件](../../../tabs/how-to/tab-requirements.md)。

### <a name="register-a-remove-handler"></a>注册删除处理程序

（可选）在删除页面逻辑中，您可以在用户删除现有选项卡配置时 `registerOnRemoveHandler((RemoveEvent) => {}` 调用事件处理程序。 当用户尝试删除内容时，该方法将接受 接口并执行 [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) 处理程序中的代码。 方法用于执行清理操作，例如删除支持选项卡内容的基础资源。 一次只能注册一个删除处理程序。

该 `RemoveEvent` 接口使用两种方法描述对象：

* `notifySuccess()`此函数是必需的。 它表示已成功删除基础资源，并且可删除其内容。

* 函数 `notifyFailure(string)` 是可选的。 它指示删除基础资源失败，并且无法删除其内容。 可选字符串参数指定失败的原因。 如果提供，则向用户显示此字符串;否则将显示一个常规错误。

#### <a name="use-the-getsettings-function"></a>使用 `getSettings()` 函数

可以使用 分配 `getSettings()` 要删除的选项卡内容。 `getSettings((Settings) =>{})`函数接受 [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) 并提供可以检索的有效 settings 属性值。

#### <a name="use-the-getcontext-function"></a>使用 `getContext()` 函数

可以使用 `getContext()` 获取正在运行帧的当前上下文。 `getContext((Context) =>{})`函数接受 [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) 。 函数提供可在删除页面逻辑中用于确定要显示在删除 `Context` 页中的内容的有效属性值。

#### <a name="include-authentication"></a>包括身份验证

在允许用户删除选项卡内容之前，需要进行身份验证。 上下文信息可用于帮助构建身份验证请求和授权页面 URL。 请参阅[Microsoft Teams的身份验证流](~/tabs/how-to/authentication/auth-flow-tab.md)。 确保选项卡页中使用的所有域都列在 `manifest.json` `validDomains` 数组中。

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

当用户从选项卡的下拉菜单中选择"删除"时，Teams将配置页中分配的可选页面 `removeUrl` 加载至 IFrame 中。  向用户显示一个使用 函数加载的按钮，该按钮调用并启用删除页面 IFrame 底部显示的 `onClick()` `microsoftTeams.settings.setValidityState(true)` "删除"按钮。 

执行删除处理程序后， `removeEvent.notifySuccess()` 或 `removeEvent.notifyFailure()` 通知Teams删除结果。

>[!NOTE]
> * 为了确保授权用户对选项卡的控制不会受到约束，Teams成功和失败时删除选项卡。
> * Teams五秒钟后启用 **"** 删除"按钮，即使选项卡尚未调用 `setValidityState()` 。
> * 当用户选择 **"删除"** 时，Teams 30 秒后删除选项卡，而不管操作是否已完成。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [移动设备上的选项卡](~/tabs/design/tabs-mobile.md)

## <a name="see-also"></a>另请参阅

* [Teams选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建频道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)
* [创建配置页](~/tabs/how-to/create-tab-pages/configuration-page.md)
