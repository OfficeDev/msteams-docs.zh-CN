---
title: 配置管理员同意
description: 介绍如何配置管理员许可
ms.topic: how-to
ms.localizationpriority: medium
keywords: Azure AD) 图形 API Microsoft Azure Active Directory (团队身份验证选项卡
ms.openlocfilehash: 4d072bba0e4900aecec63e06cb63f4ac2311d91a
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2022
ms.locfileid: "66557748"
---
# <a name="configure-admin-consent"></a>配置管理员同意

可以为公开的 API 定义应用范围，并确定用户是否可以在启用用户同意的目录中同意此范围。 只能让管理员为特权较高的权限提供许可。

## <a name="to-expose-an-api"></a>公开 API

1. 从左窗格中选择 **“管理** > **公开 API** ”。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/expose-api-menu.png" alt-text="公开 API 菜单选项。":::

    将显示 **“公开 API** ”页。

1. 选择 **“设置** ”以生成应用 ID URI。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/expose-an-api.png" alt-text="设置应用 ID URI":::

    将显示用于设置应用 ID URI 的部分。

1. 输入应用 ID URI，然后选择 **“保存**”。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/set-app-id-uri.png" alt-text="App ID URI":::

    浏览器上弹出一条消息，指出应用 ID URI 已更新。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-id-uri-msg.png" alt-text="应用 ID URI 消息":::

    应用 ID URI 显示在页面上。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-id-uri-added.png" alt-text="更新了应用 ID URI":::

## <a name="to-configure-api-scope"></a>配置 API 范围

1. 选择 **+** 在此 **API 部分定义的范围** 中添加范围。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/select-scope.png" alt-text="选择范围":::

    将显示 **“添加范围** ”页。

1. 输入应用范围的应用详细信息。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-scope.png" alt-text="添加范围详细信息":::

    1. 输入范围名称。 这是必填字段。
    1. 选择 **管理员和用户** 以配置可以同意使用用户登录凭据的用户。 默认选项 **仅限管理员**。
    1. 输入 **管理员许可显示名称**。 这是必填字段。
    1. 输入管理员同意的说明。 这是必填字段。
    1. 输入 **用户同意显示名称**。
    1. 输入用户同意说明的说明。
    1. 为状态选择 **“启用”** 选项。
    1. 选择“**添加作用域**”。

    浏览器上弹出一条消息，指出已添加范围。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/scope-added-msg.png" alt-text="作用域添加的消息":::

    应用 ID URI 显示在页面上。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/scope-added.png" alt-text="添加和显示的范围":::

## <a name="to-configure-authorized-client-application"></a>配置已授权的客户端应用程序

1. 在 **“公开 API** ”页中移动到 **“授权客户端应用程序** ”部分，然后选择 **“+ 添加客户端应用程序**”。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/auth-client-apps.png" alt-text="授权的客户端应用程序":::

    将显示 **“添加客户端应用程序** ”页。

1. 输入用于添加客户端应用程序的详细信息。 在本部分中，你将添加两个客户端应用程序。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-client-app.png" alt-text="添加客户端应用程序":::

    1. 输入 **1fec8e78-bce4-4aaf-ab1b-5451cc387264** 作为 Teams 移动或桌面应用程序的客户端 ID。
    1. 选择为应用创建的已 **授权范围的** 应用 ID。
    1. 选择“添加应用程序”。

    浏览器上弹出一条消息，指出已添加客户端应用。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/update-app-auth-msg.png" alt-text="客户端应用程序添加了消息":::

    页面上显示的客户端应用 ID。

1. 重复上一步，为 Teams Web 应用程序添加客户端应用。

    1. 输入 **5e3ce6c0-2b1f-4285-8d4b-75ee78787346** 作为 Web 应用的客户端 ID。
    1. 选择为应用创建的已 **授权范围的** 应用 ID。
    1. 选择“添加应用程序”。

    浏览器上弹出一条消息，指出已添加客户端应用。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/update-app-auth-msg.png" alt-text="客户端应用程序为 Web 应用添加了消息":::

    页面上显示的客户端应用 ID。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/client-app-added.png" alt-text="添加并显示的客户端应用":::
