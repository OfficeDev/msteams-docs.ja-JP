---
title: Teams のレート制限を使用してボットを最適化する
description: Microsoft Teams のレート制限とベスト プラクティス
ms.topic: conceptual
keywords: Teams ボットのレート制限
ms.openlocfilehash: 245c51fc736e5f888299535c3e50ec6232183623
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696998"
---
# <a name="optimize-your-bot-with-rate-limiting-in-teams"></a><span data-ttu-id="2436a-104">Teams のレート制限を使用してボットを最適化する</span><span class="sxs-lookup"><span data-stu-id="2436a-104">Optimize your bot with rate limiting in Teams</span></span>

<span data-ttu-id="2436a-105">レート制限は、メッセージを特定の最大頻度に制限する方法です。</span><span class="sxs-lookup"><span data-stu-id="2436a-105">Rate limiting is a method to limit messages to a certain maximum frequency.</span></span> <span data-ttu-id="2436a-106">一般的な原則として、アプリケーションは投稿するメッセージの数を個々のチャットまたはチャネルの会話に制限する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2436a-106">As a general principle, your application must limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="2436a-107">これにより、最適なエクスペリエンスが確保され、メッセージがユーザーにスパムとして表示されません。</span><span class="sxs-lookup"><span data-stu-id="2436a-107">This ensures an optimal experience and messages do not appear as spam to your users.</span></span>

<span data-ttu-id="2436a-108">Microsoft Teams とそのユーザーを保護するために、ボット API は受信要求のレート制限を提供します。</span><span class="sxs-lookup"><span data-stu-id="2436a-108">To protect Microsoft Teams and its users, the bot APIs provide a rate limit for incoming requests.</span></span> <span data-ttu-id="2436a-109">この制限を超えるアプリは、エラー状態 `HTTP 429 Too Many Requests` を受け取る。</span><span class="sxs-lookup"><span data-stu-id="2436a-109">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="2436a-110">すべての要求は、メッセージの送信、チャネル列挙、名簿フェッチなど、同じレート制限ポリシーの対象です。</span><span class="sxs-lookup"><span data-stu-id="2436a-110">All requests are subject to the same rate limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="2436a-111">レート制限の正確な値は変更される可能性があります。API が返される場合、アプリケーションは適切なバックオフ動作を実装する必要があります `HTTP 429 Too Many Requests` 。</span><span class="sxs-lookup"><span data-stu-id="2436a-111">As the exact values of rate limits are subject to change, your application must implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handle-rate-limits"></a><span data-ttu-id="2436a-112">レート制限の処理</span><span class="sxs-lookup"><span data-stu-id="2436a-112">Handle rate limits</span></span>

<span data-ttu-id="2436a-113">ボット ビルダー SDK 操作を発行する場合は、状態コードを処理 `Microsoft.Rest.HttpOperationException` して確認できます。</span><span class="sxs-lookup"><span data-stu-id="2436a-113">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

<span data-ttu-id="2436a-114">次のコードは、レート制限の処理例を示しています。</span><span class="sxs-lookup"><span data-stu-id="2436a-114">The following code shows an example of handling rate limits:</span></span>

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

<span data-ttu-id="2436a-115">ボットのレート制限を処理した後、指数バックオフを `HTTP 429` 使用して応答を処理できます。</span><span class="sxs-lookup"><span data-stu-id="2436a-115">After you handle rate limits for bots, you can handle `HTTP 429` responses using an exponential backoff.</span></span>

## <a name="handle-http-429-responses"></a><span data-ttu-id="2436a-116">応答 `HTTP 429` の処理</span><span class="sxs-lookup"><span data-stu-id="2436a-116">Handle `HTTP 429` responses</span></span>

<span data-ttu-id="2436a-117">一般に、応答を受信しないように、簡単な予防措置を講じ `HTTP 429` なければならない。</span><span class="sxs-lookup"><span data-stu-id="2436a-117">In general, you must take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="2436a-118">たとえば、同じ個人またはチャネルの会話に対して複数の要求を発行しないようにします。</span><span class="sxs-lookup"><span data-stu-id="2436a-118">For example, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="2436a-119">代わりに、API 要求のバッチを作成します。</span><span class="sxs-lookup"><span data-stu-id="2436a-119">Instead, create a batch of the API requests.</span></span>

<span data-ttu-id="2436a-120">ランダムなジッターで指数バックオフを使用する方法は、429 を処理するための推奨される方法です。</span><span class="sxs-lookup"><span data-stu-id="2436a-120">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="2436a-121">これにより、複数の要求が再試行時に競合を発生しない。</span><span class="sxs-lookup"><span data-stu-id="2436a-121">This ensures that multiple requests do not introduce collisions on retries.</span></span>

