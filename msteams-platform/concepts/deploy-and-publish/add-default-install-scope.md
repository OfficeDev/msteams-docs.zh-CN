---
title: 为应用配置默认安装选项
description: 介绍如何指定应用的默认安装选项。
ms.topic: how-to
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: a4b70df70c7b9442e29953dae8a8c4e892cb72c1
ms.sourcegitcommit: 7b4f383b506d4bc68a1b5641d6e0f404edbfbc6d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2021
ms.locfileid: "51946486"
---
# <a name="add-a-default-install-scope-and-group-capability"></a><span data-ttu-id="0bd46-103">添加默认安装范围和组功能</span><span class="sxs-lookup"><span data-stu-id="0bd46-103">Add a default install scope and group capability</span></span>

<span data-ttu-id="0bd46-104">应用通常支持 Teams 中的多个方案，但你在设计时可能记住了特定的范围和功能。</span><span class="sxs-lookup"><span data-stu-id="0bd46-104">It’s common for an app to support multiple scenarios in Teams, but you may have designed it with a specific scope and capability in mind.</span></span> <span data-ttu-id="0bd46-105">例如，如果你的应用主要用于团队或频道，你可以确保用户在应用商店中看到的第一个安装选项是添加到 **团队**。</span><span class="sxs-lookup"><span data-stu-id="0bd46-105">For example, if your app is primarily for team or channel use, you can make sure that the first install option users see in the store is **Add to a team**.</span></span>

![添加应用](../../assets/images/compose-extensions/addanapp.png)

<span data-ttu-id="0bd46-107">如果你的应用的主要功能是自动程序，则还可以在用户将应用安装到团队时使机器人成为默认功能。</span><span class="sxs-lookup"><span data-stu-id="0bd46-107">If your app's primary capability is a bot, you can also make the bot the default capability when a user installs your app to a team.</span></span> 

## <a name="configure-your-apps-default-install-scope"></a><span data-ttu-id="0bd46-108">配置应用的默认安装作用域</span><span class="sxs-lookup"><span data-stu-id="0bd46-108">Configure your app's default install scope</span></span>

<span data-ttu-id="0bd46-109">为应用配置默认安装范围。</span><span class="sxs-lookup"><span data-stu-id="0bd46-109">Configure the default install scope for your app.</span></span> <span data-ttu-id="0bd46-110">一次只能设置一个范围。</span><span class="sxs-lookup"><span data-stu-id="0bd46-110">You can set only one scope at a time.</span></span>

<span data-ttu-id="0bd46-111">**在应用清单中配置默认安装作用域**</span><span class="sxs-lookup"><span data-stu-id="0bd46-111">**To configure the default install scope in your app manifest**</span></span>

1. <span data-ttu-id="0bd46-112">打开应用清单并添加 `defaultInstallScope` 属性。</span><span class="sxs-lookup"><span data-stu-id="0bd46-112">Open your app manifest and add the `defaultInstallScope` property.</span></span>
2. <span data-ttu-id="0bd46-113">设置 、 `personal` `team` 、 `groupchat` 或 `meetings` 值 (请参阅下面的示例) 。</span><span class="sxs-lookup"><span data-stu-id="0bd46-113">Set a value of `personal`, `team`, `groupchat`, or `meetings` (see an example below).</span></span>

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> <span data-ttu-id="0bd46-114">有关详细信息，请参阅应用 [清单架构](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="0bd46-114">For more information, see the [app manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="configure-the-default-capability-for-shared-scopes"></a><span data-ttu-id="0bd46-115">配置共享范围的默认功能</span><span class="sxs-lookup"><span data-stu-id="0bd46-115">Configure the default capability for shared scopes</span></span>

<span data-ttu-id="0bd46-116">为团队、会议或聊天安装应用时配置默认功能。</span><span class="sxs-lookup"><span data-stu-id="0bd46-116">Configure the default capability when your app is installed for a team, meeting, or chat.</span></span>

<span data-ttu-id="0bd46-117">**在应用清单中配置详细信息**</span><span class="sxs-lookup"><span data-stu-id="0bd46-117">**To configure details in app manifest**</span></span>

1. <span data-ttu-id="0bd46-118">打开应用清单，并添加 `defaultGroupCapability` 属性。</span><span class="sxs-lookup"><span data-stu-id="0bd46-118">Open your app manifest and add the `defaultGroupCapability` property to it.</span></span>
2. <span data-ttu-id="0bd46-119">保存更新。</span><span class="sxs-lookup"><span data-stu-id="0bd46-119">Save the updates.</span></span>

    <span data-ttu-id="0bd46-120">下面是一个 JSON 示例：</span><span class="sxs-lookup"><span data-stu-id="0bd46-120">Following is a JSON example:</span></span>

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```
> [!NOTE]
> <span data-ttu-id="0bd46-121">有关完整架构的信息，请参阅 [清单架构](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="0bd46-121">For information on full schema, see [manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="0bd46-122">后续步骤</span><span class="sxs-lookup"><span data-stu-id="0bd46-122">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0bd46-123">选择如何发布应用程序</span><span class="sxs-lookup"><span data-stu-id="0bd46-123">Choose how to distribute your app</span></span>](overview.md)
