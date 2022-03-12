---
title: Teams でレートを制限してボットを最適化する
description: コード例を使用して、スレッドごとのボットごとの制限とすべてのボットの制限ごとのボットのレート制限の処理について説明します。 さらに、アプリのレート制限のベスト プラクティスMicrosoft Teams。
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Teams ボットのレート制限
ms.openlocfilehash: 5f0eba162215aeda2c0f1e433b223f21628ea5e1
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453377"
---
# <a name="optimize-your-bot-with-rate-limiting-in-teams"></a>Teams でレートを制限してボットを最適化する

レート制限は、メッセージを特定の最大頻度に制限する方法です。 一般的な原則として、アプリケーションは投稿するメッセージの数を個々のチャットまたはチャネルの会話に制限する必要があります。 これにより、最適なエクスペリエンスが確保され、メッセージがユーザーにスパムとして表示されません。

Microsoft Teams とそのユーザーを保護するために、ボット API は受信要求のレート制限を提供します。 この制限を超えるアプリは、エラー状態を `HTTP 429 Too Many Requests` 受け取る。 すべての要求は、メッセージの送信、チャネル列挙、名簿フェッチなど、同じレート制限ポリシーの対象です。

レート制限の正確な値は変更される可能性があります。API が返される場合、アプリケーションは適切なバックオフ動作を実装する必要があります `HTTP 429 Too Many Requests`。

## <a name="handle-rate-limits"></a>レート制限の処理

ボット ビルダー SDK 操作を発行する場合は、状態コードを `Microsoft.Rest.HttpOperationException` 処理して確認できます。

次のコードは、レート制限の処理例を示しています。

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

ボットのレート制限を処理した後、指数 `HTTP 429` バックオフを使用して応答を処理できます。

## <a name="handle-http-429-responses"></a>応答 `HTTP 429` の処理

一般に、応答を受信しないように、簡単な予防措置を講じ `HTTP 429` なければならない。 たとえば、同じ個人またはチャネルの会話に対して複数の要求を発行しないようにします。 代わりに、API 要求のバッチを作成します。

ランダムなジッターで指数バックオフを使用する方法は、429 を処理するための推奨される方法です。 これにより、複数の要求が再試行時に競合を発生しない。

応答を処理 `HTTP 429` した後、一時的な例外を検出する例を確認できます。

> [!NOTE]
> エラー コード **429** の再試行に加えて、エラー コード **412**、**502、および 504** も再試行する必要があります。

## <a name="detect-transient-exceptions-example"></a>一時的な例外の検出の例

次のコードは、一時的な障害処理アプリケーション ブロックを使用して指数バックオフを使用する例を示しています。

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

一時的な障害処理を使用して、バックオフと再試行 [を実行できます](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)。 NuGet パッケージの取得とインストールに関するガイドラインについては、「一時的な障害処理アプリケーション ブロックをソリューションに[追加する」を参照してください](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)。 一時的な障害 [処理も参照してください](/azure/architecture/best-practices/transient-faults)。

一時的な例外を検出する例を実行した後、指数バックオフの例を参照してください。 エラー時に再試行する代わりに指数バックオフを使用できます。

## <a name="backoff-example"></a>バックオフの例

レート制限の検出に加えて、指数バックオフも実行できます。

次のコードは、指数バックオフの例を示しています。

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

また、このセクションで説明する `System.Action` 再試行ポリシーを使用してメソッドの実行を実行できます。 参照されるライブラリでは、固定間隔または線形バックオフ メカニズムを指定することもできます。

値と戦略を構成ファイルに格納して、実行時に値を微調整および調整します。

詳細については、「再試行パターン [」を参照してください](/azure/architecture/patterns/retry)。

スレッドごとのボットごとの制限を使用して、レート制限を処理できます。

## <a name="per-bot-per-thread-limit"></a>スレッドごとのボットごとの制限

スレッドごとのボットごとの制限は、ボットが 1 回の会話で生成できるトラフィックを制御します。 ボットとユーザー、グループ チャット、またはチーム内のチャネル間の会話は 1:1 です。 したがって、アプリケーションが各ユーザーにボット メッセージを 1 つ送信しても、スレッドの制限は調整されません。

>[!NOTE]
>
> * 3600 秒と 1800 の操作のスレッド制限は、複数のボット メッセージが 1 人のユーザーに送信される場合にのみ適用されます。
> * テナントごとのアプリごとのグローバル制限は、1 秒あたり 50 要求 (RPS) です。 したがって、1 秒あたりのボット メッセージの総数がスレッドの制限を超えなけってはいけない。
> * サービス レベルでのメッセージの分割は、予想される RPS よりも高くなります。 制限への近付きが懸念される場合は、バックオフ戦略を [実装する必要があります](#backoff-example)。 このセクションで提供される値は、見積もり専用です。

次の表に、スレッドごとのボットごとの制限を示します。

| シナリオ | 期間 (秒) | 許可される操作の最大数 |
| --- | --- | --- |
| 会話に送信する | 1 | 7  |
| 会話に送信する | 2 | 8  |
| 会話に送信する | 30 | 60 |
| 会話に送信する | 3600 | 1800 |
| 会話を作成する | 1 | 7  |
| 会話を作成する | 2 | 8  |
| 会話を作成する | 30 | 60 |
| 会話を作成する | 3600 | 1800 |
| 会話メンバーを取得する| 1 | 14  |
| 会話メンバーを取得する| 2 | 16 |
| 会話メンバーを取得する| 30 | 120 |
| 会話メンバーを取得する| 3600 | 3600 |
| 会話を取得する | 1 | 14  |
| 会話を取得する | 2 | 16 |
| 会話を取得する | 30 | 120 |
| 会話を取得する | 3600 | 3600 |

>[!NOTE]
> 以前のバージョンと `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` API は非推奨です。 1 分あたり 5 つの要求に調整され、チームごとに最大 10K のメンバーが返されます。 ボット フレームワーク SDK と、ページ分割された最新の API エンドポイントを使用するコードを更新するには、「チームおよびチャット メンバーのボット API の変更」 [を参照してください](../../resources/team-chat-member-api-changes.md)。

また、すべてのボットのスレッドごとの制限を使用して、レート制限を処理できます。

## <a name="per-thread-limit-for-all-bots"></a>すべてのボットのスレッドごとの制限

すべてのボットのスレッドごとの制限は、すべてのボットが 1 回の会話で生成できるトラフィックを制御します。 ここでの会話は、ボットとユーザー、グループ チャット、またはチーム内のチャネルの間で 1:1 です。

次の表に、すべてのボットのスレッドごとの制限を示します。

| シナリオ | 期間 (秒) | 許可される操作の最大数 |
| --- | --- | --- |
| 会話に送信する | 1 | 14  |
| 会話に送信する | 2 | 16 |
| 会話を作成する | 1 | 14  |
| 会話を作成する | 2 | 16 |
| 会話を作成する| 1 | 14  |
| 会話を作成する| 2 | 16 |
| 会話メンバーを取得する| 1 | 28 |
| 会話メンバーを取得する| 2 | 32 |
| 会話を取得する | 1 | 28 |
| 会話を取得する | 2 | 32 |

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [通話と会議のボット](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)
