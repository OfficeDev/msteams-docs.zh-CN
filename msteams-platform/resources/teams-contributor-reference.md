---
title: 参与Microsoft Teams文档
description: 创建和发布文档Teams的步骤
author: laujan
ms.author: lajanuar
localization_priority: Normal
ms.topic: contributor-guide
ms.openlocfilehash: a6742b8b994cc3752df923db75a3d7d77cbebd83
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019669"
---
# <a name="contributing-to-microsoft-teams-documentation"></a>参与Microsoft Teams文档

[Teams文档](/microsoftteams/platform/overview)是[Microsoft Docs 技术](https://docs.microsoft.com/)文档库的一部分。 内容分为多个组，称为文档集，每个组表示作为单个实体管理的一组相关文档。 同一文档集内的文章在 *docs <span></span> .microsoft.com 之后具有相同的* URL 路径 microsoft.com。  例如， `/docs.microsoft.com/microsoftteams/...` 是文档Teams路径的开头。 Teams文章以[MarkDown](#markdown-reference)语法编写，并托管在 GitHub[上](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)。

## <a name="set-up-your-workspace"></a>设置工作区

> [!div class="checklist"]
>
> * 安装 [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)。
> * 安装[Visual Studio Code (VS Code) 。](https://code.visualstudio.com/)
> * 直接从[应用商店安装](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack)文档VS Code包
<br>&emsp;&emsp; 或

> [!div class="checklist"]
>
> * 从安装VS Code：

   1. 选择侧活动栏上的"扩展"图标或使用"视图 **=>** 扩展"命令 (Ctrl+Shift+X) 并搜索 Microsoft) 文档创作包 (。
   1. 选择" **安装"** 按钮。
   1. 安装完成后，" **安装"** 按钮将更改为" **管理齿轮"** 按钮。

## <a name="review-the-microsoft-docs-contributors-guide"></a>查看 Microsoft Docs Contributors 指南

参与者 [指南](/contribute) 提供了在 Microsoft Docs 平台上创建、发布和更新技术内容的指导。 *另请参阅* 文档 [样式和语音快速入门](/contribute/style-quick-start) 。

## <a name="microsoft-writing-style-and-content-guides"></a>Microsoft 编写、样式和内容指南

* **[Microsoft 写作风格指南](/style-guide/welcome)**。 请考虑将此联机指南添加到浏览器 **的收藏夹** 菜单。 它是当今技术写作的全面资源，反映了 Microsoft 的新式语音和风格方法。

* **[编写开发人员内容](/style-guide/developer-content/)**。 Teams内容面向对编程概念和过程有基本了解的开发人员受众。 在保持 Microsoft 的声调和风格的同时，以引人注目的方式提供清晰、技术准确的信息非常重要。

* **[编写分步说明](/style-guide/procedures-instructions/writing-step-by-step-instructions)**。 应用和交互式体验是开发人员了解 Microsoft 产品和技术的一种很好的方法。 以渐进格式呈现复杂或简单的过程很自然且用户友好。

## <a name="markdown-reference"></a>MarkDown 参考

 Microsoft Docs 页面使用 MarkDown 语法编写并通过 [Markdig](https://github.com/lunet-io/markdig) 引擎进行分析。 请参阅 *特定*[标记和](/contribute/markdown-reference)格式约定的文档 Markdown 参考。

## <a name="file-paths"></a>文件路径

为文档中的超链接设置有效的文件路径可能是一项挑战，尤其是在使用相对路径和创建指向其他文档集的链接时。  如果文件路径不正确或无效GitHub生成将不会成功。

有关超链接和文件路径详细信息，请参阅 *使用*[文档中的链接](/contribute/how-to-write-links)。

>[!IMPORTANT]
> 若要引用属于以下平台 *文档* 集Teams文章：<br>
> &emsp;&#x2714; 使用不带前导正斜杠的相对路径。<br>
> &emsp;&#x2714;包括 Markdown 文件扩展名。<br>
>例如  **：父目录/目录/路径到 article.md** —> `[Building an app for Microsoft Teams](../concepts/building-an-app.md)` <br><br>
> 若要引用一篇 Microsoft Docs *库文章，* 该文章不是 Teams文档集的一部分：<br>
> &emsp;&#x2714; 使用以正斜杠开头的相对路径。<br>
> &emsp;&#x2714;不包括文件扩展名。 <br> 例如  **：/docset/address-to-file-location** —> `[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`<br><br>
> 若要引用 Microsoft Docs 库外部的页面，GitHub，请使用完整的 `https` 文件路径。<br>

## <a name="code-samples-and-snippets"></a>代码示例和代码段

代码示例在帮助开发人员成功使用 API 和 SDK 方面起到重要作用。 呈现良好的代码示例可以比描述性文本和说明性信息更加清楚地传达工作方式。 您的代码示例应准确、简洁、记录良好，最重要的是，读者友好。 易于阅读的代码也易于理解、测试、调试、维护、修改和扩展。 *请参阅*[如何在文档中包括代码](/contribute/code-in-docs)。有关可读性提示，另 *请参阅边缘*[：源代码可读性使用技巧。](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)

> [!div class="nextstepaction"]
> [获取 Microsoft Docs 更新和最新公告](/teamblog)
