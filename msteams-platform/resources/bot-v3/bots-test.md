---
title: Bot のテストとデバッグ
description: Microsoft Teams でボットをテストする方法について説明します。
keywords: teams のボットテスト
ms.date: 03/20/2019
ms.openlocfilehash: bb376b1c122b367c9fe74357751459f053d3d44b
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674926"
---
# <a name="test-and-debug-your-microsoft-teams-bot"></a>Microsoft Teams bot をテストおよびデバッグする

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Bot をテストする際には、bot が実行するコンテキストと、Microsoft Teams に固有のデータが必要なすべての機能について考慮することが必要になります。 Bot をテストするために選択した方法が、その機能に合っていることを確認してください。

## <a name="test-by-uploading-to-teams"></a>Teams にアップロードしてテストする

Bot をテストする最も包括的な方法は、アプリパッケージを作成し、それを Teams にアップロードすることです。 これは、すべてのスコープで bot が使用できる完全な機能をテストする唯一の方法です。

アプリをアップロードするには、2つの方法があります。 アプリ[Studio](~/concepts/build-and-test/app-studio-overview.md)を使用して支援するか、アプリ[パッケージ](~/concepts/build-and-test/apps-package.md)を手動で作成し[てアプリをアップロード](~/concepts/deploy-and-publish/apps-upload.md)することができます。 マニフェストを変更してアプリを再アップロードする必要がある場合は、変更したアプリパッケージをアップロードする前に[bot を削除](#deleting-a-bot-from-teams)する必要があります。

## <a name="debug-your-bot-locally"></a>Bot をローカルでデバッグする

開発時にボットをローカルにホストしている場合は、bot をテストするために、 [ngrok](https://ngrok.com/)のようなトンネリングサービスを使用する必要があります。 Ngrok をダウンロードしてインストールしたら、次のコマンドを実行してトンネリングサービスを開始します (パスに ngrok を追加する必要がある場合があります)。

```bash
ngrok http <port> -host-header=localhost:<port>
```

アプリのマニフェストで ngrok によって提供される https エンドポイントを使用します。 コマンドウィンドウを閉じて再起動すると、新しい URL が表示されます。また、そのいずれかを使用するには、bot エンドポイントのアドレスも更新する必要があります。

## <a name="testing-your-bot-without-uploading-to-teams"></a>Teams にアップロードせずに bot をテストする

場合によっては、ボットをアプリとして Teams にインストールせずにテストする必要があります。 これを行うには、次の2つの方法を使用します。 Bot がアプリとしてインストールされていない状態でテストすると、bot が利用可能で応答していることを確認するのに役立ちます。ただし、bot に追加した広範な Microsoft Teams 機能をテストすることはできません。 Bot を完全にテストする必要がある場合は、「」の手順に従って、をアップロードして[テスト](#test-by-uploading-to-teams)してください。

### <a name="use-the-bot-emulator"></a>Bot エミュレーターを使用する

Bot フレームワークエミュレーターは、ボット開発者がローカルまたはリモートでボットをテストしてデバッグできるようにするデスクトップアプリケーションです。 エミュレーターを使用すると、ボットとチャットし、ボットが送受信するメッセージを検査できます。 これは、ボットが利用可能で応答していることを確認するのに便利ですが、お客様が bot に追加した Teams 固有の機能をテストすることはできません。また、お客様が bot からの応答を正確にビジュアルに表示することはできません。Teams でレンダリングされます。 これらのいずれかをテストする必要がある場合は[、bot をアップロード](#test-by-uploading-to-teams)することをお勧めします。

Bot フレームワークエミュレーターの完全な手順については、[こちら](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0)を参照してください。

### <a name="talk-to-your-bot-directly-by-id"></a>Id で自分の bot と直接会話する

>[!Important]
>Id で bot と会話することは、テストのみを目的としています。

Id を使用して、bot との会話を開始することもできます。そのためには、次の2つのメソッドを使用します。 これらのいずれかの方法で bot が追加されている場合は、チャネル会話ではアドレス指定できないため、タブやメッセージング拡張機能などの他の Microsoft Teams アプリ機能を利用することはできません。

1. Bot の[Bot ダッシュボード](https://dev.botframework.com/bots)ページの [**チャネル**] で、[ **Microsoft Teams に追加**] を選択します。 Microsoft Teams は、お客様の bot との個人チャットを使用して起動します。
2. Microsoft Teams 内から bot のアプリ ID を直接参照します。
   * Bot の[Bot ダッシュボード](https://dev.botframework.com/bots)ページで、[**詳細**] の下にある BOT の**Microsoft アプリ ID**をコピーします。
  
     ![Bot の AppID を取得する](~/assets/images/bots_appid_botframework.png)
  
   * Microsoft Teams で、**チャット**ウィンドウから [**チャットの追加**] アイコンを選択します。 [**宛先**] に、ボットの MICROSOFT アプリ ID を貼り付けます。
  
     ![Bot の AppID を取得する](~/assets/images/bots_uploading.png)

     アプリ ID は、bot 名に解決される必要があります。

   * Bot を選択し、メッセージを送信して会話を開始します。
   * または、ボットのアプリ ID を Microsoft Teams の左上にある検索ボックスに貼り付けることもできます。 検索結果ページで、[人] タブに移動して bot を表示し、それとのチャットを開始します。

Bot はチームに追加`conversationUpdate`された bot と同じようにイベントを受け取りますが、チーム情報`channelData`はオブジェクトに含めません。

## <a name="blocking-a-bot-in-personal-chat"></a>個人チャットでボットをブロックする

ユーザーが個人のチャットメッセージを送信しないようにすることを選択できることに注意してください。 チャットチャネルでボットを右クリックして、[**ブロックボット会話**] を選択すると、これを切り替えることができます。 これは、ボットが引き続きメッセージを送信するのに対し、ユーザーはメッセージを受信できないことを意味します。

![Bot をブロックする](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a>チームから bot を削除する

ユーザーは、teams ビューのボットリストで [ごみ箱] アイコンを選択することによって、bot を削除できます。 これにより、チームの使用から bot が削除されるだけであることに注意してください。個々のユーザーは、引き続き個人コンテキストで操作できます。

個人コンテキストのボットは、ユーザーが無効にすることや削除することはできません。 Teams から bot を完全に削除するのは簡単です。

## <a name="disabling-a-bot-in-teams"></a>Teams でボットを無効にする

Bot がメッセージを受信しないようにするには、Bot ダッシュボードに移動して、Microsoft Teams チャネルを編集します。 **[Microsoft Teams で有効にする**] オプションをオフにします。 これにより、ユーザーは bot と対話することができなくなりますが、引き続き検出可能で、ユーザーは引き続き teams に追加することができます。

## <a name="deleting-a-bot-from-teams"></a>Teams から bot を削除する

Bot を Teams から完全に削除するには、Bot ダッシュボードに移動して、Microsoft Teams チャネルを編集します。 下部にある [**削除**] ボタンをクリックします。 これにより、ユーザーは bot を検出、追加、または操作することができなくなります。 これにより、他のユーザーの Teams インスタンスから bot が削除されることはありませんが、機能も停止します。

## <a name="removing-your-bot-from-appsource"></a>AppSource から bot を削除する

この bot を AppSource (旧称 Office ストア) の Teams アプリから削除する場合は、アプリマニフェストから bot を削除して、検証のためにアプリを再送信する必要があります。 詳細については[、「Microsoft Teams アプリを AppSource に発行する](~/concepts/deploy-and-publish/apps-publish.md)」を参照してください。
