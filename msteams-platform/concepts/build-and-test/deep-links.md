---
title: コンテンツへのディープ リンクを作成する
description: ディープ リンクとアプリでの使用方法について説明する
ms.topic: how-to
keywords: Teams ディープ リンク ディープリンク
ms.openlocfilehash: d6efe7332035320d2114e0e834d1c971ccc7108c
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231562"
---
# <a name="create-deep-links-to-content-and-features-in-microsoft-teams"></a>Microsoft Teams のコンテンツと機能へのディープ リンクを作成する

Teams 内の情報と機能へのリンクを作成できます。 ディープ リンクの作成が役立つ例を次に示します。

* アプリのいずれかのタブ内のコンテンツにユーザーを移動します。 たとえば、アプリは、重要なアクティビティをユーザーに通知するメッセージを送信するボットを持つ場合があります。 ユーザーが通知をタップすると、ディープ リンクがタブに移動し、ユーザーがアクティビティの詳細を表示できます。
* アプリは、必要なパラメーターを使用してディープ リンクを事前に入力して、チャットの作成や会議のスケジュール設定などの特定のユーザー タスクを自動化または単純化します。 これにより、ユーザーが手動で情報を入力する必要がなくなります。

> [!NOTE]
>
> ディープリンクは、次のようにコンテンツと情報に移動する前にブラウザーを最初に起動します。
>
> **タブ**:  
> ✔ ディープリンクの URL に直接移動します。
>
> **ボット**:  
> ✔ カード本文のディープリンク - ブラウザーを最初に開きます。  
> ✔ アダプティブ カードの OpenURL アクションに追加されたディープリンク - ディープリンクの URL に直接移動します。  
> ✔ カードのハイパーリンク マークダウン テキスト - ブラウザーを最初に開きます。  
>
> **チャット**  
> ✔ テキスト メッセージ ハイパーリンク マークダウン: ディープリンクの URL に直接移動します。  
> ✔ 一般的なチャット会話に貼り付けられたリンク - ディープリンクの URL に直接移動します。

## <a name="deep-linking-to-your-tab"></a>タブへのディープ リンクの設定

Teams のエンティティへのディープ リンクを作成できます。 通常、これは、タブ内のコンテンツと情報に移動するリンクを作成するために使用されます。たとえば、タブにタスク リストが含まれている場合、チーム メンバーは個々のタスクへのリンクを作成して共有できます。 リンクを選択すると、特定の項目に焦点を当てたタブに移動します。 これを実装するには、各アイテムに「リンクのコピー」アクションを UI に最適な方法で追加します。 このアクションを実行すると、 `shareDeepLink()` を呼び出して、ユーザーがクリップボードにコピーできるリンクを含むダイアログボックスを表示します。 この呼び出しを行うと、アイテムの ID も渡されます。この ID は、リンクに従って、タブを再読み込みするとき、[コンテキスト](~/tabs/how-to/access-teams-context.md)に戻されます。

または、このトピックで後述する形式を使用して、プログラミングして、ディープ リンクを作成することもできます。 これらは、タブまたはタブ[](~/bots/what-are-bots.md)内の[](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)アイテムに対する変更をユーザーに通知するボットおよびコネクタ メッセージで使用できます。

> [!NOTE]
> このディープ リンクは、[タブへのリンクのコピー  ] メニュー項目によって提供されるリンクとは異なります。このメニュー項目は、このタブをポイントするディープ リンクを生成します。

>[!NOTE]
> 現在、shareDeepLinkは、モバイル プラットフォームでは機能しません。

### <a name="showing-a-deep-link-to-an-item-within-your-tab"></a>タブ内のアイテムへのディープ リンクを表示する

タブ内のアイテムへのディープ リンクを含むダイアログ ボックスを表示するには、`microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })` を呼び出します

次のフィールドを指定します。

* `subEntityId`&emsp;タブ内でディープ リンクを設定しているアイテムの一意の識別子
* `subEntityLabel`&emsp;ディープ リンクを表示するために使用するアイテムのラベル
* `subEntityWebUrl`&emsp;クライアントがタブのレンダリングをサポートしていない場合に使用する代替 URL を含むオプションのフィールド

### <a name="generating-a-deep-link-to-your-tab"></a>タブへのディープ リンクを作成する

