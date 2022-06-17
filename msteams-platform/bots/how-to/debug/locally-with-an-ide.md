---
title: ボットをローカルでテストしてデバッグする
author: surbhigupta
description: サイドローディングなどを使用して、Teams環境内の IDE を使用してボットをローカルでテストしてデバッグする方法について説明します
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 95a52b02c864a65454a8a03fa9917c4a5d99fdb8
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142893"
---
# <a name="test-and-debug-your-bot-locally"></a>ボットをローカルでテストしてデバッグする

ボットをテストするときは、ボットを実行するコンテキストと、Microsoft Teamsに固有のデータを必要とするボットに追加した可能性のある機能の両方を考慮する必要があります。 ボットをテストするために選択したメソッドが、その機能と一致していることを確認してください。

## <a name="test-by-uploading-to-teams"></a>Teams にアップロードしてテストする

ボットをテストする最も包括的な方法は、アプリ パッケージを作成して Teams にアップロードすることです。 これは、すべてのスコープでボットで使用できる完全な機能をテストする唯一の方法です。

アプリをアップロードするには、以下の 2 つの方法があります。

* [App Studio](~/concepts/build-and-test/app-studio-overview.md) を使用します。
* [アプリ パッケージを手動で作成](~/concepts/build-and-test/apps-package.md)し、[アプリをアップロード](~/concepts/deploy-and-publish/apps-upload.md)します。

