---
title: 在本地调试呼叫和会议机器人
description: 了解如何使用 ngrok 在本地电脑上开发呼叫和联机会议机器人。
ms.topic: how-to
keywords: 本地开发 ngrok 隧道
ms.date: 11/18/2018
ms.openlocfilehash: b764e41302ab569e40c9dacd374a31e6abb1d642
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654284"
---
# <a name="develop-calling-and-online-meeting-bots-on-your-local-pc"></a><span data-ttu-id="112aa-104">在本地电脑上开发通话和联机会议机器人</span><span class="sxs-lookup"><span data-stu-id="112aa-104">Develop calling and online meeting bots on your local PC</span></span>

<span data-ttu-id="112aa-105">在 [运行和调试你的应用中](../../concepts/build-and-test/debug.md) ，我们介绍如何使用 [ngrok](https://ngrok.com) 在本地计算机和 Internet 之间创建隧道。</span><span class="sxs-lookup"><span data-stu-id="112aa-105">In [Run and debug your app](../../concepts/build-and-test/debug.md) we explain how to use [ngrok](https://ngrok.com) to create a tunnel between your local computer and the internet.</span></span> <span data-ttu-id="112aa-106">在本主题中，了解如何使用 ngrok 和本地电脑开发支持通话和联机会议的机器人。</span><span class="sxs-lookup"><span data-stu-id="112aa-106">In this topic, learn how you can also use ngrok and your local PC to develop bots that support calls and online meetings.</span></span>

<span data-ttu-id="112aa-107">消息机器人使用 HTTP，但呼叫和联机会议机器人使用较低级别的 TCP。</span><span class="sxs-lookup"><span data-stu-id="112aa-107">Messaging bots use HTTP, but calls and online meeting bots use the lower-level TCP.</span></span> <span data-ttu-id="112aa-108">Ngrok 除了支持 HTTP 隧道外，还支持 TCP 隧道。</span><span class="sxs-lookup"><span data-stu-id="112aa-108">Ngrok supports TCP tunnels in addition to HTTP tunnels.</span></span> 

## <a name="configure-ngrokyml"></a><span data-ttu-id="112aa-109">配置 ngrok.yml</span><span class="sxs-lookup"><span data-stu-id="112aa-109">Configure ngrok.yml</span></span>

<span data-ttu-id="112aa-110">转到 [ngrok](https://ngrok.com) 并注册免费帐户或登录到现有帐户。</span><span class="sxs-lookup"><span data-stu-id="112aa-110">Go to [ngrok](https://ngrok.com) and sign up for a free account or log into your existing account.</span></span> <span data-ttu-id="112aa-111">登录后，转到 [仪表板并获取](https://dashboard.ngrok.com) 身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="112aa-111">After you've signed in, go to the [dashboard](https://dashboard.ngrok.com) and get your auth token.</span></span>

<span data-ttu-id="112aa-112">创建 ngrok 配置文件 `ngrok.yml` 并添加以下行。</span><span class="sxs-lookup"><span data-stu-id="112aa-112">Create an ngrok configuration file `ngrok.yml` and add the following line.</span></span> <span data-ttu-id="112aa-113">有关文件可以位于的位置详细信息，请参阅 [ngrok](https://ngrok.com/docs#config)：</span><span class="sxs-lookup"><span data-stu-id="112aa-113">For more information on where the file can be located, see [ngrok](https://ngrok.com/docs#config):</span></span>

  `authtoken: <Your-AuthToken>`

## <a name="set-up-signaling"></a><span data-ttu-id="112aa-114">设置信号</span><span class="sxs-lookup"><span data-stu-id="112aa-114">Set up signaling</span></span>

<span data-ttu-id="112aa-115">在 [通话和联机会议机器人](./calls-meetings-bots-overview.md)中，我们讨论了呼叫信号，关于机器人如何在呼叫期间检测和响应新呼叫和事件。</span><span class="sxs-lookup"><span data-stu-id="112aa-115">In [Calls and online meetings bots](./calls-meetings-bots-overview.md), we discussed call signaling on how bots detect and respond to new calls and events during a call.</span></span> <span data-ttu-id="112aa-116">呼叫信号事件通过 HTTP POST 发送到机器人的呼叫终结点。</span><span class="sxs-lookup"><span data-stu-id="112aa-116">Call signaling events are sent through HTTP POST to the bot's calling endpoint.</span></span>

<span data-ttu-id="112aa-117">与机器人的消息 API 一样，对于实时媒体平台与机器人通信，必须通过 Internet 访问机器人。</span><span class="sxs-lookup"><span data-stu-id="112aa-117">As with the bot's messaging API, for the Real-time Media Platform to talk to your bot, your bot must be reachable over the internet.</span></span> <span data-ttu-id="112aa-118">Ngrok 使这一点变得简单。</span><span class="sxs-lookup"><span data-stu-id="112aa-118">Ngrok makes this simple.</span></span> <span data-ttu-id="112aa-119">将以下行添加到 ngrok.yml：</span><span class="sxs-lookup"><span data-stu-id="112aa-119">Add the following lines to your ngrok.yml:</span></span>

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="set-up-local-media"></a><span data-ttu-id="112aa-120">设置本地媒体</span><span class="sxs-lookup"><span data-stu-id="112aa-120">Set up local media</span></span>

> [!NOTE]
> <span data-ttu-id="112aa-121">只有应用程序托管的媒体机器人才需要此部分，并且如果你自己不托管媒体，可以跳过此部分。</span><span class="sxs-lookup"><span data-stu-id="112aa-121">This section is only required for application-hosted media bots and can be skipped if you don't host media yourself.</span></span>

<span data-ttu-id="112aa-122">应用程序托管的媒体使用证书和 TCP 隧道。</span><span class="sxs-lookup"><span data-stu-id="112aa-122">Application-hosted media uses certificates and TCP tunnels.</span></span> <span data-ttu-id="112aa-123">需要执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="112aa-123">The following steps are required:</span></span>

1. <span data-ttu-id="112aa-124">Ngrok 的公共 TCP 终结点具有固定 URL。</span><span class="sxs-lookup"><span data-stu-id="112aa-124">Ngrok's public TCP endpoints have fixed URLs.</span></span> <span data-ttu-id="112aa-125">它们 `0.tcp.ngrok.io` 为 `1.tcp.ngrok.io` 、 等。</span><span class="sxs-lookup"><span data-stu-id="112aa-125">They are `0.tcp.ngrok.io`, `1.tcp.ngrok.io`, and so on.</span></span> <span data-ttu-id="112aa-126">服务必须具有指向这些 URL 的 DNS CNAME 条目。</span><span class="sxs-lookup"><span data-stu-id="112aa-126">You must have a DNS CNAME entry for your service that points to these URLs.</span></span> <span data-ttu-id="112aa-127">例如，假设引用 、 `0.bot.contoso.com` `0.tcp.ngrok.io` 引用 `1.bot.contoso.com` `1.tcp.ngrok.io` 等。</span><span class="sxs-lookup"><span data-stu-id="112aa-127">For example, let's say `0.bot.contoso.com` refers to `0.tcp.ngrok.io`, `1.bot.contoso.com` refers to `1.tcp.ngrok.io`, and so on.</span></span>
2. <span data-ttu-id="112aa-128">URL 需要 SSL 证书。</span><span class="sxs-lookup"><span data-stu-id="112aa-128">An SSL certificate is required for your URLs.</span></span> <span data-ttu-id="112aa-129">为简单易用，请使用颁发给通配符域的 SSL 证书。</span><span class="sxs-lookup"><span data-stu-id="112aa-129">To make it easy, use an SSL certificate issued to a wild card domain.</span></span> <span data-ttu-id="112aa-130">在这种情况下，它将是 `*.bot.contoso.com` 。</span><span class="sxs-lookup"><span data-stu-id="112aa-130">In this case, it would be `*.bot.contoso.com`.</span></span> <span data-ttu-id="112aa-131">此 SSL 证书由媒体 SDK 验证，因此必须与自动程序的公共 URL 相匹配。</span><span class="sxs-lookup"><span data-stu-id="112aa-131">This SSL certificate is validated by the media SDK, so it must match your bot's public URL.</span></span> <span data-ttu-id="112aa-132">记下指纹，并安装在计算机证书中。</span><span class="sxs-lookup"><span data-stu-id="112aa-132">Note the thumbprint and install it in your machine certificates.</span></span>
3. <span data-ttu-id="112aa-133">现在，设置 TCP 隧道以将流量转发到 localhost。</span><span class="sxs-lookup"><span data-stu-id="112aa-133">Now, set up a TCP tunnel to forward the traffic to localhost.</span></span> <span data-ttu-id="112aa-134">将以下行写入 ngrok.yml 中：</span><span class="sxs-lookup"><span data-stu-id="112aa-134">Write the following lines into your ngrok.yml:</span></span>

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a><span data-ttu-id="112aa-135">启动 ngrok</span><span class="sxs-lookup"><span data-stu-id="112aa-135">Start ngrok</span></span>

<span data-ttu-id="112aa-136">现在，ngrok 配置已准备就绪，请启动它：</span><span class="sxs-lookup"><span data-stu-id="112aa-136">Now that the ngrok configuration is ready, launch it:</span></span>

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

<span data-ttu-id="112aa-137">这将启动 ngrok 并定义为 localhost 提供隧道的公共 URL。</span><span class="sxs-lookup"><span data-stu-id="112aa-137">This starts ngrok and defines the public URLs which provide the tunnels to your localhost.</span></span> <span data-ttu-id="112aa-138">下面是一个输出示例：</span><span class="sxs-lookup"><span data-stu-id="112aa-138">Following is an example of the output:</span></span>

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

<span data-ttu-id="112aa-139">此处是信号端口，是应用程序托管的端口， `12345` `8445` 也是 `12332` ngrok 公开的远程媒体端口。</span><span class="sxs-lookup"><span data-stu-id="112aa-139">Here, `12345` is the signaling port, `8445` is the application-hosted port, and `12332` is the remote media port exposed by ngrok.</span></span> <span data-ttu-id="112aa-140">请注意，我们有一个从 转发 `1.bot.contoso.com` 到 `1.tcp.ngrok.io` 。</span><span class="sxs-lookup"><span data-stu-id="112aa-140">Note that we have a forwarding from `1.bot.contoso.com` to `1.tcp.ngrok.io`.</span></span> <span data-ttu-id="112aa-141">这将用作机器人的媒体 URL。</span><span class="sxs-lookup"><span data-stu-id="112aa-141">This will be used as the media URL for the bot.</span></span> <span data-ttu-id="112aa-142">当然，这些端口号只是示例，您可以使用任何可用的端口。</span><span class="sxs-lookup"><span data-stu-id="112aa-142">Of course, these port numbers are just examples and you can use any available port.</span></span>

### <a name="update-code"></a><span data-ttu-id="112aa-143">更新代码</span><span class="sxs-lookup"><span data-stu-id="112aa-143">Update code</span></span>

<span data-ttu-id="112aa-144">ngrok 启动并运行后，更新代码以使用刚设置的配置。</span><span class="sxs-lookup"><span data-stu-id="112aa-144">After ngrok is up and running, update the code to use the config you just set up.</span></span>

#### <a name="update-signaling"></a><span data-ttu-id="112aa-145">更新信号</span><span class="sxs-lookup"><span data-stu-id="112aa-145">Update signaling</span></span>

<span data-ttu-id="112aa-146">在 BotBuilder 调用中，将 `NotificationUrl` 更改为 ngrok 提供的信号 URL。</span><span class="sxs-lookup"><span data-stu-id="112aa-146">In the BotBuilder call, change the `NotificationUrl` to the signaling URL provided by ngrok.</span></span>

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> <span data-ttu-id="112aa-147">将 signal 替换为 ngrok 提供的 信号，将 替换为接收 `NotificationEndpoint` 通知的控制器路径。</span><span class="sxs-lookup"><span data-stu-id="112aa-147">Replace signal with the one provided by ngrok and the `NotificationEndpoint` with the controller path that receives notification.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="112aa-148">中的 URL `SetNotificationUrl` 必须为 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="112aa-148">The URL in `SetNotificationUrl` must be HTTPS.</span></span>
> 
> <span data-ttu-id="112aa-149">本地实例必须侦听信号端口上的 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="112aa-149">Your local instance must be listening to HTTP traffic on the signaling port.</span></span> <span data-ttu-id="112aa-150">除非设置了端到端加密，否则呼叫和联机会议平台提出的请求将作为 localhost HTTP 流量到达机器人。</span><span class="sxs-lookup"><span data-stu-id="112aa-150">The requests made by the calls and online meetings platform will reach the bot as localhost HTTP traffic unless end-to-end encryption is set up.</span></span>

#### <a name="update-media"></a><span data-ttu-id="112aa-151">更新媒体</span><span class="sxs-lookup"><span data-stu-id="112aa-151">Update media</span></span>

<span data-ttu-id="112aa-152">更新 `MediaPlatformSettings` 你的，如下所示：</span><span class="sxs-lookup"><span data-stu-id="112aa-152">Update your `MediaPlatformSettings` as following:</span></span>

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
> <span data-ttu-id="112aa-153">中提供的证书指纹 `MediaPlatformSettings` 必须与服务 FQDN 匹配。</span><span class="sxs-lookup"><span data-stu-id="112aa-153">The certificate thumbprint provided in the `MediaPlatformSettings` must match the Service FQDN.</span></span> <span data-ttu-id="112aa-154">这就是需要 DNS 条目的原因。</span><span class="sxs-lookup"><span data-stu-id="112aa-154">That is why the DNS entries are required.</span></span>

## <a name="caveats"></a><span data-ttu-id="112aa-155">注意事项</span><span class="sxs-lookup"><span data-stu-id="112aa-155">Caveats</span></span>

- <span data-ttu-id="112aa-156">Ngrok 免费 **帐户不提供** 端到端加密。</span><span class="sxs-lookup"><span data-stu-id="112aa-156">Ngrok free accounts **don't** provide end-to-end encryption.</span></span> <span data-ttu-id="112aa-157">HTTPS 数据以 ngrok URL 结尾，数据流未加密，从 ngrok 到 `localhost` 。</span><span class="sxs-lookup"><span data-stu-id="112aa-157">The HTTPS data ends at the ngrok URL and the data flows unencrypted from ngrok to `localhost`.</span></span> <span data-ttu-id="112aa-158">如果需要端到端加密，请考虑使用付费 ngrok 帐户。</span><span class="sxs-lookup"><span data-stu-id="112aa-158">If you require end-to-end encryption, consider a paid ngrok account.</span></span> <span data-ttu-id="112aa-159">有关设置安全的端到端隧道的步骤，请参阅 [TLS](https://ngrok.com/docs#tls) 隧道。</span><span class="sxs-lookup"><span data-stu-id="112aa-159">See [TLS tunnels](https://ngrok.com/docs#tls) for steps on setting up secure end-to-end tunnels.</span></span>
- <span data-ttu-id="112aa-160">由于机器人回调 URL 是动态的，传入呼叫方案需要频繁更新 ngrok 终结点。</span><span class="sxs-lookup"><span data-stu-id="112aa-160">Because the bot callback URL is dynamic, incoming call scenarios require you to frequently update your ngrok endpoints.</span></span> <span data-ttu-id="112aa-161">解决此问题的一个方法就是使用付费 ngrok 帐户，该帐户提供你可以将机器人和平台指向的固定子域。</span><span class="sxs-lookup"><span data-stu-id="112aa-161">One way to fix this is to use a paid ngrok account which provides fixed subdomains to which you can point your bot and the platform.</span></span>
- <span data-ttu-id="112aa-162">Ngrok 隧道还可以与 Azure [Service Fabric 一同使用](/azure/service-fabric/service-fabric-overview)。</span><span class="sxs-lookup"><span data-stu-id="112aa-162">Ngrok tunnels can also be used with [Azure Service Fabric](/azure/service-fabric/service-fabric-overview).</span></span> <span data-ttu-id="112aa-163">有关操作示例，请参阅 [HueBot 示例应用](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot)。</span><span class="sxs-lookup"><span data-stu-id="112aa-163">For an example of how to do this, see the [HueBot sample app](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot).</span></span>
