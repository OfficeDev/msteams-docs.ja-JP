---
title: Microsoft Teamsと SameSite クッキー属性 (2020 年更新)
author: laujan
description: SameSite クッキーの属性を記述します
keywords: クッキー属性同じサイト
ms.topic: reference
localization_priority: Normal
ms.author: lomeybur
ms.openlocfilehash: cf28a28050d50b2b6b2601a3231cdad30211ab2c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566713"
---
# <a name="microsoft-teams-and-the-samesite-cookie-attribute-2020-update"></a>Microsoft Teamsと SameSite クッキー属性 (2020 年更新)

## <a name="cookies-in-brief"></a>簡単にクッキー

 クッキーは、テキスト文字列で、ウェブサイトから送信され、Webブラウザによってコンピュータに保存されます。 通常、認証と個人用設定に使用されます(たとえば、ステートフルな情報の呼び出し、ユーザー設定の保持、閲覧アクティビティの記録、関連する広告の表示など)。 クッキーは常に特定のドメインにリンクされ、さまざまな当事者によってインストールすることができます。 これらは次のように分類されます。

 |クッキー|範囲|
 | ------ | ------ |
 |**ファーストパーティクッキー**|ファーストパーティの Cookie は、ユーザーが訪問した Web サイトによって作成され、ショッピング カートアイテム、ログイン資格情報などのデータを保存するために使用されます。 たとえば、認証クッキーやその他の分析。|
 |**セカンドパーティクッキー**|セカンド パーティの Cookie は、技術的にはファースト パーティの Cookie と同じです。 違いは、データはデータパートナーシップ契約を介して第二者と共有されるということです。 たとえば、[分析やレポート作成Microsoft Teams。](/microsoftteams/teams-analytics-and-reports/teams-reporting-reference) |
 |**サードパーティクッキー**|サードパーティの Cookie は、ユーザーが明示的に訪問したドメイン以外のドメインによってインストールされ、主に追跡に使用されます。 たとえば、「Like」ボタン、広告配信、ライブチャットなどです。|

### <a name="cookies-and-http-requests"></a>クッキーと HTTP リクエスト

