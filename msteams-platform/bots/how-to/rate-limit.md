---
title: レート制限
description: Microsoft Teams のレート制限とベスト プラクティス
keywords: Teams ボットのレート制限
ms.openlocfilehash: 840737178234bcd6e2da1925b0031083717e2b91
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034684"
---
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a><span data-ttu-id="cc2ed-104">ボットを最適化する: Microsoft Teams でのレート制限とベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="cc2ed-104">Optimize your bot: rate limiting and best practices in Microsoft Teams</span></span>

<span data-ttu-id="cc2ed-105">一般的な原則として、アプリケーションは投稿するメッセージの数を個々のチャットまたはチャネルの会話に制限する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-105">As a general principle, your application should limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="cc2ed-106">これにより、エンド ユーザーに "スパム" を感じない最適なエクスペリエンスが保証されます。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-106">This ensures an optimal experience that doesn't feel “spammy” to your end users.</span></span>

<span data-ttu-id="cc2ed-107">Microsoft Teams とそのユーザーを保護するために、ボット API は受信要求をレート制限します。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-107">To protect Microsoft Teams and its users, the bot APIs rate-limit incoming requests.</span></span> <span data-ttu-id="cc2ed-108">この制限を超えるアプリは、エラー状態 `HTTP 429 Too Many Requests` を受け取る。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-108">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="cc2ed-109">すべての要求は、メッセージの送信、チャネル列挙、名簿フェッチなど、同じレート制限ポリシーの対象です。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-109">All requests are subject to the same rate-limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="cc2ed-110">レート制限の正確な値は変更される可能性があります。API が返される場合は、アプリケーションで適切なバックオフ動作を実装することをお勧めします `HTTP 429 Too Many Requests` 。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-110">Because the exact values of rate limits are subject to change, we recommend your application implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handling-rate-limits"></a><span data-ttu-id="cc2ed-111">レート制限の処理</span><span class="sxs-lookup"><span data-stu-id="cc2ed-111">Handling rate limits</span></span>

<span data-ttu-id="cc2ed-112">ボット ビルダー SDK 操作を発行する場合は、状態コードを処理 `Microsoft.Rest.HttpOperationException` して確認できます。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-112">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="cc2ed-113">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="cc2ed-113">Best practices</span></span>

<span data-ttu-id="cc2ed-114">一般に、応答を受信しないように、簡単な予防措置を講 `HTTP 429` じるべきです。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-114">In general, you should take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="cc2ed-115">たとえば、同じ個人またはチャネルの会話に対して複数の要求を発行しないようにします。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-115">For instance, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="cc2ed-116">代わりに、API 要求のバッチ処理を検討してください。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-116">Instead, consider batching the API requests.</span></span>

<span data-ttu-id="cc2ed-117">ランダムなジッターで指数バックオフを使用する方法は、429 を処理するための推奨される方法です。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-117">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="cc2ed-118">これにより、複数の要求が再試行時に競合を発生しない。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-118">This ensures that multiple requests don't introduce collisions on retries.</span></span>

## <a name="example-detecting-transient-exceptions"></a><span data-ttu-id="cc2ed-119">例: 一時的な例外の検出</span><span class="sxs-lookup"><span data-stu-id="cc2ed-119">Example: detecting transient exceptions</span></span>

<span data-ttu-id="cc2ed-120">一時的な障害処理アプリケーション ブロックを介して指数バックオフを使用するサンプルを次に示します。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-120">Here is a sample using exponential backoff via the Transient Fault Handling Application Block.</span></span>

<span data-ttu-id="cc2ed-121">一時的な障害処理を使用して、バックオフと [再試行を実行できます](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-121">You can perform backoff and retries using [Transient Fault Handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="cc2ed-122">NuGet パッケージの取得とインストールに関するガイドラインについては、「一時的な障害処理アプリケーション ブロックをソリューションに追加する」 [を参照してください](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-122">For guidelines on obtaining and installing the NuGet package, see [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)).</span></span> <span data-ttu-id="cc2ed-123">*「一時的な*[障害の処理」も参照してください](/azure/architecture/best-practices/transient-faults)。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-123">*See also* [Transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

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

