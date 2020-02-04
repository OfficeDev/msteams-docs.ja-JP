---
title: レート制限
description: Microsoft Teams でのレートの制限とベストプラクティス
keywords: teams のボットレート制限
ms.openlocfilehash: 4e9efab539ec7817d259fd6c149c438ba02e3ce5
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674750"
---
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a><span data-ttu-id="50265-104">Bot を最適化する: Microsoft Teams でのレートの制限とベストプラクティス</span><span class="sxs-lookup"><span data-stu-id="50265-104">Optimize your bot: rate limiting and best practices in Microsoft Teams</span></span>

<span data-ttu-id="50265-105">一般的な原則として、アプリケーションでは、個々のチャットまたはチャネル会話に投稿するメッセージ数を制限する必要があります。</span><span class="sxs-lookup"><span data-stu-id="50265-105">As a general principle, your application should limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="50265-106">これにより、エンドユーザーに "spammy" を感じない最適な操作性が実現されます。</span><span class="sxs-lookup"><span data-stu-id="50265-106">This ensures an optimal experience that doesn't feel “spammy” to your end users.</span></span>

<span data-ttu-id="50265-107">Microsoft Teams とそのユーザーを保護するために、bot Api rate は受信要求を制限します。</span><span class="sxs-lookup"><span data-stu-id="50265-107">To protect Microsoft Teams and its users, the bot APIs rate-limit incoming requests.</span></span> <span data-ttu-id="50265-108">この制限を超えるアプリは、エラー `HTTP 429 Too Many Requests`状態を受信します。</span><span class="sxs-lookup"><span data-stu-id="50265-108">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="50265-109">すべての要求は、メッセージの送信、チャネルの列挙、名簿の取得など、同じ料金を制限するポリシーに従います。</span><span class="sxs-lookup"><span data-stu-id="50265-109">All requests are subject to the same rate-limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="50265-110">レート制限の正確な値は変更される可能性があるため、API が戻る`HTTP 429 Too Many Requests`ときに、アプリケーションで適切なバックオフ動作を実装することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="50265-110">Because the exact values of rate limits are subject to change, we recommend your application implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handling-rate-limits"></a><span data-ttu-id="50265-111">処理率の制限</span><span class="sxs-lookup"><span data-stu-id="50265-111">Handling rate limits</span></span>

<span data-ttu-id="50265-112">Bot ビルダー SDK 操作を発行するときに、状態`Microsoft.Rest.HttpOperationException`コードを処理および確認できます。</span><span class="sxs-lookup"><span data-stu-id="50265-112">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="50265-113">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="50265-113">Best practices</span></span>

<span data-ttu-id="50265-114">通常、応答を受信`HTTP 429`しないようにするには、簡単な予防措置を講じる必要があります。</span><span class="sxs-lookup"><span data-stu-id="50265-114">In general, you should take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="50265-115">たとえば、同じ個人用またはチャネル会話に対して複数の要求を発行しないようにします。</span><span class="sxs-lookup"><span data-stu-id="50265-115">For instance, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="50265-116">代わりに、API 要求のバッチ処理を検討してください。</span><span class="sxs-lookup"><span data-stu-id="50265-116">Instead, consider batching the API requests.</span></span>

<span data-ttu-id="50265-117">ランダムな変位による指数バックオフを使用することは、429s を処理するために推奨される方法です。</span><span class="sxs-lookup"><span data-stu-id="50265-117">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="50265-118">これにより、複数の要求で再試行時に競合が発生しなくなります。</span><span class="sxs-lookup"><span data-stu-id="50265-118">This ensures that multiple requests don't introduce collisions on retries.</span></span>

## <a name="example-detecting-transient-exceptions"></a><span data-ttu-id="50265-119">例: 一時的な例外を検出する</span><span class="sxs-lookup"><span data-stu-id="50265-119">Example: detecting transient exceptions</span></span>

<span data-ttu-id="50265-120">ここでは、一時的な障害処理アプリケーションブロックによる指数バックオフを使用する例を示します。</span><span class="sxs-lookup"><span data-stu-id="50265-120">Here is a sample using exponential backoff via the Transient Fault Handling Application Block.</span></span>

