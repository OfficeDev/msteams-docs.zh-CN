---
title: 重新排序 "个人应用程序" 选项卡
description: 如何对个人应用程序中的个人应用静态选项卡重新排序
keywords: 团队选项卡开发
ms.openlocfilehash: a8a7c3d23bac98ef1085a8f3443ca0fc92ae0a31
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2020
ms.locfileid: "49554825"
---
# <a name="reorder-personal-app-tabs"></a>重新排序 "个人应用程序" 选项卡

从清单版本1.7 开始，开发人员可以重新排列其个人应用程序中的所有选项卡。 特别是，开发人员可以将 "机器人聊天" 选项卡 (，该选项卡始终默认为 "个人应用程序" 选项卡标题中任何位置的第一个位置) 。 我们声明了两个保留的 tab entityId 关键字： "对话" 和 "关于"。

## <a name="moving-the-chatconversation-tab"></a>移动 "聊天/对话" 选项卡

如果您创建一个具有 "个人" 范围的 bot，它将始终显示在个人应用的第一个选项卡位置中。 如果要将其移动到其他位置，则需要使用保留关键字 "对话" 将静态 tab 对象添加到清单中。 无论您是在 "staticTabs" 数组中的什么位置添加 "对话" 选项卡，都将在 web 和桌面上显示对话选项卡。 

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```

> [!NOTE]
> 请注意，由于个人 bot 聊天已在个人应用中具有专用空间，因此此行为不会反映在移动设备上。

## <a name="moving-the-about-tab"></a>移动 "关于" 选项卡

"关于" 选项卡始终默认为个人应用程序选项卡标题栏的末尾。 如果要将其移动到其他位置，则需要使用 "关于" entityId。

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"about",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```
> [!NOTE]
> 请注意，移动设备上不显示 "关于" 选项卡。

## <a name="example-code"></a>示例代码

```json
{
   "staticTabs":[
      {
         "entityId":"homeTab",
         "name":"Home",
         "contentUrl":"https://www.contoso.com",
         "websiteUrl":" https://www.contoso.com ",
         "scopes":[
            "personal"
         ]
      },
      {
         "entityId":"about",
         "scopes":[
            "personal"
         ]
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```
