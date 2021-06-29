---
title: 创建配置页
author: surbhigupta
description: 如何创建配置页
keywords: teams 选项卡组频道可配置
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 4fb7667cdcd060d44b64de1719bff69b3f96615f
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179767"
---
# <a name="create-a-configuration-page"></a>创建配置页

配置页是一种特殊类型 [的内容页](content-page.md)。 用户使用配置页面配置 Microsoft Teams应用的一些方面，并使用以下配置：

* 频道或群聊选项卡：从用户收集信息，并设置要 `contentUrl` 显示的内容页的 。
* 消息传递 [扩展](~/messaging-extensions/what-are-messaging-extensions.md)。
* 一[Office 365连接器](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)。

## <a name="configure-a-channel-or-group-chat-tab"></a>配置频道或群聊选项卡

应用程序必须引用[JavaScript Microsoft Teams SDK 并](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)调用 `microsoft.initialize()` 。 使用的 URL 必须是安全的 HTTPS 终结点，并且可从云中访问。

### <a name="example"></a>示例

配置页的示例如下图所示：

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

以下代码是配置页的相应代码示例：

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

选择配置 **页中的**"选择灰色"或"选择红色"按钮，以显示带灰色或红色图标的选项卡内容。

下图显示带灰色图标的选项卡内容：

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

下图显示带红色图标的选项卡内容：

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

选择相应的按钮将触发 `saveGray()` 或 `saveRed()` ，并调用以下内容：

* 设置为 `settings.setValidityState(true)` true。 
* `microsoftTeams.settings.registerOnSaveHandler()`将触发事件处理程序。
* **在** 应用的配置页面上保存已启用。

配置页面代码Teams配置要求，并可以继续安装。 当用户选择"保存 **"** 时，将设置 的参数 `settings.setSettings()` ，如 接口 `Settings` 所定义。 有关详细信息，请参阅设置 [接口](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)。 `saveEvent.notifySuccess()` 调用 以指示已成功解析内容 URL。

>[!NOTE]
>
>* 如果使用 注册保存处理程序 `microsoftTeams.settings.registerOnSaveHandler()` ，回调必须调用 或 `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` 以指示配置的结果。
>* 如果未注册保存处理程序，则当用户选择"保存"时 `saveEvent.notifySuccess()` 会自动 **进行调用**。

### <a name="get-context-data-for-your-tab-settings"></a>获取选项卡设置的上下文数据

您的选项卡需要上下文信息来显示相关内容。 上下文信息通过提供更加自定义的用户体验进一步增强选项卡的吸引力。

有关用于选项卡配置的属性详细信息，请参阅 [上下文接口](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true)。 通过以下两种方式收集上下文数据变量的值：

* 在清单 中插入 URL 查询字符串占位符 `configurationURL` 。

* 使用[Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` 方法。

#### <a name="insert-placeholders-in-the-configurationurl"></a>在 中插入占位符 `configurationUrl`

将上下文接口占位符添加到基本 `configurationUrl` 。 例如：

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

上载页面后，Teams使用相关值更新查询字符串占位符。 在配置页中包括用于检索和使用这些值的逻辑。 有关使用 URL 查询字符串的信息，请参阅 MDN Web Docs 中的 [URLSearchParams。](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) 下面的代码示例提供了从 属性中提取值 `configurationUrl` 的方法：

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

`microsoftTeams.getContext((context) => {})`函数在调用[时检索](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true)上下文接口。

以下代码提供了一个向配置页添加此函数以检索上下文值的示例：

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

在允许用户配置你的应用之前进行身份验证。 否则，您的内容可能包括具有其身份验证协议的源。 有关详细信息，请参阅在"身份验证["选项卡中Microsoft Teams用户。](~/tabs/how-to/authentication/auth-flow-tab.md)使用上下文信息构建身份验证请求和授权页面 URL。 确保 选项卡页中使用的所有域都列在 `manifest.json` 和 `validDomains` 数组中。

## <a name="modify-or-remove-a-tab"></a>修改或删除选项卡

将清单的 属性设置为 ，以便用户能够修改、重新配置或 `canUpdateConfiguration` `true` 重命名频道或组选项卡。此外，通过包括应用中的删除选项页面和在配置中设置属性的值，指示删除选项卡时内容会发生什么 `removeUrl`  `setSettings()` 情况。 用户可以卸载个人选项卡，但不能修改它们。 有关详细信息，请参阅 [为选项卡创建删除页面](~/tabs/how-to/create-tab-pages/removal-page.md)。

`setSettings()`Microsoft Teams删除页面的配置：

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a>移动客户端

如果选择让频道或组选项卡显示在移动客户端Teams，则配置必须具有 `setSettings()` 的值 `websiteUrl` 。 有关详细信息，请参阅 [移动选项卡指南](~/tabs/design/tabs-mobile.md)。

## <a name="see-also"></a>另请参阅

* [Teams选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建频道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)
* [创建内容页](~/tabs/how-to/create-tab-pages/content-page.md)
* [移动设备上的选项卡](~/tabs/design/tabs-mobile.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [为选项卡创建删除页](~/tabs/how-to/create-tab-pages/removal-page.md)
