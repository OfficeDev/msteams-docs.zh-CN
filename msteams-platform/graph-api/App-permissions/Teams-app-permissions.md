---
title: 管理 Teams 应用权限
author: surbhigupta
description: 在本模块中，了解如何根据功能在不同位置管理 Teams 应用。
ms.topic: reference
ms.localizationpriority: medium
ms.author: lomeybur
ms.openlocfilehash: 2bc501444e52f31061312c325ddf7dd80370240a
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791839"
---
# <a name="permissions-in-teams-app"></a>Teams 应用中的权限

Teams 应用的权限在两个位置进行管理，具体取决于应用功能：

* [特定于资源的同意 (RSC) ](#resource-specific-consent)
* [Azure Active Directory (Azure AD)](#azure-active-directory)

:::image type="content" source="../../assets/images/teams-app-permissions.png" alt-text="屏幕截图介绍了不同的 Teams 应用权限。":::

## <a name="resource-specific-consent"></a>资源特定许可

RSC 是 Microsoft Teams 和 Microsoft 图形 API集成，使应用能够使用 API 终结点管理组织内的特定资源（团队或聊天）。 有关详细信息，请参阅 [在 Teams 中启用特定于资源的许可](../rsc/resource-specific-consent.md)。

RSC 权限仅适用于在 Teams 客户端上安装的 Teams 应用，目前不是 Azure AD 门户的一部分，并在 Teams 应用清单 (JSON) 文件中声明。

## <a name="azure-active-directory"></a>Azure Active Directory

Azure AD 是基于云的标识和访问管理服务。 此服务可帮助员工访问外部资源，例如 Microsoft 365、Azure 门户和数千个其他 SaaS 应用程序。 有关详细信息，请参阅 [Azure Active Directory](/azure/active-directory/fundamentals/active-directory-whatis)。

### <a name="microsoft-graph-api-permission"></a>Microsoft 图形 API 权限

图形 API权限在 Azure AD 中管理。 若要使你的应用可访问 Microsoft Graph 中的数据，用户或管理员必须通过同意过程向其授予正确的权限。 有关详细信息，请参阅 [Microsoft Graph 权限](/graph/permissions-reference)。

## <a name="capability-wise-management"></a>功能明智管理

### <a name="bot-and-messaging-extension"></a>机器人和消息传递扩展

机器人或消息传递扩展 ID 基于以下注册平台生成。 需要此 ID 才能将机器人或消息传递扩展添加到 Teams 应用。

* Azure AD 门户
* 开发人员或 Bot Framework 门户

#### <a name="azure-ad-portal"></a>Azure AD 门户

在 Azure AD 门户中注册机器人或消息传递扩展时，它将具有与之关联的 Azure AD 应用 ID，可以在 **Azure AD** 门户> **应用注册** 中找到该 ID。 终结点和其他机器人配置在Azure 门户进行管理。

#### <a name="developer-or-bot-framework-portal"></a>开发人员或 Bot Framework 门户

在开发人员或 Bot Framework 门户中注册机器人或消息传递扩展时，它将没有 Azure AD 应用 ID。 但是，可以在 Bot Framework 门户上找到机器人或消息传递扩展 ID。 终结点和其他机器人配置在 Bot Framework 门户中进行管理。

可以在应用的开发人员门户部分中管理机器人的其他 Teams 特定配置。

### <a name="connectors"></a>连接器

连接器具有连接器 ID，并通过连接器开发人员仪表板进行注册和管理。 此 ID 是向 Teams 应用引入连接器所必需的。 可以在应用的开发人员门户部分中管理连接器的其他 Teams 特定配置。
