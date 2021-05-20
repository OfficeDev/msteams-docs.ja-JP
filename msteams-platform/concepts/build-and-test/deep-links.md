---
title: ディープ リンクの作成
description: ディープ リンクとアプリでの使用方法について説明する
ms.topic: how-to
localization_priority: Normal
keywords: Teams ディープ リンク ディープリンク
ms.openlocfilehash: 837d180b06f69b9be49d898c62b9ab8ee64d51d0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566055"
---
# <a name="create-deep-links"></a>ディープ リンクの作成 

Teams内の情報や機能へのリンクを作成できます。 ディープ リンクを作成する場合は、次のようなシナリオが役立ちます。

* アプリのタブの 1 つ内のコンテンツにユーザーを移動します。 たとえば、重要なアクティビティをユーザーに通知するメッセージを送信するボットをアプリに含めることができます。 ユーザーが通知をタップすると、ディープリンクがタブに移動し、アクティビティの詳細を表示できます。
* アプリは、必要なパラメーターを含むディープ リンクを事前に設定することで、チャットの作成や会議のスケジュールなどの特定のユーザー タスクを自動化または簡略化します。 これにより、ユーザーが手動で情報を入力する必要がなくなります。

> [!NOTE]
>
> ディープリンクは、コンテンツに移動する前に、まずブラウザを起動します。 Teamsエンティティのディープ リンクの動作は次のとおりです。
>
> **タブ**:  
> ✔ ディープリンクの URL に直接移動します。
>
> **ボット**:  
> ✔カード本体のディープリンク: 最初にブラウザで開きます。  
> ✔アダプティブカードの OpenURL アクションにディープリンクが追加されました: ディープリンク URL に直接移動します。  
> ✔カードのハイパーリンクマークダウンテキスト: ブラウザで最初に開きます。  
>
> **チャット**  
> ✔ テキスト メッセージ ハイパーリンクマークダウン: ディープリンク URL に直接移動します。  
> ✔一般的なチャット会話で貼り付けたリンク: ディープリンク URL に直接移動します。

## <a name="deep-linking-to-your-tab"></a>タブへのディープ リンクの設定

Teams のエンティティへのディープ リンクを作成できます。 これは、タブ内のコンテンツや情報に移動するリンクを作成するために使用されます。たとえば、タブにタスク リストが含まれている場合、チーム メンバーは個々のタスクへのリンクを作成して共有できます。 リンクを選択すると、特定の項目に焦点を当てたタブに移動します。 これを実装するには、UI に最適な方法で、各項目に **コピー リンク** アクションを追加します。 このアクションを実行すると、 `shareDeepLink()` を呼び出して、ユーザーがクリップボードにコピーできるリンクを含むダイアログボックスを表示します。 この呼び出しを行うと、アイテムの ID も渡されます。この ID は、リンクに従って、タブを再読み込みするとき、[コンテキスト](~/tabs/how-to/access-teams-context.md)に戻されます。

または、このトピックで後述する形式を使用して、プログラミングして、ディープ リンクを作成することもできます。 [ボット](~/bots/what-are-bots.md)と[コネクタ](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)のメッセージにディープ リンクを使用して、タブの変更や、その中のアイテムの変更をユーザーに知らせることができます。

> [!NOTE]
> このディープ リンクは、[ **リンクをタブにコピー** ] メニュー項目によって提供されるリンクとは異なり、このタブを指すディープ リンクが生成されます。

>[!NOTE]
> 現在、shareDeepLinkは、モバイル プラットフォームでは機能しません。

### <a name="show-a-deep-link-to-an-item-within-your-tab"></a>タブ内の項目へのディープリンクを表示する

タブ内の項目へのディープリンクを含むダイアログボックスを表示するには、 を呼び出 `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })` します。

次のフィールドを指定します。

