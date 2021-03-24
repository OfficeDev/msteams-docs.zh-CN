---
title: 速率限制
description: Microsoft Teams 中的速率限制和最佳做法
keywords: teams 机器人速率限制
ms.openlocfilehash: 840737178234bcd6e2da1925b0031083717e2b91
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034679"
---
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a><span data-ttu-id="f2727-104">优化机器人：Microsoft Teams 中的速率限制和最佳做法</span><span class="sxs-lookup"><span data-stu-id="f2727-104">Optimize your bot: rate limiting and best practices in Microsoft Teams</span></span>

<span data-ttu-id="f2727-105">一般来说，您的应用程序应限制向单个聊天或频道对话发布的消息数。</span><span class="sxs-lookup"><span data-stu-id="f2727-105">As a general principle, your application should limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="f2727-106">这可确保最终用户不会感到"spa此操作"的最佳体验。</span><span class="sxs-lookup"><span data-stu-id="f2727-106">This ensures an optimal experience that doesn't feel “spammy” to your end users.</span></span>

<span data-ttu-id="f2727-107">为了保护 Microsoft Teams 及其用户，机器人 API 对传入请求进行速率限制。</span><span class="sxs-lookup"><span data-stu-id="f2727-107">To protect Microsoft Teams and its users, the bot APIs rate-limit incoming requests.</span></span> <span data-ttu-id="f2727-108">超过此限制的应用将收到 `HTTP 429 Too Many Requests` 错误状态。</span><span class="sxs-lookup"><span data-stu-id="f2727-108">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="f2727-109">所有请求都受同一速率限制策略的限制，包括发送邮件、频道枚举和名单提取。</span><span class="sxs-lookup"><span data-stu-id="f2727-109">All requests are subject to the same rate-limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="f2727-110">由于速率限制的确切值可能会更改，因此我们建议你的应用程序在 API 返回 时实现相应的退步行为 `HTTP 429 Too Many Requests` 。</span><span class="sxs-lookup"><span data-stu-id="f2727-110">Because the exact values of rate limits are subject to change, we recommend your application implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handling-rate-limits"></a><span data-ttu-id="f2727-111">处理速率限制</span><span class="sxs-lookup"><span data-stu-id="f2727-111">Handling rate limits</span></span>

<span data-ttu-id="f2727-112">发出自动程序生成器 SDK 操作时，可以处理 `Microsoft.Rest.HttpOperationException` 和检查状态代码。</span><span class="sxs-lookup"><span data-stu-id="f2727-112">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="f2727-113">最佳做法</span><span class="sxs-lookup"><span data-stu-id="f2727-113">Best practices</span></span>

<span data-ttu-id="f2727-114">通常，应该采取简单的预防措施以避免收到 `HTTP 429` 响应。</span><span class="sxs-lookup"><span data-stu-id="f2727-114">In general, you should take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="f2727-115">例如，避免向同一个人对话或频道对话发出多个请求。</span><span class="sxs-lookup"><span data-stu-id="f2727-115">For instance, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="f2727-116">相反，请考虑对 API 请求进行批处理。</span><span class="sxs-lookup"><span data-stu-id="f2727-116">Instead, consider batching the API requests.</span></span>

<span data-ttu-id="f2727-117">建议将指数退约与随机抖动一同处理 429。</span><span class="sxs-lookup"><span data-stu-id="f2727-117">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="f2727-118">这将确保多个请求不会在重试时引入冲突。</span><span class="sxs-lookup"><span data-stu-id="f2727-118">This ensures that multiple requests don't introduce collisions on retries.</span></span>

## <a name="example-detecting-transient-exceptions"></a><span data-ttu-id="f2727-119">示例：检测暂时性异常</span><span class="sxs-lookup"><span data-stu-id="f2727-119">Example: detecting transient exceptions</span></span>

<span data-ttu-id="f2727-120">下面是通过瞬态故障处理应用程序块使用指数退路的示例。</span><span class="sxs-lookup"><span data-stu-id="f2727-120">Here is a sample using exponential backoff via the Transient Fault Handling Application Block.</span></span>

