---
title: レート制限
description: Microsoft Teams でのレートの制限とベストプラクティス
keywords: teams のボットレート制限
ms.openlocfilehash: 9b244053d42aaddaf48c798e401438b614b0e1bd
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "44801314"
---
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a><span data-ttu-id="44997-104">Bot を最適化する: Microsoft Teams でのレートの制限とベストプラクティス</span><span class="sxs-lookup"><span data-stu-id="44997-104">Optimize your bot: rate limiting and best practices in Microsoft Teams</span></span>

<span data-ttu-id="44997-105">一般的な原則として、アプリケーションでは、個々のチャットまたはチャネル会話に投稿するメッセージ数を制限する必要があります。</span><span class="sxs-lookup"><span data-stu-id="44997-105">As a general principle, your application should limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="44997-106">これにより、エンドユーザーに "spammy" を感じない最適な操作性が実現されます。</span><span class="sxs-lookup"><span data-stu-id="44997-106">This ensures an optimal experience that doesn't feel “spammy” to your end users.</span></span>

<span data-ttu-id="44997-107">Microsoft Teams とそのユーザーを保護するために、bot Api rate は受信要求を制限します。</span><span class="sxs-lookup"><span data-stu-id="44997-107">To protect Microsoft Teams and its users, the bot APIs rate-limit incoming requests.</span></span> <span data-ttu-id="44997-108">この制限を超えるアプリは、 `HTTP 429 Too Many Requests` エラー状態を受信します。</span><span class="sxs-lookup"><span data-stu-id="44997-108">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="44997-109">すべての要求は、メッセージの送信、チャネルの列挙、名簿の取得など、同じ料金を制限するポリシーに従います。</span><span class="sxs-lookup"><span data-stu-id="44997-109">All requests are subject to the same rate-limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="44997-110">レート制限の正確な値は変更される可能性があるため、API が戻るときに、アプリケーションで適切なバックオフ動作を実装することをお勧め `HTTP 429 Too Many Requests` します。</span><span class="sxs-lookup"><span data-stu-id="44997-110">Because the exact values of rate limits are subject to change, we recommend your application implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handling-rate-limits"></a><span data-ttu-id="44997-111">処理率の制限</span><span class="sxs-lookup"><span data-stu-id="44997-111">Handling rate limits</span></span>

<span data-ttu-id="44997-112">Bot ビルダー SDK 操作を発行するときに、 `Microsoft.Rest.HttpOperationException` 状態コードを処理および確認できます。</span><span class="sxs-lookup"><span data-stu-id="44997-112">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="44997-113">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="44997-113">Best practices</span></span>

<span data-ttu-id="44997-114">通常、応答を受信しないようにするには、簡単な予防措置を講じる必要があり `HTTP 429` ます。</span><span class="sxs-lookup"><span data-stu-id="44997-114">In general, you should take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="44997-115">たとえば、同じ個人用またはチャネル会話に対して複数の要求を発行しないようにします。</span><span class="sxs-lookup"><span data-stu-id="44997-115">For instance, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="44997-116">代わりに、API 要求のバッチ処理を検討してください。</span><span class="sxs-lookup"><span data-stu-id="44997-116">Instead, consider batching the API requests.</span></span>

<span data-ttu-id="44997-117">ランダムな変位による指数バックオフを使用することは、429s を処理するために推奨される方法です。</span><span class="sxs-lookup"><span data-stu-id="44997-117">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="44997-118">これにより、複数の要求で再試行時に競合が発生しなくなります。</span><span class="sxs-lookup"><span data-stu-id="44997-118">This ensures that multiple requests don't introduce collisions on retries.</span></span>

## <a name="example-detecting-transient-exceptions"></a><span data-ttu-id="44997-119">例: 一時的な例外を検出する</span><span class="sxs-lookup"><span data-stu-id="44997-119">Example: detecting transient exceptions</span></span>

