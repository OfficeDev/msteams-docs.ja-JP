---
title: アプリをテストおよびデバッグするためのセットアップの選択
description: Microsoft Teams アプリのテストとデバッグのオプションについて説明します。
keywords: チームはデバッグアプリを実行します
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 1f11834ad83e8bea7e4114d25d022df2f62c1700
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565159"
---
# <a name="choose-a-setup-to-test-and-debug-your-microsoft-teams-app"></a>Microsoft Teams アプリをテストおよびデバッグするためのセットアップを選択する

Microsoft Teamsアプリには 1 つ以上の機能が含まれ、アプリを実行する方法やホストする方法も異なります。 デバッグには、次のいずれかの方法を使用します。

* **純粋にローカル**: ボットの場合は、ボットエミュレータで体験をテストできます。 その他のコンテンツについては、ブラウザでローカルに実行し、コンテンツをアドレス指定するには `http://localhost` 、 を使用します。
* **ローカルでホストされているTeams**: トンネリング ソフトウェアでローカルにアプリを実行し、Teamsに [アップロード](~/concepts/deploy-and-publish/apps-upload.md)する [パッケージを作成](~/concepts/build-and-test/apps-package.md)します。 これにより、Teams クライアント内でアプリを簡単に実行およびデバッグできます。
* **Teamsでクラウドホスト**: これは、Teams アプリの実稼働レベルのサポートを実際にシミュレートします。 ソリューションを外部からアクセス可能なサーバーまたはクラウド プロバイダーにアップロードし、Teamsに[アップロード](~/concepts/deploy-and-publish/apps-upload.md)する[パッケージを作成](~/concepts/build-and-test/apps-package.md)します。

ローカルまたはローカルのテストを行う場合は、自分のコンピュータからエクスペリエンスを実行Teams。 これにより、統合開発環境内でコンパイルおよび実行し、ブレークポイントやステップ デバッグなどの手法を最大限に活用できます。 

> [!NOTE]
> 運用環境規模のデバッグとテストでは、独自の会社のガイドラインに従って、独自のプロセスを通じてテスト、ステージング、および展開をサポートできることを確認することをお勧めします。

複数のマニフェストとパッケージを使用して、運用サービスと開発サービスの分離を維持します。 たとえば、開発ボットと運用ボットを個別に登録し、適切なパッケージを作成して、テスト環境にアップロードすることができます。 また、アプリストアでの公開や顧客への配布のためにアプリを提出する前に、本番パッケージをアップロードしてテストすることをお勧めします。

## <a name="purely-local"></a>純粋にローカル

> [!NOTE]
> ボットをローカルで実行しても、Teamsアプリ機能や、名簿呼び出しやその他のチャネル固有の機能などのTeams固有のボット機能にはアクセスできません。 さらに、Microsoft Teamsで実行すると機能しない可能性がある Bot エミュレーターの Bot フレームワークで許可される機能もあります。

ボットはボット エミュレータ内で実行できます。 これにより、ボットのコア ロジックの一部をテストし、メッセージの大まかなレイアウトを確認し、簡単なテストを実行できます。 以下の手順を実行します。

1. コードをローカルで実行します。
2. ボット エミュレーターを起動し、URL を設定します。
   * Node.js: `http://localhost:3978/api/messages`
   * .NET/C#: `http://localhost:3979/api/messages`
3. 既定の環境変数と一致するように、Microsoft アプリ ID と Microsoft アプリ パスワードを空白のままにします。

## <a name="locally-hosted"></a>ローカルでホスト

Microsoft Teams完全にクラウドベースの製品であり、アクセスするすべてのサービスが HTTPS エンドポイントを使用してパブリックに利用できる必要があります。 したがって、アプリをTeams内で動作させるには、選択したクラウドにコードを発行するか、ローカルで実行しているインスタンスを外部からアクセスできるようにする必要があります。 私たちは、トンネリングソフトウェアで後者を行うことができます。

任意のツールを使用できますが、使用するポートの外部アドレス指定可能な URL を作成する [ngrok](https://ngrok.com/download)を使用し、お勧めします。 

**Microsoft Teams アプリをローカルで実行する準備として ngrok をセットアップするには**

1. ターミナル アプリケーションにインストールngrok.exeディレクトリに移動します。 この手順を回避するために、パス変数として追加することもできます。
2. たとえば、 `ngrok http 3978 --host-header=localhost:3978` を実行するか、必要に応じてポート番号を置き換えます。
   これにより、指定したポートに表示される ngrok が起動します。 その代わりに、ngrok が実行されている間有効な外部アドレス指定可能な URL が提供されます。

> [!NOTE]
> ngrok を停止して再起動すると、URL が変更されます。

使用している機能に基づいてプロジェクトで ngrok を使用するには、この URL エンドポイントを使用するために、コード、構成、およびファイルのmanifest.js内のすべての URL 参照を置き換える必要があります。

Microsoft Bot Frameworkに登録されているボットの場合は、この新しい ngrok エンドポイントを使用するようにボットのメッセージング エンドポイントを更新します。 たとえば、「 `https://2d1224fb.ngrok.io/api/messages` 」のように入力します。 ボットの応答を Bot Framework ポータルの [テスト チャット] ウィンドウでテストすることで、ngrok が動作していることを検証できます。 この場合も、エミュレーターと同様に、このテストではTeams固有の機能にアクセスすることはできません。

> [!NOTE]
> ボットのメッセージング エンドポイントを更新するには、Bot Framework を使用する必要があります。 ボット フレームワーク の [ボットのリストでボットを](https://dev.botframework.com/bots)選択します。 ボットをMicrosoft Azureに移行する必要はありません。 [また、App Studio](~/concepts/build-and-test/app-studio-overview.md)を使用してメッセージング エンドポイントを更新することもできます。

## <a name="cloud-hosted"></a>クラウド ホスト型

外部でアドレス指定可能なサービスを使用して、開発コードと実稼働コード、および HTTPS エンドポイントをホストできます。 機能が同じサービスに存在するとは期待されません。 ファイル内のオブジェクトにリストされているMicrosoft Teamsアプリからすべてのドメインにアクセス [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) する必要 `manifest.json` があります。

> [!NOTE]
> セキュリティで保護された環境を確保するには、参照する正確なドメインとサブドメインについて明確にし、それらのドメインを制御する必要があります。 たとえば、 `*.azurewebsites.net` お勧 `contoso.azurewebsites.net` めできません。

## <a name="load-and-run-your-experience"></a>エクスペリエンスを読み込んで実行する

Microsoft Teams内でエクスペリエンスを読み込んで実行するには、パッケージを作成してTeamsにアップロードする必要があります。 詳細については、以下を参照してください。

* [Microsoft Teams アプリのパッケージを作成します](~/concepts/build-and-test/apps-package.md)。
* [アプリを Microsoft Teams でアップロード](~/concepts/deploy-and-publish/apps-upload.md)します。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"] 
> [テスト データを環境に追加する](~/concepts/build-and-test/test-data.md)

