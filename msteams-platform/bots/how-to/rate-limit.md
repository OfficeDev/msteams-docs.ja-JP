---
title: レート制限
description: Microsoft Teams でのレートの制限とベストプラクティス
keywords: teams のボットレート制限
ms.openlocfilehash: 2e401b59df075688cb6d459a881e6b813f2cf8e6
ms.sourcegitcommit: b3962a7b36f260aef1af9124d14d71ae08b01ac4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "47303711"
---
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a><span data-ttu-id="a21a9-104">Bot を最適化する: Microsoft Teams でのレートの制限とベストプラクティス</span><span class="sxs-lookup"><span data-stu-id="a21a9-104">Optimize your bot: rate limiting and best practices in Microsoft Teams</span></span>

<span data-ttu-id="a21a9-105">一般的な原則として、アプリケーションでは、個々のチャットまたはチャネル会話に投稿するメッセージ数を制限する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a21a9-105">As a general principle, your application should limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="a21a9-106">これにより、エンドユーザーに "spammy" を感じない最適な操作性が実現されます。</span><span class="sxs-lookup"><span data-stu-id="a21a9-106">This ensures an optimal experience that doesn't feel “spammy” to your end users.</span></span>

<span data-ttu-id="a21a9-107">Microsoft Teams とそのユーザーを保護するために、bot Api rate は受信要求を制限します。</span><span class="sxs-lookup"><span data-stu-id="a21a9-107">To protect Microsoft Teams and its users, the bot APIs rate-limit incoming requests.</span></span> <span data-ttu-id="a21a9-108">この制限を超えるアプリは、 `HTTP 429 Too Many Requests` エラー状態を受信します。</span><span class="sxs-lookup"><span data-stu-id="a21a9-108">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="a21a9-109">すべての要求は、メッセージの送信、チャネルの列挙、名簿の取得など、同じ料金を制限するポリシーに従います。</span><span class="sxs-lookup"><span data-stu-id="a21a9-109">All requests are subject to the same rate-limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="a21a9-110">レート制限の正確な値は変更される可能性があるため、API が戻るときに、アプリケーションで適切なバックオフ動作を実装することをお勧め `HTTP 429 Too Many Requests` します。</span><span class="sxs-lookup"><span data-stu-id="a21a9-110">Because the exact values of rate limits are subject to change, we recommend your application implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handling-rate-limits"></a><span data-ttu-id="a21a9-111">処理率の制限</span><span class="sxs-lookup"><span data-stu-id="a21a9-111">Handling rate limits</span></span>

<span data-ttu-id="a21a9-112">Bot ビルダー SDK 操作を発行するときに、 `Microsoft.Rest.HttpOperationException` 状態コードを処理および確認できます。</span><span class="sxs-lookup"><span data-stu-id="a21a9-112">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="a21a9-113">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="a21a9-113">Best practices</span></span>

<span data-ttu-id="a21a9-114">通常、応答を受信しないようにするには、簡単な予防措置を講じる必要があり `HTTP 429` ます。</span><span class="sxs-lookup"><span data-stu-id="a21a9-114">In general, you should take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="a21a9-115">たとえば、同じ個人用またはチャネル会話に対して複数の要求を発行しないようにします。</span><span class="sxs-lookup"><span data-stu-id="a21a9-115">For instance, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="a21a9-116">代わりに、API 要求のバッチ処理を検討してください。</span><span class="sxs-lookup"><span data-stu-id="a21a9-116">Instead, consider batching the API requests.</span></span>

<span data-ttu-id="a21a9-117">ランダムな変位による指数バックオフを使用することは、429s を処理するために推奨される方法です。</span><span class="sxs-lookup"><span data-stu-id="a21a9-117">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="a21a9-118">これにより、複数の要求で再試行時に競合が発生しなくなります。</span><span class="sxs-lookup"><span data-stu-id="a21a9-118">This ensures that multiple requests don't introduce collisions on retries.</span></span>