## <a name="example-backoff"></a><span data-ttu-id="cc2ed-124">例: バックオフ</span><span class="sxs-lookup"><span data-stu-id="cc2ed-124">Example: backoff</span></span>

<span data-ttu-id="cc2ed-125">レート制限の検出に加えて、指数バックオフも実行できます。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-125">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

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

<span data-ttu-id="cc2ed-126">また、前述の再試行 `System.Action` ポリシーを使用してメソッドの実行を実行できます。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-126">You can also perform a `System.Action` method execution with the retry policy described above.</span></span> <span data-ttu-id="cc2ed-127">参照されるライブラリでは、固定間隔または線形バックオフ メカニズムを指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-127">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="cc2ed-128">実行時に値を微調整および調整するには、値と戦略を構成ファイルに格納することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-128">We recommend storing the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="cc2ed-129">詳細については、さまざまな再試行パターンに関するこの便利なガイド:再試行 [パターンを参照してください](/azure/architecture/patterns/retry)。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-129">For more information, check out this handy guide on various retry patterns: [Retry pattern](/azure/architecture/patterns/retry).</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="cc2ed-130">スレッドごとのボットごとの制限</span><span class="sxs-lookup"><span data-stu-id="cc2ed-130">Per bot per thread limit</span></span>

>[!NOTE]
><span data-ttu-id="cc2ed-131">サービス レベルでのメッセージの分割は、予想される要求 /秒 (RPS) を超える結果になります。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-131">Message splitting at the service level will result in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="cc2ed-132">制限に近づくのが懸念される場合は、前述のバックオフ戦略を実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-132">If you're concerned about approaching the limits, you should implement the backoff strategy described above.</span></span> <span data-ttu-id="cc2ed-133">以下に示す値は、見積もり専用です。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-133">The values provided below are for estimation only.</span></span>

