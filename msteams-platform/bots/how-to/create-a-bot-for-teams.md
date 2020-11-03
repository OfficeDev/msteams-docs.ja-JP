---
title: App Studio を使用してボットを作成する
author: clearab
description: App Studio を使用して Microsoft Teams ボットを作成する方法について説明します。
ms.topic: conceptual
localization_priority: Priority
ms.author: anclear
ms.openlocfilehash: 3d4f954afd56bf6ee442b57961c9d6b736ffa4d8
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796352"
---
# <a name="create-a-bot-using-app-studio"></a>App Studio を使用してボットを作成する

> [!TIP]
> すばやく開始する方法をお探しですか? Microsoft Teams のツールキットを使用して[ボット](../../build-your-first-app/build-bot.md)を作成する。

会話ボットを作成するには、次の手順を実行する必要があります。

1. 開発環境を準備する。
1. Web サービスを作成する。
1. Microsoft Bot Framework に Web サービスをボットとして 登録する。
1. アプリ マニフェストとアプリ パッケージを作成する。
1. Microsoft Teams にパッケージをアップロードする。

Bot Framework に対する Web サービスの作成、Web サービスの登録、およびアプリ パッケージの作成はどの順番で行っても構いません。ただし、これらの 3 つの要素は互いに深く絡み合っているため、実行する順番に関わらず、1 つ実行するごとに Bot Framework に戻り、他 2 つを更新する必要があります。 登録するには展開した Web サービスからのメッセージング エンドポイントが必要で、Web サービスでは登録時に作成した ID とパスワードが必要です。 また、アプリ マニフェストでは、Teams を Web サービスに接続するために登録 ID が必要です。

ボットの作成中は、アプリ マニフェストの変更と Web サービスへのコードの展開の間を頻繁に行き来することになります。 アプリ マニフェストで作業する際は、JSON ファイルを手動で変更することも、App Studio を使用して変更することもできるということを覚えておいてください。 いずれの場合も、マニフェスに変更を加えた際はアプリを Teams に再展開 (アップロード) する必要があります。ただし、変更を Web サービスに展開する場合は、これを行う必要はありません。

Bot Framework の詳細については、「[Bot Framework のドキュメント](/azure/bot-service/)」を参照してください。

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a>Web サービスを作成する

ボットで一番重要なのは、Web サービスです。 すべての要求を受信する単一のルート (通常は `/api/messages`) が Web サービスにより定義されます。 作成を開始する際に選ぶことができる選択肢がいくつかあります。

