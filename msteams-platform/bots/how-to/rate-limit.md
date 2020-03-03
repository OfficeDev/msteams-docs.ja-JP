---
title: レート制限
description: Microsoft Teams でのレートの制限とベストプラクティス
keywords: teams のボットレート制限
ms.openlocfilehash: 145f65a7e17b833e11631dfc219d9f5732f43bc6
ms.sourcegitcommit: 6c692734a382865531a83b9ebd6f604212f484fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/02/2020
ms.locfileid: "42371766"
---
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a><span data-ttu-id="38853-104">Bot を最適化する: Microsoft Teams でのレートの制限とベストプラクティス</span><span class="sxs-lookup"><span data-stu-id="38853-104">Optimize your bot: rate limiting and best practices in Microsoft Teams</span></span>

<span data-ttu-id="38853-105">一般的な原則として、アプリケーションでは、個々のチャットまたはチャネル会話に投稿するメッセージ数を制限する必要があります。</span><span class="sxs-lookup"><span data-stu-id="38853-105">As a general principle, your application should limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="38853-106">これにより、エンドユーザーに "spammy" を感じない最適な操作性が実現されます。</span><span class="sxs-lookup"><span data-stu-id="38853-106">This ensures an optimal experience that doesn't feel “spammy” to your end users.</span></span>

<span data-ttu-id="38853-107">Microsoft Teams とそのユーザーを保護するために、bot Api rate は受信要求を制限します。</span><span class="sxs-lookup"><span data-stu-id="38853-107">To protect Microsoft Teams and its users, the bot APIs rate-limit incoming requests.</span></span> <span data-ttu-id="38853-108">この制限を超えるアプリは、エラー `HTTP 429 Too Many Requests`状態を受信します。</span><span class="sxs-lookup"><span data-stu-id="38853-108">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="38853-109">すべての要求は、メッセージの送信、チャネルの列挙、名簿の取得など、同じ料金を制限するポリシーに従います。</span><span class="sxs-lookup"><span data-stu-id="38853-109">All requests are subject to the same rate-limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="38853-110">レート制限の正確な値は変更される可能性があるため、API が戻る`HTTP 429 Too Many Requests`ときに、アプリケーションで適切なバックオフ動作を実装することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="38853-110">Because the exact values of rate limits are subject to change, we recommend your application implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handling-rate-limits"></a><span data-ttu-id="38853-111">処理率の制限</span><span class="sxs-lookup"><span data-stu-id="38853-111">Handling rate limits</span></span>

<span data-ttu-id="38853-112">Bot ビルダー SDK 操作を発行するときに、状態`Microsoft.Rest.HttpOperationException`コードを処理および確認できます。</span><span class="sxs-lookup"><span data-stu-id="38853-112">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="38853-113">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="38853-113">Best practices</span></span>

<span data-ttu-id="38853-114">通常、応答を受信`HTTP 429`しないようにするには、簡単な予防措置を講じる必要があります。</span><span class="sxs-lookup"><span data-stu-id="38853-114">In general, you should take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="38853-115">たとえば、同じ個人用またはチャネル会話に対して複数の要求を発行しないようにします。</span><span class="sxs-lookup"><span data-stu-id="38853-115">For instance, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="38853-116">代わりに、API 要求のバッチ処理を検討してください。</span><span class="sxs-lookup"><span data-stu-id="38853-116">Instead, consider batching the API requests.</span></span>

<span data-ttu-id="38853-117">ランダムな変位による指数バックオフを使用することは、429s を処理するために推奨される方法です。</span><span class="sxs-lookup"><span data-stu-id="38853-117">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="38853-118">これにより、複数の要求で再試行時に競合が発生しなくなります。</span><span class="sxs-lookup"><span data-stu-id="38853-118">This ensures that multiple requests don't introduce collisions on retries.</span></span>

## <a name="example-detecting-transient-exceptions"></a><span data-ttu-id="38853-119">例: 一時的な例外を検出する</span><span class="sxs-lookup"><span data-stu-id="38853-119">Example: detecting transient exceptions</span></span>

