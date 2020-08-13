---
title: Teams アプリをデバッグする
description: Microsoft Teams アプリを実行およびデバッグするために実行する手順について説明します。
keywords: teams でデバッグアプリを実行する
ms.topic: conceptual
ms.openlocfilehash: 913306bd24a55797e72396a031d917ec99c43bb9
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652090"
---
# <a name="debugging-your-teams-app"></a>Teams アプリをデバッグする

Microsoft Teams アプリには、1つ以上の機能を含めることができます。また、実行またはホストする方法も異なる場合があります。 通常、デバッグに関しては、Microsoft Teams アプリを実行するための次のような方法があります。

* **完全にローカル** &emsp;Bot の場合、Bot エミュレーターで体験をテストできます。 その他のコンテンツの場合は、ブラウザーでローカルに実行し、を使用してコンテンツのアドレスを入力でき `http://localhost` ます。
* Teams でローカルにホストされて**いる** &emsp;これには、トンネリングソフトウェアでローカルに実行し、Teams に[アップロード](~/concepts/deploy-and-publish/apps-upload.md)する[パッケージを作成](~/concepts/build-and-test/apps-package.md)する必要があります。 これにより、Teams クライアント内でアプリを簡単に実行およびデバッグできるようになります。
* **Teams でのクラウドホスト**これは、Teams アプリの運用レベルのサポートを完全にシミュレート (または) します。 外部からアクセス可能なサーバーまたはクラウドのプロバイダーにソリューションをアップロードする (もちろん、Azure をお勧めします)。また、チームに[アップロード](~/concepts/deploy-and-publish/apps-upload.md)する[パッケージを作成](~/concepts/build-and-test/apps-package.md)する必要があります。

ローカルまたはローカルの Teams テストの場合は、自分のコンピューターから実行します。 これにより、実際には IDE 内でコンパイルして実行することができ、ブレークポイントやステップのデバッグなどの手法を十分に活用することができます。 運用段階のデバッグおよびテストでは、独自のプロセスによってテスト、ステージング、および展開をサポートできるようにするために、自社のガイドラインに従うことをお勧めします。

一般的に、運用サービスと開発サービスを分離して維持するために、複数のマニフェストとパッケージを使用することをお勧めします。 たとえば、個別の開発および運用のボットを登録し、テスト環境でそれらをアップロードするための適切なパッケージを作成することができます。 また、アプリストアに発行するためにアプリを提出する前に、または顧客に配布する前に、運用パッケージをアップロードしてテストすることをお勧めします。

## <a name="purely-local"></a>完全にローカル

> [!NOTE]
> この方法を実行しても、Teams アプリの機能や、名簿呼び出しやその他のチャネル固有の機能などの Teams 固有の bot 機能にアクセスすることはできません。 さらに、一部の機能は、Microsoft Teams での実行時に機能しない可能性がある Bot エミュレーターの Bot フレームワークによって許可されることがあります。

Bot は Bot エミュレーター内で実行できます。 これにより、ボットのコアロジックの一部をテストし、メッセージの大まかなレイアウトを確認し、単純なテストを実行することができます。 それらのステップは次のとおりです。

* コードをローカルで実行する
* Bot エミュレーターを起動し、次のように URL を設定します。
  * Node.js:`http://localhost:3978/api/messages`
  * .NET/C#:`http://localhost:3979/api/messages`
* 既定の環境変数と一致させるには、Microsoft app ID と Microsoft app のパスワードを空白のままにします。

## <a name="locally-hosted"></a>ローカルでホストされる

Microsoft Teams は完全なクラウドベースの製品であるため、HTTPS エンドポイントを使用してアクセスできるようにするすべてのサービスを公開する必要があります。 そのため、Teams 内でアプリを使用できるようにするには、選択したクラウドにコードを発行するか、ローカルで実行しているインスタンスを外部からアクセス可能にする必要があります。 トンネルソフトウェアを使用して後者を行うことができます。

任意のツールを使用することもできますが、 [ngrok](https://ngrok.com/download)を使用して、コンピューター上でローカルに開くポートに対して、外部アドレス指定可能な URL を作成することをお勧めします。 Microsoft Teams アプリをローカルで実行するための準備として ngrok をセットアップするには、次のようにします。

* ターミナルアプリケーションで、ngrok.exe インストールされているディレクトリに移動します。 この手順を回避するには、この値を path 変数として追加することをお勧めします。
* などを実行し、 `ngrok http 3978 --host-header=localhost:3978` 必要に応じてポート番号を置き換えます。

これにより、指定したポートをリッスンする ngrok が起動します。 これにより、ngrok が実行されている限り、外部的にアドレス指定可能な URL が得られます。

> [!NOTE]
> Ngrok を停止してから再起動すると、URL が変更されます。

プロジェクトで ngrok を使用し、使用している機能に応じて、この URL エンドポイントを使用するには、コード、構成、またはファイルの manifest.js内のすべての URL 参照を置換する必要があります。

たとえば、Microsoft Bot フレームワークに登録されている bot の場合、この新しい ngrok エンドポイントを使用するように bot のメッセージングエンドポイントを更新します。 たとえば、`https://2d1224fb.ngrok.io/api/messages` などです。 Bot フレームワークポータルの [テストチャット] ウィンドウでボット応答をテストすることによって、ngrok が動作していることを確認できます。 (エミュレーターと同様に、このテストでは Teams 固有の機能にアクセスすることはできません)。

> [!NOTE]
> Bot のメッセージングエンドポイントを更新するには、Bot フレームワークを使用する必要があります。 Bot フレームワークの bot[リスト](https://dev.botframework.com/bots)で、bot をクリックします。 Bot を Microsoft Azure に移行する必要はありません。 また、[アプリケーション Studio](~/concepts/build-and-test/app-studio-overview.md)を使用してメッセージングエンドポイントを更新することもできます。

## <a name="cloud-hosted"></a>クラウド ホスト型

外部的に指定可能なサービスを使用して、開発および運用のコードと HTTPS エンドポイントをホストできます。 機能が同じサービスに存在することは想定されていません。 Microsoft Teams アプリからアクセスされるすべてのドメインは、[ファイルの manifest.jsのオブジェクトに一覧表示される必要があり [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) ます。

> [!NOTE]
> 安全な環境を確保するには、参照する正確なドメインとサブドメインを明確にし、それらのドメインが制御に含まれている必要があります。 たとえば、は `*.azurewebsites.net` 推奨されませんが、そうすることになり `contoso.azurewebsites.net` ます。

## <a name="loading-and-running"></a>読み込みと実行

一般に、Microsoft Teams 内での使用状況を読み込んで実行するには、次のガイダンスを使用してパッケージを作成し、Teams にアップロードする必要があります。

* [Microsoft Teams アプリ用のパッケージを作成する](~/concepts/build-and-test/apps-package.md)
* [Microsoft Teams でアプリをアップロードする](~/concepts/deploy-and-publish/apps-upload.md)
