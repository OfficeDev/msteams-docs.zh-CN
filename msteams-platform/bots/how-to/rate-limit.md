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
# <a name="optimize-your-bot-with-rate-limiting-in-teams"></a>通过团队中的速率限制来优化你的智能机器人

速率限制是一种将邮件限制为特定最大频率的方法。 一般来说，您的应用程序必须限制向单个聊天或频道对话发布的消息数。 这可确保最佳体验，并且邮件不会显示为垃圾邮件给用户。

为了保护 Microsoft Teams 及其用户，机器人 API 提供了传入请求的速率限制。 超过此限制的应用将收到 `HTTP 429 Too Many Requests` 错误状态。 所有请求都受同一速率限制策略的限制，包括发送邮件、频道枚举和名单提取。

由于速率限制的确切值可能会发生变化，因此当 API 返回 时，应用程序必须实现相应的退步行为 `HTTP 429 Too Many Requests` 。

## <a name="handle-rate-limits"></a>处理速率限制

发出自动程序生成器 SDK 操作时，可以处理 `Microsoft.Rest.HttpOperationException` 和检查状态代码。

以下代码显示了处理速率限制的示例：

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

处理自动程序速率限制后，可以使用指数 `HTTP 429` 退步处理响应。

## <a name="handle-http-429-responses"></a>处理 `HTTP 429` 响应

通常，必须采取简单的预防措施以避免收到 `HTTP 429` 响应。 例如，避免向同一个人对话或频道对话发出多个请求。 相反，请创建一批 API 请求。

建议将指数退约与随机抖动一同处理 429。 这将确保多个请求不会在重试时引入冲突。

处理响应 `HTTP 429` 后，可以浏览检测暂时性异常的示例。

## <a name="detect-transient-exceptions-example"></a>检测暂时性异常示例

以下代码显示了使用瞬态故障处理应用程序块的指数退路的示例：

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

可以使用瞬态故障处理执行回发 [并重试](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)。 有关获取和安装 NuGet 程序包的指南，请参阅将瞬态 [错误处理应用程序块添加到你的解决方案](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)。 另请参阅 [瞬态故障处理](/azure/architecture/best-practices/transient-faults)。

完成检测暂时性异常的示例后，请浏览指数退步示例。 可以使用指数退步，而不是在失败时重试。

## <a name="backoff-example"></a>退市示例

除了检测速率限制之外，还可以执行指数退市。

以下代码显示了指数退步的示例：

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

您还可以使用本节 `System.Action` 中所述的重试策略执行方法。 引用的库还允许您指定固定间隔或线性退信机制。

将值和策略存储在配置文件中，以运行时微调和调整值。

有关详细信息，请参阅 [重试模式](/azure/architecture/patterns/retry)。

您还可以使用每个机器人每线程限制处理速率限制。

## <a name="per-bot-per-thread-limit"></a>每个机器人每线程限制

>[!NOTE]
> 在服务级别拆分邮件会导致每秒请求数超过 RPS () 。 如果担心接近限制，则必须实施 [退约策略](#backoff-example)。 本节中提供的值仅用于估计。

每个线程的自动程序限制控制允许机器人在单个对话上生成的流量。 此处的对话是机器人和用户、群聊或团队中的频道之间的一对一对话。

下表提供了每个机器人每个线程的限制：

| 方案 | 时间段（以秒表示） | 允许的最大操作数 |
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
> 早期版本和 `TeamsInfo.getMembers` API `TeamsInfo.GetMembersAsync` 被弃用。 它们被限制为每分钟五个请求，并且每个团队最多返回 10，000 个成员。 若要更新 Bot Framework SDK 和代码以使用最新的分页 API 终结点，请参阅团队和聊天成员的自动程序 [API 更改](../../resources/team-chat-member-api-changes.md)。

您还可以使用所有机器人的按线程限制处理速率限制。

## <a name="per-thread-limit-for-all-bots"></a>所有自动程序每线程限制

所有机器人的线程限制控制允许所有机器人在单个对话中生成的流量。 此处的对话是机器人和用户、群聊或团队中的频道之间的一对一对话。

下表提供了所有自动程序每线程的限制：

| 方案 | 时间段（以秒表示） | 允许的最大操作数 |
| --- | --- | --- |
| 发送到对话 | 1 | 14  |
| 发送到对话 | 2 | 16  |
| 创建对话 | 1 | 14  |
| 创建对话 | 2 | 16  |
| 创建对话| 1 | 14  |
| 创建对话| 2 | 16  |
| 获取对话成员| 1 | 28 |
| 获取对话成员| 2 | 32 |
| 获取对话 | 1 | 28 |
| 获取对话 | 2 | 32 |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [通话和会议智能机器人](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

