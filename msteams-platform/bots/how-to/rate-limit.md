---
title: 速率限制
description: Microsoft 团队中的速率限制和最佳做法
keywords: 团队 bot 速率限制
ms.openlocfilehash: 4e9efab539ec7817d259fd6c149c438ba02e3ce5
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673121"
---
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a><span data-ttu-id="80993-104">优化你的机器人： Microsoft 团队中的速率限制和最佳做法</span><span class="sxs-lookup"><span data-stu-id="80993-104">Optimize your bot: rate limiting and best practices in Microsoft Teams</span></span>

<span data-ttu-id="80993-105">通常情况下，您的应用程序应限制它在单个聊天或频道对话中发布的邮件数。</span><span class="sxs-lookup"><span data-stu-id="80993-105">As a general principle, your application should limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="80993-106">这可确保对最终用户不会感到 "垃圾" 的最佳体验。</span><span class="sxs-lookup"><span data-stu-id="80993-106">This ensures an optimal experience that doesn't feel “spammy” to your end users.</span></span>

<span data-ttu-id="80993-107">为了保护 Microsoft 团队及其用户，机器人 Api 对传入请求进行评级。</span><span class="sxs-lookup"><span data-stu-id="80993-107">To protect Microsoft Teams and its users, the bot APIs rate-limit incoming requests.</span></span> <span data-ttu-id="80993-108">跳过此限制的应用程序将`HTTP 429 Too Many Requests`收到错误状态。</span><span class="sxs-lookup"><span data-stu-id="80993-108">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="80993-109">所有请求都服从相同的速率限制策略，包括发送消息、通道枚举和名单读取。</span><span class="sxs-lookup"><span data-stu-id="80993-109">All requests are subject to the same rate-limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="80993-110">由于汇率限制的确切值可能会发生更改，因此建议您的应用程序在 API 返回`HTTP 429 Too Many Requests`时实现适当的回退行为。</span><span class="sxs-lookup"><span data-stu-id="80993-110">Because the exact values of rate limits are subject to change, we recommend your application implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handling-rate-limits"></a><span data-ttu-id="80993-111">处理速率限制</span><span class="sxs-lookup"><span data-stu-id="80993-111">Handling rate limits</span></span>

<span data-ttu-id="80993-112">在颁发机器人生成器 SDK 操作时，您可以处理`Microsoft.Rest.HttpOperationException`和检查状态代码。</span><span class="sxs-lookup"><span data-stu-id="80993-112">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="80993-113">最佳做法</span><span class="sxs-lookup"><span data-stu-id="80993-113">Best practices</span></span>

<span data-ttu-id="80993-114">通常情况下，应采取简单的预防措施来`HTTP 429`避免收到响应。</span><span class="sxs-lookup"><span data-stu-id="80993-114">In general, you should take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="80993-115">例如，避免发出对相同个人或通道对话的多个请求。</span><span class="sxs-lookup"><span data-stu-id="80993-115">For instance, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="80993-116">相反，请考虑批处理 API 请求。</span><span class="sxs-lookup"><span data-stu-id="80993-116">Instead, consider batching the API requests.</span></span>

<span data-ttu-id="80993-117">使用具有随机抖动的指数回退是处理429s 的推荐方法。</span><span class="sxs-lookup"><span data-stu-id="80993-117">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="80993-118">这可确保多个请求不会导致重试冲突。</span><span class="sxs-lookup"><span data-stu-id="80993-118">This ensures that multiple requests don't introduce collisions on retries.</span></span>

## <a name="example-detecting-transient-exceptions"></a><span data-ttu-id="80993-119">示例：检测临时异常</span><span class="sxs-lookup"><span data-stu-id="80993-119">Example: detecting transient exceptions</span></span>

<span data-ttu-id="80993-120">下面是使用通过瞬时故障处理应用程序块的指数回退的示例。</span><span class="sxs-lookup"><span data-stu-id="80993-120">Here is a sample using exponential backoff via the Transient Fault Handling Application Block.</span></span>

