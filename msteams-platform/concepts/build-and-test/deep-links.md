---
title: ディープ リンクの作成
description: ディープ リンクとアプリでの使用方法について説明する
ms.topic: how-to
localization_priority: Normal
keywords: Teams ディープ リンク ディープリンク
ms.openlocfilehash: cd7735595f260431524edf1431ff22a1eeb361bc
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630146"
---
# <a name="create-deep-links"></a>ディープ リンクの作成 

情報と機能へのリンクは、Teams。 ディープ リンクの作成が役立つシナリオは次のとおりです。

* アプリのいずれかのタブ内のコンテンツにユーザーを移動します。 たとえば、アプリには、重要なアクティビティをユーザーに通知するメッセージを送信するボットを作成できます。 ユーザーが通知をタップすると、深いリンクがタブに移動し、ユーザーがアクティビティの詳細を表示できます。
* アプリは、必要なパラメーターを含むディープ リンクを事前に設定することで、チャットの作成や会議のスケジュール設定など、特定のユーザー タスクを自動化または簡素化します。 これにより、ユーザーが手動で情報を入力する必要がなくなります。

> [!NOTE]
>
> ディープリンクは、コンテンツに移動する前にブラウザーを最初に起動します。 エンティティ上のディープ リンクTeamsは次のとおりです。
>
> **タブ**:  
> ✔ ディープリンクの URL に直接移動します。
>
> **ボット**:  
> ✔本文の Deeplink: ブラウザーで最初に開きます。  
> ✔カードの OpenURL アクションに Deeplink を追加: ディープリンク URL に直接移動します。  
> ✔の [ハイパーリンク] マークダウン テキスト: ブラウザーで最初に開きます。  
>
> **チャット**  
> ✔ メッセージのハイパーリンク マークダウン: ディープリンク URL に直接移動します。  
> ✔チャット会話で貼り付けリンク: ディープリンク URL に直接移動します。

## <a name="deep-linking-to-your-tab"></a>タブへのディープ リンクの設定

Teams のエンティティへのディープ リンクを作成できます。 これは、タブ内のコンテンツと情報に移動するリンクを作成するために使用されます。たとえば、タブにタスク リストが含まれている場合、チーム メンバーは個々のタスクへのリンクを作成して共有できます。 リンクを選択すると、特定のアイテムに焦点を当てたタブに移動します。 これを実装するには、UI に最も適した方法で、各アイテムにコピー リンク アクションを追加します。 このアクションを実行すると、 `shareDeepLink()` を呼び出して、ユーザーがクリップボードにコピーできるリンクを含むダイアログボックスを表示します。 この呼び出しを行うと、アイテムの ID も渡されます。この ID は、リンクに従って、タブを再読み込みするとき、[コンテキスト](~/tabs/how-to/access-teams-context.md)に戻されます。

または、このトピックで後述する形式を使用して、プログラミングして、ディープ リンクを作成することもできます。 ボットおよびコネクタ メッセージ内のディープ [リンク](~/bots/what-are-bots.md) を [使用](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) すると、タブの変更、またはタブ内のアイテムに関する情報をユーザーに通知できます。

> [!NOTE]
> このディープ リンクは、[タブ へのコピー]リンクによって提供されるリンクとは異なります。これは、このタブをポイントするディープ リンクを生成するだけです。

>[!NOTE]
> 現在、shareDeepLinkは、モバイル プラットフォームでは機能しません。

### <a name="show-a-deep-link-to-an-item-within-your-tab"></a>タブ内のアイテムへの深いリンクを表示する

タブ内のアイテムへのディープ リンクを含むダイアログ ボックスを表示するには、を呼び出します `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })` 。

次のフィールドを指定します。

* `subEntityId`: ディープ リンク先のタブ内のアイテムの一意の識別子です。
* `subEntityLabel`: ディープ リンクの表示に使用するアイテムのラベル。
* `subEntityWebUrl`: クライアントがタブのレンダリングをサポートしていない場合に使用するフォールバック URL を含むオプションのフィールド。

### <a name="generate-a-deep-link-to-your-tab"></a>タブへのディープ リンクを生成する

> [!NOTE]
> 個人用タブにはスコープ `personal` が含まれていますが、チャネルタブとグループ タブはスコープ `team` を `group` 使用します。 構成可能なタブだけがコンテキスト オブジェクトに関連付けられている `channel` プロパティを持つため、2 つのタブの種類の構文はわずかに異なります。 タブ スコープ [の詳細](~/resources/schema/manifest-schema.md) については、マニフェスト リファレンスを参照してください。

