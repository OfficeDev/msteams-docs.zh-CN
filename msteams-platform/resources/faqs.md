---
title: Moodle 常见问题解答。
description: 在本文章中，可获取在使用 Moodle LMS 时一些常见问题的答案。
ms.topic: conceptual
ms.localizationpriority: high
ms.author: Surbhigupta
ms.openlocfilehash: 02c6a5086bd2132b43f3e36b85bb63c67c7b0d26
ms.sourcegitcommit: 79d525c0be309200e930cdd942bc2c753d0b718c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2022
ms.locfileid: "66842008"
---
# <a name="moodle-faq"></a>Moodle 常见问题解答

使用 Moodle LMS 时获取某些查询的答案。<br>

<br>

<details>

<summary><b>如果同步后未创建一个或多个课程团队，该怎么办？</b></summary>

每个 Moodle 课程必须至少有一名教职员工和一名学生与 Microsoft 365 AAD UPN 帐户匹配。 如果同步未找到匹配项，则无法创建团队。

每个团队课程实例都必须有一个所有者，并且同步会将教职员工设置为所有者，并假定教职员工拥有 Teams 许可证。

<br>

</details>

<details>

<summary><b>在 Teams 中工作时，应如何删除 Moodle 登录页？是否可以强制单一登录 (SSO)？</b></summary>

用户在 Moodle 登录页中有多个登录选项。