<span data-ttu-id="38853-120">ここでは、一時的な障害処理アプリケーションブロックによる指数バックオフを使用する例を示します。</span><span class="sxs-lookup"><span data-stu-id="38853-120">Here is a sample using exponential backoff via the Transient Fault Handling Application Block.</span></span>

<span data-ttu-id="38853-121">[一時的なエラー処理](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)を使用して、バックオフと再試行を実行できます。</span><span class="sxs-lookup"><span data-stu-id="38853-121">You can perform backoff and retries using [Transient Fault Handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="38853-122">NuGet パッケージを入手してインストールするためのガイドラインについては、「[一時的なエラー処理アプリケーションブロックをソリューションに追加](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="38853-122">For guidelines on obtaining and installing the NuGet package, see [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)).</span></span> <span data-ttu-id="38853-123">「[一時的なフォールト処理](/azure/architecture/best-practices/transient-faults) *」も参照してください*。</span><span class="sxs-lookup"><span data-stu-id="38853-123">*See also* [Transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

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

## <a name="example-backoff"></a><span data-ttu-id="38853-124">例: バックオフ</span><span class="sxs-lookup"><span data-stu-id="38853-124">Example: backoff</span></span>

<span data-ttu-id="38853-125">速度制限の検出に加えて、指数バックオフを実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="38853-125">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

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

<span data-ttu-id="38853-126">前に説明した`System.Action`再試行ポリシーを使用して、メソッドを実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="38853-126">You can also perform a `System.Action` method execution with the retry policy described above.</span></span> <span data-ttu-id="38853-127">参照されるライブラリでは、固定の間隔または線形バックオフメカニズムを指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="38853-127">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="38853-128">値と戦略を構成ファイルに格納して、実行時に値を微調整および調整することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="38853-128">We recommend storing the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="38853-129">詳細については、この便利な「再試行[パターン](/azure/architecture/patterns/retry)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="38853-129">For more information, check out this handy guide on various retry patterns: [Retry pattern](/azure/architecture/patterns/retry).</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="38853-130">スレッドの制限ごとに1つの bot</span><span class="sxs-lookup"><span data-stu-id="38853-130">Per bot per thread limit</span></span>

>[!NOTE]
><span data-ttu-id="38853-131">サービスレベルでのメッセージ分割は、予想される1秒あたりの要求数 (RPS) を超える結果になります。</span><span class="sxs-lookup"><span data-stu-id="38853-131">Message splitting at the service level will result in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="38853-132">制限への接近を懸念している場合は、前述のバックオフ戦略を実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="38853-132">If you're concerned about approaching the limits, you should implement the backoff strategy described above.</span></span> <span data-ttu-id="38853-133">以下の値は、見積のみを対象としています。</span><span class="sxs-lookup"><span data-stu-id="38853-133">The values provided below are for estimation only.</span></span>

<span data-ttu-id="38853-134">この制限は、bot が1回の会話で生成できるトラフィックを制御します。</span><span class="sxs-lookup"><span data-stu-id="38853-134">This limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="38853-135">ここでの会話は、ボットとユーザー、グループチャット、またはチーム内のチャネルの間で1:1 です。</span><span class="sxs-lookup"><span data-stu-id="38853-135">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="38853-136">**シナリオ**</span><span class="sxs-lookup"><span data-stu-id="38853-136">**Scenario**</span></span> | <span data-ttu-id="38853-137">**期間 (秒)**</span><span class="sxs-lookup"><span data-stu-id="38853-137">**Time-period (sec)**</span></span> | <span data-ttu-id="38853-138">**許可される最大操作数**</span><span class="sxs-lookup"><span data-stu-id="38853-138">**Max allowed operations**</span></span> |
| --- | --- | --- |
|| <span data-ttu-id="38853-139">1-d</span><span class="sxs-lookup"><span data-stu-id="38853-139">1</span></span> | <span data-ttu-id="38853-140">7</span><span class="sxs-lookup"><span data-stu-id="38853-140">7</span></span> |
| <span data-ttu-id="38853-141">会話に送信</span><span class="sxs-lookup"><span data-stu-id="38853-141">Send to Conversation</span></span> | <span data-ttu-id="38853-142">pbm-2</span><span class="sxs-lookup"><span data-stu-id="38853-142">2</span></span> | <span data-ttu-id="38853-143">~</span><span class="sxs-lookup"><span data-stu-id="38853-143">8</span></span> |
| <span data-ttu-id="38853-144">会話に送信</span><span class="sxs-lookup"><span data-stu-id="38853-144">Send to Conversation</span></span> | <span data-ttu-id="38853-145">31</span><span class="sxs-lookup"><span data-stu-id="38853-145">30</span></span> | <span data-ttu-id="38853-146">60</span><span class="sxs-lookup"><span data-stu-id="38853-146">60</span></span> |
| <span data-ttu-id="38853-147">会話に送信</span><span class="sxs-lookup"><span data-stu-id="38853-147">Send to Conversation</span></span> | <span data-ttu-id="38853-148">3600</span><span class="sxs-lookup"><span data-stu-id="38853-148">3600</span></span> | <span data-ttu-id="38853-149">1800</span><span class="sxs-lookup"><span data-stu-id="38853-149">1800</span></span> |
| <span data-ttu-id="38853-150">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="38853-150">Create Conversation</span></span> | <span data-ttu-id="38853-151">1-d</span><span class="sxs-lookup"><span data-stu-id="38853-151">1</span></span> | <span data-ttu-id="38853-152">7</span><span class="sxs-lookup"><span data-stu-id="38853-152">7</span></span> |
| <span data-ttu-id="38853-153">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="38853-153">Create Conversation</span></span> | <span data-ttu-id="38853-154">pbm-2</span><span class="sxs-lookup"><span data-stu-id="38853-154">2</span></span> | <span data-ttu-id="38853-155">~</span><span class="sxs-lookup"><span data-stu-id="38853-155">8</span></span> |
| <span data-ttu-id="38853-156">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="38853-156">Create Conversation</span></span> | <span data-ttu-id="38853-157">31</span><span class="sxs-lookup"><span data-stu-id="38853-157">30</span></span> | <span data-ttu-id="38853-158">60</span><span class="sxs-lookup"><span data-stu-id="38853-158">60</span></span> |
| <span data-ttu-id="38853-159">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="38853-159">Create Conversation</span></span> | <span data-ttu-id="38853-160">3600</span><span class="sxs-lookup"><span data-stu-id="38853-160">3600</span></span> | <span data-ttu-id="38853-161">1800</span><span class="sxs-lookup"><span data-stu-id="38853-161">1800</span></span> |
| <span data-ttu-id="38853-162">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="38853-162">Get Conversation Members</span></span>| <span data-ttu-id="38853-163">1-d</span><span class="sxs-lookup"><span data-stu-id="38853-163">1</span></span> | <span data-ttu-id="38853-164">14 </span><span class="sxs-lookup"><span data-stu-id="38853-164">14</span></span> |
| <span data-ttu-id="38853-165">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="38853-165">Get Conversation Members</span></span>| <span data-ttu-id="38853-166">pbm-2</span><span class="sxs-lookup"><span data-stu-id="38853-166">2</span></span> | <span data-ttu-id="38853-167">16 </span><span class="sxs-lookup"><span data-stu-id="38853-167">16</span></span> |
| <span data-ttu-id="38853-168">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="38853-168">Get Conversation Members</span></span>| <span data-ttu-id="38853-169">31</span><span class="sxs-lookup"><span data-stu-id="38853-169">30</span></span> | <span data-ttu-id="38853-170">120</span><span class="sxs-lookup"><span data-stu-id="38853-170">120</span></span> |
| <span data-ttu-id="38853-171">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="38853-171">Get Conversation Members</span></span>| <span data-ttu-id="38853-172">3600</span><span class="sxs-lookup"><span data-stu-id="38853-172">3600</span></span> | <span data-ttu-id="38853-173">3600</span><span class="sxs-lookup"><span data-stu-id="38853-173">3600</span></span> |
| <span data-ttu-id="38853-174">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="38853-174">Get Conversations</span></span> | <span data-ttu-id="38853-175">1-d</span><span class="sxs-lookup"><span data-stu-id="38853-175">1</span></span> | <span data-ttu-id="38853-176">14 </span><span class="sxs-lookup"><span data-stu-id="38853-176">14</span></span> |
| <span data-ttu-id="38853-177">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="38853-177">Get Conversations</span></span> | <span data-ttu-id="38853-178">pbm-2</span><span class="sxs-lookup"><span data-stu-id="38853-178">2</span></span> | <span data-ttu-id="38853-179">16 </span><span class="sxs-lookup"><span data-stu-id="38853-179">16</span></span> |
| <span data-ttu-id="38853-180">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="38853-180">Get Conversations</span></span> | <span data-ttu-id="38853-181">31</span><span class="sxs-lookup"><span data-stu-id="38853-181">30</span></span> | <span data-ttu-id="38853-182">120</span><span class="sxs-lookup"><span data-stu-id="38853-182">120</span></span> |
| <span data-ttu-id="38853-183">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="38853-183">Get Conversations</span></span> | <span data-ttu-id="38853-184">3600</span><span class="sxs-lookup"><span data-stu-id="38853-184">3600</span></span> | <span data-ttu-id="38853-185">3600</span><span class="sxs-lookup"><span data-stu-id="38853-185">3600</span></span> |

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="38853-186">すべてのボットに対するスレッド数の制限</span><span class="sxs-lookup"><span data-stu-id="38853-186">Per thread limit for all bots</span></span>

<span data-ttu-id="38853-187">この制限は、すべてのボットが1つの会話で生成できるトラフィックを制御します。</span><span class="sxs-lookup"><span data-stu-id="38853-187">This limit controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="38853-188">ここでの会話は、ボットとユーザー、グループチャット、またはチーム内のチャネルの間で1:1 です。</span><span class="sxs-lookup"><span data-stu-id="38853-188">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="38853-189">**シナリオ**</span><span class="sxs-lookup"><span data-stu-id="38853-189">**Scenario**</span></span> | <span data-ttu-id="38853-190">**期間 (秒)**</span><span class="sxs-lookup"><span data-stu-id="38853-190">**Time-period (sec)**</span></span> | <span data-ttu-id="38853-191">**許可される最大操作数**</span><span class="sxs-lookup"><span data-stu-id="38853-191">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38853-192">会話に送信</span><span class="sxs-lookup"><span data-stu-id="38853-192">Send to Conversation</span></span> | <span data-ttu-id="38853-193">1-d</span><span class="sxs-lookup"><span data-stu-id="38853-193">1</span></span> | <span data-ttu-id="38853-194">14 </span><span class="sxs-lookup"><span data-stu-id="38853-194">14</span></span> |
| <span data-ttu-id="38853-195">会話に送信</span><span class="sxs-lookup"><span data-stu-id="38853-195">Send to Conversation</span></span> | <span data-ttu-id="38853-196">pbm-2</span><span class="sxs-lookup"><span data-stu-id="38853-196">2</span></span> | <span data-ttu-id="38853-197">16 </span><span class="sxs-lookup"><span data-stu-id="38853-197">16</span></span> |
| <span data-ttu-id="38853-198">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="38853-198">Create Conversation</span></span> | <span data-ttu-id="38853-199">1-d</span><span class="sxs-lookup"><span data-stu-id="38853-199">1</span></span> | <span data-ttu-id="38853-200">14 </span><span class="sxs-lookup"><span data-stu-id="38853-200">14</span></span> |
| <span data-ttu-id="38853-201">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="38853-201">Create Conversation</span></span> | <span data-ttu-id="38853-202">pbm-2</span><span class="sxs-lookup"><span data-stu-id="38853-202">2</span></span> | <span data-ttu-id="38853-203">16 </span><span class="sxs-lookup"><span data-stu-id="38853-203">16</span></span> |
| <span data-ttu-id="38853-204">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="38853-204">CreateConversation</span></span>| <span data-ttu-id="38853-205">1-d</span><span class="sxs-lookup"><span data-stu-id="38853-205">1</span></span> | <span data-ttu-id="38853-206">14 </span><span class="sxs-lookup"><span data-stu-id="38853-206">14</span></span> |
| <span data-ttu-id="38853-207">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="38853-207">CreateConversation</span></span>| <span data-ttu-id="38853-208">pbm-2</span><span class="sxs-lookup"><span data-stu-id="38853-208">2</span></span> | <span data-ttu-id="38853-209">16 </span><span class="sxs-lookup"><span data-stu-id="38853-209">16</span></span> |
| <span data-ttu-id="38853-210">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="38853-210">Get Conversation Members</span></span>| <span data-ttu-id="38853-211">1-d</span><span class="sxs-lookup"><span data-stu-id="38853-211">1</span></span> | <span data-ttu-id="38853-212">個</span><span class="sxs-lookup"><span data-stu-id="38853-212">28</span></span> |
| <span data-ttu-id="38853-213">会話メンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="38853-213">Get Conversation Members</span></span>| <span data-ttu-id="38853-214">pbm-2</span><span class="sxs-lookup"><span data-stu-id="38853-214">2</span></span> | <span data-ttu-id="38853-215">32</span><span class="sxs-lookup"><span data-stu-id="38853-215">32</span></span> |
| <span data-ttu-id="38853-216">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="38853-216">Get Conversations</span></span> | <span data-ttu-id="38853-217">1-d</span><span class="sxs-lookup"><span data-stu-id="38853-217">1</span></span> | <span data-ttu-id="38853-218">個</span><span class="sxs-lookup"><span data-stu-id="38853-218">28</span></span> |
| <span data-ttu-id="38853-219">会話を取得する</span><span class="sxs-lookup"><span data-stu-id="38853-219">Get Conversations</span></span> | <span data-ttu-id="38853-220">pbm-2</span><span class="sxs-lookup"><span data-stu-id="38853-220">2</span></span> | <span data-ttu-id="38853-221">32</span><span class="sxs-lookup"><span data-stu-id="38853-221">32</span></span> |

## <a name="bot-per-data-center-limit"></a><span data-ttu-id="38853-222">データセンターあたりの Bot 数の制限</span><span class="sxs-lookup"><span data-stu-id="38853-222">Bot per data center limit</span></span>

<span data-ttu-id="38853-223">この制限は、1つのデータセンター (複数のテナント) 内のすべてのスレッド間でボットが生成できるトラフィックを制御します。</span><span class="sxs-lookup"><span data-stu-id="38853-223">This limit controls the traffic that a bot is allowed to generate across all threads in a data center (across multiple tenants).</span></span>

|<span data-ttu-id="38853-224">**期間 (秒)**</span><span class="sxs-lookup"><span data-stu-id="38853-224">**Time-period (sec)**</span></span> | <span data-ttu-id="38853-225">**許可される最大操作数**</span><span class="sxs-lookup"><span data-stu-id="38853-225">**Max allowed operations**</span></span> |
| --- | --- |
| <span data-ttu-id="38853-226">1-d</span><span class="sxs-lookup"><span data-stu-id="38853-226">1</span></span> | <span data-ttu-id="38853-227">1280</span><span class="sxs-lookup"><span data-stu-id="38853-227">20</span></span> |
| <span data-ttu-id="38853-228">1800</span><span class="sxs-lookup"><span data-stu-id="38853-228">1800</span></span> | <span data-ttu-id="38853-229">8000</span><span class="sxs-lookup"><span data-stu-id="38853-229">8000</span></span> |
| <span data-ttu-id="38853-230">3600</span><span class="sxs-lookup"><span data-stu-id="38853-230">3600</span></span> | <span data-ttu-id="38853-231">15000</span><span class="sxs-lookup"><span data-stu-id="38853-231">15000</span></span> |