* [C#/dotnet](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot) または [JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) のいずれかの Teams 会話ボット サンプルを使用して開始します。
* JavaScript を使用している場合は、[Microsoft Teams 用 Yeoman ジェネレーター](https://github.com/OfficeDev/generator-teams)を使用して、Web サービスを含む、Teams アプリをスキャフォールドします。 これは、会話ボット以外のコンポーネントも含まれる Team アプリを構築する場合に特に役立ちます。
* Web サービスを一から作成する。 お使いの言語用の Bot Framework SDK を追加することも、JSON ペイロードに対して直接作業を行うこともできます。

## <a name="register-your-web-service-with-the-bot-framework"></a>Web サービスを Bot Framework に登録する

> [!IMPORTANT]
> Web サービスを登録する際は、 **表示名** を、アプリ マニフェストで使用した **短い名前** と必ず同じ名前にします。 直接のアップロードまたは組織のアプリ カタログ経由でのアップロードのいずれかの方法でアプリを発行すると、ボットにより会話に送信されるメッセージでは、アプリの **短い名前** ではなく、登録時の **表示名** がボットにより使用されます。

Web サービスを Bot Framework に登録することで、Teams クライアントと Web サービスの間に安全な通信チャネルが提供されます。 Teams クライアントと Web サービスが直接通信することはありません。 代わりに、メッセージは Bot Framework サービス経由でルーティングされます (Microsoft Teams では、このサービスの、Office 365 の基準に準拠する別のインスタンスが使用されます)。

Web サービスを Bot Framework に登録するときは、2 つの選択肢があります。 Azure サブスクリプションを使用せずに、[App Studio](#using-app-studio) または[従来のポータル](#in-the-legacy-portal)のいずれかを使用してボットを登録できます。 または、Azure サブスクリプションがすでにある (または取得するつもりの) 場合は、[Azure ポータル](#with-an-azure-subscription)を使用して Web サービスを登録できます。 

### <a name="without-an-azure-subscription"></a>Azure サブスクリプションがない場合

ボットの登録を Azure で作成しない場合は、こちらのリンク (https://dev.botframework.com/bots/new) または App Studio のいずれかを使用する **必要があります** 。 Bot Framework ポータルで [ *ボットを作成* ] ボタンをクリックすると Microsoft Azure にボット登録が作成され、Azure サブスクリプション情報の提供を求められます。 登録の管理を行う場合、または登録作成後に登録を Azure サブスクリプションに移動する場合は、https://dev.botframework.com/bots にアクセスします。

Azure に登録されていない既存の Bot Framework 登録のプロパティを編集すると、[移行の状態] 列と、Microsoft Azure ポータルに移動するための [移行] ボタンが表示されます。 意図する場合を除き、[移行] ボタンは選択しないでください。 代わりに、ボットの [ **名前** ] を選択し、そのプロパティを編集できます。

   ![ボットのプロパティを編集する](~/assets/images/bots/bf-migrate-bot-to-azure.png)

ボットを Azure で登録 (Azure ポータルでの登録作成または移行のいずれかの方法で) する **必要がある** シナリオ: 

* Bot Framework の [OAuthPrompt](./authentication/auth-flow-bot.md) を認証に使用する場合。
* Web チャット、Direct Line、または Skype などの追加のチャネルを有効にする場合。

#### <a name="using-app-studio"></a>App Studio を使用する場合

*App Studio* は Teams アプリの構築に役立つ Teams アプリケーションです。これを使用して Web サービスをボットとして登録、アプリ マニフェストやアプリ パッケージの作成、設定や構成の更新などができます。 React 制御ライブラリとカード用の構成可能なサンプルも含まれています。 「[Teams App Studio を使う](../../concepts/build-and-test/app-studio-overview.md)」を参照してください。

繰り返しますが、App Studio を使用して Web サービスを登録する場合は、https://dev.botframework.com/bots にアクセスして登録を管理する必要があります。

#### <a name="in-the-legacy-portal"></a>従来のポータルを使用する場合

ボットの登録を、こちらのリンク (https://dev.botframework.com/bots/new) を使用して作成します。 **ボットの作成後は必ず、おすすめのチャネル一覧に Microsoft Teams をチャネルとして登録します。** アプリ パッケージまたはマニフェストを既に作成した場合は、生成した Microsoft App ID はどれでも再利用できます。

   ![Bot Framework の登録ページ](~/assets/images/bots/bfregister.png)

### <a name="with-an-azure-subscription"></a>Azure サブスクリプションがある場合

Web サービスは、Azure ポータルでボット チャネル登録リソースを作成する方法でも登録できます。

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

[Bot Framework ポータル](https://dev.botframework.com)は、Microsoft Azure でのボットの登録に最適化されています。 留意事項がいくつかあります。

* Azure で登録したボット用の Microsoft Teams チャネルは **無料** です。 Teams チャネル経由で送信されるメッセージは、ボットの消費メッセージとしてはカウントされません。
* Microsoft Azure を使用してボットを登録する場合、ボット コードは Microsoft Azure で *ホスト* される必要はあります。
* Microsoft Azure ポータルを使用してボットを登録する場合は、Microsoft Azure アカウントを持っている必要があります。 このアカウントは[無料で作成](https://azure.microsoft.com/free/)できます。 Azure アカウントを作成するときは、ユーザーの ID を確認するためにユーザーはクレジット カードを提供する必要がありますが、課金はされません。Microsoft Teams を使用してのボットの作成と使用は常に無料です。

## <a name="create-your-app-manifest-and-package"></a>独自のアプリ マニフェストとアプリ パッケージを作成する

[アプリ マニフェスト](~/resources/schema/manifest-schema.md)により、アプリのメタデータ、アプリが使用する拡張点、これらの拡張点の接続先の Web サービスへのポインターが定義されます。 アプリ マニフェストは、App Studio を使用して作成することも、手動で作成することもできます。

### <a name="add-using-app-studio"></a>App Studio を使用して追加する

1. Teams クライアントで、左側のナビゲーション レールにあるオーバーフロー メニュー ( **...** ) から App Studio を開きます。 App Studio がまだインストールされていない場合は、それを検索してインストールできます。
2. On the [ **Manifest editor** ] (マニフェスト エディター) タブで、[ **Create a new app** ] (新しいアプリの作成) を選択します (または、ボットを既存のアプリに追加する場合は、アプリ パッケージをインポートできます)。
3. アプリの詳細情報を入力します (各フィールドの詳細な説明については、「[マニフェスト スキーマの定義](~/resources/schema/manifest-schema.md)」を参照してください)。
4. [ **Bots** ] (ボット) タブで、[ **セットアップ** ] (セットアップ) ボタンを選択します。
5. 新しい Web サービス登録を作成することも ([ **New bot** ] (新しいボット))、既に登録したものがある場合は、[ **Existing bot** ] (既存のボット) を選択することもできます。
6. ボットで必要な機能とスコープを選択します。
7. 必要に応じて、ボット エンドポイント アドレスを変更して、ボットにポイントします。 だいたい次のようになります: `https://someplace.com/api/messages`
8. 必要に応じて、[ボット コマンド](~/bots/how-to/create-a-bot-commands-menu.md)を追加します。
9. 必要な場合、完成したアプリ パッケージを [ **Test and distribute** ] (テストと発行) タブからダウンロードできます。

### <a name="create-it-manually"></a>手動で作成する

メッセージング拡張機能やタブの場合と同様、ボットを定義するには [app-manifest](~/resources/schema/manifest-schema.md) を更新します。 `bots` プロパティを使用して、新しいトップレベル の JSON 構造をアプリ マニフェストに追加します。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`botId`|String|64 文字|✔|Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。 これは、全体的なアプリ ID と同じにすることができます。|
|`needsChannelSelector`|Boolean|||ボットを特定のチャネルに追加するためのユーザー用ヒントをボットで使用するかどうかの説明。 既定値: `false`。|
|`isNotificationOnly`|Boolean|||ボットが会話ボットではなく、一方向性の通知専用ボットなのかどうかを示します。 既定値: `false`。|
|`supportsFiles`|Boolean|||パーソナル チャットでのファイルのアップロード/ダウンロード機能をボットでサポートするかどうかを示します。 既定値: `false`。|
|`scopes`|列挙型の配列|3|✔|ボットがエクスペリエンスを提供するのは、`team` 内のチャネルのコンテキスでなのか、グループ チャット (`groupchat`) でなのか、あるいは個別のユーザーのみをエクスペリエンスの対象にする (`personal`) のかを指定します。 これらのオプションは非排他的です。|

必要に応じて、ボットがユーザーに勧めることが可能なコマンド リスト (1 つまたは複数) を定義できます。 オブジェクトは配列で (要素は最大で 2 つ)、`object` タイプのすべての要素が含まれます。 ボットがサポートする各スコープについて、個別のコマンド リストを定義する必要があります。  詳細については、「[ボット メニュー](./create-a-bot-commands-menu.md)」を参照してください。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`items.scopes`|列挙型の配列|3|✔|コマンド リストが有効なスコープを指定します。 `team`、`personal`、`groupchat` の中から選択できます。|
|`items.commands`|オブジェクトの配列|10|✔|ボットがサポートするコマンドの配列:<br>`title`: ボット コマンドの名前 (文字列、32)<br>`description`: コマンドの構文およびその構文の引数
の簡単な説明または例 (文字列、128)|

#### <a name="simple-manifest-example"></a>マニフェストの簡単な例

次の例は単純なボット オブジェクトで、2 つのコマンド リストが定義されています。 これは、アプリ マニフェスト ファイルの全体ではなく、メッセージング拡張機能に関わる部分のみです。

```json
...
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "scopes": [ "team", "personal", "groupchat" ],
      "supportsFiles": true,
      "commandLists": [
        {
          "scopes": [ "team", "groupchat" ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command N",
              "description": "Description of Command N"
            }
          ]
        },
        {
          "scopes": [ "personal", "groupchat" ],
          "commands": [
            {
              "title": "Personal command 1",
              "description": "Description of Personal command 1"
            },
            {
              "title": "Personal command N",
              "description": "Description of Personal command N"
            }
          ]
        }
      ]
    }
  ],
...
```

#### <a name="create-your-app-package-manually"></a>アプリ パッケージを手動で作成する

アプリ パッケージを作成するには、アプリ マニフェストと (必要に応じて) アプリ アイコンを .zip アーカイブ ファイルに追加する必要があります。 詳細については、「[アプリ パッケージを作成する](~/concepts/build-and-test/apps-package.md)」を参照してください。 .zip アーカイブには必要なファイルのみを含めるようにし、アーカイブ内にフォルダー構造が何もないことを確認します。

## <a name="upload-your-package-to-microsoft-teams"></a>Microsoft Teams にアプリ パッケージをアップロードする

> [!NOTE]
> ボットを正常にアップロードするには、テナント管理者が最初にサードパーティまたはカスタムのアプリを Teams に[アップロードすることを許可](/microsoftteams/manage-apps#manage-org-wide-app-settings)する必要があります。

App Studio を使用した場合は、[ **Manifest editor** ] (マニフェスト エディター) の [ **Test and distribute** ] (テストと発行) タブからアプリをインストールできます。 また、左側のオーバーフロー メニュー (`...`) をクリックし、[ **その他のアプリ** ] をクリックし、[ **カスタム アプリをアップロード** ] リンクをクリックする方法でもアプリ パッケージをインストールすることができます。 アプリ マニフェストまたはアプリ パッケージを App Studio にインポートして、アップロードする前に追加の更新を行うこともできます。

## <a name="bots-in-teams-meetings"></a>Teams 会議のボット

Teams は、会議中のボットの呼び出しをサポートしています。 ボットが呼び出しメッセージを受信すると、`userId` と `tenantId` からユーザーとテナントを識別できます。 `meetingId` は、`channelData` オブジェクトに含まれています。 ボットは、ユーザーの役割を取得するために `GetParticipant` API 要求に対して、`userId` と `meetingId` を使用できます。

## <a name="next-steps"></a>次の手順

* [ボット会話の基本](./conversations/conversation-basics.md)
* [会話イベントにサブスクライブする](./conversations/subscribe-to-conversation-events.md)