<span data-ttu-id="50265-121">[一時的な障害処理ライブラリ](/previous-versions/msp-n-p/hh680901(v=pandp.50))を使用して、バックオフと再試行を実行できます。</span><span class="sxs-lookup"><span data-stu-id="50265-121">You can perform backoff and retries using [Transient Fault Handling libraries](/previous-versions/msp-n-p/hh680901(v=pandp.50)).</span></span> <span data-ttu-id="50265-122">NuGet パッケージを入手してインストールするためのガイドラインについては、「[ソリューションに一時的なエラー処理アプリケーションブロックを追加](/previous-versions/msp-n-p/hh680891(v=pandp.50))する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="50265-122">For guidelines on obtaining and installing the NuGet package, see [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/hh680891(v=pandp.50))</span></span>

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

## <a name="example-backoff"></a><span data-ttu-id="50265-123">例: バックオフ</span><span class="sxs-lookup"><span data-stu-id="50265-123">Example: backoff</span></span>

<span data-ttu-id="50265-124">速度制限の検出に加えて、指数バックオフを実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="50265-124">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

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

<span data-ttu-id="50265-125">前に説明した`System.Action`再試行ポリシーを使用して、メソッドを実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="50265-125">You can also perform a `System.Action` method execution with the retry policy described above.</span></span> <span data-ttu-id="50265-126">参照されるライブラリでは、固定の間隔または線形バックオフメカニズムを指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="50265-126">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="50265-127">値と戦略を構成ファイルに格納して、実行時に値を微調整および調整することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="50265-127">We recommend storing the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="50265-128">詳細については、この便利な「再試行[パターン](/azure/architecture/patterns/retry)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="50265-128">For more information, check out this handy guide on various retry patterns: [Retry pattern](/azure/architecture/patterns/retry).</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="50265-129">スレッドの制限ごとに1つの bot</span><span class="sxs-lookup"><span data-stu-id="50265-129">Per bot per thread limit</span></span>

>[!NOTE]
><span data-ttu-id="50265-130">サービスレベルでのメッセージ分割は、予想される1秒あたりの要求数 (RPS) を超える結果になります。</span><span class="sxs-lookup"><span data-stu-id="50265-130">Message splitting at the service level will result in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="50265-131">制限への接近を懸念している場合は、前述のバックオフ戦略を実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="50265-131">If you're concerned about approaching the limits, you should implement the backoff strategy described above.</span></span> <span data-ttu-id="50265-132">以下の値は、見積のみを対象としています。</span><span class="sxs-lookup"><span data-stu-id="50265-132">The values provided below are for estimation only.</span></span>

