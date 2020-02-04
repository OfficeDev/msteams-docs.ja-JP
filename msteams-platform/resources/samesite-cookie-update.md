---
title: Microsoft Teams および SameSite cookie 属性 (2020 更新プログラム)
author: laujan
description: ''
keywords: cookie 属性 samesite
ms.topic: reference
ms.author: lomeybur
ms.openlocfilehash: 167266ba0b5af1c8233cffe1fef496dd94c27ae4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674649"
---
# <a name="microsoft-teams-and-the-samesite-cookie-attribute-2020-update"></a>Microsoft Teams および SameSite cookie 属性 (2020 更新プログラム)

## <a name="cookies-in-brief"></a>Cookie の概要

 Cookie はテキスト文字列で、web サイトから送信され、web ブラウザーによってコンピューターに保存されます。 通常、認証と個人用設定のために使用されます。たとえば、ステートフル情報を呼び戻す、ユーザー設定を保持する、レコーディング参照アクティビティを記録し、関連する広告を表示します。 Cookie は常に特定のドメインにリンクされており、さまざまな関係者がインストールできます。 これらは次のように分類されます。

 |クッキー|範囲|
 | ------ | ------ |
 |**ファーストパーティの cookie**|ファーストパーティの cookie は、ユーザーが訪問して、ショッピングカートアイテム、ログイン資格情報 (認証 cookie など)、その他の分析などのデータを保存するために使用される web サイトによって作成されます。|
 |**セカンドパーティの cookie**|2番目の cookie は、技術的には、最初のパーティの cookie と同じです。 その違いは、データがデータパートナーシップ契約 (たとえば、 [Microsoft Teams の分析とレポート](/microsoftteams/teams-analytics-and-reports/teams-reporting-reference)) を介して、2番目のパーティと共有されることです。 |
 |**サードパーティの cookie**|サードパーティの cookie は、ユーザーが明示的にアクセスしたドメイン以外のドメインによってインストールされ、主に追跡 (たとえば、"Like" ボタン)、広告サービス、ライブチャットなどに使用されます。|

### <a name="cookies-and-http-requests"></a>Cookie と HTTP 要求

