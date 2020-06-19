---
title: 速率限制
description: Microsoft 团队中的速率限制和最佳做法
keywords: 团队 bot 速率限制
ms.openlocfilehash: 9b244053d42aaddaf48c798e401438b614b0e1bd
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "44801124"
---
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a><span data-ttu-id="26598-104">优化你的机器人： Microsoft 团队中的速率限制和最佳做法</span><span class="sxs-lookup"><span data-stu-id="26598-104">Optimize your bot: rate limiting and best practices in Microsoft Teams</span></span>

<span data-ttu-id="26598-105">通常情况下，您的应用程序应限制它在单个聊天或频道对话中发布的邮件数。</span><span class="sxs-lookup"><span data-stu-id="26598-105">As a general principle, your application should limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="26598-106">这可确保对最终用户不会感到 "垃圾" 的最佳体验。</span><span class="sxs-lookup"><span data-stu-id="26598-106">This ensures an optimal experience that doesn't feel “spammy” to your end users.</span></span>

<span data-ttu-id="26598-107">为了保护 Microsoft 团队及其用户，机器人 Api 对传入请求进行评级。</span><span class="sxs-lookup"><span data-stu-id="26598-107">To protect Microsoft Teams and its users, the bot APIs rate-limit incoming requests.</span></span> <span data-ttu-id="26598-108">跳过此限制的应用程序将收到 `HTTP 429 Too Many Requests` 错误状态。</span><span class="sxs-lookup"><span data-stu-id="26598-108">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="26598-109">所有请求都服从相同的速率限制策略，包括发送消息、通道枚举和名单读取。</span><span class="sxs-lookup"><span data-stu-id="26598-109">All requests are subject to the same rate-limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="26598-110">由于汇率限制的确切值可能会发生更改，因此建议您的应用程序在 API 返回时实现适当的回退行为 `HTTP 429 Too Many Requests` 。</span><span class="sxs-lookup"><span data-stu-id="26598-110">Because the exact values of rate limits are subject to change, we recommend your application implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handling-rate-limits"></a><span data-ttu-id="26598-111">处理速率限制</span><span class="sxs-lookup"><span data-stu-id="26598-111">Handling rate limits</span></span>

<span data-ttu-id="26598-112">在颁发机器人生成器 SDK 操作时，您可以处理 `Microsoft.Rest.HttpOperationException` 和检查状态代码。</span><span class="sxs-lookup"><span data-stu-id="26598-112">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="26598-113">最佳做法</span><span class="sxs-lookup"><span data-stu-id="26598-113">Best practices</span></span>

<span data-ttu-id="26598-114">通常情况下，应采取简单的预防措施来避免收到 `HTTP 429` 响应。</span><span class="sxs-lookup"><span data-stu-id="26598-114">In general, you should take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="26598-115">例如，避免发出对相同个人或通道对话的多个请求。</span><span class="sxs-lookup"><span data-stu-id="26598-115">For instance, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="26598-116">相反，请考虑批处理 API 请求。</span><span class="sxs-lookup"><span data-stu-id="26598-116">Instead, consider batching the API requests.</span></span>

<span data-ttu-id="26598-117">使用具有随机抖动的指数回退是处理429s 的推荐方法。</span><span class="sxs-lookup"><span data-stu-id="26598-117">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="26598-118">这可确保多个请求不会导致重试冲突。</span><span class="sxs-lookup"><span data-stu-id="26598-118">This ensures that multiple requests don't introduce collisions on retries.</span></span>

## <a name="example-detecting-transient-exceptions"></a><span data-ttu-id="26598-119">示例：检测临时异常</span><span class="sxs-lookup"><span data-stu-id="26598-119">Example: detecting transient exceptions</span></span>

<span data-ttu-id="26598-120">下面是使用通过瞬时故障处理应用程序块的指数回退的示例。</span><span class="sxs-lookup"><span data-stu-id="26598-120">Here is a sample using exponential backoff via the Transient Fault Handling Application Block.</span></span>

