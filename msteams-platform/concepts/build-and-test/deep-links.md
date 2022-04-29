---
title: ディープ リンクの作成
description: ディープ リンクとアプリでの使用方法について説明する
ms.topic: how-to
ms.localizationpriority: high
keywords: Teams ディープ リンク ディープリンク
ms.openlocfilehash: cc8e71e77964ff2a07e75983c94f72091033b789
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103924"
---
# <a name="create-deep-links"></a>ディープ リンクの作成

Teams 内の情報や機能へのリンクを作成できます。 ディープ リンクの作成が役立つシナリオは次のとおりです。

* アプリのタブの 1 つにあるコンテンツにユーザーを移動します。 たとえば、アプリには、ユーザーに重要なアクティビティを通知するメッセージを送信するボットを含めることができます。 ユーザーが通知をタップすると、ディープ リンクがタブに移動し、ユーザーがアクティビティの詳細を表示できるようになります。
* アプリは、ディープ リンクに必要なパラメーターを事前に入力することで、チャットの作成や会議のスケジュール設定など、特定のユーザー タスクを自動化または簡素化します。これにより、ユーザーが手動で情報を入力する必要がなくなります。

> [!NOTE]
>
> ディープリンクは、コンテンツに移動する前に、最初にブラウザを起動します。 Teams エンティティでのディープリンクの動作は次のとおりです。
>
> **タブ**:  
> ✔ ディープリンクの URL に直接移動します。
>
> **ボット**:  
> ✔ カード本体のディープリンク: 最初にブラウザで開きます。  
> ✔ アダプティブ カードの OpenURL アクションに追加されたディープリンク: ディープリンク URL に直接移動します。  
> ✔カード内のハイパーリンク マークダウン テキスト: 最初にブラウザで開 きます。  
>
> **チャット**  
> ✔ テキスト メッセージのハイパー リンク マークダウン: ディープリンクの URL に直接移動します。  
> ✔ 一般的なチャット会話に貼り付けられたリンク: ディープリンクの URL に直接移動します。

## <a name="deep-linking-to-your-tab"></a>タブへのディープ リンクの設定

Teams のエンティティへのディープ リンクを作成できます。 これは、タブ内のコンテンツや情報に移動するリンクを作成するために使用されます。 たとえば、タブにタスク リストが含まれている場合、チーム メンバーは個々のタスクへのリンクを作成して共有できます。 リンクを選択すると、特定のアイテムに焦点を当てたタブに移動します。 これを実装するには、各アイテムに **リンクのコピー** アクションを UI に最適な方法で追加します。 このアクションを実行すると、 `shareDeepLink()` を呼び出して、ユーザーがクリップボードにコピーできるリンクを含むダイアログボックスを表示します。 この呼び出しを行うと、アイテムの ID も渡されます。この ID は、リンクに従って、タブを再読み込みするとき、[コンテキスト](~/tabs/how-to/access-teams-context.md)に戻されます。

または、この記事で後述する形式を使用して、プログラミングして、ディープ リンクを作成することもできます。 タブまたはタブ内のアイテムへの変更についてユーザーに通知する[ボット](~/bots/what-are-bots.md)および[コネクター](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) メッセージでディープ リンクを使用できます。

> [!NOTE]
> このディープリンクは、**[タブへのリンクのコピー]** メニュー項目によって提供されるリンクとは異なります。このメニュー項目は、このタブを指すディープ リンクを生成するだけです。

>[!IMPORTANT]
> 現在、shareDeepLinkは、モバイル プラットフォームでは機能しません。

### <a name="show-a-deep-link-to-an-item-within-your-tab"></a>タブ内のアイテムへのディープ リンクを表示する

タブ内のアイテムへのディープ リンクを含むダイアログ ボックスを表示するには、`microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })` を呼び出します。

次のフィールドを入力します。

* `subEntityId`: ディープ リンクしているタブ内のアイテムの一意の識別子。
* `subEntityLabel`: ディープ リンクの表示に使用するアイテムのラベル。
* `subEntityWebUrl`: クライアントがタブのレンダリングをサポートしていない場合に使用するフォールバック URL を含むオプションのフィールド。

### <a name="generate-a-deep-link-to-your-tab"></a>タブへのディープ リンクを生成する