SameSite の制限を導入する前に、cookie がブラウザーに格納されている場合、cookie は*すべて*の http web 要求に添付され、COOKIE の http 応答ヘッダーによってサーバーに送信されていました。 予測可能なパフォーマンスによって、クロスサイト要求偽造 (CSRF) 攻撃などのセキュリティ脆弱性が生じる可能性がありました。 「 [HTTP Cookie](https://developer.mozilla.org/docs/Web/HTTP/Cookies) *」を参照してください*。 SameSite コンポーネントは、SetCookie ヘッダーの実装と管理を通じてその露出を軽減します。

### <a name="samesite-attribute-initial-release"></a>SameSite 属性: 最初のリリース

Google Chrome バージョン51では、SetCookie SameSite specification が*オプション*の属性として導入されました。 ビルド17672以降、Windows 10 では、 [Microsoft Edge ブラウザー](https://blogs.windows.com/msedgedev/2018/05/17/samesite-cookies-microsoft-edge-internet-explorer/)の SameSite cookie のサポートが導入されました。

開発者は、SameSite cookie 属性を SetCookie ヘッダーに追加しないようにするか、または次の2つの設定のいずれ*かを使用*して追加することが*できます。* 未実装の SameSite 属性は既定の状態と見なされました。

## <a name="samesite-cookie-attribute-2020-release"></a>SameSite cookie 属性: 2020 リリース

Chrome 80 (2 月2020にリリースが予定されています)。新しい cookie の値を紹介し、既定で cookie のポリシーを設定します。 更新された SameSite 属性には、次の3つの値を渡すことができます: *Strict*、*甘い*、または*None*。 SameSite 属性が指定されていない cookie `SameSite=Lax`は、既定ではになります。

|Setting | 適用 | 値 |属性の指定 |
| -------- | ----------- | --------|--------|
| **甘い**  | Cookie は、*最初のパーティ*のコンテキストと HTTP GET 要求でのみ自動的に送信されます。 SameSite cookie は、画像または iframes を読み込む呼び出しなど、クロスサイトサブ要求で送信されますが、ユーザーがリンクをたどって外部サイトから URL に移動するときに送信されます。| **Default** |`Set-Cookie: key=value; SameSite=Lax`|
| **Strict** |ブラウザーは、最初のパーティのコンテキスト要求 (cookie を設定しているサイトからの要求) に対してのみ cookie を送信します。 要求が現在の場所とは異なる URL から発信された場合、その`Strict`属性でタグ付けされた cookie は送信されません。| オプション |`Set-Cookie: key=value; SameSite=Strict`|
| **なし** | Cookie は、最初のパーティのコンテキストと cross-origin 要求の両方で送信されます。ただし、値を明示的に**`None`** 設定する必要があります。また、すべてのブラウザー要求は**`Secure`** **HTTPS プロトコルに従う必要があり**、暗号化された接続を必要とする属性を含んでいる必要があります。 その要件に従わない cookie は**拒否**されます。 <br/>**両方の属性が一緒に必要**です。 **`None`** HTTPS プロトコルを使用し**`Secure`** ないで、またはを指定しない場合は、サードパーティの cookie は拒否されます。| 省略可能。ただし、設定されている場合は、HTTPS プロトコルが必要です。 |`Set-Cookie: key=value; SameSite=None; Secure` |

## <a name="handling-incompatible-clients"></a>互換性のないクライアントの処理

> [!IMPORTANT]
> 現在、 `SameSite=None`は[**Teams デスクトップクライアント**](/aspnet/core/security/samesite?view=aspnetcore-3.1#test-with-electron)または以前のバージョンの Chrome または Safari ではサポートされていません。 「[既知の互換性]( https://www.chromium.org/updates/same-site/incompatible-clients)のないクライアント」を*参照してください*。
>ただし、次の2つの**回避策**があります。
>
>1. 適切な SameSite プロパティを指定するには、ユーザーエージェントを確認してください。 ユーザーエージェントチェックは、 [**C#**](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)と[**node.js**](https://web.dev/samesite-cookie-recipes/)で実装できます。
>2. 新しいモデルと古いモデルの両方を使用して、cookie 属性を設定します。 *「* [互換性](https://web.dev/samesite-cookie-recipes/#handling-incompatible-clients)のないクライアントの処理」を参照<br><br>
>**アプリが Teams デスクトップクライアントで実行されていて、SameSite 属性をに設定`SameSite=None`している場合、アプリは期待どおりに機能しません。**

どちらの方法を使用しても、Teams デスクトップクライアントが`SameSite=None`互換性のあるバージョンの Chromium にアップグレードされるときに、アプリケーションが正常に動作するようにします。

## <a name="teams-implications-and-adjustments"></a>Teams の影響と調整

>[!WARNING]
>**Teams デスクトップクライアントで実行されているアプリケーションは`SameSite=None`属性と互換性がないため、正常に動作しません。** 上記の**解決**策を参照してください。

1. Cookie に関連する SameSite 設定を有効にし、アプリと拡張機能が Teams で引き続き動作することを確認します。
1. アプリまたは拡張機能が失敗した場合は、Chrome 80 リリースより前に、必要な修正を行います。
1. この問題<https://teams.microsoft.com/l/team/19%3A08b594cd465e4c0491fb751e823802e2%40thread.skype/conversations?groupId=4d6d04cd-dbf0-43c8-a2ff-f80dd38be034&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47>に関する詳細または支援が必要な場合は、Microsoft の内部パートナーは次のチームに参加できます。

> [!NOTE]
> ベストプラクティスとして、SameSite 属性を常に設定して、cookie の使用目的を反映することをお勧めします。既定のブラウザーの動作に依存しないようにしてください。 *「* [開発者: 新しい SameSite の準備」を参照してください。セキュリティで保護された Cookie の設定](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)。

### <a name="tabs-task-modules-and-message-extensions"></a>タブ、タスクモジュール、およびメッセージ拡張機能

* Teams タブは`<iframes>` 、トップレベルまたはファーストパーティのコンテキストで表示されるコンテンツを埋め込むために使用します。
* タスクモジュールを使用すると、Teams アプリケーションでモーダルポップアップエクスペリエンスを作成できます。 タブと同じように、現在のページ内でモーダルウィンドウが開きます。
* メッセージ拡張機能により、外部リソースからチャットメッセージに拡充されたコンテンツを挿入することができます。

埋め込みコンテンツによって使用されるすべての cookie は、サイトがに表示さ`<iframe>`れるときに、サードパーティと見なされます。 さらに、ページ上のリモートリソースが要求 (たとえば、 `<img>` `<script>`タグ、外部フォント、個人用コンテンツ) と共に送信される cookie を使用している場合は、それらのリソースがクロスサイト使用`SameSite=None; Secure`のためにマークされていることを確認する必要があります。または、フォールバックが行われていることを確認する必要があります。

### <a name="authentication"></a>認証

* タブ内の埋め込みコンテンツページの認証を必要とする場合は、web ベースの認証フローを使用する必要があります。
* Web ベースの認証フローは、構成ページ、タスクモジュール、またはメッセージング拡張機能にも使用できます。
* 会話 bot に対して web ベースの認証フローを使用して、タスクモジュールを使用する必要があります。

更新された SameSite 制限に従って、リンクが外部サイトから派生している場合、ブラウザーは既に認証された web サイトに cookie を追加しません。 認証 cookie がクロスサイト使用`SameSite=None; Secure`のためにマークされていることを確認する必要があります。または、フォールバックが行われていることを確認する必要があります。

### <a name="android-system-webview"></a>Android システムの WebView

Android WebView は、Android アプリで web コンテンツを表示できるようにするクロムシステムコンポーネントです。 新しい制限は、Chrome 80 以降の既定値になりますが、WebViews ですぐに適用されることはありません。 これらは将来適用されます。 準備するために、Android はネイティブアプリで[COOKEMANAGER API](https://developer.android.com/reference/android/webkit/CookieManager)を使用して直接 cookie を設定できます。

* 最初のパーティのコンテキストでのみ必要な cookie の場合は、必要に応じて`SameSite=Lax` 、 `SameSite=Strict`またはとして宣言する必要があります。
* サードパーティのコンテキストで必要な cookie の場合は、がとして`SameSite=None; Secure`宣言されていることを確認する必要があります。

## <a name="learn-more"></a>詳細情報

[SameSite の例](https://github.com/GoogleChromeLabs/samesite-examples)

[SameSite cookie レシピ](https://web.dev/samesite-cookie-recipes/)

[既知の互換性のないクライアント]( https://www.chromium.org/updates/same-site/incompatible-clients)

[開発者: 新しい SameSite の準備をします。セキュリティで保護された Cookie の設定](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)

**OpenId Connect への影響**<br>
[ASP.NET および ASP.NET Core での今後の SameSite Cookie の変更](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
