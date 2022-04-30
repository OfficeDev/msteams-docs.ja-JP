---
title: 前提条件
author: surbhigupta
description: Microsoft Teams のすべてのタブは、これらの要件に準拠している必要があります。
keywords: 構成可能なチーム タブ グループ チャネル
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 2ac02c7c78fca1ddf4c64e2718cdaf840b0ae59b
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2022
ms.locfileid: "65110282"
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

* コンテンツ ページ内で、スクリプト タグを使用して、[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client) への参照を追加します。 ページが読み込まれたら、`microsoftTeams.initialize()` への呼び出しを行います。それ以外の場合、ページは表示されません。

* モバイル クライアントで認証を機能させるには、Teams JavaScript SDK 1.4.1 以降にアップグレードする必要があります。

* Teams モバイル クライアントに 、チャネル/グループ タブを表示するように選択した場合、`setSettings()` の構成には `websiteUrl` プロパティの値を設定する必要があります。

* [Microsoft Teams] タブでは、自己署名証明書を使用するイントラネット Web サイトを読み込む機能はサポートされません。

## <a name="tools-to-build-tabs"></a>タブを作成するツール

| &nbsp; | インストール | 使用するには... |
| --- | --- | --- |
| **必須** | &nbsp; | &nbsp; |
| &nbsp; | [Node.js](https://nodejs.org/en/download/) | バックエンド JavaScript ランタイム環境。 最新の v14 LTS リリースを使用します。|
| &nbsp; | [Microsoft Edge](https://www.microsoft.com/edge) (推奨) または [Google Chrome](https://www.google.com/chrome/) | 開発者ツールを備えたブラウザー。 |
| &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download) | JavaScript、TypeScript、または SharePoint Framework (SPFx) ビルド環境。 |
| &nbsp; | [Visual Studio 2019](https://visualstudio.com/download)、**ASP.NET と Web 開発**、**または .NET Core クロスプラットフォーム開発** ワークロード | .NET。Visual Studio 2019 の無料コミュニティ エディションをインストールできます。 |
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

* [Teams タブ](~/tabs/what-are-tabs.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)