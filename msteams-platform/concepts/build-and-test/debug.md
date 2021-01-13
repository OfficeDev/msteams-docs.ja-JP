---
title: アプリをテストおよびデバッグするためのセットアップの選択
description: Microsoft Teams アプリをテストおよびデバッグするためのオプションについて説明します。
keywords: チームがデバッグ アプリを実行する
ms.topic: conceptual
ms.openlocfilehash: ea851a0d3ecf3ec87093bcc095050190a282c25e
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797800"
---
# <a name="choosing-a-setup-to-test-and-debug-your-microsoft-teams-app"></a>Microsoft Teams アプリをテストおよびデバッグするためのセットアップの選択

Microsoft Teams アプリには 1 つ以上の機能を含め、それらを実行またはホストする方法は異なる場合があります。 デバッグに関しては、通常、Microsoft Teams アプリを実行する方法は次のとおりです。

* **純粋にローカル** &emsp;ボットの場合は、Bot Emulator でエクスペリエンスをテストできます。 その他のコンテンツについては、ブラウザーでローカルに実行し、コンテンツにアドレスを指定できます `http://localhost` 。
* **Teams でローカルにホストされる** &emsp;これには、トンネリング ソフトウェアを使用してローカル [](~/concepts/build-and-test/apps-package.md)で実行し、Teams にアップロードするパッケージ [を作成する](~/concepts/deploy-and-publish/apps-upload.md)必要があります。 これにより、Teams クライアント内でアプリを簡単に実行およびデバッグできます。
* **クラウド ホスト型 (Teams)** これは、Teams アプリの実稼働レベルのサポートを真にシミュレート (つまり) します。 外部からアクセス可能なサーバーまたはクラウド プロバイダーにソリューションをアップロードし (もちろん、Azure をお勧めします)、Teams[](~/concepts/build-and-test/apps-package.md)にアップロードするパッケージ[](~/concepts/deploy-and-publish/apps-upload.md)を作成します。

純粋にローカルまたはローカルの Teams テストの場合は、独自のコンピューターからエクスペリエンスを実行します。 これにより、IDE 内で実際にコンパイルして実行し、ブレークポイントやステップ デバッグなどの手法をフルに活用できます。 実稼働規模のデバッグとテストでは、独自のプロセスを通じてテスト、ステージング、展開を確実にサポートするために、独自の会社のガイドラインに従う必要があります。

一般に、複数のマニフェストとパッケージを使用して、実稼働サービスと開発サービスの分離を維持することをお勧めします。 たとえば、開発ボットと実稼働ボットを個別に登録し、テスト環境でアップロードする適切なパッケージを作成できます。 また、アプリ ストアで公開するアプリを提出する前、またはユーザーに配布する前に、製品パッケージをアップロードしてテストすることをお勧めします。

## <a name="purely-local"></a>純粋にローカル

> [!NOTE]
> この方法では、Teams アプリ機能や、名簿呼び出しなどの Teams 固有のボット機能や、その他のチャネル固有の機能にアクセスできます。 また、一部の機能は、Microsoft Teams で実行すると機能しないボット エミュレーターの Bot Framework で許可される場合があります。

ボットは Bot Emulator 内で実行できます。 これにより、ボットのコア ロジックの一部をテストし、メッセージの大まかなレイアウトを確認し、簡単なテストを実行できます。 それらのステップは次のとおりです。

* コードをローカルで実行する
* Bot Emulator を起動し、URL を設定します。
  * Node.js: `http://localhost:3978/api/messages`
  * .NET/C#: `http://localhost:3979/api/messages`
* 既定の環境変数と一致するには、Microsoft アプリ ID と Microsoft アプリパスワードを空白のままにします。

## <a name="locally-hosted"></a>ローカルにホストされる

Microsoft Teams は完全にクラウドベースの製品なので、アクセスするサービスはすべて HTTPS エンドポイントを使用して一般に利用できる必要があります。 そのため、アプリが Teams 内で動作するには、選択したクラウドにコードを公開するか、ローカルで実行中のインスタンスを外部からアクセス可能にする必要があります。 この操作は、トンネリング ソフトウェアを使用して行います。

任意のツールを使用することもできますが、ngrok を使用して推奨します [。ngrok](https://ngrok.com/download)は、コンピューター上でローカルに開くポートの外部アドレス指定可能な URL を作成します。 Microsoft Teams アプリをローカルで実行する準備として ngrok をセットアップするには、

* ターミナル アプリケーションで、インストールしたディレクトリにngrok.exeします。 この手順を回避するために、パス変数として追加できます。
* たとえば、ポート番号を `ngrok http 3978 --host-header=localhost:3978` 必要に応じて置き換え、実行します。

これにより、ngrok が起動し、指定したポートでリッスンします。 その結果、ngrok が実行されている限り有効な外部アドレス指定可能な URL が提供されます。

> [!NOTE]
> ngrok を停止して再起動すると、URL が変更されます。

プロジェクトで ngrok を使用し、使用している機能に応じて、この URL エンドポイントを使用するには、ファイル上のコード、構成、または manifest.jsのすべての URL 参照を置き換える必要があります。

たとえば、Microsoft Bot Framework に登録されているボットの場合は、ボットのメッセージング エンドポイントを更新して、この新しい ngrok エンドポイントを使用します。 たとえば、`https://2d1224fb.ngrok.io/api/messages` などです。 Bot Framework ポータルの [テスト チャット] ウィンドウでボットの応答をテストすることで、ngrok が動作を検証できます。 (エミュレーターと同様に、このテストでは Teams 固有の機能にアクセスできません)。

> [!NOTE]
> ボットのメッセージング エンドポイントを更新するには、Bot Framework を使用する必要があります。 Bot Framework のボット [の一覧でボットをクリックします](https://dev.botframework.com/bots)。 ボットを Microsoft Azure に移行する必要はない。 また [、App Studio](~/concepts/build-and-test/app-studio-overview.md)を使用してメッセージング エンドポイントを更新することもできます。

## <a name="cloud-hosted"></a>クラウド ホスト型

外部でアドレス指定可能な任意のサービスを使用して、開発コードと実稼働コード、および HTTPS エンドポイントをホストできます。 機能が同じサービスに存在する可能性はありません。 Microsoft Teams アプリからアクセスしているすべてのドメインが、ファイルの manifest.js内 [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) のオブジェクトに一覧表示されている必要があります。

> [!NOTE]
> 安全な環境を確保するには、参照する正確なドメインとサブドメインを明示的に指定し、それらのドメインを制御する必要があります。 たとえば、 `*.azurewebsites.net` お勧めできませんが、推奨 `contoso.azurewebsites.net` されます。

## <a name="loading-and-running"></a>読み込みと実行

一般に、Microsoft Teams 内でエクスペリエンスを読み込み、実行するには、次のガイダンスに従ってパッケージを作成し、Teams にアップロードする必要があります。

* [Microsoft Teams アプリのパッケージを作成する](~/concepts/build-and-test/apps-package.md)
* [Microsoft Teams でアプリをアップロードする](~/concepts/deploy-and-publish/apps-upload.md)
