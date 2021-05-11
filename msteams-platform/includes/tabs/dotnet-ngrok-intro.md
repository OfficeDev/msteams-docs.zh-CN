## <a name="establish-a-secure-tunnel-to-your-tab"></a>建立到选项卡的安全隧道

Microsoft Teams完全基于云的产品，并且要求使用 HTTPS 终结点从云中提供选项卡内容。 Teams不允许本地托管。 你需要将选项卡发布到公用 URL，或使用将本地端口公开到面向 Internet 的 URL 的代理。

若要测试您的选项卡，您将使用 [ngrok](https://ngrok.com/docs)。 当 ngrok 在本地计算机上运行时，您的服务器的 Web 终结点将可用。 如果关闭 ngrok，URL 将在下次启动时不同。