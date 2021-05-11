---
title: Teams でレートを制限してボットを最適化する
description: データのレート制限とベスト プラクティスMicrosoft Teams
ms.topic: conceptual
localization_priority: Normal
keywords: Teams ボットのレート制限
ms.openlocfilehash: 3b8f80efa50d2fbf44162aec13994b747b9bd7ac
ms.sourcegitcommit: 60561c7cd189c9d6fa5e09e0f2b6c24476f2dff5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2021
ms.locfileid: "52230961"
---
# <a name="optimize-your-bot-with-rate-limiting-in-teams"></a><span data-ttu-id="c0b0d-104">Teams でレートを制限してボットを最適化する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-104">Optimize your bot with rate limiting in Teams</span></span>

<span data-ttu-id="c0b0d-105">レート制限は、メッセージを特定の最大頻度に制限する方法です。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-105">Rate limiting is a method to limit messages to a certain maximum frequency.</span></span> <span data-ttu-id="c0b0d-106">一般的な原則として、アプリケーションは投稿するメッセージの数を個々のチャットまたはチャネルの会話に制限する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-106">As a general principle, your application must limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="c0b0d-107">これにより、最適なエクスペリエンスが確保され、メッセージがユーザーにスパムとして表示されません。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-107">This ensures an optimal experience and messages do not appear as spam to your users.</span></span>

<span data-ttu-id="c0b0d-108">ボット API はMicrosoft Teamsユーザーを保護するために、受信要求のレート制限を提供します。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-108">To protect Microsoft Teams and its users, the bot APIs provide a rate limit for incoming requests.</span></span> <span data-ttu-id="c0b0d-109">この制限を超えるアプリは、エラー状態 `HTTP 429 Too Many Requests` を受け取る。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-109">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="c0b0d-110">すべての要求は、メッセージの送信、チャネル列挙、名簿フェッチなど、同じレート制限ポリシーの対象です。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-110">All requests are subject to the same rate limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="c0b0d-111">レート制限の正確な値は変更される可能性があります。API が返される場合、アプリケーションは適切なバックオフ動作を実装する必要があります `HTTP 429 Too Many Requests` 。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-111">As the exact values of rate limits are subject to change, your application must implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handle-rate-limits"></a><span data-ttu-id="c0b0d-112">レート制限の処理</span><span class="sxs-lookup"><span data-stu-id="c0b0d-112">Handle rate limits</span></span>

<span data-ttu-id="c0b0d-113">ボット ビルダー SDK 操作を発行する場合は、状態コードを処理 `Microsoft.Rest.HttpOperationException` して確認できます。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-113">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

<span data-ttu-id="c0b0d-114">次のコードは、レート制限の処理例を示しています。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-114">The following code shows an example of handling rate limits:</span></span>

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

<span data-ttu-id="c0b0d-115">ボットのレート制限を処理した後、指数バックオフを `HTTP 429` 使用して応答を処理できます。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-115">After you handle rate limits for bots, you can handle `HTTP 429` responses using an exponential backoff.</span></span>

## <a name="handle-http-429-responses"></a><span data-ttu-id="c0b0d-116">応答 `HTTP 429` の処理</span><span class="sxs-lookup"><span data-stu-id="c0b0d-116">Handle `HTTP 429` responses</span></span>

<span data-ttu-id="c0b0d-117">一般に、応答を受信しないように、簡単な予防措置を講じ `HTTP 429` なければならない。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-117">In general, you must take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="c0b0d-118">たとえば、同じ個人またはチャネルの会話に対して複数の要求を発行しないようにします。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-118">For example, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="c0b0d-119">代わりに、API 要求のバッチを作成します。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-119">Instead, create a batch of the API requests.</span></span>

<span data-ttu-id="c0b0d-120">ランダムなジッターで指数バックオフを使用する方法は、429 を処理するための推奨される方法です。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-120">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="c0b0d-121">これにより、複数の要求が再試行時に競合を発生しない。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-121">This ensures that multiple requests do not introduce collisions on retries.</span></span>

<span data-ttu-id="c0b0d-122">応答を `HTTP 429` 処理した後、一時的な例外を検出する例を確認できます。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-122">After you handle `HTTP 429` responses, you can go through the example for detecting transient exceptions.</span></span>

> [!NOTE]
> <span data-ttu-id="c0b0d-123">エラー コード **429** の再入力に加えて、エラー コード **412、502、\*\*\*\*および 504** も再試行する必要があります。 </span><span class="sxs-lookup"><span data-stu-id="c0b0d-123">In addition to retyring error code **429**, error codes **412**, **502**, and **504** must also be retried.</span></span>

