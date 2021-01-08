---
title: 创建配置页
author: laujan
description: 如何创建配置页
keywords: teams 选项卡组频道可配置
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: c041c311245bb5bfc5e2655ef8d596b2839fdb70
ms.sourcegitcommit: d0e71ea63af2f67eba75ba283ec46cc7cdf87d75
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/24/2020
ms.locfileid: "49731963"
---
# <a name="create-a-configuration-page"></a>创建配置页

配置页面是一种特殊类型 [的内容](content-page.md) 页，允许用户配置 Teams 应用的一些方面。 通常，这些用作以下部分：

* 频道或群聊选项卡 - 配置页允许您从用户收集信息，并设置要 `contentUrl` 显示的内容页。
* [邮件扩展](~/messaging-extensions/what-are-messaging-extensions.md)
* [Office 365 连接器](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

## <a name="configuring-a-channel-or-group-chat-tab"></a>配置频道或群聊选项卡

配置页通知内容页应如何呈现。 您的应用程序必须引用 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) 并调用 `microsoft.initialize()` 。 此外，URL 必须是安全的 HTTPS 终结点，并且可从云中访问。 下面是一个配置页面示例。

```html
<head>
<script src='https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js'></script>
</head>
    <body>
        <button onclick="(document.getElementById('icon').src = '/images/iconGray.png'); colorClickGray()">Select Gray</button>
        <img id="icon" src="/images/teamsIcon.png" alt="icon" style="width:100px" />
        <button onclick="(document.getElementById('icon').src = '/images/iconRed.png'); colorClickRed()">Select Red</button>

        <script>
            microsoftTeams.initialize();
            let saveGray = () => {
                microsoftTeams.settings.registerOnSaveHandler((saveEvent) => {
                    microsoftTeams.settings.setSettings({
                        websiteUrl: "https://yourWebsite.com",
                        contentUrl: "https://yourWebsite.com/gray",
                        entityId: "grayIconTab",
                        suggestedDisplayName: "MyNewTab"
                    });
                    saveEvent.notifySuccess();
                });
            }
            let saveRed = () => {
                microsoftTeams.settings.registerOnSaveHandler((saveEvent) => {
                    microsoftTeams.settings.setSettings({
                        websiteUrl: "https://yourWebsite.com",
                        contentUrl: "https://yourWebsite.com/red",
                        entityId: "redIconTab",
                        suggestedDisplayName: "MyNewTab"
                    });
                    saveEvent.notifySuccess();
                });
            }

            let gr = document.getElementById("gray").style;
            let rd = document.getElementById("red").style;

            const colorClickGray = () => {
                gr.display = "block";
                rd.display = "none";
                microsoftTeams.settings.setValidityState(true);
                saveGray()
            }

            const colorClickRed = () => {
                rd.display = "block";
                gr.display = "none";
                microsoftTeams.settings.setValidityState(true);
                saveRed();
            }
        </script>
    </body>
...
```

用户在此处显示两个选项按钮，即"选择灰色"或"选择红色"，以使用红色或灰色图标显示选项卡内容。 选择相对按钮将触发 `saveGray()` `saveRed()` 或调用以下内容：

1. 设置为 `settings.setValidityState(true)` true。
1. `microsoftTeams.settings.registerOnSaveHandler()`触发事件处理程序。
1. 应用 **配置** 页面上的"保存"按钮（在 Teams 中上载）已启用。

此代码可让 Teams 知道已满足配置要求，并且可以继续安装。 在 **Save** 中，将按接口为当前实例 `settings.setSettings()` `Settings` 设置参数。 有关详细信息，请参阅"设置 ["界面](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true)。 最后 `saveEvent.notifySuccess()` ，调用它以指示内容 URL 已成功解析。

