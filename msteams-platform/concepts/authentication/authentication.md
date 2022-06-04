---
title: 对应用用户进行身份验证
description: 介绍 Teams 中的身份验证以及如何在应用中使用它
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Teams 身份验证 OAuth SSO Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: db1a16959755668ec9aa298ed355ef657503ca03
ms.sourcegitcommit: e16b51a49756e0fe4eaf239898e28d3021f552da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2022
ms.locfileid: "65887732"
---
# <a name="authenticate-users-in-microsoft-teams"></a>在 Microsoft Teams 中对用户进行身份验证

身份验证就是验证应用用户，并保护应用和应用用户免受无理访问。 可以使用适用于应用的身份验证方法来验证想要使用 Teams 应用的应用用户。

选择通过以下两种方式之一为应用添加身份验证：

- **在 Teams 应用中启用单一登录 (SSO)**：Teams 中的 SSO 是一种身份验证方法，它使用应用用户的 Teams 标识为他们提供对应用的访问权限。 登录 Teams 的用户无需在 Teams 环境中再次登录到应用。 仅需要应用用户同意，Teams 应用将从 Azure Active Directory (AD) 检索访问详细信息。 应用用户同意后，他们甚至可以从其他设备访问应用，而无需再次进行验证。

- **使用第三方 OAuth 提供程序启用身份验证**：可以使用第三方 OAuth 标识提供者 (IdP) 对应用用户进行身份验证。 应用用户已注册到标识提供者，该提供程序与你的应用具有信任关系。 当用户尝试登录时，标识提供者会验证应用用户并为其提供对应用的访问权限。 Azure AD 是此类第三方 OAuth 提供程序之一。 可以使用其他提供商，例如 Google、Facebook、GitHub 或任何其他提供商。

## <a name="select-authentication-method"></a>选择身份验证方法

在选项卡应用、机器人应用和消息传递扩展应用中使用 SSO 或第三方 OAuth IDP 启用身份验证。 选择在应用中添加身份验证的两种方法之一：

:::row:::
    :::column span="1":::
        SSO
    :::column-end:::
    :::column span="1":::
        &nbsp;
    :::column-end:::
    :::column span="1":::
        OAuth
    :::column-end:::
:::row-end:::
:::row:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/tab-sso-icon.png" alt-text="选项卡应用的 SSO" link="../../tabs/how-to/authentication/tab-sso-overview.md" border="false":::
    :::column-end:::
    :::column span="1":::
        <br>

        &nbsp;&nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;**Tab 应用**  
        
    :::column-end:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/tab-app-idp.png" alt-text="使用选项卡应用的第三方 OAuth 提供程序进行身份验证。" link="../../tabs/how-to/authentication/auth-tab-aad.md" border="false":::
    :::column-end:::
:::row-end:::
:::row:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/bot-sso-icon.png" alt-text="适用于机器人应用的 SSO" link="../../bots/how-to/authentication/auth-aad-sso-bots.md" border="false":::
    :::column-end:::
    :::column span="1":::
        <br>

        &nbsp;&nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;**机器人应用**
        
    :::column-end:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/bot-app-idp.png" alt-text="使用机器人应用的第三方 OAuth 提供程序进行身份验证。" link="../../bots/how-to/authentication/add-authentication.md" border="false":::
    :::column-end:::
:::row-end:::
:::row:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/mex-sso-icon.png" alt-text="用于消息传递扩展应用的 SSO" link="../../messaging-extensions/how-to/enable-SSO-auth-me.md" border="false":::
    :::column-end:::
    :::column span="1":::
        <br>

        &nbsp;&nbsp; &nbsp; **消息扩展应用**
        
    :::column-end:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/mex-app-idp.png" alt-text="使用消息传递扩展应用的第三方 oAuth IDP 进行身份验证。" link="../../messaging-extensions/how-to/add-authentication.md" border="false":::
    :::column-end:::
:::row-end:::

> [!NOTE]
> “无提示身份验证”页将移到“资源”模块。 有关详细信息，请参阅 [无提示身份验证](../../tabs/how-to/authentication/auth-silent-aad.md)。

## <a name="see-also"></a>另请参阅

- [在选项卡应用中启用单一登录](../../tabs/how-to/authentication/tab-sso-overview.md)
- [选项卡的 Microsoft Teams 身份验证流](~/tabs/how-to/authentication/auth-flow-tab.md)
- [为机器人提供单一登录支持](~/bots/how-to/authentication/auth-aad-sso-bots.md)
- [为消息扩展添加身份验证](~/messaging-extensions/how-to/add-authentication.md)
