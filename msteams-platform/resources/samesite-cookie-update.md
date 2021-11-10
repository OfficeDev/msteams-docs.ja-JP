---
title: SameSite Cookie 属性
author: laujan
description: SameSite Cookie、その属性、Teams タブ、タスク モジュール、メッセージング拡張機能での Cookie の種類、および認証についてTeams
keywords: cookie 属性 samesite
ms.topic: reference
ms.localizationpriority: medium
ms.author: lomeybur
ms.openlocfilehash: 34347e172206228bed86874b44b768f87c2a63b9
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2021
ms.locfileid: "60887944"
---
# <a name="samesite-cookie-attribute"></a>SameSite Cookie 属性

Cookie は、Web サイトから送信され、Web ブラウザーによってコンピューターに保存されるテキスト文字列です。 これらは、認証と個人用設定に使用されます。 たとえば、Cookie はステートフルな情報を呼び出し、ユーザー設定を保持し、閲覧アクティビティを記録し、関連する広告を表示するために使用されます。 Cookie は常に特定のドメインにリンクされ、さまざまな関係者によってインストールされます。

## <a name="types-of-cookies"></a>Cookie の種類

Cookie の種類と対応するスコープは次のとおりです。

|クッキー|範囲|
| ------ | ------ |
|ファースト パーティ Cookie|ファースト パーティ Cookie は、ユーザーがアクセスする Web サイトによって作成されます。 ショッピング カートアイテム、サインイン資格情報などのデータを保存するために使用されます。 たとえば、認証 Cookie、その他の分析。|
|第二者の Cookie|第二者の Cookie は、技術的にはファースト パーティ Cookie と同じです。 違いは、データがデータパートナーシップ契約を通じて第二者と共有される点です。 たとえば、分析[Microsoft Teamsレポートを作成します](/microsoftteams/teams-analytics-and-reports/teams-reporting-reference)。 |
|サード パーティの Cookie|サード パーティ Cookie は、ユーザーが明示的にアクセスしたドメイン以外のドメインによってインストールされ、主に追跡に使用されます。 たとえば、 **ボタン、広告** 配信、ライブ チャットなどです。|

## <a name="cookies-and-http-requests"></a>Cookie と HTTP 要求

SameSite の制限が導入される前に、Cookie はブラウザーに保存されています。 これらはすべての HTTP Web 要求に接続され、HTTP 応答ヘッダーによって `Set Cookie` サーバーに送信されました。 このメソッドでは、CSRF 攻撃と呼ばれるクロス サイト要求フォージェリーなどのセキュリティの脆弱性が導入されました。 SameSite コンポーネントは、SetCookie ヘッダーの実装と管理を通じて露出を低減しました。

## <a name="samesite-cookie-attribute-initial-release"></a>SameSite cookie 属性: 初期リリース

