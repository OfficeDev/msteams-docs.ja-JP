---
title: 仮想テーブル エンティティ参照
author: surbhigupta
description: このモジュールでは、Microsoft Teams での仮想テーブル エンティティの参照とその属性について説明します。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 98e9ee6a2bc565c35a9b46c2990a7c548dab2e31
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243053"
---
# <a name="virtual-tables-entity-reference"></a>仮想テーブル エンティティ リファレンス

コラボレーション コントロールの仮想エンティティとその属性には、特定の Microsoft Graph リソースの種類を持つ 1 対 1 のマッピングがあります。 たとえば、Graph Planner タスク エンティティは [、Microsoft Graph Planner タスク リソースの種類](/graph/api/resources/plannertask)にマップされます。 仮想エンティティは、リソースの種類と同じ属性を共有します。

> [!NOTE]
> 現在、コラボレーション コントロールは [パブリック開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)でのみ使用できます。

## <a name="collaboration-controls-virtual-entities"></a>コラボレーションが仮想エンティティを制御する

| 名前 | 説明 |
|---|---|
| Graph Planner タスク | Graph Planner タスク テーブルは、Microsoft 365 の Planner タスクを表します。 |
| Graph Planner プラン | Graph Planner プラン テーブルは、Microsoft 365 の Planner プランを表します。 |
| Graph イベント | Graph イベント テーブルは、ユーザー予定表のイベント、または Microsoft 365 グループの既定の予定表を表します。 |
| Graph Booking Appointment | Graph Booking Appointment テーブルは、一連のスタッフ メンバーによって実行される Booking Service の顧客の予定を表し、Microsoft Bookingsのビジネスによって証明されます。 |
| Graph Drive | Graph Drive テーブルは、ユーザーの OneDrive または SharePoint のドキュメント ライブラリを表す最上位オブジェクトを表します。 |
| Graph Drive アイテム | Graph Drive Item テーブルは、ドライブに格納されているファイル、フォルダー、またはその他の項目を表します。 |

## <a name="graph-planner-task"></a>Graph Planner タスク

* エンティティ名: m365_graphplannertask。
* グラフ リソース: [plannerTask リソースの種類](/graph/api/resources/plannertask)
* 並べ替えはサポートされていません。
* フィルター処理はサポートされていません。
* サーバー駆動型の改ページネーションがサポートされており、最大ページ サイズは 400 です。

### <a name="attributes-for-graph-planner-task"></a>Graph Planner タスクの属性

