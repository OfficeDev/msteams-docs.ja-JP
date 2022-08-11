---
title: ディープ リンクの作成
description: この記事では、ディープ リンクを作成する方法と、タブを使用して Microsoft Teams アプリ内でディープ リンクを使用して移動する方法について説明します。
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: 9113491db788b187a86db21c97867540a35777d2
ms.sourcegitcommit: f192d7685ee3ddf4a55dc9787d56744403c3f8f9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/10/2022
ms.locfileid: "67302466"
---
# <a name="create-deep-links"></a>ディープ リンクの作成

ディープ リンクは、Teams および Teams アプリ内の情報と機能をユーザーと接続するために使用できるナビゲーション メカニズムです。 ディープ リンクの作成が役立つシナリオは次のとおりです:

* アプリのタブの 1 つにあるコンテンツにユーザーを移動します。 たとえば、アプリには、ユーザーに重要なアクティビティを通知するメッセージを送信するボットを含めることができます。 ユーザーが通知をタップすると、ディープ リンクがタブに移動し、ユーザーがアクティビティの詳細を表示できるようになります。
* アプリは、必要なパラメーターを使用してディープ リンクを事前に入力して、チャットの作成や会議のスケジュール設定などの特定のユーザー タスクを自動化または単純化します。 これにより、ユーザーが手動で情報を入力する必要がなくなります。

Microsoft Teams JavaScript クライアント SDK (TeamsJS) を使用すると、ナビゲーションのプロセスが簡略化されます。 タブ内のコンテンツや情報への移動やチャット ダイアログの起動など、SDK は多くのシナリオでエクスペリエンスを向上させ、ディープ リンクの代わりとなる、指定された API を提供します。 これらの API は、他のホスト (Outlook、Office) で実行される可能性がある Teams アプリに推奨されます。また、使用されている機能がそのホストでサポートされていることを確認する方法も提供されます。 次のセクションでは、ディープ リンクに関する情報を示しますが、TeamsJS v2 のリリースで、それを要求するために、使用されたシナリオがどのように変更されたかについても要点に注目して説明します。

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

> [!NOTE]
>
> ディープ リンクの動作は、さまざまな要因に依存します。 次の一覧では、Teams エンティティに対するディープ リンクの動作の概要を示します。
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
>
>
>Microsoft 365 (Outlook/Office) 全体にわたって拡張された Teams アプリのナビゲーションの動作は、次の 2 つの要因に依存します:
>
> * ディープ リンクが指すターゲット。
> * Teams アプリが実行されているホスト。
>
> ディープ リンクのターゲットになっているホスト内で Teams アプリが実行されている場合、アプリはホスト内で直接開きます。 しかしながら、Teams アプリが実行されている別のホストからディープ リンクのターゲットとして指している場合、アプリは最初にブラウザーで開きます。

## <a name="deep-link-to-your-tab"></a>タブへのディープ リンク

Teams アプリ内のエンティティへのディープ リンクを作成できます。 このメソッドは、タブ内のコンテンツと情報に案内するリンクを作成するために使用されます。たとえば、タブにタスク リストが含まれている場合、チーム メンバーは個々のタスクへのリンクを作成して共有できます。 リンクを選択すると、特定のアイテムに焦点を当てたタブに移動します。

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

