---
title: 作業の開始-bot をビルドする
author: heath-hamilton
description: Microsoft Teams ツールキットを使用して、Microsoft Teams bot をすばやく作成できます。
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: 78fe535137864a72dcacf20857572599a7c2409a
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452793"
---
# <a name="build-a-bot-for-microsoft-teams"></a>Microsoft Teams の bot を構築する

このチュートリアルでは、基本的な *bot* アプリを構築します。 Bot は Teams ユーザーと web サービス間の仲介者として機能します。 ユーザーは bot とチャットして、サービスによって実行された情報をすばやく取得したり、ワークフローやタスクを開始したりできます。

## <a name="your-assignment"></a>自分の割り当て

職場では、チーム内で重要な連絡先情報を表示するための [タブ](../build-your-first-app/build-personal-tab.md) を使用しています。 たとえば、仕事仲間は、ヘルプデスクの電話番号にすばやくアクセスできます。 しかし、通話の代わりに、ユーザーが chatbot を使用してヘルプデスクに連絡することができた場合はどうなりますか。 上司からは、Teams での基本的な会話をすばやく実行する方法を確認するように求められています。

## <a name="what-youll-learn"></a>学習内容

> [!div class="checklist"]
>
> * Microsoft Teams Toolkit for Visual Studio Code を使用してアプリプロジェクトとボットを作成する
> * Bot に関連するアプリマニフェストのプロパティとスキャフォールディングの一部を特定する
> * アプリをローカルでホストする
> * Teams の bot を構成する
> * Teams でボットをサイドロードおよびテストする

## <a name="before-you-begin"></a>はじめに

まだお持ちでない場合は、 [Teams 開発の前提条件を理解し、インストール](build-first-app-overview.md#get-prerequisites)してください。

## <a name="1-create-your-app-project"></a>1. アプリプロジェクトを作成します。

Microsoft Teams Toolkit は、アプリ用に次のコンポーネントをセットアップするのに役に立ちます。

* **アプリケーションマニフェストと** bot に関連するスキャフォールディング
* Microsoft Azure Bot サービスに自動的に登録された**Bot**

> [!TIP]
> 以前に Teams アプリプロジェクトを作成していない場合は、 [以下の手順](../build-your-first-app/build-and-run.md) に従って、プロジェクトについて詳しく説明することをお勧めします。

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft teams** ] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し、[ **新しい teams アプリの作成**] を選択します。
1. Teams アプリの名前を入力します。 (これは、アプリの既定の名前であり、ローカルコンピューター上のアプリプロジェクトディレクトリの名前でもあります。)
1. [ **機能の追加** ] 画面で、[ **Bot** ] を選択し、[ **次へ**] を選択します。
1. [ **新しい Bot を作成** し、 **ログイン** する] を選択して、Microsoft 365 開発アカウントでサインインします。<br/>
:::image type="content" source="../assets/images/build-your-first-app/vsc-create-bot.png" alt-text="Teams ツールキットで、Microsoft 365 アカウントにログインして新しい bot を作成する方法を示す図。":::
1. Bot ID とパスワードを保存します (これは後で必要になります)。
1. オプションBot のカスタム名を入力し、[ **作成**] を選択します。 (これは bot の名前であり、既に指定した Teams アプリの名前ではないことに注意してください)。
1. 画面の下部にある [ **完了** ] を選択して、プロジェクトを構成します。

## <a name="2-identify-relevant-app-project-components"></a>2. 関連するアプリプロジェクトコンポーネントを特定する

Teams ツールキットを使用してプロジェクトを作成すると、アプリマニフェストとスキャフォールディングの多くが自動的に設定されます。 Bot を構築するための主なコンポーネントを見てみましょう。

### <a name="app-manifest"></a>アプリマニフェスト

アプリマニフェスト ( `manifest.json` プロジェクトのディレクトリ内のファイル) の次のスニペットは、 `.publish` bot に関連するプロパティと既定値を示しています。