<span data-ttu-id="cc2ed-134">この制限は、ボットが 1 回の会話で生成できるトラフィックを制御します。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-134">This limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="cc2ed-135">ここでの会話は、ボットとユーザー、グループ チャット、またはチーム内のチャネルの間で 1:1 です。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-135">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="cc2ed-136">**シナリオ**</span><span class="sxs-lookup"><span data-stu-id="cc2ed-136">**Scenario**</span></span> | <span data-ttu-id="cc2ed-137">**期間 (秒)**</span><span class="sxs-lookup"><span data-stu-id="cc2ed-137">**Time-period (sec)**</span></span> | <span data-ttu-id="cc2ed-138">**許可される操作の上限**</span><span class="sxs-lookup"><span data-stu-id="cc2ed-138">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc2ed-139">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="cc2ed-139">Send to Conversation</span></span> | <span data-ttu-id="cc2ed-140">1</span><span class="sxs-lookup"><span data-stu-id="cc2ed-140">1</span></span> | <span data-ttu-id="cc2ed-141">7</span><span class="sxs-lookup"><span data-stu-id="cc2ed-141">7</span></span> |
| <span data-ttu-id="cc2ed-142">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="cc2ed-142">Send to Conversation</span></span> | <span data-ttu-id="cc2ed-143">2</span><span class="sxs-lookup"><span data-stu-id="cc2ed-143">2</span></span> | <span data-ttu-id="cc2ed-144">8</span><span class="sxs-lookup"><span data-stu-id="cc2ed-144">8</span></span> |
| <span data-ttu-id="cc2ed-145">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="cc2ed-145">Send to Conversation</span></span> | <span data-ttu-id="cc2ed-146">30</span><span class="sxs-lookup"><span data-stu-id="cc2ed-146">30</span></span> | <span data-ttu-id="cc2ed-147">60</span><span class="sxs-lookup"><span data-stu-id="cc2ed-147">60</span></span> |
| <span data-ttu-id="cc2ed-148">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="cc2ed-148">Send to Conversation</span></span> | <span data-ttu-id="cc2ed-149">3600</span><span class="sxs-lookup"><span data-stu-id="cc2ed-149">3600</span></span> | <span data-ttu-id="cc2ed-150">1800</span><span class="sxs-lookup"><span data-stu-id="cc2ed-150">1800</span></span> |
| <span data-ttu-id="cc2ed-151">会話の作成</span><span class="sxs-lookup"><span data-stu-id="cc2ed-151">Create Conversation</span></span> | <span data-ttu-id="cc2ed-152">1</span><span class="sxs-lookup"><span data-stu-id="cc2ed-152">1</span></span> | <span data-ttu-id="cc2ed-153">7</span><span class="sxs-lookup"><span data-stu-id="cc2ed-153">7</span></span> |
| <span data-ttu-id="cc2ed-154">会話の作成</span><span class="sxs-lookup"><span data-stu-id="cc2ed-154">Create Conversation</span></span> | <span data-ttu-id="cc2ed-155">2</span><span class="sxs-lookup"><span data-stu-id="cc2ed-155">2</span></span> | <span data-ttu-id="cc2ed-156">8</span><span class="sxs-lookup"><span data-stu-id="cc2ed-156">8</span></span> |
| <span data-ttu-id="cc2ed-157">会話の作成</span><span class="sxs-lookup"><span data-stu-id="cc2ed-157">Create Conversation</span></span> | <span data-ttu-id="cc2ed-158">30</span><span class="sxs-lookup"><span data-stu-id="cc2ed-158">30</span></span> | <span data-ttu-id="cc2ed-159">60</span><span class="sxs-lookup"><span data-stu-id="cc2ed-159">60</span></span> |
| <span data-ttu-id="cc2ed-160">会話の作成</span><span class="sxs-lookup"><span data-stu-id="cc2ed-160">Create Conversation</span></span> | <span data-ttu-id="cc2ed-161">3600</span><span class="sxs-lookup"><span data-stu-id="cc2ed-161">3600</span></span> | <span data-ttu-id="cc2ed-162">1800</span><span class="sxs-lookup"><span data-stu-id="cc2ed-162">1800</span></span> |
| <span data-ttu-id="cc2ed-163">会話メンバーの取得</span><span class="sxs-lookup"><span data-stu-id="cc2ed-163">Get Conversation Members</span></span>| <span data-ttu-id="cc2ed-164">1</span><span class="sxs-lookup"><span data-stu-id="cc2ed-164">1</span></span> | <span data-ttu-id="cc2ed-165">14 </span><span class="sxs-lookup"><span data-stu-id="cc2ed-165">14</span></span> |
| <span data-ttu-id="cc2ed-166">会話メンバーの取得</span><span class="sxs-lookup"><span data-stu-id="cc2ed-166">Get Conversation Members</span></span>| <span data-ttu-id="cc2ed-167">2</span><span class="sxs-lookup"><span data-stu-id="cc2ed-167">2</span></span> | <span data-ttu-id="cc2ed-168">16 </span><span class="sxs-lookup"><span data-stu-id="cc2ed-168">16</span></span> |
| <span data-ttu-id="cc2ed-169">会話メンバーの取得</span><span class="sxs-lookup"><span data-stu-id="cc2ed-169">Get Conversation Members</span></span>| <span data-ttu-id="cc2ed-170">30</span><span class="sxs-lookup"><span data-stu-id="cc2ed-170">30</span></span> | <span data-ttu-id="cc2ed-171">120</span><span class="sxs-lookup"><span data-stu-id="cc2ed-171">120</span></span> |
| <span data-ttu-id="cc2ed-172">会話メンバーの取得</span><span class="sxs-lookup"><span data-stu-id="cc2ed-172">Get Conversation Members</span></span>| <span data-ttu-id="cc2ed-173">3600</span><span class="sxs-lookup"><span data-stu-id="cc2ed-173">3600</span></span> | <span data-ttu-id="cc2ed-174">3600</span><span class="sxs-lookup"><span data-stu-id="cc2ed-174">3600</span></span> |
| <span data-ttu-id="cc2ed-175">会話の取得</span><span class="sxs-lookup"><span data-stu-id="cc2ed-175">Get Conversations</span></span> | <span data-ttu-id="cc2ed-176">1</span><span class="sxs-lookup"><span data-stu-id="cc2ed-176">1</span></span> | <span data-ttu-id="cc2ed-177">14 </span><span class="sxs-lookup"><span data-stu-id="cc2ed-177">14</span></span> |
| <span data-ttu-id="cc2ed-178">会話の取得</span><span class="sxs-lookup"><span data-stu-id="cc2ed-178">Get Conversations</span></span> | <span data-ttu-id="cc2ed-179">2</span><span class="sxs-lookup"><span data-stu-id="cc2ed-179">2</span></span> | <span data-ttu-id="cc2ed-180">16 </span><span class="sxs-lookup"><span data-stu-id="cc2ed-180">16</span></span> |
| <span data-ttu-id="cc2ed-181">会話の取得</span><span class="sxs-lookup"><span data-stu-id="cc2ed-181">Get Conversations</span></span> | <span data-ttu-id="cc2ed-182">30</span><span class="sxs-lookup"><span data-stu-id="cc2ed-182">30</span></span> | <span data-ttu-id="cc2ed-183">120</span><span class="sxs-lookup"><span data-stu-id="cc2ed-183">120</span></span> |
| <span data-ttu-id="cc2ed-184">会話の取得</span><span class="sxs-lookup"><span data-stu-id="cc2ed-184">Get Conversations</span></span> | <span data-ttu-id="cc2ed-185">3600</span><span class="sxs-lookup"><span data-stu-id="cc2ed-185">3600</span></span> | <span data-ttu-id="cc2ed-186">3600</span><span class="sxs-lookup"><span data-stu-id="cc2ed-186">3600</span></span> |

