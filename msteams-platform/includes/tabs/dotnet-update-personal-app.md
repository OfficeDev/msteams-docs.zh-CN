## <a name="update-your-application"></a>更新应用程序

### <a name="_layoutcshtml"></a>_Layout cshtml

若要在团队中显示您的选项卡，您必须包含**Microsoft 团队 JavaScript 客户端 SDK** ，并`microsoftTeams.initialize()`在加载页面后包含一个调用。 这就是您的选项卡和团队应用程序的通信方式：

- 导航到**共享**文件夹，打开 **_Layout. cshtml**，并将以下内容添加到 " `<head>`标签" 部分：

```html
`<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>`
`<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>`
```

### <a name="personaltabcshtml"></a>PersonalTab

打开**PersonalTab** ，并通过调用`<script>` `microsoftTeams.initialize()`更新嵌入的标记。

请务必保存更新后的*PersonalTab*。