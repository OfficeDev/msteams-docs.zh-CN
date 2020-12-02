1. <span data-ttu-id="66fd3-101">在 [Azure 门户](https://ms.portal.azure.com/#home)的“Azure 服务”下，选择“**创建资源**”。</span><span class="sxs-lookup"><span data-stu-id="66fd3-101">In the [Azure portal](https://ms.portal.azure.com/#home), under Azure services, select **Create a resource**.</span></span>
1. <span data-ttu-id="66fd3-102">在搜索框中，输入“机器人”。</span><span class="sxs-lookup"><span data-stu-id="66fd3-102">In the search box enter "bot".</span></span> <span data-ttu-id="66fd3-103">在下拉列表中，选择“**机器人频道注册**”。</span><span class="sxs-lookup"><span data-stu-id="66fd3-103">And in the drop-down list, select **Bot Channels Registration**.</span></span>
1. <span data-ttu-id="66fd3-104">选择“**创建**”按钮。</span><span class="sxs-lookup"><span data-stu-id="66fd3-104">Select the **Create** button.</span></span>
1. <span data-ttu-id="66fd3-105">在“**机器人频道注册**”边栏选项卡中，提供有关机器人的所需信息。</span><span class="sxs-lookup"><span data-stu-id="66fd3-105">In the **Bot Channel Registration** blade, provide the requested information about your bot.</span></span>
1. <span data-ttu-id="66fd3-106">暂时将“**消息传递终结点**”框留空，你需要在部署机器人后输入所需的 URL。</span><span class="sxs-lookup"><span data-stu-id="66fd3-106">Leave the **Messaging endpoint** box empty for now, you will enter the required URL after deploying the bot.</span></span> <span data-ttu-id="66fd3-107">下图显示了注册设置的示例：</span><span class="sxs-lookup"><span data-stu-id="66fd3-107">The following picture shows an example of the registration settings:</span></span>

    ![机器人应用频道注册](../../assets/images/authentication/auth-bot-channels-registration.png)

1. <span data-ttu-id="66fd3-109">单击“**Microsoft 应用 ID 和密码**”，然后单击“**新建**”。</span><span class="sxs-lookup"><span data-stu-id="66fd3-109">Click **Microsoft App ID and password** and then **Create New**.</span></span>

    <span data-ttu-id="66fd3-110">![创建 Microsoft 应用 ID](../../assets/images/authentication/CreateMicrosoftAppID.png) ![创建新的 Microsoft 应用 ID](../../assets/images/authentication/CreateNewMicrosoftAppID.png)</span><span class="sxs-lookup"><span data-stu-id="66fd3-110">![Create Microsoft App ID](../../assets/images/authentication/CreateMicrosoftAppID.png) ![Create New Microsoft App ID](../../assets/images/authentication/CreateNewMicrosoftAppID.png)</span></span>    

1. <span data-ttu-id="66fd3-111">单击“**在应用注册门户中创建应用 ID**”链接。</span><span class="sxs-lookup"><span data-stu-id="66fd3-111">Click **Create App ID in the App Registration Portal** link.</span></span>

   ![应用注册](../../assets/images/authentication/AppRegistration.png)
   
1. <span data-ttu-id="66fd3-113">在显示的“**应用注册**”窗口中，单击左上角的“**新建注册**”选项卡。</span><span class="sxs-lookup"><span data-stu-id="66fd3-113">In the displayed **App registration** window, click the **New registration** tab in the upper left.</span></span>
1. <span data-ttu-id="66fd3-114">输入要注册的机器人应用程序的名称，我们使用 *BotTeamsAuth*（你需要选择自己的唯一名称）。</span><span class="sxs-lookup"><span data-stu-id="66fd3-114">Enter the name of the bot application you are registering, we used *BotTeamsAuth* (you need to select your own unique name).</span></span>
1. <span data-ttu-id="66fd3-115">对于“**受支持的帐户类型**”，选择“*任何组织目录(任何 Azure AD 目录 - 多租户)中的帐户和个人 Microsoft 帐户(例如 Skype、Xbox)*”。</span><span class="sxs-lookup"><span data-stu-id="66fd3-115">For the **Supported account types** select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
1. <span data-ttu-id="66fd3-116">单击“**注册**”按钮。</span><span class="sxs-lookup"><span data-stu-id="66fd3-116">Click the **Register** button.</span></span> <span data-ttu-id="66fd3-117">完成后，Azure 将显示应用程序的“*概述*”页面。</span><span class="sxs-lookup"><span data-stu-id="66fd3-117">Once completed, Azure displays the *Overview* page for the application.</span></span>
1. <span data-ttu-id="66fd3-118">复制“**应用程序(客户端) ID**”值并将其保存到文件中。</span><span class="sxs-lookup"><span data-stu-id="66fd3-118">Copy and save to a file the **Application (client) ID** value.</span></span>
1. <span data-ttu-id="66fd3-119">在左侧窗格中，单击“**证书和密码**”。</span><span class="sxs-lookup"><span data-stu-id="66fd3-119">In the left panel, click **Certificate and secrets**.</span></span>
    1. <span data-ttu-id="66fd3-120">在“*客户端密码*”下，单击“**新建客户端密码**”。</span><span class="sxs-lookup"><span data-stu-id="66fd3-120">Under *Client secrets*, click **New client secret**.</span></span>
    1. <span data-ttu-id="66fd3-121">添加描述，以便从可能需要为此应用创建的其他密码中识别此密码。</span><span class="sxs-lookup"><span data-stu-id="66fd3-121">Add a description to identify this secret from others you might need to create for this app.</span></span>
    1. <span data-ttu-id="66fd3-122">将“*到期时间*”设置为你的选择。</span><span class="sxs-lookup"><span data-stu-id="66fd3-122">Set *Expires* to your selection.</span></span>
    1. <span data-ttu-id="66fd3-123">单击“**添加**”。</span><span class="sxs-lookup"><span data-stu-id="66fd3-123">Click **Add**.</span></span>
    1. <span data-ttu-id="66fd3-124">复制客户端密码并将其保存到文件中。</span><span class="sxs-lookup"><span data-stu-id="66fd3-124">Copy the client secret and save it to a file.</span></span>
1. <span data-ttu-id="66fd3-125">返回“**机器人频道注册**”窗口，分别复制“**Microsoft 应用 ID**”和“**密码**”框中的“*应用 ID*”和“*客户端密码*”。</span><span class="sxs-lookup"><span data-stu-id="66fd3-125">Go back to the **Bot Channel Registration** window and copy the *App ID* and the *Client secret* in the **Microsoft App ID** and **Password** boxes, respectively.</span></span>
1. <span data-ttu-id="66fd3-126">单击“**确定**”。</span><span class="sxs-lookup"><span data-stu-id="66fd3-126">Click **OK**.</span></span>
1. <span data-ttu-id="66fd3-127">最后单击“**创建**”。</span><span class="sxs-lookup"><span data-stu-id="66fd3-127">Finally, click **Create**.</span></span>

<span data-ttu-id="66fd3-128">在 Azure 创建注册资源后，它将包含在资源组列表中。</span><span class="sxs-lookup"><span data-stu-id="66fd3-128">After Azure has created the registration resource it will be included in the resource group list.</span></span>  

![机器人应用频道注册组](~/assets/images/authentication/auth-bot-channels-registration-group.PNG)

<span data-ttu-id="66fd3-130">创建机器人频道注册后，需要启用 Teams 频道。</span><span class="sxs-lookup"><span data-stu-id="66fd3-130">Once your bot channels registration is created, you'll need to enable the Teams channel.</span></span>

1. <span data-ttu-id="66fd3-131">在 [Azure 门户](https://ms.portal.azure.com/#home)的“Azure 服务”下，选择刚才创建的 **机器人频道注册**。</span><span class="sxs-lookup"><span data-stu-id="66fd3-131">In the [Azure portal](https://ms.portal.azure.com/#home), under Azure services, select the **Bot Channel Registration** you just created.</span></span>
1. <span data-ttu-id="66fd3-132">在左侧窗格中，单击“**频道**”。</span><span class="sxs-lookup"><span data-stu-id="66fd3-132">In the left panel, click **Channels**.</span></span>
1. <span data-ttu-id="66fd3-133">单击 Microsoft Teams 图标，然后选择“**保存**”。</span><span class="sxs-lookup"><span data-stu-id="66fd3-133">Click the Microsoft Teams icon, then choose **Save**.</span></span>
