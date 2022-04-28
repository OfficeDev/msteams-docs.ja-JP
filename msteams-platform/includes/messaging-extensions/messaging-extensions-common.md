## <a name="add-a-message-extension-to-your-app"></a>アプリにメッセージ拡張機能を追加する

メッセージ拡張機能は、ユーザーの要求をリッスンし、 [カード](~/task-modules-and-cards/what-are-cards.md)などの構造化データで応答するクラウドでホストされるサービスです。 Bot Framework `Activity` オブジェクトを使用して、サービスをMicrosoft Teamsと統合します。 Bot Builder SDK の .NET 拡張機能とNode.js拡張機能は、メッセージ拡張機能機能をアプリに追加するのに役立ちます。

![メッセージ拡張機能のメッセージ フローの図](~/assets/images/compose-extensions/ceflow.png)

### <a name="register-in-the-bot-framework"></a>Bot Framework に登録する

まだ行っていない場合は、まずボットをMicrosoft Bot Frameworkに登録する必要があります。 定義されているとおり、ボットの Microsoft アプリ ID とコールバック エンドポイントは、メッセージ拡張機能で使用され、ユーザー要求を受信して応答します。 ボットのMicrosoft Teams チャネルを有効にすることを忘れないでください。

ボット アプリ ID とアプリ パスワードを記録します。アプリ マニフェストでアプリ ID を指定する必要があります。

### <a name="update-your-app-manifest"></a>アプリ マニフェストを更新する

ボットとタブと同様に、アプリの [マニフェスト](~/resources/schema/manifest-schema.md#composeextensions) を更新して、メッセージ拡張機能のプロパティを含めます。 これらのプロパティは、Microsoft Teams クライアントでのメッセージ拡張機能の表示と動作を制御します。 メッセージ拡張機能は、マニフェストの v1.0 以降でサポートされています。

#### <a name="declare-your-message-extension"></a>メッセージ拡張機能を宣言する

メッセージ拡張機能を追加するには、プロパティを使用してマニフェストに新しい最上位レベルの JSON 構造を `composeExtensions` 含めます。 現時点では、アプリ用に 1 つのメッセージ拡張機能を作成することに制限されています。

> [!NOTE]
> マニフェストでは、メッセージ拡張機能 `composeExtensions`が . これは、下位互換性を維持するためです。

拡張機能定義は、次の構造を持つオブジェクトです。

| プロパティ名 | 用途 | 必須 |
|---|---|---|
| `botId` | Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。 これは通常、Teams アプリ全体の ID と同じである必要があります。 | はい |
| `scopes` | この拡張機能をスコープに追加できるかどうかを宣言する`personal``team`配列 (またはその両方)。 | はい |
| `canUpdateConfiguration` | **メニュー項目設定** 有効にします。 | いいえ |
| `commands` | このメッセージ拡張機能がサポートするコマンドの配列。 コマンドは 10 個に制限されています。 | はい |

#### <a name="define-commands"></a>コマンドを定義する

メッセージ拡張機能は 1 つのコマンドを宣言する必要があります。これは、ユーザーが作成ボックスの **[その他のオプション** ] (**&#8943;**) ボタンからアプリを選択したときに表示されます。

![Teamsのメッセージ拡張機能の一覧のスクリーンショット](~/assets/images/compose-extensions/compose-extension-list.png)

アプリ マニフェストでは、コマンド項目は次の構造を持つオブジェクトです。

| プロパティ名 | 用途 | 必須 | マニフェストの最小バージョン |
|---|---|---|---|
| `id` | このコマンドに割り当てる一意の ID。 ユーザー要求には、この ID が含まれます。 | はい | 1.0 |
| `title` | コマンド名。 この値は UI に表示されます。 | はい | 1.0 |
| `description` | このコマンドの動作を示すヘルプ テキスト。 この値は UI に表示されます。 | はい | 1.0 |
| `type` | コマンドの種類を設定します。 使用可能な値は、`query`、`action` です。 存在しない場合、既定値は `query`. | なし | 1.4 |
| `initialRun` | コマンドと共に使用される省略可能な `query` パラメーター。 **true** に設定すると、ユーザーが UI でこのコマンドを選択するとすぐに、このコマンドを実行する必要があることを示します。 | いいえ | 1.0 |
| `fetchTask` | コマンドと共に使用される省略可能な `action` パラメーター。 [タスク モジュール](~/task-modules-and-cards/what-are-task-modules.md)内に表示するアダプティブ カードまたは Web URL をフェッチするには **、true** に設定します。 これは、静的なパラメーター セットではなく、コマンドへの `action` 入力が動的な場合に使用されます。 if が **true** に設定されている場合、コマンドの静的パラメーター リストは無視されることに注意してください。 | なし | 1.4 |
| `parameters` | コマンドのパラメーターの静的リスト。 | はい | 1.0 |
| `parameter.name` | パラメーターの名前です。 これは、ユーザー要求でサービスに送信されます。 | はい | 1.0 |
| `parameter.description` | このパラメーターの目的または指定する必要がある値の例について説明します。 この値は UI に表示されます。 | はい | 1.0 |
| `parameter.title` | 短いわかりやすいパラメーターのタイトルまたはラベル。 | はい | 1.0 |
| `parameter.inputType` | 必要な入力の種類に設定します。 使用可能な値には`text`、, , `textarea`, `number`, `date`, `time``toggle`. 既定値は .`text` | なし | 1.4 |
| `context` | メッセージ アクションを使用できるコンテキストを定義する値の省略可能な配列。 指定できる値は `message`、、 `compose`、または `commandBox`. 既定値は `["compose", "commandBox"]` です。 | いいえ | 1.5 |
