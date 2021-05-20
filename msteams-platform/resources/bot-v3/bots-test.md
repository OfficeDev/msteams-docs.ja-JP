---
title: ボットのテストとデバッグ
description: Microsoft Teamsでボットをテストする方法について説明します。
keywords: チームボットテスト
ms.topic: how-to
localization_priority: Normal
ms.date: 03/20/2019
ms.openlocfilehash: 269b0680e45d764cf4cb0269c40d3d202145edb8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566461"
---
# <a name="test-and-debug-your-microsoft-teams-bot"></a>Microsoft Teamsボットのテストとデバッグ

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

ボットをテストする場合は、ボットを実行するコンテキストと、Microsoft Teamsに固有のデータを必要とするボットに追加した機能の両方を考慮する必要があります。 ボットのテストに選択したメソッドが、その機能に合っていることを確認します。

## <a name="test-by-uploading-to-teams"></a>Teamsにアップロードしてテストする

ボットをテストする最も包括的な方法は、アプリ パッケージを作成してTeamsにアップロードすることです。 これは、すべてのスコープでボットが利用できる機能をすべてテストする唯一の方法です。

アプリをアップロードするには、2 つの方法があります。 [App Studio](~/concepts/build-and-test/app-studio-overview.md)を使用して支援するか、[またはアプリ パッケージを](~/concepts/build-and-test/apps-package.md)手動で作成して[アプリをアップロード](~/concepts/deploy-and-publish/apps-upload.md)することができます。 マニフェストを変更してアプリを再アップロードする必要がある場合は、変更したアプリ パッケージをアップロードする前に [ボットを削除](#deleting-a-bot-from-teams) する必要があります。

## <a name="debug-your-bot-locally"></a>ボットをローカルでデバッグする

開発中にボットをローカルでホストしている場合は、ボットをテストするために [ngrok](https://ngrok.com/) のようなトンネリング サービスを使用する必要があります。 ngrok をダウンロードしてインストールしたら、以下のコマンドを実行してトンネリング サービスを開始します。 パスに ngrok を追加する必要がある場合があります。

```bash
ngrok http <port> -host-header=localhost:<port>
```

ngrok が提供する https エンドポイントをアプリ マニフェストで使用します。 コマンド ウィンドウを閉じて再起動すると、新しい URL が取得され、ボット エンドポイントのアドレスも更新してその URL を使用する必要があります。

## <a name="testing-your-bot-without-uploading-to-teams"></a>Teamsにアップロードせずにボットをテストする

場合によっては、Teamsでアプリとしてインストールせずにボットをテストする必要があります。 以下に、2 つの方法を提供します。 ボットをアプリとしてインストールせずにボットをテストすると、ボットが利用可能で応答できることを確認できますが、ボットに追加した可能性のあるMicrosoft Teams機能の幅を完全にテストすることはできません。 ボットを完全にテストする必要がある場合は、 [をアップロードしてテスト](#test-by-uploading-to-teams)の手順に従ってください。

### <a name="use-the-bot-emulator"></a>ボット エミュレーターを使用する

Bot Framework Emulatorは、ボット開発者が、ローカルまたはリモートでボットをテストおよびデバッグできるようにするデスクトップ アプリケーションです。 エミュレーターを使用して、ボットとチャットしたり、ボットが送受信するメッセージを調べることができます。 これは、ボットが利用可能で応答していることを確認するのに便利ですが、エミュレーターでは、ボットに追加したTeams固有の機能をテストしたり、ボットからの応答をTeamsでどのようにレンダリングするかを正確に視覚的に表現することはできません。 これらのいずれかのことをテストする必要がある場合は、 [ボットをアップロードすることをお勧めします](#test-by-uploading-to-teams)。

Bot Framework Emulatorの詳細な手順はこちらからご[覧いただけます](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)。

### <a name="talk-to-your-bot-directly-by-id"></a>ID で直接ボットに問い合わせてください

>[!Important]
>Id によってボットとの会話は、テスト目的でのみ使用されます。

また、Id を使用してボットとの会話を開始することもできます。これを行うための2つの方法を以下に示します。 これらの方法のいずれかを通じてボットが追加された場合、チャネルの会話ではアドレス指定が可能ではなく、タブやメッセージング拡張機能などの他のMicrosoft Teamsアプリ機能を利用することはできません。

1. ボットの [[Bot ダッシュボード](https://dev.botframework.com/bots)] ページの **[チャネル**] で **、[Microsoft Teamsに追加]** を選択します。 Microsoft Teamsは、あなたのボットとの個人的なチャットで起動します。
2. Microsoft Teams内からボットのアプリ ID を直接参照します。
   * ボットの [ [ボット ダッシュボード](https://dev.botframework.com/bots) ] ページの **[詳細]** で、ボットの **Microsoft アプリ ID** をコピーします。
  
     ![ボットの AppID を取得する](~/assets/images/bots_appid_botframework.png)
  
   * Microsoft Teamsの [**チャット**] ウィンドウで、[**チャットの追加**] アイコンを選択します。 **[対象] の場合:** に、ボットの Microsoft アプリ ID を貼り付けます。
  
     ![ボットの AppID のアップロード](~/assets/images/bots_uploading.png)

     アプリ ID は、ボット名に解決する必要があります。

   * ボットを選択し、メッセージを送信して会話を開始します。
   * または、Microsoft Teamsの左上の検索ボックスにボットのアプリ ID を貼り付けることもできます。 検索結果ページで[人]タブに移動してボットを表示し、チャットを開始します。

ボットは `conversationUpdate` 、チームに追加されたボットと同じようにイベントを受け取りますが、オブジェクト内のチーム情報は表示 `channelData` しません。

## <a name="blocking-a-bot-in-personal-chat"></a>パーソナルチャットでボットをブロックする

ユーザーは、ボットが個人用チャット メッセージを送信するのをブロックできます。 チャットチャンネルでボットを右クリックし、[ **ボットの会話をブロック**] を選択して、この設定を切り替えることができます。 つまり、ボットはメッセージを送信し続けますが、ユーザーはこれらのメッセージを受信しません。

![ボットのブロック](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a>チームからのボットの削除

ユーザーは、チーム ビューのボット リストでごみ箱アイコンを選択して、ボットを削除できます。 これは、そのチームの使用からボットを削除するだけです。個々のユーザーは、個人的なコンテキストで対話することができます。

個人的なコンテキストのボットは Teams、ユーザーが無効にしたり削除したりすることはできません。

## <a name="disabling-a-bot-in-teams"></a>Teamsでボットを無効にする

ボットがメッセージを受信するのを停止するには、Bot ダッシュボードに移動して、Microsoft Teamsチャネルを編集します。 [Microsoft Teams **で有効にする]** オプションをオフにします。 これにより、ユーザーはボットとやり取りできなくなりますが、引き続き検出可能であり、ユーザーは引き続きボットをチームに追加できます。

## <a name="deleting-a-bot-from-teams"></a>Teamsからボットを削除する

Teamsからボットを完全に削除するには、Bot ダッシュボードに移動してMicrosoft Teamsチャネルを編集します。 下部にある **[削除]** ボタンを選択します。 これにより、ユーザーがボットを検出、追加、または操作できなくなります。 他のユーザーのTeamsインスタンスからボットが削除されることはありませんが、ボットの機能も停止します。

## <a name="removing-your-bot-from-appsource"></a>アプリソースからボットを削除する

AppSource (以前はストアOffice) で Teams アプリからボットを削除する場合は、アプリ マニフェストからボットを削除し、検証のためにアプリを再送信する必要があります。 詳細については、「 [Microsoft Teams アプリを AppSource に発行する](~/concepts/deploy-and-publish/apps-publish.md)」を参照してください。
