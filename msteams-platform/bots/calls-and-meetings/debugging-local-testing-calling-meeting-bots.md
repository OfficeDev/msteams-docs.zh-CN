---
title: 如何在本地电脑上开发呼叫和联机会议 bot
description: 了解如何使用 ngrok 在本地电脑上开发呼叫和联机会议 bot。
keywords: 本地开发 ngrok 隧道
ms.date: 11/18/2018
ms.openlocfilehash: b6cd2ba5a3866da8085b3da42377ab9e21f12f5f
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673413"
---
# <a name="how-to-develop-calling-and-online-meeting-bots-on-your-local-pc"></a>如何在本地电脑上开发呼叫和联机会议 bot

在 "[运行" 和 "调试" 应用程序中，](../../concepts/build-and-test/debug.md)我们将介绍如何使用[ngrok](https://ngrok.com)在本地计算机和 internet 之间创建隧道。 在本主题中，您还可以了解如何使用 ngrok 和本地电脑来开发支持呼叫和联机会议的 bot。

邮件机器人使用 HTTP，但呼叫和联机会议 bot 使用低级别 TCP。 除了 HTTP 隧道之外，Ngrok 还支持 TCP 隧道;你将在下面了解如何操作。

## <a name="configuring-ngrokyml"></a>配置 ngrok yml

转到[ngrok](https://ngrok.com)并注册免费帐户或登录到现有帐户。 登录后，请转到[仪表板](https://dashboard.ngrok.com)并获取 authtoken。

创建 ngrok 配置文件`ngrok.yml` （有关此文件位于何处的详细信息，请参阅[此处](https://ngrok.com/docs#config)），并添加以下行：

  `authtoken: <Your-AuthToken>`

## <a name="setting-up-signaling"></a>设置信号

在[呼叫和联机会议 bot](./calls-meetings-bots-overview.md)中，我们讨论了呼叫信号—在呼叫过程中，bot 如何检测和响应新的呼叫和事件。 呼叫信号事件通过 HTTP POST 发送到 bot 的调用终结点。

与 bot 的邮件 API 一样，为了让实时媒体平台与你的 bot 交流，你的 bot 必须可通过 internet 访问。 Ngrok 使此简单-将以下行添加到 Ngrok 中。 yml：

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="setting-up-local-media"></a>设置本地媒体

> [!NOTE]
> 仅应用程序托管的媒体 bot 需要此部分，如果你不自己托管媒体，则可以跳过此部分。

应用程序托管的媒体使用证书和 TCP 隧道。 以下步骤是必需的：

- Ngrok 的公共 TCP 终结点具有固定的 Url。 它们是`0.tcp.ngrok.io`、 `1.tcp.ngrok.io`等。 您应具有指向这些 Url 的服务的 DNS CNAME 条目。 在此示例中， `0.bot.contoso.com`假设引用`0.tcp.ngrok.io`、 `1.bot.contoso.com`引用`1.tcp.ngrok.io`，等等。
- 您的 Url 需要 SSL 证书。 为了便于使用，请使用颁发给通配符域的 SSL 证书。 在这种情况下，应`*.bot.contoso.com`为。 此 SSL 证书由媒体 SDK 进行验证，因此它应与你的 bot 的公共 URL 相匹配。 记下指纹，并将其安装在计算机证书中。
- 现在，设置 TCP 隧道以将流量转发到本地主机。 在 ngrok 中写入以下行： yml：

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a>启动 ngrok

现在，ngrok 配置已准备就绪，请启动它：

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

这将启动 ngrok 并定义提供本地主机隧道的公共 Url。 输出外观如下所示：

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

这里`12345`是信号端口， `8445`是应用程序托管的端口， `12332`是由 ngrok 公开的远程媒体端口。 请注意，我们已从`1.bot.contoso.com`转到`1.tcp.ngrok.io`。 这将用作 bot 的媒体 URL。 当然，这些端口号只是示例，您可以使用任何可用的端口。

### <a name="update-code"></a>更新代码

在 ngrok 已启动并在运行后，更新代码以使用刚刚设置的配置。

#### <a name="update-signaling"></a>更新信号

- 在 BotBuilder 调用中，将更改`NotificationUrl`为 ngrok 提供的信号 URL。

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> 将信号替换为 ngrok 提供的和`NotificationEndpoint`接收通知的控制器路径。

> **重要说明**：中`SetNotificationUrl`的 URL 必须是 HTTPS。

> **重要说明**：您的本地实例必须侦听信号端口上的 HTTP 流量。 呼叫和联机会议平台发出的请求将机器人作为 localhost HTTP 流量，除非设置端到端加密。

#### <a name="update-media"></a>更新媒体

更新`MediaPlatformSettings`到以下项。

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
> 上面提供的证书指纹应与服务 FQDN 相匹配。 这就是为什么需要 DNS 条目的原因。

## <a name="next-steps"></a>后续步骤

你的 bot 现在可以在本地运行，并且所有流都可以从本地主机运行。

## <a name="caveats"></a>几点

- Ngrok 免费帐户**不**提供端到端加密。 HTTPS 数据在 ngrok URL 和从 ngrok 到`localhost`之间未加密的数据流处结束。 如果需要端到端加密，请考虑使用付费的 ngrok 帐户。 有关设置安全端到端隧道的步骤，请参阅[TLS 隧道](https://ngrok.com/docs#tls)。
- 由于 bot 回调 URL 是动态的，因此传入呼叫方案要求您频繁更新 ngrok 终结点。 解决此问题的一种方法是使用付费的 ngrok 帐户，该帐户提供可将你的 bot 和平台指向的固定子域。
- Ngrok 隧道也可用于[Azure Service Fabric](/azure/service-fabric/service-fabric-overview)。 有关如何执行此操作的示例，请参阅[HueBot 示例应用程序](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot)。
