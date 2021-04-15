---
title: 通过团队中的速率限制来优化你的智能机器人
description: Microsoft Teams 中的速率限制和最佳做法
ms.topic: conceptual
keywords: teams 机器人速率限制
ms.openlocfilehash: 245c51fc736e5f888299535c3e50ec6232183623
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696995"
---
# <a name="optimize-your-bot-with-rate-limiting-in-teams"></a><span data-ttu-id="61ac0-104">通过团队中的速率限制来优化你的智能机器人</span><span class="sxs-lookup"><span data-stu-id="61ac0-104">Optimize your bot with rate limiting in Teams</span></span>

<span data-ttu-id="61ac0-105">速率限制是一种将邮件限制为特定最大频率的方法。</span><span class="sxs-lookup"><span data-stu-id="61ac0-105">Rate limiting is a method to limit messages to a certain maximum frequency.</span></span> <span data-ttu-id="61ac0-106">一般来说，您的应用程序必须限制向单个聊天或频道对话发布的消息数。</span><span class="sxs-lookup"><span data-stu-id="61ac0-106">As a general principle, your application must limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="61ac0-107">这可确保最佳体验，并且邮件不会显示为垃圾邮件给用户。</span><span class="sxs-lookup"><span data-stu-id="61ac0-107">This ensures an optimal experience and messages do not appear as spam to your users.</span></span>

<span data-ttu-id="61ac0-108">为了保护 Microsoft Teams 及其用户，机器人 API 提供了传入请求的速率限制。</span><span class="sxs-lookup"><span data-stu-id="61ac0-108">To protect Microsoft Teams and its users, the bot APIs provide a rate limit for incoming requests.</span></span> <span data-ttu-id="61ac0-109">超过此限制的应用将收到 `HTTP 429 Too Many Requests` 错误状态。</span><span class="sxs-lookup"><span data-stu-id="61ac0-109">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="61ac0-110">所有请求都受同一速率限制策略的限制，包括发送邮件、频道枚举和名单提取。</span><span class="sxs-lookup"><span data-stu-id="61ac0-110">All requests are subject to the same rate limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="61ac0-111">由于速率限制的确切值可能会发生变化，因此当 API 返回 时，应用程序必须实现相应的退步行为 `HTTP 429 Too Many Requests` 。</span><span class="sxs-lookup"><span data-stu-id="61ac0-111">As the exact values of rate limits are subject to change, your application must implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handle-rate-limits"></a><span data-ttu-id="61ac0-112">处理速率限制</span><span class="sxs-lookup"><span data-stu-id="61ac0-112">Handle rate limits</span></span>

<span data-ttu-id="61ac0-113">发出自动程序生成器 SDK 操作时，可以处理 `Microsoft.Rest.HttpOperationException` 和检查状态代码。</span><span class="sxs-lookup"><span data-stu-id="61ac0-113">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

<span data-ttu-id="61ac0-114">以下代码显示了处理速率限制的示例：</span><span class="sxs-lookup"><span data-stu-id="61ac0-114">The following code shows an example of handling rate limits:</span></span>

```csharp
try
{
    // Perform Bot Framework operation
    // for example, await connector.Conversations.UpdateActivityAsync(reply);
}
catch (HttpOperationException ex)
{
    if (ex.Response != null && (uint)ex.Response.StatusCode ==  429)
    {
        //Perform retry of the above operation/Action method
    }
}
```

<span data-ttu-id="61ac0-115">处理自动程序速率限制后，可以使用指数 `HTTP 429` 退步处理响应。</span><span class="sxs-lookup"><span data-stu-id="61ac0-115">After you handle rate limits for bots, you can handle `HTTP 429` responses using an exponential backoff.</span></span>

## <a name="handle-http-429-responses"></a><span data-ttu-id="61ac0-116">处理 `HTTP 429` 响应</span><span class="sxs-lookup"><span data-stu-id="61ac0-116">Handle `HTTP 429` responses</span></span>

<span data-ttu-id="61ac0-117">通常，必须采取简单的预防措施以避免收到 `HTTP 429` 响应。</span><span class="sxs-lookup"><span data-stu-id="61ac0-117">In general, you must take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="61ac0-118">例如，避免向同一个人对话或频道对话发出多个请求。</span><span class="sxs-lookup"><span data-stu-id="61ac0-118">For example, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="61ac0-119">相反，请创建一批 API 请求。</span><span class="sxs-lookup"><span data-stu-id="61ac0-119">Instead, create a batch of the API requests.</span></span>