>[!NOTE]
> <span data-ttu-id="cc2ed-187">以前のバージョンと `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` API は非推奨です。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-187">Previous versions of `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs are being deprecated.</span></span> <span data-ttu-id="cc2ed-188">1 分あたり 5 つの要求に調整され、チームごとに最大 10K のメンバーが返されます。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-188">They will be throttled to 5 requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="cc2ed-189">ボット フレームワーク SDK と、ページ分割された最新の API エンドポイントを使用するコードを更新するには、「チームおよびチャット メンバーのボット API の変更」 [を参照してください](../../resources/team-chat-member-api-changes.md)。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-189">To update your Bot Framework SDK and the code to use the latest paginated API endpoints, see [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span></span>

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="cc2ed-190">すべてのボットのスレッドごとの制限</span><span class="sxs-lookup"><span data-stu-id="cc2ed-190">Per thread limit for all bots</span></span>

<span data-ttu-id="cc2ed-191">この制限は、すべてのボットが 1 回の会話で生成できるトラフィックを制御します。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-191">This limit controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="cc2ed-192">ここでの会話は、ボットとユーザー、グループ チャット、またはチーム内のチャネルの間で 1:1 です。</span><span class="sxs-lookup"><span data-stu-id="cc2ed-192">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="cc2ed-193">**シナリオ**</span><span class="sxs-lookup"><span data-stu-id="cc2ed-193">**Scenario**</span></span> | <span data-ttu-id="cc2ed-194">**期間 (秒)**</span><span class="sxs-lookup"><span data-stu-id="cc2ed-194">**Time-period (sec)**</span></span> | <span data-ttu-id="cc2ed-195">**許可される操作の上限**</span><span class="sxs-lookup"><span data-stu-id="cc2ed-195">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc2ed-196">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="cc2ed-196">Send to Conversation</span></span> | <span data-ttu-id="cc2ed-197">1</span><span class="sxs-lookup"><span data-stu-id="cc2ed-197">1</span></span> | <span data-ttu-id="cc2ed-198">14 </span><span class="sxs-lookup"><span data-stu-id="cc2ed-198">14</span></span> |
| <span data-ttu-id="cc2ed-199">会話に送信する</span><span class="sxs-lookup"><span data-stu-id="cc2ed-199">Send to Conversation</span></span> | <span data-ttu-id="cc2ed-200">2</span><span class="sxs-lookup"><span data-stu-id="cc2ed-200">2</span></span> | <span data-ttu-id="cc2ed-201">16 </span><span class="sxs-lookup"><span data-stu-id="cc2ed-201">16</span></span> |
| <span data-ttu-id="cc2ed-202">会話の作成</span><span class="sxs-lookup"><span data-stu-id="cc2ed-202">Create Conversation</span></span> | <span data-ttu-id="cc2ed-203">1</span><span class="sxs-lookup"><span data-stu-id="cc2ed-203">1</span></span> | <span data-ttu-id="cc2ed-204">14 </span><span class="sxs-lookup"><span data-stu-id="cc2ed-204">14</span></span> |
| <span data-ttu-id="cc2ed-205">会話の作成</span><span class="sxs-lookup"><span data-stu-id="cc2ed-205">Create Conversation</span></span> | <span data-ttu-id="cc2ed-206">2</span><span class="sxs-lookup"><span data-stu-id="cc2ed-206">2</span></span> | <span data-ttu-id="cc2ed-207">16 </span><span class="sxs-lookup"><span data-stu-id="cc2ed-207">16</span></span> |
| <span data-ttu-id="cc2ed-208">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="cc2ed-208">CreateConversation</span></span>| <span data-ttu-id="cc2ed-209">1</span><span class="sxs-lookup"><span data-stu-id="cc2ed-209">1</span></span> | <span data-ttu-id="cc2ed-210">14 </span><span class="sxs-lookup"><span data-stu-id="cc2ed-210">14</span></span> |
| <span data-ttu-id="cc2ed-211">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="cc2ed-211">CreateConversation</span></span>| <span data-ttu-id="cc2ed-212">2</span><span class="sxs-lookup"><span data-stu-id="cc2ed-212">2</span></span> | <span data-ttu-id="cc2ed-213">16 </span><span class="sxs-lookup"><span data-stu-id="cc2ed-213">16</span></span> |
| <span data-ttu-id="cc2ed-214">会話メンバーの取得</span><span class="sxs-lookup"><span data-stu-id="cc2ed-214">Get Conversation Members</span></span>| <span data-ttu-id="cc2ed-215">1</span><span class="sxs-lookup"><span data-stu-id="cc2ed-215">1</span></span> | <span data-ttu-id="cc2ed-216">28</span><span class="sxs-lookup"><span data-stu-id="cc2ed-216">28</span></span> |
| <span data-ttu-id="cc2ed-217">会話メンバーの取得</span><span class="sxs-lookup"><span data-stu-id="cc2ed-217">Get Conversation Members</span></span>| <span data-ttu-id="cc2ed-218">2</span><span class="sxs-lookup"><span data-stu-id="cc2ed-218">2</span></span> | <span data-ttu-id="cc2ed-219">32</span><span class="sxs-lookup"><span data-stu-id="cc2ed-219">32</span></span> |
| <span data-ttu-id="cc2ed-220">会話の取得</span><span class="sxs-lookup"><span data-stu-id="cc2ed-220">Get Conversations</span></span> | <span data-ttu-id="cc2ed-221">1</span><span class="sxs-lookup"><span data-stu-id="cc2ed-221">1</span></span> | <span data-ttu-id="cc2ed-222">28</span><span class="sxs-lookup"><span data-stu-id="cc2ed-222">28</span></span> |
| <span data-ttu-id="cc2ed-223">会話の取得</span><span class="sxs-lookup"><span data-stu-id="cc2ed-223">Get Conversations</span></span> | <span data-ttu-id="cc2ed-224">2</span><span class="sxs-lookup"><span data-stu-id="cc2ed-224">2</span></span> | <span data-ttu-id="cc2ed-225">32</span><span class="sxs-lookup"><span data-stu-id="cc2ed-225">32</span></span> |