<span data-ttu-id="f2727-121">可以使用瞬态故障处理执行退回 [并重试](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)。</span><span class="sxs-lookup"><span data-stu-id="f2727-121">You can perform backoff and retries using [Transient Fault Handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="f2727-122">有关获取和安装 NuGet 程序包的指南，请参阅 Adding [the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)) 。</span><span class="sxs-lookup"><span data-stu-id="f2727-122">For guidelines on obtaining and installing the NuGet package, see [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)).</span></span> <span data-ttu-id="f2727-123">*另请参阅瞬*[态故障处理](/azure/architecture/best-practices/transient-faults)。</span><span class="sxs-lookup"><span data-stu-id="f2727-123">*See also* [Transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

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

## <a name="example-backoff"></a><span data-ttu-id="f2727-124">示例：退市</span><span class="sxs-lookup"><span data-stu-id="f2727-124">Example: backoff</span></span>

<span data-ttu-id="f2727-125">除了检测速率限制之外，还可以执行指数退市。</span><span class="sxs-lookup"><span data-stu-id="f2727-125">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

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

<span data-ttu-id="f2727-126">您还可以使用上述 `System.Action` 重试策略执行方法。</span><span class="sxs-lookup"><span data-stu-id="f2727-126">You can also perform a `System.Action` method execution with the retry policy described above.</span></span> <span data-ttu-id="f2727-127">引用的库还允许您指定固定间隔或线性退信机制。</span><span class="sxs-lookup"><span data-stu-id="f2727-127">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="f2727-128">我们建议将值和策略存储在配置文件中，以运行时微调和调整值。</span><span class="sxs-lookup"><span data-stu-id="f2727-128">We recommend storing the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="f2727-129">有关详细信息，请查看此有关各种重试模式（重试模式）的 [方便指南](/azure/architecture/patterns/retry)。</span><span class="sxs-lookup"><span data-stu-id="f2727-129">For more information, check out this handy guide on various retry patterns: [Retry pattern](/azure/architecture/patterns/retry).</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="f2727-130">每个机器人每线程限制</span><span class="sxs-lookup"><span data-stu-id="f2727-130">Per bot per thread limit</span></span>

>[!NOTE]
><span data-ttu-id="f2727-131">在服务级别拆分邮件会导致每秒请求数超过 RPS () 。</span><span class="sxs-lookup"><span data-stu-id="f2727-131">Message splitting at the service level will result in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="f2727-132">如果担心接近限制，应实施上述退约策略。</span><span class="sxs-lookup"><span data-stu-id="f2727-132">If you're concerned about approaching the limits, you should implement the backoff strategy described above.</span></span> <span data-ttu-id="f2727-133">下面提供的值仅用于估计。</span><span class="sxs-lookup"><span data-stu-id="f2727-133">The values provided below are for estimation only.</span></span>

<span data-ttu-id="f2727-134">此限制控制允许机器人在单个对话上生成的流量。</span><span class="sxs-lookup"><span data-stu-id="f2727-134">This limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="f2727-135">此处的对话是机器人和用户、群聊或团队中的频道之间的一对一对话。</span><span class="sxs-lookup"><span data-stu-id="f2727-135">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="f2727-136">**应用场景**</span><span class="sxs-lookup"><span data-stu-id="f2727-136">**Scenario**</span></span> | <span data-ttu-id="f2727-137">**时间段（秒）**</span><span class="sxs-lookup"><span data-stu-id="f2727-137">**Time-period (sec)**</span></span> | <span data-ttu-id="f2727-138">**允许的最大操作数**</span><span class="sxs-lookup"><span data-stu-id="f2727-138">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f2727-139">发送到对话</span><span class="sxs-lookup"><span data-stu-id="f2727-139">Send to Conversation</span></span> | <span data-ttu-id="f2727-140">1</span><span class="sxs-lookup"><span data-stu-id="f2727-140">1</span></span> | <span data-ttu-id="f2727-141">7 </span><span class="sxs-lookup"><span data-stu-id="f2727-141">7</span></span> |
| <span data-ttu-id="f2727-142">发送到对话</span><span class="sxs-lookup"><span data-stu-id="f2727-142">Send to Conversation</span></span> | <span data-ttu-id="f2727-143">2</span><span class="sxs-lookup"><span data-stu-id="f2727-143">2</span></span> | <span data-ttu-id="f2727-144">8 </span><span class="sxs-lookup"><span data-stu-id="f2727-144">8</span></span> |
| <span data-ttu-id="f2727-145">发送到对话</span><span class="sxs-lookup"><span data-stu-id="f2727-145">Send to Conversation</span></span> | <span data-ttu-id="f2727-146">30</span><span class="sxs-lookup"><span data-stu-id="f2727-146">30</span></span> | <span data-ttu-id="f2727-147">60</span><span class="sxs-lookup"><span data-stu-id="f2727-147">60</span></span> |
| <span data-ttu-id="f2727-148">发送到对话</span><span class="sxs-lookup"><span data-stu-id="f2727-148">Send to Conversation</span></span> | <span data-ttu-id="f2727-149">3600</span><span class="sxs-lookup"><span data-stu-id="f2727-149">3600</span></span> | <span data-ttu-id="f2727-150">1800</span><span class="sxs-lookup"><span data-stu-id="f2727-150">1800</span></span> |
| <span data-ttu-id="f2727-151">创建对话</span><span class="sxs-lookup"><span data-stu-id="f2727-151">Create Conversation</span></span> | <span data-ttu-id="f2727-152">1</span><span class="sxs-lookup"><span data-stu-id="f2727-152">1</span></span> | <span data-ttu-id="f2727-153">7 </span><span class="sxs-lookup"><span data-stu-id="f2727-153">7</span></span> |
| <span data-ttu-id="f2727-154">创建对话</span><span class="sxs-lookup"><span data-stu-id="f2727-154">Create Conversation</span></span> | <span data-ttu-id="f2727-155">2</span><span class="sxs-lookup"><span data-stu-id="f2727-155">2</span></span> | <span data-ttu-id="f2727-156">8 </span><span class="sxs-lookup"><span data-stu-id="f2727-156">8</span></span> |
| <span data-ttu-id="f2727-157">创建对话</span><span class="sxs-lookup"><span data-stu-id="f2727-157">Create Conversation</span></span> | <span data-ttu-id="f2727-158">30</span><span class="sxs-lookup"><span data-stu-id="f2727-158">30</span></span> | <span data-ttu-id="f2727-159">60</span><span class="sxs-lookup"><span data-stu-id="f2727-159">60</span></span> |
| <span data-ttu-id="f2727-160">创建对话</span><span class="sxs-lookup"><span data-stu-id="f2727-160">Create Conversation</span></span> | <span data-ttu-id="f2727-161">3600</span><span class="sxs-lookup"><span data-stu-id="f2727-161">3600</span></span> | <span data-ttu-id="f2727-162">1800</span><span class="sxs-lookup"><span data-stu-id="f2727-162">1800</span></span> |
| <span data-ttu-id="f2727-163">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="f2727-163">Get Conversation Members</span></span>| <span data-ttu-id="f2727-164">1</span><span class="sxs-lookup"><span data-stu-id="f2727-164">1</span></span> | <span data-ttu-id="f2727-165">14 </span><span class="sxs-lookup"><span data-stu-id="f2727-165">14</span></span> |
| <span data-ttu-id="f2727-166">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="f2727-166">Get Conversation Members</span></span>| <span data-ttu-id="f2727-167">2</span><span class="sxs-lookup"><span data-stu-id="f2727-167">2</span></span> | <span data-ttu-id="f2727-168">16 </span><span class="sxs-lookup"><span data-stu-id="f2727-168">16</span></span> |
| <span data-ttu-id="f2727-169">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="f2727-169">Get Conversation Members</span></span>| <span data-ttu-id="f2727-170">30</span><span class="sxs-lookup"><span data-stu-id="f2727-170">30</span></span> | <span data-ttu-id="f2727-171">120</span><span class="sxs-lookup"><span data-stu-id="f2727-171">120</span></span> |
| <span data-ttu-id="f2727-172">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="f2727-172">Get Conversation Members</span></span>| <span data-ttu-id="f2727-173">3600</span><span class="sxs-lookup"><span data-stu-id="f2727-173">3600</span></span> | <span data-ttu-id="f2727-174">3600</span><span class="sxs-lookup"><span data-stu-id="f2727-174">3600</span></span> |
| <span data-ttu-id="f2727-175">获取对话</span><span class="sxs-lookup"><span data-stu-id="f2727-175">Get Conversations</span></span> | <span data-ttu-id="f2727-176">1</span><span class="sxs-lookup"><span data-stu-id="f2727-176">1</span></span> | <span data-ttu-id="f2727-177">14 </span><span class="sxs-lookup"><span data-stu-id="f2727-177">14</span></span> |
| <span data-ttu-id="f2727-178">获取对话</span><span class="sxs-lookup"><span data-stu-id="f2727-178">Get Conversations</span></span> | <span data-ttu-id="f2727-179">2</span><span class="sxs-lookup"><span data-stu-id="f2727-179">2</span></span> | <span data-ttu-id="f2727-180">16 </span><span class="sxs-lookup"><span data-stu-id="f2727-180">16</span></span> |
| <span data-ttu-id="f2727-181">获取对话</span><span class="sxs-lookup"><span data-stu-id="f2727-181">Get Conversations</span></span> | <span data-ttu-id="f2727-182">30</span><span class="sxs-lookup"><span data-stu-id="f2727-182">30</span></span> | <span data-ttu-id="f2727-183">120</span><span class="sxs-lookup"><span data-stu-id="f2727-183">120</span></span> |
| <span data-ttu-id="f2727-184">获取对话</span><span class="sxs-lookup"><span data-stu-id="f2727-184">Get Conversations</span></span> | <span data-ttu-id="f2727-185">3600</span><span class="sxs-lookup"><span data-stu-id="f2727-185">3600</span></span> | <span data-ttu-id="f2727-186">3600</span><span class="sxs-lookup"><span data-stu-id="f2727-186">3600</span></span> |

>[!NOTE]
> <span data-ttu-id="f2727-187">早期版本和 `TeamsInfo.getMembers` API `TeamsInfo.GetMembersAsync` 被弃用。</span><span class="sxs-lookup"><span data-stu-id="f2727-187">Previous versions of `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs are being deprecated.</span></span> <span data-ttu-id="f2727-188">它们将被限制为每分钟 5 个请求，并且每个团队最多返回 10，000 个成员。</span><span class="sxs-lookup"><span data-stu-id="f2727-188">They will be throttled to 5 requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="f2727-189">若要更新 Bot Framework SDK 和代码以使用最新的分页 API 终结点，请参阅团队和聊天成员的自动程序 [API 更改](../../resources/team-chat-member-api-changes.md)。</span><span class="sxs-lookup"><span data-stu-id="f2727-189">To update your Bot Framework SDK and the code to use the latest paginated API endpoints, see [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span></span>

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="f2727-190">所有自动程序每线程限制</span><span class="sxs-lookup"><span data-stu-id="f2727-190">Per thread limit for all bots</span></span>

<span data-ttu-id="f2727-191">此限制控制允许所有机器人在单个对话中生成的流量。</span><span class="sxs-lookup"><span data-stu-id="f2727-191">This limit controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="f2727-192">此处的对话是机器人和用户、群聊或团队中的频道之间的一对一对话。</span><span class="sxs-lookup"><span data-stu-id="f2727-192">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="f2727-193">**应用场景**</span><span class="sxs-lookup"><span data-stu-id="f2727-193">**Scenario**</span></span> | <span data-ttu-id="f2727-194">**时间段（秒）**</span><span class="sxs-lookup"><span data-stu-id="f2727-194">**Time-period (sec)**</span></span> | <span data-ttu-id="f2727-195">**允许的最大操作数**</span><span class="sxs-lookup"><span data-stu-id="f2727-195">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f2727-196">发送到对话</span><span class="sxs-lookup"><span data-stu-id="f2727-196">Send to Conversation</span></span> | <span data-ttu-id="f2727-197">1</span><span class="sxs-lookup"><span data-stu-id="f2727-197">1</span></span> | <span data-ttu-id="f2727-198">14 </span><span class="sxs-lookup"><span data-stu-id="f2727-198">14</span></span> |
| <span data-ttu-id="f2727-199">发送到对话</span><span class="sxs-lookup"><span data-stu-id="f2727-199">Send to Conversation</span></span> | <span data-ttu-id="f2727-200">2</span><span class="sxs-lookup"><span data-stu-id="f2727-200">2</span></span> | <span data-ttu-id="f2727-201">16 </span><span class="sxs-lookup"><span data-stu-id="f2727-201">16</span></span> |
| <span data-ttu-id="f2727-202">创建对话</span><span class="sxs-lookup"><span data-stu-id="f2727-202">Create Conversation</span></span> | <span data-ttu-id="f2727-203">1</span><span class="sxs-lookup"><span data-stu-id="f2727-203">1</span></span> | <span data-ttu-id="f2727-204">14 </span><span class="sxs-lookup"><span data-stu-id="f2727-204">14</span></span> |
| <span data-ttu-id="f2727-205">创建对话</span><span class="sxs-lookup"><span data-stu-id="f2727-205">Create Conversation</span></span> | <span data-ttu-id="f2727-206">2</span><span class="sxs-lookup"><span data-stu-id="f2727-206">2</span></span> | <span data-ttu-id="f2727-207">16 </span><span class="sxs-lookup"><span data-stu-id="f2727-207">16</span></span> |
| <span data-ttu-id="f2727-208">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="f2727-208">CreateConversation</span></span>| <span data-ttu-id="f2727-209">1</span><span class="sxs-lookup"><span data-stu-id="f2727-209">1</span></span> | <span data-ttu-id="f2727-210">14 </span><span class="sxs-lookup"><span data-stu-id="f2727-210">14</span></span> |
| <span data-ttu-id="f2727-211">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="f2727-211">CreateConversation</span></span>| <span data-ttu-id="f2727-212">2</span><span class="sxs-lookup"><span data-stu-id="f2727-212">2</span></span> | <span data-ttu-id="f2727-213">16 </span><span class="sxs-lookup"><span data-stu-id="f2727-213">16</span></span> |
| <span data-ttu-id="f2727-214">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="f2727-214">Get Conversation Members</span></span>| <span data-ttu-id="f2727-215">1</span><span class="sxs-lookup"><span data-stu-id="f2727-215">1</span></span> | <span data-ttu-id="f2727-216">28</span><span class="sxs-lookup"><span data-stu-id="f2727-216">28</span></span> |
| <span data-ttu-id="f2727-217">获取对话成员</span><span class="sxs-lookup"><span data-stu-id="f2727-217">Get Conversation Members</span></span>| <span data-ttu-id="f2727-218">2</span><span class="sxs-lookup"><span data-stu-id="f2727-218">2</span></span> | <span data-ttu-id="f2727-219">32</span><span class="sxs-lookup"><span data-stu-id="f2727-219">32</span></span> |
| <span data-ttu-id="f2727-220">获取对话</span><span class="sxs-lookup"><span data-stu-id="f2727-220">Get Conversations</span></span> | <span data-ttu-id="f2727-221">1</span><span class="sxs-lookup"><span data-stu-id="f2727-221">1</span></span> | <span data-ttu-id="f2727-222">28</span><span class="sxs-lookup"><span data-stu-id="f2727-222">28</span></span> |
| <span data-ttu-id="f2727-223">获取对话</span><span class="sxs-lookup"><span data-stu-id="f2727-223">Get Conversations</span></span> | <span data-ttu-id="f2727-224">2</span><span class="sxs-lookup"><span data-stu-id="f2727-224">2</span></span> | <span data-ttu-id="f2727-225">32</span><span class="sxs-lookup"><span data-stu-id="f2727-225">32</span></span> |
