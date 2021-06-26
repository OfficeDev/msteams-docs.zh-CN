---
title: 参与Teams文档
description: 创建和发布文档Teams的步骤
author: surbhigupta
ms.author: lajanuar
localization_priority: Normal
ms.topic: contributor-guide
ms.openlocfilehash: a567b0462397780650d6173df9dae1b340a06f97
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140508"
---
# <a name="contribute-to-teams-documentation"></a><span data-ttu-id="7d05b-103">参与Teams文档</span><span class="sxs-lookup"><span data-stu-id="7d05b-103">Contribute to Teams documentation</span></span>

<span data-ttu-id="7d05b-104">Teams文档是 **Microsoft Docs 技术** 文档库的一部分。</span><span class="sxs-lookup"><span data-stu-id="7d05b-104">Teams documentation is part of the **Microsoft Docs** technical documentation library.</span></span> <span data-ttu-id="7d05b-105">内容分为多个组，称为文档集，每个组表示作为单个实体管理的一组相关文档。</span><span class="sxs-lookup"><span data-stu-id="7d05b-105">The content is organized into groups called docsets, each representing a group of related documents managed as a single entity.</span></span> <span data-ttu-id="7d05b-106">同一文档集内的文章在更改后具有相同的 URL **docs.microsoft.com。**</span><span class="sxs-lookup"><span data-stu-id="7d05b-106">Articles in the same docset have the same URL path extension after **docs.microsoft.com**.</span></span> <span data-ttu-id="7d05b-107">例如， `/docs.microsoft.com/microsoftteams/...` 是文档Teams路径的开头。</span><span class="sxs-lookup"><span data-stu-id="7d05b-107">For example, `/docs.microsoft.com/microsoftteams/...` is the beginning of the Teams docset file path.</span></span> <span data-ttu-id="7d05b-108">Teams文章以 Markdown 语法编写，并托管在GitHub。</span><span class="sxs-lookup"><span data-stu-id="7d05b-108">Teams articles are written in Markdown syntax and hosted on GitHub.</span></span>

