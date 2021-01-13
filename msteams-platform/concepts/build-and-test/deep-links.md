---
title: コンテンツへのディープ リンクを作成する
description: ディープ リンクとアプリでの使用方法について説明する
keywords: Teams ディープ リンク ディープリンク
ms.openlocfilehash: 35aceba4b569baac9283a3355ee5719273145652
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797786"
---
# <a name="create-deep-links-to-content-and-features-in-microsoft-teams"></a>Microsoft Teams のコンテンツと機能へのディープ リンクを作成する

Teams 内の情報と機能へのリンクを作成できます。 これが役に立つ例は次のとおりです。

* アプリのいずれかのタブ内のコンテンツにユーザーを移動します。 たとえば、アプリに重要なアクティビティをユーザーに通知するメッセージを送信するボットがある場合があります。 ユーザーが通知をタップすると、ディープ リンクがタブに移動し、ユーザーがアクティビティの詳細を表示できます。
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

Teams のエンティティへのディープ リンクを作成できます。 通常は、タブ内のコンテンツと情報に移動するリンクを作成するために使用されます。たとえば、タブにタスク リストが含まれている場合、チーム メンバーはリンクを作成して、個々のタスクに共有することができます。 このリンクをクリックすると、特定のアイテムにフォーカスするタブに移動します。 これを実装するには、各アイテムに「リンクのコピー」アクションを UI に最適な方法で追加します。 このアクションを実行すると、 `shareDeepLink()` を呼び出して、ユーザーがクリップボードにコピーできるリンクを含むダイアログボックスを表示します。 この呼び出しを行うと、アイテムの ID も渡されます。この ID は、リンクに従って、タブを再読み込みするとき、[コンテキスト](~/tabs/how-to/access-teams-context.md)に戻されます。

または、このトピックで後述する形式を使用して、プログラミングして、ディープ リンクを作成することもできます。 これらは、タブまたはタブ内の[](~/bots/what-are-bots.md)アイテムに[](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)対する変更をユーザーに通知するボットおよびコネクタ メッセージで使用できます。

> [!NOTE]
> これは **[リンクをタブにコピー]** メニュー項目によって提供されるリンクとは異なり、このタブを指すディープ リンクを生成するだけです。

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
> [個人用] タブには `personal` 範囲が設定され、チャネルタブとグループ タブでは範囲 `team` が `group` 使用されます。 構成可能なタブだけがコンテキスト オブジェクトに関連付けられている `channel` プロパティを持つため、2 つのタブの種類の構文はわずかに異なります。 タブ スコープ [の詳細](~/resources/schema/manifest-schema.md) については、マニフェスト リファレンスを参照してください。

> [!NOTE]
> ディープ リンクは、タブが v0.4 以降のライブラリを使用して構成されていて、そのためエンティティ ID がある場合にのみ正常に機能します。 エンティティ ID のないタブへのディープ リンクは、引き続きタブに移動しますが、サブ エンティティ ID をタブに提供することはできません。

ボット、コネクタ、またはメッセージング拡張機能カードで使用できるディープ リンクには、次の形式を使用します。

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> ボットがディープ リンクを使用して `TextBlock` を含むメッセージを送信する場合、ユーザーがリンクを選択すると、新しいブラウザー タブが開きます。 これは、Chrome および Microsoft Teams デスクトップ アプリ (いずれも Linux で実行されています) で発生します。
> ボットが同じディープ リンク URL を `Action.OpenUrl` に送信する場合、ユーザーがリンクをクリックすると、現在のブラウザー　タブで [Teams] タブが開きます。 新しいブラウザー タブは開きません。

クエリ パラメーターは次のとおりです。

