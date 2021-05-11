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
# <a name="contributing-to-microsoft-teams-documentation"></a><span data-ttu-id="ded00-103">参与Microsoft Teams文档</span><span class="sxs-lookup"><span data-stu-id="ded00-103">Contributing to Microsoft Teams documentation</span></span>

<span data-ttu-id="ded00-104">[Teams文档](/microsoftteams/platform/overview)是[Microsoft Docs 技术](https://docs.microsoft.com/)文档库的一部分。</span><span class="sxs-lookup"><span data-stu-id="ded00-104">[Teams documentation](/microsoftteams/platform/overview) is part of the [Microsoft Docs](https://docs.microsoft.com/) technical documentation library.</span></span> <span data-ttu-id="ded00-105">内容分为多个组，称为文档集，每个组表示作为单个实体管理的一组相关文档。</span><span class="sxs-lookup"><span data-stu-id="ded00-105">The content is organized into groups called docsets, each representing a group of related documents managed as a single entity.</span></span> <span data-ttu-id="ded00-106">同一文档集内的文章在 *docs <span></span> .microsoft.com 之后具有相同的* URL 路径 microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="ded00-106">Articles in the same docset have the same URL path extension after *docs<span></span>.microsoft.com*.</span></span>  <span data-ttu-id="ded00-107">例如， `/docs.microsoft.com/microsoftteams/...` 是文档Teams路径的开头。</span><span class="sxs-lookup"><span data-stu-id="ded00-107">For example,  `/docs.microsoft.com/microsoftteams/...`   is the beginning of the Teams docset file path.</span></span> <span data-ttu-id="ded00-108">Teams文章以[MarkDown](#markdown-reference)语法编写，并托管在 GitHub[上](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)。</span><span class="sxs-lookup"><span data-stu-id="ded00-108">Teams articles are written in  [MarkDown](#markdown-reference) syntax and hosted on [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform).</span></span>

## <a name="set-up-your-workspace"></a><span data-ttu-id="ded00-109">设置工作区</span><span class="sxs-lookup"><span data-stu-id="ded00-109">Set up your workspace</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="ded00-110">安装 [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)。</span><span class="sxs-lookup"><span data-stu-id="ded00-110">Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).</span></span>
> * <span data-ttu-id="ded00-111">安装[Visual Studio Code (VS Code) 。](https://code.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="ded00-111">Install [Visual Studio Code](https://code.visualstudio.com/) (VS Code).</span></span>
> * <span data-ttu-id="ded00-112">直接从[应用商店安装](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack)文档VS Code包</span><span class="sxs-lookup"><span data-stu-id="ded00-112">Install [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directly from the VS Code Marketplace</span></span>
<br><span data-ttu-id="ded00-113">&emsp;&emsp; 或</span><span class="sxs-lookup"><span data-stu-id="ded00-113">&emsp;&emsp; or</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="ded00-114">从安装VS Code：</span><span class="sxs-lookup"><span data-stu-id="ded00-114">Install from within VS Code:</span></span>

   1. <span data-ttu-id="ded00-115">选择侧活动栏上的"扩展"图标或使用"视图 **=>** 扩展"命令 (Ctrl+Shift+X) 并搜索 Microsoft) 文档创作包 (。</span><span class="sxs-lookup"><span data-stu-id="ded00-115">Select the **Extensions icon** on the side activity bar or use the **View => Extensions** command (Ctrl+Shift+X) and search for the *Docs Authoring Pack* (Microsoft).</span></span>
   1. <span data-ttu-id="ded00-116">选择" **安装"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="ded00-116">Select the **Install** button.</span></span>
   1. <span data-ttu-id="ded00-117">安装完成后，" **安装"** 按钮将更改为" **管理齿轮"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="ded00-117">Once installation is complete, the **Install** button will change to the **Manage** gear button.</span></span>

## <a name="review-the-microsoft-docs-contributors-guide"></a><span data-ttu-id="ded00-118">查看 Microsoft Docs Contributors 指南</span><span class="sxs-lookup"><span data-stu-id="ded00-118">Review the Microsoft Docs Contributors Guide</span></span>

<span data-ttu-id="ded00-119">参与者 [指南](/contribute) 提供了在 Microsoft Docs 平台上创建、发布和更新技术内容的指导。</span><span class="sxs-lookup"><span data-stu-id="ded00-119">The [contributors guide](/contribute) offers direction for creating, publishing, and updating technical content on the Microsoft Docs platform.</span></span> <span data-ttu-id="ded00-120">*另请参阅* 文档 [样式和语音快速入门](/contribute/style-quick-start) 。</span><span class="sxs-lookup"><span data-stu-id="ded00-120">*See also*, [Docs style and voice quick start](/contribute/style-quick-start) .</span></span>

## <a name="microsoft-writing-style-and-content-guides"></a><span data-ttu-id="ded00-121">Microsoft 编写、样式和内容指南</span><span class="sxs-lookup"><span data-stu-id="ded00-121">Microsoft Writing, Style, and Content Guides</span></span>

* <span data-ttu-id="ded00-122">**[Microsoft 写作风格指南](/style-guide/welcome)**。</span><span class="sxs-lookup"><span data-stu-id="ded00-122">**[Microsoft Writing Style Guide](/style-guide/welcome)**.</span></span> <span data-ttu-id="ded00-123">请考虑将此联机指南添加到浏览器 **的收藏夹** 菜单。</span><span class="sxs-lookup"><span data-stu-id="ded00-123">Consider adding this online guide  to your browser's **Favorites** menu.</span></span> <span data-ttu-id="ded00-124">它是当今技术写作的全面资源，反映了 Microsoft 的新式语音和风格方法。</span><span class="sxs-lookup"><span data-stu-id="ded00-124">It is a comprehensive resource for today's technical writing and reflects Microsoft's modern approach to voice and style.</span></span>

* <span data-ttu-id="ded00-125">**[编写开发人员内容](/style-guide/developer-content/)**。</span><span class="sxs-lookup"><span data-stu-id="ded00-125">**[Writing developer content](/style-guide/developer-content/)**.</span></span> <span data-ttu-id="ded00-126">Teams内容面向对编程概念和过程有基本了解的开发人员受众。</span><span class="sxs-lookup"><span data-stu-id="ded00-126">Teams-specific content is aimed at a developer audience with a fundamental understanding of programming concepts and processes.</span></span> <span data-ttu-id="ded00-127">在保持 Microsoft 的声调和风格的同时，以引人注目的方式提供清晰、技术准确的信息非常重要。</span><span class="sxs-lookup"><span data-stu-id="ded00-127">It is important that you provide clear, technically-accurate information in a compelling manner while maintaining Microsoft's tone and style.</span></span>

* <span data-ttu-id="ded00-128">**[编写分步说明](/style-guide/procedures-instructions/writing-step-by-step-instructions)**。</span><span class="sxs-lookup"><span data-stu-id="ded00-128">**[Writing step-by-step instructions](/style-guide/procedures-instructions/writing-step-by-step-instructions)**.</span></span> <span data-ttu-id="ded00-129">应用和交互式体验是开发人员了解 Microsoft 产品和技术的一种很好的方法。</span><span class="sxs-lookup"><span data-stu-id="ded00-129">Applied and interactive experiences are a great way for developers to learn about Microsoft products and technologies.</span></span> <span data-ttu-id="ded00-130">以渐进格式呈现复杂或简单的过程很自然且用户友好。</span><span class="sxs-lookup"><span data-stu-id="ded00-130">Presenting complex or simple procedures in a progressive format is natural and user-friendly.</span></span>

## <a name="markdown-reference"></a><span data-ttu-id="ded00-131">MarkDown 参考</span><span class="sxs-lookup"><span data-stu-id="ded00-131">MarkDown reference</span></span>

 <span data-ttu-id="ded00-132">Microsoft Docs 页面使用 MarkDown 语法编写并通过 [Markdig](https://github.com/lunet-io/markdig) 引擎进行分析。</span><span class="sxs-lookup"><span data-stu-id="ded00-132">Microsoft Docs pages are written in MarkDown syntax and parsed through a [Markdig](https://github.com/lunet-io/markdig) engine.</span></span> <span data-ttu-id="ded00-133">请参阅 *特定*[标记和](/contribute/markdown-reference)格式约定的文档 Markdown 参考。</span><span class="sxs-lookup"><span data-stu-id="ded00-133">Please *see* [Docs Markdown reference](/contribute/markdown-reference) for specific tags and formatting conventions.</span></span>

## <a name="file-paths"></a><span data-ttu-id="ded00-134">文件路径</span><span class="sxs-lookup"><span data-stu-id="ded00-134">File Paths</span></span>

<span data-ttu-id="ded00-135">为文档中的超链接设置有效的文件路径可能是一项挑战，尤其是在使用相对路径和创建指向其他文档集的链接时。</span><span class="sxs-lookup"><span data-stu-id="ded00-135">Setting a valid file path for hyperlinks in your documentation can be a challenge, especially when using relative paths and creating links to other docsets.</span></span>  <span data-ttu-id="ded00-136">如果文件路径不正确或无效GitHub生成将不会成功。</span><span class="sxs-lookup"><span data-stu-id="ded00-136">Your build won't succeed on GitHub if the file path is incorrect or invalid.</span></span>

<span data-ttu-id="ded00-137">有关超链接和文件路径详细信息，请参阅 *使用*[文档中的链接](/contribute/how-to-write-links)。</span><span class="sxs-lookup"><span data-stu-id="ded00-137">For more information on  hyperlinks and file paths, please *see* [Use links in documentation](/contribute/how-to-write-links).</span></span>

>[!IMPORTANT]
> <span data-ttu-id="ded00-138">若要引用属于以下平台 *文档* 集Teams文章：</span><span class="sxs-lookup"><span data-stu-id="ded00-138">To reference an article that is *part of* the Teams platform docset:</span></span><br>
> <span data-ttu-id="ded00-139">&emsp;&#x2714; 使用不带前导正斜杠的相对路径。</span><span class="sxs-lookup"><span data-stu-id="ded00-139">&emsp;&#x2714; Use a relative path without a leading forward slash.</span></span><br>
> <span data-ttu-id="ded00-140">&emsp;&#x2714;包括 Markdown 文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="ded00-140">&emsp;&#x2714; Include the Markdown file extension.</span></span><br>
><span data-ttu-id="ded00-141">例如  **：父目录/目录/路径到 article.md** —> `[Building an app for Microsoft Teams](../concepts/building-an-app.md)`</span><span class="sxs-lookup"><span data-stu-id="ded00-141">Ex:  **parent directory/directory/path-to-article.md** —> `[Building an app for Microsoft Teams](../concepts/building-an-app.md)`</span></span> <br><br>
> <span data-ttu-id="ded00-142">若要引用一篇 Microsoft Docs *库文章，* 该文章不是 Teams文档集的一部分：</span><span class="sxs-lookup"><span data-stu-id="ded00-142">To reference a Microsoft Docs library article that *is not part of* the Teams platform docset:</span></span><br>
> <span data-ttu-id="ded00-143">&emsp;&#x2714; 使用以正斜杠开头的相对路径。</span><span class="sxs-lookup"><span data-stu-id="ded00-143">&emsp;&#x2714; Use a relative path that begins with a forward slash.</span></span><br>
> <span data-ttu-id="ded00-144">&emsp;&#x2714;不包括文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="ded00-144">&emsp;&#x2714; Don't include the file extension.</span></span> <br> <span data-ttu-id="ded00-145">例如  **：/docset/address-to-file-location** —> `[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`</span><span class="sxs-lookup"><span data-stu-id="ded00-145">Ex:  **/docset/address-to-file-location** —> `[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`</span></span><br><br>
> <span data-ttu-id="ded00-146">若要引用 Microsoft Docs 库外部的页面，GitHub，请使用完整的 `https` 文件路径。</span><span class="sxs-lookup"><span data-stu-id="ded00-146">To reference a page outside of the Microsoft Docs library, such as GitHub, use the full `https` file path.</span></span><br>

## <a name="code-samples-and-snippets"></a><span data-ttu-id="ded00-147">代码示例和代码段</span><span class="sxs-lookup"><span data-stu-id="ded00-147">Code Samples and Snippets</span></span>

<span data-ttu-id="ded00-148">代码示例在帮助开发人员成功使用 API 和 SDK 方面起到重要作用。</span><span class="sxs-lookup"><span data-stu-id="ded00-148">Code samples play an important role in helping developers successfully use APIs and SDKs.</span></span> <span data-ttu-id="ded00-149">呈现良好的代码示例可以比描述性文本和说明性信息更加清楚地传达工作方式。</span><span class="sxs-lookup"><span data-stu-id="ded00-149">Well-presented code samples can communicate how things work more clearly than descriptive text and instructional information alone.</span></span> <span data-ttu-id="ded00-150">您的代码示例应准确、简洁、记录良好，最重要的是，读者友好。</span><span class="sxs-lookup"><span data-stu-id="ded00-150">Your code samples should be accurate, concise, well-documented, and, most importantly, reader-friendly.</span></span> <span data-ttu-id="ded00-151">易于阅读的代码也易于理解、测试、调试、维护、修改和扩展。</span><span class="sxs-lookup"><span data-stu-id="ded00-151">Code that is easy-to-read is also easy to understand, test, debug, maintain, modify, and extend.</span></span> <span data-ttu-id="ded00-152">*请参阅*[如何在文档中包括代码](/contribute/code-in-docs)。有关可读性提示，另 *请参阅边缘*[：源代码可读性使用技巧。](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)</span><span class="sxs-lookup"><span data-stu-id="ded00-152">*See* [How to include code in docs](/contribute/code-in-docs). For readability tips, please *see also* [Cutting Edge : Source Code Readability Tips](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ded00-153">获取 Microsoft Docs 更新和最新公告</span><span class="sxs-lookup"><span data-stu-id="ded00-153">Get Microsoft Docs updates and the latest announcements</span></span>](/teamblog)
