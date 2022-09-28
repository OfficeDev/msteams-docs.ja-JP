---
title: ボットのレート制限
description: レート制限を使用してボットを最適化する方法について説明します。 ボット スレッドの制限に従って、一時的な例外を検出します。 指数バックオフを実行することもできます。
ms.localizationpriority: medium
ms.openlocfilehash: 487f251be40894464e55b891a7386cd8a04abe25
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100428"
---
# <a name="optimize-your-bot-with-rate-limiting-in-teams"></a>Teams でレートを制限してボットを最適化する

レート制限は、メッセージを特定の最大頻度に制限する方法です。 一般的な原則として、アプリケーションは、個々のチャットまたはチャネル会話に投稿するメッセージの数を制限する必要があります。 これにより、最適なエクスペリエンスが確保され、メッセージがユーザーにスパムとして表示されることはありません。

Microsoft Teams とそのユーザーを保護するために、ボット API は受信要求のレート制限を提供します。 この制限を超えるアプリは、エラー状態を `HTTP 429 Too Many Requests` 受け取ります。 すべての要求は、メッセージ、チャネル列挙、および名簿フェッチの送信など、同じレート制限ポリシーの対象となります。

レート制限の正確な値は変更される可能性があるため、API が返されるときに、アプリケーションは適切なバックオフ動作を実装する `HTTP 429 Too Many Requests`必要があります。

## <a name="handle-rate-limits"></a>レート制限を処理する

Bot Builder SDK 操作を発行するときに、状態コードを処理 `Microsoft.Rest.HttpOperationException` して確認できます。

次のコードは、レート制限の処理の例を示しています。

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

ボットのレート制限を処理した後は、指数バックオフを使用して応答を処理 `HTTP 429` できます。

## <a name="handle-http-429-responses"></a>応答を処理する`HTTP 429`

一般に、応答を受け取らないように、簡単な予防措置を `HTTP 429` 講じる必要があります。 たとえば、同じ個人またはチャネルの会話に対して複数の要求を発行することは避けてください。 代わりに、API 要求のバッチを作成します。

ランダム なジッターで指数バックオフを使用することは、429s を処理する推奨される方法です。 これにより、複数の要求で再試行時に競合が発生することはありません。

応答を処理 `HTTP 429` した後、一時的な例外を検出する例を確認できます。

> [!NOTE]
> エラー コード **429** の再試行に加えて、エラー コード **412**、 **502**、 **および 504** も再試行する必要があります。

## <a name="detect-transient-exceptions-example"></a>一時的な例外を検出する例

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

[一時的な障害処理](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)を使用してバックオフと再試行を実行できます。 NuGet パッケージの取得とインストールに関するガイドラインについては、 [ソリューションへの一時的な障害処理アプリケーション ブロックの追加に関するページを参照してください](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)。 [一時的な障害処理](/azure/architecture/best-practices/transient-faults)も参照してください。

一時的な例外を検出するための例を確認したら、指数バックオフの例を確認します。 失敗時に再試行する代わりに、指数バックオフを使用できます。

## <a name="backoff-example"></a>バックオフの例

レート制限を検出するだけでなく、指数バックオフを実行することもできます。

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

このセクションで説明する `System.Action` 再試行ポリシーを使用して、メソッドの実行を実行することもできます。 また、参照先ライブラリでは、固定間隔または線形バックオフ メカニズムを指定することもできます。

値と戦略を構成ファイルに格納して、実行時に値を微調整および調整します。

詳細については、「 [再試行パターン」を](/azure/architecture/patterns/retry)参照してください。

スレッドあたりのボットごとの制限を使用して、レート制限を処理することもできます。

## <a name="per-bot-per-thread-limit"></a>スレッドあたりのボットあたりの制限

スレッドあたりのボットごとの制限は、ボットが 1 つの会話で生成できるトラフィックを制御します。 会話は、ボットとユーザー、グループ チャット、またはチーム内のチャネル間の 1 対 1 です。 そのため、アプリケーションが各ユーザーに 1 つのボット メッセージを送信する場合、スレッドの制限は調整されません。

>[!NOTE]
>
> * スレッドの制限である 3600 秒と 1800 操作は、1 人のユーザーに複数のボット メッセージが送信された場合にのみ適用されます。
> * テナントあたりのアプリあたりのグローバル制限は、1 秒あたり 50 要求 (RPS) です。 そのため、1 秒あたりのボット メッセージの合計数がスレッドの制限を超えてはなりません。
> * サービス レベルでメッセージが分割されると、予想以上の RPS が生成されます。 制限に近づくことを心配している場合は、 [バックオフ戦略](#backoff-example)を実装する必要があります。 このセクションで指定する値は、見積もり専用です。

次の表に、スレッドごとのボットごとの制限を示します。

| シナリオ | 期間 (秒単位) | 許可される操作の最大数 |
| --- | --- | --- |
| 会話に送信する | 1 | 7  |
| 会話に送信する | 2 | 8  |
| 会話に送信する | 30 | 60 |
| 会話に送信する | 3600 | 1800 |
| 会話を作成する | 1 | 7  |
| 会話を作成する | 2 | 8  |
| 会話を作成する | 30 | 60 |
| 会話を作成する | 3600 | 1800 |
| 会話メンバーを取得する| 1 | 14 |
| 会話メンバーを取得する| 2 | 16 |
| 会話メンバーを取得する| 30 | 120 |
| 会話メンバーを取得する| 3600 | 3600 |
| 会話を取得する | 1 | 14 |
| 会話を取得する | 2 | 16 |
| 会話を取得する | 30 | 120 |
| 会話を取得する | 3600 | 3600 |

>[!NOTE]
> 以前のバージョンの `TeamsInfo.getMembers` API と `TeamsInfo.GetMembersAsync` API は非推奨になっています。 1 分間に 5 つの要求に調整され、チームあたり最大 10,000 人のメンバーが返されます。 Bot Framework SDK と最新のページ分割された API エンドポイントを使用するコードを更新するには、 [チームメンバーとチャット メンバーの Bot API の変更に関する](../../resources/team-chat-member-api-changes.md)ページを参照してください。

また、すべてのボットのスレッドごとの制限を使用してレート制限を処理することもできます。

## <a name="per-thread-limit-for-all-bots"></a>すべてのボットのスレッドごとの制限

すべてのボットのスレッドごとの制限は、すべてのボットが 1 つの会話で生成できるトラフィックを制御します。 ここでは、ボットとユーザー、グループ チャット、またはチーム内のチャネル間の 1 対 1 の会話です。

次の表は、すべてのボットに対するスレッドごとの制限を示しています。

| シナリオ | 期間 (秒単位) | 許可される操作の最大数 |
| --- | --- | --- |
| 会話に送信する | 1 | 14 |
| 会話に送信する | 2 | 16 |
| 会話を作成する | 1 | 14 |
| 会話を作成する | 2 | 16 |
| 会話を作成する| 1 | 14 |
| 会話を作成する| 2 | 16 |
| 会話メンバーを取得する| 1 | 28 |
| 会話メンバーを取得する| 2 | 32 |
| 会話を取得する | 1 | 28 |
| 会話を取得する | 2 | 32 |

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [通話と会議のボット](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

## <a name="see-also"></a>関連項目

[実行時間の長い操作を管理する](/azure/bot-service/bot-builder-howto-long-operations-guidance?view=azure-bot-service-4.0&preserve-view=true)