<span data-ttu-id="80993-121">您可以使用[临时错误处理库](/previous-versions/msp-n-p/hh680901(v=pandp.50))执行回退和重试。</span><span class="sxs-lookup"><span data-stu-id="80993-121">You can perform backoff and retries using [Transient Fault Handling libraries](/previous-versions/msp-n-p/hh680901(v=pandp.50)).</span></span> <span data-ttu-id="80993-122">有关获取和安装 NuGet 包的指南，请参阅[向解决方案中添加瞬时故障处理应用程序块](/previous-versions/msp-n-p/hh680891(v=pandp.50))</span><span class="sxs-lookup"><span data-stu-id="80993-122">For guidelines on obtaining and installing the NuGet package, see [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/hh680891(v=pandp.50))</span></span>

```csharp
public class BotSdkTransientExceptionDetectionStrategy : ITransientErrorDetectionStrategy
{
    // List of error codes to retry on
    List<int> transientErrorStatusCodes = new List<int>() { 429 };

    public bool IsTransient(Exception ex)
    {
        var httpOperationException = ex as HttpOperationException;
        if (httpOperationException != null)
        {
            return httpOperationException.Response != null &&
                    transientErrorStatusCodes.Contains((int) httpOperationException.Response.StatusCode);
        }

        return false;
    }
}
```

## <a name="example-backoff"></a><span data-ttu-id="80993-123">示例：回退</span><span class="sxs-lookup"><span data-stu-id="80993-123">Example: backoff</span></span>

<span data-ttu-id="80993-124">除了检测速率限制之外，还可以执行指数回退。</span><span class="sxs-lookup"><span data-stu-id="80993-124">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

```csharp
/**
* The first parameter specifies the number of retries before failing the operation.
* The second parameter specifies the minimum and maximum backoff time respectively.
* The last parameter is used to add a randomized  +/- 20% delta to avoid numerous clients retrying simultaneously.
*/
var exponentialBackoffRetryStrategy = new ExponentialBackoff(3, TimeSpan.FromSeconds(2),
                        TimeSpan.FromSeconds(20), TimeSpan.FromSeconds(1));


// Define the Retry Policy
var retryPolicy = new RetryPolicy(new BotSdkTransientExceptionDetectionStrategy(), fixedIntervalRetryStrategy);

//Execute any bot sdk action
await retryPolicy.ExecuteAsync(() => connector.Conversations.ReplyToActivityAsync((Activity)reply)).ConfigureAwait(false);
```

<span data-ttu-id="80993-125">您还可以使用上面`System.Action`介绍的重试策略执行方法执行。</span><span class="sxs-lookup"><span data-stu-id="80993-125">You can also perform a `System.Action` method execution with the retry policy described above.</span></span> <span data-ttu-id="80993-126">引用的库还允许您指定固定间隔或线性回退机制。</span><span class="sxs-lookup"><span data-stu-id="80993-126">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="80993-127">建议将值和策略存储在配置文件中，以便在运行时微调和调整值。</span><span class="sxs-lookup"><span data-stu-id="80993-127">We recommend storing the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="80993-128">有关详细信息，请参阅有关各种重试模式的此便捷指南：[重试模式](/azure/architecture/patterns/retry)。</span><span class="sxs-lookup"><span data-stu-id="80993-128">For more information, check out this handy guide on various retry patterns: [Retry pattern](/azure/architecture/patterns/retry).</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="80993-129">每个 bot 每个线程的限制</span><span class="sxs-lookup"><span data-stu-id="80993-129">Per bot per thread limit</span></span>

>[!NOTE]
><span data-ttu-id="80993-130">服务级别的邮件拆分会导致高于每秒预期的请求数（RPS）。</span><span class="sxs-lookup"><span data-stu-id="80993-130">Message splitting at the service level will result in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="80993-131">如果你担心接近限制，应实施上述回退策略。</span><span class="sxs-lookup"><span data-stu-id="80993-131">If you're concerned about approaching the limits, you should implement the backoff strategy described above.</span></span> <span data-ttu-id="80993-132">下面提供的值仅用于评估。</span><span class="sxs-lookup"><span data-stu-id="80993-132">The values provided below are for estimation only.</span></span>

