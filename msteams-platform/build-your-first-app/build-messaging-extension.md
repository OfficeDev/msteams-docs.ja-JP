---
title: まず、メッセージング拡張機能を構築する
author: heath-hamilton
description: Microsoft Teams ツールキットを使用して、Microsoft Teams メッセージング拡張機能をすばやく作成できます。
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
ms.openlocfilehash: b19856eacee866ebbc89f21ac12575f1392918b3
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452835"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a>Microsoft Teams のメッセージング拡張機能を構築する

Teams *メッセージング拡張機能*には、 [検索コマンド](../messaging-extensions/how-to/search-commands/define-search-command.md) と [アクションコマンド](../messaging-extensions/how-to/action-commands/define-action-command.md)の2種類があります。

このレッスンでは、 *検索コマンド* ( *検索ベースのメッセージング拡張機能*とも呼ばれます) を作成します。これは、外部コンテンツを検索して Teams で共有するためのショートカットです。 ユーザーは、[ [Teams の作成] または [コマンド] ボックス](../messaging-extensions/what-are-messaging-extensions.md)から検索コマンドにアクセスできます。

## <a name="your-assignment"></a>自分の割り当て

組織のヘルプデスクは Teams を通じてユーザーと通信しますが、チケットは別のシステムに存在します。 これは、サポートスタッフが常にアプリ間を行き来する必要があることを意味します。 Teams の簡単な検索ベースのメッセージング拡張機能を作成することによって、この大幅な切り替えを減らす方法を調査します。

## <a name="what-youll-learn"></a>学習内容

> [!div class="checklist"]
>
> * Microsoft Teams Toolkit for Visual Studio Code を使用して、アプリプロジェクトとメッセージング拡張機能を作成する
> * メッセージング拡張機能に関連するアプリマニフェストのプロパティと一部のスキャフォールディングを特定する
> * アプリをローカルでホストする
> * メッセージング拡張機能の bot を構成する
> * Teams でメッセージング拡張機能をサイドロードおよびテストする

## <a name="before-you-begin"></a>はじめに

まだお持ちでない場合は、 [Teams 開発の前提条件を理解し、インストール](build-first-app-overview.md#get-prerequisites)してください。

## <a name="1-create-your-app-project"></a>1. アプリプロジェクトを作成します。

Microsoft Teams Toolkit は、メッセージング拡張機能に次のコンポーネントをセットアップするのに役に立ちます。

* メッセージング拡張機能に関連する**アプリマニフェストとスキャフォールディング**
* Microsoft Azure Bot サービスに自動的に登録されるメッセージング拡張機能の**Bot**

> [!TIP]
> 以前に Teams アプリプロジェクトを作成していない場合は、 [以下の手順](../build-your-first-app/build-and-run.md) に従って、プロジェクトについて詳しく説明することをお勧めします。

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft teams** ] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し、[ **新しい teams アプリの作成**] を選択します。
1. Teams アプリの名前を入力します。 (これは、アプリの既定の名前であり、ローカルコンピューター上のアプリプロジェクトディレクトリの名前でもあります。)
1. [ **機能の追加** ] 画面で、[ **メッセージング内線番号** ] を選択し、[ **次へ**] をクリックします。
1. [ **メッセージング拡張機能の構成** ] 画面で、次の操作を行います。
    1. メッセージング拡張機能の種類に対して **検索ベース** のオプションのみを選択します。
    1. [ **新しい Bot を作成** し、 **ログイン** する] を選択して、Microsoft 365 開発アカウントでサインインします。
    1. Bot ID とパスワードを保存します (これは後で必要になります)。
    1. オプションBot のカスタム名を入力し、[ **作成**] を選択します。 (これは、既に指定した Teams アプリの名前ではありません)。
    1. ここでは、リンク unfurling オプションに [ **いいえ** ] を選択します。</br>
:::image type="content" source="../assets/images/build-your-first-app/choose-me-search.png" alt-text="Teams ツールキットで、メッセージング拡張機能のために新しい bot を作成するために Microsoft 365 アカウントにログインする方法を示す図。":::
1. 画面の下部にある [ **完了** ] を選択して、プロジェクトを構成します。

## <a name="2-identify-relevant-app-project-components"></a>2. 関連するアプリプロジェクトコンポーネントを特定する

Teams ツールキットを使用してプロジェクトを作成すると、アプリマニフェストとスキャフォールディングの多くが自動的に設定されます。

### <a name="app-manifest"></a>アプリマニフェスト