* `appId`&emsp;マニフェストの ID。たとえば、「fe4a8eba-2a31-4737-8e33-e5fae6fee194」のようになります
* `entityId`&emsp;タブのアイテムの ID。[タブを構成する](~/tabs/how-to/create-tab-pages/configuration-page.md)ときに表示されます。たとえば、「tasklist123」のようになります
* `entityWebUrl` または `subEntityWebUrl`&emsp;クライアントがタブのレンダリングをサポートしていない場合に使用する代替 URL を含むオプションのフィールド。たとえば、「https://tasklist.example.com/123」または「https://tasklist.example.com/list123/task456」のようになります
* `entityLabel` または `subEntityLabel`&emsp;ディープ リンクを表示するときに使用するタブのアイテムのラベル。たとえば、「Task List 123」または「Task 456」のようになります
* `context`&emsp;次のフィールドを含む JSON オブジェクト。
  * `subEntityId`&emsp;タブ _内_ のアイテムの ID。たとえば、「task456」のようになります
  * `channelId`&emsp;Microsoft Teams チャネル ID (タブ [コンテキスト](~/tabs/how-to/access-teams-context.md)から使用可能。たとえば、「19:cbe3683f25094106b826c9cada3afbe0@thread.skype」のようになります。 このプロパティは、「チーム」の範囲を持つ構成可能なタブにのみ使用できます。 「個人」の範囲を持つ静的なタブでは使用できません。

例:

* 構成可能なタブ自体へのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* 構成可能なタブ内のタスク アイテムへのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* 静的なタブ自体へのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`
* 静的なタブ内のタスク アイテムへのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`

> [!IMPORTANT]
> すべてのクエリ パラメーターが適切に URI にエンコードされていることを確認します。 上記の例では当てはまりませんが、読みやすくするために、行うことをお勧めします。 最後の例を使用します。
> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consuming-a-deep-link-from-a-tab"></a>タブからディープ リンクを使用する

ディープ リンクに移動すると、Microsoft Teams は単にタブに移動し、サブエンティティ ID (存在する場合) を取得するためのメカニズムを Microsoft Teams JavaScript ライブラリを通して提供します。

[`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) を呼び出すと、ディープ リンクを介してタブに移動する場合、`subEntityId` フィールドを含むコンテンツを返します。

## <a name="deep-linking-from-your-tab"></a>タブからのディープ リンクの設定

タブから Teams のコンテンツにディープ リンクを設定することができます。これは、チャネル、メッセージ、別のタブなど、Teams 内の他のコンテンツにリンクする必要がある場合や、スケジュール設定ダイアログを開く場合に便利です。 タブからディープリンクをトリガーするには、次のように呼び出す必要があります。

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

これにより、正しい URL に移動するか、またはスケジュール設定ダイアログやアプリ インストール ダイアログなどのクライアント アクションをトリガーします。 例: 

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a>チャットへのディープ リンクの設定

参加者のセットを指定することで、ユーザー間のプライベート チャットへのディープ リンクを作成できます。 指定した参加者とのチャットが存在しない場合は、リンクは、ユーザーを空の新しいチャットに移動します。 新しいチャットは、ユーザーが最初のメッセージを送信するまで、下書きの状態で作成されます。 必要に応じて、チャットの名前 (まだ存在しない場合) と、ユーザーの作成ボックスに挿入するテキストを指定することができます。 この機能は、ユーザーがチャットに移動したり、チャットを参加したり、メッセージを入力したりする手動操作を行うためのショートカットとして考えることができます。

ユースケースの例として、ボットから Office 365 ユーザー プロファイルをカードとして返す場合、このディープ リンクを使用すると、ユーザーはそのユーザーと簡単にチャットできます。

### <a name="generating-a-deep-link-to-a-chat"></a>チェットへのディープ リンクを作成する

ボット、コネクタ、またはメッセージング拡張機能カードで使用できるディープ リンクには、次の形式を使用します。

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

例: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

クエリ パラメーターは次のとおりです。

* `users`: チャットの参加者を表すユーザー ID のコンマ区切りのリスト。 アクションを実行するユーザーは、参加者として常に含まれます。 現在、[ユーザー ID] フィールドには、Azure AD UserPrincipalName のみがサポートされています (通常はメール アドレス)。
* `topicName`: 3 名以上のユーザーとのチャットの場合、チャットの表示名のオプション フィールド。 このフィールドを指定しない場合、チャットの表示名は、参加者の名前に基づきます。
* `message`: チャットが下書き状態の間に現在のユーザーの作成ボックスに挿入するメッセージ テキストのオプションのフィールドです。

ボットとのこのディープ リンクを使用するには、カードのボタンで URL を対象として指定するか、[ `openUrl` アクションの種類] で [アクション] をタップします。

## <a name="linking-to-the-scheduling-dialog"></a>スケジュール設定ダイアログへのリンクの設定

> [!Note]
> この機能は現在、開発者プレビュー段階です。

Teams の組み込みスケジュール ダイアログへのディープ リンクを作成できます。 これは、アプリがカレンダーやスケジュールに関連するタスクをユーザーに支援する場合に特に便利です。

### <a name="generating-a-deep-link-to-the-scheduling-dialog"></a>スケジュール設定ダイアログへのディープ リンクを作成する

ボット、コネクタ、またはメッセージングの拡張機能カードで使用できるディープ リンクには、次の形式を使用します: `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

例: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

クエリ パラメーターは次のとおりです。

* `attendees`: 会議の出席者を表すユーザー ID のコンマ区切りリスト (省略可能)。 アクションを実行するユーザーは、会議の開催者です。 現在、[ユーザー ID] フィールドには、Azure AD UserPrincipalName のみがサポートされています (通常はメール アドレス)。
* `startTime`: イベントの開始時刻 (省略可能)。 これは、[long ISO 8601 形式](https://en.wikipedia.org/wiki/ISO_8601)、たとえば、「2018-03-12T23:55:25+02:00」にする必要があります。
* `endTime`: イベントのオプションの終了時刻(ISO 8601 形式)。
* `subject`: 会議の件名の省略可能なフィールドです。
* `content`: 会議の詳細フィールドのオプションのフィールドです。

現在、場所の指定はサポートされていません。 開始時刻と終了時刻を生成するときに、UTC オフセット (タイム ゾーン) を指定してください。

ボットとのこのディープ リンクを使用するには、カードのボタンで URL を対象として指定するか、[ `openUrl` アクションの種類] で [アクション] をタップします。
