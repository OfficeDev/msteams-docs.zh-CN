---
title: 通过团队中的速率限制来优化你的智能机器人
description: Microsoft Teams 中的速率限制和最佳做法
ms.topic: conceptual
keywords: teams 机器人速率限制
ms.openlocfilehash: 690d09e4a3b611c024f32d3776ca73e42d63ee7f
ms.sourcegitcommit: 35bc2a31b92f3f7c6524373108f095a870d9ad09
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2021
ms.locfileid: "51922501"
---
# <a name="optimize-your-bot-with-rate-limiting-in-teams"></a><span data-ttu-id="c9b51-104">通过团队中的速率限制来优化你的智能机器人</span><span class="sxs-lookup"><span data-stu-id="c9b51-104">Optimize your bot with rate limiting in Teams</span></span>

<span data-ttu-id="c9b51-105">速率限制是一种将邮件限制为特定最大频率的方法。</span><span class="sxs-lookup"><span data-stu-id="c9b51-105">Rate limiting is a method to limit messages to a certain maximum frequency.</span></span> <span data-ttu-id="c9b51-106">一般来说，您的应用程序必须限制向单个聊天或频道对话发布的消息数。</span><span class="sxs-lookup"><span data-stu-id="c9b51-106">As a general principle, your application must limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="c9b51-107">这可确保最佳体验，并且邮件不会显示为垃圾邮件给用户。</span><span class="sxs-lookup"><span data-stu-id="c9b51-107">This ensures an optimal experience and messages do not appear as spam to your users.</span></span>

<span data-ttu-id="c9b51-108">为了保护 Microsoft Teams 及其用户，机器人 API 提供了传入请求的速率限制。</span><span class="sxs-lookup"><span data-stu-id="c9b51-108">To protect Microsoft Teams and its users, the bot APIs provide a rate limit for incoming requests.</span></span> <span data-ttu-id="c9b51-109">超过此限制的应用将收到 `HTTP 429 Too Many Requests` 错误状态。</span><span class="sxs-lookup"><span data-stu-id="c9b51-109">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="c9b51-110">所有请求都受同一速率限制策略的限制，包括发送邮件、频道枚举和名单提取。</span><span class="sxs-lookup"><span data-stu-id="c9b51-110">All requests are subject to the same rate limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="c9b51-111">由于速率限制的确切值可能会发生变化，因此当 API 返回 时，应用程序必须实现相应的退步行为 `HTTP 429 Too Many Requests` 。</span><span class="sxs-lookup"><span data-stu-id="c9b51-111">As the exact values of rate limits are subject to change, your application must implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handle-rate-limits"></a><span data-ttu-id="c9b51-112">处理速率限制</span><span class="sxs-lookup"><span data-stu-id="c9b51-112">Handle rate limits</span></span>

<span data-ttu-id="c9b51-113">发出自动程序生成器 SDK 操作时，可以处理 `Microsoft.Rest.HttpOperationException` 和检查状态代码。</span><span class="sxs-lookup"><span data-stu-id="c9b51-113">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

<span data-ttu-id="c9b51-114">以下代码显示了处理速率限制的示例：</span><span class="sxs-lookup"><span data-stu-id="c9b51-114">The following code shows an example of handling rate limits:</span></span>

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

<span data-ttu-id="c9b51-115">处理自动程序速率限制后，可以使用指数 `HTTP 429` 退步处理响应。</span><span class="sxs-lookup"><span data-stu-id="c9b51-115">After you handle rate limits for bots, you can handle `HTTP 429` responses using an exponential backoff.</span></span>

## <a name="handle-http-429-responses"></a><span data-ttu-id="c9b51-116">处理 `HTTP 429` 响应</span><span class="sxs-lookup"><span data-stu-id="c9b51-116">Handle `HTTP 429` responses</span></span>

<span data-ttu-id="c9b51-117">通常，必须采取简单的预防措施以避免收到 `HTTP 429` 响应。</span><span class="sxs-lookup"><span data-stu-id="c9b51-117">In general, you must take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="c9b51-118">例如，避免向同一个人对话或频道对话发出多个请求。</span><span class="sxs-lookup"><span data-stu-id="c9b51-118">For example, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="c9b51-119">相反，请创建一批 API 请求。</span><span class="sxs-lookup"><span data-stu-id="c9b51-119">Instead, create a batch of the API requests.</span></span>