> [!NOTE]
> [個人用] タブ `personal` には範囲が設定され、チャネルタブとグループ タブでは範囲 `team` が `group` 使用されます。 構成可能なタブだけがコンテキスト オブジェクトに関連付けられている `channel` プロパティを持つため、2 つのタブの種類の構文はわずかに異なります。 タブ スコープ [の詳細](~/resources/schema/manifest-schema.md) については、マニフェスト リファレンスを参照してください。

> [!NOTE]
> ディープ リンクは、タブが v0.4 以降のライブラリを使用して構成されていて、そのためエンティティ ID がある場合にのみ正常に機能します。 エンティティ ID のないタブへのディープ リンクは、タブに移動しますが、サブエンティティ ID をタブに提供できない。

ボット、コネクタ、またはメッセージング拡張機能カードで使用できるディープ リンクには、次の形式を使用します。

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> ボットがディープ リンクを使用して `TextBlock` を含むメッセージを送信する場合、ユーザーがリンクを選択すると、新しいブラウザー タブが開きます。 これは、Chrome および Microsoft Teams デスクトップ アプリ (いずれも Linux で実行されています) で発生します。
> ボットが同じディープ リンク URL を 1 つのページに送信する場合、ユーザーがリンクを選択すると、現在のブラウザー タブで `Action.OpenUrl` [Teams] タブが開きます。 新しいブラウザー タブは開きません。

クエリ パラメーターは次のとおりです。

* `appId`&emsp;マニフェストの ID。たとえば、「fe4a8eba-2a31-4737-8e33-e5fae6fee194」のようになります
* `entityId`&emsp;タブのアイテムの ID。[タブを構成する](~/tabs/how-to/create-tab-pages/configuration-page.md)ときに表示されます。たとえば、「tasklist123」のようになります
* `entityWebUrl` または `subEntityWebUrl`&emsp;クライアントがタブのレンダリングをサポートしていない場合に使用する代替 URL を含むオプションのフィールド。たとえば、「https://tasklist.example.com/123」または「https://tasklist.example.com/list123/task456」のようになります
* `entityLabel` または `subEntityLabel`&emsp;ディープ リンクを表示するときに使用するタブのアイテムのラベル。たとえば、「Task List 123」または「Task 456」のようになります
* `context`&emsp;次のフィールドを含む JSON オブジェクト。
  * `subEntityId`&emsp;タブ _内_ のアイテムの ID。たとえば、「task456」のようになります
  * `channelId`&emsp;タブ コンテキストから利用できる Microsoft Teams チャネル [ID。](~/tabs/how-to/access-teams-context.md)たとえば、「19:cbe3683f25094106b826c9cada3afbe0@thread.skype」とします。 このプロパティは、「チーム」の範囲を持つ構成可能なタブにのみ使用できます。 「個人」の範囲を持つ静的なタブでは使用できません。

例:

* 構成可能なタブ自体へのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* 構成可能なタブ内のタスク アイテムへのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* 静的なタブ自体へのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`
* 静的なタブ内のタスク アイテムへのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`

> [!IMPORTANT]
> すべてのクエリ パラメーターが適切に URI にエンコードされていることを確認します。 前の例に従って、最後の例を使用する必要があります。
> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consuming-a-deep-link-from-a-tab"></a>タブからディープ リンクを使用する

ディープ リンクに移動すると、Microsoft Teams はタブに移動するだけで、サブエンティティ ID が存在する場合は Microsoft Teams JavaScript ライブラリを介してサブエンティティ ID を取得するメカニズムを提供します。

この呼び出しは、タブがディープ リンクを介して移動する場合に、フィールドを含 [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) `subEntityId` むコンテキストを返します。

## <a name="deep-linking-from-your-tab"></a>タブからのディープ リンクの設定

タブから Teams のコンテンツにディープリンクできます。これは、タブが Teams の他のコンテンツ (チャネル、メッセージ、別のタブなど) にリンクする必要がある場合や、スケジュール ダイアログを開く場合に便利です。 タブからディープリンクをトリガーするには、次のように呼び出す必要があります。

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

この呼び出しは、正しい URL に移動するか、スケジュール設定やアプリのインストール ダイアログを開くなどのクライアント アクションをトリガーします。 次の例を参照してください。

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a>チャットへのディープ リンクの設定

