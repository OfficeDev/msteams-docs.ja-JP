---
title: 前提条件
author: surbhigupta
description: これらの要件にMicrosoft Teamsタブは必ず遵守する必要があります。
keywords: teams タブ グループ チャネル構成可能
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: fe72691465ca785cefb6a96c8eb4005a64601a17
ms.sourcegitcommit: 3dc9b539c6f7fbfb844c47a78e3b4d2200dabdad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2022
ms.locfileid: "64571517"
---
# <a name="prerequisites"></a>前提条件

個人用タブとチャネル タブまたはグループ タブの作成中に、Teams前提条件を満たしていることを確認します。

* X-Frame-Options と Content-Security-Policy HTTP 応答ヘッダーを使用して、タブ ページを iFrame で検出できます。
  * ヘッダーの設定: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * 11 Internet Explorer互換性の場合は、 を設定します `X-Content-Security-Policy`。
  * または、ヘッダーを設定します `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`。 このヘッダーは非推奨ですが、ほとんどのブラウザーでは引き続き受け入れ可能です。

* ログイン ページは、クリックジャックに対する保護手段として、iFrame では表示されません。 認証ロジックでは、リダイレクト以外のメソッドを使用する必要があります。 たとえば、トークンベースまたは Cookie ベースの認証を使用します。

    > [!NOTE]
    > 既定のブラウザー動作に依存するのではなく、Cookie の使用目的を設定することを推奨します。 詳細については、「 [SameSite cookie 属性」を参照してください](../../resources/samesite-cookie-update.md)。

* ブラウザーの同一発生元ポリシー制限により、Web ページは、提供された Web ページとは異なるドメインに対して要求を行うのを防止します。 そのため、構成ページまたはコンテンツ ページを別のドメインまたはサブドメインにリダイレクトできます。 クロスドメイン ナビゲーション ロジックでは、Teams クライアントがタブの`validDomains`読み込みまたは通信時にアプリ マニフェストの静的リストに対して原点を検証できる必要があります。

* クライアントのテーマ、デザイン、およびTeamsに基づいてタブのスタイルを設定します。 タブは、特定の必要性に対処し、小さなタスクセットまたはタブのチャネル位置に関連するデータのサブセットに焦点を当てするために構築されている場合に最適です。

* コンテンツ ページ内で、スクリプト タグを使用して [JavaScript Microsoft Teams SDK](/javascript/api/overview/msteams-client) への参照を追加します。 ページの読み込み後に、呼び `microsoftTeams.initialize()`出しを行います。それ以外の場合、ページは表示されません。

* モバイル クライアントで認証を機能するには、JavaScript SDK 1.4.1 以降Teamsにアップグレードする必要があります。

* モバイル クライアントにチャネル`setSettings()`またはグループ タブを表示する場合Teams構成には、プロパティの値が必要`websiteUrl`です。

* Microsoft Teamsタブでは、自己署名証明書を使用するイントラネット Web サイトを読み込む機能がサポートされていません。

## <a name="tools-to-build-tabs"></a>タブを作成するツール

| &nbsp; | インストール | using... |
| --- | --- | --- |
| **必須** | &nbsp; | &nbsp; |
| &nbsp; | [Node.js](https://nodejs.org/en/download/) | バック エンド JavaScript ランタイム環境。 最新の v14 LTS リリースを使用します。|
| &nbsp; | [Microsoft Edge](https://www.microsoft.com/edge) (推奨) または [Google Chrome](https://www.google.com/chrome/) | 開発者ツールを含むブラウザー。 |
| &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download) | JavaScript、TypeScript、または SharePoint Framework (SPFx) ビルド環境。 |
| &nbsp; | [Visual Studio 2019](https://visualstudio.com/download)、ASP.NET **Web 開発**、**または .NET Core** クロスプラットフォーム開発ワークロード | .NET。 2019 年の無料コミュニティ エディションVisual Studioできます。 |
| &nbsp; | [Git](https://git-scm.com/downloads) | Git を使用して、サンプル アプリリポジトリを使用GitHub。 |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/download-app) | Microsoft Teams、会議、通話のアプリを通じて作業するすべてのユーザーと共同作業を 1 か所で行います。 |
| &nbsp; | [ngrok](https://ngrok.com/download) | Ngrok はリバース プロキシ ソフトウェア ツールです。 Ngrok は、ローカルで実行中の Web サーバーのパブリックに利用可能な HTTPS エンドポイントへのトンネルを作成します。 サーバーの Web エンドポイントは、コンピューター上の現在のセッション中に使用できます。 コンピューターがシャットダウンまたはスリープ状態になった場合、サービスは使用できなくなりました。 |
| &nbsp; | [Teams の開発者ポータル](https://dev.teams.microsoft.com/) | Web ベースのポータルを使用して、組織や組織Teamsストアにアプリを構成、管理、配布Teamsします。 |

### <a name="build-your-teams-tab"></a>[ビルド] タブTeamsする

次に、タブを作成します。しかし、最初に、ビルドするタブの選択を選択します。

> [!div class="nextstepaction"]
> [個人用のタブを作成する](~/tabs/how-to/create-personal-tab.md)
> [!div class="nextstepaction"]
> [チャネルまたはグループ タブを作成する](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>関連項目

* [Teamsタブ](~/tabs/what-are-tabs.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)