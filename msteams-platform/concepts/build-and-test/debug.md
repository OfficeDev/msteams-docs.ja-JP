---
title: アプリをテストしてデバッグするためのセットアップを選択する
description: ローカルおよびクラウドでホストされる環境で Microsoft Teams アプリをテストおよびデバッグするためのオプションについて説明します。
keywords: チームがローカル クラウド ホストのホストでデバッグ アプリを実行する
ms.localizationpriority: high
ms.topic: conceptual
ms.openlocfilehash: e87032cbe9b116aa0ddbe816169c2763301edd07
ms.sourcegitcommit: 591bab4c7e01ac9099b9a540f149b64e6e31e6e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2022
ms.locfileid: "65135760"
---
# <a name="choose-a-setup-to-test-and-debug-your-microsoft-teams-app"></a>Microsoft Teams アプリをテストしてデバッグするためのセットアップを選択する

Microsoft Teams アプリには 1 つ以上の機能が含まれており、それらを実行またはホストする方法は異なります。 デバッグには、次のいずれかの方法を使用します。

* **ローカル専用**: ボットの場合は、Bot Emulator でエクスペリエンスをテストできます。 その他のコンテンツの場合は、ブラウザーでローカルに実行し、`http://localhost` を使用してコンテンツをアドレス指定できます。
* **Teams でローカルにホストされている場合**: これには、トンネリング ソフトウェアでアプリをローカルに実行し、[パッケージを作成](~/concepts/build-and-test/apps-package.md)して、Teams に [アップロード](~/concepts/deploy-and-publish/apps-upload.md)することが含まれます。 これにより、Teams クライアント内でアプリを簡単に実行およびデバッグできます。
* **Teams でクラウド ホストされている場合**: これは、Teams アプリの運用レベルのサポートを実際にシミュレートします。 これには、ソリューションを外部からアクセス可能なサーバーまたはクラウド プロバイダーにアップロードすること、および[パッケージを作成](~/concepts/build-and-test/apps-package.md)して、[Teams にアップロードする](~/concepts/deploy-and-publish/apps-upload.md)ことが含まれます。

自分のコンピューターからエクスペリエンスを実行して、ローカル専用またはローカルの Teams テストを行います。 これにより、統合開発環境内でコンパイルして実行し、ブレークポイントやステップ デバッグなどの手法を最大限に活用できます。

> [!NOTE]
> 運用環境規模のデバッグとテストでは、独自のプロセスを通じてテスト、ステージング、展開をサポートできるように、自分の会社のガイドラインに従うことをお勧めします。

複数のマニフェストとパッケージを使用して、運用サービスと開発サービスの分離を維持します。 たとえば、開発ボットと運用ボットを個別に登録し、適切なパッケージを作成してテスト環境にアップロードすることができます。 また、アプリ ストアで発行したり、顧客に配布したりするためにアプリを送信する前に、運用パッケージをアップロードしてテストすることをお勧めします。

## <a name="purely-local"></a>ローカル専用

> [!NOTE]
> ボットをローカルで実行しても、Teams アプリの機能や、参加者一覧の呼び出しやその他のチャネル固有の機能などの Teams 固有のボット機能にはアクセスできません。 さらに、一部の機能は、Microsoft Teams で実行しているときに機能しない可能性がある Bot Emulator の Bot Framework によって許可されます。

ボットは Bot Emulator 内で実行できます。 これにより、ボットのコア ロジックの一部をテストし、メッセージの大まかなレイアウトを確認し、簡単なテストを実行できます。 手順は次のとおりです。

1. コードをローカルで実行します。
2. Bot Emulator を起動し、URL を設定します。
   * Node.js: `http://localhost:3978/api/messages`
   * .NET/C#: `http://localhost:3979/api/messages`
3. 既定の環境変数と一致させるには、Microsoft アプリ ID と Microsoft アプリ パスワードを空白のままにします。

## <a name="locally-hosted"></a>ローカルにホストされている場合

