---
title: 詳細なリンクを作成する
description: 詳細なリンクとアプリでの使用方法について説明します。
keywords: teams ディープリンクディープリンク
ms.openlocfilehash: a3d5dac3fc83510ae47d91bd70390b9ca2860120
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552564"
---
# <a name="create-deep-links-to-content-and-features-in-microsoft-teams"></a>Microsoft Teams のコンテンツと機能への詳細なリンクを作成する

Teams クライアント内の情報と機能へのリンクを作成できます。 この例は、役に立ちます。

* アプリのタブのいずれか内のコンテンツにユーザーを移動します。 たとえば、アプリには、重要なアクティビティをユーザーに通知するメッセージを送信する bot がある場合があります。 ユーザーが通知をタップすると、ディープリンクがタブに移動し、ユーザーがアクティビティの詳細を表示できるようになります。
* アプリでは、必要なパラメーターでディープリンクを事前に設定することによって、チャットの作成、会議のスケジュール設定など、特定のユーザータスクを自動化または簡素化します。 これにより、ユーザーが情報を手動で入力する必要がなくなります。

> [!NOTE]
>
> ディープリンクは、ブラウザーを最初に起動してから、次のようにコンテンツと情報に移動します。
>
> **Tab**:  
> ✔、ディープリンクの url に直接移動します。
>
> **Bot**:  
> [カード本文にディープリンクを✔します。最初にブラウザーで開きます。  
> アダプティブカードで OpenURL アクションに追加されたディープリンク✔は、ディープリンク url に直接移動します。  
> ✔ハイパーリンク markdown をカードに入力します。最初にブラウザーで開きます。  
>
> **チャット**:  
> ✔テキストメッセージのハイパーリンク markdown: ディープリンク url に直接移動します。  
> 一般的なチャットの会話に貼り付けられた✔リンク-ディープリンクの url に直接移動します。

## <a name="deep-linking-to-your-tab"></a>タブへの詳細なリンク

Teams のエンティティへの詳細なリンクを作成できます。 通常、これは、タブ内のコンテンツと情報に移動するリンクを作成するために使用されます。たとえば、タブにタスクリストが含まれている場合は、チームメンバーが個々のタスクへのリンクを作成して共有することがあります。 このリンクをクリックすると、特定の項目を中心とするタブに移動します。 これを実装するには、UI に最適な方法で、各アイテムに "リンクのコピー" アクションを追加します。 ユーザーがこのアクションを実行すると、を呼び出して、 `shareDeepLink()` クリップボードにコピーできるリンクを含むダイアログボックスを表示します。 この呼び出しを行うと、アイテムの ID も渡されます。この ID は、リンクの後に tab キーが再読み込みされたときに [コンテキスト](~/tabs/how-to/access-teams-context.md) に戻されます。

または、このトピックで後述する形式を使用して、プログラムによってディープリンクを生成することもできます。 これらのメッセージを [ボット](~/bots/what-are-bots.md) および [コネクタ](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) メッセージで使用して、タブの変更やその中のアイテムについてユーザーに通知することができます。

> [!NOTE]
> これは、[ **リンクのリンク] タブ** メニュー項目で提供されるリンクとは異なり、このタブをポイントするディープリンクのみを生成します。

>[!NOTE]
> 現時点では、モバイルプラットフォームでは、この機能は使用できません。

### <a name="showing-a-deep-link-to-an-item-within-your-tab"></a>タブ内のアイテムへの詳細なリンクを表示する

タブ内のアイテムへの詳細なリンクを含むダイアログボックスを表示するには、 `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })`

次のフィールドを指定します。

* `subEntityId`&emsp;タブ内で詳細にリンクしているアイテムの一意識別子。
* `subEntityLabel`&emsp;ディープリンクの表示に使用するアイテムのラベル
* `subEntityWebUrl`&emsp;クライアントがタブのレンダリングをサポートしていない場合に使用するフォールバック URL を含むオプションフィールド

### <a name="generating-a-deep-link-to-your-tab"></a>タブに詳細なリンクを生成する

> [!NOTE]
> 静的タブのスコープは "personal" で、構成可能なタブの範囲は "team" です。 2つのタブの種類の構文は、構成可能なタブだけに `channel` コンテキストオブジェクトに関連付けられているプロパティがあるため、構文が若干異なります。 個人とチームのスコープの詳細については、「 [マニフェスト](~/resources/schema/manifest-schema.md) リファレンス」を参照してください。
> [!NOTE]
> ディープリンクは、タブが v2.0 以降のライブラリを使用して構成されている場合にのみ正しく機能し、そのためにはエンティティ ID を持っている必要があります。 エンティティ Id のないタブへの深いリンクは、タブに移動しますが、サブエンティティ ID をタブに提供することはできません。

Bot、コネクタ、またはメッセージング拡張カードで使用できるディープリンクには、次の形式を使用します。

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> Bot がディープリンクを持つを含むメッセージを送信する場合、 `TextBlock` ユーザーがリンクを選択すると、新しいブラウザータブが開きます。 これは、Chrome と Microsoft Teams デスクトップアプリ (どちらも Linux で実行されている) で発生します。
> Bot が同じディープリンク URL をに送信した場合、 `Action.OpenUrl` ユーザーがリンクをクリックすると、現在のブラウザタブで Teams タブが開きます。 新しいブラウザータブは開かれません。

クエリパラメーターは次のとおりです。

* `appId`&emsp;マニフェストからの ID。たとえば、"fe4a8eba-2a31-4737-8e33-e5fae6fee194" のようになります。
* `entityId`&emsp;タブ内のアイテムの ID。タブを [構成](~/tabs/how-to/create-tab-pages/configuration-page.md)するときに指定します。たとえば、"tasklist123" のようになります。
* `entityWebUrl`または、 `subEntityWebUrl` &emsp; クライアントがタブのレンダリングをサポートしていない場合に使用するフォールバック URL を持つオプションフィールド。たとえば、" https://tasklist.example.com/123 " または " https://tasklist.example.com/list123/task456 "
* `entityLabel`または、 `subEntityLabel` &emsp; タブ内のアイテムのラベルを使用して、ディープリンクを表示するときに使用します。たとえば、"タスクリスト 123" や "タスク 456" などです。
* `context`&emsp;次のフィールドを含む JSON オブジェクト。
  * `subEntityId`&emsp;タブ _内_ のアイテムの ID。たとえば、"task456" のようになります。
  * `channelId`&emsp;Microsoft Teams channel ID (タブ [コンテキスト](~/tabs/how-to/access-teams-context.md)から使用可能)。たとえば、"19: cbe3683f25094106b826c9cada3afbe0@thread" です。 このプロパティは、範囲が "team" である構成可能なタブでのみ使用できます。 これは、スコープが "personal" である静的タブでは使用できません。

例:

* 構成可能なタブ自体にリンクします。 `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* [構成可能] タブ内のタスクアイテムへのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* 静的タブ自体にリンクします。 `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`
* [静的] タブ内のタスクアイテムにリンクします。 `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`

> [!IMPORTANT]
> すべてのクエリパラメーターが正しい URI エンコードになっていることを確認します。 読みやすくするために、上記の例は含まれていませんが、指定する必要があります。 最後の例を使用します。
> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consuming-a-deep-link-from-a-tab"></a>タブからのディープリンクの使用

深いリンクに移動すると、Microsoft Teams は単にタブに移動し、Microsoft Teams の JavaScript ライブラリを使用して、サブエンティティ ID (存在する場合) を取得するためのメカニズムを提供します。

この [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) 呼び出しは、 `subEntityId` ディープリンクを介してタブが移動された場合に、フィールドを含むコンテキストを返します。

## <a name="deep-linking-from-your-tab"></a>タブからの詳細なリンク

タブから Teams のコンテンツにディープリンクすることができます。これは、チャネル、メッセージ、別のタブなど、Teams の他のコンテンツにリンクする必要がある場合や、スケジュール設定ダイアログを開く場合にも役立ちます。 タブからディープリンクを開始するには、次のように呼び出します。

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

これにより、正しい URL に移動するか、スケジュール設定またはアプリのインストールダイアログを開くなど、クライアントの動作を開始することができます。 例:

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a>チャットへの詳細なリンク

参加者のセットを指定することによって、ユーザー間のプライベートチャットへの詳細なリンクを作成できます。 指定した参加者のチャットが存在しない場合、リンクによってユーザーは空の新しいチャットに移動されます。 新しいチャットは、ユーザーが最初のメッセージを送信するまで下書き状態で作成されます。 必要に応じて、チャットの名前 (まだ存在しない場合)、およびユーザーの新規作成ボックスに挿入するテキストを指定できます。 この機能は、ユーザーが手動でチャットに移動したり、メッセージを入力したりする操作を実行するためのショートカットと考えることができます。

ユースケースの例として、ボットから Office 365 ユーザープロファイルをカードとして返す場合、このディープリンクを使用すると、その人物と簡単にチャットすることができます。

### <a name="generating-a-deep-link-to-a-chat"></a>チャットへの詳細なリンクの生成

Bot、コネクタ、またはメッセージング拡張カードで使用できるディープリンクには、次の形式を使用します。

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

例: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

クエリパラメーターは次のとおりです。

* `users`&emsp;チャットの参加者を表すユーザー Id のコンマ区切りのリスト。 アクションを実行するユーザーは、常に参加者として含まれます。 現時点では、ユーザー ID フィールドは Azure AD UserPrincipalName のみをサポートしています (通常はメールアドレス)。
* `topicName`&emsp;3人以上のユーザーとチャットする場合は、チャットの表示名のオプションフィールド。 このフィールドが指定されていない場合、チャットの表示名は参加者の名前に基づきます。
* `message`&emsp;現在のユーザーの新規作成ボックスに挿入するメッセージテキストのオプションフィールドで、チャットは下書きの状態になっています。

この深いリンクを bot と組み合わせて使用するには、カードのボタンの URL のターゲットとしてこれを指定するか、アクションの種類の [アクション] をタップし `openUrl` ます。

## <a name="linking-to-the-scheduling-dialog"></a>[スケジュール] ダイアログにリンクする

> [!Note]
> この機能は現在、開発者向けプレビューに含まれています。

Teams クライアントの組み込みのスケジュールダイアログへの詳細なリンクを作成できます。 これは、ユーザーが予定表またはスケジュール関連のタスクを完了するのにアプリが役立つ場合に特に便利です。

### <a name="generating-a-deep-link-to-the-scheduling-dialog"></a>スケジュールダイアログへの詳細なリンクの生成

Bot、コネクタ、またはメッセージング拡張カードで使用できるディープリンクには、次の形式を使用します。 `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

例: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

クエリパラメーターは次のとおりです。

* `attendees`&emsp;会議の出席者を表すユーザー Id のコンマ区切りリスト (オプション)。 アクションを実行するユーザーは、会議の開催者です。 現時点では、ユーザー ID フィールドは Azure AD UserPrincipalName のみをサポートしています (通常はメールアドレス)。
* `startTime`&emsp;イベントのオプションの開始時刻。 これは、"2018-03-12T23:55:25 + 02:00" のような [長い ISO 8601 形式](https://en.wikipedia.org/wiki/ISO_8601)にする必要があります。
* `endTime`&emsp;イベントのオプションの終了時刻 (ISO 8601 形式の場合もあります)。
* `subject`&emsp;会議の件名のオプションフィールド。
* `content`&emsp;会議の詳細フィールドのオプションフィールド。

現在、場所を指定することはサポートされていません。 開始時刻と終了時刻を生成するときは、必ず UTC オフセット (タイムゾーン) を指定してください。

この深いリンクを bot と組み合わせて使用するには、カードのボタンの URL のターゲットとしてこれを指定するか、アクションの種類の [アクション] をタップし `openUrl` ます。
