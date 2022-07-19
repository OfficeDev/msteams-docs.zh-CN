---
title: Microsoft 365 插件
description: 在本文中，你将了解 Microsoft 365 插件、插件列表和标签、Microsoft 365 和 One Note 交互等。
ms.topic: conceptual
ms.localizationpriority: high
ms.author: Surbhigupta
ms.openlocfilehash: 438093c5ffe9990c5aa7c8175131c654019c3120
ms.sourcegitcommit: 79d525c0be309200e930cdd942bc2c753d0b718c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2022
ms.locfileid: "66841748"
---
# <a name="microsoft-365-plugins"></a>Microsoft 365 插件

Microsoft 365 插件提供 Moodle 网站和 Teams 之间的集成。 通过这些插件，用户可以轻松安排、交付和协作课程内容。 插件可以单独使用，也可以根据要求以合作方式使用。

## <a name="plugin-list-and-labels"></a>插件列表和标签

下表列出了要根据要求使用的插件和 GitHub 标签。

<!--Old content of the table updated and revamped |Plugins to install |Description |GitHub label(s)|
|-----|-----|----|
|[**OpenID Connect**](#openid-connect)|Enable SSO for users who work using both Moodle and Microsoft Teams|auth_oidc|
|• [**OpenID Connect**](#openid-connect) </br> • [**Microsoft 365 integration**](#microsoft-365-integration) |Create Teams instances for each course in Moodle, and sync faculty as owners, and students as team members|• auth_oidc </br> • local_o365|
|• [**OpenID Connect**](#openid-connect) </br> • [**Microsoft 365 integration**](#microsoft-365-integration) </br> • [**Teams Theme**](#microsoft-365-teams-theme)| Remove Moodle blocks and extra chrome within the Moodle iframes for Teams, which applies while mapping courses to Teams instances | • auth_oidc </br> • local_o365 </br> • themeboost_o365teams |
|• [**OpenID Connect**](#openid-connect) </br> • [**Microsoft 365 integration**](#microsoft-365-integration) </br> • [**Microsoft 365 Repository**](#microsoft-365-repository) |Leverage Microsoft 365 OneDrive content for file repositories to reduce storage needs in Moodle | • auth_oidc </br> * local_o365 </br> • repository_office 365|
|• [**OpenID Connect**](#openid-connect) </br> • [**OneNote**](#onenote-integration) </br> • [**OneNote Submissions**](#onenote-integration) </br> • [**OneNote Feedback**](#onenote-integration) | Enable OneNote to be used for assignment, submission and feedback |• auth_oidc </br> • local_onenote </br> • assignsubmission_onenote </br> • assignfeedback_onenote |  
|• [**OpenID Connect**](#openid-connect) </br> • [**Microsoft 365 integration**](#microsoft-365-integration) • [**Microsoft 365 Repository**](#microsoft-365-repository) </br> • [**Microsoft Block**](#microsoft-365-repository) | Enable 365 quick access blocks within Moodle with links to Microsoft 365 collaboration services and install links for Microsoft Office | • auth_oidc </br> • local_o365 </br> • repository_office365 </br> • block_microsoft |
|[**Teams Meeting**](#teams-meetings) | Enable Atto editor in Moodle to create Teams meeting links |atto_teamsmeeting |
|[**oEmbed Filter**](#oembed-filter) | Enable video links in Moodle | Filter_oembed| -->

|要安装的插件 |说明 |GitHub 标签|
|-----|-----|----|
|[**OpenID Connect**](#openid-connect)|为同时使用 Moodle 和 Teams 的用户启用 SSO。|auth_oidc|
|[**Microsoft 365 集成**](#microsoft-365-integration)|在 Moodle 中为每个课程创建 Teams 实例，并将教职员工作为所有者同步，将学生同步为团队成员。|local_o365|
|[**Microsoft 365 存储库**](#microsoft-365-repository) |支持 Microsoft 365 文件存储库的 OneDrive 内容，以减少 Moodle 中的存储需求。| repository_office 365|
|[**Teams 会议**](#teams-meetings) |在 Moodle 中启用 Atto 编辑器以创建 Teams 会议链接。|atto_teamsmeeting |
|[**Teams主题**](#microsoft-365-teams-theme)| 删除 Moodle iframes for Teams 中的 Moodle 块和额外部件版式，这适用于将课程映射到 Teams 实例。| themeboost_o365teams |
|[**OneNote**](#onenote-integration)| 启用 OneNote 以用于布置作业、提交和反馈。|local_onenote、assignsubmission_onenote 和 assignfeedback_onenote </br>|  
|[**Microsoft Block**](#microsoft-block) | 在 Moodle 中启用 Microsoft 365 快速访问块，提供指向 Microsoft 365 协作服务的链接，并安装 Microsoft Office 链接。|block_microsoft |
|[**oEmbed 筛选器**](#oembed-filter) | 在 Moodle 中启用视频链接。|Filter_oembed|

Moodle LMS 支持以下插件：

## <a name="openid-connect"></a>OpenID Connect

Open ID Connect 插件允许用户对任何支持必要规范的网站或工具进行身份验证，并为 Microsoft Office 365 提供单一登录支持 (SSO)。 OpenID Connect 插件为机构提供以下登录选项以满足其特定要求：

* 用户可以输入其 Office 365 凭据（如电子邮件和密码）以直接登录或使用 Moodles 用户名和密码字段登录，而无需登录到 Office 365。
* 用户可以选择链接以通过 Office 365 或 Moodle 页面上的 OpenID Connect 提供程序登录。

下图显示了 OpenID connect 登录页：

:::image type="content" source="../../assets/images/MoodleInstructions/openid-connect.png" alt-text="登录到 open-id connect":::

## <a name="microsoft-365-integration"></a>Microsoft 365 集成

Microsoft 365 集成包含多个具有多个功能的应用，使用户能够保持连接并根据需要执行不同的操作。 该插件允许管理员检查以下内容：

* 检查相应的集成函数。
* 在 Office 365 和 Moodle 之间同步用户。
* 为用户配置所需的权限。
* 为课程文件设置 SharePoint 网站。

下图显示了 Microsoft 365 集成设置页：

:::image type="content" source="../../assets/images/MoodleInstructions/365-integration.png" alt-text="microsoft 365 集成":::

### <a name="user-functions"></a>用户函数

用户可以通过 Microsoft 365 集成执行以下操作：

* 检查所有 Microsoft 365 插件集成的总体运行情况。
* 上传 CSV 文件，该文件将 Moodle 与 Office 365 用户进行比较。
* 检查 Azure AD 权限配置。

## <a name="microsoft-365-repository"></a>Microsoft 365 存储库

Microsoft 365 存储库插件允许用户在 OneDrive 中存储课程文件。 教职员工可以从 OneDrive 的课程文件部分或其自己的个人空间将文件添加到存储库。

Microsoft 365 存储库允许用户将其用作机构的文件存储库，同时使 Moodle 的数据结构保持简单。 Microsoft 365 存储库插件提供以下服务：

* 教职员工可以将课程文件存储在 OneDrive 中。 每个课程都有自己的文件夹在 OneDrive 中创建，这允许教职员工从 OneDrive 的课程文件区域或其自己的个人空间添加文件。  
* 将文件作为副本添加到 Moodle 或创建指向该文件的链接。 链接文件显示在新的应用程序窗口中或嵌入到网页中。
* 使用 Moodle 文件选取器将文件上传到 OneDrive 或 SharePoint。

下图显示了 Microsoft 365 文件存储库：

:::image type="content" source="../../assets/images/MoodleInstructions/microsoft-365- repository.png" alt-text="M365 存储库" :::

## <a name="teams-meetings"></a>团队会议

Teams 会议插件允许用户根据可用性在日历、作业、论坛帖子以及 Atto 编辑器中创建会议请求。

安装插件后，教职员工和学生可以使用 Moodle 创建音频或视频会议，这需要 Microsoft 365 帐户和 Moodle 权限。

>[!NOTE]
>Teams 会议不会显示在 Outlook 或 Teams 日历上，但是可以将单个学生姓名添加到同一邀请中。

下图显示 Teams 会议登录页：

:::image type="content" source="../../assets/images/MoodleInstructions/teams-meeting.png" alt-text="登录到团队会议":::

## <a name="microsoft-365-teams-theme"></a>Microsoft 365 Teams 主题

Microsoft 365 Teams 主题插件为用户提供 Moodle 课程主页的自定义视图，并且在用户访问 Teams 中的 Moodle 课程时可供查看。

主题插件为用户提供具有以下功能的统一增强体验：

* 适应 Microsoft Teams 主题更改，例如默认、深色和高对比度。
* 重点介绍课程活动。
* 删除 Moodle 块、导航、页眉和页脚。
* 提供 Microsoft Team 用户界面 (UI) 元素。

下图显示了用户设置的 Teams 主题：

:::image type="content" source="../../assets/images/MoodleInstructions/teams-theme.png" alt-text="Microsoft Teams 主题":::

## <a name="onenote-integration"></a>OneNote 集成

OneNote 集成插件为用户提供浏览笔记本、分区和页面的选项；学生在此提交作业，教师在 OneNote 中提供相应作业的必要反馈。 OneNote 还通过添加测试和链接以外的功能来增强用户体验，同时使用数字笔、照片或视频媒体将功能扩展到移动设备，以及与组共同创作。

OneNote 集成有助于访问文本、图形和音频存储库。 该插件具有以下优点：

* 包括浏览笔记本、分区和页面，学生在其中处理作业，并在 OneNote 中提供有关这些作业的反馈。
* 结合使用数字联编程序进行笔记、作业和反馈以供参考和审阅。
* 扩展文本和链接之外的创作功能，并使用数字笔、照片或视频媒体扩展移动使用，以及与组共同创作。
* 在教职员工帐户下包含每个作业的提交和反馈页面。 当此类内容保存在 Moodle 中时，HTML 和任何关联图片的副本将打包在 zip 文件中。

> [!NOTE]
> 提交或反馈事件会触发 OneNote 创建，其中包含学生已注册的每个课程的分区。

## <a name="microsoft-block"></a>Microsoft block

Microsoft block 插件允许用户访问课程 SharePoint 文件位置并在 OneNote 笔记本中查看课程以供提交，以及修改 Office 365 集成首选项的选项。 管理员可以将 block 配置为显示在所有课程页面上。

Microsoft block 通过提供用户界面来修改 Microsoft 365 集成功能并访问其众多资源，从而增强用户体验。 管理员可以将 block 配置为查看修改后的更改以显示在每个课程页上。 该 block 允许用户执行以下活动：

* 访问课程 SharePoint 文件位置和 OneNote 笔记本。
* 在 OneNote 笔记本上查看课程以供提交。
* 配置 Outlook 日历同步。
* 管理与 Office 365 的连接。
* 自定义个人 Office 365 集成首选项。

下图显示了 Microsoft block 用户界面：

:::image type="content" source="../../assets/images/MoodleInstructions/microsoft-block-1.png" alt-text="microsoft block":::

## <a name="oembed-filter"></a>oEmbed 筛选器

oEmbed 筛选器插件简化了在 Moodle 中包含的外部 HTML 内容，从而简化和增强了用户体验。 以下是 oEmbed 筛选器的优点。

* 缩短将视频嵌入 HTML 页面的时间。
* 启用多个视频内容提供程序的嵌入。
* 确保从任何受支持的服务复制和嵌入代码都更快。
* 允许在没有 API 密钥的情况下嵌入视频。

下图显示了在 Moodle 中包含外部 HTML 内容：

:::image type="content" source="../../assets/images/MoodleInstructions/oEmbed-filter.png" alt-text="oEmbed 筛选器页":::

## <a name="see-also"></a>另请参阅

* [Moodle 合作伙伴应用](../partner-apps-for-moodle.md)
* [Moodle FAQ](../faqs.md)