<span data-ttu-id="61ac0-120">建议将指数退约与随机抖动一同处理 429。</span><span class="sxs-lookup"><span data-stu-id="61ac0-120">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="61ac0-121">这将确保多个请求不会在重试时引入冲突。</span><span class="sxs-lookup"><span data-stu-id="61ac0-121">This ensures that multiple requests do not introduce collisions on retries.</span></span>

<span data-ttu-id="61ac0-122">处理响应 `HTTP 429` 后，可以浏览检测暂时性异常的示例。</span><span class="sxs-lookup"><span data-stu-id="61ac0-122">After you handle `HTTP 429` responses, you can go through the example for detecting transient exceptions.</span></span>

## <a name="detect-transient-exceptions-example"></a><span data-ttu-id="61ac0-123">检测暂时性异常示例</span><span class="sxs-lookup"><span data-stu-id="61ac0-123">Detect transient exceptions example</span></span>

<span data-ttu-id="61ac0-124">以下代码显示了使用瞬态故障处理应用程序块的指数退路的示例：</span><span class="sxs-lookup"><span data-stu-id="61ac0-124">The following code shows an example of using exponential backoff using the transient fault handling application block:</span></span>

```csharp
public class BotSdkTransientExceptionDetectionStrategy : ITransientErrorDetectionStrategy
    {
        // List of error codes to retry on
        List<int> transientErrorStatusCodes = new List<int>() { 429 };

        public bool IsTransient(Exception ex)
        {
            if (ex.Message.Contains("429"))
                return true;

            var httpOperationException = ex as HttpOperationException;
            if (httpOperationException != null)
            {
                return httpOperationException.Response != null &&
                        transientErrorStatusCodes.Contains((int)httpOperationException.Response.StatusCode);
            }

            return false;
        }
    }
```

