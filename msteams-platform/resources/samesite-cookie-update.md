---
title: Microsoft Teams SameSite cookie 属性 (2020 更新プログラム)
author: laujan
description: SameSite Cookie の属性について説明します。
keywords: cookie 属性 samesite
ms.topic: reference
localization_priority: Normal
ms.author: lomeybur
ms.openlocfilehash: c286e01b6e2477c1ab2b787852cde0fb789a80da
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52629852"
---
# <a name="microsoft-teams-and-the-samesite-cookie-attribute-2020-update"></a>Microsoft Teams SameSite cookie 属性 (2020 更新プログラム)

## <a name="cookies-in-brief"></a>簡潔な Cookie

 Cookie は、Web サイトから送信され、Web ブラウザーによってコンピューターに保存されるテキスト文字列です。 通常、認証と個人用設定に使用されます。たとえば、ステートフルな情報の呼び出し、ユーザー設定の保持、閲覧アクティビティの記録、関連する広告の表示などです。 Cookie は常に特定のドメインにリンクされ、さまざまな関係者がインストールできます。 これらは、次のように分類されます。

 |クッキー|範囲|
 | ------ | ------ |
 |**ファースト パーティ Cookie**|ファースト パーティ Cookie は、ユーザーがアクセスした Web サイトによって作成され、ショッピング カートアイテム、ログイン資格情報などのデータを保存するために使用されます。 たとえば、認証 Cookie、その他の分析。|
 |**第二者の Cookie**|第二者の Cookie は、技術的にはファースト パーティ Cookie と同じです。 違いは、データがデータパートナーシップ契約を介して第二者と共有される点です。 たとえば、分析[Microsoft Teamsレポートを作成します](/microsoftteams/teams-analytics-and-reports/teams-reporting-reference)。 |
 |**サードパーティの Cookie**|サードパーティの Cookie は、ユーザーが明示的にアクセスしたドメイン以外のドメインによってインストールされ、主に追跡に使用されます。 たとえば、"Like" ボタン、広告配信、ライブ チャットなどです。|

### <a name="cookies-and-http-requests"></a>Cookie と HTTP 要求

