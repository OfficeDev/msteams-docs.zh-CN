---
title: 自适应卡片中的人员选取器
description: 介绍如何在自适应卡片中使用人员选取器控件
localization_priority: Normal
keywords: 自适应卡人选取器
ms.topic: reference
author: Rajeshwari-v
ms.author: surbhigupta
ms.openlocfilehash: 8a78be74d8142600ccc08093744491a19900e60b
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073420"
---
# <a name="people-picker-in-adaptive-cards"></a>自适应卡片中的人员选取器

>[!NOTE]
> 目前，自适应卡片中的人员选取器在 [公共开发人员预览](../../resources/dev-preview/developer-preview-intro.md#public-developer-preview-for-microsoft-teams) 版中仅适用于适用于桌面版的移动版和正式版 (正式版) 。

人员选取器可帮助用户在自适应卡片中搜索和选择用户。 可以将人员选取器添加为自适应卡片的输入控件，该卡可跨聊天、频道、任务模块和选项卡工作。 人员选取器支持以下功能：

* 搜索单个或多个用户。
* 选择单个或多个用户。
* 重新分配给单个或多个用户。
* 预先填充所选用户的名称。

## <a name="popular-scenarios"></a>常用方案

下表提供了自适应卡片中人员选取器的热门方案以及相应的操作：

|应用场景|操作|
|----------|-------------------------|
|基于审批的方案| 根据要求向预期用户请求、分配和重新分配审批。|
|事件管理| 跟踪事件并通知、分配和重新分配给预期用户以立即执行操作。|
|项目管理| 向特定用户分配票证或 bug。|
|用户查找| 在整个组织中搜索用户。|

# <a name="desktop"></a>[桌面设备](#tab/desktop)

Web 和桌面客户端支持自适应卡片中的人员选取器。 在 Web 上搜索时，“人员选取器”涉及内联键入体验。

### <a name="reassignment-scenario-example"></a>重新分配方案示例

用户 A (Robert) 在频道中收到任务的票证，并意识到分配者不正确。 用户 A 重新分配将信息发送回机器人的任务。

若要重新分配任何任务，请执行以下操作：

1. 选择 **“重新分配** 人员选取器”字段预填充名称的位置，以便将任务重新分配给预期用户。
1. 删除不正确的用户名。
1. 根据映像方案选择预期用户、用户 B (Mona) 和用户 C (Robin) 。
1. 选择“**分配**”。 分配后，信息将发送到机器人。
   机器人更新自适应卡片并通知预期用户。

下图显示了重新分配方案：

![桌面上的人员选取器](../../assets/images/cards/desktoppp.gif)

# <a name="mobile"></a>[移动设备](#tab/mobile)

> [!NOTE]
> 目前，此功能仅在 [公共开发人员预览版](../../resources/dev-preview/developer-preview-intro.md#public-developer-preview-for-microsoft-teams) 中可用。

Android 和 iOS 移动客户端支持自适应卡片中的人员选取器。 可以使用移动设备中的人员选取器来搜索和选择用户，以增强用户体验。 搜索体验类似于移动版中的任何其他用户选择体验。

### <a name="reassignment-scenario-example"></a>重新分配方案示例

用户 A (Robert) 在频道中收到任务的票证，并意识到分配者不正确。 用户 A 重新分配将信息发送回机器人的任务。

若要重新分配任何任务，请执行以下操作：

1. 选择 **“重新分配** 人员选取器”字段预填充名称的位置，以便将任务重新分配给预期用户。
1. 删除不正确的用户名。
1. 根据映像方案选择预期用户、用户 B (Mona) 和用户 C (Robin) 。
1. 选择“**完成**”。
1. 选择“**分配**”。 分配后，信息将发送到机器人。
   机器人更新自适应卡片并通知预期用户。

下图显示了重新分配方案：

![移动版上的人员选取器](../../assets/images/cards/mobilepp.gif)

---

## <a name="implement-people-picker"></a>实现人员选取器

人员选取器作为 [Input.ChoiceSet 控件](https://adaptivecards.io/explorer/Input.ChoiceSet.html) 的扩展实现。 输入控件包括以下选择：

* 下拉列表，例如展开的选择。
* 单选按钮，例如单个选择。
* 复选框，例如多个选择。  

> [!NOTE]
> 控件 `Input.ChoiceSet` 基于属性 `style` 和 `isMultiSelect` 属性。  

### <a name="update-schema"></a>更新架构

以下属性是架构的 `Input.ChoiceSet` 补充，用于在卡片上启用人员选取器体验：  

#### <a name="inputchoiceset-control"></a>Input.ChoiceSet 控件

|属性 |类型 |必需 |说明 |
|----|----|----|----|
|**choices.data** |**Data.Query** |否 |通过从指定的数据集提取结果，为不同的用户类型启用动态自动完成。 |

#### <a name="dataquery"></a>Data.Query

|属性 |类型 |必需 |说明|
|--|--|--|--|
|**数据** |字符串 |是 |必须动态提取的数据类型。|

#### <a name="dataset"></a>数据

下表为人员选取器提供预定义的值作为 **数据集** ：

|数据|搜索范围
|--|--|
|**graph.microsoft.com/users** |搜索整个组织中的所有成员。|
|**graph.microsoft.com/users?scope=currentContext** |在当前对话的成员中进行搜索，例如聊天或发送特定卡片的频道。|

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

下图演示了使用组织搜索的自适应卡片中的人员选取器：

:::image type="content" source="../../assets/images/Cards/peoplepicker-org-search.png" alt-text="人员选取器组织搜索":::

若要在聊天成员列表中启用搜索，请使用数据集表中定义的相应 [数据集](#dataset) 。 `isMultiSelect` 属性用于启用在控件中选择多个用户。 默认情况下，该设置设置为 false，此设置允许仅选择单个用户。

### <a name="data-submission"></a>数据提交

可以使用 `Action.Submit` 或 `Action.Execute` 将所选数据提交到机器人。 机器人上收到的`invoke`有效负载是静态列表中提供的Microsoft Azure Active Directory (Azure AD) ID 或 ID 列表。
在人员选取器中，当在控件中选择用户时， `Azure AD ID` 用户的值是发回的值。 它是 `Azure AD ID` 一个字符串，唯一标识目录中的用户。

提交给机器人的值的格式取决于属性的 `isMultiSelect` 值：

|值 `isMultiSelect`|格式|
|--|--|
|false _(单选)_|<selected_Azure_AD_ID>|
|true _(多选)_|<selected_Azure_AD_ID_1>，<selected_Azure_AD_ID_2>，<selected_Azure_AD_ID_3>|  

使用“ `Azure AD ID`人员选取器”预选相应的用户。

## <a name="preselection-of-user"></a>用户预选

人员选取器支持在创建和发送自适应卡片时预选控件中的用户。 `Input.ChoiceSet``value`支持用于预选用户的属性。 此 `value` 属性的格式与 [数据提交](#data-submission)中提交的值格式相同。  
以下列表提供预选用户的信息：

* 对于控件中的单个用户，请将 `Azure AD ID` 用户指定为 `value`该用户。
* 对于多个用户（例如`isMultiSelect``true`，指定逗号分隔的 `Azure AD ID`s 字符串）。  

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
   "value": "<Azure AD ID 1>"
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
   "value": "<Azure AD ID 1>,<Azure AD ID 2>,<Azure AD ID 3>"
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

## <a name="static-choices"></a>静态选项

静态选项支持必须将自定义配置文件插入预定义数据集的方案。 `Input.ChoiceSet` 支持在 json 中静态指定 `choices` 。 静态选项用于创建用户可从中选择的选项。

> [!NOTE]
> 静态 `choices` 与动态数据集一起使用。

选择包括 `title` 和 `value`。 与人员选取器一起使用时，这些选项将转换为具有 `title` 名称和标识符的 `value` 用户配置文件。 当搜索查询与给定的 `title`配置文件匹配时，这些自定义配置文件也是搜索结果的一部分。
以下示例描述静态选项：

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

下图演示了自适应卡片中具有组织搜索中静态选项的人员选取器：

:::image type="content" source="../../assets/images/Cards/peoplepicker-static-choice.png" alt-text="people-picker-static-choice":::

可在不同的方案中实现人员选取器，以便高效地管理任务。  

## <a name="code-sample"></a>代码示例

| 示例名称           | Description | C#    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|自适应卡片中的人员选取器控件| 此示例演示如何在自适应卡片中使用人员选取器控件。|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-people-picker-adaptive-card/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-people-picker-adaptive-card/nodejs) |

## <a name="see-also"></a>另请参阅

[卡片参考](cards-reference.md)
