---
title: ボットをローカルでテストおよびデバッグする
author: surbhigupta
description: Teams 環境内の IDE を使用してボットをローカルでテストおよびデバッグする方法について、サイドローディング、ボット エミュレーターを使用した Teams の外部、ボットと直接話し合う方法について説明します。
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 9ac6e2f7bf173e68e111b0d792ec89ba266c188f
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2021
ms.locfileid: "60888231"
---
# <a name="test-and-debug-your-bot-locally"></a>ボットをローカルでテストおよびデバッグする

ボットをテストする場合は、ボットで実行するコンテキストと、Microsoft Teams に固有のデータを必要とするボットに追加した可能性があるすべての機能の両方を考慮する必要があります。 ボットをテストするために選択したメソッドが、その機能と一致している必要があります。

## <a name="test-by-uploading-to-teams"></a>アプリにアップロードしてテストTeams

ボットをテストする最も包括的な方法は、アプリ パッケージを作成し、アプリ パッケージをアプリ パッケージにアップロードTeams。 これは、すべてのスコープでボットで使用できる完全な機能をテストする唯一の方法です。

アプリをアップロードするには、次の 2 つの方法があります。
* [App Studio を使用します](~/concepts/build-and-test/app-studio-overview.md)。
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

## <a name="test-your-bot-without-uploading-to-teams"></a>ボットにアップロードせずにボットをテストTeams

場合によっては、ボットをアプリとしてインストールせずにボットをテストする必要Teams。 ボットをテストする 2 つの方法を提供します。 アプリとしてインストールせずにボットをテストすると、ボットが利用可能で応答を確実に行うのに役立ちますが、ボットに追加した Microsoft Teams 機能の全幅をテストできません。 ボットを完全にテストする必要がある場合は、「アップロード [によるテスト」を参照してください](#test-by-uploading-to-teams)。

### <a name="use-the-bot-emulator"></a>ボット を使用Emulator

このBot Framework Emulatorは、ボット開発者がボットをローカルまたはリモートでテストおよびデバッグできるデスクトップ アプリケーションです。 エミュレーターは、ボットとチャットし、ボットが送信および受信するメッセージを調べするのに役立ちます。 これは、ボットが使用可能で応答を確認する場合に役立ちます。 ただし、エミュレーターでは、ボットに追加した Teams 固有の機能をテストできません。また、ボットからの応答は、Teams でのレンダリング方法の正確な視覚的表現です。 これらのテストを行う必要がある場合は、ボットをアップロード [する方が最適です](#test-by-uploading-to-teams)。

詳細については、「詳細な手順[」を参照Bot Framework Emulator。](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)

### <a name="talk-to-your-bot-directly-by-id"></a>ボットと ID で直接話す

> [!Important]
> ID でボットと話すのは、基本的なテストのみを目的とします。 ボットTeams特定の機能が機能しません。

ボットとの会話を開始するには、その ID を使用します。 これらの方法のいずれかを使用してボットを追加した場合、チャネル会話では対応できません。また、タブやメッセージング拡張機能などの他の Microsoft Teams アプリ機能を利用することはできません。 次のいずれかの方法で会話を開始できます。

* ボットの [[ボット ダッシュボード]](https://dev.botframework.com/bots)ページの [チャネル]**で、[ボット** に追加] を選択 **Microsoft Teams。** Microsoft Teamsボットとの個人用チャットを起動します。

* ボットのアプリ ID を次の場所から直接参照Microsoft Teams。
   1. ボットの [[ボット ダッシュボード]](https://dev.botframework.com/bots)ページの [詳細] で、ボットの **Microsoft App ID** をコピーします。
  
      ![ボットの AppID の取得](~/assets/images/bots_appid_botframework.png)
  
   2. [チャットMicrosoft Teamsを開き、[チャットの追加]**アイコンを選択** します。 **[To:]** で、ボットの Microsoft App ID を貼り付けます。
  
      ![ボットのアップロード](~/assets/images/bots_uploading.png)

      アプリ ID はボット名に解決する必要があります。

   3. ボットを選択し、メッセージを送信して会話を開始します。
      または、ボットのアプリ ID をアプリの左上の検索ボックスに貼り付Microsoft Teams。 検索結果ページで、[ユーザー] タブに移動してボットを表示し、チャットを開始します。

ボットは、オブジェクト内のチーム情報なしで、ボットをチームに追加すると `conversationUpdate` イベントを受け取 `channelData` ります。

## <a name="block-a-bot-in-personal-chat"></a>個人用チャットでボットをブロックする

ユーザーは、ボットが個人のチャット メッセージを送信するのをブロックできます。 チャット チャネルでボットを右クリックし、[ボットの会話をブロックする] を選択することで、これを **切り替える場合があります**。 つまり、ボットは引き続きメッセージを送信しますが、ユーザーはメッセージを受信しません。

![ボットのブロック](~/assets/images/bots/botdisable.png)

## <a name="remove-a-bot-from-a-team"></a>チームからボットを削除する

ユーザーは、チームのビューでボットリストのごみ箱アイコンを選択して、ボットを削除できます。 これにより、そのチームの使用からボットが削除されるだけで、個々のユーザーは個人のコンテキストで操作できます。 個人用コンテキストのボットは、ユーザーが無効にしたり削除したりすることはできません。

## <a name="disable-a-bot-in-teams"></a>アプリでボットを無効Teams

ボットがメッセージを受け取るのを停止するには、ボット ダッシュボードに移動し、ボット チャネルMicrosoft Teamsします。 [有効にする **] オプションをMicrosoft Teams** します。 これにより、ユーザーはボットを操作できませんが、検出可能であり、ユーザーは引き続きボットに追加Teams。

## <a name="delete-a-bot-from-teams"></a>ボットを削除Teams

ボットを完全に削除するにはTeamsボット ダッシュボードに移動し、ボット チャネルMicrosoft Teamsします。 下部にある **[削除** ] ボタンを選択します。 これにより、ユーザーはボットを検出、追加、操作できます。 これにより、他のユーザーのインスタンスからボットTeams削除されるわけではありませんが、ボットの機能も停止します。

## <a name="see-also"></a>関連項目

* [検査ミドルウェアでボットのデバッグを行う](/azure/bot-service/bot-service-debug-inspection-middleware)
* [ローカルで呼び出しや会議用ボットのデバッグを行う](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
