## <a name="establish-a-secure-tunnel-to-your-tab"></a>建立到您的选项卡的安全隧道

Microsoft 团队是完全基于云的产品，要求使用 HTTPS 终结点从云中获取你的选项卡内容。 团队不允许本地托管。 您需要将您的选项卡发布到公用 URL，或使用将本地端口暴露给面向 internet 的 URL 的代理。

若要测试您的选项卡，您将使用[ngrok](https://ngrok.com/docs)。 在本地计算机上运行 ngrok 时，您的服务器的 web 终结点将可用。 如果关闭 ngrok，Url 将在下次启动时有所不同。