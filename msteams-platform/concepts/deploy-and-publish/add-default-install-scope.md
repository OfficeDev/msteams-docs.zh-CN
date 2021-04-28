---
title: 为应用配置默认安装选项
description: 介绍如何指定应用的默认安装选项。
ms.topic: how-to
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 0afcce50a4779421016c23c4ec4e3d25cc3401d1
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058612"
---
# <a name="add-a-default-install-scope-and-group-capability"></a><span data-ttu-id="275d4-103">添加默认安装范围和组功能</span><span class="sxs-lookup"><span data-stu-id="275d4-103">Add a default install scope and group capability</span></span>

<span data-ttu-id="275d4-104">应用通常支持 Teams 中的多个方案，但你在设计时可能记住了特定的范围和功能。</span><span class="sxs-lookup"><span data-stu-id="275d4-104">It’s common for an app to support multiple scenarios in Teams, but you may have designed it with a specific scope and capability in mind.</span></span> <span data-ttu-id="275d4-105">例如，如果你的应用主要用于团队或频道，你可以确保用户在应用商店中看到的第一个安装选项是添加到 **团队**。</span><span class="sxs-lookup"><span data-stu-id="275d4-105">For example, if your app is primarily for team or channel use, you can make sure that the first install option users see in the store is **Add to a team**.</span></span>

![添加应用](../../assets/images/compose-extensions/addanapp.png)

<span data-ttu-id="275d4-107">如果你的应用的主要功能是自动程序，则还可以在用户将应用安装到团队时使机器人成为默认功能。</span><span class="sxs-lookup"><span data-stu-id="275d4-107">If your app's primary capability is a bot, you can also make the bot the default capability when a user installs your app to a team.</span></span>

## <a name="configure-your-apps-default-install-scope"></a><span data-ttu-id="275d4-108">配置应用的默认安装作用域</span><span class="sxs-lookup"><span data-stu-id="275d4-108">Configure your app's default install scope</span></span>

<span data-ttu-id="275d4-109">为应用配置默认安装范围。</span><span class="sxs-lookup"><span data-stu-id="275d4-109">Configure the default install scope for your app.</span></span> <span data-ttu-id="275d4-110">一次只能设置一个范围。</span><span class="sxs-lookup"><span data-stu-id="275d4-110">You can set only one scope at a time.</span></span>

<span data-ttu-id="275d4-111">**在应用清单中配置默认安装作用域**</span><span class="sxs-lookup"><span data-stu-id="275d4-111">**To configure the default install scope in your app manifest**</span></span>

1. <span data-ttu-id="275d4-112">打开应用清单并添加 `defaultInstallScope` 属性。</span><span class="sxs-lookup"><span data-stu-id="275d4-112">Open your app manifest and add the `defaultInstallScope` property.</span></span>
2. <span data-ttu-id="275d4-113">将默认安装范围值设置为 `personal` `team` `groupchat` 、、、 或 `meetings` 。</span><span class="sxs-lookup"><span data-stu-id="275d4-113">Set default install scope value as, either `personal`, `team`, `groupchat`, or `meetings`.</span></span>

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> <span data-ttu-id="275d4-114">有关详细信息，请参阅应用 [清单架构](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="275d4-114">For more information, see the [app manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="configure-the-default-capability-for-shared-scopes"></a><span data-ttu-id="275d4-115">配置共享范围的默认功能</span><span class="sxs-lookup"><span data-stu-id="275d4-115">Configure the default capability for shared scopes</span></span>

<span data-ttu-id="275d4-116">为团队、会议或群聊安装应用时配置默认功能。</span><span class="sxs-lookup"><span data-stu-id="275d4-116">Configure the default capability when your app is installed for a team, meeting, or groupchat.</span></span>

> [!NOTE]
> <span data-ttu-id="275d4-117">`defaultGroupCapability` 提供将添加到团队、群聊或会议的默认功能。</span><span class="sxs-lookup"><span data-stu-id="275d4-117">`defaultGroupCapability` provides the default capability that will be added to the team, groupchat, or meeting.</span></span> <span data-ttu-id="275d4-118">选择选项卡、机器人或连接器作为应用的默认功能，但必须确保你在应用定义中提供了所选功能。</span><span class="sxs-lookup"><span data-stu-id="275d4-118">Select a tab, bot, or connector as the default capability for your app, but you must ensure that you have provided the selected capability in your app definition.</span></span>

<span data-ttu-id="275d4-119">**在应用清单中配置详细信息**</span><span class="sxs-lookup"><span data-stu-id="275d4-119">**To configure details in app manifest**</span></span>

1. <span data-ttu-id="275d4-120">打开应用清单，并添加 `defaultGroupCapability` 属性。</span><span class="sxs-lookup"><span data-stu-id="275d4-120">Open your app manifest and add the `defaultGroupCapability` property to it.</span></span>
2. <span data-ttu-id="275d4-121">设置 、 `team` `groupchat` 或 的值 `meetings` 。</span><span class="sxs-lookup"><span data-stu-id="275d4-121">Set a value of `team`, `groupchat`, or `meetings`.</span></span>
3. <span data-ttu-id="275d4-122">对于选定的组功能，可用的组功能是、 、 `bot` `tab` 或 `connector` 。</span><span class="sxs-lookup"><span data-stu-id="275d4-122">For the selected group capability, the available group capabilities are, `bot`, `tab`, or `connector`.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="275d4-123">只能为选定的组功能选择一个默认功能 、 `bot` `tab` 或 `connector` 。</span><span class="sxs-lookup"><span data-stu-id="275d4-123">You can select only one default capability, `bot`, `tab`, or `connector` for the selected group capability.</span></span>

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```

> [!NOTE]
> <span data-ttu-id="275d4-124">有关详细信息，请参阅应用 [清单架构](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="275d4-124">For more information, see the [app manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="275d4-125">后续步骤</span><span class="sxs-lookup"><span data-stu-id="275d4-125">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="275d4-126">选择如何发布应用程序</span><span class="sxs-lookup"><span data-stu-id="275d4-126">Choose how to distribute your app</span></span>](overview.md)