> [!NOTE]
>
> * 個人用タブには `personal` スコープがあり、チャネル タブとグループ タブには `team` または `group` スコープが使用されます。 構成可能なタブだけがコンテキスト オブジェクトに関連付けられている `channel` プロパティを持つため、2 つのタブの種類の構文はわずかに異なります。 タブスコープの詳細については、[マニフェスト](~/resources/schema/manifest-schema.md) リファレンスを参照してください。
> * ディープ リンクは、タブが v0.4 以降のライブラリを使用して構成されていて、そのためエンティティ ID がある場合にのみ正常に機能します。 エンティティ ID のないタブへのディープ リンクは引き続きタブに移動しますが、サブエンティティ ID をタブに提供することはできません。

ボット、コネクタ、またはメッセージング拡張カードで使用できるディープ リンクには、次の形式を使用します:

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> ボットがディープ リンクを使用して `TextBlock` を含むメッセージを送信する場合、ユーザーがリンクを選択すると、新しいブラウザー タブが開きます。 これは、Chrome および Microsoft Teams デスクトップ アプリ (いずれも Linux で実行されています) で発生します。
> ボットが同じディープ リンク URL を `Action.OpenUrl` に送信した場合、ユーザーがリンクを選択すると、現在のブラウザ タブで Teams タブが開きます。 新しいブラウザー タブは開きません。

<!--- TBD: Edit this article.
* Admonitions/alerts seem to be overused. 
* An important alert at the end of this table does not make sense. Also, it has a code snippet inside it.
* List items in the table are not formatted well in output.
* Some headings use -ing verbs.
* Example values and some URLs should be in backticks and not emphasized.
* Codeblock are missing language.
* Check for markdownlint errors.
* Table with just a row is not really needed. Provide the content without tabulating it.
--->

クエリ パラメーターは次のとおりです。

| パラメーター名 | 説明 | 例 |
|:------------|:--------------|:---------------------|
| `appId`&emsp; | マニフェストからの ID。 |fe4a8eba-2a31-4737-8e33-e5fae6fee194|
| `entityId`&emsp; | [タブの構成時](~/tabs/how-to/create-tab-pages/configuration-page.md)に指定した、タブ内のアイテムの ID。|Tasklist123|
| `entityWebUrl` または `subEntityWebUrl`&emsp; | クライアントがタブのレンダリングをサポートしていない場合に使用するフォールバック URL を含むオプションのフィールド。 | `https://tasklist.example.com/123` または `https://tasklist.example.com/list123/task456` |
| `entityLabel` または `subEntityLabel`&emsp; | ディープ リンクを表示するときに使用する、タブ内のアイテムのラベル。 | タスク リスト 123 または "タスク 456" |
| `context.subEntityId`&emsp; | タブ内のアイテムの ID。 |Task456 |
| `context.channelId`&emsp; | タブ[コンテキスト](~/tabs/how-to/access-teams-context.md)から使用可能な Microsoft Teams チャネル ID。 このプロパティは、**チーム** のスコープを持つ構成可能なタブでのみ使用できます。 **個人** のスコープを持つ静的タブでは使用できません。| 19:cbe3683f25094106b826c9cada3afbe0@thread.skype |
| `chatId`&emsp; | グループ チャットと会議チャットのタブ[コンテキスト](~/tabs/how-to/access-teams-context.md)から使用可能な ChatId | 17:b42de192376346a7906a7dd5cb84b673@thread.v2 |
| `contextType`&emsp; |  チャットは会議でサポートされている唯一の contextType です | チャット |

**例**:

* 静的 (個人用) タブ自体へのリンク:

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`

* 静的 (個人用) タブ内のタスク アイテムへのリンク:

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`

* 構成可能なタブ自体へのリンク: 

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`

* 構成可能なタブ内のタスク アイテムへのリンク: 

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`

* 会議またはグループ チャットに追加されたタブ アプリへのリンク:

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456?context={"chatId": "17:b42de192376346a7906a7dd5cb84b673@thread.v2","contextType":"chat"}`

> [!IMPORTANT]
> すべてのクエリ パラメーターが適切に URI にエンコードされていることを確認します。 最後の例を使用して、前述の例に従う必要があります。
>
> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consume-a-deep-link-from-a-tab"></a>タブからディープ リンクを使用する

ディープ リンクに移動する場合、Microsoft Teams はタブに移動するだけで、Microsoft Teams JavaScript ライブラリを介してサブエンティティ ID が存在する場合はそれを取得するメカニズムを提供します。

タブがディープリンクを介してナビゲートされた場合、[`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-)呼び出しは `subEntityId` フィールドを含むコンテキストを返します。