## <a name="detect-transient-exceptions-example"></a><span data-ttu-id="c0b0d-124">一時的な例外の検出の例</span><span class="sxs-lookup"><span data-stu-id="c0b0d-124">Detect transient exceptions example</span></span>

<span data-ttu-id="c0b0d-125">次のコードは、一時的な障害処理アプリケーション ブロックを使用して指数バックオフを使用する例を示しています。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-125">The following code shows an example of using exponential backoff using the transient fault handling application block:</span></span>

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

<span data-ttu-id="c0b0d-126">一時的な障害処理を使用して、バックオフと再試行 [を実行できます](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-126">You can perform backoff and retries using [transient fault handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="c0b0d-127">NuGet パッケージの取得とインストールに関するガイドラインについては、「一時的な障害処理アプリケーション ブロックをソリューションに追加する[」を参照してください](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-127">For guidelines on obtaining and installing the NuGet package, see [adding the transient fault handling application block to your solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span></span> <span data-ttu-id="c0b0d-128">一時的な [障害処理も参照してください](/azure/architecture/best-practices/transient-faults)。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-128">See also [transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

<span data-ttu-id="c0b0d-129">一時的な例外を検出する例を実行した後、指数バックオフの例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-129">After you go through the example for detecting transient exceptions, go through the exponential backoff example.</span></span> <span data-ttu-id="c0b0d-130">エラー時に再試行する代わりに指数バックオフを使用できます。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-130">You can use exponential backoff instead of retrying on failures.</span></span>

## <a name="backoff-example"></a><span data-ttu-id="c0b0d-131">バックオフの例</span><span class="sxs-lookup"><span data-stu-id="c0b0d-131">Backoff example</span></span>

<span data-ttu-id="c0b0d-132">レート制限の検出に加えて、指数バックオフも実行できます。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-132">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

<span data-ttu-id="c0b0d-133">次のコードは、指数バックオフの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-133">The following code shows an example of exponential backoff:</span></span>

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

<span data-ttu-id="c0b0d-134">また、このセクションで説明 `System.Action` する再試行ポリシーを使用してメソッドの実行を実行できます。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-134">You can also perform a `System.Action` method execution with the retry policy described in this section.</span></span> <span data-ttu-id="c0b0d-135">参照されるライブラリでは、固定間隔または線形バックオフ メカニズムを指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-135">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="c0b0d-136">値と戦略を構成ファイルに格納して、実行時に値を微調整および調整します。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-136">Store the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="c0b0d-137">詳細については、「再試行パターン [」を参照してください](/azure/architecture/patterns/retry)。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-137">For more information, see [retry patterns](/azure/architecture/patterns/retry).</span></span>

<span data-ttu-id="c0b0d-138">スレッドごとのボットごとの制限を使用して、レート制限を処理できます。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-138">You can also handle rate limit using the per bot per thread limit.</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="c0b0d-139">スレッドごとのボットごとの制限</span><span class="sxs-lookup"><span data-stu-id="c0b0d-139">Per bot per thread limit</span></span>

<span data-ttu-id="c0b0d-140">スレッドごとのボットごとの制限は、ボットが 1 回の会話で生成できるトラフィックを制御します。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-140">The per bot per thread limit controls the traffic that a bot is allowed to generate in a single conversation.</span></span> <span data-ttu-id="c0b0d-141">ボットとユーザー、グループ チャット、またはチーム内のチャネル間の会話は 1:1 です。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-141">A conversation is 1:1 between bot and user, a group chat, or a channel in a team.</span></span> <span data-ttu-id="c0b0d-142">したがって、アプリケーションが各ユーザーにボット メッセージを 1 つ送信しても、スレッドの制限は調整されません。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-142">So, if the application sends one bot message to each user, the thread limit does not throttle.</span></span>

>[!NOTE]
> * <span data-ttu-id="c0b0d-143">3600 秒と 1800 の操作のスレッド制限は、複数のボット メッセージが 1 人のユーザーに送信される場合にのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-143">The thread limit of 3600 seconds and 1800 operations applies only if multiple bot messages are sent to a single user.</span></span> 
> * <span data-ttu-id="c0b0d-144">テナントごとのアプリごとのグローバル制限は、1 秒あたり 50 要求 (RPS) です。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-144">The global limit per app per tenant is 50 Requests Per Second (RPS).</span></span> <span data-ttu-id="c0b0d-145">したがって、1 秒あたりのボット メッセージの総数がスレッドの制限を超えなけってはいけない。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-145">Hence, the total number of bot messages per second must not cross the thread limit.</span></span>
> * <span data-ttu-id="c0b0d-146">サービス レベルでのメッセージの分割は、予想される RPS よりも高くなります。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-146">Message splitting at the service level results in higher than expected RPS.</span></span> <span data-ttu-id="c0b0d-147">制限への近付きが懸念される場合は、バックオフ戦略を [実装する必要があります](#backoff-example)。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-147">If you are concerned about approaching the limits, you must implement the [backoff strategy](#backoff-example).</span></span> <span data-ttu-id="c0b0d-148">このセクションで提供される値は、見積もり専用です。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-148">The values provided in this section are for estimation only.</span></span>

<span data-ttu-id="c0b0d-149">次の表に、スレッドごとのボットごとの制限を示します。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-149">The following table provides the per bot per thread limits:</span></span>

| <span data-ttu-id="c0b0d-150">シナリオ</span><span class="sxs-lookup"><span data-stu-id="c0b0d-150">Scenario</span></span> | <span data-ttu-id="c0b0d-151">期間 (秒)</span><span class="sxs-lookup"><span data-stu-id="c0b0d-151">Time period in seconds</span></span> | <span data-ttu-id="c0b0d-152">許可される操作の最大数</span><span class="sxs-lookup"><span data-stu-id="c0b0d-152">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c0b0d-153">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-153">Send to conversation</span></span> | <span data-ttu-id="c0b0d-154">1</span><span class="sxs-lookup"><span data-stu-id="c0b0d-154">1</span></span> | <span data-ttu-id="c0b0d-155">7</span><span class="sxs-lookup"><span data-stu-id="c0b0d-155">7</span></span> |
| <span data-ttu-id="c0b0d-156">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-156">Send to conversation</span></span> | <span data-ttu-id="c0b0d-157">2</span><span class="sxs-lookup"><span data-stu-id="c0b0d-157">2</span></span> | <span data-ttu-id="c0b0d-158">8</span><span class="sxs-lookup"><span data-stu-id="c0b0d-158">8</span></span> |
| <span data-ttu-id="c0b0d-159">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-159">Send to conversation</span></span> | <span data-ttu-id="c0b0d-160">30</span><span class="sxs-lookup"><span data-stu-id="c0b0d-160">30</span></span> | <span data-ttu-id="c0b0d-161">60</span><span class="sxs-lookup"><span data-stu-id="c0b0d-161">60</span></span> |
| <span data-ttu-id="c0b0d-162">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-162">Send to conversation</span></span> | <span data-ttu-id="c0b0d-163">3600</span><span class="sxs-lookup"><span data-stu-id="c0b0d-163">3600</span></span> | <span data-ttu-id="c0b0d-164">1800</span><span class="sxs-lookup"><span data-stu-id="c0b0d-164">1800</span></span> |
| <span data-ttu-id="c0b0d-165">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-165">Create conversation</span></span> | <span data-ttu-id="c0b0d-166">1</span><span class="sxs-lookup"><span data-stu-id="c0b0d-166">1</span></span> | <span data-ttu-id="c0b0d-167">7</span><span class="sxs-lookup"><span data-stu-id="c0b0d-167">7</span></span> |
| <span data-ttu-id="c0b0d-168">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-168">Create conversation</span></span> | <span data-ttu-id="c0b0d-169">2</span><span class="sxs-lookup"><span data-stu-id="c0b0d-169">2</span></span> | <span data-ttu-id="c0b0d-170">8</span><span class="sxs-lookup"><span data-stu-id="c0b0d-170">8</span></span> |
| <span data-ttu-id="c0b0d-171">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-171">Create conversation</span></span> | <span data-ttu-id="c0b0d-172">30</span><span class="sxs-lookup"><span data-stu-id="c0b0d-172">30</span></span> | <span data-ttu-id="c0b0d-173">60</span><span class="sxs-lookup"><span data-stu-id="c0b0d-173">60</span></span> |
| <span data-ttu-id="c0b0d-174">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-174">Create conversation</span></span> | <span data-ttu-id="c0b0d-175">3600</span><span class="sxs-lookup"><span data-stu-id="c0b0d-175">3600</span></span> | <span data-ttu-id="c0b0d-176">1800</span><span class="sxs-lookup"><span data-stu-id="c0b0d-176">1800</span></span> |
| <span data-ttu-id="c0b0d-177">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-177">Get conversation members</span></span>| <span data-ttu-id="c0b0d-178">1</span><span class="sxs-lookup"><span data-stu-id="c0b0d-178">1</span></span> | <span data-ttu-id="c0b0d-179">14 </span><span class="sxs-lookup"><span data-stu-id="c0b0d-179">14</span></span> |
| <span data-ttu-id="c0b0d-180">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-180">Get conversation members</span></span>| <span data-ttu-id="c0b0d-181">2</span><span class="sxs-lookup"><span data-stu-id="c0b0d-181">2</span></span> | <span data-ttu-id="c0b0d-182">16 </span><span class="sxs-lookup"><span data-stu-id="c0b0d-182">16</span></span> |
| <span data-ttu-id="c0b0d-183">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-183">Get conversation members</span></span>| <span data-ttu-id="c0b0d-184">30</span><span class="sxs-lookup"><span data-stu-id="c0b0d-184">30</span></span> | <span data-ttu-id="c0b0d-185">120</span><span class="sxs-lookup"><span data-stu-id="c0b0d-185">120</span></span> |
| <span data-ttu-id="c0b0d-186">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-186">Get conversation members</span></span>| <span data-ttu-id="c0b0d-187">3600</span><span class="sxs-lookup"><span data-stu-id="c0b0d-187">3600</span></span> | <span data-ttu-id="c0b0d-188">3600</span><span class="sxs-lookup"><span data-stu-id="c0b0d-188">3600</span></span> |
| <span data-ttu-id="c0b0d-189">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-189">Get conversations</span></span> | <span data-ttu-id="c0b0d-190">1</span><span class="sxs-lookup"><span data-stu-id="c0b0d-190">1</span></span> | <span data-ttu-id="c0b0d-191">14 </span><span class="sxs-lookup"><span data-stu-id="c0b0d-191">14</span></span> |
| <span data-ttu-id="c0b0d-192">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-192">Get conversations</span></span> | <span data-ttu-id="c0b0d-193">2</span><span class="sxs-lookup"><span data-stu-id="c0b0d-193">2</span></span> | <span data-ttu-id="c0b0d-194">16 </span><span class="sxs-lookup"><span data-stu-id="c0b0d-194">16</span></span> |
| <span data-ttu-id="c0b0d-195">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-195">Get conversations</span></span> | <span data-ttu-id="c0b0d-196">30</span><span class="sxs-lookup"><span data-stu-id="c0b0d-196">30</span></span> | <span data-ttu-id="c0b0d-197">120</span><span class="sxs-lookup"><span data-stu-id="c0b0d-197">120</span></span> |
| <span data-ttu-id="c0b0d-198">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-198">Get conversations</span></span> | <span data-ttu-id="c0b0d-199">3600</span><span class="sxs-lookup"><span data-stu-id="c0b0d-199">3600</span></span> | <span data-ttu-id="c0b0d-200">3600</span><span class="sxs-lookup"><span data-stu-id="c0b0d-200">3600</span></span> |

>[!NOTE]
> <span data-ttu-id="c0b0d-201">以前のバージョンと `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` API は非推奨です。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-201">Previous versions of `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs are being deprecated.</span></span> <span data-ttu-id="c0b0d-202">1 分あたり 5 つの要求に調整され、チームごとに最大 10K のメンバーが返されます。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-202">They are throttled to five requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="c0b0d-203">ボット フレームワーク SDK と、ページ分割された最新の API エンドポイントを使用するコードを更新するには、「チームおよびチャット メンバーのボット API の変更」 [を参照してください](../../resources/team-chat-member-api-changes.md)。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-203">To update your Bot Framework SDK and the code to use the latest paginated API endpoints, see [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span></span>

<span data-ttu-id="c0b0d-204">また、すべてのボットのスレッドごとの制限を使用して、レート制限を処理できます。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-204">You can also handle rate limit using the per thread limit for all bots.</span></span>

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="c0b0d-205">すべてのボットのスレッドごとの制限</span><span class="sxs-lookup"><span data-stu-id="c0b0d-205">Per thread limit for all bots</span></span>

<span data-ttu-id="c0b0d-206">すべてのボットのスレッドごとの制限は、すべてのボットが 1 回の会話で生成できるトラフィックを制御します。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-206">The per thread limit for all bots controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="c0b0d-207">ここでの会話は、ボットとユーザー、グループ チャット、またはチーム内のチャネルの間で 1:1 です。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-207">A conversation here is 1:1 between bot and user, a group chat, or a channel in a team.</span></span>

<span data-ttu-id="c0b0d-208">次の表に、すべてのボットのスレッドごとの制限を示します。</span><span class="sxs-lookup"><span data-stu-id="c0b0d-208">The following table provides the per thread limit for all bots:</span></span>

| <span data-ttu-id="c0b0d-209">シナリオ</span><span class="sxs-lookup"><span data-stu-id="c0b0d-209">Scenario</span></span> | <span data-ttu-id="c0b0d-210">期間 (秒)</span><span class="sxs-lookup"><span data-stu-id="c0b0d-210">Time period in seconds</span></span> | <span data-ttu-id="c0b0d-211">許可される操作の最大数</span><span class="sxs-lookup"><span data-stu-id="c0b0d-211">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c0b0d-212">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-212">Send to conversation</span></span> | <span data-ttu-id="c0b0d-213">1</span><span class="sxs-lookup"><span data-stu-id="c0b0d-213">1</span></span> | <span data-ttu-id="c0b0d-214">14 </span><span class="sxs-lookup"><span data-stu-id="c0b0d-214">14</span></span> |
| <span data-ttu-id="c0b0d-215">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-215">Send to conversation</span></span> | <span data-ttu-id="c0b0d-216">2</span><span class="sxs-lookup"><span data-stu-id="c0b0d-216">2</span></span> | <span data-ttu-id="c0b0d-217">16 </span><span class="sxs-lookup"><span data-stu-id="c0b0d-217">16</span></span> |
| <span data-ttu-id="c0b0d-218">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-218">Create conversation</span></span> | <span data-ttu-id="c0b0d-219">1</span><span class="sxs-lookup"><span data-stu-id="c0b0d-219">1</span></span> | <span data-ttu-id="c0b0d-220">14 </span><span class="sxs-lookup"><span data-stu-id="c0b0d-220">14</span></span> |
| <span data-ttu-id="c0b0d-221">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-221">Create conversation</span></span> | <span data-ttu-id="c0b0d-222">2</span><span class="sxs-lookup"><span data-stu-id="c0b0d-222">2</span></span> | <span data-ttu-id="c0b0d-223">16 </span><span class="sxs-lookup"><span data-stu-id="c0b0d-223">16</span></span> |
| <span data-ttu-id="c0b0d-224">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-224">Create conversation</span></span>| <span data-ttu-id="c0b0d-225">1</span><span class="sxs-lookup"><span data-stu-id="c0b0d-225">1</span></span> | <span data-ttu-id="c0b0d-226">14 </span><span class="sxs-lookup"><span data-stu-id="c0b0d-226">14</span></span> |
| <span data-ttu-id="c0b0d-227">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-227">Create conversation</span></span>| <span data-ttu-id="c0b0d-228">2</span><span class="sxs-lookup"><span data-stu-id="c0b0d-228">2</span></span> | <span data-ttu-id="c0b0d-229">16 </span><span class="sxs-lookup"><span data-stu-id="c0b0d-229">16</span></span> |
| <span data-ttu-id="c0b0d-230">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-230">Get conversation members</span></span>| <span data-ttu-id="c0b0d-231">1</span><span class="sxs-lookup"><span data-stu-id="c0b0d-231">1</span></span> | <span data-ttu-id="c0b0d-232">28</span><span class="sxs-lookup"><span data-stu-id="c0b0d-232">28</span></span> |
| <span data-ttu-id="c0b0d-233">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-233">Get conversation members</span></span>| <span data-ttu-id="c0b0d-234">2</span><span class="sxs-lookup"><span data-stu-id="c0b0d-234">2</span></span> | <span data-ttu-id="c0b0d-235">32</span><span class="sxs-lookup"><span data-stu-id="c0b0d-235">32</span></span> |
| <span data-ttu-id="c0b0d-236">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-236">Get conversations</span></span> | <span data-ttu-id="c0b0d-237">1</span><span class="sxs-lookup"><span data-stu-id="c0b0d-237">1</span></span> | <span data-ttu-id="c0b0d-238">28</span><span class="sxs-lookup"><span data-stu-id="c0b0d-238">28</span></span> |
| <span data-ttu-id="c0b0d-239">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="c0b0d-239">Get conversations</span></span> | <span data-ttu-id="c0b0d-240">2</span><span class="sxs-lookup"><span data-stu-id="c0b0d-240">2</span></span> | <span data-ttu-id="c0b0d-241">32</span><span class="sxs-lookup"><span data-stu-id="c0b0d-241">32</span></span> |

## <a name="next-step"></a><span data-ttu-id="c0b0d-242">次の手順</span><span class="sxs-lookup"><span data-stu-id="c0b0d-242">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c0b0d-243">通話と会議のボット</span><span class="sxs-lookup"><span data-stu-id="c0b0d-243">Calls and meetings bots</span></span>](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