<span data-ttu-id="80993-133">此限制控制允许 bot 在单个会话中生成的流量。</span><span class="sxs-lookup"><span data-stu-id="80993-133">This limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="80993-134">此处的对话是在 bot 与用户、组聊天或团队中的频道之间的1:1。</span><span class="sxs-lookup"><span data-stu-id="80993-134">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="80993-135">**应用场景**</span><span class="sxs-lookup"><span data-stu-id="80993-135">**Scenario**</span></span> | <span data-ttu-id="80993-136">**时间段（秒）**</span><span class="sxs-lookup"><span data-stu-id="80993-136">**Time-period (sec)**</span></span> | <span data-ttu-id="80993-137">**允许的最大操作**</span><span class="sxs-lookup"><span data-stu-id="80993-137">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="80993-138">NewMessage</span><span class="sxs-lookup"><span data-stu-id="80993-138">NewMessage</span></span> | <span data-ttu-id="80993-139">1 </span><span class="sxs-lookup"><span data-stu-id="80993-139">1</span></span> | <span data-ttu-id="80993-140">7 </span><span class="sxs-lookup"><span data-stu-id="80993-140">7</span></span> |
| <span data-ttu-id="80993-141">NewMessage</span><span class="sxs-lookup"><span data-stu-id="80993-141">NewMessage</span></span> | <span data-ttu-id="80993-142">2 </span><span class="sxs-lookup"><span data-stu-id="80993-142">2</span></span> | <span data-ttu-id="80993-143">8 </span><span class="sxs-lookup"><span data-stu-id="80993-143">8</span></span> |
| <span data-ttu-id="80993-144">NewMessage</span><span class="sxs-lookup"><span data-stu-id="80993-144">NewMessage</span></span> | <span data-ttu-id="80993-145">30</span><span class="sxs-lookup"><span data-stu-id="80993-145">30</span></span> | <span data-ttu-id="80993-146">60</span><span class="sxs-lookup"><span data-stu-id="80993-146">60</span></span> |
| <span data-ttu-id="80993-147">NewMessage</span><span class="sxs-lookup"><span data-stu-id="80993-147">NewMessage</span></span> | <span data-ttu-id="80993-148">3600</span><span class="sxs-lookup"><span data-stu-id="80993-148">3600</span></span> | <span data-ttu-id="80993-149">1800</span><span class="sxs-lookup"><span data-stu-id="80993-149">1800</span></span> |
| <span data-ttu-id="80993-150">UpdateMessage</span><span class="sxs-lookup"><span data-stu-id="80993-150">UpdateMessage</span></span> | <span data-ttu-id="80993-151">1 </span><span class="sxs-lookup"><span data-stu-id="80993-151">1</span></span> | <span data-ttu-id="80993-152">7 </span><span class="sxs-lookup"><span data-stu-id="80993-152">7</span></span> |
| <span data-ttu-id="80993-153">UpdateMessage</span><span class="sxs-lookup"><span data-stu-id="80993-153">UpdateMessage</span></span> | <span data-ttu-id="80993-154">2 </span><span class="sxs-lookup"><span data-stu-id="80993-154">2</span></span> | <span data-ttu-id="80993-155">8 </span><span class="sxs-lookup"><span data-stu-id="80993-155">8</span></span> |
| <span data-ttu-id="80993-156">UpdateMessage</span><span class="sxs-lookup"><span data-stu-id="80993-156">UpdateMessage</span></span> | <span data-ttu-id="80993-157">30</span><span class="sxs-lookup"><span data-stu-id="80993-157">30</span></span> | <span data-ttu-id="80993-158">60</span><span class="sxs-lookup"><span data-stu-id="80993-158">60</span></span> |
| <span data-ttu-id="80993-159">UpdateMessage</span><span class="sxs-lookup"><span data-stu-id="80993-159">UpdateMessage</span></span> | <span data-ttu-id="80993-160">3600</span><span class="sxs-lookup"><span data-stu-id="80993-160">3600</span></span> | <span data-ttu-id="80993-161">1800</span><span class="sxs-lookup"><span data-stu-id="80993-161">1800</span></span> |
| <span data-ttu-id="80993-162">NewThread</span><span class="sxs-lookup"><span data-stu-id="80993-162">NewThread</span></span> | <span data-ttu-id="80993-163">1 </span><span class="sxs-lookup"><span data-stu-id="80993-163">1</span></span> | <span data-ttu-id="80993-164">7 </span><span class="sxs-lookup"><span data-stu-id="80993-164">7</span></span> |
| <span data-ttu-id="80993-165">NewThread</span><span class="sxs-lookup"><span data-stu-id="80993-165">NewThread</span></span> | <span data-ttu-id="80993-166">2 </span><span class="sxs-lookup"><span data-stu-id="80993-166">2</span></span> | <span data-ttu-id="80993-167">8 </span><span class="sxs-lookup"><span data-stu-id="80993-167">8</span></span> |
| <span data-ttu-id="80993-168">NewThread</span><span class="sxs-lookup"><span data-stu-id="80993-168">NewThread</span></span> | <span data-ttu-id="80993-169">30</span><span class="sxs-lookup"><span data-stu-id="80993-169">30</span></span> | <span data-ttu-id="80993-170">60</span><span class="sxs-lookup"><span data-stu-id="80993-170">60</span></span> |
| <span data-ttu-id="80993-171">NewThread</span><span class="sxs-lookup"><span data-stu-id="80993-171">NewThread</span></span> | <span data-ttu-id="80993-172">3600</span><span class="sxs-lookup"><span data-stu-id="80993-172">3600</span></span> | <span data-ttu-id="80993-173">1800</span><span class="sxs-lookup"><span data-stu-id="80993-173">1800</span></span> |
| <span data-ttu-id="80993-174">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="80993-174">GetThreadMembers</span></span> | <span data-ttu-id="80993-175">1 </span><span class="sxs-lookup"><span data-stu-id="80993-175">1</span></span> | <span data-ttu-id="80993-176">14 </span><span class="sxs-lookup"><span data-stu-id="80993-176">14</span></span> |
| <span data-ttu-id="80993-177">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="80993-177">GetThreadMembers</span></span> | <span data-ttu-id="80993-178">2 </span><span class="sxs-lookup"><span data-stu-id="80993-178">2</span></span> | <span data-ttu-id="80993-179">16 </span><span class="sxs-lookup"><span data-stu-id="80993-179">16</span></span> |
| <span data-ttu-id="80993-180">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="80993-180">GetThreadMembers</span></span> | <span data-ttu-id="80993-181">30</span><span class="sxs-lookup"><span data-stu-id="80993-181">30</span></span> | <span data-ttu-id="80993-182">120</span><span class="sxs-lookup"><span data-stu-id="80993-182">120</span></span> |
| <span data-ttu-id="80993-183">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="80993-183">GetThreadMembers</span></span> | <span data-ttu-id="80993-184">3600</span><span class="sxs-lookup"><span data-stu-id="80993-184">3600</span></span> | <span data-ttu-id="80993-185">3600</span><span class="sxs-lookup"><span data-stu-id="80993-185">3600</span></span> |
| <span data-ttu-id="80993-186">GetThread</span><span class="sxs-lookup"><span data-stu-id="80993-186">GetThread</span></span> | <span data-ttu-id="80993-187">1 </span><span class="sxs-lookup"><span data-stu-id="80993-187">1</span></span> | <span data-ttu-id="80993-188">14 </span><span class="sxs-lookup"><span data-stu-id="80993-188">14</span></span> |
| <span data-ttu-id="80993-189">GetThread</span><span class="sxs-lookup"><span data-stu-id="80993-189">GetThread</span></span> | <span data-ttu-id="80993-190">2 </span><span class="sxs-lookup"><span data-stu-id="80993-190">2</span></span> | <span data-ttu-id="80993-191">16 </span><span class="sxs-lookup"><span data-stu-id="80993-191">16</span></span> |
| <span data-ttu-id="80993-192">GetThread</span><span class="sxs-lookup"><span data-stu-id="80993-192">GetThread</span></span> | <span data-ttu-id="80993-193">30</span><span class="sxs-lookup"><span data-stu-id="80993-193">30</span></span> | <span data-ttu-id="80993-194">120</span><span class="sxs-lookup"><span data-stu-id="80993-194">120</span></span> |
| <span data-ttu-id="80993-195">GetThread</span><span class="sxs-lookup"><span data-stu-id="80993-195">GetThread</span></span> | <span data-ttu-id="80993-196">3600</span><span class="sxs-lookup"><span data-stu-id="80993-196">3600</span></span> | <span data-ttu-id="80993-197">3600</span><span class="sxs-lookup"><span data-stu-id="80993-197">3600</span></span> |

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="80993-198">每个线程对所有 bot 的限制</span><span class="sxs-lookup"><span data-stu-id="80993-198">Per thread limit for all bots</span></span>