<span data-ttu-id="50265-133">この制限は、bot が1回の会話で生成できるトラフィックを制御します。</span><span class="sxs-lookup"><span data-stu-id="50265-133">This limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="50265-134">ここでの会話は、ボットとユーザー、グループチャット、またはチーム内のチャネルの間で1:1 です。</span><span class="sxs-lookup"><span data-stu-id="50265-134">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="50265-135">**シナリオ**</span><span class="sxs-lookup"><span data-stu-id="50265-135">**Scenario**</span></span> | <span data-ttu-id="50265-136">**期間 (秒)**</span><span class="sxs-lookup"><span data-stu-id="50265-136">**Time-period (sec)**</span></span> | <span data-ttu-id="50265-137">**許可される最大操作数**</span><span class="sxs-lookup"><span data-stu-id="50265-137">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="50265-138">NewMessage</span><span class="sxs-lookup"><span data-stu-id="50265-138">NewMessage</span></span> | <span data-ttu-id="50265-139">1 </span><span class="sxs-lookup"><span data-stu-id="50265-139">1</span></span> | <span data-ttu-id="50265-140">7 </span><span class="sxs-lookup"><span data-stu-id="50265-140">7</span></span> |
| <span data-ttu-id="50265-141">NewMessage</span><span class="sxs-lookup"><span data-stu-id="50265-141">NewMessage</span></span> | <span data-ttu-id="50265-142">2 </span><span class="sxs-lookup"><span data-stu-id="50265-142">2</span></span> | <span data-ttu-id="50265-143">8 </span><span class="sxs-lookup"><span data-stu-id="50265-143">8</span></span> |
| <span data-ttu-id="50265-144">NewMessage</span><span class="sxs-lookup"><span data-stu-id="50265-144">NewMessage</span></span> | <span data-ttu-id="50265-145">31</span><span class="sxs-lookup"><span data-stu-id="50265-145">30</span></span> | <span data-ttu-id="50265-146">60</span><span class="sxs-lookup"><span data-stu-id="50265-146">60</span></span> |
| <span data-ttu-id="50265-147">NewMessage</span><span class="sxs-lookup"><span data-stu-id="50265-147">NewMessage</span></span> | <span data-ttu-id="50265-148">3600</span><span class="sxs-lookup"><span data-stu-id="50265-148">3600</span></span> | <span data-ttu-id="50265-149">1800</span><span class="sxs-lookup"><span data-stu-id="50265-149">1800</span></span> |
| <span data-ttu-id="50265-150">次</span><span class="sxs-lookup"><span data-stu-id="50265-150">UpdateMessage</span></span> | <span data-ttu-id="50265-151">1 </span><span class="sxs-lookup"><span data-stu-id="50265-151">1</span></span> | <span data-ttu-id="50265-152">7 </span><span class="sxs-lookup"><span data-stu-id="50265-152">7</span></span> |
| <span data-ttu-id="50265-153">次</span><span class="sxs-lookup"><span data-stu-id="50265-153">UpdateMessage</span></span> | <span data-ttu-id="50265-154">2 </span><span class="sxs-lookup"><span data-stu-id="50265-154">2</span></span> | <span data-ttu-id="50265-155">8 </span><span class="sxs-lookup"><span data-stu-id="50265-155">8</span></span> |
| <span data-ttu-id="50265-156">次</span><span class="sxs-lookup"><span data-stu-id="50265-156">UpdateMessage</span></span> | <span data-ttu-id="50265-157">31</span><span class="sxs-lookup"><span data-stu-id="50265-157">30</span></span> | <span data-ttu-id="50265-158">60</span><span class="sxs-lookup"><span data-stu-id="50265-158">60</span></span> |
| <span data-ttu-id="50265-159">次</span><span class="sxs-lookup"><span data-stu-id="50265-159">UpdateMessage</span></span> | <span data-ttu-id="50265-160">3600</span><span class="sxs-lookup"><span data-stu-id="50265-160">3600</span></span> | <span data-ttu-id="50265-161">1800</span><span class="sxs-lookup"><span data-stu-id="50265-161">1800</span></span> |
| <span data-ttu-id="50265-162">NewThread</span><span class="sxs-lookup"><span data-stu-id="50265-162">NewThread</span></span> | <span data-ttu-id="50265-163">1 </span><span class="sxs-lookup"><span data-stu-id="50265-163">1</span></span> | <span data-ttu-id="50265-164">7 </span><span class="sxs-lookup"><span data-stu-id="50265-164">7</span></span> |
| <span data-ttu-id="50265-165">NewThread</span><span class="sxs-lookup"><span data-stu-id="50265-165">NewThread</span></span> | <span data-ttu-id="50265-166">2 </span><span class="sxs-lookup"><span data-stu-id="50265-166">2</span></span> | <span data-ttu-id="50265-167">8 </span><span class="sxs-lookup"><span data-stu-id="50265-167">8</span></span> |
| <span data-ttu-id="50265-168">NewThread</span><span class="sxs-lookup"><span data-stu-id="50265-168">NewThread</span></span> | <span data-ttu-id="50265-169">31</span><span class="sxs-lookup"><span data-stu-id="50265-169">30</span></span> | <span data-ttu-id="50265-170">60</span><span class="sxs-lookup"><span data-stu-id="50265-170">60</span></span> |
| <span data-ttu-id="50265-171">NewThread</span><span class="sxs-lookup"><span data-stu-id="50265-171">NewThread</span></span> | <span data-ttu-id="50265-172">3600</span><span class="sxs-lookup"><span data-stu-id="50265-172">3600</span></span> | <span data-ttu-id="50265-173">1800</span><span class="sxs-lookup"><span data-stu-id="50265-173">1800</span></span> |
| <span data-ttu-id="50265-174">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="50265-174">GetThreadMembers</span></span> | <span data-ttu-id="50265-175">1 </span><span class="sxs-lookup"><span data-stu-id="50265-175">1</span></span> | <span data-ttu-id="50265-176">14 </span><span class="sxs-lookup"><span data-stu-id="50265-176">14</span></span> |
| <span data-ttu-id="50265-177">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="50265-177">GetThreadMembers</span></span> | <span data-ttu-id="50265-178">2 </span><span class="sxs-lookup"><span data-stu-id="50265-178">2</span></span> | <span data-ttu-id="50265-179">16 </span><span class="sxs-lookup"><span data-stu-id="50265-179">16</span></span> |
| <span data-ttu-id="50265-180">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="50265-180">GetThreadMembers</span></span> | <span data-ttu-id="50265-181">31</span><span class="sxs-lookup"><span data-stu-id="50265-181">30</span></span> | <span data-ttu-id="50265-182">120</span><span class="sxs-lookup"><span data-stu-id="50265-182">120</span></span> |
| <span data-ttu-id="50265-183">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="50265-183">GetThreadMembers</span></span> | <span data-ttu-id="50265-184">3600</span><span class="sxs-lookup"><span data-stu-id="50265-184">3600</span></span> | <span data-ttu-id="50265-185">3600</span><span class="sxs-lookup"><span data-stu-id="50265-185">3600</span></span> |
| <span data-ttu-id="50265-186">GetThread</span><span class="sxs-lookup"><span data-stu-id="50265-186">GetThread</span></span> | <span data-ttu-id="50265-187">1 </span><span class="sxs-lookup"><span data-stu-id="50265-187">1</span></span> | <span data-ttu-id="50265-188">14 </span><span class="sxs-lookup"><span data-stu-id="50265-188">14</span></span> |
| <span data-ttu-id="50265-189">GetThread</span><span class="sxs-lookup"><span data-stu-id="50265-189">GetThread</span></span> | <span data-ttu-id="50265-190">2 </span><span class="sxs-lookup"><span data-stu-id="50265-190">2</span></span> | <span data-ttu-id="50265-191">16 </span><span class="sxs-lookup"><span data-stu-id="50265-191">16</span></span> |
| <span data-ttu-id="50265-192">GetThread</span><span class="sxs-lookup"><span data-stu-id="50265-192">GetThread</span></span> | <span data-ttu-id="50265-193">31</span><span class="sxs-lookup"><span data-stu-id="50265-193">30</span></span> | <span data-ttu-id="50265-194">120</span><span class="sxs-lookup"><span data-stu-id="50265-194">120</span></span> |
| <span data-ttu-id="50265-195">GetThread</span><span class="sxs-lookup"><span data-stu-id="50265-195">GetThread</span></span> | <span data-ttu-id="50265-196">3600</span><span class="sxs-lookup"><span data-stu-id="50265-196">3600</span></span> | <span data-ttu-id="50265-197">3600</span><span class="sxs-lookup"><span data-stu-id="50265-197">3600</span></span> |

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="50265-198">すべてのボットに対するスレッド数の制限</span><span class="sxs-lookup"><span data-stu-id="50265-198">Per thread limit for all bots</span></span>

