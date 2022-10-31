---
title: 创建配置页
author: surbhigupta
description: 创建配置页以收集用户的信息。 此外，获取 Microsoft Teams 选项卡的上下文数据，了解身份验证、修改或删除选项卡。
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 51e5ef0a6752ab70ede4d2da699f78910c08f6c9
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791700"
---
# <a name="create-a-configuration-page"></a>创建配置页

配置页是一种特殊类型的[内容页](content-page.md)。 用户将使用配置页配置 Microsoft Teams 应用的某些方面，并使用该配置作为以下内容的一部分：

* 频道或群组聊天选项卡：从用户收集信息，并设置要显示的内容页的 `contentUrl`。
* [消息扩展](~/messaging-extensions/what-are-messaging-extensions.md)。
* [Office 365 连接器](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)。

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="configure-a-channel-or-group-chat-tab"></a>配置频道或群组聊天选项卡

应用程序必须引用 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 并调用 `app.initialize()`。 使用的 URL 必须是安全的 HTTPS 终结点，并且可从云中获取。

### <a name="example"></a>示例

下图显示了配置页的示例：

:::image type="content" source="../../../assets/images/tab-images/configuration-page.png" alt-text="屏幕截图显示了配置页。":::

下面的代码是配置页的相应代码示例：

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```html
<head>
    <script src="https://res.cdn.office.net/teams-js/2.2.0/js/MicrosoftTeams.min.js" 
      integrity="sha384yBjE++eHeBPzIg+IKl9OHFqMbSdrzY2S/LW3qeitc5vqXewEYRWegByWzBN/chRh" 
      crossorigin="anonymous" >
    </script>
<body>
    <button onclick="(document.getElementById('icon').src = '/images/iconGray.png'); colorClickGray()">Select Gray</button>
    <img id="icon" src="/images/teamsIcon.png" alt="icon" style="width:100px" />
    <button onclick="(document.getElementById('icon').src = '/images/iconRed.png'); colorClickRed()">Select Red</button>

    <script>
        await microsoftTeams.app.initialize();
        let saveGray = () => {
            microsoftTeams.pages.config.registerOnSaveHandler((saveEvent) => {
                const configPromise = pages.config.setConfig({
                    websiteUrl: "https://yourWebsite.com",
                    contentUrl: "https://yourWebsite.com/gray",
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                configPromise.
                    then((result) => {saveEvent.notifySuccess()}).
                    catch((error) => {saveEvent.notifyFailure("failure message")});
            });
        }

        let saveRed = () => {
            microsoftTeams.pages.config.registerOnSaveHandler((saveEvent) => {
                const configPromise = pages.config.setConfig({
                    websiteUrl: "https://yourWebsite.com",
                    contentUrl: "https://yourWebsite.com/red",
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                configPromise.
                    then((result) => {saveEvent.notifySuccess();}).
                    catch((error) => {saveEvent.notifyFailure("failure message")});
            });
        }

        let gr = document.getElementById("gray").style;
        let rd = document.getElementById("red").style;

        const colorClickGray = () => {
            gr.display = "block";
            rd.display = "none";
            microsoftTeams.pages.config.setValidityState(true);
            saveGray()
        }

        const colorClickRed = () => {
            rd.display = "block";
            gr.display = "none";
            microsoftTeams.pages.config.setValidityState(true);
            saveRed();
        }
    </script>
    ...
</body>
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

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

***
选择配置页中的“**选择灰色**”或“**选择红色**”按钮，以显示带有灰色或红色图标的选项卡内容。

下图显示了选中 **灰色** 图标的选项卡内容：

:::image type="content" source="../../../assets/images/tab-images/configure-tab-with-gray.png" alt-text="屏幕截图显示了“配置”选项卡，其中选择灰色。":::

下图显示了选中 **红色** 图标的选项卡内容：

:::image type="content" source="../../../assets/images/tab-images/configure-tab-with-red.png" alt-text="屏幕截图显示了“配置”选项卡，其中选择了“红色”。":::

选择适当的按钮会触发 `saveGray()` 或 `saveRed()`，并调用以下命令：

* 将 `pages.config.setValidityState(true)` 设置为 true。
* 触发 `pages.config.registerOnSaveHandler()` 事件处理程序。
* 在应用的配置页上启用“**保存**”。

配置页代码会通知 Teams 满足配置要求，可以继续安装。 当用户选择“**保存**”时，将根据 `Config` 接口的定义设置 `pages.config.setConfig()` 的参数。 有关详细信息，请参阅 [配置接口](/javascript/api/@microsoft/teams-js/pages.config?)。 调用 `saveEvent.notifySuccess()` 以指示已成功解析内容 URL。

>[!NOTE]
>
>* 你有 30 秒的时间来完成保存操作， (超时前回调到 `registerOnSaveHandler`) 。 超时后，将显示一般错误消息。
>* 如果使用 `registerOnSaveHandler()` 注册保存处理程序，则回调必须调用 `saveEvent.notifySuccess()` 或 `saveEvent.notifyFailure()` 以指示配置的结果。
>* 如果未注册保存处理程序，则当用户选择“**保** 存”时，将自动进行 `saveEvent.notifySuccess()` 调用。
>* 确保具有唯一 `entityId`的 。 重复 `entityId` 重定向到选项卡的第一个实例。

### <a name="get-context-data-for-your-tab-settings"></a>获取选项卡设置的上下文数据

选项卡需要上下文信息才能显示相关内容。 上下文信息通过提供更加个性化的用户体验，进一步增强了选项卡的吸引力。

有关用于选项卡配置的属性的详细信息，请参阅[上下文接口](/javascript/api/@microsoft/teams-js/app.context?view=msteams-client-js-latest&preserve-view=true)。 通过以下两种方式收集上下文数据变量的值：

* 在清单的 `configurationURL` 中插入 URL 查询字符串占位符。

* 使用 [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `app.getContext()` 方法。

#### <a name="insert-placeholders-in-the-configurationurl"></a>在 `configurationUrl` 中插入占位符

将上下文接口占位符添加到基 `configurationUrl`。 例如：

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

页面上传后，Teams 会使用相关值更新查询字符串占位符。 请在配置页中包括逻辑以检索和使用这些值。 有关使用 URL 查询字符串的详细信息，请参阅 MDN Web Docs 中 [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams)。下面的代码示例提供了从 `configurationUrl` 属性中提取值的方法：

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```html
<script>
   await microsoftTeams.app.initialize();
   const getId = () => {
        let urlParams = new URLSearchParams(document.location.search.substring(1));
        let blueTeamId = urlParams.get('team');
        return blueTeamId
    }
