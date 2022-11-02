---
title: 创建选项卡删除页
author: surbhigupta
description: 了解如何在安装后重新配置选项卡。 通过支持 Microsoft Teams 应用中的删除和修改选项来扩展用户体验。
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 423cc386ca416fe116eb0bcb62c1238cae5547ff
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2022
ms.locfileid: "68819938"
---
# <a name="create-a-removal-page"></a>创建删除页面

可以通过在应用中支持删除和修改选项来扩展和增强用户体验。 Teams 使用户能够重命名或删除频道或群组选项卡，并且你可以允许用户在安装后重新配置选项卡。 此外，选项卡删除体验为用户提供了删除后选项以删除或存档内容。

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>使选项卡可在安装后重新配置

`manifest.json` 定义选项卡的特性和功能。 选项卡实例 `canUpdateConfiguration` 属性采用布尔值，该值指示用户是否可以在创建选项卡后修改或重新配置选项卡。 下表提供了属性详细信息：

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`canUpdateConfiguration`|Boolean|||一个值，该值指示创建后用户是否可以更新选项卡配置的实例。 默认值为“`true`”。 |

将选项卡上传到频道或群组聊天时，Teams 会为选项卡添加右键单击下拉菜单。可用选项由 `canUpdateConfiguration` 设置确定。 下表提供了设置详细信息：

| `canUpdateConfiguration`| true   | false | 说明 |
| ----------------------- | :----: | ----- | ----------- |
|     设置            |   √    |       |页面 `configurationUrl` 在 iFrame 中重新加载，允许用户重新配置选项卡。 |
|     重命名              |   √    |   √   | 用户可以更改选项卡名称，因为它显示在选项卡栏中。          |
|     删除              |   √    |   √   |  `removeURL`如果属性和值包含在 **配置页** 中，则 **删除页** 将加载到 iFrame 中并显示给用户。 如果未包含删除页，则会向用户显示确认对话框。          |

## <a name="create-a-tab-removal-page-for-your-application"></a>为应用程序创建选项卡删除页

可选删除页是你托管的 HTML 页面，在删除选项卡时显示。 删除页面 URL 由 `setConfig()` 配置页中的 (或 `setSettings()` TeamsJS v.2.0.0 之前的方法指定，) 。 与应用中的所有页面一样，删除页必须符合 [Teams 选项卡先决条件](../../../tabs/how-to/tab-requirements.md)。

### <a name="register-a-remove-handler"></a>注册删除处理程序

（可选）在删除页逻辑中，可以在用户删除现有选项卡配置时调用 `registerOnRemoveHandler((RemoveEvent) => {}` 事件处理程序。 当用户尝试删除内容时，该方法将采用 [`RemoveEvent`](/javascript/api/@microsoft/teams-js/pages.config.removeevent?view=msteams-client-js-latest&preserve-view=true) 接口，并在处理程序中执行代码。 方法用于执行清理操作，例如删除为选项卡内容提供支持的基础资源。 一次只能注册一个删除处理程序。

`RemoveEvent` 接口用两种方法描述对象：

* `notifySuccess()` 函数是必需的。 它指示基础资源删除成功，并且可以删除其内容。

* `notifyFailure(string)` 函数是可选的。 它指示删除基础资源失败，并且无法删除其内容。 可选字符串参数指定失败的原因。 如果提供，则会向用户显示此字符串；否则会显示一般性错误。

#### <a name="use-the-getconfig-function"></a>使用 `getConfig()` 函数

可以使用 `getConfig()` 以前 `getSettings()`)  (来分配要删除的选项卡内容。 函数 `getConfig()` 返回一个 promise，该承诺使用 Config 对象进行解析，并提供可检索的有效设置属性值。

#### <a name="use-the-getcontext-function"></a>使用 `getContext()` 函数

可以使用 `getContext()` 获取运行帧的当前上下文。 函数 `getContext()` 返回一个承诺，该承诺将使用 Context 对象解析。 Context 对象提供可在删除页逻辑中使用的有效 `Context` 属性值，以确定要显示在删除页中的内容。

#### <a name="include-authentication"></a>包括身份验证

在允许用户删除选项卡内容之前，需要进行身份验证。 上下文信息可用于帮助构造身份验证请求和授权页面 URL。 请参阅[选项卡的 Microsoft Teams 身份验证流程](~/tabs/how-to/authentication/auth-flow-tab.md)。 确保选项卡页中使用的所有域都列在应用清单的数组中 `validDomains` 。

下面是一个示例选项卡删除代码块：

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```html
<body>
  <button onclick="onClick()">Delete this tab and all underlying data?</button>
  <script>
    await microsoftTeams.app.initialize();
    pages.config.registerOnRemoveHandler((removeEvent) => {
      // Here you can designate the tab content to be removed and/or archived.
        const configPromise = pages.getConfig();
        configPromise.
            then((configuration) => {
                configuration.contentUrl = "...";
                removeEvent.notifySuccess()}).
            catch((error) => {removeEvent.notifyFailure("failure message")});
    });

    const onClick() => {
        pages.config.setValidityState(true);
    }
  </script>
</body>
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

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

***

当用户从选项卡的下拉菜单中选择“**删除”** 时，Teams 会将 **配置页** 中分配的可选`removeUrl`页面加载到 iFrame 中。 向用户显示一个加载了函数的 `onClick()` 按钮，该函数调用 `pages.config.setValidityState(true)` 并启用删除页面 iFrame 底部显示的“ **删除** ”按钮。

执行删除处理程序后，`removeEvent.notifySuccess()` 或 `removeEvent.notifyFailure()` 将通知 Teams 内容删除结果。

>[!NOTE]
>
> * 为了确保授权用户对选项卡的控制不遭禁止，Teams 在成功和失败情况下都会删除选项卡。
> * 调用 `registerOnRemoveHandler` 事件处理程序后，将有 15 秒的时间响应该方法。 默认情况下，即使你不调用 `setValidityState(true)`，Teams 也会在五秒后启用“**删除**”按钮。
> * 当用户选择“**删除**”时，无论操作是否已完成，Teams 都会在 30 秒后删除该选项卡。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [移动设备上的选项卡](~/tabs/design/tabs-mobile.md)

## <a name="see-also"></a>另请参阅

* [Teams 的生成选项卡](../../what-are-tabs.md)
* [Teams 的应用清单架构](../../../resources/schema/manifest-schema.md)
* [RemoveEvent 接口](/javascript/api/@microsoft/teams-js/pages.config.removeevent)
* [获取选项卡的上下文](../access-teams-context.md)
* [创建个人选项卡](../create-personal-tab.md)
* [创建频道选项卡或组选项卡](../create-channel-group-tab.md)