## <a name="deep-linking-from-your-tab"></a>タブからのディープ リンクの設定

タブから Teams のコンテンツにディープリンクを指定できます。 これは、タブが、チャネル、メッセージ、別のタブなど、Teams の他のコンテンツにリンクする必要がある場合、またはスケジュール ダイアログを開く必要がある場合に役立ちます。タブからディープリンクをトリガーするには、次の呼び出しを行います。

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

この呼び出しは、正しい URL に移動するか、スケジュールやアプリのインストール ダイアログを開くなどのクライアント アクションをトリガーします。次の例を参照してください。

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a>チャットへのディープ リンクの設定

参加者のセットを指定することで、ユーザー間のプライベート チャットへのディープ リンクを作成できます。 指定された参加者とのチャットが存在しない場合、リンクはユーザーを空の新しいチャットに移動します。 ユーザーが最初のメッセージを送信するまで、新しいチャットは下書き状態で作成されます。 それ以外の場合は、チャットの名前がまだ存在しない場合は、ユーザーの作成ボックスに挿入する必要のあるテキストとともに指定できます。 この機能は、ユーザーがチャットに移動したり、チャットを参加したり、メッセージを入力したりする手動操作を行うためのショートカットとして考えることができます。

ユースケースの例として、ボットから Office 365 ユーザー プロファイルをカードとして返す場合、このディープ リンクを使用すると、ユーザーはそのユーザーと簡単にチャットできます。

### <a name="generate-a-deep-link-to-a-chat"></a>チャットへのディープ リンクを生成する

ボット、コネクタ、またはメッセージの拡張機能カードで使用できるディープ リンクには、次の形式を使用します:

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

例: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

クエリ パラメーターは次のとおりです。

* `users`: チャットの参加者を表すユーザー ID のコンマで区切られたリスト。 アクションを実行するユーザーは、常に参加者として含まれます。 現在、[ユーザーID] フィールドは、メール アドレスのみなどの Microsoft Azure Active Directory (Azure AD) UserPrincipalName をサポートしています。
* `topicName`: 3 人以上のユーザーとのチャットの場合、チャット 表示名のオプションのフィールド。 このフィールドが指定されていない場合、チャットの表示名は参加者の名前に基づいています。
* `message`: チャットがドラフト状態のときに現在のユーザーの作成ボックスに挿入するメッセージ テキストのオプションのフィールド。

ボットでこのディープ リンクを使用するには、これをカードのボタンの URL ターゲットとして指定するか、`openUrl` アクション タイプでアクションをタップします。

## <a name="generate-deep-links-to-file-in-channel"></a>チャネル内のファイルへのディープ リンクを生成する

次のディープ リンク形式は、ボット、コネクタ、またはメッセージ拡張カードで使用されます: 

`https://teams.microsoft.com/l/file/<fileId>?tenantId=<tenantId>&fileType=<fileType>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadId>&groupId=<groupId>`

クエリ パラメーターは次のとおりです。

* `fileId`: Sharepoint Online の一意のファイル ID (`sourcedoc` とも呼ばれます)。たとえば、`1FA202A5-3762-4F10-B550-C04F81F6ACBD` です。
* `tenantId`: `0d9b645f-597b-41f0-a2a3-ef103fbd91bb` などのテナント ID。
* `fileType`: .docx、.pptx、.xlsx、.pdf などのサポートされているファイルの種類
* `objectUrl`: ファイルのオブジェクト URL。 形式は `https://{tenantName}.sharepoint.com/sites/{TeamName}/SharedDocuments/{ChannelName}/FileName.ext` です。 たとえば、「 `https://microsoft.sharepoint.com/teams/(filepath)` 」のように入力します。
* `baseUrl`: ファイルのベース URL。 形式は `https://{tenantName}.sharepoint.com/sites/{TeamName}` です。 たとえば、「 `https://microsoft.sharepoint.com/teams` 」のように入力します。
* `serviceName`: サービスの名前、アプリ ID。たとえば、`teams` などです。
* `threadId`: threadId は、ファイルが保存されているチームのチーム ID です。 これはオプションであり、ユーザーの OneDrive フォルダーに保存されているファイルには設定できません。 threadId - 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype.
* `groupId`: ファイルのグループ ID。例: `ae063b79-5315-4ddb-ba70-27328ba6c31e`。