> [!NOTE]
> マニフェストを変更してアプリを再アップロードするには、変更されたアプリ パッケージをアップロードする前に[ボットを削除](#delete-a-bot-from-teams)します。
> ボットをテストするには、Teams でサイドローディングを有効にします。 「[サイドローディングを有効にする](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)」を参照してください。

## <a name="debug-your-bot-locally"></a>ローカルでボットのデバッグを行う

開発中にボットをローカルでホストしている場合は、ボットをテストするために [ngrok](https://ngrok.com/) などのトンネリング サービスを使用する必要があります。 ngrok をダウンロードしてインストールした後、パスに `ngrok` を追加し、次のコマンドを実行してトンネリング サービスを開始します。

```bash
ngrok http <port> --host-header=localhost:<port>
```

アプリ マニフェストで ngrok によって提供される https エンドポイントを使用します。

> [!NOTE]
> コマンド ウィンドウを閉じて再起動すると、新しい URL が生成され、ボット エンドポイント アドレスも更新して使用する必要があります。

## <a name="test-your-bot-without-uploading-to-teams"></a>Teams にアップロードせずにボットをテストする

場合によっては、Teams でアプリとしてボットをインストールせずにボットをテストする必要があります。 ボットのテストには 2 つの方法があります。 ボットをアプリとしてインストールせずにテストすると、ボットが使用可能で応答していることを確認するのに役立ちます。 ただし、ボットに追加したMicrosoft Teams機能の完全な幅をテストすることはできません。 ボットを完全にテストする場合は、[アップロードによるテスト](#test-by-uploading-to-teams)を参照してください。

### <a name="use-the-bot-emulator"></a>ボット エミュレーターを使用する

Bot Framework Emulator は、ボット開発者がローカルまたはリモートでボットをテストおよびデバッグできるようにするデスクトップ アプリケーションです。 エミュレーターは、ボットとチャットし、ボットが送受信するメッセージを調べるのに役立ちます。 これは、ボットが使用可能であり、応答していることを確認するのに役立ちます。 ただし、エミュレーターでは、ボットに追加した Teams 固有の機能をテストすることは許可されておらず、ボットからの応答は、Teams でレンダリングされる方法を視覚的に正確に表しています。 これらのいずれかをテストする必要がある場合は、[ボットをアップロード](#test-by-uploading-to-teams)するのが最善策です。

詳細については、「[ボット フレームワーク エミュレーターに関する完全な手順](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)」を参照してください。

### <a name="talk-to-your-bot-directly-by-id"></a>ID を使用して直接ボットに問い合わせてください

> [!Important]
> ID を使用したボットとの会話は、テストのみを目的としています。 ボットに追加した Teams 固有の機能は動作しません。

ID を使用してボットとの会話を開始します。 これらの方法のいずれかを通じてボットが追加された場合、チャネル会話ではアドレス指定できず、タブやメッセージ拡張機能などの他の Microsoft Teams アプリ機能を利用することはできません。 次のいずれかの方法で会話を開始します。

* ボットの [[ボット ダッシュボード]](https://dev.botframework.com/bots) ページの **[チャネル]** で、**[Microsoft Teams に追加]** を選択します。 Microsoft Teams は、ボットとの個人用チャットで起動します。

* Microsoft Teams 内からボットのアプリ ID を直接参照します。
   1. ボットの [[ボット ダッシュボード]](https://dev.botframework.com/bots) ページの **[詳細]** で、ボットの **Microsoft App ID** をコピーします。
  
      ![ボットの AppID を取得する](~/assets/images/bots_appid_botframework.png)
  
   2. Microsoft Teams 内の **[チャット]** ウィンドウを開き、**[チャットの追加]** アイコンを選択します。 **[宛先]** に、ボットの Microsoft アプリ ID を貼り付けます。
  
      ![ボットのアップロード](~/assets/images/bots_uploading.png)

      アプリ ID はボット名で解決する必要があります。

   3. ボットを選択し、メッセージを送信して会話を開始します。
      または、Microsoft Teams の左上にある検索ボックスにボットのアプリ ID を貼り付けることができます。 検索結果ページで、**[ユーザー]** タブに移動してボットを表示し、チャットを開始します。

> [!Note]
> Microsoft Teams でボットのアプリ ID を参照するには、[アプリのサイドローディング](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)を有効にします。

ボットは、`channelData` オブジェクト内のチーム情報がなくても、チームに追加されたボットと同じように `conversationUpdate` イベントを受け取ります。

## <a name="block-a-bot-in-personal-chat"></a>個人用チャットでボットをブロックする

ユーザーは、ボットが個人用チャット メッセージを送信できないようにすることを選択できます。 チャット チャネルでボットを右クリックし、**[ボットの会話をブロック]** を選択することで、これを切り替えることができます。 つまり、ボットは引き続きメッセージを送信しますが、ユーザーはメッセージを受信しません。

![ボットをブロックする](~/assets/images/bots/botdisable.png)

## <a name="remove-a-bot-from-a-team"></a>チームからボットを削除する

ユーザーは、チームのビューにあるボットの一覧でごみ箱アイコンを選択することで、ボットを削除できます。 これにより、そのチームの使用からボットのみが削除されます。 個々のユーザーは、個人的なコンテキストで対話できます。 個人用コンテキストのボットは、ユーザーが無効にしたり削除したりすることはできません。

## <a name="disable-a-bot-in-teams"></a>Teams でボットを無効にする

ボットがメッセージを受信するのを停止するには、**ボット ダッシュボード** に移動し、Microsoft Teams チャネルを編集します。 **[Microsoft Teams で有効にする]** オプションをオフにします。 これにより、ユーザーはボットと対話できなくなりますが、検出は可能であり、ユーザーはボットをチームに追加できます。

## <a name="delete-a-bot-from-teams"></a>Teams からボットを削除する

Teams からボットを完全に削除するには、**ボット ダッシュボード** に移動し、Teams チャネルを編集します。 ページの下部にある **[削除]** をクリックします。 これにより、ユーザーがボットを検出、追加、および操作できなくなります。 これにより、他のユーザーの Teams インスタンスからボットが削除されることはありませんが、ボットの機能も停止します。

## <a name="see-also"></a>関連項目

* [検査ミドルウェアでボットのデバッグを行う](/azure/bot-service/bot-service-debug-inspection-middleware)
* [ローカルで呼び出しや会議用ボットのデバッグを行う](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