> [!NOTE]
> ディープ リンクは、タブが v0.4 以降のライブラリを使用して構成されていて、そのためエンティティ ID がある場合にのみ正常に機能します。 エンティティ ID のないタブへのディープ リンクは、タブに移動しますが、サブエンティティ ID をタブに提供することはできません。

ボット、コネクタ、またはメッセージング拡張機能カードで使用できるディープ リンクには、次の形式を使用します。

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> ボットがディープ リンクを使用して `TextBlock` を含むメッセージを送信する場合、ユーザーがリンクを選択すると、新しいブラウザー タブが開きます。 これは、Chrome および Microsoft Teams デスクトップ アプリ (いずれも Linux で実行されています) で発生します。
> ボットが同じディープ リンク URL を a に送信すると、ユーザーがリンクを選択すると、現在Teamsタブで [詳細リンク] タブ `Action.OpenUrl` が開きます。 新しいブラウザー タブが開かれません。

クエリ パラメーターは次のとおりです。

| パラメーター名 | 説明 | 例 |
|:------------|:--------------|:---------------------|
| `appId`&emsp; | マニフェストの ID。 |fe4a8eba-2a31-4737-8e33-e5fae6fee194|
| `entityId`&emsp; | タブの構成時に指定したタブ内のアイテムの [ID](~/tabs/how-to/create-tab-pages/configuration-page.md)です。|Tasklist123|
| `entityWebUrl` または `subEntityWebUrl`&emsp; | クライアントがタブのレンダリングをサポートしていない場合に使用するフォールバック URL を含むオプションのフィールド。 | `https://tasklist.example.com/123` または `https://tasklist.example.com/list123/task456` |
| `entityLabel` または `subEntityLabel`&emsp; | ディープ リンクを表示するときに使用するタブ内のアイテムのラベル。 | タスク リスト 123 または "タスク 456" |
| `context`&emsp; </br></br>* `subEntityId`&emsp;</br></br> * `channelId`&emsp;| 次のフィールドを含む JSON オブジェクト。</br></br> * タブ内のアイテムの ID。 </br></br> * タブ コンテキストMicrosoft Teams利用可能なチャネル ID を指定[します](~/tabs/how-to/access-teams-context.md)。 | 
| `subEntityId`&emsp; | タブ内のアイテムの ID。 |Task456 |
| `channelId`&emsp; | タブ Microsoft Teamsから使用できるチャネル ID を指定[します](~/tabs/how-to/access-teams-context.md)。 このプロパティは、チームのスコープを持つ構成可能なタブでのみ使用 **できます**。 これは、個人用の範囲を持つ静的タブでは使用 **できません**。| 19:cbe3683f25094106b826c9cada3afbe0@thread.skype |

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

ディープ リンクに移動すると、Microsoft Teams はタブに移動し、Microsoft Teams JavaScript ライブラリを介してサブエンティティ ID が存在する場合に取得するメカニズムを提供します。

この呼び出しは、タブがディープ リンクを介して移動される場合、フィールドを含 [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) `subEntityId` むコンテキストを返します。

## <a name="deep-linking-from-your-tab"></a>タブからのディープ リンクの設定

タブから、Teamsにディープリンクできます。これは、タブがチャネル、メッセージ、別のタブ、スケジュール 設定ダイアログを開くなど、Teams 内の他のコンテンツにリンクする必要がある場合に便利です。 タブからディープリンクをトリガーするには、次のように呼び出す必要があります。

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

この呼び出しでは、正しい URL に移動したり、スケジュール設定やアプリのインストール ダイアログを開くなどのクライアント アクションをトリガーします。 次の例を参照してください。

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a>チャットへのディープ リンクの設定

参加者のセットを指定することで、ユーザー間のプライベート チャットへのディープ リンクを作成できます。 指定した参加者とチャットが存在しない場合、リンクは空の新しいチャットにユーザーを移動します。 ユーザーが最初のメッセージを送信するまで、新しいチャットが下書き状態で作成されます。 それ以外の場合は、チャットが存在しない場合は、ユーザーの作成ボックスに挿入するテキストと共に、チャットの名前を指定できます。 この機能は、ユーザーがチャットに移動したり、チャットを参加したり、メッセージを入力したりする手動操作を行うためのショートカットとして考えることができます。

