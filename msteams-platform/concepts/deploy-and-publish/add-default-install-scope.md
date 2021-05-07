---
title: 为应用配置默认安装选项
description: 介绍如何指定应用的默认安装选项。
ms.topic: how-to
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 561a4f2910e703db5ffce6176f6177dfd661d2ce
ms.sourcegitcommit: 60561c7cd189c9d6fa5e09e0f2b6c24476f2dff5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2021
ms.locfileid: "52230930"
---
# <a name="configure-default-install-options-for-your-microsoft-teams-app"></a><span data-ttu-id="ac67d-103">配置应用的默认安装Microsoft Teams选项</span><span class="sxs-lookup"><span data-stu-id="ac67d-103">Configure default install options for your Microsoft Teams app</span></span>

<span data-ttu-id="ac67d-104">应用通常支持 Teams 中的多个方案，但你在设计时可能记住了特定的范围和功能。</span><span class="sxs-lookup"><span data-stu-id="ac67d-104">It’s common for an app to support multiple scenarios in Teams, but you may have designed it with a specific scope and capability in mind.</span></span> <span data-ttu-id="ac67d-105">例如，如果你的应用主要用于团队或频道，你可以确保用户在应用商店中看到的第一个安装选项是添加到 **团队**。</span><span class="sxs-lookup"><span data-stu-id="ac67d-105">For example, if your app is primarily for team or channel use, you can make sure that the first install option users see in the store is **Add to a team**.</span></span>

:::row:::
   :::column span="2":::

![添加应用下拉列表示例](../../assets/images/compose-extensions/addanapp.png)

   :::column-end:::
   :::column span="2":::
   :::column-end:::
:::row-end:::

<span data-ttu-id="ac67d-107">如果你的应用的主要功能是自动程序，则还可以在用户将应用安装到团队时使机器人成为默认功能。</span><span class="sxs-lookup"><span data-stu-id="ac67d-107">If your app's primary capability is a bot, you can also make the bot the default capability when a user installs your app to a team.</span></span>

## <a name="configure-your-apps-default-install-scope"></a><span data-ttu-id="ac67d-108">配置应用的默认安装作用域</span><span class="sxs-lookup"><span data-stu-id="ac67d-108">Configure your app's default install scope</span></span>

<span data-ttu-id="ac67d-109">为应用配置默认安装范围。</span><span class="sxs-lookup"><span data-stu-id="ac67d-109">Configure the default install scope for your app.</span></span> <span data-ttu-id="ac67d-110">一次只能设置一个范围。</span><span class="sxs-lookup"><span data-stu-id="ac67d-110">You can set only one scope at a time.</span></span>

<span data-ttu-id="ac67d-111">**在应用清单中配置默认安装作用域**</span><span class="sxs-lookup"><span data-stu-id="ac67d-111">**To configure the default install scope in your app manifest**</span></span>

1. <span data-ttu-id="ac67d-112">打开应用清单并添加 `defaultInstallScope` 属性。</span><span class="sxs-lookup"><span data-stu-id="ac67d-112">Open your app manifest and add the `defaultInstallScope` property.</span></span>
2. <span data-ttu-id="ac67d-113">将默认安装范围值设置为 `personal` `team` `groupchat` 、、、 或 `meetings` 。</span><span class="sxs-lookup"><span data-stu-id="ac67d-113">Set default install scope value as, either `personal`, `team`, `groupchat`, or `meetings`.</span></span>

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> <span data-ttu-id="ac67d-114">有关详细信息，请参阅应用 [清单架构](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="ac67d-114">For more information, see the [app manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="configure-the-default-capability-for-shared-scopes"></a><span data-ttu-id="ac67d-115">配置共享范围的默认功能</span><span class="sxs-lookup"><span data-stu-id="ac67d-115">Configure the default capability for shared scopes</span></span>

<span data-ttu-id="ac67d-116">为团队、会议或群聊安装应用时配置默认功能。</span><span class="sxs-lookup"><span data-stu-id="ac67d-116">Configure the default capability when your app is installed for a team, meeting, or groupchat.</span></span>

> [!NOTE]
> <span data-ttu-id="ac67d-117">`defaultGroupCapability` 提供将添加到团队、群聊或会议的默认功能。</span><span class="sxs-lookup"><span data-stu-id="ac67d-117">`defaultGroupCapability` provides the default capability that will be added to the team, groupchat, or meeting.</span></span> <span data-ttu-id="ac67d-118">选择选项卡、机器人或连接器作为应用的默认功能，但必须确保你在应用定义中提供了所选功能。</span><span class="sxs-lookup"><span data-stu-id="ac67d-118">Select a tab, bot, or connector as the default capability for your app, but you must ensure that you have provided the selected capability in your app definition.</span></span>

<span data-ttu-id="ac67d-119">**在应用清单中配置详细信息**</span><span class="sxs-lookup"><span data-stu-id="ac67d-119">**To configure details in app manifest**</span></span>

1. <span data-ttu-id="ac67d-120">打开应用清单，并添加 `defaultGroupCapability` 属性。</span><span class="sxs-lookup"><span data-stu-id="ac67d-120">Open your app manifest and add the `defaultGroupCapability` property to it.</span></span>
2. <span data-ttu-id="ac67d-121">设置 、 `team` `groupchat` 或 的值 `meetings` 。</span><span class="sxs-lookup"><span data-stu-id="ac67d-121">Set a value of `team`, `groupchat`, or `meetings`.</span></span>
3. <span data-ttu-id="ac67d-122">对于选定的组功能，可用的组功能是、 、 `bot` `tab` 或 `connector` 。</span><span class="sxs-lookup"><span data-stu-id="ac67d-122">For the selected group capability, the available group capabilities are, `bot`, `tab`, or `connector`.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="ac67d-123">只能为选定的组功能选择一个默认功能 、 `bot` `tab` 或 `connector` 。</span><span class="sxs-lookup"><span data-stu-id="ac67d-123">You can select only one default capability, `bot`, `tab`, or `connector` for the selected group capability.</span></span>

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```

> [!NOTE]
> <span data-ttu-id="ac67d-124">有关详细信息，请参阅应用 [清单架构](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="ac67d-124">For more information, see the [app manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="ac67d-125">后续步骤</span><span class="sxs-lookup"><span data-stu-id="ac67d-125">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ac67d-126">创建应用包</span><span class="sxs-lookup"><span data-stu-id="ac67d-126">Create your app package</span></span>](~/concepts/build-and-test/apps-package.md)
