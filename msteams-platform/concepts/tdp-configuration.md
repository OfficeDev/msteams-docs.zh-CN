---
title: 开发人员门户中的应用配置
description: 了解如何使用开发人员门户为用户配置和管理Microsoft Teams
keywords: 开发人员门户团队入门
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: ce290bd7daa46467be279aae7c608321e75e2d57
ms.sourcegitcommit: 25539046d408c4270b988fd826d7cf1275f4b9dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2021
ms.locfileid: "52763127"
---
# <a name="app-configuration"></a>应用配置

应用包最重要的部分Microsoft Teams文件上的manifest.js部分。 此文件必须符合应用Teams[架构](~/resources/schema/manifest-schema.md)。 on manifest.js文件包含元数据，Teams向用户正确呈现你的应用。

您可以在开发人员门户的"配置 **"** 部分执行以下操作：

* 轻松创建应用包。
* 描述应用。
* Upload图标。
* 生成.zip文件以轻松分发。

> [!NOTE]
> 开发人员门户不会为你的应用生成功能代码，也不托管你的应用。 应用必须已在应用上传流程的清单中列出的 URL 上托管并运行，以产生工作应用。

:::image type="content" source="~/assets/images/tdp/tdp_configure_1.png" alt-text="Screenshot showing the Configure page of Teams Developer Portal.":::

## <a name="basic-information-and-branding"></a>基本信息和品牌

基本 **信息和****品牌** 打造部分定义了你正在制作的应用的简要说明。 这包括应用的名称、说明和视觉品牌。 此部分中的信息将用于应用的应用商店Teams应用安装对话中。

## <a name="capabilities"></a>功能

配置的 **"** 功能"部分列出了应用的功能详细信息。

> [!NOTE]
> 应用自定义功能目前仅在开发人员预览版中可用。
> 
> 最佳做法是，你必须提供自定义指南，以便应用用户和客户在自定义应用时遵循这些准则。 有关详细信息，请参阅自定义[应用程序中Microsoft Teams。](/MicrosoftTeams/customize-apps)

以下是功能：

:::image type="content" source="~/assets/images/tdp/tdp_capabilities.png" alt-text="Screenshot showing the Configure page of Teams Developer Portal.":::

* **个人应用** 

  本部分允许你定义在个人应用体验中默认呈现的一组选项卡，即用户在团队或频道上下文之外使用你的应用的体验。 在此部分中，提供以下详细信息：

  * 选项卡名称。
  * 唯一标识符。
  * 指向要显示在 Teams 中的 UI 的 URL。
  * 用户选择在浏览器中查看选项卡时使用的 URL。 这是可选信息。
  * 选项卡预期从其中加载或链接到的其他任何域。

* **组和频道应用**

  "Teams选项卡将成为频道的一部分，并快速访问团队信息和资源。 例如，频道的"规划器"选项卡包含单个计划，Power BI选项卡映射到特定报表。 用户可以向下钻取相关上下文，但无法导航到选项卡外部。例如，Power BI 选项卡不会启用到其他 Power BI 报表的导航，但它允许" **转到网站** "按钮，该按钮在 Power BI 主网站中启动报表。

    > [!NOTE]
    > 对于团队选项卡，必须提供配置 URL 来显示选项和收集信息，这将帮助您自定义选项卡的内容和体验。当用户首次将选项卡添加到频道时，将显示此 iframed HTML 页面。
    > 你还必须提供选项卡期望从其加载或链接到的任何其他域。

* **机器人**

  通过此部分，可以将一 [对话自动](~/bots/what-are-bots.md) 添加到应用中。 如果你已有注册了 Bot Framework 的自动程序，您可以通过单击 **"设置** 并单击自动程序的名称"自动框架 ID"并定义自动程序工作的范围来添加自动程序。

  如果尚未向 Bot Framework 注册自动程序，请单击" **注册"** 以创建新的聊天机器人。 注册自动程序后，返回到清单编辑器的此部分以输入其名称和自动程序框架 ID。

  提供自动程序信息后，你现在可以选择定义自动程序可以建议给用户的命令列表。 添加命令的名称、指示其语法和参数的命令说明以及此命令应应用于的范围。

  请注意，如果将自动程序定义为仅支持一个作用域，则为不受支持的范围指定的命令将被忽略。 你随时都可以编辑你的自动程序支持的范围。

