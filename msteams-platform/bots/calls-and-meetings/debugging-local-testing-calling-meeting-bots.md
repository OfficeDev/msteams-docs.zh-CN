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
# <a name="how-to-develop-calling-and-online-meeting-bots-on-your-local-pc"></a><span data-ttu-id="9781c-104">如何在本地电脑上开发呼叫和联机会议 bot</span><span class="sxs-lookup"><span data-stu-id="9781c-104">How to develop calling and online meeting bots on your local PC</span></span>

<span data-ttu-id="9781c-105">在 "[运行" 和 "调试" 应用程序中，](../../concepts/build-and-test/debug.md)我们将介绍如何使用[ngrok](https://ngrok.com)在本地计算机和 internet 之间创建隧道。</span><span class="sxs-lookup"><span data-stu-id="9781c-105">In [Run and debug your app](../../concepts/build-and-test/debug.md) we explain how to use [ngrok](https://ngrok.com) to create a tunnel between your local computer and the internet.</span></span> <span data-ttu-id="9781c-106">在本主题中，您还可以了解如何使用 ngrok 和本地电脑来开发支持呼叫和联机会议的 bot。</span><span class="sxs-lookup"><span data-stu-id="9781c-106">In this topic, learn how you can also use ngrok and your local PC to develop bots that support calls and online meetings.</span></span>

<span data-ttu-id="9781c-107">邮件机器人使用 HTTP，但呼叫和联机会议 bot 使用低级别 TCP。</span><span class="sxs-lookup"><span data-stu-id="9781c-107">Messaging bots use HTTP, but calls and online meeting bots use the lower-level TCP.</span></span> <span data-ttu-id="9781c-108">除了 HTTP 隧道之外，Ngrok 还支持 TCP 隧道;你将在下面了解如何操作。</span><span class="sxs-lookup"><span data-stu-id="9781c-108">Ngrok supports TCP tunnels in addition to HTTP tunnels; you'll learn how, below.</span></span>

## <a name="configuring-ngrokyml"></a><span data-ttu-id="9781c-109">配置 ngrok yml</span><span class="sxs-lookup"><span data-stu-id="9781c-109">Configuring ngrok.yml</span></span>

<span data-ttu-id="9781c-110">转到[ngrok](https://ngrok.com)并注册免费帐户或登录到现有帐户。</span><span class="sxs-lookup"><span data-stu-id="9781c-110">Go to [ngrok](https://ngrok.com) and sign up for a free account or log into your existing account.</span></span> <span data-ttu-id="9781c-111">登录后，请转到[仪表板](https://dashboard.ngrok.com)并获取 authtoken。</span><span class="sxs-lookup"><span data-stu-id="9781c-111">Once you've logged in, go to the [dashboard](https://dashboard.ngrok.com) and get your authtoken.</span></span>

<span data-ttu-id="9781c-112">创建 ngrok 配置文件`ngrok.yml` （有关此文件位于何处的详细信息，请参阅[此处](https://ngrok.com/docs#config)），并添加以下行：</span><span class="sxs-lookup"><span data-stu-id="9781c-112">Create an ngrok configuration file `ngrok.yml` (see [here](https://ngrok.com/docs#config) for more information on where this file can be located) and add this line:</span></span>

  `authtoken: <Your-AuthToken>`

## <a name="setting-up-signaling"></a><span data-ttu-id="9781c-113">设置信号</span><span class="sxs-lookup"><span data-stu-id="9781c-113">Setting up signaling</span></span>

<span data-ttu-id="9781c-114">在[呼叫和联机会议 bot](./calls-meetings-bots-overview.md)中，我们讨论了呼叫信号—在呼叫过程中，bot 如何检测和响应新的呼叫和事件。</span><span class="sxs-lookup"><span data-stu-id="9781c-114">In [Calls and online meetings bots](./calls-meetings-bots-overview.md), we discussed call signaling — how bots detect and respond to new calls and events during a call.</span></span> <span data-ttu-id="9781c-115">呼叫信号事件通过 HTTP POST 发送到 bot 的调用终结点。</span><span class="sxs-lookup"><span data-stu-id="9781c-115">Call signaling events are sent via HTTP POST to the bot's calling endpoint.</span></span>

<span data-ttu-id="9781c-116">与 bot 的邮件 API 一样，为了让实时媒体平台与你的 bot 交流，你的 bot 必须可通过 internet 访问。</span><span class="sxs-lookup"><span data-stu-id="9781c-116">As with the bot's messaging API, in order for the Real-time Media Platform to talk to your bot, your bot must be reachable over the internet.</span></span> <span data-ttu-id="9781c-117">Ngrok 使此简单-将以下行添加到 Ngrok 中。 yml：</span><span class="sxs-lookup"><span data-stu-id="9781c-117">Ngrok makes this simple — add the following lines to your ngrok.yml:</span></span>

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="setting-up-local-media"></a><span data-ttu-id="9781c-118">设置本地媒体</span><span class="sxs-lookup"><span data-stu-id="9781c-118">Setting up local media</span></span>

> [!NOTE]
> <span data-ttu-id="9781c-119">仅应用程序托管的媒体 bot 需要此部分，如果你不自己托管媒体，则可以跳过此部分。</span><span class="sxs-lookup"><span data-stu-id="9781c-119">This section is only required for application-hosted media bots and can be skipped if you don't host media yourself.</span></span>

<span data-ttu-id="9781c-120">应用程序托管的媒体使用证书和 TCP 隧道。</span><span class="sxs-lookup"><span data-stu-id="9781c-120">Application-hosted media uses certificates and TCP tunnels.</span></span> <span data-ttu-id="9781c-121">以下步骤是必需的：</span><span class="sxs-lookup"><span data-stu-id="9781c-121">The following steps are required:</span></span>

- <span data-ttu-id="9781c-122">Ngrok 的公共 TCP 终结点具有固定的 Url。</span><span class="sxs-lookup"><span data-stu-id="9781c-122">Ngrok's public TCP endpoints have fixed URLs.</span></span> <span data-ttu-id="9781c-123">它们是`0.tcp.ngrok.io`、 `1.tcp.ngrok.io`等。</span><span class="sxs-lookup"><span data-stu-id="9781c-123">They are `0.tcp.ngrok.io`, `1.tcp.ngrok.io`, and so on.</span></span> <span data-ttu-id="9781c-124">您应具有指向这些 Url 的服务的 DNS CNAME 条目。</span><span class="sxs-lookup"><span data-stu-id="9781c-124">You should have a DNS CNAME entry for your service that points to these URLs.</span></span> <span data-ttu-id="9781c-125">在此示例中， `0.bot.contoso.com`假设引用`0.tcp.ngrok.io`、 `1.bot.contoso.com`引用`1.tcp.ngrok.io`，等等。</span><span class="sxs-lookup"><span data-stu-id="9781c-125">In this example, let's say `0.bot.contoso.com` refers to `0.tcp.ngrok.io`, `1.bot.contoso.com` refers to `1.tcp.ngrok.io`, and so on.</span></span>
- <span data-ttu-id="9781c-126">您的 Url 需要 SSL 证书。</span><span class="sxs-lookup"><span data-stu-id="9781c-126">A SSL certificate is required for your URLs.</span></span> <span data-ttu-id="9781c-127">为了便于使用，请使用颁发给通配符域的 SSL 证书。</span><span class="sxs-lookup"><span data-stu-id="9781c-127">To make it easy, use a SSL certificate issued to a wild card domain.</span></span> <span data-ttu-id="9781c-128">在这种情况下，应`*.bot.contoso.com`为。</span><span class="sxs-lookup"><span data-stu-id="9781c-128">In this case, it would be `*.bot.contoso.com`.</span></span> <span data-ttu-id="9781c-129">此 SSL 证书由媒体 SDK 进行验证，因此它应与你的 bot 的公共 URL 相匹配。</span><span class="sxs-lookup"><span data-stu-id="9781c-129">This SSL certificate is validated by the media SDK, so it should match your bot's public URL.</span></span> <span data-ttu-id="9781c-130">记下指纹，并将其安装在计算机证书中。</span><span class="sxs-lookup"><span data-stu-id="9781c-130">Note the thumbprint and install it in your machine certificates.</span></span>
- <span data-ttu-id="9781c-131">现在，设置 TCP 隧道以将流量转发到本地主机。</span><span class="sxs-lookup"><span data-stu-id="9781c-131">Now, setup a TCP tunnel to forward the traffic to localhost.</span></span> <span data-ttu-id="9781c-132">在 ngrok 中写入以下行： yml：</span><span class="sxs-lookup"><span data-stu-id="9781c-132">Write the following lines into your ngrok.yml:</span></span>

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a><span data-ttu-id="9781c-133">启动 ngrok</span><span class="sxs-lookup"><span data-stu-id="9781c-133">Start ngrok</span></span>

<span data-ttu-id="9781c-134">现在，ngrok 配置已准备就绪，请启动它：</span><span class="sxs-lookup"><span data-stu-id="9781c-134">Now that the ngrok configuration is ready, launch it:</span></span>

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

<span data-ttu-id="9781c-135">这将启动 ngrok 并定义提供本地主机隧道的公共 Url。</span><span class="sxs-lookup"><span data-stu-id="9781c-135">This starts ngrok and defines the public URLs which provide the tunnels to your localhost.</span></span> <span data-ttu-id="9781c-136">输出外观如下所示：</span><span class="sxs-lookup"><span data-stu-id="9781c-136">The output looks like the following:</span></span>

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

<span data-ttu-id="9781c-137">这里`12345`是信号端口， `8445`是应用程序托管的端口， `12332`是由 ngrok 公开的远程媒体端口。</span><span class="sxs-lookup"><span data-stu-id="9781c-137">Here, `12345` is the signaling port, `8445` is the application-hosted port, and `12332` is the remote media port exposed by ngrok.</span></span> <span data-ttu-id="9781c-138">请注意，我们已从`1.bot.contoso.com`转到`1.tcp.ngrok.io`。</span><span class="sxs-lookup"><span data-stu-id="9781c-138">Note that we have a forwarding from `1.bot.contoso.com` to `1.tcp.ngrok.io`.</span></span> <span data-ttu-id="9781c-139">这将用作 bot 的媒体 URL。</span><span class="sxs-lookup"><span data-stu-id="9781c-139">This will be used as the media URL for the bot.</span></span> <span data-ttu-id="9781c-140">当然，这些端口号只是示例，您可以使用任何可用的端口。</span><span class="sxs-lookup"><span data-stu-id="9781c-140">Of course, these port numbers are just examples and you can use any available port.</span></span>

### <a name="update-code"></a><span data-ttu-id="9781c-141">更新代码</span><span class="sxs-lookup"><span data-stu-id="9781c-141">Update code</span></span>

<span data-ttu-id="9781c-142">在 ngrok 已启动并在运行后，更新代码以使用刚刚设置的配置。</span><span class="sxs-lookup"><span data-stu-id="9781c-142">Once ngrok is up and running, update the code to use the config you just set up.</span></span>

#### <a name="update-signaling"></a><span data-ttu-id="9781c-143">更新信号</span><span class="sxs-lookup"><span data-stu-id="9781c-143">Update signaling</span></span>

- <span data-ttu-id="9781c-144">在 BotBuilder 调用中，将更改`NotificationUrl`为 ngrok 提供的信号 URL。</span><span class="sxs-lookup"><span data-stu-id="9781c-144">In the BotBuilder call, change the `NotificationUrl` to the signaling URL provided by ngrok.</span></span>

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> <span data-ttu-id="9781c-145">将信号替换为 ngrok 提供的和`NotificationEndpoint`接收通知的控制器路径。</span><span class="sxs-lookup"><span data-stu-id="9781c-145">Replace signal with the one provided by ngrok and the `NotificationEndpoint` with the controller path that receives notification.</span></span>

> <span data-ttu-id="9781c-146">**重要说明**：中`SetNotificationUrl`的 URL 必须是 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="9781c-146">**IMPORTANT**: The URL in `SetNotificationUrl` must be HTTPS.</span></span>

> <span data-ttu-id="9781c-147">**重要说明**：您的本地实例必须侦听信号端口上的 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="9781c-147">**IMPORTANT**: Your local instance must be listening to HTTP traffic on the signaling port.</span></span> <span data-ttu-id="9781c-148">呼叫和联机会议平台发出的请求将机器人作为 localhost HTTP 流量，除非设置端到端加密。</span><span class="sxs-lookup"><span data-stu-id="9781c-148">The requests made by the calls and online meetings platform will reach the bot as localhost HTTP traffic unless end-to-end encryption is set up.</span></span>

#### <a name="update-media"></a><span data-ttu-id="9781c-149">更新媒体</span><span class="sxs-lookup"><span data-stu-id="9781c-149">Update media</span></span>

<span data-ttu-id="9781c-150">更新`MediaPlatformSettings`到以下项。</span><span class="sxs-lookup"><span data-stu-id="9781c-150">Update your `MediaPlatformSettings` to the following.</span></span>

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
> <span data-ttu-id="9781c-151">上面提供的证书指纹应与服务 FQDN 相匹配。</span><span class="sxs-lookup"><span data-stu-id="9781c-151">The certificate thumbprint provided above should match the Service FQDN.</span></span> <span data-ttu-id="9781c-152">这就是为什么需要 DNS 条目的原因。</span><span class="sxs-lookup"><span data-stu-id="9781c-152">That is why the DNS entries are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9781c-153">后续步骤</span><span class="sxs-lookup"><span data-stu-id="9781c-153">Next steps</span></span>

<span data-ttu-id="9781c-154">你的 bot 现在可以在本地运行，并且所有流都可以从本地主机运行。</span><span class="sxs-lookup"><span data-stu-id="9781c-154">Your bot can now run locally and all the flows work from your localhost.</span></span>

## <a name="caveats"></a><span data-ttu-id="9781c-155">几点</span><span class="sxs-lookup"><span data-stu-id="9781c-155">Caveats</span></span>

- <span data-ttu-id="9781c-156">Ngrok 免费帐户**不**提供端到端加密。</span><span class="sxs-lookup"><span data-stu-id="9781c-156">Ngrok free accounts **don't** provide end-to-end encryption.</span></span> <span data-ttu-id="9781c-157">HTTPS 数据在 ngrok URL 和从 ngrok 到`localhost`之间未加密的数据流处结束。</span><span class="sxs-lookup"><span data-stu-id="9781c-157">The HTTPS data ends at the ngrok URL and the data flows unencrypted from ngrok to `localhost`.</span></span> <span data-ttu-id="9781c-158">如果需要端到端加密，请考虑使用付费的 ngrok 帐户。</span><span class="sxs-lookup"><span data-stu-id="9781c-158">If you require end-to-end encryption, consider a paid ngrok account.</span></span> <span data-ttu-id="9781c-159">有关设置安全端到端隧道的步骤，请参阅[TLS 隧道](https://ngrok.com/docs#tls)。</span><span class="sxs-lookup"><span data-stu-id="9781c-159">See [TLS tunnels](https://ngrok.com/docs#tls) for steps on setting up secure end-to-end tunnels.</span></span>
- <span data-ttu-id="9781c-160">由于 bot 回调 URL 是动态的，因此传入呼叫方案要求您频繁更新 ngrok 终结点。</span><span class="sxs-lookup"><span data-stu-id="9781c-160">Because the bot callback URL is dynamic, incoming call scenarios require you to frequently update your ngrok endpoints.</span></span> <span data-ttu-id="9781c-161">解决此问题的一种方法是使用付费的 ngrok 帐户，该帐户提供可将你的 bot 和平台指向的固定子域。</span><span class="sxs-lookup"><span data-stu-id="9781c-161">One way to fix this is to use a paid ngrok account which provides fixed subdomains to which you can point your bot and the platform.</span></span>
- <span data-ttu-id="9781c-162">Ngrok 隧道也可用于[Azure Service Fabric](/azure/service-fabric/service-fabric-overview)。</span><span class="sxs-lookup"><span data-stu-id="9781c-162">Ngrok tunnels can also be used with [Azure Service Fabric](/azure/service-fabric/service-fabric-overview).</span></span> <span data-ttu-id="9781c-163">有关如何执行此操作的示例，请参阅[HueBot 示例应用程序](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot)。</span><span class="sxs-lookup"><span data-stu-id="9781c-163">For an example of how to do this, see the [HueBot sample app](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot).</span></span>