<span data-ttu-id="c9b51-120">建议将指数退约与随机抖动一同处理 429。</span><span class="sxs-lookup"><span data-stu-id="c9b51-120">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="c9b51-121">这将确保多个请求不会在重试时引入冲突。</span><span class="sxs-lookup"><span data-stu-id="c9b51-121">This ensures that multiple requests do not introduce collisions on retries.</span></span>

<span data-ttu-id="c9b51-122">处理响应 `HTTP 429` 后，可以浏览检测暂时性异常的示例。</span><span class="sxs-lookup"><span data-stu-id="c9b51-122">After you handle `HTTP 429` responses, you can go through the example for detecting transient exceptions.</span></span>

## <a name="detect-transient-exceptions-example"></a><span data-ttu-id="c9b51-123">检测暂时性异常示例</span><span class="sxs-lookup"><span data-stu-id="c9b51-123">Detect transient exceptions example</span></span>

<span data-ttu-id="c9b51-124">以下代码显示了使用瞬态故障处理应用程序块的指数退路的示例：</span><span class="sxs-lookup"><span data-stu-id="c9b51-124">The following code shows an example of using exponential backoff using the transient fault handling application block:</span></span>

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

<span data-ttu-id="c9b51-125">可以使用瞬态故障处理执行回发 [并重试](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)。</span><span class="sxs-lookup"><span data-stu-id="c9b51-125">You can perform backoff and retries using [transient fault handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="c9b51-126">有关获取和安装 NuGet 程序包的指南，请参阅将瞬态 [错误处理应用程序块添加到你的解决方案](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)。</span><span class="sxs-lookup"><span data-stu-id="c9b51-126">For guidelines on obtaining and installing the NuGet package, see [adding the transient fault handling application block to your solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span></span> <span data-ttu-id="c9b51-127">另请参阅 [瞬态故障处理](/azure/architecture/best-practices/transient-faults)。</span><span class="sxs-lookup"><span data-stu-id="c9b51-127">See also [transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

<span data-ttu-id="c9b51-128">完成检测暂时性异常的示例后，请浏览指数退步示例。</span><span class="sxs-lookup"><span data-stu-id="c9b51-128">After you go through the example for detecting transient exceptions, go through the exponential backoff example.</span></span> <span data-ttu-id="c9b51-129">可以使用指数退步，而不是在失败时重试。</span><span class="sxs-lookup"><span data-stu-id="c9b51-129">You can use exponential backoff instead of retrying on failures.</span></span>

## <a name="backoff-example"></a><span data-ttu-id="c9b51-130">退市示例</span><span class="sxs-lookup"><span data-stu-id="c9b51-130">Backoff example</span></span>

<span data-ttu-id="c9b51-131">除了检测速率限制之外，还可以执行指数退市。</span><span class="sxs-lookup"><span data-stu-id="c9b51-131">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

<span data-ttu-id="c9b51-132">以下代码显示了指数退步的示例：</span><span class="sxs-lookup"><span data-stu-id="c9b51-132">The following code shows an example of exponential backoff:</span></span>

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

<span data-ttu-id="c9b51-133">您还可以使用本节 `System.Action` 中所述的重试策略执行方法。</span><span class="sxs-lookup"><span data-stu-id="c9b51-133">You can also perform a `System.Action` method execution with the retry policy described in this section.</span></span> <span data-ttu-id="c9b51-134">引用的库还允许您指定固定间隔或线性退信机制。</span><span class="sxs-lookup"><span data-stu-id="c9b51-134">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="c9b51-135">将值和策略存储在配置文件中，以运行时微调和调整值。</span><span class="sxs-lookup"><span data-stu-id="c9b51-135">Store the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="c9b51-136">有关详细信息，请参阅 [重试模式](/azure/architecture/patterns/retry)。</span><span class="sxs-lookup"><span data-stu-id="c9b51-136">For more information, see [retry patterns](/azure/architecture/patterns/retry).</span></span>

<span data-ttu-id="c9b51-137">您还可以使用每个机器人每线程限制处理速率限制。</span><span class="sxs-lookup"><span data-stu-id="c9b51-137">You can also handle rate limit using the per bot per thread limit.</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="c9b51-138">每个机器人每线程限制</span><span class="sxs-lookup"><span data-stu-id="c9b51-138">Per bot per thread limit</span></span>

<span data-ttu-id="c9b51-139">每个线程每个机器人限制控制允许机器人在单个对话中生成的流量。</span><span class="sxs-lookup"><span data-stu-id="c9b51-139">The per bot per thread limit controls the traffic that a bot is allowed to generate in a single conversation.</span></span> <span data-ttu-id="c9b51-140">聊天机器人和用户、群聊或团队中的频道之间的对话为 1：1。</span><span class="sxs-lookup"><span data-stu-id="c9b51-140">A conversation is 1:1 between bot and user, a group chat, or a channel in a team.</span></span> <span data-ttu-id="c9b51-141">因此，如果应用程序向每个用户发送一条自动程序消息，则线程限制不会受到限制。</span><span class="sxs-lookup"><span data-stu-id="c9b51-141">So, if the application sends one bot message to each user, the thread limit does not throttle.</span></span>

>[!NOTE]
> * <span data-ttu-id="c9b51-142">3600 秒和 1800 个操作线程限制仅适用于向单个用户发送多个自动程序消息的情况。</span><span class="sxs-lookup"><span data-stu-id="c9b51-142">The thread limit of 3600 seconds and 1800 operations applies only if multiple bot messages are sent to a single user.</span></span> 
> * <span data-ttu-id="c9b51-143">每个租户每个应用的全局限制为每秒 30 个请求数 (RPS) 。</span><span class="sxs-lookup"><span data-stu-id="c9b51-143">The global limit per app per tenant is 30 Requests Per Second (RPS).</span></span> <span data-ttu-id="c9b51-144">因此，每秒自动程序消息总数不能超过线程限制。</span><span class="sxs-lookup"><span data-stu-id="c9b51-144">Hence, the total number of bot messages per second must not cross the thread limit.</span></span>
> * <span data-ttu-id="c9b51-145">服务级别的邮件拆分结果高于预期的 RPS。</span><span class="sxs-lookup"><span data-stu-id="c9b51-145">Message splitting at the service level results in higher than expected RPS.</span></span> <span data-ttu-id="c9b51-146">如果担心接近限制，则必须实施 [退约策略](#backoff-example)。</span><span class="sxs-lookup"><span data-stu-id="c9b51-146">If you are concerned about approaching the limits, you must implement the [backoff strategy](#backoff-example).</span></span> <span data-ttu-id="c9b51-147">本节中提供的值仅用于估计。</span><span class="sxs-lookup"><span data-stu-id="c9b51-147">The values provided in this section are for estimation only.</span></span>

<span data-ttu-id="c9b51-148">下表提供了每个机器人每个线程的限制：</span><span class="sxs-lookup"><span data-stu-id="c9b51-148">The following table provides the per bot per thread limits:</span></span>

| <span data-ttu-id="c9b51-149">方案</span><span class="sxs-lookup"><span data-stu-id="c9b51-149">Scenario</span></span> | <span data-ttu-id="c9b51-150">时间段（以秒表示）</span><span class="sxs-lookup"><span data-stu-id="c9b51-150">Time period in seconds</span></span> | <span data-ttu-id="c9b51-151">允许的最大操作数</span><span class="sxs-lookup"><span data-stu-id="c9b51-151">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c9b51-152">发送到对话</span><span class="sxs-lookup"><span data-stu-id="c9b51-152">Send to conversation</span></span> | <span data-ttu-id="c9b51-153">1</span><span class="sxs-lookup"><span data-stu-id="c9b51-153">1</span></span> | <span data-ttu-id="c9b51-154">7 </span><span class="sxs-lookup"><span data-stu-id="c9b51-154">7</span></span> |
| <span data-ttu-id="c9b51-155">发送到对话</span><span class="sxs-lookup"><span data-stu-id="c9b51-155">Send to conversation</span></span> | <span data-ttu-id="c9b51-156">2</span><span class="sxs-lookup"><span data-stu-id="c9b51-156">2</span></span> | <span data-ttu-id="c9b51-157">8 </span><span class="sxs-lookup"><span data-stu-id="c9b51-157">8</span></span> |
| <span data-ttu-id="c9b51-158">发送到对话</span><span class="sxs-lookup"><span data-stu-id="c9b51-158">Send to conversation</span></span> | <span data-ttu-id="c9b51-159">30</span><span class="sxs-lookup"><span data-stu-id="c9b51-159">30</span></span> | <span data-ttu-id="c9b51-160">60</span><span class="sxs-lookup"><span data-stu-id="c9b51-160">60</span></span> |
| <span data-ttu-id="c9b51-161">发送到对话</span><span class="sxs-lookup"><span data-stu-id="c9b51-161">Send to conversation</span></span> | <span data-ttu-id="c9b51-162">3600</span><span class="sxs-lookup"><span data-stu-id="c9b51-162">3600</span></span> | <span data-ttu-id="c9b51-163">1800</span><span class="sxs-lookup"><span data-stu-id="c9b51-163">1800</span></span> |
| <span data-ttu-id="c9b51-164">创建对话</span><span class="sxs-lookup"><span data-stu-id="c9b51-164">Create conversation</span></span> | <span data-ttu-id="c9b51-165">1</span><span class="sxs-lookup"><span data-stu-id="c9b51-165">1</span></span> | <span data-ttu-id="c9b51-166">7 </span><span class="sxs-lookup"><span data-stu-id="c9b51-166">7</span></span> |
| <span data-ttu-id="c9b51-167">创建对话</span><span class="sxs-lookup"><span data-stu-id="c9b51-167">Create conversation</span></span> | <span data-ttu-id="c9b51-168">2</span><span class="sxs-lookup"><span data-stu-id="c9b51-168">2</span></span> | <span data-ttu-id="c9b51-169">8 </span><span class="sxs-lookup"><span data-stu-id="c9b51-169">8</span></span> |
| <span data-ttu-id="c9b51-170">创建对话</span><span class="sxs-lookup"><span data-stu-id="c9b51-170">Create conversation</span></span> | <span data-ttu-id="c9b51-171">30</span><span class="sxs-lookup"><span data-stu-id="c9b51-171">30</span></span> | <span data-ttu-id="c9b51-172">60</span><span class="sxs-lookup"><span data-stu-id="c9b51-172">60</span></span> |
| <span data-ttu-id="c9b51-173">创建对话</span><span class="sxs-lookup"><span data-stu-id="c9b51-173">Create conversation</span></span> | <span data-ttu-id="c9b51-174">3600</span><span class="sxs-lookup"><span data-stu-id="c9b51-174">3600</span></span> | <span data-ttu-id="c9b51-175">1800</span><span class="sxs-lookup"><span data-stu-id="c9b51-175">1800</span></span> |
| <span data-ttu-id="c9b51-176">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="c9b51-176">Get conversation members</span></span>| <span data-ttu-id="c9b51-177">1</span><span class="sxs-lookup"><span data-stu-id="c9b51-177">1</span></span> | <span data-ttu-id="c9b51-178">14 </span><span class="sxs-lookup"><span data-stu-id="c9b51-178">14</span></span> |
| <span data-ttu-id="c9b51-179">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="c9b51-179">Get conversation members</span></span>| <span data-ttu-id="c9b51-180">2</span><span class="sxs-lookup"><span data-stu-id="c9b51-180">2</span></span> | <span data-ttu-id="c9b51-181">16 </span><span class="sxs-lookup"><span data-stu-id="c9b51-181">16</span></span> |
| <span data-ttu-id="c9b51-182">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="c9b51-182">Get conversation members</span></span>| <span data-ttu-id="c9b51-183">30</span><span class="sxs-lookup"><span data-stu-id="c9b51-183">30</span></span> | <span data-ttu-id="c9b51-184">120</span><span class="sxs-lookup"><span data-stu-id="c9b51-184">120</span></span> |
| <span data-ttu-id="c9b51-185">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="c9b51-185">Get conversation members</span></span>| <span data-ttu-id="c9b51-186">3600</span><span class="sxs-lookup"><span data-stu-id="c9b51-186">3600</span></span> | <span data-ttu-id="c9b51-187">3600</span><span class="sxs-lookup"><span data-stu-id="c9b51-187">3600</span></span> |
| <span data-ttu-id="c9b51-188">获取对话</span><span class="sxs-lookup"><span data-stu-id="c9b51-188">Get conversations</span></span> | <span data-ttu-id="c9b51-189">1</span><span class="sxs-lookup"><span data-stu-id="c9b51-189">1</span></span> | <span data-ttu-id="c9b51-190">14 </span><span class="sxs-lookup"><span data-stu-id="c9b51-190">14</span></span> |
| <span data-ttu-id="c9b51-191">获取对话</span><span class="sxs-lookup"><span data-stu-id="c9b51-191">Get conversations</span></span> | <span data-ttu-id="c9b51-192">2</span><span class="sxs-lookup"><span data-stu-id="c9b51-192">2</span></span> | <span data-ttu-id="c9b51-193">16 </span><span class="sxs-lookup"><span data-stu-id="c9b51-193">16</span></span> |
| <span data-ttu-id="c9b51-194">获取对话</span><span class="sxs-lookup"><span data-stu-id="c9b51-194">Get conversations</span></span> | <span data-ttu-id="c9b51-195">30</span><span class="sxs-lookup"><span data-stu-id="c9b51-195">30</span></span> | <span data-ttu-id="c9b51-196">120</span><span class="sxs-lookup"><span data-stu-id="c9b51-196">120</span></span> |
| <span data-ttu-id="c9b51-197">获取对话</span><span class="sxs-lookup"><span data-stu-id="c9b51-197">Get conversations</span></span> | <span data-ttu-id="c9b51-198">3600</span><span class="sxs-lookup"><span data-stu-id="c9b51-198">3600</span></span> | <span data-ttu-id="c9b51-199">3600</span><span class="sxs-lookup"><span data-stu-id="c9b51-199">3600</span></span> |

>[!NOTE]
> <span data-ttu-id="c9b51-200">早期版本和 `TeamsInfo.getMembers` API `TeamsInfo.GetMembersAsync` 被弃用。</span><span class="sxs-lookup"><span data-stu-id="c9b51-200">Previous versions of `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs are being deprecated.</span></span> <span data-ttu-id="c9b51-201">它们被限制为每分钟五个请求，并且每个团队最多返回 10，000 个成员。</span><span class="sxs-lookup"><span data-stu-id="c9b51-201">They are throttled to five requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="c9b51-202">若要更新 Bot Framework SDK 和代码以使用最新的分页 API 终结点，请参阅团队和聊天成员的自动程序 [API 更改](../../resources/team-chat-member-api-changes.md)。</span><span class="sxs-lookup"><span data-stu-id="c9b51-202">To update your Bot Framework SDK and the code to use the latest paginated API endpoints, see [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span></span>

<span data-ttu-id="c9b51-203">您还可以使用所有机器人的按线程限制处理速率限制。</span><span class="sxs-lookup"><span data-stu-id="c9b51-203">You can also handle rate limit using the per thread limit for all bots.</span></span>

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="c9b51-204">所有自动程序每线程限制</span><span class="sxs-lookup"><span data-stu-id="c9b51-204">Per thread limit for all bots</span></span>

<span data-ttu-id="c9b51-205">所有机器人的线程限制控制允许所有机器人在单个对话中生成的流量。</span><span class="sxs-lookup"><span data-stu-id="c9b51-205">The per thread limit for all bots controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="c9b51-206">此处的对话是机器人和用户、群聊或团队中的频道之间的一对一对话。</span><span class="sxs-lookup"><span data-stu-id="c9b51-206">A conversation here is 1:1 between bot and user, a group chat, or a channel in a team.</span></span>

<span data-ttu-id="c9b51-207">下表提供了所有自动程序每线程的限制：</span><span class="sxs-lookup"><span data-stu-id="c9b51-207">The following table provides the per thread limit for all bots:</span></span>

| <span data-ttu-id="c9b51-208">方案</span><span class="sxs-lookup"><span data-stu-id="c9b51-208">Scenario</span></span> | <span data-ttu-id="c9b51-209">时间段（以秒表示）</span><span class="sxs-lookup"><span data-stu-id="c9b51-209">Time period in seconds</span></span> | <span data-ttu-id="c9b51-210">允许的最大操作数</span><span class="sxs-lookup"><span data-stu-id="c9b51-210">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c9b51-211">发送到对话</span><span class="sxs-lookup"><span data-stu-id="c9b51-211">Send to conversation</span></span> | <span data-ttu-id="c9b51-212">1</span><span class="sxs-lookup"><span data-stu-id="c9b51-212">1</span></span> | <span data-ttu-id="c9b51-213">14 </span><span class="sxs-lookup"><span data-stu-id="c9b51-213">14</span></span> |
| <span data-ttu-id="c9b51-214">发送到对话</span><span class="sxs-lookup"><span data-stu-id="c9b51-214">Send to conversation</span></span> | <span data-ttu-id="c9b51-215">2</span><span class="sxs-lookup"><span data-stu-id="c9b51-215">2</span></span> | <span data-ttu-id="c9b51-216">16 </span><span class="sxs-lookup"><span data-stu-id="c9b51-216">16</span></span> |
| <span data-ttu-id="c9b51-217">创建对话</span><span class="sxs-lookup"><span data-stu-id="c9b51-217">Create conversation</span></span> | <span data-ttu-id="c9b51-218">1</span><span class="sxs-lookup"><span data-stu-id="c9b51-218">1</span></span> | <span data-ttu-id="c9b51-219">14 </span><span class="sxs-lookup"><span data-stu-id="c9b51-219">14</span></span> |
| <span data-ttu-id="c9b51-220">创建对话</span><span class="sxs-lookup"><span data-stu-id="c9b51-220">Create conversation</span></span> | <span data-ttu-id="c9b51-221">2</span><span class="sxs-lookup"><span data-stu-id="c9b51-221">2</span></span> | <span data-ttu-id="c9b51-222">16 </span><span class="sxs-lookup"><span data-stu-id="c9b51-222">16</span></span> |
| <span data-ttu-id="c9b51-223">创建对话</span><span class="sxs-lookup"><span data-stu-id="c9b51-223">Create conversation</span></span>| <span data-ttu-id="c9b51-224">1</span><span class="sxs-lookup"><span data-stu-id="c9b51-224">1</span></span> | <span data-ttu-id="c9b51-225">14 </span><span class="sxs-lookup"><span data-stu-id="c9b51-225">14</span></span> |
| <span data-ttu-id="c9b51-226">创建对话</span><span class="sxs-lookup"><span data-stu-id="c9b51-226">Create conversation</span></span>| <span data-ttu-id="c9b51-227">2</span><span class="sxs-lookup"><span data-stu-id="c9b51-227">2</span></span> | <span data-ttu-id="c9b51-228">16 </span><span class="sxs-lookup"><span data-stu-id="c9b51-228">16</span></span> |
| <span data-ttu-id="c9b51-229">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="c9b51-229">Get conversation members</span></span>| <span data-ttu-id="c9b51-230">1</span><span class="sxs-lookup"><span data-stu-id="c9b51-230">1</span></span> | <span data-ttu-id="c9b51-231">28</span><span class="sxs-lookup"><span data-stu-id="c9b51-231">28</span></span> |
| <span data-ttu-id="c9b51-232">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="c9b51-232">Get conversation members</span></span>| <span data-ttu-id="c9b51-233">2</span><span class="sxs-lookup"><span data-stu-id="c9b51-233">2</span></span> | <span data-ttu-id="c9b51-234">32</span><span class="sxs-lookup"><span data-stu-id="c9b51-234">32</span></span> |
| <span data-ttu-id="c9b51-235">获取对话</span><span class="sxs-lookup"><span data-stu-id="c9b51-235">Get conversations</span></span> | <span data-ttu-id="c9b51-236">1</span><span class="sxs-lookup"><span data-stu-id="c9b51-236">1</span></span> | <span data-ttu-id="c9b51-237">28</span><span class="sxs-lookup"><span data-stu-id="c9b51-237">28</span></span> |
| <span data-ttu-id="c9b51-238">获取对话</span><span class="sxs-lookup"><span data-stu-id="c9b51-238">Get conversations</span></span> | <span data-ttu-id="c9b51-239">2</span><span class="sxs-lookup"><span data-stu-id="c9b51-239">2</span></span> | <span data-ttu-id="c9b51-240">32</span><span class="sxs-lookup"><span data-stu-id="c9b51-240">32</span></span> |

## <a name="next-step"></a><span data-ttu-id="c9b51-241">后续步骤</span><span class="sxs-lookup"><span data-stu-id="c9b51-241">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c9b51-242">通话和会议智能机器人</span><span class="sxs-lookup"><span data-stu-id="c9b51-242">Calls and meetings bots</span></span>](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