Microsoft Teams は完全にクラウドベースの製品であり、HTTPS エンドポイントを使用してアクセスするすべてのサービスをパブリックに利用できるようにする必要があります。 そのため、アプリを Teams 内で動作させるには、任意のクラウドにコードを発行するか、ローカルで実行されているインスタンスに外部からアクセスできるようにする必要があります。 後者はトンネリング ソフトウェアを使用して実行できます。

任意のツールを使用できますが、[ngrok](https://ngrok.com/download) を使用することをお勧めします。これにより、コンピューターでローカルに開くポートの外部アドレス指定可能な URL が作成されます。

Microsoft Teams アプリをローカルで実行するための準備として ngrok を設定するには、次の手順に従います:

1. ターミナル アプリケーションに ngrok.exe がインストールされているディレクトリに移動します。 この手順を回避するために、パス変数として追加することもできます。
2. たとえば、`ngrok http 3978 --host-header=localhost:3978` を実行するか、必要に応じてポート番号を置き換えます。
   これにより、ngrok が起動し、指定したポートで一覧表示されます。 その返しとして、ngrok が実行されている限り有効な外部アドレス指定可能な URL が提供されます。

> [!NOTE]
> ngrok を停止して再起動すると、URL が変更されます。

使用している機能に基づいてプロジェクトで ngrok を使用するには、コード、構成、manifest.json ファイル内のすべての URL 参照を、この URL エンドポイントを使用するように置き換える必要があります。

Microsoft Bot Framework に登録されているボットの場合は、この新しい ngrok エンドポイントを使用するようにボットのメッセージング エンドポイントを更新します。 たとえば、「 `https://2d1224fb.ngrok.io/api/messages` 」のように入力します。 ngrok が動作していることを検証する場合は、Bot Framework ポータルのテスト チャット ウィンドウでボットの応答をテストします。 このテストでも、エミュレーターと同様に、Teams 固有の機能にアクセスすることはできません。

> [!NOTE]
> * ボットのメッセージング エンドポイントを更新するには、Bot Framework を使用する必要があります。 [Bot Framework のボットのリスト](https://dev.botframework.com/bots)から、ボットを選択します。 ボットを Microsoft Azure に移行する必要はありません。 また、[App Studio](~/concepts/build-and-test/app-studio-overview.md) を使用してメッセージング エンドポイントを更新することもできます。
> * App Studio を使用している場合は、Teams アプリを構成、配布、管理するための開発者ポータルを試してみることをお勧めします。App Studio は 2022 年 6 月 30 日までに非推奨になります

## <a name="cloud-hosted"></a>クラウド ホスト型

外部アドレス指定可能な任意のサービスを使用して、開発および運用コードとその HTTPS エンドポイントをホストできます。 機能が同じサービスにあることを期待するものではありません。 `manifest.json` ファイルの [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) オブジェクトに一覧表示されている Microsoft Teams アプリからすべてのドメインにアクセスする必要があります。

> [!NOTE]
> セキュリティで保護された環境を確保するには、参照する正確なドメインとサブドメインについて明示的に指定し、それらのドメインを制御する必要があります。 たとえば、`*.azurewebsites.net` は推奨されませんが、`contoso.azurewebsites.net` をお勧めします。

## <a name="load-and-run-your-experience"></a>エクスペリエンスを読み込んで実行する

Microsoft Teams 内でエクスペリエンスを読み込んで実行するには、パッケージを作成して Teams にアップロードする必要があります。 詳細については、以下を参照してください。

* [Microsoft Teams アプリのパッケージを作成する](~/concepts/build-and-test/apps-package.md)。
* [Microsoft Teams でアプリをアップロードする](~/concepts/deploy-and-publish/apps-upload.md)。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [テスト データを環境に追加する](~/concepts/build-and-test/test-data.md)

## <a name="see-also"></a>関連項目

[ボットをローカルでテストしてデバッグする](../../bots/how-to/debug/locally-with-an-ide.md#test-and-debug-your-bot-locally)
