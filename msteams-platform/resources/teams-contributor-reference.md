---
title: 参与 Teams 文档
description: 创建和发布文档Teams步骤
author: surbhigupta
ms.author: lajanuar
ms.localizationpriority: medium
ms.topic: contributor-guide
ms.openlocfilehash: 28fe69d59757bf53ddd105fde403d625d5faf419
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155908"
---
# <a name="contribute-to-teams-documentation"></a>参与 Teams 文档

Teams文档是 **Microsoft Docs 技术** 文档库的一部分。 内容分为多个组，称为文档集，每个组表示作为单个实体管理的一组相关文档。 同一文档集内的文章在添加后具有相同的 URL **docs.microsoft.com。** 例如， `/docs.microsoft.com/microsoftteams/...` 是文档集Teams的开头。 Teams文章以 Markdown 语法编写，并托管在GitHub。

## <a name="set-up-your-workspace"></a>设置工作区

> [!div class="checklist"]
>
> * 安装 [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)。
> * 安装[Visual Studio Code (VS Code) 。](https://code.visualstudio.com/)
> * 直接从[应用商店安装](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack)文档创作VS Code包。
<br>&emsp;&emsp; 或

> [!div class="checklist"]
>
> * 安装VS Code：

   1. 选择侧 **活动** 栏上的"扩展"图标或使用 **"视图 => Extensions"** 命令或 Ctrl+Shift+X，搜索 **"Microsoft Docs Authoring Pack"。**
   1. 选择“安装”。
   1. 安装后 **，"安装"** 将更改到 **"管理齿轮** "按钮。

## <a name="review-the-microsoft-docs-contributors-guide"></a>查看 Microsoft Docs Contributors 指南

参与者指南提供了在 **Microsoft Docs** 平台上创建、发布和更新技术内容的指导。 

## <a name="microsoft-writing-style-and-content-guides"></a>Microsoft 编写、样式和内容指南

* **[Microsoft 写作风格指南](/style-guide/welcome)**：Microsoft 写作风格指南是一个全面的技术写作资源，反映了 Microsoft 的新式语音和风格方法。 为便于参考，将此联机指南添加到浏览器的 **"收藏夹"** 菜单中。

* **[编写开发人员内容](/style-guide/developer-content/)**：Teams内容面向对编程概念和过程有基本了解的开发人员受众。 你必须以引人注目的方式提供清晰、技术准确的信息，同时保持 Microsoft 的声调和风格，这一点非常重要。

* **[编写分步说明](/style-guide/procedures-instructions/writing-step-by-step-instructions)**：应用和交互式体验是开发人员了解 Microsoft 产品和技术的一种很好的方法。 以渐进式格式呈现复杂或简单的过程自然且用户友好。

## <a name="markdown-reference"></a>MarkDown 参考

**Microsoft Docs** 页面使用 **MarkDown** 语法编写，并通过 [Markdig](https://github.com/lunet-io/markdig) 引擎进行分析。 有关特定标记和格式约定的信息，请参阅 [Docs Markdown 参考](/contribute/markdown-reference)。

## <a name="file-paths"></a>文件路径

在使用相对路径并创建指向其他文档集的链接时，在文档中为超链接设置有效的文件路径非常重要。 只有在文件路径正确GitHub有效时，你的生成才成功。
 
有关超链接和文件路径详细信息，请参阅 [文档中的链接](/contribute/how-to-write-links)。

> [!IMPORTANT]
> 若要引用属于以下平台 **文档** 集Teams文章：<br>
> &emsp;&#x2714; 使用不带前导正斜杠的相对路径。<br>
> &emsp;&#x2714;包括 Markdown 文件扩展名。<br>
>例如 **：父目录/目录/路径到** article.md —>[生成适用于Microsoft Teams](../concepts/building-an-app.md) <br><br>
> 若要引用一篇 Microsoft Docs **库文章，** 该文章不是 Teams文档集的一部分：<br>
> &emsp;&#x2714; 使用以正斜杠开头的相对路径。<br>
> &emsp;&#x2714;不包括文件扩展名。 <br> 例如 **：/docset/address-to-file-location** ->使用 [Microsoft Graph API 处理Microsoft Teams](/graph/api/resources/teams-api-overview)<br><br>
> 若要引用 Microsoft Docs 库外部的页面（如 GitHub，请使用完整 `https` 文件路径。<br>

## <a name="code-samples-and-snippets"></a>代码示例和代码段

代码示例在有效地使用 API 和 SDK 方面起到重要作用。 良好的代码示例可以比描述性文本和说明性信息更加清楚地传达工作方式。 您的代码示例必须准确、简洁、记录良好且读者友好。 易于阅读的代码必须易于理解、测试、调试、维护、修改和扩展。 有关详细信息，请参阅 [如何在文档中包括代码](/contribute/code-in-docs)。

## <a name="see-also"></a>另请参阅

* [Microsoft Docs](/)
* [参与者指南](/contribute)
* [文档样式和语音快速入门](/contribute/style-quick-start)
* [剪切边缘：源代码可读性使用技巧](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)
* [Teams文档](/microsoftteams/platform/overview)
* [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)


## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [获取 Microsoft Docs 更新和最新公告](/teamblog)
