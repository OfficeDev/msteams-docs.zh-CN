---
title: 集成人员选取器功能
author: Rajeshwari-v
description: 如何使用 JavaScript Teams SDK 集成人员选取器功能
keywords: 人员选取器控件
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 1d8840853c6fce808b1ec5f13ad95c099698de3ebb37f3613a14c64b4a11d3f8
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2021
ms.locfileid: "57702780"
---
# <a name="integrate-people-picker-capability"></a>集成人员选取器功能 

人员选取器是一个控件，用于搜索和选择人员。 这是一项可在平台中Teams功能。 你可以将本机Teams器输入控件与 Web 应用集成。 您可以在单选或多选和配置之间选择，例如限制聊天、频道或整个组织的搜索。

可以使用[JavaScript Microsoft Teams SDK，](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)它提供 API 以将人员 `selectPeople` 选取器功能集成到 Web 应用中。 

## <a name="advantages-of-integrating-people-picker-capability"></a>集成人员选取器功能的优点

* 人员选取器控件适用于所有Teams图面，如任务模块、聊天、频道、会议选项卡和个人应用。
* 此控件允许你在聊天、频道或整个组织中搜索和选择用户。
*  人员选取器功能可帮助处理涉及任务分配、标记和通知用户的方案。 
* 可以在 Web 应用中使用此现成的控件。 它可显著节省自己构建此类控件的工作和时间。

你必须调用 `selectPeople` API 以将人员选取器控件集成到Teams应用中。 为了进行有效的集成，你必须了解 [用于](#code-snippet) 调用 API 的代码段。 熟悉 API 响应错误以处理 [Web](#error-handling) 应用中的错误非常重要。

> [!NOTE] 
> 目前Microsoft Teams对人员选取器功能的支持仅适用于移动客户端。

## <a name="selectpeople-api"></a>`selectPeople` API 

`selectPeople`API 使你能够将Teams添加到 Web `People Picker input control` 应用中。  
API 说明如下：

| API      | 说明  |
| --- | --- |
|**selectPeople**|启动人员选取器，并允许用户从列表中搜索和选择一个或多个人员。<br/><br/>此 API 将所选用户的 ID、名称和电子邮件地址返回到调用 Web 应用。<br/><br/>对于个人应用，控件将在整个组织中进行搜索。 如果将应用添加到聊天或频道，则根据方案配置搜索上下文。 搜索仅限于该聊天、频道的成员，或在整个组织中可用。|

`selectPeople`API 附带以下输入配置：

|配置参数|类型|说明| 默认值|
|-----|------|--------------|------|
|`title`| String| 它是可选参数。 它设置人员选取器控件的标题。 | 选择人员|
|`setSelected`|String| 它是可选参数。 必须传递要预先选择的人的 AAD ID。 此参数在启动人员选取器控件时预选人员。 在单选的情况下，只会预填充第一个有效用户，忽略其余用户。 |NULL| 
|`openOrgWideSearchInChatOrChannel`|Boolean | 它是可选参数。 设置为 true 时，它将在组织范围内启动人员选取器，即使该应用已添加到聊天或频道也是如此。 |错误|
|`singleSelect`|Boolean|它是可选参数。 设置为 true 时，它会启动人员选取器，将选择限制为仅一个用户。 |错误|

下图描述了示例 Web 应用中人员选取器功能的体验：

![人员选取器功能 Web 应用体验](../../assets/images/tabs/people-picker-control-capability.png)

### <a name="code-snippet"></a>代码段

**呼叫 `selectPeople` 用于** 从列表中选择人的 API：

```javascript
 microsoftTeams.people.selectPeople((error: microsoftTeams.SdkError, people: microsoftTeams.people.PeoplePickerResult[]) => 
 {
    if (error) 
    {
        if (error.message) 
           {
             alert(" ErrorCode: " + error.errorCode + error.message);
           }
            else 
            {
              alert(" ErrorCode: " + error.errorCode);
            }
      }
    if (people)
     {
            output(" People length: " + people.length + " " + JSON.stringify(people));
      }
  });
```

## <a name="error-handling"></a>错误处理

必须确保在 Web 应用中正确处理错误。 下表列出了错误代码以及生成错误的条件： 

|错误代码 |  错误名称     | 条件|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API 在当前平台上不受支持。|
| **500** | INTERNAL_ERROR | 启动人员选取器时遇到内部错误。|
| **4000** | INVALID_ARGUMENTS | 使用错误或不足的强制参数调用 API。|
| **8000** | USER_ABORT |用户已取消操作。|
| **9000** | OLD_PLATFORM | 用户位于不存在 API 实现的旧平台版本上。  升级内部版本可解决此问题。|

## <a name="see-also"></a>另请参阅

* [将媒体功能集成到Teams](mobile-camera-image-permissions.md)
* [将 QR 代码或条形码扫描仪功能集成到 Teams](qr-barcode-scanner-capability.md)
* [在 Teams 中集成位置Teams](location-capability.md)
