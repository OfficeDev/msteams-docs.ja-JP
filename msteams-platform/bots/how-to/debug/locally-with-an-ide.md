---
title: ボットをローカルでテストおよびデバッグする
author: clearab
description: IDE を使用してボットをローカルでテストおよびデバッグする
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 449d6dd5e10a72538e6443c9d17f998ebc662379
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634770"
---
# <a name="test-and-debug-your-bot-locally"></a>ボットをローカルでテストおよびデバッグする

ボットをテストする場合は、ボットで実行するコンテキストと、Microsoft Teams 固有のデータを必要とするボットに追加した可能性があるすべての機能の両方を考慮する必要があります。 ボットをテストするために選択したメソッドが、その機能と一致している必要があります。

## <a name="test-by-uploading-to-teams"></a>Teams にアップロードしてテストする

ボットをテストする最も包括的な方法は、アプリ パッケージを作成して Teams にアップロードする方法です。 これは、すべてのスコープでボットで使用できる完全な機能をテストする唯一の方法です。

アプリをアップロードするには、次の 2 つの方法があります。
* [アプリ Studio を使用する](~/concepts/build-and-test/app-studio-overview.md)
* [アプリ パッケージを手動で作成](~/concepts/build-and-test/apps-package.md) し、アプリ [をアップロードします](~/concepts/deploy-and-publish/apps-upload.md)。

> [!NOTE]
> マニフェストを変更してアプリを再アップロードする必要がある場合は、変更された[](#delete-a-bot-from-teams)アプリ パッケージをアップロードする前にボットを削除する必要があります。

## <a name="debug-your-bot-locally"></a>ボットをローカルでデバッグする

開発中にボットをローカルでホストしている場合は、ボットをテストするために [ngrok](https://ngrok.com/) のようなトンネリング サービスを使用する必要があります。 ngrok をダウンロードしてインストールした後、パスに追加し、次のコマンドを実行してトンネ `ngrok` リング サービスを開始します。

```bash
ngrok http <port> -host-header=localhost:<port>
```

アプリ マニフェストで ngrok によって提供される https エンドポイントを使用します。 

> [!NOTE]
> コマンド ウィンドウを閉じて再起動すると、新しい URL が生成され、ボット エンドポイント のアドレスを更新して使用する必要があります。

## <a name="test-your-bot-without-uploading-to-teams"></a>Teams にアップロードせずにボットをテストする

場合によっては、Teams にアプリとしてインストールせずにボットをテストする必要がある場合があります。 ボットをテストする 2 つの方法を提供します。 アプリとしてインストールせずにボットをテストすると、ボットが利用可能で応答を確実に行うのに役立ちますが、ボットに追加した Microsoft Teams 機能の全幅をテストできません。 ボットを完全にテストする必要がある場合は、「アップロード [によるテスト」を参照してください](#test-by-uploading-to-teams)。

### <a name="use-the-bot-emulator"></a>ボット エミュレーターの使用

ボット フレームワーク エミュレーターは、ボット開発者がボットをローカルまたはリモートでテストおよびデバッグできるデスクトップ アプリケーションです。 エミュレーターは、ボットとチャットし、ボットが送信および受信するメッセージを調べするのに役立ちます。 これは、ボットが使用可能で応答を確認する場合に役立ちます。 ただし、エミュレーターでは、ボットに追加した Teams 固有の機能をテストできません。また、ボットからの応答は、Teams でのレンダリング方法を正確に視覚的に表現します。 これらのテストを行う必要がある場合は、ボットをアップロード [する方が最適です](#test-by-uploading-to-teams)。

詳細については [、「Bot Framework エミュレーター」の完全な手順を参照してください](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)。

### <a name="talk-to-your-bot-directly-by-id"></a>ボットと ID で直接話す

> [!Important]
> ID でボットと話すのは、基本的なテストのみを目的とします。 ボットに追加した Teams 固有の機能は動作しません。

ボットとの会話を開始するには、その ID を使用します。 これらの方法のいずれかを使用してボットを追加した場合、チャネルの会話では対応できません。また、タブやメッセージング拡張機能などの他の Microsoft Teams アプリ機能を利用することはできません。 次のいずれかの方法で会話を開始できます。

* ボットの [[ボット ダッシュボード]](https://dev.botframework.com/bots)ページの [チャネル] で、[Microsoft Teams に **追加] を選択します**。 Microsoft Teams は、ボットとの個人用チャットを起動します。

* Microsoft Teams 内からボットのアプリ ID を直接参照します。
   1. ボットの [[ボット ダッシュボード]](https://dev.botframework.com/bots)ページの [詳細] で、ボットの **Microsoft App ID** をコピーします。
  
      ![ボットの AppID の取得](~/assets/images/bots_appid_botframework.png)
  
   2. Microsoft Teams を開き、[チャット] ウィンドウ **で** [チャットの追加 **] アイコンを選択** します。 **[To:]** で、ボットの Microsoft App ID を貼り付けます。
  
      ![ボットのアップロード](~/assets/images/bots_uploading.png)

      アプリ ID はボット名に解決する必要があります。

   3. ボットを選択し、メッセージを送信して会話を開始します。
      または、Microsoft Teams の左上にある検索ボックスにボットのアプリ ID を貼り付けることができます。 検索結果ページで、[ユーザー] タブに移動してボットを表示し、チャットを開始します。

ボットは、オブジェクト内のチーム情報なしで、ボットをチームに追加すると `conversationUpdate` イベントを受け取 `channelData` ります。

## <a name="block-a-bot-in-personal-chat"></a>個人用チャットでボットをブロックする

ユーザーは、ボットが個人のチャット メッセージを送信するのをブロックできます。 チャット チャネルでボットを右クリックし、[ボットの会話をブロックする] を選択することで、これを **切り替える場合があります**。 つまり、ボットは引き続きメッセージを送信しますが、ユーザーはメッセージを受信しません。

![ボットのブロック](~/assets/images/bots/botdisable.png)

## <a name="remove-a-bot-from-a-team"></a>チームからボットを削除する

ユーザーは、チームのビューでボットリストのごみ箱アイコンを選択して、ボットを削除できます。 これにより、そのチームの使用からボットが削除されるだけで、個々のユーザーは個人のコンテキストで操作できます。 個人用コンテキストのボットは、ユーザーが無効にしたり削除したりすることはできません。

## <a name="disable-a-bot-in-teams"></a>Teams でボットを無効にする

ボットがメッセージの受信を停止するには、ボット ダッシュボードに移動し、Microsoft Teams チャネルを編集します。 [Microsoft **Teams で有効にする] オプションをオフ** にします。 これにより、ユーザーはボットを操作できませんが、検出可能であり、ユーザーは引き続き Teams に追加できます。

## <a name="delete-a-bot-from-teams"></a>Teams からボットを削除する

Teams からボットを完全に削除するには、ボットダッシュボードに移動し、Microsoft Teams チャネルを編集します。 下部にある **[削除** ] ボタンを選択します。 これにより、ユーザーはボットを検出、追加、操作できます。 これにより、他のユーザーの Teams インスタンスからボットが削除されるわけではありませんが、ボットの機能も停止します。

## <a name="see-also"></a>関連項目

> [!div class=nextstep]
> [検査ミドルウェアでボットのデバッグを行う](/azure/bot-service/bot-service-debug-inspection-middleware)

> [!div class=nextstep]
> [ローカルで呼び出しや会議用ボットのデバッグを行う](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
