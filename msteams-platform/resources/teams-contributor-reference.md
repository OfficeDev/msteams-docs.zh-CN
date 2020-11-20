---
title: 对 Microsoft 团队文档的贡献
description: 创建和发布团队文档的步骤
author: laujan
ms.author: lajanuar
ms.topic: contributor-guide
ms.openlocfilehash: 18aae61a674cf9c4c94831f22149cd4b9e7ebeda
ms.sourcegitcommit: 43e1be9d9e3651ce73a8d2139e44d75550a0ca60
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2020
ms.locfileid: "49366894"
---
# <a name="contributing-to-microsoft-teams-documentation"></a><span data-ttu-id="9a5d3-103">对 Microsoft 团队文档的贡献</span><span class="sxs-lookup"><span data-stu-id="9a5d3-103">Contributing to Microsoft Teams documentation</span></span>

<span data-ttu-id="9a5d3-104">[团队文档](/microsoftteams/platform/overview) 是 [Microsoft 文档](https://docs.microsoft.com/) 技术文档库的一部分。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-104">[Teams documentation](/microsoftteams/platform/overview) is part of the [Microsoft Docs](https://docs.microsoft.com/) technical documentation library.</span></span> <span data-ttu-id="9a5d3-105">内容被组织到名为 docsets 的组中，每个组代表一组作为单个实体管理的相关文档。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-105">The content is organized into groups called docsets, each representing a group of related documents managed as a single entity.</span></span> <span data-ttu-id="9a5d3-106">同一 docset 中的文章在 *<span></span> microsoft.com* 之后具有相同的 URL 路径扩展名。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-106">Articles in the same docset have the same URL path extension after *docs<span></span>.microsoft.com*.</span></span>  <span data-ttu-id="9a5d3-107">例如，  `/docs.microsoft.com/microsoftteams/...`   是团队 docset 文件路径的开头。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-107">For example,  `/docs.microsoft.com/microsoftteams/...`   is the beginning of the Teams docset file path.</span></span> <span data-ttu-id="9a5d3-108">团队文章以  [MarkDown](#markdown-reference) 语法编写，并托管在 [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)上。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-108">Teams articles are written in  [MarkDown](#markdown-reference) syntax and hosted on [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform).</span></span>

## <a name="set-up-your-workspace"></a><span data-ttu-id="9a5d3-109">设置你的工作区</span><span class="sxs-lookup"><span data-stu-id="9a5d3-109">Set up your workspace</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="9a5d3-110">安装 [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-110">Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).</span></span>
> * <span data-ttu-id="9a5d3-111">安装 [Visual Studio code](https://code.visualstudio.com/) (VS code) 。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-111">Install [Visual Studio Code](https://code.visualstudio.com/) (VS Code).</span></span>
> * <span data-ttu-id="9a5d3-112">直接从 VS 代码市场安装[文档创作包](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack)</span><span class="sxs-lookup"><span data-stu-id="9a5d3-112">Install [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directly from the VS Code Marketplace</span></span>
<br><span data-ttu-id="9a5d3-113">&emsp;&emsp; 和</span><span class="sxs-lookup"><span data-stu-id="9a5d3-113">&emsp;&emsp; or</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="9a5d3-114">从 VS 代码中进行安装：</span><span class="sxs-lookup"><span data-stu-id="9a5d3-114">Install from within VS Code:</span></span>

   1. <span data-ttu-id="9a5d3-115">选择侧活动栏上的 " **扩展" 图标** ，或使用 " **视图 => 扩展** " 命令 (Ctrl + Shift + X) 并搜索 *文档创作包* (Microsoft) 。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-115">Select the **Extensions icon** on the side activity bar or use the **View => Extensions** command (Ctrl+Shift+X) and search for the *Docs Authoring Pack* (Microsoft).</span></span>
   1. <span data-ttu-id="9a5d3-116">选择 " **安装** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-116">Select the **Install** button.</span></span>
   1. <span data-ttu-id="9a5d3-117">安装完成后，" **安装** " 按钮将更改为 " **管理** 齿轮" 按钮。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-117">Once installation is complete, the **Install** button will change to the **Manage** gear button.</span></span>

## <a name="review-the-microsoft-docs-contributors-guide"></a><span data-ttu-id="9a5d3-118">查看 Microsoft 文档 "参与者指南"</span><span class="sxs-lookup"><span data-stu-id="9a5d3-118">Review the Microsoft Docs Contributors Guide</span></span>

<span data-ttu-id="9a5d3-119">" [参与者指南](/contribute) " 提供了在 Microsoft 文档平台上创建、发布和更新技术内容的方向。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-119">The [contributors guide](/contribute) offers direction for creating, publishing, and updating technical content on the Microsoft Docs platform.</span></span> <span data-ttu-id="9a5d3-120">*另请参阅*[文档样式和语音快速入门](/contribute/style-quick-start)。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-120">*See also*, [Docs style and voice quick start](/contribute/style-quick-start) .</span></span>

## <a name="microsoft-writing-style-and-content-guides"></a><span data-ttu-id="9a5d3-121">Microsoft 写作、样式和内容指南</span><span class="sxs-lookup"><span data-stu-id="9a5d3-121">Microsoft Writing, Style, and Content Guides</span></span>

* <span data-ttu-id="9a5d3-122">**[Microsoft 写作风格指南](/style-guide/welcome)**。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-122">**[Microsoft Writing Style Guide](/style-guide/welcome)**.</span></span> <span data-ttu-id="9a5d3-123">请考虑将此联机指南添加到浏览器的 **"收藏夹"** 菜单。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-123">Consider adding this online guide  to your browser's **Favorites** menu.</span></span> <span data-ttu-id="9a5d3-124">它是今天的技术写作的综合资源，反映了 Microsoft 的新式语音和风格方法。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-124">It is a comprehensive resource for today's technical writing and reflects Microsoft's modern approach to voice and style.</span></span>

* <span data-ttu-id="9a5d3-125">**[编写开发人员内容](/style-guide/developer-content/)**。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-125">**[Writing developer content](/style-guide/developer-content/)**.</span></span> <span data-ttu-id="9a5d3-126">特定于团队的内容面向开发人员群体，对编程概念和过程有基本的了解。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-126">Teams-specific content is aimed at a developer audience with a fundamental understanding of programming concepts and processes.</span></span> <span data-ttu-id="9a5d3-127">在维护 Microsoft 的语气和样式的同时，以极具吸引力的方式提供清晰、技术上的信息，这一点非常重要。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-127">It is important that you provide clear, technically-accurate information in a compelling manner while maintaining Microsoft's tone and style.</span></span>

* <span data-ttu-id="9a5d3-128">**[编写分步说明](/style-guide/procedures-instructions/writing-step-by-step-instructions)**。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-128">**[Writing step-by-step instructions](/style-guide/procedures-instructions/writing-step-by-step-instructions)**.</span></span> <span data-ttu-id="9a5d3-129">应用程序和交互式体验是开发人员了解 Microsoft 产品和技术的一种非常好的方法。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-129">Applied and interactive experiences are a great way for developers to learn about Microsoft products and technologies.</span></span> <span data-ttu-id="9a5d3-130">以渐进格式呈现复杂或简单的过程是自然的，并且是用户友好的。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-130">Presenting complex or simple procedures in a progressive format is natural and user-friendly.</span></span>

## <a name="markdown-reference"></a><span data-ttu-id="9a5d3-131">MarkDown 参考</span><span class="sxs-lookup"><span data-stu-id="9a5d3-131">MarkDown reference</span></span>

 <span data-ttu-id="9a5d3-132">Microsoft 文档页面使用 MarkDown 语法编写，并通过 [Markdig](https://github.com/lunet-io/markdig) 引擎进行分析。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-132">Microsoft Docs pages are written in MarkDown syntax and parsed through a [Markdig](https://github.com/lunet-io/markdig) engine.</span></span> <span data-ttu-id="9a5d3-133">有关特定标记和格式设置约定，请 *参阅*[文档 Markdown 参考](/contribute/markdown-reference)。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-133">Please *see* [Docs Markdown reference](/contribute/markdown-reference) for specific tags and formatting conventions.</span></span>

## <a name="file-paths"></a><span data-ttu-id="9a5d3-134">文件路径</span><span class="sxs-lookup"><span data-stu-id="9a5d3-134">File Paths</span></span>

<span data-ttu-id="9a5d3-135">为文档中的超链接设置有效的文件路径可能是一项挑战，尤其是在使用相对路径和创建指向其他 docsets 的链接时。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-135">Setting a valid file path for hyperlinks in your documentation can be a challenge, especially when using relative paths and creating links to other docsets.</span></span>  <span data-ttu-id="9a5d3-136">如果文件路径不正确或无效，则您的内部版本将不会在 GitHub 上成功。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-136">Your build won't succeed on GitHub if the file path is incorrect or invalid.</span></span>

<span data-ttu-id="9a5d3-137">有关超链接和文件路径的详细信息，请 *参阅*[在文档中使用链接](/contribute/how-to-write-links)。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-137">For more information on  hyperlinks and file paths, please *see* [Use links in documentation](/contribute/how-to-write-links).</span></span>

>[!IMPORTANT]
> <span data-ttu-id="9a5d3-138">若要 *引用属于团队* 平台 docset 的文章，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="9a5d3-138">To reference an article that is *part of* the Teams platform docset:</span></span><br>
> <span data-ttu-id="9a5d3-139">&emsp;&#x2714; 使用不带前导正斜线的相对路径。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-139">&emsp;&#x2714; Use a relative path without a leading forward slash.</span></span><br>
> <span data-ttu-id="9a5d3-140">&emsp;&#x2714; 包括 Markdown 文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-140">&emsp;&#x2714; Include the Markdown file extension.</span></span><br>
><span data-ttu-id="9a5d3-141">Ex：  **父目录/目录/路径到文章** -> `[Building an app for Microsoft Teams](../concepts/building-an-app.md)`</span><span class="sxs-lookup"><span data-stu-id="9a5d3-141">Ex:  **parent directory/directory/path-to-article.md** —> `[Building an app for Microsoft Teams](../concepts/building-an-app.md)`</span></span> <br><br>
> <span data-ttu-id="9a5d3-142">若要引用 *不属于* 团队平台 Docset 的 Microsoft 文档库文章，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="9a5d3-142">To reference a Microsoft Docs library article that *is not part of* the Teams platform docset:</span></span><br>
> <span data-ttu-id="9a5d3-143">&emsp;&#x2714; 使用以正斜杠开头的相对路径。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-143">&emsp;&#x2714; Use a relative path that begins with a forward slash.</span></span><br>
> <span data-ttu-id="9a5d3-144">&emsp;&#x2714; 不包括文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-144">&emsp;&#x2714; Don't include the file extension.</span></span> <br> <span data-ttu-id="9a5d3-145">Ex：  **/docset/address-to-file-location** — > `[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`</span><span class="sxs-lookup"><span data-stu-id="9a5d3-145">Ex:  **/docset/address-to-file-location** —> `[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`</span></span><br><br>
> <span data-ttu-id="9a5d3-146">若要引用 Microsoft 文档库外部的页面（例如 GitHub），请使用完整 `https` 文件路径。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-146">To reference a page outside of the Microsoft Docs library, such as GitHub, use the full `https` file path.</span></span><br>

## <a name="code-samples-and-snippets"></a><span data-ttu-id="9a5d3-147">代码示例和代码段</span><span class="sxs-lookup"><span data-stu-id="9a5d3-147">Code Samples and Snippets</span></span>

<span data-ttu-id="9a5d3-148">代码示例在帮助开发人员成功使用 Api 和 Sdk 方面起着重要作用。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-148">Code samples play an important role in helping developers successfully use APIs and SDKs.</span></span> <span data-ttu-id="9a5d3-149">我们提供的代码示例可以传达与描述性文本和说明信息更清晰的工作方式。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-149">Well-presented code samples can communicate how things work more clearly than descriptive text and instructional information alone.</span></span> <span data-ttu-id="9a5d3-150">您的代码示例应准确、简洁、记录良好，并且最重要的是读者友好。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-150">Your code samples should be accurate, concise, well-documented, and, most importantly, reader-friendly.</span></span> <span data-ttu-id="9a5d3-151">易于阅读的代码也易于理解、测试、调试、维护、修改和扩展。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-151">Code that is easy-to-read is also easy to understand, test, debug, maintain, modify, and extend.</span></span> <span data-ttu-id="9a5d3-152">*请参阅*[如何在文档中包含代码](/contribute/code-in-docs)。有关可读性的提示，请 *参阅*[剪切边缘：源代码可读性提示](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)。</span><span class="sxs-lookup"><span data-stu-id="9a5d3-152">*See* [How to include code in docs](/contribute/code-in-docs). For readability tips, please *see also* [Cutting Edge : Source Code Readability Tips](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9a5d3-153">获取 Microsoft 文档更新和最新通知</span><span class="sxs-lookup"><span data-stu-id="9a5d3-153">Get Microsoft Docs updates and the latest announcements</span></span>](/teamblog)