<span data-ttu-id="50265-199">この制限は、すべてのボットが1つの会話で生成できるトラフィックを制御します。</span><span class="sxs-lookup"><span data-stu-id="50265-199">This limit controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="50265-200">ここでの会話は、ボットとユーザー、グループチャット、またはチーム内のチャネルの間で1:1 です。</span><span class="sxs-lookup"><span data-stu-id="50265-200">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="50265-201">**シナリオ**</span><span class="sxs-lookup"><span data-stu-id="50265-201">**Scenario**</span></span> | <span data-ttu-id="50265-202">**期間 (秒)**</span><span class="sxs-lookup"><span data-stu-id="50265-202">**Time-period (sec)**</span></span> | <span data-ttu-id="50265-203">**許可される最大操作数**</span><span class="sxs-lookup"><span data-stu-id="50265-203">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="50265-204">NewMessage</span><span class="sxs-lookup"><span data-stu-id="50265-204">NewMessage</span></span> | <span data-ttu-id="50265-205">1 </span><span class="sxs-lookup"><span data-stu-id="50265-205">1</span></span> | <span data-ttu-id="50265-206">14 </span><span class="sxs-lookup"><span data-stu-id="50265-206">14</span></span> |
| <span data-ttu-id="50265-207">NewMessage</span><span class="sxs-lookup"><span data-stu-id="50265-207">NewMessage</span></span> | <span data-ttu-id="50265-208">2 </span><span class="sxs-lookup"><span data-stu-id="50265-208">2</span></span> | <span data-ttu-id="50265-209">16 </span><span class="sxs-lookup"><span data-stu-id="50265-209">16</span></span> |
| <span data-ttu-id="50265-210">次</span><span class="sxs-lookup"><span data-stu-id="50265-210">UpdateMessage</span></span> | <span data-ttu-id="50265-211">1 </span><span class="sxs-lookup"><span data-stu-id="50265-211">1</span></span> | <span data-ttu-id="50265-212">14 </span><span class="sxs-lookup"><span data-stu-id="50265-212">14</span></span> |
| <span data-ttu-id="50265-213">次</span><span class="sxs-lookup"><span data-stu-id="50265-213">UpdateMessage</span></span> | <span data-ttu-id="50265-214">2 </span><span class="sxs-lookup"><span data-stu-id="50265-214">2</span></span> | <span data-ttu-id="50265-215">16 </span><span class="sxs-lookup"><span data-stu-id="50265-215">16</span></span> |
| <span data-ttu-id="50265-216">NewThread</span><span class="sxs-lookup"><span data-stu-id="50265-216">NewThread</span></span> | <span data-ttu-id="50265-217">1 </span><span class="sxs-lookup"><span data-stu-id="50265-217">1</span></span> | <span data-ttu-id="50265-218">14 </span><span class="sxs-lookup"><span data-stu-id="50265-218">14</span></span> |
| <span data-ttu-id="50265-219">NewThread</span><span class="sxs-lookup"><span data-stu-id="50265-219">NewThread</span></span> | <span data-ttu-id="50265-220">2 </span><span class="sxs-lookup"><span data-stu-id="50265-220">2</span></span> | <span data-ttu-id="50265-221">16 </span><span class="sxs-lookup"><span data-stu-id="50265-221">16</span></span> |
| <span data-ttu-id="50265-222">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="50265-222">GetThreadMembers</span></span> | <span data-ttu-id="50265-223">1 </span><span class="sxs-lookup"><span data-stu-id="50265-223">1</span></span> | <span data-ttu-id="50265-224">個</span><span class="sxs-lookup"><span data-stu-id="50265-224">28</span></span> |
| <span data-ttu-id="50265-225">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="50265-225">GetThreadMembers</span></span> | <span data-ttu-id="50265-226">2 </span><span class="sxs-lookup"><span data-stu-id="50265-226">2</span></span> | <span data-ttu-id="50265-227">32</span><span class="sxs-lookup"><span data-stu-id="50265-227">32</span></span> |
| <span data-ttu-id="50265-228">GetThread</span><span class="sxs-lookup"><span data-stu-id="50265-228">GetThread</span></span> | <span data-ttu-id="50265-229">1 </span><span class="sxs-lookup"><span data-stu-id="50265-229">1</span></span> | <span data-ttu-id="50265-230">個</span><span class="sxs-lookup"><span data-stu-id="50265-230">28</span></span> |
| <span data-ttu-id="50265-231">GetThread</span><span class="sxs-lookup"><span data-stu-id="50265-231">GetThread</span></span> | <span data-ttu-id="50265-232">2 </span><span class="sxs-lookup"><span data-stu-id="50265-232">2</span></span> | <span data-ttu-id="50265-233">32</span><span class="sxs-lookup"><span data-stu-id="50265-233">32</span></span> |

