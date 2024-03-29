---
title: 前提条件
author: surbhigupta
description: この記事では、Microsoft Teams の個人用、チャネル、またはグループ タブを構築するための前提条件について説明します。タブの作成に必要なツールを把握します。
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 4471d88b7f9b0fd6364c833f6b3dd910aadb300a
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2022
ms.locfileid: "68819962"
---
# <a name="prerequisites"></a>前提条件

Teams の個人用およびチャネルまたはグループのタブを作成するときは、次の前提条件を順守していることを確認します。

* X-Frame-Options と Content-Security-Policy HTTP 応答ヘッダーを使用して、iFrame でタブ ページを検出できるようにします。
  * ヘッダーの設定: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * Internet Explorer 11 との互換性を保つには、`X-Content-Security-Policy` を設定します。
  * または、ヘッダー `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` を設定します。 このヘッダーは非推奨ですが、ほとんどのブラウザーでは引き続き受け入れられます。

* ログイン ページは、クリックジャックに対する保護策として、iFrame ではレンダリングされません。 認証ロジックは、リダイレクト以外の方法を使用する必要があります。 たとえば、トークン ベースまたは Cookie ベースの認証を使用します。

    > [!NOTE]
    > デフォルトのブラウザの動作に依存するのではなく、Cookieの使用目的を設定することをお勧めします。 詳細については、「[SameSite cookie 属性](../../resources/samesite-cookie-update.md)」を参照してください。

* ブラウザの同一生成元ポリシーの制限により、Web ページが提供された Web ページとは異なるドメインにリクエストを送信することはできません。 そのため、構成ページまたはコンテンツ ページを別のドメインまたはサブドメインにリダイレクトできます。 クロスドメイン ナビゲーション ロジックでは、Teams クライアントが、タブを読み込んだり通信したりするときに、アプリ マニフェストの静的な `validDomains` リストに対してオリジンを検証できるようにする必要があります。

* Teams クライアントのテーマ、デザイン、および意図に基づいてタブのスタイルを設定します。 タブは、特定のニーズに対応し、タブのチャネル位置に関連するタスクの小さなセットまたはデータのサブセットに焦点を当てるように構築されている場合に最適に機能します。

* コンテンツ ページ内で、スクリプト タグを使用して、[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client) への参照を追加します。 ページが読み込まれたら、 を `app.initialize()`呼び出します。それ以外の場合、ページは表示されません。

* モバイル クライアントで認証を機能させるには、Teams JavaScript SDK 1.4.1 以降にアップグレードする必要があります。

* Teams モバイル クライアントに 、チャネル/グループ タブを表示するように選択した場合、`setConfig()` の構成には `websiteUrl` プロパティの値を設定する必要があります。

* Microsoft Teams タブでは、自己署名証明書を使用するイントラネット Web サイトを読み込む機能はサポートされていません。

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="tools-to-build-tabs"></a>タブを作成するツール

| &nbsp; | インストール | 使用するには... |
| --- | --- | --- |
| **必須** | &nbsp; | &nbsp; |
| &nbsp; | [Node.js](https://nodejs.org/en/download/) | バックエンド JavaScript ランタイム環境。 最新の v16 LTS リリースを使用します。|
| &nbsp; | [Microsoft Edge](https://www.microsoft.com/edge) (推奨) または [Google Chrome](https://www.google.com/chrome/) | 開発者ツールを備えたブラウザー。 |
| &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download) | JavaScript、TypeScript、または SharePoint Framework (SPFx) ビルド環境。 |
| &nbsp; | [Visual Studio 2022](https://visualstudio.microsoft.com)、 **ASP.NET および Web 開発**、または **.NET Core クロスプラットフォーム開発** ワークロード | .NET. Visual Studio 2022 の無料コミュニティ エディションをインストールできます。 |
| &nbsp; | [Git](https://git-scm.com/downloads) | GitHub のサンプル アプリ リポジトリを使用するには、Git を使用します。 |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/download-app) | Microsoft Teams を使用して、チャット、会議、通話用のアプリを通じて共同作業を行うすべてのユーザーと 1 か所で共同作業を行うことができます。 |
| &nbsp; | [ngrok](https://ngrok.com/download) | Ngrok はリバース プロキシ ソフトウェア ツールです。 Ngrok は、ローカルで実行されている Web サーバーのパブリックに利用可能な HTTPS エンドポイントへのトンネルを作成します。 サーバーの Web エンドポイントは、コンピューター上の現在のセッション中に使用できます。 コンピューターがシャットダウンまたはスリープ状態になると、サービスは使用できなくなります。 |
| &nbsp; | [Teams の開発者ポータル](https://dev.teams.microsoft.com/) | Teams アプリを構成、管理、組織や Teams ストアなどに配布するための Web ベースのポータル。 |

### <a name="build-your-teams-tab"></a>Teams タブをビルドする

次に、タブをビルドしましょう。ただし、最初にビルドするタブの選択を選択します。

> [!div class="nextstepaction"]
> [個人用のタブを作成する](~/tabs/how-to/create-personal-tab.md)
> [!div class="nextstepaction"]
> [[チャネルとグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>関連項目

* [Teams の [ビルド] タブ](../what-are-tabs.md)
* [JavaScript を使用して初めてのタブ アプリを構築する](../../sbs-gs-javascript.yml)
* [Azure AD でタブ アプリを登録する](authentication/tab-sso-register-aad.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)
