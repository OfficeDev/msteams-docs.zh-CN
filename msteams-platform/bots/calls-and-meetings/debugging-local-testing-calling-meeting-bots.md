---
title: 在本地调试呼叫和会议机器人
description: 了解如何使用 ngrok 在本地电脑上开发呼叫和联机会议机器人。
ms.topic: how-to
ms.localizationpriority: medium
keywords: 本地开发 ngrok 隧道
ms.date: 11/18/2018
ms.openlocfilehash: c55ec6e5d7296f4ee04ae3ad3de0f9bb82cfd276
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453360"
---
# <a name="develop-calling-and-online-meeting-bots-on-your-local-pc"></a>在本地电脑上开发通话和联机会议机器人

在 [运行和调试你的应用中](../../concepts/build-and-test/debug.md) ，我们介绍如何使用 [ngrok](https://ngrok.com) 在本地计算机和 Internet 之间创建隧道。 在本主题中，了解如何使用 ngrok 和本地电脑开发支持通话和联机会议的机器人。

消息机器人使用 HTTP，但呼叫和联机会议机器人使用较低级别的 TCP。 Ngrok 除了支持 HTTP 隧道外，还支持 TCP 隧道。

## <a name="configure-ngrokyml"></a>配置 ngrok.yml

转到 [ngrok](https://ngrok.com) 并注册免费帐户或登录到现有帐户。 登录后，转到 [仪表板并获取](https://dashboard.ngrok.com) 身份验证令牌。

创建 ngrok 配置文件并 `ngrok.yml` 添加以下行。 有关文件可位于的位置详细信息，请参阅 [ngrok](https://ngrok.com/docs#config)：

  `authtoken: <Your-AuthToken>`

## <a name="set-up-signaling"></a>设置信号

在 [通话和联机会议机器人](./calls-meetings-bots-overview.md)中，我们讨论了呼叫信号，关于机器人如何在呼叫期间检测和响应新呼叫和事件。 呼叫信号事件通过 HTTP POST 发送到机器人的呼叫终结点。

与机器人的消息 API 一样，对于实时媒体平台与机器人通信，必须通过 Internet 访问机器人。 Ngrok 使这一点变得简单。 将以下行添加到 ngrok.yml：

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="set-up-local-media"></a>设置本地媒体

> [!NOTE]
> 只有应用程序托管的媒体机器人才需要此部分，如果你自己不托管媒体，可以跳过此部分。

应用程序托管的媒体使用证书和 TCP 隧道。 需要执行以下步骤：

1. Ngrok 的公共 TCP 终结点具有固定 URL。 它们为 `0.tcp.ngrok.io`、 `1.tcp.ngrok.io`等。 服务必须具有指向这些 URL 的 DNS CNAME 条目。 例如，假设`0.bot.contoso.com`引用 、 `0.tcp.ngrok.io``1.bot.contoso.com` 引用 `1.tcp.ngrok.io`等。
2. URL 需要 SSL 证书。 为简单易用，请使用颁发给通配符域的 SSL 证书。 在这种情况下，它将是 `*.bot.contoso.com`。 此 SSL 证书由媒体 SDK 验证，因此必须与自动程序的公共 URL 相匹配。 记下指纹，并安装在计算机证书中。
3. 现在，设置 TCP 隧道以将流量转发到 localhost。 将以下行写入 ngrok.yml 中：

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a>启动 ngrok

现在，ngrok 配置已准备就绪，请启动它：

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

这将启动 ngrok 并定义为 localhost 提供隧道的公共 URL。 下面是一个输出示例：

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

`12345`此处是信号端口， `8445` `12332`是应用程序托管的端口，也是 ngrok 公开的远程媒体端口。 请注意，我们有一个从 转发到 `1.bot.contoso.com` `1.tcp.ngrok.io`。 这将用作机器人的媒体 URL。 当然，这些端口号只是示例，您可以使用任何可用的端口。

### <a name="update-code"></a>更新代码

ngrok 启动并运行后，更新代码以使用刚设置的配置。

#### <a name="update-signaling"></a>更新信号

在 BotBuilder 调用中，将 `NotificationUrl` 更改为 ngrok 提供的信号 URL。

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> 将 signal 替换为 ngrok `NotificationEndpoint` 提供的 ，将 替换为接收通知的控制器路径。

> [!IMPORTANT]
>
> * 中的 URL `SetNotificationUrl` 必须为 HTTPS。
>
> 本地实例必须侦听信号端口上的 HTTP 流量。 除非设置了端到端加密，否则呼叫和联机会议平台提出的请求将作为 localhost HTTP 流量到达机器人。

#### <a name="update-media"></a>更新媒体

更新你的 `MediaPlatformSettings` ，如下所示：

```csharp
var mediaPlatform = new MediaPlatformSettings
{
    ApplicationId = <Your application id>
    MediaPlatformInstanceSettings = new MediaPlatformInstanceSettings
    {
        CertificateThumbprint = <Your SSL Cert thumbprint>,
        InstanceInternalPort = <Localhost media port>,
        InstancePublicPort = <Ngrok exposed remote media port>,
        InstancePublicIPAddress = new IPAddress(0x0),
        ServiceFqdn = <Media url for bot (eg: 1.bot.contoso.com)>,
    },
}
```

> [!NOTE]
> 中提供的证书指纹 `MediaPlatformSettings` 必须与服务 FQDN 匹配。 这就是需要 DNS 条目的原因。

## <a name="caveats"></a>注意事项

* Ngrok 免费 **帐户不提供** 端到端加密。 HTTPS 数据以 ngrok URL 结尾，数据流未加密，从 ngrok 到 `localhost`。 如果需要端到端加密，请考虑使用付费 ngrok 帐户。 有关设置安全的端到端隧道的步骤，请参阅 [TLS](https://ngrok.com/docs#tls) 隧道。
* 由于机器人回调 URL 是动态的，传入呼叫方案需要频繁更新 ngrok 终结点。 解决此问题的一个方法就是使用付费 ngrok 帐户，该帐户提供你可以将机器人和平台指向的固定子域。
* Ngrok 隧道还可以与 [Azure](/azure/service-fabric/service-fabric-overview) Service Fabric。 有关操作示例，请参阅 [HueBot 示例应用](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples/HueBot/HueBot)。
