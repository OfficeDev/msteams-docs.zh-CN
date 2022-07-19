---
title: 集成人员选取器
description: 本文介绍如何使用 Teams JavaScript 客户端 SDK 集成人员选取器控制和使用人员选取器的优势。
ms.topic: conceptual
ms.localizationpriority: high
ms.author: surbhigupta
ms.openlocfilehash: 5a45f2c3a7d098bfe95b55620fb5909fb33e3472
ms.sourcegitcommit: 79d525c0be309200e930cdd942bc2c753d0b718c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2022
ms.locfileid: "66842001"
---
# <a name="integrate-people-picker"></a>集成人员选取器

“人员选取器”是 Teams 中的输入控件，允许用户搜索和选择人员。 你可以在 Web 应用中集成终端用户可以执行不同功能的“人员选取器”输入控件，例如在聊天、频道或 Teams 内的整个组织中搜索和选择人员。 “人员选取器”控件可用于所有 Teams 客户端，例如 Web、桌面和移动设备。

可以使用 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)，它提供 `selectPeople` API 以在 Web 应用中集成“人员选取器”输入控件。

## <a name="advantages-of-using-people-picker"></a>使用“人员选取器”的优点

* 在所有 Teams 功能上运行，例如任务模块、聊天、频道、会议选项卡和个人应用。
* 允许用户在 Teams 中搜索和选择聊天、频道或整个组织中的人员。
* 在涉及任务分配、标记和通知用户的方案中提供帮助。
* 与建立任何类似的控制相比，节省了大量时间和精力。

若要在 Teams 应用中集成“人员选取器”输入控件，请使用 [`selectPeople`](#selectpeople-api) API。 若要集成和调用 API，则必须充分了解随附的 [代码片段](#code-snippet)。 还需要熟悉 [API 响应错误](#error-handling)。

## <a name="selectpeople-api"></a>`selectPeople` API

`selectPeople` API 使你能够将 Teams 人员选取器输入控制添加到 Web 应用中，还可帮助你执行以下操作:

* 允许用户搜索并从列表中选择一个或多个人员。
* 将所选用户的 ID、名称和电子邮件地址返回到 Web 应用。

在个人应用中，控件会在 Teams 中搜索整个组织的名称或电子邮件 ID。 如果将应用添加到聊天或频道中，则根据方案配置搜索上下文。 搜索受限于该聊天或频道的成员。

`selectPeople` API 附带以下输入配置:

|配置参数|类型|说明| 默认值|
|-----|------|--------------|------|
|`title`|String| 它是一个可选参数，用于设置人员选取器控件的标题。|`selectPeople`|
|`setSelected`|String| 它是一个可选参数。 必须传递要预选人员的 Microsoft Azure Active Directory (Azure AD) ID。 此参数在启动人员选取器输入控件时预先选择人员。 在单一选择的情况下，仅预先填充第一个有效用户，而忽略其余用户。|**Null**|
|`openOrgWideSearchInChatOrChannel`|Boolean| 它是一个可选参数，如果设置为 TRUE，则即使应用已添加到聊天或频道中，它也会在组织范围内启动“人员选取器”。|**False**|
|`singleSelect`|布尔|它是一个可选参数，如果设置为 TRUE，则它将启动“人员选取器“并将所选内容限制为仅一个用户。|**False**|

下图显示了在移动设备和桌面版上的“人员选取器”体验:

# <a name="mobile"></a>[移动设备](#tab/Samplemobileapp)

“人员选取器”输入控件允许用户使用以下步骤搜索和添加人员:

1. 键入所需人员的姓名。 列表中显示名称建议。
1. 从列表中选择所需人员的姓名。

   :::image type="content" source="../../assets/images/tabs/people-picker-control-capability-mobile-updated.png" alt-text="选取器选取器移动":::

# <a name="desktop"></a>[桌面设备](#tab/Sampledesktop)

Web 或桌面上的“人员选取器”控件在 Web 应用顶部的模式窗口中启动，若要添加人员，请使用以下步骤:

1. 键入所需人员的姓名。 列表中显示名称建议。
1. 从列表中选择所需人员的姓名。

   :::image type="content" source="../../assets/images/tabs/select-people-picker-byname.png" alt-text="按名称桌面人员选取器":::

---

## <a name="code-snippet"></a>代码片段

以下代码片段显示列表中 `selectPeople` API 人员的使用:

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```javascript
people.selectPeople({ setSelected: ["aad id"], openOrgWideSearchInChatOrChannel: true, singleSelect: false, title: true}).then(people) => 
 {
    output(" People length: " + people.length + " " + JSON.stringify(people));
 }).catch((error) => { /*Unsuccessful operation*/ });
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```javascript
people.selectPeople((error: microsoftTeams.SdkError, people: microsoftTeams.people.PeoplePickerResult[]) => 
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
  },{ setSelected: ["aad id"], openOrgWideSearchInChatOrChannel: true, singleSelect: false, title: true});
```

***

## <a name="error-handling"></a>错误处理

下表列出了错误代码及其说明:

|错误代码 |  错误名称     | 说明|
| --------- | --------------- | --------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | 当前平台不支持 API。|
| **500** | INTERNAL_ERROR | 启动人员选取器时遇到的内部错误。|
| **4000** | INVALID_ARGUMENTS | 调用 API 时的强制性参数错误或不足。|
| **8000** | USER_ABORT |用户取消了该操作。|
| **9000** | OLD_PLATFORM | 用户位于无法实现 API 的旧平台内部版本上。 升级到最新版本的内部版本以解决此问题。|

## <a name="see-also"></a>另请参阅

* [集成媒体功能](~/concepts/device-capabilities/media-capabilities.md)
* [在 Teams 中集成 QR 代码或条形码扫描程序功能](qr-barcode-scanner-capability.md)
* [在 Teams 中集成位置功能](location-capability.md)
