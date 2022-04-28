---
title: Microsoft Teams 选项卡
author: surbhigupta
description: Teams 平台上的自定义选项卡概述
ms.localizationpriority: high
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 1ab927f11588d58a68249c1213e6eae17346ac8d
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103290"
---
# <a name="build-tabs-for-microsoft-teams"></a>构建 Microsoft Teams 选项卡

选项卡是 Teams 中嵌入的与 Microsoft Teams 相关的网页。 它们是简单的 HTML `<iframe\>` 标记，指向在应用清单中声明的域，并且可以添加为团队内部频道、群组聊天或个人用户的个人应用的一部分。 可在应用中包含自定义选项卡，以便在 Teams 中嵌入自己的 Web 内容，或将 Teams 特定的功能添加到 Web 内容。 有关详细信息，请参阅 [Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client)。

> [!IMPORTANT]
> 目前，自定义选项卡在政府社区云 (GCC)、GCC-High 和国防部 (DOD) 中可用。

下图显示了个人选项卡：

:::image type="content" source="../assets/images/tabs/personaltab.png" alt-text="个人选项卡" lightbox="../assets/images/tabs/personaltab.png":::

下图显示了 Contoso 频道选项卡：

:::image type="content" source="../assets/images/tabs/tabs.png" alt-text="频道或组选项卡" lightbox="../assets/images/tabs/tabs.png":::

在使用选项卡之前，必须先完成几个先决条件。

Teams 中提供了两种类型的选项卡：个人选项卡和频道或组选项卡。 [个人选项卡](~/tabs/how-to/create-personal-tab.md) 和个人范围的机器人一样，是个人应用的一部分，并且只作用于单个用户。 可以将它们固定到左侧导航栏以方便访问。 [通道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)将内容传递到频道和群组聊天，是围绕基于 Web 的专用内容创建协作空间的好方法。

你可以[创建内容页面](~/tabs/how-to/create-tab-pages/content-page.md)，将其作为个人选项卡、频道或组选项卡或任务模块的一部分。 可以 [创建配置页](~/tabs/how-to/create-tab-pages/configuration-page.md)，以支持用户能够配置 Microsoft Teams 应用，并使用它来配置频道或群组聊天选项卡、消息传递扩展或 Office 365 连接器。 你可以允许用户在安装后重新配置选项卡，并为应用程序[创建选项卡删除页](~/tabs/how-to/create-tab-pages/removal-page.md)。 生成包含选项卡的 Teams 应用时，必须在 Android 和 iOS Teams 客户端上测试[选项卡函数](~/tabs/design/tabs-mobile.md)。 选项卡必须通过基本信息、区域设置、主题信息，以及标识选项卡中的内容的 `entityId` 或 `subEntityId` 来[获取上下文](~/tabs/how-to/access-teams-context.md)。

你可以使用自适应卡片生成选项卡，并通过消除对机器人和选项卡的其他后端的需求来集中所有 Teams 应用功能。 [演示区域视图](~/tabs/tabs-link-unfurling.md) 是一个新的 UI 组件，可用于呈现在 Teams 中全屏打开的内容，并将其固定为选项卡。现有的 [link unfurling](~/tabs/tabs-link-unfurling.md) 服务已更新，以便使用自适应卡片和聊天服务将 URL 转换为选项卡。 可以使用对话子实体[创建对话选项卡](~/tabs/how-to/conversational-tabs.md)，这些子实体允许用户在选项卡中就子实体（如特定任务、患者、销售机会）进行对话，而不是讨论整个选项卡。可以更改[选项卡边距](~/resources/removing-tab-margins.md)以增强开发人员在生成应用时的体验。 可以拖动选项卡并将其放置在所需的位置，以交换个人应用和频道或群组聊天中的选项卡位置。

> [!NOTE]
> **帖子** 和 **文件** 无法从其位置移动。

## <a name="tab-features"></a>选项卡功能

选项卡功能如下所示：

