---
title: Teams でレートを制限してボットを最適化する
description: Microsoft Teams のレート制限とベスト プラクティス
ms.topic: conceptual
keywords: Teams ボットのレート制限
ms.openlocfilehash: 690d09e4a3b611c024f32d3776ca73e42d63ee7f
ms.sourcegitcommit: 35bc2a31b92f3f7c6524373108f095a870d9ad09
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "51922504"
---
# <a name="optimize-your-bot-with-rate-limiting-in-teams"></a><span data-ttu-id="8f2b3-104">Teams でレートを制限してボットを最適化する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-104">Optimize your bot with rate limiting in Teams</span></span>

<span data-ttu-id="8f2b3-105">レート制限は、メッセージを特定の最大頻度に制限する方法です。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-105">Rate limiting is a method to limit messages to a certain maximum frequency.</span></span> <span data-ttu-id="8f2b3-106">一般的な原則として、アプリケーションは投稿するメッセージの数を個々のチャットまたはチャネルの会話に制限する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-106">As a general principle, your application must limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="8f2b3-107">これにより、最適なエクスペリエンスが確保され、メッセージがユーザーにスパムとして表示されません。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-107">This ensures an optimal experience and messages do not appear as spam to your users.</span></span>

<span data-ttu-id="8f2b3-108">Microsoft Teams とそのユーザーを保護するために、ボット API は受信要求のレート制限を提供します。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-108">To protect Microsoft Teams and its users, the bot APIs provide a rate limit for incoming requests.</span></span> <span data-ttu-id="8f2b3-109">この制限を超えるアプリは、エラー状態 `HTTP 429 Too Many Requests` を受け取る。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-109">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="8f2b3-110">すべての要求は、メッセージの送信、チャネル列挙、名簿フェッチなど、同じレート制限ポリシーの対象です。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-110">All requests are subject to the same rate limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="8f2b3-111">レート制限の正確な値は変更される可能性があります。API が返される場合、アプリケーションは適切なバックオフ動作を実装する必要があります `HTTP 429 Too Many Requests` 。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-111">As the exact values of rate limits are subject to change, your application must implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handle-rate-limits"></a><span data-ttu-id="8f2b3-112">レート制限の処理</span><span class="sxs-lookup"><span data-stu-id="8f2b3-112">Handle rate limits</span></span>

<span data-ttu-id="8f2b3-113">ボット ビルダー SDK 操作を発行する場合は、状態コードを処理 `Microsoft.Rest.HttpOperationException` して確認できます。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-113">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

<span data-ttu-id="8f2b3-114">次のコードは、レート制限の処理例を示しています。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-114">The following code shows an example of handling rate limits:</span></span>

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

<span data-ttu-id="8f2b3-115">ボットのレート制限を処理した後、指数バックオフを `HTTP 429` 使用して応答を処理できます。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-115">After you handle rate limits for bots, you can handle `HTTP 429` responses using an exponential backoff.</span></span>

## <a name="handle-http-429-responses"></a><span data-ttu-id="8f2b3-116">応答 `HTTP 429` の処理</span><span class="sxs-lookup"><span data-stu-id="8f2b3-116">Handle `HTTP 429` responses</span></span>

<span data-ttu-id="8f2b3-117">一般に、応答を受信しないように、簡単な予防措置を講じ `HTTP 429` なければならない。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-117">In general, you must take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="8f2b3-118">たとえば、同じ個人またはチャネルの会話に対して複数の要求を発行しないようにします。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-118">For example, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="8f2b3-119">代わりに、API 要求のバッチを作成します。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-119">Instead, create a batch of the API requests.</span></span>

<span data-ttu-id="8f2b3-120">ランダムなジッターで指数バックオフを使用する方法は、429 を処理するための推奨される方法です。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-120">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="8f2b3-121">これにより、複数の要求が再試行時に競合を発生しない。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-121">This ensures that multiple requests do not introduce collisions on retries.</span></span>

<span data-ttu-id="8f2b3-122">応答を `HTTP 429` 処理した後、一時的な例外を検出する例を確認できます。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-122">After you handle `HTTP 429` responses, you can go through the example for detecting transient exceptions.</span></span>

## <a name="detect-transient-exceptions-example"></a><span data-ttu-id="8f2b3-123">一時的な例外の検出の例</span><span class="sxs-lookup"><span data-stu-id="8f2b3-123">Detect transient exceptions example</span></span>

