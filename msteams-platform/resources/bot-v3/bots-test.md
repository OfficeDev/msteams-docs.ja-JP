---
title: ボットのテストとデバッグ
description: Microsoft Teams でボットをテストする方法について説明します。
keywords: teams ボットのテスト
ms.topic: how-to
localization_priority: Normal
ms.date: 03/20/2019
ms.openlocfilehash: 0f44a88bcf054f4e0f4112ddc8bd3fbfdc18117d
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020633"
---
# <a name="test-and-debug-your-microsoft-teams-bot"></a>Microsoft Teams ボットのテストとデバッグ

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

ボットをテストする場合は、ボットを実行するコンテキストと、Microsoft Teams 固有のデータを必要とするボットに追加した可能性がある機能の両方を考慮する必要があります。 ボットをテストするために選択したメソッドが、その機能と一致することを確認します。

## <a name="test-by-uploading-to-teams"></a>Teams にアップロードしてテストする

ボットをテストする最も包括的な方法は、アプリ パッケージを作成して Teams にアップロードする方法です。 これは、すべてのスコープでボットで使用できる完全な機能をテストする唯一の方法です。

アプリをアップロードするには、2 つの方法があります。 App Studio を使用[して支援することもできます](~/concepts/build-and-test/app-studio-overview.md)し、アプリ パッケージ[](~/concepts/build-and-test/apps-package.md)を手動で作成してアプリ[をアップロードすることもできます](~/concepts/deploy-and-publish/apps-upload.md)。 マニフェストを変更してアプリを再アップロードする必要がある場合は、変更された[](#deleting-a-bot-from-teams)アプリ パッケージをアップロードする前にボットを削除する必要があります。

## <a name="debug-your-bot-locally"></a>ボットをローカルでデバッグする

開発中にボットをローカルでホストしている場合は、ボットをテストするために [ngrok](https://ngrok.com/) のようなトンネリング サービスを使用する必要があります。 ngrok をダウンロードしてインストールしたら、次のコマンドを実行してトンネリング サービスを開始します (パスに ngrok を追加する必要がある場合があります)。

```bash
ngrok http <port> -host-header=localhost:<port>
```

アプリ マニフェストで ngrok によって提供される https エンドポイントを使用します。 コマンド ウィンドウを閉じて再起動すると、新しい URL が取得され、その URL も使用するにはボット エンドポイント アドレスを更新する必要があります。

## <a name="testing-your-bot-without-uploading-to-teams"></a>Teams にアップロードせずにボットをテストする

場合によっては、Teams にアプリとしてインストールせずにボットをテストする必要がある場合があります。 これを行う 2 つの方法を以下に示します。 アプリとしてインストールせずにボットをテストすると、ボットが利用可能で応答を確実に行うのに役立ちますが、ボットに追加した Microsoft Teams の機能全体をテストできません。 ボットを完全にテストする必要がある場合は、アップロードによるテストの手順 [に従ってください](#test-by-uploading-to-teams)。

### <a name="use-the-bot-emulator"></a>ボット エミュレーターの使用

ボット フレームワーク エミュレーターは、ボット開発者がボットをローカルまたはリモートでテストおよびデバッグできるデスクトップ アプリケーションです。 エミュレーターを使用すると、ボットとチャットし、ボットが送信および受信するメッセージを検査できます。 これは、ボットが使用可能で応答を確認する場合に役立ちますが、エミュレーターでは、ボットに追加した Teams 固有の機能をテストしたり、ボットからの応答を Teams でレンダリングする方法を正確に視覚的に表現したりできません。 これらのテストを行う必要がある場合は、ボットをアップロード [する方が最適です](#test-by-uploading-to-teams)。

Bot Framework エミュレーターの完全な手順については、こちらを参照 [してください](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)。

### <a name="talk-to-your-bot-directly-by-id"></a>Id でボットに直接話す

>[!Important]
>Id によってボットと話すのは、テスト目的のみを目的とします。

ボットの ID を使用して、ボットとの会話を開始できます。これを行う 2 つの方法を以下に示します。 これらの方法のいずれかを使用してボットが追加された場合、チャネル会話では対応できません。また、タブやメッセージング拡張機能などの他の Microsoft Teams アプリ機能を利用することはできません。

1. ボットの [[ボット ダッシュボード]](https://dev.botframework.com/bots)ページの [チャネル] で、[Microsoft Teams に **追加] を選択します**。 Microsoft Teams は、ボットとの個人用チャットで起動します。
2. Microsoft Teams 内からボットのアプリ ID を直接参照します。
   * ボットの [[ボット ダッシュボード]](https://dev.botframework.com/bots)ページの [詳細] で、ボットの **Microsoft App ID** をコピーします。
  
     ![ボットの AppID の取得](~/assets/images/bots_appid_botframework.png)
  
   * Microsoft Teams 内の [チャット] ウィンドウ **で** 、[チャットの追加] **アイコンを選択** します。 **[To:]** の場合は、ボットの Microsoft App ID を貼り付けます。
  
     ![ボットの AppID のアップロード](~/assets/images/bots_uploading.png)

     アプリ ID はボット名に解決する必要があります。

   * ボットを選択し、メッセージを送信して会話を開始します。
   * または、Microsoft Teams の左上にある検索ボックスにボットのアプリ ID を貼り付けることができます。 検索結果ページで、[ユーザー] タブに移動してボットを表示し、チャットを開始します。

ボットは、チームに追加されたボットと同様に、オブジェクト内のチーム情報なしでイベント `conversationUpdate` を受信 `channelData` します。

## <a name="blocking-a-bot-in-personal-chat"></a>個人用チャットでのボットのブロック

ユーザーは、ボットが個人のチャット メッセージを送信するのをブロックすることができます。 チャット チャネルでボットを右クリックし、[ボットの会話をブロックする] を選択することで、これを **切り替える場合があります**。 つまり、ボットは引き続きメッセージを送信しますが、ユーザーはそれらのメッセージを受信しません。

![ボットのブロック](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a>チームからボットを削除する

ユーザーは、チーム ビューでボットリストのごみ箱アイコンを選択して、ボットを削除できます。 これは、そのチームの使用からボットを削除するだけである点に注意してください。個々のユーザーは引き続き個人のコンテキストで対話できます。

個人用コンテキストのボットを無効にしたり、ユーザーが削除したりすることはできません。Teams からボットを完全に削除することはできません。

## <a name="disabling-a-bot-in-teams"></a>Teams でボットを無効にする

ボットのメッセージ受信を停止するには、ボット ダッシュボードに移動し、Microsoft Teams チャネルを編集します。 [Microsoft **Teams で有効にする] オプションをオフ** にします。 これにより、ユーザーはボットを操作できませんが、検出可能であり、ユーザーは引き続きチームに追加できます。

## <a name="deleting-a-bot-from-teams"></a>Teams からボットを削除する

Teams からボットを完全に削除するには、ボット ダッシュボードに移動し、Microsoft Teams チャネルを編集します。 下部にある **[削除** ] ボタンを選択します。 これにより、ユーザーはボットを検出、追加、または操作できます。 これは他のユーザーの Teams インスタンスからボットを削除しませんが、ボットの機能も停止します。

## <a name="removing-your-bot-from-appsource"></a>AppSource からボットを削除する

AppSource (以前は Office ストア) の Teams アプリからボットを削除する場合は、アプリ マニフェストからボットを削除し、検証のためにアプリを再送信する必要があります。 詳細 [については、「Microsoft Teams アプリを AppSource に発行する](~/concepts/deploy-and-publish/apps-publish.md) 」を参照してください。