```JSON
"bots": [
    {
        "botId": "{botId0}",
        "scopes": [
            "personal",
            "groupchat",
            "team"
        ],
        "supportsFiles": false,
        "isNotificationOnly": false,
        "commandLists": [
            {
                "scopes": [
                    "personal",
                    "groupchat",
                    "team"
                ],
                "commands": [
                    {
                        "title": "Hello",
                        "description": "Sends a hello message and @mention the sender"
                    }
                ]
            }
        ]
    }
],
```

ここでは、次の必須プロパティに焦点を絞って説明します。 (サポートされているプロパティの完全な一覧を参照してください [`bots`](../resources/schema/manifest-schema.md#bots) )。

* `botId`: 作成した bot の ID。プロジェクトを設定します。 (に保存されている場合は、の `{botId0}` 実際の ID を検索でき `Development.env` ます)。
* `scopes`: Bot が `personal` 、、 `groupchat` または `team` (つまりチャネル) コンテキストで使用可能かどうかを指定します。
* `commands`: 使用可能なコマンドは、ユーザーが bot に送信できます。
* `title`: Teams クライアントに表示される Bot コマンド名。
* `description`: ユーザーが bot コマンドの機能を理解するのに役立つ構文および引数の簡単な説明または例。

### <a name="app-scaffolding"></a>アプリのスキャフォールディング

アプリのスキャフォールディングは、 `botActivityHandler.js` ボットが Teams でのアクティビティを処理する方法について、プロジェクトのルートディレクトリにあるファイルを提供します (たとえば、"Hello" のような特定のメッセージに bot が応答する方法)。

このファイルには、 `.env` ルートディレクトリにも BOT ID とパスワードが保存されます。

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. アプリへのセキュリティで保護されたトンネルをセットアップする

テストを目的として、ボットをローカル web サーバー (ポート 3978) にホストしてみましょう。

1. ターミナルで、を実行 `ngrok http -host-header=rewrite 3978` します。
1. Teams で HTTPS 接続が必要なため、出力に HTTPS URL をコピーします。
1. ディレクトリで `.publish` 、を開き `Development.env` ます。
1. 値を `baseUrl0` コピーした URL に置き換えます。 (たとえば、 `baseUrl0=http://localhost:3000` をに変更 `baseUrl0=https://85528b2b3ca5.ngrok.io` します)。

アプリのマニフェストが bot をホストしている場所を指しています。

## <a name="4-configure-your-bot"></a>4. bot を構成する

Teams でボットを使用するには、その bot を Azure Bot サービスに登録する必要があります。 さいわい、Teams ツールキットを使用してアプリをセットアップすると、これは自動的に実行されます。

### <a name="specify-your-bot-id-and-password"></a>Bot ID とパスワードを指定する

Bot が Azure Bot サービスに登録されると、Teams アプリが知っておく必要がある ID とパスワードが割り当てられます。

1. ツールキットのセットアップ時に保存した bot ID とパスワードを見つけます。
1. ルートディレクトリで、ファイルを開き `.env` ます。
1. Bot ID とパスワードをそれぞれにに追加し `BotId` `BotPassword` ます。

### <a name="add-the-bot-endpoint-address"></a>Bot エンドポイントアドレスを追加する

Bot に送信されるユーザーメッセージ (つまり、要求) を受信して処理するためのエンドポイント URL を指定する必要があります。 通常、URL はのように `https://HOST_URL/api/messages` なります。 これは Teams ツールキットですばやく構成できます。

1. Visual Studio Code で、左側のアクティビティバーで [ **Microsoft teams** ] を選択し、 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: [ **microsoft Teams ツールキットを開く**] を選択します。
1. [ **ボット management > 既存の bot 登録** ] に移動し、セットアップ時に作成した bot を選択します。
1. **Bot エンドポイントアドレス**フィールドに、bot (値) をホストしているローカル web サーバーを入力 `baseUrl10` し、 `/api/messages` それに追加します。

    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Teams ツールキットで、Microsoft 365 アカウントにログインして新しい bot を作成する方法を示す図。":::

Bot は Teams のメッセージに応答できるようになります。

## <a name="5-run-your-app"></a>5. アプリを実行する

Bot をホストする URL を設定し、メッセージを処理するように構成します。 その後、自分の bot を起動して実行します。

1. ターミナルで、アプリプロジェクトのルートディレクトリに移動し、を実行 `npm install` します。
1. `npm start` を実行します。

成功した場合、ボットが自分のアクティビティをリッスンしていることを示す次のようなメッセージが表示され `localhost` ます。

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a>6 Teams での bot のサイドロード

Bot を実行している場合は、Teams にインストールできます。

> [!TIP]
> 以前に Teams アプリをサイドロードしていない場合は、以下の [手順](../build-your-first-app/build-and-run.md#5-sideload-your-app-in-teams)を実行します。

1. アプリのサイドロードを許可するアカウントを使用して、Teams クライアントにログインします。
1. [ **アプリ**] を選択し、[ **カスタムアプリのアップロード**] を選択します。
1. アプリプロジェクトフォルダーに移動し `.publish` 、を選択し `Development.zip` ます。
1. [モーダルのインストール] で、[ **追加** ] を選択してアプリをインストールします。

## <a name="7-test-your-bot"></a>7. bot をテストする

おもしろい部分のために、1対1のチャットで bot に "Hello" と言うことができます。

1. Teams で、左側にある [ **その他**] を選択し :::image type="icon" source="../assets/icons/teams-client-more.png"::: ます。
1. サイドロードの bot を見つけて選択します。<br/>
   :::image type="content" source="../assets/images/build-your-first-app/bot-teams-access.png" alt-text="Teams ツールキットで、Microsoft 365 アカウントにログインして新しい bot を作成する方法を示す図。":::
1. [新規作成] ボックスで、 `Hello` メッセージを送信します。

Bot は次のようなメッセージに返信します。

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="Teams ツールキットで、Microsoft 365 アカウントにログインして新しい bot を作成する方法を示す図。":::

## <a name="well-done"></a>よくやりましたね

おめでとうございます! ユーザーが1対1で、またはグループ設定 (チャネルとチャット) で通信できる基本的な Teams bot があります。

## <a name="troubleshooting"></a>トラブルシューティング

このチュートリアルを完了する際に問題が発生した場合は、次の情報が役立ちます。

### <a name="toolkit-setup-fails"></a>ツールキットのセットアップが失敗する

Teams ツールキットを使用してアプリプロジェクトをセットアップするときに、[ **新しい Bot を作成** する] オプションを選択し、Microsoft 365 開発アカウントでログインすると、エラーが発生します。

これは認証の問題である可能性があります。 プロジェクトの設定を完了するには、次の手順を実行します。

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft Teams** ] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し、[ **サインアウト**] を選択します。
1. 同じアカウントを使用してログインし、新しい bot を作成することにより、セットアッププロセスを再度実行します。

### <a name="bot-isnt-connected-to-teams"></a>Bot が Teams に接続されていない

アプリをインストールしたが、bot が動作していない場合は、ボットが[Azure Bot サービスの Teams*チャネル*に接続](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)されていることを確認してください。

これは Teams のチャネルと同じではないことを理解しておくことが重要です。 この場合、チャネルは、Azure Bot サービスが Bot を Teams または他の [サポートされている Microsoft またはサードパーティの通信アプリ](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)に接続する方法を示しています。

## <a name="learn-more"></a>詳細情報

* [サンプルのいずれかで、他の Teams のボットができることを確認する](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [ボット会話の基本](../bots/how-to/conversations/conversation-basics.md)
* [Teams での Bot 認証](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft Bot フレームワーク](https://dev.botframework.com/)
* [ツールキットなしでボットを作成する](../bots/how-to/create-a-bot-for-teams.md)
