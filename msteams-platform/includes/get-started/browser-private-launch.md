### <a name="optional-adjust-your-browser-launch-settings"></a> (可选) 调整浏览器启动设置

在开发Teams应用时，通常使用备用开发人员租户或备用凭据运行应用。  Microsoft Edge和 Google Chrome 都提供用于调整浏览器的启动设置设施。  例如，若要更新项目以支持 InPrivate 模式 (Microsoft Edge) ，请打开 `.vscode/launch.json` 项目中的文件。  查找相应的启动设置，并在每个设置中添加以下块：

``` json
"runtimeArgs": [ "--inprivate" ]
```

例如，在本地运行的启动设置如下所示：

``` json
{
   "name": "Start and Attach to Frontend (Edge)",
   "type": "pwa-msedge",
   "request": "launch",
   "url": "https://teams.microsoft.com/_#/l/app/${localTeamsAppId}?installAppPackage=true",
   "preLaunchTask": "Start Frontend",
   "postDebugTask": "Stop All Services",
   "presentation": {
         "group": "all",
         "hidden": true
   },
   "runtimeArgs": [ "--inprivate" ]
},
```

或者，可以将浏览器配置为使用上一个已知配置文件。 [在"新建配置文件"Microsoft Edge。](https://support.microsoft.com/topic/sign-in-and-create-multiple-profiles-in-microsoft-edge-df94e622-2061-49ae-ad1d-6f0e43ce6435)  然后，调整设置以将上一个已知配置文件用于新链接：

- 在Microsoft Edge中，打开 `edge://settings/profiles/multiProfileSettings` 。
- 关闭自动 **配置文件切换**。
- 对于"**外部链接的默认配置文件"，选择**"上次 **使用 (默认) "。**

在调试应用之前，请确保浏览器已打开到正确的配置文件。