<span data-ttu-id="26598-121">您可以使用[暂时性的故障处理](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)执行回退和重试。</span><span class="sxs-lookup"><span data-stu-id="26598-121">You can perform backoff and retries using [Transient Fault Handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="26598-122">有关获取和安装 NuGet 包的指南，请参阅[将临时错误处理应用程序块添加到解决方案](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)中）。</span><span class="sxs-lookup"><span data-stu-id="26598-122">For guidelines on obtaining and installing the NuGet package, see [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)).</span></span> <span data-ttu-id="26598-123">*另请参阅*[暂时性故障处理](/azure/architecture/best-practices/transient-faults)。</span><span class="sxs-lookup"><span data-stu-id="26598-123">*See also* [Transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

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

## <a name="example-backoff"></a><span data-ttu-id="26598-124">示例：回退</span><span class="sxs-lookup"><span data-stu-id="26598-124">Example: backoff</span></span>

<span data-ttu-id="26598-125">除了检测速率限制之外，还可以执行指数回退。</span><span class="sxs-lookup"><span data-stu-id="26598-125">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

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

<span data-ttu-id="26598-126">您还可以 `System.Action` 使用上面介绍的重试策略执行方法执行。</span><span class="sxs-lookup"><span data-stu-id="26598-126">You can also perform a `System.Action` method execution with the retry policy described above.</span></span> <span data-ttu-id="26598-127">引用的库还允许您指定固定间隔或线性回退机制。</span><span class="sxs-lookup"><span data-stu-id="26598-127">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="26598-128">建议将值和策略存储在配置文件中，以便在运行时微调和调整值。</span><span class="sxs-lookup"><span data-stu-id="26598-128">We recommend storing the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="26598-129">有关详细信息，请参阅有关各种重试模式的此便捷指南：[重试模式](/azure/architecture/patterns/retry)。</span><span class="sxs-lookup"><span data-stu-id="26598-129">For more information, check out this handy guide on various retry patterns: [Retry pattern](/azure/architecture/patterns/retry).</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="26598-130">每个 bot 每个线程的限制</span><span class="sxs-lookup"><span data-stu-id="26598-130">Per bot per thread limit</span></span>

>[!NOTE]
><span data-ttu-id="26598-131">服务级别的邮件拆分会导致高于每秒预期的请求数（RPS）。</span><span class="sxs-lookup"><span data-stu-id="26598-131">Message splitting at the service level will result in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="26598-132">如果你担心接近限制，应实施上述回退策略。</span><span class="sxs-lookup"><span data-stu-id="26598-132">If you're concerned about approaching the limits, you should implement the backoff strategy described above.</span></span> <span data-ttu-id="26598-133">下面提供的值仅用于评估。</span><span class="sxs-lookup"><span data-stu-id="26598-133">The values provided below are for estimation only.</span></span>

<span data-ttu-id="26598-134">此限制控制允许 bot 在单个会话中生成的流量。</span><span class="sxs-lookup"><span data-stu-id="26598-134">This limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="26598-135">此处的对话是在 bot 与用户、组聊天或团队中的频道之间的1:1。</span><span class="sxs-lookup"><span data-stu-id="26598-135">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="26598-136">**应用场景**</span><span class="sxs-lookup"><span data-stu-id="26598-136">**Scenario**</span></span> | <span data-ttu-id="26598-137">**时间段（秒）**</span><span class="sxs-lookup"><span data-stu-id="26598-137">**Time-period (sec)**</span></span> | <span data-ttu-id="26598-138">**允许的最大操作**</span><span class="sxs-lookup"><span data-stu-id="26598-138">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="26598-139">发送到对话</span><span class="sxs-lookup"><span data-stu-id="26598-139">Send to Conversation</span></span> | <span data-ttu-id="26598-140">1 </span><span class="sxs-lookup"><span data-stu-id="26598-140">1</span></span> | <span data-ttu-id="26598-141">7 </span><span class="sxs-lookup"><span data-stu-id="26598-141">7</span></span> |
| <span data-ttu-id="26598-142">发送到对话</span><span class="sxs-lookup"><span data-stu-id="26598-142">Send to Conversation</span></span> | <span data-ttu-id="26598-143">双面</span><span class="sxs-lookup"><span data-stu-id="26598-143">2</span></span> | <span data-ttu-id="26598-144">8 </span><span class="sxs-lookup"><span data-stu-id="26598-144">8</span></span> |
| <span data-ttu-id="26598-145">发送到对话</span><span class="sxs-lookup"><span data-stu-id="26598-145">Send to Conversation</span></span> | <span data-ttu-id="26598-146">30</span><span class="sxs-lookup"><span data-stu-id="26598-146">30</span></span> | <span data-ttu-id="26598-147">60</span><span class="sxs-lookup"><span data-stu-id="26598-147">60</span></span> |
| <span data-ttu-id="26598-148">发送到对话</span><span class="sxs-lookup"><span data-stu-id="26598-148">Send to Conversation</span></span> | <span data-ttu-id="26598-149">3600</span><span class="sxs-lookup"><span data-stu-id="26598-149">3600</span></span> | <span data-ttu-id="26598-150">1800</span><span class="sxs-lookup"><span data-stu-id="26598-150">1800</span></span> |
| <span data-ttu-id="26598-151">创建对话</span><span class="sxs-lookup"><span data-stu-id="26598-151">Create Conversation</span></span> | <span data-ttu-id="26598-152">1 </span><span class="sxs-lookup"><span data-stu-id="26598-152">1</span></span> | <span data-ttu-id="26598-153">7 </span><span class="sxs-lookup"><span data-stu-id="26598-153">7</span></span> |
| <span data-ttu-id="26598-154">创建对话</span><span class="sxs-lookup"><span data-stu-id="26598-154">Create Conversation</span></span> | <span data-ttu-id="26598-155">双面</span><span class="sxs-lookup"><span data-stu-id="26598-155">2</span></span> | <span data-ttu-id="26598-156">8 </span><span class="sxs-lookup"><span data-stu-id="26598-156">8</span></span> |
| <span data-ttu-id="26598-157">创建对话</span><span class="sxs-lookup"><span data-stu-id="26598-157">Create Conversation</span></span> | <span data-ttu-id="26598-158">30</span><span class="sxs-lookup"><span data-stu-id="26598-158">30</span></span> | <span data-ttu-id="26598-159">60</span><span class="sxs-lookup"><span data-stu-id="26598-159">60</span></span> |
| <span data-ttu-id="26598-160">创建对话</span><span class="sxs-lookup"><span data-stu-id="26598-160">Create Conversation</span></span> | <span data-ttu-id="26598-161">3600</span><span class="sxs-lookup"><span data-stu-id="26598-161">3600</span></span> | <span data-ttu-id="26598-162">1800</span><span class="sxs-lookup"><span data-stu-id="26598-162">1800</span></span> |
| <span data-ttu-id="26598-163">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="26598-163">Get Conversation Members</span></span>| <span data-ttu-id="26598-164">1 </span><span class="sxs-lookup"><span data-stu-id="26598-164">1</span></span> | <span data-ttu-id="26598-165">14 </span><span class="sxs-lookup"><span data-stu-id="26598-165">14</span></span> |
| <span data-ttu-id="26598-166">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="26598-166">Get Conversation Members</span></span>| <span data-ttu-id="26598-167">双面</span><span class="sxs-lookup"><span data-stu-id="26598-167">2</span></span> | <span data-ttu-id="26598-168">16 </span><span class="sxs-lookup"><span data-stu-id="26598-168">16</span></span> |
| <span data-ttu-id="26598-169">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="26598-169">Get Conversation Members</span></span>| <span data-ttu-id="26598-170">30</span><span class="sxs-lookup"><span data-stu-id="26598-170">30</span></span> | <span data-ttu-id="26598-171">120</span><span class="sxs-lookup"><span data-stu-id="26598-171">120</span></span> |
| <span data-ttu-id="26598-172">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="26598-172">Get Conversation Members</span></span>| <span data-ttu-id="26598-173">3600</span><span class="sxs-lookup"><span data-stu-id="26598-173">3600</span></span> | <span data-ttu-id="26598-174">3600</span><span class="sxs-lookup"><span data-stu-id="26598-174">3600</span></span> |
| <span data-ttu-id="26598-175">获取对话</span><span class="sxs-lookup"><span data-stu-id="26598-175">Get Conversations</span></span> | <span data-ttu-id="26598-176">1 </span><span class="sxs-lookup"><span data-stu-id="26598-176">1</span></span> | <span data-ttu-id="26598-177">14 </span><span class="sxs-lookup"><span data-stu-id="26598-177">14</span></span> |
| <span data-ttu-id="26598-178">获取对话</span><span class="sxs-lookup"><span data-stu-id="26598-178">Get Conversations</span></span> | <span data-ttu-id="26598-179">双面</span><span class="sxs-lookup"><span data-stu-id="26598-179">2</span></span> | <span data-ttu-id="26598-180">16 </span><span class="sxs-lookup"><span data-stu-id="26598-180">16</span></span> |
| <span data-ttu-id="26598-181">获取对话</span><span class="sxs-lookup"><span data-stu-id="26598-181">Get Conversations</span></span> | <span data-ttu-id="26598-182">30</span><span class="sxs-lookup"><span data-stu-id="26598-182">30</span></span> | <span data-ttu-id="26598-183">120</span><span class="sxs-lookup"><span data-stu-id="26598-183">120</span></span> |
| <span data-ttu-id="26598-184">获取对话</span><span class="sxs-lookup"><span data-stu-id="26598-184">Get Conversations</span></span> | <span data-ttu-id="26598-185">3600</span><span class="sxs-lookup"><span data-stu-id="26598-185">3600</span></span> | <span data-ttu-id="26598-186">3600</span><span class="sxs-lookup"><span data-stu-id="26598-186">3600</span></span> |

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="26598-187">每个线程对所有 bot 的限制</span><span class="sxs-lookup"><span data-stu-id="26598-187">Per thread limit for all bots</span></span>

<span data-ttu-id="26598-188">此限制控制允许所有 bot 在单个对话中生成的流量。</span><span class="sxs-lookup"><span data-stu-id="26598-188">This limit controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="26598-189">此处的对话是在 bot 与用户、组聊天或团队中的频道之间的1:1。</span><span class="sxs-lookup"><span data-stu-id="26598-189">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="26598-190">**应用场景**</span><span class="sxs-lookup"><span data-stu-id="26598-190">**Scenario**</span></span> | <span data-ttu-id="26598-191">**时间段（秒）**</span><span class="sxs-lookup"><span data-stu-id="26598-191">**Time-period (sec)**</span></span> | <span data-ttu-id="26598-192">**允许的最大操作**</span><span class="sxs-lookup"><span data-stu-id="26598-192">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="26598-193">发送到对话</span><span class="sxs-lookup"><span data-stu-id="26598-193">Send to Conversation</span></span> | <span data-ttu-id="26598-194">1 </span><span class="sxs-lookup"><span data-stu-id="26598-194">1</span></span> | <span data-ttu-id="26598-195">14 </span><span class="sxs-lookup"><span data-stu-id="26598-195">14</span></span> |
| <span data-ttu-id="26598-196">发送到对话</span><span class="sxs-lookup"><span data-stu-id="26598-196">Send to Conversation</span></span> | <span data-ttu-id="26598-197">双面</span><span class="sxs-lookup"><span data-stu-id="26598-197">2</span></span> | <span data-ttu-id="26598-198">16 </span><span class="sxs-lookup"><span data-stu-id="26598-198">16</span></span> |
| <span data-ttu-id="26598-199">创建对话</span><span class="sxs-lookup"><span data-stu-id="26598-199">Create Conversation</span></span> | <span data-ttu-id="26598-200">1 </span><span class="sxs-lookup"><span data-stu-id="26598-200">1</span></span> | <span data-ttu-id="26598-201">14 </span><span class="sxs-lookup"><span data-stu-id="26598-201">14</span></span> |
| <span data-ttu-id="26598-202">创建对话</span><span class="sxs-lookup"><span data-stu-id="26598-202">Create Conversation</span></span> | <span data-ttu-id="26598-203">双面</span><span class="sxs-lookup"><span data-stu-id="26598-203">2</span></span> | <span data-ttu-id="26598-204">16 </span><span class="sxs-lookup"><span data-stu-id="26598-204">16</span></span> |
| <span data-ttu-id="26598-205">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="26598-205">CreateConversation</span></span>| <span data-ttu-id="26598-206">1 </span><span class="sxs-lookup"><span data-stu-id="26598-206">1</span></span> | <span data-ttu-id="26598-207">14 </span><span class="sxs-lookup"><span data-stu-id="26598-207">14</span></span> |
| <span data-ttu-id="26598-208">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="26598-208">CreateConversation</span></span>| <span data-ttu-id="26598-209">双面</span><span class="sxs-lookup"><span data-stu-id="26598-209">2</span></span> | <span data-ttu-id="26598-210">16 </span><span class="sxs-lookup"><span data-stu-id="26598-210">16</span></span> |
| <span data-ttu-id="26598-211">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="26598-211">Get Conversation Members</span></span>| <span data-ttu-id="26598-212">1 </span><span class="sxs-lookup"><span data-stu-id="26598-212">1</span></span> | <span data-ttu-id="26598-213">28</span><span class="sxs-lookup"><span data-stu-id="26598-213">28</span></span> |
| <span data-ttu-id="26598-214">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="26598-214">Get Conversation Members</span></span>| <span data-ttu-id="26598-215">双面</span><span class="sxs-lookup"><span data-stu-id="26598-215">2</span></span> | <span data-ttu-id="26598-216">32</span><span class="sxs-lookup"><span data-stu-id="26598-216">32</span></span> |
| <span data-ttu-id="26598-217">获取对话</span><span class="sxs-lookup"><span data-stu-id="26598-217">Get Conversations</span></span> | <span data-ttu-id="26598-218">1 </span><span class="sxs-lookup"><span data-stu-id="26598-218">1</span></span> | <span data-ttu-id="26598-219">28</span><span class="sxs-lookup"><span data-stu-id="26598-219">28</span></span> |
| <span data-ttu-id="26598-220">获取对话</span><span class="sxs-lookup"><span data-stu-id="26598-220">Get Conversations</span></span> | <span data-ttu-id="26598-221">双面</span><span class="sxs-lookup"><span data-stu-id="26598-221">2</span></span> | <span data-ttu-id="26598-222">32</span><span class="sxs-lookup"><span data-stu-id="26598-222">32</span></span> |

## <a name="bot-per-data-center-limit"></a><span data-ttu-id="26598-223">每个数据中心的 Bot 限制</span><span class="sxs-lookup"><span data-stu-id="26598-223">Bot per data center limit</span></span>

<span data-ttu-id="26598-224">此限制控制允许机器人在数据中心中的所有线程（跨多个租户）生成的流量。</span><span class="sxs-lookup"><span data-stu-id="26598-224">This limit controls the traffic that a bot is allowed to generate across all threads in a data center (across multiple tenants).</span></span>

|<span data-ttu-id="26598-225">**时间段（秒）**</span><span class="sxs-lookup"><span data-stu-id="26598-225">**Time-period (sec)**</span></span> | <span data-ttu-id="26598-226">**允许的最大操作**</span><span class="sxs-lookup"><span data-stu-id="26598-226">**Max allowed operations**</span></span> |
| --- | --- |
| <span data-ttu-id="26598-227">1 </span><span class="sxs-lookup"><span data-stu-id="26598-227">1</span></span> | <span data-ttu-id="26598-228">20</span><span class="sxs-lookup"><span data-stu-id="26598-228">20</span></span> |
| <span data-ttu-id="26598-229">1800</span><span class="sxs-lookup"><span data-stu-id="26598-229">1800</span></span> | <span data-ttu-id="26598-230">8000</span><span class="sxs-lookup"><span data-stu-id="26598-230">8000</span></span> |
| <span data-ttu-id="26598-231">3600</span><span class="sxs-lookup"><span data-stu-id="26598-231">3600</span></span> | <span data-ttu-id="26598-232">15000</span><span class="sxs-lookup"><span data-stu-id="26598-232">15000</span></span> |