* 若要使用 Microsoft 365 凭据以专属方式登录，请为 **auth_oidc 插件** 启用 **强制重定向** 配置设置。 如果启用该服务，用户可以看到 Microsoft 登录页。
* 若要手动登录到 Moodle 门户，请参阅 [Moodle](https://moodle.org/login/index.php)。

<br>

</details>

<details>

<summary><b>如何指定要同步的用户？我不希望所有 Azure AD 用户都与 Moodle 网站同步。 </b></summary>

通过同步 **local_o365** 插件的配置选项，使用 **用户创建限制** 选项来指定用户。 **筛选器** 左侧的下拉菜单提供国家/地区、公司名称和语言等选项。

> [!TIP]
> 创建动态 Microsoft 365组，以启用具有多个配置文件属性的 **筛选器** 选项。

下图显示了用户创建限制选项：

:::image type="content" source="../assets/images/MoodleInstructions/faq-2.png" alt-text="sync":::

:::image type="content" source="../assets/images/MoodleInstructions/faq-3.png" alt-text="Azure ad":::

<br>

</details>

<details>

<summary><b>我们希望教职员工能够将课程同步到 Teams，Moodle 管理员是否是唯一可以控制课程同步的管理员？</b></summary>

默认情况下，只有 Moodle 管理员可以配置同步。 团队所有者可以控制课程是否同步到 Teams 以及是否启用 **允许在课程中配置课程同步**。 在这种情况下，团队所有者是教职员工。 block 向具有相应所有者权限的个人显示配置选项。

<!-- For more information, see Microsoft 365 block within the Moodle course interface. -->

下图显示了 **允许在课程中配置课程同步** 选项：

:::image type="content" source="../assets/images/MoodleInstructions/faq-4.png" alt-text="管理员":::

下图显示了课程同步：

:::image type="content" source="../assets/images/MoodleInstructions/faq-5.png" alt-text="同步":::

<br>

</details>

<details>

<summary><b>我们已遵循了该文档，但用户帐户无法同步 AAD 和 Moodle。我们该怎么做？</b></summary>

在用户执行 **Delta 令牌清理** 作为最终故障排除步骤之前，可以解决此问题。

下表提供了要执行和检查的操作和依赖项：

| 相关项  | Action | 参考|
|-------|------------|----------|
| 稳定版本| 验证 Moodle 的版本是否列为 **稳定版**。| 有关详细信息，请参阅[版本支持](https://docs.moodle.org/dev/Releases#Version_support)。|
|权限| 验证 Azure 应用程序是否具有运行同步所需的权限。| 有关详细信息，请参阅 [Microsoft 权限](https://docs.moodle.org/311/en/Microsoft_365#Permissions)。|
| 完全同步| 验证是否已启用 **执行每个运行** 的完全同步，并查看 **Azure AD 同步用户** 的 **任务日志**。| 有关详细信息，请参阅[启用完全同步](https://docs.moodle.org/311/en/local_o365)</br>有关详细信息，请参阅[检查任务日志](https://docs.moodle.org/311/en/local_o365#Sync_users_with_Azure_AD)。 |
|令牌刷新|在 local_o365 插件中清理 **用户同步 delta 令牌**。| 有关详细信息，请参阅[令牌刷新](https://docs.moodle.org/38/en/Office365)。|
<!-- |令牌刷新|在 local_o365 插件中清理 **用户同步 delta 令牌**| {moodle_url}\local_o365\acp.php?Mode=maintenance_cleandeltatoken| -->
<br>

</details>

<details>

<summary><b>尽管大多数用户都可以顺利登录，但还是有一个或多个用户无法使用其 Microsoft 365 凭据登录。此现象原因是什么？</b></summary>

用户无法使用其 Microsoft 365 凭据进行登录的原因可能与同步期间的用户映射操作有关。 若要解决该问题，请执行以下步骤：

* 检查 Moodle 用户身份验证类型是否 **OpenID**。
* 检查 Moodle **用户名** 是否与 AAD 用户名匹配。
* 清理 **令牌问题** 并重试。
* 检查用户是否具有访问 Azure 应用程序的 **权限**。

<br>

</details>

<details>

<summary><b>所有用户都无法使用其 Microsoft 365 凭据登录。我们该如何解决此问题？</b></summary>

无法在开始时登录的用户需要报告问题，并验证应用程序 **客户端密码** 是否过期。

下图显示了用户使用 Microsoft 365 凭据登录时收到的错误消息：

:::image type="content" source="../assets/images/MoodleInstructions/faq-6.png" alt-text="报告问题":::

下图显示了 Azure 门户中的错误：

:::image type="content" source="../assets/images/MoodleInstructions/faq-7.png" alt-text="Azure 门户":::

如果 **客户端密码** 已过期，则用户需要生成新的 **客户端密码**，并更新页面上的配置。 用户可以在更新 **客户端密码** 后重新登录，这可能需要长达 24 小时才能重新预配。

<br>

</details>

<details>

<summary><b>如何更改链接到课程的团队实例？</b></summary>

管理员可以通过 **管理 Teams 连接** 页面更改与课程关联的团队实例。 选择要更改的课程旁边的 **连接**，然后选择团队实例。 如果使用课程重置来存档团队，则可以将其链接回上一个团队。

下图显示了团队实例：

:::image type="content" source="../assets/images/MoodleInstructions/faq-8.png" alt-text="团队实例":::

<br>

</details>

<details>

<summary><b>Atto Teams 会议集成为何没有显示在 Atto 编辑器中？</b></summary>

如果在 Atto 编辑器中显示 Teams 图标的 **工具栏配置** 中缺少图标引用，则用户可能会遇到 Atto Teams 会议问题。 用户需要使用以下步骤将 Teams 会议图标添加到链接图标右侧：

* 安装插件。
* 使用 **团队会议** 更新 **工具栏配置**。

下图显示了工具栏配置调整后的工具栏图标：

:::image type="content" source="../assets/images/MoodleInstructions/faq-9.png" alt-text="工具栏":::

:::image type="content" source="../assets/images/MoodleInstructions/faq-10.png" alt-text="链接图标":::

有关编辑 Atto 工具栏详细信息，请参阅：

* [Atto editor-ModdleDocs](https://docs.moodle.org/311/en/Atto_editor)
* [Atto editor-Icon 映射](https://docs.moodle.org/311/en/Atto_editor#:~:text=in%20the%20editor.-,Atto%20editor%20toolbar,-Atto%20Row%201)
<br>

</details>

<details>

<summary><b>通过 Microsoft 集成安排的会议是否会显示在 Outlook 或 Teams 日历中？要显示的会议的标准日程表是什么？</b></summary>

通过应用安排的会议不会显示在计划的 Outlook 或 Teams 日历中，因为它们相当于频道会议。 课程频道中的所有成员都可以直接从嵌入式频道链接参加会议。 有关详细信息，请参阅[频道会议](https://www.knowledgewave.com/blog/benefits-of-channel-meetings-in-microsoft-teams)。

但是，你可以访问邀请并将参与者姓名手动添加到会议邀请的 **必需** 或 **可选** 字段，以在其日历上显示远程会议。 标准日程表基于用户在创建会议时指定的日期。 有关限制的详细信息，请参阅 [Microsoft Teams 的限制和规范](/microsoftteams/limits-specifications-teams)。

<br>

</details>

<details>

<summary><b>是否有任何支持站点，我们可以在其中获取有关产品和其他问题的更多帮助？</b></summary>

有关产品和服务问题的支持和帮助或开发人员社区帮助，请参阅[支持和反馈](/microsoftteams/platform/feedback)。
