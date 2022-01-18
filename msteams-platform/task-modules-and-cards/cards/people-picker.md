---
title: 自适应卡片中的人员选取器
description: 介绍如何在自适应卡片中使用人员选取器控件
localization_priority: Normal
keywords: 自适应卡片人员选取器
ms.topic: reference
author: Rajeshwari-v
ms.author: surbhigupta
ms.openlocfilehash: d0183ea8f00c14e93586c0c12e02b837a41572c9
ms.sourcegitcommit: 98cde8ff08552da4ce36fb0463982366bed979e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2022
ms.locfileid: "62062538"
---
# <a name="people-picker-in-adaptive-cards"></a>自适应卡片中的人员选取器

>[!NOTE]
> 目前，自适应卡片中的人员选取器仅在移动版[](../../resources/dev-preview/developer-preview-intro.md#public-developer-preview-for-microsoft-teams)开发人员预览版中提供，并公开 (GA) 桌面版。

人员选取器可帮助用户在自适应卡片中搜索和选择用户。 你可以将人员选取器作为输入控件添加到自适应卡片，它适用于聊天、频道、任务模块和选项卡。 人员选取器支持以下功能：        

* 搜索一个或多个用户。
* 选择一个或多个用户。 
* 重新分配到单个或多个用户。 
* 预填充所选用户的名称。

## <a name="popular-scenarios"></a>热门方案 

下表为自适应卡片中的人员选取器提供了热门方案以及相应的操作：

|应用场景|操作|
|----------|-------------------------|
|基于审批的方案| 根据要求请求、分配审批并将其重新分配给目标用户。|
|事件管理| 跟踪事件并通知、分配和重新分配给预期用户以立即采取措施。| 
|项目管理| 向特定用户分配票证或 Bug。|
|用户查找| 搜索整个组织的用户。|

# <a name="desktop"></a>[桌面设备](#tab/desktop)

Web 和桌面客户端支持自适应卡片中的人员选取器。 在 Web 上搜索时，人员选取器涉及内联键入体验。

### <a name="reassignment-scenario-example"></a>重新分配方案示例

用户 A (Robert) 收到频道中任务的票证，并意识到被分派人不正确。 用户 A 重新分配将信息发送回机器人的任务。 

**重新分配任何任务**

1. 选择 **"** 重新分配"，其中人员选取器字段预填充了名称，以将任务重新分配给预期用户。
1. 删除不正确的用户名。 
1. 根据图像方案选择目标用户、用户 B (Mona) 和C (Robin) 任务。 
1. 选择“**分配**”。 分配后，信息将发送给自动程序。 
   机器人更新自适应卡片并通知目标用户。 
 
下图显示了重新分配方案：    

![桌面上的"人员选取器"](../../assets/images/cards/desktoppp.gif)

# <a name="mobile"></a>[移动设备](#tab/mobile)

> [!NOTE]
> 目前，此功能仅适用于公共 [开发人员预览](../../resources/dev-preview/developer-preview-intro.md#public-developer-preview-for-microsoft-teams) 版。

Android 和 iOS 移动客户端支持自适应卡片中的人员选取器。 您可以在移动版中使用人员选取器来搜索和选择用户，以增强用户体验。 搜索体验类似于移动版中任何其他用户选择体验。

### <a name="reassignment-scenario-example"></a>重新分配方案示例

用户 A (Robert) 收到频道中任务的票证，并意识到被分派人不正确。 用户 A 重新分配将信息发送回机器人的任务。 

**重新分配任何任务**

1. 选择 **"** 重新分配"，其中人员选取器字段预填充了名称，以将任务重新分配给预期用户。
1. 删除不正确的用户名。
1. 根据图像方案选择目标用户、用户 B (Mona) 和C (Robin) 任务。
1. 选择“完成”。
1. 选择“**分配**”。 分配后，信息将发送给自动程序。 
   机器人更新自适应卡片并通知目标用户。 

下图显示了重新分配方案： 

![移动版人员选取器](../../assets/images/cards/mobilepp.gif)

---

## <a name="implement-people-picker"></a>实现人员选取器

人员选取器作为 [Input.ChoiceSet](https://adaptivecards.io/explorer/Input.ChoiceSet.html) 控件的扩展实现。 输入控件包括以下选择：   

* 下拉列表，例如展开的选定内容。
* 单选按钮，例如单个选择。
* 复选框，例如多个选择。  

> [!NOTE]
> 控件 `Input.ChoiceSet` 基于 和 `style` `isMultiSelect` 属性。  

### <a name="update-schema"></a>更新架构

以下属性是架构中 `Input.ChoiceSet` 新增的，用于启用卡片上的人员选取器体验：  

#### <a name="inputchoiceset-control"></a>Input.ChoiceSet 控件

|属性 |类型 |必需 |说明 |
|----|----|----|----|
|**choices.data** |**Data.Query** |否 |通过从指定的数据集提取结果，为不同的用户类型启用动态自动完成。 |

#### <a name="dataquery"></a>Data.Query

|属性 |类型 |必需 |说明|
|--|--|--|--|
|**dataset** |字符串 |是 |必须动态提取的数据类型。|   

#### <a name="dataset"></a>dataset
下表提供了预定义 **的值作为人员** 选取器数据集：   

|dataset|搜索范围
|--|--|
|**graph.microsoft.com/users** |搜索整个组织的所有成员。|
|**graph.microsoft.com/users?scope=currentContext** |在当前对话的成员中搜索，例如发送特定卡片的聊天或频道。|        

### <a name="example"></a>示例
使用组织搜索创建人员选取器的代码示例如下所示：

```json 
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "size": "Medium",
            "weight": "Bolder",
            "text": "People Picker with Org search enabled"
        },
        {
            "type": "Input.ChoiceSet",
            "choices": [],
            "choices.data": {
                "type": "Data.Query",
                "dataset": "graph.microsoft.com/users"
            },
            "id": "people-picker",
            "isMultiSelect": true
        }
    ],
    "actions": [
        {
            "type": "Action.Submit",
            "title": "Submit"
        }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```  

下图说明了自适应卡片和组织搜索中的人员选取器：

![人员选取器组织搜索](../../assets/images/cards/peoplepicker-org-search.png)

若要在对话成员列表中启用搜索，请使用数据集表中定义的 [相应](#dataset) 数据集。 `isMultiSelect` 属性用于启用控件中多个用户的选择。 默认情况下，此设置设置为 false，并且此设置仅允许您选择单个用户。

### <a name="data-submission"></a>数据提交

可以使用 或 `Action.Submit` `Action.Execute` 将所选数据提交到自动程序。 在 `invoke` 自动程序上收到的负载是静态AAD提供的有效负载列表。
在人员选取器中，在控件中选择用户时，用户的 `AAD ID` 是发送回的值。 `AAD ID`是字符串，唯一标识目录中的用户。

提交给自动程序的值的格式取决于属性的值 `isMultiSelect` ：

|的值 `isMultiSelect`|格式|
|--|--|
|false _(单选)_|<selected_AAD_ID>|
|true _(多选)_|<selected_AAD_ID_1>，<selected_AAD_ID_2>，<selected_AAD_ID_3>|  

使用 `AAD ID` ，人员选取器会预选相应的用户。 

## <a name="preselection-of-user"></a>用户预选

在创建和发送自适应卡片时，人员选取器支持在控件中预选用户。 `Input.ChoiceSet` 支持 `value` 用于预选用户的属性。 此属性的格式 `value` 与数据提交中提交的值 [格式相同](#data-submission)。  
以下列表提供预选用户的信息：

* 对于控件中的单个用户，将 `AAD ID` 该用户指定为 `value` 。 
* 对于多个用户，例如 `isMultiSelect` ，指定 `true` 以逗号分隔的 s `AAD ID` 字符串。  

以下示例介绍单个用户的预选：

```json
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "size": "Medium",
            "weight": "Bolder",
            "text": "People Picker with Org search enabled"
        },
        {
            "type": "Input.ChoiceSet",
            "choices": [],
            "choices.data": {
                "type": "Data.Query",
                "dataset": "graph.microsoft.com/users"
            },
            "id": "people-picker",
            "value": "<AAD ID 1>"
        }
    ],
    "actions": [
        {
            "type": "Action.Submit",
            "title": "Submit"
        }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```  

以下示例介绍多个用户的预选：

```json
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "size": "Medium",
            "weight": "Bolder",
            "text": "People Picker with Org search enabled"
        },
        {
            "type": "Input.ChoiceSet",
            "choices": [],
            "choices.data": {
                "type": "Data.Query",
                "dataset": "graph.microsoft.com/users"
            },
            "id": "people-picker",
            "isMultiSelect": true,
            "value": "<AAD ID 1>,<AAD ID 2>,<AAD ID 3>"
        }
    ],
    "actions": [
        {
            "type": "Action.Submit",
            "title": "Submit"
        }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```
 
## <a name="static-choices"></a>静态选择

静态选择支持必须将自定义配置文件插入预定义数据集的方案。 `Input.ChoiceSet` 支持在 `choices` json 中静态指定。 静态选项用于创建用户可以从中选择的选项。

> [!NOTE]
> 静态 `choices` 与动态数据集一同使用。 

选项包括 `title` 和 `value` 。 与人员选取器一起使用时，这些选项将转换为以 作为名称和 作为标识符 `title` `value` 的用户配置文件。 当搜索查询与给定 匹配时，这些自定义配置文件也是搜索结果的一部分 `title` 。    
以下示例介绍静态选择： 

```json
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "size": "Medium",
            "weight": "Bolder",
            "text": "People Picker with Org search enabled"
        },
        {
            "type": "Input.ChoiceSet",
            "choices": [
                {
                    "title": "Custom Profile 1",
                    "value": "Profile1"
                },
                {
                    "title": "Custom Profile 2",
                    "value": "Profile2"
                }
            ],
            "choices.data": {
                "type": "Data.Query",
                "dataset": "graph.microsoft.com/users"
            },
            "id": "people-picker",
            "isMultiSelect": true
        }
    ],
    "actions": [
        {
            "type": "Action.Submit",
            "title": "Submit"
        }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

下图使用组织搜索中的静态选项演示自适应卡片中的人员选取器：

![人员选取器静态选择](../../assets/images/cards/peoplepicker-static-choice.png)


您可以实现人员选取器，以在不同方案中高效地管理任务。  

## <a name="see-also"></a>另请参阅

[卡片参考](cards-reference.md)