## <a name="example-detecting-transient-exceptions"></a><span data-ttu-id="a21a9-119">例: 一時的な例外を検出する</span><span class="sxs-lookup"><span data-stu-id="a21a9-119">Example: detecting transient exceptions</span></span>

<span data-ttu-id="a21a9-120">ここでは、一時的な障害処理アプリケーションブロックによる指数バックオフを使用する例を示します。</span><span class="sxs-lookup"><span data-stu-id="a21a9-120">Here is a sample using exponential backoff via the Transient Fault Handling Application Block.</span></span>

<span data-ttu-id="a21a9-121">[一時的なエラー処理](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)を使用して、バックオフと再試行を実行できます。</span><span class="sxs-lookup"><span data-stu-id="a21a9-121">You can perform backoff and retries using [Transient Fault Handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="a21a9-122">NuGet パッケージを入手してインストールするためのガイドラインについては、「 [一時的なエラー処理アプリケーションブロックをソリューションに追加](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a21a9-122">For guidelines on obtaining and installing the NuGet package, see [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)).</span></span> <span data-ttu-id="a21a9-123">「[一時的なフォールト処理](/azure/architecture/best-practices/transient-faults) *」も参照してください*。</span><span class="sxs-lookup"><span data-stu-id="a21a9-123">*See also* [Transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

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

## <a name="example-backoff"></a><span data-ttu-id="a21a9-124">例: バックオフ</span><span class="sxs-lookup"><span data-stu-id="a21a9-124">Example: backoff</span></span>

<span data-ttu-id="a21a9-125">速度制限の検出に加えて、指数バックオフを実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="a21a9-125">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

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

<span data-ttu-id="a21a9-126">前に説明した再試行ポリシーを使用して、メソッドを実行することもでき `System.Action` ます。</span><span class="sxs-lookup"><span data-stu-id="a21a9-126">You can also perform a `System.Action` method execution with the retry policy described above.</span></span> <span data-ttu-id="a21a9-127">参照されるライブラリでは、固定の間隔または線形バックオフメカニズムを指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="a21a9-127">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="a21a9-128">値と戦略を構成ファイルに格納して、実行時に値を微調整および調整することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a21a9-128">We recommend storing the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="a21a9-129">詳細については、この便利な「再試行 [パターン](/azure/architecture/patterns/retry)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a21a9-129">For more information, check out this handy guide on various retry patterns: [Retry pattern](/azure/architecture/patterns/retry).</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="a21a9-130">スレッドの制限ごとに1つの bot</span><span class="sxs-lookup"><span data-stu-id="a21a9-130">Per bot per thread limit</span></span>

>[!NOTE]
><span data-ttu-id="a21a9-131">サービスレベルでのメッセージ分割は、予想される1秒あたりの要求数 (RPS) を超える結果になります。</span><span class="sxs-lookup"><span data-stu-id="a21a9-131">Message splitting at the service level will result in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="a21a9-132">制限への接近を懸念している場合は、前述のバックオフ戦略を実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a21a9-132">If you're concerned about approaching the limits, you should implement the backoff strategy described above.</span></span> <span data-ttu-id="a21a9-133">以下の値は、見積のみを対象としています。</span><span class="sxs-lookup"><span data-stu-id="a21a9-133">The values provided below are for estimation only.</span></span>

<span data-ttu-id="a21a9-134">この制限は、bot が1回の会話で生成できるトラフィックを制御します。</span><span class="sxs-lookup"><span data-stu-id="a21a9-134">This limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="a21a9-135">ここでの会話は、ボットとユーザー、グループチャット、またはチーム内のチャネルの間で1:1 です。</span><span class="sxs-lookup"><span data-stu-id="a21a9-135">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="a21a9-136">**シナリオ**</span><span class="sxs-lookup"><span data-stu-id="a21a9-136">**Scenario**</span></span> | <span data-ttu-id="a21a9-137">**期間 (秒)**</span><span class="sxs-lookup"><span data-stu-id="a21a9-137">**Time-period (sec)**</span></span> | <span data-ttu-id="a21a9-138">**許可される最大操作数**</span><span class="sxs-lookup"><span data-stu-id="a21a9-138">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a21a9-139">会話に送信</span><span class="sxs-lookup"><span data-stu-id="a21a9-139">Send to Conversation</span></span> | <span data-ttu-id="a21a9-140">1 </span><span class="sxs-lookup"><span data-stu-id="a21a9-140">1</span></span> | <span data-ttu-id="a21a9-141">7 </span><span class="sxs-lookup"><span data-stu-id="a21a9-141">7</span></span> |
| <span data-ttu-id="a21a9-142">会話に送信</span><span class="sxs-lookup"><span data-stu-id="a21a9-142">Send to Conversation</span></span> | <span data-ttu-id="a21a9-143">2 </span><span class="sxs-lookup"><span data-stu-id="a21a9-143">2</span></span> | <span data-ttu-id="a21a9-144">8 </span><span class="sxs-lookup"><span data-stu-id="a21a9-144">8</span></span> |
| <span data-ttu-id="a21a9-145">会話に送信</span><span class="sxs-lookup"><span data-stu-id="a21a9-145">Send to Conversation</span></span> | <span data-ttu-id="a21a9-146">31</span><span class="sxs-lookup"><span data-stu-id="a21a9-146">30</span></span> | <span data-ttu-id="a21a9-147">60</span><span class="sxs-lookup"><span data-stu-id="a21a9-147">60</span></span> |
| <span data-ttu-id="a21a9-148">会話に送信</span><span class="sxs-lookup"><span data-stu-id="a21a9-148">Send to Conversation</span></span> | <span data-ttu-id="a21a9-149">3600</span><span class="sxs-lookup"><span data-stu-id="a21a9-149">3600</span></span> | <span data-ttu-id="a21a9-150">1800</span><span class="sxs-lookup"><span data-stu-id="a21a9-150">1800</span></span> |
| <span data-ttu-id="a21a9-151">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="a21a9-151">Create Conversation</span></span> | <span data-ttu-id="a21a9-152">1 </span><span class="sxs-lookup"><span data-stu-id="a21a9-152">1</span></span> | <span data-ttu-id="a21a9-153">7 </span><span class="sxs-lookup"><span data-stu-id="a21a9-153">7</span></span> |
| <span data-ttu-id="a21a9-154">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="a21a9-154">Create Conversation</span></span> | <span data-ttu-id="a21a9-155">2 </span><span class="sxs-lookup"><span data-stu-id="a21a9-155">2</span></span> | <span data-ttu-id="a21a9-156">8 </span><span class="sxs-lookup"><span data-stu-id="a21a9-156">8</span></span> |
| <span data-ttu-id="a21a9-157">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="a21a9-157">Create Conversation</span></span> | <span data-ttu-id="a21a9-158">31</span><span class="sxs-lookup"><span data-stu-id="a21a9-158">30</span></span> | <span data-ttu-id="a21a9-159">60</span><span class="sxs-lookup"><span data-stu-id="a21a9-159">60</span></span> |
| <span data-ttu-id="a21a9-160">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="a21a9-160">Create Conversation</span></span> | <span data-ttu-id="a21a9-161">3600</span><span class="sxs-lookup"><span data-stu-id="a21a9-161">3600</span></span> | <span data-ttu-id="a21a9-162">1800</span><span class="sxs-lookup"><span data-stu-id="a21a9-162">1800</span></span> |
| <span data-ttu-id="a21a9-163">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="a21a9-163">Get Conversation Members</span></span>| <span data-ttu-id="a21a9-164">1 </span><span class="sxs-lookup"><span data-stu-id="a21a9-164">1</span></span> | <span data-ttu-id="a21a9-165">14 </span><span class="sxs-lookup"><span data-stu-id="a21a9-165">14</span></span> |
| <span data-ttu-id="a21a9-166">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="a21a9-166">Get Conversation Members</span></span>| <span data-ttu-id="a21a9-167">2 </span><span class="sxs-lookup"><span data-stu-id="a21a9-167">2</span></span> | <span data-ttu-id="a21a9-168">16 </span><span class="sxs-lookup"><span data-stu-id="a21a9-168">16</span></span> |
| <span data-ttu-id="a21a9-169">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="a21a9-169">Get Conversation Members</span></span>| <span data-ttu-id="a21a9-170">31</span><span class="sxs-lookup"><span data-stu-id="a21a9-170">30</span></span> | <span data-ttu-id="a21a9-171">120</span><span class="sxs-lookup"><span data-stu-id="a21a9-171">120</span></span> |
| <span data-ttu-id="a21a9-172">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="a21a9-172">Get Conversation Members</span></span>| <span data-ttu-id="a21a9-173">3600</span><span class="sxs-lookup"><span data-stu-id="a21a9-173">3600</span></span> | <span data-ttu-id="a21a9-174">3600</span><span class="sxs-lookup"><span data-stu-id="a21a9-174">3600</span></span> |
| <span data-ttu-id="a21a9-175">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="a21a9-175">Get Conversations</span></span> | <span data-ttu-id="a21a9-176">1 </span><span class="sxs-lookup"><span data-stu-id="a21a9-176">1</span></span> | <span data-ttu-id="a21a9-177">14 </span><span class="sxs-lookup"><span data-stu-id="a21a9-177">14</span></span> |
| <span data-ttu-id="a21a9-178">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="a21a9-178">Get Conversations</span></span> | <span data-ttu-id="a21a9-179">2 </span><span class="sxs-lookup"><span data-stu-id="a21a9-179">2</span></span> | <span data-ttu-id="a21a9-180">16 </span><span class="sxs-lookup"><span data-stu-id="a21a9-180">16</span></span> |
| <span data-ttu-id="a21a9-181">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="a21a9-181">Get Conversations</span></span> | <span data-ttu-id="a21a9-182">31</span><span class="sxs-lookup"><span data-stu-id="a21a9-182">30</span></span> | <span data-ttu-id="a21a9-183">120</span><span class="sxs-lookup"><span data-stu-id="a21a9-183">120</span></span> |
| <span data-ttu-id="a21a9-184">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="a21a9-184">Get Conversations</span></span> | <span data-ttu-id="a21a9-185">3600</span><span class="sxs-lookup"><span data-stu-id="a21a9-185">3600</span></span> | <span data-ttu-id="a21a9-186">3600</span><span class="sxs-lookup"><span data-stu-id="a21a9-186">3600</span></span> |

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="a21a9-187">すべてのボットに対するスレッド数の制限</span><span class="sxs-lookup"><span data-stu-id="a21a9-187">Per thread limit for all bots</span></span>

<span data-ttu-id="a21a9-188">この制限は、すべてのボットが1つの会話で生成できるトラフィックを制御します。</span><span class="sxs-lookup"><span data-stu-id="a21a9-188">This limit controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="a21a9-189">ここでの会話は、ボットとユーザー、グループチャット、またはチーム内のチャネルの間で1:1 です。</span><span class="sxs-lookup"><span data-stu-id="a21a9-189">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="a21a9-190">**シナリオ**</span><span class="sxs-lookup"><span data-stu-id="a21a9-190">**Scenario**</span></span> | <span data-ttu-id="a21a9-191">**期間 (秒)**</span><span class="sxs-lookup"><span data-stu-id="a21a9-191">**Time-period (sec)**</span></span> | <span data-ttu-id="a21a9-192">**許可される最大操作数**</span><span class="sxs-lookup"><span data-stu-id="a21a9-192">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a21a9-193">会話に送信</span><span class="sxs-lookup"><span data-stu-id="a21a9-193">Send to Conversation</span></span> | <span data-ttu-id="a21a9-194">1 </span><span class="sxs-lookup"><span data-stu-id="a21a9-194">1</span></span> | <span data-ttu-id="a21a9-195">14 </span><span class="sxs-lookup"><span data-stu-id="a21a9-195">14</span></span> |
| <span data-ttu-id="a21a9-196">会話に送信</span><span class="sxs-lookup"><span data-stu-id="a21a9-196">Send to Conversation</span></span> | <span data-ttu-id="a21a9-197">2 </span><span class="sxs-lookup"><span data-stu-id="a21a9-197">2</span></span> | <span data-ttu-id="a21a9-198">16 </span><span class="sxs-lookup"><span data-stu-id="a21a9-198">16</span></span> |
| <span data-ttu-id="a21a9-199">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="a21a9-199">Create Conversation</span></span> | <span data-ttu-id="a21a9-200">1 </span><span class="sxs-lookup"><span data-stu-id="a21a9-200">1</span></span> | <span data-ttu-id="a21a9-201">14 </span><span class="sxs-lookup"><span data-stu-id="a21a9-201">14</span></span> |
| <span data-ttu-id="a21a9-202">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="a21a9-202">Create Conversation</span></span> | <span data-ttu-id="a21a9-203">2 </span><span class="sxs-lookup"><span data-stu-id="a21a9-203">2</span></span> | <span data-ttu-id="a21a9-204">16 </span><span class="sxs-lookup"><span data-stu-id="a21a9-204">16</span></span> |
| <span data-ttu-id="a21a9-205">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="a21a9-205">CreateConversation</span></span>| <span data-ttu-id="a21a9-206">1 </span><span class="sxs-lookup"><span data-stu-id="a21a9-206">1</span></span> | <span data-ttu-id="a21a9-207">14 </span><span class="sxs-lookup"><span data-stu-id="a21a9-207">14</span></span> |
| <span data-ttu-id="a21a9-208">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="a21a9-208">CreateConversation</span></span>| <span data-ttu-id="a21a9-209">2 </span><span class="sxs-lookup"><span data-stu-id="a21a9-209">2</span></span> | <span data-ttu-id="a21a9-210">16 </span><span class="sxs-lookup"><span data-stu-id="a21a9-210">16</span></span> |
| <span data-ttu-id="a21a9-211">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="a21a9-211">Get Conversation Members</span></span>| <span data-ttu-id="a21a9-212">1 </span><span class="sxs-lookup"><span data-stu-id="a21a9-212">1</span></span> | <span data-ttu-id="a21a9-213">個</span><span class="sxs-lookup"><span data-stu-id="a21a9-213">28</span></span> |
| <span data-ttu-id="a21a9-214">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="a21a9-214">Get Conversation Members</span></span>| <span data-ttu-id="a21a9-215">2 </span><span class="sxs-lookup"><span data-stu-id="a21a9-215">2</span></span> | <span data-ttu-id="a21a9-216">32</span><span class="sxs-lookup"><span data-stu-id="a21a9-216">32</span></span> |
| <span data-ttu-id="a21a9-217">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="a21a9-217">Get Conversations</span></span> | <span data-ttu-id="a21a9-218">1 </span><span class="sxs-lookup"><span data-stu-id="a21a9-218">1</span></span> | <span data-ttu-id="a21a9-219">個</span><span class="sxs-lookup"><span data-stu-id="a21a9-219">28</span></span> |
| <span data-ttu-id="a21a9-220">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="a21a9-220">Get Conversations</span></span> | <span data-ttu-id="a21a9-221">2 </span><span class="sxs-lookup"><span data-stu-id="a21a9-221">2</span></span> | <span data-ttu-id="a21a9-222">32</span><span class="sxs-lookup"><span data-stu-id="a21a9-222">32</span></span> |
