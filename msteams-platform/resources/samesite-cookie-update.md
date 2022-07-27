---
title: SameSite Cookie 属性
author: laujan
description: SameSite Cookie、その属性、Teams タブ、タスク モジュール、メッセージング拡張機能における意味、Teams での認証など、Cookie の種類について説明します。
ms.topic: reference
ms.localizationpriority: medium
ms.author: lomeybur
ms.openlocfilehash: 8f61788779d34183f7000271245e683f2750f739
ms.sourcegitcommit: 1cda2fd3498a76c09e31ed7fd88175414ad428f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2022
ms.locfileid: "67035325"
---
# <a name="samesite-cookie-attribute"></a>SameSite Cookie 属性

Cookie は、Web サイトから送信され、Web ブラウザーによってコンピューターに保存されるテキスト文字列です。 認証とパーソナル化に使用されます。 たとえば、Cookie はステートフルな情報の呼び出し、ユーザー設定の保持、閲覧アクティビティの記録、関連する広告の表示に使用されます。 Cookie は常に特定のドメインにリンクされ、さまざまな関係者によってインストールされます。

## <a name="types-of-cookies"></a>Cookie の種類

Cookie の種類とそれに対応するスコープは次のとおりです。

|クッキー|範囲|
| ------ | ------ |
|ファースト パーティ Cookie|ファースト パーティ Cookie は、ユーザーがアクセスした Web サイトによって作成されます。 これは、ショッピング カート アイテムなどのデータを保存するために使用され、資格情報にサインインします。 たとえば、認証 Cookie やその他の分析などです。|
|サードパーティ Cookie|サード パーティ Cookie は、技術的にはファースト パーティ Cookie と同じです。 違いは、データ パートナーシップ契約を通じてデータが第 2 者と共有される点です。 詳細については、「[Microsoft Teams の分析とレポート](/microsoftteams/teams-analytics-and-reports/teams-reporting-reference)」を参照してください。 |
|サード パーティ Cookie|サード パーティの Cookie は、ユーザーが明示的にアクセスしたドメイン以外のドメインによってインストールされ、追跡に使用されます。 たとえば、**[いいね]** ボタン、広告配信、ライブ チャットなどです。|

## <a name="cookies-and-http-requests"></a>Cookie と HTTP 要求

SameSite の制限が導入される前は、Cookie はブラウザーに保存されていました。 これらはすべての HTTP Web 要求にアタッチされ、`Set Cookie` HTTP 応答ヘッダーによってサーバーに送信されました。 この方法では、CSRF 攻撃と呼ばれるクロスサイト リクエスト フォージェリなどのセキュリティ脆弱性が発生しました。 SameSite コンポーネントは、SetCookie ヘッダーの実装と管理を通じて露出を減らしました。

## <a name="samesite-cookie-attribute-initial-release"></a>SameSite Cookie 属性: 初期リリース

