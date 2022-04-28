---
title: 创建配置页
author: surbhigupta
description: 了解如何创建配置页来配置频道或群聊以进行设置，例如，获取上下文数据、插入占位符以及使用代码示例进行身份验证。
keywords: teams 选项卡组通道可配置
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: dc1c5c7c8852d13ab490ae0782be0a01eef3fbea
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103416"
---
# <a name="create-a-configuration-page"></a>创建配置页

配置页是一种特殊类型的 [内容页](content-page.md)。 用户使用配置页配置Microsoft Teams应用的某些方面，并使用该配置作为以下内容的一部分：

* 频道或群集聊天选项卡：从用户收集信息并设置 `contentUrl` 要显示的内容页。
* [消息扩展。](~/messaging-extensions/what-are-messaging-extensions.md)
* [Office 365连接器](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)。

## <a name="configure-a-channel-or-group-chat-tab"></a>配置频道或群组聊天选项卡

应用程序必须引用 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) 并调用`microsoft.initialize()`。 所使用的 URL 必须保护 HTTPS 终结点，并且可从云中使用。

### <a name="example"></a>示例

下图显示了配置页的示例：

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

下面的代码是配置页的相应代码示例：

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
    ...
</body>
```

选择配置页中的“ **选择灰色** ”或 **“选择红色** ”按钮，以显示带有灰色或红色图标的选项卡内容。

下图显示了选项卡内容，其中选择了 **“灰色** ”图标：

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

下图显示了选项卡内容，其中选择了 **“红色** ”图标：

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

选择适当的按钮会触发或`saveGray()``saveRed()`调用以下命令：

* 设置 `settings.setValidityState(true)` 为 true。
* 事件 `microsoftTeams.settings.registerOnSaveHandler()` 处理程序已触发。
* **“保存** 在应用的配置页上”已启用。

配置页代码通知Teams满足配置要求，并且安装可以继续进行。 当用户选择 **“保存**”时，将根据接口定义`Settings`设置参数`settings.setSettings()`。 有关详细信息，请参阅 [设置接口](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)。 `saveEvent.notifySuccess()` 调用以指示内容 URL 已成功解析。

>[!NOTE]
>
>* 有 30 秒的时间在超时前完成保存操作 (回调到 registerOnSaveHandler) 。 超时后，将显示一条泛型错误消息。
>* 如果使用 `microsoftTeams.settings.registerOnSaveHandler()`注册保存处理程序，则回调必须调用 `saveEvent.notifySuccess()` 或 `saveEvent.notifyFailure()` 指示配置的结果。
>* 如果未注册保存处理程序，则在 `saveEvent.notifySuccess()` 用户选择 **“保存**”时会自动进行调用。

### <a name="get-context-data-for-your-tab-settings"></a>获取选项卡设置的上下文数据

选项卡需要上下文信息才能显示相关内容。 上下文信息通过提供更自定义的用户体验，进一步增强了选项卡的吸引力。

有关用于选项卡配置的属性的详细信息，请参阅 [上下文接口](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true)。 通过以下两种方式收集上下文数据变量的值：

* 在清单 `configurationURL`中插入 URL 查询字符串占位符。

* 使用 [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` 方法。

#### <a name="insert-placeholders-in-the-configurationurl"></a>在其中插入占位符 `configurationUrl`

将上下文接口占位符添加到基 `configurationUrl`。 例如：

##### <a name="base-url"></a>基 URL

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a>包含查询字符串的基本 URL

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

页面上传后，Teams使用相关值更新查询字符串占位符。 在配置页中包含用于检索和使用这些值的逻辑。 有关使用 URL 查询字符串的详细信息，请参阅 MDN Web Docs 中的 [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) 。以下代码示例提供了从 `configurationUrl` 属性中提取值的方法：

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a>使用该 `getContext()` 函数检索上下文

调用时，函 `microsoftTeams.getContext((context) => {})` 数将检索 [上下文接口](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) 。

以下代码提供了将此函数添加到配置页以检索上下文值的示例：

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

在允许用户配置应用之前进行身份验证。 否则，内容可能包含具有其身份验证协议的源。 有关详细信息，请参阅[Microsoft Teams选项卡中对用户进行身份验证](~/tabs/how-to/authentication/auth-flow-tab.md)。使用上下文信息构造身份验证请求和授权页 URL。 确保选项卡页中使用的所有域都列在选项卡页和`validDomains`数组中`manifest.json`。

## <a name="modify-or-remove-a-tab"></a>修改或删除选项卡

将清单的 `canUpdateConfiguration` 属性设置为 `true`，使用户能够修改、重新配置或重命名通道或组选项卡。此外，通过在应用中包括删除选项页并在配置中设置 `removeUrl` 属性  `setSettings()` 的值，指示删除选项卡时内容会发生什么情况。 用户可以卸载个人选项卡，但不能修改它们。 有关详细信息，请参阅 [为选项卡创建删除页](~/tabs/how-to/create-tab-pages/removal-page.md)。

`setSettings()` Microsoft Teams删除页的配置：

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add a unique identifier here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a>移动客户端

如果选择在Teams移动客户端上显示频道或组选项卡，则`setSettings()`配置必须具有值`websiteUrl`。 有关详细信息，请参阅 [有关移动选项卡的指南](~/tabs/design/tabs-mobile.md)。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [为选项卡创建删除页](~/tabs/how-to/create-tab-pages/removal-page.md)

## <a name="see-also"></a>另请参阅

* [Teams选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建通道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)
* [创建内容页](~/tabs/how-to/create-tab-pages/content-page.md)
* [移动设备上的选项卡](~/tabs/design/tabs-mobile.md)