> [!NOTE]
> チャネルからの URL に `threadId` と `groupId` が表示されます。  

次のディープ リンク形式は、ボット、コネクタ、またはメッセージ拡張カードで使用されます: 

`https://teams.microsoft.com/l/file/<fileId>?tenantId=<tenantId>&fileType=<fileType>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadId>&groupId=<groupId>`

次のフォーマット例は、ファイルへのディープリンクを示しています。

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80?tenantId=0d9b645f-597b-41f0-a2a3-ef103fbd91bb&fileType=pptx&objectUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform%2FShared%20Documents%2FFC7-%20Bot%20and%20Action%20Infra%2FKaizala%20Actions%20in%20Adaptive%20Cards%20-%20Deck.pptx&baseUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform&serviceName=teams&threadId=19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype&groupId=ae063b79-5315-4ddb-ba70-27328ba6c31e`

### <a name="serialization-of-this-object"></a>このオブジェクトのシリアル化

```javascript
{
fileId: "5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80",
tenantId: "0d9b645f-597b-41f0-a2a3-ef103fbd91bb",
filetype: = "pptx",
objectUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform/Shared Documents/FC7- Bot and Action Infra/Kaizala Actions in Adaptive Cards - Deck.pptx",
baseUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform",
serviceName: "teams",
threadId: = "19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype",
groupId: "ae063b79-5315-4ddb-ba70-27328ba6c31e"
}
```

## <a name="deep-linking-to-an-app"></a>アプリへのディープ リンク

アプリが Teams ストアにリストされたら、アプリのディープリンクを作成します。 Teams を起動するためのリンクを作成するには、アプリ ID を次の URL に追加します: `https://teams.microsoft.com/l/app/<your-app-id>`。 アプリをインストールするダイアログ ボックスが表示されます。
  
## <a name="deep-linking-for-sharepoint-framework-tabs"></a>SharePoint Framework タブのディープ リンク

次のディープ リンク形式は、ボット、コネクタ、またはメッセージ拡張カードで使用できます: `https://teams.microsoft.com/l/entity/<AppId>/<EntityId>?webUrl=<entityWebUrl>/<EntityName>`

> [!NOTE]
> ボットがディープ リンクを含む TextBlock メッセージを送信すると、ユーザーがリンクを選択すると新しいブラウザ タブが開きます。 これは、Linuxで 実行されている Chrome および Microsoft Teams デスクトップ アプリで発生します。
> ボットが同じディープリンク URL を `Action.OpenUrl` に送信した場合、ユーザーがリンクを選択すると、現在のブラウザーで Teams タブが開きます。 新しいブラウザー タブは開きません。

クエリ パラメーターは次のとおりです。

* `appID`: マニフェスト ID、たとえば `fe4a8eba-2a31-4737-8e33-e5fae6fee194`。

* `entityID`: [タブを構成する](~/tabs/how-to/create-tab-pages/configuration-page.md)ときに提供したアイテム ID。 たとえば、`tasklist123` です。
* `entityWebUrl`: クライアントがタブのレンダリングをサポートしていない場合に使用するフォールバック URL を含むオプションのフィールド - `https://tasklist.example.com/123`または `https://tasklist.example.com/list123/task456`。
* `entityName`: ディープ リンク、タスク リスト 123 またはタスク 456 を表示するときに使用するタブ内のアイテムのラベル。

例: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&TaskList`

## <a name="deep-linking-to-the-scheduling-dialog"></a>スケジュール設定ダイアログへのディープ リンク

> [!NOTE]
> この機能は現在、開発者プレビュー段階です。

Teams の組み込みのスケジューリング ダイアログへのディープ リンクを作成できます。 これは、アプリがカレンダーやスケジュールに関連するタスクをユーザーに支援する場合に特に便利です。

### <a name="generate-a-deep-link-to-the-scheduling-dialog"></a>スケジュール設定ダイアログへのディープ リンクを作成する

ボット、コネクタ、またはメッセージ拡張カードで使用できるディープ リンクには、次の形式を使用します: `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

