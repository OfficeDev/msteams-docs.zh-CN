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
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a>优化机器人：Microsoft Teams 中的速率限制和最佳做法

一般来说，您的应用程序应限制向单个聊天或频道对话发布的消息数。 这可确保最终用户不会感到"spa此操作"的最佳体验。

为了保护 Microsoft Teams 及其用户，机器人 API 对传入请求进行速率限制。 超过此限制的应用将收到 `HTTP 429 Too Many Requests` 错误状态。 所有请求都受同一速率限制策略的限制，包括发送邮件、频道枚举和名单提取。

由于速率限制的确切值可能会更改，因此我们建议你的应用程序在 API 返回 时实现相应的退步行为 `HTTP 429 Too Many Requests` 。

## <a name="handling-rate-limits"></a>处理速率限制

发出自动程序生成器 SDK 操作时，可以处理 `Microsoft.Rest.HttpOperationException` 和检查状态代码。

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

## <a name="best-practices"></a>最佳做法

通常，应该采取简单的预防措施以避免收到 `HTTP 429` 响应。 例如，避免向同一个人对话或频道对话发出多个请求。 相反，请考虑对 API 请求进行批处理。

建议将指数退约与随机抖动一同处理 429。 这将确保多个请求不会在重试时引入冲突。

## <a name="example-detecting-transient-exceptions"></a>示例：检测暂时性异常

下面是通过瞬态故障处理应用程序块使用指数退路的示例。

可以使用瞬态故障处理执行退回 [并重试](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)。 有关获取和安装 NuGet 程序包的指南，请参阅 Adding [the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)) 。 *另请参阅瞬*[态故障处理](/azure/architecture/best-practices/transient-faults)。

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

## <a name="example-backoff"></a>示例：退市

除了检测速率限制之外，还可以执行指数退市。

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

您还可以使用上述 `System.Action` 重试策略执行方法。 引用的库还允许您指定固定间隔或线性退信机制。

我们建议将值和策略存储在配置文件中，以运行时微调和调整值。

有关详细信息，请查看此有关各种重试模式（重试模式）的 [方便指南](/azure/architecture/patterns/retry)。

## <a name="per-bot-per-thread-limit"></a>每个机器人每线程限制

>[!NOTE]
>在服务级别拆分邮件会导致每秒请求数超过 RPS () 。 如果担心接近限制，应实施上述退约策略。 下面提供的值仅用于估计。

此限制控制允许机器人在单个对话上生成的流量。 此处的对话是机器人和用户、群聊或团队中的频道之间的一对一对话。

| **应用场景** | **时间段（秒）** | **允许的最大操作数** |
| --- | --- | --- |
| 发送到对话 | 1 | 7  |
| 发送到对话 | 2 | 8  |
| 发送到对话 | 30 | 60 |
| 发送到对话 | 3600 | 1800 |
| 创建对话 | 1 | 7  |
| 创建对话 | 2 | 8  |
| 创建对话 | 30 | 60 |
| 创建对话 | 3600 | 1800 |
| 获取对话成员| 1 | 14  |
| 获取对话成员| 2 | 16  |
| 获取对话成员| 30 | 120 |
| 获取对话成员| 3600 | 3600 |
| 获取对话 | 1 | 14  |
| 获取对话 | 2 | 16  |
| 获取对话 | 30 | 120 |
| 获取对话 | 3600 | 3600 |

>[!NOTE]
> 早期版本和 `TeamsInfo.getMembers` API `TeamsInfo.GetMembersAsync` 被弃用。 它们将被限制为每分钟 5 个请求，并且每个团队最多返回 10，000 个成员。 若要更新 Bot Framework SDK 和代码以使用最新的分页 API 终结点，请参阅团队和聊天成员的自动程序 [API 更改](../../resources/team-chat-member-api-changes.md)。

## <a name="per-thread-limit-for-all-bots"></a>所有自动程序每线程限制

此限制控制允许所有机器人在单个对话中生成的流量。 此处的对话是机器人和用户、群聊或团队中的频道之间的一对一对话。

| **应用场景** | **时间段（秒）** | **允许的最大操作数** |
| --- | --- | --- |
| 发送到对话 | 1 | 14  |
| 发送到对话 | 2 | 16  |
| 创建对话 | 1 | 14  |
| 创建对话 | 2 | 16  |
| CreateConversation| 1 | 14  |
| CreateConversation| 2 | 16  |
| 获取对话成员| 1 | 28 |
| 获取对话成员| 2 | 32 |
| 获取对话 | 1 | 28 |
| 获取对话 | 2 | 32 |
