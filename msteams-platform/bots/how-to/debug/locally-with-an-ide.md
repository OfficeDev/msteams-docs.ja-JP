---
title: ボットをローカルでテストしてデバッグする
author: surbhigupta
description: サイドローディング、bot Emulator を使用したTeamsの外部、およびボットと直接会話することで、Teams環境内の IDE を使用してボットをローカルでテストしてデバッグする方法について説明します。
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: a673f1cd260c9b53de477cdd5084bd521c79bd41
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103987"
---
# <a name="test-and-debug-your-bot-locally"></a>ボットをローカルでテストしてデバッグする

ボットをテストする場合は、ボットを実行するコンテキストと、Microsoft Teamsに固有のデータを必要とするボットに追加した可能性のある機能の両方を考慮する必要があります。 ボットをテストするために選択した方法が、その機能と一致していることを確認します。

## <a name="test-by-uploading-to-teams"></a>Teamsにアップロードしてテストする

ボットをテストする最も包括的な方法は、アプリ パッケージを作成してTeamsにアップロードすることです。 これは、すべてのスコープでボットで使用できる完全な機能をテストする唯一の方法です。

アプリをアップロードするには、次の 2 つの方法があります。

* [App Studio を使用します](~/concepts/build-and-test/app-studio-overview.md)。
* [アプリ パッケージを](~/concepts/build-and-test/apps-package.md) 手動で作成し、 [アプリをアップロードします](~/concepts/deploy-and-publish/apps-upload.md)。