## <a name="bot-per-data-center-limit"></a><span data-ttu-id="50265-234">データセンターあたりの Bot 数の制限</span><span class="sxs-lookup"><span data-stu-id="50265-234">Bot per data center limit</span></span>

<span data-ttu-id="50265-235">この制限は、1つのデータセンター (複数のテナント) 内のすべてのスレッド間でボットが生成できるトラフィックを制御します。</span><span class="sxs-lookup"><span data-stu-id="50265-235">This limit controls the traffic that a bot is allowed to generate across all threads in a data center (across multiple tenants).</span></span>

|<span data-ttu-id="50265-236">**期間 (秒)**</span><span class="sxs-lookup"><span data-stu-id="50265-236">**Time-period (sec)**</span></span> | <span data-ttu-id="50265-237">**許可される最大操作数**</span><span class="sxs-lookup"><span data-stu-id="50265-237">**Max allowed operations**</span></span> |
| --- | --- |
| <span data-ttu-id="50265-238">1 </span><span class="sxs-lookup"><span data-stu-id="50265-238">1</span></span> | <span data-ttu-id="50265-239">1280</span><span class="sxs-lookup"><span data-stu-id="50265-239">20</span></span> |
| <span data-ttu-id="50265-240">1800</span><span class="sxs-lookup"><span data-stu-id="50265-240">1800</span></span> | <span data-ttu-id="50265-241">8000</span><span class="sxs-lookup"><span data-stu-id="50265-241">8000</span></span> |
| <span data-ttu-id="50265-242">3600</span><span class="sxs-lookup"><span data-stu-id="50265-242">3600</span></span> | <span data-ttu-id="50265-243">15000</span><span class="sxs-lookup"><span data-stu-id="50265-243">15000</span></span> |