参加者のセットを指定することで、ユーザー間のプライベート チャットへのディープ リンクを作成できます。 指定された参加者とチャットが存在しない場合、リンクは空の新しいチャットにユーザーを移動します。 ユーザーが最初のメッセージを送信するまで、新しいチャットは下書き状態で作成されます。 存在しない場合は、チャットの名前と、ユーザーの作成ボックスに挿入するテキストを指定できます。 この機能は、ユーザーがチャットに移動したり、チャットを参加したり、メッセージを入力したりする手動操作を行うためのショートカットとして考えることができます。

ユースケースの例として、ボットから Office 365 ユーザー プロファイルをカードとして返す場合、このディープ リンクを使用すると、ユーザーはそのユーザーと簡単にチャットできます。

### <a name="generating-a-deep-link-to-a-chat"></a>チェットへのディープ リンクを作成する

ボット、コネクタ、またはメッセージング拡張機能カードで使用できるディープ リンクには、次の形式を使用します。

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

例: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

クエリ パラメーターは次のとおりです。

* `users`: チャットの参加者を表すユーザー ID のコンマ区切りのリスト。 アクションを実行するユーザーは、常に参加者として含まれます。 現在、User ID フィールドは Azure AD UserPrincipalName (通常はメール アドレスのみ) をサポートしています。
* `topicName`: 3 名以上のユーザーとのチャットの場合、チャットの表示名のオプション フィールド。 このフィールドを指定しない場合、チャットの表示名は参加者の名前に基づいて設定されます。
* `message`: チャットが下書き状態の間に現在のユーザーの作成ボックスに挿入するメッセージ テキストのオプションのフィールドです。

ボットとのこのディープ リンクを使用するには、カードのボタンで URL を対象として指定するか、[ `openUrl` アクションの種類] で [アクション] をタップします。

### <a name="generating-a-deep-link-to-a-call"></a>通話へのディープ リンクの生成

ボット、コネクタ、またはメッセージング拡張機能カードで使用できるディープ リンクには、次の形式を使用します。

`https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>`

例: `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

クエリ パラメーターは次のとおりです。

* `users`: 通話の参加者を表すユーザー ID のコンマ区切りのリスト。 アクションを実行するユーザーは、常に参加者として含まれます。 現在、User ID フィールドは Azure AD UserPrincipalName (通常はメール アドレスのみ) をサポートしています。

## <a name="linking-to-the-scheduling-dialog"></a>スケジュール設定ダイアログへのリンクの設定

> [!Note]
> この機能は現在、開発者プレビュー段階です。

Teams の組み込みスケジュール ダイアログへのディープ リンクを作成できます。 これは、アプリがカレンダーやスケジュールに関連するタスクをユーザーに支援する場合に特に便利です。

### <a name="generating-a-deep-link-to-the-scheduling-dialog"></a>スケジュール設定ダイアログへのディープ リンクを作成する

ボット、コネクタ、またはメッセージング拡張機能カードで使用できるディープ リンクには、次の形式を使用します。 `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

例: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

クエリ パラメーターは次のとおりです。

* `attendees`: 会議の出席者を表すユーザー ID のコンマ区切りリスト (省略可能)。 アクションを実行するユーザーは、会議の開催者です。 User ID フィールドは現在、Azure AD UserPrincipalName (通常は電子メール アドレス) のみをサポートしています。
* `startTime`: イベントのオプションの開始時刻。 これは、[long ISO 8601 形式](https://en.wikipedia.org/wiki/ISO_8601)、たとえば、「2018-03-12T23:55:25+02:00」にする必要があります。
* `endTime`: イベントのオプションの終了時刻(ISO 8601 形式)。
* `subject`: 会議の件名の省略可能なフィールドです。
* `content`: 会議の詳細フィールドのオプションのフィールドです。

現在、場所の指定はサポートされていません。 UTC オフセットを指定する必要があります。これは、開始時刻と終了時刻を生成するときにタイム ゾーンを意味します。

ボットとのこのディープ リンクを使用するには、カードのボタンで URL を対象として指定するか、[ `openUrl` アクションの種類] で [アクション] をタップします。