* **Connector**

  此部分允许向应用添加连接器。 如果已注册连接器Office 365，**请选择"设置**"，然后输入连接器的名称和 ID。 如果需要新的连接器，请单击 **注册** 以在浏览器中访问连接器开发人员仪表板。

  > [!NOTE]
  > 通过应用自定义，管理员可以更改通过机器人、消息传递扩展、选项卡和连接器加载的应用的外观。 例如，如果Teams将应用的名称自定义为 ，则应用将显示为用户的新 `Contoso` `Contoso Agent` `Contoso Agent` 名称。 但是，在列表中向聊天添加连接器时，连接器仍将应用名称显示为 `Contoso` 。

* **消息扩展**

  [消息传递扩展](~/messaging-extensions/what-are-messaging-extensions.md) 是一种强大的方法，让用户在 Microsoft Teams 中参与你的应用。 用户可以查询服务的信息，将该信息以卡片形式发布到频道或聊天对话中。

  消息扩展由 Bot Framework 自动程序支持，因此它们要求配置自动程序运行。 如果拥有要为消息扩展提供 Power 的自动程序的名称和 Bot Framework ID，请输入该 ID。 否则，请单击 *注册* 创建一个，然后输入信息。 选择用户是否可以更新消息扩展的配置。

  配置基础自动程序后，定义邮件扩展可以接受的命令和参数。

  每个命令都需要标题和 ID。 命令可以选择性地包含用户说明。 每个命令最多支持五个参数，每个参数都需要：

  * 显示在客户端和用户请求Teams参数的名称。
  * 用户友好标题。
  * 可选说明。

  > [!NOTE]
  > 若要使用 app studio 创建消息传递扩展，请参阅 [使用 app studio 创建消息传递扩展](~/resources/create-messaging-extension-using-appstudio.md)。

* **会议扩展名**

  TODO：Rajesh R.

* **场景**

  在一起模式下的场景是场景开发人员使用 Microsoft Scene Studio 创建的一个项目，它以场景创建者所构想的创意设置将人们与视频流一起汇集在一起。 在构想的场景设置中，参与者具有指定席位，视频流呈现在这些座位中。 有关详细信息，请参阅Teams[模式](~/apps-in-teams-meetings/teams-together-mode.md)。

## <a name="permissions"></a>权限

可以使用本机设备Teams（如相机、麦克风和位置）丰富你的应用。

## <a name="languages"></a>语言

设置或更改应用支持的语言。

## <a name="single-sign-on"></a>单一登录

将应用配置为使用 SSO (单一登录) 。

## <a name="domains"></a>域

应用预期在客户端内加载的网站的有效Teams列表。 域列表可以包含通配符，例如 `*.example.com` ， 。 这完全匹配域的一个段;如果需要匹配，请使用 `a.b.example.com` `*.*.example.com` 。 如果你的选项卡配置或内容 UI 需要导航到除用于选项卡配置的其他任何其他域，则必须在此处指定该域。

不需要在应用中包含要支持的标识提供程序的域。 例如，若要使用 Google ID 进行身份验证，必须重定向到 accounts.google.com，但不得在 `validDomains[]` accounts.google.com。

Teams需要自己的 sharepoint URL 正常运行的应用程序，请包括其有效域列表中的"{teamsitedomain}"。

> [!IMPORTANT]
> 不要直接添加或通过通配符添加超出您控制的域。 例如， `yourapp.onmicrosoft.com` 是有效的，但 `*.onmicrosoft.com` 是 无效。

对象是包含类型 的所有元素的数组 `string` 。

## <a name="advanced"></a>高级
Todo by Karthig

### <a name="app-content"></a>应用内容
Todo by Karthig

### <a name="first-party-settings"></a>第一方设置
Todo by Karthig

## <a name="see-also"></a>另请参阅

* [开发人员Teams概述](~/concepts/build-and-test/teams-developer-portal.md)
* [分发Teams开发人员门户](~/concepts/tdp-distribute.md)
* [开发人员门户Teams中的工具](~/concepts/tdp-tools.md)