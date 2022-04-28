---
title: 选项卡链接展开和阶段视图
author: Rajeshwari-v
description: 了解如何展开链接、打开“阶段视图”并使用Microsoft Teams应用固定选项卡。 了解使用代码示例和示例使用自适应卡片的阶段视图和调用它。
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
ms.openlocfilehash: 043129d6a81543ac00acf8b64da49f75282823a2
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104082"
---
# <a name="tabs-link-unfurling-and-stage-view"></a>选项卡链接展开和阶段视图

阶段视图是 UI) 组件 (新的用户界面，可用于呈现在Teams中全屏打开并固定为选项卡的内容。

## <a name="stage-view"></a>阶段视图

阶段视图是一个全屏 UI 组件，可以调用它来显示 Web 内容。 现有链接展开服务已更新，以便使用自适应卡片和聊天服务将 URL 转换为选项卡。 当用户在聊天或频道中发送 URL 时，URL 将展开为自适应卡片。 用户可以在卡片中选择 **“查看** ”，并直接从“阶段视图”中将内容固定为选项卡。

## <a name="advantage-of-stage-view"></a>阶段视图的优势

阶段视图有助于提供在Teams中查看内容的更无缝体验。 用户可以在不离开上下文的情况下打开和查看应用提供的内容，并且他们可以将内容固定到聊天或频道，以便将来快速访问，从而提高用户与应用的参与度。

## <a name="stage-view-vs-task-module"></a>阶段视图与任务模块

|阶段视图|任务模块|
|:-----------|:-----------|
|当你有丰富的内容要显示给用户（例如页面、仪表板、文件等）时，阶段视图非常有用。 它提供了丰富的功能，有助于在全屏画布中呈现内容。|[任务模块](../task-modules-and-cards/task-modules/task-modules-tabs.md) 对于显示需要用户注意的消息或收集移动到下一步所需的信息特别有用。|
  
## <a name="invoke-stage-view"></a>调用阶段视图

可以通过以下方式调用阶段视图：

* [从自适应卡片调用阶段视图](#invoke-stage-view-from-adaptive-card)
* [通过深层链接调用阶段视图](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a>从自适应卡片调用阶段视图

当用户在Teams桌面客户端上输入 URL 时，将调用机器人并返回自[适应卡片](../task-modules-and-cards/cards/cards-actions.md)，其中包含在阶段中打开 URL 的选项。 启动阶段并 `tabInfo` 提供该阶段后，可以添加将阶段固定为选项卡的功能。  

以下图像显示从自适应卡片打开的阶段：

[![从自适应卡片打开一个阶段](~/assets/images/tab-images/open-stage-from-adaptive-card1.png)](~/assets/images/tab-images/open-stage-from-adaptive-card1.png#lightbox)

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

`invoke`请求类型必须为 `composeExtension/queryLink`。

> [!NOTE]
>
> * `invoke` 工作流类似于当前 `appLinking` 工作流。
> * 为了保持一致性，建议将其命名 `Action.Submit` 为 `View`。
> * `websiteUrl` 是要在对象中传递的 `TabInfo` 必需属性。

下面是调用阶段视图的过程：

* 当用户选择 **“视图**”时，机器人会收到请求 `invoke` 。 请求类型为 `composeExtension/queryLink`.
* `invoke` 来自机器人的响应包含一个自适应卡片，其中包含类型 `tab/tabInfoAction` 。
* 机器人使用代码进行响应 `200` 。

> [!NOTE]
> 在Teams移动客户端上，调用通过[Teams存储](/platform/concepts/deploy-and-publish/apps-publish-overview.md)分发的应用的阶段视图，而没有经过暴民优化的体验，则会打开设备的默认 Web 浏览器。 浏览器打开在对象参数中 `websiteUrl` 指定的 `TabInfo` URL。

## <a name="invoke-stage-view-through-deep-link"></a>通过深层链接调用阶段视图

若要通过选项卡中的深层链接调用阶段视图，必须在 API 中 `microsoftTeams.executeDeeplink(url)` 包装深层链接 URL。 也可以通过卡片中的操作 `OpenURL` 传递深层链接。

### <a name="syntax"></a>语法

下面是深度链接语法：

https://teams.microsoft.com/l/stage/{appId}/0?context={“contentUrl”：“contentUrl”，“websiteUrl”：“websiteUrl”，“name”：“Contoso”}
 
### <a name="examples"></a>示例

当用户输入 URL 时，它将展开到自适应卡片中。

下面是用于调用阶段视图的深层链接示例：

**示例 1：使用 threadId 的 URL**

未编码的 URL：

https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context={“contentUrl”：“https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191”，“websiteUrl”：“https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true”，“title”：“Quotes：Miscellaneous”，“threadId”：“19：9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2”}

编码的 URL：

https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%2C%22threadId%22%3A%2219:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2%22%7D

**示例 2：没有 threadId 的 URL**

未编码的 URL：

https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context={“contentUrl”：“https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191”，“websiteUrl”：“https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true”，“title”：“Quotes：Miscellaneous”}

编码

https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%7D

> [!NOTE]
> 粘贴 URL 之前，必须先对所有深层链接进行编码。 我们不支持未编码的 URL。
>
> * 在 `name` 深层链接中是可选的。 如果未包含，应用名称将替换它。
> * 也可以通过 `OpenURL` 操作传递深层链接。
> * 从特定上下文启动阶段时，请确保应用在该上下文中正常工作。 例如，如果阶段视图是从个人应用启动的，则必须确保应用具有个人范围。

## <a name="tab-information-property"></a>Tab information 属性

| 属性名称 | 类型 | 字符数 | 说明 |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | 字符串 | 64 | 此属性是选项卡显示的实体的唯一标识符。 这是必填字段。|
| `name` | 字符串 | 128 | 此属性是通道接口中选项卡的显示名称。 这是一个可选字段。|
| `contentUrl` | String | 2048 | 此属性是指向要在Teams画布中显示的实体 UI 的 https:// URL。 这是必填字段。|
| `websiteUrl?` | String | 2048 | 如果用户选择在浏览器中查看，则此属性是要指向的 https:// URL。 这是必填字段。|
| `removeUrl?` | String | 2048 | 此属性是指向用户删除选项卡时要显示的 UI 的 https:// URL。这是一个可选字段。|

## <a name="code-sample"></a>代码示例

| 示例名称 | Description | C# |Node.js|
|-------------|-------------|------|----|
|阶段视图中的选项卡 |Microsoft Teams选项卡示例应用，用于在阶段视图中演示选项卡。|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/nodejs)|

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [创建对话选项卡](~/tabs/how-to/conversational-tabs.md)

## <a name="see-also"></a>另请参阅

* [消息扩展链接展开](~/messaging-extensions/how-to/link-unfurling.md)
* [Teams选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建通道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)
