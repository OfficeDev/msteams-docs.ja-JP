---
title: アプリをテストおよびデバッグするためのセットアップの選択
description: アプリのテストとデバッグのMicrosoft Teams説明します。
keywords: チームがデバッグ アプリを実行する
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 1f11834ad83e8bea7e4114d25d022df2f62c1700
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565159"
---
# <a name="choose-a-setup-to-test-and-debug-your-microsoft-teams-app"></a>アプリをテストおよびデバッグするセットアップMicrosoft Teamsする

Microsoft Teamsには 1 つ以上の機能が含まれているので、それらを実行またはホストする方法は異なります。 デバッグには、次のいずれかの方法を使用します。

* **純粋にローカル**: ボットの場合は、ボット エミュレーターでエクスペリエンスをテストできます。 その他のコンテンツについては、ブラウザーでローカルで実行し、コンテンツにアドレスを指定できます `http://localhost` 。
* **ローカルでホストされる** Teams : これには、トンネリング ソフトウェアでアプリをローカルで実行 [](~/concepts/build-and-test/apps-package.md)し、アプリに [](~/concepts/deploy-and-publish/apps-upload.md)アップロードするパッケージを作成Teams。 これにより、アプリをクライアント内で簡単に実行Teamsできます。
* **クラウド ホスト型のTeams:** これは、アプリの実稼働レベルのサポートをTeamsします。 外部からアクセス可能なサーバーまたはクラウド プロバイダーにソリューションをアップロードし、ソリューションにアップロードする[](~/concepts/build-and-test/apps-package.md)パッケージを作成Teams。 [](~/concepts/deploy-and-publish/apps-upload.md)

独自のコンピューターからエクスペリエンスを実行して、ローカルまたはローカルのテストTeamsします。 これにより、統合された開発環境内でコンパイルおよび実行し、ブレークポイントやステップ デバッグなどの手法を活用できます。 

> [!NOTE]
> 実稼働規模のデバッグとテストでは、独自のプロセスを通じてテスト、ステージング、および展開をサポートするために、独自の会社のガイドラインに従う必要があります。

複数のマニフェストとパッケージを使用して、実稼働サービスと開発サービスの分離を維持します。 たとえば、個別の開発ボットと実稼働ボットを登録し、テスト環境でアップロードする適切なパッケージを作成できます。 また、アプリストアでの発行や顧客への配布のためにアプリを提出する前に、実稼働パッケージをアップロードしてテストすることをお勧めします。

## <a name="purely-local"></a>純粋にローカル

> [!NOTE]
> ボットをローカルで実行しても、Teams アプリの機能や、Teams 固有のボット機能 (名簿呼び出しなどのチャネル固有の機能など) にアクセスできます。 さらに、ボット エミュレーターでボット フレームワークによって許可される機能の中には、ボット エミュレーターで実行するときに機能しない可能性Microsoft Teams。

ボットはボット エミュレーター内で実行できます。 これにより、ボットのコア ロジックの一部をテストし、メッセージの大まかなレイアウトを確認し、簡単なテストを実行できます。 手順は次のとおりです。

1. コードをローカルで実行します。
2. ボット エミュレーターを起動し、URL を設定します。
   * Node.js: `http://localhost:3978/api/messages`
   * .NET/C#: `http://localhost:3979/api/messages`
3. 既定の環境変数と一致するには、Microsoft アプリ ID と Microsoft アプリのパスワードを空白のままにします。

## <a name="locally-hosted"></a>ローカルでホストされる

Microsoft Teams完全にクラウドベースの製品である場合、アクセスするサービスはすべて HTTPS エンドポイントを使用して一般公開する必要があります。 したがって、アプリが Teams 内で動作するには、コードを選択したクラウドに発行するか、ローカル実行中のインスタンスに外部からアクセス可能にする必要があります。 トンネリング ソフトウェアを使用して後者を実行できます。

任意のツールを使用することもできますが、コンピューター上でローカルで開くポートの外部アドレス指定可能な URL を作成する [ngrok](https://ngrok.com/download)を使用して推奨します。 

**アプリをローカルで実行する準備として ngrok をMicrosoft Teamsするには**

1. ターミナル アプリケーションにインストールされているディレクトリngrok.exe移動します。 この手順を回避するために、パス変数として追加できます。
2. たとえば、ポート番号を `ngrok http 3978 --host-header=localhost:3978` 必要に応じて実行するか、置換します。
   これにより、指定したポートのリストに ngrok が起動します。 その代り、ngrok が実行されている限り、外部でアドレス指定可能な URL が有効になります。

> [!NOTE]
> ngrok を停止して再起動すると、URL が変更されます。

使用している機能に基づいてプロジェクトで ngrok を使用するには、この URL エンドポイントを使用するには、コード、構成、および manifest.json ファイル内のすべての URL 参照を置き換える必要があります。

サーバーに登録されているボットMicrosoft Bot Framework、ボットのメッセージング エンドポイントを更新して、この新しい ngrok エンドポイントを使用します。 たとえば、「 `https://2d1224fb.ngrok.io/api/messages` 」のように入力します。 ボット フレームワーク ポータルの [テスト チャット] ウィンドウでボット応答をテストすることで、ngrok が動作しているのを検証できます。 繰り返しますが、エミュレーターと同様に、このテストでは、ユーザーが特定のTeamsにアクセスできません。

> [!NOTE]
> ボットのメッセージング エンドポイントを更新するには、ボット フレームワークを使用する必要があります。 ボット フレームワークのボット [の一覧でボットを選択します](https://dev.botframework.com/bots)。 ボットをユーザーに移行する必要Microsoft Azure。 また、App Studio を使用してメッセージング エンドポイント [を更新することもできます](~/concepts/build-and-test/app-studio-overview.md)。

## <a name="cloud-hosted"></a>クラウド ホスト型

外部アドレス指定可能なサービスを使用して、開発および実稼働コードとその HTTPS エンドポイントをホストできます。 機能が同じサービスに存在する期待はありません。 すべてのドメインに、ファイル内のオブジェクトにMicrosoft Teamsアプリからアクセス [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) する必要 `manifest.json` があります。

> [!NOTE]
> 安全な環境を確保するには、参照する正確なドメインとサブドメインについて明示的に説明し、それらのドメインを制御する必要があります。 たとえば、お `*.azurewebsites.net` 勧めできませんが、 `contoso.azurewebsites.net` お勧めします。

## <a name="load-and-run-your-experience"></a>エクスペリエンスの読み込みと実行

アプリ内でエクスペリエンスを読み込Microsoft Teamsするには、パッケージを作成し、パッケージをアプリにアップロードTeams。 詳細については、以下を参照してください。

* [アプリのパッケージをMicrosoft Teamsします](~/concepts/build-and-test/apps-package.md)。
* [アップロードでアプリをMicrosoft Teams。](~/concepts/deploy-and-publish/apps-upload.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"] 
> [テスト データを環境に追加する](~/concepts/build-and-test/test-data.md)

