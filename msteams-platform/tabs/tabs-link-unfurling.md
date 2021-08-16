---
title: 选项卡链接展开和阶段视图
author: Rajeshwari-v
description: 如何取消链接，打开"阶段视图"，然后使用"Microsoft Teams固定选项卡。
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: f465530dcc53ff3b0174f5b78ebf2240665a7d9e
ms.sourcegitcommit: 2c4c77dc8344f2fab8ed7a3f7155f15f0dd6a5ce
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "58345274"
---
# <a name="tabs-link-unfurling-and-stage-view"></a>选项卡链接展开和阶段视图

> [!NOTE]
> 此功能仅在公共 [开发人员预览版中](../resources/dev-preview/developer-preview-intro.md) 可用。

阶段视图是 UI (组件) 用户界面，允许你呈现在屏幕中全屏打开Teams固定为选项卡的内容。
 
> [!NOTE]
> 目前，Teams客户端不支持选项卡链接取消展开和阶段视图。 移动客户端使用开发人员提供的 属性在设备的 Web 浏览器中 `websiteUrl` 打开页面。

## <a name="stage-view"></a>阶段视图

阶段视图是一个全屏 UI 组件，你可以调用它来显示 Web 内容。 现有链接取消点击服务已更新，以便它可用于使用自适应卡片和聊天服务将 URL 转换为选项卡。 当用户在聊天或频道中发送 URL 时，该 URL 将取消展开到自适应卡片。 用户可以 **选择卡片中的** "查看"，并直接从"阶段视图"将内容固定为选项卡。

## <a name="advantage-of-stage-view"></a>阶段视图的优点

阶段视图有助于提供在网站中查看内容Teams。 用户无需离开上下文即可打开和查看应用提供的内容，并且可以将内容固定到聊天或频道，以便将来快速访问。 这可提高用户对你的应用的参与度。

## <a name="stage-view-vs-task-module"></a>阶段视图与任务模块

|阶段视图|任务模块|
|:-----------|:-----------|
|当您具有要向用户显示的丰富内容（如页面、仪表板、文件等）时，阶段视图非常有用。 它提供了丰富的功能，可帮助在全屏画布中呈现内容。|[任务模块](../task-modules-and-cards/task-modules/task-modules-tabs.md) 对于显示需要用户注意的消息或收集移动到下一步所需信息特别有用。|
  
## <a name="invoke-stage-view"></a>调用阶段视图

可以通过以下方法调用阶段视图：

* [从自适应卡片调用阶段视图](#invoke-stage-view-from-adaptive-card)
* [通过深层链接调用阶段视图](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a>从自适应卡片调用阶段视图

当用户在桌面客户端上Teams URL 时，将调用自动程序并返回自适应卡片，并可选择在[](../task-modules-and-cards/cards/cards-actions.md)阶段中打开 URL。 启动阶段并提供了 后，你可以 `tabInfo` 添加将阶段固定为选项卡的能力。  

下图显示从自适应卡片打开的阶段：

<img src="~/assets/images/tab-images/open-stage-from-adaptive-card1.png" alt="Open a stage from Adaptive Card" width="700"/>

<img src="~/assets/images/tab-images/open-stage-from-adaptive-card2.png" alt="Open a stage" width="700"/>

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

请求 `invoke` 类型必须为 `composeExtension/queryLink` 。

> [!NOTE]
> * `invoke` 工作流类似于当前 `appLinking` 工作流。 
> * 为了保持一致性，建议将 名称 `Action.Submit` 为 `View` 。
> * `websiteUrl` 是对象中传递的必需 `TabInfo` 属性。

以下是调用阶段视图的过程：

* 当用户选择"查看 **"时**，机器人会收到 `invoke` 一个请求。 请求类型为 `composeExtension/queryLink` 。
* `invoke` 来自自动程序的响应包含包含类型为的 `tab/tabInfoAction` 自适应卡片。
* 机器人使用代码 `200` 进行响应。

> [!NOTE]
> 目前，Teams客户端不支持阶段视图功能。 当用户 **选择"在** 移动客户端上查看"时，用户会访问设备的浏览器。 浏览器打开在 对象的 参数 `websiteUrl` 中指定的 `TabInfo` URL。

## <a name="invoke-stage-view-through-deep-link"></a>通过深层链接调用阶段视图

若要通过选项卡中的深层链接调用阶段视图，必须在 API 中包装深层链接 `microsoftTeams.executeDeeplink(url)` URL。 深度链接也可通过卡片 `OpenURL` 中的操作传递。

下图显示了通过深层链接调用的阶段视图：

<img src="~/assets/images/tab-images/invoke-stage-view-through-deep-link.png" alt="Invoke a Stage View through a deep link" width="400"/>

### <a name="syntax"></a>语法

以下是 deeplink 语法：  
 
https://teams.microsoft.com/l/stage/{appId}/0?context={"contentUrl"："[contentUrl]"，"websiteUrl"："[websiteUrl]"，"name"："[name]"}

### <a name="examples"></a>示例

当用户输入 URL 时，该 URL 将取消展开到自适应卡片中。

以下是调用阶段视图的深层链接示例：

**示例 1**

https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={"contentUrl"："https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx"，"websiteUrl"："https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx"，"name"："Contoso"}

**示例 2**

https://teams.microsoft.com/l/Meeting_Stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={"contentUrl"："https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx"，"websiteUrl"："https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx"，"name"："Contoso"}

> [!NOTE]
> * 在 `name` 深层链接中是可选的。 如果未包含，则应用名称将替换它。
> * 深度链接也可通过操作 `OpenURL` 传递。
> * 目前，Teams客户端不支持阶段视图功能。 当用户选择到阶段视图的深层链接时，他们会进入其设备的 Web 浏览器。 Web 浏览器将打开深层链接的 `websiteUrl` 参数中指定的 URL。
> * 当你从特定上下文启动阶段时，请确保你的应用在该上下文中工作。 例如，如果你的阶段视图从个人应用启动，则必须确保你的应用具有个人作用域。

## <a name="tab-information-property"></a>选项卡信息属性

| 属性名称 | 类型 | 字符数 | 说明 |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | String | 64 | 此属性是选项卡显示的实体的唯一标识符。 这是必填字段。|
| `name` | 字符串 | 128 | 此属性是显示名称界面中选项卡的列数。 这是一个可选字段。|
| `contentUrl` | 字符串 | 2048 | 此属性是指向要 https:// 画布中的实体 UI 的 Teams URL。 这是必填字段。|
| `websiteUrl?` | 字符串 | 2048 | 如果用户选择在 https:// 查看，则此属性是指向的 URL。 这是必填字段。|
| `removeUrl?` | 字符串 | 2048 | 此属性是 https:// 选项卡时要显示的 UI 的 URL。这是一个可选字段。|

## <a name="see-also"></a>另请参阅

* [取消展开消息传递扩展链接](~/messaging-extensions/how-to/link-unfurling.md)
* [Teams选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建频道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [创建对话选项卡](~/tabs/how-to/conversational-tabs.md)
