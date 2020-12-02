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
# <a name="reorder-personal-app-tabs"></a><span data-ttu-id="ce796-104">重新排序 "个人应用程序" 选项卡</span><span class="sxs-lookup"><span data-stu-id="ce796-104">Reorder personal app tabs</span></span>

<span data-ttu-id="ce796-105">从清单版本1.7 开始，开发人员可以重新排列其个人应用程序中的所有选项卡。</span><span class="sxs-lookup"><span data-stu-id="ce796-105">Starting with manifest version 1.7 developers can rearrange all tabs in their personal app.</span></span> <span data-ttu-id="ce796-106">特别是，开发人员可以将 "机器人聊天" 选项卡 (，该选项卡始终默认为 "个人应用程序" 选项卡标题中任何位置的第一个位置) 。</span><span class="sxs-lookup"><span data-stu-id="ce796-106">In particular, a developer can move the “bot chat” tab (which has always defaulted to the first position) anywhere in the personal app tab header.</span></span> <span data-ttu-id="ce796-107">我们声明了两个保留的 tab entityId 关键字： "对话" 和 "关于"。</span><span class="sxs-lookup"><span data-stu-id="ce796-107">We’ve declared two reserved tab entityId keywords: “conversations” and “about”.</span></span>

## <a name="moving-the-chatconversation-tab"></a><span data-ttu-id="ce796-108">移动 "聊天/对话" 选项卡</span><span class="sxs-lookup"><span data-stu-id="ce796-108">Moving the “Chat/Conversation” tab</span></span>

<span data-ttu-id="ce796-109">如果您创建一个具有 "个人" 范围的 bot，它将始终显示在个人应用的第一个选项卡位置中。</span><span class="sxs-lookup"><span data-stu-id="ce796-109">If you create a bot with a “personal” scope, it will always show up in the first tab position in a personal app.</span></span> <span data-ttu-id="ce796-110">如果要将其移动到其他位置，则需要使用保留关键字 "对话" 将静态 tab 对象添加到清单中。</span><span class="sxs-lookup"><span data-stu-id="ce796-110">If you wish to move it to another position, you need to add a static tab object to your manifest with the reserved keyword “conversations”.</span></span> <span data-ttu-id="ce796-111">无论您是在 "staticTabs" 数组中的什么位置添加 "对话" 选项卡，都将在 web 和桌面上显示对话选项卡。</span><span class="sxs-lookup"><span data-stu-id="ce796-111">Wherever you add the “conversations” tab in the “staticTabs” array, that’s where the conversation tab will appear on web and desktop.</span></span> 

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
> <span data-ttu-id="ce796-112">请注意，由于个人 bot 聊天已在个人应用中具有专用空间，因此此行为不会反映在移动设备上。</span><span class="sxs-lookup"><span data-stu-id="ce796-112">Note that this behavior is not reflected on mobile since the personal bot chat already has a dedicated place within the personal app.</span></span>

## <a name="moving-the-about-tab"></a><span data-ttu-id="ce796-113">移动 "关于" 选项卡</span><span class="sxs-lookup"><span data-stu-id="ce796-113">Moving the “About” tab</span></span>

<span data-ttu-id="ce796-114">"关于" 选项卡始终默认为个人应用程序选项卡标题栏的末尾。</span><span class="sxs-lookup"><span data-stu-id="ce796-114">The “About” tab always defaults to the end of the personal app tab header bar.</span></span> <span data-ttu-id="ce796-115">如果要将其移动到其他位置，则需要使用 "关于" entityId。</span><span class="sxs-lookup"><span data-stu-id="ce796-115">If you wish to move it to another position, you need to use the “about” entityId.</span></span>

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
> <span data-ttu-id="ce796-116">请注意，移动设备上不显示 "关于" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="ce796-116">Note that the about tab is not shown on mobile.</span></span>

## <a name="example-code"></a><span data-ttu-id="ce796-117">示例代码</span><span class="sxs-lookup"><span data-stu-id="ce796-117">Example code</span></span>

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