<span data-ttu-id="8f2b3-124">次のコードは、一時的な障害処理アプリケーション ブロックを使用して指数バックオフを使用する例を示しています。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-124">The following code shows an example of using exponential backoff using the transient fault handling application block:</span></span>

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

<span data-ttu-id="8f2b3-125">一時的な障害処理を使用して、バックオフと再試行 [を実行できます](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-125">You can perform backoff and retries using [transient fault handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="8f2b3-126">NuGet パッケージの取得とインストールに関するガイドラインについては、「一時的な障害処理アプリケーション ブロックをソリューションに追加する [」を参照してください](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-126">For guidelines on obtaining and installing the NuGet package, see [adding the transient fault handling application block to your solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span></span> <span data-ttu-id="8f2b3-127">一時的な [障害処理も参照してください](/azure/architecture/best-practices/transient-faults)。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-127">See also [transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

<span data-ttu-id="8f2b3-128">一時的な例外を検出する例を実行した後、指数バックオフの例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-128">After you go through the example for detecting transient exceptions, go through the exponential backoff example.</span></span> <span data-ttu-id="8f2b3-129">エラー時に再試行する代わりに指数バックオフを使用できます。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-129">You can use exponential backoff instead of retrying on failures.</span></span>

## <a name="backoff-example"></a><span data-ttu-id="8f2b3-130">バックオフの例</span><span class="sxs-lookup"><span data-stu-id="8f2b3-130">Backoff example</span></span>

<span data-ttu-id="8f2b3-131">レート制限の検出に加えて、指数バックオフも実行できます。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-131">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

<span data-ttu-id="8f2b3-132">次のコードは、指数バックオフの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-132">The following code shows an example of exponential backoff:</span></span>

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

<span data-ttu-id="8f2b3-133">また、このセクションで説明 `System.Action` する再試行ポリシーを使用してメソッドの実行を実行できます。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-133">You can also perform a `System.Action` method execution with the retry policy described in this section.</span></span> <span data-ttu-id="8f2b3-134">参照されるライブラリでは、固定間隔または線形バックオフ メカニズムを指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-134">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="8f2b3-135">値と戦略を構成ファイルに格納して、実行時に値を微調整および調整します。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-135">Store the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="8f2b3-136">詳細については、「再試行パターン [」を参照してください](/azure/architecture/patterns/retry)。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-136">For more information, see [retry patterns](/azure/architecture/patterns/retry).</span></span>

<span data-ttu-id="8f2b3-137">スレッドごとのボットごとの制限を使用して、レート制限を処理できます。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-137">You can also handle rate limit using the per bot per thread limit.</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="8f2b3-138">スレッドごとのボットごとの制限</span><span class="sxs-lookup"><span data-stu-id="8f2b3-138">Per bot per thread limit</span></span>

<span data-ttu-id="8f2b3-139">スレッドごとのボットごとの制限は、ボットが 1 回の会話で生成できるトラフィックを制御します。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-139">The per bot per thread limit controls the traffic that a bot is allowed to generate in a single conversation.</span></span> <span data-ttu-id="8f2b3-140">ボットとユーザー、グループ チャット、またはチーム内のチャネル間の会話は 1:1 です。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-140">A conversation is 1:1 between bot and user, a group chat, or a channel in a team.</span></span> <span data-ttu-id="8f2b3-141">したがって、アプリケーションが各ユーザーにボット メッセージを 1 つ送信しても、スレッドの制限は調整されません。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-141">So, if the application sends one bot message to each user, the thread limit does not throttle.</span></span>

>[!NOTE]
> * <span data-ttu-id="8f2b3-142">3600 秒と 1800 の操作のスレッド制限は、複数のボット メッセージが 1 人のユーザーに送信される場合にのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-142">The thread limit of 3600 seconds and 1800 operations applies only if multiple bot messages are sent to a single user.</span></span> 
> * <span data-ttu-id="8f2b3-143">テナントごとのアプリごとのグローバル制限は、1 秒あたり 30 要求 (RPS) です。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-143">The global limit per app per tenant is 30 Requests Per Second (RPS).</span></span> <span data-ttu-id="8f2b3-144">したがって、1 秒あたりのボット メッセージの総数がスレッドの制限を超えなけってはいけない。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-144">Hence, the total number of bot messages per second must not cross the thread limit.</span></span>
> * <span data-ttu-id="8f2b3-145">サービス レベルでのメッセージの分割は、予想される RPS よりも高くなります。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-145">Message splitting at the service level results in higher than expected RPS.</span></span> <span data-ttu-id="8f2b3-146">制限への近付きが懸念される場合は、バックオフ戦略を [実装する必要があります](#backoff-example)。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-146">If you are concerned about approaching the limits, you must implement the [backoff strategy](#backoff-example).</span></span> <span data-ttu-id="8f2b3-147">このセクションで提供される値は、見積もり専用です。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-147">The values provided in this section are for estimation only.</span></span>

<span data-ttu-id="8f2b3-148">次の表に、スレッドごとのボットごとの制限を示します。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-148">The following table provides the per bot per thread limits:</span></span>

| <span data-ttu-id="8f2b3-149">シナリオ</span><span class="sxs-lookup"><span data-stu-id="8f2b3-149">Scenario</span></span> | <span data-ttu-id="8f2b3-150">期間 (秒)</span><span class="sxs-lookup"><span data-stu-id="8f2b3-150">Time period in seconds</span></span> | <span data-ttu-id="8f2b3-151">許可される操作の最大数</span><span class="sxs-lookup"><span data-stu-id="8f2b3-151">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8f2b3-152">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-152">Send to conversation</span></span> | <span data-ttu-id="8f2b3-153">1</span><span class="sxs-lookup"><span data-stu-id="8f2b3-153">1</span></span> | <span data-ttu-id="8f2b3-154">7</span><span class="sxs-lookup"><span data-stu-id="8f2b3-154">7</span></span> |
| <span data-ttu-id="8f2b3-155">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-155">Send to conversation</span></span> | <span data-ttu-id="8f2b3-156">2</span><span class="sxs-lookup"><span data-stu-id="8f2b3-156">2</span></span> | <span data-ttu-id="8f2b3-157">8</span><span class="sxs-lookup"><span data-stu-id="8f2b3-157">8</span></span> |
| <span data-ttu-id="8f2b3-158">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-158">Send to conversation</span></span> | <span data-ttu-id="8f2b3-159">30</span><span class="sxs-lookup"><span data-stu-id="8f2b3-159">30</span></span> | <span data-ttu-id="8f2b3-160">60</span><span class="sxs-lookup"><span data-stu-id="8f2b3-160">60</span></span> |
| <span data-ttu-id="8f2b3-161">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-161">Send to conversation</span></span> | <span data-ttu-id="8f2b3-162">3600</span><span class="sxs-lookup"><span data-stu-id="8f2b3-162">3600</span></span> | <span data-ttu-id="8f2b3-163">1800</span><span class="sxs-lookup"><span data-stu-id="8f2b3-163">1800</span></span> |
| <span data-ttu-id="8f2b3-164">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-164">Create conversation</span></span> | <span data-ttu-id="8f2b3-165">1</span><span class="sxs-lookup"><span data-stu-id="8f2b3-165">1</span></span> | <span data-ttu-id="8f2b3-166">7</span><span class="sxs-lookup"><span data-stu-id="8f2b3-166">7</span></span> |
| <span data-ttu-id="8f2b3-167">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-167">Create conversation</span></span> | <span data-ttu-id="8f2b3-168">2</span><span class="sxs-lookup"><span data-stu-id="8f2b3-168">2</span></span> | <span data-ttu-id="8f2b3-169">8</span><span class="sxs-lookup"><span data-stu-id="8f2b3-169">8</span></span> |
| <span data-ttu-id="8f2b3-170">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-170">Create conversation</span></span> | <span data-ttu-id="8f2b3-171">30</span><span class="sxs-lookup"><span data-stu-id="8f2b3-171">30</span></span> | <span data-ttu-id="8f2b3-172">60</span><span class="sxs-lookup"><span data-stu-id="8f2b3-172">60</span></span> |
| <span data-ttu-id="8f2b3-173">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-173">Create conversation</span></span> | <span data-ttu-id="8f2b3-174">3600</span><span class="sxs-lookup"><span data-stu-id="8f2b3-174">3600</span></span> | <span data-ttu-id="8f2b3-175">1800</span><span class="sxs-lookup"><span data-stu-id="8f2b3-175">1800</span></span> |
| <span data-ttu-id="8f2b3-176">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-176">Get conversation members</span></span>| <span data-ttu-id="8f2b3-177">1</span><span class="sxs-lookup"><span data-stu-id="8f2b3-177">1</span></span> | <span data-ttu-id="8f2b3-178">14 </span><span class="sxs-lookup"><span data-stu-id="8f2b3-178">14</span></span> |
| <span data-ttu-id="8f2b3-179">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-179">Get conversation members</span></span>| <span data-ttu-id="8f2b3-180">2</span><span class="sxs-lookup"><span data-stu-id="8f2b3-180">2</span></span> | <span data-ttu-id="8f2b3-181">16 </span><span class="sxs-lookup"><span data-stu-id="8f2b3-181">16</span></span> |
| <span data-ttu-id="8f2b3-182">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-182">Get conversation members</span></span>| <span data-ttu-id="8f2b3-183">30</span><span class="sxs-lookup"><span data-stu-id="8f2b3-183">30</span></span> | <span data-ttu-id="8f2b3-184">120</span><span class="sxs-lookup"><span data-stu-id="8f2b3-184">120</span></span> |
| <span data-ttu-id="8f2b3-185">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-185">Get conversation members</span></span>| <span data-ttu-id="8f2b3-186">3600</span><span class="sxs-lookup"><span data-stu-id="8f2b3-186">3600</span></span> | <span data-ttu-id="8f2b3-187">3600</span><span class="sxs-lookup"><span data-stu-id="8f2b3-187">3600</span></span> |
| <span data-ttu-id="8f2b3-188">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-188">Get conversations</span></span> | <span data-ttu-id="8f2b3-189">1</span><span class="sxs-lookup"><span data-stu-id="8f2b3-189">1</span></span> | <span data-ttu-id="8f2b3-190">14 </span><span class="sxs-lookup"><span data-stu-id="8f2b3-190">14</span></span> |
| <span data-ttu-id="8f2b3-191">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-191">Get conversations</span></span> | <span data-ttu-id="8f2b3-192">2</span><span class="sxs-lookup"><span data-stu-id="8f2b3-192">2</span></span> | <span data-ttu-id="8f2b3-193">16 </span><span class="sxs-lookup"><span data-stu-id="8f2b3-193">16</span></span> |
| <span data-ttu-id="8f2b3-194">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-194">Get conversations</span></span> | <span data-ttu-id="8f2b3-195">30</span><span class="sxs-lookup"><span data-stu-id="8f2b3-195">30</span></span> | <span data-ttu-id="8f2b3-196">120</span><span class="sxs-lookup"><span data-stu-id="8f2b3-196">120</span></span> |
| <span data-ttu-id="8f2b3-197">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-197">Get conversations</span></span> | <span data-ttu-id="8f2b3-198">3600</span><span class="sxs-lookup"><span data-stu-id="8f2b3-198">3600</span></span> | <span data-ttu-id="8f2b3-199">3600</span><span class="sxs-lookup"><span data-stu-id="8f2b3-199">3600</span></span> |

>[!NOTE]
> <span data-ttu-id="8f2b3-200">以前のバージョンと `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` API は非推奨です。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-200">Previous versions of `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs are being deprecated.</span></span> <span data-ttu-id="8f2b3-201">1 分あたり 5 つの要求に調整され、チームごとに最大 10K のメンバーが返されます。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-201">They are throttled to five requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="8f2b3-202">ボット フレームワーク SDK と、ページ分割された最新の API エンドポイントを使用するコードを更新するには、「チームおよびチャット メンバーのボット API の変更」 [を参照してください](../../resources/team-chat-member-api-changes.md)。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-202">To update your Bot Framework SDK and the code to use the latest paginated API endpoints, see [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span></span>

<span data-ttu-id="8f2b3-203">また、すべてのボットのスレッドごとの制限を使用して、レート制限を処理できます。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-203">You can also handle rate limit using the per thread limit for all bots.</span></span>

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="8f2b3-204">すべてのボットのスレッドごとの制限</span><span class="sxs-lookup"><span data-stu-id="8f2b3-204">Per thread limit for all bots</span></span>

<span data-ttu-id="8f2b3-205">すべてのボットのスレッドごとの制限は、すべてのボットが 1 回の会話で生成できるトラフィックを制御します。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-205">The per thread limit for all bots controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="8f2b3-206">ここでの会話は、ボットとユーザー、グループ チャット、またはチーム内のチャネルの間で 1:1 です。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-206">A conversation here is 1:1 between bot and user, a group chat, or a channel in a team.</span></span>

<span data-ttu-id="8f2b3-207">次の表に、すべてのボットのスレッドごとの制限を示します。</span><span class="sxs-lookup"><span data-stu-id="8f2b3-207">The following table provides the per thread limit for all bots:</span></span>

| <span data-ttu-id="8f2b3-208">シナリオ</span><span class="sxs-lookup"><span data-stu-id="8f2b3-208">Scenario</span></span> | <span data-ttu-id="8f2b3-209">期間 (秒)</span><span class="sxs-lookup"><span data-stu-id="8f2b3-209">Time period in seconds</span></span> | <span data-ttu-id="8f2b3-210">許可される操作の最大数</span><span class="sxs-lookup"><span data-stu-id="8f2b3-210">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8f2b3-211">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-211">Send to conversation</span></span> | <span data-ttu-id="8f2b3-212">1</span><span class="sxs-lookup"><span data-stu-id="8f2b3-212">1</span></span> | <span data-ttu-id="8f2b3-213">14 </span><span class="sxs-lookup"><span data-stu-id="8f2b3-213">14</span></span> |
| <span data-ttu-id="8f2b3-214">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-214">Send to conversation</span></span> | <span data-ttu-id="8f2b3-215">2</span><span class="sxs-lookup"><span data-stu-id="8f2b3-215">2</span></span> | <span data-ttu-id="8f2b3-216">16 </span><span class="sxs-lookup"><span data-stu-id="8f2b3-216">16</span></span> |
| <span data-ttu-id="8f2b3-217">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-217">Create conversation</span></span> | <span data-ttu-id="8f2b3-218">1</span><span class="sxs-lookup"><span data-stu-id="8f2b3-218">1</span></span> | <span data-ttu-id="8f2b3-219">14 </span><span class="sxs-lookup"><span data-stu-id="8f2b3-219">14</span></span> |
| <span data-ttu-id="8f2b3-220">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-220">Create conversation</span></span> | <span data-ttu-id="8f2b3-221">2</span><span class="sxs-lookup"><span data-stu-id="8f2b3-221">2</span></span> | <span data-ttu-id="8f2b3-222">16 </span><span class="sxs-lookup"><span data-stu-id="8f2b3-222">16</span></span> |
| <span data-ttu-id="8f2b3-223">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-223">Create conversation</span></span>| <span data-ttu-id="8f2b3-224">1</span><span class="sxs-lookup"><span data-stu-id="8f2b3-224">1</span></span> | <span data-ttu-id="8f2b3-225">14 </span><span class="sxs-lookup"><span data-stu-id="8f2b3-225">14</span></span> |
| <span data-ttu-id="8f2b3-226">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-226">Create conversation</span></span>| <span data-ttu-id="8f2b3-227">2</span><span class="sxs-lookup"><span data-stu-id="8f2b3-227">2</span></span> | <span data-ttu-id="8f2b3-228">16 </span><span class="sxs-lookup"><span data-stu-id="8f2b3-228">16</span></span> |
| <span data-ttu-id="8f2b3-229">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-229">Get conversation members</span></span>| <span data-ttu-id="8f2b3-230">1</span><span class="sxs-lookup"><span data-stu-id="8f2b3-230">1</span></span> | <span data-ttu-id="8f2b3-231">28</span><span class="sxs-lookup"><span data-stu-id="8f2b3-231">28</span></span> |
| <span data-ttu-id="8f2b3-232">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-232">Get conversation members</span></span>| <span data-ttu-id="8f2b3-233">2</span><span class="sxs-lookup"><span data-stu-id="8f2b3-233">2</span></span> | <span data-ttu-id="8f2b3-234">32</span><span class="sxs-lookup"><span data-stu-id="8f2b3-234">32</span></span> |
| <span data-ttu-id="8f2b3-235">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-235">Get conversations</span></span> | <span data-ttu-id="8f2b3-236">1</span><span class="sxs-lookup"><span data-stu-id="8f2b3-236">1</span></span> | <span data-ttu-id="8f2b3-237">28</span><span class="sxs-lookup"><span data-stu-id="8f2b3-237">28</span></span> |
| <span data-ttu-id="8f2b3-238">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="8f2b3-238">Get conversations</span></span> | <span data-ttu-id="8f2b3-239">2</span><span class="sxs-lookup"><span data-stu-id="8f2b3-239">2</span></span> | <span data-ttu-id="8f2b3-240">32</span><span class="sxs-lookup"><span data-stu-id="8f2b3-240">32</span></span> |

## <a name="next-step"></a><span data-ttu-id="8f2b3-241">次の手順</span><span class="sxs-lookup"><span data-stu-id="8f2b3-241">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8f2b3-242">通話と会議のボット</span><span class="sxs-lookup"><span data-stu-id="8f2b3-242">Calls and meetings bots</span></span>](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

