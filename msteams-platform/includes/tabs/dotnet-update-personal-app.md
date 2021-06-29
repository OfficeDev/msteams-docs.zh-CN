## <a name="update-your-application"></a><span data-ttu-id="0b46f-101">更新应用程序</span><span class="sxs-lookup"><span data-stu-id="0b46f-101">Update your application</span></span>

### <a name="_layoutcshtml"></a><span data-ttu-id="0b46f-102">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="0b46f-102">_Layout.cshtml</span></span>

<span data-ttu-id="0b46f-103">若要在页面中显示选项卡Teams，必须包含 **Microsoft Teams JavaScript** 客户端 SDK，并包括页面加载 `microsoftTeams.initialize()` 后对 的调用。</span><span class="sxs-lookup"><span data-stu-id="0b46f-103">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="0b46f-104">这是选项卡与应用Teams方式：</span><span class="sxs-lookup"><span data-stu-id="0b46f-104">This is how your tab and the Teams app communicate:</span></span>

<span data-ttu-id="0b46f-105">转到" **共享"** 文件夹，打开 **_Layout.cshtml，** 然后向 `<head>` 标记部分添加以下内容：</span><span class="sxs-lookup"><span data-stu-id="0b46f-105">Go to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tags section:</span></span>

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

### <a name="personaltabcshtml"></a><span data-ttu-id="0b46f-106">PersonalTab.cshtml</span><span class="sxs-lookup"><span data-stu-id="0b46f-106">PersonalTab.cshtml</span></span>

<span data-ttu-id="0b46f-107">打开 **PersonalTab.cshtml，** 然后通过调用 `<script>` 更新嵌入标记 `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="0b46f-107">Open **PersonalTab.cshtml** and update the embedded `<script>` tags by calling `microsoftTeams.initialize()`.</span></span>

<span data-ttu-id="0b46f-108">确保保存已更新的 **PersonalTab.cshtml** 文件。</span><span class="sxs-lookup"><span data-stu-id="0b46f-108">Ensure you save your updated **PersonalTab.cshtml** file.</span></span>