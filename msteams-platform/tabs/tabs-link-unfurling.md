---
title: 选项卡链接展开和阶段视图
author: Rajeshwari-v
description: 了解如何取消链接、打开"阶段视图"，然后使用"应用"固定Microsoft Teams选项卡。 了解阶段视图，以及使用代码示例和示例使用自适应卡片调用它。
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
ms.openlocfilehash: 3119e444c8dd2b654f26b2fad5638f7c831619ac
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518252"
---
# <a name="tabs-link-unfurling-and-stage-view"></a>选项卡链接展开和阶段视图

阶段视图是 UI (组件) 用户界面，允许你呈现在 Teams 中全屏打开并固定为选项卡的内容。
 
## <a name="stage-view"></a>阶段视图

阶段视图是一个全屏 UI 组件，你可以调用它来显示 Web 内容。 现有链接取消点击服务已更新，以便它可用于使用自适应卡片和聊天服务将 URL 转换为选项卡。 当用户在聊天或频道中发送 URL 时，该 URL 将取消展开到自适应卡片。 用户可以 **选择卡片中的** "查看"，并直接从"阶段视图"将内容固定为选项卡。

## <a name="advantage-of-stage-view"></a>阶段视图的优点

阶段视图有助于提供在网站中查看内容Teams。 用户无需离开上下文即可打开和查看应用提供的内容，并且可以将内容固定到聊天或频道，以便将来快速访问，从而提高用户对你的应用的参与度。

## <a name="stage-view-vs-task-module"></a>阶段视图与任务模块

|阶段视图|任务模块|
|:-----------|:-----------|
|当您具有要向用户显示的丰富内容（如页面、仪表板、文件等）时，阶段视图非常有用。 它提供了丰富的功能，可帮助在全屏画布中呈现内容。|[任务模块](../task-modules-and-cards/task-modules/task-modules-tabs.md) 对于显示需要用户注意的消息或收集移动到下一步所需信息特别有用。|
  
## <a name="invoke-stage-view"></a>调用阶段视图

可以通过以下方法调用阶段视图：

* [从自适应卡片调用阶段视图](#invoke-stage-view-from-adaptive-card)
* [通过深层链接调用阶段视图](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a>从自适应卡片调用阶段视图

当用户在桌面客户端上Teams URL 时，将调用自动程序并返回自适应卡片，并可选择在阶段[](../task-modules-and-cards/cards/cards-actions.md)中打开 URL。 启动阶段并提供了 `tabInfo` 后，你可以添加将阶段固定为选项卡的能力。  

下图显示从自适应卡片打开的阶段：

[![从自适应卡片打开阶段](~/assets/images/tab-images/open-stage-from-adaptive-card1.png)](~/assets/images/tab-images/open-stage-from-adaptive-card1.png#lightbox)

[![打开一个阶段](~/assets/images/tab-images/open-stage-from-adaptive-card2.png)](~/assets/images/tab-images/open-stage-from-adaptive-card2.png#lightbox) 

### <a name="example"></a>示例

下面是从自适应卡片打开阶段的代码：

```json
{
    type: "Action.Submit",
    name: "View",
    data: {
          msteams: {
            type: "invoke",
            value: {
                type: "tab/tabInfoAction",
                tabInfo: {
                    contentUrl: contentUrl,
                    websiteUrl: websiteUrl,
                    name: "Tasks",
                    entityId: "entityId"
                 }
                }
            }
        }
} 
```

请求 `invoke` 类型必须为 `composeExtension/queryLink`。

> [!NOTE]
> * `invoke` 工作流类似于当前 `appLinking` 工作流。 
> * 为了保持一致性，建议将 名称为 `Action.Submit` `View`。
> * `websiteUrl` 是对象中传递的必需 `TabInfo` 属性。

以下是调用阶段视图的过程：

* 当用户选择"查看 **"** 时，机器人会收到一个 `invoke` 请求。 请求类型为 `composeExtension/queryLink`。
* `invoke` 来自自动程序的响应包含包含类型为的自适应 `tab/tabInfoAction` 卡片。
* 机器人使用代码进行 `200` 响应。

> [!NOTE]
> 在Teams客户端上，调用通过 [Teams](/platform/concepts/deploy-and-publish/apps-publish-overview.md) 应用商店分发的应用的阶段视图，并且没有 moblie 优化体验，这将打开设备的默认 Web 浏览器。 浏览器打开在 对象的 参数中 `websiteUrl` 指定的 `TabInfo` URL。

## <a name="invoke-stage-view-through-deep-link"></a>通过深层链接调用阶段视图

若要通过选项卡中的深层链接调用阶段视图，必须在 API `microsoftTeams.executeDeeplink(url)` 中包装深层链接 URL。 深度链接也可通过卡片 `OpenURL` 中的操作传递。

### <a name="syntax"></a>语法

以下是 deeplink 语法： 

https://teams.microsoft.com/l/stage/{appId}/0?context={"contentUrl"："contentUrl"，"websiteUrl"："websiteUrl"，"name"："Contoso"}
 
### <a name="examples"></a>示例

当用户输入 URL 时，该 URL 将取消展开到自适应卡片中。

以下是调用阶段视图的深层链接示例：

**示例 1：具有 threadId 的 URL**

未编码的 URL：
 
https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context={"contentUrl"："https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191"，"websiteUrl"："https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true"，"title"："Quotes：Miscellaneous"，"threadId"："19：9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2"}

编码的 URL：

https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%2C%22threadId%22%3A%2219:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2%22%7D


**示例 2：没有 threadId 的 URL**

未编码的 URL：

https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context={"contentUrl"："https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191"，"websiteUrl"："https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true"，"title"："Quotes：Miscellaneous"}

已编码

https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%7D


> [!NOTE]
> 粘贴 URL 之前，必须编码所有深度链接。 我们不支持未编码的 URL。
> * 在 `name` 深层链接中是可选的。 如果未包含，则应用名称将替换它。
> * 深度链接也可通过操作 `OpenURL` 传递。
> * 当你从特定上下文启动阶段时，请确保你的应用在该上下文中工作。 例如，如果你的阶段视图从个人应用启动，则必须确保你的应用具有个人作用域。

## <a name="tab-information-property"></a>选项卡信息属性

| 属性名称 | 类型 | 字符数 | 说明 |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | String | 64 | 此属性是选项卡显示的实体的唯一标识符。 这是必填字段。|
| `name` | 字符串 | 128 | 此属性是显示名称界面中选项卡的键值。 这是一个可选字段。|
| `contentUrl` | 字符串 | 2048 | 此属性是指向要 https:// 画布中的实体 UI 的 Teams URL。 这是必填字段。|
| `websiteUrl?` | String | 2048 | 如果用户选择在 https:// 查看，则此属性是指向的 URL。 这是必填字段。|
| `removeUrl?` | 字符串 | 2048 | 此属性是 https:// 选项卡时要显示的 UI 的 URL。这是一个可选字段。|

## <a name="code-sample"></a>代码示例

| 示例名称 | Description | C# |Node.js|
|-------------|-------------|------|----|
|阶段视图中的选项卡 |Microsoft Teams阶段视图中演示选项卡的选项卡示例应用。|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/nodejs)|
    

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [创建对话选项卡](~/tabs/how-to/conversational-tabs.md)

## <a name="see-also"></a>另请参阅

* [取消展开消息传递扩展链接](~/messaging-extensions/how-to/link-unfurling.md)
* [Teams选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建频道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)