<span data-ttu-id="2436a-122">応答を `HTTP 429` 処理した後、一時的な例外を検出する例を確認できます。</span><span class="sxs-lookup"><span data-stu-id="2436a-122">After you handle `HTTP 429` responses, you can go through the example for detecting transient exceptions.</span></span>

## <a name="detect-transient-exceptions-example"></a><span data-ttu-id="2436a-123">一時的な例外の検出の例</span><span class="sxs-lookup"><span data-stu-id="2436a-123">Detect transient exceptions example</span></span>

<span data-ttu-id="2436a-124">次のコードは、一時的な障害処理アプリケーション ブロックを使用して指数バックオフを使用する例を示しています。</span><span class="sxs-lookup"><span data-stu-id="2436a-124">The following code shows an example of using exponential backoff using the transient fault handling application block:</span></span>

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

<span data-ttu-id="2436a-125">一時的な障害処理を使用して、バックオフと再試行 [を実行できます](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)。</span><span class="sxs-lookup"><span data-stu-id="2436a-125">You can perform backoff and retries using [transient fault handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="2436a-126">NuGet パッケージの取得とインストールに関するガイドラインについては、「一時的な障害処理アプリケーション ブロックをソリューションに追加する [」を参照してください](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)。</span><span class="sxs-lookup"><span data-stu-id="2436a-126">For guidelines on obtaining and installing the NuGet package, see [adding the transient fault handling application block to your solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span></span> <span data-ttu-id="2436a-127">一時的な [障害処理も参照してください](/azure/architecture/best-practices/transient-faults)。</span><span class="sxs-lookup"><span data-stu-id="2436a-127">See also [transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

<span data-ttu-id="2436a-128">一時的な例外を検出する例を実行した後、指数バックオフの例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2436a-128">After you go through the example for detecting transient exceptions, go through the exponential backoff example.</span></span> <span data-ttu-id="2436a-129">エラー時に再試行する代わりに指数バックオフを使用できます。</span><span class="sxs-lookup"><span data-stu-id="2436a-129">You can use exponential backoff instead of retrying on failures.</span></span>

## <a name="backoff-example"></a><span data-ttu-id="2436a-130">バックオフの例</span><span class="sxs-lookup"><span data-stu-id="2436a-130">Backoff example</span></span>

<span data-ttu-id="2436a-131">レート制限の検出に加えて、指数バックオフも実行できます。</span><span class="sxs-lookup"><span data-stu-id="2436a-131">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

<span data-ttu-id="2436a-132">次のコードは、指数バックオフの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="2436a-132">The following code shows an example of exponential backoff:</span></span>

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

<span data-ttu-id="2436a-133">また、このセクションで説明 `System.Action` する再試行ポリシーを使用してメソッドの実行を実行できます。</span><span class="sxs-lookup"><span data-stu-id="2436a-133">You can also perform a `System.Action` method execution with the retry policy described in this section.</span></span> <span data-ttu-id="2436a-134">参照されるライブラリでは、固定間隔または線形バックオフ メカニズムを指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="2436a-134">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="2436a-135">値と戦略を構成ファイルに格納して、実行時に値を微調整および調整します。</span><span class="sxs-lookup"><span data-stu-id="2436a-135">Store the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="2436a-136">詳細については、「再試行パターン [」を参照してください](/azure/architecture/patterns/retry)。</span><span class="sxs-lookup"><span data-stu-id="2436a-136">For more information, see [retry patterns](/azure/architecture/patterns/retry).</span></span>

<span data-ttu-id="2436a-137">スレッドごとのボットごとの制限を使用して、レート制限を処理できます。</span><span class="sxs-lookup"><span data-stu-id="2436a-137">You can also handle rate limit using the per bot per thread limit.</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="2436a-138">スレッドごとのボットごとの制限</span><span class="sxs-lookup"><span data-stu-id="2436a-138">Per bot per thread limit</span></span>

>[!NOTE]
> <span data-ttu-id="2436a-139">サービス レベルでのメッセージの分割は、予想される要求 /秒 (RPS) よりも高くなります。</span><span class="sxs-lookup"><span data-stu-id="2436a-139">Message splitting at the service level results in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="2436a-140">制限への近付きが懸念される場合は、バックオフ戦略を [実装する必要があります](#backoff-example)。</span><span class="sxs-lookup"><span data-stu-id="2436a-140">If you are concerned about approaching the limits, you must implement the [backoff strategy](#backoff-example).</span></span> <span data-ttu-id="2436a-141">このセクションで提供される値は、見積もり専用です。</span><span class="sxs-lookup"><span data-stu-id="2436a-141">The values provided in this section are for estimation only.</span></span>

<span data-ttu-id="2436a-142">スレッドごとのボットごとの制限は、ボットが 1 回の会話で生成できるトラフィックを制御します。</span><span class="sxs-lookup"><span data-stu-id="2436a-142">The per bot per thread limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="2436a-143">ここでの会話は、ボットとユーザー、グループ チャット、またはチーム内のチャネルの間で 1:1 です。</span><span class="sxs-lookup"><span data-stu-id="2436a-143">A conversation here is 1:1 between bot and user, a group chat, or a channel in a team.</span></span>

<span data-ttu-id="2436a-144">次の表に、スレッドごとのボットごとの制限を示します。</span><span class="sxs-lookup"><span data-stu-id="2436a-144">The following table provides the per bot per thread limits:</span></span>

| <span data-ttu-id="2436a-145">シナリオ</span><span class="sxs-lookup"><span data-stu-id="2436a-145">Scenario</span></span> | <span data-ttu-id="2436a-146">期間 (秒)</span><span class="sxs-lookup"><span data-stu-id="2436a-146">Time period in seconds</span></span> | <span data-ttu-id="2436a-147">許可される操作の最大数</span><span class="sxs-lookup"><span data-stu-id="2436a-147">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2436a-148">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="2436a-148">Send to conversation</span></span> | <span data-ttu-id="2436a-149">1</span><span class="sxs-lookup"><span data-stu-id="2436a-149">1</span></span> | <span data-ttu-id="2436a-150">7</span><span class="sxs-lookup"><span data-stu-id="2436a-150">7</span></span> |
| <span data-ttu-id="2436a-151">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="2436a-151">Send to conversation</span></span> | <span data-ttu-id="2436a-152">2</span><span class="sxs-lookup"><span data-stu-id="2436a-152">2</span></span> | <span data-ttu-id="2436a-153">8</span><span class="sxs-lookup"><span data-stu-id="2436a-153">8</span></span> |
| <span data-ttu-id="2436a-154">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="2436a-154">Send to conversation</span></span> | <span data-ttu-id="2436a-155">30</span><span class="sxs-lookup"><span data-stu-id="2436a-155">30</span></span> | <span data-ttu-id="2436a-156">60</span><span class="sxs-lookup"><span data-stu-id="2436a-156">60</span></span> |
| <span data-ttu-id="2436a-157">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="2436a-157">Send to conversation</span></span> | <span data-ttu-id="2436a-158">3600</span><span class="sxs-lookup"><span data-stu-id="2436a-158">3600</span></span> | <span data-ttu-id="2436a-159">1800</span><span class="sxs-lookup"><span data-stu-id="2436a-159">1800</span></span> |
| <span data-ttu-id="2436a-160">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="2436a-160">Create conversation</span></span> | <span data-ttu-id="2436a-161">1</span><span class="sxs-lookup"><span data-stu-id="2436a-161">1</span></span> | <span data-ttu-id="2436a-162">7</span><span class="sxs-lookup"><span data-stu-id="2436a-162">7</span></span> |
| <span data-ttu-id="2436a-163">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="2436a-163">Create conversation</span></span> | <span data-ttu-id="2436a-164">2</span><span class="sxs-lookup"><span data-stu-id="2436a-164">2</span></span> | <span data-ttu-id="2436a-165">8</span><span class="sxs-lookup"><span data-stu-id="2436a-165">8</span></span> |
| <span data-ttu-id="2436a-166">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="2436a-166">Create conversation</span></span> | <span data-ttu-id="2436a-167">30</span><span class="sxs-lookup"><span data-stu-id="2436a-167">30</span></span> | <span data-ttu-id="2436a-168">60</span><span class="sxs-lookup"><span data-stu-id="2436a-168">60</span></span> |
| <span data-ttu-id="2436a-169">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="2436a-169">Create conversation</span></span> | <span data-ttu-id="2436a-170">3600</span><span class="sxs-lookup"><span data-stu-id="2436a-170">3600</span></span> | <span data-ttu-id="2436a-171">1800</span><span class="sxs-lookup"><span data-stu-id="2436a-171">1800</span></span> |
| <span data-ttu-id="2436a-172">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="2436a-172">Get conversation members</span></span>| <span data-ttu-id="2436a-173">1</span><span class="sxs-lookup"><span data-stu-id="2436a-173">1</span></span> | <span data-ttu-id="2436a-174">14 </span><span class="sxs-lookup"><span data-stu-id="2436a-174">14</span></span> |
| <span data-ttu-id="2436a-175">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="2436a-175">Get conversation members</span></span>| <span data-ttu-id="2436a-176">2</span><span class="sxs-lookup"><span data-stu-id="2436a-176">2</span></span> | <span data-ttu-id="2436a-177">16 </span><span class="sxs-lookup"><span data-stu-id="2436a-177">16</span></span> |
| <span data-ttu-id="2436a-178">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="2436a-178">Get conversation members</span></span>| <span data-ttu-id="2436a-179">30</span><span class="sxs-lookup"><span data-stu-id="2436a-179">30</span></span> | <span data-ttu-id="2436a-180">120</span><span class="sxs-lookup"><span data-stu-id="2436a-180">120</span></span> |
| <span data-ttu-id="2436a-181">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="2436a-181">Get conversation members</span></span>| <span data-ttu-id="2436a-182">3600</span><span class="sxs-lookup"><span data-stu-id="2436a-182">3600</span></span> | <span data-ttu-id="2436a-183">3600</span><span class="sxs-lookup"><span data-stu-id="2436a-183">3600</span></span> |
| <span data-ttu-id="2436a-184">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="2436a-184">Get conversations</span></span> | <span data-ttu-id="2436a-185">1</span><span class="sxs-lookup"><span data-stu-id="2436a-185">1</span></span> | <span data-ttu-id="2436a-186">14 </span><span class="sxs-lookup"><span data-stu-id="2436a-186">14</span></span> |
| <span data-ttu-id="2436a-187">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="2436a-187">Get conversations</span></span> | <span data-ttu-id="2436a-188">2</span><span class="sxs-lookup"><span data-stu-id="2436a-188">2</span></span> | <span data-ttu-id="2436a-189">16 </span><span class="sxs-lookup"><span data-stu-id="2436a-189">16</span></span> |
| <span data-ttu-id="2436a-190">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="2436a-190">Get conversations</span></span> | <span data-ttu-id="2436a-191">30</span><span class="sxs-lookup"><span data-stu-id="2436a-191">30</span></span> | <span data-ttu-id="2436a-192">120</span><span class="sxs-lookup"><span data-stu-id="2436a-192">120</span></span> |
| <span data-ttu-id="2436a-193">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="2436a-193">Get conversations</span></span> | <span data-ttu-id="2436a-194">3600</span><span class="sxs-lookup"><span data-stu-id="2436a-194">3600</span></span> | <span data-ttu-id="2436a-195">3600</span><span class="sxs-lookup"><span data-stu-id="2436a-195">3600</span></span> |

>[!NOTE]
> <span data-ttu-id="2436a-196">以前のバージョンと `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` API は非推奨です。</span><span class="sxs-lookup"><span data-stu-id="2436a-196">Previous versions of `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs are being deprecated.</span></span> <span data-ttu-id="2436a-197">1 分あたり 5 つの要求に調整され、チームごとに最大 10K のメンバーが返されます。</span><span class="sxs-lookup"><span data-stu-id="2436a-197">They are throttled to five requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="2436a-198">ボット フレームワーク SDK と、ページ分割された最新の API エンドポイントを使用するコードを更新するには、「チームおよびチャット メンバーのボット API の変更」 [を参照してください](../../resources/team-chat-member-api-changes.md)。</span><span class="sxs-lookup"><span data-stu-id="2436a-198">To update your Bot Framework SDK and the code to use the latest paginated API endpoints, see [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span></span>

<span data-ttu-id="2436a-199">また、すべてのボットのスレッドごとの制限を使用して、レート制限を処理できます。</span><span class="sxs-lookup"><span data-stu-id="2436a-199">You can also handle rate limit using the per thread limit for all bots.</span></span>

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="2436a-200">すべてのボットのスレッドごとの制限</span><span class="sxs-lookup"><span data-stu-id="2436a-200">Per thread limit for all bots</span></span>

<span data-ttu-id="2436a-201">すべてのボットのスレッドごとの制限は、すべてのボットが 1 回の会話で生成できるトラフィックを制御します。</span><span class="sxs-lookup"><span data-stu-id="2436a-201">The per thread limit for all bots controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="2436a-202">ここでの会話は、ボットとユーザー、グループ チャット、またはチーム内のチャネルの間で 1:1 です。</span><span class="sxs-lookup"><span data-stu-id="2436a-202">A conversation here is 1:1 between bot and user, a group chat, or a channel in a team.</span></span>

<span data-ttu-id="2436a-203">次の表に、すべてのボットのスレッドごとの制限を示します。</span><span class="sxs-lookup"><span data-stu-id="2436a-203">The following table provides the per thread limit for all bots:</span></span>

| <span data-ttu-id="2436a-204">シナリオ</span><span class="sxs-lookup"><span data-stu-id="2436a-204">Scenario</span></span> | <span data-ttu-id="2436a-205">期間 (秒)</span><span class="sxs-lookup"><span data-stu-id="2436a-205">Time period in seconds</span></span> | <span data-ttu-id="2436a-206">許可される操作の最大数</span><span class="sxs-lookup"><span data-stu-id="2436a-206">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2436a-207">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="2436a-207">Send to conversation</span></span> | <span data-ttu-id="2436a-208">1</span><span class="sxs-lookup"><span data-stu-id="2436a-208">1</span></span> | <span data-ttu-id="2436a-209">14 </span><span class="sxs-lookup"><span data-stu-id="2436a-209">14</span></span> |
| <span data-ttu-id="2436a-210">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="2436a-210">Send to conversation</span></span> | <span data-ttu-id="2436a-211">2</span><span class="sxs-lookup"><span data-stu-id="2436a-211">2</span></span> | <span data-ttu-id="2436a-212">16 </span><span class="sxs-lookup"><span data-stu-id="2436a-212">16</span></span> |
| <span data-ttu-id="2436a-213">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="2436a-213">Create conversation</span></span> | <span data-ttu-id="2436a-214">1</span><span class="sxs-lookup"><span data-stu-id="2436a-214">1</span></span> | <span data-ttu-id="2436a-215">14 </span><span class="sxs-lookup"><span data-stu-id="2436a-215">14</span></span> |
| <span data-ttu-id="2436a-216">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="2436a-216">Create conversation</span></span> | <span data-ttu-id="2436a-217">2</span><span class="sxs-lookup"><span data-stu-id="2436a-217">2</span></span> | <span data-ttu-id="2436a-218">16 </span><span class="sxs-lookup"><span data-stu-id="2436a-218">16</span></span> |
| <span data-ttu-id="2436a-219">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="2436a-219">Create conversation</span></span>| <span data-ttu-id="2436a-220">1</span><span class="sxs-lookup"><span data-stu-id="2436a-220">1</span></span> | <span data-ttu-id="2436a-221">14 </span><span class="sxs-lookup"><span data-stu-id="2436a-221">14</span></span> |
| <span data-ttu-id="2436a-222">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="2436a-222">Create conversation</span></span>| <span data-ttu-id="2436a-223">2</span><span class="sxs-lookup"><span data-stu-id="2436a-223">2</span></span> | <span data-ttu-id="2436a-224">16 </span><span class="sxs-lookup"><span data-stu-id="2436a-224">16</span></span> |
| <span data-ttu-id="2436a-225">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="2436a-225">Get conversation members</span></span>| <span data-ttu-id="2436a-226">1</span><span class="sxs-lookup"><span data-stu-id="2436a-226">1</span></span> | <span data-ttu-id="2436a-227">28</span><span class="sxs-lookup"><span data-stu-id="2436a-227">28</span></span> |
| <span data-ttu-id="2436a-228">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="2436a-228">Get conversation members</span></span>| <span data-ttu-id="2436a-229">2</span><span class="sxs-lookup"><span data-stu-id="2436a-229">2</span></span> | <span data-ttu-id="2436a-230">32</span><span class="sxs-lookup"><span data-stu-id="2436a-230">32</span></span> |
| <span data-ttu-id="2436a-231">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="2436a-231">Get conversations</span></span> | <span data-ttu-id="2436a-232">1</span><span class="sxs-lookup"><span data-stu-id="2436a-232">1</span></span> | <span data-ttu-id="2436a-233">28</span><span class="sxs-lookup"><span data-stu-id="2436a-233">28</span></span> |
| <span data-ttu-id="2436a-234">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="2436a-234">Get conversations</span></span> | <span data-ttu-id="2436a-235">2</span><span class="sxs-lookup"><span data-stu-id="2436a-235">2</span></span> | <span data-ttu-id="2436a-236">32</span><span class="sxs-lookup"><span data-stu-id="2436a-236">32</span></span> |

## <a name="next-step"></a><span data-ttu-id="2436a-237">次の手順</span><span class="sxs-lookup"><span data-stu-id="2436a-237">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2436a-238">通話と会議ボット</span><span class="sxs-lookup"><span data-stu-id="2436a-238">Calls and meetings bots</span></span>](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