例: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

> [!NOTE]
> 検索パラメーターは、空白 (` `) の代わりに `+` シグナルをサポートしていません。 URI エンコーディング コードがスペースに対して `%20` を返すことを確認します。たとえば、`?subject=test%20subject` は適切ですが、`?subject=test+subject` は不適切です。

クエリ パラメーターは次のとおりです。

* `attendees`: 会議の参加者を表すユーザー ID のオプションのコンマ区切りリスト。 アクションを実行するユーザーは、会議の開催者です。 現在、[ユーザー ID] フィールドは、Azure AD UserPrincipalName (通常はメール アドレス) のみをサポートしています。
* `startTime`: イベントのオプションの開始時間。 これは、[long ISO 8601 形式](https://en.wikipedia.org/wiki/ISO_8601) ( 例: *2018-03-12T23:55:25+02:00*)である必要があります。
* `endTime`: イベントの終了時刻 (省略可能、 ISO 8601形式)。
* `subject`: 会議の件名の省略可能なフィールド。
* `content`: 会議の詳細フィールドの省略可能なフィールド。

> [!NOTE]
> 現在、場所の指定はサポートされていません。UTC オフセットを指定する必要があります。これは、開始時刻と終了時刻を生成するときのタイム ゾーンを意味します。

ボットとのこのディープ リンクを使用するには、カードのボタンで URL を対象として指定するか、[ `openUrl` アクションの種類] で [アクション] をタップします。

## <a name="deep-linking-to-an-audio-or-audio-video-call"></a>音声通話または音声ビデオ通話へのディープ リンク

コールタイプを *オーディオ* または *av* として指定し、参加者を指定することで、単一のユーザーまたはユーザー グループに対して音声のみまたは音声ビデオ通話を呼び出すためのディープ リンクを作成できます。 ディープ リンクが呼び出された後、呼び出しを行う前に、Teams クライアントは電話をかけるための確認を求めます。 グループ通話の場合、同じディープリンク呼び出しで一連の VoIP ユーザーと一連の PSTN ユーザーを呼び出すことができます。

ビデオ通話の場合、クライアントは確認を求め、通話の発信者のビデオをオンにします。 通話の受信者は、Teams の通話通知ウィンドウを使用して、音声のみで応答するか、音声とビデオで応答するかを選択できます。

> [!NOTE]
> このディープリンクは、会議の呼び出しには使用できません。

### <a name="generate-a-deep-link-to-a-call"></a>通話へのディープ リンクを生成する

| ディープ リンク | フォーマット | 例 |
|-----------|--------|---------|
| 音声通話を行う | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com` |
| 音声またはビデオ通話を開始する | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>&withVideo=true` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withVideo=true` |
|オプションのパラメータ ソースを使用して音声通話とビデオ通話を発信する | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>&withVideo=true&source=demoApp` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withVideo=true&source=demoApp` |  
| VoIP ユーザーと PSTN ユーザーの組み合わせに音声通話とビデオ通話を発信する | `https://teams.microsoft.com/l/call/0/0?users=<user1>,4:<phonenumber>` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,4:9876543210` |
  
クエリ パラメーターは次のとおりです。

* `users`: 通話の参加者を表すユーザー ID のコンマで区切られたリスト。現在、[ユーザー ID] フィールドは Azure AD UserPrincipalName (通常はメール アドレス) をサポートしています。PSTN 通話の場合は、pstn mri 4: &lt;phonenumber&gt; をサポートしています。
* `withVideo`: これはオプションのパラメータであり、ビデオ通話を行うために使用できます。 このパラメータを設定すると、発信者のカメラだけがオンになります。 通話の受信者は、Teams の通話通知ウィンドウから音声通話または音声通話とビデオ通話を選択できます。
* `Source`: これはオプションのパラメーターで、ディープリンクのソースを通知します。

## <a name="code-sample"></a>コード サンプル

| サンプルの名前 | 説明 | C# |Node.js|
|-------------|-------------|------|----|
|Subentity ID を使用するディープ リンク  |ボット チャットからタブを消費するサブエンティティ ID へのディープリンクを示すための Microsoft Teams サンプル アプリ。|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/nodejs)|

## <a name="see-also"></a>関連項目

* [Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
* [Moodle LMS](~/resources/moodleinstructions.md)
