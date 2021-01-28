---
title: 在本地调试呼叫和会议机器人
description: 了解如何使用 ngrok 在本地电脑上开发通话和联机会议机器人。
ms.topic: how-to
keywords: 本地开发 ngrok 隧道
ms.date: 11/18/2018
ms.openlocfilehash: e9b77df18c8d80f02134dc7912b5796023082039
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014304"
---
# <a name="how-to-develop-calling-and-online-meeting-bots-on-your-local-pc"></a>如何在本地电脑上开发通话和联机会议机器人

在 ["运行和调试你的应用"中](../../concepts/build-and-test/debug.md) ，我们将介绍如何使用 [ngrok](https://ngrok.com) 在本地计算机和 Internet 之间创建隧道。 在本主题中，了解如何使用 ngrok 和本地电脑开发支持通话和联机会议的机器人。

消息机器人使用 HTTP，但呼叫和联机会议机器人使用较低级别的 TCP。 Ngrok 除了支持 HTTP 隧道外，还支持 TCP 隧道;你将在下面了解如何操作。

## <a name="configuring-ngrokyml"></a>配置 ngrok.yml

转到 [ngrok](https://ngrok.com) 并注册免费帐户或登录到现有帐户。 登录后，转到 [仪表板并获取](https://dashboard.ngrok.com) authtoken。

创建 ngrok 配置文件 (，有关详细信息，请参阅此处有关此文件在) 的位置，并 `ngrok.yml` 添加以下行： [](https://ngrok.com/docs#config)

  `authtoken: <Your-AuthToken>`

## <a name="setting-up-signaling"></a>设置信号

在 [通话和联机会议机器人](./calls-meetings-bots-overview.md)中，我们讨论了呼叫信号 — 机器人如何在通话过程中检测和响应新呼叫和事件。 呼叫信号事件通过 HTTP POST 发送到机器人的呼叫终结点。

与机器人的消息 API 一样，为了让实时媒体平台与机器人通信，必须通过 Internet 访问机器人。 Ngrok 使这一点变得简单 — 将以下行添加到您的 ngrok.yml：

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="setting-up-local-media"></a>设置本地媒体

> [!NOTE]
> 此部分仅对应用程序托管的媒体机器人是必需的，如果你自己不托管媒体，可以跳过此部分。

应用程序托管的媒体使用证书和 TCP 隧道。 需要执行以下步骤：

- Ngrok 的公共 TCP 终结点具有固定 URL。 它们 `0.tcp.ngrok.io` 为 `1.tcp.ngrok.io` ，等等。 服务应具有指向这些 URL 的 DNS CNAME 条目。 本示例中，假设 `0.bot.contoso.com` 引用 `0.tcp.ngrok.io` 、 `1.bot.contoso.com` 引用 `1.tcp.ngrok.io` 等。
- URL 需要 SSL 证书。 为了简单易用，请使用颁发给通配符域的 SSL 证书。 在这种情况下，它将 `*.bot.contoso.com` 是 。 此 SSL 证书由媒体 SDK 验证，因此应该与自动程序的公共 URL 相匹配。 记下指纹，并安装在计算机证书中。
- 现在，设置 TCP 隧道以将流量转发到 localhost。 将以下行写入您的 ngrok.yml：

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a>启动 ngrok

现在 ngrok 配置已准备就绪，请启动它：

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

这将启动 ngrok 并定义为 localhost 提供隧道的公共 URL。 输出如下所示：

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

此处是信号端口，是应用程序托管的端口，也是 `12345` `8445` `12332` ngrok 公开的远程媒体端口。 请注意，我们有一个从到的 `1.bot.contoso.com` 转发 `1.tcp.ngrok.io` 。 这将用作机器人的媒体 URL。 当然，这些端口号只是示例，您可以使用任何可用的端口。

### <a name="update-code"></a>更新代码

ngrok 启动并运行后，更新代码以使用刚设置配置。

#### <a name="update-signaling"></a>更新信号

- 在 BotBuilder 调用中，将更改为 `NotificationUrl` ngrok 提供的信号 URL。

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> 将信号替换为 ngrok 提供的信号，将信号替换为接收通知 `NotificationEndpoint` 的控制器路径。

> **重要** 提示：输入的 URL `SetNotificationUrl` 必须为 HTTPS。

> **重要** 提示：本地实例必须侦听信号端口上的 HTTP 流量。 除非设置了端到端加密，否则呼叫和联机会议平台提出的请求将作为 localhost HTTP 流量到达机器人。

#### <a name="update-media"></a>更新媒体

将 `MediaPlatformSettings` 更新为以下内容。

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
> 上面提供的证书指纹应匹配服务 FQDN。 这就是需要 DNS 条目的原因。

## <a name="next-steps"></a>后续步骤

现在，机器人可以在本地运行，并且所有流都可以从 localhost 运行。

## <a name="caveats"></a>警告

- Ngrok 免费 **帐户不提供** 端到端加密。 HTTPS 数据以 ngrok URL 结尾，数据流未加密，从 ngrok 到 `localhost` 。 如果需要端到端加密，请考虑使用付费 ngrok 帐户。 有关设置安全的端到端隧道的步骤，请参阅 [TLS](https://ngrok.com/docs#tls) 隧道。
- 由于机器人回调 URL 是动态的，因此传入呼叫方案需要频繁更新 ngrok 终结点。 解决此问题的一个方法就是使用付费 ngrok 帐户，该帐户提供你可以指向机器人和平台的固定子域。
- Ngrok 隧道还可以与 Azure [Service Fabric 一同使用](/azure/service-fabric/service-fabric-overview)。 有关如何操作的示例，请参阅 [HueBot 示例应用](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot)。