//For testing, you can invoke the following to view the pertinent value:
document.write(getId());
</script>
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

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

***

### <a name="use-the-getcontext-function-to-retrieve-context"></a>使用 `getContext()` 函数检索上下文

函数 `app.getContext()` 返回一个通过 [上下文接口](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest&preserve-view=true) 对象解析的 promise。

以下代码提供了将此函数添加到配置页以检索上下文值的示例：

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```html
<!-- `userPrincipalName` will render in the span with the id "user". -->

<span id="user"></span>
...
<script type="module">
    import {app} from 'https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js';
    const contextPromise = app.getContext();
    contextPromise.
        then((context) => {
            let userId = document.getElementById('user');
            userId.innerHTML = context.user.userPrincipalName;
        }).
        catch((error) => {/*Unsuccessful operation*/});
</script>
...
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

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

***

## <a name="context-and-authentication"></a>上下文和身份验证

在允许用户配置应用之前进行身份验证。 否则，内容可能包含具有其身份验证协议的源。 有关详细信息，请参阅[在 Microsoft Teams 选项卡中对用户进行身份验证](~/tabs/how-to/authentication/auth-flow-tab.md)。请使用上下文信息构造身份验证请求和授权页面 URL。 确保选项卡页中使用的所有域都列在 `manifest.json` 和 `validDomains` 数组中。

## <a name="modify-or-remove-a-tab"></a>修改或删除选项卡

将清单的 `canUpdateConfiguration` 属性设置为 `true`。 它使用户能够修改或重新配置频道或组选项卡。只能通过 Teams 用户界面重命名选项卡。 在删除选项卡时通知用户对内容的影响。 为此，请在应用中包括删除选项页，并在以前`setSettings()`) 配置 (中设置 `removeUrl` 属性`setConfig()`的值。 用户可以卸载个人选项卡，但无法修改它们。 有关详细信息，请参阅[为选项卡创建删除页](~/tabs/how-to/create-tab-pages/removal-page.md)。

Microsoft Teams `setConfig()` (以前 `setSettings()`) 删除配置页面：

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```javascript
import { pages } from "@microsoft/teams-js";
const configPromise = pages.config.setConfig({
    contentUrl: "add content page URL here",
    entityId: "add a unique identifier here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
configPromise.
    then((result) => {/*Successful operation*/).
    catch((error) => {/*Unsuccessful operation*/});
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add a unique identifier here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

***

## <a name="mobile-clients"></a>移动客户端

如果选择让频道或群组选项卡显示在 Teams 移动客户端上，则 `setConfig()` 配置必须具有 `websiteUrl` 的值。 有关详细信息，请参阅[移动设备上的选项卡指南](~/tabs/design/tabs-mobile.md)。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [为选项卡创建删除页](~/tabs/how-to/create-tab-pages/removal-page.md)

## <a name="see-also"></a>另请参阅

* [Teams 选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建频道或群组选项卡](~/tabs/how-to/create-channel-group-tab.md)
* [创建内容页](~/tabs/how-to/create-tab-pages/content-page.md)
* [移动设备上的选项卡](~/tabs/design/tabs-mobile.md)