SameSite の制限が導入される前に、Cookie がブラウザに保存されると、 *それらはすべての* HTTP Web 要求に添付され、http 応答ヘッダーSet-Cookieによってサーバーに送信されました。 予想通り、このパフォーマンスは、クロスサイト リクエスト フォージェリ (CSRF) 攻撃などのセキュリティの脆弱性を引き起こす可能性がありました。 [HTTP クッキー](https://developer.mozilla.org/docs/Web/HTTP/Cookies)*を参照してください*。 SameSite コンポーネントは、SetCookie ヘッダーでの実装と管理を通じて、そのエクスポージャーを軽減しました。

### <a name="samesite-attribute-initial-release"></a>SameSite 属性: 初期リリース

Google Chrome バージョン 51 は *、オプション* の属性として SetCookie SameSite 仕様を導入しました。 ビルド 17672 以降、Windows 10 [Microsoft Edge ブラウザ](https://blogs.windows.com/msedgedev/2018/05/17/samesite-cookies-microsoft-edge-internet-explorer/)の SameSite クッキー サポートが導入されました。

開発者は、SetCookie ヘッダーに SameSite クッキー属性を追加することをオプトアウトするか *、Lax* と *Strict* の 2 つの設定のいずれかを使用して追加できます。 実装されていない SameSite 属性は、既定の状態と見なされました。

## <a name="samesite-cookie-attribute-2020-release"></a>SameSite クッキー属性: 2020 リリース

2020 年 2 月にリリース予定の Chrome 80 では、新しい Cookie 値が導入され、デフォルトで Cookie ポリシーが適用されます。 更新された SameSite 属性には、 *厳密*、 *怠惰*、または *なし* の 3 つの値を渡すことができます。 SameSite 属性を指定しないクッキーは、デフォルトで `SameSite=Lax` .

|設定 | 実施 | 値 |属性の仕様 |
| -------- | ----------- | --------|--------|
| **跅**  | クッキーは、 *ファーストパーティの* コンテキストと HTTP GET リクエストでのみ自動的に送信されます。 SameSiteクッキーは、画像やiframeをロードする呼び出しなどのクロスサイトサブリクエストで差し控えられるが、ユーザーがリンクをたどるなどして外部サイトからURLに移動すると送信される。| **Default** |`Set-Cookie: key=value; SameSite=Lax`|
| **Strict** |ブラウザは、ファーストパーティのコンテキスト要求 (Cookie を設定したサイトからの要求) に対してのみ Cookie を送信します。 リクエストが現在の場所の URL とは異なる URL から発信された場合、属性でタグ付けされたクッキー `Strict` は送信されません。| 省略可能 |`Set-Cookie: key=value; SameSite=Strict`|
| **なし** | クッキーはファーストパーティコンテキストとクロスオリジンリクエストの両方で送信されます。ただし、値を明示的に設定する必要 **`None`** があり、すべてのブラウザー要求は **HTTPS プロトコルに従い** 、 **`Secure`** 暗号化された接続を必要とする属性を含める必要があります。 その要件に従わないクッキーは **拒否** されます。 <br/>**両方の属性が一緒に必要です**。 HTTPS **`None`** プロトコルを使用せずに指定した **`Secure`**  場合、または HTTPS プロトコルが使用されていない場合は、サードパーティの Cookie が拒否されます。| オプションですが、設定されている場合は HTTPS プロトコルが必要です。 |`Set-Cookie: key=value; SameSite=None; Secure` |

## <a name="teams-implications-and-adjustments"></a>Teamsの意味と調整

1. Cookie に関連する SameSite 設定を有効にし、アプリと拡張機能が引き続きTeamsで動作することを検証します。
1. アプリや拡張機能に問題がある場合は、Chrome 80 リリースより前に必要な修正を行ってください。
1. マイクロソフトの社内パートナーは、この問題に関する詳細情報や支援が必要な場合は、次のチームに参加できます <https://teams.microsoft.com/l/team/19%3A08b594cd465e4c0491fb751e823802e2%40thread.skype/conversations?groupId=4d6d04cd-dbf0-43c8-a2ff-f80dd38be034&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47> 。

> [!NOTE]
> ベストプラクティスとして、Cookie の使用目的を反映するように常に SameSite 属性を設定することをお勧めします。 既定のブラウザー動作に依存しないでください。 詳細については、「[開発者: 新しい SameSite の準備をする =なし」を参照してください。セキュアクッキー設定](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)

### <a name="tabs-task-modules-and-message-extensions"></a>タブ、タスク モジュール、およびメッセージの拡張機能

* Teamsタブ `<iframes>` は、トップレベルまたはファーストパーティのコンテキストで表示されるコンテンツを埋め込むために使用します。
* タスク モジュールを使用すると、Teams アプリケーションでモーダル ポップアップ エクスペリエンスを作成することができます。 タブと同様に、モーダル ウィンドウは現在のページ内で開きます。
* メッセージ拡張機能を使用すると、外部リソースからチャット メッセージにエンリッチコンテンツを挿入できます。

埋め込みコンテンツで使用される Cookie は、サイトが に表示されるときにサードパーティと見なされます `<iframe>` 。 さらに、ページ上のリモート リソースが、要求とタグ、外部フォント、およびパーソナライズされたコンテンツを含む Cookie の送信に依存している `<img>` `<script>` 場合は、フォールバックが適切に設定されているなどのクロスサイトでの使用にマークされていることを `SameSite=None; Secure` 確認する必要があります。

### <a name="authentication"></a>認証

* タブに埋め込まれたコンテンツ ページに認証が必要な場合は、Web ベースの認証フローを使用する必要があります。
* Web ベースの認証フローは、構成ページ、タスク モジュール、またはメッセージング拡張機能にも使用できます。
* タスク モジュールを使用する必要がある会話型ボットには、Web ベースの認証フローを使用できます。

更新された SameSite の制限に従って、ブラウザーは、リンクが外部サイトから派生した場合、既に認証済みの Web サイトに Cookie を追加しません。 認証 Cookie にクロスサイトの使用用としてマークを付ける `SameSite=None; Secure` か、フォールバックが適切であることを確認する必要があります。

### <a name="android-system-webview"></a>アンドロイドシステムウェブビュー

Android WebView は、Android アプリが Web コンテンツを表示できるようにする Chrome システム コンポーネントです。 新しい制限は Chrome 80 以降のデフォルトになりますが、Web ビューにはすぐに適用されません。 今後適用される予定です。 準備するために、Androidは、ネイティブアプリが [クックマネージャーAPI](https://developer.android.com/reference/android/webkit/CookieManager)を介して直接クッキーを設定することができます:

* ファーストパーティのコンテキストでのみ必要な Cookie の場合は、 `SameSite=Lax` 必要に応じて、 または として宣言する必要があります `SameSite=Strict` 。
* サードパーティのコンテキストで必要な Cookie の場合は、それらが `SameSite=None; Secure` .

## <a name="see-also"></a>関連項目

* [Same サイトの例](https://github.com/GoogleChromeLabs/samesite-examples)

* [サメサイトクッキーのレシピ](https://web.dev/samesite-cookie-recipes/)

* [既知の互換性のないクライアント]( https://www.chromium.org/updates/same-site/incompatible-clients)

* [開発者: 新しい SameSite の準備をする = なし;セキュアクッキー設定](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)

**オープンID Connect影響**<br>
[今後の ASP.NET と ASP.NET Coreにおける今後のサメサイトクッキーの変更](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
