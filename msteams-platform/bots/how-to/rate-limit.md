---
title: 机器人的速率限制
description: 了解如何使用速率限制优化机器人。 检测每个机器人线程限制的暂时性异常。 还可以执行指数回退。
ms.localizationpriority: medium
ms.openlocfilehash: 487f251be40894464e55b891a7386cd8a04abe25
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100425"
---
# <a name="optimize-your-bot-with-rate-limiting-in-teams"></a>通过团队中的速率限制来优化你的智能机器人

速率限制是一种将消息限制在特定最大频率的方法。 一般原则是，应用程序必须限制其发布到单个聊天或频道对话的消息数。 这可确保获得最佳体验，并且消息不会显示为用户的垃圾邮件。

为了保护 Microsoft Teams 及其用户，机器人 API 为传入请求提供速率限制。 超出此限制的应用将收到 `HTTP 429 Too Many Requests` 错误状态。 所有请求都遵循相同的速率限制策略，包括发送消息、频道枚举和名单提取。

由于速率限制的确切值可能会更改，因此当 API 返回 `HTTP 429 Too Many Requests` 时，应用程序必须实现适当的回退行为。

## <a name="handle-rate-limits"></a>处理速率限制

发出 Bot Builder SDK 操作时，可处理 `Microsoft.Rest.HttpOperationException` 和检查状态代码。

以下代码演示了处理速率限制的示例：

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

处理机器人的速率限制后，可使用指数退避来处理 `HTTP 429` 响应。

## <a name="handle-http-429-responses"></a>处理 `HTTP 429` 响应

一般情况下，必须采取简单的预防措施以避免收到 `HTTP 429` 响应。 例如，避免向同一个人或频道对话发出多个请求。 而是创建一批 API 请求。

建议将指数退避和随机抖动结合使用来处理 429 响应。 这可确保多个请求不会在重试时引入冲突。

处理 `HTTP 429` 响应后，可查看关于检测暂时性异常的示例。

> [!NOTE]
> 除了重试错误代码 **429**，还必须重试错误代码 **412**、**502** 和 **504**。

## <a name="detect-transient-exceptions-example"></a>检测暂时性异常示例

以下代码演示了通过暂时性故障处理应用程序块使用指数退避的示例：

```csharp
public class BotSdkTransientExceptionDetectionStrategy : ITransientErrorDetectionStrategy
    {
        // List of error codes to retry on
        List<int> transientErrorStatusCodes = new List<int>() { 429 };

        public static bool IsTransient(Exception ex)
          {
              if (ex.Message.Contains("429"))
                  return true;

              HttpResponseMessageWrapper? response = null;
              if (ex is HttpOperationException httpOperationException)
              {
                  response = httpOperationException.Response;
              }
              else
              if (ex is ErrorResponseException errorResponseException)
              {
                  response = errorResponseException.Response;
              }
              return response != null && transientErrorStatusCodes.Contains((int)response.StatusCode);
          }
    }
```

可使用[暂时性故障处理](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)来执行回退和重试。 有关如何获取和安装 NuGet 包的指南，请参阅[将暂时性故障处理应用程序块添加到解决方案](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)。 另请参阅[暂时性故障处理](/azure/architecture/best-practices/transient-faults)。

查看关于检测暂时性异常的示例后，请查看指数退避示例。 可使用指数退避，而不是在故障时重试。

## <a name="backoff-example"></a>回退示例

除了检测速率限制外，还可执行指数退避。

以下代码演示了指数退避的示例：

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

还可使用本部分中所述的重试策略实施 `System.Action` 方法执行。 通过引用的库,还可指定固定间隔或线性回退机制。

将值和策略存储在配置文件中，以便在运行时微调和调整值。

有关详细信息，请参阅[重试模式](/azure/architecture/patterns/retry)。

还可使用每机器人每线程限制来处理速率限制。

## <a name="per-bot-per-thread-limit"></a>每机器人每线程限制

每机器人每线程限制用于控制一台机器人可在单个会话中生成的流量。 机器人与用户、群组聊天或团队中的频道之间进行 1:1 的对话。 因此，如果应用程序向每个用户发送一条机器人消息，则线程限制不会限制。

>[!NOTE]
>
> * 仅当向一位用户发送多条机器人消息时，才需遵守 3600 秒和 1800 个操作这一线程限制。
> * 每租户每应用全局限制为每秒 50 个请求 (RPS)。 因此，每秒机器人消息总数不得超过线程限制。
> * 服务级别的消息拆分会导致超过预期的 RPS。 如果担心达到限制，必须实施[回退策略](#backoff-example)。 本部分中提供的值仅供估算。

下表提供每机器人每线程的限制：

| 应用场景 | 时间（秒） | 允许的最大操作数 |
| --- | --- | --- |
| 发送到对话 | 1 | 7  |
| 发送到对话 | 2 | 8  |
| 发送到对话 | 30 | 60 |
| 发送到对话 | 3600 | 1800 |
| 创建对话 | 1 | 7  |
| 创建对话 | 2 | 8  |
| 创建对话 | 30 | 60 |
| 创建对话 | 3600 | 1800 |
| 获取对话成员| 1 | 14 |
| 获取对话成员| 2 | 16 |
| 获取对话成员| 30 | 120 |
| 获取对话成员| 3600 | 3600 |
| 获取对话 | 1 | 14 |
| 获取对话 | 2 | 16 |
| 获取对话 | 30 | 120 |
| 获取对话 | 3600 | 3600 |

>[!NOTE]
> 即将弃用以前版本的 `TeamsInfo.getMembers` API `TeamsInfo.GetMembersAsync` 和 API。 限制是每分钟 5 个请求，对每个团队返回最多 1 万个成员。 若要更新 Bot Framework SDK 和代码来使用最新的分页 API 终结点，请参阅[针对团队和聊天成员的机器人 API 更改](../../resources/team-chat-member-api-changes.md)。

还可使用所有机器人每线程限制来处理速率限制。

## <a name="per-thread-limit-for-all-bots"></a>所有机器人每线程限制

所有机器人每线程限制用于控制所有机器人可在单个会话中生成的流量。 此处的聊天是机器人和用户之间的 1：1、群组聊天或团队中的频道。

下表提供了所有机器人每线程的限制：

| 应用场景 | 时间（秒） | 允许的最大操作数 |
| --- | --- | --- |
| 发送到对话 | 1 | 14 |
| 发送到对话 | 2 | 16 |
| 创建对话 | 1 | 14 |
| 创建对话 | 2 | 16 |
| 创建对话| 1 | 14 |
| 创建对话| 2 | 16 |
| 获取对话成员| 1 | 28 |
| 获取对话成员| 2 | 32 |
| 获取对话 | 1 | 28 |
| 获取对话 | 2 | 32 |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [通话和会议机器人](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

## <a name="see-also"></a>另请参阅

[管理长时间运行的操作](/azure/bot-service/bot-builder-howto-long-operations-guidance?view=azure-bot-service-4.0&preserve-view=true)
