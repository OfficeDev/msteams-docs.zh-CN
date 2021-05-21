---
title: Upload自定义应用
description: 了解如何在应用中旁加载Microsoft Teams。 在开发期间测试和调试应用时，旁加载很常见。
ms.topic: how-to
author: KirtiPereira
ms.author: surbhigupta
ms.openlocfilehash: 39e94317ceb615ecd7d5481276ffafed5afe5cde
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565191"
---
# <a name="upload-your-app-in-microsoft-teams"></a><span data-ttu-id="fcb34-104">Upload应用Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="fcb34-104">Upload your app in Microsoft Teams</span></span>

<span data-ttu-id="fcb34-105">你可以旁加载Microsoft Teams应用，而无需发布到你的组织或Teams应用商店。</span><span class="sxs-lookup"><span data-stu-id="fcb34-105">You can sideload Microsoft Teams apps without having to publish to your organization or the Teams store.</span></span> <span data-ttu-id="fcb34-106">在下列情况下，这是有意义的：</span><span class="sxs-lookup"><span data-stu-id="fcb34-106">This makes sense in the following scenarios:</span></span>

* <span data-ttu-id="fcb34-107">你想要自己或与其他开发人员一起在本地测试和调试应用。</span><span class="sxs-lookup"><span data-stu-id="fcb34-107">You want to test and debug an app locally yourself or with other developers.</span></span>
* <span data-ttu-id="fcb34-108">你只为自己生成了一个应用。</span><span class="sxs-lookup"><span data-stu-id="fcb34-108">You built an app just for yourself.</span></span> <span data-ttu-id="fcb34-109">例如，自动化工作流。</span><span class="sxs-lookup"><span data-stu-id="fcb34-109">For example, to automate a workflow.</span></span>
* <span data-ttu-id="fcb34-110">你为一小组用户（如工作组）生成了一个应用。</span><span class="sxs-lookup"><span data-stu-id="fcb34-110">You built an app for a small set of users, such as, your work group.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcb34-111">先决条件</span><span class="sxs-lookup"><span data-stu-id="fcb34-111">Prerequisites</span></span>

