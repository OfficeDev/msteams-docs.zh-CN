---
title: 概述 - 分发应用
description: 介绍发布应用、Microsoft Teams应用和发布应用GCC。
ms.topic: conceptual
author: KirtiPereira
ms.author: surbhigupta
ms.localizationpriority: none
keywords: 部署发布应用上传 gcc
ms.openlocfilehash: 0436388365c2d7fc355c3f8cb40a9f05283124b8
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889186"
---
# <a name="distribute-your-microsoft-teams-app"></a>分发Microsoft Teams应用

你可以向Microsoft Teams、团队、组织或想要使用它的任何人提供你的应用。 分配方式取决于多个因素，包括用户需求、业务、技术要求以及应用的目标。

## <a name="upload-your-app-in-teams"></a>Upload应用Teams

旁加载应用供个人使用、与团队协作或测试和调试。 这种分发不需要正式的审阅过程。

> [!IMPORTANT]
> 目前，旁加载应用在 政府社区云 (GCC) 中可用，但不适用于 GCC-High 和国防部 (DOD) 。

有关详细信息，请参阅上传[应用Teams。](apps-upload.md)

## <a name="publish-your-app-to-your-org"></a>将应用发布到组织

使你的应用可供组织中的人员使用。此类分发需要Teams管理员的批准。

有关详细信息，请参阅在管理[中心管理Teams应用](/MicrosoftTeams/manage-apps?toc=%2Fmicrosoftteams%2Fplatform%2Ftoc.json&bc=%2FMicrosoftTeams%2Fbreadcrumb%2Ftoc.json)。

### <a name="government-community-cloud-gcc-organizations"></a>政府社区云 (GCC) 组织

在GCC Teams环境中，默认情况下会启用合规的 Microsoft 应用。 但是，在发布应用之前，请确保应用的所有终结点都GCC组织的要求。

> [!IMPORTANT]
>如果你的应用包含自动程序或消息传递扩展，则必须在 Azure 中设置自动程序与 Microsoft Teams 之间的通道时选择"Teams政府"选项。 有关详细信息，请参阅 [将机器人连接到频道](/azure/bot-service/bot-service-manage-channels?view=azure-bot-service-4.0&preserve-view=true)。

## <a name="publish-your-app-to-the-teams-store"></a>将应用发布到应用商店Teams应用商店

使应用可供所有人使用。 此类分发需要 Microsoft 批准。

有关详细信息，请参阅发布到[Teams 应用商店](~/concepts/deploy-and-publish/appsource/publish.md)。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [配置应用的默认安装选项](~/concepts/deploy-and-publish/add-default-install-scope.md)

## <a name="see-also"></a>另请参阅

* [Microsoft 365 应用合规计划](/microsoft-365-app-certification/overview)
