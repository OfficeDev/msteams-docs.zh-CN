## <a name="update-your-application"></a>更新应用程序

### <a name="_layoutcshtml"></a>_Layout.cshtml

若要在页面中显示选项卡Teams，必须包含 **Microsoft Teams JavaScript** 客户端 SDK，并包括页面加载 `microsoftTeams.initialize()` 后对 的调用。 这是选项卡与应用Teams方式：

- 导航到 **"共享** "文件夹，打开 **_Layout.cshtml**，然后向 `<head>` 标记部分添加以下内容：

    ```html
    `<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>`
    `<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>`
    ```

### <a name="personaltabcshtml"></a>PersonalTab.cshtml

打开 **PersonalTab.cshtml，** 然后通过调用 `<script>` 更新嵌入标记 `microsoftTeams.initialize()` 。

确保保存已更新的 **PersonalTab.cshtml**。