> [!NOTE]
> マニフェストを変更してアプリを再アップロードするには、変更されたアプリ パッケージをアップロードする前に [ボットを削除](#delete-a-bot-from-teams) します。
> ボットをテストするには、Teamsでサイドローディングを有効にします。 [サイドローディングを有効にするを](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)参照してください。

## <a name="debug-your-bot-locally"></a>ボットをローカルでデバッグする

開発中にボットをローカルでホストしている場合は、ボットをテストするために [、ngrok](https://ngrok.com/) などのトンネリング サービスを使用する必要があります。 ngrok をダウンロードしてインストールした後、パスに追加 `ngrok` し、次のコマンドを実行してトンネリング サービスを開始します。

```bash
ngrok http <port> -host-header=localhost:<port>
```

アプリ マニフェストで ngrok によって提供される https エンドポイントを使用します。

> [!NOTE]
> コマンド ウィンドウを閉じて再起動すると、新しい URL が生成され、ボット エンドポイント アドレスを更新して使用する必要があります。

## <a name="test-your-bot-without-uploading-to-teams"></a>Teamsにアップロードせずにボットをテストする

場合によっては、Teamsでアプリとしてボットをインストールせずにボットをテストすることが必要になる場合があります。 ボットをテストするための 2 つの方法を提供します。 アプリとしてインストールせずにボットをテストすることは、ボットが使用可能で応答していることを確認するのに役立ちますが、ボットに追加した可能性のあるMicrosoft Teams機能の完全な幅をテストすることはできません。 ボットを完全にテストする必要がある場合は、 [アップロードによるテストを](#test-by-uploading-to-teams)参照してください。

### <a name="use-the-bot-emulator"></a>ボット Emulatorを使用する

Bot Framework Emulatorは、ボット開発者がローカルまたはリモートでボットをテストおよびデバッグできるようにするデスクトップ アプリケーションです。 エミュレーターは、ボットとチャットし、ボットが送受信するメッセージを調べるのに役立ちます。 これは、ボットが使用可能であることを確認し、応答する場合に便利です。 ただし、エミュレーターでは、ボットに追加したTeams固有の機能をテストすることはできません。また、ボットからの応答は、Teamsでのレンダリング方法を正確に視覚的に表すものではありません。 これらのいずれかをテストする必要がある場合は、 [ボットをアップロード](#test-by-uploading-to-teams)することをお勧めします。

詳細については、[Bot Framework Emulatorに関する完全な手順を](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)参照してください。

### <a name="talk-to-your-bot-directly-by-id"></a>ID で直接ボットに問い合わせてください

> [!Important]
> ID によるボットの会話は、基本的なテストのみを目的としています。 ボットに追加したTeams固有の機能は機能しません。

ID を使用してボットとの会話を開始することもできます。 これらの方法のいずれかを通じてボットが追加された場合、チャネルの会話ではアドレス指定できず、タブやメッセージ拡張機能などの他のMicrosoft Teamsアプリ機能を利用することはできません。 次のいずれかの方法で会話を開始できます。

* ボットの [[ボット ダッシュボード](https://dev.botframework.com/bots)] ページの [**チャネル**] で、[**Microsoft Teamsに追加]** を選択します。 Microsoft Teamsボットとの個人用チャットを開始します。

* Microsoft Teams内からボットのアプリ ID を直接参照します。
   1. ボットの [[ボット ダッシュボード]](https://dev.botframework.com/bots) ページの [ **詳細**] で、ボットの **Microsoft アプリ ID を** コピーします。
  
      ![ボットの AppID を取得する](~/assets/images/bots_appid_botframework.png)
  
   2. Microsoft Teamsを開き、[**チャット**] ウィンドウで [チャットの **追加**] アイコンを選択します。 **To:** に、ボットの Microsoft アプリ ID を貼り付けます。
  
      ![ボットのアップロード](~/assets/images/bots_uploading.png)

      アプリ ID はボット名に解決する必要があります。

   3. ボットを選択し、メッセージを送信して会話を開始します。
      または、Microsoft Teamsの左上にある検索ボックスにボットのアプリ ID を貼り付けることができます。 検索結果ページで 、[ **ユーザー** ] タブに移動してボットを表示し、チャットを開始します。

> [!Note]
> Microsoft Teamsボットのアプリ ID を参照するには、[アプリのサイドローディングを](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)有効にします。

ボットは、オブジェクト内の `conversationUpdate` チーム情報を含まないチームにボットを追加すると、イベントを `channelData` 受け取ります。

## <a name="block-a-bot-in-personal-chat"></a>個人用チャットでボットをブロックする

ユーザーは、ボットが個人用チャット メッセージを送信できないようにすることを選択できます。 チャット チャネルでボットを右クリックし、[ **ボットの会話をブロック**] を選択することで、これを切り替えることができます。 つまり、ボットは引き続きメッセージを送信しますが、ユーザーはメッセージを受信しません。

![ボットをブロックする](~/assets/images/bots/botdisable.png)

## <a name="remove-a-bot-from-a-team"></a>チームからボットを削除する

ユーザーは、チームのビューでボットリストのごみ箱アイコンを選択してボットを削除できます。 これにより、そのチームの使用からボットが削除されるだけで、個々のユーザーは個人のコンテキストで対話できます。 個人用コンテキストのボットは、ユーザーが無効にしたり削除したりすることはできません。

## <a name="disable-a-bot-in-teams"></a>Teamsでボットを無効にする

ボットがメッセージの受信を停止するには、**ボット ダッシュボード** に移動し、Microsoft Teams チャネルを編集します。 **[Microsoft Teamsで有効にする] オプションをオフにします**。 これにより、ユーザーはボットと対話できなくなりますが、引き続き検出可能であり、ユーザーはボットをTeamsに追加できます。

## <a name="delete-a-bot-from-teams"></a>Teamsからボットを削除する

Teamsからボットを完全に削除するには、**ボット ダッシュボード** に移動し、Microsoft Teams チャネルを編集します。 下部にある **[削除** ] ボタンを選択します。 これにより、ユーザーはボットを検出、追加、操作できなくなります。 これにより、他のユーザーのTeams インスタンスからボットが削除されることはありませんが、ボットの機能も停止します。

## <a name="see-also"></a>関連項目

* [検査ミドルウェアでボットのデバッグを行う](/azure/bot-service/bot-service-debug-inspection-middleware)
* [ローカルで呼び出しや会議用ボットのデバッグを行う](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
