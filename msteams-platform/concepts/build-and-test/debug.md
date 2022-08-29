---
title: アプリをテストしてデバッグするためのセットアップを選択する
description: このモジュールでは、ローカルおよびクラウドでホストされている環境で Microsoft Teams アプリをテストおよびデバッグするためのオプションについて説明します。
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: b064fb4ef06576251a91a4727a84bb4519d4d352
ms.sourcegitcommit: d8183bad448990f7c79b1956a6c9761c27712b4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2022
ms.locfileid: "67452354"
---
# <a name="choose-a-test-setup-and-debug-your-teams-app"></a>テストセットアップを選択し、Teams アプリをデバッグする

Microsoft Teams アプリには 1 つ以上の機能が含まれており、それらを実行またはホストする方法は異なります。デバッグには、次のいずれかの方法を使用します。

* **ローカル専用**: ボットの場合は、Bot Emulator でエクスペリエンスをテストできます。 その他のコンテンツの場合は、ブラウザーでローカルに実行し、`http://localhost` を使用してコンテンツをアドレス指定できます。
* **Teams でローカルにホストされている場合**: これには、トンネリング ソフトウェアでアプリをローカルに実行し、[パッケージを作成](~/concepts/build-and-test/apps-package.md)して、Teams に [アップロード](~/concepts/deploy-and-publish/apps-upload.md)することが含まれます。 これにより、Teams クライアント内でアプリを簡単に実行およびデバッグできます。
* **Teams でクラウド ホストされている場合**: これは、Teams アプリの運用レベルのサポートを実際にシミュレートします。 これには、ソリューションを外部からアクセス可能なサーバーまたはクラウド プロバイダーにアップロードすること、および[パッケージを作成](~/concepts/build-and-test/apps-package.md)して、[Teams にアップロードする](~/concepts/deploy-and-publish/apps-upload.md)ことが含まれます。

自分のコンピューターからエクスペリエンスを実行して、ローカル専用またはローカルの Teams テストを行います。 これにより、統合開発環境内でコンパイルして実行し、ブレークポイントやステップ デバッグなどの手法を最大限に活用できます。

> [!NOTE]
> 運用環境規模のデバッグとテストでは、独自のプロセスを通じてテスト、ステージング、展開をサポートできるように、自分の会社のガイドラインに従うことをお勧めします。

複数のマニフェストとパッケージを使用して、運用サービスと開発サービスの分離を維持します。 たとえば、開発ボットと運用ボットを個別に登録し、適切なパッケージを作成してテスト環境にアップロードすることができます。 また、アプリ ストアで発行したり、顧客に配布したりするためにアプリを送信する前に、運用パッケージをアップロードしてテストすることをお勧めします。

## <a name="purely-local"></a>ローカル専用

> [!NOTE]
> ボットをローカルで実行しても、Teams アプリの機能や、参加者一覧の呼び出しやその他のチャネル固有の機能などの Teams 固有のボット機能にはアクセスできません。 さらに、一部の機能は、Teams で実行するときに機能しない可能性がある Bot Emulator の Bot Framework によって許可されます。

ボットは Bot Emulator 内で実行できます。 これにより、ボットのコア ロジックの一部をテストし、メッセージの大まかなレイアウトを確認し、簡単なテストを実行できます。 手順は次のとおりです。

1. コードをローカルで実行します。
2. Bot Emulator を起動し、URL を設定します。
   * Node.js: `http://localhost:3978/api/messages`
   * .NET/C#: `http://localhost:3979/api/messages`
3. 既定の環境変数と一致させるには、Microsoft アプリ ID と Microsoft アプリ パスワードを空白のままにします。

## <a name="locally-hosted"></a>ローカルにホストされている場合

Teams は完全にクラウドベースの製品であり、アクセスするすべてのサービスが HTTPS エンドポイントを使用してパブリックに利用できるようにする必要があります。 そのため、アプリを Teams 内で動作させるには、任意のクラウドにコードを発行するか、ローカルで実行されているインスタンスに外部からアクセスできるようにする必要があります。 後者はトンネリング ソフトウェアを使用して実行できます。

任意のツールを使用できますが、[ngrok](https://ngrok.com/download) を使用することをお勧めします。これにより、コンピューターでローカルに開くポートの外部アドレス指定可能な URL が作成されます。

Teams アプリをローカルで実行する準備として ngrok を設定するには、次の手順に従います。

1. ターミナル アプリケーションに ngrok.exe がインストールされているディレクトリに移動します。 この手順を回避するために、パス変数として追加することもできます。
2. たとえば、`ngrok http 3978 --host-header=localhost:3978` を実行するか、必要に応じてポート番号を置き換えます。
   これにより、ngrok が起動し、指定したポートで一覧表示されます。 その返しとして、ngrok が実行されている限り有効な外部アドレス指定可能な URL が提供されます。

> [!NOTE]
> ngrok を停止して再起動すると、URL が変更されます。

使用している機能に基づいてプロジェクトで ngrok を使用するには、コード、構成、manifest.json ファイル内のすべての URL 参照を置き換えて、この URL エンドポイントを使用する必要があります。

Microsoft Bot Framework に登録されているボットの場合は、この新しい ngrok エンドポイントを使用するようにボットのメッセージング エンドポイントを更新します。 たとえば、「 `https://2d1224fb.ngrok.io/api/messages` 」のように入力します。 ngrok が動作していることを検証する場合は、Bot Framework ポータルのテスト チャット ウィンドウでボットの応答をテストします。 エミュレーターと同様に、このテストでは Teams 固有の機能にアクセスすることはできません。

> [!NOTE]
> ボットのメッセージング エンドポイントを更新するには、Bot Framework を使用する必要があります。 [Bot Framework のボットのリスト](https://dev.botframework.com/bots)から、ボットを選択します。 ボットを Microsoft Azure に移行する必要はありません。 [また、Teams 用開発者ポータル](~/concepts/build-and-test/teams-developer-portal.md)を使用してメッセージング エンドポイントを更新することもできます。

## <a name="cloud-hosted"></a>クラウド ホスト型

外部アドレス指定可能な任意のサービスを使用して、開発および運用コードとその HTTPS エンドポイントをホストできます。 機能が同じサービスに存在するとは限らない。 ファイル内のオブジェクト`manifest.json`に一覧表示されている Teams アプリからすべてのドメインに[`validDomains`](~/resources/schema/manifest-schema.md#validdomains)アクセスする必要があります。

> [!NOTE]
> セキュリティで保護された環境を確保するには、参照する正確なドメインとサブドメインについて明示的に指定し、それらのドメインを制御する必要があります。たとえば、`*.azurewebsites.net` は推奨されませんが、`contoso.azurewebsites.net` をお勧めします。

## <a name="load-and-run-your-experience"></a>エクスペリエンスを読み込んで実行する

Teams 内でエクスペリエンスを読み込んで実行するには、パッケージを作成して Teams にアップロードする必要があります。 詳細については、以下を参照してください。

* [Microsoft Teams アプリのパッケージを作成する](~/concepts/build-and-test/apps-package.md)。
* [Microsoft Teams でアプリをアップロードする](~/concepts/deploy-and-publish/apps-upload.md)。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [テスト データを環境に追加する](~/concepts/build-and-test/test-data.md)

## <a name="see-also"></a>関連項目

* [IDE を使用してボットをローカルでテストおよびデバッグする](../../bots/how-to/debug/locally-with-an-ide.md#test-and-debug-your-bot-locally-with-ide)
* [Microsoft Teams タブの DevTools](../../tabs/how-to/developer-tools.md)
