---
title: ボットのテストおよびデバッグ
description: この記事では、Microsoft Teamsでボットをテストしてデバッグし、Teamsにアップロードせずにボットをテストする方法について説明します。
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 03/20/2019
ms.openlocfilehash: 71045071666ecc21cdc376590deef90223694d15
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189751"
---
# <a name="test-and-debug-your-microsoft-teams-bot"></a>Microsoft Teams ボットのテストとデバッグ

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

ボットをテストする場合は、ボットを実行するコンテキストと、Microsoft Teamsに固有のデータを必要とするボットに追加した可能性のある機能の両方を考慮する必要があります。 ボットをテストするために選択したメソッドが、その機能と一致していることを確認します。

## <a name="test-by-uploading-to-teams"></a>Teams にアップロードしてテストする

ボットをテストする最も包括的な方法は、アプリ パッケージを作成して Teams にアップロードすることです。 これは、すべてのスコープでボットで使用できる完全な機能をテストする唯一の方法です。

アプリをアップロードするには、2 つの方法があります。 [App Studio](~/concepts/build-and-test/app-studio-overview.md) を使用することも、手動で[アプリ パッケージを作成](~/concepts/build-and-test/apps-package.md)して[アプリをアップロードする](~/concepts/deploy-and-publish/apps-upload.md)こともできます。 マニフェストを変更し、アプリを再アップロードする必要がある場合は、変更されたアプリ パッケージをアップロードする前に [ボットを削除](#deleting-a-bot-from-teams) する必要があります。

## <a name="debug-your-bot-locally"></a>ローカルでボットのデバッグを行う

開発中にボットをローカルでホストしている場合は、ボットをテストするために [、ngrok](https://ngrok.com/) などのトンネリング サービスを使用する必要があります。 ngrok をダウンロードしてインストールしたら、次のコマンドを実行してトンネリング サービスを開始します。 パスに ngrok を追加することが必要な場合があります。

```bash
ngrok http <port> -host-header=localhost:<port>
```

アプリ マニフェストで ngrok によって提供される https エンドポイントを使用します。 コマンド ウィンドウを閉じて再起動すると、新しい URL が表示され、ボット エンドポイント アドレスも更新して使用する必要があります。

## <a name="testing-your-bot-without-uploading-to-teams"></a>Teams にアップロードせずにボットをテストする

場合によっては、Teams でアプリとしてボットをインストールせずにボットをテストする必要があります。 テストには 2 つの方法があります。 ボットをアプリとしてインストールせずにテストすることは、ボットが使用可能で応答していることを確認するのに役立ちますが、ボットに追加した可能性のある機能の完全な幅Teamsテストすることはできません。 ボットを完全にテストする必要がある場合は、 [アップロードしてテストする](#test-by-uploading-to-teams)手順に従います。

### <a name="use-the-bot-emulator"></a>ボット エミュレーターを使用する

Bot Framework Emulator は、ボット開発者がローカルまたはリモートでボットをテストおよびデバッグできるようにするデスクトップ アプリケーションです。 エミュレーターを使用すると、ボットとチャットし、ボットが送受信するメッセージを調べることができます。 これは、ボットが使用可能で応答していることを確認するのに役立ちますが、エミュレーターでは、ボットに追加したTeams固有の機能をテストすることはできず、ボットからの応答は、Teamsでレンダリングされる方法を正確に視覚的に表現することもできません。 これらのいずれかをテストする必要がある場合は、[ボットをアップロード](#test-by-uploading-to-teams)するのは最善ではありません。

Bot Framework Emulatorの詳細な手順については、[こちら](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)を参照してください。

### <a name="talk-to-your-bot-directly-by-id"></a>ID を使用して直接ボットに問い合わせてください

>[!Important]
>ID を使用したボットの会話は、テストのみを目的としています。

ID を使用してボットとの会話を開始することもできます。 これを行うための 2 つの方法を次に示します。 これらの方法のいずれかを通じてボットを追加すると、チャネルの会話ではアドレス指定できず、タブやメッセージ拡張機能などの他のMicrosoft Teams アプリ機能を利用することはできません。

1. ボットの [[ボット ダッシュボード]](https://dev.botframework.com/bots) ページの **[チャネル]** で、**[Microsoft Teams に追加]** を選択します。 Teamsは、ボットとの個人用チャットで起動します。
2. Teams内からボットのアプリ ID を直接参照します。
   * ボットの [[ボット ダッシュボード]](https://dev.botframework.com/bots) ページの **[詳細]** で、ボットの **Microsoft App ID** をコピーします。
  
      :::image type="content" source="../../assets/images/bots_appid_botframework.png" alt-text="ボット ダッシュボード":::
  
   * Teams内の **[チャット**] ウィンドウで、[**チャットの追加**] アイコンを選択します。 **[To:]** に、ボットの Microsoft アプリ ID を貼り付けます。
  
      :::image type="content" source="../../assets/images/bots_uploading.png" alt-text="ボットの AppID のアップロード"border="true":::

     アプリ ID はボット名に解決する必要があります。

   * ボットを選択し、メッセージを送信して会話を開始します。

   * または、Microsoft Teams の左上にある検索ボックスにボットのアプリ ID を貼り付けることができます。 検索結果ページで、[ユーザー] タブに移動してボットを表示し、チャットを開始します。

ボットは、チームに追加されたボットと同じように `conversationUpdate` イベントを受け取りますが、`channelData` オブジェクト内のチーム情報は含めなくなります。

## <a name="blocking-a-bot-in-personal-chat"></a>個人用チャットでボットをブロックする

ユーザーは、ボットが個人用チャット メッセージを送信できないようにすることを選択できます。 チャット チャネルでボットを右クリックし、**[ボットの会話をブロック]** を選択することで、これを切り替えることができます。 つまり、ボットは引き続きメッセージを送信しますが、ユーザーはこれらのメッセージを受信しません。

  :::image type="content" source="../../assets/images/bots/botdisable.png" alt-text="ボットをブロックする"border="true":::

## <a name="removing-a-bot-from-a-team"></a>チームからボットを削除する

ユーザーは、チーム ビューでボットの一覧でごみ箱アイコンを選択することで、ボットを削除できます。 これは、そのチームの使用からボットを削除するだけであり、個々のユーザーは個人的なコンテキストで対話できることに注意してください。

個人コンテキストのボットは、ユーザーが無効にしたり削除したりすることはできません。これは、Teamsからボットを完全に削除するわけではありません。

## <a name="disabling-a-bot-in-teams"></a>Teams でボットを無効にする

ボットがメッセージを受信するのを停止するには、ボット ダッシュボードに移動し、Microsoft Teams チャネルを編集します。 **[Microsoft Teams で有効にする]** オプションをオフにします。 これにより、ユーザーはボットと対話できなくなりますが、検出は可能であり、ユーザーはボットをチームに追加できます。

## <a name="deleting-a-bot-from-teams"></a>Teams からボットを削除する

Teams からボットを完全に削除するには、ボット ダッシュボードに移動し、Microsoft Teams チャネルを編集します。 ページの下部にある **[削除]** をクリックします。 これにより、ユーザーがボットを検出、追加、または操作できなくなります。 これにより、他のユーザーのTeams インスタンスからボットが削除されることはありませんが、ボットの機能も停止します。

## <a name="removing-your-bot-from-appsource"></a>AppSource からボットを削除する

AppSource (以前は Office Store) で Teams アプリからボットを削除する場合は、アプリ マニフェストからボットを削除し、検証のためにアプリを再送信する必要があります。 詳細については、「[Microsoft Teams アプリを AppSource に発行する](~/concepts/deploy-and-publish/apps-publish.md)」を参照してください。