これを実装するには、UI に最適ないずれかの方法で、**リンクのコピー** アクションを各アイテムに追加します。 ユーザーがこの操作を実行したら、[pages.shareDeepLink()](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest#@microsoft-teams-js-pages-sharedeeplink&preserve-view=true) を呼び出して、ユーザーがクリップボードにコピーできるリンクを含むダイアログ ボックスを表示します。 この呼び出しを行うときは、アイテムの ID を渡します。 リンクがフォローされ、タブが再読み込みされると、[コンテキスト](~/tabs/how-to/access-teams-context.md)に戻されます。

```javascript
pages.shareDeepLink({ subPageId: <subPageId>, subPageLabel: <subPageLabel>, subPageWebUrl: <subPageWebUrl> })
```

フィールドを適切な情報に置き換える必要があります:

* `subPageId`: ディープ リンク先であるページ内のアイテムの一意の ID。
* `subPageLabel`: ディープ リンクの表示に使用するアイテムのラベル。
* `subPageWebUrl`: クライアントがページをレンダリングできない場合に使用するフォールバック URL。

詳細については、「[pages.shareDeepLink()](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest#@microsoft-teams-js-pages-sharedeeplink&preserve-view=true)」を参照してください。

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

これを実装するには、各アイテムに **リンクのコピー** アクションを UI に最適な方法で追加します。 このアクションを実行すると、 `shareDeepLink()` を呼び出して、ユーザーがクリップボードにコピーできるリンクを含むダイアログボックスを表示します。 この呼び出しを行うと、アイテムの ID も渡されます。この ID は、リンクに従って、タブを再読み込みするとき、[コンテキスト](~/tabs/how-to/access-teams-context.md)に戻されます。

```javascript
microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })
```

フィールドを適切な情報に置き換える必要があります:

* `subEntityId`: ディープ リンクしているタブ内のアイテムの一意の識別子。
* `subEntityLabel`: ディープ リンクの表示に使用するアイテムのラベル。
* `subEntityWebUrl`: クライアントがタブのレンダリングをサポートしていない場合に使用するフォールバック URL を含むオプションのフィールド。

---

または、この記事で後述する形式を使用して、プログラミングして、ディープ リンクを作成することもできます。 タブまたはタブ内のアイテムへの変更についてユーザーに通知する[ボット](~/bots/what-are-bots.md)および[コネクター](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) メッセージでディープ リンクを使用できます。

> [!NOTE]
> このディープリンクは、**[タブへのリンクのコピー]** メニュー項目によって提供されるリンクとは異なります。このメニュー項目は、このタブを指すディープ リンクを生成するだけです。

>[!IMPORTANT]
> 現在、shareDeepLinkは、モバイル プラットフォームでは機能しません。

### <a name="consume-a-deep-link-from-a-tab"></a>タブからディープ リンクを使用する

ディープ リンクにアクセスすると、Microsoft Teams はそのタブに移動し、サブページ ID が存在する場合は Teams JavaScript ライブラリを使用して取得するメカニズムを提供します。

TeamsJS v1 の [`app.getContext()`](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-getcontext&preserve-view=true) 呼び出し (`microsoftTeams.getContext()`) は、`subPageId` プロパティ (TeamsJS v1 の subEntityId) を含むコンテキストで解決される promise を返します (タブがディープ リンクを介して移動される場合)。 詳細については、「[PageInfo インターフェース](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-pageinfo&preserve-view=true)」を参照してください。

### <a name="generate-a-deep-link-to-your-tab"></a>タブへのディープ リンクを生成する

タブへのディープ リンクを生成するために `shareDeepLink()` を使用することをお勧めしますが、手動で作成することもできます。

> [!NOTE]
>
> * 個人用タブには `personal` スコープがあり、チャネル タブとグループ タブには `team` または `group` スコープが使用されます。 構成可能なタブだけがコンテキスト オブジェクトに関連付けられている `channel` プロパティを持つため、2 つのタブの種類の構文はわずかに異なります。 タブ スコープの詳細については、 [マニフェスト](~/resources/schema/manifest-schema.md) リファレンスを参照してください。
> * ディープ リンクは、タブが v0.4 以降のライブラリを使用して構成されていて、そのためエンティティ ID がある場合にのみ正常に機能します。 エンティティ ID のないタブへのディープ リンクは引き続きタブに移動しますが、サブエンティティ ID をタブに提供することはできません。

ボット、コネクタ、またはメッセージング拡張カードで使用できるディープ リンクには、次の形式を使用します:

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> ボットがディープ リンクを使用して `TextBlock` を含むメッセージを送信する場合、ユーザーがリンクを選択すると、新しいブラウザー タブが開きます。 これは、Chrome および Teams デスクトップ アプリ (いずれも Linux で実行されています) で発生します。
> ボットが同じディープ リンク URL を `Action.OpenUrl` に送信した場合、ユーザーがリンクを選択すると、現在のブラウザ タブで Teams タブが開きます。 新しいブラウザー タブは開きません。

<!--- TBD: Edit this article.
* Admonitions/alerts seem to be overused. 
* An important alert at the end of this table does not make sense. Also, it has a code snippet inside it.
* List items in the table are not formatted well in output.
* Some headings use -ing verbs.
* Example values and some URLs should be in backticks and not emphasized.
* Codeblock are missing language.
* Check for markdownlint errors.
* Table with just a row isn't really needed. Provide the content without tabulating it.
--->

クエリ パラメーターは次のとおりです。

| パラメーター名 | 説明 | 例 |
|:------------|:--------------|:---------------------|
| `appId`&emsp; | Teams 管理センターからの ID。 |fe4a8eba-2a31-4737-8e33-e5fae6fee194|
| `entityId`&emsp; | [タブの構成](~/tabs/how-to/create-tab-pages/configuration-page.md)時に指定したタブ内のアイテムの ID です。ディープ リンク用の URL を生成する場合は、引き続き entityID を URL のパラメーター名として使用します。 タブを構成する際は、コンテキスト オブジェクトは entityID を {page.id} として参照します。 |Tasklist123|
| `entityWebUrl` または `subEntityWebUrl`&emsp; | クライアントがタブのレンダリングをサポートしていない場合に使用するフォールバック URL を含むオプションのフィールド。 | `https://tasklist.example.com/123` または `https://tasklist.example.com/list123/task456` |
| `entityLabel` または `subEntityLabel`&emsp; | ディープ リンクを表示するときに使用する、タブ内のアイテムのラベル。 | タスク リスト 123 または "タスク 456" |
| `context.subEntityId`&emsp; | タブ内のアイテムの ID です。ディープ リンク用の URL を生成する際は、URL のパラメーター名として subEntityId を引き続き使用します。 タブを構成する場合、コンテキスト オブジェクトは subEntityID を subPageID として参照します。 |Task456 |
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
> すべてのクエリ パラメーターが適切に URI にエンコードされていることを確認します。 最後の例を使用して、前述の例に従う必要があります:
>
> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

## <a name="navigation-from-your-tab"></a>タブからのナビゲーション

TeamsJS またはディープ リンクを使用して、タブから Teams 内のコンテンツに移動できます。 これは、タブでユーザーを Teams の他のコンテンツであるチャンネル、メッセージ、別のタブなどに接続したり、スケジュール ダイアログを開いたりする必要がある場合にも便利です。 以前は、ナビゲーションにはディープ リンクが必要だったかもしれませんが、多くのインスタンスで SDK を使用して実現できるようになりました。 以降のセクションでは両方の方法について説明しますが、可能な場合 SDK の型指定を活用することが推奨されます。

TeamsJS を使用する利点の 1 つは、特に他のホスト (Outlook と Office) で実行される可能性がある Teams アプリの場合に、使用しようとしている機能をホストがサポートしていることを確認できる点です。 ホストによる機能のサポートを確認するには、API の名前空間に関連付けられている `isSupported()` 関数を使用できます。 TeamsJS SDK は、名前空間を通じて API を系統的に機能化します。 たとえば、 `pages` 名前空間における API の用法に先立ち、`pages.isSupported()` から返されたブール値を確認し、アプリとアプリ UI のコンテキスト内で適切なアクションを実行できます。  

TeamsJS の機能と API の詳細については、「[Microsoft Teams JavaScript クライアント SDK を使用したタブとその他のホスト エクスペリエンスの構築](~/tabs/how-to/using-teams-client-sdk.md#apis-organized-into-capabilities)」を参照してください。

### <a name="navigate-within-your-app"></a>アプリ内を案内する

TeamsJS を使用してアプリを操作できます。 次のコードは、Teams アプリ内の特定のエンティティに移動する方法を示しています。

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

次のコードに示すように、[pages.navigateToApp()](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest#@microsoft-teams-js-pages-navigatetoapp&preserve-view=true) 関数を使用してタブからナビゲーションをトリガーできます。

```javascript
if (pages.isSupported()) {
  const navPromise = pages.navigateToApp({ appId: <appId>, pageId: <pageId>, webUrl: <webUrl>, subPageId: <subPageId>, channelId:<channelId>});
  navPromise.
     then((result) => {/*Successful navigation*/}).
     catch((error) => {/*Failed navigation*/});
}
else { /* handle case where capability isn't supported */ }
```

ページ機能の使用の詳細については、「[pages.navigateToApp()](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest#@microsoft-teams-js-pages-navigatetoapp&preserve-view=true) とその他のナビゲーション オプションのための [pages](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest&preserve-view=true) 名前空間」を参照してください。 必要に応じて、[app.openLink()](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-openlink&preserve-view=true) 関数を使用してディープ リンクを直接開くこともできます。

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

タブからディープ リンクをトリガーするには、次を呼び出します:

```javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

---

### <a name="open-a-scheduling-dialog"></a>スケジュール設定ダイアログを開く

> [!NOTE]
> Teams でスケジュール設定ダイアログを開くには、Teams がまだカレンダー機能をサポートしていないため、開発者は元のディープリンク URL ベースのメソッドを引き続き使用する必要があります。

カレンダーの操作の詳細については、API リファレンス ドキュメントの[カレンダー](/javascript/api/@microsoft/teams-js/calendar?view=msteams-client-js-latest&preserve-view=true)名前空間を参照してください。

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```javascript
// Open a scheduling dialog from your tab
if(calendar.isSupported()) {
   const calendarPromise = calendar.composeMeeting({
      attendees: ["joe@contoso.com", "bob@contoso.com"],
      content: "test content",
      endTime: "2018-10-24T10:30:00-07:00",
      startTime: "2018-10-24T10:00:00-07:00",
      subject: "test subject"});
   calendarPromise.
      then((result) => {/*Successful operation*/}).
      catch((error) => {/*Unsuccessful operation*/});
}
else { /* handle case where capability isn't supported */ }
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");
```

---

または、Teams の組み込みのスケジューリング ダイアログへのディープ リンクを手動で作成できます。

#### <a name="generate-a-deep-link-to-the-scheduling-dialog"></a>スケジュール設定ダイアログへのディープ リンクを作成する

TeamsJS の型指定された API を使用することをお勧めしますが、Teams の組み込みスケジュール ダイアログへのディープ リンクを手動で作成することもできます。 ボット、コネクタ、またはメッセージ拡張カードで使用できるディープ リンクには、次の形式を使用します: `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

例: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

> [!NOTE]
> 検索パラメーターは、空白 (``) の代わりに `+` シグナルをサポートしていません。 URI エンコーディング コードがスペースに対して `%20` を返すことを確認します。たとえば、`?subject=test%20subject` は適切ですが、`?subject=test+subject` は不適切です。

クエリ パラメーターは次のとおりです。

* `attendees`: 会議の参加者を表すユーザー ID のオプションのコンマ区切りリスト。 アクションを実行するユーザーは、会議の開催者です。 現在、[ユーザー ID] フィールドは、一般的には電子メールアドレスの、Azure AD UserPrincipalName をサポートしています。
* `startTime`: イベントのオプションの開始時間。 これは、[long ISO 8601 形式](https://en.wikipedia.org/wiki/ISO_8601) ( 例: *2018-03-12T23:55:25+02:00*)である必要があります。
* `endTime`: イベントの終了時刻 (省略可能、 ISO 8601形式)。
* `subject`: 会議の件名の省略可能なフィールド。
* `content`: 会議の詳細フィールドの省略可能なフィールド。

> [!NOTE]
> 現在、場所の指定はサポートされていません。UTC オフセットを指定する必要があります。これは、開始時刻と終了時刻を生成するときのタイム ゾーンを意味します。

ボットとのこのディープ リンクを使用するには、カードのボタンで URL を対象として指定するか、[ `openUrl` アクションの種類] で [アクション] をタップします。

### <a name="open-an-app-install-dialog"></a>アプリのインストール ダイアログを開く

次のコードに示すように、Teams アプリからアプリのインストール ダイアログを開くことができます。

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```javascript
// Open an app install dialog from your tab
if(appInstallDialog.isSupported()) {
    const dialogPromise = appInstallDialog.openAppInstallDialog({ appId: <appId>});
    dialogPromise.
      then((result) => {/*Successful operation*/}).
      catch((error) => {/*Unsuccessful operation*/});
}
else { /* handle case where capability isn't supported */ }
```

インストール ダイアログの詳細については、API リファレンス ドキュメントの [appInstallDialog.openAppInstallDialog()](/javascript/api/@microsoft/teams-js/appinstalldialog?view=msteams-client-js-latest#@microsoft-teams-js-appinstalldialog-openappinstalldialog&preserve-view=true) 関数を参照してください。

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```javascript
// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

---

### <a name="navigate-to-a-chat"></a>チャットに移動する

参加者の組を指定することで、TeamsJS を使いユーザー間のプライベート チャットへのディープ リンクを操作、または作成できます。 指定された参加者とチャットが存在しない場合、ユーザーは空白の新しいチャットに案内されます。 新しいチャットは、ユーザーが最初のメッセージを送信するまで下書き状態で作成されます。 それ以外の場合は、チャットの名前がまだ存在しない場合は、ユーザーの作成ボックスに挿入する必要のあるテキストとともに指定できます。 この機能は、ユーザーがチャットに移動したり、チャットを参加したり、メッセージを入力したりする手動操作を行うためのショートカットとして考えることができます。

ユースケースの例として、ボットから Office 365 ユーザー プロファイルをカードとして返す場合、このディープ リンクを使用すると、ユーザーはそのユーザーと簡単にチャットできます。 次の例では、初回のメッセージとともに参加者グループにチャット メッセージを開示する方法を示します。

```javascript
if(chat.isSupported()) {
    const chatPromise = chat.openGroupChat({ users: ["joe@contoso.com","bob@contoso.com"], topic: "Prep For Meeting Tomorrow", message: "Hi folks kicking off chat about our meeting tomorrow"});
    chatPromise.
      then((result) => {/*Successful operation*/}).
      catch((error) => {/*Unsuccessful operation*/});
}
else { /* handle case where capability isn't supported */ }
```

型指定された API の使用をお勧めしますが、ボット、コネクタ、またはメッセージ拡張カードで使用できる手動で作成されたディープ リンクには、次の形式を使用することもできます。

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

例: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

クエリ パラメーターは次のとおりです。

* `users`: チャットの参加者を表すユーザー ID のコンマで区切られたリスト。 アクションを実行するユーザーは、常に参加者として含まれます。 現在、[ユーザーID] フィールドは、メール アドレスのみなどの Microsoft Azure Active Directory (Azure AD) UserPrincipalName をサポートしています。
* `topicName`: チャットに 3 人以上のユーザーがいる場合の、チャットの表示名の省略可能なフィールドです。 このフィールドが指定されていない場合、チャットの表示名は参加者の名前に基づいています。
* `message`: チャットがドラフト状態のときに現在のユーザーの作成ボックスに挿入するメッセージ テキストのオプションのフィールド。

ボットでこのディープ リンクを使用するには、これをカードのボタンの URL ターゲットとして指定するか、`openUrl` アクション タイプでアクションをタップします。

### <a name="generate-deep-links-to-channel-conversation"></a>チャネル会話へのディープ リンクを生成する

このディープ リンク形式を使用して、以下のチャネル スレッド内の特定の会話に移動します。

`https://teams.microsoft.com/l/message/<channelId>/<parentMessageId>?tenantId=<tenantId>&groupId=<groupId>&parentMessageId=<parentMessageId>&teamName=<teamName>&channelName=<channelName>&createdTime=<createdTime>`

例: `https://teams.microsoft.com/l/message/<channelId>/1648741500652?tenantId=<tenantId>&groupId=<groupId>&parentMessageId=1648741500652&teamName=<teamName>&channelName=<channelName>&createdTime=1648741500652`

クエリ パラメーターは次のとおりです。

* `channelId`: 会話のチャネル ID。 たとえば、「 `19:3997a8734ee5432bb9cdedb7c432ae7d@thread.tacv2` 」のように入力します。
* `tenantId`: `0d9b645f-597b-41f0-a2a3-ef103fbd91bb` などのテナント ID。
* `groupId`: ファイルのグループ ID。 たとえば、「 `3606f714-ec2e-41b3-9ad1-6afb331bd35d` 」のように入力します。
* `parentMessageId`: 会話の親メッセージ ID。
* `teamName`: チームの名前。
* `channelName`: チームのチャネルの名前。

> [!NOTE]
> チャネルからの URL に `channelId` と `groupId` が表示されます。

### <a name="generate-deep-links-to-file-in-channel"></a>チャネル内のファイルへのディープ リンクを生成する

次のディープ リンク形式は、ボット、コネクタ、またはメッセージ拡張カードで使用されます: 

`https://teams.microsoft.com/l/file/<fileId>?tenantId=<tenantId>&fileType=<fileType>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadId>&groupId=<groupId>`

クエリ パラメーターは次のとおりです。

* `fileId`: Sharepoint Online の一意のファイル ID (`sourcedoc` とも呼ばれます)。たとえば、`1FA202A5-3762-4F10-B550-C04F81F6ACBD` です。
* `tenantId`: `0d9b645f-597b-41f0-a2a3-ef103fbd91bb` などのテナント ID。
* `fileType`: .docx、.pptx、.xlsx、.pdf などのサポートされているファイルの種類
* `objectUrl`: ファイルのオブジェクト URL。 形式は `https://{tenantName}.sharepoint.com/sites/{TeamName}/SharedDocuments/{ChannelName}/FileName.ext` です。 たとえば、「 `https://microsoft.sharepoint.com/teams/(filepath)` 」のように入力します。
* `baseUrl`: ファイルのベース URL。 形式は `https://{tenantName}.sharepoint.com/sites/{TeamName}` です。 たとえば、「 `https://microsoft.sharepoint.com/teams` 」のように入力します。
* `serviceName`: サービスの名前、アプリ ID。 たとえば、「 `teams` 」のように入力します。
* `threadId`: threadId は、ファイルが保存されているチームのチーム ID です。 これはオプションであり、ユーザーの OneDrive フォルダーに保存されているファイルには設定できません。 threadId - 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype.
* `groupId`: ファイルのグループ ID。 たとえば、「 `ae063b79-5315-4ddb-ba70-27328ba6c31e` 」のように入力します。

> [!NOTE]
> チャネルからの URL に `threadId` と `groupId` が表示されます。  

次のディープ リンク形式は、ボット、コネクタ、またはメッセージ拡張カードで使用されます: 

`https://teams.microsoft.com/l/file/<fileId>?tenantId=<tenantId>&fileType=<fileType>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadId>&groupId=<groupId>`

次のフォーマット例は、ファイルへのディープ リンクを示しています。

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80?tenantId=0d9b645f-597b-41f0-a2a3-ef103fbd91bb&fileType=pptx&objectUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform%2FShared%20Documents%2FFC7-%20Bot%20and%20Action%20Infra%2FKaizala%20Actions%20in%20Adaptive%20Cards%20-%20Deck.pptx&baseUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform&serviceName=teams&threadId=19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype&groupId=ae063b79-5315-4ddb-ba70-27328ba6c31e`

#### <a name="serialization-of-this-object"></a>このオブジェクトのシリアル化

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

### <a name="deep-linking-to-an-app"></a>アプリへのディープ リンク

アプリが Teams ストアの一覧に表示されたら、アプリのディープ リンクを作成します。 Teams を起動するためのリンクを作成するには、アプリ ID を次の URL に追加します: `https://teams.microsoft.com/l/app/<your-app-id>`。 アプリをインストールするダイアログ ボックスが表示されます。

> [!NOTE]
> 現在、アプリへのディープ リンクはモバイル プラットフォームではサポートされていません。

### <a name="deep-linking-for-sharepoint-framework-tabs"></a>SharePoint Framework タブのディープ リンク

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

### <a name="navigate-to-an-audio-or-audio-video-call"></a>音声通話または音声ビデオ通話への案内

通話の種別と参加者を指定することで、1 人のユーザーまたはユーザーのグループに対してオーディオのみの通話または音声ビデオ通話を呼び出すことができます。 通話を発信する前に、Teams クライアントはその確認を促します。 グループ通話の場合、同じディープ リンク呼び出しで一連の VoIP ユーザーと一連の PSTN ユーザーを呼び出すことができます。

ビデオ通話の場合、クライアントは確認を求め、通話の発信者のビデオをオンにします。 通話の受信者は、Teams の通話通知ウィンドウを使用して、音声のみで応答するか、音声とビデオで応答するかを選択できます。

> [!NOTE]
> この方法は、会議の実施には使用できません。

次のコードは、TeamsJS SDK を使用して通話を開始する方法を示しています:

```javascript
if(call.isSupported()) {
    const callPromise = call.startCall({ targets: ["joe@contoso.com","bob@contoso.com","4:9876543210"], requestedModalities: [call.CallModalities.Audio], source: "demoApp"});
    callPromise.
      then((result) => {/*Successful operation*/}).
      catch((error) => {/*Unsuccessful operation*/});
}
else { /* handle case where capability isn't supported */ }

```

#### <a name="generate-a-deep-link-to-a-call"></a>通話へのディープ リンクを生成する

TeamsJS の型指定された API の使用をお勧めしますが、手動で作成されたディープ リンクを使用して通話を開始することもできます。

| ディープ リンク | フォーマット | 例 |
|-----------|--------|---------|
| 音声通話を行う | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com` |
| 音声またはビデオ通話を開始する | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>&withVideo=true` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withVideo=true` |
|オプションのパラメータ ソースを使用して音声通話とビデオ通話を発信する | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>&withVideo=true&source=demoApp` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withVideo=true&source=demoApp` |  
| VoIP ユーザーと PSTN ユーザーの組み合わせに音声通話とビデオ通話を発信する | `https://teams.microsoft.com/l/call/0/0?users=<user1>,4:<phonenumber>` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,4:9876543210` |
  
クエリ パラメーターは次のとおりです。

* `users`: 通話の参加者を表すユーザー ID のコンマで区切られたリスト。 現在、[ユーザー ID] フィールドは Azure AD UserPrincipalName (通常はメール アドレス) をサポートしています。PSTN 通話の場合は、pstn mri 4: &lt;phonenumber&gt; をサポートしています。
* `withVideo`: これはオプションのパラメータであり、ビデオ通話を行うために使用できます。 このパラメータを設定すると、発信者のカメラだけがオンになります。 通話の受信者は、Teams の通話通知ウィンドウから音声通話または音声通話とビデオ通話を選択できます。
* `Source`: これはオプションのパラメーターで、ディープ リンクのソースを通知します。

## <a name="code-sample"></a>コード サンプル

| サンプルの名前 | 説明 | C# |Node.js|
|-------------|-------------|------|----|
|Subentity ID を使用するディープ リンク  | ボット チャットからタブに消費するサブエンティティ ID へのディープ リンクを示す Teams サンプル アプリ。|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/nodejs)|

## <a name="see-also"></a>関連項目

* [Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
* [Moodle LMS](~/resources/moodleinstructions.md)
