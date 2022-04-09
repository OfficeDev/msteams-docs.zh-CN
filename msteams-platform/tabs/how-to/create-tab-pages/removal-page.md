---
title: 创建选项卡删除页
author: surbhigupta
description: 如何创建选项卡删除页
keywords: teams 选项卡组通道可配置删除
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: ea29959bf79b5e46e876f75570dcb437fa56888f
ms.sourcegitcommit: 61003a14e8a179e1268bbdbd9cf5e904c5259566
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2022
ms.locfileid: "64736864"
---
# <a name="create-a-removal-page"></a>创建删除页面

可以通过在应用中支持删除和修改选项来扩展和增强用户体验。 Teams使用户能够重命名或删除频道或组选项卡，并且你可以允许用户在安装后重新配置选项卡。 此外，选项卡删除体验为用户提供了删除后选项以删除或存档内容。

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>启用安装后重新配置选项卡

定义 `manifest.json` 选项卡的功能和功能。 Tab 实例 `canUpdateConfiguration` 属性采用一个布尔值，该值指示用户在创建选项卡后是否可以修改或重新配置该选项卡。 下表提供了属性详细信息：

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`canUpdateConfiguration`|Boolean|||一个值，该值指示创建后用户是否可以更新选项卡配置的实例。 默认值为“`true`”。 |

当选项卡上传到频道或群聊时，Teams为选项卡添加右键单击下拉菜单。可用选项由`canUpdateConfiguration`设置确定。 下表提供了设置详细信息：

| `canUpdateConfiguration`| true   | false | description |
| ----------------------- | :----: | ----- | ----------- |
|     设置            |   √    |       |页面 `configurationUrl` 在 IFrame 中重新加载，允许用户重新配置选项卡。 |
|     重命名              |   √    |   √   | 用户可以更改选项卡名称，因为它显示在选项卡栏中。          |
|     删除              |   √    |   √   |  `removeURL`如果属性和值包含在 **配置页** 中，**则删除页** 将加载到 IFrame 中并呈现给用户。 如果未包含删除页，则会向用户显示确认对话框。          |

## <a name="create-a-tab-removal-page-for-your-application"></a>为应用程序创建选项卡删除页

可选删除页是托管的 HTML 页面，在删除选项卡时显示。 删除页 URL 由 `setSettings()` 配置页中的方法指定。 与应用中的所有页面一样，删除页面必须符合[Teams选项卡先决条件](../../../tabs/how-to/tab-requirements.md)。

### <a name="register-a-remove-handler"></a>注册删除处理程序

（可选）在删除页逻辑中，当用户删除现有选项卡配置时，可以调用 `registerOnRemoveHandler((RemoveEvent) => {}` 事件处理程序。 当用户尝试删除内容时， [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) 该方法将传入接口并执行处理程序中的代码。 该方法用于执行清理操作，例如删除为选项卡内容提供电源的基础资源。 一次只能注册一个删除处理程序。

该 `RemoveEvent` 接口描述具有两种方法的对象：

* 函 `notifySuccess()` 数是必需的。 它指示基础资源的删除已成功，并且可以删除其内容。

* 该 `notifyFailure(string)` 函数是可选的。 它指示删除基础资源失败，无法删除其内容。 可选字符串参数指定失败的原因。 如果提供此字符串，则会向用户显示此字符串;否则会显示泛型错误。

#### <a name="use-the-getsettings-function"></a>使用函数`getSettings()`

可以使用 `getSettings()`它来分配要删除的选项卡内容。 该 `getSettings((Settings) =>{})` 函数接受 [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) 并提供可检索的有效设置属性值。

#### <a name="use-the-getcontext-function"></a>使用函数`getContext()`

可以使用 `getContext()` 它来获取正在运行帧的当前上下文。 该`getContext((Context) =>{})`函数接受 .[`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) 该函数提供有效的 `Context` 属性值，你可以在删除页逻辑中使用这些值来确定要在删除页中显示的内容。

#### <a name="include-authentication"></a>包括身份验证

在允许用户删除选项卡内容之前，需要进行身份验证。 上下文信息可用于帮助构造身份验证请求和授权页 URL。 请参阅[选项卡Microsoft Teams身份验证流](~/tabs/how-to/authentication/auth-flow-tab.md)。 确保选项卡页中使用的所有域都列在数组中`manifest.json``validDomains`。

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

当用户从选项卡的下拉菜单中选择 **“删除**”时，Teams将 **配置页** 中分配的`removeUrl`可选页面加载到 IFrame 中。 用户将看到一个按钮，该按钮加载了 `onClick()` 调用 `microsoftTeams.settings.setValidityState(true)` 并启用删除页 IFrame 底部显示的 **“删除** ”按钮。

执行删除处理程序后，`removeEvent.notifySuccess()`或`removeEvent.notifyFailure()`通知Teams内容删除结果。

>[!NOTE]
>
> * 若要确保未禁止授权用户对选项卡的控制，Teams在成功和失败情况下删除该选项卡。
> * 调用 `registerOnRemoveHandler` 事件处理程序后，将有 15 秒的时间响应该方法。 默认情况下，Teams在五秒钟后启用 **“删除**”按钮，即使你未调用`setValidityState(true)`。
> * 当用户选择 **“删除**”时，Teams在 30 秒后删除该选项卡，而不考虑操作是否已完成。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [移动设备上的选项卡](~/tabs/design/tabs-mobile.md)

## <a name="see-also"></a>另请参阅

* [Teams选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建通道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)
* [创建配置页](~/tabs/how-to/create-tab-pages/configuration-page.md)