ユースケースの例として、ボットから Office 365 ユーザー プロファイルをカードとして返す場合、このディープ リンクを使用すると、ユーザーはそのユーザーと簡単にチャットできます。

### <a name="generate-a-deep-link-to-a-chat"></a>チャットへのディープ リンクを生成する

ボット、コネクタ、またはメッセージング拡張機能カードで使用できるディープ リンクには、次の形式を使用します。

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

例: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

クエリ パラメーターは次のとおりです。

* `users`: チャットの参加者を表すユーザー ID のコンマ区切りリストです。 アクションを実行するユーザーは、常に参加者として含まれます。 現在、User ID フィールドは、電子メール アドレスADなど、UserPrincipalName の Azure ADをサポートしています。
* `topicName`: 3 人以上のユーザーとのチャットの場合、チャットの表示名のオプション フィールド。 このフィールドを指定しない場合、チャットの表示名は参加者の名前に基づいて行います。
* `message`: チャットが下書き状態の間に現在のユーザーの作成ボックスに挿入するメッセージ テキストのオプション フィールド。

ボットでこのディープ リンクを使用するには、これをカードのボタンの URL ターゲットとして指定するか、アクションの種類を使用してアクションを `openUrl` タップします。

## <a name="generate-deep-links-to-file-in-channel"></a>チャネル内のファイルへのディープ リンクを生成する

ボット、コネクタ、またはメッセージング拡張機能カードでは、次のディープ リンク形式を使用できます。

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80?tenantId=<tenantid>&fileType=<filetype>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadid>&groupId=<groupId>`

クエリ パラメーターは次のとおりです。

* `tenantId`: テナント ID の例、0d9b645f-597b-41f0-a2a3-ef103fbd91bb
* `fileType`: docx、pptx、xlsx、pdf などのサポートされているファイルの種類
* `objectUrl`: ファイルのオブジェクト URL、 `https://microsoft.sharepoint.com/teams/(filepath)`
* `baseUrl`: ファイルの基本 URL、 `https://microsoft.sharepoint.com/teams`
* `serviceName`: サービスの名前、アプリ ID
* `threadId`: threadId は、ファイルが保存されているチームのチーム ID です。 これはオプションで、ユーザーのフォルダーに保存されているファイルに対してOneDriveできません。 threadId - 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype
* `groupId`: ファイルのグループ ID ae063b79-5315-4ddb-ba70-27328ba6c31e

ファイルへのディープリンクのサンプル形式を次に示します。

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
## <a name="deep-linking-for-sharepoint-framework-tabs"></a>タブの詳細SharePoint Frameworkリンク

ボット、コネクタ、またはメッセージング拡張カードでは、次のディープ リンク形式を使用できます。 `https://teams.microsoft.com/l/entity/<AppId>/<EntityId>?webUrl=<entityWebUrl>/<EntityName>`

> [!NOTE]
> ボットがディープ リンクを含む TextBlock メッセージを送信すると、ユーザーがリンクを選択すると、新しいブラウザー タブが開きます。 これは、Chrome および Linux でMicrosoft Teamsデスクトップ アプリで発生します。
> ボットが同じディープ リンク URL を a に送信すると、ユーザーがリンクを選択すると、Teamsタブが現在のブラウザー `Action.OpenUrl` で開きます。 新しいブラウザー タブは開きません。

クエリ パラメーターは次のとおりです。

* `appID`: マニフェスト ID **fe4a8eba-2a31-4737-8e33-e5fae6fee194**.

* `entityID`: タブの構成時に指定 [したアイテム ID](~/tabs/how-to/create-tab-pages/configuration-page.md)です。たとえば **、tasklist123**.
* `entityWebUrl`: クライアントがタブのレンダリングをサポートしていない場合に使用するフォールバック URL を含むオプションのフィールド `https://tasklist.example.com/123` 。 `https://tasklist.example.com/list123/task456`
* `entityName`: タブ内のアイテムのラベルで、ディープ リンクであるタスク リスト 123 またはタスク 456 を表示するときに使用します。

例: https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&TaskList

## <a name="deep-linking-to-the-scheduling-dialog"></a>[スケジュール] ダイアログへのディープ リンク

> [!NOTE]
> この機能は現在、開発者プレビュー段階です。