<span data-ttu-id="80993-199">此限制控制允许所有 bot 在单个对话中生成的流量。</span><span class="sxs-lookup"><span data-stu-id="80993-199">This limit controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="80993-200">此处的对话是在 bot 与用户、组聊天或团队中的频道之间的1:1。</span><span class="sxs-lookup"><span data-stu-id="80993-200">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="80993-201">**应用场景**</span><span class="sxs-lookup"><span data-stu-id="80993-201">**Scenario**</span></span> | <span data-ttu-id="80993-202">**时间段（秒）**</span><span class="sxs-lookup"><span data-stu-id="80993-202">**Time-period (sec)**</span></span> | <span data-ttu-id="80993-203">**允许的最大操作**</span><span class="sxs-lookup"><span data-stu-id="80993-203">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="80993-204">NewMessage</span><span class="sxs-lookup"><span data-stu-id="80993-204">NewMessage</span></span> | <span data-ttu-id="80993-205">1 </span><span class="sxs-lookup"><span data-stu-id="80993-205">1</span></span> | <span data-ttu-id="80993-206">14 </span><span class="sxs-lookup"><span data-stu-id="80993-206">14</span></span> |
| <span data-ttu-id="80993-207">NewMessage</span><span class="sxs-lookup"><span data-stu-id="80993-207">NewMessage</span></span> | <span data-ttu-id="80993-208">2 </span><span class="sxs-lookup"><span data-stu-id="80993-208">2</span></span> | <span data-ttu-id="80993-209">16 </span><span class="sxs-lookup"><span data-stu-id="80993-209">16</span></span> |
| <span data-ttu-id="80993-210">UpdateMessage</span><span class="sxs-lookup"><span data-stu-id="80993-210">UpdateMessage</span></span> | <span data-ttu-id="80993-211">1 </span><span class="sxs-lookup"><span data-stu-id="80993-211">1</span></span> | <span data-ttu-id="80993-212">14 </span><span class="sxs-lookup"><span data-stu-id="80993-212">14</span></span> |
| <span data-ttu-id="80993-213">UpdateMessage</span><span class="sxs-lookup"><span data-stu-id="80993-213">UpdateMessage</span></span> | <span data-ttu-id="80993-214">2 </span><span class="sxs-lookup"><span data-stu-id="80993-214">2</span></span> | <span data-ttu-id="80993-215">16 </span><span class="sxs-lookup"><span data-stu-id="80993-215">16</span></span> |
| <span data-ttu-id="80993-216">NewThread</span><span class="sxs-lookup"><span data-stu-id="80993-216">NewThread</span></span> | <span data-ttu-id="80993-217">1 </span><span class="sxs-lookup"><span data-stu-id="80993-217">1</span></span> | <span data-ttu-id="80993-218">14 </span><span class="sxs-lookup"><span data-stu-id="80993-218">14</span></span> |
| <span data-ttu-id="80993-219">NewThread</span><span class="sxs-lookup"><span data-stu-id="80993-219">NewThread</span></span> | <span data-ttu-id="80993-220">2 </span><span class="sxs-lookup"><span data-stu-id="80993-220">2</span></span> | <span data-ttu-id="80993-221">16 </span><span class="sxs-lookup"><span data-stu-id="80993-221">16</span></span> |
| <span data-ttu-id="80993-222">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="80993-222">GetThreadMembers</span></span> | <span data-ttu-id="80993-223">1 </span><span class="sxs-lookup"><span data-stu-id="80993-223">1</span></span> | <span data-ttu-id="80993-224">28</span><span class="sxs-lookup"><span data-stu-id="80993-224">28</span></span> |
| <span data-ttu-id="80993-225">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="80993-225">GetThreadMembers</span></span> | <span data-ttu-id="80993-226">2 </span><span class="sxs-lookup"><span data-stu-id="80993-226">2</span></span> | <span data-ttu-id="80993-227">32</span><span class="sxs-lookup"><span data-stu-id="80993-227">32</span></span> |
| <span data-ttu-id="80993-228">GetThread</span><span class="sxs-lookup"><span data-stu-id="80993-228">GetThread</span></span> | <span data-ttu-id="80993-229">1 </span><span class="sxs-lookup"><span data-stu-id="80993-229">1</span></span> | <span data-ttu-id="80993-230">28</span><span class="sxs-lookup"><span data-stu-id="80993-230">28</span></span> |
| <span data-ttu-id="80993-231">GetThread</span><span class="sxs-lookup"><span data-stu-id="80993-231">GetThread</span></span> | <span data-ttu-id="80993-232">2 </span><span class="sxs-lookup"><span data-stu-id="80993-232">2</span></span> | <span data-ttu-id="80993-233">32</span><span class="sxs-lookup"><span data-stu-id="80993-233">32</span></span> |