Google Chrome バージョン 51 では、オプション `SetCookie SameSite` の属性として仕様が導入されました。 ビルド 17672 から、Windows 10ブラウザーに SameSite cookie のサポートMicrosoft Edge[しました](https://blogs.windows.com/msedgedev/2018/05/17/samesite-cookies-microsoft-edge-internet-explorer/)。

SameSite cookie 属性をヘッダーに追加することをオプトアウトするか、Lax と Strict の 2 つの設定のいずれかを使用 `SetCookie` **して** 追加 **できます**。 Anmplemented SameSite 属性は既定の状態と見なされました。

## <a name="samesite-cookie-attribute-2020-release"></a>SameSite cookie 属性: 2020 リリース

2020 年 2 月にリリースされた Chrome 80 では、新しい Cookie 値が導入され、既定で Cookie ポリシーが適用されます。 更新された SameSite 属性には、Strict、Lax、または None の **3 つの** 値が渡 **されます**。  指定しない場合、Cookie SameSite 属性は既定で値 `SameSite=Lax` を取得します。
 
SameSite cookie 属性は次のとおりです。

|Setting | 強制 | 値 |属性の指定 |
| -------- | ----------- | --------|--------|
| **Lax**  | Cookie は、ファースト パーティ **のコンテキストと** HTTP GET 要求でのみ自動的に送信されます。 SameSite Cookie は、イメージや iframe の読み込み呼び出しなど、クロス サイト のサブ要求で差し控えされます。 ユーザーが外部サイトから URL に移動するときに、たとえば、リンクに従って送信されます。| **Default** |`Set-Cookie: key=value; SameSite=Lax`|
| **Strict** |ブラウザーは、ファースト パーティのコンテキスト要求の Cookie のみを送信します。 これらは、Cookie を設定するサイトから発信された要求です。 要求が現在の場所とは異なる URL から発信された場合、属性にタグ付けされた Cookie は `Strict` 送信されません。| 省略可能 |`Set-Cookie: key=value; SameSite=Strict`|
| **なし** | Cookie は、ファースト パーティコンテキストとクロスオリジン要求の両方で送信されます。ただし、値は明示的に設定する必要があります。すべてのブラウザー要求は HTTPS プロトコルに従い、暗号化された接続を必要とする属性 **`None`**  **`Secure`** を含める必要があります。 その要件に準拠しない Cookie は拒否 **されます**。 <br/>**両方の属性が一緒に必要です**。 HTTPS プロトコルを使用せずに指定した場合、または HTTPS プロトコルを使用しない場合、サード パーティの  **`None`** **`Secure`**  Cookie は拒否されます。| オプションですが、設定されている場合は HTTPS プロトコルが必要です。 |`Set-Cookie: key=value; SameSite=None; Secure` |

## <a name="teams-implications-and-adjustments"></a>Teamsの影響と調整

1. Cookie に関連する SameSite 設定を有効にし、アプリと拡張機能が引き続き機能Teams。
1. アプリや拡張機能が失敗した場合は、Chrome 80 リリースの前に必要な修正を行います。
1. Microsoft の内部パートナーは、次のチームに参加して、この問題の詳細やヘルプを提供できます <https://teams.microsoft.com/l/team/19%3A08b594cd465e4c0491fb751e823802e2%40thread.skype/conversations?groupId=4d6d04cd-dbf0-43c8-a2ff-f80dd38be034&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47> 。

> [!NOTE]
> Cookie の使用目的を反映するように SameSite 属性を設定する必要があります。 既定のブラウザーの動作に依存しません。 詳細については[、「Developers: Get Ready for New SameSite=None」を参照してください。セキュリティで保護された Cookie 設定](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)。

### <a name="tabs-task-modules-and-messaging-extensions"></a>タブ、タスク モジュール、メッセージング拡張機能

* Teamsは、トップ レベルまたはファースト パーティのコンテキストで表示されるコンテンツを埋め込 `<iframes>` む場合に使用します。
* タスク モジュールを使用すると、Teams アプリケーションでモーダル ポップアップ エクスペリエンスを作成することができます。 タブと同様に、現在のページ内にモーダル ウィンドウが開きます。
* メッセージング拡張機能を使用すると、外部リソースからリッチコンテンツをチャット メッセージに挿入できます。

埋め込みコンテンツで使用される Cookie は、サイトが . `<iframe>` さらに、ページ上のリモート リソースが、要求とタグ、外部フォント、および個人設定されたコンテンツで送信される Cookie に依存している場合は、それらのリソースがクロス サイトの使用状況 (フォールバックなど) のマークが付いているか、フォールバックが確実に実行されている必要があります。 `<img>` `<script>` `SameSite=None; Secure`

### <a name="authentication"></a>認証

次の場合は、Web ベースの認証フローを使用する必要があります。

* タブに埋め込まれたコンテンツ ページ。
* 構成ページ、タスク モジュール、およびメッセージング拡張機能。
* タスク モジュールを使用した会話型ボット。

更新された SameSite の制限に従って、リンクが外部サイトから派生した場合、ブラウザーは既に認証された Web サイトに Cookie を追加しない。 認証 Cookie にクロス サイトの使用状況のマークが付けられているか、フォールバックが正しく `SameSite=None; Secure` 設定されている必要があります。

## <a name="android-system-webview"></a>Android System WebView

Android WebView は、Android アプリが Web コンテンツを表示できる Chrome システム コンポーネントです。 新しい制限は既定ですが、Chrome 80 から始まるが、WebViews では直ちに適用されません。 これらは将来適用されます。 Android では、準備のために、ネイティブ アプリが CookieManager API を介して [直接 Cookie を設定できます](https://developer.android.com/reference/android/webkit/CookieManager)。

> [!NOTE]
> * 必要に応じて、ファースト パーティ Cookie を宣言するか `SameSite=Lax` `SameSite=Strict` 、または宣言する必要があります。
> * サードパーティの Cookie をとして宣言する必要があります `SameSite=None; Secure` 。

## <a name="see-also"></a>関連項目

* [SameSite の例](https://github.com/GoogleChromeLabs/samesite-examples)
* [SameSite Cookie のレシピ](https://web.dev/samesite-cookie-recipes/)
* [既知の互換性のないクライアント]( https://www.chromium.org/updates/same-site/incompatible-clients)
* [Developers: Get Ready for New SameSite=None; Secure Cookie Settings](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [ASP.NET および ASP.NET Core での今後の SameSite Cookie の変更点](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [HTTP Cookie](https://developer.mozilla.org/docs/Web/HTTP/Cookies)