| Column  | Dataverse 型 | 詳細 |
|---|---|---|
| `m365_collaborationrootid` | 文字列 | コラボレーション セッション レコードのコラボレーション ルート ID は、複数のコラボレーション セッションに関連付けられます。 これはコンマ区切り文字列として返されます。 この属性は、複数のレコードを取得するときに返されないことに注意してください。 |
| `m365_activechecklistitemcount` | Int32 | 不完全な項目を表す、値が false に設定されたチェックリスト項目の数。 |
| `m365_graphplannertaskId` | Guid | グラフ プランナー タスクの一意の識別子。 |
| `m365_appliedcategories` | 文字列 | 不完全な項目を表す、値が false に設定されたチェックリスト項目の数。 |
| `m365_appliedcategories` | 文字列 | タスクが適用されているカテゴリ。 この属性は JSON でエンコードされた文字列です。例: "{ \"category1\": true, \"category6\": true, \"category9\": true }" |
| `m365_assigneepriority` | 文字列 | リスト ビューでこの種類の項目を並べ替えるために使用されるヒント。 この形式は、 [Planner で順序ヒントを使用して](/graph/api/resources/planner-order-hint-format)アウトラインとして定義されます。 |
| `m365_assignments` | 文字列 | 割り当て先のセット。タスクが割り当てられます。 この属性は、"{\" 7be....\": {assignedBy\": {\"user\": {\"\"displayName\", email\", \"\"ID\": 7be...\"}, \"group\":\" null, \"application\": null \"device\": null}" などの JSON でエンコードされた文字列です。 |
| `m365_bucketid` | String | タスクが属しているバケット ID。 バケットは、タスクが存在している計画に含まれている必要があります。 28 文字の長さと大文字と小文字が区別されます。 [書式検証](/graph/api/resources/planner-identifiers-disclaimer)はサービスによって行われます。 |
| `m365_checklistitemcount` | Int32 | タスクに存在するチェックリストの項目の数です。 |
| `m365_completedby` | 文字列 | タスクを完了したユーザーの ID。 この属性は JSON でエンコードされた文字列です。たとえば、{\"user: {\"displayName,ID\"\"\":\"d55...\"}}\" |
| `m365_completeddatetime` | DateTime | 読み取り専用です。 タスクの 'percentComplete' が '100' に設定されている日付と時刻。 Timestamp 型は、ISO 8601 形式を使用して日付と時刻の情報を表し、常に UTC 時間です。 たとえば、2014 年 1 月 1 日の午前 0 時の UTC は 2014-01-01T00:00:00Z です。 |
| `m365_conversationthreadid` |文字列 | タスク上の会話のスレッド ID。 これは、グループに作成された会話スレッド オブジェクトの ID です。 |
| `m365_createdby` | 文字列 | タスクを作成したユーザーの ID。 この属性は JSON でエンコードされた文字列です。たとえば、{\"user: {\"displayName,ID\"\"\":\"d55...\"}}\" |
| `m365_createddatetime` | DateTime | 読み取り専用。 タスクが作成された日時。 Timestamp 型は、ISO 8601 形式を使用して日付と時刻の情報を表し、常に UTC 時間です。 たとえば、2014 年 1 月 1 日の午前 0 時の UTC は 2014-01-01T00:00:00Z です。 |
| `m365_duedatetime` | DateTime | タスクが期限切れになる日時。 Timestamp 型は、ISO 8601 形式を使用して日付と時刻の情報を表し、常に UTC 時間です。 たとえば、2014 年 1 月 1 日の午前 0 時の UTC は 2014-01-01T00:00:00Z です。 |
| `m365_hasdescription` | ブール型 | 読み取り専用です。 タスクの details オブジェクトに空でない説明がある場合は true、それ以外の場合は false です。 |
| `m365_id` | String | 読み取り専用。 タスクの ID。 28 文字の長さと大文字と小文字が区別されます。 [書式検証](/graph/api/resources/planner-identifiers-disclaimer)はサービスによって行われます。|
| `m365_orderhint` | 文字列 | リスト ビューでこの種類の項目を並べ替えるために使用されるヒント。 この形式は、 [Planner で順序ヒントを使用して](/graph/api/resources/planner-order-hint-format)アウトラインとして定義されます。 |
| `m365_percentcomplete` | Int32 | タスク完了の割合。 100 に設定すると、タスクは完了したと見なされます。 |
| `m365_priority` | Int32 | タスクの優先度。 有効な値の範囲は 0 ~ 10 で、値の増加は優先度が低くなります (0 は優先度が最も高く、10 は優先順位が最も低くなります)。 現在、Planner は値 0 と 1 を "緊急" として解釈し、2、3、4 は "重要"、5、6、7 は "中"、8、9、10 は "低" と解釈します。 さらに、Planner は値 1 を "緊急" に、3 を "重要" に、5 を "中" に、9 を "低" に設定します。 |
| `m365_planid` | String | タスクが属している計画 ID。 |
| `m365_previewtype` | String | タスクに表示されるプレビューの種類を設定します。 可能な値は、自動、noPreview、チェックリスト、説明、リファレンスです。 |
| `m365_referencecount` | Int32 | タスクに上に存在している外部への参照の数。|
| `m365_startdatetime` | DateTime | タスクが開始される日時。 Timestamp 型は、ISO 8601 形式を使用して日付と時刻の情報を表し、常に UTC 時間です。 たとえば、2014 年 1 月 1 日の午前 0 時の UTC は 2014-01-01T00:00:00Z です。 |
| `m365_title` | String |タスクのタイトル。 プライマリ参照列 |

## <a name="graph-planner-plan"></a>Graph Planner プラン

* エンティティ名: m365_graphplannerplan。
* グラフ リソース: [plannerPlan リソースの種類](/graph/api/resources/plannerplan)。
* 並べ替えはサポートされていません。
* フィルター処理はサポートされていません。
* サーバー駆動型の改ページネーションがサポートされており、最大ページ サイズは 400 です。

### <a name="attributes-for-graph-planner-plan"></a>Graph Planner プランの属性

| Column  | Dataverse 型 | 詳細 |
|---|---|---|
| `m365_collaborationrootid` | 文字列 | レコードが関連付けられているコラボレーション セッションのコラボレーション ルート ID。 レコードが複数のコラボレーション セッションに関連付けられている場合は、コンマで区切られた文字列として返されます。 この属性は、複数のレコードを取得するときに返されないことに注意してください。|
| `m365_graphplannerplanid` |Guid |グラフ プランナー プランの一意の識別子。|
| `m365_createdby` | 文字列 | タスクを作成したユーザーの ID。 この属性は JSON でエンコードされた文字列です。たとえば、{\"user: {\"displayName,ID\"\"\":\"d55...\"}}\" |
| `m365_createddatetime` | DateTime | 読み取り専用。 タスクが作成された日時。 Timestamp 型は、ISO 8601 形式を使用して日付と時刻の情報を表し、常に UTC 時間です。 たとえば、2014 年 1 月 1 日の午前 0 時の UTC は 2014-01-01T00:00:00Z です。 |
| `m365_id` | String | 読み取り専用です。 計画の ID。 28 文字の長さと大文字と小文字が区別されます。 [書式検証](/graph/api/resources/planner-identifiers-disclaimer)はサービスによって行われます。|
| `m365_owner` | 文字列 | 計画を所有している [Group](/graph/api/resources/group) の ID。 設定した後、このプロパティを更新することはできません。|
| `m365_title` | 文字列 | プランのタイトル。 プライマリ参照列 |

## <a name="graph-event"></a>Graph イベント

* エンティティ名: m365_graphevent
* Graph リソース: [イベント リソースの種類](/graph/api/resources/event)
* 並べ替えは、次の列でサポートされています。
  * m365_lastmodifieddatetime
  * m365_createddatetime
  * m365_hasattachments
  * m365_importance
  * m365_responserequested
  * m365_sensitivity
  * m365_showas
  * m365_subject
* フィルター処理は、次の列でサポートされています。
  * m365_allownewtimeproposals
  * m365_lastmodifieddatetime
  * m365_createddatetime
  * m365_icaluID
  * m365_importance
  * m365_isallday
  * m365_iscancelled
  * m365_isdraft
  * m365_responserequested
  * m365_sensitivity
  * m365_showas
  * m365_subject
  * m365_type
* サーバー駆動型の改ページネーションがサポートされています。

### <a name="attributes-for-graph-event"></a>Graph イベントの属性

| Column |Dataverse 型 |詳細 |
|---|---|---|
|`m365_collaborationrootid` |文字列 |レコードが関連付けられているコラボレーション セッションのコラボレーション ルート。 レコードが複数のコラボレーション セッションに関連付けられている場合は、コンマで区切られた文字列として返されます。 この属性は、複数のレコードを取得するときに返されないことに注意してください。 |
|`m365_allownewtimeproposals` |ブール型 |True の場合、会議の開催者は、応答時に新しい時間を提案する招待を許可します。 それ以外の場合は false。省略可能です。 既定値は true です。 |
|`m365_attendees` |文字列 |イベントの出席者のコレクション。 この属性は JSON でエンコードされた文字列で、最大長は 15,000 です。 たとえば、{type:required,status\"\"\":{\"response\":\"none,time\"\"\":\"0001-01-01T00:00:00Z\"}},\"emailAddress\":\"test@contoso.com\"}}\"\"\" |
|`m365_body` |文字列 |イベントに関連付けられたメッセージの本文。 HTML 形式またはテキスト形式にできます。 この属性は JSON でエンコードされた文字列で、最大長は 15,000 です。 たとえば{contentType:html,content\"\"\":\"html/html\"}\"\"\" |
|`m365_bodypreview` |文字列 |イベントに関連付けられたメッセージのプレビュー。 テキスト形式です。 |
|`m365_categories` |String |イベントに関連付けられたカテゴリ。 各カテゴリは、ユーザーに対して定義されている outlookCategory の displayName プロパティに対応しています。 たとえば [\"string\"] |
|`m365_changekey` |文字列 |Identifies the version of the event object. Every time the event is changed, ChangeKey changes as well. This allows Exchange to apply changes to the correct version of the object. |
|`m365_createddatetime` |DateTime |Timestamp 型は、ISO 8601 形式を使用して日付と時刻の情報を表し、常に UTC 時間です。 たとえば、2014 年 1 月 1 日の午前 0 時の UTC は 2014-01-01T00:00:00Z です。 |
|`m365_start` |DateTime |イベントの開始日、時間、タイム ゾーン。 この属性は JSON でエンコードされた文字列で、最大長は 100 です。 たとえば{dateTime:2022-01-19T11:00:00+00:00,timeZone\"\"\":\"UTC}\"\"\"\"|
|`m365_end` |DateTime |イベントが終了する日付、時刻、タイムゾーン。 この属性は JSON でエンコードされた文字列で、最大長は 100 です。 たとえば{dateTime:2022-01-19T11:00:00+00:00,timeZone\"\"\":\"UTC}\"\"\"\" |
|`m365_hasattachments` |Boolean |イベントに添付ファイルが含まれている場合、true に設定します。 |
|`m365_hideattendees` |ブール型 |true に設定すると、各出席者は会議出席依頼と会議の追跡リストにのみ表示されます。 既定値は false です。 |
|`m365_icaluid` |String |予定表全体のイベントの固有識別子。 この ID は、定期的なアイテムの出現ごとに異なります。 読み取り専用。 |
|`m365_isallday`|ブール型 |Set to true if the event lasts all day. If true, regardless of whether it's a single-day or multi-day event, start and end time must be set to midnight and be in the same time zone. |
|`m365_iscancelled` |ブール値 |イベントがキャンセルされた場合に、true に設定します。 |
|`m365_id`| String |読み取り専用です。 イベントの ID。 |
|`m365_isdraft` |ブール型 |ユーザーが Outlook で会議を更新したが、出席者に更新プログラムを送信していない場合は true に設定します。 すべての変更が送信されている場合、またはイベントが出席者のいない予定の場合は、false に設定します。|
|`m365_isonlinemeeting`|ブール型|True の場合、このイベントにオンライン会議情報 (つまり、onlineMeeting が onlineMeetingInfo リソースを指します)、それ以外の場合は false。 既定値は false です (onlineMeeting は null です)。 オプション。 isOnlineMeeting を true に設定すると、Microsoft Graph によって onlineMeeting が初期化されます。 後の Outlook では、isOnlineMeeting に対するそれ以上の変更は無視され、会議はオンラインで引き続き利用できます。|
|`m365_isorganizer`|ブール型|予定表の所有者 (calendar の owner プロパティで指定) がイベントの主催者 (event の organizer プロパティで指定) の場合、true に設定されます。 代理人が所有者の代わりにイベントを主催した場合にも適用されます。|
|`m365_isremindero`n|Boolean|ユーザーにイベントを通知するアラートを設定する場合は、true に設定します。|
|`m365_lastmodifieddatetime`|DateTime|Timestamp 型は、ISO 8601 形式を使用して日付と時刻の情報を表し、常に UTC 時間です。 たとえば、2014 年 1 月 1 日の午前 0 時の UTC は 2014-01-01T00:00:00Z です。|
|`m365_location`|文字列|イベントの場所。 JSON でエンコードされた文字列、最大 4000 の長さ。 たとえば、[{\"address:null,coordinates\"\":null,displayName\"\":\"Harry\'s Bar,locationEmailAddress\"\"\":null,locationType\"\":default,locationUri\"\"\":\"null,uniqueId\"\":\"Harry\'s Bar,uniqueIdType\"\"\":\"private}\"\"|
|`m365_locations`|文字列|イベントを開催する場所、または参加者がいる場所。 location プロパティと locations プロパティは常に互いに一致します。 location プロパティを更新すると、locations コレクションに含まれる既存のすべての場所が削除されて、location の新しい値に置き換えられます。 JSON でエンコードされた文字列、最大 4000 の長さ。たとえば、[{\"address\":null,coordinates\"\":null,displayName\"\":\"Harry\'s Bar,locationEmailAddress\"\"\":null,locationType\":default,locationUri\"\"\"\":\"null,uniqueId\"\":\"2000\'\" Bar,uniqueIdType\"\":\"private\"}]|
|`m365_onlinemeeting`|文字列|参加者がオンラインで会議に参加するための詳細。 既定値は null です。 読み取り専用。isOnlineMeeting プロパティと onlineMeetingProvider プロパティを設定して会議をオンラインで有効にすると、Microsoft Graph によって onlineMeeting が初期化されます。 設定すると、会議はオンラインのままで、isOnlineMeeting、onlineMeetingProvider、onlneMeeting プロパティを再度変更することはできません。 JSON でエンコードされた文字列、最大 4000 の長さ。たとえば{\"conferenceId\": \"String,joinUrl\"\"\": \"String,phones\"\"\": [{\"@odata.type\": \"microsoft.graph.phone\"}],\"quickDial\": \"String,tollFreeNumbers\"\"\": [\"String\"],\"tollNumber\": \"String}\"|
|`m365_onlinemeetingprovider`|文字列|参加者がオンラインで会議に参加するための詳細。 既定値は null です。 読み取り専用です。 isOnlineMeeting と `onlineMeetingProvider` プロパティをオンラインで会議を有効にするように設定すると、Microsoft Graph によって onlineMeeting が初期化されます。 設定すると、会議はオンラインで引き続き使用でき、isOnlineMeeting プロパティと `onlineMeetingProvider`onlneMeeting プロパティを再度変更することはできません。|
|`m365_onlinemeetingurl`|String|オンライン会議の URL。 このプロパティは、Outlook で開催者が Skype などのオンライン会議としてイベントを指定する場合にのみ設定します。 読み取り専用です。 オンライン会議に参加するための URL にアクセスするには、イベントのプロパティを使用して`onlineMeeting`公開されている URL を使用`joinUrl`します。 プロパティは `onlineMeetingUrl` 今後非推奨となる予定です。|
|`m365_organizer`|文字列|イベントの開催者。JSON でエンコードされた文字列、最大 4000 の長さ。 {\"emailAddress\":{\"@odata.type\":\"microsoft.graph.emailAddress\"}}|
|`m365_originalendtimezone`|String|イベントの作成時に設定された終了タイム ゾーン。 tzone://Microsoft/Custom の値は、従来のカスタム タイム ゾーンがデスクトップ Outlook で設定されたことを示します。|
|`m365_originalstart`|DateTime|定期的な系列の発生または例外として最初に作成されたイベントの開始時刻を表します。 このプロパティは、単一インスタンスのイベントには返されません。 日付と時刻の情報は ISO 8601 形式で表され、常に UTC で表されます。 たとえば、2014 年 1 月 1 日の午前 0 時の UTC は 2014-01-01T00:00:00Z です。|
|`m365_originalstarttimezone`|文字列|イベントが作成されたときに設定された開始タイム ゾーン。 tzone://Microsoft/Custom の値は、従来のカスタム タイム ゾーンがデスクトップ Outlook で設定されたことを示します。|
|`m365_recurrence`|文字列|イベントの繰り返しパターン。 JSON でエンコードされた文字列、最大 4000 の長さ。たとえば{\"pattern\":{\"dayOfMonth\":0,daysOfWeek\"\":[\"monday,wednesday,friday\"\"\"\"\"],\"firstDayOfWeek\":\"sunday,index\"\"\":\"first,interval\"\"\":1,month\"\":0,type\"\":\"weekly\"},\"range\":{\"startDate\":\"2017-08-14,endDate\"\"\":\"2018-08-14,\"\"numberOfOccurrences\":0,recurrenceTimeZone\"\":\"東部標準時\",\"type\":\"endDate\"}}|
|`m365_reminderminutesbeforestart`|Int32|アラーム通知を行う、イベント開始時間前の分数。|
|`m365_responserequested`|Boolean|既定値は true なので、開催者は招待者にイベントに返信するように求めます。|
|`m365_responsestatus`|文字列|イベント メッセージへの応答で送信される応答のタイプを識別します。 JSON でエンコードされた文字列、最大 4000 の長さ。{\"response\": \"String,time\"\"\": \"String (timestamp)\"}|
|`m365_sensitivity`|文字列|可能な値は、通常、個人、プライベート、機密です。|
|`m365_seriesmasterid`|String|対象イベントが定期的なアイテムの一部である場合、定期的なアイテムのマスター アイテムの ID。|
|`m365_showas`|String|表示するステータス。 使用可能な値は、空き、仮、ビジー、oof、workingElsewhere、不明です。|
|`m365_subject`|String|イベントの件名行のテキスト。 プライマリ参照列|
|`m365_transactionid`|文字列|クライアントが同じイベントの作成を再試行した場合に冗長な POST 操作を回避するために、サーバーのクライアント アプリによって指定されたカスタム識別子。 これは、ネットワーク接続が低いと、クライアントが以前のイベント作成要求に対するサーバーからの応答を受信する前にタイムアウトする場合に役立ちます。 イベントの作成時に設定 `transactionId` した後は、後続の更新で transactionId を変更することはできません。 このプロパティは、アプリで設定されている場合にのみ、応答ペイロードで返されます。 省略可能です。|
|`m365_type`|String|イベントの種類。 指定できる値は、singleInstance、occurrence、exception、seriesMaster です。 読み取り専用|
|`m365_weblink`|String|Web 上の Outlook でイベントを開く URL。 Outlook on the web、メールボックスにサインインしている場合は、ブラウザーでイベントを開きます。 それ以外の場合は、Outlook on the web はサインインするように求めます。 この URL には、iFrame 内からアクセスできません。|
|`m365_grapheventid`|Guid|グラフ イベントの一意の識別子。|
|`m365_groupid`|文字列|イベントが属するグループ ID。|

## <a name="graph-booking-appointment"></a>Graph Booking Appointment

* エンティティ名: m365_graphbookingappointment
* Graph リソース: [bookingAppointment リソースの種類](/graph/api/resources/bookingappointment)
* 並べ替えはサポートされていません。
* フィルター処理は、次の列でサポートされています。
  * m365_bookingbusinessID
  * m365_collaborationrootID
  * m365_customertimezone
  * m365_optoutofcustomeremail
  * m365_price
  * m365_pricetype
  * m365_serviceID
  * m365_servicename
* ページ分割はサポートされていません。

### <a name="attributes-for-graph-booking-appointment"></a>Graph Booking Appointment の属性

| Column  | Dataverse 型 | 詳細 |
|---|---|---|
| `m365_collaborationrootid`| 文字列| レコードが関連付けられているコラボレーション セッションのコラボレーション ルート ID。 レコードが複数のコラボレーション セッションに関連付けられている場合は、コンマで区切られた文字列として返されます。 この属性は、複数のレコードを取得するときに返されないことに注意してください。|
| `m365_graphbookingappointmentid` | Guid | グラフの予約予定の一意識別子。|
| `m365_bookingbusinessid` | 文字列 | 予定がスケジュールされている予約ビジネスの一意の識別子。|
| `m365_additionalinformation` | 文字列 | 予定が確認されたときに顧客に送信される追加情報。|
| `m365_customers` | 文字列| 予定の顧客プロパティが一覧表示されます。 予定には顧客情報の一覧が含まれており、各ユニットはその予定の一部である顧客のプロパティを示します。 Optional[{\"customerID\":\"d243c77b-f1ff-4615-a01f-1660b5cb0e79,customQuestionAnswers\"\"\":[],\"emailAddress\":\"jordanm@contoso.com,location\"\"\":{\"address\":{\"city\":\"\",\"countryOrRegion\":\"\",\"postalCode\":\"\",\"postOfficeBox,state\"\"\":,\"street\":\"\"\"\",\"type\" },\"coordinates\":{\"精度\",\"高度\"\"Accuracy\",緯度\",\"\"経度\" },displayName\":\"\",\"\"locationEmailAddress,locationType,locationUri\"\"\"\"\":\"\",\"uniqueID,uniqueIDType\"\"\" },\"name\":\"Jordan Miller,notes,phone,timeZone\"\"\"\"\"\"\",\"@odata.type:\"\"#microsoft.graph.bookingCustomerInformation\"}] |
| `m365_customertimezone` | 文字列 | 顧客のタイム ゾーン。 使用可能な値の一覧については、 [dateTimeTimeZone リソースの種類に](/graph/api/resources/datetimetimezone)関する記事を参照してください。 |
| `m365_duration` | 文字列 | ISO8601 形式で示される予定の長さ。|
| `m365_enddatetime` | DateTime | 予定が終了する日付、時刻、タイム ゾーン。|
| `m365_filledattendeescount` | Int32 | 予定の現在の顧客数。|
| `m365_id` | 文字列 | bookingAppointment の ID。 読み取り専用です。|
| `m365_islocationonline` | ブール型 | True は、予定がオンラインで保持されることを示します。 既定値は False です。|
| `m365_joinweburl` | 文字列 | 予定のオンライン会議の URL。|
| `m365_maximumattendeescount` | Int32 | 予定で許可される顧客の最大数。|
| `m365_optoutofcustomeremail` | ブール型 | True は、この予定の bookingCustomer がこの予定の確認を受け取りたくないことを示します。|
| `m365_postbuffer` | 文字列 | 例として、予定が終了した後に予約する時間 (クリーンアップ用) を指定します。 値は ISO8601 形式で表されます。|
| `m365_prebuffer` | 文字列 | 準備のために、予定が開始される前に予約する時間を例に示します。 値は ISO8601 形式で表されます。|
| `m365_price` | DecimalType | 指定した bookingService の予定の通常価格。|
| `m365_pricetype` | 文字列 | サービスの価格構造に柔軟性を提供する設定。 指定できる値は、未定義、fixedPrice、startingAt、hourly、free、priceVaries、callUs、notSet です。|
| `m365_reminders` | 文字列 | この予定に対して送信された顧客のリマインダーのコレクション。 このプロパティの値は、ID によってこの bookingAppointment を読み取る場合にのみ使用できます。 [{\"message\":\"We 楽しみにしています!\",\"offset\":\"P1D,recipients\"\"\":\"customer\"},{\"message\":\"Reminder you have an appointment!\",\"offset\":\"P1D,recipients\"\"\":\"staff\"}] |
| `m365_selfserviceappointmentid` | 文字列 | 予定の別の追跡 ID。顧客に代わってスタッフが作成した場合とは対照的に、スケジュール 設定ページで顧客が直接作成した場合。|
| `m365_serviceid` | 文字列 | この予定に関連付けられている bookingService の ID。|
| `m365_servicelocation` | 文字列 | サービスが配信される場所。 {\"address\":{\"city\":\"\",\"countryOrRegion\":\"\",\"postalCode\":\"\",\"postOfficeBox,state\"\"\":\"\",\"street\":\"\",\"type\" },\"coordinates\":{\"精度\",\"高度\",\"高度Accuracy,latitude\"\",\"\"経度\"},\"displayName\":\"Our office address,locationEmailAddress\"\"\",\"locationType,locationUri\"\"\":\"\",\"uniqueID,uniqueIDType\"\"\" } |
| `m365_servicename` | 文字列 | この予定に関連付けられている bookingService の名前。 このプロパティは、新しい予定を作成するときに省略可能です。 指定しない場合は、予定に関連付けられているサービスから serviceID プロパティによって計算されます。 |
| `m365_servicenotes` |文字列 | bookingStaffMember からのメモ。 このプロパティの値は、ID でこの bookingAppointment を読み取る場合にのみ使用できます。|
| `m365_smsnotificationsenabled` | ブール型 | True は、SMS 通知が予定の顧客に送信されることを示します。 既定値は False です。|
| `m365_staffmemberids` | 文字列 | この予定でスケジュールされている各 bookingStaffMember の ID。 コンマ区切り文字列として格納されます。[\"string\"] |
| `m365_startdatetime` | DateTime | 予定が開始される日付、時刻、タイム ゾーン。|

## <a name="graph-drive"></a>Graph Drive

* エンティティ名: m365_graphdrive
* Graph リソース: [ドライブ リソースの種類](/graph/api/resources/drive)
* 並べ替えはサポートされていません。
* フィルター処理はサポートされていません。
* サーバー駆動型の改ページネーションがサポートされています。

### <a name="attributes-for-graph-drive"></a>Graph Drive の属性

|Column |Dataverse 型 |詳細 |
|---|---|---|
|`m365_collaborationrootid` |文字列 | レコードが関連付けられているコラボレーション セッションのコラボレーション ルート ID。 レコードが複数のコラボレーション セッションに関連付けられている場合は、コンマで区切られた文字列として返されます。 この属性は、複数のレコードを取得するときに返されないことに注意してください。 |
|`m365_createdby` |文字列 |アイテムを作成したユーザー、デバイス、またはアプリケーションの ID。 読み取り専用です。 この属性は JSON でエンコードされた文字列です。たとえば{ "user": { "displayName": "System Account" } |
|`m365_createddatetime` |DateTime |アイテム作成の日時。 読み取り専用です。 |
|`m365_description` |String |ユーザーに表示されるドライブの説明を提供します。 読み取り専用です。 |
|`m365_drivetype` |文字列 |このリソースで表されるドライブの種類についての説明。 OneDrive 個人用ドライブは個人用を返します。 OneDrive for Businessはビジネスを返します。 SharePoint ドキュメント ライブラリは documentLibrary を返します。 読み取り専用です。 |
|`m365_graphdriveid` |Guid |グラフ ドライブの一意識別子。 |
|`m365_id` |文字列 |ドライブの一意の識別子。 読み取り専用です。 |
|`m365_lastmodifiedby` | 文字列 |項目を最後に変更したユーザー、デバイス、およびアプリケーションの ID。 読み取り専用です。 この属性は、例: { "user": { "email": "user@contoso.com"、 "ID": "61de164e-21ff-4b1c-8cbd-77ac440894f8"、 "displayName": "User Name" } |
|`m365_lastmodifieddatetime` |DateTime |アイテムが最後に変更された日時。 読み取り専用です。|
|`m365_name` |文字列 |アイテムの名前。 読み取り専用です。 |
|`m365_owner` |String |省略可能。 ドライブを所有しているユーザー アカウント。 読み取り専用です。 この属性は JSON でエンコードされた文字列です。 たとえば{ "group": { "ID": "76c7286f-8645-4ba8-bc0f-c65a16424aaa", "displayName": "Group Name" }} |
|`m365_quota` |String |省略可能。 ドライブの記憶領域クォータに関する情報。 読み取り専用です。 この属性は JSON でエンコードされた文字列です。 たとえば{"deleted": 482586、"remaining": 27487788645969、"state": "normal"、"total":27487790694400、"used": 1565845 } |
|`m365_sharepointids` |文字列 |SharePoint REST の互換性に役立つ識別子を返します。 読み取り専用です。 このプロパティは既定では返されないため、$selectクエリ パラメーターを使用して選択する必要があります。 この属性は JSON でエンコードされた文字列です。 たとえば、"sharePointID": { "listID": "29d8457a-8e26-4291-9901-09718a38aaa", "siteID": "93618739-b3ca-4107-a77c-fba278c48a", "siteUrl": "<https://contoso.sharepoint.com>", "tenantID": "53986071-de92-43ad-a41f-f3c4adb2beef", "webID": "a0d0e9ec-e547-4338-92d9-4c2c62e5beef" } |
| `m365_siteid` |文字列 |ドキュメント ライブラリを含むサイトの識別子。
|`m365_system` |文字列 |存在する場合は、これがシステム管理のドライブであることを示しています。 読み取り専用です。
|`m365_weburl` |文字列 |ブラウザーでリソースを表示するための URL。 読み取り専用です。

### <a name="graph-drive-item"></a>Graph Drive アイテム

* エンティティ名: m365_graphdriveitem
* Graph リソース: [driveItem リソースの種類](/graph/api/resources/driveitem)
* 並べ替えは、次の列でサポートされています。
  * m365_name
* フィルター処理は、次の列でサポートされています。
  * m365_name
* サーバー駆動型の改ページネーションがサポートされています。

### <a name="attributes-for-graph-drive-item"></a>Graph Drive アイテムの属性

|Column |Dataverse 型 |詳細 |
|---|---|---|
|`m365_audio` |文字列 |オーディオのメタデータ (アイテムがオーディオ ファイルである場合)。 読み取り専用です。 OneDrive 個人用においてのみ。 この属性は JSON でエンコードされた文字列です。 { "album": "string", "albumArtist": "string", artist": "string", ビットレート": 128, "composers": "string", copyright": "string", "disc": 0, "discCount": 0, "duration": 567, "genre": "string", "hasDrm": false, "isVariableBitrate": false, "isVariableBitrate": false, "title": "string", "track": 1, "trackCount": 16, "year": 2014 }|
|`M365_bundle` |文字列 |バンドル メタデータ (アイテムがバンドルである場合)。 読み取り専用です。 この属性は JSON でエンコードされた文字列です。 たとえば、 { "childCount": 3, "album": { "@odata.type": "microsoft.graph.album" }, } |
|`m365_collaborationrootid` |文字列 |レコードが関連付けられているコラボレーション セッションのコラボレーション ルート ID。 レコードが複数のコラボレーション セッションに関連付けられている場合は、コンマで区切られた文字列として返されます。 この属性は、複数のレコードを取得するときに返されないことに注意してください。 |
|`m365_copy` |文字列 |要求に存在する場合は、コピー操作が実行されます。 |
|`m365_createdby` |文字列 |アイテムを作成したユーザー、デバイス、およびアプリケーションの ID。 読み取り専用です。 この属性は JSON でエンコードされた文字列です。 たとえば、{"user":{"displayName":"User Name","email":"alias@contoso.com","ID":"a298b975-3493-4d9e-b2d4-3cad78f00000"},"group": null,"application","device" } |
|`m365_createddatetime` |DateTime |アイテム作成の日時。 読み取り専用です。 |
|`m365_ctag` |文字列 |アイテムのコンテンツの eTag。 メタデータのみが変更された場合、この eTag は変更されません。 メモ:この記事は、SPFx GA バージョンではまだ検証されていません。 アイテムがフォルダーの場合、このプロパティは返されません。 読み取り専用です。 |
|`m365_deleted` |文字列 |アイテムの削除状態に関する情報。 読み取り専用です。 この属性は JSON でエンコードされた文字列です。 たとえば、 { "state": "string" } |
|`m365_description` |文字列 |ユーザーに表示されるアイテムの説明を提供します。 読み取り/書き込み。 OneDrive 個人用においてのみ。 |
|`m365_driveid` |文字列 |ドライブ項目を含むドライブの識別子。|
|`m365_etag` |文字列 |アイテム全体 (メタデータおよびコンテンツ) の eTag。 読み取り専用です。 |
| `m365_file` |文字列 |ファイルのメタデータ (アイテムがファイルである場合)。 読み取り専用です。 この属性は JSON でエンコードされた文字列です。 たとえば、{"hashes":{"crc32Hash","quickXorHash":"Biuzvwdu+Tmu6yRefayD27hD9vD=","sha1Hash","sha256Hash" },"mimeType":"application/vnd.openxmlformats-officedocument.wordprocessingml.document","processingMetadata" } |
| `m365_filesysteminfo` |文字列 |クライアント上のファイル システム情報。 この属性は JSON でエンコードされた文字列です。 たとえば、{"createdDateTime":"2022-07-21T15:02:47+00:00"、"lastAccessedDateTime"、"lastModifiedDateTime":"2022-07-21T15:02:55+00:00"} |
|`m365_folder` |文字列 | フォルダーのメタデータ (アイテムがフォルダーである場合)。 読み取り専用です。 この属性は JSON でエンコードされた文字列です。 たとえば、{"childCount":0,"view" } |
|`m365_graphdriveitemid` |Guid |グラフ ドライブ項目の一意識別子。 |
|`m365_id` |文字列 |ドライブ内のアイテムの一意の識別子。 読み取り専用です。 |
|`m365_image` |文字列 |画像のメタデータ (アイテムが画像である場合)。 読み取り専用です。 この属性は JSON でエンコードされた文字列です。 たとえば、{"height","width" } |
|`m365_lastmodifiedby` |文字列 |項目を最後に変更したユーザー、デバイス、およびアプリケーションの ID。 読み取り専用です。 この属性は JSON でエンコードされた文字列です。 たとえば、{"user":{"displayName":"User Name","email":"alias@contoso.com","ID":"a298b975-3493-4d9e-b2d4-3cad78f9a00e"},"group","application","device" } |
|`m365_lastmodifieddatetime` |DateTime |アイテムが最後に変更された日時。 読み取り専用です。 |
|`m365_location` |文字列 |場所のメタデータ (アイテムに場所データが含まれている場合)。 読み取り専用です。 この属性は JSON でエンコードされた文字列です。 たとえば、"location": { "高度": 1.0、"latitude": 1.0、"経度": 1.0 } |
|`m365_malware` |文字列 |アイテムにマルウェアが含まれていることが検出された場合のマルウェア メタデータ。 読み取り専用。 この属性は JSON でエンコードされた文字列です。 たとえば、 { "description": "string" } |
|`m365_name` |文字列 |アイテムの名前 (ファイル名と拡張子)。 読み取り/書き込み。 |
|`m365_package` |文字列 |これがある場合、アイテムはフォルダーやファイルではなく、パッケージです。 パッケージは、コンテキスト次第で、ファイルとして、あるいはフォルダーとして扱われます。 読み取り専用です。 この属性は JSON でエンコードされた文字列です。 たとえば、 { "type": "oneNote" } |
|`m365_parentreference` |文字列 |親の情報 (アイテムに親がある場合)。 この属性は JSON でエンコードされた文字列です。 たとえば、 {"driveID":"b!qgK-8nOzX0qISvfGCiC2Smbv0m0RlNhDvQNDZsCMpbSnchFAhWAaQoiTLZcSo1gq","driveType":"documentLibrary","ID":"" 01EYDCV4YHV77FE3EDDFHIVD6QN2ETT3PP","name","path":"/drives/b!qgK-8nOzX0qISvfGCiC2Smbv0m0RlNhVQNDZsCMp bSnchFAhWAaQoiTLZcSo1no/root: /folder name","shareID","sharepointIDs":{"listID":"401172a8-6085-421a-8893-2d9712a35c3c","listItemID","listItemUniqueID":"52feaf12-836c-4e19-8a8f-d64e8939ee52","siteID":"f34e02aa-b373-4a5f-884a-f7c60a20b64a,"siteUrl":"https://contoso.sharepoint.com/sites/Contoso,"tenantID","webID":"6dd2ef66-9411-43d8-bcd4-0366c08ccabd"},"siteID" } |
|`m365_parentreferenceid` |文字列 |ドライブ項目の親であるドライブ項目の識別子。 |
|`m365_pendingoperations` |文字列 |存在する場合、driveItemの状態に影響する可能性のある1つまたは複数の操作が完了保留中であることを示します。 読み取り専用です。 この属性は JSON でエンコードされた文字列です。 たとえば、 { "pendingContentUpdate": {"@odata.type": "microsoft.graph.pendingContentUpdate"} } |
|`m365_photo` |文字列 |写真のメタデータ (アイテムが写真である場合)。 読み取り専用です。 この属性は JSON でエンコードされた文字列です。 たとえば、{ "cameraMake": "Camera Make"、"cameraModel": "Camera Model"、 "exposureDenominator": 10000000, "exposureNumerator": 41671, "focalLength": 4.38, "fNumber": 1.73, "iso": 70, "orientation": 6, "takenDateTime": "2020-04-29T14:17:39Z" } |
|`m365_publication` |文字列 |アイテムが公開されているか、チェックアウトの状態かどうかの情報を、そのような操作をサポートする場所で提供します。 このプロパティは既定では返されません。 読み取り専用です。 この属性は JSON でエンコードされた文字列です。 たとえば、{"level":"published","versionID":"2.0"} |
|`m365_remoteitem` |文字列 |リモート アイテムのデータ (現在アクセス中のドライブ以外のドライブから共有されているアイテムの場合)。 読み取り専用です。 この属性は JSON でエンコードされた文字列です。 たとえば、{ "ID": "string", "createdBy": { "@odata.type": "microsoft.graph.IdentitySet" }, "createdDateTime": "timestamp", "file": { "@odata.type": "microsoft.graph.file" }, "fileSystemInfo": { "@odata.type": "microsoft.graph.fileSystemInfo" }, "folder": { "@odata.type": "microsoft.graph.folder" }, "image": { "@odata.type": "microsoft.graph.image" }, "lastModifiedBy": { "@odata.type": "microsoft.graph.IdentitySet" }, "lastModifiedDateTime": "timestamp", "name": "string", "package": {@odata.type": "microsoft.graph.package" }, "parentReference": { "@odata.type": "microsoft.graph.itemReference" }, "shared": { "@odata.type": "microsoft.graph.shared" }, "sharepointIDs": { "@odata.type": "microsoft.graph.sharepointIDs" }, "specialFolder": { "@odata.type": "microsoft.graph.specialFolder" }, "size": 1024, "video": { "@odata.type": "microsoft.graph.video" }, "webDavUrl": "url", "webUrl": "url" } |
|`m365_root` |文字列 |このプロパティが null ではない場合は、driveItem がドライブで最上位の driveItem であることを示します。 |
|`m365_searchresult` |文字列 |検索のメタデータ (検索結果に由来するアイテムの場合)。 読み取り専用です。 この属性は JSON でエンコードされた文字列です。 たとえば、 { "onClickTelemetryUrl": "url" } |
|`m365_shared` |文字列 |アイテムが他のユーザーと共有されていることを示し、アイテムの共有状態に関する情報を提供します。 読み取り専用です。 この属性は JSON でエンコードされた文字列です。 たとえば、 { "scope": "users", "owner": { "user": { "displayName": "User Name", "ID": "bbbb6fa48aaaaaaa" } } } |
|`m365_sharepointids` |文字列 |SharePoint REST の互換性に役立つ識別子を返します。 読み取り専用です。 この属性は JSON でエンコードされた文字列です。 e.g{"listID":"401172a7-6085-421a-8893-2d9712a35aba","listItemID":"338""listItemUniqueID":"0edc89e5-24ea-4c6b-a019-dc51f45eeccc","siteID":"f2be02aa-b37 3-4a5f-884a-f7c60a20bddd","siteUrl":""https://contoso.sharepoint.com/sites/Contoso,"tenantID":"1c137272-0581-487f -b195-aeeb93cc4ccc","webID":"6dd2ef66-9411-43d8-bcd4-0366c08caaaa"} |
|`m365_siteid` |文字列 |ドキュメント ライブラリを含むサイトの識別子。 |
|`m365_size` |IntType |アイテムのサイズ (バイト単位)。 読み取り専用です。 |
|`m365_specialfolder` |文字列 |現在のアイテムが特別なフォルダーとしても使用可能な場合は、このファセットが返されます。 読み取り専用です。 この属性は JSON でエンコードされた文字列です。 たとえば、 { "name": "documents" } |
|`m365_thumbnail` |文字列 |要求に存在する場合は、ドライブアイテムのサムネイルが取得されます。 |
|`m365_video` |文字列 |現在のアイテムが特別なフォルダーとしても使用可能な場合は、このファセットが返されます。 読み取り専用です。 この属性は JSON でエンコードされた文字列です。 たとえば、{"ビットレート": 10646968、 "duration": 1050683, "height": 720, "width": 1280, "audioBitsPerSample": 16, "audioChannels": 1, "audioFormat": "PCM", "audioSamplesPerSecond": 32000, "fourCC": "H264", "frameRate": 60} |
|`m365_webdavurl` |String | アイテムの WebDAV 互換性のある URL。 |
|`m365_weburl` |文字列 |ブラウザーでリソースを表示するための URL。 読み取り専用です。 |
