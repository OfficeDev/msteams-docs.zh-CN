---
title: 参与 Teams 文档
description: 了解创建和发布Teams文档的步骤
author: surbhigupta
ms.author: lajanuar
ms.localizationpriority: medium
ms.topic: contributor-guide
ms.openlocfilehash: 165f5df18395d329aa2f383d2f07e6f7ff3afdcf
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143079"
---
# <a name="contribute-to-teams-documentation"></a>参与 Teams 文档

Teams 文档是 **Microsoft Docs** 技术文档库的一部分。 内容分为称为 docsets 的组，每个组表示作为单个实体管理的一组相关文档。 同一文档集中的项目在 **docs.microsoft.com** 后具有相同的 URL 路径扩展名。 例如，`/docs.microsoft.com/microsoftteams/...`是 Teams 文档集文件路径的开头。 Teams 文章以 Markdown 语法编写，并托管在 GitHub 上。

## <a name="set-up-your-workspace"></a>设置工作区

> [!div class="checklist"]
>
> * 安装 [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)。
> * 安装 [Microsoft Visual Studio代码](https://code.visualstudio.com/) （VS Code）。
> * 直接从 VS Code 市场安装 [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack)。<br>&emsp;&emsp;或
[!div class="checklist"]
>
> * 在VS Code内安装：

   1. 选择侧边活动栏上的“**扩展”图标**，或使用 **视图 => Extensions** 命令或 Ctrl+Shift+X，然后搜索 **Microsoft Docs创作包**。
   1. 选择“**安装**”。
   1. 安装后， **安装** 更改 **管理** 齿轮按钮。

## <a name="review-the-microsoft-docs-contributors-guide"></a>查看Microsoft Docs参与者指南

参与者指南提供了在 **Microsoft Docs** 平台上创建、发布和更新技术内容的方向。

## <a name="microsoft-writing-style-and-content-guides"></a>Microsoft 写作、风格和内容指南

* **[Microsoft 写作风格指南](/style-guide/welcome)**：Microsoft 写作风格指南是一种全面的技术写作资源，反映了 Microsoft 的现代语音和风格方法。 若要轻松参考，请将此联机指南添加到浏览器的 **收藏夹** 菜单。

* **[编写开发人员内容](/style-guide/developer-content/)**：Teams 特定内容面向对编程概念和流程有基本了解的开发人员受众。 在保持 Microsoft 的语气和风格的同时，必须以令人信服的方式提供清晰、技术上准确的信息，这一点很重要。

* **[编写分步说明](/style-guide/procedures-instructions/writing-step-by-step-instructions)**：应用和交互式体验是开发人员了解 Microsoft 产品和技术的好方法。 以渐进式格式呈现复杂或简单的过程是自然的，并且用户友好。

## <a name="markdown-reference"></a>MarkDown 参考

**Microsoft Docs** 页以 **MarkDown** 语法编写，并通过 [Markdig](https://github.com/lunet-io/markdig) 引擎进行分析。 有关特定标记和格式设置约定的详细信息，请参阅 [Docs Markdown 参考](/contribute/markdown-reference)。

## <a name="file-paths"></a>文件路径

使用相对路径并创建指向其他文档集的链接时，请务必为文档中的超链接设置有效的文件路径。 仅当文件路径正确或有效时，GitHub 上的生成才会成功。

有关超链接和文件路径的详细信息，请参阅 [使用文档](/contribute/how-to-write-links)中的链接。

> [!IMPORTANT]
> 若要引用 **Teams 平台文档集** 一部分的文章，请执行以下操作：<br>
> &emsp;&#x2714; 使用不带前导正斜杠的相对路径。<br>
> &emsp;&#x2714; 包括 Markdown 文件扩展名。<br>
>例如：**父目录/目录/路径到 article.md** —> [为 Microsoft Teams 生成应用](../concepts/building-an-app.md) <br><br>
> 若要引用 **不属于 Teams 平台文档集** Microsoft Docs库文章：<br>
> &emsp;&#x2714; 使用以正斜杠开头的相对路径。<br>&emsp;&#x2714; 不要包括文件扩展名。<br>
> 例如：**/docset/address-to-file-location** —> [使用 Microsoft Graph API 与 Microsoft Teams](/graph/api/resources/teams-api-overview)<br><br>
> 若要引用Microsoft Docs库之外的页面（如 GitHub），请使用完整的 `https` 文件路径。<br>

## <a name="code-samples-and-snippets"></a>代码示例和代码片段

代码示例对于有效使用 API 和 SDK 起着重要作用。 与描述性文本和说明性信息相比，展示良好的代码示例可以更清楚地传达工作方式。 代码示例必须准确、简洁、记录良好且易于阅读。 易于阅读的代码必须易于理解、测试、调试、维护、修改和扩展。 有关详细信息，请参阅 [如何在文档](/contribute/code-in-docs)中包含代码。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [获取Microsoft Docs更新和最新公告](/teamblog)

## <a name="see-also"></a>另请参阅

* [Microsoft Docs](/)
* [参与者指南](/contribute)
* [文档样式和语音快速入门](/contribute/style-quick-start)
* [最前沿：源代码可读性提示](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)
* [Teams 文档](/microsoftteams/platform/overview)
* [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)
