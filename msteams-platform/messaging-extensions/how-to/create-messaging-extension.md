---
title: Teams のメッセージング拡張機能を作成する
author: clearab
description: Teams メッセージング拡張機能を作成する方法について説明します。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 03fe4463f7e7af0874af4ce4f487f1a01fdd5fe6
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452597"
---
# <a name="create-a-messaging-extension-for-microsoft-teams"></a>Microsoft Teams のメッセージング拡張機能を作成する

> [!TIP]
> 開始するためのより迅速な方法をお探しですか。 Microsoft Teams ツールキットを使用して、 [メッセージング拡張機能](../../build-your-first-app/build-messaging-extension.md) を作成します。

高レベルでは、次の手順を実行してメッセージング拡張機能を作成する必要があります。

1. 開発環境を準備する
2. Web サービスを作成および展開する (ngrok のようなトンネリングサービスを使用してローカルに実行する)
3. Web サービスを Bot Framework に登録する
4. アプリ パッケージを作成する
5. Microsoft Teams にアプリ パッケージをアップロードする

Web サービスを作成し、アプリパッケージを作成し、web サービスを Bot フレームワークに登録するには、任意の順序で行うことができます。 これらの3つの要素は so intertwined なので、どの順序で実行するかにかかわらず、他の要素を更新するために戻る必要があります。 登録では、展開された web サービスのメッセージングエンドポイントが必要です。また、web サービスでは、登録から作成された Id とパスワードが必要です。 アプリマニフェストには、チームを web サービスに接続するための Id も必要です。

メッセージング拡張機能を構築している間は、アプリマニフェストの変更と web サービスへのコードの展開の間に定期的に移行します。 アプリマニフェストを操作するときは、JSON ファイルを手動で操作するか、アプリ Studio を使用して変更を行うことができることに注意してください。 どちらの方法でも、マニフェストを変更したときに Teams でアプリを再展開 (アップロード) する必要がありますが、変更を web サービスに展開するときには必要ありません。

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a>Web サービスを作成する

メッセージング拡張機能の核心部分は、web サービスです。 1つのルート (通常は、 `/api/messages` すべての要求を受信する) を定義します。 最初から作業を開始する場合は、いくつかのオプションから選択できます。