* <span data-ttu-id="fcb34-112">创建[应用包并](~/concepts/build-and-test/apps-package.md)[验证其](https://dev.teams.microsoft.com/appvalidation.html)是否出错。</span><span class="sxs-lookup"><span data-stu-id="fcb34-112">Create your [app package](~/concepts/build-and-test/apps-package.md) and [validate it](https://dev.teams.microsoft.com/appvalidation.html) for errors.</span></span>
* <span data-ttu-id="fcb34-113">[在应用中启用自定义](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)Teams。</span><span class="sxs-lookup"><span data-stu-id="fcb34-113">[Enable custom app uploading](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) in Teams.</span></span>
* <span data-ttu-id="fcb34-114">确保你的应用正在运行，并且可通过 HTTPs 访问。</span><span class="sxs-lookup"><span data-stu-id="fcb34-114">Make sure that your app is running and accessible via HTTPs.</span></span>

## <a name="upload-your-app"></a><span data-ttu-id="fcb34-115">上传应用</span><span class="sxs-lookup"><span data-stu-id="fcb34-115">Upload your app</span></span>

<span data-ttu-id="fcb34-116">你可以将应用旁加载至团队、聊天、会议或个人使用，具体取决于你配置应用的范围。</span><span class="sxs-lookup"><span data-stu-id="fcb34-116">You can sideload your app to a team, chat, meeting, or for personal use depending on how you configured your app's scope.</span></span>

1. <span data-ttu-id="fcb34-117">使用你的Teams帐户登录到[Microsoft 365 客户端](~/build-your-first-app/build-and-run.md#prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="fcb34-117">Log in to the Teams client with your [Microsoft 365 development account](~/build-your-first-app/build-and-run.md#prerequisites).</span></span>
1. <span data-ttu-id="fcb34-118">选择 **应用**，然后选择 **Upload自定义应用。**</span><span class="sxs-lookup"><span data-stu-id="fcb34-118">Select **Apps** and choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="fcb34-119">选择应用包.zip文件。</span><span class="sxs-lookup"><span data-stu-id="fcb34-119">Select your app package .zip file.</span></span> <span data-ttu-id="fcb34-120">将显示安装对话框。</span><span class="sxs-lookup"><span data-stu-id="fcb34-120">An install dialog displays.</span></span>
:::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="Screenshot showing an example of a Teams app install dialog.":::
1. <span data-ttu-id="fcb34-122">将应用添加到Teams。</span><span class="sxs-lookup"><span data-stu-id="fcb34-122">Add your app to Teams.</span></span>

## <a name="troubleshoot-upload-issues"></a><span data-ttu-id="fcb34-123">上传问题疑难解答</span><span class="sxs-lookup"><span data-stu-id="fcb34-123">Troubleshoot upload issues</span></span>

<span data-ttu-id="fcb34-124">如果应用无法旁加载，请执行下列操作，直到问题解决：</span><span class="sxs-lookup"><span data-stu-id="fcb34-124">If your app fails to sideload, do the following until the issue resolves:</span></span>

1. <span data-ttu-id="fcb34-125">返回创建应用 [包的说明](../../concepts/build-and-test/apps-package.md)。</span><span class="sxs-lookup"><span data-stu-id="fcb34-125">Go back through the instructions for [creating your app package](../../concepts/build-and-test/apps-package.md).</span></span>
1. <span data-ttu-id="fcb34-126">[再次验证应用](https://dev.teams.microsoft.com/appvalidation.html) 包。</span><span class="sxs-lookup"><span data-stu-id="fcb34-126">[Validate your app package](https://dev.teams.microsoft.com/appvalidation.html) again.</span></span>
1. <span data-ttu-id="fcb34-127">确保你的应用清单与最新的架构 [匹配](../../resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="fcb34-127">Make sure your app manifest matches the latest [schema](../../resources/schema/manifest-schema.md).</span></span>

## <a name="access-your-app"></a><span data-ttu-id="fcb34-128">访问应用</span><span class="sxs-lookup"><span data-stu-id="fcb34-128">Access your app</span></span>

<span data-ttu-id="fcb34-129">Teams提供了几种打开应用的方法。</span><span class="sxs-lookup"><span data-stu-id="fcb34-129">Teams provides several ways to open apps.</span></span> <span data-ttu-id="fcb34-130">有关详细信息，请参阅访问[Teams 中的应用程序](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a)。</span><span class="sxs-lookup"><span data-stu-id="fcb34-130">For more information, see [access your apps in Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).</span></span>

## <a name="update-your-app"></a><span data-ttu-id="fcb34-131">更新应用</span><span class="sxs-lookup"><span data-stu-id="fcb34-131">Update your app</span></span>

<span data-ttu-id="fcb34-132">如果你对代码进行更改，则不必再次旁加载你的应用 (这些更改会Teams实时) 。</span><span class="sxs-lookup"><span data-stu-id="fcb34-132">You don't have to sideload your app again if you make code changes (these are reflected in Teams in real-time).</span></span> <span data-ttu-id="fcb34-133">但是，如果更改任何应用配置，则必须重新安装。</span><span class="sxs-lookup"><span data-stu-id="fcb34-133">However, you must reinstall if you change any app configurations.</span></span>

## <a name="remove-your-app"></a><span data-ttu-id="fcb34-134">删除应用</span><span class="sxs-lookup"><span data-stu-id="fcb34-134">Remove your app</span></span>

<span data-ttu-id="fcb34-135">若要删除你的应用，请右键单击应用中Teams **并选择卸载**。</span><span class="sxs-lookup"><span data-stu-id="fcb34-135">To remove your app, right click the app icon in Teams and select **Uninstall**.</span></span>

> [!NOTE]
> <span data-ttu-id="fcb34-136">你无法完全删除个人自动程序活动。</span><span class="sxs-lookup"><span data-stu-id="fcb34-136">You can't remove personal bot activity entirely.</span></span> <span data-ttu-id="fcb34-137">如果删除应用并再次添加它，则与机器人的新通信将附加到其上一次对话中。</span><span class="sxs-lookup"><span data-stu-id="fcb34-137">If you remove the app and add it again, new communication with the bot appends to the previous conversation with it.</span></span>

## <a name="next-step"></a><span data-ttu-id="fcb34-138">后续步骤</span><span class="sxs-lookup"><span data-stu-id="fcb34-138">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fcb34-139">使用Teams应用</span><span class="sxs-lookup"><span data-stu-id="fcb34-139">Use your Teams app</span></span>](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)