* `subEntityId`: 深いリンクを設定しているタブ内の項目の一意の識別子。
* `subEntityLabel`: ディープ リンクの表示に使用するアイテムのラベル。
* `subEntityWebUrl`: クライアントがタブのレンダリングをサポートしていない場合に使用するフォールバック URL を持つオプションのフィールド。

### <a name="generate-a-deep-link-to-your-tab"></a>タブへのディープリンクを生成する

> [!NOTE]
> 個人タブには `personal` スコープがあり、チャンネルタブとグループタブ `team` `group` はスコープを使用します。 構成可能なタブだけがコンテキスト オブジェクトに関連付けられている `channel` プロパティを持つため、2 つのタブの種類の構文はわずかに異なります。 タブスコープの詳細については、 [マニフェスト](~/resources/schema/manifest-schema.md) リファレンスを参照してください。

> [!NOTE]
> ディープ リンクは、タブが v0.4 以降のライブラリを使用して構成されていて、そのためエンティティ ID がある場合にのみ正常に機能します。 エンティティ ID のないタブへのディープ リンクは、タブに移動しますが、サブエンティティ ID をタブに提供することはできません。

ボット、コネクタ、またはメッセージング拡張機能カードで使用できるディープ リンクには、次の形式を使用します。

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> ボットがディープ リンクを使用して `TextBlock` を含むメッセージを送信する場合、ユーザーがリンクを選択すると、新しいブラウザー タブが開きます。 これは、Chrome および Microsoft Teams デスクトップ アプリ (いずれも Linux で実行されています) で発生します。
> ボットが同じディープ リンク URL `Action.OpenUrl` を に送信した場合、ユーザーがリンクを選択したときに、現在のブラウザ タブで [Teams] タブが開きます。 新しいブラウザ タブは開かれていない。

クエリ パラメーターは次のとおりです。

| パラメーター名 | 説明 | 例 |
|:------------|:--------------|:---------------------|
| `appId`&emsp; | マニフェストの ID。 |fe4a8eba-2a31-4737-8e33-e5fae6fee194|
| `entityId`&emsp; | タブの構成時に指定したタブ内の項目 [の](~/tabs/how-to/create-tab-pages/configuration-page.md)ID。|タスクリスト123|
| `entityWebUrl` 又は `subEntityWebUrl`&emsp; | クライアントがタブのレンダリングをサポートしていない場合に使用するフォールバック URL を持つオプションのフィールド。 | https://tasklist.example.com/123 または https://tasklist.example.com/list123/task456 |
| `entityLabel` 又は `subEntityLabel`&emsp; | 深いリンクを表示するときに使用する、タブ内の項目のラベル。 | タスク リスト 123 または "タスク 456 |
| `context`&emsp; </br></br>* `subEntityId`&emsp;</br></br> * `channelId`&emsp;| 次のフィールドを含む JSON オブジェクト。</br></br> * タブ内の項目の ID。 </br></br> * タブ[コンテキスト](~/tabs/how-to/access-teams-context.md)から取得できるMicrosoft Teamsチャネル ID。 | 
| `subEntityId`&emsp; | タブ内の項目の ID。 |タスク456 |
| `channelId`&emsp; | タブ[コンテキスト](~/tabs/how-to/access-teams-context.md)から取得できるMicrosoft Teams チャネル ID。 このプロパティは、 **チーム** のスコープを持つ構成可能なタブでのみ使用できます。 **個人用** のスコープを持つ静的タブでは使用できません。| 19:cbe3683f25094106b826c9cada3afbe0@thread.skype |

例:

* 構成可能なタブ自体へのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* 構成可能なタブ内のタスク アイテムへのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* 静的なタブ自体へのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`
* 静的なタブ内のタスク アイテムへのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`

> [!IMPORTANT]
> すべてのクエリ パラメーターが適切に URI にエンコードされていることを確認します。 最後の例を使用して、前の例に従う必要があります。

> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consume-a-deep-link-from-a-tab"></a>タブからディープ リンクを使用する