* Web サービスを作成するためのガイドとして、 [クイックスタート](#learn-more) チュートリアルの1つを使用します。
* [Bot フレームワークサンプルリポジトリ](https://github.com/Microsoft/BotBuilder-Samples)で使用可能なメッセージング拡張機能のサンプルの1つを選択し、開始します。
* JavaScript を使用している場合は、 [Microsoft teams 用の](https://github.com/OfficeDev/generator-teams) スキャフォールディングを使用して、web サービスを含む teams アプリを作成します。
* Web サービスを一から作成する。 お使いの言語用の Bot Framework SDK を追加することも、JSON ペイロードに対して直接作業を行うこともできます。

## <a name="register-your-web-service-with-the-bot-framework"></a>Web サービスを Bot Framework に登録する

メッセージング拡張機能は、Bot フレームワークのメッセージングスキーマとセキュリティで保護された通信プロトコルを利用します。まだお持ちでない場合は、ボットフレームワークに web サービスを登録する必要があります。 Microsoft App Id (Teams の内部から Bot Id として参照されている可能性があります)。また、要求に対する応答を受信して応答するために、ユーザーのメッセージング拡張機能でこの登録が使用されます。 既存の登録を使用している場合は、 [Microsoft Teams チャネルが有効に](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true)なっていることを確認してください。

クイックスタートのいずれかを実行した場合、または利用可能なサンプルのいずれかから開始した場合は、web サービスを登録することになります。 サービスを手動で登録する場合は、3つのオプションがあります。 Azure サブスクリプションを使用せずに登録することを選択した場合、Bot フレームワークによって提供される簡素化された OAuth 認証フローを利用することはできません。 作成後に、登録を Azure に移行することができます。

* Azure サブスクリプションを保有している場合 (または新しいサブスクリプションを作成する場合) は、Azure Portal を使用して web サービスを手動で登録できます。 "Bot チャネル登録" リソースを作成します。 無料料金層は、Microsoft Teams からのメッセージが1か月あたりの合計許容メッセージ数を超えないように、選択することができます。
* Azure サブスクリプションを使用しない場合は、 [従来の登録ポータル](https://dev.botframework.com/bots/new)を使用できます。
* アプリ Studio は、web サービス (bot) の登録にも役立ちます。 アプリ Studio によって登録された Web サービスが Azure に登録されていません。 [従来のポータル](https://dev.botframework.com/bots)を使用して、登録の表示、管理、移行を行うことができます。

## <a name="create-your-app-manifest"></a>アプリのマニフェストを作成する

アプリ マニフェストは、App Studio を使用して作成することも、手動で作成することもできます。

### <a name="create-your-app-manifest-using-app-studio"></a>アプリ Studio を使用してアプリマニフェストを作成する

アプリのマニフェストを作成するために、Microsoft Teams クライアント内からアプリ Studio アプリを使用することができます。

1. Teams クライアントで、左側のナビゲーション レールにあるオーバーフロー メニュー (**...**) から App Studio を開きます。 まだインストールされていない場合は、それを検索することができます。
2. [ **マニフェストエディター** ] タブで、[ **新しいアプリの作成** ] を選択します (または、既存のアプリにメッセージング拡張機能を追加している場合は、アプリパッケージをインポートできます)。
3. アプリの詳細情報を入力します (各フィールドの詳細な説明については、「[マニフェスト スキーマの定義](~/resources/schema/manifest-schema.md)」を参照してください)。
4. [ **メッセージング拡張機能** ] タブで、[ **セットアップ** ] ボタンをクリックします。
5. メッセージング拡張機能を使用する新しい web サービス (bot) を作成するか、または既に1つの選択/追加をここに登録していることを確認できます。
6. 必要に応じて、ボット エンドポイント アドレスを変更して、ボットにポイントします。 だいたい次のようになります: `https://someplace.com/api/messages`
7. **コマンド**セクションの [**追加**] ボタンを使用すると、メッセージング拡張機能にコマンドを追加できます。 コマンドの追加の詳細については、「 [詳細](#learn-more) 情報」セクションを参照してください。 メッセージング拡張機能には最大10個のコマンドを定義できます。
8. [ **メッセージハンドラ** ] セクションでは、メッセージングがトリガーされるドメインを追加できます。 詳細については、「 [link unfurling](~/messaging-extensions/how-to/link-unfurling.md) 」を参照してください。

**[完了] => [テストと配布**] タブで、アプリパッケージ (アプリのマニフェストやアプリのアイコンを含む) を**ダウンロード**したり、パッケージを**インストール**したりできます。

### <a name="create-your-app-manifest-manually"></a>アプリのマニフェストを手動で作成する

ボットやタブの場合と同様に、メッセージング拡張機能のプロパティを含むようにアプリの [アプリマニフェスト](~/resources/schema/manifest-schema.md#composeextensions) を更新します。 これらのプロパティは、Microsoft Teams クライアントでメッセージング拡張機能がどのように表示され、動作するかを制御します。 メッセージング内線番号は、マニフェストの v 1.0 以降でサポートされています。

#### <a name="declare-your-messaging-extension"></a>メッセージング拡張機能を宣言する

メッセージング拡張機能を追加するには、プロパティを使用して、アプリマニフェストに新しいトップレベルの JSON 構造を含め `composeExtensions` ます。 アプリに対して1つのメッセージング拡張機能を作成します。これには最大10個のコマンドがあります。

> [!NOTE]
> マニフェストは、としてメッセージング拡張機能を参照し `composeExtensions` ます。 これは、下位互換性を維持するためのものです。

拡張機能の定義は、次の構造を持つオブジェクトです。

| プロパティ名 | 用途 | 必須 |
|---|---|---|
| `botId` | Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。 これは通常、Teams アプリ全体の ID と同じである必要があります。 | 必要 |
| `canUpdateConfiguration` | **設定**メニュー項目を有効にします。 | いいえ |
| `commands` | このメッセージング拡張機能がサポートするコマンドの配列です。 コマンドは10個に制限されています。 | 必要 |

#### <a name="define-your-commands"></a>コマンドを定義する

メッセージング拡張機能では、1つまたは複数のコマンドを宣言します。これにより、ユーザーがメッセージング拡張機能をトリガーする場所、および対話の種類が定義されます。 メッセージング拡張機能のコマンドの詳細につい [ては、「詳細情報](#learn-more) 」を参照してください。

#### <a name="simple-manifest-example"></a>マニフェストの簡単な例

次の例では、検索コマンドを使用して、アプリマニフェストの単純なメッセージング拡張オブジェクトを示します。 これは、アプリ マニフェスト ファイルの全体ではなく、メッセージング拡張機能に関わる部分のみです。 完全な例については、「 [app manifest schema](~/resources/schema/manifest-schema.md) 」を参照してください。

```json
...
"composeExtensions": [
  {
    "botId": "abcd1234-1fc5-4d97-a142-35bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "searchCmd",
        "description": "Search you ToDo's",
        "title": "Search",
        "initialRun": true,
        "parameters": [
          {
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }
        ]
      }
    ]
  }
]
...
```

## <a name="add-your-invoke-message-handlers"></a>呼び出しメッセージハンドラーを追加する

ユーザーがメッセージング拡張機能をトリガーする場合は、最初の呼び出しメッセージを処理し、ユーザーから情報を収集し、その情報を処理して適切に応答する必要があります。 そのためには、まずメッセージング拡張機能に追加するコマンドの種類を決定し、 [アクションコマンドを追加](~/messaging-extensions/how-to/action-commands/define-action-command.md) するか、 [検索コマンドを追加](~/messaging-extensions/how-to/search-commands/define-search-command.md)する必要があります。

## <a name="messaging-extensions-in-teams-meetings"></a>Teams 会議でのメッセージング拡張機能

会議が開始されると、チームの参加者は、live 呼び出しの間にメッセージング拡張機能と直接対話できます。 会議でのメッセージング拡張機能を構築する場合は、次の点を考慮してください。

1. **Location**。 メッセージング拡張機能は、会議チャットの [メッセージの作成] 領域、コマンドボックス、または @mentioned から呼び出すことができます。

1. **メタデータ**。 メッセージング拡張機能が呼び出されると、との間でユーザーとテナントを識別できるようになり `userId` `tenantId` ます。 `meetingId` は、`channelData` オブジェクトに含まれています。 アプリでは、および API 要求にを使用して、 `userId` `meetingId`  ユーザーの役割を取得でき `GetParticipant` ます。

1. **コマンドの種類**。 メッセージ拡張機能が [アクションベースのコマンド](../../messaging-extensions/what-are-messaging-extensions.md#action-commands)を使用している場合は、タブ [シングルサインオン](../../tabs/how-to/authentication/auth-aad-sso.md) 認証に従う必要があります。

1. **ユーザーの利便性**。 会議チャット中に呼び出されるメッセージング拡張機能のエンドユーザーの環境を決定する必要があります。

## <a name="next-steps"></a>次の手順

* [アクションコマンドを作成する](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [検索コマンドを作成する](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [リンク展開](~/messaging-extensions/how-to/link-unfurling.md)

## <a name="learn-more"></a>詳細情報

クイックスタートで試してみる:

* C のクイックスタート#
  * [アクションベースのコマンドを使用したメッセージング拡張機能](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [検索ベースのコマンドを使用したメッセージング拡張機能](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* JavaScript のクイックスタート
  * [アクションベースのコマンドを使用したメッセージング拡張機能](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [検索ベースのコマンドを使用したメッセージング拡張機能](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

メッセージング拡張機能の概要について説明します。

* [Teams アプリの機能を理解する](~/concepts/extensibility-points.md)
* [メッセージング拡張機能とは](~/messaging-extensions/what-are-messaging-extensions.md)
