---
title: 创建配置页
author: laujan
description: ''
keywords: 团队选项卡组频道可配置
ms.topic: conceptualF
ms.author: laujan
ms.openlocfilehash: 55fe1efca4defacf10b9be34f788704b7b4491f5
ms.sourcegitcommit: 1b909fb9ccf6cdd84ed0d8f9ea0463243a802a23
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "45434480"
---
# <a name="create-a-configuration-page"></a>创建配置页

配置页面是一种特殊类型的[内容页面](content-page.md)，允许您的用户配置团队应用程序的某些方面。 通常将它们用作以下部分：

* 频道或组聊天选项卡-"配置" 页允许您收集用户的信息，并设置 `contentUrl` 要显示的内容页。
* [邮件扩展](~/messaging-extensions/what-are-messaging-extensions.md)
* [Office 365 连接器](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

## <a name="configuring-a-channel-or-group-chat-tab"></a>配置频道或组聊天选项卡

配置页面通知内容页面它应如何呈现。 您的应用程序必须引用[Microsoft 团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest)和调用 `microsoft.initialize()` 。 此外，您的 Url 必须是安全的 HTTPS 终结点，并可从云中使用。 下面是配置页面示例。

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

此时，用户会看到两个选项按钮，**选择 "灰色**" 或**选择 "红色**" 以显示带有红色或灰色图标的选项卡内容。 选择 "相对" 按钮触发 `saveGray()` 或 `saveRed()` 调用以下命令：

1. "" `settings.setValidityState(true)` 设置为 "true"。
1. `microsoftTeams.settings.registerOnSaveHandler()`触发事件处理程序。
1. 启用 "在团队中上载的应用程序配置" 页上的 "**保存**" 按钮。

此代码使团队知道已满足配置要求，并且可以继续安装。 在**保存**时， `settings.setSettings()` 由接口定义的参数设置为 `Settings` 当前实例（请参阅[Settings interface](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest) ）。 最后， `saveEvent.notifySuccess()` 将调用，以指示内容 URL 已成功解析。

>[!NOTE]
>
>* 如果保存的处理程序是使用注册的 `microsoftTeams.settings.registerOnSaveHandler()` ，则回调必须调用 `saveEvent.notifySuccess()` 或 `saveEvent.notifyFailure()` 以指示配置的结果。
>* 如果未注册保存处理程序，则 `saveEvent.notifySuccess()` 会在用户选择 "**保存**" 按钮后立即自动进行呼叫。

### <a name="get-context-data-for-your-tab-settings"></a>获取选项卡设置的上下文数据

您的选项卡可能需要上下文信息才能显示相关内容。 上下文信息可以通过提供更多自定义的用户体验来进一步增强您的选项卡的吸引力。

团队[上下文界面](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest)定义可用于您的选项卡配置的属性。 您可以通过两种方式收集上下文数据变量的值：

1. 在清单中插入 URL 查询字符串占位符 `configurationURL` 。

1. 使用 "[团队" SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) `microsoftTeams.getContext((context) =>{}` 方法。

#### <a name="insert-placeholders-in-the-configurationurl"></a>将占位符插入到`configurationURL`

可以将上下文界面占位符添加到您的基础 `configurationUrl` 。 例如：

##### <a name="base-url"></a>基 Url

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

页面上载后，具有相关值的团队将更新查询字符串占位符。 您可以在配置页面中包含逻辑以检索和使用这些值。 有关使用 URL 查询字符串的详细信息，请参阅 MDN web 文档中的[URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) 。下面的示例展示了如何从上述属性中提取值 `configurationURL` ：

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

调用时， `microsoftTeams.getContext((context) => {})` 函数将检索[上下文接口](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest)。 您可以将此函数添加到您的配置页面以检索上下文值：

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

你可能需要进行身份验证，然后允许用户配置你的应用或你的内容可能包含具有自己的身份验证协议的源。 请参阅[对 Microsoft 团队中的用户进行身份验证选项卡](~/tabs/how-to/authentication/auth-flow-tab.md)上下文信息可用于帮助构造身份验证请求和授权页面 url。
确保在您的选项卡页中使用的所有域都列在 `manifest.json` `validDomains` 数组中。

## <a name="modify-or-remove-a-tab"></a>修改或删除选项卡

支持的删除选项可进一步优化用户体验。 您可以通过将清单的属性设置为，使用户能够修改、重新配置或重命名 "组/通道" 选项卡 `canUpdateConfiguration` `true` 。  此外，通过在应用中添加 "删除选项" 页并在配置中设置属性值，可以指定在删除选项卡时内容会发生什么情况 `removeUrl` `setSettings()` （请参阅下文）。 个人选项卡不能修改，但可由用户卸载。 有关详细信息，请参阅[创建选项卡的删除页](~/tabs/how-to/create-tab-pages/removal-page.md)。

## <a name="mobile-clients"></a>移动客户端

如果选择在工作组移动客户端上显示频道/组选项卡，则 `setSettings()` 配置必须具有 `websiteUrl` 属性值（请参阅下文）。 将很快发布对移动客户端上的选项卡的完全支持。 若要准备更新，应按照移动选项卡[上的选项卡指南中](~/tabs/design/tabs-mobile.md)的步骤创建选项卡。

Microsoft 团队 setSettings （）配置，用于删除页面和/或移动客户端：

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "URL REQUIRED FOR MOBILE CLIENTS",
    removeUrl: "ADD REMOVAL PAGE URL HERE"
});
```