## <a name="set-up-your-workspace"></a><span data-ttu-id="7d05b-109">设置工作区</span><span class="sxs-lookup"><span data-stu-id="7d05b-109">Set up your workspace</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="7d05b-110">安装 [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)。</span><span class="sxs-lookup"><span data-stu-id="7d05b-110">Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).</span></span>
> * <span data-ttu-id="7d05b-111">安装[Visual Studio Code (VS Code) 。](https://code.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="7d05b-111">Install [Visual Studio Code](https://code.visualstudio.com/) (VS Code).</span></span>
> * <span data-ttu-id="7d05b-112">直接从[应用商店安装](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack)文档创作VS Code包。</span><span class="sxs-lookup"><span data-stu-id="7d05b-112">Install [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directly from the VS Code Marketplace.</span></span>
<br><span data-ttu-id="7d05b-113">&emsp;&emsp; 或</span><span class="sxs-lookup"><span data-stu-id="7d05b-113">&emsp;&emsp; or</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="7d05b-114">安装VS Code：</span><span class="sxs-lookup"><span data-stu-id="7d05b-114">Install within VS Code:</span></span>

   1. <span data-ttu-id="7d05b-115">选择侧 **活动** 栏上的扩展图标或使用 View = **> Extensions** 命令或 Ctrl+Shift+X，搜索 **Microsoft Docs Authoring Pack。**</span><span class="sxs-lookup"><span data-stu-id="7d05b-115">Select the **Extensions icon** on the side activity bar or use the **View => Extensions** command or Ctrl+Shift+X and, search for **Microsoft Docs Authoring Pack**.</span></span>
   1. <span data-ttu-id="7d05b-116">选择“安装”。</span><span class="sxs-lookup"><span data-stu-id="7d05b-116">Select **Install**.</span></span>
   1. <span data-ttu-id="7d05b-117">安装后 **，"安装"** 将更改到 **"管理齿轮** "按钮。</span><span class="sxs-lookup"><span data-stu-id="7d05b-117">After installation, the **Install** changes to the **Manage** gear button.</span></span>

## <a name="review-the-microsoft-docs-contributors-guide"></a><span data-ttu-id="7d05b-118">查看 Microsoft Docs Contributors 指南</span><span class="sxs-lookup"><span data-stu-id="7d05b-118">Review the Microsoft Docs Contributors Guide</span></span>

<span data-ttu-id="7d05b-119">参与者指南提供了在 **Microsoft Docs** 平台上创建、发布和更新技术内容的指导。</span><span class="sxs-lookup"><span data-stu-id="7d05b-119">The contributors guide provides direction to create, publish, and update technical content on the **Microsoft Docs** platform.</span></span> 

## <a name="microsoft-writing-style-and-content-guides"></a><span data-ttu-id="7d05b-120">Microsoft 编写、样式和内容指南</span><span class="sxs-lookup"><span data-stu-id="7d05b-120">Microsoft Writing, Style, and Content Guides</span></span>

* <span data-ttu-id="7d05b-121">**[Microsoft 写作风格指南](/style-guide/welcome)**：Microsoft 写作风格指南是一个全面的技术写作资源，反映了 Microsoft 的新式语音和风格方法。</span><span class="sxs-lookup"><span data-stu-id="7d05b-121">**[Microsoft Writing Style Guide](/style-guide/welcome)**: Microsoft Writing Style Guide is a comprehensive resource for technical writing and reflects Microsoft's modern approach to voice and style.</span></span> <span data-ttu-id="7d05b-122">为便于参考，将此联机指南添加到浏览器的 **"收藏夹"** 菜单中。</span><span class="sxs-lookup"><span data-stu-id="7d05b-122">For easy reference, add this online guide to your browser's **Favorites** menu.</span></span>

* <span data-ttu-id="7d05b-123">**[编写开发人员内容](/style-guide/developer-content/)**：Teams内容面向对编程概念和过程有基本了解的开发人员受众。</span><span class="sxs-lookup"><span data-stu-id="7d05b-123">**[Writing developer content](/style-guide/developer-content/)**: Teams specific content is aimed at a developer audience with a fundamental understanding of programming concepts and processes.</span></span> <span data-ttu-id="7d05b-124">你必须以引人注目的方式提供清晰、技术准确的信息，同时保持 Microsoft 的声调和风格，这一点非常重要。</span><span class="sxs-lookup"><span data-stu-id="7d05b-124">It is important that you must provide clear, technically accurate information in a compelling manner while maintaining Microsoft's tone and style.</span></span>

* <span data-ttu-id="7d05b-125">**[编写分步说明](/style-guide/procedures-instructions/writing-step-by-step-instructions)**：应用和交互式体验是开发人员了解 Microsoft 产品和技术的一种很好的方法。</span><span class="sxs-lookup"><span data-stu-id="7d05b-125">**[Writing step-by-step instructions](/style-guide/procedures-instructions/writing-step-by-step-instructions)**: Applied and interactive experiences are a great way for developers to learn about Microsoft products and technologies.</span></span> <span data-ttu-id="7d05b-126">以渐进式格式呈现复杂或简单的过程自然且用户友好。</span><span class="sxs-lookup"><span data-stu-id="7d05b-126">Presenting complex or simple procedures in a progressive format is natural and user friendly.</span></span>

## <a name="markdown-reference"></a><span data-ttu-id="7d05b-127">MarkDown 参考</span><span class="sxs-lookup"><span data-stu-id="7d05b-127">MarkDown reference</span></span>

<span data-ttu-id="7d05b-128">**Microsoft Docs** 页面使用 **MarkDown** 语法编写并通过 [Markdig](https://github.com/lunet-io/markdig) 引擎进行分析。</span><span class="sxs-lookup"><span data-stu-id="7d05b-128">**Microsoft Docs** pages are written in **MarkDown** syntax and parsed through a [Markdig](https://github.com/lunet-io/markdig) engine.</span></span> <span data-ttu-id="7d05b-129">有关特定标记和格式约定的信息，请参阅 [Docs Markdown 参考](/contribute/markdown-reference)。</span><span class="sxs-lookup"><span data-stu-id="7d05b-129">For more information on specific tags and formatting conventions, see [Docs Markdown reference](/contribute/markdown-reference).</span></span>

## <a name="file-paths"></a><span data-ttu-id="7d05b-130">文件路径</span><span class="sxs-lookup"><span data-stu-id="7d05b-130">File Paths</span></span>

<span data-ttu-id="7d05b-131">在使用相对路径并创建指向其他文档集的链接时，在文档中设置超链接的有效文件路径非常重要。</span><span class="sxs-lookup"><span data-stu-id="7d05b-131">When using relative paths and creating links to other docsets, it is important to set a valid file path for hyperlinks in your documentation.</span></span> <span data-ttu-id="7d05b-132">只有在文件路径正确GitHub，你的生成才成功。</span><span class="sxs-lookup"><span data-stu-id="7d05b-132">Your build succeeds on GitHub only if the file path is correct or valid.</span></span>
 
<span data-ttu-id="7d05b-133">有关超链接和文件路径详细信息，请参阅 [文档中的链接](/contribute/how-to-write-links)。</span><span class="sxs-lookup"><span data-stu-id="7d05b-133">For more information on hyperlinks and file paths, see [use links in documentation](/contribute/how-to-write-links).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7d05b-134">若要引用属于以下平台 **文档** 集Teams文章：</span><span class="sxs-lookup"><span data-stu-id="7d05b-134">To reference an article that is **part of** the Teams platform docset:</span></span><br>
> <span data-ttu-id="7d05b-135">&emsp;&#x2714; 使用不带前导正斜杠的相对路径。</span><span class="sxs-lookup"><span data-stu-id="7d05b-135">&emsp;&#x2714; Use a relative path without a leading forward slash.</span></span><br>
> <span data-ttu-id="7d05b-136">&emsp;&#x2714;包括 Markdown 文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="7d05b-136">&emsp;&#x2714; Include the Markdown file extension.</span></span><br>
><span data-ttu-id="7d05b-137">例如 **：父目录/目录/路径到** article.md —>[生成适用于Microsoft Teams](../concepts/building-an-app.md)</span><span class="sxs-lookup"><span data-stu-id="7d05b-137">Ex:  **parent directory/directory/path-to-article.md** —> [Building an app for Microsoft Teams](../concepts/building-an-app.md)</span></span> <br><br>
> <span data-ttu-id="7d05b-138">若要引用一篇 Microsoft Docs **库文章，** 该文章不是 Teams文档集的一部分：</span><span class="sxs-lookup"><span data-stu-id="7d05b-138">To reference a Microsoft Docs library article that **is not part of** the Teams platform docset:</span></span><br>
> <span data-ttu-id="7d05b-139">&emsp;&#x2714; 使用以正斜杠开头的相对路径。</span><span class="sxs-lookup"><span data-stu-id="7d05b-139">&emsp;&#x2714; Use a relative path that begins with a forward slash.</span></span><br>
> <span data-ttu-id="7d05b-140">&emsp;&#x2714;不包括文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="7d05b-140">&emsp;&#x2714; Do not include the file extension.</span></span> <br> <span data-ttu-id="7d05b-141">例如 **：/docset/address-to-file-location** — > [Microsoft Graph API 处理Microsoft Teams](/graph/api/resources/teams-api-overview)</span><span class="sxs-lookup"><span data-stu-id="7d05b-141">Ex:  **/docset/address-to-file-location** —> [Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)</span></span><br><br>
> <span data-ttu-id="7d05b-142">若要引用 Microsoft Docs 库外部的页面，GitHub，请使用完整的 `https` 文件路径。</span><span class="sxs-lookup"><span data-stu-id="7d05b-142">To reference a page outside of the Microsoft Docs library, such as GitHub, use the full `https` file path.</span></span><br>

## <a name="code-samples-and-snippets"></a><span data-ttu-id="7d05b-143">代码示例和代码段</span><span class="sxs-lookup"><span data-stu-id="7d05b-143">Code Samples and Snippets</span></span>

<span data-ttu-id="7d05b-144">代码示例在有效地使用 API 和 SDK 方面起到重要作用。</span><span class="sxs-lookup"><span data-stu-id="7d05b-144">Code samples play an important role to use APIs and SDKs effectively.</span></span> <span data-ttu-id="7d05b-145">良好的代码示例可以比描述性文本和说明性信息更加清楚地传达工作方式。</span><span class="sxs-lookup"><span data-stu-id="7d05b-145">Well presented code samples can communicate how things work more clearly than descriptive text and instructional information alone.</span></span> <span data-ttu-id="7d05b-146">您的代码示例必须准确、简洁、记录良好且读者友好。</span><span class="sxs-lookup"><span data-stu-id="7d05b-146">Your code samples must be accurate, concise, well documented, and reader friendly.</span></span> <span data-ttu-id="7d05b-147">易于阅读的代码必须易于理解、测试、调试、维护、修改和扩展。</span><span class="sxs-lookup"><span data-stu-id="7d05b-147">Code that is easy to read must be easy to understand, test, debug, maintain, modify, and extend.</span></span> <span data-ttu-id="7d05b-148">有关详细信息，请参阅 [如何在文档中包括代码](/contribute/code-in-docs)。</span><span class="sxs-lookup"><span data-stu-id="7d05b-148">For more information, see [how to include code in docs](/contribute/code-in-docs).</span></span>

## <a name="see-also"></a><span data-ttu-id="7d05b-149">另请参阅</span><span class="sxs-lookup"><span data-stu-id="7d05b-149">See also</span></span>

* [<span data-ttu-id="7d05b-150">Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="7d05b-150">Microsoft Docs</span></span>](/)
* [<span data-ttu-id="7d05b-151">参与者指南</span><span class="sxs-lookup"><span data-stu-id="7d05b-151">contributors guide</span></span>](/contribute)
* [<span data-ttu-id="7d05b-152">文档样式和语音快速入门</span><span class="sxs-lookup"><span data-stu-id="7d05b-152">Docs style and voice quick start</span></span>](/contribute/style-quick-start)
* [<span data-ttu-id="7d05b-153">剪切边缘：源代码可读使用技巧</span><span class="sxs-lookup"><span data-stu-id="7d05b-153">Cutting Edge : Source Code Readability Tips</span></span>](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)
* [<span data-ttu-id="7d05b-154">Teams文档</span><span class="sxs-lookup"><span data-stu-id="7d05b-154">Teams documentation</span></span>](/microsoftteams/platform/overview)
* [<span data-ttu-id="7d05b-155">GitHub</span><span class="sxs-lookup"><span data-stu-id="7d05b-155">GitHub</span></span>](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)


## <a name="next-step"></a><span data-ttu-id="7d05b-156">后续步骤</span><span class="sxs-lookup"><span data-stu-id="7d05b-156">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7d05b-157">获取 Microsoft Docs 更新和最新公告</span><span class="sxs-lookup"><span data-stu-id="7d05b-157">Get Microsoft Docs updates and the latest announcements</span></span>](/teamblog)