>[!NOTE]
>
>* 如果使用保存处理程序注册 `microsoftTeams.settings.registerOnSaveHandler()` ，则回调 `saveEvent.notifySuccess()` 必须调用或 `saveEvent.notifyFailure()` 指示配置的结果。
>* 如果未注册保存处理程序，则用户选择"保存"按钮 `saveEvent.notifySuccess()` 后，将立即 **进行** 调用。

### <a name="get-context-data-for-your-tab-settings"></a>获取选项卡设置的上下文数据

您的选项卡可能需要上下文信息来显示相关内容。 通过提供更加自定义的用户体验，上下文信息可以进一步增强选项卡的吸引力。

Teams [上下文接口](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) 定义可用于选项卡配置的属性。 可以通过两种方式收集上下文数据变量的值：

1. 在清单中插入 URL 查询字符串占位符 `configurationURL` 。

1. 使用 [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{}` 方法。

#### <a name="insert-placeholders-in-the-configurationurl"></a>在 `configurationURL`

上下文接口占位符可以添加到你的基本 `configurationUrl` 。 例如：

##### <a name="base-url"></a>基 URL

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a>包含查询字符串的基 URL

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

上传页面后，Teams 将用相关值更新查询字符串占位符。 可以在配置页中包括逻辑以检索和使用这些值。 有关使用 URL 查询字符串的信息，请参阅 MDN Web 文档中的 [URLSearchParams。](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) 下面是如何从上述属性中提取值 `configurationURL` 的示例：

```html
<script>
   microsoftTeams.initialize();
   const getId = () => {
        let urlParams = new URLSearchParams(document.location.search.substring(1));
        let blueTeamId = urlParams.get('team');
        return blueTeamId
    }
//For testing, you can invoke the following to view the pertinent value:
document.write(getId());
</script>
```

### <a name="use-the-getcontext-function-to-retrieve-context"></a>使用 `getContext()` 函数检索上下文

调用该函数 `microsoftTeams.getContext((context) => {})` 时，将检索 [上下文接口](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest&preserve-view=true)。 可以将此函数添加到配置页面以检索上下文值：

```html
<!-- `userPrincipalName` will render in the span with the id "user". -->

<span id="user"></span>
...
<script>
    microsoftTeams.getContext((context) =>{
        let userId = document.getElementById('user');
        userId.innerHTML = context.userPrincipalName;
    });
</script>
...
```

## <a name="context-and-authentication"></a>上下文和身份验证

在允许用户配置应用之前，可能需要进行身份验证，或者内容可能包括具有其自己的身份验证协议的源。 请参阅 ["在 Microsoft Teams 选项卡中](~/tabs/how-to/authentication/auth-flow-tab.md) 对用户进行身份验证"上下文信息可用于帮助构建身份验证请求和授权页面 URL。
确保选项卡页中使用的所有域都列在 `manifest.json` `validDomains` 数组中。

## <a name="modify-or-remove-a-tab"></a>修改或删除选项卡

支持的删除选项可以进一步优化用户体验。 您可以通过将清单的属性设置为来允许用户修改、重新配置或重命名组/频道 `canUpdateConfiguration` 选项卡 `true` 。  此外，你可以指定在删除选项卡时内容会发生什么情况，方法为在应用中包括删除选项页，并设置配置中的 (值 `removeUrl`  `setSettings()` ，) 。 个人选项卡不能修改，但用户可以卸载。 有关详细信息，请参阅 [为选项卡创建删除页](~/tabs/how-to/create-tab-pages/removal-page.md)。

## <a name="mobile-clients"></a>移动客户端

如果你选择让频道/组选项卡显示在 Teams 移动客户端上，则配置必须具有属性值， (`setSettings()` `websiteUrl` 请参阅下面的) 。 请参阅 [移动选项卡指南](~/tabs/design/tabs-mobile.md)。

用于删除页面和/ (移动客户端的 Microsoft Teams setSettings () 配置：

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "URL REQUIRED FOR MOBILE CLIENTS",
    removeUrl: "ADD REMOVAL PAGE URL HERE"
});
```
