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
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a>ボットを最適化する: Microsoft Teams でのレート制限とベスト プラクティス

一般的な原則として、アプリケーションは投稿するメッセージの数を個々のチャットまたはチャネルの会話に制限する必要があります。 これにより、エンド ユーザーに "スパム" を感じない最適なエクスペリエンスが保証されます。

Microsoft Teams とそのユーザーを保護するために、ボット API は受信要求をレート制限します。 この制限を超えるアプリは、エラー状態 `HTTP 429 Too Many Requests` を受け取る。 すべての要求は、メッセージの送信、チャネル列挙、名簿フェッチなど、同じレート制限ポリシーの対象です。

レート制限の正確な値は変更される可能性があります。API が返される場合は、アプリケーションで適切なバックオフ動作を実装することをお勧めします `HTTP 429 Too Many Requests` 。

## <a name="handling-rate-limits"></a>レート制限の処理

ボット ビルダー SDK 操作を発行する場合は、状態コードを処理 `Microsoft.Rest.HttpOperationException` して確認できます。

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

## <a name="best-practices"></a>ベスト プラクティス

一般に、応答を受信しないように、簡単な予防措置を講 `HTTP 429` じるべきです。 たとえば、同じ個人またはチャネルの会話に対して複数の要求を発行しないようにします。 代わりに、API 要求のバッチ処理を検討してください。

ランダムなジッターで指数バックオフを使用する方法は、429 を処理するための推奨される方法です。 これにより、複数の要求が再試行時に競合を発生しない。

## <a name="example-detecting-transient-exceptions"></a>例: 一時的な例外の検出

一時的な障害処理アプリケーション ブロックを介して指数バックオフを使用するサンプルを次に示します。

一時的な障害処理を使用して、バックオフと [再試行を実行できます](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)。 NuGet パッケージの取得とインストールに関するガイドラインについては、「一時的な障害処理アプリケーション ブロックをソリューションに追加する」 [を参照してください](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)。 *「一時的な*[障害の処理」も参照してください](/azure/architecture/best-practices/transient-faults)。

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

## <a name="example-backoff"></a>例: バックオフ

レート制限の検出に加えて、指数バックオフも実行できます。

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

また、前述の再試行 `System.Action` ポリシーを使用してメソッドの実行を実行できます。 参照されるライブラリでは、固定間隔または線形バックオフ メカニズムを指定することもできます。

実行時に値を微調整および調整するには、値と戦略を構成ファイルに格納することをお勧めします。

詳細については、さまざまな再試行パターンに関するこの便利なガイド:再試行 [パターンを参照してください](/azure/architecture/patterns/retry)。

## <a name="per-bot-per-thread-limit"></a>スレッドごとのボットごとの制限

>[!NOTE]
>サービス レベルでのメッセージの分割は、予想される要求 /秒 (RPS) を超える結果になります。 制限に近づくのが懸念される場合は、前述のバックオフ戦略を実装する必要があります。 以下に示す値は、見積もり専用です。

この制限は、ボットが 1 回の会話で生成できるトラフィックを制御します。 ここでの会話は、ボットとユーザー、グループ チャット、またはチーム内のチャネルの間で 1:1 です。

| **シナリオ** | **期間 (秒)** | **許可される操作の上限** |
| --- | --- | --- |
| 会話に送信する | 1 | 7 |
| 会話に送信する | 2 | 8 |
| 会話に送信する | 30 | 60 |
| 会話に送信する | 3600 | 1800 |
| 会話の作成 | 1 | 7 |
| 会話の作成 | 2 | 8 |
| 会話の作成 | 30 | 60 |
| 会話の作成 | 3600 | 1800 |
| 会話メンバーの取得| 1 | 14  |
| 会話メンバーの取得| 2 | 16  |
| 会話メンバーの取得| 30 | 120 |
| 会話メンバーの取得| 3600 | 3600 |
| 会話の取得 | 1 | 14  |
| 会話の取得 | 2 | 16  |
| 会話の取得 | 30 | 120 |
| 会話の取得 | 3600 | 3600 |

>[!NOTE]
> 以前のバージョンと `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` API は非推奨です。 1 分あたり 5 つの要求に調整され、チームごとに最大 10K のメンバーが返されます。 ボット フレームワーク SDK と、ページ分割された最新の API エンドポイントを使用するコードを更新するには、「チームおよびチャット メンバーのボット API の変更」 [を参照してください](../../resources/team-chat-member-api-changes.md)。

## <a name="per-thread-limit-for-all-bots"></a>すべてのボットのスレッドごとの制限

この制限は、すべてのボットが 1 回の会話で生成できるトラフィックを制御します。 ここでの会話は、ボットとユーザー、グループ チャット、またはチーム内のチャネルの間で 1:1 です。

| **シナリオ** | **期間 (秒)** | **許可される操作の上限** |
| --- | --- | --- |
| 会話に送信する | 1 | 14  |
| 会話に送信する | 2 | 16  |
| 会話の作成 | 1 | 14  |
| 会話の作成 | 2 | 16  |
| CreateConversation| 1 | 14  |
| CreateConversation| 2 | 16  |
| 会話メンバーの取得| 1 | 28 |
| 会話メンバーの取得| 2 | 32 |
| 会話の取得 | 1 | 28 |
| 会話の取得 | 2 | 32 |
