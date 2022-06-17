---
title: 在本地调试呼叫和会议机器人
description: 在本模块中，了解如何使用 ngrok 在本地电脑上开发呼叫和联机会议机器人。
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 11/18/2018
ms.openlocfilehash: 518d0b846737eca7f4c182dba032b2c85366cee6
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143814"
---
# <a name="develop-calling-and-online-meeting-bots-on-your-local-pc"></a>在本地电脑上开发呼叫和联机会议机器人

在 [运行和调试应用](../../concepts/build-and-test/debug.md)时，我们将介绍如何使用 [ngrok](https://ngrok.com) 在本地计算机和 Internet 之间创建隧道。 在本主题中，了解如何使用 ngrok 和本地电脑开发支持呼叫和联机会议的机器人。

消息传递机器人使用 HTTP，但呼叫和联机会议机器人使用较低级别的 TCP。 除了 HTTP 隧道，Ngrok 还支持 TCP 隧道。

## <a name="configure-ngrokyml"></a>配置 ngrok.yml

转到 [ngrok](https://ngrok.com) 并注册免费帐户或登录到现有帐户。 登录后，转到[仪表板](https://dashboard.ngrok.com)并获取身份验证令牌。

创建 ngrok 配置文件 `ngrok.yml` 并添加以下行。 有关文件所在位置的详细信息，请参阅 [ngrok](https://ngrok.com/docs#config)：

  `authtoken: <Your-AuthToken>`

## <a name="set-up-signaling"></a>设置信号

在[呼叫和联机会议机器人](./calls-meetings-bots-overview.md)中，我们讨论了有关机器人如何在呼叫期间检测和响应新呼叫和事件的呼叫信号。 呼叫信号事件通过 HTTP POST 发送到机器人的呼叫端点。

与机器人的消息传送 API 一样，为了使实时媒体平台与机器人通信，机器人必须可以通过 Internet 访问。 Ngrok 使这一点变得简单。 将以下行添加到 ngrok.yml：

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="set-up-local-media"></a>设置本地媒体

> [!NOTE]
> 此部分仅适用于应用程序托管的媒体机器人，如果自己不托管媒体，则可以跳过此部分。

应用程序托管的媒体使用证书和 TCP 隧道。 需要执行以下步骤：

1. Ngrok 的公共 TCP 端点具有固定 URL。 他们是 `0.tcp.ngrok.io`， `1.tcp.ngrok.io`等等。 必须具有指向这些 URL 的服务的 DNS CNAME 条目。 例如，假设 `0.bot.contoso.com` 指向 `0.tcp.ngrok.io`、`1.bot.contoso.com` 指向 `1.tcp.ngrok.io` 等。
2. URL 需要 SSL 证书。 若要简化操作，请使用颁发给通配符域的 SSL 证书。 在此示例中为 `*.bot.contoso.com`。 此 SSL 证书由媒体 SDK 验证，因此它必须与机器人的公共 URL 相匹配。 记下指纹并将其安装在计算机证书中。
3. 现在，设置 TCP 隧道以将流量转发到 localhost。 将以下行写入 ngrok.yml：

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a>启动 ngrok

现在 ngrok 配置已准备就绪，请启动它：

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

这会启动 ngrok 并定义公共 URL，这些 URL 为 localhost 提供隧道。 下面是一个输出示例：

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

在这里，`12345` 是信号端口，`8445` 是应用程序托管的端口，`12332` 是 ngrok 公开的远程媒体端口。 请注意，我们有一个从 `1.bot.contoso.com` 到 `1.tcp.ngrok.io` 的转发。 这会用作机器人的媒体 URL。 当然，这些端口号只是示例，你可以使用任何可用端口。

### <a name="update-code"></a>更新代码

ngrok 启动并运行后，更新代码以使用刚设置的配置。

#### <a name="update-signaling"></a>更新信号

在 BotBuilder 调用中，将 `NotificationUrl` 更改为 ngrok 提供的信号 URL。

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> 将信号替换为 ngrok 提供的信号，`NotificationEndpoint` 替换为接收通知的控制器路径。

> [!IMPORTANT]
>
> * `SetNotificationUrl` 中的 URL 必须是 HTTPS。
>
> 本地实例必须侦听信号端口上的 HTTP 流量。 除非设置了端到端加密，否则呼叫和联机会议平台发出的请求将作为 localhost HTTP 流量到达机器人。

#### <a name="update-media"></a>更新媒体

按如下所示更新 `MediaPlatformSettings`：

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
> `MediaPlatformSettings` 中提供的证书指纹必须与服务 FQDN 匹配。 这就是需要 DNS 条目的原因。

## <a name="caveats"></a>警告

* Ngrok 免费帐户 **不** 提供端到端加密。 HTTPS 数据以 ngrok URL 结尾，数据从 ngrok 未加密流到 `localhost`。 如果需要端到端加密，请考虑使用付费 ngrok 帐户。 有关设置安全端到端隧道的步骤，请参阅 [TLS 隧道](https://ngrok.com/docs#tls)。
* 由于机器人回调 URL 是动态的，传入调用方案要求你经常更新 ngrok 端点。 解决此问题的一种方法是使用付费 ngrok 帐户，该帐户提供可将机器人和平台指向的固定子域。
* Ngrok 隧道也可与 [Azure Service Fabric](/azure/service-fabric/service-fabric-overview) 一起使用。 有关如何执行此操作的示例，请参阅 [HueBot 示例应用](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples/HueBot/HueBot)。