## <a name="bot-per-data-center-limit"></a><span data-ttu-id="80993-234">每个数据中心的 Bot 限制</span><span class="sxs-lookup"><span data-stu-id="80993-234">Bot per data center limit</span></span>

<span data-ttu-id="80993-235">此限制控制允许机器人在数据中心中的所有线程（跨多个租户）生成的流量。</span><span class="sxs-lookup"><span data-stu-id="80993-235">This limit controls the traffic that a bot is allowed to generate across all threads in a data center (across multiple tenants).</span></span>

|<span data-ttu-id="80993-236">**时间段（秒）**</span><span class="sxs-lookup"><span data-stu-id="80993-236">**Time-period (sec)**</span></span> | <span data-ttu-id="80993-237">**允许的最大操作**</span><span class="sxs-lookup"><span data-stu-id="80993-237">**Max allowed operations**</span></span> |
| --- | --- |
| <span data-ttu-id="80993-238">1 </span><span class="sxs-lookup"><span data-stu-id="80993-238">1</span></span> | <span data-ttu-id="80993-239">20</span><span class="sxs-lookup"><span data-stu-id="80993-239">20</span></span> |
| <span data-ttu-id="80993-240">1800</span><span class="sxs-lookup"><span data-stu-id="80993-240">1800</span></span> | <span data-ttu-id="80993-241">8000</span><span class="sxs-lookup"><span data-stu-id="80993-241">8000</span></span> |
| <span data-ttu-id="80993-242">3600</span><span class="sxs-lookup"><span data-stu-id="80993-242">3600</span></span> | <span data-ttu-id="80993-243">15000</span><span class="sxs-lookup"><span data-stu-id="80993-243">15000</span></span> |