SameSite の制限が導入される前に、Cookie がブラウザーに保存されている場合、Cookie はすべての *HTTP* Web 要求に接続され、Set-Cookie HTTP 応答ヘッダーによってサーバーに送信されました。 予想通り、そのパフォーマンスはクロスサイト要求フォージェリ (CSRF) 攻撃などのセキュリティの脆弱性を導入する可能性がありました。 *HTTP Cookie* [を参照してください](https://developer.mozilla.org/docs/Web/HTTP/Cookies)。 SameSite コンポーネントは、SetCookie ヘッダーの実装と管理を通じて、その露出を軽減しました。

### <a name="samesite-attribute-initial-release"></a>SameSite 属性: 初期リリース

Google Chrome バージョン 51 では、オプションの属性として SetCookie SameSite 仕様が *導入* されました。 ビルド 17672 から、Windows 10ブラウザーに SameSite cookie のサポートMicrosoft Edge[しました](https://blogs.windows.com/msedgedev/2018/05/17/samesite-cookies-microsoft-edge-internet-explorer/)。

開発者は、SameSite cookie 属性を SetCookie ヘッダーに追加することをオプトアウトするか *、Lax* と Strict の 2 つの設定のいずれかを使用して追加 *できます*。 Anmplemented SameSite 属性は既定の状態と見なされました。

## <a name="samesite-cookie-attribute-2020-release"></a>SameSite cookie 属性: 2020 リリース

2020 年 2 月にリリースされる予定の Chrome 80 では、新しい Cookie 値が導入され、既定で Cookie ポリシーが適用されます。 更新された SameSite 属性には、Strict、Lax、または None の *3 つの* 値を渡 *します*。  SameSite 属性を指定しない Cookie は、既定で `SameSite=Lax` .

|設定 | 強制 | 値 |属性の指定 |
| -------- | ----------- | --------|--------|
| **Lax**  | Cookie は、ファースト パーティのコンテキストと HTTP GET 要求でのみ自動的に送信されます。 SameSite Cookie は、イメージや iframe の読み込み呼び出しなどのクロスサイト サブ要求では差し控えされますが、ユーザーがリンクに従って外部サイトから URL に移動すると送信されます。| **Default** |`Set-Cookie: key=value; SameSite=Lax`|
| **Strict** |ブラウザーは、ファースト パーティのコンテキスト要求 (Cookie を設定したサイトから発信された要求) の Cookie のみを送信します。 要求が現在の場所とは異なる URL から発信された場合、属性にタグ付けされた Cookie は `Strict` いずれも送信されません。| 省略可能 |`Set-Cookie: key=value; SameSite=Strict`|
| **なし** | Cookie は、ファースト パーティのコンテキストとクロスオリジン要求の両方で送信されます。ただし、値は明示的に設定する必要があります。すべてのブラウザー要求は HTTPS プロトコルに従い、暗号化された接続を必要とする属性 **`None`**  **`Secure`** を含める必要があります。 その要件に準拠しない Cookie は拒否 **されます**。 <br/>**両方の属性が一緒に必要です**。 HTTPS プロトコルを使用せずに指定した場合、または HTTPS プロトコルを使用しない場合、サード パーティ **`None`** **`Secure`**  Cookie は拒否されます。| オプションですが、設定されている場合は HTTPS プロトコルが必要です。 |`Set-Cookie: key=value; SameSite=None; Secure` |

## <a name="teams-implications-and-adjustments"></a>Teamsの影響と調整

1. Cookie に関連する SameSite 設定を有効にし、アプリと拡張機能が引き続き機能Teams。
1. アプリや拡張機能が失敗した場合は、Chrome 80 リリースの前に必要な修正を行います。
1. Microsoft の内部パートナーは、この問題に関する詳細やヘルプが必要な場合は、次のチームに参加できます <https://teams.microsoft.com/l/team/19%3A08b594cd465e4c0491fb751e823802e2%40thread.skype/conversations?groupId=4d6d04cd-dbf0-43c8-a2ff-f80dd38be034&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47> 。

> [!NOTE]
> ベスト プラクティスとして、Cookie の目的に合った使用を反映するように SameSite 属性を常に設定することを推奨します。 既定のブラウザーの動作に依存しません。 詳細については[、「Developers: Get Ready for New SameSite=None」を参照してください。セキュリティで保護された Cookie 設定](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)。

### <a name="tabs-task-modules-and-message-extensions"></a>タブ、タスク モジュール、およびメッセージ拡張機能

* Teamsは、トップ レベルまたはファースト パーティのコンテキストで表示されるコンテンツを埋め `<iframes>` 込む場合に使用します。
* タスク モジュールを使用すると、Teams アプリケーションでモーダル ポップアップ エクスペリエンスを作成することができます。 タブと同様に、現在のページ内にモーダル ウィンドウが開きます。
* メッセージ拡張機能を使用すると、外部リソースからリッチコンテンツをチャット メッセージに挿入できます。

埋め込みコンテンツで使用される Cookie は、サイトが . `<iframe>` さらに、ページ上のリモート リソースが、要求とタグ、外部フォント、および個人設定されたコンテンツで送信される Cookie に依存している場合は、それらのリソースがクロスサイトの使用状況 (フォールバックなど) のマークが付いているか、フォールバックが適切に設定されている必要があります。 `<img>` `<script>` `SameSite=None; Secure`

### <a name="authentication"></a>認証

* タブに埋め込まれたコンテンツ ページの認証が必要な場合は、Web ベースの認証フローを使用する必要があります。
* Web ベースの認証フローは、構成ページ、タスク モジュール、またはメッセージング拡張機能にも使用できます。
* タスク モジュールを使用する必要がある会話型ボットには、Web ベースの認証フローを使用できます。

更新された SameSite の制限に従って、リンクが外部サイトから派生した場合、ブラウザーは既に認証された Web サイトに Cookie を追加しない。 認証 Cookie がクロスサイトの使用に対してマークされているのを確認するか、フォールバックが適切に行なう `SameSite=None; Secure` 必要があります。

### <a name="android-system-webview"></a>Android System WebView

Android WebView は、Android アプリが Web コンテンツを表示できる Chrome システム コンポーネントです。 新しい制限は Chrome 80 から始まる既定の制限になりますが、WebViews では直ちに適用されません。 これらは将来適用されます。 Android では、準備のために、ネイティブ アプリが CookeManager API を介して [直接 Cookie を設定できます](https://developer.android.com/reference/android/webkit/CookieManager)。

* ファースト パーティのコンテキストでのみ必要な Cookie の場合は、必要に応じて宣言するか `SameSite=Lax` `SameSite=Strict` 、または宣言する必要があります。
* サードパーティのコンテキストで必要な Cookie の場合は、その Cookie がとして宣言されている必要があります `SameSite=None; Secure` 。

## <a name="see-also"></a>関連項目

* [SameSite の例](https://github.com/GoogleChromeLabs/samesite-examples)
* [SameSite Cookie のレシピ](https://web.dev/samesite-cookie-recipes/)
* [既知の互換性のないクライアント]( https://www.chromium.org/updates/same-site/incompatible-clients)
* [開発者: Get Ready for New SameSite=None;セキュリティで保護された Cookie 設定](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)

**OpenId Connect影響**<br>
[今後の SameSite Cookie の変更点 (ASP.NET と ASP.NET Core](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
