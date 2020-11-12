---
title: 对 Microsoft 团队文档的贡献
description: 创建和发布团队文档的步骤
author: laujan
ms.author: lajanuar
ms.topic: contributor-guide
ms.openlocfilehash: 80aaf7795a226c0437140fe72e1d74b07fa66775
ms.sourcegitcommit: f6029c8ff0c5315613a3efcd86777aa4cede39e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/11/2020
ms.locfileid: "48995014"
---
# <a name="contributing-to-microsoft-teams-documentation"></a>对 Microsoft 团队文档的贡献

[团队文档](/microsoftteams/platform/overview) 是 [Microsoft 文档](https://docs.microsoft.com/) 技术文档库的一部分。 内容被组织到名为 docsets 的组中，每个组代表一组作为单个实体管理的相关文档。 同一 docset 中的文章在 *<span></span> microsoft.com* 之后具有相同的 URL 路径扩展名。  例如，  `/docs.microsoft.com/microsoftteams/...`   是团队 docset 文件路径的开头。 团队文章以  [MarkDown](#markdown-reference) 语法编写，并托管在 [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)上。

## <a name="set-up-your-workspace"></a>设置你的工作区

> [!div class="checklist"]
>
> * 安装 [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)。
> * 安装 [Visual Studio code](https://code.visualstudio.com/) (VS code) 。
> * 直接从 VS 代码市场安装[文档创作包](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack)
<br>&emsp;&emsp; 和

> [!div class="checklist"]
>
> * 从 VS 代码中进行安装：

   1. 选择侧活动栏上的 " **扩展" 图标** ，或使用 " **视图 => 扩展** " 命令 (Ctrl + Shift + X) 并搜索 *文档创作包* (Microsoft) 。
   1. 选择 " **安装** " 按钮。
   1. 安装完成后，" **安装** " 按钮将更改为 " **管理** 齿轮" 按钮。

## <a name="review-the-microsoft-docs-contributors-guide"></a>查看 Microsoft 文档 "参与者指南"

" [参与者指南](/contribute)" 提供了在 Microsoft/docs. 上创建、发布和更新技术内容的方向 *另请参阅*[文档样式和语音快速入门](/contribute/style-quick-start)。

## <a name="microsoft-writing-style-and-content-guides"></a>Microsoft 写作、样式和内容指南

* **[Microsoft 写作风格指南](/style-guide/welcome)** 。 请考虑将此联机指南添加到浏览器的 **"收藏夹"** 菜单。 它是今天的技术写作的综合资源，反映了 Microsoft 的新式语音和风格方法。

* **[编写开发人员内容](/style-guide/developer-content/)** 。 特定于团队的内容面向开发人员群体，对编程概念和过程有基本的了解。 在维护 Microsoft 的语气和样式的同时，以极具吸引力的方式提供清晰、技术上的信息，这一点非常重要。

* **[编写分步说明](/style-guide/procedures-instructions/writing-step-by-step-instructions)** 。 应用程序和交互式体验是开发人员了解 Microsoft 产品和技术的一种非常好的方法。 以渐进格式呈现复杂或简单的过程是自然的，并且是用户友好的。

## <a name="markdown-reference"></a>MarkDown 参考

 Microsoft 文档页面使用 MarkDown 语法编写，并通过 [Markdig](https://github.com/lunet-io/markdig) 引擎进行分析。 有关特定标记和格式设置约定，请 *参阅*[文档 Markdown 参考](/contribute/markdown-reference)。

## <a name="file-paths"></a>文件路径

为文档中的超链接设置有效的文件路径可能是一项挑战，尤其是在使用相对路径和创建指向其他 docsets 的链接时。  如果文件路径不正确或无效，则您的内部版本将不会在 GitHub 上成功。

有关超链接和文件路径的详细信息，请 *参阅*[在文档中使用链接](/contribute/how-to-write-links)。

>[!IMPORTANT]
> 若要 *引用属于团队* 平台 docset 的文章，请执行以下操作：<br>
> &emsp;&#x2714; 使用不带前导正斜线的相对路径。<br>
> &emsp;&#x2714; 包括 Markdown 文件扩展名。<br>
>Ex：  **父目录/目录/路径到文章** -> `[Building an app for Microsoft Teams](../concepts/building-an-app.md)` <br><br>
> 若要引用 Microsoft 文档库 (<https://docs.microsoft.com/>) *不属于* 团队平台 docset 的文章：<br>
> &emsp;&#x2714; 使用以正斜杠开头的相对路径。<br>
> &emsp;&#x2714; 不包括文件扩展名。 <br> Ex：  **/docset/address-to-file-location** — > `[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`
>

## <a name="code-samples-and-snippets"></a>代码示例和代码段

代码示例在帮助开发人员成功使用 Api 和 Sdk 方面起着重要作用。 我们提供的代码示例可以传达与描述性文本和说明信息更清晰的工作方式。 您的代码示例应准确、简洁、记录良好，并且最重要的是读者友好。 易于阅读的代码也易于理解、测试、调试、维护、修改和扩展。 *请参阅*[如何在文档中包含代码](/contribute/code-in-docs)。有关可读性的提示，请 *参阅*[剪切边缘：源代码可读性提示](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)。

> [!div class="nextstepaction"]
> [获取 Microsoft 文档更新和最新通知](/teamblog)
