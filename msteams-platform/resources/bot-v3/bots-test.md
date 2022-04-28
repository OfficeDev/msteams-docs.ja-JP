---
title: ボットをテストしてデバッグする
description: Microsoft Teamsでボットをテストする方法について説明します
keywords: teams ボットのテスト
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 03/20/2019
ms.openlocfilehash: df403343aab60ebd802b4da0e871649ded8b8a7e
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103433"
---
# <a name="test-and-debug-your-microsoft-teams-bot"></a>Microsoft Teams ボットのテストとデバッグ

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

ボットをテストするときは、ボットを実行するコンテキストと、Microsoft Teamsに固有のデータを必要とするボットに追加した可能性のある機能の両方を考慮する必要があります。 ボットをテストするために選択したメソッドが、その機能と一致していることを確認します。

## <a name="test-by-uploading-to-teams"></a>Teamsにアップロードしてテストする

ボットをテストする最も包括的な方法は、アプリ パッケージを作成してTeamsにアップロードすることです。 これは、すべてのスコープでボットで使用できる完全な機能をテストする唯一の方法です。

アプリをアップロードするには、2 つの方法があります。 [App Studio](~/concepts/build-and-test/app-studio-overview.md) を使用することも、[アプリ パッケージを](~/concepts/build-and-test/apps-package.md)手動で作成して[アプリをアップロードすることもできます](~/concepts/deploy-and-publish/apps-upload.md)。 マニフェストを変更してアプリを再アップロードする必要がある場合は、変更されたアプリ パッケージをアップロードする前に [ボットを削除](#deleting-a-bot-from-teams) する必要があります。

## <a name="debug-your-bot-locally"></a>ボットをローカルでデバッグする

開発中にボットをローカルでホストしている場合は、ボットをテストするために [、ngrok](https://ngrok.com/) などのトンネリング サービスを使用する必要があります。 ngrok をダウンロードしてインストールしたら、次のコマンドを実行してトンネリング サービスを開始します。 パスに ngrok を追加することが必要な場合があります。

```bash
ngrok http <port> -host-header=localhost:<port>
```

アプリ マニフェストで ngrok によって提供される https エンドポイントを使用します。 コマンド ウィンドウを閉じて再起動すると、新しい URL が表示され、ボット エンドポイント アドレスも更新して使用する必要があります。

## <a name="testing-your-bot-without-uploading-to-teams"></a>Teamsにアップロードせずにボットをテストする

場合によっては、Teamsでアプリとしてボットをインストールせずにボットをテストする必要があります。 テストには 2 つの方法があります。 アプリとしてインストールせずにボットをテストすることは、ボットが使用可能で応答していることを確認するのに役立ちますが、ボットに追加した可能性のあるMicrosoft Teams機能の完全な幅をテストすることはできません。 ボットを完全にテストする必要がある場合は、 [アップロードしてテスト](#test-by-uploading-to-teams)する手順に従います。

### <a name="use-the-bot-emulator"></a>ボット Emulatorを使用する

Bot Framework Emulatorは、ボット開発者がローカルまたはリモートでボットをテストおよびデバッグできるようにするデスクトップ アプリケーションです。 エミュレーターを使用すると、ボットとチャットし、ボットが送受信するメッセージを調べることができます。 これは、ボットが使用可能で応答していることを確認するのに役立ちますが、エミュレーターでは、ボットに追加したTeams固有の機能をテストすることはできず、ボットからの応答は、Teamsでレンダリングされる方法を正確に視覚的に表現することもできません。 いずれかのテストが必要な場合は、 [ボットをアップロード](#test-by-uploading-to-teams)するのが最善ではありません。

Bot Framework Emulatorの詳細な手順については、[こちらを参照してください](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)。

### <a name="talk-to-your-bot-directly-by-id"></a>ID で直接ボットに問い合わせてください

>[!Important]
>ID によるボットの会話は、テストのみを目的としています。

ID を使用してボットとの会話を開始することもできます。 これを行うための 2 つの方法を次に示します。 これらの方法のいずれかを通じてボットが追加された場合、チャネル会話ではアドレス指定できず、タブやメッセージ拡張機能などの他のMicrosoft Teamsアプリ機能を利用することはできません。

1. ボットの [[ボット ダッシュボード](https://dev.botframework.com/bots)] ページの [**チャネル**] で、[**Microsoft Teamsに追加]** を選択します。 Microsoft Teamsは、ボットとの個人用チャットで起動します。
2. Microsoft Teams内からボットのアプリ ID を直接参照します。
   * ボットの [[ボット ダッシュボード]](https://dev.botframework.com/bots) ページの [ **詳細**] で、ボットの **Microsoft アプリ ID を** コピーします。
  
     ![ボットの AppID を取得する](~/assets/images/bots_appid_botframework.png)
  
   * Microsoft Teams内の **[チャット**] ウィンドウで、[**チャットの追加**] アイコンを選択します。 **[To:] に**、ボットの Microsoft アプリ ID を貼り付けます。
  
     ![ボットの AppID のアップロード](~/assets/images/bots_uploading.png)

     アプリ ID はボット名に解決する必要があります。

   * ボットを選択し、メッセージを送信して会話を開始します。
   * または、Microsoft Teamsの左上にある検索ボックスにボットのアプリ ID を貼り付けることができます。 検索結果ページで 、[ユーザー] タブに移動してボットを表示し、チャットを開始します。

ボットは、チームに追加された `conversationUpdate` ボットと同じようにイベントを受け取りますが、オブジェクト内 `channelData` のチーム情報は含めなくなります。

## <a name="blocking-a-bot-in-personal-chat"></a>個人用チャットでボットをブロックする

ユーザーは、ボットが個人用チャット メッセージを送信できないようにすることを選択できることに注意してください。 チャット チャネルでボットを右クリックし、[ **ボットの会話をブロック**] を選択することで、これを切り替えることができます。 つまり、ボットは引き続きメッセージを送信しますが、ユーザーはこれらのメッセージを受信しません。

![ボットをブロックする](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a>チームからのボットの削除

ユーザーは、チーム ビューでボットの一覧でごみ箱アイコンを選択することで、ボットを削除できます。 これは、そのチームの使用からボットを削除するだけで、個々のユーザーが個人的なコンテキストで対話できることに注意してください。

個人用コンテキストのボットは、Teamsからボットを完全に削除する場合を除き、ユーザーが無効にしたり削除したりすることはできません。

## <a name="disabling-a-bot-in-teams"></a>Teamsでボットを無効にする

ボットがメッセージを受信するのを停止するには、ボット ダッシュボードに移動し、Microsoft Teams チャネルを編集します。 **[Microsoft Teamsで有効にする] オプションをオフにします**。 これにより、ユーザーはボットと対話できなくなりますが、検出可能であり、ユーザーはボットをチームに追加できます。

## <a name="deleting-a-bot-from-teams"></a>Teamsからボットを削除する

Teamsからボットを完全に削除するには、ボット ダッシュボードに移動し、Microsoft Teams チャネルを編集します。 下部にある **[削除** ] ボタンを選択します。 これにより、ユーザーがボットを検出、追加、または操作できなくなります。 これにより、他のユーザーのTeams インスタンスからボットが削除されることはありませんが、ボットの機能も停止することに注意してください。

## <a name="removing-your-bot-from-appsource"></a>AppSource からボットを削除する

AppSource (以前は Office Store) でTeams アプリからボットを削除する場合は、アプリ マニフェストからボットを削除し、検証のためにアプリを再送信する必要があります。 詳細については、「[Microsoft Teams アプリを AppSource に発行する」を参照してください](~/concepts/deploy-and-publish/apps-publish.md)。