<span data-ttu-id="61ac0-125">可以使用瞬态故障处理执行回发 [并重试](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)。</span><span class="sxs-lookup"><span data-stu-id="61ac0-125">You can perform backoff and retries using [transient fault handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="61ac0-126">有关获取和安装 NuGet 程序包的指南，请参阅将瞬态 [错误处理应用程序块添加到你的解决方案](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)。</span><span class="sxs-lookup"><span data-stu-id="61ac0-126">For guidelines on obtaining and installing the NuGet package, see [adding the transient fault handling application block to your solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span></span> <span data-ttu-id="61ac0-127">另请参阅 [瞬态故障处理](/azure/architecture/best-practices/transient-faults)。</span><span class="sxs-lookup"><span data-stu-id="61ac0-127">See also [transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

<span data-ttu-id="61ac0-128">完成检测暂时性异常的示例后，请浏览指数退步示例。</span><span class="sxs-lookup"><span data-stu-id="61ac0-128">After you go through the example for detecting transient exceptions, go through the exponential backoff example.</span></span> <span data-ttu-id="61ac0-129">可以使用指数退步，而不是在失败时重试。</span><span class="sxs-lookup"><span data-stu-id="61ac0-129">You can use exponential backoff instead of retrying on failures.</span></span>

## <a name="backoff-example"></a><span data-ttu-id="61ac0-130">退市示例</span><span class="sxs-lookup"><span data-stu-id="61ac0-130">Backoff example</span></span>

<span data-ttu-id="61ac0-131">除了检测速率限制之外，还可以执行指数退市。</span><span class="sxs-lookup"><span data-stu-id="61ac0-131">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

<span data-ttu-id="61ac0-132">以下代码显示了指数退步的示例：</span><span class="sxs-lookup"><span data-stu-id="61ac0-132">The following code shows an example of exponential backoff:</span></span>

```csharp
/**
* The first parameter specifies the number of retries before failing the operation.
* The second parameter specifies the minimum and maximum backoff time respectively.
* The last parameter is used to add a randomized  +/- 20% delta to avoid numerous clients retrying simultaneously.
*/
var exponentialBackoffRetryStrategy = new ExponentialBackoff(3, TimeSpan.FromSeconds(2),
                        TimeSpan.FromSeconds(20), TimeSpan.FromSeconds(1));


// Define the Retry Policy
var retryPolicy = new RetryPolicy(new BotSdkTransientExceptionDetectionStrategy(), exponentialBackoffRetryStrategy);

//Execute any bot sdk action
await retryPolicy.ExecuteAsync(() => connector.Conversations.ReplyToActivityAsync( (Activity)reply) ).ConfigureAwait(false);
```

<span data-ttu-id="61ac0-133">您还可以使用本节 `System.Action` 中所述的重试策略执行方法。</span><span class="sxs-lookup"><span data-stu-id="61ac0-133">You can also perform a `System.Action` method execution with the retry policy described in this section.</span></span> <span data-ttu-id="61ac0-134">引用的库还允许您指定固定间隔或线性退信机制。</span><span class="sxs-lookup"><span data-stu-id="61ac0-134">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="61ac0-135">将值和策略存储在配置文件中，以运行时微调和调整值。</span><span class="sxs-lookup"><span data-stu-id="61ac0-135">Store the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="61ac0-136">有关详细信息，请参阅 [重试模式](/azure/architecture/patterns/retry)。</span><span class="sxs-lookup"><span data-stu-id="61ac0-136">For more information, see [retry patterns](/azure/architecture/patterns/retry).</span></span>

<span data-ttu-id="61ac0-137">您还可以使用每个机器人每线程限制处理速率限制。</span><span class="sxs-lookup"><span data-stu-id="61ac0-137">You can also handle rate limit using the per bot per thread limit.</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="61ac0-138">每个机器人每线程限制</span><span class="sxs-lookup"><span data-stu-id="61ac0-138">Per bot per thread limit</span></span>

>[!NOTE]
> <span data-ttu-id="61ac0-139">在服务级别拆分邮件会导致每秒请求数超过 RPS () 。</span><span class="sxs-lookup"><span data-stu-id="61ac0-139">Message splitting at the service level results in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="61ac0-140">如果担心接近限制，则必须实施 [退约策略](#backoff-example)。</span><span class="sxs-lookup"><span data-stu-id="61ac0-140">If you are concerned about approaching the limits, you must implement the [backoff strategy](#backoff-example).</span></span> <span data-ttu-id="61ac0-141">本节中提供的值仅用于估计。</span><span class="sxs-lookup"><span data-stu-id="61ac0-141">The values provided in this section are for estimation only.</span></span>

<span data-ttu-id="61ac0-142">每个线程的自动程序限制控制允许机器人在单个对话上生成的流量。</span><span class="sxs-lookup"><span data-stu-id="61ac0-142">The per bot per thread limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="61ac0-143">此处的对话是机器人和用户、群聊或团队中的频道之间的一对一对话。</span><span class="sxs-lookup"><span data-stu-id="61ac0-143">A conversation here is 1:1 between bot and user, a group chat, or a channel in a team.</span></span>

<span data-ttu-id="61ac0-144">下表提供了每个机器人每个线程的限制：</span><span class="sxs-lookup"><span data-stu-id="61ac0-144">The following table provides the per bot per thread limits:</span></span>

| <span data-ttu-id="61ac0-145">方案</span><span class="sxs-lookup"><span data-stu-id="61ac0-145">Scenario</span></span> | <span data-ttu-id="61ac0-146">时间段（以秒表示）</span><span class="sxs-lookup"><span data-stu-id="61ac0-146">Time period in seconds</span></span> | <span data-ttu-id="61ac0-147">允许的最大操作数</span><span class="sxs-lookup"><span data-stu-id="61ac0-147">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="61ac0-148">发送到对话</span><span class="sxs-lookup"><span data-stu-id="61ac0-148">Send to conversation</span></span> | <span data-ttu-id="61ac0-149">1</span><span class="sxs-lookup"><span data-stu-id="61ac0-149">1</span></span> | <span data-ttu-id="61ac0-150">7 </span><span class="sxs-lookup"><span data-stu-id="61ac0-150">7</span></span> |
| <span data-ttu-id="61ac0-151">发送到对话</span><span class="sxs-lookup"><span data-stu-id="61ac0-151">Send to conversation</span></span> | <span data-ttu-id="61ac0-152">2</span><span class="sxs-lookup"><span data-stu-id="61ac0-152">2</span></span> | <span data-ttu-id="61ac0-153">8 </span><span class="sxs-lookup"><span data-stu-id="61ac0-153">8</span></span> |
| <span data-ttu-id="61ac0-154">发送到对话</span><span class="sxs-lookup"><span data-stu-id="61ac0-154">Send to conversation</span></span> | <span data-ttu-id="61ac0-155">30</span><span class="sxs-lookup"><span data-stu-id="61ac0-155">30</span></span> | <span data-ttu-id="61ac0-156">60</span><span class="sxs-lookup"><span data-stu-id="61ac0-156">60</span></span> |
| <span data-ttu-id="61ac0-157">发送到对话</span><span class="sxs-lookup"><span data-stu-id="61ac0-157">Send to conversation</span></span> | <span data-ttu-id="61ac0-158">3600</span><span class="sxs-lookup"><span data-stu-id="61ac0-158">3600</span></span> | <span data-ttu-id="61ac0-159">1800</span><span class="sxs-lookup"><span data-stu-id="61ac0-159">1800</span></span> |
| <span data-ttu-id="61ac0-160">创建对话</span><span class="sxs-lookup"><span data-stu-id="61ac0-160">Create conversation</span></span> | <span data-ttu-id="61ac0-161">1</span><span class="sxs-lookup"><span data-stu-id="61ac0-161">1</span></span> | <span data-ttu-id="61ac0-162">7 </span><span class="sxs-lookup"><span data-stu-id="61ac0-162">7</span></span> |
| <span data-ttu-id="61ac0-163">创建对话</span><span class="sxs-lookup"><span data-stu-id="61ac0-163">Create conversation</span></span> | <span data-ttu-id="61ac0-164">2</span><span class="sxs-lookup"><span data-stu-id="61ac0-164">2</span></span> | <span data-ttu-id="61ac0-165">8 </span><span class="sxs-lookup"><span data-stu-id="61ac0-165">8</span></span> |
| <span data-ttu-id="61ac0-166">创建对话</span><span class="sxs-lookup"><span data-stu-id="61ac0-166">Create conversation</span></span> | <span data-ttu-id="61ac0-167">30</span><span class="sxs-lookup"><span data-stu-id="61ac0-167">30</span></span> | <span data-ttu-id="61ac0-168">60</span><span class="sxs-lookup"><span data-stu-id="61ac0-168">60</span></span> |
| <span data-ttu-id="61ac0-169">创建对话</span><span class="sxs-lookup"><span data-stu-id="61ac0-169">Create conversation</span></span> | <span data-ttu-id="61ac0-170">3600</span><span class="sxs-lookup"><span data-stu-id="61ac0-170">3600</span></span> | <span data-ttu-id="61ac0-171">1800</span><span class="sxs-lookup"><span data-stu-id="61ac0-171">1800</span></span> |
| <span data-ttu-id="61ac0-172">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="61ac0-172">Get conversation members</span></span>| <span data-ttu-id="61ac0-173">1</span><span class="sxs-lookup"><span data-stu-id="61ac0-173">1</span></span> | <span data-ttu-id="61ac0-174">14 </span><span class="sxs-lookup"><span data-stu-id="61ac0-174">14</span></span> |
| <span data-ttu-id="61ac0-175">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="61ac0-175">Get conversation members</span></span>| <span data-ttu-id="61ac0-176">2</span><span class="sxs-lookup"><span data-stu-id="61ac0-176">2</span></span> | <span data-ttu-id="61ac0-177">16 </span><span class="sxs-lookup"><span data-stu-id="61ac0-177">16</span></span> |
| <span data-ttu-id="61ac0-178">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="61ac0-178">Get conversation members</span></span>| <span data-ttu-id="61ac0-179">30</span><span class="sxs-lookup"><span data-stu-id="61ac0-179">30</span></span> | <span data-ttu-id="61ac0-180">120</span><span class="sxs-lookup"><span data-stu-id="61ac0-180">120</span></span> |
| <span data-ttu-id="61ac0-181">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="61ac0-181">Get conversation members</span></span>| <span data-ttu-id="61ac0-182">3600</span><span class="sxs-lookup"><span data-stu-id="61ac0-182">3600</span></span> | <span data-ttu-id="61ac0-183">3600</span><span class="sxs-lookup"><span data-stu-id="61ac0-183">3600</span></span> |
| <span data-ttu-id="61ac0-184">获取对话</span><span class="sxs-lookup"><span data-stu-id="61ac0-184">Get conversations</span></span> | <span data-ttu-id="61ac0-185">1</span><span class="sxs-lookup"><span data-stu-id="61ac0-185">1</span></span> | <span data-ttu-id="61ac0-186">14 </span><span class="sxs-lookup"><span data-stu-id="61ac0-186">14</span></span> |
| <span data-ttu-id="61ac0-187">获取对话</span><span class="sxs-lookup"><span data-stu-id="61ac0-187">Get conversations</span></span> | <span data-ttu-id="61ac0-188">2</span><span class="sxs-lookup"><span data-stu-id="61ac0-188">2</span></span> | <span data-ttu-id="61ac0-189">16 </span><span class="sxs-lookup"><span data-stu-id="61ac0-189">16</span></span> |
| <span data-ttu-id="61ac0-190">获取对话</span><span class="sxs-lookup"><span data-stu-id="61ac0-190">Get conversations</span></span> | <span data-ttu-id="61ac0-191">30</span><span class="sxs-lookup"><span data-stu-id="61ac0-191">30</span></span> | <span data-ttu-id="61ac0-192">120</span><span class="sxs-lookup"><span data-stu-id="61ac0-192">120</span></span> |
| <span data-ttu-id="61ac0-193">获取对话</span><span class="sxs-lookup"><span data-stu-id="61ac0-193">Get conversations</span></span> | <span data-ttu-id="61ac0-194">3600</span><span class="sxs-lookup"><span data-stu-id="61ac0-194">3600</span></span> | <span data-ttu-id="61ac0-195">3600</span><span class="sxs-lookup"><span data-stu-id="61ac0-195">3600</span></span> |

>[!NOTE]
> <span data-ttu-id="61ac0-196">早期版本和 `TeamsInfo.getMembers` API `TeamsInfo.GetMembersAsync` 被弃用。</span><span class="sxs-lookup"><span data-stu-id="61ac0-196">Previous versions of `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs are being deprecated.</span></span> <span data-ttu-id="61ac0-197">它们被限制为每分钟五个请求，并且每个团队最多返回 10，000 个成员。</span><span class="sxs-lookup"><span data-stu-id="61ac0-197">They are throttled to five requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="61ac0-198">若要更新 Bot Framework SDK 和代码以使用最新的分页 API 终结点，请参阅团队和聊天成员的自动程序 [API 更改](../../resources/team-chat-member-api-changes.md)。</span><span class="sxs-lookup"><span data-stu-id="61ac0-198">To update your Bot Framework SDK and the code to use the latest paginated API endpoints, see [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span></span>

<span data-ttu-id="61ac0-199">您还可以使用所有机器人的按线程限制处理速率限制。</span><span class="sxs-lookup"><span data-stu-id="61ac0-199">You can also handle rate limit using the per thread limit for all bots.</span></span>

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="61ac0-200">所有自动程序每线程限制</span><span class="sxs-lookup"><span data-stu-id="61ac0-200">Per thread limit for all bots</span></span>

<span data-ttu-id="61ac0-201">所有机器人的线程限制控制允许所有机器人在单个对话中生成的流量。</span><span class="sxs-lookup"><span data-stu-id="61ac0-201">The per thread limit for all bots controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="61ac0-202">此处的对话是机器人和用户、群聊或团队中的频道之间的一对一对话。</span><span class="sxs-lookup"><span data-stu-id="61ac0-202">A conversation here is 1:1 between bot and user, a group chat, or a channel in a team.</span></span>

<span data-ttu-id="61ac0-203">下表提供了所有自动程序每线程的限制：</span><span class="sxs-lookup"><span data-stu-id="61ac0-203">The following table provides the per thread limit for all bots:</span></span>

| <span data-ttu-id="61ac0-204">方案</span><span class="sxs-lookup"><span data-stu-id="61ac0-204">Scenario</span></span> | <span data-ttu-id="61ac0-205">时间段（以秒表示）</span><span class="sxs-lookup"><span data-stu-id="61ac0-205">Time period in seconds</span></span> | <span data-ttu-id="61ac0-206">允许的最大操作数</span><span class="sxs-lookup"><span data-stu-id="61ac0-206">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="61ac0-207">发送到对话</span><span class="sxs-lookup"><span data-stu-id="61ac0-207">Send to conversation</span></span> | <span data-ttu-id="61ac0-208">1</span><span class="sxs-lookup"><span data-stu-id="61ac0-208">1</span></span> | <span data-ttu-id="61ac0-209">14 </span><span class="sxs-lookup"><span data-stu-id="61ac0-209">14</span></span> |
| <span data-ttu-id="61ac0-210">发送到对话</span><span class="sxs-lookup"><span data-stu-id="61ac0-210">Send to conversation</span></span> | <span data-ttu-id="61ac0-211">2</span><span class="sxs-lookup"><span data-stu-id="61ac0-211">2</span></span> | <span data-ttu-id="61ac0-212">16 </span><span class="sxs-lookup"><span data-stu-id="61ac0-212">16</span></span> |
| <span data-ttu-id="61ac0-213">创建对话</span><span class="sxs-lookup"><span data-stu-id="61ac0-213">Create conversation</span></span> | <span data-ttu-id="61ac0-214">1</span><span class="sxs-lookup"><span data-stu-id="61ac0-214">1</span></span> | <span data-ttu-id="61ac0-215">14 </span><span class="sxs-lookup"><span data-stu-id="61ac0-215">14</span></span> |
| <span data-ttu-id="61ac0-216">创建对话</span><span class="sxs-lookup"><span data-stu-id="61ac0-216">Create conversation</span></span> | <span data-ttu-id="61ac0-217">2</span><span class="sxs-lookup"><span data-stu-id="61ac0-217">2</span></span> | <span data-ttu-id="61ac0-218">16 </span><span class="sxs-lookup"><span data-stu-id="61ac0-218">16</span></span> |
| <span data-ttu-id="61ac0-219">创建对话</span><span class="sxs-lookup"><span data-stu-id="61ac0-219">Create conversation</span></span>| <span data-ttu-id="61ac0-220">1</span><span class="sxs-lookup"><span data-stu-id="61ac0-220">1</span></span> | <span data-ttu-id="61ac0-221">14 </span><span class="sxs-lookup"><span data-stu-id="61ac0-221">14</span></span> |
| <span data-ttu-id="61ac0-222">创建对话</span><span class="sxs-lookup"><span data-stu-id="61ac0-222">Create conversation</span></span>| <span data-ttu-id="61ac0-223">2</span><span class="sxs-lookup"><span data-stu-id="61ac0-223">2</span></span> | <span data-ttu-id="61ac0-224">16 </span><span class="sxs-lookup"><span data-stu-id="61ac0-224">16</span></span> |
| <span data-ttu-id="61ac0-225">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="61ac0-225">Get conversation members</span></span>| <span data-ttu-id="61ac0-226">1</span><span class="sxs-lookup"><span data-stu-id="61ac0-226">1</span></span> | <span data-ttu-id="61ac0-227">28</span><span class="sxs-lookup"><span data-stu-id="61ac0-227">28</span></span> |
| <span data-ttu-id="61ac0-228">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="61ac0-228">Get conversation members</span></span>| <span data-ttu-id="61ac0-229">2</span><span class="sxs-lookup"><span data-stu-id="61ac0-229">2</span></span> | <span data-ttu-id="61ac0-230">32</span><span class="sxs-lookup"><span data-stu-id="61ac0-230">32</span></span> |
| <span data-ttu-id="61ac0-231">获取对话</span><span class="sxs-lookup"><span data-stu-id="61ac0-231">Get conversations</span></span> | <span data-ttu-id="61ac0-232">1</span><span class="sxs-lookup"><span data-stu-id="61ac0-232">1</span></span> | <span data-ttu-id="61ac0-233">28</span><span class="sxs-lookup"><span data-stu-id="61ac0-233">28</span></span> |
| <span data-ttu-id="61ac0-234">获取对话</span><span class="sxs-lookup"><span data-stu-id="61ac0-234">Get conversations</span></span> | <span data-ttu-id="61ac0-235">2</span><span class="sxs-lookup"><span data-stu-id="61ac0-235">2</span></span> | <span data-ttu-id="61ac0-236">32</span><span class="sxs-lookup"><span data-stu-id="61ac0-236">32</span></span> |

## <a name="next-step"></a><span data-ttu-id="61ac0-237">后续步骤</span><span class="sxs-lookup"><span data-stu-id="61ac0-237">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="61ac0-238">通话和会议智能机器人</span><span class="sxs-lookup"><span data-stu-id="61ac0-238">Calls and meetings bots</span></span>](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

