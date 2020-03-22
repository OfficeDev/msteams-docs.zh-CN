---
title: 选项卡的设计准则
description: 介绍为内容和协作创建选项卡的准则
keywords: 团队设计指南参考框架选项卡配置
ms.openlocfilehash: 409c8994b4266e37146038df054c0da6fb887607
ms.sourcegitcommit: 576a4768b835422545cb6b6b3f75dce8318ea02d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2020
ms.locfileid: "42896497"
---
# <a name="content-and-conversations-all-at-once-using-tabs"></a>内容和对话，所有使用选项卡一次

> [!Important]
> **移动客户端上的选项卡**
>
> 创建选项卡时，请遵循[移动电话上的选项卡指南](./tabs-mobile.md)。 如果您的选项卡使用身份验证，则必须将团队 JavaScript SDK 升级到版本1.4.1 或更高版本，否则身份验证将失败。
>
> **移动设备上的个人（静态）选项卡：**
>
> * 在[开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中，可以使用静态选项卡（个人应用）。
> * 在构建静态选项卡时，请确保遵循[移动电话上的选项卡指南](~/tabs/design/tabs-mobile.md)
>
> **移动设备上的频道/组（可配置）选项卡：**
>
> * 移动客户端仅显示具有值的`websiteUrl`选项卡。 如果希望您的选项卡显示在团队移动客户端上，则必须设置的`websiteUrl`值。
> * 移动上的默认打开行为是使用在浏览器中的`websiteUrl`外部打开。 对于发布到公用应用商店的应用程序，如果您希望频道选项卡在默认情况下在团队内打开，请遵循[移动电话上的选项卡指南](~/tabs/design/tabs-mobile.md)，并转到您的支持代表以请求列入白名单。

选项卡是可用于在团队的随机工作流中共享内容、举行对话和托管第三方服务的画布。 当您在 Microsoft 团队中构建一个选项卡时，它会将 web 应用程序的前端和中心放置在易于从关键对话中访问的位置。

## <a name="guidelines"></a>准则

一个合适的选项卡应显示以下特征：

### <a name="focused-functionality"></a>重点功能

当为满足特定需求而构建时，选项卡的工作效果最佳。 将重点放在一小部分任务或与选项卡所在通道相关的一组数据。

### <a name="reduced-chrome"></a>简化 chrome

避免在选项卡中创建多个面板、添加导航层或要求用户在一个选项卡中垂直和水平滚动。换言之，请不要在选项卡中包含选项卡。

### <a name="integration"></a>集中

查找通过将卡发布到对话来通知用户选项卡活动的方法。

### <a name="conversational"></a>对话

寻找一种有助于围绕选项卡进行对话的方法。这样可确保在现有内容、数据或流程上进行对话中心。

### <a name="streamlined-access"></a>精简访问

请确保在适当的时间授予对正确人员的访问权限。 保持您的登录过程很简单将避免为发布和协作创建障碍。

### <a name="responsiveness-to-window-sizing"></a>对窗口大小的响应

在窗口大小中，可以将团队用作720px，以确保在小窗口中可用的选项卡与极高分辨率的可用性同样重要。

### <a name="flat-navigation"></a>平面导航

我们要求开发人员不要将其整个门户添加到选项卡。保持导航相对平整有助于保持更简单的会话模式。 换言之，对话是关于事情的列表（如已会审的工作项）或一个内容（如规范）。

深入导航层次结构中有一些固有的导航挑战，在线程对话中。 为获得最佳用户体验，应将选项卡导航保持在最少，并按如下方式设计：

> [!div class="checklist"]
>
> * **打开一个任务模块，如单个工作项或实体**。 这将完全阻止聊天，并且是最佳选择，它是专门了解选项卡的聊天，而不是子实体或编辑体验。
>* **在 iframe 中打开伪对话框**。 如果与屏蔽背景一起使用，我们建议使用较亮的颜色，而不是黑色。 `app-gray-10 at 30%`透明度工作良好。
>* **打开浏览器页面**。

### <a name="personality"></a>特征

您的选项卡画布极有机会为你的体验提供品牌。 您的徽标是标识的重要部分，与您的用户的连接。，因此请务必包含它：

> [!div class="checklist"]
>
>* 将徽标放置在左右角或沿下边缘
> * 保持您的徽标较小且不引人注目

合并自己的颜色和布局 twill 也有助于传达个性。

> [!TIP]
> 请使用我们的视觉样式，让你的服务感觉像团队的一部分。 *请参阅*（例如 [团队颜色] （/concepts/design/components/typography.md

---

## <a name="tab-layouts"></a>选项卡布局

[!INCLUDE [Tab layouts](../../includes/design/tab-layouts.html)]

---

## <a name="types-of-tabs"></a>选项卡的类型

[!INCLUDE [Tab types](../../includes/design/tab-types.html)]

---

## <a name="configuration-page-height"></a>配置页高度

>[!IMPORTANT]
>在9月2018中，选项卡[配置页面](~/tabs/how-to/create-tab-pages/configuration-page.md)的高度增加，而宽度保持不变。 如果您的应用程序是为较旧的大小设计的，则选项卡配置页将具有大量的垂直空白。 从此更改中免除的旧版应用程序将需要在更新后与 Microsoft 联系，以适应新的维度。

选项卡配置页的尺寸：

<img width="450px" title="配置选项卡的大小" src="~/assets/images/tabs/config-dialog-Contoso2.png" />

### <a name="guidelines-for-tab-configuration-page-format"></a>选项卡配置页面格式的准则

* 使固定高度图形元素上的选项卡配置页的内容区域的最小高度为基准。
* 使用`window.innerHeight`计算可用的垂直间距（配置页中的内容区域的高度）。 这将返回配置页面所`<iframe>`驻留的大小，在将来的版本中可能会发生更改。 通过使用此值，你的内容将自动调整为将来的更改。
* 将垂直空间分配给可变高度元素减去固定高度元素所需的值。
* 对于 "*登录*状态"，将内容垂直和水平居中。
* 如果需要背景图像，您需要一个新图像，调整大小以适合该区域（首选），或者您可以保留相同的图像并在其中进行选择：
  * 与左上角对齐。
  * 将图像缩放到合适大小。

如果调整了适当的大小，您的选项卡配置页面应如下所示：

<img width="450px" title=""新建配置" 选项卡" src="~/assets/images/tabs/config-dialog-Contoso.png" />

## <a name="best-practices"></a>最佳做法

### <a name="always-include-a-default-state"></a>始终包含默认状态

如果您的选项卡是可配置的，则包括默认状态以使选项卡易于设置。

### <a name="deep-linking"></a>深度链接

只要有可能，卡片和 bot 应在承载的选项卡中深入链接到丰富的数据。例如，卡片可能会显示错误数据的摘要，但单击它可以在选项卡中显示整个 bug。

### <a name="naming"></a>名称

在很多情况下，您的应用程序的名称将产生很好的选项卡名称。 此外，还应考虑根据它们提供的功能命名选项卡。

## <a name="notifications-for-tabs"></a>选项卡通知

对于选项卡内容更改，有两种通知模式：

> [!div class="checklist"]
>
> * **使用应用程序 api 将更改通知用户**。 此消息将显示在用户的活动源和指向该选项卡的深层链接中。*请参阅*  [创建指向 Microsoft 团队中的内容和功能的深层链接](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest)
> * **使用 bot**。 如果为 Tab 线程的目标，则此方法是首选方法。 结果将是，选项卡的线程对话将作为最近活动的视图移动到视图中。 此方法还允许在通知的发送方式方面有一些复杂之处。

  将邮件发送到选项卡线程可将对所有用户的活动的感知提高到所有用户，而无需明确通知每个人。 这是不带噪音的感知。 此外，当您`@mention`将特定用户的通知放在其源中时，会将它们直接链接到 tab 线程。