<span data-ttu-id="44997-120">ここでは、一時的な障害処理アプリケーションブロックによる指数バックオフを使用する例を示します。</span><span class="sxs-lookup"><span data-stu-id="44997-120">Here is a sample using exponential backoff via the Transient Fault Handling Application Block.</span></span>

<span data-ttu-id="44997-121">[一時的なエラー処理](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)を使用して、バックオフと再試行を実行できます。</span><span class="sxs-lookup"><span data-stu-id="44997-121">You can perform backoff and retries using [Transient Fault Handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="44997-122">NuGet パッケージを入手してインストールするためのガイドラインについては、「[一時的なエラー処理アプリケーションブロックをソリューションに追加](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="44997-122">For guidelines on obtaining and installing the NuGet package, see [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)).</span></span> <span data-ttu-id="44997-123">「[一時的なフォールト処理](/azure/architecture/best-practices/transient-faults) *」も参照してください*。</span><span class="sxs-lookup"><span data-stu-id="44997-123">*See also* [Transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

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

## <a name="example-backoff"></a><span data-ttu-id="44997-124">例: バックオフ</span><span class="sxs-lookup"><span data-stu-id="44997-124">Example: backoff</span></span>

<span data-ttu-id="44997-125">速度制限の検出に加えて、指数バックオフを実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="44997-125">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

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

<span data-ttu-id="44997-126">前に説明した再試行ポリシーを使用して、メソッドを実行することもでき `System.Action` ます。</span><span class="sxs-lookup"><span data-stu-id="44997-126">You can also perform a `System.Action` method execution with the retry policy described above.</span></span> <span data-ttu-id="44997-127">参照されるライブラリでは、固定の間隔または線形バックオフメカニズムを指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="44997-127">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="44997-128">値と戦略を構成ファイルに格納して、実行時に値を微調整および調整することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="44997-128">We recommend storing the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="44997-129">詳細については、この便利な「再試行[パターン](/azure/architecture/patterns/retry)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="44997-129">For more information, check out this handy guide on various retry patterns: [Retry pattern](/azure/architecture/patterns/retry).</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="44997-130">スレッドの制限ごとに1つの bot</span><span class="sxs-lookup"><span data-stu-id="44997-130">Per bot per thread limit</span></span>

>[!NOTE]
><span data-ttu-id="44997-131">サービスレベルでのメッセージ分割は、予想される1秒あたりの要求数 (RPS) を超える結果になります。</span><span class="sxs-lookup"><span data-stu-id="44997-131">Message splitting at the service level will result in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="44997-132">制限への接近を懸念している場合は、前述のバックオフ戦略を実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="44997-132">If you're concerned about approaching the limits, you should implement the backoff strategy described above.</span></span> <span data-ttu-id="44997-133">以下の値は、見積のみを対象としています。</span><span class="sxs-lookup"><span data-stu-id="44997-133">The values provided below are for estimation only.</span></span>

<span data-ttu-id="44997-134">この制限は、bot が1回の会話で生成できるトラフィックを制御します。</span><span class="sxs-lookup"><span data-stu-id="44997-134">This limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="44997-135">ここでの会話は、ボットとユーザー、グループチャット、またはチーム内のチャネルの間で1:1 です。</span><span class="sxs-lookup"><span data-stu-id="44997-135">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="44997-136">**シナリオ**</span><span class="sxs-lookup"><span data-stu-id="44997-136">**Scenario**</span></span> | <span data-ttu-id="44997-137">**期間 (秒)**</span><span class="sxs-lookup"><span data-stu-id="44997-137">**Time-period (sec)**</span></span> | <span data-ttu-id="44997-138">**許可される最大操作数**</span><span class="sxs-lookup"><span data-stu-id="44997-138">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44997-139">会話に送信</span><span class="sxs-lookup"><span data-stu-id="44997-139">Send to Conversation</span></span> | <span data-ttu-id="44997-140">1 </span><span class="sxs-lookup"><span data-stu-id="44997-140">1</span></span> | <span data-ttu-id="44997-141">7 </span><span class="sxs-lookup"><span data-stu-id="44997-141">7</span></span> |
| <span data-ttu-id="44997-142">会話に送信</span><span class="sxs-lookup"><span data-stu-id="44997-142">Send to Conversation</span></span> | <span data-ttu-id="44997-143">pbm-2</span><span class="sxs-lookup"><span data-stu-id="44997-143">2</span></span> | <span data-ttu-id="44997-144">8 </span><span class="sxs-lookup"><span data-stu-id="44997-144">8</span></span> |
| <span data-ttu-id="44997-145">会話に送信</span><span class="sxs-lookup"><span data-stu-id="44997-145">Send to Conversation</span></span> | <span data-ttu-id="44997-146">31</span><span class="sxs-lookup"><span data-stu-id="44997-146">30</span></span> | <span data-ttu-id="44997-147">60</span><span class="sxs-lookup"><span data-stu-id="44997-147">60</span></span> |
| <span data-ttu-id="44997-148">会話に送信</span><span class="sxs-lookup"><span data-stu-id="44997-148">Send to Conversation</span></span> | <span data-ttu-id="44997-149">3600</span><span class="sxs-lookup"><span data-stu-id="44997-149">3600</span></span> | <span data-ttu-id="44997-150">1800</span><span class="sxs-lookup"><span data-stu-id="44997-150">1800</span></span> |
| <span data-ttu-id="44997-151">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="44997-151">Create Conversation</span></span> | <span data-ttu-id="44997-152">1 </span><span class="sxs-lookup"><span data-stu-id="44997-152">1</span></span> | <span data-ttu-id="44997-153">7 </span><span class="sxs-lookup"><span data-stu-id="44997-153">7</span></span> |
| <span data-ttu-id="44997-154">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="44997-154">Create Conversation</span></span> | <span data-ttu-id="44997-155">pbm-2</span><span class="sxs-lookup"><span data-stu-id="44997-155">2</span></span> | <span data-ttu-id="44997-156">8 </span><span class="sxs-lookup"><span data-stu-id="44997-156">8</span></span> |
| <span data-ttu-id="44997-157">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="44997-157">Create Conversation</span></span> | <span data-ttu-id="44997-158">31</span><span class="sxs-lookup"><span data-stu-id="44997-158">30</span></span> | <span data-ttu-id="44997-159">60</span><span class="sxs-lookup"><span data-stu-id="44997-159">60</span></span> |
| <span data-ttu-id="44997-160">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="44997-160">Create Conversation</span></span> | <span data-ttu-id="44997-161">3600</span><span class="sxs-lookup"><span data-stu-id="44997-161">3600</span></span> | <span data-ttu-id="44997-162">1800</span><span class="sxs-lookup"><span data-stu-id="44997-162">1800</span></span> |
| <span data-ttu-id="44997-163">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="44997-163">Get Conversation Members</span></span>| <span data-ttu-id="44997-164">1 </span><span class="sxs-lookup"><span data-stu-id="44997-164">1</span></span> | <span data-ttu-id="44997-165">14 </span><span class="sxs-lookup"><span data-stu-id="44997-165">14</span></span> |
| <span data-ttu-id="44997-166">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="44997-166">Get Conversation Members</span></span>| <span data-ttu-id="44997-167">pbm-2</span><span class="sxs-lookup"><span data-stu-id="44997-167">2</span></span> | <span data-ttu-id="44997-168">16 </span><span class="sxs-lookup"><span data-stu-id="44997-168">16</span></span> |
| <span data-ttu-id="44997-169">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="44997-169">Get Conversation Members</span></span>| <span data-ttu-id="44997-170">31</span><span class="sxs-lookup"><span data-stu-id="44997-170">30</span></span> | <span data-ttu-id="44997-171">120</span><span class="sxs-lookup"><span data-stu-id="44997-171">120</span></span> |
| <span data-ttu-id="44997-172">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="44997-172">Get Conversation Members</span></span>| <span data-ttu-id="44997-173">3600</span><span class="sxs-lookup"><span data-stu-id="44997-173">3600</span></span> | <span data-ttu-id="44997-174">3600</span><span class="sxs-lookup"><span data-stu-id="44997-174">3600</span></span> |
| <span data-ttu-id="44997-175">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="44997-175">Get Conversations</span></span> | <span data-ttu-id="44997-176">1 </span><span class="sxs-lookup"><span data-stu-id="44997-176">1</span></span> | <span data-ttu-id="44997-177">14 </span><span class="sxs-lookup"><span data-stu-id="44997-177">14</span></span> |
| <span data-ttu-id="44997-178">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="44997-178">Get Conversations</span></span> | <span data-ttu-id="44997-179">pbm-2</span><span class="sxs-lookup"><span data-stu-id="44997-179">2</span></span> | <span data-ttu-id="44997-180">16 </span><span class="sxs-lookup"><span data-stu-id="44997-180">16</span></span> |
| <span data-ttu-id="44997-181">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="44997-181">Get Conversations</span></span> | <span data-ttu-id="44997-182">31</span><span class="sxs-lookup"><span data-stu-id="44997-182">30</span></span> | <span data-ttu-id="44997-183">120</span><span class="sxs-lookup"><span data-stu-id="44997-183">120</span></span> |
| <span data-ttu-id="44997-184">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="44997-184">Get Conversations</span></span> | <span data-ttu-id="44997-185">3600</span><span class="sxs-lookup"><span data-stu-id="44997-185">3600</span></span> | <span data-ttu-id="44997-186">3600</span><span class="sxs-lookup"><span data-stu-id="44997-186">3600</span></span> |

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="44997-187">すべてのボットに対するスレッド数の制限</span><span class="sxs-lookup"><span data-stu-id="44997-187">Per thread limit for all bots</span></span>

<span data-ttu-id="44997-188">この制限は、すべてのボットが1つの会話で生成できるトラフィックを制御します。</span><span class="sxs-lookup"><span data-stu-id="44997-188">This limit controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="44997-189">ここでの会話は、ボットとユーザー、グループチャット、またはチーム内のチャネルの間で1:1 です。</span><span class="sxs-lookup"><span data-stu-id="44997-189">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="44997-190">**シナリオ**</span><span class="sxs-lookup"><span data-stu-id="44997-190">**Scenario**</span></span> | <span data-ttu-id="44997-191">**期間 (秒)**</span><span class="sxs-lookup"><span data-stu-id="44997-191">**Time-period (sec)**</span></span> | <span data-ttu-id="44997-192">**許可される最大操作数**</span><span class="sxs-lookup"><span data-stu-id="44997-192">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44997-193">会話に送信</span><span class="sxs-lookup"><span data-stu-id="44997-193">Send to Conversation</span></span> | <span data-ttu-id="44997-194">1 </span><span class="sxs-lookup"><span data-stu-id="44997-194">1</span></span> | <span data-ttu-id="44997-195">14 </span><span class="sxs-lookup"><span data-stu-id="44997-195">14</span></span> |
| <span data-ttu-id="44997-196">会話に送信</span><span class="sxs-lookup"><span data-stu-id="44997-196">Send to Conversation</span></span> | <span data-ttu-id="44997-197">pbm-2</span><span class="sxs-lookup"><span data-stu-id="44997-197">2</span></span> | <span data-ttu-id="44997-198">16 </span><span class="sxs-lookup"><span data-stu-id="44997-198">16</span></span> |
| <span data-ttu-id="44997-199">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="44997-199">Create Conversation</span></span> | <span data-ttu-id="44997-200">1 </span><span class="sxs-lookup"><span data-stu-id="44997-200">1</span></span> | <span data-ttu-id="44997-201">14 </span><span class="sxs-lookup"><span data-stu-id="44997-201">14</span></span> |
| <span data-ttu-id="44997-202">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="44997-202">Create Conversation</span></span> | <span data-ttu-id="44997-203">pbm-2</span><span class="sxs-lookup"><span data-stu-id="44997-203">2</span></span> | <span data-ttu-id="44997-204">16 </span><span class="sxs-lookup"><span data-stu-id="44997-204">16</span></span> |
| <span data-ttu-id="44997-205">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="44997-205">CreateConversation</span></span>| <span data-ttu-id="44997-206">1 </span><span class="sxs-lookup"><span data-stu-id="44997-206">1</span></span> | <span data-ttu-id="44997-207">14 </span><span class="sxs-lookup"><span data-stu-id="44997-207">14</span></span> |
| <span data-ttu-id="44997-208">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="44997-208">CreateConversation</span></span>| <span data-ttu-id="44997-209">pbm-2</span><span class="sxs-lookup"><span data-stu-id="44997-209">2</span></span> | <span data-ttu-id="44997-210">16 </span><span class="sxs-lookup"><span data-stu-id="44997-210">16</span></span> |
| <span data-ttu-id="44997-211">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="44997-211">Get Conversation Members</span></span>| <span data-ttu-id="44997-212">1 </span><span class="sxs-lookup"><span data-stu-id="44997-212">1</span></span> | <span data-ttu-id="44997-213">個</span><span class="sxs-lookup"><span data-stu-id="44997-213">28</span></span> |
| <span data-ttu-id="44997-214">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="44997-214">Get Conversation Members</span></span>| <span data-ttu-id="44997-215">pbm-2</span><span class="sxs-lookup"><span data-stu-id="44997-215">2</span></span> | <span data-ttu-id="44997-216">32</span><span class="sxs-lookup"><span data-stu-id="44997-216">32</span></span> |
| <span data-ttu-id="44997-217">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="44997-217">Get Conversations</span></span> | <span data-ttu-id="44997-218">1 </span><span class="sxs-lookup"><span data-stu-id="44997-218">1</span></span> | <span data-ttu-id="44997-219">個</span><span class="sxs-lookup"><span data-stu-id="44997-219">28</span></span> |
| <span data-ttu-id="44997-220">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="44997-220">Get Conversations</span></span> | <span data-ttu-id="44997-221">pbm-2</span><span class="sxs-lookup"><span data-stu-id="44997-221">2</span></span> | <span data-ttu-id="44997-222">32</span><span class="sxs-lookup"><span data-stu-id="44997-222">32</span></span> |

## <a name="bot-per-data-center-limit"></a><span data-ttu-id="44997-223">データセンターあたりの Bot 数の制限</span><span class="sxs-lookup"><span data-stu-id="44997-223">Bot per data center limit</span></span>

<span data-ttu-id="44997-224">この制限は、1つのデータセンター (複数のテナント) 内のすべてのスレッド間でボットが生成できるトラフィックを制御します。</span><span class="sxs-lookup"><span data-stu-id="44997-224">This limit controls the traffic that a bot is allowed to generate across all threads in a data center (across multiple tenants).</span></span>

|<span data-ttu-id="44997-225">**期間 (秒)**</span><span class="sxs-lookup"><span data-stu-id="44997-225">**Time-period (sec)**</span></span> | <span data-ttu-id="44997-226">**許可される最大操作数**</span><span class="sxs-lookup"><span data-stu-id="44997-226">**Max allowed operations**</span></span> |
| --- | --- |
| <span data-ttu-id="44997-227">1 </span><span class="sxs-lookup"><span data-stu-id="44997-227">1</span></span> | <span data-ttu-id="44997-228">1280</span><span class="sxs-lookup"><span data-stu-id="44997-228">20</span></span> |
| <span data-ttu-id="44997-229">1800</span><span class="sxs-lookup"><span data-stu-id="44997-229">1800</span></span> | <span data-ttu-id="44997-230">8000</span><span class="sxs-lookup"><span data-stu-id="44997-230">8000</span></span> |
| <span data-ttu-id="44997-231">3600</span><span class="sxs-lookup"><span data-stu-id="44997-231">3600</span></span> | <span data-ttu-id="44997-232">15000</span><span class="sxs-lookup"><span data-stu-id="44997-232">15000</span></span> |
