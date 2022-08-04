---
title: 使用Microsoft Graph提取 Teams 会议的脚本
description: 介绍在会议后方案中提取脚本的过程、方案和 API。
ms.localizationpriority: high
ms.topic: concept
ms.openlocfilehash: 0f16fff6675f6cb0f0bd7f4dc7550885a6177174
ms.sourcegitcommit: 990a36fb774e614146444d4adaa2c9bcdb835998
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2022
ms.locfileid: "67232367"
---
# <a name="get-meeting-transcripts-using-graph-apis"></a>使用图形 API 获取会议脚本

现在可以将应用配置为在会议后方案中提取 Microsoft Teams 会议脚本。 应用可以使用 Microsoft Graph REST API 访问和提取为事先安排的 Teams 会议生成的脚本。

下面是使用图形 API提取会议脚本的一些用例：

| 用例 | 脚本 API 如何帮助... |
| --- | --- |
| 你需要获取脚本，以便从“销售”垂直的多个会议中捕获有意义的见解。 跟踪所有会议并手动检索会议笔记非常耗时且效率低下。 会议结束后，你需要检查所有这些会议中的对话，以获取有用的信息。 | 在应用中使用图形 API 提取会议脚本会自动检索与你的目的相关的所有会议的脚本。 应用可以接收会议通知，并在会议结束后生成脚本时获取脚本。 然后，此数据可用于获取： <br> • 聚合见解和智能分析 <br> • 新的潜在顾客和亮点 <br> • 会议跟进和摘要 |
| 作为人力资源计划，你将召开一个集思广益的会议，以了解和提高员工的健康状况和工作效率。 必须持续做笔记来提供会议后摘要可能会妨碍想法流，并且可能不会捕获所有有价值的建议。 会话结束后，需要分析讨论以收集数据点以进行规划改进。 | 在应用中使用 Graph API 提取会议后的脚本可让你和参与者完全专注于讨论。 会议脚本的内容可用于： <br> • 参与度和情绪分析 <br> • 列出任务或问题 <br> • 后续会议和通知 |

> [!NOTE]
> 将来，Microsoft 可能需要你或你的客户根据通过 API 访问的数据量支付额外费用。

若要提取特定会议的脚本，请执行以下操作：

- [配置Azure AD访问脚本的权限](#configure-permissions-on-azure-ad-to-access-transcript)
- [获取会议 ID 和组织者 ID](fetch-id.md)
- [使用图形 API 提取脚本](/graph/api/resources/calltranscript)

## <a name="configure-permissions-on-azure-ad-to-access-transcript"></a>配置Azure AD访问脚本的权限

应用必须具有提取脚本所需的权限。 它可以使用组织范围的应用程序权限或特定会议的资源特定许可 （RSC） 应用程序权限访问和提取 Teams 会议的脚本。

### <a name="use-organization-wide-application-permissions"></a>使用组织范围的应用程序权限

可以将应用配置为访问租户中的会议脚本。 在这种情况下，会议组织者无需在 Teams 会议聊天中安装应用。 当租户管理员授权组织范围的应用程序权限时，你的应用可以读取和访问租户中所有会议的脚本。

有关可授予应用的组织范围应用程序权限的详细信息，请参阅 [联机会议权限](/graph/permissions-reference#online-meetings-permissions)。

### <a name="use-meeting-specific-rsc-application-permissions"></a>使用特定于会议的 RSC 应用程序权限

如果希望应用仅提取安装它的 Teams 会议的脚本，请为应用配置特定于会议的 RSC 权限。 授权用户可以在会议聊天中安装应用。 会议结束后，应用可以进行 API 调用以获取该会议的脚本。

有关可授予应用的特定于会议的 RSC 权限的详细信息，请参阅 [特定于资源的许可](../rsc/resource-specific-consent.md#resource-specific-permissions-for-a-chat)。

配置权限后，将应用配置为接收所有相关会议事件的更改通知。 通知包含有助于访问脚本内容的会议 ID 和组织者 ID。 应用可以在会议结束后生成时提取会议脚本。 脚本的内容可用作 `.vtt` 或 `.docx` 文件。

有关应用如何知道会议何时结束的详细信息，请参阅 [订阅更改通知](fetch-id.md#subscribe-to-change-notifications) 和 [使用Bot Framework获取会议 ID 和组织者 ID](fetch-id.md#use-bot-framework-to-get-meeting-id-and-organizer-id)。

> [!NOTE]
> 对于特定于会议的 RSC 应用程序权限或组织范围的应用程序权限，调用 Graph API 访问和检索脚本的过程保持不变。 这些 API 目前仅支持计划的会议。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [获取会议 ID 和组织者 ID](fetch-id.md)

## <a name="see-also"></a>另请参阅

- [会议应用 API 参考](../../apps-in-teams-meetings/API-references.md#meeting-apps-api-references)