組み込みのスケジュール 設定ダイアログTeams深いリンクを作成できます。 これは、ユーザーが予定表を完了したり、関連するタスクをスケジュールしたりするのに役立つ場合に特に便利です。

### <a name="generate-a-deep-link-to-the-scheduling-dialog"></a>スケジュール ダイアログへの深いリンクを生成する

ボット、コネクタ、またはメッセージング拡張カードで使用できるディープ リンクには、次の形式を使用します。 `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

例: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

クエリ パラメーターは次のとおりです。

* `attendees`: 会議の出席者を表すユーザー ID のオプションのコンマ区切りリスト。 アクションを実行するユーザーは、会議の開催者です。 [ユーザー ID] フィールドは現在、Azure AD UserPrincipalName (通常は電子メール アドレス) のみをサポートしています。
* `startTime`: イベントのオプションの開始時刻です。 これは *、2018-03-12T23:55:25+02:00* など、長い [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)形式である必要があります。
* `endTime`: イベントのオプションの終了時刻 (ISO 8601 形式)。
* `subject`: 会議の件名の省略可能なフィールドです。
* `content`: 会議の詳細フィールドのオプション フィールドです。

> [!NOTE]
> 現在、場所の指定はサポートされていません。 UTC オフセットを指定する必要があります。開始時刻と終了時刻を生成するときにタイム ゾーンを意味します。

ボットとのこのディープ リンクを使用するには、カードのボタンで URL を対象として指定するか、[ `openUrl` アクションの種類] で [アクション] をタップします。

## <a name="deep-linking-to-an-audio-or-audio-video-call"></a>音声通話または音声ビデオ通話へのディープ リンク

音声または *av* として、通話の種類と参加者を指定することで、1 人のユーザーまたはユーザーのグループに対して音声のみまたはオーディオ ビデオ通話を呼び出すディープ リンクを作成できます。 ディープ リンクが呼び出された後、呼び出しを行う前にTeamsデスクトップ クライアントから通話の確認を求めるメッセージが表示されます。 グループ呼び出しの場合は、同じディープリンク呼び出しで VoIP ユーザーのセットと PSTN ユーザーのセットを呼び出します。 

ビデオ通話の場合、クライアントは確認を求め、通話のために発信者のビデオをオンにします。 通話の受信者は、音声のみまたは音声とビデオを通じて、通話通知ウィンドウで応答Teams選択できます。

> [!NOTE]
> このディープリンクは、会議の呼び出しには使用できません。

### <a name="generate-a-deep-link-to-a-call"></a>通話へのディープ リンクを生成する

| ディープ リンク | Format | 例 |
|-----------|--------|---------|
| 音声通話を行う | https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; 、 &lt; user2&gt; | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com |
| 音声およびビデオ通話を行う | https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; 、 &lt; user2&video=true &gt; | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withvideo=true |
|オプションのパラメーター ソースを使用して音声およびビデオ通話を行う | https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; , &lt; user2&&gt; withvideo=true&source=demoApp | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withvideo=true&source=demoApp |  
| VoIP ユーザーと PSTN ユーザーの組み合わせに音声およびビデオ通話を行う | https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; ,4: &lt; phonenumber&gt; | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,4:9876543210 |
  
クエリ パラメーターは次のとおりです。
* `users`: 呼び出しの参加者を表すユーザー ID のコンマ区切りリスト。 現在、User ID フィールドは Azure AD UserPrincipalName (通常は電子メール アドレス) をサポートしています。PSTN 通話の場合は、pstn mri 4: phonenumber をサポートしています。 &lt; &gt;
* `Withvideo`: これはオプションのパラメーターで、ビデオ通話に使用できます。 このパラメーターを設定すると、呼び出し元のカメラだけがオンにされます。 通話の受信者は、通話通知ウィンドウから音声通話または音声通話とビデオ通話に応答Teams選択できます。 
* `Source`: これはオプションのパラメーターで、ディープリンクのソースを通知します。

## <a name="code-sample"></a>コード サンプル

| サンプルの名前 | 説明 | C# |Node.js|
|-------------|-------------|------|----|
|Subentity ID を使用するディープ リンク  |Microsoft Teamsチャットからサブエンティ ID を使用するタブへのディープリンクを示すサンプル アプリを作成します。|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/nodejs)|

## <a name="see-also"></a>関連項目

[Web アプリを統合する](~/samples/integrate-web-apps-overview.md)