ディープ リンクに移動すると、Microsoft Teamsタブに移動するだけで、サブエンティティ ID が存在する場合は、Microsoft Teams JavaScript ライブラリを通じてそのサブエンティティ ID を取得するメカニズムが提供されます。

[`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-)この呼び出しは、 `subEntityId` タブがディープ リンクを介してナビゲートされた場合に、フィールドを含むコンテキストを返します。

## <a name="deep-linking-from-your-tab"></a>タブからのディープ リンクの設定

タブからTeams内のコンテンツにディープリンクできます。これは、タブがチャンネル、メッセージ、別のタブ、またはスケジューリングダイアログを開くなど、Teams内の他のコンテンツにリンクする必要がある場合に便利です。 タブからディープリンクをトリガーするには、次のように呼び出す必要があります。

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

この呼び出しは、正しい URL に移動するか、スケジュールやアプリのインストール ダイアログを開くなどのクライアント アクションをトリガーします。 次の例を参照してください。

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a>チャットへのディープ リンクの設定

参加者のセットを指定することで、ユーザー間のプライベート チャットへのディープ リンクを作成できます。 指定した参加者とチャットが存在しない場合、リンクは空の新しいチャットにユーザーを移動します。 新しいチャットは、ユーザーが最初のメッセージを送信するまでドラフト状態で作成されます。 それ以外の場合は、チャットの名前が存在しない場合は、ユーザーの作成ボックスに挿入する必要があるテキストと共に指定できます。 この機能は、ユーザーがチャットに移動したり、チャットを参加したり、メッセージを入力したりする手動操作を行うためのショートカットとして考えることができます。

ユースケースの例として、ボットから Office 365 ユーザー プロファイルをカードとして返す場合、このディープ リンクを使用すると、ユーザーはそのユーザーと簡単にチャットできます。

### <a name="generate-a-deep-link-to-a-chat"></a>チャットへのディープリンクを生成する

この形式は、ボット、コネクタ、またはメッセージング拡張カードで使用できるディープ リンクに使用します。

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

例: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

クエリ パラメーターは次のとおりです。

* `users`: チャットの参加者を表すユーザー ID のコンマ区切りリスト。 アクションを実行するユーザーは、常に参加者として含まれます。 現在、ユーザー ID フィールドは、電子メール アドレスなど、Azure AD ユーザー プリンシパル名をサポートしています。
* `topicName`: チャットの表示名 (3 人以上のユーザーとチャットの場合) のオプションフィールド。 このフィールドを指定しない場合、チャットの表示名は参加者の名前に基づいて作成されます。
* `message`: チャットが下書き状態のときに、現在のユーザーの作成ボックスに挿入するメッセージ テキストの省略可能なフィールド。

ボットとのディープリンクを使用するには、カードのボタンで URL ターゲットとして指定するか、 `openUrl` アクションタイプをタップします。

## <a name="generate-deep-links-to-file-in-channel"></a>チャネル内のファイルへのディープリンクを生成する

次のディープ リンク形式は、ボット、コネクタ、またはメッセージング拡張カードで使用できます。

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80?tenantId=<tenantid>&fileType=<filetype>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadid>&groupId=<groupId>`

クエリ パラメーターは次のとおりです。

* `tenantId`: テナント ID の例, 0d9b645f-597b-41f0-a2a3-ef103fbd91bb
* `fileType`: サポートされているファイルの種類 (docx、pptx、xlsx、pdf など)
* `objectUrl`: ファイルのオブジェクト URL、 https://microsoft.sharepoint.com/teams/(filepath)
* `baseUrl`: ファイルのベース URL https://microsoft.sharepoint.com/teams
* `serviceName`: サービス名、アプリ ID
* `threadId`: スレッド ID は、ファイルが格納されているチームのチーム ID です。 これはオプションであり、ユーザーのOneDriveフォルダーに格納されているファイルに対しては設定できません。 スレッド Id - 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype
* `groupId`: ファイルのグループ ID ae063b79-5315-4ddb-ba70-27328ba6c31e

ファイルへのディープリンクの形式の例を次に示します。

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80 ?tenantId=0d9b645f-597b-41f0-a2a3-ef103fbd91bb&fileType=pptx&objectUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform%2FShared%20Documents%2FFC7-%20Bot%20and%20Action%20Infra%2FKaizala%20Actions%20in%20Adaptive%20Cards%20-%20Deck.pptx&baseUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform&serviceName=teams&threadId=19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype&groupId=ae063b79-5315-4ddb-ba70-27328ba6c31e`

### <a name="serialization-of-this-object"></a>このオブジェクトのシリアル化:
```
{
tenantId: "0d9b645f-597b-41f0-a2a3-ef103fbd91bb",
filetype: = "pptx",
objectUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform/Shared Documents/FC7- Bot and Action Infra/Kaizala Actions in Adaptive Cards - Deck.pptx",
baseUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform",
serviceName: "teams",
threadId: = "19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype",
groupId: "ae063b79-5315-4ddb-ba70-27328ba6c31e"
}
```
## <a name="deep-linking-for-sharepoint-framework-tabs"></a>SharePoint Frameworkタブのディープリンク

次のディープ リンク形式は、ボット、コネクタ、またはメッセージング拡張カードで使用できます。 `https://teams.microsoft.com/l/entity/<AppId>/<EntityId>?webUrl=<entityWebUrl>/<EntityName>`

> [!NOTE]
> ボットがディープリンクを含む TextBlock メッセージを送信すると、ユーザーがリンクを選択すると新しいブラウザタブが開きます。 これは、Chromeで発生し、Linux上で実行されているMicrosoft Teamsデスクトップアプリ。
> ボットが同じディープ リンク URL を に送信した場合、 `Action.OpenUrl` ユーザーがリンクを選択すると、Teamsタブが現在のブラウザで開きます。 新しいブラウザー タブは開きません。

クエリ パラメーターは次のとおりです。

* `appID`: マニフェスト ID **fe4a8eba-2a31-4737-8e33-e5fae6fee194**.

* `entityID`:[タブを構成](~/tabs/how-to/create-tab-pages/configuration-page.md)するときに指定した項目 ID。たとえば、**タスクリスト123。**
* `entityWebUrl`: クライアントがタブのレンダリングをサポートしていない場合に使用するフォールバック URL を持つオプションのフィールド - https://tasklist.example.com/123 または https://tasklist.example.com/list123/task456 .
* `entityName`: 深いリンク、タスク リスト 123 またはタスク 456 を表示するときに使用するタブ内の項目のラベル。

例: https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&TaskList

## <a name="deep-linking-to-the-scheduling-dialog"></a>スケジュール設定ダイアログへのディープリンク

> [!NOTE]
> この機能は現在、開発者プレビュー段階です。

組み込みのスケジュール設定ダイアログTeamsへのディープリンクを作成できます。 これは、アプリがユーザーのカレンダーの完了や関連タスクのスケジュール設定を支援する場合に特に便利です。

### <a name="generate-a-deep-link-to-the-scheduling-dialog"></a>スケジュール設定ダイアログへのディープリンクを生成する

ボット、コネクタ、またはメッセージング拡張機能カードで使用できるディープ リンクには、次の形式を使用します。 `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

例: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

クエリ パラメーターは次のとおりです。

* `attendees`: 会議の出席者を表すユーザー ID のコンマ区切りリスト (省略可能)。 アクションを実行するユーザーは、会議の開催者です。 [ユーザー ID] フィールドは、現在 Azure AD ユーザー プリンシパル名 (通常は電子メール アドレス) のみをサポートしています。
* `startTime`: イベントの開始時刻 (省略可能)。 これは *、2018-03-12T23:55:25+02:00* など、[長いISO 8601形式](https://en.wikipedia.org/wiki/ISO_8601)でなければなりません。
* `endTime`: イベントの終了時刻 (ISO 8601 形式も含む)
* `subject`: 会議の件名のオプションフィールド。
* `content`: 会議の詳細フィールドのオプション フィールド。

> [!NOTE]
> 現在、場所の指定はサポートされていません。 UTC オフセットを指定する必要があり、開始時刻と終了時刻を生成するときにタイム ゾーンを意味します。

ボットとのこのディープ リンクを使用するには、カードのボタンで URL を対象として指定するか、[ `openUrl` アクションの種類] で [アクション] をタップします。

## <a name="deep-linking-to-an-audio-or-audio-video-call"></a>オーディオ通話またはオーディオビデオ通話へのディープリンク

ディープ リンクを作成して、オーディオまたは *AV* などのコールの種類と参加者を指定することで、1 人のユーザーまたはユーザーのグループに対してオーディオ *のみまたはオーディオ* ビデオ通話を呼び出すことができます。 ディープ リンクが呼び出された後、呼び出しを行う前に、デスクトップ クライアントTeams呼び出しを行う確認を求めるプロンプトが表示されます。 グループコールの場合、同じディープリンク呼び出しで一連の VoIP ユーザと PSTN ユーザのセットを呼び出すことができます。 

ビデオ通話の場合、クライアントは確認を求め、発信者のビデオをオンにします。 通話の受信者は、Teams呼び出し通知ウィンドウを介して、オーディオのみまたはオーディオとビデオを介して応答する選択肢があります。

> [!NOTE]
> このディープリンクは、会議の呼び出しには使用できません。

### <a name="generate-a-deep-link-to-a-call"></a>通話へのディープ リンクを生成する

| ディープリンク | Format | 例 |
|-----------|--------|---------|
| 音声通話を発信する | https://teams.microsoft.com/l/call/0/0?users=&lt;ユーザー 1 &gt; , &lt; ユーザー2&gt; | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com |
| 音声通話とビデオ通話を行う | https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; , &lt; ユーザー2 &gt;&ビデオ=true | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withvideo=true |
|オプションのパラメータソースを使用して音声通話とビデオ通話を行う | https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; , &lt; ユーザー2 &gt;&ビデオ=真の&ソース=デモアプリ | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withvideo=true&source=demoApp |  
| VoIP と PSTN ユーザーの組み合わせに音声通話とビデオ通話を行う | https://teams.microsoft.com/l/call/0/0?users=&lt;ユーザー &gt; 1,4: &lt; 電話番号&gt; | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,4:9876543210 |
  
クエリ パラメーターは次のとおりです。
* `users`: コールの参加者を表すユーザー ID のコンマ区切りリスト。 現在、ユーザー ID フィールドは、Azure AD ユーザー プリンシパル名 (通常は電子メール アドレス) をサポートしているか、PSTN 呼び出しの場合は pstn mri 4: &lt; 電話番号 &gt; をサポートしています。
* `Withvideo`: これはオプションのパラメータで、ビデオコールを行うために使用できます。 このパラメータを設定すると、呼び出し元のカメラだけがオンになります。 通話の受信者は、Teams呼び出し通知ウィンドウを介して音声または音声とビデオ通話を通じて応答する選択肢があります。 
* `Source`: これは、ディープリンクのソースを知らせるオプションのパラメータです。

## <a name="code-sample"></a>コード サンプル

| サンプルの名前 | 説明 | C# |Node.js|
|-------------|-------------|------|----|
|深いリンク使用サブエンティティ ID  |Microsoft Teamsサンプル アプリで、ボット チャットからサブエンティティ ID を使用するタブへのディープリンクをデモンストレーションします。|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/nodejs)|

## <a name="see-also"></a>関連項目

[Web アプリを統合する](~/samples/integrate-web-apps-overview.md)