* 如果向同样具有机器人的应用添加了选项卡，则机器人也会添加到团队中。
* 了解当前用户的 Microsoft Azure Active Directory (Azure AD) ID。
* 用户的区域设置感知，以指示 `en-us` 的语言。
* 单一登录 (SSO) 功能（如果支持）。
* 能够使用机器人或应用通知深入链接到选项卡或服务中的子实体，例如单个工作项。
* 从选项卡中的链接打开任务模块的功能。
* 在选项卡中重复使用 SharePoint Web 部件。

## <a name="tabs-user-scenarios"></a>选项卡用户方案

**Scenario：** 在 Teams 中引入现有的基于 Web 的资源。 \
**Example：** 在 Teams 应用中创建一个向用户显示信息性公司网站的个人选项卡。

**方案：** 向 Teams 机器人或消息扩展添加支持页面。 \
**Example：** 创建为用户提供“**关于**”和“**帮助**”的网页内容的个人选项卡。

**Scenario：** 为协作对话和协作提供对用户定期交互的项目的访问权限。 \
**Example：** 创建一个频道或组选项卡，其中包含各个项目的深层链接。

## <a name="understand-how-tabs-work"></a>了解选项卡的工作原理

可以使用以下方法之一创建选项卡：

* [在应用清单中删除自定义选项卡](#declare-custom-tab-in-app-manifest)
* [使用自适应卡片生成选项卡](~/tabs/how-to/build-adaptive-card-tabs.md)

### <a name="declare-custom-tab-in-app-manifest"></a>在应用清单中声明自定义选项卡

自定义选项卡在应用包的应用清单中声明。 对于要作为选项卡包含在应用中的每个网页，可以定义一个 URL 和一个范围。 此外，还可以将 [Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 添加到页面，并在页面加载后调用 `microsoftTeams.initialize()`。 Teams 显示你的页面并提供对 Teams 特定信息的访问权限，例如 Teams 客户端正在运行深色主题。

无论是选择在频道或组或个人范围内公开选项卡，都必须在选项卡中显示 <iframe\>HTML [内容页面](~/tabs/how-to/create-tab-pages/content-page.md)。对于个人选项卡，内容 URL 由 `staticTabs` 数组中的 `contentUrl` 属性直接在 Teams 应用清单中设置。你的选项卡内容与所有用户都一样。

对于频道或组选项卡，还可以创建其他配置页。 此页允许配置内容页 URL，通常通过使用 URL 查询字符串参数加载该上下文的相应内容。 这是因为频道或组选项卡可以添加到多个团队或群组聊天。 每次后续安装时，用户都可以配置选项卡，以便根据需要定制体验。 当用户添加或配置选项卡时，URL 与 Teams 用户界面 (UI) 中显示的选项卡相关联。 配置选项卡只是向该 URL 添加其他参数。 例如，添加 Azure Boards 选项卡时，可选择配置页加载选项卡的哪个板。 配置页 URL 由应用清单中的 `configurableTabs` 数组中的 `configurationUrl` 属性指定。

可以有多个频道或组选项卡，每个应用最多可以有 16 个个人选项卡。

### <a name="tools-to-build-tabs"></a>用于生成选项卡的工具

* [适用于 Microsoft Visual Studio Code 的 Teams 工具包](../toolkit/visual-studio-code-overview.md)
* [Visual Studio 的Teams工具包](../toolkit/visual-studio-overview.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [先决条件](~/tabs/how-to/tab-requirements.md)

## <a name="see-also"></a>另请参阅

* [在Microsoft Teams 中自定义选项卡](/microsoftteams/built-in-custom-tabs#develop-custom-tabs)
* [请求设备权限](../concepts/device-capabilities/native-device-permissions.md)
* [集成媒体功能](../concepts/device-capabilities/mobile-camera-image-permissions.md)
* [集成 QR 或条形码扫描程序](../concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [集成位置功能](../concepts/device-capabilities/location-capability.md)
* [移动设备上的选项卡](design/tabs-mobile.md#tabs-on-mobile)
