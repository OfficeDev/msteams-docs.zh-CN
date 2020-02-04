## <a name="update-your-application"></a><span data-ttu-id="4c4d7-101">更新应用程序</span><span class="sxs-lookup"><span data-stu-id="4c4d7-101">Update your application</span></span>

### <a name="_layoutcshtml"></a><span data-ttu-id="4c4d7-102">_Layout cshtml</span><span class="sxs-lookup"><span data-stu-id="4c4d7-102">_Layout.cshtml</span></span>

<span data-ttu-id="4c4d7-103">若要在团队中显示您的选项卡，您必须包含**Microsoft 团队 JavaScript 客户端 SDK** ，并`microsoftTeams.initialize()`在加载页面后包含一个调用。</span><span class="sxs-lookup"><span data-stu-id="4c4d7-103">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="4c4d7-104">这就是您的选项卡和团队应用程序的通信方式：</span><span class="sxs-lookup"><span data-stu-id="4c4d7-104">This is how your tab and the Teams app communicate:</span></span>

- <span data-ttu-id="4c4d7-105">导航到**共享**文件夹，打开 **_Layout. cshtml**，并将以下内容添加到 " `<head>`标签" 部分：</span><span class="sxs-lookup"><span data-stu-id="4c4d7-105">Navigate to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tags section:</span></span>

```html
`<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>`
`<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>`
```

### <a name="personaltabcshtml"></a><span data-ttu-id="4c4d7-106">PersonalTab</span><span class="sxs-lookup"><span data-stu-id="4c4d7-106">PersonalTab.cshtml</span></span>

<span data-ttu-id="4c4d7-107">打开**PersonalTab** ，并通过调用`<script>` `microsoftTeams.initialize()`更新嵌入的标记。</span><span class="sxs-lookup"><span data-stu-id="4c4d7-107">Open **PersonalTab.cshtml** and update the embedded `<script>` tags by calling `microsoftTeams.initialize()`.</span></span>

<span data-ttu-id="4c4d7-108">请务必保存更新后的*PersonalTab*。</span><span class="sxs-lookup"><span data-stu-id="4c4d7-108">Make sure to save your updated *PersonalTab.cshtml*.</span></span>