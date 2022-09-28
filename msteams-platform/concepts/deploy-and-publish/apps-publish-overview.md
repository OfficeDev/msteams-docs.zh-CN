---
title: 概述 - 分发应用
description: 了解如何将应用分发、发布到 Microsoft Teams 应用商店或组织。了解应用的终结点必须如何符合政府社区云 (GCC) 组织的要求。
ms.topic: conceptual
author: v-rpatkur
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: df17129ce1e51093351683ad01db3be9e65c5770
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100719"
---
# <a name="distribute-your-microsoft-teams-app"></a>分发 Microsoft Teams 应用

你可以将 Microsoft Teams 应用提供给个人、团队、组织或想要使用它的任何人。 分发方式取决于多种因素，包括用户的需求、业务、技术要求和应用目标。

## <a name="configure-default-install-options"></a>配置默认安装选项

可以配置默认安装选项。 例如，如果应用的主要功能是机器人，则当用户将应用安装到团队时，可以使机器人成为默认功能。

## <a name="create-your-app-package"></a>创建应用包

若要分发 Teams 应用，必须具有有效的应用包。  应用包是包含 **应用清单** 和 **应用图标的** zip 文件。

## <a name="upload-your-app-in-teams"></a>在 Teams 中上传应用

旁加载应用以供个人使用、与团队协作或用于测试和调试。 此类分发不需要正式的评审过程。

> [!IMPORTANT]
> 目前，旁加载应用在政府社区云 (GCC) 中可用，但不适用于 GCC-High 和国防部 (DOD)。

有关详细信息，请参阅[在 Teams 中上传应用](apps-upload.md)。

## <a name="publish-your-app-to-your-org"></a>将应用发布到组织

使你的应用对你组织中的人员可用。此类分发需要 Teams 管理员批准。

有关详细信息，请参阅[在 Teams 管理中心管理应用](/MicrosoftTeams/manage-apps?toc=%2Fmicrosoftteams%2Fplatform%2Ftoc.json&bc=%2FMicrosoftTeams%2Fbreadcrumb%2Ftoc.json)。

### <a name="government-community-cloud-gcc-organizations"></a>政府社区云 (GCC) 组织

在 GCC Teams 环境中，默认情况下会启用合规的 Microsoft 应用。 但是，在发布应用之前，请确保所有应用的终结点都符合 GCC 组织的要求。 有关详细信息，请参阅[政府社区云](../app-fundamentals-overview.md#government-community-cloud)。

> [!IMPORTANT]
>如果应用包括机器人或消息扩展，则在 Azure 中建立机器人与 Teams 之间的通道时，必须选择“**Microsoft Teams 政府版**”选项。 有关详细信息，请参阅[将机器人连接到通道](/azure/bot-service/bot-service-manage-channels?view=azure-bot-service-4.0&preserve-view=true)。

## <a name="publish-your-app-to-the-teams-store"></a>将应用发布到 Teams 应用商店

使你的应用可供所有人使用。 此类分发需要 Microsoft 批准。

有关详细信息，请参阅[发布到 Teams 应用商店](~/concepts/deploy-and-publish/appsource/publish.md)。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [配置应用的默认安装选项](~/concepts/deploy-and-publish/add-default-install-scope.md)

## <a name="see-also"></a>另请参阅

[Microsoft 365 应用合规性](/microsoft-365-app-certification/overview)