Google Chrome バージョン 51 では、この `SetCookie SameSite` 仕様が省略可能な属性として導入されました。 ビルド 17672 以降の Windows 10 は、[Microsoft&nbsp;Edgeブラウザー](https://blogs.windows.com/msedgedev/2018/05/17/samesite-cookies-microsoft-edge-internet-explorer/)向けの SameSite Cookie のサポートを導入しました。

`SetCookie` ヘッダーへの SameSite Cookie 属性の追加をオプトアウトするか、**Lax** と **Strict** の 2 つの設定のいずれかを使用して追加できます。実装されていない SameSite 属性が既定の状態と見なされました。

## <a name="samesite-cookie-attribute-2020-release"></a>SameSite Cookie 属性: 2020 リリース

Chrome 80 (2020 年 2 月リリース) では、新しい Cookie 値を紹介し、既定で Cookie ポリシーを設定します。 更新された SameSite 属性には、**Strict**、**Lax**、または **None** という 3 つの値が渡されます。 指定しない場合、Cookies SameSite 属性は既定で値 `SameSite=Lax` を受け取ります。

SameSite Cookie 属性は次のとおりです。

|Setting | 施行 | 値 |属性仕様 |
| -------- | ----------- | --------|--------|
| **Lax**  | Cookie は、**ファースト パーティ** コンテキストと HTTP GET 要求でのみ自動的に送信されます。 SameSite Cookie は、イメージや iframe を読み込むための呼び出し音など、サイト横断的なサブ要求に対して保留されます。 ユーザーがリンクをたどるなどして外部サイトから URL に移動したときに送信されます。| **Default** |`Set-Cookie: key=value; SameSite=Lax`|
| **Strict** |ブラウザーは、ファースト パーティのコンテキスト要求に対してのみ Cookie を送信します。 これらは、Cookie を設定するサイトから送信された要求です。 要求が現在の場とは異なる URL から送信された場合、`Strict` 属性でタグ付けされた Cookie は送信されません。| 省略可能 |`Set-Cookie: key=value; SameSite=Strict`|
| **なし** | Cookie は、ファースト パーティコンテキストとクロスオリジン要求の両方で送信されます。ただし、値を明示的に設定する **`None`** 必要があり、すべてのブラウザー要求は **HTTPS プロトコルに従い** 、暗号化された接続が **`Secure`** 必要な属性を含める必要があります。 その要件に準拠していない Cookie は **拒否されます**。 <br/>**両方の属性が一緒に必要です**。 HTTPS プロトコルを使用せずに **`Secure`** 指定した場合 **`None`**、または HTTPS プロトコルが使用されていない場合、サード パーティの Cookie は拒否されます。| 省略可能ですが、設定した場合は HTTPS プロトコルが必要です。 |`Set-Cookie: key=value; SameSite=None; Secure` |

## <a name="teams-implications-and-adjustments"></a>Teams の影響と調整

1. Cookie に関連する SameSite 設定を有効にし、アプリと拡張機能が引き続き Teams で機能することを確認します。
1. アプリまたは拡張機能が失敗した場合は、Chrome 80 のリリース前に必要な修正を行います。
1. Microsoft 社内パートナーは、この問題の詳細やヘルプを得るために、以下のチームに参加することができます: <https://teams.microsoft.com/l/team/19%3A08b594cd465e4c0491fb751e823802e2%40thread.skype/conversations?groupId=4d6d04cd-dbf0-43c8-a2ff-f80dd38be034&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47>。

> [!NOTE]
> Cookie の使用目的を反映するように SameSite 属性を設定する必要があります。 既定のブラウザーの動作に依存しないでください。 詳細については、「[Developers: Get Ready for New SameSite=None; Secure Cookie Settings](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)」を参照してください。

### <a name="tabs-task-modules-and-message-extensions"></a>タブ、タスク モジュール、メッセージ拡張機能

* Teams タブは、`<iframes>` を使用して、最上位レベルまたはファースト パーティのコンテキストで表示されるコンテンツを埋め込みます。
* タスク モジュールを使用すると、Teams アプリケーションでモーダル ポップアップ エクスペリエンスを作成できます。 タブと同様に、モーダル ウィンドウが現在のページ内で開きます。
* メッセージ拡張機能を使用すると、外部リソースからのチャット メッセージに強化されたコンテンツを挿入できます。

`<iframe>` に表示される場合、埋め込みコンテンツで使用される Cookie は、サード パーティーとみなされます。さらに、ページ上のリモート リソースが要求 `<img>`、`<script>` タグ、外部フォント、カスタマイズされたコンテンツとともに送信される Cookie に依存している場合は、`SameSite=None; Secure` など、サイト横断的に使用できるようにマークされているか、フォールバックが確実に実行されている必要があります。

### <a name="authentication"></a>認証

次の場合は、Web ベースの認証フローを使用する必要があります。

* タブに埋め込まれたコンテンツ ページ。
* 構成ページ、タスク モジュール、メッセージング拡張機能。
* タスク モジュールを使用した会話性ボット。

更新された SameSite の制限に従って、リンクが外部サイトから派生した場合、ブラウザーは既に認証された Web サイトに Cookie を追加しません。 認証 Cookie で `SameSite=None; Secure` をサイト横断的に使用できるようにマークしておくか、フォールバックを確実に実行する必要があります。

## <a name="android-system-webview"></a>Android System WebView

Android WebView は、Android アプリが Web コンテンツを表示できるようにする Chrome システム コンポーネントです。 新しい制限は既定ですが、Chrome 80 以降では、WebView ではすぐに適用されません。 これらは今後適用される予定です。 準備のために、Android ではネイティブ アプリが [CookieManager API](https://developer.android.com/reference/android/webkit/CookieManager) 経由で直接 Cookie を設定できます。

> [!NOTE]
>
> * ファースト パーティ Cookie は、必要に応じて `SameSite=Lax` または `SameSite=Strict` として宣言する必要があります。
> * サード パーティ Cookie を `SameSite=None; Secure` として宣言する必要があります。

## <a name="see-also"></a>関連項目

* [SameSite の例](https://github.com/GoogleChromeLabs/samesite-examples)
* [SameSite Cookie レシピ](https://web.dev/samesite-cookie-recipes/)
* [既知の互換性のないクライアント]( https://www.chromium.org/updates/same-site/incompatible-clients)
* [Developers: Get Ready for New SameSite=None; Secure Cookie Settings](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [ASP.NET および ASP.NET Core での今後の SameSite Cookie の変更点](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [HTTP Cookie](https://developer.mozilla.org/docs/Web/HTTP/Cookies)