アプリケーションマニフェスト ( `manifest.json` プロジェクトのディレクトリ内のファイル) の次のスニペットは、 `.publish` メッセージング拡張機能に関連するプロパティと既定値を示しています。

```JSON
"composeExtensions": [
    {
        "botId": "{botId0}",
        "canUpdateConfiguration": true,
        "commands": [
            {
                "id": "searchQuery",
                "context": [
                    "compose",
                    "commandBox"
                ],
                "description": "Test command to run query",
                "title": "Search",
                "type": "query",
                "parameters": [
                    {
                        "name": "searchQuery",
                        "title": "Search Query",
                        "description": "Your search query",
                        "inputType": "text"
                    }
                ]
            }
        ]
    }
],
```

ツールキットによって作成されたプロパティのいくつかを理解してみましょう。 (サポートされているプロパティの完全な一覧を参照してください [`composeExtensions`](../resources/schema/manifest-schema.md#composeextensions) )。

* `botId`: 作成した bot の ID。プロジェクトを設定します。 (に保存されている場合は、の `{botId0}` 実際の ID を検索でき `Development.env` ます)。
* `commands`: メッセージング拡張機能で使用可能なコマンド。 ツールキットには、検索コマンドのためのスキャフォールディングが用意されていました。
* `context`: ユーザーがメッセージング拡張機能を呼び出すことができます。 この場合は、Teams の作成またはコマンドボックスからメッセージング拡張機能を起動できます。
* `description`: UI ヘルプテキストコマンドの機能または使用方法を示します。
* `parameters`: コマンドが受け付けるすべてのパラメーターが含まれています (少なくとも1つは必要です。最大5個を持つことができます)。
* `parameters.description`: パラメーターの目的または入力例を説明する UI ヘルプテキスト。

### <a name="app-scaffolding"></a>アプリのスキャフォールディング

アプリのスキャフォールディングには、 `.env` プロジェクトのルートディレクトリにあるファイルが含まれています。このファイルには、メッセージング拡張機能の bot の ID とパスワードが格納されています。

また、ルートディレクトリには、 `botActivityHandler.js` メッセージング拡張機能 (または、技術的には [メッセージング拡張機能](#4-configure-the-bot-for-your-messaging-extension)) が Teams の検索クエリに応答する方法を処理するためのファイルがあります。

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. アプリへのセキュリティで保護されたトンネルをセットアップする

テストを目的として、ローカル web サーバーでメッセージング拡張機能をホストします (ポート 3978)。

1. ターミナルで、を実行 `ngrok http -host-header=rewrite 3978` します。
1. Teams で HTTPS 接続が必要なため、出力に HTTPS URL をコピーします。
1. ディレクトリで `.publish` 、を開き `Development.env` ます。
1. 値を `baseUrl0` コピーした URL に置き換えます。 (たとえば、 `baseUrl0=http://localhost:3000` をに変更 `baseUrl0=https://85528b2b3ca5.ngrok.io` します)。

アプリのマニフェストは、メッセージング拡張機能によって使用される bot をホストしている場所を指しています。

## <a name="4-configure-the-bot-for-your-messaging-extension"></a>4. メッセージング拡張機能の bot を構成する

メッセージング拡張機能は、ボットに依存して、チームからのユーザー要求をホストされたサービスに送信して処理します。

ボットは、Teams ツールキットを使用してアプリをセットアップするときに実行された Azure Bot サービスに登録されている必要があります。

### <a name="specify-your-bot-id-and-password"></a>Bot ID とパスワードを指定する

Bot が Azure Bot サービスに登録されると、Teams アプリが知っておく必要がある ID とパスワードが割り当てられます。

1. ツールキットのセットアップ時に保存した bot ID とパスワードを見つけます。
1. ルートディレクトリで、ファイルを開き `.env` ます。
1. Bot ID とパスワードを `BotId` それぞれおよびプロパティに設定し `BotPassword` ます。

### <a name="add-the-bot-endpoint-address"></a>Bot エンドポイントアドレスを追加する

メッセージング拡張機能で検索クエリを受信して処理するには、ボットエンドポイントの URL を指定する必要があります。 通常、URL はのように `https://HOST_URL/api/messages` なります。 これは Teams ツールキットですばやく構成できます。

1. Visual Studio Code で、左側のアクティビティバーで [ **Microsoft teams** ] を選択し、 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: [ **microsoft Teams ツールキットを開く**] を選択します。
1. [ **ボット management > 既存の bot 登録** ] に移動し、セットアップ時に作成した bot を選択します。
1. **Bot エンドポイントアドレス**フィールドに、bot (値) をホストしているローカル web サーバーを入力 `baseUrl10` し、 `/api/messages` それに追加します。

Bot は、メッセージング拡張機能でクエリを処理できるようになります。

## <a name="5-run-your-app"></a>5. アプリを実行する

メッセージング拡張機能をホストする URL を設定し、検索を処理するように構成します。 アプリを起動して実行します。

1. ターミナルで、アプリプロジェクトのルートディレクトリに移動し、を実行 `npm install` します。
1. `npm start` を実行します。

成功した場合、次のメッセージが表示されます。メッセージング拡張サービスが自分のアクティビティをリッスンしていることを示し `localhost` ます。

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a>サイドロード Teams でのメッセージング拡張機能の作成

メッセージング拡張機能が実行されている状態で、Teams にインストールできます。

> [!TIP]
> 以前に Teams アプリをサイドロードしていない場合は、以下の [手順](../build-your-first-app/build-and-run.md#5-sideload-your-app-in-teams)を実行します。

1. アプリのサイドロードを許可するアカウントを使用して、Teams クライアントにログインします。
1. [ **アプリ**] を選択し、[ **カスタムアプリのアップロード**] を選択します。
1. アプリプロジェクトフォルダーに移動し `.publish` 、を選択し `Development.zip` ます。
1. [モーダルのインストール] で、[ **追加** ] を選択してアプリをインストールします。

## <a name="7-test-your-messaging-extension"></a>7. メッセージング拡張機能をテストする

Teams チャットでのメッセージング拡張機能のしくみについて説明します。

1. 新しいチャットを開始します。 [新規作成] ボックスで、[ **その他**] を選択し、 :::image type="icon" source="../assets/icons/teams-client-more.png"::: サイドロードしたばかりのメッセージング拡張アプリを選択します。<br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-access.png" alt-text="Teams ツールキットで、メッセージング拡張機能のために新しい bot を作成するために Microsoft 365 アカウントにログインする方法を示す図。":::
1. 何らかの検索を試してみてください (たとえば、「チケット」)。 アプリが動作している場合は、サンプルの検索結果が表示されます (後で自分で追加することができます)。<br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Teams ツールキットで、メッセージング拡張機能のために新しい bot を作成するために Microsoft 365 アカウントにログインする方法を示す図。":::

## <a name="well-done"></a>よくやりましたね

おめでとうございます! [作成] または [コマンド] ボックスで外部コンテンツを検索するように設定されている基本的な Teams メッセージング拡張機能があります。

## <a name="next-steps"></a>次の手順

次のページを参照して続行し、完全な機能を備えたメッセージング拡張機能を構築します。

1. サービスに関連する[検索コマンドを定義](../messaging-extensions/how-to/search-commands/define-search-command.md)します。
1. [ユーザーの検索に応答](../messaging-extensions/how-to/search-commands/respond-to-search.md)するようにサービスを構成します。

## <a name="troubleshooting"></a>トラブルシューティング

このチュートリアルを完了する際に問題が発生した場合は、次の情報が役立ちます。

### <a name="toolkit-setup-fails"></a>ツールキットのセットアップが失敗する

Teams ツールキットを使用してアプリプロジェクトをセットアップするときに、[ **新しい Bot を作成** する] オプションを選択し、Microsoft 365 開発アカウントでログインすると、エラーが発生します。

これは認証の問題である可能性があります。 プロジェクトの設定を完了するには、次の手順を実行します。

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft Teams** ] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し、[ **サインアウト**] を選択します。
1. 同じアカウントを使用してログインし、新しい bot を作成することにより、セットアッププロセスを再度実行します。

### <a name="bot-isnt-connected-to-teams"></a>Bot が Teams に接続されていない

アプリをインストールしたが動作していない場合は、メッセージング拡張機能の bot が[Azure Bot サービスの Teams*チャネル*に接続](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)されていることを確認してください。

これは Teams のチャネルと同じではないことを理解しておくことが重要です。 この場合、チャネルは、Azure Bot サービスが Bot を Teams または他の [サポートされている Microsoft またはサードパーティの通信アプリ](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)に接続する方法を示しています。

## <a name="learn-more"></a>詳細情報

* [Link unfurling フィーチャーを含める](../messaging-extensions/how-to/link-unfurling.md)
* [認証を追加する](../messaging-extensions/how-to/add-authentication.md)
* [アクションベースのメッセージング拡張機能を作成する](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [Microsoft Bot フレームワーク](https://dev.botframework.com/)
