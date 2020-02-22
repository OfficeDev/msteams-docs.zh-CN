---
title: 设计准则参考
description: 介绍设计个人应用程序的指南
keywords: 团队设计准则参考框架个人应用程序
ms.openlocfilehash: 0d886adf926697f8920c0893589201ea4e4c3a9c
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228071"
---
# <a name="personal-apps"></a>个人应用程序

> [!Important]
> 对移动客户端上的选项卡的完全支持即将推出。 若要为此更改做准备，应按照移动选项卡[上的选项卡指南中](~/tabs/design/tabs-mobile.md)的步骤创建选项卡。 个人应用（静态选项卡）目前可在[开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中使用。
>
> 释放对选项卡的完全支持时：
>
> * 所有选项卡将始终在移动设备上可用
> * 您`contentUrl` **将在移动团队客户端中加载**。
> * 对于频道/组选项卡，用户仍可以通过您`websiteUrl`在单独的浏览器中打开您的`contentUrl`选项卡，但您将首先加载。

个人应用是具有个人作用域的应用程序。 作为应用程序开发人员，您可以选择提供为单个用户生成的应用程序版本。 在此版本中，选项卡的集合（以及自动程序，如果您已加入）是为此人设计的。 这样，你就能够创建与你的用户的一对一交互。

个人应用程序是指有人可以查看其所有内容，以及最近在应用中查看的所有项目。 它将所有内容都放在一个位置。 在下面的屏幕截图中，Contoso 是个人应用浮出控件中的个人应用程序。

![应用程序溢出菜单的图像](~/assets/images/Personal-apps-App-flyout.png)

---

## <a name="guidelines"></a>准则

个人应用程序通常包含以下选项卡：

### <a name="your-tab"></a>您的选项卡

你的用户将看到其所有内容。 其个人空间。 该选项卡可作为列表、网格、列或单个画布进行排列。。最适用于您的应用程序的任何功能。 有关设计有效选项卡的其他信息，请参阅：[选项卡设计](../../tabs/design/tabs.md)。

由于此选项卡可以显示来自多个通道的项目，因此每个项目都应显示其自己的团队、频道和选项卡，以便用户可以轻松地查看它的来源。

!["个人任务" 选项卡](~/assets/images/Personal-apps-MY-tab.png)

### <a name="recent"></a>最近更新

"**最近**" 选项卡允许某人浏览最近在您的应用程序中查看过的所有内容。 它按时间顺序列出（从最高到最新）。 单击此列表中的某个项目会将该用户导航到该项目的频道和选项卡。

![最近选项卡](~/assets/images/Personal-apps-Recent-tab.png)

### <a name="all"></a>全部

这是个人组织中的所有选项卡的列表（仍有权访问它们）。 换句话说，它在使用应用程序的任何位置显示它们。 与**最近**的选项卡一样，选择列表中的内容会将用户直接带入相关频道和选项卡。

### <a name="bot"></a>Bot

Bot 不是必需的，但它是直接和私下与用户进行通信的绝佳方式。 通知是个人应用程序中最重要的功能之一，以及通知与直接通信是否更好的方法？

Bot 以卡片形式传递邮件，这可以提供特定信息（如通知新内容可用）或广泛的更新（如日常待办情况列表）。 有关设计有效的 bot 的其他信息，请参阅： [Bot 设计](../../bots/design/bots.md)。

![Bot 问候语](~/assets/images/Personal-apps-Bot.png)

### <a name="help-and-settings"></a>帮助和设置

帮助内容使用户能够发现您的应用程序的细微差别。 添加 "**设置**" 选项卡，让他们可以进一步自定义它。

### <a name="about"></a>关于

包括 "**关于**" 选项卡，以提供版本号码、功能、隐私和权限链接等信息。

## <a name="best-practices"></a>最佳做法

### <a name="communicate-directly-with-your-users"></a>直接与您的用户通信

使用 bot 向用户通知更改和新功能。

### <a name="customize-your-tabs"></a>自定义选项卡 .。。

你可以随意添加其他选项卡，以帮助你的用户完成特定任务。

### <a name="and-make-them-relevant-to-every-user"></a>...并使其与每个用户相关

您在应用程序清单中声明的每个选项卡将对所有用户可见。 例如，如果您的个人应用程序是由经理和员工使用的费用报告工具，则 "**审批**" 选项卡应提供对这两个角色都有意义的内容。
